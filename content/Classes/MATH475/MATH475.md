---
title: MATH475
tags:
- math475
---

Combinatorics and graph theory

---

# Section 1: Counting and Enumeration
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

### Partitions
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

> [!Abstract] Theorem: Stirling Numbers (Recurrence Relation)
> For all non-negative integers $n \ge k$, 
> $$
> S(n,k) = S(n - 1, k - 1) + k S(n - 1, k)
> $$
> 
> > [!Note]- Proof
> >
> > The LHS is the total number of partitions of $[n]$ into exactly $k$ blocks.
> > 
> > In the RHS, we consider partitions of $n$ where element "n" is a singleton block or not. If it is a singleton block, then we find the remaining $k - 1$ blocks from the $n - 1$ remaining. If it is not a singleton block, then we can create $k$ blocks from $n - 1$, and then put $n$ in any of the $k$ blocks ($k$ choices).

> [!Abstract] Theorem: Stirling Numbers (Summation)
> We have
> $$
> S(n,k) = \frac{1}{k!} \sum_{i=0}^k (-1)^i \binom{k}{i} (k - i)^n
> $$
> > The proof will be covered later!

What if we didn't want to be limited by $k$ blocks? 

The total number of partitions of $[n]$ into any \# of blocks is the **Bell number**, denoted $B(n)$. By convention, $B(0) = 1$.

> [!Example]+ Example: Bell Numbers
> From an earlier example, let $X = [3]$.
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
> So, $B(3) = 5$.

> [!Abstract] Theorem: Bell Numbers (Summation)
> We have 
> $$
> B(n) = \sum_{i=1}^n \binom{n-1}{i-1} B(n-i)
> $$
>
> > [!Note]- Proof 
> > 
> > The LHS describes all ways to partition $[n]$. 
> > 
> > In the RHS, we look at partitions depending on some element "n", lying in a subset of size $i$. 
> > 
> > First, create one subset of size $1 + (i - 1)$ (1 element is always taken out before the choosing, hence the -1). Then, of the remaining $n - i$ elements, we find the number of ways to partition it.

> [!Example]+ Example: Partitions
> Let $f : A \to B, |A| = n, |B| = k$. 
> 
> Recall that $f$ is surjective / onto if for every $b \in B$, there exists an $a \in A$ such that $f(a) = b$. 
> 
> How many surjective functions are there?
>
> Here, we want to partition our domain values into $k$ blocks, where each block will be associated with one output. We multiply by $k!$, the total number of ways to associate one combination of blocks with the outputs.

## 1.5: Integer Partitions
A **partition of integer $n$** is a positive sequence of integers $a_1, a_2, \dots a_k$, where $a_1 \ge a_2 \ge \dots \ge a_k$, such that
$$
a_1 + a_2 + \dots + a_k = n
$$
> So, $1 + 3$ is the same as $3 + 1$. What matters is not what's inside of the blocks, but the sizes of the blocks relative to one another!

We denote the total number of partitions of $n$ by $p(n)$. By convention, $p(0) = 1$.
> The formula for this is extremely complex!

> [!Example]+ Example: $n = 4$ Case
> We find that
> $$
> 3 + 1 = 2 + 2 = 2 + 1 = 1 + 1 + 1 + 1 = 4
> $$
> There are 5 total partitions of 4! $p(4) = 5$.

A **Ferrers diagram (or Young Diagram)** of an integer partition is a partial rectangular grid whose $i^{th}$ row contains $a_i$ dots (rectangles).

These diagrams can illustrate some very interesting relationships! One diagram representing $4 + 3 + 1 + 1 + 1$ is given below.
$$
\begin{matrix}
    \star & \star & \star & \star \\
    \star & \star & \star \\
    \star \\
    \star \\ 
    \star
\end{matrix}
$$

Interestingly, the **conjugate** of a partition on a diagram is a new grid whose $i^{th}$ column is now $a_i$. Here, the conjugate would yield 
$$
\begin{matrix}
    \star & \star & \star & \star & \star \\
    \star & \star \\
    \star & \star \\
    \star \\ 
