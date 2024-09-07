---
title: MATH411
tags:
- math411
---

MATH411 is a continuation of MATH410, but into $n$ dimensions ($\mathbb{R}^n$). 

$R^n$ is a vector space, with vectors and scalars (respectively) given as
$$
u = (u_1, u_2, \dots u_n) \in \mathbb{R}^n, u_i \in \mathbb{R}
$$
Satisfying vector addition and scalar multiplication.

with an inner product commonly known as the **dot product**
$$
<u, v> = u_1 v_1 + \dots + u_n v_n
$$
Satisfying the following axioms of a (real) inner product space:
- $<u,v> = <v,u>$
- $<\alpha u + \beta v, w> = \alpha <u, w> + \beta <v, w>$
- $<u, u> \ge 0$, and $<u, u> = 0$ if and only if $u = 0$.
- $|| u ||^2 = <u, u>$

> [!Abstract] Theorem: Inner Product in $\mathbb{R}^2$
> In $\mathbb{R}^2$, $<u, v> = || u || \cdot || v || \cos \theta$ where $\theta$ is the angle between the two vectors.
>
> > [!Note]- Proof
> > 
> > Using polar coordinates, we can convert our vectors into the polar space 
> > $$
> > u = ||u|| ( \cos \alpha, \sin \alpha ) \qquad
> > v = ||v|| ( \cos \beta, \sin \beta )
> > $$
> > Where $\alpha$ is the angle of $u$ to the $x$-axis, and $\beta$ is the angle of $v$ to the same axis.
> > 
> > We can find that
> > $$
> > <u,v> = ||u|| ||v|| (\cos \alpha \cos \beta + \sin \alpha \sin \beta) = ||u|| ||v|| \cos(\beta - \alpha)
> > $$

We say that $u$ is **orthogonal** to $v$, $u \perp v$, if $<u, v> = 0$.

> [!Abstract] Theorem: Properties of Orthogonality
> $$
> || u + v ||^2 = || u ||^2 + || v ||^2
> $$
> If and only if $\langle u, v \rangle = 0$.
> 
> > [!Note]- Proof
> >
> > $$
> > \begin{align*}
> > || u + v ||^2 &= \langle u + v, u + v \rangle = \langle u, u \rangle + \langle u, v \rangle + \langle v, u \rangle + \langle v,v \rangle \\
> > &= || u ||^2 + 2 \langle u, v \rangle + ||v||^2
> > \end{align*}
> > $$
> > Which is equal to $||u||^2 + ||v||^2$ if and only if $\langle u, v \rangle = 0$.

> [!Abstract] Cauchy-Schwarz Inequality
> Let $u, v \in \mathbb{R}^n$. Then, 
> $$
> | \langle u, v \rangle | \le || u || \cdot || v ||
> $$
>
> > We prove this using the axioms of inner products only (see above), making generalizable for any inner product!
> 
> > [!Note]- Proof
> > 
> > First, note that if either $u$ or $v$'s normals are 0, then this is trivially true.
> > 
> > Assume that both $||u|| \ne 0$ and $||v|| \ne 0$. Now, take the expression $|| u - \alpha v ||^2$, and note that this is (by an axiom) $\ge 0$.
> > 
> > By a previous proof,
> > $$
> > || u - \alpha v ||^2 = ||u||^2 - 2 \alpha \langle u, v \rangle + \alpha^2 ||v||^2 = ||u||^2 + \alpha(-2 \langle u, v \rangle + \alpha ||v||^2)
> > $$
> > We seek to minimize this with respect to $\alpha$. Ignoring the constants, we minimize
> > $$
> > 2 \langle u, v \rangle + \alpha ||v||^2 = 0 \to \alpha = \frac{\langle u, v \rangle}{||v||^2}
> > $$
> > 
> > Subbing this in, we have
> > $$
> > \begin{align*}
> > 0 &\le || u - \alpha v ||^2 = ||u||^2 - 2 \frac{\langle u, v \rangle}{||v||^2} \langle u, v \rangle + \left( \frac{\langle u, v \rangle}{||v||^2} \right)^2 ||v||^2 = ||u||^2 - \frac{\langle u, v \rangle^2}{||v||^2} \\
> > 0 &\le ||u||^2 - \frac{\langle u, v \rangle^2}{||v||^2} \\
> > \langle u, v \rangle^2 &\le ||u||^2 ||v||^2 \\
> > |\langle u, v \rangle| &\le ||u|| ||v|| \\
> > \end{align*}
> > $$

