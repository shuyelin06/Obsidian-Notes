---
title: Standard Representations
tags:
- graphics
- wip
---

The real world is complex, and it simply has too much detail for us to be able to simulate it with 100% accuracy (especially if we want fast graphics programs!). Thus, we need to make approximations of it, which make assumptions and have restrictions.

Here, we describe many of the assumptions and approximations commonly made in the field of graphics.

# Evaluating Representations
In nearly all cases, there are a variety of representations of some phenomena that conflict with each other, and have various properties. Thus, it may be natural to ask, which one is best for our purposes?

Some important factors to consider when evaluating these representations are given below.
- **Physical Accuracy**: In many cases, we want our representations to be as realistic as possible, and we can easily measure this using well-known benchmarks.
- **Perceived Accuracy**: At the end of the day, humans will be seeing our graphics, and human perception is limited. Thus, it's important to consider how accurate our representation is perceptually to a human, though this can be difficult to measure.
- **Design Goals**: A good representation is one that best communicates to the user for its intended purpose. Oftentimes, simplification is better to better communciate ideas.
- **Space/Time Efficiency**: A good representation should be memory and time efficient.
- **Implementation Complexity**: We want to actually be able to implement our models, and development takes time! 

> [!Tip] Quantification is Key
> For all factors, a good rule of thumb is that if we want to improve something, we need some way to quantify this factor. This way, we have a benchmark that we can use to measure improvements in our target factor!


# Real Numbers
In many areas of computer science, we often assume that we can represent real numbers with enough precision for the purposes of the application. 

This is not the case in graphics - and often, we find ourselves close to this limit of precision, which can cause visible errors. Thus, it's important to consider how we actually approximate real numbers to understand the implications of these approximations.

## Approximating Real Numbers
In computer graphics programs, we most commonly use the following versions of real number approximations: **fixed point**, **normalized fixed point**, and **floating point** approximations. 
