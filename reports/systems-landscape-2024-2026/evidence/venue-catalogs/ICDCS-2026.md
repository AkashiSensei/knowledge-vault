# ICDCS 2026 论文列表

ICDCS 2026 主会 Regular/Main Technical Sessions 共收录 138 篇研究论文；已排除 workshop、poster、demo、doctoral consortium 和 industry event。标题链接指向 DOI/IEEE 文章页（无 DOI 的少数 2026 议程论文链至官方主会程序）；已找到的 2 份合法公开 PDF 保存在 `reference/ICDCS/2026/`。

- [ZeroSwap: A Practical Solution to the Double Swapping Problem in Virtualized Environments](https://doi.org/10.1109/2575-8411.2026.00008)
  - Luc Mahop, Kilian Kemgne, Baptiste Lepers, Fabienne Boyer, Alain Tchana；University of Grenoble Alpes。
  - ZeroSwap研究OS/ Middleware : OS 与中间件中的「ZeroSwap：虚拟化环境中双重交换问题的实用解决方案」：跟踪 guest OS 和 host/hypervisor 对同一内存页的换入换出，避免两层分页机制重复搬运或回收数据。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「ZeroSwap：虚拟化环境中双重交换问题的实用解决方案」中的特定状态、约束或操作变成一级设计对象。
  - OS and Middleware, Distributed Systems

- [SLOShield: Contract-Bounded Safe Evolution for Interpretable Scheduling in Heterogeneous Accelerator Clusters](https://icdcs2026.icdcs.org/program/main-technical-sessions/)
  - Rui Li and Shuang Cao。
  - SLOShield研究OS/ Middleware : OS 与中间件中的「SLOShield：异构加速器集群中可解释调度的契约限制安全演化」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。直接目标是改善吞吐、扩展性或资源效率。
  - 相较直接套用通用分布式策略，核心创新是把「SLOShield：异构加速器集群中可解释调度的契约限制安全演化」中的特定状态、约束或操作变成一级设计对象。
  - GPU/Accelerator Systems, Scheduling, OS and Middleware, Distributed Systems

- [FractalGPU: Fair and Elastic GPU Sharing for General-Purpose Computing](https://doi.org/10.1109/2575-8411.2026.00009)
  - Jingyi Chen, Kaicheng Guo, Lingyun Yang, Yun Wang, Wenda Tang, Dongdong Ma, Pengwei Du, Qian Da, Zhengwei Qi；Shanghai Jiao Tong University; Cloud Computing Research Institute, China Telecom; Huawei Technologies; Ruijin Hospital。
  - FractalGPU研究OS/ Middleware : OS 与中间件中的「FractalGPU：用于通用计算的公平且弹性的 GPU 共享」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善资源或服务公平性。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - GPU/Accelerator Systems, OS and Middleware, Distributed Systems

- [Turmeric: A Fault-Tolerant Publish/Subscribe Service with Multiple Ordering Guarantees](https://doi.org/10.1109/2575-8411.2026.00010)
  - Luís Chula, Paulo Matos, Pedro Mascarenhas, Hervé Paulino；NOVA School of Science and Technology (NOVA FCT), NOVA University。
  - Turmeric研究OS/ Middleware : OS 与中间件中的「Turmeric：具有多重订购保证的容错发布/订阅服务」：对 topic/event 传播和 subscriber 交付建模，在节点故障下同时维持多种消息顺序语义。直接目标是改善故障下的可用性与正确性。
  - 相较直接套用通用分布式策略，核心创新是把「Turmeric：具有多重订购保证的容错发布/订阅服务」中的特定状态、约束或操作变成一级设计对象。
  - OS and Middleware, Distributed Systems

- [Sandwich: Synergizing Hierarchical Coordination with Fine-Grained Serverless Orchestration](https://doi.org/10.1109/2575-8411.2026.00011)
  - Yunfeng Zhao, Chao Qiu, Weijie Guo, Chenxuan Hou, Yuting Li, Xiaofei Wang, Qinghua Hu；College of Intelligence and Computing, Tianjin University。
  - Sandwich研究云计算 1: Hierarchical 云计算中的「三明治：将分层协调与细粒度无服务器编排相结合」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较单层级、单粒度处理，核心创新是按层级/粒度分解状态和决策，再在层间协同。
  - Serverless Computing, Hierarchical Cloud Computing, Distributed Systems

- [GMACAuth: Generative Continuous Authentication via Memory-Augmented Causal Attention](https://doi.org/10.1109/2575-8411.2026.00012)
  - Yantao Li, Yuhang Zhou, Hailong Hu, Huafeng Qin；College of Computer Science, Chongqing University; Chongqing Technology and Business University。
  - GMACAuth研究云计算 1: Hierarchical 云计算中的「GMACAuth：通过记忆增强因果注意力进行生成连续身份验证」：从用户/设备/代理的观测、credential 或时序行为中给出连续身份判定与验证。直接目标是改善内存占用与数据复用。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Security, Hierarchical Cloud Computing, Distributed Systems

- [QCLink: Offloading Hybrid Quantum-Classical Computation to SmartNICs via RDMA](https://doi.org/10.1109/2575-8411.2026.00013)
  - Xingdong Li, Yongzhuo Lu, Zhipeng Liu, Xiaofei Yue, Junyu Chen, Yu Peng, Tingting Li, Zhaoxuan Li, Ziming Zhao, Jianwei Yin；School of Software Technology, Zhejiang University; School of Computer Science and Technology, Beijing Institute of Technology; Institute of Information Engineering, Chinese Academy of Sciences。
  - QCLink研究云计算 1: Hierarchical 云计算中的「QCLink：通过 RDMA 将混合量子经典计算卸载到 SmartNIC」：对每个任务/算子选择本地、edge、cloud 或网络设备的执行位置，并同时考虑链路和节点状态。题目明确的关键手段包括RDMA、SmartNIC offload；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较让 CPU/通用软件路径承担所有数据移动和控制，核心创新是把关键操作下沉到网络或硬件数据路径。
  - Quantum Computing/Networking, Network/Hardware Offload, Hierarchical Cloud Computing, Distributed Systems

- [Sketch-Based in-Network Compression for Iot Satellite Networks](https://doi.org/10.1109/2575-8411.2026.00014)
  - Ting-Yuan Wen, Kate Ching-Ju Lin；National Yang Ming Chiao Tung University; National Taiwan University。
  - 该工作研究云计算 1: Hierarchical 云计算中的「物联网卫星网络基于草图的网络内压缩」：将终端位置/移动、传感数据、链路和能量状态一起带入感知、通信或计算决策。题目明确的关键手段包括网内处理、sketch、compression/quantization；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较让 CPU/通用软件路径承担所有数据移动和控制，核心创新是把关键操作下沉到网络或硬件数据路径。
  - IoT/CPS, Mobile/Space Networks, Network/Hardware Offload, Compression/Quantization

- [Competitive Caching for Distributed Data Access](https://doi.org/10.1109/2575-8411.2026.00015)
  - Tianyu Zuo, Xueyan Tang, Bu Sung Lee；Nanyang Technological University。
  - 该工作研究分布式算法 1 : Online 分布式算法中的「分布式数据访问的竞争性缓存」：在容量、层级和时延约束下决定哪些数据/模型状态应保留、迁移、复用或淘汰。题目明确的关键手段包括cache placement/reuse；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Caching, Online Distributed Algorithms, Distributed Systems

- [Competitive Transaction Admission in PCNs: Online Knapsack with Positive and Negative Items](https://doi.org/10.1109/2575-8411.2026.00016)
  - Marcin Bienkowski, Julien Dallot, Dominik Danelski, Maciej Pacut, Stefan Schmid；University of Wrocław; TU Berlin; TU Berlin and Weizenbaum Institute。
  - 该工作研究分布式算法 1 : Online 分布式算法中的「PCN中的竞争性交易准入：带有正负物品的在线背包」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - Online Distributed Algorithms, Distributed Systems

- [Hash-Based Asynchronous MVBA with Optimal Complexity and Near-Optimal Resilience](https://doi.org/10.1109/2575-8411.2026.00017)
  - Jovan Komatovic, Joachim Neu, Tim Roughgarden；a16z Crypto Research; Columbia University, a16z Crypto Research。
  - 该工作研究分布式算法 1 : Online 分布式算法中的「具有最佳复杂性和近乎最佳弹性的基于哈希的异步 MVBA」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善故障下的可用性与正确性。
  - 相较直接套用通用分布式策略，核心创新是把「具有最佳复杂性和近乎最佳弹性的基于哈希的异步 MVBA」中的特定状态、约束或操作变成一级设计对象。
  - Online Distributed Algorithms, Distributed Systems

- [SPML: A Proactive Congestion Control Scheme for Periodic Flows in Distributed Systems](https://doi.org/10.1109/2575-8411.2026.00018)
  - Shengwen Zhou, Jing Shao, Jiawei Huang；State Key Laboratory of Novel Software Technology, Nanjing University; School of Computer Science and Engineering, Central South University。
  - SPML研究分布式算法 1 : Online 分布式算法中的「SPML：分布式系统中周期性流量的主动拥塞控制方案」：以 flow/packet/path 和当前链路/队列为输入，决定路由、速率、分流或缓存规则。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Online Distributed Algorithms, Distributed Systems

- [Keep Fresh Digital Twins in UAV-Assisted IoT Networks by Exploiting Data Correlations](https://doi.org/10.1109/2575-8411.2026.00019)
  - Qunli Shen, Jing Li, Jian Peng, Zichuan Xu, Cheng Zhao, Pan Zhou, Weifa Liang, Xiaohua Jia, Sajal K. Das, Wenzheng Xu；College of Computer Science, Sichuan University; City University of Hong Kong; School of Software, Dalian University of Technology; Sichuan Province Commercial Investment Group Limited Company; School of Cyber Science and Engineering, Huazhong University of Science & Technology; Missouri University of Science and Technology。
  - 该工作研究边缘计算 1: 边缘计算 Networks中的「通过利用数据关联在无人机辅助物联网网络中保留新鲜的数字孪生」：将终端位置/移动、传感数据、链路和能量状态一起带入感知、通信或计算决策。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「通过利用数据关联在无人机辅助物联网网络中保留新鲜的数字孪生」中的特定状态、约束或操作变成一级设计对象。
  - Edge Computing, IoT/CPS, Mobile/Space Networks, Digital Twin

- [OrbitBFT: Enabling Scalable and Robust BFT Consensus in LEO Constellations](https://doi.org/10.1109/2575-8411.2026.00020)
  - Tianyi Sun, Shuo Liu, Minghui Xu, Xiuzhen Cheng；Shandong University & Quancheng Laboratory; Shandong University。
  - OrbitBFT研究边缘计算 1: 边缘计算 Networks中的「OrbitBFT：在 LEO Constellations 中实现可扩展且稳健的 BFT 共识」：在节点失效或拜占庭作恶假设下组织 message/quorum/round，保证 agreement、liveness 或故障检测。题目明确的关键手段包括consensus/BFT；直接目标是改善吞吐、扩展性或资源效率。
  - 相较直接套用通用分布式策略，核心创新是把「OrbitBFT：在 LEO Constellations 中实现可扩展且稳健的 BFT 共识」中的特定状态、约束或操作变成一级设计对象。
  - Edge Computing, Byzantine Fault Tolerance, Mobile/Space Networks, Edge Computing Networks

- [BeamGes: Motion Resilient Hand Gesture Recognition on Smartphones Using Beamforming Feedback Information](https://doi.org/10.1109/2575-8411.2026.00021)
  - Zijie Tang, Zejun Xu, Yan Wang, Yingying Chen；Temple University; Rutgers University。
  - BeamGes研究边缘计算 1: 边缘计算 Networks中的「BeamGes：使用波束成形反馈信息在智能手机上进行运动弹性手势识别」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善故障下的可用性与正确性。
  - 相较直接套用通用分布式策略，核心创新是把「BeamGes：使用波束成形反馈信息在智能手机上进行运动弹性手势识别」中的特定状态、约束或操作变成一级设计对象。
  - Edge Computing, Edge Computing Networks, Distributed Systems

- [Accelerating Cold Starts of On-Device LLMs via Multi-Source Inference-Aware Parameter Loading](https://doi.org/10.1109/2575-8411.2026.00022)
  - Shucheng Li, Zhenfeng Wang, Fei Zeng, Zhanxi Li, Peng Yang, Feng Lyu；School of Computer Science and Engineering, Central South University; School of Electronic Information and Communications, Huazhong University of Science and Technology。
  - 该工作研究边缘计算 1: 边缘计算 Networks中的「通过多源推理感知参数加载加速设备上 LLM 的冷启动」：以在线模型请求为单位，组织模型/算子放置、并行执行、状态缓存和请求排队。直接目标是改善吞吐、扩展性或资源效率。
  - 相较直接套用通用分布式策略，核心创新是把「通过多源推理感知参数加载加速设备上 LLM 的冷启动」中的特定状态、约束或操作变成一级设计对象。
  - Edge Computing, Edge Computing Networks, Distributed Systems

- [HandoffFL: Efficient Communication in Federated Learning Via Asynchronous Layer-Wise Handoff Training](https://doi.org/10.1109/2575-8411.2026.00023)
  - Wenjun Zhang, Xiaoli Liu, Sasu Tarkoma；University of Helsinki; University of Vaasa。
  - HandoffFL研究Real-Time : Real-Time Networking中的「HandoffFL：通过异步逐层切换训练实现联邦学习中的高效通信」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善通信量与同步等待。
  - 相较单层级、单粒度处理，核心创新是按层级/粒度分解状态和决策，再在层间协同。
  - Federated Learning, Real-Time Networking, Distributed Systems

- [EA-ONS: A Deterministic Time Synchronization Framework for 5G–TSN Integrated LEO Constellations](https://doi.org/10.1109/2575-8411.2026.00024)
  - Siqi Yang, Zonghui Li, Chaoqun You, Yue Gao；Institue of Space Internet, Fudan University; School of Computer Science and Technology, Beijing Jiaotong University。
  - EA-ONS研究Real-Time : Real-Time Networking中的「EA-ONS：5G-TSN 集成 LEO 星座的确定性时间同步框架」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「EA-ONS：5G-TSN 集成 LEO 星座的确定性时间同步框架」中的特定状态、约束或操作变成一级设计对象。
  - Mobile/Space Networks, Real-Time Networking, Distributed Systems

- [ShadowClone: Accelerating Cross-Shard Transactions via Shadow Accounts](https://doi.org/10.1109/2575-8411.2026.00025)
  - Jiahao Qi, Dian Ding, Feilong Lin, Haotian Zhu, Jie Li, Shengyun Liu, Guangtao Xue, Jiannong Cao；Shanghai Jiao Tong University; Zhejiang Normal University; Hong Kong Polytechnic University。
  - ShadowClone研究区块链 1 : Blockchain Sharding中的「ShadowClone：通过影子账户加速跨分片交易」：以交易、账户、shard/chain 和验证消息为对象，设计执行、路由、原子性或激励机制。直接目标是改善吞吐、扩展性或资源效率。
  - 相较直接套用通用分布式策略，核心创新是把「ShadowClone：通过影子账户加速跨分片交易」中的特定状态、约束或操作变成一级设计对象。
  - Blockchain, Blockchain Sharding, Distributed Systems

- [Justitia-L: Budget-Constrained Fairness Optimization in Sharded Blockchains via Lagrangian Dual Control](https://doi.org/10.1109/2575-8411.2026.00026)
  - Sihua Wang, Jian Zheng, Huawei Huang；School of Software Engineering, Sun Yat-Sen University。
  - Justitia-L研究区块链 1 : Blockchain Sharding中的「Justitia-L：通过拉格朗日双控制实现分片区块链中预算受限的公平性优化」：以 worker、model shard/layer、gradient 或 expert 为单位组织计算、集合通信、内存与容错状态。直接目标是改善资源或服务公平性。
  - 相较直接套用通用分布式策略，核心创新是把「Justitia-L：通过拉格朗日双控制实现分片区块链中预算受限的公平性优化」中的特定状态、约束或操作变成一级设计对象。
  - Blockchain, Blockchain Sharding, Distributed Systems

- [Aiming Low-Latency Atomicity for Cross-Shard Transactions in a Sharding Blockchain](https://doi.org/10.1109/2575-8411.2026.00027)
  - Huawei Huang, Jian Zheng, Qinde Chen, Yuting Yang；School of Software Engineering, Sun Yat-sen University。
  - 该工作研究区块链 1 : Blockchain Sharding中的「以分片区块链中跨分片交易的低延迟原子性为目标」：以交易、账户、shard/chain 和验证消息为对象，设计执行、路由、原子性或激励机制。题目明确的关键手段包括sharding；直接目标是改善请求时延或任务完成时间。
  - 相较直接套用通用分布式策略，核心创新是把「以分片区块链中跨分片交易的低延迟原子性为目标」中的特定状态、约束或操作变成一级设计对象。
  - Blockchain, Blockchain Sharding, Distributed Systems

- [Folium: Decoupling Transaction Execution from Consensus via Follower Nodes in a Blockchain](https://doi.org/10.1109/2575-8411.2026.00028)
  - Xiaofei Luo, Huawei Huang, Jian Zheng, Baozhou Xie；The Hong Kong Polytechnic University, Shenzhen Research Institute (PolyU SZRI); School of Software Engineering, Sun Yat-sen University。
  - Folium研究区块链 1 : Blockchain Sharding中的「Folium：通过区块链中的追随者节点将交易执行与共识解耦」：以交易、账户、shard/chain 和验证消息为对象，设计执行、路由、原子性或激励机制。题目明确的关键手段包括consensus/BFT；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「Folium：通过区块链中的追随者节点将交易执行与共识解耦」中的特定状态、约束或操作变成一级设计对象。
  - Blockchain, Byzantine Fault Tolerance, Blockchain Sharding, Distributed Systems

- [Clearing MCP Navigation Fog with Economics-Aware Hierarchical Tool Routing](https://doi.org/10.1109/2575-8411.2026.00029)
  - Jieling Yu, Zhenheng Tang, Ruiting Zhou, Baochun Li, Bo Li；Hong Kong University of Science and Technology; Southeast University; University of Toronto。
  - EHRR 面向数十个 MCP server、数百至数千 tool 时的 Agent 工具选择。LLM 只在需要外部工具时产生结构化功能子任务；随后先在 server 层以语义相关性、调用成本和 posted-price reverse auction 过滤，再在 tool 层联合相关性、成功率、时延和价格路由单次 action。
  - 相较将全部 schema 塞入 prompt 或只用 embedding similarity 检索工具，核心创新是把真实执行成功率、latency 和货币成本带入分层 Agent action routing。
  - Agent System, MCP Tool Routing, Hierarchical Retrieval, Economics-aware Routing, Tool-use Reliability

- [TurboInfer: Targeting Age of Model Inference Optimization for Joint Model Inference in Edge Cloud Systems](https://doi.org/10.1109/2575-8411.2026.00030)
  - Chenxuan Hou, Chao Qiu, Tiantian Cao, Yunfeng Zhao, Chengwei Wang, Xiaofei Wang；College of Intelligence and Computing, Tianjin University。
  - TurboInfer研究AI 1: LLM in AI中的「TurboInfer：针对边缘云系统中联合模型推理的模型推理优化年龄」：以在线模型请求为单位，组织模型/算子放置、并行执行、状态缓存和请求排队。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较把相互影响的子问题分开优化，核心创新是在同一目标下联合决定原本分离的放置、调度、通信或保护策略。
  - LLM Systems, Edge Computing, Large Language Model in AI, Distributed Systems

- [Maestro: Workload-Aware Cross-Cluster Scheduling for LLM-based Multi-Agent Systems](https://doi.org/10.1109/2575-8411.2026.00031)
  - Jinghao Wang, Xiao Zhou, Xiaoyang Sun, Yihui Zhang, Yilong Li, Tianyu Wo, Xu Wang, Chunming Hu, Renyu Yang；Beihang University; University of Leeds。
  - Maestro 是面向 LLM multi-agent workflow 在严格 GPU budget 下在线 serving 的三层调度系统。它根据 Agent role 和 stage 预测输出长度/HBM 用量：node 层用分层 weight cache 和弹性内存让多模型动态共置，cluster 层避开 cold start/内存超载做路由，global 层按整条 workflow 优先级避免互动任务 head-of-line blocking。
  - 相较把 Agent 解释为一组互不相关的 LLM request，核心创新是将 role、stage 依赖和整条 workflow SLO 作为 node–cluster–global 三级调度的共同语义。
  - Agent Infra, Multi-Agent Serving, Cross-cluster Scheduling, GPU Memory, Workflow-aware Scheduling

- [EDAgent: A Concurrent Orchestration Method for Collaborative LLM Multi-Agent System](https://doi.org/10.1109/2575-8411.2026.00032)
  - Zongyang Yuan, Zechang Zhang, Qinbin Li, Lailong Luo, Deke Guo, Mingrui Lao；National University of Defense Technology; School of Computer Science and Technology, Huazhong University of Science and Technology; School of Computer Science and Engineering, Sun Yat-sen University。
  - EDAgent 优化的是 LLM 多 Agent 协作系统本身的执行结构。Event-Driven Communication Protocol 使后续 Agent 可在所需事件/部分状态就绪时启动，而非等前置子任务整体结束；consistent-hash ring 选 Agent，incremental state synchronization 只传多轮任务中的变化状态，以提高并发度并降低通信。
  - 相较 chain/DAG orchestration 将执行顺序与任务依赖刚性绑定，核心创新是用事件和增量状态解耦「依赖已满足」与「前序 Agent 已完全结束」。
  - Agent System, Multi-Agent Orchestration, Event-driven Execution, Incremental State Sync, Concurrent Workflow

- [Efficient KV Cache Migration for Geo-Distributed LLM Inference in Collaborative Edge Computing](https://doi.org/10.1109/2575-8411.2026.00033)
  - Mingjin Zhang, Jiannong Cao, Tao Wu, Xiangchun Chen, Ne Wang；The Hong Kong Polytechnic University; National University of Defense Technology; Wuhan University。
  - 该工作研究边缘计算 2 : Cache in 边缘计算中的「协作边缘计算中地理分布式 LLM 推理的高效 KV 缓存迁移」：在容量、层级和时延约束下决定哪些数据/模型状态应保留、迁移、复用或淘汰。题目明确的关键手段包括KV cache、cache placement/reuse；直接目标是改善内存占用与数据复用。
  - 相较把相互影响的子问题分开优化，核心创新是在同一目标下联合决定原本分离的放置、调度、通信或保护策略。
  - LLM Systems, Edge Computing, Caching, Cache in Edge Computing

- [ReCache: Cost-Efficient DNN Preprocessing on Edge Servers via Group-Based Data Reuse](https://doi.org/10.1109/2575-8411.2026.00034)
  - Chang Xu, Zhixiong Niu, Juan Fang, Qian Wang；Beijing University of Technology; Microsoft Research。
  - ReCache研究边缘计算 2 : Cache in 边缘计算中的「ReCache：通过基于组的数据重用在边缘服务器上进行经济高效的 DNN 预处理」：在容量、层级和时延约束下决定哪些数据/模型状态应保留、迁移、复用或淘汰。题目明确的关键手段包括cache placement/reuse；直接目标是改善资源/货币成本。
  - 相较直接套用通用分布式策略，核心创新是把「ReCache：通过基于组的数据重用在边缘服务器上进行经济高效的 DNN 预处理」中的特定状态、约束或操作变成一级设计对象。
  - Edge Computing, Caching, Cache in Edge Computing, Distributed Systems

- [KV Cache Reuse for Elastic LLM Inference on Edge Devices](https://doi.org/10.1109/2575-8411.2026.00035)
  - Peishuo Wang, Zhenzhe Zheng, Xiaoyao Huang, Jie Wu, Fan Wu, Guihai Chen；Shanghai Jiao Tong University; China Telecom; Temple University。
  - 该工作研究边缘计算 2 : Cache in 边缘计算中的「KV 缓存重用用于边缘设备上的弹性 LLM 推理」：在容量、层级和时延约束下决定哪些数据/模型状态应保留、迁移、复用或淘汰。题目明确的关键手段包括KV cache、cache placement/reuse；直接目标是改善内存占用与数据复用。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - LLM Systems, Edge Computing, Caching, Cache in Edge Computing

- [On Hierarchical Caching with Delayed Hits](https://doi.org/10.1109/2575-8411.2026.00036)
  - Kanghuai Liu, Xueyan Tang；Nanyang Technological University。
  - 该工作研究边缘计算 2 : Cache in 边缘计算中的「关于延迟命中的分层缓存」：在容量、层级和时延约束下决定哪些数据/模型状态应保留、迁移、复用或淘汰。题目明确的关键手段包括cache placement/reuse；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较单层级、单粒度处理，核心创新是按层级/粒度分解状态和决策，再在层间协同。
  - Edge Computing, Caching, Cache in Edge Computing, Distributed Systems

- [Hardening Output Privacy for Secure Inference: A Lightweight Realization via Distributed Trust](https://doi.org/10.1109/2575-8411.2026.00037)
  - Xinqian Wang, Xiaoning Liu, Shangqi Lai, Xun Yi, Ibrahim Khalil, Kwok-Yan Lam；RMIT University; The University of Melbourne; Nanyang Technological University。
  - 该工作研究安全/隐私/信任 1 : Privacy and Security中的「强化输出隐私以实现安全推理：通过分布式信任实现轻量级实现」：以在线模型请求为单位，组织模型/算子放置、并行执行、状态缓存和请求排队。直接目标是改善安全、隐私或可验证性。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Privacy, Security, Privacy and Security, Distributed Systems

- [PriVAR: Client-Side Privacy Framework for Real-Time Location-Based Augmented Reality](https://doi.org/10.1109/2575-8411.2026.00038)
  - Shafizur Rahman Seeam, Ye Zheng, Zhengxiong Li, Yidan Hu；Rochester Institute of Technology; University of Colorado Denver。
  - PriVAR研究安全/隐私/信任 1 : Privacy and Security中的「PriVAR：基于实时位置的增强现实的客户端隐私框架」：指定对手可观测/篡改的数据和攻击面，再把检测、隔离、加密或隐私保护插入具体数据路径。直接目标是改善安全、隐私或可验证性。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - Privacy, Security, Privacy and Security, Distributed Systems

- [FedPF: Accurate Target Privacy Preserving Federated Learning Balancing Fairness and Utility](https://doi.org/10.1109/2575-8411.2026.00039)
  - Kangkang Sun, Jun Wu, Minyi Guo, Jianhua Li, Jianwei Huang；The School of Computer Science, Shanghai Jiao Tong University; The School of Science and Engineering, The Chinese University of Hong Kong。
  - FedPF研究安全/隐私/信任 1 : Privacy and Security中的「FedPF：精准目标隐私保护联邦学习平衡公平与实用」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善资源或服务公平性。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Federated Learning, Privacy, Security, Privacy and Security

- [Multi-Shuffler: Decentralized Shuffling for Differential Privacy in Mobile Edge Computing](https://doi.org/10.1109/2575-8411.2026.00040)
  - Wenjie Chen, Xinhao Huang, Yubo Zhu, Tingxuan Han, Wei Tong, Sheng Zhong；Nanjing University; School of Management and Engineering, Nanjing University。
  - Multi-Shuffler研究安全/隐私/信任 1 : Privacy and Security中的「Multi-Shuffler：移动边缘计算中差异隐私的分散洗牌」：指定对手可观测/篡改的数据和攻击面，再把检测、隔离、加密或隐私保护插入具体数据路径。题目明确的关键手段包括差分隐私；直接目标是改善安全、隐私或可验证性。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Edge Computing, Privacy, Security, Privacy and Security

- [Privacy-Preserving Chunk Scheduling in a BitTorrent Implementation of Federated Learning](https://doi.org/10.1109/2575-8411.2026.00075)
  - Naicheng Li, Javad Dogani, Rui Wang, Kaitai Liang, Nikolaos Laoutaris；IMDEA Networks Institute; Delft University of Technology; University of Turku。
  - 该工作研究AI 2: 训练与学习中的「联邦学习 BitTorrent 实现中的隐私保护块调度」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。题目明确的关键手段包括federated aggregation；直接目标是改善安全、隐私或可验证性。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Federated Learning, Privacy, Scheduling, Training and Learning

- [CARL: Crosstalk-Aware Quantum Compilation Based on Reinforcement Learning](https://doi.org/10.1109/2575-8411.2026.00043)
  - Xiangzhi Zhang, Yu Liu, Yingling Mao, Xu Xu, Yuanyuan Yang；The Hong Kong Polytechnic University; Stony Brook University。
  - CARL研究AI 2: 训练与学习中的「CARL：基于强化学习的串扰感知量子编译」：以 quantum circuit/job、qubit/entanglement 资源和网络路径为对象，决定编译、放置、路由或经典–量子协同。题目明确的关键手段包括强化学习；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「CARL：基于强化学习的串扰感知量子编译」中的特定状态、约束或操作变成一级设计对象。
  - Quantum Computing/Networking, Reinforcement Learning, Training and Learning, Distributed Systems

- [Decentralized Heterogeneous Task Offloading in Edge Computing: A Mean-Field Learning Approach](https://doi.org/10.1109/2575-8411.2026.00044)
  - Shuhui Chu, Chengzhong Xu；University of Macau。
  - 该工作研究AI 2: 训练与学习中的「边缘计算中的分散式异构任务卸载：一种平均场学习方法」：对每个任务/算子选择本地、edge、cloud 或网络设备的执行位置，并同时考虑链路和节点状态。题目明确的关键手段包括mean-field learning；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Edge Computing, Reinforcement Learning, Training and Learning, Distributed Systems

- [FEDLight: A Fuel-Economic Reinforcement Learning Model for Distributed Traffic Signal Control with Spatiotemporal Decomposition](https://doi.org/10.1109/2575-8411.2026.00042)
  - Lang Qian, Peng Sun, Jiayue Jin, Yang Liu, Azzedine Boukerche, Liang Song；Fudan University; Duke Kunshan University; University of Ottawa。
  - FEDLight研究AI 2: 训练与学习中的「FEDLight：具有时空分解的分布式交通信号控制的燃油经济性强化学习模型」：将终端位置/移动、传感数据、链路和能量状态一起带入感知、通信或计算决策。题目明确的关键手段包括强化学习；直接目标是改善资源/货币成本。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - IoT/CPS, Reinforcement Learning, Training and Learning, Distributed Systems

- [Efficient Deployment of Lightweight LLMs on Edge Devices: Kernel-Level Profiling and Cross-Platform Insights](https://doi.org/10.1109/2575-8411.2026.00045)
  - Xinyao Liu, Xingzhou Zhang, Weisong Shi；Institute of Computing Technology, Chinese Academy of Sciences; University of Delaware。
  - 该工作研究边缘计算 3: LLMs in 边缘计算中的「在边缘设备上高效部署轻量级 LLM：内核级分析和跨平台洞察」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善吞吐、扩展性或资源效率。
  - 相较直接套用通用分布式策略，核心创新是把「在边缘设备上高效部署轻量级 LLM：内核级分析和跨平台洞察」中的特定状态、约束或操作变成一级设计对象。
  - LLM Systems, Edge Computing, Large Language Models in Edge Computing, Distributed Systems

- [Prism: Proactive Workload-Aware Optimization for Hybrid-Service in LMaaS Systems](https://doi.org/10.1109/2575-8411.2026.00046)
  - Yuting Li, Chao Qiu, Shaoyuan Huang, Tengwen Zhang, Yunfeng Zhao, Xiaofei Wang；College of Intelligence and Computing, Tianjin University。
  - Prism研究边缘计算 3: LLMs in 边缘计算中的「Prism：LMaaS 系统中混合服务的主动工作负载感知优化」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「Prism：LMaaS 系统中混合服务的主动工作负载感知优化」中的特定状态、约束或操作变成一级设计对象。
  - LLM Systems, Edge Computing, Large Language Models in Edge Computing, Distributed Systems

- [Incentivizing and Orchestrating Cloud-Edge LLM Speculative Decoding via Auctions](https://doi.org/10.1109/2575-8411.2026.00047)
  - Mingtao Ji, Lei Jiao, Bin Tang, Zhihao Qu, Chen Chen, Baoliu Ye；College of Computer Science and Software Engineering, Hohai University; Center for Cyber Security and Privacy, University of Oregon; Nottingham Trent University; State Key Laboratory of Novel Software Technology, Nanjing University。
  - 该工作研究边缘计算 3: LLMs in 边缘计算中的「通过拍卖激励和协调云边缘 LLM 推测性解码」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。题目明确的关键手段包括auction mechanism；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「通过拍卖激励和协调云边缘 LLM 推测性解码」中的特定状态、约束或操作变成一级设计对象。
  - LLM Systems, Edge Computing, Large Language Models in Edge Computing, Distributed Systems

- [HiAsCC: Hierarchical Asynchronous Collective Communication Method for Large Model Training](https://doi.org/10.1109/2575-8411.2026.00048)
  - Zhihang Tang, Chenxi Li, Bo He, Qi Qi, Yulong Tao, Jingyu Wang, Laiping Zhao, Keqiu Li；College of Intelligence and Computing, Tianjin University; School of Computer Science, Beijing University of Posts and Telecommunications。
  - HiAsCC研究边缘计算 3: LLMs in 边缘计算中的「HiAsCC：大模型训练的分层异步集体通信方法」：以 worker、model shard/layer、gradient 或 expert 为单位组织计算、集合通信、内存与容错状态。直接目标是改善通信量与同步等待。
  - 相较单层级、单粒度处理，核心创新是按层级/粒度分解状态和决策，再在层间协同。
  - LLM Systems, Edge Computing, Large Language Models in Edge Computing, Distributed Systems

- [MEGATRACE: Troubleshooting Hang and Slowdown in Large-Scale LLM Training Clusters](https://doi.org/10.1109/2575-8411.2026.00049)
  - Fangzheng Jiao, Menghao Zhang, Bolin Chen, Jiaxun Huang, Yanmin Jia, Xiaohe Hu, Bohua Xu, Bowen Han, Chunming Hu；School of Software, Beihang University; Nanyang Technological University; China Unicom Research Institute。
  - MEGATRACE研究容错 1 : LLM in 容错中的「MEGATRACE：大规模 LLM 训练集群中的挂起和减速故障排除」：以 worker、model shard/layer、gradient 或 expert 为单位组织计算、集合通信、内存与容错状态。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「MEGATRACE：大规模 LLM 训练集群中的挂起和减速故障排除」中的特定状态、约束或操作变成一级设计对象。
  - LLM Systems, Large Language Model in Fault Tolerance, Distributed Systems

- [Falconf: Configuration Error Diagnosis via Log Sequence Learning and Automated Misconfiguration Injections](https://doi.org/10.1109/2575-8411.2026.00050)
  - Youyang Kim, Sahil Suneja, Yunja Choi, Young-Woo Kwon, Byungchul Tak；School of Computer Science and Engineering, Kyungpook National University; IBM TJ Watson Research Center。
  - Falconf研究容错 1 : LLM in 容错中的「Falconf：通过日志序列学习和自动错误配置注入进行配置错误诊断」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「Falconf：通过日志序列学习和自动错误配置注入进行配置错误诊断」中的特定状态、约束或操作变成一级设计对象。
  - LLM Systems, Large Language Model in Fault Tolerance, Distributed Systems

- [ShadowLLM: Resource-Efficient Hot Standby for Heterogeneous Edge LLM Serving](https://doi.org/10.1109/2575-8411.2026.00051)
  - Zhenguo Chen, Pujun Ding, Yuanwei Zhu, Hao Zhang, Jing Lv, Yakun Huang, Xiuquan Qiao；Beijing University of Posts and Telecommunications; School of Big Data and Statistics, Anhui University; China Telecom Wanwei Information Technology Co., Ltd。
  - ShadowLLM研究容错 1 : LLM in 容错中的「ShadowLLM：异构边缘 LLM 服务的资源高效热备」：以在线模型请求为单位，组织模型/算子放置、并行执行、状态缓存和请求排队。直接目标是改善吞吐、扩展性或资源效率。
  - 相较直接套用通用分布式策略，核心创新是把「ShadowLLM：异构边缘 LLM 服务的资源高效热备」中的特定状态、约束或操作变成一级设计对象。
  - LLM Systems, Edge Computing, Large Language Model in Fault Tolerance, Distributed Systems

- [D ${ }^{2}$ Write: Accelerating Erasure-Coded Writes With Distributed Encoding and Decoupled Transmission](https://doi.org/10.1109/2575-8411.2026.00052)
  - Canghai Yang, Wanyi Guo, Zhiwang Yu, Chaoxia Qin, Kan Zhong, Duo Liu；College of Computer Science, Chongqing University; School of Big Data and Software Engineering, Chongqing University。
  - D ${ }^{2}$ Write研究容错 1 : LLM in 容错中的「D ${ }^{2}$ 写入：通过分布式编码和解耦传输加速纠删码写入」：以 block/object/record 或 checkpoint state 为单位，组织读写、编码、复制、索引或恢复路径。直接目标是改善吞吐、扩展性或资源效率。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - LLM Systems, Large Language Model in Fault Tolerance, Distributed Systems

- [Providing Cross-Chain Interoperability Through Decentralized Message Routing and Delivery](https://doi.org/10.1109/2575-8411.2026.00053)
  - Amin Rezaei, Solomon L. Davidson, Bernard Wong；David R. Cheriton School of Computer Science, University of Waterloo。
  - 该工作研究区块链 2 : 区块链 Security中的「通过去中心化消息路由和传递提供跨链互操作性」：以交易、账户、shard/chain 和验证消息为对象，设计执行、路由、原子性或激励机制。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Blockchain, Security, Blockchains Security, Distributed Systems

- [Signet: Scalable Network-Driven Proof of Notification for Blockchain Systems](https://doi.org/10.1109/2575-8411.2026.00054)
  - Elham Ehsani Moghadam, Marc Wyss, Jonghoon Kwon, Marc Frei, Yih-Chun Hu, Adrian Perrig, Alberto Sonnino；ETH Zurich; University of Illinois at Urbana-Champaign。
  - Signet研究区块链 2 : 区块链 Security中的「Signet：区块链系统的可扩展网络驱动通知证明」：以交易、账户、shard/chain 和验证消息为对象，设计执行、路由、原子性或激励机制。直接目标是改善吞吐、扩展性或资源效率。
  - 相较直接套用通用分布式策略，核心创新是把「Signet：区块链系统的可扩展网络驱动通知证明」中的特定状态、约束或操作变成一级设计对象。
  - Blockchain, Security, Blockchains Security, Distributed Systems

- [Semi-Parallel Proof-Of-Work: a Practical Protocol with Improved Incentive Compatibility](https://doi.org/10.1109/2575-8411.2026.00055)
  - Mustafa Doger, Sennur Ulukus；University of Maryland。
  - Semi-Parallel Proof-Of-Work研究区块链 2 : 区块链 Security中的「半并行工作量证明：一种具有改进的激励兼容性的实用协议」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「半并行工作量证明：一种具有改进的激励兼容性的实用协议」中的特定状态、约束或操作变成一级设计对象。
  - Blockchain, Security, Blockchains Security, Distributed Systems

- [Anchor Drag Attack: Exploiting Information Asymmetry in Bitcoin's Stratified Topology](https://doi.org/10.1109/2575-8411.2026.00056)
  - Zihan Wang, Feiyang Chen, Yuxiang Zheng, Jiong Lou, Wugedele Bao, Celimuge Wu, Wei Zhao, Jie Li；Shanghai Jiao Tong University; Hohhot Minzu College; The University of Electro-Communications; Shenzhen University of Advanced Technology。
  - Anchor Drag Attack研究区块链 2 : 区块链 Security中的「锚点拖动攻击：利用比特币分层拓扑中的信息不对称」：指定对手可观测/篡改的数据和攻击面，再把检测、隔离、加密或隐私保护插入具体数据路径。直接目标是改善安全、隐私或可验证性。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Blockchain, Security, Blockchains Security, Distributed Systems

- [L-SDFL: A Lightweight Semi-Distributed Federated Learning for Communication Efficiency](https://doi.org/10.1109/2575-8411.2026.00057)
  - Dapeng Qu, Longtao Li, Ruiduo Li, Xiaojie Liu, Haozhe Wang, Geyong Min；Liaoning University; Shenyang Gas Group Company Limited; University of Exeter。
  - L-SDFL研究分布式算法 2 : 分布式算法 for Communication中的「L-SDFL：一种提高通信效率的轻量级半分布式联邦学习」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善通信量与同步等待。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Federated Learning, Distributed Algorithms for Communication, Distributed Systems

- [Byzantine Reliable Broadcast on Partially Connected Networks Under Message Adversaries](https://doi.org/10.1109/2575-8411.2026.00058)
  - Silvia Bonomi, Lorenzo Di Filippo, Sebastien Tixeuil；Sapienza University of Rome; Sorbonne University, LIP6-NPA, Sapienza University of Rome; Sorbonne University, IUF, France。
  - 该工作研究分布式算法 2 : 分布式算法 for Communication中的「消息对手下部分连接网络上的拜占庭式可靠广播」：在节点失效或拜占庭作恶假设下组织 message/quorum/round，保证 agreement、liveness 或故障检测。直接目标是改善故障下的可用性与正确性。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Byzantine Fault Tolerance, Distributed Algorithms for Communication, Distributed Systems

- [Synthesizing Algorithms to Avoid an Obstacle with a Swarm of Robots](https://doi.org/10.1109/2575-8411.2026.00059)
  - Karine Altisen, Anaïs Durand, Pascal Lafourcade, Oussama Nahnah；Université de Genève; Université Clermont Auvergne。
  - 该工作研究分布式算法 2 : 分布式算法 for Communication中的「综合算法以避开机器人群的障碍」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「综合算法以避开机器人群的障碍」中的特定状态、约束或操作变成一级设计对象。
  - Distributed Algorithms for Communication, Distributed Systems

- [Online Graph Embedding in Star Graphs](https://doi.org/10.1109/2575-8411.2026.00060)
  - Julien Dallot, Darya Melnyk, Maciej Pacut, Stefan Schmid；TU Berlin; TU Berlin and Weizenbaum Institute。
  - 该工作研究分布式算法 2 : 分布式算法 for Communication中的「星图中的在线图嵌入」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - Distributed Algorithms for Communication, Distributed Systems

- [From Alpha to Omega: Lifecycle-Aware Forgetting Defense in Federated Continual Learning for Planetary Exploration](https://doi.org/10.1109/2575-8411.2026.00061)
  - Beining Wu, Jun Huang, Yanxiao Zhao；South Dakota State University; Virginia Commonwealth University。
  - From Alpha to Omega研究边缘计算 4 : Processing and Learning in 边缘计算中的「从 Alpha 到 Omega：行星探索联合持续学习中的生命周期感知遗忘防御」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「从 Alpha 到 Omega：行星探索联合持续学习中的生命周期感知遗忘防御」中的特定状态、约束或操作变成一级设计对象。
  - Federated Learning, Edge Computing, Processing and Learning in Edge Computing, Distributed Systems

- [MS-TBImap: A Real-Time Framework for Multi-Scale Temporary Boundary Integration](https://doi.org/10.1109/2575-8411.2026.00062)
  - Hengyu Zhou, Weizhen Han, Xiang Shao, Haiyong Shi, Shihong Cui, Bingyi Liu；School of Computer Science and Artificial Intelligence, Wuhan University of Technology。
  - MS-TBImap研究边缘计算 4 : Processing and Learning in 边缘计算中的「MS-TBImap：多尺度临时边界集成的实时框架」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - Edge Computing, Processing and Learning in Edge Computing, Distributed Systems

- [Enabling Realtime Stream Processing with Partial Computation Offloading](https://doi.org/10.1109/2575-8411.2026.00063)
  - Jiamei Lv, Cheng Guo, Wenzhao Zhang, Renjie Li, Yongqi Chen, Yixiao Teng, Yi Gao, Wei Dong；Zhejiang University; State Grid Zhejiang Electric Power Research Institute。
  - 该工作研究边缘计算 4 : Processing and Learning in 边缘计算中的「通过部分计算卸载启用实时流处理」：对每个任务/算子选择本地、edge、cloud 或网络设备的执行位置，并同时考虑链路和节点状态。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「通过部分计算卸载启用实时流处理」中的特定状态、约束或操作变成一级设计对象。
  - Edge Computing, Stream Processing, Processing and Learning in Edge Computing, Distributed Systems

- [Quantization-Aware Incentive Mechanism for Communication-Efficient Federated Learning](https://doi.org/10.1109/2575-8411.2026.00064)
  - Hengrui Cui, Zhihao Qu, Baoliu Ye, Tao Zhuang, Bin Tang, Wenxuan Zhou；School of Computer Science, Nanjing University; College of Computer Science and Software Engineering, Hohai University。
  - 该工作研究边缘计算 4 : Processing and Learning in 边缘计算中的「通信高效联邦学习的量化感知激励机制」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation、compression/quantization；直接目标是改善通信量与同步等待。
  - 相较直接套用通用分布式策略，核心创新是把「通信高效联邦学习的量化感知激励机制」中的特定状态、约束或操作变成一级设计对象。
  - Federated Learning, Edge Computing, Compression/Quantization, Processing and Learning in Edge Computing

- [Dual-Blade: Dual-Path NVMe-Direct KV-Cache Offloading for Edge LLM Inference](https://doi.org/10.1109/2575-8411.2026.00065)
  - Bodon Jeong, Hongsu Byun, Youngjae Kim, Weikuan Yu, Kyungkeun Lee, Jihoon Yang, Sungyong Park；Sogang University; Florida State University; Samsung Electronics Co。
  - Dual-Blade研究Big Data 1 : LLM in Big-Data Computing中的「双刀片：用于边缘 LLM 推理的双路径 NVMe 直接 KV 缓存卸载」：在容量、层级和时延约束下决定哪些数据/模型状态应保留、迁移、复用或淘汰。题目明确的关键手段包括cache placement/reuse；直接目标是改善内存占用与数据复用。
  - 相较直接套用通用分布式策略，核心创新是把「双刀片：用于边缘 LLM 推理的双路径 NVMe 直接 KV 缓存卸载」中的特定状态、约束或操作变成一级设计对象。
  - LLM Systems, Edge Computing, Caching, Large Language Model in Big-Data Computing

- [GraphFlash: Enabling Fast and Elastic Graph Processing on Serverless Infrastructure](https://doi.org/10.1109/2575-8411.2026.00066)
  - Chen Zhao, Parsa Poorsistani, Mohammad Goudarzi, Tawfiq Islam, Adel N. Toosi；School of Computing and Information Systems, The University of Melbourne; Monash University。
  - GraphFlash研究Big Data 1 : LLM in Big-Data Computing中的「GraphFlash：在无服务器基础设施上实现快速、弹性的图形处理」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - LLM Systems, Serverless Computing, Large Language Model in Big-Data Computing, Distributed Systems

- [RcLLM: Accelerating Generative Recommendation via Beyond-Prefix KV Caching](https://doi.org/10.1109/2575-8411.2026.00067)
  - Zhan Zhao, Yuxin Wang, Amelie Chi Zhou；Hong Kong Baptist University。
  - RcLLM研究Big Data 1 : LLM in Big-Data Computing中的「RcLLM：通过超前缀 KV 缓存加速生成推荐」：在容量、层级和时延约束下决定哪些数据/模型状态应保留、迁移、复用或淘汰。题目明确的关键手段包括cache placement/reuse；直接目标是改善吞吐、扩展性或资源效率。
  - 相较直接套用通用分布式策略，核心创新是把「RcLLM：通过超前缀 KV 缓存加速生成推荐」中的特定状态、约束或操作变成一级设计对象。
  - LLM Systems, Caching, Large Language Model in Big-Data Computing, Distributed Systems

- [BCD-Megatron: A Cost-Effective Training System for Large Language Models](https://doi.org/10.1109/2575-8411.2026.00068)
  - Zeyu Liu, Yan Li, Yunquan Zhang, Boyang Zhang, Guoyong Jiang, Xin Zhang, Limin Xiao, Weifeng Zhang, Daning Cheng；North University of China; Lenovo Research; Institute of Computing Technology, Chinese Academy of Sciences; Xidian University。
  - BCD-Megatron研究Big Data 1 : LLM in Big-Data Computing中的「BCD-Megatron：一种经济高效的大型语言模型训练系统」：以 worker、model shard/layer、gradient 或 expert 为单位组织计算、集合通信、内存与容错状态。直接目标是改善资源/货币成本。
  - 相较直接套用通用分布式策略，核心创新是把「BCD-Megatron：一种经济高效的大型语言模型训练系统」中的特定状态、约束或操作变成一级设计对象。
  - LLM Systems, Large Language Model in Big-Data Computing, Distributed Systems

- [Memory-Optimized Masked CRYSTALS-Kyber Implementation on ARM Cortex-M4](https://doi.org/10.1109/2575-8411.2026.00069)
  - Ruiqi Hou, Yiwen Gao, Wei Cheng, Yuejun Liu, Jingdian Ming, Yongbin Zhou；School of Cyber Science and Engineering, Nanjing University of Science and Technology。
  - 该工作研究安全/隐私/信任 2 : Cryptography in Security中的「ARM Cortex-M4 上的内存优化 Masked CRYSTALS-Kyber 实现」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善内存占用与数据复用。
  - 相较直接套用通用分布式策略，核心创新是把「ARM Cortex-M4 上的内存优化 Masked CRYSTALS-Kyber 实现」中的特定状态、约束或操作变成一级设计对象。
  - Privacy, Security, Cryptography in Security, Distributed Systems

- [Non-Interactive Distributed Key Management With Pre-Determined Shares](https://doi.org/10.1109/2575-8411.2026.00070)
  - Yaqing Song, Yuan Zhang, Shiyu Li, Weijia Li, Zeqi Lai, Qiang Tang；University of Electronic Science and Technology of China; The University of Virginia; Tsinghua University; The University of Sydney。
  - 该工作研究安全/隐私/信任 2 : Cryptography in Security中的「具有预先确定份额的非交互式分布式密钥管理」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Privacy, Security, Cryptography in Security, Distributed Systems

- [TimeProtect: Time-Bound Policy Enforcement for Metadata-Hiding Encrypted Analytics](https://doi.org/10.1109/2575-8411.2026.00071)
  - Qingyuan Xie, Zhao Bai, Chengjun Cai, Xiaohua Jia；City University of Hong Kong; City University of Hong Kong (Dongguan)。
  - TimeProtect研究安全/隐私/信任 2 : Cryptography in Security中的「TimeProtect：针对元数据隐藏加密分析的有时限策略执行」：指定对手可观测/篡改的数据和攻击面，再把检测、隔离、加密或隐私保护插入具体数据路径。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「TimeProtect：针对元数据隐藏加密分析的有时限策略执行」中的特定状态、约束或操作变成一级设计对象。
  - Privacy, Security, Cryptography in Security, Distributed Systems

- [CITADEL: Fortifying IoT via Context-Aware Offloading of Post-Quantum Cryptography](https://doi.org/10.1109/2575-8411.2026.00072)
  - Ehan Sohn, Changjong Kim, Sunggon Kim；Seoul National University of Science and Technology。
  - CITADEL研究安全/隐私/信任 2 : Cryptography in Security中的「CITADEL：通过上下文感知卸载后量子密码学来强化物联网」：对每个任务/算子选择本地、edge、cloud 或网络设备的执行位置，并同时考虑链路和节点状态。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「CITADEL：通过上下文感知卸载后量子密码学来强化物联网」中的特定状态、约束或操作变成一级设计对象。
  - Privacy, Security, Quantum Computing/Networking, IoT/CPS

- [Spatio-Temporal Parallelism for Diffusion Model Inference on Heterogeneous Multi-GPU Systems](https://doi.org/10.1109/2575-8411.2026.00073)
  - Han Liang, Jiahui Zhou, Zicheng Zhou, Xiaoxi Zhang, Xu Chen；School of Computer Science and Engineering, Sun Yat-sen University。
  - 该工作研究AI 3 : AI-Based Parallelism中的「异构多 GPU 系统上的扩散模型推理的时空并行性」：以在线模型请求为单位，组织模型/算子放置、并行执行、状态缓存和请求排队。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「异构多 GPU 系统上的扩散模型推理的时空并行性」中的特定状态、约束或操作变成一级设计对象。
  - GPU/Accelerator Systems, AI-Based Parallelism, Distributed Systems

- [Tensor Parallelism for State-Space Models](https://doi.org/10.1109/2575-8411.2026.00074)
  - Anurag Dutt, Nimit Shah, Hazem Masarani, Anshul Gandhi；Stony Brook University。
  - 该工作研究AI 3 : AI-Based Parallelism中的「状态空间模型的张量并行性」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。题目明确的关键手段包括tensor parallelism；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「状态空间模型的张量并行性」中的特定状态、约束或操作变成一级设计对象。
  - AI-Based Parallelism, Distributed Systems

- [Pulse: Training Acceleration for Large Diffusion Models with Automatic Pipeline Parallelism](https://doi.org/10.1109/2575-8411.2026.00041)
  - Boran Sun, Guoyong Jiang, Lin Zhang, Chen Chen, Yuechen Tao, Zhishu Che, Jieling Yu, Shan Chang, Huaxi Gu, Fangming Liu, Bo Li；The Hong Kong University of Science and Technology; Xidian University; Shanghai Jiao Tong University; Pengcheng Laboratory; Donghua University。
  - Pulse研究AI 3 : AI-Based Parallelism中的「Pulse：具有自动管道并行性的大型扩散模型的训练加速」：以 worker、model shard/layer、gradient 或 expert 为单位组织计算、集合通信、内存与容错状态。题目明确的关键手段包括pipeline；直接目标是改善吞吐、扩展性或资源效率。
  - 相较直接套用通用分布式策略，核心创新是把「Pulse：具有自动管道并行性的大型扩散模型的训练加速」中的特定状态、约束或操作变成一级设计对象。
  - AI-Based Parallelism, Distributed Systems

- [MixServe: An Automatic Distributed Serving System for MoE Models with Hybrid Parallelism Based on Fused Communication Algorithm](https://doi.org/10.1109/2575-8411.2026.00076)
  - Bowen Zhou, Jinrui Jia, Wenhao He, Yong Zhang, Fang Dong；Southeast University; The Chinese University of Hong Kong。
  - MixServe研究AI 3 : AI-Based Parallelism中的「MixServe：基于融合通信算法的混合并行MoE模型自动分布式服务系统」：以在线模型请求为单位，组织模型/算子放置、并行执行、状态缓存和请求排队。直接目标是改善通信量与同步等待。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Mixture-of-Experts, AI-Based Parallelism, Distributed Systems

- [Exploring the Feasibility and Performance of Distributed Llm Serving on Consumer-Grade Gpus](https://doi.org/10.1109/2575-8411.2026.00077)
  - Lewei Jin, Yang Liu, Yongqi Chen, Xiaoqiang Guo, Kui Zhang, Yi Gao, Wei Dong；College of Computer Science and Technology, Zhejiang University。
  - 该工作研究边缘计算 5 : Offloading and LLMs in 边缘计算中的「探索消费级 GPU 上分布式 LLM 服务的可行性和性能」：以在线模型请求为单位，组织模型/算子放置、并行执行、状态缓存和请求排队。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - LLM Systems, Edge Computing, GPU/Accelerator Systems, Offloading and Large Language Models in Edge Computing

- [FlashServe: Adaptive Kernel Provision for Quantized LLM Serving](https://doi.org/10.1109/2575-8411.2026.00078)
  - Yuyan Chen, Haodong Wang, Junyuan Liang, Wuhui Chen, Zicong Hong, Song Guo, Ruiyan Zhuang, Yi Quan；School of Computer Science and Engineering, Sun Yat-sen University; Hong Kong University of Science and Technology; School of Software Engineering, Sun Yat-sen University; Greater Bay Area National Center of Technology Innovation。
  - FlashServe研究边缘计算 5 : Offloading and LLMs in 边缘计算中的「FlashServe：用于量化 LLM 服务的自适应内核配置」：以在线模型请求为单位，组织模型/算子放置、并行执行、状态缓存和请求排队。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - LLM Systems, Edge Computing, Offloading and Large Language Models in Edge Computing, Distributed Systems

- [Llm-Guided Training and Llm-Free Inference for Reliable Task Offloading in Edge Computing](https://doi.org/10.1109/2575-8411.2026.00079)
  - Hao Guo, Kaixiang Xv, Lei Yang；School of Software Engineering, South China University of Technology。
  - FLARE 面向突发任务、链路波动和节点短时故障下的边缘 offloading。训练时，轻量 LLM 从节点状态、任务属性、链路和最近 failure feedback 生成经有效性检查的短期语义 cue，用 attention 软引导 DRL；随训练逐步将权重降为零，部署时只保留小型 DRL policy。
  - 相较在边缘设备每次调用 LLM 或直接蒸馏 LLM decision，核心创新是只在训练早期使用可退火的 semantic guidance，使线上决策无 prompt/token/LLM 开销。
  - LLM for Systems, Edge Task Offloading, LLM-guided DRL, Semantic Decoupling, Failure-aware Scheduling

- [Energy-Aware Usv-Uav Cooperative Task Offloading Optimization in Water Monitoring System](https://doi.org/10.1109/2575-8411.2026.00080)
  - Chaogang Tang, Tiyu Yao, Shuo Xiao, Huaming Wu, Ruidong Li；School of Computer Science and Technology / School of Artificial Intelligence, China University of Mining and Technology; The Center for Applied Mathematics, Tianjin University; The Institute of Science and Engineering, Kanazawa University。
  - 该工作研究边缘计算 5 : Offloading and LLMs in 边缘计算中的「水监测系统中的能源感知型USV-UAV协同任务卸载优化」：对每个任务/算子选择本地、edge、cloud 或网络设备的执行位置，并同时考虑链路和节点状态。直接目标是改善能耗或碳效率。
  - 相较把相互影响的子问题分开优化，核心创新是在同一目标下联合决定原本分离的放置、调度、通信或保护策略。
  - LLM Systems, Edge Computing, Mobile/Space Networks, Offloading and Large Language Models in Edge Computing

- [Batchmon: Exploiting Serverless Functions for Cost-Effective, SLO-Driven Batch Inference Serving](https://doi.org/10.1109/2575-8411.2026.00081)
  - Josep Calero-Santo, Marc Sanchez-Artigas；Universitat Rovira i Virgili。
  - Batchmon研究云计算 2 : 云计算 Networks中的「Batchmon：利用无服务器函数实现经济高效、SLO 驱动的批量推理服务」：以在线模型请求为单位，组织模型/算子放置、并行执行、状态缓存和请求排队。直接目标是改善资源/货币成本。
  - 相较直接套用通用分布式策略，核心创新是把「Batchmon：利用无服务器函数实现经济高效、SLO 驱动的批量推理服务」中的特定状态、约束或操作变成一级设计对象。
  - Serverless Computing, Cloud Computing Networks, Distributed Systems

- [BalISAC-MAPPO: A MARL for Spacing Trade-Off Balancing in ISAC Multi-UAV Terrain Coverage](https://doi.org/10.1109/2575-8411.2026.00082)
  - Zheyi Sun, Yang Yang, Cheng Zhan, Xianlong Jiao；School of Computer and Information Science, Southwest University; College of Computer Science, Chongqing University。
  - BalISAC-MAPPO研究云计算 2 : 云计算 Networks中的「BalISAC-MAPPO：用于 ISAC 多无人机地形覆盖中的空间权衡平衡的 MARL」：将终端位置/移动、传感数据、链路和能量状态一起带入感知、通信或计算决策。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「BalISAC-MAPPO：用于 ISAC 多无人机地形覆盖中的空间权衡平衡的 MARL」中的特定状态、约束或操作变成一级设计对象。
  - Mobile/Space Networks, Cloud Computing Networks, Distributed Systems

- [AT-Cache: Towards Traffic-Aware Adaptive TCAM Rule Caching Framework](https://doi.org/10.1109/2575-8411.2026.00083)
  - Lei Guo, Zeyu Luan, Qing Li, Zhuochen Fan, Bo Tang；Southern University of Science and Technology; Pengcheng Laboratory。
  - AT-Cache研究云计算 2 : 云计算 Networks中的「AT-Cache：迈向流量感知自适应 TCAM 规则缓存框架」：在容量、层级和时延约束下决定哪些数据/模型状态应保留、迁移、复用或淘汰。题目明确的关键手段包括cache placement/reuse；直接目标是改善内存占用与数据复用。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - Caching, Cloud Computing Networks, Distributed Systems

- [Congestion Adaptive Load Balancing with in-Network Reordering for Datacenter Networks](https://doi.org/10.1109/2575-8411.2026.00084)
  - Jiacheng Qu, Shaojun Zou, Yi Jiang；School of Computer Science and Technology, Hainan University。
  - 该工作研究云计算 2 : 云计算 Networks中的「数据中心网络的拥塞自适应负载平衡和网内重新排序」：以 flow/packet/path 和当前链路/队列为输入，决定路由、速率、分流或缓存规则。题目明确的关键手段包括网内处理；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - Network/Hardware Offload, Cloud Computing Networks, Distributed Systems

- [OptiVibe: Keystroke Inference Attacks Through a New Optical-Vibration Side Channel](https://doi.org/10.1109/2575-8411.2026.00085)
  - Youngtak Cho, Sanket Suresh Badgujar, Srinivasan Murali, Xuhao Xie, Ming Li；University of Texas at Arlington; Texas A&M University–San Antonio。
  - OptiVibe研究安全/隐私/信任 3 : Security Attacks in Networking-Systems中的「OptiVibe：通过新的光学振动侧通道进行击键推理攻击」：以在线模型请求为单位，组织模型/算子放置、并行执行、状态缓存和请求排队。直接目标是改善安全、隐私或可验证性。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Privacy, Security, Security Attacks in Networking-Systems, Distributed Systems

- [A Replay-Attack Resistant and Lightweight Token Validation Framework With Hash Chain](https://doi.org/10.1109/2575-8411.2026.00086)
  - Gyeongheon Jeong, Jaeho Nam, Honggeun Park, Hyunsoo Kim, Jinhwan Jung, Jongsung Kim, Taekyoung Kwon；Seoul National University; Cloud Research Team, Samsung SDS。
  - 该工作研究安全/隐私/信任 3 : Security Attacks in Networking-Systems中的「一种基于哈希链的抗重放攻击的轻量级代币验证框架」：指定对手可观测/篡改的数据和攻击面，再把检测、隔离、加密或隐私保护插入具体数据路径。直接目标是改善安全、隐私或可验证性。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Privacy, Security, Security Attacks in Networking-Systems, Distributed Systems

- [Privacy Attacks on Stable Marriage](https://doi.org/10.1109/2575-8411.2026.00087)
  - Stephan A. Fahrenkrog-Petersen, Aleksander Figiel, Darya Melnyk, Tijana Milentijević, Stefan Schmid；University of Liechtenstein; TU Berlin; TU Berlin and Weizenbaum Institute。
  - 该工作研究安全/隐私/信任 3 : Security Attacks in Networking-Systems中的「对稳定婚姻的隐私攻击」：指定对手可观测/篡改的数据和攻击面，再把检测、隔离、加密或隐私保护插入具体数据路径。直接目标是改善安全、隐私或可验证性。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Privacy, Security, Security Attacks in Networking-Systems, Distributed Systems

- [Heterogeneous Graph Backdoor Attack](https://doi.org/10.1109/2575-8411.2026.00088)
  - Jiawei Chen, Lusi Li, Daniel Takabi, Masha Sosonkina, Rui Ning；Old Dominion University; School of Cybersecurity, Old Dominion University。
  - 该工作研究安全/隐私/信任 3 : Security Attacks in Networking-Systems中的「异构图后门攻击」：指定对手可观测/篡改的数据和攻击面，再把检测、隔离、加密或隐私保护插入具体数据路径。直接目标是改善安全、隐私或可验证性。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Privacy, Security, Security Attacks in Networking-Systems, Distributed Systems

- [ProtoGenesis: Prototype Training with Zero Local Samples for Heterogeneous Clients in Fully Decentralized Federated Systems](https://doi.org/10.1109/2575-8411.2026.00089)
  - Xianbo Wang, Shan Chang, Minghui Dai, Hao Yu, Yunnan Tu, Hongzi Zhu, Bo Li；Donghua University; Shanghai Jiao Tong University; Hong Kong University of Science and Technology。
  - ProtoGenesis研究AI 4 : Decentralized Learning in AI中的「ProtoGenesis：完全去中心化联邦系统中异构客户端的零本地样本原型训练」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Federated Learning, Decentralized Learning, Decentralized Learning in AI, Distributed Systems

- [mmLite: Leveraging mmWave Radar for Efficient Seated Pose Estimation](https://doi.org/10.1109/2575-8411.2026.00090)
  - Ruili Shi, Shuai Wang, Wenchao Jiang, Zhimeng Yin, Wei Gong, Shuai Wang；Southeast University; Leoch Battery; City University of Hong Kong; University of Science and Technology of China。
  - mmLite研究AI 4 : Decentralized Learning in AI中的「mmLite：利用毫米波雷达进行高效的坐姿估计」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善吞吐、扩展性或资源效率。
  - 相较直接套用通用分布式策略，核心创新是把「mmLite：利用毫米波雷达进行高效的坐姿估计」中的特定状态、约束或操作变成一级设计对象。
  - Decentralized Learning, Decentralized Learning in AI, Distributed Systems

- [Tackling the Runtime Context Fluctuation: Steady Scheduling in Data Stream Analytics for Industrial Internet of Things](https://doi.org/10.1109/2575-8411.2026.00091)
  - Shuyu Cao, Wenhui Zhou, Jingyi Ning, Lei Xie；Nanjing University。
  - 该工作研究AI 4 : Decentralized Learning in AI中的「应对运行时上下文波动：工业物联网数据流分析中的稳定调度」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「应对运行时上下文波动：工业物联网数据流分析中的稳定调度」中的特定状态、约束或操作变成一级设计对象。
  - Decentralized Learning, Stream Processing, Scheduling, Decentralized Learning in AI

- [RAGNAROS: Large-Scale Regex Processing Acceleration with Neural Networks for DPI](https://doi.org/10.1109/2575-8411.2026.00092)
  - Sebin Jo, Taejune Park；School of Artificial Intelligence, Chonnam National University。
  - RAGNAROS研究AI 4 : Decentralized Learning in AI中的「RAGNAROS：使用 DPI 神经网络进行大规模正则表达式处理加速」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善吞吐、扩展性或资源效率。
  - 相较直接套用通用分布式策略，核心创新是把「RAGNAROS：使用 DPI 神经网络进行大规模正则表达式处理加速」中的特定状态、约束或操作变成一级设计对象。
  - Decentralized Learning, Decentralized Learning in AI, Distributed Systems

- [Trilogy: Tag Information Collection in Multi-Category Commodity RFID Systems](https://doi.org/10.1109/2575-8411.2026.00093)
  - Yanyan Wang, Zhihao Qu, Jia Liu, Xin He, Yingchi Mao, Bin Tang, Baoliu Ye；Hohai University; Nanjing University; Nanjing University of Posts and Telecommunications。
  - Trilogy研究IoT/CPS 1 : IoT Based Distributed Computing Systems中的「三部曲：多品类商品RFID系统中的标签信息采集」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「三部曲：多品类商品RFID系统中的标签信息采集」中的特定状态、约束或操作变成一级设计对象。
  - IoT/CPS, IoT Based Distributed Computing Systems, Distributed Systems

- [A Cyber-Physical Cooperative Scheme for Energy Scheduling and Dynamic Pricing in Charging Station Alliances via Cloud-Edge Intelligence](https://doi.org/10.1109/2575-8411.2026.00094)
  - Bing Lin, Kai He, Xingyuan Lin, Jingtao Chen, Huaming Wu；College of Physics and Energy, Fujian Normal University; School of Computer Science and Engineering, Macau University of Science and Technology; College of Computer and Cyber Security, Fujian Normal University; Tianjin University。
  - 该工作研究IoT/CPS 1 : IoT Based Distributed Computing Systems中的「通过云边智能实现充电站联盟能源调度和动态定价的信息物理合作方案」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。直接目标是改善能耗或碳效率。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - Edge Computing, IoT/CPS, Scheduling, IoT Based Distributed Computing Systems

- [Lucid: Lidar-Based Uav Classification and Detection for Airspace Surveillance](https://doi.org/10.1109/2575-8411.2026.00095)
  - Deokjin Kim, Jeongyeup Paek, Saewoong Bahk；INMC, Seoul National University; Chung-Ang University。
  - Lucid研究IoT/CPS 1 : IoT Based Distributed Computing Systems中的「Lucid：用于空域监视的基于激光雷达的无人机分类和检测」：将终端位置/移动、传感数据、链路和能量状态一起带入感知、通信或计算决策。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「Lucid：用于空域监视的基于激光雷达的无人机分类和检测」中的特定状态、约束或操作变成一级设计对象。
  - IoT/CPS, Mobile/Space Networks, IoT Based Distributed Computing Systems, Distributed Systems

- [TriLoRa: Improving LoRa PHY Data Rate for High-Density LoRaWAN](https://doi.org/10.1109/2575-8411.2026.00096)
  - Yanbo Zhang, Qirui Liu, Songfan Li, Mo Li；The Hong Kong University of Science and Technology; Peking University。
  - TriLoRa研究IoT/CPS 1 : IoT Based Distributed Computing Systems中的「TriLoRa：提高高密度 LoRaWAN 的 LoRa PHY 数据速率」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「TriLoRa：提高高密度 LoRaWAN 的 LoRa PHY 数据速率」中的特定状态、约束或操作变成一级设计对象。
  - IoT/CPS, IoT Based Distributed Computing Systems, Distributed Systems

- [Rethinking Quantum Network Design Using a Verification-Based Quantum Transmission Protocol](https://doi.org/10.1109/2575-8411.2026.00097)
  - Yiming Zeng, Zhengyu Wu, Xuan Du Trinh, Yuanyuan Yang, Nengkun Yu, Aruna Balasubramanian；Binghamton University; Stony Brook University。
  - 该工作研究应用/数字孪生 1 : Quantum Computing and Networking中的「使用基于验证的量子传输协议重新思考量子网络设计」：以 quantum circuit/job、qubit/entanglement 资源和网络路径为对象，决定编译、放置、路由或经典–量子协同。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「使用基于验证的量子传输协议重新思考量子网络设计」中的特定状态、约束或操作变成一级设计对象。
  - Quantum Computing/Networking, Quantum Computing and Networking, Distributed Systems

- [Resource Allocation for Surface Code Teleportation in Distillation-Based Quantum Networks](https://doi.org/10.1109/2575-8411.2026.00098)
  - Tianjie Hu, Jindi Wu, Qun Li。
  - 该工作研究应用/数字孪生 1 : Quantum Computing and Networking中的「基于蒸馏的量子网络中表面代码隐形传态的资源分配」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「基于蒸馏的量子网络中表面代码隐形传态的资源分配」中的特定状态、约束或操作变成一级设计对象。
  - Quantum Computing/Networking, Quantum Computing and Networking, Distributed Systems

- [AURORA-Q: Asynchronous Unified Resource Optimizer for Quantum Simulation on HPC System](https://doi.org/10.1109/2575-8411.2026.00099)
  - Changjong Kim, Alex Sim, Kesheng Wu, Houjun Tang, Yongseok Son, Jisung Park, Sunggon Kim；Seoul National University of Science and Technology; Lawrence Berkeley National Laboratory; Chung-Ang University; Pohang University of Science and Technology。
  - AURORA-Q研究应用/数字孪生 1 : Quantum Computing and Networking中的「AURORA-Q：用于 HPC 系统量子模拟的异步统一资源优化器」：以 quantum circuit/job、qubit/entanglement 资源和网络路径为对象，决定编译、放置、路由或经典–量子协同。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较把相互影响的子问题分开优化，核心创新是在同一目标下联合决定原本分离的放置、调度、通信或保护策略。
  - Quantum Computing/Networking, Quantum Computing and Networking, Distributed Systems

- [Resource Allocation for Distributed Fault-Tolerant Quantum Computing With Surface Codes](https://doi.org/10.1109/2575-8411.2026.00100)
  - Xu Xu, Yu Liu, Yingling Mao, Yuanyuan Yang；Stony Brook University; Hong Kong Polytechnic University。
  - 该工作研究应用/数字孪生 1 : Quantum Computing and Networking中的「使用表面代码进行分布式容错量子计算的资源分配」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。直接目标是改善故障下的可用性与正确性。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Quantum Computing/Networking, Quantum Computing and Networking, Distributed Systems

- [GBSI: A GPU-Based Secondary Indexing Mechanism for Write-Intensive Workloads](https://doi.org/10.1109/2575-8411.2026.00101)
  - Yijie Zhang, Jiqing Song, Ji Li, Chuanwen Li, Shuai Tang, Yu Gu, Guodong Wang；School of Computer Science and Engineering, Northeastern University; Northeastern University。
  - GBSI研究区块链 3 : 区块链 and Accelerations中的「GBSI：针对写入密集型工作负载的基于 GPU 的二级索引机制」：以 block/object/record 或 checkpoint state 为单位，组织读写、编码、复制、索引或恢复路径。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「GBSI：针对写入密集型工作负载的基于 GPU 的二级索引机制」中的特定状态、约束或操作变成一级设计对象。
  - GPU/Accelerator Systems, Blockchain, Blockchains and Accelerations, Distributed Systems

- [cGraph: A Compact and Efficient Graph-Based Index for Approximate Nearest Neighbor Search](https://doi.org/10.1109/2575-8411.2026.00102)
  - Yu Liu, Mengbai Xiao, Jing Qiao, Yuan Yuan, Qi Luo, Guanghui Zhang, Dongxiao Yu；School of Computer Science and Technology, Shandong University。
  - cGraph研究区块链 3 : 区块链 and Accelerations中的「cGraph：一种紧凑且高效的基于图的索引，用于近似最近邻搜索」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善吞吐、扩展性或资源效率。
  - 相较直接套用通用分布式策略，核心创新是把「cGraph：一种紧凑且高效的基于图的索引，用于近似最近邻搜索」中的特定状态、约束或操作变成一级设计对象。
  - Blockchain, Blockchains and Accelerations, Distributed Systems

- [MosaicDB: Elastic FPGA Acceleration for Unmodified Database Engines](https://icdcs2026.icdcs.org/program/main-technical-sessions/)
  - Rui Li and Shuang Cao。
  - MosaicDB研究区块链 3 : 区块链 and Accelerations中的「MosaicDB：针对未修改数据库引擎的弹性 FPGA 加速」：以 block/object/record 或 checkpoint state 为单位，组织读写、编码、复制、索引或恢复路径。直接目标是改善吞吐、扩展性或资源效率。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - Storage/Data Systems, Blockchain, Blockchains and Accelerations, Distributed Systems

- [When Truth is Unverifiable: A Reputation-Based Oracle with Provable Equilibrium and Incentive-Compatible Aggregation](https://doi.org/10.1109/2575-8411.2026.00103)
  - Xiaoqin Feng, Zixuan Cheng；School of Information Science & Engineering, Lanzhou University。
  - When Truth is Unverifiable研究区块链 3 : 区块链 and Accelerations中的「当真相无法验证时：具有可证明均衡和激励兼容聚合的基于声誉的预言机」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「当真相无法验证时：具有可证明均衡和激励兼容聚合的基于声誉的预言机」中的特定状态、约束或操作变成一级设计对象。
  - Blockchain, Blockchains and Accelerations, Distributed Systems

- [FedRFF: Enhanced Federated Random Fourier Feature Framework for IoT Anomaly Detection](https://doi.org/10.1109/2575-8411.2026.00104)
  - Chaoqun Li, Tao Luo, Keyuan Qiu, Jinyao Liu, Xianglong Zhang, Huanle Zhang, Si Wu, Feng Li, Pengfei Hu；School of Computer Science and Technology, Shandong University; College of Information Science and Technology, Shihezi University; Intitute for Network Sciences and Cyberspace, Tsinghua University。
  - FedRFF研究IoT/CPS 2 : Industrial IoT中的「FedRFF：用于物联网异常检测的增强型联合随机傅立叶特征框架」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「FedRFF：用于物联网异常检测的增强型联合随机傅立叶特征框架」中的特定状态、约束或操作变成一级设计对象。
  - Federated Learning, IoT/CPS, Industrial IoT, Distributed Systems

- [ARTSN: Exact and Adaptive Self-Triggered Traffic Scheduling for ARTS Networks](https://doi.org/10.1109/2575-8411.2026.00105)
  - Ruide Cao, Shuangping Zhan, Jiashuo Lin, Yan Liu, Chenxi Ling, Yi Wang, Guoming Tang；Southern University of Science and Technology; Pengcheng Laboratory; Hanshan Normal University; The Hong Kong University of Science and Technology (Guangzhou)。
  - ARTSN研究IoT/CPS 2 : Industrial IoT中的「ARTSN：ARTS 网络的精确自适应自触发流量调度」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - IoT/CPS, Scheduling, Industrial IoT, Distributed Systems

- [ChainCred: Enforcing Comprehensive Credential Disclosure in WEB3 Systems](https://doi.org/10.1109/2575-8411.2026.00106)
  - Rui Song, Bin Xiao, Yu Liu, Yuanyuan Yang；The Hong Kong Polytechnic University; Stony Brook University。
  - ChainCred研究IoT/CPS 2 : Industrial IoT中的「ChainCred：在 WEB3 系统中实施全面的凭证披露」：从用户/设备/代理的观测、credential 或时序行为中给出连续身份判定与验证。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「ChainCred：在 WEB3 系统中实施全面的凭证披露」中的特定状态、约束或操作变成一级设计对象。
  - IoT/CPS, Industrial IoT, Distributed Systems

- [Integrated Load-Balanced Scheduling for Human-Vehicle Collaborative Urban Sanitation](https://doi.org/10.1109/2575-8411.2026.00107)
  - Lingzi Zhao, Huali Lu, Hao Wu, Shucheng Li, Longye Li, Tao He, Wenlong Liao, Feng Lyu；School of Computer Science and Engineering, Central South University; Nanjing University; COWAROBOT。
  - 该工作研究IoT/CPS 2 : Industrial IoT中的「人车协同城市环卫综合负载均衡调度」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较把相互影响的子问题分开优化，核心创新是在同一目标下联合决定原本分离的放置、调度、通信或保护策略。
  - IoT/CPS, Mobile/Space Networks, Scheduling, Industrial IoT

- [Distributed Covert Link Scheduling in Open Wireless Networks](https://doi.org/10.1109/2575-8411.2026.00108)
  - Li Yang, Yuhang Zhang, Yifei Zou, Hui Ge, Xingquan Li, Jia Yu, Dongxiao Yu；Qingdao University; Shandong University; China Unicom; Southeast University。
  - 该工作研究边缘计算 6 : Learning in Edge-AI中的「开放无线网络中的分布式隐蔽链路调度」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Edge Computing, Scheduling, Learning in Edge-AI, Distributed Systems

- [Physics-Inspired Decomposition for Weak Low-Rank Spatiotemporal Completion in Sparse Crowdsensing](https://doi.org/10.1109/2575-8411.2026.00109)
  - Mijia Zhang, En Wang, Wenbin Liu, Junwei Zhao, Yang Xu, Bo Yang, Jie Wu；College of Computer Science and Technology, Jilin University; China Telecom Cloud Computing Research Institute; College of Computer Science and Electronic Engineering, Hunan University。
  - 该工作研究边缘计算 6 : Learning in Edge-AI中的「稀疏人群感知中弱低阶时空完成的物理启发分解」：将终端位置/移动、传感数据、链路和能量状态一起带入感知、通信或计算决策。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「稀疏人群感知中弱低阶时空完成的物理启发分解」中的特定状态、约束或操作变成一级设计对象。
  - Edge Computing, IoT/CPS, Learning in Edge-AI, Distributed Systems

- [Graph Attention-Based Cooperative Multi-Agent Reinforcement Learning for Low-Latency Reliable Task Replication in Mobile Edge Computing](https://doi.org/10.1109/2575-8411.2026.00110)
  - Anam Nasir, Xiang He, Teng Wang, Haomai Shi, Zhongjie Wang；Harbin Institute of Technology。
  - 该工作研究边缘计算 6 : Learning in Edge-AI中的「基于图注意力的协作多智能体强化学习，用于移动边缘计算中的低延迟可靠任务复制」：将终端位置/移动、传感数据、链路和能量状态一起带入感知、通信或计算决策。题目明确的关键手段包括强化学习、graph attention；直接目标是改善请求时延或任务完成时间。
  - 相较把相互影响的子问题分开优化，核心创新是在同一目标下联合决定原本分离的放置、调度、通信或保护策略。
  - Multi-Agent Systems, Edge Computing, Reinforcement Learning, Learning in Edge-AI

- [BridgeLoRA: Privacy-Preserving Collaborative Skip-Layer Connectors for Efficient Transformer Fine-Tuning at the Edge](https://doi.org/10.1109/2575-8411.2026.00111)
  - Vilhelm Toivonen, Xiang Su, Xiaoli Liu, Sasu Tarkoma, Pan Hui；University of Helsinki; The Hong Kong University of Science and Technology (Guangzhou)。
  - BridgeLoRA研究边缘计算 6 : Learning in Edge-AI中的「BridgeLoRA：保护隐私的协作跳层连接器，用于在边缘进行高效变压器微调」：以在线模型请求为单位，组织模型/算子放置、并行执行、状态缓存和请求排队。直接目标是改善安全、隐私或可验证性。
  - 相较把相互影响的子问题分开优化，核心创新是在同一目标下联合决定原本分离的放置、调度、通信或保护策略。
  - Edge Computing, Privacy, Learning in Edge-AI, Distributed Systems

- [Minimizing Qubit Overhead in Error-Aware Distributed Quantum Computing](https://doi.org/10.1109/2575-8411.2026.00112)
  - Ranjani G. Sundaram, Himanshu Gupta；Stony Brook University。
  - 该工作研究容错 and Big Data : 容错 and Big Data中的「最小化错误感知分布式量子计算中的量子位开销」：以 quantum circuit/job、qubit/entanglement 资源和网络路径为对象，决定编译、放置、路由或经典–量子协同。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Quantum Computing/Networking, Fault Tolerance and Big Data, Distributed Systems

- [COAR: Computation-Aware Erasure-Coded Repair in Storage Clusters for Distributed Data Analytics](https://doi.org/10.1109/2575-8411.2026.00113)
  - Mingqi Li, Yuchong Hu, Lin Wang, Chenxuan Yao, Patrick P. C. Lee, Dan Feng；Huazhong University of Science and Technology; The Chinese University of Hong Kong。
  - COAR研究容错 and Big Data : 容错 and Big Data中的「COAR：存储集群中用于分布式数据分析的计算感知纠删码修复」：以 block/object/record 或 checkpoint state 为单位，组织读写、编码、复制、索引或恢复路径。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Storage/Data Systems, Fault Tolerance and Big Data, Distributed Systems

- [Deceptive Electricity Theft: New Attacks and Countermeasures in Multiple-Pricing Smart Grids](https://doi.org/10.1109/2575-8411.2026.00114)
  - Chengpeng Huang, Shang Gao, Qingqing Gan, Guyue Li, Bin Xiao；The Hong Kong Polytechnic University; Guangdong University of Foreign Studies; Southeast University。
  - Deceptive Electricity Theft研究容错 and Big Data : 容错 and Big Data中的「欺骗性窃电：多定价智能电网中的新攻击和对策」：指定对手可观测/篡改的数据和攻击面，再把检测、隔离、加密或隐私保护插入具体数据路径。直接目标是改善安全、隐私或可验证性。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Security, Fault Tolerance and Big Data, Distributed Systems

- [PARS: Optimizing High-Dimensional Vector Search with Dimensional Reduction and Ray Tracing Core](https://doi.org/10.1109/2575-8411.2026.00115)
  - Yiling Ma, Mengbai Xiao, Zhixiong Xiao, Yuan Yuan, Dongxiao Yu, Guanghui Zhang, Feng Li；Shandong University。
  - PARS研究容错 and Big Data : 容错 and Big Data中的「PARS：利用降维和光线追踪核心优化高维矢量搜索」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「PARS：利用降维和光线追踪核心优化高维矢量搜索」中的特定状态、约束或操作变成一级设计对象。
  - Fault Tolerance and Big Data, Distributed Systems

- [AgentDID: Trustless Identity Authentication for AI Agents](https://doi.org/10.1109/2575-8411.2026.00116)
  - Minghui Xu, Xiaoyu Liu, Yihao Guo, Chunchi Liu, Yue Zhang, Xiuzhen Cheng；Shandong University; The Hong Kong Polytechnic University; Huawei Technologies Co., Ltd。
  - AgentDID 为可按需创建、跨平台迁移、身份短生命的 AI Agent 提供无中心注册的认证。Agent 以 W3C DID 和 verifiable credential 自管身份/能力声明；交互时 verifier 用 challenge–response 不仅验签，还检查 context、工具/能力等动态执行状态仍有效。
  - 相较面向人或静态主机、依赖持久标识与中心 enrollment 的 IAM，核心创新是把 Agent 的短生命自主身份和「此刻执行状态」合并为可验证对象。
  - Agent Infra, Agent Identity, Decentralized Identifiers, Verifiable Credentials, Runtime State Verification

- [Trustworthy-PWS: An Operator-Agnostic Public Warning System (PWS) Security Architecture in 5G](https://doi.org/10.1109/2575-8411.2026.00117)
  - Sourav Purification, Sang-Yoon Chang；University of Colorado。
  - Trustworthy-PWS研究安全/隐私/信任 4 : Authentication in Security中的「Trustworthy-PWS：5G 中与运营商无关的公共预警系统 (PWS) 安全架构」：指定对手可观测/篡改的数据和攻击面，再把检测、隔离、加密或隐私保护插入具体数据路径。直接目标是改善安全、隐私或可验证性。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Privacy, Security, Authentication in Security, Distributed Systems

- [A Robust and Secure Decentralized Handover Authentication Scheme for HetNets](https://doi.org/10.1109/2575-8411.2026.00118)
  - Wenhao Wang, Yu Li, Minze Xu, Kang Liu, Yuan Zhang, Sheng Zhong；Nanjing University; The Hong Kong Polytechnic University。
  - 该工作研究安全/隐私/信任 4 : Authentication in Security中的「一种健壮、安全的异构网络去中心化切换认证方案」：从用户/设备/代理的观测、credential 或时序行为中给出连续身份判定与验证。直接目标是改善安全、隐私或可验证性。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Privacy, Security, Authentication in Security, Distributed Systems

- [GumSwap: Griefing-Free Universal Multi-Party Atomic Swaps](https://doi.org/10.1109/2575-8411.2026.00119)
  - Dongkun Hou, Yuanzhe Zhang, Shujie Cui, Tsz Hon Yuen, Joseph K. Liu, Jiangshan Yu；Monash University; Nanyang Technological University; The University of Sydney。
  - GumSwap研究安全/隐私/信任 4 : Authentication in Security中的「GumSwap：无忧的通用多方原子交换」：以交易、账户、shard/chain 和验证消息为对象，设计执行、路由、原子性或激励机制。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「GumSwap：无忧的通用多方原子交换」中的特定状态、约束或操作变成一级设计对象。
  - Privacy, Security, Authentication in Security, Distributed Systems

- [Fast Semantic Retrieval with Balanced Load and Implicit Privacy in Large-Scale Internet of Agents](https://doi.org/10.1109/2575-8411.2026.00120)
  - Jinkai Zheng, Tom H. Luan, Yuan Chang, Yuntao Wang, Zhendong Li, Haixia Peng, Xianhua Yu, Nan Cheng, Zhou Su；School of Cyber Science and Engineering, Xi'an Jiaotong University; School of Information and Communication Engineering, Xi'an Jiaotong University; School of Electrical Engineering and Intelligentization, Dongguan University of Technology; School of Telecommunications Engineering, Xidian University。
  - 该工作面向服务机器人、软件 Agent 和智能设备组成的大规模 Internet of Agents，让查询 Agent 在不暴露 query 和本地内容的情况下发现持有所需语义信息的同伴。每个 Agent 根据语义相似度与局部负载联合选择下一跳，使覆盖网络自组织为搜索高效且负载均衡的结构。
  - 相较固定 routing metric 或中心化语义目录，核心创新是用查询驱动的分布式选择同时编排 semantic relevance、agent load 和隐私，并对自组织收敛给出分析。
  - Agent Infra, Internet of Agents, Semantic Retrieval, Load Balancing, Implicit Privacy

- [LSCFL: Clustered Federated Learning with Label Semantics for Label-Skewed Non-IID Data](https://doi.org/10.1109/2575-8411.2026.00121)
  - Jiaxin Liu, Chunqiang Hu, Hui Xia, Meng Han, Ruinian Li, Jiguo Yu；Chongqing University; Ocean University of China; Zhejiang University; Bowling Green State University; University of Electronic Science and Technology of China。
  - LSCFL研究AI 5 : Semantic AI中的「LSCFL：针对标签倾斜非独立同分布数据的具有标签语义的集群联合学习」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「LSCFL：针对标签倾斜非独立同分布数据的具有标签语义的集群联合学习」中的特定状态、约束或操作变成一级设计对象。
  - Federated Learning, Semantic AI, Distributed Systems

- [Towards Semantic-Aware Edge-Cloud Collaboration for Cost-Efficient Video Understanding](https://doi.org/10.1109/2575-8411.2026.00122)
  - Cheng Pan, Cong Zhang, Danyang Song, Handi Chen, Edith C. H. Ngai, Jiangchuan Liu, Victor C. M. Leung；The University of Hong Kong; Jiangxing Intelligence Inc; School of Computing Science, Simon Fraser University; The University of British Columbia。
  - 该工作研究AI 5 : Semantic AI中的「实现语义感知的边缘云协作以实现经济高效的视频理解」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善资源/货币成本。
  - 相较直接套用通用分布式策略，核心创新是把「实现语义感知的边缘云协作以实现经济高效的视频理解」中的特定状态、约束或操作变成一级设计对象。
  - Edge Computing, Semantic AI, Distributed Systems

- [FloodGuard: A Prediction-Control Closed Loop for Mitigating Cold-Start Floods in Cloud Services](https://doi.org/10.1109/2575-8411.2026.00123)
  - Jiacheng Cui, Yuwei Li, Junyu Xue, Guoming Tang；The Hong Kong University of Science and Technology (Guangzhou); Southern University of Science and Technology。
  - FloodGuard研究AI 5 : Semantic AI中的「FloodGuard：用于缓解云服务中冷启动洪水的预测控制闭环」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「FloodGuard：用于缓解云服务中冷启动洪水的预测控制闭环」中的特定状态、约束或操作变成一级设计对象。
  - Semantic AI, Distributed Systems

- [ObliMIG: Enabling Data Migration on Oblivious Storage without Interruption](https://doi.org/10.1109/2575-8411.2026.00124)
  - Bo Zhang, Helei Cui, Zhe Peng, Yu Hua, Zhiwen Yu, Bin Guo；Northwestern Polytechnical University; The Hong Kong Polytechnic University; Huazhong University of Science and Technology。
  - ObliMIG研究边缘计算 7 : Storage in 边缘计算中的「ObliMIG：在 Oblivious 存储上实现不间断数据迁移」：以 block/object/record 或 checkpoint state 为单位，组织读写、编码、复制、索引或恢复路径。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「ObliMIG：在 Oblivious 存储上实现不间断数据迁移」中的特定状态、约束或操作变成一级设计对象。
  - Edge Computing, Storage/Data Systems, Storage in Edge Computing, Distributed Systems

- [THEIA: Scalable and Effective Data Prefetching for Geo-Distributed Erasure-Coded Storage](https://doi.org/10.1109/2575-8411.2026.00125)
  - Marc Tranzer, Shadi Ibrahim；Inria, Univ. Rennes, CNRS, IRISA。
  - THEIA研究边缘计算 7 : Storage in 边缘计算中的「THEIA：用于地理分布式纠删码存储的可扩展且有效的数据预取」：以 block/object/record 或 checkpoint state 为单位，组织读写、编码、复制、索引或恢复路径。直接目标是改善吞吐、扩展性或资源效率。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Edge Computing, Storage/Data Systems, Storage in Edge Computing, Distributed Systems

- [SpecPool: Storage-Layer Speculation for Parallel Smart Contract Execution](https://doi.org/10.1109/2575-8411.2026.00126)
  - Francisco Rola, Miguel Matos, Michał Nazarewicz, Paolo Romano；University of Lisbon; No affiliation。
  - SpecPool研究边缘计算 7 : Storage in 边缘计算中的「SpecPool：并行智能合约执行的存储层推测」：以 block/object/record 或 checkpoint state 为单位，组织读写、编码、复制、索引或恢复路径。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「SpecPool：并行智能合约执行的存储层推测」中的特定状态、约束或操作变成一级设计对象。
  - Edge Computing, Storage/Data Systems, Storage in Edge Computing, Distributed Systems

- [ClusterLess: Deadline-Aware Serverless Workflow Orchestration on Federated Edge Clusters](https://doi.org/10.1109/2575-8411.2026.00127)
  - Reza Farahani, Mario Colosi, Ilir Murturi, Stefan Nastic, Massimo Villari, Schahram Dustdar, Radu Prodan；TU Wien; University of Messina; University of Prishtina; University of Innsbruck。
  - ClusterLess研究边缘计算 7 : Storage in 边缘计算中的「ClusterLess：联合边缘集群上的截止日期感知无服务器工作流编排」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。题目明确的关键手段包括federated aggregation；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「ClusterLess：联合边缘集群上的截止日期感知无服务器工作流编排」中的特定状态、约束或操作变成一级设计对象。
  - Federated Learning, Edge Computing, Serverless Computing, Storage/Data Systems

- [Network Digital Untwinning: Towards Backward Optimization of Digital Twins](https://doi.org/10.1109/2575-8411.2026.00128)
  - Zifan Zhang, Dianwei Chen, Anjun Gao, Manhua Wang, Mingzhe Chen, Minghong Fang, Xianfeng Yang, Yuchen Liu；North Carolina State University; University of Maryland; University of Louisville; University of Michigan; University of Miami。
  - Network Digital Untwinning研究应用/数字孪生 2 : Computing Optimization for Digital Twins中的「网络数字孪生：迈向数字孪生的后向优化」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「网络数字孪生：迈向数字孪生的后向优化」中的特定状态、约束或操作变成一级设计对象。
  - Digital Twin, Computing Optimization for Digital Twins, Distributed Systems

- [Chimera: An Efficient Multimodal Embodied Inference Framework with Complexity-Aware Edge-Cloud Routing](https://doi.org/10.1109/2575-8411.2026.00129)
  - Siqi Luo, Muen Xue, Liekang Zeng, Tao Ouyang, Pu Wang, Shaoyong Guo, Xu Chen；School of Computer Science and Engineering, Sun Yat-sen University; The Chinese University of Hong Kong; School of Electronic Information, Central South University; CSG Electric Power Research Institute; School of Computer Science, Beijing University of Posts and Telecommunications。
  - Chimera研究应用/数字孪生 2 : Computing Optimization for Digital Twins中的「Chimera：具有复杂性感知边缘云路由的高效多模态推理框架」：以在线模型请求为单位，组织模型/算子放置、并行执行、状态缓存和请求排队。直接目标是改善吞吐、扩展性或资源效率。
  - 相较直接套用通用分布式策略，核心创新是把「Chimera：具有复杂性感知边缘云路由的高效多模态推理框架」中的特定状态、约束或操作变成一级设计对象。
  - Edge Computing, Digital Twin, Computing Optimization for Digital Twins, Distributed Systems

- [Panorama: LLM-Guided Heuristics for Digital Twin-Empowered Vehicular Edge Computing](https://doi.org/10.1109/2575-8411.2026.00130)
  - Ziyao Huang, Kui Wu, Weiwei Wu, Xiangtong Qi, Jianping Wang, Jen-Ming Wu；City University of Hong Kong; University of Victoria; Southeast University; Hong Kong University of Science and Technology; Hon Hai (Foxconn) Research Institute。
  - Panorama 面向数字孪生车联网中多基站子信道分配，用 Age of Fusible Information 同时度量数据新鲜度和多源时间对齐。多 Agent automatic heuristic design 在 centralized panorama diagnostic signal 的反馈下，让 LLM 反复生成、评估并改进可解释启发式，应对跨基站干扰、多对多关系和车辆移动。
  - 相较手工启发式或难解释的在线 learning policy，核心创新是用有诊断反馈的多 Agent 搜索自动设计能跨未见场景泛化的资源分配规则。
  - Agent for Systems, Automatic Heuristic Design, Vehicular Edge, Digital Twin, Subchannel Allocation

- [Optimizing Wide-Area Collective Communication via Flow-Dependency-Aware Rate Allocation](https://doi.org/10.1109/2575-8411.2026.00131)
  - Yining Wang, Toon Craps, Baochun Li；University of Toronto。
  - 该工作研究应用/数字孪生 2 : Computing Optimization for Digital Twins中的「通过流量依赖感知速率分配优化广域集体通信」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。直接目标是改善通信量与同步等待。
  - 相较直接套用通用分布式策略，核心创新是把「通过流量依赖感知速率分配优化广域集体通信」中的特定状态、约束或操作变成一级设计对象。
  - Digital Twin, Computing Optimization for Digital Twins, Distributed Systems

- [Coordinating Traffic at Group Granularity for Tail Latency Control in Service Meshes](https://doi.org/10.1109/2575-8411.2026.00132)
  - Hokun Park, HyungJun Kim, Hwamin Lee, Heonchang Yu；Korea University。
  - 该工作研究云计算 3 : Latency Control in Distributed Computing中的「以组粒度协调流量以实现服务网格中的尾部延迟控制」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善请求时延或任务完成时间。
  - 相较直接套用通用分布式策略，核心创新是把「以组粒度协调流量以实现服务网格中的尾部延迟控制」中的特定状态、约束或操作变成一级设计对象。
  - Latency Control in Distributed Computing, Distributed Systems

- [Task Scheduling and Transmission for Distributed Job Execution](https://doi.org/10.1109/2575-8411.2026.00133)
  - Shangyi Shao, Xueyan Tang；Nanyang Technological University。
  - 该工作研究云计算 3 : Latency Control in Distributed Computing中的「分布式作业执行的任务调度和传输」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Scheduling, Latency Control in Distributed Computing, Distributed Systems

- [EdgeTP: Enabling Distributed Full-size Large Language Model Inference on Edge Devices with Tensor Parallelism](https://doi.org/10.1109/2575-8411.2026.00134)
  - Laizhong Cui, Yi Guo, Weixuan Peng, Yaodong Huang；Guangdong Laboratory of Artificial Intelligence and Digital Economy (SZ); College of Computer Science and Software Engineering, Shenzhen University。
  - EdgeTP研究云计算 3 : Latency Control in Distributed Computing中的「EdgeTP：通过张量并行在边缘设备上实现分布式全尺寸大型语言模型推理」：以在线模型请求为单位，组织模型/算子放置、并行执行、状态缓存和请求排队。题目明确的关键手段包括tensor parallelism；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - LLM Systems, Edge Computing, Latency Control in Distributed Computing, Distributed Systems

- [PipeNN: A Predictor-Free Pipeline for Energy-Latency Co-Optimization of Heterogeneous Mobile DAG-DNN Inference](https://doi.org/10.1109/2575-8411.2026.00135)
  - Yukun Tian, Tianwei Jiang, Kun Tian, Ruiting Zhou, Yunxin Liu, Zhi Zhou, Fang Dong, Mengyang Liu, Wentao Liu；School of Computer Science and Engineering, Southeast University; Southeast University Shenzhen Research Institute; Institute for AI Industry Research (AIR), Tsinghua University; School of Computer Science and Engineering, Sun Yat-sen University; University of Macau。
  - PipeNN研究云计算 3 : Latency Control in Distributed Computing中的「PipeNN：用于异构移动 DAG-DNN 推理能量延迟协同优化的无预测器管道」：以在线模型请求为单位，组织模型/算子放置、并行执行、状态缓存和请求排队。题目明确的关键手段包括pipeline；直接目标是改善请求时延或任务完成时间。
  - 相较直接套用通用分布式策略，核心创新是把「PipeNN：用于异构移动 DAG-DNN 推理能量延迟协同优化的无预测器管道」中的特定状态、约束或操作变成一级设计对象。
  - Latency Control in Distributed Computing, Distributed Systems

- [PR-Reduce: Heterogeneity-Aware Proportional Allreduce for Distributed Training](https://doi.org/10.1109/2575-8411.2026.00136)
  - Yi-Ching Kuo, Kate Ching-Ju Lin；National Yang Ming Chiao Tung University; National Taiwan University。
  - PR-Reduce研究AI 6 : Distributed Learning in AI中的「PR-Reduce：用于分布式训练的异构感知比例 Allreduce」：以 worker、model shard/layer、gradient 或 expert 为单位组织计算、集合通信、内存与容错状态。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Distributed Learning in AI, Distributed Systems

- [From Ranking to Reasoning: Explainable Web API Recommendation via Semantic Reasoning](https://doi.org/10.1109/2575-8411.2026.00137)
  - Zishuo Xu, Dezhong Yao, Yao Wan；School of Software Engineering, Huazhong University of Science and Technology; School of Computer Science and Technology, Huazhong University of Science and Technology。
  - From Ranking to Reasoning研究AI 6 : Distributed Learning in AI中的「从排名到推理：通过语义推理进行可解释的 Web API 推荐」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「从排名到推理：通过语义推理进行可解释的 Web API 推荐」中的特定状态、约束或操作变成一级设计对象。
  - Distributed Learning in AI, Distributed Systems

- [Fast-DFL: Flexible Client Switching for Bandwidth-Constrained Hierarchical Decentralized Federated Learning](https://doi.org/10.1109/2575-8411.2026.00138)
  - Zhongkun Wang, Hailiang Yang, Laizhong Cui；Guangdong Laboratory of Artificial Intelligence and Digital Economy (SZ); College of Computer Science and Software Engineering, Shenzhen University。
  - Fast-DFL研究AI 6 : Distributed Learning in AI中的「Fast-DFL：带宽受限的分层去中心化联邦学习的灵活客户端切换」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善通信量与同步等待。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Federated Learning, Distributed Learning in AI, Distributed Systems

- [GALUPA: Gossiping Aggregated Locking and Output Proofs for Accountability in BFT](https://doi.org/10.1109/2575-8411.2026.00139)
  - Baolin Li, Huiping Sun, Zhong Chen；School of Computer Science, Peking University; School of Software & Microelectronics, Peking University。
  - GALUPA研究AI 6 : Distributed Learning in AI中的「GALUPA：八卦聚合锁定和 BFT 问责制输出证明」：在节点失效或拜占庭作恶假设下组织 message/quorum/round，保证 agreement、liveness 或故障检测。题目明确的关键手段包括consensus/BFT；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「GALUPA：八卦聚合锁定和 BFT 问责制输出证明」中的特定状态、约束或操作变成一级设计对象。
  - Byzantine Fault Tolerance, Distributed Learning in AI, Distributed Systems

- [A Hybrid Blockchain Design Integrating Proof-of-Work and Proof-of-Quantum-Work Consensus](https://doi.org/10.1109/2575-8411.2026.00140)
  - Jiarui Zhang, Yiming Zeng, Yuanyuan Yang；Stony Brook University。
  - 该工作研究边缘计算 8 : Edge-AI and Quantum Computing中的「集成工作量证明和量子工作量证明共识的混合区块链设计」：以交易、账户、shard/chain 和验证消息为对象，设计执行、路由、原子性或激励机制。题目明确的关键手段包括consensus/BFT；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「集成工作量证明和量子工作量证明共识的混合区块链设计」中的特定状态、约束或操作变成一级设计对象。
  - Edge Computing, Blockchain, Byzantine Fault Tolerance, Quantum Computing/Networking

- [TrustMix: How to Mix Messages in a Mobile Ad-Hoc Network](https://doi.org/10.1109/2575-8411.2026.00141)
  - Yu Shen, Stefanie Roos, Aiswarya Walter；RPTU University Kaiserslautern-Landau。
  - TrustMix研究边缘计算 8 : Edge-AI and Quantum Computing中的「TrustMix：如何在移动自组织网络中混合消息」：将终端位置/移动、传感数据、链路和能量状态一起带入感知、通信或计算决策。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「TrustMix：如何在移动自组织网络中混合消息」中的特定状态、约束或操作变成一级设计对象。
  - Edge Computing, Quantum Computing/Networking, Edge-AI and Quantum Computing, Distributed Systems

- [Cappuccino: Cost-Efficient Heterogeneous Lora Fine-Tuning Via Replica-Level Orchestration](https://doi.org/10.1109/2575-8411.2026.00142)
  - Lingxuan Weng, Fei Xu, Xudong Wu, Xinyi Zhang, Shiqi Cheng, Li Chen, Zhi Zhou；East China Normal University; University of Louisiana at Lafayette; Sun Yat-sen University。
  - Cappuccino研究边缘计算 8 : Edge-AI and Quantum Computing中的「Cappuccino：通过副本级编排进行经济高效的异构 Lora 微调」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。直接目标是改善资源/货币成本。
  - 相较直接套用通用分布式策略，核心创新是把「Cappuccino：通过副本级编排进行经济高效的异构 Lora 微调」中的特定状态、约束或操作变成一级设计对象。
  - Edge Computing, Quantum Computing/Networking, Edge-AI and Quantum Computing, Distributed Systems

- [Scale: Sensitivity-Aware Federated Unlearning with Information Freshness Optimization for Mobile Edge Computing](https://doi.org/10.1109/2575-8411.2026.00143)
  - Zihao Ding, Beining Wu, Jun Huang；South Dakota State University。
  - Scale研究边缘计算 8 : Edge-AI and Quantum Computing中的「规模：移动边缘计算的敏感度感知联合遗忘和信息新鲜度优化」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「规模：移动边缘计算的敏感度感知联合遗忘和信息新鲜度优化」中的特定状态、约束或操作变成一级设计对象。
  - Federated Learning, Edge Computing, Quantum Computing/Networking, Edge-AI and Quantum Computing