\end{matrix}
$$
> Basically, we flip the entire thing along a diagonal!

We can use this to establish some interesting identities!

> [!Abstract] Theorem: Integer Partitions Identity
> The total number of integer partitions of $n$ such that $a_1 = a_2 \ge a_3 \ge \dots$ equals the total number satisfying
> $$
> a_1 \ge a_2 \ge \dots \ge 2
> $$
> > Each partition has a size of at least 2!
> 
> > [!Note]- Proof
> > 
> > Consider a partition such that $a_1 = a_2$. 
> > 
> > If we were to draw a Ferrers diagram, we would find that the conjugate of the diagram corresponds to a diagram whose first two columns are always the same length, telling us that there are at least two dots in each row.
> > $$
> > \begin{matrix}
> >     \star & \star & \star & \star & \star & a_1 \\
> >     \star & \star & \star & \star & \star & a_2 \\
> >     \star & \star & \star \\
> >     \star
> > \end{matrix} 
> > \Longrightarrow
> > \begin{matrix}
> >     \star & \star & \star & \star \\
> >     \star & \star & \star \\
> >     \star & \star & \star \\
> >     \star & \star \\
> >     \star & \star \\
> >     a_1 & a_2
> > \end{matrix} 
> > $$
> > 
> > Thus, each $a_i$ must take on at least 2.
> 
> The converse also holds, with a similar proof. 

The **total partitions of $n$ into exactly $k$ parts** is denoted $P_k (n)$.
> Note that the previous definition did not establish this $k$ part requirement.

> [!Abstract] Theorem: Integer Partitions into Exactly $k$ Parts
> For $1 < k < n$,
> $$
> P_k(n) = P_{k-1}(n-1) + P_k (n-k)
> $$
>
> > [!Note]- Proof
> > 
> > The LHS describes the ways to partition $n$ into exactly $k$ parts.
> >
> > The RHS considers partitions into $k$ parts for either $a_k = 1$ or $a_k > 1$. If $a_k = 1$, we take one and partition the remaining $n - 1$ into $k - 1$ parts for a total of $k$. If $a_k > 1$, we first give 1 to all parts, then partition the remaining into $k$ parts to guarantee that all numbers have at least 2.

## 1.6: The Twelvefold Way
We throw $n$ balls into $k$ bins. We consider the cases of the balls and bins being labeled (distinguishable) or not, and if each bin has no restriction, each bin has at least 1 ball, or each bin has at most 1 ball.

This forms 12 cases total, which can be solved with the methods described previously.
1. Labeled balls to labeled bins
   1. No restriction: For every ball, we can put it in $k$ possible bins. 
   $$
   k^n
   $$
   2. At least 1 ball: We find the number of ways to partition $n$ into $k$, and then permute what bin each group goes into. 
   $$
   k! S(n,k)
   $$
   3. At most 1 ball (obvioulsly, $k \le n$): Choose $n$ of the $k$ bins to place the balls into. Then, permute the ordering of how we place the balls. 
   $$
   \binom{k}{n} n!
   $$
2. Unlabeled balls to labeled bins
   1. No restriction: Perform weak composition to decompose $n$ into $k$ (labeled) parts. 
   $$
   \binom{n+k-1}{k-1}
   $$
   2. At least 1 ball: First give each bin 1 dollar, then perform weak composition on the remaining $n - k$ parts. 
   $$
   \binom{n-1}{k-1}
   $$
   3. At most 1 ball: Choose $n$ bins of the $k$ to place a ball into. 
   $$
   \binom{k}{n}
   $$
3. Labeled balls to unlabeled bins.
   1. No restriction: We partition the set of balls $[n]$ into $i$, from $1 \le i \le k$. We do a sum instead of Bell numbers, as bell numbers will overcount (we cannot count higher than $k$).
   $$
   \sum_{i=1}^k S(n,i)
   $$
   2. At least 1 ball: We partition the set of balls $[n]$ into $k$ parts. 
   $$
   S(n,k)
   $$
   3. At most 1 ball: Just one way, as the bins are labeled!
   $$
   1
   $$
