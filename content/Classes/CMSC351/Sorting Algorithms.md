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
        [\underline{5},2,\underline{1},3] \to [1,2,5,3]
   $$
2. For the second iteration (swap 2 with itself),
   $$
        [1,\underline{2},5,3] \to [1,2,5,3]
   $$
3. For the third iteration (swap 3 with 5),
   $$
        [1,2,\underline{5},\underline{3}] \to [1,2,3,5]
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


# Insertion Sort
Take a list $A$ of length $n$
$$
        A = [4,3,1,8,3,2]
$$
We can iterate through the list, and for every iteration $i$, we check if any value at index $j < i$ is greater than our value $A[i]$. We slide any element that $A[j] > A[i]$ to the right, and place $A[i]$ in the newly created place.
1. For the first iteration (3), we slide 4 to the right to obtain
   $$
        [4,\underline{3},1,8,3,2] \to [\underline{3},4,1,8,3,2]
   $$
2. For the second iteration (1), we slide 3, 4 to the right
   $$
        [3,4,\underline{1},8,3,2] \to [\underline{1},3,4,8,3,2]
   $$
3. For the third iteration (8), we slide nothing to the right
   $$
        [1,3,4,\underline{8},3,2] \to [1,3,4,\underline{8},3,2]
   $$
4. For the fourth iteration (3), we slide 4, 8 to the right
   $$
        [1,3,4,8,\underline{3},2] \to [1,3,\underline{3},4,8,2]
   $$
5. Finally, for the 5th iteration (2), we slide 3, 3, 4, 8 to the right
   $$
        [1,3,3,4,8,\underline{2}] \to [1,\underline{2},3,3,4,8]
   $$
> Note that after every iteration $i$, the subarray to the left of $i$ is sorted. We slowly build this sorted array until we are done!

```python
def insertion_sort(array):
    for i in range(1, len(array)):
        key = array[i] # cur value to insert

        # shift elements
        j = i - 1
        while j >= 0 and key < array[j]: 
              array[j + 1] = A[j]
              j -= 1

        array[j + 1] = k # insert 
```

Let's find the time complexity of Insertion Sort. However, note that the `while` loop will run differently depending on different conditions in the array.
- If the array is **sorted**, `while`'s body will not execute at all - the algorithm will run the fastest.
- If the array is **unsorted**, `while`'s body will always execute - the algorithm will run the slowest.

Because of this, we will analyze the time complexity of Insertion Sort based on these **best** and **worst** case executions. Let $t_{i}$ indicate the runtime cost of line $i$.
- For the **best case scenario** (sorted array), we know that the while loop doesn't execute - so, only lines $t_3, t_6, t_7, t_{11}$ contribute to the runtime (the while loop check at line 7 only occurs once).
  $$
        T(n) = (n - 1) (t_3 + t_6 + t_7 + t_{11}) = \Theta(n)
  $$
- For the **worst case scenario** (unsorted array), we assume the maximum iterations by the `while` loop, in that it will always run until $j = -1$. Thus, for every iteration $i$, the while loop will run for $i$ total iterations ($j=i-1, i-2, \dots, 0$).
  $$
        T(n) = \sum_{i=1}^n \left[ t_3 + t_6 + i (t_8 + t_9) + t_{11}) \right] = \dots = \Theta(n^2)
  $$

Notice that our time complexity depends on how sorted our array is! So, how can we measure an average time complexity for Insertion Sort?

We can do this using the concepts of **inversions**.

> [!Info] Inversion
> For a list $A$, an **inversion** is a pair of elements which is out of sorted order.
>
> > [!Example]- Example: Inversions
> >
> > For example, if we have $A = [4,3,1,8,3,2]$, we have the following inversions. To find the number of inversions, find how many elements to the right of an index are out of place with the current index.
> > - For 4 at index 0, we're out of order with 3, 1, 3, 2: $(0,1), (0,2), (0,4), (0,5)$.
> > - For 3 at index 1, we're out of order with 1, 2: $(1,2), (1,5)$
> > - For 1 at index 2, we're out of order with none of them to the right.
> > - For 8 at index 3, we're out of order with 3, 2: $(3,4), (3,5)$
> > - For 3 at index 4, we're out of order with 2: $(4,5)$
> >
> > We hvae a total of 9 inversions!
>
> Observe that the number of inversions in a list gives a measurement of how sorted a list is.
> - If the list is sorted, the number of inversions is 0.
> - If the list is unsorted, the number of inversions is equal to every pair of indices, $\frac{1}{2} C(n,2) = \frac{n(n-1)}{2}$.

Let $I$ be the number of inversions in $A$. Note that for every element shift we do, we fix one inversion. Thus, the number of times the while loop runs is equal to the number of inversions! This gives us runtime
$$
        T(n) = (n-1) (t_3 + t_6) + I(t_8 + t_9) + (n-1) t_{11}
$$
So for an "average list", we get $I = \frac{n(n-1)}{4}$, giving us the **average time complexity** of
$$
        T(n) = (n-1) (t_3 + t_6) + \frac{n(n-1)}{4} (t_8 + t_9) + (n-1) t_{11} = \dots = \Theta(n^2)
$$

Additionally, we find
- The auxilliary memory to be $\Theta(1)$.
- The algorithm is stable, as our insertion sort will not shift elements that are equal.
- The algorithm is in place, as it operates solely on the list itself.
