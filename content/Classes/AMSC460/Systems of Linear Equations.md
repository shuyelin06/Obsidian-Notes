---
title: Systems of Linear Equations
tags:
- amsc460
---

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

## Solving Systems of Linear Equations
Consider the linear system $Ax = b$, where $A$ is an $n \times n$ matrix and $b$ is a vector of length $n$. Given this, how do we find all vectors $x$ which satisfy the equality (known as **solving the system**)?

### Special (Simple) Cases
In some special / simple cases, we can easily solve the system. These cases are given below.
1. When $A$ is a diagonal matrix, we simply divide all terms in $b$ by the corresponding value on $A$'s diagonal.
2. When $A$ is an upper triangular matrix, we can solve it using **back substitution**.
3. When $A$ is a lower triangular matrix, we can solve it using **forward substitution**.

It may even be possible to exchange rows of $A$ and $b$ to obtain one of the above forms!

### Gaussian Elimination
#### Motivation
What do we do if one of the above special cases cannot be easily obtained?

Suppose we have an invertible $n \times n$ matrix $M$. Then, given our system $Ax = b$,
$$
\begin{align*}
    &Ax = b \\
    \equiv &IAx = b \\
    \equiv &(M^{-1} M) Ax = b \\
    \equiv MAx = Mb
\end{align*}
$$
Letting $MA = A'$, $Mb = b'$, we obtain an equivalent system $A'x = b'$! In other words, if $x$ solves $A'x = b'$, it must also solve $Ax = b$.

Thus, we can smartly choose $M$ to obtain a matrix $A'$ that coincides with one of our special cases, to find solutions to our original system!

#### Transformations and Algorithm
Now that we understand the intuition, how do we actually find this matrix $M$?

First, we look at some useful transformations and their corresponding $M$ matrix.
1. We can **multiply** each equation $i$ with a non-zero scalar $\alpha_i$. Then, $M$ is a diagonal matrix with values $\alpha_i$ along the diagonal. 
2. We can add a scalar multiple $\alpha$ of an equation $j$ to another equation $i$. Then, $M$ is the identity matrix with $\alpha$ in the $j^{th}$ row, $i^{th}$ column.
3. We can interchange two equations $i$ and $j$. Then, $M$ is the identity matrix with the $i^{th}$ row and $j^{th}$ row swapped.
   > This is often known as a **permutation matrix**!

We can multiply each of these tranformations together to find a single $M$ matrix that collectively performs all of them! 

Below, we discuss a general algorithm that applies these transformations to obtain a simpler system - **Gaussian Elimination**. In such an algorithm, we essentially continuously subtract a row from the rows beneath it, to obtain an upper triangular matrix.

To make the algorithm clearer, we will show using an example.

Suppose we have the following system.
$$
\begin{bmatrix}
6 & -2 & 2 \\
12 & -8 & 6 \\
3 & -13 & 9 
\end{bmatrix}
\begin{bmatrix}
x_1 \\ x_2 \\ x_3
\end{bmatrix}
= 
\begin{bmatrix}
12 \\ 34 \\ 27
\end{bmatrix} 
\Longrightarrow 
\begin{bmatrix}
6 & -2 & 2 & | & 12 \\
12 & -8 & 6 & | & 34 \\
3 & -13 & 9 & | & 27
\end{bmatrix}
$$

We convert this to a simpler, upper triangular matrix. Note that to do this, we want 0's below our diagonal - and we can achieve this by using each equation to cancel out equations beneath it! 
1. Take our first equation in row 1. Use it to eliminate the first term in all rows below this row. So, we perform
   $$
   \begin{align*}
       R_2 - \frac{12}{6} R_1 \to R_2 \\
       R_3 - \frac{3}{6} R_1 \to R_3 \\
       \Longrightarrow \begin{bmatrix}
        6 & -2 & 2 & | & 12 \\
        0 & -4 & 2 & | & 10 \\
        0 & -12 & 8 & | & 21
       \end{bmatrix}
   \end{align*}
   $$
2. Take our second equation in row 2. Use it to eliminate the second term in all rows below this row. So, we perform
   $$
   \begin{align*}
       R_3 - \frac{-12}{-4} R_2 \to R_3 \\
       \Longrightarrow \begin{bmatrix}
        6 & -2 & 2 & | & 12 \\
        0 & -4 & 2 & | & 10 \\
        0 & 0 & 2 & | & -9
       \end{bmatrix}
   \end{align*}
   $$
3. We are done! Note that we could continue this process for row 3, 4, and onwards, to obtain an upper triangular matrix.

We now have an upper triangular matrix, which we can use back substitution to solve!
> Note that the computational cost of this algorithm is $O(n^3)$.


