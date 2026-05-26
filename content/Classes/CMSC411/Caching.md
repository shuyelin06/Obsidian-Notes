---
title: Caching
tags:
- cmsc411
---

# Caching
## Context
Memory is very slow compared to our processor, meaning anytime we access memory, we can get a significant stall!

We can work around this by exploiting the principle of **data locality**:
- **Temporal Locality**: If data is needed now, it is likely to be needed again in the near future
- **Spatial Locality**: If data is needed now, nearby data is likely to be needed again in the near future

We exploit this with caches. A **cache** is a fast but small memory store which is close to the processor. When the processor accesses data:
- If the data is in the cache (a **cache hit**), the cache can be used for the data instead of memory, which is a lot faster!
- If the data is not in the cache (a **cache miss**) the data is brought into the cache to be accessed. 

> Caches optimize the **average** memory access latency for the processor, by utilizing the principle of locality.

We typically will have several levels of cache with different sizes. The smaller the cache, the closer it is to the processor (and the faster it is to access).
> For example, **L1 Cache**: Roughly 16KB - 64KB, is directly read from / written to by the processor. This is large enough to get a ~90% hit rate, and small enough to get a hit in 1-3 cycles

One cache consists of block-sized **lines**, which typically have a size that is a power of 2. Typically, 1 line is 16 to 128 bytes in size.

Given a memory address, we can access a cache by using the upper bits to select the cache block, and the lower bits as an offset into that block. For example, if our block size is 128 bytes, then the lower 7 ($2^7 = 128$) bits are used as an offset, and the rest are used to select the block.
```
Memory Address
Block # | Offset into Block
```
> Caches will save the block number as a tag in the cache. This will be used to differentiate blocks.

## Cache Design
When designing a cache, we have to make some important design decisions:
1. **Placement**: Where in the cache can a block go?
2. **Identification**: How do we find a block in a cache (how quickly can we find a hit or a miss?)
3. **Replacement**: On miss, what do we kick out of a cache to make room?
4. **Write Policy**: What do we do about data stores?

These are discussed below.

### Placement 
**Placement** refers to the decision of what memory blocks are allowed to go into what cache lines. We have the following placement policies:
> Generally, as we increase the set size, we have a lower chance of getting a miss, but finding a hit / miss takes longer!

**Direct Mapped Cache**: A block can go to only one line.

> [!Example]- Example: Direct Mapped Cache
> Say we have a direct mapped cache with 8 lines ($2^3$). 
> 
> To use this cache, we will use 3-bits of the memory address as an index into our cache, usually as so:
> ```
> Memory Address
> Tag | Index | Block Offset
> ```
> 
> This way, every memory address has only one cache line it's data can be cached in.
>
> When we access the cache:
> 1. Use the index bits to find the line of the cache the address is at.
> 2. Compare the tags for a match.
> 3. If no match, fetch the block from memory.
> 4. If match, use the offset to fetch the appropriate byte we want. 

**Set-Associative Cache**: A single block can go to one of $N$ lines. This is accomplished by grouping the cache lines into **sets**, which are composed of $N$ lines each. A memory address can then be hashed to these sets. 
> Direct-Mapped Caches are essentially 1-way set associative caches, and Fully-Associative Caches are $N$-way set associative caches (where $N$ is the number of total cache lines).

> [!Example]- Example: 2-Way Set Associative Cache
> Say we have a 2-way set-associative cache with 8 lines.
> 
> Because our cache is 2-way, two lines defines a single **set**! This means we have $8 / 2 = 4$ sets, meaning we will use 2 bits of our memory address to access these sets. 
> 
> When we check the cache for a given memory address, we'll have to check every line in the set (compare the tags) to see if the data is in the cache. 

**Fully Associative**: A single block can go to any line in the cache. To determine if a memory address is in the cache, we need to check every line for the address' tag.

