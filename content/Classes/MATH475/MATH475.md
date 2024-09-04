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

> [!Example]- Example: Combinations
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

> [!Example]+ Example: Binomial Theorem Intuition, Extended
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
Many combinatorial identities can be interpreted in multiple ways. 

For example, consider
$$
\binom{n-1}{k-1} + \binom{n-1}{k} = \binom{n}{k}
$$
This describes the same count, but we can see it in 2 different ways!
- The right hand side describes the number of ways to create a $k$-size subset from $[n]$.
- The left hand side describes $k$-size subsets that do or do not contain element $n$. 
  - If we do contain $n$, then we choose $k - 1$ elements from the remaining $n - 1$ elements. $\binom{n-1}{k-1}$
  - If we do not contain $n$, then we choose $k$ elements from the remaining $n - 1$ elements. $\binom{n-1}{k}$

Another example:
$$
\sum_{k=0}^n k \binom{n}{k} = n 2^{n-1}
$$
This describes the total number of possible ways we can form a team with a leader among $n$ people.
- In the right hand side, we choose a leader from a group of $n$ people, and for the remaining people, they choose to "include" or "not include" them in the team. 
- In the left hand side, we choose a team of $k$ people from $n$ total ($0 \le k \le n$), and among those $k$ people, choose a leader.

Another example:
$$
\sum_{i=1}^n i (n - i + 1) = \binom{n+2}{3}
$$
- In the RHS, we describe all ways to create a 3-size subset from $[n + 2]$.
- In the LHS, let $\{a,b,c\} \in [n + 2]$. We assign all of the elements to $a$, $b$, or $c$, and find the number of ways we can create a 3-size subset, choosing 1 from each $\{a,b,c\}$. First, let the first $i$ elements be in $a$. Then, let the next element be in $b$, and let the remaining be in $c$. Choose 1 from each group $a,b,c$, and find the number of ways we can do this. Thus, for any iteration, we have $i$ choices for $a$, 1 choice for $b$, and $n + 2 - i - 1$ choices for $c$.

## 1.3: Pigeonhole Principle
In its simplest form, the **Pigeonhole Principle** states that if $n + 1$ pigeons into $n$ pigeonholes, there exists at least 1 pigeonhole with at least 2 pigeons. This is because you can fill in $n$ holes with 1 pigeon each, and are left with one extra pigeon that must go with one of the already filled holes.

More generally, if we have $n$ pigeons and $k$ pigeonholes, there exists a pigeonhole with at least $\lceil \frac{n}{k} \rceil$ pigeons (or, more than $\lfloor \frac{n-1}{k} \rfloor$ pigeons).

> [!Example]+ Example: Pigeonhole Principle
> Prove that in a group of 40 poeple, at least 4 people have a birthday in the same month.
>
> Here, let pigeons be people, and pigeonholes be months. We have 12 pigeonholes, and 40 pigeons.
> 
> By the pigeonhole principle, there exists at least 1 month with at least $\lceil \frac{40}{12} \rceil = 4$ people.

> [!Example]- Example: Pigeonhole Principle (2)
> Prove that if 6 distinct numbers are chosen from $[9] = \{1,2,3,4,5,6,7,8,9\}$, then two of the numbers will sum to 10.
>
> Here, let pigeonholes be pairs of numbers summing to 10: $\{1,9\}, \{2,8\}, \{3,7\}, \{4,6\}, \{5\}$, and let pigeons be our "choice" of number in our 6-number set.
>
> By the pigeonhole principle, there exists at least 1 pair with at least $\lceil \frac{6}{5} \rceil = 2$ choices, i.e. both numbers in the pair are selected. Note that we cannot have chosen $\{5\}$ twice, as the numbers are distinct.

> [!Example]- Example: Pigeonhole Principle (3)
> An athlete works out in blocks of hours. He plans to work out a total of 45 hours in a 30-day month. Assume he works out at least 1 hour each day. Prove that there is a period of consecutive days (2 or more) where the cumulative hours he has worked out is a total of exactly 14 hours.
>
> Let $a_i$ be the accumulated hours up to the day $i$. This gives us the sequence $a_1, a_2, \dots a_{30} = 45$. Because we are doing at least 1 hour a day, this is a strictly increasing sequence- each number is distinct.
>
> Consider the sequence $b_1 = a_1 + 14, b_2 = a_2 + 14, \dots b_{30} = a_{30} + 14$. Note that the $b_i$'s are distinct by our earlier assumption. We know that because $a_{30} = 45$, $b_{30} = 45 + 14 = 59$.
>
> We find that our sequences $\{a_i\}, \{b_i\}$ take on at most 59 different values, but there are 60 total values, with $a_i$'s and $b_i$'s distinct! Thus, letting the $a_i$'s and $b_i$'s be pigeons, 1 - 60 be pigeonholes, by the pigeonhole principle, there must exist some value where the sequences overlap- $a_j = b_k = a_k + 14$.
>
> So, $a_j - a_k = 14$- in other ways, from day $k$ to $j$, the athlete worked out exactly 14 hours.

