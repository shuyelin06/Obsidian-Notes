# Section 1.1: Basic Counting
## Permutations and Combinations
A **permutation** of a set of $n$ elements is a rearrangement of the elements in a specific order. A **k-permutation** is an arrangement of $k$ elements from the $n$-element set.
> By definition of a set, elements must be distinct.

The total number of $k$-permutations of an $n$-element set is given by the formula
$$ P(n,k) = \frac{n!}{(n-k)!} = n (n-1) \dots (n - k + 1) $$

> [!Example]- Example: Basic Permutations
> **Problem**: How many ways can we seat 10 people in a row?
> **Solution**: We are performing a $k$-permutation where $k = 10$ on our set of 10 people.
> $$ P(10, 10) = 10! $$

The total ways to create a $k$-size subset from an $n$-element set, known as a **combination**, is given by 

$$ C(n,k) = \binom{n}{k} = \frac{n!}{k! (n-k)!} = \frac{P(n,k)}{k!} $$

> Note that by definition of a subset, there is no element order.

> [!Abstract] Theorem: Binomial 
> For any positive integer $n$,
> $$ (x + y)^n = \sum_{k=0}^n \binom{n}{k} x^k y^{n-k} $$
> 
> > [!Note]- Proof
> > We begin with $(x + y)^n$.
> > $$ \begin{align}
> > 	(x + y)^n &= (x + y) (x + y) \dots (x + y) \\
> > 	&= c_1 x^n + c_2 x^1 y^{n-1} + c_3 x^2 y^{n-2} + \dots 
> > 	\end{align} $$
> > The product of the $n$ terms means that when we expand the binomial expression, we are "choosing" either the $x$ or $y$ term to multiply.
> > 
> > Thus, to find the coefficient of $x^k y^{n-k}$, the product of the $n$ terms requires that when we multiply each binomial together, we multiply ("choose") the $x$-term $k$ times. After this, the rest of the product's terms are forced to be $y$ (and there's only one way to pick $y$). 
> > 
> > This gives us $C(n, k)$ different ways to obtain the coefficient.
> > $$ C(n,k) x^k y^{n-k} = \binom{n}{k} x^k y^{n-k} $$

> [!Example]- Example: Basic Counting
> There are 10 cows, 9 pigs, 8 horses. The
> 1. Total ways to pick 5 animals at once:
>    
>    Because order does not matter, we are simply choosing 5 animals from our total of 27. 
>    $$ C(27, 5) $$
>    
> 2. Total ways to get 5 animals where we get 3 cows, 2 pigs or 2 cows, 3 pigs:
>    
>    We choose 3 cows and 2 pigs from our animal total to obtain
>    $$ \binom{10}{3} \binom{9}{2} $$
>    We choose 2 cows and 3 pigs from our animal total to obtain
>    $$ \binom{10}{2} \binom{9}{3} $$
>    Because these two groups of outcomes are distinct from one another, we add them together to find our total.
>    $$ \binom{10}{3} \binom{9}{2} + \binom{10}{2} \binom{9}{3} $$

