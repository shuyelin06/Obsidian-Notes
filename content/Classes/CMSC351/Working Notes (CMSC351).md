# Coin Change...

# Big-O Notation
## Motivation
Suppose we have 2 different algorithms operating on a list of length $n$. Now suppose we run these algorithms on various size lists, and obtain the following:

| $n$ | $A_1 (n)$ | $A_2(n)$ |
| :-: | :-: | :-: |
| 10 | 6 | 1 |
| 20 | 12 | 6 |
| 30 | 18 | 17 |
| 40 | 24 | 25 | 
| 50 | 28 | 40 |
| 60 | 30 | 63 |
| 70 | 38 | 82 |

We could use this table to compare the two algorithms based on their time values. For example, we can see that $A_1 (n)$ is approximately better than $A_2 (n)$ for $n \le 40$.

Is there a better way to formalize this comparison?

Well, yes! Suppose we know these functions stay within the bounds
$$ \begin{align}
	0.4n \le &A_1(n) \le 0.6 n \\
	0.01n^2 \le &A_2(n) \le 0.02 n^2
	\end{align} $$
These bounds could be used to more formally compare the two algorithms! 

The purpose of Big-O Notation is to provide a more formalized argument for performing these comparisons.


# Big-O Notation
## Big-O, Big-Omega, Big-Theta 
Suppose we have a function $f(x)$. 

We say $f(x) = O(g(x))$ to mean:
$$ \exists x_0,C \text{ such that } x \ge x_0 \to f(x) \le C g(x)$$
In other words, $O(g(x))$ is a function such that after some cutoff $x_0$, $f(x)$ is less than some multiple of $g(x)$ for all $x$!
We call $O(g(x))$ the **Big-O** (upper bound) of $f(x)$.

> [!Example]- Example: Big-O
>
> Here, $f(x) = O(x^2)$ with $C = 2$ and $x_0$ as shown. 
> 
> Note that $f(x)$ does not necessarily have to be below $C x^2$ for all $x$ - only past some cutoff $x_0$.
> 
> ![[(Big-O) Example 1.png]]


> [!Example]- Example: Big-O Proof (1)
>
> Prove that
> $$ 2x \log(x) - 1 = O(x \log(x)) $$
> 
> Observe that for all $x > 0$,
> $$ 2x \log(x) - 1 \le 2x \log(x) $$
> Thus, we've found a Big-O function $O(x \log(x))$ with $C = 2$ and $x_0 = 1$. 


> [!Example]- Example: Big-O Proof (2)
> Prove that 
> $$ 4x^2 + x \log(x) - 1 = O(x^2) $$
> 
> Observe that for all $x > 0$,
> $$ \begin{align}
> 	4x^2 + &x \log(x) - 1 \\
> 	&\le 4x^2 + x \log(x) \\
> 	&\le 4x^2 + x^2 = 5x^2
> 	\end{align} $$
> Thus, we've found a Big-O function $O(x^2)$ with $C = 5$ and $x_0 = 1$.

Note that this function is not unique! There are a multitude of functions that can satisfy the Big-O of $f(x)$.

> [!Example]- Example: Multiple Big-O Functions
> 
> Suppose $f(x) = O(x^2)$. If this is the case, then we can also say that 
> $$ \begin{align}
> 	f(x) &= O(x^3) \\ 
> 	f(x) &= O(x^4) \\
> 	&\vdots
> 	\end{align} $$
> 
> However, we often prefer to choose the upper bound that grows the slowest.


Additionally, we can say $\Omega(g(x))$ to mean:
$$ \exists x_0, B > 0 \text{ such that } \forall x \ge x_0 \to f(x) \ge B g(x) $$
In other words, $\Omega(g(x))$ is a function such that after some cutoff $x_0$, $f(x)$ is greater than some multiple of $g(x)$ for all $x$!
We call $\Omega(g(x))$ the **Big-Omega** (lower bound) of $f(x)$.

> [!Example]- Example: Big-Omega
>
> Here, $f(x) = \Omega(x^2)$ with $B = \frac{1}{2}$ and $x_0$ as shown.
> 
> ![[(Big-O) Example 2.png]]


> [!Example]- Example: Big-Omega Proof (1)
> 
> Prove that $5 x \lg(x) - x = \Omega(x \lg(x))$.
> 
> Observe that $x \le x \lg(x)$ when $\lg(x) \ge 1$ which occurs at $x \ge 2$. Then, for $x \ge 2$,
> $$ \begin{align}
> 	5x \lg(x) - x &\ge 5x \lg(x) - x \lg(x) \\
> 	&\ge 4x \lg(x)
> 	\end{align}  $$
> Thus, choosing $B = 4$ and $x_0 = 2$, we have shown that $5 x \lg(x) - x = \Omega(x \lg(x))$!

Now note that while Big-O serves as an upper bound, and Big-Omega serves as a lower bound, a variety of functions can serve as these upper / lower bounds! 