> [!Info] Corollary
> Note that equality holds if and only if $\exists \alpha \in \mathbb{R}$ such that $u = \alpha v$ (or $v = \alpha u$).
>
> > [!Note]- Proof ($\leftarrow$)
> > 
> > $$
> > u = \alpha v \to | \langle u, v \rangle | = |\alpha| ||v||^2 = ||\alpha v|| ||v|| = ||u|| ||v||
> > $$
> 
> > [!Note]- Proof ($\rightarrow$)
> > 
> > Let $||u|| ||v|| = | \langle u, v \rangle$. Then, if we repeat our original proof, we find that 
> > $$
> > ||u||^2 - \frac{\langle u, v \rangle^2}{||v||^2} = \frac{||u||^2 ||v||^2 - \langle u, v \rangle^2}{||v||^2} = 0
> > $$
> > Telling us that $||u - \alpha v|| = 0$ for our minimizer $\alpha = \frac{\langle u, v \rangle}{||v||^2}$. So, $u - \alpha v = 0$ by an axiom.

> [!Abstract] Theorem: Triangle Inequality
> $$
> || u + v || \le ||u|| + ||v|| \forall u, v \in \mathbb{R}^n
> $$
> 
> > [!Note]- Proof
> > 
> > We find that
> > $$
> > ||u + v||^2 = ||u||^2 + 2 \langle u, v \rangle + ||v||^2 =  ||u||^2 + 2 ||u||^2 ||v||^2 + ||v||^2
> > $$
> > Giving us our triangle inequality due to the Cauchy-Schwarz Inequality.

> [!Abstract] Theorem: Reverse Triangle Inequality
> $$
> || u \pm v || \le \left| ||u|| - ||v|| \right|
> $$
>
> > [!Note]- Proof ($-$)
> > 
> > $$
> > ||u|| = ||u - v + v|| \le ||u - v|| + ||v||
> > $$
> > We also know that
> > $$
> > ||u - v|| \ge ||u|| - ||v||
> > $$
> > Giving us
> > $$
> > ||v - u|| \le ||v|| - ||u||
> > $$

---

