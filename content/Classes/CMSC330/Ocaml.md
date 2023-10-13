---
title: Ocaml Programming Language
tags:
- work-in-progress
---

*Note*: Ocaml does not need `;;`, though we will use it for clarity.

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

> [!Example]
> ```ocaml
> let x = 4 in let y = 3 in x + y ;;
> (*           ------------------ Scope of X *)
> (*                     -------- Scope of Y *)
> ```
>
> There is also the concept of shadowing in Ocaml.
> ```ocaml
> let x = 4 in let x = 5 in x + x ;;
> (*
> Gives us this:
> x = 4
> { x = 5
>   x + x
> }
> Note that this shadowing does not remove our original definition of x.
> *)
> ```

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


Some operators are generic and support a wide variety of operands, given both arguments are the same type (`>, <, =`). We call these operators **generics**.
```ocaml
(e1:t > e2:t): bool
(e1:t < e2:t): bool
(e1:t = e2:t): bool
(e1:t <= e2:t): bool
(e1:t >= e2:t): bool
```
> note that `=` is equality. `==` is **physical equality**, meaning we compare the memory addresses.
>
> Using a generic in a function will return `'[char]` as the type, signifying some type that must match with any others whose type is also `'[char]`.
> ```ocaml
> (* 'a -> 'a -> 'b -> 'b -> bool = <fun> *)
> let f w x y z = x > w || y < z in f ;;
> ```
> > Note that there is nothing saying `w x` and `y z` need to be the same type, hence the different characters for their type. 


Other operators have very strict typing.
```ocaml
(e1:int + e2:int):int (* adds two ints *)
(e1:int - e2:int):int (* subtracts two ints *)
(e1:int / e2:int):int (* divides two ints *)
(e1:int * e2:int):int (* multiplies two ints *)

(e1:float +. e2:float):float (* adds two floats *)
(e1:float -. e2:float):float (* subtracts two floats *)
(e1:float /. e2:float):float (* divides two floats *)
(e1:float *. e2:float):float (* multiplies two floats *)

(e1:bool && e2:bool): bool (* logical and *)
(e1:bool || e2:bool): bool (* logical or *)
(not e1:bool):bool (* logical negate *)

(e1:string ^ e2:string):string (* concatenates two strings *)
```

In ocaml, type inference depends on the types of the operators we are using!! Ocaml will infer what the types of our expressions are, given the operands being used.

```ocaml
(* int -> int -> int = <fun> *)
let f x y = x - y in f ;;

(* notice how when we change the operator, ocaml
   knows that our type changes *)
(* float -> float -> float = <fun> *)
let f x y = x -. y in f ;;
```

> [!Example] Type Inference in Ocaml
> Because Ocaml supports rigid type inference, we can deduce the types of expressions (and parameters) purely based on their operands.
> 
> ```ocaml
> (* 'a -> 'a -> bool = <fun> *)
> let ex1 = fun a b -> b < a ;;
>
> (* int -> int -> bool = <fun> *)
> let ex2 = fun a b -> b + a > b - a ;;
>
> (* int -> int -> string -> int = <fun> *)
> let ex3 = fun a b c = -> (int_of_string c) * (b + a) ;;
>
> (* int -> int -> bool -> int list = <fun> *)
> let ex4 = fun a b c = [a + b ; if c then a else a + b]
> ```

# tpyes to Ocaml
## Functional Programming

## Ocaml Environment

## Functions and Expressions
```ocaml
(* function syntax *)
let [name] [arg1] [arg2] [...] = [expression]
(* anonymous function *)
fun [arg1] [arg2] [...] -> [expression]

(* equivalent *)
let f x t = x - y ;;
let f = fun x -> fun y -> x - y ;;
```

To make a function recursive, we need to use the `rec` keyword.
```ocaml
(* simple gaussian sum function, assuming x is greater than 0 *)
(* the recursive call would not be allowed without the rec keyword *)
let rec sum x = if x = 0 then 0 else x + sum (x - 1) ;;
```
> Note that we can add the `rec` keyword even if our function is not actually recursive.

## Data Structures in Ocaml
Lists are built into ocaml and are the default data structure.

