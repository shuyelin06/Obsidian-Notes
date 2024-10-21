---
title: MATH401
tags:
- math401
---

This course, Applications in Linear Algebra, describes various ways we can use linear algebra in the real world.

We begin by describing a brief but important theorem for this course.

> [!Abstract] Theorem: Uniqueness of Invertible Linear Systems 
> Suppose we have a linear system
> $$
> A \vec{x} = \vec{b}
> $$
> with $n$ variables and $n$ equations. Then, if $A$ is an invertible $n \times n$ matrix, then the linear system has 1 and only 1 solution, and we can find it by taking
> $$
> \vec{x} = A^{-1} \vec{b}
> $$

- [[Leontief Input-Output]]
- [[Applications of Graphics]]
- [[Least Squares]]
- Linear Discrete Dynamical systems
- Markov Chains
- Google Pagerank Algorithm
- Heat Diffusion and Systems of Linear Differential Equations
- Matrix Exponentials and Rotations
- ..
- ..

---

# (Linear) Discrete Dynamical Systems
We first review some concepts around eigenvalues and eigenvectors.

An **eigenvector** for $A$ is a non-zero vector $\vec{x}$ with the property that
$$
Ax = \lambda x
$$
Where $\lambda$ is some scalar value. In other words, $Ax$ is a scalar multiple of $x$.

We can solve for eigenvectors using the following system:
$$
A \vec{x} = \lambda \vec{x} \Longrightarrow (A - \lambda I_n) \vec{x} = 0
$$
> $I_n$ is the $n \times n$ identity matrix.

If $\lambda$ is an eigenvalue for $A$, then the following are also true.
- There is a non-zero $\vec{x}$ such that $A \vec{x} = \lambda \vec{x}$.
- There is $\vec{x} \ne 0$ such that $(A - \lambda I_n) \vec{x} = \vec{0}$
- $A - \lambda I_n$ is not invertible
- $\text{det}(A - \lambda I_n) = 0$

Additionally, if $\lambda$ is an eigenvalue, then we know that $\lambda$ satisfies the **characteristic equation**
$$
\text{det}(A - \lambda I_n) = 0
$$
So, generally, the process is:
1. Find the eigenvalues for $A$ by solving the characteristic equation for $\lambda$
2. Find eigenvectors for $\lambda$ by solving the system $(A - \lambda I_n) = 0$. 

> [!Example] Example: Eigenvectors and Eigenvalues
> $$
> A = \begin{bmatrix} 1 & 1 \\ -2 & 4 \end{bmatrix}
> $$
> We find the eigenvalues first by solving
> $$
> \begin{align*}
> \text{det} (A - \lambda I_2) &= 0 \\
> \begin{vmatrix} 1 - \lambda & 1 \\ -2 & 4 - \lambda \end{vmatrix} &= 0 \\
> (\lambda - 2) (\lambda - 3) &= 0 \\
> \lambda &= 2,3
> \end{align*}
> $$
> 
> We can now find our eigenvectors. Say we want the eigenvector for $\lambda = 2$. Then, we solve system
> $$
> \begin{align*}
> (A - 2 I_2) \vec{x} = 0 \\
> \begin{bmatrix}
> -1 & 1 \\ -2 & 2
> \end{bmatrix} \vec{x} = 0
> \end{align*}
> $$

An $n \times n$ matrix $A$ is **diagonalizable** if there is an invertible matrix $P$ and a diagonal $n \times n$ matrix $D$ such that
$$
A = P D P^{-1}
$$

> [!Abstract] Theorem: Eigenvectors of Diagonalizable Matrices
> An $n \times n$ matrix $A$ is diagonalizable if and only if $A$ must have $n$ linearly independent eigenvectors $\vec{v}_1, \vec{v}_2, \dots \vec{v}_n$.
>
> In this case, $A = P D P^{-1}$ where $P$'s columns are the eigenvectors, and $D$'s diagonal values are their respective eigenvalues.
> $$
> P = \begin{bmatrix} 
> \vec{v}_1 & \vec{v}_2 & \dots & \vec{v}_n
> \end{bmatrix} \qquad
> D = \begin{bmatrix} 
> \lambda_1 & 0 & \dots & 0  \\
> 0 & \lambda_2 & \dots & 0 \\
> \vdots & \vdots & \ddots & \vdots \\
> 0 & 0 & \dots & \lambda_n
> \end{bmatrix}
> $$

