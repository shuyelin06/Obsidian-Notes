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

# Symmetric Key Encryption (Ciphers)

One of the driving principles behind symmetric key encryption is as follows:

> [!Tip] Kerckhoffs' Principle
> A good cipher scheme should be able to be public, without adversaries being able to use it to decrypt messages. To do this, both parties share a secret key for encryption / decryption which adversaries are assumed to not know. 

We always have to assume that the crypto designs are public! This is more suitable for large-scale usage of cryptography, and exposes schemes to the public eye so that they can be revised and strengthened. 

## Historical Ciphers
For each of the following historical schemes, we will discuss the encryption algorithm, the decryption algorithm, the key-space (set of all possible keys) and secret key, and how to break the scheme.

### Atbash Cipher
The **Atbash Cipher** substitutes the first letter with the last, the 2nd with the 2nd last, and so on. To encrypt and decrypt, simply swap the letters.

Because there is nothing that is secret, there is no key for this algorithm. 

### Shift / Caesar Cipher
The **Caeser Cipher** replaces each letter by the letter which is $n$ positions away in the alphabet. On a message, this has the effect of "shifting" every letter $n$ positions in the alphabet.

As there are 26 letters in the alphabet, there are 26 possible shifts we could do. Thus, our key-space has a size of 26.

Because the key-space is so small, we can easily brute-force this cipher by trying all possible shifts! Thus, this cipher is suspectible to a **brute-force search**.
> For a secure scheme, it's necessary that the key space is large! However, a large key space does not imply security.

### Scytale Cipher
The **Scytale Cipher** stacks letters of the message into $n$ equal-sized rows. Reading the message column-by-column will give you the ciphertext (encryption), and reading the message row-by-row will give you the plain-text (decryption).

As we could have a nearly infinite number of rows, the key-space is arbitrarily large! 

That does not make this cipher secure however, as we may be able to recover the key! Starting from the first letter, we can take letters that are offset $i$ positions from the start, to try to form a word. Once we get something that makes sense, we'll have recovered our key!
> Information about our ciphertext can let us reverse engineer the key!

### Monoalphabetic Substitution
The **Monoalphabetic Substitution** maps every plaintext letter to a different ciphertext character, and substitutes them as so. Using this map, we can encrypt and decrypt our message.

The size of our key-space is $26!$, which is really large! So, brute force search is not possible, but because of the 1-1 mapping, we could do a **frequency analysis** to recover the key! 

> [!Info] Frequency Analysis
> Frequency analysis is based off the fact that letters in (gramatically correct) English generally have different usage frequencies. If we know the frequencies of the ciphertext characters, we can guess what the mappings are.

---

## Definitions
### Symmetric Encryption Scheme
Here, we define notation for a symmetric encrpytion scheme.

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

### Perfect Secrecy
We say an encryption scheme over a message space $M$ is **perfectly secret** if $\forall$ probability distributions over $M$, $\forall m \in M, \forall c \in C$ such that $Pr[C = c] > 0$,
$$
Pr[M = m | C = c] = Pr[M = m]
$$
In other words, the probability that our message is $m$ does not change even if we know what the ciphertext $c$ is. Sometimes, we denote $Pr[M = m]$ as the **a priori** distribution, and $Pr[M = m | C = c]$ as the **a posteriori** distribution.
> Thus, even if the adversary sees $c$, this does not change any of their knowledge about the message space!

> [!Abstract] Lemma 1
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

> [!Abstract] Lemma 2: Perfect Indistinguishability
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

## The One-Time Pad
The One-Time Pad is a symmetric encryption scheme. It works as so:
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
> > [!Note] Proof
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

End of lecture ---

> [!Example] 
> $M = \{0,1, \dots n-1\}$, $K = \{0,1,\dots n-1\}$. Gen() chooses a key at random from $K$, $Enc_k(m) = m + k$, $Dec_k (c) = c - k$. Is this perfectly secret?
>
> No. BWOC, suppose it is. Let $n = 20$, and let $M$ have the uniform distribution, and let $m = 10, c = 5$. Then,
> $$
> Pr[M = 10 | C = 5] = 0 \ne Pr[M = 10] = \frac{1}{20}
> $$

> [!Abstract] Shannon's Theorem
> Say we have encryption scheme with message space $M$, for which $|M| = |K| = |C|$. The scheme is perfectly secret if and only if: 
> 1. Every key $k \in K$ is chosen with equal probability $1 / |K|$ by algorithm `Gen`.
> 2. For every $m \in M$, $c \in C$, there exists a unique key $k \in K$ such that $Enc_k (m) \to c$.
>
> > [!Note] Proof
> > 

