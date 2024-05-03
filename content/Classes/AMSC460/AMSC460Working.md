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
## Forward Euler Method
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

Let's find the error for this method! At the $k^{th}$ step, we have error
$$
\begin{align*}
&e^k = |x^k - x(t_k)| \qquad \forall k = 0, \dots N \\
&e^0 = 0
\end{align*}
$$

---

??

Using Taylor expansion at $t_k$, we get
$$
\begin{align*}
x(t_{k+1}) = x(t_k + \Delta t) 
&= x(t_k) + x'(t_k) \Delta t + x''(\epsilon_k) \Delta \frac{t^2}{2} \\
&= x(t_k) + f(t_k, x(t_k)) \Delta t + x''(\epsilon_k) \frac{\Delta t^2}{2}
\end{align*}
$$

$$
\begin{align*}

\end{align*}
$$


---

$$
\begin{align*}
    &\alpha_k = | 1 + \Delta t f_x (t_k, n_k) | &\text{Amplification Factor} \\
    &r_k = \frac{\Delta t^2}{2} |\ddot{x}(\epsilon_k)| &\text{Local Truncation Error}
\end{align*}
$$

Giving us error term
$$
e^{k+1} \le \alpha_k e^k + r_k
$$

Let's analyze this error.

### General Case
Assume the following.
- $| f_x (t,x) | \le C_1$ for all $t \in [t_0, T]$, $\forall x$
- $| \ddot{x}(t) | \le C_2$ for all $t \in [t_0, T]$

Given a bound, we can find an upper bound for our error!
$$
\begin{align*}
    \alpha_k \le 1 + \Delta t C_1 = L \\
    r_k \le \frac{\Delta t^2}{2} C_2 = M \\
    \Longrightarrow e^{k+1} \le L e^k + M
\end{align*}
$$

Using this iteratively, we get error bound
$$
\begin{align*}
    Err^k 
    &\le Le^{k-1} + M \\
    &\le L (L e^{k-2} + M) + M \\
    &\vdots \\
    &\le L^k e^0  + (1 + L + L^2 + \dots + L^{k-1}) M \\
    &\le \left(\frac{L^k - 1}{L - 1} \right) M \\
    &\le \frac{L^k M}{L - 1} = \frac{(1 + \Delta t C_1)^k}{\Delta t C_1} \frac{\Delta t^2}{2} C_2 \\
    &\le e^{\Delta t C_1 k} \frac{C_2}{2 C_1} \Delta t = e^{(t_k - t_0) C_1} \frac{C_2 \Delta t}{C_1}
\end{align*}
$$

Some key takeaways:
- Our error bound can increase exponentially as our final $t_k$ step gets further away from our initial guess.
- Our error is bounded by $C \Delta t$, where $C = e^{(t_k - t_0) C_1} \frac{C_2}{C_1}$, which controls it (given our final time is the same), making our error a first order method.

> [!Example] Example
> $$
> \begin{align*}
> \dot{x} (t) = x - \sin(t) - \cos(t) \\
> x(0) = 1
> \end{align*}
> $$

### Special Case
Assume that our ordinary differential equation is stable.
- $\exists C_0 \le C_1 < 0$ such that $C_0 \le f_x (t,x) \le C_1 < 0$, for all $t \in [t_0, T]$ and $\forall x$. 
- $| \ddot{x}(t) | \le C_2$ for all $t \in [t_0, T]$.

This gives us
$$
1 + \Delta t C_0 \le 1 + \Delta t f_x (t,x) \le 1 + \Delta t C_1 < 1
$$
> Notice how as $\Delta t > 0$ becomes smaller, this converges to 1!

If we choose $\Delta t$ small enough such that
$$
- (1 + \Delta t C_1) \le 1 + \Delta t C_0 
$$
We get
$$
\Delta t \le \frac{2}{-C_0 - C_1}
$$

Then,
$$
-1 < -(1 + \Delta t C_1) \le 1 + f_x (t,x) \Delta t \le 1 + \Delta t C_1 < 1 \Longrightarrow \alpha_k \le 1 + \Delta t C_1 < 1
$$

Repeating what we did earlier, we get
$$
e^k \le \left(\frac{1 - L^k}{1 - L}\right) M \le -\frac{C_2}{2C_1} \Delta t\\
$$
Giving us a first order error whose which is not dependent on our final $t_k$! Our error remains bounded.

---

Let's take a closer look at the local truncation error. It represents the error from one time step of the algorithm, but also indicates the degree in which the true solution doesn't satisfy the algorithm.

To find the order $p$ of the method, we have
- Local Truncation Error $O(\Delta t^{p+1})$
- Global Error $O(\Delta t^p)$

For a second order method, we should try to get a local truncation error $O(\Delta t^3)$.

> [!Info] Forward Euler Takeaways
> - 1 evaluation of $f$ per step
> - Local truncation error of $O(\Delta t^2)$
> - Global error of $O(\Delta t)$ - first order.

How can we get such a method?

## Runge Kutta Method (Multi-Step Methods)
The **Runge Kutta Method** describes multi-step methods we can use to solve systems of ordinary differential equations.
> We will discuss the **RK-2** method.

Consider the system
$$
\dot{x}(t) = f(t, x(t))
$$

If we integrate our ordinary differential equation from $t_1 = t_0 + \Delta t$, we'll get
$$
x(t_1) = x(t_0) + \int_{t_0}^{t_1} f(t, x(H)) dt
$$

We have $x(t_0)$ as an initial condition, but knowing $x(H)$ requires us to have already solved the system! So, we'll approximate our integral instead.

