# PPoPP 2025 论文列表

范围以 PPoPP 2025 官方 Main Conference program 和 ACM proceedings 交叉核对为准，共 38 篇主会长文；已从 parent DOI 下 50 项中排除 11 篇短 poster 和 1 篇 keynote。以下标题均链接至论文 DOI；已找到的 4 份合法公开 PDF 保存在 `reference/PPoPP/2025/`。

- [Helios: Efficient Distributed Dynamic Graph Sampling for Online GNN Inference](https://doi.org/10.1145/3710848.3710854)
  - Jie Sun, Zuocheng Shi (Zhejiang University, China)；Li Su, Wenting Shen, Yong Li, Wenyuan Yu, Wei Lin, Jingren Zhou (Alibaba Group)；Zeke Wang, Fei Wu (Zhejiang University, China and Shanghai Institute for Advanced Study of Zhejiang University, China)；Bingsheng He (National University of Singapore, Singapore)。
  - Helios 面向推荐、反欺诈等在线 GNN inference 的动态图 K-hop sampling，把随每次请求跨机遍历的工作前移为 graph update 触发的 event-driven pre-sampling；query-aware cache 按常见查询保留可拼装邻域，使请求在本机完成多跳 sample，并以更新事件维护新鲜度和毫秒级 P99 SLO。
  - 相较以图数据库按请求实时分布式采样，核心创新是把动态图采样从 request path 解耦，用更新驱动预计算与查询感知缓存同时削减数据倾斜尾延迟和跨机通信。
  - AI Infra、在线 GNN 推理、动态图采样、Query-Aware Cache、尾延迟 SLO

- [Accelerating GNNs on GPU Sparse Tensor Cores through N:M Sparsity-Oriented Graph Reordering](https://doi.org/10.1145/3710848.3710881)
  - Jou-An Chen, Hsin-Hsuan Sung, Ruifeng Zhang, Xipeng Shen (North Carolina State University)；Ang Li (Pacific Northwest National Laboratory and University of Washington)。
  - 该方法为 GNN adjacency matrix 做无损 vertex reordering，把原本不规则 nonzero 重新聚集成 Sparse Tensor Core 要求的 V:N:M/N:M vector pattern；重排同时保持邻接矩阵对称，因而 GNN 的 SpMM 和依赖对称性的图算法都无需补零近似或改变模型精度。
  - 相较让不规则图通过大量 zero padding 勉强适配 N:M、或只优化 kernel，核心创新是在图结构层面搜索兼顾硬件稀疏格式和矩阵对称性的排列，使绝大多数通用图可直接使用 SPTC。
  - GNN 推理、Sparse Tensor Core、N:M Sparsity、图重排、无损加速

- [Adaptive Parallel Training for Graph Neural Networks](https://doi.org/10.1145/3710848.3710883)
  - Kaihao Ma (The Chinese University of Hong Kong and AWS Shanghai AI Lab)；Renjie Liu (Southern University of Science and Technology and AWS Shanghai AI Lab)；Xiao Yan (Centre for Perceptual and Interactive Intelligence and AWS Shanghai AI Lab)；Zhenkun Cai, Xiang Song (Amazon)；Minjie Wang (AWS Shanghai AI Lab)；Yichao Li, James Cheng (The Chinese University of Hong Kong)。
  - APT 面向多 GPU GNN training，把 full-graph、partition、sampling 等并行策略统一为同一 execution abstraction；cost model 根据 graph size/degree、GNN layer、训练算法、GPU 数量和通信配置估计各策略时间，在任务启动时选择并配置最合适方案，而不是为所有 workload 固定一种并行法。
  - 相较各 GNN framework 只实现并长期使用单一策略，核心创新是以统一执行引擎承载多种策略，并通过可解释的任务/硬件成本模型自动选择。
  - AI Infra、GNN 训练、多 GPU、并行策略选择、成本模型

- [RT-BarnesHut: Accelerating Barnes-Hut Using Ray-Tracing Hardware](https://doi.org/10.1145/3710848.3710885)
  - Vani Nagarajan, Artem Pelenitsyn, Milind Kulkarni (School of Electrical and Computer Engineering, Purdue University, West Lafayette, IN, USA)；Rohan Gangaraju (Department of Computer Science, University of Texas at Austin, Austin, TX, USA)；Kirshanthan Sundararajah (Department of Computer Science, Virginia Tech, Blacksburg, VA, USA)。
  - RT-BarnesHut 把 n-body Barnes–Hut 的 octree traversal 重述为 ray 与由节点 bounding volume 组成的 BVH 相交：opening criterion 决定 ray 查询接受聚合质量还是继续下钻，NVIDIA OptiX/RT core 执行树遍历，shader 只做力累加，从而绕过 GPU SIMT 上分支发散严重的手写 traversal。
  - 相较为每种树算法编写 shader-core traversal，核心创新是建立 Barnes–Hut 访问语义到 ray-tracing primitive 的等价映射，直接复用固定功能 BVH 硬件。
  - N-Body、Barnes–Hut、Ray-Tracing Core、OptiX、树遍历加速

- [EVeREST: An Effective and Versatile Runtime Energy Saving Tool for GPUs](https://doi.org/10.1145/3710848.3710875)
  - Anna Yue, Pen-Chung Yew (Department of Computer Science, University of Minnesota, USA)；Sanyam Mehta (Hardware-software Codesign, Hewlett-Packard Labs, USA)。
  - EVeREST 以 application phase 为控制粒度，只读取跨 NVIDIA/AMD GPU 都可获得的少量 counter，在线判定 compute/memory/latency 特征并估计降频后的性能；controller 除传统 memory-bound 降 core clock 外还利用两类额外 DVFS 机会，在用户给定 slowdown bound 下选择 core/memory frequency 节能。
  - 相较依赖厂商专有大量 counter、只对 memory-bound phase 降核心频率的 DVFS 工具，核心创新是以极少事件做跨厂商相位识别和性能预测，并扩展可安全调频的场景。
  - GPU Runtime、DVFS、相位识别、性能保证、跨厂商节能

- [TurboFFT: Co-Designed High-Performance and Fault-Tolerant Fast Fourier Transform on GPUs](https://doi.org/10.1145/3710848.3710853)
  - Shixun Wu, Yujia Zhai, Jiajun Huang, Zizhe Jian, Huangliang Dai, Zizhong Chen (UC Riverside, Riverside, CA, USA)；Jinyang Liu (University of Houston, Houston, TX, USA)；Sheng Di, Franck Cappello (Argonne National Laboratory, Lemont, IL, USA)。
  - TurboFFT 用架构感知、无 padding 的 template kernel 按 FFT size 配置 register/shared-memory 数据流；同时在 thread 与 threadblock 两层为中间值嵌入 checksum，two-sided ABFT 加位置编码定位传播错误，multi-transaction block FFT 把校验规约与正常并行计算摊销，在运行中检测并纠正 soft error。
  - 相较 cuFFT 只追求性能、现有 ABFT 需额外 global-memory pass，核心创新是共同设计 FFT kernel 和分层双边校验，让在线纠错复用片上数据流而非事后重算。
  - FFT、GPU、Algorithm-Based Fault Tolerance、Soft Error、Kernel Co-Design

- [Reciprocating Locks](https://doi.org/10.1145/3710848.3710862)
  - Dave Dice, Alex Kogan (Oracle Labs, USA)。
  - Reciprocating Lock 面向 cache-coherent many-core，把到达线程挂到一个可常数时间交换的等待链，release 时反向交接局部批次；每线程无论同时持有多少锁只需一个 waiting element，等待者 local spin，并以 bounded bypass 限制非 FIFO 插队，从而降低持续竞争下的 cache-line ping-pong。
  - 相较 MCS/CLH 为每个 lock acquisition 分配 queue node、严格链式交接产生较多 coherence traffic，核心创新是可复用的线程级等待槽与 reciprocating 批次交接，兼顾常数 doorway/release 和抗饥饿。
  - 互斥锁、局部自旋、Cache Coherence、Bounded Bypass、Pthreads

- [Aggregating Funnels for Faster Fetch&Add and Queues](https://doi.org/10.1145/3710848.3710873)
  - Younghun Roh, Yuanhao Wei, Julian Shun (MIT CSAIL, USA)；Eric Ruppert (York University, Canada)；Panagiota Fatourou (FORTH ICS and University of Crete, Greece)；Siddhartha Jayanti (Google Research, USA)。
  - Aggregating Funnels 面向多个线程争用同一 fetch-and-add counter，把操作先分散到多条 funnel location；同一窗口内的请求组成 batch，由代表在全局位置执行一次硬件 FAA，各请求再在另一位置用局部 FAA 计算自己在 batch 内的返回值，并可替换并发 queue 的热点计数器。
  - 相较 combining funnel 由软件串行传播每个结果，核心创新是用第二次分散 FAA 并行算出 batch 内偏移，使一次全局原子操作服务一批请求而不新增中心 combiner。
  - Fetch-and-Add、Combining、并发队列、原子热点、可扩展同步

- [Fairer and More Scalable Reader-Writer Locks by Optimizing Queue Management](https://doi.org/10.1145/3710848.3710877)
  - Takashi Hoshino (Cybozu Labs, Inc., Tokyo, Japan)；Kenjiro Taura (The University of Tokyo, Tokyo, Japan)。
  - Freezer 扩展 MCS request list 的入队/冻结/解冻操作，使 reader-writer lock 可把一批兼容 reader 在不反复访问 mutex head 的情况下交接；fast path 与公平策略解耦，四项 queue-management 优化选择 reader batching、writer handoff 和请求回收方式，以提高吞吐并压低尾延迟。
  - 相较两阶段 MCS 变体虽免 heap allocation、仍让 fast path 竞争同一 mutex 且公平性被绑定，核心创新是可冻结的等待队列让批次选择在局部完成，并独立配置公平策略。
  - Reader-Writer Lock、MCS、Queue Management、公平性、尾延迟

- [Publish on Ping: A Better Way to Publish Reservations in Memory Reclamation for Concurrent Data Structures](https://doi.org/10.1145/3710848.3710890)
  - Ajay Singh, Trevor Brown (University of Waterloo, Canada)。
  - Publish-on-Ping 让 hazard-pointer/era reader 只在线程私有区记录正在访问的 node，不再每读一次就 publish reservation 加 memory fence；reclaimer 真要释放对象时用 POSIX signal ping 相关线程，后者才批量公开 reservation，未被保护的 retire list 延迟回收；EpochPOP 在常态走 epoch、停顿时回退该协议。
  - 相较 hazard pointer 把“可能发生回收”的成本放在每次读路径，核心创新是反转通知方向，只在真实回收需求出现时按需发布保护状态，并可作为现有 HP/HE 的 drop-in replacement。
  - Safe Memory Reclamation、Hazard Pointer、POSIX Signal、按需发布、无锁结构

- [AC-Cache: A Memory-Efficient Caching System for Small Objects via Exploiting Access Correlations](https://doi.org/10.1145/3710848.3710856)
  - Fulin Nan, Ronglong Wu, Zhirong Shen, Jiahui Yang, Yiming Zhang, Jiwu Shu (Xiamen University, Xiamen, China)；Li Cheng, Zheng Chen (Tencent Inc., Shenzhen, China)。
  - AC-Cache 从 56 条生产 trace 中提取小对象热度稳定性与 multi-get 共访关系；它先用 ILP 在节点间平衡热点访问和内存，再用紧凑统计生成细粒度 correlation group，以 max-flow 分散 group、启发式放置其余 key，使一次请求常用对象可在同节点 multi-get，同时避免热点节点。
  - 相较按单 key 热度独立分片或为对象保存昂贵关联图，核心创新是把访问相关性压成可放置 group，并分别用 ILP/max-flow联合优化尾延迟、访问均衡与缓存容量。
  - 云缓存、小对象、访问相关性、Multi-Get、对象放置、尾延迟

- [Effectively Virtual Page Prefetching via Spatial-Temporal Patterns for Memory-intensive Cloud Applications](https://doi.org/10.1145/3710848.3710865)
  - Yun Wang, Tianmai Deng, Zhixiang Wei, Yixiao Xu, Minglang Huang, Zhengwei Qi (Shanghai Jiao Tong University, Shanghai, China)；Liang Chen, Ben Luo, Yibin Shen (Alibaba Group, Hangzhou, China)。
  - vPrefetcher 面向内存复用/回收导致 guest page 再次 fault 的 VM，在 hypervisor 侧监控被回收页的访问地址和时间序列；Trend algorithm 结合空间邻近与时间重复模式预测下一批虚拟页，在应用触及前恢复/预取，并控制预取量以避免 reclaim 与无用 I/O 抵消收益。
  - 相较 Leap 等只沿地址 stride 预取、未区分云 VM 中被复用的物理内存，核心创新是针对虚拟化回收轨迹建立时空趋势模型，将预取触发和内存重用状态结合。
  - 虚拟机内存、页面预取、时空模式、内存回收、云应用

- [Harnessing Inter-GPU Shared Memory for Seamless MoE Communication-Computation Fusion](https://doi.org/10.1145/3710848.3710868)
  - Hulin Wang, Yaqi Xia, Dazhao Cheng (School of Computer Science, Wuhan University, Wuhan, China)；Donglin Yang (Nvidia Corporation, Santa Clara, USA)；Xiaobo Zhou (IOTSC, University of Macau, Macau S.A.R)。
  - CCFuser 面向 multi-GPU MoE training，把 token dispatch 的 All-to-All 替换为 inter-GPU shared-memory load；单个 fused kernel 同时读取本地/远端 token 并执行 expert GEMM，避免通信阶段和计算阶段割裂；当 expert 负载倾斜时，以保持统计等价的 graph transformation 重分配 expert 计算而不丢弃 token。
  - 相较先 All-to-All 再 GEMM 的粗粒度 overlap、或通过 capacity/drop token 缓解失衡，核心创新是用跨 GPU 共享内存把远端访问融合进 GEMM，并以等价重分配保持模型质量。
  - AI Infra、MoE 训练、Inter-GPU Shared Memory、通信计算融合、Expert Reassignment

- [FlashTensor: Optimizing Tensor Programs by Leveraging Fine-grained Tensor Property](https://doi.org/10.1145/3710848.3710864)
  - Runxin Zhong (Tsinghua University, Qingcheng.AI, Beijing, China)；Yuyang Jin, Chen Zhang, Kinman Lei, Shuangyu Li, Jidong Zhai (Tsinghua University, Beijing, China)。
  - FlashTensor 从 DNN computation graph 为每条 tensor 边标注 reduce dependency、broadcastability 等细粒度性质；编译器依据这些性质把 reduction/elementwise 变换重排或融合，并把算子映射到不必物化完整 long-context intermediate 的 kernel，减少 HBM footprint 和冗余计算。
  - 相较按算子名套固定 fusion pattern，核心创新是将张量语义性质作为可证明的优化条件，使跨算子 transformation 和 kernel mapping 能安全消除大中间张量。
  - AI Compiler、长上下文推理、Tensor Property、算子融合、中间张量消除

- [Mario: Near Zero-cost Activation Checkpointing in Pipeline Parallelism](https://doi.org/10.1145/3710848.3710878)
  - Weijian Liu, Mingzhen Li, Guangming Tan, Weile Jia (SKLP, Institute of Computing Technology, CAS, Beijing, China and University of Chinese Academy of Sciences, Beijing, China)。
  - Mario 面向 GPT-3/LLaMA2 pipeline training，联合搜索每段 activation 是否 checkpoint、microbatch pipeline schedule 和 stage memory；它把 recomputation 前移到原有 bubble，并用省下的显存预执行更多 forward，再由轻量 simulator 估计组合的时间/峰值显存，在分钟内找到均衡各 GPU 的方案。
  - 相较把 activation checkpointing 当作独立内存开关、重计算反而拉长 critical path，核心创新是将重计算和前向工作 tessellate 到 pipeline bubble，并与 schedule 自动联合优化。
  - AI Infra、LLM 训练、Pipeline Parallelism、Activation Checkpointing、Bubble Filling

- [COMPSO: Optimizing Gradient Compression for Distributed Training with Second-Order Optimizers](https://doi.org/10.1145/3710848.3710852)
  - Baixi Sun, Jiannan Tian, Jinda Jia, Daoce Wang, Boyuan Zhang (Indiana University, Bloomington, IN, USA)；Weijin Liu, Xiaodong Yu (Stevens Institute of Technology, Hoboken, NJ, USA)；J. Gregory Pauloski (University of Chicago, Chicago, IL, USA)；Mingkai Zheng, Zhao Zhang (Rutgers University, New Brunswick, NJ, USA)；Sheng Di, Kamil A. Iskra (Argonne National Laboratory, Lemont, IL, USA)；Sian Jin (Temple University, Philadelphia, PA, USA)；Pete Beckman (Northwestern University, Argonne National Laboratory, Lemont, IL, USA)；Guangming Tan, Dingwen Tao (University of Chinese, Academy of Sciences, Beijing, China)。
  - COMPSO 面向采用 second-order optimizer 的分布式 DNN training，在每轮根据 gradient magnitude 过滤小项，并用 stochastic rounding 量化保留项以控制无偏误差；GPU kernel 融合筛选、编码和通信 buffer 生成，性能模型依据网络/模型选择压缩配置，确保压缩计算成本小于减少的 collective 时间。
  - 相较为一阶 SGD 设计的 compressor 直接用于二阶更新会损失精度或压缩率，核心创新是针对 curvature-sensitive optimizer 联合设计随机舍入、稀疏过滤及端到端收益判定。
  - 分布式训练、二阶优化器、梯度压缩、Stochastic Rounding、GPU Kernel

- [WeiPipe: Weight Pipeline Parallelism for Communication-Effective Long-Context Large Model Training](https://doi.org/10.1145/3710848.3710869)
  - Junfeng Lin, Rong Zhao (Tsinghua University, Beijing, China)；Ziming Liu, Yang You (National University of Singapore, Singapore)；Jun Wang (CETHIK Group Co. Ltd., Hangzhou, China)；Weihao Zhang (Lynxi Technologies Co. Ltd, Beijing, China)。
  - WeiPipe 面向长上下文 LLM training 中随 sequence length 增大的 activation/activation-gradient 通信，把 stage 间传 activation 的 pipeline 改为传 model weights 及 weight gradients；worker 依次处理完整 layer/数据分片，四种 schedule 在通信量、bubble 和 weight staleness 间取舍，其中 Interleave/zero-bubble 适配低带宽跨节点。
  - 相较传统 pipeline parallelism 固定按 layer 切模型并逐 microbatch传大 activation，核心创新是交换“移动数据”和“移动权重”的角色，使通信规模不再随上下文长度膨胀且无需 collective。
  - AI Infra、LLM 训练、长上下文、Weight Pipeline Parallelism、通信优化

- [MARLIN: Mixed-Precision Auto-Regressive Parallel Inference on Large Language Models](https://doi.org/10.1145/3710848.3710871)
  - Elias Frantar, Jiale Chen (ISTA, Klosterneuburg, Austria)；Roberto L. Castro (CITIC, Universidade da Coruña, A Coruña, Spain)；Torsten Hoefler (ETH Zürich, Zürich, Switzerland)；Dan Alistarh (ISTA, Klosterneuburg, Austria, Neural Magic, Inc., Somerville, USA)。
  - MARLIN 面向 vLLM 等多请求 batched autoregressive LLM inference，把 4-bit weight 在 shared memory/register 中异步加载并按 tensor-core tile 解包，与 FP16 activation 的 GEMM pipeline 交错；复杂 work assignment 保持 batch 16–32 时仍接近 memory-bound 的 4×理论量化收益，并可叠加 2:4 sparsity。
  - 相较既有 weight-only quantization kernel 只在 batch=1 时受访存约束、batch 增大即失速，核心创新是为中等 batch 重排解包、访存和 tensor-core 计算，使量化收益延伸到实际并发 serving。
  - LLM Infra、批量推理、Weight-Only Quantization、4-bit GEMM、vLLM

- [ATTNChecker: Highly-Optimized Fault Tolerant Attention for Large Language Model Training](https://doi.org/10.1145/3710848.3710870)
  - Yuhang Liang, Jieyang Chen (University of Oregon, Oregon, USA)；Xinyi Li, Ang Li, Bo Fang (Pacific Northwest National Laboratory, Washington, USA)；Jie Ren (College of William & Mary, Virginia, USA)。
  - ATTNChecker 通过 fault injection 追踪 attention 中 INF、NaN、near-INF 从 QK/softmax/输出向后传播到不可训练状态的路径；它在 attention 算子内嵌针对这些传播模式的 algorithm-based checksum/校正，并按模型 vulnerability 和系统可靠性选择保护点，在 checkpoint 周期内直接纠错。
  - 相较检测失败后整体 checkpoint/restore，核心创新是把 ABFT 校验专门适配 attention 的错误传播与 kernel 数据流，用约 7% 训练开销消除昂贵回滚。
  - LLM 训练、Attention、Algorithm-Based Fault Tolerance、Silent Error、在线纠错

- [SGDRC: Software-Defined Dynamic Resource Control for Concurrent DNN Inference on NVIDIA GPUs](https://doi.org/10.1145/3710848.3710863)
  - Yongkang Zhang, Haoxuan Yu, Zhifeng Jiang (HKUST, Hong Kong, China)；Chenxia Han (CUHK, Hong Kong, China)；Cheng Wang (Alibaba Group, Shenzhen, China)；Baotong Lu (Microsoft Research, Beijing, China)；Yunzhe Li (Shanghai Jiao Tong University, Shanghai, China)；Yang Li (China University of Geosciences, Wuhan, China)；Xiaowen Chu (HKUST (Guangzhou), Guangzhou, China)；Huaicheng Li (Virginia Tech, Blacksburg, USA)。
  - SGDRC 面向同一 NVIDIA GPU 上 latency-sensitive 与 best-effort DNN inference 共置，先逆向得到 VRAM address 到 memory channel 的 hash；cache coloring/bimodal tensor 分配带宽，tidal SM masking 动态调 compute unit，controller 依据离线 profile 和在线 workload 配额同时保证 LS SLO、提升 BE/总吞吐。
  - 相较硬件 MIG/静态 SM partition 无法独立分配显存带宽，核心创新是在没有厂商带宽接口时用软件页着色控制 VRAM channel，并与可变 SM mask 联合形成跨型号的动态资源隔离。
  - AI Infra、GPU 多租户、VRAM Bandwidth、Cache Coloring、SM Masking、SLO

- [DORADD: Deterministic Parallel Execution in the Era of Microsecond-Scale Computing](https://doi.org/10.1145/3710848.3710872)
  - Zhengqing Liu, Marios Kogias (Imperial College London)；Musa Unal (EPFL)；Matthew J. Parkinson (Azure Research)。
  - DORADD 面向微秒级 datacenter request，由单一 dispatcher 按到达顺序和访问集动态构建 deterministic dependency graph；无依赖的请求下发到多个 worker pool 后 work-conserving、无需彼此同步地执行，dispatcher 本身再通过 core pipeline 分阶段并行，以同时维持确定结果、低尾延迟和高吞吐。
  - 相较 deterministic system 先攒 batch 再 barrier 执行，核心创新是把确定性只放在依赖图构造，调度与执行解耦且不需要 batch；又以核间流水解除单 dispatcher 瓶颈。
  - 确定性并行、微秒级服务、动态依赖图、Datacenter Runtime、内存数据库

- [WaterWise: Co-optimizing Carbon- and Water-Footprint Toward Environmentally Sustainable Cloud Computing](https://doi.org/10.1145/3710848.3710891)
  - Yankai Jiang, Devesh Tiwari (Northeastern University)；Rohan Basu Roy (University of Utah)；Raghavendra Kanakagiri (IIT Tirupati)。
  - WaterWise 面向可跨地域调度的 parallel job，同时读取各数据中心随时间变化的电网 carbon intensity、发电/冷却 water intensity、天气与 job 资源/时限；scheduler 在地点和开始时间上做多目标分配，避免仅追逐低碳区域却增加缺水地区用水，在性能约束下共同降低两类足迹。
  - 相较 carbon-aware 或 water-aware scheduler 单独优化一个指标，核心创新是显式建模二者地理/时间上的冲突并做联合 Pareto 权衡。
  - 云调度、碳足迹、水足迹、地理分布式数据中心、多目标优化

- [FlashSparse: Minimizing Computation Redundancy for Fast Sparse Matrix Multiplications on Tensor Cores](https://doi.org/10.1145/3710848.3710858)
  - Jinliang Shi, Shigang Li, Youxuan Xu, Rongtian Fu, Xueying Wang, Tong Wu (Beijing University of Posts and Telecommunications, Beijing, China)。
  - FlashSparse 面向 Tensor Core 上通用不规则 SpMM/SDDMM，以 swap-and-transpose 改变 tile 乘法次序，把送入 MMA 的 sparse granularity 压到最小、减少因 tile 对齐而补算的零；配套压缩格式和 thread mapping 保持 coalesced access 并压低 metadata/显存。
  - 相较 DTC-SpMM 等以较大稀疏 block 喂满 TCU、产生大量冗余 FLOP，核心创新是通过乘法交换与转置在不改结果时缩小硬件看到的稀疏粒度。
  - SpMM、SDDMM、Tensor Core、Swap-and-Transpose、稀疏粒度

- [Acc-SpMM: Accelerating General-purpose Sparse Matrix-Matrix Multiplication with GPU Tensor Cores](https://doi.org/10.1145/3710848.3710888)
  - Haisha Zhao, San Li, Chunbao Zhou, Jue Wang, Zhikuang Xin, Shunde Li, Zhiqiang Liang, Fang Liu, Yangang Wang, Xuebin Chi (Computer Network Information Center, Chinese Academy of Sciences, Beijing, China and University of Chinese Academy of Sciences, Beijing, China)；Jiaheng Wang (Renmin University of China, Beijing, China)；Zhijie Pan, Yan Zeng (Hangzhou Dianzi University, Hangzhou, Zhejiang, China)。
  - Acc-SpMM 是跨 RTX/A800/H100 的通用 Tensor Core SpMM library：先按数据亲和性重排 nonzero，将矩阵压成低元数据格式；kernel 以多级 pipeline 重叠 gather、shared-memory 搬运和 MMA，并依据行稀疏度在线选择 warp/tile 负载划分。
  - 相较为某一种稀疏分布或 GPU 固定 tile 的 SpMM kernel，核心创新是将重排、压缩、流水和 sparsity-aware load balance 组成可跨架构自适应的完整 library。
  - SpMM、Tensor Core、数据亲和重排、稀疏负载均衡、GPU Library

- [BerryBees: Breadth First Search by Bit-Tensor-Cores](https://doi.org/10.1145/3710848.3710859)
  - Yuyao Niu, Marc Casas (Barcelona Supercomputing Center, Universitat Politècnica de Catalunya, Barcelona, Spain)。
  - BerryBees 把 direction-optimized BFS 统一为 bitmap adjacency 上的 SpMV/SpMSpV；Binarized Row Slice 只记录含边的行段，warp 以 Tensor Core MMA 同时展开 frontier 与多个 bit segment，并按 frontier 密度切换稀/密方向，减少传统 CSR 的 index 和访存开销。
  - 相较 GPU BFS 只用 shader core 操作 bitmap、或图线性代数依赖浮点稀疏矩阵，核心创新是为 bit-level adjacency 设计可直接驱动 TCU 的 BRS 格式与 warp 算法。
  - BFS、Bit Tensor Core、Bitmap、SpMV、方向优化图遍历

- [FlashFFTStencil: Bridging Fast Fourier Transforms to Memory-Efficient Stencil Computations on Tensor Core Units](https://doi.org/10.1145/3710848.3710897)
  - Haozhi Han (Peking University, Microsoft Research, Beijing, China)；Kun Li, Donglin Bai, Ting Cao, Mao Yang (Microsoft Research, Beijing, China)；Wei Cui (Microsoft Research, Vancouver, Canada)；Yiwei Zhang (University of Chinese Academy of Sciences, Microsoft Research, Beijing, China)；Liang Yuan, Yunquan Zhang (Chinese Academy of Sciences, Beijing, China)；Yifeng Chen (Peking University, Beijing, China)。
  - FlashFFTStencil 将多时间步 stencil 变换到频域，使 convolution kernel 通过 dense Tensor Core multiplication 处理；它在 HBM 层融合 FFT/stencil kernel 降低 materialization，在 shared memory 层重排 FFT 数据匹配 bank/矩阵布局，在 TCU/register 层压缩 pipeline stall，并能用频域乘法做不受固定 temporal tile 限制的多步 fusion。
  - 相较把稀疏 stencil 直接映射 TCU 导致零算术、或 temporal blocking 受片上容量限制，核心创新是用 FFT 将算子稠密化并跨 HBM–SMEM–TCU 三层共同设计数据流。
  - Stencil、FFT、Tensor Core、Temporal Fusion、Bound Shifting

- [PANNS: Enhancing Graph-based Approximate Nearest Neighbor Search through Recency-aware Construction and Parameterized Search](https://doi.org/10.1145/3710848.3710867)
  - Xizhe Yin, Chao Gao, Zhijia Zhao, Rajiv Gupta (University of California, Riverside, Riverside, California, USA)。
  - PANNS 面向 vector database 的 graph ANN，把查询/结果随时间的 recency correlation 编入 proximity graph construction，使近期相关点更易相连；search 端把 beam width、candidate expansion、termination 等参数完全暴露给 tuner，在给定 recall 下联合选择索引和 beam 配置。
  - 相较图 ANN 只按静态向量距离建边、beam search 采用少数手调常量，核心创新是首次把访问时序作为建图信号，并系统参数化搜索阶段的整个性能空间。
  - 向量数据库、图近似最近邻、Recency-Aware Index、Beam Search、Recall-Throughput

- [Balanced Allocations over Efficient Queues: A Fast Relaxed FIFO Queue](https://doi.org/10.1145/3710848.3710892)
  - Kåre von Geijer, Philippas Tsigas (Department of Computer Science and Engineering, Chalmers University of Technology and University of Gothenburg, Gothenburg, Sweden)；Elias Johansson, Sebastian Hermansson (Department of Computer Science and Engineering, Chalmers University of Technology, Gothenburg, Sweden)。
  - 该 relaxed FIFO 把 enqueue/dequeue 分散到 n 个高性能 linearizable sub-queue，每次以 d-choice 比较候选队列累计 operation count 后选负载较小者；计数而非当前 queue size 驱动分配，使 ordering relaxation error 不随元素规模增长，并可直接封装既有快队列。
  - 相较旧 balanced-allocation queue 用瞬时长度选子队列、误差和同步成本较高，核心创新是以操作计数建立可证明的 O(n log log n/log d) relaxation bound，同时保留组件队列的性能。
  - Relaxed FIFO、Balanced Allocation、并发队列、D-Choice、误差界

- [LibRTS: A Spatial Indexing Library by Ray Tracing](https://doi.org/10.1145/3710848.3710850)
  - Liang Geng, Xiaodong Zhang (The Ohio State University, Columbus, Ohio, USA)；Rubao Lee (Freelance, Columbus, Ohio, USA)。
  - LibRTS 把 point、range-contains 和 range-intersects 统一编码为 ray/BVH query，由 RT core 完成 spatial index traversal；library 负责将可变空间对象更新到 BVH、为不同查询生成合适 ray/geometry，并按命中分布平衡 GPU 工作，使应用不必直接编写 OptiX traversal。
  - 相较每个非渲染任务单独把算法硬套成光线追踪，核心创新是抽象出可变、通用的 spatial-index API 和三类查询映射，将 RT core 变成可复用数据库索引加速器。
  - 空间索引、Ray-Tracing Core、BVH、点查询、范围查询、GPU Library

- [Crystality: A Programming Model for Smart Contracts on Parallel EVMs](https://doi.org/10.1145/3710848.3710879)
  - Hao Wang, Minghao Pan (International Digital Economy Academy (IDEA), China)；Jiaping Wang (The Hong Kong University of Science and Technology (Guangzhou), China)。
  - Crystality 为 parallel EVM 扩展 Solidity：developer 用 programmable contract scope 把共享 state 划成不重叠分区、把函数拆成可并行 component；asynchronous functional relay 在多个 EVM 间传递后续调用，可交换操作走异步执行，其余交易回退 optimistic path 保持 block 定义的顺序，最后 transpile 为标准 Solidity。
  - 相较运行时猜测读写集后乐观冲突回滚或悲观加锁，核心创新是让合约作者显式提供状态分区和可交换语义，在语言层生成可验证的并行计划且兼容现有 EVM。
  - 智能合约、Parallel EVM、Solidity、状态分区、异步执行

- [Popcorn: Accelerating Kernel K-means on GPUs through Sparse Linear Algebra](https://doi.org/10.1145/3710848.3710887)
  - Julian Bellavita, Giulia Guidi (Cornell University, Ithaca, NY, USA and University of Trento)；Thomas Pasquali, Laura Del Rio Martin, Flavio Vella (University of Trento, Trento, Italy)。
  - Popcorn 将 kernel K-means 的相似度/簇更新重写为稀疏 kernel matrix 上的 SpMM 与 SpMV，沿用成熟 GPU sparse-linear-algebra primitive；对象粒度是样本—簇 assignment 和 centroid aggregate，稀疏表示避免显式执行全部二次 kernel pair，从而以少量专用代码得到 GPU 版本。
  - 相较为 kernel K-means 编写独立的 dense O(n²) GPU kernel，核心创新是发现其可组合成标准稀疏矩阵运算，让通用 SpMM/SpMV 同时提供并行性和工程复用。
  - Kernel K-Means、稀疏线性代数、SpMM、SpMV、GPU

- [Swift Unfolding of Communities: GPU-Accelerated Louvain Algorithm](https://doi.org/10.1145/3710848.3710884)
  - Zhibin Wang, Xi Lin, Ziheng Meng, Chen Tian, Sheng Zhong (State Key Laboratory for Novel Software Technology, Nanjing University)；Xue Li (Alibaba Group)；Pinhuan Wang, Hang Liu (Rutgers, The State University of New Jersey)。
  - GALA 面向 GPU Louvain community detection，先用有最优性保证的 modularity-gain bound 剪去不会改变社区的 vertex；余下工作按邻域规模分别进入 warp-shuffle kernel 或 shared-memory hash kernel，多 GPU 时只对变化社区做 dense/sparse 自适应同步。
  - 相较经验阈值剪枝可能损失 modularity、单一 kernel 又无法覆盖度数倾斜，核心创新是把可证明的 vertex pruning、工作量感知 kernel 和稀密跨卡同步整合。
  - 社区发现、Louvain、GPU、Modularity Pruning、多 GPU 图算法

- [GLumin: Fast Connectivity Check Based on LUTs For Efficient Graph Pattern Mining](https://doi.org/10.1145/3710848.3710889)
  - Weichen Cao, Ke Meng, Zhiheng Lin, Guangming Tan (Institute of Computing Technology, Chinese Academy of Sciences, Beijing, China, University of Chinese Academy of Sciences, Beijing, China and State Key Laboratory of Processors, ICT, Chinese Academy of Sciences, Beijing, China)。
  - GLumin 面向 graph pattern mining 中反复询问两点是否相连/共同邻居，在 runtime 识别会被高频复用的 vertex pair/区域，选择性把 CSR 的局部还原成 adjacency lookup table；LUT 压缩后按容量放入 GPU shared memory 或 CPU cache，并接入 AutoMine、G2Miner、GraphFold。
  - 相较全 CSR 每次二分/交集或完整 adjacency matrix 空间不可承受，核心创新是按模式执行动态选择一小块邻接关系物化，取得 O(1) 检查而不过度占内存。
  - 图模式挖掘、Connectivity Lookup、CSR、运行时 LUT、层次内存

- [Improving Tridiagonalization Performance on GPU Architectures](https://doi.org/10.1145/3710848.3710894)
  - Hansheng Wang, Zitian Zhao, Siqi Wu, Qiao Li, Xu Jiang, Shaoshuai Zhang (University of Electronic Science and Technology of China)；Zhekai Duan (University of Edinburgh)；Saiqi Zheng (Xi'an Jiaotong-Liverpool University)。
  - 该 EVD 实现分析 H100 上 symmetric matrix tridiagonalization 的 panel、band reduction 与 bulge chasing 瓶颈，采用 double-blocking 先以适合 GEMM 的大块把矩阵降为窄带，再在 GPU 上并行追逐 bulge，减少 level-2 BLAS、同步和主机往返，使 FP64 计算更充分占用 GPU。
  - 相较 cuSOLVER/MAGMA 的单层 blocking 和低效 bulge 阶段，核心创新是以两级带宽控制连接高吞吐 band reduction 与 GPU-native bulge chasing。
  - 特征值分解、Tridiagonalization、Double Blocking、Bulge Chasing、GPU FP64

- [Jigsaw: Toward Conflict-free Vectorized Stencil Computation by Tessellating Swizzled Registers](https://doi.org/10.1145/3710848.3710886)
  - Yiwei Zhang (University of Chinese Academy of Sciences, Microsoft Research, Beijing, China)；Kun Li, Ting Cao, Mao Yang (Microsoft Research, Beijing, China)；Liang Yuan, Yunquan Zhang (Chinese Academy of Sciences, Beijing, China)；Haozhi Han (Peking University, Microsoft Research, Beijing, China)。
  - Jigsaw 面向多维/多时间步 stencil 的 SIMD vectorization，将最细 lane 做 swizzle 后像拼图一样 tessellate；butterfly exchange 解决 lane 间邻域取数，SVD-based dimension flattening 选择低冲突维度映射，iteration temporal merging 合并时间步，消除各维的 data-alignment conflict。
  - 相较只沿一个空间维度做 vector shift、冲突转移到其余维或时间维，核心创新是统一把空间与时间索引投影到可拼接的 swizzled lane 布局。
  - Stencil、SIMD Vectorization、Register Swizzle、Temporal Merging、数据对齐

- [Semi-StructMG: A Fast and Scalable Semi-Structured Algebraic Multigrid](https://doi.org/10.1145/3710848.3710849)
  - Yi Zong, Peinan Yu (Tsinghua University, Beijing, China)；Chensong Zhang (Academy of Mathematics and Systems Science, Beijing, China)；Longjiang Mu (Laoshan Laboratory, Qingdao, China)；Jianchun Wang (China Ship Scientific Research Center, Wuxi, China)；Jian Sun (CMA Earth System Modeling and Prediction Center, Beijing, China)；Xiaowen Xu (Institute of Applied Physics and Computational Mathematics, Beijing, China)；Xinliang Wang (Huawei Technologies Co., Ltd, Beijing, China)；Wei Xue (Tsinghua University, Beijing, China, Qinghai University, Qinghai Provincial Laboratory for Intelligent Computing and Application, Xining, China)。
  - Semi-StructMG 面向由规则 block 和不规则 block connection 组成的稀疏线性系统，以 multi-dimensional coarsening 保留块内结构并减少 level/通信；smoother 与 triple-matrix product 对跨块连接单独处理，在 reservoir、ship、weather、ocean workload 上平衡收敛率、每层算量和分布式扩展。
  - 相较通用 AMG 丢失结构、传统 structured MG 又难处理块间不规则边，核心创新是让粗化和核心算子显式区分 block interior 与 inter-block connection。
  - Algebraic Multigrid、半结构网格、多维粗化、稀疏线性求解、可扩展 HPC

- [SBMGT: Scaling Bayesian Multinomial Group Testing](https://doi.org/10.1145/3710848.3710861)
  - Weicong Chen, Hao Qi, Xiaoyi Lu (University of California Merced, Merced, USA)；Curtis Tatsuoka (University of Pittsburgh, Pittsburgh, USA)。
  - SBMGT 把一个样本具有多种可区分 binary attribute 的 group testing 建模为 Bayesian Boolean product lattice；binary encoding 将 lattice state 分片并行，BBPA 根据先验风险把样本分到信息量均衡的 pool，analytics runtime 在 4096 核上搜索/更新 posterior，用更少检验同时识别多类疾病属性。
  - 相较 BGT 每轮只回答一个二元属性、直接扩到多属性会组合爆炸，核心创新是 multinomial Bayesian model 与适合并行的 product-lattice/均衡分池算法共同控制状态空间。
  - Bayesian Group Testing、多标签分类、Product Lattice、并行搜索、疾病监测

- [An AI-Enhanced 1km-Resolution Seamless Global Weather and Climate Model to Achieve Year-Scale Simulation Speed using 34 Million Cores](https://doi.org/10.1145/3710848.3710893)
  - Xiaohui Duan, Huihai An, Weiguo Liu (School of Software, Shandong University, Jinan, China)；Yi Zhang (Chinese Academy of Meteorological Sciences, Beijing, China, Piesat Information Technology Co.,Ltd., Beijing, China and Beijing Research Institute, Nanjing University of Information Science and Technology, Beijing, China)；Kai Xu, Maoxue Yu, Zhao Jing, Hailong Liu, Lixin Wu (Laoshan Laboratory, Qingdao, China)；Haohuan Fu (Tsinghua University, Beijing, China, National Supercomputing Center in Wuxi, Wuxi, China and National Supercomputing Center in Shenzhen, Shenzhen, China)；Bin Yang (College of Intelligence and Computing, Tianjin University, Tianjin, China)；Yiming Wang, Siyuan Chen (Piesat Information Technology Co.,Ltd., Beijing, China)；Yilun Han, Xiting Ju, Haopeng Huang, Zhuang Liu, Bowen Yan, Wenguang Chen (Tsinghua University, Beijing, China)；Zhuangzhuang Zhou, Chenyu Wang, Dongqiang Huang (National Supercomputing Center in Wuxi, Wuxi, China)；Wei Xue (Tsinghua University, Beijing, China, Qinghai University, Qinghai, China and National Supercomputing Center in Wuxi, Wuxi, China)；Jianye Hou (The Chinese University of Hong Kong, Shenzhen, China)；Jian Li (Chinese Academy of Meteorological Sciences, Beijing, China)。
  - 该 GRIST 天气—气候系统面向 Sunway 3400 万核，把 1–3 km global grid 按层级众核做 OpenMP 分解，关键动力/物理 kernel 采用 mixed precision，并嵌入 AI-enhanced physics suite；统一执行引擎从短期极端降雨预报连续运行到年尺度气候模拟，在精度约束下提高 simulated-days-per-day。
  - 相较纯数值 GSRM 分辨率和时间跨度受算力限制、AI weather model 又难保持物理一致性，核心创新是把学习增强物理参数化与超大规模传统动力核心协同优化到同一 seamless model。
  - AI for Science、全球天气气候模型、Sunway、混合精度、3400 万核
