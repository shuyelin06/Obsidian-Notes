---
title: Numerical Differentiation and Integration
tags:
- amsc460
---

# Numerical Differentiation
## Problem Defined
In many practical applications, we may want the derivative of a function $f$, without evaluating the true expression for $f'(x)$. This may occur because:
- The true expression for $f'(x)$ is extremely complicated, or expensive to compute!
- We only have points for $f$ - $\{ (x_i, f(x_i) ) \}$, so we don't even have an expression for $f$ to compute a derivative with!

How can we find such derivatives?

## Derivations Using Taylor Approximations
One way we can derive an iterative solution for derivatives is by using their Taylor Approximation! 

For example, recall that 
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
Where $\text{Er(h)}$ is the error value on $h$, which converges to 0 as h becomes small. This has a $1^{st}$ order error, and approximates our derivative from the left-hand side, known as the **forward difference**! 

> [!Info] Orders of Error
> For any error term $\text{Er(h)}$, we say that it is a $p^{th}$ order method ($O(h^P)$), where $p$ is the leading power term (lowest exponent) of $h$ in $\text{Er(h)}$, as the lowest exponent will contribute the most to the error.
> 
> The higher the order of error, the better!

We similarly have a **backward difference**,
$$
f'(x) = \frac{f(x) - f(x - h)}{h} + \text{Err(h)}
$$
which essentially approximates our derivative from the right-hand side (with $1^{st}$ order of error), and a **central difference**,
$$
f'(x) = \frac{f(x+h) - f(x-h)}{2h} + \text{Er}(h)
$$
which approximates our derivative using both sides. We can show that this error term has a $2^{nd}$ order of error, making it better than the previous two!

> [!Example] Central Difference for $f''$
> We also can find a **central difference for $f''$** as 
> $$
> f''(x) = \frac{f(x+h) - 2f(x) + f(x-h)}{h^2} + \text{Er}(h)
> $$
> Which similarly has an error term for $O(h^2)$.

