---
title: Taylor Polynomials
tags:
- math410
---

# Taylor Polynomials
Suppose we have a function $f$, with $n$ derivatives. How could we approximately match it?

Well, one potential way of doing this might be by matching $f's$ derivatives at a point $x_0$! If we can capture $f$'s entire state at a point, we may be able to approximate the entire function, or at least approximate nearby points.

We say two functions $f$ and $g$ have **contact of order** $n$ at $x_0$ if
$$
f^k (x_0) = g^k (x_0) \qquad \forall k = 0,1,2,\dots n
$$

> [!Example]+ Example: Contact of Order
> Let $f = x^2$, $g = x^3$. These two functions have a contact of order $1$ at $x_0 = 0$, as
> $$
> f(x_0) = 0 = g(x_0) \\
> f'(x_0) = 0 = g'(x_0) \\
> f''(x_0) = 2 \ne 0 = g''(x_0)
> $$

With Taylor Polynomials, we are trying to give $f$ and $g$ the highest contact of order we can! This has a ton of practical applications in the real world.

> [!Info] Notation: Kronecker Delta
> For convenience, we will define the notation
> $$
> \delta_{kl} = \begin{cases}
>    1 & k = l \\ 0 & k \ne l
> \end{cases}
> $$


> [!Abstract] Theorem: Taylor Polynomial
> Let $I$ be an open interval containing $x_0$, and fix $n \in \mathbb{N}$. 
> 
> Then, if $f$ is $n$-times differentiable, there exists a unique Taylor Polynomial $p_n \in \mathbb{P}_n$ such that $p_n$ and $f$ have contact of order $n$ at $x_0$.
> 
> > [!Note]- Proof
> > 
> > Start with the guess that the polynomial exists, with the form
> > $$
> > P_n (x) = \sum_{l=0}^n a_l (x - x_0)^l
> > $$
> > 
> > We show that we can choose our $a_l$'s to form such a polynomial. Let's first force 
> > $$
> > f^k (x_0) = p^k (x_0) \qquad \forall k = 0, 1, \dots, n
> > $$
> > 
> > So,
> > $$
> > \begin{align*}
> >     f^k (x_0) &= \sum_{l=0}^n a_l \frac{d^k}{dx^k} (x - x_0)^l \bigg\vert_{x=x_0} \\
> >         &= \sum_{l=0}^n a_l k! \delta_{kl} \\
> >         &= a_k k!
> > \end{align*}
> > $$
> > Giving us $a_k = \frac{f^k (x_0)}{k!}$, so
> > $$
> > p_n (x) = \sum_{l=0}^n \frac{f^l (x_0)}{l!} (x - x_0)^l
> > $$
> > > We can show uniqueness by assuming two polynomials, and showing their coefficients are the same, by evaluating their derivatives at $x_0$ (which drops everything else to 0).
> > 
> > We verify the intermediate step below. Suppose we have
> > $$
> > \frac{d^k}{dx^k} (x - x_0)^3 \bigg\vert_{x = x_0} = \Phi^k (x)
> > $$
> > Then, for various values $k$, we have
> > $$
> > \begin{align*}
> >     &k = 0 &\Phi^0 (x_0) = 0 \\
> >     &k = 1 &\Phi^1 (x_0) = 0 \\
> >     &k = 2 &\Phi^2 (x_0) = 0 \\
> >     &k = 3 &\Phi^3 (x_0) = 3! \\
> >     &k = 4 &\Phi^4 (x_0) = 0 \\
> >     &k > 4 &\Phi^k (x_0) = 0
> > \end{align*}
> > $$
> > So, 
> > $$
> > \frac{d^k}{dx^k} (x - x_0)^3 \bigg\vert_{x = x_0} = 3! \delta_{k3}
> > $$
> > We can generalize this for all $l$!

What if we extended this for $n \to \infty$? That is, given $f$, is it true that
$$
f(x) = \sum_{k=0}^\infty \frac{f^k (x_0)}{k!} (x - x_0)^k = \lim_{n\to\infty} p_n (x)
$$
This is possible, but only in some cases. This is where the remainder theorem comes in! 

For any function $f$, we can write it as
$$
f(x) = p_n (x) + r_n (x)
$$
Where $r_n (x)$ is its remainder term. The following theorem defines this remainder term for us.

