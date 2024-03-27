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
