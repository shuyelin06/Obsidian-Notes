---
title: CMSC456
tags:
- cmsc456
---

This course covers the theory behind modern cryptography. The goal of this field is to **secure information**. To do this, we want to uphold:
- **Data Privacy**: Ensure that adversaries cannot see or obtain the message.
- **Data Integrity / Authentication**: The message origin can be verified (authenticity), and the message has not been modified in transit (integrity).

Common symbols / terminology:
- $M$: The message we want to keep secure
- $K$: A key we use to encrypt and/or decrypt the message
- $C$: The encrypted message; ciphertext.

Notes are below.
- [[SymmetricEncryption | Symmetric Key Encryption]]

---

# Number Theory
## Groups
### Definition
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

### Group: Modular Arithmetic (Addition)
We say that two numbers $a,b$ are **congruent modulo $p$**, denoted
$$
a \equiv b \mod p
$$

If $p$ divides $(a - b)$, or in other words, $p \vert (a - b)$.

> [!Example] Example: Modular Equivalence
> All of the following are true.
> $$
> 2 \equiv 15 \mod 13 \qquad 
> 28 \equiv 15 \mod 13 \qquad
> -11 \equiv 15 \mod 13
> $$

Addition works in modular space as normal. You perform regular addition, and then take modulo $p$. For example,
$$
8 + 10 \mod 13 \equiv 18 \mod 13 \equiv 5 \mod 13
$$

Addition has the following properties. Consider the set of numbers $\mathbb{Z}_p = \{0,1,\dots p-1\}$:
- **Identity**: $\forall a \in \mathbb{Z}_p$, adding 0 to it yields the same number
- **Additive Inverse**: $\forall a \in \mathbb{Z}_p$, $\exists b$ such that $a + b \mod p = 0$, given as $b = p - a$.
- **Closure**: Any addition operations will yield a result that is still inside of $\mathbb{Z}_p$.
- **Associativity**: You can take modulo at any point in the operation. For example,
  $$
  ((a + b) \mod p + c) \mod p = (a + (b + c) \mod p) \mod p
  $$

The set $\mathbb{Z}_p$ with our addition modulo operator defines a group!

### Group: Modular Arithmetic (Multiplication)
For the purposes of security, we are mainly interested in **multiplicative** groups over the integers, as this introduces computational problems believed to be hard to solve.

Let's look at the **multiplication modulo $p$ group**. Let $Z^*_p = \{1, \dots p - 1\}$, with the multiplication mod operation. For $Z^*_p$ to be a group it must be true that **p is prime**. 
> If $p$ is not prime, then we won't have the property of the inverse!

We argue below that $Z^*_p$ satisfies the inverse property (the rest are trivial to prove). In other words, $\forall a \in Z^*_p$, there exists a $b$ such that $a * b \mod p = 1 \mod p$. 

> [!Example]+ Example: Brute Force Inverse
> Suppose we ant to find the multiplicative inverse of $9 \mod 11$.
>
> One way to do this is to brute-force iteratively try all 10 numbers in $Z^*_{11}$ to find our inverse. We will consider this brute-force to be exponential time! This is because when we're using this with respect to binary numbers, the length of our input is on the magnitude of $2^n$. 

> [!Abstract] Theorem: Euclidean Algorithm
> Let $a, p$ be positive integers. Then, there exists integers $X,Y$ such that $Xa + Yp = gcd (a,p)$. 
>
> The Euclidean algorithm can be used to compute $gcd (a,p)$ in polynomial time. We can then extend this to compute $X,Y$ in polynomial time.
> > This algorithm has time complexity $2 \log (b)$, for $gcd (a,b)$. 

We can use the Euclidean Algorithm to show that our group has a multiplicative inverse. 

> [!Note]- Proof
> Let $a \in Z^*_p$. Then, $gcd(a,p) = 1$ because $p$ is prime. By the Euclidean Algorithm, we can find $X,Y$ such that $aX + pY = gcd(a,p) = 1$.
> 
> Rearranging terms, we can find that $pY = (1 - aX)$, so $p$ divides $aX - 1$, so $Xa \mod p = 1$. In other words, $X$ is our multiplicative inverse for $a$. 


> [!Example]+ Example: Euclidean Algorithm
> Suppose we want $gcd(9,23)$.
> $$
> \begin{align*}
> 23 = 2 * 9 + 5 \\
> 9 = 1 * 5 + 4 \\
> 5 = 1 * 4 + 1 \\
> 4 = 4 * 1 + 0
> \end{align*}
> $$
> > Every iteration, we try to divide the second component of our product by our additive term.  
> 
> So, our greatest common divisor is 1 (take the $b$ term of the component before 0).

---