# Sequences and Limits in $\mathbb{R}^n$
Consider a sequence in $\mathbb{R}^n$ $\{u_k\}$, $k \in \mathbb{N}$. In other words, each entry in the sequence is a point in $\mathbb{R}^n$.
> Note that we will denote $u^i$ as the projection of the $i^{th}$ element of $u$ ($u$'s $i^{th}$ element).

If $\{u_k\}$ is a sequence in $\mathbb{R}^n$, $u \in \mathbb{R}^n$, then we define the **limit**
$$
\lim_{k\to\infty} u_k = u \quad \text{if} \quad \lim_{k\to\infty} || u_k - u || = 0
$$
We alternatively can write this as **$\{u_k\} \to u$ in the norm**. This is similar in idea to convergence in 1-dimensional series!

But in higher dimensions, this is not the only notion of convergence that we have! We can also say that $\{u_k\} \to u$ **componentwise**, if each $u_k^i \to u^i$ as $k \to \infty$.

> [!Abstract] Theorem: Notions of Convergence
> $\{u_k\} \to u$ in norm if and only if $\{u_k\} \to u$ componentwise.
>
> > [!Note]-  Proof
> > 
> > #### Proof $\rightarrow$
> > Assume that $\{u_k\} \to u$ in norm. Then, for each $1 \le i \le n$, 
> > $$
> > 0 \le | u_k^i - u^i | \le \sqrt{ (u_k^1 - u^1)^2 + \dots + (u_k^n - u^n)^2 } = || u_k - u || \to 0
> > $$
> > So by the squeeze theorem, $|u_k^i - u^i| \to 0$.
> > 
> > #### Proof $\leftarrow$
> > Assume that $\{u_k^i\} \to u^i$. Then,
> > $$
> > || u_k - u || = \sqrt{ (u_k^1 - u^1)^2 + \dots + (u_k^n - u^n)^2 }
> > $$
> > As each component converges to 0 by definition, and sums of sequences converging to 0 also converge to 0, we know that $|| u_k - u || \to 0$.

Note that this does not hold for infinite dimensions! In particular, component-wise convergence does not imply convergence in norm.

For example, say we have a sequence $\{u_k\}$, where for any $k$ the $k^{th}$ element is 1, all other 0. So,
$$
\begin{align*}
    u_1 &= (1, 0, 0 \dots) \\
    u_2 &= (0, 1, 0, \dots)
\end{align*}
$$
We can see that as $k \to \infty$, $\{u_k\} \to \vec{0}$, the 0 vector! However, $||u_k|| \to 1$, so it does not converge in norm to 0.

# Closed and Open Sets in $\mathbb{R}^n$
Let $r > 0$, $u \in \mathbb{R}^n$. We define the **open ball of radius $r$, centered at $u$** as
$$
B_r(u) = \{ v \in \mathbb{R}^n : || u - v || < \mathbb{R} \}
$$
In other words, the set of all $n$-dimensional points that are within some predetermined hypersphere of $u$.

We say that a set $A \subseteq \mathbb{R}^n$ is **open** if $\forall u \in A$, $\exists r > 0$ such that $B_r(u) \subseteq A$. In other words, for all vectors in $A$, we can find an open ball around the vector such that all vectors in the ball are in $A$.

> [!Abstract] Open Balls and Open Sets
> For $r > 0$, $u \in \mathbb{R}^n$, the open ball $B_r(u)$ is an open set.
> > Intuitively, this makes sense as for any vector inside the open ball, we can find a ball contained within our original ball. As our vectors get closer and closer to the ball's edge, our containing ball will shrink!
>
> > [!Note]- Proof
> > 
> > We want to show that $\forall v \in B_r(u)$, $\exists p > 0$ such that $B_p (v) \le B_r(u)$.
> > 
> > We know that for $v$, $|| u - v || \mathbb{R}$ by definition. We define the distance from $v$ to the ball's edge, $p = r - || u - v ||$. This will be the radius of our new ball around $v$.
> > 
> > We now show that $B_p(v) \subseteq B_r (u)$. Pick any $w \in B_p(v)$. By definition, 
> > $$
> > || v - w || < p \Longrightarrow || v - w || < r - || u - v ||
> > $$
> > Look at $|| u - w ||$. We know that
> > $$
> > \begin{align*}
> > || u - w || &= || u - v + v - w || \\
> > &\le || u - v || + || v - w || \\
> > &< || u - v || + p \\
> > &< || u - v || + (r - ||u - v||) \\
> > &< r
> > \end{align*}
> > $$
> > Thus, $w \in B_r (u)$!

We say that a set $A \subseteq \mathbb{R}^n$ is **closed** if for any sequence in $A$, $\{u_k\} \subseteq A$ such that $\{u_k\} \to u$, $u \in \mathbb{R}^n$, then $u \in A$. 

Furthermore, if $A \in \mathbb{R}^n$, then we call $A^c$ the **complement** of $A$, 
$$
A^c = \mathbb{R}^n \backslash A = \{ u \in \mathbb{R}^n | u \not\in A \}
$$

> [!Abstract] Theorem: Properties of Open Sets
> $A$ is an open set if and only if its complement, $A^c$, is closed.
> > The statement that "$A$ is open if and only if it is not closed" is NOT TRUE. There exist sets that are neither open or closed, and there exist sets that are both open and closed (ex. the empty set and $\mathbb{R}^n$)!
>
> > [!Note]- Proof
> > 
> > #### Proof ($\rightarrow$)
> > Assume first that $A$ is open. To show that $A^c$ is closed, pick any sequence $\{u_k\} \subseteq A^c$ such that $\{u_k\} \to u$, $u \in \mathbb{R}^n$.
> > 
> > We want to show that $u \in A^c$. Suppose $u \not\in A^c$, so $u \in A$. Then, because $A$ is open, there exists an $r > 0$ such that
> > $$
> > B_r (u) \subseteq A
> > $$
> > But no $u_k$ can be in this ball $B_r(u)$! This violates an assumption, so $u$ cannot be in $A$.
> > 
> > #### Proof ($\leftarrow$)
> > Conversely, assume $A^c$ is closed. To show that $A$ is open, choose any $u \in A$. By definition, $\exists r > 0$ such that $B_r(u) \subseteq A$.
> > 
> > By way of contradiction, assume that $\forall r > 0$, our ball around $u$ is not a subset of $A$. This means that $B_r (u)$ contains some $v \not\in A$ ($v \in A^c$), where $v$ depends on $r$.
> > 
> > Let $r = 1/a$. For all $a \in \mathbb{Z}$, we can form a sequence of $v_a$'s which, by assumption, are all in $A^c$. 
> > $$
> > || v_a - u || < r \qquad v_a \in A^c
> > $$
> > However, as $a \to \infty$, $r \to 0$! This tells us that  $\{v_a\} \to u, u \in A$, violating our assumption that $A^c$ is closed.

We continue by discussing intersections and unions of these sets.

If $\{ V_s \}_s$ is a (possibly infinite) family of open sets, then the **union of these open sets $\bigcup_{s \in S} V_s$ is open**.

Similarly, if $V_1, \dots V_k$ are open sets, then **the intersection of these sets  $V_1 \cap \dots \cap V_k$ is also open**.
> Note that the intersection clause only works for finite sets. In the infinite case, we could find a counterexample by choosing open balls with radius $r = 1/a$, so as $a \to \infty$, we are left with a point.

Let $\{F_s\}_{s} \in S$ be a possibly infinite family of closed sets. Then, $\bigcap_{s \in S} F_s$ is closed.

Let $F_1, \dots F_k$ be closed sets. Then their union $F_1 \cup \dots F_k$ is closed.

> [!Note]- Proof: Intersections and Unions of Open Sets
> #### Union of Open Sets
> Pick $u \in \bigcup_{s \in S} V_s$. We know that $\exists s_0 \in S$ such that $u \in V_{s_0}$. Since $V_{s_0}$ is open, we know that $\exists r > 0$ such that $B_r(u) \in V_{s_0} \subseteq \bigcup_{s \in S} V_s$.
>
> #### Intersection of Open Sets
> Let $u \in V_1 \cap \dots V_k$. We know that by definition,
> - Because $u \in V_1$, $\exists r_1 > 0$ such that the ball $B_{r_1} (u) \subseteq V_1$
> - Because $u \in V_2$, $\exists r_2 > 0$ such that $B_{r_2} (u) \subseteq V_2$
> - $\dots$
> 
> Continue this argument for all $k$. Now let $r = \min(r_1, \dots r_k)$. Then $B_r (u) \subseteq B_{r_i} u$ for all $i = 1 \dots k$, meaning $B_r (u) \subseteq \bigcap_{i=1}^k V_i$.

> [!Note]- Proof: Intersections and Unions of Closed Sets
> #### Intersection Proof (1)
> We know that by Demorgan's Law, $\left( \bigcap_{s \in S} F_s \right)^c = \bigcup_{s \in S} F_s^c$. We also know from an earlier theorem that each $F_s^c$ is open, and any union of open sets is open. So $\left( \bigcap_{s \in S} F_s \right)^c$ is open, and therefore $\bigcap_{s \in S} F_s$ is closed.
> 
> #### Intersection Proof (2)
> Let us have a sequence $\{u_k\} \subseteq \bigcap_{s \in S} F_s$, and assume $\{u_k\} \to u \in \mathbb{R}^n$. By definition of intersection, we know that $u_k \in F_s$ for all $s \in S$! So, by definition of a closed set, $u \in F_s$ for all $s \in S$.
> 
> This means that $u \in \bigcap_{s \in S} F_s$. 
>
> #### Union Proof (1)
> We know that by Demorgan's Law, $\left( F_1 \cup \dots F_k \right)^c = F_1^c \cap \dots F_k^c$. Each set is, by an earlier theorem, open.
>
> As etablished previously, the intersection of open sets yields an open set, so $\left( F_1 \cup \dots F_k \right)^c$ is open. By an earlier theorem, this means that $F_1 \cup \dots F_k$ is closed.
>
> #### Union Proof (2)
> Let us define a sequence in this union, $\{u_i\} \subseteq F_1 \cup \dots F_k$, where $\{u_i\} \to u \in \mathbb{R}^n$.
> 
> Because we have infinitely many $u_i$'s, and a finitely many sets $F$, at least one of these sets must contain infinitely many $u_i$ by the Pidgeonhole Principle. Let this set be $F_j$.
>
> So, there exists a subsequence $\{ u_{i_l} \}_{l \in \mathbb{N}}$ contained in $F_j$. As $\{u_i\} \to u$, it must be true that this subsequence converges to $u$ as well, and as $F_j$ is closed (by definition), $u \in F_j$. So, $u \in F_1 \cup \dots F_k$.

Let $A \subseteq \mathbb{R}^n$.

We define the **interior** of the set as
$$
\text{int} A = \{ u \in \mathbb{R}^n : \exists r > 0 \; \text{s.t.} \; B_r(u) \subseteq A \} \subseteq A
$$
In other words, the set of all points that can be contained within a ball inside of $A$.

We can also consider the interior of $A$'s complement. By definition, these two sets are mutually exclusive.

But what's between them? We call this the **boundary**:
$$
\text{Boundary} \; A = \{ u \in \mathbb{R}^n : \forall r > 0, B_r(u) \; \text{meets both} \; A \; \text{and} \; A^c \}
$$

These 3 sets are mutually exclusive, and form all of $R^n$!
- The interior of $A$
- The interior of $A^c$
- The boundary of $A$


# Functions and Continuity in $\mathbb{R}^n$
Define the function $F : A \to \mathbb{R}^m$, where $A \subseteq \mathbb{R}^n$. 

Then, $F$ is **continuous** at $u \in A$ if $\forall \{ u_k \} \to u$ where $\{u_k\} \subseteq A$, it follows that $\{F(u_k)\} \to F(u)$.
> In other words, for any sequence converging to $u$, the sequence evaluated in the function $F(u_k)$ should converge to $F(u)$!

> [!Example]+ Example: Continuity
> Let $f : \{1,2\} \cup [3, \infty) \to \mathbb{R}$ such that
> 
> $$
> f(x) = \begin{cases}
>     1 & x = 1 \\
>     0 & x = 2 \\
>     x & \text{else}
>     \end{cases}
> $$
> 
> Is $f$ continuous at $x = 1$? Yes! If $\{u_k\} \subseteq A$ such that $\{u_k\} \to u$, then $u_k = 1$ for $k$ sufficiently large.
> 
> Let $\epsilon = \frac{1}{10}$. Then, by definition of convergence, $\exists k$ such that
> $$
> | u_k - 1 | < \frac{1}{10} \quad \forall k \ge K
> $$
> But $\{u_k\} \subset \{1,2\} \cup [3, \infty)$! Thus, $u_k = 1$ $\forall k \ge K$, meaning $f(u_k) = f(1) = 1$.

> [!Abstract] Theorem: Preservation of Continuity
> Let $f, g : A \to \mathbb{R}$ such that $A \subseteq \mathbb{R}^n$. If $f, g$ are continuous at $u \in A$, then
> - $\forall \alpha, \beta \in \mathbb{R}$, $\alpha f + \beta g$ are also continuous at $u$
> - If $\forall v \in A, g(v) \ne 0$, then $\frac{f}{g}$ is continuous at $u$. 
>
> > [!Note]- Proof 
> > 
> > Let $\{u_k\} \to u$, and assume $\{u_k\} \subseteq A$.
> > 
> > Then, by assumption, $\{f(u_k)\} \to f(u)$, and $\{g(u_k)\} \to g(u)$, so
> > $$
> > \begin{align*}
> > &(f + g) (u_k) \to (f + g)(u) \\
> > &fg (u_k) \to fg(u)
> > \end{align*}
> > $$
> > By properties of sequences of real numbers.
> > 
> > Similarly, 
> > $$
> > \frac{f(u_k)}{g(u_k)} \to \frac{f(u)}{g(u)}
> > $$
> > if all $g(v) \not > 0$.

> [!Abstract] Theorem: Compositions of Functions
> Suppose we have two sets $A \subseteq \mathbb{R}^n$, $B \subseteq \mathbb{R}^m$, and define functions
> $$
> \begin{align*}
>     F: A \to B \\
>     G: B \to \mathbb{R}
> \end{align*}
> $$
> 
> If $F$ is continuous at $u \in A$, and $G$ is continuous at $F(u)$, then the composition $G \circ F$ is continuous at $u$.
>
> > [!Note]- Proof
> > 
> > Let $\{u_k\} \to u$. We know that $\{F(u_k)\} \to F(u)$ by definition and $\{G(F(u_k))\} \to G(F(u))\}$, i.e. $\{ (G \circ F) (u_k) \} \to G \circ F(u)$.

