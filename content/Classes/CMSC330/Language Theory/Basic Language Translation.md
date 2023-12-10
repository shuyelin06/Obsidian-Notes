---
title: Basic Language Translation
tags:
- cmsc330
---

# Language Translation
## Introduction
Consider the event where we take some source file for a programming language, and run a compiler or interpreter on it. For example, say I'm executing a C program from `main.c`.

```bash
gcc main.c -o main.x
main.x
```

At a high level, regardless of the language, or use of compiler / interpreter, we're really just doing the same thing: we're taking a text file, and converting it into another language. This is known as **language translation**.

This language may or may not be executable by the machine - for instance, in the case of C, the compiler does not generate machine readable code, but actually generates an intermediate language in the form of object files (`.o`) that can be assembled into machine code.

While language translation can be quite complex, there are stages which are absolutely necessary for it to occur, regardless of whether you're using a compiler or interpreter.

In this article, we discuss these core stages of translation, as well as how to use them to build a programming language of our own! 

## Stages of Language Translation (Overview)
To build our own programming language, we ask the following questions:
1. How do we build rules describing the grammatical structure of our language?
2. How do we build rules describing the semantical meaning of our language's expressions?
3. How do we implement these rules in practice?

Each of these questions will be answered in the following 3 stages of language translation. Note that while there can be many more stages, these 3 are the core stages that nearly all compilers / interpreters have.

| Stage | Description |
| - | - |
| **Lexing** | Verify that all symbols in the language are valid and form tokens | 
| **Parsing** | Verify that the grammatical structure of the tokens is valid |
| **Evaluating** | Derive meaning from the grammatical structure of the tokens |

We describe each of these stages in depth below.

# Stage 1: Lexing
Given any expresion or statement, we're really just seeing a combination of lettrs

## Regular Expressions

# Stage 2: Parsing
## Context Free Grammars

# Stage 3: Evaluating
After verifying the grammatical strucutre of our expression through parsing and receiving some tree representing the expression, we need to determine how we can use this tree to derive meaning from our expression.

Consider the following english statement:
```python
"Colorless green ideas sleep furiously"
```
While every word is valid, and the sentence is grammatically correct, it does not have meaning!

The evaluator's purpose is to ensure that such statements have valid meaning, and in some cases, evaluate the statement. We can achieve both of these goals using **operational semantics**, described below.

## Operational Semantics
### Operational Semantic Rules
**Operational semantics** is a method of defining the meaning of a program by describing how it operates. It seeks to "prove" that a statement has meaning, by breaking it down into statements we can show are true.

We do this using **argument forms**, which are rules which define a conclusion $C$ to be true, given that its hypotheses $H_1, \dots H_n$ are true. These hypotheses may be proven using argument forms of their own, and we denote a rule as the following:
$$
\frac{H_1 \quad H_2 \quad \dots \quad H_n}{C} 
$$

In our case, we will be using the following syntax:
- **Values** will be denoted as $v$
- **Expressions** in our language will be denoted as $e$
- **Environments** will be denoted as $A$

Consider the following operational semantic rule definition.

> [!Example]+ Example: Example Addition Rule
> Let's define addition in our language. Note that in this language, we don't necessarily have to use the conventional $+$ symbol - we could use anything, like $?$!
> $$
> \frac{e_1 \to v_1 \quad e_2 \to v_2 \quad e_3 \; \text{is} \; v_1 + v_2}{e_1 \; ? \; e_2 \to n_3}
> $$

Note how in the above example, we're still using the $+$ sign to describe addition, despite defining it as $?$ in our language. This is because the language our hypotheses is using is different from our actual language!

In any rule, such as the above example, the language we express our hypotheses in is called the **meta-language**. We use this language to describe our target language in a way we can understand, or in a way that can be easily implemented! 

Of course, these rules on these own won't be able to do anything, as they lack any base case (how do we know that $e_1 \to v_1$?) Thus, every operational semantic ruleset must have base cases, known as **axioms**, statements which we take as granted to be true.

