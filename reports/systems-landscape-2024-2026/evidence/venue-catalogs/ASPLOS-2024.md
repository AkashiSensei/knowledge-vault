# ASPLOS 2024 论文列表

范围以 ASPLOS 2024 官方 Main Program 实际列出的论文为准，共 193 篇，跨越四个 ACM proceedings 父 DOI；已排除 workshop、tutorial、poster 与 keynote。以下标题均链接至论文 DOI；已找到的 4 份合法公开 PDF 保存在 `reference/ASPLOS/2024/`。

- [Explainable Port Mapping Inference with Sparse Performance Counters for AMD’s Zen Architectures](https://doi.org/10.1145/3620666.3651363)
  - Fabian Ritter and Sebastian Hack (Saarland University)。
  - 该工作面向 AMD Zen 处理器缺少 Intel 式端口性能计数器、难以建立指令到执行端口映射的问题，以形式化端口模型和 SMT 驱动的反例迭代，从有限计数器观测中推断映射，并分析硬件偏离模型时的精度边界。
  - 相较依赖完整端口计数器的 uops.info 流程，核心创新是在稀疏观测下把端口映射恢复转化为可解释的反例引导约束求解。
  - CPU 性能建模、AMD Zen、端口映射、SMT 求解、反例引导

- [Longnail: High-Level Synthesis of Portable Custom Instruction Set Extensions for RISC-V Processors from Descriptions in the Open-Source CoreDSL Language](https://doi.org/10.1145/3620666.3651375)
  - Julian Oppermann, Brindusa Mihaela Damian-Kosterhon, Florian Meisel, and Tammo Mürmann (Technical University of Darmstadt)；Eyck Jentzsch (MINRES Technologies GmbH)；Andreas Koch (Technical University of Darmstadt)。
  - Longnail 面向 RISC-V 嵌入式核的自定义指令扩展设计：开发者用 CoreDSL 描述指令行为，领域专用 HLS 编译器生成兼容 SCAIE-V 的硬件模块，再自动接入四类不同微结构的宿主核，覆盖多周期计算、访存、分支和解耦执行。
  - 相较为每个处理器核手工重写 ISAX，核心创新是把开放的行为级 ISA 描述、硬件生成和跨核接口集成为端到端可移植流程。
  - RISC-V、自定义指令扩展、CoreDSL、高层综合、跨微结构移植

- [SEER: Super-Optimization Explorer for High-Level Synthesis using E-graph Rewriting](https://doi.org/10.1145/3620665.3640392)
  - Jianyi Cheng (University of Cambridge and Intel)；Samuel Coward (Imperial College London and Intel)；Lorenzo Chelini, Rafael Barbalho, and Theo Drane (Intel)。
  - SEER 在将普通软件程序综合为硬件前，用 e-graph 同时保存大量等价程序，并编排 MLIR 软件变换与硬件优化器搜索更适合 HLS 的表达；其目标是在面积约束下自动逼近甚至超过专家手写的数据通路。
  - 相较固定顺序的 HLS pass，核心创新是把大规模等价重写空间显式化，并以 e-graph 支撑跨软件与硬件优化的 super-optimization。
  - 高层综合、E-graph、MLIR、Super-optimization、硬件设计空间搜索

- [HIDA: A Hierarchical Dataflow Compiler for High-Level Synthesis](https://doi.org/10.1145/3617232.3624850)
  - Hanchen Ye, Hyegang Jun, and Deming Chen (University of Illinois Urbana-Champaign)。
  - HIDA 将算法描述自动降为 FPGA 数据流实现，以分层 IR 表达任务、循环和算子间的数据流，再按层次分解庞大的设计空间，联合决定流水、并行和模块结构；在 PyTorch 神经网络上无需开发者手工探索即可生成高吞吐设计。
  - 相较扁平化搜索或依赖手工 pragma 的 HLS，核心创新是让表示层次与优化层次对应，从而使大型数据流设计可扩展地自动优化。
  - 高层综合、分层数据流、FPGA、自动设计空间探索、神经网络加速

- [TCCL: Discovering Better Communication Paths for PCIe GPU Clusters](https://doi.org/10.1145/3620666.3651362)
  - Heehoon Kim, Junyeol Ryu, and Jaejin Lee (Seoul National University)。
  - TCCL 面向主要经 PCIe 通信、没有 NVLink 等专用互连的多 GPU 集群，先实测并发传输组合的带宽，再由 pathfinder 为 AllReduce/AllGather 搜索环形路径，最后通过修改 NCCL runtime 执行这些路径；它同时考虑 PCIe 拓扑和多传输相互干扰。
  - 相较沿用 NCCL/MSCCL 的通用路径，核心创新是以多传输实测画像驱动 PCIe 集群的 collective 路径发现，而非只按静态拓扑选路。
  - 分布式训练、PCIe GPU 集群、Collective Communication、路径搜索、NCCL

- [Centauri: Enabling Efficient Scheduling for Communication-Computation Overlap in Large Model Training via Communication Partitioning](https://doi.org/10.1145/3620666.3651379)
  - Chang Chen, Xiuhong Li, and Qianchao Zhu (Peking University)；Jiangfei Duan (Chinese University of Hong Kong)；Peng Sun and Xingcheng Zhang (Shanghai AI Lab)；Chao Yang (Peking University)。
  - Centauri 面向采用数据、张量与流水等混合并行的大模型训练，把 collective 从原语替换、拓扑分组和工作量三个维度切分，再在 operation、layer、model 三层共同调度切分后的通信与计算，使不同拓扑和并行配置下的通信空洞被计算覆盖。
  - 相较只做 kernel fusion 或在少数算子间重排，核心创新是同时扩大 communication partition space 与 scheduling scope，系统搜索跨层、跨模型的重叠机会。
  - LLM 训练、混合并行、通信切分、计算通信重叠、分层调度

- [T3: Transparent Tracking & Triggering for Fine-grained Overlap of Compute & Collectives](https://doi.org/10.1145/3620665.3640410)
  - Suchita Pati (University of Wisconsin-Madison and AMD)；Shaizeen Aga, Mahzabeen Islam, and Nuwan Jayasena (AMD)；Matthew D. Sinclair (University of Wisconsin-Madison and AMD)。
  - T3 针对张量并行中生产者算子与 collective 串行的问题，通过配置输出地址空间把生产者写入与后续通信透明融合；硬件侧 track-and-trigger 机制在数据片段就绪时触发传输，并由具计算能力的内存承担通信辅助计算，以减轻与 GEMM 的资源争用。
  - 相较软件显式切碎 kernel 和通信，核心创新是用轻量硬件跟踪数据就绪并自动触发 collective，使细粒度重叠对模型代码近乎透明。
  - LLM 训练与推理、张量并行、Collective、硬件软件协同、细粒度重叠

- [Two-Face: Combining Collective and One-Sided Communication for Efficient Distributed SpMM](https://doi.org/10.1145/3620665.3640427)
  - Charles Block, Gerasimos Gerogiannis, and Charith Mendis (University of Illinois at Urbana-Champaign)；Ariful Azad (Indiana University)；Josep Torrellas (University of Illinois at Urbana-Champaign)。
  - Two-Face 面向分布式 SpMM 中全量 collective 传输冗余、逐元素 one-sided 访问又开销过高的两难，按稀疏矩阵局部密度把通信划为稠密区和稀疏区：前者使用 collective，后者只拉取必要数据，在 4096 核平台上兼顾带宽利用和软件开销。
  - 相较全局只选一种通信方式，核心创新是依据同一矩阵内部的密度差异，在一次 SpMM 中组合 collective 与细粒度单边通信。
  - 分布式 SpMM、稀疏矩阵、Collective、One-sided Communication、通信分区

- [A Quantitative Analysis and Guidelines of Data Streaming Accelerator in Modern Intel Xeon Scalable Processors](https://doi.org/10.1145/3620665.3640401)
  - Reese Kuper (University of Illinois at Urbana Champaign)；Ipoom Jeong (University of Illinois Urbana-Champaign)；Yifan Yuan, Ren Wang, Narayan Ranganathan, and Nikhil Rao (Intel Labs)；Jiayu Hu (Tencent)；Sanjay Kumar and Philip Lantz (Intel Labs)；Nam Sung Kim (University of Illinois Urbana-Champaign)。
  - 该研究系统测量 Intel Sapphire Rapids 的 Data Streaming Accelerator，覆盖内存搬移、CRC、delta 与 DIF 等操作，并从队列配置、批量大小、NUMA 和软件栈等层面给出使用边界；DPDK Vhost 案例说明何时把数据路径卸载给 DSA 才能获得吞吐收益。
  - 相较只给出峰值微基准，核心贡献是把 DSA 的硬件特性、软件接口和真实数据中心用例连成可操作的部署指南。
  - Intel DSA、数据搬移卸载、Sapphire Rapids、DPDK Vhost、生产性能分析

- [Thesios: Synthesizing Accurate Counterfactual I/O Traces from I/O Samples](https://doi.org/10.1145/3620666.3651337)
  - Phitchaya Mangpo Phothilimthana (Google DeepMind)；Saurabh Kadekodi (Google)；Soroush Ghodrati (University of California San Diego)；Selene Moon (Google)；Martin Maas (Google DeepMind)。
  - Thesios 从 Google 多服务器、多磁盘的低频采样 I/O trace 合成完整分辨率的反事实 trace，在保留请求数、利用率与延迟分布的同时，可离线模拟容量、数据放置、磁盘转速和 buffer cache 改动，避免直接在生产存储上做高风险 A/B 实验。
  - 相较按比例放大单盘采样，核心创新是有约束地组合多盘采样，使合成 trace 能回答尚未部署的硬件与策略“如果改变会怎样”。
  - 存储系统、I/O Trace 合成、反事实分析、Google 生产负载、容量规划

- [A Journey of a 1,000 Kernels Begins with a Single Step: A Retrospective of Deep Learning on GPUs](https://doi.org/10.1145/3620665.3640367)
  - Michael Davies, Ian McDougall, Selvaraj Anandaraj, Deep Machchhar, Rithik Jain, and Karthikeyan Sankaralingam (University of Wisconsin-Madison)。
  - 该研究构建 CaSiO 套件，纵向追踪视觉、物理模拟、生成、语言、语音与表格等生产风格 AI 应用在三代 GPU 上的框架调用、设备 API、kernel 和微结构行为，用来揭示 MLPerf 偏重 CNN 时遗漏的算子多样性与硬件利用变化。
  - 相较以少数静态 benchmark 代表 AI，核心创新是以约千个 kernel 的跨代、跨层测量还原深度学习软件与 GPU 演进的真实轨迹。
  - AI 工作负载测量、GPU 微结构、Kernel 多样性、CaSiO、跨代分析

- [Expanding Datacenter Capacity with DVFS Boosting: A safe and scalable deployment experience](https://doi.org/10.1145/3617232.3624853)
  - Leonardo Piga, Iyswarya Narayanan, Aditya Sundarrajan, Matt Skach, and Qingyuan Deng (Meta)；Biswadip Maity (University of California Irvine)；Manoj Chakkaravarthy, Alison Huang, Abhishek Dhanotia, and Parth Malani (Meta)。
  - 该生产系统在 Meta 数据中心按服务与硬件类型选择安全的 CPU DVFS boost，并把额外功耗、机房 oversubscription、power capping、长尾小服务和可靠性纳入分阶段验证与回滚；三年部署由既有服务器释放约 12 MW 等效算力容量。
  - 相较单机追求最高频率，核心创新是把 DVFS 提频变成 fleet-level 容量工程，以功率预算和服务风险共同约束每次提升。
  - 数据中心容量、DVFS Boosting、功率超卖、Meta 生产部署、可靠性

- [Rubix: Reducing the Overhead of Secure Rowhammer Mitigations via Randomized Line-to-Row Mapping](https://doi.org/10.1145/3620665.3640404)
  - Anish Saxena, Saurav Mathur, and Moinuddin Qureshi (Georgia Tech)。
  - Rubix 面向低 Rowhammer 阈值下 AQUA、SRS、Blockhammer 因大量正常 hot row 被频繁缓解而严重降速的问题，用加密地址把相邻 cache line 随机映射到不同 DRAM row，并以 1–4 条 line 为组保留部分 row-buffer locality；Rubix-D 还动态更换映射增加攻击者学习难度。
  - 相较进一步优化每次缓解动作，核心创新是先随机化 line-to-row 映射，从源头把正常应用的 hot row 数量降低数个数量级。
  - Rowhammer、防御、地址随机化、DRAM、Row-buffer Locality

- [TAROT: A CXL SmartNIC-Based Defense Against Multi-bit Errors by Row-Hammer Attacks](https://doi.org/10.1145/3620666.3651325)
  - Chihun Song (University of Illinois Urbana-Champaign)；Michael Jaemin Kim (Seoul National University)；Tianchen Wang, Houxiang Ji, Jinghan Huang, and Ipoom Jeong (University of Illinois Urbana-Champaign)；Jaehyun Park, Hwayong Nam, Minbok Wi, and Jung Ho Ahn (Seoul National University)；Nam Sung Kim (University of Illinois Urbana-Champaign)。
  - TAROT 利用长期实测发现多比特 Rowhammer 不可纠错错误集中在极少数物理地址，启动时识别这些 RH-UE-vulnerable 地址并周期性访问防止错误累积；H-TAROT 在主 CPU 执行，S-TAROT 则经 CXL SmartNIC 卸载扫描以保护 Redis 等尾延迟敏感服务。
  - 相较刷新所有邻近行，核心创新是只治疗经器件画像确认的脆弱地址，并把保护流量卸载到 SmartNIC 隔离主机干扰。
  - Rowhammer、多比特错误、CXL SmartNIC、脆弱地址画像、主动刷新

- [Pythia: Compiler-Guided Defense Against Non-Control Data Attacks](https://doi.org/10.1145/3620666.3651343)
  - Sharjeel Khan, Bodhisatwa Chatterjee, and Santosh Pande (Georgia Tech)。
  - Pythia 防御通过篡改非控制数据来翻转分支的 control-flow bending：编译器对输入可影响变量的 forward slice 和关键分支变量的 backward slice 做风险筛选，对静态对象插入 ARM Pointer Authentication canary，对动态对象放入受保护区，避免保护全部变量的高开销。
  - 相较 CFI 只约束间接跳转或 DFI 全量跟踪，核心创新是以程序切片定位必须保护的数据，并复用 ARM PA 做选择性的运行时完整性验证。
  - 非控制数据攻击、Control-flow Bending、ARM Pointer Authentication、程序切片、编译器防御

- [Everywhere All at Once: Co-Location Attacks on Public Cloud FaaS](https://doi.org/10.1145/3617232.3624867)
  - Zirui Neil Zhao (University of Illinois Urbana-Champaign)；Adam Morrison (Tel Aviv University)；Christopher W. Fletcher and Josep Torrellas (University of Illinois Urbana-Champaign)。
  - 该工作研究公共 FaaS 中攻击者如何与受害函数落到同一物理机，设计两种 host fingerprint 和低成本大规模共置验证方法，测量 Google Cloud Run 的实例放置行为，并据此制定批量启动策略，在多个数据中心显著提高跨租户共置概率。
  - 相较假设攻击者已与受害者共置，核心创新是把动态、短生命周期且受 VPC 隔离的 FaaS 共置本身做成可复现的端到端攻击阶段。
  - 公共云安全、FaaS、跨租户共置、Host Fingerprinting、侧信道前置条件

- [Plankton: Reconciling Binary Code and Debug Information](https://doi.org/10.1145/3620665.3640382)
  - Anshunkang Zhou and Chengfeng Ye (The Hong Kong University of Science and Technology)；Heqing Huang (City University of Hong Kong)；Yuandao Cai and Charles Zhang (The Hong Kong University of Science and Technology)。
  - Plankton 在不改构建流程的前提下，把带 debug information 的二进制提升为可供静态分析的 LLVM IR；两套恢复算法弥合机器指令与源级变量/类型之间的信息缺口，使缺陷检测结果接近编译期插桩方案。
  - 相较现有 binary lifter 即使有调试信息仍生成低精度 IR，核心创新是系统协调二进制事实与 debug 元数据，而非盲目信任任一侧。
  - 二进制提升、LLVM IR、调试信息、静态分析、缺陷检测

- [What You Trace is What You Get: Dynamic Stack-Layout Recovery for Binary Recompilation](https://doi.org/10.1145/3620665.3640371)
  - Fabian Parzefall, Chinmay Deshpande, Felicitas Hetzelt, and Michael Franz (University of California Irvine)。
  - WYTIWYG 面向无源码的遗留或商业二进制，通过多轮插桩与动态分析恢复函数局部变量和栈布局，再提升到编译器 IR 进行重新优化；恢复只承诺用户给定输入上的行为，并以重编译后性能检验 IR 质量。
  - 相较启发式或保守过近似栈恢复，核心创新是把局部变量识别分解为一组可观测的动态分析步骤，用执行 trace 换取可优化的精确布局。
  - 二进制重编译、动态分析、栈布局恢复、遗留软件优化、Instrumentation

- [Accurate Disassembly of Complex Binaries Without Use of Compiler Metadata](https://doi.org/10.1145/3623278.3624766)
  - Soumyakant Priyadarshan, Huan Nguyen, and R. Sekar (Stony Brook University)。
  - 该反汇编器针对 stripped x86 中代码与内嵌数据难区分、又没有 relocation/exception metadata 的情况，一边用数据的统计特征识别疑似代码，一边用指令行为约束发现误判数据，再以优先级错误修正统一两类证据。
  - 相较假设不存在内嵌数据或依赖编译器元数据，核心创新是把 data-driven 概率证据与 code-driven 静态约束双向结合。
  - 二进制反汇编、Stripped Binary、代码数据区分、概率分析、错误修正

- [FITS: Inferring Intermediate Taint Sources for Effective Vulnerability Analysis of IoT Device Firmware](https://doi.org/10.1145/3623278.3624759)
  - Puzhuo Liu (Chinese Academy of Sciences)；Yaowen Zheng (Nanyang Technological University)；Chengnian Sun (University of Waterloo)；Chuan Qin, Dongliang Fang, Mingdong Liu, and Limin Sun (Chinese Academy of Sciences)。
  - FITS 面向大型闭源 IoT firmware 中从网络库 source 到危险 sink 的 taint path 过长问题，以静态和动态行为特征表示无符号函数，经聚类与相似度排序自动找出可作为中间 taint source 的自定义函数，再从这些位置启动 Karonte 等分析器缩短路径。
  - 相较人工标注或只能识别标准库 source，核心创新是学习函数行为来推断 firmware-specific 的中间污点入口，从而扩展漏洞覆盖。
  - IoT 固件安全、污点分析、中间 Taint Source、二进制行为特征、漏洞发现

- [Avoiding Instruction-Centric Microarchitectural Timing Channels Via Binary-Code Transformations](https://doi.org/10.1145/3620665.3640400)
  - Michael Flanders, Reshabh K Sharma, Alexandra E. Michael, Dan Grossman, and David Kohlbrenner (University of Washington)。
  - cio 针对 silent store 和 computation simplification 等尚未普及、但会泄漏操作数的指令级微结构优化，在二进制层检测密码代码中可能被 shortcut 的 store、算术和复杂指令 micro-op，并自动改写为不产生数据相关时序的等价序列。
  - 相较源级 constant-time 规则，核心创新是从最终指令及其隐含 micro-op 出发，为新出现的 instruction-centric channel 生成可验证缓解。
  - 微结构侧信道、二进制变换、Constant-time、Silent Store、密码实现

- [Last-Level Cache Side-Channel Attacks Are Feasible in the Modern Public Cloud](https://doi.org/10.1145/3620665.3640403)
  - Zirui Neil Zhao (University of Illinois Urbana-Champaign)；Adam Morrison (Tel Aviv University)；Christopher W. Fletcher and Josep Torrellas (University of Illinois Urbana-Champaign)。
  - 该工作在有其他租户噪声且 FaaS 执行窗口很短的 Google Cloud Run 上完成跨租户 LLC 攻击：L2 过滤与二分剪枝加速 eviction set 构造，parallel probing 提高时间分辨率，再用功率谱密度从噪声中定位受害 cache set，最终恢复 ECDSA nonce 信息。
  - 相较只在安静本机环境演示 cache attack，核心创新是把共置、快速 eviction-set、并行探测和频域降噪整成真实公共云端到端链路。
  - LLC 侧信道、公共 FaaS、跨租户攻击、Eviction Set、ECDSA

- [Pathfinder: High-Resolution Control-Flow Attacks Exploiting the Conditional Branch Predictor](https://doi.org/10.1145/3620666.3651382)
  - Hosein Yavarzadeh and Archit Agarwal (University of California San Diego)；Max Christman (University of North Carolina at Chapel Hill)；Christina Garman (Purdue University)；Daniel Genkin (Georgia Tech)；Andrew Kwong (University of North Carolina at Chapel Hill)；Daniel Moghimi (Google)；Deian Stefan (University of California San Diego)；Kazem Taram (Purdue University)；Dean Tullsen (University of California San Diego)。
  - Pathfinder 构造对条件分支预测器 PHR/PHT 的读写原语：读原语可重建受害程序完整控制流并恢复 libjpeg 处理的秘密图像，写原语可精确污染预测历史，形成提取 AES 中间值的高分辨率 transient attack。
  - 相较只推断单个分支结果，核心创新是把条件分支预测器的路径历史变成可读写状态，从而同时支持控制流观测与主动操纵。
  - 分支预测器攻击、Path History Register、Transient Execution、控制流泄漏、AES

- [Pentimento: Data Remanence in Cloud FPGAs](https://doi.org/10.1145/3620665.3640355)
  - Colin Drewes (Stanford University)；Olivia Weng and Andres Meza (University of California San Diego)；Alric Althoff (ARM)；David Kohlbrenner (University of Washington)；Ryan Kastner (University of California San Diego)；Dustin Richmond (University of California Santa Cruz)。
  - Pentimento 发现 FPGA 配置长期运行造成的晶体管老化会留下可测时序痕迹；后续云租户可在 AWS F1 上用 time-to-digital converter 读取这种 data remanence，从已撤下的 Marketplace bitstream 推断设计或密钥，也可恢复前一租户的信息。
  - 相较只考虑 SRAM 配置清除，核心创新是识别并利用 bias-temperature-instability 形成的模拟“残影”，证明重配置后仍存在跨租户泄漏。
  - 云 FPGA、数据残留、BTI 老化、Time-to-Digital Converter、跨租户泄漏

- [Kimbap: A Node-Property Map System for Distributed Graph Analytics](https://doi.org/10.1145/3620665.3640421)
  - Hochan Lee (University of Texas at Austin)；Roshan Dathathri (Microsoft Research)；Keshav Pingali (University of Texas at Austin)。
  - Kimbap 支持顶点读写图中任意节点的 property，而不局限于邻居，因此可表达 Louvain、Shiloach–Vishkin 等一般 vertex-centric 算法；编译器自动生成通信，runtime 用分区感知的稀疏 node-property map 组织并发 reduction 并避免线程冲突。
  - 相较 Pregel 式一般顶点程序的共享 map 瓶颈，核心创新是为跨邻接访问专门设计可扩展的分布式 property map 与自动通信生成。
  - 分布式图计算、Node-Property Map、Vertex-centric、稀疏归约、Louvain

- [TrackFM: Far-out Compiler Support for a Far Memory World](https://doi.org/10.1145/3617232.3624856)
  - Brian R. Tauro (Illinois Institute of Technology)；Brian Suchy, Simone Campanoni, and Peter Dinda (Northwestern University)；Kyle C. Hale (Illinois Institute of Technology)。
  - TrackFM 通过编译器分析远内存对象的访问与局部性，自动插入数据获取、预取和 runtime 协同代码；应用只需重编译，即可获得接近显式 far-memory library 的性能，同时保持 kernel paging 方案的透明性。
  - 相较在“内核透明但慢”和“库高效但侵入”之间二选一，核心创新是以编译期语义把远内存访问显式化而不改源程序。
  - 远内存、内存解耦、编译器变换、透明数据获取、运行时协同

- [Scaling Up Memory Disaggregated Applications with SMART](https://doi.org/10.1145/3617232.3624857)
  - Feng Ren, Mingxing Zhang, and Kang Chen (Tsinghua University)；Huaxia Xia (Meituan)；Zuoning Chen (Chinese Academy of Engineering)；Yongwei Wu (Tsinghua University)。
  - SMART 面向 RDMA 解耦内存应用在多核下受 doorbell 争用、过多 outstanding request 污染 cache、CAS 失败浪费 IOPS 的问题，在类似 one-sided verb 的接口下自动批处理与节流请求，并优化原子重试；RACE、FORD 和 Sherman 只需少量改动即可扩到更多核心。
  - 相较让每个应用各自调 RNIC 细节，核心创新是把三类 RNIC scale-up 瓶颈封装为通用编程框架，并对 IOPS-bound 访问统一治理。
  - 内存解耦、RDMA、RNIC、Many-core Scalability、One-sided Verb

- [CC-NIC: a Cache-Coherent Interface to the NIC](https://doi.org/10.1145/3617232.3624868)
  - Henry N. Schuh and Arvind Krishnamurthy (Google and University of Washington)；David Culler (Google)；Henry M. Levy (Google and University of Washington)；Luigi Rizzo (Google)；Samira Khan (Google and University of Virginia)；Brent E. Stephens (Google and University of Utah)。
  - CC-NIC 面向 NIC 通过一致性互连进入 CPU cache hierarchy 的新硬件，重新设计 host–NIC 队列、信号和数据结构，使包描述符不再产生多余 coherence traffic 或长期占 cache；模型基于 Ice Lake/Sapphire Rapids UPI，目标是降低延迟同时节省主机核。
  - 相较把 PCIe NIC 接口原样映射到 coherent link，核心创新是从 cache-line 所有权和一致性事件出发重构主机与 NIC 的交互协议。
  - Cache-Coherent NIC、一致性互连、Host-NIC Interface、低延迟网络、UPI

- [SpecInfer: Accelerating Large Language Model Serving with Tree-based Speculative Inference and Verification](https://doi.org/10.1145/3620666.3651335)
  - Xupeng Miao, Gabriele Oliaro, Zhihao Zhang, Xinhao Cheng, and Zeyu Wang (Carnegie Mellon University)；Zhengxin Zhang (Tsinghua University)；Rae Ying Yee Wong (Stanford University)；Alan Zhu and Lijie Yang (Carnegie Mellon University)；Xiaoxiang Shi (Shanghai Jiao Tong University)；Chunan Shi (Peking University)；Zhuoming Chen and Daiyaan Arfeen (Carnegie Mellon University)；Reyna Abhyankar (University of California San Diego)；Zhihao Jia (Carnegie Mellon University)。
  - SpecInfer 用多个小 speculative model 为一次请求产生若干候选 continuation，并组织成共享前缀的 token tree；大 LLM 不再逐 token 解码，而以 tree-based parallel decoding 一次验证多条候选路径，只接受与原模型分布一致的部分，因此在不降低生成质量下减少串行步数。
  - 相较线性 speculative decoding 一次只验证一条草稿，核心创新是把多模型、多序列预测合并为 token tree 并行验证。
  - LLM Serving、Speculative Decoding、Token Tree、并行验证、低延迟推理

- [ExeGPT: Constraint-Aware Resource Scheduling for LLM Inference](https://doi.org/10.1145/3620665.3640383)
  - Hyungjun Oh, Kihong Kim, Jaemin Kim, Sungkyun Kim, and Junyeol Lee (Hanyang University)；Du-seong Chang (KT Corporation)；Jiwon Seo (Hanyang University)。
  - ExeGPT 面向 T5、OPT、GPT-3 等自回归与编码器—解码器模型，根据线上输入/输出序列长度分布，在给定 latency constraint 下搜索 batch size、partial tensor parallelism 和 stage 资源；round-robin 或 workload-aware 策略按任务分布选择 schedule，并在分布变化时低成本重配。
  - 相较固定 batch 与固定张量并行，核心创新是把序列长度分布显式纳入执行计划搜索，直接求解吞吐最大化且延迟受限的资源配置。
  - LLM 推理、约束感知调度、序列长度分布、Partial Tensor Parallelism、Batch Size

- [Proteus: A High-Throughput Inference-Serving System with Accuracy Scaling](https://doi.org/10.1145/3617232.3624849)
  - Sohaib Ahmad and Hui Guan (University of Massachusetts Amherst)；Brian D. Friedman and Thomas Williams (Nokia Bell Labs)；Ramesh K. Sitaraman (University of Massachusetts Amherst)；Thomas Woo (Nokia Bell Labs)。
  - Proteus 面向硬件数量固定的 edge cluster 或 private cloud，在负载升高时不只扩机器，而是联合选择不同精度/大小的模型 variant、把它们放到异构设备并路由请求；adaptive batching 再根据到达波动减少 SLO timeout，在吞吐约束下最大化总体准确率。
  - 相较仅做 hardware autoscaling，核心创新是把 accuracy scaling 作为一等资源旋钮，并将模型选择、放置、请求分配和 batching 联合优化。
  - 推理服务、Accuracy Scaling、异构设备、模型放置、Adaptive Batching

- [SpotServe: Serving Generative Large Language Models on Preemptible Instances](https://doi.org/10.1145/3620665.3640411)
  - Xupeng Miao (Carnegie Mellon University)；Chunan Shi (Peking University)；Jiangfei Duan (The Chinese University of Hong Kong)；Xiaoli Xi (Carnegie Mellon University)；Dahua Lin (Chinese University of Hong Kong and Sensetime Research)；Bin Cui (Peking University)；Zhihao Jia (Carnegie Mellon University)。
  - SpotServe 用云端 preemptible GPU 降低生成式 LLM serving 成本：根据可用实例和流量动态改变模型并行配置，以二分图匹配复用旧分片、最小化 reparallelization 迁移；在回收宽限期细粒度提交 decoding 状态，使中断请求能从已生成进度继续。
  - 相较在 spot 实例消失后从头加载和重算，核心创新是联合动态并行重构、最小代价迁移与 stateful inference recovery。
  - LLM Serving、抢占式 GPU、动态重并行、状态恢复、成本优化

- [Flexible Non-intrusive Dynamic Instrumentation for WebAssembly](https://doi.org/10.1145/3620666.3651338)
  - Ben L. Titzer, Elizabeth Gilbert, Bradley Wei Jie Teo, Yash Anand, Kazuyuki Takayama, and Heather Miller (Carnegie Mellon University)。
  - Wizard 为 WebAssembly 引擎提供可运行时插入/移除的分层 probe，代码覆盖、频率、trace 与 debugger 可由低层 bytecode probe 组合；它复用引擎已有 interpreter、JIT 与 deoptimization，并保证多个分析同时启用时的一致性，未启用 probe 时不进入生产关键路径。
  - 相较模拟器或机器码插桩，核心创新是在 Wasm bytecode 层建立可编程、可组合且支持多 tier 执行的非侵入动态 instrumentation。
  - WebAssembly、动态插桩、JIT、Deoptimization、运行时观测

- [ShapleyIQ: Influence Quantification by Shapley Values for Performance Debugging of Microservices](https://doi.org/10.1145/3623278.3624771)
  - Ye Li, Jian Tan, Bin Wu, Xiao He, and Feifei Li (Alibaba)。
  - ShapleyIQ 在微服务 causal graph 上量化每个异常组件对端到端指标的边际影响，以 splitting invariance 将指数级 Shapley 计算分解为可在线执行的子问题；服务已在阿里云 86 个服务、2546 台机器上运行，用影响排序指导不同修复动作。
  - 相较只给出异常相关性或单一 root cause，核心创新是用可分解的因果 Shapley value 对多个并发异常逐一归因并量化影响。
  - 微服务诊断、Shapley Value、因果图、根因分析、阿里云生产系统

- [Loupe: Driving the Development of OS Compatibility Layers](https://doi.org/10.1145/3617232.3624861)
  - Hugo Lefeuvre (University of Manchester)；Gaulthier Gain (University of Liege)；Vlad-Andrei Bădoiu and Daniel Dinca (University Politehnica of Bucharest)；Vlad-Radu Schiller (University of Manchester)；Costin Raiciu (University Politehnica of Bucharest)；Felipe Huici (Unikraft.io)；Pierre Olivier (University of Manchester)。
  - Loupe 动态运行目标应用及其代表 workload，记录哪些 system call/OS feature 真正影响正确执行，并用 stub、fake 或完整实现试验区分必要语义；它据应用覆盖收益给兼容层开发排序，避免静态分析把可达但不会影响 workload 的接口全部列为必须实现。
  - 相较凭 Linux syscall 清单推进新 OS 兼容层，核心创新是以 workload-guided 动态实验量化“最小可用 OS surface”。
  - 操作系统兼容层、System Call、动态分析、功能优先级、Workload-guided Development

- [Amanda: Unified Instrumentation Framework for Deep Neural Networks](https://doi.org/10.1145/3617232.3624864)
  - Yue Guan, Yuxian Qiu, and Jingwen Leng (Shanghai Jiao Tong University and Shanghai Qi Zhi Institute)；Fan Yang (Microsoft Research)；Shuo Yu (Shanghai Jiao Tong University)；Yunxin Liu (Tsinghua University)；Yu Feng and Yuhao Zhu (University of Rochester)；Lidong Zhou (Microsoft Research)；Yun Liang (Peking University)；Chen Zhang, Chao Li, and Minyi Guo (Shanghai Jiao Tong University)。
  - Amanda 把 tracing、profiling、pruning、quantization 等任务统一表述为 DNN operator instrumentation，对 TensorFlow/PyTorch 和 graph/eager mode 暴露同一用户 API；内部 callback API 协调原算子与插桩代码的执行、缓存和复用，通常把额外开销控制在 5% 内。
  - 相较为每个 backend 和任务维护独立 hook，核心创新是以算子级 instrumentation 抽象跨框架复用分析与优化工具。
  - DNN Instrumentation、TensorFlow、PyTorch、Tracing、模型优化框架

- [GIANTSAN: Efficient Memory Sanitization with Segment Folding](https://doi.org/10.1145/3620665.3640391)
  - Hao Ling (The Hong Kong University of Science and Technology)；Heqing Huang (City University of Hong Kong)；Chengpeng Wang, Yuandao Cai, and Charles Zhang (The Hong Kong University of Science and Technology)。
  - GiantSan 用 folded segment 概括连续、拥有相同 shadow metadata 的内存区域，使一份编码保护更多字节，减少每次 load/store 额外读取 metadata 的次数；它保持 location-based sanitizer 的兼容性，同时降低 ASan 式稀疏保护密度带来的运行开销。
  - 相较为固定小粒度内存逐块存 shadow，核心创新是对相邻同质 metadata 做可快速查询的段折叠，在保护精度和 metadata 流量间取得更优平衡。
  - 内存安全、Sanitizer、Shadow Metadata、Segment Folding、ASan

- [Enforcing C/C++ Type and Scope at Runtime for Control-Flow and Data-Flow Integrity](https://doi.org/10.1145/3620666.3651342)
  - Mohannad Ismail and Christopher Jelesnianski (Virginia Tech)；Yeongjin Jang (Samsung Research America)；Changwoo Min (Igalia)；Wenjie Xiong (Virginia Tech)。
  - STI 从源码收集每个代码/数据指针的声明类型、作用域和权限，RSTI 在运行时用 ARM Pointer Authentication 验证指针是否仍按原意使用；三种机制在覆盖强度、metadata 与开销间提供不同权衡，既约束控制流指针也约束数量庞大的数据指针。
  - 相较只保护返回地址或 indirect branch，核心创新是把 programmer intent 形式化为 scope-type integrity，并用现成 PA 硬件统一执行控制流和数据流约束。
  - C/C++ 指针安全、Scope-Type Integrity、ARM PA、Data-oriented Attack、CFI

- [Lightweight Fault Isolation: Practical, Efficient, and Secure Software Sandboxing](https://doi.org/10.1145/3620665.3640408)
  - Zachary Yedidia (Stanford University)。
  - LFI 在单一 ARM64 address space 内用指令重写和小型静态 verifier 隔离数万个 4 GiB sandbox，对 load、store 和 jump 全部限制目标范围；它独立于特定编译器，支持异常、SIMD 等常见语义，并加入基本 Spectre hardening，适合低启动/切换成本的 cloud 与 serverless code。
  - 相较依赖进程/VM 或庞大编译器 TCB 的 sandbox，核心创新是用可验证的最小 ARM64 重写规则同时获得多 sandbox 密度、广泛软件兼容和低开销。
  - Software Fault Isolation、ARM64、Serverless Sandbox、静态验证器、小型 TCB

- [FreePart: Hardening Data Processing Software via Framework-based Partitioning and Isolation](https://doi.org/10.1145/3623278.3624760)
  - Ali Ahad (University of Virginia)；Gang Wang (University of Illinois at Urbana-Champaign)；Chung Hwan Kim (University of Texas at Dallas)；Suman Jana (Columbia University)；Zhiqiang Lin (Ohio State University)；Yonghwi Kwon (University of Virginia)。
  - FreePart 保护依赖 TensorFlow、PyTorch、OpenCV、Caffe 的数据处理应用，以 framework API 调用及其数据对象划分执行阶段，在调用边界临时隔离敏感对象和框架代码；分区依据运行时数据访问而非分析整个复杂应用依赖图。
  - 相较通用静态 compartmentalization，核心创新是利用框架 API 天然揭示数据生命周期，以低分析成本自动形成 temporal partition。
  - 软件隔离、ML Framework、安全分区、Framework API、数据生命周期

- [DREAM: A Dynamic Scheduler for Dynamic Real-time Multi-model ML Workloads](https://doi.org/10.1145/3623278.3624753)
  - Seah Kim (University of California Berkeley)；Hyoukjun Kwon (University of California Irvine)；Jinook Song, Jihyuck Jo, Yu-Hsin Chen, Liangzhen Lai, and Vikas Chandra (Meta)。
  - DREAM 面向 AR/VR、无人机等实时 multi-model inference，负载会在 task、model 和 layer 三个粒度动态变化；调度器把 deadline、模型异构性、当前 accelerator 负载和同一输入帧上的其他推理量化为分数，借可调参数快速重新选择设备和执行顺序。
  - 相较假设模型集合与到达率稳定的 inference scheduler，核心创新是统一刻画多层动态性，并以面向用户体验的 UXCost 驱动在线适配。
  - 实时多模型推理、异构加速器、动态调度、AR/VR、UXCost

- [SoCFlow: Efficient and Scalable DNN Training on SoC-Clustered Edge Servers](https://doi.org/10.1145/3617232.3624847)
  - Daliang Xu (Peking University)；Mengwei Xu (State Key Laboratory of Networking and Switching Technology)；Chiheng Lou (Peking University)；Li Zhang (State Key Laboratory of Networking and Switching Technology)；Gang Huang, Xin Jin, and Xuanzhe Liu (Peking University)。
  - SoCFlow 利用边缘 SoC cluster 在潮汐业务间隙训练 DNN，以 group-wise parallelism 把设备分组并延迟梯度聚合，降低弱网络瓶颈；数据并行 mixed-precision 算法再同时使用移动 SoC 内异构 CPU/GPU/NPU 能力，在相同功耗预算下提高闲置算力利用。
  - 相较把手机 SoC 简单当作低速 GPU worker，核心创新是围绕其弱互连和异构计算单元重构同步与数值精度策略。
  - 边缘训练、SoC Cluster、分组并行、延迟聚合、混合精度

- [Training Job Placement in Clusters with Statistical In-Network Aggregation](https://doi.org/10.1145/3617232.3624863)
  - Bohan Zhao and Wei Xu (Tsinghua University)；Shuo Liu, Yang Tian, and Qiaoling Wang (Huawei)；Wenfei Wu (Peking University)。
  - NetPack 面向共享 programmable switch memory 的 statistical in-network aggregation 集群，周期性批量处理训练 job，估计 GPU、链路和交换机聚合状态，为 server 组合按计算/带宽余量计分，再用动态规划寻找兼顾两类资源的 placement。
  - 相较只按 GPU locality 放置训练，核心创新是把统计复用下会随并发作业变化的 INA capacity 作为跨层放置资源共同优化。
  - 分布式训练、In-Network Aggregation、作业放置、GPU 集群、交换机内存

- [RAP: Resource-aware Automated GPU Sharing for Multi-GPU Recommendation Model Training and Input Preprocessing](https://doi.org/10.1145/3620665.3640406)
  - Zheng Wang (University of California San Diego)；Yuke Wang and Jiaqi Deng (University of California Santa Barbara)；Da Zheng (Amazon)；Ang Li (Pacific Northwest National Laboratory)；Yufei Ding (University of California San Diego)。
  - RAP 面向持续重训推荐模型时 CPU 预处理集群功耗过高的问题，把 input preprocessing 与多 GPU DLRM training 共置；cost model 预测预处理算子侵占的 GPU 资源，resource-aware horizontal fusion 只在空闲算力上合并小 kernel，搜索 graph mapping 与并行 schedule 避免拖慢训练。
  - 相较把预处理固定放 CPU 或与训练串行使用 GPU，核心创新是准确捕获训练期间的细粒度 GPU slack，并自动把预处理图嵌入这些空洞。
  - 推荐模型训练、GPU 共享、输入预处理、Kernel Fusion、资源感知调度

- [MAGIS: Memory Optimization via Coordinated Graph Transformation and Scheduling for DNN](https://doi.org/10.1145/3620666.3651330)
  - Renze Chen (Peking University)；Zijian Ding (University of California Los Angeles)；Size Zheng and Chengrui Zhang (Peking University)；Jingwen Leng (Shanghai Jiao Tong University)；Xuanzhe Liu and Yun Liang (Peking University)。
  - MAGIS 联合改变 DNN graph 结构与执行 schedule：Fission Transformation 缩小中间 tensor shape，随后决定算子顺序、重计算、swap-out/in 时机；分层树压缩 transformation space，增量 scheduler 避免每次改图后从头求解，在 latency constraint 下进一步降低峰值显存。
  - 相较 graph scheduler 只能缩短 tensor lifetime，核心创新是让会改变 tensor shape 的图变换与生命周期调度在同一搜索中协同。
  - DNN 显存优化、Graph Transformation、算子调度、重计算、Swap

- [8-bit Transformer Inference and Fine-tuning for Edge Accelerators](https://doi.org/10.1145/3620666.3651368)
  - Jeffrey Yu, Kartik Prabhu, Yonatan Urman, Robert M. Radway, Eric Han, and Priyanka Raina (Stanford University)。
  - 该工作让 edge accelerator 上 Transformer 的 forward、backward 与 element-wise operator 全面使用 FP8 或 Posit8，而非只量化 GEMM 输入；它把 LoRA 改造成 8-bit fine-tuning，并为 Posit8 设计基于位运算的 softmax/vector unit，在接近 BFloat16 精度下减少面积、功耗和访存。
  - 相较训练中大量保留高精度算子，核心创新是端到端评估并实现全算子 8-bit 推理与微调，同时针对 posit 数值格式协同设计硬件。
  - Transformer 边缘推理、8-bit 微调、FP8、Posit8、LoRA

- [Cocco: Hardware-Mapping Co-Exploration towards Memory Capacity-Communication Optimization](https://doi.org/10.1145/3617232.3624865)
  - Zhanhong Tan, Zijian Zhu, and Kaisheng Ma (Tsinghua University)。
  - Cocco 从 DNN 的图结构出发，在支持任意 graph pattern 的 graph-level dataflow 上共同搜索图分区 schedule 与片上 memory configuration；遗传式搜索在容量、外存访问、带宽和能耗间权衡，尤其处理残差、分支等不规则网络。
  - 相较先定 accelerator memory 再做 mapping，核心创新是利用 graph-level feature 联合探索硬件容量与执行分区，显式优化容量—通信权衡。
  - DNN 加速器、硬件映射协同、片上内存、图分区、设计空间探索

- [Atalanta: A Bit is Worth a “Thousand” Tensor Values](https://doi.org/10.1145/3620665.3640356)
  - Alberto Delmas Lascorz and Mostafa Mahmoud (University of Toronto)；Ali Hadi Zadeh (University of Toronto and 1QBit)；Milos Nikolic, Kareem Ibrahim, and Christina Giannoula (University of Toronto)；Ameer Abdelhadi (McMaster University)；Andreas Moshovos (University of Toronto and Vector Institute)。
  - Atalanta 在定点量化 DNN 的 tensor 离开芯片前透明压缩、读回时解压，以接近 arithmetic coding 的压缩率处理权重和 activation，但编码/解码单元仅需极小内部状态；它可叠加现有 quantization，并覆盖推理及训练时暂存 activation。
  - 相较复杂且难以高带宽并行的算术编码，核心创新是软硬件协同的轻状态无损 tensor codec，在 memory controller 前直接提升有效容量与带宽。
  - DNN Tensor 压缩、无损编码、量化模型、内存带宽、硬件软件协同

- [Harp: Leveraging Quasi-Sequential Characteristics to Accelerate Sequence-to-Graph Mapping of Long Reads](https://doi.org/10.1145/3620666.3651331)
  - Yichi Zhang, Dibei Chen, Gang Zeng, and Jianfeng Zhu (Tsinghua University)；Zhaoshi Li (MetaX Integrated Circuits)；Longlong Chen, Shaojun Wei, and Leibo Liu (Tsinghua University)。
  - Harp 加速长读段的 sequence-to-graph mapping，利用基因组图大部分路径近似顺序这一结构，以 HarpTree 紧凑暴露准顺序片段，再由多阶段 HarpExt 只在必要处执行昂贵图扩展；专用硬件据此减少随机图操作与面积。
  - 相较把 pangenome graph 当一般图遍历，核心创新是提取其 quasi-sequential 性质，并让数据结构、算法和 accelerator 围绕这一性质共同设计。
  - 基因组比对、Sequence-to-Graph、HarpTree、长读段、领域加速器

- [GSCore: Efficient Radiance Field Rendering via Architectural Support for 3D Gaussian Splatting](https://doi.org/10.1145/3620666.3651385)
  - Junseo Lee, Seokwon Lee, Jungi Lee, Junyong Park, and Jaewoong Sim (Seoul National University)。
  - GSCore 面向 3D Gaussian Splatting 的 radiance-field rendering，在 pipeline 中以 Gaussian shape-aware intersection 提前剔除无贡献 splat，用 hierarchical sorting 降低全局排序成本，并按 subtile 跳过空区域；硬件单元把三种算法优化流水化以服务不同场景和分辨率。
  - 相较把原始 Gaussian rasterization 直接搬到 GPU，核心创新是围绕 splat 的几何形状和 tile 稀疏性重构算法，再为新数据流定制硬件。
  - 3D Gaussian Splatting、Radiance Field、渲染加速、Hierarchical Sorting、Tile Culling

- [BeeZip: Towards An Organized and Scalable Architecture for Data Compression](https://doi.org/10.1145/3620666.3651323)
  - Ruihao Gao, Zhichun Li, Guangming Tan, and Xueqi Li (Chinese Academy of Sciences)。
  - BeeZip 面向大 sliding-window compression，把 hash lookup 与 match execution 解耦成两阶段：BeeHash 以动态调度组织哈希并行，HiveMatch 用异构规模处理单元并行比较候选，既避免为每个 matcher 复制历史窗口，也在不同压缩比目标下调节吞吐。
  - 相较以 CAM 或复制历史换吞吐的压缩器，核心创新是结构化两级并行，在可扩展内存成本下同时保住 large-window compression ratio。
  - 数据压缩加速、Sliding Window、BeeHash、HiveMatch、吞吐压缩比权衡

- [ACES: Accelerating Sparse Matrix Multiplication with Adaptive Execution Flow and Concurrency-Aware Cache Optimizations](https://doi.org/10.1145/3620666.3651381)
  - Xiaoyang Lu (Illinois Institute of Technology)；Boyu Long, Xiaoming Chen, and Yinhe Han (Chinese Academy of Sciences)；Xian-He Sun (Illinois Institute of Technology)。
  - ACES 针对 SpMM 稀疏模式随矩阵变化的问题，runtime 在数据复用优先和并行优先的执行流间自适应选择；global cache 的 replacement 同时考虑 locality 与正在等待同一数据的并发请求，non-blocking buffer 则让 miss 不阻塞其他乘加。
  - 相较为一种稀疏分布固定 dataflow，核心创新是把 sparsity-adaptive execution 与 concurrency-aware cache policy 放在同一 accelerator 中协同。
  - SpMM 加速器、稀疏模式、自适应数据流、并发感知缓存、Non-blocking Buffer

- [Explainable-DSE: An Agile and Explainable Exploration of Efficient HW/SW Codesigns of Deep Learning Accelerators Using Bottleneck Analysis](https://doi.org/10.1145/3623278.3624772)
  - Shail Dave (Arizona State University)；Tony Nowatzki (University of California Los Angeles)；Aviral Shrivastava (Arizona State University)。
  - Explainable-DSE 为 DNN accelerator 建立可插拔的 bottleneck model，从候选的算力、带宽、存储等 execution cost 判断当前瓶颈，再只采样能缓解瓶颈的硬软协同配置；多功能或多 workload 时会同时跟踪多个瓶颈，因而以较少试验找到满足延迟约束的设计。
  - 相较 evolutionary/ML black-box autotuning，核心创新是让每次 acquisition 都由显式瓶颈解释和定向，而非仅从历史分数猜下一个点。
  - DNN 加速器、可解释设计空间探索、瓶颈模型、硬软协同、Bayesian Search

- [λFS:: A Scalable and Elastic Distributed File System Metadata Service using Serverless Functions](https://doi.org/10.1145/3623278.3624765)
  - Benjamin Carver (George Mason University)；Runzhou Han (Iowa State University)；Jingyuan Zhang (George Mason University)；Mai Zheng (Iowa State University)；Yue Cheng (University of Virginia)。
  - λFS 把分布式文件系统 metadata cache 切分到 FaaS function 上，依据请求负载弹性增减并行 metadata worker，同时用状态持久化、cache coherence、请求路由与热状态恢复机制弥补函数短生命周期；目标是在工业 trace 下同时降低 metadata latency、常驻资源与成本。
  - 相较固定单机或静态 MDS cluster，核心创新是把大型有状态、性能敏感的 metadata service 重构成可弹性扩缩的 serverless cache plane。
  - Serverless 文件系统、Metadata Service、弹性缓存、FaaS、有状态函数

- [FaaSMem: Improving Memory Efficiency of Serverless Computing with Memory Pool Architecture](https://doi.org/10.1145/3620666.3651355)
  - Chuhao Xu, Yiyu Liu, Zijun Li, Quan Chen, and Han Zhao (Shanghai Jiao Tong University)；Deze Zeng (China University of Geosciences)；Qian Peng, Xueqi Wu, Haifeng Zhao, and Senbo Fu (Huawei)；Minyi Guo (Shanghai Jiao Tong University)。
  - FaaSMem 把 idle serverless container 的冷页卸载到远程 memory pool，并按页面在初始化、执行、keep-alive 等阶段的分配来源放入不同 Page Bucket，各 bucket 使用不同 offload policy；新增 semi-warm period 在本地保留近期可能复用的页，平衡部署密度与远程访问尾延迟。
  - 相较按容器整体或统一 LRU 换出，核心创新是利用函数生命周期导致的 page-segment 行为差异做分段卸载。
  - Serverless 内存、远程内存池、Page Bucket、Keep-alive、页面卸载

- [CodeCrunch: Improving Serverless Performance via Function Compression and Cost-Aware Warmup Location Optimization](https://doi.org/10.1145/3617232.3624866)
  - Rohan Basu Roy (Northeastern University)；Tirthak Patel (Rice University)；Rohan Garg (Nutanix)；Devesh Tiwari (Northeastern University)。
  - CodeCrunch 在 bursty serverless 负载下压缩已 warm 的函数代码/状态，以更小内存维持更多可快速恢复副本；控制器还利用服务器性能和成本异构，联合决定哪些函数保持 warm、以何种压缩状态以及放在哪台机器，避免 keep-alive 占满高价内存。
  - 相较只预测 invocation 后完整预热，核心创新是把函数压缩作为 warm-state 的中间层，并与成本感知的预热位置选择联合优化。
  - Serverless 冷启动、函数压缩、预热放置、异构服务器、内存压力

- [RainbowCake: Mitigating Cold-starts in Serverless with Layer-wise Container Caching and Sharing](https://doi.org/10.1145/3617232.3624871)
  - Hanfei Yu (Louisiana State University)；Rohan Basu Roy (Northeastern University)；Christian Fontenot (Louisiana State University)；Devesh Tiwari (Northeastern University)；Jian Li (Stony Brook University)；Hong Zhang (University of Waterloo)；Hao Wang (Louisiana State University)；Seung-Jong Park (Missouri University of Science and Technology)。
  - RainbowCake 把 container startup 拆成可独立缓存的多层，并识别不同函数可共享的基础层；event-driven controller 根据到达 burst、层大小和共享关系分别做 pre-warm/keep-alive，而非保留整容器，从而避免 partial caching 恢复仍慢与过度共享浪费内存。
  - 相较以 container 为唯一缓存单位，核心创新是以共享感知的 layer 为决策粒度，把部分缓存和跨函数复用统一起来。
  - Serverless 冷启动、容器分层缓存、跨函数共享、Pre-warming、内存效率

- [Flame: A Centralized Cache Controller for Serverless Computing](https://doi.org/10.1145/3623278.3624769)
  - Yanan Yang, Laiping Zhao, Yiming Li, and Shihao Wu (Tianjin University)；Yuechan Hao and Yuchi Ma (Huawei)；Keqiu Li (Tianjin University)。
  - Flame 将每台 server 自主保留哪些函数的 cache control plane 上收为集中式控制器，持续读取全局负载、cache occupancy 和函数热度，再跨节点决定副本增删与位置；这样可迁移被局部 skew 挤掉的热门函数，并减少重复冷门副本。
  - 相较 local cache policy 只见单机请求，核心创新是仿照 SDN 分离控制与数据面，用集群全局视角联合优化 hit ratio 和缓存资源。
  - Serverless Cache、集中式控制、冷启动、工作负载偏斜、资源效率

- [Characterizing Power Management Opportunities for LLMs in the Cloud](https://doi.org/10.1145/3620666.3651329)
  - Pratyush Patel (Microsoft Azure and University of Washington)；Esha Choukse, Chaojie Zhang, Íñigo Goiri, Brijesh Warrier, Nithish Mahalingam, and Ricardo Bianchini (Microsoft Azure)。
  - 该研究对不同 LLM、训练/推理阶段及配置的 GPU 功率曲线做细粒度测量，并与生产集群现象交叉验证，发现 inference 的平均/峰值功率存在可利用 headroom；POLCA 在虚拟化 GPU 遥测和控制受限条件下，用保守功率模型做机房 power oversubscription。
  - 相较按 GPU TDP 静态配置供电，核心创新是区分 LLM 训练与在线推理的实际功率形态，并把测量结论落为可部署的超卖控制框架。
  - LLM 基础设施、GPU 功率、Power Oversubscription、POLCA、云容量规划

- [Going Green for Less Green: Optimizing the Cost of Reducing Cloud Carbon Emissions](https://doi.org/10.1145/3620666.3651374)
  - Walid A. Hanafy and Qianlin Liang (University of Massachusetts Amherst)；Noman Bashir (MIT)；Abel Souza, David Irwin, and Prashant Shenoy (University of Massachusetts Amherst)。
  - GAIA 面向可延迟的云 batch job，同时读取区域/时段碳强度、job deadline 与 reserved/on-demand purchase 状态，决定何时运行和使用哪类容量；它显式计算因低碳时移造成的资源闲置，使用户在 carbon、completion time 与 monetary cost 三目标间选点。
  - 相较只最小化碳排或只约束 deadline，核心创新是把云购买折扣随利用率变化的成本损失纳入 carbon-aware scheduling。
  - 碳感知调度、云批处理、时间迁移、Reserved Instance、成本性能碳权衡

- [FOCAL: A First-Order Carbon Model to Assess Processor Sustainability](https://doi.org/10.1145/3620665.3640415)
  - Lieven Eeckhout (Ghent University)。
  - FOCAL 用 first-principles 参数化模型把 processor 的 chip area、制造碳、运行能耗、功率约束、寿命与性能归一为 NCF 指标；架构师可替换不确定参数，对 cache、core、加速机制等 archetype 判断其在不同部署条件下是强、弱或非可持续设计。
  - 相较依赖难获得的供应链精确数据，核心创新是以可解释的一阶模型揭示面积—能耗—性能的方向性边界，支持早期架构决策。
  - 处理器可持续性、Embodied Carbon、First-order Model、NCF、架构权衡

- [Predict; Don’t React for Enabling Efficient Fine-Grain DVFS in GPUs](https://doi.org/10.1145/3623278.3624756)
  - Srikant Bharadwaj (Microsoft)；Shomit Das (Qualcomm)；Kaushik Mazumdar and Bradford M. Beckmann (AMD)；Stephen Kosonocky (Uhnder)。
  - PCSTALL 面向可在微秒甚至更短 epoch 切换电压频率的 GPU，以 wavefront program counter 预测下一窗口的 stall/利用行为，再提前选 V/F state；它不把大量线程的瞬时活动简单平均，而用 PC 对重复阶段进行定位，优化 Energy-Delay²。
  - 相较 CPU 式 reactive utilization controller，核心创新是以 wavefront PC 做细粒度前瞻预测，使快速 IVR 的纳秒级调节能力真正可用。
  - GPU DVFS、Wavefront PC、功耗预测、细粒度频率控制、Energy-Delay

- [SUIT: Secure Undervolting with Instruction Traps](https://doi.org/10.1145/3620665.3640373)
  - Jonas Juffinger (Graz University of Technology)；Stepan Kalinin (North Carolina State University)；Daniel Gruss (Graz University of Technology)；Frank Mueller (North Carolina State University)。
  - SUIT 通过实测区分易受 undervolting fault 影响的指令：对频繁 faultable instruction 在硬件中放松 critical path，对少见指令设置 trap；CPU 平时运行高效 DVFS curve，trap 时临时切到保守曲线，经过安全窗口后再返回。
  - 相较为所有指令保留同一宽裕 voltage margin，核心创新是按指令脆弱性把硬件修正与动态 trap 分工，在安全前提下降压。
  - 安全降压、DVFS、Instruction Trap、Critical Path、能效

- [Kaleidoscope: Precise Invariant-Guided Pointer Analysis](https://doi.org/10.1145/3620666.3651340)
  - Tapti Palit and Pedro Fonseca (Purdue University)。
  - Kaleidoscope 在静态 pointer analysis 时先作更激进的 invariant 假设以缩小 points-to set，再插入运行时验证；若实际执行违背假设，就回退到保守 baseline 结果保持 soundness。更精确的集合可用于收紧 CFI 允许的间接目标。
  - 相较始终采用全程序保守 over-approximation，核心创新是把 optimistic analysis 与运行时 invariant guard 结合，在不牺牲可靠性的前提下换取精度。
  - 指针分析、运行时不变量、Points-to Set、CFI、Optimistic Analysis

- [Lifting Micro-Update Models from RTL for Formal Security Analysis](https://doi.org/10.1145/3620665.3640418)
  - Adwait Godbole and Kevin Cheang (University of California Berkeley)；Yatin A. Manerkar (University of Michigan)；Sanjit A. Seshia (University of California Berkeley)。
  - PAUL 从处理器 RTL 半自动提取 micro-update model，用小步状态更新抽象 pipeline、cache 等微结构效应，并支持按模块层次组合；安全验证在生成模型上检查软件是否会经硬件执行泄密，避免直接展开完整 RTL 的状态空间。
  - 相较人工手写抽象硬件模型，核心创新是给出可从 RTL 提升且保持安全分析 soundness 的 micro-update 表示与分层生成算法。
  - 形式化硬件安全、RTL、Micro-update Model、执行攻击、模型提升

- [Formal Mechanised Semantics of CHERI C: Capabilities, Undefined Behaviour, and Provenance](https://doi.org/10.1145/3617232.3624859)
  - Vadim Zaliva and Kayvan Memarian (University of Cambridge)；Ricardo Almeida (University of Edinburgh)；Jessica Clarke (University of Cambridge)；Brooks Davis (SRI International)；Alexander Richardson (University of Cambridge)；David Chisnall (Microsoft)；Brian Campbell and Ian Stark (University of Edinburgh)；Robert N. M. Watson and Peter Sewell (University of Cambridge)。
  - 该工作为用 capability 替代普通指针的 CHERI C 建立首套系统语义，明确 capability、pointer provenance 和 undefined behavior 的交互，并同时提供自然语言规范、基于 Cerberus 的可执行语义及 Coq 机械化版本，供移植、编译器和验证工具对齐。
  - 相较依赖实现经验推断 CHERI C 行为，核心创新是用三种互补形式给出可执行、可证明且覆盖 provenance/UB 的语言基础。
  - CHERI C、Capability、Pointer Provenance、Undefined Behavior、Coq 语义

- [Lightweight, Modular Verification for WebAssembly-to-Native Instruction Selection](https://doi.org/10.1145/3617232.3624862)
  - Alexa VanHattum (Wellesley College)；Monica Pardeshi (Carnegie Mellon University)；Chris Fallin (Fastly)；Adrian Sampson (Cornell University)；Fraser Brown (Carnegie Mellon University)。
  - Crocus 对 Cranelift 中 WebAssembly 到 AArch64 的每条 instruction-lowering rule 做模块化等价验证，分别建模源语义、目标指令和编译器 invariant；它覆盖 Wasm 1.0 整数操作，能重现已知 CVE、发现新 bug 和未明示的 invariant。
  - 相较验证整个优化编译器，核心创新是把证明边界缩到可独立检查的 lowering rule，同时仍连接语言隔离保证与具体 ISA。
  - WebAssembly、指令选择验证、Cranelift、AArch64、编译器正确性

- [Verifying Rust Implementation of Page Tables in a Software Enclave Hypervisor](https://doi.org/10.1145/3620665.3640398)
  - Zhenyang Dai (Tsinghua University and Ant Group)；Shuang Liu (Ant Group)；Vilhelm Sjoberg (CertiK)；Xupeng Li (Columbia University)；Yu Chen (Tsinghua University)；Wenhao Wang (Chinese Academy of Sciences)；Yuekai Jia (Tsinghua University and Ant Group)；Sean Noble Anderson (Portland State University)；Laila Elbeheiry (Max Planck Institute for Software Systems)；Shubham Sondhi (CertiK)；Yu Zhang (Yale University)；Zhaozhong Ni (CertiK)；Shoumeng Yan (Ant Group)；Ronghui Gu (Columbia University)；Zhengyu He (Ant Group)。
  - 该工作验证 Rust 编写的 HyperEnclave memory subsystem，证明 page-table 配置始终把 secure enclave 与宿主空间隔离；为此建立轻量 Rust MIR 形式语义，并用 layered proof 将页表操作、地址转换和高层隔离性质分层连接。
  - 相较只依赖 Rust memory safety，核心创新是进一步机械证明可能破坏隔离的语义配置正确性，并以 MIR 加分层证明控制系统规模。
  - Rust、软件 TEE、页表验证、Spatial Isolation、MIR 语义

- [C4CAM: A Compiler for CAM-based In-memory Accelerators](https://doi.org/10.1145/3620666.3651386)
  - Hamid Farzaneh and Joao Paulo Cardoso De Lima (TU Dresden)；Mengyuan Li (University of Notre Dame)；Asif Ali Khan (TU Dresden)；Xiaobo Sharon Hu (University of Notre Dame)；Jeronimo Castrillon (TU Dresden)。
  - C4CAM 把 TorchScript 中 KNN、HDC、推荐和 one-shot learning 的 search-like operator 逐级降低到 CAM 原语，并在不同 CAM 类型、工艺、阵列规模的延迟与功耗模型上探索配置，最终生成 accelerator code 和系统级性能/能耗估计。
  - 相较由硬件专家手写单一 CAM kernel，核心创新是用分层 compiler IR 同时承担高层可编程性与器件级 CAM 设计选择。
  - CAM In-memory Computing、TorchScript、编译器、设计空间探索、Search Operator

- [BaCO: A Fast and Portable Bayesian Compiler Optimization Framework](https://doi.org/10.1145/3623278.3624770)
  - Erik Orm Hellsten (Lund University)；Artur Souza (Federal University of Minas Gerais)；Johannes Lenfers (University of Münster)；Rubens Lacouture and Olivia Hsu (Stanford University)；Adel Ejjeh (University of Illinois at Urbana-Champaign)；Fredrik Kjolstad (Stanford University)；Michel Steuwer (University of Edinburgh)；Kunle Olukotun (Stanford University)；Luigi Nardi (Lund University and Stanford University)。
  - BaCO 为 CPU、GPU、FPGA 编译 autotuning 统一处理 permutation、ordered、continuous 参数以及已知/未知约束，以针对编译空间定制的 Bayesian optimization 在小 search budget 下选下一组 schedule；已接入 TACO、RISE/ELEVATE 和 HPVM2FPGA。
  - 相较只支持盒状连续参数的通用调参器，核心创新是让贝叶斯优化原生理解编译器的混合参数类型与非法配置。
  - 编译自动调优、Bayesian Optimization、CPU GPU FPGA、混合参数空间、低预算搜索

- [Merlin: Multi-tier Optimization of eBPF Code for Performance and Compactness](https://doi.org/10.1145/3620666.3651387)
  - Jinsong Mao (University of Massachusetts Amherst)；Hailun Ding (Rutgers University)；Juan Zhai and Shiqing Ma (University of Massachusetts Amherst)。
  - Merlin 在 kernel verifier 之前对 eBPF 做两级优化：LLVM IR pass 合并可统一执行的操作并做 strength reduction，随后 bytecode rewriter 进一步压缩指令；它以 verifier 约束为硬边界，面向 XDP 及 Sysdig/Tetragon/Tracee 的数百个程序减少长度和运行开销。
  - 相较依赖昂贵 superoptimization 或通用 LLVM pass，核心创新是针对 eBPF ISA/验证器设计可扩展的 IR+bytecode multi-tier rewrite。
  - eBPF、LLVM、Bytecode Rewriting、Kernel Verifier、XDP

- [Automatic Generation of Vectorizing Compilers for Customizable Digital Signal Processors](https://doi.org/10.1145/3617232.3624873)
  - Samuel Thomas and James Bornholt (University of Texas at Austin)。
  - Isaria 从可定制 DSP 的 ISA specification 自动合成等价 rewrite rule，用 equality saturation 搜索 vectorized implementation；系统还自动发现规则的 phase structure、安排应用顺序并剪枝中间状态，因此新 ISA extension 可立即获得相配的向量化 compiler。
  - 相较每代 DSP 手写 vectorizer 和规则，核心创新是从 ISA 语义同时生成 sound rewrite 与搜索调度，把编译器本身纳入架构探索。
  - DSP、自动向量化、Equality Saturation、规则合成、可定制 ISA

- [Fast Instruction Selection for Fast Digital Signal Processing](https://doi.org/10.1145/3623278.3624768)
  - Alexander J Root (Stanford University)；Maaz Bin Safeer Ahmad (Adobe)；Dillon Sharlet (Independent Researcher)；Andrew Adams and Shoaib Kamil (Adobe)；Jonathan Ragan-Kelley (MIT CSAIL)。
  - Pitchfork 用可移植 FPIR 表达 fixed-point DSP 中 rounding、saturation、conversion 与 fused arithmetic；编译器以经过验证及自动合成的 term-rewrite rule 将普通整数代码提升到 FPIR，再针对 AVX2、NEON、HVX 等目标选择一条或少数复合指令。
  - 相较要求程序员写平台 intrinsic 或让通用 pattern matcher 猜固定点语义，核心创新是增加显式 fixed-point IR，并以双向重写连接便携代码和定制 ISA。
  - DSP 编译、Fixed-point IR、指令选择、Term Rewriting、SIMD

- [An Encoding Scheme to Enlarge Practical DNA Storage Capacity by Reducing Primer-Payload Collisions](https://doi.org/10.1145/3620665.3640417)
  - Yixun Wei (University of Minnesota Twin Cities)；Bingzhe Li (University of Texas at Dallas)；David H.C. Du (University of Minnesota Twin Cities)。
  - CAC 面向需要 random access 的 DNA archive，系统计算编码密度、primer 数量、payload sequence 与 primer 碰撞等共同限制，主动牺牲少量碱基编码率来生成更少 primer-payload collision 的码字，从而让一个 DNA tube 可安全区分更多地址。
  - 相较只追求 bits-per-base，核心创新是把 primer 可用性纳入实际容量模型，并针对主导瓶颈设计 collision-aware code。
  - DNA 存储、Random Access、Primer-Payload Collision、编码方案、档案存储

- [Design of Novel Analog Compute Paradigms with Ark](https://doi.org/10.1145/3620665.3640419)
  - Yu-Neng Wang (Stanford University)；Glenn Cowan (Concordia University)；Ulrich Rührmair (TU Berlin and University of Connecticut)；Sara Achour (Stanford University)。
  - Ark 是描述 analog compute paradigm 的语言，允许设计者逐步把滤波、动态系统等模拟行为嵌入计算；validator 检查物理/数学约束，dynamical-system compiler 执行仿真，并在三个电路问题上量化器件非理想性与可重构资源的权衡。
  - 相较为每类模拟电路写一次性 co-design 工具，核心创新是提供介于专用电路和通用模拟阵列之间的可编程语义与验证/编译链。
  - 模拟计算、领域语言、Dynamical System、可重构电路、非理想性建模

- [LightRidge: An End-to-end Agile Design Framework for Diffractive Optical Neural Networks](https://doi.org/10.1145/3623278.3624757)
  - Yingjie Li (University of Utah and University of Maryland)；Ruiyang Chen, Minhan Lou, Berardi Sensale-Rodriguez, and Weilu Gao (University of Utah)；Cunxi Yu (University of Utah and University of Maryland)。
  - LightRidge 将 diffractive optical neural network 从模型设计到实体部署贯通：可微 optical-physics kernel 支持训练和拓扑搜索，加速 kernel 缩短 emulation，DSL 描述光学元件与系统，最终把候选映射到真实 optical prototype/on-chip integration。
  - 相较分离的光学仿真和手工硬件搭建，核心创新是以精确可微物理模型作为同一编译链的中间层，实现端到端 optical ML co-design。
  - 光学神经网络、DONN、可微物理、DSL、光学硬软协同

- [EagleEye: Nanosatellite constellation design for high-coverage, high-resolution sensing](https://doi.org/10.1145/3617232.3624851)
  - Zhuo Cheng, Bradley Denby, Kyle McCleary, and Brandon Lucia (Carnegie Mellon University)。
  - EagleEye 用低分辨率广覆盖 leader 卫星在轨检测目标，再把目标坐标发给高分辨率 follower；leader 必须在短观测窗口内同时完成检测和 ILP 调度，考虑 follower 轨道、转向/执行时间后选择可拍摄目标，从而兼顾覆盖面与图像细节。
  - 相较同质星座全用广角或长焦，核心创新是以 leader–follower mixed-resolution 分工，把 onboard vision 与星座 acquisition scheduling 闭环连接。
  - 纳卫星星座、遥感、Leader-Follower、在轨检测、ILP 调度

- [Energy Efficient Convolutions with Temporal Arithmetic](https://doi.org/10.1145/3620665.3640395)
  - Rhys Gretsch and Peiyang Song (University of California Santa Barbara)；Advait Madhavan (University of Maryland College Park)；Jeremy Lau and Timothy Sherwood (University of California Santa Barbara)。
  - 该工作把传感器 analog-to-time 输出直接留在 delay space，用 negative-log 变换令数值乘法成为时间延迟相加，并以 CMOS delay element 近似加/减；编译工具把普通 convolution 自动变换为时域电路，同时在量化式时间误差与器件噪声间选设计。
  - 相较先 ADC 再做数字 MAC，核心创新是首次在时间编码信号上构造可组合卷积算术，使 sensor readout 与计算融合。
  - Temporal Arithmetic、卷积、传感器内计算、Analog-to-Time、能效

- [Getting a Handle on Unmanaged Memory](https://doi.org/10.1145/3620666.3651326)
  - Nick Wanninger, Tommy McMichen, Simone Campanoni, and Peter Dinda (Northwestern University)。
  - ALASKA 为 C/C++ unmanaged heap 自动增加 handle 间接层：编译器把普通 pointer access 转换为优化后的 handle lookup，drop-in malloc runtime 维护映射并通过 service interface 移动物体；以 Redis defragmentation 为例，可在不改应用的情况下压紧 heap。
  - 相较每个 C/C++ 应用手工实现可移动对象，核心创新是以编译器—runtime 协同把 managed-language 的对象移动能力透明带入 unmanaged code。
  - 内存分配、对象移动、Handle、堆碎片整理、C/C++ Runtime

- [Cornucopia Reloaded: Load Barriers for CHERI Heap Temporal Safety](https://doi.org/10.1145/3620665.3640416)
  - Nathaniel Wesley Filardo (University of Cambridge and Microsoft)；Brett F. Gutstein, Jonathan Woodruff, Jessica Clarke, and Peter Rugg (University of Cambridge)；Brooks Davis (SRI International)；Mark Johnston (University of Cambridge)；Robert Norton (Microsoft)；David Chisnall (SCI Semiconductor)；Simon W. Moore (University of Cambridge)；Peter G. Neumann (SRI International)；Robert N. M. Watson (University of Cambridge)。
  - Cornucopia Reloaded 用 Arm Morello/CHERI-RISC-V 的 per-page capability load barrier 标记待撤销页；应用继续运行时，触碰旧 capability 的 load 被拦截并按需检查，后台完成 heap capability revocation，几乎消除原方案全局 stop-the-world pause。
  - 相较周期性扫描时暂停全部线程，核心创新是用页级 load barrier 将 temporal-safety revocation 变为并发、按触碰处理。
  - CHERI、Temporal Memory Safety、Capability Revocation、Load Barrier、Use-after-free

- [Characterizing a Memory Allocator at Warehouse Scale](https://doi.org/10.1145/3620666.3651350)
  - Zhuangzhuang Zhou (Cornell University)；Vaibhav Gogte, Nilay Vaish, Chris Kennelly, Patrick Xia, Svilen Kanev, and Tipp Moseley (Google)；Christina Delimitrou (MIT)；Parthasarathy Ranganathan (Google)。
  - 该研究测量 Google production fleet 中 TCMalloc 的 object size、lifetime、cache hit 与硬件异构性，据此在 thread/CPU/central cache 各层按实际使用动态定容，利用拓扑减少跨核通信，并用统计分配模式改进 packing；优化通过 fleet-wide A/B 验证。
  - 相较用少数 benchmark 固定 allocator 参数，核心创新是从 warehouse-scale 分布反推每级 cache policy，并在全 fleet 部署验证 CPU/RAM 收益。
  - 内存分配器、TCMalloc、Warehouse-scale、动态缓存、Google 生产测量

- [More Apps, Faster Hot-Launch on Mobile Devices via Fore/Background-aware GC-Swap Co-design](https://doi.org/10.1145/3620666.3651377)
  - Jiacheng Huang (City University of Hong Kong and Wuhan University)；Yunmo Zhang and Junqiao Qiu (City University of Hong Kong)；Yu Liang (ETH Zürich)；Rachata Ausavarungnirun (King Mongkut’s University of Technology North Bangkok)；Qingan Li (Wuhan University)；Chun Jason Xue (Mohamed bin Zayed University of Artificial Intelligence)。
  - Fleet 面向 Android hot-launch，同时优化后台 app 数量和恢复速度：GC 只追踪 background object、避免把长期 foreground object 换出；runtime 预测下次 hot launch 会访问的对象并指导 OS swap，且把访问模式相近的小对象聚到同页以减少随机换入。
  - 相较 GC 缩 heap 与 OS swap 各自独立，核心创新是跨 foreground/background 生命周期联合设计 object tracing、page layout 和 swap policy。
  - Android、Hot Launch、GC-Swap 协同、对象聚合、移动内存

- [MiniMalloc: A Lightweight Memory Allocator for Hardware-Accelerated Machine Learning](https://doi.org/10.1145/3623278.3624752)
  - Michael D. Moffitt (Google)。
  - MiniMalloc 为 ML accelerator 编译期静态分配 on-chip buffer，以递归 DFS 只枚举具有 canonical 结构的 layout；spatial inference 从部分分配推导必然冲突并提前回溯，dominance 检测丢弃不可能优于已有方案的候选。
  - 相较通用 bin packing/exhaustive search，核心创新是识别 accelerator tensor lifetime 问题的 canonical solution class，用结构性剪枝同时缩短求解和 allocator library。
  - ML 加速器、静态内存分配、Canonical Search、空间推理、编译器

- [Codesign of quantum error-correcting codes and modular chiplets in the presence of defects](https://doi.org/10.1145/3620665.3640362)
  - Sophia Fuhui Lin and Joshua Viszlai (University of Chicago)；Kaitlin N. Smith (Infleqtion)；Gokul Subramanian Ravi (University of Chicago)；Charles Yuan (MIT CSAIL)；Frederic T. Chong (University of Chicago)；Benjamin J. Brown (IBM T. J. Watson Research Center)。
  - 该工作共同选择量子 chiplet 大小和适应 fabrication defect 的 surface-code QEC：syndrome circuit 根据任意坏 qubit 分布重构，仿真得到 defect 对 logical fidelity 的影响，再据目标 error rate 制定 chiplet post-selection 与是否禁用某 qubit 的阈值。
  - 相较只丢弃有缺陷芯片或假设完美阵列，核心创新是让模块化装配选择与 defect-aware error-correction code 协同，限制物理 qubit 额外开销。
  - 量子纠错、Chiplet、制造缺陷、Surface Code、软硬协同

- [MECH: Multi-Entry Communication Highway for Superconducting Quantum Chiplets](https://doi.org/10.1145/3620665.3640377)
  - Hezi Zhang and Keyi Yin (University of California San Diego)；Anbang Wu (University of California Santa Barbara)；Hassan Shapourian and Alireza Shabani (Cisco Quantum Lab)；Yufei Ding (University of California San Diego)。
  - MECH 在 superconducting quantum chiplet 间铺设带多个入口的 communication highway，以额外 ancillary qubit 换取多组远程 qubit 同时路由；compiler 根据 circuit dependency、highway entry 占用和距离安排 teleport/communication，减少整体 circuit depth 与操作数。
  - 相较单入口串行跨 chiplet 通信，核心创新是把 highway 并发作为可分配资源，并由编译器联合管理入口和量子操作。
  - 量子 Chiplet、跨片通信、Ancilla Qubit、量子编译、并发路由

- [QuFEM: Fast and Accurate Quantum Readout Calibration Using the Finite Element Method](https://doi.org/10.1145/3620665.3640380)
  - Siwei Tan, Liqiang Lu, Hanyu Zhang, Jia Yu, Congliang Lang, Yongheng Shang, Xinkui Zhao, and Mingshuai Chen (Zhejiang University)；Yun Liang (Peking University)；Jianwei Yin (Zhejiang University)。
  - QuFEM 把大规模 quantum readout calibration 类比 finite-element 分解，将全局噪声矩阵拆为保留局部 qubit interaction 的小矩阵 tensor product，并与待校准概率分布迭代求解；稀疏 tensor-product engine 跳过中间零项以支撑百 qubit。
  - 相较完整矩阵校准精确但指数爆炸、局部法可扩展但失真，核心创新是有限元式 divide-and-conquer 同时保留局部耦合和稀疏可计算性。
  - 量子读出校准、Finite Element、噪声矩阵、稀疏张量、百 Qubit

- [A Fault-Tolerant Million Qubit-Scale Distributed Quantum Computer](https://doi.org/10.1145/3620665.3640388)
  - Junpyo Kim, Dongmoon Min, Jungmin Cho, Hyeonseong Jeong, Ilkwon Byun, Junhyuk Choi, Juwon Hong, and Jangwoo Kim (Seoul National University)。
  - 该方案面向多个 dilution refrigerator 组成的百万 qubit 系统，重排跨 DR surface-code error syndrome measurement 以减少慢且易错的 entanglement 操作，并设计可扩展的多 DR error-decoding unit 并行处理 syndrome，在通信延迟内完成检测和纠错。
  - 相较把单冰箱 QEC 直接扩展到多节点，核心创新是针对 inter-DR link 同时重构 syndrome sequence 与解码硬件架构。
  - 分布式量子计算、百万 Qubit、Quantum Error Correction、Dilution Refrigerator、解码器

- [Promatch: Extending the Reach of Real-Time Quantum Error Correction with Adaptive Predecoding](https://doi.org/10.1145/3620666.3651339)
  - Narges Alavisamani, Suhas Vittal, and Ramin Ayanzadeh (Georgia Tech)；Poulami Das (University of Texas at Austin)；Moinuddin Qureshi (Georgia Tech)。
  - Promatch 在实时 MWPM decoder 前先处理 Hamming weight 过高的 surface-code syndrome，以 locality-aware greedy matching 消去置信度高的简单/复杂 error pair；预解码覆盖率会按后端 decoder 在时限内可承受的规模自适应，避免过度匹配提高 logical error。
  - 相较固定规则 predecoder，核心创新是实时平衡 prematch 准确率与降维覆盖，使现有 MWPM 硬件可扩到 distance 11/13。
  - 量子纠错、MWPM、Adaptive Predecoding、Surface Code、实时解码

- [Greybox Fuzzing for Concurrency Testing](https://doi.org/10.1145/3620665.3640389)
  - Dylan Wolff, Shi Zheng, Gregory J. Duck, Umang Mathur, and Abhik Roychoudhury (National University of Singapore)。
  - Reads-From Fuzzer 针对并发程序的 thread interleaving，以事件间 reads-from relation 作为行为 coverage，优先变异能进入未探索 relation neighborhood 的 schedule；它介于完整系统搜索和纯随机 stress test 之间，以较少执行发现更多竞态/并发 bug。
  - 相较按代码边或随机 interleaving 采样，核心创新是把灰盒 fuzzing 的反馈定义为 partial-order 中的 reads-from 行为。
  - 并发测试、Greybox Fuzzing、Reads-from Relation、线程调度、竞态检测

- [Multi-Dimensional and Message-Guided Fuzzing for Robotic Programs in Robot Operating System](https://doi.org/10.1145/3620665.3640425)
  - Jia-Ju Bai (Beihang University)；Hao-Xuan Song and Shi-Min Hu (Tsinghua University)。
  - ROFER 对 ROS2 robotic program 的多维消息输入逐维估计其 coverage 贡献，优先变异高价值维度；它还抽取跨多个 ROS node 的 message feature 作为反馈，近似机器人状态转换，而非只看单节点代码覆盖，在 13 个程序中发现真实 bug。
  - 相较盲目变异完整 ROS message 或只追踪代码边，核心创新是联合 dimension-level mutation 与跨节点 message-state coverage。
  - ROS2、机器人软件 Fuzzing、消息引导、维度级变异、状态转换

- [CSSTs: A Dynamic Data Structure for Partial Orders in Concurrent Execution Analysis](https://doi.org/10.1145/3620666.3651358)
  - Hünkar Can Tunç (Aarhus University)；Ameya Prashant Deshmukh (Indian Institute of Technology Bombay)；Berk Cirisci (Amazon Web Services)；Constantin Enea (Ecole Polytechnique)；Andreas Pavlogiannis (Aarhus University)。
  - CSST 用 Collective Sparse Segment Tree 动态维护 concurrent trace 的 partial order；当 order width 近似线程数、远小于事件数时，插入、删除和 happens-before query 只需对数时间，尤其适合会回溯或修改关系的非 streaming dynamic analysis。
  - 相较 Vector Clock 更新随 trace size 线性且不能删边，核心创新是利用并发偏序窄宽结构，支持完整的动态 ordering 操作。
  - 并发执行分析、Partial Order、Sparse Segment Tree、Happens-before、动态数据结构

- [UBFuzz: Finding Bugs in Sanitizer Implementations](https://doi.org/10.1145/3617232.3624874)
  - Shaohua Li and Zhendong Su (ETH Zurich)。
  - UBFuzz 从有效 seed program 出发，以 shadow statement insertion 注入明确的 C/C++ undefined behavior，再对 GCC/LLVM sanitizer 做 differential testing；crash-site mapping 将报告位置映射回注入点，区分优化导致的差异与 sanitizer 漏报。
  - 相较只比较两个 sanitizer 输出，核心创新是同时拥有可控 UB 生成器与能定位真实漏检的专用 test oracle。
  - Sanitizer 测试、Undefined Behavior、Differential Testing、GCC LLVM、Test Oracle

- [AttAcc! Unleashing the Power of PIM for Batched Transformer-based Generative Model Inference](https://doi.org/10.1145/3620665.3640422)
  - Jaehyun Park, Jaewan Choi, Kwanhee Kyung, Michael Jaemin Kim, and Yongsuk Kwon (Seoul National University)；Nam Sung Kim (University of Illinois Urbana-Champaign)；Jung Ho Ahn (Seoul National University)。
  - AttAcc 面向 batch Transformer 生成模型，把 bandwidth-bound attention/GEMV 放到高带宽 PIM，把 compute-bound QKV/FFN GEMM 留给 GPU/xPU，并在 summarization 与逐 token generation 阶段协调数据和执行；175B 模型因此同时改善吞吐和能效。
  - 相较 GPU 承担全部算子或 PIM 独立执行模型，核心创新是按 operator arithmetic intensity 在 xPU 与 PIM 间异构分工。
  - 生成式 Transformer、PIM、Attention、GPU-PIM 异构、批量推理

- [SpecPIM: Accelerating Speculative Inference on PIM-Enabled System via Architecture-Dataflow Co-Exploration](https://doi.org/10.1145/3620666.3651352)
  - Cong Li, Zhe Zhou, Size Zheng, Jiaxi Zhang, Yun Liang, and Guangyu Sun (Peking University)。
  - SpecPIM 针对 speculative inference 中小 draft model 与大 verifier 对算力/带宽需求不同的问题，共同搜索 PIM-enabled system 的阵列/计算资源配置和两模型 dataflow，在不同 latency、throughput 或 energy 目标下选择设计，避免同一硬件阶段性闲置。
  - 相较为单个 LLM 优化的固定 PIM accelerator，核心创新是把 speculative algorithm 的模型异构性与 PIM architecture/dataflow 一起探索。
  - LLM 推理、Speculative Decoding、PIM、架构数据流协同、DSE

- [PIM-DL: Expanding the Applicability of Commodity DRAM-PIMs for Deep Learning via Algorithm-System Co-Optimization](https://doi.org/10.1145/3620665.3640376)
  - Cong Li and Zhe Zhou (Peking University)；Yang Wang (Microsoft Research Asia)；Fan Yang (Nankai University)；Ting Cao and Mao Yang (Microsoft Research)；Yun Liang and Guangyu Sun (Peking University)。
  - PIM-DL 先把 DNN linear layer 的 GEMM 校准为 lookup-table network，减少 commodity DRAM-PIM 不擅长的乘法；eLUT-NN 控制模型精度，Auto-Tuner 再按 UPMEM、HBM-PIM/AiM 的 bank、带宽和计算能力选择 LUT mapping。
  - 相较只把 element-wise/GEMV 零散卸载给 PIM，核心创新是从算法侧将主干 GEMM 改写为 LUT，使现有 DRAM-PIM 覆盖更多推理时间。
  - DRAM-PIM、LUT Neural Network、模型校准、Auto-tuning、DNN 推理

- [NeuPIMs: NPU-PIM Heterogeneous Acceleration for Batched LLM Inferencing](https://doi.org/10.1145/3620666.3651380)
  - Guseul Heo, Sangyeop Lee, Jaehong Cho, Hyunmin Choi, and Sanghyeon Lee (KAIST)；Hyungkyu Ham and Gwangsun Kim (POSTECH)；Divya Mahajan (Georgia Tech)；Jongse Park (KAIST)。
  - NeuPIMs 将 batch LLM 中 compute-bound 的 QKV/FFN GEMM 交给 NPU，将 bandwidth-bound attention GEMV 交给 PIM；每个 bank 增加 dual row buffer 允许普通访存与 PIM command 并发，runtime 把 batch 切成独立 sub-batch，在两类引擎间交错流水。
  - 相较 NPU 与 PIM 阻塞式轮流工作，核心创新是以双 row-buffer 硬件和 sub-batch interleaving 打破算子依赖造成的串行。
  - LLM 批量推理、NPU-PIM、GEMM/GEMV 分工、Dual Row Buffer、Sub-batch Pipeline

- [Felix: Optimizing Tensor Programs with Gradient Descent](https://doi.org/10.1145/3620666.3651348)
  - Yifan Zhao, Hashim Sharif, Vikram Adve, and Sasa Misailovic (University of Illinois Urbana-Champaign)。
  - Felix 将 tensor program 的 tiling、loop order、memory scope 等离散选择连续松弛为可微空间，并训练/构造 latency estimator；gradient descent 先快速移动到低延迟区域，再还原为合法 program candidate，在多种 GPU 上几分钟内找到优于通用 framework 的实现。
  - 相较 evolutionary/random search 在不可微离散空间逐点试验，核心创新是为 tensor program 建立可微表示和目标，使编译优化可直接用梯度。
  - Tensor Program、可微编译优化、Gradient Descent、Latency Estimator、GPU Autotuning

- [Optimizing Deep Learning Inference via Global Analysis and Tensor Expressions](https://doi.org/10.1145/3617232.3624858)
  - Chunwei Xia, Jiacheng Zhao, and Qianqi Sun (Chinese Academy of Sciences)；Zheng Wang (University of Leeds)；Yuan Wen (University of Aberdeen)；Teng Yu (Thewake Systems)；Xiaobing Feng and Huimin Cui (Chinese Academy of Sciences)。
  - Souffle 用 tensor expression 构造全局 dependency graph，沿数据流跨 operator 分析 tensor shape、reuse 与 resource constraint，把图分成可联合优化的 subprogram；子程序内再做语义保持变换、schedule 搜索和 instruction-level parallelism 优化。
  - 相较逐 operator fusion，核心创新是先以全局分析确定可安全跨界的优化区域，再在 tensor-expression 层联合改写多个算子。
  - DNN 编译、Tensor Expression、跨算子优化、Global Analysis、GPU 推理

- [PyTorch 2: Faster Machine Learning Through Dynamic Python Bytecode Transformation and Graph Compilation](https://doi.org/10.1145/3620665.3640366)
  - Jason Ansel, Edward Yang, and Horace He (Meta)；Natalia Gimelshein (OpenAI)；Animesh Jain, Michael Voznesensky, Bin Bao, David Berard, Geeta Chauhan, Anjali Chourdia, Will Constable, Alban Desmaison, Zachary DeVito, Elias Ellison, and Will Feng (Meta)；Jiong Gong (Intel)；Michael Gschwind, Brian Hirsh, Sherlock Huang, Laurent Kirsch, Michael Lazos, Yanbo Liang, Jason Liang, Yinghai Lu, CK Luk, and Bert Maher (Meta)；Yunjie Pan (University of Michigan)；Christian Puhrsch, Matthias Reso, Mark Saroufim, Helen Suk, and Michael Suo (Meta)；Phil Tillet (OpenAI)；Eikan Wang (Intel)；Xiaodong Wang, William Wen, Shunting Zhang, and Xu Zhao (Meta)；Keren Zhou (OpenAI)；Richard Zou, Ajit Mathews, Gregory Chanan, Peng Wu, and Soumith Chintala (Meta)。
  - PyTorch 2 的 TorchDynamo 在 Python bytecode 执行前动态改写，捕获连续 PyTorch operation 为 FX graph，遇到动态 Python 边界时 graph break 而不放弃 eager semantics；默认 TorchInductor 再把 graph 降为 GPU Triton 或 CPU C++ kernel，覆盖 180 余真实模型的训练与推理。
  - 相较 tracing 要求静态模型或完全切换图模式，核心创新是以 bytecode-level JIT 在保留动态 Python 的同时稳定提取可编译区域。
  - PyTorch 2、TorchDynamo、TorchInductor、Python Bytecode、Graph Compilation

- [Optimal Kernel Orchestration for Tensor Programs with Korch](https://doi.org/10.1145/3620666.3651383)
  - Muyan Hu (University of Illinois at Urbana-Champaign)；Ashwin Venkatram (AMD)；Shreyashri Biswas (Carnegie Mellon University)；Balamurugan Marimuthu (Sambanova Systems)；Bohan Hou and Gabriele Oliaro (Carnegie Mellon University)；Haojie Wang and Liyan Zheng (Tsinghua University)；Xupeng Miao (Carnegie Mellon University)；Jidong Zhai (Tsinghua University)；Zhihao Jia (Carnegie Mellon University)。
  - Korch 先把 DNN operator fission 为少量基础 tensor algebra primitive，再把哪些 primitive 合并为 kernel、以何种顺序执行及数据如何复用建模为 binary linear program，由求解器找到满足 dependency/resource constraint 的全局 kernel orchestration 并生成 GPU executable。
  - 相较贪心 operator fusion，核心创新是先拆后组，把跨算子的 kernel 边界选择转化为可求全局最优的约束优化。
  - Tensor Program、Kernel Orchestration、Operator Fission、Binary Linear Programming、GPU

- [Elivagar: Efficient Quantum Circuit Search for Classification](https://doi.org/10.1145/3620665.3640354)
  - Sashwat Anagolum (Pennsylvania State University)；Narges Alavisamani (Georgia Tech)；Poulami Das (The University of Texas at Austin)；Moinuddin Qureshi (Georgia Tech)；Yunong Shi (Amazon Quantum Technologies)。
  - Élivágar 面向真实 noisy quantum device 的分类 circuit search，按设备 topology 和噪声生成可直接映射的 candidate，并用 Clifford noise resilience 与 representational capacity 两个廉价 predictor 分别过滤不稳健或表达力不足的电路，剩余预算才用于真实训练和 data embedding 搜索。
  - 相较照搬 classical NAS 并对每个 circuit 完整训练，核心创新是让 search space、评价与 topology 从一开始就面向量子噪声。
  - 量子机器学习、Quantum Circuit Search、噪声感知、Clifford Predictor、拓扑映射

- [Red-QAOA: Efficient Variational Optimization through Circuit Reduction](https://doi.org/10.1145/3620665.3640363)
  - Meng Wang (University of British Columbia and Pacific Northwest National Laboratory)；Bo Fang and Ang Li (Pacific Northwest National Laboratory)；Prashant J. Nair (University of British Columbia)。
  - Red-QAOA 先用 simulated annealing 将组合优化图缩为较小 distilled graph，使其 energy landscape 的最优参数接近原图；在短而噪声更低的量子 circuit 上完成主要 parameter search，再把参数迁回原图做少量续调。
  - 相较直接在大图 QAOA 上受噪声反复调参，核心创新是利用 landscape concentration 以经典图压缩代理量子参数搜索。
  - QAOA、图约简、Variational Optimization、Simulated Annealing、NISQ

- [VarSaw: Application-tailored Measurement Error Mitigation for Variational Quantum Algorithms](https://doi.org/10.1145/3623278.3624764)
  - Siddharth Dangwal (University of Chicago)；Gokul Subramanian Ravi (University of Michigan)；Poulami Das (University of Texas at Austin)；Kaitlin N. Smith (Infleqtion)；Jonathan Mark Baker (University of Texas at Austin)；Frederic T. Chong (University of Chicago)。
  - VarSaw 为迭代式 VQA 的 measurement-error mitigation 去除两类重复：不同 circuit 间复用空间相近的 subset measurement，不必每轮都执行全部 global circuit，而是按参数变化选择性刷新相关性；在固定精度下显著减少送往量子设备的 circuit 数。
  - 相较 JigSaw 对每个 VQA iteration 重做完整 subset/global 测量，核心创新是利用跨 circuit 的空间冗余和跨 iteration 的时间冗余做应用定制采样。
  - Variational Quantum Algorithm、测量误差缓解、Subset Circuit、冗余消除、NISQ

- [ProxiML: Building Machine Learning Classifiers for Photonic Quantum Computing](https://doi.org/10.1145/3620666.3651367)
  - Aditya Ranjan (Northeastern University)；Tirthak Patel (Rice University)；Daniel Silver, Harshitta Gandhi, and Devesh Tiwari (Northeastern University)。
  - ProxiML 为 Xanadu X8 photonic quantum device 设计分类器，将光子平台的 gate、readout 与 shot noise 纳入 feature encoding、circuit architecture、训练和 inference；实机四分类任务用于验证模型而非只依赖 simulator。
  - 相较把超导/离子阱 QML circuit 原样迁移，核心创新是针对 photonic device 的噪声与可用操作共同设计可训练 classifier。
  - Photonic Quantum Computing、量子机器学习、Noise-aware Classifier、Xanadu X8、实机评测

- [FEASTA: A Flexible and Efficient Accelerator for Sparse Tensor Algebra in Machine Learning](https://doi.org/10.1145/3620666.3651336)
  - Kai Zhong and Zhenhua Zhu (Tsinghua University)；Guohao Dai (Shanghai Jiao Tong University and Infinigence-AI)；Hongyi Wang, Xinhao Yang, and Haoyu Zhang (Tsinghua University)；Jin Si (Beijing University of Posts and Telecommunications)；Qiuli Mao (Tsinghua University)；Shulin Zeng (Tsinghua University and Infinigence-AI)；Ke Hong (Tsinghua University)；Genghan Zhang (Stanford University)；Huazhong Yang and Yu Wang (Tsinghua University)。
  - FEASTA 以 sparse fiber tree 上的 Einstein summation 把不同 SpTA 统一为 fiber join/merge，再定义区分 dense/sparse operand 的指令集；可配置 function unit 按 instruction 组合不同 dataflow，使一套 accelerator 覆盖 SpMM 等多种稀疏张量和不规则 sparsity。
  - 相较每个 sparse kernel 固定专用 datapath，核心创新是从统一 fiber-tree 执行语义推导通用 SpTA ISA 和指令驱动架构。
  - 稀疏张量代数、Einstein Summation、Fiber Tree、领域 ISA、ML 加速器

- [CMC: Video Transformer Acceleration via CODEC Assisted Matrix Condensing](https://doi.org/10.1145/3620665.3640393)
  - Zhuoran Song, Chunyu Qi, Fangxin Liu, Naifeng Jing, and Xiaoyao Liang (Shanghai Jiao Tong University)。
  - CMC 利用视频解码器已有 motion/codec 信息在线找出跨帧和帧内不重要的 token/矩阵区域，跳过其 Transformer 计算并从相似重要区域恢复 feature；增强 CODEC 几乎零成本输出预测，专用 recovery engine 和 buffer 管理把理论稀疏真正转为硬件加速。
  - 相较在 VidT 内另训 sparse-attention predictor，核心创新是复用必经 CODEC 的时空冗余信号，并在算法和 accelerator 两侧共同消费。
  - Video Transformer、CODEC 辅助、时空冗余、Matrix Condensing、加速器

- [Tandem Processor: Grappling with Emerging Operators in Neural Networks](https://doi.org/10.1145/3620665.3640365)
  - Soroush Ghodrati, Sean Kinzer, Hanyang Xu, and Rohan Mahapatra (University of California San Diego)；Yoonsung Kim (KAIST)；Byung Hoon Ahn (University of California San Diego)；Dong Kai Wang (University of Illinois Urbana-Champaign)；Lavanya Karthikeyan (University of California San Diego)；Amir Yazdanbakhsh (Google DeepMind)；Jongse Park (KAIST)；Nam Sung Kim (University of Illinois Urbana-Champaign)；Hadi Esmaeilzadeh (University of California San Diego)。
  - Tandem Processor 作为 GEMM NPU 的片上伴随核，执行 normalization、activation、data movement 等日益多样的 non-GEMM operator；它对 memory access logic/ISA 专用化以跟上矩阵核吞吐，但只提供基础 vector arithmetic 保持可编程，并与 GEMM unit 紧耦合流水。
  - 相较为每个非 GEMM 算子放专用模块或回退 CPU，核心创新是在访存专用化、计算原语可编程之间建立可扩展的 companion architecture。
  - 神经网络加速器、Non-GEMM Operator、可编程向量核、NPU、硬件软件协同

- [Carat: Unlocking Value-Level Parallelism for Multiplier-Free GEMMs](https://doi.org/10.1145/3620665.3640364)
  - Zhewen Pan and Joshua San Miguel (University of Wisconsin-Madison)；Di Wu (University of Central Florida)。
  - Carat 利用 batched FP8 GEMM 中输入值重复，把每种 unique operand product 只计算一次，其他 lane 通过 temporal code 订阅对应结果，再做累加；这样以 value-level parallelism 用选择与加法替代大量 multiplier。
  - 相较只并行不同矩阵位置，核心创新是跨位置按“数值相同”共享乘积，把低精度带来的有限值域转化为新的并行维度。
  - GEMM、Value-level Parallelism、Multiplier-free、FP8、Temporal Coding

- [NetRen: Service Migration-Driven Network Renascence with Synthesizing Updated Configuration](https://doi.org/10.1145/3620666.3651365)
  - Rongxin Han, Jingyu Wang, Qi Qi, Haifeng Sun, Chaowei Xu, Zhaoyang Wan, and Zirui Zhuang (Beijing University of Posts and Telecommunications)；Yichuan Yu (Huawei)；Jianxin Liao (Beijing University of Posts and Telecommunications)。
  - NetRen 面向 enterprise service/traffic migration 后的 OSPF/BGP 重配置，先从目标网络抽取 configuration sketch，GraphTrans 根据历史优化关系并行生成高性能初值，再由 stepwise constraint repair 修复未满足的可达性、一致性等硬约束。
  - 相较纯符号 synthesis 从空解搜索或纯神经生成缺乏保证，核心创新是用 Transformer 提供接近可行的优化起点，再以逐步修复确保配置满足约束。
  - 网络配置综合、OSPF/BGP、Service Migration、Transformer、约束修复

- [Hydride: A Retargetable and Extensible Synthesis-based Compiler for Modern Hardware Architectures](https://doi.org/10.1145/3620665.3640385)
  - Akash Kothari, Abdul Rafae Noor, Muchen Xu, Hassam Uddin, Dhruv Baronia, Stefanos Baziotis, Vikram Adve, and Charith Mendis (University of Illinois at Urbana-Champaign)；Sudipta Sengupta (Amazon Web Services)。
  - Hydride 从厂商 ISA pseudocode 自动合成 target-independent AutoLLVM instruction 及到 x86/Hexagon/ARM 的 selector，并从 schedule-based language 的语义合成 code generation；397 个抽象指令即可覆盖 3557 个复杂 vector instruction。
  - 相较为每个新 ISA 手写 compiler IR、intrinsic 与 backend，核心创新是从形式化指令语义自动设计中间抽象和重定向 lowering。
  - Retargetable Compiler、AutoLLVM、指令语义、程序合成、SIMD ISA

- [RTL-Repair: Fast Symbolic Repair of Hardware Design Code](https://doi.org/10.1145/3620666.3651346)
  - Kevin Laeufer, Brandon Fajardo, Abhik Ahuja, Vighnesh Iyer, Borivoje Nikolić, and Koushik Sen (University of California Berkeley)。
  - RTL-Repair 对 failing testbench 建立 RTL semantics constraint，以 SMT optimization 在一次求解中同时定位 fault expression 和生成最小替换；adaptive windowing 只保留最能区分通过/失败的时间片，使 IDE 级秒级反馈成为可能。
  - 相较先定位再枚举 patch 的两阶段修复，核心创新是联合最小化位置与表达式修改，并动态收缩时序验证窗口。
  - RTL 修复、SMT、Fault Localization、Hardware Debugging、Testbench

- [SIRO: Empowering Version Compatibility in Intermediate Representations via Program Synthesis](https://doi.org/10.1145/3620666.3651366)
  - Bowen Zhang and Wei Chen (The Hong Kong University of Science and Technology)；Peisen Yao (Zhejiang University)；Chengpeng Wang, Wensheng Tang, and Charles Zhang (The Hong Kong University of Science and Technology)。
  - SIRO 用 divide-and-conquer skeleton 把旧版 IR 到新版 IR 的 translator 分解到 instruction 粒度，再以 program synthesis 在巨大候选空间生成语义等价 rewrite；在 LLVM 多个版本对之间自动产出十个 translator，使旧 static analyzer/fuzzer 可处理新 kernel IR。
  - 相较长期冻结工具链或人工维护每个 version pair，核心创新是用合成生成局部 IR translation，并由统一框架组合为完整兼容层。
  - LLVM IR、版本兼容、Program Synthesis、静态分析、Translator Generation

- [MemSnap μCheckpoints: A Data Single Level Store for Fearless Persistence](https://doi.org/10.1145/3620666.3651334)
  - Emil Tsalapatis, Ryan Hancock, Rakeeb Hossain, and Ali José Mashtizadeh (University of Waterloo)。
  - MemSnap 用 μCheckpoint 在单次 write transaction 粒度持久化进程内存，kernel 为每线程追踪 dirty set，并用 virtual-memory protection 冻结正在写出的页而让其他线程继续修改其他区域；SQLite、RocksDB、PostgreSQL 直接以 memory transaction 获得 ACID，不再另写 WAL。
  - 相较 whole-process checkpoint 仍需文件 WAL，核心创新是把 crash-consistent checkpoint 缩到并发事务粒度并由内核透明追踪。
  - Single-Level Store、μCheckpoint、持久化内存、ACID、Dirty Page Tracking

- [Grafu: Unleashing the Full Potential of Future Value Computation for Out-of-core Synchronous Graph Processing](https://doi.org/10.1145/3620665.3640409)
  - Tsun-Yu Yang (The Chinese University of Hong Kong)；Cale England (Oklahoma State University)；Yi Li and Bingzhe Li (University of Texas at Dallas)；Ming-Chang Yang (The Chinese University of Hong Kong)。
  - Grafu 在 out-of-core 同步图计算中提前算未来 iteration 的 vertex value，以 elevator execution order 增大可提前覆盖的顶点；conditional barrier 只在 dependency 可能被破坏时同步，greedy coloring 重排图以降低保存 future value 的额外内存。
  - 相较固定顺序 future computation 仍频繁 I/O 和全局 barrier，核心创新是同时优化执行顺序、依赖同步与图布局，逼近可提前计算的上限。
  - Out-of-core Graph、Future Value Computation、同步迭代、Conditional Barrier、图重排

- [CrossPrefetch: Accelerating I/O Prefetching for Modern Storage](https://doi.org/10.1145/3617232.3624872)
  - Shaleen Garg and Jian Zhang (Rutgers University)；Rekha Pitchumani (Samsung)；Manish Parashar (University of Utah)；Bing Xie (Microsoft)；Sudarsun Kannan (Rutgers University)。
  - CrossPrefetch 由 OS 维护并导出 page-cache state 与 prefetch effectiveness，user runtime 据真实命中反馈预测访问模式；regular I/O 与 prefetch 使用分离路径和细粒度 shared-file index，控制器再按空闲内存/带宽在保守与激进预取间自适应。
  - 相较内核 readahead 的刚性接口或用户态重复缓存，核心创新是跨 OS-runtime 共享可见性和职责，以反馈闭环控制预取。
  - I/O Prefetch、跨层优化、Page Cache、访问模式预测、存储吞吐

- [Palantir: Hierarchical Similarity Detection for Post-Deduplication Delta Compression](https://doi.org/10.1145/3620665.3640353)
  - Hongming Huang (City University of Hong Kong and Huawei)；Peng Wang (Huawei)；Qiang Su (City University of Hong Kong)；Hong Xu (The Chinese University of Hong Kong)；Chun Jason Xue (City University of Hong Kong and Mohamed bin Zayed University of Artificial Intelligence)；André Brinkmann (Johannes Gutenberg University Mainz)。
  - Palantir 在 backup dedup 后为每块构建多层 super-feature：敏感层只匹配非常相似块，宽松层扩大 delta candidate；false-positive filter 丢弃 delta 反而变大的配对，额外 feature 则利用备份流时间局部性缓存，提升总体压缩率。
  - 相较单一相似度阈值只能在候选召回和比较开销间二选一，核心创新是分层敏感度逐级扩大候选并在线过滤。
  - 备份去重、Delta Compression、Similarity Detection、Super-feature、时间局部性

- [TGLite: A Lightweight Programming Framework for Continuous-Time Temporal Graph Neural Networks](https://doi.org/10.1145/3620665.3640414)
  - Yufeng Wang and Charith Mendis (University of Illinois at Urbana-Champaign)。
  - TGLite 用 TBlock 显式表示 continuous-time graph 中节点消息流依赖、timestamp 与 temporal neighborhood，把 sampling、scatter/segment operator 和 CTDG-specific optimization 都定义在同一轻量表示上；四类 TGNN 可组合实现并在 V100/A100 上训练与推理。
  - 相较只支持离散 snapshot 或难组合的专用框架，核心创新是以 TBlock 同时承载连续时间语义和 GPU 优化接口。
  - Temporal GNN、Continuous-time Graph、TBlock、GPU Framework、Temporal Sampling

- [MaxK-GNN: Extremely Fast GPU Kernel Design for Accelerating Graph Neural Networks Training](https://doi.org/10.1145/3620665.3640426)
  - Hongwu Peng and Xi Xie (University of Connecticut)；Kaustubh Shivdikar (Northeastern University)；Md Amit Hasan, Jiahui Zhao, Shaoyi Huang, and Omer Khan (University of Connecticut)；David Kaeli (Northeastern University)；Caiwen Ding (University of Connecticut)。
  - MaxK-GNN 用只保留每行 top-k feature 的 MaxK nonlinearity 在算法层制造结构化稀疏，并以 CBSR 同时存值和 index；forward kernel 用 row-wise SpGEMM、shared-memory sparse accumulator，backward 则用 outer-product 与 sampled SpMM，令稀疏真正减少 GPU memory traffic。
  - 相较给既定稠密 GNN 事后优化 kernel，核心创新是共同设计可保持表达力的稀疏激活、数据格式和正反向 GPU 算法。
  - GNN 训练、MaxK 稀疏、CBSR、GPU Kernel、算法系统协同

- [Hector: An Efficient Programming and Compilation Framework for Implementing Relational Graph Neural Networks in GPU Architectures](https://doi.org/10.1145/3620666.3651322)
  - Kun Wu (University of Illinois at Urbana-Champaign)；Mert Hidayetoğlu (Stanford University)；Xiang Song (AWS AI)；Sitao Huang (University of California Irvine)；Da Zheng and Israt Nisa (AWS AI)；Wen-Mei Hwu (Nvidia and University of Illinois at Urbana-Champaign)。
  - Hector 用高层 IR 表达 relational GNN 的 node/edge type、relation 和 operator dependency，低层 IR 再独立描述 data layout、GEMM 与 traversal template；code generator 通过 linear operator reordering 和 compact materialization 避免 relation 中间 tensor 复制，自动产生 CUDA/C++。
  - 相较模型语义、异构图 layout 和 kernel 优化紧耦合的手写实现，核心创新是以两级 IR 解耦三者并支持跨算子 memory optimization。
  - Relational GNN、异构图、两级 IR、CUDA Codegen、Compact Materialization

- [Sleuth: A Trace-Based Root Cause Analysis System for Large-Scale Microservices with Graph Neural Networks](https://doi.org/10.1145/3623278.3624758)
  - Yu Gan, Guiyang Liu, Xin Zhang, Qi Zhou, Jiesheng Wu, and Jiangwei Jiang (Alibaba)。
  - Sleuth 将每条 distributed trace 表示为 span dependency graph，以无监督 GNN 学习各 span 对端到端异常的 causal impact，再按 trace distance 聚类，只在代表 trace 上定位 root cause；预训练模型可跨微服务迁移，必要时 few-shot 微调。
  - 相较经验阈值或只适用于小 benchmark 的 RCA，核心创新是结合 trace-level graph learning、聚类降采样与生产规模 synthetic benchmark 验证跨应用适配。
  - 微服务根因分析、Distributed Trace、GNN、无监督学习、Trace Clustering

- [PDIP: Priority Directed Instruction Prefetching](https://doi.org/10.1145/3620665.3640394)
  - Bhargav Reddy Godala (Princeton University)；Sankara Prasad Ramesh (University of California San Diego)；Gilles A. Pokam, Jared Stark, and Andre Seznec (Intel)；Dean Tullsen (University of California San Diego)；David I. August (Princeton University)。
  - PDIP 与现代 FDIP 协同，不把所有 I-cache miss 都当目标，而是记录真正导致 front-end stall 后发生 resteer 的 target，并把该 target 与更早可见的 trigger 关联；后续执行遇到 trigger 才优先预取这条困难路径。
  - 相较只追求 miss-rate 降低的 instruction prefetcher，核心创新是识别已被 FDIP 隐藏和未被隐藏的 miss，只为后者分配带宽与 cache。
  - 指令预取、FDIP、Front-end Stall、Resteer Path、Server Workload

- [Limoncello: Prefetchers for Scale](https://doi.org/10.1145/3620666.3651373)
  - Akanksha Jain (Google)；Hannah Lin (Google and University of Washington)；Carlos Villavieja (Google)；Baris Kasikci (Google and University of Washington)；Chris Kennelly, Milad Hashemi, and Parthasarathy Ranganathan (Google)。
  - Limoncello 在 Google 高利用率 fleet 上监控 memory bandwidth/latency，带宽拥塞时关闭会放大流量的 hardware prefetcher，只对已识别的 library hot path 插入 targeted software prefetch；控制策略按机器与负载动态切换，避免预取和 demand request 互相挤占。
  - 相较始终开启硬件预取，核心创新是以 fleet-level 带宽压力为反馈协调硬件开关与选择性软件预取。
  - 数据预取、内存带宽、Google Fleet、Software Prefetch、生产优化

- [PATHFINDER: Practical Real-Time Learning for Data Prefetching](https://doi.org/10.1145/3620666.3651332)
  - Lin Jia, James Patrick Mcmahon, Sumanth Gudaparthi, Shreyas Singh, and Rajeev Balasubramonian (University of Utah)。
  - PATHFINDER 用小型 spiking neural network 观察 memory-access delta，STDP 在推理同时做局部在线学习，因此无需离线 benchmark 训练即可适应未见 pattern；硬件以低功耗脉冲状态产生下一地址 prefetch。
  - 相较大型离线神经 prefetcher，核心创新是利用 SNN/STDP 的边运行边学习特性，把实时训练成本压到处理器可接受范围。
  - Data Prefetching、Spiking Neural Network、STDP、在线学习、微结构预测

- [Skip It: Take Control of Your Cache!](https://doi.org/10.1145/3620665.3640407)
  - Shashank Anand and Michal Friedman (ETH Zurich)；Michael Giardino (Huawei)；Gustavo Alonso (ETH Zurich)。
  - 该工作在开源 BOOM RISC-V 核中加入两类 user-controlled cache writeback primitive，并在其上实现 Skip It：硬件记录/判断目标 line 是否已经干净或已满足持久化要求，跳过重复 writeback，同时保持显式 cache management 的正确顺序。
  - 相较完全由不透明商业硬件执行 flush，核心创新是提供可研究的微结构接口，并在硬件侧直接消除无效 writeback。
  - Cache Writeback、RISC-V BOOM、显式缓存管理、持久化、微结构扩展

- [RPG^2: Robust Profile-Guided Runtime Prefetch Generation](https://doi.org/10.1145/3620665.3640396)
  - Yuxuan Zhang, Nathan Sobotka, and Soyoon Park (University of Pennsylvania)；Saba Jamilan (University of California Santa Cruz)；Tanvir Ahmed Khan (Columbia University)；Baris Kasikci (University of Washington and Google)；Gilles A Pokam (Intel)；Heiner Litz (University of California Santa Cruz)；Joseph Devietti (University of Pennsylvania)。
  - RPG² 直接在运行中的 C/C++ program 上 profile miss 与时机，在线注入不同距离的 prefetch instruction，再依据真实输入、processor 和 bandwidth 的速度反馈持续调参；若预取污染 cache 或争抢内存使性能下降，则自动回滚原代码。
  - 相较 profile-guided compiler 一次性静态决定，核心创新是让 prefetch generation、timing tuning 和安全回滚在部署 runtime 中闭环。
  - Runtime Prefetch、Profile-guided Optimization、在线调优、C/C++、性能回滚

- [METAL: Caching Multi-level Indexes in Domain-Specific Architectures](https://doi.org/10.1145/3620665.3640402)
  - Anagha Molakalmur Anil Kumar and Aditya Prasanna (Simon Fraser University)；Jonathan Balkind (University of California Santa Barbara)；Arrvindh Shriraman (Simon Fraser University)。
  - METAL 面向使用多级 index 的 sparse DSA，将 index metadata reuse 与实际 data reuse 分离：IX-Cache 用 range tag 直接命中索引覆盖范围、跳过 pointer walk；reuse-pattern interface 在遍历不同区域时显式控制 insertion/bypass，避免普通 cache 被 index node 冲刷。
  - 相较缓存最终地址或把 index/data 混在同一 policy，核心创新是把多级索引的范围语义和遍历阶段暴露给专用 cache。
  - 领域专用架构、多级索引、IX-Cache、稀疏数据、Range Tag

- [GMT: GPU Orchestrated Memory Tiering for the Big Data Era](https://doi.org/10.1145/3620666.3651353)
  - Chia-Hao Chang, Jihoon Han, and Anand Sivasubramaniam (Pennsylvania State University)；Vikram Sharma Mailthody, Zaid Qureshi, and Wen-Mei Hwu (NVIDIA Research)。
  - GMT 构建 GPU HBM—host DRAM—SSD 三级 memory hierarchy，由 GPU 自己编排 latency/bandwidth-sensitive page transfer，避免 host CPU 成为数据路径瓶颈；eviction 时 reuse predictor 决定页进入 host tier 还是绕过直落 SSD，而非机械逐级下放。
  - 相较 GPU 直连 SSD 的两级方案或 CPU 控制的三级 HMM，核心创新是由 GPU 控制跨层迁移并做预测式中间层插入。
  - GPU Memory Tiering、HBM DRAM SSD、页面迁移、Reuse Prediction、Big Data

- [GMLake: Efficient and Transparent GPU Memory Defragmentation for Large-scale DNN Training with Virtual Memory Stitching](https://doi.org/10.1145/3620665.3640423)
  - Cong Guo (Shanghai Jiao Tong University and Shanghai Qi Zhi Institute)；Rui Zhang (Ant Group)；Jiale Xu, Jingwen Leng, Zihan Liu, Ziyu Huang, and Minyi Guo (Shanghai Jiao Tong University and Shanghai Qi Zhi Institute)；Hao Wu, Shouren Zhao, Junping Zhao, and Ke Zhang (Ant Group)。
  - GMLake 面向 LLM 训练中 recomputation、offloading、LoRA 等造成的频繁不规则显存申请，通过 GPU virtual-memory stitching 把多个物理不连续小块映射成应用看到的连续 allocation；allocator 可重组 block 而无需搬数据，对模型和既有 memory-reduction technique 透明。
  - 相较 caching allocator 依靠 split/merge 物理块，核心创新是用虚拟地址拼接消除外部碎片，绕开昂贵 GPU 原生分配。
  - LLM 训练、GPU 显存、内存碎片、Virtual Memory Stitching、Caching Allocator

- [Direct Memory Translation for Virtualized Clouds](https://doi.org/10.1145/3620665.3640358)
  - Jiyuan Zhang (University of Illinois Urbana-Champaign)；Weiwei Jia (University of Rhode Island)；Siyuan Chai, Peizhe Liu, Jongyul Kim, and Tianyin Xu (University of Illinois Urbana-Champaign)。
  - DMT 要求 OS 把每个 VMA 的末级 PTE 连续放入 Translation Entry Area，并用少量寄存器保存 virtual page 到 TEA 的直接映射；虚拟化时 guest 与 host 协同让 guest TEA 直接落物理内存，把原本最多 24 次的 nested page walk 降为固定少数访问。
  - 相较继续扩大 TLB/page-walk cache，核心创新是重排页表物理布局，使翻译地址可计算并跨过中间层级，同时兼容 x86 软件。
  - 虚拟内存、地址翻译、虚拟化、Translation Entry Area、Page Walk

- [WASP: Workload-Aware Self-Replicating Page-Tables for NUMA Servers](https://doi.org/10.1145/3620665.3640369)
  - Hongliang Qu and Zhibin Yu (Chinese Academy of Sciences)。
  - WASP 在 Linux NUMA server 上读取通用性能指标，判断当前 workload 和 co-runner 是否会因 remote page-table access 受益于 self-replication；hierarchical gradual controller 逐层开启/关闭副本并观察反馈，避免一次全量复制反而增加一致性与内存成本。
  - 相较让用户静态开关 PTSR，核心创新是用可跨 x86/ARM 的指标对每个 workload 在线、渐进地控制页表复制。
  - NUMA、Page-table Replication、Workload-aware、Linux、地址翻译

- [Supporting Descendants in SIMD-Accelerated JSONPath](https://doi.org/10.1145/3623278.3624754)
  - Mateusz Gienieczko and Filip Murlak (University of Warsaw)；Charles Paperman (CRIStAL, Université de Lille, INRIA)。
  - 该 JSONPath engine 支持 child、descendant、wildcard 与 label，以 depth-stack automaton 跟踪嵌套深度和后代状态，并消费 SIMD classifier 产生的 structural event stream；当当前 automaton 状态判定文档片段不相关时，向量化快速跳过。
  - 相较 SIMD JSON query 只支持直接 child，核心创新是用 depth-stack automata 在不逐字符遍历的情况下表达 descendant semantics。
  - JSONPath、SIMD、Depth-stack Automata、流式查询、数据处理

- [Boost Linear Algebra Computation Performance via Efficient VNNI Utilization](https://doi.org/10.1145/3620666.3651333)
  - Hao Zhou and Qiukun Han (Enflame Tech)；Heng Shi (Enflame Tech and Shanghai Jiao Tong University)；Yalin Zhang (Enflame Tech Inc.)；Jianguo Yao (Enflame Tech and Shanghai Jiao Tong University)。
  - 该编译方法先从 dense linear algebra loop 识别 VNNI 特有的 dot-product/packing 机会，再联合选择 input feed、memory layout、register/cache reuse 与 instruction-level parallelism；静态 cost model 评估变换组合，避免只在最内层做 peephole match。
  - 相较传统 auto-vectorizer 只识别局部 pattern，核心创新是从整个 DLA dataflow 规划 VNNI 数据准备和延迟隐藏。
  - Intel VNNI、Dense Linear Algebra、Auto-vectorization、Cost Model、DNN Kernel

- [A shared compilation stack for distributed-memory parallelism in stencil DSLs](https://doi.org/10.1145/3620666.3651344)
  - George Bisbas (Imperial College London)；Anton Lydike, Emilien Bauer, Nick Brown, and Mathieu Fehr (University of Edinburgh)；Lawrence Mitchell (Unaffiliated)；Gabriel Rodriguez-Canal and Maurice Jamieson (University of Edinburgh)；Paul H J Kelly (Imperial College London)；Michel Steuwer (Technische Universität Berlin)；Tobias Grosser (University of Cambridge)。
  - 该工作在 MLIR 中加入 distributed stencil computation 的 domain abstraction 和 message-passing lowering，让 Devito、PSyclone、Open Earth Compiler 三个 DSL 共用 decomposition、halo exchange 与后端优化组件，同时仍由各前端保留领域语义。
  - 相较每个 stencil DSL 独立维护 MPI backend，核心创新是建立可共享的 HPC MLIR stack，把高层差异与分布式执行共性解耦。
  - HPC DSL、MLIR、Stencil、Distributed Memory、Message Passing

- [SlimSLAM: An Adaptive Runtime for Visual-Inertial Simultaneous Localization and Mapping](https://doi.org/10.1145/3620666.3651361)
  - Armand Behroozi and Yuxiang Chen (University of Michigan)；Vlad Fruchter, Lavanya Subramanian, and Sriseshan Srikanth (Meta)；Scott Mahlke (University of Michigan)。
  - SlimSLAM 读取 visual-inertial SLAM 内部 state（特征质量、运动和估计置信度等），在线判断哪些 worst-case algorithm parameter 过度配置，再调节 feature 数、优化工作量等旋钮；它按当前输入给计算预算，在 Raspberry Pi 等受限平台维持 pose accuracy。
  - 相较固定为最坏场景设定 SLAM 或只按 CPU utilization 降级，核心创新是使用算法状态做 domain-specific runtime scheduling。
  - Visual-Inertial SLAM、自适应运行时、算法状态、边缘计算、实时定位

- [Compiling Loop-Based Nested Parallelism for Irregular Workloads](https://doi.org/10.1145/3620665.3640405)
  - Yian Su (Northwestern University)；Mike Rainey (Carnegie Mellon University)；Nick Wanninger, Nadharm Dhiantravan, and Jasper Liang (Northwestern University)；Umut A. Acar (Carnegie Mellon University)；Peter Dinda and Simone Campanoni (Northwestern University)。
  - HBC 将 OpenMP 等可嵌套 fork-join loop 编译为带 heartbeat scheduling 的 binary，运行时按已消耗工作、剩余粒度和 worker 状态决定何时拆出 parallel task；对输入敏感的不规则 workload 可自动限制 task creation 和 load-balancing overhead。
  - 相较开发者手工设 grain size 或 runtime 固定切分，核心创新是把有形式性能保证的 heartbeat granularity control 嵌入编译产物。
  - Nested Parallelism、Irregular Workload、Heartbeat Scheduling、OpenMP、粒度控制

- [TinyForge: A Design Space Exploration to Advance Energy and Silicon Area Trade-offs in tinyML Compute Architectures with Custom Latch Arrays](https://doi.org/10.1145/3620666.3651328)
  - Massimo Giordano, Rohan Doshi, and Qianyun Lu (Stanford University)；Boris Murmann (University of Hawaii)。
  - TinyForge 以 custom latch array 储存 tinyML 权重/激活，并共同搜索 bit-serial 或 bit-parallel compute、systolic/combinational scaling、memory hierarchy 与 dataflow；功耗/面积/延迟模型和遗传算法给出 MLPerf Tiny/BERT-Tiny 的 Pareto architecture。
  - 相较只比较现成 SRAM+MAC template，核心创新是把高密度低能耗 latch array 与 compute fabric、dataflow 一起纳入多目标 DSE。
  - tinyML、Latch Array、Bit-serial Compute、硬件 DSE、MLPerf Tiny

- [MulBERRY: Enabling Bit-Error Robustness for Energy-Efficient Multi-Agent Autonomous Systems](https://doi.org/10.1145/3620665.3640420)
  - Zishen Wan (Georgia Tech)；Nandhini Chandramoorthy, Karthik Swaminathan, and Pin-Yu Chen (IBM Research)；Kshitij Bhardwaj (Lawrence Livermore National Lab)；Vijay Janapa Reddi (Harvard University)；Arijit Raychowdhury (Georgia Tech)。
  - MulBERRY 面向采用多智能体强化学习的协同 UAV swarm，在离线和机载训练中注入实测 undervolting bit-error pattern，并由 agent 与 server 协同调整鲁棒策略/参数；同时结合温度、功率和飞行实验，寻找更低电压但任务成功率不降的点。
  - 相较只给单设备 DNN 做容错，核心创新是把硬件 bit fault、协同 MARL policy 和整队 mission quality-of-flight 联合优化。
  - 多智能体强化学习、UAV Swarm、Bit-error Robustness、Undervolting、非 LLM Agent

- [Exploiting Human Color Discrimination for Memory- and Energy-Efficient Image Encoding in Virtual Reality](https://doi.org/10.1145/3617232.3624860)
  - Nisarg Ujjainkar and Ethan Shahan (University of Rochester)；Kenneth Chen, Budmonde Duinkharjav, and Qi Sun (New York University)；Yuhao Zhu (University of Rochester)。
  - 该 VR framebuffer codec 根据人眼颜色辨别阈值调整 pixel color，使数值变化落在人类不可见范围内，并对 peripheral vision 使用更宽容阈值，再选择编码成本更低的颜色；轻量硬件实时执行，以减少 DRAM traffic 和显示能耗。
  - 相较要求 bit-exact 的 framebuffer compression，核心创新是把 psychophysical color-discrimination model 直接转为可控的感知无损编码空间。
  - Virtual Reality、Framebuffer Compression、人眼感知、DRAM 流量、能效

- [MicroVSA: An Ultra-Lightweight Vector Symbolic Architecture-based Classifier Library for Always-On Inference on Tiny Microcontrollers](https://doi.org/10.1145/3620665.3640374)
  - Nuntipat Narkthong and Shijin Duan (Northeastern University)；Shaolei Ren (University of California Riverside)；Xiaolin Xu (Northeastern University)。
  - MicroVSA 将 low-dimensional vector-symbolic classifier 的编码、绑定、累加和相似度 kernel 针对 8/16/32-bit MCU 分别压缩和优化，用几十字节 RAM 完成心梗检测、活动识别与关键词唤醒；模型规模和实现均适配 always-on 低端芯片。
  - 相较把 tiny DNN 再量化到 MCU，核心创新是选择更轻的 VSA/LDC 算法并提供跨位宽手工优化库，把 inference 下沉到 8-bit MCU。
  - TinyML、Vector Symbolic Architecture、MCU、Always-on Inference、低内存分类

- [Energy-Adaptive Buffering for Efficient, Responsive, and Persistent Batteryless Systems](https://doi.org/10.1145/3620666.3651370)
  - Harrison Williams and Matthew Hicks (Virginia Tech)。
  - REACT 面向能量采集设备的波动输入，用可重构 capacitor bank 随净输入功率扩容或缩容：能量富余时并入更多电容避免溢出成热，功率下降时重新连接内部电容以榨取剩余电荷，并允许应用声明 longevity guarantee。
  - 相较设计时固定 buffer capacity，核心创新是让储能电容本身成为运行时可调资源，解耦系统电压、可用能量和响应速度。
  - Batteryless System、Energy Harvesting、可变电容、能量缓冲、持久感知

- [JUNO: Optimizing High-Dimensional Approximate Nearest Neighbour Search with Sparsity-Aware Algorithm and Ray-Tracing Core Mapping](https://doi.org/10.1145/3620665.3640360)
  - Zihan Liu (Shanghai Jiao Tong University and Shanghai Qi Zhi Institute)；Wentao Ni (Shanghai Jiao Tong University)；Jingwen Leng (Shanghai Jiao Tong University and Shanghai Qi Zhi Institute)；Yu Feng (University of Rochester)；Cong Guo (Shanghai Jiao Tong University and Shanghai Qi Zhi Institute)；Quan Chen (Shanghai Jiao Tong University)；Chao Li and Minyi Guo (Shanghai Jiao Tong University and Shanghai Qi Zhi Institute)；Yuhao Zhu (University of Rochester)。
  - JUNO 在 product-quantization ANN search 中识别可跳过的 pairwise distance/accumulation，以 sparsity/locality-aware 算法压缩候选；硬件映射把几何相交式筛选放到 GPU ray-tracing core，并与 tensor core 上的后续计算流水。
  - 相较只在 CUDA core 优化 PQ lookup，核心创新是把 ANN 稀疏筛选重表述为 RT-core 友好的任务，并与 tensor computation 异构协作。
  - Approximate Nearest Neighbor、Product Quantization、Ray-tracing Core、向量数据库、GPU

- [ngAP: Non-blocking Large-scale Automata Processing on GPUs](https://doi.org/10.1145/3617232.3624848)
  - Tianao Ge (Hong Kong University of Science and Technology Guangzhou)；Tong Zhang (Samsung)；Hongyuan Liu (Hong Kong University of Science and Technology Guangzhou)。
  - ngAP 打破 automata 一次只推进一个输入 symbol 的串行限制，预取未来可计算状态以并行处理多个 symbol；重复 state transition 存入 memoization table，部分计算私有化以固定 thread-state 映射，提升 GPU occupancy 与 locality。
  - 相较 one-symbol-at-a-time GPU automata engine，核心创新是 non-blocking 多 symbol execution，并由预取、记忆化和私有化共同支撑。
  - GPU Automata、Non-blocking Processing、Memoization、状态机、并行模式匹配

- [Marple: Scalable Spike Sorting for Untethered Brain-Machine Interfacing](https://doi.org/10.1145/3620665.3640357)
  - Eugene Sha, Andy Liu, Kareem Ibrahim, Mostafa Mahmoud, and Christina Giannoula (University of Toronto)；Ameer Abdelhadi (McMaster University)；Andreas Moshovos (University of Toronto and Vector Institute)。
  - Marple 为 untethered brain-machine interface 实时处理上千/万电极通道，固定功能前端先筛出 spike 区域，灵活 vector backend 完成 neuron identification；新模板表示将最大存储项压缩 8–11 倍，并探索以 ML 替代 template matching。
  - 相较高精度 GPU 离线 sorting 或小规模固定硬件，核心创新是围绕 template-memory 瓶颈设计可扩展的低功耗混合流水线。
  - Brain-Machine Interface、Spike Sorting、模板压缩、低功耗加速、神经信号

- [Manticore: Hardware-Accelerated RTL Simulation with Static Bulk-Synchronous Parallelism](https://doi.org/10.1145/3623278.3624750)
  - Mahyar Emami and Sahand Kashani (EPFL)；Keisuke Kamahori (University of Tokyo)；Mohammad Sepehr Pourghannad (Sharif University)；Ritik Raj (Indian Institute of Technology Roorkee)；James R. Larus (EPFL)。
  - Manticore 是为 cycle-accurate RTL simulation 定制的多核机，以 static bulk-synchronous parallel 模型运行；compiler 根据 RTL 几乎无分支的 dependency 静态分配 core、通信与 barrier，硬件无需复杂动态同步，225 核 FPGA 可并行推进细粒度信号更新。
  - 相较通用 CPU 上动态事件调度，核心创新是把全部通信/同步时序提前编译，使 RTL 的细粒度并行在极简多核硬件上可兑现。
  - RTL 仿真、Bulk-Synchronous Parallel、静态调度、FPGA、硬件验证

- [ORIANNA: An Accelerator Generation Framework for Optimization-based Robotic Applications](https://doi.org/10.1145/3620665.3640379)
  - Yuhui Hao (Tianjin University)；Yiming Gan (Chinese Academy of Sciences)；Bo Yu (Shenzhen Institute of Artificial Intelligence and Robotics for Society)；Qiang Liu (Tianjin University)；Yinhe Han (Chinese Academy of Sciences)；Zishen Wan (Georgia Tech)；Shaoshan Liu (Shenzhen Institute of Artificial Intelligence and Robotics for Society)。
  - ORIANNA 让机器人开发者用 factor graph 描述 SLAM、trajectory optimization 等目标与约束，compiler 将其降为基础矩阵操作，并为应用组合生成可 out-of-order 执行的 FPGA accelerator；共享抽象允许一个设计整合多种优化算法。
  - 相较只加速通用 GEMM 或为每个机器人算法手工做 ASIC，核心创新是以 factor graph 作为自动生成领域加速器的共同 IR。
  - 机器人计算、Factor Graph、加速器生成、FPGA、Out-of-order Matrix Ops

- [AERO: Adaptive Erase Operation for Improving Lifetime and Performance of Modern NAND Flash-Based SSDs](https://doi.org/10.1145/3620666.3651341)
  - Sungjun Cho (POSTECH)；Beomjun Kim (Kyungpook National University)；Hyunuk Cho (POSTECH)；Gyeongseob Seo (Kyungpook National University)；Onur Mutlu (ETH Zürich)；Myungsuk Kim (Kyungpook National University)；Jisung Park (POSTECH)。
  - AERO 不再给每次 NAND erase 固定最坏情况时长，而是先短擦除并读取 fail-bit 数，由器件模型预测当前 block 恰好可靠清空所需的追加时间；算法利用现代 SSD 的 reliability margin 安全缩短高压暴露，兼顾 cell endurance 与前台 read tail latency。
  - 相较所有块套同一 erase pulse schedule，核心创新是用进行中 fail-bit feedback 为每次擦除自适应定时。
  - NAND Flash、SSD 寿命、Adaptive Erase、Fail-bit Prediction、尾延迟

- [BypassD: Enabling fast userspace access to shared SSDs](https://doi.org/10.1145/3617232.3624854)
  - Sujay Yadalam (University of Wisconsin-Madison)；Chloe Alverti (National Technical University of Athens)；Vasileios Karakostas (University of Athens)；Jayneel Gandhi (Meta)；Michael Swift (University of Wisconsin-Madison)。
  - BypassD 让应用像 mmap 文件一样用 virtual address 表示 file offset，kernel 负责建立共享与保护映射，扩展 IOMMU 则把该地址直接翻译为设备 LBA；userspace I/O 可绕过 kernel data path，同时由硬件保证多个进程安全共享 SSD。
  - 相较 SPDK 需独占设备或内核路径开销高，核心创新是把虚拟内存的 translation/protection 抽象延伸到 block device。
  - NVMe SSD、Userspace I/O、IOMMU、共享存储、Virtual Address

- [Eliminating Storage Management Overhead of Deduplication over SSD Arrays Through a Hardware/Software Co-Design](https://doi.org/10.1145/3620665.3640368)
  - Yuhong Wen, Xiaogang Zhao, and You Zhou (Huazhong University of Science and Technology)；Tong Zhang (Rensselaer Polytechnic Institute and ScaleFlux)；Shangjun Yang, Changsheng Xie, and Fei Wu (Huazhong University of Science and Technology)。
  - ARM-Dedup 面向 SSD array 的 block-level dedup，把 host 重复维护的 logical-to-physical metadata 下沉并融合进每块 SSD FTL，同时令 FTL 感知 array-wide duplicate ownership；host 侧 Linux dm-dedup/mdraid 只保留轻量协调，减少 CPU、内存和额外 I/O。
  - 相较 host dedup layer 与各盘 FTL 各自做地址映射，核心创新是构造面向去重且跨盘协同的 FTL，消除双重存储管理。
  - SSD 阵列、数据去重、FTL、硬件软件协同、Block Storage

- [LazyBarrier: Reconstructing Android IO Stack for Barrier-Enabled Flash Storage](https://doi.org/10.1145/3620665.3640370)
  - Yuanyi Zhang, Heng Zhang, Wenbin Cao, Xing He, Daejun Park, Jinyoung Choi, and SungJun Park (Samsung Electronics)。
  - LazyBarrier 为 Android flash stack 建立 finite-automata 的 order-preserving write 模型，Lazy Issue 合并/延后不必要的 barrier write；修改 F2FS 标注依赖，block-layer barrier scheduler 再跨多 queue 保证顺序，使 thread 数增加时 barrier 不再线性膨胀。
  - 相较每线程遇到顺序点就立即发 BWC，核心创新是以全栈依赖状态机惰性生成最少 barrier，并在 multi-queue 统一调度。
  - Android I/O、Flash Storage、Write Barrier、F2FS、持久化顺序

- [Achieving Near-Zero Read Retry for 3D NAND Flash Memory](https://doi.org/10.1145/3620665.3640372)
  - Min Ye (City University of Hong Kong)；Qiao Li (Xiamen University)；Yina Lv (City University of Hong Kong)；Jie Zhang (Peking University)；Tianyu Ren (City University of Hong Kong)；Daniel Wen (YEESTOR Microelectronics)；Tei-Wei Kuo (National Taiwan University)；Chun Jason Xue (City University of Hong Kong and Mohamed bin Zayed University of Artificial Intelligence)。
  - 该方法从不同 3D NAND 芯片实测 page read-voltage 最优 offset 的相关性，为每种 flash model 生成定制 read-retry table；运行时先选最可能电压，再在邻近值做 proximity search，使老化和长 retention data 也几乎一次读成功。
  - 相较厂商固定 RRT 忽略 page 粒度与老化差异，核心创新是用跨电压/页面相关模型生成器件定制表并动态微调。
  - 3D NAND、Read Retry、Read Voltage、SSD 老化、Flash Reliability

- [SmartMem: Layout Transformation Elimination and Adaptation for Efficient DNN Execution on Mobile](https://doi.org/10.1145/3620666.3651384)
  - Wei Niu, Md Musfiqur Rahman Sanim, and Zhihao Shu (University of Georgia)；Jiexiong Guan (William & Mary)；Xipeng Shen (North Carolina State University)；Miao Yin (University of Texas at Arlington)；Gagan Agrawal (University of Georgia)；Bin Ren (William & Mary)。
  - SmartMem 面向 mobile CNN、Swin-like Transformer、Stable Diffusion 与 LLM，把 operator 按 layout tolerance 分四类，沿 producer–consumer edge 搜索可共享的 tensor layout，并为移动设备常见 2.5D memory 设计访问布局，尽量消除算子间 transpose/reformat。
  - 相较逐算子选择最快 kernel 后再插 layout conversion，核心创新是跨整个 graph 以转换消除为目标共同选择 operator implementation 与布局。
  - 移动 DNN 推理、Tensor Layout、Layout Transformation、Transformer、Graph Optimization

- [Dr. DNA: Combating Silent Data Corruptions in Deep Learning using Distribution of Neuron Activations](https://doi.org/10.1145/3620666.3651349)
  - Dongning Ma (Villanova University)；Fred Lin, Alban Desmaison, Joel Coburn, Daniel Moore, and Sriram Sankar (Meta)；Xun Jiao (Villanova University and Meta)。
  - Dr. DNA 在 DNN inference 中监控各层 neuron activation distribution，并从正常分布提取能区分不同 silent data corruption 的 signature；异常在传播到最终预测前即被定位和缓解，用极少 memory/latency overhead 恢复模型输出。
  - 相较只做最终 logits 合理性检查或复制执行，核心创新是把中间激活分布当作跨模型的 SDC 指纹，实现早期检测与定向恢复。
  - DNN 可靠性、Silent Data Corruption、Neuron Activation Distribution、在线检测、错误缓解

- [GPU-based Private Information Retrieval for On-Device Machine Learning Inference](https://doi.org/10.1145/3617232.3624855)
  - Maximilian Lam (Harvard University)；Jeff Johnson (Meta)；Wenjie Xiong (Virginia Tech)；Kiwan Maeng (Pennsylvania State University)；Udit Gupta (Harvard University)；Yang Li, Liangzhen Lai, and Ilias Leontiadis (Meta)；Minsoo Rhu (KAIST and Meta)；Hsien-Hsin S. Lee (Intel)；Vijay Janapa Reddi, Gu-Yeon Wei, and David Brooks (Harvard University)；Edward Suh (Meta and Cornell University)。
  - 该系统让手机保留私有 query，只向 server 以 PIR 协议获取推荐/语言模型所需的 GB 级 embedding row；GPU 并行加速密码查询，PIR 与下游模型共同设计以减少需私取的 embedding 数和表示大小，固定模型质量下进一步提高 QPS。
  - 相较把完整 embedding table 放设备或让服务端看到索引，核心创新是把 GPU-PIR 的密码计算与 ML embedding access pattern 联合优化到实时推理规模。
  - On-device ML、Private Information Retrieval、Embedding Table、GPU 加速、隐私推理

- [RECom: A Compiler Approach to Accelerate Recommendation Model Inference with Massive Embedding Columns](https://doi.org/10.1145/3623278.3624761)
  - Zaifeng Pan (Renmin University of China)；Zhen Zheng (Alibaba)；Feng Zhang and Ruofan Wu (Renmin University of China)；Hao Liang (Alibaba)；Dalin Wang (Renmin University of China)；Xiafei Qiu, Junjie Bai, and Wei Lin (Alibaba)；Xiaoyong Du (Renmin University of China)。
  - RECom 编译含大量 embedding column 的推荐模型时，把数百个小 column operator 融为单个 GPU kernel、每列映射独立 thread block 并保留 inter-column parallelism；符号表达式重建 dynamic shape，graph pass 再利用完整 column context 删除 framework 的冗余健壮性计算。
  - 相较通用 ML compiler 逐小算子生成 kernel，核心创新是把 embedding column 作为可整体编译的领域结构，统一处理融合、动态形状和子图简化。
  - 推荐模型推理、Embedding Column、GPU Compiler、Dynamic Shape、Kernel Fusion

- [NDPipe: Exploiting Near-data Processing for Scalable Inference and Continuous Training in Photo Storage](https://doi.org/10.1145/3620666.3651345)
  - Jungwoo Kim and Seonggyun Oh (DGIST)；Jaeha Kung (Korea University)；Yeseong Kim and Sungjin Lee (DGIST)。
  - NDPipe 在 photo-storage server 内部署低价 GPU，让图像不离开存储节点即可做 inference 与 continuous training；系统切分 DNN、在多存储节点做 data parallel，并以低同步代价聚合更新，同时流水化每台节点的磁盘、网络和 GPU。
  - 相较把全部照片拉到集中 GPU cluster，核心创新是利用大规模存储节点的 collective near-data compute，并针对训练同步设计模型分区。
  - Near-data Processing、照片存储、连续训练、分布式推理、Commodity GPU

- [Exploiting the Regular Structure of Modern Quantum Architectures for Compiling and Optimizing Programs with Permutable Operators](https://doi.org/10.1145/3623278.3624751)
  - Yuwei Jin, Fei Hua, Yanhao Chen, and Ari Hayes (Rutgers University)；Chi Zhang (University of Pittsburgh)；Eddy Z. Zhang (Rutgers University)。
  - 该量子 compiler 利用一组 two-qubit operator 可交换的自由度，将大规模 mapping/scheduling 分解为可在小规模求解的结构化子问题；随后针对 input graph sparsity 和真实硬件 noise variation 调整 gate order 与 placement，在 IBM/Google topology 上降低 depth 与 gate count。
  - 相较固定原电路 gate order 再路由，核心创新是把 operator permutation 与规则硬件 topology 共同利用，并从局部结构解构千 qubit 编译。
  - 量子编译、Permutable Operator、Qubit Routing、结构化求解、噪声感知

- [One Gate Scheme to Rule Them All: Introducing a Complex Yet Reduced Instruction Set for Quantum Computing](https://doi.org/10.1145/3620665.3640386)
  - Jianxin Chen and Dawei Ding (DAMO Academy)；Weiyuan Gong (Harvard University)；Cupjin Huang (DAMO Academy)；Qi Ye (DAMO Academy and Tsinghua University)。
  - 该工作提出可直接实现任意 two-qubit SU(4) operation（差单 qubit gate）的 AshN gate scheme，以少量但表达力强的 native instruction 取代长 CNOT 序列；control parameter 可吸收 transverse-coupling 系统的 ZZ coherent error，并缩短 decoherence 暴露。
  - 相较以 CNOT 为单一二比特基础门，核心创新是“复杂但精简”的量子 ISA：一个连续可调 gate family 覆盖完整双量子比特空间。
  - 量子 ISA、Two-qubit Gate、SU(4)、CRISC、Coherent Error

- [MorphQPV: Exploiting Isomorphism in Quantum Programs to Facilitate Confident Verification](https://doi.org/10.1145/3620666.3651360)
  - Siwei Tan, Debin Xiang, and Liqiang Lu (Zhejiang University)；Junlin Lu (Peking University)；Qiuping Jiang (Ningbo University)；Mingshuai Chen and Jianwei Yin (Zhejiang University)。
  - MorphQPV 让开发者在 tracepoint 标记量子 state，并用 assume-guarantee 声明输入间应保持的 isomorphism；验证器从少量执行近似其他输入的 ground-truth relation，再把 assertion check 建模为带 confidence estimate 的约束优化，减少 state collapse 导致的重复运行。
  - 相较穷举输入 assertion 或不可扩展 deductive proof，核心创新是利用量子程序结构同构，在概率置信度下复用观测状态。
  - 量子程序验证、Isomorphism、Assertion、Assume-Guarantee、Confidence Estimation

- [Fermihedral: On the Optimal Compilation for Fermion-to-Qubit Encoding](https://doi.org/10.1145/3620666.3651371)
  - Yuhao Liu, Shize Che, and Junyu Zhou (University of Pennsylvania)；Yunong Shi (AWS Quantum Technologies)；Gushu Li (University of Pennsylvania)。
  - Fermihedral 把针对具体 fermionic Hamiltonian 的 fermion-to-qubit encoding 选择，用 Pauli algebra 化为 Boolean satisfiability，目标同时压低 implementation cost、gate count 与 circuit depth；对大实例再用两种近似策略限制指数级 clause 数。
  - 相较固定采用 Jordan–Wigner/Bravyi–Kitaev encoding，核心创新是为每个 Hamiltonian 由 SAT solver 搜索最优编码。
  - 量子模拟、Fermion-to-Qubit、SAT、Pauli Algebra、量子编译

- [OnePerc: A Randomness-aware Compiler for Photonic Quantum Computing](https://doi.org/10.1145/3620666.3651372)
  - Hezi Zhang and Jixuan Ruan (University of California San Diego)；Hassan Shapourian and Ramana Rao Kompella (Cisco Systems)；Yufei Ding (University of California San Diego)。
  - OnePerc 面向 photonic quantum computing 中 fusion operation 随机成功的问题，以专用 IR 连接 offline plan 和 online reaction：离线安排可扩展资源/依赖，执行时根据实际 fusion outcome 快速重路由和补救，使成功概率与额外 photon/resource 成本共同受控。
  - 相较把 probabilistic fusion 当作固定失败率留冗余，核心创新是 compiler 在离线和在线两个阶段显式消费随机结果。
  - Photonic Quantum Computing、随机感知编译、Fusion Operation、在线重调度、量子 IR

- [FPGA Technology Mapping Using Sketch-Guided Program Synthesis](https://doi.org/10.1145/3620665.3640387)
  - Gus Henry Smith, Benjamin Kushigian, Vishal Canumalla, and Andrew Cheung (University of Washington)；Steven Lyubomirsky (OctoAI)；Sorawee Porncharoenwase, René Just, Gilbert Louis Bernstein, and Zachary Tatlock (University of Washington)。
  - Lakeroad 从 FPGA architecture 描述和厂商 primitive simulation model 提取语义，用 architecture-independent sketch template 表示待填映射，再由 program synthesis 寻找与输入 HDL 等价、能充分利用 DSP 等复杂 primitive 的实现，并给出正确性保证。
  - 相较厂商工具手写 special-case mapping rule，核心创新是以 sketch-guided synthesis 从器件语义自动发现更多技术映射。
  - FPGA Technology Mapping、Program Synthesis、Sketch、DSP Primitive、HDL

- [TAPA-CS: Enabling Scalable Accelerator Design on Distributed HBM-FPGAs](https://doi.org/10.1145/3620666.3651347)
  - Neha Prakriya, Yuze Chi, Suhail Basalama, Linghao Song, and Jason Cong (University of California Los Angeles)。
  - TAPA-CS 接收 task-parallel dataflow accelerator，自动把 task graph 分区到多块带 HBM 的云 FPGA，在 100Gbps 网络上做 congestion control、resource balance 和 communication–computation overlap；粗粒度 floorplan 与跨/片内 interconnect pipeline 共同维持时钟频率。
  - 相较单 FPGA HLS 或人工拆分 bitstream，核心创新是把 multi-FPGA partition、网络流控和 physical pipelining 统一到编译框架。
  - 多 FPGA、HBM、Task-parallel Dataflow、自动分区、云加速器

- [Zoomie: A Software-like Debugging Tool for FPGAs](https://doi.org/10.1145/3620666.3651356)
  - Tianrui Wei and Kevin Laeufer (University of California Berkeley)；Katie Lim (University of Washington)；Jerry Zhao and Koushik Sen (UC Berkeley)；Jonathan Balkind (University of California Santa Barbara)；Krste Asanovic (University of California Berkeley)。
  - Zoomie 为 million-gate FPGA design 保存增量编译和验证状态，只重编受修改影响的部分，并提供类似软件 debugger 的 breakpoint、single-step 和运行中 force value；同一开源 emulation infrastructure 可在原型验证与加速器开发间复用。
  - 相较每次调用 vendor toolchain 做全量 place-and-route，核心创新是把增量构建与交互式调试一起带到 FPGA 硬件执行。
  - FPGA Debugging、增量编译、Breakpoint、Hardware Emulation、敏捷硬件开发

- [HIR: An MLIR-based Intermediate Representation for Hardware Accelerator Description](https://doi.org/10.1145/3623278.3624767)
  - Kingshuk Majumder and Uday Bondhugula (Indian Institute of Science)。
  - HIR 是面向 affine accelerator 的 MLIR dialect，以 datapath+explicit schedule 取代 datapath+手写 FSM；compiler 从 schedule 自动综合控制状态机，高层 loop/tensor 与时间表可表达细粒度无同步并行、loop pipeline 及多 kernel overlap。
  - 相较 Verilog FSM 或封闭 HLS IR，核心创新是把硬件时间调度作为一等 IR，同时复用 MLIR 软件编译生态的 pass 和工具。
  - MLIR、硬件 IR、FPGA 加速器、Schedule、FSM Synthesis

- [FaaSGraph: Enabling Scalable, Efficient, and Cost-Effective Graph Processing with Serverless Computing](https://doi.org/10.1145/3620665.3640361)
  - Yushi Liu, Shixuan Sun, Zijun Li, and Quan Chen (Shanghai Jiao Tong University)；Sen Gao and Bingsheng He (National University of Singapore)；Chao Li and Minyi Guo (Shanghai Jiao Tong University)。
  - FaaSGraph 为大图设计 data-centric serverless execution model，把 graph partition/数据作为长期管理中心，函数围绕数据被触发和弹性扩缩；图处理 paradigm 与数据位置协同，减少传统无状态函数反复拉取图状态，在波动负载下控制 p99 和成本。
  - 相较把 IaaS 图 engine 的 worker 直接换成 FaaS，核心创新是从数据驻留和图迭代语义重新设计 serverless-native execution。
  - Serverless Graph Processing、Data-centric Execution、弹性计算、图分区、成本优化

- [In-Storage Domain-Specific Acceleration for Serverless Computing](https://doi.org/10.1145/3620665.3640413)
  - Rohan Mahapatra, Soroush Ghodrati, Byung Hoon Ahn, Sean Kinzer, Shu-Ting Wang, Hanyang Xu, and Lavanya Karthikeyan (University of California San Diego)；Hardik Sharma (Google)；Amir Yazdanbakhsh (Google DeepMind)；Mohammad Alian (University of Kansas)；Hadi Esmaeilzadeh (University of California San Diego)。
  - DSCS-Serverless 把小型 domain-specific accelerator 放进 computational storage，在数据所在设备内执行 serverless function 的核心 kernel，避免先经解耦网络把输入搬到远端 GPU；设计受 25W storage power budget 约束，并重新权衡 microprocessor、FPGA 与专用 datapath。
  - 相较 disaggregated storage 外接强 GPU，核心创新是让 accelerator 与数据共址并针对 serverless/存储功耗边界定制，而非照搬通用 computational storage。
  - Serverless、Computational Storage、领域加速器、存算解耦、Near-data Processing

- [FUYAO: DPU-enabled Direct Data Transfer for Serverless Computing](https://doi.org/10.1145/3620666.3651327)
  - Guowei Liu, Laiping Zhao, Yiming Li, Zhaolin Duan, Sheng Chen, and Yitao Hu (Tianjin University)；Zhiyuan Su (Inspur Electronic Information Industry)；Wenyu Qu (Tianjin University)。
  - FUYAO 将 serverless workflow 的 control message 与 intermediate data path 分离，由 DPU 建立函数间直接传输；根据同节点/跨节点、一次性/频繁通信选择四种通道，对高频 function pair 保持 stateful direct connection，把数据转发降到亚毫秒。
  - 相较所有数据经对象存储、gateway 或 orchestrator 第三方转发，核心创新是以 DPU 控制并执行多形态的 function-to-function direct path。
  - Serverless 数据传输、DPU、函数直连、Control/Data Plane 分离、低延迟 Workflow

- [DataFlower: Exploiting the Data-flow Paradigm for Serverless Workflow Orchestration](https://doi.org/10.1145/3623278.3624755)
  - Zijun Li, Chuhao Xu, Quan Chen, Jieru Zhao, Chen Chen, and Minyi Guo (Shanghai Jiao Tong University)。
  - DataFlower 将每个 serverless container 拆为执行函数的 function logic unit 和异步搬数据的 data logic unit，后者在上游产生数据时立即向下游传输并触发，而非等待函数结束和持久化；host–container 通信层负责跨实例高效流动。
  - 相较 control-flow orchestrator 串行执行—落盘—触发，核心创新是将数据到达变为调度信号，并让计算与传输在容器内并行。
  - Serverless Workflow、Dataflow、异步数据传输、函数编排、尾延迟

- [Fractal: Joint Multi-Level Sparse Pattern Tuning of Accuracy and Performance for DNN Pruning](https://doi.org/10.1145/3620666.3651351)
  - Yue Guan, Changming Yu, Yangjie Zhou, Jingwen Leng, Chao Li, and Minyi Guo (Shanghai Jiao Tong University and Shanghai Qizhi Institute)。
  - Fractal 把 structured sparsity 统一解释为 tensor 被多级 tiling 后在各层跳过计算，以 PatternIR 表达 block、sub-block 等组合 pattern；auto-tuner 联合搜索能保持 accuracy 的 pruning pattern 与 GPU CUDA/Tensor Core 上的低层 schedule。
  - 相较只在单一 tile level 选 N:M 或 block sparsity，核心创新是开放 multi-level sparse tiling 空间，并以统一 IR 连接剪枝与 codegen。
  - DNN Pruning、多级稀疏、PatternIR、Tensor Core、Accuracy-Performance Tuning

- [Optimizing Dynamic-Shape Neural Networks on Accelerators via On-the-Fly Micro-Kernel Polymerization](https://doi.org/10.1145/3620665.3640390)
  - Feng Yu, Guangli Li, Jiacheng Zhao, Huimin Cui, and Xiaobing Feng (Chinese Academy of Sciences)；Jingling Xue (University of New South Wales)。
  - MikPoly 预先生成覆盖不同 shape region 的高性能 micro-kernel；operator 的实际 tensor shape 到运行时确定后，轻量 cost model 选择并“聚合”若干 micro-kernel 组成完整实现，在 GPU Tensor Core 与 Ascend NPU 上避免现场做重型编译。
  - 相较为每个 dynamic shape 即时 autotune 或退回通用 kernel，核心创新是把昂贵优化前移为 micro-kernel 库，仅在运行时做快速 polymerization。
  - Dynamic Shape、Tensor Compiler、Micro-kernel Polymerization、Tensor Core、Ascend NPU

- [DTC-SpMM: Bridging the Gap in Accelerating General Sparse Matrix Multiplication with Tensor Cores](https://doi.org/10.1145/3620666.3651378)
  - Ruibo Fan, Wei Wang, and Xiaowen Chu (Hong Kong University of Science and Technology)。
  - DTC-SpMM 针对任意 sparsity 的矩阵，联合使用适合 Tensor Core tile 的压缩格式、row/column reordering 和 runtime pipeline，让可填满 dense MMA 的非零块连续供给，同时处理不规则残余，最终也加速 GNN training。
  - 相较只对特定 block sparsity 有效的 TC-SpMM，核心创新是系统补齐格式、重排与流水三个缺口，使 general sparse matrix 也能稳定利用 Tensor Core。
  - SpMM、Tensor Core、稀疏格式、矩阵重排、GNN 训练

- [SoD2: Statically Optimizing Dynamic Deep Neural Network Execution](https://doi.org/10.1145/3617232.3624869)
  - Wei Niu and Gagan Agrawal (University of Georgia)；Bin Ren (William & Mary)。
  - SoD² 先按 operator 的 shape behavior 分类，用 Rank and Dimension Propagation 将每个维度推导为常数、符号常数或符号运算；编译器据此在运行前完成可确定部分的 fusion、execution order 与 memory allocation plan，只把真正动态的值留到 runtime。
  - 相较把 dynamic DNN 全部交给 runtime，核心创新是以 RDP 精确区分静态、符号和动态 shape，扩大可静态优化边界。
  - 动态 DNN、Shape Analysis、Rank-Dimension Propagation、Memory Planning、Operator Fusion

- [SEVeriFast: Minimizing the root of trust for fast startup of SEV microVMs](https://doi.org/10.1145/3620665.3640424)
  - Benjamin Holmes (MIT and Vassar College)；Jason Waterman (Vassar College)；Dan Williams (Virginia Tech)。
  - SEVeriFast 面向 confidential serverless 的 AMD SEV microVM cold boot，重新组织 bootstrap 和 measurement：引入极小额外组件、重新压缩 guest kernel，反而减少需进入 root of trust 和启动关键路径测量的字节，同时保留常见 fast-boot 跳阶段优化。
  - 相较普通 microVM 一味删除 bootstrap stage，核心创新是围绕 SEV measurement cost 最小化可信基，而非最小化组件数量。
  - AMD SEV、Confidential Serverless、MicroVM、Root of Trust、Cold Start

- [sIOPMP: Scalable and Efficient I/O Protection for TEEs](https://doi.org/10.1145/3620665.3640378)
  - Erhu Feng (Shanghai Jiao Tong University)；Dahu Feng (Tsinghua University)；Dong Du and Yubin Xia (Shanghai Jiao Tong University)；Wenbin Zheng and Siqi Zhao (Alibaba DAMO Academy)；Haibo Chen (Shanghai Jiao Tong University)。
  - sIOPMP 为 TEE 的 DMA request 做硬件 physical-memory permission check：multi-stage tree 支持千级 region，设备按访问热度分 hot/cold，有限快速 entry 可动态挂载/重映射热门设备，冷设备仍可无限扩展；避免每次 I/O 经过完整 IOMMU 或 trusted software。
  - 相较以 CPU 页表式 IOMMU 处理设备，核心创新是按 I/O isolation 特征设计可伸缩 region checker 与热度驱动 entry virtualization。
  - TEE I/O 隔离、DMA Protection、sIOPMP、IOMMU、Device Remapping

- [A Midsummer Night’s Tree: Efficient and High Performance Secure SCM](https://doi.org/10.1145/3620666.3651354)
  - Samuel Thomas (Brown University)；Kidus Workneh (University of Colorado Boulder)；Jac McCarty (Bryn Mawr College)；Joseph Izraelevitz and Tamara Lehman (University of Colorado Boulder)；R. Iris Bahar (Colorado School of Mines)。
  - AMNT 为 storage-class memory 的加密完整性维护 crash-consistent Bonsai Merkle Tree，在主树内部嵌入小型持久化子树，software 负责复杂的 lazy propagation/recovery protocol，硬件只保留受限 on-chip metadata；power failure 后可重建一致状态。
  - 相较用大量片上缓存换取 lazy BMT update，核心创新是“tree within a tree”将一致性 bookkeeping 下沉软件，显著降低可信硬件面积。
  - Secure SCM、Bonsai Merkle Tree、Crash Consistency、Integrity Metadata、软硬协同

- [Veil: A Protected Services Framework for Confidential Virtual Machines](https://doi.org/10.1145/3623278.3624763)
  - Adil Ahmad (Arizona State University)；Botong Ou and Congyu Liu (Purdue University)；Xiaokuan Zhang (George Mason University)；Pedro Fonseca (Purdue University)。
  - Veil 在 AMD SEV confidential VM 内利用 VMPL 部署高权限 security monitor，把敏感程序/系统服务从庞大 commodity guest kernel 隔离；framework 在有限 VMPL 上复用出任意数量 secure domain，并优化 domain switch 与资源共享，普通 workload 几乎不经 monitor。
  - 相较把整个 guest OS 都放进 CVM TCB，核心创新是在同一 VM 内以 VMPL 再分 privilege domain，同时保持内核兼容。
  - Confidential VM、AMD SEV、VMPL、Protected Service、Guest Kernel 隔离

- [Accelerating Multi-Scalar Multiplication for Efficient Zero Knowledge Proofs with Multi-GPU Systems](https://doi.org/10.1145/3620666.3651364)
  - Zhuoran Ji and Zhiyuan Zhang (Shandong University)；Jiming Xu (Ant Group)；Lei Ju (Shandong University)。
  - DistMSM 将 ZKP proof generation 中占主导的 multi-scalar multiplication 扩展到多 GPU，重构 Pippenger bucket 分工和跨卡归并；GPU kernel 降低 elliptic-curve arithmetic 的 register pressure，并用 Tensor Core 加速特定大整数乘法。
  - 相较单 GPU MSM 或简单平均分 bucket，核心创新是同时解决分布式扩展瓶颈和现代 GPU 椭圆曲线 kernel 利用率。
  - Zero-Knowledge Proof、Multi-Scalar Multiplication、多 GPU、Pippenger、椭圆曲线

- [LazyDP: Co-Designing Algorithm-Software for Scalable Training of Differentially Private Recommendation Models](https://doi.org/10.1145/3620665.3640384)
  - Juntaek Lim, Youngeun Kwon, and Ranggi Hwang (KAIST)；Kiwan Maeng (Pennsylvania State University)；Edward Suh (FAIR at Meta and Cornell University)；Minsoo Rhu (KAIST)。
  - LazyDP 分析 DP-SGD 训练 recommendation model 的 noise sampling 计算瓶颈和 noisy gradient update 带宽瓶颈，利用 embedding access 的稀疏性惰性生成/应用噪声，只在参数真正被触及或需要提交时物化，同时保持与标准 DP 算法数学等价。
  - 相较为巨大 embedding table 每步密集采样并更新噪声，核心创新是把 DP 操作延迟到稀疏访问点，以算法等价性换掉无用工作。
  - Differential Privacy、推荐模型训练、DP-SGD、Lazy Noise、Embedding

- [BitPacker: Enabling High Arithmetic Efficiency in Fully Homomorphic Encryption Accelerators](https://doi.org/10.1145/3620665.3640397)
  - Nikola Samardzic and Daniel Sanchez (MIT)。
  - BitPacker 重构 CKKS ciphertext 的 residue/limb layout，将原本 30–60 bit、会浪费 datapath 高位的整数紧密打包进固定 word，运算时保持接近满宽 multiplier utilization；改变的是 FHE 软件表示，可直接运行在既有 accelerator 而不降精度。
  - 相较为 CKKS 最大 modulus 宽度配置每条算术通道，核心创新是从密码方案实现层对齐 accelerator word，使不同 bit-width residue 共用完整算力。
  - Fully Homomorphic Encryption、CKKS、Bit Packing、FHE Accelerator、算术利用率

- [ZENO: A Type-based Optimization Framework for Zero Knowledge Neural Network Inference](https://doi.org/10.1145/3617232.3624852)
  - Boyuan Feng, Zheng Wang, Yuke Wang, Shu Yang, and Yufei Ding (University of California Santa Barbara)。
  - ZENO language 保留 neural network tensor 结构和每个值的 privacy type，compiler 据此在 zkSNARK circuit 中跨 scalar gate 做公开/私有值消除、tensor-level fusion 与 NN-specific layout/parallel optimization，将 VGG16 等 proof time 从分钟级压低。
  - 相较先把 NN 完全降为无类型算术电路再优化，核心创新是让 privacy 和 tensor type 一直保留到证明 circuit 优化阶段。
  - Zero-Knowledge ML、zkSNARK、类型系统、隐私推理、Tensor Optimization

- [Performance-aware Scale Analysis with Reserve for Homomorphic Encryption](https://doi.org/10.1145/3617232.3624870)
  - Yongwoo Lee, Seonyoung Cheon, and Dongkwan Kim (Yonsei University)；Dongyoon Lee (Stony Brook University)；Hanjun Kim (Yonsei University)。
  - 该 RNS-CKKS compiler 从 program 末端反向计算每个 ciphertext 尚可容纳的 scale budget（reserve），再把预算重新分配到前驱，决定哪些 multiplication 后必须 rescale、哪些可延后，从而减少昂贵 rescale 而不做组合搜索；type system 保证 scale/capacity 正确。
  - 相较保守地每次乘法后 rescale 或枚举管理方案，核心创新是以 backward reserve analysis 直接生成性能感知的静态计划。
  - Homomorphic Encryption、RNS-CKKS、Scale Management、静态分析、类型系统

- [Heet: Accelerating Elastic Training in Heterogeneous Deep Learning Clusters](https://doi.org/10.1145/3620665.3640375)
  - Zizhao Mo, Huanle Xu, and Chengzhong Xu (University of Macau)。
  - Heet 面向 GPU 型号、算力和网络均异构的 elastic training cluster，以 3-D collaborative filtering 从少量 profile 推断作业在各种 host 数/组合上的 scaling efficiency；price function 平衡扩容收益与资源碎片，再用 minimum-weight bipartite matching 和 opportunistic trading 动态放置。
  - 相较只按 GPU 数量弹性扩缩，核心创新是低成本补全异构配置性能面，并将 scaling efficiency 直接写入调度价格。
  - 弹性训练、异构 GPU 集群、Collaborative Filtering、Bipartite Matching、作业调度

- [Efficient Microsecond-scale Blind Scheduling with Tiny Quanta](https://doi.org/10.1145/3620665.3640381)
  - Zhihong Luo, Sam Son, and Dev Bali (University of California Berkeley)；Emmanuel Amaro (VMware Research)；Amy Ousterhout (University of California San Diego)；Sylvia Ratnasamy (University of California Berkeley)；Scott Shenker (ICSI and University of California Berkeley)。
  - Tiny Quanta 面向执行时间未知的微秒级 datacenter task，以 forced multitasking 强制可抢占执行，再用两级 scheduler 将全局 fairness/priority 与每核极小 quanta dispatch 分离；即使不知道 job-size distribution，也可避免长任务阻塞短任务并控制 p99。
  - 相较非抢占 blind scheduler 或在中心调度每个微任务，核心创新是用硬/软协作的强制细粒度抢占加层次化决策承受微秒调度频率。
  - 数据中心调度、Microsecond Task、Blind Scheduling、Preemption、Tail Latency

- [AUDIBLE: A Convolution-Based Resource Allocator for Oversubscribing Burstable Virtual Machines](https://doi.org/10.1145/3620666.3651376)
  - Seyedali Jokar Jandaghi and Kaveh Mahdaviani (University of Toronto)；Amirhossein Mirhosseini (University of Michigan)；Sameh Elnikety (Microsoft Research)；Cristiana Amza and Bianca Schroeder (University of Toronto)。
  - AUDIBLE 从云厂商 production trace 建模 burstable VM 的瞬时 CPU demand，不假设正态分布，而以 non-parametric convolution 合成同机 BVM 总需求分布；allocator 据 capacity-violation probability 选择可共置集合，在给定风险上限下最大化 oversubscription。
  - 相较固定超卖比或中央极限定理近似，核心创新是直接卷积经验需求分布，无需训练 workload-specific ML model 也能给尾部容量保证。
  - Burstable VM、资源超卖、Non-parametric Model、Convolution、Capacity Risk

- [CPS: A Cooperative Para-virtualized Scheduling Framework for Manycore Machines](https://doi.org/10.1145/3623278.3624762)
  - Yuxuan Liu, Tianqiang Xu, Zeyu Mi, Zhichao Hua, Binyu Zang, and Haibo Chen (Shanghai Jiao Tong University)。
  - CPS 让 KVM hypervisor 与 guest scheduler 双向交换最新 pCPU load、vCPU–pCPU mapping、cache-group 等 runtime state；guest 据真实 host 拥塞放线程，host 也知道 guest 的 runnable/affinity intent，从而避免 manycore 上双层调度各自基于过期信息。
  - 相较只处理锁持有者被抢占或静态 NUMA，核心创新是建立持续 para-virtualized scheduling channel，解决不可见 hypervisor state。
  - 虚拟化调度、KVM、Manycore、Para-virtualization、Runtime State Sharing

- [PrimePar: Efficient Spatial-temporal Tensor Partitioning for Large Transformer Model Training](https://doi.org/10.1145/3620666.3651357)
  - Haoran Wang, Lei Wang, Haobo Xu, Ying Wang, Yuming Li, and Yinhe Han (Chinese Academy of Sciences)。
  - PrimePar 将 LLM tensor operator 不只按 device 的空间维切分，还允许 sub-operator 在时间维错开分布；optimizer 搜索 spatial-temporal partition，使某些中间结果在使用时本地生成、减少 collective，并把剩余通信塞入计算空隙，同时降低 peak memory。
  - 相较仅枚举 data/tensor/pipeline 的空间切分，核心创新是把时间分布加入 tensor partition primitive，拓展通信规避与重叠空间。
  - LLM 训练、Tensor Partition、时空并行、Collective Avoidance、显存优化

- [AdaPipe: Optimizing Pipeline Parallelism with Adaptive Recomputation and Partitioning](https://doi.org/10.1145/3620666.3651359)
  - Zhenbo Sun, Huanqi Cao, Yuanwei Wang, Guanyu Feng, Shengqi Chen, Haojie Wang, and Wenguang Chen (Tsinghua University)。
  - AdaPipe 为 GPT-3/Llama 2 pipeline parallelism 联合决定 stage boundary 和每个 activation 是否 recompute；它按 stage 实际 memory headroom 自适应选择重计算量，先压到容量内再平衡各 stage compute，使最慢 stage 不因统一 checkpoint policy 成为 bubble 来源。
  - 相较所有 stage 使用相同重计算策略或先分区后补救内存，核心创新是让 memory-aware recomputation 与 pipeline partition 同时优化。
  - LLM 训练、Pipeline Parallelism、Adaptive Recomputation、Stage Partition、GPU NPU

- [EVT: Accelerating Deep Learning Training with Epilogue Visitor Tree](https://doi.org/10.1145/3620666.3651369)
  - Zhaodong Chen (University of California Santa Barbara)；Andrew Kerr, Richard Cai, Jack Kosaian, and Haicheng Wu (NVIDIA)；Yufei Ding (University of California San Diego)；Yuan Xie (The Hong Kong University of Science and Technology)。
  - EVT 对 training graph 的 forward/backward 联合做 graph pass，暴露 normalization、loss、reduction 等可并入 GEMM epilogue 的子图；ILP partitioner 找合法且收益最大的 fusion，Epilogue Visitor Abstraction 再组合 CUTLASS mainloop 与灵活 epilogue 生成高性能 CUDA kernel。
  - 相较 inference-oriented compiler 只融合简单 producer-consumer，核心创新是联合前反向依赖求解复杂 fusion，并以 visitor tree 复用成熟主循环。
  - DNN 训练编译、Kernel Fusion、Forward-Backward Graph、CUTLASS、ILP

- [Slapo: A Schedule Language for Progressive Optimization of Large Deep Learning Model Training](https://doi.org/10.1145/3620665.3640399)
  - Hongzheng Chen (Cornell University)；Cody Hao Yu and Shuai Zheng (Boson AI)；Zhen Zhang (Amazon Web Services)；Zhiru Zhang (Cornell University)；Yida Wang (Amazon Web Services)。
  - Slapo 在不改 PyTorch model definition 的情况下，用 schedule primitive 逐步附加高性能 kernel、3D parallelism、activation checkpointing 等执行策略；用户可只优化热点模块、保留 eager debugging，并把手工 Megatron/DeepSpeed 技巧系统化组合到 8–64 GPU。
  - 相较把模型重写为某一专用训练框架，核心创新是将大模型执行 schedule 与模型语义分离，支持按需、渐进和可调试的优化。
  - 大模型训练、Schedule Language、PyTorch、3D Parallelism、Activation Checkpointing

- [BVAP: Energy and Memory Efficient Automata Processing for Regular Expressions with Bounded Repetitions](https://doi.org/10.1145/3620665.3640412)
  - Ziyuan Wen, Lingkun Kong, Alexis Le Glaunec, Konstantinos Mamouras, and Kaiyuan Yang (Rice University)。
  - BVAP 为含 bounded repetition 的 regex 建立 Action-Homogeneous Nondeterministic Bit Vector Automata，将重复次数和状态集合编码为位向量动作；compiler 把 regex 转成配置，in-memory processor 并行更新位向量，避免传统 automata 为 {m,n} 展开大量状态。
  - 相较现有 PIM automata 不支持或膨胀展开 bounded repeat，核心创新是新的 AH-NBVA 理论模型与相配的位向量硬件。
  - Regular Expression、Automata Processor、Processing-in-Memory、Bounded Repetition、Bit Vector

- [IANUS: Integrated Accelerator based on NPU-PIM Unified Memory System](https://doi.org/10.1145/3620666.3651324)
  - Minseok Seo and Xuan Truong Nguyen (Seoul National University and Inter-university Semiconductor Research Center)；Seok Joong Hwang (SAPEON)；Yongkee Kwon, Guhyun Kim, Chanwook Park, Ilkon Kim, Jaehan Park, Jeongbin Kim, Woojae Shin, Jongsoon Won, Haerang Choi, Kyuyoung Kim, Daehan Kwon, and Chunseok Jeong (SK hynix)；Sangheon Lee, Yongseok Choi, Wooseok Byun, and Seungcheol Baek (SAPEON)；Hyuk-Jae Lee (Seoul National University and Inter-university Semiconductor Research Center)；John Kim (KAIST)。
  - IANUS 用统一 main memory 同时服务 NPU 普通读写和 PIM operation，LLM 的 compute-bound kernel 映射 NPU、bandwidth-bound kernel 映射 PIM，无需在两个独立内存池复制 shared tensor；PIM Access Scheduler 协调不能同时发生的普通访问与存内计算，并做 workload mapping。
  - 相较 NPU+PIM 各自有内存再搬数据，核心创新是 unified memory architecture 加专用访问调度，实现端到端 LLM 推理而非单阶段加速。
  - LLM 推理、NPU-PIM、Unified Memory、PIM Scheduling、异构加速

- [PIM-STM: Software Transactional Memory for Processing-In-Memory Systems](https://doi.org/10.1145/3620665.3640428)
  - André Lopes, Daniel Castro, and Paolo Romano (IST/INESC-ID)。
  - PIM-STM 在商用 UPMEM 上实现多种 software transactional memory protocol，比较 versioning、conflict detection 和 commit 方案，并把 transaction metadata 分别放在低延迟小容量或高容量较慢的 PIM memory tier；由 workload contention 和 footprint 选择实现。
  - 相较把 CPU STM 原样移植，核心创新是系统探索 PIM core/多级内存约束下的 TM 设计空间，并给出可用库。
  - Processing-in-Memory、Software Transactional Memory、UPMEM、Conflict Detection、Memory Tier

- [CIM-MLC: A Multi-level Compilation Stack for Computing-In-Memory Accelerators](https://doi.org/10.1145/3620665.3640359)
  - Songyun Qu and Shixin Zhao (Chinese Academy of Sciences)；Bing Li (Capital Normal University)；Yintao He, Xuyi Cai, Lei Zhang, and Ying Wang (Chinese Academy of Sciences)。
  - CIM-MLC 用通用 hardware abstraction 描述 CIM device precision、crossbar size/count、computing granularity 与 programming interface，并分 device/circuit/array/system 多级降低；compiler 跨层搜索 mapping、scheduling 和 instruction generation，适配不同 CIM accelerator。
  - 相较每种 CIM 架构自建单层 compiler，核心创新是以多级抽象同时容纳器件差异和跨层优化，而非只调 crossbar-bound MVM。
  - Computing-in-Memory、多级编译、Crossbar、硬件抽象、Mapping Scheduling