We can also prove continuity using the following $\epsilon$-$\delta$ definition.

It can be shown that $F : A \to \mathbb{R}^m$, $A \subseteq \mathbb{R}^n$ is continuous at $u \in A$ if and only if $\forall \epsilon > 0$, $\exists \delta > 0$ such that 
$$
|| u - v || < \delta \to || F(u) - F(v) || < \epsilon
$$

> [!Note]- Proof (Epsilon-Delta Continuity)
> #### Proof ($\leftarrow$)
> Assume $\epsilon$-$\delta$ definition.
> 
> Let $\{u_k\} \to u$. Let $\epsilon > 0$. We want $\exists K$ such that $\forall k \ge K$,
> $$
> || F(u_k) - F(u) || < \epsilon
> $$
> 
> Because $\{u_k\} \to u$, we know by defintion that $\exists K$ such that $\forall k \ge K$,
> $$
> || u_k - u || < \delta
> $$
> Then
> $$
> || F(u_k) - F(u) ||  < \epsilon \qquad \forall k \ge K
> $$
> 
> #### Proof ($\rightarrow$)
> Assume that the sequence definition of continuity holds. Assume by contradiction, that the $\epsilon$-$\delta$ definition does not hold.
> 
> So, $\exists \epsilon > 0$ where $\forall \delta > 0$, $\exists v \in A$ such that
> $$
> || u - v || < \delta \to || F(u) - F(v) || \ge \epsilon
> $$
> 
> Let $\delta = \frac{1}{k}$, and $\forall k \in \mathbb{N}$ form a sequence with these $v$'s. This sequence $\{v_k\} \to u$! However, by assumption, for all $v_k$,
> $$
> || F(v_k) - F(u) || \ge \epsilon
> $$
> So the sequence $\{F(v_k)\}$ does not converge to $F(u)$, which is a contradiction!

