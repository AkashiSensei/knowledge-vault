# ICDCS 2024 论文列表

ICDCS 2024 主会 Regular/Main Technical Sessions 共收录 121 篇研究论文；已排除 workshop、poster、demo、doctoral consortium 和 industry event。标题链接指向 DOI/IEEE 文章页（无 DOI 的少数 2026 议程论文链至官方主会程序）；已找到的 3 份合法公开 PDF 保存在 `reference/ICDCS/2024/`。

- [QUART: Latency-Aware FaaS System for Pipelining Large Model Inference](https://doi.org/10.1109/icdcs60910.2024.00010)
  - Yanying Lin, Yanbo Li, Shijie Peng, Yingfei Tang, Shutian Luo, Haiying Shen, Chengzhong Xu, Kejiang Ye；Shenzhen Institute of Advanced Technology,Chinese Academy of Sciences; Yale University; University of Virginia; University of Macau。
  - QUART 面向突发在线请求下的大模型流水线推理，按 stage 而不是整个模型识别队列积压的关键瓶颈，用基于请求波动传播的关键 stage 检测和动态副本调度扩容。两级参数缓存与 fork/copy-on-write 让 FaaS 副本在数秒内启动，避免大模型加载落在请求关键路径。
  - 相较按整个模型粗粒度扩容或固定分配流水线资源，核心创新是把突发请求在各 stage 的不均衡传播变成可在线观测、缓存和独立扩容的对象。
  - LLM Serving, Serverless/FaaS, Pipeline Parallelism, Stage-level Autoscaling, Parameter Cache

- [EdgeVPR: Transformer-Based Real-Time Video Person Re-Identification at the Edge](https://doi.org/10.1109/icdcs60910.2024.00011)
  - Meng Sun, Ju Ren, Yaoxue Zhang；BNRist, Tsinghua University,Department of Computer Science and Technology,Beijing,China。
  - EdgeVPR研究AI at the Edge中的「EdgeVPR：基于 Transformer 的边缘实时视频人员重新识别」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - Edge Computing, AI at the Edge, Distributed Systems

- [AdapCC: Making Collective Communication in Distributed Machine Learning Adaptive](https://doi.org/10.1109/icdcs60910.2024.00012)
  - Xiaoyang Zhao, Zhe Zhang, Chuan Wu；The University of Hong Kong,Department of Computer Science。
  - AdapCC研究AI Optimizations中的「AdapCC：使分布式机器学习中的集体通信具有适应性」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善通信量与同步等待。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - AI Optimizations, Distributed Systems

- [TrimCaching: Parameter-Sharing AI Model Caching in Wireless Edge Networks](https://doi.org/10.1109/icdcs60910.2024.00013)
  - Guanqiao Qu, Zheng Lin, Fangming Liu, Xianhao Chen, Kaibin Huang；University of Hong Kong,Department of Electrical and Electronic Engineering,Pok Fu Lam,Hong Kong SAR,China; Peng Cheng Laboratory,Shenzhen,China。
  - TrimCaching研究AI at the Edge中的「TrimCaching：无线边缘网络中的参数共享 AI 模型缓存」：在容量、层级和时延约束下决定哪些数据/模型状态应保留、迁移、复用或淘汰。题目明确的关键手段包括cache placement/reuse；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「TrimCaching：无线边缘网络中的参数共享 AI 模型缓存」中的特定状态、约束或操作变成一级设计对象。
  - Edge Computing, Caching, AI at the Edge, Distributed Systems

- [An ML-Accelerated Framework for Large-Scale Constrained Traffic Engineering](https://doi.org/10.1109/icdcs60910.2024.00014)
  - Cheng Gu, Xin Song, Ben Hok Ng, Qiao Xiang, Zehua Guo, Geng Li；Huawei Technologies; Xiamen University; Beijing Institute of Technology, Zhengzhou Research Institute BIT,Zhejiang Lab。
  - 该工作研究AI Optimizations中的「用于大规模约束流量工程的机器学习加速框架」：以 worker、model shard/layer、gradient 或 expert 为单位组织计算、集合通信、内存与容错状态。直接目标是改善吞吐、扩展性或资源效率。
  - 相较直接套用通用分布式策略，核心创新是把「用于大规模约束流量工程的机器学习加速框架」中的特定状态、约束或操作变成一级设计对象。
  - AI Optimizations, Distributed Systems

- [Portus: Efficient DNN Checkpointing to Persistent Memory with Zero-Copy](https://doi.org/10.1109/icdcs60910.2024.00015)
  - Yuanhao Li, Tianyuan Wu, Guancheng Li, Yanjie Song, Shu Yin；Shanghaitech University,China。
  - Portus研究AI Computing Techniques中的「Portus：通过零拷贝对持久内存进行高效 DNN 检查点」：以 block/object/record 或 checkpoint state 为单位，组织读写、编码、复制、索引或恢复路径。题目明确的关键手段包括zero-copy；直接目标是改善内存占用与数据复用。
  - 相较让 CPU/通用软件路径承担所有数据移动和控制，核心创新是把关键操作下沉到网络或硬件数据路径。
  - Checkpointing, AI Computing Techniques, Distributed Systems

- [Mega: More Efficient Graph Attention for GNNs](https://doi.org/10.1109/icdcs60910.2024.00016)
  - Weishu Deng, Jia Rao；The University of Texas at Arlington,Department of Computer Science and Engineering,Arlington,TX,USA。
  - Mega研究AI Computing Techniques中的「Mega：GNN 更高效的图注意力」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。题目明确的关键手段包括graph attention；直接目标是改善吞吐、扩展性或资源效率。
  - 相较直接套用通用分布式策略，核心创新是把「Mega：GNN 更高效的图注意力」中的特定状态、约束或操作变成一级设计对象。
  - Graph Learning Systems, AI Computing Techniques, Distributed Systems

<a id="voltage"></a>

- [When the Edge Meets Transformers: Distributed Inference with Transformer Models](https://doi.org/10.1109/icdcs60910.2024.00017)
  - Chenghao Hu, Baochun Li；University of Toronto,Department of Electrical and Computer Engineering。
  - Voltage 面向多台算力弱、互联带宽低的边缘设备协同执行 Transformer 推理；评测含早期 LLM GPT-2、BERT-Large 的文本分类和 ViT 的图像分类，并非专门针对自回归生成服务。它利用除 self-attention 外大多操作按 token position 独立的结构，按序列位置分割每层计算，再根据计算量和通信量选择分区方案，以减少设备间中间特征传输。
  - 相较假设高速 GPU interconnect 的 tensor parallelism 或需要大 batch 才能填满的 pipeline parallelism，核心创新是为小 batch 边缘推理引入 position-wise 并行粒度。
  - Transformer Inference, Edge Devices, Cross-device Parallelism, Position-wise Partitioning, Communication Reduction

- [Power Profile Monitoring and Tracking Evolution of System-Wide HPC Workloads](https://doi.org/10.1109/icdcs60910.2024.00018)
  - Ahmad Maroof Karimi, Naw Safrin Sattar, Woong Shin, Feiyi Wang；Oak Ridge National Laboratory,Oak Ridge,TN,USA。
  - 该工作研究AI Computing Techniques中的「电源概况监控和跟踪系统范围 HPC 工作负载的演变」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善能耗或碳效率。
  - 相较直接套用通用分布式策略，核心创新是把「电源概况监控和跟踪系统范围 HPC 工作负载的演变」中的特定状态、约束或操作变成一级设计对象。
  - AI Computing Techniques, Distributed Systems

- [Bridging the Data Gap in Federated Preference Learning with AIGC](https://doi.org/10.1109/icdcs60910.2024.00019)
  - Chenyu Wang, Zhi Zhou, Xiaoxi Zhang, Xu Chen；School of Computer Science and Engineering, Sun Yat-sen University,Guangzhou,China。
  - 该工作研究AI Optimizations中的「使用 AIGC 弥合联邦偏好学习中的数据差距」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「使用 AIGC 弥合联邦偏好学习中的数据差距」中的特定状态、约束或操作变成一级设计对象。
  - Federated Learning, AI Optimizations, Distributed Systems

- [Robust Decentralized Online Optimization Against Malicious Agents](https://doi.org/10.1109/icdcs60910.2024.00020)
  - Dacheng Wen, Yupeng Li, Xiaoxi Zhang, Francis C.M. Lau；Hong Kong Baptist University,Deparrment of Interactive Media,Hong Kong; School of Computer Science and Engineering, Sun Yat-sen University,China; The University of Hong Kong,Department of Computer Science,Hong Kong。
  - 该工作研究AI Optimizations中的「针对恶意代理的鲁棒去中心化在线优化」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - Multi-Agent Systems, AI Optimizations, Distributed Systems

- [Fault-tolerant Consensus in Anonymous Dynamic Network](https://doi.org/10.1109/icdcs60910.2024.00021)
  - Qinzi Zhang, Lewis Tseng；Boston University,Boston,USA; Clark University,Worcester,USA。
  - 该工作研究Fault Tolerant Mechanisms中的「匿名动态网络中的容错共识」：在节点失效或拜占庭作恶假设下组织 message/quorum/round，保证 agreement、liveness 或故障检测。题目明确的关键手段包括consensus/BFT；直接目标是改善故障下的可用性与正确性。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - Byzantine Fault Tolerance, Fault Tolerant Mechanisms, Distributed Systems

- [Partition Detection in Byzantine Networks](https://doi.org/10.1109/icdcs60910.2024.00022)
  - Yérom-David Bromberg, Jérémie Decouchant, Manon Sourisseau, François Taïani；Univ Rennes, Inria, CNRS, IRISA,France; TU Delft,The Netherlands。
  - 该工作研究Fault Tolerant Mechanisms中的「拜占庭网络中的分区检测」：在节点失效或拜占庭作恶假设下组织 message/quorum/round，保证 agreement、liveness 或故障检测。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Byzantine Fault Tolerance, Fault Tolerant Mechanisms, Distributed Systems

- [The Impact of Asynchrony on Stability of MAC](https://doi.org/10.1109/icdcs60910.2024.00023)
  - Paweł Garncarek, Dariusz R. Kowalski, Shay Kutten, Lauren Murach；Institute of Computer Science University of Wroc&#x0142;aw,Wroc&#x0142;aw,Poland; School of Computer and Cyber Sciences Augusta University,Augusta,Georgia,USA; Technion, Haifa, Israel &#x0026; SIT Fraunhofer &#x0026; Athena,Darmstadt,Germany。
  - 该工作研究Reliability Enhancements中的「异步对MAC稳定性的影响」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「异步对MAC稳定性的影响」中的特定状态、约束或操作变成一级设计对象。
  - Reliability Enhancements, Distributed Systems

- [A Lock-free Binary Trie](https://doi.org/10.1109/icdcs60910.2024.00024)
  - Jeremy Ko；University of Toronto,Department of Computer Science,Ontario,Canada。
  - 该工作研究Distributed Design中的「无锁二进制 Trie」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「无锁二进制 Trie」中的特定状态、约束或操作变成一级设计对象。
  - Distributed Design, Distributed Systems

- [Learning Minimum Linear Arrangement of Cliques and Lines](https://doi.org/10.1109/icdcs60910.2024.00025)
  - Julien Dallot, Maciej Pacut, Marcin Bienkowski, Darya Melnyk, Stefan Schmid；Technische Universit&#x00E4;t,Berlin,Germany; University of Wroclaw,Poland。
  - 该工作研究Distributed Design中的「学习团和线的最小线性排列」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「学习团和线的最小线性排列」中的特定状态、约束或操作变成一级设计对象。
  - Distributed Design, Distributed Systems

- [SensorBFT: Fault-Tolerant Target Localization Using Voronoi Diagrams and Approximate Agreement](https://doi.org/10.1109/icdcs60910.2024.00026)
  - Akhil Bandarupalli, Adithya Bhat, Somali Chaterji, Michael K. Reiter, Aniket Kate, Saurabh Bagchi；Purdue University; Visa Research; Duke University。
  - SensorBFT研究Fault Tolerant Mechanisms中的「SensorBFT：使用 Voronoi 图和近似一致性进行容错目标定位」：在节点失效或拜占庭作恶假设下组织 message/quorum/round，保证 agreement、liveness 或故障检测。题目明确的关键手段包括consensus/BFT；直接目标是改善故障下的可用性与正确性。
  - 相较直接套用通用分布式策略，核心创新是把「SensorBFT：使用 Voronoi 图和近似一致性进行容错目标定位」中的特定状态、约束或操作变成一级设计对象。
  - Byzantine Fault Tolerance, IoT/CPS, Fault Tolerant Mechanisms, Distributed Systems

- [Distributed Pooled Data Intrusion Detection: Lessons Learned from Quantitative Group Testing](https://doi.org/10.1109/icdcs60910.2024.00027)
  - Max Hahn-Klimroth, Dominik Kaaser, Malin Rau；Goethe University Frankfurt,Frankfurt,Germany; Christian Doppler Laboratory for Blockchain Technologies for the Internet of Things, TU Hamburg,Hamburg,Germany; Universit&#x00E4;t Hamburg,Hamburg,Germany。
  - 该工作研究Reliability Enhancements中的「分布式池数据入侵检测：从定量组测试中汲取的经验教训」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Reliability Enhancements, Distributed Systems

- [Large-Scale Causal Data Replication for Stateful Edge Applications](https://doi.org/10.1109/icdcs60910.2024.00028)
  - Pedro Fouto, Nuno Preguiça, João Leitão；NOVA LINCS &#x0026; NOVA University Lisbon,Portugal。
  - 该工作研究Distributed Design中的「有状态边缘应用程序的大规模因果数据复制」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「有状态边缘应用程序的大规模因果数据复制」中的特定状态、约束或操作变成一级设计对象。
  - Edge Computing, Distributed Design, Distributed Systems

- [Knowledge Connectivity Requirements for Solving BFT Consensus with Unknown Participants and Fault Threshold](https://doi.org/10.1109/icdcs60910.2024.00029)
  - Hasan Heydari, Robin Vassantlal, Alysson Bessani；Universidade de Lisboa,LASIGE, Faculdade de Ci&#x00EA;ncias,Portugal。
  - 该工作研究Fault Tolerant Mechanisms中的「解决未知参与者 BFT 共识的知识连通性要求和故障阈值」：在节点失效或拜占庭作恶假设下组织 message/quorum/round，保证 agreement、liveness 或故障检测。题目明确的关键手段包括consensus/BFT；直接目标是改善故障下的可用性与正确性。
  - 相较直接套用通用分布式策略，核心创新是把「解决未知参与者 BFT 共识的知识连通性要求和故障阈值」中的特定状态、约束或操作变成一级设计对象。
  - Edge Computing, Byzantine Fault Tolerance, Fault Tolerant Mechanisms, Distributed Systems

- [Reducing First-Frame Delay of Live Streaming by Simultaneously Initializing Window and Rate](https://doi.org/10.1109/icdcs60910.2024.00030)
  - Bo Wu, Tong Li, Cheng Luo, Xu Yan, Fuyu Wang, Changkui Ouyang, Linfeng Guo, Haiyang Wang, Ke Xu；Tencent; Renmin University of China; University of Minnesota at Duluth; Tsinghua University。
  - 该工作研究Distributed Applications中的「同时初始化窗口和码率降低直播首帧延迟」：以持续到达的 record、operator state 和 partition 为单位，组织计算、状态迁移与故障恢复。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「同时初始化窗口和码率降低直播首帧延迟」中的特定状态、约束或操作变成一级设计对象。
  - Stream Processing, Distributed Applications, Distributed Systems

- [MuSAC: Mutualistic Sensing and Communication for Mobile Crowdsensing](https://doi.org/10.1109/icdcs60910.2024.00031)
  - Sijie Ji, Lixiang Lian, Yuanqing Zheng, Chenshu Wu；The University of Hong Kong,Department of Computer Science; School of Information Science and Technology, ShanghaiTech University; The Hong Kong Polytechnic University,Department of Computing。
  - MuSAC研究Distributed Applications中的「MuSAC：移动群体感知的互惠感知和通信」：将终端位置/移动、传感数据、链路和能量状态一起带入感知、通信或计算决策。直接目标是改善通信量与同步等待。
  - 相较直接套用通用分布式策略，核心创新是把「MuSAC：移动群体感知的互惠感知和通信」中的特定状态、约束或操作变成一级设计对象。
  - Distributed Applications, Distributed Systems

- [Debuglet: Programmable and Verifiable Inter-Domain Network Telemetry](https://doi.org/10.1109/icdcs60910.2024.00032)
  - Seyedali Tabaeiaghdaei, Filippo Costa, Jonghoon Kwon, Patrick Bamert, Yih-Chun Hu, Adrian Perrig；ETH Z&#x00FC; rich; Switch; Z&#x00FC;rcher Kantonalbank; University of Illinois Urbana-Champaign。
  - Debuglet研究Distributed Applications中的「Debuglet：可编程且可验证的域间网络遥测」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「Debuglet：可编程且可验证的域间网络遥测」中的特定状态、约束或操作变成一级设计对象。
  - Distributed Applications, Distributed Systems

- [Multi-User Entanglement Routing Design over Quantum Internets](https://doi.org/10.1109/icdcs60910.2024.00033)
  - Yiming Zeng, Jiarui Zhang, Xiaojun Shang, Ji Liu, Zhenhua Liu, Yuanyuan Yang；Stony Brook University,Stony Brook,NY,USA; University of Texas at Arlington,Arlington,TX,USA。
  - 该工作研究Quantum Network Entanglement Routing中的「量子互联网上的多用户纠缠路由设计」：以 flow/packet/path 和当前链路/队列为输入，决定路由、速率、分流或缓存规则。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「量子互联网上的多用户纠缠路由设计」中的特定状态、约束或操作变成一级设计对象。
  - Quantum Computing/Networking, Quantum Network Entanglement Routing, Distributed Systems

- [Learning from the History: Accurately and Efficiently Aggregating Geospatial Data Under Local Differential Privacy](https://doi.org/10.1109/icdcs60910.2024.00034)
  - Mengyuan Wang, Hongbo Jiang, Liang Hu, Jie Li, Peng Sun, Jiangchuan Liu；College of Computer Science and Electronic Engineering, Hunan University,China; School of Computer and Information Engineering, Central South University of Forestry and Technology,China; School of Computing Science, Simon Fraser University,Canada。
  - Learning from the History研究Blockchain Architecture and Frameworks中的「汲取历史教训：本地差分隐私下准确高效聚合地理空间数据」：指定对手可观测/篡改的数据和攻击面，再把检测、隔离、加密或隐私保护插入具体数据路径。题目明确的关键手段包括差分隐私；直接目标是改善安全、隐私或可验证性。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Blockchain, Privacy, Blockchain Architecture and Frameworks, Distributed Systems

- [Robust Categorical Data Clustering Guided by Multi-Granular Competitive Learning](https://doi.org/10.1109/icdcs60910.2024.00035)
  - Shenghong Cai, Yiqun Zhang, Xiaopeng Luo, Yiu-Ming Cheung, Hong Jia, Peng Liu；Guangdong University of Technology,Guangzhou,China; Guangzhou Huali College,Guangzhou,China; Hong Kong Baptist University,Hong Kong SAR,China; Guangdong Provincial Key Laboratory of Intelligent Information Processing,Shenzhen,China。
  - 该工作研究Distributed Applications中的「多粒度竞争学习引导的鲁棒分类数据聚类」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「多粒度竞争学习引导的鲁棒分类数据聚类」中的特定状态、约束或操作变成一级设计对象。
  - Distributed Applications, Distributed Systems

- [Efficient Pretraining and Finetuning of Quantized LLMs with Low-Rank Structure](https://doi.org/10.1109/icdcs60910.2024.00036)
  - Xiao-Yang Liu, Jie Zhang, Guoxuan Wang, Weiqin Tong, Anwar Walid；Rensselaer Polytechnic Institute,Department of Computer Science; School of Computer Engineering and Science, Shanghai University; Whiting School of Engineering, Johns Hopkins University,Department of Computer Science; Columbia University,Department of Electrical Engineering。
  - 该工作研究AI Computing Techniques中的「低阶结构量化 LLM 的高效预训练和微调」：以 worker、model shard/layer、gradient 或 expert 为单位组织计算、集合通信、内存与容错状态。直接目标是改善吞吐、扩展性或资源效率。
  - 相较直接套用通用分布式策略，核心创新是把「低阶结构量化 LLM 的高效预训练和微调」中的特定状态、约束或操作变成一级设计对象。
  - AI Computing Techniques, Distributed Systems

- [AcBF: A Revocable Blockchain-Based Identity Management Enabling Low-Latency Authentication](https://doi.org/10.1109/icdcs60910.2024.00037)
  - Jianan Hong, Jiayue Zhou, Yuqing Li, Jia Cheng, Cunqing Hua；School of Cyber Science and Engineering, Shanghai Jiao Tong University,Shanghai,China; SJTU-ParisTech Elite Institute of Technology, Shanghai Jiao Tong University,Shanghai,China; School of Cyber Science and Engineering, Wuhan University,Wuhan,China。
  - AcBF研究Blockchain Security and Privacy中的「AcBF：可撤销的基于区块链的身份管理，支持低延迟身份验证」：以交易、账户、shard/chain 和验证消息为对象，设计执行、路由、原子性或激励机制。直接目标是改善请求时延或任务完成时间。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Blockchain, Privacy, Security, Blockchain Security and Privacy

- [CORE: Transaction Commit-Controlled Release of Private Data Over Blockchains](https://doi.org/10.1109/icdcs60910.2024.00038)
  - Shan Wang, Ming Yang, Jiannong Cao, Zhen Ling, Qiang Tang, Xinwen Fu；Southeast University; The Hong Kong Polytechnic University; The University of Sydney; University of Massachusetts Lowell。
  - CORE研究Blockchain Security and Privacy中的「核心：通过区块链进行交易提交控制的私有数据发布」：以交易、账户、shard/chain 和验证消息为对象，设计执行、路由、原子性或激励机制。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「核心：通过区块链进行交易提交控制的私有数据发布」中的特定状态、约束或操作变成一级设计对象。
  - Blockchain, Privacy, Security, Blockchain Security and Privacy

- [Orbit: A Dynamic Account Allocation Mechanism in Sharding Blockchain System](https://doi.org/10.1109/icdcs60910.2024.00039)
  - Xin Wang, Bo Li, Linpeng Jia, Yi Sun；Institute of Computing Technology, Chinese Academy of Sciences,Beijing,China。
  - Orbit研究Blockchain Architecture and Frameworks中的「Orbit：分片区块链系统中的动态账户分配机制」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。题目明确的关键手段包括sharding；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - Blockchain, Blockchain Architecture and Frameworks, Distributed Systems

- [CubeChain: Generalized Query Framework for Intra- and Cross-Chain Scenarios](https://doi.org/10.1109/icdcs60910.2024.00040)
  - Haochen Ren, Xiulong Liu, Hao Xu, Chenyu Zhang, Keqiu Li；College of Intelligence and Computing, Tianjin University,China。
  - CubeChain研究Blockchain Architecture and Frameworks中的「CubeChain：链内和跨链场景的通用查询框架」：以交易、账户、shard/chain 和验证消息为对象，设计执行、路由、原子性或激励机制。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「CubeChain：链内和跨链场景的通用查询框架」中的特定状态、约束或操作变成一级设计对象。
  - Blockchain, Blockchain Architecture and Frameworks, Distributed Systems

- [Enabling High-Performance EOV Blockchains via Transaction Ordering Exploration](https://doi.org/10.1109/icdcs60910.2024.00041)
  - Mei Yu, Yihan Zhao, Jianrong Wang, Dengcheng Hu, Xiulong Liu, Qi Li, Keqiu Li；College of Intelligence and Computing, Tianjin University,China。
  - 该工作研究Blockchain Scalability and Payments中的「通过交易排序探索实现高性能 EOV 区块链」：以交易、账户、shard/chain 和验证消息为对象，设计执行、路由、原子性或激励机制。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「通过交易排序探索实现高性能 EOV 区块链」中的特定状态、约束或操作变成一级设计对象。
  - Blockchain, Blockchain Scalability and Payments, Distributed Systems

- [SecSCS: A User-Centric Secure Smart Camera System Based on Blockchain](https://doi.org/10.1109/icdcs60910.2024.00042)
  - Xinyuan Qian, Hongwei Li, Haoyong Wang, Guowen Xu, Shengmin Xu, Ju Ren；School of Computer Science and Engineering, University of Electronic Science and Technology of China; Chongqing Key Laboratory of Automated Reasoning and Cognition; College of Computer and Cyber Security, Fujian Normal University; Tsinghua University,Department of Computer Science and Techology。
  - SecSCS研究Blockchain Security and Privacy中的「SecSCS：基于区块链的以用户为中心的安全智能摄像头系统」：以交易、账户、shard/chain 和验证消息为对象，设计执行、路由、原子性或激励机制。直接目标是改善安全、隐私或可验证性。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Blockchain, Privacy, Security, Blockchain Security and Privacy

- [USSC: Universal and Storage-Efficient Sidechains](https://doi.org/10.1109/icdcs60910.2024.00043)
  - Taotao Li, Huawei Huang, Lingyuan Yin, Siyuan Yao, Zibin Zheng；SSE, Sun Yat-Sen University,China; China Academy of Information and Communications Technology,China; Beijing University of Posts and Telecommunications,China。
  - USSC研究Blockchain Scalability and Payments中的「USSC：通用且存储高效的侧链」：以 block/object/record 或 checkpoint state 为单位，组织读写、编码、复制、索引或恢复路径。直接目标是改善吞吐、扩展性或资源效率。
  - 相较直接套用通用分布式策略，核心创新是把「USSC：通用且存储高效的侧链」中的特定状态、约束或操作变成一级设计对象。
  - Storage/Data Systems, Blockchain, Blockchain Scalability and Payments, Distributed Systems

- [Hammer: A General Blockchain Evaluation Framework](https://doi.org/10.1109/icdcs60910.2024.00044)
  - Gang Wang, Yanfeng Zhang, Chenhao Ying, Xiaohua Lit, Ge Yu；School of Computer Science and Engineering, Northeastern University,Shenyang,China; Shanghai Jiao Tong University,Department of Computer Science and Engineering,Shanghai,China。
  - Hammer研究Blockchain Architecture and Frameworks中的「Hammer：通用区块链评估框架」：以交易、账户、shard/chain 和验证消息为对象，设计执行、路由、原子性或激励机制。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「Hammer：通用区块链评估框架」中的特定状态、约束或操作变成一级设计对象。
  - Blockchain, Blockchain Architecture and Frameworks, Distributed Systems

- [SG-FCB: A Stackelberg Game-Driven Fair Committee-Based Blockchain Consensus Protocol](https://doi.org/10.1109/icdcs60910.2024.00045)
  - Ningbin Yang, Chunming Tang, Zehui Xiong, Qian Chen, Jiawen Kang, Debiao He；School of Mathematics and Information Science, Guangzhou Center for Applied Mathematics, Guangzhou University,Guangzhou,China; Information Systems Technology and Design, Singapore University of Technology and Design,Singapore; School of Cyber Engineering, Xidian University,Xian,China; School of Automation, Guangdong University of Technology,Guangzhou,China; School of Cyber Science and Engineering, Wuhan University,Wuhan,China。
  - SG-FCB研究Blockchain Security and Privacy中的「SG-FCB：基于 Stackelberg 游戏驱动的公平委员会的区块链共识协议」：以交易、账户、shard/chain 和验证消息为对象，设计执行、路由、原子性或激励机制。题目明确的关键手段包括consensus/BFT；直接目标是改善资源或服务公平性。
  - 相较直接套用通用分布式策略，核心创新是把「SG-FCB：基于 Stackelberg 游戏驱动的公平委员会的区块链共识协议」中的特定状态、约束或操作变成一级设计对象。
  - Blockchain, Byzantine Fault Tolerance, Privacy, Security

- [Universal and Trustless Large-Value Payments in Cryptocurrencies](https://doi.org/10.1109/icdcs60910.2024.00046)
  - Zihan Liu, Chao Lin, Debiao He, Xinyi Huang, Lang Pu；Fujian Normal University,Fuzhou,China; Wuhan University,Wuhan,China; Hong Kong University of Science and Technology (Guangzhou),Guangzhou,China; Nanjing University of Aeronautics and Astronautics,Nanjing,China。
  - 该工作研究Blockchain Scalability and Payments中的「通用且无需信任的加密货币大额支付」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「通用且无需信任的加密货币大额支付」中的特定状态、约束或操作变成一级设计对象。
  - Blockchain, Blockchain Scalability and Payments, Distributed Systems

- [D2T: Dynamic Dual Threshold Policy of Shared-Memory in Data Center Switches](https://doi.org/10.1109/icdcs60910.2024.00047)
  - Jiawei Huang, Hui Li, Zhaoyi Li, Zihao Chen, Jingling Liu, Jing Shao, Wenlu Zhang, Yijun Li, Sitan Li, Shengwen Zhou, Ping Zhong, Jianxin Wang, Wanchun Jiang, Yong Cui；Central South University; Tsinghua University。
  - D2T研究Data Center Networking and Management中的「D2T：数据中心交换机共享内存的动态双阈值策略」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善内存占用与数据复用。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - Data Center Networking and Management, Distributed Systems

- [Understanding the IO Performance Gap Between OS-Level and VM-Level Containers in High-Density Deployment](https://doi.org/10.1109/icdcs60910.2024.00048)
  - Wentai Li, Kaijun Zhou, Jiacheng Shi, Xingman Chen, Yadong Liu, Luyuan Wang, Jinyu Gu；Institute of Parallel and Distributed Systems (IPADS), Shanghai Jiao Tong University,Shanghai,China; Huawei Technologies Co., Ltd.,Shenzhen,China; Beijing Institute of Spacecraft System,Beijing,China。
  - 该工作研究Cloud Storage and Communication中的「了解高密度部署中操作系统级和虚拟机级容器之间的 IO 性能差距」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「了解高密度部署中操作系统级和虚拟机级容器之间的 IO 性能差距」中的特定状态、约束或操作变成一级设计对象。
  - Storage/Data Systems, Cloud Storage and Communication, Distributed Systems

- [Optimal Wide Stripe Generation in Locally Repairable Codes via Staged Stripe Merging](https://doi.org/10.1109/icdcs60910.2024.00049)
  - Si Wu, Guantian Lin, Patrick P. C. Lee, Cheng Li, Yinlong Xu；University of Science and Technology of China; The Chinese University of Hong Kong。
  - 该工作研究Cloud Storage and Communication中的「通过分阶段条带合并在本地可修复代码中生成最佳宽条带」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「通过分阶段条带合并在本地可修复代码中生成最佳宽条带」中的特定状态、约束或操作变成一级设计对象。
  - Storage/Data Systems, Cloud Storage and Communication, Distributed Systems

- [NPV: Fast Network Policy Verification for Cloud-Native Networking](https://doi.org/10.1109/icdcs60910.2024.00050)
  - Shunbin Dong, Yumin Xie, Jin Zhao, Kun Qiu；School of Computer Science, Fudan University,Shanghai,China。
  - NPV研究Data Center Networking and Management中的「NPV：云原生网络的快速网络策略验证」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「NPV：云原生网络的快速网络策略验证」中的特定状态、约束或操作变成一级设计对象。
  - Data Center Networking and Management, Distributed Systems

- [Latency-Guaranteed Co-Location of Inference and Training for Reducing Data Center Expenses](https://doi.org/10.1109/icdcs60910.2024.00051)
  - Guoyu Chen, Srinivasan Subramaniyan, Xiaorui Wang；The Ohio State University,Columbus,Ohio,USA。
  - 该工作研究Data Center Networking and Management中的「保证延迟的推理和训练共置，以减少数据中心费用」：以在线模型请求为单位，组织模型/算子放置、并行执行、状态缓存和请求排队。直接目标是改善请求时延或任务完成时间。
  - 相较直接套用通用分布式策略，核心创新是把「保证延迟的推理和训练共置，以减少数据中心费用」中的特定状态、约束或操作变成一级设计对象。
  - Data Center Networking and Management, Distributed Systems

- [Aquilas: Adaptive QoS-Oriented Multipath Packet Scheduler with Hierarchical Intelligence for QUIC](https://doi.org/10.1109/icdcs60910.2024.00052)
  - Congxi Song, Biao Han, Ruidong Li, Xueqiang Han, Cong Liu, Jinshu Su；College of Computer Science and Technology, National University of Defense Technology,Changsha,China; Graduate School of Natural Science and Technology, Kanazawa University,Kanazawa,Japan; CMC,Inforrnation Center of Logistic Support Department,Beijing,China; Academy of Military Science,Beijing,China。
  - Aquilas研究Cloud Storage and Communication中的「Aquilas：面向 QoS 的自适应多路径数据包调度程序，具有 QUIC 的分层智能」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - Storage/Data Systems, Scheduling, Cloud Storage and Communication, Distributed Systems

- [HardWhale: A Hardware-Isolated Network Security Enforcement System for Cloud Environments](https://doi.org/10.1109/icdcs60910.2024.00053)
  - Myoungsung You, Jaehyun Nam, Hyunmin Seo, Minjae Seo, Jaehan Kim, Dongmin Choi, Seungwon Shin；KAIST; Dankook University。
  - HardWhale研究Cloud Security and Performance Optimizations中的「HardWhale：适用于云环境的硬件隔离网络安全执行系统」：指定对手可观测/篡改的数据和攻击面，再把检测、隔离、加密或隐私保护插入具体数据路径。直接目标是改善安全、隐私或可验证性。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Security, Cloud Security and Performance Optimizations, Distributed Systems

- [P4ce: Consensus over RDMA at Line Speed](https://doi.org/10.1109/icdcs60910.2024.00054)
  - Rémi Dulong, Nathan Felber, Pascal Felber, Gilles Hopin, Baptiste Lepers, Valerio Schiavoni, Gaël Thomas, Sébastien Vaucher；University of Neuch&#x00E2;tel,Switzerland; EPFL,Switzerland; Ecole Polytechnique,France; Inria,France。
  - P4ce研究Cloud Security and Performance Optimizations中的「P4ce：以线速通过 RDMA 达成共识」：在节点失效或拜占庭作恶假设下组织 message/quorum/round，保证 agreement、liveness 或故障检测。题目明确的关键手段包括RDMA、consensus/BFT；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较让 CPU/通用软件路径承担所有数据移动和控制，核心创新是把关键操作下沉到网络或硬件数据路径。
  - Byzantine Fault Tolerance, Security, Network/Hardware Offload, Cloud Security and Performance Optimizations

- [FARM: Comprehensive Data Center Network Monitoring and Management](https://doi.org/10.1109/icdcs60910.2024.00055)
  - Jérôme Graf, Pavel Chuprikov, Patrick Eugster, Patrick Jahnke；Universit&#x00E0; della Svizzera italiana (USI); SAP SE。
  - FARM研究Data Center Networking and Management中的「FARM：全面的数据中心网络监控和管理」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「FARM：全面的数据中心网络监控和管理」中的特定状态、约束或操作变成一级设计对象。
  - Data Center Networking and Management, Distributed Systems

- [Interleaved Function Stream Execution Model for Cache-Aware High-Speed Stateful Packet Processing](https://doi.org/10.1109/icdcs60910.2024.00056)
  - Ziyan Wu, Yang Zhang, Feng Tian, Minjun Wu, Antonia Zhai, Zhi-Li Zhang；University of Minnesota, Twin Cities,Minneapolis,USA。
  - 该工作研究Cloud Security and Performance Optimizations中的「用于缓存感知高速状态数据包处理的交错函数流执行模型」：在容量、层级和时延约束下决定哪些数据/模型状态应保留、迁移、复用或淘汰。题目明确的关键手段包括cache placement/reuse；直接目标是改善内存占用与数据复用。
  - 相较直接套用通用分布式策略，核心创新是把「用于缓存感知高速状态数据包处理的交错函数流执行模型」中的特定状态、约束或操作变成一级设计对象。
  - Caching, Stream Processing, Security, Cloud Security and Performance Optimizations

- [LinuxFP: Transparently Accelerating Linux Networking](https://doi.org/10.1109/icdcs60910.2024.00057)
  - Marcelo Abranches, Erika Hunhoff, Rohan Eswara, Oliver Michel, Eric Keller；University of Colorado,Boulder; Princeton University。
  - LinuxFP研究Cloud Security and Performance Optimizations中的「LinuxFP：透明地加速 Linux 网络」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善吞吐、扩展性或资源效率。
  - 相较直接套用通用分布式策略，核心创新是把「LinuxFP：透明地加速 Linux 网络」中的特定状态、约束或操作变成一级设计对象。
  - Security, Cloud Security and Performance Optimizations, Distributed Systems

- [Group-Centric Scheduling for Industrial Edge Computing Networks with Incomplete Information](https://doi.org/10.1109/icdcs60910.2024.00058)
  - Tongxin Zhu, Ouming Zou, Xiaolin Fang, Junzhou Luo, Yingshu Li, Zhipeng Cai；Southeast University; Georgia State University。
  - 该工作研究Edge Deployment and Management中的「不完全信息工业边缘计算网络的以组为中心的调度」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「不完全信息工业边缘计算网络的以组为中心的调度」中的特定状态、约束或操作变成一级设计对象。
  - Edge Computing, Scheduling, Edge Deployment and Management, Distributed Systems

- [Fine-Grained Service Lifetime Optimization for Energy-Constrained Edge-Edge Collaboration](https://doi.org/10.1109/icdcs60910.2024.00059)
  - Haodong Zou, Jianxiong Guo, Jiandian Zeng, Yupeng Li, Jiannong Cao, Tian Wang；BNU-HKBU United International College,Guangdong Provincial Key Laboratory IRADS,Zhuhai,China; Institute of Artificial Intelligence and Future Networks, Beijing Normal University,Zhuhai,China; Hong Kong Baptist University,Hong Kong,China; The Hong Kong Polytechnic University,Hong Kong,China。
  - 该工作研究Edge Deployment and Management中的「针对能源受限的边缘-边缘协作的细粒度服务生命周期优化」：以 worker、model shard/layer、gradient 或 expert 为单位组织计算、集合通信、内存与容错状态。直接目标是改善能耗或碳效率。
  - 相较直接套用通用分布式策略，核心创新是把「针对能源受限的边缘-边缘协作的细粒度服务生命周期优化」中的特定状态、约束或操作变成一级设计对象。
  - Edge Computing, Edge Deployment and Management, Distributed Systems

- [FedSZ: Leveraging Error-Bounded Lossy Compression for Federated Learning Communications](https://doi.org/10.1109/icdcs60910.2024.00060)
  - Grant Wilkins, Sheng Di, Jon C. Calhoun, Zilinghan Li, Kibaek Kim, Robert Underwood, Richard Mortier, Franck Cappello；Argonne National Laboratory,Lemont,IL,USA; Clemson University,Clemson,SC,USA; University of Cambridge,Cambridge,UK。
  - FedSZ研究Federated Learning at the Edge中的「FedSZ：利用误差有限有损压缩进行联邦学习通信」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation、compression/quantization；直接目标是改善通信量与同步等待。
  - 相较直接套用通用分布式策略，核心创新是把「FedSZ：利用误差有限有损压缩进行联邦学习通信」中的特定状态、约束或操作变成一级设计对象。
  - Federated Learning, Edge Computing, Compression/Quantization, Federated Learning at the Edge

- [EdgStr: Automating Client-Cloud to Client-Edge-Cloud Transformation](https://doi.org/10.1109/icdcs60910.2024.00061)
  - Kijin An, Eli Tilevich；Software Engineering Team, Samsung Research,Seoul,South Korea; Software Innovations Lab, Virginia Tech,Dept. of Computer Science,Blacksburg,VA,United States。
  - EdgStr研究Edge Deployment and Management中的「EdgStr：自动化客户端云到客户端边缘云转型」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「EdgStr：自动化客户端云到客户端边缘云转型」中的特定状态、约束或操作变成一级设计对象。
  - Edge Computing, Edge Deployment and Management, Distributed Systems

- [Edge Cache on WiFi Access Points: Millisecond-Level App Latency Almost for Free](https://doi.org/10.1109/icdcs60910.2024.00062)
  - Zhengquan Li, Summit Shrestha, Zheng Song, Eli Tilevich；University of Michigan at Dearborn,Department of Computer and Information Science,Dearborn,Michigan; Virginia Tech,Department of Computer Science,Blacksburg,Virginia。
  - 该工作研究Edge Deployment and Management中的「WiFi 接入点上的边缘缓存：毫秒级应用程序延迟几乎免费」：在容量、层级和时延约束下决定哪些数据/模型状态应保留、迁移、复用或淘汰。题目明确的关键手段包括cache placement/reuse；直接目标是改善请求时延或任务完成时间。
  - 相较直接套用通用分布式策略，核心创新是把「WiFi 接入点上的边缘缓存：毫秒级应用程序延迟几乎免费」中的特定状态、约束或操作变成一级设计对象。
  - Edge Computing, Caching, Edge Deployment and Management, Distributed Systems

- [Anole: Adapting Diverse Compressed Models for Cross-Scene Prediction on Mobile Devices](https://doi.org/10.1109/icdcs60910.2024.00063)
  - Yunzhe Li, Hongzi Zhu, Zhuohong Deng, Yunlong Cheng, Liang Zhang, Shan Chang, Minyi Guo；Shanghai Jiao Tong University,Shanghai,China; Donghua University,Shanghai,China。
  - Anole研究Mobile Algorithms and AI Optimizations中的「Anole：采用多种压缩模型进行移动设备上的跨场景预测」：将终端位置/移动、传感数据、链路和能量状态一起带入感知、通信或计算决策。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「Anole：采用多种压缩模型进行移动设备上的跨场景预测」中的特定状态、约束或操作变成一级设计对象。
  - Mobile Algorithms and AI Optimizations, Distributed Systems

- [OffloaDNN: Shaping DNNs for Scalable Offloading of Computer Vision Tasks at the Edge](https://doi.org/10.1109/icdcs60910.2024.00064)
  - Corrado Puligheddu, Nancy Varshney, Tanzil Hassan, Jonathan Ashdown, Francesco Restuccia, Carla Fabiana Chiasserini；Politecnico di Torino,Italy; Institute for the Wireless Internet of Things, Northeastern University,United States; Air Force Research Laboratory,United States。
  - OffloaDNN研究Edge-Enhanced AI中的「OffloaDNN：塑造 DNN 以实现边缘计算机视觉任务的可扩展卸载」：对每个任务/算子选择本地、edge、cloud 或网络设备的执行位置，并同时考虑链路和节点状态。直接目标是改善吞吐、扩展性或资源效率。
  - 相较直接套用通用分布式策略，核心创新是把「OffloaDNN：塑造 DNN 以实现边缘计算机视觉任务的可扩展卸载」中的特定状态、约束或操作变成一级设计对象。
  - Edge Computing, Edge-Enhanced AI, Distributed Systems

- [DNN Partitioning and Assignment for Distributed Inference in SGX Empowered Edge Cloud](https://doi.org/10.1109/icdcs60910.2024.00065)
  - Yuepeng Li, Deze Zeng, Lin Gut, Song Guo, Albert Y. Zomaya；School of Computer Science, China University of Geosciences,Wuhan,China; School of Computer Science and Technology, Huazhong University of Science and Technology,China; The Hong Kong Polytechnic University,Department of Computing,Hong Kong; School of Computer Science, The University of Sydney,Australia。
  - 该工作研究Edge-Enhanced AI中的「SGX Empowered Edge Cloud 中分布式推理的 DNN 分区和分配」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。直接目标是改善能耗或碳效率。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Edge Computing, Edge-Enhanced AI, Distributed Systems

- [Tangram: High-Resolution Video Analytics on Serverless Platform with SLO-Aware Batching](https://doi.org/10.1109/icdcs60910.2024.00066)
  - Haosong Peng, Yufeng Zhan, Peng Li, Yuanqing Xia；School of Automation, Beijing Institute of Technology,Beijing,China; School of Computer Science and Engineering, The University of Aizu,Aizuwakamatsu,Japan。
  - Tangram研究Edge-Enhanced AI中的「Tangram：无服务器平台上具有 SLO 感知批处理的高分辨率视频分析」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「Tangram：无服务器平台上具有 SLO 感知批处理的高分辨率视频分析」中的特定状态、约束或操作变成一级设计对象。
  - Edge Computing, Serverless Computing, Edge-Enhanced AI, Distributed Systems

- [Mobility-Aware Device Sampling for Statistical Heterogeneity in Hierarchical Federated Learning](https://doi.org/10.1109/icdcs60910.2024.00067)
  - Songli Zhang, Zhenzhe Zheng, Qinya Li, Fan Wu, Guihai Chen；Shanghai Jiao Tong University,Department of Computer Science and Engineering,Shanghai,China。
  - 该工作研究Federated Learning at the Edge中的「分层联邦学习中统计异质性的移动感知设备采样」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较单层级、单粒度处理，核心创新是按层级/粒度分解状态和决策，再在层间协同。
  - Federated Learning, Edge Computing, Federated Learning at the Edge, Distributed Systems

- [Dynamic Time-of-Use Pricing for Serverless Edge Computing with Generalized Hidden Parameter Markov Decision Processes](https://doi.org/10.1109/icdcs60910.2024.00068)
  - Feridun Tütüncüoğlu, Ayoub Ben-Ameur, György Dán, Andrea Araldo, Tijani Chahed；KTH Royal Institute of Technology,Division of Network and Systems Engineering,Sweden; SAMOVAR, Telecom SudParis, Institut Polytechnique de Paris,France。
  - 该工作研究Dynamic Pricing and Network Optimizations at the Edge中的「具有广义隐藏参数马尔可夫决策过程的无服务器边缘计算的动态使用时间定价」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - Edge Computing, Serverless Computing, Dynamic Pricing and Network Optimizations at the Edge, Distributed Systems

- [Communication-Efficient Training Workload Balancing for Decentralized Multi-Agent Learning](https://doi.org/10.1109/icdcs60910.2024.00069)
  - Seyed Mahmoud Sajjadi Mohammadabadi, Lei Yang, Feng Yan, Junshan Zhang；University of Nevada, Reno,Department of Computer Science and Engineering,Reno,NV,USA; University of Houston,Department of Computer Science,Houston,TX,USA; University of California, Davis,Department of Electrical and Computer Engineering,Davis,CA,USA。
  - 该工作研究Federated Learning at the Edge中的「用于分散式多代理学习的高效通信训练工作负载平衡」：以 worker、model shard/layer、gradient 或 expert 为单位组织计算、集合通信、内存与容错状态。直接目标是改善通信量与同步等待。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Multi-Agent Systems, Federated Learning, Edge Computing, Federated Learning at the Edge

- [Accelerating and Securing Federated Learning with Stateless In-Network Aggregation at the Edge](https://doi.org/10.1109/icdcs60910.2024.00070)
  - Junxu Xia, Wenfei Wu, Lailong Luo, Geyao Cheng, Deke Guo, Qifeng Nian；National University of Defense Technology; Peking University; Fujian Polytechnic Normal University。
  - 该工作研究Federated Learning at the Edge中的「通过边缘的无状态网络内聚合加速和保护联邦学习」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括网内处理、federated aggregation；直接目标是改善吞吐、扩展性或资源效率。
  - 相较让 CPU/通用软件路径承担所有数据移动和控制，核心创新是把关键操作下沉到网络或硬件数据路径。
  - Federated Learning, Edge Computing, Network/Hardware Offload, Federated Learning at the Edge

- [Nona: A Framework for Elastic Stream Provenance](https://doi.org/10.1109/icdcs60910.2024.00071)
  - Bastian Havers, Marina Papatriantafilou, Vincenzo Gulisano；Chalmers University, Volvo Cars,Gothenburg,Sweden; Chalmers University,Gothenburg,Sweden。
  - Nona研究Dynamic Pricing and Network Optimizations at the Edge中的「Nona：弹性流来源的框架」：以持续到达的 record、operator state 和 partition 为单位，组织计算、状态迁移与故障恢复。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - Edge Computing, Stream Processing, Dynamic Pricing and Network Optimizations at the Edge, Distributed Systems

- [Edge-Assisted Relevance-Aware Perception Dissemination in Vehicular Networks](https://doi.org/10.1109/icdcs60910.2024.00072)
  - Ruiqi Wang, Guohong Cao；Pennsylvania State University,Department of Computer Science and Engineering。
  - 该工作研究Dynamic Pricing and Network Optimizations at the Edge中的「车辆网络中的边缘辅助相关性感知感知传播」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「车辆网络中的边缘辅助相关性感知感知传播」中的特定状态、约束或操作变成一级设计对象。
  - Edge Computing, Mobile/Space Networks, Dynamic Pricing and Network Optimizations at the Edge, Distributed Systems

- [A Performance Analysis Modeling Framework for Extended Reality Applications in Edge-Assisted Wireless Networks](https://doi.org/10.1109/icdcs60910.2024.00073)
  - Anik Mallik, Jiang Xie, Zhu Han；The University of North Carolina,The Dept. of Electrical and Computer Engineering,Charlotte,NC,USA; University of Houston,The Dept. of Electrical and Computer Engineering,TX,USA。
  - 该工作研究Dynamic Pricing and Network Optimizations at the Edge中的「边缘辅助无线网络中扩展现实应用的性能分析建模框架」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「边缘辅助无线网络中扩展现实应用的性能分析建模框架」中的特定状态、约束或操作变成一级设计对象。
  - Edge Computing, Dynamic Pricing and Network Optimizations at the Edge, Distributed Systems

- [Dapper: A Lightweight and Extensible Framework for Live Program State Rewriting](https://doi.org/10.1109/icdcs60910.2024.00074)
  - Abhishek Bapat, Jaidev Shastri, Xiaoguang Wang, Abilesh Sundarasamy, Binoy Ravindran；Virginia Tech,Blacksburg,USA; University of Illinois Chicago,Chicago,USA。
  - Dapper研究Reliability Enhancements中的「Dapper：用于实时程序状态重写的轻量级可扩展框架」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「Dapper：用于实时程序状态重写的轻量级可扩展框架」中的特定状态、约束或操作变成一级设计对象。
  - Reliability Enhancements, Distributed Systems

- [HGR: A Hybrid Global Graph-Based Recovery Approach for Cloud Storage Systems with Failure and Straggler Nodes](https://doi.org/10.1109/icdcs60910.2024.00075)
  - Piao Hu, Huangzhen Xue, Chentao Wu, Minyi Guo, Jie Li, Xiangyu Chen, Shaoteng Liu, Liyang Zhou, Shenghong Xie；Shanghai Jiao Tong University,Department of Computer Science and Engineering,Shanghai,China; Huawei Technologies Co., Ltd.,Shenzhen,China。
  - HGR研究Cloud Storage and Communication中的「HGR：一种针对具有故障和落后节点的云存储系统的基于混合全局图的恢复方法」：以 block/object/record 或 checkpoint state 为单位，组织读写、编码、复制、索引或恢复路径。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「HGR：一种针对具有故障和落后节点的云存储系统的基于混合全局图的恢复方法」中的特定状态、约束或操作变成一级设计对象。
  - Storage/Data Systems, Cloud Storage and Communication, Distributed Systems

- [Ensuring Fairness in Federated Learning Services: Innovative Approaches to Client Selection, Scheduling, and Rewards](https://doi.org/10.1109/icdcs60910.2024.00076)
  - Meiying Zhang, Huan Zhao, Sheldon Ebron, Ruitao Xie, Kan Yang；University of Memphis,Dept. of Computer Science,USA; College of Computer Science and Software Engineering, Shenzhen University,China。
  - 该工作研究Fairness in Federated Learning中的「确保联邦学习服务的公平性：客户选择、调度和奖励的创新方法」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。题目明确的关键手段包括federated aggregation；直接目标是改善资源或服务公平性。
  - 相较直接套用通用分布式策略，核心创新是把「确保联邦学习服务的公平性：客户选择、调度和奖励的创新方法」中的特定状态、约束或操作变成一级设计对象。
  - Federated Learning, Scheduling, Fairness in Federated Learning, Distributed Systems

- [On Federated Multi-Armed Bandits for Mobile Social Networks](https://doi.org/10.1109/icdcs60910.2024.00077)
  - Kazuya Sakai, Takeshi Kitamura, Min-Te Sun, Wei-Shinn Ku；Tokyo Metropolitan University,Department of Electrical Engineering and Computer Science,Tokyo,Japan,191-; National Central University,Department of Computer Science and Information Engineering,Taoyuan,Taiwan,320; Auburn University,Department of Computer Science and Software Engineering,Auburn,Alabama,USA。
  - 该工作研究Incentives in Federated Learning中的「移动社交网络的联合多臂强盗」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「移动社交网络的联合多臂强盗」中的特定状态、约束或操作变成一级设计对象。
  - Federated Learning, Incentives in Federated Learning, Distributed Systems

- [Mitigating Demographic Bias of Federated Learning Models via Robust-Fair Domain Smoothing: A Domain-Shifting Approach](https://doi.org/10.1109/icdcs60910.2024.00078)
  - Huimin Zeng, Zhenrui Yue, Qian Jiang, Yang Zhang, Lanyu Shang, Ruohan Zong, Dong Wang；Unversity of Illinois at Urbana-Champaign。
  - 该工作研究Reliability Enhancements中的「通过鲁棒公平域平滑减轻联邦学习模型的人口统计偏差：域转移方法」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善资源或服务公平性。
  - 相较直接套用通用分布式策略，核心创新是把「通过鲁棒公平域平滑减轻联邦学习模型的人口统计偏差：域转移方法」中的特定状态、约束或操作变成一级设计对象。
  - Federated Learning, Reliability Enhancements, Distributed Systems

- [Libra: A Fairness-Guaranteed Framework for Semi-Asynchronous Federated Learning](https://doi.org/10.1109/icdcs60910.2024.00079)
  - Chun Wang, Huawei Huang, Ruixin Li, Jialiang Liu, Ting Cai, Zibin Zheng；Sun Yat-Sen University,China; Hubei University of Technology,China。
  - Libra研究Fairness in Federated Learning中的「Libra：半异步联邦学习的公平保证框架」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善资源或服务公平性。
  - 相较直接套用通用分布式策略，核心创新是把「Libra：半异步联邦学习的公平保证框架」中的特定状态、约束或操作变成一级设计对象。
  - Federated Learning, Fairness in Federated Learning, Distributed Systems

- [Can Federated Learning Clients be Lightweight? A Plug-and-Play Symmetric Conversion Module](https://doi.org/10.1109/icdcs60910.2024.00080)
  - Jialiang Liu, Huawei Huang, Chun Wang, Ruixin Li, Ting Car, Qinglin Yang, Zibin Zheng；School of CSE, Sun Yat-Sen University,China; SSE, Sun Yat-Sen University,China; SCS, Hubei University of Technology,China。
  - 该工作研究Secure Federated Learning中的「联邦学习客户端可以轻量级吗？即插即用的对称转换模块」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「联邦学习客户端可以轻量级吗？即插即用的对称转换模块」中的特定状态、约束或操作变成一级设计对象。
  - Federated Learning, Security, Secure Federated Learning, Distributed Systems

- [FedMark: Large-Capacity and Robust Watermarking in Federated Learning](https://doi.org/10.1109/icdcs60910.2024.00081)
  - Lan Zhang, Chen Tang, Huiqi Liu, Haikuo Yu, Xirong Zhuang, Qi Zhao, Lei Wang, Wenjing Fang, Xiang-Yang Li；University of Science and Technology of China,Hefei,China。
  - FedMark研究Security in Federated Learning中的「FedMark：联邦学习中的大容量和鲁棒水印」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「FedMark：联邦学习中的大容量和鲁棒水印」中的特定状态、约束或操作变成一级设计对象。
  - Federated Learning, Security, Security in Federated Learning, Distributed Systems

- [Mitigation of Gradient Inversion Attacks in Federated Learning with Private Adaptive Optimization](https://doi.org/10.1109/icdcs60910.2024.00082)
  - Cody Lewis, Vijay Varadharajan, Nasimul Noman, Uday Tupakula, Nan Li；The University of Newcastle,Newcastle,Australia; University of Wollongong,Wollongong,Australia。
  - 该工作研究Security in Federated Learning中的「通过私有自适应优化缓解联邦学习中的梯度反转攻击」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善安全、隐私或可验证性。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - Federated Learning, Security, Security in Federated Learning, Distributed Systems

- [Incentivizing Participation in SplitFed Learning: Convergence Analysis and Model Versioning](https://doi.org/10.1109/icdcs60910.2024.00083)
  - Pengchao Han, Chao Huang, Xingyan Shi, Jianwei Huang, Xin Liu；School of Information Engineering, Guangdong University of Technology,Guangzhou,China; The University of California,Department of Computer Science,Davis,USA; School of Data Science, The Chinese University of Hong Kong,Shenzhen,China; School of Science and Engineering, Shenzhen Institute of Artificial Intelligence and Robotics for Society, The Chinese University of Hong Kong,Shenzhen,Shenzhen,China。
  - 该工作研究Incentives in Federated Learning中的「激励参与 SplitFed 学习：收敛分析和模型版本控制」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「激励参与 SplitFed 学习：收敛分析和模型版本控制」中的特定状态、约束或操作变成一级设计对象。
  - Federated Learning, Incentives in Federated Learning, Distributed Systems

- [Federated SGD with Local Asynchrony](https://doi.org/10.1109/icdcs60910.2024.00084)
  - Bapi Chatterjee, Vyacheslav Kungurtsev, Dan Alistarh；IIIT Delhi,New Delhi,India; Czech Technical University,Prague,Czechia; IST Austria (ISTA),Klosterneuburg,Austria。
  - 该工作研究Incentives in Federated Learning中的「具有本地异步的联合 SGD」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「具有本地异步的联合 SGD」中的特定状态、约束或操作变成一级设计对象。
  - Federated Learning, Incentives in Federated Learning, Distributed Systems

- [Toward Free-Riding Attack on Cross-Silo Federated Learning Through Evolutionary Game](https://doi.org/10.1109/icdcs60910.2024.00085)
  - Tianxiang Chen, Feng Wang, Wangjie Qiu, Qinnan Zhang, Zehui Xiong, Zhiming Zheng；School of Artificial Intelligence, Beihang University,Beijing Advanced Innovation Center for Future Blockchain and Privacy Computing,Beijing,China; Singapore University of Technology and Design,Information Systems Technology and Design,Singapore。
  - 该工作研究Security in Federated Learning中的「通过进化博弈实现跨筒仓联邦学习的搭便车攻击」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善安全、隐私或可验证性。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Federated Learning, Security, Security in Federated Learning, Distributed Systems

- [Byzantine Robust Aggregation in Federated Distillation with Adversaries](https://doi.org/10.1109/icdcs60910.2024.00086)
  - Wenrui Li, Hanlin Gu, Sheng Wan, Zhirong Luan, Wei Xi, Lixin Fan, Qiang Yang, Badong Chen；Institute of Artificial Intelligence and Robotics, Xi&#x0027;an Jiaotong University,Xi&#x0027;an,China; WeBank AI Lab,Shenzhen,China; Hong Kong University of Science and Technology,Department of Computer Science,Hong Kong,China; School of Electrical Engineering, Xi&#x0027;an University of Technology,Xi&#x0027;an,China; Xi&#x0027;an Jiaotong University,Department of Computer Science,Xi&#x0027;an,China。
  - 该工作研究Security in Federated Learning中的「与对手联合蒸馏中的拜占庭稳健聚合」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Federated Learning, Byzantine Fault Tolerance, Security, Security in Federated Learning

- [Calibre: Towards Fair and Accurate Personalized Federated Learning with Self-Supervised Learning](https://doi.org/10.1109/icdcs60910.2024.00087)
  - Sijia Chen, Ningxin Su, Baochun Li；University of Toronto,Department of Electrical and Computer Engineering,Toronto,Ontario,Canada。
  - Calibre研究Fairness in Federated Learning中的「Calibre：通过自我监督学习迈向公平准确的个性化联邦学习」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善资源或服务公平性。
  - 相较直接套用通用分布式策略，核心创新是把「Calibre：通过自我监督学习迈向公平准确的个性化联邦学习」中的特定状态、约束或操作变成一级设计对象。
  - Federated Learning, Fairness in Federated Learning, Distributed Systems

- [Tackling System-Induced Bias in Federated Learning: A Pricing-Based Incentive Mechanism](https://doi.org/10.1109/icdcs60910.2024.00088)
  - Shuo Wang, Bing Luo, Ming Tang；Southern University of Science and Technology,Department of Computer Science and Engineering,Shenzhen,China; Data Science Research Center, Duke Kunshan University,Suzhou,China。
  - 该工作研究Incentives in Federated Learning中的「解决联邦学习中系统引起的偏差：基于定价的激励机制」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「解决联邦学习中系统引起的偏差：基于定价的激励机制」中的特定状态、约束或操作变成一级设计对象。
  - Federated Learning, Incentives in Federated Learning, Distributed Systems

- [MLPing: Real-Time Proactive Fault Detection and Alarm for Large-Scale Distributed IDC Network](https://doi.org/10.1109/icdcs60910.2024.00089)
  - Xian Yu, Kejiang Ye, Dongbiao He, Xiaofan Chen, Chengzhong Xu, Jianhui Li, Gaogang Xie；CNIC, CAS; SIAT, CAS; Sangfor Technologies Inc; University of Macau,Faculty of Science and Technology。
  - MLPing研究Fairness in Federated Learning中的「MLPing：大规模分布式IDC网络的实时主动故障检测和报警」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善故障下的可用性与正确性。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - Federated Learning, Fairness in Federated Learning, Distributed Systems

- [Towards Integrated Energy-Communication-Transportation Hub: A Base-Station-Centric Design in 5G and Beyond](https://doi.org/10.1109/icdcs60910.2024.00090)
  - Linfeng Shen, Guanzhen Wu, Cong Zhang, Xiaoyi Fan, Jiangchuan Liu；School of Computing Science, Simon Fraser University; Jiangxing Intelligence Inc。
  - 该工作研究Industrial Network and Data Center Optimizations中的「迈向能源、通信、交通一体化枢纽：5G 及其他领域以基站为中心的设计」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善能耗或碳效率。
  - 相较直接套用通用分布式策略，核心创新是把「迈向能源、通信、交通一体化枢纽：5G 及其他领域以基站为中心的设计」中的特定状态、约束或操作变成一级设计对象。
  - Industrial Network and Data Center Optimizations, Distributed Systems

- [Dissecting the Applicability of HTTP/3 in Content Delivery Networks](https://doi.org/10.1109/icdcs60910.2024.00091)
  - Mengying Zhou, Yang Chen, Shihan Lin, Xin Wang, Bingyang Liu, Aaron Yi Ding；School of Computer Science, Fudan University,Shanghai Key Lab of Intelligent Information Processing,China; Huawei Technologies Co. Ltd.,China; Delft University of Technology,Department of Engineering Systems and Services,The Netherlands。
  - 该工作研究Industrial Network and Data Center Optimizations中的「剖析 HTTP/3 在内容分发网络中的适用性」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「剖析 HTTP/3 在内容分发网络中的适用性」中的特定状态、约束或操作变成一级设计对象。
  - Industrial Network and Data Center Optimizations, Distributed Systems

- [The SPATIAL Architecture: Design and Development Experiences from Gauging and Monitoring the AI Inference Capabilities of Modern Applications](https://doi.org/10.1109/icdcs60910.2024.00092)
  - Abdul-Rasheed Ottun, Rasinthe Marasinghe, Toluwani Elemosho, Mohan Liyanage, Mohamad Ragab, Prachi Bagave, Marcus Westberg, Mehrdad Asadi, Michell Boerger, Chamara Sandeepa, Thulitha Senevirathna, Bartlomiej Siniarski, Madhusanka Liyanage, Vinh Hoa La, Manh-Dung Nguyen, Edgardo Montes De Oca, Tessa Oomen, João Fernando Ferreira Gonçalves, Illija Tanasković, Sasa Klopanovic, Nicolas Kourtellis, Claudio Soriente, Jason Pridmore, Ana Rosa Cavalli, Drasko Draskovic, Samuel Marchal, Shen Wang, David Solans Noguero, Nikolay Tcholtchev, Aaron Yi Ding, Huber Flores；University of Tartu,Estonia; University of Southampton,United Kingdom; Delft University of Technology,Netherlands; Vrije Universiteit Brussel,Belgium; Fraunhofer Institute for Open Communication Systems,Germany; University College Dublin,Ireland 等。
  - The SPATIAL Architecture研究Industrial Network and Data Center Optimizations中的「空间架构：衡量和监控现代应用的人工智能推理能力的设计和开发经验」：以在线模型请求为单位，组织模型/算子放置、并行执行、状态缓存和请求排队。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「空间架构：衡量和监控现代应用的人工智能推理能力的设计和开发经验」中的特定状态、约束或操作变成一级设计对象。
  - Industrial Network and Data Center Optimizations, Distributed Systems

- [Enhancing AI-Generated Content Efficiency Through Adaptive Multi-Edge Collaboration](https://doi.org/10.1109/icdcs60910.2024.00093)
  - Changfu Xu, Jianxiong Guo, Jiandian Zeng, Shengguang Meng, Xiaowen Chu, Jiannong Cao, Tian Wang；BNU-HKBU United International College,Guangdong Provincial Key Laboratory IRADS,Zhuhai,China; Institute of Artificial Intelligence and Future Networks, Beijing Normal University,Zhuhai,China; Guangdong Donghua Faster Software Co., LTD,Zhuhai,China; The Hong Kong University of Science and Technology (Guangzhou),Guangzhou,China; The Hong Kong Polytechnic University,Hong Kong,China。
  - 该工作研究Edge-Enhanced AI中的「通过自适应多边协作提高人工智能生成内容的效率」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - Edge Computing, Edge-Enhanced AI, Distributed Systems

- [ERS: Faster LiDAR Point Cloud Registration for Connected Vehicles](https://doi.org/10.1109/icdcs60910.2024.00094)
  - Yu Zhao, Jinrui Zhou, Mingjun Xiao, Jie Wu, He Sun；School of Computer Science and Technology / Suzhou Institute for Advanced Study, University of Science and Technology of China,Hefei,P. R. China; Temple University,Department of Computer and Information Sciences,USA。
  - ERS研究Vehicular Networking and Applications中的「ERS：更快的联网车辆 LiDAR 点云注册」：将终端位置/移动、传感数据、链路和能量状态一起带入感知、通信或计算决策。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「ERS：更快的联网车辆 LiDAR 点云注册」中的特定状态、约束或操作变成一级设计对象。
  - Mobile/Space Networks, Vehicular Networking and Applications, Distributed Systems

- [Fed-MS: Fault Tolerant Federated Edge Learning with Multiple Byzantine Servers](https://doi.org/10.1109/icdcs60910.2024.00095)
  - Senmao Qi, Hao Ma, Yifei Zou, Yuan Yuan, Peng Li, Dongxiao Yu；School of Computer Science and Technology, Shandong University,Qingdao,China; School of Computer Science and Technology, University of Aizu,Fukushima,Japan。
  - Fed-MS研究Secure Federated Learning中的「Fed-MS：使用多个拜占庭服务器的容错联合边缘学习」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善故障下的可用性与正确性。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Federated Learning, Edge Computing, Byzantine Fault Tolerance, Security

- [BCLB: A Scalable and Cooperative Layer-4 Load Balancer for Data Centers](https://doi.org/10.1109/icdcs60910.2024.00096)
  - Shu Yang, Xinze Wu, Laizhong Cui；Shenzhen University,College of Computer Science and Software Engineering,Shenzhen,China。
  - BCLB研究Industrial Network and Data Center Optimizations中的「BCLB：适用于数据中心的可扩展且协作的第 4 层负载均衡器」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善吞吐、扩展性或资源效率。
  - 相较把相互影响的子问题分开优化，核心创新是在同一目标下联合决定原本分离的放置、调度、通信或保护策略。
  - Industrial Network and Data Center Optimizations, Distributed Systems

- [OASIS: Offsetting Active Reconstruction Attacks in Federated Learning](https://doi.org/10.1109/icdcs60910.2024.00097)
  - Tre' R. Jeter, Truc Nguyen, Raed Alharbi, My T. Thai；University of Florida,Gainesville,FL,USA; National Renewable Energy Laboratory,Golden,CO,USA; Saudi Electronic University,Riyadh,Saudi Arabia。
  - OASIS研究Secure Federated Learning中的「OASIS：抵消联邦学习中的主动重建攻击」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善安全、隐私或可验证性。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Federated Learning, Security, Secure Federated Learning, Distributed Systems

- [BB-Align: A Lightweight Pose Recovery Framework for Vehicle-to-Vehicle Cooperative Perception](https://doi.org/10.1109/icdcs60910.2024.00098)
  - Lixing Song, William Valentine, Qing Yang, Honggang Wang, Hua Fang, Ye Liu；Rose-Hulman Institute of Technology; University of North Texas; Yeshiva University; University of Massachusetts Dartmouth; Macau University of Science and Technology。
  - BB-Align研究Vehicular Networking and Applications中的「BB-Align：用于车辆间协作感知的轻量级姿态恢复框架」：将终端位置/移动、传感数据、链路和能量状态一起带入感知、通信或计算决策。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较把相互影响的子问题分开优化，核心创新是在同一目标下联合决定原本分离的放置、调度、通信或保护策略。
  - Mobile/Space Networks, Vehicular Networking and Applications, Distributed Systems

- [Resolve Cross-Channel Interference for LoRa](https://doi.org/10.1109/icdcs60910.2024.00099)
  - Fu Yu, Xiaolong Zheng, Yuhao Ma, Liang Liu, Huadong Ma；Beijing University of Posts and Telecommunications,Beijing,P. R. China。
  - 该工作研究Wireless Network Enhancements中的「解决 LoRa 的跨通道干扰」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「解决 LoRa 的跨通道干扰」中的特定状态、约束或操作变成一级设计对象。
  - Wireless Network Enhancements, Distributed Systems

- [RideGuard: Micro-Mobility Steering Maneuver Prediction with Smartphones](https://doi.org/10.1109/icdcs60910.2024.00100)
  - Zengyi Han, Xuefu Dong, Liqiang Xu, Zhen Zhu, En Wang, Yuuki Nishiyama, Kaoru Sezaki；Dalian Maritime University,China; University of Tokyo,Japan; Jilin University,China。
  - RideGuard研究Smart Device Applications中的「RideGuard：使用智能手机进行微移动转向操作预测」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「RideGuard：使用智能手机进行微移动转向操作预测」中的特定状态、约束或操作变成一级设计对象。
  - Smart Device Applications, Distributed Systems

- [A Battery Lifespan-Aware Protocol for LPWAN](https://doi.org/10.1109/icdcs60910.2024.00101)
  - Sezana Fahmida, Akshar Chavan, Venkata Prashant Modekurthy, Abusayeed Saifullah, Marco Brocanelli；Wayne State University; The Ohio State University; University of Nevada,Las Vegas。
  - 该工作研究Wireless Network Enhancements中的「LPWAN 电池寿命感知协议」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「LPWAN 电池寿命感知协议」中的特定状态、约束或操作变成一级设计对象。
  - Wireless Network Enhancements, Distributed Systems

- [mmHand: 3D Hand Pose Estimation Leveraging mmWave Signals](https://doi.org/10.1109/icdcs60910.2024.00102)
  - Hao Kong, Haoxin Lyu, Jiadi Yu, Linghe Kong, Junlin Yang, Yanzhi Ren, Hongbo Liu, Yi-Chao Chen；Shanghai University,Shanghai,China; Shanghai Jiao Tong University,Shanghai,China; University of Electronic Science and Technology of China,Chengdu,China。
  - mmHand研究Smart Device Applications中的「mmHand：利用毫米波信号进行 3D 手部姿势估计」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「mmHand：利用毫米波信号进行 3D 手部姿势估计」中的特定状态、约束或操作变成一级设计对象。
  - Smart Device Applications, Distributed Systems

- [GesturePrint: Enabling User Identification for mmWave-Based Gesture Recognition Systems](https://doi.org/10.1109/icdcs60910.2024.00103)
  - Lilin Xu, Keyi Wang, Chaojie Gu, Xiuzhen Guo, Shibo He, Jiming Chen；Zhejiang University; University of California San Diego。
  - GesturePrint研究Smart Device Applications中的「GesturePrint：为基于毫米波的手势识别系统启用用户识别」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「GesturePrint：为基于毫米波的手势识别系统启用用户识别」中的特定状态、约束或操作变成一级设计对象。
  - Smart Device Applications, Distributed Systems

- [CoCFL: A Lightweight Blockchain-based Federated Learning Framework in IoT Context](https://doi.org/10.1109/icdcs60910.2024.00104)
  - Jianrong Wang, Yang Shi, Dengcheng Hu, Keqiu Li, Xiulong Liu；College of Intelligence and Computing, Tianjin University,China。
  - CoCFL研究Blockchain Scalability and Payments中的「CoCFL：物联网环境中基于区块链的轻量级联邦学习框架」：围绕 client 选择、本地更新、模型聚合和通信/同步，显式处理数据、算力或可靠性异构。题目明确的关键手段包括federated aggregation；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「CoCFL：物联网环境中基于区块链的轻量级联邦学习框架」中的特定状态、约束或操作变成一级设计对象。
  - Federated Learning, Blockchain, IoT/CPS, Blockchain Scalability and Payments

- [LED Can Backscatter: Multi-Modal Based 3D Localization via LED-Tag](https://doi.org/10.1109/icdcs60910.2024.00105)
  - Shiyuan Ma, Lei Xie, Chuyu Wang, Long Fan, Jingyi Ning, Qing Guo, Baoliu Ye, Sanglu Lu；Nanjing University,State Key Laboratory for Novel Software Technology,Nanjing,China。
  - LED Can Backscatter研究Smart Device Applications中的「LED 可以反向散射：通过 LED 标签进行基于多模态的 3D 定位」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「LED 可以反向散射：通过 LED 标签进行基于多模态的 3D 定位」中的特定状态、约束或操作变成一级设计对象。
  - Smart Device Applications, Distributed Systems

- [Approximation Algorithm for Connected Submodular Function Maximization Problems](https://doi.org/10.1109/icdcs60910.2024.00106)
  - Wenzheng Xu, He Xue, Jing Li, Weifa Liang, Zichuan Xu, Pan Zhou, Xiaohua Jia, Sajal K. Das；College of Computer Science, Sichuan University,Chengdu,P. R. China; The Hong Kong Polytechnic University,Department of Computing,Hong Kong,P. R. China; City University of Hong Kong,Department of Computer Science,Hong Kong,P. R. China; School of Software, Dalian University of Technology,Dalian,P. R. China; School of Cyber Science and Engineering, Huazhong University of Science &#x0026; Technology,P. R. China; Missouri University of Science and Technology,Department of Computer Science,Rolla,USA。
  - 该工作研究Mobile Algorithms and AI Optimizations中的「连通子模函数最大化问题的逼近算法」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「连通子模函数最大化问题的逼近算法」中的特定状态、约束或操作变成一级设计对象。
  - Mobile Algorithms and AI Optimizations, Distributed Systems

- [CSS: Built-In Channel State Scrambling for Secure Wi-Fi Based Sensing](https://doi.org/10.1109/icdcs60910.2024.00107)
  - Xiao Deng, Dongyu Xia, Xun Wang, Shuyu Shi, Wei Wang；Nanjing University,State Key Laboratory for Novel Software Technology,Nanjing,China。
  - CSS研究Wireless Network Enhancements中的「CSS：内置通道状态加扰，用于基于 Wi-Fi 的安全传感」：指定对手可观测/篡改的数据和攻击面，再把检测、隔离、加密或隐私保护插入具体数据路径。直接目标是改善安全、隐私或可验证性。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Security, Wireless Network Enhancements, Distributed Systems

- [Optimized Live 4K Video Multicast Streaming on Commodity WiGig Devices](https://doi.org/10.1109/icdcs60910.2024.00108)
  - Zhaoyuan He, Changhan Ge, Wangyang Li, Lili Qiu, Peijie Li, Ghufran Baig；The University of Texas at Austin,Austin,TX,United States of America; Google,Austin,TX,United States of America。
  - 该工作研究Mobile Algorithms and AI Optimizations中的「在商用 WiGig 设备上优化实时 4K 视频组播流」：以持续到达的 record、operator state 和 partition 为单位，组织计算、状态迁移与故障恢复。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「在商用 WiGig 设备上优化实时 4K 视频组播流」中的特定状态、约束或操作变成一级设计对象。
  - Stream Processing, Mobile Algorithms and AI Optimizations, Distributed Systems

- [Leveraging CAVs to Improve Traffic Efficiency: An MARL-Based Approach](https://doi.org/10.1109/icdcs60910.2024.00109)
  - Weizhen Han, Enshu Wang, Bingyi Liu, Zhi Liu, Xun Shao, Libing Wu, Jianping Wang；School of Computer Science and Artificial Intelligence, Wuhan University of Technology,Wuhan,China; School of Cyber Science and Engineering, Wuhan University,Wuhan,China; The University of Electro-Communications,Department of Computer and Network Engineering,Tokyo,Japan; Toyohashi University of Technology,Department of Electrical and Electronic Information Engineering,Aichi,Japan; City University of Hong Kong,Department of Computer Science,Hong Kong。
  - 该工作研究Vehicular Networking and Applications中的「利用 CAV 提高交通效率：基于 MARL 的方法」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「利用 CAV 提高交通效率：基于 MARL 的方法」中的特定状态、约束或操作变成一级设计对象。
  - Mobile/Space Networks, Vehicular Networking and Applications, Distributed Systems

- [Joint AI Task Allocation and Virtual Object Quality Manipulation for Improved MAR App Performance](https://doi.org/10.1109/icdcs60910.2024.00110)
  - Niloofar Didar, Marco Brocanelli；Wayne State University,Department of Computer Science,Detroit,MI,USA; The Ohio State University,Department of Electrical and Computer Engineering,Columbus,OH,USA。
  - 该工作研究Mobile Algorithms and AI Optimizations中的「联合 AI 任务分配和虚拟对象质量操纵可提高 MAR 应用程序性能」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较把相互影响的子问题分开优化，核心创新是在同一目标下联合决定原本分离的放置、调度、通信或保护策略。
  - Mobile Algorithms and AI Optimizations, Distributed Systems

- [Coreset-sharing based Collaborative Model Training among Peer Vehicles](https://doi.org/10.1109/icdcs60910.2024.00111)
  - Han Zheng, Mengjing Liu, Fan Ye, Yuanyuan Yang；Stony Brook University,Department of Electrical and Computer Engineering。
  - 该工作研究Vehicular Networking and Applications中的「基于核心集共享的同行车辆协作模型训练」：以 worker、model shard/layer、gradient 或 expert 为单位组织计算、集合通信、内存与容错状态。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较把相互影响的子问题分开优化，核心创新是在同一目标下联合决定原本分离的放置、调度、通信或保护策略。
  - Mobile/Space Networks, Vehicular Networking and Applications, Distributed Systems

- [Network Topology Design for Distributed Quantum Computing](https://doi.org/10.1109/icdcs60910.2024.00115)
  - Yingling Mao, Yu Liu, Xiaojun Shang, Yuanyuan Yang；Stony Brook University,Department of Electrical and Computer Engineering,USA; The University of Texas at Arlington,Department of Computer Science and Engineering,USA。
  - 该工作研究Distributed Design中的「分布式量子计算的网络拓扑设计」：以 quantum circuit/job、qubit/entanglement 资源和网络路径为对象，决定编译、放置、路由或经典–量子协同。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Quantum Computing/Networking, Distributed Design, Distributed Systems

- [Counterfactual Reward Estimation for Credit Assignment in Multi-agent Deep Reinforcement Learning over Wireless Video Transmission](https://doi.org/10.1109/icdcs60910.2024.00112)
  - Y. Wenhan, Liangxin Qian, Terence Jie Chua, Jun Zhao；Graduate College, Nanyang Technological University; College of Computing and Data Science, Nanyang Technological University。
  - 该工作研究Wireless Network Enhancements中的「无线视频传输多智能体深度强化学习中信用分配的反事实奖励估计」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。题目明确的关键手段包括强化学习；直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「无线视频传输多智能体深度强化学习中信用分配的反事实奖励估计」中的特定状态、约束或操作变成一级设计对象。
  - Multi-Agent Systems, Reinforcement Learning, Wireless Network Enhancements, Distributed Systems

- [EPS Placement and Lightweight Entanglement Routing for Quantum Data Networks](https://doi.org/10.1109/icdcs60910.2024.00113)
  - Qiucheng Zhu, Yangming Zhao, Hongli Xu, Liusheng Huang, Chunming Qiao；School of Computer Science and Technology, University of Science and Technology of China; University at Buffalo,Department of Computer Science and Engineering。
  - 该工作研究Quantum Network Entanglement Routing中的「量子数据网络的 EPS 布局和轻量级纠缠路由」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「量子数据网络的 EPS 布局和轻量级纠缠路由」中的特定状态、约束或操作变成一级设计对象。
  - Quantum Computing/Networking, Quantum Network Entanglement Routing, Distributed Systems

- [Adaptive User-Centric Entanglement Routing in Quantum Data Networks](https://doi.org/10.1109/icdcs60910.2024.00114)
  - Lei Wang, Jieming Bian, Jie Xu；University of Miami,Department of Electrical and Computer Engineering,Coral Gables,FL,USA。
  - 该工作研究Quantum Network Entanglement Routing中的「量子数据网络中以用户为中心的自适应纠缠路由」：以 flow/packet/path 和当前链路/队列为输入，决定路由、速率、分流或缓存规则。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - Quantum Computing/Networking, Quantum Network Entanglement Routing, Distributed Systems

- [Dynamic Routing and Post-Processing Strategies for Hybrid Quantum Key Distribution Networks](https://doi.org/10.1109/icdcs60910.2024.00116)
  - Omar Amer, Walter O. Krawec, Md. Zakir Hossain, Victoria U. Manfredi, Bing Wang；Global Technology Applied Research, JPMorgan Chase Bank,New York City,NY,United States; School of Computing, University of Connecticut,Storrs,CT,United States; Wesleyan University,Department of Mathematics and Computer Science,Middletown,CT,United States。
  - 该工作研究Quantum Network Entanglement Routing中的「混合量子密钥分配网络的动态路由和后处理策略」：以 flow/packet/path 和当前链路/队列为输入，决定路由、速率、分流或缓存规则。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - Quantum Computing/Networking, Quantum Network Entanglement Routing, Distributed Systems

- [Quantum Network Routing Based on Surface Code Error Correction](https://doi.org/10.1109/icdcs60910.2024.00117)
  - Tianjie Hu, Jindi Wu, Qun Li；William &#x0026; Mary,Department of Computer Science,Williamsburg,VA,USA。
  - 该工作研究Quantum Network Entanglement Routing中的「基于表面码纠错的量子网络路由」：以 flow/packet/path 和当前链路/队列为输入，决定路由、速率、分流或缓存规则。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「基于表面码纠错的量子网络路由」中的特定状态、约束或操作变成一级设计对象。
  - Quantum Computing/Networking, Quantum Network Entanglement Routing, Distributed Systems

- [GameTE: A Game-Theoretic Distributed Traffic Engineering in Trustless Multi-Domain SDN](https://doi.org/10.1109/icdcs60910.2024.00118)
  - Yangyang Liu, Jingyu Hua, Yuan Zhang, Sheng Zhong；Nanjing University,The State Key Laboratory of Novel Software Technology,Nanjing,China。
  - GameTE研究Network Security Management中的「GameTE：无信任多域 SDN 中的博弈论分布式流量工程」：以 flow/packet/path 和当前链路/队列为输入，决定路由、速率、分流或缓存规则。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较依赖单一中心控制器或高带宽集中环境，核心创新是把决策或执行拆到多节点并显式处理协调代价。
  - Security, Network Security Management, Distributed Systems

- [HiddenTor: Toward a User-Centric and Private Query System for Tor BridgeDB](https://doi.org/10.1109/icdcs60910.2024.00119)
  - Yichen Zang, Chengjun Cai, Wentao Dong, Lei Xu, Cong Wang；City University of Hong Kong,Hong Kong,China; City University of Hong Kong (Dongguan),Dongguan,China。
  - HiddenTor研究Privacy-preserving Networks中的「HiddenTor：面向 Tor BridgeDB 打造以用户为中心的私密查询系统」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「HiddenTor：面向 Tor BridgeDB 打造以用户为中心的私密查询系统」中的特定状态、约束或操作变成一级设计对象。
  - Privacy, Privacy-preserving Networks, Distributed Systems

- [Physical Layer Secret Key Generation Leveraging Proactive Pilot Contamination](https://doi.org/10.1109/icdcs60910.2024.00120)
  - Limin Liu, Hongbo Liu, Yicong Du, Ziyu Shao, Haomiao Yang, Yanzhi Ren；University of Electronic Science and Technology of China,Dept. of CS。
  - 该工作研究Innovative User Authentication中的「利用主动导频污染生成物理层密钥」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「利用主动导频污染生成物理层密钥」中的特定状态、约束或操作变成一级设计对象。
  - Security, Innovative User Authentication, Distributed Systems

- [EarPass: Unlock When Wearing Your Earphones](https://doi.org/10.1109/icdcs60910.2024.00121)
  - Yanze Xie, Mengzhen Gao, Xiaoning Liu, Shuo Huana, Helei Cui, Zhiwen Yu, Bin Guo；Northwestern Polytechnical University; RMIT- University; Monash University。
  - EarPass研究Innovative User Authentication中的「EarPass：佩戴耳机时解锁」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「EarPass：佩戴耳机时解锁」中的特定状态、约束或操作变成一级设计对象。
  - Security, Innovative User Authentication, Distributed Systems

- [Vehigan:Generative Adversarial Networks for Adversarially Robust V2X Misbehavior Detection Systems](https://doi.org/10.1109/icdcs60910.2024.00122)
  - Md Hasan Shahriar, Mohammad Raashid Ansari, Jean-Philippe Monteuuis, Cong Chen, Jonathan Petit, Y. Thomas Hou, Wenjing Lou；Virginia Polytechnic Institute and State University,Blacksburg,VA,USA; Qualcomm Technologies, Inc.,Boxborough,MA,USA。
  - Vehigan研究Network Security Management中的「Vehigan：用于对抗性鲁棒 V2X 不当行为检测系统的生成对抗网络」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「Vehigan：用于对抗性鲁棒 V2X 不当行为检测系统的生成对抗网络」中的特定状态、约束或操作变成一级设计对象。
  - Security, Network Security Management, Distributed Systems

- [PrivRE: Regular Expression Matching for Encrypted Packet Inspection](https://doi.org/10.1109/icdcs60910.2024.00123)
  - Xiaoyang Hou, Jian Liu, Tianyu Tu, Rui Zhang, Kui Ren；Zhejiang University。
  - PrivRE研究Privacy-preserving Networks中的「PrivRE：用于加密数据包检查的正则表达式匹配」：指定对手可观测/篡改的数据和攻击面，再把检测、隔离、加密或隐私保护插入具体数据路径。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「PrivRE：用于加密数据包检查的正则表达式匹配」中的特定状态、约束或操作变成一级设计对象。
  - Privacy, Privacy-preserving Networks, Distributed Systems

- [SPOT: Structure Patching and Overlap Tweaking for Effective Pipelining in Privacy-Preserving MLaaS with Tiny Clients](https://doi.org/10.1109/icdcs60910.2024.00124)
  - Xiangrui Xu, Qiao Zhang, Rui Ning, Chunsheng Xin, Hongyi Wu；Old Dominion University,Department of Computer Science,Norfolk,USA; Chongqing University,Department of Computer Science,Chongqing,China; Old Dominion University,Department of Electrical &#x0026; Computer Engineering,Norfolk,USA; University of Arizona,Department of Electrical &#x0026; Computer Engineering,Tucson,USA。
  - SPOT研究Secure Federated Learning中的「SPOT：结构修补和重叠调整，以实现小客户端隐私保护 MLaaS 中的有效流水线」：以在线模型请求为单位，组织模型/算子放置、并行执行、状态缓存和请求排队。直接目标是改善安全、隐私或可验证性。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Federated Learning, Privacy, Security, Secure Federated Learning

- [OpenAuth: Human Body-Based User Authentication Using mmWave Signals in Open-World Scenarios](https://doi.org/10.1109/icdcs60910.2024.00125)
  - Junlin Yang, Jiadi Yu, Linghe Kong, Yanmin Zhu, Hong-Ning Dai；Shanghai Jiao Tong University,Department of Computer Science and Engineering,Shanghai,China; Hong Kong Baptist University,Department of Computer Science,Hong Kong,China。
  - OpenAuth研究Innovative User Authentication中的「OpenAuth：在开放世界场景中使用毫米波信号进行基于人体的用户身份验证」：从用户/设备/代理的观测、credential 或时序行为中给出连续身份判定与验证。直接目标是改善安全、隐私或可验证性。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Security, Innovative User Authentication, Distributed Systems

- [WaveKey: Secure Mobile Ad Hoc Access to RFID-Protected Systems](https://doi.org/10.1109/icdcs60910.2024.00126)
  - Dianqi Han, Ang Li, Jiawei Li, Yan Zhang, Tao Li, Yanchao Zhang；University of Texas at Arlington; University of Michigan-Dearborn; Arizona State University; University of Akron。
  - WaveKey研究Privacy-preserving Networks中的「WaveKey：对 RFID 保护系统的安全移动临时访问」：指定对手可观测/篡改的数据和攻击面，再把检测、隔离、加密或隐私保护插入具体数据路径。直接目标是改善安全、隐私或可验证性。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Privacy, Security, IoT/CPS, Privacy-preserving Networks

- [Dual Study of Canvas Fingerprinting Based Authentication: A Novel Spoofing Attack and the Countermeasure](https://doi.org/10.1109/icdcs60910.2024.00127)
  - Zengrui Liu, Nitesh Saxena；Texas A&#x0026;M University。
  - 该工作研究Innovative User Authentication中的「基于画布指纹认证的双重研究：一种新型欺骗攻击及其对策」：从用户/设备/代理的观测、credential 或时序行为中给出连续身份判定与验证。直接目标是改善安全、隐私或可验证性。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Security, Innovative User Authentication, Distributed Systems

- [PIPO: Privacy-Preserving Convolutional Neural Network Inference with Plaintext Operations](https://doi.org/10.1109/icdcs60910.2024.00128)
  - Tian Zhou, Lixin Gao；University of Massachusetts,Department of Electrical and Computer Engineering,Amherst,USA。
  - PIPO研究Privacy-preserving Networks中的「PIPO：使用明文操作进行隐私保护的卷积神经网络推理」：以在线模型请求为单位，组织模型/算子放置、并行执行、状态缓存和请求排队。直接目标是改善安全、隐私或可验证性。
  - 相较在性能方案之外事后叠加安全机制，核心创新是将对手、隐私或信任假设直接写入协议与优化目标。
  - Privacy, Privacy-preserving Networks, Distributed Systems

- [HammerHead: Leader Reputation for Dynamic Scheduling](https://doi.org/10.1109/icdcs60910.2024.00129)
  - Giorgos Tsimos, Anastasios Kichidis, Alberto Sonnino, Lefteris Kokoris-Kogias；University of Maryland,Mysten Labs,College Park; Mysten Labs; University College London,Mysten Labs; IST Austria,Mysten Labs。
  - HammerHead研究Network Security Management中的「HammerHead：动态调度领域的领导者声誉」：根据任务/请求属性、节点资源和运行时约束，决定放置位置、执行顺序、并行度或资源份额。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较事先固定的静态配置，核心创新是让系统依据运行时状态在线调整。
  - Security, Scheduling, Network Security Management, Distributed Systems

- [WIRE: Web3 Integrated Reputation Engine](https://doi.org/10.1109/icdcs60910.2024.00130)
  - Suraj Shamsundar Jain, Huancheng Zhou, Guofei Gu；Texas A&#x0026;M University,SUCCESS Lab。
  - WIRE研究Network Security Management中的「WIRE：Web3 集成声誉引擎」：先明确系统中可观测的状态、可执行的操作与约束，再为该场景设计专用协议或优化方法。直接目标是改善题目所指的性能、正确性或资源目标。
  - 相较直接套用通用分布式策略，核心创新是把「WIRE：Web3 集成声誉引擎」中的特定状态、约束或操作变成一级设计对象。
  - Security, Network Security Management, Distributed Systems