4. Unlabeled balls to unlabeled bins.
   1. No restriction: Some bins can be empty, so this is integer partitions into 1 bin, then 2 bins, and so forth until $k$ bins. Simple integer partitions assume the integers (bins) can never be empty, which is not true here. 
   $$
   P_1 (n) + P_2 (n) + \dots + P_k(n)
   $$
   2. At least 1 ball: Each bin must have at least 1 ball, so this is integer partitions into $k$ parts. 
   $$
   P_k (n)
   $$
   3. At most 1 ball: If $n \le k$, since nothing is labeled, we'll just have $k$ bins filled with 1 ball. So, there is only 1 way.
   $$
   1
   $$

> [!Example]- Examples: The Twelvefold Way
> 1. A **multiset** is a set such that elements can be repeated. How many multisets of size 5 can be created using $[7] = \{1,2, \dots, 7\}$?
> 
>    We can convert this into one of the 12 ways. Consider 5 unlabeled balls to 7 labeled bins. Each ball is used as a counter to how many times the element occurs in the multiset. 
>    $$
>    \binom{5 + 7 - 1}{7 - 1}
>    $$
> 
> 2. Twenty students split into exactly 4 study groups to prepare for an exam (groups with 1 person are fine). However, brothers Bobs and Carl must be in the same group. Also, sisters Alice and Diane want to be in the same group. What are the possible number of groups?
> 
>     First, as Bob / Carl, Alice / Diane must always be together, let's group them into 1 entity each. So, we have 18 labeled balls into 4 unlabeled boxes, where each box must have at least 1 ball. 
>     $$
>     S(18,4)
>     $$
> 3. How many injective / one-to-one functions are there for $f: [n] \to [k]$?
> 
>    For each element in our range, we know that there is at most 1 value in our domain mapping to it. This is the same as $n$ labeled bins, $k$ labeled balls, where each bin can only have at most 1 ball.
>    $$
>    (k)_n = k (k - 1) \dots (k - n + 1)
>    $$
> 
> 4. Let $n \ge k$. A function $f : [n] \to [k]$ is **monotone** if $f(x) \ge f(y)$ whenever $x > y$. How many monotonic functions $f : [n] \to [k]$ are there?
> 
>    Let us have $k$ labeled bins for the output, and $n$ unlabeled balls for the domain values. Note that these can be unlabeled, as the monotone constraint forces an order (the $i$ balls in bin 1 must correspond to the first $i$ values in the domain, and so forth). This is weak compositions! Thus, we have
>    $$
>    \binom{n + k - 1}{k - 1}
>    $$

## 1.7: Inclusion-Exclusion Principle
> [!Abstract] Theorem
> Let $A_1, \dots A_n \subseteq X$, where $X$ is finite. Assume that the $A_i$'s are non-empty.
>
> Let $I \subseteq [n]$, and denote $A_I = \bigcap_{i \in I} A_i$. Define $A_\varnothing = X$.
> 
> Then,
> $$
> \left| \bigcup_{i=1}^n A_i \right| = |X| - \sum_{I \subseteq [n]} (-1)^{|I|} |A_I|
> $$
> In other words, the union of all sets is the set minus the intersection of all subset combinations.
> 
> Applying Demorgan's Law on this, we obtain 
> $$
> \left| \bigcap_{i=1}^n \bar{A}_i \right| = \sum_{I \subseteq [n]} (-1)^{|I|} |A_I|
> $$
> Where $\bar{A}_i$ is the complement of $A_i$.

Basically, sometimes when we want to find something, we can find it by considering its complements (which can be easer to solve)!

> [!Example] Example: $n = 2$ Case
> In the $n = 2$ case, we have
> $$
> \begin{align*}
> \left| \bigcup_{i=1}^2 A_i \right| 
> &= | A_1 \cup A_2 | \\
> &= |X| - \left( (-1)^0 |A_\varnothing| + (-1)^1 |A_{\{1\}}| + (-1)^1 |A_{\{2\}}| + (-1)^2 |A_{\{1,2\}}| \right) \\
> &= |X| - \left( |X| - |A_1| - |A_2| + |A_1 \cap A_2| \right) \\
> &= |A_1| + |A_2| - |A_1 \cap A_2|
> \end{align*}
> $$
> This is commonly used everywhere in probability theory!

