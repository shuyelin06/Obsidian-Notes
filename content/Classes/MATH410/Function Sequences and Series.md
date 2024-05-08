---
title: Function Sequences and Series
tags:
- math410
---

# Cauchy Sequences
We say the sequence
$$
\{a_n\}_{n=1}^\infty \in \mathbb{R}
$$
is **Cauchy** if $\forall \epsilon > 0$, $\exists N \in \mathbb{N}$ such that $\forall n, m \ge N$,
$$
| a_n - a_m | < \epsilon
$$

> [!Abstract] Theorem: Boundedness of Cauchy Sequences
> Let $\{a_n\}$ be a Cauchy sequence. Then, $\{a_n\}$ is bounded.
> 
> > [!Note]- Proof
> >
> > This proof is very similar to our proof on boundedness of convergent sequences!
> > 
> > Let $\{a_n\}$ be Cauchy. Then,
> > $$
> > \begin{align*}
> > |a_n| 
> > &= |a_n - a_N + a_N| \\
> > &\le |a_n - a_N| + |a_N| \\
> > &< \epsilon + |a_N|
> > \end{align*}
> > $$
> > This guarantees a bound for our larger values! So, we take $M = \max\{\epsilon + |a_N|, |a_n|, \dots |a_{N-1}|\}$ to find a bound.

> [!Abstract] Theorem: Convergence of Cauchy Sequences
> Let $\{a_n\}$ be a sequence of real numbers. Then, $\{a_n\}$ is Cauchy if and only if it converges.
>
> > Note that this only holds because our sequence is on real numbers! In other spaces, this may not hold.
> 
> > [!Note]- Proof
> > 
> > #### Proof ($\leftarrow$)
> > Suppose $\{a_n\}$ converges. Let $a$ be what it converges to. Then,
> > $$
> > \begin{align*}
> > | a_n - a_m | 
> > &= | a_n + a - a - a_m | \\
> > &\le | a_n - a | + | - (a_m - a) | \\
> > &< \frac{\epsilon}{2} + \frac{\epsilon}{2} \\
> > &< \epsilon
> > \end{align*}
> > $$
> > 
> > #### Proof ($\rightarrow$)
> > Suppose $\{a_n\}$ is Cauchy. By definition, $\forall \epsilon > 0$, $\exists N \in \mathbb{N}$ such that $\forall n, m \ge N$, 
> > $$
> > | a_n - a | < \epsilon
> > $$
> > 
> > We know that Cauchy sequences are bounded. By the Bolzano-Weierstrass Theorem, we can extract a convergent subsequence $\{a_{n_k}\} \to L$ forall $k \ge K$.
> >
> > Finally, fix $N$ and $K$. Then,
> > $$
> > \begin{align*}
> > | a_n - L | 
> > &\le | a_n - a_{n_k} | + | a_{n_k} - L | \\
> > &< \frac{\epsilon}{2} + \frac{\epsilon}{2} \\
> > &< \epsilon
> > \end{align*}
> > $$
> > For $n \ge N$, $n_k \ge N$, and $k \ge K$. Note that we can always obtain this, as $n_k$ is a strictly increasing seqeuence, so we can keep increasing $K$ until $n_k \ge N$.


Cauchy sequences can be very helpful in determining convergence! Recall how before, we could show that a sequence converges, but we had to know what it converged to in order to prove this! Cauchy sequences avoids this limitation. 

# Infinite Series
Let $S_n$ be a **partial sum**, given as
$$
S_n = \sum_{k=0}^n a_k
$$
Where $\{a_k\}$ are terms of a sequence. We say it is a **series** when $n \to \infty$, and this series **converges** if
$$
S = \lim_{n\to\infty} S_n \qquad S \in \mathbb{R}
$$
Otherwise, if $S$ does not exist, then the series **diverges**.

Proofs for some of the series tests are given below.

> [!Note]- Telescoping Sums (Proof)
> By assumption, suppose that $\{c_n\} \to 0$.
> $$
> \begin{align*}
> s_n &= \sum_{k=m}^\infty (c_{k-1} - c_k) \\
>     &= (c_{m_1} - c_m) + (c_m - c_{m+1} ) + \dots + (c_{n-1} - c_n) \\
>     &= c_{m-1} - c_n \to c_{m-1}
> \end{align*}
> $$