Recall that if $F : A \to \mathbb{R}^m$, if $B \subseteq A$, then we define
$$
F(B) = \{ F(b) : b \in B \}
$$
And if $C \subseteq \mathbb{R}^m$, then 
$$
F^{-1} (C) = \{ u \in A : F(u) \in C \}
$$
Or in other words, the set of all inputs to $F$ yielding possible outputs in $C$. Note that this does not require the function inverse to exist.

---

Using this definition, we claim that the epsilon-delta deinition is also equivalent to saying $\forall \epsilon > 0$, $\exists \delta > 0$ such that:
1. $$
   F( B_\delta(u) \cap A ) \subseteq B_\epsilon (F(u))
   $$
   Or in other words, all inputs of the function in a $\delta$ ball centered around $u$ must have an output which is within the ball of all all possible outputs of the function in the $\epsilon$ ball centered around $u$.

2. $$
   B_\delta(u) \cap A \subseteq F^{-1} (B_\epsilon(F(u)))
   $$
   Or in other words, all possible inputs in $A$ within the $\delta$ ball of $u$ are within the set of inputs yielding the $\epsilon$ ball of $F$ around $u$.
   
> [!Abstract] Theorem
> Let $O$ be open in $\mathbb{R}^n$, and let $F: O \to \mathbb{R}^m$. Then, $F$ is continuous (at every point of $O$) if and only if $F^{-1} (V)$ is open $\forall V \subseteq \mathbb{R}^m$, open.
>
> > [!Note]- Proof
> >
> > If $F^{-1} (V)$ is open $\forall V$ open, then $F$ is continuous (and it follows that $O = F^{-1} (\mathbb{R}^m)$ must be open).
> > 
> > Assume $F^{-1} (V)$ is open $\forall V$ open. We want to show that $\forall \epsilon > 0$, $\exists \delta > 0$ such that
> > $$
> > B_\delta (u) \cap O \subseteq F^{-1} (B_\epsilon (F(u)))
> > $$
> > 
> > Take $V = B_\epsilon (F(u))$. Then, by assumption, $F^{-1} (B_\epsilon (F(u)))$ is open. As we know $u \in F^{-1} (B_\epsilon (F(u)))$, there $\exists \delta > 0$ such that $B_\delta (u) \subseteq F^{-1} (B_\epsilon (F(u)))$.
> > > Note that we did not use the $O$ open fact, but $O = F^{-1} (\mathbb{R}^m)$ is open!
> > 
> > ---
> > 
> > Conversely, assume $F$ is continuous at every $u \in O$. Let $V \subseteq \mathbb{R}^m$ open. We want $F^{-1} (V)$ open.
> > 
> > Fix a point $u \in F^{-1}(V)$. To show openness, we want to show that $\exists r > 0$ such that $B_r (u) \subseteq F^{-1}(V)$. We know that $F(u) \subseteq V$. 
> > 
> > Since $V$ is open by assumption, there $\exists \epsilon > 0$ such that $B_\epsilon (F(u)) \subseteq V$. Since $F$ is continuous at $u$, $\exists \delta > 0$ such that
> > $$
> > B_\delta (u) \cap O \subseteq F^{-1} (B_\epsilon (F(u))) \subseteq F^{-1}(V)
> > $$
> > This is close to what we want, except for the $\cap O$! We use the assumption that $O$ is open, and $u \in O$, to find a $\delta_1$ such that
> > $$
> > B_\delta (u) \subseteq O
> > $$
> > We find our $r = \min(\delta, \delta_1)$, finding a ball centered around $u$ to be contained within $F^{-1} (V)$.
> > $$
> > B_r(u) \subseteq B_\delta(u) \cap O \subseteq F^{-1} (V)
> > $$

