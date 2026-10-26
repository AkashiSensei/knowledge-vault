# AI Inference: Concepts and Techniques

Concise entries on autoregressive LLM inference, grouped into:

- Execution phases and state
- Attention architecture and position encoding
- Request scheduling and operator batching
- KV-cache memory management
- Attention kernels
- Decoding strategies
- Serving architecture
- Serving frameworks

Related: [[knowledge/ai-infra/parallelism|Parallelism and state sharding]] covers DP, ZeRO, TP, and PP across training and inference.

## 一些研究的方向

- 动态资源感知
- 输出长度预测（长度、置信上界）
- 长短任务感知（相对顺序）
- PD 联合调度
- 缓存感知调度
- SLO 改制调度
- Chunked Prefill
- 跨 GPU 动态迁移

## I. Execution Phases and Attention State

### 1. Prefill

Processes the prompt's tokens, builds their KV cache, and produces the logits used to sample the first output token. Parallel computation across prompt tokens often makes prefill compute-intensive; its duration contributes to time to first token (TTFT).

A large prefill can delay ongoing decode steps. Controlled mixing, such as chunked prefill under a token budget, can improve utilization. [Source: vLLM optimization guide](https://docs.vllm.ai/en/latest/configuration/optimization/#chunked-prefill).

Related paper: [[paper-vault/papers/yu2022orca|Orca]].

### 2. Decode

Processes one new token per active sequence per step, reuses its KV cache, and predicts the next token. This entry assumes ordinary decoding, without [[knowledge/ai-infra/inference#1. Speculative Decoding|speculative decoding]]. Step duration affects inter-token latency (ITL).

Small-batch decode is often bandwidth-bound, spending much of its time moving model weights and KV data. The compute-bound prefill / bandwidth-bound decode distinction is a tendency: batch size, context length, model architecture, and hardware change the bottleneck. [Source: vLLM optimization guide](https://docs.vllm.ai/en/latest/configuration/optimization/#chunked-prefill).

Related paper: [[paper-vault/papers/yu2022orca|Orca]].

### 3. KV Cache

The **KV cache** stores previously computed key and value vectors for each attention layer, so later decode steps do not recompute the entire prefix. The current query attends to the cached keys and values plus the newly appended token's state. The cache saves computation but consumes memory that generally grows with sequence length. [Source: Transformers cache explanation](https://huggingface.co/docs/transformers/en/cache_explanation).

Related paper: [[paper-vault/papers/kwon2023pagedattention|PagedAttention]].

### 4. Autoregressive Token Generation

**Core idea: Process the current input through the model, then select the next token from vocabulary scores.**

For an ordinary decoder-only Transformer, a token ID is mapped to an embedding and processed through every Transformer layer. During cached decode, each layer computes the current token's Q/K/V, attends to the appropriate cached and current KV state, and appends the new KV. The LM head projects the final hidden vector of dimension `H` into `V` logits, one score per vocabulary token. Greedy decoding selects the highest score; sampling selects from a probability distribution derived from the scores. [Sources: Transformer foundations](https://arxiv.org/abs/1706.03762); [Transformers generation guide](https://huggingface.co/docs/transformers/en/llm_tutorial).

```text
Token ID -> Embedding -> All Transformer layers -> LM head -> Vocabulary logits -> Next token

Prompt [A, B, C]: prefill processes A/B/C; the final prompt position predicts D.
Next decode step: process D using cached A/B/C state to predict E.
Next decode step: process E using cached A/B/C/D state to predict F.
```

*Original schematic for ordinary autoregressive decoding; A–F denote tokens, not necessarily individual characters. KV caching reuses historical computations while the newly processed token still traverses every layer. Generation repeats until EOS, another stop condition, or a token limit. [[knowledge/ai-infra/inference#1. Speculative Decoding|Speculative decoding]] changes the one-token-per-step pattern. [Source: Transformers cache explanation](https://huggingface.co/docs/transformers/en/cache_explanation).*

## II. Attention Architecture and Position Encoding

These are model-design choices learned during training; serving engines must support the checkpoint's architecture. For standard MHA/MQA/GQA with equal key and value head dimensions, the logical KV storage for one sequence is approximately:

$$
M_{\mathrm{KV}} = 2 L T H_{\mathrm{KV}} d_h b,
$$

where `L` is the layer count, `T` the cached token count, `H_KV` the number of KV heads, `d_h` the head dimension, and `b` the bytes per element. This excludes allocator overhead and distributed replication. The following toy example fixes eight query heads and all other dimensions:

| Attention | KV heads | Query heads sharing each KV head | KV storage relative to MHA |
| --- | ---: | ---: | ---: |
| MHA (Multi-Head Attention) | 8 | 1 | 1 |
| GQA with two KV groups | 2 | 4 | 1/4 |
| MQA | 1 | 8 | 1/8 |

These ratios describe stored KV elements, not end-to-end speedups. [Sources: MQA](https://arxiv.org/abs/1911.02150); [GQA](https://arxiv.org/abs/2305.13245).

### 1. Multi-Query Attention (MQA)

Keeps multiple query heads but shares one key head and one value head across them. Each query head still computes its own attention weights. Sharing reduces KV-cache capacity and bandwidth requirements during decode; it does not eliminate the per-query-head attention computation. The reduced KV representation can affect model quality and requires an appropriately trained or adapted checkpoint. [Source: Fast Transformer Decoding](https://arxiv.org/abs/1911.02150).

### 2. Grouped-Query Attention (GQA)

Partitions query heads into groups, with each group sharing one key head and one value head. It provides a quality/efficiency trade-off between MHA and MQA: `H_KV = H_Q` gives MHA, while `H_KV = 1` gives MQA. Efficient kernels reuse each group's KV data without physically duplicating it for every query head. The GQA paper also demonstrates adapting MHA checkpoints through additional training. [Source: GQA](https://arxiv.org/abs/2305.13245).

### 3. Multi-Head Latent Attention (MLA)

DeepSeek-V2 jointly compresses each token's keys and values into a smaller learned latent vector, `c_KV`. Head-specific projections derive content keys and values from this shared latent. During optimized decode, key up-projection can be absorbed into the query projection and value up-projection into the output projection, allowing attention to use the compressed cache without materializing full historical K/V tensors.

Ordinary [[knowledge/ai-infra/inference#4. Rotary Position Embedding (RoPE)|RoPE]] on content keys obstructs this absorption. MLA therefore separates positional Q/K components from content components and caches a small RoPE key alongside `c_KV`. Its per-token, per-layer cache contains roughly `d_c + d_R` elements, where `d_c` is the KV latent dimension and `d_R` the positional-key dimension. Savings and speed depend on those dimensions and the kernel implementation. [Source: DeepSeek-V2, Sections 2.1.2–2.1.4](https://arxiv.org/html/2405.04434v5#S2.SS1.SSS2).

### 4. Rotary Position Embedding (RoPE)

Encodes position by rotating pairs of query and key coordinates through position-dependent angles, with different frequencies across pairs. For unrotated vectors `q_m`, `k_n` and rotation matrix `R(p)`:

$$
(R(m)q_m)^\top(R(n)k_n) = q_m^\top R(n-m)k_n.
$$

This makes relative position enter the attention score; standard RoPE leaves values unrotated. During decode, ordinary implementations cache rotated keys and rotate each new query/key at its assigned position. RoPE preserves vector dimensionality and does not itself compress KV state. Extrapolation beyond training lengths still needs validation; the formula alone does not guarantee long-context quality. [Source: RoFormer, Section 3](https://arxiv.org/html/2104.09864v5#S3).

## III. Request Scheduling and Operator Batching

Orca introduced iteration-level scheduling and selective batching together: the former selects requests each round; the latter executes them. The arrows show runtime information flow. [Source: Orca](https://www.usenix.org/system/files/osdi22-yu.pdf).

```mermaid
flowchart LR
    pool["Active and waiting requests"] -->|request state and capacity constraints| scheduler["Iteration-level scheduler"]
    scheduler -->|selected requests for one iteration| engine["Selective batching engine"]
    engine -->|new tokens and completion state| pool
```

### 1. Iteration-Level Scheduling / Continuous Batching

Orca schedules one model iteration at a time. At iteration boundaries, finished requests leave and waiting requests may enter, subject to batch and memory limits; arrivals do not interrupt an in-progress kernel. During ordinary decode, each selected sequence advances by one token. This removes the need to wait for the longest request before refilling a batch. **Continuous batching** is the common later name for this scheduling pattern. [Source: Orca](https://www.usenix.org/system/files/osdi22-yu.pdf).

![Two-slot decode timeline comparing fixed request-level batches with continuous batching](assets/inference/continuous-batching.svg)

*A shorter request frees a slot after iteration 2. Continuous batching lets C use that slot in iteration 3; a fixed batch waits for A to finish. This original schematic follows the scheduling mechanism in [Orca](https://www.usenix.org/system/files/osdi22-yu.pdf); equal-width iterations illustrate admission order, not measured latency, and prefill is omitted.*

Related paper: [[paper-vault/papers/yu2022orca|Orca: iteration-level scheduling]].

### 2. Selective Batching

Orca combines the current tokens from selected requests for token-wise operators, including QKV projections and feed-forward layers, while splitting attention into request-specific computations and merging their outputs afterward. Shared linear operators can consume a packed token matrix; attention must respect each sequence's own KV history. This execution strategy makes heterogeneous requests compatible with iteration-level scheduling. Modern varlen attention can batch those logically separate attention computations inside one kernel. [Source: Orca](https://www.usenix.org/system/files/osdi22-yu.pdf); [varlen attention API](https://docs.pytorch.org/docs/2.14/nn.attention.varlen.html).

The operator boundary in Orca is:

| Operator | Batched across requests? | Reason |
| --- | --- | --- |
| QKV Linear | Yes | Each token uses the same projection weights; inputs can be packed as `[sum(L_i), H]`. |
| Attention output Linear | Yes, after merging Attention outputs | The output projection acts independently on each token with shared weights. |
| MLP Linear layers and GeLU | Yes | These transformations act independently on each token. |
| LayerNorm | Yes | Normalization is over each token's hidden features, without mixing tokens from different requests. |
| Residual Add | Yes | Corresponding tensor elements are added independently. |
| Attention core: `QK^T`, scaling / causal masking, softmax, and multiplication by `V` | No; computed separately for each request | Each query uses its own request's keys and values, with potentially different history lengths. |

Here, **Attention** means the core attention computation, excluding QKV and output projections. The execution pattern is **batched QKV projection → split by request → per-request Attention → merge → batched output projection**. Batching combines token activations for each operator; it does not combine different operators into one operation or imply kernel fusion. Separate Attention computations also do not, by themselves, establish whether GPU execution overlaps. [Source: Orca, Section 3 and Figures 1b and 5](https://www.usenix.org/system/files/osdi22-yu.pdf).

Related paper: [[paper-vault/papers/yu2022orca|Orca: selective batching]].

### 3. Request Isolation

Each query may access only its own sequence's allowed context. Packing requests together must preserve this boundary; it does not require a separate kernel per request. Shared, identical prefixes may reuse physical KV storage without mixing unrelated histories.

Related papers: [[paper-vault/papers/vaswani2017attention|Transformer attention foundations]]; [[paper-vault/papers/kwon2023pagedattention|PagedAttention and KV sharing]].

### 4. Padding

Extends sequences to a common length so tensors have rectangular shapes. Lengths `[3, 1, 2]` become three rows of length 3: nine slots for six real tokens. A padding mask excludes added positions from attention, but masking alone does not guarantee that their computation or storage is skipped. [Source: PyTorch varlen tutorial](https://docs.pytorch.org/tutorials/intermediate/variable_length_attention_tutorial.html).

### 5. Ragged / Packed Batching

Packs real tokens without padding and records sequence boundaries with cumulative offsets, often named `cu_seqlens` or `indptr`. Lengths `[3, 1, 2]` use six token slots and offsets `[0, 3, 4, 6]`; request `i` occupies `[offsets[i], offsets[i + 1])`.

Variable-length (varlen) attention kernels use this metadata to batch separate sequences' attention. Query and KV offsets can differ: decode may have one query per request but many cached keys. Causal or other attention constraints still apply. [Sources: PyTorch varlen tutorial](https://docs.pytorch.org/tutorials/intermediate/variable_length_attention_tutorial.html); [FlashInfer KV layouts](https://docs.flashinfer.ai/tutorials/kv_layout.html).

![Padded and packed layouts for three sequences, with cumulative offsets and a causal attention mask](assets/inference/padding-vs-ragged.svg)

*The same six tokens occupy nine padded slots or six packed slots. The lower matrix makes the attention boundary explicit: packing C next to B does not let C attend to B. This original example follows the [PyTorch varlen tutorial](https://docs.pytorch.org/tutorials/intermediate/variable_length_attention_tutorial.html) and [FlashInfer's layout documentation](https://docs.flashinfer.ai/tutorials/kv_layout.html). The mask shows allowed positions; a kernel need not materialize this dense matrix.*

### 6. Attention Mask

Defines which key positions a query may attend to. A **padding mask** excludes artificial padding; a **causal mask** excludes future positions within a sequence. Packed sequences also require request boundaries: a single causal triangle over the entire packed array would allow later requests to see earlier ones. Kernels can enforce these constraints through metadata without materializing a dense mask. [Sources: Transformer attention](https://arxiv.org/abs/1706.03762); [PyTorch varlen tutorial](https://docs.pytorch.org/tutorials/intermediate/variable_length_attention_tutorial.html).

Related paper: [[paper-vault/papers/vaswani2017attention|Transformer]].

### 7. Chunked Prefill

Splits a long prompt's prefill into smaller token chunks, allowing decode work to run between or alongside them under a per-iteration token budget. Smaller chunks limit decode stalls; larger chunks can improve prefill efficiency. Chunk size therefore trades off TTFT, inter-token latency, and throughput. [Sources: Sarathi-Serve](https://arxiv.org/abs/2403.02310); [vLLM optimization guide](https://docs.vllm.ai/en/latest/configuration/optimization/#chunked-prefill).

### 8. Cache-Aware Scheduling

Uses reusable-prefix information to order waiting requests. SGLang offers **LPM** (Longest Prefix Match), favoring longer cached prefixes, and **DFS-Weight**, grouping requests by shared prefix subtrees to improve reuse. These are optional policies; the documented default is FCFS. Cache reuse must be balanced against waiting time and fairness. [Sources: SGLang paper](https://arxiv.org/abs/2312.07104); [SGLang scheduling options](https://docs.sglang.io/docs/advanced_features/server_arguments#memory-and-scheduling).

### 9. Overlap Scheduling

Overlaps CPU preparation of the next batch, including scheduling, prefix matching, and memory metadata, with GPU execution of the current batch. SGLang's “zero-overhead” scheduler hides this CPU work where dependencies permit, reducing GPU idle gaps; CPU work and synchronization still exist. [Source: SGLang scheduler design](https://www.lmsys.org/blog/2024-12-04-sglang-v0-4/#zero-overhead-batch-scheduler).

## IV. KV-Cache Memory Management

Orca reserves each request's maximum KV capacity; vLLM assigns blocks as needed. This allocation change complements iteration-level scheduling. The diagram compares their memory costs. [Sources: Orca](https://www.usenix.org/system/files/osdi22-yu.pdf); [PagedAttention](https://arxiv.org/abs/2309.06180).

```mermaid
flowchart TD
    history["KV histories grow by different amounts"]
    history -->|reserve for each admitted request's maximum| reserved["Orca: maximum-length reservation"]
    history -->|allocate more blocks as a sequence grows| paged["vLLM: paged KV management"]
    reserved -->|unused future capacity stays reserved| waste["Fewer requests fit in the same memory budget"]
    paged -->|reduce reservation waste and fragmentation| capacity["More usable capacity; tail-block and metadata costs remain"]
```

### 1. PagedAttention

**PagedAttention** allows attention kernels to read a sequence's logical KV history from non-contiguous physical blocks using a block table. The vLLM runtime allocates and reclaims fixed-size blocks as sequences grow and finish, and can share blocks for common prefixes with copy-on-write where needed. The kernel and runtime cooperate: paging is more than an allocation policy.

Compared with Orca's maximum-length reservation, this avoids reserving the full eventual cache for every admitted request and greatly reduces fragmentation and duplicated state. Waste is not literally zero: partially filled final blocks, metadata, and management overhead remain. Ragged batching describes sequence boundaries; paging describes physical KV placement. A kernel can consume ragged queries and paged KV together. [Sources: PagedAttention paper](https://arxiv.org/abs/2309.06180); [FlashInfer KV layouts](https://docs.flashinfer.ai/tutorials/kv_layout.html).

![Per-request logical KV blocks mapped through block tables to non-contiguous physical blocks](assets/inference/paged-kv-cache.svg)

*A's logical blocks map to physical blocks 3 and 0, so sequence order is independent of physical placement. Unassigned blocks remain available to the allocator, while unused slots inside the last assigned block are tail waste. This original schematic illustrates the logical-to-physical mapping in [PagedAttention](https://arxiv.org/abs/2309.06180), using a toy block size of four tokens. Each token slot represents its K and V state; the engine may preallocate the overall GPU pool while assigning blocks to requests on demand.*

Related papers: [[paper-vault/papers/kwon2023pagedattention|PagedAttention]]; [[paper-vault/papers/yu2022orca|Orca's reservation baseline]].

### 2. Automatic Prefix Caching

Retains computed KV state so later requests with the same prefix can skip repeated prefill. Reuse requires compatible model and input state; matching text in a different preceding context is insufficient. vLLM indexes full KV blocks using hashes incorporating the preceding prefix, block tokens, and relevant extra state. This primarily saves prompt computation; subsequent tokens still require decoding. [Source: vLLM prefix-cache design](https://docs.vllm.ai/en/latest/design/prefix_caching/).

### 3. RadixAttention

SGLang organizes token prefixes and their KV-cache locations in a **radix tree**, whose edges can represent multiple tokens. Prefix matching finds reusable state; inserting diverging requests splits edges. The original design retains completed requests' KV state and evicts unused leaves with LRU while protecting active references. The tree indexes GPU-resident KV data and exposes sharing relationships to [[knowledge/ai-infra/inference#8. Cache-Aware Scheduling|cache-aware scheduling]]. It complements paged storage. [Source: SGLang's RadixAttention design](https://www.lmsys.org/blog/2024-01-17-sglang/#backend-automatic-kv-cache-reuse-with-radixattention).

## V. Attention Kernel Optimization

Here, “Flash” is part of the technique names, suggesting speed; it does not refer to flash memory or a standalone algorithmic step.

- **FlashAttention:** Uses tiling and online softmax to reduce attention's intermediate memory traffic.
- **Flash-Decoding:** Extends this approach for decode with parallel KV splits and a final weighted reduction.

The arrows below identify mechanisms and bottlenecks, with workload-dependent benefits. [Sources: FlashAttention](https://arxiv.org/pdf/2205.14135); [Flash-Decoding](https://crfm.stanford.edu/2023/10/12/flashdecoding.html).

```mermaid
flowchart TD
    conventional["Conventional attention:<br/>materialize scores and probabilities in HBM"]
    flash["FlashAttention, 2022:<br/>tiled attention with online softmax"]
    decoding["Flash-Decoding, 2023:<br/>parallel KV splits with normalized reduction"]
    conventional -->|tiling avoids full intermediate matrices and reduces HBM traffic| flash
    flash -->|KV splitting adds parallel work for small-batch decode| decoding
```

### 1. FlashAttention

**Core idea: Compute attention in fast on-chip memory to reduce HBM reads and writes.**

Computes exact attention using tiling and online softmax, avoiding full attention score and probability matrices in high-bandwidth memory (HBM).

The gain comes from reducing memory traffic and intermediate storage, not from dropping attention entries. Dense attention still has quadratic arithmetic cost in sequence length; floating-point rounding can differ from a conventional implementation. This is complementary to paged KV storage, provided the chosen kernel supports that layout. [Source: FlashAttention paper, Section 3](https://arxiv.org/pdf/2205.14135).

Paper: [FlashAttention (Dao et al., 2022)](https://arxiv.org/abs/2205.14135). Background: [[paper-vault/papers/vaswani2017attention|Transformer attention]].

### 2. Tiling

**Core idea: Divide Q/K/V computation into tiles that fit in shared memory and registers.**

Divides computation into blocks sized for fast on-chip [[knowledge/cuda/memory#4. Shared Memory|shared memory]] and [[knowledge/cuda/memory#1. Registers|registers]]. FlashAttention loads Q, K, and V tiles, computes partial attention, and accumulates the output without writing the full intermediate matrices to HBM. [Source: FlashAttention, Section 3](https://arxiv.org/pdf/2205.14135).

### 3. Online Softmax

**Core idea: Update softmax normalization block by block without storing all scores.**

Computes softmax incrementally over blocks, maintaining a running maximum and normalization sum. In attention, an output accumulator is updated alongside them; when the maximum changes, earlier contributions are rescaled. This lets tiled attention remain correctly normalized without retaining every score. [Source: FlashAttention, Section 3](https://arxiv.org/pdf/2205.14135).

### 4. Split-KV

**Core idea: Split one sequence's KV history across parallel thread blocks on the same GPU.**

Partitions the KV sequence dimension so multiple GPU thread blocks compute partial attention for the same query in parallel. This helps when long KV histories and insufficient existing parallelism leave GPU streaming multiprocessors (SMs) underused. Reduction and temporary-storage overhead can outweigh the benefit on short contexts or already well-utilized batches. Computational splits are independent of physical KV-cache pages. [Source: Flash-Decoding author explanation](https://crfm.stanford.edu/2023/10/12/flashdecoding.html).

### 5. Flash-Decoding

**Core idea: Accelerate decode attention with Split-KV, FlashAttention-style computation, and a weighted merge.**

Applies Split-KV with FlashAttention-style computation inside each split, then merges partial outputs using their log-sum-exp statistics. It targets small-batch decode, where the short query length exposes too little parallel work. [Source: Flash-Decoding author explanation](https://crfm.stanford.edu/2023/10/12/flashdecoding.html).

![FlashAttention's on-chip tile computation and Flash-Decoding's parallel KV splits followed by normalized reduction](assets/inference/attention-tiling-and-split-kv.svg)

*The upper panel shows tiled computation for one query row with running softmax state. The lower panel distributes that row's KV range across parallel workers, each retaining the tiled computation internally. This original schematic follows [FlashAttention](https://arxiv.org/pdf/2205.14135) and the authors' [Flash-Decoding explanation](https://crfm.stanford.edu/2023/10/12/flashdecoding.html). Workers represent GPU thread blocks, not necessarily separate GPUs; computational splits and physical cache pages are different units.*

For one query row, let split `j` return a normalized output `o_j` and `L_j = log(sum(exp(scores_j)))`. The merged output is:

$$
L = \operatorname{logsumexp}_j L_j,
\qquad
o = \sum_j \exp(L_j - L)\,o_j.
$$

The partial outputs must be weighted by their normalization statistics, rather than simply averaged. [Source: Flash-Decoding author explanation](https://crfm.stanford.edu/2023/10/12/flashdecoding.html).

## VI. Decoding Strategies

### 1. Speculative Decoding

**Core idea: Draft several tokens cheaply, then verify them in one target-model pass.**

The arrows show the repeated draft-and-verify control flow. Only the new draft is checked; the confirmed prefix never rolls back.

```mermaid
flowchart TD
    prefix["Confirmed prefix"] -->|condition on fixed history| draft["Small model drafts candidate tokens"]
    draft -->|candidate sequence| verify["Target model computes verification distributions in parallel"]
    verify -->|check candidates in sequence order| accepted{"All candidates accepted?"}
    accepted -->|No| repair["Keep candidates before the first rejection<br/>Discard the rejected candidate and its suffix<br/>Generate one correction token"]
    accepted -->|Yes| bonus["Keep all candidates<br/>Generate one bonus token from the target distribution"]
    repair -->|accepted prefix plus correction| extend["Extend confirmed output<br/>Apply stopping rules in token order"]
    bonus -->|accepted draft plus bonus| extend
    extend -->|check output| stop{"EOS, stop condition,<br/>or generation limit reached?"}
    stop -->|Yes| done["Finish generation"]
    stop -->|No: start the next round| prefix
```

*All candidates being accepted ends a round, not necessarily generation. Stopping takes priority: an accepted EOS ends output there, without a later correction or bonus token; a discarded draft EOS has no effect. This schematic follows the [classic speculative decoding algorithm](https://arxiv.org/abs/2211.17192).*

A small draft model proposes a token sequence. Because those candidates are already known, the target model can evaluate their conditional distributions in parallel with causal attention. Keep the accepted prefix; at the first rejection, discard that candidate and all later ones, and generate a correction. Greedy verification checks agreement with the target's choices; exact speculative sampling uses acceptance probabilities and a corrected sampling distribution to preserve the target model's output distribution.

Multi-token verification amortizes weight reads across positions when decode is bandwidth-bound with spare compute capacity. Drafting, extra model/cache memory, and rejected work add overhead; low acceptance rates or already compute-saturated batches can erase the gain. [Source: Speculative Decoding (Leviathan et al., 2023)](https://arxiv.org/abs/2211.17192).

### 2. Structured Generation / Constrained Decoding

Tracks a grammar's state and masks invalid next tokens before sampling, constraining output to a supported JSON schema, regex, or grammar. SGLang's original work used compressed finite state machines; later integrations include XGrammar, which vLLM also supports. Constraints enforce output structure rather than factual correctness, and grammar processing adds overhead that optimized backends seek to minimize. [Sources: SGLang paper](https://arxiv.org/abs/2312.07104); [SGLang structured outputs](https://docs.sglang.io/docs/advanced_features/structured_outputs); [vLLM structured outputs](https://docs.vllm.ai/en/latest/features/structured_outputs/).

## VII. Serving Architecture

### 1. Prefill / Decode Disaggregation

**Core idea: Separate prefill and decode to control latency and improve goodput, transferring KV state between GPU groups.**

The prefill group processes the prompt; its KV cache and continuation state are handed to a decode group serving the same model, which continues generation without recomputing the prompt. DistServe separates the phases to reduce interference and independently configure resources and parallelism for first-token and per-token latency requirements. Different GPU models are optional: the groups can instead differ in GPU count, [[knowledge/ai-infra/parallelism#1. Tensor Parallelism (TP)|TP]], [[knowledge/ai-infra/parallelism#2. Pipeline Parallelism (PP)|PP]], and concurrency.

The goal is **per-GPU goodput**: the maximum request rate per GPU that meets the required attainment level for both time-to-first-token (TTFT) and time-per-output-token (TPOT) limits. Keeping the GPU busy alone does not ensure timely responses. [Source: DistServe (Zhong et al., 2024)](https://arxiv.org/abs/2401.09670).

The trade-off is latency isolation and independent resource allocation versus KV-transfer overhead, separate model deployments, and load balancing. Colocation with chunked prefill can exploit complementary resource demands while limiting decode stalls; disaggregation is not universally better. The choice depends on latency targets, workload, and interconnect capacity. [Sources: DistServe](https://arxiv.org/abs/2401.09670); [Sarathi-Serve](https://arxiv.org/abs/2403.02310).

This placement strategy can complement speculative decoding within the decode group.

### 2. Cache-Aware Routing

Places incoming requests on workers likely to hold reusable prefix KV state, while balancing load. SGLang's cache-aware router introduced approximate radix-tree tracking to estimate worker cache locality without synchronizing exact cache contents. This extends reuse across a deployment; queueing on a cache-rich worker can outweigh saved prefill work. [Source: SGLang cache-aware load balancer](https://www.lmsys.org/blog/2024-12-04-sglang-v0-4/#cache-aware-load-balancer).

## VIII. Serving Frameworks

Both **vLLM** and **SGLang** integrate these techniques into inference-serving runtimes. Their representative designs differ, while their supported capabilities overlap substantially.

| Aspect | vLLM | SGLang |
| --- | --- | --- |
| Representative foundation | PagedAttention: efficient block-based KV storage and attention access. | RadixAttention: automatic prefix reuse across generation calls. |
| Prefix-cache index | Hash-indexed full blocks, incorporating preceding-prefix identity. | Radix tree exposing shared token-prefix structure. |
| Notable design emphasis | Paged KV management integrated with continuous batching. | Prefix reuse integrated with cache-aware scheduling/routing and CPU/GPU overlap. |

Both support continuous batching, chunked prefill, speculative decoding, structured outputs, distributed parallelism, and PD disaggregation. Compare them using the same model, hardware, request lengths, prefix-sharing patterns, and latency targets; the index structure alone does not establish a performance winner. [Sources: vLLM overview](https://docs.vllm.ai/en/latest/); [vLLM prefix caching](https://docs.vllm.ai/en/latest/design/prefix_caching/); [SGLang runtime overview](https://github.com/sgl-project/sglang); [SGLang paper](https://arxiv.org/abs/2312.07104).