> [!Example]- Example: Fully Associative Cache
> Say we have a fully-associative cache of size 1024 bytes, with 16-byte lines.
> - Since a line is 16-bytes, the block offset needs 4 bits ($2^4 = 16$).
> - We have $1024 / 16 = 64$ lines total.
> - Since we have a fully associative cache, all 64 lines are in the same set!
>
> When we access the cache: 
> 1. We will use the tag bits to check **all lines** for a match. 
> 2. If no match, fetch the block from memory.
> 3. If there is a match, use the offset bits to get the byte from the matched line. 

### Identification
**Identification** refers to how we find a block in a cache. The faster we can find a block, the faster we can determine if we have a hit or a miss!

When we reference an address, we need to perform a **cache lookup** where we check if the data is in the cache, and if so, where in the cache it is. To do this, every cache line must have:
- A **valid** bit, indicating if the line has data (1) or not (0).
- A **tag**, identifying what block is in the line.

The process of finding a block is as follows:
1. Access the set of lines that a block could be in.
2. Compare the block's tag with the lines to try to find a match.
3. If no match (miss), fetch the block from memory.
4. If match (hit), use the block offset to access the data we need from the line. 

### Replacement
Suppose we need to fetch a block from memory, but our cache is full. **Replacement** refers to how we determine what cache lines to kick out to load our new block!

There are several replacement strategies. The goal of each is to choose a line to kick out of the cache:
- **Random**: Randomly select a line to kick out
- **FIFO**: Line that has been in the cache the longest
- **LRU**: Line that is least recently used
- **NMRU**: Anything but LRU
- **LFU**: Least frequently used

---

**Least Recently Used (LRU)** is a very popular choice, meaning we kick out the line that was least recently used.

To implement LRU, we need to track an **LRU Counter** for each line in a set. **These will always have different values**, and larger values indicate that the line was most recently used.
> If we have an $N$-way set-associative cache, we'll need $\log_2 N$ bit counters! This can be costly.

When we load a line into the cache:
1. Get the old value $X$ of the LRU counter
2. Set its counter to the max value
3. For every other line in the set, **if the counter is larger than $X$ (the original value), decrement it**.

When we need to replace a line in the cache:
1. Select the line whose counter is 0.

> [!Example]- Example: LRU Cache
> Suppose we have the following cache:
> | Data | Tag | Valid Bit | LRU Counter |
> | :-: | :-: | :-: | :-: |
> | | | 0 |
> | | | 1 |
> | | | 2 |
> | | | 3 |
> 
> Say we put data $A$ into the cache, into cache line 1.
> 1. Check the original value, $X = 0$. Set the counter to the max value (3).
> 2. For any other line with value larger than $X$, decrement the counter.
> 
> | Data | Tag | Valid Bit | LRU Counter |
> | :-: | :-: | :-: | :-: |
> | A | | 3 |
> | | | 0 |
> | | | 1 |
> | | | 2 |
> 
> Now say we access the data in line 3 of the cache, $B$.
> 1. Check the original value, $X = 1$. Set the counter to the max value (3).
> 2. For any other line with value larger than 1, decrement. 
> 
> | Data | Tag | Valid Bit | LRU Counter |
> | :-: | :-: | :-: | :-: |
> | A | | 2 |
> | | | 0 |
> | B | | 3 |
> | | | 1 |
> > Notice how cache line 2 was not changed!

---

Because we may need to access and update all counters in a set per access, LRU can be really costly! Sometimes, we might need something that is simpler and faster, that's close to LRU.

One such policy is the **Not Most Recently Used (NMRU)**. 
- Every set will only have **one MRU pointer**, which points to the last accessed line in the set. 
- During replacement, we randomly select any non-NMRU line to kick out!

This may not be as good as LRU, but is a lot faster and cheaper!

### Write Policy
**Write** refers to what we do, when we write back to memory on a store instruction. During a write, we ask the following key questions below.

**Do we allocate cache lines on a write?**
- **Write-Allocate**: Allocate a cache line for the data written to memory. Commonly done because of data locality. 
- **No-Write-Allocate**: Don't allocate a cache line for the data written to memory.