## 1.4: Compositions and Set Partitions
### Compositions
Let $a_1, \dots a_k$ be non-negative integers such that
$$
\sum_{i=1}^k a_i = n
$$

Then the ordered $k$-tuple $(a_1, \dots a_k)$ is a **weak composition** of $n$ into $k$ parts.
> This can be seen as a way to give $n$ dollars to $k$ people, where some people may get none! 

How many weak compositions of $n$ into $k$ are possible? 

> [!Abstract] Theorem: Stars and Bars
> There are 
> $$
> \binom{n + k - 1}{k - 1}
> $$
> Possible weak compositions of $n$ into $k$.
>
> > [!Note]- Proof
> >
> > Consider $n$ stars, and $k$ bars. We define a model where all stars to the right of the first bar (before the second bar) is the value of $a_1$, all stars to the right of the second (before the third) is the value of $a_2$, and so on and so forth for $a_3, \dots a_k$.
> > $$
> > | \star \star \star | \star | \star \star \dots
> > $$
> >
> > Observe that the first object must be a bar. This leaves $n + k - 1$ objects that are not used. However we choose to place the remaining $k - 1$ bars gives us a unique weak composition of $n$ into $k$ parts! So, we have
> > $$
> > \binom{n + k - 1}{k - 1}
> > $$
> > Possible compositions.

> [!Example]+ Example: Stars and Bars
> How many non-negative integer solutions are there to $x_1 + x_2 + x_3 = 12$?
> 
> By the theorem, we have
> $$
> \binom{12 + 3 - 1}{3 - 1} = \binom{14}{2}
> $$

> [!Example]- Example: Stars and Bars (2)
> There are 5 cokes, 7 sprites, and 6 Dr. Peppers. How many ways can we choose 4 sodas?
> 
> We can see this as $x_1$ being cokes, $x_2$ being sprites, $x_3$ being Dr. Peppers, and rephrase the problem as 
> $$
> x_1 + x_2 + x_3 = 4
> $$
> Finding the total number of non-negative integer solutions.
> $$
> \binom{4 + 3 - 1}{3 - 1}
> $$

What if a weak composition $(a_1, a_2, \dots a_k)$ requires $a_1, a_2, \dots a_k \ge 1$? Well, we can simply give each $a_1, \dots a_k$ 1, and then perform a weak composition on the $n - k$ remaining! This way, it doesn't matter if the weak composition yields that someone got nothing, as they already have at least 1. We formalize this below.

The total $k$-tuples $(a_1, \dots a_k)$ satisfying $\sum_{i=1}^k a_i = n$, where each $a_i$ is a **positive** integer ($a_i \ge 1$) is
$$
\binom{n - k + k - 1}{k - 1} = \binom{n - 1}{k - 1}
$$
Called a **composition** of $n$ into $k$ parts.

### Partition
Let $X$ be a finite set, and $A_1, A_2, \dots A_k$ be **non-empty** subsets of $X$. A **partition** of $X$ $\{A_1, \dots A_k\}$ satisfies the following:
1. $$
   \bigcup_{i=1}^k A_i = x
   $$
   Their union makes up $X$
   
2. $$
   A_i \cap A_j = \varnothing \quad \forall 1 \le i \ne j \le k
   $$
   The subsets are disjoint.

For a given $k$, we say $X$ is partitioned into **$k$ blocks**.

> [!Example]+ Example: Partitions
> Let $X = [3]$.
> 
> We have 5 possible partitions:
> $$
> \begin{align*}
>     \{1,2,3\} \\
>     \{1,2\}, \{3\} \\
>     \{1,3\}, \{2\} \\
>     \{2,3\}, \{1\} \\
>     \{1\}, \{2\}, \{3\}
> \end{align*}
> $$
> Above, you can see that there are 3 cases of "2 blocks".

A **Stirling number of the second kind**, denoted $S(n,k)$ is the total number of partitions of $[n]$ into exactly $k$ blocks. By convention, $S(0,0) = 1$.
> There's no easy formula for all $S(n,k)$! However, we have some formulas for subsets of the stirling numbers.

> [!Example]+ Example: Stirling Numbers
> What is $S(n, 2)$?
> 
> For $n$, assign each number to 1 of 2 teams: $2^n$. Subtract the cases where all are only in 1 team: $2$.
> 
> Finally, divide by 2 because sets have no ordering.
> $$
> \frac{2^n - 2}{2} = 2^{n-1} - 1
> $$
