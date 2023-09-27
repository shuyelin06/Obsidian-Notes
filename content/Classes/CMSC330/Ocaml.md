---
title: Ocaml Programming Language
---

A **programming paradigm** is a classification of programming approaches baed on behavior of code. They represent ways of thinking.
> Typically, we use paradigms interchangeably with language features.

**Functional programming** is a programming paradigm focused around functions. 

In these notes, we discuss functional programming, and implement it with **Ocaml**.
> Note that while Ocaml supports object-orientated programming, we only focus on its functional uses.

# Features of Functional Languages
All functional languages find their derivation from **lambda calculus**, and often can have their origins traced back to **Lisp**, one of the most major functional languages.

Properties of functional languages are given below.
- **Immutable State**: States are always immutable in functional languages. We cannot reassign a state upon
- **Declarative Programming**: Must declare what we're going to do?
- **Referential Transparency**: Lets us inductively prove that our algorithm is doing what its doing correctly, allowing us to minimize side effects and guarantee a program works.
- **Realistic about the Machine**: ?

## Immutable State
**Program state** represents the state of the machine at any given time. This is typically described as the contents of variables.

In **imperative languages**, state is mutable, and can be destroyed / changed in some way (ex. variable reassignment). This can cause many side effects - in other words, reliances on data outside the program which can make it difficult to reason about the machine.
> These side effects have no **referential transparency**, as we cannot treat functions as normal mathematical functions.
> 
> For example, in imperative languages, we cannot ensure `f(x) + f(x) == 2 * f(x)` due to side effects.

Thus, immutable state will let us minimize side effects.

## Declarative Programming
In **declarative programming**, it is up to us as a programmer to tell the computer what we need. However, instead of telling the machine exactly what to do, we just tell it what we want and let the machine decide how to do it itself.
> We tell the machine what we want to do, and the machine will figure out the rest.


# Our first Ocaml Program
To create an ocaml program, we create a file with the `.ml` extension.

The below program prints hello world to the console.
```ocaml
(* hello_world.ml *)
print_string "Hello World!\n"
```
> Note that there is no main function, function calls do not need parentheses.

To run this program, we need to compile our file before running it. Ocaml is a compiled language.

```bash
ocamlc hello_world.ml
```
> Include option `-o` to specify the name of the output file. Without this option, the output defaults to `a.out`.

Compiling the program wil give us the following:
- `.cmo`: Compiled Object (like `.c` file)
- `.cmi`: Compiled INterface (like a header file)

Ocaml also has a read-eval-loop in the terminal, which we can use to run statements in the terminal.

```bash
ocaml

utop # ocaml but better
dune # like makefiles
opam # package manager for ocaml
```
> In utop, we need `;;` to end expressions.

---

Recall the difference between syntax and semantics...

In ocaml, everything is an **expression**, which will always evaluate to or return a value. All values are expressions, but not vice versa. Ocaml does not have statements 
> Our goal in ocaml, is to combine expressions into larger expressions.

```
x + 2 + 1 # expression
1 + 3 # expression
x = x + 1 # statement, not allowed
```

All expressions have a **type**. Ocaml is a statically typed language (types evaluated at compile time) and is also implicitly typed (don't need to explicitly specify a type).
> For clarity, we will use syntax `e: t` to denote that expression `e` has type `t`.

```ocaml
4: int
1 + 3: int
1 + 3.0 # INVALID expression
```
> We CANNOT perform operations between different types. We can, however, cast values to other types.

```ocaml
1 + int_of_float 3.0 ;;
```
> `+` only works with integers. We have to use the `+.` operator to add floats.
>
> For example, `1.0 + 3.0` is invalid, but `1.0 +. 3.0` is.

Part of ocaml's type checker is something that does type inference.
> Ocaml supports booleans `true` and `false`. Unlike C, these booleans are the only values that can be evaluated in conditionals (they are NOT treated as any other number).

---

The `+` expression in ocaml
```ocaml
(e1:int + e2:int):int
```
> Ocaml types are extremely strict! Types MUST match, and if they do not, the program will not compile.

The `if` expression in ocaml takes the following:
```ocaml
(if el:bool then e2:t else e3:t):t

if true then 2 else 3 (* 2 *)
(if true then 5 else 2) + 3 (* 5 + 3 = 8 *)
if true then 2 else "a" (* INVALID: TYPE MISMATCH *)

(* We can recursively nest expressions! *)
if if true then false else true then 3 else 5
if (if true then false else true) then 3 else 5
```
where `t` is some type.
> because expressions MUST always return the same type, the `if` statement must always have an else branch. Notice that we're just combining expresions to form larger expresions.

---

in ocaml, functions are expressions, so we can use them as we would like an other expression! To define a function, we need to know how to define a variable (as functions are just variables!)

See the below variable definition
```ocaml
let x = 3 (* defines an immutable global variable x *)
```

We can do something similar to define a function
```ocaml
let f x1 x2 x3 ... = e (* f - function name, x1 x2 x3 - parameters, e - expression *)
(* defines a function f that takes an argument x, and returns x + 5 *)
let f x = x + 1 (* defines a function type int -> int *)
```
> A variable is really just a function with no parameters that returns a value!
> 
> `let f = 3` (function that returns 3)

The `in` keyword to define the return value of the expression.  When using this keyword, our definition can only be used in the line it is defined.
```ocaml
let f x = x + 1 in f 5 (* 6 *)
```

We can also define functions with multiple parameters!
```ocaml
let f x y z = x + y + z (* int -> int -> int = <fun> *)
```
> 3 parameter function
>
> The reason why we have a chained `int -> int` is because of currying. We have a function that returns a function that returns a function... etc.
>
> Functions take in one thing, and return one thing. We're simply defiing a function that returns another function (and so on and so forth).

```ocaml
let f x y = x + y
let g = f 5 (* g is now the function (5 + y) *)
g 2 (* 7 *)
```
> we can also define anonymous functions!
>
> ```
> (fun e1:t -> [expression)
> ```

> Interesting note, all operands that work on floats msust be appended by a `.`
> For example, `*., /., +.`.


Some operators are generic and support a wide variety of operands, given both arguments are the same type (`>, <, =`)
```ocaml
(e1:t > e2:t): bool
(e1:t < e2:t): bool
(e1:t = e2:t): bool
(e1:t <= e2:t): bool
(e1:t >= e2:t): bool
```
> note that `=` is equality. `==` is **physical equality**, meaning we compare the memory addresses.

# tpyes to Ocaml
## Functional Programming

## Ocaml Environment

## Functions and Expressions