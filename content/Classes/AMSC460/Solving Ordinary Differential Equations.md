---
title: Solving Ordinary Differential Equations
tags:
- amsc460
---

# Ordinary Differential Equations (ODEs)
## Introduction
Let $(t_0, x_0) \in \mathbb{R} \times \mathbb{R}$ and consider an open rectangular neighborhood of $(t_0, x_0)$ 
$$
B = \{ (t,x) \in \mathbb{R} \times \mathbb{R} : t_0 - \delta < t < t_0 + \delta, x_0 - \epsilon < x < x_0 + \epsilon \}
$$

Let $f(t,x)$ be a function defined on this $(t,x)$ plane. Then, for all  $t \in [t_0, T]$, we have 
$$
x'(t) = f(t,x) \qquad x(t_0) = x_0
$$

This is an **ordinary differential equation (ODE)**! 
> Essentially, this creates a slope field, where the slope varies based on our position $x,t$!

Suppose we want to **solve this ODE**, or in other words, find the $x(t)$ satisfying the relation and initial condition.

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
>     &\frac{dx}{dt} = x^{1/3} &x^{-1/3} dx = dt \\
>     &\int_{x(0)}^{x(t)} y^{-1/3} dy = \int_0^t ds \\
>     &x(t) = \left( \frac{2t}{3} \right)^{3/2}
> \end{align*}
> $$
> 
> We can also show that
> $$
> x(t) = -\left( \frac{2t}{3} \right)^{3/2} \qquad x(t) = 0
> $$
> Are also solutions. Note that we do not have uniqueness, as the derivative of $x^{1/3}$ with respect to $x$ is not continuous!

Additionally, we have the following.

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

## Systems of Ordinary Differential Equations
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

Denote the Jacobian Matrix as
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
Then, we have the following.

> [!Abstract] Theorem: Unique Solutions
> If $f$ and $D_{\vec{x}} f$ are continuous in $B$, then there exists a unique solution to the system $\forall t \in [t_0, t^*)$, where $t_0 < t^* \le T$.

### Higher Order ODEs
Suppose we have a higher order system of ordinary differential equations
$$
\frac{d^m x(t)}{dt^m} = g \left(t, x(t), \frac{dx}{dt}, \dots, \frac{d^{m-1} x}{dt} \right)
$$
With initial values
$$
\frac{d^l x}{dt^l} (t_0) = x_{l,0} \qquad \forall l = 0, \dots, m - 1
$$

Then we can rewrite this as a first order system of ODEs! Define $y_i(t)$ as the following.
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
Solving ODEs can be hard! Here, we discuss how to iteratively approximate solutions to our ordinary differential equations.

## Forward Euler Method
### Algorithm
Suppose we want to solve the system
$$
\vec{x}'(t) = \vec{f}(t, \vec{x}) \qquad \vec{x}(t_0) = \vec{x}_0
$$

Notice that with a forward difference, we can actually approximate $x'(t)$ as
$$
x'(t) = \frac{x(t + \Delta t) - x(t)}{\Delta t} \Longrightarrow x(t + \Delta t) = x(t) + (\Delta t) f(t,x)
$$
So, it's possible to approximate nearby $x$ values by taking small incremental steps in the direction we want! 

So, our algorithm is as follows:
1. First, divide $[t_0, T]$ into $N$ equal sized subintervals given by
   $$
   t_k = t_0 + k \Delta t \qquad \Delta t = \frac{T - t_0}{N}
   $$
2. Then, let $x^0 = x_0$, our initial condition. 
3. Then, for all $k = 1, 2, \dots N$, we have
   $$
   \vec{x}^k = \vec{x}^{k-1} + (\Delta t) f(t_{k-1}, \vec{x}^{k-1})
   $$
4. Repeat this for all $k$. 

