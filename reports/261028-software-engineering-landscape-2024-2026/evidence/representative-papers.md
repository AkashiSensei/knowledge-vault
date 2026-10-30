# 软件工程代表论文与证据边界

[报告正文](../REPORT.md) · [会议、期刊与统计范围](venue-sources.md)

本页记录报告使用的 15 项代表工作，区分研究对象、方法、实际评测范围和结论限制。它是报告的证据索引，不是完整会议题录；工业经验论文、期刊论文和路线图不混入主研究轨道的标题统计。年份按正式发表场所标注，在线发表与卷期年份不一致时单独说明。

<a id="assistant-usability"></a>
## AI 编程助手的开发者调查

- 论文：[A Large-Scale Survey on the Usability of AI Programming Assistants: Successes and Challenges](https://arxiv.org/abs/2303.17125)
- 发表：ICSE 2024；预印本于 2023 年公开，不能把正式发表年份当作工具或观点首次出现的年份。
- 对象与做法：调查 410 名开发者使用 AI 编程助手的动机、拒绝建议的原因及控制输出的困难，结合定量与定性分析。
- 主要依据：开发者看重减少按键、加快任务和回忆语法，也会因功能或非功能需求未满足、难控制输出而拒绝建议。
- 边界：调查反映受访者的实践与感受，不单独证明工具对长期团队生产力的因果收益。

<a id="clarifygpt"></a>
## ClarifyGPT：代码生成前的需求澄清

- 论文：[ClarifyGPT: A Framework for Enhancing LLM-Based Code Generation via Requirements Clarification](https://doi.org/10.1145/3660810)；[作者公开全文](https://linshi-website.github.io/paper/ClarifyGPT.pdf)
- 发表：FSE 2024，正式载体为 PACMSE。
- 对象与做法：针对由自然语言需求生成代码的任务，检测需求歧义，提出澄清问题，并利用用户补充的信息生成代码。
- 主要依据：论文同时评测代码生成结果，以及歧义识别和澄清问题的质量。
- 边界：该工作支持“澄清需求有助于代码生成”这一具体方法，不代表任意仓库任务都能由提问解决；提问质量与交互成本仍需检查。

<a id="autosd"></a>
## AutoSD：假设、调试实验与补丁生成

- 论文：[Explainable automated debugging via large language model-driven scientific debugging](https://link.springer.com/article/10.1007/s10664-024-10594-x)
- 发表：Empirical Software Engineering；2024-12-18 在线发表，归入 2025 年第 30 卷、第 45 号文章。
- 对象与做法：针对程序缺陷，让 LLM 提出原因假设和调试命令，执行后将结果反馈给模型，再继续调查或生成补丁及解释。
- 主要依据：在三个程序修复基准上比较修复表现，并通过 20 名参与者的研究检查解释是否帮助人工判断补丁。
- 边界：解释是调试过程生成的可检查材料，不应当作模型真实内部思维的直接记录；修复和人工判断的结论限于论文样本。

<a id="unseen-horizons"></a>
## Unseen Horizons：检查代码生成对熟悉表述的依赖

- 论文：[Unseen Horizons: Unveiling the Real Capability of LLM Code Generation Beyond the Familiar](https://arxiv.org/abs/2412.08109)
- 发表：ICSE 2025。
- 对象与做法：构建 OBFUSEVAL，从五个真实项目收集 1,354 个案例，在保留功能和输出的目标下改写描述、代码及上下文依赖，用项目官方测试评测四个 LLM。
- 主要依据：不同改写策略会使测试通过率下降，说明代码生成评测需要检查题目暴露、时效和依赖可用性。
- 边界：改写也可能增加理解难度；性能下降不能单独证明模型记住了标准答案，也不能直接换算成训练污染比例。

<a id="agentless"></a>
## Agentless：固定流程的仓库缺陷修复

- 论文：[Demystifying LLM-Based Software Engineering Agents](https://doi.org/10.1145/3715754)；[作者公开全文](https://lingming.cs.illinois.edu/publications/fse2025.pdf)；[较早预印本](https://arxiv.org/abs/2407.01489)
- 发表：FSE 2025 / PACMSE；预印本于 2024 年公开，标题带有 Agentless 前缀。
- 对象与做法：根据仓库问题单，按固定的定位、候选补丁生成和验证流程完成修复，不让 LLM 自由决定后续动作；用回归测试和生成的缺陷复现测试筛选补丁。
- 主要依据：在 SWE-bench Lite 上与 Agent 方法比较修复结果与成本，展示简单流程作为强对照的价值。
- 边界：成绩对应论文时点、模型和预算，不是永久排行榜；预印本与正式版本的实验设置应分别阅读，也不能由此断言固定流程在所有任务上更好。

<a id="agent-trajectories"></a>
## 软件修复 Agent 的执行轨迹研究

- 论文：[Understanding Software Engineering Agents: A Study of Thought-Action-Result Trajectories](https://conf.researchr.org/details/ase-2025/ase-2025-papers/40/Understanding-Software-Engineering-Agents-A-Study-of-Thought-Action-Result-Trajector)
- 发表：ASE 2025 Research Papers；官方页面标记 ACM SIGSOFT Distinguished Paper Award。
- 对象与做法：将 RepairAgent、AutoCodeRover 和 OpenHands 在程序修复及问题单解决任务中的日志统一为共同格式，分析 120 条轨迹与 2,822 次 LLM 交互。
- 主要依据：比较迭代次数、token 消耗、动作序列，以及模型分析文本、动作和反馈之间的衔接，归纳成功与失败模式。
- 边界：记录到的分析文本和行为模式不是模型内部推理的完整可见性；关联模式需要进一步实验才能作为因果诊断规则。

<a id="watson"></a>
## Watson：检查输入信息如何影响 Agent 决策

- 论文：[Watson: A Cognitive Observability Framework for the Reasoning of LLM-Powered Agents](https://conf.researchr.org/details/ase-2025/ase-2025-papers/148/Watson-A-Cognitive-Observability-Framework-for-the-Reasoning-of-LLM-Powered-Agents)
- 发表：ASE 2025 Research Papers。
- 对象与做法：以提示词归因等方法，事后推断 LLM Agent 决策所依赖的输入信息，辅助人工调试和自动定向修正。
- 主要依据：在 MMLU 多学科问答和 AutoCodeRover 的 SWE-bench Lite 修复任务上评测人工调试及自动修正场景。
- 边界：“认知可观测性”是论文提出的观察与归因目标，不表示直接读取全部隐藏推理，也不能把事后解释自动当作真实因果过程。

<a id="framework-bugs"></a>
## LLM Agent 编排框架的缺陷研究

- 论文：[A Characterization Study of Bugs in LLM Agent Workflow Orchestration Frameworks](https://conf.researchr.org/details/ase-2025/ase-2025-industry-showcase/23/A-Characterization-Study-of-Bugs-in-LLM-Agent-Workflow-Orchestration-Frameworks)
- 发表：ASE 2025 **Industry Showcase**，不是 Research Papers。
- 对象与做法：从 LangChain、LlamaIndex、Haystack 的 1,577 个缺陷相关 PR 中抽取 1,026 个缺陷，分析原因、症状和所在组件。
- 主要依据：建立九类原因、六类症状，并考察它们在数据预处理、基础结构、Agent 构造和扩展模块中的分布。
- 边界：主要研究框架实现及接口缺陷，不等于研究所有 LLM 输出错误；仅作正文补充证据，不计入主研究轨道标题样本。

<a id="triangle"></a>
## Triangle：云服务故障分诊

- 论文：[Triangle: Empowering Incident Triage with Multi-Agent](https://conf.researchr.org/details/ase-2025/ase-2025-papers/22/Triangle-Empowering-Incident-Triage-with-Multi-Agent)
- 发表：ASE 2025 Research Papers，官方摘要标记 Experience Paper。
- 对象与做法：针对云服务故障数据和分散的团队知识，用多角色 LLM Agent 协商负责团队，并结合排障信息收集完成故障分诊。
- 主要依据：在真实生产云环境中评测分诊准确率和 Time to Engage，即故障出现到责任方接手的时间。
- 边界：分诊及其配套信息收集的收益，不等于已验证所有生产配置变更或自主故障恢复的可靠性。

<a id="bug-fixing-analysis"></a>
## 自动缺陷修复系统的横向分析

- 论文：[LLM-based Agents for Automated Bug Fixing: How Far Are We?](https://conf.researchr.org/details/icse-2026/icse-2026-research-track/227/LLM-based-Agents-for-Automated-Bug-Fixing-How-Far-Are-We-)
- 发表：ICSE 2026 Research Track。
- 对象与做法：在 SWE-bench Verified 上比较六种修复系统，检查共同能修复或都不能修复的任务，以及文件/代码符号定位和缺陷复现能力。
- 主要依据：分析指出底座 LLM 能力与 Agent 执行流程均影响修复效果。
- 边界：比较范围限于这六种系统及该评测；不能把系统排名直接泛化到跨服务、长期维护或生产故障任务。

<a id="refagent"></a>
## RefAgent：多角色 Java 重构

- 论文：[RefAgent: A Multi-agent LLM-based Framework for Automatic Software Refactoring](https://conf.researchr.org/details/icse-2026/icse-2026-research-track/111/RefAgent-A-Multi-agent-LLM-based-Framework-for-Automatic-Software-Refactoring)
- 发表：ICSE 2026 Research Track。
- 对象与做法：让不同 LLM Agent 负责重构规划、执行、测试和迭代改进，在八个开源 Java 项目上评测，并进行角色消融。
- 主要依据：与单 Agent、搜索式重构工具和历史开发者重构比较，检查编译、单元测试、代码异味（可能增加维护困难的代码模式）及质量属性。
- 边界：通过测试和改善静态质量指标不等于证明所有业务语义保持不变，也不表示相同角色划分适用于任意语言和仓库。

<a id="saint"></a>
## SAINT：Java 服务接口与业务场景测试

- 论文：[SAINT: Service-level Integration Test Generation with Program Analysis and LLM-based Agents](https://conf.researchr.org/details/icse-2026/icse-2026-research-track/143/SAINT-Service-level-Integration-Test-Generation-with-Program-Analysis-and-LLM-based-)
- 发表：ICSE 2026 Research Track。
- 对象与做法：从 Java 企业应用中静态提取端点语法/语义信息和端点操作的先后约束，再让 LLM Agent 生成端点测试及业务场景测试。
- 主要依据：在八个 Java 应用上评测，包括一个非公开企业应用，检查代码/数据库交互覆盖、缺陷发现和开发者评价。
- 边界：端点模型和操作依赖图是代码分析产物，LLM 才是生成工具；覆盖率提高不等于所有需求已被正确验证。

<a id="secure-executions"></a>
## thea：代码生成推理中的安全干预

- 论文：[Repairing LLM Executions for Secure Automatic Programming](https://conf.researchr.org/details/icse-2026/icse-2026-research-track/168/Repairing-LLM-Executions-for-Secure-Automatic-Programming)
- 发表：ICSE 2026 Research Track。
- 对象与做法：利用机制可解释性分析与漏洞代码生成有关的内部表示，在 LLM 推理访问相关表示时拦截并修改；实现工具名为 thea。
- 主要依据：使用 Llama 3.1 和 CyberSecEval，检查多种漏洞类型的生成结果及干预后的表现。
- 边界：这是代码生成模型的推理干预，不是仓库修复 Agent 的角色编排；在给定模型与基准上减少漏洞，不等于形式化保证生成代码绝对安全。

<a id="commercial-llm-reproducibility"></a>
## 商业 LLM 软工实验的复现条件

- 论文：[Reflections on the Reproducibility of Commercial LLM Performance in Empirical Software Engineering Studies](https://conf.researchr.org/details/icse-2026/icse-2026-research-track/165/Reflections-on-the-Reproducibility-of-Commercial-LLM-Performance-in-Empirical-Softwar)；[DOI](https://doi.org/10.1145/3744916.3773207)
- 发表：ICSE 2026 Research Track。
- 对象与做法：检查 ICSE 2024 和 ASE 2024 的 86 项 LLM 研究，尝试复现其中提供实验材料且使用 OpenAI 模型的 18 项。
- 主要依据：只有五项具备实际复现条件，其中两项部分复现、三项未复现，没有完整复现的案例。
- 边界：结论针对所选样本、访问条件及复现时点，不代表所有商业 LLM 研究都无法复现，也不能将模型变化视为所有失败的唯一原因。

<a id="roadmap-2030"></a>
## 2030 软件工程路线图

- 论文：[A 2030 Roadmap for Software Engineering](https://doi.org/10.1145/3731559)；[机构公开记录](https://riunet.upv.es/entities/publication/e9633d24-637f-466c-9362-8002321e4470)
- 发表：ACM TOSEM，2025；路线图及专题导论。
- 对象与做法：组织 AI for SE、人因、可持续软件工程、自动编程、安全、验证与确认、量子软件工程七类开放研究问题。
- 用途：为报告提供软件工程全领域的观察框架，避免把代码生成或 Agent 热点当作整个领域。
- 边界：研究议程表达社区讨论与未来方向，不是每个方向已达到某种成熟度的实验结论。
