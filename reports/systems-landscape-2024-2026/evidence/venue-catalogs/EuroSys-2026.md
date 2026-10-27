# EuroSys 2026 论文列表

EuroSys 2026 正式 proceedings 共收录 138 篇论文。以下标题链接至 ACM DOI 页面；每篇依次列出机构与主要作者、研究场景和系统机制、相较既有方法的核心创新，以及细粒度方向。当前可合法直接获取的 43 份 PDF 已保存到 `reference/EuroSys/2026/`；其余论文依据正式摘要整理，不使用非授权镜像。

- [AdaServe: Accelerating Multi-SLO LLM Serving with SLO-Customized Speculative Decoding](https://dl.acm.org/doi/10.1145/3767295.3769315)
  - Carnegie Mellon University、Princeton University、EPFL、Amazon Web Services、Purdue University；Zikun Li、Zhuofu Chen、Remi Delacourt、Gabriele Oliaro、Zeyu Wang、Qinghan Chen 等
  - AdaServe 面向同时存在不同 latency SLO 的 LLM 请求，不为所有请求使用同一 speculative-decoding 参数；speculate-select-verify pipeline 按请求 deadline/服务等级选择 draft 长度和验证节奏，在满足差异化 SLO 的同时尽量合并 batch、提高吞吐。
  - 相较全局固定 speculative configuration，核心创新是把 speculation depth 和验证调度变成 per-SLO 决策，并在同一 serving pipeline 中共存。
  - LLM Serving、多 SLO、Speculative Decoding、请求级调度、延迟—吞吐权衡

- [FlexPipe: Adapting Dynamic LLM Serving Through Inflight Pipeline Refactoring in Fragmented Serverless Clusters](https://dl.acm.org/doi/10.1145/3767295.3769316)
  - UCAS, UCSD、Shenzhen Institute of Advanced Technology,Chinese Academy of Sciences、University of Macau、Shenzhen Institutes of Advanced Technology, Chinese Academy of Sciences；Yanying Lin、Shijie Peng、Chengzhi Lu、ChengZhong Xu、Kejiang Ye
  - FlexPipe 服务资源碎片化的 serverless LLM cluster，把模型分成细粒度 pipeline stage；它持续观察请求模式和可用 GPU，在请求仍执行时拆分、合并或重排 stage，改变 pipeline granularity 而不 drain 整个服务。
  - 相较部署时固定 pipeline parallelism，核心创新是 inflight pipeline refactoring，让模型并行结构成为运行时可变状态。
  - LLM Serving、Serverless GPU、Pipeline Refactoring、资源碎片、动态并行

- [Learn-to-Probe: Achieving Signal Distinguishability in Learning-based Congestion Control](https://dl.acm.org/doi/10.1145/3767295.3769317)
  - University of Science and Technology of China、Hong Kong University of Science and Technology、Huawei Technologies Co., Ltd.；Han Tian、Wenbo Li、Junxue Zhang、Xudong Liao、Decang Sun、Donghui Chen 等
  - Learn-to-Probe 不只让 learning-based congestion control 被动读取 RTT/ECN 等可能混淆的信号，而主动发出经过设计的 probe，使不同 bottleneck/network state 产生可区分响应，再以这些信号训练和控制。
  - 相较在不可辨识观测上堆叠更复杂模型，核心创新是先通过主动探测改造 observation space，从源头提高状态可辨识性。
  - Learning-based CC、Active Probing、Signal Engineering、网络状态辨识、鲁棒控制

- [iRoute: Local Routing Table-based Workflow Management in Serverless Computing](https://dl.acm.org/doi/10.1145/3767295.3769318)
  - Tianjin University、IEIT SYSTEMS CO., LTD.、Tsinghua University、China University of Geosciences、Inspur (Jinan) Data Technology Co., Ltd；Yiming Li、Laiping Zhao、Zhiyuan Su、Guowei Liu、Wenhao Huang、Kang Chen 等
  - iRoute 为 serverless workflow 把函数间路由下沉到本地 controller：本地 routing table 在关键路径直接选择下一函数，后台再与中心 coordinator 协作传播 workflow/version 更新并保持多副本一致。
  - 相较每一步都查询中心 orchestrator，核心创新是双层路由架构，在低延迟本地决策与全局一致配置之间分工。
  - Serverless Workflow、Local Routing、分层控制面、路由表一致性、函数编排

- [Taming Latency-Memory Trade-Off in MoE-Based LLM Serving via Fine-Grained Expert Offloading](https://dl.acm.org/doi/10.1145/3767295.3769319)
  - Stevens Institute of Technology、Rice University、University of Waterloo、Rutgers University、Stevens Institue of Technology；Hanfei Yu、Xingqi Cui、Hong Zhang、Hao Wang、Hao Wang
  - FineMoE 面向显存装不下全部 expert 的 MoE inference，从历史 routing 中学习细粒度 expert selection pattern，并结合 prompt semantic hint 预判下一层会访问哪些 expert；系统据此联合 prefetch、cache 和 offload，减少 miss 与等待。
  - 相较按全局热门 expert 或固定层序预取，核心创新是把请求语义和 layer/expert 粒度的选择相关性直接用于内存层次管理。
  - MoE Serving、Expert Offloading、语义预取、Expert Cache、显存管理

- [REPS: Recycled Entropy Packet Spraying for Adaptive Load Balancing and Failure Mitigation](https://dl.acm.org/doi/10.1145/3767295.3769320)
  - ETH Zürich / Microsoft、Microsoft、ETH Zürich、Sapienza University of Rome；Tommaso Bonato、Abdul Kabbani、Ahmad Ghalayini、Michael Papamichael、Mohammad Dohadwala、Lukas Gianinazzi 等
  - REPS 在每条连接仅维护不到 25B 状态，用可回收的 entropy 在 packet header/路径选择中做去中心 packet spraying；路径拥塞或链路失败时无需等待中心重算即可把后续 packet 快速散到可用路径。
  - 相较 per-flow ECMP 或维护大规模拓扑状态的 adaptive routing，核心创新是固定小状态的 recycled entropy 同时支持负载均衡和快速 failure mitigation。
  - 数据中心网络、Packet Spraying、负载均衡、链路故障恢复、小状态路由

- [TierScape: Harnessing Multiple Compressed Tiers to Tame Server Memory TCO](https://dl.acm.org/doi/10.1145/3767295.3769321)
  - Intel Labs；Sandeep Kumar、Aravinda Prasad、Sreenivas Subramoney
  - TierScape 把 DRAM 与多个不同压缩率/访问代价的 memory tier 纳入同一成本模型，持续监测应用 working set/access profile，按 SLA、内存价格和性能选择各 tier 容量与数据分布，直接优化 performance per dollar。
  - 相较只有 fast/slow 两层或固定 compression ratio，核心创新是可调的多压缩层 TCO 模型与在线 profile 驱动配置。
  - 分层内存、内存压缩、TCO、SLA、数据中心容量规划

- [Handling Network Faults in Distributed AI Training: Failover is Now an Option](https://dl.acm.org/doi/10.1145/3767295.3769322)
  - National University of Singapore、ByteDance；Xin Zhe Khooi、Zhuo Jiang、Pan Xie、Zhigang Cui、Meng Wang、Yuze Jin 等
  - ReCCL 为 distributed AI training 的 collective 建立可切换网络路径；链路/交换故障发生时保留 communicator 与训练进度，将未完成 collective fail over 到备用路径，而不是让整个 job rollback/restart。
  - 相较把 network fault 视为作业级失败，核心创新是 collective-library 内透明路径故障切换，并保持 collective correctness 与上层状态。
  - 分布式训练、Collective Communication、网络容错、Failover、训练连续性

- [Chimera: Transparent and High-Performance ISAX Heterogeneous Computing via Binary Rewriting](https://dl.acm.org/doi/10.1145/3767295.3769323)
  - Institute of Software Chinese Academy of Sciences; University of Chinese Academy of Sciences、Institute of Software Chinese Academy of Sciences; Key Laboratory of System Software (Chinese Academy of Sciences)、Hohai University; Institute of Software Chinese Academy of Sciences; University of Chinese Academy of Sciences, Nanjing; Nanjing Institute of Software Technology、University of Chinese Academy of Sciences; Institute of Software Chinese Academy of Sciences; University of Chinese Academy of Sciences, Nanjing; Nanjing Institute of Software Technology、Institute of Software Chinese Academy of Sciences；Jiatai He、Qinglin Pan、Ruilin Zhao、Ji Qi、Kaiwen Liang、Jiahao Xu 等
  - Chimera 通过 binary rewriting 让旧程序使用 ISAX/异构指令与 fault-based compatibility path；正常执行直接走优化代码，只有硬件/环境不支持或真正发生 fault 时才被动进入 handler，避免持续检查。
  - 相较每次执行都做能力判断或高开销动态翻译，核心创新是以 exception/fault 作为零常态成本的异构兼容触发器。
  - Binary Rewriting、ISAX、异构计算、Fault Handling、透明加速

- [Pyramid: A Secure, Resource-Efficient, and Pluggable Kubernetes for Multi-Tenancy](https://dl.acm.org/doi/10.1145/3767295.3769324)
  - Tsinghua University, China Telecom eSurfing Cloud (State Cloud)、Nankai University、Ant Group、Tsinghua University, Shanghai Qi Zhi Institute；Xiang Li、Weijie Liu、Fabing Li、Hongliang Tian、Zheli Liu、Shoumeng Yan 等
  - Pyramid 在商用 Kubernetes 上以可插拔组件提供 tenant control/data-plane 隔离和资源共享，尽量不侵入核心代码；安全边界与 fast path 共同设计，数据面吞吐较既有方案高 1.4 倍而控制面相当。
  - 相较重写 Kubernetes 或用完整 VM 隔离，核心创新是可插拔、低侵入的多租户安全层，同时保留共享集群效率。
  - Kubernetes、多租户、安全隔离、可插拔编排、资源效率

- [MegaScale-MoE: Large-Scale Communication-Efficient Training of Mixture-of-Experts Models in Production](https://dl.acm.org/doi/10.1145/3767295.3769325)
  - School of Computer Science, Peking University、ByteDance Seed；Chao Jin、Ziheng Jiang、Zhihao Bai、Zheng Zhong、Juncai Liu、Xiang Li 等
  - MegaScale-MoE 是生产级大规模 MoE training system：attention 与 FFN/expert 分别选择适合的并行和通信方式，并在 operator 内把通信切片重叠计算、在 operator 间流水不同 collective，降低 all-to-all 暴露时间。
  - 相较整层采用统一 parallelism、只做算子间 overlap，核心创新是 attention/FFN 定制并行加上 inter-与 intra-operator 双层通信重叠。
  - MoE 训练、生产集群、通信重叠、并行策略、All-to-All

- [Effective On-Hardware Fuzzing of Embedded Operating Systems](https://dl.acm.org/doi/10.1145/3767295.3769326)
  - Tsinghua University、Shandong University、Beihang University、Hunan University、Central South University；Yuheng Shen、Jianzhong Liu、Qiming Guo、Yifei Chu、Qiang Zhang、Heyuan Shi 等
  - EOF 直接在真实 embedded hardware 上 fuzz OS，而非只在 emulator 中运行；feedback-guided input/事件生成在设备上收集 coverage，并处理重启、外设和低可观测性。四种 OS 上平均覆盖提高 50.84%，发现 19 个 bug。
  - 相较仿真 fuzzing 难覆盖硬件相关路径，核心创新是为实机生命周期和有限反馈设计可持续、高吞吐的 on-hardware fuzz loop。
  - 嵌入式 OS、On-hardware Fuzzing、Coverage Feedback、实机测试、漏洞发现

- [GeDES: GPU-Driven Discrete Event Network Simulator](https://dl.acm.org/doi/10.1145/3767295.3769327)
  - University of Electronic Science and Technology of China、Department of Computer Science, University of Exeter；Qinyong Li、Zhiwei Zhao、Geyong Min、Zi Wang、Luwei Fu
  - GeDES 把离散事件网络仿真的事件队列与 handler 调度移到 GPU，通过控制 event lifecycle，并以长期/短期 alignment 把可并行事件组成适合 SIMT 的批次，减少 divergence 与同步。
  - 相较 CPU PDES 或简单 GPU batch，核心创新是以事件生命周期对齐解决因果顺序和 GPU 规则执行之间的不兼容。
  - 网络仿真、GPU、Discrete Event Simulation、事件对齐、并行模拟

- [TokenFlow: Responsive LLM Text Streaming Serving under Request Burst via Preemptive Scheduling](https://dl.acm.org/doi/10.1145/3767295.3769328)
  - Shanghai Jiao Tong University、George Mason University、China Telecom Corporation Limited Shanghai Branch；Junyi Chen、Chuheng Du、Renyuan Liu、Shuochao Yao、Dingtian Yan、Jiang Liao 等
  - TokenFlow 面向突发请求下的 LLM streaming，按每个请求 token buffer occupancy 与用户消费速度动态提高/降低优先级；抢占时在后台迁移 GPU/CPU KV cache，并把 I/O 与其他请求计算重叠，维持连续出字。
  - 相较只按到达时间或生成进度抢占，核心创新是消费端反馈驱动的 token-level scheduling 与低成本 KV state preemption。
  - LLM Streaming、突发流量、Preemptive Scheduling、KV 迁移、Token Buffer

- [Federated Fine-Tuning of Sparsely-Activated Large Language Models on Resource-Constrained Devices](https://dl.acm.org/doi/10.1145/3767295.3769329)
  - Shandong University, China, Xi'an Jiaotong University, China、Xi'an Jiaotong University, China、Shandong University, China；Fahao Chen、Jie Wan、Peng Li、Zhou Su、Dongxiao Yu
  - Flux 让资源受限 client 联邦微调 sparsely activated MoE LLM：参与方只处理/更新被路由到的部分 expert，并围绕设备算力、内存和通信能力分配 expert/训练任务，再安全聚合稀疏更新。
  - 相较每个 client 加载完整 dense/ MoE 模型，核心创新是利用 sparse activation 将联邦训练状态和工作量裁剪到设备可承受范围。
  - Federated Fine-tuning、MoE LLM、资源受限设备、稀疏更新、边缘训练

- [Multipath Collective Communication Beyond Scale-up Networks in GPU Clouds](https://dl.acm.org/doi/10.1145/3767295.3769330)
  - Peking University、Tencent；Yuchen Xu、Jianglong Nie、Baojia Li、Mingzhuo Chen、Hao Lu、Guanyu Qu 等
  - MPCCS 让 GPU collective 同时利用 scale-up fabric 与 scale-out network 的多条路径，针对不同 collective 构造满足数据依赖的 striping/scheduling，并在链路能力不均时仍寻求性能最优。
  - 相较只在单一网络内做 multipath 或固定 ring/tree，核心创新是跨网络层统一 collective correctness 与路径带宽优化。
  - GPU Collective、Multipath、Scale-up/Scale-out、通信调度、GPU Cloud

- [LoRAFusion: Efficient LoRA Fine-Tuning for LLMs](https://dl.acm.org/doi/10.1145/3767295.3769331)
  - University of Toronto, Vector Institute, NVIDIA；Zhanda Zhu、Qidong Su、Yaoyao Ding、Kevin Song、Shang Wang、Gennady Pekhimenko
  - LoRAFusion 重构 LoRA fine-tuning kernel/dataflow，融合 base GEMM 与低秩增量计算，避免重复读 activation/weight，同时不以 recomputation 或额外同步换内存；多 job 时再按 shape/资源自适应组 batch。
  - 相较把 LoRA 作为 GEMM 外独立算子，核心创新是保持 compute-bound GEMM 效率的融合执行与 multi-job adaptive batching。
  - LoRA Fine-tuning、Kernel Fusion、Memory Access、Multi-job Batching、LLM 训练

- [SKernel: An Elastic and Efficient Secure Container System at Scale with a Split-Kernel Architecture](https://dl.acm.org/doi/10.1145/3767295.3769332)
  - Tsinghua University; Ant Group、Tsinghua University、Ant Group、Shanghai Jiao Tong University、Quan Cheng Laboratory, Jinan, China; Tsinghua University；Xiaohu Chai、Keyang Hu、Jianfeng Tan、Tiwei Bie、Guotao Tan、Tianyu Zhou 等
  - SKernel 用 split-kernel architecture 将 secure container 的最小隔离/资源核心与可弹性扩展服务分开；file-descriptor-based filesystem 以受控 handle 访问文件，减少路径转换和不必要 indirection，面向生产规模快速扩缩。
  - 相较每容器完整 kernel/VM 或共享大内核，核心创新是安全关键核与功能核分离，并让文件描述符成为容器文件系统能力边界。
  - 安全容器、Split Kernel、弹性、Capability/FD Filesystem、生产系统

- [Untangling GPU Power Consumption: Job-Level Inference in Cloud Shared Settings](https://dl.acm.org/doi/10.1145/3767295.3769333)
  - École de technologie supérieure、Univ Lyon1, Inria, OVHcloud、Univ Lyon1, Inria, ENS de Lyon, CNRS、CNRS, IRISA, Rennes - France；Pierre Jacquet、Maxime Agusti、Eddy Caron、Camille Coti、Marcos Dias De Assunção、Laurent Lefèvre 等
  - 该工作在 MLaaS/IaaS 的共享 GPU 上做 job-level power attribution，从设备总功耗、利用率和可观测计数推断每个共置 job 的能耗，覆盖用户无法独占读电表的管理型服务。
  - 相较用 GPU 时间或平均 TDP 粗分，核心创新是针对共享、不同可观测权限场景建立并验证 job-level inference 方法。
  - GPU 能耗归因、云共享、MLaaS、Power Modeling、可持续计算

- [TZ-LLM: Protecting On-Device Large Language Models with Arm TrustZone](https://dl.acm.org/doi/10.1145/3767295.3769334)
  - Shanghai Jiao Tong University；Xunjie Wang、Jiacheng Shi、Zihan Zhao、Yang Yu、Zhichao Hua、Jinyu Gu
  - TZ-LLM 用 Arm TrustZone 保护端侧 LLM 权重/执行；TEE 中只放最小 NPU data-plane co-driver，复杂控制仍由 REE driver 完成，并用 pipelined restoration 在受保护/普通内存间恢复模型状态以隐藏切换成本。
  - 相较把完整 NPU driver 放入 TEE 或只加密静态模型，核心创新是 co-driver 最小可信路径与流水恢复共同保护实际推理。
  - On-device LLM、Arm TrustZone、NPU Driver、模型保护、TEE

- [STAlloc: Enhancing Memory Efficiency in Large-Scale Model Training with Spatio-Temporal Planning](https://dl.acm.org/doi/10.1145/3767295.3769335)
  - Tsinghua University、Infinigence-AI、Shanghai Jiao Tong University；Zixiao Huang、Junhao Hu、Hao Lin、Chunyang Zhu、Yueran Tang、Quanlu Zhang 等
  - STAlloc 分析大模型训练 allocation 的空间大小规律与时间 lifetime，预先规划可复用的 GPU memory region，使不重叠 tensor 共享地址、避免通用 allocator 的碎片；由此支持更大/更高吞吐配置。
  - 相较只按请求到达做 best-fit caching allocator，核心创新是从训练图提取 spatio-temporal regularity 做全局内存规划。
  - 大模型训练、GPU Allocator、显存碎片、Lifetime Planning、内存复用

- [Efficient Data Passing for Serverless Inference Workflows: A GPU-Centric Approach](https://dl.acm.org/doi/10.1145/3767295.3769336)
  - HUST、CUHK-Shenzhen、TeleAI、HKUST；Hao Wu、Yaochen Liu、Minchen Yu、Qizhen Weng、Junxiao Deng、Yue Yu 等
  - GRouter 为 serverless inference workflow 统一抽象 host-GPU 与 GPU-GPU state passing，并把 function placement 与传输共同决定；它聚合 PCIe、NVLink、NIC 多条带宽并行传数据，同时隔离不同函数流量。
  - 相较每对函数固定走 host staging/RPC，核心创新是 GPU-centric placement-aware router，在异构互连上自动选择和聚合路径。
  - Serverless Inference、GPU 数据传输、Function Placement、异构互连、性能隔离

- [PatternSketch: General and Runtime Reconfigurable Time-series Network Traffic Pattern Detection](https://dl.acm.org/doi/10.1145/3767295.3769337)
  - Soochow University, Suzhou, China、Nanjing University of Posts and Telecommunications, Nanjing, China；Yang Du、Dan Wang、He Huang、Hanwen Zhang、Jianzhi Tang、Fu Xiao 等
  - PatternSketch 用 Pattern Automaton 统一描述 time-series traffic 中的多种顺序/时间 pattern，将检测拆成 data-plane 两阶段以适配 switch pipeline；operator 可在线替换 active pattern set 而不重启设备。
  - 相较为每种 pattern 编译独立 sketch/automaton，核心创新是通用 automaton abstraction 与 runtime-reconfigurable data path。
  - 可编程网络、Time-series Pattern、Sketch、Runtime Reconfiguration、流量检测

- [Concord: Learning Network Configuration Contracts](https://dl.acm.org/doi/10.1145/3767295.3769338)
  - Microsoft Research、University of Illinois Urbana-Champaign、Microsoft；Ryan Beckett、Francis Y. Yan、Raghunadha Reddy Pocha、Vineesh V. Raj、Ayyub Shaik、Siva Kesava Reddy Kakarla
  - Concord 从大量正确 network configuration 学 relational contract，捕获跨设备、跨配置项的依赖；新配置违反 contract 时可定位到具体行，无需为 BGP/ACL 等协议建立完整 formal model。
  - 相较逐字段规则或重量级协议建模，核心创新是可扩展地学习多配置实体之间的关系型不变量。
  - 网络配置、Contract Learning、配置验证、错误定位、关系不变量

- [LLMFolder: Revisiting Constant Folding in Large Language Models](https://dl.acm.org/doi/10.1145/3767295.3769339)
  - Shanghai Jiao Tong University、Shanghai JiaoTong University；Gansen Hu、Zhaoguo Wang、Wei Huang、Jinglin Wei、Haibo Chen
  - LLMFolder 观察 LLM activation 在常见输入区间可近似线性，将部分 nonlinear activation 替换为区间线性函数，使相邻线性层可做 constant folding/weight folding，减少运行时算子。
  - 相较认为非线性必然阻断 folding，核心创新是基于实际 activation range 的受控近似，把传统编译常量折叠扩展到 LLM。
  - LLM 推理、Constant Folding、Activation Approximation、模型编译、算子消除

- [Ethane: Debloating State Data using Compact Trie for Account-based Blockchain](https://dl.acm.org/doi/10.1145/3767295.3769340)
  - Seoul National University；Junmo Lee、Jaehun Kim、Jiyong Youn、Soo-Mook Moon
  - Ethane 为 account-based blockchain 重构 current/archive state trie，以 compact trie 消除历史版本中重复 path/node，同时保持按账户和历史高度查询；archive state 缩小 60–85%，current trie 缩小 60–94%。
  - 相较对每个版本保存完整 Merkle trie 分支，核心创新是面向账户状态演化的结构共享与紧凑节点表示。
  - 区块链存储、State Trie、Archive State、去冗余、Merkle Structure

- [Scheduling Cloud Block Storage Proactively and Reactively with Omar](https://dl.acm.org/doi/10.1145/3767295.3769341)
  - Shanghai Jiao Tong University、Alibaba Group、The Chinese University of Hong Kong；Xinqi Chen、Weidong Zhang、Zhongyu Wang、Erci Xu、Xiaolu Zhang、Dong Wu 等
  - Omar 管理 cloud block storage 的细粒度 I/O scheduling：proactive 部分根据历史/趋势提前调整资源，reactive 部分在突发和 interference 出现时快速纠偏，避免每个短期波动都触发昂贵重排。
  - 相较纯周期规划或纯反馈控制，核心创新是混合双路径，在降低 64KiB tail latency 的同时减少 44.6% 调度操作。
  - 云块存储、I/O Scheduling、Proactive/Reactive、Tail Latency、控制开销

- [OptiLog: Assigning Roles in Byzantine Consensus](https://dl.acm.org/doi/10.1145/3767295.3769342)
  - University of Stavanger、Friedrich-Alexander-Universität Erlangen-Nürnberg、Reykjavik University；Hanish Gogada、Christian Berger、Leander Jehl、Hans P. Reiser、Hein Meling
  - OptiLog 在 Byzantine consensus 运行中识别 slow/misbehaving replica，并动态分配 proposer/voter 等角色或排除异常节点，使正常节点继续使用低延迟优化配置，同时保留不利条件下的安全性。
  - 相较固定角色和 quorum，核心创新是把 replica behavior 转成在线 role assignment，而不是让少数坏节点长期拖慢 fast path。
  - Byzantine Consensus、Role Assignment、异常副本、低延迟、BFT

- [FUR: Fast and Unlimited Reads on Persistent Memory Transactions](https://dl.acm.org/doi/10.1145/3767295.3769343)
  - INESC-ID, IST, Universidade de Lisboa, Portugal、São Paulo State University (Unesp), Brazil；João Barreto、Daniel Castro、Paolo Romano、Alexandro Baldassin
  - FUR 优化 persistent hash table 的 read-only transaction，消除读路径上的全局 version/日志检查与容量上限，让任意数量读取在并发更新下仍得到一致 snapshot。
  - 相较为只读事务维护昂贵 read set 或受固定 slot 限制，核心创新是无界读取的轻量一致性协议。
  - Persistent Memory、Hash Table、Read-only Transaction、并发控制、Snapshot

- [Rearchitecting Programmable Networks For In-Network Computing: From Hardware To Language](https://dl.acm.org/doi/10.1145/3767295.3769344)
  - National Key Laboratory for Multimedia Information Processing, School of Computer Science, Peking University、Huawei Cloud Computing Technologies Co., Ltd.、Huawei Technologies Co., Ltd、Institute of Computing Technology, CAS；Haifeng Sun、Bing Liu、Taixu Tian、Jinbo Sun、Jintao He、Qun Huang 等
  - 该 full-stack in-network computing 方案从硬件到语言共同设计：Solar-NP chipset 提供超越固定 pipeline 的执行资源，NPC 表达更复杂 state/control，XuanWu toolchain 完成编译、放置和部署。
  - 相较只扩展 P4 pipeline 或单点硬件加速，核心创新是 chipset-语言-编译器协同，使更多操作可安全 offload。
  - In-network Computing、可编程芯片、网络语言、Compiler Toolchain、软硬件协同

- [AdaGen: Workload-Adaptive Cluster Scheduler for Latency-Optimal LLM Inference Serving](https://dl.acm.org/doi/10.1145/3767295.3769345)
  - University of Virginia、HPE Labs、University of California, Riverside；Sudipta Saha Shubha、Ayush Goel、Diman Zad Tootaghaj、Khaled Diab、Hardik Soni、K. K. Ramakrishnan 等
  - AdaGen 为 LLM inference cluster 根据请求长度、到达率和模型配置动态选择 instance 数、tensor/pipeline layout 与 batch；simulation-based estimator 预测候选布局的延迟，再直接优化 SLO attainment。
  - 相较按平均利用率扩容或固定并行，核心创新是 workload-adaptive compute-layout search 与仿真延迟估计联合。
  - LLM Serving、集群调度、Compute Layout、Latency Estimation、SLO

- [TailorLLM: Collaborative End-Cloud Inference of Large and Small Language Models Based on Low-Rank Adaptation](https://dl.acm.org/doi/10.1145/3767295.3769346)
  - Beijing University of Posts and Telecommunications；Zian Wang、Ziyi Wang、Haonan Jin、Jie Xing、Lanshan Zhang
  - TailorLLM 以 end-cloud 协作完成不同任务：端侧 small model 加载任务 LoRA，必要时与云端 large model 协作；AdapterMgr 用 imitation learning 预测有限端侧 LoRA library 的替换，兼顾命中、传输和质量。
  - 相较所有请求上云或端侧固定 adapter，核心创新是 task-level 大小模型协作与 learned LoRA cache replacement。
  - End-Cloud LLM、大小模型协作、LoRA、Adapter Cache、Imitation Learning

- [NecoFuzz: Effective Fuzzing of Nested Virtualization via Fuzz-Harness Virtual Machines](https://dl.acm.org/doi/10.1145/3767295.3769347)
  - The University of Tokyo、National Institute of Advanced Industrial Science and Technology；Reima Ishii、Takaaki Fukai、Takahiro Shinagawa
  - NecoFuzz 针对 nested virtualization 专属 hypervisor logic，依据 VT-x/AMD-V 规格近似模型生成接近 valid/invalid 边界且可执行的 fuzz-harness VM；覆盖关键代码 84.7%/74.2%，在三种 hypervisor 发现 6 个未知漏洞。
  - 相较以普通 guest instruction 为输入的 hypervisor fuzzer，核心创新是把完整 VM internal state 作为规格导向、边界导向的 fuzz input。
  - Nested Virtualization、Hypervisor Fuzzing、Fuzz-harness VM、VT-x/AMD-V、漏洞发现

- [KUNSERVE: Parameter-centric Memory Management for Efficient Memory Overloading Handling in LLM Serving](https://dl.acm.org/doi/10.1145/3767295.3769348)
  - Shanghai Jiao Tong University、Shanghai JiaoTong University；Rongxin Cheng、Yuxin Lai、Xingda Wei、Rong Chen、Haibo Chen
  - KUNSERVE 在 LLM serving overload 时不立即 evict 整个模型/KV，而利用多 GPU 上 replicated parameter，选择性丢弃可从其他 GPU/层恢复的副本以瞬间释放显存接纳请求。
  - 相较 request rejection、模型 swap 或 KV eviction，核心创新是 parameter-centric memory reclamation，把冗余权重本身变成 overload buffer。
  - LLM Serving、Overload、Parameter Replication、显存回收、多 GPU

- [SwitchFS: Asynchronous Metadata Updates for Distributed Filesystems with In-Network Coordination](https://dl.acm.org/doi/10.1145/3767295.3769349)
  - Shanghai Jiao Tong University；Jingwei Xu、Mingkai Dong、Qiulin Tian、Ziyi Tian、Tong Xin、Haibo Chen
  - SwitchFS 让 distributed filesystem 的目录/metadata update 异步返回，更新记录由 programmable switch 协调；真正读目录或依赖元数据时再完成/合并 pending update，从而隐藏写延迟并摊销操作。
  - 相较每次 mutation 同步更新一致 metadata server，核心创新是 in-network coordination 支撑 read-triggered deferred metadata consistency。
  - 分布式文件系统、异步元数据、In-network Coordination、目录更新、延迟隐藏

- [DROPS: Managing Serverless Resource Pools in Microsoft Azure Functions](https://dl.acm.org/doi/10.1145/3767295.3769350)
  - University of Waterloo、Microsoft Research、Microsoft；Ahmed Alquraan、Abdelrahman Baba、Rafael Mendes、Sameh Elnikety、Paul Batum、Yan Chen 等
  - DROPS 使用 Azure Functions 历史 trace 为不同函数/规格计算 warm resource pool size，在 cold-start SLO 与闲置成本间优化，并随 workload 分布更新；生产上较原静态配置降成本 41%。
  - 相较固定预热池或简单 percentile 容量，核心创新是 per-pool statistical sizing 直接以目标 SLO 和历史不确定性约束。
  - Serverless、Resource Pool、Warm Instance、Trace-driven Optimization、Azure Functions

- [FlexiQ: Adaptive Mixed-Precision Quantization for Latency/Accuracy Trade-Offs in Deep Neural Networks](https://dl.acm.org/doi/10.1145/3767295.3769351)
  - Seoul National University、Hanyang University、Yonsei University；Jaemin Kim、Hongjun Um、Sungkyun Kim、Yongjun Park、Jiwon Seo
  - FlexiQ 针对 vision DNN 的 channel value range 选择 mixed precision：范围小、量化误差低的 channel 采用更低 bit，bit-lowering 方法在运行时/部署时快速切换，以满足不同 latency-accuracy target。
  - 相较 layer-wise 固定位宽，核心创新是 channel-selective、可适应目标的 mixed-precision quantization。
  - DNN 推理、Mixed Precision、Channel Quantization、Latency-Accuracy、Computer Vision

- [Turnstile: Hybrid Information Flow Control Framework for Managing Privacy in Internet-of-Things Applications](https://dl.acm.org/doi/10.1145/3767295.3769352)
  - University of British Columbia、Princeton University；Kumseok Jung、Mohanna Shahrad、Gargi Mitra、Karthik Pattabiraman
  - Turnstile 先用 static taint analysis 找出 IoT app 中真正涉及敏感数据的 path，再只对这些 path 插入 dynamic information-flow tracking；运行时阻止未授权 flow，同时避免全程序 DIFT 开销。
  - 相较纯静态误报或全量动态跟踪，核心创新是 static selection + selective DIFT 的 hybrid IFC。
  - IoT Privacy、Information Flow Control、Static Taint、DIFT、Selective Instrumentation

- [SkyWalker: A Locality-Aware Cross-Region Load Balancer for LLM Inference](https://dl.acm.org/doi/10.1145/3767295.3769353)
  - UC Berkeley、Renmin University of China、Rice University and UC Berkeley、ICSI and UC Berkeley；Tian Xia、Ziming Mao、Jamison Kerney、Ethan J. Jackson、Zhifei Li、Jiarong Xing 等
  - SkyWalker 为多地域 LLM inference 同时考虑各 region 昼夜供需互补、跨区成本/延迟和 KV-cache locality；它把流量迁到空闲地域但尽量让同一会话留在已有 KV 的位置。
  - 相较只按负载/价格跨区路由，核心创新是把 stateful KV locality 纳入 global load balancing。
  - 多地域 LLM Serving、KV Locality、跨区负载均衡、昼夜模式、成本优化

- [PASS: A Power Adaptive Storage Server](https://dl.acm.org/doi/10.1145/3767295.3769354)
  - University of Washington、Databricks；Dedong Xie、Theano Stavrinos、Jonggyu Park、Simon Peter、Baris Kasikci、Thomas E. Anderson
  - PASS 在 storage server 受 power cap 或供电波动时联合调整 CPU、device polling/queue 与 I/O 并发，使资源随功率预算降级而不出现失配；Filebench 吞吐较 SPDK+Thunderbolt 高 3–25 倍。
  - 相较通用 server power capping 独立压频，核心创新是 storage-path-aware power adaptation，让软件并发匹配实际设备/CPU 功率。
  - 存储服务器、Power Capping、SPDK、I/O 并发、能效

- [MFS: An Efficient Model Family Serving System for LLMs](https://dl.acm.org/doi/10.1145/3767295.3769355)
  - Hong Kong University of Science and Technology、University of Science and Technology of China、Inspur；Yunxuan Zhang、Hao Wang、Han Tian、Liu Yang、Xudong Liao、Wenxue Li 等
  - MFS 面向同一 LLM family 的不同 scale/variant，识别层结构与参数冗余，把公共权重、delta/特有层放在不同内存层，并按请求快速组合目标模型，避免每个尺寸完整驻留。
  - 相较把 family member 当独立模型部署，核心创新是 family-aware multi-tier parameter sharing 与按需组装。
  - LLM Model Family、Multi-tier Serving、参数共享、模型变体、显存管理

- [LightDSA: Enabling Efficient DSA Through Hardware-Aware Transparent Optimization](https://dl.acm.org/doi/10.1145/3767295.3769356)
  - Renmin University of China、Alibaba Group、CNIC, CAS；Yuansen Wang、Teng Ma、Yuanhui Luo、Dongbiao He、Zheng Liu、Yunpeng Chai
  - LightDSA 系统测量 Intel Data Streaming Accelerator 的五类内部机制，在此基础上用异步 library 自动选择 descriptor、batch、queue 与 run-to-completion path，让应用透明获得适合硬件的配置。
  - 相较直接调用通用 DSA API，核心创新是将硬件机制归纳为设计原则并封装成低开销自适应 runtime。
  - Intel DSA、数据搬运、Hardware-aware Optimization、异步 Runtime、透明加速

- [Squeezy: Rapid VM Memory Reclamation for Serverless Functions](https://dl.acm.org/doi/10.1145/3767295.3769357)
  - National Technical University of Athens, Athens, Greece、University of Illinois Urbana-Champaign, Illinois, USA；Orestis Lagkas Nikolos、Chloe Alverti、Stratos Psomadakis、Georgios Goumas、Nectarios Koziris
  - Squeezy 为 FaaS VM 快速回收数 GiB 内存，在 guest/hypervisor 间建立批量、低干扰 reclaim path，并控制回收速率避免 function tail latency 爆炸；多 GiB 可在亚秒完成。
  - 相较 balloon/逐页回收，核心创新是针对 serverless 生命周期的高速批量 reclamation 与 tail-latency guardrail。
  - Serverless VM、内存回收、Ballooning、Tail Latency、资源弹性

- [FlexiWalker: Extensible GPU Framework for Efficient Dynamic Random Walks with Runtime Adaptation](https://dl.acm.org/doi/10.1145/3767295.3769358)
  - Seoul National University；Seongyeon Park、Jaeyong Song、Changmin Shin、Sukjin Kim、Junguk Hong、Jinho Lee
  - FlexiWalker 支持动态图上的多种 random walk；轻量一阶 cost model 根据每个 node 的 degree、更新和采样特征，在运行时选择更快 GPU kernel，并允许扩展新的 walk rule。
  - 相较全图固定 kernel 或只支持一种采样，核心创新是 per-node runtime adaptation 的可扩展 GPU framework。
  - 动态图、Random Walk、GPU Kernel、Cost Model、Runtime Adaptation

- [PaCaR: Improved Buffered I/O Locality on NUMA Systems with Page Cache Replication](https://dl.acm.org/doi/10.1145/3767295.3769359)
  - RWTH Aachen University、LIP6 (UPMC/CNRS) - Inria；Jérôme Coquisart、Julien Sopena、Redha Gouicem
  - PaCaR 在 NUMA system 上为 buffered I/O page cache 跨 node 复制热点 page，让线程从本地内存命中；它维护写一致性，并在 memory pressure 下自动收缩副本，对应用透明。
  - 相较单份 page cache 导致 remote NUMA access，核心创新是可写一致、压力感知的 cache-page replication。
  - NUMA、Page Cache、Buffered I/O、页面复制、数据局部性

- [RLive: Robust Delivery System for Scaling Live Streaming Services](https://dl.acm.org/doi/10.1145/3767295.3769360)
  - Institute of Computing Technology, University of Chinese Academy of Sciences、ICT, CAS、ICT/CAS、ByteDance、Bytedance；Yu Tian、Gerui Lv、Qinghua Wu、Ruili Fang、Yajie Peng、Zhichen Xue 等
  - RLive 用 best-effort edge 扩大 live-streaming CDN：redundancy-free multi-source data plane 从多个上游补齐内容而不重复传完整流；多层 control plane 以全局容量视图分配用户、局部快速适应节点变化。
  - 相较只使用专用稳定边缘或复制多份流，核心创新是无冗余多源可靠传输与全局—局部协同映射。
  - Live Streaming、CDN、Best-effort Edge、Multi-source Delivery、分层控制面

- [Carbon-Aware Continuous Learning for Sustainable Real-Time Machine Learning Analytics](https://dl.acm.org/doi/10.1145/3767295.3769361)
  - Sungkyunkwan University、Unaffiliated、POSTECH；Gwanjong Park、Osama Khan、Dongho Ha、Myeongjae Jeon、Euiseong Seo
  - CCL 服务实时 ML analytics 的持续学习，在 data drift 后决定何时标注/重训、使用哪个 labeling model 以及 retraining hyperparameter；预测 drift severity 与未来 grid carbon intensity，把可延后的训练移到低碳窗口且维持 inference accuracy。
  - 相较只按精度下降阈值重训，核心创新是把模型更新策略与时变碳强度联合控制，而不是单纯迁移推理负载。
  - Continuous Learning、Carbon-aware Computing、Data Drift、在线分析、重训练调度

- [Canopy: Property-Driven Learning for Congestion Control](https://dl.acm.org/doi/10.1145/3767295.3769362)
  - UT Austin、Google DeepMind；Chenxi Yang、Divyanshu Saxena、Rohit Dwivedula、Kshiteej Mahajan、Swarat Chaudhuri、Aditya Akella
  - Canopy 训练 congestion controller 时由用户给出 safety/performance property，把它们转成学习过程的约束与反例反馈，使 controller 可适应新网络条件，同时对 worst-case behavior 保留可检查界限。
  - 相较只最大化平均 reward 的 learned CC，核心创新是 property-driven learning，把可靠性要求纳入 policy synthesis/training。
  - Learning-based CC、Property-driven Learning、Worst-case Reliability、网络控制、形式约束

- [Towards Improving Throughput and Scalability of DAG-based BFT SMR](https://dl.acm.org/doi/10.1145/3767295.3769363)
  - Supra Research、Supra Research / Purdue University；Nibesh Shrestha、Aniket Kate
  - 该工作为 DAG-based BFT 引入 tribe-assisted reliable broadcast：从全网 tribe 中选较小、诚实多数的 clan 执行广播/认证，再让 DAG consensus 利用这些结果减少全网通信；据此构建两种高吞吐协议。
  - 相较每个 proposal 都在全部 replica 间 reliable broadcast，核心创新是以动态小委员会提供可组合广播保证。
  - DAG BFT、Reliable Broadcast、小委员会、状态机复制、共识扩展

- [SAS: Sparse Attention Synthesizer for Efficient Language Model Inference](https://dl.acm.org/doi/10.1145/3767295.3769364)
  - Amazon；Yuan Zhou、Shaojie Xiang、Lingfan Yu、Zhenyu Song、Charith Mendis、Yida Wang
  - SAS 用一组 primitive 表达 static/dynamic sparse-attention pattern，用户通过逻辑算子和声明函数组合规则；synthesizer 再针对 shape、sparsity 和硬件自动生成并调优 GPU kernel。
  - 相较每种 sparse attention 手写 kernel，核心创新是统一 pattern DSL 与自动 kernel synthesis，既覆盖规则稀疏也覆盖运行时稀疏。
  - Sparse Attention、Kernel Synthesis、LLM Inference、DSL、GPU

- [Gopher: Efficient Dynamic Graph Pattern Mining via DAG-Driven Execution](https://dl.acm.org/doi/10.1145/3767295.3769365)
  - Huazhong University of Science and Technology, China、Michigan Technological University, USA、University of New South Wales, Australia；Yi Zhang、Yu Huang、Chaoqiang Liu、Haifeng Liu、Juntao Chen、Jingrui Yuan 等
  - Gopher 把 dynamic graph pattern mining 的匹配依赖组织成 DAG，以细粒度 task 解耦可并行步骤并维持 computation locality；canonical-expression restoration 在分支结果合并时去重并恢复完整 match。
  - 相较按 pattern tree 固定深度优先探索，核心创新是依赖 DAG 驱动的并行执行与规范表达式结果装配。
  - 动态图挖掘、Pattern Mining、DAG Execution、Fine-grained Parallelism、结果去重

- [Maya: Optimizing Deep Learning Training Workloads using GPU Runtime Emulation](https://dl.acm.org/doi/10.1145/3767295.3769366)
  - Georgia Institute of Technology、Nvidia Inc.；Srihas Yarlagadda、Amey Agrawal、Elton Pinto、Hakesh Darapaneni、Mitali Meratwal、Shivam Mittal 等
  - Maya 不真实占用目标 GPU 训练全部候选，而透明仿真 CUDA/runtime 行为以估计不同 model、parallelism 和优化配置的时间/资源；预测误差低于 5%，据此找到训练成本低 56% 的方案。
  - 相较解析性能模型或缩小训练实验，核心创新是 device-runtime emulation，直接复用真实训练栈捕获复杂交互。
  - GPU Runtime Emulation、训练性能建模、配置搜索、成本优化、DNN Training

- [Serverless Replication of Object Storage across Multi-Vendor Clouds and Regions](https://dl.acm.org/doi/10.1145/3767295.3769367)
  - School of Computer Science, Peking University and UCLA、School of Computer Science, Peking University；Junyi Shu、Xiaolong Huang、Gang Huang、Hong Mei、Xuanzhe Liu、Xin Jin
  - 该系统用按需 cloud function 在不同 vendor/region 的 object store 间复制对象，事件触发后临时建立传输/并发，完成即释放；启动从数十秒降到数秒，复制延迟降 61%–99%、成本最多低三个数量级。
  - 相较常驻 replication service 预留峰值容量，核心创新是以 serverless execution 构建跨云、按对象弹性的数据复制路径。
  - 对象存储复制、Serverless、多云、多地域、成本优化

- [Fast and Parallelized Crash Consistency with Opportunistic Order Elimination](https://dl.acm.org/doi/10.1145/3767295.3769368)
  - Harbin Institute of Technology, Shenzhen；Jiahao Chen、Yanqi Pan、Wen Xia、Hao Huang、Peixin Zeng、Yuchen Shan
  - ChimeraFS 为 persistent-memory filesystem 的 crash consistency 识别无需保持的写顺序，在运行时 opportunistically 消除这些 ordering edge，让互不依赖的持久写并行提交，接近 PM 理想并行带宽。
  - 相较以保守 fence/log 顺序串行化更新，核心创新是动态证明/判断可消除的持久化顺序并将其转为并行 I/O。
  - Persistent Memory、Crash Consistency、Write Ordering、并行文件系统、ChimeraFS

- [Zeppelin: Balancing Variable-length Workloads in Data Parallel Large Model Training](https://dl.acm.org/doi/10.1145/3767295.3769369)
  - Peking University、ETH Zurich、CUHK、Shanghai AI Laboratory、MIT；Chang Chen、Tiancheng Chen、Jiangfei Duan、Qianchao Zhu、Zerui Wang、Qinghao Hu 等
  - Zeppelin 处理 data-parallel large-model training 中序列长度差异：hierarchical partition 在 batch/设备内重分序列，attention engine 对不同长度区域使用不同 parallel strategy，使计算均衡且控制额外通信。
  - 相较 padding 或仅按样本长度分桶，核心创新是层次化序列切分与 divergent attention parallelism 协同。
  - 大模型训练、Variable Length、Data Parallelism、Attention、负载均衡

- [Efficient and Adaptable Overlapping for Computation and Communication via Signaling and Reordering](https://dl.acm.org/doi/10.1145/3767295.3769370)
  - Tsinghua University、Peking University、Infinigence-AI、Shanghai Jiao Tong University；Ke Hong、Xiuhong Li、Minxu Liu、Qiuli Mao、Tianqi Wu、Zixiao Huang 等
  - FlashOverlap 将算子切成 tile，在 tile 完成时以 signal 启动对应通信，并通过 reordering 避免通信 kernel 与计算争同一资源；接口不绑定 collective 实现，最高获得 1.65 倍加速。
  - 相较 operator-level overlap 或强依赖特定通信库，核心创新是 tile-wise signaling、无干扰重排与通信无关性。
  - 分布式训练、Computation-Communication Overlap、Tile Scheduling、Signaling、GPU

- [MTTM: Dynamic Fast Memory Partitioning with Bandwidth Optimization for Multi-tenant Cloud](https://dl.acm.org/doi/10.1145/3767295.3769371)
  - KAIST；Changjun Lee、Sangjin Choi、Youngjin Kwon
  - MTTM 在 multi-tenant cloud 中按 workload 的 DRAM sensitivity 分配有限 fast memory，并同时监控 bandwidth；当远端/慢层请求拥塞或被拒时动态重划本地 DRAM，而非只按容量/热页比例分层。
  - 相较 per-tenant 固定配额，核心创新是容量与带宽联合感知的动态 fast-memory partition。
  - Tiered Memory、多租户、DRAM Sensitivity、带宽优化、内存分配

- [BASK: Batch And SmartNIC-offloaded KSM](https://dl.acm.org/doi/10.1145/3767295.3769372)
  - KAIST；Chanshin Kwak、Jaehyeon Lee、Minkyu Jung、Changjun Lee、Youngjin Kwon
  - BASK 将 Kernel Same-page Merging 的扫描/比较批量 offload 到 SmartNIC；host 与 NIC 以 optimistic transaction 和 shadow metadata 协调页状态，批次自包含执行，减少逐页 PCIe 往返并保证并发正确性。
  - 相较 CPU KSM 或细粒度 NIC RPC，核心创新是带影子元数据的事务式批量去重 offload。
  - 内存去重、KSM、SmartNIC、Optimistic Concurrency、批处理

- [CSnake: Detecting Self-Sustaining Cascading Failure via Causal Stitching of Fault Propagations](https://dl.acm.org/doi/10.1145/3767295.3769373)
  - Purdue University；Shangshu Qian、Lin Tan、Yongle Zhang
  - CSnake 寻找单次故障结束后仍会自行传播的 cascading failure：它从不同 test workload 的单故障 trace 提取因果片段，再用 causal stitching 组合成可执行注入链，模拟现实中多阶段传播。
  - 相较同时盲目注入多故障，核心创新是按因果前置条件拼接已观测 fault propagation，系统生成复杂级联。
  - 分布式系统可靠性、Cascading Failure、Fault Injection、Causal Stitching、故障测试

- [Demystifying Serverless Costs on Public Platforms: Bridging Billing, Architecture, and OS Scheduling](https://dl.acm.org/doi/10.1145/3767295.3769374)
  - University of British Columbia、Johns Hopkins University；Changyuan Lin、Yuanzhi Ma、Mohammad Shahrad
  - 该研究把 public serverless 的 billing unit 与底层 architecture/OS scheduling 对齐分析，量化实际 CPU/memory 使用和账单资源；发现部分平台计费可达真实消耗 4.35 倍，并解释隔离、调度与定价原因。
  - 相较只比较 provider price table，核心贡献是用实测将费用膨胀归因到资源粒度和 OS scheduling。
  - Serverless Cost、Cloud Billing、OS Scheduling、资源计量、生产测量

- [E-Cube: Event Enhanced Efficient Video Streaming for Drones](https://dl.acm.org/doi/10.1145/3767295.3769375)
  - The University of Hong Kong、University of Pittsburgh、Tsinghua University；Jingao Xu、Longfei Shangguan、Danyang Li、Yunhao Liu、Zheng Yang
  - E-Cube 为 drone video streaming 同时利用 frame event/运动信息与编码器状态，只传对任务/画质有价值的区域或帧，并按链路/电量调码；H.265/AV1 省带宽 35% 以上、能耗 12% 以上，H.266 省 47%。
  - 相较统一压缩整帧，核心创新是 event-enhanced content selection 与传输/编码联合控制。
  - 无人机视频、Event Camera、Streaming、带宽优化、移动能耗

- [MinatoLoader: Accelerating Machine Learning Training Through Efficient Data Preprocessing](https://dl.acm.org/doi/10.1145/3767295.3769376)
  - McGill University, Canada、INESC TEC & University of Minho, Portugal；Rahma Nouaji、Stella Bitchebe、Ricardo Macedo、Oana Balmau
  - MinatoLoader 加速 PyTorch 单机多 GPU training data pipeline，重排 decode/transform/batch 的 CPU 并行与缓存，避免 loader process 重复预处理和 GPU starvation，同时保持样本语义与收敛。
  - 相较通用 DataLoader 仅增加 worker，核心创新是围绕多 GPU 消费节奏的共享、流水化预处理 runtime。
  - Training Data Pipeline、PyTorch、DataLoader、多 GPU、GPU 利用率

- [In-Production Characterization of an Open Source Serverless Platform and New Scaling Strategies](https://dl.acm.org/doi/10.1145/3767295.3769377)
  - University of British Columbia、IBM；Nima Nasiri、Nalin Munshi、Simon D Moser、Marius Pirvu、Vijay Sundaresan、Daryl Maier 等
  - 该工作用毫秒级到达、pod concurrency 与 minimum-scale 配置的大规模生产 trace 刻画开源 serverless 平台，再据此设计 FeMux，在 pod lifetime、multiplexing 和 scaling 间联合管理。
  - 相较只研究闭源云或粗粒度 invocation trace，核心创新是带用户配置的开源生产证据与 trace-driven lifetime controller。
  - Serverless、Production Trace、Pod Scaling、FeMux、工作负载刻画

- [Matrix‑PIC: Harnessing Matrix Outer-product for High‑Performance Particle‑in‑Cell Simulations](https://dl.acm.org/doi/10.1145/3767295.3769378)
  - Sun Yat-sen University；Yizhuo Rao、Xingjian Cui、Jiabin Xie、Shangzhi Pang、Guangnan Feng、Jinhui Wei 等
  - MatrixPIC 针对现代 CPU 的 MPU/VPU 混合 SIMD，将 particle-in-cell deposition 重写为 matrix outer product，并共同设计 data layout 与 incremental sorting，使粒子按 cell 聚集、向量单元连续执行。
  - 相较仅向量化单个 deposition loop，核心创新是算法、布局和排序的整体 co-design 来匹配矩阵/向量执行。
  - Particle-in-Cell、CPU SIMD、Matrix Outer Product、Data Layout、HPC

- [FlashPS: Efficient Generative Image Editing with Mask-aware Caching and Scheduling](https://dl.acm.org/doi/10.1145/3767295.3769379)
  - Hong Kong University of Science and Technology、Alibaba Group；Xiaoxiao Jiang、Suyi Li、Lingyun Yang、Tianyu Feng、Zhipeng Di、Weiyi Lu 等
  - FlashPS 服务 generative image editing，利用 mask 外区域不变这一结构，在 diffusion step/请求间缓存未修改区域的中间结果；scheduler 按 mask overlap、cache hit 和 GPU batch 组合编辑请求。
  - 相较把每次编辑当完整 text-to-image diffusion，核心创新是 mask-aware partial recomputation 与 cache-aware scheduling。
  - 生成式图像编辑、Diffusion Serving、Mask-aware Cache、调度、Partial Recompute

- [Neuro-C: Neural Inference Shaped by Hardware Limits](https://dl.acm.org/doi/10.1145/3767295.3769380)
  - Uppsala University, Sweden; RISE, Sweden、Politecnico di Milano, Italy; RISE, Sweden; Uppsala University, Sweden；Diletta Romano、Luca Mottola、Thiemo Voigt
  - Neuro-C 从硬件能高效实现的低位/ternary primitive 出发约束网络训练与表示，使模型在相同结构下比传统 ternary network 更易收敛、精度更高，而 inference latency 几乎不变。
  - 相较先训练模型再量化，核心创新是让 neural architecture/optimization 从一开始由硬件限制塑形。
  - Hardware-aware ML、Ternary Network、低比特推理、模型—硬件协同、边缘 AI

- [Practical and Scalable RDMA Connection Sharing for HPC Workload](https://dl.acm.org/doi/10.1145/3767295.3769381)
  - Peking University、Huawei Technologies Co., Ltd.、Grace；Yuejie Wang、Tuo Fang、Biyu Peng、Yang Cheng、Xin Sun、Chengchao Xu 等
  - 该框架让大量 HPC process 共享少量 RDMA connection：hardware-assisted data plane 保持消息 fast path 无额外复制/查表，细粒度 control plane 按 job/peer 创建映射和隔离，避免 QP 数量爆炸。
  - 相较每对进程独占 QP 或软件 multiplexing，核心创新是零常态成本的数据面共享加轻量连接控制。
  - RDMA、Connection Sharing、HPC、Queue Pair、可扩展网络

- [Scaling LLM Test-Time Compute with Mobile NPU on Smartphones](https://dl.acm.org/doi/10.1145/3767295.3769382)
  - Tsinghua University、University of Science and Technology of China、Microsoft Research、Institute for AI Industry Research (AIR), Tsinghua University；Zixu Hao、Jianyu Wei、Tuowei Wang、Minxing Huang、Huiqiang Jiang、Shiqi Jiang 等
  - 该端侧系统在 Snapdragon NPU 上让小 LLM 做多轮/多候选 test-time compute，管理 KV、batch 和 NPU memory，使额外推理预算可扩展；小模型借此达到或超过大模型准确率，形成新的性能—成本前沿。
  - 相较手机只做单次 greedy inference 或把 test-time scaling 放云端，核心创新是面向 NPU 的端到端推理时扩展 runtime。
  - Mobile LLM、Test-time Compute、NPU、端侧推理、性能—精度权衡

- [Garen: Reliable Cluster Management with Atomic State Reconciliation](https://dl.acm.org/doi/10.1145/3767295.3769383)
  - FriendliAI、Samsung Advanced Institute of Technology、POSTECH、FriendliAI, Seoul National University；Mingi Kim、Ahnjae Shin、Jaewoo Maeng、Myeongjae Jeon、Byung-Gon Chun
  - Garen 为 Kubernetes 式 cluster manager 提供 atomic state reconciliation：controller 对期望状态的一组相关写入作为原子单元发布，失败/重试不会让其他 controller 看到半完成状态，并在高 API rate/大集群保持扩展。
  - 相较 eventual reconciliation 暴露瞬时不一致，核心创新是为控制面 reconcile loop 增加事务化可见性边界。
  - Cluster Management、Atomic Reconciliation、控制面、一致性、Kubernetes

- [ASIC-based Compression Accelerators for Storage Systems: Design, Placement, and Profiling Insights](https://dl.acm.org/doi/10.1145/3767295.3769384)
  - DapuStor Corporation；Tao Lu、Jiapin Wang、Yelin Shan、Xiangping Zhang、Xiang Chen
  - 该工作设计 in-storage ASIC compression/decompression unit，并与 Intel QAT 两代对比；端到端实验系统分析 accelerator 放在 host、链路或设备内时的带宽/延迟，以及 data pattern/layout 对压缩收益的影响。
  - 相较只比较压缩 kernel 吞吐，核心贡献是将芯片设计、物理 placement、互连和真实存储 pipeline 一起评估。
  - 存储压缩、ASIC、In-storage Acceleration、QAT、软硬件放置

- [ECCB: Boosting Block Propagation of Blockchain with Erasure-Coded Compact Block](https://dl.acm.org/doi/10.1145/3767295.3769385)
  - Huazhong University of Science and Technology、Department of Computer Science and Engineering, The University of Texas at Arlington；Bingyi Cai、Shenggang Wan、Hong Jiang
  - ECCB 利用不同 blockchain node mempool 中交易高度重叠：发送 compact block 时对缺失交易做 erasure coding，接收方可用本地交易加少量编码片恢复完整 block，跨三洲提升传播。
  - 相较逐项请求 missing transaction，核心创新是把已观测 transaction redundancy 转成一次可恢复的编码传输。
  - Blockchain、Block Propagation、Erasure Coding、Compact Block、跨地域网络

- [Not A DPU in Name Only! Unleashing RDMA-capable DPUs in Multi-Tenant Serverless Clouds with NADINO](https://dl.acm.org/doi/10.1145/3767295.3769386)
  - University of Kentucky、University of California, Riverside、Hewlett Packard Enterprise Labs、Hewlett Packard Labs；Shixiong Qi、Songyu Zhang、K. K. Ramakrishnan、Diman Zad Tootaghaj、Hardik Soni、Puneet Sharma
  - NADINO 将 multi-tenant serverless 的数据面放到 RDMA-capable DPU，函数间传输绕过 host CPU、实现 zero-copy；系统比较并选择适合短生命周期/多租户的 RDMA primitive，同时隔离 tenant state。
  - 相较把 DPU 只当 SmartNIC 做封包，核心创新是 DPU-centric serverless runtime 与面向函数通信的 RDMA primitive 取舍。
  - DPU、Serverless、RDMA、Zero-copy、多租户数据面

- [Fix: externalizing network I/O in serverless computing](https://dl.acm.org/doi/10.1145/3767295.3769387)
  - Stanford University；Yuhan Deng、Akshay Srivatsan、Sebastian Ingino、Francis Chua、Yasmine Mitchell、Matthew Vilaysack 等
  - Fix 让 user、program 与 serverless platform 共享同一种“确定过程+明确输入/上游输出”表示；应用声明每阶段所需数据，所有 network I/O 由平台外置执行，从而联合安排 task 与 transfer、避免 starvation。
  - 相较应用内部自行发网络请求、云只能按执行时间计费，核心创新是 externalized I/O 和结果导向的可调度 computation contract。
  - Serverless、Externalized I/O、Declarative Computation、数据传输调度、Pay-for-results

- [ColdCode: Cold Data Encoding for Enhanced Reliability and Lifetime in 3D NAND Flash](https://dl.acm.org/doi/10.1145/3767295.3769388)
  - Mohamed bin Zayed University of Artificial Intelligence、Xiamen University、McGill University、Peking University；Qiao Li、Shangyu Wu、Zheng Wan、Yufei Cui、Jie Zhang、Chun Jason Xue
  - ColdCode 研究 8 种 3D NAND 后发现传统 randomizer 会抹掉某些天然低 raw-bit-error pattern；它为冷数据选择/编码成更可靠的 bit pattern，替代统一随机化以延长寿命。
  - 相较仅依赖 ECC 和 wear leveling，核心创新是将数据模式本身作为冷存储可靠性控制维度。
  - 3D NAND、Cold Data、Data Encoding、Raw Bit Error、Flash Lifetime

- [Efficient Multimodal Serving via Module Multiplexing](https://dl.acm.org/doi/10.1145/3767295.3769389)
  - Hong Kong University of Science and Technology、Sun Yat-sen University、Xi'an Jiaotong University、MetaX；Zicong Hong、Yuyan Chen、Haoyue Zhang、Peng Li、Wuhui Chen、Song Guo 等
  - Eevee 将 multimodal model 拆成可复用 encoder/projector/LLM module，来自不同模型/请求的相同或兼容模块在 GPU 上 multiplex、分别 batch 和调度，提升吞吐与利用率。
  - 相较整模型为单位的 replica/batching，核心创新是 module multiplexing，使共享粒度下沉到多模态流水组件。
  - Multimodal Serving、Module Multiplexing、GPU Sharing、模型组件、Batching

- [CHARM: Chiplet Heterogeneity-Aware Runtime Mapping System](https://dl.acm.org/doi/10.1145/3767295.3769390)
  - Imperial College London、Aalto University、TU Munich；Alessandro Fogli、Bo Zhao、Peter Pietzuch、Jana Giceva
  - CHARM 面向异构 chiplet CPU，用带独立 stack/state 的 user-level task 加 coroutine 式轻量切换；runtime 根据 chiplet 能力/数据位置把 task 映射到合适 core，并细粒度迁移。
  - 相较 OS thread 固定映射或无状态 coroutine，核心创新是同时保留可调度 task state 与低开销协作切换的 chiplet-aware runtime。
  - Chiplet CPU、Runtime Mapping、User-level Thread、Coroutine、异构核

- [2DIO: Configurable and Cache-Accurate Trace Generation for Storage Benchmarking](https://dl.acm.org/doi/10.1145/3767295.3769391)
  - Northeastern University；Yirong Wang、Isaac Khor、Peter Desnoyers
  - 2DIO 生成 storage benchmark trace 时同时控制 I/O request 分布和 cache reuse/working-set 行为，可在一条连续轴上合成不同 what-if cache hit pattern，并高精度复现真实 trace。
  - 相较只匹配请求大小/顺序，核心创新是把 cache behavior 作为独立可配置维度纳入 trace generation。
  - 存储基准、Trace Generation、Cache Accuracy、What-if Analysis、I/O Workload

- [Automated End-to-End Model Serving with Cooperative Compilation and Scheduling](https://dl.acm.org/doi/10.1145/3767295.3769392)
  - Nanjing University、Hunan University；Yikang Zhang、Junlong Chen、Wei Wang、Jia Liu、Nan Hu、Haipeng Dai
  - Infera 在 compile time 为模型生成适合不同 batch/shape/resource 的多个 kernel variant，serving runtime 再按实时 context 选择、组合和调度；编译器与 scheduler 共享性能信息而非各自局部优化。
  - 相较只部署单一最优 kernel 或 runtime 黑盒调度，核心创新是多版本编译与在线 scheduling cooperative co-design。
  - Model Serving、Cooperative Compilation、Kernel Variant、Runtime Scheduling、端到端优化

- [PiLLM: Resource-Efficient LLM Inference Using Workload Prediction](https://dl.acm.org/doi/10.1145/3767295.3769393)
  - ShanghaiTech University、SenseTime、Beihang University；Yunqian Fan、Shihao Bai、Ruihao Gong、Zaijun Wang、Rui Fan
  - PiLLM 预测近期 LLM 请求的长度、到达与资源需求，提前调整 GPU/CPU/replica/batch 等资源，在变化负载下减少闲置和临时扩容延迟，同时守住 SLO。
  - 相较对 queue length 被动扩缩，核心创新是把可预测 workload structure 转成前瞻性 resource allocation。
  - LLM Inference、Workload Prediction、动态资源分配、SLO、资源效率

- [MegaScale-Data: Scaling DataLoader for Multisource Large Foundation Model Training](https://dl.acm.org/doi/10.1145/3767295.3803568)
  - The University of Hong Kong、ByteDance Inc.、ByteDance；Juntao Zhao、Qi Lu、Wei Jia、Borui Wan、Lei Zuo、Junda Feng 等
  - MegaScale-Data 为多来源 foundation-model training 解耦数据预处理：Source Loader 只读取/解析源数据，Data Constructor 按训练任务组合样本，消除不同 parallel worker 的重复访问并支持多源比例动态变化。
  - 相较每个 trainer 独立执行完整 DataLoader，核心创新是 role-specific actor 的 disaggregated preprocessing architecture。
  - Foundation Model Training、Data Pipeline、多源数据、Disaggregated Preprocessing、生产系统

- [CofferOS: Hardening OS-level Virtualization with Rust](https://dl.acm.org/doi/10.1145/3767295.3803569)
  - KAIST、School of Computing, KAIST、University of Illinois Urbana-Champaign、FuriosaAI；Minkyu Jung、Chanshin Kwak、Junho Ahn、Sunho Park、Changjun Lee、Jongyul Kim 等
  - CofferOS 用 Rust 重写/重构 OS-level virtualization kernel，把 container namespace/resource/isolation primitive 放入类型与所有权约束，性能接近 Linux container，同时缩小故障传播和可定制安全边界。
  - 相较共享复杂 Linux kernel，核心创新是以 memory-safe language 构建仍兼容容器效率的专用虚拟化内核。
  - OS-level Virtualization、Rust、安全内核、Container、故障隔离

- [High Throughput and Low Latency LLM Serving via Adaptive KV Caching](https://dl.acm.org/doi/10.1145/3767295.3803570)
  - University of Macau; Shenzhen Institute of Advanced Technology, CAS、Nanyang Technological University、University of Macau、Shenzhen Institutes of Advanced Technology, Chinese Academy of Sciences；Wenyan Chen、Chengzhi Lu、Huanle Xu、Kejiang Ye、ChengZhong Xu
  - eLLM 在请求/token 粒度自适应决定 KV 保留、压缩/迁移和复用，并将 KV communication 与 GPU compute 重叠、融合互补资源 kernel，在高并发下兼顾吞吐和 tail latency。
  - 相较固定 KV cache policy，核心创新是 fine-grained adaptive caching 与通信—计算—kernel 三者协同。
  - LLM Serving、Adaptive KV Cache、通信重叠、Kernel Fusion、吞吐—延迟

- [Arena: Efficiently Training Large Models via Dynamic Scheduling and Adaptive Parallelism Co-Design](https://dl.acm.org/doi/10.1145/3767295.3803571)
  - Shanghai Jiao Tong University、Lenovo Research、Microsoft、Guizhou University、National University of Singapore；Chunyu Xue、Weihao Cui、Quan Chen、Chen Chen、Han Zhao、Shulai Zhang 等
  - Arena 对大模型 training job 联合决定何时/在哪些异构资源运行和采用何种 parallelism；profiler 建性能模型，scheduler 处理弹性/异构，adaptive-parallelism engine 在剪枝空间快速重配。
  - 相较 cluster scheduler 与自动并行器分离，核心创新是 dynamic scheduling–parallelism co-design。
  - 大模型训练、Cluster Scheduling、Adaptive Parallelism、异构 GPU、弹性

- [On-device Semantic Selection Made Low Latency and Memory Efficient with Monolithic Forwarding](https://dl.acm.org/doi/10.1145/3767295.3803572)
  - Shanghai Jiao Tong University、Huawei；Jiahao Zhou、Chengliang Lin、Dingji Li、Mingkai Dong、Haibo Chen
  - Prism 在端侧 semantic selection 中用 progressive cluster pruning 逐层淘汰不相关候选，并把模型 layer 从存储流式载入、chunk 执行与 I/O overlap，从而同时限制峰值内存和延迟。
  - 相较完整加载模型后一次性向量检索，核心创新是 monolithic forwarding 中的渐进剪枝与 layer streaming。
  - On-device Semantic Selection、内存受限推理、Progressive Pruning、Layer Streaming、边缘 AI

- [MesaFS: An I/O-Efficient Metadata Service for Distributed File Systems](https://dl.acm.org/doi/10.1145/3767295.3803573)
  - Tsinghua University；Hao Guo、Jiwu Shu、Youyou Lu
  - MesaFS 的 distributed filesystem metadata service 用 semi-ordered layout 只维持操作所需的局部次序，大多数 metadata update 只写一次 SSD，避免维护 total order 带来的额外 write amplification。
  - 相较全局排序的 LSM/B-tree metadata，核心创新是以文件系统语义确定必要顺序、其余保持半有序。
  - 分布式文件系统、Metadata Service、SSD Write、Semi-ordered Layout、I/O Efficiency

- [Practical and Efficient x86-64 Emulation on RISC-V](https://dl.acm.org/doi/10.1145/3767295.3803574)
  - Tsinghua Shenzhen International Graduate School, Tsinghua University、Institute of Software, Chinese Academy of Sciences、College of Computer Science, Chongqing University、Department of Computer Science, Tsinghua University、Tsinghua University；Xiongchuan Tan、Yang Liu、Sebastien Chevalier、Yangyu Chen、Xiaoyi Liu、Haohuan Fu
  - 该工作扩展 Box64 在 RISC-V 上执行 x86-64 binary，组合通用 dynamic binary translation 与 RISC-V 指令/寄存器/内存模型特化，覆盖复杂应用并降低 translation overhead。
  - 相较只追求 ISA 正确性的 emulator，核心创新是面向 RISC-V 的多层优化同时维持广泛 x86-64 compatibility。
  - Binary Translation、x86-64、RISC-V、Emulation、应用兼容

- [RaidenSwap: A Multi-Swap Remote System for Multi-core Applications](https://dl.acm.org/doi/10.1145/3767295.3803575)
  - SKLP, Institute of Computing Technology, CAS; University of Chinese Academy of Sciences、Huawei、Shandong University；Kefan Liu、Ke Liu、Xu Zhang、Hui Yuan、Xiaolong Zheng、Ning Liu 等
  - RaidenSwap 重做 multi-core application 的 remote swap path，让多个 swap queue/connection 并行处理 page-in/out，并减少 kernel critical section/请求串行；吞吐提升 1.8–16.5 倍、远端访问延迟降 70%。
  - 相较单一 swap backend/队列，核心创新是与多核并发匹配的 multi-swap architecture 和高效内核路径。
  - Remote Memory、Swap、多核、Page-in/out、内核内存管理

- [From Imperative to Declarative: Towards LLM-friendly OS Interfaces for Boosted Computer-Use Agents](https://dl.acm.org/doi/10.1145/3767295.3803576)
  - Key Laboratory of System Software (Chinese Academy of Sciences); Institute of Software, Chinese Academy of Sciences; University of Chinese Academy of Sciences、Key Laboratory of System Software (Chinese Academy of Sciences); Institute of Software, Chinese Academy of Sciences、Key Laboratory of System Software (Chinese Academy of Sciences); Institute of Software, Chinese Academy of Sciences; Shanghai Jiao Tong University；Yuan Wang、Mingyu Li、Haibo Chen
  - DMI 为 computer-use Agent 把 GUI/OS 转成 access、state、observation 三类声明式 primitive：Agent 直接请求对象/操作和订阅结构化状态，不再主要依赖截图坐标与低级 mouse/keyboard sequence。
  - 相较在 imperative GUI 上逐步模仿人类操作，核心创新是 Agent-native declarative OS interface，减少感知歧义、动作长度和脆弱性。
  - Agent Infra、Computer-use Agent、OS Interface、Declarative API、GUI Automation

- [Proteus: Heterogeneous FPGA Virtualization](https://dl.acm.org/doi/10.1145/3767295.3803577)
  - Technical University of Munich、University of California, Los Angeles、Tokyo University of Science；Felix Gust、Shu Anzai、Charalampos Mainas、Atsushi Koshiba、Pramod Bhatotia
  - Proteus 在不同 vendor/architecture FPGA 之上提供统一 virtualization stack/API，按 off-chip memory 类型虚拟化分配 buffer，并由 performance-aware scheduler 把 bitstream/job 放到合适设备。
  - 相较每种 FPGA stack 暴露专有接口，核心创新是同时抽象计算、内存和调度差异的 heterogeneous FPGA virtualization。
  - FPGA Virtualization、异构加速器、统一 API、Memory Virtualization、调度

- [Mitigating CDN Cache Misses with Scheduling: An Origin Shield for Billion-QPS Social Platforms](https://dl.acm.org/doi/10.1145/3767295.3803578)
  - State Key Laboratory for Novel Software Technology, Nanjing University、School of Computer Science, Central China Normal University、Tencent；Zixuan Yang、Yimeng Xu、Jiaqi Zheng、Boxi Liu、Guihai Chen、Quan Xia 等
  - TritonFlow 服务 billion-QPS social CDN，在 origin shield 层稳定地把同一对象请求调到相同/兼容 cache 节点，减少调度抖动导致的非强制 miss；生产 trace 中抖动降 96%、回源流量降 35%。
  - 相较只扩 cache 或改 eviction，核心创新是从 request scheduling 侧维持 cache affinity 来抑制 miss。
  - CDN、Origin Shield、Cache Affinity、请求调度、Billion-QPS

- [Bridging the GPU Utilization Gap: Predictive Multi-Dimensional Resource Scheduling for AI Workloads](https://dl.acm.org/doi/10.1145/3767295.3803579)
  - Tsinghua University、Southeast University、Alibaba Group、Baihai、Shanghai Jiao Tong University；Yilei Lu、Dongbiao He、Teng Ma、Zhe Liu、Letian Ruan、Jinlei Jiang 等
  - Wind 预测 AI job 的 CPU、memory、GPU 多维需求，并用 Hilbert curve 将三维资源空间映射成保持邻近性的线性序，快速匹配形状互补的 job，减少 GPU 空闲但配套资源不足的碎片。
  - 相较只按 GPU 数装箱，核心创新是 workload prediction 与几何 locality-preserving multidimensional scheduling。
  - AI Cluster、GPU Utilization、多维资源、Hilbert Curve、预测调度

- [Laminar: A Scalable Asynchronous RL Post-Training Framework](https://dl.acm.org/doi/10.1145/3767295.3803580)
  - The University of Hong Kong、ByteDance、The Chinese University of Hong Kong、Bytedance、Shanghai Jiaotong University；Guangming Sheng、Yuxuan Tong、Borui Wan、Wang Zhang、Chaobo Jia、Xibin Wu 等
  - Laminar 将 RL post-training 的 rollout/训练完全异步解耦，用一层 relay worker 作为分布式 parameter service，局部传播版本而非所有 worker 等全局 update；吞吐最高提升 5.48 倍并缩短收敛时间。
  - 相较同步迭代或 trainer 直接广播全部 rollout worker，核心创新是 relay-tier 参数传播消除全局 barrier、隔离组件速度差。
  - RL Post-training、异步训练、Parameter Service、Rollout、系统解耦

- [PARD: Enhancing Goodput for Inference Pipeline via Proactive Request Dropping](https://dl.acm.org/doi/10.1145/3767295.3803581)
  - Tianjin University、University of Texas at Dallas、Stevens Institue of Technology；Zhixin Zhao、Yitao Hu、Simin Chen、Mingfang Ji、Wei Yang、Yuhao Zhang 等
  - PARD 在多阶段 inference pipeline 中预测请求按当前进度是否已不可能满足 deadline，及时 proactive drop；若必须丢弃，再按剩余 latency budget 和实时 workload intensity 动态排序，保留最可能按时完成的请求。
  - 相较等 queue overflow 或超时末端才 drop，核心创新是 pipeline-state-aware 的 drop timing 与 request selection 分离。
  - 推理 Pipeline、Goodput、Proactive Dropping、Deadline、Admission Control

- [Fuzzing Enterprise-Grade Blockchain Systems: Industrial Practice and Solutions](https://dl.acm.org/doi/10.1145/3767295.3803582)
  - Tsinghua University、Beijing Academy of Blockchain and Edge Computing；Fuchen Ma、Yuanliang Chen、Zhen Yan、Yuanhang Zhou、Yu Jiang、Mingchao Wan
  - Thor 将企业级 blockchain 的节点、共识、存储和智能合约置于 system-level fuzzing 环境；两层并行方法一层扩展多节点/状态组合，另一层深入单执行路径，并处理长启动、昂贵重置和跨节点 oracle。
  - 相较只 fuzz 合约或单节点组件，核心贡献是可在工业区块链完整系统上运行的多层 fuzz workflow 与实践经验。
  - Blockchain Fuzzing、企业系统、System-level Testing、并行 Fuzz、工业实践

- [Digital Hole: Bypassing Commercial Audio DRM Solutions with DReaMcatcher](https://dl.acm.org/doi/10.1145/3767295.3803583)
  - Vrije Universiteit Amsterdam；Björn Ruytenberg、Mohammad Sina Karvandi、Herbert Bos、Erik van der Kouwe、Asia Slowinska
  - DReaMcatcher 分析商业流媒体 audio DRM 的受保护播放路径，在内容已解密供播放、但进入声卡前的数字链路截获无损样本，从 Netflix、Spotify 等服务导出保护歌曲。
  - 相较破解密钥或录制模拟输出，核心创新是定位通用的 post-decryption digital hole，并构造跨平台提取 proof-of-concept。
  - Audio DRM、Digital Hole、Content Protection、系统安全、流媒体

- [A Case for Elastic Quantum Error Correction Decoders](https://dl.acm.org/doi/10.1145/3767295.3803584)
  - University of Wisconsin-Madison；Satvik Maurya、Abtin Molavi、Aws Albarghouthi、Swamit Tannu
  - 该工作把 quantum error-correction decoder 视为由 quantum OS 管理的共享 accelerator：一级在多个 logical qubit/workload 间分配 decoder，二级按 syndrome burst 弹性扩缩，减少为峰值常驻的硬件。
  - 相较每个逻辑量子位独占固定 decoder，核心创新是两级共享/调度模型，使 fault-tolerant workload 的 decoder 需求降低 10%–40%。
  - Quantum OS、Error Correction Decoder、共享加速器、弹性调度、FTQC

- [EMVOD: Elastic Multi-Path QUIC Scheduling for CDN Video-on-Demand Service](https://dl.acm.org/doi/10.1145/3767295.3803585)
  - Tsinghua Shenzhen International Graduate School、Peng Cheng Laboratory、Tencent；ZiQi Wei、Qing Li、TianYun Zhao、Cheng Luo、ChangKui OuYang、XiaoFei Yu 等
  - EMVOD 只改 CDN edge，解析用户请求和播放 buffer，在 Wi-Fi 不稳时按需开启 cellular multipath QUIC；scheduler 以避免卡顿/首帧慢为先，同时最小化蜂窝流量。
  - 相较始终双链路传输或依赖客户端改造，核心创新是 edge-only、按播放状态弹性启用的多路径调度。
  - CDN Video、Multipath QUIC、Cellular、QoE、边缘调度

- [TrustWeave: Integrity Measurement and Attestation For Multi-Cloud LLMs](https://dl.acm.org/doi/10.1145/3767295.3803586)
  - University of Connecticut、Independent Researcher、Tsinghua University；Jianchang Su、Wenhui Zhang、Yifan Zhang、Kexin Chu、Hao Guo、Youyou Lu 等
  - TrustWeave 为 multi-cloud LLM deployment 度量运行时软件/模型完整性，将 Linux IMA event 扩展写入 Intel TDX RTMR，并生成可跨云验证的 attestation chain，证明启动后加载的组件未被替换。
  - 相较只证明 VM 初始镜像，核心创新是把动态 runtime measurement 与 confidential-VM hardware register 连接到 LLM 服务供应链。
  - 多云 LLM、安全证明、Intel TDX、IMA、Runtime Attestation

- [MegaScale-Omni: A Hyper-Scale, Workload-Resilient System for MultiModal LLM Training in Production](https://dl.acm.org/doi/10.1145/3767295.3803587)
  - Shanghai Jiao Tong University、ByteDance Seed、Bytedance seed、Bytedance Seed；Chunyu Xue、Yangrui Chen、Jianyu Jiang、Ningxin Zheng、Junda Feng、Jingji Chen 等
  - MegaScale-Omni 面向生产 multimodal LLM training，把 variable-length encoder 与 LLM backbone 分离设计：encoder 使用长短序列并行和 multiplexing，backbone 使用完整 5D parallelism，再按通信拓扑统一布局。
  - 相较整模型套同一并行策略，核心创新是 encoder/LLM decoupled parallelism 与跨组件通信高效组合，抵抗多模态 workload 变化。
  - 多模态大模型训练、5D Parallelism、Variable Length、生产系统、通信优化

- [Enabling Packet Spraying over Commodity RNICs with In-Network Support](https://dl.acm.org/doi/10.1145/3767295.3803588)
  - Hong Kong University of Science and Technology；Xiangzhou Liu、Wenxue Li、Zihao Wang、Kai Chen
  - Themis 在 programmable switch 上维护极小 middleware state，对 commodity RNIC 发出的 reliable transport packet 做路径标记、重排/反馈协调，使同一 RDMA flow 可 packet spray 而不破坏 RNIC 可靠性，无需改 NIC。
  - 相较 flow-level ECMP 或修改 RDMA transport，核心创新是以 in-network shim 调和 packet spraying 与商用 RNIC 语义。
  - RDMA、Packet Spraying、Programmable Switch、Commodity RNIC、负载均衡

- [Wayfinder: Automated Operating System Specialization](https://dl.acm.org/doi/10.1145/3767295.3803589)
  - Lancaster University、Politehnica University of Bucharest、The University of Manchester、The University of British Columbia、NEC Laboratories Europe；Alexander Jung、Cezar Crăciunoiu、Nikolaos Karaolidis、Hugo Lefeuvre、Daniel Oñoro Rubio、Felipe Huici 等
  - Wayfinder 将 OS configuration knob、application workload 和可量化目标组成自动搜索问题，通过实验/模型选择 kernel feature、参数与专用化配置，可面向性能、资源或安全优化且不要求 OS 专家。
  - 相较手工裁剪 unikernel/OS config，核心创新是覆盖完整 OS 配置面的自动 specialization workflow。
  - OS Specialization、Auto-tuning、Kernel Configuration、应用专用化、自动搜索

- [HetAuto: Cross-Cluster Auto-Parallelism for Heterogeneous Distributed Training](https://dl.acm.org/doi/10.1145/3767295.3803590)
  - The University of Hong Kong、Meituan Corporation；Guicheng Qi、Junwei Su、Liqi Yang、Tao Li、Tingwen Xie、Yerui Sun 等
  - HetAuto 为跨 cluster、设备性能和网络差异明显的大模型训练自动选择跨域 placement 与 intra/inter-operator parallelism，以性能模型剪枝搜索，在搜索成本与计划质量间平衡；吞吐最多提升 1.57 倍。
  - 相较单集群同构 auto-parallelism，核心创新是把跨集群网络层级和异构 accelerator 一并纳入规划。
  - Cross-cluster Training、Auto-parallelism、异构 GPU、模型并行、搜索优化

- [Low-Compilation-Cost Register Allocation in LLVM-Based Binary Translation](https://dl.acm.org/doi/10.1145/3767295.3803591)
  - Lanzhou University、Tsinghua University、Lanzhou University / Tsinghua University；Xiangwei Meng、Chen Gao、Wei Li、Fengyuan Ren
  - LCCRA 针对 LLVM-based binary translator 中 guest physical register 被数组/内存语义掩盖的问题，在 IR 中恢复其显式寄存器含义，让标准 allocator 更快决定 live range 和 host register，降低 JIT compile cost。
  - 相较为翻译器重写专用 allocator，核心创新是语义恢复式 IR 变换，使主流 LLVM allocation 重新高效。
  - Binary Translation、LLVM、Register Allocation、Compilation Cost、IR

- [ECOTE: Priority-Aware Optical Restoration for WAN Traffic Engineering](https://dl.acm.org/doi/10.1145/3767295.3803592)
  - University of Toronto、Tsinghua University、Microsoft Research Asia、Tencent；Yiren Zhao、Kunling He、Zhiquan Wang、Ran Shu、Jilong Wang、Congcong Miao
  - ECOTE 为 WAN traffic engineering 在 optical failure 后按业务 priority 恢复 lightpath，目标直接最小化 revenue loss；专用 solver 在物理光层容量/可达约束下求最大可恢复容量和 flow mapping。
  - 相较所有流同权或 IP 层独立 reroute，核心创新是将业务优先级与光层 restoration 物理约束统一优化。
  - WAN Traffic Engineering、Optical Restoration、Priority、Revenue Loss、故障恢复

- [LCMP: Distributed Long-Haul Cost-Aware Multi-Path Routing for Inter-Datacenter RDMA Networks](https://dl.acm.org/doi/10.1145/3767295.3803593)
  - Beijing University of Posts and Telecommunications、Peking University、Tsinghua University；Dong-Yang Yu、Yuchao Zhang、Xiaodi Wang、Jun Wang、Wenfei Wu、Haipeng Yao 等
  - LCMP 为 inter-datacenter RDMA flow 在多条长途链路间分布式选路，同时考虑带宽价格、传播延迟和实时拥塞；端点/网络局部反馈调整 striping，避免中心控制器成为瓶颈。
  - 相较只选最低 RTT 或单一路径，核心创新是 long-haul cost-aware multipath 与 RDMA 拥塞响应结合。
  - Inter-DC RDMA、Multipath Routing、网络成本、拥塞响应、分布式路由

- [SmartNS: Enabling Line-rate and Flexible Network Stack with SmartNIC](https://dl.acm.org/doi/10.1145/3767295.3803594)
  - Zhejiang University、Alibaba Cloud、Alibaba Group；Xuzheng Chen、Jie Zhang、Baolin Zhu、Xueying Zhu、Zhongqing Chen、Ting Fu 等
  - SmartNS 在 SmartNIC 上提供可编程 transport 与 line-rate packet processing；TX 只 offload header、避免搬完整 payload，RX 用 in-cache processing 支持超过 NIC 内存的 working set，降低受限 memory bandwidth。
  - 相较完整协议栈硬件化或频繁访问 NIC DRAM，核心创新是 header-only TX 和 unlimited-working-set RX 的内存流量设计。
  - SmartNIC、Network Stack、Line Rate、Transport Programmability、内存带宽

- [Reducing the GPU Memory Bottleneck with Lossless Compression for ML](https://dl.acm.org/doi/10.1145/3767295.3803595)
  - University of Washington、University of Washington/Google、KAUST；Aditya Kamath、Arvind Krishnamurthy、Marco Canini、Simon Peter
  - Invariant Bit Packing 在一组 ML tensor 中找始终相同/可省略的 bit，只传变化部分；GPU decompressor 用 warp 并行、低开销 bit operation，并与 asynchronous PCIe transfer 重叠，缓解显存/链路带宽。
  - 相较通用无损压缩器，核心创新是利用 tensor bit-level invariant 并为 GPU 解压/传输路径共同设计。
  - GPU Memory、Lossless Compression、Tensor、PCIe、Bit Packing

- [Once Rolling Hashing is Enough: Exploiting Rolling Hash Reuse in Delta Compression](https://dl.acm.org/doi/10.1145/3767295.3803596)
  - Harbin Institute of Technology, Shenzhen；Haoliang Tan、Wenhao Ou、Xiangyu Zou、Cai Deng、Yanqi Pan、Hao Huang 等
  - FastDelta 在一份 base/container 上只计算一次 rolling hash，通过 sampling 将结果复用于多个 delta-compression target；embedding-style sampling 和 locality-aware container compression 控制采样造成的查找开销与压缩率损失。
  - 相较每对版本重复 rolling hash，核心创新是跨 delta 任务共享 hash computation。
  - Delta Compression、Rolling Hash、Hash Reuse、采样、存储去重

- [Accurate and Ultra-Fast Launch-Time Validation of Idempotency for GPU Kernels](https://dl.acm.org/doi/10.1145/3767295.3803597)
  - Shanghai Jiao Tong University、Shanghai JiaoTong University；Mingcong Han、Weihang Shen、Rong Chen、Haibo Chen
  - Picker 在 GPU kernel launch 时根据本次 pointer、shape、grid 等实例参数验证 idempotency，而非给 kernel 永久二分类；可重放实例用于低成本 checkpoint/preemption，使 checkpoint 开销低于 4%、抢占延迟降 84.2%。
  - 相较离线分析 kernel 或保守保存所有写集，核心创新是 ultra-fast instance-level launch-time validation。
  - GPU Kernel、Idempotency、Launch-time Analysis、Checkpoint、Preemption

- [Scalable RDMA-accelerated Distributed Locks with Shared Stream Abstraction](https://dl.acm.org/doi/10.1145/3767295.3803598)
  - Nanjing University of Aeronautics and Astronautics、Hohai University、Beihang University、State Key Laboratory for Novel Software Technology, Nanjing University；Miao Cai、Junru Shen、Xiaojian Liao、Rong Gu、Yanchao Zhao、Hao Han 等
  - StreamLock 用 shared stream 给 distributed lock request 排序：现代 NIC 的 line-rate receive path 形成可扩展顺序，owner 通过 peer-to-peer notification 在一个 RTT 内把锁直接交给下一请求者。
  - 相较中心 lock server 或 RDMA atomic 争抢，核心创新是将锁队列抽象成 NIC 加速共享流并直接传递 ownership。
  - Distributed Lock、RDMA、Shared Stream、NIC Ordering、One-RTT Handoff

- [TCO-driven Storage Provisioning for Exascale Data Centers](https://dl.acm.org/doi/10.1145/3767295.3803599)
  - Carnegie Mellon University、Google、Microsoft；Timothy Kim、Saurabh Kadekodi、Arif Merchant、Prashant Nema、Jai Menon、Rashmi Vinayak 等
  - 该工作建立覆盖 device 价格/寿命、能耗、冗余、性能和数据温度的 exascale storage TCO model，optimizer 决定 dataset 如何分组并放到不同 device type，寻找最低长期成本部署。
  - 相较按容量或峰值吞吐独立采购，核心贡献是 dataset-device assignment 的全生命周期 TCO 搜索及部署规律。
  - Exascale Storage、TCO、Storage Provisioning、Dataset Placement、容量规划

- [No More Translation at Runtime: LLM-Empowered Static Binary Translation](https://dl.acm.org/doi/10.1145/3767295.3803600)
  - The Hong Kong University of Science and Technology、Lingnan University；Zhibo Liu、Huaijin Wang、Wai Kin Wong、Daoyuan Wu、Shuai Wang
  - 该方案让 LLM 理解 guest assembly block、ABI 和控制流，辅助 ahead-of-time assembly-to-assembly translation，生成可独立运行的 AArch64 binary；运行时不再需要 DBT framework。
  - 相较运行时逐块翻译，核心创新是 LLM 辅助恢复静态翻译所需语义，再由传统工具验证/生成 native-like code，属于 LLM for Systems。
  - LLM for Systems、Static Binary Translation、AArch64、Assembly、Ahead-of-time

- [FicusDB: Scalable Multi-Versioned Authenticated Archival Storage](https://dl.acm.org/doi/10.1145/3767295.3803601)
  - Cornell University、UC Santa Barbara；Hongbo Zhang、Maofan "Ted" Yin、Robbert van Renesse
  - FicusDB 在不改变 blockchain authenticated-data-structure 接口的前提下重做持久层：append-only location ID 免 compaction，CoW-aware tree cache 避免 LRU 抖动，AHA 将 child hash 当可验证 hint；11.5M Ethereum block 上吞吐高 3.7 倍、空间小 66%。
  - 相较硬分叉更换 ADS，核心创新是从 log-structured persistence、cache 与 proof hint 三处优化既有 copy-on-write trie。
  - Blockchain Storage、Authenticated Data Structure、Archival Storage、Copy-on-write Trie、Integrity Proof

- [AEP: Achieving Hierarchical Fault Tolerance in DSM Through Atomic Execution Protection](https://dl.acm.org/doi/10.1145/3767295.3803602)
  - Huazhong University of Science and Technology、The University of Texas at Arlington；Zixuan Wang、Qi Wu、Hang Huang、Jia Rao、Hui Lu、Hao Fan 等
  - AEP 由 kernel 在 user-space critical operation 期间延迟 termination，保证该区域原子完成；AEP-DSM 用受保护的 node-local allocator 加跨节点协调，形成从节点故障到分布式内存的一层层容错。
  - 相较应用自行写 undo/redo 或让进程随时被杀，核心创新是 kernel-assisted atomic execution 作为可组合的 hierarchical fault-tolerance primitive。
  - Distributed Shared Memory、Atomic Execution、Kernel Assistance、Allocator、容错

- [HARP: Orchestrating Automated Parallel Training on Heterogeneous GPU Clusters](https://dl.acm.org/doi/10.1145/3767295.3803603)
  - Fudan University、Shandong Computer Science Center (National Supercomputer Center in Jinan)；Antian Liang、Zhigang Zhao、Kai Zhang、Xuri Shi、Chuantao Li、Chunxiao Wang 等
  - HARP 为 heterogeneous GPU cluster 自动规划大模型训练，公开实现包含 GPT 类 LLM 负载；细粒度搜索 inter-operator parallel strategy，并按设备算力/互连非均匀划分 load，减少通信同时保持 accelerator 平衡。
  - 相较同构假设或固定 3D parallel template，核心创新是专为异构集群设计的细粒度 planner 和执行编排。
  - 自动并行、异构 GPU、Inter-operator Parallelism、负载均衡、分布式训练
  - 公开实现与负载配置：[作者代码仓库](https://github.com/Lssyes/harp)。

- [swKokkos: An Athread Backend for Enhanced Kokkos with the Sunway Heterogeneous Architecture](https://dl.acm.org/doi/10.1145/3767295.3803604)
  - Computer Network Information Center, Chinese Academy of Science; Pengcheng Laboratory; University of Chinese Academy of Sciences、Computer Network Information Center, Chinese Academy of Sciences;University of Chinese Academy of Sciences、Computer Network Information Center, Chinese Academy of Science、Pengcheng Laboratory、Laoshan Laboratory；Junlin Wei、Jinrong Jiang、Wu Wang、Chen Li、Yehong Zhang、Yue Yu 等
  - swKokkos 为 Sunway many-core 增加 Athread backend：compile-time 注册 C++ template kernel、runtime callback 在 CPE 执行；向量 hash dispatch、tile task mapping 和快速 device scheduler 降低抽象开销，扩到 10 万核。
  - 相较手写 Sunway backend，核心创新是打通 template-heavy Kokkos 与 Athread 的注册/回调机制并保留性能可移植性。
  - HPC、Kokkos、Sunway、Performance Portability、Many-core Runtime

- [SwiftFL: Enabling Speculative Training for On-Device Federated Deep Learning](https://dl.acm.org/doi/10.1145/3767295.3803605)
  - State Key Laboratory of Information Security, Institute of Information Engineering, CAS and University of Chinese Academy of Sciences、None、Peking University、Institute of Information Engineering, CAS、State Key Laboratory of Cyberspace Security Defense, Institute of Information Engineering, CAS；Yuhui Zhang、Guang Yan、Xin Zhang、Zimu Guo、Lutan Zhao、Jiangfeng Cao 等
  - SwiftFL 遇到慢 client 时用预测 gradient 先更新 global model，让快 client speculative 进入下一轮；真实更新到达后 gradient compensation 修正误差，client selection 在 model drift 与训练效率间决定是否投机，平均加速 6.08 倍。
  - 相较同步等待或直接丢弃 straggler，核心创新是可补偿的 speculative federated training。
  - On-device Federated Learning、Speculative Training、Gradient Prediction、Straggler、Model Drift

- [Crimson: Collaborative Parameter Updates for Efficient Pipeline Training of Large Language Models](https://dl.acm.org/doi/10.1145/3767295.3803606)
  - Sun Yat-sen University、Hong Kong University of Science and Technology、Pengcheng Laboratory；Yapeng Jiang、Wuhui Chen、Ganhong Huang、Yuzhou Huang、Zicong Hong、Song Guo 等
  - Crimson 优化 pipeline-parallel LLM 的 parameter update：multi-stage collaborative optimizer 协调 optimizer compute 与通信，trapezoid-bubble-aware scheduler 根据各 stage 空闲窗口求最优更新拆分/放置。
  - 相较所有 stage 在 iteration 末统一更新，核心创新是把参数更新分布到 pipeline bubble 并跨 stage 协作。
  - LLM Training、Pipeline Parallelism、Parameter Update、Bubble Scheduling、Optimizer

- [Five Minutes of DDoS Brings down Tor: DDoS Attacks on the Tor Directory Protocol and Mitigations](https://dl.acm.org/doi/10.1145/3767295.3803607)
  - Purdue University、Supra Research / Purdue University；Zhongtang Luo、Jianting Zhang、Akshat Neerati、Aniket Kate
  - 该安全研究证明只需约五分钟 DDoS 多数 Tor directory authority，就能破坏客户端获得共识目录、使网络大范围不可用；并分析协议集中性和提出缓解。
  - 相较攻击 relay data plane，核心创新是针对短时 directory-control-plane quorum 的低成本可用性攻击。
  - Tor、DDoS、Directory Protocol、匿名网络、控制面安全

- [A Logically Disaggregated Cache for Replicated Storage Systems](https://dl.acm.org/doi/10.1145/3767295.3803608)
  - University of Illinois Urbana-Champaign、University of Illinois Urbana Champaign、Jump Trading Group；Kiran Hombal、Henry Zhu、Shreesha G. Bhat、Neil Kaushikkar、Ramnatthan Alagappan、Aishwarya Ganesan
  - Ldc 将 replicated storage 各副本内嵌 cache 逻辑聚合成一个逻辑 cache，任意 replica 可访问不同分片以减少重复；写入对象快速 demote，online analyzer 在 replica locality 与全局覆盖率间调节，YCSB 吞吐提升 2.6–5.4 倍。
  - 相较每副本独立 LRU，核心创新是保持物理 cache 就地但逻辑解耦管理，并在线控制冗余—覆盖取舍。
  - Replicated Storage、Logically Disaggregated Cache、Cache Redundancy、KV Store、在线分析

- [Everything You Need to Know About Virtual Machine Live Migration Between Heterogeneous Processors](https://dl.acm.org/doi/10.1145/3767295.3803609)
  - Université Grenoble Alpes、INRIA、University of Rennes, INRIA；Kenta Ishiguro、Fonyuy-Asheri Caleb、Elouan Barraud、Renaud Lachaize、Yérom-David Bromberg、Alain Tchana
  - MigCheck 不执行昂贵真实迁移，而模拟 source/destination processor 的 ISA feature、microarchitecture 和 VM workload，预测 heterogeneous CPU 间 live migration 是否可行及迁后性能/异常。
  - 相较只做 CPUID compatibility check，核心创新是面向半异构处理器的迁移 outcome simulation。
  - VM Live Migration、Heterogeneous CPU、Compatibility、Simulation、虚拟化

- [Million-Scale Text-to-Video Retrieval with Hyperdimensional Computing](https://dl.acm.org/doi/10.1145/3767295.3803610)
  - DGIST；Hyunsei Lee、Jaewoo Gwak、Shinhyoung Jang、Junyoung Lee、Yeseong Kim
  - 该系统把每个 video 编成 3072-bit hypervector，以 bit packing 压缩百万级索引；HVR inverted index 优先罕见、信息量高的 bit position，再用 GPU Hamming search 精排候选。
  - 相较保存浮点 embedding 并做 ANN，核心创新是 binary hyperdimensional representation 与 frequency-aware retrieval。
  - Text-to-Video Retrieval、Hyperdimensional Computing、Binary Embedding、Inverted Index、GPU Hamming

- [PointShuffler: Accelerating Point Cloud Neural Networks on General-Purpose GPUs](https://dl.acm.org/doi/10.1145/3767295.3803611)
  - School of Computer Science and Engineering, Central South University、College of Information Science and Engineering, Hunan University、School of Future Technology, South China University of Technology；Yangfan Li、Zhengjie Jin、Yue Tian、Mengquan Li、Fengxiao Tang、Ming Zhao 等
  - PointShuffler 为 point-cloud neural network 消除邻域/点特征处理的重复工作，并通过 GPU-friendly shuffle/layout 和融合 kernel 让不规则点云映射到连续 SIMT 执行，在保持精度下加速 inference。
  - 相较直接运行通用 PCNN operator，核心创新是围绕点云冗余重排数据和计算，而非修改模型输出。
  - Point Cloud Neural Network、GPU Inference、Data Shuffling、冗余消除、Kernel Fusion

- [TAO: Tolerance-Aware Optimistic Verification for Floating-Point Neural Networks](https://dl.acm.org/doi/10.1145/3767295.3803612)
  - Princeton University、The Hong Kong University of Science and Technology (Guangzhou)、University of Illinois Urbana-Champaign；Jianzhu Yao、Hongxu Su、Taobo Liao、Zerui Cheng、Huan Zhang、Xuechao Wang 等
  - TAO 验证 heterogeneous hardware 上 floating-point neural network output，不要求 bitwise equality；它为各 operator 建原则化 tolerance region，乐观接受在误差界内的结果，只对可疑执行走昂贵验证。
  - 相较精确重算/逐 bit 对比，核心创新是 tolerance-aware optimistic verification，将数值误差语义纳入可信判断。
  - Neural Network Verification、Floating Point、Tolerance、Optimistic Protocol、异构计算

- [Efficient ML Model Updates for Deeply Embedded Microcontrollers](https://dl.acm.org/doi/10.1145/3767295.3803613)
  - University of California, Berkeley、University of California, Los Angeles；Shishir G. Patil、Sam Kumar、Prabal Dutta、Joseph Gonzalez
  - Minerva 为深度嵌入式 MCU 的 ML model 做差分/组件级更新，只传和写入真正变化的权重与代码，并适配 flash 擦写/内存限制；较完整 firmware update 快最多 89 倍。
  - 相较通过 DFU 重刷整个 image，核心创新是面向模型结构的细粒度、资源安全更新路径。
  - TinyML、Model Update、Microcontroller、Delta Update、Embedded System

- [Proactive Change Risk Detection in Production Cloud Systems: ByteDance’s Experience](https://dl.acm.org/doi/10.1145/3767295.3803614)
  - ByteDance；Jinyang Liu、Yichen Li、Tieying Zhang、Binbin Chen、Xiao He、Zhihan Jiang 等
  - Aegis 从 ByteDance 历史 change、incident 和运营记录自动构建 knowledge base，将先例归纳为可解释 risk heuristic；新变更上线前检索相关 precedent、给出风险与证据，辅助 gate。
  - 相较黑盒 failure predictor，核心创新是 knowledge-driven、可追溯到历史案例的 production change assessment，属于知识增强运维而非 Agent 闭环。
  - Cloud Reliability、Change Risk、Knowledge Base、生产运维、可解释评估

- [Avicenna: Masking Slowdowns in Replicated State Machines with Counterfactual Evaluation](https://dl.acm.org/doi/10.1145/3767295.3803615)
  - Databricks、Princeton University、Datadog、Microsoft Research、Columbia University；Christopher Hodsdon、Zijian Qin、Khiem Ngo、Siddhartha Sen、Ethan Katz-Bassett、Wyatt Lloyd
  - Avicenna 为 geo-distributed replicated state machine 用 counterfactual evaluation 判断某 replica 若未 fail-slow 时本应何时响应，从而在不增加正常路径 RTT 的情况下屏蔽单个慢副本；正常延迟同 Multi-Paxos。
  - 相较固定 timeout 或永远走更大 quorum，核心创新是用反事实进度识别/绕过 slowdown。
  - Replicated State Machine、Fail-slow、Counterfactual Evaluation、Geo-distributed、Consensus

- [Yield Not Thy Core](https://dl.acm.org/doi/10.1145/3767295.3803616)
  - University of California, Santa Cruz、U. C. Santa Cruz、UC Santa Cruz、Yale University；Achilles Benetopoulos、Peter Alvaro、Andi Quinn、Robert Soule
  - Magpie 提供数据密集型 distributed programming model，保证局部写成的 fast code 分布后不会因隐式 serialization、copy 或 scheduler yield 丢失核心；runtime 明确管理 ownership、placement 和通信。
  - 相较高层分布式框架隐藏关键资源行为，核心创新是可组合的性能保证，使单机 fast path 在分布式执行中保持。
  - Distributed Runtime、Data-intensive Application、Programming Model、Performance Guarantee、资源所有权

- [Prediction-Informed Power Management for General-Purpose Compute Servers](https://dl.acm.org/doi/10.1145/3767295.3803617)
  - University of Washington；Jonggyu Park、Simon Peter、Thomas E. Anderson
  - PIP 先用 ML power model 预测不同 CPU throttling/configuration 对当前 workload 性能和功耗的反事实影响，再由控制环选择最大化 power-budget utilization 的配置，避免在线试错。
  - 相较温度/利用率阈值式 governor，核心创新是 prediction-informed action evaluation 后再执行。
  - Server Power Management、CPU Throttling、ML for Systems、预测控制、功率预算

- [NutCracker: A Compilation Framework for Hybrid DPU Architectures](https://dl.acm.org/doi/10.1145/3767295.3803618)
  - National University of Singapore、Max Planck Institute for Software Systems (MPI-SWS)；Yihan Yang、Haifeng Sun、Antoine Kaufmann、Jialin Li
  - NutCracker 为含 host core、on-path/off-path engine 的 hybrid DPU 编译 network/storage workload，自动划分 component、生成通信和同步；开发工作降近 90%，7 个 workload 性能距手写 3% 内。
  - 相较开发者手工为每种 DPU architecture 拆程序，核心创新是跨异构 DPU component 的统一 IR 与 partition/codegen。
  - DPU、Compiler、Hybrid Architecture、Program Partitioning、代码生成

- [viNPU: Optimizing Vision Transformer Inference on Mobile NPUs](https://dl.acm.org/doi/10.1145/3767295.3803619)
  - Yonsei University；Jeho Lee、Gunjoong Kim、Chanyoung Jung、Jaehee Kim、Seonghoon Park、Hojung Cha
  - viNPU 在 mobile NPU 上执行 ViT/VFM：sensitivity-guided mixed precision 平衡精度和延迟，dataflow transformation 提高 on-chip locality，离线 profiling 选择实时配置；商用设备平均加速 11.5 倍、能耗最多降 44.9 倍。
  - 相较把 GPU ViT kernel 直接移植 NPU，核心创新是量化、数据流与异构 compute-unit balance 的整体优化。
  - Vision Transformer、Mobile NPU、Mixed Precision、Dataflow、端侧推理

- [RoPeerTo: A Datacenter-Scale Architecture for Peer-To-Peer DMA between GPUs and FPGAs](https://dl.acm.org/doi/10.1145/3767295.3803620)
  - Politecnico di Milano、ETH Zurich、AMD Research and Advanced Development；Marco Venere、Giuseppe Sorrentino、Benjamin Ramhorst、Maximilian Jakob Heer、Lucian Petrica、Dario Korolija 等
  - RoPeerTo 为 datacenter 中 GPU 与 FPGA 提供跨 PCIe hierarchy 的 direct peer-to-peer DMA，统一发现、映射、权限与传输 API，屏蔽具体 root complex/IOMMU/设备栈并开源实现。
  - 相较经 host memory bounce 或厂商私有 P2P，核心创新是可管理、可移植的数据中心级 accelerator P2P architecture。
  - GPU-FPGA、Peer-to-peer DMA、PCIe、Accelerator Interconnect、开源系统

- [Accelerating Transactional Execution via Processing-In-Memory](https://dl.acm.org/doi/10.1145/3767295.3803621)
  - INESC-ID, IST, Universidade de Lisboa,；André Lopes、Daniel Castro、Paolo Romano
  - PIM-TIDE 把 transaction operator 放到多个 memory-side DPU 执行，轻量软件协议协调跨 DPU read/write set，只在必要时让 CPU 处理全局提交，保证 consistency、atomicity、isolation 并避免频繁 inter-DPU message。
  - 相较所有事务回 CPU 或每步跨 DPU 协调，核心创新是 selective CPU coordination 的 multi-DPU transaction execution。
  - Processing-in-Memory、Transaction、DPU、原子性、近数据计算

- [AIMS: Cost-Efficient LLM-Based Agent Deployment in Hybrid Cloud-Edge Environments](https://dl.acm.org/doi/10.1145/3767295.3803622)
  - University of Virginia、Microsoft；Shiyi Liu、Haiying Shen、Shuai Che、Mahdi Ghandi、Mingqin Li
  - AIMS 面向多步 LLM-based Agent，在每个 iteration/subtask 根据任务难度、上下文和成本选择本地 SLM 或云端 LLM；它不是一次给整个请求固定模型，SLM 使用率提高最多 31.4%且准确率最高相对增 27.5%。
  - 相较 HybridLLM 的请求级或静态路由，核心创新是 iteration-level adaptive model selection，直接利用 Agent workflow 的多步结构，属于 Agent Infra。
  - Agent Infra、Hybrid Cloud-Edge、Model Routing、SLM/LLM、Iteration-level Scheduling

- [Suika: Efficient and High-quality Re-scheduling of 3D-parallelized LLM Training Jobs in Shared Clusters](https://dl.acm.org/doi/10.1145/3767295.3803623)
  - Shanghai Jiao Tong University & Institute of Artificial Intelligence (TeleAI), China Telecom、Shanghai Jiao Tong University、Institute of Artificial Intelligence (TeleAI), China Telecom、Huawei Technologies Co., Ltd.；Yuxuan Wang、Yanbo Wang、Chen Chen、Chunyu Xue、Qizhen Weng、Yin Chen 等
  - Suika 在共享 cluster 中为 3D-parallel LLM job 增减/更换 GPU 时搜索新的 DP/TP/PP placement；device-to-device redeployment 只迁移增量 shard，并将旧/新布局的重叠转换并行执行以降低停顿。
  - 相较资源变化后整模型 checkpoint/reload，核心创新是高质量 re-planning 与增量 D2D reconfiguration 联合。
  - LLM Training、3D Parallelism、Rescheduling、D2D Redeployment、共享 GPU 集群

- [LifeFuzz: Lifecycle-Guided Fuzzing for Windows Driver Cross-Handler Vulnerabilities](https://dl.acm.org/doi/10.1145/3767295.3803624)
  - Institute of Information Engineering, Chinese Academy of Sciences and School of Cyber Security, University of Chinese Academy of Sciences、University of New South Wales、Chinese Academy of Sciences、Institute of Computing Technology, Chinese Academy of Sciences、Institute of Information Engineering, Chinese Academy of Sciences;University of Chinese Academy of Sciences；Chendong Yu、Yuekang Li、Yang Xiao、Jie Lu、Yeting Li、Defang Bo 等
  - LifeFuzz 为 Windows driver 建模跨 IOCTL handler 共享 global variable 的 lifecycle，按初始化—使用—释放依赖生成合法调用序列，从而触发单 handler fuzzing 漏掉的 use-after-free/state bug；漏洞多 357%。
  - 相较独立随机 fuzz 每个 IOCTL，核心创新是 lifecycle-guided、dependency-respecting cross-handler sequence。
  - Windows Driver、Lifecycle Fuzzing、IOCTL、Cross-handler Vulnerability、内核安全

- [Rose: Reproducing External-Fault-Induced Failures in Distributed Systems with Lightweight Instrumentation](https://dl.acm.org/doi/10.1145/3767295.3803625)
  - INESC-ID、IST Lisbon & INESC-ID、Purdue University；Sebastião Amaro、Miguel Matos、Pedro Fonseca
  - Rose 从 production trace 提取通过系统接口可观测的外部 fault effect，再系统生成 message loss/delay、process/network 等 fault schedule 重放目标 failure；只需轻量 instrumentation，不要求记录全部内部 nondeterminism。
  - 相较完整 record/replay 或人工猜注入时机，核心创新是利用 external-fault observability 从真实 trace 反推可复现 schedule。
  - 分布式系统、Failure Reproduction、External Fault、Production Trace、轻量插桩

- [Lessons Learned from Incorporating Formal Methods in Huawei Cloud Reliability](https://dl.acm.org/doi/10.1145/3767295.3803626)
  - Huawei Technologies Co., Ltd, Ireland、Huawei Technologies Co., Ltd., Shenzhen, Guangdong, China；Claudia Cauli、Timo Lang、Shuo Chen、Sebti Mouelhi、Xin Jin、Subhajit Bandopadhyay 等
  - 华为云经验报告比较三种形式化投入层级，在数据库与网络基础服务中分别采用 probabilistic concurrency testing、model checking 和 deductive verification，说明如何按风险、团队能力和维护成本选择保证。
  - 相较只展示单个 verified prototype，核心贡献是生产组织中多种形式化方法的成本—保证权衡、落地流程与教训。
  - 工业形式化方法、Cloud Reliability、Concurrency Testing、Model Checking、Deductive Verification
