# SIGMETRICS 2025 论文列表

## 范围与核验

[SIGMETRICS 2025 官方 Accepted Papers](https://www.sigmetrics.org/sigmetrics2025/accepted_papers.html) 共列出 66 篇受邀在本届报告的正式论文：Summer 20 篇、Fall 15 篇、Winter 31 篇。本文只收录这些正式论文，不含 poster、SRC、workshop、tutorial 或 keynote。标题和作者逐项与 DOI 元数据及 POMACS OpenTOC 交叉核验；其中 61 篇为 POMACS 正式论文，另有 5 篇发表于 ACM SIGMETRICS Performance Evaluation Review 的 archival summary，后者在标签中单独标明，不能与常规 POMACS 全文混为一类。

标题均链接到 DOI 落地页。本地已保留并验证 23 份合法开放 PDF，目录为 `reference/SIGMETRICS/2025/`；其余条目以 DOI 摘要和官方元数据完成预读，不以 PDF 获取失败阻塞清单。

方向计数采用互斥主方向：每篇只按核心研究对象计入一类，因此跨方向工作不会重复累计。

| 主方向 | 论文数 | 占比 |
|---|---:|---:|
| 排队、调度与在线优化 | 16 | 24.2% |
| 网络测量、协议与基础设施 | 13 | 19.7% |
| 云、存储与系统运行时 | 11 | 16.7% |
| 机器学习系统与联邦学习 | 7 | 10.6% |
| 安全、隐私与区块链 | 7 | 10.6% |
| 量子与新型计算 | 6 | 9.1% |
| 公平分配、市场与博弈 | 5 | 7.6% |
| 可持续计算 | 1 | 1.5% |

年度观察：

- 排队、调度与在线优化是最大方向（16/66，24.2%），网络测量与协议（13/66）及云/存储/运行时（11/66）紧随其后；三类合计 40/66（60.6%），说明会议重心仍是可证明的性能模型、在线决策和真实系统测量。
- 热门方法不是单一模型，而是 learning-augmented online algorithm、竞争/排队分析、生产 trace 与主动测量、以及硬件—软件协同。预测主要被当作带最坏界的辅助信号，而不是无约束替代系统策略。
- 机器学习系统主要落在 GNN/PIM、联邦学习、serverless ML、故障预测和系统 surrogate；该届没有以 LLM serving 或 LLM Agent 为核心的论文。

Agent 相关分类：

| 分类 | 论文数 | 对应论文或边界 |
|---|---:|---|
| Agent System | 0 | 无 |
| Agent Infra | 0 | 无 |
| Agent for Systems | 0 | 无 |
| LLM for Systems | 0 | 无 |

标题中的 multi-agent bandit、网络化多主体优化和传统强化学习均是数学决策主体或控制策略，不属于这里的 LLM Agent 四分类。

## 论文条目

### Summer Deadline（20 篇）

- [Learning-Augmented Decentralized Online Convex Optimization in Networks](https://doi.org/10.1145/3700420)
  - Pengfei Li (UC Riverside); Jianyi Yang (University of Houston); Adam Wierman (Caltech); Shaolei Ren (UC Riverside)
  - 在网络化多主体的去中心化在线凸优化中，LADO 按每轮预测质量自适应混合机器学习策略与有最坏界的专家策略，并在节点通信受限时同时控制平均代价和竞争比；论文用分布式电池管理验证预测有用时的收益。
  - 相较固定线性混合预测与基线、因坏预测而失去保证的做法，核心创新是把安全护栏写进在线组合规则，并刻画平均性能与最坏鲁棒性的可调边界。
  - learning-augmented optimization、decentralized control、robustness-consistency

- [Beaver: A High-Performance and Crash-Consistent File System Cache via PM-DRAM Collaborative Memory Tiering](https://doi.org/10.1145/3700414)
  - Qinglin Pan, Ji Qi, Jiatai He, Heng Zhang, Jiageng Yu, Yanjun Wu (Institute of Software, Chinese Academy of Sciences)
  - Beaver 面向需要崩溃一致性的文件系统缓存，把写请求先落到持久内存以保证原子持久化，把读热点放在 DRAM，并由 kprefetcher 在写路径之外异步把数据从 PM 搬到 DRAM；在 RocksDB 和 MinIO 上同时改善读写性能。
  - 相较让一种介质同时承担持久写与高速读，Beaver 首次按访问方向划分 PM/DRAM 职责，并把迁移从写关键路径剥离，从而不以读性能换一致性。
  - file-system cache、persistent memory、crash consistency、memory tiering

- [PyGim: An Efficient Graph Neural Network Library for Real Processing-In-Memory Architectures](https://doi.org/10.1145/3700434)
  - Christina Giannoula, Peiming Yang (University of Toronto); Ivan Fernandez (Barcelona Supercomputing Center); Jiacheng Yang, Sankeerth Durvasula, Yu Xin Li (University of Toronto); Mohammad Sadrosadati (ETH Zürich); Juan Gomez Luna (NVIDIA); Onur Mutlu (ETH Zurich and Stanford University); Gennady Pekhimenko (University of Toronto / Vector Institute)
  - PyGim 把 GNN 的聚合等访存密集 kernel 放到真实 PIM DIMM，把计算密集 kernel 留给主处理器，并依据图与硬件状态自动选择 PIM 并行策略；Python API 在 1992 个 PIM 核上完成端到端协同推理。
  - 相较只在 PIM 上实现单个算子或要求用户手调映射，核心创新是用 cooperative execution 与轻量 autotuner 把异构 kernel 划分、并行化和易用接口组成完整 GNN 库。
  - GNN inference、processing-in-memory、heterogeneous execution、autotuning

- [The Power of Migrations in Dynamic Bin Packing](https://doi.org/10.1145/3700435)
  - Konstantina Mellou, Marco Molinaro (Microsoft Research); Rudy Zhou (Carnegie Mellon University)
  - 该工作研究物品动态到达/离开的 bin packing，在最小化所有 bin 累计开启时间时量化迁移预算：少于线性的迁移与不迁移渐近等价，而约 αn 次迁移可取得约 1/α 的竞争比；另把每次迁移建模为额外停机 C，给出近紧的近似界。
  - 相较只分析零迁移或无限迁移，核心创新是补齐有限迁移的完整相变，并用迁移延迟模型把抽象次数预算改成更接近作业搬迁成本的度量。
  - dynamic bin packing、migration budget、competitive analysis、job placement

- [Modeling and Simulating Rydberg Atom Quantum Computers for Hardware-Software Co-design with PachinQo](https://doi.org/10.1145/3700421)
  - Jason Ludmir, Yuqian Huo, Nicholas S. DiBrita, Tirthak Patel (Rice University)
  - PachinQo 面向 zonal-addressing 的 Rydberg 原子量子机，把任意量子算法的门、原子移动、分区拓扑和噪声参数共同输入架构模拟与编译搜索，选择映射和硬件配置以提高整条电路成功概率。
  - 相较只支持特定算法的现有 zonal 演示，核心创新是把体系结构参数与通用量子编译置于同一 co-design 框架，并以含噪成功率而非理想门数评价设计。
  - Rydberg quantum computing、architecture simulation、compiler co-design、zonal addressing

- [Beyond App Markets: Demystifying Underground Mobile App Distribution Via Telegram](https://doi.org/10.1145/3700432)
  - Yanhui Guo, Dong Wang, Liu Wang, Yongsheng Fang (Beijing University of Posts and Telecommunications); Chao Wang (Huazhong University of Science and Technology); Minghui Yang (OPPO); Tianming Liu (Monash University); Haoyu Wang (Huazhong University of Science and Technology)
  - 该测量工作构建 Telegram 地下移动应用数据集，关联频道、用户、网站和安装包，分析赌博/色情应用的推广网络、iOS 分发滥用、恶意行为与平台审核缺口；频道订阅规模合计约为 Telegram 用户量的 1%。
  - 相较只研究官方/第三方应用市场中的恶意应用，核心创新是把加密消息平台当作分发基础设施，重建跨频道—网站—应用的传播链并量化其生态规模。
  - underground apps、Telegram measurement、mobile security、distribution ecosystem

- [Towards Understanding and Analyzing Instant Cryptocurrency Exchanges](https://doi.org/10.1145/3700430)
  - Yufeng Hu, Yingshi Sun, Lei Wu, Yajin Zhou, Rui Chang (Zhejiang University)
  - 论文识别两类 Instant Cryptocurrency Exchange 服务，结合链上交易与服务流程估计跨链洗钱规模，并用输入输出金额、时间等线索匹配被服务刻意割裂的请求与兑付交易，以追踪恶意资金流。
  - 相较把 ICE 当普通交易所或仅追踪单链地址，核心创新是先建模其 Standalone/Delegated 工作流，再针对缺失 KYC 和不完整链上记录设计跨服务匹配算法。
  - cryptocurrency exchange、money laundering、cross-chain tracing、blockchain measurement

- [Piecing Together the Jigsaw Puzzle of Transactions on Heterogeneous Blockchain Networks](https://doi.org/10.1145/3700424)
  - Xiaohui Hu (Huazhong University of Science and Technology); Hang Feng (Zhejiang University); Pengcheng Xia (Beijing University of Posts and Telecommunications); Gareth Tyson (Hong Kong University of Science and Technology (GZ)); Lei Wu, Yajin Zhou (Zhejiang University); Haoyu Wang (Huazhong University of Science and Technology)
  - 该工作从 13 个跨链桥和 7 条区块链提取语义一致的 8000 多万笔交易，刻画 token、用户与用途，并在此数据上部署自动检测器，从跨链序列中发现 exploit、套利等异常行为。
  - 相较按单桥或单链抽样，核心创新是用桥合约语义把异构链交易拼接为端到端跨链事件，并让安全检测直接工作在重建后的跨链轨迹上。
  - cross-chain bridge、transaction reconstruction、Web3 security、anomaly detection

- [Tight bounds for Dynamic Bin Packing with Predictions](https://doi.org/10.1145/3700437)
  - Mozhengfu Liu (Northwestern University); Xueyan Tang (Nanyang Technological University)
  - 论文研究带作业时长预测的最小使用时间动态装箱，按最大乘性预测误差 ε 与时长跨度 μ 推导任意确定性算法下界，并设计在整个误差区间达到该界的增强算法。
  - 相较已有算法只在小误差区间接近最优，核心创新是给出覆盖从准确到失真的 tight consistency-robustness 曲线，闭合预测误差与竞争比之间的理论缺口。
  - learning-augmented algorithms、dynamic bin packing、duration prediction、tight bounds

- [MUDGUARD: Taming Malicious Majorities in Federated Learning using Privacy-preserving Byzantine-robust Clustering](https://doi.org/10.1145/3700422)
  - Rui Wang (TU Delft); Wang Xingkai (Shanghai Jiao Tong University); Huanhuan Chen, Jérémie Decouchant (TU Delft); Stjepan Picek (Radboud University); Nikolaos Laoutaris (IMDEA Networks Institute); Kaitai Liang (Delft University of Technology)
  - MUDGUARD 在联邦学习服务器侧对加密后的客户端更新做 Byzantine-robust clustering，使诚实客户端即使不是多数也能分离恶意更新；二进制秘密共享与多项式变换降低通信和计算，同时保持更新隐私。
  - 相较依赖诚实多数或服务器辅助干净数据的方案，核心创新是把抗恶意多数与更新机密性同时满足，并针对安全聚类的协议开销做系统级优化。
  - federated learning、Byzantine robustness、secure aggregation、malicious majority

- [Combinatorial Logistic Bandits](https://doi.org/10.1145/3744970.3727279)
  - Xutong Liu, Xiangxiang Dai (The Chinese University of Hong Kong); Xuchuang Wang, Mohammad Hajiesmaili (UMass Amherst); John C.S. Lui (The Chinese University of Hong Kong)
  - CLogB 把内容分发、多 LLM 选择和信道分配建模为带上下文的组合 bandit：每个基础臂以 logistic 函数产生二元回报，触发过程决定可见反馈；CLogUCB/VA-CLogUCB依据方差调整探索并降低对非线性 κ 和触发臂数 K 的遗憾依赖。
  - 相较线性回报或方差无关的组合 UCB，核心创新是同时处理 logistic 非线性、一般臂触发与组合奖励，并用 variance-adaptive bonus 消除关键问题规模因子。
  - combinatorial bandit、logistic reward、variance adaptation、PER archival summary

- [Adversarial Network Optimization under Bandit Feedback: Maximizing Utility in Non-Stationary Multi-Hop Networks](https://doi.org/10.1145/3700413)
  - Yan Dai (Massachusetts Institute of Technology); Longbo Huang (Tsinghua University)
  - UMO2 面向拓扑和效用任意随时间变化的多跳队列，只观察已执行动作的 bandit 反馈；它把自适应在线线性/凸优化嵌入 Lyapunov drift-plus-penalty，在队长可无界且差值可为负时仍保持网络稳定并追随缓慢变化参考策略。
  - 相较需要决策前网络状态或只能处理单跳的随机网络优化，核心创新是在对抗性多跳环境中联合给出效用遗憾和队列稳定保证。
  - adversarial network optimization、bandit feedback、multi-hop queues、Lyapunov control

- [INT-MC: Low-Overhead In-Band Network-Wide Telemetry Based on Matrix Completion](https://doi.org/10.1145/3700433)
  - Xin Zeng, Kun Xie (Hunan University); Yanbiao Li, Ke Xu (CNIC CAS); Gaogang Xie (ICT CAS); Jigang WEN (Hunan University of Science and Technology); Yinchuan Cong (Hunan University); Wei Liang (Hunan University of Science and Technology)
  - INT-MC 把全网端口/链路 telemetry 排成低秩矩阵，只让 INT 探针覆盖信息量高的一部分链路，再用 matrix completion 恢复未测状态；Eulerian digraph decomposition 将昂贵的覆盖路径计算化为路径选择。
  - 相较为完整可见性在每条路径携带遥测，核心创新是利用跨链路状态相关性做可恢复的稀疏测量，并共同优化探测路径与重建开销。
  - in-band telemetry、matrix completion、path selection、network observability

- [The Tale of Errors in Microservices](https://doi.org/10.1145/3700436)
  - I-Ting Angelina Lee (Washington University in St. Louis); Zhizhou Zhang, Abhishek Parwal (Uber Technologies Inc.); Milind Chabbi (Uber Technologies)
  - 论文分析 Uber 1900 个入口的 110 亿次 RPC，区分不会令顶层请求失败的 non-fatal error，并估算若删除失败子调用可节省的端到端延迟，据此排序值得排查的 API，实际将一个关键入口尾延迟降低 30%。
  - 相较只按错误率报警，核心创新是把调用图中的非致命错误映射为用户可见的反事实延迟损失，让运维优先级由性能影响而非出现次数决定。
  - microservices、RPC errors、tail latency、production measurement

- [ScaleOPT: A Scalable Optimal Page Replacement Policy Simulator](https://doi.org/10.1145/3700426)
  - Hyungseok Han (goorm Inc.); Sangjin Lee, Yongseok Son (Chung-Ang University)
  - ScaleOPT 为 Belady OPT 页替换仿真先并行构建 AccessMap，使每次访问 O(1) 得到下次引用，再用多棵按最小/最大未来时间组织的 Pipelined-Tree，让不同 cache size 的遍历和更新在多核上流水执行。
  - 相较串行标准 OPT 或逐容量重复模拟，核心创新是同时并行化未来引用预处理与多容量 cache 状态更新，使最优基线可扩展到大 trace 和多核。
  - cache simulation、optimal replacement、multicore parallelism、trace analysis

- [Beyond Data Points: Regionalizing Crowdsourced Latency Measurements](https://doi.org/10.1145/3700416)
  - Taveesh Sharma (University of Chicago); Paul Schmitt (University of Hawaii, Manoa / ICSI); Francesco Bronzino (ENS Lyon); Nick Feamster, Nicole P. Marwell (University of Chicago)
  - 论文针对众包宽带测速点在空间上不均匀、行政边界与接入网边界不一致的问题，对月度样本做插值、区域聚合与空间聚类，寻找跨月份稳定且性能相近的连续区域。
  - 相较直接按邮编或 census tract 求均值，核心创新是让测量数据反推网络性能边界，并以月度边界相似度验证结果不被采样密度牵动。
  - crowdsourced measurement、spatial clustering、broadband equity、sampling bias

- [A Global Perspective on the Past, Present, and Future of Video Streaming over Starlink](https://doi.org/10.1145/3700412)
  - Liz Izhikevich (University of California, Los Angeles); Reese Enghardt, Te-Yuan Huang, Renata Teixeira (Netflix)
  - 该工作用 85 国逾百万家庭的数据比较 Starlink 与地面网络的视频质量，定位 LEO 吞吐波动和丢包导致的码率切换/卡顿，并通过仿真及同规模真实 A/B test 调整拥塞控制与 ABR 策略。
  - 相较小规模卫星测速，核心创新是把全球被动观测与生产级主动实验结合，不只描述 Starlink 波动，还验证流媒体算法如何针对 LEO 动态性修正。
  - Starlink、video streaming、A/B testing、adaptive bitrate

- [Confidential VMs Explained: An Empirical Analysis of AMD SEV-SNP and Intel TDX](https://doi.org/10.1145/3700418)
  - Masanori Misono, Dimitrios Stavrakakis (Technical University of Munich); Nuno Santos (INESC-ID / Instituto Superior Tecnico, University of Lisbon); Pramod Bhatotia (Technical University of Munich)
  - 论文在裸机和 KVM 虚机上系统测量 AMD SEV-SNP 与 Intel TDX 的启动、内存、计算、存储、网络、attestation 和 context switch，并结合 TCB/CVE 分析解释两种 confidential VM 的安全与性能边界。
  - 相较只给单项 overhead 或厂商内对比，核心创新是用同一实验矩阵跨供应商连接微体系结构差异、系统瓶颈和可信计算基规模。
  - confidential VM、SEV-SNP、Intel TDX、performance characterization

- [Optimal Aggregation via Overlay Trees: Delay-MSE Tradeoffs under Failures](https://doi.org/10.1145/3700423)
  - Parikshit Hegde, Gustavo de Veciana (The University of Texas at Austin)
  - 论文将分布式聚合更新切成 chunk，经多棵 overlay tree 并行汇聚；同步场景给出 delay-optimal schedule，异步随机链路下证明近最优，并依据失败概率选择冗余、重试和估计器以权衡延迟与聚合 MSE。
  - 相较单树或只优化无故障延迟，核心创新是把多树调度与 failure-aware estimation 联合起来，用一个参数化模型同时控制完成时间和结果误差。
  - distributed aggregation、overlay trees、failure tolerance、delay-MSE tradeoff

- [Uncovering BGP Action Communities and Community Squatters in the Wild](https://doi.org/10.1145/3700431)
  - Brivaldo A. da Silva Jr, Adriano B. de Carvalho (UFMS); Italo Cunha (Universidade Federal de Minas Gerais); Timur Friedman (Sorbonne Université); Ethan Katz-Bassett (Columbia University); Ronaldo A. Ferreira (UFMS)
  - 该工作从 2018-2023 年数十亿条 BGP announcement 中学习 community 的行为，自动识别会触发远端路由动作的 action community，并检测长期冒用他方 information community 的 AS，以推断未公开 sibling 等关系。
  - 相较依赖运营商文档和人工字典，核心创新是从路由传播效果反推未标准化 community 语义，同时把 community squatting 变成可量化的关系发现信号。
  - BGP communities、routing policy、Internet measurement、AS relationships

### Fall Deadline（15 篇）

- [Learning-Augmented Competitive Algorithms for Spatiotemporal Online Allocation with Deadline Constraints](https://doi.org/10.1145/3711701)
  - Adam Lechowicz (University of Massachusetts Amherst); Nicolas Christianson (California Institute of Technology); Bo Sun (University of Waterloo); Noman Bashir (Massachusetts Institute of Technology); Mohammad Hajiesmaili (University of Massachusetts Amherst); Adam Wierman (California Institute of Technology); Prashant Shenoy (University of Massachusetts Amherst)
  - SOAD 将有截止期的批作业在地理数据中心间分配：每时隙揭示各地点服务成本，移动负载还支付度量空间迁移费；ST-CLIP 用成本预测调整不可撤销分配，并在碳感知调度中实现最优 consistency-robustness 权衡。
  - 相较分别处理 metrical task 或 deadline search，核心创新是统一空间迁移与时间截止约束，并给出预测准确时获益、错误时仍有最优竞争界的算法。
  - spatiotemporal allocation、deadline scheduling、carbon-aware computing、learning augmentation

- [Exploring Function Granularity for Serverless Machine Learning Application with GPU Sharing](https://doi.org/10.1145/3711699)
  - Xinning Hui (North Carolina State University); Yuanchao Xu (University of California Santa Cruz); Xipeng Shen (North Carolina State University)
  - 该工作分析 serverless ML inference 中函数切得粗或细如何同时影响冷启动、GPU sharing、SLO 命中与成本，并用预测模型根据应用和运行状态在线选择粒度，配套编程工具和 runtime extension。
  - 相较部署时固定函数边界，核心创新是把 function granularity 变成运行时可调资源旋钮，并将粒度预测直接接入现有 serverless 平台。
  - serverless ML、GPU sharing、adaptive granularity、SLO

- [The Last Survivor of PoS Pools: Staker's Dilemma](https://doi.org/10.1145/3711704)
  - Yuming Huang (National University of Singapore); Jing Tang (The Hong Kong University of Science and Technology); Qianhao Cong, Richard Ma (National University of Singapore); Lei Chen (Hong Kong University of Science and Technology); Yeow Meng Chee (National University of Singapore)
  - 论文把 block-withholding 攻击从 PoW 推到 PoS staking pool，建模攻击池把无效贡献混入受害池后 stake 份额的动态演化；两池时受害池消失，多攻击池时最终只剩一个幸运攻击者与 solo staker。
  - 相较 PoW 的 miner's dilemma，核心创新是揭示 PoS 的复利 stake 聚合会把暂时收益差放大成池退出，形成更严重且结构不同的 staker's dilemma。
  - proof of stake、staking pool、block withholding、game dynamics

- [CHash: A High Cost-Performance Hash Design for CXL-based Disaggregated Memory System](https://doi.org/10.1145/3711698)
  - Mengting Lu, Gaocong Liu, Kun Wang, Feng Zhu, Shu Li (Alibaba Group)
  - CHash 基于两类真实 CXL 设备的带宽/延迟和 allocation 测量，把 hash metadata 与 KV record 分置 DRAM/CXL，并用 staged bucket、两级过滤和 hash multiplexing 减少远端查找，兼顾约 90% load factor。
  - 相较把现有内存 hash 表整体放入 CXL，核心创新是让索引结构和查找流水显式适配 DRAM-CXL 非对称性，把容量扩展与访问成本共同优化。
  - CXL memory、hash index、disaggregated memory、hybrid placement

- [Game Theoretic Liquidity Provisioning in Concentrated Liquidity Market Makers](https://doi.org/10.1145/3711700)
  - Weizhao Tang (CMU); Rachid Elazouzi (University of Avignon); Cheng Han Lee, Ethan Chan (Allium); Giulia Fanti (CMU)
  - 论文把集中流动性做市商中 LP 选择投资额和价格区间建成博弈，将原本二次复杂度、多均衡模型化简为线性复杂度且唯一均衡的 water-filling；再用真实池数据比较实际策略与均衡收益。
  - 相较只优化单个 LP 或假设固定他人流动性，核心创新是给出可计算的多 LP 策略均衡，并揭示低预算用尽、富裕 LP 留存预算的结构。
  - automated market maker、liquidity provision、Nash equilibrium、water filling

- [VESTA: A Secure and Efficient FHE-based Three-Party Vectorized Evaluation System for Tree Aggregation Models](https://doi.org/10.1145/3711707)
  - Haosong ZHAO (The Hong Kong University of Science and Technology (Guangzhou)); Junhao HUANG (Guangdong Provincial Key Laboratory IRADS, BNU-HKBU United International College, Zhuhai, China; Hong Kong Baptist University, Hong Kong, China); Zihang CHEN, Kunxiong ZHU (The Hong Kong University of Science and Technology (Guangzhou)); Donglong CHEN (Guangdong Provincial Key Laboratory IRADS, BNU-HKBU United International College, Zhuhai, China; Hong Kong Baptist University, Hong Kong, China); Zhuoran Ji (Shandong University, School of Cyber Science and Technology); Hongyuan LIU (The Hong Kong University of Science and Technology (Guangzhou))
  - VESTA 面向模型方、算力方和用户互不信任的 tree-ensemble MLaaS，在编译期预计算部分 FHE 操作，再把森林切成可并行子模型，由 runtime 做向量化三方加密推理，降低在线延迟和内存。
  - 相较逐棵树、全在线执行的 FHE inference，核心创新是用编译期/运行时协同把可预计算密文操作和 task-level parallelism 同时暴露出来。
  - FHE inference、tree ensembles、compiler-runtime、privacy-preserving ML

- [Asynchronous Multi-Agent Bandits: Fully Distributed vs. Leader-Coordinated Algorithms](https://doi.org/10.1145/3711696)
  - Xuchuang Wang, Yu-Zhen Chen (University of Massachusetts Amherst); Xutong Liu (Carnegie Mellon University); Lin Yang (Nanjing Universary); Mohammad Hajiesmaili (UMass Amherst); Don Towsley (University of Massachusetts - Amherst); John C.S. Lui (The Chinese University of Hong Kong)
  - 论文研究每轮只有未知子集在线的异步多主体 bandit：全分布式方案按估计精度和需求触发通信并逐步淘汰臂；leader-coordinated 方案用低切换 Tsallis-INF 动态挑选有足够活跃机会的 leader。
  - 相较假定所有节点同步拉臂，核心创新是在未知、时变活跃集合下仍同时接近同步算法的遗憾界与通信界，并比较无中心和有 leader 两种协作代价。
  - multi-agent bandit、asynchronous learning、communication efficiency、非 LLM Agent

- [NetJIT: Bridging the Gap from Traffic Prediction to Preknowledge for Distributed Machine Learning](https://doi.org/10.1145/3711702)
  - Xin Ai, Zijian Li, Yuanyi Zhu, Zixuan Chen, Sen Liu, Yang Xu (Fudan University)
  - NetJIT 在分布式训练计算发生时追踪张量数据依赖，用 JIT program analysis 在通信真正发出前预测 collective/flow 的时间和规模，使 traffic engineering 能预先配置路径；原型显著降低事件检测误差并缩短迭代。
  - 相较从历史流量统计事后预测，核心创新是从即将产生通信的程序语义取得 preknowledge，把网络优化的反应点从包到达后提前到计算阶段。
  - distributed training、traffic prediction、JIT analysis、network optimization

- [Steady-State Convergence of the Continuous-Time Routing System with General Distributions in Heavy Traffic](https://doi.org/10.1145/3711703)
  - Jin Guang (The Chinese University of Hong Kong, Shenzhen); Yaosheng Xu (University of Chicago); J. G. Dai (Cornell University)
  - 论文分析一般到达和服务分布下的连续时间 JSQ 与 power-of-two routing，在仅要求 2+ε 阶矩时证明重载稳态中各站缩放队长共同收敛到同一指数随机变量，并以 Palm 版 basic adjoint relationship 完成证明。
  - 相较依赖更强分布矩或离散时间假设的 state-space collapse，核心创新是以更弱条件得到稳态交换极限，覆盖更广的实际服务分布。
  - queueing theory、heavy traffic、join-shortest-queue、steady-state convergence

- [Two choice behavioral game dynamics with myopic-rational and herding~players](https://doi.org/10.1145/3711706)
  - Khushboo Agarwal, Konstantin Avrachenkov (Inria Sophia Antipolis, 2004 Route des Lucioles, 06902 Valbonne, France); Raghupati Vyas, Veeraruna Kavitha (IEOR, IIT Bombay, Powai, Mumbai, 400076, Maharashtra, India)
  - 论文研究玩家依次选择两动作、其中 α 比例做短视最优响应而其余跟随多数的行为博弈，用 differential inclusion 描述因策略切换不连续而产生的均场极限，并用于参与和路由博弈。
  - 相较假定全体完全理性或用平滑 ODE，核心创新是把 myopic-rational 与 herding 混合行为纳入可证明几乎处处唯一的非光滑极限动力学。
  - behavioral game、herding、mean-field limit、differential inclusion

- [Tiered Cloud Routing: Methodology, Latency, and Improvement](https://doi.org/10.1145/3711705)
  - Shihan Lin, Yi Zhou, Xiao Zhang (Duke University); Todd Arnold (Army Cyber Institute, West Point); Ramesh Govindan (University of Southern California); Xiaowei Yang (Duke University)
  - 该工作用 RIPE Atlas 观测 AWS、Azure、Google Cloud 的 WAN-transit 与 Internet-transit 路由，定位流量何处进入/提前离开私有骨干，并把实测延迟与按性能选择出口的仿真策略比较。
  - 相较依据云厂商产品描述推断网络层级，核心创新是从公网 vantage point 重建三家云的 tiered routing 行为，并量化 performance-based routing 可改进的地域对。
  - cloud WAN、Internet transit、RIPE Atlas、latency routing

- [A Piecewise Lyapunov Analysis of Sub-quadratic SGD: Applications to Robust and Quantile Regression](https://doi.org/10.1145/3744970.3727269)
  - Yixuan Zhang (University of Wisconsin-Madison); Dongyan (Lucy) Huo (Cornell University); Yudong Chen, Qiaomin Xie (University of Wisconsin-Madison)
  - 论文为局部强凸但尾部次二次、且损失只一阶可微的 SGD 构造分段 Lyapunov 函数，推导递减/常步长下有限时矩界、弱收敛、CLT 与偏差，并覆盖 Huber 鲁棒回归和非光滑分位数回归。
  - 相较依赖全局二次增长或条件密度连续性，核心创新是用分区势函数分别控制中心与重尾区域，首次给出次二次 SGD 的几何收敛刻画。
  - stochastic gradient descent、Lyapunov analysis、robust regression、PER archival summary

- [Blockchain Amplification Attack](https://doi.org/10.1145/3711697)
  - Taro Tsuchiya (Carnegie Mellon University); Liyi Zhou (The University of Sydney); Kaihua Qin (Yale University); Arthur Gervais (University College London & UC Berkeley RDI); Nicolas Christin (Carnegie Mellon University)
  - 论文发现以 MEV 为动机、跳过无效交易验证的低延迟 Ethereum 节点可被攻击者反复传播同一无效交易，将流量放大约 3600 倍；工作用主网监测、传播模型、本地仿真和测试网实验评估攻击与跳验收益。
  - 相较传统向单节点发送洪泛流量，核心创新是把节点为抢 MEV 而主动削弱验证的行为变成 P2P 放大器，并给出经济收益与系统风险的联合阈值。
  - Ethereum、amplification attack、MEV、P2P propagation

- [Optimal Scheduling in a Quantum Switch](https://doi.org/10.1145/3744970.3727302)
  - Sanidhay Bhambay, Thirupathaiah Vasantam, Neil Walton (Durham University)
  - 论文把 quantum switch 建模为先在接入链路生成 link-level entanglement、再融合处理请求的双边排队系统，刻画可稳定的请求率容量域，并用一族 Max-Weight 策略在 fluid scale 两时间尺度下实现渐近吞吐最优。
  - 相较套用经典 packet switch 调度，核心创新是把纠缠生成与融合的耦合状态纳入容量分析，并将最优流体动力学归结为 average-reward MDP。
  - quantum switch、entanglement scheduling、capacity region、PER archival summary

- [Allocating Public Goods via Dynamic Max-Min Fairness: Long-Run Behavior and Competitive Equilibria](https://doi.org/10.1145/3711695)
  - Siddhartha Banerjee (Cornell); Giannis Fikioris, Chido Onyeze, Eva Tardos (Cornell University)
  - 论文研究动态 max-min fair 公共资源分配中自利参与者何时请求资源：证明固定 threshold policy 间一般不存在 Nash equilibrium，并在对称场景设计依据历史分配率、带渐消 welfare drift 的数据驱动策略，使任何人都无利改用其他固定阈值。
  - 相较只给对任意对手都安全但保守的鲁棒保证，核心创新是刻画 DMMF 的完整稳态分布，并据此分析真实自利均衡及其福利提升。
  - dynamic max-min fairness、public goods、strategic allocation、steady state

### Winter Deadline（31 篇）

- [A Case Study for Ray Tracing Cores: Performance Insights with Breadth-First Search and Triangle Counting in Graphs](https://doi.org/10.1145/3727108)
  - Zhixiong Xiao, Mengbai Xiao, Yuan Yuan, Dongxiao Yu (Shandong University); Rubao Lee (Freelance); Xiaodong Zhang (The Ohio State University)
  - 论文把 BFS、triangle counting 和 set intersection 转成 ray generation 与 BVH 查询，在多种真实/合成图上比较 RT core 与 CUDA；结果显示搜索原语虽快，但 BVH 构建和固定 pipeline 开销使普通图算法通常不占优，仅高 skew 交集受益。
  - 相较只报告把非图形 workload 搬到 RT core 的加速，核心创新是给出负结果和分解测量，明确数据偏斜、BVH 成本与 kernel 规模决定何时值得复用专用硬件。
  - ray-tracing cores、graph analytics、BVH、hardware characterization

- [A Gittins Policy for Optimizing Tail Latency](https://doi.org/10.1145/3727109)
  - Amit Harlev, George Yu, Ziv Scully (Cornell University)
  - 论文在未知 job size 的 light-tailed M/G/1 中，以带负 discount rate 的 Gittins 变体按已服务时间决定抢占顺序，使 response-time tail 达到最快可能的渐近衰减；部分 size 信息和完全已知的 γ-Boost 都可视作边界情况。
  - 相较既有 light-tail 强尾最优策略必须预知 job size，核心创新是从不完整信息的 Gittins index 推出同等 tail guarantee。
  - Gittins policy、tail latency、M/G/1、unknown job sizes

- [CertainSync: Rateless Set Reconciliation with Certainty](https://doi.org/10.1145/3727110)
  - Tomer Keniagin, Eitan Yaakobi, Ori Rottenstreich (Technion - Israel Institute of Technology)
  - CertainSync 用可保证 listing 的 IBLT 连续发送 rateless reconciliation 符号，接收方在通信量达到由实际 symmetric difference 与 universe 决定的界时必然完成，无需预估差集大小；UniverseReduceSync 进一步压缩区块链哈希的大 universe。
  - 相较概率成功或必须先参数化差集规模的集合同步，核心创新是将确定成功保证与自适应通信长度同时实现，并显式给出 universe reduction 的开销—保证权衡。
  - set reconciliation、IBLT、rateless protocol、blockchain synchronization

- [Design and Modeling of a New File Transfer Architecture to Reduce Undetected Errors Evaluated in the FABRIC Testbed](https://doi.org/10.1145/3727111)
  - Prateek Jain (Boston University); Arash Sarabi (Arizona State University); Abraham Matta (Boston University); Violet R. Syrotiuk (Arizona State University)
  - MLED 为 PB 级文件传输建立可递归的多层协议，每一层独立配置 checksum、路由和安全策略；中间节点可在错误尚未扩散时检测并修复，FABRIC 实验中避免整文件重传并维持约 800 Mbps goodput。
  - 相较只依赖链路层与端到端 transport checksum，核心创新是让 error detection 在网络内部多级组合，使漏检概率随层级下降且只重做受影响片段。
  - large file transfer、in-network error detection、FABRIC testbed、data integrity

- [Diffusion-Based Generative System Surrogates for Scalable Learning-Driven Optimization in Virtual Playgrounds](https://doi.org/10.1145/3727112)
  - Junyoung Lee, Seohyun Kim, Shinhyoung Jang, Jongho Park, Yeseong Kim (DGIST)
  - DiffNEST 用 diffusion model 学习系统 workload 与配置到连续性能 trace 的分布，在虚拟 playground 中生成可供优化器反复试验的轨迹，并通过 fine-tuning 迁移到 DVFS 和多核 cache allocation，减少直接在硬件上训练 RL 的数据成本。
  - 相较单点回归 surrogate 或必须在线采样真实机器的 RL，核心创新是生成保留时序与 workload 多样性的系统轨迹，让同一基础模型服务多个优化任务。
  - diffusion surrogate、system optimization、virtual playground、DVFS

- [DiskAdapt: Hard Disk Failure Prediction Based on Pre-Training and Fine-Tuning](https://doi.org/10.1145/3727113)
  - Rongjia Han (Ocean University of China); Kunzheng Lv (Qingdao Municipal Center For Disease Control & Prevention); Peishun Liu, Yashi Huang, Quanjie Dou, Tian Yin, Hengtao Wang, YiBao Song (Ocean University of China)
  - DiskAdapt 从多厂商、多型号硬盘 SMART 多变量时序预训练 AdaptFormer，再对新盘型少量 fine-tune，并通过特征对齐缓解设备分布变化，以预测即将发生的物理故障。
  - 相较每个盘型独立训练、换型号即失效的故障模型，核心创新是把预训练表示与轻量 adapter 迁移结合，直接针对数据中心盘型更替的泛化问题。
  - disk failure prediction、time series、pretraining-finetuning、domain adaptation

- [Exploiting Kubernetes Autoscaling for Economic Denial of Sustainability](https://doi.org/10.1145/3727114)
  - Jonathan Chamberlain, Jilin Zheng (Boston University); Zeying Zhu, Zaoxing Liu (University of Maryland); David Starobinski (Boston University)
  - 论文用 MDP 将 Kubernetes replica 数、SLA 违约、实例计费粒度和 workload 纳入 autoscaling，再用 Stackelberg game 求攻击者注入流量与服务方扩缩容策略；真实集群验证 EDoS 可用少量流量诱发显著成本，并测试随机化自定义指标防御。
  - 相较只把 EDoS 当流量洪泛，核心创新是建模云计费和 autoscaler hysteresis 如何制造经济放大，并从攻防双方最优响应推导有效条件。
  - Kubernetes、economic denial of sustainability、autoscaling、Stackelberg game

- [FastFlow: Early Yet Robust Network Flow Classification using the Minimal Number of Time-Series Packets](https://doi.org/10.1145/3727115)
  - Rushi Jayeshkumar Babaria, Minzhao Lyu, Gustavo Batista, Vijay Sivaraman (University of New South Wales)
  - FastFlow 将前几个 packet 同时编码为逐包和时间槽序列，抵抗丢包/重传造成的乱序；LSTM 在 reinforcement learning 的 sequential decision 中逐步决定继续观察还是以已知/未知类别结束，使每条 flow 用最少包完成可靠分类。
  - 相较固定取前 N 包且只能识别封闭类别的 classifier，核心创新是把采样长度作为逐流决策，并把未知流检测、早停和序列扰动鲁棒性统一训练。
  - traffic classification、early stopping、open-set detection、传统 RL 非 Agent

- [Finite-Time Behavior of Erlang-C Model: Mixing Time, Mean Queue Length and Tail Bounds](https://doi.org/10.1145/3744970.3727287)
  - Hoang Huy Nguyen (Georgia Institute of Technology); Sushil Mahavir Varma (INRIA); Siva Theja Maguluri (Georgia Institute of Technology)
  - 论文不再假定 Erlang-C 已到稳态，而是用 Lyapunov-Poincaré 方法给有限服务器 M/M/n 的有限时队长分布到稳态的 chi-square 距离界，并在 Halfin-Whitt 两侧得到紧或常数紧的 mixing rate。
  - 相较只给稳态均值或扩散极限，核心创新是把有限时间 mixing、平均队长与 tail bound 连起来，并发展可推广到可数状态可逆 Markov chain 的局部 Poincaré 技术。
  - Erlang-C、mixing time、transient queueing、PER archival summary

- [ForgetMeNot: Understanding and Modeling the Impact of Forever Chemicals Toward Sustainable Large-Scale Computing](https://doi.org/10.1145/3727116)
  - Rohan Basu Roy (University of Utah); Raghavendra Kanakagiri (Indian Institute of Technology Tirupati); Yankai Jiang, Devesh Tiwari (Northeastern University)
  - ForgetMeNot 把晶圆厂工艺实践、芯片代际/光刻节点和硬件容量映射为含氟温室气体排放，并用真实 fab 数据校准；它可比较 CPU、DRAM、存储制造方案并帮助数据中心在性能约束下组装低排放服务器。
  - 相较只核算运行和制造碳排，核心创新是把高 GWP、长寿命的 forever chemicals 纳入可配置硬件生命周期模型，使材料与工艺选择可被系统设计优化。
  - semiconductor manufacturing、fluorinated emissions、lifecycle modeling、hardware sustainability

- [Improving Multiresource Job Scheduling with Markovian Service Rate Policies](https://doi.org/10.1145/3727117)
  - Zhongrui Chen (University of North Carolina at Chapel Hill); Isaac Grosof (Northwestern University); Benjamin Berg (University of North Carolina at Chapel Hill)
  - MSR policy 面向同时消耗 CPU、内存、磁盘或加速器的 job，根据到达率、服务时间、资源容量和 job demand 选择可并行集合；同一框架覆盖可抢占、不可抢占及有 setup time 的系统，并给出吞吐最优与平均响应时间界。
  - 相较难分析的启发式装箱或难实现的最优 MDP，核心创新是用 Markovian service rate 把多资源调度化为既易部署又能取得近紧性能界的策略族。
  - multiresource scheduling、cloud jobs、response time、throughput optimality

- [Microns: Connection Subsetting for Microservices in Shared Clusters](https://doi.org/10.1145/3727118)
  - Jianxiong Liao, Juntao Li, Zhi Zhou (Sun Yat-sen University); Fei Xu (East China Normal University); Fangming Liu (Peng Cheng Laboratory); Xu Chen (Sun Yat-sen University)
  - Microns 在共享集群中先按微服务调用图决定每对服务应保留的 connection 数，再按各 downstream container 对端到端延迟的贡献选择具体连接关系，持续适应副本和依赖变化。
  - 相较均匀随机或固定 fan-out 的 connection subsetting，核心创新是同时在应用依赖层和容器层分配连接预算，把局部连接选择直接对齐端到端 latency。
  - microservices、connection subsetting、shared cluster、latency optimization

- [On the Distribution of Sojourn Times in Tandem Queues](https://doi.org/10.1145/3727140)
  - Florin Ciucu, Sima Mehri (University of Warwick)
  - 论文对一般到达、light-tailed service 的 tandem queue 推导端到端等待/逗留时间的 polynomial-exponential tail 上界， polynomial 次数由 bottleneck 数量和 service tail 强度共同决定；双队列指数服务下闭式界接近精确结果。
  - 相较只给大偏差指数率，核心创新是保留决定有限阈值精度的多项式前因子，因此可区分多个瓶颈对 tail 的叠加影响。
  - tandem queues、sojourn time、tail bounds、bottleneck analysis

- [Online Allocation with Multi-Class Arrivals: Group Fairness vs Individual Welfare](https://doi.org/10.1145/3727120)
  - Faraz Zargari, Hossein Nekouyan (University of Alberta); Bo Sun (University of Waterloo); Xiaoqi Tan (University of Alberta)
  - 论文在线接收属于不同群体的 agent，以数量公平或效用公平约束分配固定资源；threshold 算法达到两个公平定义的最优/近最优界，set-aside multi-threshold 则预留一部分资源保群体公平、其余最大化个体福利。
  - 相较只优化总效用或只满足一个 fairness quota，核心创新是证明群体公平与个体福利的 Pareto 边界，并给出在线达到该边界的资源分拆机制。
  - online allocation、group fairness、individual welfare、Pareto tradeoff

- [Online Fair Allocation of Reusable Resources](https://doi.org/10.1145/3727121)
  - Qingsong Liu, Mohammad Hajiesmaili (University of Massachusetts Amherst)
  - 论文处理容量 C 的可复用资源，请求类型、效用和占用时长分布均未知且只见 bandit feedback；算法用 optimistic penalty weight 保可行，用 dual exploration-discarding 在多种效用间最大化长期最小值，容量增大时竞争比趋近 1。
  - 相较一次性资源或已知分布的公平分配，核心创新是同时处理资源归还时间、探索成本和 max-min fairness，并给出容量相关的近最优在线保证。
  - reusable resources、max-min fairness、bandit feedback、online allocation

- [Optimal SSD Management with Predictions](https://doi.org/10.1145/3727122)
  - Tomer Lange, Joseph (Seffi) Naor, Gala Yadgar (Technion)
  - Gladiator 管理 SSD 中不可原位更新的 page 和整块清理，根据 oracle 对数据失效/未来访问的预测选择写入与 garbage collection，目标是减少有效 page 搬写；算法不需要额外非易失存储，并随预测误差平滑退化。
  - 相较对错误预测敏感或依赖额外 metadata device 的 learning-augmented FTL，核心创新是给出最优利用预测的 rewrite 界，并把同一思路扩展为高效 offline 解。
  - SSD management、garbage collection、learning augmentation、write amplification

- [Peer-to-Peer Distribution of Graph States Across Spacetime Quantum Networks of Arbitrary Topology](https://doi.org/10.1145/3727123)
  - Yuexun Huang (The University of Chicago); Xiangyu Ren (The University of Edinburgh); Bikun Li, Yat Wong (The University of Chicago); Zhiding Liang (Rensselaer Polytechnic Institute); Liang Jiang (The University of Chicago)
  - P2PGSD 在任意拓扑量子网络上把目标 graph state 拆成可由多节点并行建立和融合的子结构，并用 spacetime network 表示纠缠与 memory 占用；模型证明一类资源最小化问题的困难性并为稀疏图选择高效协议。
  - 相较仅分发 Bell pair 或依赖中心节点，核心创新是借鉴 P2P 把任意多方 graph state 的路由、存储和并行构造统一起来，稀疏状态可显著减少资源。
  - quantum network、graph state distribution、peer-to-peer、spacetime scheduling

- [Phishing Tactics Are Evolving: An Empirical Study of Phishing Contracts on Ethereum](https://doi.org/10.1145/3727138)
  - Bowen He (Zhejiang University); Xiaohui Hu (Huazhong University of Science and Technology); Yufeng Hu (Zhejiang University); Ting Yu (Mohamed bin Zayed University of Artificial Intelligence); Rui Chang, Lei Wu, Yajin Zhou (Zhejiang University)
  - 论文从 bytecode 中识别可疑函数并模拟交易，构建 37,654 个 Ethereum phishing contract 与 211,319 笔钓鱼交易的数据集，分析 victim、合约和 deployer 关系，发现一个集团部署了 85.7% 的样本。
  - 相较只跟踪 EOA 转账/授权地址，核心创新是把主动执行恶意逻辑的 phishing contract 作为新对象，以静态字节码筛选加动态交易模拟扩大样本覆盖。
  - Ethereum phishing、smart contract、transaction simulation、cybercrime measurement

- [PipeCo: Pipelining Cold Start of Deep Learning Inference Services on Serverless Platforms](https://doi.org/10.1145/3727125)
  - Jiaang Duan, Shiyou Qian, Hanwen Hu (Shanghai Jiao Tong University); Dingyu Yang (Zhejiang University); Jian Cao (Shanghai Jiaotong University); Guangtao Xue (Shanghai Jiao Tong University)
  - PipeCo 将 serverless 深度学习服务按模型纵向切成可独立预热的 slice，让加载与计算流水重叠；attention 预测请求周期和 idle container，similarity matcher 决定哪些容器可复用，从而在 CPU/GPU cluster 降低冷启动和常驻资源。
  - 相较延长整模型 keep-alive，核心创新是把 cold start miniaturize 到模型 slice，并联合预测式预热与跨服务容器复用，避免用长期占用换延迟。
  - serverless inference、cold start、model slicing、container reuse

- [Poison comes in small packages: Application-driven Reexamination of Datacenter Microbursts](https://doi.org/10.1145/3727126)
  - Mohammad Hosseini (Shahid Beheshti University); Sina Darabi (Università della Svizzera italiana (USI)); Hannaneh B. Pasandi (University of California); Mohammad Nakhjiri (Shahid Beheshti University); Patrick Eugster (Università della Svizzera italiana)
  - 论文按应用层来源重新测量数据中心 microburst，比较不同 burst 长度、强度和协议栈位置下各类缓解机制，发现同一技术只对特定形态有效，并给出应用到 mitigation 的选择关系。
  - 相较寻找一个通用 microburst 算法，核心创新是证明应用生成机制决定 burst 特征和防护效果，把部署问题改写为 workload-aware mechanism selection。
  - datacenter network、microbursts、workload characterization、mitigation selection

- [PROPHET: PRediction Of 5G bandwidtH using Event-driven causal Transformer](https://doi.org/10.1145/3727127)
  - Sheng Liu, Chuan Li, Fan Bai (General Motors Global R&D)
  - PROPHET 预测车辆移动中的 5G throughput：wavelet encoder 抓长期多尺度趋势，decoder 用 control-plane event attention 聚焦 handover 等短期扰动，再由 Granger-causality attention 选择真正有预测力的历史信号。
  - 相较只输入信号强度的 LSTM/Transformer，核心创新是把网络控制事件与环境变量的因果时间结构显式写入注意力，兼顾长趋势和事件突变。
  - 5G bandwidth prediction、vehicular network、causal transformer、handover events

- [Quantum Computing in the RAN with Qu4Fec: Closing Gaps Towards Quantum-based FEC Processors](https://doi.org/10.1145/3727128)
  - Nikolaos Apostolakis (IMDEA Networks Institute and Universidad Carlos III de Madrid); Marta Sierra-Obea, Marco Gramaglia (Universidad Carlos III de Madrid); Jose A. Ayala-Romero, Andres Garcia-Saavedra (NEC Laboratories Europe); Marco Fiore (IMDEA Networks Institute); Albert Banchs (IMDEA Networks Institute and Universidad Carlos III de Madrid); Xavier Costa-Perez (i2CAT, NEC Laboratories Europe and ICREA)
  - Qu4Fec 把无线 LDPC decoding 映射到 quantum annealer/QPU，在模拟中降低 block error rate，并在真实 QPU 上测量 qubit chain、量化和规模限制，据此提出更适合 RAN FEC 的未来量子硬件结构。
  - 相较只在理想量子模拟器展示解码，核心创新是把算法放到真实 QPU 做端到端 reality check，并由失败瓶颈反向提出 6G baseband 硬件需求。
  - quantum annealing、LDPC decoding、RAN、hardware reality check

- [Quantum Network Optimization: From Optimal Routing to Fair Resource Allocation](https://doi.org/10.1145/3727129)
  - Zhaozhen Wang, Xingang Shi, Zhengfeng Ji, Xia Yin (Tsinghua University)
  - 论文先用 routing algebra 定义量子链路成功概率、保真度等可组合 metric 并构造可证明最优路由，再在纠缠/存储等资源约束下联合分配并发请求，用近最优 heuristic 平衡总收益与请求公平。
  - 相较直接复用经典 shortest path 或只最大化吞吐，核心创新是把量子概率度量的路由最优性与多请求公平资源分配放进统一框架。
  - quantum networking、routing algebra、resource allocation、fairness

- [Reducing Sensor Requirements by Relaxing the Network Metric Dimension](https://doi.org/10.1145/3727130)
  - Paula Mürmann, Robin Jaccard, Maximilien Dreveton (EPFL); Aryan Alavi Razavi Ravari (Sharif University of Technology); Patrick Thiran (EPFL)
  - 论文把 graph metric dimension 放宽为距离小于 k 的顶点可共享 sensor distance profile，分析确定性/随机树所需传感器数量，并用两阶段定位先粗分区域再加传感器细分，在循环图和真实网络上选择最省的 k。
  - 相较要求一次性唯一识别每个顶点，核心创新是用可控空间分辨率换传感器数量，并证明目标周围不可区分集合仍保持很小。
  - source localization、network sensors、metric dimension、resolution tradeoff

- [Revisiting Traffic Splitting for Software Switch in Datacenter](https://doi.org/10.1145/3727131)
  - Yeonho Yoo, Gyeongsik Yang, Changyong Shin, Hwiju Cho, Wonmi Choi (Korea University); Zhixiong Niu (Microsoft Research); Chuck Yoo (Korea University)
  - VALO 面向 Open vSwitch 按路径权重分流却因 hash 离散和资源开销产生偏差的问题，用 score graph 表示连接到路径的可行调整，再以 VALO gravity 高效逼近期望比例，改善数据挖掘/训练 flow completion。
  - 相较静态 hash bucket 或高开销精确分配，核心创新是同时优化 splitting accuracy 与 switch state/计算成本，而不是牺牲其中一项。
  - software switch、traffic splitting、Open vSwitch、weighted multipath

- [Robust Gittins for Stochastic Scheduling](https://doi.org/10.1145/3744970.3727315)
  - Benjamin Moseley, Heather Newman (Carnegie Mellon University); Kirk Pruhs (University of Pittsburgh); Rudy Zhou (Microsoft)
  - 论文研究只拿到近似 job-size distribution 的单机抢占调度，证明直接按错误分布运行标准 Gittins 可因任意小偏差产生无界平均完成时间，再修改 index 使近似比由新定义的分布误差控制。
  - 相较把预测分布当真值，核心创新是识别 Gittins 的非鲁棒断点并构造对 modest distribution shift 平滑退化的 robust index。
  - stochastic scheduling、Gittins index、distribution shift、PER archival summary

- [Understanding Intel User Interrupts](https://doi.org/10.1145/3727132)
  - Yves Kone (IRIT, Université de Toulouse, CNRS, Toulouse INP, UT3 Toulouse); Louis Duval, Renaud Lachaize (Univ. Grenoble Alpes, CNRS, Inria, Grenoble INP, LIG); Pascal Felber (University of Neuchâtel); Daniel Hagimont (IRIT, Université de Toulouse, CNRS, Toulouse INP, UT3 Toulouse); Alain Tchana (Univ. Grenoble Alpes, CNRS, Inria, Grenoble INP, LIG)
  - 论文在物理机及 Linux/KVM 虚机上拆解 Intel User Interrupt 的发送、接收、handler 与 virtualization 开销，并用它替代 Unix signal 做进程间通知，使抢占式用户态线程调度达到微秒级 quantum。
  - 相较每次通知都陷入 kernel，核心创新是量化并利用直接 user-mode IPI 的完整路径，同时说明虚拟化与上下文切换下真正的适用边界。
  - Intel UINTR、user-level interrupts、IPC、thread scheduling

- [Internet Service Usage and Delivery As Seen From a Residential Network](https://doi.org/10.1145/3727133)
  - Shuyue Yu, Thomas Koch, Ilgar Mammadov, Hangpu Cao, Gil Zussman, Ethan Katz-Bassett (Columbia University)
  - 论文持续收集约 1000 个校外住宅的流量，区分家庭场景与校园/宿舍 trace，关联访问服务、CDN/hosting infrastructure 和服务器距离，揭示 P2P 时长、第三方 CDN 流量份额及远端 serving 等现象，并开放数据。
  - 相较用校园 trace 代替家庭网络或依赖过时私有样本，核心创新是提供可共享的长期住宅观测，并把服务使用与实际交付位置联合分析。
  - residential Internet、traffic dataset、CDN measurement、service delivery

- [UniContainer: Unlocking the Potential of Unikernel for Secure and Efficient Containerization](https://doi.org/10.1145/3727134)
  - Zhicong Zhang, Qihang Zhou, Shaowen Xu, Nan Jiang, Weijuan Zhang, Xiaoqi Jia (Institute of Information Engineering, Chinese Academy of Sciences)
  - UniContainer 将原容器内不同组件拆到各自定制 Unikernel，隔离容器之间及同容器内恶意程序；工具分析目标容器的 system-call log，自动生成最小 Unikraft image，同时保留原有部署入口。
  - 相较共享 host kernel 的容器或要求人工重写 unikernel 应用，核心创新是用自动 syscall-driven specialization 把容器便利性转成细粒度 unikernel 隔离。
  - container isolation、unikernel、Unikraft、system-call specialization

- [Universal and Tight Bounds on Counting Errors of Count-Min Sketch with Conservative Updates](https://doi.org/10.1145/3727135)
  - Younes Ben Mazziane (Inria, University of Avignon LIA); Othmane Marfoq (Meta)
  - 论文分析单数组 conservative-update sketch（CU-S）的 count overestimate，证明未出现 item 的 unseen error 最大，并把任意 stream 的误差用 reference stream 界定；再以参数 g 的有限状态 Markov chain 上下界近似原无限状态过程。
  - 相较仅给概率粗界或靠仿真调参，核心创新是建立 memory、hash 数与最坏 counting error 的可计算 tight bound，并揭示 unseen item 是统一分析入口。
  - Count-Min Sketch、conservative update、counting error、Markov analysis

- [Using Lock-Free Design for Throughput-Optimized Cache Eviction](https://doi.org/10.1145/3727136)
  - Chao Dong, Fang Wang (Huazhong University of Science and Techonolgy); Hong Jiang (University of Texas at Arlington); Dan Feng (Huazhong University of Science and Techonolgy)
  - Mobius 用两条 lock-free FIFO 管理 cache item，使 lookup、insert 和 eviction 可并行；consecutive detection 把 eviction 中连续修改合并为一次，减少 data race，在 CacheLib/RocksDB 上提高并发吞吐并保持相近 hit ratio。
  - 相较复杂全局排序和粗粒度锁的 eviction policy，核心创新是从并发数据结构而非单纯命中率设计 replacement，以近似策略换取可扩展操作路径。
  - cache eviction、lock-free data structure、CacheLib、concurrent throughput