In general, we have for any $k \in \mathbb{R}$, that there exists $z \in (x, x + kh)$
$$
f(x + kh) = f(x) + f'(x) \frac{(kh)}{1!} + f''(x) \frac{(kh)^2}{2!} + f'''(x) \frac{(kh)^3}{3!} + f''''(z) \frac{(kh)^4}{4!}
$$
We can use combinations of these Taylor expansions to approximate our derivatives!

## Derivations Using Undetermined Coefficients
Sometimes, simple Taylor expansions are not enough - in these cases, we may still be able to approximate our derivative using the method of **undetermined coefficients**! In such a problem, we are given the following values
$$
\{ f(x + k_i h) \}_{i=1}^n
$$
where $k_i \in \mathbb{R}$, $i \ne j \to k_i \ne k_j$, and want to find a linear combination of these values to approximate some derivative $f^r (x)$. We then use their Taylor expansions to solve for the coefficients.

To see how this is done, consider the following example.

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
We now attempt to find $c_1, c_2, c_3$ necessary to find our answer. As we want our second derivative, we want to drop the coefficients for our $f$ and $f'$ terms to 0, but make the coefficient for the $f''$ term 1!
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

## Rates of Convergence
Given an approximation $L(h)$ of $T$, the error is given as
$$
E(h) = |T - L(h)| 
$$
Suppose the error is approximately equal to $Ch^p$, where $C$ is a constant, indicating that it is a $p$ order method.

If we take the logarithm of this error, we obtain
$$
\log (E(h)) \approx \log C + p \log h
$$

We can use this fact to to find our order of error (rate of convergence)! So, given our error on $h_1, h_2$,
$$
E(h_1) = C h_1^p \qquad E(h_2) = C h_2^p
$$

We can find our order of error as
$$
\begin{align*}
\frac{E(h_1)}{E(h_2)} = \left( \frac{h_1}{h_2} \right)^p \\
\log \frac{E(h_1)}{E(h_2)} = \log \left( \frac{h_1}{h_2} \right)^p \\
p = \frac{\log E(h_1) / \log E(h_2)}{\log h_1 / \log h_2} 
\end{align*}
$$


## Richardson's Extrapolation
**Richardson's Extrapolation** describes a general method to boost the accuracy of our approximations. 

Consider the $p^{th}$ order approximation
$$
T = L(h) + e_0 h^p + e_1 h^{p+1} + \dots
$$
Where $T$ is our target, $L(h)$ is our algorithm, and every $e_i h^{p + i}$ is part of the error term.

Note that if we wanted to change the order of our approximation, we'd need to eliminate the $e_0 h^p$ term. 

Consider what happens if we replace $h$ with $2h$.
$$
T = L(2h) + e_0 2^p h^p + e_1 2^{p+1} h^{p+1} + \dots
$$
Then, we can use this equation to elminate our $e_0 h^p$ error term. Multiplying our first equation by $2^p$ and subtracting our second equation from it, we get
$$
\begin{align*}
    (2^p - 1) T &=  2^p L(h) - L(2h) \\
    &+ 2^p (e_0 h^p + e_1 h^{p+1} + \dots )  - 2^p (e_0 h^p + 2 e_1 h^{p+1} + 4 e_2 h^{p+2} + \dots ) \\
    T &= \frac{2^p L(h) - L(2h)}{2^p - 1} + \hat{e}_1 h^{p+1} + \hat{e}_2 h^{p+2} + \dots
\end{align*}
$$
Giving us a new algorithm that increases our order of error!


# Numerical Integration
In other practical applications, we may want the integral of a function $f$, $\int_a^b f(x) dx$. This may occur because
- We may not know $f(x)$ in order to take the integral.
- We may know $f(x)$, but a closed form expression of the integral may not be available.
- We may be able to compute the integral, but it is difficult to compute.
- We may only have $f$ at a few nodes!

To do these approximations, we'll perform what are known as **quadrature rules**, rules that let us approximate integrals.

## Integration via Interpolation
Possibly one of the more intuitive approaches to approximations is to first interpolate $f$ given its points, and then integrate this interpolation.

Assume we're given points $\{ (x_i, f(x_i) \}_{i=0}^n$, where $\forall 0 \le i \le n$, $x_i \in [a,b]$. Recall that for these points, we can find our Lagrange Polynomial as
$$
f(x) \approx P_n (x) = \sum_{i=0}^n f(x_i) l_i (x)
$$

Where $l_i (x)$ are the bais polynomials. Then, as this approximates $f$, we may also be able to approximate its integral using $P_n (x)$!
$$
\int_a^b f(x) dx \approx \int_a^b P_n (x) dx = \sum_{i=0}^n f(x_i) \int_a^b l_i (x) dx
$$

This can alternatively be given as
$$
\int_a^b f(x) dx \approx \sum_{i=0}^n A_i f(x_i) \qquad A_i = \int_a^b l_i (x) dx
$$
> Similar to our Lagrange Interpolation, this has an advantage in that we can save on a lot of computation for different functions on the same nodes!

Note that this is essentially taking a "weighted sum", as the integrals define a value determining how much each $f(x_i)$ contributes to the result.

We discuss various ways we can use this below!

## Closed Newton-Cotes Quadrature
Suppose we have our equipspaced interpolation nodes on $[a,b]$, given by
$$
x_i = a + ih \qquad \forall 0 \le i \le n
$$
Where $h = \frac{b-a}{n}$. Note that by this, $x_0 = a$, and $x_n = b$.

Then, using our integral approximation from before, we'll obtain approximation
$$
\int_a^b f(x) dx = \sum_{i=0}^n A_i f(x_i) + Er(h)
$$

> [!Abstract] Theorem: Error
> There exists a $\epsilon \in (a,b)$ such that
> $$
> Er(h) = 
> \begin{cases}
>    \frac{h^{n+3} f^{n+2} (\epsilon)}{(n+2)!} \int_0^n t^2 (t - 1) (t - 2) \dots (t - n) dt & \text{n even and } f \in C^{n+2} [a,b] \\
>    \frac{h^{n+2} f^{n+1} (\epsilon)}{(n+1)!} \int_0^n t (t - 1) \dots (t - n) dt &\text{n odd and } f \in C^{n+1} [a,b]
> \end{cases}
> $$
> 
> Note that this error is 0, meaning this quadrature is exact if $f(x)$ is a polynomial such that
> - It's degree $\deg(f) \le n+1$ if $n$ is even
> - It's degree $\deg(f) \le n$ if $n$ is odd
> 
> As in these cases, the derivative in the error term drops to 0.

Some important quadratures from this rule are given below.
- When $n = 1$, we have the **Trapezoidal rule**, giving us
  $$
  \begin{align*}
      &x_0 = a &\qquad x_1 = b \\
      &\int_a^b f(x) dx = \left( \frac{f(a) + f(b)}{2} \right) (b - a) - \frac{h^3}{12} f''(\epsilon)
  \end{align*}
  $$
- When $n = 2$, we have the **Simpson's rule**, giving us
  $$
  \begin{align*}
      &x_0 = a \qquad x_1 = \frac{a + b}{2} \qquad x_2 = b \\
      &\int_a^b f(x) dx = \frac{f(a) + 4 f (\frac{a+b}{2}) + f(b)}{6} (b - a) - \frac{h^5}{90} f^4 (\epsilon) 
  \end{align*}
  $$

## Open Newton-Cotes Quadrature
Suppose we have a set of nodes $\{x_i\}_{i=0}^n \subset (a,b)$, such that $\forall 0 \le i \le n$,
$$
x_i = a + (i + 1)h
$$
Where $h = \frac{b - a}{n + 2}$. Note that by this definition, $x_0 = a + h$, and $x_n = b - h$.

Then, for some $\epsilon \in (a,b)$, we obtain
$$
\int_a^b f(x) dx = 
\begin{cases}
    \sum_{i=0}^n A_i f(x_i) + \frac{h^{n+3} f^{n+2} (\epsilon)}{(n+2)!} \int_{-1}^{n+1} t^2 (t-1)(t-2) \dots (t-n) dt & \text{n even} \\
    \sum_{i=0}^n A_i f(x_i) + \frac{h^{n+2} f^{n+1} (\epsilon)}{(n+1)!} \int_{-1}^{n+1} t^2 (t-1)(t-2) \dots (t-n) dt & \text{n odd} \\
\end{cases}
$$

Note that we have exactness if $f(x)$ is a polynomial under the same conditions as the closed-form algorithm.

Some important quadratures from this rule are given below.
- When $n = 0$, we have the **Midpoint rule**, giving us
  $$
  \begin{align*}
      &x_0 = \frac{a+b}{2} \\
      &\int_a^b f(x) dx = f \left( \frac{a+b}{2} \right) (b - a) + \frac{h^3}{3} f''(\epsilon)
  \end{align*}
  $$
  > This takes the integral of a constant line, whose value is equal to $f$'s midpoint.


## Composite Quadrature Rules
In each of these quadrature rules, because our errors depend on $h$, as $n \to \infty$, $h \to 0$, giving us lower errors! So, we should interpolate with higher-degree polynomials, right?

Wrong! As we use higher-degree polynomials, we run into another issue - Runge's Phenomena! So, to minimize our errors, we should use other methods (as described below).

One such method is by applying a **composite quadrature rule**, which partitions $[a,b]$ into smaller intervals and applies lower-order quadrature rules on each. So, given $\{x_i\}_{j=0}^m$, we'll have partition
$$
x_0 < x_1 < x_2 < \dots < x_{m-1} < x_m
$$
And can apply our quadrature rules on each $[x_j, x_{j+1}]$ subinterval with size $x_{j+1} - x_j$, whose composite will form our function integral.
$$
\int_a^b f(x) dx = \int_{x_0}^{x_1} f(x) dx + \int_{x_1}^{x_2} f(x) dx + \dots + \int_{x_{m-1}}^{x_m} f(x) dx
$$

Each subquadrature is given as
$$
\int_{x_j}^{x_{j+1}} f(x) dx \approx \sum_{i=0}^{n_j} A_i^j f(x_i^j)
$$
Where $A_i$ are the quadrature weights on $[x_j, x_{j+1}]$, and $\{ x_i^j \}_{i=0}^{n_j}$ are the quadrature nodes in our subinterval. For each subquadrature, we commonly will apply our midpoint rule, trapezoidal rule, or simpson's rule.

Suppose we applied our midpoint rule. We can prove that our new error is of order 2! 

> [!Note]- Proof
> For simplicity, assume that the size of our subintervals is constant. Then, if we applied our midpoint rule, for any subinterval, we get error term
> $$
> Err = \frac{h^3}{3} f''(\epsilon)
> $$
> For some $\epsilon$ in our subinterval. Then, our total composite error is given as
> $$
> Err = \sum_{j=0}^{m-1} Er_j = \frac{h^3}{3} \sum_{j=0}^{m-1} f''(\epsilon_j)
> $$
> 
> Defining $M = \frac{1}{m} \sum_{j=0}^{m-1} f''(\epsilon_j)$, the average of these node values, we know that this average is bounded by $f''(x)$'s maximum and minimum along the entire interval! So, we can apply intermediate value theorem to find a $c$ such that $f''(c) = M$. 
> 
> This gives us error
> $$
> Er = \frac{m h^3}{3} f''(c)
> $$
> For some $c$ in our interval $[a,b]$. Applying our assumption that $h = \frac{(b-a)}{m}$, we get
> $$
> Er = (b - a) \frac{h^2}{3} f''(c)
> $$
> Telling us that our error term is a 2nd order method!

We can similary find that the composition trapezoidal rule is a 2nd order method, and our composition simpson's rule is a 4th order method.

### Romberg Integration 
Similarly to how we have **Richardson's Extrapolation** for boosting accuracy, we can also apply something known as **Romberg Integration** to boost the accuracy of composite integration.

Applying a similar process to Richardson's Extrapolation, we obtain
$$
T = \frac{2^p Q(h) - Q(2h)}{2^p - 1} + \hat{e_1} h^{p+1} + \hat{e_2} h^{p+2}
$$
Giving us a new quadrature which is of a higher order error! 

However, we need to be a bit careful with this - replacing $h$ by $2h$ means we're halving the number of subintervals we have for this second quadrature! This is only possible if $m$ is even, as otherwise, we won't be able to evenly cover our entire domain.
> Doing this also means we have to evaluate $f$ at different points, which are actually where the partition boundaries once were!
