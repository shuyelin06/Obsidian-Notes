---
title: Pipelining
tags:
- cmsc411
---

# Pipelining
Pipelining is a powerful concept that is used in every single computer today. We describe what pipelining is and consequences of it here.

## Instruction Stages
When running an instruction, a simple processor generally goes through the following stages:
- **Instruction Fetch (IF)**: The instruction is retrieved from instruction memory, depending on what the address the PC is pointing to.
- **Instruction Decode (ID)**: The data of the instruction is interpreted such as the opcode (operation) of the instruction and the operands it uses. 
- **Execute (EX)**: The instruction, if a computation, is performed. Register values are pulled and the computation executes (subtraction, multiplication, addition, etc.).
- **Memory (MEM)**: The instruction accesses memory (if needed). This can include instructions like LW, SW, or other instructions that access memory.
- **Write-Back (WB)**: The result of the instruction is written back to the reegisters. 

![[Classes/CMSC411/Resources/Pipeline-None.png]]

For the sake of example, say each of our stages take the following amount of time.

| Stage | Time | 
| :-: | :-: |
| IF | 1.0ns |
| ID | 0.6ns | 
| EX | 0.9ns |
| MEM | 1.2ns |
| WB | 0.4ns |

We execute our instruction in sequential stages. In this case, we would take 4.1ns to finish our instruction. 

Problem with this is, **a clock-cycle must be long enough to complete even the most time-consuming instruction**! Thus, if we wanted to run many instructions, then we would be forced to take 4.1ns to run each instruction (as a lower bound). 
## Pipeline Motivation
How can we make this better?

Well, let's try breaking up our instruction among multiple clock cycles. If we place memory between each stage, then each stage can write its output to memory for the next stage to use! 

![[Classes/CMSC411/Resources/Pipeline-Memory.png]]

This breaks our instruction up into independent stages. For example:
- Cycle 1, IF runs and writes to ID's input memory (called IF/ID memory)
- Cycle 2, ID runs and writes to EX's input memory (called ID/EX memory)
- Cycle 3, EX runs and writes to MEM's input memory (called EX/MEM memory)
- Cycle 4, MEM runs and writes to WB's input memory (caled MEM/WB memory)
 
Now, our instruction takes 5 cycles! **This actually increases the latency of a single instruction**, and in our case, as the longest stage is MEM (1.2ns), our instruction would now take 6.0ns ($5 * 1.2$ ns). Why would we want to do this?

Well, this is actually worth it because **we don't care about latency, we care about throughput!** Now, because each stage no longer needs to wait on the entire instruction to finish before executing the next, it can start on the next instruction immediately!
- Cycle 1:
  - I1: IF fetches I1 and writes to ID's input memory.
- Cycle 2:
  - I2: As I1's IF output is already written to memory, IF can already start fetching I2!
  - I1: ID decodes I1 writes to EX's input memory.
- Cycle 3:
  - I3: IF fetches I3!
  - I2: ID decodes I2!
  - I1: EX executes I1 and writes to MEM.

```bash
IF -> ID -> EX -> MEM -> WB
I1

IF -> ID -> EX -> MEM -> WB
I2    I1

IF -> ID -> EX -> MEM -> WB
I3    I2    I1

...
```

So, even though our single instruction takes 6.0ns, **we can now execute instructions every 1.2ns, because our clock-cycle is defined by the longest stage (1.2ns)!**
> Even though latency for a single instruction is higher, because we're "pre-loading" the overall throughput is higher! 

This is the motivation and idea set-up behind pipelining! By keeping each of our instruction stages independent, we can massively increase throughput!

Some consequences of this:
- Pipelining takes more memory, and makes instructions take multiple clock cycles.
- Pipelining is bounded by the **longest stage**, as this sets a bound on the processor's clock time.
  - A consequence of this is the more balanced our stages are in time-execution, the better!
