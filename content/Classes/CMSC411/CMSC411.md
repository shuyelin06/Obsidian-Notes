---
title: CMSC411
tags:
- cmsc411
---

This is logistics + introduction to computer architecture! 

In general, the goal of computer architecture is to design computers that are suited for their intended use. To do this, we need to consider factors such as speed, power usage, and cost.

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


# Pipelining
## Concept
Pipelining is a powerful concept that is used in every single computer today. We describe what pipelining is and consequences of it here.

When running an instruction, a simple processor generally goes through the following stages:
- **Instruction Fetch (IF)**: Read an instructinon
- **Instruction Decode (ID)**: See what the instruction is 
- **Execute (EX)**: Perform the computation
- **Memory (MEM)**: Access memory (if needed)
- **Write-Back (WB)**: Write the results back in registers

![["References/Pipeline-None.png"]]

For the sake of example, say our stages take the following amount of time.

| Stage | Time | 
| :-: | :-: |
| IF | 1.0ns |
| ID | 0.6ns | 
| EX | 0.9ns |
| MEM | 1.2ns |
| WB | 0.4ns |

Without pipelining, our execution would be sequential, one stage after the next. Most instructions can be made to run in 1 clock-cycle, **but a clock-cycle must be long enough to complete even the most time-consuming instruction**! So, in our case, we would take 4.1ns to run our instruction. 

If we wanted to run many instructions, then we would be able to run an instructionn every 4.1ns. 
> Even if instructions could be faster, our 4.1ns instruction sets a lower bound on the clock speed time. 

---

To make this a bit better, let's break up an instruction among multiple clock cycles. If we place memory between each stage, then they can write their output to memory for the next stage to use! This separates the instruction up into independent stages. For example:
- Cycle 1, IF runs and writes to ID's input memory
- Cycle 2, ID runs and writes to EX's input memory
- Cycle 3, EX runs and writes to MEM's input memory
- Cycle 4, MEM runs and writes to WB's input memory

![["References/Pipeline-Memory.png"]]
 
Now, our instruction takes 5 cycles! This actually increases the latency, and in our case, as the longest stage is MEM (1.2ns), our instruction would now take 6.0ns. Why would we want to do this?

This is worth it, because **we don't care about latency, we care about throughput!** Now, because each stage no longer needs to wait on the entire instruction to finish before executing the next, it can start on the next instruction immediately!
- Cycle 1, IF runs (1) and writes to ID's input memory.
- Cycle 2, ID runs (1) and writes to EX's input memory; IF starts the next instruction (2).
- Cycle 3, EX runs (1) and writes to MEM; ID runs instruction (2); IF starts the next instruction (3).

```
I1
IF -> ID -> EX -> MEM -> WB

I2    I1
IF -> ID -> EX -> MEM -> WB

I3    I2    I1
IF -> ID -> EX -> MEM -> WB

...
```

So, even though our single instruction takes 6.0ns, because our clock-cycle is defined by the longest stage (1.2ns), using pipelining we can now execute instructions every 1.2ns! Compare that with our 4.1ns time before. 
> Even though latency for a single instruction is higher, because we're "pre-loading" the overall throughput is higher! 

Some consequences of this:
- Pipelining takes more memory, and makes instructions take multiple clock cycles.
- Pipelining is bounded by the **longest stage**, as this sets a bound on the processor's clock time.
  - A consequence of this is the more balanced our stages are in time-execution, the better!
- We can add more stages, but the more stages we have, the higher the clock frequency needs to be for this to be useful! Whether we are able to do this or not depends on the technology we have. 

## Pipelining Issues
Pipelining does not automatically ensure we get an instruction per cycle of 1 if our pipeline is balanced. Some factors that get in the way of throughput include...

---

**Data Dependencies** are instructions whose execution depends on the previous one (meaning we cannot rearrange their order). This is a property of the **program alone**. Some examples of this include:
- **Read-After-Write (RAW)**: A true dependency; instructions that need to read values written by previous instructions
  ```python
  # Here, the result of t0 is being used in the next instruction.
  # There is a dependency here.
  xor t0, t1, t2
  add t4, t1, t0
  ```
- **Write-After-Read (WAR)**: An anti-dependency; an instruction writes to a register that needs to be read from in a previous instruction. 
  ```python
  # Because xor uses t1, there is a dependency as add may change the
  # contents of t1.
  xor t0, t1, t2
  add t1, t2, t3
  ```
- **Write-After-Write (WAW)**: An output-dependency; two instructions write to the same register.
  ```python
  # Both instructions write to the same register, so order of execution
  # matters.
  xor t0, t1, t2
  add t0, t2, t4
  ```

Data dependencies can create a hazard if they result in incorrect execution-- this can happen with RAW dependencies and pipelining.
> There is no hazard with WAR and WAW dependencies, though they are technically dependencies.

> [!Example]+ Example: Hazard of Raw Dependency
> Consider the following RAW dependency: 
> ```python
> xor t0, t1, t2
> add t4, t0, t3
> mul t5, t1, t3
> ```
> 
> In our pipeline, we have to execute as follows. Note the `nop` instruction (indicating no instruction). Reading occurs in ID:
> 
> | | IF | ID | EX | MEM | WB |
> | :-: | :-: | :-: | :-: | :-: | :-: |
> | 1 | xor | 
> | 2 | add | xor | 
> | 3 | mul | add | xor | 
> | 4 | >mul< | >add< | `nop` | xor | 
> | 5 | >mul< | >add< | `nop` | `nop` | xor | 
> | 6 | >mul< | >add< | `nop` | `nop` | `nop` | 
> | 7 | | mul | add | `nop` | `nop` |
> | 8 | | | mul | add | `nop` |
> | 9 | | | | mul | add | 
> | 10 | | | | | mul |
> 
> > Each entry tells us what instruction the stage is on. `><` indicates the instruction is stalled (not doing anything).
> 
> If `add` were to execute on cycle 4, our program execution would be undefined! This is because $t0$ has not been updated with the results of `xor`, so `add` must wait until `xor ` finishes and writes its output. 
> > WB (Write-Back) is where `xor` writes its output.

> Note that the order of execution above could be optimized. For example, most register files **write on the rising edge** of a clock cycle, and **read on the falling edge** of a clock cycle. This means that the dependent instruction can read the same cycle the value is written (so, cycle 6 doesn't need to stall).

RAW dependencies aren't a hazard if the instructions are far enough apart, as they won't in the pipeline at the same time. 

From a computer architecture standpoint, how can we handle hazards? 
- **Data Forwarding**: Because we're stalled until WB, we could add a write connecting the output of EX to the input of the next instruction's EX stage. ...




- Memory access
- Control dependencies (branches)


---

- Pipelining
- Branches and branch prediction
- Instruction-level parallelism (ILP)
- Memory hierarchy
- Multiprocessing
- Thread-level parallelism
- Cache coherence
- Memory consistency
- Many-core processors
