# ICDCS 2025 论文列表

ICDCS 2025 主会 Regular/Main Technical Sessions 共收录 103 篇研究论文；已排除 workshop、poster、demo、doctoral consortium 和 industry event。标题链接指向 DOI/IEEE 文章页（无 DOI 的少数 2026 议程论文链至官方主会程序）；已找到的 2 份合法公开 PDF 保存在 `reference/ICDCS/2025/`。

- [Weighted Monitoring Interval Minimization for Disaster Surveillance with a UAV](https://doi.org/10.1109/icdcs63083.2025.00112)
  - Wenzheng Xu, Yunrui Cao, Dandan Huang, Weifa Liang, Jianwei Zhang, Tang Liu, Jian Peng, Xiaohua Jia, Zichuan Xu；Sichuan University,College of Computer Science,Chengdu,P. R. China; The Hong Kong Polytechnic University,Department of Computing,Hong Kong,P. R. China; Sichuan Normal University,College of Computer Science,Chengdu,P. R. China; Dalian University of Technology,School of Software,Dalian,P. R. China。
  - 该工作研究移动计算中的「无人机灾害监测的加权监测间隔最小化」：将终端位置/移动、传感数据、链路和能量状态一起带入感知、通信或计算决策。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「无人机灾害监测的加权监测间隔最小化」中的特定状态、约束或操作变成一级设计对象。
  - Mobile/Space Networks, Mobile Computing, Distributed Systems

- [Spacker: Unified State Migration for Distributed Streaming](https://doi.org/10.1109/icdcs63083.2025.00101)
  - Yancan Mao, Shuhao Zhang, Richard T. B. Ma；National University of Singapore,School of Computing; Huazhong University of Science and Technology,School of Computer Science and Technology。
  - Spacker研究大数据系统中的「Spacker：分布式流媒体的统一状态迁移」：以持续到达的 record、operator state 和 partition 为单位，组织计算、状态迁移与故障恢复。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较把相互影响的子问题分开优化，核心创新是在同一目标下联合决定原本分离的放置、调度、通信或保护策略。
  - Stream Processing, Big Data, Distributed Systems

- [LLMSched: Uncertainty-Aware Workload Scheduling for Compound LLM Applications](https://doi.org/10.1109/icdcs63083.2025.00058)
  - Botao Zhu, Chen Chen, Xiaoyi Fan, Yifei Zhu；Shanghai Jiao Tong University,UM-SJTU Joint Institute,China; Shanghai Jiao Tong University,John Hopcroft Center for Computer Science,China; Jiangxing Intelligence Inc.,Shenzhen,China。
  - LLMSched 服务的是由多次 LLM 调用、API 和其他外部模块组成的 compound LLM DAG，调度粒度是单个应用请求及其内部 stage。它用 Bayesian network 根据已执行 stage 更新后续时长/分支的不确定性，以熵识别最能消除不确定性的 stage，再与缩短 JCT 的优先级结合排队。
  - 相较把 LLM workflow 当作已知时长的静态 DAG，核心创新是把执行中才逐渐显现的结构和时长不确定性变成显式调度信号。
  - Agent Infra, Compound LLM Applications, DAG Scheduling, Bayesian Network, Uncertainty-aware Scheduling

- [NeRFlex: Resource-aware Real-time High-quality Rendering of Complex Scenes on Mobile Devices](https://doi.org/10.1109/icdcs63083.2025.00067)
  - Zhe Wang, Yifei Zhu；Shanghai Jiao Tong University,UM-SJTU Joint Institute,Shanghai,China。
  - NeRFlex研究边缘计算中的「NeRFlex：移动设备上复杂场景的资源感知实时高质量渲染」：将终端位置/移动、传感数据、链路和能量状态一起带入感知、通信或计算决策。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - Edge Computing, Distributed Systems

- [Communication-Efficient MoE Fine-Tuning with Locality-Aware Expert Placement](https://doi.org/10.1109/icdcs63083.2025.00025)
  - Chenghao Hu, Yufei Kang, Baochun Li；University of Toronto,Department of Electrical and Computer Engineering。
  - 该工作研究分布式 AI/ML 系统中的「通过位置感知专家安置进行高效通信的 MoE 微调」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。直接目标是改善通信量与同步等待。
  - 相较直接套用通用分布式策略，核心创新是把「通过位置感知专家安置进行高效通信的 MoE 微调」中的特定状态、约束或操作变成一级设计对象。
  - Mixture-of-Experts, DS4AI/ML, Distributed Systems

- [Shuffle-Exchange: Enhancing Collective Communication Efficiency for Large Model Training](https://doi.org/10.1109/icdcs63083.2025.00094)
  - Zhihang Tang, Chenxi Li, Xiang Yang, Bo He, Qi Qi, Jingyu Wang, Laiping Zhao；Tianjin University,College of Intelligence and Computing; Beijing University of Posts and Telecommunications,School of Computer Science; Meituan Corporation。
  - Shuffle-Exchange研究分布式 AI/ML 系统中的「Shuffle-Exchange：提升大型模型训练的集体沟通效率」：以 worker、model shard/layer、gradient 或 expert 为单位组织计算、集合通信、内存与容错状态。直接目标是改善通信量与同步等待。
  - 相较直接套用通用分布式策略，核心创新是把「Shuffle-Exchange：提升大型模型训练的集体沟通效率」中的特定状态、约束或操作变成一级设计对象。
  - LLM Systems, DS4AI/ML, Distributed Systems

- [InverCRS: Generative Audio Inversion Attack in Collaborative Recognition Systems](https://doi.org/10.1109/icdcs63083.2025.00057)
  - Xianglong Zhang, Haoming Luo, Mingda Han, Qihao Dong, Guoming Zhang, Yanni Yang, Qianli Li, Pengfei Hu；Shandong University; Nanjing University of Science and Technology; Beijing University of Posts and Telecommunications,Century College。
  - InverCRS研究安全与隐私中的「InverCRS：协作识别系统中的生成音频反转攻击」：指定对手可观测/篡改的数据和攻击面，再把检测、隔离、加密或隐私保护插入具体数据路径。直接目标是改善安全、隐私或可验证性。
  - 相较把相互影响的子问题分开优化，核心创新是在同一目标下联合决定原本分离的放置、调度、通信或保护策略。
  - Security, S&P, Distributed Systems

- [U-Mesh: Deploying UAV-Mesh Network for Automatic Powerline Inspection in Remote Areas](https://doi.org/10.1109/icdcs63083.2025.00109)
  - Jieyu Zhou, Feng Lyu, Mingliu Liu, Fan Wu, Lijuan He, Huali Lu, Zaixun Ling, Yibo Cui；Central South University,School of Computer Science and Engineering,Changsha,China; The State Grid Hubei Electric Power Research Institute,Wuhan,China。
  - U-Mesh研究IoT 与赛博物理系统中的「U-Mesh：部署无人机-Mesh网络，用于偏远地区的自动电力线路检查」：将终端位置/移动、传感数据、链路和能量状态一起带入感知、通信或计算决策。直接目标是改善能耗或碳效率。
  - 相较直接套用通用分布式策略，核心创新是把「U-Mesh：部署无人机-Mesh网络，用于偏远地区的自动电力线路检查」中的特定状态、约束或操作变成一级设计对象。
  - IoT/CPS, Mobile/Space Networks, IoT&CPS, Distributed Systems

- [BEyes: Unseen Eyes Snooping Pattern Lock via BFI](https://doi.org/10.1109/icdcs63083.2025.00021)
  - Hao Chen, Penghao Wang, Feng Hong, Zhongwen Guo, Chao Liu；Ocean University of China,School of Computer Science and Technology,P.R. China。
  - BEyes研究安全与隐私中的「Beyes：看不见的眼睛通过 BFI 窥探模式锁定」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「Beyes：看不见的眼睛通过 BFI 窥探模式锁定」中的特定状态、约束或操作变成一级设计对象。
  - S&P, Distributed Systems

- [Efficient Serverless Cold Start: Reducing Library Loading Overhead by Profile-guided Optimization](https://doi.org/10.1109/icdcs63083.2025.00037)
  - Syed Salauddin Mohammad Tariq, Ali Al Zein, Soumya Sripad Vaidya, Arati Khanolkar, Zheng Song, Probir Roy；University of Michigan Dearborn,Dearborn,Michigan,USA。
  - 该工作研究云计算中的「高效无服务器冷启动：通过配置文件引导优化减少库加载开销」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善吞吐、扩展性或资源效率。
  - 相较直接套用通用分布式策略，核心创新是把「高效无服务器冷启动：通过配置文件引导优化减少库加载开销」中的特定状态、约束或操作变成一级设计对象。
  - Serverless Computing, Cloud, Distributed Systems

- [CoPe: Taming Collaborative 3D Perception via Lite Network Attention across Mobile Agents](https://doi.org/10.1109/icdcs63083.2025.00027)
  - Shifan Zhang, Hongzi Zhu, Yunzhe Li, Liang Zhang, Shan Chang, Minyi Guo；Shanghai Jiao Tong University,Shanghai,China; Donghua University,Shanghai,China。
  - CoPe研究IoT 与赛博物理系统中的「CoPe：通过跨移动代理的 Lite Network Attention 驯服协作 3D 感知」：将终端位置/移动、传感数据、链路和能量状态一起带入感知、通信或计算决策。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较把相互影响的子问题分开优化，核心创新是在同一目标下联合决定原本分离的放置、调度、通信或保护策略。
  - Multi-Agent Systems, IoT/CPS, IoT&CPS, Distributed Systems

- [P4CEMaker: automated hardware acceleration of consensus protocols](https://doi.org/10.1109/icdcs63083.2025.00072)
  - Paul Breuil, Baptiste Lepers；&#x00C9;cole Polytechnique,France; Inria,France。
  - P4CEMaker研究云计算中的「P4CEMaker：共识协议的自动化硬件加速」：在节点失效或拜占庭作恶假设下组织 message/quorum/round，保证 agreement、liveness 或故障检测。题目明确的关键手段包括consensus/BFT；直接目标是改善吞吐、扩展性或资源效率。
  - 相较让 CPU/通用软件路径承担所有数据移动和控制，核心创新是把关键操作下沉到网络或硬件数据路径。
  - Byzantine Fault Tolerance, Cloud, Distributed Systems

- [Multipath Parallel Reverse Segment Download (MPRD) for Peer-to-Peer Content Delivery](https://doi.org/10.1109/icdcs63083.2025.00066)
  - Suresh Srinivasan, Ehsan Aryafar；Portland State University,Department of Computer Science,Portland,OR,USA。
  - 该工作研究边缘计算中的「用于点对点内容交付的多路径并行反向分段下载 (MPRD)」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「用于点对点内容交付的多路径并行反向分段下载 (MPRD)」中的特定状态、约束或操作变成一级设计对象。
  - Edge Computing, Distributed Systems

- [Too Clever by Half: Detecting Sampling-based Model Stealing Attacks by Their Own Cleverness](https://doi.org/10.1109/icdcs63083.2025.00106)
  - Xin Yao, Chenyang Wang, Yimin Chen, Kecheng Huang, Jiawei Guo, Ming Zhao；Central South University,School of Computer Science and Engineering,Changsha,China; University of Massachusetts Lowell,Miner School of Computer &#x0026; Information Sciences,Lowell,MA,USA。
  - Too Clever by Half研究安全与隐私中的「太聪明了：通过自己的聪明才智检测基于采样的模型窃取攻击」：指定对手可观测/篡改的数据和攻击面，再把检测、隔离、加密或隐私保护插入具体数据路径。直接目标是改善安全、隐私或可验证性。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Security, S&P, Distributed Systems

- [RapidScribe: Bandwidth-aware Parallel Checkpoint for Distributed Neural-Network Training](https://doi.org/10.1109/icdcs63083.2025.00085)
  - Wenxuan Liu, Qihang Chen, Shuotao Xu, Hua Yang, Yuqing Yang, Peng Cheng；Shanghai Jiao Tong University,Institute of Image Communication and Network Engineering; Massachusetts Institute of Technology; Microsoft Research。
  - RapidScribe研究分布式容错中的「RapidScribe：用于分布式神经网络训练的带宽感知并行检查点」：以 worker、model shard/layer、gradient 或 expert 为单位组织计算、集合通信、内存与容错状态。直接目标是改善通信量与同步等待。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Checkpointing, Distributed FT, Distributed Systems

- [GreenFL: Carbon-efficient Federated Learning over RE Powered Edge Computing Systems](https://doi.org/10.1109/icdcs63083.2025.00051)
  - Hanlong Liao, Yu Zhang, Lailong Luo, Deke Guo, Guoming Tang；National University of Defense Technology,Changsha,China; The Chinese University of Hong Kong,Hong Kong; The Hong Kong University of Science and Technology (Guangzhou),Guangzhou,China。
  - GreenFL研究分布式 AI/ML 系统中的「GreenFL：基于 RE 驱动的边缘计算系统的碳高效联合学习」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善能耗或碳效率。
  - 相较直接套用通用分布式策略，核心创新是把「GreenFL：基于 RE 驱动的边缘计算系统的碳高效联合学习」中的特定状态、约束或操作变成一级设计对象。
  - Federated Learning, Edge Computing, DS4AI/ML, Distributed Systems

- [EquiBFT: A Framework for Achieving Fairness in BFT Consensus](https://doi.org/10.1109/icdcs63083.2025.00041)
  - Siwei Cai, Lei Fan, Shengyun Liu, Hong-Sheng Zhou；Shanghai Jiao Tong University,Shanghai,China; Virginia Commonwealth University,Richmond,United States。
  - EquiBFT研究区块链与数据库中的「EquiBFT：在 BFT 共识中实现公平的框架」：在节点失效或拜占庭作恶假设下组织 message/quorum/round，保证 agreement、liveness 或故障检测。题目明确的关键手段包括consensus/BFT；直接目标是改善资源或服务公平性。
  - 相较直接套用通用分布式策略，核心创新是把「EquiBFT：在 BFT 共识中实现公平的框架」中的特定状态、约束或操作变成一级设计对象。
  - Storage/Data Systems, Blockchain, Byzantine Fault Tolerance, Blockchain&Databases

- [SOLB: Synchronization-Objective Load Balancing for Distributed DNN Training](https://doi.org/10.1109/icdcs63083.2025.00099)
  - Jingling Liu, Zixi Wang, Zhong He, Rui Cui, Hao Fang, Jiawei Huang；Central South University,School of Computer Science and Engineering,Changsha,China。
  - SOLB研究分布式 AI/ML 系统中的「SOLB：分布式 DNN 训练的同步目标负载均衡」：以 worker、model shard/layer、gradient 或 expert 为单位组织计算、集合通信、内存与容错状态。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - DS4AI/ML, Distributed Systems

- [DiVE: Differential Video Encoding for Online Edge-assisted Video Analytics on Mobile Agents](https://doi.org/10.1109/icdcs63083.2025.00032)
  - Jiangang Shen, Hongzi Zhu, Liang Zhang, Yunzhe Li, Shan Chang, Jie Wu, Minyi Guo；Shanghai Jiao Tong University,China; Donghua University,China; Cloud Computing Research Institute China Telecom,China。
  - DiVE研究移动计算中的「DiVE：移动代理上在线边缘辅助视频分析的差分视频编码」：将终端位置/移动、传感数据、链路和能量状态一起带入感知、通信或计算决策。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - Multi-Agent Systems, Edge Computing, Mobile Computing, Distributed Systems

- [Saga: Capturing Multi-granularity Semantics from Massive Unlabelled IMU Data](https://doi.org/10.1109/icdcs63083.2025.00090)
  - Yunzhe Li, Facheng Hu, Hongzi Zhu, Shifan Zhang, Liang Zhang, Shan Chang, Minyi Guo；Shanghai Jiao Tong University; Donghua University。
  - Saga研究IoT 与赛博物理系统中的「Saga：从海量未标记 IMU 数据中捕获多粒度语义」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较单层级、单粒度处理，核心创新是按层级/粒度分解状态和决策，再在层间协同。
  - IoT/CPS, IoT&CPS, Distributed Systems

- [HarDTAPE: Hardware Dedicated Trusted transAction Pre-Executor](https://doi.org/10.1109/icdcs63083.2025.00052)
  - Sirui He, Zhibo Sun, Yuan Chen, Yajin Zhou, Cong Wang；City University of Hong Kong,Hong Kong,China; Zhejiang University,Hangzhou,China。
  - HarDTAPE研究安全与隐私中的「HarDTAPE：硬件专用可信事务预执行器」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较让 CPU/通用软件路径承担所有数据移动和控制，核心创新是把关键操作下沉到网络或硬件数据路径。
  - S&P, Distributed Systems

- [Mosaic: Client-driven Account Allocation Framework in Sharded Blockchains](https://doi.org/10.1109/icdcs63083.2025.00065)
  - Yuanzhe Zhang, Shirui Pan, Jiangshan Yu；The University of Sydney,Sydney,Australia; Griffith University,Gold Coast,Australia。
  - Mosaic研究区块链与数据库中的「Mosaic：分片区块链中客户端驱动的账户分配框架」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「Mosaic：分片区块链中客户端驱动的账户分配框架」中的特定状态、约束或操作变成一级设计对象。
  - Storage/Data Systems, Blockchain, Blockchain&Databases, Distributed Systems

- [PEE: Precise ECN Encoding for Efficient Congestion Control in Data Center Networks](https://doi.org/10.1109/icdcs63083.2025.00078)
  - Changlin Jiang, Yi Wu, Hanling Wang, Feixue Han, Dayi Zhao, Yong Jiang, Gareth Tyson, Qing Li；Pengcheng Laboratory,Shenzhen,China; Hong Kong University of Science &#x0026; Technology (GZ),Guangzhou,China。
  - PEE研究云计算中的「PEE：精确的 ECN 编码，用于数据中心网络中的高效拥塞控制」：以 flow/packet/path 和当前链路/队列为输入，决定路由、速率、分流或缓存规则。直接目标是改善吞吐、扩展性或资源效率。
  - 相较直接套用通用分布式策略，核心创新是把「PEE：精确的 ECN 编码，用于数据中心网络中的高效拥塞控制」中的特定状态、约束或操作变成一级设计对象。
  - Cloud, Distributed Systems

- [mmUAVsense: mmWave Radar-based UAV Detection via Fine-grained Rotary Sensing](https://doi.org/10.1109/icdcs63083.2025.00064)
  - Wenhao Xu, Chuyu Wang, Qiancheng Jin, Yanling Bu, Lei Xie, Sanglu Lu；Nanjing University,State Key Laboratory for Novel Software Technology,China; Nanjing University of Aeronautics and Astronautics,College of Computer Science and Technology,Nanjing,China。
  - mmUAVsense研究IoT 与赛博物理系统中的「mmUAVsense：通过细粒度旋转传感进行基于毫米波雷达的无人机检测」：将终端位置/移动、传感数据、链路和能量状态一起带入感知、通信或计算决策。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「mmUAVsense：通过细粒度旋转传感进行基于毫米波雷达的无人机检测」中的特定状态、约束或操作变成一级设计对象。
  - IoT/CPS, Mobile/Space Networks, IoT&CPS, Distributed Systems

- [Sdser: Online Deployment and Scheduling of Dynamic DAG Functions with Bayesian Prediction in Serverless Edge Computing](https://doi.org/10.1109/icdcs63083.2025.00091)
  - Wentao Liu, Ruiting Zhou, Yue Ma；Southeast University,School of Computer Science,Nanjing,China; Southeast University-Monash Joint Graduate School (Suzhou), Southeast University,Nanjing,China。
  - Sdser研究IoT 与赛博物理系统中的「Sdser：无服务器边缘计算中使用贝叶斯预测的动态 DAG 功能的在线部署和调度」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。题目明确的关键手段包括Bayesian 预测/优化；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - Edge Computing, Serverless Computing, IoT/CPS, Scheduling

- [BaroAuth: Harnessing Ear Canal Deformation for Speaking User Authentication on Earbuds](https://doi.org/10.1109/icdcs63083.2025.00020)
  - Luo Zhou, Shan Chang, Jiusong Luo, Huixiang Wen, Hongzi Zhu, Li Lu；Donghua University; Bengbu Medical University; Shanghai Jiao Tong University; University of Electronic Science and Technology of China。
  - BaroAuth研究IoT 与赛博物理系统中的「BaroAuth：利用耳道变形在耳塞上进行语音用户身份验证」：从用户/设备/代理的观测、credential 或时序行为中给出连续身份判定与验证。直接目标是改善安全、隐私或可验证性。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Security, IoT/CPS, IoT&CPS, Distributed Systems

- [Asynchronous Dynamic Committee Proactive Secret Sharing for Large Data](https://doi.org/10.1109/icdcs63083.2025.00017)
  - Zhenliang Lu, Tianyi Zhang, Alan Fekete, Kwok Yan Lam, Qiang Tang；Nanyang Technological University,Singapore; The University of Sydney,Australia。
  - 该工作研究区块链与数据库中的「异步动态委员会大数据主动秘密共享」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - Storage/Data Systems, Blockchain, Blockchain&Databases, Distributed Systems

- [Asynchronous BFT Consensus Made Wireless](https://doi.org/10.1109/icdcs63083.2025.00016)
  - Shuo Liu, Minghui Xu, Tianyi Sun, Xiuzhen Cheng；Shandong University,School of Computer Science and Technology。
  - 该工作研究安全与隐私中的「异步 BFT 共识变得无线」：在节点失效或拜占庭作恶假设下组织 message/quorum/round，保证 agreement、liveness 或故障检测。题目明确的关键手段包括consensus/BFT；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「异步 BFT 共识变得无线」中的特定状态、约束或操作变成一级设计对象。
  - Byzantine Fault Tolerance, S&P, Distributed Systems

- [Octopus: Decentralized Workflow-granular Scheduling for Serverless Workflow](https://doi.org/10.1109/icdcs63083.2025.00068)
  - Keming Wang, Liaoliao Feng, Ligang He, Chenlin Huang, Fengyuan Yu, Tao Xie；National University of Defense Technology,College of Computer Science and Technology,Changsha,China; University of Warwick,Department of Computer Science,Coventry,UK。
  - Octopus研究云计算中的「Octopus：去中心化工作流——无服务器工作流的粒度调度」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Serverless Computing, Scheduling, Cloud, Distributed Systems

- [Depermissioning Web3: a Permissionless Accountable RPC Protocol for Blockchain Networks](https://doi.org/10.1109/icdcs63083.2025.00029)
  - Weihong Wang, Tom Van Cutsem；KU Leuven,DistriNet,Leuven,Belgium。
  - Depermissioning Web3研究区块链与数据库中的「取消许可 Web3：区块链网络的无需许可的可问责 RPC 协议」：以交易、账户、shard/chain 和验证消息为对象，设计执行、路由、原子性或激励机制。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「取消许可 Web3：区块链网络的无需许可的可问责 RPC 协议」中的特定状态、约束或操作变成一级设计对象。
  - Storage/Data Systems, Blockchain, Blockchain&Databases, Distributed Systems

- [Demystifying Distributed Training of Graph Neural Networks for Link Prediction](https://doi.org/10.1109/icdcs63083.2025.00028)
  - Xin Huang, Chul-Ho Lee；Texas State University,Department of Computer Science。
  - 该工作研究分布式 AI/ML 系统中的「揭秘用于链接预测的图神经网络分布式训练」：以 worker、model shard/layer、gradient 或 expert 为单位组织计算、集合通信、内存与容错状态。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Graph Learning Systems, DS4AI/ML, Distributed Systems

- [The Cloud, Like Building and Running Go Binaries](https://doi.org/10.1109/icdcs63083.2025.00103)
  - Diana Arroyo, Paul Castro, Thuan Doan, Nick Mitchell, Sara Kokkila Schumacher, Ed Seabolt, Aleksander Slominski, Ansu Varghese, Lionel Villard, Cora Coleman；IBM Research,NY,USA; UCSD,CA,USA。
  - 该工作研究新兴与部署系统中的「云，例如构建和运行 Go 二进制文件」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「云，例如构建和运行 Go 二进制文件」中的特定状态、约束或操作变成一级设计对象。
  - Emerging and Deployed, Distributed Systems

- [S2M3: Split-and-Share Multi-Modal Models for Distributed Multi-Task Inference on the Edge](https://doi.org/10.1109/icdcs63083.2025.00089)
  - JinYi Yoon, JiHo Lee, Ting He, Nakjung Choi, Bo Ji；Virginia Tech,Blacksburg,VA,USA; Pennsylvania State University,University Park,PA,USA; Nokia Bell Labs,Murray Hill,NJ,USA。
  - S2M3研究分布式 AI/ML 系统中的「S2M3：用于边缘分布式多任务推理的分割和共享多模态模型」：以在线模型请求为单位，组织模型/算子放置、并行执行、状态缓存和请求排队。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Edge Computing, DS4AI/ML, Distributed Systems

- [Smart Blue Light Pole-Based Real-Time Crowd Counting for Smart Campuses](https://doi.org/10.1109/icdcs63083.2025.00098)
  - Yitao Chen, Kaiqi Zhao, Krishna Gundu, Zohair Zaidi, Ming Zhao；Arizona State University; Oakland University。
  - 该工作研究新兴与部署系统中的「基于智能蓝光灯杆的智慧校园实时人群计数」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - Emerging and Deployed, Distributed Systems

- [PRISAM: Efficient Personalization via BN Masks in Heterogeneous Decentralized Federated Learning](https://doi.org/10.1109/icdcs63083.2025.00083)
  - Shan Chang, Xianbo Wang, Hao Yu, Denghui Li, Guanghao Liang, Hongzi Zhu, Bo Li；Donghua University; Shanghai Jiao Tong University; Hong Kong University of Science and Technology。
  - PRISAM研究AI/ML for Distributed Systems中的「PRISAM：异构去中心化联邦学习中通过 BN Masks 实现高效个性化」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善吞吐、扩展性或资源效率。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Federated Learning, AI/ML4DS, Distributed Systems

- [QuHE: Optimizing Utility-Cost in Quantum Key Distribution and Homomorphic Encryption Enabled Secure Edge Computing Networks](https://doi.org/10.1109/icdcs63083.2025.00084)
  - Liangxin Qian, Yang Li, Jun Zhao；Nanyang Technological University,College of Computing and Data Science,Singapore。
  - QuHE研究移动计算中的「QuHE：优化量子密钥分发和同态加密支持的安全边缘计算网络的效用成本」：指定对手可观测/篡改的数据和攻击面，再把检测、隔离、加密或隐私保护插入具体数据路径。题目明确的关键手段包括同态加密；直接目标是改善资源/货币成本。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Edge Computing, Security, Quantum Computing/Networking, Mobile Computing

- [CAFGD: Reduce Fragmentation in Large-Scale Multi-tenant Clusters for GPU Sharing Workloads](https://doi.org/10.1109/icdcs63083.2025.00022)
  - Huazheng Lao, Rui Xu, Long Chen, Jinquan Zhang；Southeast University; Guangdong University of Technology。
  - CAFGD研究分布式 AI/ML 系统中的「CAFGD：减少 GPU 共享工作负载的大规模多租户集群中的碎片」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「CAFGD：减少 GPU 共享工作负载的大规模多租户集群中的碎片」中的特定状态、约束或操作变成一级设计对象。
  - GPU/Accelerator Systems, DS4AI/ML, Distributed Systems

- [TACO: Tackling Over-correction in Federated Learning with Tailored Adaptive Correction](https://doi.org/10.1109/icdcs63083.2025.00102)
  - Weijie Liu, Ziwei Zhan, Carlee Joe-Wong, Edith Ngai, Jingpu Duan, Deke Guo, Xu Chen, Xiaoxi Zhang；Sun Yat-sen University; Carnegie Mellon University; The University of Hong Kong; Pengcheng Laboratory。
  - TACO研究边缘计算中的「TACO：通过定制的自适应校正解决联邦学习中的过度校正问题」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - Federated Learning, Edge Computing, Distributed Systems

- [Few-Shot Domain Adaptation for Effective Data Drift Mitigation in Network Management](https://doi.org/10.1109/icdcs63083.2025.00048)
  - Seyed Soheil Johari, Massimo Tornatore, Raouf Boutaba, Aladdin Saleh；University of Waterloo,Canada; Politecnico di Milano,Italy; Rogers Communications Canada Inc.,Canada。
  - 该工作研究AI/ML for Distributed Systems中的「少样本域适应可有效缓解网络管理中的数据漂移」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「少样本域适应可有效缓解网络管理中的数据漂移」中的特定状态、约束或操作变成一级设计对象。
  - AI/ML4DS, Distributed Systems

- [ECCheck: Enhancing In-Memory Checkpoint with Erasure Coding in Distributed DNN Training](https://doi.org/10.1109/icdcs63083.2025.00033)
  - Guicheng Qi, Zongpeng Li, Chuan Wu, Zhuwei Peng, Yi Zheng；HKU; Tsinghua University; Huawei。
  - ECCheck研究分布式容错中的「ECCheck：在分布式 DNN 训练中使用纠删码增强内存检查点」：以 worker、model shard/layer、gradient 或 expert 为单位组织计算、集合通信、内存与容错状态。题目明确的关键手段包括擦除码；直接目标是改善内存占用与数据复用。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Checkpointing, Distributed FT, Distributed Systems

- [TSAJS: Efficient Multi-Server Joint Task Scheduling Scheme for Mobile Edge Computing](https://doi.org/10.1109/icdcs63083.2025.00108)
  - Chaoqun Li, Rongsheng Fan, Hesong Wang, Mingda Han, Si Wu, Feng Li, Pengfei Hu；Shandong University,School of Computer Science and Technology,Qingdao,China。
  - TSAJS研究IoT 与赛博物理系统中的「TSAJS：移动边缘计算高效多服务器联合任务调度方案」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。直接目标是改善吞吐、扩展性或资源效率。
  - 相较把相互影响的子问题分开优化，核心创新是在同一目标下联合决定原本分离的放置、调度、通信或保护策略。
  - Edge Computing, IoT/CPS, Scheduling, IoT&CPS

- [FedShapleX: Shapley Value Driven Context-Aware Model-Heterogeneous Federated Learning](https://doi.org/10.1109/icdcs63083.2025.00046)
  - Jifeng Chen, Haibo Zhang, Amanda Barnard；Australian National University,ANU College of Engineering, Computing &amp; Cybernetics,Canberra,Australia。
  - FedShapleX研究AI/ML for Distributed Systems中的「FedShapleX：Shapley价值驱动的上下文感知模型——异构联邦学习」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「FedShapleX：Shapley价值驱动的上下文感知模型——异构联邦学习」中的特定状态、约束或操作变成一级设计对象。
  - Federated Learning, AI/ML4DS, Distributed Systems

- [Partitioned Collaborative Inference for On-Device Models via Evolutionary Reinforcement Learning](https://doi.org/10.1109/icdcs63083.2025.00075)
  - Lin Tan, Pengzhan Zhou, Songtao Guo, Jun Zhao, Zhufang Kuang, Dewen Qiao, Lu Yang；Chongqing University,College of Computer Science; Nanyang Technological University,College of Computing and Data Science; Central South University of Forestry and Technology,College of Computer and Mathematics。
  - 该工作研究移动计算中的「通过进化强化学习对设备上模型进行分区协作推理」：以在线模型请求为单位，组织模型/算子放置、并行执行、状态缓存和请求排队。题目明确的关键手段包括强化学习；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较把相互影响的子问题分开优化，核心创新是在同一目标下联合决定原本分离的放置、调度、通信或保护策略。
  - Reinforcement Learning, Mobile Computing, Distributed Systems

- [PDSL: Privacy-Preserved Decentralized Stochastic Learning with Heterogeneous Data Distribution](https://doi.org/10.1109/icdcs63083.2025.00077)
  - Lina Wang, Yunsheng Yuan, Chunxiao Wang, Feng Li；Shandong University,School of Computer Science and Technology,Qingdao,China; Qilu University of Technology (Shandong Academy of Sciences),Key Laboratory of Computing Power Network and Information Security, Ministry of Education, Shandong Computer Science Center (National Supercomputer Center in Jinan),Jinan,China。
  - PDSL研究安全与隐私中的「PDSL：具有异构数据分布的隐私保护去中心化随机学习」：指定对手可观测/篡改的数据和攻击面，再把检测、隔离、加密或隐私保护插入具体数据路径。直接目标是改善安全、隐私或可验证性。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Privacy, S&P, Distributed Systems

- [Mahi-Mahi: Low-Latency Asynchronous BFT DAG-Based Consensus](https://doi.org/10.1109/icdcs63083.2025.00060)
  - Philipp Jovanovic, Lefteris Kokoris-Kogias, Bryan Kumara, Alberto Sonnino, Pasindu Tennage, Igor Zablotchi；UCL,London,United Kingdom; Mysten Labs,Athens,Greece; The Alan Turing Institute,London,United Kingdom; UCL,Mysten Labs,London,United Kingdom; EPFL,Lausanne,Switzerland; Mysten Labs,Zurich,Switzerland。
  - Mahi-Mahi研究区块链与数据库中的「Mahi-Mahi：基于 DAG 的低延迟异步 BFT 共识」：在节点失效或拜占庭作恶假设下组织 message/quorum/round，保证 agreement、liveness 或故障检测。题目明确的关键手段包括consensus/BFT；直接目标是改善请求时延或任务完成时间。
  - 相较直接套用通用分布式策略，核心创新是把「Mahi-Mahi：基于 DAG 的低延迟异步 BFT 共识」中的特定状态、约束或操作变成一级设计对象。
  - Storage/Data Systems, Blockchain, Byzantine Fault Tolerance, Blockchain&Databases

- [Uncovering Hidden Proxy Smart Contracts for Finding Collision Vulnerabilities in Ethereum](https://doi.org/10.1109/icdcs63083.2025.00110)
  - Cheng-Kang Chen, Wen-Yi Chu, Muoi Tran, Laurent Vanbever, Hsu-Chun Hsiao；National Taiwan University; Chalmers University of Technology and University of Gothenburg; ETH Z&#x00FC;rich。
  - 该工作研究区块链与数据库中的「揭示隐藏代理智能合约以查找以太坊中的冲突漏洞」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「揭示隐藏代理智能合约以查找以太坊中的冲突漏洞」中的特定状态、约束或操作变成一级设计对象。
  - Storage/Data Systems, Blockchain, Blockchain&Databases, Distributed Systems

- [FedLTH: A Privacy-preserving Federated Learning Framework with Model Pruning on Edge Clients](https://doi.org/10.1109/icdcs63083.2025.00045)
  - Heyu Zhang, Yulai Xie, Shengshan Hu, Miao He, Peisong He, Jun Zheng, Dan Feng；Huazhong University of Science &amp; Technology,School of Cyber Science and Engineering,Wuhan,China; Sichuan University,School of Cyber Science and Engineering,Chengdu,China; Huazhong University of Science &amp; Technology,Key Laboratory of Information Storage System, Ministry of Education,Wuhan,China。
  - FedLTH研究分布式 AI/ML 系统中的「FedLTH：一种在边缘客户端上进行模型修剪的隐私保护联合学习框架」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善安全、隐私或可验证性。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Federated Learning, Edge Computing, Privacy, DS4AI/ML

- [Plan-Based Scalable Online Virtual Network Embedding](https://doi.org/10.1109/icdcs63083.2025.00080)
  - Oleg Kolosov, David Breitgand, Dean H. Lorenz, Gala Yadgar；Technion,Israel; IBM Research,Israel。
  - 该工作研究边缘计算中的「基于计划的可扩展在线虚拟网络嵌入」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善吞吐、扩展性或资源效率。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - Edge Computing, Distributed Systems

- [Shared memory consensus on a ring: Epigenetic Consensus](https://doi.org/10.1109/icdcs63083.2025.00093)
  - Petra Berenbrink, Funda Ergun, Anna Geisler, Yannic Maus；University of Hamburg,Department of Informatics,Hamburg,Germany; Indiana University Bloomington,Department of Computer Science,Bloomington,United States; Graz University of Technology,Institute of Discrete Mathematics,Graz,Austria; Graz University of Technology,Institute of Algorithms &amp; Theory,Graz,Austria。
  - 该工作研究分布式算法中的「环上的共享内存共识：表观遗传共识」：在节点失效或拜占庭作恶假设下组织 message/quorum/round，保证 agreement、liveness 或故障检测。题目明确的关键手段包括consensus/BFT；直接目标是改善内存占用与数据复用。
  - 相较直接套用通用分布式策略，核心创新是把「环上的共享内存共识：表观遗传共识」中的特定状态、约束或操作变成一级设计对象。
  - Byzantine Fault Tolerance, Algorithms, Distributed Systems

- [PairUpLight: A Multi-agent Reinforcement Learning Approach for Coordinated Multi-intersection Traffic Signal Control](https://doi.org/10.1109/icdcs63083.2025.00073)
  - Wenlu Du, Jing Li, Guiling Grace Wang；Skidmore College,Department of Computer Science,Saratoga Springs,NY,US; New Jersey Institute of Technology,Department of Computer Science,Newark,NJ,US。
  - PairUpLight研究AI/ML for Distributed Systems中的「PairUpLight：一种用于协调多路口交通信号控制的多智能体强化学习方法」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。题目明确的关键手段包括强化学习；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「PairUpLight：一种用于协调多路口交通信号控制的多智能体强化学习方法」中的特定状态、约束或操作变成一级设计对象。
  - Multi-Agent Systems, Reinforcement Learning, AI/ML4DS, Distributed Systems

- [CloudQC: A Network-aware Framework for Multi-tenant Distributed Quantum Computing](https://doi.org/10.1109/icdcs63083.2025.00024)
  - Ruilin Zhou, Yuhang Gan, Yi Liu, Chen Qian；University of California,Santa Cruz。
  - CloudQC研究新兴与部署系统中的「CloudQC：多租户分布式量子计算的网络感知框架」：以 quantum circuit/job、qubit/entanglement 资源和网络路径为对象，决定编译、放置、路由或经典–量子协同。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Quantum Computing/Networking, Emerging and Deployed, Distributed Systems

- [Space Booking: Enabling Performance-Critical Applications in Broadband Satellite Networks](https://doi.org/10.1109/icdcs63083.2025.00100)
  - Xiaojian Wang, Ruozhou Yu, Dejun Yang, Guoliang Xue, Qiushi Wei, Huayue Gu, Zhouyu Li；NC State University,Raleigh,NC; Colorado School of Mines,Golden,CO; Arizona State University,Tempe,AZ。
  - Space Booking研究新兴与部署系统中的「空间预订：在宽带卫星网络中实现性能关键型应用」：将终端位置/移动、传感数据、链路和能量状态一起带入感知、通信或计算决策。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「空间预订：在宽带卫星网络中实现性能关键型应用」中的特定状态、约束或操作变成一级设计对象。
  - Mobile/Space Networks, Emerging and Deployed, Distributed Systems

- [Physical Backdoor Attacks against mmWave-based Human Activity Recognition](https://doi.org/10.1109/icdcs63083.2025.00079)
  - Ziqian Bi, Amit Singha, Hongfei Xue, Tao Li, Yimin Chen, Yanchao Zhang；Purdue University; University of North Carolina,Charlotte; University of Massachusetts Lowell; Arizona State University。
  - 该工作研究安全与隐私中的「针对基于毫米波的人体活动识别的物理后门攻击」：指定对手可观测/篡改的数据和攻击面，再把检测、隔离、加密或隐私保护插入具体数据路径。直接目标是改善安全、隐私或可验证性。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Security, S&P, Distributed Systems

- [Enabling Bitcoin Smart Contracts on the Internet Computer](https://doi.org/10.1109/icdcs63083.2025.00039)
  - Ryan Croote, Islam El-Ashi, Thomas Locher, Yvonne-Anne Pignolet；DFINITY。
  - 该工作研究区块链与数据库中的「在互联网计算机上启用比特币智能合约」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「在互联网计算机上启用比特币智能合约」中的特定状态、约束或操作变成一级设计对象。
  - Storage/Data Systems, Blockchain, Blockchain&Databases, Distributed Systems

- [Partitioning or Not? Hierarchical Task Offloading Optimization in Collaborative Satellite Edge Computing Networks](https://doi.org/10.1109/icdcs63083.2025.00076)
  - Yan Chen, Haiquan Wang, Jun Liu, Xiaolin Jia, Jiejie Zhao, Han Qiu；Beihang University,School of Software,Beijing,China; Institute for Network Sciences and Cyberspace, Tsinghua University,Beijing,China; Zhongguancun Laboratory,Beijing,China。
  - 该工作研究边缘计算中的「分区还是不分区？协作卫星边缘计算网络中的分层任务卸载优化」：对每个任务/算子选择本地、edge、cloud 或网络设备的执行位置，并同时考虑链路和节点状态。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较把相互影响的子问题分开优化，核心创新是在同一目标下联合决定原本分离的放置、调度、通信或保护策略。
  - Edge Computing, Mobile/Space Networks, Distributed Systems

- [Mast: Efficient Training of Mixture-of-Experts Transformers with Task Pipelining and Ordering](https://doi.org/10.1109/icdcs63083.2025.00061)
  - Wenxiang Lin, Xinglin Pan, Shaohuai Shi, Xuan Wang, Bo Li, Xiaowen Chu；School of Computer Science and Technology, Harbin Institute of Technology,Shenzhen; Data Science and Analytics Thrust, The Hong Kong University of Science and Technology (Guangzhou); The Hong Kong University of Science and Technology,Department of Computer Science and Engineering。
  - Mast 面向多 GPU 上的 MoE Transformer 训练，把 attention 层和 MoE 层内的计算、all-to-all/集合通信拆成可重叠 task。它分析 task 之间的依赖与可重叠窗口，再通过以 iteration time 为目标的优化求出近似最优执行顺序，隐藏动态 expert activation 带来的通信开销。
  - 相较只在 MoE 层内做固定 overlap 的调度，核心创新是跨 attention/MoE 层统一建模 task pipeline，并把顺序本身变成可优化变量。
  - MoE Training, Communication-Computation Overlap, Task Ordering, Pipeline Scheduling, Multi-GPU

- [Mitigating Contention in Stream Multiprocessors for Pipelined Mixture of Experts: An SM-Aware Scheduling Approach](https://doi.org/10.1109/icdcs63083.2025.00063)
  - Xinglin Pan, Rui Wang, Wenxiang Lin, Shaohuai Shi, Xiaowen Chu；Data Science and Analytics Thrust, The Hong Kong University of Science and Technology (Guangzhou); School of Computer Science and Technology, Harbin Institute of Technology,Shenzhen。
  - 该工作研究AI/ML for Distributed Systems中的「减轻流式多处理器中专家管道混合的争用：SM 感知调度方法」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。题目明确的关键手段包括pipeline；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「减轻流式多处理器中专家管道混合的争用：SM 感知调度方法」中的特定状态、约束或操作变成一级设计对象。
  - Stream Processing, Scheduling, AI/ML4DS, Distributed Systems

- [HERACLES: Hierarchical Semantic Communications for Distributed Dynamic Sensor Fusion](https://doi.org/10.1109/icdcs63083.2025.00053)
  - Langtian Qin, Yashuo Wu, Sameh Najeh, Marco Levorato, Carla Fabiana Chiasserini；University of California, Irvine,Donald Bren School of Information and Computer Science,Irvine,USA; University of Carthage,Higher School of Communications of Tunis (SUPCOM),Tunis,Tunisia; Politecnico di Torino,Department of Electronics and Telecommunications,Turin,Italy。
  - HERACLES研究边缘计算中的「HERACLES：分布式动态传感器融合的分层语义通信」：将终端位置/移动、传感数据、链路和能量状态一起带入感知、通信或计算决策。直接目标是改善通信量与同步等待。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - Edge Computing, IoT/CPS, Distributed Systems

- [Elastic Scheduling for Mix-Flow in Time-Sensitive Networking](https://doi.org/10.1109/icdcs63083.2025.00038)
  - Jiawei Huang, Yifeng Liu, Yiting Wang, Shengwen Zhou, Hui Li, Zhaoyi Li, Yijun Li, Qile Wang, Jishu Tian, Kengchang Chen, Jiacheng Xie；Central South University,School of Computer Science and Engineering,Changsha,China。
  - 该工作研究新兴与部署系统中的「时间敏感网络中混合流的弹性调度」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - Scheduling, Emerging and Deployed, Distributed Systems

- [Attributing ChatGPT-Transformed Synthetic Code](https://doi.org/10.1109/icdcs63083.2025.00018)
  - Soohyeon Choi, Ali Alkinoon, Ahod Alghuried, Abdulaziz Alghamdi, David Mohaisen；University of Central Florida,Orlando,Florida,USA。
  - 该工作研究安全与隐私中的「归因于 ChatGPT 转换的合成代码」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「归因于 ChatGPT 转换的合成代码」中的特定状态、约束或操作变成一级设计对象。
  - S&P, Distributed Systems

- [Towards Visual-Inertial Integration: Multi-Modal Collaboration-based Video Stabilization](https://doi.org/10.1109/icdcs63083.2025.00107)
  - Chaoran Li, Yanling Bu, Lei Xie；Nanjing University,State Key Laboratory for Novel Software Technology,China; Nanjing University of Aeronautics and Astronautics,College of Computer Science and Technology。
  - 该工作研究IoT 与赛博物理系统中的「迈向视觉惯性集成：基于多模态协作的视频稳定」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「迈向视觉惯性集成：基于多模态协作的视频稳定」中的特定状态、约束或操作变成一级设计对象。
  - IoT/CPS, IoT&CPS, Distributed Systems

- [Lumi: Lightweight Blockchain Layer 2 Protocol from On-chain Coordination](https://doi.org/10.1109/icdcs63083.2025.00059)
  - Xin Wang, Shuhe Cao, Keting Jia, Qidi You, Sisi Duan；Tsinghua University and State Key Laboratory of Cryptography and Digital Economy Security; Shandong University; State Key Laboratory of Space Information System and Integrated Application。
  - Lumi研究区块链与数据库中的「Lumi：来自链上协调的轻量级区块链第 2 层协议」：以交易、账户、shard/chain 和验证消息为对象，设计执行、路由、原子性或激励机制。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「Lumi：来自链上协调的轻量级区块链第 2 层协议」中的特定状态、约束或操作变成一级设计对象。
  - Storage/Data Systems, Blockchain, Blockchain&Databases, Distributed Systems

- [Carbon-Neutralizing Edge AI Inference for Data Streams via Model Control and Allowance Trading](https://doi.org/10.1109/icdcs63083.2025.00023)
  - Yining Zhang, Lei Jiao, Konglin Zhu, Yuedong Xu, Lin Zhang；Beijing University of Posts and Telecommunications,China; University of Oregon,USA; Fudan University,China。
  - 该工作研究分布式 AI/ML 系统中的「通过模型控制和配额交易对数据流进行碳中和边缘人工智能推理」：以在线模型请求为单位，组织模型/算子放置、并行执行、状态缓存和请求排队。直接目标是改善能耗或碳效率。
  - 相较直接套用通用分布式策略，核心创新是把「通过模型控制和配额交易对数据流进行碳中和边缘人工智能推理」中的特定状态、约束或操作变成一级设计对象。
  - Edge Computing, Stream Processing, DS4AI/ML, Distributed Systems

- [A Lightweight Secure Aggregation Protocol for Federated Learning Applications](https://doi.org/10.1109/icdcs63083.2025.00012)
  - Elina van Kempen, Qifei Li, Giorgia Azzurra Marson, Claudio Soriente；Univeristy of California; NEC Laboratories Europe。
  - 该工作研究安全与隐私中的「用于联邦学习应用程序的轻量级安全聚合协议」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善安全、隐私或可验证性。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Federated Learning, Security, S&P, Distributed Systems

- [Optimizing WebAssembly Garbage Collection in Go: Performance Insights, Tuning Tips, and Batch Execution Strategies](https://doi.org/10.1109/icdcs63083.2025.00071)
  - Safia Guellil, Marc Sánchez-Artigas；Computer Science and Maths, Universitat Rovira i Virgili Tarragona,Catalonia,Spain。
  - 该工作研究边缘计算中的「优化 Go 中的 WebAssembly 垃圾收集：性能见解、调优技巧和批量执行策略」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「优化 Go 中的 WebAssembly 垃圾收集：性能见解、调优技巧和批量执行策略」中的特定状态、约束或操作变成一级设计对象。
  - Edge Computing, Distributed Systems

- [Skip Hash: A Fast Ordered Map Via Software Transactional Memory](https://doi.org/10.1109/icdcs63083.2025.00097)
  - Matthew Rodriguez, Vitaly Aksenov, Michael Spear；Commonwealth University of Pennsylvania,Bloomsburg,Pennsylvania; University of London,City St George&#x2019;s,London,United Kingdom; Lehigh University,Bethlehem,Pennsylvania。
  - Skip Hash研究分布式算法中的「Skip Hash：通过软件事务内存的快速有序映射」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善内存占用与数据复用。
  - 相较直接套用通用分布式策略，核心创新是把「Skip Hash：通过软件事务内存的快速有序映射」中的特定状态、约束或操作变成一级设计对象。
  - Algorithms, Distributed Systems

- [PARDON: Privacy-Aware and Robust Federated Domain Generalization](https://doi.org/10.1109/icdcs63083.2025.00074)
  - Dung Thuy Nguyen, Taylor T. Johnson, Kevin Leach；Vanderbilt University,Department of Computer Science,Nashville,TN,USA。
  - PARDON研究分布式 AI/ML 系统中的「PARDON：隐私意识和强大的联合域泛化」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善安全、隐私或可验证性。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Federated Learning, Privacy, DS4AI/ML, Distributed Systems

- [SGX-Enabled Encrypted Cross-Cloud Data Synchronization](https://doi.org/10.1109/icdcs63083.2025.00092)
  - Jia Zhao, Yanjing Ren, Jingwei Li, Patrick P. C. Lee；The Chinese University of Hong Kong; University of Electronic Science and Technology of China。
  - 该工作研究云计算中的「支持SGX的加密跨云数据同步」：指定对手可观测/篡改的数据和攻击面，再把检测、隔离、加密或隐私保护插入具体数据路径。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「支持SGX的加密跨云数据同步」中的特定状态、约束或操作变成一级设计对象。
  - Cloud, Distributed Systems

<a id="acme"></a>

- [ACME: Adaptive Customization of Large Models via Distributed Systems](https://doi.org/10.1109/icdcs63083.2025.00014)
  - Ziming Dai, Chao Qiu, Fei Gao, Yunfeng Zhao, Xiaofei Wang；Tianjin University,College of Intelligence and Computing,China。
  - ACME 面向数据不出端、设备资源和数据分布都异构的个性化 Transformer 架构定制；论文用 ViT-B 及图像分类数据集评测，未以 LLM 为实验负载。双向单环分布式流程先在模型大小约束下搜索 backbone 的 Pareto front，再生成 task header，并按各客户端数据分布聚合个性化架构，同时降低中心化搜索的传输与训练成本。
  - 相较先在中心集群搜索统一架构再下发，核心创新是把 backbone/header 设计和数据异构个性化放入同一分布式模型定制环。
  - Distributed Model Customization, Personalized Architecture, Pareto Search, Data Heterogeneity, Edge AI

- [Distributed DNN-based Video Analytics with Adaptive Multi-Device Collaboration](https://doi.org/10.1109/icdcs63083.2025.00030)
  - Zhihao Xu, Maozhe Zhao, Qinya Li, Shengzhong Liu, Fan Wu, Guihai Chen；Shanghai Jiao Tong University,School of Computer Science,Shanghai,China。
  - 该工作研究分布式 AI/ML 系统中的「具有自适应多设备协作功能的基于 DNN 的分布式视频分析」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - DS4AI/ML, Distributed Systems

- [Hetero2Pipe: Pipelining Multi-DNN Inference on Heterogeneous Mobile Processors under Co-Execution Slowdown](https://doi.org/10.1109/icdcs63083.2025.00054)
  - Yuhao Shen, Zichen Wang, Tianyi Wang, Chaojie Gu, Zhenyu Wen, Yuanchao Shu, Cong Wang；Zhejiang University,Hangzhou,China; Zhejiang University of Technology,Hangzhou,China。
  - Hetero2Pipe研究新兴与部署系统中的「Hetero2Pipe：在协同执行速度减慢的情况下在异构移动处理器上流水线化多 DNN 推理」：以在线模型请求为单位，组织模型/算子放置、并行执行、状态缓存和请求排队。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「Hetero2Pipe：在协同执行速度减慢的情况下在异构移动处理器上流水线化多 DNN 推理」中的特定状态、约束或操作变成一级设计对象。
  - Emerging and Deployed, Distributed Systems

- [IB-SC: Simplify Key Management to Enable Quick Start for Short-session Path Validation](https://doi.org/10.1109/icdcs63083.2025.00055)
  - Keji Miao, Xinghai Wei, Dongqi Han, Jie Yuan, Zhen Qin, Qun Li, Haiguang Wang, Tieyan Li；Beijing University of Posts and Telecommunications,China; University of Chinese Academy of Sciences,China; Tsinghua University,China; Huawei International,Shield Lab,Singapore。
  - IB-SC研究安全与隐私中的「IB-SC：简化密钥管理以实现短会话路径验证的快速启动」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「IB-SC：简化密钥管理以实现短会话路径验证的快速启动」中的特定状态、约束或操作变成一级设计对象。
  - S&P, Distributed Systems

- [Efficient Deterministic Distributed Computing in Ad-Hoc Wireless Networks](https://doi.org/10.1109/icdcs63083.2025.00034)
  - Tomasz Jurdzinski, Dariusz R. Kowalski；University of Wroclaw,Poland; Augusta University,USA。
  - 该工作研究分布式算法中的「Ad-Hoc 无线网络中的高效确定性分布式计算」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善吞吐、扩展性或资源效率。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Algorithms, Distributed Systems

- [SimDC: A High-Fidelity Device Simulation Platform for Device-Cloud Collaborative Computing](https://doi.org/10.1109/icdcs63083.2025.00096)
  - Ruiguang Pei, Junjie Wu, Dan Peng, Min Fang, Jianan Zhang, Zhihui Fu, Jun Wang；OPPO Research Institute。
  - SimDC研究AI/ML for Distributed Systems中的「SimDC：端云协同计算的高保真设备仿真平台」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较把相互影响的子问题分开优化，核心创新是在同一目标下联合决定原本分离的放置、调度、通信或保护策略。
  - AI/ML4DS, Distributed Systems

- [TOB-SVD: Total-Order Broadcast with Single-Vote Decisions in the Sleepy Model](https://doi.org/10.1109/icdcs63083.2025.00104)
  - Francesco D’Amato, Roberto Saltini, Thanh-Hai Tran, Luca Zanolini；Ethereum Foundation,Berlin,Germany; Ethereum Foundation,Sydney,Australia; Independent Researcher,Sydney,Australia; Ethereum Foundation,London,United Kingdom。
  - TOB-SVD研究分布式算法中的「TOB-SVD：Sleepy 模型中具有单票决策的全序广播」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「TOB-SVD：Sleepy 模型中具有单票决策的全序广播」中的特定状态、约束或操作变成一级设计对象。
  - Algorithms, Distributed Systems

- [Congestion Control for Blockchain-enabled SDN in Web 4.0: A Reinforcement Learning Approach through Active Inference](https://doi.org/10.1109/icdcs63083.2025.00026)
  - Chenyang Wang, Xiaoxu Ren, Ying He, Fei Yu, Victor C. M. Leung；Guangdong Laboratory of Artificial Intelligence and Digital Economy (SZ),Shenzhen,China; Shenzhen University,College of Computer Science &amp; Software Engineering,Shenzhen,China; The University of British Columbia,Vancouver,Canada。
  - 该工作研究AI/ML for Distributed Systems中的「Web 4.0 中支持区块链的 SDN 拥塞控制：通过主动推理的强化学习方法」：以在线模型请求为单位，组织模型/算子放置、并行执行、状态缓存和请求排队。题目明确的关键手段包括强化学习；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「Web 4.0 中支持区块链的 SDN 拥塞控制：通过主动推理的强化学习方法」中的特定状态、约束或操作变成一级设计对象。
  - Blockchain, Reinforcement Learning, AI/ML4DS, Distributed Systems

- [Silent Self-Stabilizing Ranking: Time Optimal and Space Efficient](https://doi.org/10.1109/icdcs63083.2025.00095)
  - Petra Berenbrink, Robert Elsässer, Thorsten Götte, Lukas Hintze, Dominik Kaaser；University of Hamburg,Hamburg,Germany; University of Salzburg,Salzburg,Austria; TU Hamburg,Hamburg,Germany。
  - 该工作研究分布式算法中的「无声自稳定排序：时间最优且空间高效」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善吞吐、扩展性或资源效率。
  - 相较直接套用通用分布式策略，核心创新是把「无声自稳定排序：时间最优且空间高效」中的特定状态、约束或操作变成一级设计对象。
  - Algorithms, Distributed Systems

- [Federated Learning with Workload Reduction through Partial Training of Client Models and Entropy-Based Data Selection](https://doi.org/10.1109/icdcs63083.2025.00044)
  - Hongrui Shi, Valentin Radu, Po Yang；University of Sheffield。
  - 该工作研究AI/ML for Distributed Systems中的「通过客户端模型的部分训练和基于熵的数据选择来减少工作量的联邦学习」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「通过客户端模型的部分训练和基于熵的数据选择来减少工作量的联邦学习」中的特定状态、约束或操作变成一级设计对象。
  - Federated Learning, AI/ML4DS, Distributed Systems

- [FLdetox: Detoxify Persistent Backdoors in Federated Learning](https://doi.org/10.1109/icdcs63083.2025.00049)
  - Wenjuan Tang, Chenkai Liu, Yutong Jiang, Jianan Zhao, Peng Sun；Hunan University,ChangSha,China。
  - FLdetox研究安全与隐私中的「FLdetox：清除联邦学习中的持久后门」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「FLdetox：清除联邦学习中的持久后门」中的特定状态、约束或操作变成一级设计对象。
  - Federated Learning, S&P, Distributed Systems

- [Tombolo: Towards a Decentralized Interconnected Blockchain Ecosystem using Cross-Chain Payment Channels](https://doi.org/10.1109/icdcs63083.2025.00105)
  - Siddharth Maurya, Nitin Awathare, Vinay Joseph Ribeiro, Umesh Bellur；Indian Institute of Technology Bombay,Department of Computer Science; Indian Institute of Technology Jodhpur,Department of Computer Science。
  - Tombolo研究区块链与数据库中的「Tombolo：利用跨链支付渠道迈向去中心化互联区块链生态系统」：以交易、账户、shard/chain 和验证消息为对象，设计执行、路由、原子性或激励机制。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Storage/Data Systems, Blockchain, Blockchain&Databases, Distributed Systems

- [Rehearsal-free Federated Domain-incremental Learning](https://doi.org/10.1109/icdcs63083.2025.00086)
  - Rui Sun, Haoran Duan, Jiahua Dong, Varun Ojha, Tejal Shah, Rajiv Ranjan；Newcastle University,Newcastle Upon Tyne,UK; Mohamed Bin Zayed University of Artificial Intelligence,Abu Dhabi,UAE。
  - 该工作研究分布式 AI/ML 系统中的「免演练联邦域增量学习」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「免演练联邦域增量学习」中的特定状态、约束或操作变成一级设计对象。
  - Federated Learning, DS4AI/ML, Distributed Systems

- [PP-FCL: Privacy-Preserving Federated Continual Learning via Generative Replay and Incremental Representation Enhancement](https://doi.org/10.1109/icdcs63083.2025.00081)
  - Zaobo He, Yunkun Wang, Zhipeng Cai, Yingshu Li；Jinan University,College of Cyber Security,Guangzhou,China; Jinan University,Department of Computer Science,Guangzhou,China; Georgia State University,Department of Computer Science,Atlanta,USA。
  - PP-FCL研究安全与隐私中的「PP-FCL：通过生成重放和增量表示增强来保护隐私的联合持续学习」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善安全、隐私或可验证性。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Federated Learning, Privacy, S&P, Distributed Systems

- [Arsc: Automated Reconciliation for State Correctness of Cluster Management](https://doi.org/10.1109/icdcs63083.2025.00015)
  - Hongjing Yu, Chaoqun Li, Tao Han, Pengfei Hu；Shandong University,School of Computer Science and Technology,Qingdao,China。
  - Arsc研究新兴与部署系统中的「Arsc：集群管理状态正确性的自动协调」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「Arsc：集群管理状态正确性的自动协调」中的特定状态、约束或操作变成一级设计对象。
  - Emerging and Deployed, Distributed Systems

- [Bandwidth Optimized Scalable Designs with Inter-Layer Overlapping for MPI Broadcast](https://doi.org/10.1109/icdcs63083.2025.00019)
  - Yi Dai, Qi Zhu, Jiaqing Xu, Qiang Wang, Bo Yang, Min Xie, Dongsheng Li；National University of Defense Technology,College of Computer Science and Technology,Changsha,China。
  - 该工作研究操作系统与中间件中的「用于 MPI 广播的具有层间重叠的带宽优化可扩展设计」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善通信量与同步等待。
  - 相较直接套用通用分布式策略，核心创新是把「用于 MPI 广播的具有层间重叠的带宽优化可扩展设计」中的特定状态、约束或操作变成一级设计对象。
  - OS&Middleware, Distributed Systems

- [On Securing Data Privacy in Federated Learning Using Noise-assisted Aggregated Multi-key Homomorphic Encryption](https://doi.org/10.1109/icdcs63083.2025.00069)
  - Yuxiao Ma, Wei Lou, Song Guo；The Hong Kong Polytechnic University,Department of Computing,Hong Kong SAR; The Hong Kong University of Science and Technology,Department of Computer Science and Engineering,Hong Kong SAR。
  - 该工作研究安全与隐私中的「利用噪声辅助聚合多密钥同态加密保护联邦学习中的数据隐私」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括同态加密、federated aggregation；直接目标是改善安全、隐私或可验证性。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Federated Learning, Privacy, S&P, Distributed Systems

- [Enhancing In-network Aggregation with Adaptive Gradient Quantization for Multi-tenant Learning](https://doi.org/10.1109/icdcs63083.2025.00040)
  - Huifeng Xing, Yinfan Hu, Hao Wang, Yang Chen, Zixuan Chen, Sen Liu, Yang Xu；Fudan University。
  - 该工作研究分布式 AI/ML 系统中的「通过自适应梯度量化增强网络内聚合以实现多租户学习」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。题目明确的关键手段包括网内处理、compression/quantization；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - Network/Hardware Offload, Compression/Quantization, DS4AI/ML, Distributed Systems

- [Efficient Joint Communication and Computation Placement for Large-scale SNN Simulation on Supercomputers](https://doi.org/10.1109/icdcs63083.2025.00035)
  - Yubing Bao, Zhihui Lu, Xin Du, Qiang Duan, Jirui Yang, Jin Zhao, Geyong Min, Yang Chen, Shijing Hu, Xin Wang；Fudan University,School of Computer Science,Shanghai,China; Zhejiang University,School of Software Technology,Zhejiang,China; Pennsylvania State University,Department of Information Sciences and Technology,Abington,PA,USA; University of Exeter,Department of Computer Science,Exeter,UK。
  - 该工作研究分布式 AI/ML 系统中的「超级计算机上大规模 SNN 仿真的高效联合通信和计算布局」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。直接目标是改善通信量与同步等待。
  - 相较把相互影响的子问题分开优化，核心创新是在同一目标下联合决定原本分离的放置、调度、通信或保护策略。
  - DS4AI/ML, Distributed Systems

- [FedSU: Communication-efficient Federated Learning with Speculative Updating](https://doi.org/10.1109/icdcs63083.2025.00047)
  - Wei Yu, Chen Chen, Qinbin Li, Jieru Zhao, Shixuan Sun, Bo Li, Minyi Guo；Shanghai Jiao Tong University,Shanghai,China; Huazhong University of Science and Technology,Wuhan,China; Hong Kong University of Science and Technology,Hong Kong,China。
  - FedSU研究AI/ML for Distributed Systems中的「FedSU：具有推测性更新的高效通信联邦学习」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善通信量与同步等待。
  - 相较直接套用通用分布式策略，核心创新是把「FedSU：具有推测性更新的高效通信联邦学习」中的特定状态、约束或操作变成一级设计对象。
  - Federated Learning, AI/ML4DS, Distributed Systems

- [Exploring Dangerous Graphs with Byzantine Companions](https://doi.org/10.1109/icdcs63083.2025.00042)
  - Giuseppe Antonio Di Luna, Paola Flocchini, Debasish Pattanayak, Giuseppe Prencipe, Francesco Piselli, Nicola Santoro；Sapienza University of Rome,Rome,Italy; University of Ottawa,Ottawa,Canada; University of Pisa,Pisa,Italy; University of Perugia,Perugia,Italy; Carleton University,Ottawa,Canada。
  - 该工作研究分布式容错中的「与拜占庭同伴一起探索危险图」：在节点失效或拜占庭作恶假设下组织 message/quorum/round，保证 agreement、liveness 或故障检测。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Byzantine Fault Tolerance, Distributed FT, Distributed Systems

- [On the Complexity of Deterministic Distributed Wireless Link Scheduling](https://doi.org/10.1109/icdcs63083.2025.00070)
  - Dariusz R. Kowalski, Miguel A. Mosteiro；Augusta University,Department of Computer &#x0026; Cyber Sciences,Augusta,GA,USA; Pace University,Computer Science Department,New York,NY,USA。
  - 该工作研究分布式算法中的「确定性分布式无线链路调度的复杂性研究」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Scheduling, Algorithms, Distributed Systems

- [Wainscot: Tailoring Model Parallelism to Fit Device Memory Limits](https://doi.org/10.1109/icdcs63083.2025.00111)
  - Xiaojuan Ma, Shashwat Jaiswal, Chirag Shetty, Chen-Wei Chou, Kevin Zhang, Indranil Gupta；University of Illinois,Siebel School of Computing and Data Science,Urbana-Champaign,USA。
  - Wainscot研究分布式 AI/ML 系统中的「Wainscot：定制模型并行性以适应设备内存限制」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善内存占用与数据复用。
  - 相较直接套用通用分布式策略，核心创新是把「Wainscot：定制模型并行性以适应设备内存限制」中的特定状态、约束或操作变成一级设计对象。
  - DS4AI/ML, Distributed Systems

- [Fully Decentralized Collection of Attestations for Single-Slot Finality in Ethereum](https://doi.org/10.1109/icdcs63083.2025.00050)
  - János Tapolcai, Bence Ladóczki；Budapest University of Technology and Economics, and with the HUNREN-BME Information Systems Research Group,Faculty of Electrical Engineering and Informatics,Dept. of Telecommunications and Artificial Intelligence。
  - 该工作研究区块链与数据库中的「以太坊中单槽最终性的完全去中心化证明集合」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Storage/Data Systems, Blockchain, Blockchain&Databases, Distributed Systems

- [A Generic Framework for Cross-Chain Atomic Swaps of Digital Tokens](https://doi.org/10.1109/icdcs63083.2025.00011)
  - János Tapolcai, Bence Ladóczki, Lajos Rónyai；Budapest University of Technology and Economics, and with the HUNREN-BME Information Systems Research Group,Faculty of Electrical Engineering and Informatics,Dept. of Telecommunications and Artificial Intelligence; Institute of Mathematics, Budapest University of Technology and Economics,HUN-REN Institute for Computer Science and Control (SZTAKI),Dept. of Algebra and Geometry。
  - 该工作研究区块链与数据库中的「数字代币跨链原子交换的通用框架」：以交易、账户、shard/chain 和验证消息为对象，设计执行、路由、原子性或激励机制。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「数字代币跨链原子交换的通用框架」中的特定状态、约束或操作变成一级设计对象。
  - Storage/Data Systems, Blockchain, Blockchain&Databases, Distributed Systems

- [Failure-Aware Tasking for Teams of Drones](https://doi.org/10.1109/icdcs63083.2025.00043)
  - Jonathan Diller, Yee Shen Teoh, Robert Byers, Qi Han, John G. Rogers, Neil T. Dantam；Colorado School of Mines,Golden,USA; Army Research Laboratory,Adelphi,USA。
  - 该工作研究分布式算法中的「无人机团队的故障感知任务分配」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「无人机团队的故障感知任务分配」中的特定状态、约束或操作变成一级设计对象。
  - Algorithms, Distributed Systems

- [Practical Considerations for Implementing State Machine Replication in the Cloud](https://doi.org/10.1109/icdcs63083.2025.00082)
  - Zhiying Liang, Vahab Jabrayilov, Abutalib Aghayev, Aleksey Charapko；Pennsylvania State University; Columbia University; University of New Hampshire。
  - 该工作研究云计算中的「在云中实现状态机复制的实际注意事项」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「在云中实现状态机复制的实际注意事项」中的特定状态、约束或操作变成一级设计对象。
  - Cloud, Distributed Systems

- [Remote Gate Scheduling in Distributed Quantum Computing](https://doi.org/10.1109/icdcs63083.2025.00087)
  - Xu Xu, Yu Liu, Yingling Mao, Yuanyuan Yang；Stony Brook University,Department of Electrical and Computer Engineering,Stony Brook,USA; Hong Kong Polytechnic University,Department of Computing,Hong Kong SAR。
  - 该工作研究新兴与部署系统中的「分布式量子计算中的远程门调度」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Quantum Computing/Networking, Scheduling, Emerging and Deployed, Distributed Systems

- [A Client-level Assessment of Collaborative Backdoor Poisoning in Non-IID Federated Learning](https://doi.org/10.1109/icdcs63083.2025.00010)
  - Phung Lai, Guanxiong Liu, NhatHai Phan, Issa Khalil, Abdallah Khreishah, Xintao Wu；University at Albany,Albany,New York,USA; Meta Inc.,Menlo Park,California,USA; New Jersey Institute of Technology,Newark,New Jersey,USA; Qatar Computing Research Institute,Doha,Qatar; University of Arkansas,Fayetteville,Arkansas,USA。
  - 该工作研究AI/ML for Distributed Systems中的「非 IID 联邦学习中协作后门中毒的客户端级评估」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较把相互影响的子问题分开优化，核心创新是在同一目标下联合决定原本分离的放置、调度、通信或保护策略。
  - Federated Learning, AI/ML4DS, Distributed Systems

- [Ripple: Scalable Incremental GNN Inferencing on Large Streaming Graphs](https://doi.org/10.1109/icdcs63083.2025.00088)
  - Pranjal Naman, Yogesh Simmhan；Indian Institute of Science,Department of Computational and Data Sciences,Bangalore,India。
  - Ripple研究分布式 AI/ML 系统中的「Ripple：大型流图上的可扩展增量 GNN 推理」：以持续到达的 record、operator state 和 partition 为单位，组织计算、状态迁移与故障恢复。直接目标是改善吞吐、扩展性或资源效率。
  - 相较直接套用通用分布式策略，核心创新是把「Ripple：大型流图上的可扩展增量 GNN 推理」中的特定状态、约束或操作变成一级设计对象。
  - Stream Processing, Graph Learning Systems, DS4AI/ML, Distributed Systems

- [Efficient Partitioning Vision Transformer on Edge Devices for Distributed Inference](https://doi.org/10.1109/icdcs63083.2025.00036)
  - Xiang Liu, Yijun Song, Xia Li, Yifei Sun, Huiying Lan, Zemin Liu, Linshan Jiang, Jialin Li；National University of Singapore,School of Computing; Zhejiang University of Finance &#x0026; Economics Dongfang College,Information and Artificial Intelligence Institute; ETH Zurich,Department of Computer Science; Zhejiang University,College of Computer Science and Technology; Lumia Ltd; National University of Singapore,Institute of Data Science。
  - 该工作研究边缘计算中的「边缘设备上用于分布式推理的高效分区视觉转换器」：以在线模型请求为单位，组织模型/算子放置、并行执行、状态缓存和请求排队。直接目标是改善吞吐、扩展性或资源效率。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Edge Computing, Distributed Systems

- [Inferring Communities of Interest in Collaborative Learning-based Recommender Systems](https://doi.org/10.1109/icdcs63083.2025.00056)
  - Yacine Belal, Mohamed Maouche, Sonia Ben Mokhtar, Anthony Simonet-Boulogne；LIRIS, INSA Lyon,Lyon,France; INRIA, INSA Lyon, CITI, UR; LIRIS, INSA Lyon, CNRS,Lyon,France; iExec Blockchain Tech,Lyon,France。
  - 该工作研究分布式 AI/ML 系统中的「在基于协作学习的推荐系统中推断兴趣社区」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较把相互影响的子问题分开优化，核心创新是在同一目标下联合决定原本分离的放置、调度、通信或保护策略。
  - Decentralized Learning, DS4AI/ML, Distributed Systems

- [A Novel Reputation-based Sharding Blockchain System in Edge Sensor Networks](https://doi.org/10.1109/icdcs63083.2025.00013)
  - Jiarui Zhang, Yuanyuan Yang；Stony Brook University,Department of Electrical and Computer Engineering,NY,USA。
  - 该工作研究IoT 与赛博物理系统中的「边缘传感器网络中一种新颖的基于信誉的分片区块链系统」：以交易、账户、shard/chain 和验证消息为对象，设计执行、路由、原子性或激励机制。题目明确的关键手段包括sharding；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「边缘传感器网络中一种新颖的基于信誉的分片区块链系统」中的特定状态、约束或操作变成一级设计对象。
  - Edge Computing, Blockchain, IoT/CPS, IoT&CPS

- [Distributed Non-Duplicate Sampling with Application on Network-wide Flow Cardinality Estimation](https://doi.org/10.1109/icdcs63083.2025.00031)
  - Aayush Karki, Zibo Liu, Shigang Chen, Haibo Wang；University of Kentucky,Department of Computer Science,USA; University of Florida,Department of Computer &#x0026; Information Science &#x0026; Engineering,USA。
  - 该工作研究分布式算法中的「分布式非重复采样及其在全网流量基数估计中的应用」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Algorithms, Distributed Systems

- [MCaM : Efficient LLM Inference with Multi-tier KV Cache Management](https://doi.org/10.1109/icdcs63083.2025.00062)
  - Kexin Chu, Zixu Shen, Sheng-Ru Cheng, Dawei Xiang, Ziqin Liu, Wei Zhang；University of Connecticut,School of Computing。
  - MCaM研究分布式 AI/ML 系统中的「MCaM：具有多层 KV 缓存管理的高效 LLM 推理」：在容量、层级和时延约束下决定哪些数据/模型状态应保留、迁移、复用或淘汰。题目明确的关键手段包括KV cache、cache placement/reuse；直接目标是改善内存占用与数据复用。
  - 相较单层级、单粒度处理，核心创新是按层级/粒度分解状态和决策，再在层间协同。
  - LLM Systems, Caching, DS4AI/ML, Distributed Systems
