---
title: Tail Call Optimization
tags:
- cmsc330
---

# Tail Call Optimization
When calling a function, recall that languages will need to add a new stack frame onto the stack. While this is necessary, it is also why recursive functions are sometimes not the best, as the high number of stack frames that need to be created leads to substantial overhead!

This concept of stack frames is precisely the reason why recursion is possible, as it allows each recursion to maintain its own unique local stack!

However, what if our recursive call was the **last operation made in the function**? In this case, it's actually not necessary to create a new stack frame, as we won't need to keep a copy of the function's local data after it finishes recursing! Because of this, we may actually be able to **replace** the current stack frame with the new recursive call, instead of making a new one altogether!

This idea is known as **tail call optimization**, and is actually implemented in a variety of languages! By creating **tail recursive functions**, or in other words, functions whose last operation is the recursive call, we can avoid allocating a new stack frame for each function and avoid a lot of overhead!
> When we write tail recursive optimizations, the compiler of languages supporting tail call optimization will notice this, and implement the optimization at compile tile.

Consider the following example.

> [!Example]+ Example: Tail Call Optimization
> For example, consider the simple fibonacci function
> ```ocaml
> let rec fib n =
>     if n <= 1 then 1
>     else fib(n-1) + fib(n-2)
> ```
> 
> This function is **not tail recursive**, as it must recurse twice, and then add the results together! If we instead rewrote the `fib` function as
> 
> ```ocaml
> let rec fib n a b =
>     if n <= 1 then b
>     else fib (n-1) b (a + b)
> ```
> 
> Then, because the last thing done is the recursive call, our function is tail recursive! So, our compiler can optimize this to only use one stack frame, making our second function much faster than the first!