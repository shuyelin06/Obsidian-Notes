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
We can use these vectors to determine the cost of producing them! For example, if we wanted to produce $p_A, p_B, p_C$ units of $A,B,C$ (respectively), we can find our cost as
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

> How much do we need to tell the sectors to produce?