> [!Note]- Divergence Test (Proof)
> Suppose $\sum_{k=0}^\infty a_k$ converges. Then, 
> $$
> a_n = S_n - S_{n-1} \to 0 
> $$
> 
> So by contrapositive, if $a_n \not\to 0$, then the series diverges.

> [!Note]- Geometric Series (Proof)
> $$
> \begin{align*}
> s_n = \sum_{k=0}^n r^k = 1 + r + r^2 + \dots + r^n \\
> r s_n = r + r^2 + r^3 + \dots + r^{n+1} \\
> (1 - r) s_n = 1 - r^{n+1} \\
> s_n = \frac{1 - r^{n+1}}{1 - r} \to \frac{1}{1 - r} \qquad |r| < 1
> \end{align*}
> $$

> [!Note]- Series with Non-Negative Terms (Proof)
> $$
> s_n = \sum_{k=0}^n a_k \qquad a_k \ge 0
> $$
> By the Monotone Convergence Theorem, if $\{s_n\}$ is bounded, then it converges, and it converges to its supremum.

> [!Note]- Direct Comparison Test (Proof)
> $$
> \begin{align*}
> 0 \le a_k \le b_k \\
> 0 \le \sum_{k=1}^n a_k \le \sum_{k=1}^n b_k
> \end{align*}
> $$
> Suppose $\sum b_k$ exists. Then, $\sum a_k$ exists by the Monotone Convergence Theorem.
> 
> Otherwise, if $\sum a_k = \infty$, then $\sum b_k = \infty$ as no number can be greater than infinity.

> [!Note]- Limit Comparison Test (Proof)
> We have
> $$
> a_k \ge 0, b_k \ge 0 \qquad \lim_{k\to\infty} \frac{a_k}{b_k} = c > 0
> $$
> Thus, $\forall \epsilon > 0$, $\exists N \in \mathbb{N}$ such that $\forall k \ge N$, 
> $$
> \left| \frac{a_k}{b_k} - c \right| < \epsilon
> $$
> This gives us
> $$
> 0 \le b_k (-\epsilon + c) < a_k < b_k (\epsilon + c)
> $$
> Taking the summation, we can apply the direct comparison test to determine convergence or divergence.
> > Basically, we find that our partial sums are approximately equal (with a multiplier), so anything one sum does, the other must also do.

> [!Note]- Integral Test & P-Test (Proof)
> We have
> $$
> 0 \le \sum_{n=1}^\infty f(n+1) \le \int_a^\infty f(x) dx \le \sum_{n=1}^\infty f(n)
> $$
> Formed with the left-hand and right-hand Riemann sums, whose comparisons are known as $f$ is monotonically decreasing.
> 
> Apply direct comparison test.
>
> Apply integral test on $p-Test$ to show convergence on $p > 1$.

> [!Note]- Cauchy Convergence Criterion (Proof)
> Suppose $\{s_n\}$ is Cauchy. Then, we can combine $s_m, s_n$ into a single sum, which by definition is bounded by $\epsilon$.

> [!Note]- Absolute Convergence Test (Proof)
> Let $s_n = \sum_{k=1}^n a_k$. We show $s_n$ is Cauchy
> $$
> 0 \le | s_{n+k} - s_n | = | \sum_{i=n+1}^{n+k} a_i | \le \sum_{i=n+1}^{n+k} |a_i| < \epsilon
> $$
> We have $< \epsilon$ provided our $n$ is large enough.
>
> We now apply the Cauchy Sequence Criterion to obtain convergence.

# Convergence of Function Sequences
## Pointwise Convergence
We say a sequence of functions **$\{f_n\} \to f$ pointwise on $D \subseteq \mathbb{R}$**, if $\forall x \in D, \forall \epsilon > 0, \exists N \in \mathbb{N}$ such that $\forall n \ge N$,
$$
| f_n (x) - f(x) | < \epsilon
$$
Or in other words, $\forall x \in D$,
$$
\lim_{n \to \infty} f_n (x) = f(x)
$$
> Notice how we fix our $x$ first, before aplying our limit!