This principle is very useful in simplifying problems that may be quite complex, into simpler sub-problems that can be combined to yield our solution.

> [!Example] Example: Inclusion-Exclusion Principle
> How many non-negative integer solutions are there to $x_1 + x_2 + x_3 = 35$, where
> $$
> 0 \le x_1 \le 15, 0 \le x_2 \le 15, 0 \le x_3 \le 15
> $$
> Here, we have a max on our integers, which is really difficult to solve! However, it may be easier to solve using the inclusion-exclusion principle.
> 
> Here, we could perform weak compositions when $x_1, x_2, x_3 \ge 0$, but we also have upper bounds.
> 
> Let
> $$
> \begin{align*}
> A_1 = \{ \text{Weak Compositions of } x_1 + x_2 + x_3 = 35, x_1 \ge 16 \} \\
> A_2 = \{ \text{Weak Compositions of } x_1 + x_2 + x_3 = 35, x_2 \ge 16 \} \\
> A_3 = \{ \text{Weak Compositions of } x_1 + x_2 + x_3 = 35, x_3 \ge 16 \} \\
> \end{align*}
> $$
> Note that $A_\varnothing$, is all weak compositions.
> 
> We want 
> $$
> \begin{align*}
> |\bar{A}_1 \cap \bar{A}_2 \cap \bar{A}| &= \sum_{I \subseteq [3]} (-1)^{|I|} |A_I| \\
> &= |A_\varnothing| + (-1)^1 (|A_1| + |A_2| + |A_3|) \\
> &\qquad + (-1)^2 (|A_1 \cap A_2| + |A_2 \cap A_3| + |A_1 \cap A_3|) + (-1)^3 |A_1 \cap A_2 \cap A_3| \\
> &= \binom{35 + 3 - 1}{3 - 1} + 3 * (-1)^1 \binom{19 + 3 - 1}{3 - 1} + 3 * (-1)^2 \binom{3 + 3 - 1}{3 - 1} + (-1)^3 0
> \end{align*}
> $$

