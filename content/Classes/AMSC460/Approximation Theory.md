---
title: Approximation Theory
tags:
- amsc460
---

In [[Interpolation]], we were given a set of points $\{(x_i,y_i)\}_{i=1}^n$, $y_i = f(x_i)$, and asked to construct a polynomial $P(x)$ exactly matching these points - more formally,
$$
P(x_i) = f(x_i) \qquad \forall 1 \le i \le n
$$

But this exact fit nature of interpolation isn't always the best! In the real world, error is inevitable, and our interpolation would fit these errors precisely! In practical applications, this can give us really poor predictions.

Below, we examine various ways we can approximate our functions from given datapoints.

# Approximating $f$ Given Noisy Data
## Problem Defined
Suppose we have noisy data. How can we create a function to best approximate this data?

In general, we can express our datapoints as
$$
y_i = f(x_i) + \epsilon_i
$$
Where $\epsilon_i$ is some sort of error offseting our true value.

Pick $m$ "known" set of functions $\{\phi_i(x)\}_{i=1}^m$. For constants $c_1, \dots c_m$, we want to find approximating function
$$
f(x) = c_1 \phi_1 (x) + c_2 \phi_2 (x) + \dots c_m \phi_m (x) = \sum_{i=1}^m c_j \phi_j (x)
$$
Matching our data for all $x \in I$.

Note that to determine $m$ unknowns, we need at least $m$ datapoints. However, in most situations, we'll have an **overdetermined situation**, where we have $> m$ data points, meaning we'll have more conditions than unknowns!

In such situations, it's not possible to find a "solution" that perfectly fits our data. Thus, we need some notion of best fit! Given our function $f$, we define the **residual error** at any datapoint $\{x_i,y_i\}$ to be
$$
r_i = f(x_i) - y_i = \sum_{j=1}^m c_j \phi_j (x_i) - y_i \qquad 1 \le i \le n
$$

This gives us a residual vector $r \in \mathbb{R}^n$
$$
r =
\begin{bmatrix}
    r_1 \\ r_2 \\ \vdots \\ r_n
\end{bmatrix}
$$

