---
title: Hash Tables
tags:
- cmsc420
---

In this article, we discuss the Hash Table data structure. These useful data structures provide $O(1)$ **amortized** insertion / deletion / search operations (discussed more later)!

> [!Warning] Common Misconceptions
> Hash Tables are not to be confused with Maps, Lookup Tables, or Associated Arrays! We can implement the latter with Hash Tables, but can also implement them with other data structures like BSTs!
>
> **Maps** are key-value stores that a variety of languages use, but the data structure that actually implements the map depends on the language. 

# Hashing / Hash Functions
## Hash Functions
A **hash function** is a mapping from some input domain $K$ to $\mathbb{N}$, where the output is often within a finite range (due to machine constraints).

$$
h : K \to \mathbb{N}
$$

Hash functions can convert non-integer keys into integers, giving us a convenient way to index non-integer keys! This way, we can access non-integer keys in $O(1)$ time through array indexing. 
> This is the core idea behind Hash Tables!

However, it is often infeasible and impractical to allocate arrays that accomodate the function's entire output range! Intead, we will opt to allocate an array of smaller size $M$, and take the **modulus** of the hash function's output to constrain the output within the array's valid indices.
$$
H(x) = h(x) \mod M
$$

This is the function (given some hash algorithm) that is used in hash tables!

> [!Warning] Hashing Mutable Objects
> Note that when hashing, the **only parts of the key we can hash on** are the immutable parts! Otherwise, the key's hash could change, which would prevent us from finding it in the hash table!

## Desirable Properties of Hash Functions
Not all hash functions are the same! We say a hash function is **good**, when the following 3 properties are satisfied:
1. **Uniformly Distributed**: The function uniformly distributes values over the range, reducing **collisions** (where two keys hash to the same index), and thus avoids the computational cost of resolving these collisions.
2. **Efficient**: The function should be efficient to compute, as we will need to hash on every operation, and sometimes even multiple times.
3. **Consistent**: The function should be **consistent** on the same keys. If $k1$ and $k2$ are the same key, their hashcodes should be equal! Note that the converse of this may not be true.

## Example Hash Functions
See below for the hashing of some basic types. Note that you likely will never need to write your own hash function, as languages often have good hashing already.

Note that in the hashing of some languages, some hash functions may return negative values (ex. Java and Python). In these cases, we need to remove this negative value! This can be done very easily with the absolute value, or bitwise operations.

> [!Example]+ Example: Hashing Basic Types (Character)
> Each character can be assigned a numeric value (such as ASCII), and this numeric value can be its hash. This isconvenient, as there are only 128 possible characters that we can hash!

> [!Example]+ Example: Hashing Basic Types (String)
> As strings are sequences of characters, we need some way to combine the character values.
>
> A common way to combine the values is as given below. Define some integer value $R$. Then, for every character $c$ in the string, we calculate the new hash as
> $$
> (R * \text{hash} + \text{value}(c)) \mod M
> $$
> And repeat this process until we have iterated through all characters in the string.
>
> In doing this, we are essentially creating a number in base-$R$, where every character in the string is in a distinct base from the others! Thus, if we know we have 100 characters, for example, we can let $R = 100$ to give each character its own base in the hash!
> > The modulus $M$ is done to keep intermediate values small, so our numbers are manageable.

> [!Example]- Example: Hashing Basic Types (Floating-Points)
> One "intuitive" way to hash floating-point values would be to round, but this would give us contiguous ranges that hash to the same value. In practical applications, this likely won't be very good!
>
> Instead, note that floating-points have a binary representatio. We can treat this representation as a string, where $0$'s and $1$'s are their own characters, and perform our string hash!


# Hash Tables
## Basic Structure
A **hash table** is comprised of a continguous array of length $M$ (where each index is called a **bucket**), and a good hash function to hash keys.

