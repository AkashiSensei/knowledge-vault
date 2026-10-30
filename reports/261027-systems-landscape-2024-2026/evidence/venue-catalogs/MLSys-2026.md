# MLSys 2026 论文列表

官方 Proceedings 共收录 135 篇论文。以下标题均链接至对应的官方论文摘要页。每篇依次列出机构与主要作者、核心工作、相较既有方法的核心创新，以及便于快速识别研究对象与技术路径的细粒度方向。

- [ProfInfer: An eBPF-based Fine-Grained LLM Inference Profiler](https://proceedings.mlsys.org/paper_files/paper/2026/hash/03dbc11a22e79cd38bea53cf518c2371-Abstract-Conference.html)
  - Huawei；Bohua Zou、Debayan Roy、Dhimankumar Yogesh Airao 等
  - ProfInfer 是一个面向 llama.cpp 等 LLM 推理引擎的无侵入性能分析器，目标是回答具体请求究竟受计算、内存还是算子卸载限制。它通过 eBPF 动态挂载多层运行时函数，重建算子图、时间线和硬件计数器变化，在不修改或重新编译引擎的情况下把分析开销控制在 5% 以内。分析对象覆盖稠密模型、MoE 路由和 CPU/GPU 算子卸载，输出既包括函数级 trace，也包括可直接关联瓶颈的图、时间线和硬件趋势。
  - 相较于依赖源码插桩或只能看 kernel 汇总的 profiler，核心创新是用 eBPF 跨 LLM runtime 层恢复算子级语义与硬件行为。
  - LLM 推理可观测性、eBPF 动态插桩、边缘推理性能诊断

- [SpecDiff-2: Scaling Diffusion Drafter Alignment For Faster Speculative Decoding](https://proceedings.mlsys.org/paper_files/paper/2026/hash/041dad5ed2191b44ba3ed0e00cdc3187-Abstract-Conference.html)
  - University of Virginia；Jameson Sandler、Jacob Christopher、Tom Hartvigsen 等
  - SpecDiff-2 是一种无损推测解码框架：它用可并行生成多个候选 token 的离散扩散模型充当 drafter，再交给原自回归模型验证。其核心不是简单替换草稿模型，而是专门校准扩散 drafter 与自回归 verifier 的分布，降低候选拒绝率，在推理、代码和数学任务上最高达到标准解码的 5.5 倍速度。评测覆盖推理、代码和数学任务以及 14B/72B 模型，平均 token/s 比既有方法最高提高 55%，同时保持目标模型原始输出分布。
  - 相较自回归 drafter 或未对齐的扩散 drafter，核心创新是把并行离散扩散生成与 drafter-verifier 分布校准放在同一无损解码框架中。
  - 推测解码、离散扩散 Drafter、Drafter-Verifier 对齐

- [CDLM: Consistency Diffusion Language Models for Faster Sampling](https://proceedings.mlsys.org/paper_files/paper/2026/hash/054de805fcceb78a201f5e9d53c85908-Abstract-Conference.html)
  - University of California, Berkeley；Minseo Kim、Chenfeng Xu、Coleman Hooper 等
  - CDLM 是对扩散语言模型本身进行训练式改造的加速方法，而不是外挂的推理调度器。它用一致性建模让模型一次定稿多个 token，并在微调时加入分块因果注意力使生成过程可复用 KV Cache，从而同时减少采样轮数和重复注意力计算。在数学和代码任务上，该组合保持竞争性准确率，并把端到端采样延迟降低 3.6–14.5 倍。
  - 相较只减少扩散采样步或只改注意力的方案，核心创新是同时让 DLM 少步生成并兼容标准 KV Cache。
  - 扩散语言模型推理、一致性蒸馏、KV Cache 兼容

- [Unified LLM Model for Power, Performance, and Area Prediction from Hardware Code](https://proceedings.mlsys.org/paper_files/paper/2026/hash/0731f0e65559059eb9cd9d6f44ce2dd8-Abstract-Conference.html)
  - University of Southern California；Armin Abdollahi、Mehdi Kamal、Massoud Pedram
  - RocketPPA 不是 Agent，也不是由 LLM 辅助的规则预测器，而是一个端到端的硬件指标回归模型：输入 Verilog 代码，直接输出设计的功耗、性能和面积。LLM 主干负责把代码编码为电路语义表示，MoE 回归头预测不同指标，LoRA 降低适配成本，对比学习则让结构相似的设计表示更接近，以提升跨工艺节点和优化策略的泛化。训练数据覆盖 15 nm 与 45 nm、面积优先与延迟优先流程；预测每个设计约需 0.12 秒，在 10% 误差容限下的通过率比既有方法提高 9.4 个百分点。
  - 相较为每个工艺和目标训练独立数值模型，核心创新是用统一代码语言模型加任务专家头直接跨节点、跨优化风格预测三类 PPA。
  - Verilog PPA 预测、代码语言模型回归、跨工艺泛化

- [SuperInfer: SLO-Aware Rotary Scheduling and Memory Management for LLM Inference on Superchips](https://proceedings.mlsys.org/paper_files/paper/2026/hash/07fd64f9316f40193c6a4d87d8afa011-Abstract-Conference.html)
  - University of Illinois Urbana-Champaign；Jiahuan Yu、Mingtao Hu、Zichao Lin 等
  - SuperInfer 是为 NVIDIA GH200 一类 CPU-GPU 紧耦合 Superchip 设计的 LLM 服务系统，解决 KV Cache 不足时请求互相阻塞、TTFT 失约的问题。其 RotaSched 主动把请求在 CPU 与 GPU 内存间轮转以维持响应性，DuplexKV 则让 KV 数据经 NVLink-C2C 全双工传输，使 TTFT 达标率最高提升 74.7%。评测在 GH200 上覆盖不同模型和请求分布；改进 TTFT 达标率的同时，TBT 与总体吞吐基本不低于现有服务系统。
  - 相较被动溢出后卸载或普通 PCIe swap，核心创新是面向 CPU-GPU 一致高速互连进行主动 SLO 轮转与双向 KV 传输协同。
  - LLM 服务调度、KV Cache 异构内存、Superchip SLO

- [HELIOS : Adaptive Model And Early-Exit Selection for Efficient LLM Inference Serving](https://proceedings.mlsys.org/paper_files/paper/2026/hash/096b1019463f34eb241e87cfce8dfe16-Abstract-Conference.html)
  - University of Texas at Austin；Avinash Kumar、Shashank Nag、Jason Clemons 等
  - HELIOS 是一个运行多个早退 LLM 的服务框架，利用不同模型对同一 token 的早退位置具有互补性，而非只优化单个模型。系统在线估计早退分布并动态选择模型，只加载最可能实际执行的层，同时允许高置信 token 提前结束，由此释放显存扩大 batch，并降低被少数难退出 token 拖慢的风险。在线 profiler 根据每个请求的 token 行为更新模型选择和权重加载决策，最终把吞吐提高 1.48 倍，并把可容纳 batch 扩大 15.14 倍。
  - 相较单模型早退，核心创新是利用多个模型早退位置的互补性，并把模型选择与按需权重驻留联合决策。
  - 早退 LLM 服务、运行时模型选择、按需权重驻留

- [Scaling Up Large Language Models Serving Systems for Semantic Job Search](https://proceedings.mlsys.org/paper_files/paper/2026/hash/0a4c7cdfc0a4eb1b13bb84a9b6220c37-Abstract-Conference.html)
  - LinkedIn；Kayhan Behdin、Qingquan Song、Sriram Vasudevan 等
  - 这是一项 LinkedIn 语义职位搜索的生产系统研究，目标是把文本相关性模型部署到每秒数百万请求、同时受延迟和成本约束的线上环境。系统采用纯文本 decoder-only 小模型，以剪枝缩小最多 40% 模型体积、以输入压缩将上下文缩短十倍以上，再配合 GPU 服务优化，最终在质量达标的前提下获得 10 倍吞吐。这里既包含模型侧压缩，也包含真实 GPU 集群上的 batching 和 serving 实现，目标是同时满足搜索质量、延迟和每秒请求量，而非只比较离线模型精度。
  - 相较只压模型或只调服务引擎，核心创新是把 SLM、模型剪枝、上下文压缩与百万 QPS GPU serving 做端到端生产协同。
  - 工业语义搜索、小语言模型压缩、高 QPS 推理

- [Massive-Scale Out-Of-Core UMAP on the GPU](https://proceedings.mlsys.org/paper_files/paper/2026/hash/0badcb4e95306df76a719409155e46e8-Abstract-Conference.html)
  - NVIDIA；Jinsol Park、Corey J. Nolet、Edward Raff 等
  - 这项工作把 UMAP 改造成可处理远超主存规模向量数据的 GPU 实现，面向几十到数百 GB 数据上的降维和交互式探索。它把数据与中间状态分批在存储、主机和 GPU 间流动，并可把计算扩展到多张 GPU，因此避免一次装入全部图结构，单 GPU 相对 CPU 最高加速 22.7 倍。小规模数据上测得单 GPU 22.7 倍加速；在 CPU 已无法完成的大规模数据上，多 GPU 版本依据实测扩展趋势预计可达约 74 倍。
  - 相较要求整图驻留内存的 GPU UMAP，核心创新是保持算法语义的 out-of-core 分批执行并支持多 GPU。
  - Out-of-Core GPU 图分析、多 GPU UMAP、超大向量数据

- [AccelOpt: A Self-Improving LLM Agentic System for AI Accelerator Kernel Optimization](https://proceedings.mlsys.org/paper_files/paper/2026/hash/0f8426558905746fc38da5e335700aec-Abstract-Conference.html)
  - Stanford University；Genghan Zhang、Shaowei Zhu、Anjiang Wei 等
  - AccelOpt 是一个真正的 LLM Agent 内核优化系统：输入待优化的 Trainium 算子实现，Agent 反复生成候选内核、编译运行并依据实测性能继续修改。系统把过去出现的慢—快内核对提炼为优化记忆，使 Agent 在没有人工提供硬件规则的情况下跨任务积累经验并自我提升。在 NKIBench 的真实 LLM 算子上，Trainium 1 的平均峰值利用率从 49% 提升到 61%，Trainium 2 从 45% 提升到 59%；使用开源模型时成本仅为 Claude Sonnet 4 方案的约 1/26。
  - 相较每个内核从零提示或依赖人工硬件知识，核心创新是从实测慢-快程序对构建可积累的 Agent 优化记忆。
  - Agent for Systems—内核自动优化、自改进 Agent、Trainium

- [BOOST: BOttleneck-Optimized Scalable Training Framework for Low-Rank Large Language Models](https://proceedings.mlsys.org/paper_files/paper/2026/hash/127e7093c38a45290524237be8eb39c5-Abstract-Conference.html)
  - University of California, Santa Barbara；Zhengyang Wang、Ziyue Liu、Ruijie Zhang 等
  - BOOST 是专门服务低秩瓶颈式大模型的分布式训练框架，解决这类模型直接套用传统 3D 并行时小矩阵通信比例过高、GPU 吃不满的问题。它重新设计瓶颈感知张量切分，并联合在线 RMSNorm、线性层分组和低秩激活检查点，使低秩结构的算法节省能够转化为真实的端到端训练加速。评测同时比较全秩模型、低秩模型直接套用 3D 并行和 BOOST，端到端训练速度分别提高 1.46–1.91 倍与 1.87–2.27 倍。
  - 相较把低秩网络当作普通 Transformer 切分，核心创新是根据瓶颈层形状重构 tensor parallel 与归一化、checkpoint 数据流。
  - 低秩 LLM 训练、瓶颈感知张量并行、通信优化

- [TiDAR: Think in Diffusion, Talk in Autoregression](https://proceedings.mlsys.org/paper_files/paper/2026/hash/1367d856028f65a9555b0274db09e608-Abstract-Conference.html)
  - University of Chicago；Jingyu Liu、Xin Dong、Zhifan Ye 等
  - TiDAR 是一种新的语言模型架构，把扩散式并行草稿与自回归式高质量输出放在同一个模型、同一次前向计算中完成。结构化注意力掩码让一部分位置并行“思考”候选 token、另一部分按自回归顺序确认输出，同时保留精确 KV Cache，因此它不是两个独立模型组成的传统推测解码流水线。作者在 1.5B 和 8B 模型上同时评测生成质量与真实吞吐，结果达到自回归模型质量，并把 token/s 提高 4.71–5.91 倍。
  - 相较双模型推测解码或纯扩散左到右近似，核心创新是在单一架构的一次前向中并行 draft、精确自回归确认并复用 KV。
  - 混合扩散-自回归模型、并行生成、精确 KV Cache

- [Rethinking DVFS for Mobile LLMs: Unified Energy-Aware Scheduling with CORE](https://proceedings.mlsys.org/paper_files/paper/2026/hash/136b9a13861308c8948cd308ccd02658-Abstract-Conference.html)
  - Shanghai Jiao Tong University、Purdue University；Zongpu Zhang、Pranab Dash、Qiang Xu 等
  - CORE 是运行在移动设备上的统一 DVFS governor，面向 LLM prefill 和 decode 阶段协调 CPU、GPU 与内存频率。它针对默认 governor 各自决策造成的错误频率组合联合选择三类资源档位，从而降低 TTFT 和单 token 延迟，而不是以增加能耗换取速度。设计依据 prefill 与 decode 不同的资源瓶颈分别决策；相较设备默认策略，TTFT 平均降低 8.5%–17.7%，TBT 降低 27.8%–39.6%。
  - 相较 CPU/GPU/内存各自独立的 DVFS，核心创新是按 prefill/decode 阶段联合选择三类频率。
  - 移动端 LLM 推理、跨资源 DVFS、能耗感知调度

- [ZK-APEX: ZERO-KNOWLEDGE APPROXIMATE PERSONALIZED UNLEARNING WITH EXECUTABLE PROOFS](https://proceedings.mlsys.org/paper_files/paper/2026/hash/148865706acbd18627d3fc15cc3f3b93-Abstract-Conference.html)
  - Imperial College London；Mohammad M Maheri、Sunil Cotterill、Alex Davidson 等
  - ZK-APEX 是一个可验证的个性化模型遗忘框架：服务方要求边缘客户端删除指定样本影响，但既不能读取客户端私有模型，也不能完全信任客户端执行结果。服务方生成稀疏删除掩码，客户端用 Group-OBS 曲率补偿保持个性化精度，再用 Halo2 ZK-SNARK 证明输出确由规定变换得到，从而把遗忘算法和合规验证连接起来。在 ViT 上可恢复约 99% 个性化精度，证明生成约两小时、比基于重训练的验证快超过 107 倍；也在 OPT-125M 生成模型上验证了适用性。
  - 相较只给出遗忘结果或要求重训练验证，核心创新是把个性化近似遗忘变成可由零知识证明验证的规定计算。
  - 个性化模型遗忘、零知识证明、边缘隐私合规

- [Zero redundancy distributed learning with differential privacy](https://proceedings.mlsys.org/paper_files/paper/2026/hash/1e70ac91ad26ba5b24cf11b12a1f90fe-Abstract-Conference.html)
  - Amazon；Zhiqi Bu、Justin Chiu、Ruixuan Liu 等
  - DP-ZeRO 是把差分隐私训练扩展到超大模型的分布式训练系统，而非新的隐私定义。它把每样本梯度裁剪和隐私记账所需状态融入 ZeRO 的参数、梯度与优化器分片，使各 GPU 不再保存冗余副本，并支持混合精度，从而让 DP 训练获得接近普通 ZeRO 的计算和通信效率。论文以 GPT-100B 级可训练规模为目标，并使 DP 版本保留标准 ZeRO 的分片、通信和混合精度能力，而不是只在单卡小模型上验证隐私算法。
  - 相较现有多 GPU DP 训练或标准 ZeRO，核心创新是让逐样本隐私梯度计算与 ZeRO 分片语义兼容且不恢复冗余状态。
  - 差分隐私大模型训练、ZeRO 分片、混合精度 DP

- [CATWILD: Compiler Autotuning for TPU workloads in the Wild](https://proceedings.mlsys.org/paper_files/paper/2026/hash/2093ed77c549eda95bd6f7212b735b43-Abstract-Conference.html)
  - Google；Ignacio Cano、Yu Wang、Mike Burrows 等
  - CATWILD 是部署在 Google TPU 集群中的编译器自动调优服务，输入真实训练作业及 XLA 可调配置，输出经实测选择的更高性能编译方案。它持续从变化的模型、硬件和历史运行结果中搜索，而不是依赖固定启发式或人工逐例优化；论文总结了该系统五年生产运行以及由此节省 TPU 芯片资源的经验。系统已经在 Google 数据中心持续运行五年，为相当比例的真实 TPU 训练作业生成 tuned configuration；评价重点是 fleet 级芯片节省而非单个 benchmark 的最佳速度。
  - 相较离线一次性 auto-tuning demo，核心创新是构建能随真实 TPU fleet 和 workload 长期演化的生产编译调优闭环。
  - 生产编译器自动调优、TPU Fleet、持续优化

- [GriNNder: Breaking the Memory Capacity Wall in Full-Graph GNN Training with Storage Offloading](https://proceedings.mlsys.org/paper_files/paper/2026/hash/215597a92341c78cc3e7fe628be4a195-Abstract-Conference.html)
  - Seoul National University；Jaeyong Song、Seongyeon Park、Hongsun Jang 等
  - GriNNder 是单机完整图 GNN 训练系统，允许图和训练状态在 GPU、主机内存都放不下时继续使用 NVMe SSD。它针对图训练访问模式设计分区缓存、反向传播重聚合和绕过路径，避免直接照搬通用 out-of-core 方法产生的重复 I/O，使一张 GPU 也能训练过去需要分布式资源的大图。评测跨多种 GNN 和图数据，最高比现有单机方案快 9.78 倍，并在有限内存的一张 GPU 上达到接近分布式系统的吞吐。
  - 相较只在 GPU/DRAM 间换页，核心创新是首次针对完整图 GNN 的依赖设计 GPU-host-NVMe 三层缓存、重聚合与绕过。
  - 完整图 GNN 训练、NVMe 存储卸载、分层缓存

- [ExecuTorch - A Unified PyTorch Solution to Run ML Models On-Device](https://proceedings.mlsys.org/paper_files/paper/2026/hash/236f915dd02af4f11927f67330b21d4b-Abstract-Conference.html)
  - Meta；Mergen Nachin、Digant Desai、Stephen Jia 等
  - ExecuTorch 是 PyTorch 原生的端侧模型部署运行时，接收在 PyTorch 中定义的模型，并将其带到微控制器、手机和带专用加速器的 SoC 上执行。它保持 PyTorch 的模型语义，同时提供量化、可插拔硬件后端和可裁剪运行组件，解决端侧部署必须转换模型或在另一套生态中重写的问题。统一接口覆盖从嵌入式微控制器、可穿戴设备、手机到复杂 SoC，并允许厂商 backend 决定算子落到 CPU、GPU 或 NPU。
  - 相较每种端侧芯片单独转换或重写模型，核心创新是用统一 PyTorch 导出和 backend 契约覆盖极宽硬件范围。
  - 端侧 ML 运行时、PyTorch 部署、异构加速后端

- [EarthSight: A Distributed Framework for Low-Latency Satellite Intelligence](https://proceedings.mlsys.org/paper_files/paper/2026/hash/26289c647c6828e862e271ca3c490486-Abstract-Conference.html)
  - Georgia Institute of Technology；Ansel Erol、Seungjun Lee、Divya Mahajan
  - EarthSight 是把卫星星座与地面站视为一个整体的分布式图像分析运行时，目标是在灾害响应等场景中尽快返回有价值的影像，而不是先下传全部原图。星上用共享视觉主干同时执行多个任务，地面调度器汇总查询并分配预算，再按选择性、精度和成本动态排列过滤器，让低价值图像尽早被淘汰。仿真结果显示每张图平均计算时间减少 1.9 倍，从首次地面站接触到交付的 P90 延迟由 51 分钟降至 21 分钟。
  - 相较每颗卫星独立筛图，核心创新是联合利用地面全局查询和星上资源状态，把星座推理建模为分布式决策。
  - 卫星边缘推理、星地协同调度、多任务视觉

- [XProf: An Open, Scalable, and Extensible Profiling System for the Modern ML Stack](https://proceedings.mlsys.org/paper_files/paper/2026/hash/280776fda5970060e6a5efcfd43e5d2d-Abstract-Conference.html)
  - Google；Robert Hundt、Naveen Kumar、Jose Baiocchi Paredes 等
  - XProf 是 OpenXLA 生态的全栈性能分析系统，统一关联主机 CPU、加速器内核和分布式执行数据，并把 profiler 结果转成可操作的优化建议。它以可插拔的 PJRT 接口接入不同 GPU/TPU，在数千芯片上以低于 1% 的负载开销运行，因此解决的不只是单次 trace 查看，而是大规模持续诊断。系统可监控数千芯片，覆盖 roofline、host-device 关联和分布式 trace，并已经用于 Google 内部优化及 MLPerf 提交。
  - 相较单设备封闭 profiler，核心创新是开放、可插拔且能把数千加速器 host/device trace 转成诊断建议的全栈架构。
  - 分布式 ML Profiling、OpenXLA、Host-Device 全栈分析

- [Breaking the Ice: Analyzing Cold Start Latency in vLLM](https://proceedings.mlsys.org/paper_files/paper/2026/hash/29416b66c2149872b9d1415a3fd2c5e0-Abstract-Conference.html)
  - Paderborn University；Huzaifa Shaaban Kabakibo、Animesh Trivedi、Lin Wang
  - 这是一项对 vLLM 引擎冷启动过程的分解与建模研究，而不是新的推理引擎。作者把初始化划分为六个可解释阶段，发现主要瓶颈来自 CPU，并根据模型规模和硬件参数建立解析预测器，用于在部署前估算启动时间和规划弹性资源。模型使用各阶段随参数规模变化的稳定趋势估算指定硬件上的启动时间，输出可用于 Serverless 扩容和副本预热，而不是预测正常 token 生成延迟。
  - 相较只报告总体启动时间，核心创新是将 vLLM 冷启动拆成可解释阶段并建立可跨配置外推的解析模型。
  - vLLM 冷启动、启动阶段建模、弹性容量规划

- [Attribution-based Sparse Activation in Large Language Models](https://proceedings.mlsys.org/paper_files/paper/2026/hash/29591f355702c3f4436991335784b503-Abstract-Conference.html)
  - University of Pittsburgh；Jifeng Song、Xiangyu Yin、Boyuan Yang 等
  - 归因稀疏激活是一种推理期近似计算方法：对当前输入计算神经元归因分数，跳过对输出贡献低的激活，而不是永久剪掉模型参数。它以运行时计算量换取可控精度损失，在问答和摘要等生成任务中达到最高 70% 激活稀疏、精度下降低于 5%。稀疏决策随输入动态变化，并在问答、摘要等困难生成任务上达到最高 70% 稀疏度且精度损失低于 5%。
  - 相较静态剪枝或按激活幅值跳过，核心创新是按当前输入的归因分数动态选择低贡献神经元。
  - 输入相关稀疏激活、神经元归因、近似推理

- [Once-for-All Channel Mixers (HyperTinyPW): Generative Compression for TinyML](https://proceedings.mlsys.org/paper_files/paper/2026/hash/2d04d97593c8c33d415337f408ed0e1b-Abstract-Conference.html)
  - 作者未在可解析元数据中标明机构；Yassien Shaalan
  - HyperTinyPW 是面向 TinyML 的生成式权重压缩结构，主要压缩微控制器 CNN 中占用 Flash 最多的 1×1 pointwise mixer。模型不保存每层完整 PW 权重，而只保存短层代码，由共享微型 MLP 在加载时一次性生成并缓存整数权重，因此稳态推理仍可使用普通 INT8 算子。在三个 ECG 数据集上，约 225 KB 的模型接近 1.4 MB CNN 的效果；同一结构还在语音关键词识别上达到 96.2% 测试准确率。
  - 相较量化或存储压缩后的权重，核心创新是只保存层代码、在加载时生成 pointwise 权重并沿层共享潜在基。
  - TinyML 权重生成压缩、微控制器 CNN、加载时合成

- [Ontology-Guided Long-Term Agent Memory for Conversational RAG](https://proceedings.mlsys.org/paper_files/paper/2026/hash/2fb4be70fc9668e9ec2c71b34fb127d4-Abstract-Conference.html)
  - Hill Research；Shuang Cao、Rui Li
  - 这是一套用于多轮对话 Agent 的长期记忆与 RAG 系统，同时决定“哪些信息值得保存”和“以后怎样找回来”。它把用户偏好等持久事实抽取成轻量记忆图，查询时补入对话线索并混合检索，再由预算路由器在长上下文和检索方案间选择，从而解决隐含偏好与当前措辞不重合时的漏召回。系统在隐式偏好召回基准上把 Recall@10 从 0.58 提到 0.70、nDCG@10 从 0.41 提到 0.51，同时相对全长上下文方法降低 81% 成本。
  - 相较只做 dense retrieval 或把全历史塞入上下文，核心创新是把事实抽取、记忆图、对话增强检索和成本路由联合起来。
  - Agent System—长期记忆、对话 RAG、记忆图检索

- [GUARD: SCALABLE STRAGGLER DETECTION AND NODE HEALTH MANAGEMENT FOR LARGE-SCALE TRAINING](https://proceedings.mlsys.org/paper_files/paper/2026/hash/339caf45a6fa281cae8adc6465343464-Abstract-Conference.html)
  - University of Michigan；Guanliang Liu、Abhinandan Patni、congzhu lin 等
  - GUARD 是大规模训练集群的节点健康管理系统，专门识别不会直接报错、却持续拖慢同步训练的灰色慢节点。它一方面在真实训练中进行低开销在线性能监控，另一方面在节点加入生产作业前执行离线 sweep 资格测试，从而同时发现即时故障和传统 NCCL/burn-in 检查看不到的 fail-slow。生产部署后，平均 FLOPs 利用率最高提高 1.7 倍，训练 step 的跨运行波动由 20% 降至 1%，并减少节点诊断和人工排障开销。
  - 相较只检查硬故障的 burn-in，核心创新是把训练中在线 slow-node 监测与上岗前离线资格扫描结合。
  - 大模型训练可靠性、慢节点检测、节点准入

- [FlashInfer-Bench: Building the Virtuous Cycle for AI-driven LLM Systems](https://proceedings.mlsys.org/paper_files/paper/2026/hash/37e44c4b5321605735be9761f9b758fc-Abstract-Conference.html)
  - Carnegie Mellon University；Shanli Xing、Yiyan Zhai、Alexander Jiang 等
  - FlashInfer-Bench 不是一个执行任务的通用 Agent，而是一套让“GPU 内核生成 Agent”可以被训练、比较并接入生产的闭环基础设施。它用 FlashInfer Trace 统一描述算子、负载、实现和评测，提供真实服务数据、正确性/性能测试与排行榜，并通过 apply 机制把最佳候选动态替换进 vLLM 或 SGLang。论文还用该闭环比较不同 GPU 编程语言和 Agent 的失败模式，因此其产物同时是数据集、评测平台和生产 kernel 接入协议。
  - 相较只在独立 benchmark 上打分 Agent 代码，核心创新是统一 trace 让生成、验证、排行榜和生产动态替换形成闭环。
  - Agent Infra—内核生成闭环、Agent 评测、生产 Kernel 替换

- [CRAFT: Fine-Grained Cost-Aware Expert Replication For Efficient Mixture-of-Experts Serving](https://proceedings.mlsys.org/paper_files/paper/2026/hash/3a7f9e485845dac27423375c934cb4db-Abstract-Conference.html)
  - University of Toronto；Adrian Zhao、Zhenkun Cai、Zhenyu Song 等
  - CRAFT 是 MoE 推理服务中的专家副本规划器，输入各层专家负载和可用显存，输出每层应复制哪些专家及复制数量。它不按热度简单复制所有热门专家，而是估计每个额外副本对负载均衡的边际收益，在固定内存预算下避免无效副本反而挤占 KV Cache 或 batch 空间。对象是数百亿到万亿参数 MoE；相对现有复制方案，平均提升 1.14 倍、最高 1.2 倍端到端 serving 吞吐。
  - 相较按全局热度复制专家，核心创新是计算每层每个副本的边际均衡收益并在显存预算内选择。
  - MoE Serving、专家副本规划、显存预算负载均衡

- [Stream2LLM: Overlap Context Streaming and Prefill for Reduced Time-to-First-Token](https://proceedings.mlsys.org/paper_files/paper/2026/hash/3b3889d313ba9476c12c2d77ea66b24f-Abstract-Conference.html)
  - Georgia Institute of Technology；Rajveer Bachkaniwala、Chengqi Luo、Richard So 等
  - Stream2LLM 是支持上下文边到达边 prefill 的 LLM 服务系统，面向网页抓取、向量检索等返回时间不确定的 RAG 场景。它分别处理只追加内容和会修改旧内容的两类流，利用最长公共前缀保留有效 KV，并以硬件成本模型决定抢占和资源分配，使检索等待可以与 GPU 计算重叠。评测使用网页抓取和 ANN 检索形成的真实流式负载，区分 append 与 update 两种上下文变化，并在吞吐不降的情况下把 TTFT 最多改善 11 倍。
  - 相较等待完整检索结果后一次 prefill，核心创新是在并发、多种上下文更新语义下安全地流式 prefill 并成本感知抢占。
  - RAG Serving、流式检索、增量 Prefill 调度

- [FlexTrain: Scalable Hybrid-Parallel Training with Elastic Resource Utilization and Consistent Accuracy](https://proceedings.mlsys.org/paper_files/paper/2026/hash/3c40417b8dca30c08cc361df5b33ad7e-Abstract-Conference.html)
  - Hong Kong University of Science and Technology (Guangzhou)；Weilin Cai、Diandian Gu、Baoquan Zhong 等
  - FlexTrain 是共享 GPU 集群中的弹性大模型训练系统，能在训练过程中接收或释放 GPU，同时控制数值执行顺序是否变化。它优先只调整流水线并行度以保持确定性，需要更高弹性时才改变数据并行度，并用自动 schedule 生成和性能预测判断一次扩缩容是否值得。保持数值一致时弹性作业最高加速 1.73 倍；若允许数据顺序变化，则可联合调整 DP 获得最高 2.27 倍加速。
  - 相较仅追求 GPU 利用率的弹性训练，核心创新是把数值/精度一致性作为扩缩容的显式约束。
  - 弹性 LLM 训练、混合并行调整、精度一致性

- [SAKURAONE: An Open Ethernet–Based AI HPC System and Its Observed Workload Dynamics in a Single-Tenant LLM Development Environment](https://proceedings.mlsys.org/paper_files/paper/2026/hash/40b8fb4f90004405e14b1ede6ab42373-Abstract-Conference.html)
  - SAKURA internet Research Center；Fumikazu KONISHI、Yuuki Tsubouchi、Hirofumi Tsuruta
  - 这是一篇 SAKURAONE AI HPC 集群的系统设计与生产负载经验报告，而不是提出新的训练算法。系统由 800 张 H100、开放的 800 GbE SONiC/RoCE 网络和 2 PB 全闪存 Lustre 构成；对单一 LLM 项目的长期观测显示，资源消耗会从初期少量超大训练转向更多中等规模迭代任务。论文同时给出 HPL、HPCG、FP8 HPL-MxP 性能，并分析小作业数量占优、少数大作业消耗主要 GPU 时间以及项目阶段变化。
  - 相较封闭 InfiniBand AI 集群报告，核心贡献是验证开放 800 GbE/SONiC 的规模能力并提供单租户 LLM 生命周期的纵向数据。
  - AI HPC 集群、开放以太网/RoCE、LLM 负载画像

- [PRISM: Parametrically Refactor Inference for Speculative Decoding Draft Models](https://proceedings.mlsys.org/paper_files/paper/2026/hash/414fd191b3246a19a55741b938380136-Abstract-Conference.html)
  - University of Waterloo；Xuliang Wang、Yuetao Chen、Maochan Zhen 等
  - PRISM 是一种用于推测解码 drafter 的模型结构，目标是在不增加每次草稿成本的情况下提高候选 token 的准确率和接受长度。它把连续预测步骤的计算路径分配给不同参数子集，使总模型可以拥有更大容量、单步却只激活部分参数，因此从结构上解耦 drafter 容量与延迟。它在已经高度优化的 serving engine 上仍将解码吞吐提高 2.6 倍以上，并显示扩大训练数据时接受率比传统 drafter 结构增长更好。
  - 相较增大整个 drafter，核心创新是让不同预测步激活不同参数子集，从而容量增大但单步计算不随之增长。
  - 推测解码 Drafter 架构、参数路径重构、接受率

- [Efficient Long-Context Language Model Training by Core Attention Disaggregation](https://proceedings.mlsys.org/paper_files/paper/2026/hash/423b59ae02381f27862c21d1c41a5603-Abstract-Conference.html)
  - Carnegie Mellon University；Yonghao Zhuang、Junda Chen、Bo Pang 等
  - CAD 是一种将长上下文训练中的 core attention 从模型其他部分物理拆开的并行方法，DistCA 是其系统实现。由于 softmax(QKᵀ)V 无参数，系统可把它切成 token 级任务发送到独立 attention server 池，并动态重组批次、重叠通信，从而消除不同文档长度在数据并行和流水线并行中造成的 straggler。在 512 张 H200、最长 512K context 上，系统使 attention server 间计算和显存接近平衡，较 Megatron-LM 最高提升 1.9 倍训练吞吐。
  - 相较在每个模型副本内平衡 attention，核心创新是利用 core attention 无参数特性把它做成可跨请求重组的独立计算服务。
  - 长上下文训练、Core Attention 解耦、Attention Server

- [Demystifying the Mixture of Experts Serving Tax](https://proceedings.mlsys.org/paper_files/paper/2026/hash/42a452cbafa9dd64e9ba4aa95cc1ef21-Abstract-Conference.html)
  - University of Washington；Pratyush Patel、Dayeol Lee、Shintaro Iwasaki 等
  - 这是一项对 MoE serving tax 的系统测量和解析建模工作，而不是新的 MoE 服务框架。作者用微基准把 MoE 比等 FLOPs 稠密模型慢 2–3 倍的原因拆成专家负载、通信和执行组件，并用 balls-bins-buckets 模型解释为何负载不均会拖慢 prefill、却可能因少激活专家而帮助 decode。分析覆盖不同 MoE 架构、prefill/decode 阶段和并行方式，最终给出哪些 fine-grained expert、data-parallel attention 等设计会转移而非消除税费。
  - 相较给出单一优化，核心创新是建立能分离 phase、架构与并行因素的 MoE tax 解析框架，并揭示负载不均对 decode 的反直觉作用。
  - MoE Serving 性能建模、Serving Tax、阶段差异

- [Sparing Strategies to Minimize Reliability Impact On Large Training Jobs](https://proceedings.mlsys.org/paper_files/paper/2026/hash/437bc4ccafd3fc6d4289bd10940be42b-Abstract-Conference.html)
  - Meta；Kevin Quirk、Matthew Lennie、Ehsan K. Ardestani 等
  - 这项工作为 Meta 大模型训练集群提供备用资源配置的解析决策工具，输入硬件故障率、计算块结构和作业规模，输出备用块与 GPU tray 的合理数量。闭式模型估算不同方案对故障恢复、资源浪费和训练 goodput 的影响，再用离散事件仿真交叉验证，替代仅凭经验预留资源。模型已用于 Meta hyperscale 集群的真实规划，在计算资源冗余、故障恢复时间和训练 goodput 之间给出一阶可执行建议。
  - 相较经验式预留固定比例 GPU，核心创新是用闭式模型联合优化备用块粒度、数量和硬件层级。
  - 训练集群容错、备用资源规划、Goodput 建模

- [SkipKV: Selective Skipping of KV Generation and Storage for Efficient Inference with Large Reasoning Models](https://proceedings.mlsys.org/paper_files/paper/2026/hash/45c1f6a8cbf2da59ebf2c802b4f742cd-Abstract-Conference.html)
  - Intel Labs；Jiayi Tian、Seyedarmin Azizi、Yequan Zhao 等
  - SkipKV 是面向长链式推理的训练免 KV 压缩与生成控制方法，它处理的不是普通对话中的低价值 token，而是 CoT 中语义重复的完整句子。系统按句子相似度同时跳过这些片段的 KV 生成和存储，并动态修改隐藏状态抑制模型再次生成冗余论证，因此同时缩小缓存和最终序列。多种推理 benchmark 上，它在相近缓存预算下最高提高 26.7% 准确率，生成长度最多缩短 1.6 倍、吞吐最高提高 1.7 倍。
  - 相较 token 级 eviction，核心创新是按语义句子同时跳过 KV 和冗余文本生成，解决 CoT 被压缩后反而变长的问题。
  - 推理链 KV 压缩、句子级冗余消除、生成长度控制

- [PROMPTS: PeRformance Optimization via Multi-Agent Planning for LLM Training and Serving](https://proceedings.mlsys.org/paper_files/paper/2026/hash/48253da5351effdfea994fd7bbff7005-Abstract-Conference.html)
  - Google；Yuran Ding、Ruobing Han、Xiaofan Zhang 等
  - PROMPTS 是为大规模 LLM 训推寻找并行配置的多 Agent 优化器，而不是直接执行用户任务的应用 Agent。Analyzer Agent 读取 profiler 数据定位通信或计算瓶颈，Proposal Agent 再从系统知识库检索规则并给出带理由的分片方案；它用推理缩小搜索空间，而不是进行昂贵的黑盒穷举。八个真实工作负载涵盖稠密/MoE、预训练/后训练/服务以及 2–2048 个 TPU；一次调用的前三个建议总能包含专家生产配置，首选命中率为 87.5%。
  - 相较人工调参或无语义黑盒搜索，核心创新是让 Agent 用 profiler 证据与系统知识生成并解释少量高质量候选。
  - Agent for Systems—并行配置、Profiler 驱动规划、多 Agent 优化

- [Wave: A Symbolic Python DSL And Compiler for High-Performance Machine Learning](https://proceedings.mlsys.org/paper_files/paper/2026/hash/48c34730ff9a8574481a00ce8cb5e2cb-Abstract-Conference.html)
  - AMD；Harsh Menon、Oleksandr Zinenko、Gaurav Verma 等
  - Wave 是嵌入 Python 的 GPU 内核 DSL 和编译器，输入以 tile/符号表达的计算，输出面向 AMD 等矩阵核心的低层高性能内核。编译器负责推导复杂的地址、布局和硬件映射，让作者保留对核心计算结构的控制，而无需手写专用矩阵单元的寻址细节。实验表明生成 kernel 的性能可匹配或超过现有 DSL 与库，适用对象是需要显式控制 matrix core 和内存层次的高性能算子。
  - 相较让程序员手算 matrix-core 地址，核心创新是符号编译器自动推导映射但仍保留 DSL 对 kernel 结构的表达。
  - GPU Kernel DSL、符号编译、矩阵核心映射

- [A Lightweight High-Throughput Collective-Capable NoC for Large-Scale ML Accelerators](https://proceedings.mlsys.org/paper_files/paper/2026/hash/48fecef47b19fe501d27d338b6d52582-Abstract-Conference.html)
  - ETH Zurich；Luca Colagrande、Lorenzo Leone、Chen Wu 等
  - 这项工作提出一种为 ML 加速器定制的片上网络硬件，目标是在多 chiplet/核心间直接支持 barrier、multicast 和 reduction 等集体操作。它把同步和数据归约逻辑放进网络路由路径，而不是由端点反复收发软件消息，因此能以较小硬件开销提高常见分布式算子的带宽。硬件在 1–32 KiB 数据的 multicast 和 reduction 上分别获得 2.9 倍与 2.5 倍几何平均加速，重点针对 ML accelerator 内部而非数据中心网络。
  - 相较用软件 collective 占用端点核心，核心创新是以小型 NoC 原语直接在网络内完成同步、组播和归约。
  - ML 加速器 NoC、片上集体通信、网络内归约

- [Meeting SLOs, Slashing Hours: Automated Enterprise LLM Optimization with OptiKIT](https://proceedings.mlsys.org/paper_files/paper/2026/hash/4904fad153f6434a7bcf04465d4be2cc-Abstract-Conference.html)
  - eBay；Nicholas Santavas、Kareem Eissa、Patrycja Cieplicka 等
  - OptiKIT 是企业内部的分布式模型优化流水线，接收模型、目标硬件和 SLO，由系统自动组合压缩、量化与调优步骤并验证结果。它把原本需要专家逐项操作的模型优化做成可重复工作流，使应用团队能够在不理解底层细节的情况下获得两倍以上 GPU 吞吐。生产结果显示 GPU 吞吐提高两倍以上；框架面对的是多个团队和模型的重复优化需求，而不是一次性的单模型 benchmark。
  - 相较专家手工逐模型优化，核心创新是把多种压缩和调优步骤产品化为非专家可重复执行的分布式 workflow。
  - 企业 LLM 优化平台、自动压缩与调优、SLO

- [SONAR: Benchmarking Topology and Collaboration in Decentralized Learning](https://proceedings.mlsys.org/paper_files/paper/2026/hash/4abf39685e89559523a4d644036fd2b3-Abstract-Conference.html)
  - MIT、EPFL；Joyce Yuan、Yichuan Shi、Abhishek Singh 等
  - SONAR 是研究去中心化学习的可控实验与基准框架，不是提出某一种最优通信拓扑。它把通信协议、动态图拓扑和细粒度 telemetry 放在统一运行时中，让同一训练任务可以替换 ring、随机图等连接方式，并同时测量收敛、通信、鲁棒性和隐私。实验显示拓扑本身就是影响收敛和通信行为的主导变量，说明不能只在固定 ring 或全连接模拟器上比较去中心化算法。
  - 相较各论文在不同拓扑和模拟器上报告结果，核心创新是提供可替换拓扑、统一 telemetry 的可复现实验控制面。
  - 去中心化学习基准、网络拓扑效应、P2P Telemetry

- [Virtual Machine NUMA Placement at Scale: Learning the Norm, Shielding the Tail](https://proceedings.mlsys.org/paper_files/paper/2026/hash/4e3157021c5f833bb2204081f1dda573-Abstract-Conference.html)
  - Northeastern University；Yibo Zhao、Tianyuan Wu、Hui Xue 等
  - Catur 是大规模云环境中的 VM NUMA 放置系统，输入 VM 配置、宿主 NUMA 结构和历史性能，输出 CPU/内存的拓扑绑定方案。它从大量生产实例学习正常性能边界，并在放置时重点隔离会形成长尾资源缺陷的组合，在一亿 VM 轨迹上显著优于固定 hypervisor 规则。在一亿 VM 的生产 trace 上，平均 resource defect 比先进 hypervisor 策略降低 34.2%–50.0%，关注平均利用率之外的 NUMA 长尾。
  - 相较固定 NUMA heuristic，核心创新是从海量生产实例学习正常边界并专门抑制长尾异常放置。
  - 云 VM NUMA 放置、学习型资源调度、长尾隔离

- [Automated Algorithm Design for Auto-Tuning Optimizers](https://proceedings.mlsys.org/paper_files/paper/2026/hash/4f31327e046913c7238d5b671f5d820e-Abstract-Conference.html)
  - Leiden University；Floris-Jan Willemsen、Niki van Stein、Ben van Werkhoven
  - 这项工作不是让 LLM 直接为应用选择一个参数，而是让它生成完整的自动调优搜索算法。系统把目标空间和反馈接口描述给 LLM，由其产出可执行优化器，再在真实 tuning 任务上迭代评测算法质量，使搜索策略本身也成为自动设计对象。系统在多个高性能应用调优 benchmark 上执行生成的优化器，最佳算法平均比现有人工设计的 auto-tuner 提高 72.4%。
  - 相较用 LLM 直接猜配置，核心创新是让 LLM 产出可重复运行、可继续搜索的优化算法本身。
  - Agent for Systems—自动调优算法生成、LLM 元优化

- [RaidServe: High-performance Resilient Serving](https://proceedings.mlsys.org/paper_files/paper/2026/hash/507b4aacefe5325908e24f042617b741-Abstract-Conference.html)
  - Shanghai Jiao Tong University；Ziyi Xu、Zhiqiang Xie、Swapnil Gandhi 等
  - RaidServe 是张量并行 LLM 服务的容错运行时，目标是在某张 GPU 离线后继续服务，而不是等待整组重启和重新计算 KV Cache。它重新映射张量分片与缓存状态、利用剩余和替补 GPU 恢复均衡执行，从而避免单点故障导致整个 TP group 停止。在 8×H100 DGX 和真实故障 trace 上，它比标准故障处理实现最高两倍吞吐，并把恢复延迟降低约两个数量级。
  - 相较故障后重启 TP group 或全量复制 KV，核心创新是在 GPU 数量不规则变化时重构分片和状态仍保持服务。
  - 容错 LLM Serving、张量并行恢复、KV 状态重映射

- [Toward Principled LLM Safety Testing: Solving the Jailbreak Oracle Problem](https://proceedings.mlsys.org/paper_files/paper/2026/hash/50a2e625745ab078389ccd23747fc0d8-Abstract-Conference.html)
  - Northeastern University；Shuyi Lin、Anshuman Suri、Alina Oprea 等
  - 这项工作先把“某模型在给定 prompt 和解码策略下是否存在概率超过阈值的越狱输出”形式化为 jailbreak oracle。BOA 是求解该问题的搜索系统：先广度采样找到高概率攻击，再按 token 级安全分数进行深度优先搜索低概率路径，从而把安全测试从随机 red teaming 变成可比较的覆盖问题。该形式化支持在统一阈值下比较 red-team 攻击、评估防御漏网路径，甚至给出模型在限定条件下的安全认证结论。
  - 相较靠随机 prompt 攻击统计成功率，核心创新是把越狱存在性定义为概率阈值搜索问题并系统探索低概率路径。
  - LLM 安全评测、越狱 Oracle、概率路径搜索

- [HetRL: Efficient Reinforcement Learning for LLMs in Heterogeneous Environments](https://proceedings.mlsys.org/paper_files/paper/2026/hash/5321b1dabcd2be188d796c21b733e8c7-Abstract-Conference.html)
  - ETH Zurich；Yongjun He、Shuai Zhang、Jiading Gai 等
  - HetRL 是在 GPU 和网络异构集群上运行 LLM 强化学习的分布式系统，统一管理 actor、reference、reward 等多个模型以及 rollout、训练和数据传输任务。调度器根据各阶段的计算特性和设备能力做放置与流水，而不是假设每张 GPU 等速，由此减少异构环境中的等待和资源碎片。评测消耗约两万 GPU 小时、覆盖多类模型和异构网络，吞吐最高为现有系统的 9.17 倍、平均为 3.17 倍。
  - 相较假设 GPU 与网络同质的 RL 系统，核心创新是联合编排多模型、多任务及异构设备/链路。
  - LLM 强化学习训练、异构集群调度、多模型流水

- [Event Tensor: A Unified Abstraction for Compiling Dynamic Megakernel](https://proceedings.mlsys.org/paper_files/paper/2026/hash/53d3f45797970d323bd8a0d379c525aa-Abstract-Conference.html)
  - Carnegie Mellon University；Hongyi Jin、Bohan Hou、Guanjie Wang 等
  - Event Tensor 是编译动态 megakernel 的中间抽象：它把大算子拆成 tile 任务，并显式记录任务间何时产生、等待和消费事件。ETC 编译器据此把静态可确定部分提前排程、把数据依赖部分留到 GPU 运行时调度，使动态 shape 和条件执行也能融合进持久内核。评测表明动态工作负载上 ETC 保持先进 LLM serving latency，并显著降低需要为 shape 逐个编译 CUDA Graph 的系统 warmup。
  - 相较静态 CUDA Graph 或只支持固定 shape 的 megakernel，核心创新是用 Event Tensor 表达运行时才知道的 tile 依赖。
  - 动态 Megakernel 编译、Event Tensor、GPU 任务调度

- [MLCommons Chakra: Advancing Performance Benchmarking and Co-design using Standardized Execution Traces](https://proceedings.mlsys.org/paper_files/paper/2026/hash/53fe824f289060ce705ed7c01dae59d2-Abstract-Conference.html)
  - MLCommons；Srinivas Sridharan、Andy Balogh、Bradford M. Beckmann 等
  - MLCommons Chakra 是分布式 ML 性能研究的标准 Trace 生态，输入真实训练作业中的计算与通信事件，输出可移植、可修改并可回放的执行描述。研究者可以用同一 Trace 复现实机负载、比较系统和探索未来互连，因此它解决的是 benchmark 与软硬件协同设计之间缺少共同语言的问题。Trace 不绑定特定框架或硬件，可被编辑后回放不同模型规模、并行方式和互连，以支持未来系统的 what-if 分析。
  - 相较 framework-specific trace，核心创新是形成可移植、可修改、可回放的标准执行语义，连接 benchmark 与硬件设计。
  - 分布式训练 Trace、可回放基准、软硬件协同设计

- [AIRS: Scaling Live Inference in Resource Constrained Environments](https://proceedings.mlsys.org/paper_files/paper/2026/hash/547108084f0c2af39b956f8eadb75d1b-Abstract-Conference.html)
  - Google；Nilesh Jagnik、Xiaohao Yang、Tuan Do 等
  - AIRS 是 Meta 生产环境中为内容或模型结果生成 AI 评分的在线推理服务，面对多种评测流程共享有限 TPU、且高优先级任务必须快速完成的约束。它将模型调用组织为可恢复的流水线，并跨工作流分配和批处理 TPU 请求，在可靠生成评分的同时兼顾后台吞吐与前台延迟。调度同时考虑任务优先级、模型执行形态和 TPU 资源占用，使耗时数天的离线流程与需即时返回的在线评分共享同一资源池。
  - 相较把不同 AI 评分任务各自建服务，核心创新是以共享、优先级感知的可靠流水线统一承载实时和批量 rating。
  - 生产 AI 评分服务、TPU 优先级调度、可靠推理流水

- [Speculative Decoding: Performance or Illusion?](https://proceedings.mlsys.org/paper_files/paper/2026/hash/554e056fe2b6d9fd27ffcd3367ae1267-Abstract-Conference.html)
  - University of California, Berkeley；Xiaoxuan Liu、Jiaxiang Yu、Jongseok Park 等
  - 这是一项在生产级 vLLM 上评估推测解码真实收益的实验研究，而不是提出新的解码算法。作者覆盖 n-gram、EAGLE、draft model 等多类方案和不同 batch，发现 target verification 常是主耗时且接受长度随 token 位置和数据剧烈变化，说明小 batch 论文结果不能直接代表线上收益。结果揭示验证阶段常主导总时延，且接受长度会随输出位置、请求和数据集变化；高并发下部分方法甚至不再加速。
  - 相较小 batch 研究原型结论，核心创新是首次在生产 vLLM 和真实并发范围系统揭示推测解码收益边界。
  - 推测解码实证研究、vLLM、高并发收益边界

- [ProTrain: Efficient LLM Training via Automatic Memory Management](https://proceedings.mlsys.org/paper_files/paper/2026/hash/56280ad5fb53967fd55e4ba1b1cfc418-Abstract-Conference.html)
  - University of Massachusetts Amherst；Hanmei Yang、Jin Zhou、Yao Fu 等
  - ProTrain 是自动选择大模型训练内存策略的运行时，输入模型图、设备显存和计算/通信特征，输出每个张量应保留、重计算还是卸载的执行计划。它把这些选择联合优化并自动应用，避免工程师手工配置导致 OOM 或过度重算，使不同模型和硬件上的策略能够自适应。跨模型和硬件实验中，自动策略相对先进训练系统提高 1.43–2.71 倍吞吐，并免去每次换模型后重新手调策略。
  - 相较人工为每个模型选择 checkpoint/offload，核心创新是根据模型图和硬件自动求解并落实张量级内存策略。
  - LLM 训练显存管理、自动重计算/卸载、策略搜索

- [BatchLLM: Optimizing Large Batched LLM Inference with Global Prefix Sharing and Throughput-oriented Token Batching](https://proceedings.mlsys.org/paper_files/paper/2026/hash/5b7ae1758452854dee4e962207d38304-Abstract-Conference.html)
  - Microsoft；Zhen Zheng、Xin Ji、Taosong Fang 等
  - BatchLLM 是为离线或批处理 LLM 任务设计的推理引擎，重点处理大量请求共享系统提示、文档等非局部前缀的情况。它先在整个任务集合中构建全局前缀复用关系，再按吞吐而非流式公平性组织 token batch，因此能跨请求避免重复 prefill。在不同 GPU 和典型工业 batch 上，相对 vLLM/SGLang 提高 1.3–10.8 倍，收益来自跨整个任务集合而非单请求前缀的复用。
  - 相较只在单请求内做 prefix cache，核心创新是跨整个离线 batch 发现全局共享前缀并围绕总吞吐重新组 batch。
  - 离线批量 LLM 推理、全局前缀复用、吞吐导向 Batching

- [DisAgg: Distributed Aggregators for Efficient Secure Aggregation](https://proceedings.mlsys.org/paper_files/paper/2026/hash/5c40a52354e95a6fc701a84cdcd97bc8-Abstract-Conference.html)
  - Samsung Research；Haaris Mehmood、Giorgos Tatsis、Dimitrios Alexopoulos 等
  - DisAgg 是联邦学习的安全聚合协议，目标是让服务器只得到所有客户端更新之和，而看不到任何单个更新。每个客户端把更新向量做秘密分享并发送给少量被选为 Aggregator 的客户端，后者本地累加份额，服务器最后只重构聚合结果，从而把昂贵的中心可信聚合拆散。服务器只接收聚合份额，协议因此适合不希望中央方看到更新的 federated training；计算负担由小规模客户端委员会分担。
  - 相较中心服务器直接聚合或复杂多轮密码协议，核心创新是用小型客户端委员会秘密分享并只回传聚合份额。
  - 联邦学习安全聚合、秘密分享、分布式 Aggregator

- [OSWorld-Human: Benchmarking the Efficiency of Computer-Use Agents](https://proceedings.mlsys.org/paper_files/paper/2026/hash/5edb57c05c81d04beb716ef1d542fe9e-Abstract-Conference.html)
  - University of California, San Diego；Reyna Abhyankar、Qi Qi、Yiying Zhang
  - OSWorld-Human 是在 OSWorld 上增加人工最短操作轨迹的效率基准，用来区分 Agent 是“能完成任务”还是“以接近人的步骤和时间完成”。对 16 个 computer-use Agent 的测量显示，大模型规划、反思和裁判调用占主要延迟，而且上下文随步骤增长使后期单步可慢三倍，最佳系统仍比人工多 2.7–4.3 倍步骤。时间研究覆盖 planning、reflection、judging 等调用，并发现任务越长后续一步越慢，说明 Agent latency 不能只用平均单次模型调用估计。
  - 相较只按任务成功率评价 Agent，核心创新是引入人工轨迹作为步骤下界并分解端到端时间随步骤增长的来源。
  - Agent Evaluation—Computer Use、人工轨迹、端到端延迟

- [SwiftGS: Algorithm and System Co-Optimization for Fast 3D Gaussian Splatting on GPUs](https://proceedings.mlsys.org/paper_files/paper/2026/hash/5f96a21345c138da929e99871fda138e-Abstract-Conference.html)
  - Imperial College London；Lingjun Gao、Zhican Wang、Zhiwen Mo 等
  - SwiftGS 是 3D Gaussian Splatting 的算法—系统联合优化实现，输入已有 Gaussian 场景并输出实时渲染图像。它根据可见性自适应提前结束排序，以 GPU 友好的轴共享方式组织 rasterization，并动态调整阈值，减少对数百万 Gaussian 的冗余排序、存储和计算。相对 gsplat，SwiftGS 最高加速 1.41 倍且渲染质量几乎不变；这些优化还能与其他 3DGS 加速方法叠加。
  - 相较只改 3DGS 算法或只调 CUDA kernel，核心创新是从排序、光栅化和阈值三处联合消除跨层冗余。
  - 3D Gaussian Splatting、GPU 光栅化、算法-系统协同

- [PARROT: Persuasion and Agreement Robustness Rating of Output Truth — A Sycophancy Robustness Benchmark for LLMs](https://proceedings.mlsys.org/paper_files/paper/2026/hash/621d0fd41c720ab252e178b77c200d90-Abstract-Conference.html)
  - 作者未在可解析元数据中标明机构；Yusuf Çelebi、Özay Ezerceli、Mahmoud El Hussieni
  - PARROT 是测量 LLM 谄媚性的行为基准，而不是防御或微调方法。它将同一道题分别以中性措辞和“权威给出错误答案”的措辞呈现，通过输出概率变化和八类状态判断模型是坚持正确、被说服还是强化原错误，从而把笼统的准确率下降拆成可解释行为。评测包含 22 个模型、1302 道跨 13 领域题目；强模型 follow rate 低至 4%，部分小模型在权威压力下超过 90%。
  - 相较单一准确率或 follow rate，核心创新是成对控制问题、概率校准和八状态因果分类共同刻画谄媚。
  - LLM 行为评测、谄媚与权威压力、置信度校准

- [Search Your Block Floating Point Scales!](https://proceedings.mlsys.org/paper_files/paper/2026/hash/633b0e871a48d542280c3ad03928e60d-Abstract-Conference.html)
  - Cornell；Tanmaey Gupta、Hayden Prairie、Xiaoxia wu 等
  - ScaleSearch 是为 NVFP4 等 block floating-point 格式选择共享 scale 的量化算法。它不沿用固定最大值或简单统计量，而是在格式可表示的尾数尺度上细粒度搜索，使每个数值块的 scale 直接最小化量化误差；相同思路也被用于 attention 中间值。ScaleSearch 将 NVFP4 量化误差降低 27%，并在 Qwen3-8B 的 MATH500 上把 PTQ 得分最多提高 15 分。
  - 相较按 max/固定统计量定 scale，核心创新是直接搜索 microscaling 格式的可用尾数以最小化块级误差。
  - Block Floating-Point 量化、Scale 搜索、NVFP4

- [Accelerating Large-Scale Reasoning Model Inference with Sparse Self-Speculative Decoding](https://proceedings.mlsys.org/paper_files/paper/2026/hash/66a026c0d17040889b50f0dfa650e5e0-Abstract-Conference.html)
  - University of California, Berkeley；Yilong Zhao、Jiaming Tang、Kan Zhu 等
  - SparseSpec 是面向长 CoT 模型的 self-speculative decoding 系统，目标模型的稀疏子网络同时充当 drafter，因此无需额外小模型及其参数。系统把 draft 和 verify 请求放入统一 scheduler，延迟验证以重叠 CPU/GPU 工作，并动态把 KV Cache 卸载到主机，解决长输出转为显存带宽瓶颈的问题。三项系统机制分别扩大 draft/verify 并行、隐藏 CPU 控制开销和释放 GPU 缓存空间，面向的是长 reasoning model 而非普通短回答。
  - 相较额外 drafter 模型，核心创新是用同一 reasoning model 的稀疏子网自推测，并把调度、验证与 KV offload 协同。
  - 长推理自推测解码、稀疏 Drafter、KV Offload

- [StreamDiffusionV2: A Streaming System for Dynamic and Interactive Video Generation](https://proceedings.mlsys.org/paper_files/paper/2026/hash/698cfaf72a208aef2e78bcac55b74328-Abstract-Conference.html)
  - University of Texas at Austin；Tianrui Feng、Zhi Li、Shuo Yang 等
  - StreamDiffusionV2 是把离线视频扩散模型改造成实时交互直播服务的训练免流水线，必须同时满足首帧延迟、逐帧 deadline 和时间一致性。它联合 SLO 感知 batching、rolling KV、运动感知噪声控制，并沿去噪步和网络层跨 GPU 流水，因而不是逐帧运行独立图像扩散。四张 H100 上，14B 模型首帧低于 0.5 秒并达到 58.28 FPS；系统也支持 1–4 个去噪步和异构 GPU。
  - 相较把离线视频扩散逐帧搬到直播，核心创新是围绕首帧、逐帧 SLO 和多 GPU 去噪流水重新设计缓存与调度。
  - 实时视频扩散、多 GPU 去噪流水、帧级 SLO

- [Pylo: Towards Accessible Learned Optimizers in PyTorch](https://proceedings.mlsys.org/paper_files/paper/2026/hash/6b1d4c03391b0aa6ddde0b807a78c950-Abstract-Conference.html)
  - Mila；Paul Janson、Benjamin Thérien、Quentin Anthony 等
  - PyLO 是把 learned optimizer 带入 PyTorch 的可复用训练库，而不是重新训练一个特定任务模型。它将已经元训练好的优化器封装成标准 torch.optim.Optimizer 接口，并提供状态与更新算子的 PyTorch 实现，使用户可以像 Adam 一样插入现有训练循环。目标用户无需复现数千 TPU 月的元训练过程，便可在 PyTorch 项目中直接调用已有 learned optimizer 并进行公平复现。
  - 相较 learned optimizer 只存在于 JAX 研究代码，核心创新是提供兼容标准 PyTorch optimizer API 的可复用实现。
  - Learned Optimizer 工具链、PyTorch 生态、优化器复现

- [FaaScale: Unlocking Fast LLM Scaling for Serverless Inference](https://proceedings.mlsys.org/paper_files/paper/2026/hash/6e32c247076c2c0fb381e022c02d2c78-Abstract-Conference.html)
  - The Chinese University of Hong Kong, Shenzhen；Minchen Yu、Rui Yang、Chaobo Jia 等
  - FaaScale 是 Serverless LLM 的快速扩容系统，解决新 GPU 实例必须先完整复制大模型、冷启动期间无法处理请求的问题。其 PipeCast 将模型按块组播到多台节点，并让已收到不同层的节点立即组成临时 pipeline 执行推理，使参数传输与实际服务同时进行。真实 LLM trace 上，PipeCast 将 tail TTFT 最多降低五倍，并把 serverless 服务成本降低 31.3%。
  - 相较等模型完整加载后再服务，核心创新是组播参数的同时动态组建 pipeline 处理请求。
  - Serverless LLM Serving、模型组播、边传输边推理

- [FarSkip-Collective: Unhobbling Blocking Communication in Mixture of Experts Models](https://proceedings.mlsys.org/paper_files/paper/2026/hash/6feb9b30798abcfae937760d183605e1-Abstract-Conference.html)
  - AMD；Yonatan Dukler、Guihong Li、Deval Shah 等
  - FarSkip-Collective 通过修改 MoE 模型的数据依赖来消除 all-to-all 等阻塞式通信，而不是只优化通信库本身。它让远处层的独立计算越过尚未完成的 collective 执行，从模型图层面制造可重叠窗口，并在转换 16B–109B 模型后保持原有精度。作者把多种 16B–109B 开源 MoE 转换为可重叠版本，表明架构修改在不同规模上都能保持近似原始准确率。
  - 相较试图让 collective 本身更快，核心创新是修改模型依赖图来创造跨层计算越过阻塞通信的机会。
  - MoE 计算-通信重叠、模型依赖重构、Blocking Collective

- [REPARO: LOSS-RESILIENT GENERATIVE CODEC FOR VIDEO CONFERENCING](https://proceedings.mlsys.org/paper_files/paper/2026/hash/703f727ec10190b2fddcf8e24f52df48-Abstract-Conference.html)
  - MIT；Tianhong Li、Vibhaalakshmi Sivaraman、Pantea Karimi 等
  - Reparo 是面向视频会议丢包的生成式编解码系统，发送端不只是添加冗余 FEC，接收端还利用学习到的视频先验重建缺失帧或区域。它针对实时 deadline 组织恢复过程，从而同时减少连续丢包造成的冻结并提升 PSNR、SSIM 和感知质量。在公开会议视频数据和多种丢包模式下，Reparo 的 PSNR、SSIM、LPIPS 与冻结次数均优于 FEC 型方案。
  - 相较用冗余码硬恢复 packet，核心创新是利用生成模型的视频先验在实时约束下重建视觉内容。
  - 视频会议抗丢包、生成式 Codec、实时帧恢复

- [OPKV: A High-Throughput Plugin-Driven Framework for Recallable Sparsity in Paged KV Cache Systems](https://proceedings.mlsys.org/paper_files/paper/2026/hash/71381211d0abef73ed1887b83c4547b1-Abstract-Conference.html)
  - Southeast University；Huazheng Lao、Xiaofeng Li、Rui Xu 等
  - OPKV 是 paged KV Cache 的插件框架，用来接入“可召回稀疏”算法：被暂时移除的 KV 块在以后需要时仍能找回，而不是永久 eviction。它统一稀疏插件、页管理和 recall 调度，使不同算法不必重写 vLLM 类缓存系统，并降低多 batch 下召回带来的阻塞。在多种 batch 下，接入 OPKV 后现有稀疏方法的解码吞吐提高 1.3–1.8 倍，且无需改写分页缓存核心。
  - 相较每种 KV 稀疏算法单独侵入 page manager，核心创新是把 eviction 后可 recall 的语义抽象为统一插件和 scheduler。
  - 分页 KV Cache、可召回稀疏、插件化缓存管理

- [MAC-Attention: a Match--Amend--Complete scheme for fast and accurate attention computation](https://proceedings.mlsys.org/paper_files/paper/2026/hash/7398289396de403d7d0505ed791e704a-Abstract-Conference.html)
  - The Ohio State University、Microsoft、Anyscale；Jinghan Yao、Sam Ade Jacobs、Walid Krichene 等
  - MAC-Attention 是一种不删除 KV、不降低可访问历史范围的长上下文注意力复用算法。它先在近期 query 中 Match 相似项，再重算匹配边界进行 Amend，最后把复用结果与新 KV 尾部的精确注意力 Complete 合并；命中时开销不随总上下文长度增长。在 128K 上相对 FlashInfer，KV 访问最多减少 99%、token latency 降低 60% 以上，attention 阶段最高 14.3 倍、端到端最高 2.6 倍。
  - 相较压缩或删除历史 KV，核心创新是复用相似 query 的精确 attention 中间结果，并只修正边界和新尾部。
  - 长上下文 Attention 复用、KV I/O、Match-Amend-Complete

- [TokenWeave: Efficient Compute-Communication Overlap for Distributed LLM Inference](https://proceedings.mlsys.org/paper_files/paper/2026/hash/73ba81c7b25134a559c8a9c39ec1a4c3-Abstract-Conference.html)
  - MicrosoftResearchIndia；Raja Gond、Nipun Kwatra、Ramachandran Ramjee
  - TokenWeave 是张量并行 LLM 推理中的计算—通信重叠系统，针对 decode 小矩阵和短 token 批次难以隐藏 collective 延迟的问题。它把单个 token 的算子切成可交错执行的工作单元，并协调通信启动和 GPU 计算，使 vLLM、SGLang 等原本默认关闭的重叠在实际负载中可用。跨多个模型和负载，它在 token 数低至 1024 时仍获得最高 1.28 倍延迟加速和 1.19 倍吞吐提升。
  - 相较仅大 batch 才能隐藏 tensor-parallel 通信，核心创新是为短 token 工作量构造细粒度可重叠执行。
  - 张量并行推理、短序列通信重叠、细粒度流水

- [When Enough is Enough: Rank-Aware Early Termination for Vector Search](https://proceedings.mlsys.org/paper_files/paper/2026/hash/78834433edc3291f4c6cbbd2759324db-Abstract-Conference.html)
  - Princeton University；Jianan Lu、Asaf Cidon、Michael Freedman
  - Terminus 是磁盘型近邻图向量搜索的提前终止策略，输入当前候选排名和已经花费的 I/O，判断继续扩展图是否仍可能改变下游关心的 top-k 排名。它优化的是排序效用而非统一 recall，因此会把磁盘读取优先留给最可能影响 RAG 等应用结果的查询。评价重点是下游真正关心的高排名结果恢复，而不是让所有近邻 recall 相同，因此可在磁盘读取更少时保持应用效用。
  - 相较固定访问预算或 recall-based 停止，核心创新是按当前排名是否仍可能改变应用效用动态停止磁盘图遍历。
  - 磁盘向量检索、Rank-Aware 提前终止、RAG I/O

- [Spira: Exploiting Voxel Data Structural Properties for Efficient Sparse Convolution in Point Cloud Networks](https://proceedings.mlsys.org/paper_files/paper/2026/hash/7972f3735e104a54715922aa416fde1b-Abstract-Conference.html)
  - Max Planck Institute for Software Systems；Dionysios Adamopoulos、Anastasia Poulopoulou、Georgios Goumas 等
  - Spira 是利用体素坐标结构的 GPU sparse-convolution 执行引擎。它根据坐标为有界整数、同一物体表面邻居连续的性质改造哈希/邻居查找和 kernel 调度，避免通用稀疏算子为不存在位置付出大量随机访存。不同点云层配置上，layer kernel 平均加速 2.11 倍、最高 3.44 倍；端到端推理平均加速 1.68 倍。
  - 相较通用 sparse-convolution 哈希，核心创新是把体素整数、有界、表面连续三种几何先验写进 GPU 数据结构和执行。
  - 点云稀疏卷积、体素结构感知、GPU Kernel

- [Efficient, VRAM-Constrained xLM Inference on Clients](https://proceedings.mlsys.org/paper_files/paper/2026/hash/7cd265ae802235b8d5778a4a96ff22dd-Abstract-Conference.html)
  - NVIDIA；Aditya Ukarande、Deep Shekhar、Marc Blackstein 等
  - 这项工作提出 profile 引导的 CPU-GPU pipelined sharding，用于在用户指定 VRAM 上限下无损运行 LLM 和 VLM。模型被切到子层粒度，系统按阶段和带宽决定哪些张量常驻 GPU、哪些由 CPU 计算或流水传入，并让复制与计算重叠，而不是简单逐层卸载。评测同时包含 dense/MoE LLM、高分辨率 VLM、交互与 batch 模式；LLM TPS 最高提升 30 倍，VLM 显存需求最高降低十倍。
  - 相较粗粒度整层 CPU offload，核心创新是按 profile 做子层分片、优先 VRAM 放置与 copy-compute pipeline，并统一 dense/MoE/VLM。
  - 客户端 LLM/VLM、CPU-GPU 混合执行、VRAM 预算

- [MTraining: Distributed Dynamic Sparse Attention for Efficient Ultra-Long Context Training](https://proceedings.mlsys.org/paper_files/paper/2026/hash/7fafdf453029d7b8674b6f3dd18112bf-Abstract-Conference.html)
  - University of Cambridge；Wenxuan Li、Chengruidong Zhang、Huiqiang Jiang 等
  - MTraining 是支持动态稀疏注意力的超长上下文分布式训练系统。由于每个 head 和每一步实际保留的块不同，它同时重排 worker 间任务和 step 内执行顺序，让稀疏性带来的计算节省不会被最慢 GPU 与通信同步抵消。RULER、PG-19、InfiniteBench 等任务上，MTraining 在保持准确率的同时最高提高六倍训练吞吐。
  - 相较只平衡静态稀疏矩阵，核心创新是同时处理 worker 与 step 两级、随输入变化的动态稀疏失衡。
  - 超长上下文训练、动态稀疏 Attention、双层负载均衡

- [TeleRAG: Efficient Retrieval-Augmented Generation Inference with Lookahead Retrieval](https://proceedings.mlsys.org/paper_files/paper/2026/hash/7fd522b89ac21009b7bbe7560a9a5add-Abstract-Conference.html)
  - University of Washington；Chien-Yu Lin、Keisuke Kamahori、Yiyu Liu 等
  - TeleRAG 是将检索数据移动与 LLM 生成并行化的 RAG 推理系统，主要面向大向量库驻留 CPU、GPU 只缓存热点数据的部署。Lookahead retrieval 根据当前生成提前预测下一步需要的数据并异步搬到 GPU，再由预取和缓存感知 scheduler 协调多请求，避免模型等待检索传输。单请求平均端到端延迟最高改善 1.98 倍，batch 吞吐提高 1.83 倍；显存只保存实际热点检索数据。
  - 相较检索完成后再传数据，核心创新是从生成进度预测将用到的检索数据并与 LLM compute 并行预取。
  - RAG Serving、Lookahead Retrieval、CPU-GPU 预取

- [MorphServe: Efficient and Workload-Aware LLM Serving via Runtime Quantized Layer Swapping and KV Cache Resizing](https://proceedings.mlsys.org/paper_files/paper/2026/hash/8144a9d62e506af0fcdeac0e456b2710-Abstract-Conference.html)
  - University of Virginia；Zhaoyuan Su、Zeyu Zhang、Tingfeng Lan 等
  - MorphServe 是能在运行中改变模型精度和 KV 容量的自适应 LLM 服务系统，而非部署前一次性量化模型。负载上升时，它按 token 边界把影响较小的层切换成量化副本，并立即把释放的显存扩给 KV Cache；负载下降后又恢复高精度层，因此在同一会话中保持状态连续。在真实突发 trace 上，平均 SLO violation 减少 92.45%，P95 TTFT 改善 2.2–3.9 倍，并保持生成质量。
  - 相较部署前静态量化或独立压 KV，核心创新是会话不中断地联合改变层精度和 KV 容量。
  - 自适应 LLM Serving、在线层量化、KV Cache 扩缩

- [CSLE: A Reinforcement Learning Platform for Autonomous Security Management](https://proceedings.mlsys.org/paper_files/paper/2026/hash/87eaaa8605a1a472d9a9756e7500517b-Abstract-Conference.html)
  - KTH Royal Institute of Technology；Kim Hammar
  - CSLE 是把安全控制强化学习从纯模拟器推进到接近真实网络环境的实验平台。其 emulation 系统运行虚拟化服务并采集日志来辨识 MDP，simulation 系统快速训练流控、复制、分段或恢复策略，学到的策略再回到 emulation 验证并修正模型。平台通过 flow、replication、segmentation 和 recovery 四类用例验证，目标是让学到的策略能在接近生产的系统条件下工作。
  - 相较只在抽象 simulator 训练安全策略，核心创新是 emulation 采样建模、simulation 训练、再回 emulation 验证的闭环。
  - 自主安全管理、Sim-to-Real 强化学习、网络系统控制

- [The OpenHands Software Agent SDK: A Composable and Extensible Foundation for Production Agents](https://proceedings.mlsys.org/paper_files/paper/2026/hash/8ae9cf363ea625161f885b798c1f1f78-Abstract-Conference.html)
  - OpenHands；Xingyao Wang、Simon Rosenberg、Juan Michelini 等
  - OpenHands Software Agent SDK 是构建和部署软件工程 Agent 的运行基础，而不是某个单独的 coding agent 策略。它定义可扩展的 Agent/工具/记忆接口，并内置沙箱、本地到远端执行迁移、事件溯源、生命周期控制、多模型路由及 VS Code/CLI/API 交互。与通用模型厂商 SDK 相比，它把 sandboxed execution、事件溯源、远程生命周期和用户界面连接做成同一套生产架构。
  - 相较只提供 Agent 调用 API，核心创新是把可组合策略接口、安全沙箱、远程执行和生命周期做成统一生产 SDK。
  - Agent Infra—软件 Agent SDK、沙箱执行、生命周期管理

- [Agentic Operator Generation for ML ASICs](https://proceedings.mlsys.org/paper_files/paper/2026/hash/8c54e9bfed4119c873f575d1d1e2f0a0-Abstract-Conference.html)
  - Meta；Alec Hammond、Aram Markosyan、Aman Dontula 等
  - TritorX 是为新 ML ASIC 自动补齐 PyTorch ATen 后端的 Agent 系统，输出的是可编译、通过测试的 Triton 内核和 wrapper。LLM 生成代码后，定制 linter、JIT 编译器和 OpInfo harness 自动反馈语法、编译和语义错误，循环修复直到覆盖不同 dtype、shape 与参数组合。实验最终生成 481 个 ATen operator 及 wrapper，并通过两万余项 OpInfo 测试，强调新芯片后端的覆盖率而非少数热门 kernel 的极限速度。
  - 相较只优化少数热门 kernel，核心创新是让 Agent 以测试驱动方式追求整个 ATen backend 的正确性覆盖。
  - Agent for Systems—ASIC 算子生成、测试驱动 Agent、ATen 后端

- [MoEBlaze: Breaking the Memory Wall for Efficient MoE Training on Modern GPUs](https://proceedings.mlsys.org/paper_files/paper/2026/hash/9032e5c9ec394ce768a2fa9bdc56af6c-Abstract-Conference.html)
  - Meta；Jiyuan Zhang、Yining Liu、Siqi Yan 等
  - MoEBlaze 是针对 MoE 训练内存墙的端到端框架，重点消除 token dispatch 产生的大量路由 buffer 和物化激活。它重新设计 dispatch 数据结构与训练数据流，并把专用 kernel、激活 checkpoint 联合起来，使节省的内存可以直接换成更大 batch 或序列。相对现有 MoE framework，端到端训练最高加速超过四倍、显存节省超过 50%。
  - 相较局部 kernel 优化，核心创新是从 token dispatch 数据结构到 activation checkpoint 全链条消除 MoE 中间物化。
  - MoE 训练显存、Token Dispatch、激活物化消除

- [Blueprint, Bootstrap, and Bridge: A Security Look at NVIDIA GPU Confidential Computing](https://proceedings.mlsys.org/paper_files/paper/2026/hash/906419cd502575b617cc489a1a696a67-Abstract-Conference.html)
  - IBM Research；Zhongshu Gu、Enriquillo Valdez、Salman Ahmed 等
  - 这是一项对 NVIDIA GPU Confidential Computing 的系统安全剖析，而不是提出新的 TEE。作者依据固件、驱动、专利和实验重建 FSP/GSP/SEC2 等安全引擎及启动信任链，再对 CPU—GPU 间不同传输路径注入和观测数据，检查其机密性与完整性是否符合官方威胁模型。研究覆盖 blueprint、bootstrap 和 trusted CPU-GPU bridge 三层，并将发现负责任披露给 NVIDIA PSIRT。
  - 相较依赖厂商高层白皮书，核心创新是系统重建专有 GPU-CC 信任链并用黑盒/定向实验验证桥接路径。
  - GPU Confidential Computing、TEE 信任链、安全逆向分析

<a id="matrix"></a>

- [Matrix: Peer-to-Peer Multi-Agent Synthetic Data Generation Framework](https://proceedings.mlsys.org/paper_files/paper/2026/hash/9069a8976ff06f6443e7f4172990a580-Abstract-Conference.html)
  - Meta FAIR；Dong Wang、Yang Li、Ansong Ni 等
  - Matrix 是运行海量合成数据 Agent 工作流的去中心化执行框架，用户定义 Agent 和消息流，系统负责并发、背压、重试以及 LLM/容器服务调度。控制流和数据流都被序列化为 Ray 分布式队列中的点对点消息，每个样本可独立推进，因此不会受中央 orchestrator 吞吐限制。在对话协作、网页推理和客服工具轨迹生成中，Matrix 支持数万并发 workflow，并在相同硬件下提高 2–15 倍吞吐而不降低数据质量。
  - 相较中央 orchestrator 调度每个 Agent 步骤，核心创新是把控制与数据都变成点对点队列消息，让每条 workflow 独立推进。
  - Agent Infra—多 Agent 运行时、去中心化队列、合成数据

- [NEST: Network- and Memory-Aware Device Placement for Distributed Deep Learning](https://proceedings.mlsys.org/paper_files/paper/2026/hash/949c07bf8756d51642c40b541c7306a8-Abstract-Conference.html)
  - Georgia Institute of Technology；Irene Wang、Vishnu Varma Venkata、Arvind Krishnamurthy 等
  - NEST 是分布式训练的自动设备放置与并行规划器，输入带算子代价的模型图、每张设备显存和真实网络拓扑，输出可执行的混合并行方案。结构化动态规划同时组合层内 tensor/expert/context 并行与层间 pipeline/data/ZeRO，而不是先忽略内存搜索、最后再被动切碎模型。跨不同硬件和网络拓扑，NEST 最高提高 2.43 倍吞吐，同时减少为了事后满足显存限制而增加的无效通信。
  - 相较先搜索并行再事后修补 OOM，核心创新是把网络时延、每设备显存和混合并行可行性放进同一动态规划。
  - 分布式训练规划、拓扑感知放置、显存约束搜索

- [FlexiCache: Leveraging Temporal Stability of Attention Heads for Efficient KV Cache Management](https://proceedings.mlsys.org/paper_files/paper/2026/hash/94bcb01789fccf15afe2764d8fe0f40e-Abstract-Conference.html)
  - University of California, Irvine；Nazmul Takbir、HamidReza Alikhani Koshkak、Nikil Dutt 等
  - FlexiCache 是利用注意力 head 重要性在时间上较稳定这一现象的分层 KV Cache 系统。它持续识别需要完整保留的 head 与 token，把较不关键内容下沉或压缩，并在长生成中复用稳定决策，从而避免每一步重新打分造成的计算开销和精度波动。在 vLLM 上，长上下文显存最高减少 70%，offline 吞吐提高 1.38–1.55 倍，online token latency 改善 1.6–2.1 倍。
  - 相较每步重新选重要 token/head，核心创新是利用 head 重要性的时间稳定性进行分层缓存和低开销长期决策。
  - 长上下文 KV Cache、Head 时间稳定性、分层缓存

- [G-HEMP: FAST MULTI-GPU PRIVATE INFERENCE FOR LARGE-SCALE GCNS WITH HOMOMORPHIC ENCRYPTION](https://proceedings.mlsys.org/paper_files/paper/2026/hash/96894468eb44631a32d7ebd56f9892c7-Abstract-Conference.html)
  - North Carolina State University；Ran Ran、Zhaoting Gong、Zhaowei Li 等
  - G-HEMP 是在密文上执行大规模 GCN 推理的多 GPU 同态加密系统，云端得到加密图和特征，只返回可由数据拥有者解密的预测。块对角 packing 消除加密邻接矩阵的重复副本，多 GPU partition 再按密文算子和内存占用分工，从而同时减少 HE 运算次数与单卡峰值显存。四 GPU 配置使单卡峰值内存约减半并把 latency 最高改善 3.88 倍，相比现有 HE 多设备切分仍最高快 3.13 倍。
  - 相较 CPU 或按密文 limb 平分，核心创新是针对 GCN 邻接结构设计块对角密文 packing，再联合多 GPU 内存切分。
  - 隐私 GCN 推理、同态加密、多 GPU 密文计算

- [When Machine Learning Isn’t Sure: Building Resilient ML-Based Computer Systems by Embracing Uncertainty](https://proceedings.mlsys.org/paper_files/paper/2026/hash/96aca14d6c4dcd3adf54bc2c5ad7f138-Abstract-Conference.html)
  - MIT；Varun Gohil、Nevena Stojkovic、Noman Bashir 等
  - 这项工作为使用 ML 做系统决策的组件增加运行时可信度门控，而不是试图训练一个永不出错的预测器。模型输出决策时同时给出不确定性，超过阈值就拒绝该决策并切换到规则或保守算法；论文在服务器配置、集群管理和存储 I/O 准入中比较不同估计器与回退代价。三个案例表明最合适的不确定性估计器与回退路径取决于任务 latency 和资源成本，不能使用统一置信度阈值。
  - 相较盲信 ML 控制器或只提高 OOD 精度，核心创新是把不确定性拒绝与具体系统回退成本联合设计。
  - ML for Systems 可靠性、不确定性门控、OOD 回退

- [Shannonic: Efficient Entropy-Optimal Compression for ML Workloads](https://proceedings.mlsys.org/paper_files/paper/2026/hash/96f39c8de84678cb2a908cd52bfd7819-Abstract-Conference.html)
  - University of Toronto；Kareem Ibrahim、Mohammadjavad Maheronnaghsh、Andreas Moshovos
  - Shannonic 是针对量化权重和激活张量的无损熵编码器，目标是在接近理论压缩率的同时避免大概率表和低吞吐解码。它离线把数值空间划成适合硬件处理的区间，并用极小状态描述编码分布，因此运行时只需约 530 B 状态即可达到距 Shannon 极限 1% 内的效率。在多种 8-bit 量化模型张量上，codec 只使用 530 B 状态，编码效率距离 Shannon 极限不足 1%。
  - 相较高状态概率表或吞吐不足的通用 codec，核心创新是在极小状态下逼近熵极限并适配 ML 张量。
  - ML 张量无损压缩、熵编码、极小 Codec 状态

- [Optimizing Deployment Configurations for LLM Inference](https://proceedings.mlsys.org/paper_files/paper/2026/hash/97dc07f1253ab33ee514f395a82fa7cc-Abstract-Conference.html)
  - Meta；Sung Min Cho、Jaewon Lee、Chunqiang Tang 等
  - 这是一套 Meta 用于 Llama 生产推理部署的配置搜索方法和经验总结，不是新的推理算法。系统枚举并测量硬件型号、tensor/pipeline/expert/context 并行、batching 与 prefill-decode 解耦等数百万组合，筛出满足延迟 SLO 时吞吐最大的方案，并总结不同 phase 与 MoE 架构的最优配置为何不同。系统服务接近十亿月活用户；分析覆盖 H100、H200、MI300X 以及 TP/PP/EP/CP/DP 和 continuous batching、P/D disaggregation。
  - 相较只优化 router、kernel 或某一种 GPU，核心贡献是生产规模联合搜索模型架构、phase、并行与硬件的完整 deployment space。
  - 生产 LLM 部署搜索、异构 GPU、并行配置

<a id="flashagents"></a>

- [FlashAgents: Accelerating Multi-Agent LLM Systems via Streaming Prefill Overlap](https://proceedings.mlsys.org/paper_files/paper/2026/hash/9a6f6e0d6781d1cb8689192408946d73-Abstract-Conference.html)
  - Microsoft；Taosong Fang、Zhen Zheng、Zhengzhao Ma 等
  - FlashAgents 是多 Agent LLM 工作流的执行层，专门缩短 Agent A 输出完成后 Agent B 才开始 prefill 的串行等待。它逐 token 把上游输出流给下游，并对不断增长的前缀做增量 prefill，同时复用共享前缀，使 Agent 间通信、decode 与 prefill 形成流水。SGLang 实现对真实 workflow 最多降低 40% 端到端延迟，在受控双 Agent 场景中最高加速 3.5 倍。
  - 相较 Agent 完整输出后再启动下游，核心创新是 token 级跨 Agent streaming 与增量 prefill。
  - Agent Infra—多 Agent 流水、Token Streaming、增量 Prefill

- [SHIP: SRAM-Based Huge Inference Pipelines for Fast LLM Serving](https://proceedings.mlsys.org/paper_files/paper/2026/hash/9c20f16b05f5e5e70fa07e2a4364b80e-Abstract-Conference.html)
  - NVIDIA；Andrew Bitar、Aravind Vellora Vayalapra、Baorui Zhou 等
  - SHIP 是 Groq 公有云使用的 SRAM 型大规模 LLM 推理硬件—系统设计，模型被展开为跨数千芯片的长流水线，而不是在单张 GPU 的 HBM 中反复读取权重。同步低直径互连负责在芯片间推进 token，调度与内存布局则适应不同上下文和 prefill/decode 比例，以 SRAM 带宽换取低单 token 延迟。该架构已在 Groq 公有云每日服务数千亿 token，目标是在不同 context 和流量比例下同时维持低 TTFT、TPOT 与吞吐。
  - 相较 HBM 上批量复用权重，核心创新是以 SRAM 和跨数千芯片的确定性大流水线直接消除 decode 带宽墙。
  - SRAM LLM 推理、分布式加速器流水、Groq Serving

- [FP8-Flow-MoE: A Casting-Free FP8 Recipe without Double Quantization Error](https://proceedings.mlsys.org/paper_files/paper/2026/hash/9cb295d4dce6db99f01e0dd512e46ba0-Abstract-Conference.html)
  - ZhejiangLab,Hangzhou,China；Fengjuan Wang、Zhiyi Su、Xingzhu Hu 等
  - FP8-Flow-MoE 是 671B MoE 训练的全 FP8 数据流配方，目标是在减少 BF16↔FP8 cast 时避免不同量化维度叠加 scale 导致数值失真。Scaling-aware transpose 在转置时重排并校正 scale，融合算子让张量沿前后算子保持一致量化语义，使显式转换由 12 次降到 2 次。671B MoE 上，相对 BF16 和朴素 FP8，吞吐最高提高 21%、每 GPU 降低 16.5 GB 内存，并保持稳定收敛。
  - 相较朴素全 FP8 因 scale 维度不一致而失稳，核心创新是定义量化一致的数据流和 scaling-aware transpose，避免双重量化误差。
  - FP8 MoE 训练、无 Cast 数据流、量化一致性

- [Hippocampus: An Efficient and Scalable Memory Module for Agentic AI](https://proceedings.mlsys.org/paper_files/paper/2026/hash/a1d04870cf83a0f29819d66f1dfdbfcb-Abstract-Conference.html)
  - University of Texas at Dallas；Yi Li、Lianjie Cao、Faraz Ahmed 等
  - Hippocampus 是可插入 Agent 的长期记忆存储与检索模块，保存会话内容并按语义返回原始 token，而不是再让 LLM 摘要所有历史。它用紧凑二进制签名近似搜索相关记忆，用无损 token-ID 流精确重建命中内容，从而同时降低向量索引、文本存储和重新分词开销。LoCoMo 与 LongMemEval 上，检索最高比基线快 31.5 倍、每查询 token footprint 降低 1.1–14.5 倍且任务精度有竞争力。
  - 相较只存文本+向量或让 LLM 压缩记忆，核心创新是二进制语义签名检索与 token-ID 无损内容存储的双表示。
  - Agent Infra—长期记忆存储、语义签名、Token 无损重建

- [MixLLM: LLM Quantization with Global Mixed-precision between Output-features and Highly-efficient System Design](https://proceedings.mlsys.org/paper_files/paper/2026/hash/a66caa1703fe34705a4368c3014c1966-Abstract-Conference.html)
  - Microsoft；Zhen Zheng、Xiaonan Song、Chuanjie Liu
  - MixLLM 是一种按输出特征列分配位宽的权重量化方法，不是为每层统一选择 INT4/INT8。它先估计不同 output feature 对误差的敏感度，在全模型预算下让少量重要列使用更高精度，并配套混合精度 kernel，使多出来约 10% 的 bit 真正转化为更低困惑度而非执行碎片。在 Llama 3.1 70B 上，只增加约 10% bit 即把 perplexity 增量从约 0.5 降到 0.2 内，并在多个模型上减少 MMLU-Pro 损失。
  - 相较层级 mixed precision，核心创新是在 output-feature 维度做全局 bit 分配并提供可高效执行的 kernel。
  - LLM 混合精度量化、Output-Feature 位宽分配、Quantized Kernel

- [FlashAttention-4: Algorithm and Kernel Pipelining Co-Design for Asymmetric Hardware Scaling](https://proceedings.mlsys.org/paper_files/paper/2026/hash/ae8b0b5838ba510daff1198474e7b984-Abstract-Conference.html)
  - Princeton University；Ted Zadouri、Markus Hoehnerbach、Jay Shah 等
  - FlashAttention-4 是针对 NVIDIA Blackwell 不同计算单元扩展速度不一致而重新设计的精确注意力 kernel。它把异步 MMA、softmax 指数与重标定、tensor memory 搬运组织成多级流水，并利用 2-CTA MMA 减少共享内存和原子操作，重点解决 matmul 已很快后暴露出的非 matmul 瓶颈。B200 BF16 上最高比 cuDNN 9.13 快 1.3 倍、比 Triton 快 2.7 倍，达到 1613 TFLOP/s 和约 71% 利用率。
  - 相较沿用 Hopper pipeline，核心创新是围绕 Blackwell 异步 MMA 与非矩阵单元失衡重新协同算法和 kernel stages。
  - FlashAttention、Blackwell Kernel、异步 MMA 流水

- [ContextPilot: Fast Long-Context Inference via Context Reuse](https://proceedings.mlsys.org/paper_files/paper/2026/hash/b0131b6ee02a00b03fc3320176fec8f5-Abstract-Conference.html)
  - University of Edinburgh；Yinsicheng Jiang、Yeqi Huang、Liang Cheng 等
  - ContextPilot 是位于 RAG、Agent memory 与推理引擎之间的上下文复用层，识别不同用户、轮次和工具调用返回内容中重复但次序不同的 context block。它建立 block 索引并进行对齐、去重，再添加短注释保留原位置语义，使这些块可以复用已有 KV，而不因重排上下文损害推理质量。长上下文评测中 prefill latency 最高降低三倍，同时保持甚至改善 reasoning quality，说明复用不是以删除上下文换速度。
  - 相较只能复用相同前缀，核心创新是索引、对齐和注释任意重复 context block，在不改变语义时安全重排复用。
  - Agent Infra—上下文复用、非前缀 KV Cache、RAG/多 Agent

- [ProToken: Token-Level Attribution for Federated Large Language Models](https://proceedings.mlsys.org/paper_files/paper/2026/hash/b8bf2c0dd0b48511889b7d3b2c5fc8f5-Abstract-Conference.html)
  - Virginia Tech；Waris Gill、Ahmad Humayun、Ali Anwar 等
  - ProToken 是联邦微调 LLM 的生成溯源方法：给定最终生成文本，它为每个 token 判断主要由哪些客户端的本地更新促成。方法在不公开客户端数据或模型更新的条件下计算贡献信号，并沿自回归生成过程累计归因，用于调试恶意客户端、奖励分配和责任验证。16 组配置覆盖四类 LLM 与医疗、金融、数学、代码领域，平均 token attribution 准确率为 98.62%。
  - 相较只做客户端级训练贡献估计，核心创新是保持隐私的自回归 token 级来源定位。
  - 联邦 LLM 可追溯性、Token 级客户端归因、隐私审计

- [PLA-Serve: A Prefill-Length-Aware LLM Serving System](https://proceedings.mlsys.org/paper_files/paper/2026/hash/bbb7506579431a85861a05fff048d3e1-Abstract-Conference.html)
  - Mohamed bin Zayed University of Artificial Intelligence；JIANSHU SHE、Zonghang li、Hongchao Du 等
  - PLA-Serve 是按 prompt 长度拆分 prefill 资源与队列的 LLM 服务调度器。长多轮请求被送入独立路径，短请求则按相近长度组成 CUDA Graph batch；双队列既可在一台 prefill 实例上时间复用，也可跨实例空间隔离，避免统一 batching 中长请求拖住短请求。真实多轮负载中 prefill latency 降低 30% 以上；多实例 SLO violation 降低 28%，高并发 Qwen2.5-32B 吞吐提高 35%。
  - 相较所有 prompt 共用一条 prefill queue，核心创新是按长度拆分长短路径并结合 temporal/spatial 双形态 disaggregation。
  - Prefill 长度感知调度、P/D 解耦、双队列 Batching

- [ApproxMLIR : Accuracy-Aware Compiler for Compound ML System](https://proceedings.mlsys.org/paper_files/paper/2026/hash/bbd3e0e9913824bbc46e7e87b11461ae-Abstract-Conference.html)
  - University of Illinois Urbana-Champaign；Hao Ren、Yi Mu、Sasa Misailovic
  - ApproxMLIR 是复合 ML 系统的准确率感知编译器，输入包含多个模型/算法组件的流水线及允许的近似算子，输出端到端准确率和性能折中方案。它在 MLIR 中统一表示量化、跳过计算等近似选择，并跨组件搜索组合，避免各模块独立优化后误差叠加失控。评测表明它能表达多种常用近似，并发现比固定策略更优的 accuracy-performance 点，而非只对单模型量化有效。
  - 相较每个组件独立近似，核心创新是在统一 IR 中搜索复合 pipeline 的端到端准确率约束。
  - 近似计算编译器、复合 ML Pipeline、准确率约束搜索

- [DynaFlow: Transparent and Flexible Intra-Device Parallelism via Programmable Operator Scheduling](https://proceedings.mlsys.org/paper_files/paper/2026/hash/bbd7d8bd780fcf7143add2317ba04638-Abstract-Conference.html)
  - Shanghai Jiao Tong University；Yi Pan、Yile Gu、Jinbin Luo 等
  - DynaFlow 是把单 GPU 内多个算子并行化的可编程运行时，模型作者仍按普通顺序代码描述网络，执行者另外定义物理 schedule。系统在运行时依据依赖关系发射、暂停和交错算子，因而无需把模型重写成固定并发图，也能针对不同 shape 调整并行策略。其接口允许相同模型在不同 shape、设备状态下更换 operator schedule，核心是可编程执行而非预先固定的手工 fusion。
  - 相较模型代码同时固化执行顺序，核心创新是逻辑定义与物理 operator schedule 解耦且可在运行时替换。
  - 设备内算子并行、逻辑-物理调度解耦、可编程 Runtime

- [Flashlight: PyTorch Compiler Extensions to Accelerate Attention Variants](https://proceedings.mlsys.org/paper_files/paper/2026/hash/bc52716d13d2d72ea0f335667d86c0f8-Abstract-Conference.html)
  - University of Texas at Austin；Bozhi You、Irene Wang、Zelal Su Mustafaoglu 等
  - Flashlight 是 PyTorch 编译器中的注意力程序扩展，输入用户以普通 PyTorch 写出的任意 attention 变体，自动输出融合的 FlashAttention 风格 GPU kernel。它从程序语义推导 tile、融合和数据流，而非匹配预制模板，因此新 mask、bias 或归一化形式不必等待人工手写专用 kernel。生成结果对多类注意力程序达到与 FlexAttention 相当或更高的速度，同时保留原生 PyTorch 的可组合性。
  - 相较为每种 attention 写模板或手工 kernel，核心创新是从任意 PyTorch attention 程序自动生成融合实现。
  - Attention Kernel 自动生成、PyTorch 编译器、算子融合

- [HipKittens: Fast and Furious AMD Kernels](https://proceedings.mlsys.org/paper_files/paper/2026/hash/bc75fa9843a7905bbed9d83895a88f7f-Abstract-Conference.html)
  - Stanford University；William Hu、Drew Wadsworth、Sean Siddens 等
  - HipKittens 是 AMD GPU 上的 tile 级 C++ 内核编程框架，试图用少量矩阵、内存和异步原语替代难维护的裸汇编。它保留开发者对 tile 数据流和 worker 协作的显式控制，同时把 CDNA3/4 的寄存器、指令和搬运细节封装起来，使同一抽象可实现 GEMM、attention 等多类算子。CDNA3/4 上的 GEMM 与 attention 能竞争手写汇编并稳定超过 compiler baseline，部分内存受限 kernel 快 1.2–2.4 倍。
  - 相较 NVIDIA 专用 tile DSL 或 AMD 裸汇编，核心创新是验证并实现跨 AMD 架构的可移植 tile programming layer。
  - AMD GPU Kernel DSL、Tile 编程、CDNA3/4

- [Optimizing PyTorch Inference with LLM-Based Multi-Agent Systems](https://proceedings.mlsys.org/paper_files/paper/2026/hash/bd49b53516ce9ea248fb73522d71a508-Abstract-Conference.html)
  - Northwestern University；Kirill Nagaitsev、Luka Grbcic、Samuel Williams 等
  - 这项工作研究的是“怎样组织多个 LLM Agent 去自动优化 PyTorch 程序”，并建立统一框架比较不同 Agent 分工、反馈和搜索策略，而不是提出一个单一 kernel 算法。Agent 读取原 PyTorch 实现，生成候选代码，经编译和 KernelBench 性能反馈迭代；最佳组合相对 Eager 平均加速 2.88 倍。评测覆盖不同多 Agent 组织方案和 KernelBench 中多类 PyTorch 模型结构，最佳实现还比 torch.compile 平均快 1.85 倍。
  - 相较单 Agent prompt 技巧，核心创新是系统比较多 Agent 分工与编译执行反馈如何共同优化 PyTorch。
  - Agent for Systems—PyTorch 推理优化、多 Agent 代码搜索、KernelBench

- [Zorse: Optimizing LLM Training Efficiency on Heterogeneous GPU Clusters](https://proceedings.mlsys.org/paper_files/paper/2026/hash/bfa6dd59c1d7f7c785909f9ff7cffe67-Abstract-Conference.html)
  - University of Waterloo；Runsheng Guo、Utkarsh Anand、Khuzaima Daudjee 等
  - Zorse 是异构 GPU 集群的大模型训练配置规划器，输入各型号 GPU 的算力、显存、互连和模型结构，输出设备分组、并行维度及 batch 等训练方案。它用性能模型搜索大量异构组合，让快慢 GPU 承担与能力匹配的分片，避免按最慢设备同步或只使用同型号资源。在代表性异构训练场景中，Zorse 比现有 planner 最高提高三倍吞吐，目标是利用本来因成本或供应限制而混用的 GPU。
  - 相较同构 planner 或按最慢 GPU 对齐，核心创新是自动搜索异构设备能力匹配的训练配置。
  - 异构 GPU LLM 训练、自动配置规划、设备能力匹配

- [CAGE: Curvature-Aware Gradient Estimation For Accurate Quantization-Aware Training](https://proceedings.mlsys.org/paper_files/paper/2026/hash/c0f1eed3f3ca4b2e19ab639a8426270b-Abstract-Conference.html)
  - Institute of Science and Technology Austria；Soroush Tabesh、Mher Safaryan、Andrei Panferov 等
  - CAGE 是低比特量化感知训练中的梯度估计方法，替换的是反向传播如何穿过不可导量化操作，而不是设计新的量化格式。它在常用 straight-through estimator 上加入由局部损失曲率推导的修正项，抵消一次量化更新预计造成的损失上升，使 3-bit 训练接近既有 4-bit 精度。微调时它将既有最佳方法的压缩精度损失减半；从头训练 Llama 时，W3A3 达到此前 W4A4 的精度。
  - 相较把量化梯度直接当恒等映射，核心创新是由损失曲率修正 STE 的更新方向。
  - 量化感知训练、曲率梯度估计、低比特训练

- [From Tokens to Layers: Redefining Stall-Free Scheduling for MoE Serving with Layered Prefill](https://proceedings.mlsys.org/paper_files/paper/2026/hash/c0f460c6d63599ea870ba9db63dc96a9-Abstract-Conference.html)
  - Seoul National University；Gunjun Lee、Jiwon Kim、Jaiyoung Park 等
  - Layered Prefill 是为 MoE 服务设计的调度范式，把一个请求的 prefill 拆成若干 Transformer 层组，与正在 decode 的请求交错执行。由于调度器能在层边界控制专家权重加载和通信，它避免大 prefill chunk 长时间占用专家与链路，在不打断 token 连续输出的情况下联合改善 TTFT 和 TBT。评测显示 layered prefill 持续改善 TTFT-TBT Pareto frontier，同时降低专家加载网络流量和能耗。
  - 相较 token/chunk 级 prefill，核心创新是以层组为可抢占单元协调 MoE expert load 与 decode deadline。
  - MoE Serving 调度、Layered Prefill、TTFT/TBT 协同

- [AgenticCache: Cache-Driven Asynchronous Planning for Embodied AI Agents](https://proceedings.mlsys.org/paper_files/paper/2026/hash/c66a9db149261435664284a20b6f1d42-Abstract-Conference.html)
  - Seoul National University；Hojoon Kim、Yuheng Wu、Thierry Tambe
  - AgenticCache 是具身 Agent 的计划复用框架，缓存的是“在相似状态和目标下可执行的多步计划”，而不是普通 LLM KV Cache。运行时先检索并执行缓存计划，同时异步让 LLM 检查或补全；只有环境偏离时才重新规划，因此减少每个动作前的同步 LLM 调用。四个 embodied multi-agent benchmark、三种模型上，成功率平均提高 22%，simulation latency 降低 65%，token 消耗减少 50%。
  - 相较每一步同步重新规划，核心创新是缓存可执行计划并在执行时异步验证，且能提高成功率而非只省 token。
  - Agent System—规划复用、具身 Agent、异步计划校验

- [BLASST: Dynamic BLocked Attention Sparsity via Softmax Thresholding](https://proceedings.mlsys.org/paper_files/paper/2026/hash/c6ee784cbe46d854843e4c883a3321ef-Abstract-Conference.html)
  - NVIDIA；Jiayi Yuan、Cameron Shinn、Kai Xu 等
  - BLASST 是训练免、动态的块稀疏精确近似 attention，可直接替换 MHA、GQA、MQA 或 MLA 的 prefill/decode kernel。它复用 online softmax 的行最大值，用一个标量阈值判断当前 QK block 的贡献上界，若不可能显著影响结果便跳过 softmax、V 读取和矩阵乘。保持 benchmark accuracy 时，prefill 在 71.9% 稀疏度下加速 1.52 倍，decode 在 73.2% 稀疏度下加速 1.48 倍。
  - 相较需要训练、预计算 mask 或只支持单一 attention 的稀疏方法，核心创新是复用 online softmax 统计用单阈值实时判块。
  - 动态块稀疏 Attention、Online Softmax 判块、训练免加速

- [Locality-Aware Beam Scheduling for Efficient Test-Time Compute with a Consumer-grade GPU](https://proceedings.mlsys.org/paper_files/paper/2026/hash/c74b624843218d9b6713fcf299d6d5e4-Abstract-Conference.html)
  - National Taiwan University；Hsing-Ti Wang、Hung-Tso Shiao、Chia-Lin Yang
  - Locality-Aware Beam Scheduling 是消费级 GPU 上 test-time beam search 的执行策略，关注不同 beam 在连续步骤和模型层间重复访问相同 KV 页的现象。调度器把共享或相邻状态的 beam 放在一起推进，使已搬到 VRAM 的 KV 可被多次使用，从而减少层式卸载反复传输同一缓存。OPT、Llama 和 Qwen 模型上，KV 传输量减少 95% 以上，端到端相对 layer-wise offload 提高约 3.4–9.7 倍。
  - 相较按层顺序卸载 beam，核心创新是按 beam 间 KV 共享和访问局部性重排执行以复用一次传输。
  - Test-Time Compute、Beam Search、KV Cache 局部性

- [PLayer-FL: A Principled Approach to Personalized Layer-wise Cross-Silo Federated Learning](https://proceedings.mlsys.org/paper_files/paper/2026/hash/ca0aa7883e7dff43b6d1e44bb8c75127-Abstract-Conference.html)
  - University of Cambridge；Ahmed Elhussein、Florent Pollet、Gamze Gürsoy
  - PLayer-FL 是 cross-silo 联邦学习中的个性化分层聚合方法，决定哪些早期层应跨机构共享、哪些后期层留在本地。它用层表示的可迁移性建立原则化选择和聚合规则，替代针对每种网络手调共享深度，并避免弱相关客户端在全局平均后反而退化。跨多任务和客户端分布，方法保持竞争性精度，同时让收益分配更均衡并减少个别客户端相对本地训练的退化。
  - 相较凭经验固定共享前几层，核心创新是原则化决定层级 federation 并关注客户端收益公平性。
  - 个性化联邦学习、层级聚合、客户端公平性

- [Beat the long tail: Distribution-Aware Speculative Decoding for RL Training](https://proceedings.mlsys.org/paper_files/paper/2026/hash/cbc4ab80cd77aa0eb87da062fbcddb46-Abstract-Conference.html)
  - University of Illinois Urbana-Champaign；ZELEI SHAO、Vikranth Srivatsa、Sanjana Srivastava 等
  - DAS 是 RL rollout 阶段的分布感知推测解码器，利用同一 prompt 在不同训练 epoch 中会出现相似生成轨迹这一历史。它把近期 rollout 增量写入 suffix tree 作为非参数 drafter，并预测长尾轨迹、为其分配更激进的草稿预算，从而重点缩短真正决定整批完成时间的少数长样本。数学和代码 RL 任务上，DAS 把 rollout 时间最多减半，并保持完全相同的输出与训练曲线。
  - 相较训练独立 neural drafter，核心创新是复用历史 rollout 的 suffix tree 并把推测预算倾斜给长尾样本。
  - RL 后训练 Rollout、分布感知推测解码、历史轨迹 Drafter

- [VeriMoA: A Mixture-of-Agents Framework for Spec-to-HDL Generation](https://proceedings.mlsys.org/paper_files/paper/2026/hash/cc8c6b9d89f7a898a29f58869b238e46-Abstract-Conference.html)
  - University of Southern California；Heng Ping、Arijit Bhattacharjee、Peiyu Zhang 等
  - VeriMoA 是从自然语言规格生成 Verilog 的训练免 Mixture-of-Agents 系统。多个 Agent 的所有中间 HDL 都进入质量缓存统一验证和排序，同时另一些路径先把规格转换为 LLM 更熟悉的 C++ 或 Python 再译成 HDL，以减少错误在层间传播并扩大可探索的实现空间。VerilogEval 2.0 与 RTLLM 2.0 上，Pass@1 提升 15%–30%，并使较小模型在无需 fine-tuning 时接近较大模型。
  - 相较串行 Agent 输出或只从规格直译 HDL，核心创新是全程质量缓存加多语言中间表示的多路径搜索。
  - Agent for Systems—Spec-to-HDL、Mixture-of-Agents、质量缓存

- [AXLearn: Modular, Hardware-Agnostic Large Model Training](https://proceedings.mlsys.org/paper_files/paper/2026/hash/d1f9e4a9f109b6e8b75ed362736f22ec-Abstract-Conference.html)
  - Apple、Duke University；Mark Lee、Chang Lan、Tom Gunter 等
  - AXLearn 是 Apple 的模块化、硬件无关大模型训练框架，模型、层、优化器和并行组件通过严格封装的接口组合，而不是依靠层层继承修改内部状态。相同训练定义可落到 GPU、TPU 和 Trainium；组件数量增加时接口复杂度保持稳定，使新 RoPE 等能力能以少量代码跨大量模块接入。论文还提出量化模块化复杂度的框架；在真实 Apple 开发中，RoPE 一类能力跨数百模块接入仅需约 10 行代码。
  - 相较依赖 subtyping 导致模块耦合，核心创新是严格封装使系统功能数量增长时集成复杂度近似不变。
  - 大模型训练框架、严格模块封装、硬件无关执行

- [Beyond the Buzz: A Pragmatic Take on Inference Disaggregation](https://proceedings.mlsys.org/paper_files/paper/2026/hash/d49cee5f3a79d97d719df255689d83d7-Abstract-Conference.html)
  - NVIDIA；Tiyasa Mitra、Ritika Borkar、Nidhi Bhatia 等
  - 这是一项对大规模 prefill-decode disaggregation 的设计空间研究，并以 NVIDIA Dynamo 的部署能力验证结论，而不是声称解耦总是更快。作者测量数十万种工作负载、GPU 与资源配比，发现只有 prefill 占比较高或模型较大时收益稳定，且必须动态匹配两阶段速率并弹性扩容。结论来自不同硬件和 workload 的数十万设计点：prefill-heavy 与大模型更适合解耦，其他负载可能被协调开销抵消收益。
  - 相较把 P/D disaggregation 视为普遍最优，核心创新是大规模刻画其适用边界并识别动态 rate matching 的必要性。
  - P/D Disaggregation、LLM Serving 设计空间、动态 Rate Matching

- [HexiScale: Facilitating Large Language Model Training over Heterogeneous Hardware](https://proceedings.mlsys.org/paper_files/paper/2026/hash/d5a655b8b373737b4f2aea8f78e5e754-Abstract-Conference.html)
  - Hong Kong University of Science and Technology；Ran Yan、YOUHE JIANG、Xiaonan Nie 等
  - HexiScale 是异构硬件上的 LLM 训练系统，允许数据、流水线和张量并行中的分片大小不对称，使不同速度和显存的 GPU 不必承担等量工作。系统根据每类设备性能联合划分层、张量与 microbatch，并生成匹配的通信计划，把异构集群的总 FLOPs 转化为接近同构集群的吞吐。7B–30B LLM 上，在总理论 FLOPs 相当时接近同构基线，相对现有异构方案提高 1.5–2.4 倍吞吐。
  - 相较只在 pipeline 一个维度非对称，核心创新是联合支持 DP、PP、TP 的异构不等量切分。
  - 异构硬件 LLM 训练、非对称 3D 并行、自动分片

- [veScale-FSDP: Flexible and High-Performance FSDP at Scale](https://proceedings.mlsys.org/paper_files/paper/2026/hash/d5cd70b708f726737e2ebace18c3f71b-Abstract-Conference.html)
  - ByteDance；Zezhou Wang、Youjie Li、Zhiqi Lin 等
  - veScale-FSDP 是支持不规则和块结构状态的全分片训练系统，目标是兼容 block-wise quantization、非逐元素 optimizer 等传统行/元素分片难以表达的计算。RaggedShard 允许分片边界不等长，结构感知 planner 则让通信布局直接匹配后续算子，从而实现零拷贝 collective。系统可扩展到数万 GPU，在不同模型上比现有 FSDP 提高 5%–66% 吞吐并降低 16%–30% 内存。
  - 相较规则矩形 FSDP shard，核心创新是 RaggedShard 与结构感知 planner 共同支持块算子并实现零拷贝通信。
  - FSDP、不规则分片、结构感知零拷贝通信

- [Cost-aware Duration Prediction for Software Upgrades in Datacenters](https://proceedings.mlsys.org/paper_files/paper/2026/hash/d84c0dd9b1bfeee361f3268dcaebf849-Abstract-Conference.html)
  - Purdue University；Yi Ding、Aijia Gao、Thibaud Ryden 等
  - Acela 是数据中心软件升级的工期预测与调度辅助框架，输入服务器状态、升级类型和历史执行记录，输出带业务成本权重的时长估计。它优化的不是单纯预测误差，而是错误估计对 SLO、窗口闲置和任务取消的代价，使 scheduler 能塞入更多可按时完成的升级。Meta 生产评测中，升级窗口利用率提高 1.25 倍，排入与完成的升级分别增加 33% 和 41%，取消率降低 2.4 倍。
  - 相较最小化平均预测误差，核心创新是按错误对升级窗口和 SLO 的真实代价训练时长预测器。
  - 数据中心升级调度、成本感知时长预测、SLO

- [GhostServe: A Lightweight Checkpointing System in the Shadow for Fault-Tolerant LLM Serving](https://proceedings.mlsys.org/paper_files/paper/2026/hash/d99e8e80a6c41e148db686918dd7eab3-Abstract-Conference.html)
  - University of Central Florida；Shakya Jayakody、Youpeng Zhao、Chinmay Dhanraj Nehate 等
  - GhostServe 是 LLM 服务的流式 KV Cache 检查点系统，保护长会话和 Agent 任务在 GPU 故障后继续生成。它不复制完整 KV，而是在后台对不断增长的缓存做纠删码、只把 parity shard 存入主机内存；故障时结合幸存 shard 重建丢失部分，避免从 prompt 全量重算。故障 trace 下，单 batch checkpoint latency 最高降低 2.7 倍、恢复 latency 降低 2.1 倍，并改善故障期间的 median response latency。
  - 相较全量状态复制或故障后重算，核心创新是对不断增长的 KV 做后台纠删码，只保存低成本 parity。
  - 状态化 LLM Serving 容错、KV 纠删码、长会话恢复

- [Learning from Less: Measuring the Effectiveness of RLVR in Low Data and Compute Regimes](https://proceedings.mlsys.org/paper_files/paper/2026/hash/da85790fb1cb4f11f431648455c561b5-Abstract-Conference.html)
  - Snorkel AI；Justin Bauer、Thomas Walshe、Derek Pham 等
  - 这是一项研究低数据、低算力条件下 RLVR 何时有效的经验工作，而不是新的 RL 训练系统。作者用可程序控制规模、难度和多样性的题目训练小语言模型，发现低难度经验可迁移到高难度，而混合难度数据在相同样本预算下最有效。结果显示低难度数据可向高难度泛化，但低预算下混合难度最有效，相对只训练简单任务最高提高五倍样本效率。
  - 相较在固定公共数据集上报告低数据结果，核心创新是用可控程序数据分离规模、难度与多样性的作用。
  - 低数据 RLVR、程序化数据、样本效率

- [db-SP: Accelerating Sparse Attention for Visual Generative Models with Dual-Balanced Sequence Parallelism](https://proceedings.mlsys.org/paper_files/paper/2026/hash/db988b089d8d97d0f159c15ed0be6a71-Abstract-Conference.html)
  - Tsinghua University；Siqi Chen、Ke Hong、Tianchen Zhao 等
  - db-SP 是视觉 Diffusion Transformer 块稀疏 attention 的序列并行算法。它先量化不同 head 的稀疏度和每个 head 内 dense block 分布，再同时沿 head 与 block 两级切分，并随去噪步和网络层动态改变并行度，从而让各 GPU 获得接近相等的实际非零计算。相对现有 sequence parallel，平均端到端加速 1.25 倍、attention 部分加速 1.40 倍。
  - 相较只沿 head 或 block 单维切分，核心创新是联合两维并随去噪阶段动态选择并行度。
  - 视觉 DiT 推理、块稀疏 Sequence Parallel、双维负载均衡

- [Charon: A Unified and Fine-Grained Simulator for Large-Scale LLM Training and Inference](https://proceedings.mlsys.org/paper_files/paper/2026/hash/dbc8ce0fdfcd55172d73fb05dbae07fc-Abstract-Conference.html)
  - University of Texas at Austin；Mengtian Yang、Zhekun Zhang、Mingheng Wu 等
  - Charon 是统一预测 LLM 训练和推理性能的离散事件模拟器，输入模型图、并行策略、系统优化与硬件拓扑，输出各阶段时间线、资源占用和端到端性能。它把算子、通信、内存和调度建模到足够细粒度，从而可在购买或占用大集群前筛选配置。跨模型和配置的总体预测误差低于 5.35%，大型 GPU 训练场景低于 3.74%。
  - 相较分别模拟训练或推理、只给层级平均值，核心创新是统一细粒度事件模型覆盖两类 workload 和系统优化。
  - LLM 性能模拟器、训练/推理统一建模、配置规划

- [ReSpec: Towards Optimizing Speculative Decoding in Reinforcement Learning Systems](https://proceedings.mlsys.org/paper_files/paper/2026/hash/dcb38c6ad7911842ab31081be9540b89-Abstract-Conference.html)
  - Nanyang Technological University；Qiaoling Chen、Zijun Liu、Peng Sun 等
  - ReSpec 是把推测解码适配到在线变化的 RL 训练过程的系统：随着 policy 更新，固定 drafter 的接受率会迅速失效。它根据实时接受率调整推测参数，用最新 policy 蒸馏更新 drafter，并按 rollout 奖励给蒸馏样本加权，使加速过程跟随策略分布变化而不破坏 reward 收敛。Qwen 3B–14B 上，系统最高加速 4.5 倍，并保持 reward convergence 与训练稳定性。
  - 相较固定 SD 参数和静态 drafter，核心创新是让配置、drafter 和样本权重随 RL policy 一起演化。
  - RL 训练推测解码、自适应 Drafter、Reward-Aware 更新

- [fabric-lib: RDMA Point-to-Point Communication for LLM Systems](https://proceedings.mlsys.org/paper_files/paper/2026/hash/dea9b4b6f55ae611c54065d6fc750755-Abstract-Conference.html)
  - Perplexity AI；Nandor Licker、Kevin Hu、Vladimir Zaytsev 等
  - fabric-lib 是面向 LLM 系统的 RDMA 点对点通信库，为推理解耦、MoE token 路由和异步 RL 提供比 collective 更灵活的语义。它在普通 NIC 上统一暴露 one-sided WRITEIMM 和用于完成通知的 IMMCOUNTER，并在库内处理传输乱序及一张 GPU 对多 NIC 的映射。接口不假定底层 transport 有序，并透明聚合单 GPU 的多 NIC，可作为不同 LLM system pattern 的共同通信层。
  - 相较依赖专用 NIC collective，核心创新是在普通多 NIC 上提供对 LLM 点对点模式统一的 one-sided 语义。
  - LLM 系统通信库、RDMA 点对点、多 NIC

- [Unleashing Scalable Context Parallelism for Foundation Models Pre-Training via FCP](https://proceedings.mlsys.org/paper_files/paper/2026/hash/e01c431bbb83153632c0dcfaf8ccda0a-Abstract-Conference.html)
  - ByteDance；Yilong Zhao、Xiaonan Nie、Kan Zhu 等
  - FCP 是 foundation model 预训练的 block 级 context parallelism，不再把每条变长序列作为不可分割单元分配给 GPU。任意序列都被切成定长 token block，调度器按实际 attention 工作量跨设备组合这些块，因此短长文档混合时仍能均衡计算并接近线性扩展。在最多 256 张 NVIDIA GPU 上接近线性扩展，attention MFU 提高 1.13–2.21 倍。
  - 相较按原始 sequence 分片，核心创新是固定 token block 打散长度差异再调度。
  - Foundation Model 预训练、Block Context Parallel、变长序列

- [Hawkeye: Reproducing GPU-Level Non-Determinism](https://proceedings.mlsys.org/paper_files/paper/2026/hash/e217c271a57c365a246b0ad39e668ba8-Abstract-Conference.html)
  - Pearl Research Labs；Erez Badash、Dan Boneh、Ilan Komargodski 等
  - Hawkeye 是精确复现 NVIDIA Tensor Core 数值行为的分析工具，输入一次 GPU 矩阵乘的操作数和硬件配置，能在 CPU 上生成逐位一致的结果。它通过精心构造的探针实验反推出不同架构、数据类型下的舍入方向、subnormal 处理和非结合累加顺序，为第三方审计 GPU 训练或推理提供确定性基础。测试覆盖 Ampere、Hopper、Lovelace 以及 FP16、BF16、FP8，所有矩阵乘均可在 CPU 上逐位复现。
  - 相较容忍 GPU 非确定性或只近似复现，核心创新是通过反向测量硬件算术规则实现 CPU 逐位重放。
  - 可验证 ML、GPU 数值确定性、CPU 精确重放

- [LEANN: A Low-Storage Overhead Vector Index](https://proceedings.mlsys.org/paper_files/paper/2026/hash/e27ea0cd50b798ff8942caf9203f0992-Abstract-Conference.html)
  - University of California, Berkeley；Yichuan Wang、Zhifei Li、Shu Liu 等
  - LEANN 是低存储向量检索索引，核心选择是只存原始文本和压缩后的近邻图，不长期保存每个文本块的高维 embedding。查询遍历到候选节点时才用模型重算所需 embedding，并通过图压缩和构建更新策略控制额外计算，从而把索引体积降到原数据约 5%。系统同时支持低存储构建和增量更新，使索引占用可降到原始数据约 5%，而非只压缩静态 benchmark。
  - 相较永久存储所有 embedding，核心创新是查询时重算表示并压缩图索引，以计算换数量级存储。
  - 低存储向量索引、Embedding 重计算、压缩近邻图

- [Kitty: Accurate and Efficient 2-bit KV Cache Quantization with Dynamic Channel-wise Precision Boost](https://proceedings.mlsys.org/paper_files/paper/2026/hash/e4d8d1b5120be349d3fff8878650cf45-Abstract-Conference.html)
  - Together AI；Haojun Xia、Xiaoxia wu、Jisen Li 等
  - Kitty 是 2-bit 为主、局部 4-bit 的混合精度 KV Cache 系统。算法先按敏感度找出少数 Key 通道并提升精度，系统再把混合位宽拆成统一 2-bit 页和轻量补充数据，配套页式布局与 Triton 解量化 kernel，使精度提升不会破坏 paged attention 的连续访存。七个任务、Qwen3 与 Llama3 上，KV 内存接近缩小八倍，batch 最多扩大八倍，吞吐提高 2.1–4.1 倍。
  - 相较全部 2-bit 或静态 mixed precision，核心创新是动态识别敏感 Key channel，并设计仍可页式高效执行的编码。
  - 2-bit KV Cache、动态通道混合精度、Paged Attention

- [DriftBench: Measuring and Predicting Infrastructure Drift in LLM Serving Systems](https://proceedings.mlsys.org/paper_files/paper/2026/hash/ea0b5818ae9255ee1fb1e3b4442d2ffe-Abstract-Conference.html)
  - Universitas Mercatorum；Gianluigi Vitale
  - DriftBench 是评估 LLM 基础设施变更是否会造成输出漂移的测量集和风险预测器，不负责消除漂移。它覆盖模型、GPU、框架和精度的 105 种配置，用 Portability Risk Index 判断一次升级可由已有测量外推，还是必须重新跑测试；结果显示硬件/精度较可预测，框架/模型变化则高度特异。数据集包含 236985 组 prompt-response、105 个基础设施配置；PRI 对未见硬件的 R² 为 0.909、未见精度为 0.763。
  - 相较每次基础设施变更都重测或完全不测，核心创新是给出可预测维度与必须重测维度的 predict-or-measure 规则。
  - LLM 基础设施漂移、输出一致性、升级风险预测

- [IntAttention: A Fully Integer Attention Pipeline for Efficient Edge Inference](https://proceedings.mlsys.org/paper_files/paper/2026/hash/ea5ffdf7da91256ecd2770f9fd2dade9-Abstract-Conference.html)
  - Southern University of Science and Technology；Wanli Zhong、Haibo Feng、Zirui Zhou 等
  - IntAttention 是完全整数化的 attention 数据通路，用来消除边缘 CPU 上 INT8 matmul 前后仍需执行浮点 softmax 的转换瓶颈。IndexSoftmax 用整数索引、32 项查找表、稀疏感知裁剪和整数归一化近似指数运算，使 QK、softmax 到 AV 全程不回到 FP16。Armv8 CPU 上相对 FP16 最高加速 3.7 倍、节能 61%，相对普通 INT8 attention 最高仍快两倍。
  - 相较 INT8 matmul 后回到浮点 softmax，核心创新是 IndexSoftmax 保持 attention 全链整数。
  - 边缘 Transformer 推理、全整数 Attention、IndexSoftmax

- [BEAM: Joint Resource–Power Optimization for Energy-Efficient LLM Inference under SLO contraints](https://proceedings.mlsys.org/paper_files/paper/2026/hash/eb3c42ddfa16d8421fdba13528107cc1-Abstract-Conference.html)
  - KAIST；Hyunjae Lee、Sangjin Choi、Seungjae Lim 等
  - BEAM 是 LLM 在线服务的资源—功耗联合控制器，同时决定 batch/资源使用和 GPU DVFS 档位，而不是分别优化吞吐与频率。它根据每个请求剩余 SLO slack 细粒度调整两类旋钮，在不违反延迟目标的前提下降低空转和过高频率造成的能耗。vLLM 实现按请求 deadline 反馈调整控制，端到端 GPU 能耗最高降低 51%，而不是以统一低频牺牲尾延迟。
  - 相较单独调 batching 或 DVFS，核心创新是在每请求 SLO 反馈下联合控制资源效率与功率。
  - 节能 LLM Serving、请求级 SLO、Batching-DVFS 联合控制

- [BOute: Cost-Efficient LLM Serving with Heterogeneous LLMs and GPUs via Multi-Objective Bayesian Optimization](https://proceedings.mlsys.org/paper_files/paper/2026/hash/ed1d3d4c64dc1b95332a8cde3f2a0bdf-Abstract-Conference.html)
  - Shanghai Jiao Tong University；YOUHE JIANG、Fangcheng Fu、Eiko Yoneki
  - BOUTE 只处理在线 LLM 推理，不涉及训练；它支持能力和规模不同的多个 LLM，包括把容易或低风险请求交给较小模型、把困难或高风险请求交给较大模型。路由发生在单个请求到达时，依据 router 预测的查询难度或小模型满足质量要求的概率设置阈值，并非只看输入长度。部署优化则在服务场景级进行：离线 profile 模型在不同 GPU 上的算力、HBM 带宽、显存与不同 QPS 下的 P95 latency，在线 MOBO 联合决定模型-GPU 类型映射、GPU 数量、replica 数以及 DP/TP/PP；路由形成的各模型到达率、GPU 单价与总预算、质量下限和延迟目标共同构成约束。
  - 相较先固定 model routing 再规划 GPU，核心创新是显式解决路由改变各模型负载、部署又反过来改变最优路由的循环依赖，并搜索质量-延迟 Pareto 前沿。
  - 在线 LLM 推理、请求级模型路由、异构 GPU 部署、多目标贝叶斯优化

- [Practical Adversarial Multi-Armed Bandits with Sublinear Runtime](https://proceedings.mlsys.org/paper_files/paper/2026/hash/efbd571f139d26604e53fe2760e2c073-Abstract-Conference.html)
  - Aarhus University、University of Melbourne、University of Copenhagen；Kasper Overgaard Mortensen、Ama Bembua Bainson、Mathias Ravn Tversted 等
  - QBL 是用于非平稳 adversarial multi-armed bandit 的在线算法，适合数据库物理设计等候选配置极多且最佳项随时间变化的自动调优。它用优先队列只更新每轮实际涉及的少数 arm，并以常数成本采样和均衡探索，使单轮运行时间不再随全部候选数线性增长。在 adversarial/non-stationary benchmark 上，它同时改善运行时间和选择质量，适合候选配置数量远大于每轮可评测数的调优器。
  - 相较每轮扫描全部 arm，核心创新是优先队列限制更新与常数成本采样，使 adversarial bandit 达到关于总 arm 数的次线性运行时间。
  - 在线自动调优、Adversarial Bandit、次线性候选搜索

- [ADR: AN AGENTIC DETECTION SYSTEMFORENTERPRISE AGENTIC AI SECURITY](https://proceedings.mlsys.org/paper_files/paper/2026/hash/f03cb785864596fa5901f1359d23fd81-Abstract-Conference.html)
  - Uber、MIT、University of Oxford；Chenning Li、Pan Hu、Justin Xu 等
  - ADR 是部署在 Uber 的企业 Agent 安全监测与响应系统，监控通过 MCP 调用工具的 Agent，并把用户提示、推理链、工具参数和最终系统行为关联起来。Sensor 采集高保真 telemetry，Explorer 在上线前生成攻击样本，Detector 先低成本筛查再用上下文推理复核，从而覆盖传统 EDR 看不到的提示注入和因果意图。生产规模达到 7200 余台主机、每日一万余 Agent session；ADR-Bench 上零误报检出 67% 攻击，并发现数百次凭据暴露。
  - 相较 EDR 只看文件/网络行为或规则 guardrail，核心创新是采集 Agent 意图到工具结果的因果 telemetry，并用低成本筛查+上下文推理两级检测。
  - Agent Security—MCP Telemetry、提示注入检测、企业 EDR

- [TriInfer: Hybrid EPD Disaggregation for Efficient Multimodal Large Language Model Inference](https://proceedings.mlsys.org/paper_files/paper/2026/hash/f068c65585985c25c17f221390774ec7-Abstract-Conference.html)
  - Beihang University；Xianzhe Dong、Tongxuan Liu、Yuting Zeng 等
  - TriInfer 是多模态大模型的 Encode-Prefill-Decode 三阶段解耦服务系统。视觉编码、语言 prefill 和 token decode 被放到适合各自算力、显存与 SLO 的异构实例，调度器可独立扩缩每个阶段并做阶段内 batching，避免沿用纯语言模型的耦合流水导致设备互相等待。真实多模态 workload 上，在满足 P90 请求 SLO 时相对 vLLM/SGLang 最高提高 2.4 倍吞吐。
  - 相较沿用语言模型两阶段 serving，核心创新是把视觉 encode 独立成第三阶段，并按阶段异构扩缩容和 batching。
  - 多模态 LLM Serving、Encode-Prefill-Decode 解耦、阶段级 Batching

- [FreeScale: Distributed Training for Sequence Recommendation Models with Minimal Scaling Cost](https://proceedings.mlsys.org/paper_files/paper/2026/hash/f189e7580acad0fc7fd45405817ddee3-Abstract-Conference.html)
  - Meta；Chenhao Feng、Haoli Zhang、Shakhzod Ali-zade 等
  - FreeScale 是工业序列推荐模型的大规模训练系统，解决不同用户历史长度造成计算 straggler、embedding 通信阻塞以及通信 kernel 抢占 SM 的三重问题。它先构造计算量均衡的样本 batch，再按优先级把 embedding 传输与计算重叠，并使用不占 SM 的通信路径减少两者竞争。256 张 H100 的真实推荐训练中，计算气泡最多减少 90.3%，说明优化对象是 sequence sample 与 embedding 通信共同造成的失衡。
  - 相较只做样本均衡或通信重叠，核心创新是把 straggler、embedding 优先级和 SM 竞争三者协同消除。
  - 序列推荐训练、Embedding 通信重叠、Straggler 消除

- [FLoRIST: Singular Value Thresholding for Efficient and Accurate Federated Fine-Tuning of Large Language Models](https://proceedings.mlsys.org/paper_files/paper/2026/hash/f38cb4cf9a5eaa92b3cfa481832719c6-Abstract-Conference.html)
  - University of Arizona；Hariharan Ramesh、Jyotikrishna Dass
  - FLoRIST 是联邦 LoRA 的服务器聚合算法，目标是在不上传完整权重、也不把所有本地 adapter 拼成巨大稠密矩阵的情况下得到数学上准确的全局低秩更新。它分别对堆叠的 A/B adapter 做紧凑空间分解，再按奇异值阈值自动选择全局 rank并下发一对共享 LoRA。多数据集和 LLM 的同构、异构客户端实验中，它减少客户端下载量，同时保持或超过现有聚合方法的任务性能。
  - 相较平均 LoRA 或重建稠密全局更新，核心创新是在紧凑奇异空间精确聚合并自适应选 rank。
  - 联邦 LoRA、精确低秩聚合、奇异值阈值选 Rank

- [Dataflow Is All You Need](https://proceedings.mlsys.org/paper_files/paper/2026/hash/f502981cbe221d857ad409450a7917c3-Abstract-Conference.html)
  - SambaNova Systems；Darshan Gandhi、Pushkar Nandkar、David Koeplinger 等
  - 这是一篇围绕 SambaNova SN40 数据流处理器的 LLM 解码软硬件协同设计，而不是提出通用软件调度器。Kernel Looping 让设备端重复执行算子、Batch Streaming 让请求连续流过阵列、Schedule Offloading 把 CPU 发射工作移入数据流硬件，三者共同避免 kernel 边界和主机调度限制带宽。这些机制对小/大、dense/MoE/hybrid 和不同 attention 都适用，达到理论 roofline 75% 以上；16 张 SN40 上的推测解码比 DGX H100 快 1.7 倍。
  - 相较 GPU kernel fusion，核心创新是让数据流硬件持续执行、流式进 batch 并接管 schedule，统一消除 host 和同步开销。
  - 数据流加速器 LLM 推理、Decode 带宽墙、硬件调度卸载

- [DreamDDP: Accelerating Low-Bandwidth Geo-Distributed LLM Training with Layer-wise Partial Synchronization](https://proceedings.mlsys.org/paper_files/paper/2026/hash/f5c530d3f287c43dccfca298698e9254-Abstract-Conference.html)
  - Harbin Institute of Technology；zhenheng Tang、Zichen TANG、Junlin Huang 等
  - DreamDDP 是低带宽跨地域训练框架，核心变化是把 Local SGD 的“隔若干步同步整个模型”改为每轮只同步选定层。系统依据逐层 profile 排列同步顺序，并让某些层通信时其他层继续前后向计算，因此在不增加 GPU 内存的情况下隐藏广域网传输。32 张 GPU 上覆盖 ResNet、GPT-2 与 Llama-2，低带宽环境下相对领先方法提高 1.49–3.91 倍且保持收敛保证。
  - 相较周期性全模型 Local SGD 同步，核心创新是逐层部分同步并用 profile 安排可重叠通信。
  - 跨地域分布式训练、逐层部分同步、低带宽通信重叠

- [Using Span Queries to Optimize Cache and Attention Locality](https://proceedings.mlsys.org/paper_files/paper/2026/hash/f5d77f1e501e0496377d8b68c8e81a48-Abstract-Conference.html)
  - IBM Research；Paul Castro、Nick Mitchell、Nathan Ordonez 等
  - Span query 是统一描述 chat、RAG、inference-time scaling 和 Agent 多调用工作流的表达式树，每个输入片段还标明是否允许交换顺序。运行时可在满足语义约束的前提下重排片段，以最大化跨请求 KV 命中和注意力局部性；论文仅改动约 492 行 vLLM 即支持这种执行。在 chat 之外的两类工作流中，TTFT 降低 10–20 倍；attention 重排还使 2B 模型准确率明显超过未优化的 8B serving baseline。
  - 相较只为 RAG 特制缓存，核心创新是显式表达片段可交换性，用一个查询代数统一并安全优化非线性 LLM 工作流。
  - Agent Infra—Span Query、非线性 KV 复用、Attention 局部性

- [Privatar: Scalable Privacy-preserving Multi-user VR via Secure Offloading](https://proceedings.mlsys.org/paper_files/paper/2026/hash/fb1d9c3fc2161e12aa71cdcab74b9d2c-Abstract-Conference.html)
  - Georgia Institute of Technology；Jianming Tong、Hanshen Xiao、Krishna Kumar Nair 等
  - Privatar 是多人 VR 头像重建的隐私卸载系统，头显保留能暴露表情的高能频率分量，只把低能 DCT 分量交给局域网中的不可信设备计算。Distribution-Aware Minimal Perturbation 再根据用户表情分布加入满足本地差分隐私的最小噪声，从而在提高并发人数时兼顾形式化隐私与画质。Meta Quest Pro 上并发用户数提高 2.37 倍，重建损失增加约 5.7%–6.5%、能耗约增 9%，并抵抗表情识别攻击。
  - 相较通用加噪或完全本地渲染，核心创新是利用头像频域结构只卸载低敏感分量，再按用户分布最小化 DP 噪声。
  - 多人 VR 边缘卸载、局部差分隐私、频域分区

- [Machine Learning Fleet Efficiency: Improving TPU Systems at Scale with ML Productivity Goodput](https://proceedings.mlsys.org/paper_files/paper/2026/hash/fbe2b2f74a2ece8070d8fb073717bda6-Abstract-Conference.html)
  - Google；Arissa Wongpanich、Tayo Oguntebi、Jose Baiocchi Paredes 等
  - ML Productivity Goodput 是 Google 用于分析整个 TPU fleet 的效率指标和分解方法，不把 GPU/TPU utilization 直接等同于有效产出。它把损失归因到调度 goodput、运行时 goodput 和程序 goodput，使抢占等待、checkpoint、框架开销、编译质量及通信重叠能在不同层分别被量化和治理。在 Google 真实 TPU workload 上，框架分别发现 preemption、异步 checkpoint 和通信-计算重叠等层级的优化机会，而不是给出一个不可解释的总利用率。
  - 相较 GPU utilization 等单一指标，核心创新是把有效 ML 产出损失分解到调度、runtime 和 program 三层。
  - TPU Fleet 效率、ML Productivity Goodput、分层瓶颈归因

- [ParallelKittens: Systematic and Practical Simplification of Multi-GPU AI Kernels](https://proceedings.mlsys.org/paper_files/paper/2026/hash/ff997469ac66cf893c4183efeb22212a-Abstract-Conference.html)
  - Stanford University；Stuart H. Sul、Simran Arora、Benjamin F. Spector 等
  - ParallelKittens 是开发多 GPU 重叠 kernel 的轻量 CUDA 框架，而不是自动并行编译器。它从数据搬运、资源调度和同步中提炼八个核心原语与统一模板，让作者用不到 50 行设备代码显式组织计算—通信重叠，并覆盖数据、张量、序列和专家并行。Hopper 与 Blackwell 上，数据/张量并行最高加速 2.33 倍、序列并行 4.08 倍、专家并行 1.22 倍。
  - 相较为每个并行模式手写复杂 kernel，核心创新是以八个可复用原语和统一模板表达多 GPU 计算-通信重叠。
  - 多 GPU Kernel DSL、计算-通信重叠、统一并行原语