We want to find constants $\{c_j\}_{j=1}^m$ such that the magnitude of this residual vector is minimized (meaning we've minimized our residual error), given some norm $|| \cdot ||$.

This is known as the **Linear Least Squares Problem**! The solution is described below.

## Linear Least Squares Problem
Let $f$ be our approximating function. 

For all datapoints $\{x_i, y_i\}, 1 \le i \le n$, we have approximations given by
$$
\begin{align*}
    \tilde{y}_1 = &f(x_1) = c_1 \phi_1 (x_1) + c_2 \phi_2 (x_1) + \dots + c_m \phi_m (x_1) \\
    \tilde{y}_2 = &f(x_2) = c_1 \phi_1 (x_2) + c_2 \phi_2 (x_2) + \dots + c_m \phi_m (x_2) \\
    &\vdots
\end{align*}
$$

We can represent these approximations in the matrix form $Ac,$ where $A_{ij} = \phi_j (x_i)$, and $c$ is our constant vector.
$$
A =
\begin{bmatrix}
    \phi_1 (x_1) & \phi_2 (x_1) & \dots & \phi_m (x_1) \\
    \phi_1 (x_2) & \phi_2 (x_2) & \dots & \phi_m (x_2) \\
    \vdots & \vdots & & \vdots \\
    \phi_1 (x_n) & \phi_2 (x_n) & \dots & \phi_m (x_n)
\end{bmatrix}
\qquad
c = 
\begin{bmatrix}
    c_1 \\ c_2 \\ \vdots \\ c_m
\end{bmatrix}
$$

Now, given our vector of true datapoints $y = (y_1, y_2, \dots y_n)^T$, we can define our residual error in the matrix form
$$
r = Ac - y
$$

As mentioned before, we want to minimize the magnitude of this vector! We'll use the $l_2$ norm to minimize our error. How can we minimize $||r||_2 = \sqrt{\sum_{i=1}^n r_i^2}$?

Let's define a function $\epsilon(c)$, where $c$ are our constants as
$$
\begin{align*}
    \epsilon (c) 
    &= (||r||_2)^2 = \sum_{i=1}^n (r_i (c))^2 = (||Ac - y||_2)^2  \\
    &= (Ac - y)^T (Ac - y) = c^T A^T A c - 2 y^T A c + y^T y
\end{align*}
$$
> Note that when minimizing these distances, it's often the case we square the term to get rid of the square root.

We wish to find minimizing $c$, and to do this, we can find when our derivative is 0! Differentiating with respect to any $c_j$, we find
$$
\begin{align*}
    \frac{\partial \epsilon(c)}{\partial c_j} 
    &= \sum_{i=1}^n \frac{\partial}{\partial c_j} ( r_i (c)^2 ) = \sum_{i=1}^n 2 r_i (c) \frac{\partial r_i (c)}{\partial c_j} \\
    &= \sum_{i=1}^n 2 r_i \phi_j (x_i) = 2 (A_{1j} r_1 + A_{2j} r_2 + \dots A_{nj} r_n)
\end{align*}
$$

Continuing this for all $c_j$, we find that we want to find $c$ such that
$$
A^T r = 0
$$
Otherwise known as the **normal equations**.

We plug this back into our original equation to obtain
$$
\begin{align*}
    r = Ac - y \\
    A^T r = 0 = A^T (Ac - y) \\
    A^T A c = A^T r + A^T y \\
    A^T A c = (0) A^T y
\end{align*}
$$
This is a linear system that we can solve for $c$! 

Thus, our algorithm for solving the linear least squares problem is as follows:
1. First, construct $A$ from our $x_i$'s and $\phi_j$'s given.
2. Then, construct $M = A^T A$ and $b = A^T y$.
3. Finally, solve $Mc = b$.

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


# Approximating $f$ Given True $f$ 
## Problem Defined
Suppose we have a known function $f$, but it is really complicated. Thus, in practical applications, it may be worth approximating it with a cleaner solution. 

How can we create a polynomial of degree $\le N$ that best approximates our function?

In other words, given functions $\{\phi_i (x)\}_{i=0}^N$, we want to approximate $f$ as
$$
f(x) = c _1 \phi_1 (x) + c_2 \phi_2 (x) + \dots c_N \phi_N (x)
$$

How can we do this? 
> This is known as the **weighted least squares problem**.

## Weighted Least Squares Problem
### Linear Independence
Consider functions $\{\phi_i (x)\}_{i=0}^N$ that we want to approximate $f$ with. These functions are **linearly independent** if 
$$
c_0 \phi_0 (x) + c_1 \phi_1 (x) + \dots + c_N \phi_N (x) = 0
$$
is only possible for $c_0 = c_1 = \dots = c_N = 0$.

> [!Abstract] Theorem: Independence of Distinct Degrees
> If for $0 \le i \le N$, $\phi_i (x)$ is a polynomial of degree $= i$, then $\{\phi_i (x)\}_{i=0}^N$ is linearly independent on any $[a,b]$.

We furthermore define $\prod_{i=0}^N [a,b]$ as the set of all polynomials $P(x)$ on $[a,b]$ with degree $\le N$. We can use this to define what polynomials our functions can span.

> [!Abstract] Theorem: Linear Independence and Span
> Let $\{\phi_i\}_{i=0}^N$ be a set of linearly independent polynomials in $\prod_N [a,b]$. Then, **any polynomial** in $\prod_N [a,b]$ can be uniquely written as a linear combination of $\{\phi_i\}_{i=0}^N$.

### Weight Functions
We define $w(x)$ to be a **weight function** on $[a,b]$ if it is continuous and non-negative in $(a,b)$, and 
$$
\int_a^b w(x) dx > 0
$$
In other words, $w(x)$ has a positive max.

Given any weight function $w$, the **weighted $L^2$ norm** of some function $f$ on $[a,b]$ is defined as
$$
|| f ||_{2,w} = \sqrt{\int_a^b f^2 (x) * w(x)}
$$
> Note that if $w(x) = 1$, then our weighted $L^2$ norm is the same as a normal $L^2$ norm!

### Problem Solution
We can our weighted $L^2$ norm to get a measure of error / distance! 

Let $w(x)$ be a weight function, $f$ be the function we want to approximate. We want to construct a polynomial $P_N^*$ minimizing
$$
(|| f - P_N ||_{2,w})^2 = \int_a^b ( f(x) - P_N (x) )^2 w(x) dx
$$
Or in other words, the **weighted $L^2$ distance to $f$**. 

Let us have a set of polynomials $\{\phi_i (x)\}_{i=0}^N$ with $\deg(\phi_i) = i$. Then, given our earlier theorems, we guarantee that any $P_N (x) \in \prod_N [a,b]$ can be uniquely written as
$$
P_N (x) = c_0 \phi_0 (x) + \dots + c_N \phi_N (x) = \sum_{j=0}^N c_j \phi_j (x) 
$$
Meaning we can use this set of polynomials to construct our $P_N^*$ mentioned earlier. 

Thus, we want to find constants $c^* = [c_0^*, \dots, c_N^*]$ minimizing
$$
\epsilon(c) = \int_a^b \left( f(x) - \sum_{i=0}^N c_i \phi_i (x) \right)^2 w(x) dx 
$$

To find this minimum, we'll find where our derivative is equal to 0. For any $c_i$, we differentiate with respect to $c_i$ to get
$$
\begin{align*}
0 
&= \frac{\partial \epsilon(c)}{\partial c_i} \bigg\vert_{c = c^*} = -2 \int_a^b \left( \frac{\partial \epsilon(c)}{\partial c_i} f(x) - \frac{\partial \epsilon(c)}{\partial c_i} \sum_{j=0}^N c_j^* \phi_j (x) \right) \phi_i (x) w(x) dx \\ 
0 &= \sum_{j=0}^N \left[ c_j^* \int_a^b \phi_i (x) \phi_j (x) w(x) dx \right] 
\end{align*}
$$
> Note that we applied the chain rule here!

Continuing this for all $c_i$, we get a linear system of equations!
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

> [!Warning] Naive Solutions
> Making the simplest choice of $w(x) = 1$ and $\phi_i = x^i$, we can simplify this system of equations to
> $$
> \begin{align*}
> M_{ij} = \int_a^b x^{i + j} dx \\
> d_i = \int_a^b f(x) x^i
> \end{align*}
> $$
> 
> If $[a,b] = [0,1]$, we get matrix
> $$
> M = 
> \begin{bmatrix}
>     1/1 & 1/2 & \dots & 1/N \\
>     1/2 & 1/3 & & \vdots \\
>     \vdots  \\
>     1/(N+1) & \dots & & 1/(2N + 1)
> \end{bmatrix}
> $$
> known as a **Hilbert Matrix**. While this matrix is simple, it's really terrible for error, as it has a condition number that grows extremely fast! 

Is there another matrix we could use that's a better choice? 

Note that for any linear system, the easiest matrix we could use to solve it is a diagonal matrix. 

If we wanted this for our system, we'd need to define a set of functions $\{\phi_j\}_{j=0}^N$ that are **orthogonal** on $[a,b]$ with respect to $w(x)$. In other words,
$$
\int_a^b \phi_i (x) \phi_j (x) w(x) dx = 
\begin{cases}
    0 & i \ne j \\
    \alpha_i > 0 & i = j
\end{cases}
$$
We can furthermore say that these functions are **orthonormal** if the same conditions hold, but $\alpha_i = 1$. Note that we can convert any orthogonal set into an orthonormal set by taking
$$
\hat{\phi}_{j} (x) = \frac{\phi_j (x)}{\sqrt{\alpha_i}} = \frac{\phi_j (x)}{|| \phi_j ||_{2,w}}
$$

We can find such a set using the Gram-Schmidt process of orthonormalization! See the below example.

> [!Info] Gram-Schmidt Orthonormalization (Example)
> Suppose we have linearly independent set of functions $\{ \phi_0(x), \phi_1(x), \phi_2(x), \dots \phi_N(x) \}$. 
> 
> Find the corresponding orthonormal set of functions, given a weight function $w(x)$.
> 1. Start with $\hat{\phi}_0 (x)$.
> 2. Let $\hat{\phi}_1 (x) = \phi_1 (x)- \beta_1^0 \hat{\phi}_0 (x)$. Find $\beta_1^0$ such that
>    $$
>    \int_a^b \hat{\phi}_0 (x) \hat{\phi}_1 (x) w(x) = 0
>    $$
> 3. Let $\hat{\phi}_2 (x) = \phi_2 (x) - \beta_2^0 \hat{\phi}_0 (x) - \beta_2^1 \hat{\phi}_1 (x)$. Find $\beta_2^0$ and $\beta_1^0$ such that
>    $$
>    \begin{align*}
>    \int_a^b \hat{\phi}_2 (x) \hat{\phi}_0 (x) w(x) dx = 0 \\
>    \int_a^b \hat{\phi}_2 (x) \hat{\phi}_1 (x) w(x) dx = 0
>    \end{align*}
>    $$
> 4. ...
> 
> Continue this for all $\hat{\phi}_i (x)$ to obtain an orthogonal set. Finally, orthonormalize each function to finish!

If we choose a set of functions $\{\phi_j\}_{j=0}^N$ to be orthonormal, then $M$ becomes the identity matrix, giving us
$$
c_i^* = d_i = \int_a^b \phi_i (x) f(x) w(x) dx
$$

Which makes it super easy to find an approximation for $f$!

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

