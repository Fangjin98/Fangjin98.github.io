---
title: Survey of In-network Aggregation
date: 2023-02-15
tags:
   - Paper Reading
   - Summary
   - In-network Aggregation
---

In-network aggregation is studyed by lots of reseachers. This post contains a list of related papers and projects.

### Open Source Codes

- <https://github.com/Princeton-Cabernet/p4-projects>

### Published in 2023

- A Generic Service to Provide In-Network Aggregation for Key-Value Streams: ASPLOS 23, **the authors seems to be the same team as of ATP**

### Published in 2022

- [Using trio: juniper networks' programmable chipset - for emerging in-network applications](https://dl.acm.org/doi/pdf/10.1145/3544216.3544262)：SIGCOMM 22, mentioned INA in Section Use Case.
- [Taurus: a data plane architecture for per-packet ML](https://arxiv.org/pdf/2002.08987.pdf): ASPLOS 22, per packet inference.
- [Holistic Resource Scheduling for Data Center In-Network Computing](https://linwang.info/papers/ton22-hire.pdf): **first INC related paper published in ToN**, authored by [Lin Wang](https://linwang.info/)
- [Distributed DNN Serving in the Network Data Plane](https://linwang.info/papers/europ422-p4dnn.pdf): EuroP4 22

### Published in 2021

- [ATP: In-network Aggregation for Multi-tenant Learning](https://www.usenix.org/conference/nsdi21/presentation/lao): **Best paper of NSDI 21**
- [Scaling Distributed Machine Learning with In-Network Aggregation](https://www.usenix.org/conference/nsdi21/presentation/sapio): NSDI 21, focusing on network protocol
- [In-Network Aggregation for Privacy-Preserving Federated Learning](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9664035): ICT-DM 2021, adopting INA in federated learning.
- [In-network Aggregation for Shared Machine Learning Clusters](https://proceedings.mlsys.org/paper/2021/hash/eae27d77ca20db309e056e3d2dcd7d69-Abstract.html): MLSys 2021, focusing on routing.
- [P4COM: In-Network Computation with Programmable Switches](https://arxiv.org/pdf/2107.13694.pdf)
- [Switches for HIRE: Resource Scheduling for Data Center In-Network Computing](https://linwang.info/papers/asplos21-hire.pdf): ASPLOS 21.
- [Don't You Worry 'Bout a Packet: Unified Programming for In-Network Computing](https://dl.acm.org/doi/pdf/10.1145/3484266.3487395): HotNets'21, focusing on **programming language**

### Published in 2019

- [Accelerating Distributed Reinforcement Learning with In-Switch Computing](https://ieeexplore.ieee.org/abstract/document/8980345): ISCA 19, preseting a noval switch arch.

### Eariler

- NetAgg: Implement in-network aggregation via switch-attached high-performance middleboxes.
- CamDoop: They use servers in a direct-connect network topology.
- DAIET: Furthermore, it (refer to in-network aggregation) can help reducing network traffic, so as to alleviate congestion, which is a major cause of application performance degradation
- SHARP: Implement in dedicated switches, and the function is programmed in the chip.