# SIGMETRICS 2026 论文列表

## 范围与核验

[SIGMETRICS 2026 官方 Accepted Papers](https://www.sigmetrics.org/sigmetrics2026/accepted.html) 共列出 80 篇受邀在本届报告的正式论文：Summer 23 篇、Fall 25 篇、Winter 32 篇。本文只收录这些正式论文，不含 poster、SRC、workshop、tutorial 或 keynote。标题和作者逐项与 DOI 元数据及 POMACS OpenTOC 交叉核验；其中 73 篇为 POMACS 正式论文，另有 7 篇发表于 ACM SIGMETRICS Performance Evaluation Review 的 archival summary，后者在标签中单独标明，不能与常规 POMACS 全文混为一类。

标题均链接到 DOI 落地页。本地已保留并验证 30 份合法开放 PDF，目录为 `reference/SIGMETRICS/2026/`；其余条目以 DOI 摘要和官方元数据完成预读，不以 PDF 获取失败阻塞清单。

方向计数采用互斥主方向：每篇只按核心研究对象计入一类，因此跨方向工作不会重复累计。

| 主方向 | 论文数 | 占比 |
|---|---:|---:|
| 排队、调度与在线优化 | 15 | 18.8% |
| LLM 与生成式 AI 系统 | 13 | 16.2% |
| 云、存储与系统运行时 | 12 | 15.0% |
| 网络测量、协议与基础设施 | 11 | 13.8% |
| 安全、隐私与区块链 | 7 | 8.8% |
| 机器学习系统与加速器 | 7 | 8.8% |
| 量子与新型计算 | 6 | 7.5% |
| 公平分配、市场与博弈 | 6 | 7.5% |
| 可持续计算 | 3 | 3.8% |

年度观察：

- 排队、调度与在线优化仍居首（15/80，18.8%），但 LLM 与生成式 AI 系统已升至第二（13/80，16.2%）；云/存储/运行时（12/80）和网络（11/80）继续构成稳定底座。前四类合计 51/80（63.8%）。
- LLM 研究已经从单点 kernel 扩展为完整资源路径：跨地域扩缩容与路由、prefill/decode 调度、GPU 存储栈、KV/prefix cache、边云 speculative decoding、训练 dropout kernel，以及性能—能耗和公网部署风险测量。共同方法是把请求长度、批次/队列、缓存复用、硬件状态、网络和 SLO 放进同一在线决策。
- Agent 相关仍少且边界清楚：MeshAgent 优化的是用 LLM 执行网络管理的生成—约束—验证闭环；CAP 用 LLM 辅助配置诊断；多请求工作流论文测量 agentic/compound-AI 的基础设施代价。传统 DRL、multi-agent bandit 和经济主体模拟均不计入 LLM Agent。
- 可持续性从 1 篇主方向增至 3 篇，并从硬件生命周期扩展到按流碳核算、储能需求管理和绿色装箱；HealthServe、GreenCache 等又把健康/碳目标嵌入 LLM serving，因互斥统计按主要系统对象归入 LLM 类。

Agent 相关分类：

| 分类 | 论文数 | 对应论文或边界 |
|---|---:|---|
| Agent System | 0 | 无直接研究通用规划—行动—反馈—迭代机制的论文 |
| Agent Infra | 1 | Characterizing Performance-Energy Trade-offs of Large Language Models in Multi-Request Workflows |
| Agent for Systems | 1 | Enabling Reliable Network Management with Large Language Models（MeshAgent） |
| LLM for Systems | 1 | CAP: Detecting Network Device Misconfigurations with Context-Aware Prompting of LLMs |

四类按论文的核心贡献互斥计数。EviDex 是可被 Agent 使用的检索基础设施，但正文核心是通用、持续更新的 RAG 索引，故只标作 agent-adjacent，不纳入 Agent Infra。

## 论文条目

### Summer Deadline（23 篇）

- [From Measurement to Emissions: Assessing the Carbon Footprint of Traffic Flows](https://doi.org/10.1145/3771569)
  - Sawsan El-Zahr, Noa Zilberman (University of Oxford)
  - 论文把交换机吞吐量和包速率计数器作为输入，从三类交换机在合成与真实流量下的功耗测量拟合瞬时功率模型，再按 attributional 与 consequential 两种口径把共享设备排放分摊到单条流；模型跨设备和 trace 的功率预测准确率超过 96%。
  - 相较只能给设备或网络总量的碳核算，核心创新是仅依赖现有流量遥测便把碳成本下钻到 flow，并显式区分平均分摊与新增流量引起的边际排放，因而可直接支持按流决策。
  - flow-level carbon accounting、switch power model、network telemetry、attributional/consequential emissions

- [Shedding Light on Shadows: Automatically Tracing Illicit Money Flows on EVM-Compatible Blockchains](https://doi.org/10.1145/3771578)
  - Yicheng Huo (Zhejiang University); Yufeng Hu (City University of Hong Kong); Yajin Zhou (Zhejiang University); Ting Yu (Mohamed bin Zayed University of Artificial Intelligence); Lei Wu (Zhejiang University); Cong Wang (City University of Hong Kong)
  - MFTracer 面向 EVM 兼容链上的非法资金追踪，从交易级调用与代币转移构造可跨 DeFi 协议解释的多层资金流图，用专门的存储和下游传播模拟沿 swap、bridge 等操作恢复去向；在真实案件上取得约 94% 追踪准确率。
  - 相较依赖地址启发式或为每种协议手写规则，核心创新是以交易语义统一表达协议组合，并把大规模图存储与资金传播执行共同设计，使跨协议、跨多跳的自动取证可扩展。
  - illicit fund tracing、EVM blockchains、DeFi transaction semantics、money-flow graph

- [Anchor: Reducing Temporal and Spatial Output Performance Variability on Quantum Computers](https://doi.org/10.1145/3771562)
  - Yuqian Huo, Daniel Leeds, Jason Z. Ludmir, Nicholas S. DiBrita, Tirthak Patel (Rice University)
  - Anchor 针对同一量子电路在不同时间和不同物理区域执行时保真度波动的问题，把校准数据与电路映射候选输入线性规划，在不改变算法逻辑的前提下选择更稳定的执行时段与 qubit 区域；实验将时空输出性能变异降低约 73%。
  - 相较只最小化静态门错误率或把多次运行视为同分布样本，核心创新是把量子机的时间漂移和空间不均匀作为一等优化变量，以输出稳定性而非单次理想保真度指导放置。
  - quantum reliability、spatio-temporal variability、qubit mapping、linear optimization

- [Better than Optimal: Improving Adaptive Stochastic Quantization Using Shared Randomness](https://doi.org/10.1145/3771564)
  - Ran Ben Basat (University College London and Broadcom); Yaniv Ben-Itzhak (Broadcom); Michael Mitzenmacher (Harvard University); Shay Vargaftik (Broadcom)
  - Simba 用发送端和接收端共享的随机性，在每次通信时从多个量化值集合中随机选择编码，使同样位宽能表达远多于单一 codebook 的有效取值；它用于分布式学习的梯度/模型传输时保持无偏，并提高收敛精度与通信效率。
  - 相较自适应随机量化仍被固定值集合限制，核心创新是用共享随机数把可恢复的选择信息移出消息本身，获得随候选集合数二次增长的精度而不同比增加传输位数。
  - distributed training、unbiased quantization、shared randomness、communication compression

- [Learning with Episodic Hypothesis Testing in General Games: A Framework for Equilibrium Selection](https://doi.org/10.1145/3771571)
  - Ruifan Yang (Cornell University); Manxi Wu (University of California Berkeley)
  - 论文研究一般和博弈中的均衡选择：参与者在一个 episode 内按当前信念行动，episode 之间主动检验关于对手策略的假设并更新信念；算法在效用驱动探索下收敛到近似 Nash 均衡，并可优先选择最小变换效用最大的均衡。
  - 相较无差别收敛到任意均衡或持续逐轮探索，核心创新是把昂贵探索组织成周期性假设检验，并把均衡的社会选择目标写入学习动力学，兼顾收敛与结果偏好。
  - equilibrium selection、episodic hypothesis testing、general-sum games、utility-driven exploration

- [Exploring the 5G Digital Divide in the Non-Contiguous US: LEO Satellites to the Rescue?](https://doi.org/10.1145/3771568)
  - Sizhe Wang, Moinak Ghoshal, Yufei Feng, Imran Khan, Phuc Dinh (Northeastern University); Omar Basit (Purdue University); Zhekun Yu (Northeastern University); Y. Charlie Hu (Purdue University); Dimitrios Koutsonikolas (Northeastern University)
  - 作者沿阿拉斯加、夏威夷和美国本土约 4200 公里路线同时测量三家蜂窝运营商与 Starlink，记录 5G 覆盖、吞吐、时延和切换，在非连续州定位仍缺服务的地段，并评估蜂窝与 LEO 多路径聚合能否填补覆盖及性能缺口。
  - 相较只用覆盖图或固定测速点讨论数字鸿沟，核心创新是以跨区域同步移动测量把 5G 与卫星链路置于同一基线，并量化两类接入互补而非简单替代的条件。
  - 5G digital divide、Starlink、mobile measurement、multipath access

- [Sequential Fair Allocation With Replenishments: A Little Envy Goes An Exponentially Long Way](https://doi.org/10.1145/3820171.3806858)
  - Chido Onyeze (Cornell University); Sean R. Sinclair (Northwestern University); Chamsi Hssaine (University of Southern California, Marshall School of Business); Siddhartha Banerjee (Cornell University)
  - 论文研究库存容量为 M、资源随机补货且请求顺序到达的公平分配，设计 Bang-Bang 策略在每次到达时决定立即分配或保留库存；结果刻画允许最大 envy 为 Δ 时，效率损失如何从 1/M 量级跨越到随 ΔM 指数下降。
  - 相较只看无嫉妒或只优化利用率，核心创新是给出 envy 松弛带来效率跃迁的精确相变，并提供达到该界的在线策略；该条为 Performance Evaluation Review 的归档摘要，而非常规 POMACS 全文。
  - sequential fair allocation、stochastic replenishment、envy-efficiency tradeoff、PER archival summary

- [Optimizing Storage Overhead of User Behavior Log for ML-embedded Mobile Apps](https://doi.org/10.1145/3771575)
  - Chen Gong, Yan Zhuang, Zhenzhe Zheng (Shanghai Jiao Tong University); Yiliu Chen, Sheng Wang (ByteDance); Fan Wu, Guihai Chen (Shanghai Jiao Tong University)
  - AdaLog 面向嵌入 ML 的移动应用行为日志，把特征、模型和日志字段之间的复用关系建成超图，用最大权匹配消除跨任务重复记录；对高密度文件采用虚拟哈希，并只增量更新受模型变化影响的日志布局，以压缩设备侧存储与 I/O。
  - 相较每个模型独立保存原始特征或只做通用压缩，核心创新是利用多模型数据依赖联合决定‘记录一次、供谁复用’，并让布局在模型集合变化时无需全量重写。
  - on-device ML、behavior logging、hypergraph deduplication、storage optimization

- [Benchmarking and Characterization of Large Language Model Inference on Apple Silicon](https://doi.org/10.1145/3771563)
  - Afsara Benazir, Felix Xiaozhu Lin (University of Virginia)
  - 论文在五代 Apple Silicon 上对 8B 至 405B LLM、14 种量化和多个本地运行时做端到端基准，分别测量首 token、逐 token 吞吐、内存占用、带宽和功耗，并拆解 unified memory、解量化与计算 kernel 的瓶颈；结果显示更低位宽并不总是更快。
  - 相较只报单模型 token/s 的设备测评，核心创新是跨芯片、模型规模、量化格式和运行时建立可解释矩阵，用瓶颈分解说明容量可装下、内存带宽和实际速度之间为何不等价。
  - on-device LLM inference、Apple Silicon、quantization、performance-energy characterization

- [ScaleQsim: Highly Scalable Quantum Circuit Simulation Framework for Exascale HPC Systems](https://doi.org/10.1145/3771577)
  - Changjong Kim, Ehan Sohn, Seunghwan Kim (Seoul National University of Science and Technology); Alex Sim, Kesheng Wu, Houjun Tang (Lawrence Berkeley National Laboratory); Yongseok Son (Chung-Ang University); Sunggon Kim (Seoul National University of Science and Technology)
  - ScaleQsim 将 state-vector 分片分布到多节点多 GPU，并按量子门类型、通信范围和设备状态自适应选择计算/通信 kernel；系统在 512 张 GPU 上扩展到 42 qubit 电路，面向超算环境协调节点内和节点间数据交换。
  - 相较绑定单一 kernel 或只扩展节点内模拟器，核心创新是把大规模状态分布、门级 kernel 选择和分层通信统一进运行时，使量子电路仿真真正利用 exascale GPU 集群。
  - quantum circuit simulation、multi-GPU、state-vector partitioning、adaptive kernels

- [Three Birds with One Stone: Improving Performance, Convergence, and System Throughput with NEST](https://doi.org/10.1145/3771580)
  - Yuqian Huo, David Quiroga, Anastasios Kyrillidis, Tirthak Patel (Rice University)
  - NEST 面向 VQA 执行过程中物理 qubit 质量持续波动的环境，依据算法阶段动态选择不同保真度的 qubit 区域：早期容忍较低质量以让出稀缺好 qubit，后期逐步迁入高质量区域，从而同时改善单任务结果、收敛速度和多任务共置吞吐。
  - 相较整次 VQA 固定使用一组最好 qubit，核心创新是发现迭代阶段对噪声敏感度不同，并据此做随时间变化的质量分配，把单电路保真度优化扩展为多 VQA 系统调度。
  - variational quantum algorithms、noise-aware scheduling、qubit allocation、multi-program throughput

- [Pittacus: Optimizing LLM Serving on Cloud Data Centers with Forecast Aware Auto-Scaling](https://doi.org/10.1145/3771576)
  - Shashwat Jaiswal (University of Illinois Urbana-Champaign, USA); Kunal Jain (Microsoft); Yogesh Simmhan (Indian Institute of Science (IISc), Bangalore); Anjaly Parayil (Microsoft Research); Ankur Mallick, Rujia Wang, Renee St. Amant, Chetan Bansal (Microsoft); Victor Rühle (Microsoft Research); Anoop Kulkarni, Steve Kofsky (Microsoft); Saravan Rajmohan (Microsoft 365)
  - 论文以 Office 365 每日逾千万次请求为负载，短时间尺度依据各数据中心队列、模型副本和网络时延把单个推理请求路由到可满足 SLO 的站点，长时间尺度再用预测与整数规划决定 GPU VM 扩缩容及模型放置；正式发表标题为 SageServe，accepted 页面标题为 Pittacus。
  - 相较先固定跨地域部署再局部调路由，核心创新是把预测感知的容量规划、异构模型放置与实时跨数据中心路由做成双时间尺度闭环，从全局减少闲置 GPU 和 SLA 违约。
  - LLM serving、geo-distributed inference、forecast-aware autoscaling、request routing

- [Optimal Scheduling Algorithms for LLM Inference: Theory and Practice](https://doi.org/10.1145/3771574)
  - Agrim Bari, Parikshit Hegde, Gustavo de Veciana (The University of Texas at Austin)
  - 论文把自回归推理拆为一次性、算力密集的 prefill 与逐 token、内存密集的 decode，按 prompt 长度、当前 decode 批次和 token 间时延余量在线决定每个请求何时进入哪一阶段；RAD 保证吞吐最优，SLAI 则优先即将触碰 TBT 限制的 decode 并安排 prefill。
  - 相较 FCFS 或只对连续批处理做启发式调整，核心创新是先给出两阶段推理的可证明最优 tiling/资源分配结构，再把该结构实现为同时面向吞吐和 per-request SLO 的调度器。
  - LLM inference scheduling、prefill-decode coordination、throughput optimality、time-between-token SLO

- [Enabling Reliable Network Management with Large Language Models](https://doi.org/10.1145/3771567)
  - Yajie Zhou (University of Maryland); Kevin Hsieh, Sathiya Kumaran Mani (Microsoft Research); Srikanth Kandula (Amazon Web Services); Zaoxing Liu (University of Maryland)
  - MeshAgent 面向用 LLM 生成网络配置与诊断操作的管理任务，先从少量示例查询中抽取设备/策略必须满足的 invariants，再把这些约束用于指导候选生成、执行前验证和不确定时拒答；在多个管理任务上的有效率超过 95%。
  - 相较靠 prompt 让 LLM 直接吐出命令并事后人工检查，核心创新是从示例自动归纳可执行安全约束，把生成—验证—拒答组成闭环，因此属于 Agent for Systems，而不是单纯文本问答或 Agent Infra。
  - Agent for Systems、network management、invariant-guided generation、validation and abstention

- [Beyond Single-Tokenomics: How Farcaster’s Pluralistic Incentives Reshape Social Networking](https://doi.org/10.1145/3771565)
  - Wen Yang, Qiming Ye (Hong Kong University of Science and Technology (Guangzhou)); Onur Ascigil (Lancaster University); Saidu Sokoto (City St George’s, University of London); Leonhard Balduf (TU Darmstadt); Michał Król (City St George’s, University of London); Gareth Tyson (Hong Kong University of Science and Technology (Guangzhou))
  - 论文追踪 Farcaster 约 57.4 万用户在多种 token 激励机制下的发帖、互动、关注与内容质量，并用准实验/因果分析比较奖励上线前后；结果揭示不同激励会扩大创作量，却不一定同步改善质量或社交关系。
  - 相较把 Web3 社交平台概括为单一代币经济，核心创新是把并存激励逐项分离，估计其对供给、质量和网络形成的异质因果效应，展示 pluralistic tokenomics 的相互作用。
  - decentralized social networks、token incentives、causal measurement、Farcaster

- [Heterogeneous Multi-agent Multi-armed Bandit on Stochastic Block Models](https://doi.org/10.1145/3771570)
  - Mengfan Xu (University of Massachusetts Amherst); Liren Shan (Toyota Technological Institute at Chicago); Fatemeh Ghaffari, Xuchuang Wang (University of Massachusetts Amherst); Xutong Liu (Carnegie Mellon University); Mohammad Hajiesmaili (University of Massachusetts Amherst)
  - 论文研究网络连接和回报都具有群组异质性的多主体 bandit：通信图来自 stochastic block model，各主体只能观察本地拉臂结果并与邻居交换统计；算法联合做簇识别、加权共识和探索，在簇内共享信息同时避免跨簇负迁移，取得对数遗憾。
  - 相较假定所有主体同分布或通信图已知分群，核心创新是让 reward cluster 与 network cluster 在学习中被共同发现并用于信息聚合；这里的 agent 是数学决策主体，不属于 LLM Agent 四分类。
  - multi-agent bandit、stochastic block model、clustered rewards、non-LLM agent

- [A Tale of Two Traffics: Optimizing Tail Latency in the Light-Tailed M/G/k](https://doi.org/10.1145/3771561)
  - George Yu, Amit Harlev, Reevu Adakroy, Ziv Scully (Cornell University)
  - 论文研究轻尾服务时间下 M/G/k 的尾延迟调度，指出面向重尾任务的 Gamma-Boost 在该区间会恶化极端响应时间，并构造一种在关键状态反而优先较大作业的策略，以减少服务器碎片和后续排队；该策略在各负载下优化尾部衰减率。
  - 相较把单服务器 SRPT/重尾直觉直接移植到多服务器，核心创新是揭示轻尾场景中‘先做大作业’可改善尾延迟的反直觉机制，并给出全负载理论最优性。
  - M/G/k scheduling、tail latency、light-tailed jobs、large-job priority

- [The Impact of IP Version on Household Internet Speed: A Comparative Study](https://doi.org/10.1145/3771579)
  - Amanda Hsu (Georgia Institute of Technology); Nick Feamster (University of Chicago); Paul Pearce, Frank Li (Georgia Institute of Technology)
  - 作者从家庭宽带测量中为同一接入环境配对 IPv4 与 IPv6 测试，控制 ISP、地点、设备和测量软件后比较吞吐与时延，并追溯差异到运营商路径和基础设施；约 18.3% 家庭的两种 IP 版本速度差超过 5%。
  - 相较用全网总体均值比较 IPv4/IPv6，核心创新是以家庭级配对和基础设施控制隔离协议版本效应，避免把供应商、终端或地域差异误判成 IPv6 性能。
  - IPv4/IPv6、household broadband、paired measurement、access-network performance

- [Outperforming Multiserver SRPT at All Loads](https://doi.org/10.1145/3820171.3806892)
  - Izzy Grosof, Daniela Hurtado Lange (Northwestern University)
  - SEK-SMOD 面向 k 服务器、已知作业大小的在线队列，不总是让最短剩余作业先运行，而在会提高并行利用率的特定状态插入较大作业；论文证明它对所有负载和服务时间分布的平均响应时间都严格优于多服务器 SRPT。
  - 相较长期被视为自然基线的 SRPT-k，核心创新是识别其因同时占用多服务器而产生的利用率缺口，并给出首个全分布、全负载支配它的调度规则；该条为 PER 归档摘要。
  - multiserver scheduling、mean response time、SRPT、PER archival summary

- [ObliQ: Solving Quadratic Unconstrained Binary Optimization Problems on Real Photonic Quantum Machines](https://doi.org/10.1145/3771573)
  - Aditya Ranjan, Daniel Silver (Northeastern University); Tirthak Patel (Rice University); Bhargav Chickmagalurnanjun, Devesh Tiwari (Northeastern University)
  - ObliQ 面向真实光子量子机求解 QUBO，把问题结构固化进不可调光学电路，再以少量可调变分参数补偿实例和硬件误差，并由软硬件协同流程完成 QUBO 到光子器件配置的映射；公开摘要未披露更细的搜索器与反馈变量。
  - 相较完全可编程但校准开销高的光子线路或只支持固定问题的专用线路，核心创新是以‘问题定制固定层＋可调变分层’在可制造性、控制复杂度和解质量之间折中。
  - photonic quantum computing、QUBO、hybrid fixed-parametric circuit、hardware-software co-design

- [Cross-Chain Arbitrage: The Next Frontier of MEV in Decentralized Finance](https://doi.org/10.1145/3771566)
  - Burak Öz (Technical University of Munich); Christof Ferreira Torres (INESC-ID / Instituto Superior Técnico (IST), University of Lisbon); Christoph Schlegel, Bruno Mazorra (Flashbots); Jonas Gebele, Filip Rezabek, Florian Matthes (Technical University of Munich)
  - 论文从九条链重建一年内 24.2 万笔跨链套利、总额约 8.68 亿美元，区分预先在多链备货的 inventory 策略与等待 bridge 转移的策略，并分析价格差、桥延迟、资金占用和失败风险如何决定单笔路径与利润。
  - 相较只统计单链 MEV 或把桥交易视为普通转账，核心创新是把多链上的买卖腿按时间和金额配对为完整套利事件，首次量化低延迟库存与低资本桥接之间的系统性权衡。
  - cross-chain arbitrage、MEV、bridge latency、DeFi measurement

- [Multiple Sides of 36 Coins: Measuring Peer-to-Peer Infrastructure Across Cryptocurrencies](https://doi.org/10.1145/3771572)
  - Lucianna Kiffer (IMDEA Networks); Lioba Heimbach, Yann Vonlanthen (ETH Zurich); Dennis Trautwein (University of Göttingen); Oliver Gasser (IPinfo)
  - 作者为 36 种加密货币部署 15 个协议 crawler，并结合社区节点列表和 Internet 主动探测，持续发现 P2P 节点、版本、IPv6、AS、地理位置和 churn；数据揭示不同链的可见规模、中心化程度与节点生命周期差异。
  - 相较只测 Bitcoin/Ethereum 或使用单一 discovery 接口，核心创新是用统一采集框架跨 36 个不兼容协议交叉校验可达节点，使币种间基础设施比较具有同口径。
  - cryptocurrency P2P networks、active measurement、node discovery、infrastructure centralization

- [μ-VF: Enabling Virtualization of Embedded FPGAs](https://doi.org/10.1145/3771581)
  - Vincenzo Bucaria, Francesco Longo, Giovanni Merlino (University of Messina); Francesco Restuccia (Northeastern University)
  - μ-VF 在嵌入式 FPGA 上把处理系统软件放进容器，并把可编程逻辑划成可独占的动态区域，同时虚拟化 GPIO 等板级外设；租户可以独立装载 bitstream 与应用，额外逻辑占用低于 10%。
  - 相较只虚拟化 ARM 处理器或依赖数据中心级 FPGA 管理卡，核心创新是在资源受限 SoC 上贯通 PS、PL 与外设隔离，让嵌入式板卡支持低开销多租户全栈部署。
  - embedded FPGA virtualization、SoC isolation、partial reconfiguration、GPIO virtualization

### Fall Deadline（25 篇）

- [Online Smoothed Demand Management](https://doi.org/10.1145/3820171.3806838)
  - Adam Lechowicz (University of Massachusetts Amherst); Nicolas Christianson (Stanford University); Mohammad Hajiesmaili (University of Massachusetts Amherst); Adam Wierman (California Institute of Technology); Prashant Shenoy (University of Massachusetts Amherst)
  - OSDM 同时处理可立即调节和带截止期的电力需求、可再生供给、实时购电价格与电池状态，每时隙决定买电、充放电和延后多少任务，以平滑峰值并控制采购/违约成本；PAAD 给出竞争界，另用可微学习适应未知序列。
  - 相较只做无储能 demand response 或用预测器直接替代在线控制，核心创新是把电池差分状态、deadline 需求和平滑成本放入同一 primal-dual 规则，并让学习组件改善平均表现而不移除理论护栏；该条为 PER 归档摘要。
  - demand response、battery storage、learning-augmented online control、PER archival summary

- [Towards Scalable Storage Architectures for GPU Clusters Running Large Language Models](https://doi.org/10.1145/3788106)
  - Ali Sedaghatgoo (Sharif University of Technology); Reza Salkhordeh (Johannes Gutenberg-Universitat Mainz); Andre Brinkmann (Johannes Gutenberg University Mainz); Hossein Asadi (Sharif University of Technology)
  - 作者在 SATA/NVMe SSD、Optane/PMem 与多种 GPU 直接路径上测试 libaio、io_uring、SPDK、GDS 等超过 2.5 万种配置，分别模拟 LLM 预训练 checkpoint、微调数据加载和推理权重/缓存访问；结果给出不同阶段应选的软件栈和介质，例如推理偏向 io_uring、训练可受益于 GDS。
  - 相较以单一存储 benchmark 推断 GPU 集群需求，核心创新是把 LLM 生命周期中的实际 I/O 模式与从文件 API 到 GPU-direct 的完整路径交叉测试，得到可按阶段选型而非一刀切的存储架构。
  - LLM storage、GPU clusters、GPUDirect Storage、I/O stack characterization

- [Sumeru: Towards Understanding and Achieving Cache-Optimal Inbound Network I/O](https://doi.org/10.1145/3788104)
  - Minhu Wang (Tsinghua University); Mingwei Xu (Quan Cheng Laboratory); Jianping Wu (Tsinghua University)
  - Sumeru 从网卡接收队列和软件队列的演化推导未来数据包访问 cache 的轨迹，把不同流量分到 cache-friendly 与 bypass 路径；运行时用 active queue management 和动态 cache 分区响应流量与核负载变化，使 inbound network I/O 的命中率接近 100%。
  - 相较按 flow hash 静态绑核或事后调 LLC way，核心创新是用队列状态预测数据到达 CPU 的时间与复用距离，再联合决定路径、排队和 cache 容量，直接优化入站处理的缓存轨迹。
  - inbound network I/O、cache trajectory、active queue management、dynamic cache partitioning

- [A Comprehensive Study of Satellite Network Performance During Severe or Extreme Geomagnetic Storms over 1.5 Years (May 2024 - Oct 2025)](https://doi.org/10.1145/3788084)
  - Saeed Fadaei (University of Surrey); Aravindh Raman (Cisco ThousandEyes); Prince Bhardwaj Pawankumar Sharma (University of Surrey); Nishanth Sastry (University of Surrey, UK)
  - 论文汇总 2024 年 5 月至 2025 年 10 月的 15 次强/极强地磁暴，通过七地 LEOScope、约 400 万次 M-Lab 测试和 Cloudflare AIM 对照 Starlink 的吞吐、时延与丢包变化，并按地理纬度、天气、轨道及地面网络排除混杂；部分事件吞吐下降约 20%。
  - 相较凭个案或空间天气相关性推测卫星受扰，核心创新是用三套独立长期数据源把暴发前后和未受影响地区配对，给出可归因到地磁活动的端到端网络效应。
  - Starlink、geomagnetic storms、longitudinal measurement、satellite-network resilience

- [Higher-Order Approximations of Sojourn Times in M/G/1 Queues via Stein's Method](https://doi.org/10.1145/3788095)
  - Bihan Chatterjee, Siva Theja Maguluri, Debankur Mukherjee (Georgia Institute of Technology)
  - 论文针对 M/G/1 队列，以 Stein 方法和生成元展开从服务时间矩得到逗留时间分布的二阶及更高阶近似，并显式保留有限负载下的误差项；moment matching 让近似在尚未进入重流量极限时仍可计算。
  - 相较只给 heavy-traffic 一阶极限或均值近似，核心创新是建立可逐阶修正的预渐近展开，把有限负载、服务分布高阶矩与可证明误差连接起来。
  - M/G/1 queue、Stein's method、sojourn-time approximation、pre-asymptotic analysis

- [Cache Your Prompt When It's Green - Carbon-aware Caching for Large Language Model Serving](https://doi.org/10.1145/3788087)
  - Yuyang Tian, Desen Sun (University of Waterloo); Yi Ding (Purdue University); Sihang Liu (University of Waterloo)
  - GreenCache 面向 LLM serving 的 prompt/KV cache，按请求复用概率、GPU/存储占用、地区电力碳强度以及设备 embodied carbon 计算保留与迁移代价，运行时在延迟 SLO 下动态分配缓存资源；trace 实验比较命中收益与额外硬件碳成本。
  - 相较只按 hit rate 或电费决定缓存，核心创新是把运行电力和新增缓存设备的隐含碳统一到逐请求决策，避免为省计算而配置更多硬件反而增加全生命周期排放。
  - LLM KV cache、carbon-aware serving、embodied carbon、SLO-constrained caching

- [Shiny Objects: Object-Centric Characterization of Chromium](https://doi.org/10.1145/3788102)
  - Saket Upadhyay, Ashish Venkat (University of Virginia)
  - Shiny Objects 用轻量、线程安全的 profiler 在 Chromium 运行时跟踪对象类型、大小、生命周期、地址邻近性和读写活动，并在 12 类真实浏览负载中关联分配点与页面阶段，刻画哪些对象形成内存峰值和长尾占用。
  - 相较只看 heap 总量或离线采样 allocation，核心创新是以对象为中心联合记录时空位置、类型和访问行为，在低扰动下把浏览器内存现象定位到具体生命周期模式。
  - Chromium、object-centric profiling、memory characterization、runtime instrumentation

- [A Fine-Grained and Efficient Reliability Analysis Framework for Noisy Quantum Circuits](https://doi.org/10.1145/3788085)
  - Jindi Wu (DePaul University); Tianjie Hu, Qun Li (William & Mary)
  - 该框架先从目标量子电路移除逻辑运算、保留门序列与硬件噪声暴露结构，生成可廉价执行的 Noise Proxy Circuit，再由其统计量计算 Proxy Fidelity，以估计原电路在不同映射和噪声参数下的可靠性而无需完整含噪模拟。
  - 相较逐电路 Monte Carlo 噪声仿真或只累乘门错误率，核心创新是构造保持噪声时序却不承担算法计算的代理电路，从而得到细粒度、可在设备上验证且成本低的可靠性估计。
  - noisy quantum circuits、proxy circuit、fidelity estimation、execution-efficient reliability

- [Empirical Gittins for data-driven M/G/1 scheduling with arbitrary job size distributions](https://doi.org/10.1145/3788091)
  - Shefali Ramakrishna, Amit Harlev, Ziv Scully (Cornell University)
  - 论文从历史样本构造经验服务时间分布，再据此计算 M/G/1 的 Gittins index 在线选择作业；对尾部样本不足的情形引入截断和尾部先验，并证明以高概率逼近真实分布下的最优平均响应时间。
  - 相较假定作业大小分布已知或先拟合参数分布，核心创新是直接把经验 CDF 转为可执行 Gittins 调度，并量化有限样本、截断和未知长尾对最优性的影响。
  - data-driven scheduling、Gittins index、M/G/1、empirical job-size distribution

- [Nash Equilibria in Uniform Price Auctions: Theory, Computation, and Market Insights](https://doi.org/10.1145/3820171.3806860)
  - Yifan Feng (National University of Singapore); Negin Golrezaei (Massachusetts Institute of Technology); Qinzhen Li (National University of Singapore)
  - 论文刻画 uniform-price auction 中纯 Nash 均衡可产生的分配和清算价，并把给定估值下选择高福利或高收入均衡写成混合整数规划；进一步分析 reserve price、需求减少和串谋稳定性。
  - 相较只给最坏 price-of-anarchy 界，核心创新是提供可枚举/优化实际均衡结果的计算表述，让市场设计者能比较储备价、福利与收入而非只判断均衡是否存在；该条为 PER 归档摘要。
  - uniform-price auction、Nash equilibrium、mixed-integer optimization、PER archival summary

- [Dynamic SLA-aware Network Slice Monitoring](https://doi.org/10.1145/3788090)
  - Niloy Saha, Mina Tahmasbi Arashloo (University of Waterloo); Nashid Shahriar (University of Regina); Raouf Boutaba (University of Waterloo)
  - SliceScope 面向共享 5G/云网络切片，把各 SLA 指标和可用遥测 primitive 建成监测契约，按业务关键性与当前异常风险动态分配 INT 采样预算；只有状态变化达到阈值时才提升采样或重构路径，形成监测—判定—再配置闭环。
  - 相较每个 slice 固定周期、固定字段地全量遥测，核心创新是把 SLA 风险直接映射为 telemetry 资源分配，并以 change-triggered INT 在可见性与带宽/处理开销间动态取舍。
  - network slicing、SLA monitoring、in-band telemetry、change-triggered sampling

- [A Variegated Look at Direct-to-Cell Satellites in the Wild](https://doi.org/10.1145/3788086)
  - Wei Liu, Jingyi Lan, Yuanjie Li, Bowen Sun, Yekai Dong, Yufeng Wang, Hewu Li, Qian Wu, Zeqi Lai, Jun Liu (Tsinghua University)
  - 作者对商用 Starlink direct-to-cell 做两个月全栈测量，观察终端接入、频偏补偿、小区切换、吞吐、时延与重传，并结合 3GPP NTN 仿真解释协议栈功能划分；结果显示为兼容传统手机保留的机制会造成接入失败和切换空洞。
  - 相较只根据卫星链路预算评估 D2C，核心创新是从空口到 Internet 应用层还原在野系统，并把观测到的失败定位到 legacy cellular compatibility 与移动卫星拓扑的冲突。
  - direct-to-cell satellite、3GPP NTN、mobility handover、full-stack measurement

- [Guiding the Recommender: Information-Aware Auto-Bidding for Content Promotion](https://doi.org/10.1145/3788094)
  - Yumou Liu, Zhenzhe Zheng (Shanghai Jiao Tong University); Jiang Rong, Yao Hu (Xiaohongshu); Fan Wu, Guihai Chen (Shanghai Jiao Tong University)
  - 论文研究平台替创作者自动出价推广内容时，曝光既带来即时覆盖又会污染推荐器学习信号的问题；算法用 Fisher information 衡量一轮推广对后续推荐模型的知识增益，通过 Lagrange pacing 控预算，再以边际价值/零阶估计在线决定给哪条内容加价。
  - 相较只按点击率或短期转化出价，核心创新是把‘帮助推荐器认识内容’作为可计量的长期回报纳入竞价，并在未知推荐响应下联合优化探索覆盖与预算消耗。
  - auto-bidding、recommender systems、information gain、budget pacing

- [Robustness of the 2-Choices Dynamics to Node Failures](https://doi.org/10.1145/3788101)
  - Luke Meredith, Arpan Mukhopadhyay (University of Warwick)
  - 论文分析 power-of-two-choices 负载均衡在节点独立失效概率为 α 时的长期动力学：当 α 低于阈值，初始多数状态可保持指数时间；超过阈值后故障噪声会在对数时间内抹平偏置，并给出两侧集中界。
  - 相较默认节点永远可用的经典 two-choices 模型，核心创新是证明随机失效引起清晰相变，定量说明少量故障何时不影响选择放大效应、何时会重置系统记忆。
  - power of two choices、node failures、phase transition、load-balancing dynamics

- [The Multiserver-Job Stochastic Recurrence Equation for Cloud Computing Performance Evaluation](https://doi.org/10.1145/3788105)
  - Francois Baccelli (INRIA); Diletta Olliaro (Ca' Foscari University of Venice, KTH Royal Institute of Technology); Marco Ajmone Marsan (IMDEA Networks Institute); Marin Andrea (University Ca' Foscari of Venice)
  - 论文用 Multiserver-Job Stochastic Recurrence Equation 表示每个作业需同时占用 α_n 台服务器的 GPU/并行作业系统，从到达与服务序列递推等待状态；借助递归与遍历理论给出稳定条件，并量化资源同步造成的空闲与 sub-perfect scaling。
  - 相较把并行作业拆成独立单服务器任务或仅靠离散事件仿真，核心创新是为 gang-scheduled 多服务器作业建立可分析的随机递推模型，从而直接判断稳定性和同步损失。
  - multiserver jobs、gang scheduling、stochastic recurrence、cloud performance modeling

- [Mapping the Landscape of LLM Deployment in the Wild: Prevalence, Patterns, and Perils](https://doi.org/10.1145/3788097)
  - Xinyi Hou, Jiahao Han, Yanjie Zhao, Shenao Wang, Haoyu Wang (Huazhong University of Science and Technology)
  - 作者对公网扫描并验证 32 万余个 LLM 服务，识别 15 类框架和 158 种 API endpoint，分析云地域、TLS、认证、模型暴露与默认配置；测量揭示大量实例把管理或推理接口直接暴露在 Internet 上。
  - 相较从 GitHub 使用量或少量 honeypot 推断部署生态，核心创新是建立 LLM-specific 的 Internet-wide 指纹和主动验证流程，同时量化普及度、框架碎片化与真实攻击面。
  - LLM deployment measurement、Internet-wide scanning、exposed inference APIs、security posture

- [Stochastic Network Utility Maximization in Strategic Queueing Systems: A Game-Theoretic Approach](https://doi.org/10.1145/3788103)
  - Quang Minh Nguyen (Massachusetts Institute of Technology); Randall Berry (Northwestern University); Eytan Modiano (Massachusetts Institute of Technology)
  - 论文把用户会策略性选择队列/服务量的随机网络效用最大化写成带队列约束的重复博弈，以 primal-dual 更新价格和动作，寻找近似 generalized Nash equilibrium；半正定规划变体给出 ε-GNE、队列有界与社会福利保证。
  - 相较假定用户服从中央调度的 NUM，核心创新是同时处理个体激励、随机到达和物理队列稳定性，让均衡计算不以牺牲拥塞控制可行性为代价。
  - network utility maximization、strategic queues、generalized Nash equilibrium、primal-dual control

- [Green Bin Packing](https://doi.org/10.1145/3788093)
  - Jackson Bibbens, Cooper Sigrist (University of Massachusetts Amherst); Bo Sun (University of Ottawa); Shahin Kamali (York University); Mohammad Hajiesmaili (University of Massachusetts Amherst)
  - Green Bin Packing 假设服务器利用率超过绿色阈值 G 后边际环境代价按 β 增长，在线决定每个到达物品放入哪一 bin；论文分析 β≤1/G 时 First Fit、Harmonic 等算法的竞争界，并覆盖高惩罚与扩展成本模型。
  - 相较只最小化开启服务器数的 bin packing，核心创新是把低利用率容量与越过功率/碳阈值后的非线性代价分开建模，给出绿色运行区间随 β、G 变化的算法选择条件。
  - green bin packing、utilization threshold、online placement、carbon-aware resource allocation

- [Offline Local Search for Online Stochastic Bandits](https://doi.org/10.1145/3820171.3806893)
  - Gerdus Benade (Boston University); Rathish Das (University of Houston); Thomas Lavastida (University of Texas at Dallas)
  - 论文给出一个通用 reduction：只要离线目标存在近似 local-search oracle，就能在反馈只来自已选动作的随机组合 bandit 中周期性探索邻域、更新经验收益并调用 oracle，获得 O(log³T) 量级的近似遗憾；实例覆盖调度、matroid 与聚类。
  - 相较为每种组合结构单独设计 UCB，核心创新是把成熟离线局部搜索黑盒化为在线学习器，并把 oracle 的近似误差与 bandit 探索损失统一进遗憾界；该条为 PER 归档摘要。
  - combinatorial bandit、offline-to-online reduction、local search、PER archival summary

- [CAPSULE: A Storage Prefetcher Harnessing Spatio-Temporal Locality for Cloud-Scale Workloads](https://doi.org/10.1145/3788088)
  - Agung Rahmat Ramadhan, Seehwan Yoo, Jongmoo Choi (Dankook University)
  - CAPSULE 对云存储 block trace 在线估计长 stack distance 访问的空间邻近性，把相近 LBA 聚成可独立预取的 capsule，并依据近期命中、污染和带宽状态调整每簇预取深度；在 729 个生产负载上减少被传统短距离相关器漏掉的读。
  - 相较只跟随最近地址或固定 stride 的 prefetcher，核心创新是让很久之后才复用的数据仍可凭空间簇被发现，并把簇级收益反馈用于抑制 cache pollution。
  - storage prefetching、spatio-temporal locality、cloud block traces、adaptive prefetch depth

- [Janus: A Dual-Mask Attention Transformer for Log-based Anomaly Detection in Cellular Networks](https://doi.org/10.1145/3788096)
  - Umakant Kulkarni (Purdue University/Dept. of Computer Science); Sonia Fahmy (Purdue University)
  - Janus 以蜂窝网运维日志序列为输入，用双 mask Transformer 分工建模：全局因果 attention 学事件流程和先后语法，局部语义 attention 只连接同 tag/相关字段，再以 curriculum 从常见流程逐步学习稀有异常，输出异常位置与类型。
  - 相较单一全局 attention 把模板语义和时序混在一起，核心创新是通过两套可解释 mask 显式分离 procedural grammar 与 field semantics，并用课程学习应对极端类别不平衡。
  - cellular log anomaly detection、dual-mask attention、procedural grammar、curriculum learning

- [Characterizing Performance-Energy Trade-offs of Large Language Models in Multi-Request Workflows](https://doi.org/10.1145/3788089)
  - Md. Monzurul Amin Ifath, Israat Haque (Dalhousie University)
  - 论文把多请求 LLM 工作流分为顺序、交互、agentic 与复合模式，在 A100 上分别用 vLLM 和 Parrot 改变输入/输出长度、并发、batch 与功率上限，测量 token 延迟、吞吐和能耗；结果显示最佳 batch/功率策略强依赖请求依赖图，Parrot 在限功率时也不总占优。
  - 相较以独立 chat 请求 benchmark serving engine，核心创新是把请求间依赖与 agentic 编排作为实验变量，揭示单请求最优配置无法直接外推到 compound-AI 工作流；属 Agent Infra 的工作负载测量，而非 Agent System 算法。
  - Agent Infra、compound AI workflows、LLM serving benchmark、performance-energy tradeoff

- [On Abnormal Execution Timing of Conditional Jump Instructions](https://doi.org/10.1145/3788099)
  - Annika Wilde (Ruhr University Bochum); Samira Briongos, Claudio Soriente (NEC Laboratories Europe); Ghassan Karame (Ruhr University Bochum)
  - 作者系统改变条件跳转在指令地址、32 字节边界、宏融合对和 uop cache/L1I 中的位置，记录同一代码序列异常的执行时间差，并追踪到前端取指/解码资源；这些稳定差异还能构造泄露控制流布局的隐蔽信道。
  - 相较把 branch timing 归因于 predictor 命中率，核心创新是隔离出跳转地址布局与宏融合共同触发的前端效应，说明功能等价代码仅因字节位置也会出现可利用的时序。
  - conditional branches、instruction frontend、timing side channel、microarchitectural characterization

- [Prediction-Specific Design of Learning-Augmented Algorithms](https://doi.org/10.1145/3788100)
  - Sizhe Li (The Chinese University of Hong Kong, Shenzhen); Nicolas Christianson (Stanford University); Tongxin Li (The Chinese University of Hong Kong, Shenzhen)
  - 论文主张针对预测器会提供的具体信号设计 learning-augmented 算法，而非用统一误差标量包裹任意预测；它把算法与预测接口写成双层优化，在 ski rental、one-max、动态功率和指数交易中求同时满足 consistency 与 robustness 的策略。
  - 相较先定在线算法再加入黑盒预测，核心创新是让‘预测什么’与‘如何用预测’共同优化，得到任务特定且可证明强最优的设计边界。
  - learning-augmented algorithms、prediction design、bilevel optimization、consistency-robustness

- [Experimental Study on System-Level Performance Impact of Read Disturbance in Modern SSDs](https://doi.org/10.1145/3788092)
  - Yonggon Park, Hyunuk Cho (POSTECH); Onur Mutlu (ETH Zurich); Sungjin Lee (POSTECH); Jisung Park (POSTECH (Pohang University of Science and Technology))
  - 论文在 10 家厂商的 15 款 NVMe SSD 上通过可控读压力量化 read disturbance 对真实系统 I/O 时延、吞吐和错误行为的影响，比较闪存类型、固件、访问模式与老化程度，并演示恶意读负载如何放大性能退化。
  - 相较停留在 NAND 单元错误率的器件研究，核心创新是跨商用盘把扰动传导到 OS 可见性能与攻击面，区分设备内部纠错可遮蔽和无法遮蔽的阶段。
  - NVMe SSD、read disturbance、system-level performance、storage security

### Winter Deadline（32 篇）

- [A Minimal-Assumption Analysis of Q-Learning with Time-Varying Policies](https://doi.org/10.1145/3805624)
  - Phalguni Nanda, Zaiwei Chen (Purdue University)
  - 论文分析行为策略随时间变化的 tabular Q-learning，仅要求最小不可约性而不假定固定 i.i.d. 采样；通过 Poisson 方程分解马尔可夫噪声，给出探索逐步改变时的有限时间误差与样本复杂度。
  - 相较依赖固定 ergodic policy 或强 mixing 常数的经典分析，核心创新是在非齐次数据流下仍分离优化误差、采样偏差与策略漂移，覆盖实际衰减探索。
  - Q-learning theory、time-varying policy、finite-time analysis、non-LLM reinforcement learning

- [A Unified Framework for Online Combinatorial Allocation of Reusable Resources under Endogenous Deterioration](https://doi.org/10.1145/3805625)
  - Qingsong Liu (University of Massachusetts Amherst); Mohammad Hajiesmaili (UMass Amherst)
  - 论文研究容量可重复使用、每次分配后会随累计使用退化的组合资源，请求在线到达并占用一组资源；IPRANK 依据当前剩余质量、回报和组合大小生成随机排名，决定接受及分配，以避免高价值资源过早耗损并获得对数依赖异质性的保证。
  - 相较把每次释放后的服务器视为全新或用即时回报贪心，核心创新是把 endogenous deterioration 纳入资源状态和排名惩罚，统一处理组合需求、复用周期与长期寿命。
  - reusable resources、endogenous deterioration、online combinatorial allocation、randomized ranking

- [ACALSim: A Scalable Parallel Simulation Framework for High-Performance System Design Space Exploration](https://doi.org/10.1145/3805626)
  - Wei-Fen Lin (Taiwan High-Performance Computing Education Association); Jen-Chien Chang, Yen-Po Chen (National Cheng Kung University); Zi-Yi Tai (Taiwan High-Performance Computing Education Association); Yu-Chen Chang (National Yang Ming Chiao Tung University); Chia-Pao Chiang, Yu-Yang Lee, Yu-Chieh Wang (National Cheng Kung University)
  - ACALSim 面向 HPC/加速器设计空间探索，把组件模拟器组织为并行事件任务：可插拔线程管理分配 worker，事件时间可 fast-forward，进程间共享内存零拷贝传输状态，两阶段协议保证并行运行仍确定；以 HPCSim/A100 模型验证速度和扩展性。
  - 相较单线程 cycle simulation 或为速度牺牲可复现性的并行模拟，核心创新是把局部事件并行、跨组件同步和确定性提交分层，使同一框架可替换细节模型并扩到大系统。
  - parallel discrete-event simulation、HPC design space、deterministic execution、zero-copy shared memory

- [Analyzing Symbolic Properties for DRL Agents in Systems and Networking](https://doi.org/10.1145/3805627)
  - Mohammad Zangooei (University of Waterloo); Jannis Weil, Amr Rizk (Leibniz University Hannover); Mina Tahmasbi Arashloo, Raouf Boutaba (University of Waterloo)
  - 论文把系统/网络 DRL 策略在连续输入区间上的单调性、鲁棒性等要求编码为多次相关执行之间的符号约束，再调用 DNN verifier 搜索反例或证明性质，而不是枚举单点；对象是已训练策略的离线验证。
  - 相较只在测试 trace 上报告平均 reward，核心创新是用 relational symbolic reasoning 验证输入区域内策略行为，能暴露稀有但系统性错误；这里的 DRL agent 是传统强化学习控制器，不属于 LLM Agent。
  - DRL verification、symbolic properties、systems policies、non-LLM agent

- [Are We Ready to Enable Satellite Autonomy Through on Board Image Registration?](https://doi.org/10.1145/3805628)
  - Claudio Di Salvo (Politecnico di Milano); Emanuele Del Sozzo (MIT); Giuseppe Sorrentino (Politecnico di Milano); Eleonora D'Arnese (University of Edinburgh); Paolo Panicucci, Davide Conficconi (Politecnico di Milano)
  - STAR-Bench 在多种商用星载计算平台上测量卫星影像 registration 的精度、时延和能耗，ETNA 则依据图像质量与当前算力/能源状态，动态编排 CPU、GPU、FPGA 等不同配准流水线；QAC 用可量化质量信号决定是否在轨继续处理。
  - 相较用地面 GPU 的离线准确率判断能否上星，核心创新是把影像质量、设备能耗和实时 deadline 做成端到端 benchmark 与运行时选择器，直接回答 autonomy 在受限星载硬件上何时可行。
  - satellite autonomy、image registration、heterogeneous onboard computing、quality-aware orchestration

- [Assessing Resilience in Authoritative DNS Infrastructure Supporting Government Services](https://doi.org/10.1145/3805629)
  - Agung Septiadi, Minzhao Lyu, Hassan Habibi Gharakheili, Vijay Sivaraman (University of New South Wales)
  - 论文为政府服务的权威 DNS 构建跨 registry、主动查询、BGP/ASN 和地理位置的统一 schema，从名称服务器放置、配置依赖、查询调度与故障域四层评估韧性，并对六个国家形成可比较评分。
  - 相较只数 NS 数量或是否启用 anycast，核心创新是把看似多副本但共享运营商、网络或地域的隐性共因故障还原出来，形成多层依赖驱动的政府 DNS 韧性审计。
  - authoritative DNS、government services、infrastructure resilience、dependency analysis

- [Can Multipath TCP Congestion Control do better without adhering to its First Design Principle?](https://doi.org/10.1145/3805630)
  - Xuan Wang (The University of Texas at Arlington); Hao Che (Department of Computer Science and Engineering, The University of Texas at Arlington); Zhijun Wang (University of Texas at Arlington); Hong Jiang (UT Arlington)
  - 论文重新检查 MPTCP ‘不得伤害单路径 TCP’的第一设计原则，证明与资源汇聚、拥塞均衡等其他原则共同约束时会压低多路径吞吐；放松该原则后把耦合拥塞控制写成网络效用最大化，并提出 N-MPTCP 求取更高全局效用。
  - 相较在既定三原则下调耦合参数，核心创新是指出原则本身存在结构性性能上限，并以可优化的效用目标替代绝对不劣于单路径的逐流约束。
  - Multipath TCP、congestion control、network utility maximization、design principles

- [CAP: Detecting Network Device Misconfigurations with Context-Aware Prompting of LLMs](https://doi.org/10.1145/3805631)
  - Xi Jiang (University of Chicago); Aaron Gember-Jacobson (Colgate University); Nick Feamster (University of Chicago)
  - CAP 诊断网络设备配置时，先检索同设备邻近段、拓扑相关段和历史相似配置，再让 LLM 通过结构化对话按需请求缺失上下文，最后输出错误位置、原因和修复解释；上下文选择随当前候选和设备关系迭代，而非一次塞入整份配置。
  - 相较静态 prompt 或仅做语义相似检索，核心创新是让模型主动拉取与当前判断相关的配置上下文，并保留可解释诊断链；它是 LLM for Systems，而非能自主执行和验证修复的 Agent System。
  - LLM for Systems、network misconfiguration、context-aware prompting、iterative retrieval

- [cPMEM: A Design of Byte-Addressable Persistent Memory with Compute Express Link for Data Center Applications](https://doi.org/10.1145/3805632)
  - Gaocong Liu, Mengting Lu, Kun Wang, Feng Zhu (Alibaba Cloud); Shu Li (Alibaba Group)
  - cPMEM 实现一套可字节寻址的 CXL persistent memory，从介质/控制器 ASIC、固件到主机软件共同处理写放大、耐久、retention 和故障恢复，并以数据库/内存型应用评估访问延迟和持久语义。
  - 相较把现成持久介质简单挂到 CXL 总线，核心创新是围绕 CXL 访问粒度和数据中心可靠性做完整芯片—控制器—软件协同，而非只给接口仿真。
  - CXL memory、persistent memory、byte addressability、hardware-software co-design

- [cuPTW: Leveraging Idle Compute Units for Massively Parallel GPU Page Table Walks](https://doi.org/10.1145/3805633)
  - Zihang Chen (The Hong Kong University of Science and Technology (Guangzhou)); Tianao Ge (Hong Kong University of Science and Technology (Guangzhou)); Lieven Eeckhout (Ghent University); Hongyuan Liu (Stevens Institute of Technology); Jiayi Huang (HKUST(GZ))
  - cuPTW 在 GPU 出现 TLB miss 时，不完全依赖固定-function page-table walker，而把部分空闲 compute unit 调度为批量 page walk kernel，用 LDS 缓存页表节点并以 SIMD 合并同层访问；运行时按 CU 空闲度和 miss 队列决定是否卸载。
  - 相较仅增加 TLB/PTW 硬件或让单线程软件 walk，核心创新是把暂时闲置的通用 GPU 算力转成可扩展地址翻译资源，并通过局部缓存与向量化同时提高并行度和 locality。
  - GPU virtual memory、page-table walk、idle compute units、SIMD translation

- [d-HNSW: A High-performance Vector Search Engine on Disaggregated Memory](https://doi.org/10.1145/3805634)
  - Fei Fang, Yi Liu, Chen Qian (University of California Santa Cruz)
  - d-HNSW 面向 RDMA 解耦内存中的向量搜索，在计算端保留聚类代表构成的小索引，按查询先定位相关簇；远端把同簇节点连续布局，随后 query-aware 地批量抓取并流水重叠 RDMA 与距离计算，减少 HNSW 随机细粒度读。
  - 相较把单机 HNSW 指针遍历原样搬到远端内存，核心创新是以聚类重组索引布局和访问粒度，使算法路径适配 RDMA 的高启动开销，同时不把完整索引复制回计算节点。
  - vector search、disaggregated memory、RDMA、HNSW

- [ECCentric: An Empirical Analysis of Quantum Error Correction Codes](https://doi.org/10.1145/3805635)
  - Aleksandra Świerkowska, Jannik Pflieger, Emmanouil Giortamis, Pramod Bhatotia (Technical University of Munich (TUM))
  - ECCentric 以量子纠错码、逻辑/物理拓扑、噪声模型、decoder 和 compiler 组合为实验矩阵，统一测量逻辑错误率、qubit 开销、延迟与编译可行性，比较不同 QEC 选择在真实硬件约束下何时互换优劣。
  - 相较只在单一 depolarizing noise 下比较 code distance，核心创新是提供跨 code—topology—noise—toolchain 的全栈实证基准，暴露局部最优纠错码无法直接决定系统最优。
  - quantum error correction、full-stack benchmarking、noise models、decoder-compiler co-design

- [Efficiency-Reward Trade-Off in Queues with Dynamic Arrivals](https://doi.org/10.1145/3820171.3806908)
  - Tianze Qu (University of Michigan, Ann Arbor); Sushil Mahavir Varma (University of Michigan Ann Arbor)
  - 论文研究到达率 λ(q) 随队长状态变化且接纳请求可获奖励 F 的队列，求稳定策略下平均 backlog 与 reward 接近最优值的 Pareto 前沿；根据 λ 和 F 在最优点附近的形状，延迟代价分别呈 1/ε、1/√ε 或 log(1/ε) 等标度。
  - 相较给所有 admission-control 问题同一个 O(1/ε) 漂移界，核心创新是用局部曲率区分三类效率—奖励相变并证明紧界；该条为 PER 归档摘要。
  - state-dependent queues、reward-delay tradeoff、heavy-traffic scaling、PER archival summary

- [EviDex: Provenance-Weighted Evidence-Path Indexing for Fresh and Auditable Retrieval under Continuous Updates](https://doi.org/10.1145/3805636)
  - Rui Li, Shuang Cao, Ruihua Liu, Alexandre Duprey (Hill Research)
  - EviDex 为持续更新语料中的问答/RAG 建立带来源和权重的 evidence-path 索引，把追加日志按意图 bucket 增量压实；查询时用可证明安全的上界剪枝，精确返回 top-B 证据链，同时保留每段证据的版本与 provenance 供审计。
  - 相较只按向量相似度取孤立 chunk 或定期全量重建索引，核心创新是把跨文档证据路径、新鲜度和可追溯性作为索引原语，并在连续更新下仍保证 top-B 正确性；属于 agent-adjacent retrieval infra，未形成 Agent 循环。
  - RAG infrastructure、evidence-path indexing、continuous updates、provenance auditing

- [Geographical Centralization Resilience in Ethereum's Block-Building Paradigms](https://doi.org/10.1145/3805637)
  - Sen Yang (Yale University, IC3); Burak Öz (Flashbots); Fei Wu (King's College London); Fan Zhang (Yale University, IC3)
  - 论文形式化 Ethereum validator 在本地与外部 block builder 之间选择时的收益、网络位置和延迟激励，再用 mean-field 分析与 agent-based simulation 推演 validator/builder 地域分布，评估不同协议参数遭遇区域中断或中心化冲击后的恢复能力。
  - 相较仅从历史 IP 快照描述地理集中，核心创新是把 block-building 机制改变参与者选址收益的反馈纳入模型，可测试协议设计如何内生地放大或缓解集中风险；其中 agent 是经济仿真主体，非 LLM Agent。
  - Ethereum、geographic centralization、block building、mean-field simulation

- [HealthServe: A Public Health-Aware Inference Framework](https://doi.org/10.1145/3805638)
  - Sicheng Zhou, Rohan Basu Roy (University of Utah)
  - HealthServe 在跨地域 GPU 集群路由 LLM 推理请求时，同时输入各地队列/副本、网络与延迟 SLO、电网碳强度以及 PM2.5 等污染物对应的健康损害成本；分层优化用预计算的可行配置库快速选择站点和资源，使总公共健康外部成本下降。
  - 相较只按电价或 CO₂ 调度，核心创新是把电力生产造成的地区人口暴露和污染健康损害纳入逐请求 inference placement，并用索引化候选库把多目标模型落到在线时限内。
  - LLM inference routing、public-health externality、geo-distributed GPU、SLO-aware sustainability

- [Horizon: Understanding and Predicting Global Starlink Performance](https://doi.org/10.1145/3805639)
  - Cristian Benghe, Vlad Graure, Tanya Shreedhar, Nitinder Mohan (TU Delft)
  - Horizon 融合 M-Lab、Cloudflare 等 11 个月、90 个国家的地面观测，以及天气、卫星轨道和地面站可见性，学习不同地点/时间的 Starlink 吞吐与时延；模型既解释天气和轨道覆盖影响，也预测未充分测量地区的性能。
  - 相较用单站历史或静态覆盖图估计 LEO 网络，核心创新是把全球异构测速与物理环境特征对齐，形成可跨地区泛化的时空预测而非只做事后描述。
  - Starlink performance、global prediction、multi-source measurement、spatio-temporal modeling

- [Information Design for Prosocial Behavior](https://doi.org/10.1145/3805640)
  - Alexandre Reiffers (IMT Atlantique); Rajesh Sundaresan (Indian Institute of Science)
  - 论文把居民根据电力反馈信号决定节能程度建成 mean-field game，设计平台应披露的总体、邻里或个体信息，使自利用户的均衡接近社会节能目标；分析表明更精细信息有时诱发搭便车，较粗信号反而提高总节约并改善隐私。
  - 相较默认更多实时反馈一定更有效，核心创新是把信息粒度本身作为机制设计变量，刻画隐私、策略响应与公共利益之间的非单调关系。
  - information design、prosocial behavior、mean-field game、energy feedback

- [Learning to Allocate Reusable Resources under Stochastic Rewards and Durations](https://doi.org/10.1145/3805641)
  - Ativ Joshi, Qingsong Liu (University of Massachusetts Amherst); Mohammad Hajiesmaili (UMass Amherst)
  - 论文研究请求部分到达、资源使用时长和收益分布未知的可复用资源分配，在线策略根据历史样本估计每类请求的单位占用价值，并以 profitability threshold 决定接受；理论先给已知分布的 1/2 prophet 保证，再证明非参数学习时的遗憾界。
  - 相较只学习即时 reward 或假定占用时长已知，核心创新是同时从 censored 的已接受样本学习收益和释放时间，并把统计误差嵌入阈值分配的容量保证。
  - reusable resource allocation、unknown rewards and durations、prophet inequality、nonparametric learning

- [LPGSim: A Lightweight Parallel GPU Simulator Maximizing Speed with Trustworthy Simulation](https://doi.org/10.1145/3805642)
  - Hyunwoo Nam, Jay Hwan Lee, Yeonsoo Kim, Mengzhao Zhang (Yonsei University); Jeonggeun Kim (Kyungpook National University); Bernd Burgstaller (Yonsei University)
  - LPGSim 把 GPU 模拟拆成 trace 级与必要 cycle 级组件，删除只用于维护微架构元数据但不影响依赖的事件，并合并重复计算；各子系统用本地时钟在 NUMA 上并行，通过受控同步保持关键 pipeline/内存依赖，可按研究问题选择速度—精度档位。
  - 相较全细节 cycle-accurate 模拟器只能缩小 workload，核心创新是系统识别哪些状态可安全省略并让组件异步推进，在保留性能排序可信度的同时扩展到更长 GPU 程序。
  - GPU simulation、trace-cycle hybrid、parallel simulation、accuracy-speed tradeoff

- [MATER: Mutually Aware Framework for Teleoperated-robot with Extended Reality](https://doi.org/10.1145/3805643)
  - Ziliang Zhang, Cong Liu (University of California, Riverside); Hyoseung Kim (UC Riverside)
  - MATER 面向 XR 遥操作机器人，把操作者端和机器人端都建成可预测对方状态的镜像：网络延迟或丢包时，各端用自适应时间窗与插值重建对方动作，真实状态到达后再回滚/协调，减少视觉反馈与机械执行不一致。
  - 相较只在显示端做 dead reckoning 或只给控制链加缓冲，核心创新是双端 mutual awareness 与迟到状态修正，使感知和动作在不对称网络条件下共同保持一致。
  - XR teleoperation、robotics networking、state reconstruction、latency compensation

- [Minos: Systematically Classifying Performance and Power Characteristics of GPU Workloads on HPC Clusters](https://doi.org/10.1145/3805644)
  - Rutwik Jain, Yiwei Jiang (University of Wisconsin Madison); Matthew D. Sinclair (University of Wisconsin–Madison); Shivaram Venkataraman (University of Wisconsin-Madison)
  - Minos 先用少量 profiling run 提取 GPU workload 的算力、带宽、功率和频率敏感特征，把作业归入可迁移的性能—能耗类别；调度器据此预测换 GPU/频率后的完成时间与能耗，并为 HPC 集群选择设备或 power cap。
  - 相较逐作业穷举所有 GPU 与频率，核心创新是用低成本特征分类复用跨 workload 的 scaling 规律，让异构 GPU 放置和 DVFS 可以在小样本下联合决策。
  - GPU workload classification、HPC scheduling、power capping、performance-energy prediction

- [Optimizing Dropout in LLM Training: Performance Comparison of Fusion and Overlap](https://doi.org/10.1145/3805645)
  - Haiyue Ma (Princeton University); Jian Liu, Ronny Krashinsky (NVIDIA)
  - 论文优化 LLM 训练中的 dropout：分析发现把 dropout 完全 fuse 进 FlashAttention 会因随机数状态、寄存器和访存资源冲突而受限，于是改为在前一 GEMM 执行时并行生成 mask/RNG，随后让 attention 直接消费；解析模型按形状选择 fusion 或 overlap。
  - 相较默认 kernel fusion 总能省内存流量，核心创新是揭示 RNG 这一隐藏资源使融合反而变慢，并把 dropout 从 attention 关键路径前移，以跨 kernel overlap 取代盲目融合。
  - LLM training、dropout、FlashAttention、kernel overlap

- [PEMI: Transparent Performance Enhancements for QUIC](https://doi.org/10.1145/3805646)
  - Jie Zhang (Tsinghua University); Lei Zhang (Zhongguancun Laboratory); Ziyi Wang (Beijing University of Posts and Telecommunications); Chenxiang Sun (Tsinghua University); Yuming Hu (University of Minnesota -- Twin Cities); Xiaohui Xie, Zeqi Lai, Yong Cui (Tsinghua University)
  - PEMI 作为无需修改 QUIC 端点的路径中间盒，从加密流量可见的 packet number、ACK 时序与丢包模式估计 RTT/CWND 状态，在检测丢包时更快转发/触发重传提示，并延迟会误导拥塞控制的反馈，以减少恢复空窗。
  - 相较必须升级客户端/服务器的 QUIC 优化或试图解密 payload，核心创新是只用加密后仍公开的传输元数据推断控制状态，并透明干预 ACK/时序而保持协议端点兼容。
  - QUIC、transparent middlebox、encrypted transport、loss recovery

- [Performance Analysis of the Randomized SIEVE/CLOCK cache replacement algorithm](https://doi.org/10.1145/3805647)
  - Yirong Wang, Peter Desnoyers (Northeastern University); Benny Van Houdt (University of Antwerp)
  - 论文分析 SIEVE/CLOCK 的随机化版本：每个对象保留多个独立访问 bit，扫描淘汰时随机选择/清除，以均衡近似 LRU 的收益与常数状态；mean-field 模型证明稳态 fixed point 唯一，并预测长扫描和命中率。
  - 相较只靠 trace 仿真比较 cache policy，核心创新是给带多 bit 随机状态的时钟式淘汰建立可解的平均场动力学，从算法参数直接推导稳态性能。
  - cache replacement、SIEVE/CLOCK、mean-field analysis、randomized access bits

- [RELL-STC: An Efficient SpMM Extension of Sparse Tensor Core with Re-structured ELLPACK and Gustavson Dataflow](https://doi.org/10.1145/3805648)
  - Jianfeng Cui (National University of Defense Technology); Bo Yuan (College of Computer Science, National University of Defense Technology); Zekun Jiang (National University of Defense Technology); Sheng Liu (National University of Defense Technology,China); Kai Lu (National University of Defense Techonology)
  - RELL-STC 面向非结构化稀疏矩阵乘稠密矩阵，把行重排为适合 Tensor Core tile 的 ELLPACK 布局，并在扩展的 sparse Tensor Core 上采用 Gustavson 数据流累积非零乘积，减少 padding、索引和不规则访存。
  - 相较现有 Tensor Core SpMM 依赖固定 2:4 结构或因 ELL padding 浪费算力，核心创新是协同重构稀疏布局和硬件数据流，让高度非规则稀疏矩阵也能形成高利用率矩阵 tile。
  - sparse matrix multiplication、Tensor Core、ELLPACK、Gustavson dataflow

- [SemanticDFL: Similarity-Aware Pull-based Personalized Decentralized Federated Learning](https://doi.org/10.1145/3805649)
  - Javad Dogani (IMDEA Networks Institute); Mostafa Khastkhodaei, Farshad Khunjush (Shiraz University); Nikolaos Laoutaris (IMDEA Networks Institute)
  - SemanticDFL 在个性化去中心化联邦学习中不向所有邻居 push 模型，而为每个节点构造模型/数据语义签名，通过分层 overlay、top-P 候选和 super-peer 聚类发现相似节点，再 pull top-K 模型聚合；状态随本地训练动态更新。
  - 相较按物理邻接或随机 gossip 混合模型，核心创新是让通信拓扑由任务语义相似性驱动，并用分层索引避免全网两两比较，从而减少负迁移和带宽。
  - decentralized federated learning、personalization、similarity-aware model pull、semantic overlay

- [The Price of Interoperability: Exploring Cross-Chain Bridges and Their Economic Consequences](https://doi.org/10.1145/3805650)
  - Yiyue Cao, Mingzhe Zheng (The Hong Kong University of Science and Technology (Guangzhou)); Lin William Cong (Nanyang Technological University); Siguang Li, Xuechao Wang (The Hong Kong University of Science and Technology (Guangzhou))
  - 论文重建 2022–2025 年 20 条链、16 个桥的跨链流量超图，区分协议宣称可连接的 structural interoperability 与实际资金活跃连接，计算手续费、延迟、资本回报和流动性集中，并分析扩张如何同时提高可达性与脆弱性。
  - 相较按桥 TVL 排名，核心创新是用链—桥—资产超边刻画真实经济路径，把互操作覆盖、用户成本、收益和系统性依赖放到同一实证框架。
  - cross-chain bridges、interoperability、economic measurement、hypergraph analysis

- [The Price of Strategic Information: Degree-Based Bounds on Inefficiency in Distributed Learning Games](https://doi.org/10.1145/3805651)
  - Tuan Ngoc Do, Hai Duc Nguyen, Khanh Quoc Nguyen, Hiep Quang Dao, Anh Duc-Duy Nguyen, Luong Cong Nguyen (Phenikaa University, Hanoi, Vietnam)
  - 论文研究网络中节点可策略性隐瞒或传递私有信息的分布式学习博弈，用双边转移支付刻画分享激励，并证明 Nash/粗相关均衡的效率损失可由最大网络度控制，进一步分析哪些拓扑改善社会学习。
  - 相较假定通信者诚实共享观测，核心创新是把信息外部性与网络结构共同放入均衡分析，得到仅依赖局部 degree 的可解释 inefficiency bound。
  - information sharing game、distributed learning、price of anarchy、network topology

- [UniCache: Unifying Prefix Cache Eviction for Heterogeneous LLM Serving Workloads](https://doi.org/10.1145/3805652)
  - Bei Ouyang (Rice University); Yifan Qiao (UC Berkeley); Jiarong Xing (Rice University)
  - UniCache 以 vLLM trace 模拟器复现 chat session 的历史前缀复用和跨任务模板/结构复用，在线识别 cache block 属于哪类共享模式，再依据未来复用、重算代价、块大小和 GPU 容量统一分配及淘汰，适配请求分布变化。
  - 相较 LRU 只看最近访问或为 session/template 分设缓存，核心创新是把异构复用关系映射到统一价值尺度，让同一 KV pool 在多类 LLM 工作负载间动态竞争。
  - LLM prefix cache、heterogeneous workloads、KV eviction、session and structural reuse

- [Wasserstein-p Central Limit Theorem Rates: From Local Dependence to Markov Chains](https://doi.org/10.1145/3820171.3806885)
  - Yixuan Zhang, Qiaomin Xie (University of Wisconsin-Madison)
  - 论文在 Wasserstein-p 距离下给出中心极限定理收敛率，从局部依赖随机变量推广到具有依赖结构的 Markov chain，并用耦合/矩界控制 p 阶运输距离，得到与独立情形同阶或可比较的最优速率。
  - 相较只在 Kolmogorov/Wasserstein-1 距离或独立样本下给界，核心创新是统一处理高阶 Wasserstein 距离和链式依赖，并证明速率的紧性；该条为 PER 归档摘要。
  - central limit theorem、Wasserstein-p、Markov chains、PER archival summary

- [WISP: Waste- and Interference-Suppressed Distributed Speculative LLM Serving at the Edge via Dynamic Drafting and SLO-Aware Batching](https://doi.org/10.1145/3805653)
  - Xiangchen Li, Jiakun Fan (Virginia Tech); Qingyuan Wang (University College Dublin); Dimitrios Spatharakis (National Technical University of Athens); Saeid Ghafouri (Queen's University Belfast); Hans Vandierendonck (Queens University Belfast); Deepu John (University College Dublin); Bo Ji, Ali R. Butt, Dimitrios Nikolopoulos (Virginia Tech)
  - WISP 面向边缘小模型 draft、云端大模型 verify 的 speculative serving，监测各请求 draft 接受率、边云 RTT、GPU batch 和 SLO 余量，动态决定每轮生成多少候选 token；估时器预测验证开销，batch scheduler 隔离会互相拖慢的请求，减少无效 drafting 与验证干扰。
  - 相较固定 speculation length、仅最大化单请求接受率，核心创新是联合控制边缘动作与云端批处理，把网络延迟、错误候选浪费和跨请求 interference 纳入同一 SLO 决策。
  - distributed speculative decoding、edge-cloud LLM serving、dynamic drafting、SLO-aware batching
