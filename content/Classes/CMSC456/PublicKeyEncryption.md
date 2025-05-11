---
title: Public Key Encryption
tags:
- cmsc456
---

# Number Theory
## Groups
A **group** is a set $G$ along with a binary operation $\circ$ for which the following conditions hold:
- **Closure**: For all $g,h \in G$, $g \circ h \in G$.
- **Identity**: There exists an identity $e \in G$ such that $\forall g \in G$, $e \circ g = g = g \circ e$.
- **Inverse**: For all $g \in G$, there exists an element $h \in G$ called the **inverse** such that $g \circ h = e = h \circ g$. 
- **Associativity**: For all $g_1, g_2, g_3 \in G$,
  $$
  g_1 \circ (g_2 \circ g_3) = (g_1 \circ g_2) \circ g_3
  $$

> When $G$ has a finite number of elements, we say $G$ is **finite** and let $|G|$ denote the order (size) of the group.

We say a group $G$ with operation $\circ$ is **abelian** if it has the property of **commutativity**: $\forall g,h \in G, g \circ h = h \circ g$. 
> For the purposes of this class, we will only deal with finite, abelian groups.

> [!Example]- Example Group: Modular Arithmetic (Addition)
> We say that two numbers $a,b$ are **congruent modulo $p$**, denoted
> $$
> a \equiv b \mod p
> $$
> 
> If $p$ divides $(a - b)$, or in other words, $p \vert (a - b)$.
> > For example, all of the following are true.
> > $$
> > 2 \equiv 15 \mod 13 \qquad 
> > 28 \equiv 15 \mod 13 \qquad
> > -11 \equiv 15 \mod 13
> > $$
> 
> Addition works in modular space as normal. You perform regular addition, and then take modulo $p$. For example,
> $$
> 8 + 10 \mod 13 \equiv 18 \mod 13 \equiv 5 \mod 13
> $$
> 
> Addition has the following properties. Consider the set of numbers $\mathbb{Z}_p = \{0,1,\dots p-1\}$:
> - **Identity**: $\forall a \in \mathbb{Z}_p$, adding 0 to it yields the same number
> - **Additive Inverse**: $\forall a \in \mathbb{Z}_p$, $\exists b$ such that $a + b \mod p = 0$, given as $b = p - a$.
> - **Closure**: Any addition operations will yield a result that is still inside of $\mathbb{Z}_p$.
> - **Associativity**: You can take modulo at any point in the operation. For example,
>   $$
>   ((a + b) \mod p + c) \mod p = (a + (b + c) \mod p) \mod p
>   $$
> 
> The set $\mathbb{Z}_p$ with our addition modulo operator defines a group!

## Modular Arithmetic under Multiplication, Prime
In the context of cryptography, we are interested in **multiplicative** groups over the integers, as this introduces computational problems believed to be hard to solve. One example of this is the **multiplication modulo $p$ group**. 
> For now, we will only consider prime groups, but we will later generalize to composite groups.

Let $Z^*_p = \{1, \dots p - 1\}$, with the multiplication mod operation. For $Z^*_p$ to be a group it must be true that **p is prime**. Without a prime $p$, we won't have a multiplicative inverse!

### Multiplicative Inverses
We argue below that $Z^*_p$ satisfies the inverse property (the rest are trivial to prove). In other words, $\forall a \in Z^*_p$, there exists a $b$ such that $a * b \mod p = 1 \mod p$. 

> [!Example]+ Example: Brute Force Inverse
> Suppose we want to find the multiplicative inverse of $9 \mod 11$.
>
> One way to do this is to brute-force iteratively try all 10 numbers in $Z^*_{11}$ to find our inverse. We will consider this brute-force to be exponential time! This is because when we're using this with respect to binary numbers, the length of our input is on the magnitude of $2^n$. 

However, there's a faster way to find the multiplicative inverse, through the **Euclidean Algorithm**! This algorithm is based off the following assertion:

> [!Abstract] Theorem: Euclidean Algorithm
> Let $a, p$ be positive integers. Then, there exists integers $X,Y$ such that $Xa + Yp = gcd (a,p)$. 
>
> The Euclidean algorithm can be used to compute $gcd (a,p)$ in polynomial time. We can then extend this to compute $X,Y$ in polynomial time.
> > This algorithm has time complexity $2 \log (b)$, for $gcd (a,b)$. 

