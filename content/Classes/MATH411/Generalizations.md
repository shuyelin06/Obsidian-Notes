---
title: Generalizations
tags:
- math411
---

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

> [!Example]- Example: Continuity and Closure
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
>
>
> Let's now consider the converse. Let $f : \mathbb{R} \to \mathbb{R}$. Assume $G = \{ (x, f(x)) : x \in \mathbb{R} \}$ is closed. Does it follow that $f$ is continuous?
> 
> Let $\{x_k\} \in \mathbb{R}$, where $\{x_k\} \to x$. We want to show that $\{f(x_k)\} \to f(x)$. 
> 
> Using this, we can form a sequence $\{(x_k, f(x_k))\} \subseteq G$. Then, if $\{ (x_k, f(x_k) \} \to (x,y)$, then $f(x) = y$. So, if there exists a $y$ such that $\{f(x_k)\} \to y$, then $y = f(x)$ where $\{x_k\} \to x$.
> 
> But do we know if $\{f(x_k)\}$ converges? In fact, closure only says that **if** the sequence converges, then its result is in the set! However, we may be able to find a function that fails to satisfy this.
> 
> Let 
> $$
> f(x) = \frac{1}{x}, f(0) = 0 \qquad x_k = \frac{1}{k}
> $$
> Then, $f(x)$ is not continuous at $x = 0$, yet the set $G$ is still closed!


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

