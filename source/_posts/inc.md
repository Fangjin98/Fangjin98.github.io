---
title: In-network Computing Research
date: 2023-12-22 23:07:48
tags:
 - Summary
---

In-network computing adopts programmable network devices (e.g., programmable switches) to perform complex operations, while forwarding packets.

This post presents some representative works in the field of in-network computing.

### In-network Aggregation

See this [post](/2023/07/03/ina/) for details.

### In-network Cache

Representative group: [Xin Jin](https://xinjin.github.io/).

- SOSP 17, NetCache: Balancing Key-Value Stores with Fast In-Network Caching
- SIGCOMM 20, NetLock: Fast, Centralized Lock Management Using Programmable Switches
- NSDI 18, NetChain: Scale-Free Sub-RTT Coordination

### In-network Virtual Functions

This area of works adopt programmable switches (or smart NICs) to implement the hardware gateway, to improve the traffic throughput in the cloud.

- SIGCOMM 17, SilkRoad: Making Stateful Layer-4 Load Balancing Fast and Cheap Using Switching ASICs
- HotNets 19, Accelerated Service Chaining on a Single Switch ASIC
- SIGCOMM 21, **Sailfish: Accelerating Cloud-Scale Multi-Tenant Multi-Service Gateways with Programmable Switches**
- NSDI 22, Elixir: A High-performance and Low-cost Approach to Managing Hardware/Software Hybrid Flow Tables Considering Flow Burstiness
- NSDI 22, Tiara: A Scalable and Efficient Hardware Acceleration Architecture for Stateful Layer-4 Load Balancing

### In-network Measurement

In-network measurement is usually achieved by implementing sketch algorithms with programmable switches, to perform fine-grained measurement.

- NSDI 21, Toward Nearly-Zero-Error Sketching via Compressive Sensing
- SIGCOMM 19, BeauCoup: Answering Many Network Traffic Queries, One Memory Update at a Time
- SIGCOMM 20, Flow Event Telemetry on Programmable Data Plane
- SIGCOMM 22, FlyMon: Enabling On-the-Fly Task Reconfiguration for Network Measurement
- NSDI 23, Sketchovsky: Enabling Ensembles of Sketches on Programmable Switches

### Others

- SIGCOMM 23, NetClone: Fast, Scalable, and Dynamic Request Cloning for Microsecond-Scale RPCs
- NSDI 24, THC: Accelerating Distributed Deep Learning Using Tensor Homomorphic Compression