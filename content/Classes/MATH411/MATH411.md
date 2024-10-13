---
title: MATH411
tags:
- math411
---

MATH411 is a continuation of MATH410, but into higher dimensions.

# Generalizations in $\mathbb{R}^n$
We first generalize many of the concepts we learned about in MATH410 to higher dimensions.

## Vector Spaces 
$R^n$ is a vector space, with vectors and scalars (respectively) given as
$$
u = (u_1, u_2, \dots u_n) \in \mathbb{R}^n, u_i \in \mathbb{R}
$$
Satisfying vector addition and scalar multiplication, and inner product commonly known as the **dot product**
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

> [!Example]+ Example: Cauchy-Schwarz (1)
> Find the maximum value of
> $$
> \frac{x + 2y}{\sqrt{x^2 + y^2}}
> $$
> 
> Let $\vec{v}_1 = (x,y)$, $\vec{v}_2 = (1,2)$. Then, by Cauchy-Schwarz,
> $$
> \begin{align*}
> |\vec{v}_1 \cdot \vec{v}_2|
> &\le || \vec{v}_1 || \cdot || \vec{v}_2 || \\
> x + 2y 
> &\le \sqrt{x^2 + y^2} \sqrt{5} \\
> \frac{x + 2y}{\sqrt{x^2 + y^2}} &\le \sqrt{5}
> \end{align*}
> $$
> 
> We find our maximium is $\sqrt{5}$! Now, we find our maximizer.
> 
> Cauchy-Schwarz is only equal when $\vec{v}_1 = \vec{v}_2$. So,
> $$
> x = 1 \qquad y = 2
> $$
> We have maximizer $(1,2)$!

> [!Example]- Example: Cauchy-Schwarz (2)
> Find the maximum value of
> $$
> \frac{x + y}{\sqrt{x^2 + 4y^2}}
> $$
> 
> Let $\vec{v}_1 = (x, 2y)$, and $\vec{v}_2 = (1, 1/2)$. Then, by Cauchy Schwarz,
> $$
> \begin{align*}
> |\vec{v}_1 \cdot \vec{v}_2|
> &\le || \vec{v}_1 || \cdot || \vec{v}_2 || \\
> x + y 
> &\le \sqrt{x^2 + 4y^2} \sqrt{5/4} \\
> \frac{x + y}{\sqrt{x^2 + 4y^2}}
> &\le \sqrt{5/4}
> \end{align*}
> $$
> 
> We have found a maximum value! Now, we find our maximizer.
> 
> For Cauchy-Schwarz to be equal, it must be true that $\vec{v}_1 = \vec{v}_2$. So,
> $$
> x = 1 \qquad 2y = 1/2 \Longrightarrow y = 1/4
> $$
> Our maximizer is $(1, 1/4)$!

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