> [!Example]+ Example: Pointwise Convergence of Taylor Polynomials
> It can be shown that $\forall x_0$, the Taylor Polynomials pointwise converge to $f$
> $$
> f(x_0) = \lim_{n \to \infty} P_n (x_0)
> $$
> 
> Provided that the Lagrange Remainder drops to 0
> $$
> | r_n (x_0) | \to 0 \qquad n \to \infty
> $$

This is a very weak notion of convergence! Let's see why in the following examples.

> [!Example] Example: Pointwise Covergence (1)
> $$
> f_n (x) = x + \frac{1}{n}
> $$
> 
> Fix $x \in \mathbb{R}$. Then, as $n \to \infty$, $\{f_n (x)\} \to x$, giving us pointwise convergence.

Some notable things we can see from this example:
1. All functions $f_n$ are continuous on $x \in \mathbb{R}$, and so is $f$.
2. The limit of our derivatives is equal to our function derivative
   $$
   \lim_{n\to\infty} f_n' (x) = 1 = f'(x)
   $$
3. The limit of our integrals is equal to our function integral
   $$
   \lim_{n\to\infty} \int_a^b f_n (x) dx = \frac{1}{2} x^2 \bigg\vert_a^b = \int_a^b f(x) dx
   $$

However **none of these properties always hold for pointwise convergence**! This makes pointwise convergence is extremely weak, as we can't really use it for anything.

> [!Example]+ Example: Weakness of Pointwise Convergence (1)
> Consider $f_n (x) = x^n$ on $[0,1]$. Then,
> $$
> \{ f_n \} \to f(x) \; \text{pointwise} \; = 
> \begin{cases}
>     0 & x \in [0,1) \\
>     1 & x = 1
> \end{cases}
> $$
>
> So, we have pointwise convergence, but the limit ($f$) is not continuous!

> [!Example]+ Example: Weakness of Pointwise Convergence (2)
> Consider $f_n (x) = \sin(nx) / n$. Observe that as $n \to \infty$,
> $$
> \lim_{n\to\infty} f_n (x) = 0
> $$
> 
> However, 
> $$
> f_n' (x) = \cos(nx)
> $$
> Does not converge to $f$'s derivative which is 0!
> > We can show this by taking $\cos(2nx)$, applying a trig identity, and obtaining a contradiction by seeing that the identity gives us convergence to -1!

> [!Example]+ Example: Weakness of Pointwise Convergence (3)
> $$
> f_n (x) = 
> \begin{cases}
>     0 & x \in \{ q_1, q_2, \dots q_n \}, q_i \in \mathbb{Q} \\
>     1 & \text{else}
> \end{cases}
> $$
> 
> Then,
> $$
> f_n (x) \to f(x) \; \text{pointwise} \; = 
> \begin{cases}
>     0 & x \in \mathbb{Q} \cap [0,1] \\
>     1 & \text{else}
> \end{cases}
> $$
> 
> So the integral of $\int_0^1 f_n (x) = 1$ (we have a finite number of points), but the integral of the limit doesn't exist!


## Uniform Convergence
We say a sequence of functions $\{f_n\} \to f$ **uniformly** on $D \subseteq \mathbb{R}$, if $\forall \epsilon > 0$, $\exists N \in \mathbb{N}$ such that $\forall n \ge N$, $\forall x \in D$
$$
| f_n (x) - f(x) | < \epsilon
$$
> Notice how we fix our $x$ last! This is called uniform convergence, as our $N$ is no longer dependent on $x$, and should work "uniformly" for all $x$.

Uniform convergence is a much stronger notion of convergence than pointwise.

> [!Abstract] Theorem: Uniform and Pointwise Convergence
> If $\{f_n\} \to f$ uniformly on $D$, then $\{f_n\} \to f$ pointwise.

> [!Example]+ Example: Uniform Convergence
> $$
> f_n (x) = x + \frac{1}{n}
> $$
> 
> Let's show $\{f_n\} \to f$ uniformly. Fix $\epsilon > 0$. We want
> $$
> | f_n (x) - f(x) | = \left| x + \frac{1}{n} - x \right| = \left| \frac{1}{n} \right| \le \left| \frac{1}{N} \right| < \epsilon 
> $$
> 
> Choose $N$ such that $\frac{1}{N} < \epsilon$, whose existence is guaranteed by the Archimedian Property. Then, we have uniform convergence.