Let's see how we can use these concepts.

Suppose we have a population of predators (ex. hawks), who live among a population of prey (ex. rats). Let $H_k$ be the number of hawks after $k$ months have passed, and $R_k$ be the number of rats (in thousands) after $k$ months. We'll only consider integers of $k$ months.

We can represent and make inferences about this system as follows:

> [!Example] Example: Finding $\vec{x}_k$
> Assume that these populations evolve according to some sort of model as follows:
> $$
> \begin{align*}
> H_{k+1} = (0.4) H_k + (0.5) R_k \\
> R_{k+1} = (-0.2) H_k + (1.2) R_k
> \end{align*}
> $$
> > Note that if we know this, then given the populations in some month $k$, we should be able to compute the populations in the next month!
> 
> Now say we know initial populations $H_0 = 500$, $R_0 = 250$, and
> $$
> \begin{align*}
> H_{k+1} = 0.4 H_k + 0.5 R_k \\
> R_{k+1} = -0.2 H_k + 1.2 R_k
> \end{align*}
> $$
> 
> To find $x_{k+1}$, we find that
> $$
> \vec{x}_{k+1} = 
> \begin{bmatrix}
> H_{k+1} \\ R_{k+1} 
> \end{bmatrix}
> = 
> \begin{bmatrix} 
> 0.4 H_k + 0.5 R_k \\
> -0.2 H_k + 1.2 R_k
> \end{bmatrix}
> = 
> \begin{bmatrix} 
> 0.4 & 0.5 \\
> -0.2 & 1.2
> \end{bmatrix}
> \begin{bmatrix} 
> H_k \\ R_k
> \end{bmatrix}
> = A \vec{x}_k 
> $$
> 
> This gives us a nice way to find any $\vec{x}_k$ given our initial conditions $\vec{x}_0 = (500, 250)^T$! 
> $$
> \vec{x}_k = A^k \vec{x}_0
> $$
> > We can plug in our values to find what the populations are for any month $k$.

For this to be useful for large $k$, we want to be able to find a formula for $A^k$. How could we do this?

> [!Info] Diagonal Matrices
> If $A$ was diagonal, this would be really easy to solve! The power of any diagonal matrix is just it's entries raised to each power individually.

What if $A$ is diagonalizable?
$$
A = P D P^{-1}
$$
Then, interestingly enough,
$$
\begin{align*}
A^k &= (P D P^{-1}) (P D P^{-1}) \dots (P D P^{-1}) \\
A^k &= P D^k P^{-1}
\end{align*}
$$
This can be used to conveniently find $A^k$! We can then multiply this with $\vec{x}_0$ to find a closed formula for $\vec{x}_k$.

> [!Example]+ Example: Finding $A^k$
> In our above system, we can diagonalize our matrix as
> $$
> A = 
> \begin{bmatrix}
> 0.613 & 0.955 \\ 0.790 & 0.295
> \end{bmatrix}
> \begin{bmatrix}
> 1.045^k & 0 \\ 0 & 0.555^k
> \end{bmatrix}
> \begin{bmatrix}
> -0.517 & 1.666 \\ 1.378 & -1.069
> \end{bmatrix}
> $$
> And find
> $$
> \vec{x}_k = P D^k P^{-1} \vec{x}_0 = 
> \begin{bmatrix}
> 96.91 (1.045)^k + 403.1 (0.555)^k \\
> 125 (1.045)^k + 125 (0.555)^k
> \end{bmatrix}
> $$
> We can see that as $k \to \infty$, both populations will go to $\infty$, so they won't die off! For large $k$,
> $$
> H_k \approx 96.91 (1.045)^k \qquad R_k \approx 125 (1.045)^k
> $$
> Note that 
> $$
> \frac{H_k}{R_k} \approx \frac{96.91}{125}
> $$
> Which tells us what the stable proportion of hawks to rats is in the long term!

