---
title: Integrals
tags:
- math410
---

# Limsup / Liminf
Consider a sequence that oscillates between $-1$ and $1$ as $n \to \infty$. While its limit does not exist, it does still have a "notion" of two different limits! This is the idea behind limsup (**limit superior**) and liminf (**limit inferior**) - they let us make claims about the limit for sequences, which may not necessarily converge to a single value!

Let $\{x_n\}$ be bounded. Then,
1. We say the **limit superior (limsup)**, is
   $$
   \limsup_{n\to\infty} x_n = \lim_{n\to\infty} \sup_{k \ge n} x_k
   $$
   Equivalent to the limit of the upper bound of $x_n$, for all $n$.
2. We say the **limit inferior (liminf)** is
   $$
   \liminf_{n\to\infty} x_n = \lim_{n\to\infty} \inf_{k \ge n} x_k
   $$
   Equivalent to the limit of the lower bound of $x_n$, for all $n$.
> Note that this can be extended to unbounded sequences too! We just won't cover them.

Note that by this definition, $\bar{x}_n = \sup_{k \ge n} x_k$ is a decreasing sequence! And furthermore, because this sequence is bounded and decreasing, by the MCT, it converges to the infimum.
> This similarly holds for the liminf.

So we can alternatively write the liminf and limsup as
$$
\begin{align*}
    \limsup_{n\to\infty} x_n = \inf_{n\ge 1} (\sup_{k \ge n} x_k) \\
    \liminf_{n\to\infty} x_n = \sup_{n\ge 1} (\inf_{k \ge n} x_k )
\end{align*}
$$

> [!Example]+ Example: Computing Limsup
> Suppose we have the sequence
> $$
> x_n = \frac{(-1)^n}{n}
> $$
> 
> We find the limsup as
> $$
> \bar{x}_n = \sup_{k \ge n} x_k = 
> \begin{cases}
>     (-1)^{n+1} / n+1 & \text{n odd} \\
>     (-1)^n / n & \text{n even}
> \end{cases}
> $$
> Taking the limit as $n \to \infty$, this converges to 0. So, our limsup is 0.
> > We can similarly show that the liminf is 0. 

> [!Example]- Example: Computing Limsup (2)
> Limsups are not always easy to prove! Consider
> $$
> \lim_{n\to\infty} \sin(n) = 1
> $$
> While it seems arbitrarily, this is difficult to prove! We need to prove that $\sin(n)$ for $n \in \mathbb{N}$ is dense in $[-1,1]$.

> [!Abstract] Theorem: Addition of Limsup / Liminf
> $$
> \begin{align*}
>     \limsup_{n\to\infty} (x_n + y_n) \le \limsup_{n\to\infty} x_n + \limsup_{n\to\infty} y_n \\
>     \liminf_{n\to\infty} (x_n + y_n) \ge \liminf_{n\to\infty} x_n + \liminf_{n\to\infty} y_n \\
> \end{align*}
> $$
>
> > [!Note]- Proof (Limsup)
> > 
> > By the upper bound nature of supremums,
> > $$
> > x_n + y_n \le \sup_{k \ge n} x_k + \sup_{k \ge n} y_k
> > $$
> > And furthermore, as the supremum of $x_n + y_n$ is the least upper bound,
> > $$
> > \sup_{k \ge n} (x_k + y_k) \le \sup_{k \ge n} x_k + \sup_{k \ge n} y_k
> > $$
> > We apply the limit on both sides to obtain our theorem.

The **limit set** of $\{x_n\}_{n=1}^\infty$ is
$$
\{ x \in \mathbb{R} | \exists x_{n_j} \to x \}
$$
As $j \to \infty$. In other words, its the set of all limits that $\{x_n\}$'s subsequences converge to.

> [!Example]+ Example: Limit Sets
> $$
> x_n =
> \begin{cases}
>     \frac{5}{n+1} & \text{n odd} \\
>     \frac{(-1)^n + n^2}{n^2} & \text{n even}
> \end{cases}
> $$ 
> 
> Then, our limit set is $S = \{ 0, 1 \}$. 

Interestingly enough, in the above example, our liminf is 0, and our limsup is 1! This is no coincidence - we can use limit sets to compute our liminf and limsup!

> [!Abstract] Theorem: Limit Sets and Liminf / Limsup
> Let $\{x_n\}$ be a bounded sequence, and let $S$ be the limit set.
>
> Then, 
> $$
> \begin{align*}
>     \limsup_{n\to\infty} x_n = \sup(S) \\
>     \liminf_{n\to\infty} x_n = \inf(S)
> \end{align*}
> $$
> > We omit the proof.