> [!Example]- Example: Uniform Convergence (2)
> $$
> f_n (x) = x^n \qquad x \in [0,1]
> $$
> 
> As shown before, this converges pointwise to
> $$
> f(x) = \begin{cases}
>     1 & x = 1 \\ 0 & x \in [0,1)
>     \end{cases}
> $$
> 
> Assume $f_n \to f$ uniformly. Then, $\forall \epsilon > 0$, $\exists N \in \mathbb{N}$ such that $\forall n \ge N, \forall x \in [0,1]$,
> $$
> | x^n - f(x) | < \epsilon
> $$
> 
> Let's choose $\epsilon = \frac{1}{10}$. So,
> $$
> | x^n - f(x) | < \frac{1}{10} \qquad \forall x \in [0,1]
> $$
> 
> Choose $x = \left( \frac{1}{2} \right)^{1/n}$, which is in our interval. Then,
> $$
> \left| \left( \left( \frac{1}{2} \right)^{1/n} \right)^n - f(x) \right| \not< \frac{1}{10}
> $$

We say sequence $\{f_n\}$ is **uniformly Cauchy** on $D \subseteq \mathbb{R}$ if $\forall \epsilon > 0$, $\exists N \in \mathbb{N}$ such that $\forall n \ge N, \forall k \in \mathbb{n}, \forall x \in D$,
$$
| f_{n+k} (x) - f_n (x) | < \epsilon
$$
> While a complex definition, this lets us show convergence even if we don't know the limit!

> [!Abstract] Theorem: Uniform Cauchy and Uniform Convergence
> Uniform Cauchy convergence implies uniform convergence. 
> 

> [!Example]+ Example: Uniform Cauchy Convergence
> $$
> f_n (x) = \sum_{j=1}^n \frac{x^j}{j 2^j} \qquad f_n : [-1, 1] \to \mathbb{R}
> $$
> 
> We show this is uniformly convergent using our Cauchy definition. Let $\epsilon > 0$. We want
> $$
> \begin{align*}
>     \left| f_{n+k} (x) - f_n (x) \right| 
>     &= \left| \sum_{j=1}^{n+k} \frac{x^j}{j 2^j} - \sum_{j=1}^n \frac{x^j}{j 2^j} \right| \\
>     &= \left| \sum_{j=n+1}^{n+k} \frac{x^j}{j 2^j} \right|
>     \le \sum_{j=n+1}^{n+k} \frac{|x^j|}{j 2^j} \\
>     &\le \sum_{j=n+1}^{n+k} \frac{1}{j 2^j}
>     \le \sum_{j=n+1}^{\infty} \frac{1}{j 2^j} \\
>     &\le \sum_{j=n+1}^{\infty} \frac{1}{2^j} < \epsilon
> \end{align*}
> $$
> 
> Provided $N$ is large enough. We find this $N$ using the Geometric Series Test to finish.

Uniform convergence is much stronger than pointwise convergence! In fact, properties of continuity, differentiation, and integration that did not hold for pointwise convergence, now hold for uniform convergence!

> [!Abstract] Theorem: Continuity and Uniform Convergence
> If $f_n : D \to \mathbb{R}$ is continuous for each $n$, and $f_n \to f$ uniformly, then $f$ is continuous.
> > The same holds for uniform continuity on $f_n$ and $f$.
>
> > [!Note]- Proof
> > 
> > By definition of $f_n$'s continuity, $\forall \epsilon > 0$, $\exists \delta > 0$ such that $\forall x \in D$,
> > $$
> > | x - x_0 | < \delta \to | f_n(x) - f_n(x_0) | < \frac{\epsilon}{3}
> > $$
> > 
> > And by definition of uniform convergence, $\forall \epsilon > 0$, $\exists N \in \mathbb{N}$ such that $\forall n \ge N, \forall x \in D$,
> > $$
> > | f_n (x) - f(x) | < \frac{\epsilon}{3}
> > $$
> > 
> > We want to show that $\forall \epsilon > 0$, $\exists \delta > 0$ such that $\forall x \in D$,
> > $$
> > | x - x_0 | < \delta \to | f(x) - f(x_0) | < \epsilon
> > $$
> > 
> > Fix $\epsilon > 0$. If $| x - x_0 | < \delta$, then
> > $$
> > \begin{align*}
> > | f(x) - f(x_0) | 
> >     &= | f(x) - f(x_0) + f_n (x) - f_n (x) + f_n (x_0) - f_n (x_0) \\
> >     &\le | f_n(x) - f_n (x_0) | + | f_n (x) - f(x) | + | f_n(x_0) - f(x_0) | \\
> >     &< \frac{\epsilon}{3} + \frac{\epsilon}{3} + \frac{\epsilon}{3} = \epsilon
> > \end{align*}
> > $$