**Do we update memory on writes**?
- **Write-Through**: Immediately update memory on each write
- **Write-Back**: Update values in the cache, only updating memory when the cache line is replaced. Commonly done to avoid excessive memory writes. 
  - For write-back caches, every line needs a **dirty** bit indicating if the line has more recent data than memory. This bit is flipped on any write to it.
  - When the line is replaced, it is written back to memory if the dirty bit is flipped!
  
> [!Example]- Example: Write-Back Cache
> Suppose we have the following direct-map write-back cache.
> | Data | Tag | V | Dirty | 
> | :-: | :-: | :-: | :-: |
> | | | 0 |
> | | | 0 |
> | | | 0 |
> | | | 0 |
> 
> Now say we `Write A`. We will update the data in the cache, and mark the line as dirty.
> | Data | Tag | V | Dirty | 
> | :-: | :-: | :-: | :-: |
> | A | | 1 | 1
> | | | 0 |
> | | | 0 |
> | | | 0 |
> 
> > Any reads to A will still be valid, as the most recent data is in the cache!
> 
> Now say we `Read B`. We will move this into the cache, but keep the dirty bit 0 as we aren't updating the data.
> | Data | Tag | V | Dirty | 
> | :-: | :-: | :-: | :-: |
> | A | | 1 | 1
> | B | | 1 | 0
> | | | 0 |
> | | | 0 |
> 
> Now say we `Read E`, which maps to the same location as $A$. Because of E, we need to kick out $A$. Because the dirty bit is set, we will write the line's memory back to data before kicking out A. 
> | Data | Tag | V | Dirty | 
> | :-: | :-: | :-: | :-: |
> | E | | 1 | 0
> | B | | 1 | 0
> | | | 0 |
> | | | 0 |

## Cache Performance
How do we measure how performant our cache is?

A good cache will have a low **Average Memory Access Time (AMAT)**, which measures the time it takes to access the data needed. It is given by the following formula:
$$
\text{AMAT} = \text{Hit Time} + \text{Miss Rate} * \text{Miss Penalty}
$$
> Note that we will **always** factor in hit time. This is because to get a miss, we first need to check for a hit.

To promote AMAT, we can:
- **Reduce Hit Time**, by having a small and fast cache.
- **Reduce Miss Rate**, by having a large or smart cache.
- **Reduce Miss Penalty**, by having a fast / large main memory access.

Below, we'll discuss various ways we can reduce AMAT.

### Reducing Hit Time
**Pipelined Cache**: We can pipeline our cache so that multiple accesses can be processed at once! 
> In an unpipelined-cache, if we access the cache in cycle $N$, then accesses in later cycles will have to wait until our first access is done. 

1. Reading out the tags
2. Determining the hit by comparing values
3. Selecting data within the line (using an offset)

---

**Overlapping TLB and Cache Access**: We can combine access of our TLB with our cache access to avoid repeating expensive computations.

- **Physically Indexed, Physically Tagged Cache (PIPT)**: The cache stores data according to physical addresses, and uses the TLB to translate the addresses.
- **Virtually Index, Virtually Tagged (VIVT)**: The cache stores data according to virtual memory addresses. This means the cache doesn't need to use the TLB.
  > However, there are sitations where we still need to access the TLB on hit! (ex. we need to read permissions).
  
- **Virtually Indexed, Physically Tagged (VIPT)**: The cache indexes data using virtual addresses, but stores tags in physical addresses. This lets us quickly determine hits, while keeping the tag that can be checked with the TLB.
  - In a VIPT cache, **all index bits must come from the page offset**. Otherwise, it may be possible to have two virtual addresses that map to the same physical address!

---

**Way Prediction**: Before comparing all of our tags, we will first **guess** what line in our cache is more likely to hit. If wrong, we'll check all of the lines as normal. 
> If our guess is right, we'll get a really fast hit!

There are a few ways we can make this guess:
- **Random**: Randomly guess a line. Gives us potentially fast hits, but at a very high miss rate.
- **LRU**: Use the LRU to guess a line. Has a low miss rate, but updating the counters makes our hits slower.

---

**Replacement Policy**: Smartly replacing our cache lines on misses will give us a higher chance of getting hits later.

