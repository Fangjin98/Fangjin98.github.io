---
title: Survey of  In-network Aggregation
date: 2022-01-04
tags:
   - Paper Reading
   - Summary
   - In-network Aggregation
---

Reducing the number of gradient transfered by hosts throughput in-network aggregation is studyed by lots of reseachers before. In this post, I will summary the common technologies of in-network aggregation.

### Software Implementation

1. NetAgg: Implement in-network aggregation via switch-attached high-performance middleboxes.
2. CamDoop: They use servers in a direct-connect network topology.

### Hardware Implementation

1. DAIET: Furthermore, it (refer to in-network aggregation) can help reducing network traffic, so as to alleviate congestion, which is a major cause of application performance degradation
2. SHARP: Implement in dedicated switches, and the function is programmed in the chip.
3. iSwitch: Aiming at asynchronous RL training, which has a much smaller model size than the size of a typical DNN model. Thus, they can store the total model into the memory of programmable switches.
4. SwitchML: Using a programmable switch to replace the PS to aggregate the gradients.
5. ATP: Using programmable switches. However, they adopt static routing scheme, may leading to poor performance.