The core idea with hash tables is that given a key $K$, we can use the hash function to hash the key to an index in the array! This way, we can insert, delete, or search for the key in $O(1)$ time. 

```python
class HashTable(object):
    def __init__(self):
        self._M = 15
        self._buckets = [None] * self._M
        
    def insert(self, k, v):
        h = abs(hash(k)) % self._M # hash value
        self._buckets[h] = (k,v)
```

Unfortunately, hash tables aren't this simple, and a variety of issues can arise with **collisions**, where multiple keys hash to the same index. Collisions will make our hash table less efficient, so we want to avoid them to have an effective data structure.

There are a variety of ways we can reduce and resolve collisions, which are discussed in following sections.

## Hash Table Size
### Choosing the Hash Table Size
First, we should consider the hash table size $M$. How do we choose a good size?

Say we have $M$ buckets in our hash table, with the hash function
$$
h(x) = x \mod M
$$
Now say we insert a sequence of keys equally spaced apart such that $x_i = i * n$, where $n$ is some integer. This would give us insertions into buckets $i \times n \mod M$. 

For example, if we have $M = 100$, $n = 20$, then we would insert into buckets
$$
0, 20, 40, 60, 80, 0, 20, \dots
$$
Which would only use 5 buckets out of 100, which would guarantee collisions after the 5th element!

In general, the number of buckets we use for the sequence is given as
$$
\frac{M}{\text{GCD}(M,n)}
$$
Where $\text{GCD}()$ is the greatest common divisor of $M$ and $n$. 

Thus, if we minimize the greatest common divisor between $M$ and $n$, we will use the entire array! As $n$ can be any value, the best way to minimize this divisor is to **choose $M$ to be prime**. This way, $\text{GCD}(M,n)$ is **(almost) always** 1.

> [!Info] Hash Table Size
> In choosing our hash table size $M$, we ideally want $M$ to be prime.

### Hash Table Resizing
Note that no matter how we size our hash table, collisions will inevitably become more common as our table fills out. Thus, we will want to resize our table to reduce collisions!

Many data structures (ex. `ArrayList`) simply double their size, but this wouldn't give us a prime size! Thus, for our new size $M_2$, we will choose the **first prime number before $2M$.
> This can easily be done with a static (precalculated) lookup table!

To resize our hash table, we'll have to reinsert every key-value pair as the modulus changes (causing all hash values to change!). Interestingly enough, tables become more efficient as we resize more aggressively (though this will require more reinserts)!
> Resizing at 60-80% capacity is fairly common in hash tables. For the purposes of CMSC420, we will use 50% as our threshold.

Resizing is typically automatically done on insertion. To resize, we do the following:
1. Before inserting an element, check if the capacity has exceeded the threshold.
2. If it has been, then resize the hash table.
   - Iterate through the hash table array, and for any key found, hash / insert it into the new (resized) array.
3. Then, hash / insert our new element.

> [!Info] Resizing Hash Tables
> To resize a hash table, find the first prime number smaller than $2M$, and reinsert every element into the new hash table.

## Collision Handling
Even if we choose a good hash table size and a good hash function, collisions may still happen! In fact, handling collisions is a normal part of hash table operations.

To compare different methods of collision resolution, we will define a new unit of complexity, the **probe**. A **probe** refers to a memory access in the hash table array.
> In the best case, it will take one probe to insert or retrieve an item from our hash table. In the worst case, we may have to resize, or resolve a collision!

### Separate Chaining
Suppose the hash table bucket we hash our key to already has a key. To resolve the collision, we could simply make the bucket bigger!

This is the core idea behind one class of collision resolution mechanisms, **chaining**.

In **separate chaining**, each bucket in our hash table stores a Linked List, rather than a single item. This way, we can resolve collisions by adding to our list! Given that we're using a Linked List, we can add to the head to insert in $O(1)$ time.
> This can be quite useful in limited memory contexts, as we storage non-contiguous elements! However, this also means that we cannot use caching to our advantage.

