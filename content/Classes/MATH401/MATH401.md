---
title: MATH401
tags:
- math401
---

This course, Applications in Linear Algebra, describes various ways we can


- Leontief Input-Output Model
- Applications to Computer Graphics
- Least Squares and Curve Fitting
- Team Ranking
- Linear Discrete Dynamical systems
- Markov Chains
- Google Pagerank Algorithm
- Heat Diffusion and Systems of Linear Differential Equations
- Matrix Exponentials and Rotations
- ..
- ..

---

We begin by describing a brief but important theorem for this course.

> [!Abstract] Theorem: Uniqueness of Invertible Linear Systems 
> Suppose we have a linear system
> $$
> A \vec{x} = \vec{b}
> $$
> with $n$ variables and $n$ equations. Then, if $A$ is an invertible $n \times n$ matrix, then the linear system has 1 and only 1 solution, and we can find it by taking
> $$
> \vec{x} = A^{-1} \vec{b}
> $$

# Leontief Input-Output Model
Suppose we have an economy, divided into sectors $A,B,C$, and each sector produces a product. For a sector to produce its product, it could consume some of its own product as well as some of the products produced by the other sectors. 

For example, let $A, B, C$ be our products. Suppose that
- To produce 1 unit of product $A$, we need 0.2 units of $A$, 0.15 units of $B$, and 0.1 units of product $C$.
- To produce 1 unit of product $B$, we need 0.25 units of $A$, and 0.05 units of $B$.
- To produce 1 unit of product $C$, we need 0.2 units of $B$, and 0.1 units of $C$.

> Assume that all units are on the same scale, presented in monetary value (making the unit standardized across all products).

For each product, we can create a **consumption vector**, representing what it takes to produce that product.
$$
A : \begin{bmatrix}
0.2 \\ 0.15 \\ 0.1
\end{bmatrix}
\quad
B : \begin{bmatrix}
0.25 \\ 0.05 \\ 0
\end{bmatrix}
\quad
C : \begin{bmatrix}
0 \\ 0.2 \\ 0.1
\end{bmatrix}
$$
We can use these vectors to determine the cost of producing each product! For example, if we wanted to produce $p_A, p_B, p_C$ units of $A,B,C$ (respectively), we can find our cost as
$$
p_A \begin{bmatrix}
0.2 \\ 0.15 \\ 0.1
\end{bmatrix}
+ p_B \begin{bmatrix}
0.25 \\ 0.05 \\ 0
\end{bmatrix}
+ p_C \begin{bmatrix}
0 \\ 0.2 \\ 0.1
\end{bmatrix}
= 
\begin{bmatrix}
0.2 & 0.25 & 0 \\
0.15 & 0.05 & 0.2 \\
0.1 & 0 & 0.1 
\end{bmatrix} 
\begin{bmatrix}
p_A \\ p_B \\ p_C
\end{bmatrix}
= M \vec{p}
$$

This gives us a matrix vector product, where $\vec{p}$ contains the amounts produced, $M$ is called the **consumption matrix**, and $M \vec{p}$ is called the **internal demand** (amounts of products that are consumed).

Now say we have some demand outside of our economy for these products, say $d_A = 50$ units of $A$, $d_B = 80$ units of $B$, and $d_C = 100$ units of $C$. How much of each product do we need to produce?

Because each product uses the other products, we can't just supply exactly $d_A, d_B, d_C$. We need to supply more to be used internally as input elsewhere in the economy! This motivates the **Leontief Input-Output Model**, stating that for any product, it's amount produced is equal to the sum of its **internal** and **external demand**.
$$
\text{Amount Produced} = \text{Internal Demand} + \text{External Demand}
$$
In mathematical terms,
$$
\vec{p} = M \vec{p} + \vec{d}
$$
So given our consumption matrix $M$ and external demand $\vec{d}$, we ask: what must we set $\vec{p}$ to so that we can satisfy the external demand?

We can solve this equation for $\vec{p}$ as so.
$$
\begin{align*}
\vec{p} &= M \vec{p} + \vec{d} \\
\vec{p} - M \vec{p} &= \vec{d} \\
(I - M) \vec{p} &= \vec{d}
\end{align*}
$$

This gives us a linear system that we can solve!

So, in our example, we can solve to find our production amounts
$$
\vec{p} = \left(
I - \begin{bmatrix}
0.2 & 0.25 & 0 \\
0.15 & 0.05 & 0.2 \\
0.1 & 0 & 0.1 
\end{bmatrix} 
\right)^{-1}
\begin{bmatrix}
50 \\ 80 \\ 100
\end{bmatrix} \approx
\begin{bmatrix}
101.89 \\ 126.07 \\ 122.43
\end{bmatrix}
$$
101.89 of $A$, 126.07 of $B$, and 122.43 of $C$.
> Note that our solution requires that $(I - M)$ is invertible. While it may not always be, "reasonable" conditions in economies typically imply that $I - M$ would be invertible.

> [!Info] Conceptually Interpreting $(I - M)^{-1}$
> Note that each column of $(I - M)^{-1}$ gives us the **increase** tells us the amount of extra production needed for each product! For example, if we wanted to produce $(1,0,0)$ of products, we can find it as $\vec{p} = (I - M)^{-1} (1,0,0)^T$, which is just the first column!
>
> In more mathematical terms, the $j^{th}$ colum of $(I - M)^{-1}$ contains the additional production required to satisfy an additional unit of external demand for product $j$.

Given this interpretation, it should make sense that:
- The diagonal entries of $(I - M)^{-1}$ are $\ge 1$. 
- The entries of $(I - M)^{-1}$ should be non-negative.

But is there a mathematical explanation for this? Under certain conditions of $M$, it is true that
$$
(I - M)^{-1} = I + M + M^2 + M^3 + \dots
$$
First, we observe that all terms on the right-hand side should have non-negative entries (as $M$ has all non-negative entries- we cannot consume negative products)! Furthermore, as $I$ has 1's down the diagonal, this means that our inverse must have values $\ge 1$, as we are only adding positive numbers to 1!

These conditions are $M$ are as follows. We define a **column sum** of a matrix to be the sum of the entires in any given column of the matrix. Any matrix $M$ with column sums $<1$ satisfy the above condition, and in fact, any "reasonable" economy is one where each column sum is $<1$.
> Otherwise, it would take more than one unit to produce a unit of a product, which is not smart!
