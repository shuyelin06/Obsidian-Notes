---
title: MATH401
tags:
- math401
---

This course, Applications in Linear Algebra, describes various ways we can use linear algebra in the real world.

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

- [[Leontief Input-Output]]
- [[Applications of Graphics]]
- [[Least Squares]]
- Linear Discrete Dynamical systems
- Markov Chains
- Google Pagerank Algorithm
- Heat Diffusion and Systems of Linear Differential Equations
- Matrix Exponentials and Rotations
- ..
- ..

---

# (Linear) Discrete Dynamical Systems
We first review some concepts around eigenvalues and eigenvectors.

An **eigenvector** for $A$ is a non-zero vector $\vec{x}$ with the property that
$$
Ax = \lambda x
$$
Where $\lambda$ is some scalar value. In other words, $Ax$ is a scalar multiple of $x$.

We can solve for eigenvectors using the following system:
$$
A \vec{x} = \lambda \vec{x} \Longrightarrow (A - \lambda I_n) \vec{x} = 0
$$
> $I_n$ is the $n \times n$ identity matrix.

If $\lambda$ is an eigenvalue for $A$, then the following are also true.
- There is a non-zero $\vec{x}$ such that $A \vec{x} = \lambda \vec{x}$.
- There is $\vec{x} \ne 0$ such that $(A - \lambda I_n) \vec{x} = \vec{0}$
- $A - \lambda I_n$ is not invertible
- $\text{det}(A - \lambda I_n) = 0$

Additionally, if $\lambda$ is an eigenvalue, then we know that $\lambda$ satisfies the **characteristic equation**
$$
\text{det}(A - \lambda I_n) = 0
$$
So, generally, the process is:
1. Find the eigenvalues for $A$ by solving the characteristic equation for $\lambda$
2. Find eigenvectors for $\lambda$ by solving the system $(A - \lambda I_n) = 0$. 

> [!Example] Example: Eigenvectors and Eigenvalues
> $$
> A = \begin{bmatrix} 1 & 1 \\ -2 & 4 \end{bmatrix}
> $$
> We find the eigenvalues first by solving
> $$
> \begin{align*}
> \text{det} (A - \lambda I_2) &= 0 \\
> \begin{vmatrix} 1 - \lambda & 1 \\ -2 & 4 - \lambda \end{vmatrix} &= 0 \\
> (\lambda - 2) (\lambda - 3) &= 0 \\
> \lambda &= 2,3
> \end{align*}
> $$
> 
> We can now find our eigenvectors. Say we want the eigenvector for $\lambda = 2$. Then, we solve system
> $$
> \begin{align*}
> (A - 2 I_2) \vec{x} = 0 \\
> \begin{bmatrix}
> -1 & 1 \\ -2 & 2
> \end{bmatrix} \vec{x} = 0
> \end{align*}
> $$

An $n \times n$ matrix $A$ is **diagonalizable** if there is an invertible matrix $P$ and a diagonal $n \times n$ matrix $D$ such that
$$
A = P D P^{-1}
$$

> [!Abstract] Theorem: Eigenvectors of Diagonalizable Matrices
> An $n \times n$ matrix $A$ is diagonalizable if and only if $A$ must have $n$ linearly independent eigenvectors $\vec{v}_1, \vec{v}_2, \dots \vec{v}_n$.
>
> In this case, $A = P D P^{-1}$ where $P$'s columns are the eigenvectors, and $D$'s diagonal values are their respective eigenvalues.
> $$
> P = \begin{bmatrix} 
> \vec{v}_1 & \vec{v}_2 & \dots & \vec{v}_n
> \end{bmatrix} \qquad
> D = \begin{bmatrix} 
> \lambda_1 & 0 & \dots & 0  \\
> 0 & \lambda_2 & \dots & 0 \\
> \vdots & \vdots & \ddots & \vdots \\
> 0 & 0 & \dots & \lambda_n
> \end{bmatrix}
> $$

Let's see how we can use these concepts.

Suppose we have a population of predators (ex. hawks), who live among a population of prey (ex. rats). Let $H_k$ be the number of hawks after $k$ months have passed, and $R_k$ be the number of rats (in thousands) after $k$ months. We'll only consider integers of $k$ months.

Assume that these populations evolve according to some sort of model as follows:
$$
\begin{align*}
H_{k+1} = (0.4) H_k + (0.5) R_k \\
R_{k+1} = (-0.2) H_k + (1.2) R_k
\end{align*}
$$
> Note that if we know this, then given the populations in some month $k$, we should be able to compute the populations in the next month!

> [!Example] 
> Say we know initial populations $H_0 = 500$, $R_0 = 250$.
>
> We can find closed formulas for $H_k$, $R_k$ using our model above, and determine their limits as $k \to \infty$.