To define a list, we use `[ ]`, and separate each item with a semicolon. Note that the empty list, sometimes called `nil`, is of type `'a list` (generic type).
```ocaml
[e1:t ; e2:t ; ... en:t]:t ;;

(* int list = [1; 2; 3; 4] *)
[1 ; 2 ; 3 ; 4] ;;
```
Lists must be homogeneous - in other words, all elements in the list must be the same type.
> In the backend, ocaml implements these lists as LinkedLists. Note that we can nest lists within one another (sizes don't matter in lists).

Note that because functions are just like any other type, we can have lists of functions as well! If this occurs, **all functions in our list must have the same type**.
```ocaml
let f = fun x -> x + 1 ;;
let g = fun y -> y - 1 ;;
[f ; g] ;;
```

To operate on list, we have the `cons` operator (`::`), which will add an item to the front of the list (not in place - returns a new list as all data types are immutable).
```ocaml
(e1:t :: e2:t list): t list

(* adds 1 to list [2;3;4] to yield [1;2;3;4] *)
1::[2 ; 3 ; 4] ;;
```

We can also concatenate two lists together using the append operator (`@`).
```ocaml
(e1:t list @ e2:t list):t list
[1;2;3]@[2;3;4] (* [1;2;3;2;3;4] *)
```

Ocaml treats lists as being recursive in nature. All lists are equal to an item `cons` with a list. Thus, to work with lists, we have the `head` of a list representing the first element of the list, and the `tail` representing the other elements.

We can use this with **pattern matching**, using a `match` keyword to specify which expressions we need to match with. `match` returns the result of whatever expression is matched with.
```ocaml
(match e1:'a with
       p1 -> e2: 'b
       | p2 -> e3: 'b
       | p3 -> e4: 'b
       ...):'b

(* matches with 3, returning string "nom" *)
match 3 with
      1 -> "hi"
      | 2 -> "bye"
      | 3 -> "nom" 
      | 4 -> "agga" ;;

(* use x to specify a default case *)
(* no match, defaults to x to give us string "x" *)
match 3 with
      1 -> "hi"
      | 2 -> "bye"
      | x -> "x" ;;
```
> We can think of `match` like the `switch` statement! Note that our element to match `e1` can be an expression, which will be evaluated first before matching with anything.

Match attempts to match patterns top-down - so, order of patterns we give is important.

> [!Info]
> The `in` operator limits the scope of a definition (variable or function) to the following expression.
>
> `let x = e1 in e2 ;;`
> > `x` is only bound in expression `e2`. Without in, `x` has global scope.

We can use `match` with lists, and use the `cons` operator for pattern matching
```ocaml
match [1;2;3] with
      [] -> -1
      | h::t -> h;; (* matches a list with a head and a tail (returns 1 here) *)
```

This works because of our recursive definition of a list.
```ocaml
(* all equivalent *)
[1;2;3]
1::[2;3]
1::2::[3]
1::2::3::[]
```

We can use this to do things with lists!
```ocaml
(* returns the length of a list using pattern matching
    and recursion *)
let rec len lst = match lst with
    [] -> 0
    | h::t -> 1 + len t ;;
```
> We can use the wildcard character `_` to specify we aren't going to use the variable.

---

To create a **tuple** in ocaml, we use the `( )` operators. Tuples are defined by their type, AS WELL AS THEIR SIZE.

Tuples can be heterogenenous - they can have varying types inside them.
```ocaml
(e1:'a , e2:'b , ... en:'x): 'a * 'b * ... * 'x

(* not the same types!! *)

(* string * int *)
("hiya", 2)

(* int * int *)
(1, 2)

(* int * int * int *)
(1,2,3) 
```

We can use pattern matching to break down a tuple as well! Tuples will match if the types and length of the patterns are the same
```ocaml
(* int * int -> int = <fun> *)
let f = match f with
      (x,y) -> x + y ;;
```

---

We can also define **variants**, which are analogous to enums. Variants let us define custom data types.

The syntax of a variant is as so:
```ocaml
type [name] = Value1 | Value2 | ... | ValueX

type coin = Heads | Tails

(* we can use the `of` keyword to associate a datatype with a value (or range of values)! *)
(* Red, Blue, Green must all be ints *)
type color = Red of int | Blue of int | Green of int ;;
type rbg = Hue of color * color * color ;;
```

We can pattern match with variants! From before,
```ocaml
match Red(255) with
Red(x) -> x
| Green(y) -> y
| Blue(z) -> z ;; (* 255 *)
```

> [!Example] Functions in Ocaml
> Write a function that will calculate the $n^{th}$ fibonacci number.
> ```ocaml
> (* Naive Recursive Solution *)
> let rec fib x =
>     if (x == 0) || (x == 1) then x else fib (x - 1) + fib (x - 2) ;;
> 
> let fast_fib x =
>     let rec helper first second num =
>         if (num == 0) then second else helper second (first + second) (num - 1)
>            in helper 0 1 (x - 1) ;;
> ```

---

### Higher Order Functions in Ocaml
Map function in ocaml!
```ocaml
(* 'a list -> ('a -> 'b fun) -> 'b list = <fun> *)
let rec map lst f = 
    match lst with
          [] -> [] 
          | h::t -> (f h)::(map t f) ;;
```

Fold (reduce) function in Ocaml.
```ocaml
(* 'a list -> ('b -> 'a -> 'b fun) -> 'b -> 'b = <fun> *)
let rec reduce lst f init =
    match lst with
          [] -> init 
          | h::t -> reduce t f (f init h) ;;

(* fold right *)
let rec fold_right f lst a =
    match lst with
          [] -> a
          | h::t -> f h (fold_right f t a) ;;

let rec map_with_reduce lst f = 
    reduce lst (fun x y -> (f y)::x) [] ;;
```

> ```ocaml
> type 'a tree =
>  | Leaf
>  | Node of 'a tree * 'a * 'a tree ;;
>
> let rec fold_tree f init tree = 
>     match tree with
>     | Leaf -> init
>     | Node (left, n, right) -> f (fold_tree f init left) n (fold_tree f init right) ;;
>
> let tree_a = Node(Node(Leaf, "Hello", Leaf), " World", Node(Leaf, "!", Leaf)) ;;
> fold_tree (fun l s r -> l ^ s ^ r) "" tree_a = "Hello World!" ;;
>
> let rec map_tree f t =
>     match t with
>     | Leaf -> Leaf
>     | Node (l, n, r) -> Node( map_tree f l, f n, map_tree f r ) ;;
>
> let tree_b = Node(Node(Leaf, 5, Leaf), 6, Leaf) ;;
> map_tree string_of_int tree_b = Node(Node(Leaf, "5", Leaf), "6", Leaf) ;;
> ```

---

`_` is used as a placeholder variable name, indicating that it will not be used (discarded).

```
(* returns 2, but also prints something at the
   same time - may be useful *)
let _ = print_int 3 in 2 ;;
```

---

**tail call optimization**: An optimization we can do, if the last thing we do is recurse. Consider the followig example.

In some recursive sequences )such as fold), we will create numerous stack frames until we finish our recursion. However, for every recursive call, we don't actually need the extra stack frames needed!

