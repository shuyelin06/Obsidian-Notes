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
Pick $m$ "known" set of functions $\{\phi_i(x)\}_{i=1}^m$, and assume that for constants $c_1, \dots c_m$, we want to find approximating function
$$
f(x) = c_1 \phi_1 (x) + c_2 \phi_2 (x) + \dots c_m \phi_m (x) = \sum_{i=1}^m c_j \phi_j (x)
$$
For all $x \in I$.

Now suppose we are given noisy data $\{(x_i,y_i)\}_{i=1}^n$. Note that to determine $m$ unknowns, we need $n \ge m$. However, if we have $n > m$, which is typically the case, we have an **overdetermined situation**, where we have more conditions than unknowns.

Because of this, we need some notion of "best fit"! Given our function $f(x)$, we define the residual error at $x_i$ to be
$$
r_i = f(x_i) - y_i = \sum_{i=1}^m c_j \phi_j (x_i) - y_i \qquad \forall 1 \le 1 \le n
$$
Giving us a residual vector  $r = [r_1, r_2, \dots r_n]^T \in \mathbb{R}^n$. We want to find constants $\{c_j\}_{j=1}^m$ such that this residual vector has as small of a magnitude as possible, given some norm $|| \cdot ||$.

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
Which is a linear system we can solve for $c$! 

> [!Info] Linear Least Squares Problem
> To solve a given linear least squares problem, we:
> 1. Construct $A$ from our $x_i$'s and $\phi_j$'s given
> 2. Construct $M = A^T A$ and $b = A^T y$
> 3. Solve $Mc = b$
> 
> > Typically, we want to solve the normal equations ourselves, as solving them on a computer can lead to a highly unstable algorithm!

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

-- 3/26/24 --- 

# Approximating f when f is known
Suppose we have a known function $f$. We want to find a polynomial $P_N (x)$ of degree $\le N$ such that $P_N (x)$ is a "good" approximation of $f(x)$ on $[a,b]$.
> This may be useful in cases where $f$ is extremely complex, and an approximation could significantly simplify it.

Suppose we have functions $\{\phi_i (x)\}_{i=0}^N$. These functions are **linearly independent** if 
$$
c_0 \phi_0 (x) + c_1 \phi_1 (x) + \dots + c_N \phi_N (x) = 0
$$
is only possible for $c_0 = c_1 = \dots = c_N = 0$.

> [!Abstract] Theorem
> If for $0 \le i \le N$, $\phi_i (x)$ is a polynomial of degree $= i$, then $\{\phi_i (x)\}_{i=0}^N$ is linearly independent on any $[a,b]$.

Furthermore, we define $\prod_{i=0}^N [a,b]$ as the set of polynomials $P(x)$ on $[a,b]$ with degree $\le N$.

> [!Abstract] Theorem
> Let $\{\phi_i\}_{i=0}^N$ be a set of linearly independent polynomials in $\prod_N [a,b]$. Then, **any polynomial** in $\prod_N [a,b]$ can be uniquely written as a linear combination of $\{\phi_i\}$

We further define $w(x)$ to be a **weight function** on $[a,b]$ if it is continuous and non-negative in $(a,b)$ and 
$$
\int_a^b w(x) dx > 0
$$
In other words, $w(x)$ has a positive max.

Given a weight function $w$, the **weighted $L^2$ norm** of a function $f$ on $[a,b]$ is defined as
$$
|| f ||_{2,w} = \sqrt{\int_a^b f^2 (x) * w(x)}
$$
> Note that if $w(x) = 1$, then our weighted $L^2$ norm is the same as a normal $L^2$ norm!

Given $f$ on $[a,b]$ and a weight function $w(x)$ on $[a,b]$, we wish to find $P_N^* (x) \in \prod_N [a,b]$ such that $P_N^*$ minimizes 
$$
|| f - P_N ||_{2,w}^2 = \int_a^b ( f(x) - P_N (x) )^2 w(x) dx
$$
Or in other words, the **weighted $L^2$ distance to $f$**. This is known as the **weighted least squares problem (when $f$ is known)**.

