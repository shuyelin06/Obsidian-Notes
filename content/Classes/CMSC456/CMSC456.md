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
