---
title: Parallelization With GPUs
tags:
- graphics
- wip
---

One of the biggest advantages of the graphics pipeline is it's ability to be massively parallelized for efficiency. Over recent years, dedicated graphics hardware has significantly advanced, incorporating more and more parts of the rendering pipeline for significant speed-ups.

In the modern day, a lot of graphics processing isperformed by the **graphics processing unit (GPU)**, enabling us to transform large quantities of data at once using programs called **shaders**. But what makes a GPU so fast?

Broadly, this is accomplished through two means:
1. A highly parallelized architecture
2. Dedicated hardware for highly parallelizable tasks (e.g. depth testing, texture accessing).

This article describes each of these in more detail.


# Parallelized Architectures
## The Problem of Latency
**Latency** is a big problem for any processor. Accessing data takes time, and during this time, the processor cannot continue execution until the retrieval operation finishes. In order words, it's forced to **stall**, and this reduces performance.
> This happens because if data is not at the processor, it needs to physically travel to it - and this takes time. 

Different processor architectures have varying strategies to avoid stalling. For example, CPUs use local caches, which store data closer to the processor to minimize the effect of latency. 

GPUs also have a strategy, and that's context switches; more on this in the next section.

## Motivation Behind GPUs
GPUs are built to maximize **throughput**, the rate in which data can be processed. GPUs achieve this by having thousands of processors (called **shader cores**), which can process sets of similar data together in parallel. 

This parallel structure is enabled by the assumption that **invocations executing on each processor are as independent as possible**, so that they don't need to wait on each other to finish.

However, with less area for caches and additional logic, latency for each shader core is a lot higher than a CPU processor! So does can a GPU minimize stalling? Consider the following.

> [!Example]+ Scenario: Minimizing Stalling on One Processor
> Say we have 2,000 pixels, and we need to process them by running a pixel shader program on each. Additionally, suppose we have a single shader processor to do this with.
>
> This processor executes our program on the first pixel. During this exeuction, if it hits an operation that needs to access data (e.g. a texture access), our processor will be forced to stall until the this data is retrieved, which wastes computational power!
>
> Instead, let's give each pixel some storage space for its local registers. Then, we could have our processor switch to other pixels and execute the program on them while we wait on retrieving the data! This way, our processor never stops working, and by the time it finishes, our initial program will have the data retrieved, letting us continue it's execution.

Like in the above example, switching lets us keep our processor busy, avoiding stalls and minimizing our overall execution time! This is the idea behind GPUs.

## GPU Architecture & Warp Swapping
Each shader that a GPU needs to run is called a **thread**, containing memory for the shader's inputs, as well as any register space. Threads running the same shader program are then grouped into **warps (NVIDIA)**, otherwise called **wavefronts (AMD)**, which can be scheduled for execution on the GPU cores.

Execution on these cores is done using **single instruction, multiple data (SIMD)** processing. In this form of processing, we can execute one command, which will apply to multiple threads at once! 

So, to execute programs, a GPU will do the following.
1. The GPU will load a warp, containing threads that may have different inputs, but are running the same program. Each thread will have a processor assigned to it.
2. The GPU will then execute the shader program on the threads, where all of the processors will execute the same instruction at once, instruction by instruction.
3. By this arrangement, when an instruction causes a delay, all threads will stall at the same time. Thus, if a delay will happen, the GPU can swap out the warp for a different warp, and continue executing on this new warp without stalling.
   
   > Note that swapping is fast, as threads are independent of each other!

This process of **warp swapping** is continued until all warps are completed, and is the major mechanism for hiding latency by all GPUs.

An example of warp swapping is given below. 

> [!Example]- Example: Warp Swapping on a GPU 
> Say we have 3 warps executing a program doing the following:
> 1. `mad`: Multiply and add numbers
> 2. `mul`: Multiply numbers
> 3. `txr`: Access a texture (**causes a stall**)
> 4. `cmp`: Compare numbers
> 5. `add`: Add numbers
> 
> Then, our GPU could perform warp swaps as follows:
> 1. Load **warp 1**. 
>    1. Execute `mad` instruction on all threads.
>    2. Execute `mul` instruction on all threads.
>    3. Execute `txr` instruction on all threads. Because of the stall, switch to **warp 2**.
> 2. Load **warp 2**.
>    1. Execute `mad` instruction on all threads.
>    2. Execute `mul` instruction on all threads.
>    3. Execute `txr` instruction on all threads. Because of the stall, switch to **warp 3**.
> 3. Load **warp 3**.
>    1. Execute `mad` instruction on all threads.
>    2. Execute `mul` instruction on all threads.
>    3. Execute `txr` instruction on all threads. Because of the stall, switch back to **warp 1**.
> 4. Load **warp 1**. Continue execution.
>    1. Execute `cmp` instruction on all threads.
>    2. Execute `add` instruction on all threads. Because this warp is finished, switch to **warp 2**.
> 5. Load **warp 2**. Continue execution.
>    1. Execute `cmp` instruction on all threads.
>    2. Execute `add` instruction on all threads. Because this warp is finished, switch to **warp 3**.
> 5. Load **warp 3**. Continue execution.
>    1. Execute `cmp` instruction on all threads.
>    2. Execute `add` instruction on all threads. Because all warps are finish, we are done!
>
> By performing warp switching, we always keep our GPU busy! Note that during a switch, we could switch to any other warp that is not stalled, but if all warps are stalled, we're forced to wait until one becomes available.

While GPU warp swapping helps hide latency, it also has limitations! In particular, there are many factors we should be aware of when it comes to keeping our shader programs efficient.

> [!Warning] Occupancy
> GPU memory is limited. So, the more registers needed by a shader program, the fewer threads we can create for it. This limits the number of warps we can create!
> 
> If we don't have enough warps, we won't be able to hide a stall using a warp swap, which is bad. We can measure this using **occupancy**, representing the number of warps available for processing (lower occupancy means lower performance).

> [!Warning] Thread Divergence
> By the parallel architecture of GPUs, if threads branch differently in the same warp, then the warp will need to execute both branches on **all threads** to account for the differing branches, as the SIMD architecture means we execute thesame commands on all threads and throw away some of the results. 
>
> This is called **thread divergence**, and wastes computational power!