### Variations of Gaussian Elimination
Note that while the above Gaussian Elimination method is effective, it is also naive. In fact, there exist some systems that the algorithm is not able to solve.

Below, we propose some variations on Gaussian Elimination that avoid these issues, particularly on the computer.

#### Partial Pivoting 
Consider the following systems. Let $\epsilon$ be an extremely small number.
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

\qquad 

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

In these examples, Gaussian Elimination will fail to obtain the correct solution!
1. In the first system, the leading coefficient in the first row is 0, preventing us from obtaining an upper triangular matrix!
2. In the second sytem, while this coefficient is not 0, it is extremely small, which will blow up our numbers and create lots of errors! 

In both examples, we may be able to fix our issues if we swap our first and second row before applying Gaussian Elimination. This is the idea of **partial pivoting**!

In partial pivoting, before we apply a Gaussian Elimination with row $i$, we will check if there exists a row $j$ among rows $\{ i + 1, i + 2, \dots \}$ with a larger leading coefficient. If there does, we perform a row exchange $R_i \leftrightarrow R_j$, and continue as normal. 
> If we swap and our leading coefficient is still 0, our solution is not unique!

#### Scaled Partial Pivoting
However, partial pivoting is also not without issue. Consider the following system, where $c$ is an extremely large number, say $c = 10^{18}$.
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

We apply Gaussian Elimination with partial pivoting.
$$
\begin{bmatrix}
2 & 2c & | & 2c \\ 1 & 1 & | & 2
\end{bmatrix}
\Longrightarrow
\begin{bmatrix}
2 & 2c & | & 2c \\ 0 & 1 - c & | & 2 - c
\end{bmatrix}
$$
Without rounding, we obtain 
$$
\begin{align*}
    &x_2 = \frac{2 - c}{1 - c} \\
    &x_1 = \frac{1}{2} \left( 2c - \frac{2 - c}{1 - c} 2c \right) = \frac{-c}{1 - c} 
\end{align*}
$$
So we should expect to obtain $x_1 \approx 1, x_2 \approx 1$! 

However, on a computer, loss of precision will cause numbers such as $1 - c$ and $2 - c$ to round to $-c$, which will skew our answers!
> Note that to calculate a result, the machine pushes everything to the same exponent (choosing the highest one). However, it only has precision to the $10^{-16}$ power, so we lose the 1 after converting it (as it drops to 0).

$$
\begin{align*}
    &x_2 = \frac{2 - c}{1 - c} \approx 1 \\
    &x_1 = \frac{1}{2} (2c - (1) 2c) = 0
\end{align*}
$$
This gives us an incorrect solution!

To address this, we can use a variant of partial pivoting called **scaled partial pivoting**. Here, we find the **scale** of each row (equation) as the largest coefficient in that row
$$
S_i = \max_{1\le j \le n} |a_{ij}|
$$
> These scales are fixed to each equation, and will not be recomputed.

And while pivoting, we determine row swaps by swapping with the row that has the highest ratio
$$
\left\{ \frac{|a_{11}|}{S_1}, \frac{|a_{21}|}{S_2}, \frac{|a_{31}|}{S_3} \dots \right\}
$$
Then we perform Gaussian Elimination, and repeat as normal.
> We are essentially scaling our pivots to account for the largest element in the row!

Consider the following example.

> [!Example]+ Example: Scaled Partial Pivoting
> Consider the system
> $$
> \begin{bmatrix}
> 2 & 3 & -6 \\ 4 & -6 & 8 \\ 3 & -3 & 3
> \end{bmatrix}
> \begin{bmatrix}
> x_1 \\ x_2 \\ x_3
> \end{bmatrix} 
> =
> \begin{bmatrix}
> 1 \\ 2 \\ 3
> \end{bmatrix}
> $$
> 
> 1. Start with row 1. We have ratios $\{ \frac{2}{6}, \frac{4}{8}, \frac{3}{3} \}$. Swap row 1 and 3.
>    $$
>    \begin{bmatrix}
>    2 & 3 & -6 & \vert & 1\\ 4 & -6 & 8 & \vert & 2 \\ 3 & -3 & 3 & \vert & 3
>    \end{bmatrix}
>    \Longrightarrow 
>    \begin{bmatrix}
>    3 & -3 & 3 & \vert & 3 \\
>    4 & -6 & 8 & \vert & 2 \\ 
>    2 & 3 & -6 & \vert & 1
>    \end{bmatrix}
>    \Longrightarrow 
>    \begin{bmatrix}
>    3 & -3 & 3 & \vert & 3 \\
>    0 & -2 & 4 & \vert & -2 \\ 
>    0 & 5 & -8 & \vert & -1
>    \end{bmatrix}
>    $$
> 2. Continue with row 2. We have ratios $\{ \_ ,\frac{2}{4}, \frac{5}{8} \}$. Swap row 2 and 3.
>    $$
>    \begin{bmatrix}
>    3 & -3 & 3 & \vert & 3 \\
>    0 & -2 & 4 & \vert & -2 \\ 
>    0 & 5 & -8 & \vert & -1
>    \end{bmatrix}
>    \Longrightarrow
>    \begin{bmatrix}
>    3 & -3 & 3 & \vert & 3 \\
>    0 & 5 & -8 & \vert & -1 \\
>    0 & -2 & 4 & \vert & -2 
>    \end{bmatrix}
>    \Longrightarrow
>    \begin{bmatrix}
>    3 & -3 & 3 & \vert & 3 \\
>    0 & 5 & -8 & \vert & -1 \\
>    0 & 0 & \frac{4}{5} & \vert & -\frac{12}{5} 
>    \end{bmatrix}
>    $$
> 
> We have an upper triangular matrix!

