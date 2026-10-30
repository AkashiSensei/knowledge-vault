# 系统顶会方向分析

[报告目录](../README.md)

研究和分析 2024-2026 系统领域顶会的整体研究方向及其变化趋势，在完整观察各会议论文主题分布的基础上，重点分析 AI Infra、Agent System 等与 AI 相关方向的演进，而非预先从会议中筛选特定论文。

**对象说明约定**：技术路线首次出现时，写明“具体对象或负载＋主要做法”：学习负载区分大语言模型（LLM）、视觉语言模型（VLM）、文生图/视频扩散模型、图神经网络（GNN）、推荐模型等，并说明训练、微调或推理阶段；其他系统写明内核、文件系统、数据库事务、网络传输或内存管理等对象。方法使用的模型与实际优化对象分别说明，通用方法与已评测负载也不混同；材料不足时注明待确认。AI/ML 等宽泛名称仅用于汇总分类，不代表某一种模型或规模。

## 会议名录

CCF 等级统一采用[《中国计算机学会推荐国际学术会议和期刊目录》第七版（2026 年）](https://www.ccf.org.cn/Academic_Evaluation/By_category/)（[正式版目录全文，浙江工商大学图书馆提供](https://lib.zjgsu.edu.cn/_upload/article/files/f5/b1/f4f7201343b88c0f10564f590ebe/854a3c68-36a6-4698-a359-5184d5e30a0c.pdf)）。MLSys 未列入该版目录；USENIX ATC 在该版目录中以“ACM SIGOPS ATC（原 USENIX ATC）”列为 CCF-A，本报告保留所分析年份的会议名称。

### 核心名录

| 会议      | CCF 等级 | 英文全称                                                            | 主要方向                                                                   |
| ------- | ------ | --------------------------------------------------------------- | ---------------------------------------------------------------------- |
| MLSys   | 未列入    | Conference on Machine Learning and Systems                      | 机器学习与系统交叉；涵盖机器学习训练与推理、分布式与联邦学习、系统优化、调度、编译器、运行时、数据处理、专用硬件和 Agent System |
| OSDI    | CCF-A  | USENIX Symposium on Operating Systems Design and Implementation | 系统软件的设计、实现与实践；涵盖操作系统、分布式与云系统、存储、网络、资源管理、可靠性、安全和机器学习系统                  |
| SOSP    | CCF-A  | ACM Symposium on Operating Systems Principles                   | 计算机系统软件的原理与实践；涵盖操作系统、分布式系统、存储、并发、资源管理、正确性、可靠性、安全和机器学习系统                |
| EuroSys | CCF-A  | ACM European Conference on Computer Systems                     | 综合计算机系统；涵盖操作系统、分布式系统、云与边缘计算、网络、存储、资源管理、嵌入式系统和机器学习系统                    |
| NSDI    | CCF-A  | USENIX Symposium on Networked Systems Design and Implementation | 网络化与分布式系统；涵盖网络服务、云系统、分布式存储、资源管理、虚拟化、测量诊断、安全和面向机器学习的网络系统                |
| FAST    | CCF-A  | USENIX Conference on File and Storage Technologies              | 广义存储系统；涵盖存储设备、文件系统、分布式存储、缓存、内存层次、数据管理、可靠性、性能以及 AI 与存储的交叉               |
| ICDCS   | CCF-B  | IEEE International Conference on Distributed Computing Systems  | 分布式计算系统；涵盖分布式算法、云边计算、分布式操作系统与中间件、容错、存储、数据库、安全和分布式 AI/ML 系统             |
| SoCC    | CCF-B  | ACM Symposium on Cloud Computing                                | 云计算系统与云数据管理；涵盖集群管理、多租户、资源隔离、弹性伸缩、Serverless、云存储、分布式应用和云上机器学习           |

### 备选名录

| 会议 | CCF 等级 | 英文全称 | 主要方向 |
| --- | --- | --- | --- |
| ASPLOS | CCF-A | ACM International Conference on Architectural Support for Programming Languages and Operating Systems | 体系结构、编程语言与操作系统及其交叉；涵盖软硬件协同、云与分布式系统、存储、异构平台、性能分析和机器学习系统 |
| PPoPP | CCF-A | ACM SIGPLAN Symposium on Principles and Practice of Parallel Programming | 并行与高性能程序设计；涵盖并行理论、语言、编译器、运行时系统、工具、应用和实践经验 |
| SC | CCF-A | International Conference for High Performance Computing, Networking, Storage and Analysis | 高性能计算、网络、存储与分析；涵盖算法、应用、体系结构、系统软件、大规模部署、性能和 AI/ML |
| HPDC | CCF-A | ACM International Symposium on High-Performance Parallel and Distributed Computing | 高性能并行与分布式计算；涵盖高端计算系统的设计、实现、评估和应用 |
| SIGMETRICS | CCF-B | ACM International Conference on Measurement and Modeling of Computer Systems | 计算机系统的设计、测量、建模和性能分析；涵盖网络、云、ML 系统、资源分配、调度和可靠性 |
| SIGCOMM | CCF-A | ACM SIGCOMM Conference | 通信网络与网络化系统；涵盖网络体系结构、协议、实现、运行、测量、资源管理、可靠性和安全 |
| USENIX ATC | CCF-A | USENIX Annual Technical Conference | 综合且偏实践的系统研究，涉及云、分布式系统、存储、网络、性能和运维；2025 年后终止，本轮只分析最后一届 2025 |

## 各会议研究方向分析

分析各个会议以及整体上的研究方向，以及其变化趋势。重点关注 Agent System 相关内容。

### 整体

本报告最终覆盖 39 个“会议—年份”列表、3,354 篇论文。各年的会议集合并不完全相同：2024 年尚未纳入 HPDC、SIGMETRICS、SC、SIGCOMM 和 USENIX ATC，2025 年覆盖全部 15 个会议，2026 年因 ATC 已终止而覆盖 14 个会议；此外，部分 2026 会议采用截至当前的官方 program 快照。因此，年度论文总数适合描述本报告的覆盖规模，不能直接当作领域论文产量的同比指标。

| 年份   | 覆盖会议数 |   论文数 | 观察边界                      |
| ---- | ----: | ----: | ------------------------- |
| 2024 |    10 |   747 | 核心名录 8 个会议，加 ASPLOS、PPoPP |
| 2025 |    15 | 1,188 | 核心与备选名录全部覆盖；ATC 为最后一届     |
| 2026 |    14 | 1,419 | 除已终止的 ATC 外全部覆盖；部分为当前官方快照 |

#### 2024

2024 年的 LLM 系统主线是先让模型“放得下、跑得动、扩得开”。MLSys、ASPLOS、OSDI、EuroSys 和 PPoPP 围绕已有模型与机制展开优化：用低比特量化（用更少位数表示数值）压缩权重、降低访存量；对 KV Cache（历史 token 的注意力键/值缓存）做关键 token 保留、前缀复用和 CPU–GPU 卸载，减少显存占用与重复计算；让不同 LoRA adapter（低秩微调适配器）共享基础模型并混合批处理；压缩 MoE（混合专家模型）的专家权重并配套设计高效执行 Kernel（设备上的计算内核）；通过并行切分、通信与计算重叠、编译优化和算子融合加速训练与推理。例如，[Keyformer](evidence/venue-catalogs/MLSys-2024.md#keyformer)通过保留关键 token 缩减 KV Cache。多数论文仍把模型、训练 job、GPU 或单个 serving engine 作为优化单元。经典系统主题——分布式一致性、存储与 I/O、网络协议、隔离、可靠性和安全——仍占各综合会议主体。

Agent 尚未成为稳定论文簇。与 LLM 有关的系统工作更多是 LLM serving，或用 LLM 辅助生成配置、代码和数据；它们可能为 Agent 提供底层能力，但通常既不研究“规划—行动—反馈”的 Agent 机制，也不针对多步 Agent workflow 设计基础设施。

#### 2025

2025 年 LLM 系统的重心从单算子和单模型效率，扩展到在线服务的完整资源路径。研究者将 prefill/decode（输入处理/逐 token 生成）分开部署并分别配置算力，对 prefix/KV Cache 做跨请求复用、分层存储和按需迁移，按负载调整异构 GPU 上的模型与 adapter/expert 放置，并优化长上下文和推测解码的执行与资源分配。例如，[BlitzScale](evidence/venue-catalogs/OSDI-2025.md#blitzscale)通过 GPU 间参数传输和逐层接管计算加快弹性扩容，缩短负载突增时的等待。研究方法也从离线静态配置转向由请求长度、队列、显存、带宽和 SLO（如响应延迟上限等服务目标）驱动的在线准入、路由和再调度，同时约束质量、成本、吞吐与尾延迟。

Agent 相关工作开始从零散案例变为可辨认的四类交叉：一类直接改进 Agent 的规划、记忆或反馈；一类承载多轮、分支或多 Agent workflow；一类让 Agent 闭环执行网络运维、故障诊断、配置或代码任务；还有一类只用 LLM 生成或解释系统对象。SIGCOMM 的 Confucius 等生产系统说明 Agent for Systems 已能进入真实运维流程，但从全部系统论文看，Agent 仍是新兴而非主导方向。

#### 2026

2026 年 LLM 与 Agent 系统最明显的变化是决策粒度继续下沉：从 job、模型和 GPU，细化到单请求、token、KV block、expert、layer、通信 collective、流水线 stage、工具调用和 workflow DAG。相应方法包括按 token/expert 的实际负载重新分配任务，按状态的访问与复用需求决定 KV block 的存放和搬运，将计算、通信与 I/O 流水重叠，并结合性能模型和在线反馈联合调整并行、放置与资源分配。LLM 训推研究由此共同考虑计算、显存、存储、网络、能耗、故障与跨地域容量，同时通过故障定位、状态保存与恢复降低长任务中断的代价。

Agent Infra 也成为显式研究对象：通过上下文与前缀复用减少重复计算，让上下游 Agent 的生成与输入处理流水重叠，并用分布式队列、背压和重试机制支撑大量并发工作流。[FlashAgents](evidence/venue-catalogs/MLSys-2026.md#flashagents)和[Matrix](evidence/venue-catalogs/MLSys-2026.md#matrix)分别体现了跨 Agent 流水与去中心化执行这两类方法。相比之下，系统会议中的 Agent System 仍较少：这些会议更常研究如何可靠、高效地承载 Agent，或让 Agent 完成系统任务，而规划算法、反思机制和通用智能体能力本身更多留在 AI/NLP 会议。与此同时，LLM for Systems 与 Agent for Systems 在配置、根因分析、形式化、代码生成和科学工作流中快速增加，是否具有可执行动作和反馈验证成为区分两者的关键。

#### 变化

三年的共同演进可以概括为三条。第一，研究对象从“训练或推理一个模型”扩展到“管理持续变化的在线 AI 服务与多阶段工作流”；第二，优化从单层局部加速走向模型结构、runtime、调度、存储和网络的跨层协同；第三，生成式 AI 从被系统承载的 workload，进一步成为系统管理方法，并反过来产生 Agent-specific infrastructure 的新需求。

对本项目最有价值的观察范围因此不是传统操作系统或体系结构本身，而是四条相互连接的路径：训练与推理 runtime，GPU/网络/存储资源调度，面向长上下文和多步 workflow 的 Agent Infra，以及用 LLM/Agent 完成诊断、配置、优化和科学计算任务的自治系统。阅读具体论文时需要保持四分类边界：支持 Agent 的通用 LLM serving 不自动算 Agent Infra，使用 LLM 的系统工具不自动算 Agent for Systems，传统 RL/MARL 也不因使用“agent”一词而进入生成式 Agent 类别。

#### 当前研究版图：热点、进展与前沿

下面主要概括 LLM 及生成式 Agent 的系统研究：哪些方向已有成熟做法，哪些正在快速发展，哪些刚成为新问题；通用方法也可用于其他 AI 模型。

| 阶段   | 主要研究目标                                                                                       |
| ---- | -------------------------------------------------------------------------------------------- |
| 2024 | 先让 LLM 放得下、跑得动。低比特压缩、算子加速、显存节省和基本推理服务是主要问题。                                                  |
| 2025 | 开始关注真实在线服务：如何同时处理更多请求，同时控制延迟、成本和服务质量。调度、缓存和不同型号 GPU 的混合使用明显增多。                               |
| 2026 | 研究对象从“一次模型调用”扩展到“一个完整 AI 任务”。一个任务可能多次调用模型和外部工具，中途等待、分支、失败或重试，因此 Agent 的调度、状态、存储和可靠性开始成为明确方向。 |

三年的主线可以概括为：从追求“一次模型调用更快”，逐步转向“整个 AI 任务更便宜、稳定、可恢复”。底层加速仍然重要，但研究边界正在向上层的完整服务扩展。

##### 主要方向已经做到什么程度

| 方向 | 已经做到的程度 | 当前前沿 | 所处阶段 |
|---|---|---|---|
| LLM 训练系统 | 把训练任务拆到多张 GPU 的常见方法已经成熟；一边计算一边通信、定期保存训练状态和故障恢复也已有大量工作。 | 超长上下文、只激活部分专家模块的 MoE 模型、模型训练完成后的强化学习、不同型号 GPU 共同工作，以及集群变动或故障时不停止训练。 | 成熟且持续发展，资源门槛高 |
| LLM 在线推理 | 请求持续进出同一批次、按小块管理显存、KV Cache（生成过程中的中间状态）管理、输入和生成阶段分开执行、量化和“先用小模型猜、再用大模型验证”等做法已有成熟系统。 | 在实时负载下联合决定用哪个模型、哪类 GPU、保留哪些状态，并同时考虑质量、延迟、成本和故障。 | 最热也最拥挤 |
| LLM/Agent 存储与数据通路 | 模型参数、KV Cache 和检查点已能在 GPU、CPU 内存和 SSD 之间搬运；相同输入前缀也已能被复用。 | 系统不再只看“数据有多少”，而开始判断它属于哪个任务、是否过期、能否跨分支复用，以及失败后如何恢复。 | 快速发展 |
| LLM 训练与服务集群网络 | 多张 GPU 之间的同步通信、高速远程内存传输，以及根据网络结构安排训练已是主流方法。 | 数万乃至十万张 GPU 的网络、光互连、网内通信加速，以及跨机架或跨数据中心搬运 KV 和模型状态。 | 快速发展，硬件门槛高 |
| Agent System（研究 Agent 本身如何思考和行动） | 在系统顶会中数量仍少；规划、记忆和推理算法更常出现在 AI 或自然语言处理会议。 | 如何让 Agent 更准确地理解环境、选择工具、利用反馈并评估长期任务。 | 早期探索，但不是系统会议的主体 |
| Agent Infra（支撑 Agent 运行的平台） | 已出现第一批工作流运行平台、上下文管理、多 Agent 调度、工具执行、日志和文件回退系统。 | 如何管理长期状态、动态分支、工具等待、外部操作的影响，以及失败后的重放和恢复。目前还没有统一的运行模型和评测方法。 | 刚形成的前沿 |
| Agent for Systems（让 Agent 操作和优化系统） | 已能在一些范围清楚的任务中完成“生成方案—执行—检查—修正”，例如优化算子、生成配置、完成系统证明或诊断故障。 | 权限限制、安全执行、独立验证、失败回退和跨系统泛化。通用的自动运维 Agent 还远未成熟。 | 早期但升温很快 |
| 可靠性、安全与可观测性 | 传统系统已有成熟的故障恢复、隔离和监控方法，正在被移入 AI 训练、推理和 Agent 系统。 | 追踪一次失败究竟来自模型、数据、工具还是平台；保证结果可复现；在 Agent 产生不正确外部操作时可以阻止或回退。 | 明显升温 |
| 能源与成本 | 已能测量 GPU、整机和数据中心的能耗，并将电价、碳排和散热加入调度。 | 将模型质量、请求延迟、电力限制和跨地区容量一起管理，而不是只降低单次运行能耗。 | 稳定升温 |

##### 哪些基本做法已经比较成熟

“成熟”不等于“方向过时”，而是说某些做法已经从新研究问题变成新系统默认应有的基础能力：

- 在线推理中，请求持续进出同一批次、基本的 KV Cache 复用与搬运、输入和生成阶段分开处理，都已有成熟的现成系统。
- 在压缩与算子中，只报告更低的位数或单个算子的加速已很难说明整个服务真的变好。
- 在训练中，传统的数据、模型和流水线并行已是基础；新问题更多来自新模型、不同类型硬件的混合使用、资源变动和故障。
- 用 LLM 一次性总结日志、生成配置或代码已经很常见；前沿正在转向实际执行、独立检查结果，并根据失败继续修正。
- 通用云调度、普通缓存替换和只在模拟器中评估的强化学习调度，都已有很多研究。新工作需要说明 AI 或 Agent 带来了什么过去不存在的问题。

因此，目前很少有整个大方向真的“被研究透了”。更准确的说法是：只在固定负载、同一种硬件和简单指标下重复优化，已经显得陈旧；但这些方向遇到新模型、新硬件、多步任务和可靠性要求时，又会出现新问题。

##### 目前最前沿的变化

1. 系统管理的单位正在从单个模型或请求，变成一个会分支、等待工具和反复修正的完整任务。
2. 缓存和存储不再只关心数据大小，而要知道数据属于哪个任务、是否过期、能否安全复用。
3. 调度开始同时考虑模型、GPU、内存、存储、网络和电力，而不再只优化其中一层。
4. AI 系统的目标正在从“正常时跑得快”，扩展到“出错时能找到原因、恢复状态并保证结果可信”。
5. Agent 正在从生成建议的助手，变成可以实际操作系统的执行者；因此权限、验证、审计和回退也成为核心问题。

整体上，大模型推理和训练系统已经形成成熟而拥挤的主战场；AI 存储、网络、成本与可靠性处于快速扩展期；Agent Infra、可验证的 Agent for Systems 和 Agent 可靠性则刚形成稳定的研究问题。系统领域当前最明显的前沿，不是单纯让一次模型调用更快，而是让一个长时间、多步骤、会操作外部系统的 AI 任务变得可管理、可恢复和可信。

##### 对方向选择的简短提示

- 大模型训练和推理资料最多、产业需求也最明确，但竞争强，通常需要更多 GPU 和更完整的工程系统。
- AI 存储、状态管理、可靠性和可观测性处于扩展期，既能与真实系统问题结合，又不一定依赖超大规模集群。
- Agent Infra 和可验证的 Agent for Systems 更接近新前沿，机会较多，但标准做法和评测方法尚未稳定，不确定性也更高。
- 大规模网络、底层算子和新硬件同样是前沿，但对硬件、底层开发和实验规模的要求最高。
- 如果关心的是 Agent 本身如何规划、记忆和推理，主要研究阵地更偏向 AI 和自然语言处理会议；系统会议更关心如何承载 Agent，以及如何让 Agent 安全地操作系统。

### MLSys

#### 2024

论文列表：[MLSys 2024 完整论文列表](evidence/venue-catalogs/MLSys-2024.md)

MLSys 2024 共收录 37 篇论文。以下采用多标签计数，同一论文可能同时属于“LLM serving”“量化压缩”和“Kernel/硬件协同”，比例不能直接相加。

| 研究问题 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| 编译器、Kernel 与软硬件协同 | 13 | 35.1% |
| LLM 推理、Serving 与缓存数据路径 | 12 | 32.4% |
| 量化、稀疏与张量/梯度压缩 | 10 | 27.0% |
| 分布式训练、并行与通信 | 8 | 21.6% |
| 端侧与资源受限部署 | 4 | 10.8% |
| 联邦学习系统 | 3 | 8.1% |
| 隐私推理与模型机密性 | 3 | 8.1% |

2024 年最鲜明的主题是“大模型已经出现，首先怎样让它放得下、跑得动”。LLM 推理侧的 12 篇工作集中在四个具体问题：Punica、SLoRA 让大量 LoRA adapter 共享基础模型和 batch；AWQ、Atom、QMoE 将权重或 activation 压到 4 bit 乃至 1 bit 以下；Keyformer、Q-Hitter、Prompt Cache 减少或复用 KV；HeteGen、SiDA 则把权重或计算分到 CPU 与 GPU。此时的研究重心主要是单模型/单服务组件的内存和带宽瓶颈，尚未大量出现后来常见的 P/D 解耦、跨模型路由和复杂在线 SLO 调度。

训练侧仍覆盖更广的 ML workload。Lancet 在 MoE 语言模型的计算图上隐藏 All-to-All，DiffusionPipe 在扩散模型训练中利用冻结 encoder 填 pipeline bubble，L-GreCo 与 MCBench 研究 gradient/activation compression，分布式 GNN 与推荐系统工作则通过矩阵化采样或拓扑感知模型重构减少跨卡数据移动。这里的共同问题是“通信已经限制扩展”，但多数方案仍针对一种模型结构或一种并行模式做专门设计。

2024 年的热门方法并不是单纯采用低精度，而是算法、数据格式和执行 kernel 联合设计。AWQ 用 activation 选择要保护的权重通道，Atom 为 W4A4 设计服务 kernel，QMoE 为 MoE LLM 的亚 1-bit expert 权重设计在线解码，JIT-Q 把量化移到 PIM（内存侧计算），vMCU 则让 kernel 直接参与内存生命周期管理。13 篇编译器/Kernel/硬件相关工作和 10 篇压缩工作高度交叉，说明 MLSys 已要求“理论上的位数或 FLOPs 减少”能够转化为真实 latency、throughput 或容量收益。

| 高频技术路线 | 约涉及论文数 | 对象/负载与主要做法 |
|---|---:|---|
| 低比特、稀疏与压缩 | 10 | 语言模型推理压缩权重/KV，图像分类网络与语言 Transformer 训练压缩激活/梯度，或跳过部分元素计算；FP8 指 8 位浮点，W4A4 指权重和激活均为 4 位，亚 1-bit MoE 则将专家权重平均压到每参数不足 1 位。 |
| 缓存、分页与 CPU-GPU 卸载 | 8 | 面向 LLM 推理，将 KV、LoRA adapter 和 MoE expert 按块管理、共享并提前加载；卸载（offload）指把部分状态移到 CPU 内存等位置，用传输开销换取更多可用 GPU 显存。 |
| 编译与专用 Kernel | 13 | ACRoBat 为含分支、循环的动态神经网络合并跨输入算子；Lancet 重叠 MoE 语言模型训练的计算与通信；FlashDecoding++ 加速自回归语言模型的逐 token 解码算子。 |
| 推理性能预测与配置评估 | 至少 2 | [VIDUR](evidence/venue-catalogs/MLSys-2024.md#vidur)预测不同负载、batching 和并行配置下的 LLM 服务延迟与吞吐；[NAS latency predictor](evidence/venue-catalogs/MLSys-2024.md#nas-latency-predictors)预测候选神经网络在目标设备上的推理延迟，辅助模型结构搜索。 |
| 训练与云管理策略自适应 | 至少 4 | [L-GreCo](evidence/venue-catalogs/MLSys-2024.md#l-greco)调整 ResNet 与语言 Transformer 训练的梯度压缩；[HeteroSwitch](evidence/venue-catalogs/MLSys-2024.md#heteroswitch)处理设备成像差异造成的联邦数据偏差；[FedTrans](evidence/venue-catalogs/MLSys-2024.md#fedtrans)变换并分配客户端训练网络；[FLASH](evidence/venue-catalogs/MLSys-2024.md#flash)适配云资源配置、扩缩容和功率控制器。 |

这里的 activation 是前向计算产生的中间张量，gradient 是更新参数所依据的梯度；多卡训练的 All-Reduce 用于归约并同步数据，All-to-All 则让各设备相互交换各自不同的数据。联邦学习是在客户端本地训练，再聚合模型更新。

Agent 尚未形成独立论文簇。CloudEval-YAML 与 UniDM 是 LLM for Systems/Data，即用 LLM 生成云配置或处理数据；formal-methods feedback 工作研究用验证结果训练控制器生成模型；FLASH 则是传统 ML for Systems，用 meta-learning 适配云资源 controller。它们分别触及工具使用、规划反馈和系统自治，但还没有 2025 以后更明确的多 Agent runtime、Agent 评测环境或面向 Agent workload 的上下文基础设施。

#### 2025

论文列表：[MLSys 2025 完整论文列表](evidence/venue-catalogs/MLSys-2025.md)

MLSys 2025 共收录 61 篇论文。以下仍为多标签计数，重点描述论文形成的研究簇，而不是互斥的官方 track。

| 研究问题 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| LLM/生成模型推理与 Serving | 17 | 27.9% |
| Attention、KV Cache 与长上下文数据路径 | 15 | 24.6% |
| 量化、稀疏、剪枝与状态压缩 | 14 | 23.0% |
| 编译器、Kernel 与加速器协同 | 12 | 19.7% |
| 分布式训练、并行与资源调度 | 11 | 18.0% |
| 端侧与资源受限执行 | 9 | 14.8% |
| 联邦与协作学习系统 | 4 | 6.6% |

2025 年的中心明显转向“怎样让 LLM 长上下文和复杂在线负载成为可服务的系统”。15 篇 Attention/KV/长上下文工作覆盖单请求百万 token 的 context parallel、prefill 的动态稀疏、decode 的精确 kernel、hybrid LLM prefix cache、树状 prefix 共享、KV compression 与低比特 attention。研究不再只问“能省多少 KV”，而开始同时测 TTFT（首 token 等待时间）、TPOT（每输出 token 时间）、output length、cache hit、kernel 可执行性和高并发端到端收益；《Rethinking KV Cache Compression》本身就说明这一方向已进入反思算法指标与生产收益落差的阶段。

LLM serving 调度也从 2024 年的容量管理变得更动态、更细粒度。SOLA 每个 iteration 根据请求与系统 state 平衡 TTFT/TPOT；Seesaw 在 prefill/decode 之间 re-shard 模型；FlexInfer 为两个阶段分别选择 CPU/GPU policy；ThunderServe 根据 GPU 型号、价格、网络和 workload shift 重新规划异构云部署；另有 DiffServe 按 prompt 难度路由不同文生图扩散模型。共同特征是执行策略不再在部署时固定，而会随 phase、query、SLO 和集群状态变化。

训练系统的热点是“可重配置 workflow”。LLM 侧，ReaL 在 RLHF 的 rollout（生成训练轨迹）/update（更新参数）及多个 LLM 之间重分布参数，PipeFill 把其他任务放进 LLM 训练的 pipeline bubble，FPDT 对超长上下文 LLM 做序列分块流水；通用训练侧，[Rubick](evidence/venue-catalogs/MLSys-2025.md#rubick)（含 LLM 负载）联合作业 execution plan 与集群资源，JaxPP 开放 MPMD schedule。与 2024 年针对单个通信点的优化相比，2025 更常把模型训练看成包含多阶段、多模型和可切换并行策略的完整执行图。

| 高频技术路线                             | 约涉及论文数 | 对象/负载与主要做法 |
| ---------------------------------- | -----: | ------------------------------------------------------------------------------------------------------ |
| Attention/KV 的结构化稀疏、量化和复用 | 15 | 面向 LLM 长上下文，以注意力头（head）、缓存块（page）、共享前缀树（tree/prefix）或上下文分片（context shard）组织计算与缓存，配合稀疏、量化和共享减少开销，或通过分片分摊单卡容量需求；须适配实际内核与推理运行时。 |
| 压缩模型和训练：量化、稀疏、剪枝与低秩补偿 | 14 | QServe、TurboAttention、MiLo、DIP、HyC-LoRA 等面向 LLM 推理或微调，压缩权重、KV、训练中间激活和优化器状态，并通过选择精度、保留重要部分或补偿误差来控制质量损失。 |
| Phase(执行阶段)/State(当前状态)-Aware 动态决策 | 至少 9 | 对自回归语言模型的输入处理/逐 token 生成、文生图扩散请求的不同难度，根据延迟目标、设备能力和负载，切换模型、并行方式、卸载比例或执行顺序，使同一任务在不同情况下采用合适的方案。 |
| Pipeline 与计算通信重叠 | 至少 8 | 对语言模型训练、长序列 attention、视频扩散模型的时空 attention 和多 GPU 算子，按阶段、序列或矩阵小块拆分流水，让下一块计算与上一块传输并行。Bubble 是流水线空闲时段；collective 是 All-Reduce 等多设备通信，重叠执行减少其暴露的等待时间。 |
| Trace/Estimator 驱动配置 | 至少 6 | FlexInfer、Lumos、ThunderServe 用测量、执行记录和性能估计器预测 LLM 训推计划的耗时/资源，再选并行、设备或卸载策略；Rubick 将类似方法用于包含 LLM 作业的通用训练集群调度。 |

KV Cache 这边还有一些更细的方向：

- **稀疏**：只计算一部分注意力连接，或者只保留部分 token 的 KV，减少工作量。
- **量化**：用更少的位数保存或计算 Q/K/V 等数据，减少内存、带宽或计算开销。
- **复用**：相同内容已经计算过，就复用对应 KV，避免重算。

对于 KV 这边，不拘泥于这个会这年，从技术方向上来看可以更近一步抽象为：KV Cache 压缩与高效管理，包括更多的方向。

|技术类别|包含的方法|分类依据|
|---|---|---|
|**结构共享**|MQA、GQA|多个 Query 头共享 K/V，减少重复表示|
|**低维表示压缩**|MLA|用更紧凑的潜在表示保存 KV 信息|
|**低精度压缩**|KV 量化|减少每个数值占用的位数|
|**选择性保留／稀疏化**|token 重要性筛选、KV 淘汰、稀疏注意力|只保留或访问部分信息|
|**缓存复用**|前缀共享、跨请求 KV 共享|相同计算结果减少重复计算和存储|

对于压缩模型和训练：

| 方法       | 做什么             | 直观例子                       |
| -------- | --------------- | -------------------------- |
| **量化**   | 降低数值精度          | 原来用 16 bit 保存，现在用 4 bit 保存 |
| **稀疏**   | 让部分元素或计算不再参与执行  | 注意力只关注选中的 token 块          |
| **剪枝**   | 按重要性移除部分参数或结构   | 删除部分权重、通道或注意力头             |
| **低秩补偿** | 用两个较小矩阵的乘积近似补回压缩误差 | 主权重低比特存储，再附加一小部分修正量        |

优化器状态指训练中维护的动量、二阶矩等更新辅助信息。上面的 KV 分类按通用机制归纳，覆盖范围超出本届论文；结构共享、低维压缩和稀疏化是并列路线。

明确的 LLM Agent 相关工作共有 4 篇，占 6.6%：

| Agent 方向 | 论文数 | 代表工作 |
|---|---:|---|
| Agent System | 1 | 多模态规划中分解感知与决策不确定性，并以主动感知和形式验证反馈闭环干预。 |
| Agent Infra | 2 | AI Metropolis 的多 Agent 乱序仿真运行时；XGrammar 的结构化输出与 function-call constrained decoding。 |
| Agent Evaluation / AgentOps | 1 | AIOpsLab 提供云环境、工作负载、故障注入、遥测和操作接口，端到端评估运维 Agent。 |

SwiftVI 虽研究 MDP planning，ProtoRAIL 虽称 imitation agent，但它们分别属于经典决策算法和传统 learned system controller，不计入这里的 LLM Agent 统计。2025 的关键变化并不是 Agent 论文已经很多，而是 Agent 首次作为需要专门 runtime、结构化接口和可执行评测环境的新型系统工作负载出现。

#### 2026

论文列表：[MLSys 2026 完整论文列表](evidence/venue-catalogs/MLSys-2026.md)

MLSys 2026 共收录 135 篇论文。以下统计依据重新细化后的论文方向进行多标签计数；一篇论文可同时涉及多个系统问题，因此各项比例之和不等于 100%。

| 研究问题 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| 训练并行、显存与通信 | 22 | 16.3% |
| 请求调度、批处理与部署 | 19 | 14.1% |
| 编译器、Kernel 与加速器 | 19 | 14.1% |
| 安全、隐私与可靠性 | 16 | 11.9% |
| KV Cache、长上下文与检索数据路径 | 13 | 9.6% |
| 端侧与资源受限部署 | 9 | 6.7% |
| 推测或扩散式解码 | 8 | 5.9% |

本届 AI/ML 类别同时包含 LLM 与其他模型；下文明确区分对象。会议关注的并非笼统的“性能优化”，而是几个具体系统瓶颈：训练侧主要研究异构并行、显存与通信；服务侧主要研究请求级调度、batching、P/D 解耦、模型部署与 KV 数据路径；底层则持续关注 Kernel、编译器和专用加速器。安全、隐私和故障恢复也已经形成较稳定的一组工作。

具体来看，MLSys 2026 的主要研究图景可以概括为：

- 训练负载包括长上下文语言模型、MoE 语言模型和完整图 GNN；优化对象是并行执行计划、训练状态与跨设备通信。22 篇工作集中处理 3D（数据、张量与流水线组合）/FSDP（将参数、梯度等状态分片）/Context Parallel（切分上下文）等并行策略、异构 GPU 放置、弹性扩缩容、显存重计算与卸载、MoE 通信，以及慢节点和故障对训练 goodput（计入停顿与故障损失后的有效吞吐）的影响。研究目标已经不只是峰值吞吐，还包括数值一致性、资源波动下的稳定训练和跨地域低带宽场景。

- 推理调度以文本生成、视觉语言理解等任务为负载，管理自回归/扩散语言模型、多模态 LLM 的请求、批次、执行阶段与服务副本。19 篇调度与部署工作研究 prefill/decode 或 encode/prefill/decode 的阶段划分、请求长度与 SLO 感知 batching、模型和 GPU 的联合选择、Serverless 冷启动、弹性扩容及故障恢复；13 篇 KV Cache、长上下文与检索数据路径工作则处理缓存容量、非前缀复用、跨层级卸载、流式 RAG（先检索相关资料再生成）和向量检索 I/O。两组有交叉，说明当前热点是把模型生成过程拆成可独立调度、存储和迁移的细粒度阶段。

- 编译器、Kernel 与加速器方向的 19 篇工作，以矩阵乘、attention、专家计算和跨设备通信等算子为对象，重点是把高性能算子开发从“为单一 GPU 手工写 kernel”推进到可移植 DSL（领域专用语言）、编译自动生成、动态 megakernel、计算通信协同以及生产级自动调优。研究硬件已扩展到 NVIDIA、AMD、TPU、Trainium、Superchip 和专用数据流/SRAM 加速器，软硬件异构性本身成为需要由系统吸收的问题。

- 安全、隐私与可靠性的 16 篇工作覆盖差分隐私训练、联邦安全聚合、零知识遗忘证明、同态加密推理、GPU 机密计算、越狱检测、输出漂移、慢节点和状态化服务恢复。这里的共同变化是从“给模型增加一个安全指标”转向让训练、推理和运维流程本身可验证、可恢复、可审计。

- 端侧与资源受限部署共有 9 篇，负载包括手机语言模型生成、客户端视觉语言推理、微控制器 CNN 的心电/关键词识别、卫星图像分析及多人 VR 应用。常见约束是显存或 Flash 容量、能耗、网络可用性和实时延迟，因此会联合使用量化、权重生成、CPU-GPU/NPU 混合执行及边云协同，而不是单纯缩小模型。

从同一年内形成的论文簇看，以下技术路线最热门。这里的“热门”表示在 MLSys 2026 中高频出现，尚不表示相较 2024、2025 一定上升；跨年趋势需要在另外两届整理完成后再判断。

| 高频技术路线 | 约涉及论文数 | 对象/负载与主要做法 |
|---|---:|---|
| 量化、稀疏、压缩与早退 | 21 | 对自回归语言模型的权重、KV 和逐层解码，以及微控制器 CNN 的权重存储等对象，按输入、层、通道或 token 分配精度与计算量。早退指依据中间结果的置信度提前结束后续层计算，以减少执行成本。 |
| 阶段解耦、流水化与计算通信重叠 | 16 | 对 LLM/多模态 LLM 推理及训练通信，将 prefill/decode、视觉编码、core attention、通信或检索从原执行路径中拆出，再跨设备流水或与其他阶段重叠；用于缓解长短请求干扰、同步阻塞和异构资源利用不均。 |
| Profiling、Trace、模拟与解析建模 | 至少 12 | 对语言模型训推的算子/通信、GPU 作业性能和集群资源需求，用 trace、计数器、profile 或模拟解释瓶颈，再选择并行、容量或诊断方案；这类方法也开始成为优化 Agent 的观测输入。 |
| 推测解码与扩散式文本生成 | 8 | LLM 推测解码先由草稿模型提出多个 token，再由目标模型批量验证；扩散式语言模型则多位置并行预测并迭代修正。两者都在改变逐 token 串行生成方式，需评估接受率、并发负载与端到端收益。 |
| Agent 驱动的系统优化 | 6 | 以 LLM Agent 为优化工具，生成或修改 GPU kernel、算子、硬件描述代码（HDL）和并行配置，并通过编译、测试、profiling 与实测反馈继续迭代；核心方法是把系统工具链变成可执行反馈环境，而不是只让 LLM 一次性生成代码。 |

这些方法呈现出三条清晰主线。第一，系统越来越强调联合决策，例如同时优化请求路由与 GPU 部署、batching 与 DVFS（动态调节电压和频率）、并行方式与设备放置，而不是逐层独立调参。第二，优化粒度继续下沉，从作业级扩缩容细化到请求、token、Attention head、专家副本和 kernel tile。第三，经验规则正在被“观测—建模—搜索—验证”闭环替代，搜索器可以是成本模型、贝叶斯优化、bandit，也可以是能够调用编译器和 profiler 的 Agent。

Agent 相关论文共有 17 篇，但研究角色不同，不能全部归为 Agent System：

| Agent 方向 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| Agent System：优化规划、记忆等 Agent 闭环机制 | 2 | 1.5% |
| Agent Infra：运行时、服务、存储与上下文基础设施 | 7 | 5.2% |
| Agent for Systems：用 Agent 优化内核、配置或硬件代码 | 6 | 4.4% |
| Agent Evaluation | 1 | 0.7% |
| Agent Security | 1 | 0.7% |

从数量和内容看，MLSys 2026 对 Agent 的关注主要落在基础设施和“Agent for Systems”，而直接修改规划—行动—反馈闭环的 Agent System 工作只有 2 篇。Agent 已成为明确的新方向，但在 MLSys 中更常被视为新的系统工作负载或系统优化工具，而不是会议的主体研究对象。

#### 变化

MLSys 的收录规模从 2024 年 37 篇、2025 年 61 篇扩大到 2026 年 135 篇。由于会议规模变化很大，跨年比较应同时观察论文数和会内占比，不能只用绝对数量判断方向升温。

- LLM 推理从“压缩单个模型”走向“管理完整在线服务”。2024 主要是低比特权重、KV 淘汰、LoRA 多租户和 CPU-GPU offload；2025 转向长上下文、Attention/KV 的真实端到端收益，以及 phase/state-aware 调度；2026 则进一步出现 P/D 或 E/P/D 解耦、异构模型路由与 GPU 部署联合优化、Serverless 弹性、容错恢复和 RAG/Agent 上下文数据路径。

- 训练优化的决策范围持续扩大。2024 多数论文优化一个 communication point、tensor 类型或 pipeline 结构；2025 开始动态改变 RLHF 多模型布局、作业 execution plan 和 sequence pipeline；2026 更强调异构 GPU、弹性资源、长上下文 attention server、慢节点治理与跨地域训练，评价目标也从 raw throughput 扩展到 goodput、稳定性和精度一致性。

- Kernel 开发方式从手工专用实现走向自动生成闭环。2024 代表方法是为低比特、MoE、MCU 和 decode 手工做算法-Kernel co-design；2025 出现 FlexAttention、TileLink、FlashInfer 等可组合 programming model/JIT engine；2026 则进一步出现用 Agent 生成、编译、实测和迭代 kernel/算子的 Agent for Systems，以及让最佳生成结果进入生产 serving 的闭环基础设施。

- Agent 方向呈现清楚的萌芽到扩展过程。2024 主要是 LLM for Systems、传统 ML controller 和形式验证反馈等相邻工作，尚无稳定的 Agent 系统论文簇；2025 出现 4 篇可明确归类的 Agent System、Agent Infra 或 Agent Evaluation；2026 增至 17 篇，主体却不是直接改规划算法，而是 Agent runtime、memory/context、kernel 生成闭环、评测和安全。对本项目而言，这意味着更值得持续跟踪的交叉点是 Agent Infra 与 Agent for Systems，而不仅是通用 Agent 应用。

### OSDI

#### 2024

论文列表：[OSDI 2024 完整论文列表](evidence/venue-catalogs/OSDI-2024.md)

OSDI 2024 共收录 53 篇论文。按官方 session 归并后的分布如下；这里每篇只计入一个 session，因此比例之和为 100%。

| 官方研究簇 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| 形式化验证与正确性分析 | 10 | 18.9% |
| AI/ML 系统：LLM Serving、深度学习与 ML 调度 | 15 | 28.3% |
| 内存管理与远端/分层内存 | 6 | 11.3% |
| 操作系统 | 5 | 9.4% |
| 云计算与资源管理 | 5 | 9.4% |
| 分布式系统 | 4 | 7.5% |
| 云安全与隐私 | 4 | 7.5% |
| 数据与存储管理 | 4 | 7.5% |

形式化方法用明确的规格和逻辑约束检查系统行为；不变量要求某条件始终成立，活性（liveness）要求操作最终能够完成。结论的保证范围取决于采用的规格与系统假设。

2024 最突出的变化是 AI/ML 系统已成为 OSDI 最大单一研究簇，但研究对象非常具体，而非笼统“AI 系统优化”。8 篇工作直接处理 LLM serving：Sarathi-Serve 用 chunked prefill 消除 decode stall，DistServe 分离 prefill/decode 并分别配置资源，Llumnix 在实例间迁移请求与 KV 状态，ServerlessLLM 围绕 checkpoint locality 缩短按需启动，InfiniGen 只预取下一层需要的 KV；dLoRA、VTC 和 Parrot 又分别处理多 adapter、客户公平性和多调用 workflow。共同趋势是把请求执行拆成可观察、可迁移、可独立调度的状态与阶段，优化目标也由平均吞吐转为同时满足 TTFT、TPOT、尾延迟、公平与成本。

另一条强主线是“用编程语言、程序分析和形式化方法减少系统正确性成本”。10 篇官方验证/正确性工作之外，SquirrelFS 与 DRust 也把 Rust 语义用于系统设计。SquirrelFS 用 typestate 在编译期检查 crash consistency，Anvil 证明 controller 最终稳定收敛，RefFS 证明并发文件系统 liveness，VeriSMo 验证敌对 hypervisor 下的 confidential-VM module；CFAR、eBPF state embedding、EET、blocked samples 则通过构造中间表示或变换自动暴露性能、安全和逻辑错误。这里的热点不是单一 verification language，而是找到能把昂贵证明或测试问题结构化的系统边界。

内存方向的 6 篇论文集中反映 CXL、far memory 和 memory disaggregation 开始进入可部署阶段。Nomad 允许快慢层保留副本并异步迁移，Memstrata 将硬件 CXL tiering 与多租户隔离结合，Atlas 根据在线 locality 在 page/object fetch 间切换，DRust 用 Rust ownership 简化 DSM coherence；它们共同避免“一种固定粒度适合所有 workload”的假设。

以下按跨领域方法归纳，研究对象包括 LLM 服务、操作系统、文件系统、内存、网络与分布式协议。

| 高频技术路线 | 约涉及论文数 | 对象/负载与主要做法 |
|---|---:|---|
| 运行时状态感知的动态调度/迁移 | 至少 10 | 对象包括 LLM 请求、云存储 I/O 和分层内存。根据请求长度、队列、缓存位置或访问局部性调整批次、实例、I/O 调度或内存访问粒度；如 [BurstCBS](evidence/venue-catalogs/OSDI-2024.md#burstcbs)按 I/O 成本和租户需求调度云盘请求。 |
| 语言/IR/程序分析驱动的系统构造 | 至少 10 | 对张量程序，用中间表示（IR）表达数据流和依赖以便优化；对文件系统与共享内存程序，用 Rust ownership（资源归属）和 typestate（合法状态转换）限制错误操作，如 [SquirrelFS](evidence/venue-catalogs/OSDI-2024.md#squirrelfs)检查文件系统元数据的持久化顺序。 |
| 硬件—软件职责拆分 | 至少 9 | 对分层内存组织 CXL 容量；对网络收发、存储 I/O 和同步操作，将数据搬运等步骤交给 DPU（数据处理器）、FPGA 或网卡；如 [ZeroNIC](evidence/venue-catalogs/OSDI-2024.md#zeronic)让网卡搬运数据、软件处理协议控制。 |
| 批处理、分阶段和离线/在线工作拆分 | 至少 8 | 对象包括 LLM 推理、数据库事务和分布式协议。分别拆分输入处理与生成、批量准备事务、提前准备验签材料；如 [Chop Chop](evidence/venue-catalogs/OSDI-2024.md#chop-chop)批量组织拜占庭容错广播消息，摊薄认证、去重和排序开销。 |

Agent 相关论文尚未形成论文簇。Parrot 是 1 篇明确的 Agent Infra：它不改 agent 的规划逻辑，而是用 Semantic Variable 把多次 LLM 调用的 dataflow 暴露给 serving 平台做端到端优化。TLM 属于 LLM/Language Model for Systems，用生成模型导航 tensor program 搜索；Caravan 的 labeling agents 是可组合标签源，不是具有规划—行动—反馈闭环的 LLM agent。因此 OSDI 2024 的 Agent 交叉点主要是“支持多调用 agent workflow 的基础设施”，直接研究 Agent System 的论文为 0。

#### 2025

论文列表：[OSDI 2025 完整论文列表](evidence/venue-catalogs/OSDI-2025.md)

OSDI 2025 共收录 53 篇论文，规模与 2024 相同。按官方 session 合并后的互斥分布如下。

| 官方研究簇 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| AI + Systems | 13 | 24.5% |
| 分布式系统与数据中心 | 11 | 20.8% |
| 内核与操作系统 | 10 | 18.9% |
| 数据库系统 | 5 | 9.4% |
| 调度与资源管理 | 5 | 9.4% |
| 文件与存储系统 | 5 | 9.4% |
| 隐私与安全 | 4 | 7.5% |

AI + Systems 仍是最大单一簇，但内部重心从 2024 的多种 LLM request scheduler，转为“执行层、编译层和硬件层如何共同利用异构资源”。LLM 侧，WaferLLM 针对 wafer-scale mesh 重做模型并行与 GEMM/GEMV，NanoFlow 在单 GPU 内让计算、内存和网络通过 nano-batch 重叠，WLB-LLM 处理 4D parallel 中 document 长度造成的多层不均，BlitzScale 则通过 GPU 网络分发权重并按 layer 边装载边扩容。另有面向 DNN 算子（含 LLM Attention）的 PipeThreader 将专用单元流水交给编译器调度。直接研究 LLM serving 的论文数量少于 2024，但每篇优化范围从一个 queue/batch 扩展到设备内部流水、跨机权重网络或新型芯片架构。

编译与可观测性形成很强的方法簇。[Mirage](evidence/venue-catalogs/OSDI-2025.md#mirage) 对 DNN 张量程序（含 LLM 算子）以跨 kernel/block/thread 的 µGraph 做 superoptimization，QiMeng-Xpiler 用 LLM 生成加 symbolic repair 跨平台移植 tensor code，Bayesian code diffusion 加速 autotuning；KPerfIR、Neutrino、Tintin 又分别把 profiling 下沉到 compiler pass、assembly probe 和带 uncertainty 的 OS counter abstraction。共同趋势是“优化器不再只需要一个平均 latency”，而需要可定位到 IR、指令、硬件事件并带可信度的观测。

非 AI 系统的热点是解耦原本绑在一起的系统职责。Mako 解耦 transaction execution 与 geo-replication，SpecLog 重叠应用计算与全序协调，rxBisect 拆开 NIC buffer supply 与 packet delivery，Okapi 拆开 data striping 与 redundancy grouping，Tigon 则用 CXL atomic 取代网络消息同步。大量论文以“decouple/decompose”为核心，并不是为了模块化本身，而是让两侧能按不同时间尺度、硬件或目标独立优化。

| 高频技术路线                   | 约涉及论文数 | 对象/负载与主要做法 |
| ------------------------ | -----: | --------------------------------------------------------------------------------------- |
| 解耦后流水、投机或独立优化            |  至少 12 | 通用系统拆开事务执行与复制、全局排序与本地计算；LLM 服务拆开权重加载与层执行等依赖；投机指在最终确认前先推进可撤销的工作，以减少等待，同时约束失败后的回退代价。                    |
| 编译、IR 与自动搜索              |   至少 8 | 对语言模型的 attention/MoE 及其他矩阵/张量算子，用 µGraph/sTask 表达执行并搜索优化；QiMeng-Xpiler 用语言模型辅助移植张量代码，再以符号方法修复，优化对象是代码。 |
| CXL、RDMA、DPU/NIC 等数据路径协同 |  至少 10 | 对象是共享内存访问、数据库同步与 GPU 间通信；利用 CXL 共享内存、RDMA（远程直接内存访问）、DPU/网卡分配或搬运数据，减少 CPU 介入、热点和拷贝。     |
| 正确性、错误与不确定性显式化           |  至少 10 | 对分布式服务、内核执行和性能计数器，分别生成线上不变量检查、记录/重放执行、标明测量不确定性，使错误定位与性能诊断可核验。                     |

Agent 仍不是独立研究簇。QiMeng-Xpiler 和 SysGPT 是两篇 LLM for Systems：前者用 LLM 提议 tensor-program transformation、再由符号合成修复，后者生成上下文相关的性能优化建议；它们没有持续感知系统、调用工具执行、根据真实反馈自主迭代的完整 Agent for Systems 闭环。Quake、PipeANN、Compass 可作为 RAG/Agent 的向量检索与隐私数据基础设施，但论文优化对象是通用 semantic search，因此更准确地记为 AI/LLM Infra，而不是专门 Agent Infra。直接的 Agent System、Agent Infra 和 Agent for Systems 论文均为 0。

#### 2026

论文列表：[OSDI 2026 完整论文列表](evidence/venue-catalogs/OSDI-2026.md)

OSDI 2026 共收录 136 篇论文。会议扩展为大量并行 session；下表将官方 session 按相近对象合并，每篇仍只计一次，因此比例之和为 100%。

| 官方研究簇（合并）                             | 论文数 | 占全部论文比例 |
| ------------------------------------- | --: | ------: |
| AI 训练、推理、Agent、GPU 编译与训练可靠性           |  37 |   27.2% |
| 程序分析、测试、内核调度、同步、工具与正确性                |  31 |   22.8% |
| CXL/分离内存与缓存                           |  14 |   10.3% |
| 文件系统、持久存储与 Serverless/韧性              |  13 |    9.6% |
| 虚拟化与加速器/设备虚拟化                         |   8 |    5.9% |
| 网络数据路径与共识/BFT                         |   8 |    5.9% |
| Fleet/集群调度与能源可持续性                     |   8 |    5.9% |
| Confidential Computing                |   5 |    3.7% |
| 图、ANN 与向量检索                           |   4 |    2.9% |
| 移动与边缘系统                               |   4 |    2.9% |
| Quantum、加密协作、NAS、SMART 运维等 Wild Cards |   4 |    2.9% |

AI 系统论文已从“为 LLM 增加一种调度策略”发展为覆盖完整生命周期的系统栈。LLM serving 侧同时出现 GPU/CPU/SSD 分层 KV（Strata、ECHO、DirectKV）、多模型显存 ballooning（Prism）、普通 Ethernet 上的部分 P/D 解耦（EcoServe）、跨 HPC 管理域的服务控制面（OpenTela）和本地大 MoE 的 CPU–GPU 分工。训练侧覆盖 LLM/MoE 的万卡异构流水与训练故障恢复，以及通用 HSPMD、算子内通信重叠、数据流水和 RL 基础设施。研究对象已经细化到 layer、neuron、KV block、trajectory、operator boundary 和 SM task。

本届最普遍的方法不是某一种模型算法，而是“先拆开原来同步绑定的阶段，再以运行时观测重新组合”。Tessera 在 MoE LLM 训练中联合设计 partition 与 overlap cost，Syncopate 在一颗 fused kernel 内按 communication chunk 重叠，RollArt 在 LLM Agent 强化学习中解耦轨迹的生成、环境交互与评分，UCCL-Tran/UEP 分离网络 data/control path，Oxbow 在 kernel/userspace/device 间分配文件系统职责，LogDrive 分离 durability 与 sequencing。不同领域共享同一系统思想：把各阶段放到最适合的硬件和时间尺度，同时为新的异步性补上 correctness boundary。

CXL 与 disaggregated memory 已形成 14 篇稳定研究簇。与 2024/2025 主要研究页迁移或 CXL 数据库不同，2026 同时处理 bandwidth/capacity 独立分配、metadata near-memory acceleration、对象—页冷热对齐、memory-controller telemetry、共享内存软件 coherence、远端 GC、SSD 间计算资源共享以及 sub-microsecond stall harvesting。CXL 不再只被视为“更慢的大内存”，而成为需要新观测、同步、虚拟化和设备内计算的完整系统层。

可靠性与生产可运维性同样明显增强。AEGIS、SDCHunter、OpGuard 分别在线筛查、精确重放和定位 LLM training SDC；StriaTrace 只在异常时打开细节 trace；PIMS、DVLA、Alibaba AI cluster study、Meta power planning 将五年到十年的 production experience 抽象为可复用机制。很多论文带有 Operational Systems 标识，评价从单一 throughput 扩展到 SLO、ETTR、placement debt、capacity buffer、故障恢复时间和实际节省资源。

| 高频技术路线 | 约涉及论文数 | 对象/负载与主要做法 |
|---|---:|---|
| 解耦/分离后异步流水与重组 | 至少 25 | LLM 推理拆分 P/D、LLM Agent 强化学习拆分 rollout/training；通用网络、存储和文件系统拆分数据/控制、持久化/排序、内核/用户态/设备职责，再以协议连接。 |
| Runtime state、trace、profiling 与预测驱动决策 | 至少 22 | 语言模型推理按 KV 位置与专家路由调度；训练按激活与故障记录调整；云资源、内存与设备管理按计数器、能源、寿命和队列状态决策。 |
| 编译 IR、自动变换和细粒度 kernel schedule | 至少 15 | 对语言模型 attention、矩阵乘及多 GPU 计算/通信算子，将执行组织成任务图、通信块和矩阵小块，再搜索并安排重叠；CUDA Graph 记录可重用的执行图，mega-kernel 则把多个步骤合入一个内核，减少反复启动和同步开销。 |
| 软硬件职责重新划分与 offload | 至少 20 | 对分层内存管理、GPU 网络传输、文件系统 I/O 和地址映射，分别把处理放到近内存单元、网卡/DPU、SSD 或 GPU；CPU 保留适合软件控制的部分。 |
| 以真实反馈闭环约束 ML/LLM 生成 | 至少 6 | LLM 工具用于生产代码修改、系统证明、资源分析与 SSD 诊断，以测试/证明约束结果；Mimesys 则用扩散模型生成测试负载，再以真实执行校准。 |

Agent 相关工作需要按研究角色拆分，而不能把官方 “Agentic AI and LLM Operations” session 的 4 篇全部视为 Agent System：

| Agent/LLM 角色 | 论文数 | 代表工作与边界 |
|---|---:|---|
| Agent System | 1 | SPEX 直接改变 Tree-of-Thought 的 reward-guided 探索、跨 query 预算和终止机制。 |
| Agent Infra | 4 | Murakkab 优化多模型/工具 workflow serving；RLinf、DynaRL、RollArt 提供 reasoning/embodied/agentic RL 的拆分、调度与异构训练基础设施。 |
| Agent for Systems | 2 | ECO 闭环修改并验证生产代码；neuro-symbolic proof generation 让 LLM 与 Isabelle 工具持续交互完成系统证明。 |
| LLM for Systems（非 Agent） | 至少 2 | gigiprofiler 用 LLM 找应用资源后由静态分析验证；SMARTTalk 将 SSD 数值趋势转成 token 后让 LLM 诊断。 |

RobustRL、Weave、Seer 等也能支撑 agentic RL，但其机制针对通用 RL rollout/training，因此未重复计入“明确 Agent Infra”四篇。StriaTrace 是 LLM 运维系统而非 Agent；CoreSec 的 telemetry agents 是规则化诊断组件；LMetric 只是用 coding-agent trace 评测通用 LLM scheduler。按这一口径，OSDI 2026 的 Agent 交叉点以 Agent Infra 和 Agent for Systems 为主，直接研究 agent 规划/推理闭环的工作仍少。

#### 变化

OSDI 的论文数从 2024、2025 各 53 篇扩大到 2026 年 136 篇，因此跨年应观察比例和问题结构，不能只比较绝对数量。AI/ML 系统按官方 session 占比三年约为 28.3%、24.5%、27.2%，始终约占四分之一；变化主要发生在研究粒度和系统边界，而不是简单的占比持续上升。

- LLM 系统从请求调度走向全栈生命周期。2024 重点是 chunked prefill、P/D 分离、KV offload、多 adapter 和请求迁移；2025 更强调 wafer-scale/单 GPU 内流水、LLM 编译与 live autoscaling；2026 则覆盖多级 context storage、异构 RL post-training、训练 SDC、GPU kernel/compiler、跨管理域 serving 和 agent workflow runtime。

- “动态”决策范围逐年扩大。2024 多在单个请求或内存页进入系统后重调度；2025 出现运行时 data path、CXL synchronization 和跨层 pipeline；2026 进一步同时迁移计算、内存和通信资源，并根据 activation、trajectory、外部电力信号、failure trace 与 fleet lifetime 持续更新计划。

- 系统正确性研究从证明核心组件，扩展为开发和生产全周期工具。2024 有 Rust typestate、controller liveness、eBPF verifier testing；2025 出现 test-derived online checker、training invariant、kernel record/replay；2026 则将 deterministic scheduler testing、bitwise LLM alignment、reference model CI/CD、LLM+ITP proof search 和带 uncertainty 的 observability 纳入持续运行流程。

- Agent 方向在 2026 才形成明确会议簇。2024 只有 Parrot 这一 Agent Infra，2025 主要是 LLM for Systems 和可供 RAG 使用的通用向量基础设施，2026 才同时出现 Agent System、Agent Infra 与 Agent for Systems。即便如此，数量主体依旧是 workflow/RL 基础设施和用 Agent 优化系统，而不是直接改进通用 agent 的规划—行动—反馈算法。

### SOSP

#### 2024

论文列表：[SOSP 2024 完整论文列表](evidence/venue-catalogs/SOSP-2024.md)

SOSP 2024 共收录 43 篇论文，也是 SOSP 改为每年举办后的首个偶数年份届次。下表按论文实际研究对象做多标签统计；同一工作可同时属于例如“内存解耦”和“存储系统”，比例不应相加。

| 研究问题 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| AI/ML 训练、推理、编译与资源管理 | 11 | 25.6% |
| 正确性、形式化验证、安全与系统测试 | 11 | 25.6% |
| 云、Serverless 与分布式协议/运维 | 9 | 20.9% |
| 内存解耦、分层内存与 I/O 虚拟化 | 8 | 18.6% |
| 操作系统内核、隔离与用户态调度 | 8 | 18.6% |
| 存储、索引、日志与数据冗余 | 7 | 16.3% |

SOSP 2024 的 AI 系统工作已经覆盖训练、推理和编译，但重心仍是明确的系统瓶颈，而不是模型能力本身。推理侧，Apparate 与 E3 面向视觉/NLP 模型及 LLM 使用 early exit，分别解决在线阈值自适应和 batch 逐层缩小造成的设备利用率下降；LoongServe 在 LLM 推理中 把单个长上下文请求的 sequence-parallel degree 变成随 prefill/decode 阶段变化的运行时变量；PowerInfer 则把本地 LLM 的 CPU–GPU 划分粒度降到 neuron。训练侧，HotSPa 面向 LLM，[ReCycle](evidence/venue-catalogs/SOSP-2024.md#recycle)、[Tenplex](evidence/venue-catalogs/SOSP-2024.md#tenplex) 面向大型 DNN 训练（均含 LLM 负载），三者 分别处理序列长度变化、GPU 故障和资源集合变化，说明研究对象正从固定作业计划转向“执行期间如何重构并行布局与状态”。

另一条同样强的主线是正确性工具必须能覆盖真实系统代码和硬件边界。Icarus 证明 JIT 未来可能生成的所有代码，Parfait 将 HSM 应用规范连接到电路及时序泄漏，TPot 让标准 C 测试成为 proof specification，Verus 则以 Rust 为基础统一多类系统证明。Anduril、Ozz 和 retry-bug 工具不追求全证明，而是分别用反馈搜索、可控内存乱序和 LLM 语义识别把难以重现的故障转化成可执行测试。这些工作共同表明，SOSP 对“正确性”的关注正在从单一 verified artifact 扩展到开发、测试、重现和生产诊断流程。

内存与数据路径方向体现了 disaggregation 开始从“能否远程访问”进入具体机制设计。Aceso 和 SWARM 分别处理内存池键值存储的空间高效容错与单往返强一致复制，CHIME 重新设计远端范围索引，Colloid 根据排队后的实测延迟而非标称速度放置页面；Fast & Safe、VPRI 又分别优化安全 DMA 映射和 passthrough device 的 I/O page fault。研究单位已细化到索引元数据、remote object、page、IOTLB miss 和 fault request。

| 高频技术路线 | 约涉及论文数 | 对象/负载与主要做法 |
|---|---:|---|
| 运行时反馈驱动的动态选择 | 至少 9 | 图像/NLP 分类及自回归语言生成按置信度调整早退；长上下文语言模型按阶段调整并行；内存页、云作业和故障测试分别按访问延迟、碳/价格或搜索反馈调度。 |
| 解耦原有关键路径并延迟工作 | 至少 10 | 通用日志 LazyLog 延迟全局排序，Serverless 平台 Dirigent 移除调用路径的持久化；含 LLM 负载的 DNN 训练系统 ReCycle 分段反传填空闲，LLM 训练 Perseus 降低非关键路径功耗。 |
| 语言、类型、IR 与可证明抽象 | 至少 9 | Rust/Verus 和符号执行验证内核、JIT 代码及 C 程序；FractalTensor 用嵌套表示暴露 RNN、attention 的并行/复用结构，供编译器优化。 |
| 软硬件协同与异构数据放置 | 至少 10 | 对象包括设备 DMA/I/O 映射、线程隔离、存储写入和加速器张量放置；其中 PowerInfer 按神经元划分语言模型的 CPU/GPU 推理工作。 |

Agent 方向在本届尚未形成论文簇。retry-bug 工作是 1 篇明确的 LLM for Systems：LLM 用来理解 ad-hoc retry 代码并寻找测试位置，但它不自主修改系统、执行修复并根据真实反馈持续迭代，因此不是 Agent for Systems。Anduril 虽然有“注入—观察—选择下一故障”的反馈搜索，控制器也会自动行动，但其决策不是通用 Agent/LLM；Zodiac 的部署验证同样属于传统自动化程序分析。按本报告口径，SOSP 2024 的 Agent System、Agent Infra 与 Agent for Systems 均为 0。

#### 2025

论文列表：[SOSP 2025 完整论文列表](evidence/venue-catalogs/SOSP-2025.md)

SOSP 2025 共收录 66 篇论文。下表采用多标签计数，目的是显示研究簇之间的交叉；例如 PhoenixOS 同时属于 GPU/AI 基础设施和 OS checkpoint，TrainVerify 同时属于训练系统和形式化验证。

| 研究问题 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| AI/ML 训练、推理、RAG、编译与可靠性 | 21 | 31.8% |
| 正确性、形式化验证、安全与系统测试 | 18 | 27.3% |
| OS 内核、运行时、调度与隔离 | 19 | 28.8% |
| 云、Serverless、资源分配与生产运维 | 19 | 28.8% |
| 内存、CXL、设备虚拟化与数据移动 | 13 | 19.7% |
| 存储、数据库、事务与遥测数据系统 | 15 | 22.7% |

AI 系统从 2024 年的单点训练/推理机制扩展到“模型执行之外的控制面和可靠性”。LLM serving 侧，Aegaeon 在 token 粒度复用模型市场中的 GPU，Jenga 针对不同 layer 的 attention/embedding shape 管显存，DiffKV 把 K/V、token 与 head 的重要性差异转成真正可整理的显存空洞；Pie 则把固定 generation loop 开放成可编程 inferlet，使 agentic workflow 可以控制 KV、工具 I/O 与生成过程。面向 LLM 的 RAG 形成 HedraRAG 和 METIS 两种互补路线：前者变换整个 workflow graph 来流水 CPU/GPU stage，后者按 query 的质量需求调整检索数量、合成方法和排队次序。

LLM 训练系统明显把“跑得快”和“出错后是否可信”放到一起。Sailor 为动态、异构、跨地域 GPU 搜索非对称并行计划，DCP 根据每批序列长度和 attention pattern 重分 context block，Tempo 编译带动态时间依赖的 RL/LLM 程序；ByteRobust 与 Mycroft分别处理万卡故障恢复和 collective dependency root cause。TrainVerify 更进一步，以未并行模型为规范证明 Llama3 405B、DeepSeek-V3 671B 的 distributed execution plan 数学等价，说明 silent training bug 已成为可单独研究的系统问题。

本届另一强主线是用更小、可检查的可信部件替换“大而复杂但只能相信”的系统边界。eBPF proof-guided refinement 把复杂推理移到用户态、内核只验 proof；Miralis 降权运行原 vendor firmware；AutoMan 不信任 code generator，而验证最终生成/手调代码 refinement；CortenMM 直接删除 VMA 与 page table 的双重状态以便验证；Atmosphere、TickTock 则展示 Rust+SMT verifier 已能覆盖完整 microkernel 和生产嵌入式 OS。相比 2024，形式化方法更频繁地与 production code、生成工具和架构简化共同设计。

资源管理方法也从单一容量转向互依资源和连续时间控制。Spirit 联合交易 far-memory cache 与带宽，COpter 复用上一轮 LP/MILP 的求解状态，LithOS 在 TPC 粒度联动 GPU 空间调度、right-sizing 和功率，Tai Chi 在 SmartNIC 上以数据面 SLO 为约束回收 control-plane CPU。共同点是 controller 不再每轮从静态快照重新开始，而是保留资源之间的替代关系、上轮解或实时运行状态。

| 高频技术路线 | 约涉及论文数 | 对象/负载与主要做法 |
|---|---:|---|
| 细粒度运行时调度与状态重组 | 至少 18 | 自回归语言模型推理管理 token、attention block 与 KV head；GPU 训练/推理混部管理 TPC 硬件分区；内核调度、远程内存和设备 I/O 管理持锁线程、页及队列。 |
| 规格、证明、等价或独立 oracle | 至少 15 | 对内核/固件与生成代码检查规格符合性，对 Llama/DeepSeek 等语言模型检查并行训练与参考执行的数学等价；oracle 是独立判断结果正确性的机制。 |
| 解耦后异步/流水执行 | 至少 17 | LLM 的 CPU/GPU 专家计算与 RAG 检索/生成阶段拆分重叠；通用系统重叠内存复制、缺页/淘汰、GPU 检查点、边缘事务和存储完成处理。 |
| 软硬件边界重划与设备能力复用 | 至少 14 | 对共享内存池、内存访问隔离、网络控制、GPU 文件 I/O 与训练/推理混部，利用 CXL、CHERI、SmartNIC 和 GPU 运行时重分控制与数据处理职责。 |
| Trace、历史状态与生产反馈驱动决策 | 至少 12 | 语言模型服务按历史查询/请求相似性管理执行，训练按 collective 依赖诊断；内核检查器、云资源分配与优化求解器利用补丁、遥测或上一轮求解状态决策。 |

Agent/LLM 相关工作仍需严格区分：

| Agent/LLM 角色 | 论文数 | 代表工作与边界 |
|---|---:|---|
| Agent System | 0 | 没有论文直接改进通用 Agent 的规划、记忆或行动反馈算法。 |
| Agent Infra | 1 | Pie 明确把 agentic workflow 的生成、KV、工具 I/O 和应用逻辑开放为可编程 serving runtime。 |
| Agent for Systems | 0 | 没有以通用 Agent 持续调用系统工具、执行变更并根据实测反馈迭代的工作。 |
| LLM for Systems（非 Agent） | 1 | KNighter 从历史 kernel patch 合成并验证静态 checker；核心产物是可重复执行的 analyzer，而非运行时自主 Agent。 |

HedraRAG、METIS、IC-Cache 是 RAG/LLM Infra，可成为 Agent 应用的下层组件，但论文优化对象是通用 RAG 或 LLM request，未专门利用 Agent 的多轮工具闭环，因而不重复记作 Agent Infra。ByteRobust、Mycroft、COpter 等具有自动检测、定位或优化闭环，但控制器不是 LLM/通用 Agent；本报告将它们归为传统自治系统或 AIOps，而不是因“自动化”就归入 Agent for Systems。

#### 2026

论文列表：[SOSP 2026 完整论文列表](evidence/venue-catalogs/SOSP-2026.md)

截至 2026-09-20，SOSP 2026 已公布 62 篇录用论文，但会议尚未召开、正式 proceedings 尚未发布。下表采用官方日程的互斥 session 分类，每篇只计一次；论文列表中 31 篇已有可解释核心工作的公开摘要或预印本，另外 31 篇会前信息不完整，因此本节对整体方向的判断以官方 session 和已公开材料为主，不提前虚构未公开机制。

| 官方 session                                  | 论文数 | 占全部论文比例 |
| ------------------------------------------- | --: | ------: |
| Model Serving at Scale                      |   5 |    8.1% |
| Privacy and Confidential Computing          |   5 |    8.1% |
| CXL and Memory Systems                      |   6 |    9.7% |
| Storage and File Systems                    |   6 |    9.7% |
| Operating Systems and Virtualization        |   6 |    9.7% |
| AI Workflows and Performance Tuning         |   5 |    8.1% |
| Verification and Formal Methods             |   6 |    9.7% |
| Distributed Systems                         |   6 |    9.7% |
| Predictable and Resilient AI Infrastructure |   5 |    8.1% |
| Debugging, Testing, and Program Analysis    |   6 |    9.7% |
| GPU Kernels and Accelerators                |   6 |    9.7% |

AI 系统已经不是一个孤立的 serving session。将 Model Serving、AI Workflows、AI Infrastructure 与 GPU Kernels 四个官方 session 合并，共有 21 篇，占 33.9%；Agent-native filesystem、Agent shared log 和模型仓库存储等交叉论文还被安排在 Storage session。研究对象覆盖完整生命周期：PrismLLM 用少量真实 GPU 复现 8192 卡 LLM 训练行为，Janus 在 768 个异构设备上联合部署 LLM 与路由请求，TensorHub 处理 LLM 强化学习的 trainer/rollout worker 权重传输，LLM-42 保障 LLM 推理确定性；Anchor 处理 AI 训练/推理的 GPU 浅层故障。热点因此从“怎样提高正常状态吞吐”扩展为怎样复现、扩缩、同步、验证和恢复模型服务。

细粒度状态重组是最集中的方法路线。[DiFlow](evidence/venue-catalogs/SOSP-2026.md#diflow) 把文生图扩散模型的生成流程拆成文本编码器、扩散模型等可独立扩缩和共享的节点；Moebius 调整 MoE LLM 中张量并行（TP）与专家并行（EP）的设备分工；[TensorHub](evidence/venue-catalogs/SOSP-2026.md#tensorhub) 复用 LLM 强化学习中推理 GPU 已驻留的权重版本；TStore 则按模型仓库中的权重张量寻找压缩冗余。它们分别以模型节点、专家/KV 分片、权重版本或张量为管理单位，按并发、拓扑和运行状态调整资源组织。

CXL 与共享内存第一次成为独立的 6 篇 session。论文不再只把 CXL 当作慢一档的大内存：disk-based LSM 用“可原地修改表面”设计部分一致内存索引，StarfishOS 切分 CXL-resident OS state，XTRA 复用事务冲突检测来保证 cache freshness，Tierce 则解决共置负载污染 page-criticality 观测的问题。研究重点已转向 coherence boundary、同步元数据、故障隔离和可观测性，即怎样把有限硬件一致性转化为可扩展的软件抽象。

验证、调试和测试仍占两个完整 session，共 12 篇、19.4%。其中方法明显强调“结构化反馈”：SaSh 用风险导向符号执行检查 shell effect，DDB 用 distributed backtrace 和虚拟时间恢复可交互调试，M2K 抽取 LLM 输入与 CUDA kernel 的接口约束，再做符号执行，Welder 以可组合 CORE 规格逐个验证 controller。LLM 的使用也开始被可信工具约束：I3DP 让 LLM 提出 invariant 候选，但最终由 IC3/TLAPS 检查；Ave 让优化 Agent 收到 SMT 反例，而不是把 LLM 输出直接当作正确结果。

以下按共同方法归纳，横跨 LLM、扩散模型和通用系统；每行的具体研究对象见末列。

| 高频技术路线 | 约涉及论文数 | 对象/负载与主要做法 |
|---|---:|---|
| 对整体系统对象做细粒度分解并动态重组 | 至少 14 | 文生图扩散服务拆分生成流程，MoE 语言模型调整并行布局，模型仓库按权重张量压缩；[XTRA](evidence/venue-catalogs/SOSP-2026.md#xtra) 组织分布式事务的缓存一致性/冲突检测元数据，[StarfishOS](evidence/venue-catalogs/SOSP-2026.md#starfishos) 切分跨主机操作系统状态，以减少同步或隔离故障。 |
| 编译表示与形式化约束共同参与优化或验证 | 至少 12 | 对 GPU 算子约束数据流、对 LLM 推理内核检查越界；对 CNN、BERT 和 LLM 的全同态加密推理生成 GPU 代码；对分布式协议、事务系统和 Kubernetes 控制器建立状态模型并证明正确性。各自验证算子、加密计算或协议/控制器行为。 |
| 运行时反馈驱动的双时间尺度或闭环控制 | 至少 8 | [Janus](evidence/venue-catalogs/SOSP-2026.md#janus) 面向多 LLM 服务，慢周期优化模型共置，快周期扩缩副本，并按请求期限路由；[TuxBot](evidence/venue-catalogs/SOSP-2026.md#tuxbot) 面向 Linux 主机，用 LLM 辅助调整调度、功耗、内存和 I/O 参数，快环调参、慢环改策略。 |
| 训练/推理状态的可靠性与输出确定性 | 至少 7 | TensorHub 保证语言模型强化学习的权重版本一致；Anchor 恢复轻微中断后的 GPU 作业内存状态（具体模型配置待公开）；[LLM-42](evidence/venue-catalogs/SOSP-2026.md#llm-42) 对 LLM 候选输出做验证和回滚，使动态批处理下同一输入仍可得到可复现输出。 |

Agent/LLM 交叉点已经可以按系统角色形成清晰分类：

| Agent/LLM 角色 | 论文数 | 代表工作与边界 |
|---|---:|---|
| Agent System | 0 | 没有论文直接修改通用 Agent 的规划、记忆、反思或行动反馈算法。 |
| Agent Infra | 3 | AgileLog 为流上 Agent 提供 forkable log；YoloFS 提供可观察、可回滚、可门控的文件副作用；SkVM 编译并运行跨模型/harness 的可移植 skill。 |
| Agent for Systems | 2 | Ave 让 Agent 在 SMT 反例反馈下持续优化 GPU kernel；TuxBot 观察主机状态、写入 Linux knob，再根据 action–response history 调整策略。 |
| LLM for Systems（非 Agent） | 2 | I3DP 用 LLM 辅助 invariant synthesis，JavaScript engine fuzzing 用 LLM 指导 instrumentation；核心产物是验证/测试结果，不是持续管理真实系统的行动主体。 |

这一分布说明 SOSP 2026 的新变化不是大量研究 Agent 推理算法，而是系统开始同时成为 Agent 的运行底座和 Agent 的操作对象。尤其是 YoloFS、AgileLog 与 SkVM 针对多步、会产生副作用且运行时长不确定的 agentic workload 设计新抽象，属于 Agent Infra；Ave、TuxBot 则真正把“观察—提出动作—执行—验证/反馈—再行动”用于系统优化，属于 Agent for Systems。

#### 变化

三届论文规模分别为 43、66、62 篇。按本报告的多标签统计，AI/ML 系统相关论文从 2024 年 11 篇（25.6%）增至 2025 年 21 篇（31.8%）；2026 年仅合并四个明确 AI/GPU 官方 session 就有 21 篇（33.9%）。由于 2026 使用互斥 session、前两年使用多标签口径，比例只适合判断趋势，不能视为严格同口径增长。

- AI 系统从单点机制走向完整运行周期。2024 重点是 early exit、动态 sequence parallel、CPU–GPU neuron placement 和故障后重构；2025 把 token/TPC/KV head 等细粒度调度与训练正确性、生产恢复结合；2026 又补上超大规模仿真、offline inference、多 LLM 生产部署、RL 权重传输、推理确定性与 GPU disruption recovery。

- 动态优化的基本单位持续变小，同时控制范围变大。2024 多改变 request、page 或 parallel degree，2025 下沉到 token、attention block 和 device queue，2026 则同时操纵 model node、expert/KV slice、tensor、weight version 和跨主机同步目录；局部单位更细，但决策已跨 compiler、runtime、storage 与 cluster control plane。

- 正确性研究从独立工具转向系统数据路径中的在线 guardrail。2024 主要是 proof language、JIT meta-execution 和故障测试，2025 强调小可信核、proof checking 与生成结果验证，2026 出现 fixed-shape verify–rollback、model–kernel interface、SMT counterexample feedback 和可组合 controller liveness。生成式模型可以参与搜索，但最终结论越来越由符号约束、独立 oracle 或机器证明封闭。

- Agent 方向呈现 0 → 基础设施萌芽 → 基础设施与系统闭环并行的变化。2024 没有明确 Agent 论文，2025 有 Pie 这一 Agent Infra；2026 出现 3 篇 Agent Infra 和 2 篇 Agent for Systems，但 Agent System 仍为 0。对本调研而言，SOSP 的主要价值因此是观察 agentic workload 如何反向改变日志、文件系统和 runtime，以及 LLM/Agent 如何在可验证反馈下参与系统优化，而不是寻找新的通用规划算法。

### EuroSys

#### 2024

论文列表：[EuroSys 2024 完整论文列表](evidence/venue-catalogs/EuroSys-2024.md)

EuroSys 2024 共收录 71 篇论文。下表为按研究对象整理的多标签统计，同一论文可能同时属于 AI 系统、云资源管理和正确性等多个方向，因此比例不应相加。

| 研究问题 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| AI/ML 训练、推理、联邦学习与编译 | 22 | 31.0% |
| 正确性、容错、安全与系统测试 | 19 | 26.8% |
| 云、Serverless、资源管理与能效 | 17 | 23.9% |
| 存储、缓存、持久内存与内存分层 | 15 | 21.1% |
| 网络数据平面、拥塞控制与网络管理 | 13 | 18.3% |
| 分布式协议、图与数据处理系统 | 12 | 16.9% |

AI 系统论文数量已达约三成，但对象较分散。训练侧，[DynaPipe](evidence/venue-catalogs/EuroSys-2024.md#dynapipe) 面向 LLM 多任务训练重组动态流水；Aceso（含 LLM 负载）、HAP、ScheMoE 分别在 DNN 瓶颈、异构 SPMD 和 MoE task 层重组执行计划；推理侧，RAMSIS 根据 arrival lull 选择更准确模型，Optimus 在 serverless function 间变换模型以复用 warm state，Orion 在 kernel 粒度控制多租户 GPU interference，GMorph 则直接融合多个已有 DNN 的执行图。联邦学习同时出现 Dordis、Totoro、FLOAT、DeTA 四种系统路径，分别关注 dropout 下的精确 DP、边缘 P2P 扩展、deadline 自动调优和去中心可信聚合，说明 AI 系统的“性能”已经与隐私、容错和资源异质性深度交叉。

本届最常见的方法是把传统整体对象拆成可重组的更小单位。DNN 训练被拆成 bottleneck、micro-batch 或 MoE task，GPU sharing 下沉到 kernel，serverless model 下沉到 meta-operator，GNN 同时拆 graph 与 operator，异构内存则以 page/huge page 为迁移单位。拆分后，系统再依据在线 queue、inter-arrival、设备速度、干扰或访问热度改变组合。这条路线比单纯提出一个更快 kernel 更具普遍性：它首先暴露原来被框架隐藏的决策边界，再让 scheduler/compiler 能够操作。

存储与内存方向集中在“避免重复搬运和写放大”。RMMap 消除 serverless state 的序列化，EasyIO 用 DMA 隐藏慢内存文件系统搬运，Volley 让 writeback/fetch 并发而在远端恢复顺序；CSAL、CCL-BTree、Wormhole Filter 分别从 SSD 分层、leaf buffer 和持久 hash metadata 降低写放大。CXL 尚处在实证与管理阶段：ASIC CXL 论文给出真实性能—成本边界，MTM 则开始统一多层内存 profiling 与 migration，尚未出现 2026 年那样围绕一致性与共享 OS state 的完整研究簇。

正确性工具强调用中间表示或独立证据把复杂系统行为变得可检查。Noctua 用 SOIR 连接 Web 代码、数据库和 SMT，SandTable 在 specification state space 搜索后回到实现确认，Emme 从数据库 version chain 恢复 isolation certificate，eBPF 工作则构造 verifier-specific oracle。共同点不是追求一个万能证明器，而是寻找比原始代码/执行 trace 更小、仍保留错误语义的验证边界。

| 高频技术路线 | 约涉及论文数 | 对象/负载与主要做法 |
|---|---:|---|
| 细粒度拆分与运行时重组 | 至少 16 | 语言模型多任务训练拆分微批次，MoE 训练拆分专家/通信任务，GNN 训练拆分图与算子；分层内存和 Serverless 平台分别管理页与函数状态。 |
| 在线反馈、学习或预测驱动配置 | 至少 14 | 推理服务按请求间隔选择准确率/延迟不同的网络；GPU 作业按干扰调频，分层内存按热度迁页，云作业按价格或故障状态扩缩与保存状态。 |
| IR、DSL、编译器与程序合成 | 至少 12 | 用领域专用语言（DSL）描述计算或安全约束，再转换为 IR、生成目标代码；程序合成则从规格和约束搜索满足条件的实现，用于并行程序、加密计算或系统扩展。 |
| 跨软件层或软硬件协同重划数据路径 | 至少 15 | 对设备直通 I/O、网络包处理、Serverless 状态访问和 SSD 分层，利用 DMA、网卡/交换机或远端映射减少复制、CPU 处理与写放大。 |

Agent 方向尚未形成独立论文簇。RCACopilot 是 1 篇 LLM for Systems：它把云事故证据交给 LLM 做根因分类和解释，但没有自主提出并执行系统变更、再依据结果迭代，因此不属于 Agent for Systems。Astraea 虽使用 multi-agent reinforcement learning 训练相互竞争的 congestion-control flow，但这里的 agent 是传统 RL policy，不是本报告关注的 LLM/通用工具 Agent；Atlas、Aceso、FLOAT 等自动优化器也同理。按统一口径，Agent System、Agent Infra 和 Agent for Systems 均为 0。

#### 2025

论文列表：[EuroSys 2025 完整论文列表](evidence/venue-catalogs/EuroSys-2025.md)

EuroSys 2025 共收录 85 篇论文。以下仍采用多标签统计，主要用于观察交叉研究簇。

| 研究问题 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| AI/ML 训练、推理、联邦学习与编译 | 28 | 32.9% |
| OS、虚拟化、内存管理与系统运行时 | 23 | 27.1% |
| 正确性、容错、安全与系统测试 | 18 | 21.2% |
| 云、Serverless、资源调度与能效 | 17 | 20.0% |
| 存储、索引、缓存与持久内存 | 16 | 18.8% |
| 网络数据平面、拥塞控制与验证 | 13 | 15.3% |

AI 系统仍是最大研究簇，并开始围绕 LLM 的状态和变体形成新的数据管理问题。Pensieve 把 conversation state 变成跨请求的一等缓存对象；CacheBlend 复用非前缀 RAG 知识块的 KV，只选择性重算受上下文影响的 token；DeltaZip 压缩并服务 full-model fine-tuning delta；HCache 又在 KV 全量加载与从头重算之间加入 intermediate activation recovery。它们的共同点是：服务对象已经不是一次 request，而是会话、知识块、模型变体和可恢复执行状态。

LLM 训练系统的控制范围也明显扩大。HybridFlow 同时表达 RLHF rollout、reward 和训练阶段并完成 actor resharding，Mist 联合选择 parallelism 与所有减显存技术，MEPipe 把 pipeline 粒度降到 sequence slice，FlowCheck 将 checkpoint 持久化从训练关键路径解耦，DFCCL 则在 collective library 底层提供抢占以消除应用级通信死锁。研究不再只优化某个 collective，而是管理训练阶段之间的模型布局、状态一致性和故障边界。

内存与存储工作反复出现“先获得更真实的观测，再做迁移或调度”。Chrono 区分各 memory tier 的 page frequency，vSched 用 guest 内 microbenchmark 恢复动态 vCPU capacity/topology，TUNA 去除云实验噪声后再 autotune，Heimdall 用 period label 和三阶段过滤构造可用于 I/O admission 的稳定信号。相比 2024，controller 更少直接相信单个 hardware counter 或一次 benchmark，而是先修复 observability，再据此行动。

系统正确性研究继续向生产代码和接口演进。Multi-grained TLA+ 以不同粒度连接 ZooKeeper 模型与实现，Efeu 同时生成并验证 I2C 的软硬件 driver，BESA 用 runtime failure 约束静态搜索，Seal 从 security patch 推断 Linux interface value-flow specification，DepSurf 则揭示 eBPF extension 与 kernel image 间普遍的 dependency mismatch。规格来源已经从专家手写扩展到 patch、运行时失败、驱动描述和实际依赖面。

| 高频技术路线 | 约涉及论文数 | 对象/负载与主要做法 |
|---|---:|---|
| 状态复用、压缩与跨阶段布局变换 | 至少 17 | LLM 会话 KV、RAG 知识块、微调权重差量、训练中间激活、RLHF actor 状态与检查点被缓存、压缩或异步迁移。 |
| 联合而非串行地优化相互耦合决策 | 至少 18 | 语言模型训练联合显存与并行，推理服务联合批次与扩缩容；图计算联合图/算子划分，分层内存联合冷热判断与迁移，多资源管理联合调频。 |
| 更精确的观测、去噪与自省 | 至少 13 | 先用探测程序估计虚拟 CPU 的真实能力，区分不同内存层的数据访问热度，并剔除云实验噪声；再据此决定放置、迁移和调度，避免把测量偏差当成性能变化。 |
| 软硬件/内核—用户态边界重构 | 至少 18 | 调整哪些检查和操作在内核、用户进程、可信执行环境或设备中完成；例如以内核旁路减少部分 I/O 的系统调用路径，以共享分配器减少重复管理，同时保留必要隔离。 |

本届依然没有明确的 Agent System、Agent Infra 或 Agent for Systems 论文。HybridFlow 是通用 RLHF infrastructure，Pensieve、CacheBlend、DeltaZip 是 LLM/RAG infrastructure，它们可被 Agent workload 使用，但论文没有针对多步工具调用、可回滚副作用或 agent harness 设计专门机制，因此不重复标为 Agent Infra。Jury、Flex、VMR2L 使用传统强化学习做拥塞控制、层放置和 VM 调度，也不能因存在“policy/agent”就算作 LLM Agent。按本报告口径，LLM for Systems 论文同样为 0。

#### 2026

论文列表：[EuroSys 2026 完整论文列表](evidence/venue-catalogs/EuroSys-2026.md)

EuroSys 2026 共收录 138 篇论文。以下继续采用多标签口径：例如一篇为 LLM 服务设计的显存管理论文，可同时进入 AI 系统、内存管理和云资源调度，因此各行比例不应相加。

| 研究问题 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| AI/ML 训练、推理、服务、Agent 与 ML for Systems | 54 | 39.1% |
| 云、Serverless、集群资源与数据中心管理 | 42 | 30.4% |
| 正确性、容错、安全、测试与故障恢复 | 34 | 24.6% |
| OS、虚拟化、内存、运行时与异构加速器 | 33 | 23.9% |
| 存储、缓存、文件系统与持久数据结构 | 30 | 21.7% |
| 网络传输、数据平面、RDMA 与 WAN/CDN | 26 | 18.8% |

AI 系统已成为最大研究簇，且范围从某个训练或推理 kernel 扩展到整个模型生命周期。LLM 侧，MegaScale-MoE、Zeppelin、MegaScale-Omni 分别处理 MoE 通信、变长序列与多模态 LLM 组件；Crimson、Suika 处理参数更新空闲与运行中重部署，Laminar 流水化 RL 后训练。HARP 面向异构训练，含 GPT 类 LLM 负载；HetAuto 优化跨集群自动并行，具体模型负载待确认。LLM 推理从 AdaServe 的请求级 speculative policy，到 FlexPipe 的 inflight pipeline refactoring、FineMoE 的 expert 级卸载、KUNSERVE 的参数级内存管理、MFS 的模型家族组件复用，决策粒度明显下沉；PARD 则面向通用推理流水线做主动请求丢弃。

这种“把一个大对象拆成可独立观测和调度的状态”并不局限于 LLM。TierScape 在多个压缩内存 tier 之间分配 page，MTTM 为多租户划分 fast memory 与 bandwidth，SwitchFS 把文件系统 metadata update 与前台 I/O 解耦，Ldc 把多副本中物理独立的 cache 改成逻辑共享的缓存。共同点是先暴露 parameter、expert、module、page、cache shard 或 metadata operation 等中间层状态，再让运行时根据负载、带宽、热度和 SLO 重组它们。

网络方向的显著特征是不再只替换拥塞控制算法，而是改造可观测性和数据路径。Learn-to-Probe 主动发 probe 使混淆的 network state 变得可辨，PatternSketch 把时序流量规律压入可重配数据平面，Themis 用交换机中间层让 commodity RNIC 支持 packet spraying，SmartNS 以 header-only TX 和 in-cache RX 绕开 SmartNIC memory-bandwidth 瓶颈。ECOTE、LCMP 又把光层故障、业务优先级、长途带宽价格和实时拥塞引入 WAN/RDMA 路由，说明新的优化目标是跨层约束下的业务结果，不只是单链路吞吐。

可靠性研究一端向更复杂的真实系统深入：NecoFuzz 通过 fuzz-harness VM 覆盖 nested virtualization，Thor 在完整企业区块链上组合多节点状态，LifeFuzz 按 Windows driver 跨 handler lifecycle 生成调用序列，Rose 从生产 trace 反推可重放的外部故障 schedule。另一端则从生产证据构建可检查的中间层：Concord 学习 network configuration contract，CSnake 拼接故障传播因果链，Aegis 把历史 change/incident 变成可追溯的风险规则，华为云经验报告则比较 concurrency testing、model checking 与 deductive verification 在不同成本—保证强度下的选择。

| 高频技术路线 | 约涉及论文数 | 对象/负载与主要做法 |
|---|---:|---|
| 细粒度状态拆分与运行时重组 | 至少 28 | 语言模型服务细分请求、MoE 专家、参数和流水阶段，多模态语言模型细分编码器/主干；内存、缓存与文件系统分别调度页、分片和元数据操作。 |
| 基于在线观测、预测或学习的控制 | 至少 23 | 语言模型服务按请求与资源需求选择执行计划；网络路由按链路信号选路径，内存管理按热度迁移，云变更按风险先例和功耗估计决策。 |
| 状态复用、压缩和避免搬运 | 至少 24 | 语言模型推理复用 KV、模型家族组件与参数分片；副本缓存共享数据，模型仓库压缩权重张量，GPU/FPGA 数据路径减少复制和搬运。 |
| 编译器、运行时与硬件边界的协同设计 | 至少 25 | 对象包括网络包处理、内存侧事务执行和 NPU/FPGA 上的计算图；按 DPU、PIM 与 chiplet（芯粒）的执行/互联特征调整布局、编译和调度，按各论文的具体计算任务区分适用范围。 |

Agent 相关工作终于出现，但是两篇都是 Agent Infra，而不是 Agent System 或 Agent for Systems。DMI 把截图坐标和 mouse/keyboard sequence 改为 access、state、observation 三类声明式 OS primitive，直接降低 computer-use Agent 的感知歧义和动作长度；AIMS 利用 Agent workflow 的 iteration/subtask 边界，在每一步选择本地 SLM 或云端 LLM，而不是对整个请求一次性路由。它们优化的都是“如何支持已存在的 Agent 工作流”，没有改写 Agent 自身的规划—行动—反馈机制。LLM-Empowered Static Binary Translation 使用 LLM 恢复 assembly/ABI/control-flow 语义并由传统工具生成、验证 AArch64 binary，它是 1 篇 LLM for Systems，但没有对运行中系统形成行动反馈闭环。Wayfinder、Aegis、PIP 虽然会自动搜索、判断或控制，仍是针对固定目标的专用优化器，不因“自动”就归为 Agent for Systems。因此严格口径下：Agent System 0 篇、Agent Infra 2 篇、Agent for Systems 0 篇、LLM for Systems 1 篇。

#### 变化

EuroSys 三届论文数从 71 增至 85，再增至 138；2026 的规模扩大会放大绝对数，但 AI/ML 系统的多标签占比仍从 31.0%、32.9% 上升到 39.1%，因而不只是总篇数增加。2024 的主线是在已有训推框架下拆 micro-batch、MoE task、kernel 和 graph partition；2025 开始把 conversation KV、RAG 知识块、model delta、intermediate activation 和 RLHF actor state 变成可管理状态；2026 则进一步覆盖训练、post-training、推理、模型更新、安全证明和 Agent 部署的全生命周期。

三年中更稳定的方法趋势是“变粗粒度固定配置为细粒度可重组状态”。2024 主要打开框架内部的新调度边界，2025 强调状态复用与跨阶段 layout transformation，2026 则把决策单位继续下沉到 speculative depth、expert、parameter、module、iteration、packet 和 accelerator component。同时，controller 的输入从单一 counter 扩展到主动探测、反事实估计、多资源预测、生产先例和故障因果链，表明研究重点已从“有一个调度器”转向“调度器是否真正看见了可决策的系统状态”。

Agent 趋势需要谨慎解读：2024 只有 1 篇一次性根因分析的 LLM for Systems，2025 在严格口径下没有 Agent/LLM for Systems 论文，2026 首次出现 2 篇 Agent Infra 与 1 篇 LLM for Systems，但仍没有 Agent System 或 Agent for Systems。这说明 EuroSys 开始把 Agent 视为需要 OS interface、模型路由和成本控制的新 workload，却还没有形成“让 Agent 自主管理系统”或“优化 Agent 内部规划环”的论文簇。

### NSDI

#### 2024

论文列表：[NSDI 2024 完整论文列表](evidence/venue-catalogs/NSDI-2024.md)

NSDI 2024 共收录 112 篇正式论文。以下采用多标签统计：同一篇工作可以同时属于云系统、网络测量和可靠性，比例不应相加。

| 研究问题 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| 视频、移动、无线与边缘系统 | 35 | 31.2% |
| 云、微服务、虚拟化与资源管理 | 32 | 28.6% |
| 可靠性、验证、测试与安全 | 31 | 27.7% |
| AI/ML 系统及学习驱动的系统机制 | 26 | 23.2% |
| 数据中心传输、拥塞控制、RDMA 与 collective | 18 | 16.1% |
| 存储、内存、缓存与 checkpoint | 18 | 16.1% |
| 可编程数据平面、网络测量与 telemetry | 13 | 11.6% |

本届的网络研究已经明显从“设计一个协议”扩展到端到端服务结果。视频与移动系统同时控制编码、码率、FEC、边缘资源和无线链路；云网络工作则把 path、queue、transport 和应用优先级串起来处理 tail latency。研究对象仍以 flow、packet、connection 和 service request 为主，LLM 相关论文主要关注开发/训练基础设施，尚未形成 agentic workload。

AI 系统开始进入 NSDI 的主航道，但焦点仍集中在大规模训练网络和数据路径：MegaScale 把 LLM 训练扩到万卡，训练表征/压缩、collective、checkpoint 与故障恢复成为网络系统问题；同时，多篇 learning-based congestion control、video adaptation 和 resource allocation 说明 ML 已被当作控制器或预测器使用。这里的“learning agent”通常是固定状态—动作空间里的 RL policy，不等于本报告所说的 LLM Agent。

可靠性工作反复使用“可重放/可验证的中间证据”。系统不直接从最终性能回归猜根因，而是保留 packet event、control-plane state、协议 transition 或 production trace，再用 differential execution、formal model 或 targeted fault injection 检查。网络测量则更多下沉到 programmable switch/NIC，在数据源附近压缩状态并把高价值信号送回控制面。

本届没有符合严格定义的 Agent System、Agent Infra、Agent for Systems 或 LLM for Systems。NetAssistant 虽提供自然语言式网络运维交互，但使用预定义 workflow 和传统 NLU 将请求映射到已有诊断流程，没有 LLM 自主规划—行动—反馈环；Cloud-LoRa 等在线 RL controller 也属于专用自动控制。

#### 2025

论文列表：[NSDI 2025 完整论文列表](evidence/venue-catalogs/NSDI-2025.md)

NSDI 2025 共收录 82 篇正式论文。论文总数较 2024 少，但研究簇更加集中，尤其是数据中心传输、存储/内存与训练通信。

| 研究问题 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| 数据中心传输、拥塞控制、RDMA 与 collective | 25 | 30.5% |
| 存储、内存、缓存与 checkpoint | 24 | 29.3% |
| 可靠性、验证、测试与安全 | 22 | 26.8% |
| AI/ML 系统及学习驱动的系统机制 | 19 | 23.2% |
| 云、微服务、虚拟化与资源管理 | 19 | 23.2% |
| 可编程数据平面、网络测量与 telemetry | 16 | 19.5% |
| 视频、移动、无线与边缘系统 | 11 | 13.4% |

LLM 训练与网络的交叉最为突出。Multiverse、SimAI 解决万卡 LLM 的网络/架构仿真，RLHFuse 拆分 rollout、reward 与 training stage，ByteCheckpoint 解耦 checkpoint 与并行布局，AutoCCL 在真实 compute–communication interference 下在线调 collective。研究不再假设通信库已经“调好”，而是把 collective 参数、pipeline bubble、gradient 丢失、checkpoint layout 和故障节点都纳入训练运行时。

推理与云服务开始采用更细的请求级控制。SuperServe 在共享权重 supernet 内为每个请求选择满足 accuracy–latency target 的 subnet；Prism 将推荐模型按 CPU/GPU subgraph 解耦部署；GREEN、Leopard、Quicksand 分别把碳强度、真实资源消耗和碎片化 CPU/内存带入调度。共同方法是先改变可调对象的边界，再做优化：从 VM/container 下沉到 subnet、subgraph、proclet、page 或 packet。

网络数据平面的主要趋势是暴露原本封闭的控制点。SCR 把 RDMA 每包 transport decision 交给软件而保留硬件 fast path，eTran 用 eBPF 在受保护内核里加载新 transport，P-ECMP 把 ECMP primitive 编译成精确 flow policy，AppNet 又把 RPC policy 从手工 sidecar 配置提升为可验证的高层语言。与此同时，Pyrrha、SIRD、State-Compute Replication 等工作通过新的等价类或状态边界减少 PFC、receiver scheduling 和 flow sharding 的结构性瓶颈。

本届有 1 篇 LLM for Systems：CEGS 用 GNN 检索并推广配置示例，再由 LLM 合成具体网络配置；它没有持续观察运行结果、执行修复并迭代，因此不归为 Agent for Systems。Agent System、Agent Infra 与 Agent for Systems 均为 0。Mutant、BFTBrain 等使用在线强化学习的控制器仍属于固定任务的传统 RL 系统。

#### 2026

论文列表：[NSDI 2026 完整论文列表](evidence/venue-catalogs/NSDI-2026.md)

NSDI 2026 共收录 150 篇正式论文，规模显著扩大。下表仍是多标签统计，主要用于识别研究密度而非互斥分类。

| 研究问题 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| AI/ML 系统及学习驱动的系统机制 | 49 | 32.7% |
| 可靠性、验证、测试与安全 | 44 | 29.3% |
| 存储、内存、缓存与 checkpoint | 44 | 29.3% |
| 云、微服务、虚拟化与资源管理 | 43 | 28.7% |
| 视频、移动、无线与边缘系统 | 34 | 22.7% |
| 数据中心传输、拥塞控制、RDMA 与 collective | 33 | 22.0% |
| 可编程数据平面、网络测量与 telemetry | 27 | 18.0% |

AI workload 已经贯穿网络、存储和云运行时。LLM 侧覆盖 MoE 专家/优化器解耦、RL 后训练、稀疏检查点和故障诊断；通用训练也研究异构参数服务器与 collective 调度。LLM 推理侧则围绕 token-level preemption、prefill/decode 切分、MoE all-to-all、跨模型 KV 复用、serverless cold start、分离式 KV memory 和 agent program 调度展开。热点不只是“把模型跑快”，而是管理 request、token、KV、expert、gradient、reward batch 和 program dependency 这些生命周期不同的状态。

网络控制研究出现两个相反但互补的方向。一类用更强模型恢复隐藏状态：UNUM 学历史网络 state embedding，Geminet 学可跨拓扑的优化 update operator，BayWatch 用动态贝叶斯模型选择 probe，NetNomos 用逻辑约束生成模型。另一类刻意减少对黑盒学习的依赖：OSCAR、CCC、FRCC 从 delay、可信度、flow count 建可分析控制律，Syntra 从 symbolic model 综合跨层 controller，Count-Based Abstractions、CCEval 则给性能验证和实验置信度明确边界。热门方法已经从“预测一个配置”演进到“同时说明观测何时可信、动作何时安全”。

生产系统论文强调跨层联合控制。ZooRoute、Harp 在 VPC overlay 事前维护健康候选路径；Bifrost 把 multipath reliability 放进 SmartNIC；LADR 统一避免、检测和恢复云游戏丢包；MAE 把 encoder 也接入 congestion loop；HEDGE 将 wavelength-specific optical fault 表成 probabilistic capacity。控制对象从单一路由/速率扩展到应用 QoE、编码、存储 I/O、光层容量和多域资源。

Agent 相关工作已经形成小而清晰的簇。AVA 是 1 篇 Agent System：它让 VLM Agent 围绕 Event Knowledge Graph 多步检索和生成，直接改进长视频任务中的规划—观察—迭代。DroidSpeak、JITServe、SYMPHONY、Cortex、Agentix 共 5 篇 Agent Infra，分别优化 compound-AI 的跨模型 KV、agent pipeline SLO、对话/工作流提示驱动的分离式 KV、远端知识语义缓存，以及 program-aware LLM call scheduling。Eywa 和 Themis 是 2 篇 LLM for Systems：LLM 分别参与协议模型和并发测试输入生成，但最终测试、oracle 和 directed fuzzing 仍由传统系统闭环完成。没有明确的 Agent for Systems 论文；S2Sim、Mortise、Syntra、MoCE 等虽能自动修复、调参或诊断，仍是固定目标和固定动作空间的专用系统。

#### 变化

NSDI 三届论文数为 112、82、150 篇；规模波动较大，因此更应看比例和研究对象。AI/ML 相关多标签占比从 23.2%、23.2% 上升到 32.7%，2026 的增量主要来自 LLM serving/post-training、AI cluster network 和 ML/生成模型用于网络，而不是传统分类模型重复出现。存储和内存也从通用 remote memory/cache，转向 KV cache、模型存储、checkpoint、CXL 与训练 I/O 等 AI 驱动的新访问模式。

方法上，2024 仍常以 flow、connection、service 和 edge session 为控制单位；2025 明显下沉到 packet、collective parameter、subnet、subgraph 和 proclet；2026 又把 token、KV layer、expert/optimizer state、reward batch、agent program 和 semantic knowledge 变成一等对象。粒度越来越细，但 controller 需要同时考虑的层次更多，因而 state estimation、可信度判断、形式化 guardrail 和生产 trace 校准变成高频配套技术。

Agent 方向呈现 0 → 1 篇 LLM for Systems → Agent System/Infra 与 LLM for Systems 同时出现的变化。2026 的 1 篇 Agent System、5 篇 Agent Infra、2 篇 LLM for Systems 说明 NSDI 已开始把 agentic program 的状态、依赖、知识访问和服务 SLO 当成真正的网络系统问题；但 Agent for Systems 仍为 0，说明“让通用 Agent 自主管理网络/云系统并在真实反馈中修正行动”尚未在本届形成成熟范式。

### FAST

#### 2024

论文列表：[FAST 2024 完整论文列表](evidence/venue-catalogs/FAST-2024.md)

FAST 2024 共收录 22 篇正式论文。下表按官方 session 统计，每篇只计入一个 session，因此比例可以相加。

| 官方方向 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| Key-Value Systems | 4 | 18.2% |
| Distributed Storage | 3 | 13.6% |
| Caching | 3 | 13.6% |
| File Systems | 3 | 13.6% |
| Flash Storage | 3 | 13.6% |
| Cloud Storage | 3 | 13.6% |
| AI and Storage | 3 | 13.6% |

这里的 Key-Value Systems 指按键读写数据的键值存储系统；它与前文 Attention 的 Key/Value Cache 是两类对象。Flash Storage 指 SSD 等闪存介质上的数据管理。

本届仍以典型存储问题为主体：文件系统数据路径、缓存、SSD 内部布局、KV replication/index 和云存储冗余。最稳定的方法主线是消除同一数据或状态在层间重复搬运。TeRM 让 SSD 扩展的 RDMA memory 不经过 CPU/page-fault critical path，FLAC 将 VM mapping 与 DRAM cache 合并以实现 zero-copy，NetMigrate 用 switch 记录 shard migration progress，MinFlow 联合重写 serverless shuffle topology 和 function placement。很多性能问题的根因并不是介质慢，而是原软件层次重复转换、复制或等待。

另一条主线是把原本固定的系统选择变成在线可调策略。Lustre 工作在 buffered/direct I/O 间根据请求、锁和内存切换，Symbiosis 动态协调 application 与 kernel cache，OmniCache 同时选择 host/device cache 和 compute placement，MiDAS 根据 update-interval model 改变 log group 数量与大小。这里虽出现 model-driven/Markov 方法，但 controller 都有固定目标和动作空间，不属于 Agent。

“AI and Storage” 还处于早期交叉阶段。COLE 用 learned index 改造 blockchain 多版本状态，Baleen 用 episode-level ML 联合 flash admission/prefetch，Seraph 则借现代 SSD 的随机访问能力重设外存图计算。AI workload 本身尚未成为主要服务对象，也没有 Agent System、Agent Infra、Agent for Systems 或 LLM for Systems。

#### 2025

论文列表：[FAST 2025 完整论文列表](evidence/venue-catalogs/FAST-2025.md)

FAST 2025 共收录 36 篇正式论文。两个 ML session 合计 9 篇，占 25.0%，AI 与存储的交叉已从单个 learned policy 扩展为明确研究簇。

| 官方方向 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| Machine Learning and Storage + More Machine Learning | 9 | 25.0% |
| File Systems | 5 | 13.9% |
| Hardware Assist | 5 | 13.9% |
| Security, Integrity, and Consistency | 5 | 13.9% |
| Cloud Storage | 4 | 11.1% |
| Compression and Deduplication | 4 | 11.1% |
| Storage Diversity and Heterogeneity | 4 | 11.1% |

AI/ML 相关论文可分成两个方向。第一类是存储支撑具体推理/训练负载：Mooncake 为 LLM 组织全局 KVCache storage，IMPRESS 为 LLM 只加载关键 prefix KV；通用 GPU 文件系统 GeminiFS 提供直达 NVMe 接口，LeapGNN 在 GNN 训练中迁移网络参数，减少搬运顶点特征。第二类是学习方法优化存储：3L-Cache 降低 learning eviction 的线上成本，HiDPU/PIMLex 用 learned/hybrid index 适配 DPU 和 PIM，Baleen 延续 ML admission/prefetch。两类工作的共同点都是让模型语义进入 I/O 决策，而非只在应用层调用通用文件接口。

硬件协同开始系统性改变数据管理边界。HaSiS 借 computational-storage compression 让 HTAP 单 index 同时服务事务与分析，AegonKV/D2FS 将 value GC 或 filesystem GC 下沉 SmartSSD/FTL，on-device execution 延续 data-dependent read chain，ShiftLock 则把锁移交变成 client-to-client RDMA protocol。研究重点不再是“有没有 offload”，而是 offload 后谁拥有 metadata、如何恢复一致性、前后台路径如何互不干扰。

正确性研究围绕已有硬件/软件保证做状态空间裁剪或契约补齐。Silhouette 先验证 journaling/replication mechanism，再只枚举未保护 PM store；OPIMQ 将跨 queue/thread 的 write order 传到 FTL；AWUPF 工作把 SSD 已保证的原子写单元用作 transaction primitive；AtomicDisk 又说明完整性和 crash consistency 仍不足以防止未 sync transient state 被恶意观察。性能与可靠性因而越来越由跨层契约共同决定。

本届没有严格意义上的 Agent System、Agent Infra、Agent for Systems 或 LLM for Systems。Mooncake、IMPRESS 是通用 LLM serving/storage infrastructure，但没有针对多步 Agent workflow 的特殊状态、依赖或副作用机制，因此不重复标为 Agent Infra。

#### 2026

论文列表：[FAST 2026 完整论文列表](evidence/venue-catalogs/FAST-2026.md)

FAST 2026 共收录 44 篇正式论文。两个 AI and LLMs session 合计 9 篇，占 20.5%；绝对数与 2025 相同，但研究对象从通用 ML/cache/index 更集中地转向 LLM 状态、训练 checkpoint、AI I/O 与 Agent。

| 官方方向 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| AI and LLMs I + II | 9 | 20.5% |
| Cloud Technologies I + II | 8 | 18.2% |
| Indexing | 5 | 11.4% |
| SSDs and CXL | 5 | 11.4% |
| Tiering, Mobile, and SSDs | 5 | 11.4% |
| Virtualization | 4 | 9.1% |
| Integrity | 4 | 9.1% |
| OS | 4 | 9.1% |

LLM 存储系统从“保存更多 KV”转向理解 KV 和 workflow 的语义。SolidAttention 用 sparse-attention token locality 决定 SSD block/prefetch；CacheSlide 识别 Agent prompt 中相对位置不变的可复用段；Bidaw 让 compute scheduler 看见 KV tier、storage eviction 看见对话 response；PPC/MAIO 用模型加载模板控制 page cache；AITURBO 又用 grouped I/O API 把 checkpoint/KV 访问意图交给 storage layer。研究热点是暴露比 read/write 更高层的模型状态，让底层可安全地少读、预取或重排。

状态压缩分为不同对象：GCR 为 GPU 进程检查点推导脏缓冲区；AdaCheck 识别语言模型训练中参数/优化器状态的冗余；Seneca 管理训练样本的编码、解码、增强缓存，并跨作业共享预处理结果。这些工作都先回答“哪些状态必须保留、哪些可重建”，再优化 I/O，而不是单纯增加 checkpoint bandwidth。

传统存储方向呈现“新硬件需要新的软件契约”。Cylon、Xerxes、WARP 分别为 CXL-SSD、最新 CXL protocol 和 FDP SSD 提供可校准的 emulator；ZUFS 需要 firmware 到 Android 全栈共同维护 buffer、order 和 GC；FS-PI 补齐 application、io_uring、block layer、XFS/BTRFS 到设备的 end-to-end integrity metadata path。与此同时，RASK、OdinANN、HATS、DMTree 表明 index 也从静态数据结构转向持续 insert、背景 compaction 和 disaggregated coordination 下的在线系统。

Agent 相关工作有 2 篇，但分属不同范式。CacheSlide 是 1 篇 Agent Infra：它利用 Agent prompt 固定段相对顺序的 workload 特征优化跨位置 KV reuse，不改变 Agent 的规划机制。SYSSPEC 是 1 篇 Agent for Systems：SpecCompiler 生成文件系统代码，SpecValidator 对照功能/模块/并发规范验证，并将错误反馈给生成器 retry；DAG spec patch 驱动后续演化，形成明确的感知/验证—行动—反馈闭环。它不是 Agent System，因为研究对象是“让 Agent 构建和演化文件系统”，不是改进 Agent 自身的一般规划/记忆结构。严格口径下 Agent System 0、Agent Infra 1、Agent for Systems 1、LLM for Systems 0。

#### 变化

FAST 三届论文数从 22 增至 36、44。官方 AI/ML session 从 2024 年 3 篇（13.6%）扩展到 2025 年 9 篇（25.0%），2026 仍为 9 篇（20.5%）；比例回落主要来自会议总规模增加，但研究内容更靠近 LLM/Agent。2024 的 AI 是 learned index、cache policy 和外存图；2025 同时出现 LLM KV storage、GPU direct file system 与多种 learned cache/index；2026 则直接处理 Agent prompt、multi-round KV、LLM model loading、训练 checkpoint 和 specification-guided Agent coding。

三年更普遍的演进是“介质感知”转向“语义感知”。2024 系统主要依据 I/O size、hotness、lock、SSD layout 做路径选择；2025 开始理解 tensor importance、graph feature locality、transaction/analytical access、consistency mechanism；2026 又理解 prompt segment、conversation future access、tensor redundancy、grouped AI I/O 和 system specification。随着上层语义下沉，存储接口不再只是 byte/block/file，而成为连接模型、runtime、OS 与硬件的可编程契约。

Agent 方向从 2024/2025 的空白发展到 2026 的 1 篇 Agent Infra 和 1 篇 Agent for Systems。值得注意的是，FAST 的切入点都与“状态”直接相关：一篇复用 Agent prompt 产生的 KV state，另一篇用形式化 specification 和 validator feedback 约束 Agent 生成的持久系统。这与 FAST 的传统优势一致，也说明 Agent 研究进入存储领域时，首先出现的是状态复用、正确性和可恢复演化，而不是通用规划算法。

### ICDCS

#### 2024

论文列表：[ICDCS 2024 完整论文列表](evidence/venue-catalogs/ICDCS-2024.md)

ICDCS 2024 主会共收录 121 篇 Regular Submissions。下表将官方的 30 个细分 session 合并为宏观方向，每篇只计入一个官方 session。

| 合并方向 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| AI/ML 与边缘智能 | 20 | 16.5% |
| 联邦学习：效率、公平、激励与安全 | 20 | 16.5% |
| 分布式设计、容错与可靠性 | 16 | 13.2% |
| 无线、车联网、IoT 与数据中心网络 | 16 | 13.2% |
| 区块链 | 12 | 9.9% |
| 云存储、云通信与数据中心 | 12 | 9.9% |
| 网络安全、隐私与用户认证 | 12 | 9.9% |
| 边缘部署、定价与网络优化 | 8 | 6.6% |
| 量子网络 | 5 | 4.1% |

2024 的 AI 重心仍是“把模型放到分布式/边缘环境里”。QUART 按 LLM 流水阶段识别瓶颈并用 FaaS 快速扩副本；[Voltage](evidence/venue-catalogs/ICDCS-2024.md#voltage) 覆盖早期 LLM（GPT-2）及 BERT/ViT 的边缘协同推理；TrimCaching 研究通用模型共享参数缓存，动机包含 LLM/LoRA，未专门优化 LLM 生成。这些工作已经出现 LLM workload，但研究对象是模型训推和模型分发，不是 Agent workflow。

联邦学习占 20 篇，与 AI/ML 主线并列。方法从单纯减少 gradient/update 通信，扩展到 client fairness、定价激励、恶意 client/server、secure aggregation 与 local asynchrony。一个共同倾向是把实际系统异构——可用客户端、带宽、数据偏斜、可靠性和参与意愿——直接写进聚合与选择策略，而不再默认 client 同质。

严格口径下，2024 年 Agent System、Agent Infra、Agent for Systems 和 LLM for Systems 均为 0。标题中的 malicious agents、mobile agents 以及 multi-agent reinforcement learning 分别指分布式算法节点、移动载体或固定 MARL policy，不应与 LLM Agent 混同。

#### 2025

论文列表：[ICDCS 2025 完整论文列表](evidence/venue-catalogs/ICDCS-2025.md)

ICDCS 2025 主会 Main Tracks 共收录 103 篇论文。DS4AI/ML 与 AI/ML4DS 合计 31 篇，占 30.1%，表明会议同时关注“系统服务 AI”和“AI 服务分布式系统”。

| 合并方向 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| DS4AI/ML + AI/ML4DS | 31 | 30.1% |
| Security & Privacy | 13 | 12.6% |
| Blockchain & Databases | 11 | 10.7% |
| IoT & CPS | 9 | 8.7% |
| Edge Computing | 8 | 7.8% |
| Emerging and Deployed Systems | 8 | 7.8% |
| Distributed Algorithms | 8 | 7.8% |
| Cloud + Big Data + OS/Middleware | 8 | 7.8% |
| Mobile Computing | 4 | 3.9% |
| Distributed Fault Tolerance | 3 | 2.9% |

DS4AI/ML 指用分布式系统支撑 AI 训练与推理，AI/ML4DS 指用学习方法优化分布式系统；CPS 是传感、计算与物理设备相互作用的信息物理系统。

LLM 方向从单点部署扩展到训练、推理和 workflow scheduling：Mast 重排 attention/MoE 层的计算通信，Shuffle-Exchange 重设 LLM collective communication，MCaM 联合调度与 HBM–DRAM 分层缓存复用多轮 LLM 会话 KV。[ACME](evidence/venue-catalogs/ICDCS-2025.md#acme) 则以视觉 Transformer（ViT）验证个性化架构定制。研究单位从「整个模型」继续下沉到 expert/task、KV layer/token 和 workflow stage。

LLMSched 是本届唯一篇按严格口径计入 Agent Infra 的工作。它面向 LLM、API 和外部模块组成的 compound LLM application，用 Bayesian network 随执行进度更新 DAG 结构/时长不确定性，再优先执行最能消除不确定性的 stage。它不改变 Agent 的规划或记忆机制，而是为具有 Agent-like 动态 workflow 的应用提供调度支持，因此归 Agent Infra 而非 Agent System。本届 Agent System 0、Agent Infra 1、Agent for Systems 0、LLM for Systems 0。

#### 2026

论文列表：[ICDCS 2026 完整论文列表](evidence/venue-catalogs/ICDCS-2026.md)

ICDCS 2026 Main Technical Sessions 共收录 138 篇论文。Edge Computing 和 AI 两类合计 56 篇，占 40.6%；其中 5 个官方 session 的名称直接包含 Large Language Model，合计 20 篇，占 14.5%。

| 合并方向 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| Edge Computing | 32 | 23.2% |
| AI | 24 | 17.4% |
| Security / Privacy / Trust | 16 | 11.6% |
| Blockchain | 12 | 8.7% |
| Cloud Computing | 12 | 8.7% |
| Fault Tolerance + Big Data | 12 | 8.7% |
| Distributed Algorithms | 8 | 5.8% |
| Applications / Digital Twins | 8 | 5.8% |
| IoT / CPS | 8 | 5.8% |
| OS / Middleware | 4 | 2.9% |
| Real-Time Networking | 2 | 1.4% |

LLM 训推系统成为最明显的新热点。推理端同时研究 on-device cold start、地理分布式 KV migration、edge KV reuse、NVMe-direct KV offload、量化 GEMM kernel 动态选择、consumer GPU 分布式 serving 和 edge tensor parallelism；训练端研究 LLM 的层次异步通信、成本优化与集群 hang/slowdown tracing，另有文生图扩散模型的流水训练。方法上的共同点是让 model/KV/workflow 语义直接驱动内存、缓存、kernel、调度和容错，而不再只看 request size 和 GPU utilization。

Agent 相关工作形成了可区分的四类。Agent System 有 2 篇：EHRR 在 MCP server/tool 两层同时按语义、成功率、时延和价格选 action，EDAgent 用事件通信和增量状态同步解耦 multi-agent 依赖与执行顺序。Agent Infra 有 3 篇：Maestro 按 Agent role/workflow 做跨集群 GPU 调度，AgentDID 为短生命、可迁移 Agent 验证身份与动态执行状态，Internet of Agents 工作提供隐私且负载均衡的语义检索。

Agent for Systems 有 1 篇 Panorama：多 Agent automatic heuristic design 通过 panorama diagnostic feedback 反复生成、评估和改进车联网子信道分配启发式，形成面向系统优化的明确闭环。LLM for Systems 有 1 篇 FLARE：LLM 只在训练期根据节点、任务、链路和 failure feedback 生成 semantic cue 引导 DRL，权重随后退火到零，线上 offloading 不运行 LLM 或 Agent 环。严格口径合计为 Agent System 2、Agent Infra 3、Agent for Systems 1、LLM for Systems 1。

#### 变化

ICDCS 主会规模从 121 篇、103 篇上升到 138 篇。三年不只是论文数增长，AI 与分布式系统的接口也在改变：2024 主要解决模型在 edge/FaaS 上怎样放、分、传，并大量研究联邦学习；2025 下沉到 MoE task、collective communication、个性化架构、KV tier 和 compound workflow；2026 则同时覆盖 LLM serving/training 的全栈以及 Agent 的工具路由、协作执行、GPU 调度、身份和检索服务。

方法走向也从「针对一个分布式子问题设计算法」变为「联合多层状态做决策」。典型例子包括 scheduler 与 KV tier 联合、node–cluster–global 三级 workflow scheduling、LLM 语义与 DRL 表示的训练期解耦，以及 MCP 中语义/可靠性/时延/货币成本的联合 tool routing。这个走向与我们关心的机器学习系统平台、调度、存储、训推系统和 Agent 基础设施高度重合。

### SoCC

#### 2024

论文列表：[SoCC 2024 完整论文列表](evidence/venue-catalogs/SoCC-2024.md)

SoCC 2024 正式 proceedings 共收录 63 篇论文。下表采用互斥主方向，每篇只计入最主要的研究问题。

| 主方向 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| AI/ML 系统 | 20 | 31.7% |
| Serverless/FaaS 与云运行时 | 13 | 20.6% |
| 存储、数据、数据库与流系统 | 9 | 14.3% |
| 云资源调度、运维与可靠性 | 8 | 12.7% |
| 可持续与碳感知计算 | 5 | 7.9% |
| 网络、边缘与分布式协议 | 5 | 7.9% |
| 安全、隐私与隔离 | 3 | 4.8% |

Serverless/FaaS 由平台按调用或负载管理执行实例；冷启动指新实例准备运行环境、加载代码或模型所需的等待。相关研究优化启动、实例复用、状态保存与弹性分配。

AI/ML 已是最大方向，但研究对象仍以「把模型可靠且经济地放进云里」为主。QLM 在单个用户请求层面统一编排交互式与 batch LLM 请求的排队、驱逐、负载均衡和模型换入；MoEsaic 在 MoE LLM 服务中跨租户识别相同 expert，既去重显存中的 expert 权重又合并发往同一 expert 的请求；Trainium 工作则把数据、tensor 和 pipeline parallelism 落到 AWS 自研加速器集群。训练侧同时出现异构 GPU 公平调度、在线训练弹性扩缩、梯度压缩和 checkpoint 动态量化，说明大模型只是更大 AI 系统簇的一部分。

Serverless/FaaS 的 13 篇论文覆盖冷启动、snapshot、MicroVM 内存弹性、网络 sidecar、状态管理、workflow 和 serverless ML。共同方法是把原来以整个 VM/容器为单位的管理下沉到 snapshot page、函数状态、loop iteration 或请求队列，再按实时负载和 SLO 做局部迁移、预取或扩缩容。另有 5 篇可持续计算工作同时研究 operational carbon、embodied carbon、CDN 空间迁移和模块化数据中心，碳开始成为与 latency/cost 并列的调度信号。

严格口径下，本届 Agent for Systems 1 篇，Agent System、Agent Infra 和 LLM for Systems 均为 0。Building AI Agents for Autonomous Clouds 用 AIOpsLab 部署应用、注入故障、向 Agent 暴露 telemetry 与 cloud API，并在 Agent 的诊断—行动—环境反馈闭环中评价恢复效果；研究对象是执行云运维任务的 Agent，因而归 Agent for Systems。Vista、Deoxys 是传统 ML/因果 ML for Systems，QLM、MoEsaic 和 Trainium 是 AI Infra，均不能因使用 AI 或出现控制组件而算作 Agent。

#### 2025

论文列表：[SoCC 2025 完整论文列表](evidence/venue-catalogs/SoCC-2025.md)

SoCC 2025 正式 proceedings 共收录 67 篇论文。明确涉及 LLM、LMM、compound AI 或 AI-agent traffic 的论文有 10 篇，占 14.9%。

| 主方向 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| AI/ML 系统与 GPU 基础设施 | 30 | 44.8% |
| 存储、内存、数据库与数据系统 | 13 | 19.4% |
| 云原生、Serverless、容器编排与通用调度 | 11 | 16.4% |
| 共识、网络、运行时与可观测性 | 7 | 10.4% |
| 可持续数据中心、能源与 CPU 资源效率 | 6 | 9.0% |

最明显的变化是生产 AI workload 成为云资源管理的主要设计对象。LLM 侧，Oneiros 不交换持续变化的 KV，而把非活跃模型的静态参数内存重映射给活跃 KV；AdaSpec 根据实时负载和配置选择 speculative decoding 策略；Cauchy 把 prefill/decode 放到不同类型 GPU，并在 GPU combo 内外分层调度请求；ModServe 又把多模态 LLM 按 modality 和 stage 拆分资源。研究粒度已从「给一个模型分几张卡」下沉到 model stage、adapter、KV layer、request 和 token-generation phase。

Compound AI 与训练也形成独立系统问题。DyOrc 面向按中间结果才决定后续组件的动态 workflow，把共享模型变成可独立伸缩的服务，跨 workflow 在线 batching，并以 speculative scheduling 和 proactive loading 隐藏分支与冷启动；Symbiosis 让多租户共享冻结的 LLM 基座，把私有 adapter 推理或微调留在各自资源域；10Cache 则按 LLM 训练的 tensor 执行顺序协调 GPU、CPU 和 NVMe 缓存与预取。与此同时，storage、serverless 和 sustainability 没有消失，而是开始把 GPU QoS、跨站点功率、水生命周期成本等状态纳入同一控制回路。

严格口径下，Agent Infra 2 篇，Agent System、Agent for Systems 和 LLM for Systems 均为 0。DyOrc 同时服务 multi-agent debate 等动态组合工作流，属于覆盖范围较宽的 Compound AI/Agent Infra；Rethinking Web Cache Design for the AI Era 把低复用、高容量的 AI-agent 请求作为独立 workload class，通过 cache tier 与 admission/eviction 隔离保护人类流量，也属于 Agent workload-specific infra。MARLess 中的 agent 是传统 MARL policy，Digital Twin 的 actor-critic 和 ALAP 的 online learner 也不是 LLM Agent。

#### 2026

论文列表：[SoCC 2026 第一轮论文列表（非最终完整名单）](evidence/venue-catalogs/SoCC-2026.md)

截至 2026 年 9 月 20 日，SoCC 2026 只公布了 Round 1 的 19 篇录用论文，第二轮通知日期是 9 月 26 日；因此以下数字是当前快照，不代表最终 proceedings，也不用于和前两届比较会议规模。标题明确涉及 LLM 或 Agent 的论文有 6 篇，占当前名单的 31.6%。

| 当前第一轮主方向 | 论文数 | 占 19 篇比例 |
|---|---:|---:|
| AI/ML、Agent 与 GPU 云系统 | 11 | 57.9% |
| 网络、RDMA 与流量处理 | 3 | 15.8% |
| 数据库、组播与复制协议 | 3 | 15.8% |
| 云弹性与请求路由 | 1 | 5.3% |
| 内核隔离与干扰分析 | 1 | 5.3% |

当前论文继续强化 SLO、成本与异构资源的联合控制。Medha 将 LLM 的百万 token 长 prefill 切成可抢占 chunk，用 adaptive chunking、stream pipeline/KV-cache parallelism 和 relative-slack scheduling 避免长请求阻塞短交互请求；PEACE 对神经网络训练/推理与科学 CUDA 作业的 GPU 混部，联合建模功率、频率与 MPS 空间切分；Spandana 用逐请求 VM–FaaS 分流保护严格 SLO，再以较慢的全局控制器优化容量成本。MosaicKV 的标题明确面向 LLM 多租户 KV 虚拟化；另一篇 Tessera 研究合同驱动的成本/SLO 优化，对象细节待正文确认，不能仅凭同名系统推断为 LLM。

Agent 方向目前有 1 篇 Agent Infra 和 1 篇 Agent System Evaluation，但核心 Agent System 机制、Agent for Systems、LLM for Systems 均为 0。Cadence 研究 disaggregated agent cloud 各资源池之间会沿 workflow 传播的耦合竞争，目标是优化承载规划—工具调用—反馈链的基础设施，不改变 Agent 自身算法。Evaluating Agentic Systems Across the Lifecycle 则把 drift 与 success criteria 组织到 Agent 生命周期中，研究对象是 Agent System 的评测方法；由于摘要尚未公开，不能进一步声称它改进了规划、记忆或行动—反馈机制。

#### 变化

SoCC 2024、2025 的完整论文数为 63、67；2026 目前只有第一轮 19 篇，不能据此判断会议规模变化。可以可靠比较的是方向结构：2024 仍是 Serverless、云运行时和通用资源管理承接第一批 LLM workload；2025 AI/ML 与 GPU 基础设施已占 44.8%，并覆盖 KV、P/D 异构部署、多模态 stage、adapter 训推和动态 Compound AI workflow；2026 第一轮又直接出现 Agent cloud contention、Agent 生命周期评测、多租户 KV 虚拟化和长上下文抢占调度。

三年的共同演进是决策粒度持续细化、跨层状态持续增多。早期方案多在模型、实例或函数层面扩缩容；随后开始同时观察 request SLO、prefill/decode stage、KV 层级、adapter、GPU partition、供电与网络；当前工作进一步按 chunk、flow、connection-table segment 和 contract 做控制。对于我们关注的机器学习系统平台、调度、存储、训推系统与 Agent Infra，SoCC 的价值正在于把这些组件放回真实多租户云环境，研究它们如何在成本、隔离、弹性和 SLO 约束下一起工作。

### ASPLOS

#### 2024

论文列表：[ASPLOS 2024 完整论文列表](evidence/venue-catalogs/ASPLOS-2024.md)

ASPLOS 2024 主会跨四卷 proceedings 共收录 193 篇论文。下表按每篇最主要的研究问题做互斥归类；AI/ML 系统是最大方向，但编译、可信计算、体系结构、存储和分布式系统仍共同构成会议主体。

| 主方向 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| AI/ML 系统 | 50 | 25.9% |
| 编译器与程序设计 | 29 | 15.0% |
| 安全、隐私与可信计算 | 26 | 13.5% |
| 体系结构与加速器 | 19 | 9.8% |
| 存储与内存系统 | 17 | 8.8% |
| 云与分布式系统 | 17 | 8.8% |
| 量子计算 | 14 | 7.3% |
| 边缘、移动与嵌入式 | 9 | 4.7% |
| 高性能与数据系统 | 7 | 3.6% |
| 可持续与能源系统 | 5 | 2.6% |

AI/ML 论文已经形成从训练到服务、从软件到硬件的完整栈。训练侧的 Centauri、T3、PrimePar、AdaPipe 和 Slapo 围绕 LLM 训练，从通信切分、细粒度触发、并行计划和调度语言寻找计算—通信重叠；LLM 服务侧的 SpecInfer、ExeGPT 和 SpotServe 把 speculative tree、SLO 约束以及抢占式云实例状态写入请求调度；GMLake、POLCA 又将显存碎片和功率画像变成运行时控制对象。会议关注的已不是单个加速 kernel，而是模型并行、runtime、内存、网络和资源策略如何共同决定端到端效率。

以 LLM 或大 Transformer 为核心对象的论文至少 14 篇，占 7.3%。除通用训推系统外，AttAcc、SpecPIM、NeuPIMs 和 IANUS 等工作把 attention、speculative decoding 或 batched inference 映射到 PIM/NPU 异构结构，显示 ASPLOS 的典型路径是从 workload 的算子与数据流特征反推硬件—系统接口。与此同时，编译与 runtime 有 29 篇，覆盖 MLIR、tensor compiler、动态 shape、程序综合、二进制提升与插桩；安全与隐私有 26 篇，覆盖侧信道、Rowhammer、内存安全、TEE、机密 VM 和密码计算，跨层协同仍是会议最鲜明的共同方法。

严格口径下，本届 Agent System、Agent Infra、Agent for Systems 和 LLM for Systems 均为 0。虽然 LLM Infra 已经相当密集，但这些系统处理的是训练、推理、显存、通信和能耗，没有以多步规划—工具行动—环境反馈为工作负载特征，也没有让 LLM/Agent 执行系统任务。MulBERRY 中的 multi-agent 指传统多智能体强化学习 UAV swarm，不纳入 LLM Agent 分类。

#### 2025

论文列表：[ASPLOS 2025 完整论文列表](evidence/venue-catalogs/ASPLOS-2025.md)

ASPLOS 2025 主会跨三卷 proceedings 共收录 184 篇论文。AI/ML 系统与加速、传统体系结构/内存两类合计 105 篇，占 57.1%，说明 AI workload 已成为体系结构与系统研究的主要牵引力，同时没有挤掉编译、安全、云和量子等经典板块。

| 主方向 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| AI/ML 系统与加速 | 53 | 28.8% |
| 体系结构、加速器、内存与存储 | 52 | 28.3% |
| 编译、测试、安全与验证 | 39 | 21.2% |
| 云、分布式、Serverless、网络与可观测性 | 25 | 13.6% |
| 量子与同态计算 | 15 | 8.2% |

LLM/MoE/serving 的三个官方专场有 15 篇，占 8.2%；若按标题显式出现 LLM、RAG、MoE 或 CoE 统计则有 21 篇，占 11.4%。LLM 服务侧的研究单位已经从「一个模型占几张 GPU」下沉到请求阶段和状态：FlashGen 跨 GPU、CPU 与 SSD 保存多轮对话 KV，POD-Attention 在同一 SM 内重叠 compute-bound prefill 与 bandwidth-bound decode，Helix 用同一容量图联合决定异构 GPU 上的 layer placement 与 request routing，TAPAS 又把机架温度、功率、SaaS request routing 和模型配置放入一个控制面。共同热点是围绕 KV 生命周期、prefill/decode 不对称性、异构网络和 SLO 联合调度。

训练方向突出动态并行和生产约束。FlexSP 按 LLM 每步的序列长度组合选择序列并行，Vela 支撑千卡级生产 LLM 训练；Spindle 则拆解多任务多模态模型的依赖并搜索并行方案；MoE 通信、checkpoint、故障恢复和共享校园集群也各自形成系统问题。CXL、PIM、NPU、DPU 与 FPGA 论文普遍采用 hardware–compiler–runtime co-design：上层先暴露 tensor、稀疏性、密文层级或 I/O 语义，底层再据此安排数据移动和执行位置，而不是单独增加一个加速器。

本届四类 Agent 各 1 篇。ReCA 是 Agent System：它联合设计多具身 Agent 的长短期记忆、分层协作规划、多步执行与异构硬件，直接改变规划—行动闭环。Ayo 是 Agent Infra：它把含 LLM 和非 LLM module 的应用展开为 primitive-level dataflow，在模块间统一流水和调度。KernelGPT 是 Agent for Systems：LLM 生成 syscall specification，Syzkaller 执行验证并把错误反馈给 LLM 反复修复。MetaMut 是 LLM for Systems：LLM 离线生成 compiler mutation operator，运行时 fuzzing 不需要自主 Agent 环。FleetIO 使用传统 MARL policy，不计入 LLM Agent。

#### 2026

论文列表：[ASPLOS 2026 完整论文列表](evidence/venue-catalogs/ASPLOS-2026.md)

ASPLOS 2026 官网页眉写“167 unique papers”，但当前主会 program 实际有 168 个标题与作者均不重复的 paper card，且全部能对齐正式 DOI；因此列表和下表保留全部 168 篇，不为匹配错误页眉任意删除论文。54 篇有可核验公开 PDF，其余条目在没有公开摘要或正文时明确限制为题录级判断。

| 主方向 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| ML 系统、GPU 与加速器 | 53 | 31.5% |
| LLM 与生成式 AI 系统 | 35 | 20.8% |
| 安全、可靠性、验证与测试 | 22 | 13.1% |
| 内存、存储与解耦资源 | 19 | 11.3% |
| 量子、FHE 与新型计算 | 18 | 10.7% |
| 编译、PL 与处理器微体系结构 | 15 | 8.9% |
| 云、网络与 Serverless | 6 | 3.6% |

AI/ML 相关两类合计 88 篇，占 52.4%，第一次超过全体论文的一半；LLM 与生成式 AI 本身已有 35 篇。LLM serving 研究集中在动态负载与阶段不对称：MuxWise、Bullet、QoServe 和 Shift Parallelism 分别在单 GPU 内复用 prefill/decode、做时空资源编排、统一不同 QoS 请求和在线切换并行策略；ZipServ、SwiftSpec、SpeContext 又处理权重/KV 压缩、分离式 speculative decoding 和长上下文稀疏性。训练侧则覆盖 sub-byte mixed precision、微秒级流量监测、superchip offload、MoE 和通信压缩。热门方法不再只是新增算子，而是让 runtime 根据 SLO、队列、KV、SM/带宽和流量测量在线改变执行方案。

硬件—软件共同设计仍是另一半主线。STARC、Mugi、Ouroboros 等工作把 token、value 或 pipeline 粒度映射到 PIM/CIM；内存与存储论文围绕 CXL、远端资源、cache 和预取器重设数据移动；编译论文通过专用 DSL/IR、MLIR lowering、形式验证和反馈搜索连接高层程序与异构硬件。ASPLOS 因而与 MLSys/SoCC 的区别更清楚：同样研究 LLM 训推，但更常从指令、kernel、memory hierarchy、编译表示和芯片数据流切入。

严格口径下，Agent System 为 0，Agent Infra 2 篇，Agent for Systems 2 篇，LLM for Systems 3 篇。FastTTS 把边缘 Agent 的多路径 test-time scaling 变成显存受限的生成—验证调度，CREATE 为 LLM planner 与 RL controller 组成的具身 Agent 做跨层容错，二者属于 Agent Infra。LPO 用 LLM 提议 peephole rewrite、形式验证并反馈失败，LOOPRAG 让检索、编译、测试与性能结果驱动下一轮循环变换，二者属于 Agent for Systems。Once4All、CacheMind 和 PF-LLM 分别让 LLM 离线合成 SMT fuzzing generator、解释 cache trace、生成硬件预取提示，但没有自主行动闭环，归 LLM for Systems。另有 1 篇 Compound AI System 表征工作，不在四分类中硬塞为 Agent。

#### 变化

ASPLOS 三届主会规模为 193、184、168 篇；2026 的数量下降不影响 AI 方向绝对扩张。AI/ML 主方向从 2024 年 50 篇（25.9%）、2025 年 53 篇（28.8%），发展到 2026 年 ML 系统 53 篇加 LLM/生成式 AI 35 篇（合计 52.4%）。LLM 核心对象从 2024 年至少 14 篇（7.3%），增至 2025 年标题显式相关 21 篇（11.4%），再到 2026 年独立方向 35 篇（20.8%）。这说明大模型从若干训练/推理 workload，演变成足以重组 session 和技术栈的系统对象。

研究粒度也在连续下沉。2024 主要联合模型并行、通信、显存和 PIM/NPU；2025 进一步处理每步 sequence length、prefill/decode、KV 生命周期、异构网络、机架功率和 serverless materialization；2026 则把决策细化到 SM、token、搜索路径、微秒级流量和在线并行策略切换。与此同时，Agent 方向从 2024 年空白，发展到 2025 年四类各 1 篇，再到 2026 年以 Agent Infra、Agent for Systems 和 LLM for Systems 为主、核心 Agent System 为 0。对我们的选题而言，ASPLOS 当前最强的交集是 LLM/Agent workload 与编译、runtime、内存、互连、GPU/PIM 的跨层系统，而不是纯 Agent 算法。

### PPoPP

#### 2024

论文列表：[PPoPP 2024 完整论文列表](evidence/venue-catalogs/PPoPP-2024.md)

PPoPP 2024 主会共收录 32 篇长文；正式 proceedings 中另有 12 篇 poster 和 1 篇 keynote，均未混入列表。

| 主方向 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| 并发、同步与内存回收 | 7 | 21.9% |
| AI/ML 并行系统 | 5 | 15.6% |
| 图算法与图处理 | 5 | 15.6% |
| GPU、稀疏与张量计算 | 5 | 15.6% |
| 编译与程序分析 | 3 | 9.4% |
| HPC 与科学计算 | 3 | 9.4% |
| 分布式系统与通信 | 2 | 6.3% |
| 并行算法理论 | 2 | 6.3% |

并发同步研究多线程如何协调访问共享状态；内存回收研究何时能安全释放仍可能被其他线程访问的对象。这里的稀疏张量计算利用矩阵或图中的稀疏结构，关注的数据结构与 KV token 筛选有所不同。

会议主体仍是并发与通用并行计算，但 AI workload 已进入主要方向。Liger 在 LLM 推理请求间交错算子内/算子间并行，FastFold 为蛋白质结构预测模型 AlphaFold 共同设计模型并行、异步通信和自动显存分块；它们的共同问题不是模型算法，而是如何把不规则计算、collective 和显存压力映射到 GPU 集群。图与稀疏计算论文则持续围绕重排、batch、访存局部性和负载不均，让硬件真正吃满。

严格口径下四类 Agent 均为 0。这里的 AI/ML 工作是模型训练、推理和科学计算基础设施，没有针对 Agent workflow 的规划、工具调用、反馈状态或副作用做特殊设计。

#### 2025

论文列表：[PPoPP 2025 完整论文列表](evidence/venue-catalogs/PPoPP-2025.md)

PPoPP 2025 主会共收录 38 篇长文；论文集中的 11 篇 poster 和 1 篇 keynote 已排除。

| 主方向 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| AI/ML 并行系统 | 11 | 28.9% |
| HPC 与科学计算 | 7 | 18.4% |
| 并发、同步与内存回收 | 5 | 13.2% |
| 图算法与图处理 | 5 | 13.2% |
| GPU、稀疏与张量计算 | 4 | 10.5% |
| 分布式系统与通信 | 4 | 10.5% |
| 编译与程序分析 | 1 | 2.6% |
| 并行算法理论 | 1 | 2.6% |

AI/ML 论文接近三成，研究对象从一般 DNN 加速扩展到 MoE、LLM 量化推理、attention 容错与生产 GPU 共享。MARLIN 将 4-bit weight 解包与 Tensor Core GEMM 融合，ATTNChecker 为 LLM training 的 attention 设计低开销容错，inter-GPU shared memory 工作直接融合 MoE 通信和计算，SGDRC 又在单卡并发 DNN 推理中动态分配资源。热点方法是把 collective、量化格式、故障检测和 GPU 资源控制嵌入执行路径，而不是在模型外侧增加一个通用 scheduler。

HPC 论文也开始与 AI 融合。GRIST 将学习增强物理参数化、混合精度和 3400 万核 Sunway 并行化放入同一个公里级天气—气候系统；这类工作体现 PPoPP 的典型评价方式：既看算法/模型，也要求它在真实极大规模并行机上保持数值和扩展性。四类 Agent 仍均为 0。

#### 2026

论文列表：[PPoPP 2026 完整论文列表](evidence/venue-catalogs/PPoPP-2026.md)

PPoPP 2026 正式 proceedings 的 51 篇均为主会长文。

| 主方向 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| AI/ML 并行系统 | 17 | 33.3% |
| 图算法与图处理 | 7 | 13.7% |
| GPU、稀疏与张量计算 | 7 | 13.7% |
| HPC 与科学计算 | 7 | 13.7% |
| 并发、同步与内存回收 | 6 | 11.8% |
| 编译与程序分析 | 4 | 7.8% |
| 分布式系统与通信 | 3 | 5.9% |

AI/ML 上升到三分之一，并形成较完整的 LLM 训推链条。RoMeo、Quantix 和 JanusQuant 分别处理 4-bit 双维 outlier、3-bit 非均匀权重和 2-bit KV cache；Laser 把多 SLO serving 的抢占粒度下沉到 layer；COCCL 将压缩变成 collective library 的一等阶段；Elastor、HelixPipe 和 CCL-D 又处理弹性 checkpoint、长序列并行和大规模训练 hang/slow 诊断。研究单位由整个 job 下沉到 layer、token、KV、communication chunk 和故障事件。

与此同时，传统并行主题没有消失。锁、事务内存、内存回收、稀疏矩阵、图训练和科学 kernel 仍占多数非 AI 论文；新的共同方法是让 runtime 根据结构、稀疏度、精度敏感性和实时负载选择执行方案。严格口径下 Agent System、Agent Infra、Agent for Systems 和 LLM for Systems 仍全部为 0：PPoPP 在为 LLM/AI 提供高效并行底座，但尚未把 Agent 工作流本身当成专门研究对象。

#### 变化

PPoPP 主会规模从 32、38 增至 51 篇；AI/ML 并行系统从 5 篇（15.6%）增至 11 篇（28.9%）和 17 篇（33.3%）。三年演进并不是从传统并行“转行”到 AI，而是把经典优势应用到新工作负载：2024 主要研究大型模型的模型并行与计算通信重叠，2025 深入 MoE、量化、attention 容错和 GPU 共置，2026 又细化到 KV、layer-level scheduling、collective compression 与训练故障诊断。

因此，PPoPP 对我们最有价值的交集是训练/推理 runtime、GPU kernel、collective、稀疏计算和并行调度；它能解释模型执行内部怎样变快、怎样扩展和怎样容错。Agent 四分类连续三年为 0，也说明它目前更像 Agent/LLM Infra 的底层技术来源，而不是直接研究 Agent System 或 Agent-specific infrastructure 的主场。

### SC

#### 2025

论文列表：[SC 2025 完整论文列表](evidence/venue-catalogs/SC-2025.md)

SC25 早期公告曾宣布接收 137 篇；本报告按会议结束后的最终日程统计其中实际出现的 134 个唯一 Paper 条目，并排除奖项报告、keynote、workshop、poster 等非普通 Technical Papers。下表采用互斥主方向。

| 主方向 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| 数值算法、算子与图计算 | 27 | 20.1% |
| AI/ML 系统与算法 | 20 | 14.9% |
| 编程、编译与系统软件 | 20 | 14.9% |
| 可靠性、性能分析与运维 | 20 | 14.9% |
| 网络、集合通信与索引结构 | 12 | 9.0% |
| 存储、数据与压缩 | 12 | 9.0% |
| 科学计算应用 | 11 | 8.2% |
| 能源、功耗与资源利用 | 8 | 6.0% |
| 量子计算与模拟 | 4 | 3.0% |

SC 仍以高性能计算的经典核心为主体：稀疏矩阵、GEMM、张量、图匹配和低精度数值表示组成最大的 27 篇研究簇，通信避免、算子映射、编译和软硬件协同贯穿多个方向。与纯体系结构研究不同，这些工作通常把算法结构、数据布局、并行分区和真实 GPU/异构设备一起设计，并以大规模机器或科学 workload 的端到端结果检验优化。

LLM 相关工作已深入训练和 serving 内部。X-MoE、Balanced and Elastic、MLP-Offload、RingX、SlimPipe 和 BurstEngine 等处理专家通信、动态负载、分层显存卸载、长上下文 attention 与流水内存；其中 RingX 也覆盖图像/视频模型。MaverIQ、Hetis、gLLM 和 Smurfs 则覆盖量化部署、异构服务、token 级流水线和多草稿模型推测解码。存储侧又出现 GPU Direct Storage 栈、GPU KV 存储与科学数据有损压缩，说明 AI workload 正在吸收 SC 原有的通信、I/O 和数值优化能力。

严格 Agent 四分类只有 3 篇交叉工作。STELLAR 读取文件系统手册和应用 I/O trace，选择配置、在真实系统重跑并根据性能反馈反复调整，属于 Agent for Systems；PerfDojo 用 LLM 表示辅助传统 RL 代码变换，ChatHPC 用专门微调的 Code Llama 助手支持 HPC 软件开发，二者均缺少生成式 Agent 的工具执行—回验闭环，计为 LLM for Systems。Agent System 与 Agent Infra 均为 0。

#### 2026

论文列表：[SC 2026 当前论文列表](evidence/venue-catalogs/SC-2026.md)

SC26 尚未举行；以下是截至 2026-09-20 官方 program 中 149 个唯一 Paper 条目的快照，不是会后最终 proceedings，后续撤稿、更名或日程调整应以最终版本为准。

| 主方向 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| AI/ML 训练、推理与 Agent 系统 | 29 | 19.5% |
| 数值算法与高性能算子 | 25 | 16.8% |
| 科学应用与大规模模拟 | 17 | 11.4% |
| 量子、空间与专用加速器 | 16 | 10.7% |
| 可靠性、性能观测与运维 | 16 | 10.7% |
| 网络与集合通信 | 17 | 11.4% |
| 存储、I/O 与压缩 | 10 | 6.7% |
| GPU 图计算与图搜索 | 9 | 6.0% |
| 安全、可持续与弹性云 HPC | 5 | 3.4% |
| 内存体系结构与 CXL | 3 | 2.0% |
| 自适应 HPC 决策算法 | 2 | 1.3% |

AI/ML 以 29 篇成为最大方向，包含 LLM、扩散模型及其他 AI 负载。LLM 相关的算子侧出现分层半结构化 KV 稀疏注意力、面向中低稀疏率的推理、超低比特 CPU 执行和 irregular GEMM；训练侧研究 MoE LLM 动态显存与层次专家并行，另有扩散模型流水；LLM 服务侧将控制粒度下沉到 prefill/decode 组合、KV 压力下的单请求抢占、异构 stage、动态稀疏上下文和在线 draft model。热门方法是根据运行状态重新组织阶段、内存、collective 与 kernel，而不是只固定一种并行配置。

科学应用和网络/集合通信各 17 篇，量子、空间与专用加速器有 16 篇，可靠性与运维也有 16 篇。通信工作覆盖 SmartNIC/交换机协同稀疏 AllReduce、网内浮点聚合、长距离 RDMA、万卡压缩和微秒级 GPU collective；可靠性从普通 checkpoint 扩展到永久 GPU fault、LLM 训练 silent data corruption 和推理软错误；量子工作则从电路映射走向控制平面、真实硬件接入、trace replay 与量子—经典混合 runtime。

严格口径下共有 8 篇 Agent 交叉。CoreFlow、Grape 和 Maze 分别从上下文/KV 感知资源分配、micro-task serving 和多租户分布式 runtime 承载 Agent 工作流，属于 3 篇 Agent Infra。HPC job management、Star-LAFT 与 SZ-GEN 让 Agent 闭环完成作业调度/诊断、材料工作流与异构压缩 kernel 优化，属于 3 篇 Agent for Systems。CIODI-Bench 分解 grounding、process-aware review 与 orchestration 对工具 Agent 可靠性的作用，Vigil 设计 trigger—render—reason 的科学状态感知—行动接口；两者把 Agent 机制本身作为核心研究对象，计为 2 篇 Agent System。LLM for Systems 为 0；只在附加评测中使用 LLM 的 LEO/ORCA，以及未证明生成式 Agent 和执行反馈的工作均不计入。

#### 变化

SC 的论文数由最终日程 134 篇增至当前快照 149 篇。主方向从 2025 年数值算子领先，变为 2026 年 AI/ML 训推与 Agent 系统领先，但数值/算子仍有 25 篇，科学应用与网络各 17 篇，因此这不是传统 HPC 被 AI 取代，而是通信、内存、可靠性和科学工作流围绕 AI 重新组合。

决策粒度由作业、模型和 GPU 下沉到 token、KV block、expert、micro-task、kernel phase 和 failure layer；方法也从离线静态映射走向运行时观测、预测、调度与反馈。Agent 四类交叉由 3 篇增至 8 篇，并首次出现 3 篇 Agent-specific infrastructure 和 2 篇以 Agent grounding/感知—行动结构为研究对象的 Agent System。对本项目而言，SC 的主要价值是大规模训推、通信/I/O、异构资源和科学工作流，2026 的 Agent 簇则提供了从底层 HPC 机制通向 Agent Infra 与 Agent for Systems 的明确桥梁。

### HPDC

#### 2025

论文列表：[HPDC 2025 完整论文列表](evidence/venue-catalogs/HPDC-2025.md)

HPDC 2025 主会 numbered paper sessions 共收录 25 篇论文；列表与 DBLP proceedings 的 Technical Papers article no. 1–25 逐项一致，未混入 keynote、workshop、poster 或 PhD symposium。

| 主方向 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| 存储、数据管理与隐私 | 6 | 24.0% |
| AI/ML 训练与模型—系统协同 | 5 | 20.0% |
| 数值/GPU Kernel、通信与自动调优 | 5 | 20.0% |
| 云、边缘、FaaS、微服务与可持续计算 | 4 | 16.0% |
| 科学数据压缩 | 2 | 8.0% |
| 图分析与解耦/NDP 架构 | 2 | 8.0% |
| LLM 推理可靠性 | 1 | 4.0% |

科学数据压缩常允许在指定数值误差内近似保存模拟结果；NDP（近数据处理）把部分计算移到更靠近存储或内存的位置，减少远距离搬运。

AI 相关工作尚未由 LLM 主导，而是分散在 GNN/DNN 训练、梯度通信、科学基础模型和性能建模。GNN 半精度训练为稀疏邻居聚合重写无原子 FP16 数据流，SAFusion 先逐 tensor 稀疏再融合并根据通信覆盖反馈调整 buffer，MACE 训练同时按分子图计算量/显存做跨 rank 装箱和重写等变张量收缩 kernel。ModelX 又用少量目标数据把异构性能特征映射到冻结的源预测器，说明“学习增强系统”更常用来迁移性能模型，而非让 Agent 接管系统控制。

存储与云方向强调把内部状态暴露给调度器。TSUE 将纠删码随机更新拆成前台顺序日志和后台局部性聚合，AutoSSD 让 SSD 经 CXL 共享忙闲状态并自主重定向 RAID 请求，DPU-KV 只把剖析后最重的网络路径卸载到 DPU；CarbonEdge、FluidFaaS 等则把碳强度、突发负载和请求阶段纳入放置或扩缩容。共同方法是先识别数据路径中的真实瓶颈，再以跨层状态驱动细粒度决策，而不是增加一个通用资源池。

严格口径下 Agent System、Agent Infra、Agent for Systems、LLM for Systems 均为 0。FT2 保护的是 LLM 自回归推理中的关键层和逐 token 软错误，FluidFaaS 是通用 Serverless ML inference 基础设施；二者都没有 Agent workflow 或自主系统任务闭环。

#### 2026

论文列表：[HPDC 2026 完整论文列表](evidence/venue-catalogs/HPDC-2026.md)

HPDC 2026 官方 program 的 12 个主会 paper sessions 共列出 40 篇正式论文；官方未另分 full/short，列表按带 Authors 的论文条目纳入并排除其他活动。

| 主方向 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| LLM 与生成式模型训推系统 | 11 | 27.5% |
| 编程模型、编译与 Runtime | 4 | 10.0% |
| 科学应用 | 4 | 10.0% |
| 科学压缩与渐进检索 | 4 | 10.0% |
| 存储与 I/O | 4 | 10.0% |
| 通信、跨设施工作流与能耗 | 4 | 10.0% |
| 图分析 | 3 | 7.5% |
| 云、Serverless 与微服务 | 3 | 7.5% |
| AI 与实时分析数据系统 | 3 | 7.5% |

LLM/生成式模型成为最大单一方向。以下 STAR、PKAS、Omnia 等明确以 LLM 请求为对象：STAR 从隐藏状态预测剩余输出长度并重新分配 decode 序列，PKAS 前向模拟请求进入 decode 后的 KV 占用再决定 prefill 准入，Omnia 把 RAG 的 chunk 重排、渐进 prefill 和 KV 反压合成跨阶段流水。Beyond 与 MoE-Lens 分别让 CPU 直接承担历史 attention、用统一性能模型逼近 CPU–GPU 混合 MoE 的硬件上限；训练侧的 UniEP、ResiHP、TACO 又将 expert dispatch、混合并行故障恢复和张量并行激活压缩嵌入执行路径。热门方法已从静态并行方案转向未来状态预测、阶段重叠、在线再调度和计算—通信—显存联合建模。

其余部分保持 HPDC 的传统优势，另有通用 AI 数据系统：科学模拟把物理算法、数据布局、CPU/GPU 负载和通信共同设计；科学压缩从单一字段推进到 QoI 误差传播和按需渐进检索；存储工作则覆盖训练 I/O 自动调优、权重快照审计、LSM compaction，以及流式向量索引和十亿规模 GNN 的外存推理。科学应用、压缩、图处理和跨设施通信合计 15 篇，占 37.5%，因此会议并未转变为纯 AI venue。

严格口径下四类 Agent 仍均为 0。FAME 的 multi-agent 是传统多智能体强化学习；名为 “Agentic AI Workloads” 的 session 实际包含扩散模型与 MoE 推理工作，session 命名不能替代逐篇机制判断。

#### 变化

HPDC 主会规模由 25 篇增至 40 篇。AI 相关主题从 2025 年的训练/系统协同 5 篇加 LLM 可靠性 1 篇（合计 24.0%），发展到 2026 年 LLM/生成模型 11 篇加 AI 数据系统 3 篇（合计 35.0%）；其中 2026 年的 11 篇是 LLM/生成式模型合并类别，不能全部算作 LLM。研究重心也从半精度、梯度压缩、科学模型训练和通用推理可靠性，转向 LLM serving、RAG、KV Cache、MoE 训推、混合并行容错和生成模型推理。

决策粒度同步从 job、rank、tensor 和设备层下沉到请求、序列、chunk、KV block、token、expert 以及运行时并行范式切换。对我们的方向而言，HPDC 的价值主要在大规模训推 runtime、通信与存储路径、异构资源调度和科学 AI；它提供 Agent/LLM 基础设施所需的底层机制，但两年尚未出现直接针对 Agent 规划—行动闭环或 Agent-specific workflow 的论文。

### SIGMETRICS

#### 2025

论文列表：[SIGMETRICS 2025 完整论文列表](evidence/venue-catalogs/SIGMETRICS-2025.md)

SIGMETRICS 2025 官方 accepted papers 共 66 篇，其中 61 篇为 POMACS 正式论文，5 篇为 ACM SIGMETRICS Performance Evaluation Review 的 archival summary；列表保留官方 Summer、Fall、Winter 三轮次顺序并明确区分两类出版物。

| 主方向 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| 排队、调度与在线优化 | 16 | 24.2% |
| 网络测量、协议与基础设施 | 13 | 19.7% |
| 云、存储与系统运行时 | 11 | 16.7% |
| 机器学习系统与联邦学习 | 7 | 10.6% |
| 安全、隐私与区块链 | 7 | 10.6% |
| 量子与新型计算 | 6 | 9.1% |
| 公平分配、市场与博弈 | 5 | 7.6% |
| 可持续计算 | 1 | 1.5% |

在线优化指在未来请求尚未完全知道时逐步作出决策；竞争比等理论指标比较它与预先知道未来的理想方案之间的差距，用来刻画最坏情况下的保证。

前三类合计 40 篇，占 60.6%，会议主体仍是可建模、可测量并能给出界限的系统问题。在线优化论文常用 learning-augmented algorithm：预测信号表现好时获取平均收益，预测失效时由竞争比、排队稳定性或安全策略兜底，而不是让黑盒模型直接替代控制律。网络方向将主动测量、生产 trace、协议状态和理论模型结合；云/存储方向则围绕缓存、持久内存、资源共享、Serverless 与尾延迟建立可解释性能模型。

机器学习系统只有 7 篇，研究对象主要是 GNN/PIM、联邦学习、Serverless ML、故障预测和系统 surrogate。PyGim 根据图与硬件状态把 GNN kernel 分配到真实 PIM DIMM 和主处理器，体现这一届较典型的 hardware–runtime co-design；AI 在这里更多是被建模的工作负载或系统决策的辅助工具，尚未形成 LLM serving 主题。

严格口径下 Agent System、Agent Infra、Agent for Systems、LLM for Systems 均为 0。论文中的 multi-agent bandit、网络化多主体优化和传统强化学习表示数学决策主体或控制策略，不属于 LLM Agent。

#### 2026

论文列表：[SIGMETRICS 2026 完整论文列表](evidence/venue-catalogs/SIGMETRICS-2026.md)

SIGMETRICS 2026 官方三轮 accepted papers 共 80 篇，其中 73 篇为 POMACS 正式论文、7 篇为 PER archival summary。

| 主方向 | 论文数 | 占全部论文比例 |
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

LLM 系统以 13 篇成为第二大方向，且覆盖了完整资源路径。Pittacus/SageServe 用生产请求预测做跨地域容量规划、模型放置和逐请求路由；Optimal Scheduling Algorithms for LLM Inference 从 prefill/decode 两阶段模型推导吞吐最优结构，再实现面向 TBT SLO 的在线调度；GPU 存储架构工作以 2.5 万余种配置比较 checkpoint、数据加载、权重与缓存路径。UniCache 将 session 历史、模板和结构复用映射到统一 prefix-cache 淘汰价值，WISP 又根据接受率、边云 RTT、GPU batch 和 SLO 动态联动 draft 长度与云端验证。研究热点不是孤立优化某个 kernel，而是把请求长度、队列、缓存、GPU/存储、网络与 SLO 放进同一决策模型。

测量和可持续性也进入 LLM 路径。公网扫描工作量化 32 万余个 LLM 服务的框架、API 与暴露面，多请求工作流论文比较顺序、交互、agentic 和 compound-AI 请求图下的性能—能耗，GreenCache 同时核算电力碳和新增缓存设备的 embodied carbon。可持续计算作为主方向由 1 篇增至 3 篇，另有碳与健康目标因主要对象是 LLM serving 而计入 LLM 类。

严格口径下 Agent System 为 0，Agent Infra、Agent for Systems、LLM for Systems 各 1 篇。多请求工作流测量专门揭示 agentic/compound-AI 依赖图的基础设施代价，属于 Agent Infra 的表征工作；MeshAgent 从示例归纳网络约束，以“生成—执行前验证—不确定时拒答”闭环完成网络管理，属于 Agent for Systems；CAP 让 LLM 迭代检索设备、拓扑和历史配置来诊断误配置，但不自主执行和验证修复，属于 LLM for Systems。EviDex 提供持续更新、可追溯的 RAG evidence-path index，可被 Agent 使用但没有 Agent-specific workflow，故只记为 agent-adjacent RAG infrastructure。

#### 变化

SIGMETRICS 论文数由 66 增至 80。排队/调度/在线优化仍居第一，但占比由 24.2% 降至 18.8%；网络也从 19.7% 降至 13.8%，不是绝对衰退，而是 LLM 系统和更多应用方向扩充了会议版图。最突出的变化是 LLM 从 2025 年未形成主方向，直接增长为 2026 年 13 篇、占 16.2%，并从性能测量延伸到跨地域资源控制、prefill/decode 理论、GPU 存储、KV/prefix cache、边云推测服务、训练 kernel、能耗与安全暴露面。

方法上，会议没有因 LLM 兴起而放弃其传统特色：新系统仍强调 workload characterization、排队/优化模型、可证明边界和生产 trace，LLM 只是新的复杂工作负载与控制对象。对我们的方向而言，SIGMETRICS 最有价值的是用严格模型回答训推或 Agent workflow 的容量、SLO、缓存、能耗和跨地域资源问题；2026 出现的三类 Agent 交叉也说明，Agent 工作负载开始进入系统测量与运维，但尚未成为核心 Agent System 研究。

### SIGCOMM

#### 2025

论文列表：[SIGCOMM 2025 完整论文列表](evidence/venue-catalogs/SIGCOMM-2025.md)

SIGCOMM 2025 主会共 88 篇论文，包括 74 篇 full paper 和 14 篇 short paper。下表采用互斥主方向，合计等于全部论文数。

| 主方向 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| AI 集群网络与大模型系统 | 14 | 15.9% |
| 数据中心网络、传输与互连 | 12 | 13.6% |
| 可编程数据平面与云网络 | 11 | 12.5% |
| 网络测量、诊断与可观测性 | 13 | 14.8% |
| 网络验证、管理与安全 | 7 | 8.0% |
| 互联网架构、路由与流量控制 | 7 | 8.0% |
| 无线、蜂窝与感知 | 7 | 8.0% |
| 卫星、海洋与非地面网络 | 7 | 8.0% |
| 视频、实时通信与 QoE（用户体验质量） | 7 | 8.0% |
| 分布式系统与网络服务 | 3 | 3.4% |

AI 已是最大单一方向，含 LLM 和多模态 LLM；研究重点是“怎样为模型集群提供网络”，而不是模型算法本身。InfiniteHBD 以收发器内 OCS 建立可重构高带宽域，DistTrain 为多模态模型的 encoder、LLM backbone 和 generator 分别编排资源，ResCCL 将 collective 的 primitive 和 thread block 调度下沉到通信库，SCX 则把 KV Cache 编码纳入机密推理路径。共同方法是围绕训练 collective、RDMA、光互连、KV 传输和 SmartNIC/DPU 做软硬件协同，并用生产规模部署验证网络机制是否真正转化为吞吐、尾延迟或成本收益。

网络运维开始出现两种不同的生成式 AI 用法。Confucius 把意图拆成 DAG，由多个 LLM Agent 调用现有工具、共享 RAG 记忆并在操作前验证，属于 Agent for Systems；BIAN 用 LLM 对监控证据排序并解释疑似故障设备，但没有自主执行—回验闭环，属于 LLM for Systems。严格口径下两类各 1 篇，Agent System 与 Agent Infra 均为 0；标题中的 agentless、传统 RL 或普通 AI networking 不计入。

#### 2026

论文列表：[SIGCOMM 2026 完整论文列表](evidence/venue-catalogs/SIGCOMM-2026.md)

SIGCOMM 2026 官方 accepted 页页眉写有 110 篇，但实际只有 109 个唯一题名，最终主 proceedings 也恰有 109 篇；列表采用可逐篇核验的 109 篇，并排除 program 中属于另外两个 proceedings 的条目。

| 主方向 | 论文数 | 占全部论文比例 |
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

可编程数据平面与云网络以 23 篇居首，AI 集群网络也增至 21 篇；两者共同覆盖 scale-up/scale-out fabric、光互连、网内 collective、100K+ GPU 训练栈、KV Cache 远程 I/O 和跨 prefill/decode/storage 数据路径。DualPath 是其中最直接的 Agent Infra：多轮 Agent 请求需要反复加载外部 KV，它让 storage 数据可先进入 NIC 空闲的 decode engine，再经计算网络 RDMA 送往 prefill，并依据两侧实时负载选择路径。这里优化的是 Agent workload 的持久上下文 I/O，不是 Agent 的规划逻辑。

Agent for Systems 增至 3 篇：Elastispec 用多步一致性保持的 Agent 将防火墙文档形式化，XiHe 让多个证据驱动 Agent 共享网络化记忆并合成可核验因果图，RepLLM 用四类 Agent 在 sandbox 中完成“读论文—搭架构—生成代码—审计修复”。AliYANG 与 AIDA 分别用 LLM 辅助配置模型维护和根因推理，但生产动作仍由既有系统或人员控制，计为 2 篇 LLM for Systems。Agent System 仍为 0。

#### 变化

SIGCOMM 的 AI 集群网络由 14 篇增至 21 篇，占比从 15.9% 升至 19.3%，同时论文总数由 88 增至 109；可编程数据平面与云网络也由 11 篇增至 23 篇。研究对象从训练 collective、RDMA 与基础可编程数据面，进一步扩展到 KV I/O、prefill/decode/storage 解耦、scale-up fabric、光网络重构和超大 GPU 集群的跨层通信栈；网络已经从 AI 的外部支撑，变成决定模型与 Agent 服务架构的核心资源。

四类 Agent 交叉由 2025 年的 2 篇增至 2026 年的 6 篇，且从单个网络管理框架扩展到 Agent-specific KV 数据路径、共享记忆与因果表示、形式化配置、自动复现和多步根因分析。对本项目而言，SIGCOMM 的价值不只在“网络加速 LLM”，更在于解释长上下文、多阶段推理和自治运维如何把网络状态、存储 I/O、验证与故障证据带入系统闭环；不过两年均没有直接改进规划—行动—反馈算法的 Agent System 论文。

### USENIX ATC

#### 2025

论文列表：[USENIX ATC 2025 完整论文列表](evidence/venue-catalogs/USENIX-ATC-2025.md)

USENIX ATC 2025 官方 Technical Sessions 共收录 100 篇正式论文；joint keynote、Flame Award、poster、break 等非论文活动均已排除。这是 ATC 的最后一届，下表采用互斥主方向。

| 主方向 | 论文数 | 占全部论文比例 |
|---|---:|---:|
| AI/ML 系统与加速计算 | 37 | 37.0% |
| 可靠性、安全、验证、测试与工程工具 | 17 | 17.0% |
| 网络、传输、媒体与空间系统 | 15 | 15.0% |
| 云、Serverless、分布式协议与资源调度 | 11 | 11.0% |
| OS、虚拟化、内存与低层运行时 | 11 | 11.0% |
| 存储、数据库与数据处理 | 9 | 9.0% |

AI/ML 系统以 37 篇成为最大方向。LLM 相关工作覆盖长上下文、PEFT、MoE、多模态 LLM 训练与多 LoRA 服务，以及 KV、量化、检查点和训练故障；其他工作包括文生图扩散模型服务和通用 DNN/GPU 系统。调度粒度已经从整模型或整 GPU 下沉到 tensor、token、expert、adapter、operator 和显存片段。DEEPSERVE 统一 LLM 后训练与推理并为 Ascend NPU 提供 PD 布置和快速扩容，LLMStation、SIRIUS 分别在迭代/显存粒度共置微调与延迟敏感推理，UCP 则把 checkpoint 从保存时的并行布局中解耦。

最常见的方法是先分解固定的数据或执行路径，再按运行状态动态重组。Elastic Tensor 管理 LLM 微调 tensor 的动态物化与丢弃，Weaver 将热 LLM 的 attention 卸载到冷 LLM 所在 GPU；文生图扩散服务 Katz 拆开 ControlNet/LoRA 路径；DecouKV 分离索引和数据，DShuffle 把 shuffle 分成三个可卸载阶段。另一条主线用 pipeline、prefetch、CPU–GPU 协同和异步 producer–consumer 隐藏搬运或同步；SmartNIC、DPU、P4、CXL、DSA 与 PIM 工作则不只卸载一个算子，而是围绕设备能力重画完整数据路径。

可靠性与工程工具占 17%，体现 ATC 偏实践的特色：主动注错、coverage-guided fuzzing、model checking、differential testing、e-graph 等价性检查与独立 oracle 被用于编译器、内核、分布式存储、DBMS 和 BLE，并常以发现及修复真实 bug 为结果。与 OSDI 相比，ATC 题材更宽；与 EuroSys 相比，它更常直接呈现特定设备路径、完整工程实现和工业长期部署。

严格口径下四类 Agent 均为 0。DEEPSERVE 虽提供 Agent serving API，核心机制仍是通用 LLM/NPU 训练与推理平台，不能据此记为 Agent Infra；NetKeeper 的 multi-agent controller 是传统多智能体强化学习；Swift 的 GAN+BO 和 Trochilus 的 BRNN+蒸馏也都不是 LLM for Systems。由于会议在 2025 年后终止，本报告只描述最后一届，不构造会内年度变化趋势。
