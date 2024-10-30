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
- [[Markov Chains]]
- Heat Diffusion and Systems of Linear Differential Equations
- Matrix Exponentials and Rotations
- ..
- ..

---




# Heat Diffusion and Differential Equations
Suppose we have a thin metal rod of length $L$, and let $u(x,t)$ be the temperature at some point in the rod at some particular point in time. We'll assume that the rod is perfectly insulated for $x$, $0 < x < L$ (so no heat can be lost in the middle).

The function $u(x,t)$ satisfies the **Heat Equation**
$$
\frac{\partial u}{\partial t} = k \frac{\partial^2 u}{\partial x^2}
$$
For some physical constant $k$. 
> This is a partial differential equation!

Additionally, the function must also satisfy some **boundary conditions**, specifying what the temperature should be at the ends:
- Temperature at $x = 0$ and $x = L$ is held fixed.
- The rod is perfectly insulated at the endpoints.

In this class, rather than studying the PDE, we will model the rod differently by discretizing space. Divide the rod into $n$ chunks, and assume that for any chunk at a particular time, the temperature is uniform along the entire chunk. 

With this simplified setup, each chunk will have its own temperature function only depending on time, $u_i (t)$.
$$
u_1 (t), u_2 (t), \dots u_n (t)
$$
So instead of trying to solve for $u(x,t)$, we'll try to solve for the vector-valued function
$$
\vec{u}(t) = (u_1 (t), u_2 (t), \dots, u_n (t))^T
$$
Which is a lot easier to solve for!

---

We start in the case where $n = 2$. We'll assume that $u = 0$ outside of the endpoints of the rod, and heat can flow from the rod outside the endpoints.
$$
0 \quad u_1 (t) \quad u_2 (t) \quad 0
$$
The main principle is that the rate at which heat flows across a boundary is proportional to the temperature difference of the two regions on either side. We'll assume the constant proportionality is 1. Then, our regions would have temperature functions given by
$$
\begin{align*}
u_1'(t) 
&= 1 (0 - u_1(t)) + (u_2(t) - u_1(t)) \\
&= -2 u_1(t) + u_2 (t) \\
u_2'(t)
&= (u_1 - u_2(t)) + (0 - u_2(t)) \\
&= -2 u_2(t) + u_1 (t)
\end{align*}
$$
This gives us a system of ordinary differential equations! We put the functions in a vector valued function $\vec{u}(t) = (u_1(t), u_2(t))^T$
$$
\vec{u}'(t) = 
\begin{bmatrix} u_1'(t) \\ u_2'(t) \end{bmatrix} =
\begin{bmatrix} -2 u_1(t) + u_2 (t) \\ -2 u_2(t) + u_1(t) \end{bmatrix} =
\begin{bmatrix}
-2 & 1 \\
1 & -2 
\end{bmatrix} \vec{u}(t) = A \vec{u}(t)
$$
To solve for $\vec{u}(t)$, we need an initial condition, say $\vec{u}(0) = (10, 0)^T$. We ask, how do we solve these general forms of equations?
