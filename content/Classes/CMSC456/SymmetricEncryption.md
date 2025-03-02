---
title: Symmetric Key Encryption
tags:
- cmsc456
---

Here, we will explore the theory behind **symmetric key encryption**. This is encryption, where both parties can send secure messages to each other with some shared (and private) key. 
> Sometimes, we call symmetric key encryption schemes **ciphers**.

One of the driving principles behind symmetric key encryption is as follows:

> [!Tip] Kerckhoffs' Principle
> A good cipher scheme should be able to be **public**, without adversaries being able to use it to decrypt messages. To do this, both parties share a secret key for encryption / decryption which adversaries are assumed to not know. 
>
> **Secure schemes do not get their security from being poorly defined.** 

We always have to assume that the crypto designs are public! This is more suitable for large-scale usage of cryptography, and exposes schemes to the public eye so that they can be revised and strengthened. 

# Historical Ciphers
Let's first examine some historical schemes before going into the theory.

For each of the following historical schemes, we will discuss the encryption algorithm, the decryption algorithm, the key-space (set of all possible keys) and secret key, and how to break the scheme.

## Atbash Cipher
The **Atbash Cipher** substitutes the first letter with the last, the 2nd with the 2nd last, and so on. To encrypt and decrypt, simply swap the letters.

Because there is nothing that is secret, there is no key for this algorithm. 

## Shift / Caesar Cipher
The **Caeser Cipher** replaces each letter by the letter which is $n$ positions away in the alphabet. On a message, this has the effect of "shifting" every letter $n$ positions in the alphabet.

As there are 26 letters in the alphabet, there are 26 possible shifts we could do. Thus, our key-space has a size of 26.

Because the key-space is so small, we can easily brute-force this cipher by trying all possible shifts! Thus, this cipher is suspectible to a **brute-force search**.
> For a secure scheme, it's necessary that the key space is large! However, a large key space does not imply security.

## Scytale Cipher
The **Scytale Cipher** stacks letters of the message into $n$ equal-sized rows. Reading the message column-by-column will give you the ciphertext (encryption), and reading the message row-by-row will give you the plain-text (decryption).

As we could have a nearly infinite number of rows, the key-space is arbitrarily large! 

That does not make this cipher secure however, as we may be able to recover the key! Starting from the first letter, we can take letters that are offset $i$ positions from the start, to try to form a word. Once we get something that makes sense, we'll have recovered our key!
> Information about our ciphertext can let us reverse engineer the key!

## Monoalphabetic Substitution
The **Monoalphabetic Substitution** maps every plaintext letter to a different ciphertext character, and substitutes them as so. Using this map, we can encrypt and decrypt our message.

The size of our key-space is $26!$, which is really large! So, brute force search is not possible, but because of the 1-1 mapping, we could do a **frequency analysis** to recover the key! 

> [!Info] Frequency Analysis
> Frequency analysis is based off the fact that letters in (gramatically correct) English generally have different usage frequencies. If we know the frequencies of the ciphertext characters, we can guess what the mappings are.


# Symmetric Key Encryption 
## Formal Definition
A **symmetric encryption scheme** is defined by 3 algorithms: `Gen`, `Enc`, `Dec`. Let $M$ be our message space, with $|M| > 1$.
1. `Gen`: The **key-generation algorithm** (typically probabilistic), which creates a key $k$ according to some distribution (must be probabilistic). 
   - $K$ denotes the keyspace, the set of all possible keys.
2. `Enc`: The **encryption algorithm**, which takes an input key $k \in K$ and message $m \in M$ to create ciphertext $c \leftarrow Enc_k (m)$ (could be probabilitic). 
   - $C$ denotes the ciphertext space, the set of all possible ciphertexts.
3. `Dec`: The **decryption algorithm**, which takes an input key $k \in K$ and ciphertext $c \in C$ to create message $m := Dec_k (c)$ (must be deterministic).

> **Correctness** mandates that $Dec_k (Enc_k (m)) = m$. If this does not hold, our encryption scheme won't be very practical.

Each of the spaces $K,M,C$ can be given as random variables with probability distributions. Let $Pr[...]$ denote the probability function. Then:
- $Pr[K = k], k \in K$ denotes the probability that the key output by `Gen` yields $k$.
  > Typically, we will assume that $K$ has the uniform probability distribution (each key is of equal probability)
- $Pr[M = m], m \in M$ denotes the probability that the message is equal to $m$, modeling some prior knowledge the adversary may have about the message.
- $Pr[C = c], c \in C$ denotes the probability that the ciphertext is $c$, which is fully determined by the distribution on $K$, $M$, and `Enc`.
  - $C = Enc_K (M)$

We assume that the distributions over $K$ and $M$ are independent.

## Perfect Secrecy
We say an encryption scheme over a message space $M$ is **perfectly secret** if $\forall$ probability distributions over $M$, $\forall m \in M, \forall c \in C$ such that $Pr[C = c] > 0$,
$$
Pr[M = m | C = c] = Pr[M = m]
$$
In other words, the probability that our message is $m$ does not change even if we know what the ciphertext $c$ is. Sometimes, we denote $Pr[M = m]$ as the **a priori** distribution, and $Pr[M = m | C = c]$ as the **a posteriori** distribution.
> This means that seeing $c$ does not give us any information about the message space!

There are a few equivalent definitions to perfect secrecy.

> [!Abstract] Equivalence 1
> An encryption scheme over a message space $M$ is **perfectly secret** if and only if $\forall $ probability distribution over $M$, $\forall m \in M$, $\forall c \in C$,
> $$
> Pr[C = c | M = m] = Pr[C = c]
> $$
> In other words, this is saying that the ciphertext is independent of the message (as we can still vary the key $k$).
>
> > [!Note]- Proof (One-Way)
> > 
> > Suppose that we have a perfectly secret scheme. We wish to show that $Pr[C = c | M = m] = Pr[C = c]$ is also true. 
> > 
> > Fix message distribution $M$, $m \in M$, $c \in C$. By definition, we know that the following must hold by perfect secrecy.
> > $$
> > Pr[M = m | C = c] = Pr[M = m]
> > $$
> > and by Baye's Rule,
> > $$
> > \begin{align*}
> > Pr[M = m | C = c] = Pr[M = m] \\
> > \frac{Pr[C = c | M = m] P[M = m]}{Pr[C = c]} = Pr[M = m] \\
> > Pr[C = c | M = m] = Pr[C = c]
> > \end{align*}
> > $$