Instead, we can **replace** the current stack frame with the new stack frame to be recursively called, minimizing the memory usage of our recursive function!
> Tail call optimization is the method in which we avoid allocating a new stack frame for a function, because the calling function will simply just return the value it gets from the called function.

Tail call automatically occurs, if we make our recursive call the **last thing to happen** - in other words, after performing the operations, the very last thing to be done is the recursive call, which the functino will then return.

The ocaml compiler will notice this, and will replace the current stack frame of the function to save memory. This is a compiler optimization!

Consider the simple fibonacci function
```ocaml
let rec fib n =
    if n <= 1 then 1
    else fib(n-1) + fib(n-2)
```

This function is NOT tail recursive, as it must recurse twice, then add the results together! If we instead rewrote the `fib` function as
```ocaml
let rec fib n a b =
    if n <= 1 then b
    else fib (n-1) b (a + b)
```

Because the last thing done is the recursive call, our funciton is tail recursive! So, our compiler can optimize this to only use one stack frame.

---

Datatypes, trees and variance
> `unit()` is analogous to a void return type - it is a tuple of size 0. It means there's no meaningful data to be had from the function.

Let's create a tree with variants!

```ocaml
type tree = Node of int * tree * tree | Leaf ;;
type lst = List of int * lst | EmptyList ;;
```
> Some other languages (racket, Lisp) actually implement lists as this!

We can use the `when` keyword to make pattern matching even more complex.
```ocaml
(* matches only when left is = Leaf *)
match ...
| Node(v,left,right) when left = Leaf -> ...
```