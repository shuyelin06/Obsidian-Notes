---
title: The Ocaml Programming Language
tags:
- cmsc330
---

This article serves as brief documentation for the **Ocaml Programming Language**. It is by no means comprehensive; for full documentation, refer to the official documentation [here](https://v2.ocaml.org/manual/).

Ocaml is a **functional programming language**. While more recent versions of Ocaml have allowed object-orientated programming paradigms, these notes will only focus on Ocaml's functional uses, per its original intended use.

# Introduction to Ocaml
## My First Ocaml Program
To create an Ocaml program, we will first create a file with the `.ml` extension. Below, we create a hello world program, which prints `Hello World!`.

```ocaml
(* hello_world.ml *)
let _ = print_string "Hello World!"
```

Note how unlike other programming languages, Ocaml lacks any main method. In fact, programs in Ocaml do not start with a main method - they simply run from the top of the file down to the bottom.

## Compiling Ocaml Programs
Like many other languages, Ocaml is a **compiled language**. This means that to run the program, we need to first  **compile** our file into something we can execute and run. To do this, we use the command `ocamlc`.

```bash
ocamlc hello_world.ml -o hello_world.x
hello_world.x
```
> Include option `-o` to specify the name of the output file. Without this option, the output defaults to `a.out`.

Compiling an Ocaml program will produce the following files:
- A `.cmo` file, representing a compiled object file (like a `.o` file in C)
- A `.cmi` file, representing a interface file (like a `.h` file in C)
- An executable file, which will run our Ocaml program

## Ocaml's Read-Eval-Loop
While we can create and compile Ocaml programs to explore the language, Ocaml also has a terminal read-eval-loop we can use, which provides a convenient way to test Ocaml functions (and commands)!

To run the read-eval-loop for Ocaml, use the commmand `utop`. Note that while in `utop`, you need to end every expression with `;;` to run it.

```bash
utop
```

Apart from these commands, the following commands may also be quite useful:
- `dune`: A makefile equivalent for Ocaml
- `opam`: The Ocaml package manage


# Basic Ocaml Concepts
## Expressions in Ocaml
In Ocaml, everything is treated as an **expression**, which is code that will always evaluate to some value. All data returned by expressions is **immutable**, meaning that once any data is created, we cannot modify it - we can only create new, modified copies of it.

```ocaml
let x = 5 ;;
let _ = x + 2 + 1 ;;       (* valid, expression *)
let _ = 1 + 3 ;;           (* valid, expression *)
x = x + 1 ;;               (* invalid, statement - variables are immutable*)
```

By adding this constraint, Ocaml guarantees that our code will always do the exact same thing with the same inputs, as our behavior can no longer depend on states whose value is not known! This concept is known as **referential transparency**.
> In other languages, running a function more than once may not necessarily yield the same behavior, due to side effects.

All expressions in Ocaml have a **type**, which indicates what data the expression returns. Ocaml is a **statically implicitly typed language**, meaning that such types are inferred by the compiler at compilation, and do not need to be explicitly given by the programmer.

In order for the compiler to correctly infer the types of expressions, Ocaml imposes the following constraints:
- An expression must always return the same type.
- An operator / function must always expect the same type as input.

Because of these rigid typing guidelines, it's possible to infer what the types of expressions are based on the operators (or functions) they use! See the following section.

> [!Example]+ Example: Type Inference
> Consider the following, where we determine the validity of expressions from their expected types.
>
> ```ocaml
> let _ = if true then 2 else 3 ;;    (* valid *)
> let _ = 2 + 3 ;;                    (* valid *)
> let _ = if true then 2 else 2.0 ;;  (* invalid *)
> let _ = 4 + 3.0 ;;                  (* invalid *)
> ```
> 
> Consider the following, where we infer the type of variables from expressions.
>
> ```ocaml
> let _ = a + b ;; (* a and b must be ints *)
> let _ = if c then x else y ;; (* c is bool, x and y are the same type *)
> ```

## Ocaml Types and Operations
In this section, we describe Ocaml's base types and operators. Like many other languages, Ocaml has many distinct types.
> To create our own custom user types, refer to [[User-Defined Types in Ocaml]]

### Scalar Types
Some of Ocaml's **scalar types** (single-value types) are given as follows:
- `int`: Integer value
- `float`: Floating-point value
- `bool`: Boolean value

Ocaml supports a variety of operations using these basic scalar types. Below, we list the most common. Note that to describe types of expressions in the following sections, we use syntax `e:t` to describe that the expression `e` has type `t`. 

| Arithmetic Operator | Type | Description |
| :-: | :- | - |
| `+` | `(e1:int + e2:int):int` | Adds two integers |
| `-` | `(e1:int - e2:int):int` | Subtracts two integers |
| `*` | `(e1:int * e2:int):int` | Multiplies two integers |
| `+.` | `(e1:float +. e2:float):float` | Adds two floats |
| `-.` | `(e1:float -. e2:float):float` | Subtracts two floats |
| `*.` | `(e1:float *. e2:float):float` | Multiplies two floats |
| `/.` | `(e1:float /. e2:float):float` | Divides two floats |
| `&&` | `(e1:bool && e2:bool):bool` | Logical and |
| `\|\|` | `(e1:bool \|\| e2:bool):bool`  | Logical or |
| `not` | `(not e1:bool):bool` | Logical negate |
> We also have the operator `^`, which concatenates two strings.

### Generic Type
In addition to scalar types, Ocmal also has the **generic type** `'a` (where `a` can be any character), such that this type can be anything, but any expression with the same character returns the same type! 

| Generic Operators | Description |
| :- | - |
| `(if e1:bool then e2:'a else e3:'a):'a` | Conditional |
| `(e1:t > e2:t):bool` | Greater than |
| `(e1:t < e2:t):bool` | Less than |
| `(e1:t = e2:t):bool` | Equality |
| `(e1:t >= e2:t):bool` | Greater than or equal to |
| `(e1:t <= e2:t):bool` | Less than or equal to |
> Note that `==` (what we may be used to) actually compares **physical equality**, aka the memory addresses, and not the values themselves.

### Compound Types
Ocaml also supports **compound types**, which use a combination of scalar types. These are given as **tuples** and **lists**.

A **list** is a homogeneous collection of elements, meaning that all elements in the list must have the same type. To define a list, we use brackets `[]`, and separate each item with a semicolon `;`.
> The empty list, sometimes called `nil`, has type `'a` list.
```ocaml
(* [e1:'a ; e2:'a ; ... en:'a]:'a list *)
let _ = [1 ; 2 ; 3 ; 4] ;; (* int list *)
```

To use lists, we can use the following operators:
- The **cons operator** `::`, which can be used to add a single item to the front of the list.
- The **append operator** `@`, which can be used to merge two lists together.

```ocaml
(* (e1:'a :: e2:'a list):'a list *)
let _ = 1::[2 ; 3 ; 4] ;; (* [1 ; 2 ; 3 ; 4] ;; *)

(* (e1:'a list @ e2:'a list):'a list *)
let _ = [1;2;3] @ [2;3;4] (* [1 ; 2 ; 3 ; 2 ; 3 ; 4] *)
```

---

A **tuple** is a heterogeneous collection of elements, meaning that all elements in the tuple can have different types. To define a tuple, we use parentheses `( )`, and separate each item with a comma `,`.

```ocaml
(* (e1:'a , e2:'b , ... en:'x): 'a * 'b * ... * 'x *)
let _ = (1, 2.0, true) ;; (* int * float * bool *)
```

Tuples do not have any operations that can directly be used to manipulate them; they are fixed upon definition.

---

To extract elements of lists and tuples, we can use **pattern matching** with the `match` keyword, to match these lists or tuples with "expression patterns", containing variables which are populated with values upon a successful match.

Given a pattern, Ocaml asks if the pattern can be equivalent to the expression given. If it is, then Ocaml will populate the variables in the pattern for use. Note that pattern matching chooses the first match from top to bottom, and can be used for more than just compound data.

```ocaml
(*
(match e1:'a with
       | p1 -> e2:'b
       | p2 -> e3:'b
       | p3 -> e4:'b
       ...):'b
*)

(* using match *)
(* x is a default case - everything matches with a variable *)
let _ = match 3 with
   | 1 -> "hi"
   | 2 -> "bye"
   | 3 -> "nom"
   | x -> "woah" ;; 
   
(* matching a list *)
let _ = match [1 ; 2 ; 3] with
   | [] -> print_string "Empty List" (* empty list case *) 
   | h::t -> print_int h ;;          (* h is 1, t is [2 ; 3] *)

(* matching a tuple *)
let _ = match (2, 3.0, true) with
   | (a, b, c) -> print_int a ;;     (* a is 2, b is 3.0, c is true *)
```

Note that we can also pattern match for a specific case using a normal `let` binding (refer to the next section), where the variable name is the pattern.

```ocaml
let h::t = [1 ; 2 ; 3] ;;         (* h is 1, t is [2 ; 3] *)
let (a, b, c) = (1, 2.0, true) ;; (* a is 1, b is 2.0, c is true *)
```

## Variables and Functions in Ocaml
### Variables and Scoping
Like many other languages, Ocaml supports **variables**, which are identifiers that store a value. To create a variable, we use a `let` binding, which follows syntax `let [Variable] = [Value]`.

```ocaml
let x = 3 ;;       (* x is 3 *)
let y = "hello" ;; (* y is "hello" *)
```

Note that if we don't care about storing the value to any variable, convention is to use the wildcard variable `_` to denote we don't care about this value. This is often useful in pattern matching.

```ocaml
let (a,b,_) = (1,2.0,3) ;; (* a is 1, b is 2, we don't care about the 3rd element *)
```

As all states are immutable in Ocaml, variables cannot be modified upon creation. We can, however, **overshadow** variables by using another `let` binding, though this will not remove the original variable.

Once a variable is defined, it can be used anywhere else in the same scope. We can also limit the scope to which it is defined, by using the `in` operator, which will limit the use of the variable to the expression following `in`.

```ocaml
(* x is only bound in expression e2 *)
let x = e1 in e2 ;;

let x = 3 in x + 5 ;;           (* 8 *)
let y = (let x = 2 in x - 1) ;; (* y is 1 *)
```

> [!Example] Example: Scoping with `in`
> ```ocaml
> let x = 4 in let y = 3 in x + y ;;
> (*           ------------------ Scope of X *)
> (*                     -------- Scope of Y *)
> ```

The `in` operator can be quite handy in chaining variable definitions together (without making them global), or in creating and calling helper functions (which we'll see later).

### Functions in Ocaml
As Ocaml is a **functional programming language**, it treats functions like any other data type! This means that we can treat functions like any other variable in our program.

To define a function, use a standard `let` binding, followed by variables which are the parameters to the function. We can also do this by assigning a variable to an **anonymous function**, created using the `fun` keyword.

Types of functions are typically denoted by the syntax `t1 -> t2 -> .. -> x = <fun>`, where $t_i$ denotes the types of the function inputs (in order), and `x` denotes the type of the function output.
> The reason for this chained sequence is because of **currying**. Functions in Ocaml actually only take in one input, and return one output. However, with multiple parameters, we're defining a function that returns another function, that returns another... for as many parameters as needed.

```ocaml
(* int -> int -> int -> int = <fun> *)
let f x y z = x + y + z ;;        (* equivalent *)
let f = fun x y z -> x + y + z ;; (* equivalent *)
```

To call a function, simply use the variable name for the function, followed by all of its necessary inputs. Note that parentheses are optional, but often helpful for readability and to enforce a specific order of evaluation to occur.

```ocaml
(* from before *)
f 1 2 3 ;; (* 1 + 2 + 3 = 6 *)
```
> Interestingly enough, given this definition of a function in Ocaml, we can think of variables as just **functions with no input**!

> [!Info] Lists of Functions
> Because functions are just like any other type, we can have lists of functions as well! If this occurs, **all functions in our list must have the same type**.
> 
> ```ocaml
> let f = fun x -> x + 1 ;;
> let g = fun y -> y - 1 ;;
> [f ; g] ;;
> ```

Note that as functions are also just variables, the `in` keyword can also be used with them too! Many times, this is used in writing functions that use helper functions, which is often necessary when writing **recursive functions**.

While functions in Ocaml by default do not support recursion, we can allow recursion by adding the `rec` keyword before the function name. 

```ocaml
(* computes the factorial of n using recursion *)
let rec factorial n =
    if n == 0 then 1 else n * factorial (n - 1)

(* iterates and prints all the elements of an int list *)
let rec print_list lst =
    match lst with
       | [] -> print_string ""
       | h::t -> let _ = print_int h in (print_list t)
```
> When writing recursive functions, note that it's possible to optimize their runtime through [[Tail Call Optimization]].

Consider some examples of type inference in Ocaml, now using functions.

> [!Example]+ Example: Type Inference of Functions in Ocaml
> ```ocaml
> (* int -> int -> int = <fun> *)
> let f1 a b = a + b ;;
>
> (* bool -> 'a -> 'a = <fun> *)
> let f2 a b c = if a then b else c ;;
>
> (* int -> int -> string -> int = <fun> *)
> let f3 = fun a b c = -> (int_of_string c) * (b + a) ;;
> ```