---
title: Root Finding Algorithms
tags:
- amsc460
---


Consider the function $f(x) = ax^2 + bx + c$. Suppose we want to find its root, i.e. $x^*$ such that $f(x^*) = 0$. Then we can easily do this using the **quadratic formula**!
$$
x^* = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}
$$

What if we had $f(x) = \sin(x) - e^{-x}$? Now our example is too complicated to find roots for! So, given a non-linear function, how can we find the roots of these functions? 

Here, we discuss **root-finding algorithms** that can do this for us! Note that:
- These algorithms are iterative, giving us a sequence of approximations $x_n$ that converge to a root $x^*$.
- The roots $x^*$ we find are NOT guaranteed to be unique, and the $x^*$ we converge to will depend on our initial guess $x_0$!

# Bisection Algorithm
Assume $f$ is continuous. Pick $a_0$ and $b_0$ such that $f(a_0) f(b_0) < 0$. Then, by the intermediate value theorem, we can guarantee the existence of a root between $a_0$ and $b_0$.

For each step $n = 0, 1, 2, \dots$, do the following:
1. Define the midpoint, $c_n = \frac{a_n + b_n}{2}$.
2. Then, we check the following cases.
   - If $f(c_n) = 0$, we have found our root and stop!
   - If $f(c_n) f(a_n) < 0$, then pick the next interval $[a_{n+1}, b_{n+1}] = [a_n, c_n]$ and repeat (1).
   - If $f(c_n) f(b_n) < 0$, then pick the next interval $[a_{n+1}, b_{n+1}] = [c_n, b_n]$ and repeat (1).

As we have our interval's size (about the root) every iteration, we should intuitively have convergence! The following theorem guarantees this.

> [!Abstract] Theorem: Convergence of the Bisection Algorithm
> Let $f$ be a continuous function on $[a_0, b_0]$ and $f(a_0) f(b_0) < 0$. Then,
> $$
> \lim_{n \to \infty} a_n = \lim_{n \to \infty} b_n = x^*
> $$
> 
> Where $f(x^*) = 0$.

How fast (efficient) is this algorithm? Well, we say that any given method is said to **converge with order $p$** if for some constant $c$,
$$
E_{n+1} \le c E_n^p
$$

In this case, note that because $c_n = \frac{a_n + b_n}{2}$, and $x^* \in [a_n, b_n]$, for every iteration $n$, 
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
Define $E_n = \frac{1}{2} (b_n - a_n)$. So for our bisection, we converge with order $p = 1$ (linearly) and $c = 1/2$.
> Higher orders of convergence are better, as it means our error term drops faster!


# Newton's Method
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

## Secant Method
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


---

# Non-Linear Systems of Equations
## Problem Defined
Suppose we have $n$ variables
$$
x = [x_1, x_2, \dots x_n]^T \in \mathbb{R}^n
$$

And we have $m$ functions on these variables 
$$
\begin{align*}
&f(x) = 
\begin{bmatrix}
    f_1 (x_1, x_2, \dots x_n) \\
    f_2 (x_1, x_2, \dots x_n) \\
    \vdots \\
    f_n (x_1, x_2, \dots x_n)
\end{bmatrix} \in \mathbb{R}^m
&f_j : \mathbb{R}^n \to \mathbb{R}
\end{align*}
$$

Similar to before, suppose we want to find $x^*$ such that $f(x^*) = 0$. We may be able to do this using a process similar to Newton's Method!
> This is a generalization of our previous problem, onto multiple variables!

## Problem Solution
First, let's define the **Jacobian Matrix** as $D_f (x) \in \mathbb{R}^{m \times n}$ such that
$$
D_f (x) = 
\begin{bmatrix}
    \frac{\partial f_1 (x)}{\partial x_1} & \dots & \frac{\partial f_1}{\partial x_n} (x) \\
    \vdots & & \vdots \\
    \frac{\partial f_m (x)}{d x_1} & \dots & \frac{\partial f_m (x)}{\partial x_n}
\end{bmatrix}
$$

### $m = n$ Case
Now, let's look at the case where $m = n$. Then, we have the following Taylor expansion of $f : \mathbb{R}^n \to \mathbb{R}^n$ about $x_0$
$$
f(x) = f(x_0) + D_f (x_0) (x - x_0) + R(x)
$$
Where $R(x)$ is a remainder based on the Taylor Remainder Theorem. Say we want to solve to obtain 0.
$$
D_f (x) (x - x_0) = - f(x_0) \\
\Longrightarrow A \delta x_0 = b
$$

This is a system of linear equations! So, given an initial guess $x^0$, for $k = 0, 1, 2, \dots$
1. Evaluate $A^k = D_f (x^k)$.
2. Evaluate $b^k = -f(x^k)$.
3. Solve for $\delta x^k$ satisfying
   $$
   A^k (\delta x^k) = b^k
   $$
4. Set $x^{k+1} = x^k + \delta x^k$.

> In MATLAB, we can actually do this process through the function `fsolve()`!

> [!Abstract] Theorem: Convergence
> Assume there is a root $f(x^*) = 0$. Then suppose the following properties hold:
> - $f$ is continuous on two derivatives, on some neighborhood $B$ around $x^*$.
> - The Jacobian at $x^*$, $D_f (x^*)$, is invertible.
> 
> Then, $\exists \delta > 0, c > 0$ such that for all guesses sufficiently close, $|| x^0 - x^* ||_\infty \le \delta$, we have
> - Convergence is guaranteed; $\lim_{k\to\infty} x^k \to x^*$
> - Our convergence is quadratic; $|| x^{k+1} - x^* ||_\infty \le C || x^k - x^* ||_\infty^2$

### $m > n$ Case
Let's now look at the case where $m > n$. 

As we now have more equations than unknowns, we may no longer have a solution! So, we instead want to find an $x^*$ that minimizes our problem. 
$$
x^* = \argmin_{x \in \mathbb{R}^n} || f(x) ||_2^2
$$
> This is known as the **Gauss-Newton Algorithm**.

So, writing our Taylor Remainder theorem from before, for any step $k$, we have approximation
$$
\begin{align*}
f(x) &\approx f(x^k) + D_f (x^k) (x - x^k) \\
&= -b^k + A^k (\delta x^k)
\end{align*}
$$

But this may not have a solution! So, applying our iterative method, we get the following. Take $x^0 \in \mathbb{R}^n$. Then, for $k = 0, 1, 2, \dots$,
1. Evaluate $A^k = D_f (x^k)$
2. Evaluate $b^k = f(x^k)$
3. Solve $\delta x^k = \argmin_{\delta x \in \mathbb{R}^n} || A^k \delta x - b^k ||_2^2$. 

    This is equivalent to solving our minimization problem (see above)
   $$
   (A^k)^T A^k \delta x^* = (A^k)^T b^k
   $$
4. Add $x^{k+1} = x^k + \delta x^k$.

Our error estimate on this algorithm is
$$
|| x^{k+1} - x^* ||_2 \le C ( || f(x^*) ||_2 \cdot || x^k - x^* ||_2 + || x^k - x^* ||_2^2 )
$$

This is comparing our new error every $x^{k+1}$ to our old error! We get quadratic convergence if $|| f(x^*) || = 0$, which is not usually true!

Thus, if $\epsilon = || f(x^*) ||_2$ is small, then you initially have **quadratic decay**, but once $|| x^k - x^* ||_2 \approx \epsilon$, then decay becomes linear, as we can no longer ignore the $|| f(x^*) ||_2 \cdot || x^k - x^* ||_2$ term.
