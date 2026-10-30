# ASPLOS 2026 论文列表

- 范围：ASPLOS 2026 官方主会议程中的 regular paper card；排除 workshop、tutorial、poster、keynote。
- 边界审计：官网页眉写“167 unique papers”，但 2026-09-20 保存页与当前在线页均实际解析出 168 个 paper card，且标题与作者集合均无重复。为避免任意漏删，本列表按 168 篇列全，方向统计也以 168 为分母。
- DOI 对齐：20 篇对应 ASPLOS 2026 Volume 1（parent DOI 10.1145/3760250），132 篇对应 Volume 2（10.1145/3779212）；其余 16 个官方节目单 card 可逐项对齐 ASPLOS 2025 Volume 3（10.1145/3676642）DOI，说明不能只按 Crossref 出版年份筛选会议现场内容。
- 证据：标题、作者和机构以官方 program 为准，标题链接指向 DOI；53 篇有可核验 arXiv 预印本，另保存 PF-LLM 的作者机构公开版，共 54 份 PDF。无公开摘要/正文的条目明确限制为标题级预读，不推断未公开机制。

## 主会论文

- [Towards High-Goodput LLM Serving with Prefill-decode Multiplexing](https://doi.org/10.1145/3779212.3790236)
  - Weihao Cui (Shanghai Jiao Tong University), Yukang Chen (Shanghai Jiao Tong University), Han Zhao (Shanghai Jiao Tong University), Ziyi Xu (Shanghai Jiao Tong University), Xiaoze Fan (Shanghai Jiao Tong University), Xusheng Chen (University of Hong Kong), Yangjie Zhou (National University of Singapore), Shixuan Sun (Shanghai Jiao Tong University), Bingsheng He (National University of Singapore), Quan Chen (Shanghai Jiao Tong University)
  - MuxWise 面向同时受 TTFT/TPOT SLO 约束的在线 LLM 请求，在同一 GPU 内让 prefill 与 decode 独立执行并复用算力；无气泡复用引擎、抗争用估计器和 SLO-aware dispatcher 根据实时争用调整两阶段资源，避免分离部署的空闲与 chunked-prefill 的相互阻塞。
  - 核心创新是把 prefill/decode 的复用粒度推进到单 GPU 内部，并把算力调度与 KV 内存管理解耦；相较固定切分或混合 batch，直接针对阶段间硬件互补性做动态分配。
  - LLM 与生成式 AI 系统；MuxWise；阶段复用；LLM

- [Bullet: Boosting GPU Utilization for LLM Serving via Dynamic Spatial-Temporal Orchestration](https://doi.org/10.1145/3779212.3790135)
  - Zejia Lin (Sun Yat-sen University), Hongxin Xu (Sun Yat-sen University), Guanyi Chen (Sun Yat-sen University), Zhiguang Chen (Sun Yat-sen University), Yutong Lu (Sun Yat-sen University), Xianwei Zhang (Sun Yat-sen University)
  - Bullet 针对 compute-bound prefill 与 memory-bound decode 共置时的 SM 和带宽空洞，以实时性能模型观测阶段负载，在空间上分配 SM、在时间上并发编排两阶段，并以 SLO-aware 调度在延迟约束内提高 GPU 利用率。
  - 核心创新是把混合 batch 的粗粒度折中改成可伸缩的空间-时间资源编排：阶段共享权重/KV 映射，但运行时按模型预测细调 GPU 资源。
  - LLM 与生成式 AI 系统；Bullet；SM 分配；LLM；GPU

- [QoServe: Breaking the Silos of LLM Inference Serving](https://doi.org/10.1145/3779212.3790206)
  - Kanishk Goel (Microsoft Research India), Jayashree Mohan (Microsoft Research India), Nipun Kwatra (Microsoft Research India), Ravi Anupindi (Microsoft Research India), Ram Ramjee (Microsoft Research India)
  - QoServe 将交互式与批量 LLM 请求放入共享集群，按请求声明的细粒度延迟目标分类，并依据队列和执行状态动态 chunk、混合优先级与选择性降级；目标是在过载时仍区分不同 QoS，而不是只提供统一的 SLO。
  - 核心创新是打破按 workload silo 独立部署的做法，把细粒度 QoS、实时状态调度和过载降级统一到同一 serving plane。
  - LLM 与生成式 AI 系统；QoServe；QoS；多租户；LLM

- [Shift Parallelism: Low-Latency, High-Throughput LLM Inference for Dynamic Workloads](https://doi.org/10.1145/3779212.3790219)
  - Mert Hidayetoglu (Snowflake), Aurick Qiao (Snowflake), Michael Wyatt (Snowflake), Jeff Rasley (Snowflake), Yuxiong He (Snowflake), Samyam Rajbhandari (Snowflake)
  - Shift Parallelism 面向到达率随时间变化的生产推理流量，在低负载使用 tensor parallel 降低单请求延迟，在高负载切换到保持 KV cache 布局不变的 sequence parallel 提升吞吐，从而避免 TP 与 DP 切换需要重排 KV cache。
  - 核心创新是利用推理版 sequence parallel 的 KV-cache invariance，使并行策略能在线切换；既有 TP/DP 方案通常只能在低延迟和高吞吐之间静态选边。
  - LLM 与生成式 AI 系统；并行策略切换；动态流量；LLM

- [XY-Serve: End-to-End Versatile Production Serving for Dynamic LLM Workloads](https://doi.org/10.1145/3760250.3762228)
  - Mingcong Song (Huawei Technologies Co., Ltd.), Xinru Tang (Tsinghua University, BNRist), Fengfan Hou (Huawei Technologies Co., Ltd.), Jing Li (Huawei Technologies Co., Ltd.), Wei Wei (Huawei Technologies Co., Ltd.), Yipeng Ma (Huawei Technologies Co., Ltd.), Runqiu Xiao (Huawei Technologies Co., Ltd.), Hongjie Si (Huawei Technologies Co., Ltd.), Dingcheng Jiang (Tsinghua University, BNRist), Shouyi Yin (Tsinghua University, BNRist and Shanghai AI Laboratory), Yang Hu (Tsinghua University, BNRist), Guoping Long (Huawei Technologies Co., Ltd.)
  - 官方标题和主会议程可确认 XY-Serve 是面向动态 LLM workload 的端到端生产 serving 系统；当前未找到可核验的公开摘要或正文，因而不能确认其请求粒度、状态观测、并行策略和生产评测配置。
  - 标题可确认的差异是把动态负载适配覆盖到端到端 serving 链路，而非单一 kernel；具体机制与相对基线需正文核验。
  - LLM 与生成式 AI 系统；production serving；动态工作负载；LLM

- [PAT: Accelerating LLM Decoding via Prefix-Aware Attention with Resource Efficient Multi-Tile Kernel](https://doi.org/10.1145/3779212.3790200)
  - Jinjun Yi (Tianjin University), Zhixin Zhao (Tianjin University), Yitao Hu (Tianjin University), Ke Yan (Tianjin University), Weiwei Sun (Tianjin University), Hao Wang (Stevens Institue of Technology), Laiping Zhao (Tianjin University), Yuhao Zhang (Tianjin University), Wenxin Li (Tianjin University), Keqiu Li (Tianjin University)
  - PAT 针对共享 system prompt、tool template 与 RAG prefix 的 decode 请求，把共享前缀相同的 query 打包，采用 pack-forward-merge 数据流和定制 multi-tile kernel 减少重复 KV 读取，再以多 stream forwarding、KV splitting 和 online softmax 消除不等长 KV 引起的资源气泡。
  - 核心创新是让 attention kernel 直接感知跨请求的层次化前缀共享；相比 one-query-per-CTA 或固定 tile，不只复用 KV，还随前缀和长度组织 GPU tile。
  - LLM 与生成式 AI 系统；prefix sharing；attention kernel；LLM

- [ZipServ: Fast and Memory-Efficient LLM Inference with Hardware-Aware Lossless Compression](https://doi.org/10.1145/3779212.3790250)
  - Ruibo FAN (Data Science and Analytics Thrust, HKUST(GZ)), Xiangrui YU (Data Science and Analytics Thrust, HKUST(GZ)), Xinglin Pan (Data Science and Analytics Thrust, HKUST(GZ)), Zeyu Li (Data Science and Analytics Thrust, HKUST(GZ)), Weile Luo (Data Science and Analytics Thrust, HKUST(GZ)), QIANG WANG (Harbin Institute of Technology (Shenzhen)), Wei Wang (Hong Kong University of Science and Technology), Xiaowen Chu (Data Science and Analytics Thrust, HKUST(GZ))
  - ZipServ 对 LLM 权重做 bit-exact 无损压缩，以固定长度的 TCA-TBE 编码保持 SIMT 友好，并在 ZipGEMM 中把解压与 GEMM 融合，让压缩权重从显存读取后直接在 Tensor Core 寄存器中解码计算，避免中间解压缓冲。
  - 核心创新是把无损编码格式与 GPU Tensor Core 数据通路协同设计；不同于通用熵编码只节省存储却拖慢推理，它同时削减模型占用和内存带宽。
  - LLM 与生成式 AI 系统；无损压缩；ZipGEMM；LLM

- [BlendServe: Optimizing Offline Inference with Resource-Aware Batching](https://doi.org/10.1145/3779212.3790133)
  - Yilong Zhao (University of California, Berkeley), Shuo Yang (University of California, Berkeley), Kan Zhu (University of Washington), Lianmin Zheng (UC Berkeley), Baris Kasikci (University of Washington), Yifan Qiao (UC Berkeley), Yang Zhou (UC Berkeley and UC Davis), Jiarong Xing (UC Berkeley and Rice University), Ion Stoica (UC Berkeley)
  - 官方标题可确认 BlendServe 面向离线推理，以 resource-aware batching 组织请求；尚无公开摘要可核验其 batch 构造是否基于输入/输出长度、算术强度或显存状态，也不能确认适用的模型族。
  - 标题可确认的创新边界是用资源互补性而非仅到达顺序/长度形成离线 batch；具体代价模型和收益需正文核验。
  - LLM 与生成式 AI 系统；offline inference；batching

- [BAT: Efficient Generative Recommender Serving with Bipartite Attention](https://doi.org/10.1145/3779212.3790131)
  - Jie Sun (Zhejiang University), Shaohang Wang (The University of Hong Kong), Zimo Zhang (Zhejiang University), Zhengyu Liu (Alibaba Group), Yunlong Xu (Alibaba Group), Peng Sun (Alibaba Group), Bingsheng He (National University of Singapore), Fei Wu (Zhejiang University), Zeke Wang (Zhejiang University), Bo Zhao (Aalto University)
  - 官方标题把 BAT 的对象限定为生成式推荐模型 serving，并以 bipartite attention 为核心计算结构；无公开摘要时不能确认它优化的是候选侧、用户侧还是跨请求复用。
  - 可确认的差异是针对生成式推荐的二部注意力结构做专用 serving，而不是把通用 LLM attention kernel 直接套用。
  - LLM 与生成式 AI 系统；generative recommender；bipartite attention

- [MoE-APEX: An Efficient MoE Inference System with Adaptive Precision Expert Offloading](https://doi.org/10.1145/3779212.3790187)
  - Peng Tang (Shanghai Jiaotong University), Jiacheng Liu (CUHK), Xiaofeng Hou (Shanghai Jiao Tong University), Yifei Pu (Shanghai Jiao Tong University), Jing Wang (Shanghai Jiao Tong University), Pheng-Ann Heng (CUHK), Chao Li (Shanghai Jiao Tong University), Minyi Guo (Shanghai Jiao Tong University)
  - MoE-APEX 的标题明确面向 MoE 推理，在 expert offloading 时自适应选择精度；当前证据不足以确认决策依据是专家热度、带宽、显存水位还是 token routing，因此这些细节不作推断。
  - 可确认的创新是把专家卸载与精度选择联合起来，区别于固定精度、只按热度换入换出的 expert offloading。
  - LLM 与生成式 AI 系统；MoE inference；expert offloading；adaptive precision；MoE

- [PowerMove: Optimizing Compilation for Neutral Atom Quantum Computers with Zoned Architecture](https://doi.org/10.1145/3676642.3736128)
  - Jixuan Ruan (University of California San Diego), Xiang Fang (University of California, San Diego), Hezi Zhang (University of California San Diego), Ang Li (PNNL and UW), Travis Humble (Quantum Science Center, Oak Ridge National Laboratory), Yufei Ding (UCSD)
  - PowerMove 的官方标题与主会议程把研究对象限定为量子程序编译、映射与门级优化中的“Optimizing Compilation for Neutral Atom Quantum Computers with Zoned Architecture”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Optimizing Compilation for Neutral Atom Quantum Computers with Zoned Architecture”作为独立系统问题，而不只是沿用不感知硬件约束的通用量子编译；相对基线、机制组合和收益仍需正文核验。
  - 量子、FHE 与新型计算；Quantum Computing: Compilation；量子编译；硬件感知；量子计算

- [Reconfigurable Quantum Instruction Set Computers for High Performance Attainable on Hardware](https://doi.org/10.1145/3779212.3790208)
  - Zhaohui Yang (The Hong Kong University of Science and Technology), Dawei Ding (Tsinghua University), Qi Ye (Tsinghua University), Cupjin Huang (Alibaba Group USA), Jianxin Chen (Tsinghua University), Yuan Xie (The Hong Kong University of Science and Technology)
  - ReQISC 面向存在不同耦合 Hamiltonian 的量子硬件，用统一微体系结构直接执行任意双量子比特 SU(4) 操作（模去单比特旋转）；编译器依次做程序感知高层优化、与程序无关的电路优化和 SU(4)-aware routing，并把指令落到可校准脉冲，平均把脉冲时长降至 CNOT/CZ 基线的约 1/4.97。
  - 核心创新是把连续、表达力更强的 SU(4) 指令集同时落实到微体系结构、路由编译和脉冲校准，而不是先把程序离散分解成固定 CNOT/CZ 再映射。
  - 量子、FHE 与新型计算；ReQISC；quantum ISA；SU(4)；compiler-hardware co-design；量子计算

- [QTurbo: A Robust and Efficient Compiler for Analog Quantum Simulation](https://doi.org/10.1145/3760250.3762227)
  - Junyu Zhou (University of Pennsylvania), Yuhao Liu (University of Pennsylvania), Shize Che (University of Pennsylvania), Anupam Mitra (Lawrence Berkeley National Laboratory), Efekan Kökcü (Lawrence Berkeley National Laboratory), Ermal Rrapaj (Lawrence Berkeley National Laboratory), Costin Iancu (Lawrence Berkeley National Laboratory), Gushu Li (University of Pennsylvania)
  - QTurbo 的官方标题与主会议程把研究对象限定为量子程序编译、映射与门级优化中的“A Robust and Efficient Compiler for Analog Quantum Simulation”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“A Robust and Efficient Compiler for Analog Quantum Simulation”作为独立系统问题，而不只是沿用不感知硬件约束的通用量子编译；相对基线、机制组合和收益仍需正文核验。
  - 量子、FHE 与新型计算；Quantum Computing: Compilation；量子编译；硬件感知；量子计算；compiler

- [Reducing T Gates with Unitary Synthesis](https://doi.org/10.1145/3779212.3790210)
  - Tianyi Hao (University of Wisconsin-Madison), Amanda Xu (University of Wisconsin-Madison), Swamit Tannu (University of Wisconsin-Madison)
  - trasyn 面向容错量子编译中的任意单量子比特 U3 门，直接用 tensor-network search 合成 Clifford+T 电路，避免先拆成多个 Rz 再分别近似；实验相对 Gridsynth 最多减少 3.5 倍 T 门、7 倍 Clifford 门并把电路不保真度降低 4 倍。
  - 核心创新是把完整 U3 作为一次容错 unitary synthesis 的搜索对象，利用门之间可共享的结构联合压缩，而非接受逐个 Rz 分解带来的重复 T 门和近似误差。
  - 量子、FHE 与新型计算；trasyn；fault-tolerant quantum；T-count；unitary synthesis

- [Borrowing Dirty Qubits in Quantum Programs](https://doi.org/10.1145/3779212.3790134)
  - Bonan Su (Department of Computer Science and Technology, Tsinghua University), Li Zhou (Institute of Software, Chinese Academy of Sciences), Yuan Feng (Tsinghua University), Mingsheng Ying (University of Technology, Sydney)
  - Borrowing Dirty Qubits in Quantum 的官方标题与主会议程把研究对象限定为量子程序编译、映射与门级优化中的“Borrowing Dirty Qubits in Quantum Programs”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Borrowing Dirty Qubits in Quantum Programs”作为独立系统问题，而不只是沿用不感知硬件约束的通用量子编译；相对基线、机制组合和收益仍需正文核验。
  - 量子、FHE 与新型计算；Quantum Computing: Compilation；量子编译；硬件感知；量子计算

- [HybridTier: An Adaptive and Lightweight CXL-Memory Tiering System](https://doi.org/10.1145/3676642.3736119)
  - Kevin Song (University of Toronto), Jiacheng Yang (University of Toronto), Zixuan Wang (University of California San Diego), Jishen Zhao (UCSD), Sihang Liu (Waterloo), Gennady Pekhimenko (Univ. of Toronto / CentML)
  - HybridTier 的官方标题与主会议程把研究对象限定为CXL 内存分层、共享语义、桥接与安全分配中的“An Adaptive and Lightweight CXL-Memory Tiering System”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“An Adaptive and Lightweight CXL-Memory Tiering System”作为独立系统问题，而不只是沿用把 CXL 仅视为慢速 NUMA 内存的管理方式；相对基线、机制组合和收益仍需正文核验。
  - 内存、存储与解耦资源；CXL & Memory Fabric；CXL；内存解耦

- [vCXLGen: Automated Synthesis and Verification of CXL Bridges for Heterogeneous Architectures](https://doi.org/10.1145/3779212.3790245)
  - Anatole Lefort (Technical University of Munich), Julian Pritzi (Technical University of Munich), Nicolò Carpentieri (Technical University of Munich), David Schall (Technical University of Munich), Simon Dittrich (Technical University of Munich), Soham Chakraborty (TU Delft), Nicolai Oswald (NVIDIA), Pramod Bhatotia (Technical University of Munich)
  - vCXLGen 的官方标题与主会议程把研究对象限定为CXL 内存分层、共享语义、桥接与安全分配中的“Automated Synthesis and Verification of CXL Bridges for Heterogeneous Architectures”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Automated Synthesis and Verification of CXL Bridges for Heterogeneous Architectures”作为独立系统问题，而不只是沿用把 CXL 仅视为慢速 NUMA 内存的管理方式；相对基线、机制组合和收益仍需正文核验。
  - 内存、存储与解耦资源；CXL & Memory Fabric；CXL；内存解耦

- [CXLMC: Model Checking CXL Shared Memory Programs](https://doi.org/10.1145/3779212.3790150)
  - Simon Guo (University of California, Irvine), Conan Truong (University of California, Irvine), Brian Demsky (University of California, Irvine)
  - CXLMC 的官方标题与主会议程把研究对象限定为CXL 内存分层、共享语义、桥接与安全分配中的“Model Checking CXL Shared Memory Programs”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Model Checking CXL Shared Memory Programs”作为独立系统问题，而不只是沿用把 CXL 仅视为慢速 NUMA 内存的管理方式；相对基线、机制组合和收益仍需正文核验。
  - 内存、存储与解耦资源；CXL & Memory Fabric；CXL；内存解耦

- [A Programming Model for Disaggregated Memory over CXL](https://doi.org/10.1145/3779212.3790121)
  - Gal Assa (Technion), Moritz Lumme (ETH Zürich), Lucas Bürgi (ETH Zürich), Michal Friedman (ETH Zürich), Ori Lahav (Tel Aviv University)
  - CXL0 为跨主机共享 CXL 内存上的并发程序建立高层访问抽象和形式化 operational semantics，显式描述本地/远端访问及部分节点崩溃；其变换可把任意 linearizable 并发算法提升为在分布式 partial-crash 模型下保持持久性的实现。
  - 核心创新是首次把 CXL disaggregated memory 的共享内存行为、持久性和故障语义统一为可推理的编程模型，而不是只提供容量分层 API 或针对单个数据结构手写恢复协议。
  - 内存、存储与解耦资源；CXL0；programming model；linearizability；partial crash；CXL

- [Cxlalloc: Safe and Efficient Memory Allocation for a CXL Pod](https://doi.org/10.1145/3779212.3790149)
  - Newton Ni (UT Austin), Yan Sun (UIUC), Zhiting Zhu (UT Austin/NVIDIA), Emmett Witchel (UT Austin)
  - Cxlalloc 的官方标题与主会议程把研究对象限定为CXL 内存分层、共享语义、桥接与安全分配中的“Safe and Efficient Memory Allocation for a CXL Pod”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Safe and Efficient Memory Allocation for a CXL Pod”作为独立系统问题，而不只是沿用把 CXL 仅视为慢速 NUMA 内存的管理方式；相对基线、机制组合和收益仍需正文核验。
  - 内存、存储与解耦资源；CXL & Memory Fabric；CXL；内存解耦

- [SNIP: An Adaptive Mixed Precision Framework for Subbyte Large Language Model Training](https://doi.org/10.1145/3779212.3790223)
  - Yunjie Pan (University of Michigan), Jiecao Yu (Meta Platforms, Inc.), Yongyi Yang (University of Michigan, Ann Arbor), Hanmei Yang (University of Massachusetts Amherst), Zhaoxia (Summer) Deng (Meta), Scott Mahlke (University of Michigan)
  - SNIP 面向 1B 至 70B 级 LLM 预训练，周期性采集 activation、gradient 和 optimizer state，分别估计前向 loss divergence 与反向 weight divergence，再用 ILP 在效率约束下逐层选择 sub-byte 精度，而非全模型统一量化。
  - 核心创新是把训练阶段的质量损失显式分解为前向和反向两类可测指标，并据此在线重求 layer-wise precision；相比固定或启发式 mixed precision 更能跨模型和训练阶段迁移。
  - LLM 与生成式 AI 系统；sub-byte training；ILP；mixed precision

- [Fine-grained and Non-intrusive LLM Training Monitoring via Microsecond-level Traffic Measurement](https://doi.org/10.1145/3779212.3790163)
  - Yibo Xiao (Nanjing University), Hao Zheng (Nanjing University, China.), Haifeng Sun (National University of Singapore), Qingkai Meng (Nanjing University), Jiong Duan (Nanjing University), Xiaohe Hu (Infrawaves), Rong Gu (Nanjing University), Guihai Chen (Nanjing University), Chen Tian (Nanjing University)
  - 官方标题可确认该工作以微秒级网络流量测量为观测面，对 LLM 训练做细粒度且非侵入式监控；尚不能确认它从流量中重建的是迭代阶段、collective、straggler 还是故障。
  - 可确认的差异是绕开训练框架插桩，从网络侧高时间分辨率信号恢复训练状态；映射模型和准确率需正文核验。
  - LLM 与生成式 AI 系统；training observability；traffic measurement；LLM

- [SuperOffload: Unleashing the Power of Large-Scale LLM Training on Superchips](https://doi.org/10.1145/3760250.3762217)
  - Xinyu Lian (University of Illinois Urbana Champaign), Masahiro Tanaka (Microsoft), Olatunji Ruwase (Snowflake), Minjia Zhang (University of Illinois Urbana Champaign)
  - SuperOffload 面向 NVIDIA GH200 这类 CPU-GPU 同封装 Superchip，在 Hopper、Grace 与 NVLink-C2C 之间联合执行 adaptive weight offload、bucket repartition、casting、speculative execution 和 CPU Adam，使单机可训练更大模型并扩展到 ZeRO/Ulysses。
  - 核心创新是重写传统 PCIe 松耦合 offload 的假设，把一致内存和高带宽 C2C 当作一等资源联合调度，而非仅把 CPU 当容量后端。
  - LLM 与生成式 AI 系统；GH200；training offload；NVLink-C2C；LLM

- [DIP: Efficient Large Multimodal Model Training with Dynamic Interleaved Pipeline](https://doi.org/10.1145/3779212.3790154)
  - Zhenliang Xue (Shanghai Jiao Tong University), Hanpeng Hu (StepFun), Xing Chen (StepFun), Yimin Jiang (StepFun), Yixin Song (Shanghai Jiao Tong University, Zenergize AI), Zeyu Mi (Shanghai Jiao Tong University, Zenergize AI), Yibo Zhu (StepFun), Daxin Jiang (StepFun), Yubin Xia (Shanghai Jiao Tong University), Haibo Chen (Shanghai JiaoTong University)
  - DIP 面向每批模态组合和 token/patch 数动态变化的 LMM 训练，把不同模态计算拆成专用 pipeline segment，再按当前 batch 切成模态级 sub-microbatch；CPU 在后台异步生成本批调度，以同时缓解异构模型结构造成的 stage imbalance 与数据动态性。
  - 核心创新是 pipeline 划分和 microbatch 形成都感知模态并随输入变化，而非为平均 workload 离线生成一个静态 schedule。
  - LLM 与生成式 AI 系统；multimodal training；dynamic pipeline

- [Dynamic Sparsity in Large-Scale Video DiT Training](https://doi.org/10.1145/3760250.3762216)
  - Xin Tan (The Chinese University of Hong Kong), Yuetao Chen (The Chinese University of Hong Kong), Yimin Jiang (Unaffiliated), Xing Chen (StepFun), Kun Yan (StepFun), Nan Duan (StepFun), Yibo Zhu (StepFun), Daxin Jiang (StepFun), Hong Xu (The Chinese University of Hong Kong)
  - Dynamic Sparsity in Large-Scale Video 的官方标题与主会议程把研究对象限定为大模型与多模态模型的训练精度、流水线和监控中的“Dynamic Sparsity in Large-Scale Video DiT Training”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Dynamic Sparsity in Large-Scale Video DiT Training”作为独立系统问题，而不只是沿用固定精度、静态流水线或侵入式训练监控；相对基线、机制组合和收益仍需正文核验。
  - LLM 与生成式 AI 系统；LLM Training Systems；LLM training；训练系统

- [DFVG: A Heterogeneous Architecture for Speculative Decoding with Draft-on-FPGA and Verify-on-GPU](https://doi.org/10.1145/3779212.3790153)
  - Shaoqiang Lu (Shanghai Jiao Tong University, Shanghai, China and Eastern Institute of Technology, Ningbo, China), Yangbo Wei (Shanghai Jiao Tong University, Shanghai, China and Eastern Institute of Technology, Ningbo, China), Junhong Qian (Southest University, Nanjin, China), Dongge Qin (Southest University, Nanjin, China), Shiji Gao (Southest University, Nanjin, China), Yizhi Ding (Southest University, Nanjin, China), Qifan Wang (Shanghai Jiao Tong University, Shanghai, China and Eastern Institute of Technology, Ningbo, China), Chen Wu (Ningbo Institute of Digital Twin，Eastern Institute of Technology , Ningbo, China), Xiao Shi (Southest University, Nanjin, China), Lei He (Eastern Institute of Technology, Ningbo, China)
  - DFVG 的官方标题与主会议程把研究对象限定为推测解码、异构草稿验证与长上下文推理中的“A Heterogeneous Architecture for Speculative Decoding with Draft-on-FPGA and Verify-on-GPU”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“A Heterogeneous Architecture for Speculative Decoding with Draft-on-FPGA and Verify-on-GPU”作为独立系统问题，而不只是沿用草稿与验证紧耦合或固定推测策略；相对基线、机制组合和收益仍需正文核验。
  - LLM 与生成式 AI 系统；Speculative Decoding；推测解码；异构推理；GPU

- [SwiftSpec: Disaggregated Speculative Decoding and Fused Kernels for Low-Latency LLM Inference](https://doi.org/10.1145/3779212.3790246)
  - Ziyi Zhang (ByteDance Seed & University of Chicago), Ziheng Jiang (ByteDance Seed), Chengquan Jiang (ByteDance Seed), Menghan Yu (ByteDance Seed), Size Zheng (ByteDance Seed), Haibin Lin (ByteDance Seed), Xin Liu (ByteDance Seed), Henry Hoffmann (University of Chicago)
  - SwiftSpec 的官方标题与主会议程把研究对象限定为推测解码、异构草稿验证与长上下文推理中的“Disaggregated Speculative Decoding and Fused Kernels for Low-Latency LLM Inference”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Disaggregated Speculative Decoding and Fused Kernels for Low-Latency LLM Inference”作为独立系统问题，而不只是沿用草稿与验证紧耦合或固定推测策略；相对基线、机制组合和收益仍需正文核验。
  - LLM 与生成式 AI 系统；Speculative Decoding；推测解码；异构推理；LLM

- [SpeContext: Enabling Efficient Long-context Reasoning with Speculative Context Sparsity in LLMs](https://doi.org/10.1145/3779212.3790224)
  - Jiaming Xu (Shanghai Jiao Tong University; SII;), Jiayi Pan (Shanghai Jiao Tong University; Infinigence-AI;), Hanzhen Wang (Shanghai Jiao Tong University), Yongkang Zhou (Shanghai Jiao Tong University; SII;), Jiancai Ye (Shanghai Jiao Tong University), Yu Wang (Tsinghua University), Guohao Dai (Shanghai Jiao Tong University; Infinigence-AI; SII;)
  - SpeContext 用蒸馏小模型的 attention 信息构造轻量 retrieval head，预测长上下文中需访问的 KV token；运行时异步预取这些 KV，并依据内存模型弹性装载，使检索、传输和 LLM 计算重叠，覆盖云与边缘资源受限环境。
  - 核心创新是把 context sparsity 检索目标视为对原 LLM 注意力焦点的蒸馏，再与异步 KV 数据流和自适应显存管理联合设计。
  - LLM 与生成式 AI 系统；long-context reasoning；KV retrieval；algorithm-system co-design；LLM

- [SpecProto: A Parallelizing Compiler for Speculative Decoding of Large Protocol Buffers Data](https://doi.org/10.1145/3779212.3790225)
  - Zhijie Wang (University of California, Riverside), Chales Hong (University of California, Riverside), Dhruv Parmar (University of California, Riverside), Shengbo Ma (University of California, Riverside), Zhijia Zhao (University of California, Riverside), Qidong Zhao (Google), Xu Liu (Google)
  - SpecProto 的官方标题与主会议程把研究对象限定为推测解码、异构草稿验证与长上下文推理中的“A Parallelizing Compiler for Speculative Decoding of Large Protocol Buffers Data”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“A Parallelizing Compiler for Speculative Decoding of Large Protocol Buffers Data”作为独立系统问题，而不只是沿用草稿与验证紧耦合或固定推测策略；相对基线、机制组合和收益仍需正文核验。
  - LLM 与生成式 AI 系统；Speculative Decoding；推测解码；异构推理；compiler

- [EARTH: An Efficient MoE Accelerator with Entropy-Aware Speculative Prefetch and Result Reuse](https://doi.org/10.1145/3779212.3790155)
  - Fangxin Liu (Shanghai Jiao Tong University), Ning Yang (Shanghai Jiao Tong University), Jingkui Yang (National University of Defense Technology), Zongwu Wang (Shanghai Jiao Tong University), Chenyang Guan (Shanghai Jiao Tong University), Yu Feng (Shanghai Jiao Tong University), Li Jiang (Shanghai Jiaotong University), Haibing Guan (Shanghai Jiao Tong University)
  - EARTH 的官方标题与主会议程把研究对象限定为推测解码、异构草稿验证与长上下文推理中的“An Efficient MoE Accelerator with Entropy-Aware Speculative Prefetch and Result Reuse”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“An Efficient MoE Accelerator with Entropy-Aware Speculative Prefetch and Result Reuse”作为独立系统问题，而不只是沿用草稿与验证紧耦合或固定推测策略；相对基线、机制组合和收益仍需正文核验。
  - LLM 与生成式 AI 系统；Speculative Decoding；推测解码；异构推理；MoE

- [gShare: Efficient GPU Sharing with Aggressive Scheduling in Multi-tenant FaaS platform](https://doi.org/10.1145/3779212.3790168)
  - Yanan Yang (China Telecom Cloud Computing Research Institute), Zhengxiong Jiang (China Telecom Cloud Technology Co. Ltd.), Meiqi Zhu (China Telecom Cloud Technology Co. Ltd.), Hongqiang Xu (China Telecom Cloud Technology Co. Ltd.), Yujun Wang (China Telecom Cloud Technology Co. Ltd.), Liang Li (China Telecom Cloud Computing Research Institute), Jiansong zhang (China Telecom Cloud Computing Research Institute), Jie Wu (China Telecom Cloud Computing Research Institute)
  - gShare 的官方标题与主会议程把研究对象限定为多租户 GPU 调度、GPU I/O 与集体通信中的“Efficient GPU Sharing with Aggressive Scheduling in Multi-tenant FaaS platform”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Efficient GPU Sharing with Aggressive Scheduling in Multi-tenant FaaS platform”作为独立系统问题，而不只是沿用粗粒度 GPU 独占和通用通信库；相对基线、机制组合和收益仍需正文核验。
  - ML 系统、GPU 与加速器；GPU Systems & Scheduling；GPU runtime；集群调度；GPU

- [GFS: A Preemption-aware Scheduling Framework for GPU Clusters with Predictive Spot Instance Management](https://doi.org/10.1145/3760250.3762231)
  - Jiaang Duan (Shanghai Jiao Tong University), Shenglin Xu (Shanghai Jiao Tong University), Shiyou Qian (Shanghai Jiao Tong University), Dingyu Yang (Zhejiang University), Kangjin Wang (Alibaba Group), Chenzhi Liao (Alibaba Group), Yinghao Yu (Alibaba Group), Qin Hua (Shanghai Jiao Tong Univeristy), Hanwen Hu (Shanghai Jiao Tong University), Qi Wang (Alibaba Group), Wenchao Wu (Alibaba Group), Dongqing Bao (Alibaba Group), Tianyu Lu (Alibaba Group), Jian Cao (Shanghai Jiao Tong University), Guangtao Xue (Shanghai Jiao Tong University), Guodong Yang (Alibaba Group), Liping Zhang (Alibaba Group), Gang Chen (Zhejiang University)
  - GFS 面向万卡生产集群中的高优先级任务与低优先级 spot 任务，用轻量预测器预估各租户 GPU 需求，动态调整带保证时长的 spot quota，并在高优先级任务到来时选择尽量少伤害低优先级作业的抢占。
  - 核心创新是把需求预测、可承诺 spot 时长和 preemption-aware 排队联合起来；不同于被动驱逐，调度器在需求到来前预留可回收容量。
  - ML 系统、GPU 与加速器；GPU cluster；spot instance；predictive scheduling；GPU

- [Asynchrony and GPUs: Bridging this Dichotomy for I/O with AGIO](https://doi.org/10.1145/3779212.3790130)
  - Jihoon Han (Pennsylvania State University), Anand Sivasubramaniam (Pennsylvania State University), Chia-Hao Chang (Nvidia), Vikram Sharma Mailthody (Nvidia Research), Zaid Qureshi (Nvidia Research), Wen-mei W. Hwu (Nvidia Research)
  - Asynchrony and GPUs 的官方标题与主会议程把研究对象限定为多租户 GPU 调度、GPU I/O 与集体通信中的“Bridging this Dichotomy for I/O with AGIO”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Bridging this Dichotomy for I/O with AGIO”作为独立系统问题，而不只是沿用粗粒度 GPU 独占和通用通信库；相对基线、机制组合和收益仍需正文核验。
  - ML 系统、GPU 与加速器；GPU Systems & Scheduling；GPU runtime；集群调度；GPU

- [MSCCL++: Rethinking GPU Communication Abstractions for AI Inference](https://doi.org/10.1145/3779212.3790188)
  - Changho Hwang (Microsoft Research), Peng Cheng (Microsoft Research), Roshan Dathathri (Microsoft Research), Abhinav Jangda (Microsoft Research), Saeed Maleki (Microsoft Research), Madan Musuvathi (Microsoft Research), Olli Saarikivi (Microsoft Research), Aashaka Shah (Microsoft Research), Ziyue Yang (Microsoft Research), Binyang Li (Microsoft Azure), Caio Rocha (Microsoft Azure), Qinghua Zhou (Microsoft Azure), Mahdieh Ghazimirsaeed (Microsoft Azure), Sreevatsa Anantharamu (Microsoft Azure), Jithin Jose (Microsoft Azure)
  - MSCCL++ 为异构 GPU/互连提供低层硬件原语、面向 workload 的通信 DSL 和兼容标准 collective API 的算法库，使服务可写自定义通信 kernel 又不自行处理同步与一致性；已用于 Azure AI 服务和 AMD RCCL。
  - 核心创新是在通用 collective 与手写专用栈之间增加性能不丢失的两层抽象，让新硬件特性和 inference-specific 通信算法能快速组合。
  - ML 系统、GPU 与加速器；GPU communication；DSL；collective；GPU

- [Insum: Sparse GPU Kernels Simplified and Optimized with Indirect Einsums](https://doi.org/10.1145/3779212.3790176)
  - Jaeyeon Won (MIT), Willow Ahrens (Georgia Tech), Joel Emer (MIT/NVIDIA), Saman Amarasinghe (MIT)
  - Insum 从格式无关的 sparse einsum 出发，将稀疏数据和元数据映射为带 indirect indexing 的 dense tensor operation，再扩展 PyTorch compiler 生成 Tensor Core kernel，并配套 GroupCOO/BlockGroupCOO 定长格式。
  - 核心创新是以 indirect einsum 统一表达稀疏格式与稠密计算区，避免现有稀疏编译器在 GPU 和 sparse-dense 混合区域同时失效。
  - ML 系统、GPU 与加速器；sparse compiler；indirect einsum；Tensor Core；GPU

- [RowArmor: Efficient and Comprehensive Protection Against DRAM Disturbance Errors](https://doi.org/10.1145/3779212.3790213)
  - Minbok Wi (Seoul National University), Yoonyul Yoo (Samsung Electronics), Yoojin Kim (Sungkyunkwan University), Jaeho Shin (Sungkyunkwan University), Jumin Kim (Seoul National University), Yesin Ryu (Sungkyunkwan University, Samsung Electronics), Saeid Gorgin (Sungkyunkwan University), Jung Ho Ahn (Seoul National University), Jungrae Kim (Sungkyunkwan University)
  - RowArmor 的官方标题与主会议程把研究对象限定为DRAM/NAND 扰动、可信存储与硬件事件量化中的“Efficient and Comprehensive Protection Against DRAM Disturbance Errors”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Efficient and Comprehensive Protection Against DRAM Disturbance Errors”作为独立系统问题，而不只是沿用固定阈值或仅设备侧的可靠性保护；相对基线、机制组合和收益仍需正文核验。
  - 安全、可靠性、验证与测试；DRAM Reliability & Security；存储可靠性；硬件安全

- [APT: Securing Against DRAM Read Disturbance via Adaptive Probabilistic In-DRAM Trackers](https://doi.org/10.1145/3779212.3790126)
  - Runjin Wu (School of Computer Science & Technology, Huazhong University of Science and Technology, Wuhan, China), Meng Zhang (School of Computer Science & Technology, Huazhong University of Science and Technology, Wuhan, China), You Zhou (School of Computer Science & Technology, Huazhong University of Science and Technology, Wuhan, China), Changsheng Xie (Wuhan National Laboratory for Optoelectronics, Huazhong University of Science and Technology, Wuhan, China), Fei Wu (Wuhan National Laboratory for Optoelectronics, Huazhong University of Science and Technology, Wuhan, China)
  - APT 的官方标题与主会议程把研究对象限定为DRAM/NAND 扰动、可信存储与硬件事件量化中的“Securing Against DRAM Read Disturbance via Adaptive Probabilistic In-DRAM Trackers”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Securing Against DRAM Read Disturbance via Adaptive Probabilistic In-DRAM Trackers”作为独立系统问题，而不只是沿用固定阈值或仅设备侧的可靠性保护；相对基线、机制组合和收益仍需正文核验。
  - 安全、可靠性、验证与测试；DRAM Reliability & Security；存储可靠性；硬件安全

- [STRAW: Stress-Aware WL-Based Read Disturbance Management for High-Density NAND Flash Memory](https://doi.org/10.1145/3779212.3790228)
  - Myoungjun Chun (Soongsil University), Jaeyong Lee (Seoul National University), Inhyuk Choi (Seoul National University), Jisung Park (POSTECH (Pohang University of Science and Technology)), Myungsuk Kim (Kyungpook National University), Jihong Kim (Seoul National University)
  - STRAW 的官方标题与主会议程把研究对象限定为DRAM/NAND 扰动、可信存储与硬件事件量化中的“Stress-Aware WL-Based Read Disturbance Management for High-Density NAND Flash Memory”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Stress-Aware WL-Based Read Disturbance Management for High-Density NAND Flash Memory”作为独立系统问题，而不只是沿用固定阈值或仅设备侧的可靠性保护；相对基线、机制组合和收益仍需正文核验。
  - 安全、可靠性、验证与测试；DRAM Reliability & Security；存储可靠性；硬件安全

- [Trust-V: Toward Secure and Reliable Storage for Trusted Execution Environments](https://doi.org/10.1145/3779212.3790242)
  - SeungKyun Han (Chungnam National University), Jiyeon Yang (Chungnam National University), Jinsoo Jang (Chungnam National University)
  - Trust-V 的官方标题与主会议程把研究对象限定为DRAM/NAND 扰动、可信存储与硬件事件量化中的“Toward Secure and Reliable Storage for Trusted Execution Environments”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Toward Secure and Reliable Storage for Trusted Execution Environments”作为独立系统问题，而不只是沿用固定阈值或仅设备侧的可靠性保护；相对基线、机制组合和收益仍需正文核验。
  - 安全、可靠性、验证与测试；DRAM Reliability & Security；存储可靠性；硬件安全；storage

- [Optimizer-Friendly Instrumentation for Event Quantification with PRUE Algorithm](https://doi.org/10.1145/3779212.3790196)
  - Hao Ling (The Hong Kong University of Science and Technology), Yiyuan Guo (The Hong Kong University of Science and Technology), Charles Zhang (The Hong Kong University of Science and Technology)
  - Optimizer-Friendly Instrumentation for Event Quantification 的官方标题与主会议程把研究对象限定为DRAM/NAND 扰动、可信存储与硬件事件量化中的“Optimizer-Friendly Instrumentation for Event Quantification with PRUE Algorithm”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Optimizer-Friendly Instrumentation for Event Quantification with PRUE Algorithm”作为独立系统问题，而不只是沿用固定阈值或仅设备侧的可靠性保护；相对基线、机制组合和收益仍需正文核验。
  - 安全、可靠性、验证与测试；DRAM Reliability & Security；存储可靠性；硬件安全

- [I/O Analysis is All You Need: An I/O Analysis for Long-Sequence Attention](https://doi.org/10.1145/3779212.3790174)
  - Xiaoyang Lu (Illinois Institute of Technology), Boyu Long (Institute of Computing Technology, Chinese Academy of Sciences, University of Chinese Academy of Sciences), Xiaoming Chen (Institute of Computing Technology, Chinese Academy of Sciences), Yinhe Han (Institute of Computing Technology, Chinese Academy of Sciences), Xian-He Sun (Illinois Institute of Technology)
  - I/O Analysis is All You Need 的官方标题与主会议程把研究对象限定为长序列 attention、KV cache 与 PIM/解耦推理中的“An I/O Analysis for Long-Sequence Attention”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“An I/O Analysis for Long-Sequence Attention”作为独立系统问题，而不只是沿用完整 KV 搬运和通用张量并行；相对基线、机制组合和收益仍需正文核验。
  - LLM 与生成式 AI 系统；LLM Attention & KV Cache；KV cache；长上下文；PIM

- [REPA: Reconfigurable PIM for the Joint Acceleration of KV Cache Offloading and Processing](https://doi.org/10.1145/3779212.3790212)
  - Yang Hong (Shanghai Jiao Tong University), Junlong Yang (Shanghai Jiao Tong University), Bo Peng (Shanghai Jiao Tong University), Jianguo Yao (Shanghai Jiao Tong University)
  - REPA 的官方标题与主会议程把研究对象限定为长序列 attention、KV cache 与 PIM/解耦推理中的“Reconfigurable PIM for the Joint Acceleration of KV Cache Offloading and Processing”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Reconfigurable PIM for the Joint Acceleration of KV Cache Offloading and Processing”作为独立系统问题，而不只是沿用完整 KV 搬运和通用张量并行；相对基线、机制组合和收益仍需正文核验。
  - LLM 与生成式 AI 系统；LLM Attention & KV Cache；KV cache；长上下文；PIM；cache

- [STARC: Selective Token Access with Remapping and Clustering for Efficient LLM Decoding on PIM Systems](https://doi.org/10.1145/3779212.3790226)
  - Zehao Fan (Rensselaer Polytechnic Institute), Yunzhen Liu (University of Massachusetts, Amherst), Garrett Gagnon (Rensselaer Polytechnic Institute), Zhenyu Liu (Rensselaer Polytechnic Institute), Yayue Hou (Rensselaer Polytechnic Institute), Hadjer Benmeziane (IBM Research – Ruschlikon, Switzerland), Kaoutar El Maghraoui (IBM T. J. Watson Research Center), Liu Liu (Rensselaer Polytechnic Institute)
  - STARC 的官方标题与主会议程把研究对象限定为长序列 attention、KV cache 与 PIM/解耦推理中的“Selective Token Access with Remapping and Clustering for Efficient LLM Decoding on PIM Systems”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Selective Token Access with Remapping and Clustering for Efficient LLM Decoding on PIM Systems”作为独立系统问题，而不只是沿用完整 KV 搬运和通用张量并行；相对基线、机制组合和收益仍需正文核验。
  - LLM 与生成式 AI 系统；LLM Attention & KV Cache；KV cache；长上下文；PIM；LLM

- [Mugi: Value Level Parallelism For Efficient LLMs](https://doi.org/10.1145/3779212.3790189)
  - Daniel Price (University of Central Florida), Prabhu Vellaisamy (Carnegie Mellon University), John Paul Shen (Carnegie Mellon University), Di Wu (University of Central Florida)
  - Mugi 将 value-level parallelism 从低精度 GEMM 扩展到 softmax 等非线性、weight-only/KV-cache quantization 和 GQA 下的小 batch 非对称 GEMM，并设计专用架构按数值重要性分配近似精度，覆盖完整 LLM 执行。
  - 核心创新是把并行和精度资源按数值而非张量维度组织，使同一架构同时处理线性与非线性算子，而非只加速一种量化 GEMM。
  - LLM 与生成式 AI 系统；value-level parallelism；LLM accelerator；LLM

- [TPLA: Tensor Parallel Latent Attention for Efficient Disaggregated Prefill & Decode Inference](https://doi.org/10.1145/3779212.3790237)
  - Xiaojuan Tang (Peking University), Fanxu Meng (Peking University), Pingzhi Tang (Peking University), Yuxuan Wang (Peking University), Di Yin (Tencent YouTu Lab), Xing Sun (Tencent YouTu Lab), Muhan Zhang (Peking University)
  - TPLA 的官方标题与主会议程把研究对象限定为长序列 attention、KV cache 与 PIM/解耦推理中的“Tensor Parallel Latent Attention for Efficient Disaggregated Prefill & Decode Inference”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Tensor Parallel Latent Attention for Efficient Disaggregated Prefill & Decode Inference”作为独立系统问题，而不只是沿用完整 KV 搬运和通用张量并行；相对基线、机制组合和收益仍需正文核验。
  - LLM 与生成式 AI 系统；LLM Attention & KV Cache；KV cache；长上下文；PIM

- [LAER-MoE: Load-Adaptive Expert Re-layout for Efficient Mixture-of-Experts Training](https://doi.org/10.1145/3779212.3790180)
  - Xinyi Liu (Peking University), Yujie Wang (Peking University), Fangcheng Fu (Shanghai Jiao Tong University), Xuefeng Xiao (Bytedance Seed), Huixia Li (Bytedance Seed), Jiashi Li (Bytedance Seed), Bin Cui (Peking University)
  - LAER-MoE 在训练时将每个 expert 参数全分片到多设备，按本轮 token routing 恢复部分 expert，并由 planner 联合决定 expert re-layout 与 token 路由；通信操作被细粒度排程，以避免动态热点专家拖慢整轮。
  - 核心创新是让 expert placement 在训练中可重排，而非把完整 expert 永久绑定设备；FSEP 将参数分片能力直接转化为负载均衡自由度。
  - LLM 与生成式 AI 系统；MoE training；expert re-layout；FSEP；MoE

- [oFFN: Outlier and Neuron-aware Structured FFN for Fast yet Accurate LLM Inference](https://doi.org/10.1145/3779212.3790194)
  - Geunsoo Song (Sogang University), Hoeseok Yang (Santa Clara University), Youngmin Yi (Sogang University)
  - oFFN 的官方标题与主会议程把研究对象限定为MoE 训练/推理、扩散模型服务和推理时扩展中的“Outlier and Neuron-aware Structured FFN for Fast yet Accurate LLM Inference”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Outlier and Neuron-aware Structured FFN for Fast yet Accurate LLM Inference”作为独立系统问题，而不只是沿用静态专家布局或单模型服务；相对基线、机制组合和收益仍需正文核验。
  - LLM 与生成式 AI 系统；Mixture-of-Experts & Efficient Inference；MoE；生成式推理；LLM

- [MoDM: Efficient Serving for Image Generation via Mixture-of-Diffusion Models](https://doi.org/10.1145/3760250.3762220)
  - Yuchen Xia (University of Michigan), Divyam Sharma (University of Michigan), Yichao Yuan (University of Michigan), Souvik Kundu (Intel Labs), Nishil Talati (University of Michigan)
  - MoDM 面向文本到图像请求，用最终图像而非某个模型内部 feature 作为跨模型族 cache；命中请求可交给小模型并借缓存保持质量，未命中用大模型，global monitor 随请求率分配 GPU 以满足质量和延迟 SLO。
  - 核心创新是以模型无关的 final-image cache 联合路由大小 diffusion model，把质量-延迟选择和集群资源分配合并为 serving 决策。
  - LLM 与生成式 AI 系统；diffusion serving；image cache；quality-aware routing

- [Taming the Long-Tail: Efficient Reasoning RL Training with Adaptive Drafter](https://doi.org/10.1145/3779212.3790231)
  - Qinghao Hu (MIT), Shang Yang (MIT), Junxian Guo (MIT), Xiaozhe Yao (ETH Zurich), Yujun Lin (NVIDIA), Yuxian Gu (NVIDIA), Han Cai (NVIDIA), Chuang Gan (MIT-IBM Watson AI Lab, UMass Amherst), Ana Klimovic (ETH Zurich), Song Han (MIT)
  - TLT 针对 reasoning RL rollout 中少数超长响应形成的尾部拖延，在空闲 GPU 上持续训练轻量 drafter，并由 rollout engine 为每个 batch 选择推测解码策略、复用预捕获 CUDA Graph，从而在目标模型持续变化时仍加速生成。
  - 核心创新是把 draft model 更新成本塞入长尾造成的空闲资源，并使 speculative decoding 随 RL workload 与模型版本自适应；这是训练系统优化，不等同于 Agent。
  - LLM 与生成式 AI 系统；reasoning RL；adaptive drafter；传统 RL 非 Agent

- [FastTTS: Accelerating Test-Time Scaling for Edge LLM Reasoning](https://doi.org/10.1145/3779212.3790161)
  - Hao (Mark) Chen (Imperial College London), Zhiwen Mo (Imperial College London), Guanxi Lu (Imperial College London), Shuang Liang (Imperial College London), Lingxiao Ma (Microsoft Research), Wayne Luk (Imperial College London), Hongxiang Fan (Imperial College London)
  - FastTTS 面向单张消费级 GPU 上的边缘 LLM agent 推理，把多路径 test-time scaling 拆为生成与验证，采用 speculative beam extension 缓解不规则路径 straggler、非对称多模型显存分配和 prefix-aware 调度复用搜索分支 KV cache。
  - 核心创新是把 TTS 搜索路径当作可调度 serving workload，在显存受限环境联合处理路径长尾、生成/验证模型驻留和前缀复用；它属于 Agent Infra 的推理层，而非修改完整规划-行动循环。
  - LLM 与生成式 AI 系统；Agent Infra；edge agent；test-time scaling；LLM

- [GS-Scale: Unlocking Large-Scale 3D Gaussian Splatting Training via Host Offloading](https://doi.org/10.1145/3779212.3790167)
  - Donghyun Lee (Seoul National University), Dawoon Jeong (Seoul National University), Jae W. Lee (Seoul National University), Hongil Yoon (Google)
  - GS-Scale 的官方标题与主会议程把研究对象限定为3D Gaussian Splatting 的训练、渲染与显存管理中的“Unlocking Large-Scale 3D Gaussian Splatting Training via Host Offloading”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Unlocking Large-Scale 3D Gaussian Splatting Training via Host Offloading”作为独立系统问题，而不只是沿用完全驻留单 GPU 的 3DGS 流水线；相对基线、机制组合和收益仍需正文核验。
  - ML 系统、GPU 与加速器；3D Gaussian Splatting & Rendering；3DGS；GPU memory

- [Neo: Real-Time On-Device 3D Gaussian Splatting with Reuse-and-Update Sorting Acceleration](https://doi.org/10.1145/3779212.3790192)
  - Changhun Oh (KAIST), Seongryong Oh (KAIST), Jinwoo Hwang (KAIST), Yoonsung Kim (KAIST), Hardik Sharma (Meta), Jongse Park (KAIST)
  - Neo 的官方标题与主会议程把研究对象限定为3D Gaussian Splatting 的训练、渲染与显存管理中的“Real-Time On-Device 3D Gaussian Splatting with Reuse-and-Update Sorting Acceleration”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Real-Time On-Device 3D Gaussian Splatting with Reuse-and-Update Sorting Acceleration”作为独立系统问题，而不只是沿用完全驻留单 GPU 的 3DGS 流水线；相对基线、机制组合和收益仍需正文核验。
  - ML 系统、GPU 与加速器；3D Gaussian Splatting & Rendering；3DGS；GPU memory

- [CLM: Removing the GPU Memory Barrier for 3D Gaussian Splatting](https://doi.org/10.1145/3779212.3790140)
  - Hexu Zhao (NYU), Xiwen Min (NYU), Xiaoteng Liu (NYU), Moonjun Gong (NYU), Yiming Li (NYU), Ang Li (PNNL and UW), Saining Xie (NYU), Jinyang Li (NYU), Aurojit Panda (NYU)
  - CLM 的官方标题与主会议程把研究对象限定为3D Gaussian Splatting 的训练、渲染与显存管理中的“Removing the GPU Memory Barrier for 3D Gaussian Splatting”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Removing the GPU Memory Barrier for 3D Gaussian Splatting”作为独立系统问题，而不只是沿用完全驻留单 GPU 的 3DGS 流水线；相对基线、机制组合和收益仍需正文核验。
  - ML 系统、GPU 与加速器；3D Gaussian Splatting & Rendering；3DGS；GPU memory；GPU

- [Nebula: Infinite-Scale 3D Gaussian Splatting in VR via Collaborative Rendering and Accelerated Stereo Rasterization](https://doi.org/10.1145/3779212.3790190)
  - He Zhu (Shanghai Jiao Tong University), Zheng Liu (Shanghai Jiao Tong University), Xingyang Li (Shanghai Jiao Tong University), Anbang Wu (Shanghai Jiao Tong University), Jieru Zhao (Department of Computer Science and Engineering, Shanghai Jiao Tong University), Fangxin Liu (Shanghai Jiao Tong University), Yiming Gan (ICT, Chinese Academy of Sciences), Jingwen Leng (Shanghai Jiao Tong University), Yu Feng (Shanghai Jiao Tong University)
  - Nebula 的官方标题与主会议程把研究对象限定为3D Gaussian Splatting 的训练、渲染与显存管理中的“Infinite-Scale 3D Gaussian Splatting in VR via Collaborative Rendering and Accelerated Stereo Rasterization”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Infinite-Scale 3D Gaussian Splatting in VR via Collaborative Rendering and Accelerated Stereo Rasterization”作为独立系统问题，而不只是沿用完全驻留单 GPU 的 3DGS 流水线；相对基线、机制组合和收益仍需正文核验。
  - ML 系统、GPU 与加速器；3D Gaussian Splatting & Rendering；3DGS；GPU memory

- [AGS: Accelerating 3D Gaussian Splatting SLAM via CODEC-Assisted Frame Covisibility Detection](https://doi.org/10.1145/3760250.3762229)
  - Houshu He (Shanghai Jiao Tong University), Naifeng Jing (Shanghai Jiao Tong University), Li Jiang (Shanghai Jiao Tong University), Xiaoyao Liang (Shanghai Jiao Tong University), Zhuoran Song (Shanghai Jiao Tong University)
  - AGS 的官方标题与主会议程把研究对象限定为3D Gaussian Splatting 的训练、渲染与显存管理中的“Accelerating 3D Gaussian Splatting SLAM via CODEC-Assisted Frame Covisibility Detection”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Accelerating 3D Gaussian Splatting SLAM via CODEC-Assisted Frame Covisibility Detection”作为独立系统问题，而不只是沿用完全驻留单 GPU 的 3DGS 流水线；相对基线、机制组合和收益仍需正文核验。
  - ML 系统、GPU 与加速器；3D Gaussian Splatting & Rendering；3DGS；GPU memory

- [Detecting Inconsistencies in ARM CCA’s Formally Verified Specification](https://doi.org/10.1145/3779212.3790152)
  - Changho Choi (Samsung Research), Xiang Cheng (Georgia Institute of Technology), Bokdeuk Jeong (Samsung Research), Taesoo Kim (Georgia Institute of Technology, Samsung Research)
  - Detecting Inconsistencies in ARM CCA’s 的官方标题与主会议程把研究对象限定为TEE、机密 serverless 与隐私保护模型监督中的“Detecting Inconsistencies in ARM CCA’s Formally Verified Specification”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Detecting Inconsistencies in ARM CCA’s Formally Verified Specification”作为独立系统问题，而不只是沿用单体 enclave 或仅软件隔离；相对基线、机制组合和收益仍需正文核验。
  - 安全、可靠性、验证与测试；Trusted Execution Environments；TEE；机密计算

- [WorksetEnclave: Towards Optimizing Cold Starts in Confidential Serverless with Workset-Based Enclave Restore](https://doi.org/10.1145/3779212.3790249)
  - Xiaolong Yan (Institute of Information Engineering, Chinese Academy of Sciences; School of Cyber Security, University of Chinese Academy of Sciences), Qihang Zhou (Institute of Information Engineering, Chinese Academy of Sciences), Zisen Wan (Institute of Information Engineering, Chinese Academy of Sciences; School of Cyber Security, University of Chinese Academy of Sciences), Feifan Qian (Institute of Information Engineering, Chinese Academy of Sciences; School of Cyber Security, University of Chinese Academy of Sciences), Wentao Yao (Institute of Information Engineering, Chinese Academy of Sciences; School of Cyber Security, University of Chinese Academy of Sciences), Weijuan Zhang (Institute of Information Engineering, Chinese Academy of Sciences), Xiaoqi Jia (Institute of Information Engineering, Chinese Academy of Sciences; School of Cyber Security, University of Chinese Academy of Sciences)
  - WorksetEnclave 的官方标题与主会议程把研究对象限定为TEE、机密 serverless 与隐私保护模型监督中的“Towards Optimizing Cold Starts in Confidential Serverless with Workset-Based Enclave Restore”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Towards Optimizing Cold Starts in Confidential Serverless with Workset-Based Enclave Restore”作为独立系统问题，而不只是沿用单体 enclave 或仅软件隔离；相对基线、机制组合和收益仍需正文核验。
  - 安全、可靠性、验证与测试；Trusted Execution Environments；TEE；机密计算；serverless

- [TEEM³: Core-Independent and Cooperating Trusted Execution Environments](https://doi.org/10.1145/3779212.3790232)
  - Nils Asmussen (Barkhausen Institut), Sebastian Haas (Barkhausen Institut), Carsten Weinhold (Barkhausen Institut), Nicholas Gordon (Barkhausen Institut), Stephan Gerhold (TU Dresden), Friedrich Pauls (Barkhausen Institut), Nilanjana Das (Barkhausen Institut), Michael Roitzsch (Barkhausen Institut)
  - TEEM³ 的官方标题与主会议程把研究对象限定为TEE、机密 serverless 与隐私保护模型监督中的“Core-Independent and Cooperating Trusted Execution Environments”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Core-Independent and Cooperating Trusted Execution Environments”作为独立系统问题，而不只是沿用单体 enclave 或仅软件隔离；相对基线、机制组合和收益仍需正文核验。
  - 安全、可靠性、验证与测试；Trusted Execution Environments；TEE；机密计算

- [WAVE: Leveraging Architecture Observation for Privacy-Preserving Model Oversight](https://doi.org/10.1145/3779212.3790247)
  - Haoxuan Xu (USC), Chen Gong (USC), Beijie Liu (USC), Haizhong Zheng (Carnegie Mellon University), Beidi Chen (Carnegie Mellon University), Mengyuan Li (USC)
  - WAVE 的官方标题与主会议程把研究对象限定为TEE、机密 serverless 与隐私保护模型监督中的“Leveraging Architecture Observation for Privacy-Preserving Model Oversight”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Leveraging Architecture Observation for Privacy-Preserving Model Oversight”作为独立系统问题，而不只是沿用单体 enclave 或仅软件隔离；相对基线、机制组合和收益仍需正文核验。
  - 安全、可靠性、验证与测试；Trusted Execution Environments；TEE；机密计算

- [Compass: Navigating the Design Space of Taint Schemes for RTL Security Verification](https://doi.org/10.1145/3779212.3790144)
  - Yuheng Yang (MIT), Qinhan Tan (Princeton University), Thomas Bourgeat (EPFL), Sharad Malik (Princeton University), Mengjia Yan (MIT)
  - Compass 的官方标题与主会议程把研究对象限定为TEE、机密 serverless 与隐私保护模型监督中的“Navigating the Design Space of Taint Schemes for RTL Security Verification”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Navigating the Design Space of Taint Schemes for RTL Security Verification”作为独立系统问题，而不只是沿用单体 enclave 或仅软件隔离；相对基线、机制组合和收益仍需正文核验。
  - 安全、可靠性、验证与测试；Trusted Execution Environments；TEE；机密计算

- [T-Control: An Efficient Dynamic Tensor Rematerialization System for DNN Training](https://doi.org/10.1145/3779212.3790230)
  - Zehua Wang (Institute of Computing Technology, Chinese Academy of Sciences), Junmin Xiao (Institute of Computing Technology, Chinese Academy of Sciences), Xiaochuan Deng (Institute of Computing Technology, Chinese Academy of Sciences), Huibing Wang (Institute of Computing Technology, Chinese Academy of Sciences), Hui Ma (Institute of Computing Technology, Chinese Academy of Sciences), Mingyi Li (Institute of Computing Technology, Chinese Academy of Sciences), Yunfei Pang (Institute of Computing Technology, Chinese Academy of Sciences), Guangming Tan (Institute of Computing Technology, Chinese Academy of Sciences)
  - T-Control 的官方标题与主会议程把研究对象限定为训练显存重计算、交互式 GPU 平台与性能诊断中的“An Efficient Dynamic Tensor Rematerialization System for DNN Training”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“An Efficient Dynamic Tensor Rematerialization System for DNN Training”作为独立系统问题，而不只是沿用长期绑定 GPU 和单层 profiler；相对基线、机制组合和收益仍需正文核验。
  - ML 系统、GPU 与加速器；ML Training & Monitoring；ML platform；profiling

- [NotebookOS: A Replicated Notebook Platform for Interactive Training with On-Demand GPUs](https://doi.org/10.1145/3760250.3762230)
  - Benjamin Carver (George Mason University), Jingyuan Zhang (George Mason University), Haoliang Wang (Adobe Research), Kanak Mahadik (Adobe Research), Yue Cheng (University of Virginia)
  - NotebookOS 针对交互式训练中 notebook 长时间在线但 GPU cell 间歇执行的问题，用 Raft 同步的多副本 kernel 分布在 GPU server 上，过量订阅资源并只在 cell 执行时分配 GPU，同时支持 replica migration 与集群弹性扩缩。
  - 核心创新是把 notebook 会话状态复制与按 cell 的 GPU 租约结合，解除交互状态长期存活和 GPU 长期占用之间的绑定。
  - ML 系统、GPU 与加速器；interactive training；notebook platform；on-demand GPU；GPU

- [DeepContext: A Context-aware, Cross-platform, and Cross-framework Tool for Performance Profiling and Analysis of Deep Learning Workloads](https://doi.org/10.1145/3676642.3736127)
  - Qidong Zhao (North Carolina State University), Hao Wu (George Mason University), Yueming Hao (North Carolina State University), Zilingfeng Ye, Jiajia Li (North Carolina State University), Xu Liu (North Carolina State University), Keren Zhou (George Mason University)
  - DeepContext 将 Python、PyTorch/JAX、C/C++ library 与 GPU device kernel 的调用上下文串联，在 NVIDIA/AMD GPU 和 x86/Arm CPU 上同时采集粗细粒度指标，并通过 GUI 与自动分析器把热点映射回可操作的源代码优化建议。
  - 核心创新是跨语言、框架和设备保留一条统一上下文链，而非让 CPU、framework 与 GPU profiler 各自输出无法关联的时间线。
  - ML 系统、GPU 与加速器；cross-stack profiling；performance diagnosis

- [Triton-Sanitizer: A Fast and Device-Agnostic Memory Sanitizer for Triton with Rich Diagnostic Context](https://doi.org/10.1145/3779212.3790241)
  - Hao Wu (George Mason University), Qidong Zhao (Google), Songqing Chen (George Mason University), Yang Chen (Meta), Yueming Hao (Meta), Tony CW Liu (Anthropic), Sijia Chen (Meta), Adnan Aziz (Meta), Keren Zhou (George Mason University)
  - Triton-Sanitizer 的官方标题与主会议程把研究对象限定为训练显存重计算、交互式 GPU 平台与性能诊断中的“A Fast and Device-Agnostic Memory Sanitizer for Triton with Rich Diagnostic Context”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“A Fast and Device-Agnostic Memory Sanitizer for Triton with Rich Diagnostic Context”作为独立系统问题，而不只是沿用长期绑定 GPU 和单层 profiler；相对基线、机制组合和收益仍需正文核验。
  - ML 系统、GPU 与加速器；ML Training & Monitoring；ML platform；profiling；Triton

- [LAIKA: Machine Learning-Assisted In-Kernel APU Acceleration](https://doi.org/10.1145/3779212.3790181)
  - Haoming Zhuo (South China Normal University), Dingding Li (South China Normal University), Ronghua Lin (South China Normal University), Yong Tang (South China Normal University)
  - LAIKA 的官方标题与主会议程把研究对象限定为训练显存重计算、交互式 GPU 平台与性能诊断中的“Machine Learning-Assisted In-Kernel APU Acceleration”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Machine Learning-Assisted In-Kernel APU Acceleration”作为独立系统问题，而不只是沿用长期绑定 GPU 和单层 profiler；相对基线、机制组合和收益仍需正文核验。
  - ML 系统、GPU 与加速器；ML Training & Monitoring；ML platform；profiling

- [FuseFlow: A Fusion-Centric Compilation Framework for Sparse Deep Learning on Streaming Dataflow](https://doi.org/10.1145/3779212.3790165)
  - Rubens Lacouture (Stanford University), Nathan Zhang (SambaNova Systems), Ritvik Sharma (Stanford University), Marco Siracusa (Barcelona Supercomputing Center), Fredrik Kjolstad (Stanford University), Kunle Olukotun (Stanford University), Olivia Hsu (Stanford University)
  - FuseFlow 将 PyTorch 稀疏模型编译成面向可重构数据流架构的 fused sparse dataflow graph，支持跨表达式融合、并行化、数据流排序和 sparsity blocking，并用周期级模拟器搜索 fusion granularity。
  - 核心创新是把跨 kernel 的通用稀疏融合纳入编译与设计空间探索；结论不是一味 full fusion，而是按模型剪枝不合适的融合配置。
  - ML 系统、GPU 与加速器；sparse ML compiler；cross-expression fusion

- [Trinity: Three-Dimensional Tensor Program Optimization via Tile-level Equality Saturation](https://doi.org/10.1145/3779212.3790240)
  - Jaehyeong Park (KAIST), Youngchan Kim (KAIST), Haechan An (KAIST), Gieun Jeong (KAIST), Jeehoon Kang (FuriosaAI), Dongsu Han (KAIST)
  - Trinity 的官方标题与主会议程把研究对象限定为ML 编译、张量程序、算子融合与动态数据流中的“Three-Dimensional Tensor Program Optimization via Tile-level Equality Saturation”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Three-Dimensional Tensor Program Optimization via Tile-level Equality Saturation”作为独立系统问题，而不只是沿用手写内核或局部、静态编译优化；相对基线、机制组合和收益仍需正文核验。
  - ML 系统、GPU 与加速器；ML Compilers & Tensor Programs；ML compiler；tensor program

- [RedFuser: An Automatic Operator Fusion Framework for Cascaded Reductions on AI Accelerators](https://doi.org/10.1145/3779212.3790209)
  - Xinsheng Tang (Alibaba Cloud Computing), Yangcheng Li (Alibaba Cloud Computing), Nan Wang (Alibaba Cloud Computing), Zhiyi Shu (Alibaba Cloud Computing), Xingyu Ling (Alibaba Cloud Computing), Junna Xing (Alibaba Cloud Computing), Peng Zhou (Alibaba Cloud Computing), Qiang Liu (Alibaba Cloud Computing)
  - RedFuser 针对 safe-softmax→GEMM 这类多循环且存在跨循环依赖的 cascaded reduction，先用形式化方法把它变换为单循环增量计算，再自动识别模式并生成融合 kernel。
  - 核心创新是把过去依赖手写特例的级联归约融合抽象成可判定、可生成的一般方法，覆盖现有 AI compiler 难以自动处理的模式。
  - ML 系统、GPU 与加速器；operator fusion；cascaded reduction

- [Linear Layouts: Robust Code Generation of Efficient Tensor Computation Using F2](https://doi.org/10.1145/3760250.3762221)
  - Keren Zhou (George Mason University and OpenAI), Mario Lezcano (OpenAI), Adam Goucher (OpenAI), Akhmed Rakhmati (OpenAI), Jeff Niu (OpenAI), Justin Lebar (OpenAI), Pawel Szczerbuk (OpenAI), Peter Bell (OpenAI), Phil Tillet (OpenAI), Thomas Raoux (OpenAI), Zahi Moudallal (OpenAI)
  - Linear Layouts 的官方标题与主会议程把研究对象限定为ML 编译、张量程序、算子融合与动态数据流中的“Robust Code Generation of Efficient Tensor Computation Using F2”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Robust Code Generation of Efficient Tensor Computation Using F2”作为独立系统问题，而不只是沿用手写内核或局部、静态编译优化；相对基线、机制组合和收益仍需正文核验。
  - ML 系统、GPU 与加速器；ML Compilers & Tensor Programs；ML compiler；tensor program

- [Streaming Tensor Program: A streaming abstraction for dynamic parallelism](https://doi.org/10.1145/3779212.3790229)
  - Gina Sohn (Stanford University), Genghan Zhang (Stanford University), Konstantin Hossfeld (Stanford University), Jungwoo Kim (Stanford University), Nathan Sobotka (Stanford University), Nathan Zhang (SambaNova Systems), Olivia Hsu (Stanford University), Kunle Olukotun (Stanford University)
  - STeP 为 spatial dataflow accelerator 引入 flexible routing、显式内存层次和 symbolic-shape 语义，使数据依赖 shape/control flow 能触发 dynamic tiling、dynamic parallelization 与 configuration time-multiplexing。
  - 核心创新是让动态数据率和张量维度成为编程抽象的一部分，而不是把动态模型静态展开后丢失优化机会。
  - ML 系统、GPU 与加速器；dynamic tensor；spatial dataflow

- [AlphaSyndrome: Tackling the Syndrome Measurement Circuit Scheduling Problem for QEC Codes](https://doi.org/10.1145/3779212.3790123)
  - Yuhao Liu (University of Pennsylvania), Shuohao Ping (University of Pennsylvania), Junyu Zhou (University of Pennsylvania), Ethan Decker (University of Pennsylvania), Justin Kalloor (University of California, Berkeley), Mathias Weiden (University of California, Berkeley), Kean Chen (University of Pennsylvania), Yunong Shi (Amazon Quantum Technologies), Ali Javadi-Abhari (IBM Research), Costin Iancu (Lawrence Berkeley National Laboratory), Gushu Li (University of Pennsylvania)
  - AlphaSyndrome 面向一般 commuting stabilizer code 的 syndrome-measurement 电路，在同时决定 stabilizer 测量顺序与可并行批次时，估计传播错误是否逼近 logical operator、能否被 decoder 纠正；MCTS 以编码结构和 decoder 反馈引导搜索，而不是只压低电路深度。
  - 核心创新是把 syndrome schedule 的目标从门数/深度改成真实 logical-error risk，并让 decoder-in-the-loop 的 MCTS 联合搜索顺序和并行性，覆盖手工规则难以处理的通用稳定子码。
  - 量子、FHE 与新型计算；AlphaSyndrome；QEC scheduling；MCTS；decoder feedback

- [PropHunt: Automated Optimization of Quantum Syndrome Measurement Circuits](https://doi.org/10.1145/3779212.3790205)
  - Joshua Viszlai (University of Chicago), Satvik Maurya (University of Wisconsin-Madison), Swamit Tannu (University of Wisconsin-Madison), Margaret R. Martonosi (Princeton University), Fred Chong (University of Chicago)
  - PropHunt 面向 CSS 量子纠错码，显式模拟 syndrome-measurement 电路内部的 hook error 传播，迭代修改 ancilla/CNOT 结构以压低逻辑错误；它既能自动恢复已知手工方案，也能为 Hook-ZNE 构造具有细粒度可控 logical error 的测量电路。
  - 核心创新是把可纠错性与逻辑错误传播作为自动优化信号；相比面向 NISQ 的通用门数/深度优化器，它专门搜索容错 syndrome circuit 的错误形态而非只缩短电路。
  - 量子、FHE 与新型计算；PropHunt；syndrome circuit；hook error；CSS code；量子计算

- [iSwitch: QEC on Demand via In-Situ Encoding of Bare Qubits for Ion Trap Architectures](https://doi.org/10.1145/3779212.3790177)
  - Keyi Yin (University of California, San Diego), Xiang Fang (University of California, San Diego), Zhuo Chen (University of California, San Diego), David Hayes (Quantinuum), Eneet Kaur (Cisco Quantum Lab), Reza Nejabati (Cisco Quantum Lab), Hartmut Haeffner (University of California, Berkeley), Wes Campbell (University of California, Los Angeles), Eric Hudson (University of California, Los Angeles), Jens Palsberg (University of California, Los Angeles), Travis Humble (Oak Ridge National Laboratory), Yufei Ding (University of California, San Diego)
  - iSwitch 的官方标题与主会议程把研究对象限定为量子纠错电路调度、编码与体系结构中的“QEC on Demand via In-Situ Encoding of Bare Qubits for Ion Trap Architectures”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“QEC on Demand via In-Situ Encoding of Bare Qubits for Ion Trap Architectures”作为独立系统问题，而不只是沿用固定纠错电路和静态编码；相对基线、机制组合和收益仍需正文核验。
  - 量子、FHE 与新型计算；Quantum Error Correction；量子纠错；QEC

- [Architecting Scalable Trapped Ion Quantum Computers using Surface Codes](https://doi.org/10.1145/3779212.3790128)
  - Scott Jones (University of Cambridge), Prakash Murali (University of Cambridge)
  - 该工作把 surface-code logical operation 编译到 trapped-ion QCCD 架构，使用接近最优的 topology-aware compiler 联合评估离子阱容量、阱间连接与控制电极布线；结果显示每阱仅 2 个离子反而优于常见 20–30 离子设想，并可把 logical clock 提升约 3.8 倍。
  - 核心创新是用完整纠错 workload 的编译与时序反馈反推 QCCD 物理拓扑，而不是先固定大容量 ion trap 再单独优化 mapping，得到违反直觉但可量化的架构设计点。
  - 量子、FHE 与新型计算；trapped ion；QCCD；surface code；architecture co-design；量子计算

- [Accelerating Computation in Quantum LDPC Code](https://doi.org/10.1145/3779212.3790122)
  - Jungmin Cho (Seoul National University), Hyeonseong Jeong (Seoul National University), Junpyo Kim (Seoul National University), Junhyuk Choi (Seoul National University), Juwon Hong (Seoul National University), Jangwoo Kim (Seoul National University / MangoBoost)
  - Accelerating Computation in Quantum LDPC 的官方标题与主会议程把研究对象限定为量子纠错电路调度、编码与体系结构中的“Accelerating Computation in Quantum LDPC Code”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Accelerating Computation in Quantum LDPC Code”作为独立系统问题，而不只是沿用固定纠错电路和静态编码；相对基线、机制组合和收益仍需正文核验。
  - 量子、FHE 与新型计算；Quantum Error Correction；量子纠错；QEC；量子计算

- [DARTH-PUM: A Hybrid Processing-Using-Memory Architecture](https://doi.org/10.1145/3779212.3790151)
  - Ryan Wong (University of Illinois Urbana-Champaign), Ben Feinberg (Sandia National Laboratories), Saugata Ghose (University of Illinois Urbana-Champaign)
  - DARTH-PUM 的官方标题与主会议程把研究对象限定为PIM/CIM、近存储处理与内存内数据库中的“A Hybrid Processing-Using-Memory Architecture”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“A Hybrid Processing-Using-Memory Architecture”作为独立系统问题，而不只是沿用频繁跨层搬运数据的 CPU/GPU 执行；相对基线、机制组合和收益仍需正文核验。
  - ML 系统、GPU 与加速器；Processing-in-Memory；PIM；CIM；近数据处理

- [PUSHtap: PIM-based In-Memory HTAP with Unified Data Storage Format](https://doi.org/10.1145/3676642.3736120)
  - Yilong Zhao (Shanghai Jiao Tong University), Mingyu Gao (Tsinghua University), Huanchen Zhang (Tsinghua University), Fangxin Liu (Shanghai Jiao Tong University), Gongye Chen (Shanghai Jiao Tong University), He Xian (Shanghai Qi Zhi Institute), Li Jiang (Shanghai Jiao Tong University)
  - PUSHtap 用 CPU 的交错访问与 PIM unit 的局部访问构成二维数据通路，以统一布局同时服务行式 OLTP 和列式 OLAP，并加入单实例 HTAP 所需的 MVCC 及 CPU/PIM 并发访问支持。
  - 核心创新是用一种物理格式同时满足事务新鲜度、分析隔离和两类访问局部性，避免多实例 HTAP 的复制与同步开销。
  - ML 系统、GPU 与加速器；HTAP；unified format；PIM；storage

- [CoGraf: Fully Accelerating Graph Applications with Fine-Grained PIM](https://doi.org/10.1145/3779212.3790142)
  - Mehmetali Semi Yenimol (Uppsala University), Anirban Nag (Huawei), Chang Hyun Park (Uppsala University), David Black-Schaffer (Uppsala University)
  - CoGraf 的官方标题与主会议程把研究对象限定为PIM/CIM、近存储处理与内存内数据库中的“Fully Accelerating Graph Applications with Fine-Grained PIM”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Fully Accelerating Graph Applications with Fine-Grained PIM”作为独立系统问题，而不只是沿用频繁跨层搬运数据的 CPU/GPU 执行；相对基线、机制组合和收益仍需正文核验。
  - ML 系统、GPU 与加速器；Processing-in-Memory；PIM；CIM；近数据处理

- [Ouroboros: Wafer-Scale SRAM CIM with Token-Grained Pipelining for Large Language Model Inference](https://doi.org/10.1145/3779212.3790197)
  - Yiqi Liu (University of Chinese Academy of Sciences), Yudong Pan (University of Chinese Academy of Sciences), Mengdi Wang (Institute of Computing Technology, Chinese Academy of Sciences), Shixin Zhao (University of Chinese Academy of Sciences), Haonan Zhu (University of Chinese Academy of Sciences), Yinhe Han (Institute of Computing Technology, Chinese Academy of Sciences), Lei Zhang (Institute of Computing Technology, Chinese Academy of Sciences), Ying Wang (Institute of Computing Technology, Chinese Academy of Sciences)
  - Ouroboros 在 wafer-scale SRAM CIM 上原位执行 LLM，通过 token-grained pipeline 消除序列长度差异造成的气泡，分布式动态 KV 管理利用碎片 SRAM，并以通信感知 mapping 兼顾局部性和坏核容错。
  - 核心创新是把 pipeline 粒度从 sequence 降到 token，并把 KV placement 与 wafer 通信映射联合设计，避免片外数据迁移。
  - ML 系统、GPU 与加速器；wafer-scale；SRAM CIM；token pipeline；CIM

- [A Cost-Effective Near-Storage Processing Solution for Offline Inference of Long-Context LLMs](https://doi.org/10.1145/3779212.3790119)
  - Hongsun Jang (Seoul National University), Jaeyong Song (Seoul National University), Changmin Shin (Seoul National University), Si Ung Noh (Seoul National University), Jaewon Jung (Seoul National University), Jisung Park (POSTECH (Pohang University of Science and Technology)), Jinho Lee (Seoul National University)
  - HILOS 面向长上下文离线 batch 推理，把 memory-bound attention 下推到 SmartSSD 的 near-storage accelerator，利用 cooperative X-cache 减少 KV I/O、延迟写回隐藏存储时延，并在 16 块 SmartSSD 上保持长序列 attention 吞吐。
  - 核心创新是只把 attention/KV 数据面推近存储，同时让 host 资源继续协作，而非把整模型粗粒度 offload 到 SSD。
  - ML 系统、GPU 与加速器；HILOS；near-storage processing；offline LLM；LLM；storage

- [TetriServe: Efficiently Serving Mixed DiT Workloads](https://doi.org/10.1145/3779212.3790233)
  - Runyu Lu (University of Michigan), Shiqi He (University of Michigan), Wenxuan Tan (UW-Madison), Shenggui Li (Nanyang Technological University), Ruofan Wu (University of Michigan), Jeff J. Ma (University of Michigan), Ang Chen (University of Michigan), Mosharaf Chowdhury (University of Michigan)
  - TetriServe 的官方标题与主会议程把研究对象限定为生成模型服务、组合式 AI 与低精度 GPU 编程中的“Efficiently Serving Mixed DiT Workloads”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Efficiently Serving Mixed DiT Workloads”作为独立系统问题，而不只是沿用单一模型/单一计算范式的 AI 栈；相对基线、机制组合和收益仍需正文核验。
  - LLM 与生成式 AI 系统；Generative Model Serving；生成模型；compound AI

- [Segment Only Where You Look: Leveraging Human Gaze Behavior for Efficient Computer Vision Applications in Augmented Reality](https://doi.org/10.1145/3779212.3790216)
  - Tianhua Xia (New York University), Haiyu Wang (New York University), Sai Qian Zhang (New York University)
  - Segment Only Where You Look 的官方标题与主会议程把研究对象限定为生成模型服务、组合式 AI 与低精度 GPU 编程中的“Leveraging Human Gaze Behavior for Efficient Computer Vision Applications in Augmented Reality”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Leveraging Human Gaze Behavior for Efficient Computer Vision Applications in Augmented Reality”作为独立系统问题，而不只是沿用单一模型/单一计算范式的 AI 栈；相对基线、机制组合和收益仍需正文核验。
  - LLM 与生成式 AI 系统；Generative Model Serving；生成模型；compound AI

- [Compositional AI Beyond LLMs: System Implications of Neuro-Symbolic-Probabilistic Architectures](https://doi.org/10.1145/3760250.3762235)
  - Zishen Wan (Georgia Tech), Hanchen Yang (Georgia Tech), Jiayi Qian (Georgia Tech), Ritik Raj (Georgia Tech), Joongun Park (Georgia Tech), Chenyu Wang (Princeton University), Arijit Raychowdhury (Georgia Tech), Tushar Krishna (Georgia Tech)
  - 该工作系统性表征由神经网络、符号推理和概率推断组合的 compound AI：建立组合 taxonomy，并在数学推理、安全/幻觉检测与具身规划等 workload 上分析 CPU/GPU 的 kernel、内存访问、控制流、依赖、通信和扩展性。
  - 核心创新不是提出一个更大的 LLM，而是首次把神经-符号-概率组合的准确性优势转化为跨算法、系统与硬件的瓶颈图谱和协同设计机会；它与 Agent 相关但不等于规划-行动型 Agent System。
  - LLM 与生成式 AI 系统；Compound AI System；neuro-symbolic-probabilistic；Agent 相关非 Agent System；LLM

- [It Takes Two to Entangle](https://doi.org/10.1145/3779212.3790178)
  - Zhanghan Wang (New York University), Ding Ding (New York University), Hang Zhu (ByteDance Inc.), Haibin Lin (ByteDance Inc.), Aurojit Panda (New York University)
  - It Takes Two to Entangle 的官方标题与主会议程把研究对象限定为生成模型服务、组合式 AI 与低精度 GPU 编程中的“It Takes Two to Entangle”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“It Takes Two to Entangle”作为独立系统问题，而不只是沿用单一模型/单一计算范式的 AI 栈；相对基线、机制组合和收益仍需正文核验。
  - LLM 与生成式 AI 系统；Generative Model Serving；生成模型；compound AI

- [Tilus: A Tile-Level GPGPU Programming Language for Low-Precision Computation](https://doi.org/10.1145/3760250.3762219)
  - Yaoyao Ding (Univerisity of Toronto / CentML), Bohan Hou (Carnegie Mellon University), Xiao Zhang (University of Toronto), Allan Lin (University of Waterloo), Tianqi Chen (Carnegie Mellon University), Cody Yu Hao (Anyscale), Yida Wang (Amazon), Gennady Pekhimenko (Univerisity of Toronto / CentML)
  - Tilus 是 tile-level GPGPU DSL，支持 1–8 bit 任意位宽、层次化内存和 algebraic layout，并经自动 vectorization/instruction selection 生成低精度 kernel，以开放寄存器和访存控制而不要求手写 CUDA。
  - 核心创新是在比 Triton 更低但仍可编程的 tile 抽象层统一任意位宽与布局，补齐高层 GPU DSL 无法表达细粒度低精度优化的问题。
  - LLM 与生成式 AI 系统；GPU DSL；arbitrary-bit precision；GPU

- [Neuralink: Fast on-Device LLM Inference with Neuron Co-Activation Linking](https://doi.org/10.1145/3676642.3736114)
  - Tuowei Wang (Tsinghua University), Ruwen Fan (Tsinghua University), Minxing Huang (Tianjin University), Zixu Hao (Tsinghua University), Kun Li (Microsoft Research), Ting Cao (Microsoft Research), Youyou Lu (Tsinghua University), Yaoxue Zhang (Tsinghua University), Ju Ren (Tsinghua University)
  - Neuralink 的官方标题与主会议程把研究对象限定为端侧 LLM/DNN、神经渲染和低比特加速中的“Fast on-Device LLM Inference with Neuron Co-Activation Linking”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Fast on-Device LLM Inference with Neuron Co-Activation Linking”作为独立系统问题，而不只是沿用整模型预加载和云端执行；相对基线、机制组合和收益仍需正文核验。
  - ML 系统、GPU 与加速器；On-Device & Edge AI；edge AI；on-device；LLM

- [Lifetime-Aware Design for Item-Level Intelligence at the Extreme Edge](https://doi.org/10.1145/3779212.3790182)
  - Shvetank Prakash (Harvard University), Andrew Cheng (Harvard University), Olof Kindgren (Qamcom), Ashiq Ahamed (Pragmatic Semiconductor), Graham Knight (Pragmatic Semiconductor), Jed Kufel (Pragmatic Semiconductor), Francisco Rodriguez (Pragmatic Semiconductor), Arya Tschand (Harvard University), David Kong (Harvard University), Mariam Elgamal (Harvard University), Jerry Huang (Harvard University), Emma Chen (Harvard University), Gage Hills (Harvard University), Richard Price (Pragmatic Semiconductor), Emre Ozer (Pragmatic Semiconductor), Vijay Janapa Reddi (Harvard University)
  - Lifetime-Aware Design for Item-Level Intelligence 的官方标题与主会议程把研究对象限定为端侧 LLM/DNN、神经渲染和低比特加速中的“Lifetime-Aware Design for Item-Level Intelligence at the Extreme Edge”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Lifetime-Aware Design for Item-Level Intelligence at the Extreme Edge”作为独立系统问题，而不只是沿用整模型预加载和云端执行；相对基线、机制组合和收益仍需正文核验。
  - ML 系统、GPU 与加速器；On-Device & Edge AI；edge AI；on-device

- [FlashMem: Supporting Modern DNN Workloads on Mobile with GPU Memory Hierarchy Optimizations](https://doi.org/10.1145/3779212.3790164)
  - Zhihao Shu (University of Georgia), Md Musfiqur Rahman Sanim (University of Georgia), Hangyu Zheng (University of Georgia), Kunxiong Zhu (University of Georgia), Miao Yin (University of Texas at Arlington), Gagan Agrawal (University of Georgia), Wei Niu (University of Georgia)
  - FlashMem 面向无法把大模型或多模型全集驻留的移动 GPU，离线确定权重加载 schedule，运行时按需流式传入，并利用 2.5D texture memory 减少格式转换和复制。
  - 核心创新是把移动端推理由全量 weight preload 改为编译期计划、运行时流式的层次化加载，使大模型容量和多模型切换不再直接受 DRAM 上限约束。
  - ML 系统、GPU 与加速器；mobile GPU；weight streaming；GPU

- [ASDR: Exploiting Adaptive Sampling and Data Reuse for CIM-based Instant Neural Rendering](https://doi.org/10.1145/3676642.3736117)
  - Fangxin Liu (Shanghai Jiao Tong University), Haomin Li (Shanghai Jiao Tong University), Bowen Zhu (Shanghai Jiao Tong University), Zongwu Wang (Shanghai Jiao Tong University), Zhuoran Song (Shanghai Jiao Tong University), Li Jiang (Shanghai Jiaotong University)
  - ASDR 面向 NeRF instant neural rendering，在运行时按像素难度动态决定射线采样量，将 volume rendering 的 color 与 density 计算解耦并近似复用中间数据，再把访问模式映射到 ReRAM CIM；相对既有 NeRF 加速器和 Jetson Xavier 分别实现约 9.55 倍、69.75 倍加速，PSNR 损失约 0.1。
  - 核心创新是让采样密度和数据复用随画面难度变化，并与 CIM 数据布局共同设计；不同于固定每射线采样或只把 MLP 搬进存内计算，它同时减少无效样本、重复计算和数据搬运。
  - ML 系统、GPU 与加速器；ASDR；NeRF；adaptive sampling；ReRAM CIM；CIM

- [BitRed: Taming Non-Uniform Bit-Level Sparsity with a Programmable RISC-V ISA for DNN Acceleration](https://doi.org/10.1145/3779212.3790132)
  - yanhuan liu (ICT), wenming li (ICT), kunming zhang (ICT), yuqun liu (ICT), siao wen (SmarCo Co., Ltd), lexin wang (ICT), tianyu liu (ICT), haibin wu (ICT), zhihua fan (ICT), xiaochun ye (ICT), dongrui fan (SmarCo Co., Ltd), xuejun an (ICT)
  - BitRed 的官方标题与主会议程把研究对象限定为端侧 LLM/DNN、神经渲染和低比特加速中的“Taming Non-Uniform Bit-Level Sparsity with a Programmable RISC-V ISA for DNN Acceleration”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Taming Non-Uniform Bit-Level Sparsity with a Programmable RISC-V ISA for DNN Acceleration”作为独立系统问题，而不只是沿用整模型预加载和云端执行；相对基线、机制组合和收益仍需正文核验。
  - ML 系统、GPU 与加速器；On-Device & Edge AI；edge AI；on-device；RISC-V

- [Graphiti: Formally Verified Out-of-Order Execution in Dataflow Circuits](https://doi.org/10.1145/3779212.3790166)
  - Yann Herklotz (EPFL), Ayatallah Elakhras (EPFL), Martina Camaioni (EPFL), Paolo Ienne (EPFL), Lana Josipovic (ETH Zurich), Thomas Bourgeat (EPFL)
  - Graphiti 的官方标题与主会议程把研究对象限定为形式验证、符号执行与 LLM 辅助系统测试中的“Formally Verified Out-of-Order Execution in Dataflow Circuits”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Formally Verified Out-of-Order Execution in Dataflow Circuits”作为独立系统问题，而不只是沿用人工编写生成器或单一验证层；相对基线、机制组合和收益仍需正文核验。
  - 安全、可靠性、验证与测试；Formal Verification；形式验证；fuzzing

- [Highly Automated Verification of Security Properties for Unmodified System Software](https://doi.org/10.1145/3779212.3790171)
  - Ganxiang Yang (Columbia University), Wei Qiang (Columbia University), Yi Rong (Columbia University), Xuheng Li (Columbia University), Fanqi Yu (Columbia University), Jason Nieh (Columbia University), Ronghui Gu (Columbia University)
  - Highly Automated Verification of Security 的官方标题与主会议程把研究对象限定为形式验证、符号执行与 LLM 辅助系统测试中的“Highly Automated Verification of Security Properties for Unmodified System Software”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Highly Automated Verification of Security Properties for Unmodified System Software”作为独立系统问题，而不只是沿用人工编写生成器或单一验证层；相对基线、机制组合和收益仍需正文核验。
  - 安全、可靠性、验证与测试；Formal Verification；形式验证；fuzzing

- [SylQ-SV: Scaling Symbolic Execution of Hardware Designs with Query Caching](https://doi.org/10.1145/3676642.3736123)
  - Kaki Ryan (University of North Carolina at Chapel Hill), Cynthia Sturton (University of North Carolina at Chapel Hill)
  - SylQ-SV 的官方标题与主会议程把研究对象限定为形式验证、符号执行与 LLM 辅助系统测试中的“Scaling Symbolic Execution of Hardware Designs with Query Caching”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Scaling Symbolic Execution of Hardware Designs with Query Caching”作为独立系统问题，而不只是沿用人工编写生成器或单一验证层；相对基线、机制组合和收益仍需正文核验。
  - 安全、可靠性、验证与测试；Formal Verification；形式验证；fuzzing

- [Once-for-All: Skeleton-Guided SMT Solver Fuzzing with LLM-Synthesized Generators](https://doi.org/10.1145/3779212.3790195)
  - Maolin Sun (Nanjing University), Yibiao Yang (Nanjing University), Yuming Zhou (Nanjing University)
  - Once4All 不让 LLM 在每次 fuzzing 时直接生成 SMT 公式，而是一次性从文档提取 solver/理论的 CFG，并合成可组合 Boolean term generator；运行阶段用这些生成器填充既有公式 skeleton，以保证语法有效并扩展语义多样性。
  - 核心创新是把 LLM 成本前移为可复用生成器合成，区别于逐样本 prompt；运行时没有规划-行动反馈闭环，因此归为 LLM for Systems 而非 Agent。
  - 安全、可靠性、验证与测试；LLM for Systems；SMT fuzzing；generator synthesis；LLM

- [LPO: Discovering Missed Peephole Optimizations with Large Language Models](https://doi.org/10.1145/3779212.3790184)
  - Zhenyang Xu (University of Waterloo), Hongxu Xu (University of Waterloo), Yongqiang Tian (Monash University), Xintong Zhou (University of Waterloo), Chengnian Sun (University of Waterloo)
  - LPO 让 LLM 提议此前遗漏的 peephole rewrite，再由形式验证器检查语义等价，并把失败信息反馈给后续探索，持续在 LLVM 中发现可接受优化。
  - 核心创新是把 LLM 的探索性与 formal verifier 的正确性组成闭环，而非直接采信生成代码；具有提议-验证-反馈迭代，归为 Agent for Systems。
  - 安全、可靠性、验证与测试；Agent for Systems；peephole optimization；formal feedback

- [Nemo: A Low-Write-Amplification Cache for Tiny Objects on Log-Structured Flash Devices](https://doi.org/10.1145/3779212.3790191)
  - Xufeng Yang (Xiamen University), Tingting Tan (Xiamen University), Jingxin Hu (Chongqing University of Posts and Telecommunications), Congming Gao (Xiamen University), Mingyang Liu (Xiamen University), Tianyang Jiang (Huawei Technologies Co., Ltd.), Jian Chen (Tsinghua University), Linbo Long (Chongqing University of Posts and Telecommunications), Yina Lv (Xiamen University), Jiwu Shu (Xiamen University)
  - Nemo 针对 log-structured flash 上的大量 tiny object cache，故意提高 hash collision 来填满每次顺序写入的 set、降低应用层写放大；Bloom-filter 索引压低 DRAM 元数据开销，混合 hotness tracking 则避免碰撞带来的命中率损失。
  - 核心创新是认识到设备自身低写放大并不能消除 tiny-object cache 的碎片写入，于是联合设计碰撞式布局、近似索引和热度跟踪，同时优化应用写放大、内存占用和 miss rate。
  - 内存、存储与解耦资源；Nemo；tiny-object cache；write amplification；log-structured flash；cache

- [ICARUS: Criticality and Reuse based Instruction Caching for Datacenter Applications](https://doi.org/10.1145/3779212.3790175)
  - Vedant Kalbande (Indian Institute of Technology Bombay), Hrishikesh Jedhe Deshmukh (Indian Institute of Technology Bombay), Alberto Ros (University of Murcia), Biswabandan Panda (Indian Institute of Technology Bombay)
  - ICARUS 的官方标题与主会议程把研究对象限定为Flash cache、指令缓存、网络 I/O 与请求提交中的“Criticality and Reuse based Instruction Caching for Datacenter Applications”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Criticality and Reuse based Instruction Caching for Datacenter Applications”作为独立系统问题，而不只是沿用仅以 miss rate 或设备级写放大衡量缓存；相对基线、机制组合和收益仍需正文核验。
  - 内存、存储与解耦资源；Storage & Caching；storage；cache；I/O

- [CacheMind: From Miss Rates to Why – Natural-Language, Trace-Grounded Reasoning for Cache Replacement](https://doi.org/10.1145/3779212.3790136)
  - Kaushal Mhapsekar (NC State University), Azam Ghanbari (Department of ECE, NC State University), Bita Aslrousta (North Carolina State University), Samira Mirbagher (NC State University)
  - CacheMind 用面向 cache trace 的检索器加 LLM，让体系结构研究者以自然语言追问某个 PC 为何发生 eviction，并把答案落回 trace 与程序语义；CacheMindBench 分别检验 trace-grounded 和 policy-specific reasoning。
  - 核心创新是从只比较 miss rate 转向可追溯的因果解释接口；它给人分析建议但不自主修改和验证 cache policy，因此归为 LLM for Systems。
  - 内存、存储与解耦资源；LLM for Systems；trace-grounded RAG；cache analysis；cache

- [Toasty: Speeding up network I/O with cache-warm buffers](https://doi.org/10.1145/3779212.3790235)
  - Preeti Preeti (IIT Bombay), Nitish Bhat (IIT Bombay), Ashwin Kumar (IIT Bombay), Mythili Vutukuru (Indian Institute of Technology, Bombay)
  - Toasty 的官方标题与主会议程把研究对象限定为Flash cache、指令缓存、网络 I/O 与请求提交中的“Speeding up network I/O with cache-warm buffers”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Speeding up network I/O with cache-warm buffers”作为独立系统问题，而不只是沿用仅以 miss rate 或设备级写放大衡量缓存；相对基线、机制组合和收益仍需正文核验。
  - 内存、存储与解耦资源；Storage & Caching；storage；cache；I/O

- [Hitchhike: Efficient Request Submission via Deferred Enforcement of Address Contiguity](https://doi.org/10.1145/3779212.3790173)
  - xuda zheng (Huazhong University of Science and Technology), Jian Zhou (Huazhong University of Science and Technology), Shuhan Bai (Huazhong University of Science and Technology), Runjin Wu (Huazhong University of Science and Technology), Xianlin Tang (Huazhong University of Science and Technology), Zhiyuan Li (Huazhong University of Science and Technology), Hong Jiang (UT Arlington), Fei Wu (Huazhong University of Science and Technology)
  - Hitchhike 的官方标题与主会议程把研究对象限定为Flash cache、指令缓存、网络 I/O 与请求提交中的“Efficient Request Submission via Deferred Enforcement of Address Contiguity”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Efficient Request Submission via Deferred Enforcement of Address Contiguity”作为独立系统问题，而不只是沿用仅以 miss rate 或设备级写放大衡量缓存；相对基线、机制组合和收益仍需正文核验。
  - 内存、存储与解耦资源；Storage & Caching；storage；cache；I/O

- [History Doesn’t Repeat Itself but Rollouts Rhyme: Accelerating Reinforcement Learning with HistoRL](https://doi.org/10.1145/3779212.3790172)
  - Jingkai He (Shanghai Jiao Tong University), Tianjian Li (ByteDance), Erhu Feng (Shanghai Jiao Tong University), Dong Du (Shanghai Jiao Tong University), Qian Liu (ByteDance), Tao Liu (ByteDance), Yubin Xia (Shanghai Jiao Tong University), Haibo Chen (Shanghai Jiao Tong University)
  - History Doesn’t Repeat Itself but Rollouts Rhyme 的官方标题与主会议程把研究对象限定为RL 执行、神经算子和具身 AI 可靠加速中的“Accelerating Reinforcement Learning with HistoRL”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Accelerating Reinforcement Learning with HistoRL”作为独立系统问题，而不只是沿用模型层和硬件层彼此独立的优化；相对基线、机制组合和收益仍需正文核验。
  - ML 系统、GPU 与加速器；Neural Network Acceleration；AI accelerator；embodied AI

- [Hardwired-Neuron Language Processing Units as General-Purpose Cognitive Substrates](https://doi.org/10.1145/3779212.3790169)
  - Yang Liu (Institute of Computing Technology, Chinese Academy of Sciences), Yi Chen (University of Science and Technology of China), Yongwei Zhao (Institute of Computing Technology, Chinese Academy of Sciences), Yifan Hao (Institute of Computing Technology, Chinese Academy of Sciences), Zifu Zheng (Institute of Computing Technology, Chinese Academy of Sciences), Weihao Kong (Institute of Computing Technology, Chinese Academy of Sciences), Zhangmai Li (University of Science and Technology of China), Dongchen Jiang (Institute of Computing Technology, Chinese Academy of Sciences), Ruiyang Xia (Institute of Computing Technology, Chinese Academy of Sciences), Zhihong Ma (Institute of Computing Technology, Chinese Academy of Sciences), Zisheng Liu (Institute of Computing Technology, Chinese Academy of Sciences), Zhaoyong Wan (Institute of Computing Technology, Chinese Academy of Sciences), Yunqi Lu (Institute of Computing Technology, Chinese Academy of Sciences), Ximing Liu (Institute of Computing Technology, Chinese Academy of Sciences), Hongrui Guo (Institute of Computing Technology, Chinese Academy of Sciences), Zhihao Yang (Institute of Software, Chinese Academy of Sciences), Zhe Wang (Institute of Computing Technology, Chinese Academy of Sciences), Tianrui Ma (Institute of Computing Technology, Chinese Academy of Sciences), Mo Zou (Institute of Computing Technology, Chinese Academy of Sciences), Rui Zhang (Institute of Computing Technology, Chinese Academy of Sciences), Ling Li (Institute of Software, Chinese Academy of Sciences), Xing Hu (Institute of Computing Technology, Chinese Academy of Sciences), Zidong Du (Institute of Computing Technology, Chinese Academy of Sciences), Zhiwei Xu (Institute of Computing Technology, Chinese Academy of Sciences), Qi Guo (Institute of Computing Technology, Chinese Academy of Sciences), Tiashi Chen (Cambricon Technologies), Yunji Chen (Institute of Computing Technology, Chinese Academy of Sciences)
  - Hardwired-Neuron Language Processing Units as 的官方标题与主会议程把研究对象限定为RL 执行、神经算子和具身 AI 可靠加速中的“Hardwired-Neuron Language Processing Units as General-Purpose Cognitive Substrates”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Hardwired-Neuron Language Processing Units as General-Purpose Cognitive Substrates”作为独立系统问题，而不只是沿用模型层和硬件层彼此独立的优化；相对基线、机制组合和收益仍需正文核验。
  - ML 系统、GPU 与加速器；Neural Network Acceleration；AI accelerator；embodied AI

- [Voyager: Input-Adaptive Algebraic Transformations for High-Performance Graph Neural Networks](https://doi.org/10.1145/3676642.3736121)
  - Yangjie Zhou (Shanghai Jiao Tong University), Wenting Shen (Alibaba Group), Jingwen Leng (Shanghai Jiao Tong University), Shuwen Lu (Shanghai Jiao Tong University), Zihan Liu (Shanghai Jiao Tong University), Weihao Cui (Shanghai Jiao Tong University), Zhendong Zhang (Shanghai Qi Zhi Institute), Wencong Xiao (Alibaba Group), Baole Ai (Alibaba Group), Wei Lin (Alibaba Group), Deze Zeng (China University of Geosciences), Yun Liang (Peking University), Quan Chen (Shanghai Jiao Tong University), Ning Liu (Shanghai Jiao Tong University), Minyi Guo (Shanghai Jiao Tong University)
  - Voyager 的官方标题与主会议程把研究对象限定为RL 执行、神经算子和具身 AI 可靠加速中的“Input-Adaptive Algebraic Transformations for High-Performance Graph Neural Networks”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Input-Adaptive Algebraic Transformations for High-Performance Graph Neural Networks”作为独立系统问题，而不只是沿用模型层和硬件层彼此独立的优化；相对基线、机制组合和收益仍需正文核验。
  - ML 系统、GPU 与加速器；Neural Network Acceleration；AI accelerator；embodied AI

- [CREATE: Cross-Layer Resilience Characterization and Optimization for Efficient yet Reliable Embodied AI Systems](https://doi.org/10.1145/3779212.3790147)
  - Tong Xie (Peking University), Yijiahao Qi (Peking University), Jinqi Wen (Peking University), Zishen Wan (Georgia Tech), Yanchi Dong (Peking University), Zihao Wang (Peking University), Shaofei Cai (Peking University), Yitao Liang (Peking University), Tianyu Jia (Peking University), Yuan Wang (Peking University), Runsheng Wang (Peking University), Meng Li (Peking University)
  - CREATE 面向由 LLM planner 和 RL controller 组成的具身 AI，在降压 bit error 下做跨层韧性设计：电路层检测/清除异常，模型层旋转权重增强 planner 容错，应用层按 autonomy 状态在线调 controller 电压。
  - 核心创新是先测得规划器、控制器与电路的非均匀容错，再据此跨层分配电压和冗余；论文优化的是具身 Agent 的可靠执行平台，不是规划算法本身。
  - ML 系统、GPU 与加速器；Agent Infra；embodied AI；cross-layer resilience

- [Syno: Structured Synthesis for Neural Operators](https://doi.org/10.1145/3676642.3736118)
  - Yongqi Zhuo (Tsinghua University), Zhengyuan Su (Tsinghua University), Chenggang Zhao (Tsinghua University), Mingyu Gao (Tsinghua University)
  - Syno 用定义在 tensor dimension 上的细粒度 primitive、表达式 canonicalization、受维度约束的 guided synthesis 和 stochastic tree search，自动发现新的 neural operator，而非只组合已有 operator。
  - 核心创新是把 NAS 与 tensor compiler 之外的 operator synthesis 做成端到端搜索，并用结构约束压缩等价候选空间。
  - ML 系统、GPU 与加速器；operator synthesis；structured search

- [Parameterized Hardware Design with Latency-Abstract Interfaces](https://doi.org/10.1145/3779212.3790199)
  - Rachit Nigam (Massachusetts Institute of Technology), Edmund Lam (Cornell University), Ethan Gabizon (Cornell University), Carolyn Zech (Massachusetts Institute of Technology), Jonathan Balkind (UC Santa Barbara), Adrian Sampson (Cornell University)
  - 该工作提出 latency-abstract interface，让硬件模块在设计期可改变流水延迟，同时通过 output parameter 编译成高效 latency-sensitive 接口；Lilac HDL 的类型系统追踪参数对信号时序的影响，并静态保证组合后不存在 structural hazard。
  - 核心创新是让 timing adaptability 成为可类型检查、可在编译后擦除的接口抽象，兼得 latency-insensitive 设计复用性与 latency-sensitive 电路效率，而不是靠人工同步不同参数化实现。
  - 编译、PL 与处理器微体系结构；Lilac；latency-abstract interface；HDL type system；structural hazard

- [Anvil: A General-Purpose Timing-Safe Hardware Description Language](https://doi.org/10.1145/3779212.3790125)
  - Jason Zhijingcheng Yu (National University of Singapore), Aditya Ranjan Jha (National University of Singapore), Umang Mathur (National University of Singapore), Trevor E. Carlson (National University of Singapore), Prateek Saxena (National University of Singapore)
  - Anvil 在保留寄存器、wire 和逐周期控制的同时，用类型系统追踪 mutation、signal use 与跨模块 timing contract；参数化 abstract time point 还能表达随配置变化的动态时序，从编译期阻止读写冲突和错误周期连接。
  - 核心创新是以通用 HDL 的静态类型保证 timing safety，而不是通过高层抽象隐藏周期或依赖仿真发现 hazard，使模块仍可做精细微体系结构优化并安全组合。
  - 编译、PL 与处理器微体系结构；Anvil；timing safety；HDL；type system

- [Rage Against the State Machine: Type-Stated Hardware Peripherals for Increased Driver Correctness](https://doi.org/10.1145/3779212.3790207)
  - Tyler Potyondy (UC San Diego), Anthony Tarbinian (UC San Diego), Leon Schuermann (Princeton University), Eric Mugnier (UC San Diego), Adin Ackerman (UC San Diego), Amit Levy (Princeton University), Pat Pannuto (UC San Diego)
  - Rage Against the State Machine 的官方标题与主会议程把研究对象限定为硬件描述语言、接口类型和 RTL 仿真中的“Type-Stated Hardware Peripherals for Increased Driver Correctness”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Type-Stated Hardware Peripherals for Increased Driver Correctness”作为独立系统问题，而不只是沿用时序/状态约束隐含在实现中的 HDL；相对基线、机制组合和收益仍需正文核验。
  - 编译、PL 与处理器微体系结构；Hardware Design Languages；HDL；RTL

- [RTeAAL Sim: Using Tensor Algebra to Represent and Accelerate RTL Simulation](https://doi.org/10.1145/3779212.3790214)
  - Yan Zhu (University of California, Berkeley), Boru Chen (University of California, Berkeley), Christopher W. Fletcher (University of California, Berkeley), Nandeeka Nayak (University of California, Berkeley)
  - RTeAAL Sim 把 RTL 状态更新表示为 sparse tensor algebra，使模拟器的编译前端和生成代码规模不再随被模拟二进制线性膨胀，并复用稀疏代数优化来执行状态转换；在多种 CPU/ISA 上性能可与 Verilator 竞争，同时降低编译和 I-cache 压力。
  - 核心创新是用张量表达把 RTL 行为与程序镜像大小解耦，将电路仿真转化为已有成熟优化空间，而非继续生成庞大的逐信号 C++ 模拟代码。
  - 编译、PL 与处理器微体系结构；RTeAAL Sim；RTL simulation；sparse tensor algebra；I-cache

- [Sequential Specifications for Precise Hardware Exceptions](https://doi.org/10.1145/3760250.3762233)
  - Yulun Yao (Cornell University), Drew Zagieboylo (NVIDIA), G. Edward Suh (Cornell University / NVIDIA), Andrew Myers (Cornell University)
  - Sequential Specifications for Precise Hardware 的官方标题与主会议程把研究对象限定为硬件描述语言、接口类型和 RTL 仿真中的“Sequential Specifications for Precise Hardware Exceptions”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Sequential Specifications for Precise Hardware Exceptions”作为独立系统问题，而不只是沿用时序/状态约束隐含在实现中的 HDL；相对基线、机制组合和收益仍需正文核验。
  - 编译、PL 与处理器微体系结构；Hardware Design Languages；HDL；RTL

- [TempGraph: An Efficient Chain-driven Temporal Graph Computing Framework on the GPU](https://doi.org/10.1145/3676642.3736116)
  - Jin Zhao (Huazhong University of Science and Technology), Qian Wang (Huazhong University of Science and Technology), Ligang He (University of Warwick), Yu Zhang (Huazhong University of Science and Technology), Sheng Di (Argonne National Laboratory), Bingsheng He (National University of Singapore), Xinlei Wang (Huazhong University of Science and Technology), Hui Yu (Huazhong University of Science and Technology), Hao Qi (Huazhong University of Science and Technology), Longlong Lin (Southwest University), Linchen Yu (Huazhong University of Science and Technology), Xiaofei Liao (Huazhong University of Science and Technology), Hai Jin (Huazhong University of Science and Technology)
  - TempGraph 的官方标题与主会议程把研究对象限定为图、稀疏计算和图数据库优化中的“An Efficient Chain-driven Temporal Graph Computing Framework on the GPU”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“An Efficient Chain-driven Temporal Graph Computing Framework on the GPU”作为独立系统问题，而不只是沿用不利用时序/稀疏结构的通用执行；相对基线、机制组合和收益仍需正文核验。
  - ML 系统、GPU 与加速器；Graph & Sparse Computing；graph systems；sparse computing；GPU

- [Leveraging Sparsity to Accelerate Automata Processing](https://doi.org/10.1145/3676642.3736126)
  - Xingran Du (MIT), Joel S. Emer (MIT/NVIDIA), Daniel Sanchez (MIT)
  - Leveraging Sparsity to Accelerate Automata 的官方标题与主会议程把研究对象限定为图、稀疏计算和图数据库优化中的“Leveraging Sparsity to Accelerate Automata Processing”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Leveraging Sparsity to Accelerate Automata Processing”作为独立系统问题，而不只是沿用不利用时序/稀疏结构的通用执行；相对基线、机制组合和收益仍需正文核验。
  - ML 系统、GPU 与加速器；Graph & Sparse Computing；graph systems；sparse computing

- [SLAWS: Spatial Locality Analysis and Workload Orchestration for Sparse Matrix Multiplication](https://doi.org/10.1145/3779212.3790222)
  - Guoyu Li (Fudan University), Zheng Guan (Fudan University), Beichen Zhang (Fudan University), Jun Yu (Fudan University), Kun Wang (Fudan University)
  - SLAWS 的官方标题与主会议程把研究对象限定为图、稀疏计算和图数据库优化中的“Spatial Locality Analysis and Workload Orchestration for Sparse Matrix Multiplication”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Spatial Locality Analysis and Workload Orchestration for Sparse Matrix Multiplication”作为独立系统问题，而不只是沿用不利用时序/稀疏结构的通用执行；相对基线、机制组合和收益仍需正文核验。
  - ML 系统、GPU 与加速器；Graph & Sparse Computing；graph systems；sparse computing

- [Efficient Temporal Graph Network Training via Unified Redundancy Elimination](https://doi.org/10.1145/3779212.3790157)
  - Yiqing Wang (Beihang University), Hailong Yang (Beihang University), Kejie Ma (Beihang University), Enze Yu (Beihang University), Pengbo Wang (Beihang University), Xin You (Beihang University), Qingxiao Sun (Beihang University), Chenhao Xie (Beihang University), Zhongzhi Luan (Beihang University), Yi Liu (Beihang University), Depei Qian (Beihang University)
  - Efficient Temporal Graph Network Training 的官方标题与主会议程把研究对象限定为图、稀疏计算和图数据库优化中的“Efficient Temporal Graph Network Training via Unified Redundancy Elimination”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Efficient Temporal Graph Network Training via Unified Redundancy Elimination”作为独立系统问题，而不只是沿用不利用时序/稀疏结构的通用执行；相对基线、机制组合和收益仍需正文核验。
  - ML 系统、GPU 与加速器；Graph & Sparse Computing；graph systems；sparse computing

- [Understanding Query Optimization Bugs in Graph Database Systems](https://doi.org/10.1145/3779212.3790244)
  - Zhongxing Yu (Shandong University), Yuyu Chen (Shandong University)
  - Understanding Query Optimization Bugs in 的官方标题与主会议程把研究对象限定为图、稀疏计算和图数据库优化中的“Understanding Query Optimization Bugs in Graph Database Systems”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Understanding Query Optimization Bugs in Graph Database Systems”作为独立系统问题，而不只是沿用不利用时序/稀疏结构的通用执行；相对基线、机制组合和收益仍需正文核验。
  - ML 系统、GPU 与加速器；Graph & Sparse Computing；graph systems；sparse computing

- [Efficient Remote Memory Ordering for Non-Coherent Systems](https://doi.org/10.1145/3779212.3790156)
  - Wei Siew Liew (University of Utah), Md Ashfaqur Rahaman (University of Utah), Adarsh Patil (Arm), Ryan Stutsman (University of Utah), Vijay Nagarajan (University of Utah)
  - Efficient Remote Memory Ordering for 的官方标题与主会议程把研究对象限定为远端内存顺序、事务、页迁移与存储下推中的“Efficient Remote Memory Ordering for Non-Coherent Systems”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Efficient Remote Memory Ordering for Non-Coherent Systems”作为独立系统问题，而不只是沿用单机一致性假设和全页迁移；相对基线、机制组合和收益仍需正文核验。
  - 内存、存储与解耦资源；Disaggregated Memory Systems；disaggregated memory；remote memory

- [CPU-Oblivious Offloading of Failure-Atomic Transactions for Disaggregated Memory](https://doi.org/10.1145/3779212.3790146)
  - Cheng Chen (Huazhong University of Science and Technology), Chencheng Ye (Huazhong University of Science and Technology), Yuanchao Xu (University of California, Santa Cruz), Xipeng Shen (North Carolina State University), Xiaofei Liao (Huazhong University of Science and Technology), Hai Jin (Huazhong University of Science and Technology), Wenbin Jiang (Huazhong University of Science and Technology), Yan Solihin (U. of Central Florida)
  - CPU-Oblivious Offloading of Failure-Atomic Transactions 的官方标题与主会议程把研究对象限定为远端内存顺序、事务、页迁移与存储下推中的“CPU-Oblivious Offloading of Failure-Atomic Transactions for Disaggregated Memory”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“CPU-Oblivious Offloading of Failure-Atomic Transactions for Disaggregated Memory”作为独立系统问题，而不只是沿用单机一致性假设和全页迁移；相对基线、机制组合和收益仍需正文核验。
  - 内存、存储与解耦资源；Disaggregated Memory Systems；disaggregated memory；remote memory

- [PIPM: Partial and Incremental Page Migration for Multi-host CXL Disaggregated Shared Memory](https://doi.org/10.1145/3779212.3790203)
  - Gangqi Huang (University of California, Santa Cruz), Heiner Litz (University of California, Santa Cruz), Yuanchao Xu (University of California, Santa Cruz)
  - PIPM 的官方标题与主会议程把研究对象限定为远端内存顺序、事务、页迁移与存储下推中的“Partial and Incremental Page Migration for Multi-host CXL Disaggregated Shared Memory”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Partial and Incremental Page Migration for Multi-host CXL Disaggregated Shared Memory”作为独立系统问题，而不只是沿用单机一致性假设和全页迁移；相对基线、机制组合和收益仍需正文核验。
  - 内存、存储与解耦资源；Disaggregated Memory Systems；disaggregated memory；remote memory；CXL

- [CREST: High-Performance Contention Resolution for Disaggregated Transactions](https://doi.org/10.1145/3779212.3790148)
  - Qihan Kang (Institute of Computing Technology, Chinese Academy of Sciences), Mi Zhang (Institute of Computing Technology, Chinese Academy of Sciences), Patrick P. C. Lee (The Chinese University of Hong Kong), Yongkang Hu (Institute of Computing Technology, Chinese Academy of Sciences)
  - CREST 的官方标题与主会议程把研究对象限定为远端内存顺序、事务、页迁移与存储下推中的“High-Performance Contention Resolution for Disaggregated Transactions”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“High-Performance Contention Resolution for Disaggregated Transactions”作为独立系统问题，而不只是沿用单机一致性假设和全页迁移；相对基线、机制组合和收益仍需正文核验。
  - 内存、存储与解耦资源；Disaggregated Memory Systems；disaggregated memory；remote memory

- [Understanding and Optimizing Database Pushdown on Disaggregated Storage](https://doi.org/10.1145/3779212.3790243)
  - Hua Zhang (University of Wisconsin at Madison/Beihang University), Xiao Li (University of Wisconsin at Madison/Beihang University), Yuebin Bai (Beihang University), Ming Liu (University of Wisconsin–Madison)
  - Understanding and Optimizing Database Pushdown 的官方标题与主会议程把研究对象限定为远端内存顺序、事务、页迁移与存储下推中的“Understanding and Optimizing Database Pushdown on Disaggregated Storage”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Understanding and Optimizing Database Pushdown on Disaggregated Storage”作为独立系统问题，而不只是沿用单机一致性假设和全页迁移；相对基线、机制组合和收益仍需正文核验。
  - 内存、存储与解耦资源；Disaggregated Memory Systems；disaggregated memory；remote memory；storage

- [A Framework for Developing and Optimizing Fully Homomorphic Encryption Programs on GPUs](https://doi.org/10.1145/3779212.3790120)
  - Zhuoran Ji (Shandong University), Jianyu Zhao (Shandong University), Guang Fan (Ant Group), Mingzhe Zhang (Ant Research), Shoumeng Yan (Ant Group), Xueyu Wu (The University of Hong Kong), Lei Ju (Shandong University)
  - A Framework for Developing and 的官方标题与主会议程把研究对象限定为GPU/FHE 编程、私有推理与加速器中的“A Framework for Developing and Optimizing Fully Homomorphic Encryption Programs on GPUs”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“A Framework for Developing and Optimizing Fully Homomorphic Encryption Programs on GPUs”作为独立系统问题，而不只是沿用CPU 主导或孤立算子的 FHE 实现；相对基线、机制组合和收益仍需正文核验。
  - 量子、FHE 与新型计算；Fully Homomorphic Encryption；FHE；privacy；GPU

- [HEPIC: Private Inference over Homomorphic Encryption with Client Intervention](https://doi.org/10.1145/3779212.3790170)
  - Kevin Nam (Seoul National University), Youyeon Joo (Seoul National University), Seungjin Ha (Seoul National University), Hyungon Moon (Ulsan National Institute of Science and Technology (UNIST)), Yunheung Paek (Seoul National University)
  - HEPIC 的官方标题与主会议程把研究对象限定为GPU/FHE 编程、私有推理与加速器中的“Private Inference over Homomorphic Encryption with Client Intervention”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Private Inference over Homomorphic Encryption with Client Intervention”作为独立系统问题，而不只是沿用CPU 主导或孤立算子的 FHE 实现；相对基线、机制组合和收益仍需正文核验。
  - 量子、FHE 与新型计算；Fully Homomorphic Encryption；FHE；privacy

- [Falcon: Algorithm-Hardware Co-Design for Efficient Fully Homomorphic Encryption Accelerator](https://doi.org/10.1145/3779212.3790160)
  - Liang Kong (Ant Group), Shengyu Fan (Chinese Academy of Sciences, CAS), Xianglong Deng (Chinese Academy of Sciences, CAS), Lei Chen (Ant Group), Guang Fan (Ant Group), Yilan Zhu (Ant Group), Geng Yang (Ant Group), Yisong Chang (Ant Group), Shoumeng Yan (Ant Group), Mingzhe Zhang (Ant Group)
  - Falcon 的官方标题与主会议程把研究对象限定为GPU/FHE 编程、私有推理与加速器中的“Algorithm-Hardware Co-Design for Efficient Fully Homomorphic Encryption Accelerator”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Algorithm-Hardware Co-Design for Efficient Fully Homomorphic Encryption Accelerator”作为独立系统问题，而不只是沿用CPU 主导或孤立算子的 FHE 实现；相对基线、机制组合和收益仍需正文核验。
  - 量子、FHE 与新型计算；Fully Homomorphic Encryption；FHE；privacy

- [Maverick: Rethinking TFHE Bootstrapping on GPUs via Algorithm-Hardware Co-Design](https://doi.org/10.1145/3779212.3790186)
  - Zhiwei Wang (State Key Laboratory of Cyberspace Security Defense, Institute of Information Engineering, CAS), Haoqi He (State Key Laboratory of Cyberspace Security Defense, Institute of Information Engineering, CAS), Lutan Zhao (State Key Laboratory of Cyberspace Security Defense, Institute of Information Engineering, CAS), Qingyun Niu (State Key Laboratory of Cyberspace Security Defense, Institute of Information Engineering, CAS), Dan Meng (Institute of Information Engineering, CAS), Rui Hou (State Key Laboratory of Cyberspace Security Defense, Institute of Information Engineering, CAS)
  - Maverick 的官方标题与主会议程把研究对象限定为GPU/FHE 编程、私有推理与加速器中的“Rethinking TFHE Bootstrapping on GPUs via Algorithm-Hardware Co-Design”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Rethinking TFHE Bootstrapping on GPUs via Algorithm-Hardware Co-Design”作为独立系统问题，而不只是沿用CPU 主导或孤立算子的 FHE 实现；相对基线、机制组合和收益仍需正文核验。
  - 量子、FHE 与新型计算；Fully Homomorphic Encryption；FHE；privacy；GPU

- [COGENT: Adaptable Compiler Toolchain for Tagging RISC-V Binaries](https://doi.org/10.1145/3676642.3736125)
  - David B Demicco (Binghamton University), Matthew Cole (Binghamton University), Gokturk Yuksek (Binghamton University), RaviTheja Gollapudi (Binghamton University), Aravind Prakash (Binghamton University), Kanad Ghose (Binghamton University), Zerksis D Umrigar (Binghamton University)
  - COGENT 的官方标题与主会议程把研究对象限定为编译工具链、指令复用和 LLM 辅助循环优化中的“Adaptable Compiler Toolchain for Tagging RISC-V Binaries”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Adaptable Compiler Toolchain for Tagging RISC-V Binaries”作为独立系统问题，而不只是沿用纯启发式编译搜索；相对基线、机制组合和收益仍需正文核验。
  - 编译、PL 与处理器微体系结构；Compilers & Code Generation；compiler；code generation；RISC-V

- [Finding Reusable Instructions via E-Graph Anti-Unification](https://doi.org/10.1145/3779212.3790162)
  - Youwei Xiao (Peking University), Chenyun Yin (Peking University), Yitian Sun (Peking University), Yuyang Zou (Peking University), Yun Liang (Peking University)
  - Finding Reusable Instructions via E-Graph 的官方标题与主会议程把研究对象限定为编译工具链、指令复用和 LLM 辅助循环优化中的“Finding Reusable Instructions via E-Graph Anti-Unification”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Finding Reusable Instructions via E-Graph Anti-Unification”作为独立系统问题，而不只是沿用纯启发式编译搜索；相对基线、机制组合和收益仍需正文核验。
  - 编译、PL 与处理器微体系结构；Compilers & Code Generation；compiler；code generation

- [LOOPRAG: Enhancing Loop Transformation Optimization with Retrieval-Augmented Large Language Models](https://doi.org/10.1145/3779212.3790183)
  - Yijie Zhi (Zhejiang University), Yayu Cao (Zhejiang University), Jianhua Dai (Zhejiang Institute of Administration), Xiaoyang Han (Zhejiang University), Jingwen Pu (Zhejiang University), Qingran Wu (zhejiang university), Sheng Cheng (Beijing ShenZhou Aerospace Software Technology Ltd), Ming Cai (zhejiang university)
  - LOOPRAG 先按 loop feature 从合法变换示例中检索兼顾相似性和多样性的 demonstration，再让 LLM 生成优化代码，并把编译、测试和性能结果反馈到下一轮；mutation、coverage 与 differential test 用于等价性检查。
  - 核心创新是把 RAG 与真实 toolchain 的正确性/性能反馈闭合，而非一次性代码生成；因能观察-行动-验证-迭代，归为 Agent for Systems。
  - 编译、PL 与处理器微体系结构；Agent for Systems；loop transformation；RAG；tool feedback

- [Evaluating Compiler Optimization Impacts on zkVM Performance](https://doi.org/10.1145/3779212.3790159)
  - Thomas Gassmann (ETH Zurich), Stefanos Chaliasos (Imperial College London & zkSecurity), Thodoris Sotiropoulos (ETH Zurich), Zhendong Su (ETH Zurich)
  - Evaluating Compiler Optimization Impacts on 的官方标题与主会议程把研究对象限定为编译工具链、指令复用和 LLM 辅助循环优化中的“Evaluating Compiler Optimization Impacts on zkVM Performance”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Evaluating Compiler Optimization Impacts on zkVM Performance”作为独立系统问题，而不只是沿用纯启发式编译搜索；相对基线、机制组合和收益仍需正文核验。
  - 编译、PL 与处理器微体系结构；Compilers & Code Generation；compiler；code generation；KV cache

- [DejaVuzz: Disclosing Transient Execution Bugs with Dynamic Swappable Memory and Differential Information Flow Tracking assisted Processor Fuzzing](https://doi.org/10.1145/3676642.3736115)
  - Jinyan Xu (Zhejiang University), Yangye Zhou (Zhejiang University), Xingzhi Zhang (Zhejiang University), Yinshuai Li (Southern University of Science and Technology), Qinhan Tan (Princeton University), Yinqian Zhang (Southern University of Science and Technology (SUSTech)), Yajin Zhou (Zhejiang University & BlockSec), Rui Chang (Zhejiang University), Wenbo Shen (Zhejiang University)
  - DejaVuzz 面向处理器 transient-execution 漏洞，用 dynamic swappable memory 隔离不同执行流并精确触发短暂窗口，再以 differential information-flow tracking 的 taint/coverage 信号引导输入变异，并用 liveness 检查判断秘密是否泄漏；其覆盖率提高约 4.7 倍并发现 5 个 bug、获得 6 个 CVE。
  - 核心创新是同时提升 transient state 的可控性和 secret flow 的可观测性；相比只比较架构结果或随机扰动的 processor fuzzer，它直接把微结构信息流差异作为搜索反馈。
  - 安全、可靠性、验证与测试；DejaVuzz；transient execution；processor fuzzing；information-flow tracking

- [Signal Breaker: Fuzzing Digital Signal Processors](https://doi.org/10.1145/3779212.3790220)
  - Cameron Garcia (Virginia Tech), Matthew Hicks (Virginia Tech)
  - Signal Breaker 的官方标题与主会议程把研究对象限定为处理器/DSP/数据库模糊测试与静默数据错误中的“Fuzzing Digital Signal Processors”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Fuzzing Digital Signal Processors”作为独立系统问题，而不只是沿用单一输入生成器和离线故障检测；相对基线、机制组合和收益仍需正文核验。
  - 安全、可靠性、验证与测试；Testing & Fuzzing；fuzzing；SDC

- [Scaling Automated Database System Testing](https://doi.org/10.1145/3779212.3790215)
  - Suyang Zhong (National University of Singapore), Manuel Rigger (National University of Singapore)
  - Scaling Automated Database System Testing 的官方标题与主会议程把研究对象限定为处理器/DSP/数据库模糊测试与静默数据错误中的“Scaling Automated Database System Testing”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Scaling Automated Database System Testing”作为独立系统问题，而不只是沿用单一输入生成器和离线故障检测；相对基线、机制组合和收益仍需正文核验。
  - 安全、可靠性、验证与测试；Testing & Fuzzing；fuzzing；SDC

- [SEVI: Silent Data Corruption of Vector Instructions in Hyper-Scale Datacenters](https://doi.org/10.1145/3779212.3790217)
  - Yixuan Mei (Carnegie Mellon University), Shreya Varshini (Meta Platforms, Inc.), Harish Dattatraya Dixit (Meta Platforms, Inc.), Sriram Sankar (Meta Platforms, Inc.), Rashmi Vinayak (Carnegie Mellon University)
  - SEVI 的官方标题与主会议程把研究对象限定为处理器/DSP/数据库模糊测试与静默数据错误中的“Silent Data Corruption of Vector Instructions in Hyper-Scale Datacenters”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Silent Data Corruption of Vector Instructions in Hyper-Scale Datacenters”作为独立系统问题，而不只是沿用单一输入生成器和离线故障检测；相对基线、机制组合和收益仍需正文核验。
  - 安全、可靠性、验证与测试；Testing & Fuzzing；fuzzing；SDC

- [Co-Exploration of RISC-V Processor Microarchitectures and FreeRTOS Extensions for Lower Context Switch Latency](https://doi.org/10.1145/3779212.3790141)
  - Markus Scheck (Technische Universität Darmstadt), Tammo Mürmann (Technische Universität Darmstadt), Andreas Koch (Technische Universität Darmstadt)
  - Co-Exploration of RISC-V Processor Microarchitectures 的官方标题与主会议程把研究对象限定为处理器微结构、上下文切换与弱内存模型中的“Co-Exploration of RISC-V Processor Microarchitectures and FreeRTOS Extensions for Lower Context Switch Latency”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Co-Exploration of RISC-V Processor Microarchitectures and FreeRTOS Extensions for Lower Context Switch Latency”作为独立系统问题，而不只是沿用固定微结构和聚合性能计数；相对基线、机制组合和收益仍需正文核验。
  - 编译、PL 与处理器微体系结构；Processor Microarchitecture；microarchitecture；memory model；RISC-V

- [Chips Need DIP: Time-Proportional Per-Instruction Cycle Stacks at Dispatch](https://doi.org/10.1145/3779212.3790139)
  - Silvio Campelo de Santana (Norwegian University of Science and Technology (NTNU)), Joseph Rogers (Norwegian University of Science and Technology (NTNU)), Lieven Eeckhout (Ghent University), Magnus Jahre (Norwegian University of Science and Technology (NTNU))
  - Chips Need DIP 的官方标题与主会议程把研究对象限定为处理器微结构、上下文切换与弱内存模型中的“Time-Proportional Per-Instruction Cycle Stacks at Dispatch”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Time-Proportional Per-Instruction Cycle Stacks at Dispatch”作为独立系统问题，而不只是沿用固定微结构和聚合性能计数；相对基线、机制组合和收益仍需正文核验。
  - 编译、PL 与处理器微体系结构；Processor Microarchitecture；microarchitecture；memory model

- [Arm Weak Memory Consistency on Apple Silicon: What Is It Good For?](https://doi.org/10.1145/3779212.3790129)
  - Yossi Khayet (Tel Aviv University), Adam Morrison (Tel Aviv University)
  - Arm Weak Memory Consistency on Apple Silicon 的官方标题与主会议程把研究对象限定为处理器微结构、上下文切换与弱内存模型中的“What Is It Good For?”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“What Is It Good For?”作为独立系统问题，而不只是沿用固定微结构和聚合性能计数；相对基线、机制组合和收益仍需正文核验。
  - 编译、PL 与处理器微体系结构；Processor Microarchitecture；microarchitecture；memory model

- [A Data-Driven Dynamic Execution Orchestration Architecture](https://doi.org/10.1145/3760250.3762226)
  - Zhenyu Bai (National University of Singapore), Pranav Dangi (National University Of Singapore), Rohan Juneja (National University of Singapore), Zhaoying Li (National University of Singapore), Zhanglu Yan (National university of Singapore), Huiying Lan (Lumai Ltd.), Tulika Mitra (National University of Singapore)
  - Canon 以可编程 FSM 在编译期编码高层 dataflow，并在运行时把 sparse coordinate 等数据 metadata 翻译为控制动作；time-lapsed SIMD 让不同数据项错开发射，随数据稀疏性动态演化执行流，而无需为每种 workload 固化 datapath。
  - 核心创新是把数据驱动控制拆为可编程 metadata-to-control 层，使同一架构在运行时编排动态 dataflow；相较固定专用加速器或通用核，在效率和可编程性之间增加新的系统点。
  - 编译、PL 与处理器微体系结构；Canon；dynamic dataflow；programmable FSM；time-lapsed SIMD

- [cuJSON: A Highly Parallel JSON Parser for GPUs](https://doi.org/10.1145/3760250.3762222)
  - Ashkan Vedadi Gargary (University of California, Riverside), Soroosh Safari Loaliyan (University of California, Riverside), Zhijia Zhao (University of California, Riverside)
  - cuJSON 的官方标题与主会议程把研究对象限定为GPU 编程、能力安全、神经符号与 FHE中的“A Highly Parallel JSON Parser for GPUs”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“A Highly Parallel JSON Parser for GPUs”作为独立系统问题，而不只是沿用CPU 实现或不暴露 GPU 专用机制的框架；相对基线、机制组合和收益仍需正文核验。
  - ML 系统、GPU 与加速器；GPU Programming；GPU programming；runtime；GPU

- [CHERI-SIMT: Implementing Capability Memory Protection in GPGPUs](https://doi.org/10.1145/3760250.3762234)
  - Matthew Naylor (University of Cambridge), Alexandre Joannou (University of Cambridge), A. Theodore Markettos (University of Cambridge), Paul Metzger (University of Cambridge), Simon Moore (University of Cambridge), Timothy M. Jones (University of Cambridge)
  - CHERI-SIMT 的官方标题与主会议程把研究对象限定为GPU 编程、能力安全、神经符号与 FHE中的“Implementing Capability Memory Protection in GPGPUs”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Implementing Capability Memory Protection in GPGPUs”作为独立系统问题，而不只是沿用CPU 实现或不暴露 GPU 专用机制的框架；相对基线、机制组合和收益仍需正文核验。
  - ML 系统、GPU 与加速器；GPU Programming；GPU programming；runtime；GPU

- [Lobster: A GPU-Accelerated Framework for Neurosymbolic Programming](https://doi.org/10.1145/3760250.3762232)
  - Paul Biberstein (University of Pennsylvania), Ziyang Li (University of Pennsylvania), Joseph Devietti (University of Pennsylvania), Mayur Naik (University of Pennsylvania)
  - Lobster 将类 Datalog 的神经符号程序编译到 APM 中间表示，以 provenance semiring 统一离散、概率与可微推理，并通过专门 pass 把包括 symbolic join/fixpoint 在内的端到端执行映射到 GPU；在 NLP、图像、程序分析、生物和规划任务上相对 Scallop 最高约 3.9 倍。
  - 核心创新是让符号推理部分也成为 GPU 编译对象，而不是只在 GPU 跑 neural operator、把规则求值留给 CPU，从而统一多种 reasoning semantics 和异构执行。
  - ML 系统、GPU 与加速器；Lobster；neurosymbolic programming；Datalog；GPU compiler；GPU

- [ReliaFHE: Resilient Design for Fully Homomorphic Encryption Accelerators](https://doi.org/10.1145/3779212.3790211)
  - Fan Li (University of Central Florida), Mayank Kumar (University of Central Florida), Ruizhi Zhu (University of Central Florida), Mengxin Zheng (University of Central Florida), Qian Lou (University of Central Florida), Xin Xin (University of Central Florida)
  - ReliaFHE 的官方标题与主会议程把研究对象限定为GPU 编程、能力安全、神经符号与 FHE中的“Resilient Design for Fully Homomorphic Encryption Accelerators”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Resilient Design for Fully Homomorphic Encryption Accelerators”作为独立系统问题，而不只是沿用CPU 实现或不暴露 GPU 专用机制的框架；相对基线、机制组合和收益仍需正文核验。
  - ML 系统、GPU 与加速器；GPU Programming；GPU programming；runtime；FHE

- [Lambda-trim: Reducing Monetary and Performance Cost of Serverless Cold Starts with Cost-driven Application Debloating](https://doi.org/10.1145/3676642.3736129)
  - Spyros Pavlatos (University of Pennsylvania), Xuting Liu (University of Pennsylvania), Yuhao Liu (University of Pennsylvania), Vincent Liu (University of Pennsylvania)
  - Lambda-trim 的官方标题与主会议程把研究对象限定为serverless 冷启动、成本分析和云网络虚拟化中的“Reducing Monetary and Performance Cost of Serverless Cold Starts with Cost-driven Application Debloating”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Reducing Monetary and Performance Cost of Serverless Cold Starts with Cost-driven Application Debloating”作为独立系统问题，而不只是沿用整包加载和粗粒度网络虚拟化；相对基线、机制组合和收益仍需正文核验。
  - 云、网络与 Serverless；Serverless & Cloud Networking；serverless；cloud networking

- [Skyler: Static Analysis for Predicting API-Driven Costs in Serverless Applications](https://doi.org/10.1145/3779212.3790221)
  - Bernardo Ribeiro (INESC-ID, Instituto Superior Técnico, University of Lisbon), Mafalda Ferreira (INESC-ID, Instituto Superior Técnico, University of Lisbon), José Fragoso Santos (INESC-ID, Instituto Superior Técnico, University of Lisbon), Rodrigo Bruno (INESC-ID, Instituto Superior Técnico, University of Lisbon), Nuno Santos (INESC-ID, Instituto Superior Técnico, University of Lisbon)
  - Skyler 的官方标题与主会议程把研究对象限定为serverless 冷启动、成本分析和云网络虚拟化中的“Static Analysis for Predicting API-Driven Costs in Serverless Applications”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Static Analysis for Predicting API-Driven Costs in Serverless Applications”作为独立系统问题，而不只是沿用整包加载和粗粒度网络虚拟化；相对基线、机制组合和收益仍需正文核验。
  - 云、网络与 Serverless；Serverless & Cloud Networking；serverless；cloud networking

- [Enabling fast networking in the public cloud](https://doi.org/10.1145/3779212.3790158)
  - Alireza Sanaee (University of Cambridge & Huawei), Vahab Jabrayilov (Columbia University), Ilias Marinos (NVIDIA), Farbod Shahinfar (Politecnico di Milano), Divyanshu Saxena (The University of Texas at Austin), Kostis Kaffes (Columbia University), Gianni Antichi (Politecnico di Milano & Queen Mary University of London)
  - Enabling fast networking in the 的官方标题与主会议程把研究对象限定为serverless 冷启动、成本分析和云网络虚拟化中的“Enabling fast networking in the public cloud”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Enabling fast networking in the public cloud”作为独立系统问题，而不只是沿用整包加载和粗粒度网络虚拟化；相对基线、机制组合和收益仍需正文核验。
  - 云、网络与 Serverless；Serverless & Cloud Networking；serverless；cloud networking

- [SG-IOV: Socket-Granular I/O Virtualization for SmartNIC-Based Container Networks](https://doi.org/10.1145/3779212.3790218)
  - Chenxingyu Zhao (University of Washington), Hongtao Zhang (University of Washington), Jaehong Min (University of Washington), Shengkai Lin (Shanghai Jiao Tong University), Wei Zhang (University of Connecticut), Kaiyuan Zhang (University of Washington), Ming Liu (University of Wisconsin–Madison), Arvind Krishnamurthy (University of Washington)
  - SG-IOV 的官方标题与主会议程把研究对象限定为serverless 冷启动、成本分析和云网络虚拟化中的“Socket-Granular I/O Virtualization for SmartNIC-Based Container Networks”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Socket-Granular I/O Virtualization for SmartNIC-Based Container Networks”作为独立系统问题，而不只是沿用整包加载和粗粒度网络虚拟化；相对基线、机制组合和收益仍需正文核验。
  - 云、网络与 Serverless；Serverless & Cloud Networking；serverless；cloud networking；SmartNIC

- [PACT: A Criticality-First Design for Tiered Memory](https://doi.org/10.1145/3779212.3790198)
  - Hamid Hadian (Virginia Tech), Jinshu Liu (Virginia Tech), Hanchen Xu (Virginia Tech), Hansen Idden (Virginia Tech), Huaicheng Li (Virginia Tech)
  - PACT 的官方标题与主会议程把研究对象限定为分层内存、性能可预测性与硬件预取中的“A Criticality-First Design for Tiered Memory”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“A Criticality-First Design for Tiered Memory”作为独立系统问题，而不只是沿用只依赖运行时局部历史的内存策略；相对基线、机制组合和收益仍需正文核验。
  - 内存、存储与解耦资源；Memory Hierarchy & Performance；memory hierarchy；prefetching

- [CounterPoint: Using Hardware Event Counters to Refute and Refine Microarchitectural Assumptions](https://doi.org/10.1145/3779212.3790145)
  - Nick Lindsay (Yale University), Caroline Trippel (Stanford University), Anurag Khandelwal (Yale University), Abhishek Bhattacharjee (Yale University)
  - CounterPoint 的官方标题与主会议程把研究对象限定为分层内存、性能可预测性与硬件预取中的“Using Hardware Event Counters to Refute and Refine Microarchitectural Assumptions”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Using Hardware Event Counters to Refute and Refine Microarchitectural Assumptions”作为独立系统问题，而不只是沿用只依赖运行时局部历史的内存策略；相对基线、机制组合和收益仍需正文核验。
  - 内存、存储与解耦资源；Memory Hierarchy & Performance；memory hierarchy；prefetching

- [Performance Predictability in Heterogeneous Memory](https://doi.org/10.1145/3779212.3790201)
  - Jinshu Liu (Virginia Tech), Hanchen Xu (Virginia Tech), Daniel S. Berger (Microsoft and University of Washington and CMU), Marcos K. Aguilera (NVIDIA), Huaicheng Li (Virginia Tech)
  - Performance Predictability in Heterogeneous Memory 的官方标题与主会议程把研究对象限定为分层内存、性能可预测性与硬件预取中的“Performance Predictability in Heterogeneous Memory”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Performance Predictability in Heterogeneous Memory”作为独立系统问题，而不只是沿用只依赖运行时局部历史的内存策略；相对基线、机制组合和收益仍需正文核验。
  - 内存、存储与解耦资源；Memory Hierarchy & Performance；memory hierarchy；prefetching

- [PF-LLM: Large Language Model Hinted Hardware Prefetching](https://doi.org/10.1145/3779212.3790202)
  - Ceyu Xu (The Hong Kong University of Science and Technology), Xiangfeng Sun (The Hong Kong University of Science and Technology), Weihang Li (Duke University), Chen Bai (The Hong Kong University of Science and Technology), Bangyan Wang (The Hong Kong University of Science and Technology), Mengming Li (The Hong Kong University of Science and Technology), Zhiyao Xie (The Hong Kong University of Science and Technology), Yuan Xie (The Hong Kong University of Science and Technology)
  - PF-LLM 把“何时、如何以及多激进地预取”的复杂决策从面积受限的在线硬件移到离线 LLM 程序分析，再把生成的提示交给轻量 on-chip prefetcher 执行；LLM 使用更广的程序上下文，硬件仍负责低开销运行时动作。
  - 核心创新是离线 LLM 与在线硬件预取器分工，而非用大模型进入关键路径；它没有自主工具反馈循环，归为 LLM for Systems。
  - 内存、存储与解耦资源；LLM for Systems；hardware prefetching；offline analysis；LLM

- [Neura: A Unified Framework for Hierarchical and Adaptive CGRAs](https://doi.org/10.1145/3779212.3790193)
  - Cheng Tan (Google/ASU), Miaomiao Jiang (Shandong University), Yuqi Sun, Ruihong Yin (University of Minnesota Twin Cities), Yanghui Ou (Cornell University), Qing Zhong (Google), Lei Ju (Shandong University), Jeff Zhang (Arizona State University)
  - Neura 的官方标题与主会议程把研究对象限定为CGRA、可重构互连、配置开销与流式 tokenization中的“A Unified Framework for Hierarchical and Adaptive CGRAs”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“A Unified Framework for Hierarchical and Adaptive CGRAs”作为独立系统问题，而不只是沿用静态映射和忽略配置成本的加速器；相对基线、机制组合和收益仍需正文核验。
  - ML 系统、GPU 与加速器；Reconfigurable Architectures；reconfigurable architecture；CGRA

- [Transforming Torus Fabrics for Efficient Multi-tenant ML](https://doi.org/10.1145/3779212.3790238)
  - Abhishek Vijaya Kumar (Cornell University), Eric Ding (Cornell University), Arjun Devraj (Cornell University), Darius Bunandar (Lightmatter), Rachee Singh (Cornell)
  - Transforming Torus Fabrics for Efficient 的官方标题与主会议程把研究对象限定为CGRA、可重构互连、配置开销与流式 tokenization中的“Transforming Torus Fabrics for Efficient Multi-tenant ML”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Transforming Torus Fabrics for Efficient Multi-tenant ML”作为独立系统问题，而不只是沿用静态映射和忽略配置成本的加速器；相对基线、机制组合和收益仍需正文核验。
  - ML 系统、GPU 与加速器；Reconfigurable Architectures；reconfigurable architecture；CGRA

- [The Configuration Wall: Characterization and Elimination of Accelerator Configuration Overhead](https://doi.org/10.1145/3760250.3762225)
  - Josse Van Delm (KU Leuven), Anton Lydike (The University of Edinburgh), Joren Dumoulin (KU Leuven), Jonas Crols (KU Leuven), Xiaoling Yi (KU Leuven), Ryan Antonio (KU Leuven), Jackson Woodruff (The University of Edinburgh), Tobias Grosser (University of Cambridge), Marian Verhelst (KU Leuven)
  - 该工作用扩展 roofline 模型判断系统何时从 compute/memory-bound 转为 configuration-bound，再在 MLIR 中加入专用 abstraction 和 pass，消除冗余配置周期并隐藏剩余 setup。
  - 核心创新是把加速器配置开销从零散工程问题提升为可量化瓶颈区间，并给出可移植的编译消除机制。
  - ML 系统、GPU 与加速器；configuration wall；MLIR

- [Static Analysis for Efficient Streaming Tokenization](https://doi.org/10.1145/3779212.3790227)
  - Angela W. Li (Rice University), Yudi Yang (Rice University), Konstantinos Mamouras (Rice University)
  - Static Analysis for Efficient Streaming 的官方标题与主会议程把研究对象限定为CGRA、可重构互连、配置开销与流式 tokenization中的“Static Analysis for Efficient Streaming Tokenization”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Static Analysis for Efficient Streaming Tokenization”作为独立系统问题，而不只是沿用静态映射和忽略配置成本的加速器；相对基线、机制组合和收益仍需正文核验。
  - ML 系统、GPU 与加速器；Reconfigurable Architectures；reconfigurable architecture；CGRA

- [Arancini: A Hybrid Binary Translator for Weak Memory Model Architectures](https://doi.org/10.1145/3779212.3790127)
  - Sebastian Reimers (Technical University of Munich (TUM)), Dennis Sprokholt (TU Delft), Martin Fink (TU Munich), Theofilos Augoustis (Technical University of Munich (TUM)), Simon Kammermeier (Technical University of Munich), Rodrigo C. O. Rocha (Huawei), Tom Spink (University of St Andrews, United Kingdom), Redha Gouicem (RWTH Aachen University), Soham Chakraborty (TU Delft), Pramod Bhatotia (TU Munich)
  - Arancini 的官方标题与主会议程把研究对象限定为系统 profile、二进制翻译、低比特格式与 GPU FHE中的“A Hybrid Binary Translator for Weak Memory Model Architectures”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“A Hybrid Binary Translator for Weak Memory Model Architectures”作为独立系统问题，而不只是沿用离线单点 profile 或通用数值格式；相对基线、机制组合和收益仍需正文核验。
  - ML 系统、GPU 与加速器；Systems Profiling & Optimization；profiling；quantization

- [Wax: Optimizing Data Center Applications With Stale Profile](https://doi.org/10.1145/3779212.3790248)
  - Tawhid Bhuiyan (Columbia University in the City of New York), Sumya Hoque (Columbia University in the City of New York), Angelica Moreira (Microsoft Research), Tanvir Ahmed Khan (Columbia University in the City of New York)
  - Wax 的官方标题与主会议程把研究对象限定为系统 profile、二进制翻译、低比特格式与 GPU FHE中的“Optimizing Data Center Applications With Stale Profile”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Optimizing Data Center Applications With Stale Profile”作为独立系统问题，而不只是沿用离线单点 profile 或通用数值格式；相对基线、机制组合和收益仍需正文核验。
  - ML 系统、GPU 与加速器；Systems Profiling & Optimization；profiling；quantization

- [M2XFP: A Metadata-Augmented Microscaling Data Format for Efficient Low-bit Quantization](https://doi.org/10.1145/3779212.3790185)
  - Weiming Hu (Shanghai Jiao Tong University), Zihan Zhang (Shanghai Jiao Tong University), Haoyan Zhang (Shanghai Jiao Tong University), Chen Zhang (Shanghai Jiao Tong University), Cong Guo (Shanghai Jiao Tong University), Yu Feng (Shanghai Jiao Tong University), Tianchi Hu (Computing Product Line, Huawei), Guanglin Li (Computing Product Line, Huawei), Guipeng Hu (Computing Product Line, Huawei), Junsong Wang (Computing Product Line, Huawei), Jingwen Leng (Shanghai Jiao Tong University)
  - M2XFP 在共享 power-of-two scale 的 microscaling 低比特格式上增加少量可编码 metadata，配套在线量化单元和加速器数据通路，以恢复 MXFP4/NVFP4 在多种 LLM 上丢失的精度。
  - 核心创新是用极少 metadata 调整 group 内数值表达并与硬件共同设计，在位效率、量化质量和执行开销间取得新折中。
  - ML 系统、GPU 与加速器；microscaling；low-bit quantization；algorithm-hardware co-design

- [Cheddar: A Swift Fully Homomorphic Encryption Library Designed for GPU Architectures](https://doi.org/10.1145/3760250.3762223)
  - Wonseok Choi (Seoul National University), Jongmin Kim (Seoul National University), Jung Ho Ahn (Seoul National University)
  - Cheddar 面向 GPU 上的 FHE 运算，围绕 32-bit integer datapath 设计底层多项式/模运算 kernel，并通过运算序列重排与 kernel fusion 降低全局内存流量；在端到端同态 workload 上比既有 GPU FHE 库快约 2.18–4.45 倍。
  - 核心创新不是孤立优化某个 NTT，而是让数值表示、完整操作序列和 GPU kernel 数据通路共同适配 32-bit 硬件，系统性减少宽整数与中间结果搬运。
  - ML 系统、GPU 与加速器；Cheddar；FHE library；GPU integer datapath；kernel fusion；GPU

- [COMPAS: A Distributed Multi-Party SWAP Test for Parallel Quantum Algorithms](https://doi.org/10.1145/3779212.3790143)
  - Brayden Goldstein-Gelb (Brown University), Kun Liu (Yale University), John M. Martyn (Massachusetts Institute of Technology), Hengyun (Harry) Zhou (QuEra Computing Inc.), Yongshan Ding (Yale University), Yuan Liu (North Carolina State University)
  - COMPAS 在多个模块化 QPU 之间执行 multi-party SWAP / multivariate trace estimation：各节点预共享 Bell pair，以常数额外电路深度比较并行量子状态，所需 Bell pair 随寄存器宽度线性增长；设计同时评估网络噪声以及 circuit depth、GHZ width 的渐近代价。
  - 核心创新是把 SWAP-test 原语改写为适合分布式 QPU 网络的协议，使跨节点状态比较无需把量子数据汇聚到单机，并把通信资源和物理网络误差纳入算法设计。
  - 量子、FHE 与新型计算；COMPAS；distributed quantum；SWAP test；Bell pair；量子计算

- [TreeVQA: A Tree-Structured Execution Framework for Shot Reduction in Variational Quantum Algorithms](https://doi.org/10.1145/3779212.3790239)
  - Yuewen Hou (University of Michigan), Dhanvi Bharadwaj (University of Michigan), Gokul Ravi (University of Michigan)
  - TreeVQA 把多个结构相近的 VQA 任务组织成共享执行树：相同电路前缀只采样一次，只有当参数化执行路径真正分歧时才分叉，并以框架 wrapper 对现有 VQA 透明复用 shots；平均减少约 25.9 倍采样，在大规模任务上超过 100 倍。
  - 核心创新是跨 VQA 任务复用尚未分歧的量子执行，而不是对每个参数点独立运行或仅在单电路内优化 shot allocation，把任务间结构相似性直接转化为采样节省。
  - 量子、FHE 与新型计算；TreeVQA；variational quantum algorithm；shot reduction；execution tree；量子计算

- [CHEHAB RL: Learning to Optimize Fully Homomorphic Encryption Computations](https://doi.org/10.1145/3779212.3790138)
  - Bilel Sefsaf (New York University Abu Dhabi and Ecole Superieure d'Informatique), Abderraouf Dandani (New York University Abu Dhabi and Ecole Superieure d'Informatique), Abdessamed Seddiki (New York University Abu Dhabi and Ecole Superieure d'Informatique), Arab Mohammed (New York University Abu Dhabi and Ecole Superieure d'Informatique), Eduardo Chielle (New York University Abu Dhabi), Mihalis Maniatakos (New York University Abu Dhabi), Riyadh Baghdadi (New York University Abu Dhabi)
  - CHEHAB RL 的官方标题与主会议程把研究对象限定为量子执行、FHE 优化与计算存储仿真中的“Learning to Optimize Fully Homomorphic Encryption Computations”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Learning to Optimize Fully Homomorphic Encryption Computations”作为独立系统问题，而不只是沿用单节点量子执行或受物理设备规模限制的仿真；相对基线、机制组合和收益仍需正文核验。
  - 量子、FHE 与新型计算；Quantum & Emerging Computing；quantum；computational storage

- [CEMU: Enabling Full-System Emulation of Computational Storage beyond Hardware Limits](https://doi.org/10.1145/3779212.3790137)
  - Qiuyang Zhang (Huazhong University of Science and Technology), Jiapin Wang (Huazhong University of Science and Technology), You Zhou (Huazhong University of Science and Technology), Peng Xu (Research Center for High Efficiency Computing Infrastructure, Zhejiang Lab), Kai Lu (Huazhong University of Science and Technology), Jiguang Wan (Huazhong University of Science and Technology), Fei Wu (Huazhong University of Science and Technology), Tao Lu (DapuStor)
  - CEMU 的官方标题与主会议程把研究对象限定为量子执行、FHE 优化与计算存储仿真中的“Enabling Full-System Emulation of Computational Storage beyond Hardware Limits”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Enabling Full-System Emulation of Computational Storage beyond Hardware Limits”作为独立系统问题，而不只是沿用单节点量子执行或受物理设备规模限制的仿真；相对基线、机制组合和收益仍需正文核验。
  - 量子、FHE 与新型计算；Quantum & Emerging Computing；quantum；computational storage；storage

- [Fault Escaping: Improving Robustness of DPU Enhanced Platform with Mutual Assisted VM Recovery](https://doi.org/10.1145/3676642.3736124)
  - Chao Zhang (Alibaba Group), Tao Xu (Alibaba Group), Junming Liu (Alibaba Group), Pai Liu (Alibaba Group), Zhilang Xu (Alibaba Group), Kang Yan (Alibaba Group), Shuo Shi (Shanghai Jiao Tong University), Jintao Li (Alibaba Group), Jinhu Li (Alibaba Group), Chen Liang (Alibaba Cloud), Wenhui kevin (Intel Corporation), FeiFei Fan (Intel Corporation), Yibin Shen (Alibaba Cloud), Hang Yang (Alibaba Cloud), Jianming Song (Alibaba Group), Xudong Zheng (Alibaba Group), Jiesheng Wu (Alibaba Group), Jian Li (Shanghai Jiao Tong University)
  - Fault Escaping 的官方标题与主会议程把研究对象限定为平台容错、辐射防护与边缘 AI 故障注入中的“Improving Robustness of DPU Enhanced Platform with Mutual Assisted VM Recovery”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Improving Robustness of DPU Enhanced Platform with Mutual Assisted VM Recovery”作为独立系统问题，而不只是沿用均匀故障模型和单层恢复；相对基线、机制组合和收益仍需正文核验。
  - 安全、可靠性、验证与测试；Reliability & Fault Tolerance；fault tolerance；reliability

- [Radshield: Software Radiation Protection for Commodity Hardware in Space](https://doi.org/10.1145/3760250.3762218)
  - Haoda Wang (Columbia University), Yonatan Winetraub (Aptos Orbital), Steven Myint (Jet Propulsion Laboratory, California Institute of Technology), Vandi Verma (Jet Propulsion Laboratory, California Institute of Technology), Junfeng Yang (Columbia University), Asaf Cidon (Columbia University)
  - Radshield 的官方标题与主会议程把研究对象限定为平台容错、辐射防护与边缘 AI 故障注入中的“Software Radiation Protection for Commodity Hardware in Space”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“Software Radiation Protection for Commodity Hardware in Space”作为独立系统问题，而不只是沿用均匀故障模型和单层恢复；相对基线、机制组合和收益仍需正文核验。
  - 安全、可靠性、验证与测试；Reliability & Fault Tolerance；fault tolerance；reliability

- [TierX: A Simulation Framework for Multi-tier BCI System Design Evaluation and Exploration](https://doi.org/10.1145/3779212.3790234)
  - Seunghyun Song (Seoul National University), Yeongwoo Jang (Seoul National University), Daye Jung (Seoul National University), Kyungsoo Park (Seoul National University), Donghan Kim (Seoul National University), Gwangjin Kim (Seoul National University), Hunjun Lee (Hanyang University), Jerald Yoo (Seoul National University), Jangwoo Kim (Seoul National University / MangoBoost)
  - TierX 是多层 brain-computer interface 的系统级模拟与设计空间探索框架；输入可配置 BCI workload、处理节点、电极数量与层间参数，搜索计算位置、通信、供电和节点放置的组合，并输出延迟、功耗等端到端权衡，而不是研究故障注入。
  - 核心创新是把植入端、可穿戴/边缘端等多层 BCI 的计算、通信和供能选择放进同一可搜索模型，使研究者能比较跨层设计，而非只模拟单个神经处理器或无线链路。
  - ML 系统、GPU 与加速器；TierX；brain-computer interface；multi-tier system；design-space exploration

- [PrioriFI: More Informed Fault Injection for Edge Neural Networks](https://doi.org/10.1145/3779212.3790204)
  - Olivia Weng (UC San Diego), Andres Meza (UC San Diego), Nhan Tran (Fermilab), Ryan Kastner (UC San Diego)
  - PrioriFI 的官方标题与主会议程把研究对象限定为平台容错、辐射防护与边缘 AI 故障注入中的“More Informed Fault Injection for Edge Neural Networks”。当前未检索到可核验的公开摘要或正文，因此不能确认其输入粒度、运行时状态、具体算法和量化结果。
  - 标题可确认的差异是把“More Informed Fault Injection for Edge Neural Networks”作为独立系统问题，而不只是沿用均匀故障模型和单层恢复；相对基线、机制组合和收益仍需正文核验。
  - 安全、可靠性、验证与测试；Reliability & Fault Tolerance；fault tolerance；reliability

- [TiNA: Tiered Network Buffer Architecture for Fast Networking in Chiplet-based CPU](https://doi.org/10.1145/3760250.3762224)
  - Siddharth Agarwal (UIUC), Tianchen Wang (UIUC), Jinghan Huang (UIUC), Saksham Agarwal (UIUC), Nan Sung Kim (UIUC)
  - TiNA 面向 chiplet CPU 上对内存延迟敏感的微秒级网络 I/O：平时以 Sub-NUMA Clustering 把收包与处理限制在本地 chiplet，检测到长 packet burst 时才由增强 NIC 与网络栈借用其他 chiplet 的 LLC slice 做 Direct Cache Access；相对 SNC 和 non-SNC，平均分别降低 25%/18% 与 28%/22% 的均值/尾延迟。
  - 核心创新是把 packet buffer 的 DCA 位置做成随 burst 动态切换的 LLC tier，而非固定选择低本地延迟的 SNC 或大共享 LLC 的 non-SNC，从而同时覆盖短流和突发流量。
  - 云、网络与 Serverless；TiNA；chiplet CPU；Sub-NUMA Clustering；Direct Cache Access；network buffer

- [An MLIR Lowering Pipeline for Stencils at Wafer-Scale](https://doi.org/10.1145/3779212.3790124)
  - Nicolai Stawinoga (Technische Universität Berlin), David Katz (University of Edinburgh), Anton Lydike (University of Edinburgh), Justs Zarins (University of Edinburgh), Nick Brown (University of Edinburgh), George Bisbas (Imperial College London), Tobias Grosser (University of Cambridge)
  - 该编译流水线把保持 stencil 领域语义的 MLIR 程序自动 lower 为 Cerebras WSE 异步执行模型下的优化 CSL，无需应用开发者手写消息传递；5 个 stencil benchmark 在 WSE-2/3 上接近手工代码，WSE-3 对 128 张 A100 和 128 个 CPU 节点分别约快 14 倍、20 倍。
  - 核心创新是用多级 MLIR lowering 把规则网格的高层依赖转成 wafer-scale 的分布式异步通信与布局，弥合顺序 stencil 表达和专用超大芯片编程模型之间的鸿沟。
  - 编译、PL 与处理器微体系结构；MLIR；stencil compiler；Cerebras WSE；wafer-scale

- [JOSer: Just-In-Time Object Serialization for Heavy Java Serialization Workloads](https://doi.org/10.1145/3779212.3790179)
  - Chaokun Yang (Ant Group), Pengbo Nie (Shanghai Jiao Tong University), Ziyi Lin (Alibaba Group), Weipeng Wang (Ant Group), Qianwei Yu (Shanghai Jiao Tong University), Chengcheng Wan (East China Normal University), He Jiang (Dalian University of Technology), Yuting Chen (Shanghai Jiao Tong University)
  - JOSer 的官方标题把对象限定为大量 Java object serialization/deserialization，并明确采用 just-in-time 路径；目前未检索到可核验公开摘要或正文，因此不能确认它在 JVM 中专门化的是 schema、对象图遍历、反射调用还是生成代码，也不报告未公开性能数字。
  - 可确认的创新边界是把 serialization path 的运行时专门化作为独立系统机制，目标是摆脱通用反射或人工编写 serializer 的代价；具体 profiling 信号、缓存策略与回退机制需正文核验。
  - 编译、PL 与处理器微体系结构；JOSer；JVM runtime；object serialization；just-in-time specialization

- [Wave: Offloading Resource Management to SmartNIC Cores](https://doi.org/10.1145/3676642.3736113)
  - Jack Tigar Humphries (Stellar Development Foundation), Neel Natu (Google, Inc.), Kostis Kaffes (Columbia University), Stanko Novaković (Google, Inc.), Paul Turner (Google, Inc.), Henry M. Levy (Google, Inc. and University of Washington), David Culler (Google, Inc. and University of California, Berkeley), Christos Kozyrakis (Stanford University)
  - Wave 把用户态调度、内存管理和 RPC 等系统软件决策卸载到 SmartNIC 的 Arm 核心，由新的 host–SmartNIC API 在微秒级接收主机事件并返回资源动作；这些普通 Linux 进程在不占用 host core 的情况下执行控制逻辑，并非 AI Agent。
  - 核心创新是把 SmartNIC 从数据面 offload 扩展为系统资源管理的控制执行端，并提供低延迟通用 API；相较固定 NIC firmware 或主机常驻管理线程，它允许现有用户态策略迁移且及时介入主机运行。
  - 云、网络与 Serverless；Wave；SmartNIC；resource management offload；非 AI Agent

## 互斥方向统计

| 方向 | 论文数 | 占比 |
| --- | ---: | ---: |
| ML 系统、GPU 与加速器 | 53 | 31.5% |
| LLM 与生成式 AI 系统 | 35 | 20.8% |
| 安全、可靠性、验证与测试 | 22 | 13.1% |
| 内存、存储与解耦资源 | 19 | 11.3% |
| 量子、FHE 与新型计算 | 18 | 10.7% |
| 编译、PL 与处理器微体系结构 | 15 | 8.9% |
| 云、网络与 Serverless | 6 | 3.6% |
| 合计 | 168 | 100.0% |

## Agent 四分类

- Agent System：0 篇。没有论文以修改完整的规划—行动—反馈—迭代机制为中心贡献。
- Agent Infra：2 篇。FastTTS 是边缘 Agent 的 reasoning/TTS serving 层；CREATE 是具身 Agent 的跨层可靠执行基础设施。二者都不等于改造 Agent 规划算法。
- Agent for Systems：2 篇。LPO 用 LLM 提议、形式验证和反馈迭代发现编译优化；LOOPRAG 用检索、编译、测试和性能反馈闭环优化循环。
- LLM for Systems：3 篇。Once4All 合成可复用 SMT fuzzing 生成器，CacheMind 做 trace-grounded cache 分析，PF-LLM 离线生成硬件预取提示；它们使用 LLM 解决系统问题，但没有完整自主行动闭环。
- 另有 1 篇 Compound AI System 表征工作 Compositional AI Beyond LLMs；它研究神经—符号—概率组合体系及其系统瓶颈，与 agentic workload 相关，但证据不足以归入上述四类。
- Taming the Long-Tail、HistoRL 和 CHEHAB RL 等传统强化学习/优化论文不计为 Agent。

## 年度方向观察

- AI/ML 系统与加速器相关方向合计 88/168（52.4%）：其中 LLM 与生成式 AI 系统 35 篇，其他 ML/GPU/专用加速器 53 篇，说明 ASPLOS 2026 的主轴已经是模型、runtime、编译器、存储层次与硬件的跨层协同，而不是孤立的新算子。
- 35 篇 LLM/生成式 AI 论文形成完整系统栈：在线 serving 吞吐与延迟 10 篇，训练系统、推测解码、attention/KV cache、MoE/高效推理、生成模型 serving 各 5 篇。热点集中在阶段复用、动态负载调度、KV 数据移动、专家布局和异构资源，而非提出新基础模型。
- 内存、存储与解耦资源另有 19 篇（11.3%），CXL 已从“扩容或慢速 NUMA”推进到共享/持久性语义、资源分配、桥接与安全检查；cache、远端内存和 near-data processing 也普遍联合优化数据布局与运行时状态。
- 安全/验证/可靠性 22 篇（13.1%），量子/FHE/新型计算 18 篇（10.7%），编译/PL/处理器 15 篇（8.9%）。这三组显示 ASPLOS 仍保持体系结构—语言—系统的宽口径：形式方法、类型系统、fuzzing、QEC 与隐私计算并非 AI 主题的附属项。
- 与 Agent 直接相关的四分类只有 7/168（4.2%），且 Agent System 为 0；主要是 Agent Infra、Agent for Systems 和 LLM for Systems。另有 1 篇 compound AI 表征工作。传统 RL 或标题中的 software agent/process 不计入 Agent，避免把“用了智能方法”误判为规划—行动—反馈系统。
- 高频方法论是运行时自适应与硬软协同：系统根据 SLO、队列、token/KV、专家负载、稀疏元数据或故障反馈动态做分配/路由/精度/布局选择，再用专用 kernel、DSL/IR 或硬件接口把决策落地。
