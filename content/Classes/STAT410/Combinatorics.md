---
title: Combinatorics
tags:
- stat410
---

**Combinatorics** is an area of mathematics primarily concerned with counting, as well as properties of finite structures (such as graphs).

For the purposes of STAT410, we will only be addressing simple counting in combinatorics, for use in probability functions later.

# Permutations and Combinations
A **permutation** of a set of $n$ elements is a rearrangement of the elements in a specific order. A **k-permutation** is an arrangement of $k$ elements from the $n$-element set.
> By definition of a set, elements must be distinct.

The total number of $k$-permutations of an $n$-element set is given by the formula
$$
P(n,k) = \frac{n!}{(n-k)!} = n (n-1) \dots (n - k + 1)
$$

> [!Example]+ Example: Basic Permutations
> **Problem**: How many ways can we seat 10 people in a row?
> **Solution**: We are performing a $k$-permutation where $k = 10$ on our set of 10 people.
> $$
> P(10, 10) = 10!
> $$

The total ways to create a $k$-size subset from an $n$-element set, known as a **combination**, is given by 

$$
C(n,k) = \binom{n}{k} = \frac{n!}{k! (n-k)!} = \frac{P(n,k)}{k!}
$$
> Note that by definition of a subset, there is no element order.

> [!Abstract] Theorem: Binomial Theorem
> For any positive integer $n$,
> $$
> (x + y)^n = \sum_{k=0}^n \binom{n}{k} x^k y^{n-k}
> $$
> 
> > [!Note]- Proof
> > 
> > We begin with $(x + y)^n$.
> > $$
> > \begin{align*}
> > 	(x + y)^n &= (x + y) (x + y) \dots (x + y) \\
> > 	&= c_1 x^n + c_2 x^1 y^{n-1} + c_3 x^2 y^{n-2} + \dots 
> > \end{align*}
> > $$
> > 
> > The product of the $n$ terms means that when we expand the binomial expression, we are "choosing" either the $x$ or $y$ term to multiply.
> > 
> > Thus, to find the coefficient of $x^k y^{n-k}$, the product of the $n$ terms requires that when we multiply each binomial together, we multiply ("choose") the $x$-term $k$ times. After this, the rest of the product's terms are forced to be $y$ (and there's only one way to pick $y$). 
> > 
> > This gives us $C(n, k)$ different ways to obtain the coefficient.
> > $$
> > C(n,k) x^k y^{n-k} = \binom{n}{k} x^k y^{n-k}
> > $$

We give some more counting examples below.

> [!Example]+ Example: Basic Counting
> There are 10 cows, 9 pigs, 8 horses. The
> 1. Total ways to pick 5 animals at once:
>    
>    Because order does not matter, we are simply choosing 5 animals from our total of 27. 
>    $$
>    C(27, 5)
>    $$
>    
> 2. Total ways to get 5 animals where we get 3 cows, 2 pigs or 2 cows, 3 pigs:
>    
>    We choose 3 cows and 2 pigs from our animal total to obtain
>    $$
>    \binom{10}{3} \binom{9}{2}
>    $$
>    We choose 2 cows and 3 pigs from our animal total to obtain
>    $$
>    \binom{10}{2} \binom{9}{3}
>    $$
>
> Because these two groups of outcomes are distinct from one another, we add them together to find our total.
> $$
> \binom{10}{3} \binom{9}{2} + \binom{10}{2} \binom{9}{3}
> $$

> [!Example]+ Example: Basic Counting (2)
> There are 10 kids and 3 types of candy. How many ways can we distribute this candy such that exactly 3 children get type 1, 2 children get type 2, and 5 children get type 3?
> 
> We can think of our children as the distinct elements, and choose who gets what candy. So, we first select 3 children to get type 1, 2 children to get type 2, and 5 children to get type 3.
> $$
> \binom{10}{3} \binom{7}{2} \binom{5}{5}
> $$
> 
> We can think about this another way as well. Say we have 10 children numbered 1-10, and we assign each a candy type of 1, 2, or 3 (for the total we're looking for). We want to find the number of different ways we can order these candy types!
> 
> However, because there are repeated elements, we need to count some cases as one. We do this by dividing by the total number of possible cases that we want to count as one case. 
> $$
> \frac{P(10, 10)}{3! \cdot 2! \cdot 3!}
> $$
> In fact, this is called the **multinomial coefficient**, described below.

> [!Abstract] Theorem: Multinomial Coefficient (Permutations with Repetition)
> Suppose there are $k$ distinct objects, and object $i$ occurs $a_i$ times.
> 
> Assume $a_1 + a_2 + \dots + a_k = n$. 
> 
> Then, the total number of rearrangements of the $n$ objects is
> $$
> \frac{n!}{a_1! \cdot a_2! \cdots a_k!} = \binom{n}{a_1 a_2 \dots a_k}
> $$
> called the **multinomial coefficient**. 

We can use the multinomial coefficient to generalize our previous binomial theorem.

> [!Abstract] Theorem: Multinomial Theorem
> $$
> (x_1 + x_2 + \dots + x_k)^n = \sum_{a_1 + a_2 + \dots + a_k = n} \binom{n}{a_1 a_2 \dots a_k} x_1^{a_1} x_2^{a_2} \dots x_k^{a_k}
> $$

> [!Example]+ Example: Multinomial Coefficient
> Find the coefficient of $x_1^3 x_2 x_4^2$ in $(x_1 + x_2 + x_3 + x_4)^6$.
> 
> To find the coefficient, we need to find the number of times we obtain $x_1^3 x_2 x_4^2$ in the product.
> 
> In other words, if we select 6 positions, where each represents the $x_i$ term we "selected" to multiply out, then we want to choose 3 positions to have $x_1$, 1 position to have $x_2$, and 2 positions to have $x_4$. 
> 
> This comes out to be
> $$
> C(6, 3) * C(3, 1) * C(2,2) = \binom{6}{3 \quad 1 \quad 2}
> $$

> [!Example]+ Example: Permutations and Combinations
> How many arrangements of $AAABBCC$ are there?
> 
> Suppose we have 7 positions. We want to choose 3 to fill with $A$, 2 to fill with $B$, and 2 to fill with $C$. This comes out to be
> $$
> C(7,3) * C(4,2) * C(2,2)
> $$
> 
> --- 
> 
> What if the $B$'s must all be together, but none of the $C$'s can be together?
> 
> If the $B$'s must be together, we block them together as one term $X = BB$ to find arrangements of $AAAXCC$. Then, to find permutations where the $C$'s are not together, we first will find the number of arrangements of $AAAX$ (without the $C$'s').
> $$
> C(4,3)
> $$
>
> Then, between every term $AAAX$, we can place $C$'s suchthat they are not next to each other. This comes out to 5 positions, and we have 2 $C$'s to place to give us
> $$
> C(5,2)
> $$
> different ways to place our $C$'s. Thus, our final result is
> $$
> C(4,3) * C(5,2)
> $$
