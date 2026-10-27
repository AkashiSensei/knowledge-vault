# PPoPP 2026 论文列表

范围以 PPoPP 2026 官方 Main Conference program 和 ACM proceedings 交叉核对为准，parent DOI 下 51 篇均为主会长文。以下标题均链接至论文 DOI；已找到的 4 份合法公开 PDF 保存在 `reference/PPoPP/2026/`。

- [Binary Compatible Critical Section Delegation](https://doi.org/10.1145/3774934.3786439)
  - Junyao Zhang, Zhe Zhou (Fudan University, Shanghai, China)；Zhuo Wang (Alibaba Cloud Computing, Shanghai, China)。
  - BCD 让未改源码/二进制的现有程序也能做 critical-section delegation：kernel 在 futex_wake 处截获锁交接，把被唤醒线程的 userspace 临界区交给固定 core 执行；in-kernel VM 逐条监督用户指令，动态识别 syscall、fault 等不支持路径并安全退回原锁执行。
  - 相较需要重写临界区为 closure 或修改 lock library 的 delegation，核心创新是以内核 futex 边界和受控 VM 实现 binary compatibility，同时在运行时证明/排除不可安全委托的区段。
  - 临界区委托、Futex、内核虚拟机、Binary Compatibility、锁竞争

- [Hapax Locks: Scalable Value-Based Mutual Exclusion](https://doi.org/10.1145/3774934.3786443)
  - Dave Dice (Independent, Burlington, USA)；Alex Kogan (Oracle Labs, Burlington, USA)。
  - Hapax Lock 用 value-based 状态把 owner、等待序列和交接信息压入紧凑 lock word；arrival 与 unlock 都在常数步内完成，等待线程在本地状态上 spin，release 按 FIFO 将所有权传给唯一后继，从而在高竞争时减少共享 cache line 反复写和额外 queue node。
  - 相较 MCS/CLH 依赖运行时为每次申请管理节点、或紧凑锁牺牲 FIFO，核心创新是用值编码的交接协议同时获得常数路径、FIFO、低空间和较少 coherence traffic，便于直接替换既有 API。
  - 互斥锁、FIFO、公平交接、Cache Coherence、Value-Based Synchronization

- [Fixing Non-blocking Data Structures for Better Compatibility with Memory Reclamation Schemes](https://doi.org/10.1145/3774934.3786455)
  - Md Amit Hasan Arovi, Ruslan Nikolaev (The Pennsylvania State University, University Park, USA)。
  - SCOT 面向 Harris list、Natarajan–Mittal tree 等先 optimistic traversal、后 validation/update 的非阻塞结构，在遍历期间以安全的并发访问协议保护可能被删除的路径，并在确认操作点时重验证；它不改 hazard pointer、hazard era、IBR、Hyaline 的回收器接口，也提供 wait-free traversal 变体。
  - 相较把结构改成 Harris–Michael 式每步保护、或只能依赖不抗停顿的 EBR，核心创新是给数据结构侧增加通用 traversal layer，让多种健壮 SMR 保持原结构的乐观读性能。
  - 非阻塞数据结构、Safe Memory Reclamation、Optimistic Traversal、Hazard Pointer、SCOT

- [Multiverse: Transactional Memory with Dynamic Multiversioning](https://doi.org/10.1145/3774934.3786436)
  - Gaetano Coccimiglio, Trevor Brown (University of Waterloo, Waterloo, Canada)；Srivatsan Ravi (University of Southern California, Los Angeles, USA)。
  - Multiverse STM 在同一 heap 上并发支持普通单版本事务和为 long-running read 保留历史值的多版本事务；runtime 根据读集合规模/更新冲突选择版本化路径，普通短事务避免维护无用版本，长读则在稳定 snapshot 上扫描频繁更新地址并由回收协议清理旧版本。
  - 相较 MVCC/多版本 STM 让所有写都支付版本成本、单版本 STM 又会不断 abort 长读，核心创新是允许两类事务动态共存并只为确有需要的执行保留版本。
  - Software Transactional Memory、MVCC、长事务、动态多版本、并发控制

- [Rethinking Thread Scheduling under Oversubscription: A User-Space Framework for Coordinating Multi-runtime and Multi-process Workloads](https://doi.org/10.1145/3774934.3786451)
  - Aleix Roca, Vicenç Beltran (Barcelona Supercomputing Center, Barcelona, Spain)。
  - USF 面向 co-located process 和 OpenMP/BLAS/PyTorch 等多 runtime 造成的 oversubscription，在 glibc 与 nOS-V 中让 userspace runtime 共享 core/ready-thread 状态；默认 SCHED_COOP 只在线程 blocking 时协作换出，避免 OS 周期抢占 lock holder/waiter，并无需 root 权限或侵入应用。
  - 相较每个 runtime 独立向 OS 创建线程、由通用 scheduler 盲目时分，核心创新是一个跨进程/跨 runtime 的用户态协调层；它把调度点放在可观察的 blocking event 而非固定时间片。
  - 用户态调度、Oversubscription、多 Runtime、Lock-Holder Preemption、HPC/AI 共置

- [Waste-Efficient Work Stealing](https://doi.org/10.1145/3774934.3786452)
  - Kyle Singer, Tao B. Schardl (Massachusetts Institute of Technology, Cambridge, USA)；Kunal Agrawal (Washington University in St. Louis, St. Louis, USA)。
  - WEWS 扩展 randomized work stealing runtime，在线依据 steal success/可用 parallelism 调整 active worker 数；多余线程进入低开销休眠而非持续随机探测，工作出现再逐步唤醒，并保持 work-first fast path，使执行时间仍具传统 stealing 的渐近界、浪费指令受 O(min{PT∞, T1+P²}) 限制。
  - 相较固定 P 个 worker 或经验 backoff 只能缓和空偷，核心创新是给动态 worker 收缩/扩张同时提供 work/span 时间保证和显式 waste bound，并在 OpenCilk 中无需 OS/硬件支持。
  - Work Stealing、OpenCilk、动态线程数、资源浪费、Work-First Runtime

- [DiggerBees: Depth First Search Leveraging Hierarchical Block-Level Stealing on GPUs](https://doi.org/10.1145/3774934.3786457)
  - Yuyao Niu, Marc Casas (Barcelona Supercomputing Center, Barcelona, Spain; Universitat Politècnica de Catalunya, Barcelona, Spain)；Yuechen Lu, Weifeng Liu (China University of Petroleum-Beijing, Beijing, China)。
  - DiggerBees 面向 GPU DFS 的深栈与不规则 frontier，用 shared-memory 顶层加 global-memory 溢出层构成 two-level stack；warp 内协作推进一条 DFS 并在 block 内窃取子树，block 之间再暴露可窃取任务，分别解决栈容量、频繁 push/pop 和跨 block 负载倾斜。
  - 相较把 CPU thread-level DFS stealing 直接移植 GPU，核心创新是把 stealing hierarchy 与 GPU warp/block memory hierarchy 对齐，并为深窄图保留 DFS 的低 frontier 优势。
  - GPU DFS、层次 Work Stealing、Two-Level Stack、Warp 协作、图遍历

- [PANA: A Fine-Grained Runtime-Adaptive Load Balancing for Parallel SpMV on Multicore CPUs](https://doi.org/10.1145/3774934.3786459)
  - Haodong Bian (Tsinghua University, Beijing, China; Qinghai University, Xining, China)；Youhui Zhang (Tsinghua University, Beijing, China; Zhongguancun Laboratory, Beijing, China)；Xiang Fei (Zhongguancun Laboratory, Beijing, China)；Jianqiang Huang, Xiaoying Wang (Qinghai University, Xining, China)。
  - PANA 面向 multicore CPU 的 CSR SpMV，把 row/nonzero 继续拆为 micro-operation；runtime 同时观察各 core 的算术工作与 memory-access progress，细粒度调整分区边界/任务归属，使长行、短行和 cache/NUMA 差异不会令某核计算或访存先成为尾部。
  - 相较按 nonzero 数静态均分只平衡 FLOP、按 memory model 划分又忽略运行时差异，核心创新是在微操作粒度联合平衡计算和访存，并随真实执行动态修正。
  - SpMV、多核 CPU、运行时负载均衡、微操作、稀疏矩阵

- [UFO Trees: Practical and Provably-Efficient Parallel Batch-Dynamic Trees](https://doi.org/10.1145/3774934.3786431)
  - Quinten De Man, Atharva Sharma, Kishen N Gowda, Laxman Dhulipala (University of Maryland, College Park, USA)。
  - UFO Tree 维护可批量 link/cut 的动态树，同时支持 connectivity、path aggregate 等通用 query；数据结构按 tree diameter 调整 cluster/exposure，使低直径树的更新和查询可低于 logarithmic，batch update 用 work-efficient parallel rebuild，并以紧凑 C++ 布局扩到十亿节点。
  - 相较 link-cut tree 虽串行快却难批并行、既有 parallel tree 又功能或常数差，核心创新是统一获得广泛查询、work-efficient batch dynamics 和可与 link-cut 媲美的顺序性能，并解释低直径优势。
  - 动态图数据结构、Batch-Dynamic Tree、路径查询、Work Efficiency、十亿级图

- [Sharded Elimination and Combining for Highly-Efficient Concurrent Stacks](https://doi.org/10.1145/3774934.3786458)
  - Ajay Singh (ICS-FORTH, Heraklion, Greece)；Nikos Metaxakis (University of Crete, Heraklion, Greece)；Panagiota Fatourou (ICS-FORTH, Heraklion, Greece; University of Crete, Heraklion, Greece)。
  - 该 concurrent stack 将 push/pop 先按 shard 分散，互补操作在 shard 内 elimination，无匹配请求则以 fetch-and-increment 形成 batch，由 combiner 一次访问 central stack 并回填各请求结果；两条路径按竞争状况衔接，减少所有线程触碰同一 top pointer。
  - 相较只做 elimination 在负载偏单向时失效、只做 combining 又集中到单队列，核心创新是用 sharding 和 FAA 把 elimination 与 batching 融成可线性化的自适应执行。
  - 并发栈、Elimination、Combining、Sharding、Fetch-and-Increment

- [Concurrent Balanced Augmented Trees](https://doi.org/10.1145/3774934.3786437)
  - Evan Wrench, Yuanhao Wei (University of British Columbia, Vancouver, Canada)；Ajay Singh (ICS-FORTH, Heraklion, Greece)；Younghun Roh (Massachusetts Institute of Technology, Cambridge, USA)；Panagiota Fatourou (ICS-FORTH, Heraklion, Greece; University of Crete, Heraklion, Greece)；Siddhartha Jayanti (Dartmouth College, Hanover, USA)；Eric Ruppert (York University, Toronto, Canada)。
  - 该结构在 lock-free balanced search tree 的节点维护用户定义 aggregate，使 insert/delete/lookup 与 range/order-statistic query 共存；更新路径通过非阻塞重平衡原子维护 augmentation，解决 retired node 与 aggregate version 的回收，并提供 delegation 版本把热点子树更新交给少数执行者。
  - 相较已有 lock-free augmented tree 不平衡、最坏路径过长，核心创新是首次把 generic augmentation 和平衡旋转同时做成 lock-free，并用可选 delegation 进一步扩大高竞争吞吐。
  - Lock-Free Tree、Augmentation、平衡搜索树、Range Query、Delegation

- [Parallel Dynamic Spatial Indexes](https://doi.org/10.1145/3774934.3786412)
  - Ziyang Men, Bo Huang, Yan Gu, Yihan Sun (University of California at Riverside, Riverside, USA)。
  - 该研究为高度动态 2D/3D point set 设计 P-Orth tree 与 SPaC-tree：前者并行更新 quadtree/octree cell，后者把 R-tree/BVH 节点组织成可批量重构的 spatial cluster；batch insert/delete 只重建受影响区域，query 在稳定版本上并行执行，并系统比较 kd-tree、Orth-tree、R-tree/BVH 的更新—查询权衡。
  - 相较 parallel spatial index 主要优化静态 build/query，核心创新是为两类低延迟索引给出专门的 work-efficient batch update，并在相同基准下揭示结构选择边界。
  - 空间索引、Batch Update、Quadtree、R-Tree、BVH、并行数据结构

- [PRISM: An Efficient GPU-Based Lossy Compression Framework for Progressive Data Retrieval with Multi-Level Interpolation](https://doi.org/10.1145/3774934.3786438)
  - Bing Lu, Zedong Liu, Guangming Tan, Dingwen Tao (Institute of Computing Technology, Chinese Academy of Sciences, Beijing, China)；Hairui Zhao (Jilin University, Changchun, China)；Dejun Luo, Wenjing Huang, Yida Gu (Institute of Computing Technology, Chinese Academy of Sciences, Beijing, China; University of Chinese Academy of Sciences, Beijing, China)；Jinyang Liu (University of California, Riverside, Riverside, USA)。
  - PRISM 面向科学数据按需多精度 retrieval，把多个 interpolation predictor 生成的 residual 分层编码；GPU bitplane extraction 允许只取满足当前 error bound 的高位层，sign-absolute coding 与 zero-aware parallel lossless stage 压缩稀疏 bitplane，从一次压缩结果逐级恢复更高精度。
  - 相较 GPU lossy compressor 只能整块单精度解压、既有 progressive codec 又吞吐低，核心创新是将多级插值、bitplane 和零感知无损编码组成全 GPU pipeline，同时优化传输量和渐进吞吐。
  - 科学数据压缩、Error-Bounded Lossy Compression、Progressive Retrieval、Bitplane、GPU

- [Dynamic Detection of Inefficient Data Mapping Patterns in Heterogeneous OpenMP Applications](https://doi.org/10.1145/3774934.3786454)
  - Luke Marzen, Junhyung Shim, Ali Jannesari (Iowa State University, Ames, USA)。
  - OMPDataPerf 通过 OMPT 在 heterogeneous OpenMP runtime 中跟踪 target data map、allocation、host-device transfer 与 kernel 使用区间，把重复映射、过早/过晚 copy、未复用 allocation 等低效模式归因到源码 directive；同时估计若复用/扩大 data region 可省的字节和时间，以约 5% 开销输出 trace。
  - 相较 profiler 只列出传输带宽、依赖开发者人工关联 directive，核心创新是在线识别有语义的 data-mapping anti-pattern，并给出 source attribution 与可优化收益。
  - OpenMP Offloading、数据映射、动态分析、OMPT、性能诊断

- [Root-Down Exposure for Maximal Clique Enumeration on GPUs](https://doi.org/10.1145/3774934.3786449)
  - Zhe Pan, Peng Qu (Tsinghua University, Beijing, China)；Youhui Zhang (Tsinghua University, Beijing, China; Zhongguancun Laboratory, Beijing, China)。
  - RDMCE 面向 GPU maximal clique enumeration，让繁忙 worker 只暴露当前 DFS root/搜索状态，空闲 worker 从该 root 直接生成并领取子任务，不暂停 owner 或复制整个栈；bitmap-centric candidate set 和 aggressive node generation 进一步压缩状态、提前制造可窃取并行度。
  - 相较 donor-driven workload handoff 要同步繁忙线程且占用额外队列，核心创新是 root-down、receiver-pull exposure，使负载再平衡不在 owner critical path。
  - 最大团枚举、GPU、Root-Down Exposure、Bitmap、动态负载均衡

- [ROME: Maximizing GPU Efficiency for All-Pairs Shortest Path via Taming Fine-Grained Irregularities](https://doi.org/10.1145/3774934.3786461)
  - Weile Luo, Yuhan Chen, Xiangrui Yu, Ruibo Fan (The Hong Kong University of Science and Technology (Guangzhou), Guangzhou, China)；Qiang Wang (Harbin Institute of Technology, Shenzhen, Shenzhen, China)；Hongyuan Liu (Stevens Institute of Technology, Hoboken, USA)；Xiaowen Chu (The Hong Kong University of Science and Technology (Guangzhou), Guangzhou, China; Hong Kong University of Science and Technology, Hong Kong, Hong Kong)。
  - ROME 面向 vertex-reordered APSP 在 GPU 上产生的细粒度大小、形状和依赖不规则，将多个 min-plus 子任务在空间上重组为规则 tile；不同依赖波次进入 asynchronous pipeline，在数据就绪时交叠搬运与计算，使 tensor/SM 维持批量工作而不被短小 kernel 和 barrier 切碎。
  - 相较 vertex reordering 只减少理论工作量却忽略 GPU 执行形态，核心创新是同时在空间把不规则任务 regularize、在时间按依赖异步重叠，转化出稳定硬件利用率。
  - APSP、Min-Plus、GPU、不规则计算、异步流水

- [SPIDER: Unleashing Sparse Tensor Cores for Stencil Computation via Strided Swapping](https://doi.org/10.1145/3774934.3786414)
  - Qiqi Gu, Chenpeng Wu, Jianguo Yao (Shanghai Jiao Tong University, Shanghai, China)；Heng Shi (Shanghai Enflame Technology Co.,Ltd., Shanghai, China; Shanghai Jiao Tong University, Shanghai, China)。
  - SPIDER 把 stencil kernel matrix 通过 ahead-of-time strided swapping 重排成 Sparse Tensor Core 接受的结构化稀疏 pattern；运行时只对 input row 做规则化 on-the-fly swap 与之配对，避免显式布局转换，再以 tile/fusion 优化执行 MMA。
  - 相较 ConvStencil/FlashFFTStencil 在 dense Tensor Core 上补算 stencil 中固有的零，核心创新是成对设计 kernel 静态交换和输入动态行交换，把这部分稀疏直接变成 SpTC 加速机会且零运行时转换开销。
  - Stencil、Sparse Tensor Core、Strided Swapping、结构化稀疏、GPU

- [ASM-SpMM: Unleashing the Potential of Arm SME for Sparse Matrix Multiplication Acceleration](https://doi.org/10.1145/3774934.3786422)
  - Jiazhi Jiang, Xijia Yao, Jiayu Chen, Jinhui Wei, Dan Huang, Yutong Lu (Sun Yat-sen University, Guangzhou, China)。
  - ASM-SpMM 面向 Armv9 SME 的 outer-product matrix tile，将 sparse row 压为低元数据格式，用 SME-aware prefetch 提前流入 dense operand；规则部分走矩阵 tile，极稀/短行切到 matrix-vector path，异构 core 间以 work stealing 吸收行长度倾斜，并用于 GNN inference。
  - 相较把 x86/NEON SpMM 原样搬到 SME、只使用一种执行形态，核心创新是围绕 SME outer-product 共同设计压缩/预取，并在 matrix 与 vector path、异构 core 间动态选择。
  - SpMM、Arm SME、Outer Product、混合矩阵向量执行、异构多核

- [Exploiting Efficient Mapping and Pipelined Execution for Accelerating SpMV on Tensor Cores](https://doi.org/10.1145/3774934.3786441)
  - Kaige Zhang, Hailong Yang, Xin You, Tianyu Feng, Zhongzhi Luan, Yi Liu, Depei Qian (Beihang University, Beijing, China)；Yufan Xu (Independent Researcher, Cupertino, USA)。
  - Drawloom 面向 Tensor Core SpMV 的 matrix-tile 与单 vector 不匹配，使用 zig-zag chained sparse format 把跨行 nonzero 串成可映射 MMA 的 tile，减少 padding/partial tile；multi-stage register pipeline 重叠 index decode、value/vector load、MMA 和 reduction，覆盖 FP16/32/64。
  - 相较现有 TCU SpMV 以规则 block 补零或频繁回写部分和，核心创新是链式之字映射配 register pipeline，在保留通用稀疏矩阵时提高每个 MMA 的有效元素率。
  - SpMV、Tensor Core、Zig-Zag Sparse Format、Register Pipeline、GPU

- [VDHA: Vector-Driven Hash Aggregation for Sparse Matrix-Sparse Vector Multiplication on GPUs](https://doi.org/10.1145/3774934.3786447)
  - Yuchen Li, Zhe Pan, Peng Qu (Tsinghua University, Beijing, China)；Youhui Zhang (Tsinghua University, Beijing, China; Zhongguancun Laboratory, Beijing, China)。
  - VDHA 面向 SpMSpV 的 many-to-one output scatter，在每个 thread block 建私有 hash table，先聚合同一 output index 的 multiply–accumulate 再合并写回；column splitting/轻重排提高同 block 局部性，fetch–compute–writeback pipeline 隐藏 hash 与访存，并以预测模型判断何种 matrix 适用。
  - 相较每个 nonzero 直接 atomic scatter 到全局 vector，核心创新是以 block-local vector-driven hash 将冲突写转化为片上规约，并通过列切分主动制造可聚合性。
  - SpMSpV、GPU Hash Aggregation、写冲突、列切分、Spiking Neural Network

- [RoMeo: Mitigating Dual-dimensional Outliers with Rotated Mixed Precision Quantization](https://doi.org/10.1145/3774934.3786419)
  - Qihao Zhang, MingLiang Tang, Mingshu Zhai, Kinman Lei, Jidong Zhai (Tsinghua University, Beijing, China)。
  - RoMeo 面向 LLM serving 的 4-bit mixed-precision quantization，先用 rotation 抑制 channel-wise outlier 并把剩余异常迁到 token 维；runtime 在每批 token 动态检测稀疏高精度项，将普通值走低精度 dense kernel、异常值走专用 sparse path，再融合结果，兼顾模型精度与 GPU 利用率。
  - 相较 QuaRot/MixQ 只处理 channel outlier、在 4-bit 下仍被 token outlier 拉低精度，核心创新是算法上做二维异常迁移，并为动态 token-wise 高精度残差配套 serving kernel。
  - LLM Infra、4-bit 量化、二维 Outlier、Rotation、混合精度 Serving

- [High-Throughput Non-uniformly Quantized 3-bit LLM Inference](https://doi.org/10.1145/3774934.3786423)
  - YuAng Chen (Chinese University of Hong Kong, Hong Kong, China)；Wenqi Zeng (Hong Kong University of Science and Technology, Hong Kong, China)；Jeffrey Xu Yu (Hong Kong University of Science and Technology (Guangzhou), Hong Kong, China)。
  - Quantix 面向 clustering-based non-uniform 3-bit weight LLM inference，把 codebook index 做硬件对齐 bit shuffling，使连续 warp load 可直接解码；fused dequantization–matmul pipeline 将查表/解包分配给 CUDA core、乘法送 Tensor Core并重叠，避免省下 HBM 流量后反被 dequantization 阻塞，支持高吞吐 batch。
  - 相较非均匀量化只压缩显存、推理需单独 dequantize 导致比 FP16 更慢，核心创新是重排 bit layout 并跨 CUDA/Tensor Core 融合解码和 GEMM，把 3-bit 压缩真正转为速度。
  - LLM Infra、3-bit 非均匀量化、Bit Shuffling、融合反量化、Tensor Core

- [JanusQuant: Accurate and Efficient 2-bit KV Cache Quantization for Long-Context Inference](https://doi.org/10.1145/3774934.3786428)
  - Chengyu Sun, Yaqi Xia, Hulin Wang, Dazhao Cheng (Wuhan University, Wuhan, China)；Donglin Yang (Nvidia Corporation, Santa Clara, USA)；Xiaobo Zhou (University of Macau, Macau, China)。
  - JanusQuant 面向 long-context decoding 的 KV cache，以 RtSmooth 在 runtime 根据当前 token/channel outlier 自适应变换后做 2-bit quantization；fast absmax positioning 降低量化统计成本，recent token 用紧凑结构保留较高精度，自定义 mixed-precision attention 在读取时直接解码并计算。
  - 相较固定 offline smoothing 或硬件不友好的 2-bit KV 方法，核心创新是把动态 outlier smoothing、近期 token 管理和 attention kernel 共同设计，在 99% 精度下同时获得容量与吞吐收益。
  - LLM Infra、KV Cache、2-bit 量化、长上下文、Mixed-Precision Attention

- [HierCut: Enabling 16-bit Format Mixed Precision for Molecular Dynamics through Hierarchical Cutoff](https://doi.org/10.1145/3774934.3786433)
  - Zeyu Song, Lin Gan, Zhengrui Li, Jiayu Fu, Yinuo Wang, Guangwen Yang (Tsinghua University, Beijing, China)；Xiaohui Duan (Shandong University, Jinan, China)；Guangzhao Li (Institute of Software Chinese Academy of Sciences, Beijing, China)。
  - HierCut 面向 LAMMPS/Kokkos molecular dynamics，把邻居按 distance cutoff 划成多个层：对力贡献敏感的近邻用 FP32/64，远层用 FP16/BF16 等低精度；error analysis 根据势函数和 layer 误差决定各层比例，配套 16-bit force kernel，并在 multi-GPU 上保持相同分解。
  - 相较整个 MD kernel 统一降精度导致截断误差、或所有 pair 保持高精度，核心创新是借用物理 cutoff hierarchy 作为精度边界，让数值敏感度和硬件格式逐层匹配。
  - 分子动力学、混合精度、Hierarchical Cutoff、FP16、LAMMPS、Multi-GPU

- [Cacheman: A Comprehensive Last-Level Cache Management System for Multi-tenant Clouds](https://doi.org/10.1145/3774934.3786415)
  - Xiaokang Hu, Yuchao Cao, Naixuan Guan, Yifan Wu, Xishi Qiu, Shengdong Dai, Ben Luo, Sanchuan Cheng, Fudong Qiu, Yibin Shen, Jiesheng Wu (Alibaba Cloud Computing, Hangzhou, China)。
  - Cacheman 面向云上 co-located VM 的 LLC contention，按秒采集 tenant performance/LLC response，gradient-based sharing 依据增加/减少 cache way 的边际收益平滑调整 allocation；实时算法检测相对 SLA 的不公平并回收低收益 way，对同一分布式应用的多个 VM 还执行协商的 cache 上限以保持 performance consistency。
  - 相较静态 CAT partition 或只最大化总 throughput，核心创新是将效用梯度、公平/SLA 检测和分布式 tenant 一致性纳入一个生产 cache controller。
  - 云资源管理、Last-Level Cache、Multi-Tenancy、SLA、公平分配

- [zBuffer: Zero-Copy and Metadata-Free Serialization for Fast RPC with Scatter-Gather Reflection](https://doi.org/10.1145/3774934.3786426)
  - Xiangyu Liu, Shun Gai (Xiamen University, Xiamen, China; Alibaba Cloud, Beijing, China)；Huiba Li (Alibaba Cloud, Beijing, China)；Youmin Chen (Shanghai Jiao Tong University, Shanghai, China)；Yiming Zhang (Shanghai Jiao Tong University, Shanghai, China; Alibaba Cloud, Beijing, China)。
  - zBuffer 对复杂 C++ object 在编译期用 template/macro 做 static reflection，生成分散 field 的 iovec，而不构造运行时 schema metadata或连续 serialization buffer；NIC scatter–gather 直接从原对象内存发包，接收侧按类型布局落位，zRPC 因而贯穿序列化和网络传输都不 copy/coalesce。
  - 相较 Protobuf/Cornflakes 仍需元数据或预先拼接 buffer，核心创新是将语言静态反射与 NIC scatter–gather 协同，把类型查询和数据聚合分别移到编译期与硬件。
  - RPC、Zero-Copy Serialization、Scatter-Gather、Static Reflection、NIC Offload

- [Scaling GPU-to-CPU Migration for Efficient Distributed Execution on CPU Clusters](https://doi.org/10.1145/3774934.3786435)
  - Ruobing Han, Hyesoon Kim (Georgia Institute of Technology, Atlanta, USA)。
  - CuCC 把 CUDA/GPU program 迁移到多节点 CPU cluster：runtime 将 GPU thread/block work 分发到 CPU node，并在跨节点维护原 GPU memory/同步语义；它依据访问范围聚合 consistency message、重叠通信计算并减少 barrier，使大量 CPU 核弥补单 CPU 与 GPU 的算力差距。
  - 相较既有 GPU-to-CPU translation 仅在单机执行，核心创新是为迁移后的 GPU execution model 增加分布式一致性与通信优化，使无需 GPU 的集群执行可扩展。
  - GPU-to-CPU Migration、CPU 集群、CUDA 兼容、分布式执行、数据一致性

- [Trojan Horse: Aggregate-and-Batch for Scaling Up Sparse Direct Solvers on GPU Clusters](https://doi.org/10.1145/3774934.3786442)
  - Yida Li, Siwei Zhang, Yiduo Niu, Yang Du, Qingxiao Sun, Zhou Jin, Weifeng Liu (China University of Petroleum-Beijing, Beijing, China)。
  - Trojan Horse 面向 SuperLU_DIST/PanguLU 中大量形状、尺寸各异的小 sparse-direct-solver task；Prioritizer 按 dependency urgency 将急任务送 Collector、其余暂存 Container，Collector 凑齐能占满 GPU 的异构 batch 后由 Executor 一次提交，在节点间保持原 solver dependency 并扩展到 NVIDIA/AMD GPU cluster。
  - 相较每个稀疏消元小任务单独 launch、或 batch 只容纳同形算子，核心创新是以优先级 aggregate 加异构 batch 在不改 solver library 的情况下持续喂满 GPU。
  - 稀疏直接求解、GPU 集群、异构 Batching、Task Aggregation、SuperLU_DIST

- [COCCL: A Collective Communication Library Supporting Easy Integration and Configuration of Customized Compression for Scalable LLM Training](https://doi.org/10.1145/3774934.3786432)
  - Xingchen Liu, Shengkai Lyu, Zheng Wei, Man Liu, Xingjian Tian, Liyang Zhao, Zhuohan Chen, Zhan Wang, Guangming Tan, Dingwen Tao (University of Chinese Academy of Sciences, Beijing, China)；Haoran Kong, Zizhong Chen (Shenzhen Loop Area Institute, Shenzhen, China; Chinese University of Hong Kong, Shenzhen, Shenzhen, China)；Hairui Zhao (Jilin University, Jilin, China)；Fakang Wang (Ant Group, Hangzhou, China)。
  - COCCL 在 NCCL 上为 data/tensor/pipeline parallel LLM training 提供可插拔 compression operator；programming model 指定 collective 哪一段压缩、格式和误差策略，library 选择 compression-aware ring/tree algorithm，并在 chunk pipeline 中重叠 encode、网络与 decode；runtime 为 3D parallel GPT/Qwen 搜索不会累积精度误差的配置。
  - 相较把 compressor 包在 collective 外、需应用手工改通信且无法与分块算法协同，核心创新是将压缩变成 collective library 的一等可配置阶段，并共同设计通信拓扑、overlap 和误差传播。
  - AI Infra、LLM 训练、Collective Compression、NCCL、3D Parallelism

- [Elastor: Elastic and Efficient Model Partitioning and Checkpointing for Fault-Tolerant Distributed Training](https://doi.org/10.1145/3774934.3786445)
  - Xuanyu Wang, Haoyang Li, Hao Ge, Sheng Lin, Jiawen Niu, Bin Cui (Peking University, Beijing, China)；Fangcheng Fu (Shanghai Jiao Tong University, Shanghai, China)。
  - Elastor 面向 distributed training 中整 node 或部分 GPU 失效，把 model tensor 切成与当前 partition 无关的细粒度 checkpoint shard；恢复时 strategy search 根据剩余 GPU 数/异构能力重新选择 model-parallel partition，并直接把 shard 组合到新布局，周期保存与 data preprocessing/训练重叠。
  - 相较 checkpoint 绑定原 rank/partition、只能相同 GPU 数恢复，核心创新是 partition-agnostic tensor split 加 heterogeneous repartition，使任意数量剩余 GPU 都能快速弹性续训。
  - AI Infra、分布式训练、故障恢复、Elastic Model Parallelism、Checkpoint Resharding

- [HelixPipe: Efficient Distributed Training of Long Sequence Transformers with Attention Parallel Pipeline Parallelism](https://doi.org/10.1145/3774934.3786417)
  - Geng Zhang, Shenggan Cheng, Xuanlei Zhao, Ziming Liu, Yang You (National University of Singapore, Singapore, Singapore)。
  - HelixPipe 面向 128K 等 long-sequence Transformer training，把每个 microbatch 的 attention 沿序列并行拆给不同 pipeline stage，使各 stage 可交错处理不同 microbatch attention；two-fold first-in-last-out schedule 控制 activation lifetime并重叠通信，非 attention 重计算和 chunked MLP 降低峰值/碎片。
  - 相较 pipeline 只沿 layer 切分、长序列二次 attention 让某 stage 过重且显存失衡，核心创新是把 attention parallelism 直接织入 pipeline schedule，并以专门 microbatch 次序配平内存。
  - AI Infra、长序列 Transformer、Pipeline Parallelism、Attention Parallelism、FILO Schedule

- [CCL-D: A High-Precision Diagnostic System for Slow and Hang Anomalies in Large-Scale Model Training](https://doi.org/10.1145/3774934.3786429)
  - Yida Gu, Xingchen Liu, Wenjing Huang, Zedong Liu, Jinwu Yang, Yueyuan Zhou, Haoxu Li, Zhan Wang, Guangming Tan, Dingwen Tao (University of Chinese Academy of Sciences, Beijing, China)；Fakang Wang, Jianhao Fu, Zhenhang Sun, Qianyu Zhang, Yang Tian, Yifan Chen, Qian Zhao, Tao Wang, Feng Yu (Ant Group, Hangzhou, China)；Hairui Zhao (Jilin University, Changchun, China)。
  - CCL-D 面向 4000-GPU training cluster 的 collective slow/hang，rank-level probe 以轻量 distributed tracing 关联 GPU kernel、NCCL traffic、network 和 host 指标；decision analyzer 比较 rank 间时序/拓扑异常，自动区分慢链路、故障 GPU 或软件阻塞并定位具体 rank，在 6 分钟内给出根因。
  - 相较人工拼接多层日志或只发现 job 超时，核心创新是将跨层通信 trace 对齐到 collective/rank，并用集群长期故障知识自动完成检测和定位。
  - AI Infra、训练可观测性、Collective Hang、分布式追踪、根因定位

- [Pipelonk: Accelerating End-to-End Zero-Knowledge Proof Generation on GPUs for PLONK-Based Protocols](https://doi.org/10.1145/3774934.3786448)
  - Zhiyuan Zhang, Lei Ju (Shandong University, Qingdao, China; Quan Cheng Laboratory, Jinan, China)；Yanxin Cai, Wenhao Yin (Shandong University, Qingdao, China)；Xueyu Wu (University of Hong Kong, Hongkong, China)；Yi Wang (Shenzhen University, Shenzhen, China)；Zhuoran Ji (Shandong University, Qingdao, China; State Key Laboratory of Cryptography and Digital Economy Security, Jinan, China)。
  - Pipelonk 面向内存受限 GPU 上端到端 PLONK proof generation，把 MSM、FFT 及原本难并行的每个 operator 都改成可按 input segment 独立执行的 library；global executor 在保持 polynomial/data/security dependency 下排列 compute/memory task，按显存和算子特征选 segment size，并以双缓冲重叠 PCIe transfer。
  - 相较只加速若干热点 kernel、其余阶段回 CPU 或要求大显存，核心创新是全算子可分段接口加 dependency-aware pipeline，使 8–80GB GPU 都能端到端执行。
  - Zero-Knowledge Proof、PLONK、GPU Pipeline、Segmented Operator、计算传输重叠

- [ParDiff: Efficiently Parallelizing Reverse-Mode Automatic Differentiation with Direct Indexing](https://doi.org/10.1145/3774934.3786418)
  - Shuhong Huang, Huanqi Cao, Ruibai Tang, Yidong Chen, Jiping Yu (Tsinghua University, Beijing, China)；Shizhi Tang (Qingcheng.AI, Beijing, China)；Yuan Wen (University of Aberdeen, Aberdeen, United Kingdom)；Yang Li, Chao Jiang, Limin Xiao (Lenovo Research, China)；Jidong Zhai (Tsinghua University, China)。
  - ParDiff 为 reverse-mode AD 使用 direct-indexed tape：每个 intermediate 的 adjoint 可由静态索引直接定位，不再沿原 control flow 顺序 pop；编译器据 summation pattern 做 loop interchange/partition/reduction transformation，将跨线程原子累加改成局部规约，并为 CPU/GPU 选择并行方案。
  - 相较传统 tape 把取值顺序和原程序控制流绑定、妨碍重排且依赖 atomic add，核心创新是解耦记录与回放索引，使 AD 后代码可应用 summation-aware parallel transformation。
  - 自动微分、Reverse Mode、Direct-Indexed Tape、并行编译、规约优化

- [Faster and Cheaper: Pushing the Sequence Alignment Throughput with Commercial CPUs](https://doi.org/10.1145/3774934.3786421)
  - Zhonghai Zhang (Institute of Computing Technology at Chinese Academy of Sciences, Beijing, China; University of Chinese Academy of Sciences, Beijing, China)；Yewen Li (Hong Kong University of Science and Technology, Hong Kong, China)；Ke Meng, Guangming Tan (Institute of Computing Technology at Chinese Academy of Sciences, Beijing, China)；Chunming Zhang (Institute of Computing Technology at Chinese Academy of Sciences, Beijing, China; Phil Rivers Technology, Beijing, China)。
  - FastAlign 面向 commodity CPU 的 BWA-MEM 等价 sequence alignment，multi-stage seeding 逐层缩小候选位置、控制 index/内存；单条 query 的 seed extension 再在 SIMD lane 间并行，并消除重叠 candidate 的重复 dynamic-programming work，在输出 100% 一致时提高 node throughput 和成本效率。
  - 相较 CPU aligner 主要跨 read 并行、长 read/难 query 留下尾部，或 GPU 方案改变 pipeline，核心创新是同时优化 seed search 与单 query 内 extension，并保持 de facto output compatibility。
  - 基因序列比对、CPU SIMD、Multi-Stage Seeding、Intra-Query Parallelism、BWA-MEM

- [PIM-zd-tree: A Fast Space-Partitioning Index Leveraging Processing-in-Memory](https://doi.org/10.1145/3774934.3786411)
  - Yiwei Zhao, Guy E. Blelloch, Phillip B. Gibbons (Carnegie Mellon University, Pittsburgh, USA)；Hongbo Kang (Tsinghua University, Beijing, China)；Ziyang Men, Yan Gu (University of California, Riverside, Riverside, USA)；Laxman Dhulipala (University of Maryland, College Park, USA)；Charles McGuffey (Reed College, Portland, USA)。
  - PIM-zd-tree 面向真实 PIM DIMM 的多维 point/query，使用可调 multi-layer z/d-tree；各层按访问频率和剩余粒度选择不同 layout、partition 与 cache，理论模型约束 PIM core 负载、memory-channel transfer 和空间，practical chunking/lazy counter 降低构建与更新开销。
  - 相较把 CPU kd/R-tree 直接分片到 PIM、导致通道通信和 core 倾斜，核心创新是让索引每一层采用不同数据组织，并从理论到实现共同适配近存计算限制。
  - Processing-in-Memory、空间索引、多层数据结构、负载均衡、内存通道通信

- [BEEMS: Boosting Machine Vision Efficiency via Computation Graph-Based Memory Smoothing](https://doi.org/10.1145/3774934.3786430)
  - Hanjing Shen, Fangxin Liu, Li Jiang, Haibing Guan (Shanghai Jiao Tong University, Shanghai, China)；Jian Liu (Beijing University of Aeronautics and Astronautics, Beijing, China)。
  - BEEMS 面向 edge vision foundation model inference，分析 computation graph 中随时间变化达 10× 的 memory peak/trough；search 对 peak operator 选择 partition、kernel substitution、swap 或 rematerialization，对 trough subgraph 用替换追回 latency，在动态 memory budget 下联合最小化峰值和端到端时间。
  - 相较逐 layer 使用单一 offload/checkpoint 策略、把内存峰值压低却普遍加慢，核心创新是以整图时间线做 memory smoothing，用低占用区间吸收高峰并按算子性质组合不同机制。
  - AI Compiler、视觉基础模型、边缘推理、Memory Smoothing、Rematerialization

- [Laser: Unlocking Layer-Level Scheduling for Efficient Multi-SLO LLM Serving](https://doi.org/10.1145/3774934.3786413)
  - Jianxiong Liao, Quanxing Dong, Yunkai Liang, Zhi Zhou, Xu Chen (Sun Yat-sen University, Guangzhou, China)。
  - Laser 面向同一 LLM service 中不同 TTFT/TPOT/吞吐 SLO，把 iteration 内模型执行拆为 layer operation；instance 内 scheduler 可让高优先 request 只在下一层插入而不等整轮结束，跨 instance dispatcher 根据队列、layer progress 和 SLO slack 迁入/分发请求，协调细粒度执行同时维持 batching。
  - 相较 continuous batching 仍以整次 decoding iteration 为最小调度单位，核心创新是把 preemption/优先级下沉到 layer，并与跨实例 dispatch 统一，打破 multi-SLO 请求被同一轮锁步的限制。
  - LLM Infra、Layer-Level Scheduling、Multi-SLO Serving、Request Dispatch、Continuous Batching

- [MixFusion: A Patch-Level Parallel Serving System for Mixed-Resolution Diffusion Models](https://doi.org/10.1145/3774934.3786420)
  - Desen Sun (University of Waterloo, Waterloo, Canada)；Zepeng Zhao (Carnegie Mellon University, Pittsburgh, USA)；Yuke Wang (Rice University, Houston, USA)。
  - MixFusion 面向不同输出分辨率混合到达的 diffusion request，把 image latent 切为 patch 作为 batch/schedule 粒度；不同请求的 patch 可组成形状兼容的并行 task，patch-aware cache 保留可复用 locality，online latency predictor 估计组合执行时间，SLO scheduler 决定何时拼批和分配 GPU。
  - 相较按整张图 batching 只能同分辨率成批、异构请求导致 padding 或 GPU 空洞，核心创新是将 serving 并行和 cache 管理共同下沉到 patch，并在 SLO 下混合分辨率。
  - AI Infra、Diffusion Serving、Patch-Level Parallelism、Mixed Resolution、SLO Scheduling

- [ChituDiffusion: A Data-Characteristic-Aware Serving System for Diffusion Models](https://doi.org/10.1145/3774934.3786424)
  - Chengzhang Wu, Liyan Zheng, Haojie Wang, Kezhao Huang, Zixuan Ma, Dong Dong, Jidong Zhai (Tsinghua University, Beijing, China)。
  - ChituDiffusion 面向图像/视频等 diffusion serving，从分辨率、shape、step 等 data property 的局部性把 pipeline 重组为 dGraph；compile time 为每类性质生成多个专用 execution engine，runtime 将到达请求细分并按相似性质重新 batching，再路由到匹配 engine，协同 fusion、layout 与并行配置。
  - 相较每个模型编译一个通用 engine、runtime 只按模型/尺寸粗分 batch，核心创新是以数据性质为跨请求与跨 stage 的共同优化键，连接编译多版本和在线重组。
  - AI Infra、Diffusion Serving、Data-Characteristic、Multi-Version Compilation、细粒度 Batching

- [ElasGNN: An Elastic Training Framework for Distributed GNN Training](https://doi.org/10.1145/3774934.3786440)
  - Siqi Wang, Hailong Yang, Pengbo Wang, Hongliang Cao, Xuezhu Wang, Zhongzhi Luan, Yi Liu, Depei Qian (Beihang University, Beijing, China)；Yufan Xu (Independent Researcher, Cupertino, USA)。
  - ElasGNN 面向共享 cluster 中 GNN training job 的动态 GPU 增减，scale-out/scale-in 时分别用增量 graph repartition algorithm 迁移最少 vertex/feature 并重建 sampler；elastic engine 保持训练状态，scheduler 根据预计 repartition cost、剩余时长和空闲 GPU 决定是否扩缩，联合缩短 JCT/makespan。
  - 相较 DNN elastic training 只 reshard dense model/data、用于 GNN 会全图重分区，核心创新是为图数据设计方向不同的低迁移扩/缩算法，并让调度器显式计入 scaling cost。
  - AI Infra、GNN 训练、Elastic Scaling、Graph Repartition、集群调度

- [APERTURE: Algorithm-System Co-optimization for Temporal Graph Network Inference](https://doi.org/10.1145/3774934.3786450)
  - Yiqing Wang, Hailong Yang, Enze Yu, Qingxiao Sun, Kejie Ma, Kaige Zhang, Chenhao Xie, Depei Qian (Beihang University, Beijing, China)。
  - APERTURE 面向 temporal graph network inference，打破每个时间点必须 memory update 后才 aggregate 的锁步，在保持预测等价时将 update 与 aggregation 解耦；computation-graph transformation 联合聚合多个 temporal state，dependency-aware reconstruction 去掉重复 memory traffic，解析模型选择可安全合并的时间/状态粒度。
  - 相较 step-wise TGN runtime 串行处理每个 temporal event，核心创新是先从算法语义证明两阶段可重排，再利用全局状态视图共同优化中间表示、访存和并行粒度。
  - AI Infra、Temporal GNN 推理、状态解耦、计算图变换、粒度建模

- [TAC: Cache-Based System for Accelerating Billion-Scale GNN Training on Multi-GPU Platform](https://doi.org/10.1145/3774934.3786460)
  - ZhiQiang Liang, Hongyu Gao, Jue Wang, Xingguo Shi (Computer Network Information Center, Chinese Academy of Sciences, Beijing, China; University of Chinese Academy of Sciences, Beijing, China)；Fang Liu, Junyu Gu, Sian Li, Lei Tang, Chunbao Zhou, Lian Zhao, Yangang Wang, Xuebin Chi (Computer Network Information Center at Chinese Academy of Sciences, Beijing, China; University of Chinese Academy of Sciences, Beijing, China)；Peng Di (Ant Group, Beijing, China; The University of New South Wales, Sydney, Australia)。
  - TAC 面向 billion-scale power-law graph 的 multi-GPU mini-batch GNN training，根据 cache hit 顶点分布做 data-affinity placement，提高 sampler/feature cache 局部性；sparsity-aware operator 依据数据在 cache/remote 的位置动态选 dense/sparse 计算路径，细粒度 pipeline 重叠 sampling、传输和 GPU compute。
  - 相较仅缓存高频 vertex、忽略命中数据的分布和算子形态，核心创新是把 cache placement、位置感知 sparse operator 与训练 pipeline 联合设计。
  - AI Infra、十亿级 GNN 训练、多 GPU、Feature Cache、稀疏算子、自流水

- [DTMiner: A Data-Centric System for Efficient Temporal Motif Mining](https://doi.org/10.1145/3774934.3786416)
  - Yinbo Hou, Hao Qi, Jin Zhao, Yu Zhang, Lin Gu, Wenbin Jiang, Xiaofei Liao, Hai Jin (Huazhong University of Science and Technology, Wuhan, China)；Ligang He (University of Warwick, Coventry, United Kingdom)；Hui Yu (Hong Kong University of Science and Technology, Hongkong, China)；Longlong Lin (Southwest University, Chongqing, China)。
  - DTMiner 面向多条 temporal motif matching task 在同一图上反复、碎片化 traversal，按时间顺序把 graph chunk 依次加载 cache；Load–Explore–Synchronize 模型在每个 chunk 驻留时唤醒所有相关 search-tree task 完成扩展，再细粒度同步进入下一块，从而共享读取并把随机访问限制在 cache 内。
  - 相较以 motif task 为中心各自遍历完整 temporal graph，核心创新是反转执行循环为 data-centric chunk 驱动，使空间相似、时间单调的访问在任务间合并。
  - Temporal Motif Mining、Data-Centric Execution、Cache Locality、Search Tree、图挖掘

- [FlashAttention-T: Towards Fully Tensorized Attention by Exploiting Tensor-Vector Parallelism](https://doi.org/10.1145/3774934.3786425)
  - Jianxing Xu (University of Science and Technology of China, Hefei, China; Institute of Computing Technology, Chinese Academy of Sciences, Beijing, China)；Yuanbo Wen, Jun Bi, Guanglin Xu, Rui Zhang, Wei Li, Qi Guo (Institute of Computing Technology, Chinese Academy of Sciences, Beijing, China)；Ruibai Xu (University of Science and Technology of China, Hefei, China; Institute of Computing Technology, Chinese Academy of Sciences, Beijing, China)；Ling Li (Institute of Software, Chinese Academy of Sciences, Beijing, China; University of Chinese Academy of Sciences, Beijing, China)；Tianshi Chen (Cambricon Technologies, Beijing, China)；Yunji Chen (Institute of Computing Technology, Chinese Academy of Sciences, Beijing, China; University of Chinese Academy of Sciences, Beijing, China)。
  - FlashAttention-T 面向 fused attention 中 Tensor Core 做 GEMM、CUDA vector unit 做 softmax 导致的 vector interval，将 scaling/max/sum 等 softmax primitive 编码为特殊 operand 的 MMA；numerically stable online softmax 在 tensor/vector unit 间并行分工，architecture-aware schedule 让空闲 Tensor Core 接手关键 vector 工作。
  - 相较 FlashAttention 只融合 HBM traffic、内部仍串行衔接 GEMM 与 vector softmax，核心创新是把非矩阵 softmax 原语合法映射到 MMA，并做 tensor–vector heterogeneous parallelism。
  - LLM Kernel、Attention、Tensor Core、Online Softmax、Tensor-Vector Parallelism

- [Accelerating Sparse Transformer Inference on GPU](https://doi.org/10.1145/3774934.3786434)
  - Wenhao Dai, Haodong Deng, Mengfei Rong, Qianwen Cao (China University of Petroleum-Beijing, Beijing, China)；Xinyu Yang, Hailong Yang, Qingxiao Sun (Beihang University, Beijing, China)；Hongyu Liu (Baidu, Beijing, China)；Fangxin Liu (Shanghai Jiao Tong University, Shanghai, China)。
  - STOF 面向带动态/多种 mask 的 sparse Transformer inference，解析模型根据稀疏形态把 MHA 映射为 row-wise 或 block-wise kernel 及对应 storage format；下游 operator fusion 表达为 compilation template，再以两阶段搜索选择 fusion boundary、tile 和 launch configuration，适配不同模型/输入。
  - 相较静态 fusion 固定算子组合、稀疏 attention 仍走通用 dense kernel，核心创新是以解析稀疏模型选择 MHA 路径，再用模板化搜索动态配置后续融合。
  - LLM Kernel、Sparse Transformer、Mask、Operator Fusion、GPU Autotuning

- [MetaAttention: A Unified and Performant Attention Framework across Hardware Backends](https://doi.org/10.1145/3774934.3786444)
  - Feiyang Chen, Xingda Wei, Haibo Chen (Shanghai Jiao Tong University, Shanghai, China)；Yu Cheng, Lei Wang, Zhi Yang (Peking University, Beijing, China)；Yuqing Xia, Ziming Miao, Lingxiao Ma, Fan Yang, Jilong Xue, Mao Yang (Microsoft Research, Beijing, China)。
  - MetaAttention 将标准、稀疏、变长等 attention 抽象成 relevance scoring 与 aggregation 两个主操作，加用户可定制函数/shape；跨 backend runtime 生成候选实现，IntermediateTensor search 枚举中间张量 tile、materialization 与并行映射，根据算法参数和硬件特征选最优配置。
  - 相较 FlashAttention/FlashMLA 为单算法和单平台手写 kernel，核心创新是以两个操作加 IntermediateTensor 搜索统一 attention family，在新变体/硬件上自动导出接近手调性能的实现。
  - AI Compiler、Attention Framework、跨硬件 Backend、Tiling Search、Kernel Generation

- [Towards Singular Value Decomposition for Rank-Deficient Matrices: An Efficient and Accurate Algorithm on GPU Architectures](https://doi.org/10.1145/3774934.3786427)
  - Lu Shi, Shaoshuai Zhang (University of Electronic Science and Technology of China, Chengdu, China)；WeiWei Xu (Nanjing University of Information Science and Technology, Nanjing, China)。
  - 该 SVD 面向 rank 未知但实际 rank-deficient 的 dense matrix，先以 rank-revealing Householder QB factorization 自动找出有效子空间，再只对小 B matrix 做 SVD；mixed-precision 路径将大规模投影放低精度、关键正交/分解保留高精度，并给出 backward-error/稳定性分析。
  - 相较 cuSOLVER 按 full rank 处理大量零奇异方向、randomized SVD 需预先给 rank 且精度不稳，核心创新是 rank revealing QB 与稳定 Householder/混合精度组合，自动按真实秩缩小问题。
  - 奇异值分解、Rank-Deficient Matrix、Householder QB、混合精度、GPU

- [A Diagonal Block Memory-Aware Polynomial Preconditioner for Linear and Eigenvalue Solvers](https://doi.org/10.1145/3774934.3786446)
  - Xiaojian Yang, Yuhui Ni, Shengguo Li, Dezun Dong, Chuanfu Xu, Jie Liu (National University of Defense Technology, Changsha, China)；Fan Yuan (Xiangtan University, Changsha, China)；Haipeng Jia (University of Chinese Academy of Sciences, Beijing, China)。
  - DBMPK 面向 polynomial preconditioner 中反复执行 A^k x 的 matrix-power kernel，把 sparse A 切为 diagonal block 与 off-diagonal region；block 内多个 power step 重用 cache 中数据且彼此独立并行，边界贡献按阶段合并，避免通用 temporal blocking 的复杂依赖与高预处理。
  - 相较逐次 SpMV 每阶都读完整矩阵、或复杂 graph partition 预处理，核心创新是简单 diagonal blocking 同时暴露局部多步复用和无跨 block 依赖，并能扩展到线性/特征值 solver。
  - Polynomial Preconditioner、Matrix-Power Kernel、Diagonal Blocking、Cache Reuse、Krylov Solver

- [A Distributed Matrix-Block-Vector Multiplication in Presence of System Performance Variability](https://doi.org/10.1145/3774934.3786453)
  - Yuchen Ma, Bin Ren, Andreas Stathopoulos (College of William & Mary, Williamsburg, USA)。
  - SMatVec 面向维度 10^6–10^7 的 distributed dense matrix–block-vector multiplication，将 on-the-fly kernel matrix generation 与 1D pipeline matvec 融合；trace/simulator用约 5% node performance variation解释 pipeline bubble，随后以进程间预取、非常规静态线程调度、cache tile 和多版本 unroll 吸收抖动。
  - 相较假定各 rank 等速并用 work stealing 的 MatVec，核心创新是先量化小幅系统变异如何放大成流水空洞，再设计不引入动态争用的静态多版本执行来容忍它。
  - 分布式 MatVec、性能抖动、1D Pipeline、静态调度、Kernel Matrix

- [Characterizing Matrix Multiplication Units across General Parallel Patterns in Scientific Computing](https://doi.org/10.1145/3774934.3786456)
  - Yuechen Lu, Hongwei Zeng, Weifeng Liu (China University of Petroleum-Beijing, Beijing, China)；Marc Casas (Barcelona Supercomputing Center, Barcelona, Spain; Universitat Politècnica de Catalunya, Barcelona, Spain)。
  - Cubie 是面向科学计算 Matrix Multiplication Unit 的十类 parallel-pattern benchmark，把 stencil、reduction、sparse/structured 等 kernel 重写为 tile MMA；在不同处理器/精度上同时测 throughput、power、numerical error 和 memory behavior，并按计算密度与映射规则性划分四个利用象限、总结九项限制。
  - 相较只用 AI GEMM 峰值推断 Tensor/MMU 对 HPC 的价值，核心创新是以覆盖一般并行模式的统一 benchmark 做多维实测，区分哪些科学算子真正受益及受何种精度/访存边界限制。
  - Matrix Multiplication Unit、科学计算基准、Tensor Core、能耗、数值精度、性能表征