Let $g(t) = f(t, x(H))$. Then, we'll approximate our integral $I$ using a quadrature $Q_\Delta$ such that
$$
I = \int_{t_0}^{t_1} g(t) dt \qquad | I - Q_\Delta | \le C \Delta t^3 
$$
> Note that this gives us error
> $$
> | I - Q_\Delta | \le \frac{\Delta t^3}{12} | g''(\epsilon) | = O(\Delta t^3)
> $$

Let $Q_\Delta$ be the trapezoidal rule. Then, we have approximation
$$
I \approx Q_\Delta = \frac{g(t_1) + g(t_0)}{2} (t_1 - t_0) = \frac{f(t_0, x(t_0)) + f(t_1, x(t_1))}{2} (t_1 - t_0)
$$
But we're trying to solve for $x(t_1)$, so we don't know $f(t_1, x(t_1))$! Suppose we used Forward Euler to approximate $x(t_1)$ in $Q_\Delta$ to get quadrature 
$$
\hat{Q}_\Delta = \frac{f(t_0, x(t_0)) + f(t_1, x^\text{1, Euler})}{2} (t_1 - t_0)
$$
> Recall that the error of this would be
> $$
> | x^\text{1, Euler} - x(t_1) | \le C \Delta t^2 = O(\Delta t^2)
> $$


Furthermore, let's use MVT to find an $n$ between $x(t_1)$, $x^\text{1, Euler}$ such that
$$
| f(t_1, x(t_1)) - f(t_1, x^\text{1, Euler}) | = | f_x (t_1, n) | \cdot | x(t_1) - x^\text{1, Euler} |
$$

We find error
$$
\begin{align*}
| I - \hat{Q}_\Delta | &= | I - Q_\Delta + Q_\Delta - \hat{Q}_\Delta | \\
&= | I - Q_\Delta | + | Q_\Delta - \hat{Q}_\Delta | \\
&\le C \Delta t^3 + \frac{\Delta t}{2} | f(t_1, x(t_1)) - f(t_1, x^\text{1, Euler}) | \\
&\le C \Delta t^3 + \frac{\Delta t}{2} | f_x (t_1, n) | C \Delta t^2
\end{align*}
$$

Assume that $| f_x (t,x) | \le C_2$. Then, our RK-2 scheme will have local truncation error $O(\Delta t^3)$!

Our **RK-2** Scheme is given as
$$
x^{k+1} = x^k + \frac{\Delta t}{2} ( f(t_k, x^k) + f(t_k, x^{t_k, \text{Euler}}) )
$$

So, our algorithm is as follows:
1. Divide $[t_0, T]$ into $N$ subintervals with size $\Delta t = \frac{T - t_0}{N}$, where $t_k = t_0 + k \Delta t$.
2. Set $x^0 = x_0$. solve for the following.
3. For $k = 1, 2, \dots N$, 
   - We first perform Forward Euler. 
   - $s_1 = f(t_{k-1}, x^{k-1})$
   - $x^\text{Euler} = x^{k-1} + \Delta t s_1$
   - $s_2 = f(t_k, x^\text{Euler})$
   - $x^k = x^{k-1} + \frac{\Delta t}{2} (s_1 + s_2)$

> [!Info] RK-2 Takeaways
> - 2 evaluations of $f$ per step
> - Local truncation error of $O(\Delta t^3)$
> - Global error of $O(\Delta t^2)$ - second order.

So RK-2 is far more accurate than Forward Euler, but this comes at a cost! We need to do more computations to get this higher order.

We can generalize this to obtain higher orders! One of the most popular ODE integration schemes is RK-4, which has the following properties:
- 4 evaluations of $f$ per step.
- Local truncation error of $O(\Delta t^5)$
- Global error of $O(\Delta t^4)$

We state the algorithm below without proof.
1. Divide $t_0$ into $n$ equal intervals.
2. Set $x^0 = x_0$.
3. For $k = 1, 2, \dots N$,
   - $s_1 = f(t_k, x^{k-1})$
   - $s_2 = f(t_{k-1} + \frac{\Delta t}{2}, x^{k-1} + \frac{\Delta t}{2} s_1)$
   - $s_3 = f(t_{k-1} + \frac{\Delta t}{2}, x^{k-1} + \frac{\Delta t}{2} s_2)$
   - $s_4 = f(t_{k-1} + \frac{\Delta t}{2}, x^{k-1} + \frac{\Delta t}{2} s_3)$
   - $x^k = x^{k-1} + \frac{\Delta t}{6} (s_1 + 2s_2 + 2s_3 + s_4)$

# Stiff ODEs
Consider the ordinary differential equation
$$
\dot{x}(t) = f(t_1, x(t)) \qquad x(t_0) = x_0
$$

Assume the ODE is stable. In other words, $\exists $C_0 \le C_1 < 0$ such that
$$
C_0 \le f_x (t,x) \le C_1 < 0
$$

Then, applying methods like Forward Euler, we get solutions that are nice and bounded close to our ODE! 
$$
\Delta t \le \frac{2}{-C_0 - C_1}
$$

But what if the ODE is "too stable"? Then, $\Delta t$ needs to be **very small** for stability! 

This is known as a **stiff ODE**, where there are region in the solution where the solution might var rapidly, and require very small $\Delta t$ for stability.

$$
\dot{x}(t) = - 100 x \qquad x(0) = 1 \qquad t \in [0, 10]
$$
The exact solution to this is $x(t) = e^{-100t}$!

If $f_x (t,x) = -100$, with large time steps, we have large oscillations which are not very reflective of our actual solution! We need to make our time step small enough to aviod this.
