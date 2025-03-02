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

# Message Integrity
In the previous section, we discussed how to create a secure encryption scheme. However, security is not everything! Even without knowing the original message in the previous schemes, attackers can still modify the message with no way for the sender / receiver to tell.

In other words, there's secrecy, but not **integrity**! In this section, we will discuss how we can create schemes that maintain integrity.

# Message Authentication Codes (MAC)
## Secure MACs
Suppose we have a sender, receiver, and eavesdropper, where only the sender and receiver have knowledge of the $k$. Say the sender doesn't care about security, and just wants the receiver to be able to verify that the message came from them, and was not modified in transit. How can they do this?

They do this using a **message authentication code (MAC) scheme** $\Pi = Gen, Mac, Vrfy$. 
1. Both the sender and receiver share a key randomly generated with `Gen`.
2. The sender runs a **MAC Algorithm $Mac_k (m)$**, which generates a tag $t$ that can be used for authentication. 
3. The sender sends the message and tag together, $(m,t)$, to the receiver. 
4. The receiver runs a **Verification Algorithm $Vrfy_k (m,t)$**, which returns 1 (valid) or 0 (invalid) indicating if the message was sent by the sender or not (based on if the tag matches the message). 

> **Corectness** guarantees that $Vrfy_k (m, Mac_k(m)) = 1$. In other words, the verify algorithm should always work if the message truly wasn't modified. 

Like before, we will formalize this scheme with an experiment
$$
\text{Experiment} \; MACforge_{A,II} (n)
$$
Let $\Pi$ be a MAC scheme, $A$ be an adversary, and $n$ be the security parameter. Let the challenger play the part of the sender / receiver.
1. The challenger first generates a random key $Gen(1^n) \to k$.
2. $A$ gets oracle access to the MAC algorithm, $A^{Mac_k (\cdot)}$. In other words, they can query any message they want, and get back a tag for that message. Let $Q$ be the set of all messages $m'$ queried by $A$.
3. $A$ tries to forge the message authenticity, by sending message and tag pair $(m,t)$ to the challenger.
4. The adversary wins, $Macforge_{A,II} (n) = 1$, if:
   - $m \not\in Q$. In other words, the adversary did not query and get the tag for $m$ (if they queried $m$, this is known as a **replay attack**, which has to dealt with separately in practice).
   - $Vrfy(m,t) = 1$. In other words, the challenger was tricked into finding the tag matches the message

We say $\Pi$ is **existentially unforgeable under an adaptive chosen message attack** if $\forall$ PPT $A$, $\exists$ negligible function $negl$ such that
$$
Pr[Macforge_{A,II} (n) = 1] \le negl(n)
$$
Note that unlike security, this probability must be less than negligible probability, not $\frac{1}{2} + negl$.
> For shorthand, we will just say the scheme is **secure** in this case.

> [!Info] Strong Security
> There's also a stronger notion of security for MAC schemes, which we'll call **strong security**. In this case, $Q$ is the set of all **message, tag pairs** $(m',t')$, and the adversary wins if 
> - $(m,t) \not\in Q$
> - $Vrfy_k (m,t) = 1$
>
> In other words, the adversary is allowed to replay a message, as long as the tag is different.
> > In practice, we don't worry about this too much as the schemes we use are deterministic, so there's only one valid tag per message (so strong security and normal security are the same).

## Constructing Secure MACs
We can construct secure MACs using pseudorandom functions! 

### Fixed-Length Messages
Let $F$ be a pseudorandom function. We define a fixed-length MAC for messages of length $n$ as follows:
- `Gen`: Outputs a random key $k$.
- `Mac`: For key $k$ and message $m$, output $F_k (m) = t$.
- `Vrfy`: For key $k$, message $m$, tag $t$, output 1 if and only if $t = F_k (m)$.

> This only works for fixed-length messages. Later, we'll use this to create schemes that work for variable length messages.

> [!Abstract] Theorem: MAC Security
> If $F$ is a PRF, then the construction above is a secure fixed-length MAC for messages of length $n$.
>
> > [!Note]- Proof
> > 
> > By contrapositive, suppose the construction is not a secure MAC. So, there exists a PPT adversary $A$, non-negligible function $\rho$, such that
> > $$
> > Pr[MACforge_{A,\Pi} (n) = 1] \ge \rho
> > $$
> > 
> > We must show that there exists a distinguisher $D$ such that
> > $$
> > | Pr[D^{f(\cdot)} (1^n) = 1] - Pr[D^{F_k(\cdot)} (1^n) = 1] | \ge \rho'(n)
> > $$
> > For non-negligible function $\rho'(n)$.
> > 
> > Let $D$ do the following, playing the PRF experiment.
> > 1. Let $D$ get the oracle, which is either random function $f$, or $F_k$.
> > 2. $D$ gives $A$ oracle access. For any MAC query from $A$, $D$ forwards messgae $m$ to the oracle to get $t = O(m)$ and sends it back to $A$.
> > 3. When ready, $A$ sends $(m^*,t^*)$ to $D$ as a forgery. 
> > 4. $D$ checks if $m^* \in Q$, output 0. If $m^* \not\in Q$, forward $m^*$ to the oracle and check if $O(m^*) = t^*$. If so, output 1, 0 otherwise.
> > 
> > Note that $D$ is running $A$, so $D$ is running in PPT. We have the following probabilities.
> > $$
> > \begin{align*}
> > Pr[D^{F_k(\cdot)} (1^n) = 1] = Pr[MACforge_{A,\Pi} (n) = 1] \ge \rho(n) \\
> > Pr[D^{f(\cdot)} (1^n) = 1] \le \frac{1}{2^n} \\
> > | Pr[D^{f(\cdot)} (1^n) = 1] - Pr[D^{F_k(\cdot)} (1^n) = 1] | \ge \left| \rho(n) - frac{1}{2^n} \right|
> > \end{align*}
> > $$
> > 
> > Which is non-negligible. Thus, $F$ is not a PRF.

### Variable Length Messages
TODO...
