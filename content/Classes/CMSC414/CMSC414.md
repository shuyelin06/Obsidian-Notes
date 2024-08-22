---
title: CMSC414
tags:
- cmsc414
---

This course provides a survey of computer and network security. 

Computer security is a very large field; too large for a single course to cover. This course dives into some topics in depth, as a good introduction to the field. 

Before discussing these, it's important to first define some terminology for later use.

# Security Terminology and Properties
It's important for us to define the following terminologies before discussing security.

First, we define a **system** as any group of protocols/designs, software, hardware, infrastructure, and people. Our goal is to build systems that are robust and secure.

## Security Properties
We cannot design or evaluate these systems, however, without first defining what **properties** we want- things that we want to guarantee against some sort of **threat model (adversary)** against our system.

The three most traditional security properties are given as follows:
- **Confidentiality**: Protecting data from unauthorized access.
- **Integrity**: Assuring that data has not been modified.
- **Authenticity**: Integrity and **freshness**, a guarantee that data was generated within a certain timeframe.

> [!Example] Example: Techniques for Security Properties
> To provide these properties, we can use a variety of techniques! These can include but are not limited to:
> - Encryption
> - Digital Signatures
> - Hashes

The following are relatively more recent security properties which are also quite common today:
- **Privacy**: Control over your own data- information about you. 
- **Anonymity**: Control over your own metadata- what you're doing and who you're interacting with.
- **Availability**: Ability for legitimate users to access a system.

> Metadata is really just another type of data! They just pertain to different types of data.

We also need to consider the location of data. 
- Data **in motion** (on the wire): Data that is transmitted rapidly, and likely has short-term value.
- Data **at rest** (on the disk): Data that is stored for long periods of time, but has long-term value. 

So to provide security properties for sytsems, it's important to know what we're doing with the data, as well as what we need to protect.

## Threats and Vulnerabilities
It's also important to understand the **threats** to our system. Different systems have different threats, with differing motivations and goals. Understanding what type of threat is targetting our system is very important in defining what type of security properties we want.
- **Nation States**: Major countries with their own intelligence services. Highly capable organizations that serve to fulfill their countries' geopolitical agendas.
- **Criminal Organizations**: Large, well-funded organizations that are similar in magnitude to nation states, but may have differing agendas.
- **Hacktivists**: Not very well funded groups, with highly varying skill levels that bring together like-minded people to amplify their attacks.
- **Glory Hounds / Bored Hackers**: Threats who exist just for the publicity. Generally not very sophisiticated.
- **Script Kiddies**: People who are not technically competent, and use off the shelf tools without knowing how they work. 
- **Insiders**: Threats inside the target orgnization. 

> Insiders are the number 1 type of threat actor!!

## Types of Vulnerabilities
The following are some types of vulnerabilities commonly found in systems. They are elaborated on more later:
- **Programming Errors**: One of the most common. Any error that creates a vulnerability.
- **Improper Use of Crptography**: Use of cryptography does not guarantee security of a system. 
- **Misplaced Trust**: Trust placed in an individual or system that may lead to an insider threat.
- **Imbalanced Economic Motivations**: Those left to maintain the security of a system could be bribed to do otherwise. 
- **Incorrect Assumptions**: Assumptions that lead to an overlooking of one of the previous vulnerabilities. 

## System Participants
Within a system, we have the following definitions: 
- **Subject**: A person who is a part of the system. 
- **Principal**: People (subjects) of the system as well as any piece of the system that makes it up (technology, data, etc.). Often, a subject participates **indirectly** in a system through another principal.
- **Identity**: Defines if two principals are the same.
- **Group**: A set of principals. Principles are added to groups, which remain fairly static.
- **Role**: A set of functions or permissions. Can be assigned dynamically to principles for more fluid configurations.


