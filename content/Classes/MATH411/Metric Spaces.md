---
title: Metric Spaces
tags:
- math411
---

# Metric Spaces
## Introduction and Common Metrics
A set $X$ and a function of two variables $d : X \times X \to \mathbb{R}$ is a **metric space** if for for all $u,v,w \in X$, the following 3 properties are true: 
1. **Non-Negativity**: $d(u,v) \ge 0$, and $d(u,v) = 0$ if and only if $u = v$
2. **Symmetry**: $d(u,v) = d(v,u)$, $\forall u,v \in X$
3. **Triangle Inequality**: $d(u,v) \le d(u, w) + d(w, v)$, $\forall u,v,w \in X$.

In this case, we call $d$ a **metric** on $X$. Note that a single set could have multiple valid metrics, though there are some metrics that are more commonly used than others.
> Note that if $Y$ is a metric space with metric $d$, then any $X \subseteq Y$ is also a metric space with metric $d$.

We describe 3 of the most important metric spaces in the below theorems.

> [!Abstract] Theorem: Common Metric on $\mathbb{R}$
> For any two real numbers $p, q \in \mathbb{R}$, we have the metric on $\mathbb{R}$
> $$
> d(p,q) = | p - q |
> $$
> 
> > The proof for the metric is trivial, as it all follows from properties of absolute values.

> [!Abstract] Theorem: Common Metric on $\mathbb{R}^n$
> For any two points $p,q \in \mathbb{R}^n$, we have the metric on $\mathbb{R}^n$, otherwise known as the **norm**,
> $$
> d(p,q) = || p - q || = \sqrt{\sum_{i=1}^n (p_i - q_i)^2}
> $$
> 
> > Like the prior metric, the properties for the norm can be proven fairly easily. 

> [!Example]- Example: Norms (1)
> In $\mathbb{R}^2$, some of the following are examples of norms.
>
> We have the typical norm we are used to, $||x|| = \sqrt{x_1^2 + x_2^2}$.
> 
> But we also have other options for norms! For example,
> $$
> \begin{align*}
> || x ||_1 = |x_1| + |x_2| \\
> || x ||_\infty = \max( |x_1|, |x_2| )
> \end{align*}
> $$
>
> The proof for the former is trivial. For (3) of the latter, note that
> $$
> \begin{align*}
> || x + y ||_\infty &= \max\{ |x_1 + y_1|, |x_2 + y_2| \} \\ &\le \max\{ |x_1| + |y_1|, |x_2| + |y_2| \} \\ &\le \max\{ |x_1|, |x_2| \} + \max\{ |y_1|, |y_2| \}
> \end{align*}
> $$
>
> And comparing the norms, we find that
> $$
> \max\{ |x_1|, |x_2| \} \le \sqrt{x_1^2 + x_2^2} \le |x_1| + |x_2| \le 2 \max\{|x_1|, |x_2| \}
> $$
> So in finite dimensions, we find that convergence along any one of the norms implies convergence along the others, by squeeze!
> > This fails to hold in infinite dimenions!

