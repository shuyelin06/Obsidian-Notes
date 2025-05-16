---
title: Multiprocessing
tags:
- cmsc411
---

# Multiprocessing and Multithreading
## Multi-Processing
Uniprocessor speed is improving, but is only improving slowly. If we want to continue doubling performance, 1 processor won't be enough-- we'll need multiple.

We can categorize parallel architectures based on (1) how many instruction streams we have, and (2) how many data streams we have.
- **SISD**: Single I Stream, Single D Stream (Uniprocessor)
- **SIMD**: Single I Stream, Multiple D Streams
- **MISD**: Multiple I Stream, Single D Stream
- **MIMD**: Multiple I, Multiple D Streams

## MIMD
MIMD processors are the typical off-the-shelf multiprocessor. There are multiple varieties of MIMD processors, varying based on how memory is organized.

In **Centralized Shared Memory**, each processor has its own cache, and all caches are connected to a shared memory. These are also called **Symmetric Multiprocessors (SMP)** or **Uniform Memory Access (UMA)**.
> Centralized shared memory is not very scalable, and is only typically used for smaller machines.

In **Distributed Memory**, each processor has its own cache and memory. On a miss, a cache either goes to the core's memory, or access another core's memory through an interconnection network. Distributed shared memory scales well, and can be implemented in different ways.
- **Message Passing**: A processor can only directly address local memory, and must send messages to communicate with other processors
- **Distributed Shared-Memory (DSM / NUMA)**: All processors can address all memory locations.

> Message passing tends to be a lot more manual and difficult for the programmer (you need to explicitly code the message passing), but can allow for better performance gains.

## Multi-Threading
Using multi-threading, we can simulate a multi-processor using a single processor. We could benefit from this, as it lets us share core execution time between different threads.

However, to do this to get maximal benefit requires that we have hardware support in the core.
- **Chip Multi-Processor (CMP)**: We add extra hardware to execute more than one thread at the same time on a core.
- **Simultaneous Multi-Threading (SMT, Hyperthreading)**: In any given cycle, we can execute a mix of instructions belonging to different threads

> We need hardware support, because even if we switch threads, they can still have stalls! 

To implement SMT for $N$-threads, we'll need:
- The ability to fetch from $N$ threads, and $N$ sets of registers, one set for each thread (this includes program counters)
- $N$ RATs for renaming
- $N$ virtual memory spaces

This lets us improve overall throughput, but this can also degrade cache performance! This is because the cache is still shared by all threads, so the cache capacity and associativity are also shared!
> This is known as **cache thrashing**. A cache may be enough for one thread, but not multiple! This can cause higher miss rates, which can actually lead to worse performance than a normal uniprocessor.