> [!Example]- Example: Basic Counting (2)
> There are 10 kids and 3 types of candy. How many ways can we distribute this candy such that exactly 3 children get type 1, 2 children get type 2, and 5 children get type 3?
> 
> We can think of our children as the distinct elements, and choose who gets what candy. So, we first select 3 children to get type 1, 2 children to get type 2, and 5 children to get type 3.
> $$ \binom{10}{3} \binom{7}{2} \binom{5}{5} $$
> 
> We can think about this another way as well. Say we have 10 children numbered 1-10, and we assign each a candy type of 1, 2, or 3 (for the total we're looking for). We want to find the number of different ways we can order these candy types!
> However, because there are repeated elements, we need to count some cases as one. We do this by dividing by the total number of possible cases that we want to count as one case. 
> $$ \frac{P(10, 10)}{3! \cdot 2! \cdot 3!} $$
> In fact, this is called the **multinomial coefficient**, described below.

> [!Abstract] Theorem: Multinomial Coefficient (Permutations with Repetition)
> Suppose there are $k$ distinct objects, and object $i$ occurs $a_i$ times.
> 
> Assume $a_1 + a_2 + \dots + a_k = n$. 
> 
> Then, the total number of rearrangements of the $n$ objects is
> $$ \frac{n!}{a_1! \cdot a_2! \cdots a_k!} = \binom{n}{a_1 a_2 \dots a_k} $$
> called the **multinomial coefficient**. 

We can use the multinomial coefficient to generalize our previous binomial theorem.

> [!Abstract] Theorem: Multinomial
> $$ (x_1 + x_2 + \dots + x_k)^n = \sum_{a_1 + a_2 + \dots + a_k = n} \binom{n}{a_1 a_2 \dots a_k} x_1^{a_1} x_2^{a_2} \dots x_k^{a_k} $$

> [!Example]- Example: Multinomial Coefficient
> Find the coefficient of $x_1^3 x_2 x_4^2$ in $(x_1 + x_2 + x_3 + x_4)^6$.
> 
> To find the coefficient, we need to find the number of times we obtain $x_1^3 x_2 x_4^2$ in the product.
> 
> In other words, if we select 6 positions, where each represents the $x_i$ term we "selected" to multiply out, then we want to choose 3 positions to have $x_1$, 1 position to have $x_2$, and 2 positions to have $x_4$. 
> 
> This comes out to be
> $$ C(6, 3) * C(3, 1) * C(2,2) = \binom{6}{3 \quad 1 \quad 2} $$

> [!Example]- Example: Permutations and Combinations
> How many arrangements of $AAABBCC$ are there?
> 
> Suppose we have 7 positions. We want to choose 3 to fill with $A$, 2 to fill with $B$, and 2 to fill with $C$. This comes out to be
> $$ C(7,3) * C(4,2) * C(2,2) $$
> 
> --- 
> 
> What if the $B$'s must all be together, but none of the $C$'s can be together?
> 
> If the $B$'s must be together, we block them together as one term $X = BB$ to find arrangements of $AAAXCC$. Then, to find permutations where the $C$'s are not together, we first will find the number of arrangements of $AAAX$ (without the $C$'s').
> $$ C(4,3) $$
> Then, between every term $AAAX$, we can place $C$'s such that they are not next to each other. This comes out to 5 positions, and we have 2 $C$'s to place to give us
> $$ C(5,2) $$
> different ways to place our $C$'s. Thus, our final result is
> $$ C(4,3) * C(5,2) $$


# Section 2.1: Axioms of Probability
We define the set of all possible outcomes of an experiment as the **sample space** $S$. A subset of this sample space $S$ is called an **event**. 
> The **null event**, denoted $\varnothing$, is the set with no elements.

For $A,B \subseteq S$, the **union** and **intersection** of the two sets is defined as
$$ A \cup B = \{ x : x \in A \lor x \in B \} $$
$$ A \cap B = \{ x : x \in A \land x \in B \} $$
We say sets $A$ and $B$ are **disjoint (mutually exclusive)** if $A \cap B = \varnothing$.

The **complement** of $A$ is defined as
$$ \bar{A} = A^c = \{ x : x \not\in A \}$$

> [!Example]- Example: Sets
> Let $S = [6] = \{ 1,2,3,4,5,6 \}$. 
> 
> If $A = \{ 1,3 \}$ and $B = \{ 1, 2 \}$, then
> $$ A^c \cap B^c = \{ 2,4,5,6 \} \cap \{ 3,4,5,6 \} = \{ 4,5,6 \} $$

> [!Abstract] Theorem: De Morgan's Law
> For $A_1, A_2 \dots A_n \subseteq S$,
> 1. $$ \left( \bigcap_{i=1}^n A_i \right)^c = \bigcup_{i=1}^n A_i^c $$
> 2. $$ \left( \bigcup_{i=1}^n A_i \right)^c = \bigcap_{i=1}^n A_i^c $$

Let $F$ be a family of subsets of $S$ (a subset of the power-set of $S$).

We say $F$ is a **$\sigma$-algebra on a set $S$** if
1. $S \in F$
2. **Closed Under Complements**: If $A \in F$, then $A^c \in F$
3. **Closed Under Union**: If $A_1, \dots, A_n \in F$, then $\bigcup_{i = 1}^n A_i \in F$

> By (2) and (3) and De Morgan's Law, it must be true that we have **closure under intersection** as well.

> [!Example]- Example: $\sigma$-Algebra
> Let $S = [6]$. Then
> $$ F = \{ \varnothing, S, \{1,2,3\}, \{4,5,6\} \}$$
> is a $\sigma$-algebra on $S$. 
> 
> Let $S = [5]$. Then
> $$ f = \{ \varnothing, S, \{1,2\}, \{3,4\}, \{5\} \}$$
> is not a $\sigma$-algebra, as the complement of the subset $\{ 1,2 \}$ does not exist in $F$.

A **probability function** $P: F \to \mathbb{R}$ is a function satisfying the following **axioms of probability**:
1. $P(A) \in [0, 1]$ for all $A \in F$ 
   *Probability must be given as a number between 0 and 1*
2. $P(S) = 1$
   *The probability of the set of all outcomes must be 1*
3. If $A_1, A_2, \dots$ are pairwise disjoint, then 
   $$ P \left( \bigcup_{i \ge 1} A_i \right) = \sum_{i \ge i} P(A_i) $$
   *The probability of the union of pairwise disjoint events is equal to the summation of their individual probabilities*

> [!Example]- Example: Axioms of Probability
> You flip a two-sided coin, and the probability of heads $H$ is $\frac{1}{2}$. How can we use the axioms of probability to justify the probability of $T$?
> 
> Here, we know that the set of all outcomes $S = \{ H, T \}$, so the $\sigma-algebra$ of $S$ is
> $$ F = \{ \varnothing, S, \{H\}, \{T\} \} $$
> We know by the axioms that $P(S) = 1$, so 
> $$ \begin{align} 
> 	&P(S) = 1 \\
> 	\to &P( \{ H, T \} ) = 1 \\
> 	\to &P( \{H\} \cup \{T\} ) = 1 \\
> 	\to &P(\{H\}) + P(\{T\}) = \frac{1}{2} + P(\{T\}) \\
> 	\to &P(\{T\}) = \frac{1}{2}
> 	\end{align} $$

Additionally, we have the following **properties of probability**, which can be derived using the axioms of probability. Let $A, B$ be events of sample space $S$. Then,
1. $P(A^c) = 1 - P(A)$
2. $P(\varnothing) = 0$
3. $P(A \cup B) = P(A) + P(B) - P(A \cap B)$
4. If $A \subseteq B$, then $P(A) \le P(B)$

> Note that the third property can be extended for more sets. For example, for 3 sets, we have
> $$ P(A \cup B \cup C) = P(A) + P(B) + P(C) - P(A \cap B) - P(A \cap B) - P(B \cap C) + P(A \cap B \cap C) $$

> [!Example]- Example: Proof (Property 2)
> We know that
> $$ \varnothing = \varnothing \cup \varnothing $$
> and moreover, the empty set is pairwise disjoint with itself.
> 
> Thus, it must be true that
> $$ P(\varnothing) = P(\varnothing \cup \varnothing) = P(\varnothing) + P(\varnothing) = 2 P(\varnothing) $$
> Thus, $P(\varnothing) = 2P(\varnothing)$, which is only possible if $P(\varnothing) = 0$. 

> [!Example]- Example: Proof (Property 3)
> Let $A / B$ denote the set of elements in $A$, but not in $B$. Then,
> $$ P(A \cup B) = P(A/B \cup (A \cap B) \cup B/A) $$
> Because these sets are mutually exclusive, we can apply the third axiom
> $$ P(A/B \cup (A \cap B) \cup B/A) = P(A/B) + P(A \cap B) + P(B/A) $$
> Adding $P(A \cap B) - P(A \cap B) = 0$ to both sides, we obtain
> $$ = P(A/B) + 2 P(A \cap B) - P(A \cap B) + P(B/A) $$
> Which, after applying axiom 3, gives us
> $$ \begin{align}
> 	&= P(A / B \cup (A \cap B)) + P(B / A \cup (A \cap B) - P(A \cap B) \\
> 	&= P(A) + P(B) - P(A \cap B)
> 	\end{align} $$

> [!Abstract] Theorem: Inclusion-Exclusion
> If $A_1, \dots, A_n \subseteq S$, then 
> $$ P \left( \bigcup_{i = 1}^n A_i \right) = \sum_{i = 1}^n P(A_i) - \sum_{i < j} P(A_i \cap A_j) + \sum_{i < j < k} P(A_i \cap A_j \cap A_k) + (-1)^{n-1} P \left( \bigcap_{i = 1}^n A_i \right) $$
> 
> > [!Note]- Alternative Definition
> > We can think about this another way. 
> > Let $I \subseteq [n] = \{ 1,2 \dots, n \}$. Denote $A_I = \bigcap_{i \in I} A_i$, with $A_\varnothing = S$.
> > 
> > Then $P \left( \bigcup_{i = 1}^n A_i \right) = 1 - \sum_{I \subseteq [n]} (-1)^{|I|} P(A_I)$ where $I \subseteq [n]$ is the power set of $[n]$, and $| I |$ is the magnitude of $I$.
> > 
> > For example, when $n = 2$, we have $I = \varnothing, \{1\}, \{2\}, \{1,2\}$, giving us
> > $$ \begin{align}
> > 	&1 - \sum_{I \subseteq [n]} (-1)^{|I|} P(A_I) \\
> > 	&= 1 - \left( P(A_\varnothing) -P(A_{\{1\}}) - P(A_{\{2\}}) + P(A_{\{1,2\}}) \right) \\
> > 	&= P(A_1) + P(A_2) - P(A_1 \cap A_2)
> > 	\end{align} $$
> > 
> > By Demorgan's Law, this becomes
> > $$ P\left( \bigcap_{i=1}^n A^c \right) = \sum_{I \subseteq [n]} (-1)^{|I|} P(A_I) $$
> > Which is the definition often used in combinatorics.

> [!Example]- Example: Inclusion-Exclusion Theorem
> A person visits the dentist. There is a 0.7 chance a cavity is filled, 0.2 a tooth is extracted, and 0.1 change that both occur.
> What is the probability in a visit that neither occur?
> 
> If $A$ is the event of a cavity, and $B$ is the event of an extraction, then
> $$ \begin{align}
> 	&P(\text{Neither Occur}) = P( (A \cup B)^c ) \\
> 	&= 1 - P(A \cup B) \\
> 	&= 1 - (P(A) + P(B) - P(A \cap B)) \\
> 	&= 1 - (0.7 + 0.2 - 0.1) = 0.2
> 	\end{align}  $$ 

We often focus on the case the sample space $S$ is finite. In the case every element has equal chance, we have for any event $E \subseteq S$,
$$ P(E) = \frac{|E|}{|S|} $$
or in other words, the probability of the event is equal to all ways the event can occur, divided by the total number of outcomes.

> [!Example]- Example: Calculating Probability (1)
> A coin is flipped 10 times. What is the probability of getting exactly 3 heads? 
> 
> To find the number of outcomes where we have 3 heads, choose 3 "coins" to be heads.
> $$ C(10, 3) $$
> Furthermore, as every position can either be heads or tails, our total number of outcomes is equal to 
> $$ 2^{10} $$
> Giving us probability
> $$ P = \frac{C(10,3)}{2^{10}} $$

> [!Example]- Example: Calculating Probability (2)
> There are 10 cats, 7 dogs, and 5 mice. Four animals are chosen at once. What is the probability we get at most 1 mouse?
> 
> Let's count the cases where we have either 0 or 1 mice. 
> 1. For 0 mice, we choose 4 animals from our remaining  17 available $\to C(17, 4)$.
> 2. For 1 mouse, we choose 3 animals from our remaining 17 available $\to C(17, 3)$.
> 
> Adding these cases together, we have number of outcomes
> $$ C(17,4) + C(17,3) $$
> 
> Out of our 22 animals, we choose 4 of them. This gives us total number of outcomes
> $$ C(22, 4) $$
> 
> Combining these results, we get probability
> $$ P = \frac{C(17,4) + C(17,3)}{C(22,4)}$$

> [!Example]- Example: Calculating Probability (3)
> If $n$ labeled balls are placed in $n$ labeled boxes, what is the probability that exactly 1 box is empty?
> 
> If one box must be empty and the others with balls, there must be **exactly 1 box with 2 balls**, the others having 1 ball. 
> 
> To find the number of outcomes where exactly 1 box is empty, we first choose one of $n$ boxes to be empty. Then, we choose another box from our remaining $(n-1)$ boxes to place a distinct pair of balls $C(n, 2)$. Finally, we permute the remaining $n - 2$ balls in the other boxes.
> $$ n \cdot (n - 1) \cdot C(n, 2) \cdot P(n-2, n-2) = \binom{n}{2} \cdot n! $$
> 
> To find the total number of outcomes, we observe that every ball has a choice to be in $n$ boxes, so we have total number of outcomes
> $$ n^n $$
> 
> Giving us probability 
> $$ P = \frac{C(n,2) \cdot n! }{n^n}$$

In some cases $S$ may be uncountable, but we can still find the probability. 

> [!Example]- Example: Calculating Probability - Uncountable Set (3)
> As an extremely simple example, let $S = [0, 1]$. While we may not be able to find the probability of one specific number (say, $0.1111$), we can easily find the probability of a range of numbers.
> 
> Let $E = [a,b] \subseteq [0,1]$. Then,
> $$ P(E) = \frac{b-a}{1-0} $$ 

> [!Abstract] Theorem: Probability with Uncountable Sets 
> Let $A_1 \subseteq A_2 \subseteq A_3 \subseteq \dots A_n$ be events in $S$. Then
> 1. $$ P\left(\bigcup_{i=1}^\infty A_i\right) = \lim_{n\to\infty} P(A_n) $$
> 2. $$ P\left(\bigcap_{i=1}^\infty A_i\right) = \lim_{n\to\infty} P(A_1) $$
>    
> > [!Note]- Proof
> > Let $B_1 = A_1, B_2 = A_2 / A_1, \dots B_i = A_i / A_i$, where $X/Y$ indicates the set of elements in $X$ not in $Y$.
> > 
> > These are disjoint sets whose union form $A$. In other words,
> > $$ P\left( \bigcup_{i=1}^\infty A_i \right) = P\left( \bigcup_{i=1}^\infty B_i \right) $$
> > Applying the axioms of probability, 
> > $$ P\left( \bigcup_{i=1}^\infty B_i \right) = \sum_{i=1}^\infty P(B_i) $$
> > Finally, we can convert the summation to a limit and convert back in terms of $A$.
> > $$ \sum_{i=1}^\infty P(B_i) = \lim_{n\to\infty} \sum_{i=1}^n P(B_i) = \lim_{n\to\infty} P\left( \bigcup_{i=1}^n B_i \right) = \lim_{n\to\infty} P(A_n) $$

> [!Example]- Example: Probability with Uncountable Sets (1)
> 1. At 11:59, balls labeled 1 to 10 are put into a box. One ball is removed at 11:59:30.
> 2. At 11:59:30, balls labeled 11 to 20 are put into the box. One ball is removed at 11:59:45.
> 3. At 11:59:45, balls labeled 21 to 30 are put into the box...
> 
> At 12:00, how many balls are in the box?
> 
> Let $A_i$ denote the event in which ball $1$ survives step $i$. Then,
> $$ P(A_1) = \frac{9}{10} \qquad P(A_2) = \frac{9}{10} \cdot \frac{18}{19} \qquad P(A_3) = \frac{9}{10} \cdot \frac{18}{19} \cdot \frac{27}{28} \dots $$
> Combining these, we have
> $$ A = \bigcap_{i=1}^\infty A_i $$
> as the event in which ball 1 survives till 12:00. Because $A_1 \subseteq A_2 \subseteq A_3 \subseteq \dots$, we apply our previous theorem to find
> $$ P(A) = P \left( \bigcap_{i=1}^\infty A_i  \right) = \lim_{n\to\infty} A_n = \lim_{n\to\infty} \frac{9}{10} \cdot \frac{18}{19} \dots \frac{9n}{9n + 1} = 0 $$
> Let $c_n = \prod_{i=1}^\infty \frac{a_n}{a_n + 1} = \lim_{n\to\infty} c_n$. Then,
> $$ \frac{1}{c_n} = \frac{10}{9} \cdot \frac{19}{18} \dots \frac{9_{n+1}}{9_n} = (1 + \frac{1}{9}) (1 + \frac{1}{2(9)}) \dots (1 + \frac{1}{9n}) $$
> Which is bounded by the harmonic set!
> $$ \frac{1}{c_n} \ge \frac{1}{9} (1 + \frac{1}{2} + \frac{1}{3} + \dots + \frac{1}{n}) $$
> So,as $n \to \infty$, 
> $$ \lim \frac{1}{c_n} = \infty $$
> forcing $P(A) = \lim_{n\to\infty} c_n = 0$.
>
> Now let $B_k$ be the event where ball $k$ survives till 12:00. If we wo0rk for any ball, we can see that we're dropping terms from the harmonic set, which still diverges. This holds for any ball, so if $B$ is the event that at least 1 ball survives, then
> $$ P(B) = P \left( \bigcup_{i=1}^\infty B_i \right) = \sum_{i=1}^\infty P(B_i) = 0 $$
> Thus, at 12:00, no balls would remain in the box!


# Section 3.1: Introduction to Conditional Probability
Let $A,B \subseteq S$, where $P(B) \ne 0$.

The **conditional probability** of $A$ given $B$ ("probability of $A$ given $B$) is given as
$$ P(A \mid B) = \frac{P(A \cap B)}{P(B)} $$
> This essentially has the effect of restricting our sample space.

Properties of conditional probability are given as follows:
1. $0 \le P(A \mid B) \le 1$
2. $P(S \mid B) = 1$
3. If $A_1, A_2, \dots$ are pairwise disjoint, then
   $$ P\left( \bigcup_{i=1}^\infty A_i \mid B \right) = \sum_{i=1}^\infty P(A_i \mid B) $$

> [!Example]- Example: Proof (Property 3)
> $$ P\left( \bigcup_{i=1}^\infty A \mid B \right) = \frac{P\left( (\bigcup_{i=1}^\infty A_i) \cap B \right)}{P(B)} $$
> By definition of conditional probability. Then, we apply the distributive property to obtain
> $$ = \frac{P(\cup (A_i \cap B)}{P(B)} $$
> Because the $A_i$'s by assumption are disjoint, then it must be true that the $A_i \cap B$'s are also disjoint. Applying our probability axiom,
> $$ = \sum_{i=1}^\infty \frac{P(A_i \cap B)}{P(B)} = \sum_{i=1}^\infty P(A_i \mid B) $$


> [!Example] Example: Conditional Probability (1)
> A loaded 6-sided die has an odd number occurring twice as likely as even. Determine the number is a perfect square, given the value is larger than 3.
>
> Let $A = \{ 1, 4 \}$ denote the event of a perfect square, and let $B = \{ 4, 5, 6 \}$ denote the event of a number larger than 3.
> We can easily see that $A \cap B = \{ 4 \}$.
>
> Let $x$ be the probability that we roll an even number.
> $$ 2x + x + 2x + x + 2x + x = 1 \to x = 1/9 $$
> Thus, the probability of rolling an even number is $1/9$, and an odd number $2/9$.
>
> We now find our answer as
> $$ P(A \mid B) = \frac{P(A \cap B)}{P(B)} = \frac{P(\{4\})}{P(\{4,5,6\})} = \frac{1/9}{4/9} = \frac{1}{4} $$


> [!Example]- Conditional Probability (2)
>
> There are 7 black socks, 5 white socks. The socks are distinct, and we take 2, one at a time, without replacement.
>
> What is the probability that both socks are black?
>
> This question is a conditional probability question in disguise, asking for the probability of a black sock given the first is black as well.
>
> Let $A_1$ denote the event that the first sock is black, and $A_2$ denote the event that the second sock is black.
> We want $P(A_1 \cap A_2)$, which is actually equivalent to $P(A_1) P(A_2 \mid A_1)$.
> $$ P(A_1 \cap A_2) = P(A_1) P(A_2 \mid A_2) = \frac{7}{12} \cdot \frac{6}{11} $$

Let $A_1, \dots, A_2 \subseteq S$, where $P(A_1 \cap A_2 \dots A_n) > 0$ Then,
$$ P(A_1 \cap A_2 \dots A_n) = P(A_1) P(A_2 \mid A_1) P(A_3 \mid A_1 \cap A_2) \dots $$
This is known as the **multiplication rule**.