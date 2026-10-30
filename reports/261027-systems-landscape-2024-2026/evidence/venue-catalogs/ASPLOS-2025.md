# ASPLOS 2025 论文列表

ASPLOS 2025 官方主会议程共包含 184 篇唯一正式论文（跨 Volume 1–3 的三个 DOI 前缀）；已排除 keynote、workshop、poster 与 WACI。标题链接指向 DOI 官方文章页；已找到的 76 份合法公开 PDF 保存在 `reference/ASPLOS/2025/`。

- [Mosaic: Exploiting Instruction-Level Parallelism on Deep Learning Accelerators with iTex Tessellation](https://doi.org/10.1145/3676641.3716262)
  - Jianxing Xu (University of Science and Technology of China,SKL of Processors, Institute of Computing Technology, Chinese Academy of Sciences), Yuanbo Wen (SKL of Processors, Institute of Computing Technology, Chinese Academy of Sciences), Zikang Liu (SKL of Processors, Institute of Computing Technology, Chinese Academy of Sciences,University of Chinese Academy of Sciences), Ruibai Xu (University of Science and Technology of China,SKL of Processors, Institute of Computing Technology, Chinese Academy of Sciences), Tingfeng Ruan (SKL of Processors, Institute of Computing Technology, Chinese Academy of Sciences,University of Chinese Academy of Sciences), Jun Bi (SKL of Processors, Institute of Computing Technology, Chinese Academy of Sciences), Rui Zhang (SKL of Processors, Institute of Computing Technology, Chinese Academy of Sciences), Di Huang (SKL of Processors, Institute of Computing Technology, Chinese Academy of Sciences), Xinkai Song (SKL of Processors, Institute of Computing Technology, Chinese Academy of Sciences), Yifan Hao (SKL of Processors, Institute of Computing Technology, Chinese Academy of Sciences), Xing Hu (SKL of Processors, Institute of Computing Technology, Chinese Academy of Sciences), Zidong Du (SKL of Processors, Institute of Computing Technology, Chinese Academy of Sciences), Chongqing Zhao (Tencent), Jie Jiang (Tencent), Qi Guo (SKL of Processors, Institute of Computing Technology, Chinese Academy of Sciences)
  - Mosaic 是面向同时具有 scalar、vector、tensor unit 的 CPU/GPU 深度学习编译器。它不先固定 tile 再选同类指令，而用 iTex affine abstraction 表达各类指令语义，从底向上把同一 tensor computation 拼成异构 instruction mapping，并调度这些指令避开结构冲突、挖掘跨单元 ILP。
  - 相较 top-down tiling 生成同质指令映射，核心创新是把不同算术指令当作可拼接 tile，在语义等价约束下共同覆盖计算并并发占用多类执行单元。
  - Deep-learning Compiler、Instruction-level Parallelism、iTex Tessellation、异构执行单元、Tensor Operator Scheduling

- [DynaX: Sparse Attention Acceleration with Dynamic X:M Fine-Grained Structured Pruning](https://doi.org/10.1145/3676641.3715991)
  - Xiao Xiong (College of Computer Science, Chongqing University), Zhaorui Chen (College of Computer Science, Chongqing University), Yue Liang (College of Computer Science, Chongqing University), Minghao Tian (College of Computer Science, Chongqing University), Jiaxing Shang (College of Computer Science, Chongqing University), Jiang Zhong (College of Computer Science, Chongqing University), Dajiang Liu (College of Computer Science, Chongqing University)
  - DynaX 是一种算法-硬件协同设计框架，通过动态 X:M 细粒度结构化剪枝加速注意力计算，通过两步剪枝方法实现高稀疏性和更少的预测内存开销，同时在一定程度上保持模式规律性。
  - 固定 N:M 剪枝要求每组都保留同样数量的权重，规则但难以适应注意力分数的局部差异；与传统的 N:M 剪枝不同，DynaX 通过 2 步剪枝方法从一组中动态选择变量 X（而不是固定的 N）重要分数，从而在一定程度上保持模式规律性的同时，具有较高的稀疏性和较少的预测内存开销。
  - 稀疏计算、ML 算子加速、稀疏/张量数据流、加速器映射、算术单元利用率

- [Accelerating Retrieval-Augmented Generation](https://doi.org/10.1145/3669940.3707264)
  - Derrick Quinn (Cornell University), Mohammad Nouri (Cornell University), Neel Patel (Cornell University), John Salihu (University of Kansas), Alireza Salemi (UMass Amherst), Sukhan Lee (Samsung Electronics), Hamed Zamani (UMass Amherst), Mohammad Alian (Cornell University)
  - 该工作先剖析 RAG 的检索—生成流水线，发现更昂贵的精确近邻检索反而可用更少、更准的文档缩短端到端生成。IKS 将 512 GB 向量库放入 type-2 CXL 近存设备，以 cache-coherent CPU/accelerator 接口横向扩展 exact search，使检索加速 13.4–27.9 倍、代表性 RAG 推理缩短 1.7–26.3 倍。
  - 相较把 ANN 当作 RAG 的默认选择，核心创新是从端到端精度—上下文长度权衡证明 exact retrieval 值得加速，并把向量检索与可复用 CXL memory-expander 合为同一设备。
  - RAG 检索流水线、CXL 近存向量搜索、Exact Nearest Neighbor、CPU-加速器一致性、LLM 推理

- [GUST: Graph Edge-Coloring Utilization for Accelerating Sparse Matrix Vector Multiplication](https://doi.org/10.1145/3622781.3674186)
  - Armin Gerami (Computer Science, University of Maryland), Bahar Asgari (Computer Science, University of Maryland)
  - GUST，一种硬件/软件协同设计，其关键在于分离硬件中的乘法器和加法器，从而实现多行和多列的资源共享，从而实现高效的硬件利用率并改善稀疏性带来的负面性能影响。
  - 固定 PE 将乘法和归约绑定，稀疏空洞会同时拖低两类算术单元利用率；GUST 首先拆开 multiplier/adder 供多行多列共享，再用 graph edge coloring 排除共享资源碰撞。
  - 稀疏 SpMV 加速、Graph Edge Coloring、乘加资源解耦、DSA/FPGA、非零冲突调度

- [RASSM: Residue-based Acceleration of Single Sparse Matrix Computation via Adaptive Tiling](https://doi.org/10.1145/3669940.3707219)
  - Anirudh Jain (Georgia Institute of Technology), Pulkit Gupta (Georgia Institute of Technology), Thomas M. Conte (Georgia Institute of Technology)
  - RASSM 面向 SpMM、SDDMM、SpMV、SpTS 等 single-sparse-matrix kernel，为每个输入构建 compact residue matrix 表达 nonzero pattern；runtime/compiler 据此选择输入相关的二维 tile 大小，提高 cache occupancy，并分别利用 spatial 与 temporal locality 减少数据搬运。
  - uniform-shape 或 uniform-occupancy tiling 只看到固定局部统计；RASSM 用 compact residue matrix 表达每个输入的 nonzero pattern，据此分别为时空局部性选择二维 tile。
  - Single-Sparse-Matrix Kernel、Residue Matrix、输入自适应二维 Tiling、Cache Locality、CPU 稀疏线性代数

- [Orion: A Fully Homomorphic Encryption Framework for Deep Learning](https://doi.org/10.1145/3676641.3716008)
  - Austin Ebel (Tandon School of Engineering, New York University), Karthik Garimella (Tandon School of Engineering, New York University), Brandon Reagen (Tandon School of Engineering, New York University)
  - Orion 将任意 PyTorch DNN 自动编译为 FHE private-inference program：single-shot multiplexed packing 映射卷积数据，compiler 同时决定 ciphertext scale、level 与高成本 bootstrap 的插入位置。它支持 ResNet-50 和 1.39 亿参数 YOLO-v1 等此前难以映射的大模型。
  - 相较要求专家手工 packing、rescale 和 bootstrap，核心创新是把卷积布局与噪声/层级管理统一自动化，使通用 PyTorch 网络可端到端转为高效 FHE 程序。
  - Private Neural Inference、FHE Compiler、Ciphertext Packing、Bootstrap Placement、Scale/Noise Management

- [CIPHERMATCH: Accelerating Homomorphic Encryption-Based String Matching via Memory-Efficient Data Packing Packing and In-Flash Processing](https://doi.org/10.1145/3676641.3716251)
  - Mayank Kabra (ETH Zurich), Rakesh Nadig (ETH Zurich), Harshita Gupta (ETH Zurich), Manos Frouzakis (ETH Zurich), Rahul Bera (ETH Zurich), Vamanan Arulchelvan (ETH Zurich), Yu Liang (ETH Zurich), Haiyu Mao (ETH Zurich), Mohammad Sadrosadati (ETH Zurich), Onur Mutlu (ETH Zurich)
  - CIPHERMATCH改进了现有HE方案的基于软件的数据打包方案，仅使用同态加法执行安全字符串匹配，并设计了IFP架构，利用基于NAND闪存的固态硬盘（SSD）的阵列级和位级并行性来加速同态加法。
  - 既有同态字符串匹配会放大密文占用，并依赖昂贵的乘法、旋转和主机—SSD 数据搬运；CIPHERMATCH，它（i）使用基于软件的优化数据打包方案减少了加密后内存占用的增加，（ii）消除了昂贵的同态运算（例如乘法和旋转）的使用，以及（iii）通过设计新的闪存内处理（IFP）架构减少了数据移动。
  - 同态加密字符串匹配、Ciphertext Packing、Addition-only HE Protocol、In-flash Processing、NAND Flash Parallelism

- [ReSBM: Region-based Scale and Minimal-Level Bootstrapping Management for FHE via Min-Cut](https://doi.org/10.1145/3669940.3707276)
  - Yan Liu (Ant Group), Jianxin Lai (Ant Group), Long Li (Ant Group), Tianxiang Sui (Ant Group), Linjie Xiao (Ant Group), Peng Yuan (Ant Group), Xiaojing Zhang (Ant Group), Qing Zhu (Ant Group), Wenguang Chen (Tsinghua University,Ant Group), Jingling Xue (UNSW)
  - ReSBM 把 RNS-CKKS program 的 DFG 切成 multiplicative depth 为 1 的 region，使 scale-management operation 与 bootstrap 只影响区内延迟；区内用 min-cut 联合放置 SMO/bootstrap，跨区再做 bootstrapping-guided rescaling 与 minimal-level placement，平均加速密文推理 12.1%。
  - 分别优化 ciphertext scale 与 bootstrap 会互相破坏 level 决策；ReSBM 先用 depth-1 region 隔离跨区影响，再以 min-cut 和 hierarchical search 联合求解区内、跨区及 minimal target level。
  - FHE Compiler、RNS-CKKS、Scale/Level Management、Min-cut Bootstrapping Placement、Encrypted Inference

- [HALO: Loop-aware Bootstrapping Management for Fully Homomorphic Encryption](https://doi.org/10.1145/3669940.3707275)
  - Seonyoung Cheon (Yonsei University), Yongwoo Lee (Yonsei University), Hoyun Youm (Yonsei University), Dongkwan Kim (Yonsei University), Sungwoo Yun (Yonsei University), Kunmo Jeong (Yonsei University), Dongyoon Lee (Stony Brook University), Hanjun Kim (Yonsei University)
  - HALO 直接在含 flat/nested loop 的 FHE program 上管理 bootstrap：匹配 live-in 与 loop-carried ciphertext 的 type/level，把多个 loop-carried variable 打包到同一密文，按 loop body 长度选择展开程度，并调整 bootstrap target level。
  - 先完全展开 loop 再放 bootstrap 会造成编译/代码爆炸且浪费 ciphertext level；HALO 保留循环结构，并联合决定 carried-value packing、选择性 unrolling 与 target level。
  - FHE Compiler、Loop-aware Bootstrapping、Loop-carried Ciphertext、Ciphertext Packing/Unrolling、Encrypted Program Optimization

- [Affinity-based Optimizations for TFHE on Processing-in-DRAM](https://doi.org/10.1145/3676641.3716246)
  - Kevin Nam (Department of Electrical and Computer Engineering (ECE), Seoul National University,Inter-university Semiconductor Research Center (ISRC), Seoul National University), Heonhui Jung (Department of Electrical and Computer Engineering (ECE), Seoul National University,Inter-university Semiconductor Research Center (ISRC), Seoul National University), Hyunyoung Oh (Department of AI·Software, Gachon University), Yunheung Paek (Department of Electrical and Computer Engineering (ECE), Seoul National University,Inter-university Semiconductor Research Center (ISRC), Seoul National University)
  - 该工作面向真实 Processing-in-DRAM 上的 TFHE，把 sub-task 的 data affinity 与 PIM bank 位置一起分析；offline scheduler 在保持足够并行度时优先把相关计算留在本地，减少 remote data access，并用少量硬件修改在 FPGA PIM 上验证。
  - 既有 TFHE accelerator 只扩大并行度，PIM 上反而触发大量 remote data access；该方法把 sub-task affinity 变成 offline placement/schedule 的一等约束，在本地性与并行性之间求解。
  - TFHE on PIM、Data-affinity Scheduling、Remote Data Access Reduction、Processing-in-DRAM、Offline Task Placement

- [FMCC: Flexible Measurement-based Quantum Computation over Cluster State](https://doi.org/10.1145/3622781.3674185)
  - Yingheng Li (University of Pittsburgh), Aditya Pawar (University of Pittsburgh), Zewei Mo (University of Pittsburgh), Youtao Zhang (University of Pittsburgh), Jun Yang (University of Pittsburgh), Xulong Tang (University of Pittsburgh)
  - FMCC，一种采用启发式动态编程来有效最小化簇状态深度的编译框架，实验结果表明，与最先进的 MBQC 编译相比，FMCC 在小型、中型和大型量子位计数方面实现了 51.7%、57.4% 和 56.8% 的平均深度减少。
  - 既有 MBQC 编译难以在快速增长的 cluster-state 搜索空间中压低执行深度；FMCC 是一种编译框架，它采用启发式动态编程来有效地最小化集群状态深度。
  - 量子计算系统、量子电路编译、量子资源映射、量子互连/存储、量子执行调度

- [QRCC: Evaluating Large Quantum Circuits on Small Quantum Computers through Integrated Qubit Reuse and Circuit Cutting](https://doi.org/10.1145/3622781.3674179)
  - Aditya Pawar (Electrical and Computer Engineering Department, University of Pittsburgh), Yingheng Li (Computer Science Department, University of Pittsburgh), Zewei Mo (Computer Science Department, University of Pittsburgh), Yanan Guo (Electrical and Computer Engineering Department, University of Pittsburgh), Xulong Tang (Computer Science Department, University of Pittsburgh), Youtao Zhang (Computer Science Department, University of Pittsburgh), Jun Yang (Electrical and Computer Engineering Department, University of Pittsburgh)
  - QRCC 是一种利用量子位重用和电路切割（包括线切割和门切割）的集成方法，在小型量子计算机上运行大型电路，并将切割次数减少 29％，并在考虑门切割时进一步减少。
  - qubit reuse、wire cutting 与 gate cutting 往往被分别规划，局部最优会增加总体切割与重构代价；QRCC 是一种利用量子位重用和电路切割（包括线切割和门切割）在小型量子计算机上运行大型电路的集成方法。
  - 量子电路切分与 Qubit 复用、量子计算系统、量子电路编译、量子资源映射、量子互连/存储

- [Optimizing Quantum Circuits, Fast and Slow](https://doi.org/10.1145/3669940.3707240)
  - Amanda Xu (University of Wisconsin-Madison), Abtin Molavi (University of Wisconsin-Madison), Swamit Tannu (University of Wisconsin-Madison), Aws Albarghouthi (University of Wisconsin-Madison)
  - 该工作把量子电路优化统一为两类抽象变换：快速的局部 rewrite rule 与计算昂贵、但能跨更大范围重综合 unitary 的 slow optimizer。guoq 在同一搜索流程中交替组合两者，以门数/操作数为目标保留能为后续重综合创造机会的局部变换。
  - 相较只跑便宜局部重写、或直接承担全局 unitary resynthesis 的高成本，核心创新是把两类优化器放入可组合的统一接口与搜索环中，利用快慢方法之间的互补增益。
  - 量子电路优化、Rewrite Rules、Unitary Resynthesis、guoq、Gate-count Reduction

- [BQSim: GPU-accelerated Batch Quantum Circuit Simulation using Decision Diagram](https://doi.org/10.1145/3676641.3715984)
  - Shui Jiang (The Chinese University of Hong Kong ,University of Wisconsin-Madison), Yi-Hua Chung (University of Wisconsin-Madison), Chih-Chun Chang (University of Wisconsin-Madison), Tsung-Yi Ho (The Chinese University of Hong Kong), Tsung-Wei Huang (University of Wisconsin-Madison)
  - BQSim 面向同一量子电路的大批输入态仿真：先用 decision diagram 压缩电路并消除冗余，再把图结构转换为适合 GPU 顺序/并行访问的表示；task graph 同时安排 GPU kernel、主机处理和数据搬运以隐藏传输开销。
  - 相较把 decision diagram 留在 CPU 上执行，核心创新是先利用它缩减仿真工作量，再转换成 GPU 友好的批处理执行图，从而兼得图压缩率与 GPU 吞吐。
  - 量子电路仿真、Batch Simulation、Decision Diagram、GPU Task Graph、计算与传输重叠

- [Fat-Tree QRAM: A High-Bandwidth Shared Quantum Random Access Memory for Parallel Queries](https://doi.org/10.1145/3676641.3716256)
  - Shifan Xu (Yale Quantum Institute, Yale University), Alvin Lu (Yale Quantum Institute, Yale University), Yongshan Ding (Yale Quantum Institute, Yale University)
  - Fat-Tree QRAM 是一种查询架构，能够同时管道化多个量子查询，同时保持查询速度和保真度的理想扩展，并提出了基于超导电路的 Fat-Tree QRAM 的模块化和片上实现。
  - 传统 QRAM 主要优化单次查询延迟，多个并发查询仍在共享路由结构上串行化；Fat-Tree QRAM 是一种查询架构，能够同时管道化多个量子查询，同时保持查询速度和保真度方面的理想扩展。
  - QRAM Architecture、并行量子查询流水线、Fat-tree Interconnect、超导量子内存实现、Quantum Memory Bandwidth

- [Energy-aware Scheduling and Input Buffer Overflow Prevention for Energy-harvesting Systems](https://doi.org/10.1145/3676641.3715995)
  - Harsh Desai (Carnegie Mellon University), Xinye Wang (Carnegie Mellon University), Brandon Lucia (Carnegie Mellon University)
  - Quetzal 面向能量采集设备上固定速率到达、但计算时间和可用能量波动的推理任务。运行时测量功耗，把等待充电计入端到端 deadline，并用 queue model 预测输入缓冲区何时溢出；风险迫近时选择降低单个任务的质量/算力需求以维持持续处理。
  - 相较按静态能量预算固定降质，核心创新是联合在线功耗、充电等待和输入队列演化做 deadline-aware 决策，只在预测到缓冲溢出时有选择地牺牲质量。
  - 能量采集边缘系统、Energy-aware Scheduling、队列溢出预测、Approximate Computing、Deadline Management

- [Generalizing Reuse Patterns for Efficient DNN on Microcontrollers](https://doi.org/10.1145/3676641.3716257)
  - Jiesong Liu (North Carolina State University), Bin Ren (College of William and Mary), Xipeng Shen (North Carolina State University)
  - 广义重用的概念，揭示了广义重用模式与 DNN 输入矩阵视图或激活图的行/列重新排序之间的关系，彻底改变了可探索重用模式的传统视图，极大地扩展了重用空间。
  - 微控制器 DNN 优化只探索少数预定义 reuse pattern，无法系统利用行列重排产生的更大复用空间；它还开发了两种分析模型，用于分析重用模式对 DNN 准确性和延迟的影响，从而能够有效选择适当的重用模式。
  - TinyML Inference、DNN Reuse Pattern、Activation Row/Column Reordering、Accuracy/Latency Modeling、Microcontroller Acceleration

- [Earth+: On-Board Satellite Imagery Compression Leveraging Historical Earth Observations](https://doi.org/10.1145/3669940.3707222)
  - Kuntai Du (University of Chicago), Yihua Cheng (University of Chicago), Peder Olsen (Microsoft Research), Shadi Noghabi (Microsoft Research), Junchen Jiang (University of Chicago)
  - Earth+ 面向 earth-observation satellite 下行带宽不足、九成以上影像无法回传的问题。地面站把星座内其他卫星最近拍摄的同区域图像上传为 onboard reference，卫星只编码/下载相对 reference 发生变化的区域，在不降低图像质量或增加总资源的情况下把下行用量减少 3.3 倍。
  - 相较逐幅独立压缩，核心创新是把整个卫星星座的跨时间观测变成在轨 reference，使压缩目标从“完整图像像素”改为“相对最新全局观测的变化区域”。
  - 卫星边缘计算、On-board Image Compression、跨卫星历史参考、Change-region Encoding、下行带宽

- [Pirate: No Compromise Low-Bandwidth VR Streaming for Edge Devices](https://doi.org/10.1145/3676641.3716268)
  - Yingtian Zhang (The Pennsylvania State University), Yan Kang (The Pennsylvania State University), Ziyu Ying (The Pennsylvania State University), Wanhang Lu (The Pennsylvania State University), Sijie Lan (The Pennsylvania State University), Huijuan Xu (The Pennsylvania State University), Kiwan Maeng (The Pennsylvania State University), Anand Sivasubramaniam (The Pennsylvania State University), Mahmut T. Kandemir (The Pennsylvania State University), Chita R. Das (The Pennsylvania State University)
  - Pirate 为算力/存储受限的 edge VR 只传输一只眼的画面，并利用该眼图像、disparity 与 optical flow 迭代合成另一眼；左右眼交替作为源视图，在 0.1 bit/pixel 带宽下仍达到 90 FPS，同时节省 20%–40% 带宽。
  - 相较用大型神经网络从双目/视差生成目标视图，核心创新是利用连续帧和双目间的 stereo similarity 做轻量迭代合成，使低带宽与实时高帧率不再二选一。
  - Edge VR Streaming、Stereo View Synthesis、Optical Flow、低带宽视频压缩、90-FPS 实时渲染

- [Nazar: Monitoring and Adapting ML Models on Mobile Devices](https://doi.org/10.1145/3669940.3707246)
  - Wei Hao (Columbia University), Zixi Wang (Columbia University), Lauren Hong (Columbia University), Lingxiao Li (Columbia University), Nader Karayanni (Columbia University), AnMei Dasbach-Prisk (University of California San Diego), Chengzhi Mao (Columbia University), Junfeng Yang (Columbia University), Asaf Cidon (Columbia University)
  - Nazar 在移动设备上持续估计已部署模型的实际准确率；当多个设备共同退化时，平台聚合无用户反馈的观测，定位影响设备群的具体 data-drift root cause，并针对该原因适配模型。两个视觉数据集上准确率相对既有方案最高提升 19.4%。
  - 相较依赖用户标注或逐设备重新训练，核心创新是把跨设备共同退化当作诊断信号，形成“检测群体漂移—定位根因—定向适配”的端到端闭环。
  - 端侧模型运维、Data Drift Monitoring、跨设备根因定位、Model Adaptation、Mobile ML

- [Composing Distributed Computations Through Task and Kernel Fusion](https://doi.org/10.1145/3669940.3707216)
  - Rohan Yadav (Stanford University), Shiv Sundram (Stanford University), Wonchan Lee (NVIDIA), Michael Garland (NVIDIA), Michael Bauer (NVIDIA), Alex Aiken (Stanford University), Fredrik Kjolstad (Stanford University)
  - Diffuse 面向由 cuPyNumeric、Legate Sparse 等 task-based library 组合出的分布式 Python 程序，用分布式计算 IR 跨函数/库边界发现可合并的 task，再由 JIT compiler 融合 task 内 kernel；无需改应用即可在最多 128 GPU 上减少调度、同步和中间数据开销。
  - 相较只在单个库内部做 kernel fusion，核心创新是以可扩展 IR 同时表达跨节点 task dependency 与设备 kernel，使 task fusion 和 JIT kernel fusion 可以联合进行。
  - 分布式 Task Runtime、跨库算子融合、JIT Kernel Fusion、多 GPU 计算、编译器/运行时协同

- [CXLfork: Fast Remote Fork over CXL Fabrics](https://doi.org/10.1145/3676641.3715988)
  - Chloe Alverti (University of Illinois Urbana-Champaign), Stratos Psomadakis (National Technical University of Athens), Burak Ocalan (University of Illinois Urbana-Champaign), Shashwat Jaiswal (University of Illinois Urbana-Champaign), Tianyin Xu (University of Illinois Urbana-Champaign), Josep Torrellas (University of Illinois Urbana-Champaign)
  - CXLfork 在 CXL fabric 上提供跨节点 remote fork：进程状态驻留全局共享 CXL memory，目标节点按需映射并细粒度决定哪些页面留在本地或远端，从而接近零序列化、零复制地克隆进程。基于它的 CXL-porter 用于 serverless 横向扩缩，恢复时延接近本地 fork且本地内存平均减少 87%。
  - 相较把函数 snapshot 经网络复制到每个节点，核心创新是把 fork 的 copy-on-write 状态提升为集群共享对象，使冷启动与跨节点状态去重由 CXL 一致内存直接承担。
  - CXL Fabric、Remote Fork、Serverless Cold Start、进程状态去重、分层内存

- [OS2G: A High-Performance DPU Offloading Architecture for GPU-based Deep Learning with Object Storage](https://doi.org/10.1145/3676641.3716265)
  - Zhen Jin (Zhejiang University,Alibaba Group), Yiquan Chen (Alibaba Group), Mingxu Liang (Alibaba Group), Yijing Wang (Alibaba Group), Guoju Fang (Alibaba Group), Ao Zhou (Alibaba Group), Keyao Zhang (Zhejiang University), Jiexiong Xu (Zhejiang University), Wenhai Lin (Zhejiang University), Yiquan Lin (Zhejiang University), Shushu Zhao (Alibaba Group), Wenkai Shi (Alibaba Group), Zhenhua He (Alibaba Group), Shishun Cai (Alibaba Group), Wenzhi Chen (Zhejiang University)
  - OS2G 面向以 object storage 喂数据的 GPU 训练任务，把对象存储 client 下沉到 DPU，并以异步、预读和并发访问提高吞吐；GPUDirect DPU 让数据从 DPU 直接进入 GPU，绕过 host CPU/DRAM 的二次搬运。ResNet18 实验同时降低训练时间和 57%–62% CPU 消耗。
  - 相较只把 S3 协议处理卸载到 DPU、数据仍需 DPU→host→GPU 的方案，核心创新是把存储控制面卸载与 DPU-GPU 直传数据面合为一体。
  - DPU 卸载、GPU 训练数据管线、对象存储、GPUDirect DPU、Host Bypass

- [pulse: Accelerating Distributed Pointer-Traversals on Disaggregated Memory](https://doi.org/10.1145/3669940.3707253)
  - Yupeng Tang (Yale University), Seung-seob Lee (Yale University), Abhishek Bhattacharjee (Yale University), Anurag Khandelwal (Yale University)
  - pulse 面向 rack-scale disaggregated memory 上的链表、树和图 pointer traversal。CPU 节点提交 traversal program，靠近远端内存的执行单元沿依赖指针继续访问，并把一个遍历分布到多个 memory node；这样避免每一步都经网络返回 CPU，同时保留对不同 linked structure 的可编程性。
  - 相较只在 CPU 侧增加 cache，核心创新是把地址依赖的“下一跳计算”移到数据所在的 disaggregated-memory 端并支持跨节点协同，从根本上消除逐指针网络往返。
  - Disaggregated Memory、Pointer Traversal、Near-memory Execution、Rack-scale Distribution、Linked Data Structures

- [RANGE-BLOCKS: A Synchronization Facility for Domain-Specific Architectures](https://doi.org/10.1145/3669940.3707225)
  - Anagha Molakalmur Anil Kumar (Simon Fraser University), Aditya Prasanna (Simon Fraser University), Arrvindh Shriraman (Simon Fraser University)
  - Range-blocks（RBlox）给 domain-specific accelerator 增加 key-range hardware lock：一个 symbolic range 可覆盖多个嵌套动态对象，约 2 KB on-chip table 即可表示同步状态；range 还直接标出互斥区域，无需按地址逐项排序。
  - address-based atomic 为每个对象保存 lock，动态嵌套结构需要大 cache；RBlox 用 symbolic key range 一次描述整片嵌套对象，并利用不重叠范围直接开放并行。
  - Domain-specific Accelerator、计算/通信资源匹配、Operator Mapping、可重构硬件

- [Enhancing CGRA Efficiency Through Aligned Compute and Communication Provisioning](https://doi.org/10.1145/3669940.3707230)
  - Zhaoying Li (National University of Singapore), Pranav Dangi (National University of Singapore), Chenyang Yin (Peking University), Thilini Kaushalya Bandara (National University of Singapore), Rohan Juneja (National University of Singapore), Cheng Tan (Google), Zhenyu Bai (National University of Singapore), Tulika Mitra (National University of Singapore)
  - Plaid 面向 communication network 明显过度配置的 edge CGRA，把应用 dataflow graph 分解为反复出现的小型 communication motif；collective processing unit 一次执行 motif 内多项运算并共同路由依赖，compiler 再按层次映射/调度 motif，使计算与互连供给匹配。
  - 相较为任意逐 PE 路由预留通用互连，核心创新是以真实程序中的 motif 作为计算—通信共同分配单位，用受控结构化降低面积/功耗而不牺牲 CGRA 通用性。
  - CGRA、Communication Motif、Collective Processing Unit、Hierarchical Mapping、Compute/Network Co-design

- [Squeezing Operator Performance Potential for the Ascend Architecture](https://doi.org/10.1145/3676641.3716243)
  - Yuhang Zhou (State Key Laboratory for Novel Software Technology, Nanjing University), Zhibin Wang (State Key Laboratory for Novel Software Technology, Nanjing University), Guyue Liu (Peking University), Shipeng Li (State Key Laboratory for Novel Software Technology, Nanjing University), Xi Lin (State Key Laboratory for Novel Software Technology, Nanjing University), Zibo Wang (State Key Laboratory for Novel Software Technology, Nanjing University), Yongzhong Wang (Huawei Technologies Co., Ltd.), Fuchun Wei (Huawei Technologies Co., Ltd.), Jingyi Zhang (Huawei Technologies Co., Ltd.), Zhiheng Hu (Huawei Technologies Co., Ltd.), Yanlin Liu (Huawei Technologies Co., Ltd.), Chunsheng Li (Huawei Technologies Co., Ltd.), Ziyang Zhang (Huawei Technologies Co., Ltd.), Yaoyuan Wang (Huawei Technologies Co., Ltd.), Bin Zhou (Shandong University), Wanchun Dou (Nanjing University, State Key Laboratory for Novel Software Technology), Guihai Chen (Nanjing University, State Key Laboratory for Novel Software Technology), Chen Tian (Nanjing University, State Key Laboratory for Novel Software Technology)
  - 该工作为 Ascend NPU operator 建立 component-based roofline：把片上不同计算、搬运和存储组件分别抽象为性能上界，以实测/模型数据判断当前 operator 被哪个组件限制；随后按诊断结果选择对应优化，并在端到端模型获得 1.07–2.15 倍加速。
  - 相较只有 compute-vs-bandwidth 两条总上界的传统 roofline，核心创新是把 Ascend 需要用户显式管理的内部组件分别建模，使分析结果能直接定位到可执行的算子优化动作。
  - Ascend NPU、Operator Optimization、Component Roofline、性能瓶颈诊断、AI Accelerator

- [PICACHU: Plug-In CGRA Handling Upcoming Nonlinear Operations in LLMs](https://doi.org/10.1145/3676641.3716013)
  - Jiajun Qin (New York University,Zhejiang University), Tianhua Xia (New York University), Cheng Tan (Google,Arizona State University), Jeff Zhang (Arizona State University), Sai Qian Zhang (New York University)
  - PICACHU 是插接式 CGRA 加速器，专门承接 LLM 中 softmax、normalization、activation 等非线性算子；定制近似/数值算法和 compiler toolchain 把不同精度的算子映射到可重构阵列，再与主 LLM accelerator 协同执行。
  - 相较为单个非线性算子设计固定功能单元，核心创新是用一个可编程 CGRA 和统一编译路径覆盖 LLM 全部非线性操作，在效率、精度选择与未来算子变化间取得可扩展性。
  - LLM 推理、非线性算子、CGRA 加速器、插接式协处理器、编译映射

- [Salus: A Practical Trusted Execution Environment for CPU-FPGA Heterogeneous Cloud Platforms](https://doi.org/10.1145/3622781.3674169)
  - Yu Zou (Alibaba Group), Yiran Li (Alibaba Group), Sheng Wang (Alibaba Group), Le Su (Alibaba Group), Zhen Gu (DAMO Academy, Alibaba Group,Hupan Lab), Yanheng Lu (DAMO Academy, Alibaba Group,Hupan Lab), Yijin Guan (DAMO Academy, Alibaba Group,Hupan Lab), Dimin Niu (DAMO Academy, Alibaba Group,Hupan Lab), Mingyu Gao (Tsinghua University,Shanghai AI Laboratory), Yuan Xie (DAMO Academy, Alibaba Group,Hupan Lab), Feifei Li (Alibaba Group)
  - Salus 在支持 TEE 的 host CPU enclave 中建立 FPGA 控制与 attestation 根，复用商用云的 bitstream utility 验证/装载 bitstream，并在 FPGA 侧加入 security-enhanced IP 保护执行期数据。它因而能在不改云厂商完整基础设施的前提下，为 COTS CPU-FPGA 平台提供端到端 TEE。
  - 相较假定独占/可定制 FPGA 的 standalone TEE，核心创新是让 CPU enclave 为受限的商用 FPGA 服务补上可信控制面，并用少量 FPGA IP 封住数据面信任缺口。
  - CPU-FPGA TEE、Cloud FPGA、Bitstream Attestation、Host Enclave、异构可信计算

- [Harmonia: A Unified Framework for Heterogeneous FPGA Acceleration in the Cloud](https://doi.org/10.1145/3676641.3716259)
  - Luyang Li (Institute of Computing Technology, Chinese Academy of Sciences,University of Chinese Academy of Sciences), Heng Pan (Computer Network Information Center, Chinese Academy of Sciences), Xinchen Wan (Hong Kong University of Science and Technology), Kai Lv (Institute of Computing Technology, Chinese Academy of Sciences), Zilong Wang (Hong Kong University of Science and Technology), Qian Zhao (Douyin Co., Ltd.), Feng Ning (Douyin Co., Ltd.), Qingsong Ning (Douyin Co., Ltd.), Shideng Zhang (Douyin Co., Ltd.), Zhenyu Li (Institute of Computing Technology, Chinese Academy of Sciences,University of Chinese Academy of Sciences), Layong Luo (Researcher), Gaogang Xie (Computer Network Information Center, Chinese Academy of Sciences,University of Chinese Academy of Sciences)
  - Harmonia 是一种用于云中异构 FPGA 加速的统一框架，可将 shell 开发工作量减少 69%-93%，并简化角色和软件配置，而开销可以忽略不计。
  - 平台专用 shell 让每种 FPGA/role 都要重复适配；Harmonia 以自动 platform adapter 隔离器件差异，以 reusable building block 和 hierarchical tailoring 生成统一但不过量的 shell。
  - FPGA 系统、Cloud FPGA、FPGA Runtime/Toolchain、Bitstream/Hardware Security、FPGA Verification

- [PhasePrint: Exposing Cloud FPGA Fingerprints by Inducing Timing Faults at Runtime](https://doi.org/10.1145/3676641.3716012)
  - Jubayer Mahmod (Virginia Tech), Matthew Hicks (Virginia Tech)
  - PhasePrint 在 cloud FPGA 内用 internal clock synthesizer 生成严格相位相关的双时钟，逐步调相使特制但功能合法的电路出现 timing fault；fault location 形成反映制造差异的 feature vector，再由分类器识别具体板卡。300 块 AWS FPGA 上准确率超过 99%。
  - 相较依赖被云商屏蔽的温度、传感器或设备标识，核心创新是主动注入可控时序故障，把纯片上 error pattern 转成 fingerprint；既可用于攻击定位，也可用于防御性轮换设备。
  - Cloud FPGA Fingerprinting、Timing-fault Injection、Manufacturing Variation、On-chip Signature、云硬件安全

- [Hassert: Hardware Assertion-Based Verification Framework with FPGA Acceleration](https://doi.org/10.1145/3622781.3698899)
  - Ziqing Zhang (State Key Lab of Processors, Institute of Computing Technology, Chinese Academy of Sciences,University of Chinese Academy of Sciences), Weijie Weng (Xiamen University of Technology), Yaning Li (University College Dublin), Lijia Cai (Hong Kong University of Science and Technology), Haoyu Wang (Zhejiang University), David Boland (The University of Sydney), Yungang Bao (State Key Lab of Processors, Institute of Computing Technology, Chinese Academy of Sciences,University of Chinese Academy of Sciences), Kan Shi (State Key Lab of Processors, Institute of Computing Technology, Chinese Academy of Sciences,University of Chinese Academy of Sciences)
  - Hassert是一种高效的ABV框架，它将FPGA上的高性能验证与软件中的细粒度调试相结合，并提出了微架构引导的硬件快照方案来提高调试效率。
  - 软件 ABV 仿真保留可见性但速度慢，FPGA prototype 速度快却难以定位 assertion 触发时的微架构状态；为了应对这些挑战，该工作推出了 Hassert，这是一种高效的 ABV 框架，它将 FPGA 上的高性能验证与软件中的细粒度调试相结合。
  - FPGA 系统、形式化验证、Cloud FPGA、FPGA Runtime/Toolchain、Bitstream/Hardware Security

- [Coach: Exploiting Temporal Patterns for All-Resource Oversubscription in Cloud Platforms](https://doi.org/10.1145/3669940.3707226)
  - Benjamin Reidys (University of Illinois Urbana-Champaign), Pantea Zardoshti (Microsoft), Íñigo Goiri (Microsoft), Celine Irvene (Microsoft), Daniel S. Berger (Microsoft,University of Washington), Haoran Ma (University of California-Los Angeles), Kapil Arya (Microsoft), Eli Cortez (Microsoft), Taylor Stark (Microsoft), Eugene Bak (Microsoft), Mehmet Iyigun (Microsoft), Stanko Novaković (Google), Lisa Hsu (Meta), Karel Trueba (Microsoft), Abhisek Pan (Microsoft), Chetan Bansal (Microsoft), Saravan Rajmohan (Microsoft), Jian Huang (University of Illinois Urbana-Champaign), Ricardo Bianchini (Microsoft)
  - Coach 根据 Azure VM 的长期 CPU、内存等多资源时间序列预测互补负载，把每种资源拆成 guaranteed 与 oversubscribed 份额后进行 VM placement；运行时监控争用并重点处理迁移代价高的内存回收。它在性能退化很小的情况下让平台最多多容纳约 26% VM。
  - 相较只超卖 CPU 或按瞬时峰值装箱，核心创新是利用 VM 间长期时间互补性同时超卖所有资源，并以可兑现的 guaranteed/borrowed 双份额控制风险。
  - 云 VM 调度、多资源超卖、时间序列预测、内存争用控制、资源利用率

- [Cooperative Graceful Degradation in Containerized Clouds](https://doi.org/10.1145/3669940.3707244)
  - Kapil Agrawal (University of California, Irvine), Sangeetha Abdu Jyothi (University of California, Irvine and VMware Research)
  - Phoenix 在大规模故障造成容量紧缩时读取容器 criticality tag 和应用 dependency graph，执行 diagonal scaling：优先关闭非关键容器，把剩余容量留给关键服务，同时兼顾云运营方目标。Kubernetes controller 可在 10 秒内处理十万节点故障场景，并把关键服务可用性最多提高 2 倍。
  - 相较由云平台无差别驱逐 Pod 或由应用各自降级，核心创新是建立应用—运营方共享的 criticality contract，把业务语义直接用于全局故障资源重分配。
  - Cloud Resilience、Kubernetes 故障恢复、Graceful Degradation、容器关键性、Dependency-aware Scaling

- [DarwinGame: Playing Tournaments for Tuning Applications in Noisy Cloud Environments](https://doi.org/10.1145/3669940.3707259)
  - Rohan Basu Roy (University of Utah), Vijay Gadepally (Massachusetts Institute of Technology), Devesh Tiwari (Northeastern University)
  - DarwinGame 面向存在邻居干扰和噪声的共享云，将不同参数配置的应用执行组织成 tournament，以相对胜负而非单次绝对时间判断配置优劣；反复比较可抵消不可控干扰，最终选择稳定的高性能配置。
  - 相较假设 benchmark 可重复、直接比较噪声测量值的 autotuner，核心创新是用 tournament ranking 将云环境干扰转化为成对统计证据。
  - Cloud Autotuning、共享集群干扰、Tournament Search、应用参数调优、稳健性能测量

- [Copper and Wire: Bridging Expressiveness and Performance for Service Mesh Policies](https://doi.org/10.1145/3669940.3707257)
  - Divyanshu Saxena (The University of Texas at Austin), William Zhang (The University of Texas at Austin), Shankara Pailoor (The University of Texas at Austin), Isil Dillig (The University of Texas at Austin), Aditya Akella (The University of Texas at Austin)
  - Copper and Wire 从头设计 service mesh policy 栈：以明确语义的通信抽象和 policy language 表达 L7 规则，control plane 再针对不同 dataplane 生成最小化执行计划。复杂策略代码最多缩短 6.75 倍，尾延迟降低 2.6 倍且 CPU 少用最多 39%。
  - 相较把策略绑定到特定 sidecar/dataplane、让表达能力直接换取运行开销，核心创新是把“策略语义”与“执行载体”分离，并由控制面证明式地选择正确且低成本的 enforcement。
  - Service Mesh、L7 Policy Language、控制面/数据面解耦、微服务网络、尾延迟

- [MetaSapiens: Real-Time Neural Rendering with Efficiency-Aware Pruning and Accelerated Foveated Rendering](https://doi.org/10.1145/3669940.3707227)
  - Weikai Lin (University of Rochester), Yu Feng (Shanghai Jiao Tong University), Yuhao Zhu (University of Rochester)
  - MetaSapiens 是一种PBNR系统，首次在移动设备上提供实时神经渲染，同时保持人类视觉质量，并引入了PBNR的注视点渲染方法，利用人类外围区域的低视力来放松渲染质量并提高渲染速度。
  - 移动端 PBNR 若对整幅画面使用同等模型容量和视觉质量，算力不足以达到实时帧率；MetaSapiens 是一种 PBNR 系统，首次在移动设备上提供实时神经渲染，同时保持人类视觉质量。
  - 实时神经渲染、图形渲染流水线、Graphics Pipeline、Neural/Ray Rendering、GPU Rendering Architecture

- [D-VSync: Decoupled Rendering and Displaying for Smartphone Graphics](https://doi.org/10.1145/3669940.3707235)
  - Yuanpei Wu (IPADS, Shanghai Jiao Tong University,Engineering Research Center for Domain-specific Operating Systems, Ministry of Education), Dong Du (IPADS, Shanghai Jiao Tong University,Engineering Research Center for Domain-specific Operating Systems, Ministry of Education), Chao Xu (Fields Lab, Huawei Central Software Institute), Yubin Xia (IPADS, Shanghai Jiao Tong University,Engineering Research Center for Domain-specific Operating Systems, Ministry of Education), Ming Fu (Fields Lab, Huawei Central Software Institute), Binyu Zang (IPADS, Shanghai Jiao Tong University,Engineering Research Center for Domain-specific Operating Systems, Ministry of Education), Haibo Chen (IPADS, Shanghai Jiao Tong University,Key Laboratory of System Software (Chinese Academy of Science))
  - D-VSync 解决 VSync 限制的关键在于，解耦使零星的长帧能够利用常见短帧节省的计算能力，从而提供更大的时间窗口来容忍工作负载波动。
  - VSync 要求 frame 在一个同步周期内 render 并 display；D-VSync 允许提前多个周期执行，把大量短帧留下的计算余量转给偶发长帧，同时仍按原 display 时序提交。
  - 图形渲染流水线、Graphics Pipeline、Neural/Ray Rendering、GPU Rendering Architecture、Frame/Atomic Scheduling

- [StreamGrid: Streaming Point Cloud Analytics via Compulsory Splitting and Deterministic Termination](https://doi.org/10.1145/3676641.3716021)
  - Yu Feng (Shanghai Jiao Tong University,Shanghai Qi Zhi Institute), Zheng Liu (Shanghai Jiao Tong University), Weikai Lin (University of Rochester), Zihan Liu (Shanghai Jiao Tong University,Shanghai Qi Zhi Institute), Jingwen Leng (Shanghai Jiao Tong University,Shanghai Qi Zhi Institute), Minyi Guo (Shanghai Jiaotong University,Shanghai Qi Zhi Institute), Zhezhi He (Shanghai Jiao Tong University), Jieru Zhao (Shanghai Jiao Tong University), Yuhao Zhu (University of Rochester)
  - StreamGrid 为点云处理建立全流式硬件流水线：compulsory splitting 把不规则空间邻域拆成有界工作单元，deterministic termination 保证每段流在有限时间结束，设计工具再按数据依赖自动确定片上 line buffer 容量。这样可持续处理点流而不把中间邻域写回片外内存。
  - 相较只能用于规则图像窗口的 line-buffer pipeline，核心创新是把大小不定、邻居数变化的点云访问转化为边界可证明的流，使其也能用有限片上缓存连续执行。
  - 点云加速、Streaming Pipeline、Compulsory Splitting、片上 Buffer Sizing、片外流量消除

- [ARC: Warp-level Adaptive Atomic Reduction in GPUs to Accelerate Differentiable Rendering](https://doi.org/10.1145/3669940.3707238)
  - Sankeerth Durvasula (Vector Institute, University of Toronto), Adrian Zhao (Vector Institute, University of Toronto), Fan Chen (University of Toronto), Ruofan Liang (Vector Institute, University of Toronto), Pawan Kumar Sanjaya (Vector Institute, University of Toronto), Yushi Guan (Vector Institute, University of Toronto), Christina Giannoula (Vector Institute, University of Toronto), Nandita Vijaykumar (Vector Institute, University of Toronto)
  - ARC 加速 differentiable rendering 训练中的 gradient atomic：先在 GPU core 寄存器内合并同一 warp 对相同地址的更新，再依据每个 warp 的 atomic traffic，把剩余归约动态分配到 core 或 L2 atomic unit；同时给出硬件版 ARC-HW 与纯软件 ARC-SW。
  - L2 atomic unit 集中处理所有 gradient update，既串行又浪费 warp 内相同地址；ARC 先在 core 内做 warp reduction，再按 traffic 在 core/L2 间分摊剩余 atomic。
  - GPU 系统、图形渲染流水线、Graphics Pipeline、Neural/Ray Rendering、GPU Rendering Architecture

- [Treelet Accelerated Ray Tracing on GPUs](https://doi.org/10.1145/3676641.3716279)
  - Yuan Hsi Chou (University of British Columbia), Tor M. Aamodt (University of British Columbia)
  - Virtualized Treelet Queues 把 BVH 切成可复用 treelet；ray virtualization 在发出 trace-ray 后回收 raygen CUDA core，以增加同时在途 ray，dynamic queue 根据局部状态切换 traversal mode，warp repacking 再提高 RT unit 的 SIMT 利用率。
  - 把专用 treelet accelerator 直接移植到 GPU 会因在途 ray 不足和 warp divergence 失效；该设计同时虚拟化 ray 生命周期、动态切 traversal mode，并在 RT unit 前重新打包 warp。
  - 分布式追踪与可观测性、GPU 系统、Graphics Pipeline、Neural/Ray Rendering、GPU Rendering Architecture

- [EXIST: Enabling Extremely Efficient Intra-Service Tracing Observability in Datacenters](https://doi.org/10.1145/3676641.3716283)
  - Xinkai Wang (Shanghai Jiao Tong University), Xiaofeng Hou (Shanghai Jiao Tong University), Chao Li (Shanghai Jiao Tong University), Yuancheng Li (Shanghai Jiao Tong University), Du Liu (Shanghai Jiao Tong University), Guoyao Xu (Alibaba Group), Guodong Yang (Alibaba Group), Liping Zhang (Alibaba Group), Yuemin Wu (Alibaba Cloud), Xiaopeng Yuan (Alibaba Cloud), Quan Chen (Shanghai Jiao Tong University), Minyi Guo (Shanghai Jiao Tong University)
  - EXIST 用现成 hardware tracing 收集数据中心服务内部事件，先消除昂贵 tracing control operation，再按应用状态动态分配有限 trace buffer，并在集群级协调 coverage。它将 intra-service tracing 开销压到千分位量级，同时相对 exhaustive trace 保持 90% 以上诊断准确度。
  - 相较固定采样率或只采 RPC 边界，核心创新是把控制操作、buffer 配额和跨实例覆盖率作为一体优化，使内部因果追踪可在高负载生产集群持续开启。
  - Datacenter Observability、Hardware Tracing、Intra-service Causality、Trace Buffer Allocation、集群级采样

- [Mint: Cost-Efficient Tracing with All Requests Collection via Commonality and Variability Analysis](https://doi.org/10.1145/3669940.3707287)
  - Haiyu Huang (Sun Yat-sen University), Cheng Chen (Alibaba Group), Kunyi Chen (Alibaba Group), Pengfei Chen (Sun Yat-sen University), Guangba Yu (Sun Yat-sen University), Zilong He (Sun Yat-sen University), Yilun Wang (Sun Yat-sen University), Huxing Zhang (Alibaba Group), Qi Zhou (Alibaba Group)
  - Mint 不再按请求整条保留或整条丢弃 trace，而是在 agent 端把每条 trace 分解为跨请求共享的 pattern 与变化 parameter：模式聚合、参数过滤后仍覆盖所有请求，存储与网络量分别降至平均 2.7% 和 4.2%。
  - 相较 head/tail sampling 的“1 或 0”取舍，核心创新是用 commonality + variability 表示压缩完整 trace population，在保留罕见变化线索时消除重复结构。
  - Distributed Tracing、全请求采集、Trace Pattern Compression、Observability Agent、存储/网络开销

- [Automatic Tracing in Task-Based Runtime Systems](https://doi.org/10.1145/3669940.3707237)
  - Rohan Yadav (Stanford University), Michael Bauer (NVIDIA), David Broman (KTH Royal Institute of Technology), Michael Garland (NVIDIA), Alex Aiken (Stanford University), Fredrik Kjolstad (Stanford University)
  - Apophenia，这是一个自动跟踪基于任务的运行时系统的依赖分析的系统，消除了程序员手动注释的负担，并使新的复杂程序能够被跟踪。
  - task-based runtime 的 tracing 依赖程序员手写 dependency annotation，复杂新程序容易遗漏因果边；Apophenia 是一个可以自动跟踪基于任务的运行时系统的依赖分析的系统，消除了程序员手动注释的负担，并能够跟踪新的复杂程序。
  - 运行时系统、分布式追踪与可观测性、Systems Observability、Trace Collection/Compression、Runtime Dependency Tracking

- [Enabling Efficient Mobile Tracing with BTrace](https://doi.org/10.1145/3676641.3715994)
  - Jiawei Wang (Huawei Dresden Research Center,Huawei Central Software Institute), Nian Liu (Huawei Central Software Institute), Arnau Casadevall-Saiz (Huawei Dresden Research Center,Huawei Central Software Institute), Yutao Liu (Huawei Dresden Research Center,Huawei Central Software Institute), Diogo Behrens (Huawei Dresden Research Center,Huawei Central Software Institute), Ming Fu (Huawei Central Software Institute), Ning Jia (Huawei Central Software Institute), Hermann Härtig (Technische Universität Dresden), Haibo Chen (Huawei Central Software Institute,Shanghai Jiao Tong University)
  - BTrace 为 smartphone tracing 把一个 global buffer 切成 block，再按各 CPU core 的实时 trace 压力动态分配；写入仍走低争用 per-core path，同时可跨 block 保留更长连续历史，并处理 core oversubscription 与在线 resize。
  - per-core buffer 快但很快覆盖历史，单一 global buffer 又争用严重；BTrace 把全局空间切成 block，按各 core 的 trace 压力动态分配，从而同时保留局部写入与更长连续窗口。
  - 分布式追踪与可观测性、Systems Observability、Trace Collection/Compression、Runtime Dependency Tracking、Performance Methodology

- [Rethinking Java Performance Analysis](https://doi.org/10.1145/3669940.3707217)
  - Stephen M. Blackburn (Google,Australian National University), Zixian Cai (Australian National University), Rui Chen (Unaffiliated-Independent), Xi Yang (IOP Systems), John Zhang (Canva), John Zigman (The University of Sydney)
  - 该工作重建 DaCapo Java benchmark suite：用 47 个维度和 PCA 刻画 22 个新增/更新 workload 的多样性，并把新的测量方法纳入统一框架；随后用它重新评估生产级 JVM 与 garbage collector，展示旧 workload/方法会怎样改变性能结论。
  - 相较把 benchmark 当作静态程序集合，核心贡献是把 workload representativeness、测量方法和持续维护一起作为性能分析基础设施，并给出可复现的 Java 生产性能基线。
  - Java Performance、DaCapo Benchmark、方法学验证、Garbage Collection、Workload Characterization

- [MPC-Pipe: an Efficient Pipeline Scheme for Semi-honest MPC Machine Learning](https://doi.org/10.1145/3622781.3674175)
  - Yongqin Wang (Department of Electrical & Computer Engineering, University of Southern California), Rachit Rajat (Department of Electrical & Computer Engineering, University of Southern California), Murali Annavaram (Department of Electrical & Computer Engineering, University of Southern California)
  - MPC-Pipe 面向半诚实多数方设置下的 CNN/Transformer 训练与推理，把 MPC online phase 的 share computation 与 communication 重新编排为三类流水：跨 linear layer、non-linear layer 内部，以及不同 batch 之间的 pipeline，并在修改后的 CrypTen 中实现。
  - 相较每层先算完 share 再通信的串行协议执行，核心创新是按算子和 batch 的真实依赖拆开安全计算阶段，在不改变 MPC 安全模型时覆盖计算—通信空隙。
  - Secure ML、Semi-honest MPC、Training/Inference Pipeline、Compute-Communication Overlap、CrypTen

- [Cinnamon: A Framework for Scale-Out Encrypted AI](https://doi.org/10.1145/3669940.3707260)
  - Siddharth Jayashankar (Carnegie Mellon University), Edward Chen (Carnegie Mellon University), Tom Tang (Carnegie Mellon University), Wenting Zheng (Carnegie Mellon University), Dimitrios Skarlatos (Carnegie Mellon University)
  - Cinnamon 通过利用程序各个级别的并行性，使用算法、编译器和硬件技术来为 FHE 创建横向扩展设计（而不是单片芯片设计），从而加速加密计算。
  - 单片 FHE accelerator 的资源规模随模型膨胀且难承载 BERT；Cinnamon 把算法、编译和硬件的多层并行统一映射到 scale-out 节点，使密文计算可横向扩展而非继续增大一颗芯片。
  - Encrypted AI、Scale-out FHE、BERT 密文推理、多层并行化、Algorithm-Compiler-Hardware Co-design

- [PipeLLM: Fast and Confidential Large Language Model Services with Speculative Pipelined Encryption](https://doi.org/10.1145/3669940.3707224)
  - Yifan Tan (Institute of Parallel and Distributed Systems, SEIEE, Shanghai Jiao Tong University), Cheng Tan (Northeastern University), Zeyu Mi (Institute of Parallel and Distributed Systems, SEIEE, Shanghai Jiao Tong University), Haibo Chen (Institute of Parallel and Distributed Systems, SEIEE, Shanghai Jiao Tong University)
  - PipeLLM 为机密 LLM 在线服务把 model weight/数据的加密、PCIe 传输和 GPU 推理组成 speculative pipeline：系统预测后续会用到的数据并提前加密/搬运，在预测错误时回退，从而隐藏 CPU 加密和 I/O 开销并保持 enclave/加密保护。
  - 相较先完成整模型加密与传输再启动推理，核心创新是把保护操作放入可推测的流水线，使机密性成本与 GPU 计算重叠。
  - LLM Serving、Confidential AI、Speculative Pipeline、加密/传输重叠、GPU 推理

- [Practical Federated Recommendation Model Learning Using ORAM with Controlled Privacy](https://doi.org/10.1145/3676641.3716014)
  - Jinyu Liu (The Pennsylvania State University), Wenjie Xiong (Virginia Tech), G. Edward Suh (NVIDIA,Cornell University), Kiwan Maeng (The Pennsylvania State University)
  - FEDORA 通过引入 ε-FDP（一种平衡 ORAM 隐私与性能的正式方法），并将大型 ORAM 放置在具有 SSD 友好优化的节能且经济高效的 SSD 中，减少了 ORAM 令人望而却步的延迟和内存开销。
  - 严格 ORAM 会让大 embedding 的联邦训练不可用；FEDORA 只让用户访问私有样本涉及的 table subset，以 ε-FDP 显式选择隐私—性能点，并用 SSD-friendly ORAM 承担大容量状态。
  - 联邦学习、Privacy-preserving ML、Secure ML Runtime、模型/控制流安全、隐私—性能权衡

- [Tackling ML-based Dynamic Mispredictions using Statically Computed Invariants for Attack Surface Reduction](https://doi.org/10.1145/3676641.3716276)
  - Chris Porter (IBM Research), Sharjeel Khan (Georgia Institute of Technology), Kangqi Ni (Georgia Institute of Technology), Santosh Pande (Georgia Institute of Technology)
  - 该框架先用 whole-application ML 预测运行时合法 function-call set 以缩减 code-reuse gadget；预测未命中时，Datalog 静态计算的 ensue(f) 集合给出任何合法执行中可跟随 f 的函数，轻量 runtime check 据此区分普通误判与攻击。
  - 单靠 ML call-set predictor 无法证明一次未命中是 benign 还是 attack；ensue() 用全程序静态不变量为运行时误判提供可验证边界，把精度模型与安全判定解耦。
  - ML-based Control-flow Prediction、Static Invariants、Program Debloating、Datalog Call Relation、Attack/Misprediction Discrimination

- [Control Logic Synthesis: Drawing the Rest of the OWL](https://doi.org/10.1145/3622781.3674170)
  - Zachary D. Sisco (University of California, Santa Barbara), Andrew David Alex (University of California, Santa Barbara), Zechen Ma (University of California, Santa Barbara), Yeganeh Aghamohammadi (University of California, Santa Barbara), Boming Kong (University of California, Santa Barbara), Benjamin Darnell (University of Illinois Urbana-Champaign), Timothy Sherwood (University of California, Santa Barbara), Ben Hardekopf (University of California, Santa Barbara), Jonathan Balkind (University of California, Santa Barbara)
  - Control Logic Synthesis 让设计者只写 datapath sketch 并把控制位置留作 hole；工具读取 architectural specification，以 program synthesis 自动补全 state machine 或 instruction decoder，并给生成硬件保留形式化正确性保证。
  - 既有 synthesis 多生成 datapath 或要求完整 RTL；Control Logic Synthesis 把 datapath sketch 中的控制 hole 与 architecture-level behavior 对齐，自动补全且可形式验证。
  - Hardware EDA、RTL/HLS Toolchain、Hardware Verification、Simulation/Compilation

- [CRUSH: A Credit-Based Approach for Functional Unit Sharing in Dynamically Scheduled HLS](https://doi.org/10.1145/3669940.3707273)
  - Jiahui Xu (ETH Zurich), Lana Josipović (ETH Zurich)
  - CRUSH，一种能够在动态调度的 HLS 中实现高效功能单元共享并保持动态性优势的策略，并实现平均减少 12% DSP、15% FF 和 90% 优化运行时间。
  - 直接共享 dynamic-HLS functional unit 会形成资源依赖和 deadlock；CRUSH 用 credit/interaction decoupling 破除共享环，同时保留 out-of-order request 带来的动态复用机会。
  - Hardware EDA、RTL/HLS Toolchain、Hardware Verification、Simulation/Compilation

- [AMuLeT: Automated Design-Time Testing of Secure Speculation Countermeasures](https://doi.org/10.1145/3676641.3716247)
  - Bo Fu (University of Toronto), Leo Tenenbaum (University of Toronto), David Adler (University of Toronto), Assaf Klein (Technion – Israel Institute of Technology), Arpit Gogia (IMDEA Software Institute), Alaa R. Alameldeen (Simon Fraser University), Marco Guarnieri (IMDEA Software Institute), Mark Silberstein (Technion – Israel Institute of Technology), Oleksii Oleksenko (Azure Research, Microsoft), Gururaj Saileshwar (University of Toronto)
  - AMuLeT 的开发是第一个能够在模拟器设计阶段早期测试投机泄漏的安全投机对策的工具，并首次表明 SpecLFB 的开源实现是不安全的。
  - 安全推测机制通常到 RTL/芯片后期才用具体攻击验证，设计阶段缺少可自动生成关系测试的工具；关键机制是利用基于模型的关系测试工具来检测商用 CPU 中的推测泄漏，并将其应用于微架构模拟器来测试安全的推测防御。
  - 推测执行防护测试、Hardware EDA、RTL/HLS Toolchain、Hardware Verification、Simulation/Compilation

- [Don't Repeat Yourself! Coarse-Grained Circuit Deduplication to Accelerate RTL Simulation](https://doi.org/10.1145/3622781.3674184)
  - Haoyuan Wang (UC Santa Cruz), Thomas Nijssen (UC Santa Cruz), Scott Beamer (UC Santa Cruz)
  - 该工作指出共享末级缓存是影响 RTL 仿真吞吐量的主要瓶颈，并提出了一种集成到 RTL 仿真器中的粗粒度电路重复数据删除策略，通过增加代码重用来减少缓存占用空间，从而有利于缓存和分支预测器等处理器组件。
  - RTL simulator 重复展开结构相同的电路代码，导致 instruction footprint 和 LLC 压力随设计规模增长；采用一种集成到 RTL 模拟器中的粗粒度电路重复数据删除策略。
  - RTL 仿真、Hardware EDA、RTL/HLS Toolchain、Hardware Verification、Simulation/Compilation

- [Parendi: Thousand-Way Parallel RTL Simulation](https://doi.org/10.1145/3676641.3716010)
  - Mahyar Emami (EPFL), Thomas Bourgeat (EPFL), James R. Larus (EPFL)
  - Parendi 是一款 RTL 模拟器，它通过利用 RTL 模拟中固有的丰富细粒度并行性并将其有效映射到大规模并行 Graphcore IPU（智能处理单元）架构来应对这一挑战。
  - 多核 CPU 的同步与调度开销限制 RTL 并行度；Parendi 用新的 partition/compilation 把细粒度事件映射到最多 5888 个 Graphcore IPU core，并显式优化跨分区同步、通信和计算成本。
  - RTL 仿真、Hardware EDA、RTL/HLS Toolchain、Hardware Verification、Simulation/Compilation

- [Necro-reaper: Pruning away Dead Memory Traffic in Warehouse-Scale Computers](https://doi.org/10.1145/3676641.3716007)
  - Sotiris Apostolakis (Google), Chris Kennelly (Google), Xinliang David Li (Google), Parthasarathy Ranganathan (Google)
  - Necro-reaper 面向 warehouse-scale computer 中短生命周期的大块 heap allocation，识别已释放数据的无意义 writeback 和未初始化数据的无意义 fetch。Profile-guided compiler 与定制 allocator 插入新 ISA hint，硬件据此丢弃 dead traffic，无需逐 cache line 增加追踪状态。
  - 相较由硬件持续跟踪每条 cache line 生死，核心创新是利用 WSC 的垂直软硬件栈，让编译器/allocator 显式通知内存系统跳过已知无效流量。
  - Warehouse-scale Computing、Dead Memory Traffic、Profile-guided Compilation、Memory Allocator、ISA/Memory-system Co-design

- [Embracing Imbalance: Dynamic Load Shifting among Microservice Containers in Shared Clusters](https://doi.org/10.1145/3676641.3716255)
  - Shutian Luo (Yale University), Jianxiong Liao (Sun Yat-sen University,University of Macau), Chenyu Lin (University of Macau), Huanle Xu (University of Macau), Zhi Zhou (Sun Yat-sen University), Chengzhong Xu (University of Macau)
  - Imbres 面向共享集群内同一微服务多个容器的时空性能不均，不再强求负载均衡，而是根据在线 latency gradient 把请求主动移向更高效的实例，并联动 connection management 与资源 scaling。无需离线 profiling 即可快速响应，资源分配最多减少 62%。
  - 相较先均衡流量再独立 autoscale，核心创新是把可利用的实例性能不均作为优化信号，联合决定连接、请求迁移与容量。
  - 微服务调度、Dynamic Load Shifting、在线梯度、Autoscaling、SLA 保障

- [Tela: A Temporal Load-Aware Cloud Virtual Disk Placement Scheme](https://doi.org/10.1145/3669940.3707252)
  - Difan Tan (Huazhong University of Science and Technology), Jiawei Li (Huazhong University of Science and Technology), Hua Wang (Huazhong University of Science and Technology), Xiaoxiao Li (Huazhong University of Science and Technology), Wenbo Liu (Huazhong University of Science and Technology), Zijin Qin (Huazhong University of Science and Technology), Ke Zhou (Huazhong University of Science and Technology), Ming Xie (Tencent Inc.), Mengling Tao (Tencent Inc.)
  - Tela 为云块存储把每个 virtual disk 放到具体 storage warehouse，使用可解释模型预测磁盘随时间变化的 I/O pattern/value 与仓库峰值，再匹配互补负载以削峰并避免 overload。实验将过载次数降低 86.8%–93.8%。
  - 相较依据平均或当前 IOPS 静态放盘，核心创新是把磁盘和仓库未来峰值同时纳入 placement，以时间互补性而非容量余额做负载平衡。
  - Cloud Block Storage、Virtual Disk Placement、Temporal Load Prediction、Peak Shaving、过载避免

- [FleetIO: Managing Multi-Tenant Cloud Storage with Multi-Agent Reinforcement Learning](https://doi.org/10.1145/3669940.3707229)
  - Jinghan Sun (UIUC), Benjamin Reidys (UIUC), Daixuan Li (UIUC), Jichuan Chang (Google), Marc Snir (UIUC), Jian Huang (UIUC)
  - FleetIO 在可编程 SSD 上把共置租户按实时 I/O trace 区分为 latency-sensitive、bandwidth-intensive 等类型，多个传统 RL policy 依据队列/设备状态细粒度回收和再分配带宽/通道，并为各 workload type 调整 reward，在 SLO 隔离与利用率间权衡。它是存储调度用 MARL，不属于 LLM Agent。
  - 相较固定硬件隔离或弱隔离共享，核心创新是让多个 workload-specific RL controller 协同执行动态 storage harvesting；“multi-agent”指传统强化学习控制器。
  - 传统多智能体强化学习、Multi-tenant SSD、I/O 性能隔离、Storage Harvesting、SLO-aware Scheduling

- [ZRAID: Leveraging Zone Random Write Area (ZRWA) for Alleviating Partial Parity Tax in ZNS RAID](https://doi.org/10.1145/3669940.3707248)
  - Minwook Kim (Seoul National University), Seongyeop Jeong (Seoul National University), Jin-Soo Kim (Seoul National University)
  - ZRAID 在 ZNS SSD 的每个 data zone 写指针附近使用 Zone Random Write Area（ZRWA），把 incomplete stripe 的 partial parity 暂存在对应数据区并就地更新；stripe 完整后再按顺序写入，避免少量专用 parity-log zone 成为热点。
  - 旧方案把 partial parity 永久写入少量 reserved zone，造成集中写放大；ZRAID 利用新 ZRWA 的受限随机写能力，让 parity 跟随所属 data zone 临时更新，消除专用日志热点。
  - Memory/Storage Security、ZNS/DRAM Management、RowHammer Defense/Attack、虚拟化内存隔离

- [Marionette: A RowHammer Attack via Row Coupling](https://doi.org/10.1145/3669940.3707242)
  - Seungmin Baek (Seoul National University), Minbok Wi (Seoul National University), Seonyong Park (Seoul National University), Hwayong Nam (Seoul National University), Michael Jaemin Kim (Seoul National University), Nam Sung Kim (University of Illinois), Jung Ho Ahn (Seoul National University)
  - Marionette 是一种新型的 RowHammer 攻击，它利用耦合行来扩展现有的 RowHammer 攻击面，并通过向系统公开耦合行关系来探索 Marionette 的轻量级缓解方案。
  - 按物理邻接行追踪/隔离的 RowHammer 防御看不到共享 wordline、但地址相距很远的 coupled row；首先，耦合行使攻击者能够逃避两种现有的基于软件的 RowHammer 防御：基于跟踪和隔离的防御。
  - 微体系结构安全、Memory/Storage Security、ZNS/DRAM Management、RowHammer Defense/Attack、虚拟化内存隔离

- [MOAT: Securely Mitigating Rowhammer with Per-Row Activation Counters](https://doi.org/10.1145/3669940.3707278)
  - Moinuddin Qureshi (Georgia Institute of Technology), Salman Qazi (Google)
  - MOAT，一种可证明安全的设计，它使用两个内部阈值：ETH（用于缓解行的资格阈值）和 ATH（用于启动 ABO 的警报阈值），并表明配置为 ATH=64 的 MOAT 可以安全地容忍 99.7% 的 Rowhammer 阈值。
  - DDR5 PRAC+ABO 只定义框架，若内部阈值与 back-off 策略不当仍可被高激活 Jailbreak pattern 绕过；在该工作中，该方案首先表明之前的工作 Panopticon（构成 PRAC+ABO 的基础）是不安全的，因为该工作的越狱模式可能会导致 Panopticon 配置为 128 阈值的攻击行出现 1150 次激活。
  - 微体系结构安全、Memory/Storage Security、ZNS/DRAM Management、RowHammer Defense/Attack、虚拟化内存隔离

- [HyperHammer: Breaking Free from KVM-Enforced Isolation](https://doi.org/10.1145/3676641.3716002)
  - Wei Chen (Peking University), Zhi Zhang (University of Western Australia), Xin Zhang (Peking University), Qingni Shen (Peking University), Yuval Yarom (Ruhr University Bochum), Daniel Genkin (Georgia Institute of Technology), Chen Yan (Peking University), Zhe Wang (SKLP, Institute of Computing Technology, Chinese Academy of Sciences,Zhongguancun Laboratory)
  - HyperHammer 是一种 Rowhammer 攻击，它破坏了虚拟机管理程序强制执行的内存隔离，并进一步损害了虚拟机管理程序，这表明硬件辅助虚拟化并不能完全保护虚拟机管理程序，并且通过足够的工程设计，坚定的攻击者可能会实现彻底的虚拟机管理程序妥协。
  - 以往虚拟化 RowHammer 攻击多止于共置 guest，并假定 KVM/host 边界本身不会被跨越；HyperHammer 是一种 Rowhammer 攻击，它破坏了虚拟机管理程序强制执行的内存隔离，并进一步损害了虚拟机管理程序。
  - Memory/Storage Security、ZNS/DRAM Management、RowHammer Defense/Attack、虚拟化内存隔离

- [ReCA: Integrated Acceleration for Real-Time and Efficient Cooperative Embodied Autonomous Agents](https://doi.org/10.1145/3676641.3716016)
  - Zishen Wan (Georgia Institute of Technology), Yuhang Du (University of Minnesota, Twin Cities), Mohamed Ibrahim (Georgia Institute of Technology), Jiayi Qian (Georgia Institute of Technology), Jason Jabbour (Harvard University), Yang (Katie) Zhao (University of Minnesota, Twin Cities), Tushar Krishna (Georgia Institute of Technology), Arijit Raychowdhury (Georgia Institute of Technology), Vijay Janapa Reddi (Harvard University)
  - ReCA 面向多个 LLM 驱动 embodied agent 协作的长程任务，联合改变 agent 与硬件：本地模型处理降低通信/推理成本，长短期双层 memory 保存任务状态，分层集中—分散 planning 协调 agent，planning-guided multi-step execution 减少频繁重规划；GPU 承担高层规划、专用 accelerator 承担低层执行。
  - 相较只加速单次模型调用，核心创新是把多 Agent 的 memory—cooperative planning—action execution 全闭环与异构硬件共同设计，直接优化任务成功率、规划/通信延迟和扩展性。
  - Agent System、协作式具身 Agent、分层规划、长短期记忆、Planning-guided Execution、异构 Agent 加速器

- [AnA: An Attentive Autonomous Driving System](https://doi.org/10.1145/3669940.3707261)
  - Wonkyo Choe (University of Virginia), Rongxiang Wang (University of Virginia), Felix Xiaozhu Lin (University of Virginia)
  - AnA 重构自动驾驶 perception—planning 闭环：planning 通过 query interface 指明当前关注对象/区域，executor 将查询映射为最合适的感知任务，monitor 再用驾驶知识处理异常执行。系统按决策需要分配感知算力，在不牺牲安全下少用 44% 计算并更快响应对抗事件。
  - 相较感知模块固定、与驾驶决策无关地处理全场景，核心创新是让 planning 的即时信息需求反向控制 perception granularity，并保留异常监控闭环。
  - 自主驾驶系统、Planning-guided Perception、感知任务选择、异常监控、资源比例化

- [SuperNoVA: Algorithm-Hardware Co-Design for Resource-Aware SLAM](https://doi.org/10.1145/3669940.3707258)
  - Seah Kim (University of California, Berkeley), Roger Hsiao (University of California, Berkeley), Borivoje Nikolić (University of California, Berkeley), James Demmel (University of California, Berkeley), Yakun Sophia Shao (University of California, Berkeley)
  - SuperNoVA 为资源受限设备的 SLAM backend 按 latency target 动态选取图 subgraph，同时虚拟化 graph-processing hardware resource；专用架构执行选中图上的优化，在图规模、定位精度与实时 deadline 间在线平衡。
  - 固定大小 SLAM graph 只能在最坏延迟与精度间静态折中；SuperNoVA 让 subgraph construction 直接服从当前 deadline，并让虚拟化硬件按图规模供给处理资源。
  - 自主系统感知与控制、Autonomous Systems、Planning/Perception Runtime、SLAM/3D Mapping、实时资源分配

- [OctoCache: Caching Voxels for Accelerating 3D Occupancy Mapping in Autonomous Systems](https://doi.org/10.1145/3676641.3716263)
  - Peiqing Chen (University of Maryland), Minghao Li (Harvard University), Zishen Wan (Georgia Institute of Technology), Yushun Hsiao (Harvard University), Minlan Yu (Harvard University), Vijay Janapa Reddi (Harvard University), Zaoxing Liu (University of Maryland)
  - OctoCache 是一款软件系统，可通过优化的缓存访问、精细的体素排序和工作流程并行化来加速 OctoMap，凸显了 OctoCache 在提高自主导航、推进机器人技术和环境建模方面的 3D 绘图效率的潜力。
  - OctoMap 更新会反复访问离散 voxel/octree node，通用 cache layout 与串行流程产生大量慢内存访问；OctoCache，这是一个软件系统，它通过 (1) 优化的缓存内存访问、(2) 精细的体素排序和 (3) 工作流程并行化来加速 OctoMap。
  - Cache 管理、自主系统感知与控制、Autonomous Systems、Planning/Perception Runtime、SLAM/3D Mapping

- [Efficient Lossless Compression of Scientific Floating-Point Data on CPUs and GPUs](https://doi.org/10.1145/3669940.3707280)
  - Noushin Azami (Department of Computer Science, Texas State University), Alex Fallin (Department of Computer Science, Texas State University), Martin Burtscher (Department of Computer Science, Texas State University)
  - 该工作为 single/double-precision scientific floating-point data 设计四种 lossless codec，保持同一压缩格式和实现思路可在 CPU、GPU 之间互操作，同时针对并行访存与轻量变换优化 encode/decode。RTX 4090 上最快方案超过 500 GB/s，且维持较高压缩率。
  - 相较专为单一处理器调优、或用复杂模型换压缩率的方案，核心创新是让压缩表示与计算路径同时适合 CPU/GPU SIMD/SIMT，从而不以跨设备兼容性换吞吐。
  - Scientific Data Compression、Lossless Floating Point、CPU/GPU Compatibility、High-throughput Codec、存储/传输优化

- [Data Cache for Intermittent Computing Systems with Non-Volatile Main Memory](https://doi.org/10.1145/3676641.3715989)
  - Sourav Mohapatra (Department of Computer Science, TU Delft,ARM Limited), Vito Kortbeek (Department of Computer Science, TU Delft,Synopsys), Marco Antonio van Eerden (Department of Computer Science, TU Delft), Jochem Broekhoff (Department of Computer Science, TU Delft,DSP Innovation B.V.), Saad Ahmed (School of Interactive Computing, Georgia Institute of Technology), Przemysław Pawełczak (Department of Computer Science, TU Delft)
  - NACHO 通过与 WAR 检测集成来进行扩展，从而不再需要额外的内存跟踪器，并且与最先进的基于缓存的系统相比，间歇性计算运行时开销减少了 54%。
  - 既有 intermittent cache 还需独立 WAR tracker 才知道断电前必须保存哪些依赖；NACHO 把 WAR detection 合入 cache 状态本身，既减少 checkpoint 写入又删掉额外追踪器。
  - Cache 管理、Scientific/Graph Data Processing、Cache/Object-store Runtime、Data Compression/Layout、I/O Pipeline

- [Fusion: An Analytics Object Store Optimized for Query Pushdown](https://doi.org/10.1145/3669940.3707234)
  - Jianan Lu (Princeton University), Ashwini Raina (Princeton University), Asaf Cidon (Columbia University), Michael J. Freedman (Princeton University)
  - Fusion 是一种用于分析的对象存储，针对纠删码数据的查询下推进行了优化，并共同设计了其纠删码和文件放置拓扑，同时考虑到流行的分析文件格式（例如 Parquet）。
  - erasure-coded object store 做 query pushdown 时仍需跨节点重组固定 stripe，选择性查询也产生网络放大；Fusion 采用了一种条带构造算法，可以防止对象内可计算单元的碎片，并最大限度地减少擦除编码期间的存储开销。
  - 对象存储、Scientific/Graph Data Processing、Cache/Object-store Runtime、Data Compression/Layout、I/O Pipeline

- [VertexSurge: Variable Length Graph Pattern Match on Billion-edge Graphs](https://doi.org/10.1145/3622781.3674173)
  - Weiyu Xie (Department of Computer Science and Technology, Beijing National Research Center for Information Science and Technology (BNRist), Tsinghua University), MingXing Zhang (Department of Computer Science and Technology, Beijing National Research Center for Information Science and Technology (BNRist), Tsinghua University), Xia Liao (Department of Computer Science and Technology, Beijing National Research Center for Information Science and Technology (BNRist), Tsinghua University), Kang Chen (Department of Computer Science and Technology, Beijing National Research Center for Information Science and Technology (BNRist), Tsinghua University), Jinlei Jiang (Department of Computer Science and Technology, Beijing National Research Center for Information Science and Technology (BNRist), Tsinghua University), YongWei Wu (Department of Computer Science and Technology, Beijing National Research Center for Information Science and Technology (BNRist), Tsinghua University)
  - VertexSurge 为十亿边图上的 variable-length graph pattern matching 设计 VExpand operator，以面向微体系结构的 reachability-matrix 计算控制多跳扩展产生的 vertex explosion；再结合 multi-set intersection、rule-based planning 和超内存图的 disk offload 形成完整查询引擎。
  - 相较把多跳模式拆成大量 single-hop join，核心创新是把可变长度扩展做成一等物理算子，并从执行内核到查询规划共同处理不定路径长度。
  - Graph Database、Variable-length Pattern Matching、VExpand Operator、Billion-edge Graph、Query Planning/Offloading

- [Fast On-device LLM Inference with NPUs](https://doi.org/10.1145/3669940.3707239)
  - Daliang Xu (Key Lab of HCST (PKU), MOE; SCS, Peking University), Hao Zhang (Beijing University of Posts and Telecommunications), Liming Yang (Key Lab of HCST (PKU), MOE; SCS, Peking University), Ruiqi Liu (Key Lab of HCST (PKU), MOE; SCS, Peking University), Gang Huang (Key Lab of HCST (PKU), MOE; SCS, Peking University,National Key Laboratory of Data Space Technology and System), Mengwei Xu (Beijing University of Posts and Telecommunications), Xuanzhe Liu (Key Lab of HCST (PKU), MOE; SCS, Peking University)
  - llm.npu 把移动端 LLM 的 prefill 分配给 NPU、CPU/GPU：prompt 被切成保持依赖的固定长度 chunk，tensor outlier 留给 CPU/GPU 并行处理，Transformer block 再按硬件亲和性和精度敏感度乱序映射。它在端侧十亿参数模型达到超过 1000 token/s prefill，并显著降低能耗。
  - 相较把完整 LLM graph 静态编译到 NPU 或全留在 GPU，核心创新是从 prompt、tensor、block 三个层次重构工作量，使固定形状 NPU 与灵活 CPU/GPU 可协同而不过度量化。
  - 端侧 LLM 推理、NPU Offloading、Prefill 加速、Outlier 分流、异构 Block Scheduling

- [Helix: Serving Large Language Models over Heterogeneous GPUs and Network via Max-Flow](https://doi.org/10.1145/3669940.3707215)
  - Yixuan Mei (Carnegie Mellon University), Yonghao Zhuang (Carnegie Mellon University), Xupeng Miao (Carnegie Mellon University), Juncheng Yang (Carnegie Mellon University), Zhihao Jia (Carnegie Mellon University), Rashmi Vinayak (Carnegie Mellon University)
  - Helix 在异构 GPU 与异构网络组成的集群上，把 GPU instance 建模为节点、算力与链路带宽建模为容量，将 LLM layer placement 和 request routing 联合转化为 max-flow/MILP。它针对具体模型、GPU 型号和拓扑输出部署与在线调度策略，24–42 节点上吞吐最多提高 3.3 倍。
  - 相较先做模型切分、再独立做请求路由，核心创新是用同一有向容量图表达计算与网络瓶颈，联合求解强耦合的 layer placement 和流量调度。
  - LLM Serving、异构 GPU 集群、Model Placement、Request Routing、Max-flow/MILP、网络感知调度

- [FlexSP: Accelerating Large Language Model Training via Flexible Sequence Parallelism](https://doi.org/10.1145/3676641.3715998)
  - Yujie Wang (Peking University), Shiju Wang (Beihang University), Shenhan Zhu (Peking University), Fangcheng Fu (Peking University), Xinyi Liu (Peking University), Xuefeng Xiao (ByteDance Inc.), Huixia Li (ByteDance Inc.), Jiashi Li (ByteDance Inc.), Faming Wu (ByteDance Inc.), Bin Cui (Peking University)
  - FlexSP 针对 LLM 长上下文训练中每个 batch 的 sequence length 呈长尾分布，在每个 training step 读取实际长度组合，并用线性规划为不同序列选择不同 scatter/sequence-parallel strategy；高效 solver 将方案落入分布式训练 runtime，避免短序列跟随最长序列过度通信。
  - 相较整个训练固定一种 sequence-parallel degree/切分方式，核心创新是把序列异质性提升为 step 级优化输入，为同批不同长度自适应组合并行策略。
  - LLM Training、Long-context Training、Sequence Parallelism、长度异质性、Step-level Linear Programming

- [Spindle: Efficient Distributed Training of Multi-Task Large Models via Wavefront Scheduling](https://doi.org/10.1145/3676641.3715992)
  - Yujie Wang (Peking University), Shenhan Zhu (Peking University), Fangcheng Fu (Peking University), Xupeng Miao (Purdue University), Jie Zhang (Alibaba Group), Juan Zhu (Alibaba Group), Fan Hong (Alibaba Group), Yong Li (Alibaba Group), Bin Cui (Peking University)
  - Spindle 服务共享 base model、含多个 task/modality-specific component 的多任务多模态大模型训练。它把执行分解成 wave，依次求解异质 workload parallelization 与 dependency-driven schedule，让不同任务/模态的可并行部分跨设备重叠。
  - 相较把多任务模型按单一静态 pipeline 执行，核心创新是以 wavefront 顺序化原本巨大的联合搜索，同时保留任务异质性与依赖带来的并行机会。
  - 多任务多模态模型、分布式训练、Wavefront Scheduling、异质 Workload Parallelism、依赖感知执行

- [Vela: A Virtualized LLM Training System with GPU Direct RoCE](https://doi.org/10.1145/3676641.3716280)
  - Apoorve Mohan (IBM Research), Robert Walkup (IBM Research), Bengi Karacali (IBM Research), Ming-Hung Chen (IBM Research), Abdullah Kayi (IBM Research), Liran Schour (IBM), Shweta Salaria (IBM Research), Sophia Wen (IBM Research), IHsin Chung (IBM Research), Abdul Alim (IBM Research), Constantinos Evangelinos (IBM Research), Lixiang Luo (IBM Research), Marc Dombrowa (IBM Research), Laurent Schares (IBM Research), Ali Sydney (IBM Research), Pavlos Maniotis (IBM Research), Sandhya Koteshwara (IBM Research), Brent Tang (IBM), Joel Belog (IBM), Rei Odaira (IBM), Vasily Tarasov (IBM Research), Eran Gampel (IBM Cloud), Drew Thorstensen (IBM), Talia Gershon (IBM Research), Seetharami Seelam (IBM Research)
  - Vela 是 IBM Cloud 用现成 A100、Linux KVM 与虚拟 RoCE 构建的云原生 LLM 训练平台，VM 内 GPU 可经 SR-IOV NIC 做 peer-to-peer DMA。论文总结约 2.5 年设计运营经验，并验证 1500 GPU 规模训练 500 亿参数 decoder 时达到约理想吞吐的 80%。
  - 相较依赖裸机和专用互连的训练集群，核心贡献是证明通用虚拟化与 RoCE 也能在千卡规模接近高效运行，并公开隔离、网络和运维瓶颈的生产经验。
  - LLM Training Platform、GPU 虚拟化、RoCE/SR-IOV、千卡集群、Production Experience

- [Forecasting GPU Performance for Deep Learning Training and Inference](https://doi.org/10.1145/3669940.3707265)
  - Seonho Lee (Georgia Institute of Technology), Amar Phanishayee (Meta), Divya Mahajan (Georgia Institute of Technology)
  - NeuSight 在目标 model 或 GPU 尚不可执行/尚未获得时预测训练与推理性能。它不直接用一个黑盒模型回归整 kernel latency，而按 GPU 执行结构拆成 tile，以性能定律给出上下界、ML 预测 tile，再聚合到 kernel 和端到端模型；对未见 GPT-3/H100 的误差显著低于既有方法。
  - 相较用历史 model×GPU 样本直接黑盒外推，核心创新是把学习问题嵌入硬件执行分解和解析边界，使对“新模型、新 GPU、两者皆新”仍可泛化。
  - GPU 性能预测、DL 训推建模、Tile-level Model、解析模型+机器学习、跨硬件泛化

- [MVQ: Towards Efficient DNN Compression and Acceleration with Masked Vector Quantization](https://doi.org/10.1145/3669940.3707268)
  - Shuaiting Li (Zhejiang University), Chengxuan Wang (Zhejiang University), Juncan Deng (Zhejiang University), Zeyu Wang (Zhejiang University), Zewen Ye (Zhejiang University), Zongsheng Wang (Zhejiang University), Haibin Shen (Zhejiang University), Kejie Huang (Zhejiang University)
  - MVQ 先用 N:M pruning 移除不重要 weight，再用 masked k-means 只对保留 weight 与 codeword 计算聚类误差；配套 accelerator 采用 enhanced weight-stationary dataflow 和 sparse systolic array，联合减少模型存储、weight loading 与无效乘加。
  - 相较标准 vector quantization 平等逼近所有权重，核心创新是把重要性 mask 同时用于 codebook 学习和稀疏硬件执行，以有限 codeword 优先保存关键权重。
  - DNN Compression、Masked Vector Quantization、N:M Pruning、Sparse Systolic Array、Algorithm-hardware Co-design

- [PartIR: Composing SPMD Partitioning Strategies for Machine Learning](https://doi.org/10.1145/3669940.3707284)
  - Sami Alabed (Google DeepMind), Daniel Belov (Google DeepMind), Bart Chrzaszcz (Google DeepMind), Juliana Franco (Google DeepMind), Dominik Grewe (Google DeepMind), Dougal Maclaurin (Google DeepMind), James Molloy (Google DeepMind), Tom Natan (Google DeepMind), Tamara Norman (Google DeepMind), Xiaoyue Pan (Google DeepMind), Adam Paszke (Google DeepMind), Norman Alexander Rink (Google DeepMind), Michael Schaarschmidt (Isomorphic Labs), Timur Sitdikov (Google DeepMind), Agnieszka Swietlik (Google DeepMind), Dimitrios Vytiniotis (Google DeepMind), Joel Wee (Google DeepMind)
  - PartIR 是一种与硬件和运行时无关的神经网络分区系统，它利用类似调度的 API，在每个策略之后逐步重写 ML 程序中间表示 (IR)，从而允许模拟器和用户验证策略的性能。
  - 大模型并行策略与具体框架/运行时耦合，data、model、optimizer sharding 难以组合并验证中间结果；为了解决这些策略日益复杂的问题，该工作引入了 PartIR，一种与硬件和运行时无关的神经网络分区系统。
  - SPMD Partitioning Compiler、Composable Sharding、IR Incremental Rewrite、Data/Model/Optimizer Parallelism、硬件/运行时解耦

- [Using Analytical Performance/Power Model and Fine-Grained DVFS to Enhance AI Accelerator Energy Efficiency](https://doi.org/10.1145/3669940.3707231)
  - Zibo Wang (State Key Laboratory for Novel Software Technology, Nanjing University), Yijia Zhang (Peng Cheng Laboratory), Fuchun Wei (Huawei Technologies Co., Ltd), Bingqiang Wang (Peng Cheng Laboratory), Yanlin Liu (Huawei Technologies Co., Ltd), Zhiheng Hu (Huawei Technologies Co., Ltd), Jingyi Zhang (Huawei Technologies Co., Ltd), Xiaoxin Xu (Huawei Technologies Co., Ltd), Jian He (Huawei Technologies Co., Ltd), Xiaoliang Wang (State Key Laboratory for Novel Software Technology, Nanjing University), Wanchun Dou (State Key Laboratory for Novel Software Technology, Nanjing University), Guihai Chen (State Key Laboratory for Novel Software Technology, Nanjing University), Chen Tian (State Key Laboratory for Novel Software Technology, Nanjing University)
  - 该方案为 Ascend NPU 每个 operator 建立频率—cycle 的凸分段线性模型和含温度项的 power model，再先分类/预处理 operator、用 genetic search 选择毫秒级 DVFS 频率；GPT-3 训练等 workload 上把 AICore 功耗降 13.44%，性能损失限制在 1.76%。
  - 粗粒度 DVFS 无法利用相邻 operator 的频率敏感度差异；该方案以 operator 级解析模型约束 genetic search，让每次调频同时满足性能与温度相关功耗目标。
  - Operator-level DVFS、Ascend NPU、Performance/Power Modeling、Genetic Search、AI 加速器能效

- [Early Termination for Hyperdimensional Computing Using Inferential Statistics](https://doi.org/10.1145/3669940.3707254)
  - Pu (Luke) Yi (Stanford University), Yifan Yang (Stanford University), Chae Young Lee (Stanford University), Sara Achour (Stanford University)
  - Omen，这是第一个动态 HDC 优化器，它使用推理统计提前终止推理，同时提供准确性保证，并开发了 HDC 的统计视图，将 HD 计算重新构建为统计采样和测试任务，从而支持统计测试的使用。
  - HDC early termination 依赖经验阈值，可能过早损害准确率或过晚浪费计算，且没有统计保证；Omen，这是第一个动态 HDC 优化器，它使用推理统计提前终止推理，同时提供准确性保证。
  - Hyperdimensional Computing、ML Training/Inference Runtime、模型并行与压缩、AI Accelerator Control、能效/吞吐建模

- [Saving Energy with Per-Variable Bitwidth Speculation](https://doi.org/10.1145/3676641.3716271)
  - Tommy McMichen (Northwestern University), David Dlott (Northwestern University), Panitan Wongse-ammat (Northwestern University), Nathan Greiner (Northwestern University), Hussain Khajanchi (Northwestern University), Russ Joseph (Northwestern University), Simone Campanoni (Northwestern University)
  - BitSpec，这是一个对程序变量的位宽进行细粒度推测的系统，并作为编译器架构协同设计实现，其中编译器透明地将程序变量的位宽减少到其预期需求，并且硬件监视推测变量。
  - 编译器照搬源码整数位宽，而多数变量在绝大多数执行时间只使用其中少量 bit；为了利用这个机会，采用 BitSpec：一个对程序变量的位宽进行细粒度推测的系统。
  - 能耗/功率/温度管理、CPU/GPU Microarchitecture、Front-end/Cache/Atomic、Speculative Execution、硬件运行时控制

- [ShadowLoad: Injecting State into Hardware Prefetchers](https://doi.org/10.1145/3676641.3716020)
  - Lorenz Hetterich (CISPA Helmholtz Center for Information Security), Fabian Thomas (CISPA Helmholtz Center for Information Security), Lukas Gerlach (CISPA Helmholtz Center for Information Security), Ruiyi Zhang (CISPA Helmholtz Center for Information Security), Nils Bernsdorf (CISPA Helmholtz Center for Information Security), Eduard Ebert (CISPA Helmholtz Center for Information Security), Michael Schwarz (CISPA Helmholtz Center for Information Security)
  - ShadowLoad，一种新的攻击原语，通过将状态注入硬件预取器，将不可访问的受害者数据带入缓存，并演示了 FetchProbe，一种跨步预取器侧通道攻击，泄漏具有子缓存行粒度的内存访问偏移量，扩展了之前关于控制流泄漏的工作。
  - 既有 prefetcher side channel 主要读取已被 victim 访问的数据，难以主动把不可访问地址带入 cache；ShadowLoad 是一种新的攻击原语，通过将状态注入到硬件预取器中，将无法访问的受害者数据带入缓存。
  - CPU/GPU Microarchitecture、Front-end/Cache/Atomic、Speculative Execution、硬件运行时控制

- [Skia: Exposing Shadow Branches](https://doi.org/10.1145/3676641.3716273)
  - Chrysanthos Pepi (Texas A&M University,Intel), Bhargav Reddy Godala (Princeton University,Intel), Krishnam Tibrewala (Texas A&M University), Gino A. Chacon (Intel,AheadComputing), Paul V. Gratz (Texas A&M University), Daniel A. Jiménez (Texas A&M University,Barcelona Supercomputing Center), Gilles A. Pokam (Intel), David I. August (Princeton University)
  - Skia 是一种影子分支解码技术，可识别并解码 FDIP 获取的缓存行中未使用的字节，将它们插入到影子分支缓冲区 (SBB) 中，从而允许 FDIP 在 BTB 未命中的情况下进行推测。
  - FDIP 遇到 BTB miss 时只看已识别 branch，已取回 cache line 中尚未解码的 branch byte 被浪费；该方案将缓存行被忽略部分中存在的分支指令称为“影子分支”。在这里，该工作介绍 Skia，这是一种影子分支解码技术，它可以识别并解码 FDIP 获取的缓存行中未使用的字节，并将它们插入到影子分支缓冲区 (SBB) 中。
  - CPU/GPU Microarchitecture、Front-end/Cache/Atomic、Speculative Execution、硬件运行时控制

- [Hierarchical Prefetching, A Software-Hardware Instruction Prefetcher for Server Applications](https://doi.org/10.1145/3676641.3716260)
  - Tingji Zhang (Tsinghua University), Boris Grot (University of Edinburgh,Huawei Research), Wenjian He (Huawei Technologies Co., Ltd.), Yashuai Lv (Huawei Technologies Co., Ltd.), Peng Qu (Tsinghua University), Fang Su (Huawei Technologies Co., Ltd.), Wenxin Wang (Tsinghua University), Guowei Zhang (Huawei Technologies Co., Ltd.), Xuefeng Zhang (Tsinghua University), Youhui Zhang (Tsinghua University,Zhongguancun National Laboratory)
  - Hierarchical Prefetching 由软件分析识别几十到数百 KB、对应完整程序功能的 instruction Bundle，把 Bundle 边界和大部分元数据放在内存中；硬件只用不足 2 KB 状态预测并回放当前 Bundle。即使 Bundle 内细粒度控制流变化，也能提前取回整段相关指令。
  - 相较依赖精确 branch/path history 的 cache-line 级预取，核心创新是预测语义更稳定的粗粒度功能块，并把庞大元数据下沉到内存，以很小硬件预算覆盖更大的 instruction footprint。
  - Instruction Prefetching、Hierarchical Bundles、Software/Hardware Co-design、I-cache Miss、低元数据硬件

- [Bounding Speculative Execution of Atomic Regions to a Single Retry](https://doi.org/10.1145/3622781.3674176)
  - Eduardo José Gómez-Hernández (Computer Engineering Department, University of Murcia), Juan M. Cebrian (Computer Engineering Department, University of Murcia), Stefanos Kaxiras (Department of Information Technology, Uppsala University), Alberto Ros (Computer Engineering Department, University of Murcia)
  - 关键机制是，在重新执行时访问完全相同的地址集的 AR 可以在第一次执行中了解该地址集，并通过执行有序的缓存行锁定在下一次执行中非推测性地执行。
  - 固定次数 blind retry 无法保证事务何时成功；cleAR 在第一次执行学习 atomic region 的完整地址集合，首次 abort 后按全序锁住这些 cache line，使下一次转为非推测执行并把 retry 上界收紧为一次。
  - CPU/GPU Microarchitecture、Front-end/Cache/Atomic、Speculative Execution、硬件运行时控制

- [Formalising CXL Cache Coherence](https://doi.org/10.1145/3676641.3715999)
  - Chengsong Tan (Kaihong), Alastair F. Donaldson (Imperial College London), John Wickerson (Imperial College London)
  - Isabelle 证明助手用于为 CXL.cache 创建正式模型，CXL.cache 是 Compute Express Link 标准的设备间缓存一致性协议，基于英语散文规范，但该规范的多个部分不清楚、不明确或不准确。
  - prose 规范只能靠人工解释协议边角；该工作将 CXL.cache 转写为 Isabelle model，以 scenario validation 校准语义并机械化证明 coherence，同时把发现的歧义反馈给 CXL consortium。
  - CXL 内存/互连、Cache 管理、形式化验证、CXL Memory System、Coherence/Persistence

- [CtXnL: A Software-Hardware Co-Designed Solution for Efficient CXL-Based Transaction Processing](https://doi.org/10.1145/3676641.3716244)
  - Zhao Wang (Peking University, School of Integrated Circuits,Peking University, School of Computer Science), Yiqi Chen (Peking University, School of Integrated Circuits), Cong Li (Peking University, School of Integrated Circuits), Yijin Guan (Alibaba Group, DAMO Academy,Hupan Lab), Dimin Niu (Alibaba Group, DAMO Academy,Hupan Lab), Tianchan Guan (Alibaba Group, DAMO Academy,Hupan Lab), Zhaoyang Du (Alibaba Group, DAMO Academy,Hupan Lab), Xingda Wei (Shanghai Jiao Tong University, Institute of Parallel and Distributed Systems, SEIEE), Guangyu Sun (Peking University, School of Integrated Circuits,Beijing Advanced Innovation Center for Integrated Circuits)
  - CtXnL 用 CXL shared memory 承载多节点 OLTP，但不对所有 transactional data 强制同一种 coherence；software 标注需要同步的对象/阶段，hardware 提供可选择的 hybrid coherence primitive，最高把吞吐提高到 vanilla CXL 的 2.08 倍。
  - vanilla CXL 对所有共享事务数据维持强 cache coherence，协议流量抵消低延迟优势；CtXnL 暴露 hybrid primitive，让数据库按数据语义选择哪些对象/阶段真正需要一致。
  - CXL 内存/互连、CXL Memory System、Coherence/Persistence、Tiered-memory Migration、CXL Performance Characterization

- [ByteFS: System Support for (CXL-based) Memory-Semantic Solid-State Drives](https://doi.org/10.1145/3669940.3707250)
  - Shaobo Li (University of Illinois Urbana-Champaign), Yirui (Eric) Zhou (University of Illinois Urbana-Champaign), Hao Ren (University of Illinois Urbana-Champaign), Jian Huang (University of Illinois Urbana-Champaign)
  - ByteFS 为 PCIe/CXL memory-semantic SSD 同时保留 byte 与 block persistence path：扩展文件系统数据结构支持双粒度访问，把 SSD DRAM 组织成 log 合并细粒度写，并协调 host page cache 与 device cache；实际设备上最高加速 2.7 倍、写流量降 5.1 倍。
  - 传统 NVM file system 或 block SSD stack 只能发挥一种接口；ByteFS 让 byte write、block transfer、device log/coalescing 和两级 cache 在同一路径协同。
  - CXL 内存/互连、CXL Memory System、Coherence/Persistence、Tiered-memory Migration、CXL Performance Characterization

- [M5: Mastering Page Migration and Memory Management for CXL-based Tiered Memory Systems](https://doi.org/10.1145/3676641.3711999)
  - Yan Sun (University of Illinois Urbana-Champaign), Jongyul Kim (University of Illinois Urbana-Champaign), Zeduo Yu (University of Illinois Urbana-Champaign), Jiyuan Zhang (University of Illinois Urbana-Champaign), Siyuan Chai (University of Illinois Urbana-Champaign), Michael Jaemin Kim (Seoul National University), Hwayong Nam (Seoul National University), Jaehyun Park (Seoul National University), Eojin Na (Seoul National University), Yifan Yuan (Intel Labs), Ren Wang (Intel Labs), Jung Ho Ahn (Seoul National University), Tianyin Xu (University of Illinois Urbana-Champaign), Nam Sung Kim (University of Illinois Urbana-Champaign)
  - M5 在 CXL controller 中透明统计每个 4 KB page 及其中 64 B word 的访问，区分真正 hot page、被误判的 warm page，以及只有少数字热门的 sparse-hot page；硬件 hot-page/hot-word tracker 为 migration policy 提供信号，平均识别多 47% 热页并提升 14% 性能。
  - 相较 CPU sampling 只见粗粒度访问且自身干扰应用，核心创新是把 page/word heat measurement 下沉到 CXL 数据路径，为分层内存迁移提供低开销、双粒度 ground truth。
  - CXL Tiered Memory、Page Migration、Hot-page/Hot-word Tracking、CXL Controller、Memory Profiling

- [Systematic CXL Memory Characterization and Performance Analysis at Scale](https://doi.org/10.1145/3676641.3715987)
  - Jinshu Liu (Virginia Tech), Hamid Hadian (Virginia Tech), Yuyue Wang (Virginia Tech), Daniel S. Berger (Microsoft and University of Washington), Marie Nguyen (Samsung), Xun Jian (Virginia Tech), Sam H. Noh (Virginia Tech), Huaicheng Li (Virginia Tech)
  - Melody 是一个用于系统表征和分析 CXL 内存性能的框架，并产生了许多见解：工作负载对亚μs CXL 延迟的敏感性、CXL 尾部延迟的首次披露、CPU 对 CXL 延迟的容忍度、用于查明 CXL 瓶颈的新颖方法 (SPA) 以及 CXL 下 CPU 预取器的低效率。
  - 单设备微基准无法外推 CXL 部署；Melody 统一横跨 265 个 workload、4 个真实设备、7 档延迟和 5 类 CPU，并用 SPA 将端到端 slowdown 归因到具体 CXL 瓶颈。
  - CXL 内存/互连、CXL Memory System、Coherence/Persistence、Tiered-memory Migration、CXL Performance Characterization

- [MoE-Lightning: High-Throughput MoE Inference on Memory-constrained GPUs](https://doi.org/10.1145/3669940.3707267)
  - Shiyi Cao (UC Berkeley), Shu Liu (UC Berkeley), Tyler Griggs (UC Berkeley), Peter Schafhalter (UC Berkeley), Xiaoxuan Liu (UC Berkeley), Ying Sheng (Stanford University), Joseph E. Gonzalez (UC Berkeley), Matei Zaharia (UC Berkeley), Ion Stoica (UC Berkeley)
  - MoE-Lightning 让 Mixtral 等 MoE 在显存受限的低成本 GPU 上做 batch inference：paged expert weight 跨 SSD/CPU/GPU 流动，CGOPipe 将 I/O、CPU 管理和 GPU 计算流水化；Hierarchical Roofline Model 根据各层带宽/算力选择 batch 与 offload policy，单 T4 上吞吐最高提升 10.3 倍。
  - 相较沿用 dense-model 的逐层 offload pipeline，核心创新是针对稀疏 expert activation 建模三级资源上限，并让分页权重与 CPU-GPU-I/O schedule 共同逼近吞吐上界。
  - MoE 推理、显存受限 GPU、Expert Weight Offloading、CPU-GPU-I/O Pipeline、Hierarchical Roofline

- [FSMoE: A Flexible and Scalable Training System for Sparse Mixture-of-Experts Models](https://doi.org/10.1145/3669940.3707272)
  - Xinglin Pan (The Hong Kong University of Science and Technology (Guangzhou)), Wenxiang Lin (Harbin Institute of Technology, Shenzhen), Lin Zhang (Hong Kong University of Science and Technology), Shaohuai Shi (Harbin Institute of Technology, Shenzhen), Zhenheng Tang (The Hong Kong University of Science and Technology), Rui Wang (The Hong Kong University of Science and Technology (Guangzhou)), Bo Li (Hong Kong University of Science and Technology), Xiaowen Chu (The Hong Kong University of Science and Technology (Guangzhou),Hong Kong University of Science and Technology)
  - FSMoE 将 token routing、all-to-all communication、expert compute 与 gradient aggregation 抽象成可 profiling 的任务图，跨不同 MoE routing 实现统一调度；它共同安排节点内/节点间通信与计算，并按运行状态自适应切分 gradient 形成流水。
  - 相较为某一种 MoE 实现手写固定 overlap，核心创新是统一模块抽象加在线 profiling，让 task scheduler 可跨 routing function 和 cluster topology 自动组合通信—计算流水。
  - MoE Training、Task-graph Scheduling、Communication-computation Overlap、Adaptive Gradient Partitioning、在线 Profiling

- [CoServe: Efficient Collaboration-of-Experts (CoE) Model Inference with Limited Memory](https://doi.org/10.1145/3676641.3715986)
  - Jiashun Suo (State Key Laboratory of CCSE and School of Computer Science and Engineering, Beihang University), Xiaojian Liao (State Key Laboratory of CCSE and School of Computer Science and Engineering, Beihang University), Limin Xiao (State Key Laboratory of CCSE and School of Computer Science and Engineering, Beihang University), Li Ruan (State Key Laboratory of CCSE and School of Computer Science and Engineering, Beihang University), Jinquan Wang (State Key Laboratory of CCSE and School of Computer Science and Engineering, Beihang University), Xiao Su (State Key Laboratory of CCSE and School of Computer Science and Engineering, Beihang University), Zhisheng Huo (State Key Laboratory of CCSE and School of Computer Science and Engineering, Beihang University)
  - CoServe 在 CPU/GPU/存储层级内服务由多个小 expert model 协作完成一个请求的 CoE。它从 expert dependency 预测后续调用，依此重排 request、保留/换入相关 expert，并离线搜索各处理器资源配额，减少有限内存下的频繁 model switching。
  - 相较把 CoE 当作互不相关的模型调用逐个换入，核心创新是把 expert 间工作流依赖同时用于请求调度和模型驻留管理。
  - Compound AI Workflow、Collaboration-of-Experts、Dependency-aware Scheduling、Expert Cache、异构 CPU/GPU

- [Klotski: Efficient Mixture-of-Expert Inference via Expert-Aware Multi-Batch Pipeline](https://doi.org/10.1145/3676641.3716261)
  - Zhiyuan Fang (Sun Yat-sen University), Yuegui Huang (Sun Yat-sen University), Zicong Hong (Hong Kong University of Science and Technology), Yufeng Lyu (Huawei Technologies Co. Ltd), Wuhui Chen (Sun Yat-sen University,Peng Cheng Laboratory), Yue Yu (Peng Cheng Laboratory), Fan Yu (Huawei Technologies Co. Ltd), Zibin Zheng (Sun Yat-sen University)
  - Klotski 为 offloaded MoE inference 同时运行多个 batch，以当前层计算覆盖下一层 expert 从 CPU/disk 加载；planner 根据不同 batch 激活 expert 的重合、各 expert 计算/I/O 时长编排 batch 顺序，prefetcher 再利用激活相关性预取，避免 batch 越多反而加载更多 expert。
  - 相较直接套用 dense LLM 的 multi-batch pipeline，核心创新是让 pipeline 明确感知稀疏 expert activation，以计算—I/O 平衡而非固定 batch 数消除 bubble。
  - MoE 推理、Expert Offloading、Multi-batch Pipeline、Activation-aware Prefetch、I/O-Compute Overlap

- [MoC-System: Efficient Fault Tolerance for Sparse Mixture-of-Experts Model Training](https://doi.org/10.1145/3676641.3716006)
  - Weilin Cai (The Hong Kong University of Science and Technology (Guangzhou)), Le Qin (The Hong Kong University of Science and Technology (Guangzhou)), Jiayi Huang (The Hong Kong University of Science and Technology (Guangzhou))
  - MoC-System 管理万卡 MoE 训练产生的大量 checkpoint shard：Partial Experts Checkpointing 只保存策略选出的部分 expert，其余可从共享/冗余状态恢复；fully-sharded 写入均分各 rank 负载，两级管理把内存 snapshot 与持久化异步流水化。
  - 相较像 dense model 一样保存全部 MoE 参数，核心创新是利用 expert 稀疏与可恢复性选择性持久化，把 checkpoint 体量压回 dense-model 量级。
  - MoE Training、Partial Expert Checkpoint、分布式容错、Asynchronous Persistence、Megatron-DeepSpeed

- [Concerto: Automatic Communication Optimization and Scheduling for Large-Scale Deep Learning](https://doi.org/10.1145/3669940.3707223)
  - Shenggan Cheng (National University of Singapore), Shengjie Lin (Georgia Institute of Technology), Lansong Diao (Alibaba Group), Hao Wu (George Mason University), Siyu Wang (Alibaba Group), Chang Si (Alibaba Group), Ziming Liu (National University of Singapore), Xuanlei Zhao (National University of Singapore), Jiangsu Du (Sun Yat-sen University), Wei Lin (Alibaba Group), Yang You (National University of Singapore)
  - Concerto 将大规模训练的 collective/point-to-point communication 与 compute 组成 resource-constrained project scheduling，自动分解关键同步通信以制造 overlap，再由通用 solver 求近优执行顺序。它与 model/data/pipeline parallelism 解耦，可匹配或超过 Megatron-LM、JAX/XLA、DeepSpeed、Alpa 的手工通信优化。
  - 相较每种并行框架内嵌专用 overlap schedule，核心创新是用独立 compiler IR 和通用约束调度器自动生成跨并行策略的通信优化。
  - Distributed DL Training、Communication Scheduling、Compiler Automation、Compute-Communication Overlap、RCPSP

- [Design and Operation of Shared Machine Learning Clusters on Campus](https://doi.org/10.1145/3669940.3707266)
  - Kaiqiang Xu (Hong Kong University of Science and Technology), Decang Sun (Hong Kong University of Science and Technology), Hao Wang (Hong Kong University of Science and Technology), Zhenghang Ren (Hong Kong University of Science and Technology), Xinchen Wan (Hong Kong University of Science and Technology), Xudong Liao (Hong Kong University of Science and Technology), Zilong Wang (Hong Kong University of Science and Technology), Junxue Zhang (Hong Kong University of Science and Technology), Kai Chen (Hong Kong University of Science and Technology)
  - SING 是面向大学共享 GPU cluster 的全栈平台，从 bare-metal/configuration、身份与配额、job scheduling 到 usage/incident management 分四层组织，并总结有限运维人力下的真实使用模式与故障处置。目标不是提出单个 scheduler，而是降低长期维护成本并提高公平共享与设备利用率。
  - 相较只用通用 Kubernetes/Slurm 拼装校园集群，核心贡献是把部署、用户治理、调度和运维观测作为统一可扩展系统，并提供长期运行经验和开源资源。
  - Shared ML Cluster、Campus GPU Infrastructure、Multi-user Scheduling、运维与事件管理、Production Experience

- [PCcheck: Persistent Concurrent Checkpointing for ML](https://doi.org/10.1145/3669940.3707255)
  - Foteini Strati (ETH Zurich), Michal Friedman (ETH Zurich), Ana Klimovic (ETH Zurich)
  - PCcheck 在训练继续推进时异步抓取 model/optimizer state，并把持久化流水线并行写入本地 SSD、持久内存或分布式存储；训练线程只承担短暂快照动作，后台完成格式转换与 I/O。高频到每 10 个 iteration 保存一次时，端到端训练开销约 3%。
  - 相较同步 checkpoint 让所有 worker 等待慢速持久化，核心创新是把一致状态捕获与实际写盘解耦，使细粒度容错频率不再直接受存储延迟限制。
  - 分布式训练检查点、Asynchronous Persistence、SSD/PMEM、训练容错、高频快照

- [Tally: Non-Intrusive Performance Isolation for Concurrent Deep Learning Workloads](https://doi.org/10.1145/3669940.3707282)
  - Wei Zhao (Stanford University,CentML), Anand Jayarajan (University of Toronto,Vector Institute), Gennady Pekhimenko (University of Toronto,Vector Institute)
  - Tally，一种非侵入式 GPU 共享机制，可提供强大的性能隔离和全面的工作负载兼容性，并证明当与尽力而为训练工作负载同时执行时，它在高优先级推理任务的 99% 延迟上产生的平均开销仅为 7.2%。
  - 现有 GPU 共享要修改应用/kernel、限制 API，或只能给弱隔离，难以兼容任意 DL workload；该工作引入了 Tally，一种非侵入式 GPU 共享机制，可提供强大的性能隔离和全面的工作负载兼容性。
  - GPU 共享、非侵入式 Kernel Interposition、并发 DL Workload、强性能隔离、CUDA 兼容性

- [Load and MLP-Aware Thread Orchestration for Recommendation Systems Inference on CPUs](https://doi.org/10.1145/3676641.3716003)
  - Rishabh Jain (The Pennsylvania State University), Teyuh Chou (Advanced Micro Devices, Inc.), Onur Kayiran (Advanced Micro Devices, Inc.), John Kalamatianos (Advanced Micro Devices, Inc.), Gabriel H. Loh (Advanced Micro Devices, Inc.), Mahmut T. Kandemir (The Pennsylvania State University), Chita R. Das (The Pennsylvania State University)
  - Balance 服务 CPU 上的 DLRM inference：按 embedding table 特征只分配足够 core，并用 memory-level-parallelism-aware task order 吃满带宽；work stealing 与 table reordering 再修复 chiplet 间负载失衡，96 核上最高加速 1.67 倍。
  - 平均分核或只按 table size 调度会同时损失 core occupancy、MLP 和 chiplet balance；Balance 把最小分核、MLP-aware ordering、work stealing 与 table reorder 合为一个 thread scheduler。
  - DLRM Inference、CPU Thread Orchestration、MLP-aware Scheduling、Embedding Table、Chiplet Load Balance

- [Validating JVM Compilers via Maximizing Optimization Interactions](https://doi.org/10.1145/3622781.3674188)
  - Zifan Xie (Huazhong University of Science and Technology), Ming Wen (Huazhong University of Science and Technology), Shiyu Qiu (Huazhong University of Science and Technology), Hai Jin (Huazhong University of Science and Technology)
  - MopFuzzer 在同一代码位置连续组合 13 类 Java program mutator，并读取 JVM optimization profile，引导样例触发 inlining、loop unrolling、dead-code elimination 等多 pass 之间的交互；再对 OpenJDK 与 OpenJ9 做差分执行，得到 59 个有效缺陷报告。
  - 相较让每个变异只覆盖单一优化 pass，核心创新是把跨优化阶段的组合交互作为搜索目标，并用运行时 profile 而非纯语法覆盖反馈引导变异。
  - JVM Compiler Fuzzing、Optimization-profile Guidance、Mutation Composition、Differential Testing、OpenJDK/OpenJ9

- [Faster Chaitin-like Register Allocation via Grammatical Decompositions of Control-Flow Graphs](https://doi.org/10.1145/3669940.3707286)
  - Xuran Cai (Hong Kong University of Science and Technology), Amir Kafshdar Goharshady (University of Oxford), S. Hitarth (Hong Kong University of Science and Technology), Chun Kit Lam (Hong Kong University of Science and Technology)
  - 该工作基于一种语法设计了一种新的但自然的图分解概念，该语法精确地捕获了可以实现为程序 CFG 的图集，并为 Chaitin 定义的寄存器分配经典问题的两种变体提供了渐近更有效的算法。
  - 通用 Chaitin-style register allocation 在真实 CFG 上搜索代价高，精确方法又难扩展到无 spill 的工程实例；对于此类架构，该工作的方法是第一个精确的算法，可以扩展以解决无溢出寄存器分配的现实世界实例。
  - 编译器与代码生成、Compiler Algorithms、IR/Scheduling Transformation、Code Generation/Reassembly、Compiler Search

- [Towards Sound Reassembly of Modern x86-64 Binaries](https://doi.org/10.1145/3676641.3716026)
  - Hyungseok Kim (The Affiliated Institute of ETRI), Soomin Kim (KAIST), Sang Kil Cha (KAIST)
  - SURI 对现代 x86-64 binary 做可靠 reassembly：利用 CET 带来的代码属性精确符号化动态计算 pointer，并对 indirect-branch target 取安全上界，因而能在不改语义时覆盖所有 memory reference；评估包含 9,600 个真实 binary。
  - 保守 binary reassembly 要么漏掉动态 pointer、要么过度改写；SURI 利用 CET 精确约束 computed pointer，并用 indirect-target over-approximation 保证引用完备与语义保持。
  - 二进制分析与重组、Compiler Algorithms、IR/Scheduling Transformation、Code Generation/Reassembly、Compiler Search

- [SmoothE: Differentiable E-Graph Extraction](https://doi.org/10.1145/3669940.3707262)
  - Yaohui Cai (Cornell University), Kaixin Yang (Cornell University), Chenhui Deng (Cornell University), Cunxi Yu (University of Maryland, College Park), Zhiru Zhang (Cornell University)
  - SmoothE 是一种可微的电子图提取算法，旨在处理复杂的成本模型并针对 GPU 加速进行了优化，并在 PyTorch 中实现 SmoothE 以利用现代机器学习生态系统的进步。
  - 传统 e-graph extraction 是离散组合优化，面对复杂非线性 cost model 时难以求解并利用 GPU；SmoothE 是一种可微的电子图提取算法，旨在处理复杂的成本模型并针对 GPU 加速进行了优化。
  - E-graph Extraction、Differentiable Optimization、复杂 Cost Model、GPU-accelerated Compiler Search、PyTorch

- [Exo 2: Growing a Scheduling Language](https://doi.org/10.1145/3669940.3707218)
  - Yuka Ikarashi (MIT CSAIL), Kevin Qian (MIT CSAIL), Samir Droubi (MIT CSAIL), Alex Reinking (Adobe), Gilbert Louis Bernstein (University of Washington), Jonathan Ragan-Kelley (MIT CSAIL)
  - Exo 2 是用户可扩展的 tensor scheduling language：可信核心只提供细粒度语义保持 primitive，用户通过统一的 Cursor 接口检查 IR、引用位置并组合 action，从而在语言外定义新的 scheduling library。论文用同一机制复现/扩展 80 个 kernel 的优化计划。
  - 相较把 tile、fusion、vectorize 等 transform 固化在编译器中，核心创新是把调度语言本身设计成可由用户安全扩展的库接口，同时用小型可信 primitive 保留正确性边界。
  - Tensor Compiler、User-extensible Scheduling、Cursor API、可信变换原语、Kernel Optimization Library

- [Manta: Hybrid-Sensitive Type Inference Toward Type-Assisted Bug Detection for Stripped Binaries](https://doi.org/10.1145/3622781.3674177)
  - Chengfeng Ye (The Hong Kong University of Science and Technology), Yuandao Cai (The Hong Kong University of Science and Technology), Anshunkang Zhou (The Hong Kong University of Science and Technology), Heqing Huang (City University of Hong Kong), Hao Ling (The Hong Kong University of Science and Technology), Charles Zhang (The Hong Kong University of Science and Technology)
  - Manta 为 stripped binary 组合多种 flow/context sensitivity 的 data-flow analysis，互补推断变量 type；这些 type 用于删去不可能的 indirect-call target 和 data dependency，再交给 bug detector/program slicing，最终发现 86 个开发者确认的 IoT firmware 漏洞。
  - 单一 sensitivity 的 type recovery 在 stripped binary 上不是漏类型就是不可扩展；Manta 让多种敏感度分析互相补足，并把恢复类型直接反馈给 call-target pruning 与 bug slicing。
  - 在线模型推理、Automated Program Testing、Binary/UI/Concurrency Analysis、Cross-level Validation、Runtime Bug Detection

- [Selectively Uniform Concurrency Testing](https://doi.org/10.1145/3669940.3707214)
  - Huan Zhao (National University of Singapore), Dylan Wolff (National University of Singapore), Umang Mathur (National University of Singapore), Abhik Roychoudhury (National University of Singapore)
  - SURW 是在线随机并发测试器，可对整个程序的 interleaving，或用户选定的一组关键 event 之间的相对顺序进行近似均匀采样；后者缩小状态空间，并让真正影响 bug 的行为组合获得更均衡的探索概率。它不需要预先枚举完整 schedule。
  - 相较受线程调度器偏置的 random walk，核心创新是直接以 interleaving-uniform 为采样目标，并允许把均匀性投影到选定事件子空间以兼顾覆盖广度与可扩展性。
  - 并发程序测试、Uniform Interleaving Sampling、Randomized Scheduler、事件子集、并发 Bug 发现

- [TAOPT: Tool-Agnostic Optimization of Parallelized Automated Mobile UI Testing](https://doi.org/10.1145/3676641.3716282)
  - Dezhi Ran (Key Lab of HCST (PKU), MOE; SCS, Peking University), Zihe Song (University of Texas at Dallas), Wenyu Wang (University of Illinois at Urbana-Champaign), Wei Yang (University of Texas at Dallas), Tao Xie (Key Lab of HCST (PKU), MOE; SCS, Peking University)
  - TaOPT 是一种完全自动化、与工具无关的方法，它可以在不修改工具内部工作流程的情况下提高任何给定测试工具的并行化有效性，并持续增强自动化 UI 测试工具，在给定相同测试资源的情况下检测到 1.2 到 2.1 倍的独特崩溃。
  - 移动 UI test 的并行化优化通常嵌入特定测试工具，无法在不改内部工作流时复用；为了优化自动化移动 UI 测试的并行化，采用 TaOPT，一种完全自动化的、与工具无关的方法，它可以提高任何给定测试工具的并行化有效性，而无需修改工具的内部工作流程。
  - 移动 UI 并行测试、Automated Program Testing、Binary/UI/Concurrency Analysis、Cross-level Validation、Runtime Bug Detection

- [Debugger Toolchain Validation via Cross-Level Debugging](https://doi.org/10.1145/3669940.3707271)
  - Yibiao Yang (State Key Laboratory for Novel Software Technology, Nanjing University), Maolin Sun (State Key Laboratory for Novel Software Technology, Nanjing University), Jiangchang Wu (State Key Laboratory for Novel Software Technology, Nanjing University), Qingyang Li (State Key Laboratory for Novel Software Technology, Nanjing University), Yuming Zhou (State Key Laboratory for Novel Software Technology, Nanjing University)
  - Devil是一个实用的框架，它采用了CLD中的三个关键关系：程序位置的可达性保留、可达程序位置的顺序保留以及程序位置的值一致性，这适用于不同调试级别的跟踪。
  - debugger toolchain 往往只在源码、IR、机器码中的单层自测，跨层状态不一致缺少系统 oracle；为了解决这些限制，采用一种称为跨级调试（CLD）的新概念，用于验证调试器工具链。
  - 调试器工具链验证、Automated Program Testing、Binary/UI/Concurrency Analysis、Cross-level Validation、Runtime Bug Detection

- [Dynamic Partial Deadlock Detection and Recovery via Garbage Collection](https://doi.org/10.1145/3676641.3715990)
  - Georgian-Vlad Saioc (Aarhus University,Programming Systems Group, Uber Technologies, Inc.), I-Ting Angelina Lee (Washington University in St. Louis), Anders Møller (Aarhus University), Milind Chabbi (Programming Systems Group, Uber Technologies, Inc.)
  - GOLF 把 partial-deadlock detection 嵌入 Go garbage collector：mark phase 对 goroutine/channel 关联对象做保守 liveness approximation，识别仍被内存引用但无法继续通信的子图，并可自动解除/回收其状态；Uber 服务 24 小时内检出 252 次 partial deadlock。
  - 专用 deadlock instrumentation 难判断对象是否仍有用；GOLF 复用 GC 本已执行的全堆 mark，以 sound liveness approximation 同时定位和回收只阻塞部分程序的通信子图。
  - 动态死锁检测与恢复、Automated Program Testing、Binary/UI/Concurrency Analysis、Cross-level Validation、Runtime Bug Detection

- [Accelerating LLM Serving for Multi-turn Dialogues with Efficient Resource Management](https://doi.org/10.1145/3676641.3716245)
  - Jinwoo Jeong (Korea University), Jeongseob Ahn (Korea University)
  - FlashGen 面向 chatbot 的多轮对话请求，把历史 turn 的 attention KV 保存在 GPU—CPU DRAM—SSD 多级 cache，按成本恢复而非重新 prefill；调度器还在保持公平的约束下重排请求，避免长 prompt 形成 head-of-line blocking。OPT-30B/Llama-2-70B 上吞吐较 vLLM 提高 1.63–2.85 倍。
  - 相较把每轮拼接后的完整对话重新计算并按 FCFS 排队，核心创新是让跨 turn KV 生命周期和 request order 联合管理，在容量层级与 GPU 批处理间权衡。
  - LLM Serving、多轮对话、GPU-CPU-SSD KV Cache、请求重排、Head-of-line Blocking

- [COMET: Towards Practical W4A4KV4 LLMs Serving](https://doi.org/10.1145/3676641.3716252)
  - Lian Liu (Institute of Computing Technology, CAS,University of Chinese Academy of Sciences), Long Cheng (North China Electric Power University), Haimeng Ren (ShanghaiTech University), Zhaohui Xu (ShanghaiTech University), Yudong Pan (Institute of Computing Technology, CAS,University of Chinese Academy of Sciences), Mengdi Wang (Institute of Computing Technology, CAS), Xiaowei Li (Institute of Computing Technology, CAS,Zhongguancun Laboratory), Yinhe Han (Institute of Computing Technology, CAS), Ying Wang (Institute of Computing Technology, CAS)
  - COMET 实现 W4A4KV4 LLM serving：FMPQ 将大多数 activation 压到 4 bit、敏感部分保留 8 bit，W4Ax kernel 用混合精度 layout 与 GPU software pipeline 隐藏反量化/加载，并按 SM 做细粒度负载平衡。LLaMA-3-70B 在单 A100 上端到端吞吐较 TensorRT-LLM 提高约 2.02 倍。
  - 相较只量化 weight 或维持 8-bit activation，核心创新是把 activation、weight、KV 全部压到 4 bit，同时以专用混合精度 kernel 解决硬件利用率与精度损失。
  - LLM Serving、W4A4KV4 Quantization、Mixed-precision Kernel、KV Cache 压缩、GPU SM Scheduling

- [Past-Future Scheduler for LLM Serving under SLA Guarantees](https://doi.org/10.1145/3676641.3716011)
  - Ruihao Gong (Beihang University), Shihao Bai (SenseTime), Siyu Wu (Beihang University), Yunqian Fan (SenseTime), Zaijun Wang (SenseTime), Xiuhong Li (Peking University), Hailong Yang (Beihang University), Xianglong Liu (Beihang University)
  - LightLLM 的 Past-Future scheduler 为 continuous batching 预测正在运行 batch 的未来峰值显存：它从历史 output-length distribution 估计每个未来时刻的 KV 占用，在排队等待与因 OOM 驱逐请求之间自适应取舍，面对不同输入/输出长度分布仍维持 SLA goodput。
  - 相较用固定最大长度做保守预留或按平均长度激进超卖，核心创新是将历史分布转成随时间演化的 batch memory curve，直接用未来峰值作准入。
  - LLM Serving、Continuous Batching、KV Memory Forecasting、SLA Goodput、Request Admission

- [POD-Attention: Unlocking Full Prefill-Decode Overlap for Faster LLM Inference](https://doi.org/10.1145/3676641.3715996)
  - Aditya K Kamath (Paul G Allen School of Computer Science and Engineering, University of Washington), Ramya Prabhu (Microsoft Research India), Jayashree Mohan (Microsoft Research India), Simon Peter (Paul G Allen School of Computer Science and Engineering, University of Washington), Ramachandran Ramjee (Microsoft Research India), Ashish Panwar (Microsoft Research India)
  - POD-Attention 针对同时含 compute-bound prefill 与 bandwidth-bound decode 的 hybrid batch，在同一 GPU multiprocessor 内分配算力、带宽和并行工作，使两种 attention 同时执行，而非分别调用两个 kernel；attention 最多加速 59%。
  - 相较只在线性层重叠 prefill/decode、attention 仍由阶段专用 kernel 串行处理，核心创新是首个面向 hybrid batch 的融合 attention kernel，在 SM 内做互补资源共置。
  - LLM Inference、Prefill/Decode Overlap、Hybrid Batching、Attention Kernel、GPU Resource Co-location

- [TAPAS: Thermal- and Power-Aware Scheduling for LLM Inference in Cloud Platforms](https://doi.org/10.1145/3676641.3716025)
  - Jovan Stojkovic (University of Illinois at Urbana-Champaign), Chaojie Zhang (Microsoft Azure Research), Íñigo Goiri (Microsoft Azure Research), Esha Choukse (Microsoft Azure Research), Haoran Qiu (Microsoft Azure Research), Rodrigo Fonseca (Microsoft Azure Research), Josep Torrellas (University of Illinois at Urbana-Champaign), Ricardo Bianchini (Microsoft Azure)
  - TAPAS 在云端 LLM inference cluster 联合决定新 GPU VM 放在哪个机架、SaaS request 路由到哪个实例，以及模型并行度/量化等 VM configuration。它读取历史与实时温度、功率、负载及冷却/供电约束，利用 SaaS 比 IaaS 更可重配的特性，在常态超卖和冷却/电力故障时避免 throttle。
  - 相较只按 GPU utilization 放置推理副本，核心创新是把毫秒级 LLM phase 的热功率画像、机架基础设施约束和 request routing/模型配置纳入同一控制面。
  - LLM Serving、Thermal-aware Scheduling、Power Oversubscription、Request Routing、GPU VM Reconfiguration

- [The Mutators Reloaded: Fuzzing Compilers with Large Language Model Generated Mutation Operators](https://doi.org/10.1145/3622781.3674171)
  - Xianfei Ou (Nanjing University), Cong Li (Ant Group,Zhejiang University), Yanyan Jiang (Nanjing University), Chang Xu (Nanjing University)
  - MetaMut 把 compiler domain knowledge 编入 prompt 与验证流程，让 LLM 生成 semantic-aware mutation operator，再由人和测试反馈筛选/修正；118 个 mutator 驱动 fuzzer 在 GCC/Clang 中发现 131 个 bug。LLM 在这里生成系统测试工具，不参与在线系统控制。
  - 相较专家手写少量 mutator，核心创新是把“生成 mutation operator”本身交给带领域约束的 LLM pipeline，以低成本扩大语义变换空间。
  - LLM for Systems、Compiler Fuzzing、Mutation Operator Generation、GCC/Clang、领域知识 Prompt

- [ClosureX: Compiler Support for Correct Persistent Fuzzing](https://doi.org/10.1145/3669940.3707281)
  - Rishi Ranjan (Virginia Tech), Ian Paterson (Virginia Tech), Matthew Hicks (Virignia Tech)
  - ClosureX 是一种模糊测试执行机制，它位于状态恢复连续体的一个新位置，其中仅重置测试用例执行特定的状态，并提供近乎持久的性能和重量级状态恢复的正确性。
  - persistent fuzzing 在每个 test case 后要么恢复全部进程状态、要么不恢复，性能与正确隔离难兼得；ClosureX，一种模糊测试执行机制，它位于状态恢复连续体的一个新位置，其中仅重置测试用例执行特定的状态。
  - 编译器与代码生成、程序/内核模糊测试、Compiler/Kernel Fuzzing、Mutation/Test Generation、Coverage/Validation Feedback

- [Ratte: Fuzzing for Miscompilations in Multi-Level Compilers Using Composable Semantics](https://doi.org/10.1145/3676641.3716270)
  - Pingshi Yu (Imperial College London), Nicolas Wu (Imperial College London), Alastair F. Donaldson (Imperial College London)
  - Ratte 为 MLIR dialect 定义可组合 reference semantics，并由语义自动导出 modular fuzzer；generator 只构造无 undefined behavior 的 testcase，执行结果又反向校验 dialect 语义/实现，组合不同 dialect 时无需重写 oracle。
  - 普通 MLIR fuzzer 缺少跨 dialect 的合法性 oracle；Ratte 让 composable semantics 同时充当 testcase generator 与 reference interpreter，因此可廉价组合 dialect 并排除 undefined behavior。
  - 编译器与代码生成、程序/内核模糊测试、Compiler/Kernel Fuzzing、Mutation/Test Generation、Coverage/Validation Feedback

- [Snowplow: Effective Kernel Fuzzing with a Learned White-box Test Mutator](https://doi.org/10.1145/3676641.3716019)
  - Sishuai Gong (Purdue University), Wang Rui (Purdue University), Deniz Altinbüken (Google DeepMind), Pedro Fonseca (Purdue University), Petros Maniatis (Google DeepMind)
  - Snowplow 是一种内核模糊器，它使用学习的白盒测试变异器来增强测试变异，并且通过以 8.5 倍的速度达到 19 个目标代码位置以及最先进的定向内核模糊器错过的两个附加位置来加速定向内核模糊器。
  - 手工 mutator heuristic 不知道哪次 argument change 会走向目标 kernel path；Snowplow 的 white-box model 同时读取当前 test、已达 coverage 与 desired coverage，预测最有希望的变异。
  - Kernel Fuzzing、Learned White-box Mutator、Coverage-guided Mutation、Directed Fuzzing、Linux Kernel

- [KernelGPT: Enhanced Kernel Fuzzing via Large Language Models](https://doi.org/10.1145/3676641.3716022)
  - Chenyuan Yang (University of Illinois at Urbana-Champaign), Zijie Zhao (University of Illinois at Urbana-Champaign), Lingming Zhang (University of Illinois at Urbana-Champaign)
  - KernelGPT 读取 kernel code、文档和既有用例生成 syscall specification，再让 Syzkaller validation feedback 驱动 LLM 迭代 debug/repair，最终将有效 spec 纳入 fuzzing；已发现 24 个 Linux kernel 新 bug。由于它闭环执行“生成—验证—修复”，这里归为 Agent for Systems。
  - 相较人工维护或静态分析生成 syscall spec，核心创新是把执行验证结果返回 LLM 形成“推断—测试—修复”闭环，持续补齐复杂 syscall 语义。
  - Agent for Systems、Kernel Fuzzing、Syscall Specification Synthesis、Validation Feedback Loop、Syzkaller

- [Controlled Preemption: Amplifying Side-Channel Attacks from Userspace](https://doi.org/10.1145/3676641.3715985)
  - Yongye Zhu (University of California, Berkeley), Boru Chen (University of California, Berkeley), Zirui Neil Zhao (NVIDIA,UT Austin), Christopher W. Fletcher (University of California, Berkeley)
  - Controlled Preemption 让无特权攻击者与 victim 共置在同一 logical core，操纵 Linux CFS/EEVDF 的公平性启发式，使 victim 运行 0 到数条指令后便被反复抢占数百次；攻击者由此获得细粒度观测窗口，并在 SGX 等侧信道场景提高分辨率。
  - 相较依赖多个 helper thread、定时器或特殊权限的既有 single-step 技术，核心创新是把通用调度器的 fairness tripwire 转化为单用户线程即可触发的可控抢占原语。
  - OS Scheduler Security、Controlled Preemption、Linux CFS/EEVDF、SGX Side Channel、Unprivileged Attack

- [Protecting Cryptographic Code Against Spectre-RSB](https://doi.org/10.1145/3676641.3716015)
  - Santiago Arranz Olmos (MPI-SP), Gilles Barthe (MPI-SP, IMDEA Software Institute), Chitchanok Chuengsatiansup (University of Melbourne), Benjamin Gregoire (Inria), Vincent Laporte (Université de Lorraine, CNRS, Inria, LORIA), Tiago Oliveira (Sandbox AQ), Peter Schwabe (MPI-SP,Radboud University), Yuval Yarom (Ruhr University Bochum), Zhiyuan Zhang (MPI-SP)
  - 该工作为 constant-time cryptographic code 建立 value-dependent information-flow type system，编译器据此插入/重写防护，使秘密值不能经 Spectre v1/v2 及 return-stack-buffer speculation 泄漏；机制在 Jasmin 工具链中实现，并以 Coq 证明从源级到低级代码的安全性，多数密码原语开销低于 2%。
  - 相较靠局部 fence 或只覆盖 Spectre v1 的补丁，核心创新是把 return speculation 也纳入可证明的信息流规则，并给出编译变换的端到端形式化保证。
  - Spectre-RSB 防护、Constant-time Cryptography、Information-flow Types、Verified Compilation、Jasmin/Coq

- [Reload+Reload: Exploiting Cache and Memory Contention Side Channel on AMD SEV](https://doi.org/10.1145/3676641.3716017)
  - Li-Chung Chiang (National Taiwan University), Shih-Wei Li (National Taiwan University)
  - 发现了来自支持 SEV 的 AMD 处理器的两个以前未知的侧通道：缓存刷新和内存争用侧通道，并制定了两种重新加载+重新加载攻击：重新加载+重新加载刷新集（RRFS）和重新加载+重新加载内存块（RRMB）。
  - Prime+Probe 一类攻击主要观察 set occupancy；Reload+Reload 分别利用 SEV CPU 的 cache-flush 时延和 memory-block contention，构造 RRFS/RRMB，即使 guest memory 加密也能建立信道和提取 AES key。
  - Cache 管理、微体系结构安全、Microarchitectural Side Channel、Speculation/Cache Attack、Secure Scheduling

- [SMaCk: Efficient Instruction Cache Attacks via Self-Modifying Code Conflicts](https://doi.org/10.1145/3676641.3716274)
  - Seonghun Son (Iowa State University), Daniel Moghimi (Google), Berk Gulmezoglu (Iowa State University)
  - SMaCk 测量会影响 instruction-cache line 的 x86 self-modifying-code instruction 在 hit/miss 时的 timing gap，并把该信号嵌入 Prime+Probe、Flush+Reload 等攻击以降低噪声；同一工作还用 hardware performance counter 做动态检测。
  - 传统 I-cache channel 受共享代码/flush 条件限制；SMaCk 把 self-modifying-code conflict 的 hit/miss 时差变成新的测量原语，增强既有 cache attack 并配套 HPC detector。
  - Cache 管理、微体系结构安全、Microarchitectural Side Channel、Speculation/Cache Attack、Secure Scheduling

- [FlexProf: Flexible, Side-Channel-Free Memory Access](https://doi.org/10.1145/3676641.3715997)
  - Jarrett Minton (University of Utah), Rajeev Balasubramonian (University of Utah)
  - FlexProf 在阻断共置 VM 内存控制器侧信道时，把固定轮转时隙细分为 read-optimized 与 write-optimized turn；粗粒度、无泄漏 profile 决定两类时隙比例，空闲时还允许机会式发出另一类请求，在固定访问形状和带宽利用率间平衡。
  - 相较每个 VM turn 都按读写最坏情况预留并插入 gap，核心创新是公开且固定的读写 pattern specialization，在不暴露瞬时请求类型时减少安全调度浪费。
  - Memory-controller Side Channel、Secure Scheduling、Read/Write Turn、VM Co-location、Performance Isolation

- [Clapton: Clifford Assisted Problem Transformation for Error Mitigation in Variational Quantum Algorithms](https://doi.org/10.1145/3622781.3674178)
  - Lennart Maximilian Seifert (Department of Computer Science, University of Chicago), Siddharth Dangwal (Department of Computer Science, University of Chicago), Frederic T. Chong (Department of Computer Science, University of Chicago), Gokul Subramanian Ravi (Electrical Engineering and Computer Science Department, University of Michigan)
  - Clapton 被构建为端到端应用程序到设备框架，在对噪声模型和真实量子设备上的物理和化学等各种科学应用进行评估时，与最先进的基线相比，平均 VQA 初始化提高了 1.7 倍到 3.3 倍。
  - VQA 的 error mitigation 通常直接在原问题电路上采样，深电路噪声使估计方差和成本迅速上升；为了系统地减轻量子设备误差对 VQA 的影响，采用 Clapton：用于变分量子算法中误差缓解的 Clifford 辅助问题转换。
  - 量子误差缓解、量子计算系统、Quantum Error Correction、QEC Layout/Decoder、Fault-tolerant Scheduling

- [QECC-Synth: A Layout Synthesizer for Quantum Error Correction Codes on Sparse Architectures](https://doi.org/10.1145/3669940.3707236)
  - Keyi Yin (University of California, San Diego), Hezi Zhang (University of California, San Diego), Xiang Fang (University of California, San Diego), Yunong Shi (AWS Quantum Technologies), Travis S. Humble (Oak Ridge National Laboratory), Ang Li (Pacific Northwest National Laboratory), Yufei Ding (University of California, San Diego)
  - QECC-Synth 把 QEC circuit 所需的 dense qubit connectivity 映射到 sparse hardware：系统化展开 ancilla-bridge 的可选布局/路由，把 code 与设备约束编码成 MaxSAT，自动选择 bridge 与 placement，覆盖多种 QEC code 和 topology。
  - 手工为单一 QEC code/设备画 layout 无法迁移；QECC-Synth 把 ancilla-bridge flexibility 完整参数化并交给 MaxSAT，在 code 和 sparse topology 同变时仍能自动优化。
  - 量子纠错、量子计算系统、Quantum Error Correction、QEC Layout/Decoder、Fault-tolerant Scheduling

- [HetEC: Architectures for Heterogeneous Quantum Error Correction Codes](https://doi.org/10.1145/3676641.3716001)
  - Samuel Stein (Future Computing Technologies, Pacific Northwest National Laboratory), Shifan Xu (Yale Quantum Institute, Yale University), Andrew W. Cross (IBM Quantum, IBM T.J Watson Research Center), Theodore J. Yoder (IBM Quantum, IBM T. J. Watson Research Center), Ali Javadi-Abhari (IBM Quantum, IBM T. J. Watson Research Center), Chenxu Liu (Future Computing Technologies, Pacific Northwest National Laboratory), Kun Liu (Yale Quantum Institute, Yale University), Zeyuan Zhou (Yale Quantum Institute, Yale University), Charlie Guinn (Department of Physics, Princeton University), Yufei Ding (Department of Computer Science & Engineering, University of California San Diego), Yongshan Ding (Yale Quantum Institute, Yale University), Ang Li (Future Computing Technologies, Pacific Northwest National Laboratory,Department of Electrical & Computer Engineering, University of Washington)
  - 该工作对异构纠错码进行了首次完整的系统研究，发现架构权衡并围绕它们进行优化，并建议使用辅助总线集成表面代码和总代码以进行代码间数据移动。
  - QEC accelerator 通常假定所有 logical qubit 使用同一种 code，无法利用异构错误率和保护需求；受物理量子位开销潜在减少（实现容错计算的一个重要特征）的推动，该工作对异构纠错码进行了首次完整的系统研究，发现架构权衡并围绕它们进行优化。
  - 量子纠错、量子计算系统、Quantum Error Correction、QEC Layout/Decoder、Fault-tolerant Scheduling

- [Micro Blossom: Accelerated Minimum-Weight Perfect Matching Decoding for Quantum Error Correction](https://doi.org/10.1145/3676641.3716005)
  - Yue Wu (Yale University), Namitha Liyanage (Yale University), Lin Zhong (Yale University)
  - Micro Blossom 把 exact minimum-weight perfect matching decoder 拆到软件与 programmable accelerator：decode graph 的 vertex/edge 各由并行单元处理，FPGA prototype 在 distance-13、0.1% error rate 下把平均 decoding latency 压到 0.8 μs。
  - 纯软件 MWPM 难满足 superconducting qubit 的微秒周期；Micro Blossom 按 decode-graph vertex/edge 配置并行单元，把精确算法而非近似 decoder 下沉到可编程硬件。
  - 量子纠错、量子计算系统、Quantum Error Correction、QEC Layout/Decoder、Fault-tolerant Scheduling

- [RESCQ: Realtime Scheduling for Continuous Angle Quantum Error Correction Architectures](https://doi.org/10.1145/3676641.3716018)
  - Sayam Sethi (Department of Electrical and Computer Engineering, The University of Texas at Austin), Jonathan Mark Baker (Department of Electrical and Computer Engineering, The University of Texas at Austin)
  - RESCQ（发音为rescue），一种用于编译到这些连续角度系统上的程序的实时调度程序，一种用于编译到这些连续角度系统上的程序的实时调度程序，它通过基于预期生产率的资源按需重新分配来主动最小化总周期计数。
  - continuous-angle QEC 的操作持续时间不等，沿用离散 time-step scheduler 会错估冲突和 deadline；RESCQ（发音为rescue），它是一个实时调度程序，用于编译到这些连续角度系统上的程序。
  - 量子纠错、量子计算系统、运行时调度与放置、Quantum Error Correction、QEC Layout/Decoder

- [GraphPipe: Improving Performance and Scalability of DNN Training with Graph Pipeline Parallelism](https://doi.org/10.1145/3669940.3707220)
  - Byungsoo Jeon (NVIDIA), Mengdi Wu (Carnegie Mellon Univerisity), Shiyi Cao (UC Berkeley), Sunghyun Kim (Massachusetts Institute of Technology), Sunghyun Park (NVIDIA), Neeraj Aggarwal (Carnegie Mellon University), Colin Unger (Stanford University), Daiyaan Arfeen (Carnegie Mellon University), Peiyuan Liao (Carnegie Mellon University), Xupeng Miao (Carnegie Mellon University), Mohammad Alizadeh (Massachusetts Institute of Technology), Gregory R. Ganger (Carnegie Mellon University), Tianqi Chen (Carnegie Mellon University), Zhihao Jia (Carnegie Mellon University)
  - 图管道并行（GPP），这是一种新的管道并行方案，它将 DNN 划分为管道阶段，其依赖关系由有向无环图识别，并保留 DNN 的固有拓扑，以实现计算独立运算符的并发执行。
  - 传统 pipeline parallelism 按线性 layer 切 stage，难以表达 DNN computation graph 的分支与跨 stage dependency；此外，该工作还开发了 GraphPipe，这是一个分布式系统，利用 GPP 策略来实现高性能和可扩展的 DNN 训练。
  - DNN Training、Graph Pipeline Parallelism、DAG Stage Partitioning、Independent-operator Concurrency、分布式训练

- [Cascade: A Dependency-aware Efficient Training Framework for Temporal Graph Neural Network](https://doi.org/10.1145/3676641.3716250)
  - Yue Dai (Department of Computer Science, University of Pittsburgh), Xulong Tang (Department of Computer Science, University of Pittsburgh), Youtao Zhang (Department of Computer Science, University of Pittsburgh)
  - Cascade 在 TGNN training 中按节点空间邻接把 independent event 放进同一 batch，并用 node-memory similarity 判断哪些 stabilized node 可暂时打破 temporal dependency；runtime feedback 再调整各节点 memory-update frequency，在不降准确率时平均加速 2.3 倍。
  - 增大 TGNN batch 会让 node memory 过期，小 batch 又闲置 GPU；Cascade 用拓扑独立性、memory stabilization 和在线更新频率共同判断哪些 event 可以安全并行。
  - 图神经网络系统、Distributed Model Training、Pipeline/Graph Parallelism、Embedding/GNN Training、数据—计算流水

- [Frugal: Efficient and Economic Embedding Model Training with Commodity GPUs](https://doi.org/10.1145/3669940.3707245)
  - Minhui Xie (Tsinghua University,Renmin University of China), Shaoxun Zeng (Tsinghua University), Hao Guo (Tsinghua University), Shiwei Gao (Tsinghua University), Youyou Lu (Tsinghua University)
  - Frugal 在没有 PCIe peer-to-peer 的 commodity GPU 上训练 embedding model：每张 GPU 主动把其他 GPU 即将读取的本地参数刷新到 host memory，使一半跨卡通信离开 critical path，并以调度维持 host-buffer 一致性。
  - 普通 host-staged all-to-all 让两次方向的数据搬运都阻塞训练；Frugal 的 proactive flushing 让拥有者提前写 host buffer，把其中一个方向与计算重叠，令低价 GPU 接近数据中心卡吞吐。
  - 分布式模型训练、GPU 系统、Distributed Model Training、Pipeline/Graph Parallelism、Embedding/GNN Training

- [FastGL: A GPU-Efficient Framework for Accelerating Sampling-Based GNN Training at Large Scale](https://doi.org/10.1145/3622781.3674167)
  - Zeyu Zhu (Institute of Automation, Chinese Academy of Sciences,School of Future Technology, University of Chinese Academy of Sciences), Peisong Wang (Institute of Automation, Chinese Academy of Sciences), Qinghao Hu (Institute of Automation, Chinese Academy of Sciences,AiRiA), Gang Li (Shanghai Jiao Tong University), Xiaoyao Liang (Shanghai Jiao Tong University), Jian Cheng (Institute of Automation, Chinese Academy of Sciences,AiRiA)
  - FastGL 面向大规模 sampling-based GNN 训练，联合处理 subgraph sampling、feature memory I/O 和 GPU computation：根据图结构组织采样/数据布局，并按 GPU 执行特性重叠三个阶段，避免单独加速一段后瓶颈转移到下一段。
  - 相较分别优化 sampler、feature loader 或 kernel，核心创新是以同一端到端 pipeline 联合利用图的结构复用和 GPU 并行/访存特征，使三阶段吞吐匹配。
  - GNN Training、GPU Pipeline、Subgraph Sampling、Feature I/O、端到端阶段协同

- [Extended User Interrupts (xUI): Fast and Flexible Notification without Polling](https://doi.org/10.1145/3676641.3716028)
  - Berk Aydogmus (Purdue University), Linsong Guo (UC San Diego), Danial Zuberi (UC San Diego), Tal Garfinkel (UC San Diego), Dean Tullsen (UC San Diego), Amy Ousterhout (UC San Diego), Kazem Taram (Purdue University)
  - 该工作通过分析和测量解构了英特尔当前的 UIPI 设计，并用其开发了精确的时序模型，并介绍了对用户中断的四种增强功能：跟踪中断、硬件安全点、内核旁路定时器和中断转发。
  - 现有 UIPI 只提供基本用户中断，缺少可追踪投递、安全抢占点、内核旁路 timer 与转发能力；然后介绍了对用户中断的四个​​增强功能：跟踪中断、硬件安全点、内核旁路计时器和中断转发。 xUI 在 gem5 模拟中建模，并在三个用例上进行评估：高性能用户级运行时中的抢占、使用 DPDK 的第 3 层路由器中的 IO 通知，以及使用以英特尔数据流加速器为模型的流加速器的合成工作负载中的 IO 通知。
  - OS/Compiler Mechanism、Heterogeneous-ISA Runtime、Formal Invariant/Numerical Compilation、用户级通知

- [Stramash: A Fused-kernel Operating System For Cache-Coherent, Heterogeneous-ISA Platforms](https://doi.org/10.1145/3676641.3716275)
  - Tong Xing (The University of Edinburgh), Cong Xiong (Imperial College London), Tianrui Wei (UC Berkeley), April Sanchez (Google), Binoy Ravindran (Virginia Tech), Jonathan Balkind (UC Santa Barbara), Antonio Barbalace (The University of Edinburgh)
  - Stramash 的 fused-kernel OS 让 heterogeneous-ISA CPU 共享同一 kernel 与 cache-coherent memory，而非各跑一个 kernel 再 RPC；Stramash-Linux 实现跨 ISA 的内核机制，Stramash-QEMU 用于验证设计，NPB 上相对 multi-kernel 最高加速 2.1 倍。
  - multi-kernel OS 把 coherent heterogeneous CPU 仍当分布式节点；fused-kernel 直接把一致共享内存作为 OS 原语，消除跨 ISA kernel 间多余协调层。
  - Cache 管理、OS/Compiler Mechanism、Heterogeneous-ISA Runtime、Formal Invariant/Numerical Compilation、用户级通知

- [H-Houdini: Scalable Invariant Learning](https://doi.org/10.1145/3669940.3707263)
  - Sushant Dinesh (University of California, Berkeley), Yongye Zhu (University of California, Berkeley), Christopher W. Fletcher (University of California, Berkeley)
  - H-Houdini 为大型硬件设计学习 inductive invariant：把 ML-inspired synthesis 原本的单体 SMT 检查拆成层次化的小型 incremental SMT query，这些 query 可并行、memoize，并按 construction 重新组合为正确 invariant；实现 VeloCT 可在约 7–199 分钟验证多种 RISC-V BOOM 配置。
  - 相较每轮求解一个随设计规模爆炸的 monolithic SMT formula，核心创新是用可组合的层次分解保留 invariant 正确性，同时开放并行与增量复用空间。
  - Hardware Formal Verification、Invariant Learning、Incremental SMT、H-Houdini、RISC-V BOOM

- [Target-Aware Implementation of Real Expressions](https://doi.org/10.1145/3669940.3707277)
  - Brett Saiki (University of Washington), Jackson Brough (University of Utah), Jonas Regehr (University of Utah), Jesus Ponce (University of Utah), Varun Pradeep (University of Washington), Aditya Akhileshwaran (University of Washington), Zachary Tatlock (University of Washington), Pavel Panchekha (University of Utah)
  - 该工作将传统编译器和数值编译器的各个方面结合起来，产生了 Chassis，这是一种目标感知数值编译器，它通过利用低精度加速器、精度优化的数值辅助函数和库子组件，找到了比 Clang 或 Herbie 更好的精度和性能权衡。
  - 传统 backend 只看 target cost、数值编译器只看误差；Chassis 的 target description 同时记录每个 operator 近似的实数表达式、代价和精度，再以 modulo-equivalence instruction selection 联合搜索。
  - OS/Compiler Mechanism、Heterogeneous-ISA Runtime、Formal Invariant/Numerical Compilation、用户级通知

- [TaintEMU: Decoupling Tracking from Functional Domains for Architecture-Agnostic and Efficient Whole-System Taint Tracking](https://doi.org/10.1145/3676641.3716023)
  - Lei Cui (Guangxi Normal University), Youquan Xian (Guangxi Normal University), Peng Liu (Guangxi Normal University), Longjin Lu (Independent Researcher)
  - 引入了 TaintEMU，这是一种与架构无关的高效解决方案，通过完全解耦在 QEMU TCG 层分离功能和跟踪逻辑的两个域，将影子寄存器映射到主机而不是客户寄存器，确保跨客户 CPU 架构的兼容性。
  - taint 与功能执行共享 guest shadow register 和 host 标量资源会绑定 ISA 并放大开销；TaintEMU 在 QEMU TCG 层拆域，把 shadow state 映到 host、让 vector resource 专职 tracking，并直接从 TCG 生成跟踪指令。
  - Whole-system Taint Tracking、Systems Security、Taint/Sandbox/Confidential VM、Information-flow/Isolation、Transient-execution Defense

- [Segue & ColorGuard: Optimizing SFI Performance and Scalability on Modern Architectures](https://doi.org/10.1145/3669940.3707249)
  - Shravan Narayan (UT Austin), Tal Garfinkel (UC San Diego), Evan Johnson (UC San Diego), Zachary Yedidia (Stanford University), Yingchen Wang (UC Berkeley), Andrew Brown (Intel), Anjo Vahldiek-Oberwagner (Intel Labs), Michael LeMay (Intel Labs), Wenyong Huang (Intel), Xin Wang (Intel), Mingqiu Sun (Intel), Dean Tullsen (UC San Diego), Deian Stefan (UC San Diego)
  - 两种提高 SFI 性能和可扩展性的优化：Segue 使用 x86-64 分段来降低内存访问检测的成本，ColorGuard 利用内存标记将可在单个地址空间中并发运行的 Wasm 实例数量增加多达 15 倍，从而提高大规模服务器端工作负载的效率。
  - Wasm SFI 为每次访问插入检查且在单地址空间容纳实例有限，性能和服务端密度同时受限；两种提高 SFI 性能和可扩展性的优化：Segue 使用 x86-64 分段来降低内存访问检测的成本，例如，它消除了 SPEC CPU 2006 的 Wasm 兼容子集上 44.7% 的 Wasm 开销，并将 Firefox 中 Wasm 沙盒字体渲染的开销降低了 75%； ColorGuard 利用内存标记（例如 MPK），使可在单个地址空间中同时运行的 Wasm 实例数量增加多达 15 倍，从而提高大规模服务器端工作负载的效率。
  - Systems Security、Taint/Sandbox/Confidential VM、Information-flow/Isolation、Transient-execution Defense

- [Pave: Information Flow Control for Privacy-preserving Online Data Processing Services](https://doi.org/10.1145/3676641.3716266)
  - Minkyung Park (University of Texas at Dallas), Jaeseung Choi (Sogang University), Hyeonmin Lee (University of Virginia), Taekyoung Kwon (Seoul National University)
  - Pave 在 SGX PaveBox 内执行任意远端数据处理程序，runtime monitor 截获所有输入、输出与外部交互，只放行满足声明式信息流策略、不会泄漏敏感数据的路径；用户通过 remote attestation 确认正确 monitor/策略后再提交数据。
  - 相较要求用户信任云端服务程序本身，核心创新是在 enclave 边界统一强制信息流，并同时形式化证明安全性与对合规程序的 transparency，因而不需要重写具体应用。
  - 可信执行环境、SGX Sandbox、Information-flow Enforcement、Remote Attestation、数据机密性

- [Sharing is leaking: blocking transient-execution attacks with core-gapped confidential VMs](https://doi.org/10.1145/3622781.3674190)
  - Charly Castes (EPFL,Google), Andrew Baumann (Google)
  - 核心间隙机密虚拟机，这是一组纯软件修改，可确保没有不信任的代码共享核心，从而消除来宾 TCB 中的所有相同核心侧通道和瞬时执行漏洞。
  - 补丁式缓解仍把复杂共享 core 状态纳入 confidential-VM TCB；core-gapping 直接改变调度/分配约束，禁止不互信代码共享任何 core，以软件方式一次消除同核 transient channel。
  - 可信执行环境、微体系结构安全、Systems Security、Taint/Sandbox/Confidential VM、Information-flow/Isolation

- [EDM: An Ultra-Low Latency Ethernet Fabric for Memory Disaggregation](https://doi.org/10.1145/3669940.3707221)
  - Weigao Su (Purdue University), Vishal Shrivastav (Purdue University)
  - EDM 采用了一种激进的方法，在以太网的物理层 (PHY) 内实现用于远程内存访问的整个网络协议栈，从而克服了 MAC 层带来的基本延迟和带宽开销。
  - TCP/IP/RDMA 位于 Ethernet MAC 之上，小粒度远程内存请求仍承担 MAC 与排队开销；首先，虽然用于通过以太网进行远程内存访问的现有网络协议（例如 TCP/IP 和 RDMA）是在以太网 MAC 层之上实现的，但 EDM 采取了一种激进的方法，在以太网的物理层 (PHY) 内实现用于远程内存访问的整个网络协议栈。
  - 内存解耦、SmartNIC/数据中心网络、Datacenter Networking、SmartNIC/vSwitch、Remote-memory Fabric

- [Performance Prediction of On-NIC Network Functions with Multi-Resource Contention and Traffic Awareness](https://doi.org/10.1145/3669940.3707232)
  - Shaofeng Wu (The Chinese University of Hong Kong), Qiang Su (The Chinese University of Hong Kong), Zhixiong Niu (Microsoft Research), Hong Xu (The Chinese University of Hong Kong)
  - Yala 为 SmartNIC 上共置的 network function 建模：输入包括包速率/大小等 traffic attribute，以及片上 accelerator、memory bandwidth 等多资源争用状态；预测各 NF 的吞吐/延迟后再用于放置与准入。BlueField 实验把预测准确率提高 78.8%，SLA violation 降低 92.2%。
  - 相较只按 CPU 利用率或单一 accelerator contention 估计 NF 性能，核心创新是把流量形态与 SmartNIC 内多类共享资源联合建模，能够区分相同 NF 在不同输入下的干扰响应。
  - SmartNIC NF Placement、性能干扰预测、多资源争用、Traffic-aware Modeling、SLA 保障

- [Gigaflow: Pipeline-Aware Sub-Traversal Caching for Modern SmartNICs](https://doi.org/10.1145/3676641.3716000)
  - Annus Zulfiqar (University of Michigan), Ali Imran (University of Michigan), Venkat Kunaparaju (Purdue University), Ben Pfaff (Feldera Inc.), Gianni Antichi (Politecnico di Milano), Muhammad Shahbaz (University of Michigan)
  - Gigaflow 为 SmartNIC vSwitch cache 利用 L2/L3/ACL 等 programmable pipeline 的执行顺序，把多条 flow 共享的 sub-traversal 缓存为规则片段，而非缓存完整 flow path；有限片上内存可覆盖最高 450 倍规则空间并保持 line rate。
  - 按完整 flow/traversal 缓存时，每条规则只服务少数 packet；Gigaflow 缓存 pipeline-aware 共享子路径，让同一片段被多条 flow 复用，从容量端扩大 rule-space coverage。
  - SmartNIC/数据中心网络、Cache 管理、Datacenter Networking、SmartNIC/vSwitch、Remote-memory Fabric

- [TNIC: A Trusted NIC Architecture](https://doi.org/10.1145/3676641.3716277)
  - Dimitra Giantsidi (The University of Edinburgh), Julian Pritzi (Technical University of Munich), Felix Gust (Technical University of Munich), Antonios Katsarakis (Huawei Research), Atsushi Koshiba (Technical University of Munich), Pramod Bhatotia (Technical University of Munich)
  - 一组通用的编程 API 以及为拜占庭设置构建高性能、值得信赖的分布式系统的秘诀，并正式验证了 TNIC 的安全性和安保属性，同时通过构建四个值得信赖的分布式系统来展示其用途。
  - 拜占庭云系统若把信任根放在 host CPU/软件栈，TCB 大且不同主机难提供统一 non-equivocation；TNIC 是一种可信 NIC 架构，用于构建部署在异构、不可信（拜占庭）云环境中的可信分布式系统。
  - SmartNIC/数据中心网络、Datacenter Networking、SmartNIC/vSwitch、Remote-memory Fabric、Trusted Network Interface

- [Einsum Trees: An Abstraction for Optimizing the Execution of Tensor Expressions](https://doi.org/10.1145/3676641.3716254)
  - Alexander Breuer (Friedrich Schiller University Jena), Mark Blacher (Friedrich Schiller University Jena), Max Engel (Friedrich Schiller University Jena), Joachim Giesen (Friedrich Schiller University Jena), Alexander Heinecke (Intel Corporation), Julien Klaus (Friedrich Schiller University Jena), Stefan Remke (Friedrich Schiller University Jena)
  - Einsum Tree IR 在 contraction-path 已确定后，把整棵二元 tensor contraction tree 的 shape、layout 和中间张量关系放入同一 IR；optimizer 跨节点选择 permutation/packing，而不是逐个 GEMM 只优化本地输入布局，并在 Arm/x86 平台生成执行计划。
  - 相较把 contraction path search 与局部 binary contraction layout 分开，核心创新是把 data layout 变成树级全局决策，使一个节点的布局代价可与其所有下游复用共同权衡。
  - Tensor Compiler、Einsum Tree IR、Global Data-layout Optimization、Tensor Contraction、跨算子规划

- [Optimizing Deep Learning Inference Efficiency through Block Dependency Analysis](https://doi.org/10.1145/3676641.3716264)
  - Zhanyuan Di (SKLP, Institute of Computing Technology, CAS,University of Chinese Academy of Sciences), Leping Wang (SKLP, Institute of Computing Technology, CAS), En Shao (SKLP, Institute of Computing Technology, CAS,University of Chinese Academy of Sciences), Zhaojia Ma (SKLP, Institute of Computing Technology, CAS,University of Chinese Academy of Sciences), Ziyi Ren (SKLP, Institute of Computing Technology, CAS,University of Chinese Academy of Sciences), Feng Hua (SKLP, Institute of Computing Technology, CAS,University of Chinese Academy of Sciences), Lixian Ma (SKLP, Institute of Computing Technology, CAS,University of Chinese Academy of Sciences), Jie Zhao (Hunan University), Guangming Tan (SKLP, Institute of Computing Technology, CAS,University of Chinese Academy of Sciences), Ninghui Sun (SKLP, Institute of Computing Technology, CAS,University of Chinese Academy of Sciences)
  - BlockDepend 从 ML compiler 的低层 block/loop IR 抽取跨 operator 的块级读写依赖，把复杂 element relation 压缩成可调度 block relation，并显式找出可并发的计算块；编译器据此联合改善 memory access 与 GPU occupancy。
  - 相较只在 graph 的 operator/element 层静态分析，核心创新是把依赖判断下沉到实际执行 block 粒度，在仍可扩展的表示中同时暴露跨算子融合与隐藏并行。
  - ML Compiler、Block-level Dependency、Inter-operator Optimization、GPU Parallelism、Memory Access Optimization

- [Pruner: A Draft-then-Verify Exploration Mechanism to Accelerate Tensor Program Tuning](https://doi.org/10.1145/3676641.3716269)
  - Liang Qiao (University of Science and Technology of China), Jun Shi (University of Science and Technology of China), Xiaoyu Hao (University of Science and Technology of China), Xi Fang (University of Science and Technology of China), Sen Zhang (University of Science and Technology of China), Minfan Zhao (University of Science and Technology of China), Ziqi Zhu (University of Science and Technology of China), Junshi Chen (University of Science and Technology of China), Hong An (University of Science and Technology of China), Xulong Tang (University of Pittsburgh), Bing Li (NIO), Honghui Yuan (NIO), Xinyang Wang (NIO)
  - Pruner 为 GPU tensor program auto-tuning 先用低成本 symbolic analyzer 生成大量候选并排除不可行配置，learned cost model 只对 shortlist 做昂贵验证；迁移到新 GPU 时，Mixture-of-Adaptations 通过带 momentum 的在线更新组合已有知识与少量新测量。
  - 相较让 cost model 为全部候选打分、且跨 GPU 需重新离线训练，核心创新是 draft-then-verify 两级筛选加在线多源适配，同时降低搜索调用量与新硬件冷启动成本。
  - Tensor Program Auto-tuning、Draft-then-Verify、Symbolic Pruning、Cross-GPU Cost Model、Online Adaptation

- [Relax: Composable Abstractions for End-to-End Dynamic Machine Learning](https://doi.org/10.1145/3676641.3716249)
  - Ruihang Lai (Carnegie Mellon University), Junru Shao (OpenAI), Siyuan Feng (Shanghai Jiao Tong University), Steven Lyubomirsky (NVIDIA), Bohan Hou (Carnegie Mellon University), Wuwei Lin (OpenAI), Zihao Ye (University of Washington), Hongyi Jin (Carnegie Mellon University), Yuchen Jin (Hyperbolic), Jiawei Liu (University of Illinois Urbana-Champaign), Lesheng Jin (Hyperbolic), Yaxing Cai (NVIDIA), Ziheng Jiang (ByteDance), Yong Wu (NVIDIA), Sunghyun Park (NVIDIA), Prakalp Srivastava (Netflix), Jared Roesch (NVIDIA), Todd C. Mowry (Carnegie Mellon University), Tianqi Chen (Carnegie Mellon University,NVIDIA)
  - Relax 为动态 shape 的端到端 ML workload 提供跨层 compiler IR，在同一表示中组合 computation graph、loop-level tensor program 与 external library call；first-class symbolic shape 在全程序追踪尺寸关系，使 graph—kernel—library 间可以做 dynamic-shape-aware optimization，并部署到 GPU、手机、嵌入式和浏览器。
  - 相较 graph IR、tensor IR 与外部库各自优化，核心创新是用可组合跨层抽象和全局 symbolic shape 同时连接这些层级，避免动态尺寸在接口处丢失。
  - ML Compiler、Dynamic Shape、Cross-level IR、Symbolic Shape Analysis、端到端模型部署

- [Towards End-to-End Optimization of LLM-based Applications with Ayo](https://doi.org/10.1145/3676641.3716278)
  - Xin Tan (The Chinese University of Hong Kong), Yimin Jiang (Unaffiliated), Yitao Yang (The Chinese University of Hong Kong), Hong Xu (The Chinese University of Hong Kong)
  - Ayo 优化同时包含 LLM 与非 LLM module 的应用工作流，把每个 query 展开为 task-primitive 级 dataflow graph；orchestrator 因而能跨 module 发现 primitive 间的 parallelism 和 pipeline，并按端到端 latency 调度，而不是只优化各 module 内部。
  - 相较以粗粒度 task module 为最小编排单位，核心创新是暴露跨模块 primitive dependency，使原本被接口边界遮蔽的并行、流水和调度空间可统一利用。
  - Agent Infra、LLM-based Applications、Primitive-level Dataflow、Cross-module Pipelining、End-to-end Orchestration

- [PAPI: Exploiting Dynamic Parallelism in Large Language Model Decoding with a Processing-In-Memory-Enabled Computing System](https://doi.org/10.1145/3676641.3716009)
  - Yintao He (SKLP, Institute of Computing Technology, CAS,University of Chinese Academy of Sciences), Haiyu Mao (King's College London,ETH Zürich), Christina Giannoula (University of Toronto,Vector Institute), Mohammad Sadrosadati (ETH Zürich), Juan Gómez-Luna (NVIDIA), Huawei Li (SKLP, Institute of Computing Technology, CAS,University of Chinese Academy of Sciences), Xiaowei Li (SKLP, Institute of Computing Technology, CAS,University of Chinese Academy of Sciences), Ying Wang (SKLP, Institute of Computing Technology, CAS), Onur Mutlu (ETH Zürich)
  - PAPI（PA rallel Decoding with PI M）是一种支持 PIM 的异构架构，它利用将计算限制或内存限制内核动态调度到合适的硬件单元来加速 LLM 解码，同时考虑所涉及内核的动态变化特征。
  - LLM decode kernel 会随 batch、sequence 与系统状态在 compute-bound/memory-bound 间变化，静态 GPU/PIM mapping 很快失配；PAPI（PA rallel Decoding with PI M），这是一种支持 PIM 的异构架构，它利用计算限制或内存限制内核到合适的硬件单元的动态调度。
  - LLM Decoding、PIM/GPU 异构执行、Dynamic Kernel Mapping、Compute/Memory-bound Classification、运行时异构调度

- [PIM is All You Need: A CXL-Enabled GPU-Free System for LLM Inference](https://doi.org/10.1145/3676641.3716267)
  - Yufeng Gu (University of Michigan), Alireza Khadem (University of Michigan), Sumanth Umesh (University of Michigan), Ning Liang (University of Michigan), Xavier Servot (ETH Zurich), Onur Mutlu (ETH Zurich), Ravi Iyer (Google), Reetuparna Das (University of Michigan)
  - CENT，一种用于 LLM 推理的 CXL-ENabled GPU-Free 系统，它利用 CXL 内存扩展功能来适应大量的 LLM 大小，并利用近库处理单元来提供高内存带宽，从而无需昂贵的 GPU。
  - 继续增加 GPU 算力不能解决 decode 的容量/带宽瓶颈；CENT 用 CXL 扩展模型与 KV 容量、以 near-bank unit 提供带宽，并在多 CXL device 上实现 peer-to-peer/collective 与模型并行。
  - LLM 系统、在线模型推理、CXL 内存/互连、GPU 系统、存内/近存计算、PIM/CIM System

- [CINM (Cinnamon): A Compilation Infrastructure for Heterogeneous Compute In-Memory and Compute Near-Memory Paradigms](https://doi.org/10.1145/3622781.3674189)
  - Asif Ali Khan (Technische Universität Dresden), Hamid Farzaneh (Technische Universität Dresden), Karl Friedrich Alexander Friebel (Technische Universität Dresden), Clément Fournier (Technische Universität Dresden), Lorenzo Chelini (Intel), Jeronimo Castrillon (Technische Universität Dresden)
  - Cinnamon 用分层 IR 编译 compute-in/near-memory 程序：上层先表达与设备无关的数据移动和并行语义，随后逐级降低为设备感知表示，并在每层应用匹配的布局、通信与算子优化；同一流程可落到 UPMEM PIM 与 memristor CIM 等不同目标。
  - 相较每种近存/存内设备维护独立编程模型与编译器，核心创新是用逐层细化的共同 IR 覆盖异质器件，同时保留各层可做的设备专属优化。
  - CIM/PIM Compiler、Hierarchical IR、UPMEM、Memristor、异构近存计算

- [Toleo: Scaling Freshness to Tera-scale Memory Using CXL and PIM](https://doi.org/10.1145/3622781.3674180)
  - Juechu Dong (University of Michigan), Jonah Rosenblum (University of Michigan), Satish Narayanasamy (University of Michigan)
  - Toleo 不再需要使用不可扩展的 Merkle 树来保护版本号的完整性，而是使用智能内存作为信任根，从而实现隐形版本，从而将版本存储开销减少一半。
  - 大容量可信内存用 Merkle tree 维护每条 cache line 的版本完整性，树访问随容量扩展到 TB 后不可承受；Toleo，它使用通过安全 CXL IDE 网络连接的可信智能内存来安全存储版本号。
  - CXL 内存/互连、存内/近存计算、PIM/CIM System、Memory-centric Model Execution、Compiler/Runtime Mapping

- [Be CIM or Be Memory: A Dual-mode-aware DNN Compiler for CIM Accelerators](https://doi.org/10.1145/3676641.3716248)
  - Shixin Zhao (Institute of Computing Technology, Chinese Academy of Sciences,University of Chinese Academy of Sciences), Yuming Li (Institute of Computing Technology, Chinese Academy of Sciences,University of Chinese Academy of Sciences), Bing Li (Institute of Microelectronics, Chinese Academy of Sciences), Yintao He (Institute of Computing Technology, Chinese Academy of Sciences,University of Chinese Academy of Sciences), Mengdi Wang (State Key Lab of Processors, Institute of Computing Technology, Chinese Academy of Sciences), Yinhe Han (State Key Lab of Processors, Institute of Computing Technology, Chinese Academy of Sciences), Ying Wang (State Key Lab of Processors, Institute of Computing Technology, Chinese Academy of Sciences)
  - CMSwitch 把 CIM bank 的 compute/memory mode 纳入 compiler resource-allocation space：hardware abstraction 显式标记双模式能力，dynamic programming 与 mixed-integer programming 联合选择 network segment、切换点和各模式资源，meta-operator 表达最终 schedule。
  - 现有 CIM compiler 固定 bank 角色，无法按 layer 的算存需求回收资源；CMSwitch 首次把 mode switch、network segment 与资源配额放进同一 DP/MIP 搜索空间。
  - CIM Compiler、Compute/Memory Dual Mode、DP/MIP Resource Allocation、DNN/LLM Mapping、Adaptive Mode Switching

- [RTL Verification for Secure Speculation Using Contract Shadow Logic](https://doi.org/10.1145/3669940.3707243)
  - Qinhan Tan (Princeton University), Yuheng Yang (Massachusetts Institute of Technology), Thomas Bourgeat (École Polytechnique Fédérale de Lausanne), Sharad Malik (Princeton University), Mengjia Yan (Massachusetts Institute of Technology)
  - Contract Shadow Logic 把 secure-speculation 的 software-hardware contract 编译成与 RTL 并行执行的 shadow state/logic，用体系结构语义提前聚合安全相关状态；同一验证框架可在多种乱序核和 defense 上找攻击或给完整 proof。
  - 通用 RTL model checking 面对 OOO speculation 状态爆炸；Contract Shadow Logic 把软硬件 security contract 编成随 RTL 执行的 shadow logic，以体系结构约束缩小 proof state 且复用于多种 defense。
  - 形式化验证、Hardware/Software Verification、Crash/SDC Detection、RTL Security Proof、Runtime Reliability

- [ElasticMiter: Formally Verified Dataflow Circuit Rewrites](https://doi.org/10.1145/3676641.3715993)
  - Ayatallah Elakhras (EPFL), Jiahui Xu (ETH Zurich), Martin Erhart (ETH Zurich), Paolo Ienne (EPFL), Lana Josipovic (ETH Zurich)
  - ElasticMiter 为 latency-insensitive dataflow circuit 定义适用的等价性验证框架，并用它证明一组 graph rewrite 在改变 token 时序/缓冲结构后仍保持功能；经验证的 rewrite 再系统地简化 HLS 生成 datapath。
  - 相较直接套用要求逐周期对应的 sequential equivalence，核心创新是为数据流电路建立弹性时序语义下的 miter，使优化 rewrite 可组合且带形式化正确性保证。
  - Dataflow Circuit、Formal Equivalence、Graph Rewriting、High-level Synthesis、Verified Compiler Optimization

- [Robustness Verification for Checking Crash Consistency of Non-volatile Memory](https://doi.org/10.1145/3669940.3707269)
  - Zhilei Han (School of Software, Tsinghua University), Fei He (School of Software, Tsinghua University)
  - PMVerify 把 NVM crash consistency 表述为 robustness：给定 pre-crash execution 后，post-crash persistent state 的可达性被化为附加持久化顺序约束的执行有效性；search-based symbolic encoding 与 SMT/DPLL(T) 枚举 partial execution 并返回 violation。
  - 测试式 crash checker 依赖人工选择 crash point；PMVerify 把 post-crash reachability 归约为 ordering-constrained pre-crash validity，并在 DPLL(T) 内系统探索所有 partial execution。
  - 形式化验证、Hardware/Software Verification、Crash/SDC Detection、RTL Security Proof、Runtime Reliability

- [Proactive Runtime Detection of Aging-Related Silent Data Corruptions: A Bottom-Up Approach](https://doi.org/10.1145/3622781.3674182)
  - Jiacheng Ma (University of Michigan), Majd Ganaiem (Technion – Israel Institute of Technology), Madeline Burbage (University of Washington), Theo Gregersen (University of Washington), Rachel McAmis (University of Washington), Freddy Gabbay (The Hebrew University of Jerusalem), Baris Kasikci (University of Washington,Google)
  - Vega 是一种工作流程，可以在软件运行时有效检测与老化相关的故障，生成有效的测试用例并将其集成到应用程序中，平均性能开销为 0.8%。
  - 老化相关 SDC 通常靠出厂/离线硬件测试，无法在具体应用运行时主动触发并定位正在退化的电路；Vega，一种工作流程，可以在软件运行时有效检测与老化相关的故障。
  - Hardware/Software Verification、Crash/SDC Detection、RTL Security Proof、Runtime Reliability

- [Hardware Sentinel: Protecting Software Applications from Hardware Silent Data Corruptions](https://doi.org/10.1145/3676641.3716258)
  - Rhea Dutta (Meta Platforms, Inc.), Harish Dattatraya Dixit (Meta Platforms, Inc.), Rik Van Riel (Meta Platforms, Inc.), Gautham Vunnam (Meta Platforms, Inc.), Sriram Sankar (Meta Platforms, Inc.)
  - Hardware Sentinel 从应用层 segmentation fault、core dump、crash 与 kernel log 中提取和硬件 SDC 高相关的 failure signature，并跨机型、kernel、workload 与 region 聚合验证；六年 fleet 数据定位数百颗 defect CPU。
  - 器件侧离线测试无法覆盖 workload/environment 才触发的 SDC；Hardware Sentinel 反向利用生产软件 failure indicator 做 top-down fleet 筛查，并跨六年数据校准关联。
  - Hardware/Software Verification、Crash/SDC Detection、RTL Security Proof、Runtime Reliability

- [TensorTEE: Unifying Heterogeneous TEE Granularity for Efficient Secure Collaborative Tensor Computing](https://doi.org/10.1145/3622781.3674168)
  - Husheng Han (SKLP, Institute of Computing Technology, Chinese Academy of Sciences,University of Chinese Academy of Sciences), Xinyao Zheng (SKLP, Institute of Computing Technology, Chinese Academy of Sciences,University of Chinese Academy of Sciences ), Yuanbo Wen (SKLP, Institute of Computing Technology, Chinese Academy of Sciences), Yifan Hao (SKLP, Institute of Computing Technology, Chinese Academy of Sciences), Erhu Feng (IPADS, Shanghai Jiao Tong University,Engineering Research Center for Domain-specific Operating Systems (MoE)), Ling Liang (Peking university), Jianan Mu (SKLP, Institute of Computing Technology, Chinese Academy of Sciences,University of Chinese Academy of Sciences ), Xiaqing Li (SKLP, Institute of Computing Technology, Chinese Academy of Sciences), Tianyun Ma (SKLP, Institute of Computing Technology, Chinese Academy of Sciences,Cambricon Technologies), Pengwei Jin (SKLP, Institute of Computing Technology, Chinese Academy of Sciences,University of Chinese Academy of Sciences ), Xinkai Song (SKLP, Institute of Computing Technology, Chinese Academy of Sciences), Zidong Du (SKLP, Institute of Computing Technology, Chinese Academy of Sciences,Shanghai Innovation Center for Processor Technologies, SHIC), Qi Guo (SKLP, Institute of Computing Technology, Chinese Academy of Sciences), Xing Hu (SKLP, Institute of Computing Technology, Chinese Academy of Sciences,ZGC LAB)
  - TensorTEE 是一种用于高效安全协作张量计算的统一张量粒度异构 TEE，可实现直接数据传输，无需重新加密和调度困境，并将大型语言模型训练工作负载的性能比现有工作提高 4.0 倍。
  - CPU/NPU TEE 的保护粒度不同，跨 enclave tensor 传输需要片外元数据、重加密和额外调度；首先，该工作实际上支持 CPU TEE 中的张量粒度，通过检测和维护片上张量结构来消除片外元数据访问。
  - Heterogeneous TEE、Tensor-granularity Protection、CPU-NPU Collaborative Computing、Direct Secure Transfer、LLM Training Security

- [MDPeek: Breaking Balanced Branches in SGX with Memory Disambiguation Unit Side Channels](https://doi.org/10.1145/3676641.3716004)
  - Chang Liu (Tsinghua University), Shuaihu Feng (Zhongguancun Laboratory), Yuan Li (Zhongguancun Laboratory), Dongsheng Wang (Tsinghua University), Wenjian He (Huawei Technologies Co., Ltd.), Yongqiang Lyu (Tsinghua University), Trevor E. Carlson (National University of Singapore)
  - MDPeek 逆向 Intel SGX memory-disambiguation unit 的启用/更新逻辑，利用其状态区分 secret-dependent balanced branch；端到端攻击覆盖 Libjpeg、MbedTLS、WolfSSL，store-to-load coupling mitigation 比串行化/对齐 load 的延迟低 7 倍。
  - flush 与 branch balancing 只覆盖已知 predictor/cache channel；MDPeek 将此前未建模的 MDU 变成控制流泄漏源，并给出针对该状态机的低开销 store-to-load coupling。
  - 微体系结构安全、Trusted/Verifiable Computing、TEE/ZKP Acceleration、Secure Tensor/Data Pipeline、Cryptographic Hardware

- [Accelerating Number Theoretic Transform with Multi-GPU Systems for Efficient Zero Knowledge Proof](https://doi.org/10.1145/3669940.3707241)
  - Zhuoran Ji (School of Cyber Science and Technology, Shandong University), Jianyu Zhao (School of Cyber Science and Technology, Shandong University), Peimin Gao (School of Cyber Science and Technology, Shandong University), Xiangkai Yin (School of Cyber Science and Technology, Shandong University), Lei Ju (Quan Cheng Laboratory)
  - UniNTT 把多 GPU NTT 递归分解成相同形式的小 NTT，让 warp、thread block、单 GPU 与 GPU 间各层都运行同一抽象算法；再针对每层互连定制 data permutation/communication，8 GPU 上平均加速 4.26 倍。
  - 传统 multi-GPU NTT 为每个 hierarchy level 手写不同 permutation，跨卡通信难复用优化；UniNTT 的零额外开销递归分解统一各层 computation，再按抽象硬件模型迁移同一组优化。
  - GPU 系统、零知识证明加速、Trusted/Verifiable Computing、TEE/ZKP Acceleration、Secure Tensor/Data Pipeline

- [BatchZK: A Fully Pipelined GPU-Accelerated System for Batch Generation of Zero-Knowledge Proofs](https://doi.org/10.1145/3669940.3707270)
  - Tao Lu (Zhejiang University,National University of Singapore), Yuxun Chen (Zhejiang University), Zonghui Wang (Zhejiang University), Xiaohang Wang (Zhejiang University), Wenzhi Chen (Zhejiang University), Jiaheng Zhang (National University of Singapore)
  - 用于批量生成零知识证明的全流水线 GPU 加速系统，与最先进的 GPU 加速系统相比，吞吐量提高了 259.5 倍以上，并在该领域首次实现了亚秒级证明生成。
  - 既有 GPU ZKP 主要压低单个 proof latency，线程在阶段切换和 host-device 传输期间空闲，批吞吐不足；首先，该工作设计了一种流水线方法，使每个 GPU 线程能够连续执行其指定的证明生成任务而不会空闲。
  - ZKP Batch Generation、GPU Full Pipeline、Sum-check/Merkle/Encoder、Multi-stream Transfer Overlap、Verifiable ML

- [UniZK: Accelerating Zero-Knowledge Proof with Unified Hardware and Flexible Kernel Mapping](https://doi.org/10.1145/3669940.3707228)
  - Cheng Wang (Xi'an Jiaotong University,Institute for Interdisciplinary Information Core Technology), Mingyu Gao (Tsinghua University,Shanghai Qi Zhi Institute)
  - UniZK 为 elliptic-curve 与 hash-based ZKP 共享一套 accelerator：systolic array 增加局部互连和 vector mode，把 NTT、hash 与 polynomial arithmetic 映射为可复用数据流，而不是给每个协议/算子配置独立模块。控制器按证明阶段切换阵列模式并复用片上存储。
  - 相较为单一 ZKP 协议定制固定功能单元，核心创新是用少量可重构互连与映射规则让同一阵列覆盖两类证明体系及其异质 kernel，提升跨协议利用率。
  - 零知识证明加速、Unified ZKP Accelerator、Systolic Array、NTT/Hash/Polynomial、可重构数据流

- [Litmus: Fair Pricing for Serverless Computing](https://doi.org/10.1145/3622781.3674181)
  - Qi Pei (Computer Science / Watson School, The State University of New York at Binghamton), Yipeng Wang (Intel Lab., Intel), Seunghee Shin (Computer Science / Watson School, The State University of New York at Binghamton)
  - Litmus 处理 serverless 共置过载导致函数变慢、租户反而因执行时间增长付更多钱的问题。平台周期性运行轻量 litmus test 估计当前机器拥塞程度，再按该状态推断租户损失并给予折扣，无需预先 profiling 每个函数。
  - 相较仍按受干扰后的 wall-clock time 全额计费，核心创新是以机器侧可观测的 congestion index 代理不可见的函数 slowdown，把运营方超卖造成的损失返还给租户。
  - Serverless Pricing、Co-location Interference、Machine-state Litmus Test、Slowdown Compensation、公平云计费

- [Concurrency-Informed Orchestration for Serverless Functions](https://doi.org/10.1145/3676641.3716253)
  - Qichang Liu (University of Virginia), Yue Cheng (University of Virginia), Haiying Shen (University of Virginia), Ao Wang (Alibaba Group), Bharathan Balaji (Amazon)
  - CIDRE 面向同一 serverless function 的并发 invocation：当所有 warm container 忙碌时，它预测等待复用现有实例还是立即 cold-start 新实例更快；回收内存时同时利用 container 级复用历史和 function 并发度，避免刚驱逐马上又要用的实例。
  - 相较仅按最近一次调用时间决定 keep-alive/eviction，核心创新是把并发造成的 busy-container wait 与 scale-out cold start 显式比较，并让驱逐在函数间保持平衡。
  - Serverless Container Orchestration、Concurrency-aware Keep-alive、Cold Start、Warm-container Reuse、Balanced Eviction

- [Dilu: Enabling GPU Resourcing-on-Demand for Serverless DL Serving via Introspective Elasticity](https://doi.org/10.1145/3669940.3707251)
  - Cunchi Lv (ICT, CAS,UCAS), Xiao Shi (ICT, CAS,Nanjing Institute of InforSuperBahn), Zhengyu Lei (ICT, CAS,UCAS), Jinyue Huang (ICT, CAS, UCAS), Wenting Tan (ICT, CAS), Xiaohui Zheng (ICT, CAS), Xiaofang Zhao (ICT, CAS,IICT, Suzhou, CAS)
  - Dilu 为 serverless DL 训推函数提供 GPU resource-on-demand：multi-factor profiler 用剪枝搜索得到不同资源配置的性能，scheduler 优先共置资源互补任务；运行时再同时横向调实例数、纵向调单实例 GPU 份额，随负载修复 15%–94% 的静态分配碎片。
  - 相较只做横向 function autoscaling 或给容器固定 GPU slice，核心创新是 introspective elasticity：依据模型 profile 联合做水平—垂直二维扩缩，并以互补共置守住 QoS。
  - Serverless DL Serving/Training、GPU On-demand Resourcing、2D Co-scaling、GPU Defragmentation、QoS-aware Colocation

- [Medusa: Accelerating Serverless LLM Inference with Materialization](https://doi.org/10.1145/3669940.3707285)
  - Shaoxun Zeng (Tsinghua University), Minhui Xie (Tsinghua University), Shiwei Gao (Tsinghua University), Youmin Chen (Tsinghua University), Youyou Lu (Tsinghua University)
  - Medusa 面向 serverless LLM inference 的冷启动，把 KV-cache 容量 profiling 信息和不同 batch size 的 CUDA graph 在离线阶段 materialize，在线只恢复；offline/online 协同恢复参数，并用 triggering kernel 重新定位非确定的 kernel address，使十个模型的 CUDA graph 可跨实例复用。
  - 相较每次函数启动都重新 profile KV cache、动态 capture CUDA graph，核心创新是把这两类依赖具体模型/批量的运行时初始化变成可持久化、可修复地址的离线状态。
  - Serverless LLM Inference、CUDA Graph Materialization、KV-cache Initialization、Cold Start、TTFT

- [Virgo: Cluster-level Matrix Unit Integration in GPUs for Scalability and Energy Efficiency](https://doi.org/10.1145/3676641.3716281)
  - Hansung Kim (University of California, Berkeley), Ruohan Richard Yan (University of California, Berkeley), Joshua You (University of California, Berkeley), Tieliang Vamber Yang (NVIDIA Corporation), Yakun Sophia Shao (University of California, Berkeley)
  - Virgo 是一种在 SIMT 核心集群级别集成专用矩阵单元的 GPU 微架构，消除了核心微架构带来的可扩展性限制，并增加了硬件级别的操作粒度，减少了核心指令处理的能量开销。
  - GPU matrix unit 紧耦合单个 SIMT core 和 register file，operand/accumulator 带宽限制了矩阵操作粒度；为了应对这一挑战，采用 Virgo，一种在 SIMT 核心集群级别集成专用矩阵单元的 GPU 微架构。
  - GPU Matrix-unit Architecture、Cluster-level Tensor Core、Register-file Bypass、Fused DNN Mapping、Energy Efficiency

- [Towards Unified Analysis of GPU Consistency](https://doi.org/10.1145/3622781.3674174)
  - Haining Tong (University of Helsinki), Natalia Gavrilenko (Huawei Dresden Research Center), Hernan Ponce de Leon (Huawei Dresden Research Center), Keijo Heljanko (University of Helsinki,Helsinki Institute for Information Technology)
  - Dartagnan 是第一个多 GPU 一致性模型的分析工具，可以分析真实的 GPU 代码，并发现了原始 Ptx 和 Vulkan 一致性模型中的两个 bug。
  - PTX 与 Vulkan consistency model 各有形式规范，但工具分散且难直接检查真实 multi-GPU code；这使得 Dartagnan 成为第一个可以分析真实 GPU 代码的多 GPU 一致性模型的分析工具。
  - GPU 系统、GPU 内存一致性模型、GPU Architecture/Runtime、Matrix/Relational Kernel、GPU Consistency

- [Aqua: Network-Accelerated Memory Offloading for LLMs in Scale-Up GPU Domains](https://doi.org/10.1145/3676641.3715983)
  - Abhishek Vijaya Kumar (Cornell University), Gianni Antichi (Politecnico di Milano), Rachee Singh (Cornell University)
  - Aqua 在 8-GPU scale-up server 上让高负载 LLM prompt 可被时间片抢占，但不把 KV/inference state 通过 host 慢速 paging；它利用节点内高速网络把状态卸载到其他 GPU/内存端点并加速回迁，在 burst 时兼顾响应性与吞吐。实验将响应性提高 20 倍、单长 prompt 吞吐提高 4 倍。
  - 相较用 admission control 拒绝/排队新请求，或抢占后经 CPU 交换 KV，核心创新是以 scale-up network 作为 GPU memory offload fabric，使 preemptive prompt scheduling 实际可用。
  - LLM Serving、KV/Inference-state Offloading、Network-accelerated Paging、Prompt Preemption、Scale-up GPU

- [Optimizing Datalog for the GPU](https://doi.org/10.1145/3669940.3707274)
  - Yihao Sun (Syracuse University), Ahmedur Rahman Shovon (University of Illinois, Chicago), Thomas Gilray (Washington State University), Sidharth Kumar (University of Illinois, Chicago), Kristopher Micinski (Syracuse University)
  - GPUlog 将 Datalog 的 semi-naive recursive evaluation 编译为 GPU 上反复执行的 relational-algebra kernel，并以 hash-indexed sorted array 同时支持增量 range lookup 与连续 dense operation；在 context-sensitive points-to analysis 等任务上较 CPU Soufflé 最多加速 45 倍。
  - 相较把通用 GPU join 简单串接成递归查询，核心创新是为 Datalog 增量关系设计 HISA 数据结构和迭代 kernel backend，在索引能力、并行吞吐和显存占用间协同。
  - Datalog Engine、GPU Query Processing、Semi-naive Evaluation、Hash-indexed Sorted Array、Static Analysis

- [MaxEmbed: Maximizing SSD bandwidth utilization for huge embedding models serving](https://doi.org/10.1145/3622781.3674172)
  - Ruwen Fan (Tsinghua University), Minhui Xie (Tsinghua University), Haodi Jiang (Tsinghua University), Youyou Lu (Tsinghua University)
  - MaxEmbed 在 SSD 上存放超出 DRAM 的 DLRM embedding table，并允许受控复制热点 embedding：离线布局让经常共同访问的条目可同时分布到多个 SSD channel，在线服务再选择 replica、合并查询并限制复制带来的额外读取。它利用空闲容量换并行带宽，吞吐提高 18.7%。
  - 相较用 hypergraph partition 把每个 embedding 只放一次、共同访问集合受互斥分区限制，核心创新是允许重叠复制，使高频组合可同时跨盘并行而不必完全消除 read amplification。
  - Recommendation Serving、SSD-resident Embeddings、Controlled Replication、Parallel I/O、DLRM

- [AnyKey: A Key-Value SSD for All Workload Types](https://doi.org/10.1145/3669940.3707279)
  - Chanyoung Park (Hanyang University), Jungho Lee (Hanyang University), Chun-Yi Liu (Micron Technology Inc.), Kyungtae Kang (Hanyang Univeristy), Mahmut Taylan Kandemir (Pennsylvania State University), Wonil Choi (Hanyang University)
  - AnyKey 重新设计 KV-SSD metadata，使索引空间不随 key length 线性膨胀；同一设备因此能同时处理传统 small-key/large-value 和 large-key workload，而不必为某一类 key/value 比例重配数据结构。
  - 既有 KV-SSD metadata 为小 key 假设定型，key 一大索引即膨胀；AnyKey 改变 metadata organization，使 key/value 尺寸变化不再决定设备可服务的 workload 类型。
  - SSD/Flash 存储、SSD/Flash System、Key-value/Embedding Storage、Embedded Flash Runtime、I/O Layout/Cache

- [Simplifying and Accelerating NOR Flash I/O Stack for RAM-Restricted Microcontrollers](https://doi.org/10.1145/3676641.3716272)
  - Hao Huang (Harbin Institute of Technology, Shenzhen), Yanqi Pan (Harbin Institute of Technology, Shenzhen), Wen Xia (Harbin Institute of Technology, Shenzhen), Xiangyu Zou (Harbin Institute of Technology, Shenzhen), Darong Yang (Harbin Institute of Technology, Shenzhen), Liang Shi (East China Normal University), Hongwei Du (Harbin Institute of Technology, Shenzhen)
  - NF2FS 面向 RAM 极少的 microcontroller NOR flash，把小文件从 block organization 改为 flat file layout，并利用应用较确定的 I/O pattern 以 coarse file swapping 做 wear leveling；all-logging layout、dual-bitmap allocator 与 soft-update-like consistency 共同减少索引更新和全盘扫描。
  - 相较把 block index 和 wear-leveling metadata 细粒度写回 NOR，核心创新是把数据组织与磨损均衡统一提升到文件粒度，以应用结构换取更少写放大和 RAM 状态。
  - NOR Flash File System、RAM-constrained MCU、File-level Wear Leveling、Logging Layout、Write Amplification

- [A Software Caching Runtime for Embedded NVRAM Systems](https://doi.org/10.1145/3622781.3674183)
  - Harrison Williams (Virginia Tech), Matthew Hicks (Virginia Tech)
  - 为了消除这一性能瓶颈，采用 SwapRAM，这是一种针对基于 NVRAM 的平台的新操作模型，它将未充分利用的 SRAM 重新用作指令缓存，从而最大限度地提高针对高性能 SRAM 的访问比例。
  - 硬件 cache 固定且 instruction 仍频繁从慢 NVRAM 获取；SwapRAM 由 compile-time transform 与 runtime manager 透明搬移 hot code 到空闲 SRAM，并按热度延迟逐出。
  - Cache 管理、SSD/Flash System、Key-value/Embedding Storage、Embedded Flash Runtime、I/O Layout/Cache

- [Velosiraptor: Code Synthesis for Memory Translation](https://doi.org/10.1145/3676641.3711998)
  - Reto Achermann (University of British Columbia), Em Chu (JuliaHub), Ryan Mehri (Replit), Ilias Karimalis (University of British Columbia), Margo Seltzer (University of British Columbia)
  - Velosiraptor 是一个自动生成正确的低级操作系统代码的系统，用于对机器的内存硬件进行编程，并将操作系统环境纳入此过程中，允许将操作系统移植到新的硬件平台，而无需担心编写代码来配置内存硬件。
  - OS 为每种 memory-translation/protection hardware 手写底层配置代码，重复且容易破坏隔离保证；Velosiraptor，这是一个可以自动生成正确的低级操作系统代码的系统，该代码可以对机器的内存硬件进行编程。
  - 编译器与代码生成、虚拟内存与地址翻译、Virtual Memory System、Address Translation/TLB、OS/Architecture Simulation

- [vAttention: Dynamic Memory Management for Serving LLMs without PagedAttention](https://doi.org/10.1145/3669940.3707256)
  - Ramya Prabhu (Microsoft Research), Ajay Nayak (Indian Institute of Science), Jayashree Mohan (Microsoft Research), Ramachandran Ramjee (Microsoft Research), Ashish Panwar (Microsoft Research)
  - vAttention 继续按需分配 LLM KV cache 的物理 GPU page，但用 CUDA virtual memory API 让每个 request 在虚拟地址上保持连续；attention kernel 因而无需理解 PagedAttention 的非连续 page table。LLM-specific 映射优化使现有 FlashAttention-2/FlashInfer 可直接使用，吞吐最高提高 1.23 倍。
  - 相较为动态物理分配而同时破坏虚拟连续性的 PagedAttention，核心创新是解耦 virtual/physical allocation：在保留消除碎片能力时恢复普通连续 KV layout。
  - LLM Serving、KV Cache Memory、CUDA Virtual Memory、PagedAttention Alternative、Attention Kernel Compatibility

- [Virtuoso: Enabling Fast and Accurate Virtual Memory Research via an Imitation-based Operating System Simulation Methodology](https://doi.org/10.1145/3676641.3716027)
  - Konstantinos Kanellopoulos (ETH Zürich), Konstantinos Sgouras (ETH Zürich), Nisa Bostanci (ETH Zürich), Andreas Kosmas Kakolyris (ETH Zürich), Berkin Kerim Konar (ETH Zürich), Rahul Bera (ETH Zürich), Mohammad Sadrosadati (ETH Zürich), Rakesh Kumar (Norwegian University of Science and Technology (NTNU)), Nandita Vijaykumar (University of Toronto), Onur Mutlu (ETH Zürich)
  - 该工作将 Virtuoso 集成到五个不同的架构模拟器中，每个模拟器专门从事系统设计的不同方面，并通过多种最先进的 VM 方案大大丰富了它，为研究人员评估当前 VM 设计以及开发和测试新的 VM 设计建立了共同基础。
  - 现有 VM simulator 要么省略 OS 软件路径而不准，要么运行完整内核而难以快速修改硬软协同方案；Virtuoso 的关键思想是采用名为 MimicOS 的轻量级用户空间操作系统内核，它 (i) 通过仅模仿所需的内核功能来加速仿真时间，(ii) 使用可访问的高级编程接口，促进模仿真实操作系统例程的新操作系统例程的开发，(iii) 在将 Virtuoso 集成到所需的架构模拟器后，能够准确、灵活地评估 VM 的应用程序级和系统级影响。
  - 虚拟内存与地址翻译、Virtual Memory System、Address Translation/TLB、OS/Architecture Simulation、Page-table/Cache Policy

- [Instruction-Aware Cooperative TLB and Cache Replacement Policies](https://doi.org/10.1145/3669940.3707247)
  - Dimitrios Chasapis (Barcelona Supercomputing Center (BSC)), Georgios Vavouliotis (Unaffiliated), Daniel A. Jiménez (Texas A&M University), Marc Casas (Barcelona Supercomputing Center (BSC),Universitat Politècnica de Catalunya (UPC))
  - 指令翻译优先级（iTP）和扩展页表优先级（xPTP），前者是一种 STLB 替换策略，它以增加数据页遍历为代价来最大化 STLB 中的指令命中数，后者是一种新的 L2C 替换策略，可以通过有效减少数据页遍历导致的 L2C 缺失来放大 iTP 的优势。
  - 通用 LRU 同等对待 instruction/data translation；大 instruction footprint 下 iTLB miss 会直接停住 pipeline；指令翻译优先级（iTP），这是一种 STLB 替换策略，它以增加数据页遍历为代价来最大化 STLB 中的指令命中数量。
  - Cache 管理、虚拟内存与地址翻译、运行时调度与放置、Virtual Memory System、Address Translation/TLB
