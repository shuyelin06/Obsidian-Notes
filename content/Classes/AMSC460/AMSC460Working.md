---
title: AMSC460Working
tags:
- amsc460
- wip
---

# Approximation Theory
In [[Interpolation]], we were given a set of points $\{(x_i,y_i)\}_{i=1}^n$, $y_i = f(x_i)$, and asked to construct a polynomial $P(x)$ such that $P(x_i) = f(x_i)$ for all $1 \le i \le n$.

But such interpolations aren't always the best! In the real world, imprecisions can create error, but interpolations will fit these errors precisely! This can give us really poor predictions in practical applications.

In general, our data is not clean. All of our datapoints can be expressed as
$$
y_i = f(x_i) + \epsilon_i
$$
Where $\epsilon_i$ is measurement noise (error) offseting the measurement value.

Below, we examine various ways we can approximate such data.

# Linear Least Squares Problem
Pick $m$ "known" set of functions $\{\phi_i(x)\}_{i=1}^m$, and assume that for constants $c_1, \dots c_m$
$$
f(x) = c_1 \phi_1 (x) + c_2 \phi_2 (x) + \dots c_m \phi_m (x) = \sum_{i=1}^m c_j \phi_j (x)
$$
For all $x \in I$.

Now suppose we are given noisy data $\{(x_i,y_i)\}_{i=1}^n$. Note that to determine $m$ unknowns, we need $n \ge m$. However, if we have $n > m$, which is typically the case, we have an **overdetermined situation**, where we have more conditions than unknowns.

Because of this, we need some notion of "best fit"! Given our function $f(x)$, we define the residual error at $x_i$ to be
$$
r_i = f(x_i) - y_i = \sum_{i=1}^m c_j \phi_j (x_i) - y_i \qquad \forall 1 \le 1 \le n
$$
Giving us a residual vector  $r = [r_1, r_2, \dots r_n]^T \in \mathbb{R}^n$. We want to find constants $\{c_j\}_{j=1}^m$ such that this residual vector has as small of  amagnitude as possible, given some norm $|| \cdot ||$.

Define the matrix $A \in \mathbb{R}^{n \times m}$ where $A_{ij} = \phi_j (x_i)$, and our constant vector $c$.
$$
A =
\begin{bmatrix}
    \phi_1 (x_1) & \phi_2 (x_1) & \dots & \phi_m (x_1) \\
    \phi_1 (x_2) & \phi_2 (x_2) & \dots & \phi_m (x_2) \\
    \vdots \\
    \phi_1 (x_n) & \phi_2 (x_n) & \dots & \phi_m (x_n)
\end{bmatrix}
\qquad
c = 
\begin{bmatrix}
    c_1 \\ c_2 \\ \dots \\ c_m
\end{bmatrix}
$$

We can define our residual error vector as follows:
$$
r = Ac - y
$$

We want to minimize $||r||_2 = (\sum_{i=1}^n r_i^2)^\frac{1}{2}$. To do this, let's define the objective function, with our constant vector $c$ as a parameter
$$
\begin{align*}
    \epsilon(c) 
    &= \sum_{i=1}^n (r_i(c))^2 = || Ac -  y||_2^2 \\
    &= (Ac - y)^T (Ac - y) = c^T A^T Ac - 2 y^T A c + y^T y
\end{align*}
$$
We wish to find the $c$ that minimizes this. Differentiating with respect to any $c_j$, we get
$$
\begin{align*}
    \frac{\partial \epsilon(c)}{\partial c_j} 
    &= \sum_{i=1}^n \frac{\partial}{\partial c_j} ( r_i (c)^2 ) = \sum_{i=1}^n 2 r_i (c) \frac{\partial r_i (c)}{\partial c_j} \\
    &= \sum_{i=1}^n 2 r_i \phi_j (x_i) = 2 (A_{1i} r_1 + A_{2i} r_2 + \dots A_{ni} r_n)
\end{align*}
$$

So, to find where the derivative is 0 (the minimum), we wish to find
$$
A^T r = 0
$$
Which are known as the **normal equations**.
> We call it this, as our residual vector $r$ is normal (orthogonal) to the column vectors of $A$!

We can plug this back into our original equation to obtain
$$
\begin{align*}
    r = Ac - y \\
    A^T r = 0 = A^T (Ac - y) \\
    A^T A c = A^T y
\end{align*}
$$
Which is a linear system we can solve for $c$! So, to find our best fit, we:
1. Construct $A$ from our $x_i$'s and $\phi_j$'s given
2. Construct $M = A^T A$ and $b = A^T y$
3. Solve $Mc = b$

> Typically, we want to solve the normal equations ourselves, as solving them on a computer can lead to a highly unstable algorithm!

> [!Abstract] Theorem: Uniqueness of Solutions
> If the columns of $A$ are linearly independent, then
> 1. The normal equations have a unique solution for $c$.
> 2. If $c$ is this unique solution, then it minimizes the residual error - that is, $||Ac - y|| \le ||Ac^* - y||$ for all $c \ne c^*$.

> [!Example]+ Example: Deriving $f$
> Let $m = 2$, where
> $$
> \phi_1 (x) = 1 \qquad \phi_2 (x) = x
> $$
>
> Say we have $n$ points $\{(x_i,y_i)\}_{i=1}^n$. We want function
> $$
> f(x) = c_1 + c_2 x
> $$
> > We are essentially finding a line that minimizes the square of the vertical distances to each point.
> 
> To find our constants, we first find $A$ as
> $$
> A =
> \begin{bmatrix}
>     1 & x_1 \\
>     1 & x_2 \\
>     \vdots \\
>     1 & x_n
> \end{bmatrix}
> $$
> We use this to find $A^T A$, $A^T y$ as
> $$
> A^T A =
> \begin{bmatrix}
>     n & \sum_{i=1}^n x_i \\
>     \sum_{i=1}^n x_i & \sum_{i=1}^n x_i^2
> \end{bmatrix}
> \qquad
> A^T y =
> \begin{bmatrix}
>     \sum_{i=1}^n y_i \\
>     \sum_{i=1}^n x_i y_i
> \end{bmatrix}
> $$
> We can use this to solve for $c$!

> [!Info] Linear Least Squares Pros
> Note that Linear Least Squares only works well if we know the following about the noise:
> - The average noise has no bias; as in, the average is 0.
> - The noise is uncorrelated.
> - The noise's variance is approximately the same.
