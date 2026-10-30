# EuroSys 2024 论文列表

EuroSys 2024 正式 proceedings 共收录 71 篇论文。以下标题链接至 ACM DOI 页面；每篇依次列出机构与主要作者、研究场景和系统机制、相较既有方法的核心创新，以及细粒度方向。当前可合法直接获取的 17 份 PDF 已保存到 `reference/EuroSys/2024/`；其余论文依据正式摘要整理，不使用非授权镜像。

- [Automatic Root Cause Analysis via Large Language Models for Cloud Incidents](https://doi.org/10.1145/3627703.3629553)
  - University of Illinois at Urbana-Champaign, Champaign, USA、Peking University, Beijing, China、Microsoft, Beijing, China、Microsoft, Shanghai, China、Microsoft, Suzhou, China；Yinfang Chen、Huaibing Xie、Minghua Ma、Yu Kang、Xin Gao、Liu Shi 等
  - RCACopilot 面向云平台 on-call incident，把告警类型先路由给相应诊断 handler，聚合运行时诊断信息，再让 LLM 预测 root-cause category 并生成带证据的解释文本；它做的是告警到根因报告的自动化链路，而不是让 LLM 直接修改生产系统。
  - 相较只检索相似事故或让 LLM 读取原始日志，核心创新是把告警路由、诊断证据聚合、分类与解释组织成受系统上下文约束的 RCA pipeline。
  - LLM for Systems、云故障诊断、Root Cause Analysis、On-call 自动化、日志与告警

- [Aceso: Efficient Parallel DNN Training through Iterative Bottleneck Alleviation](https://doi.org/10.1145/3627703.3629554)
  - Institute of Computing Technology, CAS、Microsoft Research、University of Science and Technology of China、Shanghai Jiao Tong University；Guodong Liu、Youshan Miao、Zhiqi Lin、Xiaoxiang Shi、Saeed Maleki、Fan Yang 等
  - Aceso 为多 GPU DNN 训练联合选择并行方式、tensor 划分与通信配置，实验/公开实现覆盖 GPT、T5 等 LLM 和 ResNet；但不在巨大的组合空间中一次性搜索；它识别当前计划的主瓶颈，每轮只放宽和重配相关维度，再迭代到更优配置。
  - 相较把搜索空间预先切成若干子空间，核心创新是 bottleneck-by-bottleneck 的增量搜索，能以较低搜索成本到达会被固定子空间遗漏的配置。
  - 分布式训练、自动并行、配置搜索、瓶颈消除、GPU 集群
  - 公开实现与负载配置：[作者代码仓库](https://github.com/MachineLearningSystem/24Eurosys-Aceso/tree/EuroSys24AE)。

- [Puddles: Application-Independent Recovery and Location-Independent Data for Persistent Memory](https://doi.org/10.1145/3627703.3629555)
  - UC San Diego、University of Colorado, Boulder、UCSD；Suyash Mahar、Mingyao Shen、TJ Smith、Joseph Izraelevitz、Steven Swanson
  - Puddles 把持久内存中的数据和恢复元数据组织成 location-independent object，使断电后的 recovery 由系统统一完成，应用无需为每种数据结构编写恢复代码；同一持久数据也可在不同虚拟地址或进程中重新映射。
  - 相较把 crash recovery 逻辑嵌入每个 PM application，核心创新是把恢复与位置独立性变成存储对象自身的系统级属性。
  - Persistent Memory、崩溃恢复、位置无关数据、系统级持久化、应用透明

- [Pronghorn: Effective Checkpoint Orchestration for Serverless Hot-Starts](https://doi.org/10.1145/3627703.3629556)
  - Stanford University、Cornell University、INESC-ID, IST, ULisboa、University of California, Berkeley、Purdue University；Sumer Kohli、Shreyas Kharbanda、Rodrigo Bruno、Joao Carreira、Pedro Fonseca
  - Pronghorn 服务 snapshot-based serverless hot start，持续观察函数执行与初始化状态，决定何时截取 snapshot，并在新 worker 启动时从多个 snapshot 中选择恢复点，避免人工为每个函数固定 checkpoint。
  - 相较只在预设生命周期点拍快照，核心创新是由 orchestrator 基于在线性能自动联合决定 snapshot timing 与 snapshot selection。
  - Serverless、Hot Start、Snapshot Orchestration、Checkpoint、函数启动

- [HD-IOV: SW-HW Co-designed I/O Virtualization with Scalability and Flexibility for Hyper-Density Cloud](https://doi.org/10.1145/3627703.3629557)
  - Shanghai Jiao Tong University、Intel Asia-Pacific R&D Ltd.；Zongpu Zhang、Jiangtao Chen、Banghao Ying、Yahui Cao、Lingyu Liu、Jian Li 等
  - HD-IOV 为高密度云中的网络与 accelerator passthrough 设计软硬件协同 I/O virtualization，在设备侧保留接近 SR-IOV 的 fast path，同时让控制面可扩展地创建更多隔离实例并动态调整资源。
  - 相较 SR-IOV 的固定硬件 VF 数量与软件虚拟化的数据路径开销，核心创新是把性能关键隔离下沉硬件、把灵活管理留给软件。
  - I/O 虚拟化、设备直通、SR-IOV、云多租户、软硬件协同

- [Blaze: Holistic Caching for Iterative Data Processing](https://doi.org/10.1145/3627703.3629558)
  - FriendliAI、Seoul National University、Samsung Research、UNIST、Seoul National University and FriendliAI；Won Wook SONG、Jeongyoon Eo、Taegeon Um、Myeongjae Jeon、Byung-Gon Chun
  - Blaze 面向 iterative data processing，把执行引擎、shuffle/存储等原本分离的 cache 统一管理：对过大 partition 避免反复落盘，对 lineage 很长的数据避免昂贵重算，并在有限内存下联合选择保留对象。
  - 相较每个执行层独立缓存，核心创新是以端到端重算与 I/O 代价进行 holistic caching，消除跨层重复和局部最优。
  - 迭代数据处理、统一缓存、Lineage、重算成本、内存管理

- [Dordis: Efficient Federated Learning with Dropout-Resilient Differential Privacy](https://doi.org/10.1145/3627703.3629559)
  - Hong Kong University of Science and Technology、Nokia Bell Labs；Zhifeng Jiang、Wei Wang、Ruichuan Chen
  - Dordis 在 federated learning 每轮为客户端更新加入 distributed-DP noise，并允许部分采样客户端掉线；add-then-remove 先准备足量噪声，再按实际完成者移除多余部分，使最终聚合精确达到目标隐私噪声而不过度损害精度。
  - 相较按预期参与人数设噪声、遇 dropout 后隐私或效用失控，核心创新是可逆噪声份额协议，在每轮结束时按实际参与集合校准 DP。
  - 联邦学习、Distributed Differential Privacy、客户端掉线、噪声校准、安全聚合

- [Minuet: Accelerating 3D Sparse Convolutions on GPUs](https://doi.org/10.1145/3627703.3629560)
  - University of Toronto / Vector Institute、University of Toronto、Amazon、Meta、Samsung AI Centre Toronto；Jiacheng Yang、Christina Giannoula、Jun Wu、Mostafa Elhoushi、James Gleeson、Gennady Pekhimenko
  - Minuet 加速点云等 3D sparse convolution，针对现代 GPU 重做 coordinate map 构建和稀疏输入到输出的索引映射，减少 Map step 的中间状态与不规则访存，再为后续稀疏计算生成适合 GPU 的任务布局。
  - 相较通用 sparse-convolution engine，核心创新是把 Map 阶段作为首要瓶颈并以 memory-efficient GPU mapping 专门优化。
  - 3D 稀疏卷积、GPU Kernel、点云、索引映射、稀疏 DNN

- [SplitFT: Fault Tolerance for Disaggregated Datacenters via Remote Memory Logging](https://doi.org/10.1145/3627703.3629561)
  - University of Illinois at Urbana-Champaign、University of Illinois Urbana-Champaign and VMware Research；Xuhao Luo、Ramnatthan Alagappan、Aishwarya Ganesan
  - SplitFT 为 disaggregated datacenter 应用把故障恢复日志写入远端内存，使计算节点失败后可从其他节点保存的操作状态恢复；应用获得强持久/一致保证，同时尽量接近可能丢数据的弱保证版本性能。
  - 相较每个应用自建复制协议或同步写慢存储，核心创新是利用低延迟 remote memory logging 提供可复用的故障容忍层。
  - 内存解耦、Remote Memory Logging、容错、POSIX 应用、快速恢复

- [Finding Correctness Bugs in eBPF Verifier with Structured and Sanitized Program](https://doi.org/10.1145/3627703.3629562)
  - Tsinghua University、City University of Hong Kong；Hao Sun、Yiru Xu、Jianzhong Liu、Yuheng Shen、Nan Guan、Yu Jiang
  - 该 eBPF verifier 测试器生成结构化 program，并围绕 verifier 的 accept/reject 结果设计两类 correctness indicator；sanitation 将随机程序规整到能形成可靠 oracle 的状态，从而同时发现错误接受与错误拒绝。
  - 相较以 kernel crash 或执行差异作为模糊 oracle，核心创新是从 verifier 语义中构造可检查的正确性指标，并用程序净化减少无效测试。
  - eBPF Verifier、Fuzzing、Specification Oracle、程序净化、内核安全

- [Accelerating Privacy-Preserving Machine Learning With GeniBatch](https://doi.org/10.1145/3627703.3629563)
  - Hong Kong University of Science and Technology、University of Waterloo、The Hong Kong University of Science and Technology；Xinyang Huang、Junxue Zhang、Xiaodian Cheng、Hong Zhang、Yilun Jin、Shuihai Hu 等
  - GeniBatch 把使用 partially homomorphic encryption 的 PPML program 编译为批处理密文运算：它打包多个标量操作以提高 SIMD 利用，并用 bit-reserving algorithm 控制中间值溢出，在最大化压缩比的同时证明编译前后结果一致。
  - 相较人工选择密文 packing，核心创新是由编译器联合决定 batch layout 与位宽预留，并把结果一致性作为编译约束。
  - 隐私保护机器学习、PHE、批处理编译、密文 Packing、位宽分析

- [Hoda: a High-performance Open vSwitch Dataplane with Multiple Specialized Data Paths](https://doi.org/10.1145/3627703.3629564)
  - Computer Network Information Center, Chinese Academy of Sciences、ByteDance Inc.、Institute of Computing Technology, Chinese Academy of Sciences、Intel Corporation；Heng Pan、Peng He、Zhenyu Li、Pan Zhang、Junjie Wan、Yuhao Zhou 等
  - Hoda 为每个 OpenFlow program 生成专用 parser 与 microflow cache，只解析该规则集真正使用的 header、缓存其常见流；可配置版本把 specialization knob 留在 datapath，兼顾高吞吐与规则变化。
  - 相较所有流共用通用 OVS parser/cache，核心创新是按控制平面程序派生多条专用数据路径，而不是用一条复杂 fast path 处理所有协议。
  - Open vSwitch、可编程数据平面、Parser Specialization、Microflow Cache、云网络

- [Model Selection for Latency-Critical Inference Serving](https://doi.org/10.1145/3627703.3629565)
  - Stanford University；Daniel Mendoza、Francisco Romero、Caroline Trippel
  - RAMSIS 面向 latency-critical inference，联合观察请求 inter-arrival pattern、各候选模型的准确率/延迟与 deadline；在到达间歇的空档把部分请求送往更准确但更慢的模型，而高负载时回退到快速模型。
  - 相较只按当前 queue 或静态阈值选模型，核心创新是把未来到达间隔的时间余量显式纳入 model selection and scheduling policy。
  - 推理服务、模型选择、到达过程、延迟 SLO、准确率—延迟权衡

- [CSAL: the Next-Gen Local Disks for the Cloud](https://doi.org/10.1145/3627703.3629566)
  - Alibaba Group、Solidigm；Yanbo Zhou、Erci Xu、Li Zhang、Kapil Karkra、Mariusz Barczak、Wayne Gao 等
  - CSAL 是阿里云本地盘的两级 SSD 设计：高性能 SSD 吸收细粒度写并作 buffer，大容量 QLC SSD 保存持久数据；系统协调两层映射、刷写和回收，降低 host 与 QLC 内部的双重 write amplification。
  - 相较单一介质 local disk 或简单 SSD cache，核心创新是针对云盘访问粒度共同设计 write buffer 与 QLC persistence data path。
  - 云本地盘、QLC SSD、写缓冲、Write Amplification、分层存储

- [Optimus: Warming Serverless ML Inference via Inter-Function Model Transformation](https://doi.org/10.1145/3627703.3629567)
  - The Hong Kong Polytechnic University、Shantou University、Hong Kong Polytechnic University、Sun Yat-sen University、ETH Zurich；Zicong Hong、Jian Lin、Song Guo、Sifu Luo、Wuhui Chen、Roger Wattenhofer 等
  - Optimus 加速 serverless ML cold/warm start，不把模型视为不可分 blob，而在容器内用 CNN/Transformer meta-operator 把已有 warm model 转换成目标模型；线性复杂度 scheduler 在转换代价、拉取代价和函数到达间选择最低成本路径。
  - 相较为每个函数独立缓存完整模型，核心创新是利用模型算子级相似性做 inter-function transformation，将已有 warm state 复用给另一模型。
  - Serverless ML 推理、模型预热、算子变换、Cold Start、缓存复用

- [Serialization/Deserialization-free State Transfer in Serverless Workflows](https://doi.org/10.1145/3627703.3629568)
  - Shanghai Jiao Tong University、Shanghai Jiao Tong University, Shanghai Artificial Intelligence Laboratory、University of Electronic Science and Technology of China；Fangming Lu、Xingda Wei、Zhuobin Huang、Rong Chen、Mingyu Wu、Haibo Chen
  - RMMap 让未修改的 serverless workflow 在函数间传递状态时直接映射同一远端内存对象，避免语言对象反复 serialization/deserialization；实现同时改造网络、OS 映射、language runtime 与平台生命周期。
  - 相较经对象存储或 RPC 字节流传状态，核心创新是跨函数共享可映射状态表示，并端到端消除序列化路径。
  - Serverless Workflow、状态传输、Remote Memory Mapping、零序列化、跨层协同

- [Enoki: High Velocity Linux Kernel Scheduler Development](https://doi.org/10.1145/3627703.3629569)
  - University of Washington、University of Michigan、Duke University；Samantha Miller、Anirudh Kumar、Tanay Vakharia、Ang Chen、Danyang Zhuo、Thomas Anderson
  - Enoki 允许开发者用 safe Rust 编写 Linux scheduler policy，在 userspace 调试后 live-upgrade 进内核，并提供 application 与 scheduler 的双向通信，缩短策略实验到部署周期。
  - 相较直接修改、重编译和重启 Linux kernel，核心创新是把安全语言、用户态开发体验和内核热替换结合成 scheduler development framework。
  - Linux 调度器、Rust、Live Upgrade、内核扩展、调度策略开发

- [Noctua: Towards Automated and Practical Fine-grained Consistency Analysis](https://doi.org/10.1145/3627703.3629570)
  - University of Science and Technology of China、University of California, Riverside、Nokia Bell Labs、University of Houston、Tsinghua University；Kai Ma、Cheng Li、Enzuo Zhu、Ruichuan Chen、Feng Yan、Kang Chen
  - Noctua 自动分析 Web application 在细粒度数据库 consistency model 下是否满足业务 invariant。SOIR 中间表示把高层语言控制流、数据库读写与 SMT constraint 对齐，使工具能枚举并验证弱一致执行。
  - 相较为每个应用人工建立形式模型，核心创新是用统一 IR 跨越应用代码、数据库交互和 solver 语义，自动恢复并检查 consistency requirement。
  - Web 应用一致性、自动验证、SOIR、SMT、数据库语义

- [Core Graph: Exploiting Edge Centrality to Speedup the Evaluation of Iterative Graph Queries](https://doi.org/10.1145/3627703.3629571)
  - UC Riverside；Xiaolin Jiang、Mahbod Afarin、Zhijia Zhao、Nael Abu-Ghazaleh、Rajiv Gupta
  - Core Graph 为 iterative graph query 找出由高 centrality edge 组成的核心子图，先在小图上得到大多数 vertex 的精确结果，再只对仍不确定的外围 vertex 做补充计算。
  - 相较每轮遍历完整图，核心创新是利用 edge centrality 划分“足以确定多数答案”的核心与按需精化部分。
  - 图查询、Core Graph、Edge Centrality、迭代计算、增量精化

- [CDMPP: A Device-Model Agnostic Framework for Latency Prediction of Tensor Programs](https://doi.org/10.1145/3627703.3629572)
  - The University of Hong Kong、ByteDance Inc.；Hanpeng Hu、Junwei Su、Juntao Zhao、Yanghua Peng、Yibo Zhu、Haibin Lin 等
  - CDMPP 预测 tensor program 在未见模型和未见设备上的 latency；compact AST 保留 loop、memory 和 operator 结构，pre-order positional encoding 表示节点关系，再用跨设备可迁移模型学习执行时间。
  - 相较把算子特征展平或每台设备重新采样训练，核心创新是结构化 compact AST 表示，使同一 predictor 能跨 model 与 device 泛化。
  - Tensor Program、Latency Prediction、跨设备泛化、Compact AST、性能建模

- [Concealing Compression-accelerated I/O for HPC Applications through In Situ Task Scheduling](https://doi.org/10.1145/3627703.3629573)
  - Indiana University、Argonne National Laboratory、INRIA, France、Ecole Normale Supérieure de Lyon, France；Sian Jin、Sheng Di、Frédéric Vivien、Daoce Wang、Yves Robert、Dingwen Tao 等
  - 该工作在 HPC application 运行期间联合调度 compute task、compression task 和 I/O queue，根据数据可压缩性与设备拥塞选择压缩方式和写入队列，使压缩开销被计算重叠、I/O 减量真正转化为端到端收益。
  - 相较先压缩再独立提交 I/O，核心创新是把计算、压缩与 I/O 建成一个 in-situ scheduling problem 联合优化。
  - HPC I/O、数据压缩、In-situ 调度、任务重叠、并行文件系统

- [Unison: A Parallel-Efficient and User-Transparent Network Simulation Kernel](https://doi.org/10.1145/3627703.3629574)
  - Nanjing University、Peking University、Nanjing University of Posts and Telecommunications、Xiamen University；Songyuan Bai、Hao Zheng、Chen Tian、Xiaoliang Wang、Chang Liu、Xin Jin 等
  - Unison 为网络仿真做细粒度 partition，并根据事件负载动态调度 partition，在不要求用户重写模型的情况下并行离散事件执行；24 核上较串行 DES 加速 40 倍、较现有 PDES 加速 10 倍。
  - 相较固定拓扑分区，核心创新是为网络事件依赖设计细粒度切分和 load-adaptive scheduling，同时保持用户透明。
  - 网络仿真、Parallel DES、动态负载均衡、事件调度、可扩展模拟

- [Totoro: A Scalable Federated Learning Engine for the Edge](https://doi.org/10.1145/3627703.3629575)
  - University of California Santa Cruz、Georgia Institute of Technology、Virginia Tech、Louisiana State University、Texas A&M University；Cheng-Wei Ching、Xin Chen、Taehwan Kim、Bo Ji、Qingyang Wang、Dilma Da Silva 等
  - Totoro 让大量 FL job 同时运行在 edge network：locality-aware P2P multi-ring 承载模型更新，publish/subscribe forest 组织多任务传播，bandit path planner 在探索链路与利用稳定路径间选择。
  - 相较每个 FL job 由中心服务器独立聚合，核心创新是共享边缘 P2P overlay，并以任务/拓扑感知路径规划扩展并发 job 数。
  - 边缘联邦学习、P2P Multi-ring、Pub/Sub Forest、Bandit 路径规划、多任务 FL

- [Effective Bug Detection with Unused Definitions](https://doi.org/10.1145/3627703.3629576)
  - UCSD、Meta、Whova、UC San Diego；Li Zhong、Chengcheng Xiang、Haochen Huang、Bingyu Shen、Eric Mugnier、Yuanyuan Zhou
  - ValueCheck 静态分析程序中定义后从未使用的 value，重点检查位于开发者改动/模块交互边界的 unused definition，因为它常意味着遗漏消费、拼写错误或逻辑分支失效；工具据此缩小告警并定位真实 bug。
  - 相较把 unused definition 一律当低价值 lint，核心创新是用 developer-interaction boundary 判断其语义风险。
  - 静态分析、Unused Definition、Bug Detection、代码边界、软件质量

- [Snatch: Online Streaming Analytics at the Network Edge](https://doi.org/10.1145/3627703.3629577)
  - Northwestern University、Boston University；Yunming Xiao、Yibo Zhao、Sen Lin、Aleksandar Kuzmanovic
  - Snatch 把 streaming analytics 推到 network edge，并以 QUIC 在数据产生、边缘处理和用户间建立低延迟传输；分析在数据仍流动时在线执行，避免先汇聚到中心再批处理，常见场景加速 10–30 倍。
  - 相较中心云收集完整流后分析，核心创新是把 QUIC 传输控制与边缘流算子协同，使结果随数据到达渐进产生。
  - 边缘流处理、QUIC、在线分析、低延迟传输、Edge Computing

- [Orion: Interference-aware, Fine-grained GPU Sharing for ML Applications](https://doi.org/10.1145/3627703.3629578)
  - ETH Zurich；Foteini Strati、Xianzhe Ma、Ana Klimovic
  - Orion 透明截获多个 ML client 的 GPU kernel launch，以 kernel 为调度单位估计执行与 interference，再做时空细粒度共享；对 latency-sensitive job 控制排队/干扰，对吞吐 job 填充剩余资源。
  - 相较进程级 time slicing 或固定 MPS 配额，核心创新是无需改应用地在 kernel 粒度感知干扰并联合安排并发与顺序。
  - GPU Sharing、Kernel Scheduling、干扰感知、Tail Latency、多租户 ML

- [Characterization and Reclamation of Frozen Garbage in Managed FaaS Workloads](https://doi.org/10.1145/3627703.3629579)
  - Shanghai Jiao Tong University；Ziming Zhao、Mingyu Wu、Haibo Chen、Binyu Zang
  - Desiccant 面向会 freeze/thaw 的 managed FaaS instance，识别冻结期间 runtime heap 中已经不可达却因 GC 不运行而长期占用的 frozen garbage，并在平台层安全回收，提升同机函数密度。
  - 相较等待实例解冻后由语言 GC 清理，核心创新是 freeze-aware memory manager 跨越 FaaS lifecycle 与 managed runtime 回收窗口。
  - FaaS、Managed Runtime、Frozen Garbage、内存回收、函数密度

- [HAP: SPMD DNN Training on Heterogeneous GPU Clusters with Automated Program Synthesis](https://doi.org/10.1145/3627703.3629580)
  - The University of Hong Kong、Alibaba Group；Shiwei Zhang、Lansong Diao、Chuan Wu、Zongyan Cao、Siyu Wang、Wei Lin
  - HAP 为异构 GPU 集群合成 SPMD 训练程序，联合决定 tensor sharding dimension、不同性能 GPU 的非均匀 shard ratio，以及 tensor exchange 使用的 collective/point-to-point method。
  - 相较假定同构设备和均匀 SPMD partition，核心创新是把非均匀切分与通信程序一起自动合成。
  - 异构 GPU 训练、SPMD、程序合成、Tensor Sharding、通信优化

- [TraceUpscaler: Upscaling Traces to Evaluate Systems at High Load](https://doi.org/10.1145/3627703.3629581)
  - The Pennsylvania State University、Microsoft Research；Sultan Mahmud Sajal、Timothy Zhu、Bhuvan Urgaonkar、Siddhartha Sen
  - TraceUpscaler 在用旧 trace 压测高负载系统时，把 request parameter/data 与 arrival timestamp 解耦，只压缩时间轴并保持 burst、周期和相关性，从而生成更高 QPS trace 而不伪造请求内容分布。
  - 相较简单倍增请求或均匀缩短间隔，核心创新是只变换 arrival process 并显式保持原 trace 的 temporal pattern。
  - 系统评测、Trace Upscaling、到达过程、负载生成、时间模式

- [CCL-BTree: A Crash-Consistent Locality-Aware B+-Tree for Reducing XPBuffer-Induced Write Amplification in Persistent Memory](https://doi.org/10.1145/3627703.3629582)
  - Zhejiang University、Washington State University Vancouver；Zhenxin Li、Shuibing He、Zheng Dang、Peiyi Hong、Xuechen Zhang、Rui Wang 等
  - CCL-BTree 为 persistent memory 保持相邻 leaf 的 key locality 以支持 range query，并让写入先在以 leaf 为中心的 buffer 合并后成批 flush，减少 XPBuffer 导致的小随机持久写；更新顺序同时满足 crash consistency。
  - 相较把通用 B+ tree 直接配外部 write buffer，核心创新是让 leaf layout、buffering 与恢复顺序共同设计。
  - Persistent Memory、B+ Tree、Crash Consistency、写放大、Range Query

- [Blox: A Modular Toolkit for Deep Learning Schedulers](https://doi.org/10.1145/3627703.3629583)
  - University of Wisconsin-Madison、Microsoft Research；Saurabh Agarwal、Amar Phanishayee、Shivaram Venkataraman
  - Blox 把 DL cluster scheduler 拆成 admission、placement、fairness、job state 等可组合 abstraction，重实现多个已有 scheduler 并复现实验结果，使新 policy 可在同一 toolkit 中替换组件、统一比较。
  - 相较每篇调度论文自建 simulator/runtime，核心创新是抽取可复用的 scheduler building block 并验证其对既有系统的 fidelity。
  - 深度学习调度、模块化 Toolkit、集群模拟、策略复现、资源管理

- [Improving GPU Energy Efficiency through an Application-transparent Frequency Scaling Policy with Performance Assurance](https://doi.org/10.1145/3627703.3629584)
  - Peng Cheng Laboratory、Harbin Institute of Technology (Shenzhen)、Sun Yat-sen University；Yijia Zhang、Qiang Wang、Zhe Lin、Pengxiang Xu、Bingqiang Wang
  - GEEPAFS 是 application-transparent GPU DVFS policy，不需要离线 profile 或修改 workload；它在线判断频率降低对当前 kernel 的性能敏感度，在满足 performance assurance 的边界内压频降能耗。
  - 相较基于固定模型或用户标注的 DVFS，核心创新是无需先验 profile 的在线频率控制，同时显式约束性能损失。
  - GPU 能效、DVFS、性能保证、在线控制、应用透明

<a id="dynapipe"></a>

- [DynaPipe: Optimizing Multi-task Training through Dynamic Pipelines](https://doi.org/10.1145/3627703.3629585)
  - The University of Hong Kong、Amazon Web Services、Boson AI；Chenyu Jiang、Zhen Jia、Shuai Zheng、Yida Wang、Chuan Wu
  - DynaPipe 面向 LLM（T5/GPT）的多任务训练，处理 sequence length 的显著差异，用动态规划把样本组成执行时间接近的 micro-batch，再根据实际 batch 时长动态安排 pipeline stage 与通信，减少 padding 和 bubble。
  - 相较固定 micro-batch/pipeline schedule，核心创新是把 batch construction 与运行时 pipeline/communication scheduling 联合适应长度变化。
  - 多任务训练、Pipeline Parallelism、动态 Micro-batching、序列长度、通信调度

- [Exploring the Asynchrony of Slow Memory Filesystem with EasyIO](https://doi.org/10.1145/3627703.3629586)
  - Xiamen University、Tsinghua University；Bohong Zhu、Youmin Chen、Jiwu Shu
  - EasyIO 服务由慢内存支撑的 filesystem，把 copy/move 等数据搬运 offload 到片上 DMA，并把释放的 CPU 周期用于执行细粒度 application task；异步 I/O 完成与任务执行透明交错。
  - 相较 CPU 同步搬运并等待慢内存，核心创新是 DMA offload 后立即回收 CPU 时间，以 task scheduler 隐藏 slow-memory I/O。
  - 慢内存文件系统、DMA Offload、异步 I/O、任务交错、CPU 利用率

- [Atlas: Hybrid Cloud Migration Advisor for Interactive Microservices](https://doi.org/10.1145/3627703.3629587)
  - Georgia Institute of Technology、IBM Research - Almaden；Ka-Ho Chow、Umesh Deshpande、Veera Deenadhayalan、Sangeetha Seshadri、Ling Liu
  - Atlas 为 interactive microservice 规划哪些 service 留在私有云、哪些迁到公有云；学习模型从数百万组合中快速提出方案，并允许用户在端到端 API latency、availability 和 hosting cost 间选择 trade-off。
  - 相较只按单服务资源成本迁移，核心创新是用学习引导的组合搜索处理调用图端到端影响，并返回可定制 Pareto 方案。
  - 混合云迁移、微服务、学习型优化、成本—性能权衡、可用性

- [ScaleCache: A Scalable Page Cache for Multiple Solid-State Drives](https://doi.org/10.1145/3627703.3629588)
  - Chung-Ang University、University of Illinois Urbana-Champaign、DGIST；Kiet Tuan Pham、Seokjoo Cho、Sangjin Lee、Lan Anh Nguyen、Hyeongi Yeo、Ipoom Jeong 等
  - ScaleCache 重做多 SSD 服务器的 Linux page cache：ccXArray 允许 lookup/update 并发，dflush 绕过集中 flush bottleneck，把 dirty page 机会式并行刷到多个设备。
  - 相较为单盘设计、由集中线程串行回写的 page cache，核心创新是同时并行化元数据访问和设备 flush path。
  - Page Cache、多 SSD、并发 XArray、并行回写、Linux 存储

- [Contigra: Graph Mining with Containment Constraints](https://doi.org/10.1145/3627703.3629589)
  - Simon Fraser University；Joanna Che、Kasra Jamshidi、Keval Vora
  - Contigra 处理带 containment constraint 的 graph mining，先把约束转成 exploration task 之间的 dependency，再把相关 task fusion，使它们共享邻接数据和 cache line，而不是重复遍历相同局部图。
  - 相较把 constraint 只当剪枝谓词，核心创新是利用约束诱导的任务相关性重组执行以提高 locality。
  - 图挖掘、Containment Constraint、Task Fusion、Cache Locality、并行探索

- [Wormhole Filters: Caching Your Hash on Persistent Memory](https://doi.org/10.1145/3627703.3629590)
  - State Key Laboratory for Novel Software Technology, Nanjing University, Nanjing 210023, China、Tsinghua University、Huawei Technologies Co., Ltd.；Hancheng Wang、Haipeng Dai、Rong Gu、Youyou Lu、Jiaqi Zheng、Jingsong Dai 等
  - Wormhole Filter 是 persistent-memory approximate membership query structure，通过缓存 hash/metadata 减少 PM random read，并将更新组织成顺序写；更少 log record 同时降低 crash recovery 成本。
  - 相较直接把 DRAM Bloom/Cuckoo filter 持久化，核心创新是围绕 PM 的随机访问和持久日志代价共同设计查询与更新布局。
  - Persistent Memory、AMQ、Wormhole Filter、写优化、恢复日志

- [Transparent Multicore Scaling of Single-Threaded Network Functions](https://doi.org/10.1145/3627703.3629591)
  - EPFL；Lei Yan、Yueyang Pan、Diyu Zhou、George Candea、Sanidhya Kashyap
  - NFOS 让开发者按单线程语义编写 stateful network function，runtime 自动把 flow/state 分配到多核，profiler 找出共享热点并生成扩展策略；串行 NF 可达到接近手工并发 VPP 实现的伸缩性。
  - 相较要求 NF 作者自己加锁、分片和并发调试，核心创新是以编程模型+runtime 透明提取多核并行。
  - Network Function、多核扩展、状态分片、Runtime、可编程网络

- [Draconis: Network-Accelerated Scheduling for Microsecond-Scale Workloads](https://doi.org/10.1145/3627703.3650060)
  - University of Waterloo；Sreeharsha Udayashankar、Ashraf Abdel-Hadi、Ali Mashtizadeh、Samer Al-Kiswany
  - Draconis 把 microsecond-scale task 的排队与分配放入 programmable switch，在网络入口维护可调度状态并直接选 worker，绕过中心 scheduler 的往返和热点，面向大集群降低 tail scheduling latency。
  - 相较认为交换机无法容纳复杂 scheduler data structure，核心创新是设计适合数据平面的状态表示与操作，让 in-network scheduling 可扩展。
  - In-network Scheduling、可编程交换机、微秒任务、Tail Latency、集群调度

- [Exploring Performance and Cost Optimization with ASIC-Based CXL Memory](https://doi.org/10.1145/3627703.3650061)
  - Yale University、ByteDance；Yupeng Tang、Ping Zhou、Wenhui Zhang、Henry Hu、Qirui Yang、Hao Xiang 等
  - 该工作以真实 ASIC-based CXL memory 评测 latency、bandwidth、NUMA/topology 与应用 cost，比较 DRAM 扩容、内存分层等配置，给出何种 workload/容量点值得采用 CXL 的经验边界。
  - 相较只用模拟器或 FPGA prototype，核心贡献是生产级 ASIC CXL 的端到端性能—成本实证与部署规律，而非新调度算法。
  - CXL Memory、实证测量、性能—成本、内存扩容、系统部署

- [Halflife: An Adaptive Flowlet-based Load Balancer with Fading Timeout in DCNs](https://doi.org/10.1145/3627703.3650062)
  - Fudan University、Beijing Institute of Technology, Beijing Institute of Technology Zhengzhou Academy of Intelligent Technology, Zhejiang Lab、Fudan University, Peng Cheng Laboratory；Sen Liu、Yongbo Gao、Zixuan Chen、Jiarui Ye、Haiyang Xu、Furong Liang 等
  - Halflife 为 DCN flowlet load balancing 维护随时间衰减的 flowlet-timeout value，不依赖预知 workload 就能在长间隔时快速换路径、短间隔时避免 packet reordering；作为 CONGA/LetFlow 增强后多类负载提升 30%–200%。
  - 相较固定或慢速自适应 timeout，核心创新是 fading timeout 让路径切换阈值连续反映近期流量节奏。
  - 数据中心网络、Flowlet Load Balancing、Fading Timeout、Packet Reordering、自适应路由

- [WiseGraph: Optimizing GNN with Joint Workload Partition of Graph and Operations](https://doi.org/10.1145/3627703.3650063)
  - Tsinghua University、Microsoft、University of Seoul、North Carolina State University；Kezhao Huang、Jidong Zhai、Liyan Zheng、Haojie Wang、Yuyang Jin、Qihao Zhang 等
  - WiseGraph 用 gTask 同时描述 graph partition 与 GNN operator partition，把数据放置、采样/聚合计算和跨设备通信放入统一搜索空间，既覆盖已有策略，也能生成混合的新划分。
  - 相较先切图再固定切算子，核心创新是联合优化 graph data 与 operation workload partition。
  - GNN 训练、图划分、算子划分、gTask、分布式 GPU

- [Improving Resource and Energy Efficiency for Cloud 3D through Excessive Rendering Reduction](https://doi.org/10.1145/3627703.3650064)
  - University of Texas at San Antonio、University of Arizona、University of Massachusetts Amherst；Tianyi Liu、Jerry Lucas、Sen He、Tongping Liu、Xiaoyin Wang、Wei Wang
  - ODR 面向 cloud 3D/game streaming，识别已经不会被用户看到的 excessive frame rendering；用 multi-buffering、动态延迟/加速渲染和优先处理 input，在保持交互 QoS 下减少 GPU 工作与能耗。
  - 相较简单限制 FPS，核心创新是依据显示与输入时序按需决定是否生成每一帧，而非只降低固定帧率。
  - Cloud 3D、远程渲染、GPU 能效、On-demand Rendering、交互 QoS

- [Polynima - Practical Hybrid Recompilation for Multithreaded Binaries](https://doi.org/10.1145/3627703.3650065)
  - University of California, Irvine；Chinmay Deshpande、Fabian Parzefall、Felicitas Hetzelt、Michael Franz
  - Polynima 对没有源码的 x86/x64 multithreaded binary 做 lifting 和 recompilation；hybrid control-flow recovery 以静态分析覆盖常见路径、动态观测补未知间接跳转，并保留线程同步语义，平均开销约 1.23 倍。
  - 相较纯静态无法覆盖动态路径、纯动态难完整重编译，核心创新是混合恢复控制流并专门处理多线程未知路径。
  - Binary Recompilation、控制流恢复、多线程、x86/x64、程序变换

- [TTLs Matter: Efficient Cache Sizing with TTL-Aware Miss Ratio Curves and Working Set Sizes](https://doi.org/10.1145/3627703.3650066)
  - University of Toronto、Huawei；Sari Sultan、Kia Shakiba、Albert Lee、Paul Chen、Michael Stumm
  - 该工作把 TTL expiration 纳入 miss-ratio curve 与 working-set-size 估计：对象到期相当于在 reuse-distance 之外额外失效，并扩展 HyperLogLog 以统计带寿命对象，帮助 cache operator 正确 sizing。
  - 相较假定对象永久有效的 MRC/WSS，核心创新是把时间到期与容量 eviction 统一进估计模型。
  - Cache Sizing、TTL、Miss Ratio Curve、Working Set、HyperLogLog

- [NeuroFlux: Memory-Efficient CNN Training Using Adaptive Local Learning](https://doi.org/10.1145/3627703.3650067)
  - University of St Andrews；Dhananjay Saikumar、Blesson Varghese
  - NeuroFlux 面向显存受限 CNN training，按 block 使用 local learning 以避免保存全网 activation；adaptive auxiliary network 动态改变 filter 数，block-specific batch size 再把不同阶段剩余显存转为吞吐。
  - 相较固定 local classifier 和统一 batch size，核心创新是按 block 联合调节辅助网络容量与 batch，使显存约束下仍保持训练效率。
  - 内存高效训练、Local Learning、CNN、动态 Batch、边缘 GPU

- [Save the Bruised Striver: A Reliable Live Patching Framework for Protecting Real-World PLCs](https://doi.org/10.1145/3627703.3650068)
  - School of Cyber Science and Engineering, Nanjing University of Science and Technology、Virginia Tech、NARI Group Corporation State Grid Electric Power Research Institute、School of Cyber Security, University of Chinese Academy of Sciences, Institute of Information Engineering, CAS；Ming Zhou、Haining Wang、Ke Li、Hongsong Zhu、Limin Sun
  - RLPatch 为无源码 PLC binary 做 live patch：监控 PLC 实时条件和动态行为，识别会导致不可恢复故障的 vulnerability，再生成/注入 hot patch，尽量不中断控制任务。
  - 相较停机升级或只支持有源码软件，核心创新是把实时状态约束纳入第三方 PLC 二进制补丁生成与安全切换。
  - 工业控制、PLC、Live Patching、Binary Patch、实时可靠性

- [Astraea: Towards Fair and Efficient Learning-based Congestion Control](https://doi.org/10.1145/3627703.3650069)
  - Hong Kong University of Science and Technology；Xudong Liao、Han Tian、Chaoliang Zeng、Xinchen Wan、Kai Chen
  - Astraea 用 multi-agent deep RL 训练彼此竞争的 congestion-control flow，reward 不只优化单流吞吐/延迟，还显式要求多流快速、稳定地收敛到公平份额，因此部署后面对新竞争者也能恢复公平。
  - 相较单 Agent 在固定背景流上训练，核心创新是把交互 policy 与 fairness convergence dynamics 直接放进多 Agent 训练目标。
  - Multi-Agent RL、拥塞控制、公平性、收敛稳定性、网络传输

- [Adaptable Runtime Monitoring for Intermittent Systems](https://doi.org/10.1145/3627703.3650070)
  - Ege University、University of Trento、SINTEF Digital、Eindhoven University of Technology；Eren Yildiz、Khakim Akhunov、Lorenzo Antonio Riva、Arda Goknil、Ivan Kurtev、Kasim Sinan Yildirim
  - ARTEMIS 为掉电后反复重启的 intermittent program 提供 runtime monitoring，可按能源/开销选择要检查的 property 和 instrumentation 强度，并跨 checkpoint 保持 monitor state，发现会因中断时序触发的违规。
  - 相较固定 property、固定开销的监控器，核心创新是让检查策略适应间歇能源与执行阶段。
  - Intermittent Computing、Runtime Monitoring、属性检查、断电恢复、自适应验证

- [SmartNIC Security Isolation in the Cloud with S-NIC](https://doi.org/10.1145/3627703.3650071)
  - Harvard University；Yang Zhou、Mark Wilkening、James Mickens、Minlan Yu
  - S-NIC 在 SmartNIC 上为不同 tenant 的 network function 与 host-side code 建立硬件保证隔离，同时保留 NIC acceleration；威胁模型还包括云 provider，不让其看到或篡改 tenant 数据路径状态。
  - 相较只隔离 host VM 或信任 NIC 管理面，核心创新是把 enclave-like security boundary 扩展到 SmartNIC 与主机协同应用。
  - SmartNIC、安全隔离、云多租户、Network Function、硬件可信边界

- [Trinity: A Fast Compressed Multi-attribute Data Store](https://doi.org/10.1145/3627703.3650072)
  - UC Berkeley、NetApp、Yale University；Ziming Mao、Kiran Srinivasan、Anurag Khandelwal
  - TRINITY 用动态、succinct multi-dimensional structure MdTrie 存储大规模多属性 record；压缩共享前缀/维度结构的同时支持按多个 attribute 过滤和聚合，兼顾空间与查询速度。
  - 相较列式压缩后另建多个 index，核心创新是一个可动态更新的紧凑多维结构同时承担存储和查询索引。
  - 多属性数据存储、Succinct Data Structure、MdTrie、压缩索引、查询处理

- [Dashing and Star: Byzantine Fault Tolerance with Weak Certificates](https://doi.org/10.1145/3627703.3650073)
  - Tsinghua University、Yangtze Delta Region Institute of Tsinghua University, Zhejiang、Shandong University、Beijing Institute of Technology、Digital Currency Institute, the People's Bank of China；Sisi Duan、Haibin Zhang、Xiao Sui、Baohan Huang、Changchun Mu、Gang Di 等
  - Dashing 设计两种使用 weak certificate 的 HotStuff-style BFT，Star 则从 n−f replica 收集并交付 transaction，以不同网络/故障条件在 liveness、通信、state transfer 与扩展性间选择。
  - 相较始终要求强 quorum certificate，核心创新是重新界定较弱 certificate 在各阶段足以保证的安全条件，降低正常路径成本。
  - BFT、Weak Certificate、HotStuff、状态机复制、共识协议

- [GMorph: Accelerating Multi-DNN Inference via Model Fusion](https://doi.org/10.1145/3627703.3650074)
  - University of Massachusetts Amherst、Adobe Research；Qizheng Yang、Tianyi Yang、Mingcan Xiang、Lijun Zhang、Haoliang Wang、Marco Serafini 等
  - GMorph 为同时执行多个 DNN 的服务找出可融合 subgraph/operator，把模型转换成共享执行图并安排 fused batch，在满足每个任务 accuracy target 下减少重复计算；延迟较多任务学习基线改善 1.1–3 倍。
  - 相较重新训练一个 multi-task model，核心创新是部署时对已有独立模型做结构化 model fusion，不改变任务精度。
  - 多 DNN 推理、Model Fusion、共享计算、服务优化、准确率约束

- [MTM: Rethinking Memory Profiling and Migration for Multi-Tiered Large Memory](https://doi.org/10.1145/3627703.3650075)
  - William & Mary、University of California, Merced、SK hynix；Jie Ren、Dong Xu、Junhee Ryu、Kwangsik Shin、Daewoo Kim、Dong Li
  - MTM 管理 DRAM/CXL/PM 等多层大内存：profiling rate 与观测机制联动以控制开销，统一 page migration policy 根据访问收益跨多 tier 移动，并识别 huge page，避免为每对层写独立迁移器。
  - 相较热页采样与两层 promotion/demotion，核心创新是让 profiling quality、开销和多层迁移决策在同一反馈回路中联合控制。
  - Tiered Memory、页面迁移、内存 Profiling、Huge Page、应用透明

- [LSGraph: A Locality-centric High-performance Streaming Graph Engine](https://doi.org/10.1145/3627703.3650076)
  - Huazhong University of Science and Technology、University of Warwick、Zhejiang Lab, China；Hao Qi、Yiyang Wu、Ligang He、Yu Zhang、Kang Luo、Minzhi Cai 等
  - LSGraph 同时服务 streaming graph update 与 analytics，以 locality-centric layout 存放相邻顶点/边；更新时限制数据移动距离并局部重组，避免持续 ingest 破坏分析阶段的 cache locality。
  - 相较写优化 delta store 与只读主图分离，核心创新是让 update mechanism 主动维护后续 graph computation 所需 locality。
  - Streaming Graph、动态图更新、数据局部性、图分析、内存布局

- [SandTable: Scalable Distributed System Model Checking with Specification-Level State Exploration](https://doi.org/10.1145/3627703.3650077)
  - Nanjing University、University of Illinois at Urbana-Champaign；Ruize Tang、Xudong Sun、Yu Huang、Yuyang Wei、Lingzhi Ouyang、Xiaoxing Ma
  - SandTable 不直接枚举分布式实现的巨大 concrete state，而把执行投影到较小 specification state space 搜索，再将候选 counterexample 回放到实现确认，从而减少无意义 interleaving。
  - 相较 implementation-level model checking，核心创新是 specification-level exploration + implementation confirmation 的双层验证。
  - 分布式系统 Model Checking、规格状态空间、Counterexample、可扩展验证、并发错误

- [FLOWS: Balanced MRC Profiling for Heterogeneous Object-Size Cache](https://doi.org/10.1145/3627703.3650078)
  - Huazhong University of Science and Technology,Tencent Inc.、Huazhong University of Science and Technology、University of Texas at Arlington；Xiaojun Guo、Hua Wang、Ke Zhou、Hong Jiang、Yaodong Han、Guangjie Xing
  - FLOWS 为对象大小差异很大的 cache 估计 miss-ratio curve：Cache Filter 平衡被大流量对象支配的 request sample，weighted sampling 再降低按 byte 估计的方差，兼顾 object miss 与 byte miss。
  - 相较均匀请求采样，核心创新是把频率偏斜和对象大小偏斜分别用过滤与加权处理。
  - Cache Profiling、Miss Ratio Curve、异构对象大小、Weighted Sampling、容量规划

- [On the Limitations of Carbon-Aware Temporal and Spatial Workload Shifting in the Cloud](https://doi.org/10.1145/3627703.3650079)
  - University of Massachusetts Amherst、Massachusetts Institute of Technology、University of Massachusetts, Amherst；Thanathorn Sukprasert、Abel Souza、Noman Bashir、David Irwin、Prashant Shenoy
  - 该工作量化 cloud workload 在时间和地域间迁移所能减少的 carbon emission，并考虑电网逐渐变绿、容量/SLO/迁移窗口约束；结果显示相对 carbon-agnostic baseline 的收益会随绿电普及下降，实际上界远低于理想模型。
  - 相较只报告单一 trace 下的减排，核心贡献是推导并实证 carbon-aware shifting 的可达上界与长期递减条件。
  - Carbon-aware Computing、时空负载迁移、云调度、碳强度、局限性分析

- [Validating Database System Isolation Level Implementations with Version Certificate Recovery](https://doi.org/10.1145/3627703.3650080)
  - Imperial College London、National University of Singapore；Jack Clark、Alastair F. Donaldson、John Wickerson、Manuel Rigger
  - Emme 白盒检查数据库 isolation-level 实现，从版本链和读写关系恢复 version certificate，判定一个历史是否可能由目标隔离级别产生；它能发现 Elle 等仅看外部 history 漏掉的异常。
  - 相较纯黑盒 dependency-cycle checker，核心创新是利用内部 version information 重建更强的 isolation certificate。
  - 数据库隔离级别、History Checking、Version Certificate、并发事务、白盒验证

- [FLOAT: Federated Learning Optimizations with Automated Tuning](https://doi.org/10.1145/3627703.3650081)
  - Virginia Tech、Indian Institute of Technology, Guwahati、Queen Mary University of London、University of Minnesota；Ahmad Faraz Khan、Azal Ahmad Khan、Ahmed M. Abdelmoniem、Samuel Fountain、Ali R. Butt、Ali Anwar
  - FLOAT 在有训练 deadline 的 FL 中在线调节参与客户端、local epoch、压缩/聚合等 optimizer，并根据设备速度、straggler 和 dropout 动态切换配置，在资源利用与收敛进度间平衡。
  - 相较固定 FL hyperparameter 或一次性调参，核心创新是 deadline-aware automated tuning 随每轮真实参与状态重新优化。
  - 联邦学习、自动调优、Deadline、Straggler、资源管理

- [DeTA: Minimizing Data Leaks in Federated Learning via Decentralized and Trustworthy Aggregation](https://doi.org/10.1145/3627703.3650082)
  - IBM Research、Amazon Inc.；Pau-Chen Cheng、Kevin Eykholt、Zhongshu Gu、Hani Jamjoom、K. R. Jayaram、Enriquillo Valdez 等
  - DeTA 不让单一中心看到所有 client update，而用 decentralized trusted aggregation 分散聚合权力，并以 defense-in-depth 同时应对聚合结果篡改与模型更新泄漏，在保持训练精度下控制额外开销。
  - 相较只保护传输或完全信任 aggregator，核心创新是把机密性与聚合完整性放进多方、分层防御架构。
  - 联邦学习安全、去中心化聚合、模型更新隐私、Integrity、纵深防御

- [ScheMoE: An Extensible Mixture-of-Experts Distributed Training System with Tasks Scheduling](https://doi.org/10.1145/3627703.3650083)
  - Harbin Institute of Technology, Shenzhen、The Hong Kong University of Science and Technology (Guangzhou)、Shenzhen Technology University、Huawei Central Research Institute, Huawei Technologies、The Hong Kong University of Science and Technology；Shaohuai Shi、Xinglin Pan、Qiang Wang、Chengjian Liu、Xiaozhe Ren、Zhongzhe Hu 等
  - ScheMoE 把 MoE training 拆成 expert compute、dispatch/combine 和通信 task，由可扩展 scheduler 依据依赖和设备状态重叠执行，并允许替换 routing/parallel component；较 Tutel/Faster-MoE 提升 9%–30%。
  - 相较把 MoE 并行流程固化在框架中，核心创新是 task-based extensible runtime，用统一 scheduler 组合不同优化。
  - MoE 训练、Task Scheduling、可扩展 Runtime、All-to-All、分布式 GPU

- [Erlang: Application-Aware Autoscaling for Cloud Microservices](https://doi.org/10.1145/3627703.3650084)
  - Google、NYU；Vighnesh Sachidananda、Anirudh Sivaraman
  - Erlang 为 cloud microservice 根据 application SLO 和调用结构自动扩缩 replica，比较用户自管 GKE Standard 与 provider 管理的 Autopilot 资源语义，在 90% 场景找到最优、其余接近最优。
  - 相较只按单 service CPU threshold，核心创新是 application-aware autoscaling 并显式适配不同云资源管理模式。
  - 微服务、Autoscaling、Kubernetes、应用感知、云资源管理

- [Just-In-Time Checkpointing: Low Cost Error Recovery from Deep Learning Training Failures](https://doi.org/10.1145/3627703.3650085)
  - Microsoft Research India；Tanmaey Gupta、Sanjeev Krishnan、Rituraj Kumar、Abhishek Vijeev、Bhargav Gulavani、Nipun Kwatra 等
  - Just-In-Time Checkpointing 在 DNN training failure 被检测时才触发状态保存/重建，通过训练迭代的确定性和数据/optimizer state 组织，让所有 GPU 最多重放一个 minibatch；稳态几乎无 checkpoint I/O，恢复从分钟降到秒。
  - 相较周期 checkpoint 持续占带宽或故障后回退多个 iteration，核心创新是把 checkpoint work 延迟到 failure time 但仍限制重放为一批。
  - 深度学习训练、故障恢复、JIT Checkpoint、GPU 集群、低稳态开销

- [Occam: A Programming System for Reliable Network Management](https://doi.org/10.1145/3627703.3650086)
  - Rice University、Meta、Max Planck Institute for Informatics、University of Michigan；Jiarong Xing、Kuo-Feng Hsu、Yiting Xia、Yan Cai、Yanping Li、Ying Zhang 等
  - Occam 用声明式任务描述和受控执行 primitive 编写 network management，系统规划设备更新顺序、验证中间状态并在失败时恢复，缩短配置变更期间的 vulnerability window。
  - 相较脚本直接逐设备下发命令，核心创新是把可靠性条件纳入 management programming system 的计划与运行时。
  - 网络管理、声明式编程、配置更新、故障恢复、可靠性

- [Jade: A High-throughput Concurrent Copying Garbage Collector](https://doi.org/10.1145/3627703.3650087)
  - Shanghai Jiao Tong University、Alibaba Group、Shanghai Jiao Tong University; Engineering Research Center for Domain-specific Operating Systems；Mingyu Wu、Liang Mao、Yude Lin、Yifeng Jin、Zhe Li、Hongtao Lyu 等
  - Jade 是 concurrent copying GC：group-wise collection 缩短对象真正可回收前的周期并控制 full-GC 频率，generational heap 与 single-phase young collection 提高吞吐，同时让应用 pause 保持短。
  - 相较传统并发复制器在低 pause 与 copy efficiency 间取舍，核心创新是按 group 组织回收并简化 young-generation path。
  - Garbage Collection、Concurrent Copying、Generational Heap、Pause Time、Managed Runtime

- [ZKML: An Optimizing System for ML Inference in Zero-Knowledge Proofs](https://doi.org/10.1145/3627703.3650088)
  - UIUC、Stanford、UC Berkeley；Bing-Jyue Chen、Suppakit Waiwitlikhit、Ion Stoica、Daniel Kang
  - ZKML 把 TensorFlow model 编译成 halo2 ZK-SNARK circuit，针对 tensor operator、量化/查表和约束布局做优化，使证明者能为视觉模型、distilled GPT-2 与推荐模型生成“正确执行且不泄漏输入/模型”的证明。
  - 相较只支持小型手写神经网络电路，核心创新是端到端 optimizing compiler 将现实 ML graph 系统化 lowering 到 ZK constraint。
  - Zero-Knowledge ML、ZK-SNARK、TensorFlow Compiler、隐私推理、可验证计算

- [Efficient Auditing of Event-driven Web Applications](https://doi.org/10.1145/3627703.3650089)
  - NYU and Google、NYU、ETH Zurich；Ioanna Tzialla、Jeffery Wang、Jingyi Zhu、Aurojit Panda、Michael Walfish
  - 该工作审计现代 event-driven Web application 是否按部署者认可的代码和事件顺序执行，在 server 记录紧凑 execution evidence，由 auditor 重建关键 handler/data dependency，兼顾 completeness、soundness 与可接受通信/计算开销。
  - 相较记录全部指令或只验证静态页面，核心创新是利用事件驱动框架边界生成最小但足够的执行证明。
  - Web 应用审计、Event-driven Runtime、执行完整性、可验证日志、安全

- [Volley: Accelerating Write-Read Orders in Disaggregated Storage](https://doi.org/10.1145/3627703.3650090)
  - Tsinghua University；Shaoxun Zeng、Xiaojian Liao、Hao Guo、Youyou Lu
  - Volley 在 disaggregated storage 的 writeback cache 与远端存储间保证 write-read I/O order，但允许 eviction write 和随后 fetch 并发发出；协议在接收/提交侧恢复顺序，应用于 VM storage 与 out-of-core computing。
  - 相较为保持顺序串行等待写完成，核心创新是把网络传输并行性与可见顺序解耦，以协议元数据在远端重建依赖。
  - Disaggregated Storage、Writeback Cache、I/O Ordering、并行传输、远端存储

- [Bandle: Asynchronous State Machine Replication Made Efficient](https://doi.org/10.1145/3627703.3650091)
  - Central South University and Shanghai Jiao Tong University、Shanghai Jiao Tong University、AntChain Platform Division, Ant Group、Fudan University、Central South University；Bo Wang、Shengyun Liu、He Dong、Xiangzhe Wang、Wenbo Xu、Jingjing Zhang 等
  - Bandle 是 asynchronous SMR：各 process 均匀拥有 sequence-number slot、无固定 leader 推进 proposal；FlashBA 对每个 proposal 做 binary agreement，决定能否提交，在任意消息延迟下保持安全。
  - 相较异步 BFT 由单 leader 排序或使用昂贵公共 coin 路径，核心创新是均匀序号分配与轻量 FlashBA 组合的 leaderless commit。
  - 异步状态机复制、Leaderless、Binary Agreement、BFT、分布式共识