The below theorems let us find such a polynomial.
> [!Abstract] Theorem
> If for $0 \le i \le N$, $\phi_i (x)$ is a polynomial of degree $= i$, then $\{\phi_i (x)\}_{i=0}^N$ is linearly independent on any $[a,b]$.

> [!Abstract] Theorem
> Let $\{\phi_i\}_{i=0}^N$ be a set of linearly independent polynomials in $\prod_N [a,b]$. Then, **any polynomial** in $\prod_N [a,b]$ can be uniquely written as a linear combination of $\{\phi_i\}$

Let us choose a set of polynomials $\{\phi_i (x)\}_{i=0}^N$ with $\deg(\phi_i) = i$. Then, any $P_N (x) \in \prod_N [a,b]$ can be uniquely written as
$$
P_N (x) = c_0 \phi_0 (x) + \dots + c_N \phi_N (x) = \sum_{j=0}^N c_j \phi_j (x) 
$$

Thus, our problem now is as follows. Given $f$, $w$, and $\{\phi_i (x)\}_{i=0}^N$, we wish to find $c^* = [c_0^*, \dots, c_N^*]$ such that $c^*$ minimizes
$$
\epsilon(c) = \int_a^b ( f(x) - \sum_{j=0}^N c_j \phi_j (x) )^2 w(x) dx 
$$

At this minimum, we know that
$$
0 = \frac{\partial \epsilon(c)}{\partial c_i} \bigg\vert_{c = c^*}
$$

By the Leibniz Integral Rule, we know our integral in $\epsilon(c)$ doesn't depend on $c$, so we can just directly differentiate the term inside!

$$
\begin{align*}
0 
&= \frac{\partial \epsilon(c)}{\partial c_i} \bigg\vert_{c = c^*} = -2 \int_a^b \left( f(x) - \sum_{j=0}^N c_j^* \phi_j (x) \right) \phi_i (x) w(x) dx \\ 
&= \sum_{j=0}^N \left[ c_j^* \int_a^b \phi_i (x) \phi_j (x) w(x) dx \right] 
\end{align*}
$$
This gives us a linear system of equations in $c^*$!
$$
Mc^* = d
$$
where
$$
\begin{align*}
M_{ij} = \int_a^b \phi_i (x) \phi_j (x) w(x) dx \\
d_i = \int_a^b f(x) \phi_i (x) w (x)
\end{align*}
$$

Making the simplest choice of $w(x) = 1$ and $\phi_i = x^i$, we can simplify this to
$$
\begin{align*}
M_{ij} = \int_a^b x^{i + j} dx \\
d_i = \int_a^b f(x) x^i
\end{align*}
$$

If $[a,b] = [0,1]$, we get matrix
$$
M = 
\begin{bmatrix}
    1/1 & 1/2 & \dots & 1/N \\
    1/2 & 1/3 & & \vdots \\
    \vdots  \\
    1/(N+1) & \dots & & 1/(2N + 1)
\end{bmatrix}
$$
known as a **Hilbert Matrix**. While this matrix is simple, it's really bad for error, as it has a condition number that grows extremely fast! 

So, is there another matrix we could use that's a better choice? 

The best (easiest) matrix we could use for any linear system is a diagonal matrix. If we wanted to do this, we'd need $\phi_i (x) \cdot \phi_j (x) = 0$ for any $i \ne j$. 

To do this, we define the set of functions $\{\phi_j\}_{j=0}^N$ as **orthogonal** on $[a,b]$ with respect to $w(x)$ if
$$
\int_a^b \phi_i (x) \phi_j (x) w(x) dx = 
\begin{cases}
    0 & i \ne j \\
    \alpha_i > 0 & i = j
