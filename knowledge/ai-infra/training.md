# Model Training: Concepts and Techniques

Concise entries on training state, memory, numerical precision, model architecture, parameter-efficient fine-tuning, and learning-rate scheduling. Parallel execution is covered in [[knowledge/ai-infra/parallelism|Parallelism and state sharding]].

## I. Training State and Memory

### 1. Parameters

**Core idea: The learned values that define the model's transformations.**

Examples include embedding tables, attention projection weights (`W_Q`, `W_K`, `W_V`, `W_O`), MLP weights and biases, and normalization scales and biases where present. Input-dependent Q/K/V tensors are activations, not learned parameters. [[knowledge/ai-infra/parallelism#5. ZeRO-3|ZeRO-3]] shards parameter storage across data-parallel workers.

### 2. Gradients

**Core idea: Derivatives of the loss with respect to trainable parameters, used to compute updates.**

Backward propagation computes `g_i = ∂loss / ∂θ_i`. In dense full-parameter training, each parameter has a corresponding gradient element; its storage precision need not match the parameter's precision. [[knowledge/ai-infra/training#4. Gradient Accumulation|Gradient accumulation]] combines gradients across microbatches before an update. [[knowledge/ai-infra/parallelism#4. ZeRO-2|ZeRO-2]] shards the reduced gradients retained for updates. [Source: PyTorch DDP tutorial](https://docs.pytorch.org/tutorials/intermediate/ddp_tutorial.html).

### 3. Optimizer State

**Core idea: Persistent update information, such as Adam's moving averages of gradients and squared gradients.**

Adam maintains a first moment `m` and a second moment `v` per parameter. Mixed-precision training may also keep FP32 master weights for accurate updates; [[knowledge/ai-infra/parallelism#2. ZeRO|ZeRO]]'s accounting includes these in optimizer state. [[knowledge/ai-infra/parallelism#3. ZeRO-1|ZeRO-1]] shards this state across data-parallel workers. [Source: DeepSpeed ZeRO documentation](https://deepspeed.readthedocs.io/en/latest/zero3.html).

**Memory example — mixed-precision Adam, before sharding.** Assume all parameters are trainable, with FP16 compute weights and gradients, plus FP32 master weights and Adam moments. The percentages below cover model state only.

| Component | Bytes per parameter | Share of model-state memory |
| --- | ---: | ---: |
| FP16 compute parameter | 2 | 12.5% |
| FP16 gradient | 2 | 12.5% |
| FP32 master parameter (optimizer state) | 4 | 25% |
| FP32 first moment `m` (optimizer state) | 4 | 25% |
| FP32 second moment `v` (optimizer state) | 4 | 25% |
| **Total** | **16** | **100%** |

In ZeRO's three categories, this is **2 bytes of parameters + 2 bytes of gradients + 12 bytes of optimizer state** per parameter. Thus, optimizer state accounts for 75% in this example. One billion parameters require about 16 GB (decimal) for these states per unsharded DP replica. [Source: ZeRO, Section 3.1](https://arxiv.org/html/1910.02054v3).

Total training memory also includes saved activations, operator workspaces, communication/gather buffers, and allocator overhead. Activations can be substantial, especially with long sequences or large microbatches. The 75% figure is not a share of total GPU memory; different precisions, optimizers, and master-weight policies change the accounting. [Source: ZeRO, Section 3.2](https://arxiv.org/html/1910.02054v3).

### 4. Gradient Accumulation

**Core idea: Accumulate gradients over multiple microbatches before updating parameters once.**

Each [[knowledge/ai-infra/parallelism#1. Microbatch|microbatch]] runs forward and backward using unchanged parameters. Its gradients accumulate in gradient buffers; after the configured number of microbatches, the optimizer updates parameters once, then gradients are cleared for the next accumulation window. Adam's moment estimates persist across updates.

For equal-sized microbatches and synchronized data-parallel replicas:

`effective global batch size = microbatch size per replica × accumulation steps × DP degree`

For example, 16 samples per microbatch × 4 accumulation steps × 2 DP replicas gives 128 samples per optimizer update. TP and PP degrees do not multiply the sample count. Loss or gradient scaling must produce the intended batch average; unequal microbatch sizes or valid-token counts require appropriate weighting.

This permits a larger effective batch without processing all samples simultaneously. It does not remove parameter or optimizer-state memory, and increasing the effective batch changes update frequency. In GPipe, gradients from the pipeline's microbatches accumulate before a synchronous update. [Sources: PyTorch DDP tutorial](https://docs.pytorch.org/tutorials/intermediate/ddp_tutorial.html); [GPipe](https://arxiv.org/abs/1811.06965).

## II. Numerical Precision and Stability

Exponent bits determine the available magnitude range; fraction bits determine significand precision. The counts below exclude the implicit leading bit of normal values.

| Format | Sign bits | Exponent bits | Fraction bits |
| --- | ---: | ---: | ---: |
| FP32 | 1 | 8 | 23 |
| FP16 | 1 | 5 | 10 |
| BF16 | 1 | 8 | 7 |

[Sources: NVIDIA floating-point formats](https://docs.nvidia.com/deeplearning/transformer-engine-releases/release-2.19/features/low_precision_training/introduction/introduction.html); [NVIDIA mixed-precision guide](https://docs.nvidia.com/deeplearning/performance/mixed-precision-training/index.html#half-precision-format).

### 1. FP16

Uses 16 bits with a narrower exponent range than FP32. Its maximum finite value is 65,504 and its smallest positive subnormal is approximately `5.96e-8`. Small gradients can round to zero, while large values can overflow. [[knowledge/ai-infra/training#4. Loss Scaling|Loss scaling]] helps preserve small gradients during backward computation. [Source: NVIDIA half-precision format](https://docs.nvidia.com/deeplearning/performance/mixed-precision-training/index.html#half-precision-format).

### 2. BF16

Uses the same 8-bit exponent field as FP32, giving a comparable magnitude range, but only 7 fraction bits. This makes range-related overflow and underflow less likely than FP16, so BF16 training usually does not require loss scaling. Its significand precision is lower than FP16's; rounding errors and overflow remain possible. [Source: NVIDIA precision overview](https://docs.nvidia.com/deeplearning/transformer-engine-releases/release-2.19/features/low_precision_training/introduction/introduction.html).

### 3. Mixed-Precision Training

Uses formats such as FP16 or BF16 for suitable operations while retaining higher precision where needed, including sensitive reductions, accumulation, or parameter updates. Tensor storage, computation, and accumulation precision can differ. The [[knowledge/ai-infra/training#3. Optimizer State|FP32 master-weight example]] is one configuration, not a requirement for every mixed-precision implementation. [Source: NVIDIA mixed-precision training](https://docs.nvidia.com/deeplearning/performance/mixed-precision-training/index.html).

### 4. Loss Scaling

Multiplies the loss by a factor `S` before backward propagation. By the chain rule, the resulting gradients are also scaled:

$$
L' = S L, \qquad g' = \nabla_\theta L' = S g.
$$

Unscale gradients with sufficient precision before clipping and parameter updates, restoring their intended magnitude. For example, `g = 1e-8` can round to zero in FP16, while `S = 65536` shifts it to approximately `6.55e-4`. Scaling must protect the backward computation itself; multiplying an already-underflowed zero cannot recover it. This preserves gradient range rather than intentionally increasing the learning rate. [Sources: NVIDIA loss scaling](https://docs.nvidia.com/deeplearning/performance/mixed-precision-training/index.html#loss-scaling-to-preserve-small-gradient-magnitudes); [PyTorch gradient scaling](https://docs.pytorch.org/docs/stable/amp.html#gradient-scaling).

### 5. Dynamic Loss Scaling

Adjusts `S` during training. If gradients contain Inf/NaN, skip that optimizer update and reduce the scale; after enough finite steps, increase it. This balances preserving small gradients against overflow from excessive scaling. It does not repair arbitrary forward-pass numerical problems. [Source: PyTorch GradScaler](https://docs.pytorch.org/docs/stable/amp.html#torch.amp.GradScaler).

## III. Model Architecture

### 1. Mixture of Experts (MoE)

Replaces selected Transformer FFN sublayers with multiple expert FFNs having distinct learned weights. A router selects a small subset for each token, often top-k, and combines their outputs. Experts need not use different code or architectures. Shared attention and other shared components still run; some designs also have always-active shared experts. Sparse routing increases parameter capacity without executing every expert for every token. [Source: Switch Transformers](https://arxiv.org/abs/2101.03961).

For example, top-2 routing among eight equal-sized experts executes two expert FFNs per token. Different tokens can select different experts, so a batch may exercise all eight. Relative to evaluating all eight experts per token, expert computation is reduced; relative to one dense FFN of the same expert size, top-2 can require more computation. Routing, token dispatch, and load imbalance also affect runtime. [Source: Megatron MoE routing and dispatch](https://docs.nvidia.com/megatron-core/developer-guide/latest/user-guide/features/moe.html).

### 2. Activated Parameter Count

Counts the weights used for one token's computation, including shared components and selected experts. **Activated parameters are weights, not intermediate activation tensors.** Total parameter count includes all experts and shared weights; per-token activated count covers only the executed subset. These affect resources differently:

| Resource | Main considerations |
| --- | --- |
| Resident weight memory | All resident weights count. With all weights GPU-resident, the GPU group must hold the total model, potentially sharded across devices; quantization and offloading change the requirement. |
| Per-token computation | Depends on executed components and token/context shapes, plus routing and communication overhead. Activated count alone does not determine latency. |
| Activation memory | Depends on token count, expert width, top-k, saved tensors, padding, and dispatch buffers. It does not automatically shrink in proportion to activated/total parameters. |

Experts placed on different GPUs require token exchange, often [[knowledge/ai-infra/parallelism#8. All-to-All|All-to-All]]. Inactive experts for one token can still be needed by other tokens in the same batch. [Sources: Switch Transformers](https://arxiv.org/abs/2101.03961); [Megatron MoE](https://docs.nvidia.com/megatron-core/developer-guide/latest/user-guide/features/moe.html).

### 3. SwiGLU Feed-Forward Network

Applies a nonlinear, token-wise transformation between attention sublayers. For column-vector input `x` with hidden dimension `H`, two projections independently map the same input to an intermediate dimension `D`:

$$
u = W_{\mathrm{up}}x, \qquad
g = \operatorname{SiLU}(W_{\mathrm{gate}}x), \qquad
y = W_{\mathrm{down}}(g \odot u).
$$

Here `SiLU(z) = z * sigmoid(z)` and `odot` denotes elementwise multiplication. Biases, normalization, and the residual connection are omitted. The projections have distinct roles:

| Projection | Dimensions | Role |
| --- | --- | --- |
| Up | `H -> D` | Produces a wider set of learned features; expansion alone remains linear and does not create new input information. |
| Gate | `H -> D` | Produces input-dependent modulation values after SiLU; the product with the up branch introduces nonlinear feature interactions. |
| Down | `D -> H` | Learns how to combine the intermediate features into the hidden dimension expected by the residual stream; this is not simple truncation. |

For example, `H = 4096` and `D = 11008` give two `4096 -> 11008` branches and one `11008 -> 4096` projection. Each token follows both branches. SwiGLU gating continuously modulates feature values, rather than selecting a subset of experts as an MoE router does; SiLU gate values are not restricted to `[0, 1]`. The same FFN weights apply independently at each token position. [Sources: GLU Variants Improve Transformer](https://arxiv.org/abs/2002.05202); [Llama dimensions](https://huggingface.co/docs/transformers/en/model_doc/llama#transformers.LlamaConfig).

## IV. Parameter-Efficient Fine-Tuning

### 1. Low-Rank Adaptation (LoRA)

Freezes the pretrained model and adds trainable low-rank updates to selected weight matrices, such as attention projections or MLP linear layers. For column-vector input `x` and frozen weight `W_0` of shape `[d_out, d_in]`:

$$
y = W_0 x + s B A x, \qquad
A \in \mathbb{R}^{r \times d_{\mathrm{in}}}, \quad
B \in \mathbb{R}^{d_{\mathrm{out}} \times r}.
$$

Here `r` is a small rank and `s` is a scaling factor, conventionally `alpha/r` in standard LoRA. Training updates `A` and `B` while keeping `W_0` fixed. The low-rank restriction applies to the learned update `sBA`; the pretrained weight itself need not be low-rank. The method uses the empirical observation that useful task-adaptation updates can often be represented with low rank, rather than guaranteeing equivalence to full fine-tuning. [Source: LoRA, Section 4](https://arxiv.org/html/2106.09685v2#S4).

The update obeys the rank bound:

$$
\operatorname{rank}(BA) \leq \min\bigl(\operatorname{rank}(B), \operatorname{rank}(A)\bigr) \leq r.
$$

Thus, `r = 8` caps the update rank at eight; its actual rank can be lower. The sum `W_0 + sBA` can still be full-rank because this constraint applies only to the update.

For one `4096 × 4096` matrix, full fine-tuning updates 16,777,216 weights. With `r = 8`, LoRA trains `8 × 4096 + 4096 × 8 = 65,536` weights, about 0.39% of that layer's original count. This is an illustrative layer-level comparison, not a whole-model memory ratio.

Frozen base weights need no parameter gradients or optimizer states, but still occupy memory; activations and backward computation needed to train the adapters remain. For a fixed adapter and compatible weights, merge `W_merged = W_0 + sBA` for inference, eliminating the separate low-rank branch. Keeping adapters separate instead allows task switching over a shared base model, with runtime overhead depending on implementation. [Sources: LoRA](https://arxiv.org/abs/2106.09685); [PEFT LoRA guide](https://huggingface.co/docs/peft/main/en/conceptual_guides/lora).

### 2. LoRA Target Modules

A Transformer block contains multiple learned linear projections. Only selected targets receive LoRA branches. Each selected projection normally has its own `A` and `B`, including separate copies at different block depths; configuring the same rank does not share those weights. Other modules retain their original computation. Common names in Llama-style implementations are:

| Location | Example module names | Role |
| --- | --- | --- |
| Attention inputs | `q_proj`, `k_proj`, `v_proj` | Project hidden states into queries, keys, and values. |
| Attention output | `o_proj` | Project concatenated attention-head outputs back to the hidden dimension. |
| SwiGLU FFN expansion | `up_proj`, `gate_proj` | Produce expanded features and the branch used for activation/gating. |
| FFN contraction | `down_proj` | Project the combined intermediate features back to the hidden dimension. |
| Final vocabulary projection | `lm_head` | Map final hidden states to vocabulary logits, as in [[knowledge/ai-infra/inference#4. Autoregressive Token Generation|token generation]]. |

The [[knowledge/ai-infra/training#3. SwiGLU Feed-Forward Network|SwiGLU FFN]] as a whole is nonlinear; LoRA targets its linear projections. Other architectures may use two FFN projections or fuse Q/K/V, so module names and shapes vary. With GQA/MQA, K/V projections can be narrower than Q. [Sources: Llama architecture](https://arxiv.org/abs/2302.13971); [[knowledge/ai-infra/inference#2. Grouped-Query Attention (GQA)|GQA]]; [LoRA projection choices, Section 4.2](https://arxiv.org/html/2106.09685v2#S4.SS2).

Target selection is configurable: one can adapt only Q/V or include other attention and FFN projections. PEFT's `target_modules` specifies these choices; its documented `all-linear` option excludes the output layer for Transformers `PreTrainedModel`s, so the LM head should not be assumed to be adapted automatically. [Source: PEFT LoRA configuration](https://huggingface.co/docs/peft/main/package_reference/lora).

In standard LoRA, targets and rank are configured before training. Gradient descent learns the selected modules' `A` and `B` values; it does not choose which modules receive adapters. For example:

```python
from peft import LoraConfig

config = LoraConfig(r=8, target_modules=["q_proj", "v_proj"])
```

This targets matching Q/V modules across the model, with independent rank-8 updates. `layers_to_transform` can restrict the block indices. If targets are omitted, supported architectures may use a predefined framework mapping; that is a setup-time rule, not a learned routing decision. [Source: PEFT LoraConfig](https://huggingface.co/docs/peft/main/package_reference/lora#peft.LoraConfig).

### 3. Quantized LoRA (QLoRA)

Combines [[knowledge/ai-infra/training#1. Low-Rank Adaptation (LoRA)|LoRA]] with a frozen, quantized base model. Standard 16-bit LoRA stores base weights in FP16/BF16; QLoRA stores them primarily in 4-bit form while training floating-point adapters. Conceptually:

$$
y = \operatorname{dequant}(Q(W_0))x + sBAx.
$$

Storage precision differs from computation precision: the original method dequantizes weights to BF16 for forward and backward matrix multiplications. Backpropagation still passes through frozen base layers to train adapters; the base weights receive no updates. Dequantization reconstructs approximate values, not the exact original weights. [Source: QLoRA, Section 3](https://arxiv.org/html/2305.14314v1#S3).

NF4 codes and block scales encode approximate weight values; dequantization decodes these values into the floating-point format used by the matrix multiplication. If `W_hat = dequant(Q(W_0))`, computing with BF16 does not remove the quantization error `W_hat - W_0`. It allows multiplication with floating-point activations using suitable hardware kernels and avoids forcing activations and intermediate results into the same 4-bit format. Operation and accumulation precision are separate choices. Direct low-bit matrix multiplication is possible with compatible formats and kernels, but NF4 weight storage alone does not make QLoRA a fully 4-bit computation pipeline.

Integer matrix multiplication is valid in quantized computation, with appropriate scaling and other corrections. NF4 codes, however, index nonuniform codebook values; treating those codes as ordinary integer weights would compute a different function. Decoding can be fused into a multiplication kernel rather than materializing a separate floating-point copy of the entire model. The relevant constraint is the representation and the chosen kernel's supported operation, rather than a universal inability of hardware to mix integer and floating-point inputs.

The paper combines NF4, a nonuniform 4-bit format designed for normally distributed weights; double quantization of the quantization constants; and paged optimizers using CPU/GPU unified memory to handle memory spikes. Actual paging depends on memory pressure. [Source: QLoRA](https://arxiv.org/abs/2305.14314).

Ideally, 16-to-4-bit compression quarters the base-weight payload. Total training memory falls by a smaller, workload-dependent ratio because quantization metadata, unquantized modules, adapters, optimizer state, activations, and temporary buffers remain.

Lower memory use does not guarantee higher throughput. Dequantization and kernel overhead can make a QLoRA implementation slower than 16-bit LoRA. Checkpointing or actual CPU/GPU paging can add costs if enabled or triggered. These are possible explanations for an observed slowdown, not a diagnosis without profiling. Check `bnb_4bit_compute_dtype`: the documented bitsandbytes default is FP32; BF16 can improve speed on supported hardware. [Source: Transformers bitsandbytes guide](https://huggingface.co/docs/transformers/en/quantization/bitsandbytes#compute-data-type).

For a controlled comparison, match model, adapter targets/rank, sequence lengths, token count, microbatch and gradient accumulation, checkpointing, and compute dtype; compare steady-state tokens/s and peak memory separately from loading/initial quantization time. Quantization introduces approximation error, so validate task quality as well.

### 4. Adapter Precision

LoRA and QLoRA do not prescribe a universal adapter dtype. Both train floating-point `A` and `B`; QLoRA's 4-bit storage applies to the frozen base, not automatically to the adapters. The original QLoRA formulation uses BF16 adapters, whereas PEFT currently defaults to FP32 adapter weights and promotes FP16/BF16 adapters where appropriate. Explicit configuration and framework versions can change this behavior. [Sources: QLoRA, Section 3](https://arxiv.org/html/2305.14314v1#S3); [PEFT adapter dtype guide](https://huggingface.co/docs/peft/en/developer_guides/troubleshooting#selecting-the-dtype-of-the-adapter).

Distinguish parameter storage, operation dtype under mixed precision, and optimizer-state dtype. FP32 adapter parameters can participate in BF16/FP16 operations under autocast; enabling mixed precision does not by itself establish parameter or saved-checkpoint dtype. Optimizer states follow the optimizer implementation and configuration. Inspect tensors directly:

```python
for name, param in model.named_parameters():
    if "lora_A" in name or "lora_B" in name:
        print(name, param.dtype)
```

A checkpoint's adapter tensor dtypes determine its stored precision; saving or loading with conversion can change them. Neither method's name fixes the resulting artifact to 16-bit or 32-bit.

## V. Learning-Rate Scheduling

### 1. Learning-Rate Scheduler

A learning rate is a hyperparameter, but it need not be constant throughout training. A scheduler automatically sets the current learning rate using a configured rule, commonly indexed by optimizer-update step. For warmup followed by decay, setup-time hyperparameters include the peak learning rate, warmup duration, total update count, decay shape, and any final learning rate. The current value changes according to that rule; the user does not need to adjust it manually at every step. This scheduling is separate from learning model parameters through gradient descent.

For example, a simplified linear schedule can increase from near zero to a peak of `1e-4` over 100 optimizer updates, then decrease toward zero by update 1,000. Exact endpoint conventions depend on the scheduler. The original Transformer similarly configures a time-varying learning-rate formula with a fixed warmup duration. [Source: Attention Is All You Need, Section 5.3](https://arxiv.org/html/1706.03762v7#S5.SS3).

### 2. Learning-Rate Warmup

Starts with a small learning rate and gradually increases it to a target value over an initial training interval. Its main purpose is to stabilize early updates: large initial gradients or large adaptive-optimizer update terms can otherwise cause loss spikes or divergence. For Adam, this startup behavior relates to its evolving [[knowledge/ai-infra/training#3. Optimizer State|moment estimates]]; warmup limits update magnitudes during that phase. This is not primarily a strategy for escaping local minima or finding a global optimum. [Source: On the Adequacy of Untuned Warmup for Adaptive Optimization](https://arxiv.org/abs/1910.04209).

The need and duration depend on architecture, optimizer, and training setup. For example, analysis of the original Post-LN Transformer identifies large initial gradients near its output layers, while Pre-LN changes that behavior; warmup is not universally required. [Source: On Layer Normalization in the Transformer Architecture](https://arxiv.org/abs/2002.04745).

### 3. Learning-Rate Decay

Reduces the learning rate later in training, allowing finer updates and reducing overshooting or noise-driven fluctuations as optimization progresses. This supports the intuition of taking smaller steps near a useful low-loss region; it does not establish proximity to a global optimum. Excessively early or aggressive decay can also slow progress.

A schedule can combine warmup and decay: the original Transformer uses linear warmup followed by inverse-square-root decay. The schedule is set by training progress, rather than detecting that an optimum has been reached. See [[paper-vault/papers/vaswani2017attention|Attention Is All You Need]] and its [optimizer schedule, Section 5.3](https://arxiv.org/html/1706.03762v7#S5.SS3).

## VI. Generalization and Validation

### 1. Overfitting

Training increasingly fits the observed examples while performance on held-out data deteriorates. A sustained decrease in training loss alongside an increase in validation loss is a typical signal, including during LLM fine-tuning on small or repetitive datasets. A single validation fluctuation is insufficient: evaluate a fixed, representative held-out set with consistent tokenization, loss masking, and evaluation settings, and examine the trend across evaluations.

Possible responses include [[knowledge/ai-infra/training#2. Early Stopping|early stopping]], fewer training passes, better or more diverse training data, and appropriate regularization. Validation loss measures the chosen prediction objective; for instruction tuning, also check relevant task metrics because token-level loss alone does not fully capture response quality.

### 2. Early Stopping

Monitors a held-out validation metric and stops training after it fails to improve sufficiently for a configured patience interval. For example, stop after three consecutive evaluations without a meaningful validation-loss improvement. Define the interval in the training framework's units, which may be epochs or evaluation events.

Save and select the checkpoint with the best validation metric, which may precede the stopping point. Stopping alone does not automatically restore those weights; enable restoration or best-checkpoint loading explicitly where needed. Keep a separate test set for final evaluation. [Source: Keras EarlyStopping, including patience, minimum improvement, and optional best-weight restoration](https://keras.io/api/callbacks/early_stopping/).

### 3. Weight Decay

Shrinks selected trainable parameters during optimization. AdamW applies a decoupled shrinkage step `theta <- (1 - lr * weight_decay) * theta` in addition to its adaptive gradient update. This can discourage overly large weights; it is distinct from [[knowledge/ai-infra/training#3. Learning-Rate Decay|learning-rate decay]] and from simply adding an L2 term to Adam's loss. [Source: PyTorch AdamW](https://docs.pytorch.org/docs/stable/generated/torch.optim.AdamW.html).

For LoRA/QLoRA, decay applies to trainable adapter parameters included in the optimizer's decay groups, not frozen base weights. Shrinking A/B is not a direct penalty on distance from pretrained weights. For illustration, after attaching adapters:

```python
from torch.optim import AdamW

optimizer = AdamW(
    (p for p in model.parameters() if p.requires_grad),
    lr=1e-4,
    weight_decay=0.01,
)
```

This minimal example decays all included parameters; production trainers may use separate groups excluding biases or normalization parameters. Choose decay strength using held-out performance, rather than treating `0.01` as a universal setting.

### 4. Dropout

Randomly zeroes activation elements during training, reducing dependence on particular feature combinations. Standard inverted dropout rescales retained elements by `1 / (1 - p)` and becomes an identity operation in evaluation mode. It does not permanently delete weights or prune the model. [Source: PyTorch Dropout](https://docs.pytorch.org/docs/stable/generated/torch.nn.Dropout.html).

LLMs may expose attention or hidden-state dropout settings, depending on architecture. Configure supported sites and verify that the instantiated modules use them; changing a configuration field after construction need not change existing modules. Evaluate with dropout disabled. Stronger dropout can also cause underfitting, so more is not necessarily better.

### 5. LoRA Dropout

Adds dropout specifically to the adapter branch. For standard PEFT linear LoRA during training, `y = W_0 x + s B A Dropout(x)`; the original base branch receives the original input. This remains available when the base is frozen or quantized. [Sources: PEFT LoraConfig](https://huggingface.co/docs/peft/main/package_reference/lora); [PEFT linear LoRA implementation](https://github.com/huggingface/peft/blob/main/src/peft/tuners/lora/layer.py).

```python
from peft import LoraConfig

config = LoraConfig(
    r=8,
    target_modules=["q_proj", "v_proj"],
    lora_dropout=0.05,
)
```

Here `0.05` is an illustrative training-time drop probability for adapter input elements. Compare held-out loss and task quality against a zero-dropout baseline while holding other settings fixed. LoRA rank and target coverage also constrain adaptation capacity, but lowering either is not guaranteed to improve generalization.