Let $f : \mathbb{R}^n \to \mathbb{R}$. If $f$ is continuous, $\alpha \in \mathbb{R}$ fixed, then the sets
$$
\begin{align*}
f^{-1} ( (-\infty, a) ) = \{ u \in \mathbb{R}^n : f(u) < \alpha \} \\
f^{-1}( (\alpha, \infty) ) = \{ u : \mathbb{R}^n : f(u) > \alpha \}
\end{align*}
$$
are open. Similarly, $\{ u \in \mathbb{R}^n : f(u) \le \alpha \}$ is closed because $\{ u \in \mathbb{R}^n : f(u) \le \alpha \}^c = \{ u \in \mathbb{R}^n : f(u) > \alpha \}$ is open.

# (11.2) Compactness
## Compactness
$K \subseteq \mathbb{R}^n$ is **sequentially compact** if for all sequences $\{ u_l \} \subseteq K$, there exists a subsequence $\{u_{l_m}\}$ and $u \in K$ such that
$$
\{u_{l_m}\} \to u
$$

A set $A \subseteq \mathbb{R}^n$ is **bounded** if $\exists M$ such that
$$
|| u || \le M \quad \forall u \in A
$$

> [!Abstract] Theorem: Sequential Compactness and Bounded
> If $K \subseteq \mathbb{R}^n$ is sequentially compact, then $K$ is bounded.
>
> > [!Note]- Proof
> >
> > We want $\exists M \ge 0$ such that
> > $$
> > ||u|| \le M \quad u \in K
> > $$
> > By way of contraction, assume that $K$ is sequetially compact but not bounded.
> > 
> > Then, $\forall M > 0$, $\exists u \in K$ such that
> > $$
> > ||u|| \le M
> > $$
> > Now let $M$ = m \in \mathbb{N}$, to get a sequence $u_m \in K$ such that $$|| u_m || > M$. For any subsequence in this sequence,
> > $$
> > || m_{m_l} || > m_l \to \infty
> > $$
> > So $u_{m_l}$ cannot converge! This is a contradiction.