We define $\Theta(g(x))$ to mean
$$ \exists B > 0, C> 0, x_0 \text{ such that }x \ge x_0 \to Bg(x) \le f(x) \le Cg(x)$$
In other words, $\Theta(g(x))$ is a function that can serve as an upper and lower bound for $f(x)$! We call $\Theta(g(x))$ the **Big-Theta** of $f(x)$.
> To prove $\Theta(g(x))$, we prove $O(g(x))$ and $\Omega(g(x))$.

We should generally prefer to use Big-Theta when possible.

## Limit Theorem (Alternative Proof)
The previous section explicitly finds values $B$ (or $C$) and $x_0$ to find / prove a function for $O(g(x))$ and $\Omega(g(x))$. However, there is another method of proving using **limits**.

> [!Abstract] Theorem: Big-O, Proof by Limits
>
> Let $f(x)$ and $g(x)$ be functions such that
> $$ \lim_{x\to\infty}f(x) \qquad \lim_{x\to\infty}g(x) $$
> exist. 
> 
> The following cases are true.
> 1. $$ \text{If } \lim_{x\to\infty} \frac{f(x)}{g(x)} \ne \infty \text{ then } f(x) = O(g(x)) $$
> 2. $$ \text{If } \lim_{x\to\infty} \frac{f(x)}{g(x)} \ne 0 \text{ then } f(x) = \Omega(g(x)) $$
> 
> Thus, if both hold true, then $f(x) = \Theta(g(x))$!

Some examples are given below.

> [!Example]- Big-O, Proof by Limits
> Observe that
> $$ \lim_{n\to\infty} \frac{n \ln(n)}{n^2} = \lim_{n\to\infty} \frac{\ln(n)}{n} = \lim_{n\to\infty} \frac{1/n}{1} = 0 $$
> Thus, $n \ln(n) = O(n^2)$.

## Code Analysis using Big-O Notation
Big-O notation is especially important in computer science, as it serves as a benchmark for comparing algorithms with one another.

Typically we'll have some algorithm that depends on some varying $n$, where $n$ can be the length of a list, loop iterations, etc. Based on this algorithm, we can form a function $T(n)$ representing its runtime complexity.

What do we mean by nice functions?

Well, computer scientists have settled on a collection of **nice functions** which easily be compared with one another. A non-comprehensive list of these functions is given below, in order of slowest to fastest growing:
$$ 1, \lg(n), n, n \lg(n), n^2, n^2 \lg(n), \dots $$
> Use of $n$ over $x$ does not typically matter, but we tend to prefer $n$ when we're restricted to integers.

Choosing the respective Big-Theta function for our time function, $T(n) = \Theta(g(n))$, will give us an idea on how fast (or slow) our algorithm runs!

> [!Info] Big-O Algorithm Analysis: Intuition
>
> Apart from using definitions and limit theorems, we can often intuitively find a function's Big-Theta! For a given function $T(n)$, the $\Theta(g(n))$ is often the fastest growing term.
>
> For example,
> $$ n^2 \lg(n) + n \lg(n) - n + \lg(n) - 7 = \Theta(n^2 \lg(n)) $$

Note that a slow-growing $\Theta(g(n))$ for an algorithm does not necessarily mean its good for all values $n$!

> [!Example]- Example: Big-O Misconceptions
> Suppose we have two algorithms
> $$ T_1(n) = \Theta(n) \qquad T_2(n) = \Theta(n^2) $$
> We may intuitively be led to think that $T_1$ is automatically better. However, this is not true - this only tells us that $T_1(n)$ is better for sufficiently large $n$, but does not tell us which is better for small values $n$.
>
> > We'll have algorithms later in the course where they may be efficient for large values $n$, but terribly inefficient for small values!

> [!Info] Time Complexity Analysis with Algorithms
>
> Say we have a block of code with some input whose size is $n$, and we want to know $T(n) = \Theta(g(n))$.
>
> Note that every statement in a block of code has overhead, and takes time. However, some statements "matter more" than others, as they have more meaningful contributions to the time complexity than others.
>
> We can generalize this in the following rules:
> 1. **Precedence**: We don't need to include a time function ($n, n^2, \dots$) provided there is a faster growing function in the analysis.
> 2. **Loops**: We don't need to include the time it takes for a loop iteration to occur, provided the loop body takes time.
> 3. **Conditionals**: We don't need ot include the time it takes for a conditional to evaluate, provided the conditional body takes time.


> ![Example] Example: Algorithm Analysis
>
> Suppose we have the following, with each statement taking some amount of time:
> 
> ```
> sum = 0 # a time
> for i to n: # b time for each iteration
>     sum += i # c time
> end for
> ```
> 
> We would find total time $T(n) = n \cdot (b + c) + a$. However, if all we want is the most relevant time complexity, then
> 1. We can ignore $a$, as it has an insignificant effect on the time complexity compared to the loop.
> 2. We can ignore $n \cdot b$, as the body of the loop takes time ($n \cdot c$).
>
> This gives us $T(n) = n \cdot c$.