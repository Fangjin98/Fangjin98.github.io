---
title: Summary of SIGCOMM 22
date: 2022-09-03 13:34:32
tags:
    - Paper Reading
    - Summary
---

[SIGCOMM 22](https://conferences.sigcomm.org/sigcomm/2022/) contains 11 technical sessions and 55 papers are accepted.

1. _Datacenter Networking_
2. 5G Networks
3. Congestion Control
4. Wide Area Networks
5. _Testing and Verification_ (most of them mentioned programmable dataplane)
6. Machine Learning
7. _Monitoring and Measurement_
8. Sensing and Wireless Communication
9. _Programmable Data Planes_
    - Predictable vFabric on Informative Data Plane
    - Using trio: juniper networks' programmable chipset - for emerging in-network applications
    - Thanos: Programmable Multi-Dimensional Table Filters for Line Rate Network Functions (hard core)
    - Stateful Multi-Pipelined Programmable Switches (same author as the above paper)
    - FAst In-Network GraY Failure Detection for ISPs
10. Denial of Service Defense and Storage Networks
11. Host Networking and Video Delivery

### Interested Papers

- [Jupiter Evolving: Transforming Google’s Datacenter Network via Optical Circuit Switches and Software-Defined Networking](https://research.google/pubs/pub51587/)
- [Aequitas: Admission Control for Performance-Critical RPCs in Datacenters](https://yiwenzhang92.github.io/assets/docs/aequitas-sigcomm22.pdf): Targeting guarteeing SLO of RPCs
- [Cebinae: Scalable In-network Fairness Augmentation](https://liangchengyu.com/doc/cebinae-sigcomm2022.pdf): Enabling the fairness among different congestion control protocols with programmable switches
- [FlyMon: Enabling On-the-Fly Task Reconfiguration for Network Measurement](https://yangtonghome.github.io/uploads/sigcomm22-flyMon-final220.pdf): Sketch-based measurement system that can make on-the-fly reconfigurations on a large set of measurement tasks
- [Design and Evaluation of IPFS: A Storage Layer for the Decentralized Web](https://research.protocol.ai/publications/design-and-evaluation-of-ipfs-a-storage-layer-for-the-decentralized-web/trautwein2022.pdf): Illustrating the implementation of IPFS, the largest and most widely used Decentralized Web platform
- [Using trio: juniper networks' programmable chipset - for emerging in-network applications](https://dl.acm.org/doi/pdf/10.1145/3544216.3544262)：Mentioned INA

### Jupiter Evolving: Transforming Google’s Datacenter Network via Optical Circuit Switches and Software-Defined Networking

Google proposed a new datacenter architecture in this paper.

- A datacenter  interconnection layer
- Centralized SDN controller for traffic engineering
- Automated network operations for topology engineering

The combination of traffic and topology engineering  on direct-connect fabrics achieves simliar throughput as Clos fabrics for Google's production traffic patterns.

The paper targets the challenge of _incremental refresh_ of the network infrastructure. Since the typical Clos network requires pre-building spine at the maximum-scale, which may derated the bandiwidth of links to aggregation block.

1. spine层一旦建好，难以修改，因为这需要很大的成本
2. spine层的带宽会限制后续更新的其他模块带宽，造成计算和网络资源失配

为了解决Clos架构难以增量更新的问题，这篇论文提出了一个新的架构，包含对应的网络管理，流量和拓扑工程。该架构能够在流量不确定，集群异构的场景下工作。

### Aequitas: Admission Control for Performance-Critical RPCs in Datacenters

Another paper of Google, targeting guarteeing SLO of RPCs.

Traditional traffic classification categories cannot sufficiently capture their importance due to wide variations in RPC characteristics.

As of 2021, _RPCs generate 95%+ of the application traffic in Google production datacenters_, of which ∼75% is to and from storage systems.

An RPC is a programmatic request for action or information between components of applications, and it can consist of dozens of individual packets. Hundreds of RPCs can be on the critical path to completing an application-level operation.

### Cebinae: Scalable In-network Fairness Augmentation

Enabling the fairness among different congestion control protocols with programmable switches. 

现有拥塞控制协议的多样性会导致租户资源占用不公平，Cebinae通过惩罚超过max-min份额的流，增强现有网络。

Key insights

1. High-level flow scheduling is enough: > it suffices for the network to redistribute bandwidth from flows that have met/exceeded their fair share to flows that have not.
2. Advanced scheduling logic can be adopted based on the above simplification.

Open sourced in https://github.com/eniac/Cebinae

### FlyMon: Enabling On-the-Fly Task Reconfiguration for Network Measurement

一作是南大，三作是北大杨仝。

Sketch-based measurement system that can make on-the-fly reconfigurations on a large set of measurement tasks.

> This paper may be useful for my future research.
