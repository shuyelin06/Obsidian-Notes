---
title: AMSC460Working
tags:
- amsc460
- wip
---

# Interpolation and Polynomial Approximations
## Motivation
Consider a function $f(x)$ defined along the interval $[a,b]$. While we may be able to calculate it by hand, in practice, computers are unable to calculate all possible types of functions - and in these cases, it's necessary to approximate the function $f(x)$.

A common way to do this is by approximating $f(x)$ using a polynomial
$$
P_n (x) = a_0 + a_1 x + a_2 x^2 + a_3 x_3 + \dots + a_n x^n
$$
As the existence of these polynomials is guaranteed, granted we have continuity (see below).

> [!Abstract] Theorem: Weierstrass Approximation
> If $f$ is a function that is continuous on the interval $[a,b]$, then for any $\epsilon > 0$, there exists a polynomial $P(x)$ such that for all $x \in [a,b]$,
> $$
> | f(x) - P(x) | < \epsilon
> $$
> In other words, there exists a polynomial that can become infitesminally close to our function $f(x)$.

One of the most popular polynomial approximations out there is the **Taylor Series approximation**. 

Supposing that $f$ is differentiable $n$ times, then its Taylor Series approximation about $x_0$ is given as 
$$
f(x) \approx P_n (x) = f(x_0) + f'(x_0) (x - x_0) + \dots + f^n (x_0) \frac{(x - x_0)^n}{n!}
$$

This approximation is good, but is typically only used for error estimation, as it has a few issues.
- This approximation requires $f$ to be differentiable $n$-times, limiting the functions we can approximate.
- This approximation is only good for approximations around $x_0$!

Below, we explore alternative, more practical ways to approximate $f$.

## The Interpolation Problem
### The Interpolation Property
One way we can approximate functions is by using **interpolation**.

Given $(n + 1)$ distinct nodes $\{x_i\}_{i=0}^n$ along the function's domain, interpolation aims to find a polynomial $P_n(x)$ such that for all $0 \le i \le n$,
$$
P_n (x_i) = f(x_i)
$$
In other words, the polynomial guarantees equality at all points $x_i$, and approximates the function elsewhere. Such a function is said to satisfy the **interpolation property**.

This polynomial must have the minimum degree needed to achieve this. This gives us some notion of uniqueness for interpolating polynomials - otherwise, without this restriction, we could construct infinitely many polynomials that interpolate $f$.
> We typically want to minimize our degree, so we can minimize error with our approximation.

> [!Example]+ Example: Non-Uniqueness of Interpolators
> Let $P_n (x)$ have the interpolating property. Then, we can create a polynomial of higher degree with the same interpolating property.
> $$
> Q_n (x) = P_n (x) + \prod_{i=0}^n (x - x_i)^{v_i} \qquad v_i \ge 1
> $$
>
> This argument could be repeatedly applied to obtain higher and higher degrees!

The following theorem sets an upper bound on the degree needed for such a polynomial.

> [!Abstract] Theorem: Interpolation - Maximum Degree Needed
> If $\{x_i\}_{i=0}^n$ are $(n + 1)$ distinct nodes, then for any set of $(n + 1)$ values $f(x_0), f(x_1), \dots f(x_n)$, there exists a **unique** polynomial $P_n(x)$ with degree $\le n$ such that the interpolation property holds.

How can we explicitly construct such polynomials?

### Lagrange Interpolating Polynomials
One way we can explicitly construct such polynomials is by using the **Lagrange Interpolating Polynomial**.

Suppose we have $\{ x_i \}_{i=0}^n$ distinct nodes. Then, for any $0 \le j \le n$, define the polynomial
$$
l_j (x) = \frac{(x - x_0) (x - x_1) \dots (x - x_{j-1}) (x - x_{j+1}) \dots (x - x_n)}{(x_j - x_0) (x_j - x_1) \dots (x_j - x_{j - 1}) (x_j - x_{j + 1}) \dots (x_j - x_n)}
$$
> Note how we don't include the $(x - x_j)$ and $(x_j - x_j)$ terms.