If we can use the Euclidean Algorithm to find $X,Y$, then we can find a multiplicative inverse. This is because for $p$ prime, $gcd(a,p) = 1$, so for
$$
Xa + Yp = gcd(a,p) = 1
$$
We can rearrange our terms to find that $Yp = (1 - Xa)$, telling us that $p$ divides $(1 - Xa)$. Because of this, we know that 
$$
Xa \mod p \equiv 1
$$
In other words, **$X$ is our multiplicative inverse for $a$**!

> [!Example]+ Example: Inverses with the Euclidean Algorithm
> Suppose we want to find the multiplicative inverse of $a = 9$ for $p = 23$. In other words, we want to find
> $$
> 9X + 23Y = gcd(9,23) = 1
> $$
> We can do this by iteratively dividing as follows. Let $b = 23, a = 9$. Every iteration, modular divide $b$ by $a$, to get
> $$
> b = k * a + c
> $$
> Then, let $b = a, a = c$ and repeat.
> 
> $$
> \begin{align*}
> 23 = 2 * 9 + 5 \\
> 9 = 1 * 5 + 4 \\
> 5 = 1 * 4 + 1 \\
> 4 = 4 * 1 + 0
> \end{align*}
> $$
> Once we find a 0 for $c$, we can work our way back up to find our inverse. If we rearrange every expression (ignoring the last) to be in terms of $c$, we'll find that
> $$
> \begin{align*}
> 23 = 2 * 9 + 5 \Longrightarrow 5 = 23 - 2 * 9 \\
> 9 = 1 * 5 + 4 \Longrightarrow 4 = 9 - 1 * 5 \\
> 5 = 1 * 4 + 1 \Longrightarrow 1 = 5 - 1 * 4 \\
> \end{align*}
> $$
> So, starting from the bottom, we can plug each equation back into the previous to get an expression in terms of 5, 23. 
> $$
> \begin{align*}
> 1 = 5 - 1 * 4 \\
> 1 = 5 - 1 * (9 - 1 * 5) \\
> 1 = (23 - 2 * 9) - 1 * (9 - 1 * (23 - 2 * 9)) \\
> 1 = 2 * 23 - 5 * 9
> \end{align*}
> $$
> 
> Thus, we find our multiplicative inverse as $-5$.

> [!Info] Polynomial Time of Multiplicative Inverses
> Note that when we use the Euclidean Algorithm, our "b" value is being halved every two rounds. So, our time complexity is $2 \log (b)$. This means our time complexity is polynomial given the input!
> 
> Thus, we can not only find multiplicative inverses, **but find them efficiently**.

### Modular Exponentiation
What about **Modular Exponentiation**? Given $a, m, N$, can we efficiently compute $a^m \mod N$?
> This is the result of multiplying $a$ by itself $m$ times, and taking the modulus of the result.

One way we could compute this is as follows:
```python
def ModExp(a, m, N):
    temp = 1
    for i in range(1, m + 1)
        temp = temp * a % N
    return temp
```
But this has runtime $O(m)$, where $m$ could be exponential! For an efficient algorithm, we need our runtime to be on the logarithmic order.

We can, in fact, achieve an efficient algorithm with repreated squaring. Let $m = m_{n-1} m_{n_2} \dots m_1 m_0$ be the bits of $m$.
```python
def ModExp(a, m, N):
    s = a
    temp = 1
    for i in range(0, n):
        if (mi == 1)
            temp = temp * s % N
        s = s^2 % N
    return temp
```
This has runtime $O(\log_2(m))$! So, **we can also perform Modular Exponentiation efficiently**. 

In the context of a prime $p$, we can also use **Fermat's Little Theorem** to speed up our computation. 

> [!Abstract] Theorem: Fermat's Little Theorem
> For prime $p$, integer $a$, $a^p \equiv a \mod p$. 
>
> > [!Info] Corollary
> > 
> > For prime $p$ and $a$ such that $gcd(a,p) = 1$, $a^{p-1} \equiv 1 \mod p$.

This theorem can be generalized to any finite group!