### Error
Let's find the error of this algorithm. At any step $k$, we can find our error as
$$
e^k = | x^k - x(t_k) |
$$
Where $x^k$ is our approximation, and $x(t_k)$ is our true value. Using the Taylor expansion about $t_k$, we can find
$$
\begin{align*}
x(t_{k+1}) 
&= x(t_k + \Delta t) \\
&= x(t_k) + x' (t_k) \Delta t + \frac{\Delta t^2}{2} x''(\epsilon_k)
\end{align*}
$$
We also know that we can find $x^{k+1}$ as
$$
x^{k+1} = x^k + \Delta t f(t^k, x^k)
$$
Combining these equations, we find 
$$
x^{k+1} - x(t_{k+1}) = (x^k - x(t_k)) + \Delta t [ f(t^k, x^k) - f(t_k, x(t_k)) ] - \frac{\Delta t^2}{2} x''(\epsilon_k)
$$
By the Mean Value Theorem, we can guarantee the $\exists n_k$ between $x^k$ and $x(t_k)$ such that
$$
\begin{align*}
f(t^k, x^k) - f(t_k, x(t_k)) = f_x (t_k, n_k) * (x^k - x(t_k)) \\
\Longrightarrow 
x^{k+1} - x(t_{k+1}) = (1 + \Delta t f_x (t_k, n_k) (x^k - x(t_k)) - \frac{\Delta t^2}{2} x''(\epsilon_k)
\end{align*}
$$

So, we find our error as 
$$
e^{k+1} \le \alpha_k e^k + r_k
$$
where
$$
\begin{align*}
    &\alpha_k = | 1 + \Delta t f_x (t_k, n_k) | &\text{Amplification Factor} \\
    &r_k = \frac{\Delta t^2}{2} |\ddot{x}(\epsilon_k)| &\text{Local Truncation Error}
\end{align*}
$$
Where **amplification factor** is the amount in which the previous error is amplified, and **local truncation error** is the additional error added from one step.

Let's analyze what this error means for us in different cases.

---

In the **general case**, assume that
- $| f_x (t,x) | \le C_1$ for all $t \in [t_0, T]$, $\forall x$
- $| x''(t) | \le C_2$ for all $t \in [t_0, T]$

Then, we can find our error as
$$
\begin{align*}
    &\alpha_k \le 1 + \Delta t C_1 = L
    &r_k \le \frac{\Delta t^2}{2} C_2 = M \\
    &\Longrightarrow e^{k+1} \le \alpha_k e^k + r_k \le Le^k + M
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
    &\le 0 + \left(\frac{L^k - 1}{L - 1} \right) M
\end{align*}
$$

Additionally, because $L > 1$, we have
$$
\begin{align*}
    &\le \frac{L^k M}{L - 1} = \frac{(1 + \Delta t C_1)^k}{\Delta t C_1} \frac{\Delta t^2}{2} C_2 \\
    &\le e^{\Delta t C_1 k} \frac{C_2}{2 C_1} \Delta t = e^{(t_k - t_0) C_1} \frac{C_2 \Delta t}{2 C_1}
\end{align*}
$$

Some key takeaways:
- As $T \to \infty$, our error will increase exponentially! 
- For a finite $T$, our error grows linearly, and is bounded by $O(\Delta t)$. Thus, for finite $T$, Forward Euler is a **first order method**. 

---

In the **special case**, assume that our ordinary differential equation is stable. In other words,
- $\exists C_0 \le C_1 < 0$ such that $C_0 \le f_x (t,x) \le C_1 < 0$, for all $t \in [t_0, T]$ and $\forall x$. 
- $| \ddot{x}(t) | \le C_2$ for all $t \in [t_0, T]$.

This gives us
$$
1 + \Delta t C_0 \le 1 + \Delta t f_x (t,x) \le 1 + \Delta t C_1 < 1
$$
Notice how as $\Delta t > 0$ becomes smaller, both bounds go to 1! As they'll have to cross 0 to do this, we can choose $\Delta t$ such that
$$
- (1 + \Delta t C_1) \le 1 + \Delta t C_0 \Longrightarrow \Delta t \le \frac{2}{-C_0 - C_1}
$$

Then, we have
$$
\begin{align*}
-1 < -(1 + \Delta t C_1) \le 1 + f_x (t,x) \Delta t \le 1 + \Delta t C_1 < 1 \\
\alpha_k \le 1 + \Delta t C_1 < 1
\end{align*}
$$

Let $L = 1 + \Delta t C_1$. Then, repeating the same process as the general case, we get 
$$
e^k \le \left(\frac{1 - L^k}{1 - L}\right) M \le -\frac{C_2}{2C_1} \Delta t
$$

Giving us a first order that is always bounded by a factor of our timstep $\Delta t$! Thus, our method is 1st order in this case as well.
> Note that for this to happen, we assumed stability condition $\Delta t \le \frac{2}{-C_0 - C_1}$. This **must** hold for us to get this error!

---

> [!Info] Forward Euler Takeaways
> - 1 evaluation of $f$ per step
> - Local truncation error of $O(\Delta t^2)$
> - Global error of $O(\Delta t)$ - first order.

> [!Abstract] Theorem: Local Truncation Error
> Let's take a closer look at the **local truncation error**. It not only represents the error from one time step of the algorithm, but also indicates the degree in which the true solution doesn't satisfy the algorithm.
> 
> To find the order $p$ of some method, we have
> - Local Truncation Error $O(\Delta t^{p+1})$
> - Global Error $O(\Delta t^p)$
> 
> So, for a second order method, we should try to get a local truncation error $O(\Delta t^3)$. How can we get such a method?

## Runge Kutta-2 (Multi-Step Methods)
The **Runge Kutta Method** describes multi-step methods we can use to solve systems of ordinary differential equations. Here, we will discuss **RK-2**.

Consider the system
$$
x'(t) = f(t, x) \qquad x(t_0) = x_0
$$

If we integrate our ordinary differential equation from $t_1 = t_0 + \Delta t$, we'll get
$$
x(t_1) = x(t_0) + \int_{t_0}^{t_1} f(t, x(H)) dt
$$

While we have $x(t_0)$ as an initial condition, we can't find $x(H)$! But what if we could approximate our integral instead?

Let $g(t) = f(t, x(H))$. Then, we can approximate our integral $I$ using a quadrature $Q_\Delta$ giving us a third order error.
$$
I = \int_{t_0}^{t_1} g(t) dt \qquad | I - Q_\Delta | \le C \Delta t^3 
$$

Let $Q_\Delta$ be the trapezoidal rule. Then, we have approximation
$$
I \approx Q_\Delta = \frac{g(t_1) + g(t_0)}{2} (t_1 - t_0) = \frac{f(t_0, x(t_0)) + f(t_1, x(t_1))}{2} (t_1 - t_0)
$$
> Note that this gives us error
> $$
> | I - Q_\Delta | \le \frac{\Delta t^3}{12} | g''(\epsilon) | = O(\Delta t^3)
> $$

But we're trying to solve for $x(t_1)$, so we don't know $f(t_1, x(t_1))$! So, let's use Forward Euler to approximate $x(t_1)$ in $Q_\Delta$ to get 
$$
\hat{Q}_\Delta = \frac{f(t_0, x(t_0)) + f(t_1, x^\text{1, Euler})}{2} (t_1 - t_0)
$$
> Recall that the error of this would be
> $$
> | x^\text{1, Euler} - x(t_1) | \le C \Delta t^2 = O(\Delta t^2)
> $$

Our **RK-2 scheme** is given as
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

---

Let's find our error. Using MVT, we can find an $n$ between $x(t_1)$, $x^\text{1, Euler}$ such that
$$
| f(t_1, x(t_1)) - f(t_1, x^\text{1, Euler}) | = | f_x (t_1, n) | \cdot | x(t_1) - x^\text{1, Euler} |
$$

Using this, we find error
$$
\begin{align*}
| I - \hat{Q}_\Delta | &= | I - Q_\Delta + Q_\Delta - \hat{Q}_\Delta | \\
&= | I - Q_\Delta | + | Q_\Delta - \hat{Q}_\Delta | \\
&\le C \Delta t^3 + \frac{\Delta t}{2} | f(t_1, x(t_1)) - f(t_1, x^\text{1, Euler}) | \\
&\le C \Delta t^3 + \frac{\Delta t}{2} | f_x (t_1, n) | C \Delta t^2
\end{align*}
$$

Assume that $| f_x (t,x) |$ is bounded. Then, our RK-2 scheme will have local truncation error $O(\Delta t^3)$!

> [!Info] RK-2 Takeaways
> - 2 evaluations of $f$ per step
> - Local truncation error of $O(\Delta t^3)$
> - Global error of $O(\Delta t^2)$ - second order.

So RK-2 is far more accurate than Forward Euler, but this comes at a cost! We need to do more computations to get this higher order.

### RK-4 Method
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
   - $s_4 = f(t_{k-1} + \Delta t, x^{k-1} + \Delta t s_3)$
   - $x^k = x^{k-1} + \frac{\Delta t}{6} (s_1 + 2s_2 + 2s_3 + s_4)$


# Stiff Ordinary Differential Equations
Consider the ordinary differential equation
$$
\dot{x}(t) = f(t_1, x(t)) \qquad x(t_0) = x_0
$$

Assume this ODE is stable. In other words, $\exists C_0 \le C_1 < 0$ such that
$$
C_0 \le f_x (t,x) \le C_1 < 0
$$

Then, applying methods like Forward Euler, we get solutions that are nice and bounded close to our ODE, granted $\Delta t$ is small enough! 
$$
\Delta t \le \frac{2}{-C_0 - C_1}
$$

But what if the ODE is "too stable"? In other words what if $C_0, C_1$ are too negative? Then, $\Delta t$ needs to be **extremely small** for stability! This is known as a **stiff ODE**, where there are region in the solution where the solution can vary rapidly, and require very small $\Delta t$ for stability.

> [!Example]+ Example: Stiff ODEs
> $$
> x'(t) = - 100 x \qquad x(0) = 1 \qquad t \in [0, 10]
> $$
> The exact solution to this is $x(t) = e^{-100t}$!
> 
> If $f_x (t,x) = -100$, with large time steps, we have large oscillations which are not very reflective of our actual solution! We need to make our time step small enough to aviod this.

Because of this, the methods we know aren't suited very well for Stiff ODEs! Here, we cover alternative methods built to solve these Stiff ODEs.

## Backward Euler (Implicit Euler)
Suppose we have the Stiff ODE
$$
x'(t) = f(t, x(t)) \qquad x(0) = x_0
$$
That is very stable. 

Recall that for Forward Euler, the ampliciation factor is given by
$$
\alpha_k = | 1 + \Delta f_x (t_k, n_k) | = 
\begin{cases}
    \le 1 &\Delta t \; \text{Small} \\
    > 1 &\Delta t \; \text{Large}
\end{cases}
$$
Where we approximate
$$
x'(t) \approx \frac{x(t + \Delta t) - x(t)}{\Delta t}
$$

For **Backward Euler**, we take the backward difference, finding
$$
x'(t) \approx \frac{x(t) - x(t - \Delta t)}{\Delta t}
$$
Giving us the scheme
$$
x^{k+1} = x^k + \Delta t f(t_{k+1} x^{k+1})
$$

Interestingly enough, with this scheme we have an $x^{k+1}$ that is given in terms of itself! If $f$ is linear, then we can solve the linear system of equations to isolate $x^{k+1}$. 
$$
\begin{align*}
    x'(t) = A x(t) \\ 
    x^{k+1} = x^k + \Delta A x^{k+1} \\
    (1 + \Delta t A) x^{k+1} = x^k
\end{align*}
$$
> If $f$ is non-linear, we need to apply a few steps of Newton's method to approximate $x^{k+1}$.

We can use this scheme like all of our other methods to approximate our solution!

---

Let's estimate our error. By Taylor expansion at $t_{k+1}$, we get
$$
\begin{align*}
x(t_k) 
&= x(t_{k+1} - \Delta t) \\
&= x(t_{k+1}) - \Delta t x' (t_{k+1}) + \frac{\Delta t^2}{2} x''(\epsilon_{k+1}) \\
x(t_{k+1}) 
&= x(t_k) + \Delta t f(t_{k+1}, x(t_{k+1})) - \frac{\Delta t^2}{2} x''(\epsilon_{k+1})
\end{align*}
$$

Subtracting our estimation from this, we get
$$
x^{k+1} = x^k + \Delta t f(t_{k+1}, x^{k+1})
$$
We get
$$
x^{k+1} - x(t_{k+1}) = x^k - x(t_k) + \Delta t (f(t_{k+1}, x^{k+1}) - f(t_{k+1}, x(t_{k+1}))) + \frac{\Delta t^2}{2} x''(\epsilon_{k+1})
$$

By MVT, we can guarantee the existence of some $n_{k+1}$ between $x^{k+1}$ and $x(t_{k+1})$ such that
$$
f(t_{k+1}, x^{k+1}) - f(t_{k+1}, x(t_{k+1})) = f_x (t_{k+1}, n_{k+1}) (x^{k+1} - x(t_{k+1}))
$$
We can sub this back into our above equation to get
$$
(1 - \Delta t f_x (t_{k+1}, n_{k+1})) (x^{k+1} - x(t_{k+1})) = x^k - x(t_k) + \frac{\Delta t^2}{2} x''(\epsilon_{k+1})
$$

We can find our error as
$$
\begin{align*}
e^k = | x^k - x(t_k) | \\
e^{k+1} = |1 - \Delta t f_x (t_{k+1}, n_{k+1}) | \le e^k + \frac{\Delta t^2}{2} |x''(\epsilon_{k+1})|
\end{align*} \\
e^{k+1} \le \frac{1}{\beta_{k+1}} e^k + \frac{\Delta t^2}{2 \beta_{k+1}} | x''(\epsilon_{k+1}) |
$$

So, we find that a local truncation error of $O(\Delta t^2)$, telling us that our method is **first order**! 

Let's check for what $\Delta t$ we need a stability condition. For a stable ODE where $C_0 \le C_1 < 0$, we have
$$
\begin{align*}
&C_0 \le f_x(t,x) \le C_1 < 0 \\
&1 < 1 - \Delta t C_1 \le 1 - \Delta t f_x (t,x) \le 1 - \Delta t C_0 \\
&0 < \frac{1}{1 - \Delta C_0} \le \frac{1}{1 - \Delta t f_x} \le \frac{1}{1 - \Delta t C_1} < 0
\end{align*}
$$

Assume $|x''(t)| \le C_2$. Then, we have
$$
r_{k+1} \le \frac{\Delta t^2}{2} C_2 L_\Delta := M_\Delta
$$
Where 
$$
L_\Delta = \frac{1}{1 - \Delta t C_1}
$$
To give us
$$
e^{k+1} \le L_\Delta e^k + M_\Delta \Longrightarrow e^{k} \le \frac{1 - L_\Delta^k}{1 - L_\Delta} M_\Delta \le \frac{M_\Delta}{1 - L_\Delta} = \frac{C_2}{-2 C_1} \Delta t
$$
Now, we have no condition on $\Delta t$! So, our error is **always** bounded, meaning our method is **unconditionally stable** for all $\Delta t$.
> Unlike Forward Euler, our stability holds for all $\Delta t$!

> [!Info] Key Takeaways (Implicit Euler)
> - Local truncation error of $O(\Delta t^2)$
> - Global error of $O(\Delta t)$
> - Stability of method for all $\Delta t$