- **Not Most Recently Used (NMRU)**: Track the most recently used block in a set, and randomly remove any other block on replacement.
- **Pseudo-LRU (PLRU)**: Keep 1-bit per line in a set, and on every line access, set the bit to 1. On replacement, replace any line with bit set to 0, and set it to 1. If this is the last line that gets bit 1, reset the bit for all other lines.

### Reduce Miss Rate
To reduce the miss rate, we first need to understand why misses occur. There are 3 types of misses:
- **Compulsory Miss**: Miss the first time each block is accessed.
- **Capacity Miss**: Miss because the cache size is limited.
- **Conflict Miss**: Miss because of limited associativity.

The following ways can help us reduce miss rates.

---

**Prefetching**: We can guess what blocks will be accessed soon, and bring them into the cache ahead of time. This will let us avoid a miss!
> If we guess incorrectly though, we'll get higher misses, since we brought something useless into the cache (**cache pollution**)!

1. **Software**: One way to implement prefetching is to add prefetech instructions to the instruction set, and let the compiler figure out when to request them.
2. **Hardware**: Another way is to implement it in hardware, which guesses that will be accessed soon. This includes:
   - Stream buffers
   - Stride prefetchers
   - Correlating prefetchers

---

**Loop Interchange**: A compiler optimization where we change the order of iteration to match memory layout better.

For example, suppose we had the following loop:
```cpp
for (int j = 0; j < 10000; j++)
    for (int i = 0; i < 40000; i++)
        c[i][j] = a[i][j] + b[i][j];
```
As we iterate through i, we find that `a[i][j]` and `a[i+1][j]` are thousands of elements apart! This means we'll get a lot of cache misses.

Instead, if we rewrote the loop as so, we'd be able to use our cache a lot better.
```cpp
for (int j = 0; j < 10000; j++)
    for (int i = 0; i < 40000; i++)
        c[i][j] = a[i][j] + b[i][j];
```

### Reduce Miss Penalty
The following methods may help us reduce the miss penalty.

---

**Overlap Misses**: On a cache miss, we can continue to perform other operations during the miss so that we're still performing work. 
- Find other independent instructions to execute
- Overlap cache misses and process other requests during the miss.

The latter is only possible in a **non-blocking cache**, a cache that allows other requests to be processed while a miss is being serviced. 
> A **blocking cache** will service one access at a time, so during a miss, other accesses are blocked.

With non-blocking caches, we can do:
- **Hit Under a Miss**: Allow cache hits while one miss is in progress, but block other misses.
- **Miss Under Miss**: Allow hits and misses while a miss is in progress.
  - This requires that the memory system allows multiple requests, called **Memory Level Parallelism (MLP)**.
  
To track pending misses for the **miss under miss** policy, we use a **Miss Status Handling Register (MSHR)**. The MSHR tracks the status / data of misses that are currently being handled.
- On a cache miss, search the MSHR for a pending access to the same block.
  - If **found**, allocate a load/store entry in the same MSHR entry
  - If **not found**, allocate a new MSHR entry
  - If the MSHR has no free entries, stall
- When the data returns from memory,
  1. Check what loads/stores are waiting on the data, and forward the data to the load/stores. Then, deallocate the load/store entry. 
  2. Write data in the cache, and deallocate the MSHR entry after writing to the cache

---

**Cache Hierarchy**: Maintain multiple caches of varying size. As the cache gets smaller, it generally gets faster-- and we store them in order of L1, L2, L3... (in order of increasing size / decreasing speed).

Cache hierarchies reduce the chance we need to fetch data from memory, as a miss in one cache may still yield a hit in a slower cache. 
$$
\begin{align*}
\text{AMAT} = \text{HitTime}_{L1} + \text{MissRate}_{L1} \text{MissPenalty}_{L1} \\
\text{MissPenalty}_{L1} = \text{HitTime}_{L2} + \text{MissRate}_{L2} \text{MissPenalty}_{L2} \\
\text{MissPenalty}_{L2} = \text{HitTime}_{L3} + \text{MissRate}_{L3} \text{MissPenalty}_{L3} \\
\end{align*}
$$