> [!Abstract] Theorem: Integration and Uniform Convergence
> Let $f_n \to f$ uniformly on $[a,b]$, and assume $\int_a^b f_n$ exists for al $n$. Then,
> $$
> \lim_{n\to\infty} \int_a^b f_n = \int_a^b \lim_{n\to\infty} f_n = \int_a^b f
> $$
>
> > [!Note]- Proof
> > 
> > By definition, $\forall \epsilon > 0$, $\exists N \in \mathbb{N}$ such that $\forall n \ge N, \forall x \in [a,b]$,
> > $$
> > | f_n (x) - f(x) | < \epsilon \Longrightarrow f_n (x) - \epsilon < f(x) < f_n (x) + \epsilon
> > $$
> > 
> > Taking the upper integral on the right-side inequality, and the lower integral on the left-side inequality,
> > $$
> > \begin{align*}
> >     \overline{\int_a^b} f < \overline{\int_a^b} f_n (x) dx + \epsilon (b - a) \\
> >     \underline{\int_a^b} f_n (x) dx - \epsilon (b - a) < \underline{\int_a^b} f
> > \end{align*}
> > $$
> > 
> > Combining these, we get
> > $$
> > \begin{align*}
> > 0 \le \overline{\int_a^b} f - \underline{\int_a^b} f < \left( \overline{\int_a^b} f_n dx + \epsilon (b - a) \right) + \left( \epsilon (b - a) - \underline{\int_a^b} f_n dx \right) \\
> > 0 \le \overline{\int_a^b} f - \underline{\int_a^b} f < 2 \epsilon (b - a)
> > \end{align*}
> > $$
> > 
> > Thus, by squeeze theorem, the upper and lower integral of $f$ is the same, so $f$ is integrable. Knowing that $f$ is integrable, we can now integrate our first inequality to get
> > $$
> > \begin{align*}
> > \int_a^b f_n (x) dx - \epsilon (b - a) < \int_a^b f(x) < \int_a^b f_n (x) dx + \epsilon (b - a) \\
> > \left| \int_a^b f_n (x) - \int_a^b f \right|  < \epsilon (b - a)
> > \end{align*}
> > $$
> > Letting $\epsilon \to 0$, we get equality! So, as $\epsilon \to 0$, $\int_a^b f_n \to \int_a^b f$.

> [!Abstract] Theorem: Differentiation and Uniform Convergence
> Let $f_n \in C^1 (D)$ for all $n$. Suppose $f_n \to f$ pointwise on $D$, and suppose $f_n' \to g$ uniformly on $D$, where $g$ is some function.
> 
> Then, $g(x) = f'(x)$, and $f' \in C^1 (D)$.
>
> > If we don't know the limit $g$, we can also find that $f_n'$ is uniformly Cauchy.
>
> > [!Note]- Proof
> > 
> > $\forall x, x_0 \in D$, we have that
> > $$
> > f_n (x) - f_n (x_0) = \int_{x_0}^x f_n' (t) dt
> > $$
> > 
> > Taking the limit as $n \to \infty$, we get
> > $$
> > \begin{align*}
> >     \lim_{n\to\infty} f_n (x) - f_n (x_0) = \lim_{n\to\infty} \int_{x_0}^x f_n' (t) dt \\
> >     f(x) - f(x_0) = \int_{x_0}^x g(t) dt
> > \end{align*}
> > $$
> > 
> > Since the map $x \to \int_{x_0}^x g$ is continuous, we get that $f$ is continuous. 
> > 
> > Also, $f'(x) = g(x)$, as we take the derivative of both sides and apply the second fundamental theorem. Note that this works because $g$ is continuous, as $f_n'$ are continuous, and they converge uniformly to $g$.

