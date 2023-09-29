---
title: Recurrence Relations
tags:
- cmsc351
- work-in-progress
---

In this section, we discuss a new method for analyzing algorithm complexity.

# Recurrence Relations
A **recurrence relation** is an equation defining the value of a function in terms of earlier values.
> Typically, we'll have one (or more) base cases as well.

> [!Example]+ Example: Recurrence Relations
> $$
> T(n) = T(n/2) + c \qquad T(1) = d
> $$
> Where $c,d$ are constants.
> 
> This is in fact the recurrence relation for binary search, as the time required to process a list of length $n$ equals the check of the list's center, plus the time required to process the subsequent list of length $n/2$.

Given these recurrence relations, we can solve for specific values of $T(n)$! We can do this by recursively plugging in $n_0$ into our recurrence relation, until we reach a base case.

> [!Example]+ Example: Solving for Specific Values
> Consider the previous recurrence relation.
>
> We can find various times given specific input sizes $n_0$. 
> $$
> \begin{align*}
>       &T(2) = T(2/2) + c = T(1) + c = c + d \\
>       &T(4) = T(2) + c = [T(1) + c] + c = d + 2c
> \end{align*}
> $$
> > Note that recurrence relations often will need ceilings or floors to ensure that our values remain as integers (otherwise things don't make sense).

## Technique 1: Digging Down
We can use these recurrence relations to determine $\Theta$ of a function!
1. Using the relation to expand itself, we can continuously expand it until we find some general pattern.
2. Then, we solve for when this pattern ends with regard to the base case.
3. Finally, we sub in this base case to find our final time complexity.

This technique is known as **digging down**.
> Note that this technique only works for simple relations which have an easily identifiable pattern.

> [!Example]+ Example: Digging Down
> Consider the previous recurrence relation.
>
> Notice that
> $$
> \begin{align*}
>       T(n) &= T(n/2) + c \\
>            &= [T(n/2^2) + c] + c = T(n/2^2) + 2c \\
>            &= T(n/2^3) + 3c \\
>            &\vdots \\
>            &= T(n/2^k) + k \cdot c
> \end{align*}
> $$
>
> Note that by our base case, we will stop this expansion when
> $$
> \frac{n}{2^k} = 1 \to k = \lg(n)
> $$
>
> Giving us a final value of
> $$
> T(n) = T(n / 2^k) + k \cdot c = T(1) + c \lg(n) = d + c \lg(n)
> $$
> This gives us a time complexity of $\Theta(\lg(n))$!

> [!Example]- Example: Digging Down (2)
> $$
> T(n) = 2 T(n/2) + 5n \qquad T(1) = 7
> $$
>
> We expand it to find the following pattern:
> $$
> \begin{align*}
>       T(n) &= 2 T(n/2) + 5n \\
>            &= 2 [2 T(n/2^2) + 5 (n/2) ] + 5n = 2^2 T(n/2^2) + 2 (5n) \\
>            &= 2^3 T(n/2^3) + 3 (5n) \\
>            &\vdots \\
>            &= 2^k T(n/2^k) + k (5n)
> \end{align*}
> $$
>
> We find this pattern stops when we have
> $$
> \frac{n}{2^k} = 1 \to k = \lg(n)
> $$
>
> Giving us final time complexity $\Theta(n\lg(n))$.
> $$
> T(n) = 2^{\lg(n)} T(1) + \lg(n) (5n) = n \cdot 7 + 5n \lg(n)
> $$

## Technique 2: Recurrence Trees
Another method of solving recurrence relations involves the use of a **recurrence tree**.

Consider the recurrence relation given by
$$
T(n) = 2T(n/2) + n \qquad T(1) = 3
$$

Say we want to find some value $T(n)$. We can do this by drawing a tree to represent our summation, where every level $i$ (and its leaves) represents the result of $T(n / 2^i)$. The combination of all the nodes in this tree will therefore sum to $T(n)$.

```mermaid
graph TD
      r[n] -.-> t1[n/2] & t2[n/2];

      t1 -.-> t3[n/4] & t4[n/4];
      t2 -.-> t5[n/4] & t6[n/4];
      
      t3 -.-> t7[n/8] & t8[n/8];
      t4 -.-> t9[n/8] & t10[n/8];
      t5 -.-> t11[n/8] & t12[n/8];
      t6 -.-> t13[n/8] & t14[n/8];
```

Note that every level represents the result of $T(n/2^i)$. Thus, we can find when our levels end by finding when
$$
n/2^i = 1 \to i = \lg(n)
$$

We can then sum up all our results to find our total time. We make a table to represent this for us.

| Level | Num Nodes | Time / Node | Level Total |
| - | - | - | - |
| $0$ | $1$ | $n$ | $n$ |
| $1$ | $2$ | $n/2$ | $n$ |
| $2$ | $4$ | $n/4$ | $n$ |
| $\vdots$ | | | |
| $\lg(n) - 1$ | $2^{\lg(n) - 1}$ | $n / 2^{\lg(n)-1}$ | $n$ |
| $\lg(n)$ | $2^{\lg(n)}$ | $7$ | $7 n$ |

Using this table, we find total sum as the sum of the level totals (rightmost column).
$$
T(n) = \sum_{i=0}^{\lg(n)-1} n + 7n = n \lg(n) + 7n
$$