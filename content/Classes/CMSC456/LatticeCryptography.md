---
title: Lattice Cryptography
tags:
- cmsc456
---

Advances in quantum computing has quickly turned many of our modern cryptographic standards obsolete. Here, we talk about new hard problems which are forming the new basis of post-quantum cryptography.

# Lattice Based Cryptography
## Lattices
An $n$-dimensional lattice $L$ is an additive discrete subgroup of $\mathbb{R}^n$. Given a basis forming $\mathbb{R}^n$, we can use it to define a lattice as 
$$
L(B) = \{ v \in \mathbb{R}^n : v = Bz, z \in \mathbb{Z}^n \}
$$
In other words, the integer linear combinations of the basis vectors.
> This forms a grid of points in space!

Given two bases $B, B'$, they define the same lattice if and only if $B' = BU$, where $U$ is a **unimodular matrix**, an integer matrix with determinant equal to $\pm 1$.

With lattices, we have the following hard problems. Given "approximation factor" $\gamma > 1$:
1. **Shortest Vector Problem (SVP)**: Given a basis $B$, find a non-zero vector in the lattice whose length is at most $\gamma * \lambda_1 (L(B))$.
2. **Shortest Independent Vector Problem (SIVP)**: Given a basis $B$, find a linearly independent set $\{v_1, \dots v_n\}$ such that all vectors have length at most $\gamma * \lambda_n (L(B))$. 
3. **Gap Shortest Vector Problem (GapSVP)**: Given a basis $B$, and a radius $r > 0$, 
   - Return YES if $\lambda_1 (L(B)) \le r$
   - Return NO otherwise.

## Shortest Integer Solution (SIS)
Consider the following scheme called the **Shortest Integer Solution (SIS)** problem.

Given a random public matrix $A$, find the shortest vector $z$ such that
$$
A z = 0 
$$
In other words, find the shortest vector that is in the null-space of $A$.
> Finding vectors in the nullspace is not hard. However, finding the **shortest** vector in a space is hard!

## Learning with Errors (LWE)
Since lattices are often hard to work with, we have a simplified representation. Now, many of us use the intermediate problem **Learning with Errors (LWE)**.

**(Search) LWE** has the following setup: 
- Take $A$ with random entries, $e$ with random (and small) noise. 
- Given $A$ and $u = As + e$ (under $\mathbb{Z}_p$), compute $s$ (where $e$ is chosen randomly).

> In our case, we will consider $e$'s entries to take on values $(-1, 0, 1)$ with $1/3$ probability each.

There is also an equivalent **Decisional LWE** problem. 
- You are given $(A,u)$ or $(A,v)$, where $v$ is chosen randomly.
- Try to distinguish which one you got.

Both search and decision LWE are equally hard.

### Regev's Cryptosystem
LWE sets up a post-quantum scheme called **Regev's Cryptosystem**. 

First, choose a random public matrix $A$ from $\mathbb{Z}_p$, and a random secret vector $s$. Then, use LWE to compute
$$
u = As + e
$$
Where $e$ is small. Here, $A, u$ will be our public key, and $s$ will be our secret key.
> For our purposes, we will say that $e \in \{-1,0,1\}^n$.

Our scheme works as follows:
1. **Encryption**: For $r \in \{0,1\}^m$ chosen at random, compute $c_1 = r^T \times A$. Then, compute $c_2 = \text{dot}(r, u) + m * \lfloor \frac{p}{2} \rfloor$. Our ciphertext is $(c_1, c_2)$. 
   - Here, we choose the size of $r$ to be larger than the output size, so that we cannot recover $r$ (since we lose information)
2. **Decryption**: Compute $c_2 - c_1 * s$ to get
   $$
   c_2 - c_1 * s = r(As + e) + m * \frac{p}{2} - rAs = \text{dot}(r,e) + m * \frac{p}{2}
   $$
   And because $e$ is small, we will locally be close to a single message point, letting us unambiguously determine what our message is. This requires we set things up so that $|r \cdot e| \le m < \frac{p}{4}$.

    > In the case that our setup is secure, then $\text{dot}(r,e)$ essentially functions as a one-time pad, as it yields a random result.
    
## Rejection Sampling
Suppose we want to sample from a distribution $D_f$ with probability density function $f$. However, we are only given draws from a distribution $D_g$ with probability density function $g(x)$. Could we simulate sampling from $D_f$ with $f(x)$?
> Sometimes, it may be cheaper or simpler to sample from $D_g$ than $D_f$. 

If we assume that for all $x$, $f(x) \le M * g(x)$, then we can do this as follows:
- For $x$, sample from $D_g$.
- Accept $x$ with probability $\frac{f(x)}{M * g(x)}$.

This will give us a scaled version of $f$. This is because
$$
Pr[\text{x Accepted}] = g(x) * \frac{f(x)}{M * g(x)} = \frac{f(x)}{M}
$$
Thus, after normalizing, we can recover our desired distribution.

### Lyubashevsky's Scheme
Rejection sampling lets us create a lattice-based signature scheme, known as **Lyubashevsky's Scheme**.
- **Prover**:
  1. Compute $A \times S = T$, where $S$ has small entries. Then, our public key is $A,T$, and our secret key is $S$.
  2. Now, compute $y$ from the Gaussian distribution. Compute $A \times y = d$.
  3. Hash this to get $H(d || m) = c$, and compute $S \times c + y = z$. Output $(c,z)$.
- **Verifier**:
  1. A verifier can compute $A \times z - T \times c = d$. Now, check that $c = H(d || m)$ and $z$ is short.