> [!Abstract] Theorem: Generalized Fermat's
> Let $G$ be a finite group with $m = |G|$. Then, for any element $g \in G$, appling the group operation to it $m$ times will yield 1. 
> $$
> g^m = 1
> $$
> > Recall that for our group $\mathbb{Z}^*_p$, we have $m = p - 1$ elements. So, this is making the same assertion as our previous corollary. 

## Modular Arithmetic under Multiplication, N Composite
Using primes to construct groups is very limiting, as there are only so many primes we could use. What about multiplicative groups modulo $N$, where $N$ is composite? Can we create such groups? 

For numbers $\{1, \dots, N - 1\}$, only numbers $a$ such that $gcd(a,N) = 1$ have a multiplicative inverse by the Extended Euclidean Algorithm. Because all of the others do not have a multiplicative inverse, to obtain a valid group, **we must disclude these values from our group.**

So, we will define our group $\mathbb{Z}^*_N$ as follows:
$$
Z^*_N = \{a \in \{1, \dots N-1\} : gcd(a,N) = 1\}
$$
Then, $Z^*_N$ is an abelian, multiplicative group.

In practice, we will often create composite groups where $N = p \cdot q$, for distinct primes $p, q$. We can create this group as follows:
1. For $p$, remove numbers $1p, 2p, 3p, 4p \dots q * p$
2. For $q$, remove numbers $1q, 2q, 3q, 4q, \dots q * p$.

This gives us order, denoted $\phi(N)$ (the **Euler totient function**)
$$
\phi(N) = N - p - q + 1 = (p - 1) (q - 1)
$$
> We add 1 as we're double counting the $q * p$ element in our removal.

Generalizing this, for $N = \prod_i  p_i^{e_i}$, where $\{p_i\}$ are distinct primes and $e_i \ge 1$, then 
$$
\phi(N) = \prod_i p_i^{e_i - 1} (p_i - 1)
$$
This gives us a very easy way to create large groups quickly! We take prime factors, and multiply them together to get a large group!
> However, finding this prime factorization of $N$ is a very difficult problem! 

By this theorem, and using the previous theorems, we know that for any $a$ such that $gcd(a,N) = 1$,
$$
a^{\phi(N)} \equiv 1 \mod N
$$
This can be used as a "quick / easy" vertification that someone has found $\phi(N)$!
> A corollary of this theorem is that $g^x = g^{x \mod \phi(N)}$ (since every $\phi(N)$, we wrap around). This makes things easy if we can find the prime factorization of $N$. 

## Cyclic Groups
For a finite group $G$ of order $m$ and $g \in G$, consider
$$
\langle g \rangle = \{g^0, g^1, \dots g^{m-1} \}
$$
Here, $\langle g \rangle$ **always forms a cyclic subgroup of $G$**. However, as there may be repeats, $\langle g \rangle$ may be a subgroup with a smaller order than $m$.

If the order of $\langle g \rangle$ is equal to $G$, we say that $G$ is a **cyclic group** and $g$ is a **generator** of $G$. In other words, by apply modular exponentiation on $g$, we can cycle between all values in $G$.

> [!Example]+ Example: Cyclic Group + Generator
> Define $Z^*_{13}$. Then, 2 is a generator of $Z^*_{13}$.
> 
> | Input | Output | | Input | Output |
> | :-: | :-: | - | :-: | :-: |
> | $2^0$ | 1 | | $2^6$ | 12 | 
> | $2^1$ | 2 | | $2^7$ | 11 | 
> | $2^2$ | 4 | | $2^8$ | 9 |
> | $2^3$ | 8 | | $2^9$ | 5 | 
> | $2^4$ | 3 | | $2^{10}$ | 10 | 
> | $2^5$ | 6 | | $2^{11}$ | 7 |
> | $2^{12}$ | 1 |
> 

Let $G$ be a finite group and $g \in G$. The **order** of $g$ is the smallest positive integer $i$ such that $g^i = 1$.

> [!Abstract] Proposition: Generators
> 1. Let $G$ be a finite group, $g \in G$ with order $i$. Then, for any integer $x$, we have $g^x = g^{x \mod i}$.
> 2. Let $G$ be a finite group and $g \in G$ with order $i$. Then, $g^x = g^y$ if and only if $x \equiv y \mod i$.
> 3. Let $G$ be a finite group of order $m$, and $g \in G$ with order $i$. Then, $i | m$.