> [!Abstract] Theorem: Sequential Compactness and Closed
> If $K \subseteq \mathbb{R}^n$ is sequentially compact, then $K$ is closed.
>
> > [!Note]- Proof
> >
> > Pick a sequence of points $\{u_l\} \subseteq K$, and assume that this sequence $\{u_l\} \to u \in \mathbb{R}^n$. We want to show that $u \in K$.
> > 
> > By sequential compactness, there exists a subsequence $\{u_{l_m}\} \to v$ such that $v \in K$. But $\{u_l\} \to u$, so $\{u_{l_m}\} \to u$! As limits are unique, this implies $u = v$, so $u \in K$!

Recall that if we have a sequence $\{x_l\} \subseteq \mathbb{R}$, and $\{x_l\}$ is bounded, then there exists a subsequence $\{x_{l_m}\}$ and $x \in \mathbb{R}$ such that
$$
\{ x_{l_m} \} \to x
$$
This is known as the **Bolzano-Weirstrass Theorem**. We can generalize this to $\mathbb{R}^n$.

> [!Abstract] Bolzano Weierstrass Theorem (Higher Dimensions)
> If $\{u_l\} \subseteq \mathbb{R}^n$, and $\{u_l\}$ is bounded, then $\exists \{ u_{l_m} \} \to u \in \mathbb{R}^n$.
>
> > [!Note]- Proof by Induction
> > 
> > We know that if $n = 1$, this is true.
> > 
> > Assume true for $n$. We wish to prove that this theorem holds for $n + 1$.
> > 
> > Let $\{u_l\} \in \mathbb{R}^{n+1}$, bounded. Write 
> > $$
> > u_l = (u'_l, u^{n+1}_l)
> > $$
> > Where $u_l \in \mathbb{R}^{n+1}$, $u'_l \in \mathbb{R}^n$, $u^{n+1}_l \in \mathbb{R}$.
> > 
> > By assumption, $\exists \{u'_{l_m}\} \to u' \in \mathbb{R}^n$. Now look at the corresponding sequence of $u^{n+1}$, $\{u^{n+1}_{l_m}\}$. By our base case, $\exists \{ u^{k+1}_{l_{m_p}} \} \to u^{n+1} \in \mathbb{R}$. Then, 
> > $$
> > \{u_{l_{m_p}}\} \to (u', u^{n+1})
> > $$

> [!Abstract] Theorem: Closed + Bounded and Compactness
> $K \subseteq \mathbb{R}^n$ is sequentially compact if and only if $K$ is closed and bounded.
> 
> > [!Note]- Proof
> > 
> > We already proved $\rightarrow$. We now prove the converse.
> > 
> > Let $K$ be closed and bounded. Choose any sequence $\{u_l\} \subseteq K$. As $K$ is bounded, by the Bolzano-Weierstrass Theorem we know that there exists a subsequence $\{u_{l_m}\} \to v$, where $v \in \mathbb{R}^n$.
> > 
> > But we also know that $K$ is closed! So, as $\{u_{l_m}\} \subseteq K$, it must be true that $v \in K$. So, 
> > $$
> > \exists \{u_{l_m}\} \to v \in K
> > $$

## Compactness and Functions
We find that functions on sequentially compact sets have some guaranteed properties.

> [!Abstract] Theorem
> If $K$ is sequentially compact and $F : K \to \mathbb{R}^m$ is continuous, then the image, $F(K)$, is sequentially compact.
>
> > [!Note]- Proof
> > 
> > Let $\{v_l\} \subseteq F(K)$. We want to show that there is a subsequence that converges to something in $F(K)$.
> > 
> > By definition of the image, we know that $\exists \{u_k\} \subseteq K$ such that
> > $$
> > F(u_k) = v_k
> > $$
> > By sequential compactness on $K$, there is a subsequence $\{u_{k_l}\} \to u \in K$, and furthermore, $\{ F(u_{k_l}) \} \to F(u)$ as $F$ is continuous.