Note that if we have a tie between our pivot values, we can break the tie by choosing any row we want! 


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


# Norms and Errors
## Vector Spaces and Norms
A vector space is a set $V$ with two operations
$$
\begin{align*}
    &u + v \in V \quad u,v \in V &\text{Addition} \\
    &au \in V \quad a \in \mathbb{R}, u \in V &\text{Scalar Multiplication}
\end{align*}
$$

Satisfying the following properties:
1. **Commutivity**: $u + v = v + u$
2. **Additive Identity**: There $\exists 0 \in V$ such that $0 + u = u$ for all $u \in V$.
3. **Additive Inverse**: For every $u \in V$, there exists a $w \in V$ such that $u + w = 0$.
4. **Multiplicative Identity**: There $\exists 1 \in \mathbb{R}$ such that $1v = v$ for all $v \in V$.
5. **Distributivity**: For $u,v \in V$, and $a,b \in \mathbb{R}$, 
   $$
   \begin{align*}
       a (u + v) = au + av \\
       (a + b) u = au + bu
   \end{align*}
   $$

Given a vector space $V$, a **norm** is a function $|| \cdot || : V \to \mathbb{R}^+$ satisfying:
1. For all $v \in V$, $||v|| > 0$.
2. If $v = 0$, then $||v|| = 0$.
3. $|| \lambda v || = |\lambda| ||v||$ for some scalar $\lambda$.
4. **Triangle Inequality**: $|| u + v || \le ||u|| + ||v||$

If $V = \mathbb{R}^n$, then the **$l_p$ norm** is given as
$$
|| x ||_p = \left( \sum_{i=1}^n (|x_i|)^p \right)^\frac{1}{p}
$$

> [!Example]+ Example: Norms 
> Some examples are given below.
> $$
> \begin{align*}
>     &|| x ||_2 = \left( \sum_{i=1}^n x_i^2 \right)^\frac{1}{2} &l_2 \; \text{norm - Euclidean Norm} \\
>     &|| x ||_1 = \sum_{i=1}^n |x_i| &l_1 \; \text{norm} \\
>     &|| x ||_\infty = \max_{1 \le i \le n} |x_i|
> \end{align*}
> $$
>
> For example, if $v = (1,2,4)$, then $||v||_\infty = 4$.

> [!Abstract] Theorem: Norm Comparisons
> On $\mathbb{R}^n$, we have
> $$
> || x ||_\infty \le || x ||_2 \le || x ||_1 \le \sqrt{n} || x ||_2 \le n || x ||_\infty 
> $$

Given any norm $|| \cdot ||$ on $\mathbb{R}^n$, the **induced matrix norm** on $\mathbb{R}^{n \times m}$ is given as
$$
||A|| = \sup \{ ||Ax|| : x \in \mathbb{R}^n \& ||x|| = 1 \}
$$
In other words, the maximum norm of $Ax$ given all possible unit vectors $x$.

> [!Abstract] Theorem: Properties of the Matrix Norm
> The following properties of the matrix norm are true.
> - If $A \ne 0$, then $|| A || > 0$.
> - If $A = 0$, then $|| A || = 0$.
> - For any scalar $\lambda$, then $|\lambda| \cdot ||A||$.
> - **Triangle Inequality**: $||A + B|| \le ||A|| + ||B||$
>
> Furthermore, for any vector $x$,
> $$
> ||Ax|| \le ||A|| \cdot ||x||
> $$
> > Note that while $||A||$ is an induced matrix norm, $||Ax||$ is just a vector norm!