Proposition (3) is particularly important! This is because if $m$ is prime, then the only generator orders we can get are 1 and $p$! Furthermore, because $i = 1$ is only possible with the identity element, this means all other elements are generators of $G$. 

**We want to find these prime order groups, as they give us a basis for cryptographic problems**.

> [!Abstract] Theorem
> If $p$ is prime, then $Z^*_p$ is a **cyclic group of order** $p - 1$. 

Using the above theorem, we can construct a subgroup of $Z^*_p$ that is of prime order! 

> [!Note] Prime Order Cyclic Groups
> Let $Z^*_p$, where $p$ is a strong prime: $p = 2q + 1$, where $q$ is also prime. By the above theorem, $Z^*_p$ is a cyclic group of order $p - 1 = 2q$. 
> > We will cleverly take 1/2 of the elements of $Z^*_p$, to get a group of order $q$, which is prime!
>
> Because $Z^*_p$ is cyclic, it has a generator $g$. Choose this generator. 
>
> By definition of a generator, we can get every element in this group using it! So, let's take every even power of $g$, giving us a subgroup of order $q$. This gives us a prime order group!
> > We take even powers, as even if you raise even powers to an exponent, you will still have an even power!

# Cryptographic Problems on Cyclic Groups
Cyclic groups form the basis of many cryptographic problems. In particular, there are 3 main problems on cyclic groups, each building on the last.

## Discrete Logarithm
We define the **Discrete-Log Experiment** $DLog_{A,G} (n)$ as follows:
1. Run $G(1^n)$ to get $(G,q,g)$, where $G$ is a cyclic group of order $q$, and generator $g$.
2. Choose a $h \in G$ uniformly.
3. Adversary $A$ is given $G,q,g,h$, and needs to guess the $x \in Z_q$ such that $g^x = h$.
4. The output of the experient is 1 if $g^x = h$ and 0 otherwise.

> As $q$ is typically on the magnitude of $2^{2048}$ or $2^{1024}$, it would be extremely inefficient to do a brute force attack. 

We say the **Discrete-Logarithm Problem** is hard relative to $G$ if for all PPT algorithms $A$, there exists a negligible function such that
$$
Pr[Dlog_{A,G} (n) = 1] \le negl(n)
$$

This is the hardest problem on cyclic groups! All of the following problems are based off of this. 

## Computational Diffie-Hellman
We define the **Computational Diffie-Hellman (CDH)** problem as follows. 

*Given $(G,q,g)$ and uniform $h_1 = g^{x_1}$, $h_2 = g^{x_2}$, compute $g^{x_1 \cdot x_2}$.*
> Note that $h_1 \cdot h_2 = g^{x_1 + x_2}$, which won't solve our problem.

This problem is based on the Discrete Logarithm problem, as if we could solve Discrete Log, we could solve for $x_1, x_2$ in PPT time and compute our result. 

However, because Discrete Log is a hard problem, this is also hard. 

## Decisional Diffie-Hellman
We define the **Decisional Diffie-Hellman (DDH)** problem as follows.
1. Define a distinguisher $D$, who gets one the group $G$, order $q$, generator $g$, and one of the following:
   - **Ideal World**: $g^x, g^y, g^z$, 3 independent group elements with no correlation to each other.
   - **Real World**: $g^x, g^y, g^{xy}$, 3 group elements where the 3rd is related to the first two through the CDH problem.
2. The distinguisher gets one of the worlds, and has to guess the world that they're in.

We say that the DDH problem is hard if for all PPT adversaries $A$, they can only guess what world they're in with a negligible probability.
$$
| Pr[D(G,q,g,g^x,g^y,g^z) = 1] - Pr[D(G,q,g,g^x,g^y,g^{xy}) = 1] | \le negl
$$

Note that DDH is **not hard** over $Z^*_p$ for for prime $p$. This is because for $a \in Z^*_p$, we can compute the **Legendre symbol**
$$
\frac{a}{p}
$$
Which is 1 if $a$ is a perfect square in the group (if $a = b^2 \mod p$, then $(b^2)^{(p-1)/2} \equiv b^{p-1} \equiv 1 \mod p$), and -1 if $a$ is not. There exists an algorithm to do this efficiently to distinguish the ideal and real world.

