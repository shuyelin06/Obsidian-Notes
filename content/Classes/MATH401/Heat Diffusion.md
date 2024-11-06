---
title: Heat Diffusion
tags:
- math401
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

Let $A$ be an $n \times n$ matrix and let $\vec{x}(t) = (x_1 (t), x_2 (t), \dots x_n(t))^T$. We'd like to be able to solve the problem
$$
\vec{x}' (t) = A \vec{x} (t) \qquad \vec{x}(0) = \vec{x}_0
$$
For $\vec{t}$.

> [!Example]+ Example: $n = 1$ Case
> What if $n = 1$? Then, we have
> $$
> x'(t) = a x(t) \qquad x(0) = x_0
> $$
> Where $a$ is a scalar, and $x(t)$ is real-valued. Here, any solution of this has the form $x(t) = C e^{at}$, and with our initial value, then our solution is $x(t) = x_0 e^{at}$!

Given the above, could it be true that $e^{At}$ is a solution to our problem? Maybe, but what does this mean?

Recall that for any real number $x$, we have Taylor Series
$$
e^x = \sum_{k=0}^\infty \frac{x^k}{k!} = 1 + x + \frac{x^2}{2} + \frac{x^3}{3!} + \dots
$$
So, if $A$ is an $n \times n$ matrix, we can define the **matrix exponential** as
$$
e^A = \sum_{k=0}^\infty \frac{1}{k!} A^k = I + A + \frac{1}{2} A^2 + \frac{1}{3!} A^3 + \dots
$$

> [!Abstract] Proposition
> For any $n \times n$ matrix, this series converges. Note that as this series is a sum of matrix products, $e^A$ too is a matrix.

Now consider $e^{tA}$, where $t$ is a real variable and $A$ is a fixed $n \times n$ matrix. $e^{tA}$ is a matrix valued function of $t$. What is its derivative with respect to $t$?

> [!Abstract] Proposition
> Let $A$ be an $n \times n$ matrix. Then, 
> $$
> \frac{d}{dt} e^{tA} = A e^{tA}
> $$

> [!Abstract] Theorem
> Let $A$ be $n \times n$. The unique solution to the problem
> $$
> \vec{x}'(t) = A \vec{x} (t) \qquad \vec{x}(0) = \vec{x}_0
> $$
> Is $\vec{x}(t) = e^{tA} \vec{x}_0$.
>
> > [!Note]- Proof
> > 
> > Let's show that $\vec{x}(t) = e^{tA} \vec{x}_0$ satisfies the differential equation and initial condition.
> > 
> > $$
> > \vec{x}' (t) = \frac{d}{dt} e^{tA} \vec{x}_0 = A e^{tA} \vec{x}_0 = A \vec{x}(t)
> > $$
> > $$
> > \vec{x} (0) = e^{0A} \vec{x}_0 = I \vec{x_0} = \vec{x}_0
> > $$

So to solve our problem, we need to solve the matrix exponential! But how does one actually compute the matrix exponential, $e^A$ or $e^{tA}$? 

This can be done with diagonalization! This is very easy for a diagonal matrix.

> [!Example]+ Example: Matrix Exponentials for Diagonal Matrices
> $$
> D = 
> \begin{bmatrix}
> \lambda_1 & 0 \\
> 0 & \lambda_2 
> \end{bmatrix}
> $$
> 
> What is $e^D$? 
> $$
> e^D = \sum_{k=0}^\infty \frac{1}{k!} D^k =
> \begin{bmatrix}
> \sum_{k=0}^\infty \frac{1}{k!} \lambda_1^k & 0 \\
> 0 & \sum_{k=0}^\infty \frac{1}{k!} \lambda_2^k
> \end{bmatrix} = 
> \begin{bmatrix}
> e^{\lambda_1} & 0 \\
> 0 & e^{\lambda_2}
> \end{bmatrix} 
> $$

In general, for any diagonal matrix $D$, the matrix exponential is
$$
e^D = 
\begin{bmatrix}
e^{\lambda_1} & 0 & \dots & 0 \\
0 & e^{\lambda_2} & \dots & 0 \\
\vdots & \vdots & \ddots & \vdots \\
0 & 0 & \dots & e^{\lambda_n}
\end{bmatrix} 
$$

What if $A$ is diagonalizable ($A = P D P^{-1}$)? Then, our matrix exponential is
$$
e^A = \sum_{k=0}^\infty \frac{1}{k!} A^k = P \left( \sum_{k=0}^\infty \frac{1}{k!} D^k \right) P^{-1}
$$
We can use this to find the solution to our system!

> [!Abstract] Theorem: Diagonalizable Matrix Exponentials
> Suppose $A = P D P^{-1}$. Then $e^A = P e^D P^{-1}$
>
> More generally, if $e^{tA}$, then $e^A = P e^{tD} P^{-1}$.

> [!Example]+ Example
> Suppose we have system
> $$
> \vec{u}'(t) = 
> \begin{bmatrix} -2 & 1 \\ 1 & -2 \end{bmatrix}
> \vec{u}(t) \qquad 
> u(t) = \begin{bmatrix} 10 \\ 0 \end{bmatrix}
> $$
> 
> By our theorem, we can find the solution as
> $$
> \vec{u}(t) = e^{tA} \begin{bmatrix} 10 \\ 0 \end{bmatrix}
> $$
> 
> So, let's solve for $e^{tA}$! We can diagonalize $A$ as
> $$
> A = P D P^{-1} = 
> \begin{bmatrix} 1 & 1 \\ 1 & -1 \end{bmatrix}
> \begin{bmatrix} -1 & 0 \\ 0 & -3 \end{bmatrix}
> \begin{bmatrix} 1/2 & 1/2 \\ 1/2 & -1/2 \end{bmatrix}
> $$
> And can then find $e^{tA}$ as
> $$
> e^{tA} = P e^{tD} P^{-1}
> \begin{bmatrix} 1 & 1 \\ 1 & -1 \end{bmatrix}
> \begin{bmatrix} e^{-t} & 0 \\ 0 & e^{-3t} \end{bmatrix}
> \begin{bmatrix} 1/2 & 1/2 \\ 1/2 & -1/2 \end{bmatrix}
> $$
> We can multiply this with our vector to obtain the final result!
> $$
> \vec{u}(t) = 
> \begin{bmatrix} 
> 5e^{-t} + 5e^{-3t} \\ 
> 5e^{-t} - 5e^{-3t}
> \end{bmatrix}
> $$