Axioms are denoted as conclusions without any hypotheses that need to be fulfilled (making them vacuously true).
$$
\text{Axiom} \qquad \frac{\quad \quad}{C}
$$

Now, using our rules with base axioms, we can prove that statements in our language are valid, and derive meaning from them!

> [!Example]+ Example: Simple Operational Semantic Proof
> Consider the following operational semantic rules.
> $$
> \frac{}{n \to n} \qquad \frac{e_1 \to n_1 \quad e_2 \to n_2 \quad n_3 \; \text{is} \; n_1 + n_2}{e_1 \; ? \; e_2 \to n_3}
> $$
> Where $e_i$ denotes some expression in our language, and $n$ denotes some integer number.
>
> Prove the statement $4 \; ? \; 5 \to 9$ using our operational semantic definition.
>
> To prove this, we will begin with our statement $4 \; ? \; 5 \to 9$ at the bottom, and match it with our operational semantic rules to show that it is valid.
> $$
> \frac{\frac{}{4 \to 4} \quad \frac{}{5 \to 5} \quad 9 \; \text{is} \; 4 + 5}{4 \; ? \; 5 \to 9} 
> $$
> > While this is a really simple example, these rules can quickly create extremely complicated behavior! 

> [!Example] Example: Operational Semantic Proof
> Using the rules given above, show that $1 + (2 + 3) \to 6$.
> 
> $$
> \frac{\frac{}{1 \to 1} \quad \frac{\frac{}{2 \to 2} \quad \frac{}{3 \to 3} \quad 5 \; \text{is} \; 2 + 3}{2 + 3 \to 5} \quad 6 \; \text{is} \; 1 + 5}{1 + (2 + 3) \to 6}
> $$

Below, we discuss some important features we could add to our operational semantic language, which are common in many languages.

### Feature 1: The Environment and Variables
Let's add some more complexity to our language. Many languages have a concept of **variables**, which can store values, and be used in place of the values throughout the program.

```python
x = 2 + 3 # binds variable x to the value 5
```

When a language does a variable binding, this variable binding is saved to something called the **environment**, which can later be used to see what a variable is bound to, in a process called a **lookup**.

To account for the addition of an environment, our operational semantic rules will have the environment prepended to them with the syntax `A;`, where values can be added to the environment with the comma `,` operator.

Furthermore, we define the following two operations with our environment:
1. A **lookup**, where we use the environment to obtain the value of a variable, denoted in the rule
   $$
   \frac{A, x : v; (x) \to v}{A, x : v; x \to v}
   $$

2. A **variable binding**, where we save a variable binding to our environment for later lookup.

   While there are numerous ways to represent this, in our case we will be doing this with the `let` and `in` keywords, where we bind a value to a variable, then evaluate another expression with this new environment.
   $$
   \frac{A; e_1 \to v \quad A, x : v; e_2 \to e_3}{\text{let} \; x = e_1 \; \text{in} \; e_2 \to e_3}
   $$

Consider the following examples with the environment.

> [!Example]+ Example: Environment Rules
> Given the aforementioned environment rules, with the rule for addition
> $$
> \frac{A;e_1 \to v_1 \quad A;e_2 \to v_2 \quad v_3 \; \text{is} \; v_1 + v_2}{e_1 + e_2 \to v_3}
> $$
> 
> Prove that statement `let x = 3 in x + 4` is equal to 7.
> 
> We begin from our expression, and apply our operational semantic rules.
> $$
> \frac{\frac{}{A; 3 \to 3} \quad \frac{\frac{A,x:3; (x) \to 3}{x \to 3} \quad \frac{}{A, x:3; 4 \to 4} \quad 7 \; \text{is} \; 3 + 4}{A,x:3; x + 4 \to 7}}{A; \text{let} \; x = 3 \; \text{in} \; x + 4}
> $$
> 
> Note that when making these proofs, its easier to first apply our rules, and then fill in results after starting from our axiom base cases.


## Feature 2: Conditionals and Booleans
Let's add even more complexity to our language. Many languages have a concept of **conditionals** and **booleans**, which let it change behavior based on some input.

