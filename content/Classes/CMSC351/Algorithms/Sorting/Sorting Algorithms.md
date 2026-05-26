---
title: Sorting Algorithms
tags:
- cmsc351
---

**Problem**: Given an array of elements, how can we **sort** this array of elements?

We define a **sorted array** as an array such thtat for every two consecutive elements in the array $E_1, E_2$,
$$
E_1 \le E_2
$$

Here, we discuss various algorithms we can employ to sort an array we're given.

# Sorting Algorithms
## Properties of Sorting Algorithms 
Sorting algorithms all have pros and cons compared to one another.

We will be analyzing each sorting algorithm based on their time and space complexity, as well as their **stability** and **in-place** property, described below.

> [!Info] Stability
> Say we have two equal values $E_1, E_2$, where $E_1$ is to the left of $E_2$.
> 
> A sorting algorithm is **stable** if the relative positions of these values do not change relative to one another when the algorithm ends. Otherwise, the algorithm is **unstable**.

> [!Info] In Place
> A sorting algorithm is **in-place** if the algorithm operates on the list itself.

## Comparison Based Sorting Algorithms
In this section, we discuss various algorithms we can use to sort our array, which use comparisons to achieve our objective.

These algorithms are given below.
- [[Bubble Sort]]
- [[Selection Sort]]
- [[Insertion Sort]]
- [[Merge Sort]]
- [[Heap Sort]]
- [[Quick Sort]]

However, regardless of how we choose to sort with comparisons, the use of comparisons limit the algorithms! We discuss this more in [[Limitations of Comparison-Based Sorting Algorithms]].

## Non-Comparison Based Sorting Algorithms
In this section, we discuss alternative algorithms we can use to sort our array, which do not use comparisons to achieve our objective. Because of this, under certain conditions, these algorithms can achieve worst case time complexities faster than $\Theta(n \lg(n))$!

These algorithms are given below.
- [[Counting Sort]]
- [[Radix Sort]]

