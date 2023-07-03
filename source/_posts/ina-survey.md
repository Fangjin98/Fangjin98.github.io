---
title: Survey of In-network Aggregation
date: 2023-07-03
tags:
   - Paper Reading
   - Summary
   - In-network Aggregation
---

In-network aggregation is studied by lots of reseachers, such as 

- [Wenfei Wu](http://wenfei-wu.github.io/) at PKU
- [Lin Wang](https://linwang.info/) at VU Amsterdam

This post includes a list of related papers and projects.

### Published in 2023

In this year, some works are proposed to simplify the development and expand the application scenario of in-network aggregation.

- ClickINC: In-network Computing as a Service in Heterogeneous Programmable Data-center Networks, SIGCOMM 23, Wenfei Wu
- NetRPC: Enabling In-Network Computation in Remote Procedure Calls, NSDI 23, Wenfei Wu
- A Generic Service to Provide In-Network Aggregation for Key-Value Streams, ASPLOS 23 (Distinguished Paper Award), Wenfei Wu
- [In-Network Aggregation with Transport Transparency for Distributed Training](https://mcanini.github.io/papers/netreduce.asplos23.pdf), ASPLOS 23, Wenfei Wu

Additionaly, some works are proposed to improve the performance of in-network aggregation.

- A2TP: Aggregator-aware In-network Aggregation for Multi-tenant Learning, Eurosys 23, Zhaoyi Li at CSU

### Published in 2022

In fact, papers listed below do not strictly relate to in-network **aggregation**. They either discuss the performance of novel programmable chip under INA workloads (trio) or propose works on running tasks related to DNN with programmable switches.

- [Using trio: juniper networks' programmable chipset - for emerging in-network applications](https://dl.acm.org/doi/pdf/10.1145/3544216.3544262), SIGCOMM 22, Mingran Yang at MIT
- [Taurus: a data plane architecture for per-packet ML](https://arxiv.org/pdf/2002.08987.pdf): ASPLOS 22, Tushar Swamy at Stanford: Proposing a FPGA-based prototype to run per packet inference at programmable switches
- [Holistic Resource Scheduling for Data Center In-Network Computing](https://linwang.info/papers/ton22-hire.pdf),TON , Lin Wang group
- [Distributed DNN Serving in the Network Data Plane](https://linwang.info/papers/europ422-p4dnn.pdf), EuroP4 22, Lin Wang group

### Published in 2021

- [ATP: In-network Aggregation for Multi-tenant Learning](https://www.usenix.org/conference/nsdi21/presentation/lao), NSDI 21 (**best paper award**), Wenfei Wu group
- [Scaling Distributed Machine Learning with In-Network Aggregation](https://www.usenix.org/conference/nsdi21/presentation/sapio), NSDI 21, Microsoft: This work was proposed in 2019, focusing on in-network aggregation with one switch
- [In-Network Aggregation for Privacy-Preserving Federated Learning](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9664035), ICT-DM 2021: Performing federated learning with in-network aggregation
- [In-network Aggregation for Shared Machine Learning Clusters](https://people.csail.mit.edu/ghobadi/papers/panama.pdf), MLSys 2021, Manya Ghobadi at MIT: Focusing on routing protocol with in-network aggregation
- [P4COM: In-Network Computation with Programmable Switches](https://arxiv.org/pdf/2107.13694.pdf), Arxiv, Ge Chen at Alibaba

Some papers focus on improving peformance of in-network **computing** from resource scheduling or programming language.

- [Switches for HIRE: Resource Scheduling for Data Center In-Network Computing](https://linwang.info/papers/asplos21-hire.pdf), ASPLOS 21, Lin Wang group
- [Don't You Worry 'Bout a Packet: Unified Programming for In-Network Computing](https://dl.acm.org/doi/pdf/10.1145/3484266.3487395), HotNets 21, Lin Wang group

### Published in 2019

- [Accelerating Distributed Reinforcement Learning with In-Switch Computing](http://jianh.web.engr.illinois.edu/platformx/papers/iswitch-isca2019.pdf): ISCA 19, Youjie Li at UIUC

### Eariler

- DAIET: a system for data aggregation inside the network, SoCC 17: Preliminary work of SwitchML
- [Scalable Hierarchical Aggregation Protocol (SHArP): A Hardware Architecture for Efficient Data Reduction](https://network.nvidia.com/related-docs/solutions/hpc/paperieee_copyright.pdf),COMHPC 16, NVIDIA: Proposing a dedicated switch architecture to perform in-network aggregation (reduction)
- [NetAgg: Using Middleboxes for Application-specific On-path Aggregation in Data Centres](https://conferences.sigcomm.org/co-next/2014/CoNEXT_papers/p249.pdf), CoNEXT 14: Implement in-network aggregation via switch-attached high-performance middleboxes
- Camdoop: Exploiting In-network Aggregation for Big Data Applications, NSDI 12: They use servers in a direct-connect network topology to perform in-network aggregation

### Open Sourced Codes

Some useful codes for p4 beginners.

- [Source codes of SwitchML](https://github.com/p4lang/p4app-switchML)
- https://github.com/Princeton-Cabernet/p4-projects