```python
if True:
   print("true!")
else:
   print("false!")
```

To implement conditionals, the naive programmer would add a rule such as the following:
$$
\frac{A; e_1 \to v_1 \quad A; e_2 \to v_2 \quad A; e_3 \to v_3 \quad \text{if} \; v_1 \; \text{then} \; v_2 \; \text{else} \; v_3}{\text{if} \; e_1 \; \text{then} \; e_2 \; \text{else} \; e_3 \to e_4}
$$

However, this wouldn't be very good, as this definition of a conditional will always evaluate $e_2$ and $e_3$ no matter what $e_1$ evaluates to! This will become problematic, especially in languages where expressions produce side effects (meaning we only want to evaluate either $e_2$ or $e_3$).

To get around this, instead of creating one rule to encompass all conditionals, we will define **separate rules** for every conditional case! Let's define `true` and `false` as the true and false boolean types in our language.

Then, to implement conditionals, we would have the rules

$$
\frac{A; e_1 \to \text{true} \quad A;e_2 \to v_2 \quad v_2}{\text{if} \; e_1 \; \text{then} \; e_2 \; \text{else} \; e_3 \to e_4}

\quad

\frac{A; e_1 \to \text{false} \quad A;e_3 \to v_3 \quad v_3}{\text{if} \; e_1 \; \text{then} \; e_2 \; \text{else} \; e_3 \to e_4}
$$

These rules would ensure that only $e_2$ or $e_3$ will evaluate, as our expression will only match with one of the two rules based on $e_1$!

## Implementing an Evaluator
*How do we implement an evaluator using operational semantic rule?*

# WIP
---
Meta language for LOLCODE is ocaml as ocaml is being used to implement the LOLCODE language

`#use "cma file"` in dune will load a ocaml file for us to use!


`#load "str.cma" ;;` will load the `Str` regex module.


What if we want to add multiple types? Well, then we need to implement type checking!

Type checking can be in one or two steps: parsing or evaluation.

By rewriting our grammar, we can make it so that the initial production rule splits into either a number expression, or a true/false expression! This will ensure that our number and bool expressions are separate. This adds type checking in the parser stage. if the parser can enforce strong typing, then the evaluator doesn't need to worry about it.
> This lets us make our evaluator not need to worry about types! Most languages without static typing will have typing in the evaluator.

We may also need to build a wrapper type in our evaluator, so that our recursive function can return multiple types without conflicts occurring. This forces us to need to check the types of the variables, if they're equal, and if they work with the expression.
> This introduces overhead in the evaluator!

```ocaml
match v1,v2 with
      | NUM(v1), NUM(v2) -> v1 + v2
      | _ -> raise (Failure "Type error!")
```

$$
L \to N | T
\text{N defines numbers operations}
\text{T defines bool operations}
$$

**Bootstrapping**: writing a compiler in a language that can compile the language itself!

Main idea: Describe what a language does in terms of a META LANGUAGE, another language whose behavior we know! This will let us do virtually anything with our language (not just booleans and integers, but like anything we want, so long as we implement it with our meta language!)

Note that with booleans, conditionals and short circuiting will cause special cases to occur, where in our opsem, we should NOT be evaluating both expressions at once before evaluating the final expression (due to side-effects). Thus, we will need multiple rules such that we only check one at a time.

Consider the following opsem rule
$$
\frac
{A; e_1 \to v_1 \quad A; e_2 \to v_2 \quad A; e_3 \to v_3 \quad \text{if e1 then e2 else e3}}
{\text{if } e_1 \text{ then } e_2 \text{ else } e_3 }
$$
the issue with this rule is that no matter what $e_1$ evaluates to, $e_2$ and $e_3$ will ALWAYS run! Thus, we need multiple opsem rules for our conditional
- 1 such that $e_1$ is true, so we only evaluate $e_2$
- 1 such that $e_1$ is false, so we only evaluate $e_3$

This ensures we maintain referential transparency and minimize side effects which may cause unintended behavior.