> [!Example]- Example: Inclusion-Exclusion (2)
> Use inclusion-exclusion to count the total surjective functions $f : [n] \to [k]$. In other words, each $b \in [k]$ has at least 1 $a \in [n]$ such that $f(a) = b$.
> 
> Define
> $$
> \begin{align*}
> A_1 = \{ \text{Functions s.t } f(j) \ne 1, j \in [n] \\
> A_2 = \{ \text{Functions s.t } f(j) \ne 2, j \in [n] \\
> \vdots
> A_i = \{ \text{Functions s.t } f(j) \ne i, j \in [n] \\
> \end{align*}
> $$
> 
> So, the number of surjective functions can be found as
> $$
> \begin{align*}
> | \bigcap_{i=1}^k \bar{A}_i | &= \sum_{I \subseteq [k]} (-1)^{|I|} |A_I| \\
> &= \sum (-1)^i \binom{k}{i} (k - i)^n 
> \end{align*}
> $$
> Note that the first term describes the number of indices we DON'T want to map to. If we do not map to $i$ indices, then there are $k - i$ indices that we need to map to, and for each value in our domain it can map to any one of these indices (hence the $(k - i)^n$.
> $$
> = k! S(n,k) \Longrightarrow S(n,k) = \frac{1}{k!} \sum_{i=1}^k (-1)^k \binom{k}{i} (k - i)^n
> $$
> Which is a formula for Stirling numbers we found from earlier!

> [!Example]- Example: Inclusion-Exclusion (3)
> The Euler totient function is given as
> $$
> \phi(n)= | \{ i \in \mathbb{Z}^+ : \text{GCD}(i,n) = 1, 1 \le i \le n \} | 
> $$
> Which is equivalent to the total number of values in $[n]$ that are relatively prime to $n$ (meaning they have no common divisors besides 1).
> 
> Let the prime factorization of $n$ be $n = p_1^{e_1} p_2^{e_2} \dots p_t^{e_t}, e_i \ge 1$. Let
> $$
> A_i  = \{ a \in [n] : p_i \text{ divides } a \}
> $$
> So, for example, if we have $p = 7$, $n = 70$, $|A_1|$ would be the number of numbers where 7 divides $a$, $1 \le a \le 70$. In other words, the number of multiples of 7!
> 
> So, 
> $$
> \begin{align*}
> \phi(n) = | \bigcap_{i=1}^t \bar{A}_i | 
> &= \sum_{I \subseteq [t]} (-1)^{|I|} |A_I| \\ 
> &= n - \left( \frac{n}{p_1} + \frac{n}{p_2} + \dots + \frac{n}{p_t} \right) + \left( \frac{n}{p_1 p_2} + \dots + \frac{n}{p_1 p_3} + \dots \right) \\
> &\qquad + \left( \frac{n}{p_1 p_2 p_3} + \frac{n}{p_1 p_2 p_4} + \dots \right) \\
> &= n \left[ 1 - \sum_{i=1}^t \frac{1}{p_i} + \sum_{1 \le i < j \le t} \frac{1}{p_i p_j} - \sum_{1 \le i < j < k \le t} \frac{1}{p_i p_j p_k} + \dots \right] \\
> &= n \prod_{i=1}^t \left( 1 - \frac{1}{p_i} \right)
> \end{align*}
> $$
> Between the last two steps, we find that this is equal to the ugly summations, as we're basically choosing $p_i$'s to find all possible combinations!

> [!Example] Example: Inclusion-Exclusion (4)
> Twenty couples attend counseling. They sit at a circular, unlabeled table (exactly 40 chairs).
>
> How many seatings assure no one sits next to their significant other?
>
> Let $A_i$ denote the set where couple $1 \le i \le 20$ sits next to each other. We want
> $$
> \begin{align*}
> \left| \bigcap_{i=1}^{20} \bar{A}_i \right| 
> &= \sum_{I \subseteq [20]} (-1)^{|I|} |A_I| \\
> &= \sum_{i=0}^{20} \binom{20}{i} (-1)^i \frac{(40 - i)!}{40 - i}
> \end{align*}
> $$
> 
> Note that what we are doing per term is selecting $i$ couples, then finding the number of orderings of our "40" people given that the $i$ couples are tied together ($40 - i$, because for each tied couple they're 1 entity). Furthermore, we need to multiply by $2^i$, as each couple pair could be swapped in order. Finaly, we divide by the number of rotations.
> > Note that we start at $i = 0$ to include the empty set.


# Section 2
## 2.1, 2.2: Power Series Review, Intro to Ordinary Generating Functions
A **formal power series** is an infinite sum 
$$
\sum_{n=0}^\infty a_n x^n
$$
whose coefficients represent a sequence $\{a_n\}$.

The function $F(x) = \sum_{n=0}^\infty a_n x^n$ is the **ordinary generating function** of $\{a_n\}_{n=0}^\infty$, sometimes denoted the OGF.
> These functions are quite interesting! Oftentimes, we can manipulate these functions into something else that we can recognize.

> [!Example]+ Example: Ordinary Generating Functions of Sequences
> Let $\{a_n\}$ be given by
> $$
> \frac{1}{2!}, \frac{1}{3!}, \frac{1}{4!}, \dots
> $$
> 
> What is $F(x)$?
> 
> We can find $F(x)$ as
> $$
> \begin{align*}
> F(x) &= \frac{1}{2!} + \frac{1}{3!} x + \frac{1}{4!} x^2 + \dots \\
> &= \frac{1}{x^2} \left( \frac{1}{2!} x^2 + \frac{1}{3!} x^3 + \dots \right) \\
> &= \frac{1}{x^2} (e^x - x - 1)
> \end{align*}
> $$

> [!Example]+ Example: Sequences of Ordinary Generating Functions
> Find $\{a_n\}$ if the OGF is
> $$
> F(x) = \frac{-4x + 3}{(1 - x)(1 - 2x)}
> $$
> 
> Note that our denominator looks like the output of a geometric series, but as a product! So, we apply partial fractions to get separate geometric series.
> 
> $$
> \begin{align*}
> \frac{-4x + 3}{(1 - x)(1 - 2x)} 
> &= \frac{A}{(1 - x)} + \frac{B}{(1 - 2x)} \\ 
> -4x + 3 
> &= A (1 - 2x) + B(1 - x) \\
> A = 1&, B = 2
> \end{align*}
> $$
> 
> So, we get
> $$
> \begin{align*}
> F(x) 
> &= \frac{-4x + 3}{(1 - x)(1 - 2x)} = \frac{1}{1 - x} + \frac{2}{1 - 2x} \\
> &= \sum_{n=0}^\infty x^n + 2 \sum_{n=0}^\infty (2x)^n \\
> &= \sum{n=0}^\infty (1 + 2^{n + 1}) x^n
> \end{align*}
> $$
> So we find our sequence to be
> $$
> \{a_n\} = \{1 + 2^{n+1}\}
> $$

Given a **recurrence**, say $a_n = a_{n-1} + a_{n-2}$ (the fibonacci recurrence) where we are given a term in terms of the previous ones, we can obtain the closed form OGF, and then use a series expansion to get an explicit closed form formula for our sequence $\{a_n\}$. 

> [!Info] Lemma
> We have
> $$
> h(x) = 1 - x - x^2 = - \left( x + \frac{1 + \sqrt{5}}{2} \right) \left( x + \frac{1 - \sqrt{5}}{2} \right)
> $$
> Moreover, if $r_1 = \frac{1 + \sqrt{5}}{2}$, $r_2 = \frac{1 - \sqrt{5}}{2}$, then $r_2 = -\frac{1}{r_1}$.

> [!Example] Example: Closed Form Fibonacci Sequence
> $$
> a_n = a_{n-1} + a_{n-2} \qquad a_0 = 0, a_1 = 1
> $$
> 
> Find a closed form ogf for the sequence, and find a closed form for $a_n$ with it.
> 
> Our goal is first to find the closed form OGF.
> 
> We first start with the ogf, and then apply our sequence definition to the $a_n$ term. Note that we need to take out the base case as the definition for $a_n$ is only defined for $n \ge 2$.
> $$
> \begin{align*}
> F(x) 
> &= \sum_{n=0}^\infty a_n x^n = 0 + 1x + \sum_{n=2}^\infty a_n x^n \\
> &= x + \sum_{n=2}^\infty (a_{n-1} + a_{n-2}) x^n \\
> &= x + \sum_{n=2}^\infty a_{n-1} x^n + \sum_{n=2}^\infty a_{n-2} x^n \\
> &= x + x \sum_{n=2}^\infty a_{n-1} x^{n-1} + x^2 \sum_{n=2}^\infty a_{n-2} x^{n-2}
> \end{align*}
> $$
> We can use this to express $F(x)$ as a function of itself. Note that the first summation is $F(x)$ without the $a_0$ term, and the second summation is just $F(x)$.
> $$
> \begin{align*}
> F(x)
> &= x + x \sum_{n=2}^\infty a_{n-1} x^{n-1} + x^2 \sum_{n=2}^\infty a_{n-2} x^{n-2} \\
> &= x + x (F(x) - a_0) + x^2 F(x) \\
> &= x + x F(x) + x^2 F(x) \\
> F(x)
> &= \frac{x}{1 - x - x^2}
> \end{align*}
> $$
> We have found a closed form ogf. We can now use this to find our closed form sequence. We do this by applying partial fraction decomposition and converting the result into a geometric series.
> > Here, we apply our lemma.
> $$
> \begin{align*}
> F(x)
> &= \frac{x}{1 - x - x^2} \\
> &= \frac{-x}{\left( x + \frac{1 + \sqrt{5}}{2} \right) \left( x + \frac{1 - \sqrt{5}}{2} \right)} \\
> &= \frac{-x}{(x + r_1) (x + r_2)} = \frac{A}{x + r_1} + \frac{B}{x + r_2} \\
> &= \frac{-1}{\sqrt{5}} \left( \frac{r_1}{x + r_1} - \frac{r_2}{x + r_2} \right) \\
> &= \frac{1}{\sqrt{5}} \left( \frac{r_2}{x + r_2} - \frac{r_1}{x + r_1} \right) \\
> &= \frac{1}{\sqrt{5}} \left( \frac{1}{1 - (-x / r_2)} - \frac{1}{1 - (-x / r_1)} \right) \\ 
> &= \frac{1}{\sqrt{5}} \left( \sum_{n=0}^\infty (r_2 x)^n - \sum_{n=0}^\infty (r_1 x)^n \right) \\
> &= \sum_{n=0}^\infty \frac{1}{\sqrt{5}} (r_2^n - r_1^n) x^n 
> \end{align*}
> $$
> We've found our closed form sequence!
> $$
> \{a_n\} = \frac{1}{\sqrt{5}} (r_2^n - r_1^n) =  \frac{1}{\sqrt{5}} \left( \left( \frac{1 - \sqrt{5}}{2} \right)^n - \left(  \frac{1 + \sqrt{5}}{2} \right)^n \right)
> $$

> [!Example]
> Consider codes of length $n$ using $A,B,C,D$. Let $a_n$ denote the total codes with an even number of $A$'s. 
> 1. Find a recurence of $a_n$ in terms of $a_{n-1}$
> 2. Find a closed form ogf.
> 3. Find a closed form for $a_n$.
> 
> We first find a recurrence. If we have $n - 1$ length strings, we could add a $B,C,D$ to get a $n$ length string. Or, with $n - 1$ length strings, we need an odd number of $A$'s to add an extra $A$ onto, which we can find as all strings minus the even ones.
> $$
> a_n = a_{n-1} + a_{n-1} + a_{n-1} + (4^{n-1} - a_{n-1}) = 2a_{n-1} + 4^{n-1}
> $$
> We now need to find our base case. Clearly, $a_1 = 3$, as the string can only be a $B,C,D$. So, $a_0 = 1$.
> 
> We now use our recurrence to find a closed form ogf.
> $$
> \begin{align*}
> F(x) 
> &= \sum_{n=0}^\infty a_n x^n = 1 + \sum_{n=1}^\infty a_n x^n \\
> &= 1 + \sum_{n=0}^\infty (2a_{n-1} + 4^{n-1}) x^n \\
> &= 1 + 2 \sum_{n=1}^\infty a_{n-1} x^n + \sum_{n=1}^\infty 4^{n-1} x^n \\
> &= 1 + 2 x \sum_{n=1}^\infty a_{n-1} x^{n-1} + x \sum_{n=1}^\infty 4^{n-1} x^{n-1} \\
> &= 1 + 2 x \sum_{n=1}^\infty a_{n-1} x^{n-1} + x \sum_{n=1}^\infty 4^{n-1} x^{n-1} \\
> &= 1 + 2x F(x) + x \frac{1}{1 - 4x} \\
> F(x) 
> &= \frac{1}{1 - 2x} \left(1 + \frac{x}{1 - 4x} \right) \\
> &= \frac{1}{1 - 2x} + \frac{x}{(1 - 4x) (1 - 2x)}
> \end{align*}
> $$
> 
> We now use our closed form ogf to find a closed form sequence.
> $$
> \begin{align*}
> F(x) 
> &= \frac{1}{1 - 2x} + \frac{x}{(1 - 4x) (1 - 2x)} \\
> &= \frac{1}{2(1 - 2x)} + \frac{1}{2(1 - 4x)} \\
> &= \frac{1}{2} \sum_{n=0}^\infty (2x)^n + \frac{1}{2} \sum_{n=0}^\infty (4x)^n \\
> &= \sum_{n=0}^\infty \frac{1}{2} (2^n + 4^n) x^n
> \end{align*}
> $$
> We found our closed form solution as
> $$
> \{a_n\} = \left\{ \frac{1}{2} (2^n + 4^n) \right\}
> $$

What if $a_n$ is a combinatorial value, like $S(n,k)$? Well, using our techniques, we can actually find the closed form solution of $S(n,k)$ (at least in some cases)!


--- End of Exam 1 Content ---

