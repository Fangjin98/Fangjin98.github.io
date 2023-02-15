---
title: One Switch is Not Enough, What about More Switches?
date: 2022-12-2 14:35:22
tags: 
 - Programmable Network
 - Distributed Training
 - In-network Aggregation
mathjax: true
---

> This work is a continuation of the gradient routing (see this [post](/2023/02/10/GradientRouting/)).
> ~~INFOCOM23: (Rejected) Scores 3 3 3.~~

By aggregating gradients in programmable switches, multiple gradients can be reduced to 1 aggregated gradient, thus mitigating the communication overhead. However, the aggregation performance is limited by its on-chip memory size.

### How Do Exsiting Methods Aggregate Gradient in Programmable Switches?

Existing solutions adopt the *memory sharing scheme* to conduct in-network aggregation.

In particular, the switch memory is divided into $N$ memory units, each of which can store a part of gradients (i.e., gradient fragments) at a time.

Correspondingly, the gradient is divided into $M$ fragments, *each having the same size as the memory unit*. When one fragment arrives at a switch, it will be hashed to a specific unit according to its index (e.g., fragment $i$ will be hashed to memory unit $i\%N$).

Given that the switch memory size is usually smaller than the gradient size, multiple gradient fragments will be hashed to the same memory unit. Therefore, **asynchronously arriving fragments may encounter hash collision, degrading the throughput of in-network aggregation**.

<p style="text-align: center;">
    <img src="2023-02-11T151628.png" alt="memory sharing example" width="60%" alignment="center">
</p>

### Little On-chip Memory of Programmable Switches Needs More Design for In-network Aggregation

The motivation of this work is simple. **Since one switch can not store the entire gradient, what about using multiple switches to store?**

Given some switches, the traditional way is each switch aggregates a set of workers' gradients. But we change the way of gradient fragments assignment.

In practice, one model can be divided into a set of sub-models (e.g., model layers), whose gradient is aggregated independently. Our key idea is to schedule sub-model gradients to multiple switches for collaborative in-network aggregation. This makes programmable switches possible to store all gradients and aggregate asynchronously arriving gradients
