---
title: CMSC411
tags:
- cmsc411
---

This is logistics + introduction to computer architecture! 

In general, the goal of computer architecture is to design computers that are suited for their intended use. To do this, we need to consider factors such as speed, power usage, and cost.

# Performance Metrics
**Performance** is a general term that we use to describe processors. But what actually is performance? 

There are two common measures for performance:
- **Latency (Response Time, Execution Time)**: How long it takes to perform a task
- **Throughput**: How often can a task be performed

> Note that throughput is not always equal to 1 / latency! If we have multiple processors, the latency of the processors stays the same, but their total throughput would increase! 
>
> (This in fact, motivates the idea behind GPUs-- by combining tons of processors with high latency, they can still have a really high throughput!)

---

- Introduction to computer architecture
- Performance metrics
- Pipelining
- Branches and branch prediction
- Instruction-level parallelism (ILP)
- Memory hierarchy
- Multiprocessing
- Thread-level parallelism
- Cache coherence
- Memory consistency
- Many-core processors
