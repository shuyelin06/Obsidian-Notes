---
title: Operating Systems
---

These are personal notes for operating systems, referenced from the free online textbook [Operating Systems: Three Easy Pieces](https://pages.cs.wisc.edu/~remzi/OSTEP/).

# What is the Operating System?
Programs, at their very core, are very simple- they exist to execute instructions. Many many times per second, the processor:
1. **Fetches** an instruction from memory
2. **Decodes** the instruction to figure out which one it is
3. **Executes** the instruction to do the thing it is supposed to do

And then repeats this until the program completes! 

However, while programs run, there are a lot of other things going on in the background that make the system **easy to use** by the program. This body of software, which makes sure the system is easy (and efficient) to operate, is known as the **Operating System (OS)**.

The OS primarily achieves ease of use through a technique known as **virtualization**, where a physical resource is transformed into an easier to use "virtual form". Thus, sometimes, we call the OS a **virtual machine**.

This "virtual form" can be used through interfaces (**APIs**) that the use can call.
> A large part of the notes will describe how these interfaces are implemented!

> [!Example] Example: Commonly Known OS APIs
> A typical operating system provides numerous APIs that we can use!
> 
> These include the **system calls** and **standard libraries** that applications have at their disposal!

As virtualization allows many programs to run and concurrently access shared resoruces, such as the CPU, disk, and memory, the OS is sometimes also known as a **resource manager**.

# Notes
Notes for operating systems are given below.
