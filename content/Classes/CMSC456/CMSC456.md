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

> When $G$ has a finite number of elements, we say $G$ is **finite** and let $|G|$ denote the order of the group.

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

> [!Abstract] Theorem: Euclidean Algorith
> Let $a, p$ be 