> [!Note] Attack
> Note that if we compute the Zegendre symbol on the 3 group elements we're given, then:
> - For $g^x, g^y, g^z$, we can get any of the 8 patterns by computing the Zegendre symbol on them.
> - For $g^x, g^y, g^{xy}$, there are some patterns we cannot get. If $g^{xy}$'s symbol is 1, then at least $g^x$ or $g^y$ must have a symbol of 1. If $g^{xy}$'s symbol is -1, then $g^x$ and $g^y$ must have a symbol of -1.
>
> If we compute these patterns and match one of the patterns that is possible in the $g^x g^y g^{xy}$ case, we return that we're in the real world. This gives us a distinguishing algorithm with constant probability. 

# Elliptic Curves
Here, we will define Elliptic Curve groups. This is another group that can be used for Diffie-Hellman, and is the go-to method in cryptography right now.

## Points on the Elliptic Curve
A **finite field** is a set of elements that can be viewed as a group with respect to two operations: addition and multiplication.
> In fields, the identity element for addition (0)is not required to have a multiplicative inverse.

With fields, we now define whole polynomials over the elements in the group! 

Let $Z_p$ be a finite field for prime $p \ge 5$. Now consider equation $E$ in variables $x,y$ of the form:
$$
y^2 = x^3 + Ax + B \mod p
$$
Where $A,B$ are constants such that $4A^3 + 27B^2 \ne 0$ (ensuring the cubic polynomial has no repeated roots).

Define $E(Z_p)$ as the set of pairs $(x,y)$ satisfying the above equation as well as a special value of $O$.
$$
E(Z_p) = \{ (x,y) : x,y \in Z_p \land y^2 = x^3 + Ax + B \mod p \} \cup \{O\}
$$
These elements are called the **points on the Elliptic Curve $E$**, where the special value $O$ is called the **point at infinity**.

> [!Example]+ Example: Finding Elliptic Curve Points
> To find the points on an Elliptic Curve:
> 1. First, find the quadratic residues (squares) over $Z_p$. These will be our possible values $y$, and their $y^2$ values.
> 2. Now, take $y^2 = f(x) = x^3 + Ax + B$. Plug in all values for $x$.
>    - Every value of $x$ such that $f(x)$ is a non-zero quadratic residue yields 2 points on our curve. 
>    - Every value of $x$ such that $f(x)$ is a non-quadratic residue are not on the curve
>    - Every value of $x$ such that $f(x) \equiv 0 \mod p$ give 1 point on the curve.
> 
> > Given an $x$ yielding a quadratic residue, we find $y$ by matching the result with matching $y^2$ values in (1). 
> 
> Consider $y^2 = x^3 + 3x + 3 \mod 7$. First, we find our quadratic residues as $\{0,1,2,4\}$.
> - Take $f(0) = 3 \mod 7$. This is a not a quadratic residue.
> - Take $f(1) = 0 \mod 7$. This gives us 1 point on the curve $(1,0)$.
> - Take $f(2) = 3 \mod 7$. This is not a quadratic residue.
> - Take $f(3) = 4 \mod 7$. This is a quadratic residue with roots 2,5, giving us points $(3,2), (3,5)$. 

## Elliptic Curve Groups
For any elliptic curve, we will guarantee the property that every line intersecting $E(Z_p)$ in 2 points, intersects it in exactly 3 points:
1. A point $P$ is counted 2 times if the line is tangent to the curve at $P$.
2. The point at infinity is counted when the line is vertical.

With this property, we will define a group on the Elliptic Curve elements. We define the binary operation **addition ($+$)** as follows:
- For any two points $P_1 + P_2$, the result is the 3rd point intersecting the curve from the line between $P_1, P_2$. 
- We say $O$ is the additive identity, $P + O = O + P = P$.

Under this operation, we can find that for two points $P_1, P_2 \ne 0$, we can calculate their addition as:
1. If $x_1 \ne x_2$, then $P_1 + P_2 = (x_3, y_3)$ with
   $$
   x_3 = [m^2 - x_1 - x_2 \mod p], y_3 = [m - (x_1 - x_3) - y_1 \mod p]
   $$
   for $m = \frac{y_2 - y_1}{x_2 - x_1} \mod p$
