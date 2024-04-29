---
title: AMSC460Working
tags:
- amsc460
- wip
---

Ordinary Differential Equations

# Introduction
## Ordinary Differential Equations (ODEs)
Let $(t_0, x_0) \in \mathbb{R} \times \mathbb{R}$ and consider an open rectangular neighborhood of $(t_0, x_0)$ 
$$
B = \{ (t,x) \in \mathbb{R} \times \mathbb{R} : t_0 - \delta < t < t_0 + \delta, x_0 - \epsilon < x < x_0 + \epsilon  \}
$$

Let $f(t,x)$ be a funciton defined on this $(t,x)$ plane, and let $T \in \mathbb{R}$ such that
$$
t_0 < T < t_0 + \delta
$$

Then, we want to find the solution of the **ordinary differential equation** (ODE)
$$
\begin{align*}
&\frac{dx (t)}{dt} = f(t,x) \qquad \forall t \in [t_0, T] \\
&x(t_0) = x_0
\end{align*}
$$

This is basically developing a slope field, where the slope varies based on our position $x,t$!

> [!Abstract] Theorem: Uniqueness of Solutions
> Assume that $f(t,x)$ and $f_x (t,x)$ are continuous on $B$. Then, there exists a $t^* \in (t_0, T]$ such that we have a unique solution on $t \in [t_0, t^*)$.

> [!Example]+ Example: Ordinary Differential Equations
> $$
> \begin{align*}
>    &x'(t) = x^{1/3} & t \ge 0\\
>    &x(0) = 0
> \end{align*}
> $$
> 
> We can solve this!
> $$
> \begin{align*}
>     \frac{dx}{dt} = x^{1/3} \\
>     x^{-1/3} dx = dt \\
>     \int_{x(0)}^{x(t)} y^{-1/3} dy = \int_0^t ds \\
>     x(t) = \left( \frac{2t}{3} \right)^{3/2}
> \end{align*}
> $$
> 
> We can also show that
> $$
> x(t) = -\left( \frac{2t}{3} \right)^{3/2} \qquad x(t) = 0
> $$
> Are also solutions. Note that we do not have uniqueness, as the derivative of $x^{1/3}$ with respect to $x$ is not continuous!

> [!Abstract] Theorem: Convergence of Solutions
> Let $x(t)$ and $\tilde{x}(t)$ be the solutions of the ordinary differential equation with initial conditions $x_0$ and $\tilde{x}_0$, respectively. 
> 
> Assume $f_x (t,x) \le M$ for all $t$ and $x$. Then,
> $$
> | x(t) - \tilde{x}(t) | \le | x_0 - \tilde{x}_0 | e^{M (t - t_0)} \qquad \forall t \in [t_0, T]
> $$

This theorem implies the following:
- If $M < 0$, then $e^{M (t - t_0)} \to 0$, implying convergence of $x(t)$ to $\tilde{x}(t)$ exponentially. We call such ODEs **stable**, as solutions converge
- If $M > 0$, then $x(t)$ may diverge away exponentially from $\tilde{x}(t)$. We call such ODEs **unstable**, as solutions diverge.

> [!Example]+ Example: Stability of ODEs
> $$
> x'(t) = e^{4x} - 1 \qquad x(0) = x_0
> $$
> 
> Because $f_x (t,x) = 4e^{4x} > 0$ for all $t,x$, our ODE is unstable! Thus, solutions will diverge.

## Systems of ODEs
### First-Order ODEs
Suppose we have $x_1 (t), x_2 (t), \dots$ and want to find them satisfying 
$$
\begin{align*}
    &x_1'(t) = f_1 (t, x_1(t), x_2(t), \dots ) \\
    &x_2'(t) = f_2 (t, x_1(t), x_2(t), \dots ) \\
    &x_3'(t) = f_3 (t, x_1(t), x_2(t), \dots ) \\
    &\vdots
\end{align*}
$$
With initial conditions $x_i (t_0) = x_{i,0}$.
> Note that our unknowns can be coupled together. If they aren't, then we just have multiple independent ODEs that we can solve separately.