Because we now have a hierarchy of caches, any hits in one cache are not propagated into the lower caches. Given this, how do we measure the miss rate of our caches?
- **Global Miss Rate**: \# Misses Divided by All Memory References
- **Local Miss Rate**: \# Misses Divided by \# Misses of Previous Cache

We may also use **Misses per 1000 Instructions (MPKI)**, which similar to global miss rate, but also normalizes misses to the number of total instructions as well (not just memory references).


# Cache Coherence
## Definition
So far, we've looked at a single processor and how caching makes it much faster. However, we don't always just have one processor! When we have multiple processors, we need a way to make all caches behave as a single memory!
> If Core A writes $x = 15$, then Core B must be able to read $x = 15$.

The mechanism of doing this is known as **cache coherence**. This is defined by 3 properties:
1. **Read What is Written**: A read from address X on Core1 returns the value written by the most recent write to X on Core2, if **no other processor has written to X between that time**.
2. **Writes Happen Eventually**: If Core1 writes to X and Core2 reads X after sufficient time, and there are no other writes to X between, Core2's read returns the value written by Core1.
3. **Casuality of Writes**: Writes to the same location are serialized; two writes to location X are seen in the same order by all processors.

## Maintaining Cache Coherence
Let's look at a few ways we can maintain cache coherence.
> One way we can easily enforce this is by **sharing caches**, but this does not give good performance and is not scalable.

The basic premise is to force reads in one cache to see writes in another. This has two components:
- First, how a write in a cache affects other caches
  - **Write-Update Coherence**: After every write, we update the other caches.
  - **Write-Invalidate Coherence**: After every write, we prevent hits to other caches by invalidating all other lines of the same address. This way, they retrieve data only when needed.
- Second, how to broadcast the required data from the writes to other caches
  - **Snooping**: Writes are broadcasted on a shared bus.
  - **Directory** Each block of memory is assigned an ordering point.

> Write-Invalidate Coherence is more commonly used.


### Write-Update Coherence
The premise of **Write-Update Coherence** is simple. Anytime we have a write, we will update the content of every other cache.

For example, consider 4 cores. Now say core 0 reads 0x700 (and gets value 6). Then, our cores would look as follows: 
| Core 0 | Core 1 | Core 2 | Core 3 |
| :-: | :-: | :-: | :-: | 
| V: 1, T: 700, Data: 6 | | | |

Say core 1 reads 0x700. It pulls the value that core 0 has.
| Core 0 | Core 1 | Core 2 | Core 3 |
| :-: | :-: | :-: | :-: | 
| V: 1, T: 700, Data: 6 | V: 1, T: 700, Data: 6 | | |

Now, say core 2 writes 0x700 (say 17). This will update both core 0 and 1.
| Core 0 | Core 1 | Core 2 | Core 3 |
| :-: | :-: | :-: | :-: | 
| V: 1, T: 700, Data: 17 | V: 1, T: 700, Data: 17 | V: 1, T: 700, Data: 17 | |

Finally, say core 3 reads 0x700. It will also pull 17.
| Core 0 | Core 1 | Core 2 | Core 3 |
| :-: | :-: | :-: | :-: | 
| V: 1, T: 700, Data: 17 | V: 1, T: 700, Data: 17 | V: 1, T: 700, Data: 17 | V: 1, T: 700, Data: 17 |

Below are some write-update optimizations we can do. 

> [!Tip] Write-Update Optimization: Dirty Bits
> If we write back to memory on every write, our memory can quickly become a bottleneck. Instead, we can use write-back caches so that the memory is not responsible for every write. 
>
> Now, when a cache is written to, it broadcasts the write for other caches to update, and **sets its own dirty bit to 1**. With this bit set, we know that: 
> 1. The memory is not updated for what's stored in that cache line
> 2. This particular cache has the responsibility of keeping memory updated on replacement.
>
> At any given moment, only one line should have its dirty bit set for any given memory block.
> 
> Now, on a cache write:
> - Write the line into the cache.
> - For any other caches with the same line, update their value.
> - Set the dirty bit to 1 (most recent data), and set all other dirty bits for the same line to 0 to signal that this cache is responsible for updating memory.

