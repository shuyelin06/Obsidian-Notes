---
title: Coin Change
tags:
- cmsc351
---

**Problem**: Given coins with values $c_1, c_2, \dots c_n$, what is the minimum number of coins needed to obtain a cumulative value of $n$ cents out of these coins?

> [!Example]+ Coin Change
> Suppose we have coins with values given as
> $$
> C = \{ 2, 5, 10 \}
> $$
>
> - Can we make up the value of 7 with these coins? Yes, with coins $[2,5]$!
> - Can we make up the value of 25 with these coins? Yes, with coins $[10, 10, 5]$!
> - Can we make up the value of 23 with these coins? No.

While this problem is quite easy to solve with simple coin values such as $\{ 5, 10 \}$, it easily becomes difficult with values we're not used to (ex. $\{ 3, 7 \}$)!


# Solution (Kinda) 1: Greedy Approach
A rather intuitive approach to solving this problem is by using a **greedy algorithm**. If we want to minimize the number of coins used, then it would make sense to choose the largest coins to make up our sum, and work our way down to the smallest!

Thus, the greedy approach would attempt to solve the problem as follows. Given a cumulative coin value $v$ and a set of coins $C$,
- Choose the largest coin in the set of coins, $c_1$. If $v > c_1$, then subtract $c_1$ from $v$ as many times as needed until $v \not> c_1$, and record the number of coins used.
- Choose the 2nd largest coin in the set of coins, $c_2$. If $v > c_2$, then subtract $c_2$ from $v$ as many times as needed until $v \not> c_2$, and record the number of coins used.
- ...

Consider the following examples.

> [!Example]+ Example: Coin Change (Greedy Approach)
> Consider the set of coins
> $$
> C = [1,5,10]
> $$
>
> What is the minimum number of coins needed to obtain $n = 27$ cents?
> 1. We have 27 cents. Choose the largest coin, 10. We can use two 10-cent coins, to have 7 cents left.
> 2. We have 7 cents. Choose the 2nd largest coin, 5. We can use one 5-cent coin to have 2 cents left.
> 3. We have 2 cents. Choose the smallest coin, 1. We can use two 1-cent coins to have 0 cents left.
>
> Thus, by greedy, we've found that our minimum number of coins is $2 + 1 + 2 = 5$ coins!

Unfortunately, greedy may not yield the correct answer in all cases. Consider the following:

> [!Example]+ Example: Limitations of the Greedy Approach
> Suppose the set of coins
> $$
> C = [1, 10, 25]
> $$
>
> What is the minimum number of coins needed to obtain $n = 40$ cents?
>
> By the greedy approach, we would choose the coins (in this order) $[25, 10, 1, 1, 1, 1, 1]$, giving us a "minimum" of 7. However, we know this isn't the most optimal solution, as we can just choose four 10-cent coins instead ($[10,10,10,10]$)!
>
> Thus, in this case, the greedy approach does not yield the correct results.


# Solution 2: Dynamic Programming
Recall that while the greedy algorithm may have seemed intuitive, it in fact fails in specific cases. Here, we discuss a solution to the problem that indeed does work in all cases, and uses **dynamic programming**.

Say we have the set of coins with values $C = [1, 3, 5]$. Now suppose we have an array $A$, where index $i$ of this array denotes the minimum number of coins needed to obtain coin value $i$. Then, observe the following:
$$
\begin{align*}
   &A[0] = 0 &\text{No Coins} \\
   &A[1] = 1 &\text{One 1-Cent Coin} \\
   &A[2] = 2 &\text{Two 1-Cent Coins} \\
   &A[3] = 1 &\text{Three 1-Cent Coins} \\
   &A[4] = 2 &\text{Four 1-Cent Coins} \\
   &A[5] = 1 &\text{One 5-Cent Coin} \\
   &A[6] = 2 &\text{One 5-Cent and One 1-Cent Coin} \\
\end{align*}
$$

Say we wanted to find the next minimum coin count for $n = 7$, or in other words, $A[7]$. Interestingly enough, we can find this value as one of the following 3 possibilities:
- The minimum number of coins for $n = 6$, plus a 1-cent coin. In other words, $A[6] + 1$.
- The minimum number of coins for $n = 4$, plus a 3-cent coin. In other words, $A[4] + 1$.
- The minimum number of coins for $n = 2$, plus a 5-cent coin. In other words, $A[2] + 1$.

We can generalize this finding. Say we have a set of coins with values $\{ c_1, c_2, \dots c_n \}$, and we have the array $A$ where $A[i]$ denotes the minimum number of coins needed to obtain value $i$. Then, we can do the following.
1. First, we let all elements in the array be $\infty$, and set $A[0] = 0$.
2. Then, iterating through this array from left to right, we can find the value at $A[i]$ as 
   $$
   \min ( A[i - c_1], A[i - c_2], \dots A[i - c_n] ) + 1
   $$
   For all indices $i - c_j$, $1 \le j \le n$ that exist.

Pseudocode for this algorithm is given below.

```python
def min_coins(coins, n):
    A = [sys.maxsize] * (n + 1) # sys.maxsize is a large number
    A[0] = 0 # Base case, no coins needed at all

    # Iterate, and populate all cells of A with minimum counts
    for i in range(0, len(A)):
        min_ways = sys.maxsize
        for coin in coins: # Find min_ways
            if 0 <= i - coin:
               min_ways = min(min_ways, A[i - coin])
        A[i] = min_ways

    return A[n]
```

Analyzing the time complexity of this algorithm, we see that it takes $\Theta(n)$ time.