---
title: CMSC456
tags:
- cmsc456
---

This course covers the theory behind modern cryptography. The goal of this field is to **secure information**. To do this, we want to uphold:
- **Data Privacy**: Ensure that adversaries cannot see or obtain the message.
- **Data Integrity / Authentication**: The message origin can be verified (authenticity), and the message has not been modified in transit (integrity).

Common symbols / terminology:
- $M$: The message we want to keep secure
- $K$: A key we use to encrypt and/or decrypt the message
- $C$: The encrypted message; ciphertext.

Notes are below.
- [[SymmetricEncryption | Symmetric Key Encryption]]

---

# Number Theory
## Groups
### Definition
A **group** is a set $G$ along with a binary operation $\circ$ for which the following conditions hold:
- **Closure**: For all $g,h \in G$, $g \circ h \in G$.
- **Identity**: There exists an identity $e \in G$ such that $\forall g \in G$, $e \circ g = g = g \circ e$.
- **Inverse**: For all $g \in G$, there exists an element $h \in G$ called the **inverse** such that $g \circ h = e = h \circ g$. 
- **Associativity**: For all $g_1, g_2, g_3 \in G$,
  $$
  g_1 \circ (g_2 \circ g_3) = (g_1 \circ g_2) \circ g_3
  $$

> When $G$ has a finite number of elements, we say $G$ is **finite** and let $|G|$ denote the order (size) of the group.

We say a group $G$ with operation $\circ$ is **abelian** if it has the property of **commutativity**: $\forall g,h \in G, g \circ h = h \circ g$. 
> For the purposes of this class, we will only deal with finite, abelian groups.

### Group: Modular Arithmetic (Addition)
We say that two numbers $a,b$ are **congruent modulo $p$**, denoted
$$
a \equiv b \mod p
$$

If $p$ divides $(a - b)$, or in other words, $p \vert (a - b)$.

> [!Example] Example: Modular Equivalence
> All of the following are true.
> $$
> 2 \equiv 15 \mod 13 \qquad 
> 28 \equiv 15 \mod 13 \qquad
> -11 \equiv 15 \mod 13
> $$

Addition works in modular space as normal. You perform regular addition, and then take modulo $p$. For example,
$$
8 + 10 \mod 13 \equiv 18 \mod 13 \equiv 5 \mod 13
$$

Addition has the following properties. Consider the set of numbers $\mathbb{Z}_p = \{0,1,\dots p-1\}$:
- **Identity**: $\forall a \in \mathbb{Z}_p$, adding 0 to it yields the same number
- **Additive Inverse**: $\forall a \in \mathbb{Z}_p$, $\exists b$ such that $a + b \mod p = 0$, given as $b = p - a$.
- **Closure**: Any addition operations will yield a result that is still inside of $\mathbb{Z}_p$.
- **Associativity**: You can take modulo at any point in the operation. For example,
  $$
  ((a + b) \mod p + c) \mod p = (a + (b + c) \mod p) \mod p
  $$

The set $\mathbb{Z}_p$ with our addition modulo operator defines a group!

### Group: Modular Arithmetic (Multiplication)
For the purposes of security, we are mainly interested in **multiplicative** groups over the integers, as this introduces computational problems believed to be hard to solve.

Let's look at the **multiplication modulo $p$ group**. Let $Z^*_p = \{1, \dots p - 1\}$, with the multiplication mod operation. For $Z^*_p$ to be a group it must be true that **p is prime**. 
> If $p$ is not prime, then we won't have the property of the inverse!

We argue below that $Z^*_p$ satisfies the inverse property (the rest are trivial to prove). In other words, $\forall a \in Z^*_p$, there exists a $b$ such that $a * b \mod p = 1 \mod p$. 

> [!Example]+ Example: Brute Force Inverse
> Suppose we ant to find the multiplicative inverse of $9 \mod 11$.
>
> One way to do this is to brute-force iteratively try all 10 numbers in $Z^*_{11}$ to find our inverse. We will consider this brute-force to be exponential time! This is because when we're using this with respect to binary numbers, the length of our input is on the magnitude of $2^n$. 

> [!Abstract] Theorem: Euclidean Algorithm
> Let $a, p$ be positive integers. Then, there exists integers $X,Y$ such that $Xa + Yp = gcd (a,p)$. 
>
> The Euclidean algorithm can be used to compute $gcd (a,p)$ in polynomial time. We can then extend this to compute $X,Y$ in polynomial time.
> > This algorithm has time complexity $2 \log (b)$, for $gcd (a,b)$. 

We can use the Euclidean Algorithm to show that our group has a multiplicative inverse. 

> [!Note]- Proof
> Let $a \in Z^*_p$. Then, $gcd(a,p) = 1$ because $p$ is prime. By the Euclidean Algorithm, we can find $X,Y$ such that $aX + pY = gcd(a,p) = 1$.
> 
> Rearranging terms, we can find that $pY = (1 - aX)$, so $p$ divides $aX - 1$, so $Xa \mod p = 1$. In other words, $X$ is our multiplicative inverse for $a$. 


> [!Example]+ Example: Euclidean Algorithm
> Suppose we want $gcd(9,23)$.
> $$
> \begin{align*}
> 23 = 2 * 9 + 5 \\
> 9 = 1 * 5 + 4 \\
> 5 = 1 * 4 + 1 \\
> 4 = 4 * 1 + 0
> \end{align*}
> $$
> > Every iteration, we try to divide the second component of our product by our additive term.  
> 
> So, our greatest common divisor is 1 (take the $b$ term of the component before 0).