# Power Series
A **power series** is defined as
$$
f(x) = \sum_{n=0}^\infty a_n (x - x_0)^n
$$
> We'll typically just use $x_0 = 0$.

We can often find the domain of $f$ using a Ratio Test (or Root Test) where we check the endpoints as well. Can we differentiate and integrate this series?

> [!Abstract] Theorem (9.40 Fitzpatrick)
> Define the power series
> $$
> f(x) = \sum_{k=0}^\infty a_k x^k
> $$
> 
> And let $x_0$ be in its domain of convergence, $D$. Furthermore, let $0 < r < |x_0|$.
> 
> Then, $[-r, r] \subseteq D$ and 
> $$
> \sum_{k=0}^\infty a_k x^k \qquad \sum_{k=1}^\infty a_k k x^{k-1} 
> $$
> Both converge uniformly on $[-r, r]$.
> 
> > This means that the partial sums converge uniformly!

This does not mean that we have uniform convergence on $D$! For example,

> [!Example]+ Example: Uniform Convergence Counterexample
> $$
> f(x) = \sum_{n=0}^\infty x^n = \frac{1}{1 - x}
> $$
> 
> We have that the domain of convergence is $(-1, 1)$. Since our partialsums are bounded on $(-1, 1)$, but the limit is unbounded, we cannot have uniform convergence!

> [!Abstract] Theorem: Integrability of Power Series
> Let $[a,b] \subseteq (-r, r) \subset D$, where
> $$
> f(x) = \sum_{k=0}^\infty a_k x^k
> $$
>
> Then, we're allowed to integrate our term!
> $$
> \int_a^b f(x) dx = \sum_{k=0}^\infty \left( \int_a^b a_k x^k dx \right) = \sum_{k=0}^\infty a_k \frac{x^{k+1}}{k + 1} \bigg\vert_a^b
> $$
>
> > [!Note]- Proof
> > 
> > We know by Theorem 9.40 that our partial sums converge uniformly.
> > 
> > So,
> > $$
> > \lim_{n\to\infty} \int_a^b s_n (x) dx = \int_a^b \lim_{n\to\infty} s_n (x) dx
> > $$
> > > This is enabled by our uniform convergence!
> > 
> > This simplifies to 
> > $$
> > \begin{align*}
> > &\sum_{k=0}^\infty \left( \int_a^b a_k x^k \right) = \lim_{n\to\infty} \int_a^b s_n (x) dx = \int_a^b \lim_{n\to\infty} s_n (x) dx = \int_a^b f(x) dx \\
> > &\int_a^b f(x) dx = \sum_{k=0}^\infty \frac{a_k x^{k+1}}{k+1} \bigg\vert_a^b
> > \end{align*}
> > $$

> [!Abstract] Theorem: Differentiability of Power Series
> Let $(-r, r) \subset D$ where
> $$
> f(x) = \sum_{k=0}^\infty a_k x^k
> $$
>
> Then, $f \in C^\infty (-r, r)$ and 
> $$
> f^n (x) = \sum_{k=n}^\infty a_k \frac{d^n}{dx^n} x^k = \frac{k!}{(k - n)!} x^{k - n}
> $$
> 
> > Note that $f^n (0) = a_n n!$, as we have a $0^0$ term which we define as equal to 1.
> 
> > [!Note]- Proof
> > 
> > We know the partial sums $\{ s_n (x) \}$ and $\{ s_n' (x) \}$ converge uniformly on $[-R, R] \subseteq (-r, r)$ by Theorem 9.40.
> > 
> > So $s_n \to f$ uniformly on $[-R, R]$, $s_n' \to g$ uniformly to some $g$. But as $s_n \to f$, then $s_n' = f'$ by property of uniform convergence, so $s_n \to f'$ uniformly on $[-R, R]$. Taking our limit, we get
> > $$
> > \begin{align*}
> > \lim_{n\to\infty} s_n' (x)
> > &=\lim_{n\to\infty} \frac{d}{dx} \sum_{k=0}^n a_k x^k \\
> > &= \lim_{n\to\infty} \sum_{k=1}^n a_k k x^{k-1} \\
> > &= f'(x) = \frac{d}{dx} \sum_{k=0}^\infty a_k x^k
> > \end{align*}
> > $$