> [!Tip] Write-Update Optimization: Shared Bits
> Another optimization is to reduce the number of bus writes. The more writes we have in the bus, the more of a bottleneck our bus becomes.
> 
> To do this, we will add a **shared bit** to cache lines, to signal if this data is in other caches. If the shared bit is not set (0), then the cache does not need to broadcast the data to the other caches.
>
> So, for any read/write:
> - Check if any other cache has the memory address. If so, set all shared bits to 1.
>
> > If this is done for Write-Invalidate, then we shold also check if we can toggle off the shared bit. This will let us minimize bus usage.

### Write-Invalidate Coherence
In **Write-Invalidate Coherence**, anytime we get a write, we will invalidate every other copy of the data. This forces a miss the next time the invalidated data is accessed. 

Write-Invalidate Coherence also uses shared and dirty bits. The benefit of this protocol is that after a write, subsequent writes won't need to issue invalidations, as the data will no longer be shared!

## Snoopy Protocol
Instead of using a valid bit, dirty bit, and shared bit, it helps to define states to track the state of caches. Introducing the **MSI Snoopy Protocol**!

### MSI Snoopy Protocol
In MSI, any cache block can have the following states:
- **Invalid (I)**: Valid 0
  - The data for that cache is not valid.
  - To read or write, a request must be made on the bus.
- **Modify (M)**: Valid 1, Dirty 1
  - The cache has the block, and its dirty, so the memory not updated.
    - When replacing block, memory must be updated
  - No other cache has the block
    - Read or writes to the block can be done without the bus.
- **Shared (S)**: Valid 1, Dirty 0
  - The cache has the block and its clean (updated with memory).
    - When replacing the block, no memory update is needed.
    - Reads from the block can be done without the bus
  - The block may or may not be shared with others.
    - To write, an upgrade request must be sent
  

> We will build onto this protocol with additional states.

Based on these states, the MSI Snoopy Protocol defines the following state machine. 

![[Classes/CMSC411/Resources/MSI.png]]

To maintain coherence, a cache can issue **coherence requests** on the bus, so that other caches can snoop / update themselves accordingly.
- **GetS Request**: Issued on a read miss; requests data with the intent to share.
  - Notifies other caches that they are now sharing the data.
- **GetM (GetX) Request**: Issued on a write; requests data with the intent to modify.
  - Notifies other caches that a write occurred, so they must invalidate.

> [!Info] Cache to Cache Transfers
> Suppose one core has block $B$ in state $M$, and another core wants to read $B$. To do this, it will put a `GetS` on the bus.
> 
> Because core 1 has the most recent data for $B$, it has to somehow provide this data! This is known as a **cache to cache transfer**. But how?
> 1. **(1) Abort / Retry**: Core1 can cancel (abort) the `GetS` request, and write the data back. Core2 can then later retry `GetS` to get the data from memory.
>    > This can be really slow, since memory becomes a bottleneck!
> 2. **(2) Intervention**: Core1 can submit an **intervention** bus signal, indicating it will supply the data. Then, when writing the data back to memory, Core2 can snoop the data transfered by Core1 during the write-back.
> 
> ```mermaid
> graph LR
> 0[Invalid];
> 1[Shared];
> 2[Modified];
> 
> 1 -. See GetM .-> 0;
> 1 -. See GetS .-> 1;
> 2 -. See GetM, Writeback Data .-> 0;
> 2 -. See GetS, Writeback Data .-> 1;
> ```
> 
> This works, as the data is in the $M$ state, so it is clear that nobody else has the correct data. Cache to cache transfers let us avoid the overhead of using memory!

### MOSI Snoopy Protocol
What if a cache has requested data that is shared? If we wanted to do a cache to cache transfer, who should supply the data?

We can handle this case is by introducing a new state, **Owner (O)**! The owner will be responsible for performing cache to cache transfers on shared caches.
- The cache has a clean copy of the data, that is potentially shared with others.
- This cache is responsible for providing the data on a `GetS` request.