By this definition, we know that given any $l_j$ polynomial, called the **basis polynomials**, for any $0 \le i \le n$,
$$
l_j (x) = 
\begin{cases}
    0 & i \ne j \\
    1 & i = j
\end{cases}
$$
And furthermore, the degree of each $l_j$ polynomial is $n$.

Summing the $l_j$ polynomials, we can obtain the **Lagrange Polynomial**.
$$
P_n (x) = \sum_{j=0}^n f(x_j) l_j (x)
$$
Which, by property of the basis functions, is guaranteed to be equal to $f(x_j)$ at $x = x_j$ (all other basis functions will drop to 0 except the $l_j$ function).

> [!Example]+ Example: Lagrange Interpolating Polynomials 
> Let $x_0 = 2, x_1 = 3, x_2 = 5$, and let $f = 1/n$. We find
> $$
> f(x_0) = \frac{1}{2} \qquad f(x_1) = \frac{1}{3} \qquad f(x_2) = \frac{1}{5}
> $$
> 
> We first determine each $l_j$ polynomial.
> $$
> \begin{align*}
>     &l_0 (x) = \frac{(x - 3) (x - 5)}{(2 - 3) (3 - 5)} = \frac{1}{3} (x^2 - 8x + 15) \\
>     &l_1 (x) = \frac{(x - 2) (x - 5)}{(3 - 2) (3 - 5)} = -\frac{1}{2} (x^2 - 7x + 10) \\
>     &l_2 (x) = \frac{(x - 2) (x - 3)}{(5 - 2) (5 - 3)} = \frac{1}{6} (x^2 - 5x + 6) 
> \end{align*}
> $$
> 
> We use these to create our Lagrange Polynomial.
> $$
> \begin{align*}
> P_3 (x) 
> &= \frac{1}{6} (x^2 - 8x + 15) - \frac{1}{6} (x^2 - 7x + 10) + \frac{1}{30} (x^2 - 5x + 6) \\
> &= \frac{1}{30} (x^2 - 10x + 31)
> \end{align*}
> $$

### Newton's Form of Interpolation
Another way we can explicitly construct such polynomials is by using **Newton's Form of Interpolation**. 

This method attempts to find the polynomial in the form
$$
P_n (x) = a_0 + a_1 (x - x_0) + x_2 (x - x_0) (x - x_1) + \dots + a_n \prod_{j=0}^{n-1} (x - x_j)
$$
Where $a_0 \dots a_n$ are constants we are attempting to find.

Suppose we have $\{ x_i \}_{i=0}^n$ distinct nodes. Then, we define the **$k^{th}$ divided difference of $f$**.
- The **zeroth divided difference** of $f$ at $x_i$ is
  $$
  f[x_i] = f(x_i) 
  $$
- The **first divided difference** of $f$ at $x_i, x_{i + 1}$ uses the zeroth divided difference.
  $$
  f[x_i, x_{i + 1}] = \frac{f[x_{i+1}] - f[x_i]}{x_{i+1} - x_i} ] = \frac{f(x_{i+1}) - f(x_i)}{x_{i+1} - x_i}
  $$
- The **second divided difference** of $f$ at $x_i, x_{i + 1}, x_{i + 2}$ uses the first divided difference.
  $$
  f[x_i, x_{i+1}, x_{i+2}] = \frac{f[x_{i+1}, x_{i+2}] - f[x_i, x_{i+1}]}{x_{i+2} - x_i}
  $$
- The **$k^{th}$ divided difference** of $f$ at $x_i, x_{i+1}, \dots x_{i + k}$ uses the $(k-1)^{th}$ divided difference.
  $$
  f[x_i, x_{i+1}, \dots x_{i + k}] = \frac{f[x_{i+1}, x_{i+2}, \dots x_{i+k}] - f[x_{i}, x_{i+1}, \dots x_{i+k-1}]}{x_{i+k} - x_i}
  $$

We continue determining the divided differences, until we have a divided difference on all the $x_i$ terms.