- We can add more stages, but the more stages we have, the higher the clock frequency needs to be for this to be useful! Whether we are able to do this or not depends on the technology we have. 

## Hazards (Overview)
**Hazards** are problems that reduce the performance of the pipeline. There are 3 kinds of hazards:
- **Data Hazards**: Dependencies between instructions preventing their overlapped execution
- **Structural Hazards**: There are not enough hardware resources for all combinations of instructions
- **Control Hazards**: A branch instruction may change the program counter (PC).

Many of the following sections are dedicated to reducing a particular type of hazard, or working around it. Below, we'll talk about some ways we can reduce **data hazards**.

## Data Hazards (+ Data Forwarding)
Here, we'll talk about data hazards. Data hazards occur when there are **data dependencies**-- instructions whose execution depends on the previous one (meaning we cannot rearrange their order). 

This is a property of the **program alone**. 

Some data dependencies include:
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

Data dependencies are **hazards** if they result in incorrect execution-- this can happen with RAW dependencies if we pipeline.
> There is no hazard with WAR and WAW dependencies, though they are technically dependencies.

---

Consider the following example. Say we have the following RAW dependency: 
```python
xor t0, t1, t2
add t4, t0, t3
mul t5, t1, t3
```

Note that `add` as a RAW dependency on `xor`, and because the register data is only updated after write-back, `add` has to wait until `xor` finishes WB to execute! Otherwise, our program execution would be undefined-- this causes a major stall.

| | IF | ID | EX | MEM | WB |
| :-: | :-: | :-: | :-: | :-: | :-: |
| 1 | xor | 
| 2 | add | xor | 
| 3 | mul | add | xor | 
| 4 | S-mul | S-add | `nop` | xor | 
| 5 | S-mul | S-add | `nop` | `nop` | xor | 
| 6 | S-mul | S-add | `nop` | `nop` | `nop` | 
| 7 | | mul | add | `nop` | `nop` |
| 8 | | | mul | add | `nop` |
| 9 | | | | mul | add | 
| 10 | | | | | mul |

> Each entry tells us what instruction the stage is on. `S-` indicates the instruction is stalled (not doing anything). `nop` indicates no operation.

How could we minimize the effects of this?

### Minimizing Stalls: Optimizing Execution
Optimize the order of command execution (if possible). RAW dependencies aren't a hazard if the instructions are far enough apart, as they won't in the pipeline at the same time. 

Optimize how the processor handles the commands. For example, most register files **write on the rising edge** of a clock cycle, and **read on the falling edge** of a clock cycle. This means that the dependent instruction can read the same cycle the value is written (so, cycle 6 doesn't need to stall).

### Minimizing Stalls: Data Forwarding
Another option is **data forwarding**. Our pipeline is forced to stall because `add` must wait on `xor`'s WB to finish, but the result of `xor` is actually already ready at EX! 

So, instead of waiting on WB, we could instead directly wire the output of EX to its input! This way, the output of `xor` can immediately be used as an input into `add`!

![[Classes/CMSC411/Resources/Pipeline-Forwarding.png]]

> Note that this wire has to be connected in the MEM stage, as if we connect EX's output directly to its input in the EX stage we could have timing issues.
>
> In general, **there needs to be some sort of pipeline memory between the source and destination of the forwarding line**.

Note that this simple forwarding doesn't always work.
- If the dependent instructions are not next to each other, forwarding fails as the output of EX is no longer present.
- If the first instruction is a load, the data comes directly from memory, and the value will have to go to the WB stage to be used as input (it won't reach the data forwarding path).

It is possible to address the latter issue, by adding more wires! We can wire the output of MEM to our EX input!

However, this doesn't come without cost. Adding more wires not only is more complex, but also means we have to know how to choose between our different wires. This requires extra logic (which can stall things down).

Forwarding does not remove all possible pipeline stalls. Some stalls it cannot remove include:
- Long memory stalls
- Long latency instruction stalls
- Control dependency or branch stalls

