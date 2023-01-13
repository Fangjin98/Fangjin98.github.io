---
title: Reading Summary of NetHint
tags:
 - paper reading
 - NSDI
---
> Why do we need a white-box network?
> How to realize a white-box network?
> How to utilize a white-box network?

## Motivation

Due to the emergence of data-intensive applications, the traditional black-box network doesn't suit the needs of cloud tenants and providers. The cloud tenant is unaware of the network characteristics, and the cloud provider is unaware of the application communication semantics and the transfer schedule. This mismatch incurs low performance and efficiency for data-intensive applications.

To address this issue, this paper proposes the NetHint, a mechanism for a cloud tenant and cloud provider to interact to enhance the application performance jointly, by providing a hint (an indirect indication of the bandwidth allocation) to a cloud tenant. NetHint mainly answers the following three questions:

1. What information should the hint contain?
2. How to provide this hint at a low cost?
3. How should applications react to the hint?

## Background

### Black-box Network

Nowadays, black-box network abstraction is a per-VM bandwidth allocation at the end hosts. Therefore, tenants are unaware of the underlying network characteristics and cannot predict their network performance. 

*The authors present an example of Allreduce with 4 VMs in the paper (Sec. 2.1).*

### Data-intensive Applications

Many distributed data analytics workloads contain network-intensive shuffle phases between different job stages. Given network characteristics, distributed data analytics applications can change their transfer schedules (by changing the task placement) to minimize shuffle completion time.

The black-box nature of the existing networking abstraction and the adaptiveness of data-intensive applications create a mismatch. Data-intensive applications would benefit from more network information from the cloud provider to configure their transfer schedules, but black-box networking hides this information. To address this mismatch, the authors propose the NetHint.

## Overview

The key idea of NetHint is that the provider provides a hint — an *indirect indication* of the underlying network characteristics (e.g., a virtual link-layer topology for a tenant's VMs, number of co-located tenants, network bandwidth utilization) to a cloud tenant.

The provider provides a NetHint service, which periodically (100 ms by default) collects the hint information to capture changes of the underlying network characteristics. A tenant application can query the NetHint service to get the hint information, and then adapt its transfer schedules based on this provided hint.

NetHint describes a virtual link-layer topology that connects a tenant's VMs. In addition, NetHint provides to the tenant recent utilization summaries and counts of co-locating tenant connections on shared network links in the virtual topology.

The network traffic can be measured in the physical switches using network telemetry. However, this depends on specific programmable switch features. One alternative is each machine monitors local flows and transmits statistics to one dedicated machine, which runs a NetHint server process to aggregate the rack-level information. These NetHint servers use all-to-all communication to exchange information.

The tenants can make use of the NetHint information via simple scheduling algorithms.

## Others

- Sec. 4 illustrate the realization of NetHint.
- Sec. 5 illustrates how to adapt to NetHint's hints.

Evaluation results show that NetHint improves the average performance of allreduce completion time, broadcast completion time, and MapReduce shuffles completion time by **2.7×**, **1.5×**, and **1.2×**, respectively.
