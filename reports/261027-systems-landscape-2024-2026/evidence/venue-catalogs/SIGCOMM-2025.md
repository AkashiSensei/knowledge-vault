# SIGCOMM 2025 论文列表

## 范围与核验

[2025 官方 accepted papers](https://conferences.sigcomm.org/sigcomm/2025/accepted-papers/)。本列表以 SIGCOMM 2025 官方 accepted list 和最终 program 为边界，共 88 篇主会论文：74 篇 Full Paper、14 篇 Short Paper；两类都进入正式主会，故全部纳入。逐篇标题、作者/机构、摘要和 DOI 已与最终 program、ACM proceedings 父 DOI `10.1145/3718958` 及 Crossref 元数据交叉核验；早期 accepted 页的 `Caching as Differentiation` 在最终版本改名为 `Edge Caching as Differentiation`，作者一致，按同一论文处理。

本地保留 13 份 DOI 对应的合法 arXiv 预印本，位于 `reference/SIGCOMM/2025/`；全部通过 `%PDF-` 文件头、PDF 解析、页数和首页文本检查。其余论文严格依据官方 program 摘要预读，不因 ACM 下载受限而臆造正文细节。

方向统计互斥：每篇只按核心研究对象进入一个主方向，合计严格等于年度论文总数。

## 互斥主方向统计

| 主方向 | 论文数 | 占比 |
|---|---:|---:|
| AI 集群网络与大模型系统 | 14 | 15.9% |
| 数据中心网络、传输与互连 | 12 | 13.6% |
| 可编程数据平面与云网络 | 11 | 12.5% |
| 网络测量、诊断与可观测性 | 13 | 14.8% |
| 网络验证、管理与安全 | 7 | 8.0% |
| 互联网架构、路由与流量控制 | 7 | 8.0% |
| 无线、蜂窝与感知 | 7 | 8.0% |
| 卫星、海洋与非地面网络 | 7 | 8.0% |
| 视频、实时通信与 QoE | 7 | 8.0% |
| 分布式系统与网络服务 | 3 | 3.4% |

## 热门问题与方法

- 主方向前三位为 AI 集群网络与大模型系统 14 篇、网络测量、诊断与可观测性 13 篇、数据中心网络、传输与互连 12 篇。AI 训练/推理网络、RDMA/可编程硬件与生产可观测性构成会议的主要系统轴。
- 热门问题集中在 LLM/MoE 训练通信、KV-cache 传输、RDMA 可靠性与虚拟化、生产网络故障定位、卫星/水下连接，以及超大规模视频 QoE；常见方法是光电混合互连、集合通信调度、SmartNIC/DPU offload、形式验证、主动测量和生产 A/B 实验。
- Agent 相关只有 Confucius 与 BIAN：前者把规划、工具和验证组成网络运维闭环，后者是 LLM 辅助故障定位。标题中的 agentless probing、传统神经网络/RL 或一般 AI networking 不纳入 Agent 四分类。

## Agent 四分类

| 分类 | 论文数 | 论文与判定依据 |
|---|---:|---|
| Agent System | 0 | 无 |
| Agent Infra | 0 | 无 |
| Agent for Systems | 1 | Intent-Driven Network Management with Multi-Agent LLMs: The Confucius Framework：以 DAG 规划网络运维流程，连接既有工具、RAG 记忆与验证环，属于面向网络管理的多 Agent 执行闭环。 |
| LLM for Systems | 1 | Towards LLM-Based Failure Localization in Production-Scale Networks：BIAN 用 LLM 对监控数据排序并解释故障设备，但核心是辅助诊断，没有自主行动—验证迭代。 |

四类只统计以 LLM/生成式 Agent 为核心对象或方法的论文；传统 RL/MARL、神经网络流量预测、一般 AI 网络优化，以及仅出现 software agent/agentless 等字样的工作均不计入。

## 论文条目

- [InfiniteHBD: Building Datacenter-Scale High-Bandwidth Domain for LLM with Optical Circuit Switching Transceivers](https://dl.acm.org/doi/10.1145/3718958.3750468)
  - Chenchen Shou (Peking University & StepFun & Lightelligence Pte. Ltd.); Guyue Liu (Peking University); Hao Nie (StepFun); Huaiyu Meng (Lightelligence Pte. Ltd.); Yu Zhou (StepFun); Yimin Jiang (Unaffiliated); Wenqing Lv, Yelong Xu (Lightelligence Pte. Ltd.); Yuanwei Lu (StepFun); Zhang Chen (Lightelligence Pte. Ltd.); Yanbo Yu (StepFun); Yichen Shen (Lightelligence Pte. Ltd.); Yibo Zhu, Daxin Jiang (StepFun)
  - 扩展大型语言模型 (LLM) 训练依赖于多维并行性，其中高带宽域 (HBD) 对于张量并行性等通信密集型并行性至关重要；然而，现有的 HBD 架构在可扩展性、成本和故障恢复方面面临着根本性的限制：以交换机为中心的 HBD（例如 NVL-72）会产生过高的扩展成本，而以 GPU 为中心的 HBD（例如 TPUv3/Dojo）会遭受严重的故障传播。InfiniteHBD 是一种以收发器为中心的 HBD 架构，通过在每个收发器中嵌入光路交换 (OCS)，在收发器级别集成连接和动态切换；它支持可重新配置的点对多点通信和可扩展的可变大小环拓扑；评估表明，InfiniteHBD 将成本降低至 NVL-72 的 31%，实现近乎零的 GPU 浪费率（比 NVL-72 和 TPUv4 低 10 倍以上），在 7% 的节点故障率下保持近零的跨 ToR 流量。
  - 相较Switch-GPU 混合 HBD（例如 TPUv4）采取中间立场，但故障影响半径仍然很大，核心创新是InfiniteHBD 是一种以收发器为中心的 HBD 架构，通过在每个收发器中嵌入光路交换 (OCS)，在收发器级别集成连接和动态切换；它支持可重新配置的点对多点通信和可扩展的可变大小环拓扑。
  - AI 集群网络与大模型系统、Full Paper、LLM Systems、Optical Interconnect、Scheduling/Orchestration

- [DistTrain: Addressing Model and Data Heterogeneity with Disaggregated Training for Multimodal Large Language Models](https://dl.acm.org/doi/10.1145/3718958.3750472)
  - Zili Zhang, Yinmin Zhong (School of Computer Science, Peking University); Yimin Jiang (Independent Researcher); Hanpeng Hu, Jianjian Sun, Zheng Ge, Yibo Zhu, Daxin Jiang (StepFun); Xin Jin (School of Computer Science, Peking University)
  - 多模态大语言模型 (LLM) 使 LLM 能够接收输入并生成多种形式的输出，例如文本、图像和音频；然而，多种模态的集成在模型和训练数据中引入了异质性，从而带来了独特的系统挑战。DistTrain 是一个针对多模态 LLM 的解耦训练系统；DistTrain 结合了两种新颖的解耦技术，分别解决模型和数据异构性；第一个是解耦式模型编排，它将模态编码器、LLM 主干和模态生成器的训练分开；这使得三个组件能够自适应且独立地编排其资源和并行配置；实验结果表明，在 1172 个 GPU 上训练 72B 多模态 LLM 时，DistTrain 实现了 54.7% 的模型 FLOP 利用率（MFU），并且在训练吞吐量方面优于 Megatron-LM 高达 2.2×。
  - 相较多种模态的集成在模型和训练数据中引入了异质性，从而带来了独特的系统挑战，核心创新是DistTrain 是一个针对多模态 LLM 的解耦训练系统；DistTrain 结合了两种新颖的解耦技术，分别解决模型和数据异构性；第一个是解耦式模型编排，它将模态编码器、LLM 主干和模态生成器的训练分开。
  - AI 集群网络与大模型系统、Full Paper、LLM Systems、Scheduling/Orchestration、NetAI

- [SCX: Stateless KV-Cache Encoding for Cloud-Scale Confidential Transformer Serving](https://dl.acm.org/doi/10.1145/3718958.3750509)
  - Mu Yuan (The Chinese University of Hong Kong); Lan Zhang (University of Science and Technology of China); Liekang Zeng, Siyang Jiang, Bufang Yang, Di Duan, Guoliang Xing (The Chinese University of Hong Kong)
  - Transformer 模型彻底改变了自然语言处理和计算机视觉等领域，但在医疗诊断等敏感应用中面临隐私问题；现有的机密服务方法，包括基于密码学、基于内存隔离和基于访问控制的方法，在隐私和效率之间提供了权衡，但常常面临高延迟或硬件依赖性的问题。该工作设计无状态 KV 缓存编码（SCX），这是一种新颖的框架，可在 Transformer 推理期间使用用户控制的密钥对中间键值缓存进行编码；SCX 确保云端既不能恢复输入，也不能独立完成下一个 token 预测，有效保护隐私；通过引入高效的编码和解码方案，SCX 解决了通信复杂性和攻击漏洞，同时确保推理质量零损失；对大型 Transformer 模型的实验表明，SCX 实现了较低的延迟（例如，LLaMA-7B 为 36 毫秒），其性能优于最先进的密码学和内存隔离方法几个数量级。
  - 相较现有的机密服务方法，包括基于密码学、基于内存隔离和基于访问控制的方法，在隐私和效率之间提供了权衡，但常常面临高延迟或硬件依赖性的问题，核心创新是该工作设计无状态 KV 缓存编码（SCX），这是一种新颖的框架，可在 Transformer 推理期间使用用户控制的密钥对中间键值缓存进行编码；SCX 确保云端既不能恢复输入，也不能独立完成下一个 token 预测，有效保护隐私。
  - AI 集群网络与大模型系统、Full Paper、KV Cache、Failure Diagnosis、Security/Privacy、Caching/CDN

- [ResCCL: Resource-Efficient Scheduling for Collective Communication](https://dl.acm.org/doi/10.1145/3718958.3750514)
  - Tongrui Liu, Chenyang Hei, Fuliang Li (Northeastern University); Chengxi Gao (Shenzhen Institutes of Advanced Technology, Chinese Academy of Sciences); Jiamin Cao, Tianshu Wang, Ennan Zhai (Alibaba Cloud); Xingwei Wang (Northeastern University)
  - 随着分布式深度学习训练（DLT）系统的规模扩大，集体通信已成为一个重要的性能瓶颈；虽然当前的方法优化了带宽利用率和任务完成时间，但现有的通信库 (CCL) 后端无法在算法执行期间有效管理 GPU 资源，从而限制了高级算法的性能；ResCCL 是一种专为资源高效调度而设计的新型 CCL 后端，旨在解决当前系统中的关键限制。ResCCL 通过优化原语级别的调度（例如 send、recvReduceCopy 等）、实现灵活的线程块 (TB) 分配以及生成轻量级通信内核以最小化运行时开销来提高执行效率；在运行相同算法的情况下，它可以将 SM 资源开销降低 77.8%，并将 TB 利用率提高 41.6%。
  - 相较现有的通信库 (CCL) 后端无法在算法执行期间有效管理 GPU 资源，从而限制了高级算法的性能，核心创新是ResCCL 是一种专为资源高效调度而设计的新型 CCL 后端，旨在解决当前系统中的关键限制；ResCCL 通过优化原语级别的调度（例如 send、recvReduceCopy 等）、实现灵活的线程块 (TB) 分配以及生成轻量级通信内核以最小化运。
  - AI 集群网络与大模型系统、Full Paper、Collective Communication、Scheduling/Orchestration、NetAI

- [Albatross: A Containerized Cloud Gateway Platform with FPGA-accelerated Packet-level Load Balancing](https://dl.acm.org/doi/10.1145/3718958.3750473)
  - Jianyuan Lu (Alibaba Cloud); Shunmin Zhu (Hangzhou Feitian Cloud and Alibaba Cloud); Jun Liang, Yuxiang Lin, Tian Pan, Yisong Qiao, Yang Song, Wenqiang Su, Yixin Xie, Yanqiang Li, Enge Song, Shize Zhang, Xiaoqing Sun, Rong Wen, Xionglie Wei, Biao Lyu (Alibaba Cloud); Xing Li (Zhejiang University and Alibaba Cloud)
  - 阿里云的集中式网关严重依赖大容量交换 ASIC，但 2023 年 1 月 Tofino 芯片演进的突然停止迫使运营团队寻找能够满足性能、供应链安全、代码复用和资源效率要求的替代方案。在评估多个选项后，Albatross 是基于 FPGA 和 x86 CPU 的第三代云网关；Albatross 为主机 CPU 提供基于 FPGA 的数据包级负载平衡，以防止 CPU 核心过载，在复杂的云服务处理过程中管理高延迟抖动 (100μs) 下的大型重排序缓冲区，并解决由于数据包丢失或 CPU 中软件异常而导致的队头 (HOL) 阻塞；为了避免由于异常或攻击而导致 heavy hitter 过载，它还为仅 2MB FPGA 内存的数百万租户实现了两级速率限制器；经过数百人月的开发，单个 Albatross 节点可以处理 80–120Mpps 的云网络流量，平均延迟为 20μs，将网关和沙箱基础设施成本降低 50%。
  - 相较阿里云的集中式网关严重依赖大容量交换 ASIC，但 2023 年 1 月 Tofino 芯片演进的突然停止迫使运营团队寻找能够满足性能、供应链安全、代码复用和资源效率要求的替代方案，核心创新是在评估多个选项后，Albatross 是基于 FPGA 和 x86 CPU 的第三代云网关；Albatross 为主机 CPU 提供基于 FPGA 的数据包级负载平衡，以防止 CPU 核心过载。
  - 可编程数据平面与云网络、Full Paper、Programmable Network Hardware、Failure Diagnosis、Security/Privacy、Internet Routing

- [Revisiting RDMA Reliability for Lossy Fabrics](https://dl.acm.org/doi/10.1145/3718958.3750480)
  - Wenxue Li (Hong Kong University of Science and Technology and Huawei); Xiangzhou Liu, Yunxuan Zhang, Zihao Wang (Hong Kong University of Science and Technology); Wei Gu, Tao Qian, Gaoxiong Zeng, Shoushou Ren (Huawei); Xinyang Huang, Zhenghang Ren, Bowen Liu, Junxue Zhang, Kai Chen (Hong Kong University of Science and Technology); Bingyang Liu (Huawei)
  - 由于无损 RDMA 网络的高操作复杂性和有限的部署规模，社区一直在探索有损结构上的高效 RDMA 通信；最先进的 (SOTA) 有损 RDMA 解决方案在 RDMA NIC (RNIC) 中实施简化的选择性重复机制，以提高丢失恢复效率；然而，它们仍然面临性能挑战，例如不可避免的 ECMP 冲突和过多的重传超时 (RTO)。研究团队重新审视 RDMA 可靠性，目标是独立于 PFC、兼容数据包级负载均衡、不受 RTO 影响、对硬件卸载友好；为此，该工作设计 DCP，一种将交换机和 RNIC 共同设计的传输架构，完全满足设计目标；DCP-Switch 的核心是引入了一个简单而有效的无损控制平面，DCP-RNIC 利用该控制平面来增强对高速有损结构的可靠性支持，主要包括基于 header 的重传和无位图数据包跟踪；大量实验表明，与 SOTA 无损和有损 RDMA 解决方案相比，DCP 分别实现了 1.6× 和 2.1× 的性能提升。
  - 相较它们仍然面临性能挑战，例如不可避免的 ECMP 冲突和过多的重传超时 (RTO)，核心创新是研究团队重新审视 RDMA 可靠性，目标是独立于 PFC、兼容数据包级负载均衡、不受 RTO 影响、对硬件卸载友好；为此，该工作设计 DCP，一种将交换机和 RNIC 共同设计的传输架构，完全满足设计目标。
  - 数据中心网络、传输与互连、Full Paper、RDMA、Programmable Network Hardware、Datacenter Networking

- [Software-based Live Migration for RDMA](https://dl.acm.org/doi/10.1145/3718958.3750487)
  - Xiaoyu Li (Tsinghua University/Microsoft Reaearch); Ran Shu, Yongqiang Xiong (Microsoft Research); Fengyuan Ren (Tsinghua University)
  - 热迁移对于保证数据中心主机维护期间业务不中断至关重要；另一方面，RDMA 已在数据中心广泛采用，多年来吸引了学术界和工业界的关注；然而，当今的数据中心不支持 RDMA 的实时迁移。该工作设计 MigrRDMA，一种基于软件的 RDMA 实时迁移，不依赖任何额外的硬件支持；MigrRDMA 提供软件间接层以实现到新 RDMA 通信的透明切换；与之前提供共享和隔离的 RDMA 虚拟化不同，MigrRDMA 的间接层侧重于从应用程序的角度保持迁移源和目标上的 RDMA 状态相同；评估表明，当迁移具有线速运行的实时 RDMA 连接的容器时，MigrRDMA 几乎不会增加停机时间。
  - 相较当今的数据中心不支持 RDMA 的实时迁移，核心创新是该工作设计 MigrRDMA，一种基于软件的 RDMA 实时迁移，不依赖任何额外的硬件支持；MigrRDMA 提供软件间接层以实现到新 RDMA 通信的透明切换。
  - 数据中心网络、传输与互连、Full Paper、RDMA、Cloud/Distributed Systems、Datacenter Networking

- [ByteDance Jakiro: Enabling RDMA and TCP over Virtual Private Cloud](https://dl.acm.org/doi/10.1145/3718958.3750496)
  - Yirui Liu, Lidong Jiang, Deguo Li, Daxiang Kang, Zhaoyang Wei, Yuqi Chai, Bin Niu, Ke Lin, Xiaoning Ding, Jianwen Pi, Hao Luo (ByteDance)
  - 同时支持 RDMA 和 TCP 的虚拟私有云为租户和云提供商提供了优势；它满足租户应用程序对 RDMA 和 TCP 的灵活需求，同时与构建两个不同的覆盖网络相比，提供经济高效的解决方案。该工作设计 Jakiro，这是一种创新的 vNIC 设计框架，支持字节跳动云中的 RDMA 和 TCP；Jakiro 能够支持 RDMA 和 TCP 流的基本 VPC 功能，例如 QoS、安全组等，同时保持与应用程序和主机内 RDMA 优化技术的兼容性；研究使用基本测试用例和现实世界的高性能计算应用程序以及分布式机器学习训练来对 Jakiro 的性能进行基准测试；Jakiro 已经在字节跳动云部署一年了，该工作总结其关键设计和部署决策，以及生产中的经验和教训。
  - 官方摘要未展开更细的直接基线；可核验的核心创新是该工作设计 Jakiro，这是一种创新的 vNIC 设计框架，支持字节跳动云中的 RDMA 和 TCP；Jakiro 能够支持 RDMA 和 TCP 流的基本 VPC 功能，例如 QoS、安全组等。
  - 数据中心网络、传输与互连、Full Paper、RDMA、Security/Privacy、Datacenter Networking

- [LeoCC: Making Internet Congestion Control Robust to LEO Satellite Dynamics](https://dl.acm.org/doi/10.1145/3718958.3750491)
  - Zeqi Lai, Zonglun Li, Qian Wu, Hewu Li (Tsinghua University); Jihao Li (Zhongguancun Laboratory); Xin Xie, Yuanjie Li, Jun Liu, Jianping Wu (Tsinghua University)
  - 最近近地轨道（LEO）卫星网络的复兴扩大了全球互联网接入的边界，但也给现有的端到端拥塞控制算法（CCA）带来了巨大的新挑战；LEO 卫星的快速且连续的运动会导致基础设施级的动态变化，导致低地球轨道动态引起的链路容量、延迟和丢包率频繁变化，这可能会进一步误导现有 CCA 中的速率控制并导致性能自限。LeoCC 是一种新颖的 CCA，可以解决上述挑战，并且对 LEO 卫星动力学具有鲁棒性；LeoCC 背后的核心思想在于新兴 LEO 网络的一个关键特征，即“连接重新配置”，它隐式地反映了卫星路径的变化，并且与网络变化密切相关；具体来说，LeoCC 采用了一套新技术来： (i) 有效地检测端点上的重新配置； (ii) 应用重新配置感知模型来准确描述和估计网络状况； (iii) 精准调控发送速率；结果表明，与其他现有的 CCA 相比，LeoCC 在各种 LEO 网络条件下都能实现最佳的吞吐量-延迟平衡：比 Cubic、Copa、BBRv3 提高 85∼494%的吞吐量，比 BBRv1 和 VIVACE 降低 44∼56%的延迟。
  - 相较现有 CCA 中的速率控制并导致性能自限，核心创新是LeoCC 是一种新颖的 CCA，可以解决上述挑战，并且对 LEO 卫星动力学具有鲁棒性；LeoCC 背后的核心思想在于新兴 LEO 网络的一个关键特征，即“连接重新配置”，它隐式地反映了卫星路径的变化，并且与网络变化密切相关。
  - 卫星、海洋与非地面网络、Full Paper、Congestion Control、Satellite/LEO

- [Censys: A Map of Internet Hosts and Services](https://dl.acm.org/doi/10.1145/3718958.3754344)
  - Zakir Durumeric, Hudson Clark, Jeff Cody, Elliot Cubit, Matt Ellison, Liz Izhikevich, Ariana Mirian (Censys Inc.)
  - Censys 持续扫描并结构化 Internet host/service 数据，这项经验总结说明其从 2015 年研究数据集演进为商业与政府用户基础设施后的采集管线、服务行为建模和当前架构；同时量化数据可见性，并交代不同使用场景下的边界与未解问题。
  - 相较把 Internet-wide scan 当作静态数据集，核心贡献是公开长期运营中采集、行为解析与覆盖率评估的演进经验，使下游研究能判断数据偏差。
  - 网络测量、诊断与可观测性、Full Paper、Measurements

- [Edge Caching as Differentiation](https://dl.acm.org/doi/10.1145/3718958.3754350)
  - Muhammad Abdullah (EPFL); Mughees Ur Rehman (Virginia Tech); Pavlos Nikolopoulos, Katerina Argyraki (EPFL)
  - 该工作考察同类内容提供商 A/B 经由同一 ISP 访问时的 QoE：即使 ISP 没有显式区分流量，边缘缓存对 A 的命中率高于 B 也会使用户感受到类似优先级的质量差异；论文用这一机制讨论缓存部署的公平性与政策影响。
  - 相较只把流量调度视为差别待遇来源，核心创新是揭示内容特定的缓存命中率本身也会产生可观测的 QoE 分化。
  - 互联网架构、路由与流量控制、Full Paper、Network Measurement/Telemetry、Video/QoE、Caching/CDN

- [Raha: A General Tool to Analyze WAN Degradation](https://dl.acm.org/doi/10.1145/3718958.3754348)
  - Behnaz Arzani (Microsoft Research); Sina Taheri (Microsoft); Pooria Namyar (University of Southern California); Ryan Beckett, Siva Kesava Reddy Kakarla (Microsoft Research); Elnaz Jalilipour (Microsoft)
  - Raha 分析 traffic-engineered WAN 在任意故障组合与流量转移下可能出现的性能退化：它以无故障设计点和故障状态之间的性能差为搜索目标，不限定故障数 k 或特定 TE 方案，并从反例生成容量增强建议。Microsoft 生产网和 Topology Zoo 实验显示，它能找到比只考虑最多两个故障的工具高至少 2 倍的最坏退化。
  - 相较固定故障上限、固定 TE 策略或只找绝对最坏值的方法，核心创新是把“偏离当前设计点的幅度”作为通用退化分析目标。
  - 互联网架构、路由与流量控制、Full Paper、Traffic Engineering

- [ParserHawk: Hardware-aware parser generator using program synthesis](https://dl.acm.org/doi/10.1145/3718958.3750484)
  - Xiangyu Gao (University of Washington); Jiaqi Gao (Alibaba Cloud); Karan Kumar G, Muhammad Haseeb (New York University); Ennan Zhai (Alibaba Cloud); Bili Dong (Google); Joseph Tassarotti (New York University); Srinivas Narayana (Rutgers University); Anirudh Sivaraman (New York University)
  - ParserHawk 面向 Intel IPU 和 Tofino 可编程交换机的 parser 编译：输入是高层 parser program 与目标硬件资源约束，编译器用 program synthesis 搜索低层映射，再用多项优化将原本可能耗时数小时的搜索压到分钟级。它能编译被现有规则式编译器误拒的合法程序，并用更少硬件资源，合成搜索几何平均加速 309.44 倍。
  - 相较依赖预定义 rewrite rule、对源程序写法敏感的 parser 编译器，核心创新是把硬件映射表达为可优化的程序合成问题。
  - 可编程数据平面与云网络、Full Paper、Programmable Network Hardware、Hardware

- [Nezha: SmartNIC-based Virtual Switch Load Sharing](https://dl.acm.org/doi/10.1145/3718958.3750466)
  - Xing Li (Zhejiang University and Alibaba Cloud); Enge Song, Bowen Yang, Tian Pan, Ye Yang (Alibaba Cloud); Qiang Fu (School of Computing Technologies, RMIT University); Yang Song, Yilong Lv, Zikang Chen, Jianyuan Lu, Shize Zhang, Xiaoqing Sun, Rong Wen, Xionglie Wei (Alibaba Cloud); Biao Lyu (Zhejiang University and Alibaba Cloud); Zhigang Zong (Alibaba Cloud); Qinming He (Zhejiang University); Shunmin Zhu (Hangzhou Feitian Cloud and Alibaba Group)
  - 云提供商使用 SmartNIC 加速虚拟交换机 (vSwitches) 为租户虚拟机提供丰富的网络功能 (NF)；受 SmartNIC 资源有限的限制，为高需求的虚拟机提供足够的网络性能是一个挑战。Nezha 是一种分布式 vSwitch 负载共享系统；哪吒复用现有闲置的 SmartNIC 来处理本地 SmartNIC 的过量负载，而无需添加新设备；Nezha 将无状态规则/流表卸载到远程，同时在本地保留状态；这消除了状态同步的需要，从而促进负载共享和故障转移；从生产中收集的数据表明，其 CPS 能力瓶颈已从 vSwitch 转移到 VM 内核堆栈，#concurrent 流和 #vNIC 分别增加了 50.4 倍和 40 倍。
  - 相较受 SmartNIC 资源有限的限制，为高需求的虚拟机提供足够的网络性能是一个挑战，核心创新是Nezha 是一种分布式 vSwitch 负载共享系统；哪吒复用现有闲置的 SmartNIC 来处理本地 SmartNIC 的过量负载，而无需添加新设备；Nezha 将无状态规则/流表卸载到远程，同时在本地保留状态。
  - 可编程数据平面与云网络、Full Paper、SmartNIC/DPU、Network Measurement/Telemetry、Hardware

- [Mosaic: Breaking the Optics versus Copper Trade-off with a Wide-and-Slow Architecture and MicroLEDs](https://dl.acm.org/doi/10.1145/3718958.3750510)
  - Kaoutar Benyahya, Ariel Gomez Diaz, Junyi Liu, Vassily Lyutsarev, Marianna Pantouvaki, Kai Shi, Shawn Yohanes Siew, Hitesh Ballani, Thomas Burridge, Daniel Cletheroe, Thomas Karagiannis, Brian Robertson, Ant Rowstron, Mengyang Yang (Microsoft Research); Arash Behziz, Jamie Gaudette (Microsoft Azure); Paolo Costa (Microsoft Research)
  - 当今网络中的链路技术在覆盖范围、功率和可靠性之间进行了基本的权衡；铜链路节能且可靠，但覆盖范围非常有限 (<2 m)；相比之下，光链路提供了更长的传输距离，但代价是高功耗和低可靠性。Mosaic 是一种打破这种权衡的新颖光链路技术；与现有的铜缆和光链路依赖于具有少量高速通道的窄而快速的架构不同，它采用宽而慢的设计，采用数百个并行低速、面积和功率高效的通道；实验演示一个具有 100 个光通道的端到端 Mosaic 原型，每个光通道的传输速度为 2Gbps，并展示了它如何扩展到 800Gbps 及以上，传输距离可达 50m。
  - 相较相比之下，光链路提供了更长的传输距离，但代价是高功耗和低可靠性，核心创新是Mosaic 是一种打破这种权衡的新颖光链路技术；与现有的铜缆和光链路依赖于具有少量高速通道的窄而快速的架构不同，它采用宽而慢的设计，采用数百个并行低速、面积和功率高效的通道。
  - 数据中心网络、传输与互连、Full Paper、Optical Interconnect

- [Falcon: A Reliable, Low Latency Hardware Transport](https://dl.acm.org/doi/10.1145/3718958.3754353)
  - Arjun Singhvi (Google); Nandita Dukkipati (Google LLC); Prashant Chandra, Hassan M. G. Wassel, Naveen Kr. Sharma, Anthony Rebello, Henry Schuh, Praveen Kumar, Behnam Montazeri, Neelesh Bansod, Sarin Thomas, Inho Cho, Hyojeong Lee Seibert, Baijun Wu, Rui Yang, Yuliang Li, Kai Huang, Qianwen Yin, Abhishek Agarwal (Google); Srinivas Vaduvatha (Meta); Weihuang Wang, Masoud Moshref (Nvidia); Tao Ji (Microsoft); David Wetherall, Amin Vahdat (Google)
  - RoCE 等硬件传输以最少的主机 CPU 提供高性能，但最适合限制其使用的特殊用途部署，例如具有优先级流量控制 (PFC) 的后端网络或以太网。Falcon 是第一个在通用以太网数据中心环境中支持多个上层协议 (ULP) 和异构应用程序工作负载的硬件传输（有损耗且无需特殊交换机支持）；关键设计元素包括：基于延迟的拥塞控制和多路径负载平衡；具有简单请求响应事务接口的分层设计，用于多 ULP 支持；基于硬件的重传和错误处理以实现可扩展性；以及一个具有灵活性的可编程引擎。
  - 相较RoCE 等硬件传输以最少的主机 CPU 提供高性能，但最适合限制其使用的特殊用途部署，例如具有优先级流量控制 (PFC) 的后端网络或以太网，核心创新是Falcon 是第一个在通用以太网数据中心环境中支持多个上层协议 (ULP) 和异构应用程序工作负载的硬件传输（有损耗且无需特殊交换机支持）；关键设计元素包括：基于延迟的拥塞控制和多路径负载平衡。
  - 可编程数据平面与云网络、Full Paper、Congestion Control、Hardware

- [Hattrick: Solving Multi-Class TE using Neural Models](https://dl.acm.org/doi/10.1145/3718958.3750470)
  - Abd AlRhman AlQiam, Zhuocong Li (Purdue University); Satyajeet Singh Ahuja (Meta Platforms, Inc); Zhaodong Wang, Ying Zhang (Meta); Sanjay G. Rao, Bruno Ribeiro, Mohit Tawarmalani (Purdue University)
  - 虽然最近的研究表明基于机器学习的方法是流量工程 (TE) 传统优化方法的一种有前途的替代方法，但现有的研究仅限于单一流量类别。Hattrick 是第一个基于 ML 的方法，用于处理多个流量类别，这是云和 ISP WAN 的关键要求；作为 Hattrick 的一部分，该工作设计 (i) 一种新颖的神经架构，与多类 TE 中的优化问题序列相一致； (ii) 经典多任务学习方法的变体，用于应对优化具有优先关系的多个指标的独特挑战；对大型私有 WAN 和其他公共数据集的评估表明，Hattrick 通过更好地应对预测误差，优于最先进的基于优化的多类 TE 方法 - 例如，对于 GEANT，在考虑可支持 2 个 9 的时间的流量时。
  - 相较传统优化方法的一种有前途的替代方法，但现有的研究仅限于单一流量类别，核心创新是Hattrick 是第一个基于 ML 的方法，用于处理多个流量类别，这是云和 ISP WAN 的关键要求；作为 Hattrick 的一部分，该工作设计 (i) 一种新颖的神经架构，与多类 TE 中的优化问题序列相一致。
  - 互联网架构、路由与流量控制、Full Paper、Traffic Engineering

- [CClinguist: An Expert-Free Framework for Future-Compatible Congestion Control Algorithm Identification](https://dl.acm.org/doi/10.1145/3718958.3750485)
  - Jiahui Li, Han Qi, Ruyi Yao, Jialin Wei, Ruoshi Sun, Zixuan Chen, Sen Liu, Yang Xu (Fudan University)
  - 拥塞控制算法 (CCA) 在确定传输质量方面发挥着关键作用；随着过去几十年的快速发展，了解互联网上的 CCA 格局对于网络发展变得越来越重要；然而，传统的 CCA 普查工具严重依赖手动配置和构建，需要大量人力才能跟上新 CCA 的引入。CClinguist 是一个框架，它是一个无需专家的 CCA 识别工具；它主要包括网络概况自动生成器和自学习分类器，以适应新兴的 CCA 和新的网络场景，确保未来网络普查在时间和空间方面的兼容性；值得注意的是，它在新场景和新兴 CCA 中保持了高精度，包括基于学习和基于 ECN 的 CCA，其性能优于最先进的识别工具。
  - 相较传统的 CCA 普查工具严重依赖手动配置和构建，需要大量人力才能跟上新 CCA 的引入，核心创新是CClinguist 是一个框架，它是一个无需专家的 CCA 识别工具；它主要包括网络概况自动生成器和自学习分类器，以适应新兴的 CCA 和新的网络场景，确保未来网络普查在时间和空间方面的兼容性。
  - 网络测量、诊断与可观测性、Full Paper、Congestion Control、Network Measurement/Telemetry、AI for SysNet

- [The Sweet Danger of Sugar: Debunking Representation Learning for Encrypted Traffic Classification](https://dl.acm.org/doi/10.1145/3718958.3750498)
  - Yuqi Zhao, Giovanni Dettori, Matteo Boffa, Luca Vassio, Marco Mellia (Politecnico di Torino)
  - 最近，研究团队目睹了提案的激增，这些提案受到 BERT 等语言模型的启发，利用表示学习模型来创建流量表示；它们都承诺在加密流量分类方面具有惊人的性能（准确率高达 98%）；然而，其复杂性质疑其在实际环境中的适用性。该工作设计正确的评估方法，并强调需要严格的基准测试。
  - 相较其复杂性质疑其在实际环境中的适用性，核心创新是该工作设计正确的评估方法，并强调需要严格的基准测试。
  - 网络验证、管理与安全、Full Paper、Security/Privacy

- [DeepSpace: Super Resolution Powered Efficient and Reliable Satellite Image Data Acquistion](https://dl.acm.org/doi/10.1145/3718958.3750523)
  - Chuanhao Sun, Yu Zhang (The University of Edinburgh); Bill Tao, Deepak Vasisht (University of Illinois Urbana-Champaign); Mahesh Marina (The University of Edinburgh)
  - 大型低地球轨道卫星星座可以为众多地理空间应用提供频繁的高分辨率地球成像；它们在太空中生成大量数据，每天数百太字节，其中大部分数据通过与地面站的有限间歇性连接传输到地球；大量数据导致数据下载的日级延迟和高昂的云存储成本。DeepSpace 是一种基于深度学习的新型超分辨率方法，可将卫星图像压缩两个数量级以上，同时使用定制的专家混合 (MoE) 超分辨率框架保持图像质量；DeepSpace 降低了天地传输的网络带宽需求，并且可以压缩图像以进行云存储；研究团队通过几个不同的下游应用（野火检测、土地利用和农田分类以及海洋中的细粒度塑料检测）进一步证明了 DeepSpace 的有效性。
  - 相较大量数据导致数据下载的日级延迟和高昂的云存储成本，核心创新是DeepSpace 是一种基于深度学习的新型超分辨率方法，可将卫星图像压缩两个数量级以上，同时使用定制的专家混合 (MoE) 超分辨率框架保持图像质量；DeepSpace 降低了天地传输的网络带宽需求，并且可以压缩图像以进行云存储。
  - 卫星、海洋与非地面网络、Full Paper、MoE、Satellite/LEO、Underwater/Submarine Network、Compression/Encoding

- [Agua: A Concept-Based Explainer for Learning-Enabled Systems](https://dl.acm.org/doi/10.1145/3718958.3754341)
  - Sagar Patel (University of California, Irvine); Dongsu Han (KAIST); Nina Narodytska (VMware Research by Broadcom); Sangeetha Abdu Jyothi (University of California, Irvine)
  - 虽然深度学习在系统和网络方面提供了卓越的性能，但其采用常常因理解和调试方面的困难而受到阻碍；可解释性旨在通过提供对模型决策的洞察来弥合这一差距；然而，现有方法主要识别最有影响力的输入特征，迫使操作员对低级信号（例如缓冲区 t−1、块大小 t+2）进行广泛的手动分析。Agua 是一个可解释性框架，它使用人类可理解的高级概念（例如“不稳定的网络条件”）来解释模型的决策；研究团队基于概念的可解释性框架为智能网络系统奠定了基础，使操作员能够与数据驱动的系统进行交互；为了使用概念级推理解释控制器的输出，Agua 构建了一个基于代理概念的控制器模型，具有两种映射：一种是从控制器的嵌入到预定义的概念空间，另一种是从概念空间到控制器的输出；最后，结果展示 Agua 在网络环境中的几个实际用例——调试意外行为、识别分布变化、设计基于概念的策略以进行有效的再训练，以及增强特定于环境的数据集。
  - 相较现有方法主要识别最有影响力的输入特征，迫使操作员对低级信号（例如缓冲区 t−1、块大小 t+2）进行广泛的手动分析，核心创新是Agua 是一个可解释性框架，它使用人类可理解的高级概念（例如“不稳定的网络条件”）来解释模型的决策；研究团队基于概念的可解释性框架为智能网络系统奠定了基础，使操作员能够与数据驱动的系统进行交互。
  - 网络测量、诊断与可观测性、Full Paper、Congestion Control、Video/QoE、AI for SysNet

- [Intent-Driven Network Management with Multi-Agent LLMs: The Confucius Framework](https://dl.acm.org/doi/10.1145/3718958.3750537)
  - Zhaodong Wang, Samuel Lin, Guanqing Yan (Meta); Soudeh Ghorbani (Johns Hopkins University & Meta); Minlan Yu (Harvard University); Jiawei Zhou (Stony Brook University); Nathan Hu, Lopa Baruah, Sam Peters, Srikanth Kamath, Jerry Yang, Ying Zhang (Meta)
  - Confucius 面向超大规模网络运维，把一次 intent 拆成 DAG 形式的管理步骤；多个 LLM Agent 读取检索增强的长期记忆和人工/模型交互原语，调用 Meta 既有管理工具，并在关键操作前接入现有网络验证与自有回归检查。框架已运行两年、接入 60 多个应用，重点不是一次性生成命令，而是让规划、工具执行和验证进入同一生产流程。
  - 相较只让单个 LLM 回答运维问题，核心创新是把 DAG 规划、多 Agent 协作、RAG 记忆、真实工具和防回归验证组合成可上线的网络管理闭环。
  - 网络验证、管理与安全、Full Paper、Agent for Systems、LLM Systems

- [Hermes: Enhancing Layer-7 Cloud Load Balancers with Userspace-Directed I/O Event Notification](https://dl.acm.org/doi/10.1145/3718958.3750469)
  - Tian Pan, Enge Song, Yueshang Zuo, Shaokai Zhang, Yang Song, Jiangu Zhao, Wengang Hou, Jianyuan Lu, Xiaoqing Sun, Shize Zhang, Ye Yang (Alibaba Cloud); Jiao Zhang, Tao Huang (Purple Mountain Laboratories); Biao Lyu, Xing Li (Zhejiang University and Alibaba Cloud); Rong Wen, Zhigang Zong (Alibaba Cloud); Shunmin Zhu (Hangzhou Feitian Cloud and Alibaba Cloud)
  - 第 7 层负载均衡器 (L7 LB) 可提高公共云中的服务性能、可用性和可扩展性；他们使用 Linux epoll 等 I/O 事件通知工具将连接从内核分派到用户空间 worker；Reuseport (Linux 3.9) 在 worker 之间均匀分配流量，但容易发生哈希冲突，并且不知道 worker 不可用。Hermes 是一个用户空间定向的 I/O 事件通知框架，用于增强 L7 LB；Hermes 将用户空间工作者状态视为一等公民，并使用它通过闭环指导内核空间连接调度；具体来说，研究团队为工作状态读取/更新以及从用户空间到内核的调度决策同步实现了无锁并发管理；在内核中，研究团队利用 eBPF 以非侵入方式覆盖重用端口套接字选择，以进行工作调度；CPU 核心负载均衡显著提升，日均 Worker 挂起率下降 99.8%。
  - 相较Reuseport (Linux 3.9) 在 worker 之间均匀分配流量，但容易发生哈希冲突，并且不知道 worker 不可用，核心创新是Hermes 是一个用户空间定向的 I/O 事件通知框架，用于增强 L7 LB；Hermes 将用户空间工作者状态视为一等公民，并使用它通过闭环指导内核空间连接调度。
  - 数据中心网络、传输与互连、Full Paper、Scheduling/Orchestration、Datacenter Networking

- [CEIO: A Cache-Efficient Network I/O Architecture for NIC-CPU Data Paths](https://dl.acm.org/doi/10.1145/3718958.3750488)
  - Bowen Liu, Xinyang HUANG, Qijing LI (Hong Kong University of Science and Technology); Zhuobin Huang (University of Electronic Science and Technology of China); Yijun Sun, Wenxue Li, Junxue Zhang (Hong Kong University of Science and Technology); Ping Yin (Inspur); Kai Chen (Hong Kong University of Science and Technology)
  - NIC 和 CPU/DRAM 之间的高效输入/输出 (I/O) 数据路径对于支持具有高性能网络传输的数据中心应用至关重要，尤其是当链路速度扩展到 100Gbps 及以上时；传统的 I/O 加速策略，例如数据直接 I/O (DDIO) 和远程直接内存访问 (RDMA)，由于末级缓存 (LLC) 的利用率低下，性能不佳。CEIO 是一种新颖的高速缓存高效网络 I/O 架构，它采用主动速率控制和弹性缓冲来实现 I/O 数据路径中的零 LLC 缺失，同时确保 DDIO 和 RDMA 在各种网络条件下的有效性；研究团队在商用 SmartNIC 上实施了 CEIO，并将其纳入广泛使用的 DPDK 和 RDMA 库中；在实际工作负载下使用经过良好优化的 RPC 框架和分布式文件系统进行的实验表明，与之前的工作相比，CEIO 的吞吐量提高了 2.9×，P99.9 延迟降低了 1.9×。
  - 相较传统的 I/O 加速策略，例如数据直接 I/O (DDIO) 和远程直接内存访问 (RDMA)，由于末级缓存 (LLC) 的利用率低下，性能不佳，核心创新是CEIO 是一种新颖的高速缓存高效网络 I/O 架构，它采用主动速率控制和弹性缓冲来实现 I/O 数据路径中的零 LLC 缺失，同时确保 DDIO 和 RDMA 在各种网络条件下的有效性。
  - 数据中心网络、传输与互连、Full Paper、RDMA、SmartNIC/DPU、Congestion Control、Caching/CDN

- [Centralium: A Hybrid Route-Planning Framework for Large-Scale Data Center Network Migrations](https://dl.acm.org/doi/10.1145/3718958.3750519)
  - Yikai Lin, Mohab Gawish, Shih-Hao Tseng (Meta); Lixin Gao (UMass); Cen Zhao, John Tracey, Sunyi Shao, Hyojeong Kim, Ying Zhang (Meta)
  - 由于 BGP 的可扩展性和简单性，Meta 的数据中心网络依赖 BGP 进行路由和互连；然而，随着网络的发展，BGP 在支持复杂网络迁移方面的局限性变得越来越明显；为了应对这一挑战，该工作设计一种新颖的路由规划抽象 (RPA)，它增强了 BGP 协议以支持迁移。它可以实现集中式路线规划，同时保持分布式执行；研究团队在大型数据中心与 BGP 一起部署 Centralium 的生产经验表明，网络迁移操作的时间和风险大幅减少。
  - 相较随着网络的发展，BGP 在支持复杂网络迁移方面的局限性变得越来越明显，核心创新是该工作设计一种新颖的路由规划抽象 (RPA)，它增强了 BGP 协议以支持迁移；它可以实现集中式路线规划，同时保持分布式执行。
  - 数据中心网络、传输与互连、Full Paper、Internet Routing、Datacenter Networking

- [ZENITH: Towards A Formally Verified Highly-Available Control Plane](https://dl.acm.org/doi/10.1145/3718958.3750533)
  - Pooria Namyar, Arvin Ghavidel (University of Southern California); Mingyang Zhang (Google); Harsha V. Madhyastha, Srivatsan Ravi, Chao Wang, Ramesh Govindan (University of Southern California)
  - 如今，大规模软件定义网络使用基于微服务的控制器；这些控制器中的错误可能会导致数据平面状态与高层意图不一致，从而降低网络可用性；然而，定期协调会限制大规模网络的可用性和性能。该工作设计 Zenith，这是一种基于微服务的控制器，它通过设计避免不一致，而不是始终依赖恢复机制；研究团队已经正式验证了 Zenith 的规范，并证明它可以确保网络状态最终与意图一致；研究团队根据 Zenith 的规范自动生成代码，以最大程度地减少最终实现中出现错误的可能性；Zenith 的保证和抽象还使开发人员能够独立验证 SDN 应用程序并确保端到端的安全性和正确性；Zenith 解决不一致问题的速度比当今的设计快 5 倍，并显著提高了可用性。
  - 相较定期协调会限制大规模网络的可用性和性能，核心创新是该工作设计 Zenith，这是一种基于微服务的控制器，它通过设计避免不一致，而不是始终依赖恢复机制；研究团队已经正式验证了 Zenith 的规范，并证明它可以确保网络状态最终与意图一致。
  - 数据中心网络、传输与互连、Full Paper、Formal Verification、Cloud/Distributed Systems、Datacenter Networking

- [Firefly: Scalable, Ultra-Accurate Clock Synchronization for Datacenters](https://dl.acm.org/doi/10.1145/3718958.3750502)
  - Pooria Namyar (USC & Google LLC); Yuliang Li, Weitao Wang, Nandita Dukkipati, KK Yap, Junzhi Gong, Chen Chen, Peixuan Gao (Google LLC); Devdeep Ray (NVIDIA); Gautam Kumar, Yidan Ma (Google LLC); Ramesh Govindan (USC & Google LLC); Amin Vahdat (Google LLC)
  - 基于云的金融交易需要低于 10nsns 的设备间时钟同步精度，同时遵守协调世界时 (UTC)；现有的时钟同步技术难以大规模满足这一需求，并且容易受到时钟漂移、抖动和路径不对称的影响。Firefly 是一种软件驱动的数据中心时钟同步系统，可扩展、经济高效且可靠地实现非常高的时钟同步精度；它在随机覆盖图上采用分布式共识算法，以快速收敛到公共时间，同时对设备硬件时钟进行逐步调整；为了实现跨设备一致的同步到 UTC（外部同步），同时保持稳定的设备间内部同步，Firefly 使用了一种新颖的技术，即分层同步，该技术可解耦内部和外部同步；在 248 台机器的 Clos 网络中，Firefly 实现了低于 10nsns 的设备到设备和≤1μs 的设备到 UTC 同步，并且能够适应时间服务器故障和不稳定的时钟。
  - 相较现有的时钟同步技术难以大规模满足这一需求，并且容易受到时钟漂移、抖动和路径不对称的影响，核心创新是Firefly 是一种软件驱动的数据中心时钟同步系统，可扩展、经济高效且可靠地实现非常高的时钟同步精度；它在随机覆盖图上采用分布式共识算法，以快速收敛到公共时间，同时对设备硬件时钟进行逐步调整。
  - 数据中心网络、传输与互连、Full Paper、Datacenter Networking

- [Alibaba Stellar: A New Generation RDMA Network for Cloud AI](https://dl.acm.org/doi/10.1145/3718958.3750539)
  - Jie Lu, Jiaqi Gao, Fei Feng, Zhiqiang He, Menglei Zheng, Kun Liu, Jun He, Binbin Liao, Suwei Xu, Ke Sun, Yongjia Mo, Qinghua Peng, Jilie Luo, Qingxu Li, Gang Lu, Zishu Wang, Jianbo Dong, Kunling He, Sheng Cheng, Jiamin Cao, Hairong Jiao, Pengcheng Zhang, Shu Ma, Lingjun Zhu, Chao Shi, Yangming Zhang, Yiquan Chen, Wei Wang, Shuhong Zhu, Xingru Li, Qiang Wang, Jiang Liu, Chao Wang, Wei Lin, Ennan Zhai, Jiesheng Wu, Qiang Liu, Binzhang Fu, Dennis Cai (Alibaba Cloud)
  - 云环境中大型语言模型 (LLM) 的快速采用加剧了对高性能人工智能训练和推理的需求，其中远程直接内存访问 (RDMA) 发挥着关键作用；然而，现有的 RDMA 虚拟化解决方案，例如单根输入/输出虚拟化 (SR-IOV)，在可扩展性、性能和稳定性方面面临重大限制；为了应对这些挑战，该工作设计 Stellar，一种用于云 AI 的新一代 RDMA 网络。Stellar 推出了三项关键创新：用于按需内存固定的半虚拟化直接内存访问 (PVDMA)、用于优化 GPU 直接 RDMA (GDR) 性能的扩展内存转换表 (eMTT) 以及用于高效多路径利用的 RDMA 数据包喷射；评估表明，Stellar 的性能显著优于现有解决方案，为云 AI 提供可扩展、稳定且高性能的 RDMA 网络。
  - 相较现有的 RDMA 虚拟化解决方案，例如单根输入/输出虚拟化 (SR-IOV)，在可扩展性、性能和稳定性方面面临重大限制，核心创新是该工作设计 Stellar，一种用于云 AI 的新一代 RDMA 网络；Stellar 推出了三项关键创新：用于按需内存固定的半虚拟化直接内存访问 (PVDMA)、用于优化 GPU 直接 RDMA (GDR) 性能的扩展内存转换表。
  - 数据中心网络、传输与互连、Full Paper、LLM Systems、RDMA、Cloud/Distributed Systems

- [Coflow Scheduling for LLM Training](https://dl.acm.org/doi/10.1145/3718958.3750467)
  - Xinchen Wan, Xinyu Yang, Kaiqiang Xu, Xudong Liao (Hong Kong University of Science and Technology); Yilun Jin (The Hong Kong University of Science and Technology); Yijun Sun, Zhenghang Ren (Hong Kong University of Science and Technology); Han Tian (The University of Science and Technology of China); Kai Chen (Hong Kong University of Science and Technology)
  - 训练大型语言模型 (LLM) 在集群内生成不同的协同流，需要优化调度来增强通信计算重叠并最大限度地减少训练时间；现有的调度程序无法充分处理协同流之间和内部的争用，从而导致性能不佳。该工作设计 Hermod，一个综合的协流调度程序，可以协调 LLM 训练的所有协流类型；Hermod 背后的关键见解是，协同流可以通过三个模型因素（微批次 ID、协同流类型和层 ID）进行独特表征，从而实现最佳调度决策；利用这种洞察力，Hermod 应用与 LLM 训练 DAG 一致的模型因子驱动的协流间优先级调度；初步模拟结果显示了性能改进的潜力。
  - 相较现有的调度程序无法充分处理协同流之间和内部的争用，从而导致性能不佳，核心创新是该工作设计 Hermod，一个综合的协流调度程序，可以协调 LLM 训练的所有协流类型；Hermod 背后的关键见解是，协同流可以通过三个模型因素（微批次 ID、协同流类型和层 ID）进行独特表征，从而实现最佳调度决策。
  - AI 集群网络与大模型系统、Short Paper、LLM Systems、Scheduling/Orchestration

- [HardMesh: Enabling High-performance Service Mesh Ingress Processing with SmartNICs](https://dl.acm.org/doi/10.1145/3718958.3750471)
  - Myoungsung You (University of Seoul); Jaehyun Nam (Dankook University); Minjae Seo (ETRI); Taejune Park (Chonnam National University); Seungwon Shin (KAIST)
  - 服务网格对于在云环境中实现微服务通信至关重要；然而，它们也带来了大量的网络开销；特别是，作为外部流量主要入口点的入口网关，由于 CPU 密集型流量分析和通过多个网络堆栈层的长时间转发路径，已成为主要性能瓶颈。为此，HardMesh 是一种硬件软件混合入口网关，利用 SmartNIC 进行高性能流量分析和高效的外部流量路由；这个过程通过基于 CPU 的轻量级流量管理代理得到增强；实验结果表明，HardMesh 的性能优于现有入口网关，在提供相同范围的流量管理服务的同时，吞吐量提高了 4.4×。
  - 相较特别是，作为外部流量主要入口点的入口网关，由于 CPU 密集型流量分析和通过多个网络堆栈层的长时间转发路径，已成为主要性能瓶颈，核心创新是为此，HardMesh 是一种硬件软件混合入口网关，利用 SmartNIC 进行高性能流量分析和高效的外部流量路由；这个过程通过基于 CPU 的轻量级流量管理代理得到增强。
  - 可编程数据平面与云网络、Short Paper、SmartNIC/DPU、Internet Routing、Cloud/Distributed Systems

- [SpliDT: Partitioned Decision Trees for Scalable Stateful Inference at Line Rate](https://dl.acm.org/doi/10.1145/3718958.3750475)
  - Murayyiam Parvez (Purdue University); Annus Zulfiqar (University of Michigan); Roman Beltiukov (University of California, Santa Barbara); Shir Landau Feibish (Open University of Israel); Walter Willinger (NIKSUN, Inc.); Arpit Gupta (University of California, Santa Barbara); Muhammad Shahbaz (University of Michigan)
  - 机器学习越来越多地应用于可编程数据平面，例如交换机和智能网卡，以实现线速实时流量分析和安全监控；决策树 (DT) 由于其可解释性以及与可重新配置匹配操作表 (RMT) 架构的兼容性，特别适合这些任务；然而，当前的 DT 实现需要预先收集所有特征，由于数据平面资源有限，这限制了可扩展性和准确性。SpliDT 是一个可扩展的框架，它将 DT 部署重新想象为数据包滑动窗口上的分区推理问题（图 1）；通过将推理划分为顺序子树（每个子树使用自己的一组 top-k 特征），SpliDT 支持更多有状态特征，而不会超出硬件限制；通过数据包再循环实现的带内控制通道管理子树之间的转换并跨分区重用匹配密钥和寄存器；这种设计允许有效地共享物理资源，同时保持线速处理；评估表明，SpliDT 支持多达 5 倍的功能，可扩展到数百万个流，并且性能优于基线，且开销较低，检测时间 (TTD) 最短。
  - 相较当前的 DT 实现需要预先收集所有特征，由于数据平面资源有限，这限制了可扩展性和准确性，核心创新是SpliDT 是一个可扩展的框架，它将 DT 部署重新想象为数据包滑动窗口上的分区推理问题（图 1）；通过将推理划分为顺序子树（每个子树使用自己的一组 top-k 特征），SpliDT 支持更多有状态特征，而不会超出硬件限制。
  - 可编程数据平面与云网络、Short Paper、SmartNIC/DPU、Programmable Network Hardware、Security/Privacy、Scheduling/Orchestration

- [Carbon- and Precedence-Aware Scheduling for Data Processing Clusters](https://dl.acm.org/doi/10.1145/3718958.3750478)
  - Adam Lechowicz (University of Massachusetts Amherst); Rohan Shenoy (University of California Berkeley); Noman Bashir (Massachusetts Institute of Technology); Mohammad Hajiesmaili (University of Massachusetts Amherst); Adam Wierman (California Institute of Technology); Christina Delimitrou (Massachusetts Institute of Technology)
  - 该工作面向带 DAG 依赖的数据处理作业：调度器同时观测任务前驱关系、资源需求和随时间变化的电网碳强度，避免把上游关键任务延迟到低碳时段后反而阻塞整条临界路径。100 节点 Kubernetes 原型在总效率受控时最高减少 32.9% 碳排。
  - 相较假设每个任务可独立延后的碳感知调度，核心创新是把作业前驱约束和碳强度联合纳入调度决策。
  - 分布式系统与网络服务、Short Paper、Scheduling/Orchestration、Shorts

- [HACK: Homomorphic Acceleration via Compression of the Key-Value Cache for Disaggregated LLM Inference](https://dl.acm.org/doi/10.1145/3718958.3750481)
  - Zeyu Zhang, Haiying Shen (University of Virginia); Shay Vargaftik (VMware Research); Ran Ben Basat (University College London); Michael Mitzenmacher, Minlan Yu (Harvard University)
  - 解耦式大语言模型 (LLM) 推理将计算密集型预填充阶段与内存密集型解码阶段解耦，允许使用低端、以计算为重点的 GPU 进行预填充，使用高端、内存丰富的 GPU 进行解码，从而在保持高吞吐量的同时降低成本；然而，在两个阶段之间传输键值（KV）数据可能是一个瓶颈，特别是对于长提示；现有的 KV 量化方法可以缓解传输和内存瓶颈，但它们引入了显著的反量化开销，从而加剧了计算时间。该工作设计通过压缩 KV 缓存的同态加速 (HACK) 来进行解耦式 LLM 推理；HACK 消除了繁重的 KV 反量化，直接对量化的 KV 数据进行计算以近似并减少昂贵的矩阵乘法的成本；大量的跟踪驱动实验表明，与解耦式 LLM 推理基线相比，HACK 将 JCT 减少了高达 70.9%，与最先进的 KV 量化方法相比，减少了高达 52.3%。
  - 相较现有的 KV 量化方法可以缓解传输和内存瓶颈，但它们引入了显著的反量化开销，从而加剧了计算时间，核心创新是该工作设计通过压缩 KV 缓存的同态加速 (HACK) 来进行解耦式 LLM 推理；HACK 消除了繁重的 KV 反量化，直接对量化的 KV 数据进行计算以近似并减少昂贵的矩阵乘法的成本。
  - AI 集群网络与大模型系统、Short Paper、LLM Systems、KV Cache、Caching/CDN、Compression/Encoding

- [Designing Transport-Level Encryption for Datacenter Networks](https://dl.acm.org/doi/10.1145/3718958.3750482)
  - Tianyi Gao, Xinshu Ma, Suhas Narreddy, Eugenio Luo, Steven Chien, Michio Honda (University of Edinburgh)
  - 该工作设计 SDP，这是一种针对新兴数据中心传输（例如 NDP 和 Homa）的协议设计，用于集成数据加密。它支持专为 TCP 上的 TLS 设计的 NIC 卸载、TCP 和 UDP 的本机协议号以及基于消息的抽象，可实现具有细粒度并行性的低延迟 RPC。
  - 官方摘要未展开更细的直接基线；可核验的核心创新是该工作设计 SDP，这是一种针对新兴数据中心传输（例如 NDP 和 Homa）的协议设计，用于集成数据加密；它支持专为 TCP 上的 TLS 设计的 NIC 卸载、TCP 和 UDP 的本机协议号以及基于消息的抽象。
  - 网络验证、管理与安全、Short Paper、Security/Privacy

- [ZooRoute: Enhancing Cloud-Scale Network Reliability via Overlay Proactive Rerouting](https://dl.acm.org/doi/10.1145/3718958.3750483)
  - Xiaoqing Sun, Xionglie Wei (Alibaba Cloud); Xing Li (Zhejiang University and Alibaba Cloud); Ju Zhang, Bowen Yang, Yi Wang, Ye Yang, Yu Qi, Le Yu, Chenhao Jia, Zhanlong Zhang, Xinyu Chen, Jianyuan Lu, Shize Zhang, Enge Song, Yang Song, Tian Pan, Rong Wen, Biao Lyu (Alibaba Cloud); Yang Xu (Fudan University); Shunmin Zhu (Hangzhou Feitian Cloud and Alibaba Cloud)
  - ZooRoute 是一种对租户透明的快速故障恢复服务，无需修改物理设备。ZooRoute 利用覆盖层，通过在封装期间更改数据包 header 中的源端口 (srcPorts) 来使流量绕过故障；ZooRoute 在阿里云部署 18 个月，网络可靠性显著提升，累计宕机时间减少 92.71%。
  - 官方摘要未展开更细的直接基线；可核验的核心创新是ZooRoute 是一种对租户透明的快速故障恢复服务，无需修改物理设备；ZooRoute 利用覆盖层，通过在封装期间更改数据包 header 中的源端口 (srcPorts) 来使流量绕过故障。
  - 互联网架构、路由与流量控制、Short Paper、Network Measurement/Telemetry、Wireless/Sensing、Internet Routing、Compression/Encoding

- [Achieving High-Speed and Robust Encrypted Traffic Anomaly Detection with Programmable Switches](https://dl.acm.org/doi/10.1145/3718958.3750493)
  - Han Zhang (Tsinghua University); Guyue Liu (Peking University); Xingang Shi (Tsinghua University); Yahui Li (Tsinghua University,China); Dongbiao He (Sangfor Technologies Inc); Jilong Wang, Zhiliang Wang (Tsinghua University); Yongqing Zhu, Ke Ruan, Weihua Cao (China telecom); Xia Yin (Tsinghua University)
  - 由于应用程序的快速扩展，针对数据中心的攻击变得越来越普遍；为了跟上连接到网络的数据中心数量不断增长的步伐，互联网服务提供商必须提供全面的安全服务；然而，现有的网络入侵检测系统（NIDS）对于高速加密网络流量要么无效要么效率低下。该工作设计并实现了 Mazu，这是一种带有可编程交换机的内联网络入侵检测系统，专门用于保护连接到互联网服务提供商的数据中心；Mazu 提出了一种双平面特征提取模型，以近线速度提取广泛的交通特征；Mazu 还提出了一种轻量级的一类解耦式模型，专门针对良性流量训练最佳参数，以识别恶意流量；此外，Mazu 还引入了在线更新机制，旨在根据环境变化动态调整检测模型；生产与测试平台评估表明，Mazu 可以在几分钟内检测进入数据中心站点的恶意流量，准确率约为 90%。
  - 相较现有的网络入侵检测系统（NIDS）对于高速加密网络流量要么无效要么效率低下，核心创新是该工作设计并实现了 Mazu，这是一种带有可编程交换机的内联网络入侵检测系统，专门用于保护连接到互联网服务提供商的数据中心；Mazu 提出了一种双平面特征提取模型，以近线速度提取广泛的交通特征。
  - 网络验证、管理与安全、Short Paper、Programmable Network Hardware、Failure Diagnosis、Security/Privacy

- [Palladium: A DPU-enabled Multi-Tenant Serverless Cloud over Zero-copy Multi-node RDMA Fabrics](https://dl.acm.org/doi/10.1145/3718958.3750494)
  - Shixiong Qi (University of Kentucky); Songyu Zhang, K. K. Ramakrishnan (University of California, Riverside); Diman Zad Tootaghaj, Hardik Soni, Puneet Sharma (Hewlett Packard Labs)
  - 无服务器计算提供了资源效率，但受到重量级数据平面的影响。Palladium 是一种 DPU 卸载的无服务器数据平面，支持分布式零拷贝通信；Palladium 使用两侧 RDMA 和跨处理器共享内存来缓解弱 DPU 内核的限制；其支持 DPU 的网络引擎 (DNE) 可隔离 RDMA 资源并管理跨租户的流量；通过在入口处将 HTTP/TCP 转换为 RDMA，Palladium 减少了关键路径上的协议开销。
  - 相较无服务器计算提供了资源效率，但受到重量级数据平面的影响，核心创新是Palladium 是一种 DPU 卸载的无服务器数据平面，支持分布式零拷贝通信；Palladium 使用两侧 RDMA 和跨处理器共享内存来缓解弱 DPU 内核的限制。
  - 可编程数据平面与云网络、Short Paper、RDMA、SmartNIC/DPU、Cloud/Distributed Systems

- [Threading the Ocean: Mapping Digital Routes Across Submarine Cables using Calypso](https://dl.acm.org/doi/10.1145/3718958.3750512)
  - Caleb Wang, Ying Zhang, Esteban Carisimo, Fabián E. Bustamante (Northwestern University); Ram Durairajan (University of Oregon); Qianli Dong (Northwestern University)
  - 海底电缆网络（SCN）——全球互联网连接的支柱——面临着日益严重的威胁，带来严重的经济和安全影响；增强其弹性需要更深入地了解特定电缆和着陆点的重要性，而这又取决于准确地将流量映射到电缆，以识别漏洞并评估其对区域和全球连接的影响；然而，由于缺乏评估 SCN 重要性的稳健框架，研究人员和政策制定者缺乏切实可行的见解来保护这一重要基础设施。该工作设计 Calypso（一种将跟踪路由映射到其所穿越的海底电缆的新颖框架）以及路由压力（一种通过实验推断的指标，可使用跟踪路由数据来估计海底电缆基础设施的相对重要性）；Calypso 解决了海底电缆行业的不透明性以及将网络层路径映射到物理基础设施的复杂性所带来的关键挑战；通过严格的验证和案例研究，结果展示 Calypso 在评估 SCN 漏洞方面的功效，并强调其为增强全球潜艇基础设施的弹性提供见解的潜力。
  - 相较由于缺乏评估 SCN 重要性的稳健框架，研究人员和政策制定者缺乏切实可行的见解来保护这一重要基础设施，核心创新是该工作设计 Calypso（一种将跟踪路由映射到其所穿越的海底电缆的新颖框架）以及路由压力（一种通过实验推断的指标，可使用跟踪路由数据来估计海底电缆基础设施的相对重要性）。
  - 卫星、海洋与非地面网络、Short Paper、Security/Privacy、Underwater/Submarine Network

- [AoRA: AI-on-RAN for Backhaul-free Edge Inference](https://dl.acm.org/doi/10.1145/3718958.3750517)
  - Siyavushkhon Kholmatov (Korea Advanced Institute of Science and Technology); Seongsik Cho (Seoul National University); Song Chong (Korea Advanced Institute of Science and Technology); Kyunghan Lee (Seoul National University)
  - 在蜂窝网络中，边缘智能通常由多接入边缘计算（MEC）实现，旨在让人工智能服务更接近最终用户；尽管 MEC 通过将计算放置在网络边缘附近来减少延迟，但它仍然位于无线接入网络 (RAN) 及其本机执行环境的外部，从而引入了额外的传输和缓冲延迟；新兴的 AI-on-RAN 范式旨在克服这些限制，但主要仍处于概念性阶段，缺乏实际实施和可行性验证。AoRA 是第一个实现 AI-on-RAN 愿景的框架，通过动态利用 GPU 和 NPU 加速的 RAN 平台中的可用计算空间，直接从基站内提供 AI 服务；AoRA 利用 5G RAN 堆栈中的容器化 AI 工作负载来实现内联和机会性 AI 服务配置，而不会降低核心电信运营的性能；该框架完全符合 O-RAN 接口，可以与现有边缘计算基础设施无缝运行；评估表明，与 MEC 相比，AoRA 的传输延迟降低了 30% 以上，与基于云的设置相比，传输延迟降低了 70%。
  - 相较新兴的 AI-on-RAN 范式旨在克服这些限制，但主要仍处于概念性阶段，缺乏实际实施和可行性验证，核心创新是AoRA 是第一个实现 AI-on-RAN 愿景的框架，通过动态利用 GPU 和 NPU 加速的 RAN 平台中的可用计算空间，直接从基站内提供 AI 服务。
  - 无线、蜂窝与感知、Short Paper、Cellular/RAN、Cloud/Distributed Systems

- [NIER: Practical Neural-enhanced Low-bitrate Video Conferencing](https://dl.acm.org/doi/10.1145/3718958.3750518)
  - Anlan Zhang (University of Southern California); Yuming Hu (University of Minnesota Twin Cities); Chendong Wang (University of Wisconsin Madison); Yu Liu, Zejun Zhang (University of Southern California); Haoyu Gong (University of Minnesota, Twin Cities); Ahmad Hassan (University of Southern California); Shichang Xu (Google); Zhenhua Li (Tsinghua University); Bo Han (George Mason University); Feng Qian (University of Southern California)
  - NIER 是一种实用的低比特率视频会议解决方案。它可以自适应地保持低比特率（例如 10-100 Kbps）和合理的视觉质量，同时对数据包丢失具有鲁棒性；满足这些设计要求使 NIER 适用于各种使用场景，特别是在具有挑战性/计量的网络上；在底层，NIER 利用基于关键点的深度图像动画 (DIA) 作为关键构建块，其中发送器将稀疏关键点与参考图像一起传输，而接收器则通过使用关键点的运动对参考图像进行动画处理来重建原始视频帧；其广泛评估（包括 IRB 批准的涉及 20 名参与者的用户研究）表明，NIER 在端到端延迟、可解码帧比、帧速率、视频质量和/或用户体验方面明显优于多种基准解决方案（传统视频编解码器、超分辨率增强视频会议、前向纠错编码 (FEC)、丢失弹性神经编解码器和基于关。
  - 官方摘要未展开更细的直接基线；可核验的核心创新是NIER 是一种实用的低比特率视频会议解决方案；它可以自适应地保持低比特率（例如 10-100 Kbps）和合理的视觉质量，同时对数据包丢失具有鲁棒性；满足这些设计要求使 NIER 适用于各种使用场景，特别是在具有挑战性/计量的网络上。
  - 视频、实时通信与 QoE、Short Paper、Video/QoE

- [Discovering Millions of New Nodes and Links in the Internet by Challenging the Uniformity Assumption in Multipath Detection](https://dl.acm.org/doi/10.1145/3718958.3750534)
  - Zhongxu Guan (Tsinghua University); Shuai Wang, Li Chen, Zhaoteng Yan (Zhongguancun Laboratory); Jiaye Lin, Dan Li (Tsinghua University); Yong Jiang (Tsinghua Shenzhen International Graduate School); Yingxin Wang, Ziqian Liu (China Telecom Cybersecurity Technology Co.,Ltd.)
  - 多路径检测算法（MDA）被提出来发现负载平衡（LB）下的互联网拓扑；现有方法假设负载均衡响应（LBR）的一致性，即来自 LB 路由器后继路由器的响应；该工作设计 BayMuDA，这是一种通过消除均匀性假设来克服这一限制的新颖系统。利用数据包转发的马尔可夫特性，BayMuDA 采用贝叶斯网络将 LBR 分布检索构建为不完整数据的参数估计问题；使用估计的 LBR 分布，BayMuDA 计算统计发现给定跃点内的所有节点和边所需的最小探测次数；在受控拓扑验证中，BayMuDA 在约 90% 的情况下发现至少 85%/73% 的节点/链路；基于综合拓扑，研究观察到互联网路径稳定性有所提高，而多路径拓扑的规模也变得更大。
  - 相较现有方法假设负载均衡响应（LBR）的一致性，即来自 LB 路由器后继路由器的响应，核心创新是该工作设计 BayMuDA，这是一种通过消除均匀性假设来克服这一限制的新颖系统；利用数据包转发的马尔可夫特性，BayMuDA 采用贝叶斯网络将 LBR 分布检索构建为不完整数据的参数估计问题。
  - 网络测量、诊断与可观测性、Short Paper、Network Measurement/Telemetry

- [Wisely Optimizing Short Video Streaming for a User-Vendor Win-Win Outcome](https://dl.acm.org/doi/10.1145/3718958.3754346)
  - Jinlong E (Renmin Univerity of China); Wei Xu, Jianfei Bi (Renmin University of China); Lin He (Tsinghua University); Haoyang Li (Columbia University); Anqi Gu (Renmin University of China); Dan Yang (ByteDance Inc.); Yunpeng Chai (Renmin University of China)
  - 短视频流媒体平台广泛采用视频预取来保证用户的体验质量（QoE），但用户频繁的刷屏会导致大量数据浪费，给厂商带来巨大的经济负担；现有的学术和工业解决方案无法取得平衡，通常会牺牲数据节省或真实的用户感知 QoE。该工作设计一个框架，可以在不影响用户体验的情况下智能地减少流数据消耗；核心思想是使预取决策适应用户滑动行为和动态网络条件；现实世界的评估表明，其框架在数据浪费以及用户感知的 QoE 方面显著优于最先进的解决方案。
  - 相较现有的学术和工业解决方案无法取得平衡，通常会牺牲数据节省或真实的用户感知 QoE，核心创新是该工作设计一个框架，可以在不影响用户体验的情况下智能地减少流数据消耗；核心思想是使预取决策适应用户滑动行为和动态网络条件。
  - 视频、实时通信与 QoE、Short Paper、Video/QoE

- [DNSLogzip: A Novel Approach to Fast and High-Ratio Compression for DNS Logs](https://dl.acm.org/doi/10.1145/3718958.3750476)
  - Yunwei Dai (Southeast University; Jiangsu Future Networks Innovation Institute); Guyue Liu (Peking University); Tao Huang (Southeast University; State Key Laboratory of Networking and Switching Technology, BUPT, China; Purple Mountain Laboratories); Shuo Wang (State Key Laboratory of Networking and Switching Technology, BUPT, China; Purple Mountain Laboratories); Yong Wang, Xingli Wu (Jiangsu Zhiwang Technology Co., Ltd.); Lei Song, Heshun Li, Chuang Wang (China Mobile Communications Group Shandong Co., Ltd.); Fanglong Hu (China Telecom Co., Ltd.); Hong Sun, Yanan Li (China United Network Communications Corporation Jiangsu Branch)
  - 域名系统 (DNS) 日志捕获 DNS 服务器和客户端之间交换的查询和响应的详细记录，在网络安全监控和法规遵从性等通常需要长期数据保留的应用中发挥着至关重要的作用；随着互联网流量的快速增长，DNS 日志量激增，给存储带来了巨大的挑战；尽管许多 DNS 运营商使用通用压缩算法来降低存储成本，但这些解决方案未能充分利用 DNS 数据的独特特征，导致效率低下和存储需求不断上升。该工作设计一种新颖的解决方案 DNSLogzip，旨在实现 DNS 日志的无损、快速和高比率压缩；基于对现实世界 DNS 日志数据集的深入实证研究，研究确定了四个关键的行间和行内特征，这些特征能够有效减少冗余而不丢失信息；DNSLogzip 通过模块化压缩架构利用这些见解，使其能够处理不同的日志格式，并根据特定要求提供轻松的集成和定制；结果显示，DNSLogzip 可以将存储成本降低约三分之二，每个 DNS 服务节点每月可能节省高达 163,000 美元。
  - 相较尽管许多 DNS 运营商使用通用压缩算法来降低存储成本，但这些解决方案未能充分利用 DNS 数据的独特特征，导致效率低下和存储需求不断上升，核心创新是该工作设计一种新颖的解决方案 DNSLogzip，旨在实现 DNS 日志的无损、快速和高比率压缩；基于对现实世界 DNS 日志数据集的深入实证研究，研究确定了四个关键的行间和行内特征，这些特征能够有效减少冗余而不丢失信息。
  - 网络测量、诊断与可观测性、Full Paper、Security/Privacy、Compression/Encoding、NetMon

- [Hawkeye: Diagnosing RDMA Network Performance Anomalies with PFC Provenance](https://dl.acm.org/doi/10.1145/3718958.3750490)
  - Shicheng Wang (Tsinghua University); Menghao Zhang (Beihang University); Xiao Li (Tsinghua University); Qiyang Peng (Beihang University); Haoyuan Yu, Zhiliang Wang, Mingwei Xu (Tsinghua University); Xiaohe Hu (Infrawaves); Jiahai Yang, Xingang Shi (Tsinghua University)
  - 由于其显著的性能提升，RDMA 从私有数据中心到公共多租户云变得越来越普遍；然而，其无损流量控制（即 PFC）由于其级联拥塞扩散特性，在网络性能异常（NPA）中引入了新的复杂性，这通常会引起客户/应用程序对某些流量性能下降的抱怨；现有研究缺乏 PFC 影响的细粒度可见性和 PFC 因果关系的可追溯性，因此无法有效诊断 RDMA NPA 的根本原因。Hawkeye 是一种基于 PFC 起源的准确高效的 RDMA NPA 诊断系统；Hawkeye 包括 1) 细粒度 PFC 感知遥测机制，用于记录 PFC 对流量的影响； 2）网内 PFC 因果关系分析和追踪机制，可快速有效地收集因果遥测数据以进行诊断； 3）基于溯源的诊断算法，全面呈现异常故障，准确识别异常类型和根本原因；通过对 NS-3 模拟和 Tofino 测试台进行广泛评估，Hawkeye 可以快速准确地诊断多个 RDMA NPA，其精度超过 90%，开销比基线低 1-4 个数量级。
  - 相较现有研究缺乏 PFC 影响的细粒度可见性和 PFC 因果关系的可追溯性，因此无法有效诊断 RDMA NPA 的根本原因，核心创新是Hawkeye 是一种基于 PFC 起源的准确高效的 RDMA NPA 诊断系统；Hawkeye 包括 1) 细粒度 PFC 感知遥测机制，用于记录 PFC 对流量的影响。
  - 网络测量、诊断与可观测性、Full Paper、RDMA、Network Measurement/Telemetry、Failure Diagnosis

- [Towards LLM-Based Failure Localization in Production-Scale Networks](https://dl.acm.org/doi/10.1145/3718958.3750505)
  - Chenxu Wang (Nanjing University and Alibaba Cloud); Xumiao Zhang (Alibaba Cloud); Runwei Lu (New York University Shanghai and Alibaba Cloud); Xianshang Lin, Xuan Zeng, Xinlei Zhang, Zhe An, Gongwei Wu, Jiaqi Gao (Alibaba Cloud); Chen Tian, Guihai Chen (Nanjing University); Guyue Liu (Peking University); Yuhong Liao, Tao Lin, Dennis Cai, Ennan Zhai (Alibaba Cloud)
  - BIAN 面向生产网络 incident 的设备级根因定位，输入是海量监控数据；LLM 生成疑似故障设备排序及逐项解释，帮助 operator 缩小调查范围。系统已部署 10 个月，并用 17 个月真实案例评估：定位准确率较基线提高 9.2%，总体根因分析时间减少 20.5%，高风险事件减少 55.2%。
  - 相较依赖人工浏览告警或只输出无解释分类结果，核心创新是把监控证据转成带解释的设备级候选排序；它是 LLM 辅助诊断，不是自主修复 Agent。
  - 网络测量、诊断与可观测性、Full Paper、LLM for Systems、LLM Systems、Failure Diagnosis

- [SkyNet: Analyzing Alert Flooding from Severe Network Failures in Large Cloud Infrastructures](https://dl.acm.org/doi/10.1145/3718958.3750536)
  - Bo Yang, Huanwu Hu, Yifan Li, Yunguang Li, Xiangyu Tang, Bingchuan Tian, Gongwei Wu, Jianfeng Xu, Xumiao Zhang, Feng Chen, Cheng Wang, Ennan Zhai, Yuhong Liao, Dennis Cai, Tao Lin (Alibaba Cloud)
  - 对于像研究团队这样运营大规模全球网络的企业来说，网络故障恢复的及时性极大地影响了网络服务的可靠性；理想情况下，网络监控系统应该有足够的覆盖范围来检测即使是很小的问题，但高覆盖范围意味着在严重的网络故障期间警报泛滥；现有的解决方案使用有限的网络监控数据源和启发式诊断规则，缺乏全面的覆盖范围和解决严重故障的能力，尤其是网络运营商以前从未处理过的类似故障。SkyNet 是一个网络分析系统，用于从警报洪水中提取范围和严重性信息；SkyNet 通过统一的输入格式集成多个监控数据源，确保全面覆盖，增强了新网络监控工具的可扩展性；在警报泛滥期间，SkyNet 对警报进行分组、评估其严重性并过滤掉不重要的警报，以帮助网络运营商减轻网络故障；迄今为止，SkyNet 已在其网络上稳定运行了 9 个月，没有出现任何误报，并成功缩短了自部署到生产环境以来超过 80% 的网络故障的缓解时间。
  - 相较现有的解决方案使用有限的网络监控数据源和启发式诊断规则，缺乏全面的覆盖范围和解决严重故障的能力，尤其是网络运营商以前从未处理过的类似故障，核心创新是SkyNet 是一个网络分析系统，用于从警报洪水中提取范围和严重性信息；SkyNet 通过统一的输入格式集成多个监控数据源，确保全面覆盖，增强了新网络监控工具的可扩展性。
  - 网络测量、诊断与可观测性、Full Paper、Failure Diagnosis、NetMon

- [SkeletonHunter: Diagnosing and Localizing Network Failures in Containerized Large Model Training](https://dl.acm.org/doi/10.1145/3718958.3750513)
  - Wei Liu (Tsinghua University and Alibaba Cloud); Kun Qian (Alibaba Cloud); Zhenhua Li (Tsinghua University); Tianyin Xu (University of Illinois Urbana-Champaign); Yunhao Liu (Tsinghua University); Weicheng Wang, Yun Zhang, Jiakang Li, Shuhong Zhu, Xue Li, Hongfei Xu, Fei Feng, Ennan Zhai (Alibaba Cloud)
  - 灵活性、可移植性、隔离性等特点使得容器成为近年来大型模型训练的流行环境；不幸的是，由于容器的高动态性、底层网络和覆盖网络之间复杂的相互作用以及对故障检测和定位的严格要求，这些优势使得对容器化大型模型训练的网络支持变得极具挑战性；现有的数据中心网络调试工具依赖于全面或机会性监控，在这种情况下要么效率低下，要么不准确。SkeletonHunter 是一种容器网络监控和诊断系统，它利用了大型模型训练所产生的网络流量固有的和规律的稀疏性；其关键思想是对流量骨架进行推理，流量骨架由训练流量一致遍历的一组关键网络路径组成，以便在短时间内可靠地检测和定位网络故障；研究团队将其部署在生产环境中六个月，以 98.2% 的准确率和 99.3% 的召回率发现了 4,816 个网络故障，并以 95.7% 的高精度进行了定位。
  - 相较现有的数据中心网络调试工具依赖于全面或机会性监控，在这种情况下要么效率低下，要么不准确，核心创新是SkeletonHunter 是一种容器网络监控和诊断系统，它利用了大型模型训练所产生的网络流量固有的和规律的稀疏性；其关键思想是对流量骨架进行推理，流量骨架由训练流量一致遍历的一组关键网络路径组成，以便在短时间内可靠地检测和定位网络故障。
  - 网络测量、诊断与可观测性、Full Paper、Failure Diagnosis、Cloud/Distributed Systems、NetMon

- [ByteTracker: An Agentless and Real-time Path-aware Network Probing System](https://dl.acm.org/doi/10.1145/3718958.3750515)
  - Shixian Guo (ByteDance China); Kefei Liu (Beijing University of Posts and Telecommunications); Yulin Lai, Yangyang Bai, Ziwei Zhao, Songlin Liu, Jianghang Ning, Gen Li, Jianwei Hu, Yongbin Dong, Feng Luo, Sisi Wen, Qi Zhang, Yuan Chen, Jiale Feng, Yang Bai, Chengcai Yao, Zhe Liu, Xin Hu, Yang Lv, Zhuo Jiang (ByteDance China); Jiao Zhang, Tao Huang (Beijing University of Posts and Telecommunications)
  - 随着数据中心服务器数量增长到数百万台，以及对更准确、更快速、更强大的网络故障检测和定位的需求，现有以 Pingmesh 为中心的监控和诊断系统已经不够高效。ByteTracker 是第一个用于大规模数据中心网络的无代理探测和诊断系统；它不需要在终端主机上部署探测进程或进行任何配置，所有探测均由少数集中式探测器发起；在部署过程中，ByteTracker 可以检测几乎所有网络异常并在 5 秒内定位，准确率 100%。
  - 相较现有以 Pingmesh 为中心的监控和诊断系统已经不够高效，核心创新是ByteTracker 是第一个用于大规模数据中心网络的无代理探测和诊断系统；它不需要在终端主机上部署探测进程或进行任何配置，所有探测均由少数集中式探测器发起。
  - 网络测量、诊断与可观测性、Full Paper、Failure Diagnosis、NetMon

- [MixNet: A Runtime Reconfigurable Optical-Electrical Fabric for Distributed Mixture-of-Experts Training](https://dl.acm.org/doi/10.1145/3718958.3750465)
  - Xudong Liao, Yijun Sun (Hong Kong University of Science and Technology); Han Tian (The University of Science and Technology of China); Xinchen Wan (Hong Kong University of Science and Technology); Yilun Jin (The Hong Kong University of Science and Technology); Zilong Wang, Zhenghang Ren, Xinyang Huang, Wenxue Li (Hong Kong University of Science and Technology); Kin Fai Tse (ITSC, The Hong Kong University of Science and Technology); Zhizhen Zhong (Massachusetts Institute of Technology); Guyue Liu (Peking University); Ying Zhang (Meta); Xiaofeng Ye (EmbedWay); Yiming Zhang (Xiamen University); Kai Chen (Hong Kong University of Science and Technology)
  - 专家混合 (MoE) 模型通过基于每个代币有选择地激活不同的子网（称为专家），优于传统模型；这种门控计算会生成无法事先确定的动态通信，对分布式训练期间保持静态的现有 GPU 互连提出了挑战。该工作设计创建一种名为 MixNet 的首创系统，该系统可以在分布式 MoE 训练期间解锁拓扑重新配置；为了实现这一愿景，系统首先进行了生产测量研究，结果表明 MoE 动态通信模式具有很强的局部性，减轻了全局重新配置的要求；大规模数据包级仿真表明，MixNet 实现了与非阻塞胖树结构相当的性能，同时在 100 Gbps 和 400 Gbps 链路带宽下，将四种代表性 MoE 模型的网络成本效率（例如，每美元性能）分别提高了 1.2×–1.5× 和 1.9×–2.3×。
  - 相较现有 GPU 互连提出了挑战，核心创新是该工作设计创建一种名为 MixNet 的首创系统，该系统可以在分布式 MoE 训练期间解锁拓扑重新配置；为了实现这一愿景，系统首先进行了生产测量研究，结果表明 MoE 动态通信模式具有很强的局部性，减轻了全局重新配置的要求。
  - AI 集群网络与大模型系统、Full Paper、MoE、Collective Communication、Optical Interconnect、Network Measurement/Telemetry

- [Orderlock: A New Type of Deadlock and its Implications on High Performance Network Protocol Design](https://dl.acm.org/doi/10.1145/3718958.3750497)
  - Weihao Jiang, Wenli Xiao, Yuqing Yang (Shanghai Jiao Tong University); Peirui Cao (Nanjing University); Shizhen Zhao (Shanghai Jiao Tong University)
  - 在设计高性能网络 (HPN) 协议的过程中，有效传输的三个关键特性得到了广泛研究：按序传送、无损传输和乱序能力；然而，还没有任何实际实施能够同时成功实现这三个目标。研究确定并证明这些功能的同时实现构成了一种新型死锁的充分必要条件，研究团队将其称为订单锁；结果表明在有 Orderlock 风险的网络中运行是不切实际的，并通过调整 AI 工作负载性能的案例研究对无 Orderlock 协议进行了全面的探索和比较。
  - 相较还没有任何实际实施能够同时成功实现这三个目标，核心创新是研究确定并证明这些功能的同时实现构成了一种新型死锁的充分必要条件，研究团队将其称为订单锁。
  - AI 集群网络与大模型系统、Full Paper、NetAI

- [MegaScale-Infer: Efficient Mixture-of-Experts Model Serving with Disaggregated Expert Parallelism](https://dl.acm.org/doi/10.1145/3718958.3750506)
  - Ruidong Zhu (School of Computer Science, Peking University); Ziheng Jiang (ByteDance Ltd); Chao Jin (School of Computer Science, Peking University); Peng Wu, Cesar A. Stuardo, Dongyang Wang, Xinlei Zhang, Huaping Zhou, Haoran Wei, Yang Cheng, Jianzhe Xiao, Xinyi Zhang, Lingjun Liu, Haibin Lin, Li-Wen Chang, Jianxi Ye, Xiao Yu (ByteDance Ltd); Xuanzhe Liu, Xin Jin (School of Computer Science, Peking University); Xin Liu (ByteDance Ltd)
  - 专家混合 (MoE) 展示了扩展大型语言模型 (LLM) 的巨大潜力，同时增强了性能并降低了计算复杂性；然而，其稀疏激活的架构在推理过程中将前馈网络 (FFN) 从计算密集型转变为内存密集型，从而导致 GPU 利用率大幅降低并增加运营成本。MegaScale-Infer 是一种高效且经济高效的系统，用于为大规模 MoE 模型提供服务；MegaScale-Infer 将注意力模块和 FFN 模块分解在每个模型层中，从而实现两个模块的独立扩展、定制并行策略和异构部署；为了在 MoE 稀疏性的情况下充分利用分解，MegaScale-Infer 引入了乒乓管道并行性，它将请求批次划分为微批次，并在注意力和 FFN 之间穿梭以进行推理；实验结果表明，MegaScale-Infer 的每 GPU 吞吐量比最先进的解决方案高出 1.9×。
  - 相较其稀疏激活的架构在推理过程中将前馈网络 (FFN) 从计算密集型转变为内存密集型，从而导致 GPU 利用率大幅降低并增加运营成本，核心创新是MegaScale-Infer 是一种高效且经济高效的系统，用于为大规模 MoE 模型提供服务；MegaScale-Infer 将注意力模块和 FFN 模块分解在每个模型层中，从而实现两个模块的独立扩展、定制并行策略和异构部署。
  - AI 集群网络与大模型系统、Full Paper、LLM Systems、MoE、NetAI

- [Astral: A Datacenter Infrastructure for Large Language Model Training at Scale](https://dl.acm.org/doi/10.1145/3718958.3750521)
  - Qingkai Meng, Hao Zheng, Zhenhui Zhang (Nanjing University); ChonLam Lao (Harvard University); Chengyuan Huang (Nanjing University); Baojia Li, Ziyuan Zhu, Hao Lu, Weizhen Dang, Zitong Lin, Weifeng Zhang, Lingfeng Liu, Yuanyuan Gong, Chunzhi He, Xiaoyuan Hu, Yinben Xia, Xiang Li, Zekun He, Yachen Wang, Xianneng Zou (Tencent); Kun Yang (Nanjing University); Gianni Antichi (Politecnico di Milano and Queen Mary University of London); Guihai Chen, Chen Tian (Nanjing University)
  - 大型语言模型（LLM）的蓬勃发展需要越来越大规模的训练；该工作总结研究团队在设计、部署和运营新型 Astral 数据中心基础设施方面的经验，以及从其生产使用中获得的运营经验教训和演变见解。为了物理部署这种高密度基础设施，该工作设计分布式高压直流电源系统和新型气液集成冷却系统；(ii) 具有跨主机和分层日志关联的全栈监控系统，可大规模诊断故障并精确定位根本原因；(iii) 算子粒度预测组件 Seer，能够以可接受的精度高效生成算子执行时间线，有助于故障诊断、模型调整和网络架构升级；Astral 基础设施已在 18 个月内逐步部署，支持多个客户的 LLM 训练和推理。
  - 官方摘要未展开更细的直接基线；可核验的核心创新是为了物理部署这种高密度基础设施，该工作设计分布式高压直流电源系统和新型气液集成冷却系统；(ii) 具有跨主机和分层日志关联的全栈监控系统，可大规模诊断故障并精确定位根本原因。
  - AI 集群网络与大模型系统、Full Paper、LLM Systems、Failure Diagnosis、NetAI

- [SGLB: Scalable and Robust Global Load Balancing in Commodity AI Clusters](https://dl.acm.org/doi/10.1145/3718958.3750527)
  - Chenchen Qi (ByteDance); Wenfei Wu (Peking University); Yongcan Wang (ByteDance); Keqiang He (Shanghai Jiao Tong University); Yu-Hsiang (Sean) Kao (ByteDance); Zongying He (Broadcom); Chen-Yu Yen, Zhuo Jiang, Feng Luo (ByteDance); Surendra Anubolu, Yanjin Gao (Broadcom); Bingfeng Lin, Wenda Ni, Yiming Yang, Donglin Wei, Boyang Zhou, Jian Wang, Shan Ding (ByteDance)
  - 互联网公司正在利用商用以太网交换机构建大规模人工智能集群，用于人工智能模型训练以支持其业务；人工智能训练工作负载提出了严格的网络要求，要求集群网络提供高峰值吞吐量，同时在面临链路故障时保持鲁棒性和弹性。SGLB 是一种用于 AI 集群的分布式全局拥塞感知负载平衡系统；SGLB 运行控制平面协议 SyncMesh，以在现代商用交换机中启用新的负载平衡抽象 — 全局负载平衡 (GLB) 引擎 — 该引擎利用全局拥塞信息在所有可用路径上分配流量；研究团队解决了设计 SGLB 时的三个关键挑战：快速路由收敛以最大限度地减少链路故障时的停机时间、在有限交换机硬件资源的限制下可扩展地维护拥塞配置文件，以及在路径带宽不对称的情况下防止 GLB 吞吐量抑制；研究团队对 SGLB 进行原型设计并进行大量实验来评估 SGLB。
  - 官方摘要未展开更细的直接基线；可核验的核心创新是SGLB 是一种用于 AI 集群的分布式全局拥塞感知负载平衡系统；SGLB 运行控制平面协议 SyncMesh，以在现代商用交换机中启用新的负载平衡抽象 — 全局负载平衡 (GLB) 引擎 — 该引擎利用全局拥塞信息在所有可用路径上分配流量。
  - AI 集群网络与大模型系统、Full Paper、Collective Communication、Network Measurement/Telemetry、Internet Routing

- [SyCCL: Exploiting Symmetry for Efficient Collective Communication Scheduling](https://dl.acm.org/doi/10.1145/3718958.3750499)
  - Jiamin Cao (Alibaba Cloud); Shangfeng Shi (Tsinghua University and Alibaba Cloud); Jiaqi Gao (Alibaba Cloud); Weisen Liu, Yifan Yang (Tsinghua University and Alibaba Cloud); Yichi Xu, Zhilong Zheng, Yu Guan, Kun Qian (Alibaba Cloud); Ying Liu, Mingwei Xu (Tsinghua University); Tianshu Wang, Ning Wang, Jianbo Dong, Binzhang Fu, Dennis Cai, Ennan Zhai (Alibaba Cloud)
  - 集体通信调度的性能对于机器学习作业的效率和 GPU 集群的利用率至关重要；现有的开源集体通信库（例如 NCCL 和 RCCL）依赖于固定的时间表，无法适应不同的拓扑和模型要求；最先进的集体调度合成器（例如 TECCL 和 TACCL）利用混合整数线性程序进行建模，但遇到搜索空间爆炸和可扩展性挑战。SyCCL 是一种可扩展的集体调度合成器，旨在在数十分钟内为生产规模的机器学习作业合成接近最优的调度；SyCCL 利用集体和拓扑对称性将原始集体通信需求分解为较小拓扑子集中的较小子需求；SyCCL 提出高效的搜索策略来快速探索潜在的子需求，合成相应的子调度，并将这些子调度集成为完整的调度；其 32-A100 测试台和生产规模模拟实验表明，与最先进的技术相比，SyCCL 将总体性能提高了 127%，同时将合成时间缩短了 2 到 4 个数量级。
  - 相较最先进的集体调度合成器（例如 TECCL 和 TACCL）利用混合整数线性程序进行建模，但遇到搜索空间爆炸和可扩展性挑战，核心创新是SyCCL 是一种可扩展的集体调度合成器，旨在在数十分钟内为生产规模的机器学习作业合成接近最优的调度；SyCCL 利用集体和拓扑对称性将原始集体通信需求分解为较小拓扑子集中的较小子需求。
  - AI 集群网络与大模型系统、Full Paper、Collective Communication、Scheduling/Orchestration、NetAI

- [Fornax: A Hardware-Centric Session Management in Large Public Cloud Network](https://dl.acm.org/doi/10.1145/3718958.3750501)
  - Heng Yu (Zhongguancun Laboratory); Jian Wang, Jian Zhao, Kai Ren (Tencent); Guozhi Lin (Zhongguancun Laboratory); Baozeng Zhang, Yunpeng Guan, Xin Li, Hao Yin, Jiajun Liang, Liang Wang, Chao Pei, Yachen Wang (Tencent); Xin Jin (Peking University); Jilong Wang (Zhongguancun Laboratory); Congcong Miao (Tencent)
  - SmartNIC 越来越多地用于加速云网络组件；硬件加速的有效性和正确性很大程度上取决于其管理机制；遗憾的是，传统的管理机制采用以软件为中心的架构，以流为基本管理单元，完全依赖单向命令来管理流表，在管理超大表的同时，难以支持各种云网络场景。该工作设计并实施了一个名为 Fornax 的首创系统，这是一种针对大型公共云网络的新颖管理架构；Fornax 的核心是利用会话授权的硬件引擎来提供各种管理功能；其大规模生产结果表明，Fornax 可以管理多达 16M 的会话条目，同时显著降低超过 79% 的资源开销。
  - 相较传统的管理机制采用以软件为中心的架构，以流为基本管理单元，完全依赖单向命令来管理流表，在管理超大表的同时，难以支持各种云网络场景，核心创新是该工作设计并实施了一个名为 Fornax 的首创系统，这是一种针对大型公共云网络的新颖管理架构；Fornax 的核心是利用会话授权的硬件引擎来提供各种管理功能。
  - 可编程数据平面与云网络、Full Paper、SmartNIC/DPU

- [NPC: Rethinking Dataplane through Network-aware Packet Classification](https://dl.acm.org/doi/10.1145/3718958.3750511)
  - Xinyi Zhang, Qianrui Qiu (Computer Network Information Center, CAS; University of Chinese Academy of Sciences); Zhiyuan Xu (University of Chinese Academy of Sciences); Peng He (Independent Researcher); Xilai Liu (Institute of Computing Technology, Chinese Academy of Sciences;University of Chinese Academy of Sciences); Kavé Salamatian (LISTIC; Université Savoie Mont Blanc); Changhua Pei, Gaogang Xie (Computer Network Information Center, CAS; University of Chinese Academy of Sciences)
  - 数据包分类是对网络系统中的流量进行准确分类的关键组件；数据包分类算法的效率主要由两个关键因素决定：分类器的数据结构和被分类的流量的特征；尽管研究团队在优化数据结构方面做出了巨大努力，但利用流量特征的潜力仍未得到充分开发。研究团队通过将网络测量模块与数据包分类模块集成来重新审视网络数据平面；该工作设计一种创新的网络感知数据包分类系统（NPC），该系统利用草图技术来提取网络流量特征；这些功能指导决策树的构建，从而在不同的网络环境中实现高效且适应性强的数据包分类；此外，与原生 OVS 相比，将 NPC 集成到 Open vSwitch (OVS) 中可将吞吐量提高 10.71× 至 13.01×。
  - 相较尽管研究团队在优化数据结构方面做出了巨大努力，但利用流量特征的潜力仍未得到充分开发，核心创新是研究团队通过将网络测量模块与数据包分类模块集成来重新审视网络数据平面；该工作设计一种创新的网络感知数据包分类系统（NPC），该系统利用草图技术来提取网络流量特征；这些功能指导决策树的构建，从而在不同的网络环境中实现高效且适应性强的数据包分类。
  - 可编程数据平面与云网络、Full Paper、Network Measurement/Telemetry

- [Pegasus: A Universal Framework for Scalable Deep Learning Inference on the Dataplane](https://dl.acm.org/doi/10.1145/3718958.3750529)
  - Yinchao Zhang, Su Yao, Yong Feng, Kang Chen (Tsinghua University); Tong Li (Renmin University of China); Zhuotao Liu (Tsinghua University); Yi Zhao (Beijing Institute of Technology); Lexuan Zhang, Xiangyu Gao (Tsinghua University); Feng Xiong (Beihang University); Qi Li, Ke Xu (Tsinghua University)
  - 智能数据平面 (IDP) 的范例在网络数据平面上嵌入深度学习 (DL) 模型，以实现线速智能流量分析；然而，当前在数据平面上使用的匹配动作表 (MAT) 抽象与深度学习推理不一致，导致了几个关键限制，包括准确性下降、规模有限和缺乏通用性；Pegasus 是 来解决这些限制。Pegasus 将 DL 操作转换为三个面向数据平面的原语以实现通用性：Partition、Map 和 SumReduce；与此同时，Pegasus 的性能优于最先进的方法，平均准确度提高了 22.8%，模型尺寸扩大了 248 倍，输入规模扩大了 212 倍。
  - 相较Pegasus 是 来解决这些限制，核心创新是Pegasus 将 DL 操作转换为三个面向数据平面的原语以实现通用性：Partition、Map 和 SumReduce。
  - 可编程数据平面与云网络、Full Paper、Programmable Network Hardware

- [PtCAM: Scalable High-Speed Name Prefix Lookup using TCAM](https://dl.acm.org/doi/10.1145/3718958.3750531)
  - Tian Song, Tianlong Li, Yating Yang (Beijing Institute of Technology)
  - 名称前缀查找是 ICN 中基于名称的数据包转发以及 CDN 中的 URL 重定向的核心特征；该操作本质上是对类似 URL 的名称进行最长前缀匹配，由于名称集大、长度无限制以及逐包查找的需要，该操作在高速处理方面面临着重大挑战。该工作设计一种方案，使用 TCAM 支持对数百万个前缀进行通用分层名称查找，并具有快速、恒定和有保证的性能；其工作有三个贡献；首先，提出了一种名为 PtCAM 的方案，利用二进制 Patricia trie 来利用 TCAM 进行名称查找；其次，提出了几种提高效率和可扩展性的方法；值得注意的是，PtCAM 可以在基于 TCAM 的 IP 线卡上实施，这意味着工业商业现成设备可以直接参与以信息为中心的创新和部署的推进。
  - 相较该操作本质上是对类似 URL 的名称进行最长前缀匹配，由于名称集大、长度无限制以及逐包查找的需要，该操作在高速处理方面面临着重大挑战，核心创新是该工作设计一种方案，使用 TCAM 支持对数百万个前缀进行通用分层名称查找，并具有快速、恒定和有保证的性能；其工作有三个贡献；首先，提出了一种名为 PtCAM 的方案，利用二进制 Patricia trie 来利用 TCAM 进行名称查找。
  - 可编程数据平面与云网络、Full Paper、Programmable Network Hardware、Caching/CDN

- [Scaling SCIERA: A Journey Through the Deployment of a Next-Generation Network](https://dl.acm.org/doi/10.1145/3718958.3750532)
  - François Wirz (ETH Zurich); Marten Gartner (OVGU Magdeburg); Jelte van Bommel, Elham Ehsani Moghadam (ETH Zurich); Grace H. Cimaszewski (Princeton); Anxiao He, Yizhe Zhang (UVA); Henry Birge-Lee (Princeton); Felix Kottmann (ETH Zurich); Cyrill Krähenbühl (Princeton); Jonghoon Kwon (ETH Zurich); Kyveli Mavromati (Anapaya Systems); Liang Wang (Princeton); Daniel Bertolo (SWITCH); Marco Canini (KAUST); Buseung Cho (KISTI); Ronaldo A. Ferreira (UFMS); Simon Peter Green (SingAREN); David Hausheer (OVGU Magdeburg); Junbeom Hur (Korea University); Xiaohua Jia (CityUHK); Heejo Lee (Korea University); Prateek Mittal (Princeton); Omo Oaiya (WACREN); Chanjin Park (KISTI); Adrian Perrig (ETH Zurich); Jerry Sobieski (GMU / Sobieski Systems & Services); Yixin Sun (UVA); Cong Wang (CityUHK); Klaas Wierenga (GÉANT)
  - SCIERA 在研究教育网中部署 SCION，以 SCION-IP gateway 在不修改应用的条件下完成 IP–SCION–IP 转换。部署覆盖五大洲约 25 万用户，通过多条域间路径提供不依赖 BGP 的连接；论文总结了本地接入、网关兼容和跨域运营的实际障碍。
  - 相较只在测试床验证新一代 Internet 架构，核心贡献是给出跨多洲、与现有 IP 应用兼容的 SCION 规模化部署路径及运营经验。
  - 互联网架构、路由与流量控制、Full Paper、Internet Routing、Network Architecture

- [RANBooster: Democratizing advanced cellular connectivity through fronthaul middleboxes](https://dl.acm.org/doi/10.1145/3718958.3754349)
  - Xenofon Foukas (Microsoft); Tenzin Samten Ukyab (UC Berkeley); Bozidar Radunovic (Microsoft); Sylvia Ratnasamy (UC Berkeley); Scott Shenker (ICSI AND UC Berkeley)
  - 5G 无线接入网络已转向虚拟化和分解；这一变化旨在通过促进供应商互操作性和扩展生态系统来降低成本并促进创新；为了解决这些问题，该工作设计一种称为 RANBooster 的中间盒架构，通过利用开放前传接口，在不修改现有网络功能的情况下增强 RAN 功能。为了展示 RANBooster 框架的优势，该工作设计四个参考应用（分布式天线系统、分布式 MIMO、RU 共享、实时物理资源块监控），并在企业级商业级 5G 测试台上对其进行评估。
  - 相较这一变化旨在通过促进供应商互操作性和扩展生态系统来降低成本并促进创新，核心创新是该工作设计一种称为 RANBooster 的中间盒架构，通过利用开放前传接口，在不修改现有网络功能的情况下增强 RAN 功能。
  - 无线、蜂窝与感知、Full Paper、Cellular/RAN

- [Understanding and Profiling CXL.mem Using PathFinder](https://dl.acm.org/doi/10.1145/3718958.3750479)
  - Xiao Li (University of Wisconsin-Madison/Beihang University); Zerui Guo (University of Wisconsin-Madison); Yuebin Bai (Beihang University); Mahesh Ketkar, Hugh Wilkinson (Intel); Ming Liu (University of Wisconsin-Madison)
  - CXL.mem 和由此产生的内存池很有前景并得到广泛部署；与本地 DIMM 不同，CXL DIMM 驻留在 I/O 子系统（即 FlexBus），很容易使处理器管道和内存子系统停顿，从而危及共置应用程序；然而，其社区缺乏一种工具来理解和分析 CPU 和远程 DIMM 之间端到端的 CXL.mem 执行。该工作设计 PathFinder，这是一个用于捕获服务器系统中 CXL.mem 执行的系统实用程序；其关键思想是将端到端 CXL.mem 数据路径建模为基于架构性能计数器的执行图，并应用图分析技术；PathFinder 将 CXL 和竞争内存流与底层硬件关联起来，创建一系列快照，并识别性能瓶颈；研究团队将 PathFinder 应用到许多实际用例中，并证明了其在应用程序分析、瓶颈分析和性能异常诊断方面的功效。
  - 相较其社区缺乏一种工具来理解和分析 CPU 和远程 DIMM 之间端到端的 CXL.mem 执行，核心创新是该工作设计 PathFinder，这是一个用于捕获服务器系统中 CXL.mem 执行的系统实用程序；其关键思想是将端到端 CXL.mem 数据路径建模为基于架构性能计数器的执行图，并应用图分析技术。
  - 数据中心网络、传输与互连、Full Paper、Network Measurement/Telemetry、Failure Diagnosis

- [PreTE: Traffic Engineering with Predictive Failures](https://dl.acm.org/doi/10.1145/3718958.3750508)
  - Congcong Miao (Tencent); Zhizhen Zhong (Massachusetts Institute of Technology); Yiren Zhao (Tencent); Arpit Gupta (UCSB); Ying Zhang (Meta); Sirui Li, Zekun He, Xianneng Zou (Tencent); Jilong Wang (Tsinghua university)
  - 广域网 (WAN) 中的光纤链路暴露在复杂的环境中，因此很容易出现断纤等故障；使用静态概率故障的传统方法在光纤切断场景中存在不足，因为这些光纤切断很少见，但具有破坏性，使得网络运营商很难在 WAN 流量工程中平衡网络利用率和可用性；研究团队对每秒光层数据的大规模测量表明，当经历罕见且短暂的退化状态时，光纤的故障概率会增加几个数量级。因此，该工作设计一种称为 PreTE 的新型流量工程 (TE) 系统，将动态光纤切断概率直接纳入 TE 系统；作为 PreTE 系统的核心，光纤退化有助于故障预测和主动更新流量隧道，进而优化更新隧道之间的流量分配；其大规模仿真结果表明，与现有 TE 方案相比，PreTE 在相同可用性水平下可以支持高达 2 倍的需求。
  - 相较传统方法在光纤切断场景中存在不足，因为这些光纤切断很少见，但具有破坏性，使得网络运营商很难在 WAN 流量工程中平衡网络利用率和可用性，核心创新是因此，该工作设计一种称为 PreTE 的新型流量工程 (TE) 系统，将动态光纤切断概率直接纳入 TE 系统；作为 PreTE 系统的核心，光纤退化有助于故障预测和主动更新流量隧道，进而优化更新隧道之间的流量分配。
  - 网络测量、诊断与可观测性、Full Paper、Optical Interconnect、Traffic Engineering、Network Measurement/Telemetry、Scheduling/Orchestration

- [S2: A Distributed Configuration Verifier for Hyper-Scale Networks](https://dl.acm.org/doi/10.1145/3718958.3750516)
  - Dan Wang, Peng Zhang, Wenbing Sun, Wenkai Li (Xi'an Jiaotong University); Xing Feng (NorthWest University); Hao Li (Xi'an Jiaotong University); Jiawei Chen, Weirong Jiang, Yongping Tang (ByteDance)
  - 网络配置验证者可以主动推断网络的正确性，以防止网络中断；然而，即使最近提出了将验证“扩展”到数千台交换机的算法，这些算法仍然无法用于具有超过 10K 交换机或 1000M 路由的网络，这对于大型服务提供商来说很常见。研究团队不是进一步扩展仅限于单个服务器的验证，而是研究如何利用多个服务器的资源来“扩展”验证；为了实现这一目标，S2 是一个用于网络配置的分布式验证器；S2 对网络模型进行划分，并将控制平面仿真和数据平面验证等验证任务分布在多个服务器上并行运行；基于大型服务提供商的真实数据中心拓扑和合成的 FatTree 拓扑，研究团队表明 S2 可以在 2 小时内验证具有 10K 路由器和 1000M 路由的网络。
  - 相较即使最近提出了将验证“扩展”到数千台交换机的算法，这些算法仍然无法用于具有超过 10K 交换机或 1000M 路由的网络，这对于大型服务提供商来说很常见，核心创新是研究团队不是进一步扩展仅限于单个服务器的验证，而是研究如何利用多个服务器的资源来“扩展”验证；为了实现这一目标，S2 是一个用于网络配置的分布式验证器；S2 对网络模型进行划分，并将控制平面仿真和数据平面验证等验证任务分布在多个服务器上并行运行。
  - 网络验证、管理与安全、Full Paper、Formal Verification

- [New Evolution of Hoyan: Enhancing Scalability, Usability, and Accuracy for Alibaba's Global WAN Verification](https://dl.acm.org/doi/10.1145/3718958.3754343)
  - Yifei Yuan, Fangdan Ye, Yifan Li, Jingkai Zhang, Mengqi Liu, Yuyang Sang, Ruizhen Yang, Duncheng She, Zhiqing Ye, Tianchen Guo, Xiaobo Zhu, Xinji Tang, Li Jia, Zhongyu Guan, Lingpeng Su, Ci Wang, Ruiyang Feng, Shuo Wu, Zhonghui Xie, Cheng Jin, Peng Zhang (Alibaba Cloud); Qing Ma (Alibaba Group); Xianlong Zeng, Dennis Cai, Ennan Zhai (Alibaba Cloud)
  - Hoyan 是阿里云全球 WAN 的生产验证系统；新版把集中式仿真改为分布式框架，并联合改进可用性与准确性，以处理万级路由器、数百万前缀和数十亿流。其仿真效率提高 5 倍，每周支撑百级验证请求，并促使误配置事件占比由 56% 降至 5%。
  - 相较为较小 WAN 设计的集中式验证，核心创新是将控制面仿真分布执行，同时以生产工作流约束结果的可用性和准确性。
  - 网络验证、管理与安全、Full Paper、Failure Diagnosis、Formal Verification

- [Lessons learned from operating a large network telescope](https://dl.acm.org/doi/10.1145/3718958.3754347)
  - Alexander Männel, Jonas Mücke (TU Dresden); KC Claffy (CAIDA/UC San Diego); Max Gao (UC San Diego); Ricky K. P. Mok (CAIDA/UC San Diego); Marcin Nawrocki (NETSCOUT); Thomas C. Schmidt (HAW Hamburg); Matthias Wählisch (TU Dresden)
  - 该工作总结 UCSD Network Telescope 长期接收 Internet background radiation 的生产经验，观测粒度覆盖扫描、伪造源 DDoS 回波和配置错误流量。团队利用第三方扫描活动作为外部参照，持续检查采集数据完整性并定位测量设施的配置问题，再用具体案例说明这些偏差会怎样改变对中断与安全事件的结论。
  - 相较把 darknet 数据默认视为稳定可信的既有测量，核心创新是把传感设施本身当作待验证系统，并用独立扫描源建立长期完整性校验；这些经验也可迁移到 honeypot 等被动观测平台。
  - 网络测量、诊断与可观测性、Full Paper、Network Measurement/Telemetry、Security/Privacy、NetMon & Hyperscalers

- [Unlocking Superior Performance in Reconfigurable Data Center Networks with Credit-Based Transport](https://dl.acm.org/doi/10.1145/3718958.3754342)
  - Federico De Marchi, Jialong Li (Max Planck Institute for Informatics); Ying Zhang (Meta); Wei Bai (NVIDIA); Yiting Xia (Max Planck Institute for Informatics)
  - 微秒交换可重构数据中心网络 (RDCN) 的大规模端到端实施，加上创新的路由和拓扑设计，提供连续路由，消除频繁的拓扑变化，证明了在后摩尔定律时代作为 Clos 网络的可行替代方案的前景；然而，运输性能方面仍然存在差距，当前的运输解决方案未能充分发挥其性能。该工作设计 Flare，一种基于信用的新型传输协议，可确保可靠的流量传输、低延迟，并利用 RDCN 的快速重新配置电路，在短路径上机会性地路由流量，从而最大化吞吐量；在模拟中，Flare 使 RDCN 的性能优于 Clos 网络，即使在对抗流量下也能实现高达 1.15 倍的吞吐量提升；此外，它的吞吐量比 NDP 和 ExpressPass 高 2 倍和 1.5 倍，并且流完成时间 (FCT) 比 ExpressPass、TDTCP 和 Bolt 短 10 倍、15 倍和 3.5 倍；其测试平台实施进一步证明了 Flare 机制与可编程开关和 DPDK 的可行性。
  - 相较运输性能方面仍然存在差距，当前的运输解决方案未能充分发挥其性能，核心创新是该工作设计 Flare，一种基于信用的新型传输协议，可确保可靠的流量传输、低延迟，并利用 RDCN 的快速重新配置电路，在短路径上机会性地路由流量，从而最大化吞吐量。
  - 数据中心网络、传输与互连、Full Paper、Programmable Network Hardware、Internet Routing

- [From ATOP to ZCube: Automated Topology Optimization Pipeline and A Highly Cost-Effective Network Topology for Large Model Training](https://dl.acm.org/doi/10.1145/3718958.3750503)
  - Zihan Yan, Dan Li (Tsinghua University); Li Chen (Zhongguancun Laboratory); Dian Xiong (Harnets.AI); Kaihui Gao (Zhongguancun Laboratory); Yiwei Zhang, Rui Yan (Tsinghua University); Menglei Zhang, Bochun Zhang, Zhuo Jiang, Jianxi Ye, Haibin Lin (ByteDance)
  - 大语言模型（LLM）的发展给数据中心网络拓扑设计带来了新的挑战。为了帮助探索拓扑设计，该工作设计 ATOP，一种自动拓扑优化管道，它将网络拓扑建模为一组超参数，从而能够发现潜在的拓扑；ATOP 通过丰富的优化算法和可定制的优化目标，实现了数万 GPU 规模的自动化拓扑优化；研究团队在 256256、10241024、40964096 和 1638416384 GPU 的网络拓扑上应用 ATOP，优化 LLM 训练流量模式、集体通信性能、容错和网络成本下的性能；结果表明，与轨道优化拓扑相比，ZCube 降低了 25% 的硬件成本，同时保持相同的 all-reduce 和 all-to-all 性能。
  - 相较大语言模型（LLM）的发展给数据中心网络拓扑设计带来了新的挑战，核心创新是为了帮助探索拓扑设计，该工作设计 ATOP，一种自动拓扑优化管道，它将网络拓扑建模为一组超参数，从而能够发现潜在的拓扑；ATOP 通过丰富的优化算法和可定制的优化目标，实现了数万 GPU 规模的自动化拓扑优化。
  - AI 集群网络与大模型系统、Full Paper、LLM Systems、Collective Communication

- [Reliable and Decentralized Certificate Revocation via DNS: The Case for RevDNS](https://dl.acm.org/doi/10.1145/3718958.3754351)
  - Protick Bhowmick (Virginia Tech); Dave Levin (University of Maryland); Taejoong Chung (Virginia Tech)
  - 在线证书状态协议的长期下滑——经过 25 年的软失败规则、隐私泄露和不稳定的基础设施——暴露了网络 PKI 撤销方面更深层次的失败；证书颁发机构越来越多地通过 CDN 路由 OCSP 流量以提高速度，但这会重新集中信任：其测量显示 Akamai 服务了 62% 的吊销响应，从而造成了单点故障并违背了 PKI 的去中心化理念。该工作设计 RevDNS，这是一种基于 DNS 的撤销方案，可以在保持实时保证的同时消除对 CDN 的依赖；已撤销的序列号存在于 DNSSEC 签名的 TXT 记录中； NSEC 证明允许积极的负缓存，因此递归解析器可以回答 99.8% 的检查，而无需打扰 CA；从 11 亿个证书和 500 万个吊销中，研究发现像 Let’s Encrypt 这样的大型 CA 可以在 345MB 区域中发布 6.12 亿个证书的数据，解析器几乎承担所有查找。
  - 相较证书颁发机构越来越多地通过 CDN 路由 OCSP 流量以提高速度，但这会重新集中信任：其测量显示 Akamai 服务了 62% 的吊销响应，从而造成了单点故障并违背了 PKI 的去中心化理念，核心创新是该工作设计 RevDNS，这是一种基于 DNS 的撤销方案，可以在保持实时保证的同时消除对 CDN 的依赖；已撤销的序列号存在于 DNSSEC 签名的 TXT 记录中。
  - 网络验证、管理与安全、Full Paper、Network Measurement/Telemetry、Security/Privacy、Caching/CDN

- [SaTE: Low-Latency Traffic Engineering for Satellite Networks](https://dl.acm.org/doi/10.1145/3718958.3750524)
  - Hao Wu, Yizhan Han (Department of Computer Science, National University of Singapore); Mohit Rajpal (National University of Singapore); Qizhen Zhang (University of Toronto); Jingxian Wang (National University of Singapore)
  - 该工作研究大规模低地轨道卫星星座的流量工程（TE）；虽然针对全球云广域网 (WAN) 的 TE 算法有丰富的先前工作，但它们是针对静态网络拓扑设计的，并且通常需要大量的计算时间来处理大型网络；这些限制使得现有的 WAN TE 算法不适合快速改变拓扑并需要在严格的延迟约束下计算最佳流量分配的大规模卫星网络。SaTE 是一种用于大规模卫星网络的低延迟 TE 算法，以毫秒延迟计算流量分配；SaTE 制定异构图来模拟 TE 问题，适应动态卫星拓扑；其结果显示，平均 TE 运行时间为 17 𝑚𝑠，满足的需求提高了 23.5%，与商业求解器相比，实现了 2738 倍的加速。
  - 相较现有的 WAN TE 算法不适合快速改变拓扑并需要在严格的延迟约束下计算最佳流量分配的大规模卫星网络，核心创新是SaTE 是一种用于大规模卫星网络的低延迟 TE 算法，以毫秒延迟计算流量分配；SaTE 制定异构图来模拟 TE 问题，适应动态卫星拓扑。
  - 卫星、海洋与非地面网络、Full Paper、Traffic Engineering、Satellite/LEO、Scheduling/Orchestration

- [Small-scale LEO Satellite Networking for Global-scale Demands](https://dl.acm.org/doi/10.1145/3718958.3750525)
  - Yuanjie Li, Yimei Chen, Jiabo Yang, Jinyao Zhang, Bowen Sun, Lixin Liu, Hewu Li, Jianping Wu, Zeqi Lai, Qian Wu, Jun Liu (Tsinghua University)
  - TinyLEO 面向地理分布高度不均的全球 Internet 需求：它用多样但稀疏的轨道按时空供需动态裁减卫星，以 orbital model-predictive control 隐藏稀疏网络的连通复杂性，再由地面段 anycast 承担快速切换。开源原型评估显示，在保持需求和相近数据面性能时，现有巨型星座可缩小 2.0–7.9 倍，控制面成本降低 1–3 个数量级。
  - 相较以均匀巨型星座覆盖不均需求，核心创新是联合稀疏轨道、预测控制和地理 anycast，使卫星供给按时空需求匹配。
  - 卫星、海洋与非地面网络、Full Paper、Satellite/LEO、Compression/Encoding、Scheduling/Orchestration

- [Direct-to-Cell Satellite Network without Satellite Navigation](https://dl.acm.org/doi/10.1145/3718958.3750522)
  - Wei Liu, Yuanjie Li, Jingyi Lan, Hewu Li, Yimei Chen, Lixin Liu, Jiabo Yang, Xi Long, Li Ouyang, Minghao Tang, Jianping Wu, Qian Wu, Jun Liu, Zeqi Lai (Tsinghua University)
  - 该工作研究 direct-to-cell 卫星网对外部 GNSS 的跨技术依赖：用户定位与授时错误会传导成断连、错误计费、未授权服务或拒绝服务。SN2 按“命运共享”原则让 direct-to-cell 卫星网自行提供导航状态；商用卫星电话与 3GPP NTN 协议栈测试中，可用性提高 6.6–23.5 倍，接入延迟降低 2.8–12.3 倍。
  - 相较用 GNSS 支撑接入、鉴权与漫游策略的 direct-to-cell 方案，核心创新是将导航能力收回到卫星网内，切断 GNSS 故障的传导链。
  - 卫星、海洋与非地面网络、Full Paper、Satellite/LEO、Cellular/RAN、Network Architecture & Satellites

- [StarCDN: Moving Content Delivery Networks to Space](https://dl.acm.org/doi/10.1145/3718958.3754345)
  - William X. Zheng, Aryan Taneja, Maleeha Masood (University of Illinois Urbana-Champaign); Anirudh Sabnis (Akamai Technologies); Ramesh K. Sitaraman (UMass Amherst & Akamai Technologies); Deepak Vasisht (University of Illinois Urbana-Champaign)
  - 低地球轨道 (LEO) 卫星网络（例如 Starlink）提供全球互联网接入，目前为数百万用户提供内容；最近的研究表明，现有的网络基础设施，例如内容交付网络（CDN），不太适合卫星网络架构；传统的地面 CDN 会降低卫星网络用户的性能，并且不能缓解地面卫星链路的拥塞。StarCDN 是一种新的 CDN 架构，可在太空中缓存内容，以改善用户体验并减少地面卫星带宽使用；设计 StarCDN 的根本挑战在于卫星的轨道运动，这会导致每颗卫星的覆盖区域快速变化，在几分钟内为截然不同的地区（例如美国和欧洲）提供服务；为了解决这个问题，该工作设计专为 LEO 卫星网络量身定制的新的一致哈希和中继获取方案；其设计使缓存的内容能够沿轨道运动的相反方向流动，以对抗卫星运动；评估表明，StarCDN 可以将地面到卫星的带宽利用率降低 80%，并将用户感知的延迟提高 2.5 倍。
  - 相较传统的地面 CDN 会降低卫星网络用户的性能，并且不能缓解地面卫星链路的拥塞，核心创新是StarCDN 是一种新的 CDN 架构，可在太空中缓存内容，以改善用户体验并减少地面卫星带宽使用；设计 StarCDN 的根本挑战在于卫星的轨道运动，这会导致每颗卫星的覆盖区域快速变化，在几分钟内为截然不同的地区（例如美国和欧洲）提供服务。
  - 卫星、海洋与非地面网络、Full Paper、Satellite/LEO、Caching/CDN、Network Architecture & Satellites

- [ByteScale: Communication-Efficient Scaling of LLM Training with a 2048K Context Length on 16384 GPUs](https://dl.acm.org/doi/10.1145/3718958.3754352)
  - Hao Ge (Peking University); Junda Feng, Qi Huang (ByteDance Inc.); Fangcheng Fu (Shanghai Jiao Tong University); Xiaonan Nie, Lei Zuo, Haibin Lin (ByteDance Inc.); Bin Cui (Peking University); Xin Liu (ByteDance Inc.)
  - 扩展长上下文能力对于大型语言模型 (LLM) 至关重要；为了在长上下文训练中分摊跨多个设备的内存消耗，数据间分区（又名；然而，LLM 训练的序列通常在长度上有所不同，无论是文本、多模态还是强化学习。ByteScale 是一种高效、灵活、可扩展的 LLM 训练框架，用于长短序列的大规模混合训练；ByteScale 的核心是一种新颖的并行策略，即混合数据并行（HDP），它将数据间和数据内分区与动态网格设计相结合；特别是，该工作设计一个通信优化器，通过数据感知分片和动态通信消除了短序列的冗余通信，并通过选择性卸载进一步压缩长序列的通信成本；此外，研究团队还开发了一个平衡调度程序，通过并行感知数据分配来减轻不平衡计算；实验结果表明，ByteScale 的性能优于最先进的训练系统高达 7.89×7.89×。
  - 相较无论是文本、多模态还是强化学习，LLM 训练的序列通常长度各不相同，核心创新是ByteScale 是一种高效、灵活、可扩展的 LLM 训练框架，用于长短序列的大规模混合训练；ByteScale 的核心是一种新颖的并行策略，即混合数据并行（HDP），它将数据间和数据内分区与动态网格设计相结合。
  - AI 集群网络与大模型系统、Full Paper、LLM Systems、Compression/Encoding、Scheduling/Orchestration

- [Making Cellular Networks More Efficient By Roaming-in-Place](https://dl.acm.org/doi/10.1145/3718958.3750538)
  - Tenzin Samten Ukyab (UC Berkeley); Lisa Suzuki (Waseda University); Demetrius Davis (Virginia Tech); Zhihong Luo, Silvery Fu (UC Berkeley); Shaddi Hasan (Virginia Tech); Sylvia Ratnasamy (UC Berkeley); Scott Shenker (ICSI AND UC Berkeley)
  - 该工作设计就地漫游 (RinP)，这是一种在移动网络运营商之间动态共享容量的技术。RinP 是一种新形式的基础设施共享，它扩展了蜂窝网络中漫游的传统概念，以便用户可以根据负载和性能条件在具有重叠覆盖区域的运营商之间漫游；该工作设计一个原型 RinP 测试台，并表明该工作设计的设计可以通过对现有蜂窝基础设施进行适度更改来实现，无需更改当前协议标准，并且增加最小的延迟开销。
  - 官方摘要未展开更细的直接基线；可核验的核心创新是该工作设计就地漫游 (RinP)，这是一种在移动网络运营商之间动态共享容量的技术；RinP 是一种新形式的基础设施共享，它扩展了蜂窝网络中漫游的传统概念，以便用户可以根据负载和性能条件在具有重叠覆盖区域的运营商之间漫游。
  - 无线、蜂窝与感知、Full Paper、Cellular/RAN、NetAI & Wireless

- [Enabling Over-the-Air AI for Edge Computing via Metasurface-Driven Physical Neural Networks](https://dl.acm.org/doi/10.1145/3718958.3750474)
  - Chao Feng, Shuo Liang, Chenghui Li, Gaoteng Zhao, Beier Jing (Northwest University); Yaxiong Xie (University at Buffalo SUNY); Xiaojiang Chen (Northwest University)
  - 该工作设计 MetaAI，一种新颖的无线计算范式，它将神经网络计算直接集成到无线信号传播中。该工作设计 MetaAI，一种新颖的无线计算范例，它将神经网络计算直接集成到无线信号传播中；与将无线通道视为单纯数据管道的传统方法不同，MetaAI 通过可编程超表面将它们转变为主动计算元素，从而实现并发数据传输和神经网络处理；通过利用无线传播和神经网络的固有线性，其设计解决了顺序无线传输和并行神经计算之间的根本不匹配问题，同时支持高效的多传感器后期数据融合；研究使用超表面在双频段 (2.4/5 GHz) 和单频段 (3.5 GHz) 频率下实现了 MetaAI；多传感器融合进一步提高准确率高达 27.06%。
  - 官方摘要未展开更细的直接基线；可核验的核心创新是该工作设计 MetaAI，一种新颖的无线计算范例，它将神经网络计算直接集成到无线信号传播中；与将无线通道视为单纯数据管道的传统方法不同，MetaAI 通过可编程超表面将它们转变为主动计算元素，从而实现并发数据传输和神经网络处理。
  - 无线、蜂窝与感知、Full Paper、Wireless/Sensing、NetAI & Wireless

- [Towards Next-Generation Global IoT: Empowering Massive Connectivity with Harmonious Multi-Network Coexistence](https://dl.acm.org/doi/10.1145/3718958.3750504)
  - Ziyue Zhang, Xianjin Xia, Ruonan Li, Yuanqing Zheng (The Hong Kong Polytechnic University)
  - LoRaWAN 提供了一种引人注目的解决方案，可为全球数百万个物联网设备提供经济高效的网络访问；然而，运营商在扩展服务以满足物联网连接不断增长的需求方面面临挑战；其研究首次表明，LoRaWAN 中的容量下降并不是由于传统认为的问题（例如无线争用或干扰）造成的，而是新发现的解码器争用问题。根据其新发现，该工作设计设计原则，指导研究团队探索有效策略来解决这一新出现的实际问题；该工作设计具体的可部署解决方案，以缓解争用、优化频谱利用率并促进网络运营商之间的频谱共享；广泛的评估表明，其策略有效地将网络容量提升到接近理论极限，并支持多达六个网络的共存，并显著提高了频谱效率。
  - 相较传统认为的问题（例如无线争用或干扰）造成的，而是新发现的解码器争用问题，核心创新是根据其新发现，该工作设计设计原则，指导研究团队探索有效策略来解决这一新出现的实际问题；该工作设计具体的可部署解决方案，以缓解争用、优化频谱利用率并促进网络运营商之间的频谱共享。
  - 无线、蜂窝与感知、Full Paper、Failure Diagnosis、Wireless/Sensing、NetAI & Wireless

- [Mobile Underwater Backscatter Networking](https://dl.acm.org/doi/10.1145/3718958.3750507)
  - Purui Wang, Sayed Saad Afzal (MIT); Fadel Adib (MIT & Cartesian)
  - 水下反向散射是一种很有前途的超低功耗水下网络技术，但现有系统在移动场景中会崩溃。该工作设计 EchoRider，这是第一个在移动条件下实现可靠的水下反向散射网络的系统；EchoRider 引入了三个关键组件；首先，它采用了强大且节能的下行链路架构，在读取器处使用线性调频脉冲调制传输，并在反向散射节点上使用亚奈奎斯特线性调频解码器，从而为水下反向散射带来 LoRa 风格信令的弹性，同时保持超低功耗；其次，它引入了基于 NACK 的全双工重传协议，可实现高效、可靠的数据包传输；最后，研究团队在涉及移动无人机和传感器节点的端到端部署中演示了 EchoRider，展示了其在实际水下网络应用中的有效性。
  - 相较现有系统在移动场景中会崩溃，核心创新是该工作设计 EchoRider，这是第一个在移动条件下实现可靠的水下反向散射网络的系统；EchoRider 引入了三个关键组件；首先，它采用了强大且节能的下行链路架构，在读取器处使用线性调频脉冲调制传输。
  - 无线、蜂窝与感知、Full Paper、Underwater/Submarine Network、Wireless/Sensing、NetAI & Wireless

- [Acoustic Backscatter Network for Vehicle Body-in-white](https://dl.acm.org/doi/10.1145/3718958.3750486)
  - Weiguo Wang (NIO, Tsinghua University); Yuan He, Yadong Xie, Chuyue Xie (Tsinghua University); Yi Kai, Chengchen Hu (NIO)
  - ArachNet 利用白车身金属结构传播振动，同时进行能量传输和 acoustic backscatter 通信；无电池 tag 从车身振动取能，超低功耗电路与分布式 slot allocation 解决启动供能和冲突。12 个 tag 的电动 SUV 原型中，tag 收/发功耗为 24.8/51.0 μW，slot 利用率最高 81.2%。
  - 相较在金属车身内布线或使用易遮挡的无线传感器，核心创新是把车身本体变成取能与通信共用的振动介质。
  - 无线、蜂窝与感知、Full Paper、Wireless/Sensing、Scheduling/Orchestration、NetAI & Wireless

- [Low-Overhead Distributed Application Observation with DeepTrace: Achieving Accurate Tracing in Production Systems](https://dl.acm.org/doi/10.1145/3718958.3750477)
  - Yantao Geng, Han Zhang, Zhiheng Wu (Tsinghua University); Yahui Li (Tsinghua University,China); Jilong Wang (Tsinghua university); Xia Yin (Tsinghua University)
  - 随着微服务规模和复杂性的增长，其操作和调试变得越来越具有挑战性；即使单个用户请求也可能涉及数百个组件之间的交互；为了应对这些挑战，该工作设计 DeepTrace，这是一种专为微服务设计的基于事务的非侵入式分布式跟踪框架。DeepTrace 利用请求内容中嵌入的 API 端点和事务字段将请求分类为不同的事务，从而降低错误合并来自不同事务的跟踪的可能性；与最先进的框架相比，DeepTrace 即使在高并发下也能保持超过 95% 的准确率；它还被数十家公司在其生产系统中采用，用于故障诊断和资源优化等任务。
  - 相较随着微服务规模和复杂性的增长，其操作和调试变得越来越具有挑战性，核心创新是该工作设计 DeepTrace，这是一种专为微服务设计的基于事务的非侵入式分布式跟踪框架；DeepTrace 利用请求内容中嵌入的 API 端点和事务字段将请求分类为不同的事务，从而降低错误合并来自不同事务的跟踪的可能性。
  - 网络测量、诊断与可观测性、Full Paper、Network Measurement/Telemetry、Failure Diagnosis、Cloud/Distributed Systems

- [Hummingbird: Fast, Flexible, and Fair Inter-Domain Bandwidth Reservations](https://dl.acm.org/doi/10.1145/3718958.3750495)
  - Karl Wüst, Giacomo Giuliari, Markus Legner, Jean-Pierre Smith (Mysten Labs); Marc Wyss, Jules Bachmann, Juan A. Garcia-Pardo (ETH Zurich); Adrian Perrig (Mysten Labs)
  - 在过去的十年中，互联网集中化及其对隐私、弹性和创新的影响已成为人们热议的话题；虽然网络社区非正式地同意集中化的定义，但研究团队缺乏量化它的正式指标，这限制了深入分析。该工作设计严格的互联网集中化统计指标；在此过程中，研究团队还揭示了区域化（地缘政治对互联网的依赖）如何从根本上影响集中化；研究团队认为，集中化和区域化是相互交织的依赖形式，两者都会影响用户的生活体验，应该共同研究；该工作设计一套统计工具，用于更好地了解 150 个国家/地区的三层网络基础设施（托管提供商、DNS 基础设施、证书颁发机构）之间的依赖关系；研究团队希望这个统计工具包可以作为未来分析互联网行为的基础。
  - 相较虽然网络社区非正式地同意集中化的定义，但研究团队缺乏量化它的正式指标，这限制了深入分析，核心创新是该工作设计严格的互联网集中化统计指标；在此过程中，研究团队还揭示了区域化（地缘政治对互联网的依赖）如何从根本上影响集中化；研究团队认为，集中化和区域化是相互交织的依赖形式，两者都会影响用户的生活体验，应该共同研究。
  - 互联网架构、路由与流量控制、Full Paper、Formal Verification、Security/Privacy、Internet Routing

- [Inter-domain Routing with Extensible Criteria](https://dl.acm.org/doi/10.1145/3718958.3750528)
  - Seyedali Tabaeiaghdaei (Anapaya Systems AG); Jelte van Bommel, Marc Wyss (ETH Zurich); João Luis Sobrinho (Instituto de Telecomunicações, Instituto Superior Técnico); Giovanni Barbiero (UBS AG); Giacomo Giuliari (Mysten Labs); Ahad N. Zehmakan (Australian National University); Adrian Perrig (ETH Zurich)
  - IREC 面向 SCION path-aware Internet，让域间控制面按应用所需的可扩展标准优化路径；新标准可加入或修改，而无状态转发保持数据面可扩展。原型和真实 Internet 拓扑仿真证明可行，相对静态路由的全局开销可忽略。
  - 相较只能支持固定或有限路由准则的域间协议，核心创新是利用 path-aware 网络的无状态转发，把路径选择准则做成可扩展控制面接口。
  - 互联网架构、路由与流量控制、Full Paper、Internet Routing

- [Network Support For Scalable And High Performance Cloud Exchanges](https://dl.acm.org/doi/10.1145/3718958.3750530)
  - Muhammad Haseeb (New York University); Jinkun Geng (Clockwork Systems, Inc); Daniel Duclos-Cavalcanti (Technical University of Munich); Xiyu Hao, Ulysses Butler (New York University); Radhika Mittal (University of Illinois Urbana-Champaign); Srinivas Narayana (Rutgers University); Anirudh Sivaraman (New York University)
  - 该工作设计 Onyx，一个用于满足公共云上金融交易网络要求的系统。Onyx 使用覆盖树将市场数据从交易所多播到 1000 个参与者，任何两个参与者之间的数据接收时间差异≤ 1 μs，这对于维持公平竞争至关重要；Onyx 重用同一棵树进行可扩展的入站通信（交换参与者），引入调度策略以增强交换在突发流量期间的吞吐量；Onyx 在支持的参与者数量、交易的订单匹配率和多播延迟方面优于现有系统 CloudEx [2]。
  - 官方摘要未展开更细的直接基线；可核验的核心创新是该工作设计 Onyx，一个用于满足公共云上金融交易网络要求的系统；Onyx 使用覆盖树将市场数据从交易所多播到 1000 个参与者，任何两个参与者之间的数据接收时间差异≤ 1 μs，这对于维持公平竞争至关重要。
  - 分布式系统与网络服务、Full Paper、Scheduling/Orchestration、Distributed Systems

- [Formalizing Dependence of Web Infrastructure](https://dl.acm.org/doi/10.1145/3718958.3750492)
  - Rumaisa Habib, Kimberly Ruth, Gautam Akiwate, Zakir Durumeric (Stanford University)
  - 在过去的十年中，互联网集中化及其对隐私、弹性和创新的影响已成为人们热议的话题；虽然网络社区非正式地同意集中化的定义，但研究团队缺乏量化它的正式指标，这限制了深入分析。该工作设计严格的互联网集中化统计指标；在此过程中，研究团队还揭示了区域化（地缘政治对互联网的依赖）如何从根本上影响集中化；研究团队认为，集中化和区域化是相互交织的依赖形式，两者都会影响用户的生活体验，应该共同研究；该工作设计一套统计工具，用于更好地了解 150 个国家/地区的三层网络基础设施（托管提供商、DNS 基础设施、证书颁发机构）之间的依赖关系；研究团队希望这个统计工具包可以作为未来分析互联网行为的基础。
  - 相较虽然网络社区非正式地同意集中化的定义，但研究团队缺乏量化它的正式指标，这限制了深入分析，核心创新是该工作设计严格的互联网集中化统计指标；在此过程中，研究团队还揭示了区域化（地缘政治对互联网的依赖）如何从根本上影响集中化；研究团队认为，集中化和区域化是相互交织的依赖形式，两者都会影响用户的生活体验，应该共同研究。
  - 分布式系统与网络服务、Full Paper、Formal Verification、Security/Privacy、Distributed Systems

- [Towards User-level QoE: Large-scale Practice in Personalized Optimization of Adaptive Video Streaming](https://dl.acm.org/doi/10.1145/3718958.3750526)
  - Lianchen Jia (Tsinghua University); Chao Zhou (Kuaishou); Chaoyang LI (Tsinghua University); Jiangchuan Liu (Simon Fraser University); Lifeng Sun (Tsinghua University)
  - 基于系统范围服务质量 (QoS) 指标的传统优化方法在现代大规模流媒体系统中已接近性能极限；然而，将用户级体验质量（QoE）与算法优化目标保持一致仍然是一个尚未解决的挑战。因此，该工作设计 LingXi，第一个大规模部署的基于用户体验的个性化自适应视频流系统；LingXi 通过分析用户参与度动态优化自适应视频流算法的目标；以退出率作为关键指标，研究团队根据生产环境日志研究 QoS 指标和退出率之间的相关性，随后开发个性化的退出率预测器；通过蒙特卡洛采样和在线贝叶斯优化，研究团队迭代确定最佳参数；在最大的短视频平台之一的快手上利用 8% 的流量进行大规模 A/B 测试，证明了灵犀的卓越性能；LingXi 使所有用户的总观看时间增加了 0.15%，比特率提高了 0.1%，卡顿时间减少了 1.3%，尤其是低带宽用户的改善尤为显著，卡顿时间减少了 15%。
  - 相较将用户级体验质量（QoE）与算法优化目标保持一致仍然是一个尚未解决的挑战，核心创新是因此，该工作设计 LingXi，第一个大规模部署的基于用户体验的个性化自适应视频流系统；LingXi 通过分析用户参与度动态优化自适应视频流算法的目标。
  - 视频、实时通信与 QoE、Full Paper、Video/QoE、Video & QoE

- [TLadder: QoE-Centric Video Ladder Optimization with Playback Feedback at Billion Scale](https://dl.acm.org/doi/10.1145/3718958.3750500)
  - Zhuqi Li, He Liu, Shenglan Huang, Baojin Geng, Jack Chen, Jialin Chen, Liyang Sun, Qianyun Ma, Peizhe Liu, Junjun Zhao, Yiting Liao, Jamie Chen, Qian Ma, Qiang Ma, Feng Qian (ByteDance)
  - 运营团队维护着全球最大的短视频流媒体平台之一，每天为全球数十亿用户提供服务；与其他平台类似，研究团队采用自适应比特率（ABR）流媒体，它自适应地从形成比特率阶梯的一组视频表示中选择适当的表示；研究团队没有开发另一种 ABR 算法，而是通过开发一个名为 TLadder 的系统来优化构成 ABR 决策空间的比特率阶梯配置。TLadder 通过具有多项式复杂性和可证明最优性的原则性优化框架，显式地最大化梯子预期产生的体验质量 (QoE)；TLadder 的优化联合考虑了视频内容维度（即候选表示的比特率质量权衡）和播放反馈维度（例如网络状况、重新缓冲时间和播放比特率）；TLadder 还引入了高保真模拟器，为优化器提供准确的 QoE 估计；它还优于基于广泛跟踪驱动模拟的现有最先进方法。
  - 官方摘要未展开更细的直接基线；可核验的核心创新是研究团队没有开发另一种 ABR 算法，而是通过开发一个名为 TLadder 的系统来优化构成 ABR 决策空间的比特率阶梯配置；TLadder 通过具有多项式复杂性和可证明最优性的原则性优化框架，显式地最大化梯子预期产生的体验质量 (QoE)。
  - 视频、实时通信与 QoE、Full Paper、Video/QoE、Caching/CDN、Video & QoE

- [ACE: Sending Burstiness Control for High-Quality Real-time Communication](https://dl.acm.org/doi/10.1145/3718958.3750520)
  - Xiangjie Huang, Jiayang Xu (Hong Kong University of Science and Technology); Haiping Wang, Hebin Yu (ByteDance); Sandesh Dhawaskar Sathyanarayana, Shu Shi (Bytedance); Zili Meng (Hong Kong University of Science and Technology)
  - 实时通信 (RTC) 需要超低延迟，同时始终保持高质量；然而，研究观察到，随着内容可变性的增加和 RTT 的减少，视频编码器和网络之间的发送者的调步队列中会出现长尾排队延迟；现有方法通过节奏平滑比特率来缓解这一问题，但这通常需要在视频质量和延迟之间进行权衡。为了解决这个问题，该工作设计一种协调的方法来管理编码复杂性和发送速度；在传输方面，研究团队动态调整基于令牌的定步器的桶大小以控制帧级别内的突发性；在编码器方面，该工作设计一种自适应复杂度机制，可以在不牺牲质量的情况下平滑帧大小；通过跟踪驱动的仿真和真实世界的实验，其解决方案 ACE 可将端到端 95% 的延迟降低高达 43%，同时与最先进的替代方案相比，保持卓越的视频质量。
  - 相较现有方法通过节奏平滑比特率来缓解这一问题，但这通常需要在视频质量和延迟之间进行权衡，核心创新是该工作设计一种协调的方法来管理编码复杂性和发送速度；在传输方面，研究团队动态调整基于令牌的定步器的桶大小以控制帧级别内的突发性；在编码器方面，该工作设计一种自适应复杂度机制，可以在不牺牲质量的情况下平滑帧大小。
  - 视频、实时通信与 QoE、Full Paper、Network Measurement/Telemetry、Video/QoE、Compression/Encoding

- [Harnessing WebRTC for Large-Scale Live Streaming](https://dl.acm.org/doi/10.1145/3718958.3750535)
  - Wei Zhang (ByteDance); Tong Meng, Xianhua Zeng, Wei Yang, Changqing Yan, Chao Li, Chenguang Li (ByteDance Inc.); Feng Qian (ByteDance); Junfeng Yang (Hunan University of Technology and Business); Lei Zhang (Shenzhen University); Zhi Wang (Shenzhen International Graduate School, Tsinghua University)
  - 抖音 RTM 将大规模直播从 HTTP-FLV 迁移到 WebRTC，并以观众渗透率和观看时长筛选优化目标，集中调整首帧延迟、启动/重缓冲、音视频漂移和单会话 CPU 开销。该栈已运行 4 年，每日服务数十亿观看会话。
  - 相较直接用通用 WebRTC 替换 HTTP-FLV，核心贡献是用长期生产用户参与指标决定协议栈的优化优先级，并给出超大规模部署经验。
  - 视频、实时通信与 QoE、Full Paper、Video/QoE、Video & QoE

- [Scalable Video Conferencing Using SDN Principles](https://dl.acm.org/doi/10.1145/3718958.3750489)
  - Oliver Michel, Satadal Sengupta (Princeton University); Hyojoon Kim (University of Virginia); Ravi Netravali, Jennifer Rexford (Princeton University)
  - 视频会议应用程序面临着流量的持续激增，以前所未有的方式对其底层基础设施造成压力；该工作重新设计会议基础设施的关键构建块 - 选择性转发单元 (SFU)；通过剖析生产 SFU 服务器的操作，研究团队得出的主要见解是，SFU 在很大程度上模仿了传统的数据包处理操作，例如丢弃和转发。在此指导下，该工作设计 Scallop，这是一种受 SDN 启发的 SFU，它将视频会议应用程序解耦到基于硬件的数据平面中，用于对延迟敏感且频繁的媒体操作，以及用于（不频繁的）剩余任务的软件控制平面，例如分析反馈信号和会话管理；Scallop 是一种通用设计，适用于各种硬件平台，包括可编程交换机和 SmartNIC；研究团队基于 Tofino 的实施完全支持 WebRTC，并在 32 核商用服务器上提供了 7-422 倍的改进扩展，同时通过将转发引起的延迟减少 26 倍来获得性能改进。
  - 相较传统的数据包处理操作，例如丢弃和转发，核心创新是在此指导下，该工作设计 Scallop，这是一种受 SDN 启发的 SFU，它将视频会议应用程序解耦到基于硬件的数据平面中，用于对延迟敏感且频繁的媒体操作，以及用于（不频繁的）剩余任务的软件控制平面，例如分析反馈信号和会话管理。
  - 视频、实时通信与 QoE、Full Paper、SmartNIC/DPU、Programmable Network Hardware、Video/QoE
