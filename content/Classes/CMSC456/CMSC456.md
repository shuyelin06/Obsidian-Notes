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