2. If $x_1 = x_2$ but $y_1 \ne y_2$, then $P_1 = -P_2$ and so $P_1 + P_2 = O$.
3. If $P_1 = P_2$ and $y_1 = 0$, then $P_1 + P_2 = 2P_1 = O$
4. If $P_1 = P_2$ and $y_1 \ne 0$, then $P_1 + P_2 = 2P_1 = (x_3, y_3)$ with
   $$
   x_3 = [m^2 - 2x_1 \mod p], y_3 = [m - (x_1 - x_3) - y_1 \mod p]
   $$
   Where $m = \frac{3x_1^2 + A}{2y_1 } \mod P$.

> [!Info] DDH Over Elliptic Curves
> Under this, we can perform Decisional Diffie Hellman over Elliptic Curves. In other words, we want to distinguish $(aP, bP, abP)$ from $(aP, bP, cP)$. 
> > Here, $abP$ is the third point from the line drawn by $a,b$, and $c$ is another randomly chosen third point.

> [!Abstract] Theorem: Hasse Bound
> For prime $p$, and Elliptic Curve $E(Z_p)$, we know that the size of the group is
> $$
> p + 1 - 2 \sqrt{p} \le | E(Z_p) | p + 1 + 2 \sqrt{p} 
> $$


# Diffie Hellman Key Exchange
Using the Diffie-Hellman problems, we can define a **key-exchange protocol**.

## EAV-Security for Key Exchange
First, to define security for this protocol, let's define the **key-exchange experiment** $KE^{eav}_{A,\Pi} (n)$.
1. Two parties holding $1^n$ execute the protocol, $\Pi$. This gives a transcript $trans$ containing all messages sent by the parties, and a key $k$ output by each of the parties.
2. A uniform $b = \{0,1\}$ is chosen. If $b = 0$, set $\hat{k} = k$, and if $b = 1$ then choose $\hat{k}$ uniformly at random.
3. Adversary $A$ is given $trans$ and $\hat{k}$, and outputs a bit $b'$ distinguishing what $\hat{k}$ is.
4. The output of the experiment is 1 if $b' = b$, and 0 otherwise.

We say a key-exchange protocol $\Pi$ is secure in the presence of an eavesdropped if for all PPT adversaries $A$, there exists a negligible function $negl$ such that
$$
Pr[KE^{eav}_{A,\Pi} (n) = 1] \le \frac{1}{2} + negl(n)
$$

## Diffie-Hellman Key Exchange
One protocol satisfying this is the **Diffie Hellman Key Exchange**. It works as follows.
1. Both parties agree ahead of time on some group $G$, order $q$, and generator $g$.
2. Alice will randomly choose $x \in \mathbb{Z}_q$, and take $h_1 = g^x$. Alice sends $h_1$ to Bob.
3. Bob will randomly choose $y \in \mathbb{Z}_q$, and similarly compute $h_2 = g^y$. Bob sends $h_2$ to Alice.
4. Alice computes $k_A = h_2^x$, and Bob computes $k_B = h_1^y$. This gives them the same key.
   - This is secure, as the adversary cannot see $x,y$! So, even if the adversary sees $h_1, h_2$, it cannot easily compute $g^{xy}$ as they need to reverse engineer $x,y$ (which is a hard problem).

> This is a protocol used everywhere! Typically, we use ECDH, Elliptic Curve Diffie Hellman.

> [!Abstract] Theorem: Security of Diffie Hellman Key Exchange
> If the DDH problem is hard relative to $G$, then the Diffie-Hellman key exchange protocol $\Pi$ is secure in the presence of an eavesdropper.
>
> > [!Note]- Proof (Sketch)
> > 
> > Intuitively, this is because if the DDH is hard, then a distinguisher has no PPT way of finding $g^{xy}$ given $g^x, g^y$. 

