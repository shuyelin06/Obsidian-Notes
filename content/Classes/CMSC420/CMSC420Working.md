---
title: CMSC420Working
tags:
- cmsc420
- wip
---

Working notes for CMSC420, Spring Semester 2024.


---

(Basic Data Structures)

# Hash Tables
*Hash Tables are not to be confused with Maps, Lookup Tables, or Associated Arrays! We We can implement the latter with BSTs and key-value pairs but not Hash Tables.*

## Hash Functions
### Key Idea
A **hash function** is a mapping from some input domain $K$ to $\mathbb{N}$, where the output is often within a finite range (due to machine constraints).

$$
h : K \to \mathbb{N}
$$

As hash functions can convert non-integer keys into corresponding integers, they provide a convenient way index non-integer keys into arrays! This could let us access non-integer keys in $O(1)$ time through array indexing.

However, it is often infeasible and impractical to allocate arrays to accomodate the function's entire output range! So intead, we opt to allocate an array of smaller size $M$, and take the **modulus** of the hash function's output to constrain the output within the array's valid indices.
$$
H(x) = h(x) \mod M
$$

A 
indices, which can be used

Typically, our output range is of a finite size, and are integers for convenient use in an array. This way, hash functions can be used to convert non-integer keys into a corresponding integer value!