\end{cases}
$$
Furthermore, we say they are **orthonormal** if $\alpha_i = 1$. We can convert any orthogonal set into an orthonormal set by taking
$$
\hat{\phi}_{j} (x) = \frac{\phi_j (x)}{\sqrt{\alpha_i}} = \frac{\phi_j (x)}{|| \phi_j ||_{2,w}}
$$
We can find such a set using the Gram-Schmidt process of orthonormalization!

---

Starting from $\{1, x, x^2, \dots x^n\}$, find an orthogonal set given a weight function $w(x)$
1. Set $\phi_0 (x) = 1$.
2. Let $\phi_1 (x) = x - \beta_1^0 \phi_0 (x) = x - \beta_1^0$ where we find $\beta_1^0$ such that
   $$
   \beta_1^0 = \int_a^b \phi_0 (x) \phi_1 (x) w(x) \Longrightarrow \beta_1^0 = \frac{\int x w(x) dx}{\int w(x) dx}
   $$
3. Let $\phi_2 (x) = x^2 - \beta_2^0 \phi_0 (x) - \beta_2^1 \phi_1 (x)$ where we find $\beta_2^0$ and $\beta_1^0$ as
   $$
   \begin{align*}
   \int_a^b \phi_2 (x) \phi_0 (x) w(x) dx = 0 \\
   \int_a^b \phi_2 (x) \phi_1 (x) w(x) dx = 0
   \end{align*}
   $$
   This gives us a linear system
   $$
   \begin{align*}
       \beta_2^0 \int_a^b w(x0 dx + \beta_2^1 \int_a^b \phi_1 (x) w (x) dx = \int_a^b x^2 w(x) dx \\
       \beta_2^0 \int_a^b \phi_1 (x) w(x) dx + \beta_2^1 \int_a^b \phi_1 (x)^2 w(x) dx = \int_a^b x^2 \phi_1 (x) w(x) dx
   \end{align*}
   $$


---

If we choose a set of functions $\{\phi_j\}_{j=0}^N$ to be orthonormal, then $M$ becomes the identity matrix, giving us
$$
c_i^* = d_i = \int_a^b \phi_i (x) f(x) w(x) dx
$$

Some important examples of these orthonormal polynomials are given as follows:
- The **Legendre Polynomials**: Given $w(x) = 1$, and applying Grahm Schmidt on $[-1,1]$, we have
  $$
  \phi_0 (x) = 1 \\
  \phi_1 (x) = x \\
  \phi_{n+1} (x) = {(2n + 1) x \phi_n (x) - n \phi_{n-1} (x)}{n + 1} \qquad \forall n \ge 1
  $$
  
  with $L^2$ norm given as
  $$
  || \phi_n ||_{2,w} = \sqrt{\frac{2}{2n + 1}}
  $$
- The **Chebyshev Polynomials**: Given $w(x) = \frac{1}{\sqrt{1 - x^2}}$ on $[-1, 1]$, we get 
  $$
  \phi_0 (x) = 1 \\
  \phi_1 (x) = x \\
  \phi_{n+1} = 2x \phi_n (x) - \phi_{n-1} (x) \qquad \forall n \ge 1
  $$
  With $L^2$ norm given as
  $$
  || \phi_n ||_{2,w} = \begin{cases}
      \sqrt{\pi} & n = 0 \\
      \sqrt{\frac{\pi}{2}} & n \ne 0 
  \end{cases}
  $$


--- New Chapter ----


# Nonlinear Functions

# Root Finding Algorithms
Consider the function $f(x) = ax^2 + bx + c$. Suppose we want to find its root, i.e. $x^*$ such that $f(x^*) = 0$. Note that we can easily find this using the **quadratic formula**
$$
x^* = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}
$$

What if we had $f(x) = \sin(x) - e^{-x}$? Now our example is too complicated!

This section describes, given a non-linear function, how do we find the roots of these functions? We discuss **root-finding algorithms** that can do this for us! Notes:
- These algorithms are iterative, giving us a sequence of approximations $x_n \to x^*$.
- The roots $x^*$ we find are NOT guaranteed to be unique, and the $x^*$ we converge to will depend on an initial guess $x_0$!