> [!Warning] MiTM Attack Against Diffie-Hellman Key Exchange
> Diffie-Hellman Key Exchange works well, but it assumes that the adversary is only eavesdropping on the communications. If the adversary had the ability to modify the messages in transit, they can perform a **man in the middle attack**.
> 1. Given $A,B$, an adversary can complete a key-exchange protocol with both $A$,$B$.
> 2. Later, when $A$ and $B$ try to communicate, the adversary can decrypt the messages, and re-encrypt them before sending them to the other party. 
> 
> The reason this happens is because there's no way for a client to know who they're communicating with! 


# Public Key Encryption
One way we can prevent the aformentioned man-in-the-middle attack is by using **public key encryption**. A public key encryption scheme is a triplet of PPT algorithms such that:
- `Gen` takes a security parameter and outputs a pair of keys $pk, sk$ called the public key, and secret key, respectively. 
- `Enc` encrypts the message $m$ under the public key $pk$
- `Dec` decrypts the ciphertext $c$ under the secret key $sk$.

## CPA-Security for Public Key Encryption
For a public key encryption scheme, we define the CPA experiment $PubK^{cpa}_{A,\Pi} (n)$:
1. `Gen` is ran to obtain the public key $pk$ and secret key $sk$.
2. The adversary is given $pk$, and returns a pair of equal length messages $m_0, m_1$ in the message space.
3. A uniform bit $b \in \{0,1\}$ is chosen, and $m_b$ is encrypted and sent back to $A$.
4. $A$ guesses which ciphertext they received.

We say the scheme is **CPA-Secure** if for all PPT adversaries $A$, there is a negligible function such that
$$
Pr[PubK^{cpa}_{A,\Pi} (n) = 1] \le \frac{1}{2} + negl
$$

Under a public key encryption scheme, we can send an encrypted message to the other party using $pk$. They can then verify their identity by decrypting with the secret key, which only they have.

But how do we create a public key encryption scheme? 

## El Gamal Encryption
With any key exchange, we can convert it to a public key encryption scheme! 

Below, we show how we can convert Diffie-Hellman Key Exchange into a public key scheme called **El Gamal Encryption**. To see why, consider the following:
- In Diffie-Hellman, $R$ sends $h_1$ to $S$, who sends $h_2$ to $R$. Then, both parties to generate a shared key.
- However, after receiving $h_1$, $S$ can already generate the shared key! So, $S$ can generate the shared key, and encrypt the message with this shared key. It then sends $h_2$ and this ciphertext to $R$.
- $R$ can then generate the shared key, decrypting the ciphertext to get the message. 

Formally, **El Gamal Encryption** works as follows:
1. `Gen`: Obtain $G,q,g$. Choose a uniform $x \in Z_q$, and compute $h = g^x$. The public key and secret key are defined as follows:
   $$
   pk = (G,q,g,h = g^x) \qquad
   sk = (G,q,g,x)
   $$
2. `Enc`: Given $pk = (G,q,g,h = g^x)$ and message $m \in G$, choose a uniform $y \in Z_q$ and create ciphertext
   $$
   c = (g^y, h^y \cdot m)
   $$
3. `Dec`: Given $sk = (G,q,g,x)$ and ciphertext $c = (c_1, c_2)$, we can find message
   $$
   m = c_2 * (c_1^x)^{-1}
   $$

> Note that in decryption, $(c_1^x)^{-1}$ stands for us applying the group operation $x$ times (to find h^{xy}), then finding its multiplicative inverse. 

> [!Abstract] Theorem: Security of El Gamal
> If the DDH problem is hard relative to $G$, then the El Gamal encryption scheme is CPA-secure.

# Digital Signatures
Using public key encryption, we can also define a signature scheme. 

We define a **digital signature scheme** as follows:
1. `Gen`: Takes a security parameter $1^n$, and outputs a public key $pk$ and secret key $sk$. 
2. `Sign`: A signing algorithm that takes a private key $sk$, and a message $m$ from some message space. It outputs a signature $Sign_{sk} (m) = \sigma$.
3. `Vrfy`: Takes the public key $pk$, a message $m$, and a signature $\sigma$, and output a $b$ that is 1 if we have validity, 0 otherwise. 

## Signature Security
For security, we define the $SigForge_{A,\Pi} (n)$ experiment:
1. `Gen` is ran to obtain $pk,sk$.
2. The adversary is given $pk$ and access to an oracle $Sign_{sk} (\cdot)$.
3. The adversary outputs $(m, \sigma)$. Let $Q$ denote the set of all queries that $A$ asked the oracle.
4. $A$ succeeds if and only if $Vrfy(m, \sigma) = 1$ and $m \not\in Q$ (not queried before).
5. If $A$ succeeds, the experiment is 1.

