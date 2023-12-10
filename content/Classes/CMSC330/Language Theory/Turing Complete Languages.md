---
title: Turing Complete Languages
tags:
- cmsc330
---

Despite how useful both Regular Languages and Context Free Languages are, they are still limited in the problems they can solve.

However, there exists a theoretical machine that can solve any solveable problem. This machine is known as the **turing (atomic) machine**. A turing machine must have the following:
1. An infinite number of cells which can store either 0 or 1.
2. A pointer pointing to some cell, which can read from or write to a cell, and move left and right betwen cells.

This, coupled with a finite set of states with directions to manipulate the pointer, can (theoretically) solve any solveable problem!

Unfortunately, turing machines don't exist - it's simply not possible to have an infinite number of cells. However, we can do the next best thing, and simulate these machines! A language that can simulate a turing machine, and theoretically solve any solveable problem (given sufficient memory) is known as a **turing complete language**.

Below, we discuss a minimal turing complete language, **lambda calculus**.
> Nearly all programming languages we use are turing complete!

# Lambda Calculus
**Lambda calculus** is a universal model of computation, that serves as the minimal turing complete language. It consists of expressions which are defined as the following:
$$
\begin{align*}
   e \to \; &x &\text{Variable} \\
         &\lambda x.e &\text{Function Definition} \\
         &ee &\text{Application}
\end{align*}
$$
> Note that because lambda calculus is turing complete, it can (theoretically) be used to solve any solveable problem.

### Derivation and Left Associativity
We can use our definition of a lambda expression to prove that different expressions are valid in the lambda calculus language. The process of recursively applying our definitions on the lambda expression is known as **derivation**.

Consider the following examples

> [!Example]+ Example: Lambda Calculus
> Show that $\lambda x.x$ is accepted by the lambda calculus language.
>
> $$
> e \to \lambda x.e \to \lambda x.x
> $$

> [!Example]+ Example: Lambda Calculus (2)
> Suppose we have string `abc`. Show that it is accepted by the lambda calculus language.
>
> We can show this with the following derivation:
> $$
> \begin{align*}
>       e &\to ee \to ae \\
>         &\to aee \to abe \\
>         &\to abc
> \end{align*}
> $$

Sometimes, however, derivations using our our lambda expression can yield ambiguous results. Consider the following example.

> [!Example]+ Example: Ambiguity of Lambda Expressions
> At the simplest example, consider the expression
> $$
> eee
> $$
>
> We could evaluate this in the other $(ee)e$, or the order $e(ee)$ to obtain the same result. This creates ambiguity!

To address this ambiguity, lambda calculus has a concept of **left associativty**, meaning that for any ambiguous expression, we will always evaluate the leftmost two expressions first. In other words, there will always be an implicity set of parentheses around the 2 left-most expressions.

> [!Example]+ Example: Left Associativity
> Consider the above example. To remove ambiguity, the concept of left associativity tells us to evaluate our expression in the order $(ee)e$ first.

## Alpha Equivalence
Suppose we have two lambda expressions. We say they are **alpha equivalent ($\alpha$-equivalent)** if the two expressions are semantically equivalent - in other words, they both evaluate to the same result!

### Beta-Reduction and Beta-Normal Form
We can show that two expressions are alpha-equivalent by reducing them, and comparing their most basic forms.

Note that the function definition
$$
\lambda x.e
$$
represents an **anonymous function**, which takes in some parameter $x$ and uses it to return an expression. Any variable supplied after this function is taken as a parameter to the function, meaning we can actually "plug in" this variable input and evaluate our function to reduce our lambda expression.
> Note that the function's expression will be anything after the function definition $(x.)$, up until the end of the lambda expression, or the first valid closed parentheses. Only in this expression will the function's parameter exist and be referenced.

This process of applying an argument to a function is known as **beta-reduction ($\beta$-reduction)**.

> [!Example]+ Example: Beta-Reduction
> Consider the following lambda expression
> $$
> (\lambda x.xyz) a
> $$
>
> We have a function $\lambda x.xyz$ which takes in an input $x$, and returns an output $xyz$. Furthermore, our function is taking the parameter $a$. We can thus $\beta$-reduce our function to become
>
> $$
> (\lambda x.xyz) a \to ayz
> $$

> [!Example]- Example: Beta-Reduction (2)
> Consider the following lamdbda expression
> $$
> (\lambda x . \lambda y . xy) a 
> $$
>
> We can beta reduce it as so:
> $$
> (\lambda x . \lambda y . xy) a \to \lambda y . ay
> $$

By applying beta reduction, we are minimizing the number of **bound variables** in our lambda expression.
- A **bound variable** is a variable that refers to the function's argument (including the function's argument itself)
- A **free variable** is a variable that is not bound.

In the above example, we would say that $x$ is a **bound variable**, and $a, y, z$ are **free variables**.