What about **Modular Exponentiation**? Given $a, m, N$, can we efficiently compute $a^m \mod N$?

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
This has runtime $O(\log_2(m))$! So, Modular Exponentiation can be done efficiently.

---

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

## Group: Modular Multiplication, N Composite
What about multiplicative groups modulo $N$, where $N$ is composite? 

For numbers $\{1, \dots, N - 1\}$, only numbers $a$ such that $gcd(a,N) = 1$ have a multiplicative inverse by the Extended Euclidean Algorithm. All others do not have a multiplicative inverse, so because of this, to obtain a group, we must disclude these values from our group.
$$
Z^*_N = \{a \in \{1, \dots N-1\} : gcd(a,N) = 1\}
$$

Then, $Z^*_N$ is an abelian, multiplicative group.

Assume $N = p \cdot q$, where $p, q$ are distinct primes. What is the order of $Z^*_N$, denoted $\phi(N)$, the **Euler totient function**?
$$
\phi(N) = (p - 1) (q - 1) = N - p - q + 1
$$
> Intuitively, this is because we only have to take out numbers $1p, 2p, 3p, \dots q * p$ which have $q$ elements, and $1q, 2p, 3p, \dots q * p$ which have $p$ elements. We add 1 as we're double counting the $q * p$ element in our removal.

Generalizing this, we can find $\phi(N)$ as

> [!Abstract] Theorem
> Let $N = \prod_i  p_i^{e_i}$, where $\{p_i\}$ are distinct primes and $e_i \ge 1$. Then
> $$
> \phi(N) = \prod_i p_i^{e_i - 1} (p_i - 1)
> $$

> However, finding this prime factorization of $N$ is a very difficult problem! 

By this theorem, and using the previous theorems, we know that for any $a$ such that $gcd(a,N) = 1$,
$$
a^{\phi(N)} \equiv 1 \mod N
$$
This can be used as a "quick / easy" vertification that someone has found $\phi(N)$!
> A corollary of this theorem is that $g^x = g^{x \mod \phi(N)}$ (since every $\phi(N)$, we wrap around). This makes things easy if we can find the prime factorization of $N$. 

### Cyclic Groups
For a finite group $G$ of order $m$ and $g \in G$, consider
$$
\langle g \rangle = \{g^0, g^1, \dots g^{m-1} \}
$$
Here, $\langle g \rangle$ always forms a cyclic subgroup of $G$. As there may be repeats, $\langle g \rangle$ may be a subgroup with a smaller order than $m$.

If the order of $\langle g \rangle$ is equal to $G$, we say that $G$ is a **cyclic group** and $g$ is a **generator** of $G$

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

Let $G$ be a finite group and $g \in G$. The **order** of $g$ i the smallest positive integer $i$ such that $g^i = 1$.

> [!Abstract] Propositions
> 1. Let $G$ be a finite group, $g \in G$ with order $i$. Then, for any integer $x$, we have $g^x = g^{x \mod i}$.
> 2. Let $G$ be a finite group and $g \in G$ with order $i$. Then, $g^x = g^y$ if and only if $x \equiv y \mod i$.
> 3. Let $G$ be a finite group of order $m$, and $g \in G$ with order $i$. Then, $i | m$.

Thus, if we have a prime order group, then the only orders that we can get for $i$ are 1 and $p$! Because $i = 1$ is only possible with the identity element, this means all other elements are generators of $G$. **We want to find these prime order groups, as they give us a basis for cryptographic problems**.

> [!Abstract] Theorem
> If $p$ is prime, then $Z^*_p$ is a **cyclic group of order** $p - 1$. 

Using the above theorem, we will construct a subgroup of $Z^*_p$ to construct a prime order group. 

> [!Note] Prime Order Cyclic Groups
> Let $Z^*_p$, where $p$ is a strong prime: $p = 2q + 1$, where $q$ is also prime. By the above theorem, $Z^*_p$ is a cyclic group of order $p - 1 = 2q$. 
> > We will cleverly take 1/2 of the elements of $Z^*_p$, to get a group of order $q$, which is prime!
>
> Take the subgroup of perfect squares in $Z^*_p$ (quadratic residues): $i^2 \mod 2q$. This will yield the prime order group we want.
>
> Because $Z^*_p$ is cyclic, it has a generator $g$. For this generator, every even power of $g$ yields a perfect square! As the order of the group is $2q$, we take every other power of $g$ to give us a subgroup of order $q$. This gives us a prime order group!

## Cyclic Group Problems
There are 3 main problems on cyclic groups.

