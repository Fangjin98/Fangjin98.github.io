---
title: Fault Injection Research
date: 2023-12-21 23:29:55
tags:
  - Summary
---

### Existing Works

- [故障演练 Chaos](https://www.aliyun.com/product/aliware/ahas/chaos)
- [火山引擎混沌工程之云原生场景实现](https://developer.volcengine.com/articles/7257050491912192019)
- [字节跳动异构场景下的高可用建设实践](https://developer.volcengine.com/articles/7041808990837145636)
- [AWS FIS](https://aws.amazon.com/cn/fis/)
  - [AWS Fault Injection Simulator](https://aws.amazon.com/cn/blogs/aws/aws-fault-injection-simulator-use-controlled-experiments-to-boost-resilience/)
  - Can select the target _figures by type, tag, ARN, or by querying for specific attributes. 
  - Can stop the experiment if one or more stop conditions (as defined by CloudWatch Alarms) are met.
- [Alibaba](https://help.aliyun.com/document_detail/185036.html)
  - 只能**针对单个实例设置故障**
  - 提供的故障注入配置项较多，能够设置流量精确匹配，设置的一些内容和AWS在会场上说的都比较一致。
- [Huawei](https://www.huaweicloud.com/guide/category-17376220)
  - 配置项是简单的开启关闭，开启多久，故障概率，**没有实现流量精确匹配**，也不能制定故障行为（时延，包损坏等）
- [awesome-chaos-engineering](https://github.com/dastergon/awesome-chaos-engineering)
- [ChaosBlade](https://github.com/chaosblade-io/chaosblade)：阿里开源的故障注入工具。
- [**Chaos Mesh**](https://chaos-mesh.org/)
  - [Github Repo](https://github.com/chaos-mesh/chaos-mesh): Implimented by Go.
  - [Supported network failures](https://chaos-mesh.org/docs/simulate-network-chaos-on-kubernetes/)

---

- NSDI 11, [FATE and DESTINI: A Framework for Cloud Recovery Testing](https://dsf.berkeley.edu/papers/nsdi11-fate-destini.pdf): Testing *cloud services* with system failure injection.
- NSDI 12, [A NICE Way to Test OpenFlow Applications](https://www.usenix.org/system/files/conference/nsdi12/nsdi12-final105.pdf): *OpenFlow* applications.
- HotCloud 13, [Towards a Fault-Resilient Cloud Management Stack](https://www.usenix.org/system/files/conference/hotcloud13/hotcloud13-ju.pdf): *Openstack*
- ASE 20, [CoFI: Consistency-Guided Fault Injection for Cloud Systems](https://web.cse.ohio-state.edu/~qin.34/pub-papers/CoFI-ASE20.pdf): *network paration* fault
- OSDI 22, [Automatic Reliability Testing for Cluster Management Controllers](https://www.usenix.org/system/files/osdi22-sun.pdf):*k8s* applications.
- NSDI 23, [Push-Button Reliability Testing for Cloud-Backed Applications with Rainmaker](https://www.usenix.org/system/files/nsdi23-chen-yinfang.pdf) : *dot Net* Applications, Rainmaker puts its focus on transient errors faced by cloud-backed applications
- [VirtualWire: a fault injection and analysis tool for network protocols](https://ieeexplore.ieee.org/document/1203468), ICDCS 2003: with a fault specific language
- ThorFI: A Novel Approach for Network Fault Injection as a Service: targeting OVS network failures, implemented with Openstack
- [Observability and Chaos Engineering on System Calls for Containerized Applications in Docker](https://arxiv.org/abs/1907.13039): targeting system call in docker
- [Maelstrom: Mitigating Datacenter-level Disasters by Draining Interdependent Traffic  Safely and Efficiently](https://www.usenix.org/system/files/osdi18-veeraraghavan.pdf)
- [Using Chaos Engineering to Improve The Resiliency of Transportation Cyber Physical Systems: A Novel Approach to the Test and Evaluation of Complex Systems](https://ep.jhu.edu/wp-content/uploads/2021/08/GLRC14_v4.pdf)

### Network Faults

- SIGCOMM 11, [Understanding Network Failures in Data Centers: Measurement, Analysis, and Implications](https://conferences.sigcomm.org/sigcomm/2011/papers/sigcomm/p350.pdf)
- OSDI 18, [An Analysis of Network-Partitioning Failures in Cloud Systems](https://www.usenix.org/system/files/osdi18-alquraan.pdf)
- TON 19, [Understanding the Limits of Passive Realtime Datacenter Fault Detection and Localization](https://ieeexplore.ieee.org/abstract/document/8836620): Moreover, failures are not always obvious; network components can fail partially, dropping or delaying only subsets of packets. Thus, traditional fault detection techniques involving end-host or router-based statistics can fall short in their ability to identify these errors. 
- NSDI 21, [**Debugging Transient Faults in Data Centers using Synchronized Network-wide Packet Histories**](https://www.usenix.org/system/files/nsdi21-kannan.pdf)
- [Understanding and Mitigating Packet Corruption in Data Center Networks](https://dl.acm.org/doi/pdf/10.1145/3098822.3098849)

### Testing

- [Frisbee: automated testing of Cloud-native applications in Kubernetes](https://arxiv.org/pdf/2109.10727.pdf)
- [Test Coverage for Network Configurations](https://ratul.org/papers/nsdi2023-netcov.pdf)
- [Norma: Towards Practical Network Load Testing](https://ennanzhai.github.io/pub/nsdi23fall-norma.pdf)