> [!Example]+ Example: Bound and Free Variables
> Consider the following lambda expression
> $$
> (( \lambda a . \lambda b . cb ) d ) a
> $$
>
> Then, we have
> $$
> \begin{align*}
>       &\text{Bound Variables} &(( \lambda \underline{a} . \lambda \underline{b} . c\underline{b} ) d ) a \\
>       &\text{Free Variables} &(( \lambda a . \lambda b . \underline{c} b ) \underline{d} ) \underline{a}      
> \end{align*}
> $$
> > Note that one of the $a$'s are bound, while the other is free - this is because the free $a$ is outside of the scope of the $\lambda a$ function, so it is not bound to this function.

Note that lambda calculus also has a concept of **variable shadowing**. For example, given the lambda expression $\lambda x . (\lambda x . x) x$, the following variables are bound to one another.
$$
\lambda \underline{x} . (\lambda x . x) \underline{x} \qquad \lambda x . (\lambda \underline{x} . \underline{x}) x
$$
Thus, this expression is actually equivalent to:
$$
\lambda x . (\lambda y . y) x
$$

When a lambda expression can no longer be reduced any further using $\beta$-reduction, we say it is in **beta-normal form ($\beta$-normal form)**. Two lambda expressions that are alpha equivalent should be the same when they're in $\beta$-normal form.

> [!Example]+ Example: Alpha Equivalence
> Suppose we have lambda expressions
> $$
> (\lambda x. \lambda y. xxy) a \qquad \lambda b.aab
> $$
>
> Show that they are alpha equivalent.
>
> Taking our first lambda expression, we beta reduce it to obtain the beta-normal form
> $$
> \begin{align*}
>       &(\lambda x. \lambda y. xxy) a \\
>       \to &\lambda y. aay
> \end{align*}
> $$
>
> Because $y$ stands for any arbitrary variable, we can change it to represent $b$ and obtain $\lambda b.aab$ (this is known as **beta-conversion**). Thus, our two expressions are alpha equivalent!

### Lazy and Eager Evaluation
Note that when $\beta$-reducing, we have different orders of evaluation. Given a function and its argument, 
- In **call by name (lazy evaluation)**, we choose to plug in our argument into the function before attempting to evaluate it.
- In **call by value (eager evaluation)**, we choose to evaluate our argument to the function before passing it in.

> [!Example]+ Example: Eager vs. Lazy Evaluation
> Consider the lambda expression
> $$
> (\lambda x.y) ( (\lambda a.b) c )
> $$
>
> - If we were to call by name, we would pass in $( (\lambda a.b) c )$ to obtain $y$ with one beta-reduction.
> - If we were to call by value, we would evaluate $( (\lambda a.b) c ) \to b$ first, then pass this into $\lambda x.y$ to obtain $y$ with two beta-reductions.

Evaluating lazy and eager expressions might yield differing results! Consider the following examples.

> [!Example]+ Example: Eager vs. Lazy Evaluation
> Consider the lambda expression
> $$
> (\lambda a.b) ( (\lambda x.xx) (\lambda x.xx) )
> $$
>
> With lazy evaluation, we pass our argument into the function to obtain the output $b$. However, with eager evaluation, our evaluation would never end, as $(\lambda x.xx) (\lambda x.xx)$ evaluates to itself!
>
> Thus, in this example, lazy and eager evaluation will yield differing results. Note that languages like Ocaml use eager evaluation.

> Note that languages like Ocaml perform eager evaluation.

## Church Encodings
Recall that Lambda Calculus can theoretically be used to solve any solveable problem. If this is the case, then it must be possible to use lambda expressions to represent common programming constructs. This is known as an **encoding**.

One common representation for these expressions is known as **church encodings**.

Consider the following subset of the church encodings:

$$
\begin{align*}
        \text{True} &\equiv \lambda x . \lambda y . x \\
        \text{False} &\equiv \lambda x . \lambda y . y \\
        \text{if } a \text{ then } b \text{ else} &\equiv a \; b \; c
\end{align*}
$$

These can be used to represent conditional boolean expressions! Consider the below examples.

> [!Example]+ Example: Church Encodings
> Represent the expression `if true then false else true` in lambda calculus, and evaluate it to obtain a result.
> 
> We convert this expression to church encodings to obtain
> $$
> (\lambda x . \lambda y . \lambda x) (\lambda x . \lambda y . \lambda y) (\lambda x . \lambda y . \lambda x)
> $$
> 
> We will now apply beta-reduction (lazy evaluation) to this expression to obtain a result.
> $$
> \begin{align*}
>         &(\lambda x . \lambda y . \lambda x) (\lambda x . \lambda y . \lambda y) (\lambda x . \lambda y . \lambda x) \\
>         \to &(\lambda x . \lambda y . \lambda y)
> \end{align*}
> $$
> 
> Which represents the result `false`.