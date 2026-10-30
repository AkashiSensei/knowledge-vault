# PPoPP 2024 论文列表

范围以 PPoPP 2024 官方 Main Conference program 和 ACM proceedings 交叉核对为准，共 32 篇主会长文；已从 proceedings 的 45 项中排除 12 篇 poster 和 1 篇 keynote。以下标题均链接至论文 DOI；已找到的 3 份合法公开 PDF 保存在 `reference/PPoPP/2024/`。

- [Scaling Up Transactions with Slower Clocks](https://doi.org/10.1145/3627535.3638472)
  - Pedro Ramalhete (Cisco Systems, Lausanne, Switzerland)；Andreia Correia (University of Neuchatel, Neuchatel, Switzerland)。
  - DCTL 面向读乐观、写悲观的事务并发控制，把每次写事务都递增的全局版本时钟改为延迟更新：连续且写集互不相交的事务可沿用时钟，DCOTL 还允许部分写集重叠的连续事务不推进时钟；在保持 opacity、可选无饥饿和持久化语义下，目标是解除高核数写事务的原子时钟瓶颈。
  - 相较 TL2 类算法把一次写提交绑定一次全局时钟递增，核心创新是依据连续事务的访问关系证明何时可以安全省略时钟更新，并把这一条件扩展到磁盘持久事务数据库。
  - 事务内存、并发控制、全局版本时钟、Opacity、持久化数据库

- [Locks as a Resource: Fairly Scheduling Lock Occupation with CFL](https://doi.org/10.1145/3627535.3638477)
  - Jonggyu Park (University of Washington, Seattle, United States of America)；Young Ik Eom (Dept. of Electrical and Computer Engineering / College of Computing and Informatics, Sungkyunkwan University, Suwon, Kyunggi-Do, Republic of Korea)。
  - CFL 把容器间共享锁的占用时间视作可调度资源：锁在交接时读取线程的优先级与 cgroup 归属，按应用累计持锁时间公平选取下一持有者，并按 NUMA 拓扑组织等待者以避免跨节点扩展瓶颈，从而抑制多租户应用因锁竞争产生的吞吐抖动与不公平。
  - 相较只优化锁本身吞吐或 FIFO 公平性的方案，核心创新是把操作系统的 cgroup/优先级语义嵌入锁交接，让公平对象从线程提升为应用的持锁时间份额。
  - 多租户同步、锁调度、Cgroup、公平性、NUMA

- [Are Your Epochs Too Epic? Batch Free Can Be Harmful](https://doi.org/10.1145/3627535.3638491)
  - Daewoo Kim, Trevor Brown, Ajay Singh (University of Waterloo, Waterloo, Canada)。
  - 该研究定位出 EBR 等批量内存回收在延迟线程出现时的真实慢点并非只有 epoch 推进，而是大批 free 绕过现代 allocator 的有界线程缓存、触发高延迟释放；它把一个大回收批次摊到后续操作中渐进释放，并把同一修复应用到十种回收器和 token-passing EBR。
  - 相较继续缩短 grace period 或替换回收协议，核心创新是揭示回收批量与通用 allocator 缓存之间的跨层干扰，并用协议无关的 batch amortization 修复多种既有算法。
  - Epoch-Based Reclamation、内存分配器、批量释放、无锁数据结构、尾延迟

- [Liger: Interleaving Intra- and Inter-Operator Parallelism for Distributed Large Model Inference](https://doi.org/10.1145/3627535.3638466)
  - Jiangsu Du, Jinhui Wei, Jiazhi Jiang, Dan Huang, Zhiguang Chen, Yutong Lu (Sun Yat-sen University, Guangzhou, China)；Shenggan Cheng (National University of Singapore, Singapore, Singapore)。
  - Liger 面向多 GPU 大模型在线推理，以单个请求内算子切分的低延迟和请求间流水的低通信为两端，在多个请求之间交错排布计算核与 collective；runtime 用 CPU–GPU/stream 间同步精确控制执行顺序，以 contention factor 预估资源争用，并在运行时切碎长 kernel 扩大重叠窗口。
  - 相较只选 tensor parallel 或 pipeline/inter-operator parallelism，核心创新是在请求粒度跨流交错两类并行，并显式把 kernel 争用与可切分性纳入调度，而非静态固定一种部署。
  - LLM Infra、分布式推理、请求间调度、计算通信重叠、多 GPU

- [A Holistic Approach to Automatic Mixed-Precision Code Generation and Tuning for Affine Programs](https://doi.org/10.1145/3627535.3638484)
  - Jinchen Xu, Bei Zhou, Fei Li, Jiangwei Hao (Information Engineering University, Zhengzhou, China)；Guanghui Song (Li Auto Inc., Shanghai, China)；Jie Zhao (College of Computer Science and Electronic Engineering, Hunan University, Changsha, China)。
  - PrecTuner 面向 affine loop 程序的混合精度优化，把每个运算的精度选择、由此引入的 cast、loop transformation 与允许的数值误差共同编码为一个搜索参数；它只采样少量生成代码做 profiling，拟合性能模型后预测最佳参数，避免等到生成代码后才发现转换开销。
  - 相较先做精度分配、再独立 autotune 的两阶段流程，核心创新是让代码生成器与调优器共享同一参数化空间，从搜索时就同时计入转换成本、循环变换和质量预算。
  - 混合精度、Affine Program、自动调优、代码生成、数值误差预算

- [Language-Agnostic Static Deadlock Detection for Futures](https://doi.org/10.1145/3627535.3638487)
  - Stefan K Muller (Illinois Institute of Technology, Chicago, Illinois, United States of America)。
  - 该工作对 futures 程序先抽取与源语言无关的 graph type，再在类型图上推导 future 创建、get 与控制依赖形成的等待环；新的类型系统给出 soundness 证明，并以扩展 futures 的 OCaml 子集验证可实现性，从编译期报告潜在死锁。
  - 相较为某一种语言直接构造依赖图，核心创新是在可复用的 graph-type 中间表示上完成有证明的死锁判定，同时修正此前依赖错误猜想的分析。
  - Future、静态死锁检测、Graph Type、类型系统、语言无关分析

- [Recurrence Analysis for Automatic Parallelization of Subscripted Subscripts](https://doi.org/10.1145/3627535.3638493)
  - Akshay Bhosale (Electrical and Computer Engineering, University of Delaware, Newark, DE, USA)；Rudolf Eigenmann (Electrical and Computer Engineering, University of Delaware, Newark, DE, United States of America)。
  - 该编译分析面向 `a[b[i]]` 一类间接下标循环，沿数组值的递推定义求解一维的非规则/间歇单调性和多维单调性；自动并行器据此排除跨迭代依赖并安全插入 OpenMP directive，使过去因 index array 未知而保持串行的循环可并行执行。
  - 相较只能识别简单一维单调递推的 dependence analysis，核心创新是把复杂递推和间歇/多维单调性质纳入编译期证明，扩大 subscripted-subscript 可自动并行化范围。
  - 自动并行化、间接下标、递推分析、依赖分析、OpenMP

- [OsirisBFT: Say No to Task Replication for Scalable Byzantine Fault Tolerant Analytics](https://doi.org/10.1145/3627535.3638468)
  - Kasra Jamshidi, Keval Vora (Simon Fraser University, Burnaby, British Columbia, Canada)。
  - OsirisBFT 面向分布式 task-parallel analytics，把纯计算任务与会改变状态的任务分开：前者不再为容忍每个 Byzantine failure 做全副本执行，而由应用提供的通用 verification operator 检查输出，状态更新再走必要的一致性路径；正常执行时尽量本地验证、少协调，并可独立横向增加计算 worker。
  - 相较按容错数复制所有任务的 state-machine replication，核心创新是用应用语义验证替代无差别计算复制，使分析吞吐的扩展不再被预期故障数绑定。
  - Byzantine Fault Tolerance、任务并行、结果验证、分布式分析、可扩展性

- [Towards Scalable Unstructured Mesh Computations on Shared Memory Many-Cores](https://doi.org/10.1145/3627535.3638473)
  - Haozhong Qiu, Jianbin Fang, Qingsong Wang, Yue Ding, Shizhao Chen (College of Computer Science and Technology, National University of Defense Technology, Changsha, China)；Chuanfu Xu, Yonggang Che, Jie Liu (Laboratory of Digitizing Software for Frontier Equipment, College of Computer Science and Technology, National University of Defense Technology, Changsha, China)；Liang Deng, Jian Zhang, Zhe Dai (China Aerodynamic Research and Development Center, Mianyang, China)。
  - 该方法把不规则网格递归划分并重排为 task dependency tree，以叶/子树为执行粒度显式记录共享顶点造成的数据冲突和真实依赖；两种递归策略分别适配 CPU task runtime 与 GPU 执行，使工业 CFD 网格在保证更新顺序的同时暴露跨分区和树层的并行度。
  - 相较 graph coloring 或固定 mesh partition 只处理某类冲突，核心创新是以统一依赖树同时表达冲突与数据依赖，并能映射到 CPU/GPU 两类共享内存编程模型。
  - 非结构网格、任务依赖树、共享内存、多核 CPU、GPU、CFD

- [Extreme-scale Direct Numerical Simulation of Incompressible Turbulence on the Heterogeneous Many-core System](https://doi.org/10.1145/3627535.3638479)
  - Jiabin Xie, Guangnan Feng, Han Huang, Junxuan Feng, Zhiguang Chen, Yutong Lu (Sun Yat-sen University, Guangzhou, China)。
  - PowerLLEL++ 面向天河异构众核上的不可压湍流 DNS，在网格、节点和加速核多层分解工作；runtime 依据层级内存做 stencil tiling/复用与 kernel fusion，用 PDD 并行三对角求解减少全局 transpose，再以 RDMA 优化剩余 transpose 和 halo exchange，扩展到 258 亿网格点。
  - 相较把 CPU CFD solver 逐 kernel 移植到加速器，核心创新是同时重构多层并行、内存局部性、线性求解与 RDMA 通信，形成面向超算拓扑的端到端 DNS solver。
  - 直接数值模拟、异构众核、Stencil、三对角求解、RDMA、超大规模 CFD

- [Pure: Evolving Message Passing To Better Leverage Shared Memory Within Nodes](https://doi.org/10.1145/3627535.3638503)
  - James Psota (CSAIL, Massachusetts Institute of Technology, Cambridge, MA, USA)；Armando Solar-Lezama (CSAIL, Massachusetts Institute of Technology, Cambridge, MA, United States of America)。
  - Pure 在以 message passing 为主的多节点程序中识别每节点空闲核和 rank 间通信状态：等待远端消息的核可从同节点 rank 窃取 task，节点内消息与 collective 则绕过进程间协议，落到共享内存中的 lock-free queue/structure；目标是在保留消息传递接口时利用节点内共享内存。
  - 相较纯 MPI 把每个 rank 固定到核、或另起一套共享内存编程模型，核心创新是把跨 rank work stealing 与无锁节点内通信同时嵌入 message-passing runtime。
  - 消息传递、共享内存、Work Stealing、节点内 Collective、混合并行 Runtime

- [INFINEL: An efficient GPU-based processing method for unpredictable large output graph queries](https://doi.org/10.1145/3627535.3638490)
  - Sungwoo Park, Min-Soo Kim (Korea Advanced Institute of Science and Technology, Daejeon, Republic of Korea)；Seyeon Oh (GraphAI, Daejeon, Republic of Korea)。
  - INFINEL 面向 triangle listing 等输出规模事前不可知且可能超过 GPU buffer 的图查询，让每个线程按需领取 output chunk，并在空间阈值到达时停止/重启 kernel，从一次遍历持续产出结果；它依据运行中的实际输出量扩展空间，而不先执行计数阶段再静态切子任务。
  - 相较 count-then-execute 的两阶段 GPU 图查询，核心创新是将线程级 chunk allocation 与可恢复 kernel 组合成单阶段协议，对极端倾斜输出也不必重复整条查询。
  - GPU 图查询、不可预测输出、Chunk Allocation、Kernel Restart、Triangle Listing

- [GraphCube: Interconnection Hierarchy-aware Graph Processing](https://doi.org/10.1145/3627535.3638498)
  - Xinbiao Gan, Guang Wu, Feng Xiong, Jiaqi Si, Jianbin Fang, Dezun Dong, Chunye Gong, Tiejun Li (National University of Defense Technology, Changsha, China)；Shenghao Qiu, Zheng Wang (University of Leeds, Leeds, United Kingdom)。
  - GraphCube 面向具有节点内、机架/组间等多级通信代价的超大规模机器，把图顶点和边按 interconnect hierarchy 做层次化 partition：每层同时估计分区负载与跨该层链路的数据量，再将图算子按同一映射执行，减少最昂贵层级的通信并扩展到 7.9 万节点、120 万核。
  - 相较只平衡顶点/边数或把所有网络链路视作同价的 partitioner，核心创新是让图划分结构与机器互连层级同构，逐层优化负载和通信。
  - 大规模图计算、拓扑感知划分、层次互连、Graph500、通信优化

- [Exploiting Fine-Grained Redundancy in Set-Centric Graph Pattern Mining](https://doi.org/10.1145/3627535.3638507)
  - Zhiheng Lin, Chaoyang Shui, Kewei Zhang, Junmin Xiao, Guangming Tan (Institute of Computing Technology, Chinese Academy of Sciences, University of Chinese Academy of Sciences, beijing, China)；Ke Meng (Alibaba, beijing, China)。
  - 该工作面向 set-centric GPU 图模式挖掘，把不同 set formula 中反复检查的同一顶点对识别为细粒度冗余；它向关系代数式抽象加入 set union，把若干集合运算合并后只做一次 edge check，同时保留 matching order、automorphism breaking 和结果复用等既有优化。
  - 相较只复用完全相同集合表达式的粗粒度消重，核心创新是跨不相关集合操作融合由图局部性产生的重复边检查。
  - 图模式挖掘、Set-Centric Abstraction、集合并、边检查复用、GPU 集群

- [Memory Bounds for Concurrent Bounded Queues](https://doi.org/10.1145/3627535.3638497)
  - Vitaly Aksenov (City, University of London, London, United Kingdom)；Nikita Koval (JetBrains, Amsterdam, Netherlands)；Petr Kuznetsov (Telecom Paris, Institut Polytechnique Paris, Paris, France)；Anton Paramonov (EPFL, Lausanne, Switzerland)。
  - 该理论工作研究容量固定为 n 的非阻塞 queue，在预分配 element array 之外最少还需多少同步元数据：若硬件提供 LL/SC 或元素全异，常数个定位 counter 足够；在一般 CAS/ABA 条件下，则证明任何 memory-optimal 实现都需要随并发进程数线性增长的额外空间。
  - 相较只给出新的 bounded queue 实现，核心创新是首次按硬件原语与 ABA 条件给出额外内存的可达上界和线性下界，刻画“常数开销”何时不可能。
  - 非阻塞有界队列、空间下界、ABA、CAS、并发算法理论

- [VERLIB: Concurrent Versioned Pointers](https://doi.org/10.1145/3627535.3638501)
  - Guy E. Blelloch (Computer Science, Carnegie Mellon University, Pittsburgh, Pennsylvania, USA)；Yuanhao Wei (Computer Science, Carnegie Mellon University, Pittsburgh, Pennsylvania, United States of America)。
  - Verlib 以 C++ versioned pointer 封装 load、CAS 和常数时间 snapshot，让 B-tree、ART 与 hash table 的 range query 可在一个一致版本上执行；indirection-on-need 只在必须保留旧版本时加间接层，idempotent CAS 又让 snapshot 能与 lock-free lock 共存。
  - 相较此前 snapshot transformation 要么强制每个指针间接访问、要么限制数据结构形态，核心创新是按需间接化并复用版本元数据实现幂等 CAS，使锁式与 CAS 式结构可低改动接入。
  - 版本化指针、线性化快照、Range Query、Idempotent CAS、C++ 并发库

- [Practical Hardware Transactional vEB Trees](https://doi.org/10.1145/3627535.3638504)
  - Mohammad Khalaji, Trevor Brown, Khuzaima Daudjee (University of Waterloo, Waterloo, Ontario, Canada)；Vitaly Aksenov (City, University of London, London, United Kingdom)。
  - 该 concurrent vEB tree 用 HTM 将递归 summary、cluster 更新及 predecessor/successor 路径包入短事务；无冲突时保留 vEB 的 O(log log U) 操作复杂度，并通过紧凑布局将传统 vEB 的巨大 universe 空间压低，从而提供可实用的 ordered set/map。
  - 相较并发 vEB 通过删掉 recursive summary 换取同步简单、因而失去快速前驱/后继查询，核心创新是用硬件事务完整保留递归结构及双对数复杂度。
  - Van Emde Boas Tree、硬件事务内存、并发 Map、Predecessor Query、空间优化

- [Tetris: Accelerating Sparse Convolution by Exploiting Memory Reuse on GPU](https://doi.org/10.1145/3627535.3638471)
  - Xiaoyan Liu, Xuegui Zheng, Hailong Yang, Zhongzhi Luan, Depei Qian (Beihang University, Beijing, China)。
  - Tetris 面向权重非结构化稀疏的 CNN inference，先按输出位置聚合可复用 input，减少从 global memory 重取；随后以 stride-packed filter 和 bank-sensing 重排把不规则稀疏访问变成 coalesced/bank-friendly 访问，再按 filter group 重排平衡线程工作，并自动选择 tile/并行参数。
  - 相较直接调用通用稀疏卷积或只压缩权重，核心创新是围绕 input reuse 共同设计稀疏 filter format、shared-memory bank 布局和负载重排。
  - DNN 推理、稀疏卷积、GPU 内存复用、Stride-Packed Filter、负载均衡

- [Shared Memory-contention-aware Concurrent DNN Execution for Diversely Heterogeneous System-on-Chips](https://doi.org/10.1145/3627535.3638502)
  - Ismet Dagli (Computer Science Department, Colorado School of Mines, Golden, United States of America)；Mehmet E. Belviranli (Computer Science Department, Colorado School of Mines, Golden, USA)。
  - HaX-CoNN 面向 Orin、Xavier、Snapdragon 等共享内存异构 SoC 上并发到达的多个 DNN inference，把调度粒度降到 layer；离线/在线 characterization 提供各层在 CPU/GPU/DLA 等 accelerator 的时延、共享内存带宽争用和跨 accelerator transition 成本，优化器据此映射各层以最小化端到端时延或最大化总吞吐。
  - 相较按整模型绑定单一 accelerator 或只比较单层执行时间，核心创新是把共享内存 contention 与跨设备切换代价一并纳入多模型逐层映射。
  - AI Infra、并发 DNN 推理、异构 SoC、Layer Mapping、共享内存争用

- [Training one DeePMD Model in Minutes: a Step towards Online Learning](https://doi.org/10.1145/3627535.3638505)
  - Siyu Hu (State Key Lab of Processors, Institute of Computing Technology, Chinese Academy of Sciences, Beijing, Beijing, China; University of Chinese Academy of Sciences, Beijing, China)；Tong Zhao, Qiuchen Sha, Guangming Tan, Weile Jia (State Key Lab of Processors, Institute of Computing Technology, Chinese Academy of Sciences, Beijing, China; University of Chinese Academy of Sciences, Beijing, China)；Enji Li (State Key Lab of Processors, Institute of Computing Technology, Chinese Academy of Sciences, Beijing, China)；Xiangyu Meng (College of Computer Science and Technology, Qingdao Institute of Software, China University of Petroleum, Qingdao, Shandong, China)；Liping Liu, Lin-Wang Wang (Institute of Semiconductors, Chinese Academy of Sciences, Beijing, China; University of Chinese Academy of Sciences, Beijing, China)。
  - 该系统面向需要同时拟合能量和原子力梯度的 DeePMD 训练，以 Extended Kalman Filter 构造 heuristic minibatch quasi-Newton optimizer；在多样本间提前规约 gradient/error，减少显存和通信，再用对称性 descriptor 定制 kernel 利用异构 GPU，把单模型训练从小时压到分钟。
  - 相较 Adam 难以高效扩大该任务的 minibatch、旧有逐层 EKF 又通信和显存过重，核心创新是把准牛顿更新重写为可批量并行的早规约形式并与领域 kernel 协同。
  - 科学机器学习、DeePMD 训练、Extended Kalman Filter、Minibatch、GPU Kernel

- [ParlayANN: Scalable and Deterministic Parallel Graph-Based Approximate Nearest Neighbor Search Algorithms](https://doi.org/10.1145/3627535.3638475)
  - Magdalen Dobson Manohar, Guy Blelloch (Carnegie Mellon University, Pittsburgh, USA)；Zheqi Shen (University of California, Riverside, Riverside, USA)；Laxman Dhulipala (University of Maryland, College Park, College Park, United States)；Yan Gu, Yihan Sun (University of California, Riverside, Riverside, United States of America)；Harsha Vardhan Simhadri (Microsoft Research Lab India, Bangalore, India)。
  - ParlayANN 把 graph-based ANN index 的建图、搜索和更新拆成无锁/低同步的确定性并行原语，并为四种主流算法实现 billion-scale 版本；相同输入与参数在不同 thread interleaving 下仍生成一致索引和结果，同时随多核扩展以保持 recall–throughput 权衡。
  - 相较现有 ANN library 依赖锁和串行阶段、运行结果随调度变化，核心创新是为一组图 ANN 算法给出共享的确定性并行构件，而非只优化单个索引。
  - 近似最近邻、确定性并行、图索引、十亿级向量、相似度搜索

- [Parallel k-Core Decomposition with Batched Updates and Asynchronous Reads](https://doi.org/10.1145/3627535.3638508)
  - Quanquan C. Liu (Yale University, New Haven, USA)；Julian Shun (Massachusetts Institute of Technology, Cambridge, United States of America)；Igor Zablotchi (Mysten Labs, Zürich, Switzerland)。
  - 该 dynamic k-core 结构让 edge update 仍以 batch 并行处理，但 read 不必等整个 batch 结束：系统跟踪 update 间的 causal dependency，把因果相关的一组更新对 reader 原子呈现，读者异步获取一致的近似 coreness；同时证明 read/update 的 linearizability、liveness 与原近似界。
  - 相较 SPAA 方案强制读和更新轮流批处理，核心创新是以因果组为最小原子单元，在不串行所有读的条件下保持动态 k-core 的一致性保证。
  - 动态图、K-Core、批量更新、异步读取、因果依赖、线性一致性

- [Parallel Integer Sort: Theory and Practice](https://doi.org/10.1145/3627535.3638483)
  - Xiaojun Dong, Yan Gu, Yihan Sun (University of California, Riverside, Riverside, United States of America)；Laxman Dhulipala (University of Maryland, College Park, College Park, United States of America)。
  - DovetailSort 面向多核 integer key，把 radix/integer sorting 的按位分桶与 comparison sorting 对重复 key 的聚合能力组合；算法在采样/partition 时识别高频值并单独处理，使分布含大量 duplicates 时不再重复递归或产生倾斜，同时保持 work/depth 的理论效率。
  - 相较并行 radix sort 通常把重复键当独立元素、比较排序又未利用整数位宽，核心创新是用一条算法路径自适应衔接两类排序思想，并同时给出更紧的理论界和工程实现。
  - 并行整数排序、重复键、DovetailSort、Work-Depth 分析、多核

- [Fast American Option Pricing using Nonlinear Stencils](https://doi.org/10.1145/3627535.3638506)
  - Zafar Ahmad (Stony Brook University, Stony Brook, United States of America)；Reilly Browne, Rezaul Chowdhury, Yushen Huang, Yimin Zhu (Stony Brook University, Stony Brook, USA)；Rathish Das (University of Houston, Houston, United States of America)。
  - 该算法把美式期权的 binomial、trinomial 与 Black–Scholes–Merton 离散时间递推视作带提前执行 max 操作的非线性一维 stencil；通过分块多项式/FFT 加速跨时间步传播，把 T 步工作从二次量级降到 O(T log²T)，并在 greedy scheduler 上并行。
  - 相较逐时间步推进整条价格网格的 O(T²) 串/并行算法，核心创新是首次把含非线性 exercise boundary 的 stencil 重构为可用 FFT 的次二次算法。
  - 美式期权、非线性 Stencil、FFT、并行算法、次二次复杂度

- [ConvStencil: Transform Stencil Computation to Matrix Multiplication on Tensor Cores](https://doi.org/10.1145/3627535.3638476)
  - Yuetao Chen, Kun Li, Donglin Bai, Lingxiao Ma, Ting Cao, Mao Yang (Microsoft Research, Beijing, China)；Yuhao Wang (Microsoft Research, Beijing, China; University of Science and Technology of China, Hefei, China)；Lei Wang (Microsoft Research, Beijing, China; University of Chinese Academy of Sciences, Beijing, China)；Liang Yuan, Yunquan Zhang (Chinese Academy of Sciences, Beijing, China)。
  - ConvStencil 把 regular stencil 的邻域采样转换成 Tensor Core matrix multiplication：性能模型决定 tile，stencil2row 只物化必要布局，dual tessellation 与 kernel fusion 提高有效矩阵密度，lookup table 加 dirty-bit padding 消除 bank conflict/边界冲突，以在不改数值算子的前提下利用 TCU。
  - 相较专用 CUDA stencil kernel 或把完整 im2col 展开后调用 GEMM，核心创新是围绕 Tensor Core 约束共同设计低膨胀布局和计算 tessellation，并用模型选择实现。
  - Stencil、Tensor Core、Stencil2row、Kernel Fusion、科学计算加速

- [CPMA: An Efficient Batch-Parallel Compressed Set Without Pointers](https://doi.org/10.1145/3627535.3638492)
  - Brian Wheatman (Computer Science, Johns Hopkins University, Baltimore, MD, USA)；Randal Burns (Johns Hopkins University, Baltimore, MD, United States of America)；Aydin Buluc (Lawrence Berkeley National Laboratory, Berkeley, CA, United States of America)；Helen Xu (School of Computational Science and Engineering, Georgia Institute of Technology, Atlanta, GA, United States of America)。
  - CPMA 是无指针的 batch-parallel ordered set：元素按 packed-memory array 连续压缩存放，batch insert 只在局部密度越界时并行重平衡，range scan 直接顺序访问 cache line；它还作为动态图 edge store 支撑图算法与批量更新。
  - 相较 PaC-tree/Aspen 借指针快速做 parallel union 却牺牲 cache locality，核心创新是让压缩 PMA 的局部重平衡可批量并行，从而同时提高 update 与 scan。
  - Packed Memory Array、批并行集合、压缩数据结构、范围查询、动态图存储

- [Gallatin: A General-Purpose GPU Memory Manager](https://doi.org/10.1145/3627535.3638499)
  - Hunter Mccoy (University of Utah, Salt Lake City, United States of America)；Prashant Pandey (University of Utah, Salt Lake City, USA)。
  - Gallatin 面向 GPU kernel 内任意尺寸、并发的动态 allocation，以高度并发的 van Emde Boas tree 按空闲块大小索引内存，insert/delete/successor 为常数级操作；allocator 不再为若干固定 size class 各建专用 pipeline，也无需大对象回退 CUDA allocator，可支撑 streaming graph 的扩展/删除。
  - 相较 Ouroboros/Reg-Eff 只对固定尺寸快、混合或大尺寸即退化，核心创新是把并发 vEB size index 做成 GPU 可用的通用 allocator，统一覆盖 single-size 与 mixed-size 请求。
  - GPU 内存分配器、Van Emde Boas Tree、动态分配、混合尺寸、Streaming Graph

- [A Row Decomposition-based Approach for Sparse Matrix Multiplication on GPUs](https://doi.org/10.1145/3627535.3638470)
  - Meng Pang, Xiang Fei, Peng Qu, Youhui Zhang, Zhaolin Li (Department of Computer Science and Technology, Tsinghua University, Beijing, China)。
  - RoDe 对 CSR sparse row 按 nonzero 分布切成规则主体和残余段，前者用均匀 warp/tile 批量执行，后者单独负载均衡；SpMM/SDDMM kernel 再以细粒度 pipeline 重叠 sparse index、dense operand 读取和算术，依据行形态选择两条路径。
  - 相较为所有不规则行套同一种 mapping 或昂贵重排格式，核心创新是在保留标准 CSR 的条件下做 row decomposition，让规则计算和长尾残余分别获得合适并行度。
  - SpMM、SDDMM、CSR、行分解、GPU 负载均衡

- [Fast Kronecker Matrix-Matrix Multiplication on GPUs](https://doi.org/10.1145/3627535.3638489)
  - Abhinav Jangda (Microsoft Research, Redmond, Washington, United States of America)；Mohit Yadav (Manning College of Information & Computer Sciences, University of Massachusetts Amherst, Amherst, Massachusetts, USA)。
  - FastKron 为矩阵乘 Kronecker product 设计原生单/多 GPU kernel，不再把每一因子展开成一串通用 GEMM、transpose 和 tensor contraction；它依据因子尺寸融合中间阶段、重排 tile 和共享内存数据，并在多 GPU 间划分输出以减少中间 tensor materialization 与通信。
  - 相较用现成线性代数算子拼接 Kron-Matmul，核心创新是把 Kronecker 因子结构暴露给专用 kernel 和分布式执行，从而启用跨阶段融合与专属数据复用。
  - Kronecker Matrix Multiplication、GPU Kernel、多 GPU、算子融合、科学机器学习

- [Arrow Matrix Decomposition: A Novel Approach for Communication-Efficient Sparse Matrix Multiplication](https://doi.org/10.1145/3627535.3638496)
  - Lukas Gianinazzi (Computer Science, ETH Zurich, Zurich, Switzerland)；Alexandros Nikolaos Ziogas, Langwen Huang, Piotr Luczynski, Saleh Ashkboosh, Florian Scheidl, Armon Carigiet, Chio Ge, Nabil Abubaker, Maciej Besta, Tal Ben-Nun, Torsten Hoefler (ETH Zurich, Zurich, Switzerland)。
  - 该方法面向超出单节点内存、需反复执行 SpMM 的图/科学 workload，把原 sparse matrix 经 permutation 分解为少量 arrow matrix；每个 arrow 只在对角和窄边界保留非零，使节点持有的 dense feature 与矩阵块大多本地相乘，迭代时只交换结构化边界。
  - 相较沿用 dense 2D matrix multiplication 的分块通信，核心创新是先改变 sparse matrix 的结构表示；对 planar/minor-excluded graph 可证明每轮通信量获得多项式下降。
  - 分布式 SpMM、Arrow Matrix、通信规避、稀疏矩阵分解、GNN

- [FastFold: Optimizing AlphaFold Training and Inference on GPU Clusters](https://doi.org/10.1145/3627535.3638465)
  - Shenggan Cheng, Yang You (National University of Singapore, Singapore, Singapore)；Xuanlei Zhao, Guangyang Lu, Jiarui Fang (HPC-AI Tech, Beijing, China)；Tian Zheng (Xi'an Jiaotong University, Xi'an, China)；Ruidong Wu, Xiwen Zhang, Jian Peng (HeliXon, Beijing, China)。
  - FastFold 面向 AlphaFold 的训练和长序列推理：Dynamic Axial Parallelism 沿 MSA/pair representation 的轴动态切 tensor，在算子之间用 duality async operation 重叠 collective；定制 kernel 降低 Evoformer 开销，AutoChunk 根据序列长度和显存预算搜索 intermediate tensor 的分块，训练扩到多 GPU、推理避免 OOM。
  - 相较通用 data/tensor parallel 或人工设置固定 chunk，核心创新是利用 AlphaFold 二维表示的轴向结构共同设计模型并行、异步通信和自动显存分块，覆盖训练与推理全流程。
  - AI Infra、AlphaFold、模型并行、AutoChunk、计算通信重叠、GPU 集群

- [AGAThA: Fast and Efficient GPU Acceleration of Guided Sequence Alignment for Long Read Mapping](https://doi.org/10.1145/3627535.3638474)
  - Seongyeon Park, Jaeyong Song, Jinho Lee (Seoul National University, Seoul, Korea, South ? Republic of Korea)；Junguk Hong (Seoul National University, Seoul, Republic of Korea)；Hajin Kim (Yonsei University, Seoul, Republic of Korea)；Youngsok Kim (Yonsei University, Seoul, Korea, South ? Republic of Korea)。
  - AGAThA 在不改变 guided dynamic programming 语义的条件下，把 long-read alignment 的 band/guide 工作分配到 GPU：以重排与缓存消除跨步 strided/redundant access，按运行时 guide 长度和有效 cell 数处理难以预估的 workload imbalance，并保持与 CPU pipeline 完全一致的 alignment 结果。
  - 相较 GPU mapper 为吞吐采用会改变结果的启发式近似，核心创新是逐项诊断 exact guided alignment 的访存与负载问题，在保留算法结构和下游兼容性时加速。
  - 基因序列比对、Long Read、GPU、Guided Dynamic Programming、精确加速