Note that this is fast for insertion, but as a consequence of this, searching will no longer take $O(1)$ time, and now will take linear time equal to the bucket's size.

A nice "middle ground" to this is **ordered separate chaining**, where elements are inserted into the bucket in **sorted order**. This makes insertion linear (which sometimes may not be desirable), but lets searching be faster!
> This however, is only the case if we expect our searches to fail often. If we expect our searches to succeed, then sorting doesn't really do much for us.

### Open Addressing
Suppose the hash table bucket we hash our key to already has a key. To resolve the collision, we could utilize free spaces within the hash table itself to resolve the collision!

This is the core idea behind another class of collision resolution mechanisms, **open addressing (closed hashing)**. There are numerous ways to make this happen, but they all involve offsetting the key's index using a deterministic algorithm, and continuing this until we find an open bucket. 

A common form of open addressing is **linear probing**, where we continuously increment our index by $1$ until we find an empty bucket. 
1. Hash our key (resize if needed). 
2. Check the corresponding bucket.
3. If the bucket is full, increment our index by 1 and repeat step 2.
4. Otherwise, the bucket is free, so we insert our key here.

For example, suppose we have keys $81, 68, 75$, where $81$ and $75$ hash to index 1, and $68$ hashes to index 2. Then, linear probing would do the following:
$$
\begin{align*}
    &\_, \_, \_, \_, \_ \\
    &\_,\colorbox{blue}{81}, \_, \_, \_ &\text{1 Probe} \\
    &\_, 81, \colorbox{blue}{68}, \_, \_ &\text{1 Probe} \\
    &\_, \colorbox{purple}{81}, \colorbox{purple}{68}, \colorbox{blue}{75}, \_ &\text{3 Probes} \\
\end{align*}
$$

Note from the above example that open addressing increases the number of probes that may be needed while inserting. Furthermore, this rate will increase as our table fills up. 

> [!Info] Clusters and Collision Chains
> To see why insertion / search become expensive, consider a key's **collision chain**, the group of cells which can be reached with subsequent linear probes.
>
> Whenever we hit any collision chain, we have to follow it to its end for insertion, and in the worst-case search! 
>
> Inserting into any collision chain will cause it to grow, and as we insert more elements, we risk merging collision chains together! This creates larger and larger clusters that are inefficient to traverse through!
>
> > This is a problem with open addressing in general. Changing the offset to the index (instead of adding 1) will still create these clusters!

Thus, to minimize the number of probes performed, it may may be worth resizing the table at a specific capacity threshold (refer to hash table resizing).
> By convention, we will set the threshold to a 50% full table, though this is conventionally done between 60-80%.

> [!Info] Deletion with Linear Probing
> While inserting / searching with linear probing is simple, deletion can be a bit more complex. In the case that we delete the element, we need to be careful that elements after can still be found upon a search.
> 
> There are two forms of deletion:
> - **Hard Deletion**: Remove the element entirely, and loop through the rest of the cluster, reinserting every element.
> - **Soft Deletion**: Replace the element with a "deleted marker", that will be treated as a normal (non-matching) element in search, but a deleted element in insertion. 
>   > Note resizing will treat such "deleted elements" as occupying a cell (to determine when to resize), yet ignore it when re-inserting.

> [!Abstract]- Knuth's Result for Linear Probing
> Say $\alpha$ of our cells are occupied (where we resize at a threshold greater than $\alpha$). Then, the average number of probes needed for:
> 1. A **successful search** is
>    $$
>    \frac{1}{2} \left( 1 + \frac{1}{1-\alpha} \right)
>    $$
> 2. A **failed search** is
>    $$
>    \frac{1}{2} \left( 1 + \frac{1}{(1 - \alpha)^2} \right)
>    $$
>
> Note that on average, successful searches will require fewer probes than failed searches. This is an interesting, well-known theoretical result for linear probing!


