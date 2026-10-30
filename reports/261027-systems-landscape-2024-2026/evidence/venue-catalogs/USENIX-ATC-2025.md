# USENIX ATC 2025 论文列表

USENIX ATC 2025 官方 Technical Sessions 中共有 100 篇标记为 `node-paper` 的正式论文。本列表逐项核验后排除 joint keynote、Flame Award、poster、break 及其他非论文活动；标题均链接到 USENIX 官方 presentation 页。每篇依次列出作者与机构、基于官方详细摘要的预读说明、相较既有方法的核心创新和细粒度方向。

- [Fast ACS: Low-Latency File-Based Ordered Message Delivery at Scale](https://www.usenix.org/conference/atc25/presentation/gupta)
  - Sushant Kumar Gupta, Anil Raghunath Iyer, Chang Yu, Neel Bagora, Olivier Pomerleau, Vivek Kumar, and Prunthaban Kanthakumar, Google LLC
  - Fast ACS 面向生产者向跨城、跨洲集群中数千个不同速消费者分发文件式消息的实时链路，需同时保证有序、至少一次交付且不压垮慢消费者。系统在集群间用两边 RPC 运送消息，在集群内以单边 RDMA 从文件向消费者扇出；已部署于数十个集群，单集群峰值为 Tbps 级流量，全球交付 p99 为数秒或亚秒且资源成本较低。
  - 相较把跨集群与集群内扇出都放在普通 broker/RPC 路径上，核心创新是以文件作为可追赶的有序介质，并按通信边界组合 RPC 与 RDMA，在保留交付语义时避免数千消费者复制放大。
  - 跨集群消息系统、文件式有序交付、RDMA 扇出、生产级低尾延迟

- [Poby: SmartNIC-accelerated Image Provisioning for Coldstart in Clouds](https://www.usenix.org/conference/atc25/presentation/chang)
  - Zihao Chang and Jiaqi Zhu, SKLP, Institute of Computing Technology, CAS; University of Chinese Academy of Sciences; Haifeng Sun, Peking University; Yunlong Xie, Kan Shi, Ninghui Sun, Yungang Bao, and Sa Wang, SKLP, Institute of Computing Technology, CAS; University of Chinese Academy of Sciences;
  - Poby 处理容器与 FaaS 冷启动中常被忽视的镜像供应路径：将下载、解压、校验和文件安装等操作按特性分配到 BlueField SmartNIC 的嵌入式 CPU 与专用加速器，再用数据驱动流水线并行阶段，并以分布式供应缓解集中 registry 瓶颈。微服务/FaaS 测试中比 containerd 和 iSulad 分别快 13.2 倍和 8.0 倍，主机 CPU 占用比 iSulad 低 87.5%。
  - 相较仅预热实例、缩短镜像下载或用轻量隔离减少其他冷启动成本，核心创新是将“镜像供应”本身分解为可异构卸载、可流水化且可分布式执行的数据面。
  - SmartNIC 镜像供应、容器冷启动、软硬件协同流水线、分布式 Registry

- [Burst Computing: Quick, Sudden, Massively Parallel Processing on Serverless Resources](https://www.usenix.org/conference/atc25/presentation/barcelona-pons)
  - Daniel Barcelona-Pons, Universitat Rovira i Virgili and Barcelona Supercomputing Center; Aitor Arjona, Pedro García-López, Enrique Molina-Giménez, and Stepan Klymonchuk, Universitat Rovira i Virgili
  - Burst computing 针对突发到达、短时间内需大规模并行的作业，用 group invocation 一次启动一组具有同时就绪保证的 worker，并将 worker 紧凑装入更少容器以获得数据与通信局部性。OpenWhisk 原型用零拷贝消息和集合通信支持 worker 同步协作；相比标准 FaaS，TeraSort 加速 2 倍，PageRank 远程通信减少 98.5% 并加速 13 倍。
  - 相较以独立函数为隔离和伸缩单位、不保证并行成员同时就绪的 FaaS，核心创新是引入作业级隔离与成组调用语义，使 serverless 首次可直接运行同步消息传递型并行程序。
  - Serverless 突发并行、Group Invocation、作业级隔离、零拷贝集合通信

- [DEEPSERVE: Serverless Large Language Model Serving at Scale](https://www.usenix.org/conference/atc25/presentation/hu-junhao)
  - Junhao Hu, Peking University and Key Lab of HCST (PKU), MOE; Jiang Xu, Zhixia Liu, Yulong He, Yuetao Chen, Hao Xu, Jiang Liu, Jie Meng, Baoquan Zhang, Shining Wan, Gengyuan Dan, Zhiyu Dong, Zhihao Ren, and Changhong Liu, Huawei Cloud; Tao Xie, Key Lab of HCST (PKU), MOE and Peking University; Dayun Lin, Qin Zhang, Yue Yu, Hao Feng, Xusheng Chen, and Yizhou Shan, Huawei Cloud
  - DEEPSERVE 是运行于大规模 Ascend NPU 集群的生产级 serverless AI 平台：request–job–task 抽象同时承载后训练和模型服务，FLOWSERVE 以微内核式组件、NPU 中心执行和 SPMD 并行跑 LLM，调度器联合选择 prefill/decode 分离或同置实例。预热 pod、DRAM 预载和 NPU-fork 可在数秒内扩到 64 实例；系统已运行一年以上并对外提供微调、Agent 和普通模型服务 API。
  - 相较只管理单一推理引擎或把 serverless 仅当作容器弹性层，核心创新是统一任务抽象、NPU 微内核 serving、PD 混合布置和快速复制路径，形成从接口到扩容的完整生产栈。
  - Serverless LLM 平台、Ascend NPU、Prefill/Decode 混合调度、快速弹性扩容

- [Cosmic: Cost-Effective Support for Cloud-Assisted 3D Printing](https://www.usenix.org/conference/atc25/presentation/yao)
  - Yuan Yao, University of Southern California; Chuan He and Chinedum Okwudire, University of Michigan; Harsha V. Madhyastha, University of Southern California
  - Cosmic 将对时限极敏感的 3D 打印控制器放到公有云 serverless 中执行：测量表明通用平台的毫秒级唤醒和调用开销会让控制算法错过 deadline。系统按时间与数据依赖将控制计算拆到多个函数，并对可能超时的分支做及时投机执行。AWS Lambda 上 30 类打印作业均能按时控制，费用比对照方案低 2.8–3.5 倍。
  - 相较预留长驻服务或直接将整个控制循环装入一个函数，核心创新是以 deadline 为中心的函数分区和有节制的 speculative execution，用弹性资源抵消平台抖动。
  - 云辅助 3D 打印、实时 Serverless 控制、Deadline-Aware 分区、投机执行

- [GMI-DRL: Empowering Multi-GPU DRL with Adaptive-Grained Parallelism](https://www.usenix.org/conference/atc25/presentation/wang-yuke)
  - Yuke Wang, Rice University; Boyuan Feng, University of California Santa Barbara; Zheng Wang, University of California San Diego; Guyue Huang, University of California Santa Barbara; Tong (Tony) Geng, University of Rochester; Ang Li, Pacific Northwest National Laboratory; Yufei Ding, University of California San Diego
  - GMI-DRL 面向工业控制和自动驾驶等 DRL 训练中采样、推理、学习等异质任务对 GPU 资源与通信的不同需求，定义容量可调的子 GPU 抽象 GPU Multiplexing Instance。Coordinator 按运行时负载改变 GMI 粒度与资源配比，Communicator 为不同 GMI 间交互选择高效路径。DGX-A100 上训练吞吐最高提升 2.34 倍，GPU 利用率最高增加 40.8%。
  - 相较将 DRL 各阶段绑到整 GPU 或固定切分子 GPU，核心创新是用统一、可伸缩的 GMI 表达异质任务，再联动调度和专用通信，使并行粒度能跟随 DRL 阶段变化。
  - 多 GPU 深度强化学习、子 GPU 弹性分割、异质任务调度、GMI 通信

- [mTuner: Accelerating Parameter-Efficient Fine-Tuning on Multi-GPU Servers with Elastic Tensor](https://www.usenix.org/conference/atc25/presentation/huang-kezhao)
  - Kezhao Huang, Siqi Zhu, Mingshu Zhai, Liyan Zheng, Kinman Lei, Jiaao He, Yuyang Jin, and Jidong Zhai, Tsinghua University
  - mTuner 针对 7B–70B LLM 的多 GPU PEFT：冻结权重需高速缓存，激活和临时 tensor 又使显存在时间上碎片化。Elastic Tensor 用 gather、discard、execute 和 checkpoint 四种可调操作管理静态/运行时 tensor，延迟物化、放松依赖并按当前容量积累中间状态。对 PCIe 和 NVLink 服务器，吞吐最高分别提升 51.2% 和 24.8%，平均提升 28.3% 和 14.5%。
  - 相较训练框架的固定 tensor 生命期或只缩小可训参数的 PEFT，核心创新是把 tensor 的可用性、累积与释放提升为运行时可控抽象，用时间弹性而不是单一分片提高显存效率。
  - LLM PEFT、Elastic Tensor、多 GPU 显存管理、时间自适应累积

- [JENGA: Enhancing LLM Long-Context Fine-tuning with Contextual Token Sparsity](https://www.usenix.org/conference/atc25/presentation/wang-tuowei)
  - Tuowei Wang and Xingyu Chen, Tsinghua University; Kun Li and Ting Cao, Microsoft Research; Ju Ren and Yaoxue Zhang, Tsinghua University
  - JENGA 面向长上下文 LLM 微调中随序列增长的激活显存，按输入和层判断 token embedding 的信息量，动态淘汰冗余 token。训练好的 predictor 低成本预测稀疏模式，permutation-free、segment-based kernel 则直接在不规则模式上执行，避免 Shadowy Activation 让稀疏仅省计算而不省激活。端到端显存最高降低 1.93 倍，速度最高提升 1.36 倍。
  - 相较只减少可训参数的 PEFT 或只追求 FLOP 节省的 token sparsity，核心创新是定义 Contextual Token Sparsity 并将识别、模式预测和无排列 kernel 连成真正减少激活常驻量的微调路径。
  - 长上下文微调、Contextual Token Sparsity、激活显存压缩、Segment Kernel

- [FlexPipe: Maximizing Training Efficiency for Transformer-based Models with Variable-Length Inputs](https://www.usenix.org/conference/atc25/presentation/zhao-hairui)
  - Hairui Zhao, Jilin University and University of California, Riverside; Qi Tian, Jilin University; Hongliang Li, Jilin University and Key Laboratory of Symbolic Computation and Knowledge Engineering of the Ministry of Education, China; Zizhong Chen, University of California, Riverside
  - FlexPipe 处理多任务 Transformer 中 batch 序列长度跨迭代大幅波动、静态 pipeline partition 同时造成阶段等待和显存闲置的问题。它把每轮工作量和容量状态输入吞吐最大化问题，用高效启发式选新的并行配置，并通过 live flexibility 在不丢训练状态的情况下改变 pipeline parallelism。对现有方法平均提升 1.25 倍训练吞吐。
  - 相较只在单次迭代内对变长样本排序/打包、但跨迭代固定分区的方法，核心创新是把 pipeline 配置本身变成可无损热调整的运行时决策。
  - 变长 Transformer 训练、动态 Pipeline Parallelism、Live Reconfiguration、吞吐最大化

- [Optimus: Accelerating Large-Scale Multi-Modal LLM Training by Bubble Exploitation](https://www.usenix.org/conference/atc25/presentation/feng)
  - Weiqi Feng, Harvard University; Yangrui Chen, ByteDance; Shaoyu Wang, University of Southern California; Yanghua Peng and Haibin Lin, ByteDance; Minlan Yu, Harvard University
  - Optimus 针对 ViT/audio encoder 与 LLM 组成的多模态大模型在 3D 并行中因模态异质和复杂依赖产生的 GPU bubble。系统为 encoder 与 LLM 分别搜索并行方案，在不破坏数据依赖时将 encoder 计算填入 LLM bubble；它进一步将 encoder layer 拆成 kernel，以使用亚毫秒空隙。生产集群上 ViT-22B+GPT-175B、3072 GPU 训练时间缩短 20.5%–21.3%。
  - 相较对整个 MLLM 使用同一并行布局或只减少常规 pipeline bubble，核心创新是利用 encoder/LLM 的计算异质性，分别布局后在 kernel 粒度填充跨模块气泡。
  - 多模态大模型训练、3D 并行、Bubble Filling、Encoder/LLM 异质调度

- [Towards Optimal Rack-scale μs-level CPU Scheduling through In-Network Workload Shaping](https://www.usenix.org/conference/atc25/presentation/liao)
  - Xudong Liao, Hong Kong University of Science and Technology; Han Tian, University of Science and Technology of China; Xinchen Wan, Hong Kong University of Science and Technology; Chaoliang Zeng, BitIntelligence; Hao Wang, Hong Kong University of Science and Technology; Junxue Zhang, University of Science and Technology of China; Mengyu Ma, Inspur; Guyue (Grace) Liu, Peking University; Kai Chen, Hong Kong University of Science and Technology
  - Pallas 为微秒级服务做 rack-scale CPU 调度：数据面先按请求的 CPU demand 在网内将工作负载整形为高同质 shard，使服务器间负载均衡与机内排队可用简单策略近似最优。它同时跟踪长期分布漂移和短期 burst；比 RackSched 在中负载将尾延迟降低 8.5 倍，高负载时最高降低两个数量级。
  - 相较网络层做与应用无关的流量均衡、服务器内再使用复杂调度，核心创新是把任务 CPU 需求提前编码进网内分片，用输入整形消除后端调度的不确定性。
  - Rack-Scale CPU 调度、微秒级服务、网内工作负载整形、尾延迟

- [TGW: Operating an Efficient and Resilient Cloud Gateway at Scale](https://www.usenix.org/conference/atc25/presentation/yang-yifan)
  - Yifan Yang, Lin He, Jiasheng Zhou, Xiaoyi Shi, Yichi Xu, and Shicheng Wang, Tsinghua University; Jinlong E, Renmin University of China; Ying Liu, Tsinghua University; Junwei Zhang, Zhuang Yuan, and Hengyang Xu, Tencent
  - TGW 是服务腾讯云游戏与直播流量的生产级云网关，必须在大规模弹性公网接入和负载均衡中严格限制时延、抖动与丢包。其模块化架构分离高速转发面、可扩展状态迁移、故障恢复与故障检测/定位。测试床单节点转发能力为先前系统的 2.9 倍，集群间状态/流量可在 4 秒内无丢包迁移；连续八年的生产系统处理数十 Tbps，最坏丢包率为 10^-7–10^-4，多年保持 100% 可用性。
  - 相较把网关视为一个高速 middlebox 或仅优化转发内核，核心贡献是把数据面、海量连接状态生命周期和可观测的弹性恢复做成解耦系统，并以长期生产运行验证。
  - 生产云网关、有状态弹性迁移、故障检测定位、游戏/直播网络

- [MARC: Motion-Aware Rate Control for Mobile E-commerce Cloud Rendering](https://www.usenix.org/conference/atc25/presentation/zhao-yuankang)
  - Yuankang Zhao, Alibaba Group; University of Chinese Academy of Sciences; Furong Yang, Alibaba Group; Gerui Lv, University of Chinese Academy of Sciences; Qinghua Wu, University of Chinese Academy of Sciences and Purple Mountain Laboratories; Yanmei Liu, Jiuhai Zhang, Yutang Peng, Feng Peng, Hongyu Guo, and Ying Chen, Alibaba Group; Zhenyu Li, University of Chinese Academy of Sciences and Purple Mountain Laboratories; Gaogang Xie, University of Chinese Academy of Sciences and Computer Network Information Center, Chinese Academy of Sciences
  - MARC 从百万级手机电商云渲染会话观察到：用户正在旋转/移动 3D 场景时与静止观看时对延迟和画质的偏好不同，但交互高峰反而更易发生延迟尖峰和早退。它根据 motion/non-motion frame 实时切换 QoE 目标，用随机优化联合选码率与延迟风险。百万会话部署中冻结率降低 71%，交互时长增加 20%。
  - 相较对整段会话使用固定 QoE 权重或只根据带宽自适应码率，核心创新是把用户运动状态映射为逐帧可变效用函数，使传输决策与真实交互意图对齐。
  - 移动云渲染、Motion-Aware 码率控制、动态 QoE、大规模在线部署

- [Accelerating Distributed Graph Learning by Using Collaborative In-Network Multicast and Aggregation](https://www.usenix.org/conference/atc25/presentation/li-zhaoyi)
  - Zhaoyi Li, Central South University and Nanyang Technological University; Jiawei Huang, Yijun Li, and Jingling Liu, Central South University; Junxue Zhang, Hong Kong University of Science and Technology; Hui Li, Xiaojun Zhu, Shengwen Zhou, Jing Shao, Xiaojuan Lu, Qichen Su, and Jianxin Wang, Central South University; Chee Wei Tan, Nanyang Technological University; Yong Cui, Tsinghua University; Kai Chen, Hong Kong University of Science and Technology
  - SwitchGNN 优化分布式 GNN 每轮跨 worker 的一对多顶点特征广播与多对一聚合。P4 交换机先按边界顶点邻居数重排上传顺序，尽早发送扇出大的顶点以减少链路空闲和队列堵塞；再用多级图分区将边界顶点分成可独立批处理的 block，避免少数热点占满 switch aggregator。真实平台与 NS3 中训练时间最高缩短 74%。
  - 相较直接将所有图聚合卸载到有限 switch register/aggregator，核心创新是让 multicast 排序和 aggregation 分批共同感知图拓扑，在正确传播语义下协调链路与片上稀缺资源。
  - 分布式 GNN 训练、网内多播与聚合、P4 交换机、图感知分批

- [Opening Up Kernel-Bypass TCP Stacks](https://www.usenix.org/conference/atc25/presentation/awamoto)
  - Shinichi Awamoto and Michio Honda, University of Edinburgh
  - 该工作构建可复现环境，在多百 GbE 大块传输、小消息请求–响应等基本但差异显著的工作负载上，横向比较六种内核或 kernel-bypass TCP stack。实验表明代表性高性能栈往往只优化吞吐或低延迟中一类，难以在同一实现中兼得，且部署可用性与通用性仍不足；论文据此提出实用用户态网络栈的设计路径。
  - 相较各自论文在不同硬件、应用和指标上报告峰值，核心贡献是在共同基础负载上打开六个栈的实现“黑箱”，把峰值优势与通用性缺口放到同一可比较边界。
  - Kernel-Bypass TCP、网络栈横向评测、百 GbE、吞吐-延迟权衡

- [GPREEMPT: GPU Preemptive Scheduling Made General and Efficient](https://www.usenix.org/conference/atc25/presentation/fan)
  - Ruwen Fan and Tingxu Ren, Tsinghua University; Minhui Xie, Renmin University of China; Shiwei Gao, Jiwu Shu, and Youyou Lu, Tsinghua University
  - GPreempt 服务于延迟敏感与 best-effort GPU 任务同置，以 timeslice-based yield 让正在执行的 kernel 在安全点保存上下文后让出 GPU，因而不要求 kernel 幂等。为了不让上下文保存抵消预占收益，hint-based pre-preemption 在延迟任务的必需数据准备阶段就提前启动切换。它对非幂等 workload 仍通用，预占延迟可控制在 40 微秒内。
  - 相较通用但必须等待 kernel 结束的 wait-based 方案，以及低延迟但只能重置幂等 kernel 的方案，核心创新是将可保存的时间片让出与预占前移结合，同时取得通用性和微秒级响应。
  - GPU 预占调度、非幂等 Kernel、Timeslice Yield、SLA 隔离

- [μEFI: A Microkernel-Style UEFI with Isolation and Transparency](https://www.usenix.org/conference/atc25/presentation/chen-le)
  - Le Chen, Yiyang Wu, Jinyu Gu, Yubin Xia, and Haibo Chen, Shanghai Jiao Tong University
  - μEFI 把 UEFI driver/application 从高权限同地址空间退权到用户态 sandbox，按模块分配独立地址空间。Trampoline injection 在不改模块的情况下截获调用，protocol analysis 还原 UEFI 协议交互；seccomp-like capability filter 限制模块权限，自动输入校验拦截无效数据。复杂现有模块可透明运行，启动阶段开销仅 1.91%。
  - 相较仅依赖 Secure Boot 验证模块签名、加载后仍给予全权限，核心创新是把微内核式权限分离引入固件环境，并用 trampoline/协议分析保持旧 UEFI ABI 透明。
  - UEFI 隔离、固件微内核、权限削减、透明 Sandbox

- [PageFlex: Flexible and Efficient User-space Delegation of Linux Paging Policies with eBPF](https://www.usenix.org/conference/atc25/presentation/yelam)
  - Anil Yelam and Kan Wu, Google; Zhiyuan Guo, UC San Diego; Suli Yang, Google; Rajath Shashidhara, University of Washington; Wei Xu and Stanko Novaković, Google; Alex C. Snoeren, Google and UC San Diego; Kimberly Keeton, Google
  - PageFlex 让超大规模平台在不改应用的情况下，把冷页降级到压缩内存或 NVMe 的策略从 Linux 内核交给用户态。eBPF 程序低成本读取内核页状态与访问信息并返回 paging decision，而实际迁移仍沿用内核高效机制；同一应用的不同区域/阶段可装载不同策略。委托现有内核策略的慢化小于 1%，且可落地 Hyperbolic caching 和 Leap prefetching。
  - 相较将新 paging policy 写进内核的高部署成本，或 userfaultfd/库方案的频繁上下文切换与侵入性，核心创新是仅用 eBPF 外置“策略”而保留内核“机制”，并以区域/阶段作为专用化边界。
  - Linux 分页策略、eBPF 用户态委托、分层内存、区域/阶段专用化

- [ASTERINAS: A Linux ABI-Compatible, Rust-Based Framekernel OS with a Small and Sound TCB](https://www.usenix.org/conference/atc25/presentation/peng-yuke)
  - Yuke Peng, SUSTech; Hongliang Tian, Ant Group; Junyang Zhang and Ruihan Li, Peking University and Zhongguancun Laboratory; Chengjun Chen and Jianfeng Jiang, Ant Group; Jinyi Xian, SUSTech; Xiaolin Wang, Chenren Xu, Diyu Zhou, and Yingwei Luo, Peking University and Zhongguancun Laboratory; Shoumeng Yan, Ant Group; Yinqian Zhang, SUSTech
  - ASTERINAS 用 framekernel 架构在 Rust OS 内部建立权限分离：OSTD 将不可避免的 unsafe 硬件/底层边界收缩成小型且可论证的 TCB，其余内核用 safe Rust 实现。系统提供 Linux ABI 兼容层并支持 210 多个 system call，完整应用性能与 Linux 相当，而内存安全 TCB 仅约占代码库 14.0%。
  - 相较在内核大量散布 unsafe Rust、仅依靠 code review 守住边界的 Rust OS，核心创新是用 framekernel 在架构上强制内核内权限分离，使 TCB 的小型化与 soundness 可同时审计。
  - Rust 操作系统、Framekernel、Linux ABI 兼容、最小内存安全 TCB

- [Rex: Closing the language-verifier gap with safe and usable kernel extensions](https://www.usenix.org/conference/atc25/presentation/jia)
  - Jinghao Jia and Ruowen Qin, University of Illinois Urbana-Champaign; Milo Craun and Egor Lukiyanov, Virginia Tech; Ayush Bansal and Minh Phan, University of Illinois Urbana-Champaign; Michael V. Le, Hubertus Franke, and Hani Jamjoom, IBM; Tianyin Xu, University of Illinois Urbana-Champaign; Dan Williams, Virginia Tech
  - Rex 针对 eBPF 类内核扩展中“语言已保证安全，verifier 却无法证明”的 language–verifier gap。扩展使用 safe Rust 和内核 crate 提供的安全接口编写，内存/类型安全由语言承担；难以静态表达的异常处理、栈空间与终止性则由轻量语言外 runtime 约束，无需另做符号执行验证，同时保持 eBPF 级性能。
  - 相较内核 verifier 对每个程序重复做保守符号执行并误拒安全程序，核心创新是把可组合的安全证明前移到 Rust 类型/所有权合约，只用小 runtime 补足非局部性质。
  - 安全内核扩展、Rust 语言安全、Verifier Gap、轻量运行时

- [Barre: Empowering Simplified and Versatile Programmable Congestion Control in High-Speed AI Clusters](https://www.usenix.org/conference/atc25/presentation/peng-yajuan)
  - Yajuan Peng, Shanghai Key Laboratory for Intelligence Information Processing, Fudan University, China; Haoran Wei, Xiaolong Zhong, Junkai Huang, Haohan Xu, Zicheng Wang, Yang Bai, Zhuo Jiang, and Jianxi Ye, ByteDance; Xiaoliang Wang, /; Xiaoming Fu, Shanghai Key Laboratory for Intelligence Information Processing, Fudan University, China; Huichen Dai, ByteDance
  - Barre 面向 400 Gbps RoCEv2 AI/HPC 集群中突发训练流对拥塞反应、公平性和大规模参数调整的要求，只依赖商用 NIC/交换机与标准网络功能构建简化的可编程控制环，避免对复杂硬件 feature 和大量 workload-specific knob 的依赖。该方案已在最多支持一万 GPU 的生产集群运行一年以上，平均提高 AI 训练吞吐 9.6%，核心原理还可增强 DCQCN。
  - 相较依赖特殊遥测/队列硬件和繁重经验调参的新 CCA，核心创新是从商品 RoCE 现有反馈中抽取一组简单、可复用的原则，在可部署性下达到近似最优响应与公平性。
  - 400 Gbps RoCE、AI 集群拥塞控制、商品硬件可部署性、生产网络

- [FLB: Fine-grained Load Balancing for Lossless Datacenter Networks](https://www.usenix.org/conference/atc25/presentation/hu-jinbin)
  - Jinbin Hu, Central South University, Hong Kong University of Science and Technology, Changsha University of Science and Technology; Wenxue Li, Xiangzhou Liu, Junfeng Wang, and Bowen Liu, Hong Kong University of Science and Technology; Ping Yin, Inspur; Jianxin Wang and Jiawei Huang, Central South University; Kai Chen, Hong Kong University of Science and Technology
  - FLB 针对 RoCE+PFC 无损数据中心网络，发现在路径间频繁细粒度改道会把已拥塞流扩散到更多队列，反而放大 PFC head-of-line blocking。它在正常时用无阈值改道持续均衡链路，一旦拥塞则及时隔离问题流，避免 PAUSE 传染无关流。原型将 PFC PAUSE 率最多降低 96%，goodput 最高增加 45%，并对多种基线降低 18%–40% 平均 FCT。
  - 相较直接把有损 DCN 的 packet/flowlet rerouting 套到 PFC 网络，核心创新是根据 PFC 交互把“正常均衡”与“拥塞隔离”分为两个运行模式，避免精细改道制造新的 HoL。
  - 无损数据中心网络、PFC、细粒度负载均衡、拥塞流隔离

- [SNARY: A High-Performance and Generic SmartNIC-accelerated Retrieval System](https://www.usenix.org/conference/atc25/presentation/gan)
  - Qiaoyin Gan, Institute of Computing Technology, Chinese Academy of Sciences; Heng Pan, Computer Network Information Center, Chinese Academy of Sciences; Luyang Li, Kai Lv, and Hongtao Guan, Institute of Computing Technology, Chinese Academy of Sciences; Zhaohua Wang, Computer Network Information Center, Chinese Academy of Sciences; Zhenyu Li, Institute of Computing Technology, Chinese Academy of Sciences; Gaogang Xie, Computer Network Information Center, Chinese Academy of Sciences
  - SNARY 将大规模推荐的 candidate retrieval 卸载到商用 Xilinx SmartNIC，用 HBM 容纳并扫描百万级 corpus。系统分别设计数据并行 exact-search engine 与基于 LSH 的 fuzzy-search engine，再将扫描、Top-K 选择和输出变成连续流水。比现有硬件检索，exact search 延迟降低 20.91%–83.88%、SLO 内吞吐高 1.26–18.27 倍；fuzzy search 延迟降低 85.13%–87.40%、吞吐高 20.18–23.81 倍。
  - 相较只对精确匹配定制固定-function accelerator，核心创新是在同一 SmartNIC/HBM 数据路径中同时抽象 exact 和 LSH fuzzy search，并使 Top-K 成为可与扫描流式重叠的阶段。
  - SmartNIC 推荐检索、HBM Corpus Scan、LSH 模糊搜索、流水化 Top-K

- [Minos : A Lightweight and Dynamic Defense against Traffic Analysis in Programmable Data Planes](https://www.usenix.org/conference/atc25/presentation/wang-zihao)
  - Zihao Wang, Pengcheng Laboratory and Tsinghua Shenzhen International Graduate School; Qing Li, Guorui Xie, Dan Zhao, Kejun Li, and Zhuochen Fan, Pengcheng Laboratory; Lianbo Ma, Northeastern University; Yong Jiang, Pengcheng Laboratory and Tsinghua Shenzhen International Graduate School
  - Minos 在 Tofino1 可编程交换机上同时隐藏加密流量的身份和时序/长度特征。Proxy 模块压缩加密轮次以适配 match-action pipeline 并线速加密包头；Schedule 模块穿插多流包，在不真实发送 dummy 的部分场景模仿其效果；Morphing 模块再通过优先级 dummy queue 和 padding 处理剩余特征。对 Website/IoT Fingerprinting，攻击准确率压到 20% 以下，开销约为现有防御的十分之一。
  - 相较在端主机大量填充/延迟每条流，或使用固定模式而难跟随攻击变化，核心创新是把包头保护、跨流调度和 morphing 均映射为线速数据面原语，用流间穿插减少真实 dummy 代价。
  - 加密流量分析防御、P4/Tofino 数据面、Traffic Morphing、动态包调度

- [GeneralSparse: Bridging the Gap in SpMM for Pruned Large Language Model Inference on GPUs](https://www.usenix.org/conference/atc25/presentation/wang-yaoyu)
  - Yaoyu Wang, Xiao Guo, Junmin Xiao, De Chen, and Guangming Tan, SKLP, Institute of Computing Technology, CAS; and University of Chinese Academy of Sciences
  - GeneralSparse 面向裁剪 LLM 权重产生的多种结构化/非结构化稀疏模式，不为每种格式手写一个 SpMM kernel，而用 memory-access space 和 reduction space 抽象读取与归约。动态 box division 根据实际稀疏形态分工，分层 reduction 对齐 GPU warp/block 层级。在裁剪 LLM 与 SuiteSparse 矩阵上比 cuSPARSE 最高快 20.82 倍，端到端 LLM 推理最高快 2.33 倍。
  - 相较将 kernel 绑定某一 pruning pattern、稀疏率或存储格式，核心创新是把寻址和归约视为独立可组合空间，由输入形态自适应分块并映射到 GPU 层次。
  - 裁剪 LLM 推理、通用 SpMM、Memory/Reduction Space、GPU 分层归约

- [HyCache: Hybrid Caching for Accelerating DNN Input Preprocessing Pipelines](https://www.usenix.org/conference/atc25/presentation/jha)
  - Keshav Vinayak Jha, Independent Researcher; Shweta Pandey, Indian Institute of Science; Murali Annavaram, University of Southern California; Arkaprava Basu, Indian Institute of Science
  - HyCache 解决 GPU 训练变快后 CPU 数据读取与多阶段预处理成为主瓶颈的问题。它不仅缓存 pipeline 最终样本，而允许多个中间阶段的部分输出分别放入 DRAM 与存储；ILP 把各阶段重算时间、缓存大小和介质 I/O 作为约束，自动选择哪些样本/阶段应缓存在哪一层。多类输入 pipeline 原始吞吐提升 1.11–10.1 倍。
  - 相较只缓存某一固定处理阶段或要求人工划分 DRAM/磁盘的方案，核心创新是将多阶段、部分样本、双介质缓存统一建模为重算–I/O 取舍优化。
  - DNN 输入预处理、混合缓存、中间结果复用、ILP 缓存规划

- [The Koala Benchmarks for the Shell: Characterization and Implications](https://www.usenix.org/conference/atc25/presentation/lamprou)
  - Evangelos Lamprou and Ethan Williams, Brown University; Georgios Kaoukis, National Technical University of Athens; Zhuoxuan Zhang, Brown University; Michael Greenberg, Stevens Institute of Technology; Konstantinos Kallas, University of California, Los Angeles; Lukas Lazarek and Nikos Vasilakis, Brown University Awarded Best Paper!
  - KOALA 为 Unix/Linux shell 性能研究建立系统基准：从真实任务收集包含 POSIX shell 主要语言特性、GNU Coreutils 与第三方程序的脚本，同时提供小型到云规模的真实输入、特征分析和可复现工具。使用 KOALA 重新评估四个 shell 加速系统，暴露原有窄基准未显示的性能权衡，并检验其结论能否外推。
  - 相较为某一加速方法手选少量脚本和合成输入，核心贡献是同时覆盖程序语义、组件组合与输入规模的实地基准，使 shell 优化结论可横向比较。
  - Shell 系统基准、真实工作负载、可复现性、POSIX/GNU 程序组合

- [KVCache Cache in the Wild: Characterizing and Optimizing KVCache Cache at a Large Cloud Provider](https://www.usenix.org/conference/atc25/presentation/wang-jiahao)
  - Jiahao Wang, Jinbo Han, and Xingda Wei, Shanghai Jiao Tong University; Sijie Shen, Alibaba Group; Dingyan Zhang, Shanghai Jiao Tong University; Chenguang Fang, Alibaba Group; Rong Chen, Shanghai Jiao Tong University; Wenyuan Yu, Alibaba Group; Haibo Chen, Shanghai Jiao Tong University
  - 该工作分析大型云 LLM 服务商的真实 KVCache cache 轨迹，发现复用在请求间高度偏斜，单轮请求间复用与多轮会话同样重要；全局复用时间/概率差异大，但在具体 request category 内可预测，理想命中率所需总容量也并非无限。系统据此构造 workload-aware eviction，在容量受限时用类别化未来复用代替通用 LRU，提高真实轨迹服务性能。
  - 相较从合成 multi-turn/prefix workload 推导缓存策略，核心创新是首次用产线全量轨迹分解单轮、多轮与请求类别的复用分布，并将这些分布直接转为 eviction signal。
  - LLM KV Cache 工作负载表征、生产轨迹、类别感知淘汰、容量规划

- [LogCrisp: Fast Aggregated Analysis on Large-scale Compressed Logs by Enabling Two-Phase Pattern Extraction and Vectorized Queries](https://www.usenix.org/conference/atc25/presentation/wei)
  - Junyu Wei, Guangyan Zhang, and Junchao Chen, Tsinghua University; Qi Zhou, Alibaba Cloud
  - LogCrisp 让云平台能在近 7 TB 经模式编码的高压缩日志上直接做聚合分析。两阶段提取把 pattern 分成离线获得全局结构的 Sketch，以及在线为当前 query 细化过滤的 Specs；前缀/后缀向量查询再用 AVX SIMD 把数值编码上的全文条件改成 range/point query。分析延迟降低一个数量级，摄取快 3.8 倍而压缩率基本不变。
  - 相较用一套静态 pattern 同时承担压缩与查询过滤，核心创新是将“全局描述”和“查询特化”分开生成，并在压缩编码上直接做 SIMD 查询而不先解压。
  - 压缩日志分析、Sketch/Specs 模式提取、AVX 向量查询、全文聚合

- [HotRAP: Hot Record Retention and Promotion for LSM-trees with Tiered Storage](https://www.usenix.org/conference/atc25/presentation/qiu)
  - Jiansheng Qiu and Fangzhou Yuan, Tsinghua University; Mingyu Gao and Huanchen Zhang, Tsinghua University and Shanghai Qi Zhi Institute
  - HotRAP 在快慢存储混合的 RocksDB 中保留层次化写入路径，同时以单条 record 为粒度将慢层热数据提升到快层并在其仍热时留存。专用 on-disk LSM 记录 key hotness，两条 promotion path 分别处理可及时捕获的访问与后台整理，避免热数据长期被 compaction 固定在慢介质。读写平衡 YCSB 比次优系统最高快 1.6 倍，Twitter 轨迹最高快 1.5 倍。
  - 相较“上层全快/下层全慢”的 tiering 让热键滞留慢盘，或把快盘纯当 cache 导致 compaction 也在慢盘，核心创新是在保留快层写路径时引入细粒度热 record 升降级。
  - 分层存储 LSM-Tree、热记录提升、键级热度追踪、RocksDB

- [Mitigating Resource Usage Dependency in Sorting-based KV Stores on Hybrid Storage Devices via Operation Decoupling](https://www.usenix.org/conference/atc25/presentation/zhang-qingyang)
  - Qingyang Zhang and Yongkun Li, University of Science and Technology of China; Yubiao Pan, Huaqiao University; Haoting Tang, University of Science and Technology of China; Yinlong Xu, University of Science and Technology of China, and Anhui Provincial Key Laboratory of High Performance Computing
  - DecouKV 解决混合存储上 LSM flush/compaction 中 CPU 排序、I/O 读写与多操作争用相互捆绑、造成资源碎片和 write stall 的问题。它分离 index/data：索引用可合并 skip-list 结构执行 CPU-intensive merge，数据只追加并由独立 data append/flush 任务处理；弹性 level capacity 和参数化 queue scheduler 按资源状态组合任务。写密集负载中吞吐提高 2.3–4.9 倍，尾延迟降低 74.3%–91.4%。
  - 相较只给 compaction 排队或固定将数据分配到快慢盘，核心创新是从文件布局上分开 index merge 和 data movement，将原本不可分的排序操作变成可独立调度的 CPU/I/O 任务。
  - 混合存储 KV、LSM 操作解耦、索引-数据分离、Write Stall

- [SolFS: An Operation-Log Versioning File System for Hash-free Efficient Mobile Cloud Backup](https://www.usenix.org/conference/atc25/presentation/pan)
  - Riwei Pan, Department of Computer Science, City University of Hong Kong; Yu Liang, ETH Zurich; Lei Li and Hongchao Du, Department of Computer Science, City University of Hong Kong; Tei-Wei Kuo, Delta Electronics and National Taiwan University; Chun Jason Xue, Mohamed bin Zayed University of Artificial Intelligence
  - SolFS 为资源受限手机的多个云备份应用提供文件操作日志版本化。每个文件在 extent tree 中记录每次 write 的 offset/length，合并连续或重叠范围；持久化和版本机制为各 backup app 维护独立的上次同步点，compact log 与动态粒度控制额外存储。应用可直接获取改变区间而无需扫描全文件哈希，端侧/云侧计算平均减少超 90%，更新文件同步时间降低超 88.8%。
  - 相较 backup app 为 delta sync 周期性哈希整个大文件，核心创新是让文件系统在写入时产生可合并、可多客户端版本化的变更证据，以日志记录取代事后内容比对。
  - 移动云备份、操作日志版本文件系统、Hash-Free Delta Sync、Extent Merge

- [Z-LFS: A Zoned Namespace-tailored Log-structured File System for Commodity Small-zone ZNS SSDs](https://www.usenix.org/conference/atc25/presentation/hwang)
  - Inhwi Hwang, Seoul National University; Sangjin Lee, Chung-Ang University; Sunggon Kim, Seoul National University of Science and Technology; Hyeonsang Eom, Seoul National University; Yongseok Son, Chung-Ang University
  - Z-LFS 针对商品 small-zone ZNS SSD 重新设计 F2FS 类日志文件系统：利用 LFS metadata 更新特征把元数据也改成 append-only，避免与 zone 顺序写语义冲突；根据 workload temperature 投机管理 log stream，提高同时活跃的小 zone 利用率；conflict-aware allocation 再将可能在 SSD 内部争用资源的 stream 分开。在真实商用 ZNS 盘上比 F2FS 最高快 33.44 倍，比现有 small-zone 接口快 3.5 倍。
  - 相较为大 zone 假设设计的 ZNS LFS 或通过通用适配层隐藏 zone，核心创新是把元数据、热度 stream 与设备内部冲突都显式纳入 small-zone 空间/时间分配。
  - ZNS SSD 文件系统、Small-Zone LFS、Append-Only Metadata、冲突感知 Zone 分配

- [CLONE: Customizing LLMs for Efficient Latency-Aware Inference at the Edge](https://www.usenix.org/conference/atc25/presentation/tian)
  - Chunlin Tian, Xinpeng Qin, Kahou Tam, Li Li, Zijian Wang, Yuanzhe Zhao, Minglei Zhang, and Chengzhong Xu, University of Macau
  - CLONE 面向长时开机和中等算力的商用边缘设备，在实时延迟、电量/功耗与 LLM 生成质量之间做动态取舍。它在模型级按当前约束定制计算，在系统级联动 runtime 与能耗控制，并将这些操作与可扩展 28 nm 专用加速器协同设计。在两个现货边缘平台上，推理最高加速 11.92 倍、能耗最高降低 7.36 倍，同时保持生成质量。
  - 相较对通用压缩模型和现有 edge accelerator 分开调优，核心创新是模型算法、运行时能源控制与专用硬件的跨层共设计，以运行时 latency/energy 目标选实际执行点。
  - 边缘 LLM 推理、算法-硬件协同、延迟/能耗自适应、28 nm 加速器

- [Weaver: Efficient Multi-LLM Serving with Attention Offloading](https://www.usenix.org/conference/atc25/presentation/gao)
  - Shiwei Gao, Qing Wang, Shaoxun Zeng, Youyou Lu, and Jiwu Shu, Tsinghua University
  - Weaver 服务于“少数热 LLM+大量冷 LLM”的生产流量：将热模型的 attention operator 穿插卸载到正在运行冷模型的 GPU，用其未被完全占用的显存/计算而无需新建完整 model-parallel instance。GPU-driven control flow 使新 attention 可越过硬件队列中待执行的大 kernel，operator splitting 则切小冷模型 kernel 降低 HoL blocking。真实轨迹上热模型吞吐最高增加 77%且 TPOT 不恶化，冷模型仅增 3–5 ms。
  - 相较为冷热模型预留独立 GPU 或以完整模型并行复用导致高通信，核心创新是以 operator 为单位把热模型负载编织到冷模型正在执行的 GPU，并将调度决策下沉到 GPU。
  - 多 LLM Serving、Attention Offloading、GPU-Driven 控制流、冷热模型编织

- [Torpor: GPU-Enabled Serverless Computing for Low-Latency, Resource-Efficient Inference](https://www.usenix.org/conference/atc25/presentation/yu)
  - Minchen Yu, The Chinese University of Hong Kong, Shenzhen; and Hong Kong University of Science and Technology; Ao Wang, Alibaba Group; Dong Chen, Haoxuan Yu, Xiaonan Luo, Zhuohao Li, and Wei Wang, Hong Kong University of Science and Technology; Ruichuan Chen, Nokia Bell Labs; Dapeng Nie, Haoran Yang, and Yu Ding, Alibaba Group
  - Torpor 让 serverless worker 上四块 GPU 同时服务数百个推理函数：模型平时保留在主存，请求到达才 late-bind 到 GPU 并交换权重。异步 API 重定向、共享 GPU runtime、分段模型执行与细致显存管理共同隐藏 swap；interference-aware scheduler 通过高速 GPU 互连将请求放到仍能满足各函数 SLO 的设备。生产试点中用户与平台 GPU 供给成本分别降低 70% 和 65%，延迟接近独占常驻。
  - 相较每个函数长驻一份 GPU 模型或等完整加载后才执行，核心创新是将请求–GPU 绑定推迟到运行时，并用可流水的模型 swap 与 SLO 感知放置消化动态性。
  - GPU Serverless 推理、Late Binding、模型交换、干扰感知 SLO 调度

- [Toppings: CPU-Assisted, Rank-Aware Adapter Serving for LLM Inference](https://www.usenix.org/conference/atc25/presentation/li-suyi-toppings)
  - Suyi Li, Hanfeng Lu, and Tianyuan Wu, Hong Kong University of Science and Technology; Minchen Yu, The Chinese University of Hong Kong, Shenzhen; Qizhen Weng, TeleAI, China Telecom; Xusheng Chen and Yizhou Shan, Huawei Cloud; Binhang Yuan and Wei Wang, Hong Kong University of Science and Technology
  - Toppings 服务于共享一个 base LLM 的多 LoRA adapter：base 常驻 GPU，adapter 按请求从主存加载。在 adapter DMA 期间，CPU 先计算 prefill 的轻量 LoRA 增量，加载完后在精确同步点切换到 GPU，从而既不阻塞新请求 TTFT，也不中断 continuous batching 中已在解码的请求。加载流水与 rank-aware scheduler 还根据 LoRA rank 选择组批顺序；延迟最高改善 1.7 倍，SLO 达标率最高 99%。
  - 相较 adapter 到达后暂停整个 GPU batch 等待加载，核心创新是以 CPU prefill 作为加载窗口的过渡执行路径，再用 rank 显式表达不同 adapter 的计算成本。
  - LoRA Adapter Serving、CPU/GPU 协同 Prefill、Rank-Aware 调度、Adapter 加载隐藏

- [QFactory: Accelerating Quantized Large Language Model Serving with Qtile Graphs](https://www.usenix.org/conference/atc25/presentation/zhang-qihao)
  - Qihao Zhang, Mingshu Zhai, Rui Sun, and Jidong Zhai, Tsinghua University
  - QFactory 把 LLM 量化权重和临时反量化不再当作 eager operator 序列，而定义 Qtile 表示一块带精度/编码语义的量化 tensor，将计算转为 QGraph。编译器先在图层做等价 Qtile 转换，把反量化与后续计算的组合方式纳入搜索，再在 operator 层为每个 Qtile 选数据加载/排程。量化 kernel 平均快 1.66 倍，接入现有 serving 后端到端生成快 1.23 倍。
  - 相较为每种 quantization format 手写固定 dequantize+GEMM kernel，核心创新是把量化 tile 提升为编译 IR，使图级等价变换与 tile 级内存调度能在同一搜索空间协同。
  - 量化 LLM 编译、Qtile/QGraph、在线反量化、图-算子联合调度

- [PluS: Highly Efficient and Expandable ML Compiler with Pluggable Graph Schedules](https://www.usenix.org/conference/atc25/presentation/wu-ruofan)
  - Ruofan Wu, Renmin University of China; Zhen Zheng, Microsoft; Feng Zhang, Renmin University of China; Chuanjie Liu, Microsoft; Zaifeng Pan, Renmin University of China; Jidong Zhai, Tsinghua University; Xiaoyong Du, Renmin University of China
  - PluS 处理 ML compiler 难以及时吸收 FlashAttention 类新 subgraph 优化，而 template compiler 又对模型小变体过于脆弱的问题。它将原本内嵌在 compiler pass 中的 graph rewrite 解耦，让专家用轻量 loop-centric 抽象描述可插拔 graph schedule，并维护可演进 pattern warehouse；compiler 自动识别并生成匹配 subgraph。在常用 ML 模型上比 rule-based embedded compiler 最高快 4.04 倍。
  - 相较为每个优化把 pattern/rewrite 硬编码到编译器内部，核心创新是将专家 subgraph implementation 与通用 graph compiler 通过 loop-centric schedule 合约连接，保留性能又允许模式变化。
  - ML 编译器、可插拔图调度、Loop-Centric 抽象、Subgraph Pattern Warehouse

- [Obscura: Concealing Recomputation Overhead in Training of Large Language Models with Bubble-filling Pipeline Transformation](https://www.usenix.org/conference/atc25/presentation/huang-yuzhou)
  - Yuzhou Huang and Yapeng Jiang, Sun Yat-sen University; Zicong Hong, Hong Kong University of Science and Technology; Wuhui Chen, Sun Yat-sen University; Bin Wang and Weixi Zhu, Huawei Technologies; Yue Yu, Peng Cheng Laboratory; Zibin Zheng, Sun Yat-sen University
  - Obscura 针对 LLM pipeline parallelism 早期 stage 激活占用较高、必须用 recomputation 换内存而增加计算的问题。它改写 pipeline 时间表，把重算填入 backward 之后本会空闲的 bubble；同时把 activation swapping 放入统一执行时模型，在给定显存约束下选重算/换出组合，再调整分区平衡新时间表的 stage。Llama-2/GPT-3 训练吞吐比常用重算基线最高提升 1.33 倍。
  - 相较把 recomputation 当作不可避免的额外前向计算，核心创新是通过 pipeline transformation 将它重新定位到可遮蔽空隙，并联合搜索 swapping 与 stage partition。
  - LLM Pipeline Training、重算遮蔽、Bubble Filling、激活换出联合优化

- [PPipe: Efficient Video Analytics Serving on Heterogeneous GPU Clusters via Pool-Based Pipeline Parallelism](https://www.usenix.org/conference/atc25/presentation/kong)
  - Z. Jonny Kong, Qiang Xu, and Y. Charlie Hu, Purdue University
  - PPipe 将训练中常用的 pipeline parallelism 应用到有延迟 SLO 的视频分析推理，利用不同 CNN layer 在新旧 GPU 上的相对速度差异：许多 layer 在低端 GPU 上延迟接近高端卡，因而可将它们放入分层设备池。MILP control plane 选择分层和实例数，data plane 以资源预留的 adaptive batching 守住延迟。18 个 CNN 上低端 GPU 利用率提高 41.1%–65.5%，整体 serving 吞吐提高 32.2%–75.1%。
  - 相较把异构 GPU 整卡分配给完整模型或只在同构训练中做 pipeline，核心创新是用 layer–GPU 性能对齐建立分层设备池，并将全局分区与请求级自适应组批解耦。
  - 视频分析 Serving、异构 GPU 集群、Pool-Based Pipeline、SLO 感知组批

- [Voltrix: Sparse Matrix-Matrix Multiplication on Tensor Cores with Asynchronous and Balanced Kernel Optimization](https://www.usenix.org/conference/atc25/presentation/xia)
  - Yaqi Xia and Weihu Wang, Wuhan University; Donglin Yang, Nvidia Corporation; Xiaobo Zhou, University of Macau; Dazhao Cheng, Wuhan University
  - Voltrix-SpMM 让稀疏矩阵的不规则读取与 Tensor Core 的稠密 tile 计算更好对齐。数据路径用 bit-wise 压缩格式读稀疏输入、bulk copy 读稠密矩阵，并以 warp-specialized producer–consumer 将异步加载与 MMA 重叠；持久 kernel 用两阶段分区同时平衡 input work 与 output reduction/I/O。CUDA 12.6 实现比 TC-GNN 和 DTC-SpMM 平均快 36.5 倍和 1.8 倍，比 CUDA-core RoDe 快 1.7 倍。
  - 相较只用稠密填充把稀疏 block 塞入 Tensor Core，核心创新是联合设计压缩读取、warp 职责分离和输入/输出双向均衡，同时消除供数不足和负载偏斜。
  - Tensor Core SpMM、异步数据流水线、Warp 生产者-消费者、双向负载均衡

- [NetKeeper: Enhancing Network Resilience with Autonomous Network Configuration Update on Traffic Patterns and Anomalies](https://www.usenix.org/conference/atc25/presentation/wan)
  - Zhaoyang Wan, Rongxin Han, Haifeng Sun, Qi Qi, Zirui Zhuang, and Bo He, State Key Laboratory of Networking and Switching Technology, Beijing University of Posts and Telecommunications; Liang Zhang, Huawei Technologies Co., Ltd; Jianxin Liao and Jingyu Wang, State Key Laboratory of Networking and Switching Technology, Beijing University of Posts and Telecommunications
  - NetKeeper 把运维人员的自然语言意图和管理系统产生的 anomaly log 组成多模态网络意图，经 northbound/southbound interface 翻译为可执行配置目标。一个按配置参数类型分工的传统 multi-agent RL controller 观测流量模式与异常，在满足 forwarding policy 时更新参数以提高韧性。动态网络中平均策略一致性 99.6%，性能提升 5.3%，traffic shift 减少 8.7%。
  - 相较人工把语言意图/异常逐次转成静态配置，核心创新是打通意图接口、异常状态与配置参数化 controller；这里的 multi-agent 是传统强化学习策略，不属于 LLM Agent 四分类。
  - 自主网络配置、多模态意图、传统多智能体强化学习、异常感知韧性

- [GREYHOUND: Hunting Fail-Slows in Hybrid-Parallel Training at Scale](https://www.usenix.org/conference/atc25/presentation/wu-tianyuan)
  - Tianyuan Wu and Wei Wang, Hong Kong University of Science and Technology; Yinghao Yu, Siran Yang, and Wenchao Wu, Alibaba Group; Qinkai Duan, Hong Kong University of Science and Technology; Guodong Yang, Jiamang Wang, Lin Qu, and Liping Zhang, Alibaba Group
  - GREYHOUND 从一万多 GPU 共享生产集群表征 hybrid-parallel training fail-slow，发现计算争用、设备退化或网络拥塞可使某 GPU/链路在亚分钟到近十小时内间歇变慢，大作业平均被拖慢 1.34 倍。系统从并行迭代各层的计算/集合时序快速定位慢 GPU 或通信链路，并用多层缓解机制在不停作业时绕行或隔离。线上检测准确率超 99%，256 张 H800 上吞吐提升 1.58 倍。
  - 相较人工观察后将 fail-slow 一律当 fail-stop checkpoint/restart，核心创新是从混合并行的结构性时序比较分离计算与网络根因，并按影响层级选择在线缓解而非全作业重启。
  - 大规模训练 Fail-Slow、GPU/链路定位、多层在线缓解、生产可观测性

- [Crash Consistency in Block-Level Caching Systems: An Open CAS Case Study](https://www.usenix.org/conference/atc25/presentation/duan-shaohua)
  - Shaohua Duan, Washington State University; Youmin Chen, Shanghai Jiao Tong University
  - 该工作对持久内存作块级 cache 的 Open CAS 做系统崩溃一致性实验，在不同 write ordering、flush 和故障时点检查 cache 与 backing store 恢复后的内容。结果表明 Open CAS 的持久缓存层不总能维持 crash consistency，且部分文件系统可靠性 feature 经 cache 重排/合并后不再成立。论文以反例揭示端到端持久语义不能由文件系统或 cache 单独保证。
  - 相较只测 cache 吞吐/延迟或假设下层持久就自动保留上层顺序，核心贡献是将系统性 crash injection 用到块 cache，并把缓存序列与文件系统可靠性机制的兼容性作为共同设计对象。
  - 块级持久缓存、崩溃一致性、Open CAS、端到端可靠性测试

- [FiDe: Reliable and Fast Crash Failure Detection to Boost Datacenter Coordination](https://www.usenix.org/conference/atc25/presentation/rovelli)
  - Davide Rovelli, Università della Svizzera Italiana and SAP SE; Pavel Chuprikov, Télécom Paris and Institut Polytechnique de Paris; Philipp Berdesinski, turba; Ali Pahlevan, SAP SE; Patrick Jahnke, turba; Patrick Eugster, Università della Svizzera Italiana
  - FiDe 从网络与端主机争用会使 heartbeat RTT 尾部不可预测这一根因出发，重新构建稳定的端到端 process interaction 路径，使数据中心远程进程崩溃可在 30 微秒内高可信报告，比现有最佳方案快 7.2 倍。基于可信的最坏检测界，作者又设计两个 FiDe-aware consensus protocol，接入 KV store 和同步服务后吞吐最高提升 2.23 倍、延迟降到 0.46 倍。
  - 相较继续改良自适应 timeout 以容忍抢占抖动，核心创新是先把 failure detector 的通信路径做成可界定的稳定原语，再让上层协调协议直接使用该时间界优化正常路径。
  - 微秒级故障检测、稳定端到端交互、数据中心共识、协调服务

- [LEOCraft: Towards Designing Performant LEO Networks](https://www.usenix.org/conference/atc25/presentation/basak)
  - Suvam Basak and Amitangshu Pal, Indian Institute of Technology Kanpur; Debopam Bhattacherjee, Microsoft Research India
  - LEOCraft 是面向数百到数万颗低轨卫星的星座设计框架，让研究者可视化并评估轨道壳层、卫星数量、星间链路和地面站布局对端到端性能的影响。它从数千个已评估 constellation 中抽取领域知识，作为 integrated optimization 的搜索引导，设计新星座比通用黑箱优化快约 5 倍。框架可扩展到 8.3 万颗卫星、多 shell 和 1000 个地面站。
  - 相较以单一星座仿真器做手工参数 sweep 或完全黑箱搜索，核心创新是将大量设计评估中的 LEO 领域规律编入优化器，并在超大多壳层规模上保持可视化与可评估性。
  - LEO 星座设计、轨道/拓扑协同优化、超大规模卫星网络、设计框架

- [Emulating Space Computing Networks with RHONE](https://www.usenix.org/conference/atc25/presentation/wang-liying)
  - Liying Wang, Peking University; Qing Li, Beijing University of Posts and Telecommunications; Yuhan Zhou and Zhaofeng Luo, Peking University; Donghao Zhang and Shangguang Wang, Beijing University of Posts and Telecommunications; Xuanzhe Liu and Chenren Xu, Peking University; and Key Laboratory of High Confidence Software Technologies, Ministry of Education (PKU)
  - RHONE 在普通服务器上仿真同时受功耗、热、轨道连通性与 COTS 芯片性能影响的空间计算网络。离线阶段用真实卫星 telemetry 和 hardware-in-the-loop chip mirroring 构建功耗、热、轨道、网络与计算模型；在线阶段以 container 执行应用，COTS aligner 和 network aligner 持续将资源/链路限制对齐到当前星座状态。单机可模拟 700 星，功耗/计算误差小于 5%，热误差 1.3–2.5°C。
  - 相较只回放网络时延或用统一 CPU quota 近似卫星的平台，核心创新是在同一双阶段环境中联动单星的功耗/热/芯片状态与星座级动态拓扑。
  - 空间计算网络仿真、Hardware-in-the-Loop、功耗/热忠实度、星座动态

- [Roaming Free in the VR World with MP2](https://www.usenix.org/conference/atc25/presentation/xu)
  - Yifei Xu, University of California, Los Angeles; Xumiao Zhang, University of Michigan and Alibaba Cloud; Yuning Chen, University of California, Merced; Pan Hu, Uber Technologies, Inc.; Xuan Zeng, Zhilong Zheng, Xianshang Lin, and Yanmei Liu, Alibaba Cloud; Songwu Lu, University of California, Los Angeles; Z. Morley Mao, University of Michigan; Wan Du, University of California, Merced; Dennis Cai and Ennan Zhai, Alibaba Cloud; Yunfei Ma, Uber Technologies, Inc.
  - MP2 为多用户自由行走 VR 统一协调 Wi-Fi AP 切换、多链路分配和视频码率。中心 controller 持续收集每个头显的无线/应用跨层状态，建模所有用户移动和竞争后联合优化 handover、AP load 和 bitrate；高效 pruning/partitioning 使全局决策能跟上实时变化。真实测试、大规模仿真与用户研究中，尾延迟改善 35 倍，码率提高 1.56 倍，QoE 提高 1.86 倍。
  - 相较每个 VR 用户仅用本地链路状态独立选 AP/码率、彼此产生负载振荡，核心创新是用跨用户的全局模型在一次决策中同时解 handover、链路和应用码率。
  - 自由行走 VR、多用户无线协调、跨层 QoE 优化、AP Handover

- [STORM: a Multipath QUIC Scheduler for Quick Streaming Media Transport under Unstable Mobile Networks](https://www.usenix.org/conference/atc25/presentation/hu-liekun)
  - Liekun Hu, East China Normal University; Changlong Li, East China Normal University, Jianghuai Advance Technology Center, and MoE Engineering Research Center of Hardware/Software Co-Design Technology and Application
  - STORM 面向手机同时使用 Wi-Fi/5G 的流媒体 Multipath QUIC，测量表明尾延迟主要来自不稳定的最后一跳无线，且可靠数据的重传会阻塞不可靠但更时敏的帧数据。调度器直接获取手机无线模块状态，按数据可靠性/时效性分类选路，避免重传队列压住关键流。真机上尾包延迟降低 98.2%，不稳定网络下帧率提高 1.95 倍。
  - 相较只按 RTT/吞吐选路、将所有 QUIC 数据视为同一可靠字节流的多路径调度，核心创新是同时感知最后一跳与应用数据语义，隔离重传对时敏媒体的 HoL 影响。
  - Multipath QUIC、Wi-Fi/5G 协同、可靠/不可靠流分类、流媒体尾延迟

- [Internet Connection Splitting: What’s Old is New Again](https://www.usenix.org/conference/atc25/presentation/yuan)
  - Gina Yuan, Thea Rossman, and Keith Winstein, Stanford University
  - 该测量工作重新审视在端点间插入 performance-enhancing proxy、将一条长距离 TCP 拆成多段的价值。通过仿真多类丢包/长 RTT 路径，它发现 2016 版 BBR 受益不大，更新 BBR 反而在部分情况比传统 loss-based CCA 更需要 split。研究还显示声称使用相同 CCA 的不同 QUIC implementation 行为差异巨大，也与 Linux TCP 不可直接等同。
  - 相较由“BBR 不靠丢包、QUIC 不能透明拆分仍表现好”直接得出 PEP 已过时，核心贡献是用跨版本/跨实现对照证明新拥塞控制仍可从路径分段受益，且实现差异会压过协议标签。
  - TCP 连接拆分、Performance-Enhancing Proxy、BBR 版本差异、QUIC 实现测量

- [WIC: Hiding Producer-Consumer Synchronization Delays with Warp-Level Interrupt-based GPU Communications](https://www.usenix.org/conference/atc25/presentation/zhang-jiajian)
  - Jiajian Zhang, Xi'an Jiaotong-Liverpool University and University of Liverpool; Fangyu Wu, Xi'an Jiaotong-Liverpool University; Hai Jiang, Beijing University of Posts and Telecommunications; Qiufeng Wang, Xi'an Jiaotong-Liverpool University; Genlang Chen and Chaoyi Pang, NingboTech University
  - WIC 解决跨 GPU producer–consumer 通信中 consumer warp 提前开始 polling，持续占用计算资源却等不到数据的问题。它向 GPU 通信引入 warp-level interrupt：识别反复轮询的 warp 后先挂起，让 scheduler 将 execution slot 交给其他计算，数据就绪事件再精确唤醒。这使同步等待与有用计算重叠，在多种通信模式应用中比传统 polling 平均快 1.13 倍。
  - 相较使用 GPU thread/warp 忙等 flag 或用粗粒度 kernel 间同步，核心创新是把中断下沉到 warp，使仅等待数据的最小执行单位可被暂停并及时复用资源。
  - GPU 间通信、Warp-Level Interrupt、Producer–Consumer 同步、Polling 消除

- [Primus: Unified Training System for Large-Scale Deep Learning Recommendation Models](https://www.usenix.org/conference/atc25/presentation/shan-jixi)
  - Jixi Shan, ByteDance Inc.; Xiuqi Huang, Zhejiang University; Yang Guo, Hongyue Mao, Ho-Pang Hsu, Hang Cheng, Can Wang, and Jun Song, ByteDance Inc.; Rui Shi, Bytedance Inc.; Xiaofeng Gao, Shanghai Jiao Tong University; Jingwei Xu, Shiru Ren, Jiaxiao Zheng, Hua Huang, Lele Yu, and Peng Xu, ByteDance Inc.; Guihai Chen, Shanghai Jiao Tong University
  - Primus 是字节跳动运行五年的大规模 DLRM 训练平台，统一三个长期割裂的维度：资源层对接多调度系统，在资源池间支持横向/纵向动态扩缩；数据层用三层定义与 task graph 编排 batch/stream 多源样本；训练层精细控制参数更新与混合数据优先级，同时保证模型时效性。动态扩缩使集群成本降 17.1%、作业 CPU 利用率从 50% 到 80%，数据任务生成快 23 倍，并为四个 DLRM 带来 0.4%–2.4% 广告收入增长。
  - 相较分别建设资源 scheduler、离线/实时数据 pipeline 和训练 engine，核心创新是用一套训练抽象联动资源弹性、数据编排和 batch–stream 混合更新，并以多年生产成果验证。
  - 工业级 DLRM 训练、资源池动态扩缩、Batch/Stream 数据编排、混合训练范式

- [Chitu: Avoiding Unnecessary Fallback in Byzantine Consensus](https://www.usenix.org/conference/atc25/presentation/huang-rongji)
  - Rongji Huang, Xiangzhe Wang, Xiaofeng Yan, and Lei Fan, Shanghai Jiao Tong University; Guangtao Xue and Shengyun Liu, Shanghai Jiao Tong University and Shanghai Key Laboratory of Trusted Data Circulation, Governance and Web3
  - Chitu 重新拆解异步 BFT consensus：节点平时先仅通过消息交换尝试在提案上直接会合，只有正确节点意见真正分歧才启动 random coin 或 leader election 的 fallback。具体异步 DAG 协议在最好情况下即使存在坏节点/网络异步也可用四个 message delay 提交，最坏情况期望复杂度仍为 O(1)。EC2 实验显著降低了始终将 leader 或随机化放在必经路径的 DAG 协议延迟。
  - 相较部分同步协议每轮预选单 leader，或异步协议每轮必用 random coin，核心创新是将它们从常规路径降为“意见分歧时才必需”的恢复机制。
  - 异步 BFT 共识、DAG 协议、条件式 Fallback、低延迟提交

- [Fast Distributed Transactions for RDMA-based Disaggregated Memory](https://www.usenix.org/conference/atc25/presentation/lu)
  - Haodi Lu, Haikun Liu, Yujian Zhang, Zhuohui Duan, Xiaofei Liao, Hai Jin, and Yu Zhang, Huazhong University of Science and Technology
  - HDTX 在计算与被动内存节点分离的 RDMA 系统中执行跨分片事务。Fast Commit Protocol 合并传统事务处理的多个网络阶段以减少 RTT；RDMA-aware offloading 通过组合单边/两边原语将计算推向数据所在端，减少 compute–memory 之间搬运；去中心优先级锁为紧急事务提供可控等待。相比 FaRM/FORD，延迟最高降低 88.3%/72.1%，吞吐最高提升 2.08 倍/84.7%。
  - 相较直接将经典 2PC/锁协议搬到 RDMA 且每阶段独立往返，核心创新是联合压缩 commit 阶段、编排 RDMA 操作与分布锁优先级，以整条事务路径为优化单位。
  - RDMA 解耦内存、分布式事务、Fast Commit、去中心优先级锁

- [Cuckoo for Clients: Disaggregated Cuckoo Hashing](https://www.usenix.org/conference/atc25/presentation/grant)
  - Stewart Grant and Alex C. Snoeren, UC San Diego
  - RCuckoo 让多个 client 只通过单边 RDMA 协同访问被动 memory server 上的 lock-based KV table。Cuckoo hashing 使小 value read 只用一个 RTT，update/delete 只需两个；locality-enhanced dependent hashing 可调整同一 key 候选槽位的预期距离，从而在插入搬运、I/O amplification 与最大 fill factor 间选取。Lease-based locking 又能在每秒数百 client failure 时自动回收。小值读领先现有 RDMA KV，高争用 YCSB 中吞吐最高高 7 倍。
  - 相较为了单 RTT 读而将数据复制到相距很远的 hash 位置，或依赖 memory-node CPU 解冲突，核心创新是通过可调候选位置局部性使 cuckoo relocation 适合 RDMA，并以 client lease 守住被动内存一致性。
  - 解耦 KV Store、单边 RDMA、Cuckoo Hashing、Lease 故障恢复

- [LITESHIELD: Secure Containers via Lightweight, Composable Userspace μKernel Services](https://www.usenix.org/conference/atc25/presentation/manakkal)
  - Kaesi Manakkal, The University of Texas at Arlington; Nathan Daughety and Marcus Pendleton, Air Force Research Laboratory (AFRL); Hui Lu, The University of Texas at Arlington
  - LITESHIELD 将容器中传统 guest kernel 的网络、文件系统等功能拆为可组合的用户态微内核服务，应用通过低延迟共享内存 IPC 调用它们。POSIX-compatible runtime 细粒度截获旧程序 syscall，多数请求在用户态完成，最终暴露给 host 的接口只剩 22 个 syscall。因此在不引入 hypervisor/硬件虚拟化复杂度时得到接近 VM 的攻击面隔离，性能与传统容器相当。
  - 相较直接向 host 内核暴露大量 syscall 的容器，或为强隔离加载完整 guest kernel/VM，核心创新是在用户态拆分并组合微内核系统服务，用最小 host ABI 同时保持 POSIX 兼容。
  - 安全容器、用户态微内核服务、共享内存 IPC、Host Syscall 收缩

- [Accelerating Nested Virtualization with HyperTurtle](https://www.usenix.org/conference/atc25/presentation/zur)
  - Ori Ben Zur and Jakob Krebs, Technion - Israel Institute of Technology; Shai Aviram Bergman, Huawei Zurich Research Center; Mark Silberstein, Technion - Israel Institute of Technology Awarded Best Paper!
  - HyperTurtle 加速 nested virtualization 中频繁在 L2 guest、virtualized hypervisor 和 bare-metal hypervisor 间发生的 world switch。它将虚拟 hypervisor 关键路径中的局部操作封装成 eBPF program，安全下沉到裸机 hypervisor 上下文执行，避免整个控制流跨层往返，又保留上层对 nested VM 的管理。该方法可用于内存、网络和 profiling，EPT fault 处理快 5 倍，Kata container 启动最高快 27%。
  - 相较修改虚拟化基础设施整个路径或放宽 nested hypervisor 权限，核心创新是用 eBPF 作为可验证的跨虚拟层函数卸载格式，只下沉对 world switch 最敏感的片段。
  - 嵌套虚拟化、eBPF Hypervisor Offload、World Switch 削减、EPT Fault

- [Efficient Performance-Aware GPU Sharing with Compatibility and Isolation through Kernel Space Interception](https://www.usenix.org/conference/atc25/presentation/zhang-shulai)
  - Shulai Zhang, Ao Xu, Quan Chen, Han Zhao, and Weihao Cui, Shanghai Jiao Tong University; Zhen Wang, Yan Li, and Limin Xiao, Lenovo; Minyi Guo, Shanghai Jiao Tong University
  - KRYPTON 在内核 GPU driver 层截获 command buffer，为每个应用暴露独立 virtual GPU，从而不依赖某一 CUDA runtime，也不让一个用户态 sharing daemon 的崩溃/越界影响其他租户。运行时不使用固定 partition，而根据任务性能需求联合做空间额度与时间复用，在给出性能保证时回收碎片。实验中比现有方案少需 32.1% GPU，同时支持更广 runtime 并强化 fault/security isolation。
  - 相较在用户态 CUDA API 层复用、容易被绕过或因共享进程故障连锁崩溃，核心创新是将兼容性与隔离边界下沉到 command buffer 内核路径，再在该强边界上做空时调度。
  - GPU 内核虚拟化、Command Buffer 截获、空时复用、多租户隔离

- [AnchorNet: Bridging Live and Collaborative Streaming with a Unified Architecture](https://www.usenix.org/conference/atc25/presentation/meng)
  - Tong Meng, Wei Zhang, Dong Chen, Zhen Wang, Quanqing Li, Changqing Yan, Wei Yang, Chao Yuan, Le Zhang, Jianxin Kuang, and Jianlin Xu, ByteDance
  - AnchorNet 为大型直播应用将单主播 live streaming 与多主播 collaborative streaming 合并为一条从 host broadcaster 到 viewer 的统一 stream path，使主播在不结束会话、不重建观众链路的情况下切换单人/连麦模式。由于多路音频时钟与编码边界不同，系统另做 audio stream splicing 来隐藏切换处的缺口和杂音。生产部署将切换期 rebuffering 降低超 60%，用户参与最高增加 3.83%。
  - 相较为单主播和连麦分别维护两套传输拓扑、切模式时全链路重建，核心创新是设计模式不变的统一 stream path，只在源组合和音频缝合层处理转换。
  - 直播/连麦统一架构、连续流路径、音频流拼接、生产 QoE

- [Katz: Efficient Workflow Serving for Diffusion Models with Many Adapters](https://www.usenix.org/conference/atc25/presentation/li-suyi-katz)
  - Suyi Li, Lingyun Yang, Xiaoxiao Jiang, Hanfeng Lu, and Dakai An, Hong Kong University of Science and Technology; Zhipeng Di, Weiyi Lu, Jiawei Chen, Kan Liu, Yinghao Yu, Tao Lan, Guodong Yang, Lin Qu, and Liping Zhang, Alibaba Group; Wei Wang, Hong Kong University of Science and Technology
  - Katz 优化生产级文生图 workflow 中 base diffusion model 同时挂载多个 ControlNet 和 LoRA 的执行路径。对计算密集的 ControlNet，ControlNet-as-a-Service 将其从 base model 关键路径剥离到可独立扩展的专用 GPU 服务，使结果可缓存、共享和并行；对计算轻但加载慢的 LoRA，有界异步加载最多与前 K 步 base execution 重叠，保证图像质量不变；latent parallelism 再加速 base model。SDXL/H800 上延迟最高降低 7.8 倍，吞吐提高 1.7 倍。
  - 相较将 base、ControlNet 和 LoRA 按一个完整 replica 共伸缩、每个 workflow 重复运行相同 adapter，核心创新是按 adapter 的计算/加载特性重画服务边界，分别使用独立服务和有界重叠。
  - Diffusion Workflow Serving、ControlNet-as-a-Service、LoRA 有界异步加载、Latent Parallelism

- [PopFetcher: Towards Accelerated Mixture-of-Experts Training Via Popularity Based Expert-Wise Prefetch](https://www.usenix.org/conference/atc25/presentation/zhang-junyi)
  - Junyi Zhang, Chuanhu Ma, Xiong Wang, and Yuntao Nie, Huazhong University of Science and Technology; Yuqing Li, Wuhan University; Yuedong Xu, Fudan University; Xiaofei Liao, Huazhong University of Science and Technology; Bo Li, Hong Kong University of Science and Technology; Hai Jin, Huazhong University of Science and Technology
  - PopFetcher 观察 MoE 训练中 token 选 expert 具有偏斜与跨层相关性，用轻量 sliding window 预测下一层热门 expert，在当前非 MoE 计算阶段利用空闲网络预取这些 expert，从而减少后续 All-to-All 必须 dispatch 的 token/权重。系统对端到端训练时间建模，用定制 pruning 求全局最优预取集，同时恢复通信/计算均衡；backward 还给 All-to-All 流优先级以减少阻塞。集群实验将训练时间降低 15%–94.5%。
  - 相较每层等 router 决策后才在前向关键路径做全量 All-to-All，核心创新是用 expert popularity 预测在空闲链路提前搬运，并在全局时间模型中同时考虑预取带来的通信和计算重平衡。
  - MoE 训练、Expert Popularity 预测、跨层预取、All-to-All 隐藏

- [HypeReca: Distributed Heterogeneous In-Memory Embedding Database for Training Recommender Models](https://www.usenix.org/conference/atc25/presentation/he-jiaao)
  - Jiaao He, Shengqi Chen, Kezhao Huang, and Jidong Zhai, Tsinghua University
  - HypeReca 将超大 DLRM embedding table 抽象为分布式异构 in-memory KV database，统一使用 GPU 和 CPU 内存而不是将 host memory 当作被动溢出层。它利用 DNN 训练成批访问特征，在去中心 index table 上建立数据管理流水，以 contention-avoiding exchange schedule 排 All-to-All；两级并行保证 embedding 更新一致性，性能模型只复制少量高频 vector 削减跨节点通信。32 GPU 上端到端比 HugeCTR、TorchRec 和 TFDE 快 2.16–16.8 倍。
  - 相较将巨大 embedding 简单 offload 到每个节点 host 并在多节点发生大量稀疏 All-to-All，核心创新是以数据库接口统一索引、批量交换、一致更新与热点复制，让 CPU/GPU 容量可跨节点扩展。
  - DLRM Embedding Database、CPU/GPU 异构内存、去中心索引、热点向量复制

- [CrossPipe: Towards Optimal Pipeline Schedules for Cross-Datacenter Training](https://www.usenix.org/conference/atc25/presentation/chen-tiancheng)
  - Tiancheng Chen, Ales Kubicek, Langwen Huang, and Torsten Hoefler, ETH Zurich
  - CrossPipe 面向单个数据中心已放不下的 LLM 训练，显式建模跨地理数据中心的高 RTT 和低带宽，在同一 schedule 中考虑 pipeline parallel stage 与 data-parallel communication 的可重叠机会。框架可用 solver 得到最优 schedule，也可用快速 greedy 近似，底层 execution engine 将时间表与具体通信操作解耦。同显存限制下比传统 pipeline 缩短最高 33.6% 训练时间，放宽内存后仍能接近理想无延迟 schedule。
  - 相较先生成单机房 pipeline schedule、再被动承受 WAN 停顿，核心创新是把 PP 阶段顺序与 DP 通信重叠在 WAN 成本模型中联合求解，并以可编程 execution engine 实现不同 schedule。
  - 跨数据中心 LLM 训练、WAN-Aware Pipeline、PP/DP 通信重叠、最优/贪心调度

- [Unveiling Compiler Faults via Attribute-Guided Compilation Space Exploration](https://www.usenix.org/conference/atc25/presentation/wu-jiangchang)
  - Jiangchang Wu, Yibiao Yang, Maolin Sun, and Yuming Zhou, State Key Laboratory for Novel Software Technology, Nanjing University
  - ATLAS 扩展 compiler fuzzing 的 compilation space：不再只对整个程序切换全局 optimization flag，而向具体 function、variable 等程序元素策略性插入 `always_inline` 类 C/C++ attribute，迫使编译器对不同元素应用特定 constraint 或 pass，从而组合出以往未触达的局部优化路径。对 GCC/LLVM 比不用 attribute 的基线有更高 coverage 与缺陷发现能力，共发现 73 个独立 bug，其中 58 个已确认或修复。
  - 相较将一组 compiler option 均匀施加给所有程序元素，核心创新是以 attribute 作为元素级 compilation control input，使测试能在同一源程序中探索异质 pass/约束组合。
  - 编译器测试、Attribute-Guided Fuzzing、GCC/LLVM、编译空间探索

- [Understanding and Detecting Fail-Slow Hardware Failure Bugs in Cloud Systems](https://www.usenix.org/conference/atc25/presentation/dong)
  - Gen Dong and Yu Hua, Huazhong University of Science and Technology; Yongle Zhang, Purdue University; Zhangyu Chen and Menglei Chen, Huazhong University of Science and Technology
  - 该研究先分析 ZooKeeper、Kafka、HDFS 等云系统的 48 个真实 fail-slow hardware bug，发现慢硬件不是简单降低吞吐，而会在软件同步与 timeout 逻辑中触发故障，且必须以精确 I/O/设备操作为粒度注入才能复现。Sieve 静态定位受同步或 timeout 保护的 I/O，在候选点前插 hook，再用 grouping 和 context-sensitive injection 减少搜索。三个系统中发现 6 个未知 bug，2 个已确认。
  - 相较以整块磁盘/整张 NIC 级降速或随机 delay 做粗粒度注错，核心创新是从真实 bug 中得出“同步/timeout-sensitive I/O+细粒度退化”的触发模型，用程序上下文定向注入。
  - Fail-Slow 硬件故障、云系统注错、同步/Timeout 分析、上下文敏感测试

- [Converos: Practical Model Checking for Verifying Rust OS Kernel Concurrency](https://www.usenix.org/conference/atc25/presentation/tang)
  - Ruize Tang, State Key Laboratory for Novel Software Technology, Nanjing University; Minghua Wang, Ant Group; Xudong Sun, University of Illinois Urbana-Champaign; Lin Huang, Ant Group; Yu Huang and Xiaoxing Ma, State Key Laboratory for Novel Software Technology, Nanjing University
  - CONVEROS 对 Rust/Linux-ABI 内核 ASTERINAS 的 lock、scheduler 和关键 thread-safety component 做可持续的 model checking。多层、多粒度 specification 允许从局部原语到组合模块逐层写 PlusCal，避免为整个内核构造单一巨型模型；incremental conformance checking 自动对照 Rust 代码与演进规格。12 个并发模块在四人月内完成验证，发现 20 个会引起 data race、deadlock、livelock 或 panic 的 bug，spec/code 比为 0.3–2.3。
  - 相较要求专家一次建立与大量实现细节紧耦合的形式模型，核心创新是把并发规格分层/分粒度并将代码一致性检查增量化，使 model checking 能跟随实际 Rust kernel 开发。
  - Rust 内核并发验证、PlusCal Model Checking、多层规格、增量 Conformance

- [Bin2Wrong: a Unified Fuzzing Framework for Uncovering Semantic Errors in Binary-to-C Decompilers](https://www.usenix.org/conference/atc25/presentation/yang-zao)
  - Zao Yang and Stefan Nagy, University of Utah
  - BIN2WRONG 将影响 binary-to-C decompilation 正确性的四个维度——源构造、compiler、optimization level 和 executable format——统一编进一个 testcase 并联合变异，通过原 binary 与反编译后 C 再执行的语义差异判定错误。这使测试既能深入单维度，也能触发以往工具未覆盖的多因素组合。在 7 个开源/商业 decompiler 上代码覆盖与 binary diversity 均超过 Cornucopia/DecFuzzer，发现 48 个新 bug，30 个已确认，并促使 Binary Ninja 重设计。
  - 相较只变异源程序或只切换编译选项的 decompiler fuzzer，核心创新是将生成 binary 的全部因素组成可交叉变异的单一语义测试单元，并保持工具无关。
  - 反编译器 Fuzzing、语义错误、多维 Binary 生成、跨工具测试

- [HEC: Equivalence Verification Checking for Code Transformation via Equality Saturation](https://www.usenix.org/conference/atc25/presentation/yin)
  - Jiaqi Yin and Zhan Song, University of Maryland, College Park; Nicolas Bohm Agostini and Antonino Tumeo, Pacific Northwest National Laboratory; Cunxi Yu, University of Maryland, College Park
  - HEC 验证 HLS/编译器的 loop unrolling、tiling、fusion 等 source-to-source transformation 是否保持语义。MLIR frontend 将控制流和数据路径转为 e-graph，静态 rewrite 注入已知等式，动态 rewrite 在具体程序上扩展可等价表达，通过 equality saturation 判断变换前后能否收敛到共同等价类。它在 40 分钟处理超 10 万行 MLIR，并在 `mlir-opt` 中找到 unroll 边界多执行和 fusion 导致 read-after-write 语义改变的两个严重错误。
  - 相较仅用随机测试对比输出或为单类 loop pass 写专用证明器，核心创新是在 MLIR 上以 e-graph 统一表示控制流/数据流变换，通过动静结合的等式饱和扩大可验证范围。
  - 编译变换等价性、E-Graph、MLIR、Equality Saturation

- [Para-ksm: Parallelized Memory Deduplication with Data Streaming Accelerator](https://www.usenix.org/conference/atc25/presentation/ji)
  - Houxiang Ji, University of Illinois Urbana-Champaign; Minho Kim and Seonmu Oh, Daegu Gyeongbuk Institute of Science and Technology; Daehoon Kim, Yonsei University; Nam Sung Kim, University of Illinois Urbana-Champaign
  - Para-ksm 使用 Intel Data Streaming Accelerator 卸载 Linux KSM 中最耗 CPU 的页比较和 checksum，避免内存去重对同机应用产生过大 datacenter tax。朴素 DSA-ksm 虽能减少干扰，但每页一次经 on-chip PCIe 卸载延迟高，反而让去重吞吐下降；Para-ksm 重组 KSM scanner，利用 DSA batch 一次对多页执行相同函数。相比 KSM，每个 CPU cycle 去重的内存量增加 31%–50%，对同置应用的慢化降至 1.3–2.7 倍。
  - 相较用 DSA 一对一替换 CPU 函数，核心创新是围绕加速器的固定提交延迟重写 KSM 数据路径，把原有单页 scanner 变成多页批处理以摊销 on-chip PCIe 成本。
  - KSM 内存去重、Intel DSA、批量页比较/Checksum、Datacenter Tax

- [DSA-2LM: A CPU-Free Tiered Memory Architecture with Intel DSA](https://www.usenix.org/conference/atc25/presentation/liu-ruili)
  - Ruili Liu, Tsinghua University and University of Electronic Science and Technology of China; Teng Ma, Alibaba Group; Mingxing Zhang, Jialiang Huang, and Yingdi Shan, Tsinghua University; Zheng Liu, Alibaba Group; Lingfeng Xiang, Zhen Lin, Hui Lu, and Jia Rao, The University of Texas at Arlington; Kang Chen and Yongwei Wu, Tsinghua University
  - DSA-2LM 把 Intel DSA 集成到 DRAM–Persistent/CXL memory 分层系统的 page migration，用专用引擎代替 CPU 拷贝。为避免 Linux 细粒度、同步迁移无法发挥 DSA 最高约 4 倍单核带宽的能力，系统构造 fast-migration workflow，依据当前页批次与带宽调整并发 data path 和 DSA queue/configuration，使放置策略可快速落地。在真实应用上比 MEMTIS、TPP 和 NOMAD 分别提升 20%、30% 和 16%。
  - 相较仅将 `memcpy` 换成 DSA 而保留原有单页串行流程，核心创新是让迁移 workflow、数据路径并发度和加速器参数共同适应页迁移粒度与当前负载。
  - 分层内存、Intel DSA 页迁移、CPU-Free Data Movement、CXL/Persistent Memory

- [Turbocharge ANNS on Real Processing-in-Memory by Enabling Fine-Grained Per-PIM-Core Scheduling](https://www.usenix.org/conference/atc25/presentation/wu-puqing)
  - Puqing Wu, Minhui Xie, Enrui Zhao, Dafang Zhang, and Jing Wang, Renmin University of China; Xiao Liang and Kai Ren, Kuaishou; Yunpeng Chai, Renmin University of China
  - PIMANN 针对 ANNS 近 1:1 的计算/访存比使用 UPMEM PIM，但商品 PIM 与 CPU 共用 DDR bus，无法同时访问，现有 batch 调度因而在 CPU 搬数时让全部 PIM 空闲，且 batch 内各核 query 难度不均。作者发现每个 PIM core 尚有用于启动 kernel 的独立控制接口，将其改作细粒度 DDR arbitration；persistent kernel 消除批间空档，per-PU dispatch 按实时负载逐核发 query。比 CPU/GPU ANNS 系统吞吐提高 2.4–10.4 倍。
  - 相较把全部 PIM core 作为一个批次同步切换 CPU/PIM 访存，核心创新是复用未公开细节化的 per-core control interface，将总线仲裁和 query 分发粒度从 batch 下沉到 PIM core。
  - PIM ANNS、UPMEM、Per-Core DDR 仲裁、Persistent PIM Kernel

- [SwCC: Software-Programmable and Per-Packet Congestion Control in RDMA Engine](https://www.usenix.org/conference/atc25/presentation/huang-hongjing)
  - Hongjing Huang, Jie Zhang, Xuzheng Chen, Ziyu Song, Jiajun Qin, and Zeke Wang, Zhejiang University
  - SwCC 在 RDMA NIC 内集成 RISC-V core，使拥塞算法可用 C 实现并对每个 packet 执行，以应对 400/800 Gbps 与突发 ML 流中快速变化的反馈。为了不让可编程 core 拖慢数据面，它联合设计 RISC-V memory subsystem、RDMA engine pipeline 和 core/NIC resource 交互，并向开发者暴露支持 rate/window/credit-based CCA 的 API。U280 原型与 ConnectX-5 同样达到 3.1 微秒 control-loop RTT，512B 包即可跑满 100 Gbps。
  - 相较 NIC 固化 CCA 无法跟随应用，或把反馈交给 host CPU 拉长控制环，核心创新是将通用软件编程下沉到 RDMA engine 内的 packet fast path，同时为其专门构造不阻塞的存储与交互路径。
  - 可编程 RDMA NIC、Per-Packet 拥塞控制、On-NIC RISC-V、微秒控制环

- [DRack: A CXL-Disaggregated Rack Architecture to Boost Inter-Rack Communication](https://www.usenix.org/conference/atc25/presentation/zhang-xu)
  - Xu Zhang and Ke Liu, SKLP, Institute of Computing Technology, CAS; and University of Chinese Academy of Sciences; Yuan Hui and Xiaolong Zheng, Huawei; Yisong Chang, SKLP, Institute of Computing Technology, CAS; and University of Chinese Academy of Sciences; Yizhou Shan, Huawei Cloud; Guanghui Zhang, Shandong University; Ke Zhang, Yungang Bao, Mingyu Chen, and Chenxi Wang, SKLP, Institute of Computing Technology, CAS; and University of Chinese Academy of Sciences
  - DRack 针对数据密集应用跨 rack 流量被源 host NIC 和 core network oversubscription 卡住，而同 rack 其他 host NIC 大量空闲的不匹配。它用 CXL 把 rack 内所有 NIC 从主机解耦成共享池，使任一 host 可使用多出口；由于单 host PCIe/内存带宽又会限制 NIC 池，它同时解耦多个 memory device，让 NIC 并行读写内存池，CPU 仍以 load/store 访问数据。DNN 训练与图处理中跨 rack 通信阶段平均缩短 37.3%。
  - 相较 ToR-centric rack 将每块 NIC/内存静态绑定到 host，核心创新是同时池化 NIC 与内存：前者打破出口绑定，后者避免新的单主机数据通道成为瓶颈。
  - CXL Rack 解耦、共享 NIC 池、内存池、跨 Rack 通信

- [ShieldReduce: Fine-Grained Shielded Data Reduction](https://www.usenix.org/conference/atc25/presentation/yang-jingyuan)
  - Jingyuan Yang, Jun Wu, Ruilin Wu, and Jingwei Li, University of Electronic Science and Technology of China; Patrick P. C. Lee, The Chinese University of Hong Kong; Xiong Li and Xiaosong Zhang, University of Electronic Science and Technology of China
  - ShieldReduce 在不可信备份服务器上以 Intel SGX TEE 同时执行 deduplication、delta compression 和 local compression，避免加密后的数据只能做粗粒度去重。因为 delta 需读 base chunk 且 enclave I/O 昂贵，系统将 inline 和 offline compression 结合成双向 delta：写入时选择便于局部访问的参照，后台可反向重编码以持续保留 base/target 物理邻近。多种 backup workload 下比无双向 delta 的 TEE 基线显著加速，存储节省接近明文精细压缩。
  - 相较只在密文上做 convergent dedup 或在 enclave 中随机读大量 base chunk，核心创新是用双向 delta 和 inline/offline 协同主动维护参照块物理局部性，降低 TEE 边界 I/O。
  - TEE 加密备份、去重+差分+局部压缩、双向 Delta、SGX I/O 局部性

- [MemoryTrap: Booby Trapping Memory to Counter Memory Disclosure Attacks with Hardware Support](https://www.usenix.org/conference/atc25/presentation/luo)
  - Chenke Luo, Wuhan University and Tulane University; Jiang Ming, Tulane University; Dongpeng Xu, University of New Hampshire; Guojun Peng and Jianming Fu, Wuhan University
  - MemoryTrap 防御 JIT-ROP 攻击者反复读取 executable memory 来在 ASLR 进程中实时搜索 gadget。编译阶段在代码空间中撒布不可读的“booby trap”区域，运行时用 Intel Memory Protection Keys 高效实施权限；直接线性/探测式泄露一旦跨入 trap 立即被检测和终止。它支持应用、shared library 和动态 JIT code，能阻断真实 JIT-ROP 及合成 code-inference 攻击，宏/微基准开销可忽略。
  - 相较 execute-only memory 仍可被 code-inference 绕过，或 destructive code read 不允许 von Neumann 式代码/数据混合，核心创新是保留混合布局，只在攻击扫描必经路径上随机布置硬件保护陷阱。
  - JIT-ROP 防御、内存泄露检测、Intel MPK、代码空间陷阱

- [Separate but Together: Integrating Remote Attestation into TLS](https://www.usenix.org/conference/atc25/presentation/weinhold)
  - Carsten Weinhold, Barkhausen Institut; Muhammad Usama Sardar, TU Dresden; Ionuț Mihalcea and Yogesh Deshpande, Arm; Hannes Tschofenig, University of Applied Sciences Bonn-Rhein-Sieg; Yaron Sheffer, Intuit; Thomas Fossati, Linaro; Michael Roitzsch, Barkhausen Institut
  - 该协议将 TEE remote attestation 与常规 certificate-based TLS 结合，同时证明远程端点的 Web/service identity 和安全通道确实终止在特定软件/硬件 TEE 内。设计将两种 assurance 作为 additive 且独立验证的信任轨道：证书生态可在不理解 attestation 时照常运作，attestation 失败也不被证书身份所掩盖，两者可独立部署、升级和失效。
  - 相较将 attestation evidence 塞进 certificate 或用 attested key 取代 Web PKI，导致两种信任互相依赖，核心创新是将身份与运行环境证明建模为可叠加、可各自失败的 TLS assurance。
  - Confidential Computing、Remote Attestation、TLS 协议组合、独立信任保证

- [DDLumos: Understanding and Detecting Atomic DDL Bugs in DBMSs](https://www.usenix.org/conference/atc25/presentation/wu-zhiyong)
  - Zhiyong Wu, Tsinghua University; Jie Liang, Beihang University; Jingzhou Fu, Wenqian Deng, and Yu Jiang, Tsinghua University
  - 该工作研究 PostgreSQL、MySQL 等 DBMS 中 schema change 应全成功或全回滚的 Atomic DDL，分析 207 个真实 bug 后发现主要后果为错误结果、恢复后数据不一致和服务不可用，根因常是并发 DDL 间 metadata conflict。DDLUMOS 根据元数据冲突合成并发 DDL/故障用例，再从执行前后 schema/data 结构构图检查原子性与恢复一致性。六个流行 DBMS 上发现 73 个未知 bug，14 个已修复。
  - 相较随机组合 DDL 或仅在无故障串行环境校验返回值，核心创新是用大规模 bug study 提取 metadata conflict 作为生成导航，并以图化恢复后状态作为跨 DBMS oracle。
  - DBMS Atomic DDL、Metadata Conflict、崩溃恢复测试、图一致性分析

- [SpaceExit: Enabling Efficient Adaptive Computing in Space with Early Exits](https://www.usenix.org/conference/atc25/presentation/liu-jiacheng)
  - Jiacheng Liu, Shanghai Jiao Tong University and The Chinese University of Hong Kong; Xiaozhi Zhu, Tongqiao Xu, Xiaofeng Hou, and Chao Li, Shanghai Jiao Tong University
  - SpaceExit 面向 LEO 地球观测卫星在下行带宽受限时就地筛选高分辨率影像，但不再对所有影像用固定网络深度。Geospatial-contextual detector 同时使用视觉语义与地理上下文判断每张图所需 early exit；复杂度 scheduler 将图像切 tile，按内容难度和星上异构设备能力分配推理；resource-adaptive controller 在功耗/热等条件变化时保持安全运行。多种星上硬件中性能提升 5.2%–37.6%。
  - 相较全部影像使用一个静态 early-exit 阈值或固定设备映射，核心创新是将地理语义、tile 级计算难度和实时星上资源串联成三层自适应控制。
  - 星上地球观测、Early Exit、地理上下文推理、功耗/热自适应调度

- [XRT: An Accelerator-Aware Runtime for Accelerated Chip Multiprocessors](https://www.usenix.org/conference/atc25/presentation/patel)
  - Neel Patel and Mohammad Alian, Cornell University
  - XRT 面向集成多个 on-chip accelerator 的 many-core chip multiprocessor，处理微秒级数据中心服务在 CPU core 与加速器间频繁切换、共享设备和队列而使通用 runtime 反而慢于纯 CPU 的问题。它把请求 critical path、accelerator availability 与尾延迟 SLO 统一纳入调度，在多核与多加速器之间安排异步调用/后续执行，避免局部吞吐改善造成端到端排队。代表性服务中 SLO 内吞吐最高比未优化 runtime 高 3.2 倍，且从不慢于全 CPU。
  - 相较把 on-chip accelerator 当作普通异步设备、仅根据本次函数快慢决定卸载，核心创新是使 runtime 显式感知多加速器争用和请求级 SLO，用端到端服务目标驱动卸载。
  - On-Chip Accelerator Runtime、Many-Core CMP、加速器共享、Throughput-under-SLO

- [DShuffle: DPU-Optimized Shuffle Framework for Large-scale Data Processing](https://www.usenix.org/conference/atc25/presentation/ding)
  - Chen Ding, Sicen Li, and Kai Lu, Wuhan National Laboratory for Optoelectronics, Huazhong University of Science and Technology; Ting Yao, Daohui Wang, and Huatao Wu, Huawei Cloud; Jiguang Wan, Zhihu Tan, and Changsheng Xie, Wuhan National Laboratory for Optoelectronics, Huazhong University of Science and Technology
  - DShuffle 将 Spark 类大数据处理中高 CPU 与 I/O 占用的 shuffle 数据路径卸载到 DPU。它将 shuffle 拆成 serialization、preprocessing 和 I/O 三阶段，按 DPU 的嵌入式核、高并发内存访问单元和存储/网络 I/O 能力流水布置。serialization 在专用内存单元上并行，中间数据从 DPU 直接落盘，避免在 host memory 与 NIC/DPU 间往返拷贝。真实 DPU 与工业 Spark 实验同时提高 host CPU/I/O 效率并缩短任务完成时间。
  - 相较只将 shuffle 网络发送卸载、但 serialization 与落盘仍经 host CPU/多次拷贝，核心创新是按 DPU 异构部件重分三阶段路径，使序列化、预处理和存储 I/O 在设备上端到端重叠。
  - DPU Shuffle、Spark 数据处理、异构流水线、零冗余拷贝

- [Accelerating Model Training on Ascend Chips: An Industrial System for Profiling, Analysis and Optimization](https://www.usenix.org/conference/atc25/presentation/zhou)
  - Yuhang Zhou, Zibo Wang, Zhibin Wang, Ruyi Zhang, Chen Tian, Xiaoliang Wang, Wanchun Dou, and Guihai Chen, Nanjing University; Bingqiang Wang, Yonghong Tian, Yan Zhang, and Hui Wang, Peng Cheng Laboratory; Fuchun Wei, Boquan Sun, Jingyi Zhang, Bin She, Teng Su, Yifan Yao, Chunsheng Li, Ziyang Zhang, and Yaoyuan Wang, Huawei; Bin Zhou, Shandong University; Guyue Liu, Peking University
  - Hermes 总结三年、135 个 Huawei Ascend 训练优化案例，为长时间训练中偶发波动、多因素瓶颈定位和优化方案选择建立一体系统。轻量 profiler 用有选择的事件/时间线采集长期运行证据；层次化 analysis 从作业、通信/计算、operator 下钻根因；advisor 将诊断映射为可实施优化建议。PanGu-α、MobileNetV1 和 MoE 分别加速 3.05 倍、1.91 倍和 1.19 倍。
  - 相较只在问题复现后手工打开高开销全量 profiler，或给出无根因的低层 counter，核心贡献是把长期轻量采集、跨层诊断和经验驱动的优化建议连成可生产使用的闭环工具链。
  - Ascend 训练优化、轻量 Profiling、分层瓶颈分析、优化顾问

- [CAFault: Enhance Fault Injection Technique in Practical Distributed Systems via Abundant Fault-Dependent Configurations.](https://www.usenix.org/conference/atc25/presentation/chen-yuanliang)
  - Yuanliang Chen, Fuchen Ma, Yuanhang Zhou, Zhen Yan, and Yu Jiang, Tsinghua University
  - CAFault 针对分布式系统注错通常只在默认配置下执行，而真实部署中 timeout、replication 等参数会改变 fault-handling path 的问题。它先从代码/执行中构建 fault-dependent model，只保留能影响某故障处理逻辑的配置，削减 fault×configuration 组合空间；在每个高质量配置内再以 fault-handling coverage 引导 fuzzing 深入异常路径。在 HDFS、ZooKeeper、MySQL-Cluster 和 IPFS 上比 CrashFuzz/Mallory/Chronos 多覆盖 31.5%/29.3%/81.5% 容错逻辑，发现 16 个严重未知 bug。
  - 相较把 configuration 固定为测试背景、只搜索 fault sequence，核心创新是根据故障处理依赖选择与其相关的参数组合，再在该配置下以容错代码覆盖导航注错。
  - 配置感知注错、分布式系统 Fuzzing、Fault-Dependent Model、容错路径覆盖

- [Revealing Floating-Point Accumulation Orders in Software/Hardware Implementations](https://www.usenix.org/conference/atc25/presentation/xie)
  - Peichen Xie, Yanjie Gao, Yang Wang, and Jilong Xue, Microsoft Research
  - FPRev 在不查看源码/硬件实现的情况下，推断 summation、matrix multiplication 等浮点累加的实际运算顺序。它构造一组数值经精心设计的输入，使不同加法树/分块顺序因非结合性产生可区分的输出，再用测得数值缩小候选累加图。工具展示 NumPy/PyTorch 在 CPU、GPU 及 Tensor Core 上的实际顺序，时间复杂度低于基本穷举方案，可用于跨系统复现和实现等价性检查。
  - 相较依赖文档/反汇编或穷举所有加法树，核心创新是将浮点非结合性变成一个主动探测通道，用少量鉴别性输入从黑箱输出恢复并行累加结构。
  - 浮点可复现性、累加顺序推断、黑箱数值测试、CPU/GPU/Tensor Core

- [Inferring Likely Counting-related Atomicity Program Properties for Persistent Memory](https://www.usenix.org/conference/atc25/presentation/zhang-yunmo)
  - Yunmo Zhang and Junqiao Qiu, City University of Hong Kong; Hong Xu, The Chinese University of Hong Kong; Chun Jason Xue, MBZUAI
  - 该工作为 persistent-memory program 自动推断 container-like array 与其 logical-size/count variable 之间的原子性属性，例如崩溃后不能看到 count 已增加但新 element 未持久的状态。它定义 counting-correlation invariant，用 symbolic range analysis 提取数组写入区间与 count 更新行为，编码为 SMT 约束，将满足不变式的候选关系输出为 likely atomicity specification。将推断属性接入 PM bug detector 后发现 14 个原子性 bug，其中 11 个是新问题。
  - 相较属性推断主要关注 persist-order relation、需人工标注数组与 size 的共同原子更新，核心创新是将这类计数相关行为建模为 range+SMT 可推断的程序不变式。
  - 持久内存原子性、Counting Correlation、符号范围分析、SMT 属性推断

- [Optimizing Input Minimization in Kernel Fuzzing](https://www.usenix.org/conference/atc25/presentation/guo)
  - Hui Guo, East China Normal University; Hao Sun, ETH Zurich; Shan Huang, Ting Su, and Geguang Pu, East China Normal University; Shaohua Li, The Chinese University of Hong Kong
  - SyzMini 优化 coverage-guided kernel fuzzing 中为保留新覆盖而将 seed 缩短的 input minimization：该阶段在 Syzkaller 中可消耗超过一半执行资源。Influence-guided call removal 优先尝试删除对目标 coverage 影响小的 syscall，type-informed argument simplification 根据参数类型直接生成高概率保留路径的简化值，两者都减少为验证 coverage 反复执行 kernel 的次数。minimization 成本降低 60.7%，branch coverage 提高 12.5%，独立 bug 数高 1.7–2 倍，并在最新内核发现 13 个新 bug。
  - 相较对每个 call/参数都用 trial deletion 与完整动态重放验证，核心创新是用输入内部的影响关系和 syscall 类型信息对 minimization 操作排序/定向，将节省的执行预算返还 fuzzing。
  - Linux Kernel Fuzzing、Seed Minimization、影响引导删除、类型感知参数简化

- [IRHash: Efficient Multi-Language Compiler Caching by IR-Level Hashing](https://www.usenix.org/conference/atc25/presentation/landsberg)
  - Tobias Landsberg and Johannes Grunenberg, Leibniz Universität Hannover; Christian Dietrich, Technische Universität Braunschweig; Daniel Lohmann, Leibniz Universität Hannover
  - IRHash 将 compiler cache lookup 从预处理源码/token/AST 下沉到 LLVM IR，对已消除语言表面差异的中间程序求 hash，因此源级变化若未改变优化后 IR，后端编译可直接命中；任何有 LLVM backend 的语言都可使用，不限于 C-family。在 C、C++、Fortran、Haskell 的 16 个开源项目历史上评估，C 项目平均 build time 减少 19%，超过 Ccache 的 10% 与 cHash 的 16%，并增加多语言覆盖。
  - 相较为尽早查 cache 只 hash source/token，因无语义差异的表面变化也 miss，核心创新是接受较晚查询的前端成本，换取 IR 级更精确的等价命中与跨语言复用。
  - 编译缓存、LLVM IR Hashing、多语言 Build、语义级 Cache Hit

- [On-Demand Container Partitioning for Distributed ML](https://www.usenix.org/conference/atc25/presentation/bartolomeo)
  - Giovanni Bartolomeo, Navidreza Asadi, Wolfgang Kellerer, and Jorg Ott, Technical University of Munich; Nitinder Mohan, TU Delft
  - 2DFS 重设计分布式 ML 部署镜像：传统 OCI layered filesystem 的纵向 layer 使模型局部重训、partition 或更新时必须重建/下载大 layer；两维文件系统除版本 layer 外，还把 model component 作为独立分区轴，允许任意组件独立更新、缓存和按需组装。作者实现 builder、registry 和 cache hierarchy，保持 OCI 兼容并接入现有流程。14 个模型上 build 最高快 56 倍，cache 效率高 25 倍，按需 image partition 开销可忽略。
  - 相较容器只能沿 layer 轴粗粒度复用，核心创新是增加正交的 model-component 维度，让模型分割/更新不再改写无关容器层，同时以完整 OCI 生态实现该抽象。
  - 分布式 ML 部署、二维容器文件系统、模型组件分区、OCI 兼容

- [PathWeaver: A High-Throughput Multi-GPU System for Graph-Based Approximate Nearest Neighbor Search](https://www.usenix.org/conference/atc25/presentation/kim)
  - Sukjin Kim, Seongyeon Park, Si Ung Noh, Junguk Hong, Taehee Kwon, Hunseong Lim, and Jinho Lee, Seoul National University
  - PathWeaver 针对大数据 graph-based ANNS 的多 GPU 扩展，避免每卡在自己分区中独立从头搜索并最后合并。Pipelined path extension 通过 GPU-to-GPU 传递已发现的路径/候选，让各分区连续扩展同一搜索而减少重复 iteration；ghost staging 从代表性数据为难 query 预置更好起点；direction-guided selection 按当前路径方向提前过滤无关点，减少访存和距离计算。95% recall 时对现有多 GPU 框架几何平均加速 3.24 倍，最高 5.30 倍。
  - 相较仅把额外 GPU 当作容量扩展、每个分区重复搜索，核心创新是让搜索路径本身跨 GPU 流水扩展，并以代表点与方向先验同时缩短起点和局部搜索空间。
  - 多 GPU ANNS、Graph Search Pipeline、Ghost Staging、Direction-Guided Selection

- [Universal Checkpointing: A Flexible and Efficient Distributed Checkpointing System for Large-Scale DNN Training with Reconfigurable Parallelism](https://www.usenix.org/conference/atc25/presentation/lian)
  - Xinyu Lian, University of Illinois Urbana–Champaign; Sam Ade Jacobs, Lev Kurilenko, and Masahiro Tanaka, Microsoft; Stas Bekman, Snowflake; Olatunji Ruwase, Microsoft; Minjia Zhang, University of Illinois Urbana–Champaign
  - Universal Checkpointing 解决大模型训练的 distributed checkpoint 与保存时使用的 tensor/data/pipeline/expert parallel 分片和硬件数量紧耦合，导致故障恢复或弹性扩缩后不能换 parallel strategy。UCP 用与训练布局无关的规范 checkpoint structure 表达参数、optimizer 等状态，再由 pattern-based reconfiguration pipeline 识别 shard pattern，自动映射、聚合或切分到新并行配置。对 dense/sparse LLM 支持比现有系统更广的配置转换，额外重配置成本可忽略，已用于真实 LLM 训练。
  - 相较为每组源/目标 parallelism 手写 checkpoint converter，核心创新是将持久状态先解耦为独立规范表示，再用可识别的分片 pattern 生成重分布流程，将 O(n²) 转换规则收敛到一个中间形式。
  - 大模型分布式检查点、并行策略重配置、布局无关状态、Pattern Mapping

- [Towards High-Performance Transactional Stateful Serverless Workflows with Affinity-Aware Leasing](https://www.usenix.org/conference/atc25/presentation/zhao-jianjun)
  - Jianjun Zhao, Haikun Liu, Shuhao Zhang, and Haodi Lu, Huazhong University of Science and Technology; Yancan Mao, School of Computing, National University of Singapore; Zhuohui Duan, Xiaofei Liao, and Hai Jin, Huazhong University of Science and Technology
  - RTSFaaS 为多函数共享状态的 transactional serverless workflow 提供一致性，但不把每次读写都导向外部 datastore。Lease-based concurrency control 将数据使用权动态分配到 worker；affinity-aware assignment 根据 data–function 共现将 lease 给能最大化本地 cache 复用的 worker；当并发 workflow 需要转移使用权时，单边 RDMA 在远端序列化访问，减少锁竞争/消息往返。比 Boki/Beldi 最高快 5 倍/20 倍，就算将其协议移植到 RDMA 也快 1.7 倍/2.1 倍。
  - 相较依赖外部存储统一锁定或在 worker 间频繁 RPC 交接状态，核心创新是将事务 lease 同时作为并发权限和缓存放置单位，用 function affinity 选所有者，用单边 RDMA 低成本迁移。
  - Transactional Serverless Workflow、Affinity-Aware Lease、单边 RDMA 锁、状态缓存一致性

- [Swift: Fast Performance Tuning with GAN-Generated Configurations](https://www.usenix.org/conference/atc25/presentation/chen-chao)
  - Chao Chen and Shixin Huang, Shenzhen Institutes of Advanced Technology, Chinese Academy of Sciences; Xuehai Qian, Tsinghua University; Zhibin Yu, Shenzhen Institutes of Advanced Technology, Chinese Academy of Sciences; and Shuhai Lab, Huawei Cloud
  - Swift 为 Apache Flink、Spark 等大数据系统的高维配置做 Bayesian Optimization，但不在每轮只用 acquisition function 从广阔空间中挑少量点。GAN 以当前已评估最佳配置及其附近的高质量样本学习配置分布，生成偏向高性能区域的新候选；系统将它们与随机候选混合，保留 exploration 同时让 BO 更快收敛。在 Flink、Spark 和工业环境中，用显著更短的调优时间超过现有配置优化性能。
  - 相较纯 BO 在全空间上依赖单点 acquisition 或手工缩窄参数范围，核心创新是用 GAN 学习当前优区的候选分布，再与随机点混合以在局部收敛和全局探索之间取舍。
  - 大数据系统配置调优、Bayesian Optimization、GAN 候选生成、搜索空间偏置

- [PMR: Fast Application Response via Parallel Memory Reclaim on Mobile Devices](https://www.usenix.org/conference/atc25/presentation/li-wentong)
  - Wentong Li, MoE Engineering Research Center of Software/Hardware Co-Design Technology and Application, East China Normal University, Shanghai, China; and School of Computer Science and Technology, East China Normal University; Li-Pin Chang, National Yang Ming Chiao Tung University, Taiwan; Yu Mao, City University of Hong Kong, Hong Kong; and MBZUAI, Abu Dhabi; Liang Shi, MoE Engineering Research Center of Software/Hardware Co-Design Technology and Application, East China Normal University, Shanghai, China; and School of Computer Science and Technology, East China Normal University
  - PMR 优化 Android 内存压力下应用切换/唤醒被内核 reclaim 拖慢的问题。Proactive Page Shrinking 将 victim page 的筛选/映射收缩与耗时的脏页 writeback 从串行路径解耦，让多组回收任务并行推进；Storage-Friendly Page Writeback 将一批 victim 集中 unmap，再合并为适合现代 flash 的批量写 I/O。真实手机上比原 Android reclaim 将应用响应时间最高改善 43.6%。
  - 相较在同一 reclaim thread 中逐页完成 shrink–unmap–writeback，核心创新是先分离页管理与存储 I/O 以提取并行性，再为 flash 把零散脏页重组为批量写，同时利用多核与新存储。
  - Android 内存回收、并行 Page Shrinking、批量脏页回写、移动应用响应

- [SAVE: Software-Implemented Fault Tolerance for Model Inference against GPU Memory Bit Flips](https://www.usenix.org/conference/atc25/presentation/zheng)
  - Wenxin Zheng, Bin Xu, Jinyu Gu, and Haibo Chen, Shanghai Jiao Tong University
  - SAVE 保护自动驾驶、工业机器人和卫星等边缘模型推理免受 GPU memory bit flip，但不复制整个模型。Selection 根据模型非线性激活与 bit significance 识别会静默破坏结果的脆弱 bit/计算；Allocation 优先将其映射到加速器上容量小但 bit-flip-free 的 reliable memory；Verification 用异步 CPU check 低成本验错，Edit 修复已检出故障。在视觉、机器人和决策模型上即使注入 4K bit flips 仍保持准确率，性能开销小于 9%。
  - 相较对全部权重/激活使用 ECC/双写，或议练出状态容错模型而损失精度，核心创新是根据模型语义分级 bit 脆弱性，只将关键计算放入稀缺可靠存储并与异步验证/修复配合。
  - 边缘 ML 可靠推理、GPU Bit Flip、脆弱 Bit 选择、可靠内存分配

- [Identifying and Analyzing Pitfalls in GNN Systems](https://www.usenix.org/conference/atc25/presentation/gong)
  - Yidong Gong, Arnab Kanti Tarafder, Saima Afrin, and Pradeep Kumar, William & Mary
  - 该工作系统审查近期 GNN system 论文，发现常见评估省略训练 accuracy，并直接或间接使用较小图数据；这会让不保持模型语义/收敛的系统改写被错当成可用优化，并进一步影响实现、框架集成与性能结论。作者归纳根因、提出评估建议，并构建 GRAPHPY 定量展示 pitfall 对 accuracy、memory 和 runtime 的影响，给出可实际集成的基准与优化路径。
  - 相较仅以 epoch time、kernel throughput 或峰值显存表示 GNN 系统进步，核心贡献是将模型准确性与真实数据规模恢复为系统正确性的必要条件，并用可运行原型证明忽略它会改变结论。
  - GNN 系统评估、训练准确性、数据集规模偏差、GRAPHPY 基准

- [Bluetooth Low Energy Security Testing with Combinatorial Methods](https://www.usenix.org/conference/atc25/presentation/schreiber)
  - Dominik-Philip Schreiber, Manuel Leithner, and Jovan Zivanovic, SBA Research; Dimitris E. Simos, SBA Research, Salzburg University of Applied Sciences, and Paris Lodron University of Salzburg
  - 该工作将 Combinatorial Security Testing 接入可越过 Host Controller Interface 限制、用自定义固件操作 BLE controller 的已有 fuzzing 框架。CST 不依赖随机变异是否刚好命中协议状态/字段组合，而生成 covering array，保证输入参数任意 t-way 组合被覆盖。对 10 种 BLE 设备和多固件版本共找到 19 类独立问题，既复现原 fuzzer 结果，也发现其漏掉的故障，并量化两者执行时间与检错差异。
  - 相较纯 coverage-guided fuzzing 只提供概率性探索、无法说明哪些字段交互已被穷尽，核心创新是用组合覆盖强度给 BLE 低层测试可量化保证，与随机 fuzzing 形成互补。
  - Bluetooth Low Energy 安全测试、Combinatorial Testing、Covering Array、Controller 固件

- [Resource Multiplexing in Tuning and Serving Large Language Models](https://www.usenix.org/conference/atc25/presentation/he-yongjun)
  - Yongjun He and Haofeng Yang, ETH Zurich; Yao Lu, National University of Singapore; Ana Klimovic and Gustavo Alonso, ETH Zurich
  - LLMStation 在同一 GPU 池上并发执行 LLM fine-tuning 与有严格延迟 SLO 的推理，用空间和时间双重复用消除单用途部署的空闲。Iteration-level multitasking scheduler 在微调迭代和推理 burst 之间分配时间/容量；定制 Autograd engine 将一个 tuning iteration 分解为可安全暂停/恢复的 pipeline；serving engine 可把 inference 和 tuning 内部计算共同 batching。在保持推理 SLO 时，吞吐比现有系统高 1.38–14.77 倍。
  - 相较为 tuning/serving 静态分开 GPU，或只在 kernel 边界粗粒度抢占训练，核心创新是重写 Autograd 使迭代内部可暂停，并把这种可中断性与跨工作负载 batching 结合。
  - LLM 微调/推理同置、空时 GPU 复用、可暂停 Autograd、推理 SLO

- [Colocating ML Inference and Training with Fast GPU Memory Handover](https://www.usenix.org/conference/atc25/presentation/wang-jiali)
  - Jiali Wang, Yankui Wang, Mingcong Han, and Rong Chen, Institute of Parallel and Distributed Systems, Shanghai Jiao Tong University
  - SIRIUS 让延迟敏感 ML inference 和 best-effort training 在同一 GPU 上空间共享：推理可随时无干扰地使用全部 GPU，训练只占用当前剩余容量。系统利用一个 batch 中 gradient computation 的阶段性，在数毫秒内改变训练显存占用；显式回收流程确保 memory handover 完整安全；SLO-aware reallocation 保留合适的可复用内存，避免频繁波动时初始化与 thrashing。推理 SLO 达标率平均提高 57% 、最高 97%，训练吞吐平均提高 2.2 倍、最高 13.7 倍。
  - 相较为训练预留固定 GPU memory 或在推理 burst 到达时停止/重启整个 job，核心创新是利用 gradient 计算的显存可塑性做毫秒级安全交接，再用 SLO 预测控制回收/重建频率。
  - ML 训练/推理同置、GPU 显存快速交接、梯度计算可塑性、SLO 感知重分配

- [AssyLLM: Efficient Federated Fine-tuning of LLMs via Assembling Pre-trained Blocks](https://www.usenix.org/conference/atc25/presentation/zhan)
  - Shichen Zhan, Li Li, and Chengzhong Xu, University of Macau
  - AssyLLM 为内存受限移动设备的联邦 LLM 适配避免反向传播：它将多个预训练 LLM 分解为 transformer block，各 client 根据私有 corpus 迭代选择并拼装最合适的 block。Block Comparator 评估相邻 block 兼容性，Elastic Adapter 吸收结构差异，Block Quanter 根据输出激活调整候选权重精度以降低常驻内存，Block Swapper 依据块相关性排换入/换出流水。比传统微调准确率最高提升 18.26%、速度高 30.04 倍，内存最多减少 92%。
  - 相较在每个 client 上对参数/adapter 做 backprop，核心创新是把适配问题改写为预训练 block 的选择与结构化拼装，并用兼容 adapter、动态量化和相关性 swapping 解决候选块带来的新成本。
  - 联邦 LLM 适配、预训练 Block 拼装、无反向传播微调、边缘内存压缩

- [Learning-Enhanced High-Throughput Pattern Matching Based on Programmable Data Plane](https://www.usenix.org/conference/atc25/presentation/duan-guanglin)
  - Guanglin Duan and Yucheng Huang, Peng Cheng Laboratory, Tsinghua Shenzhen International Graduate School; Zhengxin Zhang, Peng Cheng Laboratory, Tsinghua Shenzhen International Graduate School, and Cornell University; Qing Li and Dan Zhao, Peng Cheng Laboratory; Zili Meng, Hong Kong University of Science and Technology; Dirk Kutscher, Hong Kong University of Science and Technology (Guangzhou); Ruoyu Li, Shenzhen University and Peng Cheng Laboratory; Yong Jiang, Tsinghua Shenzhen International Graduate School; Mingwei Xu, Tsinghua University
  - Trochilus 在可编程数据面直接做网络安全复杂 pattern matching。它先用 byte-level RNN 学习难以手写规则表达的模式，在新威胁到达时可自动更新；由于标注流量稀缺且 RNN 无法进交换机，semi-supervised knowledge distillation 将教师转成轻量 soft multi-view forest，再映射到 match-action table；entry clustering 合并相似决策区域，减少昂贵 TCAM。系统支持多类 pattern set，达到多 Tbps 吞吐且在自动更新下保持高准确率。
  - 相较全靠专家将规则手工编码为 TCAM 或在主机/GPU 运行高成本模型，核心创新是以半监督知识蒸馏连接表达能力强的 BRNN 与数据面可执行的 forest/table，再以 entry clustering 控制片上成本。
  - 可编程数据面 Pattern Matching、BRNN 知识蒸馏、Soft Multi-View Forest、TCAM 条目聚类
