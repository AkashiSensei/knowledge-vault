# SIGCOMM 2026 论文列表

## 范围与核验

[2026 官方 accepted papers](https://conferences.sigcomm.org/sigcomm/2026/accepted/)。SIGCOMM 2026 accepted 页页眉写有 110 篇，但逐项只有 109 个唯一题名；最终 program 中恰有 109 篇论文属于 ACM 主 proceedings 父 DOI `10.1145/3789240.*`，并全部通过 Crossref 标题核验，因此本列表采用 109。program 另列 `10.1145/3806097.3806099` 与 `10.1145/3787927.3787929` 两个不同父 proceedings 的条目，明确排除，不能用它们补足页眉数字。

本地保留 17 份 DOI 对应的合法 arXiv 预印本，位于 `reference/SIGCOMM/2026/`；全部通过 `%PDF-` 文件头、PDF 解析、页数和首页文本检查。其余论文严格依据官方 program 摘要预读，不因 ACM 下载受限而臆造正文细节。

方向统计互斥：每篇只按核心研究对象进入一个主方向，合计严格等于年度论文总数。

## 互斥主方向统计

| 主方向 | 论文数 | 占比 |
|---|---:|---:|
| AI 集群网络与大模型系统 | 21 | 19.3% |
| 数据中心网络、传输与互连 | 13 | 11.9% |
| 可编程数据平面与云网络 | 23 | 21.1% |
| 网络测量、诊断与可观测性 | 11 | 10.1% |
| 网络验证、管理与安全 | 13 | 11.9% |
| 互联网架构、路由与流量控制 | 9 | 8.3% |
| 无线、蜂窝与感知 | 11 | 10.1% |
| 卫星、海洋与非地面网络 | 4 | 3.7% |
| 视频、实时通信与 QoE | 3 | 2.8% |
| 分布式系统与网络服务 | 1 | 0.9% |

## 热门问题与方法

- 主方向前三位为 可编程数据平面与云网络 23 篇、AI 集群网络与大模型系统 21 篇、数据中心网络、传输与互连 13 篇。与 2025 相比，AI 集群网络进一步扩展到 KV I/O、scale-up fabric、in-network collective、训练集群调度和 100K+ GPU 通信栈。
- 形式化与可解释网络管理明显增多：运行时 BGP 检查、分布式网内程序验证、verification-aware 语言、局部 subspecification、弹性防火墙规范和全球 WAN 收敛验证形成完整链条。
- 生产经验论文的粒度更细，从单一协议优化走向跨层协同：DPU/host、prefill/decode/storage、模型并行/网络、视频语义/码率、RAN 配置/模型漂移和光互连重配置都被联合建模。

## Agent 四分类

| 分类 | 论文数 | 论文与判定依据 |
|---|---:|---|
| Agent System | 0 | 无 |
| Agent Infra | 1 | DualPath: Accelerating Agentic LLM Inference by Harvesting Disaggregated KV-Cache Storage I/O：核心贡献是承载多轮 agentic workload 的 KV-cache I/O 与调度数据路径，而非修改 Agent 规划。 |
| Agent for Systems | 3 | Elastispec: Formalizing Enterprise Firewall Management with Informal and Elastic Specifications：多步一致性保持 LLM Agent 把厂商文档形式化，并与配置审计和人工反馈相连。；Networked Agent Memory and Causality Representation: Experiences towards Interpretable Cloud-Scale Root-Causing：XiHe 让证据驱动 Agent 分解诊断、共享网络化记忆并合成可核验因果图。；RepLLM: Toward Automatically Reproducing Network Research Results：四个专门 Agent 通过共享记忆执行解析、架构设计、代码生成、审计与修复闭环。 |
| LLM for Systems | 2 | Evolution of AliYANG: Model-driven and LLM-assisted Network Configuration Management：LLM 用于模型补全与翻译代码生成，生产工作流仍由模型驱动基础设施控制。；AIDA: Accelerating Root Cause Analysis for Multi-Vendor Device Failures with LLM-Powered Reasoning：AIDA 用知识图谱引导多步 LLM 推理生成可解释 RCA，但不自主操作并回验网络。 |

四类只统计以 LLM/生成式 Agent 为核心对象或方法的论文；传统 RL/MARL、神经网络流量预测、一般 AI 网络优化，以及仅出现 software agent/agentless 等字样的工作均不计入。

## 2025–2026 变化

- AI 集群网络与大模型系统从 14/88 增至 21/109，研究对象从训练 fabric/MoE/长上下文和少量 KV 传输，扩展为 serving、KV-cache 存储 I/O、collective synthesis、in-network aggregation、scale-up/photonic fabric 与多租户训练调度。
- 网络验证、管理与安全从 7/88 增至 13/109，并从 WAN/DCN 验证和加密流量检测，推进到运行时协议检查、verification-aware 编程语言、自然语言规范形式化及生产配置/证书系统。
- Agent 相关由 2025 的 2 篇增至 2026 的 6 篇：新增 agentic serving 基础设施、共享记忆/因果诊断、多 Agent 系统复现和规范形式化；但两年 Agent System 均为 0，说明 SIGCOMM 的 Agent 重点仍是网络基础设施与网络运维，而非通用规划算法。

## 论文条目

- [KVServe: Service-Aware KV Cache Compression for Communication-Efficient Disaggregated LLM Serving](https://dl.acm.org/doi/10.1145/3789240.3829139)
  - Zedong Liu, Xinyang Ma, Dejun Luo (University of Chinese Academy of Sciences), Hairui Zhao (Institute of Computing Technology, Chinese Academy of Sciences), Bing Lu (Institute of Computing Technology Chinese Academy of Sciences), Wenjing Huang (University of Chinese Academy of Sciences), Yida Gu, Xingchen Liu, Zheng Wei (Institute of Computing Technology, Chinese Academy of Sciences), Jinyang Liu (University of California, Riverside), Dingwen Tao, Guangming Tan (Institute of Computing Technology, Chinese Academy of Sciences)
  - LLM 在生产中被广泛采用，将推理系统推向极限；解耦式 LLM 服务（例如 PD 分离和 KV 状态分解）提高了可扩展性和成本效率，但它也将 KV 变成了跨越网络和存储边界的显式有效负载，使 KV 成为主要的端到端瓶颈；尽管生产服务上下文在工作负载组合、带宽和 SLO/质量预算方面随时间变化，但现有的 KV 压缩通常在运行时静态配置。KVServe 是第一个用于解耦式 LLM 服务的服务感知和自适应 KV 通信压缩框架：KVServe (1) 通过新组件和跨方法重组将 KV 压缩统一到模块化策略空间中； (2) 引入贝叶斯分析引擎，可有效搜索该空间并提取 3D Pareto 候选集，减少 50 倍离线搜索开销； (3) 部署一个服务感知在线控制器，该控制器将分析延迟模型与轻量级 bandit 相结合，以在约束下选择配置文件并纠正离线到在线的不匹配；KVServe 集成到 vLLM 中并跨数据集、模型、GPU 和网络进行评估，在 PD 分离服务中实现高达 9.13 倍的 JCT 加速，在 KV 解耦服务中实现高达 32.8 倍的 TTFT 减少。
  - 相较现有的 KV 压缩通常在运行时静态配置，核心创新是KVServe 是第一个用于解耦式 LLM 服务的服务感知和自适应 KV 通信压缩框架：KVServe (1) 通过新组件和跨方法重组将 KV 压缩统一到模块化策略空间中。
  - AI 集群网络与大模型系统、LLM Systems、KV Cache、Network Measurement/Telemetry、Caching/CDN、Compression/Encoding

- [DualPath: Accelerating Agentic LLM Inference by Harvesting Disaggregated KV-Cache Storage I/O](https://dl.acm.org/doi/10.1145/3789240.3829159)
  - Yongtong Wu (Peking University, DeepSeek-AI), Shaoyuan Chen (Tsinghua University, DeepSeek-AI), Rilin Huang (Peking University), Yixuan Tan (DeepSeek-AI), Yinmin Zhong (Peking University, DeepSeek-AI), Mingxing Zhang (Tsinghua University), Xin Jin (Peking University), Panpan Huang (DeepSeek-AI)
  - DualPath 面向多轮 Agentic LLM 推理：外部存储读取的大量 KV cache 使 prefill 侧存储 NIC 饱和，而 decode 侧 NIC 空闲。系统增加 storage→decode→prefill 的第二条路径，先把 KV 读入 decode engine，再经计算网络 RDMA 转给 prefill，并由全局调度器按两类 engine 的实时负载分配读取；生产式 workload 上离线吞吐最高提高 1.87 倍，在线吞吐平均提高 1.96 倍且不违反 SLO。
  - 相较所有 KV 都经 storage→prefill 单路径加载，核心创新是同时利用 decode 侧闲置存储带宽和计算网络，并以全局调度避免与延迟敏感模型通信相互干扰。
  - AI 集群网络与大模型系统、Agent Infra、LLM Systems、KV Cache、RDMA、Caching/CDN

- [Efficient Remote KV Cache Reuse with GPU-native Video Codec](https://dl.acm.org/doi/10.1145/3789240.3829120)
  - Liang Mi (Nanjing University and Institute for AI Industry Research (AIR), Tsinghua University), Weijun Wang (Institute for AI Industry Research (AIR), Tsinghua University), Jinghan Chen (Nanjing University), Ting Cao (Institute for AI Industry Research (AIR), Tsinghua University), Haipeng Dai (Nanjing University), Yunxin Liu (Institute for AI Industry Research (AIR), Tsinghua University)
  - 远程 KV 缓存重用从远程存储中获取相同上下文的 KV 缓存，避免重新计算，加速 LLM 推理；虽然它在高速网络中表现出色，但在带宽有限的情况下其性能会显著下降；最近的研究通过以压缩形式传输 KV 缓存来解决这个问题，但相关的重量级解压缩抵消了 KV 重用的好处。该工作设计一种高效且可广泛部署的远程 KV 缓存重用解决方案，该解决方案利用 GPU 原生视频编解码器；其系统 KVCodec 通过两种技术实现有效的 KV 缓存编码；编解码器友好的张量布局以高度紧凑的视频格式压缩 KV 缓存，从而实现快速传输；实验表明，与 SOTA 方法相比，它在保持无损精度的同时将 TTFT 降低了高达 3.51 倍。
  - 相较最近的研究通过以压缩形式传输 KV 缓存来解决这个问题，但相关的重量级解压缩抵消了 KV 重用的好处，核心创新是该工作设计一种高效且可广泛部署的远程 KV 缓存重用解决方案，该解决方案利用 GPU 原生视频编解码器；其系统 KVCodec 通过两种技术实现有效的 KV 缓存编码；编解码器友好的张量布局以高度紧凑的视频格式压缩 KV 缓存，从而实现快速传输。
  - AI 集群网络与大模型系统、LLM Systems、KV Cache、Video/QoE、Caching/CDN、Compression/Encoding

- [Connex: Endpoint Mobility Primitives for Dynamic LLM Serving](https://dl.acm.org/doi/10.1145/3789240.3829200)
  - Yanying Lin (University of Chinese Academy of Sciences, Penn), Vincent Liu, Tao Luo (University of Pennsylvania), ChengZhong Xu (University of Macau), Kejiang Ye (Shenzhen Institutes of Advanced Technology, Chinese Academy of Sciences)
  - 现代 LLM 服务系统越来越多地采用弹性推理管道，其中阶段频繁地加入、离开和跨节点迁移；然而，现有的 GPU 通信框架（例如 NCCL）采用静态拓扑，导致在 worker 转换期间出现路由故障和 P99 延迟峰值，违反了亚毫秒级尾部延迟要求；Connex 是一种通信系统，可将端点移动性从异常故障提升为一流的原语。Connex 不是单独优化各个机制，而是定义了一个移动合约，每当 worker 在 token 流、激活或 KV 传输正在进行时加入、离开或迁移时，通信层都会强制执行该合约；该合约通过三种协作机制实现：(1) 基于纪元的路由，在没有全局协调的情况下限制过时性；(2) 显式切换协议，保留流排序并在迁移过程中提供一次性交付；(3) 基于信用的背压，具有流量类隔离，可防止成员变动引起的对延迟关键路径的干扰；对合成和生产衍生的成员变动下的 5 节点 GPU 集群进行的评估表明，与基于 NCCL 的基线相比，Connex 将 P99 尾部尖峰减少了高达 85%，实现了亚秒级切换，并在基线下降到 0-28% 的中等负载下保持了 100% 的有效吞吐。
  - 相较现有的 GPU 通信框架（例如 NCCL）采用静态拓扑，导致在 worker 转换期间出现路由故障和 P99 延迟峰值，违反了亚毫秒级尾部延迟要求，核心创新是Connex 是一种通信系统，可将端点移动性从异常故障提升为一流的原语；Connex 不是单独优化各个机制，而是定义了一个移动合约，每当 worker 在 token 流、激活或 KV 传输正在进行时加入、离开或迁移时，通信层都会强制执行该合约。
  - AI 集群网络与大模型系统、LLM Systems、KV Cache、Internet Routing、LLM Inference & Serving

- [TurboBus: Pooling PCIe Bandwidth for LLM Workloads via Scale-Up Fabrics](https://dl.acm.org/doi/10.1145/3789240.3829130)
  - Xinyu Yang, Kaiqiang Xu, Kai Chen (Hong Kong University of Science and Technology)
  - GPU 内存卸载广泛应用于 LLM 工作负载，但将瓶颈转移到 GPU-CPU 传输，这可能占用高达 90% 的端到端推理/训练时间；矛盾的是，超过 60% 的 PCIe 带宽仍然闲置；根本原因是 PCIe 链路单独存在瓶颈，但整体利用率不足。TurboBus 是通过新兴的纵向扩展结构在同一地点的作业之间汇集 PCIe 带宽；TurboBus 使任何 GPU 都能从相邻 GPU（甚至属于其他作业的 GPU）借用空闲 PCIe 链路，同时通过特权守护程序保持隔离；作为 TurboBus 的核心，它通过具有有限内存开销的中继 GPU 传输数据，通过细粒度 PCIe 分配保持所有链路繁忙，利用 PCIe/NVLink 带宽不对称实现双向传输，并通过大小感知调度平衡公平性和完成时间；系统实现并评估了 TurboBus，实验表明，它可以将按需模型加载的第一个令牌延迟减少高达 40%（在分析最佳值的 5% 以内），为 KV 缓存卸载推理实现高达 1.6 倍的吞吐量，并将训练速度提高高达 7%，同时对共置工作负载施加不到 1% 的开销。
  - 相较根本原因是 PCIe 链路单独存在瓶颈，但整体利用率不足，核心创新是TurboBus 是通过新兴的纵向扩展结构在同一地点的作业之间汇集 PCIe 带宽；TurboBus 使任何 GPU 都能从相邻 GPU（甚至属于其他作业的 GPU）借用空闲 PCIe 链路，同时通过特权守护程序保持隔离。
  - AI 集群网络与大模型系统、LLM Systems、KV Cache、Collective Communication、Failure Diagnosis、Caching/CDN

- [Towards Efficient Verification of Distributed In-Network Computing Programs](https://dl.acm.org/doi/10.1145/3789240.3829122)
  - Mingyuan Song, Huan Shen, Jinghui Jiang, Qiang Su, Ziheng Zhang, Qingyu Song (Xiamen University), Yuchao Zhang (Beijing University of Posts and Telecommunications), Wanjian Feng (Yealink), Fei Yuan (Xiamen University), Yitao Xing, Wenjia Wei (Huawei Technologies Co., Ltd.), Qiao Xiang, Jiwu Shu (Xiamen University)
  - 分布式网络内程序因其性能优势而越来越多地部署在数据中心，但将应用程序逻辑转移到交换机也扩大了故障范围；因此，在部署之前确保其正确性对于可靠性至关重要；虽然现有的验证框架可以有效地验证在单个交换机上运行的程序，但它们忽略了分布式设置中常见的交互行为，从而遗漏了可能导致系统故障的相关错误。该工作设计 Procurator，这是一个验证框架，可以有效地捕获分布式网络内程序中的交互行为；Procurator 将每个 P4 管道建模为反应参与者，并将它们的交互统一为消息传递，以捕获事件驱动范例下的交互行为；评估表明，Procurator 在 12 个现实世界的分布式网络系统中发现了 28 个不同的错误，并且比最先进的框架实现了高达 9.1 倍的加速。
  - 相较现有的验证框架可以有效地验证在单个交换机上运行的程序，但它们忽略了分布式设置中常见的交互行为，从而遗漏了可能导致系统故障的相关错误，核心创新是该工作设计 Procurator，这是一个验证框架，可以有效地捕获分布式网络内程序中的交互行为；Procurator 将每个 P4 管道建模为反应参与者，并将它们的交互统一为消息传递，以捕获事件驱动范例下的交互行为。
  - 网络验证、管理与安全、Programmable Network Hardware、Formal Verification、Scheduling/Orchestration、Network Verification & Formal Methods

- [When static verification is not enough: revealing BGP bugs at runtime](https://dl.acm.org/doi/10.1145/3789240.3829137)
  - Pietro Ronchetti, Tibor Schneider, Laurent Vanbever (ETH Zurich)
  - 运营商竭尽全力确保其 BGP 网络正确；然而，尽管他们付出了努力，但由于软件或硬件错误而导致的故障仍然会发生，这通常会在整个网络范围内产生有害的后果；如今，操作员所能做的就是对此类故障做出反应，但往往已经为时已晚。该工作设计 GhostBuster，这是一个运行时系统，用于监视 BGP 路由器的执行并验证其是否符合协议规范；具体来说，GhostBuster 检查观察到的传出 BGP 消息是否可能是由传入消息生成的；这样做的关键挑战是 BGP 路由器不一定按顺序处理传入消息，这迫使人们考虑输入消息的所有可能的重新排序；研究团队对模拟网络的评估进一步证实了 GhostBuster 具有可扩展性和准确性：它在检测超过 60% 的错误时从未误报错误。
  - 相较如今，操作员所能做的就是对此类故障做出反应，但往往已经为时已晚，核心创新是该工作设计 GhostBuster，这是一个运行时系统，用于监视 BGP 路由器的执行并验证其是否符合协议规范；具体来说，GhostBuster 检查观察到的传出 BGP 消息是否可能是由传入消息生成的。
  - 网络验证、管理与安全、Network Measurement/Telemetry、Formal Verification、Internet Routing、Network Verification & Formal Methods

- [Explainable Network Verification via Localized Subspecification](https://dl.acm.org/doi/10.1145/3789240.3829155)
  - Yongzheng Zhang, Yaxuan Lin, Haoxian Chen, Ruize Ma (Shanghai Tech University), Amirmohammad Nazari, Mukund Raghothaman (University of Southern California), Peng Zhang (Xi'an Jiaotong University)
  - 网络验证、综合和修复工具有助于实施高级操作意图，但其有限的可解释性使得配置维护在实践中成本高昂，因为操作员仍然必须手动推理大型低级配置。该工作设计局部子规范，它解释了各个配置元素如何通过限制其可接受的行为来保留给定的网络属性；一项针对 15 名专业网络运营商和 8 名研究生的用户研究表明，准确率提高了 52%，时间节省了 23%，70% 的参与者表示他们希望在日常运营中使用子规范，这展示了实际的好处；为了支持实际部署，该工作设计 SpecLens，这是一种可解释的网络验证系统，它使用具有健全性保证的可扩展算法生成本地化子规范。
  - 相较网络验证、综合和修复工具有助于实施高级操作意图，但其有限的可解释性使得配置维护在实践中成本高昂，因为操作员仍然必须手动推理大型低级配置，核心创新是该工作设计局部子规范，它解释了各个配置元素如何通过限制其可接受的行为来保留给定的网络属性；一项针对 15 名专业网络运营商和 8 名研究生的用户研究表明，准确率提高了 52%，时间节省了 23%，70% 的参与者表示他们希望在日常运营中使用子规范。
  - 网络验证、管理与安全、Formal Verification、Network Verification & Formal Methods

- [VeriLucid: A Verification-aware Data-plane Programming Language](https://dl.acm.org/doi/10.1145/3789240.3829171)
  - John Sonchack, Pamela Zave, Jennifer Rexford (Princeton University)
  - 数据平面程序运行在连接数百万用户的关键基础设施上，正确性非常重要；验证可以帮助程序员构建正确的软件，但当前的数据平面工具只能检查简单的属性或需要程序员付出巨大的努力。作为解决方案，该工作设计第一个验证感知数据平面语言：VeriLucid；核心思想是用一种高级语言统一编程和规范，并具有内置的证明自动化；集成使程序员可以自然地在整个开发过程中连续使用验证，就像单元测试一样，但有强有力的保证；在评估中，研究团队表明，与具有相当表达能力的其他验证工具相比，就代码行数而言，VeriLucid 所需的程序员工作量减少了 10 倍。
  - 相较验证可以帮助程序员构建正确的软件，但当前的数据平面工具只能检查简单的属性或需要程序员付出巨大的努力，核心创新是作为解决方案，该工作设计第一个验证感知数据平面语言：VeriLucid；核心思想是用一种高级语言统一编程和规范，并具有内置的证明自动化；集成使程序员可以自然地在整个开发过程中连续使用验证，就像单元测试一样，但有强有力的保证。
  - 网络验证、管理与安全、Formal Verification、Network Verification & Formal Methods

- [Elastispec: Formalizing Enterprise Firewall Management with Informal and Elastic Specifications](https://dl.acm.org/doi/10.1145/3789240.3829191)
  - Chenan Wen, Yizhan Qing, Curt P Jansen, Xiaokang Qiu, Sanjay G Rao (Purdue University)
  - Elastispec 面向企业管理员从数千页自然语言厂商文档提取防火墙策略的工作：多步一致性保持 LLM Agent 先把可选项写入定制 DSL，再关联可能不完整的企业资产数据，将抽象规范落到具体环境；交互式 auditor 随后逐条比对真实配置，生成 compliance tree、差异和待人工确认的推断。真实配置与主流应用文档实验能发现放行非合规流量的错误。
  - 相较人工抄写规则或把完整规范视为已知，核心创新是显式容纳非正式、不完整且随环境变化的规范，并用 LLM 形式化、数据关联和人机审计三级约束控制幻觉风险。
  - 网络验证、管理与安全、Agent for Systems、LLM Systems、Formal Verification、Network Verification & Formal Methods

- [Trivance: Latency-Optimal AllReduce by Shortcutting Multiport Networks](https://dl.acm.org/doi/10.1145/3789240.3829181)
  - Anton Juerss (Weizenbaum Institut Berlin), Vamsi Addanki (Purdue University), Stefan Schmid (Technische Universität Berlin)
  - AllReduce 是分布式计算中基本的集体通信操作，也是大规模训练和推理的关键性能瓶颈；其完成时间取决于通信步骤的数量（主导延迟敏感的工作负载）以及影响延迟和带宽限制状态的通信距离。Trivance 是一种新颖的 AllReduce 算法，可在 log3 nsteps 内完成，与 Swing 和递归加倍相比，改进了 50%，同时与 Bruck 算法相比，拥塞减少了三倍，并保持了带宽最优性；Trivance 在每个步骤中利用双向环的两个传输端口，同时将两个方向上的通信距离增加了三倍；在整个评估过程中，Trivance 仍然是性能最佳的延迟优化算法。
  - 相较AllReduce 是分布式计算中基本的集体通信操作，也是大规模训练和推理的关键性能瓶颈，核心创新是Trivance 是一种新颖的 AllReduce 算法，可在 log3 nsteps 内完成，与 Swing 和递归加倍相比，改进了 50%，同时与 Bruck 算法相比，拥塞减少了三倍，并保持了带宽最优性。
  - AI 集群网络与大模型系统、Collective Communication、Collective Communication Algorithms

- [OptCCL: Scalable Synthesis of Optimal Collective Communication Algorithms](https://dl.acm.org/doi/10.1145/3789240.3829207)
  - Richard Shapley, Rachit Agarwal, David Shmoys (Cornell University)
  - OptCCL 是一种合成 collective communication 算法的技术，该算法对于给定的主机和网络硬件和拓扑来说是最佳的。OptCCL 是通用的：它能够为所有现有 collective、所有现有硬件、甚至共享主机和网络资源的多个并发集合综合最佳算法；然而，OptCCL 具有可扩展性：它可以在数十分钟内为数百个 GPU 合成最佳算法。
  - 官方摘要未展开更细的直接基线；可核验的核心创新是OptCCL 是一种合成 collective communication 算法的技术，该算法对于给定的主机和网络硬件和拓扑来说是最佳的。
  - AI 集群网络与大模型系统、Collective Communication、Collective Communication Algorithms

- [DynamiQ: Accelerating Gradient Synchronization using Compressed Multi-hop All-reduce](https://dl.acm.org/doi/10.1145/3789240.3829148)
  - Wenchen Han (University College London), Shay Vargaftik (Broadcom), Michael Mitzenmacher (Harvard University), Ran Ben Basat (University College London and Broadcom)
  - 多跳全归约是大型模型训练事实上的支柱；随着训练规模的增加，网络往往成为瓶颈，导致传输数据量的减少；然而，这些系统并未针对多跳聚合进行优化，其中条目沿着其聚合拓扑多次部分求和。DynamiQ 是一个量化框架，它弥补了量化最佳实践和多跳聚合之间的差距；DynamiQ 引入了新技术来更好地表示部分和，并与解压缩-累加-再压缩融合内核共同设计，以促进快速执行；此外，DynamiQ 是唯一能够持续达到接近基线精度（例如 BF16 基线的 99.9%）的评估方法，并且在显著加速训练的同时实现这一点。
  - 相较这些系统并未针对多跳聚合进行优化，其中条目沿着其聚合拓扑多次部分求和，核心创新是DynamiQ 是一个量化框架，它弥补了量化最佳实践和多跳聚合之间的差距；DynamiQ 引入了新技术来更好地表示部分和，并与解压缩-累加-再压缩融合内核共同设计，以促进快速执行。
  - AI 集群网络与大模型系统、Collective Communication、Compression/Encoding、Collective Communication Algorithms

- [ZipCCL: Efficient Lossless Data Compression of Communication Collectives for Accelerating LLM Training](https://dl.acm.org/doi/10.1145/3789240.3829204)
  - Wenxiang Lin (Harbin Institute of Technology, Shenzhen), Xinglin Pan, Ruibo FAN (Data Science and Analytics Thrust, HKUST(GZ)), Shaohuai Shi (Harbin Institute of Technology, Shenzhen), Xiaowen Chu (Data Science and Analytics Thrust, HKUST(GZ))
  - 通信已成为大型语言模型（LLM）分布式训练的关键瓶颈；虽然已经提出了许多方法来减少通信开销，但无损压缩的潜力在很大程度上仍未得到充分开发，因为压缩和解压缩通常消耗比减少通信流量的好处更大的开销。因此，ZipCCL 是一个用于 LLM 训练的无损压缩集体通信库；ZipCCL 配备了其新技术：(1) 理论上的指数编码，利用 LLM 张量的高斯分布来加速压缩，而无需昂贵的在线统计数据；(2) GPU 优化的压缩和解压缩内核，使用通信感知数据布局仔细设计内存访问模式和管道；(3) 自适应通信策略，根据工作负载模式和系统特征动态切换集体操作；使用专家混合模型和密集 Transformer 模型在 64-GPU 集群上进行评估，ZipCCL 将通信时间缩短了高达 1.35 倍，并实现了高达 1.18 倍的端到端训练加速，并且对模型质量没有任何影响。
  - 相较通信已成为大型语言模型（LLM）分布式训练的关键瓶颈，核心创新是因此，ZipCCL 是一个用于 LLM 训练的无损压缩集体通信库；ZipCCL 配备了其新技术：(1) 理论上的指数编码，利用 LLM 张量的高斯分布来加速压缩，而无需昂贵的在线统计数据。
  - AI 集群网络与大模型系统、LLM Systems、MoE、Collective Communication、Network Measurement/Telemetry、Compression/Encoding

- [Theseus: Runtime-Adaptive GPU Collective Communication with Hot-Swappable Schedules](https://dl.acm.org/doi/10.1145/3789240.3829134)
  - Rui Ding (National Key Laboratory for Multimedia Information Processing, School of Computer Science, Peking University), Xiandong Lu (Hangzhou Institute for Advanced Study, University of Chinese Academy of Sciences), Jiajun Wang (Yuanpei College, Peking University), Xunpeng Liu (National Key Laboratory for Multimedia Information Processing, School of Computer Science, Peking University), Feiyang Wang, Xuran Hao, Houyuan Zhu, Anyi Xu (School of Electronics Engineering and Computer Science, Peking University), Sinuo Cao (National Key Laboratory for Multimedia Information Processing, School of Computer Science, Peking University), Haifeng Sun (National University of Singapore), Qun Huang (National Key Laboratory for Multimedia Information Processing, School of Computer Science, Peking University), Jiamin Cao, Jiaqi Gao (Alibaba Cloud)
  - 当前的 GPU 集体通信库 (CCL) 采用针对稳定环境进行优化的预定义调度；它们支持的调度和选择逻辑在通信器初始化时是固定的，这无法考虑不断变化的运行时条件，例如工作负载特征和硬件健康状态。为了解决这个问题，Theseus 是一种新颖的 CCL 后端，它提供了调度级别的运行时自适应性；它允许用户定义的时间表和选择策略；随着运行时条件的变化，Theseus 使用超越 CCL 内部指标的集群范围运行时属性来选择合适的调度；此外，它能够以较低的开销跨 GPU 一致地从之前的计划进行热交换；它将端到端作业完成时间提高了 1.84 倍，同时产生的开销相当或更低。
  - 相较它们支持的调度和选择逻辑在通信器初始化时是固定的，这无法考虑不断变化的运行时条件，例如工作负载特征和硬件健康状态，核心创新是Theseus 是一种新颖的 CCL 后端，它提供了调度级别的运行时自适应性；它允许用户定义的时间表和选择策略；随着运行时条件的变化，Theseus 使用超越 CCL 内部指标的集群范围运行时属性来选择合适的调度。
  - AI 集群网络与大模型系统、Collective Communication、Scheduling/Orchestration、Collective Communication Algorithms

- [CausalTune: Causal Learning based Automated Cellular RAN Configuration Tuning Framework](https://dl.acm.org/doi/10.1145/3789240.3829109)
  - Leyang Xue, Bolun Zhang, Yibo Ma, Mahesh Marina (University of Edinburgh), He Yan, Yu Zhou, Cheuk Yiu Ip, Senthil Dhandapani, James Klosowski (AT&T)
  - 蜂窝无线接入网络 (RAN) 中的持续配置调整对于维持性能、可靠性、能源效率和用户体验至关重要；然而，这项任务在实践中仍然主要是手动的；现有的 RAN 配置调整方法在应对这些挑战方面效果有限。CausalTune 是一种新颖的因果学习框架，用于基于观测遥测的自动 RAN 配置优化；CausalTune 将配置效应与环境和操作混杂因素分开，推广到稀疏且以前未见过的参数设置，并捕获高影响力的多参数交互；其主要见解是，操作 RAN 中的有效因果推理需要重塑原始遥测数据，以揭示混杂和学习环境不变的机制；在这一见解的指导下，CausalTune 采用了多级管道，集成了分布式表示学习、因果建模和交互感知推荐；这些发现证明了因果学习在实现可靠、可扩展和可解释的 RAN 配置调整方面的潜力。
  - 相较现有的 RAN 配置调整方法在应对这些挑战方面效果有限，核心创新是CausalTune 是一种新颖的因果学习框架，用于基于观测遥测的自动 RAN 配置优化；CausalTune 将配置效应与环境和操作混杂因素分开，推广到稀疏且以前未见过的参数设置，并捕获高影响力的多参数交互。
  - 无线、蜂窝与感知、Network Measurement/Telemetry、Cellular/RAN、Cellular & RAN Systems

- [SAGE: A Real-Time AI System for Reducing Latency in NextG Cellular Networks](https://dl.acm.org/doi/10.1145/3789240.3829112)
  - Aoyu Gong, Raphael Cannatà, Arman Maghsoudnia, Néstor Lomba Lomba (EPFL), Dan Mihai Dumitriu (Pavonis LLC), Haitham Hassanieh (EPFL)
  - AR/VR、工业自动化、云游戏和自主机器人等 NextG 应用越来越需要更低的延迟；然而，当前的 5G 网络由于基于请求的调度而导致严重延迟，用户必须在基站为上行链路传输分配资源之前发出需求信号。该工作设计 Sage，这是一种实时人工智能系统，可以以毫秒为单位预测每个用户的上行链路需求，并主动分配资源以减少上行链路延迟；Sage 提出了交通列车：一种新颖的抽象概念，可以减轻观测到的到达基站的交通流量的扭曲，并产生稳定的预测目标；Sage 从用户流量中提取统计特征，并从专用人工智能预测器的流量感知数据库中检索适当的模型；Sage 进一步执行低延迟推理、错误跟踪和在线持续学习，以动态调整预测模型；广泛的评估表明，Sage 以亚毫秒级的推理开销实现了毫秒级的预测精度，在不同应用程序中平均将上行链路延迟减少了 2.53 倍，同时保持了较高的资源效率。
  - 相较之前发出需求信号，核心创新是该工作设计 Sage，这是一种实时人工智能系统，可以以毫秒为单位预测每个用户的上行链路需求，并主动分配资源以减少上行链路延迟；Sage 提出了交通列车：一种新颖的抽象概念，可以减轻观测到的到达基站的交通流量的扭曲，并产生稳定的预测目标。
  - 无线、蜂窝与感知、Network Measurement/Telemetry、Cellular/RAN、Scheduling/Orchestration、Cellular & RAN Systems

- [RANPilot: Making AI Functionalities Robust to Dynamic O-RAN Reconfigurations](https://dl.acm.org/doi/10.1145/3789240.3829146)
  - Shiming Yu, Leming Shen, Jianing Zhang, Xin Li, Xianjin Xia, Yuanqing Zheng (The Hong Kong Polytechnic University), Yaxiong Xie (University at Buffalo SUNY)
  - 开放无线接入网络 (O-RAN) 通过其可重新配置的架构和人工智能驱动的控制提供了前所未有的灵活性；然而，这种敏捷性暴露了一个严重的脆弱性：在一种网络配置上训练的人工智能模型在升级后由于剧烈的数据漂移而遭受显著的性能下降；RANPilot 是第一个通过主动人工智能适应来应对这一挑战的框架。RANPilot 构建了一个轻量级的“虚拟 O-RAN”（跟踪驱动的模拟器）来合成表示物理变化发生之前的重新配置后状态的高保真训练数据，从而允许 AI 模型提前适应；通过将人工智能演进范式从被动式重新开发转变为主动式准备，RANPilot 探索了一种数字引导方法，以在可重新配置的 O-RAN 部署中实现强大的人工智能。
  - 相较这种敏捷性暴露了一个严重的脆弱性：在一种网络配置上训练的人工智能模型在升级后由于剧烈的数据漂移而遭受显著的性能下降，核心创新是RANPilot 是第一个通过主动人工智能适应来应对这一挑战的框架；RANPilot 构建了一个轻量级的“虚拟 O-RAN”（跟踪驱动的模拟器）来合成表示物理变化发生之前的重新配置后状态的高保真训练数据，从而允许 AI 模型提前适应。
  - 无线、蜂窝与感知、Cellular/RAN、Cellular & RAN Systems

- [Synchronizing with the Scheduler: Dual-Loop Congestion Control for 5G Uplink on Commodity Devices](https://dl.acm.org/doi/10.1145/3789240.3829199)
  - Qiang Wu, Yuxin Liu, Tianyang Zhang (University at Buffalo SUNY), Haoran Wan, Kyle Jamieson (Princeton University), Yaxiong Xie (University at Buffalo SUNY)
  - 当前的端到端拥塞控制反馈太慢，无法跟踪蜂窝网络中快速的无线动态。研究团队将授权缓冲比 (GBR)（基站上行链路授权与移动设备报告的需求之比）确定为上行链路资源稀缺的毫秒级 RAN 信号；对 AT&T、Verizon 和 T-Mobile LTE/5G FDD/TDD 部署的测量表明，GBR 跟踪基站上行链路负载，并比端到端反馈更早地揭示拥塞情况；由于 GBR 源自强制 BSR 授权交换，因此它不需要更改基站并在其本地时间尺度捕获调度程序决策；在商用蜂窝网络上的实验表明，GBR-CC 比 GCC 平均吞吐量提高了 50%，同时中位播放延迟降低了 32%~53%，卡顿率降低了 60%；与 BBR 相比，平均吞吐量提高了 5%，中位 RTT 降低了一半。
  - 相较当前的端到端拥塞控制反馈太慢，无法跟踪蜂窝网络中快速的无线动态，核心创新是研究团队将授权缓冲比 (GBR)（基站上行链路授权与移动设备报告的需求之比）确定为上行链路资源稀缺的毫秒级 RAN 信号；对 AT&T、Verizon 和 T-Mobile LTE/5G FDD/TDD 部署的测量表明。
  - 无线、蜂窝与感知、Congestion Control、Network Measurement/Telemetry、Cellular/RAN、Wireless/Sensing、Scheduling/Orchestration

- [Unveiling Low-Altitude 5G Performance: Linking Key Influencing Factors with UAV Flight Parameters](https://dl.acm.org/doi/10.1145/3789240.3829198)
  - Xinzhe Liu (Pengcheng Laboratory, Shenzhen, China, and South China University of Technology, Guangzhou, China), Jianer Zhou, Xiaoyong Ni, Ke Luo (Pengcheng Laboratory, Shenzhen, China), Zhenyu Li (Institute of Computing Technology, Chinese Academy of Sciences (ICT, CAS), Beijing, China), Xiaofeng Tao (Beijing University of Posts and Telecommunications, Beijing, China, and Pengcheng Laboratory, Shenzhen, China), Weichao Li (Pengcheng Laboratory, Shenzhen, China)
  - 尽管 5G 被广泛认为是无人机蜂窝通信的关键技术，但其在低空场景中的实际性能仍知之甚少。为了解决这个问题，研究团队通过商业 5G 网络进行大规模飞行测量，并构建跨层数据集来比较低空和地面之间的通信性能；通过联合分析 5G 配置、链路层参数和端到端指标，研究确定了显著影响低空性能的四个关键因素：空间层、调制阶数、切换和资源块分配；这些发现为提高蜂窝连接无人机的可靠性提供了经验证据和见解。
  - 相较尽管 5G 被广泛认为是无人机蜂窝通信的关键技术，但其在低空场景中的实际性能仍知之甚少，核心创新是研究团队通过商业 5G 网络进行大规模飞行测量，并构建跨层数据集来比较低空和地面之间的通信性能；通过联合分析 5G 配置、链路层参数和端到端指标，研究确定了显著影响低空性能的四个关键因素：空间层、调制阶数、切换和资源块分配。
  - 无线、蜂窝与感知、Network Measurement/Telemetry、Cellular/RAN、Scheduling/Orchestration、Cellular & RAN Systems

- [Turbo: Efficiently Serving Long-Context Large Language Models with In-Network Aggregation](https://dl.acm.org/doi/10.1145/3789240.3829140)
  - Ying Wan (Southeast University), Yuchen Xu (Peking University), Chuwen Zhang (Tsinghua Unigroup), Yingsheng Huang (Southeast University), Yong Feng, Wenquan Xu (Tsinghua University), Jialin Li (National University of Singapore), Mingwei Xu (Tsinghua University), Wenfei Wu (Peking University), Congcong Miao (National University of Singapore)
  - 由于 KV 缓存的线性增长，支持长上下文的 LLM 面临着严重的内存瓶颈；将存储分布在多个 GPU 上可以减轻这种负担，但会带来大量的通信开销或流量 incast，尤其是在解码阶段。Turbo 是一种首个网络内聚合系统，它通过将查询广播和注意力聚合卸载到交换机来加速长上下文推理；NS-3 上的大规模模拟表明，Turbo 在推理延迟和网络流量减少方面均显著优于最先进的基线，且精度损失可以忽略不计。
  - 相较将存储分布在多个 GPU 上可以减轻这种负担，但会带来大量的通信开销或流量 incast，尤其是在解码阶段，核心创新是Turbo 是一种首个网络内聚合系统，它通过将查询广播和注意力聚合卸载到交换机来加速长上下文推理。
  - AI 集群网络与大模型系统、LLM Systems、KV Cache、Caching/CDN、In-Network Aggregation for ML

- [HyNA: Taming Tail Latency in MoE Training with Hybrid Switch Silicon](https://dl.acm.org/doi/10.1145/3789240.3829178)
  - Yang Liu, Tianxiang Liu, Haipeng Yao (Beijing University of Posts and Telecommunications)
  - 向万亿参数模型的过渡，特别是专家混合模型（MoE），将分布式训练的瓶颈从计算转移到通信；然而，现有的参数服务器 (PS) 架构会受到组播拥塞的影响，而 ATP 等最先进的网内聚合 (INA) 解决方案无法处理 MoE 工作负载的稀疏、突发流量；这些解决方案由于依赖缓慢的、基于主机的冲突和溢出回退而遭受严重的尾部延迟放大。为了拆除这堵通信墙，HyNA 是一种完全无服务器的聚合系统，它通过利用新颖的硬件-软件共同设计的交换机架构来消除专用的参数服务器节点；HyNA 将线速可重配置匹配表 (RMT) 与嵌入式 RISC-V 内核结合在一起；通过遵循严格的片上闭合原则，系统完全在交换机 ASIC 内处理所有流量异常（包括哈希冲突和浮点方差），将不可预测的网络 RTT 转换为确定性的片上延迟；至关重要的是，在 MoE 梯度同步阶段，与动态 INA 基线相比，该系统消除了回退损失，并将同步时间缩短了 1.6 倍，且不影响位级模型精度。
  - 相较现有的参数服务器 (PS) 架构会受到组播拥塞的影响，而 ATP 等最先进的网内聚合 (INA) 解决方案无法处理 MoE 工作负载的稀疏、突发流量，核心创新是为了拆除这堵通信墙，HyNA 是一种完全无服务器的聚合系统，它通过利用新颖的硬件-软件共同设计的交换机架构来消除专用的参数服务器节点；HyNA 将线速可重配置匹配表 (RMT) 与嵌入式 RISC-V 内核结合在一起。
  - AI 集群网络与大模型系统、MoE、Collective Communication、Programmable Network Hardware、Failure Diagnosis、Cloud/Distributed Systems

- [EPIC: Abstraction and Polymorphism of In-Network Collectives on Ethernet](https://dl.acm.org/doi/10.1145/3789240.3829196)
  - Yitao Yuan, Jianglong Nie, Tianyu Bai, Ruizhe Zhou, Siyuan Cao, Xujie Fan, Yuchen Xu, Junkai Chen, Chenqi Zhao, Nengyuan Zhang, Shaoke Fang (Peking University), Jiangyuan Chen (University of Science and Technology of China), Yuanfeng Chen (National University of Defense Technology), Jiaqi Sun (Peking University), Zhan Wang (Institute of Computing Technology, Chinese Academy of Sciences), Xiaohua Xu (University of Science and Technology of China), Yuchao Zhang, Yang Liu (Beijing University of Posts and Telecommunications), Xiangrui Yang (National University of Defense Technology), Jing Lin, Xiaohe Hu (Infrawaves), Yang Li, Chao Jiang, Limin Xiao, Weifeng Zhang (Lenovo Research), Junjie Wang, Wei Cheng (Beijing Centec Communications Co., Ltd.), Yazhu Lan, Jianbo Dong, Binzhang Fu (Alibaba Cloud), Wenfei Wu (Peking University)
  - 网络内集体（INC）加速在优化人工智能训练和推理方面具有巨大潜力；然而，其跨层性质历来阻碍了开放以太网生态系统的投资和采用。为了弥补这一差距，EPIC 是（以太网多态网内集体），这是一种基于“统一抽象、多态实现”原则构建的 INC 协议规范和参考系统；EPIC 引入了与标准以太网兼容的抽象，将功能边界与参与者角色保持一致，同时提供针对不同硬件功能量身定制的多态实现；研究团队解决了三个基本挑战：首先，研究团队采用模块化设计，实现从简单到复杂实现的演进路径，允许供应商逐步迭代其硬件；其次，研究团队应用形式验证方法来证明所有提出的多态模式的正确性；研究团队进行了大量的实验——模型检查、数据包/流仿真、VM 仿真、Tofino/NP 测试台和 FPGA/RTL 验证——以验证 EPIC 的正确性、性能增益和可行性。
  - 相较网络内集体（INC）加速在优化人工智能训练和推理方面具有巨大潜力；然而，其跨层性质历来阻碍了开放以太网生态系统的投资和采用，核心创新是EPIC 是（以太网多态网内集体），这是一种基于“统一抽象、多态实现”原则构建的 INC 协议规范和参考系统；EPIC 引入了与标准以太网兼容的抽象，将功能边界与参与者角色保持一致，同时提供针对不同硬件功能量身定制的多态实现。
  - AI 集群网络与大模型系统、Collective Communication、Programmable Network Hardware、Formal Verification、In-Network Aggregation for ML

- [PReCCL: Performant and Resilient Collective Communication via Integrated Inband Telemetry and Workload Reallocation](https://dl.acm.org/doi/10.1145/3789240.3829133)
  - Zhiyong Chen (Tsinghua University), Kaihui Gao, Li Chen (Zhongguancun Laboratory), Rui Yan, Zihan Yan (Tsinghua University), Fei Gui (Zhongguancun Laboratory), Dan Li (Tsinghua University), Jiamin Cao, Jiaqi Gao (Alibaba Cloud)
  - 现代集体通信库 (CCL) 通过将集体通信任务 (CCT) 分解为多个子任务来执行集体通信任务 (CCT)，每个子任务映射到特定的虚拟拓扑 (VT)，这是 GPU 的有序图（例如环或树），以最大限度地提高并行性和链接利用率；随着 AI 训练扩展到更大的集群，网络异常（拥塞和故障）是不可避免的，单个落后的 VT 可能会延迟整个 CCT。PReCCL 是一种直接的 NCCL 替代品，它将软件带内遥测与跨 VT 工作负载重新分配相结合；与依赖于硬件的遥测（例如 P4-INT）不同，PReCCL 在 CCL 内实现带内监控；它精确测量每个 VT 的停顿计数，并搭载现有集体流量的遥测元数据；凭借这种细粒度的可见性，PReCCL 采用动态跨 VT 重新分配机制，将工作负载从落后的 VT（遭受拥塞或故障）转移到健康的 VT；在测试床上，PReCCL 将 CCT 完成度提高了 2.1 倍，将端到端训练提高了 1.21 倍，并且开销低于调整后的消息大小阈值。
  - 相较现有的解决方案要么依赖于低层传输层解决方案，缺乏跨子任务的视角，要么依赖于静态的 CCL 调度，无法适应动态和异构网络，核心创新是PReCCL 是一种直接的 NCCL 替代品，它将软件带内遥测与跨 VT 工作负载重新分配相结合；与依赖于硬件的遥测（例如 P4-INT）不同，PReCCL 在 CCL 内实现带内监控。
  - AI 集群网络与大模型系统、Collective Communication、Programmable Network Hardware、Network Measurement/Telemetry、Failure Diagnosis、Scheduling/Orchestration

- [UBEP: Re-architecting Expert Parallelism Communication Library for Production Superpods](https://dl.acm.org/doi/10.1145/3789240.3829183)
  - Yipeng Liu, Chang Liu, Si Shen, Jiaqi Zheng (Nanjing University), Mingfan Li (Huawei Technologies Co., Ltd.), Yuyang Yang, Guanhua Li, Yuquan Zhang, Yimeng Xu (Nanjing University), Zhongzhe Hu, Zhiyuan Huang, Qihang Duan, Junsong Wang, Wenkai Ling, Baochuan Yang, Xianzhi Yu, Han Bao, Yijie Chen (Huawei Technologies Co., Ltd.), Guihai Chen (Nanjing University)
  - 在生产高带宽超级节点（例如 NVIDIA 的 NVL72/576 和华为的 CloudMatrix384）上部署专家混合 (MoE) 模型带来了超出原始互连带宽的严峻挑战。为了消除这些瓶颈，UBEP 是（统一总线专家并行），这是一个生产就绪的通信库，它重新考虑了 MoE 的现代超级 Pod 架构的 All-to-All 原语；通过大规模实验，UBEP 将 All-to-All 延迟降低高达 52.4%，将每个输出令牌的 MoE 推理时间 (TPOT) 降低高达 11.1%。
  - 相较为了消除这些瓶颈，UBEP 是（统一总线专家并行），这是一个生产就绪的通信库，它重新考虑了 MoE 的现代超级 Pod 架构的 All-to-All 原语，核心创新是通过大规模实验，UBEP 将 All-to-All 延迟降低高达 52.4%，将每个输出令牌的 MoE 推理时间 (TPOT) 降低高达 11.1%。
  - AI 集群网络与大模型系统、MoE、Collective Communication、Scheduling/Orchestration、In-Network Aggregation for ML

- [Dorado: Scaling SmartNIC Session Tables on Commodity DDRs](https://dl.acm.org/doi/10.1145/3789240.3829121)
  - Heng Yu (Zhongguancun Laboratory), Kai Ren, Jiajun Liang, Baozeng Zhang (Tencent), Guozhi Lin (Zhongguancun Laboratory), Xinyi Zhang (CNIC CAS), Jian Wang, Jian Zhao (Tencent), Ziyue Zhai (Zhongguancun Laboratory), Liang Wang, Chao Pei (Tencent), Jilong Wang (Tsinghua University), Gaogang Xie (CNIC CAS), Ang Chen (University of Michigan), Congcong Miao (National University of Singapore)
  - 基于 FPGA 的 SmartNIC 被广泛部署用于云网络功能加速，但由于会话表过大，其内存子系统面临越来越大的压力；传统观点认为，高数据包处理性能依赖于先进的存储器（例如 SRAM、HBM），但在云规模上添加这些存储器的成本很高。Dorado 是一种新颖的设计，可以完全在廉价的 DDR 模块上扩展 SmartNIC 会话表；其生产结果表明，Dorado 可以容纳多达 16M 会话条目，将内存成本降低 80%，同时实现 50Mpps 线速处理。
  - 相较传统观点认为，高数据包处理性能依赖于先进的存储器（例如 SRAM、HBM），但在云规模上添加这些存储器的成本很高，核心创新是Dorado 是一种新颖的设计，可以完全在廉价的 DDR 模块上扩展 SmartNIC 会话表。
  - 可编程数据平面与云网络、SmartNIC/DPU、Programmable Network Hardware、Scheduling/Orchestration、Cloud Networking: DPUs, SmartNICs & Gateways

- [XFir: Accelerating New-Flow Setup on Host Servers of a Large Cloud Network](https://dl.acm.org/doi/10.1145/3789240.3829131)
  - Shihan Lin (University of Michigan), Shunqiao Jiang, Liang Wang, Jian Wang, Chao Pei, Jian Zhao, Wenjun Wu, Kai Ren (Tencent), Lijun Zhuang, Qingmin Liu (JaguarMicro, Shenzhen), Heng Yu (Tsinghua University), Sirui Li (Tencent), Yibo Huang (University of Michigan), Yifei Zhu (Shanghai Jiao Tong University), Yunming Xiao (The Chinese University of Hong Kong, Shenzhen), Ang Chen (University of Michigan), Linghe Kong (Shanghai Jiao Tong University), Congcong Miao (National University of Singapore)
  - 在当今的云网络中，主机服务器广泛部署数据处理单元（DPU）作为“Sep-Path”范式下的网络加速器；然而，随着服务器功能随着 CPU 内核和网络带宽的增加而扩展，软件慢速路径（在 DPU 的 CPU 上执行）已成为高新流速率工作负载的关键瓶颈。为了解决这一差距，XFir 是第一个用于云主机服务器的硬件加速新流程设置系统，可提供高 CPS 吞吐量，同时保留足够的灵活性；XFir 利用配备云网络协处理器 (CNP) 的下一代 DPU 来执行主机服务器的新流程设置逻辑；总体而言，XFir 提高了新流程吞吐量，同时以较低的财务成本保持了开发灵活性。
  - 相较随着服务器功能随着 CPU 内核和网络带宽的增加而扩展，软件慢速路径（在 DPU 的 CPU 上执行）已成为高新流速率工作负载的关键瓶颈，核心创新是XFir 是第一个用于云主机服务器的硬件加速新流程设置系统，可提供高 CPS 吞吐量，同时保留足够的灵活性；XFir 利用配备云网络协处理器 (CNP) 的下一代 DPU 来执行主机服务器的新流程设置逻辑。
  - 可编程数据平面与云网络、SmartNIC/DPU、Cloud Networking: DPUs, SmartNICs & Gateways

- [FlowTurbo: From Best-Effort to Hit-Driven MegaFlow Hardware Offloading in Open vSwitch](https://dl.acm.org/doi/10.1145/3789240.3829138)
  - Zhongxian Liang (Harbin Institute of Technology), Sheng Lan (Peking University Shenzhen Graduate School), Ying Li (Southern University of Science and Technology), Zihan Li (Harbin Institute of Technology), Wenjun Li (Pengcheng Laboratory), Yao Xin (Guangzhou University), Han Wang (Pengcheng Laboratory), Tong Yang (Peking University), Yu Zhang (Harbin Institute of Technology), Gaogang Xie (Chinese Academy of Sciences), Bin Liu (Tsinghua University), Weizhe Zhang (Harbin Institute of Technology)
  - 将 Open vSwitch 中的快速路径 MegaFlow 卸载到硬件加速器是在现代云数据中心加速数据包转发的常用方法；然而，由于当前硬件加速器的能力有限，现有解决方案仍然依赖于粗粒度、尽力卸载，这难以应对动态、大规模的流量，导致资源利用效率低下，性能提升有限。FlowTurbo 是一种自适应的系统级卸载方法，通过联合优化软件规则调度和硬件规则查找来实现命中驱动的 MegaFlow 硬件卸载；FlowTurbo 的核心创新有三点：（1）流量感知、命中驱动的 MegaFlow 卸载框架，选择性地将热点通配符规则迁移到硬件； (2) 针对 MegaFlow 规则的特定领域、硬件友好的草图，用于跟踪规则热度并使调度程序能够做出及时、精确的卸载决策； (3) 特定领域、算法与硬件共同设计的数据包分类加速器，支持线速规则匹配和在线规则更新；使用多个真实流量轨迹进行评估表明，FlowTurbo 的平均加速覆盖率达到 89.4%，硬件加速器可提供 400 MOPS 的最大吞吐量，同时仅消耗 3.3% 的 FPGA 逻辑资源。
  - 相较现有解决方案仍然依赖于粗粒度、尽力卸载，这难以应对动态、大规模的流量，导致资源利用效率低下，性能提升有限，核心创新是FlowTurbo 是一种自适应的系统级卸载方法，通过联合优化软件规则调度和硬件规则查找来实现命中驱动的 MegaFlow 硬件卸载；FlowTurbo 的核心创新有三点：（1）流量感知、命中驱动的 MegaFlow 卸载框架。
  - 可编程数据平面与云网络、Programmable Network Hardware、Scheduling/Orchestration、Cloud Networking: DPUs, SmartNICs & Gateways

- [CubeTrace: Microscopic Network Tracing for Heterogeneous Cloud Gateways](https://dl.acm.org/doi/10.1145/3789240.3829165)
  - Yunming Xiao (The Chinese University of Hong Kong, Shenzhen), Yinchao Yang (Tencent), Jiaqi Zheng (Nanjing University), Xuqian Li, Dongbo Gu, Jun Zhang, Miantao Wan, Chao Pei (Tencent), Chen Tian (Nanjing University), Mingwei Xu (Tsinghua University), Ang Chen (University of Michigan), Congcong Miao (National University of Singapore)
  - 现代云网关已经发展到包含多种网络功能和异构硬件，例如可编程交换机和 FPGA，以处理不断增加的工作负载并最大限度地减少转发延迟；然而，现有的网络跟踪工具主要在设备粒度上运行，无法查明哪个硬件组件上的哪个功能导致数据包丢失或延迟峰值。为了弥补这一差距，CubeTrace 是一个统一的功能级流跟踪系统，可以在异构云网关内进行微观跟踪；CubeTrace 将跟踪单元标准化为跨不同硬件平台的立方体，无论其底层实现如何变化，并且出于可靠性原因以流粒度运行；这为异构网关引入了新的跟踪抽象，同时保持较低的开销；此外，CubeTrace 收集的流立方体数据可以解码为数据包级表示，并与完善的分布式跟踪框架集成，从而可以使用现成的分析工具；CubeTrace 部署在大型云网关中后，显著改进了问题定位，将解决时间从几小时甚至几天缩短到几分钟。
  - 相较现有的网络跟踪工具主要在设备粒度上运行，无法查明哪个硬件组件上的哪个功能导致数据包丢失或延迟峰值，核心创新是CubeTrace 是一个统一的功能级流跟踪系统，可以在异构云网关内进行微观跟踪；CubeTrace 将跟踪单元标准化为跨不同硬件平台的立方体，无论其底层实现如何变化，并且出于可靠性原因以流粒度运行。
  - 可编程数据平面与云网络、Programmable Network Hardware、Network Measurement/Telemetry、Cloud Networking: DPUs, SmartNICs & Gateways

- [Rethinking Cloud Optimization: Volatility-Driven for Better Outcomes](https://dl.acm.org/doi/10.1145/3789240.3829141)
  - Baoqing Wang, Gongming Zhao, Hongli Xu, Shibo Wu, Zhuolong Yu, Jiawei Liu, Junhong Lu (University of Science and Technology of China), Shaohui Xu, Fanjie Meng (Tencent Cloud)
  - 云提供商通常采用超额订阅策略来最大限度地提高盈利能力，利用租户购买的资源与其工作负载实际消耗的资源之间的巨大差距；然而，工作负载的时间波动可能会导致超额订阅节点过载；事实上，减少工作负载的时间波动是解决上述挑战的关键。受这一见解的启发，系统首先设计了一个新指标，称为基于最大变异系数（MCV），以量化工作负载的时间波动性；然后该工作设计 Hestia，一个通过工作负载聚合实现长期稳定超额订阅的框架；具体来说，该工作设计一种基于平滑的方法来根据周期性对适合聚合的工作负载进行分类；随后，该工作设计一种聚合算法来最小化总体 MCV，并将聚合的工作负载视为超额订阅的单位；实验结果表明，以 CPU 为代表，Hestia 降低了 MCV 43.3%，超额认购利润增加了 66.74%。
  - 相较事实上，减少工作负载的时间波动是解决上述挑战的关键，核心创新是受这一见解的启发，系统首先设计了一个新指标，称为基于最大变异系数（MCV），以量化工作负载的时间波动性；然后该工作设计 Hestia，一个通过工作负载聚合实现长期稳定超额订阅的框架。
  - 可编程数据平面与云网络、Network Measurement/Telemetry、Scheduling/Orchestration、Cloud Networking: DPUs, SmartNICs & Gateways

- [Connecting 100K+ GPUs: Building the Communication Stack for Large-Scale LLM Training](https://dl.acm.org/doi/10.1145/3789240.3829152)
  - Hongyi Zeng, Min Si, Pavan Balaji, Yongzhou Chen, Ching-Hsiang Chu, Adithya Gangidi, Prashanth Kannan, Bingzhe Liu, Saif Hasan, Dong He, Deep Shah, Ashmitha Jeevaraj Shetty, Gregory R Steinbrecher, Srikanth Sundaresan, Yulun Wang, Yexin Wu, Mingran Yang, Kenny Yu, Minlan Yu (Harvard University), Cen Zhao, Shengbao Zheng, Wesley Bland, Denis Boyda, Suman Gumudavelli, Subodh Iyengar, Daniel Johnson, Cristian Lumezanu, Kai Luo, Rui Miao, Zhe Qu, Venkatraghavan Ramesh, Jingliang Ren, Maxim Samoylov, Jan Seidel, Qiye Tan, Feng Tian, Xinfeng Xie, Jingyi Yang, Yimeng Zhao, Shuqiang Zhang, Tiane “Art” Zhu (Meta)
  - 10 万+ GPU 集群的到来标志着人工智能基础设施的新前沿；标准通信堆栈面临着新的挑战，因为物理拓扑跨越多个数据中心建筑，引入了高带宽延迟产品链路，与机架内流量相比，延迟增加了高达 30 倍；研究团队展示 Meta 的网络架构和软件堆栈，旨在支持世界上最大的 RoCE 结构之一，目前跨多个数据中心建筑连接超过 100,000 个 GPU。为了克服扩展障碍，该工作设计可扩展的初始化策略，通过急切的进程组创建和 O(N) 拓扑发现将启动时间减少了 11 倍，同时还引入了资源管理系统，通过按需分配将 GPU 内存使用量减少了 2 倍；研究团队进一步详细介绍了利用动态队列对负载平衡来饱和链路的自定义传输层以及一组操作工具；这些创新已部署在生产中，为训练最先进的大型语言模型提供了基础通信结构。
  - 相较标准通信堆栈面临着新的挑战，因为物理拓扑跨越多个数据中心建筑，引入了高带宽延迟产品链路，与机架内流量相比，延迟增加了高达 30 倍，核心创新是研究团队展示 Meta 的网络架构和软件堆栈，旨在支持世界上最大的 RoCE 结构之一，目前跨多个数据中心建筑连接超过 100,000 个 GPU。
  - 可编程数据平面与云网络、LLM Systems、MoE、Collective Communication、Failure Diagnosis、Scheduling/Orchestration

- [DistDPU: A Disaggregated DPU Architecture for High-Performance and Cost-Efficient AI Clouds](https://dl.acm.org/doi/10.1145/3789240.3829161)
  - Hao Mei (Fudan University), Lizhou Gao (Tencent), Yuanyi Zhu (Fudan University), Liang Wang, Peng Yang, Chao Pei (Tencent), Chuhao Chen, Zijian Li (Fudan University), Jian Zhao, Dongbo Gu, Hongchen Ren, Jiyuan Chen, Junpeng Zhang, Yunpeng Guan, Jianye Yuan, Jian Wang (Tencent), Yibo Huang (University of Michigan), Yang Xu (Fudan University)
  - AI 训练和推理正在推动云网络的每台服务器带宽达到太比特每秒 (Tbps)，这对当今云网络架构的可扩展性和效率提出了挑战；流行的设计通过堆叠单片数据处理单元 (DPU) 来扩展带宽，但这种方法紧密耦合控制和数据平面资源，导致成本、功耗和操作复杂性过高。DistDPU 是一种分解的 DPU 架构，它重新定义了高带宽云网络的扩展抽象；DistDPU 将单片 DPU 分解为轻量级、带宽配置执行模块 (EM) 和共享的、以控制为中心的编排模块 (OM)，从而实现数据和控制平面资源的独立扩展；通过在单个 OM 下横向扩展低成本 EM，DistDPU 向云管理平面公开统一的高带宽逻辑 DPU 接口；DistDPU 已在生产环境中部署了两年。
  - 相较流行的设计通过堆叠单片数据处理单元 (DPU) 来扩展带宽，但这种方法紧密耦合控制和数据平面资源，导致成本、功耗和操作复杂性过高，核心创新是DistDPU 是一种分解的 DPU 架构，它重新定义了高带宽云网络的扩展抽象；DistDPU 将单片 DPU 分解为轻量级、带宽配置执行模块 (EM) 和共享的、以控制为中心的编排模块 (OM)，从而实现数据和控制平面资源的独立扩展。
  - 可编程数据平面与云网络、RDMA、SmartNIC/DPU、Security/Privacy、Scheduling/Orchestration

- [Pegasus: A Data Center Network for Bare-Metal AI Cloud](https://dl.acm.org/doi/10.1145/3789240.3829186)
  - Xianneng Zou (Tsinghua), Yadong Liu (Tencent), Yiran Zhang (Unaffiliated), Jian Zhao, Zhaoxun Zhou (Tencent), Qing Wang (Nanjing University), Xingyi Li, Liang Wang (Tencent), Xingda Wei (Shanghai Jiao Tong University), Xiaojie Huang, Zhaohe Chen, Yinben Xia (Tencent), Yuxi Wang (Unaffiliated), Kai Ren, Lizhou Gao, Jiajun Liang, Jian Wang, Chunxu Zhao, Weifeng Zhang, Lu Shi, Xin Li, Jiewei Yang, Hao Lu, Yunpeng Guan, Dongbo Gu, Chao Pei, Xiang Li, Zekun He (Tencent), Yong Jiang (Tsinghua), Yachen Wang (Tencent)
  - 如今，人工智能云是为不同用户提供人工智能服务的关键，而云网络是其基础；该工作总结设计、部署和运营 Pegasus（一个为 AI 云量身定制的数据中心网络）的经验，以及从其部署中汲取的运营经验教训；Pegasus 的关键设计包括： 1）网络虚拟化：DPU-RNIC 解耦的协作硬件架构，使单个 DPU 能够虚拟化多个 RNIC，同时降低功耗。研究团队在 DPU 和 RNIC 上设计了两级流表，以支持 underlay-overlay IP 地址转换并确保隔离；对于 DPU-RNIC 通信，该工作设计每个 RNIC 通信状态机以减少通信开销；2) 网络传输：RNIC 中定制且透明的传输卸载，为各种 AI 工作负载提供低延迟和高吞吐量的通信性能；研究团队仔细卸载 RNIC 中的每数据包负载平衡和基于信用的拥塞控制，优化重新排序延迟并消除硬件抖动的影响；Pegasus 已经在生产中部署了两年多，目前覆盖 8K GPU 并支持广泛的租户 AI 应用。
  - 官方摘要未展开更细的直接基线；可核验的核心创新是研究团队在 DPU 和 RNIC 上设计了两级流表，以支持 underlay-overlay IP 地址转换并确保隔离；对于 DPU-RNIC 通信，该工作设计每个 RNIC 通信状态机以减少通信开销。
  - 可编程数据平面与云网络、SmartNIC/DPU、Congestion Control、Cloud Networking: DPUs, SmartNICs & Gateways

- [Balancing and Beyond: Communication-Centric Optimizations in Expert Parallelism](https://dl.acm.org/doi/10.1145/3789240.3829201)
  - Jiamin Cao, Qingxu Li, Yaozhong Liu, Jiaqi Gao, Yan Zhang, Shangfeng Shi, Zian Chen, Yizhi Wang, Jun Zhang, Kunling He, Ennan Zhai, Jianbo Dong, Binzhang Fu, Dennis Cai (Alibaba Cloud)
  - 专家混合 (MoE) 架构通过每个代币仅激活一小部分专家，将大型语言模型 (LLM) 扩展到数万亿个参数；在实践中，MoE 推理通常与专家并行 (EP) 一起部署，它将整个专家置于不同的 GPU 上以保持内核效率；然而，生产 EP 部署通常会遇到两个瓶颈：(1) 专家工作负载不平衡，这会导致计算和通信落后；(2) 通信效率低下，即使在平衡之后，GPU 间传输也会主导延迟。该工作设计 EPIC，这是一种经验驱动的 EP 推理系统，可以逐步解决这些问题以进行实际部署；EPIC 通过性能感知专家迁移和运行时专家激活来缓解不平衡，然后改善与拓扑自适应传输内核的通信以及细粒度计算通信重叠；EPIC 已在其在线推理服务中针对开源模型（例如 Qwen3-Coder 和 DeepSeek-R1）和内部模型在 O(10K) GPU 上大规模部署，将通信时间和每个令牌延迟分别减少了高达 40% 和 21%。
  - 相较生产 EP 部署通常会遇到两个瓶颈：(1) 专家工作负载不平衡，这会导致计算和通信落后；(2) 通信效率低下，即使在平衡之后，GPU 间传输也会主导延迟，核心创新是该工作设计 EPIC，这是一种经验驱动的 EP 推理系统，可以逐步解决这些问题以进行实际部署；EPIC 通过性能感知专家迁移和运行时专家激活来缓解不平衡，然后改善与拓扑自适应传输内核的通信以及细粒度计算通信重叠。
  - 可编程数据平面与云网络、LLM Systems、MoE、Cloud Networking: DPUs, SmartNICs & Gateways

- [FlowForm: Scalable Passive Metasurface Network for mmWave Coverage Expansion](https://dl.acm.org/doi/10.1145/3789240.3829102)
  - Wuqiong Zhao, Baicheng Chen, Kai Zheng, Xingyu Chen, Wenqian Zhang, Xinyu Zhang (University of California San Diego)
  - 毫米波 (mmWave) 网络提供数千兆位数据速率，但存在严重的路径损耗和阻塞，导致覆盖范围参差不齐；新兴的可重构智能表面 (RIS) 可以缓解这些挑战，但它们对主动控制通道、电源和复杂的运行时协调的依赖会带来巨大的硬件和部署开销。FlowForm 是一种使用无源超表面网络扩展毫米波覆盖范围的系统，无需电源、控制或运行时协调；FlowForm 的关键创新是分层流拓扑，它将无源超表面组织为主要流（使用近场聚焦的定向中继链）和次要流（广域扇形光束），从而实现多跳无源路由和模拟信号的无线组合；该工作设计一个理论框架，建立了该拓扑的最优性，以及共同确定超表面放置和梁配置的分层优化算法；FlowForm 使用标准毫米波网络协议透明地运行，通过多样性感知设计而不是运行时重新配置来管理信道动态和多用户干扰；研究团队对五个室内环境进行的实验评估表明，使用低成本 3D 打印超表面（每单位 2 美元），平均速率提高了 94%，覆盖范围扩大了 114%，以低几个数量级的成本实现了与主动 RIS 相当的性能。
  - 相较新兴的可重构智能表面 (RIS) 可以缓解这些挑战，但它们对主动控制通道、电源和复杂的运行时协调的依赖会带来巨大的硬件和部署开销，核心创新是FlowForm 是一种使用无源超表面网络扩展毫米波覆盖范围的系统，无需电源、控制或运行时协调；FlowForm 的关键创新是分层流拓扑，它将无源超表面组织为主要流（使用近场聚焦的定向中继链）和次要流（广域扇形光束）。
  - 无线、蜂窝与感知、Wireless/Sensing、Internet Routing、Wireless, Backscatter & Sensing

- [Concurrent OFDM Backscatter with a Single Commercial Receiver](https://dl.acm.org/doi/10.1145/3789240.3829127)
  - Caihui Du, Jihong Yu (Beijing Institute of Technology), Rongrong Zhang (Capital Normal University)
  - 并发 OFDM 反向散射有望实现飞速增长的超低功耗物联网设备的高效连接；然而，现有设计依赖频域划分，存在同步距离短、抗干扰能力差、与商用 Wi-Fi 接收器不兼容等问题。该工作设计 C2Scatter，这是第一个并发 OFDM 反向散射系统，可与单个商用 OFDM Wi-Fi 接收器并行解码标签数据；它是通过两项关键技术实现的；(1)标签上的拉动驱动同步方案，通过利用注入拉动能力而不是放大接收信号来实现长距离同步，从而解决了现有工作中的灵敏度-功率权衡；(2)轻量级延迟域划分方案，刻意引入唯一的时间偏移(TO)作为每个标签的信号特征，以在延迟域中分离并发标签的信号；其设计与放大驱动的同步方案相比，灵敏度提高了 37dB，功耗降低了 131.1 倍，并且与商用 802.11n Wi-Fi NIC 兼容，与 SOTA NanoScatter 和 ConcurScatter 相比。
  - 相较现有设计依赖频域划分，存在同步距离短、抗干扰能力差、与商用 Wi-Fi 接收器不兼容等问题，核心创新是该工作设计 C2Scatter，这是第一个并发 OFDM 反向散射系统，可与单个商用 OFDM Wi-Fi 接收器并行解码标签数据；它是通过两项关键技术实现的。
  - 无线、蜂窝与感知、Wireless/Sensing、Wireless, Backscatter & Sensing

- [Deep-Soil Acoustic Backscatter Networking for Electrical Substation Grounding Assessment](https://dl.acm.org/doi/10.1145/3789240.3829168)
  - Fengrui Zhang, Shanyue Wang, Bowen Xue (Hong Kong Polytechnic University), Lei Yang (The Hong Kong Polytechnic University)
  - 变电站接地完整性是电力系统安全的基础，但其长期性能受到难以连续监测的土壤条件的强烈影响；由于土壤中信号严重衰减、强电磁干扰以及频繁遭受高压雷击，现有的地下传感方法基本上无效。该工作设计 SoilCapsule，这是一种分布式、无电池、胶囊式声学反向散射传感系统，用于变电站接地评估；SoilCapsule 收集超声波能量用于计算、传感和通信，使其具有固有的抗高压冲击能力；最后，在运行中的中型变电站中现场部署 20 个 SoilCapsule 传感器证明了在现实环境中进行长期接地监测的可行性。
  - 相较现有的地下传感方法基本上无效，核心创新是该工作设计 SoilCapsule，这是一种分布式、无电池、胶囊式声学反向散射传感系统，用于变电站接地评估；SoilCapsule 收集超声波能量用于计算、传感和通信，使其具有固有的抗高压冲击能力。
  - 无线、蜂窝与感知、Wireless/Sensing、Wireless, Backscatter & Sensing

- [Concord: Airtime-Aware Contention Control for Taming Tail Latency from Wi-Fi Frame Bursting](https://dl.acm.org/doi/10.1145/3789240.3829149)
  - Fengqian Guo, Siqi Wei, Sihao Miao (University of Science and Technology of China), Xinle Du (Tsinghua University), Hancheng Lu (University of Science and Technology of China)
  - 在拥塞的 Wi-Fi 中，发送较少并不能保证较低的延迟；根据对野外商用 Wi-Fi 路由器的测量，即使在负载可以忽略不计的情况下，稀疏的微流也会遭受类似批量的尾部延迟；这种延迟是由 MAC 级竞争动态而不是流的发送速率驱动的，导致基于速率的拥塞控制无效。Concord 是一种 Wi-Fi MAC 机制，它使突发通话时间成为一个明确的控制信号，并惩罚过度的媒体持有；Concord 完全在 Wi-Fi 驱动程序内运行，无需流分类，无需更改客户端或协议，并且每次突发仅产生 O(1) 工作量；对于交互式工作负载（云游戏），与默认 IEEE 堆栈相比，它可将 99.9% 的延迟从 231/441 毫秒减少至 92 毫秒，并将饥饿现象减少多达 10 倍。
  - 官方摘要未展开更细的直接基线；可核验的核心创新是Concord 是一种 Wi-Fi MAC 机制，它使突发通话时间成为一个明确的控制信号，并惩罚过度的媒体持有；Concord 完全在 Wi-Fi 驱动程序内运行，无需流分类，无需更改客户端或协议，并且每次突发仅产生 O(1) 工作量。
  - 无线、蜂窝与感知、Congestion Control、Network Measurement/Telemetry、Wireless/Sensing、Wireless, Backscatter & Sensing

- [LITE: Loss-resilient Immersive Telepresence with Multi-modal Semantics](https://dl.acm.org/doi/10.1145/3789240.3829116)
  - Ruizhi Cheng (George Mason University), Harshvardhan Takawale (University of Maryland, College Park), Nan Wu (George Mason University), Nirupam Roy, Sennur Ulukus (University of Maryland, College Park), Matteo Varvello (Nokia), Eugene Chai (Nokia Bell Labs), Bo Han (George Mason University)
  - 沉浸式远程呈现有潜力通过高度互动和引人入胜的体验来改变实时通信；尽管最近在降低通信和计算成本方面取得了进展，但现有系统在很大程度上忽视了数据包丢失，这可能严重降低体验质量 (QoE)；为了应对这些挑战，LITE 是第一个具有抗丢失能力的沉浸式远程呈现系统。LITE 包含三个关键设计原则：(1) 利用语义通信来传输紧凑的运动和音频语义，这些语义可以重构为远程用户的沉浸式表示和语音，从而实现快速语义级恢复，并在丢失情况下对拥塞控制引起的速率降低保持鲁棒性； （2）通过轻量级多模态模型融合音频和运动语义，实现运动语义的准确、实时恢复； (3) 将过去多个帧的音频语义编码为简洁的神经冗余，以实现稳健的恢复；结果表明，与现有方案相比，LITE 将 QoE 提高了 109%，同时维持每秒 30 帧的实时流传输并保持高视觉保真度（结构相似性指数测量值高于 0.9，其中 1 表示完美相似）。
  - 相较现有系统在很大程度上忽视了数据包丢失，这可能严重降低体验质量 (QoE)，核心创新是LITE 是第一个具有抗丢失能力的沉浸式远程呈现系统；LITE 包含三个关键设计原则：(1) 利用语义通信来传输紧凑的运动和音频语义，这些语义可以重构为远程用户的沉浸式表示和语音，从而实现快速语义级恢复。
  - 无线、蜂窝与感知、Video/QoE、Compression/Encoding、Wireless, Backscatter & Sensing

- [FabricPerf: Measuring NIC-less Scale-Up Network through GPU Communication Kernel Profiling](https://dl.acm.org/doi/10.1145/3789240.3829172)
  - Songlin Huang, Chenshu Wu (The University of Hong Kong)
  - 分布式机器学习系统的快速增长将 ML 网络从 CPU/GPU-NIC 架构转变为 GPU-Fabrics 架构，从而产生了测量和优化无 NIC 扩展网络的新兴需求；然而，NIC 的消失消除了关键的可观测点，并使现有的测量工具在很大程度上仅限于粗略的应用层遥测。FabricPerf 是一个扩展网络测量工具包，可实现细粒度的数据包级时间戳和跨层硬件洞察；FabricPerf 采用软件-硬件协同设计，将 GPU 通信内核中的协议级探测和 GPTP 时钟同步与物理管道的内存分析集成在一起；研究团队相信 FabricPerf 提高了 Scale-up 网络的可观测性，为更完整、更高效的网络堆栈奠定了基础。
  - 相较现有的测量工具在很大程度上仅限于粗略的应用层遥测，核心创新是FabricPerf 是一个扩展网络测量工具包，可实现细粒度的数据包级时间戳和跨层硬件洞察；FabricPerf 采用软件-硬件协同设计，将 GPU 通信内核中的协议级探测和 GPTP 时钟同步与物理管道的内存分析集成在一起。
  - 数据中心网络、传输与互连、Network Measurement/Telemetry、Cellular/RAN、Scale-Up Fabrics: Measurement & Design

- [Efficient and Flexible Datapaths for Fine-Grained Rack-Scale Interconnects with Elastic QP](https://dl.acm.org/doi/10.1145/3789240.3829160)
  - Chenxingyu Zhao (University of Washington), Yibo Wu (University of Wisconsin-Madison), Hongtao Zhang, Jaehong Min (University of Washington), Ming Liu (University of Wisconsin–Madison), Arvind Krishnamurthy (University of Washington)
  - 机架级互连是新兴通信密集型系统扩展的关键数据路径；该数据路径的创新解决方案正在快速崛起，尤其是基于以太网的解决方案；然而，现有的基于硬件的解决方案（例如 RDMA）面临性能问题，特别是对于小消息内存访问，并且受到硬件固定处理的不灵活性的影响。该工作设计软件插入数据路径（SID），这是一种高效、软件灵活且低成本的机架级互连解决方案，特别针对细粒度内存访问进行了优化；提高小消息效率是一个众所周知的挑战，而软件的灵活性似乎进一步放大了性能障碍；SID 通过利用一种见解来提高性能：现有 NIC 主要依赖于队列对 (QP) 级并行性，但未充分利用 QP 内工作队列元素 (WQE) 级并行性；由于排序语义和请求分派，利用并行性并非易事，尤其是在 WQE 级别；评估表明，SID 的小消息速率比基于 RDMA 的基准高出 11.03 倍，并且支持 CPU 和 GPU-Direct 操作。
  - 相较现有的基于硬件的解决方案（例如 RDMA）面临性能问题，特别是对于小消息内存访问，并且受到硬件固定处理的不灵活性的影响，核心创新是该工作设计软件插入数据路径（SID），这是一种高效、软件灵活且低成本的机架级互连解决方案，特别针对细粒度内存访问进行了优化；提高小消息效率是一个众所周知的挑战，而软件的灵活性似乎进一步放大了性能障碍。
  - 数据中心网络、传输与互连、RDMA、Scale-Up Fabrics: Measurement & Design

- [Balanced Sparse Tree: A Scalable Network Topology for Large Language Models](https://dl.acm.org/doi/10.1145/3789240.3829208)
  - Shaoteng Liu (Huawei), Dejun Kong (Shanghai Jiao Tong University), Huitian Wang (Huawei), Hongji Dong (Shanghai Jiao Tong University), Xiangyu Chen, Yi Zhang, Xiaotian Zhou, Peng Dong, Rui Meng, Fuguang Huang, Xia Zhu (Huawei), Xiaofeng Gao (Shanghai Jiao Tong University), Bingyang Liu (Huawei), Guihai Chen (Shanghai Jiao Tong University)
  - 大型语言模型（LLM）的发展催生了对计算网络前所未有的需求，特别是大规模、少跳和低延迟的需求，这直接支撑了 LLM 任务效率；然而，诸如 Clos 之类的主流拓扑受到成本和延迟的困扰，而具有良好可扩展性的拓扑则存在对称或集体通信问题。为了在设计指标之间实现良好的平衡，该工作设计一种名为平衡稀疏树（BST）的新型拓扑，这是一种以对称设计和稀疏连接为特征的拓扑，受到超图理论和斯坦纳系统的启发；其直径度上限接近二部双正则图的摩尔界，比其他已知的直径 2 拓扑更大；此外，BST 在集体通信方面实现了 3.9% 至 11.8% 的增益，并且比最先进的拓扑有 13.4% 的改进。
  - 相较诸如 Clos 之类的主流拓扑受到成本和延迟的困扰，而具有良好可扩展性的拓扑则存在对称或集体通信问题，核心创新是为了在设计指标之间实现良好的平衡，该工作设计一种名为平衡稀疏树（BST）的新型拓扑，这是一种以对称设计和稀疏连接为特征的拓扑，受到超图理论和斯坦纳系统的启发；其直径度上限接近二部双正则图的摩尔界，比其他已知的直径 2 拓扑更大。
  - 数据中心网络、传输与互连、LLM Systems、Collective Communication、Internet Routing、Scale-Up Fabrics: Measurement & Design

- [Understanding and Profiling the Accelerator Chiplet Network Using PingPoint](https://dl.acm.org/doi/10.1145/3789240.3829110)
  - Junyeol Ryu (University of Wisconsin-Madison), Ming Liu (University of Wisconsin–Madison), Matthew D. Sinclair (University of Wisconsin–Madison)
  - 新兴的基于 Chiplet 的加速器引入了一种新型主机内网络——加速器 Chiplet 网络 (ACN)，它链接计算 Chiplet、IO Chiplet 和内存模块，并越来越多地控制应用程序性能；然而，ACN 行为在很大程度上仍然不透明：现有工具忽略了包上通信，而是将开销归因于计算或内存子系统，而由于专有微架构、与执行管道的紧密耦合以及应用程序活动和硬件之间的复杂映射。为了克服这一挑战，该工作设计一个 ACN 表征框架，可以对路径和链路进行细粒度、拓扑感知的探测；然后，研究团队用它来揭示多芯片 GPU 上的基本 ACN 性能属性；在这些见解的指导下，该工作设计 PingPoint，这是一个用于 ACN 原生分析的轻量级实用程序；其主要见解是，将 ACN 建模为具有排队抽象的逻辑、基于软管的图，并结合现场软件探测，使得对原本不透明的 ACN 进行系统剖析成为可能；在不同的工作负载和硬件中，它可以暴露隐藏的瓶颈，指导内核布局和流量整形，量化 ACN 争用的性能影响，并以边际开销实现实际优化。
  - 相较现有工具忽略了包上通信，而是将开销归因于计算或内存子系统，而由于专有微架构、与执行管道的紧密耦合以及应用程序活动和硬件之间的复杂映射，ACN 引起的延迟、带宽异构性和拥塞很难观察到，核心创新是该工作设计一个 ACN 表征框架，可以对路径和链路进行细粒度、拓扑感知的探测；然后，研究团队用它来揭示多芯片 GPU 上的基本 ACN 性能属性。
  - 数据中心网络、传输与互连、Network Measurement/Telemetry、Scale-Up Fabrics: Measurement & Design

- [Prefetching for Short Video Streaming: Experiences from a Longitudinal Evolution at Planetary Scale](https://dl.acm.org/doi/10.1145/3789240.3829158)
  - Yinjie Zhang, Ying Chen, Yuming Hu, Aoyang Zhang, Pengcheng Chen, Zhixiang Luo, Shaopeng Li, Zhendong Zhong, Haiqing Tao, Lan Xie, Shenglan Huang, Zhiwei Fan, Feng Qian (ByteDance)
  - 短视频流的特点是快节奏、滚动驱动的用户交互；这对其流式算法设计提出了独特的挑战。据作者所知，人们对短视频流算法在大规模生产平台中的表现知之甚少；研究团队从现实世界的部署中提取了可行的见解，强调了启动延迟、带宽效率和低开销设计对于大规模短视频流的重要性。
  - 相较这对其流式算法设计提出了独特的挑战，核心创新是据作者所知，人们对短视频流算法在大规模生产平台中的表现知之甚少。
  - 视频、实时通信与 QoE、Video/QoE

- [Adaptive Bitrate Live Streaming over HTTP-FLV: A Practical System Perspective](https://dl.acm.org/doi/10.1145/3789240.3829169)
  - Le Zhang, Tong Meng (ByteDance), Bingcong Lu (SJTU and ByteDance), Jinghao Yuan, Lu Chen, Huanting Liu, Lei Xiao, Nailiang Wu, Zhou Sha, Changqing Yan, Jianrong Zhang, Jianxin Kuang (ByteDance), Li Song (SJTU)
  - 该工作设计 TikTok Live 中基于 HTTP-FLV 的自适应比特率直播的实现和部署经验。HTTP-FLV 不会像 HLS 和 DASH 等基于分段的流媒体协议那样将媒体流划分为单独的分段；正如预期的那样，服务器执行的 ABR 切换被证明可以提供更好的 QoE。
  - 官方摘要未展开更细的直接基线；可核验的核心创新是该工作设计 TikTok Live 中基于 HTTP-FLV 的自适应比特率直播的实现和部署经验；HTTP-FLV 不会像 HLS 和 DASH 等基于分段的流媒体协议那样将媒体流划分为单独的分段。
  - 视频、实时通信与 QoE、Congestion Control、Video/QoE

- [Horizon: A Hyper-Edge Observability Engine for Live Streaming Networks](https://dl.acm.org/doi/10.1145/3789240.3829153)
  - Ziqian Liu, Daqian Ding (The University of Hong Kong), Rui Han (ByteDance), Shixian Guo (ByteDance), Zhendong Xie, Aifang Xu, Changqian Wang, Kefei Liu (ByteDance), Jialin Li (National University of Singapore), Yunming Xiao (The Chinese University of Hong Kong, Shenzhen), Heming Cui, Yiming Qiu (The University of Hong Kong)
  - 实时流媒体服务在专用实时流媒体网络 (LiveNets) 上为主流实时交互提供支持；然而，使 LiveNet 大规模可靠具有挑战性：故障出现在面向用户的交付路径以及流协议和应用程序逻辑内，因此运营商需要持续的运行时监控来快速检测和定位事件，并需要主动的预检测试来在代表性环境和持续播放行为下进行更改。Horizon 是利用近用户、提供商管理的超边缘设备，并将它们编排到一个共享队列中，支持始终在线的监控和可定制的、场景驱动的验证；Horizon 已在生产环境中部署了三年多；到 2025 年，它使用 100,000 多个超边缘代理识别了 2,000 多个重大网络事件。
  - 相较使 LiveNet 大规模可靠具有挑战性：故障出现在面向用户的交付路径以及流协议和应用程序逻辑内，因此运营商需要持续的运行时监控来快速检测和定位事件，并需要主动的预检测试来在代表性环境和持续播放行为下进行更改，核心创新是Horizon 是利用近用户、提供商管理的超边缘设备，并将它们编排到一个共享队列中，支持始终在线的监控和可定制的、场景驱动的验证；Horizon 已在生产环境中部署了三年多。
  - 网络测量、诊断与可观测性、Network Measurement/Telemetry、Video/QoE、Scheduling/Orchestration

- [CacheFlare: Optimizing Cold Content Performance in CDNs](https://dl.acm.org/doi/10.1145/3789240.3829206)
  - Tiansheng Zhang, Yuling Chen, Ahmed Kamal, Liang Zhou, Jianfeng Tang, Huapeng Zhou, Thilan Ganegedata, Yuhan Guo, Sanjay Sane, Ben Vallis (Meta Platform Inc.), Theophilus A. Benson (Carnegie Mellon University), Ying Zhang (Meta Platform Inc.)
  - 现有的内容分发网络（CDN）研究主要集中在优化热门内容的分发，即吸引大量用户频繁且重复访问的热门内容；然而，在 Meta，研究发现不太受欢迎且访问频率较低的冷内容对用户体验构成了重大挑战，尤其是在大量直接消息媒体的情况下。受这些发现的启发，CacheFlare 是一套生产部署的解决方案，旨在通过提高冷内容的 CDN 命中率来增强体验质量 (QoE)；通过实验和生产验证，研究团队表明，即使是冷内容也可以受益于改进的缓存策略，使一系列网络性能指标提高高达 10%。
  - 相较在 Meta，研究发现冷内容不太受欢迎且访问频率较低，对用户体验构成了重大挑战，尤其是在大量直接消息媒体的情况下，核心创新是受这些发现的启发，CacheFlare 是一套生产部署的解决方案，旨在通过提高冷内容的 CDN 命中率来增强体验质量 (QoE)；通过实验和生产验证，研究团队表明，即使是冷内容也可以受益于改进的缓存策略，使一系列网络性能指标提高高达 10%。
  - 互联网架构、路由与流量控制、Video/QoE、Caching/CDN

- [Evolution of AliYANG: Model-driven and LLM-assisted Network Configuration Management](https://dl.acm.org/doi/10.1145/3789240.3829193)
  - Mohan Yu (Jilin University and Alibaba Cloud), Xumiao Zhang, Zhe An (Alibaba Cloud), En Wang (Jilin University), Bin Zheng (Alibaba Cloud)
  - AliYANG 面向多厂商、CLI/API 并存且持续演化的云网络配置，把 CLI 语义扩展进 YANG，并抽取 vendor-agnostic core model；NetCMDB 将模型编译为有类型配置对象，驱动端到端配置流程。LLM 只辅助厂商模型补全、核心模型设计和双向翻译代码生成，系统已管理数十万设备并积累三年部署经验。
  - 相较按厂商和接口维护难验证的模板/脚本，核心创新是先用统一语义模型隔离厂商实现，再把 LLM 放在模型维护与代码生成环节，而不是让其直接控制生产配置。
  - 网络验证、管理与安全、LLM for Systems、LLM Systems

- [Networked Agent Memory and Causality Representation: Experiences towards Interpretable Cloud-Scale Root-Causing](https://dl.acm.org/doi/10.1145/3789240.3829145)
  - Yanyu Ren (Tsinghua University), Xianshang Lin (Alibaba Cloud), Chenxu Wang (Nanjing University), Li Chen, Shuai Wang, Kaihui Gao (Zhongguancun Laboratory), Dan Li, Yunfeng Bai (Tsinghua University), Chen Tian (Nanjing University), Xinlei Zhang, Yunguang Li, Tao Lin, Ennan Zhai (Alibaba Cloud)
  - XiHe 面向云规模网络 incident 的根因诊断，让证据驱动的多个 Agent 分解任务，以 networked agent memory 共享全局上下文而不挤爆单个上下文窗口，并把观测到的依赖与证据合成为可核验因果图。系统在全球云基础设施部署 12 个月、处理 3,000 多起事件，准确率 94.6%，将 operator 根因分析时间降低 25.8%。
  - 相较黑盒分类器或每个 Agent 各自维护有限记忆，核心创新是把跨 Agent 记忆和网络化因果表示作为共同诊断状态，使最终根因链可追溯验证。
  - 网络测量、诊断与可观测性、Agent for Systems、Failure Diagnosis、Formal Verification

- [Detection and Localization of End-to-end Bitflip Errors in Data Centers](https://dl.acm.org/doi/10.1145/3789240.3829132)
  - Abhigyan Sharma, Neil Spring, Srikanth Sundaresan, Francesco Caggioni, Laurent Virot, Arber Mancaj (Meta)
  - Flipperino 定位能绕过 link-level check 的数据中心 bitflip：全网被动监测主机发现的 L4 checksum error，主动探测再将错误缩小到 host、rack switch 或 link，loopback test 最后复现并确认具体 switch port。生产结果已定位造成 97% L4 checksum error 的设备，三个月内在 8 台交换机上复现数据损坏。
  - 相较只依赖链路校验或零散主机报错，核心创新是用“被动发现—主动局部化—端口回环复现”的三层流程追到故障端口。
  - 网络测量、诊断与可观测性

- [Anytest: Localizing the Root Cause of Hardware Transport Performance Anomalies](https://dl.acm.org/doi/10.1145/3789240.3829125)
  - Zhaochen Zhang (Nanjing University), Jiaqi Gao, Sheng Cheng, Peiwen Yu, Feiyang Xue, Chang Liu (Alibaba Cloud), Boliang Liu (Fudan University), Kun Liu, Yubin Li (Alibaba Cloud), Rui Li, Li Wang, Peirui Cao, Qingkai Meng, Guihai Chen (Nanjing University), Gang Lu, Bo Shi, Shuguang Cheng, Shu Ma, Yongqing Xi, Binzhang Fu, Dennis Cai (Alibaba Cloud), Chen Tian (Nanjing University)
  - 基于 RoCEv2 的 RDMA 结构是现代高性能数据中心工作负载的支柱，但大规模部署越来越多地遭受传输层网络性能异常 (NPA)，例如吞吐量崩溃、持续不公平和延迟膨胀，即使没有链路故障。Anytest 是一种原位黑盒测试工具，可以定位商用 RoCEv2 RNIC 和以太网交换机上传输层 NPA 的根本原因，而无需重新布线或修改硬件；Anytest 将 RoCEv2 网络系统分解为逻辑角色，并通过使用协议正确的 DPDK 端点模拟其他角色来隔离被测硬件；Anytest 集成到跟踪-再现-本地化工作流程中，已在生产环境中部署约 1 年，将平均本地化工作量减少至 3.1 人时。
  - 相较定位 NPA 的根本原因是当今最困难的运营挑战之一：RoCEv2 传输逻辑被卸载到可观察性有限的专有 NIC/交换机硬件中；可用计数器错过μs 级动态；类似的症状可能源自紧密耦合的 RoCEv2 系统中的发送方、接收方或交换机行为，核心创新是Anytest 是一种原位黑盒测试工具，可以定位商用 RoCEv2 RNIC 和以太网交换机上传输层 NPA 的根本原因，而无需重新布线或修改硬件。
  - 网络测量、诊断与可观测性、RDMA、Network Measurement/Telemetry、Failure Diagnosis

- [Rules Offload Engine (ROE): Accelerating Host SDN Policy Evaluation](https://dl.acm.org/doi/10.1145/3789240.3829118)
  - Anshuman Verma, Tian Tan, Ahmed Abdelsalam, Milan Dasgupta, Jonathan Hunter, Zach Libby, Narayanan Ravichandran, Harish Srinivasan, Matt Reat, Nadeen Gebara, Vishal Gondaliya (Microsoft), Ezz Hamed (Meta), Rahul Garlapati, Lok Chand Koppaka, Abdullah Mughrabi, Dev Desai, Alexander Malysh, Shwetha Bhat, Rohan Kandi, Megan Sng (Microsoft), Tushar Garg (Meta), Muluken Hailesellasie, Andrew Putnam, Derek Chiou, Osman Ertugay (Microsoft), Alireza Dabagh (Microsoft Azure), Vivek Bhanu, Daniel Firestone (Microsoft)
  - 软件定义网络 (SDN) 策略评估分析和验证网络规则，以实现准确的数据包路由、管理访问控制并确保安全和隐私；因此，SDN 策略评估是每个网络数据包必须在公共云服务（例如 Azure）托管的虚拟机中经过的强制性步骤；在云规模上，这个问题会更加严重，因为需要在数百万个虚拟机上提供更多的每秒连接数 (CPS)。该工作设计规则卸载引擎 (ROE)，这是一种硬件软件共同设计的解决方案，可通过基于 FPGA 的 SmartNIC 加速 SDN 策略评估；该工作设计 ROE 指令集架构 (RISA)，该架构具有专用的网络友好指令；RISA 将控制策略数据和操作直接融合到指令中，以促进高效的 FPGA 实现；该工作设计一个 ROE 编译器，可以将 SDN 规则转换为 RISA 指令；ROE 部署在 Azure 中，并作为第二代 Azure Boost 的一部分。
  - 官方摘要未展开更细的直接基线；可核验的核心创新是该工作设计规则卸载引擎 (ROE)，这是一种硬件软件共同设计的解决方案，可通过基于 FPGA 的 SmartNIC 加速 SDN 策略评估；该工作设计 ROE 指令集架构 (RISA)，该架构具有专用的网络友好指令。
  - 可编程数据平面与云网络、SmartNIC/DPU、Programmable Network Hardware、Formal Verification、Security/Privacy、Internet Routing

- [Spillway: Orchestrating DPU and Host into a Unified vSwitching Fabric](https://dl.acm.org/doi/10.1145/3789240.3829154)
  - Xiaochong Jiang (Zhejiang University), Dian Fan, Yilong Lv, Naixuan Guan (Alibaba Cloud), Qiming Zhao, Sihan Fu (Zhejiang University), Ye Yang, Yu Zhou, Xuyang Ge, Denghui Wu, Yibin Shen, Guochun Hong, Zhipeng Zhang, Yijian Dong, Yiquan Chen, Shaoliang An, Zhixiong Guo, Yixin Xie, Yisong Qiao, Hongwei Ding, Haitao Jiang, Yimin Liu, Tao Shen, Baosheng Wang, Shize Zhang, Bowen Yang, Zikang Chen, Xiaomin Wu, Rong Wen, Yang Song, Jun Liang, Zhigang Zong, Xing Li (Alibaba Cloud), Chengkun Wei (Zhejiang University), Shunmin Zhu (Alibaba Cloud), Wenzhi Chen (Zhejiang University)
  - 向以数据处理单元 (DPU) 为中心的架构的过渡已成为现代云网络的事实标准，从而实现基础设施卸载并提高主机资源利用率；然而，DPU 的固定硬件限制越来越无法跟上主机计算密度和网络密集型工作负载的快速增长。Spillway 是一种统一的 vSwitching 结构，可将虚拟交换容量与静态 DPU 硬件限制解耦；Spillway 引入了 DPU-主机混合数据平面，当 DPU 成为瓶颈时，它可以重新利用空闲主机 CPU 资源来处理溢出流量；与传统的软件交换不同，Spillway 通过统一的资源调度程序有选择地激活基于主机的转发，在正常操作条件下不会产生任何开销；为了确保生产可行性，Spillway 在异构数据平面之间强制执行严格的性能隔离；大规模部署的实验结果表明，在突发流量工作负载下，Spillway 可将单节点连接处理能力提高高达 90%，并且对共置应用程序的干扰可以忽略不计。
  - 相较DPU 的固定硬件限制越来越无法跟上主机计算密度和网络密集型工作负载的快速增长，核心创新是Spillway 是一种统一的 vSwitching 结构，可将虚拟交换容量与静态 DPU 硬件限制解耦；Spillway 引入了 DPU-主机混合数据平面，当 DPU 成为瓶颈时，它可以重新利用空闲主机 CPU 资源来处理溢出流量。
  - 可编程数据平面与云网络、SmartNIC/DPU、Scheduling/Orchestration

- [From Nimitz to NetPila: The Evolution of Production-Scale Container Network](https://dl.acm.org/doi/10.1145/3789240.3829203)
  - Jiaqi Gao, Chao Qin, Sheng Cheng, Jiamin Cao, Guodong Yang, Zhenyu Zhang, Shuhong Zhu, Ennan Zhai, Dennis Cai (Alibaba Group)
  - 该工作总结字节跳动五年多的两代容器网络：Nimitz 以 VxLAN 做 overlay–underlay 映射，但在超过 10 万容器时受地址表和复杂封装处理限制；NetPila 改用简洁 IPv6 寻址，去掉 VxLAN 封装和映射表，以支撑 AI 训练/推理等大规模服务。论文给出两代系统的部署结果与迁移经验。
  - 相较依赖 VxLAN 封装与 overlay–underlay 映射的 Nimitz，核心改进是让 NetPila 用 IPv6 地址直接表达容器网络位置，消除 C100K 规模下的映射与封装开销。
  - 可编程数据平面与云网络、Cloud/Distributed Systems

- [Open the Floodgates in a Digital Twin: Experiences of Building Spillway for 100M+-User Signaling Storms in Cellular Core Network](https://dl.acm.org/doi/10.1145/3789240.3829205)
  - Hongtao Xie (Tsinghua University), Jianmin Liu (Tsinghua University), Ce Yang, Yu He (China Mobile), Li Chen (Zhongguancun Laboratory), Dan Li (Tsinghua University), Mineng Fu, Xi Chen, Siyu Chen (China Mobile)
  - 当大量设备同步重新连接尝试触发级联、亚稳态过载时，信令风暴就会威胁蜂窝核心网络；现有的防御依赖于本地过载控制的手动静态配置，而忽略了异构网络元素之间的串行依赖性。该工作设计 Spillway，这是一个数字孪生驱动的系统，可自动缓解全球信号泛滥；Spillway 引入了一种分层防御架构，强制实施无私节流，允许上游节点在下游瓶颈崩溃之前卸载负载；在实际事件中，包括应用程序异常和 RAN 故障，使用 Spillway 优化配置的网络所经历的用户回退次数比传统配置下预测的要少得多；事件后分析证实，预先部署的参数使所有网络元素保持在安全操作范围内。
  - 相较现有的防御依赖于本地过载控制的手动静态配置，而忽略了异构网络元素之间的串行依赖性，核心创新是该工作设计 Spillway，这是一个数字孪生驱动的系统，可自动缓解全球信号泛滥；Spillway 引入了一种分层防御架构，强制实施无私节流，允许上游节点在下游瓶颈崩溃之前卸载负载。
  - 无线、蜂窝与感知、Failure Diagnosis、Cellular/RAN

- [λ λ : A Programming Language for Silicon Photonics](https://dl.acm.org/doi/10.1145/3789240.3829151)
  - Vaibhav Mehta, Arjun Devraj (Cornell University), Bill Owens (Nysernet), Justin Hsu, Rachee Singh (Cornell University)
  - 该工作设计 δ1，一种用于硅光子学的编程语言；Δ使用线性类型系统对光学的物理约束进行编码，在编译时拒绝无法实现的程序。编译器将类型良好的程序降低为基于图形的中间表示，然后解决约束嵌入问题，将这些图形映射到任意硅光子开关目标，同时最大限度地减少信号损失；研究团队在商用光子开关上验证了 δ，证明了电路切换、时变转子切换和模拟网内计算的正确操作。
  - 相较Δ使用线性类型系统对光学的物理约束进行编码，在编译时拒绝无法实现的程序，核心创新是该工作设计 δ1，一种用于硅光子学的编程语言；编译器将类型良好的程序降低为基于图形的中间表示，然后解决约束嵌入问题，将这些图形映射到任意硅光子开关目标，同时最大限度地减少信号损失。
  - 数据中心网络、传输与互连、Optical Interconnect、Formal Verification、Optical & Photonic Fabrics

- [Opus: Photonic Rail-Optimized Fabric in ML Datacenters](https://dl.acm.org/doi/10.1145/3789240.3829187)
  - Eric Ding (Cornell University), Barry Lyu (University of Michigan), Bhaskar Kataria, Rachee Singh (Cornell University)
  - 铁路优化的网络结构已成为用于大规模机器学习训练的事实上的数据中心横向扩展结构；然而，使用高基数电气开关在轨道中提供全面的连接会带来大量的电力和成本；研究团队建议通过保留其通信语义来重新思考铁路抽象，但使用光路开关来实现它。关键挑战是光交换机一次支持一对一连接，从而限制使用混合并行性的 ML 工作负载中的流量扇出；研究团队通过并行驱动的轨道重新配置来克服这个问题，它利用了不同并行维度的非重叠通信阶段；这可以在针对训练迭代中的每个阶段定制的电路配置中对一组物理端口进行时间复用；结果表明，光子轨可以实现超过 23 倍的网络功耗降低和 4 倍的成本节省，同时在与生产相关的 OCS 重新配置延迟下仅产生适度的训练开销。
  - 相较研究团队建议通过保留其通信语义来重新思考铁路抽象，但使用光路开关来实现它，核心创新是关键挑战是光交换机一次支持一对一连接，从而限制使用混合并行性的 ML 工作负载中的流量扇出；研究团队通过并行驱动的轨道重新配置来克服这个问题，它利用了不同并行维度的非重叠通信阶段。
  - 数据中心网络、传输与互连、Collective Communication、Optical Interconnect、Scheduling/Orchestration、Optical & Photonic Fabrics

- [OmniPath Ping: Active Network Measurement in the Era of Packet Spraying](https://dl.acm.org/doi/10.1145/3789240.3829105)
  - Kaicheng Yang, Zongwei Lv, Peijun Huang, Kaitai Zhang, Qiuheng Yin, Yaoming Li, Feiyu Wang, Zhuochen Fan (Peking University), Yikai Zhao, Chen Sun (Huawei Technologies Co., Ltd.), Xia Zhu (Huawei Technologies Co., Ltd), Tong Yang (Peking University)
  - Ping 和 Traceroute 构成了网络监控的基本工具包；基于这些原语，最初的主动探测系统专注于实现交换机和链路的足够覆盖；通过将单个流的数据包分散到多个路径上，数据包喷射导致传统原语在故障定位中遭受路径模糊性的困扰，并导致全路径覆盖的开销过高。OmniPath Ping 是 (OPP)，这是第一个为数据包喷射下的服务跟踪而设计的诊断原语；OPP 通过交换机-主机协同设计克服了这些挑战，该设计采用两项关键技术：(1) 网络内 OmniPath 缓存，可捕获每跳遥测数据以解决路径模糊性； (2) 网内重复和重复数据删除机制，实现零冗余的全路径覆盖；为了进一步确保网络范围服务跟踪的可扩展性，OPP 结合了 (3) 拓扑感知并发控制机制来平衡 OmniPath 缓存 SRAM 使用和探测及时性；大量结果表明，OPP 以最小的主机和网络开销实现了 10 毫秒级的服务跟踪和全路径覆盖，仅需要 181 KB 的交换机 SRAM。
  - 相较传统原语在故障定位中遭受路径模糊性的困扰，并导致全路径覆盖的开销过高，核心创新是OmniPath Ping 是 (OPP)，这是第一个为数据包喷射下的服务跟踪而设计的诊断原语；OPP 通过交换机-主机协同设计克服了这些挑战，该设计采用两项关键技术：(1) 网络内 OmniPath 缓存，可捕获每跳遥测数据以解决路径模糊性。
  - 网络测量、诊断与可观测性、Network Measurement/Telemetry、Failure Diagnosis、Caching/CDN、Internet Measurement & Routing

- [HERMES: Repurposing User-Driven Speed Tests to Monitor the Internet](https://dl.acm.org/doi/10.1145/3789240.3829129)
  - Loqman Salamatian (Columbia University), Kevin Vermeulen (Ecole Polytechnique), David Choffnes (Northeastern University), Ethan Katz-Bassett (Columbia University), Phillipa Gill (Google)
  - 诊断性能下降并查明其根源对于运营商做出明智的路由决策以及政策制定者和研究人员评估互联网的稳定性至关重要，但目前还没有公开的观测站提供此功能；现有解决方案依赖于粗粒度信号，无法捕获最终用户的性能，而专有解决方案无法访问，并且为识别问题根源提供的归因有限。HERMES 是第一个填补这一空白的开放系统；HERMES 使用公开的 M-Lab 速度测试数据，该数据已存在多年，但以前从未用于自动检测和解释大规模的最终用户性能下降；结果展示它跟踪天气和电缆中断、诊断路由效率低下以及识别持续拥塞链路的能力。
  - 相较现有解决方案依赖于粗粒度信号，无法捕获最终用户的性能，而专有解决方案无法访问，并且为识别问题根源提供的归因有限，核心创新是HERMES 是第一个填补这一空白的开放系统；HERMES 使用公开的 M-Lab 速度测试数据，该数据已存在多年，但以前从未用于自动检测和解释大规模的最终用户性能下降。
  - 网络测量、诊断与可观测性、Network Measurement/Telemetry、Failure Diagnosis、Internet Routing、Internet Measurement & Routing

- [A Global Inference and Assessment of Large Shared IP Addresses](https://dl.acm.org/doi/10.1145/3789240.3829192)
  - Vasileios Giotsas (Cloudflare), Loqman Salamatian (Columbia University), Antoine Cordelle, Nick Wood (Cloudflare), Marwan Fayed (Cloudflare, and University of St Andrews (UK))
  - 该工作推断 VPN、proxy 和 carrier-grade NAT 背后的 multi-user IP：先用公开标注数据与全球 CDN request log 特征训练分类器，再用纯公开 M-Lab 数据建立独立模型验证可复现性，并分析 CGN 对用户、IPv6 和区域分布的影响。两类特征获得相近准确率，且 /24 级特征比单 IP 更关键。
  - 相较仅用单 IP 局部信号或私有可见性判断共享地址，核心创新是把全球 CDN 请求特征与公开数据交叉验证，并在 /24 粒度推断 M-IP。
  - 网络测量、诊断与可观测性、Caching/CDN、Scheduling/Orchestration、Internet Measurement & Routing

- [LARS: Keeping Local Traffic Local with Latency-Aware Route Servers at IXPs](https://dl.acm.org/doi/10.1145/3789240.3829211)
  - David de Andres Hernandez (IMDEA Networks Institute, Universidad Carlos III de Madrid), Yasin Alhamwy (University of Kassel), Daniel Wagner (DE-CIX / MPI-INF), Maximilian Stephan (Technische Universität München), Matthias Wichtlhuber (DE-CIX), Oliver Hohlfeld (University of Kassel)
  - Internet 交换点通过使用 BGP 进行路径选择的路由服务器促进流量交换，而无需考虑延迟。LARS 是第一个在 IXP 路由服务器上实现延迟感知路径优化的系统；它不需要更改 BGP，也不需要成员之间的双边协调，从而直接为所有 IXP 成员启用延迟感知路由；LARS 不断探测路由服务器 RIB，使用 RTT 派生的 BGP 社区来注释路由，并使成员能够 (i) 强制实施可配置的延迟半径，以抑制高延迟路由，以及 (ii) 在存在多个路径时首选较低延迟的替代方案；研究使用生产级原型在非常大的 IXP 上评估 LARS，该原型展示了稳定的延迟估计、通过选择性重新分配进行有效的尾部延迟控制以及优化 BGP 最佳路径的潜力。
  - 官方摘要未展开更细的直接基线；可核验的核心创新是LARS 是第一个在 IXP 路由服务器上实现延迟感知路径优化的系统；它不需要更改 BGP，也不需要成员之间的双边协调，从而直接为所有 IXP 成员启用延迟感知路由。
  - 网络测量、诊断与可观测性、Internet Routing、Internet Measurement & Routing

- [Near-optimal Online Traffic Engineering](https://dl.acm.org/doi/10.1145/3789240.3829123)
  - Arvin Ghavidel (University of Southern California), Pooria Namyar (Microsoft Research), Nikolai Matni (University of Pennsylvania), Walter Willinger (Northwestern University), Ramesh Govindan (University of Southern California)
  - 大多数部署的 WAN 流量工程 (TE) 系统都使用逻辑上集中的控制器，该控制器定期收集流量需求、运行 TE 优化或启发式算法，然后对网络进行编程；从规模上看，这些解决方案通常不是最优的，并且可能需要几分钟才能对需求变化或故障做出反应；该工作设计 OnlineTE，这是一个可以对需求变化和故障立即做出反应的系统，并在变化后几秒钟内提供接近最佳的解决方案。OnlineTE 基于优化分解理论，为基于路径的 MLU 和 Max-Flow 问题设计可扩展、接近最优的分布式 TE 求解器；在 OnlineTE 中，每个交换机解决一个局部子问题，并且一个中央协调器协调它们的收敛；因此，交换机一旦检测到需求变化或故障就可以触发重新优化，从而实现高反应性；在 750 节点 WAN 拓扑的测试台仿真中，OnlineTE 的性能比最先进的技术高出一个数量级。
  - 官方摘要未展开更细的直接基线；可核验的核心创新是该工作设计 OnlineTE，这是一个可以对需求变化和故障立即做出反应的系统，并在变化后几秒钟内提供接近最佳的解决方案；OnlineTE 基于优化分解理论，为基于路径的 MLU 和 Max-Flow 问题设计可扩展、接近最优的分布式 TE 求解器。
  - 网络测量、诊断与可观测性、Traffic Engineering、Internet Measurement & Routing

- [MonkeyTree: Near-Minimal Congestion for Multi-tenant Training via Migration](https://dl.acm.org/doi/10.1145/3789240.3829150)
  - Anton A. Zabreyko, Weiyang Wang, Manya Ghobadi (MIT)
  - MonkeyTree 是第一个通过基于作业迁移的碎片整理而不是网络层技术来缓解多租户 GPU 集群中的网络拥塞的系统。由于云运营商将机器学习训练作业共同部署在共享的、超额订阅的网络上，拥塞会降低超过三分之一作业的训练吞吐量；MonkeyTree 在 1,024 个 GPU 的集群上以 4:1 的超额订阅率将平均作业完成时间提高了 14%。
  - 官方摘要未展开更细的直接基线；可核验的核心创新是MonkeyTree 是第一个通过基于作业迁移的碎片整理而不是网络层技术来缓解多租户 GPU 集群中的网络拥塞的系统；由于云运营商将机器学习训练作业共同部署在共享的、超额订阅的网络上，拥塞会降低超过三分之一作业的训练吞吐量。
  - AI 集群网络与大模型系统、Collective Communication、RDMA、Internet Routing、Scheduling/Orchestration

- [Aegis: Contract-Bounded Online Adaptation for Networked Accelerator Clusters](https://dl.acm.org/doi/10.1145/3789240.3829167)
  - Rui Li, Shuang Cao (Dawn Computing)
  - 加速器集群产生突发网络流量：分布式训练通过全归约交换梯度，推理管道扇出请求，存储与延迟敏感的 RPC 竞争；位置不当会加剧拥堵：错误安排的训练作业可能会使 ECN 标记率提高 3 倍，并使同地服务尾部延迟增加 40%；然而调度程序忽略了实时结构状态。Aegis 是一种调度程序，可以根据运营商定义的合约使用实时结构遥测来调整布局；Aegis 以 1 秒的粒度摄取每个 ToR 队列深度和 ECN 计数器，将拥塞压力术语纳入放置评分中，并通过具有曝光控制的保守 bandit 在线发展；关于尾部延迟、公平性和拥塞的合约编译成安全信封，以控制推出并触发自动回滚；209.6 毫秒），将 SLO 违规减少 3.6 倍，并将 ECN 标记率降低 51%，同时将利用率从 68.4% 提高到 79.1%。
  - 相较调度程序忽略了实时结构状态，核心创新是Aegis 是一种调度程序，可以根据运营商定义的合约使用实时结构遥测来调整布局；Aegis 以 1 秒的粒度摄取每个 ToR 队列深度和 ECN 计数器，将拥塞压力术语纳入放置评分中，并通过具有曝光控制的保守 bandit 在线发展。
  - AI 集群网络与大模型系统、Network Measurement/Telemetry、Scheduling/Orchestration、Scheduling for ML Training Clusters

- [LEVELLER: Fair Communication Scheduling via Progress-Rate Awareness in Multi-Tenant Training Clusters](https://dl.acm.org/doi/10.1145/3789240.3829174)
  - Geng Li (China Telecom Cloud Computing Research Institute), Yang Li (China Telecom Cloud Computing Research Institute; Beijing University of Posts and Telecommunications), Mingyuan Zang (China Telecom Cloud Computing Research Institute), Jie Wu (China Telecom Cloud Computing Research Institute; Temple University)
  - 大型语言模型 (LLM) 的快速扩展已使深度学习训练 (DLT) 成为现代多租户 GPU 集群中的主要工作负载；虽然公平计算调度已得到充分研究，但处理执行时网络争用的公平通信调度仍有待探索；当前的 DLT 通信调度程序主要关注以效率为导向的目标，当并发作业竞争共享带宽时，通常会导致不同的性能下降甚至作业匮乏。LEVELLER 是第一个专门针对 DLT 工作负载实现最大最小公平性的通信调度系统；为了弥合传统流程级别公平性和 DLT 工作级别公平性之间的差距，LEVELER 引入了一种新颖的在线指标，即标准化进度率，它通过根据无争用理想情况衡量实际进度来量化训练经验；在 10 个 LLM 上的实验结果表明，与最先进的解决方案（包括 CASSINI、CRUX、Symphony 和 Sincronia）相比，LEVELER 将最低进度率提高了 57%，公平性提高了 17%，同时保持了有竞争力的集群效率。
  - 相较虽然公平计算调度已得到充分研究，但处理执行时网络争用的公平通信调度仍有待探索，核心创新是LEVELLER 是第一个专门针对 DLT 工作负载实现最大最小公平性的通信调度系统；为了弥合传统流程级别公平性和 DLT 工作级别公平性之间的差距，LEVELER 引入了一种新颖的在线指标，即标准化进度率。
  - AI 集群网络与大模型系统、LLM Systems、RDMA、Scheduling/Orchestration、Scheduling for ML Training Clusters

- [GeoOrchestra: Orchestrating Heterogeneous Geo-Distributed Training with Network-Aware Scheduling](https://dl.acm.org/doi/10.1145/3789240.3829136)
  - Ting Liu, Qinghua Wu (Institute of Computing Technology, Chinese Academy of Sciences), Jun Zhou, Yuan Sun (Purple Mountain Laboratories), Jingbin Yang, Jinglei Pei (Institute of Computing Technology, Chinese Academy of Sciences), Chen Zhang (Purple Mountain Laboratories), Heng Pan (Computer Network Information Center, Chinese Academy of Sciences), Zhenyu Li (Institute of Computing Technology, Chinese Academy of Sciences), Yunjie Liu (Purple Mountain Laboratories)
  - 扩展大型语言模型 (LLM) 越来越需要聚合地理上分散的资源；然而，由于极端的硬件异构性和有限的广域网 (WAN) 带宽，跨数据中心 (Cross-DC) 训练面临重大障碍；对 2,000 公里跨 DC 测试台的经验测量表明，硬件不匹配、组合搜索复杂性和共享网络争用的相互作用为异构训练带来了严重的性能瓶颈。为了解决这些复杂性，GeoOrchestra 是一个将资源过滤与细粒度策略搜索分离的系统；通过计算和内存配置文件抽象计算节点，同时将 WAN 链路建模为虚拟硬管道，GeoOrchestra 将并行策略搜索问题解构为三个级联阶段；具体来说，它采用异构感知修剪来过滤无效资源集，然后进行资源驱动搜索，利用资源差异来最大限度地提高效率；最后，系统通过动态时隙切片来协调训练流量，以强制执行单个作业的下限带宽保证；对研究团队测试台的评估表明，GeoOrchestra 的吞吐量比最先进的基准提高了 1.6 倍至 1.8 倍，同时在现实世界的共享 WAN 争用下保持稳定的执行。
  - 相较对 2,000 公里跨 DC 测试台的经验测量表明，硬件不匹配、组合搜索复杂性和共享网络争用的相互作用为异构训练带来了严重的性能瓶颈，核心创新是GeoOrchestra 是一个将资源过滤与细粒度策略搜索分离的系统；通过计算和内存配置文件抽象计算节点，同时将 WAN 链路建模为虚拟硬管道，GeoOrchestra 将并行策略搜索问题解构为三个级联阶段。
  - AI 集群网络与大模型系统、LLM Systems、Network Measurement/Telemetry、Scheduling/Orchestration、Scheduling for ML Training Clusters

- [Dynamic Compute and Network Orchestration for Disaggregated RL](https://dl.acm.org/doi/10.1145/3789240.3829124)
  - Xin Tan, Yicheng Feng (The Chinese University of Hong Kong), Yu Zhou, Yimin Jiang, Yibo Zhu (StepFun), Hong Xu (The Chinese University of Hong Kong)
  - 强化学习中的生成阶段和训练阶段的分解被广泛采用来扩展 LLM 的后期训练；这里有两个关键挑战；首先，由于动态工作负载变化和严重的执行不平衡，生成阶段常常成为瓶颈。该工作设计 Silverstone 来动态协调分解 RL 中的计算和网络；Silverstone 采用自适应计算调度程序，可调整并行配置，以匹配生成步骤内和跨生成步骤不断变化的工作负载特征；Silverstone 采用名为 RFabric 的可重构光电结构：它利用光路交换机按需重新配置拓扑的聚合层和核心层，根据训练、生成和权重同步各个阶段的独特通信模式定制带宽资源；使用高保真模拟器，研究团队还表明 RFabric 比静态 Fat-Tree 网络实现了大规模的卓越性能成本效率。
  - 相较首先，由于动态工作负载变化和严重的执行不平衡，生成阶段常常成为瓶颈，核心创新是该工作设计 Silverstone 来动态协调分解 RL 中的计算和网络；Silverstone 采用自适应计算调度程序，可调整并行配置，以匹配生成步骤内和跨生成步骤不断变化的工作负载特征。
  - AI 集群网络与大模型系统、LLM Systems、Optical Interconnect、Scheduling/Orchestration、Scheduling for ML Training Clusters

- [Understanding Host Network Stack Latency](https://dl.acm.org/doi/10.1145/3789240.3829115)
  - Tianyu Zuo (University of Virginia), Jaehyun Hwang (Sungkyunkwan University), Ao Tang, Rachit Agarwal (Cornell University), Qizhe Cai (University of Virginia)
  - 该工作用细粒度测量分解 Linux host network stack 的毫秒级尾延迟，发现主要瓶颈不在 packet processing，而在 CPU scheduler 对处理时间的错误归因、CPU runtime 公平性抽象的限制，以及不可预测到包时的 interrupt tuning。针对这三点修正后，吞吐基本不变而性能最高提高 5.3 倍。
  - 相较直接绕过 Linux 、改用 userspace stack 或专用硬件，核心创新是将尾延迟根因定位到 CPU 调度与 host–NIC 交互。
  - 可编程数据平面与云网络、Network Measurement/Telemetry、Failure Diagnosis、Scheduling/Orchestration、Host Networking & Packet Processing

- [Don't Stall Me Now: Hiding Memory Latency in eBPF](https://dl.acm.org/doi/10.1145/3789240.3829175)
  - Farbod Shahinfar, Marco Molè (Politecnico di Milano), Aurojit Panda (NYU), Gianni Antichi (Politecnico di Milano & Queen Mary University of London)
  - eBPF 已成为构建高性能 I/O 程序的流行平台；然而，eBPF 的编程模型限制了常用性能优化的使用，使程序容易受到缓存未命中引起的性能开销的影响。该工作设计一种解决这两个限制的蜂蜡方法；这种方法要求程序员采用多阶段数据结构并将程序划分为多个阶段；它与程序阶段的执行重叠，从而隐藏了缓存未命中开销；该工作设计该方法，以便它可以应用于现有程序，而无需进行重大更改；研究发现吞吐量提高了高达 99%。
  - 相较eBPF 的编程模型限制了常用性能优化的使用，使程序容易受到缓存未命中引起的性能开销的影响，核心创新是该工作设计一种解决这两个限制的蜂蜡方法；这种方法要求程序员采用多阶段数据结构并将程序划分为多个阶段；它与程序阶段的执行重叠，从而隐藏了缓存未命中开销；该工作设计该方法，以便它可以应用于现有程序，而无需进行重大更改。
  - 可编程数据平面与云网络、Caching/CDN、Host Networking & Packet Processing

- [PacketExpress: Fully Exploiting Large MTUs for Internet Traffic in Private Networks](https://dl.acm.org/doi/10.1145/3789240.3829113)
  - Junghan Yoon (Seoul National University), Youngmin Choi (KAIST), Juyoung Park (Seoul National University), Daehyeok Kim (The University of Texas at Austin), Changhoon Kim (Unaffiliated), KyoungSoo Park (Seoul National University)
  - 网络带宽继续快速扩展，但互联网数据传输性能仍然受到传统 1500 B MTU 的限制；这种较小的 MTU 将高带宽转化为高数据包速率，从而使中间盒和终端主机的 CPU 处理变得紧张。PacketExpress 是一种数据包处理架构，使网络能够利用大型 MTU 来处理 Internet 流量，而无需修改相邻网络；网络边界的 MTU 转换网关动态地将传入的小数据包聚合为较大的数据包，以便进行高效处理，然后在外部转发时将其分段；其原型通过 8 个 CPU 核心实现了 1.47 Tbps 的吞吐量，同时将超过 90% 的 1500 B 数据包转换为 9000 B 数据包，将中间盒性能提高了 5.1 倍，将终端主机性能提高了 2.5 倍。
  - 相较传统 1500 B MTU 的限制，核心创新是PacketExpress 是一种数据包处理架构，使网络能够利用大型 MTU 来处理 Internet 流量，而无需修改相邻网络；网络边界的 MTU 转换网关动态地将传入的小数据包聚合为较大的数据包，以便进行高效处理，然后在外部转发时将其分段。
  - 可编程数据平面与云网络、Host Networking & Packet Processing

- [Honey, I Shrunk the Headers With Flow.ZIP](https://dl.acm.org/doi/10.1145/3789240.3829104)
  - Yinda Zhang (University of Pennsylvania), Liangcheng Yu (Microsoft Research), Gianni Antichi (Politecnico di Milano & Queen Mary University of London), Ran Ben Basat (University College London and Broadcom), Vincent Liu (University of Pennsylvania)
  - 包头开销是包交换网络效率低下的一个持久根源，它会降低吞吐量并增加网络负载；隧道挖掘等趋势进一步增加了这种开销，显著影响了流程完成时间；该工作设计 Flow.zip，这是一种专为现有数据中心网络设计的向后兼容的 header 压缩机制。其解决方案结合了最后一跳网络卸载和 MPLS 支持，这两者在现代数据中心部署中都很普遍；Flow.zip 通过有选择地、智能地协调流子集的压缩，克服了这些组件中的可扩展性限制；这样一来，Flow.zip 可将实际数据中心工作负载的平均流程完成时间缩短 58%。
  - 相较隧道挖掘等趋势进一步增加了这种开销，显著影响了流程完成时间，核心创新是该工作设计 Flow.zip，这是一种专为现有数据中心网络设计的向后兼容的 header 压缩机制；其解决方案结合了最后一跳网络卸载和 MPLS 支持，这两者在现代数据中心部署中都很普遍。
  - 可编程数据平面与云网络、Compression/Encoding、Host Networking & Packet Processing

- [Simplifying Prioritization and Scheduling with P2CS](https://dl.acm.org/doi/10.1145/3789240.3829173)
  - Ali Munir, Xiaolin Pang, Junyi Zhang (Huawei Technologies Co., Ltd.)
  - 现代数据中心网络承载着各种服务和工作负载，具有不同的服务质量 (QoS) 要求，但仍受到硬件限制；最值得注意的是，商用交换机中可用的物理优先级队列数量较少；该工作设计 P2CS（基于优先级的概率拥塞信令），这是一种轻量级且可扩展的方法，仅使用单个 FIFO 队列即可实现细粒度的流量优先级排序。P2CS 结合了优先级感知概率拥塞信令、优先级感知数据包丢弃和简单的交换机端仲裁，以强制执行跨流的优先级；对代表性工作负载（包括多租户 ML 训练、HPC 和混合喷射/ECMP 流量）的评估表明，P2CS 实现了与网络内机制相当的性能，同时显著降低了复杂性和成本。
  - 相较现代数据中心网络承载着各种服务和工作负载，具有不同的服务质量 (QoS) 要求，但仍受到硬件限制，核心创新是该工作设计 P2CS（基于优先级的概率拥塞信令），这是一种轻量级且可扩展的方法，仅使用单个 FIFO 队列即可实现细粒度的流量优先级排序；P2CS 结合了优先级感知概率拥塞信令、优先级感知数据包丢弃和简单的交换机端仲裁，以强制执行跨流的优先级。
  - 可编程数据平面与云网络、Scheduling/Orchestration、Host Networking & Packet Processing

- [STORM: Enabling Traffic Scheduling for RDMA](https://dl.acm.org/doi/10.1145/3789240.3829117)
  - Jichun Wu (University of Cambridge), Ran Shu (Microsoft Research), Gianni Antichi (Politecnico di Milano & Queen Mary University of London), Yongqiang Xiong (Microsoft Research), Jon Crowcroft, Andrew Moore (University of Cambridge)
  - 远程直接内存访问 (RDMA) 越来越多地用作跨数据中心工作负载的共享通信基础，这些工作负载具有非常不同的调度需求，从请求响应服务和存储扇出到 AI 训练集合；适当的请求调度可以减少通信时间，但实际上，数据中心中没有启用 RDMA 流调度，从而使流量进行简单的公平共享。STORM 是一种 NIC 级调度程序，适用于所有类型的 RDMA 工作负载，使用仅 NIC 信息：已知的 RDMA 请求大小和每个队列对积压；STORM 将这些信号转换为线路上的少量额外优先级，并对接近完成或阻塞排队相关工作的请求进行优先级排序；STORM 不需要应用程序提示，并且可以与有序 RoCEv2 和允许重新排序的较新 RDMA 堆栈配合使用；在代表性的云和 LLM 训练工作负载中，与公平调度相比，STORM 将训练迭代时间减少了高达 12%，并将平均和 P99 流程完成速度减慢了高达 90%。
  - 相较适当的请求调度可以减少通信时间，但实际上，数据中心中没有启用 RDMA 流调度，从而使流量进行简单的公平共享，核心创新是STORM 是一种 NIC 级调度程序，适用于所有类型的 RDMA 工作负载，使用仅 NIC 信息：已知的 RDMA 请求大小和每个队列对积压；STORM 将这些信号转换为线路上的少量额外优先级，并对接近完成或阻塞排队相关工作的请求进行优先级排序。
  - 数据中心网络、传输与互连、LLM Systems、Collective Communication、RDMA、Programmable Network Hardware、Scheduling/Orchestration

- [PSN-PATH: When Multipath RDMA Meets Lossy Networks](https://dl.acm.org/doi/10.1145/3789240.3829128)
  - Zhexiong Li, Shugui Wei, Puyu Zhao, Feifan Wang, Yuepeng Li (China University of Geosciences), Lin Gu (Huazhong University of Science and Technology), Deze Zeng (China University of Geosciences), Xiaoliang Wang (Nanjing University), Laiping Zhao (Tianjin University)
  - 远程直接内存访问 (RDMA) 广泛应用于高性能数据中心工作负载，但其严格的排序要求与有损网络中的多路径传输相冲突；RDMA 网络接口卡 (RNIC) 可能会将由不同路径延迟引起的无序 (OOO) 到达解释为数据包丢失。PSN-PATH 是一种新颖的 RDMA 协议，用于区分数据包丢失和 OOO 并避免不必要的重传，从而提高有损网络中多路径 RDMA 的吞吐量和 FCT；PSN-PATH 将数据包序列号 (PSN) 映射到网络路径，使接收器能够验证每个映射路径内的数据包连续性，并区分实际丢失和 OOO 到达；PSN-PATH 仅重传丢失的数据包并将流量重定向远离降级路径；实验结果表明，PSN-PATH 显著优于现有解决方案，在高负载、有损条件下，FCT 降低了 95.81%，吞吐量提高了 5.11 倍，重传率降低了 99% 以上。
  - 相较远程直接内存访问 (RDMA) 广泛应用于高性能数据中心工作负载，但其严格的排序要求与有损网络中的多路径传输相冲突，核心创新是PSN-PATH 是一种新颖的 RDMA 协议，用于区分数据包丢失和 OOO 并避免不必要的重传，从而提高有损网络中多路径 RDMA 的吞吐量和 FCT。
  - 数据中心网络、传输与互连、RDMA、Programmable Network Hardware、Formal Verification、Datacenter Transport: RDMA & Congestion Control

- [InfiniFlow: Decoupling Virtual Channel Scalability from Buffer Requirements in Lossless Datacenter Networks](https://dl.acm.org/doi/10.1145/3789240.3829135)
  - Zerui Tian, Sen Liu, Minkun Xue, Hao Shangguan, Ruyi Yao, Hao Mei, Deli Huang, Songchen Xue, Yang Xu (Fudan University)
  - 现代数据中心越来越依赖远程直接内存访问 (RDMA) 来实现高吞吐量和低延迟；为了确保无损传输，RDMA 结构在虚拟通道 (VC) 粒度上采用逐跳流量控制；现有方法试图通过增加 VC 的数量来提高隔离性，但需要为每个 VC 保留缓冲区，导致缓冲区需求随 VC 的数量线性扩展，并从根本上限制了 VC 的可扩展性。InfiniFlow 是一种基于信用的逐跳流量控制方法，通过每端口缓冲区共享以有限的缓冲区预算支持大量 VC；InfiniFlow 引入了缓冲区管理的范式转变：上游为下游分配缓冲区 (UABD)，其中，对于每个链路，上游调度程序维护每个端口的共享信用池，并向 VC 动态分配信用；InfiniFlow 在 UABD 的基础上进一步整合了缓冲区使用控制协议，该协议使用实时积压反馈强制执行每个 VC 的动态信用阈值，以限制信用消耗并防止缓冲区垄断；广泛的 NS-3 模拟表明，InfiniFlow 在实际工作负载下实现了接近最佳的流量完成时间，而不依赖于缓慢的端到端速率自适应，优于先前的逐跳流量控制方法和最先进的拥塞控制方案。
  - 相较现有方法试图通过增加 VC 的数量来提高隔离性，但需要为每个 VC 保留缓冲区，导致缓冲区需求随 VC 的数量线性扩展，并从根本上限制了 VC 的可扩展性，核心创新是InfiniFlow 是一种基于信用的逐跳流量控制方法，通过每端口缓冲区共享以有限的缓冲区预算支持大量 VC；InfiniFlow 引入了缓冲区管理的范式转变：上游为下游分配缓冲区 (UABD)，其中，对于每个链路。
  - 数据中心网络、传输与互连、RDMA、Programmable Network Hardware、Congestion Control、Scheduling/Orchestration

- [Odin: Rethinking Congestion Control under All-to-All Traffic](https://dl.acm.org/doi/10.1145/3789240.3829164)
  - Wanchun Jiang, Yujie Hu, Kai Wang, Xiao Han (School of Computer Science and Engineering, Central South University, Changsha, China), Haoran Wei, Yong Zhang, Jianxi Ye, Huichen Dai (ByteDance)
  - 多对多（A2A）通信主导着大型语言模型的训练和推理时间，尤其是在专家混合（MoE）架构下，专家调度会产生密集的并发流；研究观察到 A2A 流量持续在交换机上建立大量的总缓冲区占用率 (TBO)；如果没有意识到这些问题，现有的 CC 算法很容易在 TBO 较大时触发 PFC，导致拥塞响应无效，并导致吞吐量损失。基于这些见解，研究团队建议 Odin 增强 A2A 流量下的 CC；Odin 根据交换机级 TBO 信号抑制大的 TBO，主动分配入口带宽以消除速率膨胀，并对入口-出口匹配进行带宽补偿；实验和模拟表明，Odin 在 A2A 流量下实现了低 TBO 和高吞吐量，加速了训练过程。
  - 相较现有的 CC 算法很容易在 TBO 较大时触发 PFC，导致拥塞响应无效，并导致吞吐量损失，核心创新是基于这些见解，研究团队建议 Odin 增强 A2A 流量下的 CC；Odin 根据交换机级 TBO 信号抑制大的 TBO，主动分配入口带宽以消除速率膨胀，并对入口-出口匹配进行带宽补偿。
  - 数据中心网络、传输与互连、LLM Systems、MoE、Collective Communication、Congestion Control、Network Measurement/Telemetry

- [CSIG: Congestion Signaling for Datacenter Transports](https://dl.acm.org/doi/10.1145/3789240.3829179)
  - Abhiram Ravi, Nandita Dukkipati, Weiwu Pang, Neal Cardwell (Google), Brad Karp (Google and UCL), Mohammad Jafar Akhbarizadeh, Weida Huang, Konstantinos Prasopoulos, Kok Kiong Yap, Arjun Singh, Amin Vahdat (Google)
  - 优化突发性的数据中心工作负载需要细粒度的网络控制和可见性；CSIG 是一种通过固定长度的以太网 header 提供精确的多位瓶颈拥塞信号的协议。该架构捕获细粒度交换机指标，例如可用带宽，并使用带内线速操作将它们发送给终端主机；研究团队通过在五代商用交换机硬件（高达 102.4 Tbps）、四代 NIC 和五种传输堆栈中验证 CSIG 的广泛可部署性。
  - 官方摘要未展开更细的直接基线；可核验的核心创新是CSIG 是一种通过固定长度的以太网 header 提供精确的多位瓶颈拥塞信号的协议；该架构捕获细粒度交换机指标，例如可用带宽，并使用带内线速操作将它们发送给终端主机。
  - 数据中心网络、传输与互连、Congestion Control、Network Measurement/Telemetry、Datacenter Transport: RDMA & Congestion Control

- [Towards High-Performance Intrusion Detection with Robustness Guarantees on Programmable Switches at ISP Scale](https://dl.acm.org/doi/10.1145/3789240.3829107)
  - Han Zhang, Xuefeng Liu, Linqiang Qian (Tsinghua University), Guyue (Grace) Liu (Peking University), Tianyu Zhang, Kaiyang Zhao, Yantu Tong, Zeji Xiao (Tsinghua University), Dongbiao He (Sangfor Technologies Inc), Yahui Li (Tsinghua University), Ke Ruan (China Telecom), Jilong Wang (Tsinghua University), Yongqing Zhu (Institute of Network Technology & China Telecom Corporation Limited Research Institute), Xia Yin (Tsinghua University)
  - 为了提供与企业园区站点的安全连接，互联网服务提供商正在网络层提供全面的入侵检测服务；然而，现有的网络入侵检测系统（NIDS）对于高速网络保护，特别是对于加密流量分析来说，要么效果不佳，要么效率低下。该工作设计并实现了 SiteGuard，这是一种内联网络入侵检测系统，带有可编程交换机，专门用于保护连接到 ISP 的企业园区站点；SiteGuard 提出了一种双平面特征提取模型，以近线速提取广泛的流量特征；SiteGuard 还提出了一种轻量级的一类解耦式模型，专门针对良性流量训练最佳参数，以识别恶意流量；此外，SiteGuard 引入了在线更新机制，旨在根据环境变化动态调整检测模型；生产与测试平台评估表明 SiteGuard 可以在几分钟内以大约 90% 的准确度检测恶意流量。
  - 相较现有的网络入侵检测系统（NIDS）对于高速网络保护，特别是对于加密流量分析来说，要么效果不佳，要么效率低下，核心创新是该工作设计并实现了 SiteGuard，这是一种内联网络入侵检测系统，带有可编程交换机，专门用于保护连接到 ISP 的企业园区站点；SiteGuard 提出了一种双平面特征提取模型，以近线速提取广泛的流量特征。
  - 网络验证、管理与安全、Programmable Network Hardware、Security/Privacy、Security, Privacy & Networked Systems

- [Zero-Knowledge Cloud Analytics](https://dl.acm.org/doi/10.1145/3789240.3829157)
  - Zeying Zhu, Clarence Lam, Alexander Frolov, Ian Miers, Zaoxing Liu (University of Maryland)
  - 该工作设计 zk-Analytics，这是一种分布式云分析系统，可实现可公开验证的分析，而无需泄露原始日志或依赖于分析提供商基础设施中的可信硬件。当今的云分析在很大程度上是自我主张的：提供商收集遥测数据、执行聚合并报告结果，使得外部各方在无法访问敏感数据或可信执行环境的情况下无法验证正确性；zk-Analytics 通过使用轻量级仅附加日志承诺以及使用零知识证明的可验证聚合和查询执行来增强分析管道，从而解决了这一差距；该系统将在线日志提交与离线、分布式批量聚合和查询验证完全分开，从而实现可扩展性，同时保持较低的在线开销；研究使用基于 zkVM 的执行环境实现 zk-Analytics，并在现实世界和合成工作负载上对其进行评估，证明可验证、保护隐私的云分析对于现实世界的云工作负载是可行的。
  - 官方摘要未展开更细的直接基线；可核验的核心创新是该工作设计 zk-Analytics，这是一种分布式云分析系统，可实现可公开验证的分析，而无需泄露原始日志或依赖于分析提供商基础设施中的可信硬件。
  - 网络验证、管理与安全、Network Measurement/Telemetry、Formal Verification、Security/Privacy、Security, Privacy & Networked Systems

- [DeepSFU: Scalable Deepfake Detection for Video Conferencing](https://dl.acm.org/doi/10.1145/3789240.3829184)
  - Tuan Tran, Shirin Ebadi, S. M. H. Hosseini, Woongsub Shin, Evan Ram, Youngwook Son (University of Colorado Boulder), Seyeon Kim (Korea University), Nam Bui (University of Colorado Denver), Kyunghan Lee (Seoul National University), Eric Keller, Sangtae Ha (University of Colorado Boulder)
  - Deepfake 已成为在线通信的重大威胁，在视频通话期间几乎无法区分高管、公众人物和可信联系人的冒充行为；虽然最先进的 Deepfake 检测模型可以离线实现高精度，但将它们部署在实时视频会议系统中仍然具有挑战性：增加的计算很快就会超出交互延迟预算，并极大地限制可扩展性。DeepSFU 是一种新颖的视频会议架构，可将可扩展的 Deepfake 检测作为本机功能；DeepSFU 通过直接检测编码视频比特流上的异常来减少每帧开销，避免昂贵的高分辨率视频解码和繁重的检测模型推理；对大规模测试台的深入评估表明，DeepSFU 将每帧处理延迟降低了 143.7 倍，转化为会议容量提高了 26.2 倍，同时为所有参与者提供连续的 Deepfake 检测。
  - 相较虽然最先进的 Deepfake 检测模型可以离线实现高精度，但将它们部署在实时视频会议系统中仍然具有挑战性：增加的计算很快就会超出交互延迟预算，并极大地限制可扩展性，核心创新是DeepSFU 是一种新颖的视频会议架构，可将可扩展的 Deepfake 检测作为本机功能；DeepSFU 通过直接检测编码视频比特流上的异常来减少每帧开销，避免昂贵的高分辨率视频解码和繁重的检测模型推理。
  - 网络验证、管理与安全、RDMA、SmartNIC/DPU、Failure Diagnosis、Security/Privacy、Video/QoE

- [Integrating 2PC with Consensus for Fast Replication](https://dl.acm.org/doi/10.1145/3789240.3829177)
  - Yan Chen (SJTU & Tsinghua University), Xinyi Yu, Shengyun Liu, Ruofan Xiong, Tianjing Xu (SJTU), Yongwei Wu (Tsinghua University), Yiming Zhang (SJTU)
  - xRaft 面向低延迟容错复制：无冲突、无节点/网络故障时，客户端向全部副本广播并用 2PC 在一个 RTT 内完成更新；出现不利执行条件时再切到 consensus 模式容错。评估显示其显著优于现有快速共识协议。
  - 相较让单一 consensus protocol 同时承担快速路径与容错，核心创新是用 2PC 处理正常情况的低延迟复制，仅在需要时进入共识。
  - 分布式系统与网络服务

- [Tuning into the Web: A Low-Cost Access Solution for Developing Countries](https://dl.acm.org/doi/10.1145/3789240.3829209)
  - Ayush Pandey, Rohail Asim (New York University Abu Dhabi (NYUAD)), Jean Louis K. E. Fendji (University of Ngaoundere), Talal Rahwan (New York University Abu Dhabi), Matteo Varvello (Nokia Bell Labs), Yasir Zaki (New York University Abu Dhabi)
  - 到 2026 年，全球仍有超过四分之一的人口无法接入互联网，这主要是由于发展中地区的成本和基础设施有限；随着信息的获取越来越依赖于可靠、高带宽连接的人工智能系统，这种差距变得越来越重要。为此，该工作设计 WebFM，这是一种低成本、可扩展的 Web 和 AI 访问解决方案，它建立在发展中地区广泛部署的基础设施之上：用于下行链路广播的 FM 无线电和用于个性化上行链路的 SMS；先前有关调频网络的工作仅限于模拟、短程实验和无损链接，很大程度上未探索地理引起的信号变化的影响；WebFM 通过多项系统级创新来解决这一差距，以有效地传输 Web 内容，并以可靠和压缩的形式通过 FM 广播声音实现 LLM 互动；其评估显示，下行链路吞吐量持续为 10 kbps，信号强度高于 -90 dBm 的大多数传输损失低于 20%，并且用户在网页浏览和 ChatGPT 交互中的参与度很高。
  - 相较到 2026 年，全球仍有超过四分之一的人口无法接入互联网，这主要是由于发展中地区的成本和基础设施有限，核心创新是为此，该工作设计 WebFM，这是一种低成本、可扩展的 Web 和 AI 访问解决方案，它建立在发展中地区广泛部署的基础设施之上：用于下行链路广播的 FM 无线电和用于个性化上行链路的 SMS。
  - 网络验证、管理与安全、LLM Systems、Compression/Encoding、Security, Privacy & Networked Systems

- [Presto: A Match-Action TCP Stack for the Terabit Era](https://dl.acm.org/doi/10.1145/3789240.3829111)
  - Rajath Shashidhara (University of Washington), Antoine Kaufmann (Max Planck Institute for Software Systems (MPI-SWS)), Simon Peter (University of Washington)
  - Presto 是第一个在可编程可重配置匹配操作表 (RMT) 管道上提供 ASIC 级性能和能效的 TCP 堆栈，在提供灵活性的同时保留了标准 TCP 语义和 POSIX 套接字兼容性。设计 Presto 的关键挑战是将 TCP 复杂的、依赖的状态更新与 RMT 的单向、锁步执行模型相协调；为了克服这一挑战，Presto 引入了三种新颖的技术：乐观并发（下游验证的推测更新）、伪段注入（无停顿的循环依赖解析）和在线碰撞处理（单通道段处理）；这些共同支持 TCP 重传、重组、流量和拥塞控制，作为简单匹配操作操作的管道；最后，Presto 推广到 FPGA SmartNIC，在相同时序下比 Tonic 的单片设计高出 3 倍。
  - 官方摘要未展开更细的直接基线；可核验的核心创新是Presto 是第一个在可编程可重配置匹配操作表 (RMT) 管道上提供 ASIC 级性能和能效的 TCP 堆栈，在提供灵活性的同时保留了标准 TCP 语义和 POSIX 套接字兼容性。
  - 可编程数据平面与云网络、RDMA、SmartNIC/DPU、Programmable Network Hardware、Congestion Control、Video/QoE

- [OBM: Optimal Shared Packet Buffer Management in Switches](https://dl.acm.org/doi/10.1145/3789240.3829188)
  - Dan Mani Binu, Jason Lei, Vishal Shrivastav (Purdue University)
  - 为了更好地利用交换机内存进行数据包缓冲，数据中心交换机中的数据包缓冲区在所有交换机端口之间共享；因此，缓冲区共享算法对于数据中心交换机和网络的性能至关重要；然而，当今的交换机仍然采用 drop-tail 算法，因为以数据中心交换机的线速实现推出操作极具挑战性。OBM 是一种用于管理网络交换机中共享数据包缓冲区的新系统，该系统基于最著名的缓冲区共享在线推出算法（称为最长队列丢弃 (LQD)）；OBM 做出了两项重要贡献；首先，OBM 扩展了经典的 LQD 算法，使其能够感知数据包的准入和推出的优先级，而不牺牲 LQD 的吞吐量保证；其次，OBM 提出了一种新颖的硬件管道和基于树的交换互连，可以以低延迟和低硬件资源使用的线速执行推出操作，从而使基于 LQD 的推出在现代交换机上实现变得切实可行；通过大规模网络仿真，研究团队表明 OBM 不仅显著优于最先进的 drop-tail 和 Push-out 缓冲区管理方案，而且对于单个优先级类别而言，其性能与理想但不切实际的 LQD 的性能相匹配，同时对于多个优先级类别而言，其性能显著优于它。
  - 相较当今的交换机仍然采用 drop-tail 算法，因为以数据中心交换机的线速实现推出操作极具挑战性，核心创新是OBM 是一种用于管理网络交换机中共享数据包缓冲区的新系统，该系统基于最著名的缓冲区共享在线推出算法（称为最长队列丢弃 (LQD)）；OBM 做出了两项重要贡献。
  - 可编程数据平面与云网络、Programmable Network Hardware、Programmable Switches & Data-Plane Hardware

- [Scale-up PIFO: Interleaving Multiple Priority Queues for High Speed Programmable Scheduling](https://dl.acm.org/doi/10.1145/3789240.3829190)
  - Hao Mei, Shili Chen, Xu Chen (Fudan University), Zixuan Chen (China Telecom), Ruyi Yao, Zhiyu Zhang, Hao Wang, Deli Huang, Weiyi Chen (Fudan University), Yibo Fan (State Key Laboratory of ASIC and System, Fudan University), Yang Xu (Fudan University)
  - 推入先出 (PIFO) 提供了统一的抽象，可以在同一硬件上快速部署不同的调度算法；随着 SerDes 通道聚合将端口速率推至 1.6 Tbps，每个数据包的处理预算达到亚纳秒级，使得单队列 PIFO 设计无法跟上；然而，简单的循环并行化会引入大量的调度错误，并且在最坏的情况下，它可能会增长到缓冲区大小的数量级。Scale-up PIFO 是可以扩展吞吐量，同时以硬件友好的方式限制调度错误；关键的观察结果是，当级别相似的数据包集中在单个 PIFO 中时，循环出队机制会错误排序数据包；因此，纵向扩展 PIFO 引入了等级范围负载平衡算法，将等级空间划分为多个范围，将每个范围内的数据包均匀地分布在并行 PIFO 队列中，并根据流量模式动态调整边界；数据包级仿真表明，与之前的近似 PIFO 方案相比，调度错误和短流完成时间 (FCT) 显著减少。
  - 相较简单的循环并行化会引入大量的调度错误，并且在最坏的情况下，它可能会增长到缓冲区大小的数量级，核心创新是Scale-up PIFO 是可以扩展吞吐量，同时以硬件友好的方式限制调度错误；关键的观察结果是，当级别相似的数据包集中在单个 PIFO 中时，循环出队机制会错误排序数据包。
  - 可编程数据平面与云网络、Programmable Network Hardware、Network Measurement/Telemetry、Scheduling/Orchestration、Programmable Switches & Data-Plane Hardware

- [Trie-Structure-Guided Compression, Allocation, and Mapping for Storage-Efficient IPv6 Lookup Pipelines](https://dl.acm.org/doi/10.1145/3789240.3829185)
  - Donghong Jiang, Zhenhao Yuan, Yanbiao Li, Shi Meng (CNIC CAS; UCAS, China), Yuxuan Chen (University of Chinese Academy of Sciences), Taiji Chen (Peking University), Xian Yu (Computer Network Information Center, Chinese Academy of Sciences), Gaogang Xie (CNIC CAS; UCAS, China)
  - IPv6 转发信息库 (FIB) 的快速增长给高速路由器带来了压力；虽然基于 trie 的算法最长前缀匹配 (ALPM) 管道得到了广泛部署，但现有设计强调 trie 压缩，但忽略了管道内存利用率，限制了长 IPv6 前缀和不平衡分布下的可扩展性。该工作设计 SCAMP-Trie，这是一种 trie 结构引导的方法，它联合解决了 trie 压缩、节点映射和管道内存分配问题，以实现存储高效的 IPv6 查找；该工作设计一种基于特里树的管道查找模型（TPLM），它通过统一的存储效率指标捕获这些维度之间的耦合；利用距离叶节点较远的节点出现频率较低的观察结果，该工作设计基于反距离的映射原理，该原理通过基于警告线的动态映射算法和元启发式搜索框架来实现；FPGA 原型通过 240k 条目 FIB 实现 256 字节数据包的 768 Gbps 线速转发，仅使用 41% 的片上内存和 1% 的逻辑。
  - 相较现有设计强调 trie 压缩，但忽略了管道内存利用率，限制了长 IPv6 前缀和不平衡分布下的可扩展性，核心创新是该工作设计 SCAMP-Trie，这是一种 trie 结构引导的方法，它联合解决了 trie 压缩、节点映射和管道内存分配问题，以实现存储高效的 IPv6 查找。
  - 可编程数据平面与云网络、Programmable Network Hardware、Network Measurement/Telemetry、Compression/Encoding、Scheduling/Orchestration

- [Capybara: Dynamic Load Balancing with Microsecond-Scale TCP Migration](https://dl.acm.org/doi/10.1145/3789240.3829197)
  - Inho Choi (National University of Singapore), Nimish Wadekar (ETH Zürich), Guangda Sun (National University of Singapore), Raj Joshi (Red Hat / Harvard University), Joshua Fried, Omar S. Navarro Leija (University of Pennsylvania), Dan R. K. Ports, Irene Zhang (Microsoft Research), Jialin Li (National University of Singapore)
  - 第 4 层负载均衡器是解决高尾延迟的流行解决方案，但在不可预测的倾斜工作负载下表现不佳，因为它们静态地将连接分配到服务器。Capybara 是一种新的负载均衡器架构，可以动态重新平衡已建立的连接；Capybara 将负载均衡职责划分为快速 L4 负载均衡器、主机交换机共同设计的连接迁移协议以及用于应用程序级连接状态迁移的传输接口；Capybara 利用可编程交换机和内核旁路这两种趋势，在不中断的情况下高效地实现连接迁移，同时保持对客户端的透明度；在实际工作负载下，与最先进的负载平衡方法相比，Capybara 的尾部延迟降低了 149 倍，横向扩展服务的吞吐量提高了 2 倍以上。
  - 相较第 4 层负载均衡器是解决高尾延迟的流行解决方案，但在不可预测的倾斜工作负载下表现不佳，因为它们静态地将连接分配到服务器，核心创新是Capybara 是一种新的负载均衡器架构，可以动态重新平衡已建立的连接；Capybara 将负载均衡职责划分为快速 L4 负载均衡器、主机交换机共同设计的连接迁移协议以及用于应用程序级连接状态迁移的传输接口。
  - 可编程数据平面与云网络、Programmable Network Hardware、Programmable Switches & Data-Plane Hardware

- [CommSAR: Enabling Bidirectional Communication in SAR Imaging Satellites via Shared Waveform](https://dl.acm.org/doi/10.1145/3789240.3829144)
  - Yimin Zhao (Shanghai Jiao Tong University), Zhenning Li (Aerospace Information Research Institute, Chinese Academy of Sciences), Hao Pan (Shanghai Jiao Tong University), Hua Li (Aerospace Information Research Institute, Chinese Academy of Sciences), Minhao Cui (Seoul National University), Jie Xiong (Nanyang Technological University), Yihai Wei, Yang Liu, Haonan Zhao, Mohan Zhang (Aerospace Information Research Institute, Chinese Academy of Sciences), Weibo Wang, Guihai Chen (Shanghai Jiao Tong University), Kaiyu Liu (Aerospace Information Research Institute, Chinese Academy of Sciences), Linghe Kong (Shanghai Jiao Tong University)
  - 近地轨道 (LEO) 合成孔径雷达 (SAR) 卫星通常依赖于专用通信链路，随着卫星星座规模的扩大，这会带来过高的硬件、频谱和功率开销；CommSAR 是一种新颖的系统，可重用现有的 SAR 成像波形以实现双向通信，而无需修改卫星硬件或影响成像性能。对于下行链路，通过调制成像波形的起始频率偏移来嵌入数据，保留波形结构和成像质量；实验结果表明，CommSAR 保持了成像性能而不降低，同时下行链路和上行链路数据速率分别高达 105 kbps 和 112 kbps，显著优于现有技术并展示了实用级性能。
  - 相较近地轨道 (LEO) 合成孔径雷达 (SAR) 卫星通常依赖于专用通信链路，随着卫星星座规模的扩大，这会带来过高的硬件、频谱和功率开销，核心创新是CommSAR 是一种新颖的系统，可重用现有的 SAR 成像波形以实现双向通信，而无需修改卫星硬件或影响成像性能；对于下行链路，通过调制成像波形的起始频率偏移来嵌入数据，保留波形结构和成像质量。
  - 卫星、海洋与非地面网络、Satellite/LEO、Cellular/RAN、Wireless/Sensing、Satellite & Non-Terrestrial Networks

- [Planet-Scale IoT Connectivity via LEO Satellites](https://dl.acm.org/doi/10.1145/3789240.3829147)
  - Ziyue Zhang, Xianjin Xia, Ruonan Li, Jinhong Liu, Yuanqing Zheng (The Hong Kong Polytechnic University), Linghe Kong (Shanghai Jiao Tong University), Mo Li (HKUST)
  - 直接到低地轨道卫星 (DtS) 被广泛吹捧为全球物联网连接的途径，但其实际性能仍然不透明。研究使用世界上最大的卫星物联网网络之一进行首次大规模、野外的 DtS 测量；研究结果推翻了一个普遍的看法：DtS 容量并不是紧迫的问题；相反，今天的 DtS 受到低吞吐量、长尾延迟和能源可持续性差等问题的阻碍，这些问题从根本上限制了实际采用；研究团队查明了这些瓶颈背后的架构和协议级原因，揭示了当今 DtS 设计中的系统效率低下；研究团队通过测试台实验和实时生产部署验证了重新设计的协议，证明吞吐量提高了 2.1 倍，长尾延迟减少了 52%，能源减少了 38%。
  - 相较直接到低地轨道卫星 (DtS) 被广泛吹捧为全球物联网连接的途径，但其实际性能仍然不透明，核心创新是研究使用世界上最大的卫星物联网网络之一进行首次大规模、野外的 DtS 测量；研究结果推翻了一个普遍的看法：DtS 容量并不是紧迫的问题；相反，今天的 DtS 受到低吞吐量、长尾延迟和能源可持续性差等问题的阻碍，这些问题从根本上限制了实际采用。
  - 卫星、海洋与非地面网络、Network Measurement/Telemetry、Satellite/LEO、Satellite & Non-Terrestrial Networks

- [Dissecting the StarLink: Characterizing Queuing and Flow Dynamics in the Starlink Network](https://dl.acm.org/doi/10.1145/3789240.3829162)
  - Hendrik Cech (Technical University of Munich), Nitinder Mohan (TU Delft), Jörg Ott (Technical University of Munich)
  - 星链已成为最大的商业低地球轨道卫星网络，但对其内部队列管理和带宽分配机制知之甚少；之前的测量研究已经记录了性能变化，但缺乏解释根本原因的粒度。研究团队首次展示了星链传输行为的微观特征，使用来自多个终端的受控测量来以微秒精度捕获每个数据包的动态；其分析揭示了一些以前未记录的机制；Starlink 采用头丢弃队列而不是尾丢弃队列，下行链路和上行链路的容量分别约为 1500 个和 4000 个数据包；带宽分配是由需求驱动的，从下行链路和上行链路 100/30 Mbps 的基线开始，当流量承受队列压力时，该基线在 400 毫秒内增加 3.4×/2×。
  - 相较之前的测量研究已经记录了性能变化，但缺乏解释根本原因的粒度，核心创新是研究团队首次展示了星链传输行为的微观特征，使用来自多个终端的受控测量来以微秒精度捕获每个数据包的动态；其分析揭示了一些以前未记录的机制。
  - 卫星、海洋与非地面网络、Network Measurement/Telemetry、Satellite/LEO、Scheduling/Orchestration、Satellite & Non-Terrestrial Networks

- [Achieving Efficient Storage and Communication via Collaboration](https://dl.acm.org/doi/10.1145/3789240.3829176)
  - Ruichen Li, Yufan Wu, Zhengyi Hu, Sheng-Jyun Cai, Lang Wei, Qifan Yang, Ting Zhu (The Ohio State University)
  - 由 Planet、Google 和 Amazon 等组织运营的地球观测 (EO) 星座每天生成数百 TB 的图像；然而，有限的下行链路带宽阻碍了即时数据传输，迫使卫星在卫星上存储大量图像，并且经常在下行链路之前覆盖有价值的数据；现有的 EO 管道独立处理每次捕获，无法利用 EO 星座中自然存在的大量冗余。为了解决这些低效率问题，该工作设计 CoOrbit，这是一种协作式 EO 系统，通过仅保留已更改和非重叠区域来节省机载存储；CoOrbit 结合了轻量级机载嵌入差分、基于 TLE 的重叠推理和自适应参考嵌入规划；研究团队通过应用驱动的设计进一步扩展了 CoOrbit，允许卫星仅下行传输与应用相关的图块，以实现更高的效率；其评估还显示，当应用野火驱动设计时，性能进一步降低了一个数量级。
  - 相较现有的 EO 管道独立处理每次捕获，无法利用 EO 星座中自然存在的大量冗余，核心创新是该工作设计 CoOrbit，这是一种协作式 EO 系统，通过仅保留已更改和非重叠区域来节省机载存储；CoOrbit 结合了轻量级机载嵌入差分、基于 TLE 的重叠推理和自适应参考嵌入规划。
  - 卫星、海洋与非地面网络、Network Measurement/Telemetry、Satellite/LEO、Satellite & Non-Terrestrial Networks

- [Improving Evaluation of Heterogenous Congestion Control Algorithm Interactions](https://dl.acm.org/doi/10.1145/3789240.3829156)
  - Ranysha Ware (Swarthmore College), Haochen Zhang (Tsinghua University), Isabel Suizo, Srinivasan Seshan, Justine Sherry (Carnegie Mellon University)
  - 该工作面向新旧 CCA 共存评估：Mahak 用新公平性指标和实验收敛判定器统一自动测试，HarmGen 再用遗传算法搜索交互最差的网络配置与 workload。同样 300 次实验预算下，HarmGen 优于爬山与随机搜索，并接近 3500 次参数扫描找到的高伤害值。
  - 相较不一致的手工参数扫描，核心创新是把可比的公平性度量、自动收敛判断与敌对式搜索组成同一 CCA 共存测试流程。
  - 互联网架构、路由与流量控制、Congestion Control、Congestion, Rate & Schedule Control

- [Forewarned is Forearmed: A Responsive Congestion Control with Non-intrusive Uplink Dynamics Capture](https://dl.acm.org/doi/10.1145/3789240.3829143)
  - Mu Wang, Yiying Lin, Shenghui Wei (Beijing University of Posts and Telecommunications), Enhuan Dong, Kang Chen (Tsinghua University), Tong Li (Renmin University of China), Yinchao Zhang (Tsinghua University), Renjie Xie (Guilin University of Electronic Technology), Su Yao, Ke Xu (Tsinghua University), Changqiao Xu (Beijing University of Posts and Telecommunications)
  - 蜂窝上行链路对于现代应用越来越重要，但由于高度动态的条件和复杂的操作，给拥塞控制算法（CCA）带来了重大挑战；现有的 CCA 范例主要用于下载数据，无法对上行链路波动做出及时反应，因为它们依赖于 ACK 来指示拥塞，从而引入了不可避免的控制循环延迟。该工作设计 Aether，主要包括：（1）部署在驱动层的监视器，利用其关键发现（驱动缓冲区动态作为上行链路拥塞的指标）来捕获上行链路动态； (2) 瓶颈检测器，当上行链路成为瓶颈时激活 Aether； (3) 速率控制器，将传输引导至上行链路容量；研究团队在商业设备上实现了 Aether，并开发了一个跟踪驱动的模拟器来测试 Aether；广泛的评估表明，Aether 的性能优于最先进的方案，将平均吞吐量提高了 9.28% 至 234.11%，同时持续将延迟降低了 5.34% 至 56.94%。
  - 相较现有的 CCA 范例主要用于下载数据，无法对上行链路波动做出及时反应，因为它们依赖于 ACK 来指示拥塞，从而引入了不可避免的控制循环延迟，核心创新是该工作设计 Aether，主要包括：（1）部署在驱动层的监视器，利用其关键发现（驱动缓冲区动态作为上行链路拥塞的指标）来捕获上行链路动态； (2) 瓶颈检测器，当上行链路成为瓶颈时激活 Aether； (3) 速率控制器，将传输引导至上行链路容量。
  - 互联网架构、路由与流量控制、Congestion Control、Network Measurement/Telemetry、Cellular/RAN、Wireless/Sensing

- [Queueless and Dropless Rate Control](https://dl.acm.org/doi/10.1145/3789240.3829202)
  - Ammar Tahir (University of Illinois Urbana-Champaign), Yongzhou Chen (University of Illinois, Urbana-Champaign), Radhika Mittal (UIUC)
  - QLDL 面向云游戏和会议的瞬时码率突发：ISP 端 token-bucket policer 按平均速率执行套餐上限，端点与 policer 之间的轻量显式速率控制在不排队的同时避免 policer 丢包。WebRTC 原型较 SOTA 实现 2 倍码率、2–3 倍更低帧延迟和 20 倍更少卡顿。
  - 相较用固定容量物理队列吸收视频突发，核心创新是利用 ISP 人工限速瓶颈的可编程性，以 policer 加端点速率反馈同时消除排队和丢包。
  - 互联网架构、路由与流量控制、Congestion Control、Network Measurement/Telemetry、Video/QoE、Congestion, Rate & Schedule Control

- [Credit-Guided Congestion Control on Wafer-Scale On-Chip Networks for Molecular Dynamics](https://dl.acm.org/doi/10.1145/3789240.3829210)
  - Tao Jiang (Institute of Computing Technology, Chinese Academy of Sciences), Shixiong Qi (University of Kentucky), Zhan Wang, Ning Kang, Fan Yang (Institute of Computing Technology, Chinese Academy of Sciences), Yuanzhe Wang (University of Chinese Academy of Sciences), Zejun Li, Guanglei Chen, Jing Xu, Wenzhe Li, Guangming Tan, Guojun Yuan (Institute of Computing Technology, Chinese Academy of Sciences)
  - 分子动力学 (MD) 是科学计算的基石，但强扩展常常在高并行性下崩溃，因为通信是突发性的并且对尾部延迟高度敏感；MD 通过重复固定的时间步循环（力计算和状态更新的一次迭代）来进步，性能很大程度上取决于时间步完成的速度。该工作设计 WaveCC，一种信用引导的运行时，可以动态调整小波注入以适应瞬时织物压力；WaveCC 利用路由器信用（无损 WSC 结构中的本机背压信号），无需修改路由器微架构；在粗粒度上，WaveCC 使用阶段级信用统计来适应阶段边界的全局步幅；在细粒度上，它使用信用梯度在突发窗口内塑造每个 PE 的喷射注入；在微基准测试和跟踪驱动的评估中，WaveCC 可以显著减少平均和尾部通信完成时间，并提高时间步吞吐量。
  - 相较现有的小波调度依赖于静态步幅，随着条件的发展，该步幅要么过度注入（触发信用背压），要么过度节流（浪费带宽），核心创新是该工作设计 WaveCC，一种信用引导的运行时，可以动态调整小波注入以适应瞬时织物压力；WaveCC 利用路由器信用（无损 WSC 结构中的本机背压信号），无需修改路由器微架构；在粗粒度上，WaveCC 使用阶段级信用统计来适应阶段边界的全局步幅。
  - 互联网架构、路由与流量控制、Congestion Control、Scheduling/Orchestration、Congestion, Rate & Schedule Control

- [Harvest: Adaptive Photonic Switching Schedules for Collective Communication in Scale-up Domains](https://dl.acm.org/doi/10.1145/3789240.3829166)
  - Mahir Rahman, Samuel Joseph, Nihar Kodkani (Purdue University), Behnaz Arzani (Microsoft), Vamsi Addanki (Purdue University)
  - 随着芯片到芯片硅光子因其带宽和能源效率而受到关注，其电路交换特性提出了集体通信的一个基本问题：何时以及如何重新配置互连以实现这些优势；建立直接光路可以减少拥塞和传播延迟；然而，每次重新配置都会产生不可忽略的开销，使得简单的每步重新配置变得不切实际。Harvest 是一种用于综合拓扑重新配置时间表的系统方法，可最大限度地减少光子互连中的集体完成时间；给定集体通信算法及其固定的通信时间表，Harvest 确定互连在集体过程中应如何发展，明确平衡重新配置延迟与拥塞和传播延迟；通过使用数据包级和流级评估以及商用 GPU 上的硬件仿真，研究团队表明，与静态互连和重新配置每一步基线相比，Harvest 合成的调度显著缩短了多个集体算法的集体完成时间。
  - 相较建立直接光路可以减少拥塞和传播延迟；然而，每次重新配置都会产生不可忽略的开销，使得简单的每步重新配置变得不切实际，核心创新是Harvest 是一种用于综合拓扑重新配置时间表的系统方法，可最大限度地减少光子互连中的集体完成时间；给定集体通信算法及其固定的通信时间表，Harvest 确定互连在集体过程中应如何发展，明确平衡重新配置延迟与拥塞和传播延迟。
  - 互联网架构、路由与流量控制、Collective Communication、Optical Interconnect、Scheduling/Orchestration、Congestion, Rate & Schedule Control

- [Nüwa: A Generative Control Plane for AI Network Simulation](https://dl.acm.org/doi/10.1145/3789240.3829106)
  - Wenkai Li (Xi'an Jiaotong University), Ran Shu (Microsoft Research Asia), Peng Zhang (Xi'an Jiaotong University), Yiren Zhao (University of Toronto), Danfeng Shan (Xi'an Jiaotong University), Yongqiang Xiong (Microsoft Research Asia)
  - 网络仿真对于提高大规模人工智能集群的设计验证、参数调整和协议开发的效率起着至关重要的作用；然而，高保真网络模拟在规模上变得极其缓慢，尤其是在使用数万或数十万个加速器的拓扑上运行大批量实验时；现有的网络模拟器通常在初始化时计算路由并安装转发表，这可能会在数据包事件执行开始之前消耗数百 GB 内存并限制总体模拟吞吐量。Nüwa 是将路由视为一个编译问题，它利用 AI 结构中常见的分层和对称结构，并将声明性拓扑描述和路由策略编译成紧凑的转发工件，这些工件可以快速生成且高效查找；评估表明，对于 65,536 个 GPU 集群，Nüwa 可以将模拟初始化时间从数小时缩短至仅 25 秒；对于端到端仿真时间，Nüwa 只需要 40K 以上 GPU 集群中现有方法所需时间的 20%，并且 Nüwa 可以扩展到 221,184 个 GPU 集群。
  - 相较之前消耗数百 GB 内存并限制总体模拟吞吐量，核心创新是Nüwa 是将路由视为一个编译问题，它利用 AI 结构中常见的分层和对称结构，并将声明性拓扑描述和路由策略编译成紧凑的转发工件，这些工件可以快速生成且高效查找。
  - AI 集群网络与大模型系统、Network Measurement/Telemetry、Internet Routing

- [EMA: Efficient Model Adaptation for Learning-based Systems](https://dl.acm.org/doi/10.1145/3789240.3829142)
  - Daiyang Yu, Xinyu Chen, Yihan Zhang (University of Illinois Urbana Champaign), Yan Liang (The Hong Kong University of Science and Technology), Yaqi Qiao (University of Illinois Urbana Champaign), Fan Lai (University of Illinois Urbana-Champaign)
  - 机器学习 (ML) 越来越多地应用于优化资源管理和网络模拟等任务中的系统性能；与传统的机器学习任务（例如图像分类）不同，网络系统通常在异构、长时间运行和动态的环境状态下运行，其中输入条件（例如网络负载）和操作目标可能随着时间和设置的不同而变化；现有的基于学习的系统对适应的支持很少，导致模型训练成本高昂、数据收集广泛、系统性能下降和响应缓慢。EMA 是第一个支持基于学习的系统的模型适应系统，以最小的运营开销适应不断变化的环境；EMA 采用系统驱动、以数据为中心的方法，可适应不同的系统和模型设计，同时解决两个关键的部署挑战；对七个代表性的基于学习的系统的评估表明，EMA 将适应成本（例如 GPU 训练时间）降低了 14.9-42.4%，同时将系统性能（例如网络吞吐量）提高了 6.9-31.3%。
  - 相较现有的基于学习的系统对适应的支持很少，导致模型训练成本高昂、数据收集广泛、系统性能下降和响应缓慢，核心创新是EMA 是第一个支持基于学习的系统的模型适应系统，以最小的运营开销适应不断变化的环境；EMA 采用系统驱动、以数据为中心的方法，可适应不同的系统和模型设计，同时解决两个关键的部署挑战。
  - 网络测量、诊断与可观测性

- [RepLLM: Toward Automatically Reproducing Network Research Results](https://dl.acm.org/doi/10.1145/3789240.3829170)
  - Yining Jiang, Yunxin Xu, Wenyun Xu, Yufan Zhu, Rui Liu, Tangtang He, Haiying Huang, Letian Zhu, Qingyu Song, Qiang Su, Lizhao You, Lu Tang (Xiamen University), Wanjian Feng (Yealink), Yuchao Zhang (Beijing University of Posts and Telecommunications), Linghe Kong (Shanghai Jiaotong University), Qiao Xiang (Xiamen University), Jiwu Shu (Xiamen University, Tsinghua University)
  - RepLLM 从论文内容自动复现网络系统代码：Content Parsing、Architecture Design、Code Generation、Audit & Repair 四类 Agent 通过共享记忆保持长文语义一致，在隔离 sandbox 中结合静态检查和动态调试，把编译或运行错误反馈给修复阶段。对顶会论文的实验中约两小时可复现 95% 原始 benchmark，并减少最多 10% token 消耗。
  - 相较单轮代码生成或缺少全局上下文的通用 coding Agent，核心创新是按系统复现生命周期分工，并以共享记忆和静态—动态验证闭合“读论文—搭架构—写代码—修错误”循环。
  - 网络验证、管理与安全、Agent for Systems、LLM Systems

- [Artic: AI-oriented Real-time Communication for MLLM Video Assistant](https://dl.acm.org/doi/10.1145/3789240.3829189)
  - Jiangkai Wu, Zhiyuan Ren, Junquan Zhong, Liming Liu, Xinggong Zhang (Peking University)
  - Artic 面向云端 MLLM 观看实时视频的工作负载：响应能力感知 ABR 在模型准确率饱和后主动限码率、为带宽波动留余量，context-aware streaming 则把码率给最影响回答的画面区域；另有 benchmark 衡量 RTC 退化对 MLLM 理解的影响。真实上行 trace 中，准确率提高 15.12%，延迟降低 135.31 ms。
  - 相较以人类视觉 QoE 为目标的 RTC，核心创新是直接用 MLLM 响应饱和度与语义相关区域驱动码率和带宽分配。
  - 视频、实时通信与 QoE、LLM Systems、Network Measurement/Telemetry、Video/QoE

- [Critical Path Guided Decision Making with CALLIGATOR](https://dl.acm.org/doi/10.1145/3789240.3829103)
  - Meghna Pancholi (Columbia University), Lee Baugh (Open AI), Olaf Schnapauff, David Culler (Google), Kostis Kaffes (Columbia University), Yu Gan, Brent Stephens (Google)
  - CALLIGATOR 输入微服务 distributed traces，推断显式执行依赖并计算精确 critical path 与 p99 指标；依赖图驱动 retiming 式 what-if 预测和尾延迟瓶颈分析，再用于对冲策略调优和资源分配。其延迟预测精度较 SOTA 提高 81.7%，DeathStarBench 等资源下 p99 最高降低 94.7%。
  - 相较只提供局部微服务指标的工具，核心创新是把 trace 恢复的执行依赖、临界路径和 what-if 重定时结合成可操作的尾延迟决策工具。
  - 互联网架构、路由与流量控制、Cloud/Distributed Systems

- [GGN: Experiences in Designing and Deploying the Next-Generation Google Global Network](https://dl.acm.org/doi/10.1145/3789240.3829114)
  - Mohammad Al-Fares, Anees Shaikh, Arjun Muralidharan, Bikash Koley, Charith Wickramaarachchi, Chi-Yao Hong, Jonathan Zolla, Min Zhu, Namrata Kadam, Priya Mahadevan, Subhasree Mandal, Rob Shakir, Aman Shaikh, Arda Balkanay, Arjun Singh, Dennis Fetterly, Nachikethas A. Jagadeesan, Richard Alimi, Sankalp Singh, Warren Martins (Google)
  - 云和 AI/ML 工作负载对广域网提出了前所未有的新要求：它必须结合严格的可用性、大规模增长和功能敏捷性；越来越明显的是，传统的广域网设计无法适应这些要求。结果展示 Google 的全球网络 (GGN)，这是对 WAN 进行重大架构重新设计，将 B2 和 B4 发展为单一、模块化且高度可用的软件定义网络；该架构围绕三个支柱进行设计：（1）具有明确定义的 API 的功能域模块化设计； (2) 用于故障隔离和水平扩展的物理分片和区域化核心； (3) 基于开放标准的与供应商无关的硬件策略；该工作总结 GGN 的多年部署历程，包括安全、主机引导的迁移策略，并展示其提高网络可用性和故障反应时间的能力，为全球范围内的现代 WAN 奠定基础。
  - 相较传统的广域网设计无法适应这些要求，核心创新是结果展示 Google 的全球网络 (GGN)，这是对 WAN 进行重大架构重新设计，将 B2 和 B4 发展为单一、模块化且高度可用的软件定义网络；该架构围绕三个支柱进行设计：（1）具有明确定义的 API 的功能域模块化设计。
  - 互联网架构、路由与流量控制

- [Achieving Network Efficiency Through Service Collaborative Capacity Sharing and Enforcement](https://dl.acm.org/doi/10.1145/3789240.3829163)
  - Vinayak Dangui (Meta), Guyue (Grace) Liu (Peking University), Alaleh Razmjoo, Guanqing Yan, Mahesh Nayak, Mansi Babbar, Brian Bierig, Tejas Birajdar, Prabhakaran Ganesan, Lilian Liu, Matt Maia, Jerry Yang, Shrinivas Petale (Meta), Satyajeet Singh Ahuja, Abhinav Triguna (Meta Platforms, Inc), Ying Zhang (Meta)
  - 该工作面向 Meta backbone 在光纤、空间和电力受限时的容量利用：“safe capacity”将当前/预测网络状态暴露给计算与存储分配，hose-carving 把服务需求转为细粒度 traffic matrix，rate card 归因各服务的网络消耗，端主机执行器在运行时调整资源和流量。
  - 相较只通过扩容或网络内部 TE 管理骨干网，核心创新是让业务共享容量状态、承担可归因的网络成本，并参与端到端容量执行。
  - 互联网架构、路由与流量控制、Scheduling/Orchestration

- [Verifying Non-Deterministic Convergence on a Global Production WAN](https://dl.acm.org/doi/10.1145/3789240.3829180)
  - Xing Fang (Xiamen University), Fangdan Ye, Yifei Yuan (Alibaba Group), Zhongyu Guan (Alibaba Cloud), Duncheng She (Alibaba Group), Xiaobo Zhu (Alibaba Cloud), Qiao Xiang (Xiamen University)
  - TianYan 验证同一 WAN 配置可能收敛到不同 data plane 的情况：它利用容错组内路由器的路由相似性，将分析的指数复杂度从路由器数降为组数。阿里云全球生产 WAN 一年部署发现约 2% 前缀存在非确定性收敛，并将结果回馈给仿真配置验证器。
  - 相较假设配置只会产生单一收敛 data plane 的仿真验证，核心创新是按路由相似性分组压缩非确定收敛空间。
  - 网络验证、管理与安全、Formal Verification、Internet Routing

- [AIDA: Accelerating Root Cause Analysis for Multi-Vendor Device Failures with LLM-Powered Reasoning](https://dl.acm.org/doi/10.1145/3789240.3829126)
  - Haoran Xu (Sun Yat-sen University and Alibaba Cloud), Xuan Zeng, Xumiao Zhang (Alibaba Cloud), Xiaoxi Zhang (Sun Yat-sen University), Yang Lv, Peng Zhang (Alibaba Cloud), Deke Guo (Sun Yat-sen University), Ennan Zhai (Alibaba Cloud)
  - AIDA 面向多厂商网络设备已知发生故障后“为什么失败”的细粒度 RCA：先用强化学习微调 LLM 蒸馏专家推理链，再把链条持续合成知识图谱，运行时由 RAG 按图谱顺序引导多步推理并输出可解释证据。阿里云一年以上部署达到 95.4% precision，中位诊断时间从 72.6 小时降至 1.6 分钟。
  - 相较粗粒度 ML/LLM 分类或依赖大量手工规则，核心创新是将专家逻辑、演化知识图谱和受检索约束的多步推理串成可核验诊断链；系统不直接执行网络变更。
  - 网络测量、诊断与可观测性、LLM for Systems、LLM Systems、Failure Diagnosis、Formal Verification

- [Comprehensive Revocation Checking at Scale: the Deployment of CRLite in Mozilla Firefox](https://dl.acm.org/doi/10.1145/3789240.3829108)
  - Nehal Fooda (University of Maryland), James Larisch (Cloudflare), John Schanck (Mozilla), Tijay Chung (Virginia Tech), Dave Levin (University of Maryland), Bruce Maggs (Duke University and Emerald Innovations), Christo Wilson (Northeastern University)
  - CRLite 在 Firefox 中用分区 Ribbon filter 下发 TLS 证书撤销状态，并同步 Certificate Transparency log 以消除误报；论文总结从研究原型到广泛部署的七年数据结构、CA 撤销实践和浏览器同步改造。Firefox opt-in telemetry 显示有效覆盖率 87.8%，在真实大规模撤销事件中仍保持中等带宽开销。
  - 相较在线 OCSP 查询或不完整的本地列表，核心创新是用可分区概率结构与 CT 严格同步，以适中带宽实现隐私、低延迟和全证书撤销检查。
  - 网络验证、管理与安全、Network Measurement/Telemetry、Security/Privacy

- [Rethinking Transparent TCP Replacement: Practical Lessons from SMC-R in the Cloud](https://dl.acm.org/doi/10.1145/3789240.3829194)
  - Jingxuan Li, Wen Gu, Wei Shi, Yang Lu, Guangguan Wang, Lie Lu, Yong Yang, Jinhu Li (Alibaba Cloud), Teng Ma (Alibaba Group), Tao Ma (Alibaba Cloud)
  - 透明 TCP 加速多年来一直是广泛学术研究的主题，旨在绕过内核开销而不修改遗留应用程序；然而，之前的工作主要强调理想化设置下的性能，并且对实际生产环境中成本和收益如何体现进行了有限的讨论。在过去的四年里，研究团队在阿里云内部署并评估了 SMC-R，以加速一般云工作负载；其经验表明，透明的 TCP 替换在实践中远非“直接”进行；现有生态系统的整合障碍和破坏会带来巨大的隐性成本。
  - 相较之前的工作主要强调理想化设置下的性能，并且对实际生产环境中成本和收益如何体现进行了有限的讨论，核心创新是在过去的四年里，研究团队在阿里云内部署并评估了 SMC-R，以加速一般云工作负载；其经验表明，透明的 TCP 替换在实践中远非“直接”进行；现有生态系统的整合障碍和破坏会带来巨大的隐性成本。
  - 数据中心网络、传输与互连、Failure Diagnosis

- [Planogram: A Multi-dimensional Physical Location Planning System for DC Networks](https://dl.acm.org/doi/10.1145/3789240.3829195)
  - Richard Cziva, Alexander Mafusalov, Shrinivas Petale, Varun Gupta, Abhinav Triguna, Jason Wilson, Manikantan KR, Susana Contrera, Jimmy Williams, Alexey Andreyev, Tian Fang, Satyajeet Singh Ahuja, Ying Zhang (Meta Platforms, Inc)
  - Meta 的数据中心支撑着大量的互联网服务，并且由于人工智能工作负载的快速扩张而面临着前所未有的需求；构建标准化数据中心的传统方法日益受到所需容量呈指数增长的挑战，而这些容量现在源自各种非标准物理环境和数据中心设计；这种转变带来了一个复杂的挑战：如何快速、可重复地设计定制数据中心网络，以平衡不同工程学科中多个常常相互冲突的目标。作为回应，Planogram 是一种用于 DC 网络的物理位置映射框架；Planogram 自动化了将逻辑网络实体映射到物理数据中心平面图的传统手动且耗时的过程；通过摄取逻辑网络、物理约束的 DC 模板和一组设计目标，Planogram 利用整数线性规划和强化学习来生成完全映射的平面图；研究团队在 Planogram 方面的生产经验已经设计了多个数据中心区域，这表明设计时间大大缩短，同时提高了设计质量和跨网络段和区域的一致性。
  - 相较这种转变带来了一个复杂的挑战：如何快速、可重复地设计定制数据中心网络，以平衡不同工程学科中多个常常相互冲突的目标，核心创新是Planogram 是一种用于 DC 网络的物理位置映射框架；Planogram 自动化了将逻辑网络实体映射到物理数据中心平面图的传统手动且耗时的过程。
  - 数据中心网络、传输与互连

- [Gryphon: Scaling Hyperscale Multi-Tenant Gateways Beyond the Petabit-Era via DPU-Augmented Hierarchical Co-Offloading](https://dl.acm.org/doi/10.1145/3789240.3829119)
  - Yuemeng Xu (Peking University), Haoran Chen (ByteDance), Jiarui Guo (Peking University), Mingwei Cui (ByteDance), Qiuheng Yin (Peking University), Cheng Dong, Peng He, Chenmin Sun (ByteDance), Yangyujia Wang (Peking University), Daxiang Kang, Xian Wu, Yang Gao, Lirong Lai, Kai Wang (ByteDance), Zhuochen Fan, Tong Yang (Peking University), Hongyu Wu (ByteDance)
  - 在字节跳动，云网关集群负责编排 PB 级聚合流量；由于严格的片上资源限制和有限的可编程灵活性，传统的纯 ASIC 网关无法满足这些不断增长的需求，而纯软件解决方案或分解式 SmartNIC 等替代方案则难以满足太比特级线速吞吐量。为了弥补这一差距，Gryphon 是一种基于混合架构构建的超大规模云网关，可将 DPU 直接集成到交换 ASIC 的转发路径中；该设计解决了容量和速度之间的根本矛盾，将表规模扩展至 1000 倍并增强了可编程性，同时维持 1.6 Tbps 线速吞吐量，而额外平均延迟仅为约 8 μs；研究团队还分享生产测量和运营经验，作为下一代 DPU 增强云网关的第一个经过超大规模验证的指南。
  - 相较传统的纯 ASIC 网关无法满足这些不断增长的需求，而纯软件解决方案或分解式 SmartNIC 等替代方案则难以满足太比特级线速吞吐量，核心创新是Gryphon 是一种基于混合架构构建的超大规模云网关，可将 DPU 直接集成到交换 ASIC 的转发路径中；该设计解决了容量和速度之间的根本矛盾，将表规模扩展至 1000 倍并增强了可编程性。
  - 可编程数据平面与云网络、SmartNIC/DPU、Network Measurement/Telemetry、Scheduling/Orchestration
