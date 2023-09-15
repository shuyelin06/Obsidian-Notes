---
title: Sorting Algorithms
---

Oftentimes, we have an array of elements which we want **sorted** - in other words, we want to arrange the elements in such a way that for every two consecutive elements $E_1, E_2$,

$$
E_1 \le E_2
$$

In this section, we discuss various algorithms designed to accomplish this problem, known as **sorting algorithms**. We will also analyze these algorithms for their time and memory complexity, as well as various properties given below.

> [!Info] Stability
> Say we have two equal values $E_1, E_2$, where $E_1$ is to the left of $E_2$.
> 
> A sorting algorithm is **stable** if the relative positions of these values do not change relative to one another when the algorithm ends. Otherwise, the algorithm is **unstable**.

> [!Info] In Place
> A sorting algorithm is **in-place** if the algorithm operates on the list itself.


# Bubble Sort
Take a list $A$ of length $n$.

$$
A = [5,2,-3,1]
$$

We can iterate through adjacent pairs in the loop, and swap those out of order. Performing this $k$ times, we can guarantee that the final $k$ values are correct (and sorted) - the below example illustrates why.
1. For the first iteration,
   $$
   [5,2,-3,1] \to [2,-3,1,5]
   $$

2. For the second iteration,
   $$
   [2,-3,1,5] \to [-3,1,2,5]
   $$

3. For the third iteration,
   $$
   [-3,1,2,5] \to [-3,1,2,5]
   $$

We are done! Notice how in every iteration $i$ (starting from 1) of the loop, we guarantee the $n - i$ index of the loop correctly contains the $i^{th}$ largest element. Thus, performing this $n - 1$ times, we can guarantee a sorted array (if all $n - 1$ elements are sorted, the first element must be the smallest element).

```python
def bubble_sort(array):
    # i only needs to iterate n - 1 times
    for i in range(0, len(array) - 1):
        # we don't need to check / sort the ith last
        # elements of the array, as they're already sorted
        for j in range(0, n - i - 1):
            # swap the elements if not sorted
            if array[j] > array[j + 1]:
               temp = array[j]
               array[j] = array[j + 1]
               array[j + 1] = temp
```

We find the time complexity of Bubble Sort to be $\Theta(n^2)$, and the **auxilliary memory** to be $\Theta(1)$ (no extra memory). This implementation of Bubble Sort is stable and in-place.
> It's worth noting that regardless if the list is sorted, Bubble Sort **always** takes the same amount of time.

> [!Warning] Bubble Sort Stability
> While this implementation of Bubble sort is stable, that does not mean all implementations necessarily are. If we replaced the $>$ in line 8 with $\ge$, we would make our algorithm unstable!


# Selection Sort
Take a list $A$ of length $n$
$$
        A = [5,2,1,3]
$$

We can iterate through the list, and for every iteration, pick the next smallest element to place at the front of our list. So, for every iteration $i$, we find the $i^{th}$ smallest element and swap it with the element at the $i-1$ index.
1. For the first iteration (swap 1 with 5),
   $$
        [5,2,1,3] \to [1,2,5,3]
   $$
2. For the second iteration (swap 2 with itself),
   $$
        [1,2,5,3] \to [1,2,5,3]
   $$
3. For the third iteration (swap 3 with 5),
   $$
        [1,2,5,3] \to [1,2,3,5]
   $$

We are done!
> Every iteration, we are essentially "picking" the next smallest element to place in the next position!

```python
def selection_sort(array):
    # for every iteration, we pick the next smallest
    # element to place at i
    for i in range(0, len(array) - 1):
        # find the ith smallest element
        min_index = i
        
        for j in range(i + 1, len(array)):
            if array[j] < array[min_index]:
               min_index = j

        # place next smallest element at index i
        temp = array[i]
        array[i] = array[min_index]
        array[min_index] = temp
```

Let's find the time complexity of Selection Sort. Let $c$ denote the amount of time it takes for line 9-10 to run. Then, we can find the $\Theta$ of Selection Sort using the number of times $t_{10}$ runs (as it has the most significant contribution to the runtime).
$$
\begin{align*}
        T(n) &= \sum_{i=0}^{n-2} \sum_{i+1}^{n-1} c = \sum_{i=0}^{n-2} c \left( (n-1) - (i+1) + 1 \right) \\
        &= c \sum_{i=0}^{n-2} n-i-1 = c \left(\sum_{i=0}^{n-2} (n-1) - \sum_{i=0}^{n-2} i \right) \\
        &= c \left( \ (n-1) \left((n-2) - 0 + 1\right) - \frac{(n-2)(n-1)}{2} \right) \\
        &= \Theta(n^2)
\end{align*}
$$
> Note that Selection Sort will always take the same amount of time!

Additionally we find,
- The auxilliary memory to be $\Theta(1)$.
- The algorithm is not stable, as our selection can swap and change the relative order of equal elements.
- The algorithm to be in-place, as no additional memory is used.