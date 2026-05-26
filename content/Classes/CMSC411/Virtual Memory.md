---
title: Virtual Memory
tags:
- cmsc411
---

# Virtual Memory
## Context
When we work with memory as programmers, we are not directly addressing physical memory on our machine. This is for a variety of reasons.
- Real machines only have a few GB of memory, and this can vary between machines. 
- Processes have their own "memory" which could conflict on physical memory.

Instead, we write code that references **virtual memory**. This is a concept of memory that abstracts the machine's physical memory from us (the programmer) so that we don't need to worry about physical limitations. 

This does make things more convenient, but the CPU only knows about physical memory! So, how are these virtual addresses mapped to physical addresses?

## Pages and the Page Table
Introducing **pages**! These are fixed-size, aligned regions of memory, which are typically 4KB each (but not always). A page on physical memory corresponds to a page in virtual memory.
> On physical memory, we call these "pages" **frames**.

We can map virtual memory pages to physical memory pages. To track these mappings, each process stores one **page table**, which stores the physical addresses corresponding to each virtual addresses.
> Page tables may also store meta-data, such as permissions, dirtiness, etc. (covered later).

A virtual address is split into two sections:
- The **virtual page number**, which indexes the page table to tell us what page of physical memory we're using
- The **page offset**, which specifies the number of bytes into the memory page

> [!Example]+ Example: Virtual Address Composition
> On a 32-bit machine, a simple virtual address would be split as follows (assuming a 4KB page):
> ```
> Virtual Page Number (20 Bits) | Page Offset (12 Bits)
> ```
> 1. We need 12 bits ($2^12 = 4096$) to address an entire 4KB page
> 2. The remaining 20 bits ($32 - 12 = 20$) are used to differentiate the page we're working on.

And on a memory instruction, the CPU would do the following:
1. Compute the virtual address 
2. Compute the virtual page number(s)
3. Compute the physical address for the page table entry
   1. Read page table entry(s)
   2. Compute physical address by appending offset
4. Perform the actual load from memory

> [!Example] Example: Translating Virtual Addresses
> For example, suppose we have virtual address 0xFC51908B, on the 32-bit machine from before.
> - It's virtual page number is 0xFC519, the first 20 bits
> - It's page offset is 0x08B, the last 12 bits
> 
> To translate this address into a physical address, we first index the page table with the virtual page number - say this returns 0x00152. Then, we append the page offset.
> 
> So, our physical address is 0x0015208B.

## Page Table Types
Let's look at some of the ways we can store a page table.

### Simple (Flat) Page Table
In a **Simple (Flat) Page Table**, we store one entry per virtual page, where each entry contains a physical page number, and indicates whether or not the page is on disk or invalid.

The problem with this is, this is a lot of entries! Because this layout stores entries for pages the program never uses, the table takes up way too many resources!

> [!Example]+ Example: Simple Page Table Size
> Let's calculate the size of this table. To do this, first assume:
> - The process has a 32-bit address space
> - Pages are 4KB
> - Each page table entry must be 4 bytes
> 
> Then, the overall size is
> $$
> \text{Size} = \frac{\text{Size of Virtual Memory}}{\text{Page Size}} * \text{Entry Size}
> $$
> 
> So, our page table size would be $\frac{4GB}{4KB} * 4B = 4MB$!
> > This is not the best. 4MB can be a lot for programs that don't take up a lot of memory, and if the address space was larger, this page table size would explode!

### Multi-Level Page Tables
The previous table wasted a lot of space, as a lot of entries could be unused.

To make this better, consider the **Multi-Level Page table**, which establishes a hierarchy of page tables. Each table tells us where we should look in the next level. 

For example, for a 2-level table, our virtual address would be split as
```
Outer Page # | Inner Page # | Page Offset
```
Where:
- **Outer Page \#** indexes the outer page table. We index the outer page table to the inner page table to look at.
- **Inner Page \#** indexes this specific inner page table. We index the inner page table to get the physical page address to look at.
- **Page Offset** is appended to the physical page address to give us the final physical address.

This page table setup is (on average) space efficient, as it does not require that all entries be allocated! If the outer page table entry is empty, **we do not need to allocate space for their respective inner page table entry**! 
> Inner page tables will only be allocated if needed.

> [!Example] Example: Multi-Level Page Table Size
> Suppose we have the following assumptions:
> - 32-bit address space for a process, and 4 KB page.
> - 1024-entry outer page table, 1024-entry inner page table.
> - Page table entry: 8 bytes
>
> Say we know our program only uses virtual memory at 0x00000000 to 0x00010000, and 0xFFFF0000 to 0xFFFFFFFF.
> - Outer Page Table Size: $2^{10} * 8B = 8KB$
> - Inner Page Table Size: $2^{10} * 8B = 8KB$
> 
> Based on our virtual memory, we have ranges
> ```
> 0x0000 0000
> 0000 0000 00 | 00 0000 0000 | 0000 0000 0000
> 0x00010000
> 0000 0000 00 | 00 0001 0000 | 0000 0000 0000
>
> 0xFFFF 0000
> 1111 1111 11 | 11 1111 0000 | 0000 0000 0000
> 0xFFFF FFFF
> 1111 1111 11 | 11 1111 1111 | 1111 1111 1111
> ```
> As the outer page table number can only take on 2 values (all 0s or all 1s), we need 2 inner page tables. So, we have total size
> $$
> 8KB + 2 * 8 KB = 24 KB
> $$
> > If we repeat this calculation for the simple page table, we'd have space 8MB!

## The Translation Look-Aside Buffer (TLB)
From virtual addressing, note that everytime we access memory, the CPU must access the page tables to translate the address! This invokes overhead.

To make things more efficient, first observe that in the general case, when a virtual page is used, it is often used more in the near future. So, we could **cache the virtual to physical translations** to avoid repeated computations!

This can be achieved with the **Translation Look-Aside Buffer (TLB)**. 
- After a virtual address is translated, the TLB will store the corresponding physical address.
- If this address is accessed again in the near future, the already-computed physical address can be reused!
- If the TLB does not contain the address (a miss), there are a few ways we can resolve the miss:
  1. **Hardware TLB Miss Handling**: The hardware knows how to read the page tables, so the TLB stalls until the hardware finds the translation.
  2. **Software TLB Miss Handling**: The OS knows how to read the page tables, so an exception is raised so the OS can compute the translation.

The TLB used to be **fully-associative**, meaning that any mapping can be kept in any TLB entry, so all entries had to be checked on a memory access. To achieve low latency, this means the TLB can only store a few entries! 
> Newer processors include larger, but **set-associative** TLBs, where the lowest bits of the virtual page number determine where a mapping can go. 
>
> Other processors include **multi-level** TLBs, where you check level 1 (smallest but fastest), then level 2 (larger for better hit-rate), then memory.

The TLB may also store process IDs, so that it can be shared between multiple processes (process virtual memory addresses are the same, so some differentiation is needed).
