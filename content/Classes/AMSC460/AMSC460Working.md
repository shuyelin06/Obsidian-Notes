---
title: AMSC460Working
tags:
- amsc460
- wip
---

(Solving systems of linear equations)

# Systems of Linear Equations
## Introduction
Consider a **system of $m$ equations on $n$ variables** $x_1, x_2, \dots x_n$
$$
\begin{align*}
        &a_{11} x_1 + a_{12} x_2 + \dots a_{1n}x_n = b_1 \\
        &a_{21} x_1 + a_{22} x_2 + \dots a_{2n}x_n = b_2 \\
        &\vdots \\
        &a_{m1} x_1 + a_{m2} x_2 + \dots a_{mn}x_n = b_m \\
\end{align*}
$$
Alternatively represented in a more compact, matrix form $Ax = b, A \in \mathbb{R}^{m \times n}$ such that
$$
[A]_{ij} = a_{ij}
\qquad
x = \begin{bmatrix}
    x_1 \\ x_2 \\ \vdots \\ x_n
  \end{bmatrix} \in \mathbb{R}^n
\qquad
b = \begin{bmatrix}
    b_1 \\ b_2 \\ \vdots \\ b_n
  \end{bmatrix} \in \mathbb{R}^n
$$

> [!Abstract] Theorem: Existence and Uniqueness of Solutions
> Consider the **augmented matrix** $[A|b] \in \mathbb{R}^{m \times (n + 1)}$, where we simply add $b$ as a new column of $A$. Then, the following cases apply.
> 1. **Case 1**: If $\text{rank}(A) = \text{rank}([A|b]) = n$, then there exists one solution that is unique.
> 2. **Case 2**: If $\text{rank}(A) = \text{rank}([A|b]) < n$, there are infinitely many solutions.
> 3. **Case 3**: If $\text{rank}(A) \ne \text{rank}([A|b])$, then there does not exist any solution!

In this article, we discuss efficient and practical ways to solve such systems in the real world.

## Solving
### $m = n$ Case
In the case that $m = n$, then we can easily solve 

Convert to one of the forms
1. Upper triangular
2. Lower triangular
3. Unknown, just reorder

---

Recap: Lecture Video

Solve $Ax = b$, where $A$ is a $n \times n$ matrix.
- Inverse transforms: $Ax = b \to (MA)x = Mb$. We can choose suitable $M$ such that our $MA$ becomes easier to handle.

---

The above Gaussian Elimination method is quite naive.
$$
\begin{bmatrix}
0 & 1 \\ 1 & 1
\end{bmatrix}
\begin{bmatrix}
x_1 \\ x_2
\end{bmatrix}
=
\begin{bmatrix}
1 \\ 2
\end{bmatrix}
$$
In such an example, we can't use Gaussian Elimination, as our first
row's pivot is 1! 

In another example, consider
$$
\begin{bmatrix}
\epsilon & 1 \\ 1 & 1
\end{bmatrix}
\begin{bmatrix}
x_1 \\ x_2
\end{bmatrix}
=
\begin{bmatrix}
1 \\ 2
\end{bmatrix}
$$
This can be solved with Gaussian elimination, but will blow up our
matrix numbers, creating lots of error!
> This occurs due to a loss of precision on large numbers ($1 / \epsilon$), which will cause machines to round and giving us imprecise results.

Both of these issues can be fixed if we swap our first and second row
before applying Gaussian Elimination.

This is the idea of **partial pivoting** - before applying Gaussian
Elimination on column $j$, we perform a row exchange $R_i
\leftrightarrow R_j$, $j > i$, so that the pivot element has the
largest magnitude in that column, among all rows $j, j+1, j+2, \dots
n$.

---

$$
\begin{bmatrix}
2 & 2c \\ 1 & 1
\end{bmatrix}
\begin{bmatrix}
x_1 \\ x_2
\end{bmatrix} 
=
\begin{bmatrix}
2c \\ 2
\end{bmatrix}
$$
Where $c \gg 1$, say $c = 10^8$.

As $2 > 1$, we don't apply partial pivoting, and perform Gaussian Elimination as normal. We can do this elimination to find $x_1, x_2 \approx 1$.

On a computer, we round $1 - c \to -c$, due to how large $c$ is, and similarly $2 - c \to -c$.
> Note that to calculate a result, the machine pushes everything to the same exponent (choosing the highest one). However, it only has precision to the $10^{-16}$ power, so we lose the 1 after converting it (as it drops to 0).

This gives us $x_1 = 0$, $x_2 = 1$, which is wrong! Thus, even with partial pivoting, we may still have issues.

---

To address this, we can use a variant of partial pivoting called **scaled partial pivoting**. In this method, we evaluate the "scale" of each row (equation) as
$$
S_i = \max_{1\le j \le n} |a_{ij}|
$$
These scales are fixed to each equation, and will not be recomputed.

While pivoting, find the pivot element for column i by looking at the ratios
$$
\left\{ \frac{|a_{11}|}{S_1}, \frac{|a_{21}|}{S_2}, \frac{|a_{31}|}{S_3} \right\}
$$
And choose the pivot row to be the highest one. Then we perform Gaussian Elimination, and repeat as normal.
> This is essentially scaling our pivots to account for the largest element in the row!

$$
\begin{bmatrix}
2 & 3 & -6 \\ 4 & -6 & 8 \\ 3 & -3 & 3
\end{bmatrix}
\begin{bmatrix}
x_1 \\ x_2 \\ x_3
\end{bmatrix} 
=
\begin{bmatrix}
1 \\ 2 \\ 3
\end{bmatrix}
$$
In this example, $S_1 = 6, S_2 = 8, S_3 = 3$.

We should end with
$$
\begin{bmatrix}
3 & -3 & 3 \\ 0 & 5 & -8 \\ 0 & 0 & 4/5
\end{bmatrix}
\begin{bmatrix}
x_1 \\ x_2 \\ x_3
\end{bmatrix} 
=
\begin{bmatrix}
3 \\ -1 \\ -12/5
\end{bmatrix}
$$

- What if there's a tie between our pivot values? We will break the tie however we want!
- What if pivoting gives us a 0 on our diagonal? We either may not have a solution, or we'll have infinitely many solutions!

When can Gaussian Elimination be used without pivoting? If $A$ is "diagonally dominant", i.e.
$$
|a_{ii}| > \sum_{j=1, j \ne i}^n |a_{ij}|, \forall 1 \le i \le n
$$

---

We can also consider full pivoting, where we swap the order of the variables in the equations... (not really covered).

---
