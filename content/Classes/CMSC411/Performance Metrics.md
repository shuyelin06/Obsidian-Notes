---
title: Performance Metrics
tags:
- cmsc411
---

# Performance Metrics
## Metrics
**Performance** is a general term that we use to describe processors. But what actually is performance? 

There are two common measures for performance:
- **Latency (Response Time, Execution Time)**: How long it takes to perform a task
- **Throughput**: How often can a task be performed

Throughput is not always equal to 1 / latency! Below are some examples in which this equality fails to hold.

> [!Example]- Example: Throughput and Latency
> Say we have a throughput of 4 units / hour. This could be achieved with:
> 1. 1 processor with a latency of 15 min
> 2. 2 processors with a latency of 30 min
> 3. 4 processors with a latency of 1 hour
>
> Notice that if we have multiple processors, throughput is no longer equal to 1 / latency! In fact, it can be reasonable to accept more (slower) processors to achieve the same throughput, as slower processors are typically more expensive. 
> > This in fact, motivates the idea behind GPUs-- by combining tons of processors with high latency, they can still have a really high throughput!

## Comparing Performance
### Benchmarks
Say we have two machines that we know the throughput and latency of. Can you simply divide these values to find what machine is "faster"?

No! Machines run differently on different applications. So to compare performance, we need some way to benchmark our machines to measure performance.
> Ex (Standard Benchmarks): SPEC CPU2000, SPEC 2006, ...

Some examples of benchmarks include:
- **Real Applications**: Applications that are representative of actual use-cases, but are difficult to set up.
- **Kernels**: Representative parts of real applications, which are easier to set up and run. Often not representative of the entire application.
- **Toy Programs / Synthetic Benchmarks**: Tests / stress specific functions or features of your design. Often not very representative of real use-cases.

With benchmarks, it's useful to have some sort of representative number that summarizes performance. 
- **Arithmetic Mean**: Computes the average execution time, but gives more weight to longer-running programs.
  > Because of this, the arithmetic mean reports different statistics depending on the order in which we compute the speed-up. 
- **Weighted Arithmetic Mean**: Lets us adjust and emphasize more important programs; however, different weights can make different machines look better (making things very relative).
- **Geometric Mean**: Removes the bias that arithmetic mean has; generally better and reliable.

### Iron law
So we have a way to measure performance. But how do we know what's contributing to better or worse performance? 

> [!Info] Iron Law
> The **Iron Law** states that
> $$
> \begin{align*}
> \text{CPU Time} = \text{CPU Clock Cycles} \times \text{Clock Cycle Time} \\
> \text{CPU Time} = \text{Instruction Count} \times \text{Cycles Per Instruction} \times \text{Clock Cycle Time} \\
> \text{CPU Time} = \frac{\text{Seconds}}{\text{Program}} = \frac{\text{Instructions}}{\text{Program}} \times \frac{\text{Clock Cycles}}{\text{Instruction}} \times \frac{\text{Seconds}}{\text{Clock Cycle}}
> \end{align*}
> ```

The Iron Law breaks CPU time into its 3 influencing components, which can be influenced to increase performance.
- Instructions / Program: Influenced by the algorithm, compiler, or instruction set.
- Clock Cycles / Instruction: Influenced by the instruction set or processor design.
- Seconds / Clock Cycle: Influenced by the processor design, circuit design, or technology.

Out of these components, the **instruction set** and **processor design** are under the scope of Computer Architecture!

> [!Example]- Example: Iron Law Example
> Say we have a program that takes 33 billion instructions to run, and the CPU processes instructions at 2 cycles per instruction (CPI), with a clockspeed of 3 GHz.
>
> By the Iron Law, our CPU Time is
> $$
> \text{CPU Time} = (33 * 10^9) * 2 * (3 * 10^{-9}) = 22 \; \text{Seconds}
> $$

If instructions are unequal, we can modify `CPU Clock Cycles` in our equation as follows.
$$
\begin{align*}
\text{CPU Clock Cycles} = \left( \sum_{i=1}^n IC_i \times CPI_i \right) \\
\text{CPU Time} = \left( \sum_{i=1}^n IC_i \times CPI_i \right) \times \text{Clock Cycle Time}
\end{align*}
$$
> `IC` stands for instruction count (of some type of instruction), and `CPI` stands for clock cycles per instruction.

In a general program:

| Instruction Type | % of Instructions | CPI |
| :-: | :-: | :-: |
| Integer | 50% | 1.0 |
| Branch | 20% | 4.0 |
| Load | 20% | 2.0 | 
| Store | 10% | 3.0 |

So, in a general program with 50 Billion Instructions, Clock Speed of 2 GHz, we would have CPU Time

$$
\text{CPU Time} = (25B * 1 + 10B * 4 + 10 * 2 + 5 * 3) * (2 * 10^{-9}) = 50 \; \text{Seconds}
$$

> [!Tip] CPU Times
> Sometimes, we don't have to calculate the CPU Time! When making comparisons in computer architecture, if the program and clock speed is the same for two CPU, then we could just directly compare CPI (or IPC)!
>
> When doing this, note that Average IPC is not the same as 1 / Average CPI. You need to convert all IPC's to CPI's and then compute the average to find the Average IPC.

### Amdahl's Law
So far, we've developed a way to measure performance, and break it down into components that we can use Computer Architecture to improve.

Now how do we know what to improve? If we improve a component, how does this influence the overall speed-up?

> [!Info] Amdahl's Law
> Amdahl's Law states that
> $$
> \text{Overall Speedup} = \frac{1}{\left( (1 - \text{Fraction}_\text{Enhanced}) + \frac{\text{Fraction}_\text{Enhanced}}{\text{Speedup}_\text{Enhanced}} \right)}
> $$
> - The first component of the sum is the part that we didn't improve
> - The second component of the sumis the speed up we achieved on that enhancement
> 
> Note that $\text{Fraction}_\text{Enhanced}$ is the **percent of time** that is affected by the enhancement, not the percent of instructions!

From this law, we conclude that we want to **accelerate the common case**. Observe the following.

Say we have a 20x speedup on only 10% of the time. Then, we have an overall speedup of
$$
\text{Speedup}_1 = \frac{1}{(1 - 0.1) + \frac{0.1}{20}} = 1.105
$$

Now say we have a 1.2x speedup on 90% of the time. Then, we have an overall speedup of
$$
\text{Speedup}_2 = \frac{1}{(1 - 0.9) + \frac{0.9}{1.2}} = 1.176
$$

> [!Tip] Main Idea
> **Accelerate the common case**! Small speedups on most of the time is better than a speedup on only a portion of the time! Furthermore,
> - While we still achieve a speed-up in either case, sometimes significant speedups are a lot more expensive than minor speedups across the board.
> - If we keep improving only one part of a program, our overall speedup will increase slower and slower! There are diminishing returns for focusing only on one part of a program.
