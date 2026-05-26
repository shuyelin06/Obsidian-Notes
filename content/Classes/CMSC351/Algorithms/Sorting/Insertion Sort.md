---
title: Insertion Sort
tags:
- cmsc351
---

# Algorithm
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

# Pseudocode
Pseudocode for Insertion Sort is given below.

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
- If the array is **reverse sorted**, `while`'s body will always execute - the algorithm will run the slowest.

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
