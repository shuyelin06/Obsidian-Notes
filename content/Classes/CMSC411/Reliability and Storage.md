---
title: Reliability and Storage
tags:
- cmsc411
---

# Reliability and Storage
## Dependability
Any system has two notions of service:
- A **specified service** is what the behavior should be
- A **delivered service** is the actual behavior of the system

If the specified service meets the delivered service, then the system is **dependeable**. Here, we propose definitions to describe the dependability of systems. 

For any system:
- A **fault** occurs when a module in a system works incorrectly
- An **error** occurs when a fault causes an incorrect behavior in a system
- A **failure** occurs when the high-level behavior of the behavior deviates from the system specified behavior.

> [!Info] Fault Classifications
> There are various ways we can classify faults.
> 
> One way is **by cause**:
> - **Hardware Faults**: A hardware device fails to perform as expected
> - **Design Faults**: A fault in software or hardware that occurs during system designing
> - **Operation Faults**: Operation / user mistakes
> - **Environmental Faults**: Environmental factors, such as fire, power failure, sabotage, etc.
> 
> Another way is **by duration**: 
> - **Transient Faults**: Last for a limited time and are not recurring
> - **Intermittent Faults**: Last for a limited time but are recurring
> - **Permanent Faults**: Do not get correced when time passes

When a failure occurs, an error took place, and when an error takes place, a fault took place. However, no all faults cause errors, and not all errors cause failures. 

> [!Example] Example: Fault, Error, Failure
> Say we have an `add()` function that tries to add 5+3, but returns 7. This is a fault.
>
> If we call our function, and it returns 7 for 5+3, then we have an error.
>
> If this function causes us to schedule a meeting on the 7th instead of the 8th, then we have a failure. 
> > If we never use the result of the function, then we don't have any failure!

To concretely define a system's dependability, we define **reliability** metrics that we can measure or calculate. One common measure is **mean time to failure (MTTF)**, which measures the average time of continuous service accomplishment before a failure.

Using MTTF, and the **mean time to repair (MTTR)**, we can define **availability**! This is the fraction of overall time the system is operational.
$$
\text{Availability} = \frac{MTTF}{MTTF + MTTR}
$$

## Improving Reliability
Knowing that faults can occur, we have ways to improve reliability.
- One way is **fault avoidance**, where we prevent the occurrence of faults.
- Another way is **fault tolerance**, where we prevent faults from becoming failures through redundancy.

Fault tolerance is very important, as it's nearly impossible to completely prevent faults from occurring. Fault tolerance includes techniques such as:
- **Detection**: Use 2-way redundancy, where two modules do the same work, and compare their results. If the results are different, then do a roll back. 
- **Recover**: Periodically save state, and on detection of an error, restore this state.
- **Correct**: Have $N$ modules do the same work, then vote for the correct result. 
  - This is also called **N-Module Redunancy**.
  
Another way of implementing redundancy is through **data redundancy**.
- **Error Detection Code (EDC)**: Codes we add to data to detect if an error exists.
  - **Parity Bit**: Use a bit to track if the number of 1s is odd or even. Lets us detect if an odd number of bit flips took place.
  - **Checksum Code**: Split the data into equal sized words, and XOR them together. This essentially is a generalization of a parity bit check into more bits.
  - **Berger Code**: Stores the number of 1s in the data.
- **Error Correction Code** Codes we add to data to correct and remove errors that exist (can both detect and correct errors).
  - **Hamming Code**: Based on **hamming distance**, which is how many bit flips are neded to change the current number to another one.

## Hamming Code (7,4)
One way we can make our data more reliable is by using Hamming Codes.

Let's see how to generate a hamming code. In particular, we will generate a hamming code (7,4) (7 bits total for 4 data bits). 

First, number each of our bit positions in binary.
| | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 
| :- | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| Binary | 111 | 110 | 101 | 100 | 011 | 010 | 001 |

Now, for any power-of-two position, make it a parity bit. All others are data bits.
| | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 
| :- | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| Binary | 111 | 110 | 101 | 100 | 011 | 010 | 001 |
| Parity / Data | d4 | d3 | d2 | p3 | d1 | p2 | p1 |

Now, set the parity bits based on the data elements where the $n^{th}$ bit is set to 1. For example, parity bit `p1` will track the parity of the data elements whose address has the first bit set.
> Note that instead of operating on bits, we typically give the data bits and code bits in separate chunks: `<data><code>`.

This gives the hamming code!

> [!Example] Example: Hamming Code
> Suppose we have data `0110`. Then, our hamming code is `011`, giving us final message `0110011`.

Hamming Codes add bits to our data in a way such that all $2^4 = 16$ configurations of data are possible, **and the minimum distance between any two configurations is 3+**! Thus, if we detect an invalid code word, we may be able to correct it by finding the closest valid word. 

Note that if we correct invalid words, we are assuming that **we can only have 1-bit errors, and 2-bit errors are not possible**. 
- If we correct errors, then we will falsely correct 2-bit errors! 
- If we detect 2-bit errors, we have no way of knowing what the closest word is!

So, our scheme can only be used for 1-bit correction, or 2-bit detection, but not both. 

> [!Info] SECDED
> We can resolve this by adding **another parity code** onto each valid code word! This adds 1 more distance between every word, letting us lets us detect two errors and correct one error at the same time!
> ```
> <Data><Code><ParityOfCode+Data>
> ```
> 
> This extended scheme is known as **SECDED (Extended Hamming Code)**

## Disk Fault Tolerance (RAID)
Another way we can improve reliability is by using RAID. This defines ways we can group disk hardware together to increase performance.

![[Classes/CMSC411/Resources/RAID0.png]]
![[Classes/CMSC411/Resources/RAID1.png]]

**RAID 0** distributes data across multiple disks, instead of keeping all of the data on 1 disk. 
- **Pros**: This shares the load across disks, which can now work in parallel (increasing throughput and reducing latency!).
- **Cons**: If we do not duplicate any data, our reliability is actually lower! This is because any one of our disks could fail and produce a problem.

**RAID 1** improves this with **disk mirroring**. Here, disks are paired and share identical data. 
- On any write, both copies are updated
- On a read, either copies can be read from.
- This improves both performance and reliability! We can do more reads at once (same amount of writes though), and if one disk fails, its mirror still has the data!

> [!Info] Combining RAID 0 and 1
> If we have more than 2 disks, we can combine RAID 0 and 1!
> - With **Striped Mirrors**, we can pair disks for mirroring, and then stripe (distribute) across the 4 pairs.
> - With **Mirrored Stripes**, we can distribute across 2 disks, and then mirror them. 

![[Classes/CMSC411/Resources/RAID4.png]]

**RAID 4** inter-leaves blocks between disks, and keeps an extra disk purely for parity blocks. 
- On read, we access only the data disk
- On write, we access both the data block and parity block.

RAID 4 lets us detect and recover from an error on any one disk, using the parity and other data disks. However, write performance is lower than with one disk, as all writes must use the parity disk.

![[Classes/CMSC411/Resources/RAID5.png]]

**RAID 5** extends the concept of RAID 4, by distributing the parity blocks across the disks. 
- Now, while reads and writes are the same, the parity block a write affects changes depending on the block we're writing to. 
  - This shares the parity update load across all of the blocks!
