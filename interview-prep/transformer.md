# Transformer 结构

## I. Block 的组成与作用

### Transformer block 中 Attention、Add & Norm 和 FFN 分别做什么？

Attention 让 token 从允许关注的位置汇总信息，FFN 对每个 token 的特征独立进行非线性变换，Add 是残差连接，Norm 用于归一化以帮助稳定训练。原始 Transformer 编码器使用 Post-Norm：`h = LayerNorm(x + Attention(x))`，`y = LayerNorm(h + FFN(h))`（省略 dropout）。输入输出通常保持 `[batch, sequence, hidden]` 的形状，便于残差相加和堆叠。原始编码器—解码器模型的解码器还有 Cross-Attention，不能把这条两子层流程当作所有 Transformer 的统一结构。[参考：Transformer 原论文](https://arxiv.org/html/1706.03762v7#S3.SS1)。

### Add（残差连接）有什么作用？

把子层输入与子层计算结果逐元素相加，即 `x + F(x)`。它为原有表示提供直接通路，使子层可以学习对表示的修正，并为反向梯度提供较直接的传播路径，帮助深层网络训练；不是拼接，输入和输出的对应维度必须匹配。[参考：Transformer 残差结构](https://arxiv.org/html/1706.03762v7#S3.SS1)。

### Norm（归一化）有什么作用？

以常见 LayerNorm 为例，对每个 token 的 hidden 维度计算均值和方差，先标准化，再使用可学习的缩放和偏移，帮助控制进入后续计算的数值尺度、改善训练稳定性。通常不跨 batch 或 token 求均值；经过可学习变换后的输出也不必严格均值为零、方差为一。[参考：PyTorch LayerNorm](https://docs.pytorch.org/docs/stable/generated/torch.nn.LayerNorm.html)。

### FFN（前馈网络）有什么作用？

FFN（Feed-Forward Network，前馈网络）对每个 token 的特征向量做可学习的非线性加工：先用线性层组合各个特征，再经过激活函数，最后用第二个线性层组合结果并投影回原维度。例如一个 token 的 4 维向量可以映射为 8 维、经过激活、再回到 4 维；这是示意维度，不是固定配置。不同位置使用同一组参数分别计算，序列长度不变；Attention 汇总其他位置的信息，FFN 加工当前位置已经得到的特征，并不在此处读取其他 token。基本形式是 `FFN(x) = activation(xW1 + b1)W2 + b2`。[参考：Transformer FFN](https://arxiv.org/html/1706.03762v7#S3.SS3)。

### Post-Norm 和现代大模型常见的 Pre-Norm 顺序有什么区别？

Post-Norm 是子层计算、残差相加后再归一化；Pre-Norm 是先归一化再送入子层，随后与残差相加。例如简化的 Pre-Norm block：`h = x + Attention(Norm(x))`，`y = h + FFN(Norm(h))`。LLaMA 使用 Pre-Norm 和 RMSNorm，并以 SwiGLU 作为 FFN 的变体，所以记忆结构时要区分原始教学图与具体模型实现。[参考：LLaMA 架构](https://arxiv.org/html/2302.13971v1#S2.SS2)。

### Norm 放在前面，block 最后的输出不就没有归一化了吗？

对，Pre-Norm 的单个 block 输出是残差相加的结果，没有再整体做 Norm。它归一化的是送进 Attention/FFN 分支的输入：残差流直接传递，下一子层再对自己的分支输入做 Norm；不要求每个 block 输出都已标准化。这样残差路径不必每次经过归一化，保留较直接的梯度通路。以 LLaMA 为例，所有 block 完成后还有一次最终 RMSNorm，再送入输出线性层生成 logits；这里归一化的是最后的隐藏表示，并非声称 logits 已归一化。[参考：Meta 官方 LLaMA 实现中的 TransformerBlock 与 Transformer.forward](https://github.com/meta-llama/llama/blob/main/llama/model.py)。

### FFN 中的非线性层就是 Norm 吗？

不是，这里指 ReLU、GELU、SiLU 等激活函数。以原始 FFN 使用的 ReLU 为例，它对每个元素执行 `max(0, z)`，如 `[-2, 3, -1, 4] → [0, 3, 0, 4]`。激活函数使整个 FFN 能表示非线性关系；若没有它，两次线性/仿射变换可以合并为一次。Norm 调整输入的统计尺度，和激活函数承担不同职责；这并不是说 Norm 在数学上一定是线性运算。[参考：PyTorch ReLU](https://docs.pytorch.org/docs/stable/generated/torch.nn.ReLU.html)、[Transformer FFN](https://arxiv.org/html/1706.03762v7#S3.SS3)。

### Attention 是线性的吗？

标准 Self-Attention 整体是非线性的。Q、K、V 的投影（如 `Q = XW_Q`）是线性变换，但 `softmax(QKᵀ / √d_k)V` 中的注意力权重依赖输入，Softmax 也是非线性运算；Q、K 同时随 X 变化时，点积本身也不是 X 的线性函数。因此不能因为 Attention 大量使用矩阵乘，就认为它整体线性。若把注意力权重矩阵 A 固定，则 `AV` 对 V 是线性的，但这只是固定权重条件下的局部关系。FFN 的激活函数提供另一种逐 token 的非线性变换，并非 Transformer 中非线性的唯一来源。[参考：Transformer 的 Scaled Dot-Product Attention](https://arxiv.org/html/1706.03762v7#S3.SS2.SSS1)。

## II. 现代模型的结构方向

### 现代大模型相对原始 Transformer 主要有哪些结构改进方向？

常见方向包括归一化位置与形式、FFN 的门控变换、Attention 的 KV 存储结构、位置编码与长上下文、MoE 稀疏扩容，以及面向生成和多模态的整体架构选择。它们分别针对稳定性、表达能力、显存与带宽、位置建模、容量和任务适配，不是一条所有模型必须依次采用的升级路线。一个常见的自回归语言模型组合是 Decoder-only、Pre-Norm、RMSNorm、RoPE、GQA 和 SwiGLU，但不是所有模型的统一配置。[参考：LLaMA](https://arxiv.org/abs/2302.13971)、[GQA](https://arxiv.org/abs/2305.13245)。

### 归一化结构上有哪些常见变化？

一是由 Post-Norm 改为 Pre-Norm，改变归一化相对残差分支的位置；二是用 RMSNorm 替代 LayerNorm，改变归一化的具体计算。RMSNorm 按均方根缩放，不像 LayerNorm 那样先减去均值，计算更简单，仍保留可学习的缩放。两者是独立选择，不应混为一个改动，也不意味着所有模型都采用相同方案。[参考：RMSNorm](https://arxiv.org/abs/1910.07467)、[LLaMA 架构](https://arxiv.org/html/2302.13971v1#S2.SS2)。

### 普通 FFN 为什么会改为 SwiGLU 等门控 FFN？

基本 FFN 是线性变换、激活、再线性变换；SwiGLU 则从输入形成两路线性投影，其中一路经过 SiLU 激活，再将两路逐元素相乘后投影回输出维度。它增加输入相关的门控，让模型学习如何调制特征；这是连续数值的调制，不是简单的 0/1 开关。通常有三组投影矩阵，中间维度需结合参数与计算预算设置，不能只替换激活名字就认定成本相同。[参考：GLU Variants](https://arxiv.org/abs/2002.05202)。

### MQA、GQA 和 MLA 在优化 Attention 的什么部分？

它们主要改变 K/V 的组织和缓存成本。MQA 让多个 Q 头共享一组 K/V 头；GQA 将 Q 头分组，每组共享 K/V，在完整多头和单组共享之间取舍。MLA 是另一条方案，用低维潜在表示压缩缓存的 KV 信息，并配合相应的投影计算。目标是减少自回归推理的 KV Cache 占用和读取开销，同时权衡模型质量和实现复杂度；这些方案不是同一条必经演进顺序。[参考：GQA](https://arxiv.org/abs/2305.13245)、[DeepSeek-V2 MLA](https://arxiv.org/abs/2405.04434)。

### RoPE 相对直接添加位置向量改变了什么？

RoPE 按位置对 Q、K 的成对分量施加旋转，让注意力点积体现相对位置信息，而不是只在输入 embedding 上加一个位置向量。它是常见的位置建模方式，但采用 RoPE 不等于自动获得无限长上下文，长度扩展仍涉及训练分布、频率/缩放策略以及注意力的计算和缓存成本。[参考：RoFormer](https://arxiv.org/abs/2104.09864)。相关追问见 [[interview-prep/transformer#III. 长上下文支持|长上下文支持]]。

### MoE 在 Transformer block 中通常改变什么？

常见做法是把部分稠密 FFN 换成多个专家 FFN 加路由器，每个 token 只选择少数专家计算并合并结果。这使总参数容量增长时，每 token 激活的计算量不必按同样比例增长，但总参数仍需要存储，分布式训练还会引入 token 分发与回收、通信和负载均衡问题。MoE 不是简单增加 Attention 的头数。[参考：Switch Transformer](https://arxiv.org/abs/2101.03961)。

### 从语言模型到多模态和生成模型，整体架构有哪些变化？

自回归语言模型常用 Decoder-only，围绕带因果掩码的自注意力预测下一个 token，不再保留原始翻译模型的独立编码器及对应 Cross-Attention；这是任务相关的架构选择，不是所有任务都应照搬。视觉语言模型可用视觉编码器与投影器，把图像特征接入语言模型；其他融合方案也可使用 Cross-Attention。DiT 则将 Transformer 用作扩散模型中的去噪骨干，处理图像潜在 patch 等表示，不能直接等同于自回归文本解码器。[参考：LLaMA](https://arxiv.org/abs/2302.13971)、[LLaVA](https://arxiv.org/abs/2304.08485)、[DiT](https://arxiv.org/abs/2212.09748)。

### FlashAttention 属于模型结构改进吗？

标准精确 FlashAttention 主要改变 Attention 的计算和数据搬运方式，通过分块等方法减少 HBM 读写，不是像 GQA/MoE 那样改变模型的参数组织或连接结构。数学目标仍是相同的 Attention，实际浮点结果可因运算顺序不同存在误差；因此谈模型架构时要与算子实现优化区分。[参考：FlashAttention](https://arxiv.org/abs/2205.14135)。

### 现代大模型仍然是类似的 Attention 和 FFN block 堆叠起来的吗？

对，常规稠密自回归 Transformer 通常仍是“输入 embedding → 多个相似 block → 最终 Norm → 输出头”。每个 block 主要包含自注意力、FFN、归一化，以及分别绕过 Attention 和 FFN 的残差连接；现代变化多发生在这些组件内部或它们的顺序上。结构相似不等于参数共享，各层通常有独立的 Attention 和 FFN 权重。也并非所有模型的 block 完全相同，例如部分层可使用 MoE FFN，或不同的注意力形式。[参考：Meta LLaMA 的 TransformerBlock 与层堆叠实现](https://github.com/meta-llama/llama/blob/main/llama/model.py)、[Switch Transformer](https://arxiv.org/abs/2101.03961)。

### MoE 是 Attention 不变、使用多个不同 FFN 的结构吗？

常见 Transformer MoE 基本如此：Attention 可以保持原样，把部分层原来的一个 FFN 换成多个参数独立的专家 FFN，再增加一个可训练路由器。路由器根据每个 token 的当前表示选择少数专家，例如从 4 个专家中选 2 个，各自计算后按路由权重合并结果，再接残差；不同 token 可以选择不同专家。专家通常输入输出维度一致、结构相似，但权重不同，稀疏路由时每个 token 不会执行全部专家。这样可扩大总参数容量，而每 token 的专家计算量由选中的专家决定；全部专家仍需存储，跨卡放置会带来分发、回收和负载均衡开销。MoE 不要求 Attention 同时改变，也可与 GQA/MLA 等改进组合；并非每层都必须使用 MoE。[参考：Switch Transformer](https://arxiv.org/abs/2101.03961)、[DeepSeek-V2](https://arxiv.org/abs/2405.04434)。

### Router 怎么选择专家，它又是怎么训练的？

以常见 token-choice 门控为例，Router 用一个可训练的线性投影，将 token 当前的 hidden 向量映射为每个专家的分数，再用 Softmax 等方式得到门控权重，选 Top-k 专家执行并加权合并输出；具体评分、归一化与选择规则随模型不同。它通常没有“这个 token 应交给哪个专家”的人工标签，而是和整个模型端到端训练：任务损失沿专家输出及可微门控权重回传，计算 Router 和所选专家的梯度，再由优化器更新。Top-k 的离散索引本身不可直接求导；以 Switch 的 Top-1 为例，仍将被选专家的输出乘以其原门控概率，使任务梯度可沿概率路径回到 Router，不能把“选中谁”误认为可微运算。[参考：Switch 的路由与训练](https://arxiv.org/html/2101.03961v3#S2.SS1)。

还要防止大量 token 集中到少数专家，导致过载、空闲专家缺少训练和跨卡负载不均。常见方法是增加负载均衡辅助损失；也有按近期负载调整路由偏置、避免用辅助损失提供均衡梯度的方法。均衡一般看一批 token 或一段时间内的专家负载，而不是要求每个 token 均匀使用所有专家。[参考：Switch 负载均衡](https://arxiv.org/html/2101.03961v3)、[Loss-Free Balancing](https://arxiv.org/abs/2408.15664)。

### MoE 为什么计算稀疏，但系统实现仍然很难？

稀疏只意味着每个 token 执行少数专家，不代表通信、显存和调度成本同比减少。专家分布在多卡时，需按路由结果重排并发送 token，在目标卡计算后将结果送回原位置合并，常见专家并行实现用 All-to-All 组织交换；反向也有对应的数据流。专家收到的 token 数动态且可能不均，热门专家或其所在卡拖慢进度；每个专家分到的 token 较少时，矩阵乘规模小，GPU 利用率可能下降。所有专家的参数及相应训练状态仍需由系统存储，也有路由、重排和缓冲区开销。优化通常围绕负载均衡、Grouped GEMM/融合、专家放置与网络拓扑，以及通信计算重叠展开；并不能仅凭激活参数量推断端到端速度。[参考：Megatron Core MoE 的负载均衡、专家计算与 Token Dispatcher](https://docs.nvidia.com/megatron-core/developer-guide/latest/user-guide/features/moe.html)。

### MoE 问题里的“系统实现”具体指什么？

这里指训推框架如何将 MoE 的模型计算高效、正确地执行在 GPU 集群上。模型结构规定 Router 选专家并合并输出；执行实现还要安排专家权重放在哪张卡、按专家聚合和重排 token、组织跨卡通信、启动专家计算、恢复 token 顺序，以及训练时的反向传播与参数更新。还需处理显存、负载均衡和通信计算重叠。典型涉及 Megatron-Core 等框架、CUDA 算子和 NCCL 通信库，是模型计算的执行层，不等同于平台层的作业提交或资源配额管理。[参考：Megatron Core MoE](https://docs.nvidia.com/megatron-core/developer-guide/latest/user-guide/features/moe.html)。

## III. 长上下文支持

### 如何让大语言模型支持更长的上下文，主要瓶颈是什么？

要同时解决“位置能否泛化、信息能否有效利用、系统成本能否接受”三个问题。超出训练长度时，位置关系可能偏离已学分布；即使位置可表示，模型也未必能在大量干扰中检索和关联远处信息；更长序列还会增加 Attention 计算、训练激活和推理 KV Cache 成本。通常结合位置插值或频率缩放、长上下文继续预训练或微调，以及高效 Attention、缓存优化和多卡并行，并在目标长度上验证检索与推理效果，不能只修改最大长度配置。[参考：Position Interpolation](https://arxiv.org/abs/2306.15595)、[Lost in the Middle](https://arxiv.org/abs/2307.03172)、[FlashAttention](https://arxiv.org/abs/2205.14135)。

### 超出训练长度就遇到陌生的位置编码，这个理解对吗？RoPE 能解决吗？

部分正确，但不能理解为所有位置编码都在查一张位置表。可学习的绝对位置表可能没有超出范围的条目；RoPE 则按位置计算旋转，能为更远的位置生成编码，并让 Q/K 点积体现相对位置。不过，“公式算得出来”不等于模型能理解未训练过的距离和旋转相位组合，直接外推仍可能失效。位置插值把更长序列的位置压回原有范围，YaRN 等进一步调整旋转频率与注意力缩放，常配合微调适应；RoPE 提供了扩展的基础，不会自动赋予无限长上下文能力。原理见 [[knowledge/ai-infra/inference#4. Rotary Position Embedding (RoPE)|RoPE]]。[参考：Position Interpolation](https://arxiv.org/abs/2306.15595)、[YaRN](https://arxiv.org/abs/2309.00071)。

### 支持长输入，是否还需要用长数据训练模型捕捉远距离信息？

通常需要相应的训练适配，但不一定从头就用目标最大长度完成全部预训练，可以在已有模型上做长上下文继续预训练或指令微调。数据应让模型实际使用远距离信息，例如跨段检索、关联和长文总结；仅把互不相关的短文本拼成长序列，并不保证学会这些能力。部分位置扩展方法可在有限训练长度之外取得外推收益，因此也不能把训练时最大长度当成绝对上限。最终要评测相关信息位于不同位置、存在干扰时的表现；能接收长输入不等于能有效利用它。[参考：LongAlign](https://arxiv.org/abs/2401.18058)、[YaRN](https://arxiv.org/abs/2309.00071)、[Lost in the Middle](https://arxiv.org/abs/2307.03172)。

### 显存装得下长上下文，为什么仍可能很慢？系统优化能解决什么？

对标准稠密 Attention，在模型维度固定时，整段 prefill 的注意力计算量随长度近似二次增长；使用 KV Cache 的 decode 每生成一个 token，仍需关注已有上下文，注意力计算和 KV 读取随当前长度增长。固定 batch、层数和 KV 格式时，KV Cache 容量近似线性增长，训练还需保存或重算激活。FlashAttention 减少中间存储和显存搬运，但不消除稠密 Attention 的二次计算量；GQA/MLA、KV 量化可降低缓存成本，激活重计算和多卡切分可缓解容量压力，各有计算、通信或质量取舍。这些优化改善“装得下、跑得动”，不能替代模型对长距离信息的学习。详见 [[knowledge/ai-infra/inference#1. FlashAttention|FlashAttention]]、[[knowledge/ai-infra/inference#3. KV Cache|KV Cache]] 和 [[interview-prep/training#IV. 激活重计算|激活重计算]]。
