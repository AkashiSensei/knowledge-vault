# MLSys 2025 论文列表

官方 Proceedings 共收录 61 篇论文。以下标题均链接至对应的官方论文摘要页。每篇依次列出机构与主要作者、核心工作、相较既有方法的核心创新，以及便于快速识别研究对象与技术路径的细粒度方向。

- [Graph Learning at Scale: Characterizing and Optimizing Pre-Propagation GNNs](https://proceedings.mlsys.org/paper_files/paper/2025/hash/0badcb4e95306df76a719409155e46e8-Abstract-Conference.html)
  - Cornell University、NVIDIA；Zichao Yue、Chenhui Deng、Zhiru Zhang
  - 该工作系统比较先离线传播特征、再训练模型的 pre-propagation GNN 与在线 neighbor sampling GNN。作者发现 PP-GNN 虽避免邻居爆炸，但训练会被细粒度 data loading 和预传播后的 input expansion 限制；据此重新组织数据布局、加载和训练流程，使吞吐较原 PP-GNN 平均提高 15 倍，在大图上较 sampling 方案最高加速两个数量级且保持相近准确率。
  - 相较把 pre-propagation 只当作算法层面的去采样方案，核心创新是首次定位其真实数据路径瓶颈，并为扩张后的特征输入专门设计端到端训练管线。
  - Pre-Propagation GNN、训练数据加载、Input Expansion、大图训练

- [SwiftVI: Time-Efficient Planning and Learning with MDPs](https://proceedings.mlsys.org/paper_files/paper/2025/hash/0f8426558905746fc38da5e335700aec-Abstract-Conference.html)
  - Aarhus University、University of Copenhagen；Kasper Overgaard Mortensen、Konstantinos Skitsas、Emil Morre Christensen 等
  - SwiftVI 加速大状态/动作空间 MDP 的 value iteration 和模型学习。它为每个 state 按 Q-value 上界维护 action priority queue，在一次 Bellman backup 中先利用紧上界排除不可能成为最优的动作，只对剩余候选做完整转移计算；多种算法变体在不同 MDP 参数下都减少 planning 时间，同时保持最优策略语义。
  - 相较每轮对每个 state 的全部 action 做精确 Bellman backup，核心创新是用可证明的 Q 上界和单优先队列安全剪枝动作搜索。
  - 经典 Agent Planning、Markov Decision Process、Value Iteration、Action Pruning

- [Balancing Pipeline Parallelism with Vocabulary Parallelism](https://proceedings.mlsys.org/paper_files/paper/2025/hash/10e400a587ff6925e4e26333b419ff55-Abstract-Conference.html)
  - Sea AI Lab、National University of Singapore；Yeung Man Tsung、Penghui Qi、Min Lin、Xinyi Wan
  - 该工作处理大词表 LLM 训练中 embedding/output vocabulary layer 使首尾 pipeline stage 显存和计算失衡的问题。系统把 vocabulary layer 横向均分到所有 pipeline device，再把其计算组织成可插入既有 schedule 的 pass，并减少 vocabulary parallel 引入的 barrier 与 activation buffer；对不同词表大小都能平衡参数和计算，吞吐提高 5%–51%，与 V-Half 组合时同时达到内存和计算平衡。
  - 相较只对 Transformer block 做 stage partition、把词表层完整留在边界 stage，核心创新是把 vocabulary parallel 变成可组合的 pipeline 维度并控制额外 activation 常数级增长。
  - LLM Pipeline Training、Vocabulary Parallelism、Stage Balance、Activation Memory

- [Youmu: Efficient Columnar Data Pipeline for LLM Training](https://proceedings.mlsys.org/paper_files/paper/2025/hash/136b9a13861308c8948cd308ccd02658-Abstract-Conference.html)
  - University of Virginia、University of Toronto、The Chinese University of Hong Kong；Tianle Zhong、Jiechen Zhao、Qiang Su、Geoffrey Fox
  - Youmu 让万亿 token 级 LLM 预训练直接读取 Parquet 等 columnar dataset，避免先转换并复制为专用训练格式。它针对随机 shuffle 造成的大量细粒度读取，重新设计列级索引、I/O 聚合和内存受控缓存，把数据从存储直接送往 GPU；吞吐接近使用大规模分布式内存缓存的最快 pipeline，但内存减少约 80%，同时更充分 shuffle 使 perplexity 改善 0.3–0.7。
  - 相较用格式转换换取顺序大块 I/O，核心创新是在原生列存上同时支持细粒度随机访问和低内存预取，消除额外数据副本而不牺牲训练随机性。
  - LLM 训练数据管线、Columnar Storage、细粒度随机 I/O、Shuffle

- [LeanAttention: Hardware-Aware Scalable Attention Mechanism for the Decode-Phase of Transformers](https://proceedings.mlsys.org/paper_files/paper/2025/hash/16ec6494e9b5a4138de7238761d715b4-Abstract-Conference.html)
  - Microsoft；Rya Sanovar、Srikant Bharadwaj、Renée St. Amant 等
  - LeanAttention 是针对长上下文 decode 的精确 attention kernel，处理单个 query token 读取超长 KV 时不同 thread block 工作量和归约不均的问题。它重新安排分块 attention 的执行与中间结果合并，使硬件并行度随 context length 扩展而不采用近似稀疏；相较 FlashDecoding，attention 平均加速 1.73 倍，在 256K context 上最高 2.18 倍。
  - 相较沿用 prefill 风格的分块或静态 split-K，核心创新是为 decode 的极不对称 query/KV 形状设计可扩展的工作分配和归约数据流。
  - 长上下文 Decode、Exact Attention Kernel、硬件感知工作划分、KV 读取

- [Photon: Federated LLM Pre-Training](https://proceedings.mlsys.org/paper_files/paper/2025/hash/185087ea328b4f03ea8fd0c8aa96f747-Abstract-Conference.html)
  - University of Cambridge、Flower Labs、Beijing University of Posts and Telecommunications、Zhejiang University；Lorenzo Sani、Alex Iacob、Zeyu Cao 等
  - Photon 是跨组织、低带宽网络上的端到端 LLM 预训练系统：每个 silo 内可用多 GPU 本地训练，只周期性聚合模型更新，而不是每 step 同步梯度。系统通过小 client batch、很高 local learning rate 和 federated averaging 兼顾异构数据与收敛，训练出最高 7B 的 decoder-only 模型；通信量减少 64–512 倍，wall time 较基线分布式方案缩短 35%，并可随可用计算资源扩展。
  - 相较把 FL 限于微调或小模型，核心创新是给出可从零预训练数十亿参数 LLM 的完整跨 silo 配方，并验证极低通信下仍有接近集中式的 compute-time scaling。
  - 联邦 LLM 预训练、Cross-Silo Training、低带宽同步、互联网算力协作

- [MEADOW: Memory-efficient Dataflow and Data Packing for Low Power Edge LLMs](https://proceedings.mlsys.org/paper_files/paper/2025/hash/259a5df46308d60f8454bd4adcc3b462-Abstract-Conference.html)
  - Yale University、IIT Roorkee、IBM Research；Abhishek Moitra、Arkapravo Ghosh、Shrey Agrawal 等
  - MEADOW 面向不到 10 W、off-chip bandwidth 很低的边缘 FPGA LLM 推理。TPHS dataflow 按 token 并行、按 attention head 顺序执行，使大中间 activation 尽量留在片上并减少反复 DRAM 写回；weight packing 将矩阵分解为唯一值及索引，降低权重读取量。ZCU102 上 decode、prefill latency 分别降低 1.5 倍和 2.5 倍，端到端较既有方案改善 40% 以上。
  - 相较把数据中心 GEMM dataflow 原样缩到边缘硬件，核心创新是围绕小片上缓存重排 token/head 执行，并用无损权重唯一值打包共同压低外存流量。
  - 边缘 LLM 加速器、Token-Parallel Head-Sequential、权重打包、片外内存流量

- [Rethinking Key-Value Cache Compression Techniques for Large Language Model Serving](https://proceedings.mlsys.org/paper_files/paper/2025/hash/26289c647c6828e862e271ca3c490486-Abstract-Conference.html)
  - Nanyang Technological University、Shanghai AI Laboratory、SenseTime；Gao Wei、Xinyu Zhou、Peng Sun 等
  - 这是一项面向生产 serving 的 KV compression 复核研究，而不是新压缩算法。作者统一实现代表性 eviction/quantization 方法，除平均准确率和显存外，还测 sample-level 失败、实际 throughput、端到端 latency 与输出长度；结果显示现有 Flash/Paged Attention 未必把稀疏状态转成吞吐，压缩还可能让模型生成更长答案而抵消收益，并提供开源测试工具。
  - 相较只在离线任务上报告 KV 减少率和平均质量，核心贡献是揭示实现支持、输出长度变化与单样本脆弱性这三个生产落差，重新定义压缩是否“有效”的评价口径。
  - KV Cache Compression、生产 Serving 评测、输出长度膨胀、Sample-Level Accuracy

<a id="rubick"></a>

- [Rubick: Exploiting Job Reconfigurability for Deep Learning Cluster Scheduling](https://proceedings.mlsys.org/paper_files/paper/2025/hash/270339c997293ca2988c62f4308e389f-Abstract-Conference.html)
  - East China Normal University、Alibaba Group、Peng Cheng Laboratory、Huazhong University of Science and Technology；Xinyi Zhang、Hanyu Zhao、Wencong Xiao 等
  - Rubick 调度可在 3D parallel、ZeRO、offload 等 execution plan 间切换的训练作业，实验包含 LLaMA-2-7B、LLaMA-30B 等 LLM，也包含 ViT、BERT 等其他模型。性能模型预测每种 plan 对 GPU、CPU、memory 和 bandwidth 的需求，集群调度器持续联合决定“每个作业用什么 plan”和“分多少类资源”，同时约束单作业性能保证；64 GPU 集群中平均 JCT 最高降低 3.2 倍、makespan 降低 1.4 倍。
  - 相较把用户提交的并行方案视为固定黑盒后再分配 GPU，核心创新是把 execution-plan reconfiguration 本身纳入多租户集群调度决策。
  - 深度学习集群调度、可重构训练作业、Execution Plan、Multi-Resource Allocation

- [SampleAttention: Near-Lossless Acceleration of Long Context LLM Inference with Adaptive Structured Sparse Attention](https://proceedings.mlsys.org/paper_files/paper/2025/hash/2d04d97593c8c33d415337f408ed0e1b-Abstract-Conference.html)
  - Peking University、The Chinese University of Hong Kong、Zhipu.AI；Qianchao Zhu、Jiangfei Duan、Chang Chen 等
  - SampleAttention 加速长 prompt 的 prefill attention，并允许不同输入、head 和模型使用不同稀疏模式。它以 Cumulative Residual Attention 表示被召回的 attention mass，在给定质量阈值下先由 query 引导采样，再选取硬件友好的 column/slash strip，寻找满足阈值的最小 KV 子集；相较 FlashAttention2，TTFT 最高降低 5.29 倍并形成更好的准确率-速度 Pareto 前沿。
  - 相较固定 window/stride 或统一 sparsity ratio，核心创新是用可解释的 attention recall 指标驱动每个 head 的动态结构化稀疏选择。
  - 长上下文 Prefill、Structured Sparse Attention、Query-Guided Sampling、TTFT

- [SPA: Scaling Graph Neural Network Training on Large Graphs via Probabilistic Splitting](https://proceedings.mlsys.org/paper_files/paper/2025/hash/3619b2fc65a5538a24b48efc089da709-Abstract-Conference.html)
  - University of Massachusetts Amherst、University of Illinois Urbana-Champaign、Oak Ridge National Laboratory；Sandeep Polisetty、Juelin Liu、Yi Fung 等
  - SPA 的 split parallelism 让多个 GPU 协作处理同一个 GNN mini-batch，把 sampling、feature loading 和训练都拆开，从而避免 data parallel worker 对高度重叠子图重复采样和取数。由于拆分会新增通信，系统用轻量概率 partition 让相关顶点尽可能共置并控制跨卡边；在大图上优于 DGL、Quiver 和 P3。
  - 相较仅把不同 mini-batch 分到不同 GPU，核心创新是跨 GPU 分割单 batch 的完整数据路径，并用概率分区抵消去重带来的通信代价。
  - GNN Split Parallelism、重复子图消除、概率分区、采样-加载-训练协同

- [SparseTransX: Efficient Training of Translation-Based Knowledge Graph Embeddings Using Sparse Matrix Operations](https://proceedings.mlsys.org/paper_files/paper/2025/hash/36e2967f87c3362e37cf988781a887ad-Abstract-Conference.html)
  - Texas A&M University；Md Saidul Hoque Anik、Ariful Azad
  - SparseTransX 把 TransE、TransR、TransH、TorusE 等知识图谱 embedding 训练中的多次 scatter/gather 与梯度累加统一改写为 sparse-dense matrix multiplication。由成熟 SpMM kernel 一次处理批量实体和关系更新，减少不规则访存、kernel launch 与临时内存；CPU 最高加速 5.3 倍、GPU 最高 4.2 倍，并可扩展到其他 translation/non-translation KGE。
  - 相较针对每种 KGE 手写索引更新 kernel，核心创新是用稀疏矩阵代数统一表达核心训练数据移动，使算法共享同一高性能实现。
  - 知识图谱 Embedding、SpMM、Scatter-Gather 融合、稀疏训练 Kernel

- [ReaL: Efficient RLHF Training of Large Language Models with Parameter Reallocation](https://proceedings.mlsys.org/paper_files/paper/2025/hash/3b3889d313ba9476c12c2d77ea66b24f-Abstract-Conference.html)
  - Tsinghua University、Shanghai Qi Zhi Institute、OpenPsi；Zhiyu Mei、Wei Fu、Kaiwei Li 等
  - ReaL 面向 RLHF 中 actor、critic、reward、reference 多个 LLM 交替 rollout 和训练的复杂 workflow。execution plan 为每阶段分别指定设备、parallelism 和资源份额，轻量 estimator 搜索计划；runtime 在阶段切换时重新分布参数，使 rollout 与 update 不再被一套固定并行方式束缚。70B、128 GPU 上最高加速 3.58 倍，长上下文计划较 Megatron 启发式平均快 81%。
  - 相较为全部 RLHF 模型和阶段固定同一种 3D parallel，核心创新是通过 parameter reallocation 在工作流内部动态改变并行布局，并自动联合搜索各阶段计划。
  - RLHF 训练系统、Parameter Reallocation、多模型 Workflow、并行计划搜索

- [Interference-aware Edge Runtime Prediction with Conformal Matrix Completion](https://proceedings.mlsys.org/paper_files/paper/2025/hash/40b8fb4f90004405e14b1ede6ab42373-Abstract-Conference.html)
  - Carnegie Mellon University、Robert Bosch GmbH、Polytechnic Institute of Porto；Tianshu Huang、Arjun Ramesh、Emily Ruppel 等
  - 该工作预测异构 edge device 上多个 workload 共置时的 runtime，但历史“设备×任务×干扰组合”矩阵非常稀疏且难以全面插桩。方法以 matrix factorization 补全缺失性能，并用 conformal prediction 给每个预测提供有覆盖保证的不确定区间，从而可在资源 provisioning 时识别风险；24 类设备的 WebAssembly 数据上误差 5.2%，约为朴素既有方法的一半。
  - 相较只输出点估计或要求每种共置组合都 profile，核心创新是把干扰感知矩阵补全与分布无关的不确定性校准结合。
  - 边缘性能预测、多租户干扰、Conformal Prediction、Matrix Completion

- [DiffServe: Efficiently Serving Text-to-Image Diffusion Models with Query-Aware Model Scaling](https://proceedings.mlsys.org/paper_files/paper/2025/hash/414fd191b3246a19a55741b938380136-Abstract-Conference.html)
  - University of Massachusetts Amherst、Adobe Research；Sohaib Ahmad、Qizheng Yang、Haoliang Wang 等
  - DiffServe 为在线 text-to-image 请求在多个质量/成本不同的 diffusion model variant 间路由。系统先自动构建 model cascade，估计 prompt 难度后让容易请求在轻量模型提前获得合格图像、困难请求升级到更强模型，并随 QPS 波动调整各模型副本；相较单模型 serving，在 latency violation 降低 19%–70% 的同时，响应质量最高提高 24%。
  - 相较为全部 prompt 固定部署同一个 diffusion model，核心创新是把 query-aware cascade 与在线副本伸缩共同用于生成质量和 SLO 的联合控制。
  - 文生图 Serving、Query-Aware Model Cascade、动态扩缩容、Quality-SLO Tradeoff

- [ProtoRAIL: A Risk-cognizant Imitation Agent for Adaptive vCPU Oversubscription In the Cloud](https://proceedings.mlsys.org/paper_files/paper/2025/hash/42e2b24104bc92d724ce45c0c2f91e1d-Abstract-Conference.html)
  - Microsoft；Lu Wang、Mayukh Das、Fangkai Yang 等
  - ProtoRAIL 是控制云主机 vCPU oversubscription margin 的 imitation-learning agent，不是 LLM Agent。它从历史专家策略学习随时间和利用率变化的超卖动作，利用负载模式近似对称性共享经验，并在 active knowledge-in-the-loop 模块检测高风险状态、请求专家纠正；Microsoft 内部部署将过载风险降低约 90 倍，同时回收 7%–10% stranded capacity。
  - 相较固定超卖阈值或无保护的 learned policy，核心创新是把原型化模式泛化与主动专家门控结合，在资源收益之外显式控制尾部风险。
  - ML for Systems—vCPU 超卖、风险感知模仿学习、Human-in-the-Loop、云容量管理

- [APOLLO: SGD-like Memory, AdamW-level Performance](https://proceedings.mlsys.org/paper_files/paper/2025/hash/437bc4ccafd3fc6d4289bd10940be42b-Abstract-Conference.html)
  - The University of Texas at Austin、Meta AI；Hanqing Zhu、Zhenyu Zhang、Wenyan Cong 等
  - APOLLO 研究 AdamW 逐参数 adaptive learning rate 的冗余，将其粗化为 channel-wise scaling，并用随机投影得到的低秩辅助 optimizer state 近似；APOLLO-Mini 进一步使用 tensor-wise rank-1 state，使内存接近 SGD 而保持接近 AdamW 的预训练表现。节省的显存可把 batch 放大 4 倍，在 8×A100 上吞吐约提高 3 倍，并支持单卡不足 12 GB 训练 7B。
  - 相较 GaLore 依赖频繁 SVD、Adam-mini 仍保留较大 momentum，核心创新是发现结构化学习率缩放对极低 rank 状态容忍，从而用纯随机投影近似而无需昂贵分解。
  - LLM Memory-Efficient Optimizer、低秩优化状态、随机投影、单卡预训练

- [AI Metropolis: Scaling Large Language Model-based Multi-Agent Simulation with Out-of-order Execution](https://proceedings.mlsys.org/paper_files/paper/2025/hash/4f31327e046913c7238d5b671f5d820e-Abstract-Conference.html)
  - Stanford University、Georgia Institute of Technology；Zhiqiang Xie、Hao Kang、Ying Sheng 等
  - AI Metropolis 是 LLM multi-agent simulation runtime，目标是加速大量 Agent 在社会或游戏环境中的交互，而不修改各 Agent 的规划策略。调度器动态追踪消息、环境读写形成的真实依赖，让没有因果关系的 Agent step 越过全局 barrier 乱序执行；相较每轮同步或保守并行，速度提高 1.3–4.15 倍，Agent 数量增大时接近理论最优。
  - 相较按 simulation round 对所有 Agent 做全局同步，核心创新是把 CPU 式 out-of-order dependency tracking 引入 Agent 交互调度，消除伪依赖而保持模拟语义。
  - Agent Infra—多 Agent 仿真、Out-of-Order Scheduling、依赖追踪、并行执行

- [The Hidden Bloat in Machine Learning Systems](https://proceedings.mlsys.org/paper_files/paper/2025/hash/5321b1dabcd2be188d796c21b733e8c7-Abstract-Conference.html)
  - Chalmers University of Technology；Huaifeng Zhang、Ahmed Ali-Eldin
  - Negativa-ML 分析 ML framework 运行时实际触达的 CPU/GPU shared-library code，并删除对给定 workload 永不使用的 feature、kernel 和依赖。它特别处理传统 debloater 看不到的 GPU binary，在 4 个框架、10 个 workload、300 多个 library 上发现 GPU code 是主要膨胀源；GPU/CPU code 分别最高缩小 75%/72%，并降低峰值内存和执行时间。
  - 相较通用软件 debloating 只追踪 host code，核心创新是跨 CPU 与 GPU library 恢复 ML workload 的实际可达代码，使设备 kernel 也能安全裁剪。
  - ML Framework Debloating、GPU Binary Analysis、依赖裁剪、运行时 Footprint

- [PipeFill: Using GPUs During Bubbles in Pipeline-parallel LLM Training](https://proceedings.mlsys.org/paper_files/paper/2025/hash/53d3f45797970d323bd8a0d379c525aa-Abstract-Conference.html)
  - Carnegie Mellon University、Amazon Web Services；Daiyaan Arfeen、Zhen Zhang、Xinwei Fu 等
  - PipeFill 不改变主 LLM 的 pipeline schedule，而是把其他待执行的小作业塞进其 15%–60% 的 bubble。系统测量每个 stage 的空闲时长和剩余显存，显式插入 bubble instruction，选择能在窗口内完成的 fill-job slice 并控制 context switch；主作业 slowdown 低于 2%，大规模训练 GPU 总利用率最高提高 63%，8K GPU 场景相当于额外完成约 2.6K GPU 的工作。
  - 相较只通过 micro-batch schedule 缩小 bubble，核心创新是把不可消除的空闲窗口暴露给集群作为可抢占资源，并按时间和显存双约束安全填充外部作业。
  - Pipeline Training、Bubble Harvesting、GPU 多租户、机会式调度

- [HyC-LoRA: Memory Efficient LoRA Fine-tuning with Hybrid Activation Compression](https://proceedings.mlsys.org/paper_files/paper/2025/hash/5431dca75a8d2abc1fb51e89e8324f10-Abstract-Conference.html)
  - Tsinghua University；Yujin Wang、Shunan Dong、Zongle Huang 等
  - HyC-LoRA 针对 LoRA 已缩小 optimizer/parameter 后仍占主导的 backward buffered activation，把几乎所有算子缓存压到约 2 bit。算子内部单独保存结构化 outlier，算子之间则重排/融合，让 LoRA adapter 补偿量化误差并选择性重计算难压 activation；集成现有框架后，在多种 Llama 下游微调中端到端显存最高减少 3.97 倍且精度损失可忽略。
  - 相较只压线性层 activation 或统一低比特存储，核心创新是用“outlier 保留 + LoRA 误差补偿 + selective recomputation”覆盖非线性模块的困难缓存。
  - LoRA Fine-Tuning、Activation Compression、Outlier Storage、选择性重计算

- [Radius: Range-based Gradient Sparsity for Large Foundation Model Pre-training](https://proceedings.mlsys.org/paper_files/paper/2025/hash/54dd9e0cff6d9214e20d97eb2a3bae49-Abstract-Conference.html)
  - Rutgers University；Mingkai Zheng、Zhao Zhang
  - Radius 在 data-parallel foundation model 预训练中利用大梯度位置随 step 变化缓慢的现象，不再每轮对整个 dense gradient 做 global top-k。它维护包含重要梯度的结构化 range，只通信这些连续区域，使后续阶段仍可使用稀疏表示；GPT-2B、64×A100、40% sparsity 时 step time 降低 21%、总预训练时间降低 19%，下游分数不降，而传统 top-k+AdamW 可能不收敛。
  - 相较逐元素 top-k 产生无结构索引并在后续恢复 dense tensor，核心创新是用时间稳定的连续 range 表示显著梯度，同时保留通信和算子可执行性。
  - Foundation Model 预训练、结构化梯度稀疏、Data Parallel Communication、收敛保持

- [XGrammar: Flexible and Efficient Structured Generation Engine for Large Language Models](https://proceedings.mlsys.org/paper_files/paper/2025/hash/5c20ca4b0b20b0bd2f1d839dc605e70f-Abstract-Conference.html)
  - Carnegie Mellon University、NVIDIA、Shanghai Jiao Tong University、University of California, Berkeley；Yixin Dong、Charlie F. Ruan、Yaxing Cai 等
  - XGrammar 为 LLM/Agent 生成 JSON、SQL、function call 和具身命令时执行 CFG constrained decoding。它预先检查与 parser state 无关的大部分 vocabulary token，只在运行时解释少量 context-dependent token；grammar expansion 减少后者，persistent stack 加速状态迁移，并把 CPU grammar check 与 GPU forward overlap。grammar engine 较既有方案快 10 倍以上，在 H100 serving 中接近零额外 latency。
  - 相较每生成一个 token 都遍历全词表并推进多个 parser stack，核心创新是把 token 合法性拆成可离线预判与必须在线解释两部分，并与推理引擎流水。
  - Agent Infra—Structured Generation、CFG Constrained Decoding、Function Calling、CPU-GPU Overlap

- [FlexAttention: A Programming Model for Generating Fused Attention Variants](https://proceedings.mlsys.org/paper_files/paper/2025/hash/61a9278dfef5f871b5e472389f8d6fa1-Abstract-Conference.html)
  - Meta、University of Michigan；Juechu Dong、Boyuan Feng、Driss Guessous 等
  - FlexAttention 让研究者用少量普通 PyTorch 函数描述 attention score modification 和 block mask，编译器再生成接近手写 FlashAttention 的 fused kernel。它覆盖 Alibi、document masking、PagedAttention 等变体，并允许多种 modification 组合，而无需为每个组合维护一套 CUDA；生成性能与对应手写 kernel 具有竞争力。
  - 相较单体 FlashAttention kernel 或为每种 mask/score 组合重新手写 Triton/CUDA，核心创新是找到既保留融合机会、又足以表达多数 attention 变体的高层编程接口。
  - Attention 编程模型、Fused Kernel Generation、PyTorch Compiler、组合式 Mask

- [NEO: Saving GPU Memory Crisis with CPU Offloading for Online LLM Inference](https://proceedings.mlsys.org/paper_files/paper/2025/hash/66a026c0d17040889b50f0dfa650e5e0-Abstract-Conference.html)
  - Peking University、University of California, Berkeley、University of California, Davis、Harvard University；Xuanlin Jiang、Yang Zhou、Shiyi Cao 等
  - NEO 用本机 CPU 同时承接部分 attention computation 和 KV Cache，使在线 LLM serving 能扩大 GPU batch，而非仅把状态放到主存后再传回 GPU。asymmetric CPU-GPU pipeline 适配两侧不同速度，load-aware scheduler 依据模型、序列长度、batch 和 CPU 能力分配工作；在 T4/A10G/H100 及 7B–70B 上保持 latency 时吞吐最高提高 7.5 倍，强 CPU 的 A10G 场景提高 79.3%。
  - 相较 CPU 只充当 KV/权重交换空间，核心创新是让 offloaded attention 在 CPU 原地计算，并用非对称流水主动平衡 CPU、GPU 的计算和内存压力。
  - 在线 LLM Serving、CPU Attention Offload、KV Cache、异构流水

- [AdaParse: An Adaptive Parallel PDF Parsing and Resource Scaling Engine](https://proceedings.mlsys.org/paper_files/paper/2025/hash/678773d96b5822e93348aeb5c80d4dc5-Abstract-Conference.html)
  - University of Chicago、Argonne National Laboratory；Carlo Siebenschuh、Kyle Hippe、Ozan Gokdemir 等
  - AdaParse 为构建科学语料库逐文档选择 PDF parser：便宜 heuristic 处理简单版面，昂贵 ML parser 处理复杂或损坏文档。科学家偏好用于 DPO 训练质量预测器，调度器再根据预测准确率、各 parser 的 CPU/GPU 需求和当前资源并行分配；1,000 篇文档上质量略高 0.2% 的同时吞吐提高 17 倍，可扩展到 trillion-token corpus。
  - 相较给全部 PDF 固定使用最强或最快 parser，核心创新是把人类质量偏好与 parser resource profile 联合成逐文档模型选择和弹性调度问题。
  - 科学 PDF 数据管线、Parser Routing、DPO 偏好对齐、异构资源调度

- [FlexInfer: Flexible LLM Inference with CPU Computations](https://proceedings.mlsys.org/paper_files/paper/2025/hash/698cfaf72a208aef2e78bcac55b74328-Abstract-Conference.html)
  - Georgia Institute of Technology、Meta、University of California San Diego、Intel Labs；Seonjin Na、Geonhwa Jeong、Byung Hoon Ahn 等
  - FlexInfer 面向单 GPU 显存和 CPU memory 均有限的 LLM 推理，允许 prefill 与 decode 分别选择 GPU-only、CPU compute、权重/KV offload 等 execution policy。performance estimator 以硬件带宽/算力、sequence length 和 batch size 为输入，在运行时为两个 phase 选策略；两种服务器上相对 FlexGen 平均端到端 latency 分别降低 75% 和 76%。
  - 相较整个请求固定采用同一 CPU-GPU offload 比例，核心创新是认识到 prefill 与 decode 瓶颈不同，并按运行时形状独立切换两阶段执行策略。
  - 资源受限 LLM 推理、Phase-Specific Offload、CPU-GPU Execution、性能估计

- [Know Where You’re Uncertain When Planning with Multimodal Foundation Models: A Formal Framework](https://proceedings.mlsys.org/paper_files/paper/2025/hash/703f727ec10190b2fddcf8e24f52df48-Abstract-Conference.html)
  - The University of Texas at Austin；Neel P. Bhatt、Yunhao Yang、Rohan Siva 等
  - 该框架把具身/机器人 foundation model 的失败拆成视觉 perception uncertainty 与 plan decision uncertainty。前者用 conformal prediction 校准，后者用 formal-methods-driven prediction 检查计划满足规范的稳健性；系统对高感知不确定场景主动重新观测，对高决策不确定样本自动筛出高置信数据再微调。在真实与模拟机器人任务中，输出波动最高降低 40%，成功率提高 5%。
  - 相较用单一 confidence 混合表示“没看清”和“不会规划”，核心创新是分别量化两种不确定性，并触发不同的闭环干预动作。
  - Agent System—多模态规划、不确定性分解、主动感知、形式验证反馈

- [Supply-Chain Attacks in Machine Learning Frameworks](https://proceedings.mlsys.org/paper_files/paper/2025/hash/75bb91b908e6924763c9f2bbe87e921e-Abstract-Conference.html)
  - University of Wisconsin-Madison、Google DeepMind；Yue Gao、Ilia Shumailov、Kassem Fawaz
  - 该工作展示一种针对 Python ML framework 供应链的攻击：恶意依赖或看似正常的代码不必直接窃取数据，而可悄悄降低训练后模型的 robustness。作者同时用 LLM 辅助分析 GitHub 前 50 个 ML 项目的安全讨论，发现其 supply-chain awareness 并未高于普通开源社区，说明传统 package/CI 风险会转化为 ML 特有的模型质量破坏。
  - 相较只研究权重后门或传统依赖执行任意代码，核心创新是连接软件供应链注入与模型稳健性退化，并从生态讨论量化防护认知缺口。
  - ML Supply-Chain Security、Python 依赖攻击、模型稳健性破坏、开源生态测量

- [Context Parallelism for Scalable Million-Token Inference](https://proceedings.mlsys.org/paper_files/paper/2025/hash/78834433edc3291f4c6cbbd2759324db-Abstract-Conference.html)
  - Meta；Amy Yang、Jingyi Yang、Aya Ibrahim 等
  - 该工作把单个超长请求的 context token 分到最多 128 张 H100，并设计两种精确 ring attention：pass-KV 适合完整 prefill，pass-Q 覆盖持久 KV prefill 与 decode，使通信消息和显存随场景选择。Llama3-405B 的 1M context prefill 在 16 节点上用 77 s 完成，parallel efficiency 93%、FLOPS utilization 63%，在 RDMA 和 TCP 网络上均接近线性扩展。
  - 相较 tensor parallel 主要分模型权重、pipeline parallel 主要提吞吐，核心创新是直接沿单请求 context 维度扩展，并以双 ring variant 适配不同 KV 生命周期和网络条件。
  - Million-Token Inference、Context Parallelism、Ring Attention、跨节点 Prefill

- [Marconi: Prefix Caching for the Era of Hybrid LLMs](https://proceedings.mlsys.org/paper_files/paper/2025/hash/7c180af017258d239bac6248d1eb26ac-Abstract-Conference.html)
  - Princeton University、Amazon Web Services；Rui Pan、Zhuang Wang、Zhen Jia 等
  - Marconi 为 attention 与 SSM/recurrent layer 混合的 LLM 提供 prefix cache。由于 recurrent state 原地更新，部分前缀命中不能像纯 Transformer KV 那样任意 rollback，系统对候选 cache entry 预测 exact/partial 等不同命中概率，并用“可节省计算/占用内存”而非 recency 决定 admission 和 eviction；跨多种 workload，token hit rate 最高提高 34.4 倍，TTFT 最多降低 71.1% 或 617 ms。
  - 相较把纯 Transformer 的 LRU prefix cache 直接套到 hybrid model，核心创新是把 recurrent state 的不可回滚语义纳入命中分类和价值估计。
  - Hybrid LLM Serving、Prefix Cache、SSM Recurrent State、价值感知淘汰

- [Venn: Resource Management For Collaborative Learning Jobs](https://proceedings.mlsys.org/paper_files/paper/2025/hash/7fd522b89ac21009b7bbe7560a9a5add-Abstract-Conference.html)
  - University of Michigan、University of Illinois Urbana-Champaign；Jiachen Liu、Fan Lai、Eric Ding 等
  - Venn 中的 Auxo resource manager 在多个 collaborative/federated learning job 之间分配短暂上线且硬件异构的 edge client。它先求解 Intersection Resource Scheduling，识别不同作业对同一设备集合的重叠需求并减少排队，再按设备速度、可用时间和作业需求匹配客户端以抑制 straggler；相较随机分配型管理器，平均 JCT 最高改善 1.88 倍。
  - 相较逐作业独立招募设备，核心创新是显式建模多个 CL job 的交集资源竞争，并把跨作业等待与作业内响应收集分别优化。
  - Collaborative Learning 调度、短暂在线设备、资源竞争、Straggler-Aware Matching

- [On Distributed Larger-Than-Memory Subset Selection With Pairwise Submodular Functions](https://proceedings.mlsys.org/paper_files/paper/2025/hash/8144a9d62e506af0fcdeac0e456b2710-Abstract-Conference.html)
  - ETH Zurich、Google；Maximilian Böther、Abraham Sebastian、Pranjal Awasthi 等
  - 该工作从数十亿样本中选择高价值训练子集，且目标 subset 本身也放不进任何单机 DRAM。分布式 bounding algorithm 迭代维护每个样本 pairwise submodular utility 的上下界，提前选定高价值点、丢弃无关点；仍未决的部分再用多轮 partitioned greedy 合并，并给出近似保证。算法在 CIFAR/ImageNet 保持集中式质量，并扩展到 130 亿点。
  - 相较要求 central coordinator 容纳全部候选 subset 的分布式 submodular selection，核心创新是用全分布式上下界逐轮缩小候选，移除单机内存上限。
  - 训练数据子集选择、分布式 Submodular Optimization、Larger-Than-Memory、迭代 Bounding

- [Lightweight Software Kernels and Hardware Extensions for Efficient Sparse Deep Neural Networks on Microcontrollers](https://proceedings.mlsys.org/paper_files/paper/2025/hash/8cb5b08f912600de3de07c6503599ba8-Abstract-Conference.html)
  - Politecnico di Torino、University of Bologna、ETH Zurich；Francesco Daghero、Daniele Jahier Pagliari、Francesco Conti 等
  - 该工作在超低功耗多核 RISC-V MCU 上执行 N:M pruned CNN/ViT。软件层为 1:8、1:16 等模式设计规则访存 sparse kernel，ISA 只增加间接 load 和 non-zero index 解压指令，面积开销约 5%；编译器再自动把完整网络映射到这些 kernel。单 kernel 较 dense 最高快 3.4 倍，ResNet18/ViT 端到端最高加速 3.21 倍，精度下降低于 1.5%。
  - 相较用通用稀疏格式拖累 MCU 或设计重型专用加速器，核心创新是以极小 ISA 扩展补齐 N:M kernel 的索引瓶颈，并打通编译器端到端部署。
  - TinyML 稀疏推理、RISC-V MCU、N:M Kernel、轻量 ISA 扩展

- [MiLo: Efficient Quantized MoE Inference with Mixture of Low-Rank Compensators](https://proceedings.mlsys.org/paper_files/paper/2025/hash/9032e5c9ec394ce768a2fa9bdc56af6c-Abstract-Conference.html)
  - University of Illinois Urbana-Champaign；Beichen Huang、Yueming Yuan、Zelei Shao、Minjia Zhang
  - MiLo 将 MoE expert 压到 3 bit 等极低精度，并为不同 dense/sparse 权重附加很小的 low-rank compensator 来恢复量化误差。系统根据各层/专家敏感度自适应选 rank、迭代优化 compensator，且不依赖 calibration dataset；配套 Tensor-Core-friendly 3-bit kernel 避免非标准位宽只省内存不省 latency，在多种 SoTA MoE 和任务上优于既有量化。
  - 相较统一 bit/rank 的 MoE quantization，核心创新是用 mixture of low-rank residual 专门补偿各 expert 的异质误差，并与可执行 3-bit kernel 共同设计。
  - MoE Quantization、Low-Rank Error Compensation、3-Bit Kernel、Calibration-Free

- [FastTree: Optimizing Attention Kernel and Runtime for Tree-Structured LLM Inference](https://proceedings.mlsys.org/paper_files/paper/2025/hash/96894468eb44631a32d7ebd56f9892c7-Abstract-Conference.html)
  - University of California San Diego、University of Pittsburgh、Amazon Web Services；Zaifeng Pan、Yitong Ding、Yue Guan 等
  - FastTree 面向 beam search、parallel sampling、Agent 分支等多个 query 共享树状 prefix 的推理。专用 attention kernel 一次读取 radix-tree 上公共 KV 并服务多个 query，runtime 再按实际树结构贪心分组、切开过长 context 以降低 tail；在 SGLang 上吞吐最高提高 2.2 倍，解决只共享存储却仍重复执行 attention 的问题。
  - 相较 radix-tree cache 只去除 KV 副本，核心创新是让 attention 计算本身理解树状共享，并联合选择适合 kernel 的 context-query group。
  - Tree-Structured LLM Inference、Prefix Sharing、Attention Kernel、Runtime Grouping

- [FedProphet: Memory-Efficient Federated Adversarial Training via Robust and Consistent Cascade Learning](https://proceedings.mlsys.org/paper_files/paper/2025/hash/96f39c8de84678cb2a908cd52bfd7819-Abstract-Conference.html)
  - Duke University、Accenture Cyber Labs；Minxue Tang、Yitu Wang、Jingyang Zhang 等
  - FedProphet 让显存受限 edge client 参与 federated adversarial training。客户端用带 strong-convexity regularization 的 adversarial cascade 分模块训练，避免完整大模型和对抗样本状态同时驻留；服务器根据 utility-robustness 平衡调 perturbation，并按客户端目标差异分配模块。相较低内存 FL 基线，它在减少 80% 内存、训练最高加速 10.8 倍时保持接近完整 FAT 的准确率与鲁棒性。
  - 相较单纯拆层训练导致 local/global model 不一致，核心创新是用可证明连接 robustness 与 consistency 的 cascade learning，再由服务器协调扰动和模块分配。
  - 联邦对抗训练、Cascade Learning、边缘显存、Robustness-Consistency

- [LAVA: Lifetime-Aware VM Allocation with Learned Distributions and Adaptation to Mispredictions](https://proceedings.mlsys.org/paper_files/paper/2025/hash/9de62e421d58234dbf773abf43268630-Abstract-Conference.html)
  - Google、Google DeepMind；Jianheng Ling、Pratik Worah、Yawen Wang 等
  - LAVA 用 VM lifetime distribution 而非单一结束时间预测来做数据中心 host placement。运行过程中一旦观测到 VM 超过预测寿命，系统重新估计 VM/host 剩余 lifetime、迁移或调整 placement，并把 defragmentation 和定期 maintenance drain 也纳入决策；因此短 VM 可集中释放整机，长 VM 则减少未来迁移，对误预测的适应优于 one-shot lifetime scheduling。
  - 相较提交时预测一次寿命并固定放置，核心创新是利用生存过程的新证据持续重预测，并把放置、碎片整理与维护窗口统一到 lifetime-aware 策略。
  - ML for Systems—VM 放置、Lifetime Distribution、在线重预测、数据中心碎片整理

- [Scaling Deep Learning Training with MPMD Pipeline Parallelism](https://proceedings.mlsys.org/paper_files/paper/2025/hash/9f73d65a4186198152357be871345771-Abstract-Conference.html)
  - NVIDIA；Anxhelo Xhebraj、Sean Lee、Hanfeng Chen、Vinod Grover
  - JaxPP 让用户在 JAX 中直接定义 gradient accumulation 的 pipeline schedule，把每个 stage 表示为独立 SPMD task，再由系统自动放到集群 mesh、推导跨 stage 通信。MPMD runtime 异步运行这些形状和程序不同的 SPMD task，避免整个 pipeline 被编译为一份僵硬的全局 SPMD 程序；硬件利用率较最佳 SPMD 配置最高提高 1.16 倍。
  - 相较只支持少数内置 schedule 的 SPMD pipeline，核心创新是以 MPMD 组合异步 SPMD stage，在保留自动 sharding 的同时开放用户级 schedule 编程。
  - JAX 分布式训练、MPMD Pipeline、可编程 Schedule、异步 SPMD Runtime

- [ScaleFusion: Scalable Inference of Spatial-Temporal Diffusion Transformers for High-Resolution Long Video Generation](https://proceedings.mlsys.org/paper_files/paper/2025/hash/a2fe4bb50fc6f3564cee1551d6309fea-Abstract-Conference.html)
  - University of Toronto、Amazon Web Services；Jiacheng Yang、Jun Wu、Zhen Zhang 等
  - ScaleFusion 加速 1080p、20 秒长视频 ST-DiT 的多机推理。它利用 spatial attention 与 temporal attention 的不同通信维度，在层内切分/流水 collective，并跨相邻层重排通信，使跨机传输被另一维 attention 计算覆盖；32×A100 对 8×A100 强扩展 3.60 倍，较 Ulysses/RingAttention 等平均加速 1.36 倍、最高 1.58 倍。
  - 相较把通用 sequence parallel 直接用于时空 token，核心创新是按 spatial/temporal attention 交替结构联合设计层内与层间通信 schedule。
  - 视频扩散 Transformer、Sequence Parallelism、跨机通信隐藏、长视频生成

- [Lumos: Efficient Performance Modeling and Estimation for Large-scale LLM Training](https://proceedings.mlsys.org/paper_files/paper/2025/hash/a66caa1703fe34705a4368c3014c1966-Abstract-Conference.html)
  - Cornell University、Meta、MIT；Mingyu Liang、Hiwot Tadese Kassa、Wenyin Fu 等
  - Lumos 从真实 LLM 训练 trace 恢复算子、通信和等待事件，建立可重放的 execution model，并把已有配置上的测量迁移到新模型规模、并行方案和集群设置。它不需要在每个候选上完整跑训练，在最高 512×H100 的生产集群上平均 3.3% 误差复现 execution time，同时输出更细的 runtime 行为以定位瓶颈和探索部署空间。
  - 相较只累加 microbenchmark latency 或只能回放原 trace，核心创新是用 trace-driven 模型同时保持事件依赖细节和跨配置估计能力。
  - LLM 训练性能建模、Trace Replay、配置估计、生产集群诊断

- [Self-Data Distillation for Recovering Quality in Pruned Large Language Models](https://proceedings.mlsys.org/paper_files/paper/2025/hash/af2d9fb5bcee19ef2dfa70d843520c97-Abstract-Conference.html)
  - Cerebras Systems、University of Calgary；Vithursan Thangarasa、Ganesh Venkatesh、Mike Lasby 等
  - 该工作在结构化删除 LLM decoder block 后，用原始未剪枝模型自己生成语义丰富的 fine-tuning dataset，恢复推理能力并减轻普通 SFT 对基础知识的 catastrophic forgetting。Llama3.1-8B 删除 6/32 层、参数降到 6.72B 后保留原模型 91.2% 准确率，而普通 SFT 为 81.7%；实际 FLOPs 降低 16.3%，剪枝模型还可充当 speculative drafter 提高接受率。
  - 相较用外部指令数据直接 SFT 剪枝模型，核心创新是让 teacher 生成贴近自身知识分布的数据，专门同时修复 pruning loss 与 SFT distribution shift。
  - LLM Structured Pruning、Self-Data Distillation、质量恢复、Speculative Drafter

- [Efficient LLM Inference using Dynamic Input Pruning and Cache-Aware Masking](https://proceedings.mlsys.org/paper_files/paper/2025/hash/afd6374c7f2839cba22f537f15f4f760-Abstract-Conference.html)
  - Qualcomm AI Research；Marco Federici、Davide Belli、Mart Van Baalen 等
  - DIP 面向 DRAM bandwidth 受限的移动端 SwiGLU LLM decode，在每个输入上按 magnitude 动态跳过 FFN activation，但无需另训 sparsity predictor；少量 fine-tuning 和 LoRA 可恢复误差。cache-aware mask 还联合考虑 activation 大小与当前 cache line，使保留元素更集中、提高命中率；Phi-3-Medium 上内存流量降 46%、吞吐增 40%，perplexity 增量低于 0.1。
  - 相较依赖 ReLU 天然零值或预测下一层稀疏模式，核心创新是无预测器地产生 SwiGLU 输入相关稀疏，并让 mask 服从真实 cache locality 而非只追求稀疏率。
  - 移动端 LLM、Dynamic Input Pruning、Cache-Aware Sparsity、SwiGLU

- [Efficient On-Device Machine Learning with a Biologically-Plausible Forward-Only Algorithm](https://proceedings.mlsys.org/paper_files/paper/2025/hash/b0131b6ee02a00b03fc3320176fec8f5-Abstract-Conference.html)
  - Lund University；Baichuan Huang、Amir Aminifar
  - Bio-FO 是不保存标准 backprop 反向图的 forward-only 学习算法，目标是在 wearable/Jetson 等设备本地更新模型。它以生物可解释的局部前向信号训练各层，并针对既有 forward-forward 类方法的准确率和扩展性不足改进 objective；在医学 wearable 数据和 mini-ImageNet 上优于其他 forward-only 算法，并在 Jetson Nano 验证真实能效。
  - 相较把 forward-only 仅作为生物学习概念验证，核心创新是设计可扩展到较大数据和端侧硬件的训练规则，并同时以任务准确率与设备效率验证。
  - 端侧训练、Forward-Only Learning、生物可解释算法、Wearable ML

- [Optimizing LLM Queries in Relational Data Analytics Workloads](https://proceedings.mlsys.org/paper_files/paper/2025/hash/b5dc49f44db2fadc5c4d717c57f4a424-Abstract-Conference.html)
  - University of California, Berkeley、Technical University of Munich、Stanford University；Shu Liu、Asim Biswal、Amog Kamsetty 等
  - 该工作优化“对关系表每一行调用 LLM”的 batch analytics。执行器重新排列 row 顺序，让共享值或文本前缀的记录相邻，并重排同一 row 内 field 顺序以制造更长公共 prefix，从而让现有 serving engine 直接复用 KV Cache；无需修改模型，在多类 Llama3 查询上 JCT 最高改善 3.4 倍，按 OpenAI/Anthropic 计价最多节省 32%。
  - 相较只增大 inference batch 或逐行独立发请求，核心创新是把关系代数中的行列重排转化为 LLM prefix-cache locality 优化。
  - LLM 数据分析、关系查询重排、KV Cache 复用、批处理成本

- [SOLA: Optimizing SLO Attainment for Large Language Model Serving with State-Aware Scheduling](https://proceedings.mlsys.org/paper_files/paper/2025/hash/bc82dbfbfa43232be85b8d9838f49c3e-Abstract-Conference.html)
  - Tsinghua University、Infinigence AI、Shanghai Jiao Tong University、Peking University；Ke Hong、Xiuhong Li、Lufang Chen 等
  - SOLA 在每个 decode iteration 决定哪些请求先执行、这一轮接纳多少 workload，而不是整条请求固定 FCFS。scheduler 同时读取单请求已等待时间、prefill/decode 进度和 TTFT/TPOT slack，以及系统当前 batch、负载与资源状态，在首 token 与后续 token、请求间公平性之间动态平衡；SLO attainment 从 45.5% 提到 99.4%，同约束下平均多服务 1.04–1.27 倍请求。
  - 相较全程使用同一 request-level priority，核心创新是形式化 iteration-level 调度空间，并融合 per-request 与 system-wide state 细粒度改变执行顺序和负载。
  - 在线 LLM 调度、Iteration-Level Scheduling、TTFT/TPOT SLO、State-Aware Control

- [ThunderServe: High-performance and Cost-efficient LLM Serving in Cloud Environments](https://proceedings.mlsys.org/paper_files/paper/2025/hash/c2a0e26dd9ee7d57e92bb1c24b39659a-Abstract-Conference.html)
  - University of Cambridge、Peking University、ETH Zurich；Youhe Jiang、Fangcheng Fu、Xiaozhe Yao 等
  - ThunderServe 在云上型号、价格和互联带宽不同的 GPU 中规划 LLM serving，选择每个模型阶段放在哪些 GPU、采用何种并行与请求调度，使同一预算下兼顾 throughput 和 latency deadline。运行时监测 node failure 与 workload shift，用轻量 re-scheduling 调整部署而不重启全部服务；异构云上吞吐最高提高 2.1 倍、平均 1.7 倍，deadline violation 最高降低 2.5 倍。
  - 相较假设同构高端 GPU 并在负载变化时重新部署，核心创新是把 GPU 性能/价格与网络异构共同纳入初始 plan，并支持不中断服务的在线局部重配置。
  - 异构云 LLM Serving、部署规划、Network-Aware Scheduling、在线重配置

- [TileLink: Generating Efficient Compute-Communication Overlapping Kernels using Tile-Centric Primitives](https://proceedings.mlsys.org/paper_files/paper/2025/hash/c6ee784cbe46d854843e4c883a3321ef-Abstract-Conference.html)
  - ByteDance Seed；Size Zheng、Jin Fang、Xuegui Zheng 等
  - TileLink 编译生成把 collective communication 融进矩阵计算的 multi-GPU kernel。前端分别表达 compute tile 与 communication tile，并用 tile-centric primitive 连接依赖，后端再降为底层传输指令、安排 producer/consumer 流水；程序员不必手写高风险 fused kernel，又避免 operator decomposition 的 launch 和同步开销。相对不重叠基线加速 1.17–20.76 倍，接近专用 overlap library。
  - 相较在算子层拆分计算通信或手工融合 NCCL/device code，核心创新是用 tile 作为二者共同编译单位，在保持设计空间解耦时自动生成细粒度融合。
  - 多 GPU Kernel 编译、计算通信重叠、Tile-Centric DSL、Collective Fusion

- [Seesaw: High-throughput LLM Inference via Model Re-sharding](https://proceedings.mlsys.org/paper_files/paper/2025/hash/cbc4ab80cd77aa0eb87da062fbcddb46-Abstract-Conference.html)
  - University of Toronto、Vector Institute、CentML、Stanford University；Qidong Su、Wei Zhao、Xin Li 等
  - Seesaw 服务离线/吞吐导向 LLM workload，在 prefill 和 decode 之间动态改变 model sharding，因为前者计算密集、后者受 memory/batching 约束。tiered KV buffer 在不同层级保留状态，transition-minimizing scheduler 聚合相同 phase 的工作，降低反复 reshard 权重和切换开销；相较 vLLM 吞吐平均提高 1.36 倍、最高 1.78 倍。
  - 相较整个 serving 生命周期固定 tensor/pipeline parallel，核心创新是允许模型在 phase 边界重分片，并用 KV 分层与调度共同摊薄转换成本。
  - LLM Model Re-sharding、Prefill-Decode Phase、KV Tiering、吞吐调度

- [LServe: Efficient Long-sequence LLM Serving with Unified Sparse Attention](https://proceedings.mlsys.org/paper_files/paper/2025/hash/cc8c6b9d89f7a898a29f58869b238e46-Abstract-Conference.html)
  - MIT、Shanghai Jiao Tong University、NVIDIA；Shang Yang、Junxian Guo、Haotian Tang 等
  - LServe 用同一套硬件友好 block sparsity 同时加速长序列 prefill 和 decode。部分 attention head 转成近乎零成本的 streaming head；其余 head 在 prefill 使用静态/动态模式组合，decode 则依据当前 query similarity 分层选择固定数量 KV page，使 cache 不随 context 无界增长。Llama3-8B 相对 TensorRT-LLM，prefill 平均加速 2.4 倍、decode 最高 3.3 倍并保持长上下文准确率。
  - 相较分别设计 prefill sparse attention 与 decode KV eviction，核心创新是统一两阶段的结构化稀疏表示，使 head streaming 与 page pruning 的收益可乘性组合。
  - 长序列 Serving、Unified Sparse Attention、Streaming Head、KV Page Selection

- [AIOpsLab: A Holistic Framework to Evaluate AI Agents for Enabling Autonomous Clouds](https://proceedings.mlsys.org/paper_files/paper/2025/hash/d1f9e4a9f109b6e8b75ed362736f22ec-Abstract-Conference.html)
  - University of Illinois Urbana-Champaign、University of California Berkeley、Microsoft、Indian Institute of Science；Yinfang Chen、Manish Shetty、Gagan Somashekar 等
  - AIOpsLab 是面向云运维 Agent 的可执行评测环境，不直接提出新的故障处理 Agent。框架部署可控 cloud environment、生成 workload、注入 fault、导出 logs/metrics/traces，并给 Agent 提供观察和操作接口，以端到端 incident lifecycle 评估 detection、localization、root-cause analysis 和 mitigation；作者用多种 LLM Agent 展示它们在复杂运维任务上的能力边界。
  - 相较按静态日志数据集分别测单个 AIOps 算法，核心创新是把真实故障、遥测、Agent 动作和恢复结果闭环到可重复环境中，支持 AgentOps 全流程比较。
  - Agent Evaluation、Agent Infra—AIOps、故障注入、云运维闭环

- [MAS-Attention: Memory-Aware Stream Processing for Attention Acceleration on Resource-Constrained Edge Devices](https://proceedings.mlsys.org/paper_files/paper/2025/hash/d3cf1559a8795eb1ed2b3ad52409ac7d-Abstract-Conference.html)
  - University of Alberta、Huawei Technologies；Mohammadali Shakerdargah、Shan Lu、Chao Gao、Di Niu
  - MAS-Attention 在片上 cache 和计算单元很少的 edge NPU 上精确执行 attention。它把 matrix unit 与 vector unit 分成两个依赖流，用多级 tiling 搜索让 QK/GEMM、softmax 等向量操作并行，并把 I/O 代价纳入 tile factor；proactive cache overwrite 在数据最后一次使用后提前复用空间，避免 spill。模拟中最高加速 2.75 倍、能耗降 54%，真机最高加速 1.76 倍。
  - 相较为数据中心多核设计的 fused attention，核心创新是围绕异构计算单元和极小 cache 建立双流 schedule，并联合搜索 tiling 与缓存生命周期。
  - 边缘 Attention、Matrix-Vector 双流、Memory-Aware Tiling、Cache Overwrite

- [Training Ultra Long Context Language Model with Fully Pipelined Distributed Transformer](https://proceedings.mlsys.org/paper_files/paper/2025/hash/d5a655b8b373737b4f2aea8f78e5e754-Abstract-Conference.html)
  - The Ohio State University、Microsoft；Jinghan Yao、Sam Ade Jacobs、Masahiro Tanaka 等
  - FPDT 把超长 sequence 切成 chunk，并将 attention、前后向、activation/KV 移动沿 chunk 完全流水，使 context 所需状态不必一次驻留单卡。它可与已有 data/tensor parallel 组合，在相同硬件上把可训练 sequence length 提高 16 倍；仅 4 GPU 即可训练 8B 模型的 2M-token context，同时保持 55% 以上 MFU。
  - 相较依靠下游适配扩 context 或仅沿序列做普通 ring attention，核心创新是设计贯穿完整 Transformer 训练的 sequence-chunk pipeline，把计算、通信和显存占用同时摊开。
  - Ultra-Long-Context Training、Sequence Chunk Pipeline、分布式 Transformer、Activation Memory

- [FlashInfer: Efficient and Customizable Attention Engine for LLM Inference Serving](https://proceedings.mlsys.org/paper_files/paper/2025/hash/dbf02b21d77409a2db30e56866a8ab3a-Abstract-Conference.html)
  - University of Washington、NVIDIA、Perplexity AI、Carnegie Mellon University；Zihao Ye、Lequn Chen、Ruihang Lai 等
  - FlashInfer 是可嵌入 SGLang、vLLM、MLC-Engine 的 serving attention engine。block-sparse 与 composable format 统一不同 KV layout，JIT template 针对 GQA、paged KV、parallel generation 等场景生成 kernel；load-balanced scheduler 根据请求长度动态分工，同时保持 CUDA Graph 所需的静态 launch 形状。相较编译器后端 inter-token latency 降 29%–69%，长上下文 latency 降 28%–30%。
  - 相较为每种 serving pattern 维护独立手写 attention kernel，核心创新是把可组合 KV format、JIT 模板和兼容 CUDA Graph 的动态负载均衡合成通用 engine。
  - LLM Attention Engine、JIT Kernel、Paged/Block-Sparse KV、CUDA Graph

- [A Bring-Your-Own-Model Approach for ML-Driven Storage Placement in Warehouse-Scale Computers](https://proceedings.mlsys.org/paper_files/paper/2025/hash/e01c431bbb83153632c0dcfaf8ccda0a-Abstract-Conference.html)
  - The University of Texas at Austin、Google、Google DeepMind；Chenxi Yang、Yan Li、Martin Maas 等
  - 该工作在 Google warehouse-scale computer 中用 ML 决定数据放 SSD 还是 HDD，但不在 storage layer 维护一个难随 workload 更新的全局黑盒模型。每个 application 自行训练小型可解释 workload model，随 I/O 携带预测；存储层用统一 heuristic 将不同模型输出转成 placement，在工作负载变化时由应用独立更新。生产原型和 trace simulation 中 TCO savings 最高为既有方法的 3.47 倍。
  - 相较由存储系统集中训练单一 placement model，核心创新是把模型所有权上移到最了解语义的 workload，同时保留存储层可控、可解释的统一调度边界。
  - ML for Systems—存储放置、Bring-Your-Own-Model、SSD/HDD Tiering、跨层协同

- [COMET: Fine-grained Computation-communication Overlapping for Mixture-of-Experts](https://proceedings.mlsys.org/paper_files/paper/2025/hash/e27ea0cd50b798ff8942caf9203f0992-Abstract-Conference.html)
  - ByteDance Seed、Shanghai Jiao Tong University；Shulai Zhang、Ningxin Zheng、Haibin Lin 等
  - COMET 针对 MoE layer 中 token dispatch/All-to-All 可占 47% 时间的问题，从数据依赖图把 expert compute 和 communication 切成更细 task，重新排序并按运行时负载自适应分配，避免粗粒度 pipeline 为了重叠而降低 GEMM 效率。单层最高加速 1.96 倍，端到端平均 1.71 倍，并已在万卡级生产集群节省数百万 GPU 小时。
  - 相较按固定 chunk 粗粒度交错 All-to-All 与 expert GEMM，核心创新是以依赖分析生成细粒度 schedule，并动态平衡各通信/计算 task 的大小。
  - MoE 训练与推理、Fine-Grained Overlap、All-to-All、生产万卡集群

- [Enabling Unstructured Sparse Acceleration on Structured Sparse Accelerators](https://proceedings.mlsys.org/paper_files/paper/2025/hash/e2ec2530db26b54d0b3b060c1e4a1bda-Abstract-Conference.html)
  - Georgia Institute of Technology、NVIDIA；Geonhwa Jeong、Po-An Tsai、Abhimanyu Rajeshkumar Bambhaniya 等
  - TASDER 让只支持固定 N:M pattern 的 accelerator 执行任意 unstructured sparse weight/activation。它利用线性代数分配律，把原稀疏 tensor 近似分解为一串符合硬件 pattern 的 structured tensor，再由软件选择分解数量和误差，无需针对目标硬件重新 fine-tune 模型；dense/sparse DNN 的 EDP 最高改善 83%/74%，真机最高加速 39%。
  - 相较强制把模型重新剪成某一种硬件结构，核心创新是在执行前用多个结构化分量表示任意稀疏模式，从而把模型 sparsity 与加速器 sparsity 解耦。
  - 稀疏加速器、Unstructured-to-Structured Decomposition、模型-硬件兼容、TASDER

- [VoLUT: Efficient Volumetric Streaming Enhanced by LUT-Based Super-Resolution](https://proceedings.mlsys.org/paper_files/paper/2025/hash/f189e7580acad0fc7fd45405817ddee3-Abstract-Conference.html)
  - University of Wisconsin-Madison、University of Southern California、Microsoft Research Asia；Chendong Wang、Anlan Zhang、Yifan Yang 等
  - VoLUT 在网络发送前下采样 3D volumetric video，移动端再用 lookup table 查询预计算的高分辨率局部模式完成 super-resolution，避免运行重型神经网络。ABR 根据实时带宽选择下采样率，联合控制传输量与重建质量；商品手机上可线速执行，带宽减少 70%、QoE 提高 36.7%，3D SR 加速 8.4 倍且质量不降。
  - 相较把 2D neural SR 逐帧迁移到点云/体素，核心创新是为 volumetric 邻域构造可查表的重建表示，并把 SR 计算成本纳入 ABR 决策。
  - 体积视频流、LUT Super-Resolution、移动端重建、Adaptive Bitrate

- [FLStore: Efficient Federated Learning Storage for Non-Training Workloads](https://proceedings.mlsys.org/paper_files/paper/2025/hash/f37347375d8b54e3203e5d24aeb6c58c-Abstract-Conference.html)
  - Virginia Tech、University of Minnesota、Queen Mary University of London；Ahmad Faraz Khan、Samuel Fountain、Ahmed M. Abdelmoniem 等
  - FLStore 服务 personalization、clustering、debugging、incentive 等需要跨轮读取大量 client update 和 metadata 的 FL 非训练任务。它在 serverless cache 上合并数据与 compute plane，让函数在缓存数据旁执行，并以定制 admission/eviction 和 locality routing 减少对象存储往返；相对 object-store aggregator，平均 latency 降 71%、成本降 92.45%，同时支持扩展与容错。
  - 相较让中央 aggregator 从远端对象存储拉取每轮状态，核心创新是把可弹性计算直接放进共享缓存数据路径，为非训练 FL workload 提供 locality-aware execution。
  - 联邦学习存储、Serverless Cache、Non-Training Workload、Data-Compute Colocation

- [TurboAttention: Efficient Attention Approximation for High-Throughput LLMs](https://proceedings.mlsys.org/paper_files/paper/2025/hash/f4f55846501f3336f293fd8b6de10770-Abstract-Conference.html)
  - Microsoft、Georgia Institute of Technology；Hao Kang、Srikant Bharadwaj、James Hensman 等
  - TurboAttention 让 attention 从 KV 读取到 QK、softmax、PV 都尽量保持低比特执行。FlashQ 按 head 量化 KV 和 activation-activation multiplication，SAS 利用 attention score 稀疏特征近似 softmax，避免先反量化到 FP32 再求指数；attention 加速 1.2–1.8 倍、KV 缩小 4.4 倍以上，最大 serving throughput 较 FP16 提高 2.37 倍。
  - 相较仅压 KV、但 attention 计算前必须恢复浮点，核心创新是把 quantized execution 延伸到 attention arithmetic 与 softmax，从而同时兑现带宽和计算收益。
  - Quantized Attention、KV Cache Compression、Softmax Approximation、低比特执行

- [QServe: W4A8KV4 Quantization and System Co-design for Efficient LLM Serving](https://proceedings.mlsys.org/paper_files/paper/2025/hash/fbe2b2f74a2ece8070d8fb073717bda6-Abstract-Conference.html)
  - MIT、University of Massachusetts Amherst、MIT-IBM Watson AI Lab、NVIDIA；Yujun Lin、Haotian Tang、Shang Yang 等
  - QServe 用 QoQ 将 weight/activation/KV 分别量化为 W4A8KV4，目标是大 batch 云端 serving 而非只在 batch-1 端侧省内存。progressive quantization 降低 W4A8 GEMM partial-sum 反量化，SmoothAttention 控制 KV4 误差；系统侧重排 weight 并用 register-level parallelism 避免低吞吐 CUDA-core 操作。相较 TensorRT-LLM，8B 吞吐最高提高 1.4 倍、72B 最高 3.5 倍，L40S 可超过 A100 基线。
  - 相较已有 INT4 在 GPU 上消耗 20%–90% 时间做 dequantization，核心创新是从量化公式到数据布局/kernel 共同消除低精度转换瓶颈，使 W4A8KV4 在高并发 serving 中获得实测加速。
  - 云端 LLM Serving、W4A8KV4、Progressive Quantization、GPU Kernel Co-Design
