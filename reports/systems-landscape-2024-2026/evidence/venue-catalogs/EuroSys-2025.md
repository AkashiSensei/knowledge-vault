# EuroSys 2025 论文列表

EuroSys 2025 正式 proceedings 共收录 85 篇论文。以下标题链接至 ACM DOI 页面；每篇依次列出机构与主要作者、研究场景和系统机制、相较既有方法的核心创新，以及细粒度方向。当前可合法直接获取的 24 份 PDF 已保存到 `reference/EuroSys/2025/`；其余论文依据正式摘要整理，不使用非授权镜像。

- [Deft: A Scalable Tree Index for Disaggregated Memory](https://doi.org/10.1145/3689031.3696062)
  - Tsinghua University；Jing Wang、Qing Wang、Yuhao Zhang、Jiwu Shu
  - Deft 是 disaggregated memory 上的有序 tree index，重排远端节点访问和并发更新路径，减少网络往返与根部争用；不同负载下吞吐较既有有序索引高 2.4–9.5 倍。
  - 核心创新是按远端内存的 latency/parallelism 重新组织树遍历与并发控制，而非直接远程化本地 B-tree。
  - 内存解耦、远端索引、Tree Index、RDMA、并发访问

- [ParallelEVM: Operation-Level Concurrent Transaction Execution for EVM-Compatible Blockchains](https://doi.org/10.1145/3689031.3696063)
  - Zhejiang University；Haoran Lin、Hang Feng、Yajin Zhou、Lei Wu
  - ParallelEVM 把 EVM transaction 拆到 operation 粒度并发执行；SSA operation log 记录读写依赖，redo phase 只识别和重跑真正冲突的操作，而非回滚整笔交易。
  - 相较 transaction-level OCC，核心创新是可精确追踪依赖的 SSA 日志与 operation-level selective redo。
  - 区块链、EVM、并发事务、SSA 日志、冲突重执行

- [Understanding and Detecting SQL Function Bugs: Using Simple Boundary Arguments to Trigger Hundreds of DBMS Bugs](https://doi.org/10.1145/3689031.3696064)
  - Tsinghua University、National University of Defense Technology；Jingzhou Fu、Jie Liang、Zhiyong Wu、Yanyang Zhao、Shanshan Li、Yu Jiang
  - Soft 从 318 个 SQL built-in function bug 归纳 boundary argument 模式，用类型边界、极值和异常组合系统测试 7 个 DBMS，确认 132 个未知 bug。
  - 相较随机 SQL 生成，核心创新是把函数边界条件变成高命中率、跨 DBMS 的测试空间。
  - DBMS 测试、SQL Function、Boundary Value、Fuzzing、Bug Study

- [Achieving Fairness Generalizability for Learning-based Congestion Control with Jury](https://doi.org/10.1145/3689031.3696065)
  - University of Science and Technology of China、Hong Kong University of Science and Technology、BitIntelligence、The Hong Kong University of Science and Technology；Han Tian、Xudong Liao、Decang Sun、Chaoliang Zeng、Yilun Jin、Junxue Zhang 等
  - Jury 训练 learning-based congestion control 时显式优化多流公平性的收敛速度和稳定性，并在模拟与真实、未见过的网络条件中保持吞吐与延迟。
  - 相较只在固定训练拓扑追求 reward，核心创新是把 fairness generalization 与 convergence property 纳入 DRL 目标。
  - Learning-based CC、公平性、DRL、泛化、网络传输

- [FastIOV: Fast Startup of Passthrough Network I/O Virtualization for Secure Containers](https://doi.org/10.1145/3689031.3696066)
  - Shanghai Jiao Tong University & Alibaba Cloud、Alibaba Cloud、Shanghai Jiao Tong University、Zhejiang University & Alibaba Cloud、Hangzhou Feitian Cloud & Alibaba Cloud；Yunzhuo Liu、Junchen Guo、Bo Jiang、Yang Song、Pengyu Zhang、Rong Wen 等
  - FastIOV 缩短 secure container 启用 SR-IOV passthrough 的启动路径，通过锁分解、跳过无用 mapping、zeroing 解耦和 VF driver 异步初始化降低 96.1% 开销。
  - 核心创新是逐项拆解 VF provisioning critical path，而非牺牲 passthrough 性能改用软件虚拟网络。
  - 安全容器、SR-IOV、Fast Startup、VF 初始化、I/O 虚拟化

- [Flex: Fast, Accurate DNN Inference on Low-Cost Edges Using Heterogeneous Accelerator Execution](https://doi.org/10.1145/3689031.3696067)
  - University of Virginia、Georgia Tech；Tanmoy Sen、Haiying Shen、Anand Iyer
  - Flex 在低成本 edge 上把 DNN layer 动态分给 CPU 和 accelerator；轻量 heuristic 先缩小可行划分，RL 再依据层代价和设备状态选择执行位置。
  - 相较整模型绑定单一设备，核心创新是运行时 layer-level heterogeneous execution，同时约束 accuracy 与 latency。
  - 边缘推理、异构加速器、Layer Placement、强化学习、低成本设备

- [Hey Hey, My My, Skewness Is Here to Stay: Challenges and Opportunities in Cloud Block Store Traffic](https://doi.org/10.1145/3689031.3696068)
  - Shanghai Jiao Tong University、Alibaba Group；Haonan Wu、Erci Xu、Ligang Wang、Yuandong Hong、Changsheng Niu、Bo Shi 等
  - 该实证研究分析 EBS stack 中请求、tenant、volume 等多层 skew，定位 I/O virtualization、throttle、storage-cluster management 与 cache 四类典型症状。
  - 核心贡献是用生产统计证明偏斜会跨层传递并归纳可操作的系统机会，而非提出单一调度器。
  - 云块存储、流量偏斜、生产测量、缓存、I/O Throttling

- [Multi-Grained Specifications for Distributed System Model Checking and Verification](https://doi.org/10.1145/3689031.3696069)
  - Nanjing University、University of Illinois Urbana-Champaign；Lingzhi Ouyang、Xudong Sun、Ruize Tang、Yu Huang、Madhav Jivrajani、Xiaoxing Ma 等
  - 该工作为 ZooKeeper 建立从粗协议到细实现行为的 multi-grained TLA+ specification，用 TLC 检查 correctness，并允许软件局部演化时只精化受影响模块。
  - 相较单一粒度规格，核心创新是以多层模型控制 model-code gap 与状态空间之间的取舍。
  - 分布式验证、TLA+、ZooKeeper、Multi-grained Spec、Model Checking

- [Improving GPU Sharing Performance through Adaptive Bubbleless Spatial-Temporal Sharing](https://doi.org/10.1145/3689031.3696070)
  - Shanghai Jiao Tong University、Microsoft、Alibaba Group；Shulai Zhang、Quan Chen、Weihao Cui、Han Zhao、Chunyu Xue、Zhen Zheng 等
  - Bless 在多用户 GPU 上联合空间配额与时间切片，动态微调 SM/resource allocation 来填平执行 bubble，同时严格保证每个 tenant 的 quota 和延迟公平性。
  - 相较固定 spatial partition 或独立 time sharing，核心创新是 bubbleless spatial-temporal co-scheduling。
  - GPU Sharing、空间—时间调度、Quota、干扰隔离、多租户

- [A House United Within Itself: SLO-Awareness for On-Premises Containerized ML Inference Clusters via Faro](https://doi.org/10.1145/3689031.3696071)
  - University of Illinois Urbana-Champaign、IBM Research；Beomyeol Jeon、Chen Wang、Diana Arroyo、Alaa Youssef、Indranil Gupta
  - Faro 为 on-prem ML inference cluster 联合 replica scaling、placement 与 batching，并用可控的近似算法快速响应 workload；相比既有系统 SLO violation 降低 2.3–23 倍。
  - 核心创新是系统性地让多个优化组件“sloppy but fast”，以少量解质量换取在线适应速度。
  - 推理集群、SLO、Autoscaling、近似优化、On-premises

- [Fast State Restoration in LLM Serving with HCache](https://doi.org/10.1145/3689031.3696072)
  - Tsinghua University；Shiwei Gao、Youmin Chen、Jiwu Shu
  - HCache 恢复被换出/迁移的 LLM serving state 时，不总从 token 或 KV 全量读回，而从选定 intermediate activation 继续计算，在 compute 与 I/O 间选低成本恢复路径。
  - 相较纯 recompute 或纯 KV reload，核心创新是以中间激活作为第三种恢复点，联合利用算力和存储带宽。
  - LLM Serving、KV/状态恢复、Intermediate Activation、计算—I/O 权衡、迁移

- [Serverless Cold Starts and Where to Find Them](https://doi.org/10.1145/3689031.3696073)
  - Huawei、Huawei, University of St Andrews；Artjom Joosen、Ahmed Hassan、Martin Asenov、Rajkarn Singh、Luke Darlow、Jianfeng Wang 等
  - 该工作分析华为 Serverless 平台一个月 850 亿请求和 1190 万次 cold start，区分发生数量、持续时间与根因，说明冷启动来自多种平台/函数生命周期交互。
  - 核心贡献是用超大规模生产 trace 拆解 cold start 的多维来源，纠正只看平均启动时间的简化模型。
  - Serverless、Cold Start、生产 Trace、FaaS、工作负载刻画

- [Multiplexing Dynamic Deep Learning Workloads with SLO-awareness in GPU Clusters](https://doi.org/10.1145/3689031.3696074)
  - University of Macau; Shenzhen Institute of Advanced Technology, Chinese Academy of Sciences、Shenzhen Institute of Advanced Technology, Chinese Academy of Sciences; University of Chinese Academy of Sciences; University of Macau、University of Macau, Macau SAR, China、Shenzhen Institute of Advanced Technology, Chinese Academy of Sciences、University of Macau；Wenyan Chen、Chengzhi Lu、Huanle Xu、Kejiang Ye、ChengZhong Xu
  - Mudi 在 GPU cluster 中空间共享 inference service 与 training job，并根据服务 SLO 动态调 batch、资源份额和扩缩，使训练填充推理空闲但不破坏 tail latency。
  - 相较推理/训练分池或固定 MPS 配额，核心创新是 SLO-aware multiplexing 与快速联合 adaptation。
  - GPU 集群、训练推理共置、SLO、Adaptive Batching、资源伸缩

- [HybridFlow: A Flexible and Efficient RLHF Framework](https://doi.org/10.1145/3689031.3696075)
  - The University of Hong Kong、ByteDance；Guangming Sheng、Chi Zhang、Zilingfeng Ye、Xibin Wu、Wang Zhang、Ru Zhang 等
  - HybridFlow 用 hybrid controller 表示 RLHF 的 rollout、reward、actor/critic training 数据流；3D-HybridEngine 在 generation 与 training 阶段间快速 reshard actor model。
  - 相较单 controller 难扩展、多 controller 难全局优化，核心创新是混合控制流与跨阶段 3D 并行状态转换。
  - RLHF、分布式训练、Hybrid Controller、Model Resharding、Actor Rollout

- [Collaborative Text Editing with Eg-walker: Better, Faster, Smaller](https://doi.org/10.1145/3689031.3696076)
  - Independent、University of Cambridge；Joseph Gentle、Martin Kleppmann
  - Eg-walker 让多端离线编辑的 operation 在合并时按因果图行走，避免典型 text CRDT 的 tombstone/metadata 膨胀，同时性能接近中心化算法。
  - 相较长期保存逐字符 CRDT 状态，核心创新是以可压缩操作历史恢复并发位置语义。
  - 协同编辑、CRDT、P2P、因果历史、文本数据结构

- [Phantom: Virtualizing Switch Register Resources for Accurate Sketch-based Network Measurement](https://doi.org/10.1145/3689031.3696077)
  - Zhejiang University、The University of Hong Kong、Fuzhou University、Yangzhou University and Southeast University、Nanyang Technological University；Xiang Chen、Hongyan Liu、Zhengyan Zhou、Xi Sun、Wenbin Zhang、Hongyang Du 等
  - Phantom 在 programmable switch 上虚拟化 register，让多个 sketch 共享有限 on-chip state；它按访问和误差需求映射约百万逻辑寄存器，在 Tbps 流量下把测量精度提高最多 86%。
  - 相较每个 sketch 静态独占物理 register，核心创新是面向近似测量语义的寄存器虚拟内存层。
  - 可编程交换机、Sketch、寄存器虚拟化、网络测量、片上内存

- [JABAS: Joint Adaptive Batching and Automatic Scaling for DNN Training on Heterogeneous GPUs](https://doi.org/10.1145/3689031.3696078)
  - UNIST、Samsung SDS；Gyeongchan Yun、Junesoo Kang、Hyunjoon Jeong、Sanghyeon Eom、Minsung Jang、Young-ri Choi
  - JABAS 在异构 GPU training 中联合改变每设备 batch size 与集群规模，保持全局优化等价并按价格/速度扩缩；平均训练时间短 33.3%、成本低 54.2%。
  - 相较只调 batch 或只弹性扩缩，核心创新是把 adaptive batching 与 autoscaling 放进同一收敛约束下。
  - 异构训练、Adaptive Batching、Autoscaling、成本优化、GPU 集群

- [RoboRebound: Multi-Robot System Defense with Bounded-Time Interaction](https://doi.org/10.1145/3689031.3696079)
  - University of Pennsylvania；Neeraj Gandhi、Yifan Cai、Andreas Haeberlen、Linh Thi Xuan Phan
  - RoboRebound 保护 multi-robot system，将机器人交互限制为 bounded-time protocol，即使部分节点异常也在期限内恢复协调，面向跟踪、仓储和探索任务。
  - 相较无界等待邻居或完全隔离故障机器人，核心创新是把防御与实时交互上界共同建模。
  - 多机器人系统、容错、Bounded-time Interaction、Cyber-physical、实时系统

- [Cheetah: Metadata Aggregation for Fast Object Storage without Distributed Ordering](https://doi.org/10.1145/3689031.3696080)
  - SJTU & XMU、KylinSoft、SJTU、NICE XLAB、Huawei Theory Lab；Yiming Zhang、Li Wang、Shengyun Liu、Shun Gai、Haonan Wang、Xin Yao 等
  - Cheetah 将 object store 分成 rich metadata server 与 raw data server，聚合多对象操作所需元数据但不建立全局 distributed order，从而缩短 small-object path。
  - 相较依赖强排序 metadata service，核心创新是用聚合元数据局部完成操作，避免全局协调。
  - 对象存储、Metadata Aggregation、无全局排序、分布式存储、低延迟

- [SuperFE: A Scalable and Flexible Feature Extractor for ML-based Traffic Analysis Applications](https://doi.org/10.1145/3689031.3696081)
  - Beihang University、Tsinghua University；Menghao Zhang、Guanyu Li、Cheng Guo、Renyu Yang、Shicheng Wang、Han Bao 等
  - SuperFE 在高速数据平面统一提取 ML traffic-analysis 所需 flow/packet feature，为多个模型共享 parsing 与 state；multi-100Gbps 下保持检测精度、吞吐比软件高近两个数量级。
  - 相较每个分析应用重复抓包和提特征，核心创新是可编程、可共享的高速 feature-extraction substrate。
  - 网络流量分析、Feature Extraction、ML Data Plane、100Gbps、共享预处理

- [Themis: Finding Imbalance Failures in Distributed File Systems via a Load Variance Model](https://doi.org/10.1145/3689031.3696082)
  - Tsinghua University、Harbin Institute of Technology；Yuanliang Chen、Fuchen Ma、Yuanhang Zhou、Zhen Yan、Qing Liao、Yu Jiang
  - Themis 从四个 DFS 的真实 imbalance failure 建 load-variance model，系统注入会触发负载偏斜的操作/故障并以 variance 作为 oracle，发现 10 个新问题。
  - 相较等待 crash 或 invariant violation，核心创新是把持续负载不均本身形式化为 failure oracle。
  - 分布式文件系统、负载不均、故障测试、Variance Model、性能 Bug

- [Pegasus: Transparent and Unified Kernel-Bypass Networking for Fast Local and Remote Communication](https://doi.org/10.1145/3689031.3696083)
  - Purdue University、Intel Labs；Dinglan Peng、Congyu Liu、Tapti Palit、Anjo Vahldiek-Oberwagner、Mona Vij、Pedro Fonseca
  - Pegasus 为未修改 binary 提供本地和远端统一 kernel-bypass communication，在 userspace 实现 scheduling、memory 等必要 OS service，使 IPC 与网络都绕开 kernel critical path。
  - 相较只支持改写应用或只优化远端网络，核心创新是同一透明 userspace substrate 覆盖 local/remote communication。
  - Kernel Bypass、用户态网络、IPC、未修改应用、OS Runtime

- [Introspective Congestion Control for Consistent High Performance](https://doi.org/10.1145/3689031.3696084)
  - School of Computer Science and Engineering, Central South University、Department of Computer Science and Technology, Tsinghua University；Wanchun Jiang、Haoyang Li、Jia Wu、Kai Wang、Fengyuan Ren、Jianxin Wang
  - Introspective CC 不直接相信从少量信号推断的 path condition，而把候选状态投影回可观测约束，发现错误判断后调整控制动作，因此在变化网络中保持一致性能。
  - 相较固定分类网络状态再选策略，核心创新是让 congestion controller 检查自身推断是否与观测相容。
  - 拥塞控制、自省控制、Path Inference、鲁棒性、在线反馈

- [CAPSys: Contention-aware task placement for data stream processing](https://doi.org/10.1145/3689031.3696085)
  - Boston University；Yuanli Wang、Lei Huang、Zikun Wang、Vasiliki Kalavri、Ibrahim Matta
  - CAPSys 联合 stream-processor autoscaling 与 operator placement；CAPS 搜索把 compute/I/O/network-intensive task 均衡到节点，避免扩容后因资源争用反而变慢。
  - 相较先扩实例再独立放置，核心创新是 contention-aware joint scaling and placement。
  - 流处理、Autoscaling、Task Placement、资源争用、Dataflow

- [Stateful Large Language Model Serving with Pensieve](https://doi.org/10.1145/3689031.3696086)
  - New York University；Lingfan Yu、Jinkun Lin、Jinyang Li
  - Pensieve 跨多轮请求保留 conversation state，缓存已处理历史的 KV/中间状态，scheduler 按会话复用与显存压力组织 batch，避免每轮重新 prefill；吞吐较 vLLM/TensorRT-LLM 高 1.14–3 倍。
  - 相较把每次请求视为无状态 prompt，核心创新是让 serving runtime 以 conversation 为一等调度/缓存对象。
  - LLM Serving、会话状态、KV Cache、Multi-turn、Stateful Batching

- [SpaceFusion: Advanced Deep Learning Operator Fusion via Space-Mapping Graph](https://doi.org/10.1145/3689031.3696087)
  - Shanghai Jiao Tong University；Liang Zhu、Jianguo Yao、Haibing Guan
  - SpaceFusion 用 space-mapping graph 表示 operator fusion 后的 iteration space，spatial/temporal slicer 分解空间并变换依赖，再按硬件资源自动生成 fusion schedule。
  - 相较基于固定 pattern 融合算子，核心创新是可切分的空间表示，使 fusion 与 schedule 可联合自动搜索。
  - DNN 编译、Operator Fusion、Space-Mapping Graph、Auto-scheduling、GPU Kernel

- [FlowCheck: Decoupling Checkpointing and Training of Large-Scale Models](https://doi.org/10.1145/3689031.3696088)
  - Shanghai Jiao Tong University & Alibaba Cloud、Alibaba Cloud & Peking University、Alibaba Cloud、Shanghai Jiao Tong University、Zhejiang University & Alibaba Cloud；Zimeng Huang、Hao Nie、Haonan Jia、Bo Jiang、Junchen Guo、Jianyuan Lu 等
  - FlowCheck 把大模型 checkpoint 写出从 training process 解耦，让训练生成一致 snapshot 后立即继续，后台流水复制/持久化；实际故障率下 effective training time 超过 98%。
  - 相较同步停训保存 checkpoint，核心创新是以一致性边界连接前台训练与异步持久化 pipeline。
  - 大模型训练、Checkpoint、异步 I/O、故障恢复、训练效率

- [BESA: Extending Bugs Triggered by Runtime Testing via Static Analysis](https://doi.org/10.1145/3689031.3696089)
  - Beihang University；Jia-Ju Bai
  - BESA 以 runtime testing 已触发的 null dereference 为种子，静态追踪相似 value-flow/path，扩展到未被测试覆盖的同源 bug，额外发现 57 个问题。
  - 相较运行时测试和全程序静态分析各自独立，核心创新是用真实 failure 约束静态搜索范围与语义。
  - Bug Detection、动态—静态结合、Null Pointer、程序分析、测试扩展

- [RAKIS: Secure Fast I/O Primitives Across Trust Boundaries on Intel SGX](https://doi.org/10.1145/3689031.3696090)
  - Georgia Institute of Technology、Intel Labs；Mansour Alharthi、Fan Sang、Dmitrii Kuvaiskii、Mona Vij、Taesoo Kim
  - RAKIS 让 SGX enclave 安全使用 io_uring 等 Linux fast-I/O primitive，在 trust boundary 校验共享 descriptor/buffer 与完成事件，不改应用且不把复杂 kernel 纳入 TCB。
  - 相较 enclave exit 的同步 I/O 或扩大可信内核，核心创新是面向异步 fast path 的小型验证桥。
  - Intel SGX、Fast I/O、Trust Boundary、Enclave、TCB

- [Towards Efficient Flash Caches with Emerging NVMe Flexible Data Placement SSDs](https://doi.org/10.1145/3689031.3696091)
  - Samsung Electronics；Michael Allison、Arun George、Javier Gonzalez、Dan Helmick、Vikash Kumar、Roshan R Nair 等
  - 该工作把 NVMe Flexible Data Placement 接入 CacheLib，按对象寿命/写入模式把数据放到不同 reclaim unit，降低 flash write amplification、功耗与 embodied carbon，其他性能几乎不受损。
  - 相较由 SSD FTL 完全决定放置，核心创新是 cache software 将数据寿命 hint 传给 FDP 设备。
  - Flash Cache、NVMe FDP、Write Amplification、设备寿命、可持续存储

- [Optimizing Task Scheduling in Cloud VMs with Accurate vCPU Abstraction](https://doi.org/10.1145/3689031.3696092)
  - Hofstra University、The University of Rhode Island、New Jersey Institute of Technology；Edward Guo、Weiwei Jia、Xiaoning Ding、Jianchen Shan
  - vSched 用轻量 vProber 在 guest 内测量 vCPU 的实际 capacity、activity 与 topology，再用 biased selection、intra-VM harvesting 和 relaxed work conservation 调度 task。
  - 相较相信静态 vCPU abstraction，核心创新是无需改 hypervisor 地恢复动态虚拟 CPU 真实能力并反馈给 Linux scheduler。
  - Cloud VM、vCPU、任务调度、微基准探测、虚拟化

- [Efeu: generating efficient, verified, hybrid hardware/software drivers for I2C devices](https://doi.org/10.1145/3689031.3696093)
  - ETH Zurich；Daniel Schwyn、Zikai Liu、Timothy Roscoe
  - Efeu 从 I2C device spec 生成可验证的 hybrid hardware/software driver，并在 throughput、CPU 使用与 FPGA footprint 间搜索切分；生成接口还证明软硬件 interoperable。
  - 相较手写 driver 或固定硬件 offload，核心创新是把正确性证明与 HW/SW partition synthesis 联合。
  - 设备驱动、I2C、程序生成、形式化验证、FPGA Offload

- [eNetSTL: Towards an In-kernel Library for High-Performance eBPF-based Network Functions](https://doi.org/10.1145/3689031.3696094)
  - Southeast University、Hong Kong University of Science and Technology、Peking Univeristy；Bin Yang、Dian Shen、Junxue Zhang、Hanlin Yang、Lunqi Zhao、Beilun Wang 等
  - eNetSTL 从 35 个 eBPF network function 提炼共同的高频操作，在 kernel 内提供最小、稳定的 library component，减少每个程序重复实现 map/packet fast path。
  - 相较不断扩充 eBPF helper 或复制模板，核心创新是面向 NF 共性的 in-kernel STL-style library。
  - eBPF、In-kernel Library、Network Function、代码复用、数据平面

- [Understanding the Linux Kernel, Visually](https://doi.org/10.1145/3689031.3696095)
  - Nanjing University；Hanzhi Liu、Yanyan Jiang、Chang Xu
  - Visualinux 把运行中 Linux kernel 的复杂 pointer/object state 映射成可声明的可视化，开发者可查看 scheduler、memory 等结构随事件变化并辅助定位 bug。
  - 相较用 debugger 手工追指针，核心创新是从 kernel type/state 自动生成领域化动态图。
  - Linux 内核、可视化调试、Kernel State、Bug Diagnosis、开发工具

- [DPack: Efficiency-Oriented Privacy Budget Scheduling](https://doi.org/10.1145/3689031.3696096)
  - Columbia University、University of Michigan、University of British Columbia；Pierre Tholoniat、Kelly Kostopoulou、Mosharaf Chowdhury、Asaf Cidon、Roxana Geambasu、Mathias Lécuyer 等
  - DPack 将多个 DP job 对多维 privacy budget 的竞争建模为 privacy knapsack，在不同 user/cohort budget 上选择任务，近似最大化单位隐私消耗的效用。
  - 相较按到达顺序或单一 epsilon 调度，核心创新是多维 DP budget 的近似 knapsack scheduler。
  - 差分隐私、Privacy Budget、任务调度、多维背包、数据分析

- [Pre-Stores: Proactive Software-guided Movement of Data Down the Memory Hierarchy](https://doi.org/10.1145/3689031.3696097)
  - The University of Sydney、Inria and The University of Neuchâtel、University of Sydney；Xiaoxiang Wu、Baptiste Lepers、Willy Zwaenepoel
  - DirtBuster 识别即将被逐出/写回的数据，在 cache pressure 前用 software pre-store 主动向更慢层移动 dirty data，与 prefetch 相反，从而把未来 eviction latency 移出关键路径。
  - 相较只在缺页前预取读数据，核心创新是把写数据下移也变成编译/软件可提示的提前动作。
  - 内存层次、Pre-store、Dirty Data、软件提示、数据迁移

- [CacheBlend: Fast Large Language Model Serving for RAG with Cached Knowledge Fusion](https://doi.org/10.1145/3689031.3696098)
  - Chinese University of Hong Kong (Shenzhen)、University of Chicago、Stanford University、Microsoft Research and University of Chicago；Jiayi Yao、Hanchen Li、Yuhan Liu、Siddhant Ray、Yihua Cheng、Qizheng Zhang 等
  - CacheBlend 为 RAG 拼接的非前缀知识块复用预计算 KV；只重算少量受跨块 attention 影响最大的 token 来融合 cache，允许 KV 放慢速大容量设备而不增加延迟。
  - 相较 prefix-only cache 或全量重算，核心创新是 selective recomputation 修正任意知识块 KV 的上下文偏差。
  - RAG Serving、KV Cache、非前缀复用、Selective Recompute、慢速存储

- [T-MAC: CPU Renaissance via Table Lookup for Low-Bit LLM Deployment on Edge](https://doi.org/10.1145/3689031.3696099)
  - USTC and Microsoft Research、Microsoft Research、UCAS and Microsoft Research、University of Science and Technology of China；Jianyu Wei、Shijie Cao、Ting Cao、Lingxiao Ma、Lei Wang、Yanyong Zhang 等
  - T-MAC 将低比特 weight-quantized LLM 的乘法改写为 CPU-friendly lookup table，围绕 cache/SIMD 组织查表，使无高端 GPU 的 edge CPU 也能高效推理。
  - 相较依赖整数矩阵乘单元，核心创新是用 LUT 直接利用 bit pattern，重塑低比特 CPU kernel。
  - 边缘 LLM、低比特推理、Lookup Table、CPU Kernel、量化

- [Moko: Marrying Python with Big Data Systems](https://doi.org/10.1145/3689031.3696100)
  - Alibaba Group；Ke Meng、Tao He、Sijie Shen、Lei Wang、Wenyuan Yu、Jingren Zhou
  - MOKO 用统一 IR 捕获 Python data/compute flow，再分别生成 Spark、Dask、Torch、GRAPE 可执行代码，让同一 Python 程序跨大数据/图/ML backend 分布式运行。
  - 相较绑定单一 Python framework，核心创新是以 IR 分离语言语义和异构 distributed engine。
  - Python、大数据系统、Compiler IR、跨框架执行、分布式 Runtime

- [Fork: A Dual Congestion Control Loop for Small and Large Flows in Datacenters](https://doi.org/10.1145/3689031.3696101)
  - Tianjin University、Tianjin University & Huaxiahaorui Technology (Tianjin) Co., Ltd.、Peking University；Yuan Liu、Wenxin Li、Yulong Li、Lide Suo、Xuan Gao、Xin Xie 等
  - Fork 为 datacenter small/large flow 使用相互协调的双 congestion-control loop，短流环快速抢占降低 FCT，长流环保持吞吐与稳定；DPDK prototype 对 Homa/Aeolus 显著改善。
  - 相较一种控制律兼顾两类流，核心创新是按 flow scale 分环控制并协调共享 bottleneck。
  - 数据中心网络、拥塞控制、Small Flow、Large Flow、FCT

- [Ladon: High-Performance Multi-BFT Consensus via Dynamic Global Ordering](https://doi.org/10.1145/3689031.3696102)
  - University of British Columbia、Southern University of Science and Technology；Hanzheng Lyu、Shaokang Xie、Jianyu Niu、Chen Feng、Yinqian Zhang、Ivan Beschastnikh
  - Ladon 并行运行多个 BFT instance，允许各实例不同 block rate；block 获得单调 global rank 后可动态合并顺序，不再等待最慢实例。
  - 相较 round-robin Multi-BFT，核心创新是 rate-independent dynamic global ordering。
  - BFT、Multi-instance Consensus、Global Ordering、慢实例、区块链

- [Samoyeds: Accelerating MoE Models with Structured Sparsity Leveraging Sparse Tensor Cores](https://doi.org/10.1145/3689031.3717455)
  - Shanghai Jiao Tong University、Shanghai Enflame Technology Co.Ltd; Shanghai Jiao Tong University；Chenpeng Wu、Qiqi Gu、Heng Shi、Jianguo Yao、Haibing Guan
  - Samoyeds 同时对 MoE activation 与 parameter 施加 structured sparsity，并设计适配不同 sparse tensor core 的布局/kernel，在保留精度下提高执行与硬件可移植性。
  - 相较只稀疏权重或绑定一种加速器，核心创新是双侧结构稀疏与硬件感知 kernel 协同。
  - MoE 推理、Structured Sparsity、Sparse Tensor Core、Activation、GPU

- [BINGO: Radix-based Bias Factorization for Random Walk on Dynamic Graphs](https://doi.org/10.1145/3689031.3717456)
  - Rutgers, The State University of New Jersey、Nanjing University、The University of Texas at Arlington；Pinhuan Wang、Chengying Huan、Zhibin Wang、Chen Tian、Yuede Ji、Hang Liu
  - BINGO 在动态 graph 上做 GPU random walk；radix-based bias factorization 让有偏采样保持 O(1)，group adaptation 压缩状态并支持 streaming update。
  - 相较 alias table 随图更新昂贵，核心创新是可增量维护的 radix factorization。
  - 动态图、Random Walk、GPU、Radix Sampling、流式更新

- [Achilles: Efficient TEE-Assisted BFT Consensus via Rollback Resilient Recovery](https://doi.org/10.1145/3689031.3717457)
  - Southern University of Science and Technology、Southern University of Science and Technology.、University of British Columbia、The University of Sydney、Southern University of Science and Technology (SUSTech)；Jianyu Niu、Guanlong Wu、Shengqi Liu、Xiaoqing Wen、Jiangshan Yu、Yinqian Zhang
  - Achilles 把 TEE rollback prevention 移出 BFT transaction commit critical path；若 enclave 状态回退，节点通过 rollback-resilient recovery 互助恢复可信状态。
  - 相较每次提交同步持久化 monotonic state，核心创新是正常路径乐观执行、故障时用协议恢复 TEE freshness。
  - TEE-assisted BFT、Rollback、Recovery、共识、可信硬件

- [LOFT: A Lock-free and Adaptive Learned Index with High Scalability for Dynamic Workloads](https://doi.org/10.1145/3689031.3717458)
  - Huazhong University of Science and Technology；Yuxuan Mo、Yu Hua
  - LOFT 是 lock-free learned index，动态 workload 下并发查改不因模型 retraining 停顿；self-tuning 根据分布漂移选择重训时机和范围。
  - 相较全局锁或离线重建 learned index，核心创新是 lock-free update 与 adaptive retraining 协同。
  - Learned Index、Lock-free、动态负载、自适应重训、索引结构

- [SkyServe: Serving AI Models across Regions and Clouds with Spot Instances](https://doi.org/10.1145/3689031.3717459)
  - UC Berkeley、ICSI AND UC Berkeley；Ziming Mao、Tian Xia、Zhanghao Wu、Wei-Lin Chiang、Tyler Griggs、Romil Bhardwaj 等
  - SkyServe/SpotHedge 在多 region/cloud 混用 spot 与 on-demand replica，预测抢占风险并保留跨域 hedge，在 availability 约束下平均降成本 43%。
  - 相较单 region spot 或全 on-demand，核心创新是把地理/云故障相关性纳入 replica placement 与 failover。
  - AI 模型 Serving、Spot Instance、多云、多地域、成本—可用性

- [Groot: Graph-Centric Row Reordering with Tree for Sparse Matrix Multiplications on Tensor Cores](https://doi.org/10.1145/3689031.3717460)
  - The Chinese University of Hong Kong、Hong Kong University of Science and Technology；YuAng Chen、Jiadong Xie、Siyi Teng、Wenqi Zeng、Jeffrey Xu Yu
  - Groot 把 sparse graph matrix 的 row 以 tree-guided graph structure 重排，提高 SpMM/SDDMM 在 Tensor Core 上的 tile density，平均加速 1.8/2.0 倍。
  - 相较只按 nnz 数排序，核心创新是利用图结构寻找能共同填满 tensor-core tile 的行组合。
  - Sparse Matrix、Tensor Core、Row Reordering、GNN、GPU

- [Mist: Efficient Distributed Training of Large Language Models via Memory-Parallelism Co-Optimization](https://doi.org/10.1145/3689031.3717461)
  - University of Toronto, CentML, Vector Institute、University of Toronto、CentML、UC Berkeley、Independent Researcher；Zhanda Zhu、Christina Giannoula、Muralidhar Andoorveedu、Qidong Su、Karttikeya Mangalam、Bojian Zheng 等
  - Mist 自动选择大模型训练的 parallelism，并把 checkpointing、offload、recompute 等所有减显存技术与 communication overlap、异构 imbalance 联合优化。
  - 相较先定并行再局部省内存，核心创新是 memory–parallelism co-optimization 的统一搜索。
  - LLM 训练、自动并行、显存优化、通信重叠、异构 GPU

- [Chrono: Meticulous Hotness Measurement and Flexible Page Migration for Memory Tiering](https://doi.org/10.1145/3689031.3717462)
  - Shanghai Jiao Tong University、Intel；Zhenlin Qi、Shengan Zheng、Ying Huang、Yifeng Hui、Bowen Zhang、Linpeng Huang 等
  - Chrono 在 OS 层分别测量不同 memory tier 的 page access frequency，动态识别 cold page 并灵活迁移，平衡 fast-memory 利用率和可用容量。
  - 相较用统一采样阈值，核心创新是 tier-specific precise hotness 与动态 cold identification。
  - Tiered Memory、Page Hotness、页面迁移、OS 内存管理、CXL

- [Enabling Virtual Priority in Data Center Congestion Control](https://doi.org/10.1145/3689031.3717463)
  - Nanjing University、Shanghai Jiao Tong University、City University of Hong Kong、Politecnico Milano & Queen Mary University of London、Unaffiliated；Zhaochen Zhang、Feiyang Xue、Keqiang He、Zhimeng Yin、Gianni Antichi、Jiaqi Gao 等
  - PozoPlus 在没有额外物理优先队列的情况下，为现有 CC 编码 virtual priority，按 job urgency 调整发送/拥塞反应，较 Swift 物理队列基线改善 JCT。
  - 相较依赖 switch priority queue，核心创新是端主机 congestion-control 层模拟优先级。
  - 数据中心拥塞控制、Virtual Priority、Job Completion Time、端主机、QoS

- [Erebor: A Drop-In Sandbox Solution for Private Data Processing in Untrusted Confidential Virtual Machines](https://doi.org/10.1145/3689031.3717464)
  - National University of Singapore、Arizona State University、Intel Labs；Chuqi Zhang、Rahul Priolkar、Yuancheng Jiang、Yuan Xiao、Mona Vij、Zhenkai Liang 等
  - Erebor 在不可信 confidential VM 内用 secure container 处理客户数据，既阻止外部组件访问，也限制 sandbox 经共享内存、软件接口或 covert exit 外泄。
  - 相较默认信任整个 CVM software stack，核心创新是 CVM 内再建立双向受限的 drop-in sandbox。
  - Confidential VM、Sandbox、私有数据处理、Data Exfiltration、隔离

- [SeBS-Flow: Benchmarking Serverless Cloud Function Workflows](https://doi.org/10.1145/3689031.3717465)
  - Karlsruhe Institute of Technology、ETH Zurich；Larissa Schmid、Marcin Copik、Alexandru Calotoiu、Laurin Brandner、Anne Koziolek、Torsten Hoefler
  - SeBS-Flow 提供 platform-agnostic serverless workflow model 与可复现 workload，在不同云上统一测 cold start、data transfer、cost 和 end-to-end latency。
  - 相较只 benchmark 单函数，核心创新是可移植的 workflow-level suite 与长期可比方法。
  - Serverless Benchmark、Workflow、跨云比较、性能评测、FaaS

- [Comprehensive Deadlock Prevention for GPU Collective Communication](https://doi.org/10.1145/3689031.3717466)
  - School of Computer Science, Peking University、OneFlow Inc.、Science and Technology Laboratory of Parallel and Distributed Processing; College of Computer, National University of Defense Technology, Changsha, Hunan province, China、None；LiChen Pan、Juncheng Liu、Yongquan Fu、Jinhui Yuan、Rongkai Zhang、PengZe Li 等
  - DFCCL 在 collective library 底层实现可抢占 collective，即便应用形成循环 collective dependency，也能暂停/让行并打破死锁。
  - 相较要求应用严格保持 collective order，核心创新是通信库级 preemption，覆盖多框架和错误调用。
  - GPU Collective、Deadlock Prevention、Preemption、分布式训练、通信库

- [Hourglass: Enabling Efficient Split Federated Learning with Data Parallelism](https://doi.org/10.1145/3689031.3717467)
  - Huazhong University of Science and Technology、Swinburne University of Technology、University of Adelaide、Deakin University；Qiang He、Kaibin Wang、Zeqian Dong、Liang Yuan、Feifei Chen、Hai Jin 等
  - Hourglass 在 split FL 的 server side 不为每个 client 常驻一份模型，而让 client 分组共享 partition，并在多 GPU 上 data parallel 处理 intermediate feature；避免 swap，收敛最多快 35.2 倍。
  - 相较 client-to-model 一一映射，核心创新是共享 server partition 与按差异分组的数据并行。
  - Split Federated Learning、Data Parallelism、模型共享、多 GPU、收敛

- [DeltaZip: Efficient Serving of Multiple Full-Model-Tuned LLMs](https://doi.org/10.1145/3689031.3717468)
  - ETH Zurich、MIT；Xiaozhe Yao、Qinghao Hu、Ana Klimovic
  - DeltaZip 同时服务多个 full-model-finetuned LLM，把各变体相对 base 的 delta 压缩最多 10 倍，并在请求执行时高效解码/应用，保持模型质量。
  - 相较 LoRA-only serving 或完整复制权重，核心创新是面向 full fine-tune delta 的压缩存储与执行路径。
  - 多模型 LLM Serving、Model Delta、权重压缩、Full Fine-tuning、显存管理

- [MEPipe: Democratizing LLM Training with Memory-Efficient Slice-Level Pipeline Scheduling on Cost-Effective Accelerators](https://doi.org/10.1145/3689031.3717469)
  - Tsinghua University、Zhipu AI；Zhenbo Sun、Shengqi Chen、Yuanwei Wang、Jian Sha、Guanyu Feng、Wenguang Chen
  - MEPipe 在廉价 accelerator 上做 sequence pipeline parallelism，以 slice 为单位安排不同序列片段，降低峰值激活；细粒度 weight-gradient computation 填补 slice 不均衡 idle。
  - 相较 micro-batch 级 pipeline，核心创新是更细 slice schedule 同时控制显存和 bubble。
  - LLM 训练、Pipeline Parallelism、Slice Scheduling、显存效率、低成本加速器

- [Empowering WebAssembly with Thin Kernel Interfaces](https://doi.org/10.1145/3689031.3717470)
  - Carnegie Mellon University、CMU；Arjun Ramesh、Tianshu Huang、Ben Titzer、Anthony Rowe
  - Thin kernel interface 让 WebAssembly module 直接调用受控 userspace syscall，同时保持同进程 sandbox，使 Wasm 可作为 universal binary 承载更接近原生的 OS/virtualization workload。
  - 相较厚 WASI shim 或完整 VM，核心创新是最小直接内核接口与语言 sandbox 共存。
  - WebAssembly、Kernel Interface、Sandbox、Universal Binary、轻量虚拟化

- [PET: Proactive Demotion for Efficient Tiered Memory Management](https://doi.org/10.1145/3689031.3717471)
  - Seoul National University、Samsung Electronics、Inha University；Wanju Doh、Yaebin Moon、Seoyoung Ko、Seunghwan Chung、Kwanhee Kyung、Eojin Lee 等
  - PET 在 fast memory 满前主动 demote 预计变冷的 page，为未来 promotion 预留空间，避免 demand eviction 阻塞关键访问；容量超限时显著减小 Linux slowdown。
  - 相较缺页时被动回收，核心创新是预测性 proactive demotion 与容量水位控制。
  - Tiered Memory、Proactive Demotion、Page Migration、Fast Memory、Linux

- [Empower Vision Applications with LoRA LMM](https://doi.org/10.1145/3689031.3717472)
  - Nanjing University、Institute for AI Industry Research (AIR), Tsinghua University、Tsinghua University；Liang Mi、Weijun Wang、Wenming Tu、Qingfeng He、Kui Kong、Xinyu Fang 等
  - VaLoRA 为视觉应用共享 LMM base，并按请求装载 LoRA adapter，联合管理视觉 encoder、语言模型与 adapter batch，使多种 vision task 延迟降低 20%–89%。
  - 相较把 LoRA LLM serving 直接套到多模态，核心创新是端到端协调视觉与语言模块的共享/切换。
  - 多模态 Serving、LoRA、Vision-Language Model、Adapter、模块共享

- [A Hardware-Software Co-Design for Efficient Secure Containers](https://doi.org/10.1145/3689031.3717473)
  - Shanghai Jiao Tong University；Jiacheng Shi、Yang Yu、Jinyu Gu、Yubin Xia
  - CKI 用 Intel PKS 建立介于 host 与 container 的新 privilege level，让每个 container kernel 隔离运行，并用单级地址转换减少跨权限和内存访问开销。
  - 相较共享 host kernel 或 nested VM，核心创新是硬件 protection key 支撑的 per-container kernel boundary。
  - 安全容器、PKS、Container Kernel、单级地址转换、软硬件协同

- [OHMiner: An Overlap-centric System for Efficient Hypergraph Pattern Mining](https://doi.org/10.1145/3689031.3717474)
  - Huazhong University of Science and Technology、University of Warwick、National University of Singapore、Zhejiang Lab, China、Jilin University；Hao Qi、Kang Luo、Ligang He、Yu Zhang、Minzhi Cai、Jingxin Dai 等
  - OHMiner 将 hypergraph pattern matching 改写为 hyperedge overlap set operation，incremental overlap pruning 逐步验证 candidate，并行 engine 围绕 overlap relation 分工。
  - 相较枚举顶点映射，核心创新是 overlap-centric abstraction 降低同构检查空间。
  - Hypergraph Mining、Pattern Matching、Overlap、并行引擎、图计算

- [Adios to Busy-Waiting for Microsecond-scale Memory Disaggregation](https://doi.org/10.1145/3689031.3717475)
  - KAIST；Wonsup Yoon、Jisu Ok、Sue Moon、Youngjin Kwon
  - Adios 在 remote-memory page fault 时让等待线程 yield、调度其他 runnable work，而不是 busy-wait 网络完成；在微秒级延迟下仍控制切换开销并提高吞吐/延迟。
  - 相较为省调度开销持续轮询，核心创新是为 memory disaggregation 重新设计 yield-based fault path。
  - 内存解耦、Page Fault、Busy-wait、Yield Scheduling、远端内存

- [Towards VM Rescheduling Optimization Through Deep Reinforcement Learning](https://doi.org/10.1145/3689031.3717476)
  - University of California, Merced、University of California, Berkeley、ByteDance、UC Berkeley、Bytedance；Xianzhong Ding、Yunkai Zhang、Binbin Chen、Donghao Ying、Tieying Zhang、Jianjun Chen 等
  - VMR2L 用两阶段 DRL 先产生满足 placement/migration constraint 的 VM reschedule，再优化 latency/cost；关系特征表示主机—VM，risk-seeking evaluation 允许调节求解速度与质量。
  - 相较通用 RL 直接输出巨大组合动作，核心创新是 constraint-aware two-stage action space。
  - VM Rescheduling、Deep RL、资源放置、约束优化、云管理

- [HawkSet: Automatic, Application-Agnostic, and Efficient Concurrent PM Bug Detection](https://doi.org/10.1145/3689031.3717477)
  - INESC-ID, IST、INESC-ID & IST U. Lisboa、IST Lisbon；João Oliveira、João Gonçalves、Miguel Matos
  - HawkSet 无需应用规格地探索 persistent-memory 并发 interleaving，聚焦会破坏 persist order 的关键 event set，最高加速 159 倍并触达罕见 bug。
  - 相较枚举所有线程/flush 顺序，核心创新是 application-agnostic 的持久化相关事件约简。
  - Persistent Memory、并发 Bug、Crash Consistency、Interleaving、测试

- [Solid State Drive Targeted Memory-Efficient Indexing for Universal I/O Patterns and Fragmentation Degrees](https://doi.org/10.1145/3689031.3717478)
  - POSTECH、DGIST、Virginia Tech；Junsu Im、Jeonggyun Kim、Seonggyun Oh、Jinhyung Koo、Juhyung Park、Hoon Sung Chwa 等
  - AppL 为 SSD index 组合 memory-efficient approximate structure 与 append-only sorted LSM，不依赖 workload locality 或 fragmentation 程度仍能限制 DRAM metadata。
  - 相较为特定 I/O pattern 选择精确索引，核心创新是近似定位+LSM 精确收敛的通用两级结构。
  - SSD、内存高效索引、Approximate Index、LSM Tree、碎片化

- [Byte vSwitch: A High-Performance Virtual Switch for Cloud Networking](https://doi.org/10.1145/3689031.3717479)
  - ByteDance Inc.；Xin Wang、Deguo Li、Zhihong Wang、Lidong Jiang、Shubo Wen、Daxiang Kang 等
  - Byte vSwitch 总结生产 BVS 的设计部署，以更短 packet path、batch 与多核队列管理服务云网络；较 OVS 最高 PPS 3.3 倍、延迟低 25%。
  - 相较研究 prototype，核心贡献是生产级 virtual switch 的端到端数据路径和运维经验。
  - Virtual Switch、云网络、生产系统、Packet Processing、OVS

- [TUNA: Tuning Unstable and Noisy Cloud Applications](https://doi.org/10.1145/3689031.3717480)
  - University of Wisconsin - Madison、University of Wisconsin-Madison、Microsoft；Johannes Freischuetz、Konstantinos Kanellis、Brian Kroth、Shivaram Venkataraman
  - TUNA 在 noisy cloud 上做 autotuning，先检测并剔除 outlier configuration/measurement，再用 ML 恢复更稳定的 true performance signal 交给 optimizer。
  - 相较直接增加重复实验，核心创新是把配置异常与测量噪声显式建模、去噪后再搜索。
  - Autotuning、云噪声、Outlier Detection、性能建模、实验优化

- [SpInfer: Leveraging Low-Level Sparsity for Efficient Large Language Model Inference on GPUs](https://doi.org/10.1145/3689031.3717481)
  - Data Science and Analytics Thrust, HKUST(GZ)、Harbin Institute of Technology (Shenzhen)、Hong Kong University of Science and Technology；Ruibo FAN、Xiangrui YU、Peijie Dong、Zeyu Li、Gu Gong、QIANG WANG 等
  - SpInfer 为 sparse LLM GPU inference 设计 Tensor-Core-Aware Bitmap Encoding，压低稀疏索引/解码成本，并让稀疏 weight tile 对齐 Tensor Core 执行。
  - 相较通用 CSR/结构稀疏格式，核心创新是把 bitmap metadata 与 tensor-core tile 共同设计。
  - 稀疏 LLM 推理、GPU、Tensor Core、Bitmap Encoding、Kernel

- [Daredevil: Rescue Your Flash Storage from Inflexible Kernel Storage Stack](https://doi.org/10.1145/3689031.3717482)
  - The University of Hong Kong、Microsoft Research、Peking University；Junzhe Li、Ran Shu、Jiayi Lin、Qingyu Zhang、Ziyue Yang、Jie Zhang 等
  - Daredevil 解耦 CPU core 与 NVMe submission queue 的静态绑定，建立全连接 routing，并在 queue 上做 multi-tenant-aware scheduling。
  - 相较 Linux block stack 的固定 core–queue mapping，核心创新是动态请求路由与设备队列共享。
  - NVMe、Kernel Storage Stack、Queue Mapping、多租户、I/O Scheduling

- [Eva: Cost-Efficient Cloud-Based Cluster Scheduling](https://doi.org/10.1145/3689031.3717483)
  - University of Wisconsin-Madison；Tzu-Tao Chang、Shivaram Venkataraman
  - Eva 调度 long-running batch task 到不同云实例，依据价格和执行依赖共享/回收 VM，在 JCT 仅增 15% 时总成本降 42%。
  - 相较每 task 独占实例，核心创新是面向云计费与任务生命周期的 cost-aware consolidation。
  - 云集群调度、Batch Job、成本优化、Instance Sharing、JCT

- [HyperAlloc: Efficient VM Memory De/Inflation via Hypervisor-Shared Page-Frame Allocators](https://doi.org/10.1145/3689031.3717484)
  - Leibniz Universität Hannover、Technische Universität Braunschweig；Lars Wrenger、Kenny Albes、Marco Wurps、Christian Dietrich、Daniel Lohmann
  - HyperAlloc 让 hypervisor 直接访问 guest page-frame allocator，在不逐页握手的情况下批量 de/inflate VM memory；收缩速度较 virtio-balloon 快 362 倍。
  - 相较 balloon driver 与 host/guest 消息协议，核心创新是共享 allocator state 形成快速安全回收路径。
  - VM 内存、Ballooning、Hypervisor、Page Allocator、弹性内存

- [Impeller: Stream Processing on Shared Logs](https://doi.org/10.1145/3689031.3717485)
  - Lepton AI、Google、University of Texas at Austin、UT Austin；Zhiting Zhu、Zhipeng Jia、Newton Ni、Dixin Tang、Emmett Witchel
  - Impeller 在 distributed shared log 上做 stream processing，以 string tag progress marker 和 selective read 精确追踪已处理范围，实现 exactly-once 而无需外部 checkpoint store。
  - 相较每 operator 独立日志/事务，核心创新是复用 shared-log order 与轻量进度协议统一状态。
  - 流处理、Shared Log、Exactly-once、Progress Marking、分布式系统

- [Marlin: Enabling High-Throughput Congestion Control Testing in Large-Scale Networks](https://doi.org/10.1145/3689031.3717486)
  - Nanjing University、Shanghai Jiao Tong University；Yanqing Chen、Li Wang、Jingzhi Wang、Songyue Liu、Keqiang He、Jian Wang 等
  - Marlin 用低可编程但超高吞吐设备放大由高可编程流量发生器产生的 pattern，从而在大网络中以线速、复杂 workload 测 congestion control。
  - 相较单一 tester 在吞吐与可编程性间取舍，核心创新是两类硬件协同的 traffic amplification。
  - 网络测试、Congestion Control、Traffic Generator、硬件协同、规模化评测

- [Seal: Towards Diverse Specification Inference for Linux Interfaces from Security Patches](https://doi.org/10.1145/3689031.3717487)
  - The Hong Kong University of Science and Technology、HKUST；Wei Chen、Bowen Zhang、Chengpeng Wang、Wensheng Tang、Charles Zhang
  - Seal 从 Linux security patch 提取 interface 交互的 value-flow property，既学习单接口输入约束，也学习多接口调用间的关系，用于后续检测类似漏洞。
  - 相较人工写 syscall spec 或只挖 patch pattern，核心创新是把安全修复自动转成多样接口规格。
  - Linux Interface、Specification Inference、安全补丁、Value Flow、程序分析

- [Overcoming the Last Mile between Log-Structured File Systems and Persistent Memory via Scatter Logging](https://doi.org/10.1145/3689031.3717488)
  - Harbin Institute of Technology, Shenzhen、Harbin institute of Technology, Shenzhen；Yifeng Zhang、Yanqi Pan、Hao Huang、Yuchen Shan、Wen Xia
  - Slot/SlotFS 将 log entry 分散到 PM slot 并按 entry 粒度回收，失效后立即重分配，不必等待 segment cleaning，因此消除传统 LFS 的 GC 搬运。
  - 相较大 segment 顺序日志，核心创新是利用 PM 随机访问把日志管理粒度降到单条记录。
  - Persistent Memory、Log-structured FS、Scatter Logging、垃圾回收、SlotFS

- [NeuStream: Bridging Deep Learning Serving and Stream Processing](https://doi.org/10.1145/3689031.3717489)
  - Peking University、Peking University and Microsoft Research、Microsoft Research；Haochen Yuan、Yuanqing Wang、Wenhao Xie、Yu Cheng、Ziming Miao、Lingxiao Ma 等
  - NeuStream 把 DL serving 表示成 stream-processing graph，global 层分配 module 资源、local 层为每个 module 决定 batch，联合满足端到端 SLO。
  - 相较单模型 request queue，核心创新是两级 scheduler 管理多模块连续数据流。
  - 深度学习 Serving、流处理、Two-level Scheduling、Batching、SLO

- [AlloyStack: A Library Operating System for Serverless Workflow Applications](https://doi.org/10.1145/3689031.3717490)
  - Tianjin University、Tsinghua University；Jianing You、Kang Chen、Laiping Zhao、Yiming Li、Yichi Chen、Yuxuan Du 等
  - AlloyStack 为 serverless workflow 提供 LibOS，OS component 按需加载缩短 cold start，同一 workflow 的 function 共享地址空间直接传数据。
  - 相较每函数独立 container/kernel，核心创新是 workflow-scoped OS 与 address space。
  - Serverless Workflow、Library OS、Cold Start、共享地址空间、函数通信

- [Jupiter: Pushing the Speed and Scalability Limitations for Subgraph Matching on Multi-GPUs](https://doi.org/10.1145/3689031.3717491)
  - Institute of Computing Technology, Chinese Academy of Sciences、Institute of Computing Technology；Zhiheng Lin、Ke Meng、Changjie Xu、Weichen Cao、Guangming Tan
  - Jupiter 在多节点多 GPU 上做大图 subgraph matching，分区并并行扩展 candidate，控制中间结果与跨卡通信；相同内存可处理比既有系统大 10 倍的图。
  - 相较单机 GPU 或 CPU cluster，核心创新是面向 pattern expansion 的多 GPU 内存/通信协同。
  - Subgraph Matching、多 GPU、分布式图计算、Candidate Expansion、可扩展性

- [MetaHG: Enhancing HGNN Systems Leveraging Advanced Metapath Graph Abstraction](https://doi.org/10.1145/3689031.3717492)
  - Huazhong University of Science and Technology、University of New South Wales；Haiheng He、Haifeng Liu、Long Zheng、Yu Huang、Xinyang Shen、Wenkan Huang 等
  - MetaHG 用 compact metapath graph 一次编码所有 metapath instance 的结构，避免为每种语义关系重复构图/存实例，并直接支撑 HGNN inference。
  - 相较逐 metapath 构 semantic graph，核心创新是可共享的高级 MG abstraction。
  - HGNN、Metapath Graph、图存储、推理优化、异构图

- [Garbage Collection Does Not Only Collect Garbage: Piggybacking-Style Defragmentation for Deduplicated Backup Storage](https://doi.org/10.1145/3689031.3717493)
  - Harbin Institute of Technology, Shenzhen、DapuStor、Dell Technologies；Dingbang Liu、Xiangyu Zou、Tao Lu、Philip Shilane、Wen Xia、Wenxuan Huang 等
  - GCCDF 在 deduplicated backup 的正常 garbage collection 中顺带重排仍存活 chunk，消除 fragmentation，不再另做一次全量 defragmentation I/O。
  - 相较 GC 与碎片整理分开，核心创新是 piggyback relocation 复用已经发生的数据搬运。
  - 备份存储、Deduplication、Garbage Collection、Defragmentation、I/O 优化

- [Atlas: Towards Real-Time Verification in Large-Scale Networks via a Native Distributed Architecture](https://doi.org/10.1145/3689031.3717494)
  - State Key Laboratory of Networking and Switching Technology, Beijing University of Post and Telecommunication、Huawei Technologies、State Key Laboratory of Networking and Switching Technology, Beijing University of Posts and Telecommunications；Mingxiao Ma、Yuehan Zhang、Jingyu Wang、Bo He、Chenyang Zhao、Qi Qi 等
  - Atlas 以 native distributed architecture 并行维护/验证大规模网络 data plane state，使拓扑或规则变化后能实时重新检查 reachability 等 property。
  - 相较集中 verifier，核心创新是验证状态与计算原生分区并随网络更新增量协调。
  - 网络验证、Distributed Architecture、Data Plane、实时检查、可扩展性

- [Occamy: A Preemptive Buffer Management for On-chip Shared-memory Switches](https://doi.org/10.1145/3689031.3717495)
  - Xi'an Jiaotong University、Huawei、Central South University、Tsinghua University；Danfeng Shan、Yunguang Li、Jinchao Ma、Zhenxing Zhang、Zeyu Liang、Xinyu Wen 等
  - Occamy 面向 shallow-buffer switch 和突发流量，允许高优先级/新流抢占已分配 shared buffer，快速回收并重分配，避免静态阈值反应过慢。
  - 相较非抢占动态 buffer management，核心创新是 packet buffer 的 preemptive reclamation。
  - 交换机缓存、Preemptive Buffer、Burst Traffic、Shared Memory、数据中心网络

- [Heimdall: Optimizing Storage I/O Admission with Extensive Machine Learning Pipeline](https://doi.org/10.1145/3689031.3717496)
  - University of Chicago and MangoBoost Inc.、Bandung Institute of Technology and University of Chicago、University of Chicago、Bandung Institute of Technology、Florida International University；Daniar H. Kurniawan、Rani Ayu Putri、Peiran Qin、Kahfi S. Zulkifli、Ray A. O. Sinurat、Janki Bhimani 等
  - Heimdall 为 flash storage 做黑盒 I/O admission；period-based label、三阶段去噪、feature engineering 与细调把准确率从 67% 提到 93%，并把推理压到亚微秒、28KB。
  - 相较通用 ML classifier，核心创新是端到端 domain-specific ML pipeline 与可进 kernel 的部署优化。
  - Flash Storage、I/O Admission、ML for Systems、亚微秒推理、生产 Trace

- [Revealing the Unstable Foundations of eBPF-Based Kernel Extensions](https://doi.org/10.1145/3689031.3717497)
  - University of Wisconsin-Madison、Microsoft Research、UW-Madison、University of Wisconsin–Madison；Shawn Zhong、Jing Liu、Andrea Arpaci-Dusseau、Remzi Arpaci-Dusseau
  - DepSurf 检查 eBPF program 对 kernel type、helper、config 与行为的隐含依赖是否和目标 image 匹配；研究发现 83% 程序受 mismatch 影响。
  - 相较只验证 eBPF bytecode safety，核心创新是系统化建模 extension–kernel compatibility surface。
  - eBPF、Kernel Extension、Dependency Mismatch、兼容性、系统测量

- [CRAVE: Analyzing Cross-Resource Interaction to Improve Energy Efficiency in Systems-on-Chip](https://doi.org/10.1145/3689031.3717498)
  - University of Illinois, Urbana-Champaign、Sandia National Labs、University of Illinois Urbana-Champaign、University of Illinois at Urbana-Champaign；Dipayan Mukherjee、Sam Hachem、Jeremy Bao、Curtis Madsen、Tian Ma、Saugata Ghose 等
  - CRAVE 学习 SoC 各 CPU/GPU/memory resource 的交互和 design characteristic，联合控制 DVFS，而非各部件独立 governor；TX2 上性能升 20%、能耗降 16%。
  - 相较 per-resource DVFS，核心创新是 cross-resource interaction-aware governor。
  - SoC 能效、DVFS、跨资源交互、学习型控制、嵌入式系统