> [!Abstract] Theorem: Lagrange Remainder Theorem
> Fix $n \in \mathbb{N}$, and let $x_0 \in I$. Let $f : I \to \mathbb{R}$ be $(n + 1)$ times differentiable. Then, $\forall x \ne x_0$, there $\exists c \in I$ such that
> $$
> f(x) = p_n (x) + \frac{f^{n+1} (c)}{(n+1)!} (x - x_0)^{n+1}
> $$
>
> > Note that $c$ depends on $x$ and $n$. Thus, changing $x$ or $n$ may give us a different $c$.
>
> > [!Note]- Proof
> > 
> > $$
> > f(x) - p_n (x) = r_n (x)
> > $$
> > Since $f$ and $p_n$ have contact of order $n$ at $x_0$, 
> > $$
> > r(x_0) = r'(x_0) = r''(x_0) = \dots = r^n (x_n) = 0
> > $$
> > By the Function Value Theorem, we have that for any $x \ne x_0$, $\exists c$ such that
> > $$
> > r (x) = \frac{r^{n+1} (c)}{n!} (x - x_0)^{n+1} = \frac{f^{n+1} (c)}{n!} (x - x_0)^{n+1}
> > $$
> > Because $p_n^{n+1} = 0$.

Then, for $f$ to equal it's Taylor Series, we need this remainder to drop to 0 as $n \to \infty$!

When does this remainder term converge to 0?
$$
|r(x)| \le \frac{|f^{n+1}(c)|}{(n+1)!} |x - x_0|^{n+1}
$$
Notice that in the denominator, we have a factorial $(n+1)!$, whereas in the numerator we have a power $|x-x_0|^{n+1}$. 

> [!Abstract] Theorem: Factorials vs Powers
> $$
> \lim_{n\to\infty} \frac{|c|^n}{n!} = 0 \qquad \forall c \in \mathbb{R}
> $$
> 
> > [!Note]- Proof
> >
> > Using the Ratio Test, our sum converges if our limit
> > $$
> > \lim_{n\to\infty} \left| \frac{a_{n+1}}{a_n} \right| = r < 1
> > $$
> > In which case our series converges to 0.
> > 
> > $$
> > \frac{|c|^{n+1}/(n+1)!}{|c|^n / n!} = \frac{|c|}{n+1} \to 0
> > $$

As seen above, factorials grow faster than powers - so for convergence, we need our numerator term to be a power or slower! So, if we assume our function grows no faster than a power function,
$$
|f^n (x)| \le C M^n \qquad \forall n
$$
For some $C > 0, M > 0$, then we obtain convergence of our remainder term.
$$
|r(x)| \le \frac{CM^{n+1} |x - x_0|^{n+1}}{(n+1)!} \to 0
$$

This is given in the below theorem. 

> [!Abstract] Theorem: Convergence of Taylor Polynomial
> Let $f \in C^\infty (I)$, and let $x_i \in I$. Suppose $\exists \delta, C, M$ such that
> $$
> |f^n (x)| \le CM^n \qquad \forall x \in [x_0 - \delta, x_0 + \delta]
> $$
> > Note that this condition is sufficient, but not necessary for all cases of convergence.
> 
> Then, $f$ is equal to its Taylor series on $[x_0 - \delta, x_0 + \delta]$.
> $$
> f(x) = \sum_{k=0}^\infty \frac{f^k (x_0)}{k!} (x - x_0)^k
> $$

> [!Example]+ Example: Convergence of Taylor Polynomial
> $$
> \cos x = \sum_{n=0}^\infty \frac{(-1)^n}{(2n)!} x^{2n} \qquad x = x_0
> $$
> 
> Convergence occurs because every derivative of $\cos x$ is bounded between $-1$ and $1$. In other words,
> $$
> \left| \frac{d^n}{dx^n} \cos x \right| \le 1 \le C \cdot M^n 
> $$
> Where $C = 1$, $M = 1$.

