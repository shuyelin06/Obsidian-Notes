---
title: Virtualization
---

# Processes
## Introduction
One of the most fundamental abstractions provided by the OS is the **process**, any sort of running program. Programs are simply just data that sit on disk-- it is the job of the OS to take this data and transform it into something useful. 

In modern systems, the user can simply run whatever programs they want, with seemingly no limits on the number of concurrent programs they can have at once. But how can modern systems run so many processes at a time with a limited number of physical CPUs?

The OS achieves this using a technique known as **time sharing**. By running one process, stopping it and running another, the OS creates the "illusion" of many concurrently executing virtual CPUs, even if there is only one physical CPU doing all of the work.

To achieve this, the OS will need to implement the following:
- Low level **mechanisms**, which define protocols implementing a needed piece of functionality.
- High level **policies**, which define some algorithm for making decisions within the OS.

In this case, the OS will need mechanisms for processes, and a scheduling policy to determine what programs should be ran at any given time.
> It is often the case in OS to separate the high-level policies from the low-level mechanisms. Separating them lets us change policies without changing the mechanisms.

## The Abstraction: Processes
### Process Machine State
A process' **machine state** defines what constitutes it-- the parts of the machine that are important to the program's execution. These are parts of the machine that the program can read or update.

One part of the state are the **memory**. These include the instructions the program executes and data that the program reads and writes. The memory that the program can address is called the **address space**.

Another part of the state are the **registers**, which temporarily store data relevant to the process. Programs have many registers, but of them there are some notable registers given below:
- The **program counter (PC) / instruction pointer (IP)**: Maintains the instruction that the program will execute next.
- The **stack pointer (SP)** and **frame pointer (fp)**: Manages the stack for function parameters, local variables, and return addresses.

Finally, programs often may access storage devices, and have access to input/output information, which is maintained as a list of files the process currently has open.

### Process API
To manage processes, interfaces of any modern OS have the following mechanisms available:
- **Creation**: Some interface to create new processes.
- **Destroy**: Some interface to destroy processes forcefully.
- **Wait**: Some interface for waiting on processes to stop running.
- **Miscellaneous Control**: Other controls that may be possible on processes, such as suspending them.
- **Status**: Some interface to get some sort of status information from a process.

https://pages.cs.wisc.edu/~remzi/OSTEP/

https://pages.cs.wisc.edu/~remzi/OSTEP/cpu-intro.pdf

The data that constitutes a process

On an an abstract level, the


which virtualizes the CPU.