Another application of these systems is in Recurrence Relations. Consider the following example.

> [!Example]+ Example: Recurrence Relations
> THe Fibonacci Numbers are given as
> $$
> F_0 = 0 \qquad F_1 = 1 \qquad F_n = F_{n-1} + F_{n-2}
> $$
>
> Can we find a closed formula for $F_k$?
> 
> To know what comes next, we need a pair of consecutive Fibonacci numbers. Let $\vec{x}_k = (F_k, F_{k+1})$. Then, 
> $$
> \vec{x}_{k+1} =
> \begin{bmatrix} F_{k+1} \\ F_{k+2} \end{bmatrix} = 
> \begin{bmatrix} F_{k+1} \\ F_{k} + F_{k + 1} \end{bmatrix} = 
> \begin{bmatrix} 0 & 1 \\ 1 & 1 \end{bmatrix}
> \begin{bmatrix} F_{k} \\ F_{k+1} \end{bmatrix}
> $$
> We've found a formula for $\vec{x}_{k+1}$ in terms of $\vec{x}_k$ (with initial conditions $\vec{x}_0 = [0, 1]$. 
> 
> We can solve for $\vec{x}^k$ as
> $$
> \vec{x}_k = A^k \vec{x}_0 = P D^k P^{-1} \vec{x}_0
> $$
> To find a closed form solution.


# Markov Chains
Suppose every year, we have changes
- 10% of those living in the city, decide to move to the suburbs.
- 5% of those living in the suburbs decide to move to the city.

Let $C_k$ denote the proportion of the total population living in the city after $k$ years, $S_k$ denote the proportion of the tital population living in the suburbs after $k$ years. Note that by this definition,
$$
C_k + S_k = 1
$$

Let $\vec{x}_k = (C_k, S_k)^T$. This gives us system
$$
\begin{align*}
C_{k+1} = 0.9 C_k + 0.05 S_k \\
S_{k+1} = 0.1 C_k + 0.95 S_k \\
\vec{x}_{k+1} = 
\begin{bmatrix}
0.9 & 0.05 \\ 0.10 & 0.95
\end{bmatrix} \vec{x}
\end{align*}
$$
Which is a special kind of linear discrete system called a **Markov Chain**! This matrix has the unique property that all column sums equal 1.

Now suppose we initially have 40% of the population in the city, 60% of the population in the suburbs. Then, using our matrix we can deduce unique things about our system! For example, what happens to $\vec{x}_k$ as $k \to \infty$?

While we could diagonalize our matrix like in linear discrete systems, the unique properties of Markov Chains gives us a more convenient way to do this!

> [!Info] Theorem
> Say we have a Markov Chain such that
> $$
> \vec{x} = \lim_{k\to\infty} \vec{x}_k = \lim_{k\to\infty} T^k \vec{x}_0
> $$ 
> exists is non-zero. Then, $\vec{x}$ is an eigenvector for $T$ with eigenvalue $\lambda = 1$.

Given the above theorem, we can find what we converge to by solving for the eigenvalues and eigenvectors! In our previous example, we find eigenvalue and eigenvector
$$
\lambda = 1 \vec{v} = (1/3,2/3)^T
$$
> Note that by the assumption that the proportions should sum to 1, there is only one eigenvector that satisfies our requirements.

This is what our system will converge to for our input, and in fact, for any valid input to the system!

---

A **probability vector** is a vector $\vec{v}$ such for all $i$, $0 \le v_i \le 1$, and
$$
v_1 + v_2 + \dots + v_n = 1
$$

An $n \times n$ matrix $T$ is called a **stochastic matrix** if every column of $T$ is a probability vector.

> [!Abstract] Theorem: Stochastic Matrices and Probability Vectors 
> If $T$ is $n \times n$ stochastic and $\vec{v}$ is an $n \times 1$ probability vector, then $T \vec{v}$ is a probability vector.
>
> Furthermore, the product of two stochastic matrices is stochastic (as multiplying one matrix by another is essentially a bunch of matrix-vector products)
>
> So, if $T$ is stochastic, then $T^k$ is stochastic for any positive integer $k$.