> [!Abstract] Theorem: Convergence and Limsup / Liminf
> $$
> \limsup x_n = \liminf x_n \iff \lim x_n = L \text{ exists}
> $$
> In which case, all 3 limits are equal to $L$.
>
> > [!Note]- Proof (Forward Direction)
> > 
> > #### Proof ($\rightarrow$)
> > Assume $\liminf x_n = \limsup x_n = L$. Then, for any $n$,
> > $$
> > \inf_{k \ge n} x_k \le x_n \le \sup_{k \ge n} x_k
> > $$
> > 
> > Taking the limit of both sides as $n \to \infty$, we get
> > $$
> > L \le \lim_{n\to\infty} x_n \le L
> > $$
> > Forcing our limit to be equal to $L$.


# Integration
## Darboux Integrals
Suppose we have a function $f: [a,b] \to \mathbb{R}$. In this section, we formally define what an **integral** is.
$$
\int_a^b f(x) dx
$$

> [!Info] Definition of an Integral
> Recall that in earlier calculus classes, we define an integral as the sum of progressionally smaller rectangles under the curve, known as a **Riemann Sum**.
> $$
> \int_a^b f(x) dx = \lim_{n\to\infty} \sum_{i=1}^n f(x_i) \Delta x_i
> $$

Consider the closed interval $[a,b]$, and partition it using $n + 1$ points $x_0, x_1, x_2, \dots x_{n} \in [a,b]$, where 
$$
x_0 = a \qquad x_i < x_{i+1}, \forall i \qquad x_n = b
$$

Let $f$ be bounded, and consider the interval between any two partition points $[x_{i-1}, x_i]$. By assumption, we can define the quantities $m_i$, the infimum of $f$ along this interval, and $M_i$, the supremum of $f$ along this interval.
$$
m_i = \inf_{x \in [x_{i-1}, x_i]} f(x) \qquad \qquad M_i = \sup_{x \in [x_{i-1}, x_i]} f(x)
$$
And use this to define the **lower ($L$) and upper ($U$) Darboux sums** of $f$,
$$
L(f,P) = \sum_{i=1}^n m_i \Delta x_i \qquad \qquad U(f,P) = \sum_{i=1}^n M_i \Delta x_i
$$
Where $\Delta x_i = x_i - x_{i-1}$.

> Note that as $\Delta x_i$ is the width of our interval, we are defining rectangles under $f$ (whose heights are either the infimum of supremum along the interval)! This is very similar to Riemann Sums.

> [!Abstract] Theorem: Darboux Sums
> Suppose $m \le f(x) \le M$ for all $x \in [a,b]$. Then,
> $$
> m(b - a) \le L(f,P) \le U(f,P) \le M(b-a)
> $$
>
> > [!Note]- Proof
> >
> > $P = \{x_0, \dots x_n\}$ be a partition of $[a,b]$, where $x_i$ is a subinterval, and let $m_i$, $M_i$ be the infimum and supremums along this subinterval. Then,
> > $$
> > \begin{align*}
> >     m \Delta x_i \le f(x) \Delta x_i \le M \Delta x_i \\
> >     \Delta x_i \le m_i \Delta x_i \le M_i \Delta x_i \le  M \Delta x_i
> > \end{align*}
> > $$
> > 
> > Summing this over all of the subintervals, we get
> > $$
> > m (b - a) \le L(f,P) \le U(f,P) \le M (b - a)
> > $$

Now let $P$ be a partition of $[a,b]$. Then, we say $P^*$ is a **refinement** of $P$ if $P^*$ contains all points of $P$, and possibly others.
> A refinement is essentially just a partition with more points inside it.

> [!Example]+ Example: Refinement
> $$
> \left\{ 0, \frac{1}{3}, \frac{1}{2}, 1 \right\} 
> $$
>
> The below is an example of a refinement of this partition
> $$
> \left\{ 0, \frac{1}{3}, \frac{1}{2}, \frac{3}{4}, 1 \right\}
> $$

Refinements are important, as they let us define finer and finer sums for $L$ and $U$!

> [!Abstract] Theorem: Refinements and Darboux Sums
> Let $P$ be a partition of $[a,b]$, and $P^*$ refine $P$. Then,
> $$
> \begin{align*}
>     L(f,P) \le L(f,P^*) \\
>     U(f,P) \ge U(f,P^*)
> \end{align*}
> $$
>
> > This should intuitively make sense! If we more finely divide up $[a,b]$, then the minimum of $f$ along our new subintervals can only increase, and the maximum of $f$ along these subintervals can only decrease!

> [!Abstract] Theorem: Partitions and Darboux Sums
> For any partitions $P_1$ and $P_2$ of $[a,b]$, lower sums are always less than upper sums.
> $$
> L(f, P_1) \le U(f, P_2)
> $$
>
> > [!Note]- Proof
> > 
> > Define the common refinement of $P_1$ and $P_2$, by combining them as $P^* = P_1 \cup P_2$. Then, we can apply our previous theorem to obtain
> > $$
> > L(f, P_1) \le L(f, P^*) \le U(f, P^*) \le U(f, P_2)
> > $$

