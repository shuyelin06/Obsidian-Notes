---
title: MATH475
tags:
- math475
---

Combinatorics and graph theory

---

# Section 1: 
## 1.1: The Basics
### Permutations
A **permutation** on an $n$-element set is an arrangement of the elements in a specific order. A **$k$-permutation** is an arragement of $k$ elements from the set.
> We assume that all elements are distinct, by property of sets.

The total number of $k$-permutations on an $n$ element set is given as
$$
P(n,k) = \frac{n!}{(n - k)!} = n (n - 1) \dots (n - k + 1)
$$

This is also known as the **$k^{th}$ falling factorial of $n$**. Let $n \ge k$ be positive integers. Then, the $k^{th}$ falling factorial is given as 
$$
(n)_k = n (n - 1) \dots (n - k + 1)
$$

> [!Example]+ Example: Permutations with Repetition
> How many rearrangements of $AAAABCDEEE$ are there? 
>
> Note the repetition. If they were all distinct, we would have $10!$ combinations!
>
> If we treat our $A$'s as 4 distinct letters, there are $4! = 24$ ways to permute them. Similarly, for $E$, there are $3! = 6$ ways to permute them. These cases should only be counted one in the original question, so we need to divide them out.
>
> So, we find that our answer is 
> $$
> \frac{10!}{4! \cdot 3!}
> $$

This result (and intuition) can be generalized to a theorem. 

> [!Abstract] Theorem: Multinomial Coefficient
> Suppose object 1 occurs $a_1$ times, object 2 occurs $a_2$ times, $\dots$ object k occurs $a_k$ times, to give us $n = a_1 + a_2 + \dots a_k$ objects.
>
> Then, the total number of arrangements of the $n$ objects is
> $$
> \frac{n!}{a_1! a_2! \dots a_k!} = \binom{n}{a_1 \; a_2 \; \dots \; a_k}
> $$
> Called the **multinomial coefficient**.

### Combinations
The total number of ways to create a $k$-element subset from $[n] = \{1, 2, \dots n\}$, **n choose k**, is denoted
$$
\binom{n}{k} = C(n,k) = \frac{n!}{k! (n - k)!}
$$
and called a combination of **binomial coefficient**.
> Note that this is essentially a permutation without the ordering! This is why we divide by $k!$ - we're removing all cases that have the same ordering!

> [!Example] Example: Combinations
> There are 5 cats, 4 dogs, 5 mice. Three are chosen. 
> 
> What are the total ways to get exactly 2 cats, 1 dog? Well, out of our 5 cats we choose 2, and out of our 4 dogs we choose 1! This gives us
> $$
> \binom{5}{2} \binom{4}{1}
> $$
>
> What are the total ways to get at least 1 cat (3 animals total)? Note that in this case, we can't simply do $\binom{5}{1} \binom{13}{2}$, as this double counts some cases! Instead, we want to make our cases mutually exclusive.
> 1. First, say we choose 1 cat. We have $\binom{5}{1} \binom{9}{2}$ options (choose 2 from the other non-cats to make 3).
> 2. Next, say we choose 2 cats. We have $\binom{5}{2} \binom{9}{1}$ options (choose 1 from the other non-cats to make 3).
> 3. Finally, say we choose 3 cats. We have $\binom{5}{3}$ options.
> This gives us
> $$
> \binom{5}{1} \binom{9}{2} + \binom{5}{2} \binom{9}{1} + \binom{5}{3}
> $$
> options.

> [!Abstract] Binomial Theorem
> For a positive integer $n$, we have
> $$
> (x + y)^n = \sum_{k=0}^n \binom{n}{k} x^k y^{n-k}
> $$
> 

The proof for above is omitted. However, intuitively, you can think of it as expanding $(x + y)^n = (x + y)(x + y) \dots$

Then, for any $x^k y^{n-k}$, we can find its coefficient by choosing $k$ $(x + y)$ terms to contribute to the x, and choosing the remaining $n - k$ terms to contribute to the way. We find all ways we can do this (leading to the binomial coefficient you see!)

> [!Example] Example: Binomial Theorem Intuition, Extended
> Suppose we are interested in the coefficient of $x_1^3 x_3 x_4$ from $(x_1 + x_2 + x_3 + x_4)^5$!
>
> Well, of the 5 $(x_1 + x_2 + x_3 + x_4)$ terms, we choose 3 to multiply the $x_1$, 1 to multiply the $x_3$, and 1 to multiply the $x_4$. This gives us
> $$
> \binom{5}{3} \binom{2}{1} \binom{1}{1} 
> $$
> > This is essentially permutations with repetition!

> [!Abstract] Multinomial Theorem
> $$
> (x_1 + \dots x_k)^n = \sum_{a_1 + a_2 + \dots a_k = n} \binom{n}{a_1 \; a_2 \dots a_k} x_1^{a_1} x_2^{a_2} \dots x_k^{a_k}
> $$

## 1.2: Counting in Two Ways
We can count a combinatorial identity in two ways.

For example, consider
$$
\binom{n-1}{k-1} + \binom{n-1}{k} = \binom{n}{k}
$$
This describes the same count, but we can see it in 2 different ways!
- The right hand side describes the number of ways to create a $k$-size subset from $[n]$.
- The left hand side describes $k$-size subsets that do or do not contain element $n$. 
  - If we do contain $n$, then we choose $k - 1$ elements from the remaining $n - 1$ elements. $\binom{n-1}{k-1}$
  - If we do not contain $n$, then we choose $k$ elements from the remaining $n - 1$ elements. $\binom{n-1}{k}$