A **Markov Chain** is a dynamical system
$$
\vec{x}_{k+1} = T \vec{x}_k, \vec{x}_0 = \vec{v}
$$
Where $T$ is stochastic, and $\vec{x}_0$ is a probability vector. By the above theorem, it follows that all $\vec{v}_k$ are also probability vectors.

In a Markov Chain, sometimes the stochastic matrix $T$ is called a **transition matrix**.

> [!Abstract] Theorem
> If $A$ is stochastic, then $\lambda = 1$ is an eigenvalue for $A$.
>
> > [!Note]- Proof (Sketch)
> > 
> > It can be shown that $A$ and $A^T$ always have the same eigenvalues, and because of this, any vector times $A^T$ is itself (as the rows of $A^T$ are probability vectors).

A stochastic matrix $T$ is called **regular** if there is some integer $k \ge 1$ such that all entries of $T^k$ are strictly positive (nonzero).
> If $T^k$ is regular, then it holds that $T^{k + i}$ is regular for all $i \ge 0$. So, one way to verify if a matrix is regular is just to raise it to a high power and check if we get a regular matrix!

> [!Example]+ Example: Regular Stochastic Matrices
> $$
> T =
> \begin{bmatrix}
> 0.90 & 0.05 \\ 0.1 & 0.95
> \end{bmatrix}
> $$
> $T^1$ has all positive entries, so it is regular with $k = 1$.
> 
> $$
> T = 
> \begin{bmatrix}
> 0.9 & 0 & 0.5 \\ 
> 0 & 0.8 & 0.5 \\
> 0.1 & 0.2 & 0
> \end{bmatrix}
> \qquad
> T^2 =
> \begin{bmatrix}
> 0.86 & 0.10 & 0.45 \\ 
> 0.05 & 0.74 & 0.4 \\
> 0.09 & 0.16 & 0.15
> \end{bmatrix}
> $$
> $T^2$ has all positive entries, so $T$ is regular with $k = 2$.
>
> $$
> T = 
> \begin{bmatrix}
> 1 & 0.05 \\ 0 & 0.05
> \end{bmatrix}
> $$
> $T$ is upper triangular, and a product of upper triangular matrices is upper triangular. Thus, $T$ is not stochastic.

A **steady state vector** for a stochastic $T$ is a probability vector $\vec{x}$ such that
$$
T(\vec{x}) = \vec{x}
$$
In other words, a probability vector that is an eigenvector for $T$ for $\lambda = 1$.

> [!Abstract] Theorem
> Suppose $T$ is a regular stochastic matrix. Then, there is a unique steady state vector $\vec{v}$ for $T$.
>
> Further, if $\vec{x}$ is any probability vector, then 
> $$
> \lim_{k\to\infty} T^k \vec{x}_0 = \vec{v}
> $$
> > This is an important result we use to solve Markov Chains!

> [!Example]- Example
> The weather in Columbus is either good, indifferent, or bad on any given day.
> - If good today, then for tomorrow we have 60% of good, 30% of indifferent, 10% of bad.
> - If indifferent today, then for tomorrow we have 40% good, 30% indifferent, 30% bad.
> - If bad today, then for tomorrow we have 40% good, 50% indifferent, 10% bad.
>
> What is the probability that any given day has good weather?
> 
> We start by creating transition matrix
> $$
> T =
> \begin{bmatrix}
> 0.6 & 0.4 & 0.4
> 0.3 & 0.3 & 0.5
> 0.1 & 0.3 & 0.1
> \end{bmatrix}
> $$
> 
> This is a Markov Chain with a regular $T$! So, by our theorem, we can find a unique steady state vector $\vec{v}$.
> > Recall the steady state vector has to be a probability vector! So, we need to normalize the eigenvector we find for $\lambda = 1$.
> 
> $$
> \vec{v} = (1/2, 1/3, 1/6)^T
> $$
> 
> So in the long term, $1/2$ of the days are good, $1/3$ are indifferent, and $1/6$ of the days are bad.
> > Note that if $\vec{x}_0$ contains probabilities for the weather today, then $\vec{x}_k = T^k \vec{x}_0$ contains the probabilities $k$ days from now.