We say the scheme is secure if
$$
Pr[SigForge_{A,\Pi} (n) = 1] \le negl
$$

## Schnorr Identification Scheme
To construct a signature from the discrete logarithm, we will first construct an **identification scheme**. This is a scheme which can be used to prove knowledge of a secret key without revealing the secret key.
> After this, we will perform a **Fiat-Shamir Transform** to covert an identification scheme into a signature scheme.

The **Schnorr Identification Scheme** works as follows. Consider two parties, the prover $P$ and the verifier $V$:
1. Prover $P$ has secret key $x$, and verifier $V$ has public key $y = g^x$.
2. $P$ chooses uniform $k \in Z_q$, and computes $I = g^k$. $P$ sends this to $V$. 
3. $V$ now chooses a challenge, a uniform $r \in Z_q$. $V$ sends this to $P$.
4. $P$ computes $s = [rx + k \mod q]$, and sends this to $V$.
5. $V$ can now check whether $g^s \cdot y^{-r} = g^k$. 
   - If the prover is legitimate, then the verifier will find that $g^s \cdot y^{-r} = g^{rx + k} \cdot g^{-rx} = g^k$. 

This scheme is secure, and does not actually leak what $x$ is. Intuitively, this is because $s$ functions as a one-time pad, because $k$ is chosen uniformly. This obscures $x$.

To formally show this, we will want to prove the following.

> [!Note] Proof: Prover Knows $x$
> We first show that under this scheme, the prover knows $x$. To do this, suppose we have a "knowledge extractor". This extractor will take a prover who won the scheme. Given this prover, we can use it to compute the discrete log of $y = g^x$ in polynomial time. 
> > This shows that the prover knows $x$, as a polynomial computation of the discrete log would be impossible otherwise.
>
> What our extractor will do is find two "paths", starting with $I$, that are accepted in our scheme. After we find these paths, we have for some initial $I$, one path $r_1, s_1$, and another $r_2, s_2$. Using these, we can compute $x$.
> $$
> \begin{align*}
> g^{s_1} * y^{-r_1} = I = g^{s_2} * y^{-r_2} \\
> g^{s_1 - s_2} = y^{r_1 - r_2} \\
> g^{\frac{s_1 - s_2}{r_1 - r_2}} = y \\
> x = \frac{s_1 - s_2}{r_1 - r_2}
> \end{align*}
> $$
> > This is called the Forking Lemma. We can get 2 accepting transcripts in polynomial time using rewinding.


> [!Note] Proof: No Information is Leaked about $x$
> We also show that under this scheme, no information is leaked about $x$. To do this, we will show that we can take a polynomial-time simulation, which, given $y$, can simulate transcripts of identification protocols. 
>
> We construct a simulator that outputs correctly distributed transcripts $(I,r,s)$. 
> 1. Sample from the marginal distribution over $(r,s)$, both selected randomly. 
> 2. Sample consistent $I$ from the space of $g$, dependent on $r,s$, which we can compute as $g^s * y^{-r} = I$.
>    - By definition of the scheme, we have exactly 1 possible $I$ value that works!
> 
> These are all successful transcripts of identification protocols.
> > This is called Honest Verifier Zero Knowledge.

## Fiat-Shamir Transform
After constructing an identification scheme, we then apply the **Fiat-Shamir Transform** to it to obtain a signature scheme. 

This transform works as follows, giving us the **Schnorr Signature Scheme**.
- `Gen`: Obtain keys $pk = g^x, sk = x$. 
- `Sign`: Given a private key $sk$ and message $m$,
  1. Compute $I = g^k$ for uniform $k$.
  2. Instead of a random $r$, compute $r = H(I || m)$. 
  3. Use this $r$ to compute $s = rx + k$.
  4. Return signature $(r,s)$.
- `Vrfy`: Given public key $pk$, message $m$, and signature $(r,s)$, compute $I = g^s y^{-r}$. Rehash $H(I || m)$, and return 1 if this hash equals our original $r$.