## Sequences and Convergence
Consider a **sequence in $\mathbb{R}^n$**, denoted $\{u_k\}$ for all $k \in \mathbb{N}$. In other words, each entry in the sequence is a point in $\mathbb{R}^n$.
> Note that by convention we will denote $u^i$ as the projection of the $i^{th}$ element of $u$ ($u$'s $i^{th}$ element).

If $\{u_k\}$ is a sequence in $\mathbb{R}^n$, and for some $u \in \mathbb{R}^n$ the following holds:
$$
\lim_{k\to\infty} u_k = u \quad \text{if} \quad \lim_{k\to\infty} || u_k - u || = 0
$$
Then we call this the **limit** of the sequence, alternatively written as $\{u_k\} \to u$ ($u_k$ converges to $u$) **in the norm**. 
> This is similar in idea to convergence in 1-dimensional series!

But in $\mathbb{R}^n$, this is not the only notion of convergence that we have! We can also say that $\{u_k\} \to u$ **componentwise**, if each $u_k^i \to u^i$ as $k \to \infty$.

> [!Abstract] Theorem: Synonymous Notions of Convergence
> $\{u_k\} \to u$ in norm if and only if $\{u_k\} \to u$ componentwise.
>
> > [!Note]-  Proof
> > 
> > #### Proof ($\rightarrow$) 
> > Assume that $\{u_k\} \to u$ in norm. Then, for each $1 \le i \le n$, 
> > $$
> > 0 \le | u_k^i - u^i | \le \sqrt{ (u_k^1 - u^1)^2 + \dots + (u_k^n - u^n)^2 } = || u_k - u || \to 0
> > $$
> > So by the squeeze theorem, $|u_k^i - u^i| \to 0$.
> > 
> > #### Proof ($\leftarrow$)
> > Assume that $\{u_k^i\} \to u^i$. Then,
> > $$
> > || u_k - u || = \sqrt{ (u_k^1 - u^1)^2 + \dots + (u_k^n - u^n)^2 }
> > $$
> > As each component converges to 0 by definition, and sums of sequences converging to 0 also converge to 0, we know that $|| u_k - u || \to 0$.

Note that this does not hold if we have infinite dimensions ($n$ not fixed)! In particular, component-wise convergence does not imply convergence in norm.

> [!Info] Remark: Dissimilarity of Convergence in Infinite Dimensions
> Say we have a sequence $\{u_k\}$, where for any $k$ the $k^{th}$ element is 1, all other 0. So,
> $$
> \begin{align*}
>     u_1 &= (1, 0, 0 \dots) \\
>     u_2 &= (0, 1, 0, \dots) \\
>     u_3 &= (0, 0, 1, \dots) \\
> \end{align*}
> $$
> We can see that as $k \to \infty$, $\{u_k\} \to \vec{0}$, the 0 vector! However, $||u_k|| \to 1$, so it does not converge in norm to 0.

## Closed and Open Sets
Let $r > 0$, $u \in \mathbb{R}^n$. We define the **open ball of radius $r$, centered at $u$** as
$$
B_r(u) = \{ v \in \mathbb{R}^n : || u - v || < \mathbb{R} \}
$$
In other words, the set of all $n$-dimensional points that are within some predetermined hypersphere of $u$.
> In $\mathbb{R}$, this is the open interval around a value $u$!

We say that a set $A \subseteq \mathbb{R}^n$ is **open** if $\forall u \in A$, $\exists r > 0$ such that $B_r(u) \subseteq A$. In other words, for all vectors in $A$, we can find an open ball around the vector such that all vectors in the ball are in $A$.

> [!Abstract] Theorem: Open Balls and Open Sets
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

We say that a set $A \subseteq \mathbb{R}^n$ is **closed** if for any sequence in $A$, $\{u_k\} \subseteq A$, such that $\{u_k\} \to u$, $u \in \mathbb{R}^n$, then $u \in A$. In other words, for any convergent sequence in $A$, the vector it converges to is also in $A$.

Furthermore, if $A \in \mathbb{R}^n$, then we call $A^c$ the **complement** of $A$, the set of all vectors not in $A$.
$$
A^c = \mathbb{R}^n \backslash A = \{ u \in \mathbb{R}^n | u \not\in A \}
$$

> [!Abstract] Theorem: Open Sets and their Complements
> $A$ is an open set if and only if its complement, $A^c$, is closed.
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

Note that the statement ``$A$ is open if and only if it is not closed" is **not true**. There exist sets that are neither open or closed, and there exist sets that are both open and closed (ex. the empty set and $\mathbb{R}^n$)!

We continue by discussing intersections and unions of open and closed sets.

> [!Info] Intersections / Unions of Open Sets
> Let $\{ V_s \}_s$ be a (possibly infinite) family of open sets. Then, the **union of these open sets $\bigcup_{s \in S} V_s$ is also open**.
> 
> Let $V_1, \dots V_k$ be a finite family of open sets. Then, **the intersection of these sets  $V_1 \cap \dots \cap V_k$ is also open**.
> > Note that the intersection clause only works for finite sets. We can find a counterexample for an infinite family by choosing open balls with radius $r = 1/a$, so that as $a \to \infty$, we are left with a point.
>
> > [!Note]- Proof: Intersections and Unions of Open Sets
> > #### Union of Open Sets
> > Pick $u \in \bigcup_{s \in S} V_s$. We know that $\exists s_0 \in S$ such that $u \in V_{s_0}$. Since $V_{s_0}$ is open, we know that $\exists r > 0$ such that $B_r(u) \in V_{s_0} \subseteq \bigcup_{s \in S} V_s$.
> >
> > #### Intersection of Open Sets
> > Let $u \in V_1 \cap \dots V_k$. We know that by definition,
> > - Because $u \in V_1$, $\exists r_1 > 0$ such that the ball $B_{r_1} (u) \subseteq V_1$
> > - Because $u \in V_2$, $\exists r_2 > 0$ such that $B_{r_2} (u) \subseteq V_2$
> > - $\dots$
> > 
> > Continue this argument for all $k$. Now let $r = \min(r_1, \dots r_k)$. Then $B_r (u) \subseteq B_{r_i} u$ for all $i = 1 \dots k$, meaning $B_r (u) \subseteq \bigcap_{i=1}^k V_i$.

> [!Info] Intersections / Unions of Closed Sets 
> Let $F_1, \dots F_k$ be a finite family of closed sets. Then their union $F_1 \cup \dots F_k$ is closed.
> 
> Let $\{F_s\}_{s} \in S$ be a possibly infinite family of closed sets. Then, their intersection $\bigcap_{s \in S} F_s$ is closed.
>
> > [!Note]- Proof: Intersections and Unions of Closed Sets
> > #### Intersection Proof (1)
> > We know that by Demorgan's Law, $\left( \bigcap_{s \in S} F_s \right)^c = \bigcup_{s \in S} F_s^c$. We also know from an earlier theorem that each $F_s^c$ is open, and any union of open sets is open. So $\left( \bigcap_{s \in S} F_s \right)^c$ is open, and therefore $\bigcap_{s \in S} F_s$ is closed.
> > 
> > #### Intersection Proof (2)
> > Let us have a sequence $\{u_k\} \subseteq \bigcap_{s \in S} F_s$, and assume $\{u_k\} \to u \in \mathbb{R}^n$. By definition of intersection, we know that $u_k \in F_s$ for all $s \in S$! So, by definition of a closed set, $u \in F_s$ for all $s \in S$.
> > 
> > This means that $u \in \bigcap_{s \in S} F_s$. 
> >
> > #### Union Proof (1)
> > We know that by Demorgan's Law, $\left( F_1 \cup \dots F_k \right)^c = F_1^c \cap \dots F_k^c$. Each set is, by an earlier theorem, open.
> >
> > As etablished previously, the intersection of open sets yields an open set, so $\left( F_1 \cup \dots F_k \right)^c$ is open. By an earlier theorem, this means that $F_1 \cup \dots F_k$ is closed.
> >
> > #### Union Proof (2)
> > Let us define a sequence in this union, $\{u_i\} \subseteq F_1 \cup \dots F_k$, where $\{u_i\} \to u \in \mathbb{R}^n$.
> > 
> > Because we have infinitely many $u_i$'s, and a finitely many sets $F$, at least one of these sets must contain infinitely many $u_i$ by the Pidgeonhole Principle. Let this set be $F_j$.
> >
> > So, there exists a subsequence $\{ u_{i_l} \}_{l \in \mathbb{N}}$ contained in $F_j$. As $\{u_i\} \to u$, it must be true that this subsequence converges to $u$ as well, and as $F_j$ is closed (by definition), $u \in F_j$. So, $u \in F_1 \cup \dots F_k$.

Using the concept of an open ball, we can formally define the interior, exterior, and boundary of a set. Let $A \subseteq \mathbb{R}^n$.

We define the **interior** of $A$ as
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


## Continuity and Compactness
### Continuity of Functions
Let $A \subseteq \mathbb{R}^n$ be a set, and define the function $F : A \to \mathbb{R}^m$.

We say $F$ is **continuous** at $u \in A$ if $\forall \{ u_k \} \to u$ where $\{u_k\} \subseteq A$, it follows that $\{F(u_k)\} \to F(u)$. In other words, for any sequence in $A$ converging to $u$, the sequence evaluated in the function $F(u_k)$ should converge to $F(u)$!

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

We can also prove continuity using what's known as an **$\epsilon$-$\delta$ definition**. 

By $\epsilon$-$\delta$, $F : A \to \mathbb{R}^m$, $A \subseteq \mathbb{R}^n$ is continuous at $u \in A$ if and only if $\forall \epsilon > 0$, $\exists \delta > 0$ such that 
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

We also find the following equivalence definitions for epsilon-delta. First, recall that if $F : A \to \mathbb{R}^m$, then for $B \subseteq A$, we define
$$
F(B) = \{ F(b) : b \in B \}
$$
And if $C \subseteq \mathbb{R}^m$, then 
$$
F^{-1} (C) = \{ u \in A : F(u) \in C \}
$$
Or in other words, the set of all inputs to $F$ yielding possible outputs in $C$. 
> Note that this does not require the function inverse to exist. We're just defining the set of all inputs in $A$ yielding something in $C$.

Using these definitions, we claim that the epsilon-delta deinition is also equivalent to saying $\forall \epsilon > 0$, $\exists \delta > 0$,
1. $$
   F( B_\delta(u) \cap A ) \subseteq B_\epsilon (F(u))
   $$
   In other words, all inputs of the function in a $\delta$ ball centered around $u$ must have an output which is within the set of all possible outputs of the function in the $\epsilon$ ball centered around $u$. 
   
   > Note that we intersect with $A$ to guarantee that we have an input for the function, as not all vectors in a ball around $u$ may be an input for the function.

2. $$
   B_\delta(u) \cap A \subseteq F^{-1} (B_\epsilon(F(u)))
   $$
   In other words, all possible inputs within the $\delta$ ball of $u$ are contained within the set of inputs that yield the $\epsilon$ ball of $F$ around $u$.
   
> [!Abstract] Theorem: Continuity and Open Sets
> Let $O$ be open in $\mathbb{R}^n$, and let $F: O \to \mathbb{R}^m$. 
> 
> Then, $F$ is continuous at every point of $O$ if and only if the set of inputs $F^{-1} (V)$ is open for all $V \subseteq \mathbb{R}^m$ open.
>
> > [!Note]- Proof
> > 
> > #### Proof $\rightarrow$
> > Let $F$ be continuous for all $x \in O$. We wish to show that the set of inputs $F^{-1} (V)$ is open $\forall V \in \mathbb{R}^n$.
> > 
> > Let $V \in \mathbb{R}^n$. We want to show that $F^{-1} (V)$ is open. In other words, $\forall x \in F^{-1}(V)$, $\exists r > 0$ such that $B_r (x) \subseteq F^{-1} (V)$.
> > 
> > Because $x \in F^{-1} (V)$, $F(x) \in V$. By the openness on $V$, we can find a $r > 0$ such that
> > $$
> > B_r (F(x)) \subseteq V
> > $$
> > Because all values of $B_r (F(x))$ are in $V$, all values of the domain mapping to values $B_r (F(x))$ also map to values in $V$. Thus, taking the inverse $F^{-1}$ maintains the subset property.
> > $$
> > F^{-1} (B_r (F(x))) \subseteq F^{-1} (V)
> > $$
> > 
> > Because $F$ is continuous, we find that $\forall \epsilon > 0$, $\exists \delta > 0$ 
> > $$
> > B_\delta (x) \cap O \subseteq F^{-1} (B_\epsilon (F(x)))
> > $$
> > We let $\epsilon = r$, to find a $\delta_1 > 0$ such that
> > $$
> > B_{\delta_1} (x) \cap O \subseteq F^{-1} (B_r (F(x))) \subseteq F^{-1} (V)
> > $$
> > 
> > We now end by modifying our $\delta$ to guarantee that $B_\delta (x) \subseteq O$. Because $x \in F^{-1} (V)$, it is in the domain of $F$ ($O$), and as $O$ is open, we can find a $\delta_2 > 0$ such that $B_{\delta_2} \subseteq O$. Choose $\delta = \min(\delta_1, \delta_2)$. Then, we find tha
> > $$
> > B_\delta (x) \cap O = B_\delta (x) \subseteq F^{-1} (B_r (F(x))) \subseteq F^{-1} (V)
> > $$
> > 
> > Thus, $F^{-1} (V)$ is open. 
> > 
> > 
> > #### Proof ($\leftarrow$)
> > Suppose that for all $V \subseteq \mathbb{R}^m$ open, we have that $F^{-1} (V)$ is also open. We want to show that $F$ is continuous.
> > 
> > Let $x \in O$. Now let $\epsilon > 0$. We want to find a $\delta > 0$ such that
> > $$
> > F(B_\delta (x) \cap O) \subseteq B_\epsilon (F(x))
> > $$
> > Take the ball $B_\epsilon (F(x))$. Because open balls are always open, and $B_\epsilon (F(x)) \subseteq \mathbb{R}^m$, we know that $F^{-1} (B_\epsilon (F(x)))$ is open by assumption.
> > 
> > Because this is open, and $x \in F^{-1} (B_\epsilon (F(x))$, by definition, we can find a $r > 0$ such that
> > $$
> > B_r (x) \subseteq F^{-1} (B_\epsilon (F(x))
> > $$
> > Let $\delta = r$. We have found our $\delta$!
> > 
> > $$
> > B_r (x) \cap O \subseteq B_r (x) \subseteq F^{-1} (B_\epsilon (F(x))
> > $$

We have a similar case with closed sets.

> [!Abstract] Theorem: Continuity and Closed Sets
> Let $F : \mathbb{R}^n \to \mathbb{R}^m$.
> 
> Then, $F$ is continuous at every point of $O$ if and only if the set of inputs $F^{-1} (V)$ is closed for all $V \subseteq \mathbb{R}^m$ closed.
>
> > [!Note]- Proof
> > 
> > #### Proof ($\rightarrow$)
> > Let $F$ be continuous. We want to show that $F^{-1} (V)$ is closed for all $V \subseteq \mathbb{R}^m$ closed.
> > 
> > Choose some $V \subseteq \mathbb{R}^m$ closed, and take its complement, $V^c$ which is open. Because $V^c$ is open and $F$ is continuous, by the previous theorem it must hold that $F^{-1} (V^c)$ is open.
> > 
> > Note that if $x \in F^{-1} (V^c)$, then it cannot be in $F^{-1} (V)$, as $V^c \cap V = \varnothing$ and a single domain value cannot map to two values. Thus, $F^{-1} (V^c) = F^{-1} (V)^c$! As $F^{-1} (V)^c$ is open, it therefore must hold that $F^{-1} (V)$ is closed. 
> > 
> > #### Proof ($\leftarrow$)
> > Suppose that for all $V \subseteq \mathbb{R}^m$ closed, $F^{-1} (V)$ is closed. We wish to show that $F$ is continuous.
> > 
> > We show that if for any $V \subseteq \mathbb{R}^m$ open, $F^{-1} (V)$ is open, then $F$ is continuous. Let $V \subseteq \mathbb{R}^m$ open. Then, $V^c$ is closed, so by assumption, $F^{-1} (V^c)$ is closed. By a similar argument from before, $F^{-1} (V^c) = F^{-1} (V)^c$, so $F^{-1} (V)$ is open.

> [!Info] Remark
> Let $f : \mathbb{R}^n \to \mathbb{R}$. If $f$ is continuous, $\alpha \in \mathbb{R}$ fixed, then the following sets are open.
> $$
> \begin{align*}
> f^{-1} ( (-\infty, a) ) = \{ u \in \mathbb{R}^n : f(u) < \alpha \} \\
> f^{-1}( (\alpha, \infty) ) = \{ u : \mathbb{R}^n : f(u) > \alpha \}
> \end{align*}
> $$
> 
> Similarly, $\{ u \in \mathbb{R}^n : f(u) \le \alpha \}$ is closed because $\{ u \in \mathbb{R}^n : f(u) \le \alpha \}^c = \{ u \in \mathbb{R}^n : f(u) > \alpha \}$ is open.

Consider the following examples.

> [!Example]- Example: Continuity Proof
> Let $f : \mathbb{R} \to \mathbb{R}$ continuous. Prove that
> $$
> G = \{ (x, f(x)) : x \in \mathbb{R} \}
> $$
> is closed.
> 
> Let $\{a_k\} \in G$, where $\{a_k\} \to a$. We wish to show that $a \in G$.
> 
> By definition of $G$, we can express our sequence $\{a_k\}$ as
> $$
> \{a_k\} = \{(x_k, f(x_k))\} \to (x,y)
> $$
> Because $\{x_k\} \to x$, by continuity on $f$ we know that
> $$
> \{f(x_k)\} \to f(x)
> $$
> And by the uniqueness of limits, if $\{f(x_k)\} \to f(x), \{f(x_k)\} \to y$, then $y = f(x)$. Thus,
> $$
> \{x_k,f(x_k)\} \to (x, f(x)) \in G
> $$
> Thus, $G$ is closed.

### Sequential Compactness
A set $A \subseteq \mathbb{R}^n$ is **bounded** if $\exists M$ such that
$$
|| u || \le M \quad \forall u \in A
$$
In other words, there exists an $M$ which is an upper bound for all vector lengths in the set.

We say set $K \subseteq \mathbb{R}^n$ is **sequentially compact** if for all sequences $\{ u_l \} \subseteq K$, there exists a subsequence $\{u_{l_m}\}$ and $u \in K$ such that
$$
\{u_{l_m}\} \to u
$$
In other words, all sequences have a convergent subsequence that converge to something in $K$.

We show that sequential compactness is synonymous with closure and boundedness (together).

> [!Abstract] Theorem: Sequential Compactness and Boundedness
> If $K \subseteq \mathbb{R}^n$ is sequentially compact, then $K$ is bounded.
>
> > [!Note]- Proof
> >
> > We want $\exists M \ge 0$ such that
> > $$
> > ||u|| \le M \quad u \in K
> > $$
> > By way of contradiction, assume that $K$ is sequentially compact but not bounded.
> > 
> > Then, $\forall M > 0$, $\exists u \in K$ such that
> > $$
> > ||u|| > M
> > $$
> > Now let $M = m \in \mathbb{N}$, to get a sequence $u_m \in K$ such that $|| u_m || > M$. For any subsequence in this sequence,
> > $$
> > || m_{m_l} || > m_l \to \infty
> > $$
> > So $u_{m_l}$ cannot converge! This is a contradiction.

> [!Abstract] Theorem: Sequential Compactness and Closure
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

We find that functions on sequentially compact sets have some guaranteed properties.

> [!Abstract] Theorem: Images of Sequentially Compact Domains
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

Note that both closure and boundedness (implying compactness) must hold for this to be true! They do not hold on their own.

> [!Example]+ Example: Failure of Image Closure and  of Images
> If $C \subseteq \mathbb{R}^n$ is closed, $F : C \to \mathbb{R}^m$ is continuous, is $F(C)$ closed?
>
> No! As a counterexample, let $f : \mathbb{R} \to \mathbb{R}$, where $f = \frac{1}{1 + x^2}$. Then, $\mathbb{R}$ is closed, but $f$ is not, as it asymptotes towards $0 \not\in f(\mathbb{R})$!
>
> If $B \subseteq \mathbb{R}$ is bounded, and $f : B \to \mathbb{R}$ is continuous, is $f(B)$ bounded?
>
> No! Let $f(x) = \frac{1}{x}$ on $B = (0,1)$. Then, $F(B) = (1, \infty)$ which is unbounded.
>
> > Note the specific wording on the domain.
> > 
> > If $B \subseteq \mathbb{R}$ is bounded and $f : \mathbb{R} \to \mathbb{R}$ is continuous (domain is now $\mathbb{R}$), now $f(B)$ is bounded! We can find a sequentially compact domain containing $B$, and find that $f$ on this domain is sequentially compact (and thus bounded!).

We also find that functions on sequentially compact sets obey the extreme value theorem.

> [!Abstract] Theorem: Extreme Value Theorem (Generalization)
> Let $K$ be sequentially compact, $f : K \to \mathbb{R}$ continuous.
> 
> Then $f$ has a minimum and maximum value.
>
> > [!Note]- Proof
> > 
> > We know that from an earlier theorem, $f(K)$ is bounded.
> > 
> > By definition, $\exists m$ which is the infimum of $f$ over all $K$. We want to show that $\exists u \in K$ such that $f(u) = m$. 
> > 
> > By definition of infimum, we know that $\exists \{u_i\} \subseteq K$ such that $\{f(u_i)\} \to m$. Since $K$ is sequentially compact, we know there exists a convergent subsequence $\{u_{i_l}\}$ such that $\{u_{i_l}\} \to u \in K$. Then, by continuity,
> > $$
> > \lim f(u_{i_l}) = \lim f(u_i) = m
> > $$

Interestingly enough, the converse of the above theorem can actually be used to prove sequential compactness.

> [!Abstract] Theorem: Sequential Compactness via Minimums and Maximums
> Let $A \subseteq \mathbb{R}^n$ be a set such that any function $f : A \to \mathbb{R}$ has a minimum and maximum value. Then, $A$ is sequentially compact.
> 
> > [!Note]- Proof
> > 
> > We wish to show that $A$ is bounded and closed.
> > 
> > To show that $A$ is bounded, choose some function $f(x) = ||x||$. By assumption, we know that $\exists x_\text{max}$ such that $\forall x \in A$,
> > $$
> > f(x) \le f(x_\text{max}) \Longrightarrow 0 \le ||x|| \le ||x_\text{max}||
> > $$
> > Let $x_\text{max}$ be our bound.
> > 
> > To show that $A$ is closed, let $\{u_i\} \in A$ such that $\{u_i\} \to u \in \mathbb{R}^n$. We want to show that $u \in A$. 
> > 
> > Let $f(x) = ||x - u||$. Note that $f$'s infimum is 0. Thus, the minimum of $f$ is also 0! But the minimum can only be attained at $x = u$, so $u \in A$.

We also say set $K \subseteq \mathbb{R}^n$ is **compact** if for every family of open sets $\{V_\alpha\}$ such that $K \subseteq \bigcup_\alpha V_\alpha$,  then there exist finitely many sets $V_{\alpha_1}, \dots, V_{\alpha_l}$ such that
$$
K \subseteq V_{\alpha_1} \cup \dots \cup V_{\alpha_l}
$$
In other words, $K$ is compact if for any family of (possibly infinite) open sets covering $K$, we can find a finite number of sets that cover $K$.
> If $K \subseteq \bigcup_\alpha V_\alpha$, we say that $\bigcup_\alpha V_\alpha$ **covers** $K$.

We similarly prove compactness with respect to closure and boundedness.

> [!Abstract] Theorem: Compactness vs. Closure and Boundedness
> $K$ is compact if and only if $K$ is closed and bounded.
>
> > [!Info]- Proposition 1: $K$ compact implies $K$ bounded. 
> > 
> > Let $K \subseteq \bigcup_{l=1}^\infty B_l (0)$ (this is always true, as this union is all of $\mathbb{R}^n$). Then by definition, there must exist some "largest" ball that contains $K$ given by a finite value. So, there is a $l_0$ such that $K \subseteq B_{l_0}$. 
> > 
> > So, $K$ is bounded.
> > 
>
> > [!Info]- Proposition 2: $K$ compact implies $K$ closed.
> > 
> > Let $K$ be compact, and let $\{u_k\}$ be a sequence of points in $K$, where $\{u_k\} \to u \in \mathbb{R}^n$. We wish to show that $u \in K$.
> > 
> > Assume by contradiction that $u \not\in K$.
> > 
> > Now, we must make a family of open sets whose union is guaranteed to cover (contain) $K$, so we can apply our definition. 
> > 
> > Let $V_l = \{ x \in \mathbb{R}^n : || x - u || > 1/l \}$. Then, the union of all $V_l$'s is all of $\mathbb{R}^n$, with the exception of the point $u$.
> > > We are looking at the set of points outside of circles that are closing in on $u$.
> > 
> > $$
> > \bigcup_l V_l = \{ x \in \mathbb{R}^n : x \ne u \}
> > $$
> > Therefore $K$ must be contained in this family of open sets. By definition, there must exist a finite amount of sets that contains $K$. But since each of these sets contain each other, their union is the same as the largest set, meaning we can find a $V_{l_0}$ such that
> > $$
> > K \subseteq V_{l_0}
> > $$
> > This contradicts $\{u_k\} \subseteq K$, $\{u_k\} \to u$, as there cannot be any $\{u_k\}$ in the ball $V_{l_0}$! 
> > > We can choose an epsilon to show that convergence fails, as there is an open ball around $u$ that $K$ is NOT a part of.
> 
> > [!Info]- Proposition 3: If the set $L$ is compact, and $K \subseteq L$, $K$ is closed, then $K$ is compact.
> > 
> > Let $V_\alpha$ be a family of open sets where $K \subseteq \bigcup_\alpha V_\alpha$. We wish to find a finite amount of sets in this family containing $K$.
> > 
> > For any $x$, if it is in $K$, then it is in $\bigcup_\alpha V_\alpha$. Otherwise, if must be in $K^c$. Because $K$ is closed, $K^c$ must be open. So,
> > $$
> > L \subseteq \bigcup_\alpha V_\alpha \cup K^c
> > $$
> > Since $L$ is compact, there must exist a finite amount of sets $V_{\alpha_1}, V_{\alpha_2}, \dots, V_{\alpha_l}$ from this family such that
> > $$
> > L \subseteq \bigcup_{i=1}^l V_{\alpha_i}
> > $$
> > As $K \subseteq L$, then,
> > $$
> > K \subseteq \bigcup_{i=1}^l V_{\alpha_i}
> > $$
> > 
> > But this union could contain $K^c$! So, we show that $K^c$ cannot be in this union, to find a finite amount of sets from $\{V_\alpha\}$ covering $K$.
> > 
> > By definition, a point in $K$ cannot be in $K^c$! So, $K$ is contained in a finite number of the $V_\alpha$.
> 
> > [!Note]- Proof ($\leftarrow$)
> > 
> > Note that this proof heavily relies on the fact that $K$ is in finitely many dimensions.
> > 
> > Let $K$ be closed and bounded. Since $K$ is bounded, $K$ is contained in some closed cube in $\mathbb{R}^n$. Without loss of generality, assume $K \subseteq C = [0,1] \times [0,1] \dots \times [0,1]$.
> > 
> > It suffices to show that this cube is compact, after which we apply the previous theorem (because $K$ is closed) to get our result. 
> > 
> > Let $\{V_\alpha\}$ be open sets such that $C \subseteq \bigcup_\alpha V_\alpha$. Assume by contradiction that we cannot find a finite number of sets from $\{V_\alpha\}$ containing $C$. 
> > 
> > Divide $C$ into $2^n$ subcubes of size $\frac{1}{2}$. We show that these subcubes can be contained in finitely many sets, and therefore, so can $C$.
> > 
> > By assumption, we must be able to find a closed subcube $C_1$ which cannot be covered by finitely many $V_\alpha$'s. Continue, dividing $C_1$ into $2^n$ subcubes of size $\frac{1}{4}$. Then, among these subcubes, there must be one that cannot be covered by finitely many sets. Repeating this, we get
> > $$
> > C_i \subseteq \dots \subseteq C_2 \subseteq C_1 \subseteq C
> > $$
> > Where no $C_i$ can be covered by finitely many sets.
> > 
> > By a generalization of the nested interval theorem, there must exist a single unique point contained within all nested cubes- formally, $\exists ! x_0 \in C_i \forall i$.
> > 
> > We know that as $x_0 \in C$, the point must exist in at least one of the $V_\alpha$'s, say $V_{\alpha_0}$. By definition of an open set, there exists a ball around $x_0$ completely contained within $V_{\alpha_0}$.
> > 
> > So, we can find some $C_i \in V_{\alpha_0}$, which is covered by finitely many sets. This is a contradiction!

> [!Example]- Example
> Let $f : \mathbb{R} \to \mathbb{R}$. Assume that $f^{-1}(K)$ is closed for every (sequentially) compact set $K$ in $\mathbb{R}$. Is $f$ continuous?
>
> Not necessarily. The theorem above requires that all closed sets are closed in $f^{-1}(K)$, but not all closed sets are sequentially compact.
>
> Let $f$ be the function
> $$
> f(x) =
> \begin{cases}
> \frac{1}{x} & x \ne 0 \\
> 0 & x = 0
> \end{cases}
> $$
> 
> Then, every sequentially compact set $K$ on $f$'s range maps to a closed set in $f$'s domain, but $f$ is not continuous at 0!

### Uniform Continuity
The function $F : A \to \mathbb{R}^n$, $A \subseteq \mathbb{R}^m$ is **uniformly continuous** if for any two sequences $\{u_i\}, \{v_i\} \subseteq A$, if
$$
\{ || u_i - v_i || \} \to 0
$$
Then,
$$
\{ || f(u_i) - f(v_i) || \} \to 0
$$

Note that uniform continuity implies continuity. Simply let $v_i$ be the sequence of whatever $\{u_i\}$ converges to so we get our continuity definition! 
> The converse is not true. See the example below.

> [!Example]+ Example: Continuity Doesn't Imply Uniform Continuity
> Let $f(x) = x^2$, which is a continuous function.
> 
> Then, for $u_i = \frac{1}{i} + i$, $v_i = i$, we have that $u_i - v_i \to 0$, but $f(u_i) - f(v_i) = 2 + \frac{1}{i^2} \not\to 0$!

> [!Abstract] Theorem: Uniform Continuity and Sequential Compactness
> If $K$ is sequentially compact, and $F: K \to \mathbb{R}^n$ is continuous, then $F$ is uniformly continuous.
>
> > [!Note]- Proof
> >
> > Let $K$ be sequentially compact, and $F : K \to \mathbb{R}^n$ continuous. We wish to show that $F$ is uniformly continuous.
> > 
> > By way of contradiction, suppose that $F$ is not uniformly continuous. Then, there exists some $\{x_k\}, \{y_k\}$ such that $\{x_k - y_k\} \to 0$, but
> > $$
> > \{ f(x_k) - f(y_k) \} \not\to 0
> > $$
> > 
> > By definition of continuity, $\exists \epsilon > 0$ such that $\forall N \in \mathbb{N}$, $\forall k \ge N$,
> > $$
> > || f(x_k) - f(y_k) || \ge \epsilon
> > $$
> > Choose this $\epsilon$. Then, by sequential compactness of $K$, we can find a subsequence such that for $i \ge N$, all terms have a difference greater than $\epsilon$.
> > $$
> > || f(x_{k_i}) - f(y_{k_i}) || \ge \epsilon
> > $$
> > But by sequential compactness on each $f(x_{k_i})$, $f(y_{k_i})$, we can find convergent subsequences
> > $$
> > \{ f(x_{k_{i_j}}) \} \to u_1 \qquad \{ f(y_{k_{i_j}}) \} \to u_2
> > $$
> > As $f$ is continuous, and $\{x_k\}, \{y_k\}$ converge, then $u_1 = u_2$. This means that our subsequence $f(x_{k_i}) - f(y_{k_i})$ converges to 0, but this is a contradiction! 

Note that there exist non-compact sets that also satisfy this property! Consider the following example.

> [!Example]- Example
> Let $C \subseteq \mathbb{R}^n$ with the property that any $f : C \to \mathbb{R}^n$ continuous is uniformly continuous. Is it true that $C$ must be closed and bounded?
> 
> #### Must $C$ be Closed?
> Let $\{x_k\} \in C$, where $\{x_k\} \to x_0$. If $C$ is bounded, then we need to show that $x_0 \in C$.
> 
> By way of contradiction, suppose $x_0 \not\in C$. Then, we can define function 
> $$
> f(x) = \frac{1}{|x - x_0|}
> $$
> Which is continuous on $C$, as $x = x_0$ is by assumption not continuous on $C$.
> 
> By assumption, $f(x)$ must be uniformly continuous. So, $\forall \epsilon > 0$, $\exists \delta > 0$ such that $\forall x,y \in C$,
> $$
> | x - y | < \delta \to | f(x) - f(y) | < \epsilon
> $$
> 
> Let $\epsilon = 1$. By assumption, we have a delta $\delta > 0$ such that for $|x - y| < \delta$, $|f(x) - f(y)| < 1$ for all $x,y$ satisfying this condition.
> 
> Choose $x_k, y_k$ converging to $x_0$ such that
> $$
> |x_k - x_0| < \frac{\delta}{2} \qquad |y_k - x_0| < \frac{\delta}{2}
> $$
> Then,
> $$
> |x_k - y_k| < \delta
> $$
> 
> Fix $x_k$, but let $y_k \to x_0$. Then, our assumptions should still hold as we are within $\delta$, but $f(y_k) \to \infty$! This is a contradiction.
> 
> So, $C$ must be closed.
> 
> #### Must $C$ be Bounded?
> Suppose $C = \mathbb{N}$. 
> 
> Let $f : \mathbb{N} \to \mathbb{R}$ continuous. Then, $f$ is automatically continuous, as in the integers, any convergent sequence must hover at the same epsilon value (due to the spacing between the integers)- it'll be the same integer value (due to the spacing between integers).
> > Let $\epsilon > 0$. Let $\delta = 1/2$. If $x,y \in \mathbb{N}$, then if $|x - y| < 1/2$, then $x = y$, so $f(x) = f(y)$, so $|f(x) - f(y)| = 0 < \epsilon$.
> 
> However, $C$ is not bounded! So, $C$ does not have to be bounded.



Like continuity, we also have a $\epsilon-\delta$ definition for uniform continuity too!

Let $F : A \to \mathbb{R}^m$. Then, the following are equivalent.
1. If $\{u_i\}, \{v_i\} \subseteq A$ with $\{ ||u_i - v_i|| \} \to 0$, then $\{ || F(u_i) - F(v_i) || \} \to 0$.
2. $\forall \epsilon > 0$, $\exists \delta > 0$ such that if $u,v \in A$ with $|| u - v || < \delta$, then $|| F(u) - F(v) || < \epsilon$.

The latter is the **$\epsilon-\delta$ definition for uniform continuity**.

> [!Note]- Proof
> #### Proof (1 to 2)
> We prove this by contrapositive. Assume that (2) is not true. We wish to show that as a result, (1) cannot be true.
>
> By the negation of (2), $\exists \epsilon > 0$ such that $\forall \delta > 0$, $\exists u,v \in A$, $|| u - v || < \delta$ with $|| F(u) - F(v) || \ge \epsilon$. 
>
> Choose $\delta = \frac{1}{k}$, and let $k \in \mathbb{N}$ to create sequences $\{u_k\}, \{v_k\}$ such that $|| u_k - v_k || < \frac{1}{k} \to 0$, where $|| F(u_k) - F(v_k) || \ge \epsilon$.
> 
> Thus, (1) is not true.
> 
> #### Proof (2 to 1)
> Assume (2). Let $\{u_i\}, \{v_i\} \subseteq A$ with $\{ ||u_i - v_i|| \} \to 0$. We wish to show that $\{ || F(u_i) - F(v_i) || \} \to 0$.
>
> Let $\epsilon > 0$. Then, $\exists \delta > 0$ such that (2) holds. Let $I$ such that $|| u_i - v_i || < \delta$. Then, by (2), $\forall i \ge I$, $|| F(u_i) - F(v_i) || < \epsilon$.


## Convexity and Connectedness
We say the set $A$ is **convex** if $\forall u,v \in A$, $\forall 0 \le t \le 1$,
$$
t(u) + (1 - t) v \in A
$$
In other words, for any two points in the set, all points along the line between these two points are also within the set.
> In lower dimensions, this defines a convex shape!

We say $A \subseteq \mathbb{R}^n$ is **path connected** if $\forall u,v \in A$, if there exists a continuous function $\gamma : [a,b] \to A$, with 
$$
\gamma(a) = u \qquad \gamma(b) = v
$$
In other words, for any two points in the set, we can define a function (a "path") between these two points that remains completely within the shape! We call $\gamma$ (gamma) the **parameterized path**.
> In lower dimensions, this defines a completely connected shape!

> [!Abstract] Theorem: Path Connected Subsets of the Real Line
> On the real line, $A \subseteq \mathbb{R}$ is path connected if and only if $A$ is an interval.
>
> > [!Note]- Proof
> > 
> > #### Proof ($\leftarrow$)
> > If $A$ is an interval, let $u,v$ be points in this interval. Define function $\gamma (t) = tu + (1 - t) v$ for $0 \le t \le 1$. We can trivially show that $\gamma(0) = u, \gamma(1) = v$, and furthermore, $\gamma$ is continuous. We have our parameterized path.
> > 
> > #### Proof ($\rightarrow$)
> > Conversely, if $A \subseteq \mathbb{R}$ is path connected, let $u,v \in A$. We wish to show that the interval $[u,v] \subseteq A$, which implies that $A$ is an interval (as we chose $u,v$ arbitrarily).
> > 
> > We know that $\exists \gamma : [a,b] \to A$ continuous with $\gamma[a] = u, \gamma[b] = v$. Choose any $w \in (u,v)$. We wish to show that $w \in A$, which then shows that $[u,v] \subseteq A$ ($u,v$ are trivially in $A$).
> > 
> > By the intermediate value theorem, $\exists c \in (a,b)$ such that $\gamma(c) = w$! Thus, $w \in A$ as it is in the image of $\gamma$, which is defined to be $A$. 

> [!Abstract] Theorem: Path Connected Sets on Continuous Functions
> If $A \subseteq \mathbb{R}^n$ is path connected and $F: A \to \mathbb{R}^m$ is continuous, then the image $F(A)$ is also path connected. In other words, continuity preserves path connectedness!
> 
> > [!Note]- Proof
> > 
> > Let $u,v \in F(A)$. We wish to find a parameterized path between $u$ and $v$.
> > 
> > By definition of an image, we can find $x,y \in A$ such that $F(x) = u, F(y) = v$. By path connectedness of $A$, we can find an interval $[a,b]$ with a parameterized function $\gamma$ such that $\gamma(a) = x, \gamma(b) = y$.
> > 
> > Then, as $F$ is also continuous, we can find a composition of the functions $F \circ \gamma : [a,b] \to F(A)$, which is continuous such that $F \circ \gamma (a) = F (x) = u$, and $F \circ \gamma (b) = F(y) = v$. We have found a parameterized path from $u$ to $v$.

We say that the set $A$ has the **Intermediate Value Property (IVP)** if for any continuous function defined on the set, $f : A \to \mathbb{R}$, the image $f(A)$ is an interval.
> It can be shown that if $A$ is path connected, it has the intermediate value property!

Set $A \subseteq \mathbb{R}^n$ is **not connected** if $\exists U,V$ open sets such that:
1. $U \cap A \ne \varnothing, V \cap A \ne \varnothing$
2. $(U \cap A) \cap (V \cap A) = \varnothing$
3. $(U \cap A) \cup (V \cap A) = A$

In other words, we can find two disjoint open sets that make up $A$. If $U,V$ satisfythese conditions, then we say $U,V$ **separate** $A$. 

Thus, by this definition, a set is **connected** if we cannot find two disjoint open sets that make up $A$.
> Note that by this more intuitive definition, we can deduce that $\mathbb{R}^n$ is connected, as we cannot form 2 disjoint open sets by partitioning the space- there must be one with a boundary.

> [!Abstract] Theorem: Connected Sets and IVP
> $A$ is connected if and only if $A$ has the Intermediate Value Property.
>
> > [!Note]- Proof
> > 
> > We want to show that if $A$ is not connected if and only if A does not have the intermediate value property. In other words, $\exists f : A \to \mathbb{R}$ continuous, with $f(A)$ not an interval.
> > 
> > #### Proof ($\rightarrow$)
> > Assume that $A$ is not connected, and let $U,V$ open separate $A$.
> > 
> > Define
> > $$
> > f(x) = 
> > \begin{cases}
> >     1 & x \in A \cap U \\
> >     0 & x \in A \cap V
> > \end{cases}
> > $$
> > Note the following:
> > - $f$ is defined $\forall x \in A$ because of property (3) of not connected
> > - The value $f(x)$ is unique because of (2).
> > - $f(A) = \{ 0 , 1 \}$ because of (1), because there is at least one element of $U$ in $A$, and one element of $V$ in $A$.
> > 
> > To show $f$ is continuous at $x_0 \in U \cap A$, we want to show that $\exists \delta > 0$ such that $B_\delta (x_0) \subseteq U$. Then, if $x \in A$ and $||x - x_0|| < \delta$, then $f(x) = f(x_0)$, so $| f(x) - f(x_0) | < \epsilon$ trivially.
> > 
> > So we found $f : A \to \mathbb{R}$, continuous, where $f(A)$ is not on an interval.
> > 
> > #### Proof ($\leftarrow$).
> > Assume $A$ does not have the intermediate value property. Let $f : A \to \mathbb{R}$ continuous, with $f(A)$ not an interval.
> > 
> > Then, $\exists c \in \mathbb{R}$ such that $c \not\in f(A)$, $f(A) \cap (-\infty, c) \ne \varnothing$, $f(A) \cap (c, \infty) \ne \varnothing$.
> > 
> > To construct $U,V$ separating $A$, let
> > $$
> > \tilde{U} = f^{-1} ( (-\infty, c) ), \tilde{V} = f^{-1} ( (c,\infty) )
> > $$
> > Then, $\tilde{U} \ne \varnothing, \tilde{V} \ne \varnothing$.
> > - $\tilde{U} \cup \tilde{V} = A$ because we know that $c \not\in f(A)$.
> > - $\tilde{U} \cap \tilde{V} = \varnothing$, as there are no points that are in both $(-\infty, c)$ and $(c, \infty)$.
> > 
> > To finish, we will find $U,V$ open such that $\tilde{U} = U \cap A$, $\tilde{V} = V \cap A$.
> > 
> > Let $x \in \tilde{U}$. Then, $f(x) < c$. Since $f$ is continuous, $\exists r > 0$ such that $\forall y \in B_r (x) \cap A$, $f(y) < c$. Let $U = \cup_{x \in \tilde{U}} B_r (x)$. 
> > 
> > Notice that $U \cap A = \tilde{U}$, so $\bigcup_{x\in\tilde{U}} (B_r(x) \cap A) = \tilde{U}$. 

We can also find that if $A$ is path connected, then $A$ is connected.

> [!Info] Remark: Connected $\not\to$ Path Connected
> Note that the converse is **not true**. If $A$ is connected, it may not be path connected. 
> 
> For example, let $A = \{0\} \times [-1,1] \cup \{ (x, \sin(1/x)) : 0 < x \le 1 \}$, which oscillates as we get closer to the $y$ axis, but never touches! Thus, even if $A$ is connected, it is not path connected.

Thus, we end with the following graph of implications. Below, an arrow indicates that the source implies the destination.

```mermaid
graph LR
1[Path Connected];
2[Connected];
3[Intermediate Value Property];

1 -.-> 2 & 3;
2 -.-> 3;
3 -.-> 2;
```

We can use the idea of path connectedness to prove a remark earlier about sets that are both open and closed!

> [!Info] Corollary
> IF $U \subseteq \mathbb{R}^n$ is both open and closed, then $U = \mathbb{R}^n$, or $U = \varnothing$
> 
> > [!Note]- Proof
> > 
> > We know that $\mathbb{R}^n$ is path connected, so $\mathbb{R}$ is connected.
> > 
> > Let $U$ be both open and closed. Let $V = U^c$. Because $U$ is open, $V$ is also open.
> > 
> > In this case, $U \cap V = \varnothing$, and $U \cup V = \mathbb{R}^n$! 
> > 
> > So, $U \ne \varnothing, V \ne \varnothing$ is impossible! So, it must be true that either $U = \mathbb{R}^n, V = \varnothing$, or $U = \varnothing, V = \mathbb{R}^n$.





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

> [!Abstract] Theorem: Common Metric on $C([a,b], \mathbb{R})$
> Let $C([a,b], \mathbb{R})$ be the set of all continuous functions $f : [a,b] \to \mathbb{R}$.
> 
> For any two functions $f,g \in C([a,b], \mathbb{R}$, we have the metric
> $$
> d(f,g) = \max_{x \in [a,b]} |f(x) - g(x)|
> $$
> > This finds the maximum single difference between the functions in the interval $[a,b]$!

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




--- End of Exam 1 ---

Many examples are given below.

> [!Example] 
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



---

In class examples

> [!Example]
Let $f : \mathbb{R} \to \mathbb{R}$ continuous. Prove that $G = \{ (x, f(x)) : x \in \mathbb{R} \}$ is closed.

Suppose we have a sequence of points $\{ (x_k, y_k) \} \in G$, where $\{ (x_k, y_k) \} \to (x, y)$. We want to show that $(x,y) \in G$. We know that because $\{x_k\} \to x$, by continuity on $f$, then $f(x_k) \to f(x)$! Note that because $y_k = f(x_k)$ (by definition), then
$$
\{ (x_k, y_k) \} \to (x,y) = (x, f(x)) \in G
$$

> [!Example]
Let $f : \mathbb{R} \to \mathbb{R}$. Assume $G = \{ (x, f(x)) : x \in \mathbb{R} \}$ is closed. Does it follow that $f$ is continuous?

Let $\{x_k\} \in \mathbb{R}$, where $\{x_k\} \to x$. We want to show that $\{f(x_k)\} \to f(x)$. 

Using this, we can form a sequence $\{(x_k, f(x_k))\} \subseteq G$. Then, if $\{ (x_k, f(x_k) \} \to (x,y)$, then $f(x) = y$. So, if there exists a $y$ such that $\{f(x_k)\} \to y$, then $y = f(x)$ where $\{x_k\} \to x$.

But do we know if $\{f(x_k)\}$ converges? In fact, closure only says that **if** the sequence converges, then its result is in the set! However, we may be able to find a function that fails to satisfy this.

Let 
$$
f(x) = \frac{1}{x}, f(0) = 0 \qquad x_k = \frac{1}{k}
$$
Then, $f(x)$ is not continuous at $x = 0$, yet the set $G$ is still closed!




---

Supplemental problems 8

Fixed point will guaranteed be on the exam o.o..

> [!Example]
> Define the set of functions 
> $$
> X = \{ f \in C([0,1],\mathbb{R}) : 1 - \pi \le f(x) \le 1 + \pi, \forall x \in [0, \pi] \}
> $$
> 
> Now define the function $T : X \to C([0,\pi], \mathbb{R})$, where 
> $$
> (Tf) (x) = 1 + \int_{0}^x \cos(f(t)) dt
> $$
> 
> #### Problem 1
> Prove that $T : X \to X$.
> 
> Let $f \in X$. We want to show that $(Tf)(x) \in X$ as well. We can trivially see that $T$, by definition, maps to a continuous function on $[0,\pi]$. We must show that $(Tf)(x)$'s range is bounded between $[1 - \pi, 1 + \pi]$
> $$
> \begin{align*}
> &1 - \pi \le 1 + \int_0^x \cos(f(t)) dt \le 1 + \pi &\forall x \in [0, \pi] \\
> &-\pi \le \int_0^x \cos(f(t)) dt \le \pi &\forall x \in [0, \pi] \\
> &\left| \int_0^x \cos(f(t)) \right| \le \pi \\
> \end{align*}
> $$
> We know that this is true, as
> $$
> \left| \int_0^x \cos(f(t)) \right| \le \left| \int_0^\pi \cos(f(t)) \right| \le \left| \int_0^\pi 1 \right| \le \pi
> $$
> 
> #### Problem 2
> Is $T$ a contraction?
> 
> Let $f_1, f_2 \in X$. We know that by definition,
> $$
> \begin{align*}
> (Tf_1) (x) = 1 + \int_0^x \cos(f_1(t)) dt \\
> (Tf_2) (x) = 1 + \int_0^x \cos(f_2(t)) dt
> \end{align*}
> $$
> 
> We find that
> $$
> \begin{align*}
> d(Tf_1, Tf_2) 
> &= \max_{x \in [0,\pi]} \left| \int_0^x \cos(f_1(t)) - cos(f_2(t)) dt\right| \\
> &\le \int_0^\pi | \cos(f_1(t)) - \cos(f_2(t)) | dt \\
> &\le C d(f_1, f_2)
> \end{align*}
> $$
> We wish to find a $C$ satisfying this. We choose $C = \pi$ and find that this works, as $d(f_1, f_2)$ is defined as the maximum difference of $\cos(f_1(t)) - \cos(f_2(t))$.
> 
> Unfortunately, we need a $C < 1$ to prove that we have a contraction. So, this seems to suggest that $T$ is not a contraction! To show this, we need to find a $f_1, f_2$ such that
> $$
> d(Tf_1, Tf_2) > d(f_1, f_2)
> $$
> 
> Let $f_1 = \pi$, $f_2 = 0$. Then,
> $$
> \begin{align*}
> d(Tf_1, Tf_2) 
> &= \max_{x \in [0, \pi]} \left| \int_0^x \cos(f_1(t)) - \cos(f_2(t)) dt \right| \\
> &= \max_{x \in [0, \pi]} \left| \int_0^x 2 dt \right| \\
> &= 2 \pi \\
> d(f_1, f_2) 
> &= \max_{x \in [0,\pi]} | f_1(t) - f_2(t) | \\
> &= \max_{x \in [0,\pi]} | \pi | \\
> &= \pi
> \end{align*}
> $$
> Thus, $d(Tf_1, Tf_2) = 2d(f_1, f_2)$, meaning $T$ fails to be a contraction.
> 
> #### Problem 3
> If $f$ is a fixed point of $T$, what differential equation does $T$ satisfy?
> 
> A fixed point means that $Tf(x) = f(x)$. So,
> $$
> f(x) = 1 + \int_0^x \cos(f(t)) dt
> $$
> We make this into a differential equation by differentiating.
> $$
> f'(x) = \cos(f(x)), f(0) = 1
> $$
> 
> We ask, does the solution above exist for all $x \ge 0$?
> 
> We have $g(x,y) = \cos(y)$, and bound $|g(x,y)| \le K = 1$. By the mean value theorem applied to this function with respect to $y$,
> $$
> | g(x, y_1) - g(x, y_2) | \le M |y_1 - y_2| \qquad \forall (x,y_1), (x,y_2)
> $$
> For $M = 1$. Thus, there exists an $h = h(K,M)$ such that the solution to $f'(x) = \cos(f(x))$, with any initial conditions, $f(x_0) = y_0$, exists and is unique in $[x_0 - h, x_0 + h]$. We extend this argument to show that the solution exits and is unique on $[x_0 + h, x_0 + 2h]$, and continue for all $x$.
> > The length of the intervals that we extend our solution does not get shorter, so we can repeat this to encompass all values of $x$!

> [!Info] Remark
> Let $g : \mathbb{R}^2 \to \mathbb{R}$ be continuous, such that $\exists M, K$ with
> $$
> \begin{align*}
> &g(x,y) \le K &\forall (x,y) \in \mathbb{R}^2 \\
> &| g(x, y_1) - g(x, y_2) | \le M |y_1 - y_2| &\forall (x,y_1), (x,y_2)
> \end{align*}
> $$
> Then, the solution to $f'(x) = g(x,f(x))$, $f(x_0) = y_0$ exists for all $x \in \mathbb{R}$.
> > This happens because $K, M$ do not depend on $x_0$ and $y_0$! 

Define $X = \{ f \in C([0,1], \mathbb{R}) : 0 \le f(x) \le 1, \forall x \in [0,1] \}$. Define $T$ as
$$
Tf(x) = \int_0^x f(t)^{2/3} dt
$$

#### Problem 1
Prove that $T : X \to X$. We see that if $0 \le f(x) \le 1$, then
$$
0 \le \int_0^x f^{2/3} dt \le 1
$$

#### Problem 2
We show that $T$ is not a contraction.

Let $f_1 (t) = 0$, $f_2(t) = 1$. Then,
$$
T(f_1) (x) = 0 \forall x \qquad T(f_2) (x) = x
$$
So, 
$$
d(f_1, f_2) = 1 \qquad d(Tf_1, Tf_2) = 1
$$
So we fail to have a contraction.



> [!Example] 
> Define $X = [0,1)$ with $d(x,y) = |x-y|$. Then, $X$ is open and closed (in itself).

We say that if $\{f_k\} \subseteq C([a,b], \mathbb{R})$, $\{f_k\} \to f$ with respect to 
$$
d(f,g) = \max_{x\in[a,b]} |f(x) - g(x)|
$$
If $f_k \to f$ uniformly.


Let's look at continuous functions $f \in C([a,b], \mathbb{R}$. Then, we know there exist
$$
\int_a^b |f(x)| dx \le (b - a) \max_{x\in[a,b]} |f(x)|
$$
But does there exist a constant such that
$$
\max_{x\in[a,b]} |f(x)| \le \alpha \int_a^b |f(x)|
$$
In infinite dimensions, this is not possible! Let $f_k (x) = x^k$. Then,
$$
\max_{x \in [0,1]} f_k (x) = 1
$$ 
But
$$
\int_0^1 x^k dx = \frac{1}{k + 1}
$$
Where as $k \to \infty$ (which is possible as we are in the space of ALL continuous functions), this goes to 0! 

Is $C([0,1], \mathbb{R})$ with $d(f,g) = \int_0^a |f - g|$ complete? In other words, if $f_k$ is Cauchy in our space, does there exist a function $f \in C([0,1],\mathbb{R})$ such that $\int_0^1 |f_k - f| = 0$?
> Discussion if continuous functions on these L2 norms are a metric space?


We have the space of continuous functions $C([a,b], \mathbb{R})$, and a norm 
$$
|| f ||_1 \int_a^b |f(x)| dx
$$
Note that if $||f|| = 0$, $f = 0$ if $f$ is continuous.
> If $f$ is a general Riemann integrable function, the above may fail (consider a function with a jump discontinuity).

> [!Example] Example: Incomplete Space
> We can find that $C([a,b], \mathbb{R})$ and 
> $$
> d_1 (f,g) = \int_a^b | f(x) - g(x) | dx
> $$ is not complete.
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

^^ 11.3... 12.1




Let $X = \mathbb{R}^n$, $d(u,v) = ||u - v||$. In general, if $V$ is a vector space, $|| \cdot ||$ is called a **norm**, if
1. $||u|| \ge 0$, $\forall u \in V$, and $||u|| = 0$ if and only if $u = 0$.
2. $||u + v|| \le ||u|| + ||v||$
3. $|| \alpha u || \le |\alpha| ||u||$

We find that if $||\cdot||$ if a norm on $V$, then $d(u,v) = ||u-v||$ is a metric.

> [!Note]- Proof
> 
> We check our 3 axioms.
> 1. $d(u,v) = ||u - v|| = |-1| ||v - u|| = ||v - u|| = d(v,u)$, by (3) where we take $\alpha = -1$.
> 2. $d(u,v) \ge 0$, by (1), and $d(u,v) = 0$ if and only if $||x - y|| = 0$, if and only if $x - y = 0$, by (1) again. 
> 3. Let $x,y,z \in V$.
>    $$
>    \begin{align*}
>    d(x,y) 
>    &= ||x - y|| = ||x - y + z - z|| \\
>    &\le ||x - z|| + ||z - y|| = d(x,z) + d(z,y) \\
>    \end{align*}
>    $$

> [!Example]
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

> [!Example] 
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


---

Chapter 13

$x^*$ is a limit point of $A \subseteq \mathbb{R}^n$ if there is a sequence  $\exists \{ x_k \} \subseteq A / \{x^*\}$ such that $\{x_k\} \to x^*$. In other words, there is a sequence not containing $x^*$ converging to it.

If a function $f : A \to \mathbb{R}$, and $x^*$ is a limit point of $A$, then **the limit of the function** is defined as $\lim_{x \to x^*} f(x) = l$ if $\forall \{x_k\} \subseteq A / \{x^*\}$, 
$$
\lim_{k \to \infty} f(x_k) = l
$$

> [!Example] 
> $$
> f(x,y) = \frac{xy}{x^2 + y^2}
> $$
>
> $f : \mathbb{R}^2 \to \{(0,0)\}$. 
>
> $\lim_{(x,y) \to (0,0)} f(x,y)$ does not exist, as we can chose $\{x_k\} = (1/k, 0)$, and $\{x_k\} = (1/k, 1/k)$, which have different limits as $k \to \infty$. 

> [!Example] 
> $$
> g(x,y) = \frac{x^2 y}{x^2 + y^2}
> $$
> In this case, $\lim_{(x,y) \to (0,0)} g(x,y)$ exists and equals 0.
> 
> Let $(x_k, y_k) \to (0,0)$ not containing $(0,0)$. Then, 
> $$
> | g(x_k, y_k) | \le |x_k| \frac{ |x_k y_k| }{x_k^2 + y_k^2} \le |x_k| \frac{1}{2} \to 0
> $$


A function $f : \mathbb{R}^n / \{0\} \to \mathbb{R}$ is **homogeneous of degree $k$** if
$$
f(tx) = t^k f(x) \qquad \forall t > 0, \forall x \in \mathbb{R}^n / \{0\}
$$
> Basically, we should be able to replace $x,y$ with $t$, and take out the $t$ into a $t^k$ term.

> [!Example] Example: Homogenoeus Functions
> $$
> g(x,y) = \frac{x^2 y}{x^2 + y^2}
> $$
> Is homogeneous of degree 1, because
> $$
> g(tx, ty) = \frac{t^3 xy}{t^2 (x^2 + y^2)} = t g(x,y)
> $$
> 
> $$
> f(x,y) = \frac{xy}{x^2 + y^2}
> $$
> Is homogeneous of degree 0, because
> $$
> f(tx, ty) = t^0 f(x,y)
> $$

Notice how above, $g$ is homogeneous of degree 1 and has a limit to $(0,0)$, whereas $f$ is homogeneous of degree 0 and doesn't. Does there exist some generalizaiton for this?

> [!Abstract] Proposition: Limits of Homogeneous Functions
> If $f : \mathbb{R}^n / \{0\} \to \mathbb{R}$ is continuous, and homogeneous of degree $k > 0$, then
> $$
> \lim_{x \to 0} f(x) = 0
> $$
>
> > [!Note]- Proof
> > 
> > We look at $f(x)$, and we try to make the case that as $x \to 0$, $f(x) \to 0$.
> > $$
> > f(x) = f \left( ||x|| \frac{x}{||x||} \right)
> > $$
> > We write this as a product of something that approaches 0 and something that is bounded. 
> > 
> > By assumption, $f(x)$ is homogeneous of degree $k$, so letting $t = ||x||$,
> > $$
> > f \left( ||x|| \frac{x}{||x||} \right) = ||x||^k f \left( \frac{x}{||x||} \right)
> > $$
> > As $x \to 0$, $||x||^k \to 0$! Also, as $\frac{x}{||x||} \in S^{n-1}$ (the unit sphere of dimension $n - 1$), which is a sequentially compact, then continuous functions on sequentially compact sets are bounded. 
> > $$
> > ||x||^k f \left( \frac{x}{||x||} \right) \to 0 
> > $$

This does not necessarily mean that homogeneous functions of degree $k = 0$ don't have a limit at 0! Just that some don't. 
> Any constant function (ex. $f(x) = 1$) have defined limits as $x \to 0$!

## 13.2
Let $f : O \to \mathbb{R}$, $x = (x_1, \dots x_n) \in O$. We define the **partial derivative of $f$ with respect to $x_i$ as**
$$
\frac{\partial f}{\partial x_i} (x) = \lim_{t \to 0} \frac{f(x + t e_i) - f(x)}{t}
$$
if the latter limit exists.
> Keep all variables constant except $x_i$, and take $\frac{d}{dx_i}$!

> [!Example]+ Example: Partial Derivatives and Continuity
> Let $f : \mathbb{R}^2 \to \mathbb{R}$,
> $$
> f(x,y) = 
> \begin{cases}
> \frac{xy}{x^2 + y^2} & (x,y) \ne (0,0) \\
> 0 & (x,y) = (0,0)
> \end{cases}
> $$
> 
> We noticed that $f$ is not continuous at $(0,0)$, and $\frac{\partial f}{\partial x}, \frac{\partial f}{\partial y}$ exist (by the quotient rule) at all $(x,y) \ne (0,0)$.
> 
> Then, does $\frac{\partial f}{\partial x}$ exist at $(0,0)$?
> $$
> \lim_{t \to 0} \frac{f(t,0) - f(0,0)}{t} = \lim_{t \to 0} \frac{0 - 0}{t}
> $$
> Yes! It exists and is equal to 0.
> 
> Similarly, we can find $\frac{\partial f}{\partial y} = 0$.
> 
> This is very interesting! Even though $f(x,y)$ is not continuous at $(0,0)$, our partial derivatives still exist! This goes against our understanding of differentiability and continuity in the single variable case. 

If all $\frac{\partial f}{\partial x_i} (x)$ exist for all $x \in O$ open, then we can define
$$
\frac{d}{d x_i} \left( \frac{\partial f}{\partial x_j} \right) (x) = \frac{\partial^2 f}{\partal x_i \partial x_j} (x)
$$

Typically, these mixed partials are equal in any order, but there are some cases where they're not! The following theorem tells us when they are equivalent.

> [!Abstract] Theorem:
> If $\frac{d}{d x_i} \left( \frac{\partial f}{\partial x_j} \right)$ and $\frac{d}{d x_j} \left( \frac{\partial f}{\partial x_i} \right)$ exists and are continuous in $O$, then
> $$
> \frac{d}{d x_i} \left( \frac{\partial f}{\partial x_j} \right) = \frac{d}{d x_j} \left( \frac{\partial f}{\partial x_i} \right)
> $$
>
> > [!Note] Proof 
> > 
Let $x = x_i, y = x_j$. Then,
$$
A = f(x_0 + r, y_0 + r) - f(x_0 + r, y_0) - f(x_0, y_0 + r) + f(x_0, y_0)
$$
Define $\phi(x) = f(x, y_0 + r) - f(x, y_0)$. Then,
$$
A = \phi(x_0 + r) - \phi(x_0)
$$
By the mean value theorem, this is equal to
$$
\begin{align*}
= \phi' (x_0 + \theta_1) * r = \frac{\partial}{\partial x} [ f(x_0 + \theta_1, y_0 + r) - f(x_0 + \theta_1, y_0) ] R 
\end{align*}
$$
> We create two equivalent functions that converge to the two partial derivatives, respectively, forcing equality.

## 13.3
From prior courses, we learned to define the **directional derivative** of a function $f$ as
$$
\frac{d}{dt} \bigg|_{t = 0} [ f(x + th) ] = \langle \nabla f(x), h \rangle
$$
For $x \in \mathbb{R}^n, h \in \mathbb{R}^n$. Where the **gradient** of the function**, $\nabla f$, is given as
$$
\nabla f(x) = \left( \frac{\partial f}{\partial x_1}, \dots, \frac{\partial f}{\partial x_n} \right)
$$

But this may not actually hold for all functions! Consider
$$
f(x,y) =
\begin{cases}
\frac{xy}{x^2 + y^2} & (x, y) \ne 0 \\
0 & (x,y) = 0
\end{cases}
$$
Then, for $x = (0,0)$, $h = (1,1)$, the directional derivative does not exist, even though $\langle \nabla f(x), h \rangle = 0$!

We prove the above definition, and show the conditions in which it holds.

> [!Abstract] Proposition
> Let $f : \mathbb{R}^n \to \mathbb{R}$, and assume all $\frac{\partial f}{\partial x_i}$ exist $\forall x \in \mathbb{R}^n$, $\forall i \in \{1, \dots n\}$.
> 
> Fix $x, h \ne 0$ ($h \in \mathbb{R}^n$). Then, there exists a $z_1, \dots z_n \in B_{||h||} (x)$ such that
> $$
> f(x + h) - f(x) = \frac{\partial f}{\partial x_1} (z_1) h_1 + \dots + \frac{\partial f}{\partial x_n} (z_n) h_n
> $$
>
> > [!Note]- Proof
> > 
> > We prove this for $n = 2$, though the proof can very easily be extended to more dimensions.
> > 
> > Consider the points $(x_1, x_2)$, $(x_1 + h, x_2 + h)$, and look at
> > $$
> > f(x_1 + h, x_2 + h) - f(x_1, x_2) = f(x_1 + h, x_2 + h) - f(x_1, x_2 + h_2) + f(x_1, x_2 + h_2) - f(x_1, x_2)
> > $$
> > 
> > By doing this, we convert our problem into 1 dimensions, where we can solve for the differences
> > $$
> > f(x_1 + h, x_2 + h) - f(x_1, x_2 + h_2) \qquad f(x_1, x_2 + h_2) - f(x_1, x_2)
> > $$
> > separately.
> > 
> > By the Mean Value Theorem, 
> > $$
> > \begin{align*}
> > f(x_1 + h, x_2 + h) - f(x_1, x_2 + h_2) = \frac{\partial f}{\partial x_1} (x_1 + \theta h_1, x_2 + h_2) h_1 \\
> > f(x_1, x_2 + h_2) - f(x_1, x_2) = \frac{\partial f}{\partial x_2} (x_1, x_2 + \theta_2 h_2) h_2 \\
> > f(x_1 + h, x_2 + h) - f(x_1, x_2) = \frac{\partial f}{\partial x_1} (x_1 + \theta h_1, x_2 + h_2) h_1 + \frac{\partial f}{\partial x_2} (x_1, x_2 + \theta_2 h_2) h_2
> > \end{align*}
> > $$
> > 
> > Let $z_1 = (x_1 + \theta_1 h_1, x_2 + h_2)$, and $z_2 = (x_1, x_2 + \theta_2 h_2)$. We are done.

If $f : O \to \mathbb{R}^n$, $O$ open, and all $\frac{\partial f}{\partial x_i} (x)$ exist $\forall x \in O$, and are continuous, $f$ is called **continuously differentiable**, called $C^1 (O)$.

> [!Abstract] Theorem: Formula for The Directional Derivative
> If $f : \mathbb{R}^n \to \mathbb{R}$ is $C^1$, then $\forall x \in \mathbb{R}^n$, $\forall h \ne 0$, the limit
> $$
> \frac{d}{dt} \bigg|_{t=0} f(x + th) = \lim_{t \to 0} \frac{f(x + th) - f(x)}{t}
> $$
> Exists and equals $\langle \nabla f(x), h \rangle$.
> $$
> \langle \nabla f(x), h \rangle = \sum_{i=1}^n \frac{\partial f}{\partial x_i} (x) h_i
> $$
>
> > [!Note]- Proof
> > 
> > By our previous proposition, 
> > $$
> > \begin{align*}
> > \frac{f(x + th) - f(x)}{t} 
> > &= \frac{1}{t} \left( \frac{\partial f}{\partial x_1} (z_1) t h_1 + \dots + \frac{\partial f}{\partial x_n} (z_n) t h_n \right) \\
> > &= \frac{\partial f}{\partial x_1} (z_1) h_1 + \dots + \frac{\partial f}{\partial x_n} (z_n) h_n
> > \end{align*}
> > $$
> > For $z_1, \dots z_n \in B_{||th||} (x)$. Let $t \to 0$. Then, the ball of $B_{||th||} (x)$ will shrink towards $x$, forcing all $z_i$'s to converge to $x$! Thus, as $t \to 0,$ we have
> > $$
> > \frac{\partial f}{\partial x_1} (x) h_1 + \dots + \frac{\partial f}{\partial x_n} (x) h_n
> > $$

Let $P \ne 0$, $P \in \mathbb{R}^n$, $f : \mathbb{R}^n \to \mathbb{R}$. Then, **the partial derivative in direction $P$** of $f$ is given as
$$
\frac{\partial f}{\partial P} (x) = \frac{d}{dt} \bigg|_{t=0} f(x + tP)
$$
If it exists. By the previous theorem, the partial derivative of $f$ in the direction $P$ exists and equals $\langle \nabla f, P \rangle \rangle$ if $f \in C^1$.

> [!Abstract] Proposition
> Let $f : \mathbb{R}^n \to \mathbb{R}, C^1$, $x \in \mathbb{R}^n$, $h \in \mathbb{R}^n$ where $h \ne 0$. 
> 
> Then, there exists $0 < \theta < 1$ such that
> $$
> f(x + h) - f(x) = \langle \nabla f(x + \theta h), h \rangle
> $$
>
> > This is similar to the first proposition we have, except all $z_1, \dots z_n$ are assumed to be at the point.
>
> > [!Note]- Proof
> > 
> > Let $\phi : \mathbb{R} \to \mathbb{R}$, $\phi(t) = f(x + th)$ so that 
> > $$
> > \phi(1) = f(x + h) \qquad \phi(0) = f(x)
> > $$
> > 
> > Then, $f(x + h) - f(x) = \phi(1) - \phi(0) = \phi'(\theta) (1 - 0)$ by the mean value theorem (for $0 < \theta < 1$) and furthermore, as the derivative of $\phi(t)$ is the directional derivative,
> > $$
> > f(x + h) - f(x) = \phi'(\theta) = \langle \nabla f(x + \theta h), h \rangle
> > $$

> [!Abstract] Theorem: Partial Derivatives and Continuity
> Let $f : \mathbb{R}^n \to \mathbb{R}$, and assume all $\frac{\partial f}{\partial x_i} (x)$ exist and are continuous. 
>
> Then, $f$ is continuous.
>
> > [!Note] Proof (? Missing something) 
> > 
> > Look at $f(x + h) - f(x)$. We would like to claim that as $h \to 0$, $f(x + h) \to f(x)$.
> > 
> > By the previous proposition, for some $0 < \theta < 1$
> > $$
> > | f(x + h) - f(x) | = | \langle \nabla f(x + \theta h, h) \rangle |
> > $$
> > By Cauchy Schwarz, this is less than or equal to
> > $$
> > \le || \nabla f(x + \theta h) || \cdot || h ||
> > $$
> > But as c, we can bound the first term! 
> > $$
> > || \nabla f(x + \theta h) || \le \max || \nabla f(y) || \cdot || x - y || \le C
> > $$
> > So, this drops to 0.
> 
> > By this proof, in fact, if all the partials exist $\forall x \in O$ and are bounded, then $f$ is still continuous!

Let $f : \mathbb{R}^n \to \mathbb{R}$, $C^1$. Fix $x$, and assume $\nabla f \ne 0$. Then, the maximum of the directional derivative at $x$ is given as
$$
\max_{||P|| = 1} \frac{\partial f}{\partial P} (x)
$$
Is attained for
$$
P = \frac{\nabla f(x)}{|| \nabla f (x) ||}
$$
In other words, the direction of the gradient.

> [!Note] Proof
> If $||P|| = 1$, we have
> $$
> \frac{\partial f}{\partial P} (x) = \langle \nabla f(x), P \rangle
> $$
> By Cauchy-Schwarz, this is
> $$
> \le || \nabla f(x) || \cdot || P || = || \nabla f(x) ||
> $$
> We have an upper bound on our directional derivative! We can attain our upper bound if $P = \frac{\nabla f(x)}{|| \nabla f(x) ||}$.
> $$
> \begin{align*}
> \langle \nabla f(x), P \rangle 
> &= \langle \nabla f(x), \frac{\nabla f(x)}{|| \nabla f(x) ||} \rangle \\ 
> &= \frac{1}{|| \nabla f(x) ||} \langle \nabla f(x), \nabla f(x) \rangle \\
> &= || \nabla f(x) ||
> \end{align*}
> $$
> We've found a maximizer.

We end with a small remark that will segway into the next section. Let $f : \mathbb{R}^n \to \mathbb{R}, C^1$. Then,
$$
\lim_{h \to 0} \frac{f(x + h) - f(x) - \langle \nabla f(x), h \rangle}{||h||} = 0
$$
>  This can be proven by using Cauchy-Schwarz.

We use this to define differentiable functions!

$f : \mathbb{R}^n \to \mathbb{R}$ is **differentiable** at $x$ if $\exists Q \in \mathbb{R}^n$ such that
$$
\frac{f(x + h) - f(x) - \langle Q, h \rangle}{||h||} \to 0
$$
as $h \to 0$.

This is a stronger notion than partial diffentiation! So, $f \in C^1$ implies that $f$ is differentiable, which implies that all partials of $f$ exist. But, the converses are not true!

--- Chapter 14 ---

# Local Approximation of Real-Valued Functions
## First Order Approximation
Recall previously that if $f \in C^1 (\mathbb{R}^n)$, then
$$
f(x + h) - f(x) = \langle \nabla f(x + \theta h), h \rangle
$$
For some $0 < \theta < 1$.

A consequence of this is that
$$
\lim_{h\to 0} \frac{f(x+h) - f(x) - \langle \nabla f(x), h \rangle}{h} = 0
$$
Known as the **first order approximation formula**. In other words,
$$
f(x + h) = f(x) + \langle \nabla f(x), h \rangle + E(x,h) \qquad \lim_{h\to 0} \frac{E(x,h)}{||h||} = 0
$$
As the error drops to 0 when dividing by $||h||$, we can also say that the error is of **first order**, $O(||h||)$.

Letting $y = x+h$, $x$ fixed, this can alternatively be written as
$$
f(y) = f(x) + \langle \nabla f(x), (y - x) \rangle + O( ||x - y|| )
$$
So if $x$ is fixed, and $y$ is cloed to $x$, then we have a close approximation!

How does this relate to the tangent plane of $g$?

Define $G = \{ (y_1, y_2, f(y_1, y_2)) \}$. Define the tangent directions at $(x_1, x_2)$, as
$$
\begin{align*}
&\gamma_1 (t) = (x_1 + t, x_2, f(x_1 + t, x_2)) &\gamma_1'(0) = (1, 0, \frac{\partial f}{\partial x_1} (x_1, x_2)) \\
&\gamma_2 (t) = (x_1, x_2 + t, f(x_1, x_2 + t)) &\gamma_1'(0) = (0, 1, \frac{\partial f}{\partial x_2} (x_1, x_2)) \\
\end{align*}
$$
We can find a vector orthogonal to both of these, giving us a vector that is normal to our function.
$$
N = \left( -\frac{\partial f}{\partial x_1}, \frac{\partial f}{\partial x_2}, 1 \right)
$$
We use this to define the tangent plane at $(x_1, x_2, f(x_1, x_2)$ as
$$
\begin{align*}
&(y_1 - x_1, y_2 - x_2, y_3 - f(x_1,x_2)) \cdot \left( -\frac{\partial f}{\partial x_1}, \frac{\partial f}{\partial x_2}, 1 \right) = 0 \\
&y_3 - f(x_1, x_2) - \frac{\partial f}{d x_1} (x_1, x_2) (y_1 - x_1) - \frac{\partial f}{\partial x_2} (x_1, x_2) (y_2 - x_2) = 0 \\
&= y_3 = f(x_1, x_2) + \frac{\partial f}{d x_1} (x_1, x_2) (y_1 - x_1) + \frac{\partial f}{\partial x_2} (x_1, x_2) (y_2 - x_2)
\end{align*}
$$
Thus, we find that $f(y)$ defined before is actually a tangent plane approximation of our function!

## Second Order Approximation
Let $A$ be an $n \times n$ symmetric matrix (so, $a_{ij} = a_{ji}$ for all $i,j$). Define the function 
$$
Q(h) = \langle Ah, h \rangle = \sum_{i,j=1}^n a_{ij} h_i h_j
$$
This is the quadratic form for $A$. The main application of this, is when we for when we have the Hessian Matrix of a function (assuming $f \in C^2$)
$$
A = \nabla^2 f(x) = 
\begin{bmatrix}
\frac{\partial^2 f}{\partial x_1^2} & \dots & \frac{\partial^2 f}{\partial x_1 \partial x_n} \\
\vdots & & \vdots \\
\frac{\partial^2 f}{\partial x_n \partial x_i} & \dots & \frac{\partial^2 f}{\partial x_n^2}
\end{bmatrix}
$$

If $f \in C^2 (\mathbb{R})$, $x,h$ fixed, then
1. $$
   \frac{d}{dt} f(x + th) = \langle \nabla f(x + th), h \rangle = \sum_{i=1}^n \frac{\partial f}{\partial x_i} (x + th) h_i
   $$
2. $$
   \frac{d^2}{dt^2} f(x + th) = \langle \nabla^2 f(x + th, h) \rangle = \sum_{i,j=1}^n \frac{\partial^2 f}{\partial x_i \partial x_j} (x + th) h_i h_j
   $$
   
> [!Info] Remark
> If $f \in C^3$, then
> $$
> \frac{d^3}{dt^3} f(x + th) = \sum_{i,j,k=1}^n \frac{\partial^3 f}{\partial x_i \partial x_j \partial x_k} (x + th) h_i h_j h_k
> $$

> [!Note]- Proof 
> For (1), this is a chain rule.
> 
> For (2), we have
> $$
> \begin{align*}
> \frac{d}{dt} \left[ \frac{d}{dt} f(x + th) \right] 
> &= \frac{d}{dt} \left[ \sum_{i=1}^n \left( \frac{\partial f}{\partial x_i} \right) (x + th) h_i \right] \\
> &= \sum_{i=1}^n \left[ \sum_{j=1}^n \frac{\partial}{\partial x_j} \frac{\partial f}{\partial x_i} (x + th) h_j \right] h_i
> \end{align*}
> $$

Let $A$ be an $n \times n$ matrix, $A = (a_{ij})$. Define the **Hilbert-Schmidt norm** of $A$ to be
$$
||A|| = \left( \sum_{i,j=1}^n a_{ij}^2 \right)^{1/2}
$$
In other words, we think of the matrix as a long vector, and take the vector norm.

> [!Abstract] Generalized Cauchy Schwarz Inequality
> $$
> || Ah || \le ||A|| \cdot ||h||
> $$
> 
> > [!Note]- Proof
> > 
> > $$
> > \begin{align*}
> > Ah 
> > &= 
> > \begin{bmatrix}
> > \text{Row 1} \\ \vdots \\ \text{Row n}
> > \end{bmatrix} h \\
> > &= 
> > \begin{bmatrix}
> > \langle r_1, h \rangle \\ \vdots \\ \langle r_n, h \rangle
> > \end{bmatrix} \\
> > ||Ah||^2 &= \left( \langle r_1, h \rangle^2 + \dots + \langle r_n, h \rangle^2 \right) \\
> > &\le (||r_1||^2 + \dots + ||r_n||^2) ||h||^2 \\
> > &\le ||h||^2 \sum_{i,j=1}^n a_{ij}^2 \\
> > &= ||A||^2 ||h||^2
> > \end{align*}
> > $$

Let $A : \mathbb{R}^n \to \mathbb{R}^m$. We define the **operator norm** of $A$ as
$$
||A||_\text{op} = \max_{||h|| = 1} || Ah || 
$$
Based on this, we can find that for $||h|| = 1$,
$$
||Ah|| \le ||A||_{HS} \qquad ||A||_{op} \le ||A||_{HS}
$$

Let $A$ be an $n \times m$, symmetric matrix. $A$ is **positive definite** if 
$$
\langle Au, u \rangle > 0
$$
For all $u \ne 0$. Conversely, $A$ is negative definite if $\forall u \ne 0$,
$$
\langle Au, u \rangle < 0
$$

> [!Abstract] Lemma
> Let $A$ be semmtric positive definite matrix. Then, there exists a $c > 0$ such that
> $$
> \langle Au , u \rangle \ge c ||u||^2
> $$
> For all $u \in \mathbb{R}^n$.
>
> > [!Note]- Proof
> > 
> > Note that the LHS and the RHS are both homogeneous degree 2.
> > $$
> > \langle A(tu), tu \rangle = t^2 \langle Au, u \rangle \qquad ||tu||^2 = t^2 ||u||^2 \quad \forall t > 0, \forall u \in \mathbb{R}^n
> > $$
> > Thus, our equation is true for $u$ if and only if it is true for any other $tu$, $(t > 0)$.
> > 
> > Thus, it suffices to show that our equation is true for unit vectors $\frac{u}{||u||}$, as by the earlier proposition, the argument applies for all $u$. Then,
> > $$
> > \langle Au, u \rangle \ge c \qquad \forall ||u|| = 1
> > $$
> > This creates a continuous function along a $S^{n-1}$ hypersphere in $\mathbb{R}^n$, which is sequentially compact. Thus, it must have a minimum and maximum. Choose the minimum to find our $c$.
> > > In fact, we can find $c$ by taking the minimum of the eigenvalues.


