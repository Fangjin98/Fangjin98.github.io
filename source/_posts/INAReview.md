---
title: Research on In-network Aggregation
date: 2022-01-04
tags:
   - paper reading
---
Reducing the number of gradient transfered by hosts throughput in-network aggregation is studyed by lots of reseachers before. In this post, I will summary the common technologies of in-network aggregation.

## Implementing in-network aggregation through software

1. NetAgg: Implement in-network aggregation via switch-attached high-performance middleboxes.
2. CamDoop: They use servers in a direct-connect network topology.

## Implementing in-network aggregation through hardware

1. DAIET: Furthermore, it (refer to in-network aggregation) can help reducing network traffic, so as to alleviate congestion, which is a major cause of application performance degradation
2. SHARP: Implement in dedicated switches, and the function is programmed in the chip.
3. iSwitch: Aiming at asynchronous RL training, which has a much smaller model size than the size of a typical DNN model. Thus, they can store the total model into the memory of programmable switches.
4. SwitchML: Using a programmable switch to replace the PS to aggregate the gradients.
5. ATP: Using programmable switches. However, they adopt static routing scheme, may leading to poor performance.

**KEYWORDS**

- FPGA based programmable switches.
- aggregate the entire gradient vector

**FEATURES**

- consider the impact of in-network aggregation to synchronous training and asynchronous training
  - Synchronous: reduce end-to-end latency.
  - Asynchronous: convergence with faster weight updates.
- Hierarchical aggregation at the rack scale.
  - The switch will forward the aggregated segment to the switches in the higher level for global aggregation.
  - The switch will select the one with the smallest value of IP address among the multiple higher level switches.
- The control plane  maintains a member ship table for the current training job.
- **Asynchronous training: Local gradient computing, gradient aggregation and weight update can be pipelined.**

<!-- **CHALLENGES**

- Deadlock: the simultaneous and uncoordinated execution of multiple reduction operations may result in several reduction operations waiting for  the same AN resources, allowing none to complete.
- Fault tolerance:
    - transport-level errors
    - end-node errors
    - protocol errors
- Floating point numbers should be calculated in a specific order not the arriving order.

**FEATURES**

- Aggregation request header
    - data type
    - data size
    - the number of elements
    - aggregation operation to be performed (eg. min or sum)
- performs the aggregation operation *once all the expected requests arrive*.

--- -->

<!-- ## **SwitchMl**

**CHALLENGES**

- limited memory: solving it by streaming the gradient to aggregate.
- limited computation: move the floating-point calculation and division execution into workers.

**FEATURES**

- workers using self-clocked scheme to manage the memory of the switch.

**SHORTAGES** -->