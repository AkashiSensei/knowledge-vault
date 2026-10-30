# MLSys 2024 论文列表

官方 Proceedings 共收录 37 篇论文。以下标题均链接至对应的官方论文摘要页。每篇依次列出机构与主要作者、核心工作、相较既有方法的核心创新，以及便于快速识别研究对象与技术路径的细粒度方向。

- [Punica: Multi-Tenant LoRA Serving](https://proceedings.mlsys.org/paper_files/paper/2024/hash/054de805fcceb78a201f5e9d53c85908-Abstract-Conference.html)
  - University of Washington、Duke University、OctoAI；Lequn Chen、Zihao Ye、Yongji Wu 等
  - Punica 面向共享 GPU 集群中的在线多租户 LLM 推理：不同租户使用同一基础模型的不同 LoRA adapter，系统只在 GPU 中保留一份基础权重，并在请求进入 decode 时按 adapter 合并成 batch。新的 SGMV CUDA kernel 可在一个批次中执行不同 LoRA 矩阵，调度器优先把请求压到已激活 GPU、按需装载 adapter 并迁移既有请求；在 Llama2 7B/13B/70B 上，相同 GPU 数量下吞吐最高提高 12 倍，每 token 仅增加约 2 ms。
  - 相较把每个 LoRA 当作独立模型部署或只能对同一 adapter batching，核心创新是让异构 adapter 的低秩计算可共同批处理，从而同时实现权重共享和租户间资源整合。
  - 多租户 LoRA Serving、异构 Adapter Batching、SGMV Kernel、GPU Consolidation

- [ACROBAT: Optimizing Auto-batching of Dynamic Deep Learning at Compile Time](https://proceedings.mlsys.org/paper_files/paper/2024/hash/096b1019463f34eb241e87cfce8dfe16-Abstract-Conference.html)
  - Carnegie Mellon University、OctoAI；Pratik Fegade、Tianqi Chen、Phillip Gibbons、Todd Mowry
  - ACRoBat 处理含分支、循环和早退的动态深度学习程序，这类程序不同样本走过的控制流不同，人工 batching 难以保持硬件利用率。编译器先静态识别可跨样本合并的算子与依赖，再在运行时依据实际控制路径形成 batch，并端到端生成张量代码；在 RTX 3070 上，相对 DyNet 自动 batching 最高加速 8.5 倍。
  - 相较完全依赖运行时逐步聚合算子，核心创新是把静态控制流分析与动态 batching 协同到同一编译流程，在保留动态语义的同时提前消除调度和解释开销。
  - 动态神经网络编译、自动 Batching、静态-动态联合优化、张量代码生成

<a id="heteroswitch"></a>

- [HeteroSwitch: Characterizing and Taming System-Induced Data Heterogeneity in Federated Learning](https://proceedings.mlsys.org/paper_files/paper/2024/hash/0badcb4e95306df76a719409155e46e8-Abstract-Conference.html)
  - Korea University、Arizona State University、Meta；Gyudong Kim、Mehdi Ghasemi、Soroush Heidari 等
  - HeteroSwitch 研究联邦学习中由摄像头、传感器、软件栈和设备档位差异造成的“系统诱导数据异质性”，它与用户本身的非 IID 数据不同，会让同一现实对象在不同设备上产生系统性偏差。作者先用异构真机采集数据量化其对准确率、公平性和域泛化的影响，再根据观测到的设备偏差强度在 ISP 变换与 SWAD 泛化训练之间自适应切换；在 FLAIR 设置中把不同设备类型的平均精度方差降低 6.3%。
  - 相较只按标签分布处理客户端非 IID，核心创新是把硬软件配置引入数据生成链路，并针对可测的设备偏差动态选择泛化机制。
  - 联邦学习数据异质性、设备偏差建模、域泛化、客户端公平性

- [JIT-Q: Just-in-time Quantization with Processing-In-Memory for Efficient ML Training](https://proceedings.mlsys.org/paper_files/paper/2024/hash/136b9a13861308c8948cd308ccd02658-Abstract-Conference.html)
  - AMD；Mohamed Ibrahim、Shaizeen Aga、Ada Li 等
  - JIT-Q 面向需要同时保存高精度主权重和一种或多种低精度计算副本的训练任务。系统只在内存中长期保存高精度权重，在算子即将消费时由 processing-in-memory 单元就地生成 MX9、MX6 等低精度副本，并与 GPU 计算并发，从而避免低精度副本占用容量及在内存总线上往返；最多节省 24% 权重内存，吞吐损失不超过 2.4%。
  - 相较预先量化并长期保存每种数据格式，核心创新是把量化变成内存侧的即时数据供给阶段，以 PIM 隐藏转换成本并释放训练容量。
  - 低精度训练、即时量化、Processing-in-Memory、权重内存容量

- [Schrodinger's FP Training Neural Networks with Dynamic Floating-Point Containers](https://proceedings.mlsys.org/paper_files/paper/2024/hash/185087ea328b4f03ea8fd0c8aa96f747-Abstract-Conference.html)
  - University of Toronto、Vector Institute、Qualcomm、AMD 等；Milos Nikolic、Enrique Torres Sanchez、Jiahui Wang 等
  - 该工作在训练过程中自动决定每一层的权重和激活该用多少 exponent、mantissa 位，并允许位宽随训练阶段变化，而不要求用户反复试精度。Quantum Mantissa/Exponent 借助梯度下降学习不会损害精度的最小位宽，BitWave 根据 loss 变化做全网调整，Gecok 再无损压缩偏斜的 exponent 分布；组合后张量占用最高平均缩小 5.61 倍。
  - 相较为全模型固定选择 FP16/FP8 或人工搜索混合精度，核心创新是把浮点容器的格式、张量归属和时间变化同时纳入训练自适应过程。
  - 动态浮点格式、训练张量压缩、逐层混合精度、内存流量降低

- [Lancet: Accelerating Mixture-of-Experts Training via Whole Graph Computation-Communication Overlapping](https://proceedings.mlsys.org/paper_files/paper/2024/hash/339caf45a6fa281cae8adc6465343464-Abstract-Conference.html)
  - The University of Hong Kong、Amazon Web Services、Boson AI；Chenyu Jiang、Ye Tian、Zhen Jia 等
  - Lancet 是 MoE 训练编译优化系统，针对 expert parallel 的 All-to-All 长时间阻塞 GPU。它不只在单个 MoE 层内部切分 expert computation，而是分析整个前向/反向计算图：前向把非 MoE 算子分块并与通信流水，反向重排 weight-gradient 计算来覆盖 All-to-All；编译器自动生成计划，最多减少 77% 未被覆盖的通信时间，端到端最高加速 1.3 倍。
  - 相较仅让当前 MoE 层的 expert kernel 与通信重叠，核心创新是把可用于隐藏通信的计算范围扩大到全图，并分别利用前向非 MoE 计算和反向权重梯度。
  - MoE 分布式训练、全图调度、All-to-All 重叠、编译器优化

- [AWQ: Activation-aware Weight Quantization for On-Device LLM Compression and Acceleration](https://proceedings.mlsys.org/paper_files/paper/2024/hash/42a452cbafa9dd64e9ba4aa95cc1ef21-Abstract-Conference.html)
  - MIT、Shanghai Jiao Tong University、NVIDIA、Tsinghua University 等；Ji Lin、Jiaming Tang、Haotian Tang 等
  - AWQ 是训练免的 LLM weight-only 低比特量化：它根据校准输入的 activation 判断哪些权重通道对输出最敏感，通过搜索逐通道缩放保护约 1% 的关键权重，再把其余权重量化，而不做反向传播或逐层重构。配套边缘推理引擎用低比特 kernel 在桌面和移动 GPU 上获得 3 倍以上加速，并使 70B Llama2 可在移动 GPU 环境部署。
  - 相较只根据权重幅值选择异常值或在校准集上重构层输出，核心创新是用 activation 而非 weight 本身识别显著通道，以极少保护量换取跨任务、指令模型和多模态模型的泛化。
  - LLM Weight-Only Quantization、Activation-Aware Scaling、端侧推理、低比特 Kernel

- [DiffusionPipe: Training Large Diffusion Models with Efficient Pipelines](https://proceedings.mlsys.org/paper_files/paper/2024/hash/45c1f6a8cbf2da59ebf2c802b4f742cd-Abstract-Conference.html)
  - The University of Hong Kong、Amazon Web Services、The Ohio State University；Ye Tian、Zhen Jia、Ziyue Luo 等
  - DiffusionPipe 面向含一个或多个可训练 backbone、同时含冻结文本/图像 encoder 的大型扩散模型训练。动态规划联合搜索 stage partition 和同步 pipeline schedule，再用贪心算法把冻结模块计算塞入 backbone pipeline bubble，而不是让这些独立组件扩大空闲时间；在多种扩散模型上较既有流水并行最高加速 1.41 倍、较数据并行最高 1.28 倍。
  - 相较按 Transformer 层均分或把冻结模块固定在流水线外执行，核心创新是利用扩散模型“可训练 backbone + 非训练组件”的结构特征专门填充 pipeline bubble。
  - 扩散模型训练、Pipeline Parallelism、Bubble Filling、Stage Partition

<a id="keyformer"></a>

- [Keyformer: KV Cache reduction through key tokens selection for Efficient Generative Inference](https://proceedings.mlsys.org/paper_files/paper/2024/hash/48fecef47b19fe501d27d338b6d52582-Abstract-Conference.html)
  - The University of British Columbia、d-Matrix；Muhammad Adnan、Akhil Arunkumar、Gaurav Jain 等
  - Keyformer 面向长上下文自回归生成的 decode 阶段，观察到约 90% attention weight 集中在少量 key token。它用考虑被丢弃 token 影响的新评分函数动态选择要保留的 KV，而非按固定窗口保存全部历史；在 GPT-J、Cerebras-GPT 和 MPT 的摘要、对话任务中同时减少显存与带宽，使 latency 改善 2.1 倍、token throughput 提高 2.4 倍且维持准确率。
  - 相较只按最近位置或累计 attention 大小淘汰 KV，核心创新是让 token 重要性评分显式补偿已丢弃上下文，从而在不同位置编码模型上稳定保留关键状态。
  - 长上下文推理、KV Cache Eviction、Key Token Selection、Decode 带宽

- [Accelerating ReLU for MPC-Based Private Inference with a Communication-Efficient Sign Estimation](https://proceedings.mlsys.org/paper_files/paper/2024/hash/4e3157021c5f833bb2204081f1dda573-Abstract-Conference.html)
  - Pennsylvania State University、Meta FAIR、Cornell University；Kiwan Maeng、G. Edward Suh
  - HummingBird 加速两方/多方安全计算中的私有 DNN 推理，瓶颈是为了判断 ReLU 输入正负而通信完整位宽。它通过理论界限和搜索器为不同层确定只需交换的高有效位：精确模式可丢弃 66%–72% 位且不改变 ReLU，近似模式可丢弃 87%–91%；真实 MPC 环境中无误差端到端加速 2.03–2.67 倍，允许精度损失时最高 8.42 倍。
  - 相较把 sign/ReLU 当作必须执行完整比较的黑盒协议，核心创新是证明并搜索“判断符号所需的最小位前缀”，直接削减非线性层通信。
  - MPC 私有推理、ReLU Sign Estimation、通信削减、安全计算

- [FlashDecoding++: Faster Large Language Model Inference with Asynchronization, Flat GEMM Optimization, and Heuristics](https://proceedings.mlsys.org/paper_files/paper/2024/hash/5321b1dabcd2be188d796c21b733e8c7-Abstract-Conference.html)
  - Tsinghua University、Infinigence-AI、Shanghai Jiao Tong University、Peking University；Ke Hong、Guohao Dai、Jiaming Xu 等
  - FlashDecoding++ 是覆盖 NVIDIA 与 AMD GPU 的 LLM 推理 kernel/engine。它用统一最大值消除分块 softmax 的同步更新并细粒度流水，用双缓冲和形状专用方案提高小 batch 下 flat GEMM 利用率，再依据输入形状和 Tensor/CUDA core 资源选择数据流；相对 FlashDecoding 平均加速 1.37 倍，相对 Hugging Face 在不同硬件上最高 4.86 倍。
  - 相较只优化 attention 或为所有 GEMM 使用单一静态数据流，核心创新是把异步 softmax、flat GEMM 和硬件感知数据流作为 decode 全链路共同设计。
  - LLM Decode Kernel、异步 Softmax、Flat GEMM、跨 GPU 后端

- [HeteGen: Efficient Heterogeneous Parallel Inference for Large Language Models on Resource-Constrained Devices](https://proceedings.mlsys.org/paper_files/paper/2024/hash/5431dca75a8d2abc1fb51e89e8324f10-Abstract-Conference.html)
  - National University of Singapore；Zhao Xuanlei、Bin Jia、Haotian Zhou 等
  - HeteGen 面向单机 GPU 显存放不下 LLM、且 batch 通常为 1 的交互式推理。它把模型计算和权重/激活在 CPU、GPU 间做异构并行，不再只是按层顺序 offload；运行时将 CPU 计算、GPU 计算和 I/O 异步重叠，以降低 PCIe 数据搬移暴露时间，相较既有低内存推理方案最高提升约 317%。
  - 相较 CPU 仅作为权重仓库、逐层传输后由 GPU 计算的 offloading，核心创新是让 CPU 也承担可并发的模型计算，并用统一异构并行计划覆盖 I/O。
  - 资源受限 LLM 推理、CPU-GPU 异构并行、权重卸载、异步重叠

- [CloudEval-YAML: A Practical Benchmark for Cloud Configuration Generation](https://proceedings.mlsys.org/paper_files/paper/2024/hash/554e056fe2b6d9fd27ffcd3367ae1267-Abstract-Conference.html)
  - Alibaba Cloud、University of Michigan、UCLA、UC Merced；Yifei Xu、Yuning Chen、Xumiao Zhang 等
  - CloudEval-YAML 评估 LLM 生成 Kubernetes 等云原生工具 YAML 配置的实际可用性。数据集含 1,011 个由人工编写、带单元测试的问题，并提供简写、精简和双语表述以模拟运维输入；并行评测平台将执行速度提高 20 倍，作者比较 12 个 LLM 的正确率、成本及通过提示或输入简化改善表现的方法。
  - 相较 HumanEval 一类通用代码题或从仓库自动抽取配置，核心创新是用人工场景、可执行测试和多种真实提问形式建立面向云配置的功能正确性基准。
  - LLM for Systems—云配置生成、可执行 Benchmark、YAML、运维代码评测

- [Atom: Low-Bit Quantization for Efficient and Accurate LLM Serving](https://proceedings.mlsys.org/paper_files/paper/2024/hash/5edb57c05c81d04beb716ef1d542fe9e-Abstract-Conference.html)
  - Shanghai Jiao Tong University、University of Washington、Peking University、OctoAI 等；Yilong Zhao、Chien-Yu Lin、Kan Zhu 等
  - Atom 针对高并发在线 LLM serving，把权重和 activation 同时量化到 4 bit，使 batching 后的矩阵计算能直接使用现代 GPU 的低比特算子。为控制异常值误差，它采用细粒度 group quantization、混合精度并专门布局数据和 kernel；在相同 latency target 下，吞吐较 FP16 最高提高 7.73 倍、较 INT8 最高提高 2.53 倍。
  - 相较只做 weight-only 或停留在 INT8 的服务量化，核心创新是把 W4A4 精度策略、内存布局和 GPU kernel 联合设计，使低比特算力真实转化为 batch throughput。
  - LLM Serving Quantization、W4A4、混合精度、低比特 GPU Kernel

- [Accurate Low-Degree Polynomial Approximation of Non-Polynomial Operators for Fast Private Inference in Homomorphic Encryption](https://proceedings.mlsys.org/paper_files/paper/2024/hash/621d0fd41c720ab252e178b77c200d90-Abstract-Conference.html)
  - Georgia Institute of Technology、Carnegie Mellon University；Jingtian Dang、Jianming Tong、Anupam Golder 等
  - SmartPAF 面向全同态加密 DNN 推理，将昂贵的 ReLU、MaxPooling 替换为低阶多项式。它先根据输入分布调系数，再逐个替换非线性并微调，交替训练多项式和线性层，部署时固定训练所得的输入 scale；因此可用更低 degree 保持准确率，在 ImageNet ResNet-18 上同等准确率下 14 阶方案较 27 阶 minimax 近似加速 7.81 倍。
  - 相较脱离模型数据分布独立拟合多项式，核心创新是把系数、替换顺序、分层训练和输入缩放纳入端到端精度恢复流程。
  - 同态加密推理、多项式近似、非线性算子替换、Accuracy-Latency Tradeoff

- [SiDA: Sparsity-Inspired Data-Aware Serving for Efficient and Scalable Large Mixture-of-Experts Models](https://proceedings.mlsys.org/paper_files/paper/2024/hash/698cfaf72a208aef2e78bcac55b74328-Abstract-Conference.html)
  - Duke University、Clemson University、University of Maryland；Zhixu Du、Shiyu Li、Yuhao Wu 等
  - SiDA-MoE 在 GPU 无法常驻全部 expert 权重时，把大部分参数放在主存，并根据输入即将激活哪些 expert 决定预取和驻留，而不是逐层被动换入。系统利用 token routing 的稀疏性形成 data-aware CPU-GPU 权重流，在性能下降最低约 1% 的设置中最高节省 80% GPU memory、提高 3.93 倍吞吐并降低 72% latency。
  - 相较静态把固定 expert 放在 GPU 或按访问发生后再 offload，核心创新是利用输入相关 expert 激活预测来组织异构内存中的权重供给。
  - MoE Serving、Expert Weight Offload、Data-Aware Prefetch、CPU-GPU 内存层次

- [Does Compressing Activations Help Model Parallel Training?](https://proceedings.mlsys.org/paper_files/paper/2024/hash/71381211d0abef73ed1887b83c4547b1-Abstract-Conference.html)
  - University of Wisconsin-Madison、Carnegie Mellon University、MBZUAI、Petuum；Song Bian、Dacheng Li、Hongyi Wang 等
  - MCBench 系统评估 tensor/pipeline model parallel 训练中压缩跨 GPU activation 是否真正有益，覆盖四类压缩算法、语言与视觉模型、预训练和微调，以及 200 多种 Megatron-LM 配置。作者同时建立包含压缩开销、链路和并行规模的 cost model，用来解释为何 data-parallel gradient compression 的经验不能直接迁移到 activation；主要产出是适用边界而非单一新压缩器。
  - 相较只报告某个压缩算法在少量模型上的通信量，核心创新是首次把模型并行 activation compression 的质量、计算开销和扩展性放在统一实证与成本模型中比较。
  - 模型并行训练、Activation Compression、MCBench、通信成本建模

- [Distributed Matrix-Based Sampling for Graph Neural Network Training](https://proceedings.mlsys.org/paper_files/paper/2024/hash/75bb91b908e6924763c9f2bbe87e921e-Abstract-Conference.html)
  - University of California, Berkeley、Lawrence Berkeley National Laboratory；Alok Tripathy、Katherine Yelick、Aydin Buluc
  - 该工作把分布式 GNN 的多 mini-batch 邻居采样统一表达为 sparse matrix multiplication，并一次批量采样多个 batch。当图拓扑跨 GPU 时使用 communication-avoiding SpGEMM；当拓扑可装入单 GPU 时在本地无通信采样，再通过一次 All-to-All 复制 feature 以减少后续随机拉取。在 128 GPU 上较 Quiver 最高获得 2.5 倍，其他大图每 epoch 最高加速 8.46 倍。
  - 相较为每种 sampling algorithm 编写逐 batch 图遍历和远程 feature 请求，核心创新是用矩阵构造统一采样语义，并复用成熟的分布式 SpGEMM 通信优化。
  - 分布式 GNN 训练、矩阵化邻居采样、Communication-Avoiding SpGEMM、Feature Replication

- [Disaggregated Multi-Tower: Topology-aware Modeling Technique for Efficient Large Scale Recommendation](https://proceedings.mlsys.org/paper_files/paper/2024/hash/78834433edc3291f4c6cbbd2759324db-Abstract-Conference.html)
  - Meta AI、NVIDIA；Liang Luo、Buyun Zhang、Michael Tsang 等
  - DMT 解决推荐模型平坦 embedding 架构与数据中心分层网络不匹配的问题。它在保持推荐语义的前提下把全局 embedding lookup 划为若干 locality-aware tower，每个 tower 附加 dense module 做局部 feature interaction，再由基于 learned embedding 的 partitioner 平衡负载并把强相关特征放在一起；大规模多代硬件上最高加速 1.9 倍且不损失准确率。
  - 相较在原模型上单独优化 All-to-All，核心创新是直接重构模型为匹配网络拓扑的多 tower，使跨域通信在建模阶段就被消除或缩小。
  - 推荐系统训练、拓扑感知模型重构、Embedding Locality、All-to-All 削减

- [VQPy: An Object-Oriented Approach to Modern Video Analytics](https://proceedings.mlsys.org/paper_files/paper/2024/hash/87eaaa8605a1a472d9a9756e7500517b-Abstract-Conference.html)
  - UCLA、Intel、Harvey Mudd College、Cisco Research；Shan Yu、Zhenting Zhu、Yu Chen 等
  - VQPy 把视频中的人、车及其时序关系建模为对象，让用户用带视频对象、属性和交互构造的 Python 方言声明查询。后端依据对象依赖自动建立检测、跟踪和过滤 pipeline，并允许接入不同算子和优化；系统已开源并用于工业 DeepVision 框架，目标是降低复杂视频分析应用的表达和部署成本。
  - 相较把查询写成手工串联的 detector/tracker DAG，核心创新是以面向对象语义同时承载视频查询表达与后端 pipeline 构造优化。
  - 视频分析 DSL、对象化查询、自动 Pipeline 构建、可扩展运行时

- [SLoRA: Scalable Serving of Thousands of LoRA Adapters](https://proceedings.mlsys.org/paper_files/paper/2024/hash/906419cd502575b617cc489a1a696a67-Abstract-Conference.html)
  - University of California, Berkeley、Stanford University、Shanghai Jiao Tong University；Ying Sheng、Shiyi Cao、Dacheng Li 等
  - SLoRA 面向成千上万个共享基础 LLM 的 LoRA adapter 在线服务。adapter 长期保存在 CPU memory，仅把当前请求所需权重调入 GPU；统一分页内存池同时管理不同 rank adapter 和不同长度 KV Cache，配合专用 batched LoRA kernel 与 tensor parallel 策略，在单/多 GPU 上减少碎片和传输。相较 Hugging Face PEFT、朴素 vLLM 支持，吞吐最高提高 4 倍、可服务 adapter 数量提高数个数量级。
  - 相较只优化 LoRA 矩阵计算，核心创新是把 adapter 权重与 KV 状态放入统一动态分页体系，并使跨 adapter batching 可扩展到 tensor parallel。
  - 多租户 LoRA Serving、统一分页内存、Adapter Offload、Tensor Parallel

<a id="l-greco"></a>

- [L-GreCo: Layerwise-adaptive Gradient Compression For Efficient Data-parallel Deep Learning](https://proceedings.mlsys.org/paper_files/paper/2024/hash/9069a8976ff06f6443e7f4172990a580-Abstract-Conference.html)
  - Institute of Science and Technology Austria；Ilia Markov、Kaveh Alimohammadi、Elias Frantar、Dan Alistarh
  - L-GreCo 在同步 data-parallel 训练中按层动态选择 gradient quantization、sparsification 或 low-rank compression 的强度。系统先测量各层压缩误差对 loss 的影响，再在全局误差预算下为参数量和敏感度不同的层分配压缩率；跨图像和语言模型最高获得 5 倍压缩、2.5 倍训练加速且恢复原准确率。
  - 相较所有层使用相同 bit、稀疏率或 rank，核心创新是把层级压缩配置建模为满足全局误差约束的资源分配问题，并能包裹多类已有压缩器。
  - 数据并行训练、逐层梯度压缩、误差预算、通信自适应

- [Prompt Cache: Modular Attention Reuse for Low-Latency Inference](https://proceedings.mlsys.org/paper_files/paper/2024/hash/a66caa1703fe34705a4368c3014c1966-Abstract-Conference.html)
  - Yale University、Google；In Gim、Guojun Chen、Seung-seob Lee 等
  - Prompt Cache 面向 system message、模板、共享文档等在不同请求中重复但不一定构成同一完整前缀的内容。开发者用 schema 把 prompt 定义为可复用 module，服务端预计算并保存其 attention state，并在组合新 prompt 时保持位置编码正确；文档问答和推荐等长输入场景中，TTFT 在 GPU 上最高改善 8 倍、CPU 上最高 60 倍，无需修改模型参数。
  - 相较只缓存完全相同的 prompt prefix，核心创新是用显式模块 schema 支持跨 prompt 组合复用 attention state，同时保证位置语义正确。
  - LLM Prompt Cache、模块化 KV 复用、TTFT、结构化 Prompt

- [Fine-Tuning Language Models Using Formal Methods Feedback: A Use Case in Autonomous Systems](https://proceedings.mlsys.org/paper_files/paper/2024/hash/b0131b6ee02a00b03fc3320176fec8f5-Abstract-Conference.html)
  - University of Texas at Austin；Yunhao Yang、Neel P. Bhatt、Tyler Ingebrand 等
  - 该工作让语言模型根据自然语言任务生成自动机控制器，并在抽象 world model 或高保真模拟器中用独立 formal specification 验证控制器。验证通过比例成为排序反馈，自动产生偏好数据并迭代微调模型，避免为自动驾驶等领域持续收集人工反馈；实验中控制器满足规范的比例从 60% 提高到 90%。
  - 相较 RLHF 依赖人工评价生成控制策略，核心创新是把形式验证器变成可自动、可重复且与任务规范直接对齐的反馈来源。
  - LLM for Autonomous Systems、形式化反馈、可验证控制器、自动偏好微调

<a id="vidur"></a>

- [VIDUR: A Large-Scale Simulation Framework for LLM Inference](https://proceedings.mlsys.org/paper_files/paper/2024/hash/b74a8de47d2b3c928360e0a011f48351-Abstract-Conference.html)
  - Georgia Institute of Technology、Microsoft Research India；Amey Agrawal、Nitin Kedia、Jayashree Mohan 等
  - VIDUR 是 LLM serving 的高保真离散事件模拟器，用 microbenchmark profile 与预测模型表示 attention、GEMM 和通信等算子，再重放具体请求到达、输入输出长度、batching、scheduler 和 tensor-parallel 配置。它以低于 5% 的误差预测 latency、throughput、TTFT，用于在不真实占用数十张 GPU 的情况下回答集群规模和配置 what-if 问题，并配套 VIDUR-BENCH 工作负载。
  - 相较只拟合单个请求 latency 的解析模型，核心创新是把算子级性能模型与完整 serving 调度事件结合，支持大规模配置和负载的可扩展重放。
  - LLM Serving Simulator、算子 Profiling、配置规划、Workload Replay

- [Torch2Chip: An End-to-end Customizable Deep Neural Network Compression and Deployment Toolkit for Prototype Hardware Accelerator Design](https://proceedings.mlsys.org/paper_files/paper/2024/hash/b8bf2c0dd0b48511889b7d3b2c5fc8f5-Abstract-Conference.html)
  - Cornell University；Jian Meng、Yuan Liao、Anupreetham Anupreetham 等
  - Torch2Chip 面向 ASIC/FPGA 原型设计者，把 PyTorch 中自定义 quantization/pruning、训练、layer fusion、整数参数导出和硬件验证串成一条可修改流水。它允许非标准 bit width、data format 和用户自定义压缩算法，覆盖 CNN 与 ViT，并把量化后的真实整数权重而非“离散化浮点数”交给芯片端，减少算法结果到原型硬件之间的手工转换。
  - 相较绑定厂商 8-bit 格式或只输出研究模型的压缩工具，核心创新是开放从自定义算法到部署就绪整数参数和融合图的端到端接口。
  - 模型压缩工具链、ASIC/FPGA 部署、可定制量化、算法-硬件协同

- [Q-Hitter: A Better Token Oracle for Efficient LLM Inference via Sparse-Quantized KV Cache](https://proceedings.mlsys.org/paper_files/paper/2024/hash/bbb7506579431a85861a05fff048d3e1-Abstract-Conference.html)
  - University of Texas at Austin、University of Oxford、Eindhoven University of Technology、LLNL、Meta FAIR 等；Zhenyu Zhang、Shiwei Liu、Runjin Chen 等
  - Q-Hitter 联合处理长上下文 KV Cache 的 token sparsification 和低比特 quantization。它指出按累计 attention 选出的 heavy hitter 未必耐量化，而且低比特 KV 又会破坏后续重要 token 判断；因此评分同时考虑注意力重要性与逐层 quantization friendliness，选择既关键又可安全压缩的 token。实验在保持模型质量时最高减少 20 倍内存，并较多种 offload/稀疏基线提高吞吐。
  - 相较先用 H2O 选 token、再独立量化剩余 KV，核心创新是显式建模两种压缩的相互影响，用同一个 oracle 联合决定“保留谁”和“谁适合低比特”。
  - Sparse-Quantized KV Cache、Token Oracle、长上下文推理、联合压缩

<a id="fedtrans"></a>

- [FedTrans: Efficient Federated Learning via Multi-Model Transformation](https://proceedings.mlsys.org/paper_files/paper/2024/hash/bbd7d8bd780fcf7143add2317ba04638-Abstract-Conference.html)
  - University of Illinois Urbana-Champaign、University of Michigan；Yuxuan Zhu、Jiachen Liu、Mosharaf Chowdhury、Fan Lai
  - FedTrans 为设备能力和数据分布各异的大规模 FL 客户端自动产生不同模型，而不是先固定一组 architecture。训练从一个 global model 开始，持续定位结构上的准确率瓶颈、按需执行 model transformation，并把硬件可运行的派生模型分配给客户端；不同结构的更新通过 soft aggregation 共享知识。现实设置下个体准确率提高 13%，总训练成本降低 4 倍。
  - 相较只个性化同一模型权重或并行训练预设模型池，核心创新是在联邦训练过程中按准确率瓶颈在线派生 architecture，并联合模型分配与跨模型聚合。
  - 多模型联邦学习、在线模型变换、设备适配、Soft Aggregation

- [LIFL: A Lightweight, Event-driven Serverless Platform for Federated Learning](https://proceedings.mlsys.org/paper_files/paper/2024/hash/c2a0e26dd9ee7d57e92bb1c24b39659a-Abstract-Conference.html)
  - University of California, Riverside、Cisco Research；Shixiong Qi、K. K. Ramakrishnan、Myungjin Lee
  - LIFL 将大规模 FL 的层次化 model aggregation 改造成弹性 serverless 数据路径。事件驱动设计移除每个 aggregator 的重型 broker 和 container sidecar，以 eBPF proxy 转发更新；同机层级通过 shared memory 处理，locality-aware placement 尽量把有父子关系的聚合放在一起，并精确扩缩、复用函数实例以适应参与客户端数量变化。
  - 相较常驻聚合服务器或每函数携带消息 sidecar 的 serverless FL，核心创新是把 eBPF、共享内存 locality 与层次聚合的弹性生命周期共同设计。
  - 联邦学习基础设施、Serverless Aggregation、eBPF Proxy、Locality-Aware Placement

- [Proteus: Preserving Model Confidentiality during Graph Optimizations](https://proceedings.mlsys.org/paper_files/paper/2024/hash/c66a9db149261435664284a20b6f1d42-Abstract-Conference.html)
  - University of Toronto、Vector Institute、CentML；Yubo Gao、Maryam Haghifam、Christina Giannoula 等
  - Proteus 允许模型开发者把计算图交给外部编译/性能团队优化，又不暴露具有知识产权价值的完整 architecture。它将原图切成 subgraph，并把每个真实片段隐藏在自动生成、外观和优化特征均合理的候选池中，使观察者面对最高约 10^32 种组合；混淆图仍保留可供 ONNXRuntime 等工具发现的优化机会，并抵抗学习型识别攻击。
  - 相较加密整个模型导致编译器无法分析，或只匿名化算子名称，核心创新是在“隐藏原始结构”与“保留第三方图优化空间”之间建立可调的子图混淆机制。
  - 模型 IP 保护、计算图混淆、保密编译优化、模型窃取防御

- [QMoE: Sub-1-Bit Compression of Trillion Parameter Models](https://proceedings.mlsys.org/paper_files/paper/2024/hash/c74b624843218d9b6713fcf299d6d5e4-Abstract-Conference.html)
  - Institute of Science and Technology Austria；Elias Frantar、Dan Alistarh
  - QMoE 面向参数量极大但每 token 只激活少量 expert 的 MoE 推理，把 expert 权重压到平均 1 bit 以下，并用自定义编码格式和 GPU 解码 kernel 边解压边计算。1.6T 参数 SwitchTransformer-c2048 可由约 3.2 TB 缩到不足 160 GB，在单台 4×A6000 或 8×3090 服务器运行，压缩在单 GPU 一天内完成，推理额外开销低于 5%。
  - 相较通用 2/4-bit dense quantization，核心创新是为 trillion-scale MoE 的权重分布设计亚 1-bit 压缩算法，并与可直接执行该格式的 kernel 联合设计。
  - MoE 权重压缩、Sub-1-Bit Quantization、在线解码 Kernel、单机部署

- [vMCU: Coordinated Memory Management and Kernel Optimization for DNN Inference on MCUs](https://proceedings.mlsys.org/paper_files/paper/2024/hash/d5a655b8b373737b4f2aea8f78e5e754-Abstract-Conference.html)
  - Peking University、University of Washington、OctoAI；Size Zheng、Renze Chen、Meng Li 等
  - vMCU 针对只有数百 KB RAM 的 Cortex-M4/M7，把物理内存虚拟成由各算子共同使用的大 pool。每个 kernel 将输入、输出和 workspace 划为可加载/回写的 segment，并在计算过程中细粒度复用彼此不同时存活的空间，而不是先由全局 planner 固定整 tensor buffer；单层最高减少 49.5% RAM 和 53% 能耗，端到端把内存瓶颈降低 61.5%。
  - 相较内存 planner 与 kernel 独立、仅做 tensor 级 in-place reuse，核心创新是让 kernel 暴露 segment 生命周期，使跨 tensor 内存重叠可细化到算子内部。
  - TinyML 推理、MCU 内存虚拟化、Kernel-Memory 协同、Segment Streaming

- [UniDM: A Unified Framework for Data Manipulation with Large Language Models](https://proceedings.mlsys.org/paper_files/paper/2024/hash/dcb38c6ad7911842ab31081be9540b89-Abstract-Conference.html)
  - Alibaba Group、University of Science and Technology of China；Yichen Qian、Yongyi He、Rong Zhu 等
  - UniDM 将数据湖中的 entity matching、数据清洗等不同 manipulation task 归一为三阶段 LLM 流程，并为每阶段使用专门 prompt。系统从数据湖自动检索当前记录所需的 evidence 与事实上下文，再让同一框架执行多类任务，减少为每个任务重新收集标注、训练模型或手工编排规则；多组 benchmark 上展示跨任务泛化和领先结果。
  - 相较为每种数据处理任务分别设计 prompt、检索和后处理，核心创新是抽象统一任务表示与三阶段执行模板，使 context retrieval 和 LLM 推理可以跨任务复用。
  - LLM for Data Systems、数据清洗与匹配、自动上下文检索、统一任务 Pipeline

- [Efficient Post-training Quantization with FP8 Formats](https://proceedings.mlsys.org/paper_files/paper/2024/hash/dea9b4b6f55ae611c54065d6fc750755-Abstract-Conference.html)
  - Intel、AMD；Haihao Shen、Naveen Mellempudi、Xin He 等
  - 该工作系统比较 E5M2、E4M3、E3M4 三种 FP8 在 75 个 NLP、视觉和扩散网络上的 post-training quantization，分析 exponent range 与 mantissa precision 对各类算子的影响，并由此形成无需逐模型定制的量化 workflow。FP8 覆盖 92.64% 工作负载而 INT8 为 65.87%，其中 E4M3 更适合 NLP、E3M4 在视觉上略优。
  - 相较依据少数模型宣布某一 FP8 格式通用，核心创新是用大规模跨架构实证建立格式选择规则和统一 PTQ 流程，揭示不同任务的 range/precision 偏好。
  - FP8 Post-Training Quantization、跨工作负载评测、数据格式选择、模型部署

- [COMET: Neural Cost Model Explanation Framework](https://proceedings.mlsys.org/paper_files/paper/2024/hash/eb261df4322a8bd0a73093c4d8a0d02d-Abstract-Conference.html)
  - University of Illinois Urbana-Champaign、MIT CSAIL、VMware Research；Isha Chaudhary、Alex Renda、Charith Mendis、Gagandeep Singh
  - COMET 为输入 assembly basic block、输出 CPU 执行 cost 的 neural cost model 生成忠实且可泛化的解释。框架把预测关联到可理解的指令、依赖和微架构特征，并对比 Ithemal 与 simulation-based uiCA 的解释粒度；实验发现解释中缺失的细粒度特征与两类模型各自的预测误差相关，可用于诊断黑盒 cost model 为何失准。
  - 相较只用整体误差评价 neural cost model，核心创新是建立面向编译成本预测的专用解释框架，并用解释粒度连接预测错误与微架构因素。
  - 可解释编译成本模型、Assembly 性能预测、Neural Cost Model、微架构诊断

<a id="nas-latency-predictors"></a>

- [On Latency Predictors for Neural Architecture Search](https://proceedings.mlsys.org/paper_files/paper/2024/hash/f03cb785864596fa5901f1359d23fd81-Abstract-Conference.html)
  - Cornell University；Yash Akhauri、Mohamed Abdelfattah
  - 该工作研究 hardware-aware NAS 中如何用少量目标设备测量预测候选网络 latency。作者自动划分多设备集合构造困难 transfer task，系统比较 predictor architecture、网络样本选择、设备表示和算子编码，再给出端到端训练策略；在 12 个困难迁移任务中胜出 11 个，平均误差改善 22.5%，使 NAS wall-clock time 缩短 5.8 倍。
  - 相较在人工挑选的相似训练/测试设备上比较 predictor，核心创新是用原则化跨设备任务生成暴露泛化薄弱点，并联合验证模型、样本和硬件表示设计。
  - Hardware-Aware NAS、跨设备延迟预测、Transfer Learning、采样策略

<a id="flash"></a>

- [FLASH: Fast Model Adaptation in ML-Centric Cloud Platforms](https://proceedings.mlsys.org/paper_files/paper/2024/hash/f502981cbe221d857ad409450a7917c3-Abstract-Conference.html)
  - University of Illinois Urbana-Champaign、IBM Research；Haoran Qiu、Weichao Mao、Archit Patke 等
  - FLASH 服务使用 ML controller 管理资源配置、autoscaling 和 server power 的云平台。当应用、workload 或基础设施变化时，它复用既有控制器及训练数据，通过 meta-learning 学到跨环境初始化，再经统一 API 用少量新数据快速适配，而不是完全重训；三个系统管理任务中，对未见应用/环境的适配速度最高为 transfer learning 的 5.5 倍。
  - 相较为每个集群变化重新训练或直接微调单个 controller，核心创新是把多种既有 ML 管理 agent 的经验转化为可跨应用和基础设施迁移的元初始化。
  - ML for Systems—云资源控制、Meta-Learning、快速模型适配、Autoscaling
