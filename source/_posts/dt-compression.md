---
title: Compression Works for Sparse Model Training
date: 2024-03-26 15:11:49
tags:
 - LLM Training
 - Sparse Model
 - Distributed Training
---

[模型稀疏化是未来大模型发展的趋势](https://mp.weixin.qq.com/s/kpuxrDg2qpVNY2JsHFzbyQ)，其中包括：

- 激活稀疏性：Attention 编码呈对焦聚焦，特殊token与邻近token的注意力得分比较高
- 权重稀疏性：Linear 层权重矩阵中较少比例的 outliers 或敏感值，对推理精度起重要作用
- 梯度稀疏性：包含了大量 embedding 层权重，具有非零数值通常集中在部分区域（**只有对应 batch 部分有非零值，其他部分为零**）。

为了克服稀疏化数据的影响，现有工作提出了权重压缩和梯度压缩工作。
现有工作主要集中在软件层面研究如何进行梯度压缩（例如参数调优，模型架构调优），但是会导致端侧工作量增加，从而抵消通信量/参数量减少带来的好处。

## MoE Model Distributed Training

### Model Architecture

传统 Transformer 模型层包含 Multihead Self-Attention (MSA) 和 Feed Forward Network (FFN) 模块，MoE 模块替代传统 Transformer 中的 FFN 模块，包含 1 个 Router 和多个 FFN，其中的一个 FFN 被称为一个专家。

多个 Transformer 层组成一个大模型。根据 Transformer 层的功能可以区分成 Encoder 和 Decoder。
Encoder 通常为 MSA+FFN/MoE，Decoder 通常为  MSA+MLP(全联接层)。

### Expert Parallel

随着专家数变多，专家会分散在不同设备上，因此提出专家并行(Expert Parallel, EP)。
Router 根据策略将每张卡的输入 token 路由到不同专家上。
例如 Top-k 策略将 token 分配给概率最高的 k 个专家。

专家并行需要在 EP 域不同的卡之间引入 All-to-All 通信，收集每个专家负责的token。根据收集和分配一共需要 2 次 All-to-All。
由于 All-to-All 通信需求均匀且多对多通信，每个专家具有相同的 capacity，多余的 token 会被丢弃，造成模型精度下降。

> 通信域： Router 在每一路 DP 上存在相同的副本，不同 DP 下同一 EP 域内的卡间通信。

### Sequence Parallel

单机无法处理超长输入序列，因此划分多个子序列给不同设备处理，称为序列并行 (Sequence Parallel, SP)。
SP 将 Layer Normalization 和 Dropout 进一步划分给不同设备上，相当于每个卡负责部分 Sequence 训练参数。
引入 Ring Self-Attention 模组代替原先 Self-Attention 模组，训练过程中需要交换各自的Query、Key、Value embeddings（All-to-All通信）。

> 通信内容：
>
> - 前向传递：Attention 部分需要2次 ring-P2P，MLP部分被TP切割，需要新增Linear1前1次 All-gather，Linear2后1次 Reduce scatter。
> - 反向传递：MLP部分1次 allgather和1次reduce scatter。Attention可以复用1次allreduce通信。

### Related Papers

一些其他大模型训练相关的经典论文：

- ZeRO++: Extremely Efficient Collective Communication for Giant Model Training
- DeepSpeed-MoE: Advancing Mixture-of-Experts Inference and Training to Power Next-Generation AI Scale
- [Colossal-AI A Unified Deep Learning System For Large-Scale Parallel Training](https://arxiv.org/pdf/2110.14883.pdf)
- Efficient Large-Scale Language Model Training on GPU Clusters Using Megatron-LM
- GPipe: Efficient Training of Giant Neural Networks using Pipeline Parallelism

## Existing Work

### Model (Weight Matrix) Compression

> 权重矩阵压缩多用于优化端侧内存读写，提高 cache 命中率，增加计算和访存的吞吐率。
> MoE 模型训练引入了大量权重矩阵、Attention层的通信内容，这类稀疏通信内容如何优化还未被讨论。

针对稀疏权重压缩主要有结构化、半结构与非结构实现方式。

1. 结构化稀疏剪枝，粗粒度规整剪枝，压缩率提升，难以保证模型精度
2. 半结构化稀疏，粒度较细，压缩率与精度受规整性影响
3. 非结构稀疏化，粒度最细，高稀疏度下精度效果最好，但是压缩与加速收益取决于软硬件实现方法

### Gradient Compression

在分布式训练过程中，梯度通常用于数据并行阶段，不同节点进行全局更新的聚合操作。
现有工作聚焦如何设计通信、压缩策略，让稀疏梯度能够被高效聚合。

- Gradient Compression Supercharged High-Performance Data Parallel DNN Training
- [Efficient Sparse Collective Communication and its Application to Accelerate Distributed Deep Learning](https://conferences.sigcomm.org/sigcomm/2021/files/papers/3452296.3472904.pdf)：设计流式算法，包含协议设计，将梯度划分为block，按block传输数据，只传输非零数据
- [Accelerating Distributed Deep Learning using Lossless Homomorphic Compression](https://arxiv.org/pdf/2402.07529.pdf)：同态压缩，纯算法工作，设计机器学习压缩算法，支持在交换机上直接聚合
- [THC: Accelerating Distributed Deep Learning Using Tensor Homomorphic Compression](https://arxiv.org/pdf/2302.08545.pdf)：结合同态压缩设计网内聚合系统，交换机只负责聚合。
  - Count Sketch (CS): an offline algorithm, that needs an index table and aggregated results. Not implemented in Tofino yet. Can be used in the DP phase.