> [!Abstract] Theorem: 
> If $f$ is continuous on $[a,b]$, and $k$ is a value between $f(a)$ and $f(b)$, then there exists some $c \in (a,b)$ such that $f(c) = k$.

> [!Info] Corollary
> If $f$ is a continuous function on $[a,b]$ and $f(a) f(b) < 0$, then $\exists c \in (a,b)$ such that $f(c) = 0$.

## Bisection Algorithm
Assume $f$ is continuous. Pick $a_0$ and $b_0$ such that $f(a_0) f(b_0) < 0$. Note that by our corollary, we are guaranteed the existence of a root between $a_0$ and $b_0$.

Then, for each step $n = 0, 1, 2, \dots$,
1. Define the midpoint, $c_n = \frac{a_n + b_n}{2}$.
2. Then, we check the following cases.
   - If $f(c_n) = 0$, we have found our root and stop!
   - If $f(c_n) f(a_n) < 0$, then pick the next interval $[a_{n+1}, b_{n+1}] = [a_n, c_n]$ and repeat (1).
   - If $f(c_n) f(b_n) < 0$, then pick the next interval $[a_{n+1}, b_{n+1}] = [c_n, b_n]$ and repeat (1).

As we have our interval's size (about the root) every iteration, it should intuitively converge! The following theorem guarantees this.

> [!Abstract] Theorem: Convergence of the Bisection Algorithm
> Let $f$ be a continuous function on $[a_0, b_0]$ and $f(a_0) f(b_0) < 0$. Then,
> $$
> \lim_{n \to \infty} a_n = \lim_{n \to \infty} b_n = x^*
> $$
> 
> Where $f(x^*) = 0$.

How fast (efficient) is this algorithm? Well, note that because $c_n = \frac{a_n + b_n}{2}$, and $x^* \in [a_n, b_n]$,
$$
|c_n - x^*| \le \frac{1}{2} (b_n - a_n)
$$
and furthermore,
$$
\begin{align*}
| c_{n+1} - x^* | &\le \frac{1}{2} ( b_{n+1} - a_{n+1} ) \\
    &\le \frac{1}{4} (b_n - a_n)
\end{align*}
$$
Define $E_n = \frac{1}{2} (b_n - a_n)$. Any given  method is said to **converge with order $p$** if for some constant $c$,
$$
E_{n+1} \le c E_n^p
$$
So for our bisection, we converge with order $p = 1$ (linearly) and $c = 1/2$.


## Newton's Method
Assume $f$ has at least one real root. Additionally, assume $f$ is differentiable.