We can use these theorems to define what an integral is!

Let $P$ be an arbitrary partition of $[a,b]$. Then, we define the **lower / upper (Darboux) integral** as
$$
\underline{\int_a^b} f = \sup_P \{ L(f,P) \} \qquad \overline{\int_a^b} f = \inf_P \{ U(f,P) \}
$$
Or in other words, the maximum lower sum, and the minimum upper sum over all possible partitions $P$.
> Note that the $P$ underneath the supremums and infimums is notation! We're essentially applying a "supremum / infimum" over all possible $L$ and $U$, where $P$ is arbitrary (like the $dx$ in an integral).

If these two integrals are equal, then we say $f$ is **integrable** (in terms of Darboux) and we write
$$
\int_a^b  f = \underline{\int_a^b} f = \overline{\int_a^b} f
$$
for the commmon value.

> [!Abstract] Theorem: Darboux Sums and Integrals
> Let $f: [a,b] \to \mathbb{R}$ be a function. Then,
>
> $$
> L(f,P) \le \underline{\int_a^b} f \le \overline{\int_a^b} f \le  U(f,P)
> $$
>
> > [!Note]- Proof
> > 
> > The first and last inequalities naturally hold by definition of infimums and supremums.
> >
> > We apply our theorem above. For any two arbitrary partitions $P_1, P_2$,
> > $$
> > L(f, P_1) \le U(f, P_2)
> > $$
> > 
> > Because $P_1$ and $P_2$ are arbitrary, we can apply our supremum on $P_1$ to obtain
> > $$
> > \sup_{P_1} L(f, P_1) \le U(f, P_2)
> > $$
> > We know that the supremum exists, as $L(f,P_1)$ is bounded above by $U$. 
> >
> > By the same idea, we apply our infimum on $P_2$ to obtain
> > $$
> > \sup_{P_1} L(f, P_1) \le \inf_{P_2} U(f, P_2)
> > $$
> > Which translates to our integrals by definition!

> [!Example]+ Example: Computing Darboux Integrals
> Consider the constant function over interval $[a,b]$, $f(x) = c$.
>
> We find our integral.
> $$
> \begin{align*}
>     &L(f,P) = \sum_{i=1}^n m_i \Delta x_i = \sum_{i=1}^n c \Delta x_i = c (b - a) \\
>     &U(f,P) = \sum_{i=1}^n M_i \Delta x_i = \sum_{i=1}^n c \Delta x_i = c (b - a) \\
>     &\sup_P L(f,P) = c(b - a) = \inf_P U(f,P) \\
>     &\int_a^b f = c (b - a)
> \end{align*}
> $$

> [!Example]- Example: Computing Darboux Integrals
> Consider the Dirichlet function
> $$
> f(x) = 
> \begin{cases}
>     0 & x \in \mathbb{Q} \\
>     1 & x \not\in \mathbb{Q}
> \end{cases}
> $$
> 
> Is $f$ integrable along $[0,1]$?
> 
> Because the rationals / irrationals are dense, any subinterval will always contain a rational and an irrational, so $f$ will always be both 0 and 1 at some point in the interval.
> $$
> \begin{align*}
>    &L(f,P) = \sum_{i=1} m_i \Delta x_i = \sum_{i=1} 0 \Delta x_i = 0 \\
>    &\sup_P L(f,P) = 0 \\
>    &U(f,P) = \sum_{i=1} M_i \Delta x_i = \sum_{i=1} 1 \Delta x_i = (1 - 0) \\
>    &\inf_P U(f,P) = 1 \\
>    &\sup_P L(f,P) \ne \inf_P U(f,P) 
> \end{align*}
> $$
> 
> As these are not equal, our function is not integrable along $[0,1]$ in the sense of the Riemann Darboux.

## Archimedes-Riemann Theorem
Computing these integrals can be annoying, especially as we need to compute infimums and supremums! The below theorem can help simplify our integral computations in specific cases.

