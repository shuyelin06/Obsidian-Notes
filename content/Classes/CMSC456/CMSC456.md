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

> [!Example]+ Example: MAC Disproof
> Suppose we have a MAC, where for mesage $m = m_1 || \dots || m_\ell$, $m_i \in \{0,1\}^n$, choose $r \in \{0,1\}^n$ at random and compute $t = r || F_k (m_1 \oplus r) || \dots || F_k (m_\ell \oplus r)$.
> 
> This is, in fact, not a secure MAC. We can show this below. 
> 
> Let $A$ be an adversary which does the following:
> 1. Suppose we have some message $m$ we want to authenticate. Query the oracle to get the tag $t$.
> 2. From the tag $t$, take random bit-string $r$ in the beginning.
> 3. Now create forgery, where $m'$ is the message where each block of the message is XORed with $r$ from above. Let $t'$ be the tag where $0$ is our random bit-string, with $t$ after. 
> 
> This is a valid forgery, which gives us a non-negligible probability of breaking the MAC!

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

### Domain Extension for MACs
Let's see how we can extend MACs for variable-length MACs.

Suppose we have a MAC $\Pi$, which works for fixed-length messages of length $n$. For a message of any length,
$$
m = m_1 m_2 \dots m_\ell
$$
How can we generate a tag for this message?

> [!Warning] Naive Extension
> One way we could do this is by running each block of the message through the MAC to get a tag for each block. 
>
> Unfortunately, this is not secure. This is because there's nothing "tying" the blocks of the messages together-- so, an adversary can easily reorder the blocks to break the security of the scheme.

Let's see some ways we can extend the MAC.

---

**CBC-MAC**: We generate one tag by running each message through $F_k$, XORing the result with the next message, and repeating this process. Formally, 
$$
\begin{align*}
&c_1 = F_k (m_1) \\
&c_2 = F_k (m_2 \oplus c_1) \\
&c_3 = F_k (m_3 \oplus c_2) \\
&\vdots \\
&t = c_\ell = F_k (m_\ell \oplus c_{\ell - 1})
\end{align*}
$$

This is secure only if the message and forgery are both required to have a fixed length $\ell$! If these conditions are relaxed, we can perform a **length extension attack** to break the security of the MAC-- let's see how below. 

> [!Example] Example: Length Extension Attack
> Suppose the message and forgery are not required to have block-length $\ell = 6$. Then, let $A$ be the adversary who queries two messages $m_1, m_2$ of length 3 blocks each. $A$ will use these messages to then generate a forgery on a 6 block message $m' = m_1' m_2' m_3' m_4' m_5' m_6'$.
> 1. $A$ can query $m_1 = m_1' || m_2' || m_3'$, to get tag $t_1$.
> 2. Then, $A$ can query $m_2 = (m_4' \oplus t_1) || m_5' || m_6'$ to get tag $t_2$.
> 3. This tag is our forgery! Return forgery $(m', t')$ where $t' = t_2$.
>
> This creates a forgery that breaks the security of our MAC!

> This happens because we're allowed to query the oracle on a prefix of the previous message. This relation breaks the security.

To fix CBC-MAC, we will first instead start the MAC not on $m_1$, but on some **prefix-free encoding**. This is a scheme that maps an input message into a space of valid code-words, where for any two valid code-words, one does not prefix the other. 

One easy way to do this is by encoding the length of the message! So, CBC-MAC would do the following:
$$
\begin{align*}
&c_0 = F_k (\text{Length of m}) \\
&c_1 = F_k (m_1 \oplus c_0) \\
&c_2 = F_k (m_2 \oplus c_1) \\
&\vdots \\
&t = c_\ell = F_k (m_\ell \oplus c_{\ell - 1})
\end{align*}
$$
> The prefix-free encoding ensures that messages cannot prefix each other in the MAC scheme!

Essentially, what we are doing is prepending an extra message block to the message, which indicates its length.


# Authenticated Encryption
## CCA Security
We've seen a secure way to encrypt our message for security, and a secure way to authenticate our message for integrity. Now, let's tie the two together!

**Chosen Ciphertext Attack (CCA) Security** is a standard security notion, which is even stronger than CPA security. We define the following game.

Consider a private-key encryption scheme $\Pi$, some adversary $A$, and security parameter $n$. Define the following experiment
$$
PrivK^{cca}_{A,\Pi} (n)
$$

1. The challenger generates a key $Gen(1^n) = k$.
2. The adversary gets oracle access to both the encryption and decryption algorithm, $A^{Enc_k, Dec_k}$. They can query messages to get ciphertexts, and ciphertexts to get messages.
3. The adversary chooses 2 messages, $m_0, m_1$ and sends them to the challenger.
4. The challenger chooses one of the messages at random, $b \in \{0,1\}$, encrypts it, and sends the ciphertext $c$ of $m_b$ back.
5. The adversary can again query the encryption and decryption oracle. When ready, it returns $b'$ guessing what message was encrypted.
   - To make sure this game is possible, in this step, the adversary is NOT allowed to query challenge ciphertext $c$ to the decryption oracle. It can query anything else though, as long as it is not $c$. We'll denote this slight limitation as $A^{Dec_k^*}$
6. The experiment is 1 if $b' = b$, 0 otherwise.

We say $\Pi$ has **indistinguishable encryptions under a chosen-ciphertext attack (CCA secure)** if $\forall$ PPT adversaries $A$, $\exists$ a negligible function $negl$ such that
$$
Pr[PrivK^{cca}_{A,\Pi} (n) = 1] \le negl
$$
> This is a really strong notion of security! 

Authenticated encryption schemes satisfy this type of security, by using MACs to tag the ciphertext for authentication. Then, $Dec$ throws an error if it detects an invalid ciphertext. By doing this, the adversary can only decrypt the ciphertexts its seen, and can't make its own!