> [!Example]- Example: Convergence of Taylor Polynomial (2)
> $$
> e^x = \sum_{n=0}^\infty \frac{x^n}{n!} \qquad x_0 = 0
> $$
>
> Let's show convergence directly through remainder theorem. Our Lagrange Remainder is given as
> $$
> \frac{f^{n+1} (c)}{(n+1)!} x^n = \frac{e^c}{(n+1!} x^n
> $$
> $c$ depends on both $x$ and $n$! So, we need to restrict our $x \in [-R,R]$ to be able to restrict $c$, and claim convergence.
> $$
> \frac{e^c}{(n+1!} x^n \le \frac{e^R}{(n+1)!} |x|^n \to 0
> $$
> As this works for any $x \in [-R,R]$ we can expand $R$ to infinity to obtain convergence along all $x$!

> [!Example]- Example: Convergence of Taylor Polynomial (3)
> Does the Taylor Polynomial for $1/x$ converge?
> $$
> \frac{1}{x} \approx \sum (-1)^n (x - 1)^n \qquad x_0 = 1
> $$
>
> Yes, but only for $0 < x < 2$. Otherwise, our $(x - 1)$ term would be 1 or greater, making our remainder term fail to converge!
>
> We attempt to show convergence using the Lagrange Remainder Theorem. By the Lagrange Remainder Theorem, we obtain remainder
> $$
> | r_n (x) | = \frac{|x - 1|^{n+1}}{|c_{n,x}|^{n+2}}
> $$
> 
> 1. **Case 1**: Suppose $1 < x < 2$. Then, we have $\frac{1}{c_{n,x}} < 1$, and we furthermore know that $0 < x - 1 < 1$, so our remainder converges to 0 as $n \to \infty$! In other words, our Taylor series converges to $f$ on $1 \le x < 2$.
> 2. **Case 2**: Suppose $0 < x < 1$. Then, we have $x < c_{n,x} < 1 \Longrightarrow \frac{1}{c_{n,x}} < \frac{1}{x}$, so we have remainder term
>    $$
>    |r_n (x)| \le \frac{|x - 1|^{n+1}}{x^{n+2}}
>    $$
>    Which fails to converge to 0 for all $x \in (0,1)!
> 
> Notice how Lagrange fails in case 2, but we still have convergence on $x \in (0,1)$! Thus, Lagrange is a sufficient condition to prove convergence, but is not necessary for convergence.

# Analytic Functions
We say $f : D \to \mathbb{R}$ is **(real)-analytic** if $\forall x_0 \in D$, $\exists \delta > 0$ and $I = (x_0 - \delta, x_0 + \delta)$ such that
$$
f(x) = \sum_{n=0}^\infty a_n (x - x_0)^n
$$
For $x \in I$, and some $\{a_n\}$. In other words, all points in the function has a localized power series expansion!

Note that if $f$ is analytic, then it is smooth ($f \in C^\infty$). However, the converse of this is false! See the below example.

> [!Example]+ Example: Analytic Function Counterexample
> Consider the **bump function (mollifier)**
>
> $$
> f(x) = 
> \begin{cases}
>    c_\epsilon e^{\frac{1}{|\frac{x}{\epsilon}|^2 - 1}} & |x| < \epsilon \\
>    0 & |x| \ge \epsilon
> \end{cases}
> $$
> Where $c_\epsilon$ is chosen to make the integral equal to 1.
>
> This is a smooth function, but it doesn't have a globally convergent Taylor series, nor is it analytic!

> [!Abstract] Theorem: Weierstrass Approximation Theorem
> Let $f \in C[a,b]$. Then, $\forall \epsilon > 0$, there exists a polynomial $p_n$ of degree $n$ such that $\forall x \in [a,b]$, 
> $$
> | f(x) - p_n (x) | < \epsilon
> $$
>
> > Note that $n$ can be a very high degree!

This theorem is very strong, but needs all of the clauses! See the below counterexample. 

> [!Example] 
> Suppose $[a,b]$ is not compact. Then, we can form a counterexample to this theorem with $e^x$ on $(-\infty, \infty)$!
> 
> Suppose $| p_n (x) - f(x) | < \epsilon$ for all $x$. Then, we get a counterexample as for any non-zero polynomial, it will eventually go to $-\infty$ or $\infty$, so it cannot be bounded!
> 
> In other words,
> $$
> |p_n (x)| = |p_n (x) - e^x + e^x| \le |p_n - e^x| + e^x < \epsilon + e^x
> $$
> So as $x \to -\infty$, this forces $p_n(x)$ to go to $\epsilon$, but this is not possible for a non-zero polynomial!