### Discrete Logarithm Problem
We define the **Discrete-Log Experiment** $DLog_{A,G} (n)$ as follows:
1. Run $G(1^n)$ to get $(G,q,g)$, where $G$ is a cyclic group of order $q$, and generator $g$.
2. Choose a uniform $h \in G$.
3. Adversary $A$ is given $G,q,g,h$, and outputs $x \in Z_q$.
4. The output of the experient is 1 if $g^x = h$ and 0 otherwise.
   - The adversary has to guess the exponent $x$ to get $g^x = h$.

> As $q$ is typically on the magnitude of $2^{2048}$ or $2^{1024}$, it would be extremely inefficient to do a brute force attack. 

We say the **Discrete-Logarithm Problem** is hard relative to $G$ if for all PPT algorithms $A$, there exists a negligible function such that
$$
Pr[Dlog_{A,G} (n) = 1] \le negl(n)
$$
> This is the hardest problem, that all of the Diffie-Hellman problems are based off of.

### Diffie-Hellman Problems
We define the **Computational Diffie-Hellman (CDH)** problem as follows. 

*Given $(G,q,g)$ and uniform $h_1 = g^{x_1}$, $h_2 = g^{x_2}$, compute $g^{x_1 \cdot x_2}$.*
> Note that $h_1 \cdot h_2 = g^{x_1 + x_2}$, which won't solve our problem.

This problem is based on the Discrete Logarithm problem, as if we could solve Discrete Log, we could solve for $x_1, x_2$ in PPT time and compute our result. However, because Discrete Log is a hard problem, this is also hard. 

---

We define the **Decisional Diffie-Hellman (DDH)** problem as follows.
1. Define a distinguisher $D$, who gets one the group $G$, order $q$, generator $g$, and one of the following:
   - **Ideal World**: $g^x, g^y, g^z$, 3 independent group elements with no correlation to each other.
   - **Real World**: $g^x, g^y, g^{xy}$, 3 group elements where the 3rd is related to the first two through the CDH problem.
2. The distinguisher gets one of the worlds, and has to guess the world that they're in.

We say that the DDH problem is hard if for all PPT adversaries $A$, they can only guess what world they're in with a negligible probability.
$$
| Pr[D(G,q,g,g^x,g^y,g^z) = 1] - Pr[D(G,q,g,g^x,g^y,g^{xy}) = 1] | \le negl
$$

Note that DDH is **NOT HARD** over $Z^*_p$ for for prime $p$. This is because for $a \in Z^*_p$, we can compute the **Zegendre symbol**
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

## Elliptic Curves
### Setup
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
> 1. First, find the quadratic residues (squares) over $Z_p$.
> 2. Now, take $y^2 = f(x) = x^3 + Ax + B$. Plug in all values for $x$.
>    - Every value of $x$ such that $f(x)$ is a non-zero quadratic residue yields 2 points on our curve. 
>    - Every value of $x$ such that $f(x)$ is a non-quadratic residue are not on the curve
>    - Every value of $x$ such that $f(x) \equiv 0 \mod p$ give 1 point on the curve.
>
> Consider $y^2 = x^3 + 3x + 3 \mod 7$. First, we find our quadratic residues as $\{0,1,2,4\}$.
> - Take $f(0) = 3 \mod 7$. This is a not a quadratic residue.
> - Take $f(1) = 0 \mod 7$. This gives us 1 point on the curve $(1,0)$.
> - Take $f(2) = 3 \mod 7$. This is not a quadratic residue.
> - Take $f(3) = 4 \mod 7$. This is a quadratic residue with roots 2,5, giving us points $(3,2), (3,5)$. 

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

### DDH Over Elliptic Curves
Under this, we can perform Decisional Diffie Hellman over Elliptic Curves. In other words, we want to distinguish $(aP, bP, abP)$ from $(aP, bP, cP)$, where 

---

Size and Hasse BOund

---

Using this, we define the following key-exchange experiment $KE^{eav}_{A,\Pi} (n)$.
1. Two parties holding $1^n$ execute $\Pi$. This gives a transcript containing all messages sent by the parties, and a key $k$ output by each of the parties.
2. A uniform $b = \{0,1\}$ is chosen. If $b = 0$, set $\hat{k} = k$, and if $b = 1$ then choose $\hat{k}$ uniformly at random.
3. Adversary $A$ is given $trans$ and $\hat{k}$, and outputs a bit $b'$ distinguishing what $\hat{k}$ is.
4. The output of the experiment is 1 if $b' = b$, and 0 otherwise.

We say a key-exchange protocol $\Pi$ is secure in the presence of an eavesdropped if for all PPT adversaries $A$, there exists a negligible function $negl$ such that
$$
Pr[KE^{eav}_{A,\Pi} (n) = 1] \le \frac{1}{2} + negl(n)
$$
