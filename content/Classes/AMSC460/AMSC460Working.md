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

# Gaussian Elimination

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

Recap:
- Gaussian Elimination with back substitution. 
- The above is naive and can create issues due to loss of precision, so we discuss possible better algorithms
  - Partial pivoting (MATLAB does partial pivoting with $A \ b$ automatic solving)
  - Scaled partial pivoting

---

We can also consider full pivoting, where we swap the order of the variables in the equations... (not really covered).

---

# LU Factorization
## Introduction
Suppose we can factorize $A$ into a product of two matrices $L$ and $U$, where $L$ is a lower triangular matrix, and $U$ is an upper triangular matrix. This is known as a **LU Factorization (Decomposition)** of $A$.


$$
L = 
\begin{bmatrix}
    a_{11} & 0 & 0 \\
    a_{21} & a_{22} & 0 \\
    a_{31} & a_{32} & a_{33}
\end{bmatrix}
\qquad
U =
\begin{bmatrix}
    a_{11} & a_{12} & a_{13} \\
    0 & a_{22} & a_{23} \\
    0 & 0 & a_{33}
\end{bmatrix}
$$

If $L$ and $U$ are non-singular (which we can check by seeing if any of the diagonals is 0), then the following two systems are equivalent.
$$
Ax = b \Longleftrightarrow Ly = b \qquad Ux = y
$$
This can easily be solved via forward and backward substitutions, which are fairly efficient!

> [!Info] Practical Applications
> LU Factorizations can be useful in solving a system many times under different $b$ vectors! This lets us use backwards / forwards substitution instead of Gaussian elimination, which is faster!
>
> One useful way this can be applied is in finding matrix inverses, as when finding them, we are really just solving the system $A A^{-1} = I$ for each column of $I$! If we factorize $A$ beforehand, we can use substitution to save on a lot of complexity!

Such a decomposition may not even exist! The following theorem lets us know whether or not such a decomposition exists.

> [!Abstract] Theorem: Existence of Decompositions
> Let $A$ be an $n \times n$ matrix. Then, if $A$ can be transformed to $U$ using Gaussian Elimination without any pivoting, there exists a decomposition of $A$.
> > The elimination may still continue after a 0 pivot, as it may still yield a decomposition (albeit with 0's on the diagonal).
>
> Moreover, this decomposition is equal to the inverse of the transform matrix applied to $A$.

Common cases where this occurs is as follows:
- $A$ is **diagonally dominant**
- $A$ is **symmetric and positive definite**: $A = A^T$, and $x^T A x > 0, \forall x \in \mathbb{R}^n, x \ne 0$

However, if we are allowed to interchange the rows of $A$, then we can always obtain an $LU$ factorization!

> [!Abstract] Theorem: Permutations and Factorizations
> Given an $n \times n$ matrix $A$, there exists a $P$ such that
> $$
> PA = LU
> $$
> Where $P$ is the **permutation matrix** of $A$, swapping its rows.

## General Approach to Factorization
Finding a factorization can be a bit tricky! We discuss a general algorithm to find it below.

Let $L$ and $U$ be lower and upper triangular matrices (respectively). If $A = LU$, then 
$$
a_{ij} = \sum_{k=1}^n l_{ik} u_{kj} = \sum_{k=1}^{\min(i,j)} l_{ik} u_{kj}
$$
> Note that we can simplify our summation, because we know $L$ and $U$ are triangular matrices (by assumption), so $l_{ik} = 0$ for $i < k$, and $u_{kj} = 0$ for $j < k$.

Now suppose we either know $l_{11}$ or $u_{11}$. We can use what we know above to derive our $LU$ factorization!
1. We start by deriving row 1 of $U$. Then, for $a_{1j}$, we know that 
   $$
   a_{1j} = l_{11} u_{1j} \Longrightarrow u_{1j} = \frac{a_{1j}}{l_{11}}
   $$
2. Then, we derive column 1 of $L$. Then, for $a_{i1}$, we know that
   $$
   a_{i1} = l_{i1} u_{11} \Longrightarrow l_{i1} = \frac{a_{i1}}{u_{11}}
   $$
3. Now, suppose we want to derive the next row of $U$, or column of $L$. Suppose we have already determined rows $1, 2, \dots s - 1$ of $U$ and columns $1, 2, \dots s - 1$ of $L$ from previous steps. 

    Then, we can find the next rows and columns using the following summations. For the diagonals $l_{ss}$ and $u_{ss}$, choose an arbitrary number for one diagonal, to find the other. 
   $$
   \begin{align*}
       a_{ss} &= \sum_{k=1}^{s-1} l_{sk} u_{ks} + l_{ss} u_{ss} &\text{Next Diagonal} \\
       a_{sj} &= \sum_{k=1}^{s-1} l_{sk} u_{kj} + l_{ss} u_{sj} &\text{Next Row of U, } u_{sj} \\
       a_{is} &= \sum_{k=1}^{s-1} l_{ik} u_{ks} + l_{is} u_{ss} &\text{Next Column of L, } l_{is}
   \end{align*}
   $$
   We repeat this until we are done!

> This algorithm works, provided $l_{ss}$ and $u_{ss}$ are not zero! 

$LU$ decompositions are not unique! If one exists for a matrix $A$, may more could too! Below, we discuss some special decompositions that can be unique in some scenarios.

## Special LU Factorizations
We can find some special LU factorizations of $A$! The following theorem guarantees uniqueness of these factorizations.

> [!Abstract] Uniqueness of LU Factorizations
> If $A$ is invertible, then there exists a $P$ giving us a unique Doolittle factorization, Grout factorization, and Cholesky's factorization.

### Doolittle Factorization
If $A = LU$ where the elements on $L$'s diagonal are 1, then we have a **Doolittle Factorization**.

This is obtained by finding the matrix $M$ with 1's on the diagonal, where the entries below the diagonal are the multipliers used by the Gaussian Elimination, and taking the inverse.

$$
M = 
\begin{bmatrix}
    1 & \\
    \alpha_{21} & 1 \\
    \alpha_{31} & \alpha_{41} & 1 \\ 
    \vdots & & \ddots & \ddots \\
    \alpha_{n1} & \cdots & \cdots & \alpha_{n(n-1)} & 1
\end{bmatrix}

\qquad 

L = M^{-1}
$$

When finding this factorization, set $l_{ss} = 1$ when solving for the diagonal along $u_{ss}$.

> [!Info] Grout's Factorization
> We similarly have **Grout's Factorization**, if $A = LU$ where the elements on $U$'s diagonal are 1.

### Cholesky's Factorization
If $A = LU$ with $L = U^T$, then we have a **Cholesky Factorization**. By definition, $A = L L^T$, meaning that $A$ is not only symmetric, but also positive semi-definite. 