1. Start with an initial "guess" $x_0$, and let $l(x)$ be the tangent to $f$ at $x_0$.
   $$
   l(x) - f(x_0) = f'(x_0) (x - x_0)
   $$
   Let $x_1$ be the x-intercept of $l(x)$, 
   $$
   x_1 = x_0 - \frac{f(x_0)}{f'(x_0)}
   $$
2. Start with $x_1$, and let $l(x)$ be the new tangent line to $f$ at $x_1$. Similarly, pick $x_2$ to be the x-intercept of this line.
   $$
   x_2 = x_1 - \frac{f(x_1)}{f'(x_1)}
   $$
3. Continuing this, given any $x_n$, we can find $x_{n+1}$ as
   $$
   x_{n+1} = x_n - \frac{f(x_n)}{f'(x_n)}
   $$

> Note that at each step, we're essentially making a linear approximation of $f$, and using its root!

We can find the convergence rate of this method to be quadratic, which is faster than our previous method!
$$
E_n \le c E_n^2
$$

However, there's a major trade-off - there's no guarantee that Newton's Method converges, depending on our choice of $x_0$! Only if the following properties hold, can we guarantee convergence.

> [!Abstract] Theorem: Global Convergence of Newton's Method
> Let $f$ have the following properties:
> - $f$ has 2 continuous derivatives
> - $f$ is strictly monotone increasing, i.e. $f'(x) > 0$
> - $f$ is convex, i.e. $f''(x) > 0$
> - $f$ has to have a root $x^*$
> 
> Then, $x^*$ is unique, and Newton's method will converge to $x^*$ for any initial $x_0$ (known as **global convergence**).

Otherwise, for localized convergence, we need that
1. $f$ has 2 continuous derivatives.
2. $f'(x^*) \ne 0$ at the root $x^*$.
3. Our initial guess $x_0$ is close enough to $x^*$.

### Secant Method
We can also modify Newton's method to be the formula
$$
x_{n+1} = x_n - \frac{f(x_n) (x_n - x_{n-1})}{f(x_n) - f(x_{n-1})}
$$

Known as the **secant method**, which, instead of using the tangent line, essentially finds the $x$-intercept of the line passing through $(x_{n-1}, f(x_{n-1})), (x_n, f(x_n))$. 

This method doesn't require us to know $f$'s derivatives! However, this method also has an order 
$$
p = \frac{\sqrt{5} + 1}{2}
$$ 
which is between 1 and 2 (known as being **super-linear**). This makes the secant method more efficient than bisection, but less than Newton's!

## Hybrid Methods
Newton's is fast, but does not guarantee convergence, whereas Bisection guarantees convergence, but is slow. Could we reap the benefits of both?

This is the point behind a **hybrid approach**, where we alternative between using bisection with a secant-type method together! We will use the secant-type method until it stops working, then switch to bisection!
> This is in fact, what MatLab does when we call the function `fzero()`!


# Non-Linear Systems of Equations
Let us consider $m$ equations in $n$ unknowns
$$
\begin{align*}
&x = [x_1, x_2, \dots x_n]^T \in \mathbb{R}^N \\
&f_j : \mathbb{R}^N \to \mathbb{R} \\
&f(x) = 
\begin{bmatrix}
    f_1 (x_1, x_2, \dots x_n) \\
    f_2 (x_1, x_2, \dots x_n) \\
    \vdots \\
    f_n (x_1, x_2, \dots x_n)
\end{bmatrix} \in \mathbb{R}^m
\end{align*}
$$

Suppose we want to find $x^*$ such that $f(x^*) = 0$. How can we do this?
> In the case that there exists no such $x^*$, we find the $x^*$ MINIMIZING this norm!!!

We may be able to do this using a process similar to Newton's Method! Define the **Jacobian Matrix** as $D_f (x) \in \mathbb{R}^{m \times n}$ such that
$$
D_f (x) = 
\begin{bmatrix}
    \frac{\partial f_1 (x)}{d x_1} & \dots & \frac{\partial f_1}{\partial x_n} (x) \\
    \vdots & & \vdots \\
    \frac{\partial f_m (x)}{d x_1} & \dots & \frac{\partial f_m (x)}{d x_n}
\end{bmatrix}
$$


1. Look at the case where $m = n$. Then, we have the following Taylor expansion of $f : \mathbb{R}^n \to \mathbb{R}^n$ about $x_0$:
   $$
   f(x) = f(x_0) + D_f (x_0) (x - x_0) + R(x)
   $$

    Where $R(x)$ is a remainder based on the Taylor Remainder Theorem. Say we want to solve to obtain 0.
    $$
    D_f (x) (x - x_0) = - f(x_0) \\
    \Longrightarrow A \delta x_0 = b
    $$

    So, given an initial guess $x^0$, for $k = 0, 1, 2, \dots$
    1. Evaluate $A^k = D_f (x^k)$.
    2. Evaluate $b^k = -f(x^k)$.
    3. Solve for $\delta x^k$ satisfying
       $$
       A^k \delta x^k = b^k
       $$
    4. 
       Set $x^{k+1} = x^k + \delta x^k$.

> In MATLAB, we can actually do this process through the function `fsolve()`!

> [!Abstract] Theorem: Convergence
> Assume there is a root $f(x^*) = 0$. Then suppose the following properties hold:
> - $f$ is continuous on two derivatives, on some neighborhood $B$ around $x^*$.
> - The Jacobian at $x^*$, $D_f (x^*)$, is invertible.
> 
> Then, $\exists \delta > 0, c > 0$ such that for all guesses sufficiently close, $|| x^0 - x^* ||_\infty \le \delta$, we have
> - Convergence is guaranteed; $\lim_{k\to\infty} x^k \to x^*$
> - Our convergence is quadratic; $|| x^{k+1} - x^* ||_\infty \le C || x^k - x^* ||_\infty^2$

2. Let's now look at the case where $m > n$. In this case, as we have more equations than unknowns, we may not have a solution! So, we instead want to find an $x^*$ that minimizes our problem. This is known as the **Gauss-Newton Algorithm**.
   $$
   x^* = \argmin_{x \in \mathbb{R}^n} || f(x) ||_2^2
   $$
   
   So, writing our Taylor Remainder theorem, we have
   $$
   \begin{align*}
   f(x) &\approx f(x^k) + D_f (x^k) (x - x^k) \\
   &= -b^k + A^k \delta x^k
   \end{align*}
   $$
   
   But this may not have a solution! So, if we apply our iterative method, we get the following. Take $x^0 \in \mathbb{R}^n$. Then, for $k = 0, 1, 2, \dots$,
   1. Evaluate $A^k = D_f (x^k)$
   2. Evaluate $b^k = f(x^k)$
   3. Solve $\delta x^k = \argmin_{\delta x \in \mathbb{R}^n} || A^k \delta x - b^k ||_2^2$. This is equivalent to solving our minimization problem (see above)
      $$
      (A^k)^T A^k \delta x^* = (A^k)^T b^k
      $$
   4. Add $x^{k+1} = x^k + \delta x^k$.

Our errors estimate on this algorithm is
$$
|| x^{k+1} - x^* ||_2 \le C ( || f(x^*) ||_2 \cdot || x^k - x^* ||_2 + || x^k - x^* ||_2^2 )
$$

This is comparing our new error every $x^{k+1}$ to our old error! We get quadratic convergence if $|| f(x^*) || = 0$, which is not usually true!

If $\epsilon = || f(x^*) ||_2$ is small, then you initially have **quadratic decay**, but once $|| x^k - x^* ||_2 \approx \epsilon$, then decay becomes linear, as we can no longer ignore the $|| f(x^*) ||_2 \cdot || x^k - x^* ||_2$ term.



--- END OF CHAPTER ---

# Numerical Differentiation (Derivative Approximations)
In many practical applications, we may want the derivative of a function $f$, without evaluating the true expression for $f'(x)$. This may occur because:
- The true expression for $f'(x)$ is extremely complicated, or expensive to compute!
- We only have points for $f$ - $\{ (x_i, f(x_i) ) \}$, so we don't even have an expression for $f$ to compute a derivative with!

How can we find such derivatives?

Recall that 
$$
f'(x) = \lim_{h \to 0} \frac{f(x+h) - f(x)}{h}
$$
If $h > 0$ and is very small, we approximately have that
$$
f'(x) \approx \frac{f(x + h) - f(x)}{h}
$$
By the Taylor Remainder Theorem of $f(x + h)$ about $x$, we have that for some $z \in (x, x + h)$,
$$
\begin{align*}
    f(x + h) 
    &= f(x) + f'(x) \cdot h + \frac{f''(x)}{2!} h^2 + \frac{f'''(x)}{3!} h^3 + \frac{f'''(z)}{4!} h^4 \\
    f'(x) 
    &= \frac{f(x + h) - f(x)}{h} - \frac{f''(x)}{2!} h - \frac{f'''(x)}{3!} h^2 -  \frac{f'''(z)}{4!} h^3 \\
    f'(x) 
    &= \frac{f(x + h) - f(x)}{h} + \text{Er(h)}
\end{align*}
$$
Where $\text{Er(h)}$ is the error value on $h$, which converges to 0 as h becomes small. In particular, this method is known as a $p^{th}$ order method, where $p$ is the leading power term (lowest exponent) of $h$ in $\text{Er(h)}$, as the lowest exponent will contribute the most.
> We say the rate of convergence is $p$ if $\text{Er}(h) = O(h^p)$

This essentially approximates our derivative from the left-hand side, known as the **forward difference**! 

We similarly have a **backward difference**,
$$
f'(x) = \frac{f(x) - f(x - h)}{h} + \text{Err(h)}
$$
which essentially approximates our derivative from the right-hand side.

Finally, we have a **central difference**,
$$
f'(x) = \frac{f(x+h) - f(x-h)}{2h} + \text{Er}(h)
$$
We can prove that this error term is $O(h^2)$, meaning it's a 2nd order method!

We also can find a **central difference for $f''$** as 
$$
f''(x) = \frac{f(x+h) - 2f(x) + f(x-h)}{h^2} + \text{Er}(h)
$$
Where this error term is $O(h^2)$, meaning it's a second order method!

In general, we have $k \in \mathbb{R}$, $z \in (x, x + kh)$
$$
f(x + kh) = f(x) + f'(x) \frac{(kh)}{1!} + f''(x) \frac{(kh)^2}{2!} + f'''(x) \frac{(kh)^3}{3!} + f''''(z) \frac{(kh)^4}{4!}
$$

---

How can we use these formulas to actually approximate our derivatives? There are many methods, but the one we will focus on is the **method of undetermined coefficients**!

Given the values of $f$
$$
\{ f(x + k_i h) \}_{i=1}^n
$$
Where $k_i \in \mathbb{R}$ and $i \ne j \to k_i \ne k_j$, find a linear combination of these values to approximate some derivative $f^r (x)$.

> [!Example] 
Say we want to approximate $f''(x)$ using a linear combination of $f(x - h), f(x), f(x + h)$. Then, we can approximate it as
$$
f''(x) = c_1 f(x-h) + c_2 f(x) + c_3 f(x+h) = L(h)
$$

We expand each using their Taylor Expansions (performed above) to obtain
$$
\begin{align*}
    L(h) 
    &= c_1 \left[ f(x) - f'(x) h + \frac{f''(x)}{2!} h^2 - \frac{f'''(x)}{3!} h^3 + \frac{f''''(z_1)}{4!} h^4 \right] \\
    &+ c_2 f(x) \\
    &+ c_3 \left[ f(x) + f'(x) h + \frac{f''(x)}{2!} h^2 + \frac{f'''(x)}{3!} h^3 + \frac{f''''(z_2)}{4!} h^4 \right] \\
    &= (c_1 + c_2 + c_3) f(x) + (-c_1 + c_3) h f'(x) + (c_1 + c_3) \frac{h^2}{2} f''(x) \\
    &+ (-c_1 + c_3) \frac{h^3}{3!} f'''(x) + (c_1 f''''(z_1) + c_3 f''''(z_2)) \frac{h^4}{4!}
\end{align*}
$$
We now attempt to find $c_1, c_2, c_3$ necessary to find our answer. As we want our second derivative, we want to drop our $f$ and $f'$ terms to 0, but keep the $f''$ term!
$$
\begin{align*}
    c_1 + c_2 + c_3 &= 0 \\
    -c_1 h + c_3 h &= 0 \\
    c_1 \frac{h^2}{2} + c_3 \frac{h^2}{2} &= 1
\end{align*}
$$
We solve this as
$$
c_1 = c_3 = \frac{1}{h^2} \qquad c_2 = -\frac{2}{h^2}
$$
Subbing this back into our equation, we get
$$
f''(x) = \frac{f(x - h) - 2f(x) + f(x + h)}{h^2} + O(h^2)
$$
Which we can use to approximate our $f''(x)$ value!
