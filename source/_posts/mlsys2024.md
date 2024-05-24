---
title: Selected MLsys Papers Published on Top-Conferences
date: 2024-05-24 21:21:52
tags:
 - LLM Training
 - Sparse Model
 - Distributed Training
 - Conference
---

This post lists some papers published on top-conferences (e.g., NSDI'24, OSDI'24, ASPLOS'24, Eurosys'24) about MLsys or LLM.

## Systems

### GPU Cluster

- [NSDI’24] MegaScale: Scaling Large Language Model Training to More Than 10,000 GPUs：字节万卡集群实践
- [NSDI’24] Resiliency at Scale: Managing Google’s TPUv4 Machine Learning Supercomputer
	- 容错路由指的是容什么错？
- [NSDI'24] Characterization of Large Language Model Development in the Datacenter
- [ASPLOS’24] TCCL: Discovering Better Communication Paths for PCIe GPU Clusters

### Networking

- [NSDI’24] Towards Domain-Specific Network Transport for Distributed DNN Training
- [NSDI’24] Swing: Short-cutting Rings for Higher Bandwidth Allreduce

### Scheduling

- [ASPLOS’24] Centauri: Enabling Efficient Scheduling for Communication-Computation Overlap in Large Model Training via Communication Partitioning
- [NSDI’24] Parcae: Proactive, Liveput-Optimized DNN Training on Preemptible Instances
	- 什么是spot实例
	- 这里的并行化策略主要影响bubble是吗？
- [NSDI’24] CASSINI: Network-Aware Job Scheduling in Machine Learning Clusters

### Parallelism

- [Eurosys'24] Aceso: Efficient Parallel DNN Training through Iterative Bottleneck Alleviation：根据集群配置和模型参数，生成合适的并行化配置（DP、PP、TP size）。不用传统最优化方法，使用梯度下降法迭代寻找配置。
- [ASPLOS'24] AdaPipe: Optimizing Pipeline Parallelism with Adaptive Recomputation and Partitioning：流水线并行会带来资源不均，重计算会带来额外的计算。因此确定流水线和重计算阶段的划分，来最大化内存利用率。
- [ASPLOS'24, Best Paper] Centauri: Enabling Efficient Scheduling for Communication-Computation Overlap in Large Model Training via Communication Partitioning：提出一个并行化抽象，并从三个维度进行划分，实现细粒度并行/重叠。

## ML Related

### LLM Training

- [Eurosys'24] ScheMoE: An Extensible Mixture-of-Experts Distributed Training System with Tasks Scheduling：提出一个 MoE 训练系统
	- 提出了一个通用路由框架
	- 提出一个all-to-all算法
	- 允许用户自定义all-to-all算法和压缩机制
- [Eurosys'24] DynaPipe: Optimizing Multi-task Training through Dynamic Pipelines：大语言模型接收的text长度可变，因此提出可变micro-batching机制来训练大语言模型
- [NSDI’24] DISTMM: Accelerating Distributed Multimodal Model Training
	- 多模态的模型拆分和常见的模型拆分有啥不同？

### LLM Serving

LLM 推理请求由两部分组成：prefill 和 decoder，两部分特点不同，因此现有工作针对这两部分内容进行优化。

- [OSDI'24] Taming Throughput-Latency Tradeoff in LLM Inference with Sarathi-Serve：基于已有工作调度prefill和decoder阶段。
- [OSDI'24] DistServe: Disaggregating Prefill and Decoding for Goodput-optimized Large Language Model Serving：解耦prefill和decoding处理
- [OSDI'24] Fairness in Serving Large Language Models
- [OSDI'24] ServerlessLLM: Locality-Enhanced Serverless Inference for Large Language Model

### Sparse

- [NSDI'24] Accelerating Neural Recommendation Training with Embedding Scheduling：类似于梯度压缩工作。嵌入层存在零值，细粒度确定嵌入层哪部分应该训练，来降低系统负载。
- [ASPLOS’24] FEASTA: A Flexible and Efficient Accelerator for Sparse Tensor Algebra in Machine Learning
- [ASPLOS’24] ACES: Accelerating Sparse Matrix Multiplication with Adaptive Execution Flow and Concurrency-Aware Cache Optimizations：提出一个accelerator来适应灵活的稀疏矩阵相乘
