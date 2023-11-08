---
title: Building a Programming Language
tags:
- cmsc330
---

This article details how we can build our very own programming language from scratch, and the various stages needed to make this happen.

At their core, programming languages are just a combination of symbols and rules which bind these symbols together to make meaning. Thus, given an expression $E$ from some language, **what are the rules for the language**, and **how can we implement these rules to meaning from our expression**?

To do this, we will go through the following stages:

| Stage | Description |
| - | - |
| **Lexing** | Verify that all symbols in the language are valid and form tokens | 
| **Parsing** | Verify that the grammatical structure of the tokens is valid |
| **Evaluating** | Derive meaning from the grammatical structure of the tokens |

We describe each of these stages in depth below.

---

# Lexing Stage
At their core, programming languages consist of a combination of letters variety of letters



- **Parsing**:
- **Evaluating**:

Suppose w ehave rule $E -> PRODUKT OF A AN E$,
so we parse PRODUKT, OF, call parse_A, then AN, then call parse_E.




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