---
title: 330Working
---

# Operational Semantics
**Semantics**: The meaning of a phrase. Consider the following code snippets:

```javascript
// java
int x = 2 + 3;

(* ocaml *)
let x = 2 + 3 ;;

# python
x = 2 + 3

// javascript
var x = 2 + 3;
```

These phrases all mean the same thing, despite being syntactically different!

There are multiple ways we can describe meaning:
- **Denotational Semantics**: Describe semantics through mathematical constructs
- **Axiomatic Semantics**: Describe meanings through promises
- **Operational Semantics**: Describe meanings through how things execute.

Here, we will only talk about operational semantics. These semantics are helpful in making interpreters.

Operational semantics will ultimately create a proof of correctness or properties.

Our syntax is as follows:
- Values will be denoted as $v$
- Expressions will be denoted as $e$.
- Environments will be denoted as $A$.

Our interpreter will get expressions, and it needs rules to understand what to do with these expressions.

Let's create rules for how an ocaml program will execute. Suppose our language is small, and only has numbers $3,2,-1$.

Our interpreter needs a rule to know what an expression returns. If our language is only numbers, then our only rule is
$$
e \to v \qquad e := n, v := n
$$

Now let's add addition to our language.
$$
e \to v \qquad e := n \mid e + e, v := n
$$

If $e$ is a number $n$ then $n \to n$. Else, if $e$ is an expression of $e_1 + e_2$, then
- if $e_1 \to n_1$
- if $e_2 \to n_2$
- if $n_1 + n_2 = n_3$
- then $e \to n_3$

This is known as an argument structure (refer to propositional logic). Basically, if our conditions are true, then our conclusion is true. This takes the base structure

$$
\frac{H_1 \dots H_n}{C}
$$

If there are no hypotheses ($n = 0$), then the conclusion automatically holds, in what we call an **axiom**.

Given all the argument forms, we can build a tree representing what we can do?

> [!Example] Example: Argument Structure
> The argument structure
> $$
> \frac{e_1 = v_1 \quad e_2 = v_2 \quad v_1 + v_2 = v_3}{e_1 + e_2 = v_3}
> $$

We call $v_1 + v_2 = v_3$ a **meta language**, language in our language describing what it should do.

The argument form is essentially proving definitions of our target language hold. The meta language helps us in this proof.

---

An environment can be defined as follows:

$$
\frac{A(x) = v}{a; x \to v}
$$

This tells us that if in some environment $A$, $x$ is bound to some value, then in the environment $x$ and this value are equivalent. $A$ is essentially serving as a place to "look up variables", so we can determine their value.

$$
\frac{[x:3;y:4] x \to 3 \quad [x:3;y:4] y \to 4 \quad 7 = 3 + 4}{[x:3;y:4] x + y = 7}
$$

Let binding

Suppose $e$ is $\text{let } x = e_1 \text{ in } e_2$. Then,
$$
\frac{A;e_1 \to v_1 \quad A,x:v_1; e_2 \to v_2}{A ; \text{let } x = e_1 \text{ in } e_2 \to v_2}
$$
Basically, this say aht we will extend our existing environment $A,x:v_1$ by adding the binding to it, then evaluating our expression $e_2 \to v_2$.

> Given rules, draw a proof...

---

Consider the expression

```python
A; Let x = 3 in x + 4 = _
```

Our argument form then would be
$$
A;3 \to 3_{v_1} \quad \frac{A,x:3; x \to 3_{n_1} \quad A,x:3; 4 \to 4_{n_2} \quad 7 \; \text{is} \; 3 + 4}{A,x:3;x+4 \to 7}
$$

We have the following axioms
$$
\begin{align*}
        &A;e_1 + e_2 \to n_3            &\equiv A; e_1 \to n_1 \quad A; e_2 \to n_2 \quad n_3 \; \text{is} \; n_1 + n_2 \\
        &A;\text{Let } x = n \text{ in } e       &\equiv A,x=n; e \\
        &A;x \to v                      &\equiv A(x) \to v
\end{align*}
$$
> For variable bindings, always look at the most recent binding. THe `,` operator adds a variable binding to our environment.

---

Let's talk about Lambda Calculus. Recall that the grammar is given as
$$
\begin{align*}
        e \to \; &x \\
              \mid &\lambda x.e \\
              \mid &e \; e
\end{align*}
$$

What are the operational semantic rules for lambda calculus?
$$
\begin{align*}
        
\end{align*}
$$

Prof K's description
$$
\lambda x.e \to \lambda x . e
$$

Compiler Optimization (you could evaluate $e$)
$$
\frac
{e \to e'}
{\lambda x . e \to \lambda x . e'}
$$

$$
\frac
{e_1 \to e_1' \quad e_2 \to e_2'}
{(e_1 \; e_2) \to (e_1' \; e_2')}
$$

OR

EAGER EVALUATION
$$
\frac
{e_2 \to e_2'}
{(e_1 \; e_2) \to (e_1 \; e_2')}
$$

LAZY EVALUATION
$$
\frac
{e_1 \to e_1'}
{(e_1 \; e_2) \to (e_1' \; e_2)}
$$

EAGER
$$
\frac
{e_2 \to e_2' \quad e_2 \ne e_2'}
{(\lambda x . e_1) e_2 \to (\lambda x . e_1) (e_2')}
$$
> Does NOT account for any infinite looping

LAZY
$$
\frac
{A,x:e_2 ; e_1 \to e_1'}
{A; (\lambda x. e_1) e_2 \to e_1'}
$$


$$
(\lambda x.y) \left[ (\lambda x.x) [ (\lambda x . xx) (\lambda x . xx) ] \right]
$$

LOLCODE example

Our rules are:

AXIOM
$$
\frac
{}
{A; n \to n}
$$

$$
\frac
{A; e_1 \to v_1 \quad A; e_2 \to v_2 \quad v_3 \; \text{ is } v_1 + v_2  }
{\text{SUM of} \; e_1 \; \text{AN} \; e_2}
$$

$$
\frac
{A; e_1 \to v_1 \quad A, \text{var} \; : v_1 ; e_2 \to v_2 }
{\text{I has a var itz} \; e_1 \; \backslash n \; e_2}
$$

$$
\frac
{A ( \text{var} ) = v}
{A; \text{var} \; \to v}
$$

> [!Example]
Using the rules given below, show that $1 + (2 + 3) \to 6$

$$
\frac{}{n \to n} \qquad \frac{e_1 \to n_1 \quad e_2 \to n_2 \quad n_3 \; \text{is} \; n_1 + n_2}{e_1 + e_2 \to n_3}
$$

We can prove this as follows:
$$
\frac{1 \to 1 \quad \frac{2 \to 2 \quad 3 \to 3 \to 5 \; \text{is} \; 2 + 3}{(2 + 3) \to 5} \quad 6 \; \text{is} \; 1 + 5}{1 + (2 + 3) \to 6}
$$

---

*Operational Semantics will be very useful in building an evaluator!*
> We can follow operational semantic rules to write evaluators for our code! Each hypothesis in our operational semantic can be parsed through to build our evaluator.


Lexing (REGEX) -> Parsing (CFGs) -> Evaluating (OpSem)


# Building a Programming Language
This article details the process of building a programming language, from reading its syntax, to making meaning from it. Note that there are far more complex ideas with 