> [!Abstract] Theorem: Archimedes-Riemann Theorem
> Let $f: [a,b] \to \mathbb{R}$ be bounded. Then, $f$ is integrable if and only if there exists a sequence of partitions $\{P_n\}$ such that
> $$
> \lim_{n \to \infty} ( U(f,P_n) - L(f,P_n) ) = 0
> $$
> In this case, we say that $\{P_n\}$ is **archimedian**.
> 
> Furthermore, in the case that it is integrable,
> $$
> \int_a^b f = \lim_{n\to\infty} U(f,P_n) = \lim_{n\to\infty} L(f,P_n)
> $$
>
> > [!Note]- Proof
> > 
> > #### Proof ($\leftarrow$)
> > Suppose there exists a sequence of partitions $\{P_n\}$ such that 
> > $$
> > \{ U(f,P_n) - L(f, P_n) \} \to 0
> > $$
> > 
> > We know that
> > $$
> > \begin{align*}
> >     \overline{\int_a^b} f \le U(f,P_n) \\
> >     \underline{\int_a^b} f \ge L(f, P_n)
> > \end{align*}
> > $$
> > 
> > So we use these to obtain
> > $$
> > 0 \le \overline{\int_a^b} - \underline{\int_a^b} f \le U(f,P_n) - L(f, P_n) \to 0
> > $$
> > So by squeeze theorem, 
> > $$
> > \overline{\int_a^b} f = \underline{\int_a^b} f
> > $$
> >
> > #### Proof ($\rightarrow$)
> > Suppose
> > $$
> > \overline{\int_a^b} f = \underline{\int_a^b} f = \int_a^b f
> > $$
> > 
> > By definition,
> > $$
> > \overline{\int_a^b} f = \inf_P U(f,P) \qquad \underline{\int_a^b} f = \sup_P L(f,P)
> > $$
> > 
> > So by the epsilon-definition of supremums, we know that $\forall \epsilon > 0$, there exists a $L(f,P)$, $U(f,P)$ such that
> > $$
> > L(f,P) < \inf_P U(f,P) + \epsilon \qquad \sup_P L(f,P) - \epsilon < U(f,P)
> > $$
> > We choose $\epsilon = 1/n$, and for all $n \in \mathbb{N}$ choose these $L$'s and $U$'s to find a sequence. Note that these sequences converge by squeeze theorem.
> > $$
> > \begin{align*}
> > \inf_P U(f,P) < L(f,P_n) < \inf_P U(f,P) + \frac{1}{n} \\
> > \sup_P L(f,P) - \frac{1}{n} < U(f,P'_n) < \sup_P L(f,P)
> > \end{align*}
> > $$ 
> > 
> > Our partitions are not guaranteed to be the same, so we can take the union of them, $P'_n \cup P_n = Q_n$
> > $$
> > \begin{align*}
> > \inf_P U(f,P) < L(f,Q_n) \le L(f,P_n) < \inf_P U(f,P) + \frac{1}{n} \\
> > \sup_P L(f,P) - \frac{1}{n} < U(f,P'_n) \le U(f, Q_n) < \sup_P L(f,P)
> > \end{align*}
> > $$ 
> > Finally,
> > $$
> > \begin{align*}
> >     0 
> >     &\le U(f, Q_n) - L(f,Q_n) \\
> >     &< \int_a^b f + \frac{1}{n} + \frac{1}{n} - \int_a^b f \\
> >     &= \frac{2}{n} \to 0
> > \end{align*}
> > $$
> > 
> > We apply squeeze theorem to obtain convergence.
> > 
> > 
> > We now show that
> > $$
> > \int_a^b f = \lim_{n\to\infty} U(f,P_n)
> > $$
> > To do this, we use the property of infimums that
> > $$
> > \begin{align*}
> >     \overline{\int_a^b} f \le U(f, P_n) \\
> >     0 \le U(f,P_n) - \overline{\int_a^b} f \le U(f,P_n) - L(f,P_n)
> > \end{align*}
> > $$
> > 
> > As $n \to 0$, we apply squeeze theorem.
> > $$
> > U(f,P_n) - \overline{\int_a^b} = 0 \Longrightarrow \overline{\int_a^b} = U(f,P_n)
> > $$
> > > We have similar argument for the limit of the lower sum!

This theorem is really important, and can be used to prove a lot! In fact, many of the below properties of integrals can be proven using the Archimedes-Riemann Theorem. See below.


## Properties of Integrals
Below, we discuss various useful properties of integrals.

### Monotonicity and Integrals
> [!Abstract] Theorem: Monotonicity and Integrability
> Any monotone function $f : [a,b] \to \mathbb{R}$ is integrable.
> > The monotonicity on $f$ and its restricted domain automatically implies boundedness!
>
> > [!Note]- Proof 
> > 
> > Let $P_n = \{ x_0, x_1, \dots x_n \}$ where $\Delta x_i = x_i - x_{i-1} = (b-a) / n$ is constant.
> > 
> > We show that $\{P_n\}$ is Archimedian, to apply the previous theorem.
> > $$
> > \begin{align*}
> >     0 &\le U(f,P_n) \Delta x - L(f, P_n) \\
> >       &= \sum_{i=1}^n M_i \Delta x - \sum_{i=1}^n m_i \Delta x \\
> >       &= \frac{b-a}{n} \left( \sum_{i=1}^n f(x_i) - \sum_{i=1}^n f(x_{i-1}) \right) \\
> >       &= \frac{b-a}{n} (f(x_n) - f(x_0)) \\
> >       &= \frac{b-a}{n} (f(b) - f(a)) \to 0 
> > \end{align*}
> > $$
> > 
> > Thus, we apply our above theorem to obtain integrability.

We can use a similar idea to show that any step function is integrable, though this is much more difficult.

> [!Abstract] Lemma
> Let $\{P_n\}$ be Archimedian for $f: [a,b] \to \mathbb{R}$. Then any refinement $\{P_n^*\}$ is also Archimedian.
>
> > [!Note]- Proof
> > 
> > By property of refinements, $U$ will get smaller, and $L$ will get larger, so
> > $$
> > \begin{align*}
> >     0 &\le U(f, P_n^*) - L(f, P_n^*) \\
> >     &\le U(f,P_n) - L(f,P_n) \to 0
> > \end{align*}
> > $$

> [!Abstract] Theorem: Monotonicity
> Let $f(x) \le g(x)$ for all $x \in [a,b]$. Then,
> $$
> \int_a^b f \le \int_a^b g
> $$
> 
> > [!Note]- Proof
> >
> > Let $\{P_n\}$ be Archimedian for $f$, and $\{P_n'\}$ for $g$. Let $Q_n = P_n \cup P_n'$, which is still Archimedian for $f$ and $g$!
> >
> > With a common refinement, we have $U(f, Q_n) \le U(g, Q_n)$. Then, as $n \to \infty$, by the Archimedian Riemann theorem, we are done.

### Additivity, Linearity, Absolute Value of Integrals
> [!Abstract] Theorem: Additivity of Integrals
> Let $f : [a,b] \to \mathbb{R}$ be an integrable function. Then, $\forall c \in (a,b)$,
> $$
> \int_a^b f = \int_a^c f + \int_c^b f
> $$
> 
> > [!Note]- Proof
> > 
> > Suppose there exists an Archimedian Sequence $\{P_n\}$ for $f$ on $[a,b]$. Without loss of generality, suppose $\{P_n\}$ contains $c$ (since any refinement is also Archimedian).
> > 
> > Split $\{P_n\}$ into mutually exclusive partitions $P_n'$ and $P_n''$ based on $c$. We want to show that both subsequences are Archimedian.
> > 
> > We have
> > $$
> > \begin{align*}
> >     &U(f,P_n) - L(f,P_n) \to 0 \\
> >     &(U(f,P_n') + U(f,P_n'')) - (L(f,P_n') + L(f,P_n'')) \to 0 \\
> >     &(U(f,P_n') - L(f,P_n')) + (U(f,P_n'') - L(f,P_n'')) \to 0
> > \end{align*}
> > $$
> > 
> > Because $U(f,P_n') - L(f,P_n')$ and $U(f,P_n'') - L(f,P_n'')$ are both non-negative for all $n$, for this sequence to converge it must be true that they both converge to 0.

> [!Abstract] Theorem: Linearity of Integrals
> Let $\alpha, \beta \in \mathbb{R}$, and $f,g : [a,b] \to \mathbb{R}$ be integrable. Then,
> $$
> \int_a^b (\alpha f + \beta g) = \alpha \int_a^b f + \beta \int_a^b g
> $$
> 
> > [!Note]- Proof (Half)
> > 
> > We show the first part of the proof.
> > $$
> > \int_a^b f + g = \int_a^b f + \int_a^b g
> > $$
> > 
> > Let $P_n$ be an Archimedian sequence for $f$ and $g$ on $[a,b]$, which is possible by common refinement.
> >    
> > We know that
> > $$
> > \begin{align*}
> >     f(x) + g(x) \le \sup f(x) + \sup g(x) \\
> >     \sup( f(x) + g(x) ) \le \sup f(x) + \sup g(x) \\
> >     U(f + g, P_n) \le U(f,P_n) + U(g,P_n)
> > \end{align*}
> > $$
> >    
> > Similarly, we can obtain
> > $$
> > L(f + g, P_n) \ge L(f,P_n) + L(g,P_n)
> > $$
> >    
> > Giving us
> > $$
> > \begin{align*}
> >     &L(f,P_n) + L(g,P_n) \le L(f + g, P_n) \le U(f + g, P_n) \le U(f,P_n) + U(g,P_n) \\
> >     &\int_a^b f + \int_a^b f \le \int_a^b f + g \int_a^b f + g \le \int_a^b f + \int_a^b g &n \to \infty \\
> >     &\int_a^b f + \int_a^b g = \int_a^b f + g
> > \end{align*}
> > $$

> [!Abstract] Theorem: Absolute Value and Integrals
> Let $f$ and $|f|$ be integrable on $[a,b]$. Then, 
> $$
> \left| \int_a^b f \right| \le \int_a^b |f|
> $$
> 
> > [!Note]- Proof
> > 
> > We know that
> > $$
> > -|f(x)| \le f(x) \le |f(x)|
> > $$
> > By monotonicity,
> > $$
> > -\int_a^b |f| \le \int_a^b f \le \int_a^b |f|
> > $$
> > But this is essentially an absolute value!
> > $$
> > \left| \int_a^b f \right| \le \int_a^b |f|
> > $$


### Continuity and Integrals
The follow theorems guarantee integrability for continuous functions.

> [!Abstract] Theorem: Continuity and Integrability
> Let $f$ be a continuous function on compact interval $[a,b]$. Then, its integral along this interval exists.
>
> > [!Note]- Proof
> >
> > Since we have a continuous function on a compact interval, we know $f$ is uniformly continuous. By definition, $\forall \epsilon > 0, \exists \delta > 0$ such that $\forall x,y \in [a,b]$,
> > $$
> > |x - y| < \delta \to |f(x) - f(y)| < \epsilon
> > $$
> >
> > For later convenience, take the constant $\frac{\epsilon}{b-a}$.
> >
> > Let $\{P_n\} = \{x_0, \dots, x_n\}$ be a uniform sequence of partitions for $[a,b]$, where $x_0 = a, x_n = b$. As the partition is uniform, we have that $\Delta x_i = \frac{b-a}{n}$. We wish to show that $\{P_n\}$ is Archimedian.
> > 
> > We know that by a theorem,
> > $$
> > \begin{align*}
> >     0 
> >     &\le U(f,P_n) - L(f,P_n) \\
> >     &\le \sum_{i=1}^n \left( \sup_{x \in [x_{i-1}, x_i]} f \right) \Delta x_i - \sum_{i=1}^n \left( \inf_{x \in [x_{i-1}, x_i]} f \right) \Delta x_i 
> > \end{align*}
> > $$
> > 
> > By the Extreme Value theorem, we know that for some $u_i, v_i \in [x_{i-1}, x_i]$,
> > $$
> > \sup_{x \in [x_{i-1}, x_i]} f = f(u_i) \qquad \inf_{x \in [x_{i-1}, x_i]} f = f(v_i)
> > $$
> > 
> > This gives us
> > $$
> > \begin{align*}
> >     0 &\le \sum_{i=1}^n \left( \sup_{x \in [x_{i-1}, x_i]} f \right) \Delta x_i - \sum_{i=1}^n \left( \inf_{x \in [x_{i-1}, x_i]} f \right) \Delta x_i  \\
> >     &\le \sum_{i=1}^n ( f(u_i) - f(v_i) ) \Delta x_i \\
> >     &\le \max_{1 \le i \le n} ( f(u_i) - f(v_i) ) \sum_{i=1}^n \Delta x_i \\
> >     &\le f(u_{i_0}) - f(v_{i_0}) (b - a)
> > \end{align*}
> > $$
> > 
> > Where $u_{i_0}, v_{i_0}$ is the greatest difference between the maximum and minimum.
> > 
> > If $|u_{i_0} - v_{i_0}| < \delta$, we can apply uniform continuity, we have
> > $$
> > f(u_{i_0}) - f(v_{i_0}) (b - a) < \frac{\epsilon}{b-a} (b - a) < \epsilon
> > $$
> > 
> > And since this holds for all $\epsilon$, we can let $\epsilon \to 0$ and apply squeeze theorem, to have
> > $$
> > \{ U(f,P_n) - L(f,P_n) \} \to 0
> > $$
> > 
> > To guarantee the $|u_{i_0} - v_{i_0}| < \delta$ condition, we choose $N$ large enough such that $\Delta x_i < \delta$, so that $\Delta x_i < \delta$ for all $n \ge N$.

> [!Abstract] Theorem: Continuity and Integrability
> Let $f$ be continuous on open $(a,b)$ and bounded on $[a,b]$. Then, $\int_a^b f$ exists and does NOT depend on $f(a)$ or $f(b)$.
> 
> > [!Note]- Proof (Sketch)
> > 
> > Create an interval $I_n = [a + \frac{1}{n}, b - \frac{1}{n}]$. For each $I_n$, choose a partition $\{P_n^*\}$ satisfying
> > 
> > $$
> > 0 \le U(f, P_n^*) - L(f,P_n^*) \le \frac{1}{n}
> > $$
> > Whose existence is guaranteed by our previous proof.
> > 
> > Let $P_n = P_n^* \cup \{a,b\}$. We show that $\{P_n\}$ is Archimedian for $[a,b]$ to show that $\int_a^b f$ exists, and then show that
> > $$
> > U(f,P_n^*) \to \int_a^b f
> > $$
> > 
> > Since $P_n^*$ doesn't depend on $a$ or $b$, it must be true that the integral also doesn't depend on $f(a)$ or $f(b)$!

> [!Example]+ Example: Continuity and Integrability
> $$
> f = \begin{cases}
>       \sin(1/x) & x \in (0,1) \\
>       0 & x = 0
>     \end{cases}
> $$
> 
> As $f$ is continuous on $(0,1)$, and bounded on $[0,1]$, its integral $\int_0^1 f$ exists.

## Fundmental Theorems of Calculus
> [!Abstract] Theorem: First Fundamental Theorem of Calculus
> Let $F$ be a continuous function on $[a,b]$, and $F'$ be bounded and continuous on $[a,b]$.
>
> Then,
> $$
> \int_a^b F'(x) dx = F(b) - F(a) 
> $$
>
> > [!Note]- Proof
> >
> > Since $F'$ is continuous and bounded, our integral $\int_a^b F'$ exists by a theorem.
> > 
> > Let $P = \{x_0, \dots, x_n\}$ be a partition. Because $F$ is continuous, we apply Mean Value Theorem on each subinterval $[x_{i-1}, x_i]$, we know that $\exists c_i$ such that
> > $$
> > F(x_i) - F(x_{i-1}) = F'(c_i) \Delta x_i
> > $$
> > 
> > Since $F'$ is bounded, we know that 
> > $$
> > \begin{align*}
> > \inf_{[x_{i-1}, x_i]} F'(x) \le &F'(c_i) \le \sup_{[x_{i-1}, x_i]} F'(x) \\
> > m_i \le &F'(c_i) \le M_i
> > \end{align*}
> > $$
> > 
> > So $m_i \Delta x_i \le F(x_i) - F(x_{i-1}) \le M_i \Delta x_i$. We take the sum over all the subintervals to get
> > $$
> > L(F',P) \le F(b) - F(a) \le U(F',P) \\
> > $$
> > 
> > As this holds for all lower sums, we have
> > $$
> > \begin{align*}
> >     \sup_P L(F',P) \le F(b) - F(a) \le \inf_P U(F',P) \\
> >     \underline{\int_a^b} F' \le F(b) - F(a) \le \overline{\int_a^b} F'
> > \end{align*}
> > $$
> > 
> > And as we assume integrability, this gives us
> > $$
> > \int_a^b F' \le F(b) - F(a) \le \int_a^b F' \Longrightarrow \int_a^b F' = F(b) - F(a)
> > $$

We need the below theorems to prove the second fundamental theorem.

> [!Abstract] Lemma
> If $a > b$, then
> $$
> \int_a^b f = - \int_b^a f
> $$

> [!Abstract] Theorem: Integral Mean Value Theorem
> If $f$ is a continuous function on $[a,b]$, then $\exists c \in (a,b)$ such that
> $$
> \int_a^b f = f(c) (b - a)
> $$
> 
> > [!Note]- Proof
> > 
> > By EVT, $f(x_\text{min}) \le f(x) \le f(x_\text{max})$. We integrate this to obtain
> > $$
> > \begin{align*}
> > f(x_\text{min}) (b - a) \le \int_a^b f \le f(x_\text{max}) (b - a) \\
> > f(x_\text{min}) \le \frac{1}{(b-a)} \int_a^b f \le f(x_\text{max})
> > \end{align*}
> > $$
> > 
> > Now, for all points between the minimum and maximum, we can find a $c$ by intermediate value theorem equal to $f$ at that point - finishing our proof.


> [!Abstract] Theorem: Second Fundamental Theorem of Calculus
> If $f$ is a continuous function on $[a,b]$, then for any $x \in (a,b)$, 
> $$
> \frac{d}{dx} \int_a^x f(t) dt = f(x)
> $$
>
> > [!Note]- Proof
> > 
> > Let $\{x_n\} \to x_0$, $\{x_n\} \in [a,b] / \{x_0\}$. By definition of derivative,
> > $$
> > \begin{align*}
> > \frac{\int_a^{x_n} f - \int_a^{x_0} f}{x_n - x_0} 
> > &= \frac{\int_{x_0}^{x_n} f}{x_n - x_0} \\
> > &= \frac{1}{x_n - x_0} f(C_n) \int_{x_0}^{x_n} 1 dx \\
> > &= f(C_n)
> > \end{align*}
> > $$
> > 
> > By the Integral Mean Value Theorem where $C_n$ is between $x_0$ and $x_n$. We evaluate this and take the limit to obtain $f(x_0)$.

## Extra Integral Properties
> [!Abstract] Theorem: Generalized Integral MVT
> Let $g$ be integrable and $g(x) > 0$, and let $f : [a,b] \to \mathbb{R}$ be continuous. Then, $\exists x_0 \in (a,b)$ such that
> $$
> \int_a^b fg = f(x_0) \int_a^b g
> $$
> 
> > Note that if $g = 1$, we have the Integral MVT!
> 
> > [!Note]- Proof
> > 
> > By assumption, we know that $f : [a,b] \to \mathbb{R}$. Thus, by the Extreme Value Theorem, $f$ has a minimum and maximum at $x_\text{min}, x_\text{max}$ (respectively). 
> > 
> > By property of minimums and maximums, we know that $\forall x \in [a,b]$,
> > $$
> > \begin{align*}
> > f(x_\text{min}) \le &f(x) \le f(x_\text{max}) &\text{Mins and Maxes} \\
> > f(x_\text{min}) g(x) \le &f(x) g(x) \le f(x_\text{max}) g(x) &g(x) \ge 0 \\
> > \int_a^b f(x_\text{min}) g(x) \le \int_a^b &f(x) g(x) \le \int_a^b f(x_\text{max}) g(x) &\text{Monotonicity} \\
> > f(x_\text{min}) \int_a^b g(x) \le \int_a^b &f(x) g(x) \le f(x_\text{max}) \int_a^b g(x) &\text{Constants} \\
> > f(x_\text{min}) \le &\frac{\int_a^b f(x) g(x)}{\int_a^b g(x)} \le f(x_\text{max})
> > \end{align*}
> > $$
> > 
> > Since this value is bounded by the minimum and maximum of $f$,by the Intermediate Value Theorem, we know that there exists a $x_0 \in (a,b)$ such that
> > $$
> > f(x_0) = \frac{\int_a^b f(x) g(x)}{\int_a^b g(x)} \\
> > \Longrightarrow \int_a^b f(x) g(x) = f(x_0) \int_a^b g(x)
> > $$


> [!Abstract] Theorem: Continuity of Integration
> Define $F(x) = \int_a^x f(t) dt$ where $f$ is integrable. Then $F(x)$ is a continuous function, and in fact is uniformly continuous!
> 
> > [!Note]- Proof (Sketch)
> > 
> > Let $F(x) = \int_a^x f(t) dt$. Without loss of generality, say $x > y$. We have
> > $$
> > \begin{align*}
> > |F(x) - F(y)| 
> > &= \left| \int_a^x f - \int_a^y \right| = \left| \int_y^x f \right| \\
> > &\le \int_y^x |f| &\text{Property of Absolute Values} \\
> > &\le \max_{a \le x \le b} |f| \cdot (x - y)
> > \end{align*}
> > $$
> >
> > Choose $\delta = \frac{1}{\max_{a \le x \le b} |f| \cdot (x - y)}$ to obtain uniform continuity.

> [!Abstract] Theorem: Fundamental Theorem of Calculus + Chain Rule
> $$
> \frac{d}{dx} \int_{a(x)}^{b(x)} f(t) dt = f(b(x)) \frac{db}{dx} - f(a(x)) \frac{da}{dx} 
> $$
>
> > We can easily prove this by splitting our integral along a middle $c$ value, and applying the second fundamental theorem.


## Integration by Parts
> [!Abstract] Theorem: Integration by Parts
> If $f$ and $g$ are continuous on $[a,b]$, and $f'$ and $g'$ are bounded and continuous on $(a,b)$. Then
> $$
> \int f g' = f g - \int g f'
> $$
>
> Additionally,
> $$
> \int_a^b f g' = fg \bigg\vert_{x=a}^{x=b} - \int_a^b f' g
> $$
> > What we are essentially doing with integration by parts is "moving" the derivative on $g$ onto $f$!
>
> > [!Note]- Proof
> > 
> > $$
> > \begin{align*}
> >     (fg)' = fg' + gf' \\
> >     fg = \int fg' + \int gf'
> > \end{align*}
> > $$

> [!Example] Example: Integration by Parts
> $$
> \begin{align*}
>     \int x e^x 
>     &= \int x \frac{d}{dx} e^x dx \\
>     &= x e^x - \int e^x \frac{d}{dx} x dx \\
>     &= x e^x - e^x + C
> \end{align*}
> $$


> [!Abstract] Theorem: u-Substitution
> Let $f : [a,b] \to \mathbb{R}$ be continuous, $g : [c,d] \to \mathbb{R}$ be continuous, $g'$ continuous and bounded on $(c,d)$, and $\text{range}(g) \subset (a,b)$. Then,
> $$
> \int_c^d f ( g(t) ) g'(t) dt = \int_{g(c)}^{g(d)} f(u) du
> $$
>
> > [!Note]- Proof
> > 
> > Let $H(x) = \int_c^x f(g(t)) g'(t) - \int_{g(c)}^{g(x)} f(u) du$. We show it is equal to the 0 function to obtain our result.
> > 
> > First, note that $H(c) = 0$. By the second fundamental theorem of calculus,
> > $$
> > \frac{d}{dx} H(x) = f(g(x)) g'(x) - f(g(x)) g'(x) = 0
> > $$
> > And as the derivative is also 0, this forces $H(x) = 0$ for all $x$.
> > 
> > Thus, we have
> > $$
> > \int_c^x f(g(t)) g'(t) - \int_{g(c)}^{g(x)} f(u) du = 0
> > $$
> > Let $x = d$ and rearrange to get our result.