> [!Abstract] Theorem: Common Metric on $C([a,b], \mathbb{R})$
> Let $C([a,b], \mathbb{R})$ be the set of all continuous functions $f : [a,b] \to \mathbb{R}$.
> 
> For any two functions $f,g \in C([a,b], \mathbb{R}$, we have the metric
> $$
> d(f,g) = \max_{x \in [a,b]} |f(x) - g(x)|
> $$
> > This finds the maximum single difference between the functions in the interval $[a,b]$!

> [!Example]+ Remark
> In the metric space $C([0,1], \mathbb{R})$, with norm 
> $$
> ||f|| = \max_{x \in [0,1]} |f(x)|
> $$
> We find that closed and bounded sets need not be sequentially compact.
> 
> For example, consider the set $B =  \{ f : ||f|| \le 1 \}$, and take sequence $f_k (x) = x^k$ in $B$. Then, 
> $$
> f_k (x) = 
> \begin{cases}
> 0 & 0 \le x < 1 \\
> 1 & x = 1
> \end{cases}
> $$
> Converges pointwise. However, there does not exist a convergent $f_{k_l}$!

> [!Example]- Example: Norms (2) 
> Let $X$ be a set of continuous functions on $[a,b]$ to $\mathbb{R}$.
> $$
> x = C ( [a,b],\mathbb{R} ) = \{ f : [a,b] \to \mathbb{R}, f \text{ continuous} \}
> $$
> 
> We can define the following norms and verify them. Note that we only verify their triangle inequalities, as the rest is obvious to show.
>
> We define the norm $||f|| = ||f||_\infty = \max_{x \in [a,b]} |f(x)|$. 
> $$
> \begin{align*}
> \max_{x \in [a,b]} |f_1 (x) + f_2 (x)| \le \max_{x\in[a,b]} |f_1(x)| + \max_{x\in[a,b]} |f_2(x)|
> \end{align*}
> $$
> 
> We can also define the norm $||f||_1 = \int_a^b |f(x)| dx$.
> $$
> \int_a^b | f_1(x) + f_2(x) | dx \le \int_a^b |f_1(x)| dx + \int_a^b |f_2(x)| dx
> $$
> 
> We can also define $||f||_2 = \left( \int_a^b f^2 (x) dx \right)^{1/2}$.
> $$
> \begin{align*}
> \left( \int_a^b (f_1(x) + f_2(x))^2 \right)^{1/2} 
> &= \left( \int_a^b f_1(x)^2 + \int_a^b 2 f_1(x) f_2(x) + \int_a^b f_2(x)^2 \right)^{1/2} \\
> &\le \left( \int_a^b f_1(x)^2 + 2 \int_a^b (f_1^2 (x))^{1/2} (f_2^2(x))^{1/2} + \int_a^b f_2(x)^2 \right)^{1/2} \\
> &\le \left( \int_a^b f_1^2 (x) \right)^{1/2} + \left( \int_a^b f_2^2 (x) \right)^{1/2}
> \end{align*}
> $$

> [!Abstract] Theorem: The Discrete Metric
> Let $X$ be any set. For any two points $p, q \in X$, we have metric known as **discrete metric**
> $$
> d(p,q) = 
> \begin{cases}
> 0 & p = q \\ 1 & p \ne q
> \end{cases}
> $$

## Generalized Metric Space Definitions
With metric spaces, we can generalize many of the definitions we had previously, by using our metric as a "distance" function! In fact, many of our definitions (ex. open sets) were given in terms of the norm $|| \cdot ||$.

Let $X$ be a metric space. 

A sequence $\{p_k\} \subseteq X$ is said to **converge** to a point $p \in X$, if $\forall \epsilon > 0$, $\exists N \in \mathbb{N}$ such that
$$
d(p_k, p) < \epsilon \qquad \forall k \ge N
$$
We call $p$ the **limit** of the sequence $\{p_k\}$. Note that by this definition, we can see that a sequence converges if and only if the real sequence $\{d(p_k, p)\} \to 0$.

We also have the following set definitions:
- For a point $p \in X$, $r > 0$, the set
  $$
  B_r (p) = \{ q \in X : d(q,p) < r \}
  $$
  is the **open ball** around $p$ in $X$.
- $A \subseteq X$ is **open** if $\forall p \in X$, $\exists r > 0$ such that $B_r(p) \subseteq X$.
- $A \subseteq X$ is **closed** if $\forall \{p_k\} \subseteq A$, if $\{p_k\} \to p \in X$, then $p \in A$.
- For $A \subseteq X$, a point $p \in A$ is an **interior point** if $\exists r > 0$ where $B_r (p) \subseteq A$.

> [!Abstract] Theorem: The Complementing Characterization
> Let $X$ be a metric space, and $A \subseteq X$. Then, $A$ is open if and only if $A^c$ is closed in $X$.

> [!Abstract] Theorem: Open and Closure of $X$ in Itself
> Let $X$ be a metric space. Then, $X$ is open in $X$, and $X$ is also closed in $X$!

> [!Abstract] Theorem: Intersection and Union of Closed / Open Sets
> Let $X$ be a metric space.
>
> Then, 
> - The union of a (potentially infinite) collection of open subsets of $X$ is open. 
> - The intersection of a finite collection of open subsets of $X$ is open.
>
> Also,
> - The union of a finite collection of closed subsets of $X$ is closed.
> - The intersection of a (potentially infinite) collection of closed subsets of $X$ is closed.

## Completeness and the Contraction Mapping Principle 
Let $X$ be a metric space. Then, a sequence $\{p_k\} \subseteq X$ is **Cauchy** if $\forall \epsilon > 0$, $\exists K$ such that
$$
d(p_k, p_l) < \epsilon \qquad \forall k,l \ge K
$$

> [!Abstract] Theorem: Convergence and Cauchy Sequences
> Every convergent sequence is a Cauchy sequence.

> [!Example] Example: Cauchy Sequences in $C([a,b], \mathbb{R})$
> Consider a sequence $\{f_k\} \subseteq C([a,b], \mathbb{R})$. Then, from definition of the metric, $\{f_k\}$ is a Cauchy sequence if and only if $\forall \epsilon > 0$, $\exists N \in \mathbb{N}$ such that
> $$
> | f_k (x) - f_l (x) | < \epsilon \qquad \forall x \in [a,b] \quad k, l \ge N
> $$
> > Note that this must hold, as the metric takes the maximum difference between the functions.
>
> In other words, $\{f_k\}$ is cauchy if and only if it is **uniformly cauchy** (converges uniformly).

We say metric space $X$ is **complete**, if $\forall \{p_k\}$ Cauchy sequence in $X$, $\exists p \in X$ such that $\{p_k\} \to p$. In other words, all Cauchy sequences converge to a point in $X$. 

> [!Info] Remark
> The metric spaces $\mathbb{R}, \mathbb{R}^n, C([a,b], \mathbb{R})$ are complete.

> [!Example]- Example: Incomplete Space
> We can find that $C([a,b], \mathbb{R})$ and 
> $$
> d_1 (f,g) = \int_a^b | f(x) - g(x) | dx
> $$ 
> is not complete.
> 
> We form a series of functions that converge to a function that is not continuous (and thus not in our space).
> 
> Lets consider $f_n : [0,2] \to \mathbb{R}$ where
> $$
> f_n (x) =
> \begin{cases}
> x^n & 0 \le x \le 1 \\
> 1 & 1 \le x \le 2
> \end{cases}
> $$
> Then,
> $$
> \int_0^2 | f_n (x) - f(x) | dx = 0
> $$
> If $f(x) = 0$ for $0 \le x < 1$, $f(x) = 1$ for $1 \le x \le 2$.
> 
> So, $f_n \to f$ with respect to the $d_1$ metric, so $f_n$ is Cauchy. However, there does not exist a $g$ that is continuous from $[0,2]$ with real values such that
> $$
> \int_0^2 | f - g | dx = 0
> $$

> [!Abstract] Theorem: Complete Subspaces
> Let $X$ be a complete metric space, and $Y$ a subspace of $X$. Then, $Y$ is a complete metric space if and only if $Y$ is a closed subset of $X$.
> > A corollary from this is that, every closed subset of $R, \mathbb{R}^n, C([a,b], \mathbb{R})$ is a complete metric space (from the previous remark).

Let $X$ be a metric space, and $T : X \to X$ be a function. Then, $T$ is **Lipschitz** if $\exists M \ge 0$ such that
$$
d(T(p), T(q)) \le M d(p, q)
$$
For all $p,q \in X$. In other words, the change in distance between any two points $p,q$ after the mapping is bounded by some value.
> Note that the same $M$ must work for all $p,q$ pairs.

A Lipschitz function $T : X \to X$ is a **contraction** if $M < 1$. That is, there exists a $0 \le c < 1$ such that
$$
d(T(p), T(q)) \le c \cdot d(p,q)
$$

> [!Info] Lipschitz Functions on $\mathbb{R}$
> If $f : \mathbb{R} \to \mathbb{R}$ differentiable, then $f$ is Lipschitz with constant $M$ if and only if $|f'(x)| \le M$.
> 
> > [!Note]- Proof
> > 
> > #### Proof $\rightarrow$
> > If $f$ is differentiable and Lipschitz, then by definition of Lipschitz functions, $\forall x,y \in \mathbb{R}$,
> > $$
> > | f(x) - f(y) | \le M |x - y|
> > $$
> > 
> > And
> > $$
> > f'(x) = \lim_{h \to 0} \frac{f(x + h) - f(x)}{h}
> > $$
> > So, applying our Lipschitz definition,
> > $$
> > |f'(x)| \le \lim_{h \to 0} \left| \frac{f(x + h) - f(x)}{h} \right| \le M 
> > $$
> > 
> > #### Proof $\leftarrow$
> > Conversely, if $\forall x \in \mathbb{R}$, $|f'(x)| \le M$, then we want to show that $\forall x,y$,
> > $$
> > | f(x) - f(y) | \le M |x - y| 
> > $$
> > As $f$ is differentiable, by the mean value theorem, there exists a $c$ between $x,y$ such that
> > $$
> > |f'(c)| = \left| \frac{f(x) - f(y)}{x - y} \right| \le M
> > $$
> > We multiply $x - y$ on either side to find our result.

If $X$ is a metric space, and $T : X \to X$ is a function, then $p \in X$ is called a **fixed point** if
$$
T(p) = p
$$
In other words, the point after being mapped does not change.

With some assumptions on $T$, we can guarantee the existence of a fixed point for a function $T$.

> [!Abstract] Theorem: The Contraction Mapping Principle
> Let $X$ be a complete metric space, and suppose $T : X \to X$ is a contraction. Then, $T : X \to X$ has exactly one fixed point.
> 
> > [!Note]- Proof
> > 
> > #### Proof (Uniqueness)
> > Say $T(p_1) = p_1$, and $T(p_2) = p_2$. By contraction, we find a $0 \le c < 1$ such that
> > $$
> > | T(p_1) - T(p_2) | \le c | p_1 - p_2 | \Longrightarrow |p_1 - p_2| \le c |p_1 - p_2|
> > $$
> > This is only possible if $p_1 = p_2$.
> > 
> > #### Proof (Existence)
> > Start with any $p_0 \in X$. Let $p_1 = T(p_0), p_2 = T(p_1), \dots$. We show that the sequence of points $\{p_k\}$ is Cauchy, thus there exists a $p$ where $\{p_k\} \to p$, and $T(p) = p$.
> > 
> > First, look at the distance between adjacent terms in the sequence.
> > $$
> > \begin{align*}
> > &d(p_2, p_1) = d(T(p_1), T(p_0)) \le C d(p_1, p_0) \\
> > &d(p_3, p_2) = d(T(p_2), T(p_1)) \le C d(p_2, p_1) \le C^2 d (p_1, p_0) \\
> > &\vdots \\
> > &d(p_{k+1}, p_k) \le C^k d(p_1, p_0)
> > \end{align*}
> > $$
> > Thus, we find that
> > $$
> > \begin{align*}
> > d(p_{k+l}, p_k) 
> > &\le d(p_{k+l}, p_{k+l-1}) + d(p_{k+l-1}, p) \\
> > &\le d(p_{k+l}, p_{k+l-1}) + d(p_{k+l-1}, p_{k+l-2}) + d(p_{k+l-1}, p) \\
> > &\le \dots \\
> > &\le (C^{k+l-1} + C^{k+l-2} + \dots + C^k) d(p_1, p_0) \\
> > &\le C^k \left( \sum_{m=0}^\infty C^m \right) d(p_1, p_0) \\
> > &= C^k \frac{1}{1-C}
> > \end{align*}
> > $$
> > Thus, our sequence is Cauchy! 
> > 
> > #### Bringing it Together
> > Let $\{p_k\} \to p$. We show that $T(p) = p$.
> > 
> > We essentially show that $T$ is continuous, so that if $\{p_k\} \to p$, then $\{T(p_k)\} \to T(p)$.
> > $$
> > d(T(p_k), T(p)) \le C d(p_k, p) \to 0
> > $$
> > By squeeze. So, $\{T(p_k)\} \to T(p)$.
> > 
> > We know that $\{p_k\} \to p$, and $\{p_{k+1}\} \to T(p)$, so $T(p) = p$ by the uniqueness of limits.
> > > Note that by this, Lipschitz functions are essentially a stronger form of continuity!

> [!Example]- Example: The Contraction Mapping Principle
> Let $X = \{ F \in C([0, \frac{1}{2}],\mathbb{R}) : 0 \le f(x) \le 4 \quad \forall x \in [0, \frac{1}{2}] \}$. Let $T : X \to C([0, \frac{1}{2}], \mathbb{R})$ be given as
> $$
> T(f(x)) = 1 + \int_0^x f(t) dt
> $$
> 
> #### Part 1
> Show that $T$ maps $X$ onto $X$.
> 
> Take any $f \in X$. We wish to show that $T(f) \in X$.
> $$
> \begin{align*}
> T(f) 
> &= 1 + \int_0^x f(t) dt \\
> &\le 1 + \frac{1}{2} \max_{x \in [0,1/2]} f(x) \\
> &\le 1 + \frac{1}{2} 4 \\
> &\le 3
> \end{align*}
> $$
> 
> And furthermore, because $f(x) \ge 0$, 
> $$
> T(f) = 1 + \int_0^x f(t) dt \ge 1
> $$
> 
> So, $1 \le T(f) \le 3$, meaning $T(f) \in X$! 
> 
> #### Part 2
> Is $T: X \to X$ a contraction?
> 
> Take any $f_1, f_2 \in X$. To show that $T$ is a contraction, we wish to show that for some $M < 1$,
> $$
> \begin{align*}
> d(T(f_1), T(f_2)) 
> &\le M d(f_1, f_2) \\
> \max_{x \in [0,\frac{1}{2}]} \left| \int_0^x f_1 (t) - f_2 (t) dt \right| 
> &\le 
> \max_{x \in [0,\frac{1}{2}]} \int_0^x |f_1(t) - f_2(t)| dt \\
> &\le
> \frac{1}{2} \max_{x \in [0,\frac{1}{2}]} |f_1(t) - f_2(t)|
> \end{align*}
> $$
> 
> We find $M = 1/2$! So, $T$ is a contraction.
> 
> #### Part 3
> Write down a fixed point of $T$.
> 
> For a fixed point of $T$,
> $$
> T(f) = f \Longrightarrow f(x) = 1 + \int_0^x f(t) dt
> $$
> This gives us system
> $$
> \begin{cases}
> f'(x) = f(x) \\
> f(0) = 1
> \end{cases}
> $$
> 
> Which has a solution of $e^x$. $e^x$ is a fixed point of our system! 

This theorem is quite important in differential equations!

## The Existence Theorem for Nonlinear Differential Equations
Let $I$ be an open interval of real numbers, $x_0 \in I$. Then, for $y_0$ and a function $h : I \to \mathbb{R}$, consider the differential system.
$$
\begin{cases}
f'(x) = h(x) & \forall x \in I \\
f(x_0) = y_0 
\end{cases}
$$

We ask, does there exist a differentiable function $f : I \to \mathbb{R}$ that satisfies the above differential equation?

Previously, we established that given $h$ continuous, there does exist an $f$, and this $f$ is unique with formula
$$
f(x) = y_0 + \int_{x_0}^x h(t) dt \qquad \forall x \in I
$$

Now, we consider much more general differential systems. 

Suppose $O$ is an open subset of $\mathbb{R}^2$, and let $(x_0, y_0) \in O$. Also suppose that we have a continuous function $g : O \to \mathbb{R}$. 

Let $I$ be an interval in $\mathbb{R}$, and define the function $f : I \to \mathbb{R}$ such that the set of inputs/outputs is contained within $O$.
$$
\{ (x,f(x)) : x \in I\} \subseteq O
$$

We ask, can we find this interval $I$ containing $x_0$, and a differentiable function $f(x)$ satisfying
$$
\begin{cases}
f'(x) = g(x,f(x)) \\
f(x_0) = y_0
\end{cases}
$$
> Note how now, the derivative of our $f$ is given in terms of $f$ as well!

We use this setup from here on.

> [!Abstract] Lemma: The Equivalence Lemma
> Let $O$ be an open subset of $\mathbb{R}^2$ with the point $(x_0, y_0)$, and suppose we have $g : O \to \mathbb{R}$ continuous.
>
> If $I$ is a neighborhood of the point $x_0$, and $f : I \to \mathbb{R}$ has the property that $(x, f(x)) \in O$ for all $x \in I$, then the following two are equivalent:
> - The function $f : I \to \mathbb{R}$ is differentiable and is a solution of the differential equation
>   $$
>   \begin{cases}
>   f'(x) = g(x,f(x)) & \forall x \in I \\
>   f(x_0) = y_0 
>   \end{cases}
>   $$
> - The function $f : I \to \mathbb{R}$ is continuous and is a solution of the integral equation
>   $$
>   f(x) = y_0 + \int_{x_0}^x g(t, f(t)) dt \qquad \forall x \in I
>   $$
> 
> > [!Note]- Proof 
> > 
> > #### Proof $\rightarrow$
> > Assume (1). Then, $f$ differentiable implies $f$ continuous, and because $f'(x) = g(x, f(x))$ (a composition of continuous functions), $f'$ is also continuous. So, by the fundamental theorem of calculus, we find
> > $$
> > \begin{align*}
> > f(x) - y_0 = f(x) - f(x_0) = \int_{x_0}^x f'(t) dt = \int_{x_0}^x g(t, f(t)) dt
> > \end{align*}
> > $$
> > Which is formula 2.
> > 
> > #### Proof $\leftarrow$
> > Assume (2). Since $f(x) = y_0 + \int_{x_0}^x g(t, f(t)) dt$, and $g$ is continuous (as remarked earlier), we know the integral of a continuous function is differentiable. So, $f$ is differentiable, and
> > $$
> > f'(x) = g(x, f(x))
> > $$
> > Also, $f(x_0) = y_0$ can be obtained as $\int_{x_0}^{x_0} g(t, f(t)) dt = 0$.

Let's define a function $T(f)$ as the equation in point 2 of the equivalence lemma.
$$
T(f) = y_0 + \int_{x_0}^x g(t,f(t)) dt
$$

Using this function $T(f)$, with an additional constraint on $g$, we can guarantee the existence of a unique solution for our system! This is known as the Existence and Uniqueness Theorem. 

> [!Abstract] Theorem: Existence and Uniqueness
> Let $O$ be an open subset of the plane $\mathbb{R}^2$ that contains the point $(x_0, y_0)$. Suppose that the function $g : O \to \mathbb{R}^2$ is continuous.
>
> Now, assume an additional constraint, that $\exists M > 0$ such that $\forall (x,y_1), (x, y_2) \in O$,
> $$
> | g(x,y_1) - g(x,y_2) | \le M | y_1 - y_2 |
> $$
> 
> Then, there is an open interval $I$ with $x_0$ such that the differential equation
> $$
> \begin{cases}
> f'(x) = g(x,f(x)) & x \in I \\
> f(x_0) = y_0
> \end{cases}
> $$
> Has exactly one solution.
> 
> > [!Note]- Proof: Existence and Uniqueness
> > 
> > Because $O$ is open, we can choose numbers $a, b > 0$ such that the box of width $2a$, height $2b$ centered around $(x_0, y_0)$ is contained within $O$.
> > $$
> > R = [x_0 - a, x_0 + a] \times [y_0 - b, y_0 + b] \subseteq O
> > $$
> > 
> > For some positive number $0 < l \le a$, let $I_l$ be the closed interval $[x_0 - l, x_0 + l]$, and define
> > $$
> > X_l = \{ f : [x_0 - l, x_0 + l] \to [y_0 - b, y_0 + b], \text{Continuous} \}
> > $$
> > Or in other words, the set of all continuous functions along our interval $I_l$. Note that the domain and image of these functions are contained within our box $R$ by assumption. 
> > 
> > For a function $f \in X_l$, we define the function $T(f)$ in $C(I_l, \mathbb{R}$ as
> > $$
> > T(f)(x) = y_0 + \int_{x_0}^x g(t, f(t)) dt \qquad \forall x \in I_l
> > $$
> > 
> > We now prove two conditions: 
> > 1. $T$ maps the space $X_l$ to itself
> > 2. $T : X_l \to X_l$ is a contraction
> > 
> > Then, by the Contraction Mapping Principle, we have a unique fixed point.
> > 
> > #### $T : X_l \to X_l$
> > Because we $g(x,y)$ is continuous on a compact set, we know that $\exists K$ such that $|g(x,y)| \le K$ for all $(x,y)$ in our box $R$.
> > 
> > Then, if $f \in X_l$, and $x \in I_l$ (so $x \in [x_0 - l, x_0 + l]$), we have
> > $$
> > \begin{align*}
> > | T(f)(x) - y_0 |
> > &= \left| \int_{x_0}^x g(t, f(t)) dt \right| \\
> > &\le |x - x_0| \max_{t \in [x_0 - l, x_0 + l]} | g(t, f(t)) | \\
> > &\le |x - x_0| K & \text{Bounds} \\
> > &\le l * K &\text{Domain of Function}
> > \end{align*}
> > $$
> > So, if $Kl \le b$, the range of our function is bounded between $[y_0 - b, y_0 + b]$, meaning $T : X_l \to X_l$. We choose $l$ small enough to make this happen.
> >
> > 
> > #### $T$ is a Contraction
> > We now show that $T : X_l \to X_l$ is a contraction provided $l$ is sufficiently small. We want
> > $$
> > d(T(f_1), T(f_2)) \le C d(f_1, d_2)
> > $$
> > Where $d$ is the uniform metric. 
> > $$
> > \begin{align*}
> > T(f_1)(x) - T(f_2)(x) &= \int_{x_0}^x g(t, f_1 (t)) dt - g(t, f_2 (t)) dt \\
> > | T(f_1)(x) - T(f_2)(x) | &= \left| \int_{x_0}^x g(t, f_1 (t)) dt - g(t, f_2 (t)) dt \right| \\
> > &\le \int_{x_0}^x | g(t, f_1 (t)) dt - g(t, f_2 (t)) | dt &\text{Integral Property} \\
> > &\le \int_{x_0}^x M(f_1(t) - f_2(t)) dt &\text{Assumption on g} \\
> > &\le M (x - x_0) \max_{t \in [x_0 - l, x_0 + l]} | f_1(t) - f_2(t) | \\
> > &\le M \cdot l \cdot \max_{t \in [x_0 - l, x_0 + l]} | f_1(t) - f_2(t) | = M \cdot l \cdot d(f_1, f_2)\\
> > \end{align*}
> > $$
> > So, we found that
> > $$
> > d(T(f_1), T(f_2)) \le M l d(f_1, f_2)
> > $$
> > As $M$ is fixed, and we can determine $l > 0$, we make $l$ as small as we want! So, provided that $Ml < 1$, we have a contraction.
> >
> > Thus, by the Contraction Mapping Principle, there is exactly one fixed point for $T$. In other words, there exists a unique $f : (x_0 - l, x_0 + l) \to (y_0 - b, y_0 + b)$ such that $f'(x) = g(x, f(x)), f(x_0) = y_0$.

This is a really important proof!

Note that there are many constraints that this theorem assumes in order for our result to hold; below, we address some common misconceptions.

> [!Info] Remark: Failure of Uniqueness 
> There are examples of continuous $g$ for which uniqueness fails. Consider 
> $$
> f'(t) = 3 f(t)^{2/3} \qquad f(0) = 0
> $$
> 
> Then, we can find the following solutions that are non-unique.
> $$
> f(t)
> = 
> \begin{cases}
> 0 & t \le 0 \\
> t^3 & t \ge 0 
> \end{cases} \qquad f(t) = 0
> $$
>
> In fact, we can find any solution of the form
> $$
> f(t) = \begin{cases}
> 0 & t \le C \\
> (t - C)^3 & t \ge C
> \end{cases}
> $$
> 
> And find that in fact, our initial problem fails the Lipschitz condition, as for $g(t,y) = 3 y^{2/3}$, $g_y$ is **unbounded** as $y \to 0$.

> [!Info] Remark: Existence is a Local Property
> Consider system
> $$
> f'(t) = f^2 (t) \qquad f(0) = 0
> $$
>
> Note that one solution to this is $f(t) = 1 / (1 - t)$, which only works for $(-\infty < t < 1)$.

> [!Info] Remark 3
> Let $g : \mathbb{R}^2 \to \mathbb{R}$, and assume that
> $$
> | g(t,y_1) - g(t,y_2) | \le M |y_1 - y_2| 
> $$
> For some $M > 0$, and for all $(x,y_1), (x,y_2)$.
> 
> If $f_1' (t) = g(t, f_1(t))$, $f_1 (t_0) = y_0$, and $f_2' (t) = g(t, f_2(t))$, $f_2 (t_0) = y_0$, then $f_1(t) = f_2(t)$ for all $t$.
> 
> > [!Note]- Proof
> > 
> > Look at $E(t) = (f_1 (t) - f_2 (t))^2$. We find that
> > $$
> > \begin{align*}
> > E'(t) 
> > &= 2 (f_1(t) - f_2(t)) (f_1'(t) - f_2'(t)) \\
> > &\le 2 | f_1 (t) - f_2 (t) | | g(t, f_1(t)) - g(t, f_2(t)) | \\
> > &\le 2M | f_1 (t) - f_2 (t) | | f_1 (t) - f_2 (t) | = 2M E(t)
> > \end{align*}
> > $$
> > 
> > Thus, $E'(t) \le 2M E(t)$, $E(t_0) = 0$.
> > $$
> > \begin{align*}
> > E'(t) - 2ME(t) \le 0 \\
> > \frac{d}{dt} E(t) e^{-2Mt} = E'(t) e^{-2Mt} - 2M E(t) e^{-2Mt} \le 0
> > \end{align*}
> > $$
> > Because $E(t) e^{-2Mt}$ is monotonically decreasing, and it is 0 at $t_0$, and $E(t) e^{-2t} \ge 0$ for all $t$, we know that
> > $$
> > E(t) = 0
> > $$
> > Which forces $f_1 (t) = f_2 (t)$.
>
> > [!Note]- Proof (2)
> > 
> > Let $f_1, f_2 : \mathbb{R} \to \mathbb{R}$ differentiable, satisfying
> > $$
> > f_1'(t) = g(t, f_1(t)) \qquad f_2'(t) = g(t, f_2(t))
> > $$
> > And $f_1(t_0) = f_2(t_0) = y_0$. Also assume the Lipschitz condition
> > $$
> > | g(t,y_1) - g(t, y_0) | \le M |y_1 -  y_2|
> > $$
> > 
> > From our main theorem, $\exists l > 0$ such that $f_1 (t) = f_2 (t)$ $\forall |t - t_0| < l$.We wish to show that this holds for all $t$. 
> > 
> > Look at the set $S = \{ t : f_1(t) = f_2(t) \}$. We find that
> > - Because $f_1, f_2$ are continuous, then $S$ is closed! 
> > - $S$ is open. Let $t_1 \in S$. Thus, $f_1 (t_1) = f_2 (t_1)$, and there exists a $\delta > 0$ such that $f_1(t) = f_2(t)$ $\forall |t - t_1| < \delta$, by from the local uniqueness theorem applied to $t_1$.
> > 
> > Because $S$ is open and closed, the only set that satisfies this is the empty set, or the entire space! Because $t_0 \in S$, we find that $S$ must be the entire space. 