> [!Info] Interpreting $T$
> The $(i,j)$ entry of $T$, $t_{ij}$, represents the probability of moving from state $j$ to state $i$. What about the entries of $T^k$?
>
> The $(i,j)$ entry of $T^k$ represents the probability of starting at state $j$, and ending at state $i$ after $k$ steps.
> > Based on this, if $T^k$ is regular, then we know that for all $i,j$, there is some integer $k$ such that it is possible to get from $j \to i$!

> [!Example]- Example: Random Walks
> Consider the following maze with rooms.
> ```mermaid
> graph LR
> 1 o--o 2 & 3;
> 2 o--o 3 & 4;
> 4 o--o 3;
> 5 o--o 3 & 4;
> ```
> 
> A mouse runs through this maze with 5 rooms. At each time step, (every second), the mouse will leave its current room and move to a new room, choosing the next room randomly.
>
> This is a particular type of Markov Chain called a **random walk**. This gives us matrix
> $$
> T = 
> \begin{bmatrix}
> 0 & 1/3 & 1/4 & 0 & 0    \\
> 1/2 & 0 & 1/4 & 1/3 & 0  \\
> 1/2 & 1/3 & 0 & 1/3 & 0  \\
> 0 & 1/3 & 1/4 & 0 & 1/2  \\
> 0 & 0  & 1/4 & 1/3 & 1/2 \\
> \end{bmatrix} 
> $$
>
> We can analyze this matrix as we've done previously!

## Google Pagerank Algorithm
The **Google Pagerank** algorithm is an application of Markov Chains.

Google needs to rank webpages based on which are "important". This will be based entirely on how the webpages link to each other. The basic idea is that a webpage is **important** if many other pages link to it. However, being linked to by an important webpage should carry more weight than being linked to by a page no one cares about.

Google's idea is to **treat websurfing like a random walk** in which the websurfer is rnadomly clicking links. A page is ranked based on the percentage of time the of the random walk is spent on the page (from the steady state).

Some issues with this:
- Some pages don't have outbound links.
- Sometimes, websurfers load up a new page without following a link.

We assume the following about the random websurfer (RW):
1. RW starts at some page.
2. If there are outbound links, there is an 85% chance that RW chooses one of the links, considered equally likely. There is a 15% chance that RW chooses to visit a page at random from all possible pages (not following a link).
3. If the page has no outbound links, there is a 100% chance RW visits a random page, chosen from all possible pages.
4. RW continues this forever.

> [!Example]+ Example: Google Pagerank
> Suppose there are 4 webpages, linked as follows:
> ```mermaid
> graph LR
> 3 --> 1;
> 2 --> 3;
> 1 --> 2 & 3;
> 4 --> 2 & 3;
> ```
> 
> This gives us transition matrix
> $$
> \begin{align*}
> T 
> &= 0.85 (\text{Click a Link}) + 0.15 (\text{Go Somewhere Random}) \\
> &= 
> 0.85 
> \begin{bmatrix}
> 0 & 0 & 1 & 0 \\
> 1/2 & 0 & 0 & 1/2 \\
> 1/2 & 1 & 0 & 1/2 \\
> 0 & 0 & 0 & 0
> \end{bmatrix}
> +
> 0.15
> \begin{bmatrix}
> 1/4 & 1/4 & 1/4 & 1/4 \\
> 1/4 & 1/4 & 1/4 & 1/4 \\
> 1/4 & 1/4 & 1/4 & 1/4 \\
> 1/4 & 1/4 & 1/4 & 1/4 
> \end{bmatrix}
> \end{align*}
> $$
> > Note that if there no outbound links, then the page would have a 100% chance to go somewhere random. We list this by just filling both columns in the 0.85 and 0.15 matrix with an equal chance of going to any website.
> 
> We can then use this matrix and create a steady state vector!