---

What about **Modular Exponentiation**? Given $a, m, N$, can we efficiently compute $a^m \mod N$?

One way we could compute this is as follows:
```python
def ModExp(a, m, N):
    temp = 1
    for i in range(1, m + 1)
        temp = temp * a % N
    return temp
```
But this has runtime $O(m)$, where $m$ could be exponential! For an efficient algorithm, we need our runtime to be on the logarithmic order.

We can, in fact, achieve an efficient algorithm with repreated squaring. Let $m = m_{n-1} m_{n_2} \dots m_1 m_0$ be the bits of $m$.
```python
def ModExp(a, m, N):
    s = a
    temp = 1
    for i in range(0, n):
        if (mi == 1)
            temp = temp * s % N
        s = s^2 % N
    return temp
```
This has runtime $O(\log_2(m))$! So, Modular Exponentiation can be done efficiently.

---

> [!Abstract] Theorem: Fermat's Little Theorem
> For prime $p$, integer $a$, $a^p \equiv a \mod p$. 
>
> > [!Info] Corollary
> > 
> > For prime $p$ and $a$ such that $gcd(a,p) = 1$, $a^{p-1} \equiv 1 \mod p$.

This theorem can be generalized to any finite group!

> [!Abstract] Theorem: Generalized Fermat's
> Let $G$ be a finite group with $m = |G|$. Then, for any element $g \in G$, appling the group operation to it $m$ times will yield 1. 
> $$
> g^m = 1
> $$

### Group: Modular Arithmetic (Multiplication), N Composite
What about multiplicative groups modulo $N$, where $N$ is composite? 

For numbers $\{1, \dots, N - 1\}$, only numbers $a$ such that $gcd(a,N) = 1$ have a multiplicative inverse by the Extended Euclidean Algorithm. All others do not have a multiplicative inverse, so because of this, to obtain a group, we must disclude these values from our group.
$$
Z^*_N = \{a \in \{1, \dots N-1\} : gcd(a,N) = 1\}
$$

Then, $Z^*_N$ is an abelian, multiplicative group.

Assume $N = p \cdot q$, where $p, q$ are distinct primes. What is the order of $Z^*_N$, denoted $\phi(N)$, the **Euler totient function**?
$$
\phi(N) = (p - 1) (q - 1) = N - p - q + 1
$$
> Intuitively, this is because we only have to take out numbers $1p, 2p, 3p, \dots q * p$ which have $q$ elements, and $1q, 2p, 3p, \dots q * p$ which have $p$ elements. We add 1 as we're double counting the $q * p$ element in our removal.

Generalizing this, we can find $\phi(N)$ as

> [!Abstract] Theorem
> Let $N = \prod_i  p_i^{e_i}$, where $\{p_i\}$ are distinct primes and $e_i \ge 1$. Then
> $$
> \phi(N) = \prod_i p_i^{e_i - 1} (p_i - 1)
> $$

> However, finding this prime factorization of $N$ is a very difficult problem! 

By this theorem, and using the previous theorems, we know that for any $a$ such that $gcd(a,N) = 1$,
$$
a^{\phi(N)} \equiv 1 \mod N
$$
This can be used as a "quick / easy" vertification that someone has found $\phi(N)$!
> A corollary of this theorem is that $g^x = g^{x \mod \phi(N)}$ (since every $\phi(N)$, we wrap around). This makes things easy if we can find the prime factorization of $N$. 

### Cyclic Groups
For a finite group $G$ of order $m$ and $g \in G$, consider
$$
\langle g \rangle = \{g^0, g^1, \dots g^{m-1} \}
$$
Here, $\langle g \rangle$ always forms a cyclic subgroup of $G$. As there may be repeats, $\langle g \rangle$ may be a subgroup with a smaller order than $m$.

If the order of $\langle g \rangle$ is equal to $G$, we say that $G$ is a **cyclic group** and $g$ is a **generator** of $G$

> [!Example]+ Example: Cyclic Group + Generator
> Define $Z^*_{13}$. Then, 2 is a generator of $Z^*_{13}$.
> 
> | Input | Output | | Input | Output |
> | :-: | :-: | - | :-: | :-: |
> | $2^0$ | 1 | | $2^6$ | 12 | 
> | $2^1$ | 2 | | $2^7$ | 11 | 
> | $2^2$ | 4 | | $2^8$ | 9 |
> | $2^3$ | 8 | | $2^9$ | 5 | 
> | $2^4$ | 3 | | $2^{10}$ | 10 | 
> | $2^5$ | 6 | | $2^{11}$ | 7 |
> | $2^{12}$ | 1 |
> 

Let $G$ be a finite group and $g \in G$. The **order** of $g$ i the smallest positive integer $i$ such that $g^i = 1$.

> [!Abstract] Propositions
> 1. Let $G$ be a finite group, $g \in G$ with order $i$. Then, for any integer $x$, we have $g^x = g^{x \mod i}$.
> 2. Let $G$ be a finite group and $g \in G$ with order $i$. Then, $g^x = g^y$ if and only if $x \equiv y \mod i$.
> 3. Let $G$ be a finite group of order $m$, and $g \in G$ with order $i$. Then, $i | m$.