> [!Example]+ Example: Matrix Norms
> Note that our matrix norm depends on our selection of the vector norm.
> - If we use the $||x||_\infty$, then $||A||_\infty$ will be the max of each of $A$'s rows sums.
> - If we use $||x||_1$, then $||A||_1$ will be the max of each of $A$'s columns sums.

## Errors in Systems of Equations
### Propagation of Errors on $b$
We can use norms to calculate error propagation!

Consider the system of equations $Ax = b$, and assume $A$ is non-singular.

Let's say we make an error, and take an approximation $\hat{b}$ instead of $b$. Then, our relative error on $b$ is given as
$$
\epsilon_b = \frac{|| b - \hat{b} ||}{||b||}
$$

Given this, how does our error propagate? In other words, what is our relative error in $x$?
1. First, we find that
   $$
   \begin{align*}
   |x - \hat{x}| 
   &= || A^{-1} b - A^{-1} \hat{b} || \\
   &= || A^{-1} (b - \hat{b}) || \\
   &\le || A^{-1} || \cdot || b - \hat{b} ||
   \end{align*}
   $$
2. We also find
   $$
   ||b|| = ||Ax|| \le ||A|| \cdot ||x||
   $$

Using this, we can find the relative error on $x$ as
$$
\begin{align*}
    \epsilon_x 
    &= \frac{||x - \hat{x}||}{||x||} \\
    &\le \frac{||A||}{||b||} || x - \hat{x} || \\
    &\le \frac{||A||}{||b||} ||A^{-1}|| \cdot ||b - \hat{b}|| \\
    &\le ||A|| \cdot ||A^{-1}|| \epsilon_b \\
    &\le K(A) \epsilon_b
\end{align*}
$$

Where $K(A) = ||A|| \cdot ||A^{-1}||$ is the **condition number of $A$**! This tells us the amount in which our error will be magnified.
> Note that our condition number $K(A)$ depends on the vector norm we are using.

> [!Abstract] Theorem: Condition Numbers
> Let $B$ be a singular matrix. Then, for any matrix $A$,
    > $$
> \frac{||A - B||}{||A||} = \frac{1}{K(A)}
> $$

> [!Example]+ Example: Condition Numbers
> $$
> A = 
> \begin{bmatrix}
> 1 & 1 + \epsilon \\
> 1 - \epsilon & 1 
> \end{bmatrix}
> \qquad 
> A^{-1} =
> \frac{1}{\epsilon^2}
> \begin{bmatrix}
> 1 & -1 - \epsilon \\
> -1 + \epsilon & 1 
> \end{bmatrix}
> $$
> 
> Assume we are using the $l_\infty$ norm. Then,
> $$
> \begin{align*}
> &||A||_\infty = 2 + \epsilon \\
> &||A^{-1}||_\infty = \frac{2 + \epsilon}{\epsilon^2} \\
> \Longrightarrow &K(A) = \frac{(2 + \epsilon)^2}{\epsilon^2} > \frac{4}{\epsilon}
> \end{align*}
> $$
> 
> Suppose our $\epsilon$ is small. Then, our condition number will be huge, which is not good!

### Propagation of Errors on $A$
Say for the system $Ax = b$, we now have an approximation of $A$, $\hat{A}$. Also assume that $A$ is non-singular.

What is our error on $x$?

First note the following.
$$
\begin{align*}
       || x - \hat{x} || &= || A^{-1} b - \hat{x} || \\
       &= || A^{-1} (\hat{A} \hat{x}) - \hat{x} || \\
       &= || A^{-1} \hat{A} \hat{x} - A^{-1} A \hat{x} \\
       &\le || A^{-1} || \cdot || \hat{A} - A || \cdot || \hat{x} ||
\end{align*}
$$
Additionally, note that
$$
\begin{align*}
    || \hat{x} || 
    &= || \hat{x} - x + x || \\
    &\le || \hat{x} - x || + || x || \\
    \Longrightarrow \frac{||\hat{x}||}{||x||} &\le \epsilon_x + 1
\end{align*}
$$

We use this to calculate $\epsilon_x$ as
$$
\begin{align*}
    \epsilon_x 
    &= \frac{|| x - \hat{x} ||}{||x||} \\
    &\le || A^{-1} || \cdot || \hat{A} - A || \cdot \frac{||\hat{x}||}{||x||} \\
    &\le || A^{-1} || \cdot || A || \cdot \frac{||\hat{A} - A||}{||A||} \cdot (\epsilon_x + 1) \\
    &\le K(A) \epsilon_A \epsilon_x + K(A) \epsilon_A
\end{align*}
$$
We can refactor to obtain
$$
\epsilon_x \le \left( \frac{K(A)}{1 - K(A) \epsilon_A} \right) \epsilon_A
$$
