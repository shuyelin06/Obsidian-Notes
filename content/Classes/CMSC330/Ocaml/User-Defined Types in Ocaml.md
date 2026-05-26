---
title: User-Defined Types in Ocaml
tags:
- cmsc330
---

In this section, we describe how we can define our own user defined types in Ocaml. There are two primary ways to go about this - using **variants**, and using **records**.

# Variants
In Ocaml, a **variant** is a datatype representing a value that can be one of several possibilities. Variants in Ocaml are analogous to enumerators in other languages.

To define a variant, we use the `type` keyword followed by a `|` delimited list of possible values. We can also assign data to a variant possibility by using the `of` keyword, followed by the type to assign.

```ocaml
(* define a variant *)
type [Type] = [Value1] | [Value2] | ... | [ValueX]

(* define a variant Coin which can either be Heads or Tails *)
type coin = Heads | Tails
(* define a variant Color, which can be Red, Green, or Blue,
   each with an associated integer value *)
type color = Red of int | Blue of int | Green of int ;;
```
> Variant types must begin with a lowercase letter.

Note that we can use a variant in its own definition! This can be used to create recursive data structures, which may be useful in creating LinkedLists, Trees, and more.

```ocaml
type tree = Node of int * tree * tree | Leaf ;;
type lst = List of int * lst | ListEnd ;;
```

To assign a variable to a variant type, we use the name of a variant possibility, followed by a value if that possibility has associated data.

```ocaml
let a = Heads ;; (* a is Heads of type coin *)
let b = Tails ;; (* b is Tails of type coin *)

let r = Red(3) ;; (* r is Red with value 3, of type color *)
let g = Green ;;  (* INVALID - Green has associated data *)
```

Variants can be used in pattern matching operations! To pattern match with a variant, we list the variant's possibilities as patterns to match with.

```ocaml
(* match variable of type coin *)
let _ = match a with
    | Heads -> print_string "Heads!"
    | Tails -> print_string "Tails!" ;;

(* match variable of type color *)
let _ = match r with
    | Red(x) -> x
    | Green(y) -> y
    | Blue(z) -> z ;;
```

> [!Example]+ Example: Variants
> Below, we create a variant of type `tree` representing a Tree datastructure, and define a function to recurse through it using inorder traversal.
>
> ```ocaml
> type tree = Tree of int * tree * tree | Leaf ;;
>
> let rec print_all t =
>     match t with
>        | Tree (v, left, right) ->
>           let _ = print_all left in
>           let _ = print_int v in
>                   print_all right
>        | Leaf -> ()
> ```

# Records
Another way to define a new type is Ocaml is to use **records**, which represents a composite of other data types, where each type has an associated name. Records in Ocaml are analogous to structures in other languages.

To define a record, we use the `type` keyword, followed by a `;` delimited list of `Name: Type` pairs, denoting a particular field of the record, and its type.

```ocaml
type <record-name> =
    { <field> : <type>;
      <field> : <type>;
      ...
    }

type player =
     {
        health: int;
        defense: int;
        attack: int;
     } ;;
```

Then, to create an instance of a type, we use braces `{ }` containing a `;` delimited list of `Field = Value` pairs, assigning a value to each field of the record. Then, to access fields of the instance, we can use the `.` operator.

```ocaml
let p1 =
    {
       health = 1;
       defense = 2;
       attack = 10;
    } ;; 

let h = p1.health ;;  (* h is 1 *)
let d = p1.defense ;; (* d is 2 *)
let a = p1.attack ;;  (* a is 10 *)
```

To define a record with generic types, we need to specify what generic types are to be used in the record, before it's name.

```ocaml
type ('a, 'b) graph =
     {
        var1 : 'a ;
        var2 : 'b ;
     } ;;
```

