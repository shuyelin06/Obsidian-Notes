---
title: Cryptography
tags:
- cmsc414
---

There are two main goals of cryptography:
- Keep secrets a secret (confidentiality, privacy, anonymity)
- Ensure that data is correct (integrity, authencity)

We survey the landscape of cryptography below.

# Introduction to Cryptography
## Principles
For any crypto system, there are some general principles to follow. 

**Kerckhoff's Principle** states that a cryptosystem should be secure even if everything about the system, except the key, is public knowledge.

**Schneier's Law** states that any person can invent a security system so clever that he or she can't imagine a way of breaking it.

There is no security through obscurity! It's important to have many people try to break through a system based on a full knowledge of it. Just because you think its unbreakable, does not mean it really is unbreakable.
> Don't trust any system that is not public! These systems are not vetted.

## Terminology
Cryptography and related topics all have terminology of their own. This is discussed below.

One of the goals in cryptography is **keeping secrets**. This means that we want to be able to replace some or all of our message with something else, while being able to recover the original.
- **Encoding** refers to the replacement of a semantic unit (word, phrase) with something else
- **Enciphering** refers to replacing individual letters or bits with something else
- **Plaintext / Cleartext** refers to a message as written and intended to be read
- **Ciphertext** refers to a transformation of a plaintext so that it cannot be read, other than the intended recipient