We can also write this in the compact form
$$
\vec{x} (t) =
\begin{bmatrix}
    x_1 (t) \\ x_2 (t) \\ \vdots \\ x_n (t)
\end{bmatrix}
\qquad
\vec{x_0} =
\begin{bmatrix}
    x_{1,0} \\ x_{2,0} \\ \vdots \\ x_{n,0}
\end{bmatrix}
\qquad
\vec{f} (t, \vec{x} (t)) =
\begin{bmatrix}
    f_1 (t, x_1(t), x_2(t), \dots, x_n(t)) \\
    \vdots \\
    f_n (t, x_1(t), x_2(t), \dots, x_n(t))
\end{bmatrix}
$$
$$
\vec{x}'(t) = \vec{f} (t, \vec{x}(t)) \qquad \vec{x}(t_0) = \vec{x_0}
$$

We denote the Jacobian Matrix as
$$
D_{\vec{x}} f(t, \vec{x}) = 
\begin{bmatrix}
    \frac{\partial f_1}{\partial x_1} & \dots & \frac{\partial f_1}{\partial x_n} \\
    \vdots & & \vdots \\
    \frac{\partial f_n}{\partial x_1} & \dots & \frac{\partial f_n}{\partial x_n} \\
\end{bmatrix} 
$$
And define the open rectangle as
$$
B = \{ (t, \vec{x}) \in \mathbb{R} \times \mathbb{R} : t_0 - \delta < t < t_0 + \delta, x_{i,0} - \epsilon_i < x_i < x_{i,0} + \epsilon_i
$$

> [!Abstract] Theorem: Unique Solutions
> If $f$ and $D_{\vec{x}} f$ are continuous in $B$, then there exists a unique solution to the system $\forall t \in [t_0, t^*)$, $t_0 < t^* \le T$.

### Higher Order ODEs
Suppose we have a higher order ordinary differential equation
$$
\frac{d^m x(t)}{dt^m} = g \left(t, x(t), \frac{dx}{dt}, \dots, \frac{d^{m-1} x}{dt} \right)
$$
With initial values
$$
\frac{dx^l}{dt^l} (t_0) = x_{l,0} \qquad \forall l = 0, \dots, m - 1
$$

We can rewrite this as a first order system of ODEs!
$$
y_1 (t) = x(t) \qquad y_2 (y) = x'(t) \qquad \dots \qquad y_m (t) = \frac{d^{m-1} x(t)}{dt^{m-1}}
$$

Then, we can use this and solve our first order system of ODEs as normal. Note that for any $i$, $y_i ' (t) = y_{i+1} (t)$.
$$
\vec{y}(t) = 
\begin{bmatrix}
    y_1 (t) \\ y_2 (t) \\ \vdots \\ y_m (t)
\end{bmatrix}
\vec{y}(t_0) = \vec{y}_0
\qquad
\vec{f}(t,\vec{y}) = 
\begin{bmatrix}
    y_2 (t) \\ \vdots \\ y_m (t) \\ g(t, y_1 (t), \dots, y_m (t))
\end{bmatrix}
$$
$$
\vec{y}'(t) = \vec{f} (t, \vec{y}(t))
$$

# Solving Ordinary Differential Equations
## Forward Euler
We'll begin our discussion of solving ODEs with possibly the simplest algorithm.

Suppose we want to solve the system
$$
\vec{x}'(t) = \vec{f}(t, \vec{x}) \qquad \vec{x}(t_0) = \vec{x}_0
$$

Given our initial condition, we can take incremental small steps in the direction we want!
$$
\tilde{x} (t + \Delta t) = \vec{x} (t) + \Delta t f(t, \vec{x})
$$

So, our algorithm is as follows:
1. We first will divide $[t_0, T]$ into $N$ equal sized subintervals given by
   $$
   t_k = t_0 + k \Delta t \qquad \Delta t = \frac{T - t_0}{N}
   $$
2. Then, we find 
   $$
   \vec{x}^k (t + \Delta t) = \vec{x}^{k-1} (t) + \Delta t f(t, \vec{x}^{k-1})
   $$
   and continue this for all of our steps.