To guarantee that only one cache is in the owner state at a time, we will turn $M$ caches into $O$ caches on snoop reads. 
- If we are in $M$ and snoop a read, provide data and move to $O$ state. 
- If we are in $O$ state and snoop a read, we provide data.

The addition of the owner state into our model is called the **MOSI** model. For a single block, we have the following state machine:
![[Classes/CMSC411/Resources/MOSI.png]]

### MESI Snoopy Protocol
We can do even better than this! 

Right now, if a core reads a block, it goes into the shared state. Then, on a write, it needs to issue a `GetM` on the bus. But if no other core has the block, this request doesn't need to be issued! 

To address this, we can add yet another state, the **Exclusive (E)** state.
- Our cache has the only clean copy besides memory

The exclusive state means that this cache can perform cache to cache transfers. Additionally, it means that on a write request, this cache can **silently upgrade to $M$ without using the bus**!

![[Classes/CMSC411/Resources/MESI.png]]
> On a `GetS`, to know that our block is exclusive, we also add a **Share** bus signal. If another core snoops the request, it can pull this signal to 1 to indicate if other cores have the same block or not.

### MOESI Snoopy Protocol
When we combine these states together, we get the **MOESI Model**.
- $M$: Modified
  - I have the only copy, and it's dirty (memory is not updated).
- $O$: Owned
  - I have the most up-to-date copy, but others may have copies too.
  - I am responsible for supplying data and updating memory.
- $E$: Exclusive
  - I have the only copy, and its clean
- $S$: Shared
  - There are multiple copies present, all of which are clean
- $I$: Invalid

We can define these states with 3 bits: a valid bit, a dirty bit, and a shared bit.

| | I | E | S | M | O |
| :- | :-: | :-: | :-: | :-: | :-: |
| Valid | 0 | 1 | 1 | 1 | 1 |
| Dirty | X | 0 | 0 | 1 | 1 | 
| Shared | X | 0 | 1 | 0 | 1 | 

![[Classes/CMSC411/Resources/MOESI.png]]

> [!Info] Coherence Cache Misses
> With multiple caches, we now have a new additional type of miss, the **coherence  miss**. These happen when writes to one block in a cache invalidate blocks in another cache (causing a miss).
> - **True Sharing** occurs when different cores access the same data, so a coherence miss is inevitable.
> - **False Sharing** occurs when different cores access different data in the same block, so a coherence miss only occurred because of the granularity of the blocks.

## Directory-Based Coherence
One of the drawbacks of snooping is that the reliance on the bus can quickly become a bottleneck if we scale our processor up to several cores. Here, instead, we'll consider non-broadcast networks.

**Directory-Based Coherence** instead relies on a directory data-structure, which is distributed across cores. 
- For any directory entry, it has a **dirty bit**, indicating if the block is dirty, and 1 bit per processor, indicating if that processor's cache has the line. 
- Each block has its own directory entry. 

> By tracking what processors have the block, the directory tracks what caches need to be notified on an update (without wasting bandwidth). 

The MOESI model can be integrated into a directory based coherence structure as well, in a similar way to the snoopy protocol.

> [!Info] Exclusive State, Directory
> When a node enters the exclusive state in directory, it will mark dirty to 1. This will let it silently upgrade to $M$ without accessing the directory.

> [!Info] Optimizations: Reducing Directory Overhead (Processors)
> Instead of storing 1 bit per core, we instead represent cores with **Node IDs**. For $K$ cores, we'll need $\log K$ bits to represent it's ID.
>
> Then, for each block, we can store $N$ node IDs. We can then tune $N$ such that 
> $$
> N \times \log K < K
> $$
> If there are not enough node spaces, we broadcast instead. 
>
> Another option we could do is grouping processors. Then, send point-to-point messages to all processors within a group!

> [!Info] Optimizations: Reducing Directory Overhead (Memory)
> Directories take up a lot of memory. To reduce the amount of overhead, we won't store directory entries for all memory blocks! Instead, we will have one entry per cache line!
