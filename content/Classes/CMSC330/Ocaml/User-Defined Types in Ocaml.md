---
title: User-Defined Types in Ocaml
tags:
- cmsc330
- wip
---

# tpyes to Ocaml

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