> [!Abstract] Equivalence 2: Perfect Indistinguishability
> An encryption scheme over a message space $M$ is **perfectly secret** if and only if $\forall$ probability distribution $M$, $\forall m_0, m_1 \in M$, and $\forall c \in C$,
> $$
> Pr[C = c | M = m_0] = Pr[C = c | M = m_1]
> $$

> [!Example]- Example: Perfect Secrecy Example
> An encryption scheme with message space $M$ is perfectly secret if and only if $\forall$ probability distribution over $M$, $\forall m, m' \in M$ and $\forall c \in C$, we have
> $$
> Pr[M = m | C = c] = P[M = m' | C = c]
> $$
> 
> Prove or refute this.
> 
> This is false. For every perfectly secret encryption scheme, we can always choose a distribution on $M$ for which this is false.
> 
> By way of contradiction, suppose this is true. Now, choose a distribution such that
> $$
> Pr[M = m] > Pr[M = m']
> $$
> Then, by definition of perfect secrecy,
> $$
> Pr[M = m | C = c] = Pr[M = m] > Pr[M = m'] = Pr[M = m' | C = c]
> $$
> Which is a contradiction!

> [!Example]- Example: Perfect Secrecy Example (2)
> An encryption scheme with message space $M$ is perfectly secret if and only if $\forall$ probability distribution over $M$, $\forall m, m' \in M$ and $\forall c \in C$, $Pr[C = c] > 0$,
> $$
> Pr[K = k | C = c] = Pr[K = k]
> $$
> 
> 1. Explain this definition in English.
> 2. Why is this a bad definition? Describe an encryption scheme that leaks information about the message but still satisfies the definition.
> 
> Seeing the ciphertext does not tell us any information about the key.
> 
> This is bad, because we could just choose an encryption scheme with only one key, so it's completely deterministic! For example, we do a shift cipher with only possible key $k = 13$. Then, for any ciphertext, $Pr[K = k | C = c] = 1 = Pr[K = k]$, but we can easily reverse the encryption scheme.
> > Another solution is, this definition says nothing about the message! So, we could have a scheme that doesn't do anything to the message (leaves it unencrypted), and generates a random key! 

> [!Example]- Example: Perfect Secrecy Example (3)
> $M = \{0,1, \dots n-1\}$, $K = \{0,1,\dots n-1\}$. Gen() chooses a key at random from $K$, $Enc_k(m) = m + k$, $Dec_k (c) = c - k$. Is this perfectly secret?
>
> No. BWOC, suppose it is. Let $n = 20$, and let $M$ have the uniform distribution, and let $m = 10, c = 5$. Then,
> $$
> Pr[M = 10 | C = 5] = 0 \ne Pr[M = 10] = \frac{1}{20}
> $$

## The One-Time Pad
Here, we describe a perfectly secret symmetric encryption scheme -- the **One-Time Pad**. It works as so:
1. Fix integer $\ell > 0$. $M,K,C$ are all equal to $\{0,1\}^\ell$.
2. `Gen`: Choose a string from $K = \{0,1\}^\ell$ according to the uniform distribution
3. `Enc`: Given $k \in \{0,1\}^\ell$, $m \in \{0,1\}^\ell$, output $c := k \oplus m$.
4. `Dec`: Given $k \in \{0,1\}^\ell$, $c \in \{0,1\}^\ell$, output $m := k \oplus c$.

> Note that the notation $\{0,1\}^\ell$ stands for binary numbers (digits 0 or 1) of length $\ell$.

> [!Example]+ Example: One-Time Pad Example
> Let's see an example of the one-time pad. Let $\ell = 3$, and suppose we have message $m = 011$, key $k = 101$. 
> 
> One time pad encrypts the ciphertext by XORing the binary numbers.
> ```
> 011 XOR 101 = 110
> ```
> $c = 110$! To decrypt, we XOR the ciphertext with our key again.
> ```
> 110 XOR 101 = 011
> ```

> [!Abstract] Theorem: OTP Secrecy
> The one-time pad encryption scheme is perfectly secret.
>
> > [!Note]- Proof
> > 
> > Recall that a scheme is perfectly secret if for all distributions on $M$, $\forall c \in C$, $\forall m_0, m_1 \in M$,
> > $$
> > Pr[C = c | M = m_0] = Pr[C = c | M = m_1]
> > $$
> > 
> > Fix distribution over $M$, $c \in C$, $m_0, m_1$. 
> >
> > For $c, m$,
> > $$
> > \begin{align*}
> > Pr[C = c | M = m] 
> > &= Pr[M \oplus K = c | M = m] &\text{OTP Scheme} \\
> > &= \frac{Pr[M \oplus K = c \land M = m]}{Pr[M = m]} &\text{Conditionals} \\
> > &= \frac{Pr[m \oplus K = c \land M = m]}{Pr[M = m]} \\
> > &= \frac{Pr[K = c \oplus m \land M = m]}{Pr[M = m]} \\
> > &= \frac{Pr[K = c \oplus m] Pr[M = m]}{Pr[M = m]} &\text{K, M Independent} \\
> > &= Pr[K = m \oplus c] = \frac{1}{2^\ell}
> > \end{align*}
> > $$
> > 
> > Thus,
> > $$
> > Pr[C = c | M = m_0] = \frac{1}{2^\ell} = Pr[C = c | M = m_1]
> > $$
> > By perfect indistinguishability, OTP is perfectly secret.

The one-time pad is one of the few perfectly secret algorithms, and in fact, many schemes are variants / equivalent to the one-time pad. Thus, for proofs it's often a good idea to start from the OTP and modify the scheme from there.

> [!Example]- Example: Perfectly Secret Example
> Prove or refute: An encryption scheme with message space $M$ is perfectly secret if and only if for every probability distribution over $M$ and every $c_0, c_1 \in C$ we have $Pr[C = c_0] = Pr[C = c_1]$.
> 
> Not true. To show why, we will construct a perfectly secret scheme that violates this. To do this, we will start from the one-time-pad (this is a good technique).
>
> For message of length $\ell$, let's take a key of length $\ell + 1$, $k||b$ where $k \in \{0,1\}^\ell$, $b = 0,1$ with varying probabilities. Then, 
> $$
> c = (m \oplus k) || b
> $$
> > $||$ stands for the concatenating of binary strings together.
> 
> Because of the biased bit, our ciphertexts do not have the same probability, but no information is released!
>
> Formally, choose any distribution over $M$, $c_0, c_1$, where $c_0 = c || 0, c_1 = c || 1$. Then,
> $$
> Pr[C = c || 0] = Pr[C = c] * Pr[B = 0] \ne Pr[C = c] * Pr[B = 1] = Pr[C = c || 1]
> $$

The one-time pad is a powerful scheme, but it doesn't come without its flaws:
1. The key length is the same as the message length, so for every bit communicated over a public channel, a bit must be shared privately. 
   - This is an inherent problem in perfectly secret encryption schemes! We prove this in the following theorem. 
2. Key can only be used once.

> This makes it very difficult to use the one-time pad in practice.


> [!Abstract] Theorem: Limitations of Perfect Secrecy
> Let us have a perfectly secret encryption scheme over message space $M$, key space $K$. Then, it must be true that $|K| \ge |M|$.
> > In most cases, this means that the lengths of the keys must be the same or longer than the lengths of our messages!
>
> > [!Note]- Proof
> > 
> > By way of contradiction, assume we have a perfectly secret encryption scheme where $|K| < |M|$.
> > 
> > To obtain our contradiction, we must show that there exists a probability distribution $M$, message $m \in M$, and ciphertext $c \in C$ such that
> > $$
> > Pr[M = m | C = c] \ne P[M = m]
> > $$
> > > Often, when contradicting perfect secrecy, we use the uniform distribution on $M$.
> > 
> > Let $M$ have the uniform distribution. By perfect secrecy, for $m \in M$, $c \in C$,
> > $$
> > Pr[M = m | C = c] = P[M = m]
> > $$
> > Let's do a brute force search over the key-space. Let $\mathbb{M}(c)$ be the set of all messages $Dec_K (c)$. Because the decryption is deterministic, we have that $|\mathbb{M}(c)| \le |K| < |M|$ (it can be smaller if multiple keys decrypt to the same message). 
> > 
> > So, there exists some message $m^* \in M$ that is contained in $M$ but not $\mathbb{M}(c)$. Choose this message instead. Then,
> > $$
> > Pr[M = m^* | C = c] = 0 \ne P[M = m^*] = \frac{1}{|M|}
> > $$
> > This is a contradiction! So, our scheme cannot be perfectly secret.

> [!Abstract] Shannon's Theorem
> Let `Gen, Enc, Dec` be an encryption scheme with message space $M$, for which $|M| = |K| = |C|$. Then, the scheme is perfectly secret if and only if:
> 1. Every key $k \in K$ is chocsen with equal probability $1 / |K|$ by `Gen`.
> 2. For every $m \in M, c \in C$, there exists a unique key $k \in K$ such that $Enc_k (m) \to c$.
>
> > Note that this **only applies when $|M| = |K| = |C|$**! If this condition is not true, then we cannot use Shannon's Theorem.

> [!Example] Example: Shannon's Theorem Example
> Let $M = \{0, \dots n - 1\}, K = \{0, \dots n - 1\}$. Let $Gen()$ choose a key at random.
> - $Enc_k (m) = m + k \mod n$
> - $Dec_k (c) = c - k \mod n$
> 
> Shannon's theorem applies here! First, we know by assumption that all keys are chosen uniformly.
>
> We also show that for $m, c$, we explicitly can solve for a single $k$ such that $Enc_k (m) \to c$. We find
> $$
> m + k \mod n = c \Longrightarrow k = c - m \mod n
> $$


# The Computational Approach 
## Motivation
Shannon's Theorem asserts that for correct schemes that are perfectly secret, $|K| = |M|$. Thus, achieving perfect secrecy is, in many cases, unpractical for many real world situations.

Here, we explore a more relaxed definition for security, known as the **computational approach**. The computational approach only requires the following:
- Security is only guaranteed against efficient adversaries that run for some feasible amount of time.
  - **Efficient adversaries** are adversaries that can run in polynomial time (we also call them PPT adversaries).
- Adversaries **can** potentially succeed with some very small probability.
  - Adversaries can succeed, but they would need to run in non-polynomial time-- they would run out of time if they were running in non-polynomial time. 

We formally define these notions below.

## Formal Definitions
Under the computational approach, schemes now have an additional parameter called the **security parameter ($n$)**. 

Prior to running our scheme, we can set our security parameter, which tells us the run time of the adversary and its success probability as functions of $n$. This gives a sort of guarantee against adversaries running in polynomial time. 
> We can think of the security parameter as the length of the key.

---

An adversary is **efficient** if they are in polynomial time (PPT). To be in polynomial time means that there exists some polynomial $p$, such that the adversary runs for time at most $p(n)$ when the security parameter is $n$.

> [!Example] Example: Polynomial Time Functions
> - $2n^2 + 3n + 5$ is a polynomial function in $n$
> - $\log n^{\log n}$ is not a polynomial function in $n$
> - $2^{\sqrt{\log n}}$ is a polynomial function in $n$
> 
> > To know if a function is polynomial, it may help to take the log, and see if this is bounded below or above by $\log(n)$ (this is the logarithm of a polynomial!) 
> 
> Given a security parameter $n$, to say an adversary is running in time $p(n) = n^2$ means that for $n$, the adversary has that amount of time to run.

---

A small probability of success means we have a **negligible probability**. A function $f$ is **negligible** if for every polynomial $p$, and sufficienly large $n$, it holds that
$$
f(n) < \frac{1}{p(n)}
$$
In other words, as $n \to \infty$, the function is smaller than all polynomial functions.
$$
f(n) < \frac{1}{n^c} \qquad \forall c \in \mathbb{R}
$$
**The product of any polynomial with a negligible function is a negligible function**! 
> To know if a function is negligible, take its reciprocal and see if its super-polynomial or not! If its reciprocal is a super-polynomial, then $f$ is negligible.

> [!Example] Example: Negligible Functions
> - $1 / 2^n$ is negligible
> - $1 / \log n$ is not negligible
> - $1 / 2^{\sqrt{n}}$ is negligible
> - $1 / n^2$ is not negligible

> [!Tip] Practical Implications of Computational Security
> Why do we define computational security as so?
> 
> Let's say for key size $n$, any adversary running in time $2^{n/2}$ breaks the scheme with probability $1 / 2^{n/2}$. Meanwhile, `Gen, Dec, Enc` take time $n^2$.
>
> If $n = 128$, then
> - `Gen,Enc,Dec` take time $16,384$
> - Adversary runs in time $2^{64} = 10^{18}$!
>
> If $n = 256$, then
> - `Gen,Enc,Dec` take time $65,536$
> - Adversary runtime is multiplied by $2^{64}$! Becomes $2^{128} \approx 10^{38}$.
>
> > This makes it really easy to adjust schemes to the adversary time! As adversary capabilities increase, we can shift our security parameter so that they will continue to be unable to break our scheme!

A **private-key encryption scheme** is a tuple of probabilistic polynomial-time algorithms `Gen, Enc, Dec` such that:
1. `Gen` takes security parameter $1^n$ (1 repeated $n$ times), and outputs a key $k$ denoted $k \leftarrow Gen(1^n)$. WLOG, assume $|k| \ge n$.
2. `Enc` takes a key $k$, message $m \in \{0,1\}^*$, and outpus a ciphertext $c$, $Enc_k (m) \to c$.
3. `Dec` takes a key $k$, ciphertext $c$, and outputs a message $Dec_k (c) \to m$.

> By **correctness**, we mandate that for every $n$, every $k$, and every $m$, it holds that $Dec_k (Enc_k (m)) = m$ (the scheme must be deterministic).

## Security in the Presence of an Eavesropper (EAV)
To define security under the computational approach, we think of an experiment. 

Consider a private-key encryption scheme $\Pi = (Gen, Enc, Dec)$, any adversary $A$, and any value $n$ for the security parameter. We define a random variable experiment
$$
\text{Experiment} Priv K^{eav}_{A, \Pi} (n)
$$

Where the adversary and our challenger play the following game:
1. The adversary chooses two messages $m_0, m_1$ from the message space.
2. The challenger will generate a key $Gen(1^n) \to k$ and choose $b = 0 \; \text{or} \; 1$ randomly. Based on $b$, the challenger then encrypts one of the messages $Enc_k (m_b) \to c$.
3. The adversary receives the ciphertext $c$, and now has to guess $b' \in \{0,1\}$, denoting which message they think was encrypted.
4. We check if the adversary was right, and set the random variable to 1 if the adversary was right ($b' = b$), 0 if wrong ($b' \ne b$).


We say $\Pi$ has **indistinguishable encryptions in the presence of an eavesdropper (EAV-secure)** if $\forall$ PPT adversaries $A$, $\exists$ a negligible function $negl$ such that
$$
Pr[PrivK^{eav}_{A, \Pi} (n) = 1] \le \frac{1}{2} + negl(n)
$$
In other words, **the adversary has close to a 50/50 chance of correctly guessing the message** (as there are only 2 messages to choose from), with some negligible offset that drops to 0 quickly as $n \to \infty$! This tells us that they don't really get any information about the message!
> This is a weak notion of security and is not very useful in practice!

Similar to the different definitions of perfect secrecy, computational security also has equivalent definitions-- though these other definitions are outside of the scope of this class.

### Pseudorandom Generator (PRG)
Here, we define a pseudorandom generator. These can be used to create schemes that are computationally secure, with $|K| < |M|$ (making the scheme more practical). 
> Recall that this wouldn't be possible for perfect secrecy!

A **pseudorandom generator (PRG)** is a deterministic algorithm $G$, that takes as input a short random seed $s$, and outputs a longer string $G(s)$. It has the property that no polynomial time algorithm can "distinguish" $G(s)$ from a truly random string $r$, despite being a deterministic function.

What this generator essentially does is "stretch" a small amount of true randomness ($s$) to a larger amount of pseudorandomness, without compromising on security.

To have a PRG, we also define a game. 
- **Ideal World**: We sample a truly random bit string $r$ of length $\ell(n)$, $r \in \{0,1\}^\ell$. It must hold that $\ell(n) > n$, where $\ell(n)$ is called the **expansion factor** ($G$'s output must be longer than the input).
- **Real World**: We sample a truly random bit string $s$ of length $n$, and compute $G(s)$. 
- We give either the ideal world or real world bit string to $D$, the distinguisher. For a PRG, any efficient distinguisher cannot tell which "world" the string is from (if it got $r$ or $G(s)$).

Formally, the probability that the distinguisher guesses the ideal world is about the same in either case.
$$
\left| Pr[D(r) = 1] - Pr[D(G(s)) = 1] \right| \le \text{Negligible}
$$
> This means that the distinguisher has no way of really knowing which is the ideal world! 
> 
> Here, $G$ only gets $n$ bits of true randomness, but need to "stretch" that randomness to $\ell(n)$ bits!

Given a PRG, we can only assume the following: 
- If our input random string is uniform, the PRG's output will also be uniform.

> [!Example]- Example: PRG Proof (1)
> Let $G$ be a PRG where $|G(s)| = |s| + 1$.
>
> Let $G'(s) = G(s||\bar{s})$, where $\bar{s}$ is the negation of $s$. Is $G'$ a PRG?
>
> We know that $s || \bar{s}$ is not uniformly random, as $\bar{s}$ depends on $s$. Because the input is not random, we cannot assume $G'$ is a PRG.
>
> Let's construct a pathological example. Let's construct $G$ from another PRG, $\tilde{G}$, which is a function from $\{0,1\}^n \to \{0,1\}^{2n+1}$ as so:
> $$
> G(s_1 || s_2) := \tilde{G} (s_1) || \tilde{G} (\bar{s}_2)
> $$
>
> We must show that $G$ is a PRG, and $G'$ is not a PRG. Let's start with $G$.
>
> 1. $G$ is a PRG, as if $s_1 || s_2$ forms a truly random string, then $s_1, s_2$ are random, and $\bar{s}_2$ is also random. So, $\tilde{G}$, being a PRG on a uniformly random input, outputs a uniformly random output.
> 2. $G'(s) = G(s || \bar{s}) = \tilde{G} (s) || \tilde{G} (s)$, but by the deterministic nature of PRGs, we have the same string concatenated with itself! So, the output does not have a uniform distribution.
>
> Formally, define a distinguisher $D$, which get some input $w$. We choose a polynomial time algorithm for $D$ which lets it distinguish randomness from the PRG with non-negligible probability.
>
> One algorithm $D$ could do is split the string in half, return 1 (PRG output) if the halves are the same, 0 otherwise. With this algorithm, we have the following probabilities:
> - $Pr[D(G'(s)) = 1] = 1$, as we will always be able to tell the PRG as its two halves are always the same (shown above)
> - $Pr[D(r) = 1] = \frac{1}{2^{2n+1}}$, as for any string in the first half we need to match it in the second half.
> 
> So, 
> $$
> | Pr[D(G'(s)) = 1] - Pr[D(r) = 1] | = 1 - \frac{1}{2^{2n+1}} \ge \frac{1}{2}
> $$
> This is not a negligible function, as when $n$ increases this goes to 1! So, we can define a constant function $1/2$ which this is greater than as $n \to \infty$.
>
> So, we have a $D$ that breaks the security of $G'$

Using PRGs, we can create a secure fixed-length encryption scheme that is secure, and breaks the Shannon bound. Let $G$ be a PRG taking $\{0,1\}^n \to \{0,1\}^{\ell(n)}$, $\ell(n) > n$, and let $K = \{0,1\}^n, M = \{0,1\}^{\ell(n)}$.
- `Gen` outputs a random key $k \in K$.
- `Enc` takes the key, runs it through the pseudo-random generator to get a pad $G(k) \to p \in \{0,1\}^\ell$. It then XORs the output with the message to get our ciphertext $c$.
- `Dec` reverses this by XORing the same pad with the ciphertext. 

This is a computationally-secure scheme, and $|K| < |M|$, breaking the Shannon bound! We can prove this below.

> [!Note]- Proof
> We wish to show that given $G$ is a PRG, our scheme is EAV-secure. So, $\forall$ PPT adversaries, $\exists negl$ such that
> $$
> Pr[PrivK^{eav}_{A,II} (n) = 1] \le \frac{1}{2} + negl(n)
> $$
> 
> In many cryptographic proofs, we cannot prove the definition directly. So, we prove by contradiction or contrapositive.
> 
> So, we will show that if $\exists$ PPT adversaries such that $\forall negl$,
> $$
> Pr[PrivK^{eav}_{A,II} (n) = 1] > \frac{1}{2} + negl(n)
> $$
> Then $G$ cannot be a PRG.
> 
> Let $A$ be this adversary. Then, $\exists$ PPT distinguisher such that there exists a non-negligible function $\ell'(n)$, where
> $$
> | Pr[D(r) = 1] - Pr[D(G(s)) = 1] | \ge \ell'(n)
> $$
> Given this distinguisher, we will contruct another distinguisher against the PRG, that uses $A$ as a subroutine.
> > This is based off proof reduction! The idea that if one algorithm solves the boolean satisfiability problem, then it can be used to solve all NP-complete problems in polynomial time!
> 
> - $D$ is a distinguisher that needs to take a string $w \in \{0,1\}^{\ell(n)}$, and needs to return 0, 1 guessing what world the string came from. It contains and can use $A$
> - $A$ is an adversary that will first send $m_0, m_1$ to the challenger ($D$). It expects a ciphertext, and guesses if $c$ is an encryption of $m_0$ or $m_1$.
> 
> This is almost an algorithm! We just need to fill it in with a few steps.
> 1. How does $D$ generate the challenger ciphertext for $A$?
>    - $D$ randomly chooses a $b \in \{0,1\}$, and sends back $w \oplus m_b$.
> 2. After getting the response from $A'$, $b'$, what response does $D$ output?
>    - If $b = b'$, then return 1
>    - If $b \ne b'$, then return 0
> 
> We now analyze the probabilities to show that our PRG is not actually a PRG.
> 1. The probability $Pr[D(G(s)) = 1]$ is the probability $A$ guesses correctly if $w = G(s)$. This is
>    $$
>    Pr[PrivK^{eav}_{A,II} (n) = 1] \ge \frac{1}{2} + negl
>    $$
> 2. The probability $Pr[D(r) = 1]$ is the probability that $A$ guesses the one-time pad, which (by perfect secrecy) is
>    $$
>    Pr[D(w) = 1] = \frac{1}{2}
>    $$
>    As no matter what $A$ guesses, it cannot do better or worse by perfect secrecy.
> 
> So,
> $$
> | Pr[D(G(s)) = 1] - Pr[D(r) = 1] | \ge \frac{1}{2} + \rho(n) - \frac{1}{2} = \rho(n)
> $$
> As $\rho(n)$ is non-negligible, $D$ breaks the security of the PRG. Because $A$ is a PPT, $D$ is also a PPT as it uses $A$, we are done.

However, this compuationally secure scheme is not very practical.
- The length of the message is fixed
- The scheme can only be used once, as if the same key is used twice, the scheme would no longer be secure!

### Stream Ciphers
To make something that can be used in practice, recall that for two PRGs, inputting the output of one into another will still yield a pseudo-random string! So, if we chain these PRGs together, we'll get a "stream" of unique keys we can encrypt with. 

This is the idea behind the **stream cipher**. 
- Let $G$ be a PRG that takes as input $\{0,1\}^n$ and outputs $\{0,1\}^{n+1}$.
- Let $s_0$ represent some initial state, which is a truly random key.

Both the sender and receiver will store a state, which will let them generate a pseudorandom stream of 0s and 1s to use in a one-time pad. For every application of the PRG, the 1st bit will be used for the one-time pad, and the remaining bits will be used as the next state.
$$
\begin{align*} 
s_0 = k \\
s_{i+1} = G(s_i)_2, \dots G(s_i)_{n+1} \\
\text{pad}_{i+1} = G(s_i)_1
\end{align*}
$$

Then, for some message, we can generate the ciphertext for the $i+1^{th}$ bit as
$$
c_{i+1} = m_{i+1} \oplus \text{pad}_{i+1}
$$
> Both the sender and receiver are in sync (so long as they have the same initial key), so the receiver can decrypt the ciphertext with the same pad!

Because the stream cipher does not use the same key, we have a secure scheme that can be used to send multiple variable-length messages! However, this requires that the sender and receiver are in sync-- if any bit is dropped, then they won't be in sync and the decryption will fail.

> [!Tip] Key Idea
> It's possible to use a PRG to create a practical encryption scheme, with the cavaet that the sender and receiver need to share a state!

## Chosen Plain-Text Attack Security (CPA)
Computational security was a bit of a weak and limited notion. Here, we define a notion that can actually be used in practice.
> This notion can be used for multiple messages, and is a very standard notion of security!

Consider a private-key encryption scheme `Gen, Enc, Dec`, any adversary $A$, and any value $n$ for the security parameter.

We define the following experiment, $PrivK^{cpa}_{A, II} (n)$.
1. The challenger (sender / receiver) will generate some key $k = Gen(1^n)$.
2. The adversary gets **oracle access** to the encryption algorithm, denoted $A^{Enc_k (\cdot)}$. This means that $A$ does not know $k$, but gets to use the encryption scheme. They're allowed to choose a plaintext message $m$ and get back a ciphertext $c$, for as many messages as they want (in polynomial time).
3. When the adversary has sampled enough input-output pairs, it sends two messages $m_0, m_1$ to the challenger.
4. The challenger picks a bit $b = \{0,1\}$ at random, and based on this chooses one of the messages to encrypt $Enc_k (m_b) = c$.
5. After receiving the ciphertext, $A$ gets oracle-access to the encrpytion scheme to query again.
6. When ready the adversary outputs $b'$, guessing what message the challenger chose.
7. $PrivK^{cpa}_{A, II} (n) = 1$ if $b' = b$, and 0 if $b' \ne b$.

We say our scheme has **indistinguishable encryptions under a chosen-plaintext attack (CPA-secure)** if for all PPT adversaries $A$, there exists a negligible function such that
$$
Pr[PrivK^{cpa}_{A,II} (n) = 1] \le \frac{1}{2} + negl(n)
$$

While this is a one-shot game, we can prove that CPA-security gives us security for multiple encryptions!

> [!Abstract] Theorem
> Any adversary $A$ that has indistinguishable encryptions under a CPA-attack also has indistinguishable **multiple encryptions** under a chosen plain-text attack!
>
> This means that we can use CPA-secure schemes with the same key, as many times as we want while maintaining security!

> [!Info]
> If the adversary $A$ is allowed to query the oracle, what is stopping the adversary from just querying $m_0, m_1$? They could just query $m_0, m_1$ and see what the ciphertext is!
>
> Because of this, any scheme that satisfies CPA-security **must necessarily be probabilistic**, meaning when we call the oracle, the ciphertext for any given message will be different.
>
> This motivates the following theorem.

> [!Abstract] Theorem
> If $II$ is an encryption scheme where `Enc` is a deterministic function of the key and the message, then $II$ cannot be CPA-secure.
>
> > [!Note]- Proof
> > 
> > Let $A$ be an adversary.
> > 1. $A$ chooses two messages $m_0, m_1, m_0 \ne m_1$. 
> > 2. $A$ query its oracle $m_0$ to get $c_0$.
> > 3. $A$ sends $m_0, m_1$ to the challenger and gets back $c$.
> > 4. If $c_0 = c$, $A$ predicts $b' = 0$. Otherwise, $A$ predicts $b' = 1$.
> > 
> > Clearly, $A$ is efficient as it only queries the oracle once, which is polynomial.
> > 
> > Furthermore, $A$ will always win the game with probability 1, which is greater than $1/2 + negl(n)$.

### Pseudorandom Functions
> We will use pseudorandom functions to create schemes that are CPA-secure! As it does not make sense for a fixed function to be pseudorandom, we will define pseudorandomness on our **selection from a set of fixed functions**.

A **keyed function** $F : \{0,1\}^* \times \{0,1\}^* \to \{0,1\}^*$ ($F_k(x)$) is a two-input function, where
1. The first input is the **key**, denoted $k$.
2. The second input is $x$.

We say $F$ is **efficient** if there is a polynomial-time algorithm that can compute $F(k,x)$ given $k$ and $x$. We will only be interested in efficient pseudo-functions.
> $F(\cdot, \cdot)$ is **public** and polynomial-time efficient.

Let $D$ be a PPT distinguisher. We define the following experiment:
1. $D$ gets access to an oracle $O$ which is either equal to $F_k$ ($k$ chosen at random) or $f : \{0,1\}^n \to \{0,1\}^n$, a uniformly chosen random function. ($D$ does not know which is the case). 
   - $f$ is a function with input set $\{0,1\}^n$, and for each input one output in $\{0,1\}^n$. Then, to choose $f$ uniformly at random, uniformly assign one output from $\{0,1\}^n$ to each input. After being chosen, it then behaves deterministically.
2. $D$ may query the oracle for any $x$, at which point the oracle returns $O(x)$.
   - Because the oracle computes a deterministic function, it returns the same result if queried twice on the same input.
3. $D$ may interact freely with the oracle, denoted $D^{O(\cdot)} (1^n)$, choosing its queries based on the outputs (as long it runs in polynomial time).
4. $D$ returns 1 if it thinks the oracle is our pseudorandom function $F_k(x)$, 0 otherwise.

Then, a keyed function $F : \{0,1\}^* \times \{0,1\}^* \to \{0,1\}^*$ is **pseudorandom** if for all PPT distinguishers $D$, there exists a negligible function such that
$$
| Pr[D^{F_k(\cdot)} (1^n) = 1] - Pr[D^{f(\cdot)} (1^n) = 1] | \le negl(n)
$$
In other words, for any polynomial-time distinguisher, the probability that the distinguisher guesses that our function is the pseudorandom function (1) is negligible.
> $F_k$, for uniform key $k$, is indistinguishable from a function chosen uniformly at random from the set of all functions with the same domain and range ($f(\cdot)$). 

To disprove that a function is a PRF, the question is: can we find a set of inputs whose outputs are correlated? 

> [!Example] Example: Pseudo-Random Functions (Disproof)
> Let $F$ be a PRF. For $F' : \{0,1\}^{n-1} \to \{0,1\}^{2n}$, show if $F'$ is a PRF.
> $$
> F'_k (x) = F_k (0||x) || F(x||1)
> $$
> Suppose we plug in the following values of $x$.
> $$
> \begin{align*}
> F'_k (0^{n-1}) = F_k (0^n) || F(0^{n-1} 1) \\
> F'_k (0^{n-2} 1) = F_k (O^{n-1} 1) || F_k (O^{n-2} 1^2)
> \end{align*}
> $$
> 
> Notice how the second half of the first input, and first half of the second input are the same! Thus, these two inputs have correlated outputs, and the distinguisher could use this fact to determine if it has the PRF or not. It can query these two inputs, and return 1 if these halves are the same!
> 
> With this attack,
> $$
> | Pr[D^{F_k(x)} (1^n) = 1] - Pr[D^{f(x)} (1^n) = 1] | = \left| 1 - \frac{1}{2^n} \right|
> $$
> > The probability for the truly random function comes from the fact that we need all $n$ bits of half of the second output to match the first, and under a uniform distribution, this is probability $1/2^n$.


> [!Example] Example: Pseudo-Random Functions (Proof)
> Let $F$ be a PRF. For $F' : \{0,1\}^{n-1} \to \{0,1\}^{2n}$, show if $F'$ is a PRF.
>
> $$
> F'_k (x) = F_k (0||x) || F(1||x)
> $$
> This is a PRF! To see why, think of the input/output table for $F'_k$.
> 
> Because of the bit in front, we're partitioning the input space of $F_k$! So, there will never be any collision where the same query $x$ yields correlated outputs. Thus, this PRF is secure. 
> > Show that the space of inputs to $F$ are partitioned, and as $F$ is a PRF there will be no collisions. An intuitive argument is acceptable for this course.


### CPA-Security with PRFs
Like with PRGs, we will now use PRFs to construct a CPA-secure scheme.

Let `Gen` output a random key $k$, chosen uniformly randomly. Also, let $F_k (x)$ be a pseudorandom function.
1. Choose a random string $r \in \{0,1\}^n$. 
2. Use the random string $r$ with $F_k (x)$ to create a pad, $F_k (r) = w$. 
3. With this pad, XOR it with our message to get $c_2$. Let $c_1$ be our random string. Then, our ciphertext is given as $c = c_1 || c_2$.
   - We need the random string in the ciphertext to be able to decrypt our message.

> Intuitively, this is secure because despite knowing $r$, we don't know $k$, and the security of PRFs guarantee that without knowing $k$, we cannot differentiate $F_k (x)$ from a random function!

> [!Abstract] Theorem
> If $F$ is a pseudorandom function, then the construction above is a CPA-secure private-key encryption scheme for messages of length $n$.
>
> > [!Note]- Proof
> > 
> > We will prove this via contrapositive (as typical of these proofs). Suppose the construction above is not CPA-secure. Then, $\exists$ some PPT $A$ and non-negligible function $\rho$ such that
> > $$
> > Pr[PrivK^{cpa}_{A,II} (n) = 1] \ge \frac{1}{2} + \rho(n)
> > $$
> > We wish to show that $F$ is not a pseudo-random function. In other words, that $\exists PPT$ distinguisher and non-negligible function $f'$ such that
> > $$
> > | Pr[D^{F_k'(\cdot)} (1^n) = 1] - Pr[D^{f'(\cdot)} (1^n) = 1] | \ge f'(n)
> > $$
> > 
> > Define a distinguisher $D$, who has $A$ within it. $D$ is playing a PRF game; $A$ is playing a CPA-security game.
> > - $D$ gets an oracle $O$, talks to the oracle, and returns 0/1 indicating if it thinks the oracle is the PRF.
> > - $A$ can make queries to the oracle, sends $m_0, m_1$ to get $c$, makes queries again, and then guesses 0/1 indicating what message it thinks $c$ is from.
> > 
> > So, $D$ would do the following:
> > 1. First, $D$ gets an oracle $O$ which is either $F_k$ or $f$.
> > 2. $D$ will now choose a random string $r \in \{0,1\}^n$.
> > 3. $A$ will be allowed to query the encryption scheme as needed. To query, $D$ will take $A$'s message, query $O(r)$, and return $(r || m \oplus O(r))$ to $A$.
> > 4. $A$ now take $m_0, m_1$, and send them to $D$.
> > 5. $D$ will randomly choose $b \in \{0,1\}$, choose a random message based on this, and encrypt this as shown above. It sends this back to $A$.
> > 6. $A$ will return an answer $b'$. If $b' = b$, then output 1. Otherwise, output 0.
> > 
> > In the case that $O = F_k$, 
> > $$
> > Pr[D^{F_k} (1^n) = 1] = Pr[PrivK^{cpa}_{A,II} (n) = 1] \ge \rho(n)
> > $$
> > As it is the same probability as when $A$ guesses correctly.
> > 
> > In the case that $O = f$, 
> > $$
> > Pr[D^{f} (1^n) = 1] = Pr[Bad] + (1 - Pr[Bad]) \frac{1}{2} \le Pr[Bad] + \frac{1}{2} \le \frac{q(n)}{2^n} + \frac{1}{2}
> > $$
> > As this is the one-time pad game with probability 1/2, but there is exactly 1 case where $A$ can guess correctly, which is if the same $r$ is chosen when generating the challenger ciphertext and in a CPA-query. In this event, $A$ guesses correctly 100% of the time. 
> > > $q(n)$ stands for the number of CPA queries, and gives us a bound on this event happening.
> > 
> > $$
> > | Pr[D^{F_k} (1^n) = 1] - Pr[D^{f} (1^n) = 1] | \le \frac{1}{2} + \rho(n) - \frac{1}{2} - negl
> > $$
> > And as a non-negligible minus a negligible is non-negligible, this is $\le$ some non-negligible function. Thus, our function is not a PRF.

### Pseudo-Random Permutations
A **pseudorandom permutation** is exactly the same as a pseudorandom function, except that for every key $k$, $F_k$ must be a permutation and it must be indistinguishable from a random permutation.

Permutation means, every function $F_k$ is a bijection! So, on the truth table, every input $x$ has a 1-1 mapping to a unique output, where every output has an input!

So, for the input-output table, each output $y \in \{0,1\}^n$ appears exactly once!
> This means that pseudo-random permutations are invertible! Furthermore, if you know the key, it should be possible to efficiently invert it!

Using pseudo-random permutations, we can define the following scheme.

1. The challenger chooses a random key $k$ from the key-space. This chooses a pseudo-random permutation.
2. The adversary gets oracle $O$, which is either the pseudo-ranodm permutation $F_k$, or a truly random permutation $f(x)$. 
   - A truly random permutation is one where for each output $y$, it randomly gets assigned to one input $x$!
3. The adversary can query the oracle in the forward and backward direction, which is either $f(x), f^{-1} (y)$, or $F_k (x), f^{-1}_k (y)$. 
4. The adversary guesses what function the oracle is. 

A **strong pseudo-random permutation (PRP)** is one in which any efficient adversary cannot tell which world the oracle belongs to.
$$
| Pr[A^f () = 1] - Pr[A^{F_k ()} () = 1] | \le negl
$$
> There are $(2^n)!$ possible permutations from $\{0,1\}^n \to \{0,1\}^n$.

Previously, we created a CPA-secure encryption scheme for 1 block messages. We can now use PRPs to create a scheme that can encrypt multiple blocks!

Let message $m$ have the following blocks $m_1, m_2, m_\ell$. How can we encrypt this message?
- One way we could do this is by running the 1-block scheme $\ell$ times! This is okay in terms of security, but wastes a lot of resources!
   - We need to generate a random key every time, which could be costly
   - Every block needs the random ciphertext concatenated with it, doubling the size of each ciphertext block! This uses a lot of data. 

The various ways we can use PRPs to encrypt blocks of messages are known as **modes of operation**. They are described below.
1. **Electronic Code Block (ECB)**: Encrypt each message block with the PRP, and concatenate them together.
   $$
   F_k (m_1) || F_k (m_2) || F_k (m_3) || \dots
   $$
   To decrypt, simply run the inverse of the function on each ciphertext block.
   $$
   F^{-1}_m (c_1) || F^{-1}_m (c_2) || F^{-1}_m (c_3) || \dots
   $$
   > This is not a secure scheme, as it will give us the same output for the same input. However, it is intuitive and makes a lot of sense!

2. **Cipher Block Chaining (CBC)**: Start with some initialization vector $IV$, a truly random bit-string. Then, for every block, we can compute its ciphertext as 
   $$
   F_k (m_i \oplus c_{i-1}) = c_i \qquad c_0 = IV
   $$
   In other words, to get our next ciphertext, we XOR the block with the previous ciphertext and run it through the PRP. 
   
   To decrypt, run the inverse on the ciphertext, and XOR it with the previous ciphertext.
   $$
   F^{-1} (c_i) \oplus c_{i-1} = m_i
   $$

3. **Output Feedback (OFB)**: Start with some initialization vector $IV$. Then, to generate the ciphertext, we will first generate keys by repeatedly running the $IV$ through the PRP.
   $$
   F_k (z_{i-1}) = z_i \qquad z_0 = IV
   $$
   Then, we XOR the key with our message block to get our ciphertext.
   $$
   z_i \oplus m_i = c_i
   $$
   To decrypt, we repeat the key-stream and XOR each key with the ciphertext.
   $$
   z_i \oplus c_i = m_i
   $$
   
4. **Counter (CTR)**: Start with some random number which will serve as a counter, $ctr$. Then, to generate the ciphertext, we will run $ctr + i$ through the PRP and XOR the output with the message. Increment counter after each message block.
   $$
   F_k (ctr + i) \oplus m_i = c_i
   $$
   To decrypt, we repeat the same process.
   $$
   F^{-1}_k (c_i) \oplus (ctr + i) = m_i
   $$

2,3,4 all achieve similar levels of security!

> In looking at each mode, we should also think about if the mode is parallelizable!
