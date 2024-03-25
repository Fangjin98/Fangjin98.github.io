---
title: Distributed Training Research
date: 2024-03-18 23:19:13
tags:
  - Summary
---

### LLM Training

- NSDI 24, MegaScale: Scaling Large Language Model Training to More Than 10,000 GPUs
- ZeRO++: Extremely Efficient Collective Communication for Giant Model Training
- DeepSpeed-MoE: Advancing Mixture-of-Experts Inference and Training to Power Next-Generation AI Scale
- [Colossal-AI A Unified Deep Learning System For Large-Scale Parallel Training](https://arxiv.org/pdf/2110.14883.pdf)
- **Efficient Large-Scale Language Model Training on GPU Clusters Using Megatron-LM**
- GPipe: Efficient Training of Giant Neural Networks using Pipeline Parallelism

### Gradient Compression

- ATC 22, Campo: Cost-Aware Performance Optimization for Mixed-Precision Neural Network Training
- Rethinking Floating Point Overheads for Mixed Precision DNN Accelerators
- SIGCOMM 21, [Efficient Sparse Collective Communication and its application to Accelerate Distributed Deep Learning](https://conferences.sigcomm.org/sigcomm/2021/files/papers/3452296.3472904.pdf), Sparsity, Communication
- SOSP 21, Gradient Compression Supercharged High-Performance Data Parallel DNN Training,  Quantization, Collective Communication
- [Accelerating Distributed Deep Learning using Lossless Homomorphic Compression](https://arxiv.org/pdf/2402.07529.pdf)
- NSDI 24, [THC: Accelerating Distributed Deep Learning Using Tensor Homomorphic Compression](https://arxiv.org/pdf/2302.08545.pdf)

### Model Parallelism

- PipeDream: Generalized Pipeline Parallelism for DNN Training
- OSDI'23, AlpaServe: Statistical Multiplexing with Model Parallelism for Deep Learning Serving
- OSDI'22, Alpa: Automating Inter- and Intra-Operator Parallelism for Distributed Deep Learning
- INFOCOM'22, Efficient Pipeline Planning for Expedited Distributed DNN Training
- HPDC'22, [Hare: Exploiting Inter-job and Intra-job Parallelism of Distributed Machine Learning on Heterogeneous GPUs](https://dl.acm.org/doi/pdf/10.1145/3502181.3531462)

### In-network Aggregation

> See this [post](/2023/07/03/ina/) for details.

### Asynchronous Training

- Developing a Loss Prediction-based Asynchronous Stochastic Gradient Descent Algorithm for Distributed Training of Deep Neural Networks：这篇文章介绍了异步更新的模式。看来参数服务器并没有一个具体的阈值确定何时进行异步更新。这篇文章提出一个算法以弥补梯度损失值。
- ICDCS 19, Dynamic Stale Synchronous Parallel Distributed Training for Deep Learning：提出一种自适应确定延迟轮数方法。
- [Staleness-aware Async-SGD for Distributed Deep Learning](https://arxiv.org/pdf/1511.05950.pdf): 针对异步分布式模型训练调整学习率。
- **Pathways: Asynchronous Distributed Dataflow for ML**: PATHWAYS makes use of a novel asynchronous distributed dataﬂow design that lets the control plane execute in parallel despite dependencies in the data plane
- [Accelerating Distributed Reinforcement Learning with In-Switch Computing](:/85780103fdc6433fa3bf60bd545cc777)：这篇文章提到了使用可编程交换机优化异步训练，理论上来说，我们是可以转移到深度神经网络场景的。这篇文章仅仅通过显性设置延迟边界保证收敛。
- [FedLesScan: Mitigating Stragglers in Serverless Federated Learning](https://arxiv.org/pdf/2211.05739.pdf)
- **Communication-Efficient Federated Deep Learning With Layerwise Asynchronous Model Update and Temporally Weighted Aggregation**：模型不同层的更新频率不一样，一般来说，shallow 层的参数比 deep 层的参数更新更加频繁，因此本文提出根据不同层的更新频率异步训练。本文还提出一个加权聚合策略，从而利用之前聚合的本地模型。
- [AMPNet: Asynchronous Model-Parallel Training for Dynamic Neural Networks](https://arxiv.org/pdf/1705.09786.pdf)
- INT Lab, FedSA: A Semi-Asynchronous Federated Learning Mechanism in Heterogeneous Edge Computing：在联邦学习场景中，由于节点异构，数据分布以及网络资源等问题，同步学习需要忍受很大的同步代价。因此现有研究关注异步学习。这篇论文确定每轮训练中，参数服务器收到哪*k*个工作节点的梯度才更新全局模型。这篇论文根据*边缘异构性*和*数据分布*决定*k*的值。
- INT Lab, Adaptive Asynchronous Federated Learning in Resource-Constrained Edge Computing：这篇文章根据实时系统状态，例如网络资源，为每一轮异步训练确定聚合的工作节点比例。和上一篇工作内容相似。这里是根据全局信息确定的M，感觉参考意义不大

#### Straggler Problem

- Nurd: Negative-Unlabeled Learning for Online Datacenter Straggler Prediction：这篇文章并不是分布式模型训练场景，而是分布式系统中。提出了一个利用无监督学习预测数据中心慢节点的方法。
- [**Live Gradient Compensation for Evading Stragglers in Distributed Learning**](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9488815)：清华深研院发表于 INFOCOM 21。通过梯度补偿机制，解决较慢工作节点拖累训练速度的问题，并能保证训练快速收敛
- [Gradient Coding: Avoiding Stragglers in Distributed Learning](http://proceedings.mlr.press/v70/tandon17a/tandon17a.pdf)：在同步场景下通过复制数据和编码梯度，容忍一部分错误和慢节点
- [Fast Distributed Deep Learning via Worker-adaptive Batch Sizing](https://arxiv.org/pdf/1806.02508v1.pdf)：根据节点处理容量分配数据批大小，使较慢的节点处理更少的数据（这种方式的问题在于，完全认为慢节点是由于计算容量限制造成的）
- [**Straggler-Resilient Distributed Machine Learning with Dynamic Backup Workers**](https://arxiv.org/pdf/2102.06280.pdf)：发表在 Arxiv 上。为了解决慢节点问题，一个方式是中心节点只聚合一部分工作节点的梯度，未被聚合的工作节点称为 Backup Workers。
  - 通过一个分布式算法确定每个工作节点的备份工作节点数
  - 实验数据集有点小
  - 有收敛性分析

### GPU Scheduling

- Gandiva: Introspective Cluster Scheduling for Deep Learning
- TON'23, Deep Learning-Based Job Placement in Distributed Machine Learning Clusters With Heterogeneous Workloads
- SOCC'22, [Anticipatory Resource Allocation for ML Training](https://dl.acm.org/doi/pdf/10.1145/3620678.3624669)
- [Pollux: Co-adaptive Cluster Scheduling for Goodput-Optimized Deep Learning](https://cn287zbjkb.feishu.cn/docx/XWdhdYaxDoncKBxlJBhcbL3Xnwd)：基于**模型超参**来优化放置任务
	- https://zhuanlan.zhihu.com/p/442196995
- [THEMIS: Fair and Efficient GPU Cluster Scheduling](https://www.usenix.org/system/files/nsdi20-paper-mahajan.pdf)： **考虑任务公平性**的GPU资源分配机制。
- [CASSINI: Network-Aware Job Scheduling in Machine Learning Clusters](https://arxiv.org/pdf/2308.00852.pdf)：结合ML训练任务流量特点的带宽分配机制。通过调整任务开始时间，使带宽错峰分配。
- Tessel: Boosting Distributed Execution of Large DNN Models via Flexible Schedule Search

#### Resource Fragmentation Problem

- ATC 23, [Beware of Fragmentation Scheduling GPU-Sharing Workloads with Fragmentation Gradient Descent](https://cse.hkust.edu.hk/~weiwa/papers/fgd-atc23.pdf)