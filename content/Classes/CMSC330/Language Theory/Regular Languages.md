---
title: Regular Languages
tags:
- cmsc330
---

This article describes **regular languages**, which describe any formal language that can be described by a regular expression.

Consider a text based problem. Oftentimes, the minimum language to solve this problem can be given in terms of a **regular expression (regex)**, which is a pattern describing a set of strings. Some examples of these problems are given below.
- Find all words in a sentence.
- Find all numbers in a report.
- Determine if the format of a phone number is correct.

These problems can be solved using the text matching capabilities of regular expressions, though the capabilities of regular expressions can extend far beyond that!

Do note, however, that regular expressions have their limitations, as they lack any concept of memory. Because of this, all symbols in regular expressions are independent of one another, and cannot establish dependencies between one another.
> This is a problem that will later be fixed in the next class of languages, Context Free Languages.

> [!Info] Note
> In the following sections, we will prepend and append our regular expression pattern string with `/` to denote a regular expression. 

We first will describe how regular expressions can be used, and then describe how they can be implemented.

# Rules of Regular Expressions
A **regular expression** is a pattern that describes a set of strings. This set of strings can then be used to determine whether or not an input string `str` is within this set, to solve a variety of problems.

To create a regular expression, we use the following base constructs that make up regular expressions.

## (1) Alphabet
First, we need to define an **alphabet**, which describes a set of valid acceptable symbols which can be used. This is commonly the english alphabet with characters $a-z$, $A-Z$, $0-9$, and other related symbols.

```python
"/a/" # Matches with the character {"a"}
"/0/" # Matches with the character {"0"}
```

## (2) Concatenation
Using this alphabet, we may want to use it to form sequences of symbols (called **words**).

This is where **concatenation** comes in, allowing us to combine our symbols to form longer words we can match against.

```python
"/hello/" # Matches with the word {"hello"}
"/bye bye/" # Matches with the word {"bye bye"}
```

## (3) Boolean
It is often the case that we'll want to match against multiple potential words, instead of just one.

This is where **boolean or** comes in, an operator which specifies an "option" a word can take when matching against a regular expression. This operation is often performed with the `OR` operator (`|`), which operates from the start of the expression to the end of the expression (or another `OR` operator).

```python
"/a|b|c/" # Matches with words {"a","b","c"}
"/gray|grey/" # Matches with words {"gray", "grey"}
```
> Note the second example, where we cannot share symbols between words split by `OR`.

### Bracket Operator
To allow us to conveniently perform an `OR` on a much wider range of characters in a range, many implementations will have a **bracket operator** (`[ ]`), allowing us to specify an ASCII range of characters.

```python
"/a|e|i|o|u/" # Matches any vowel
"/[aeiou]/"   # Matches any vowel
 
"/0|1|2|3|4|5|6|7|8|9/" # Matches with any characters from "0" to "9"
"/[0-9]/"               # Matches with any characters from "0" to "9"

"/[a-z]/"     # Matches with any characters from "a" to "z"
"/[A-Za-sz]/" # Matches with any characters from "a" to "z" and "A" to "Z"
```

Some implementations may even provide shorthand symbols to denote some of these common ranges!

```python
"/./" # Matches any possible character
"/\w/" # Matches any alphanumeric character
"/\d/" # Matches any digit
```

We can also negate bracket operators to specify characters that **cannot** be matched against, by adding the `NOT` operator (`^`) just after the opening bracket.
```python
"[^aei]" # Matches with anything but "a", "e", and "i"
```

## (4) Precedence
Note that in previous examples, we could not share characters between words, due to the scope of the `OR` operator encompassing up to the ends of the regular expresion, or another `OR` operator.

We can solve this with **precedence**, by using symbols  (commonly `( )`) to limit the scope of the `OR` operator!

```python
"/gray|grey/" # Matches with {"gray", "grey"}
"/gr(a|e)y/" # Matches with {"gray", "grey"}
```

> [!Info] Extra Precedence Symbols
> Some implementations include extra nifty symbols to force an order of characters!
>
> We can use symbols `^` and `$`, to denote the characters that must be at the start and end of the string (respectively).
> ```python
> "^[0-9]" # Must begin with a digit
> "[0-9]$" # Must end with a digit
> ```

## (5) Quantification
Finally, suppose we have a group of potential characters to match against, and we want to match against this group multiple times in a row. This can become quite annoying to type out!

To address this, we have **quantification**, symbols (`{ }`) that denote the number of repetitions of some expression that we want.

```python
"(0|1|2|3|4|5|6|7|8|9)(0|1|2|3|4|5|6|7|8|9)" # Set of all 2 digit strings
"(0|1|2|3|4|5|6|7|8|9){2}" # Set of all 2 digit strings

"(0|1|2|3|4|5|6|7|8|9){2,5}" # Set of all 2 digit to 5 digit strings (inclusive)
```

> [!Info] Kleene Operator
> For infinite quantification, we have the **kleene operator** (`*`), telling us that the previous regular expression is to be repeated 0 or more times.
>
> ```python
> "(ha)*" # Matches against the set {"", "ha", "haha", "hahaha", ... }
> ```
> 
> We can also use the `+` to force at least 1 or more repetition, and use `?` for only 0 or 1 repeats.

With these base constructs, we should be able to match any string we want with regular expressions! Let's now see how we can implement regular expressions.

## Implementing Regular Expressions
To implement regular expressions, we use what is known as a **finite state machine**. 

### Finite State Machines
Recall that all problems have a minimum language set that can be used to solve the problem. In some problems, this minimum language can be given as a finite set of **states**, as well as a finite set of **actions**, which can be used to transition between states.

For example, say we want to know the cardinal direction we're facing in given a set of 90 degree turns. Then, we may be able to define the following states and actions:

| Category | Description |
| :-: | - |
| States | The cardinal directions, $N, E, S, W$ |
| Actions | Left and right 90 degree turns, denoted $L$ and $R$, respectively |

Using these finite sets of states and actions, we can generate a graph to solve our problem, where states are nodes, and actions are edges connecting nodes.

```mermaid
graph LR
      N[North]
      E[East]
      S[South]
      W[West]
      
      N -. Left .-> W;
      N -. Right .-> E;

      E -. Right .-> S;
      E -. Left .-> N;
      
      S -. Left .-> E;
      S -. Right .-> W;

      W -. Left .-> S;
      W -. Right .-> N;
```

Thus, given a series of left and right turns, as well as a starting position, we can figure out our final cardinal direction! For example, if we started at North and turned $L, L, R$, we could traverse our graph to find that our final direction is West.

This graph is known as a **finite state machine**! These are machines with a finite set of states and actions, and can be modeled as a traversable graph, where nodes denote states, and edges denote actions.

We can generate a finite state machine to represent our regular expression, and this machine can be traversed through to determine if a string matches with the pattern or not!
> Despite the usefulness of finite state machines, they are limited in the number of problems they solve, as finite state machines only know their current state, as well as the next action to take. In other words, **finite state machines lack any concept of memory**.

## Mathematical Model for Regular Expressions
To understand how we can solve regular expressions using finite state machines, we first need to derive a mathematical model for regular expressions. We define each of the regular expression base constructs in mathematical terms below.

We define the **alphabet** as $\sum$, denoting the set of acceptable symbols, and define $L_1$ and $L_2$ as valid sequence of symbols (strings) from this alphabet. We'll additionally define $\sigma$ as the set of any single character from the alphabet, and $\epsilon$ as the set of any empty string.

We define **concatenation** as $L_1 L_2$ where
$$
L_1 L_2 = \{ xy : x \in L_1 \land y \in L_2 \}
$$
For example, if $L_1 = \{a\}, L_2 = \{b\}$, then $L_1 L_2 = \{ab\}$.

We define **union** as $L_1 \cup L_2$ where
$$
L_1 \cup L_2 = \{ x : x \in L_1 \lor x \in L_2 \}
$$
For example, if $L_1 = \{a\}, L_2 = \{b\}$, then $L_1 \cup L_2 = \{a, b\}$.

Finally, we define the **kleene operator** as
$$
L_1^* = \{ x : x \in \varnothing \lor x \in L_1 \lor x \in L_1 L_1 \lor \dots \}
$$
For example, if $L_1 = \{a\}$, then $L_1^* = \{\varnothing, a, aa, aaa, \dots \}$.
> While the number of states and actions in our machine must be finite, the **series of actions** we can take to move throughout the machine can be infinite!

Given these definitions, we can recursively generate any arbitrary set of strings, which can be used to describe a regular expression output.

Thus, given any regular expression $R$, we can recursively define it as follows:
$$
\begin{align*}
	R = \; &\epsilon \to \text{Set of Empty String}\\
	&\varnothing \to \text{Empty Set}\\ 
	&\sigma \to \text{Set of Any Single Character} \\
	&R_1 R_2 \to \text{Concatenation of any Set} \\
	&R_1 | R_2 \to \text{The Union of any Set} \\
	&R_1^* \to \text{The Kleene Operator}
\end{align*}
$$

## Regular Expressions as Finite State Machines
Using these definitions, we can now create a finite state machine for any given regular expression.

We can represent our regular expression in two different types of finite state machines: deterministic and non-deterministic.
- **Deterministic Finite State Machine (DFA)**: Finite state machines where for any given stage and action taken, there is only one possible path. 
- **Non-Deterministic Finite State Machine (NFA)**: Finite state machines where for any given stage and action taken, there may be multiple paths available to take.

> DFAs are easier to evaluate for a string match, but NFAs are easier to build! Thus, we will first build our regular expression into an NFA, and then convert this NFA into a DFA machine for evaluation.

Then, for any string $s$, we can use its characters as a "sequence of actions" to traverse through our machine, and check if we end on a "matched" state! 

### Non-Deterministic Finite State Machines (NFAs)
To **build a non-deterministic finite state machine**, we will use our mathematical definition of a regular expression. We define the following:
- Let `START` denote the starting position of our machine
- Let `ACCEPT` denote the state indicating the string input matches our regular expression.
- Let `Epsilon` ($\epsilon$) be an action representing an empty string - in other words, an action which can always be taken at no cost, regardless of our input string.

We want to build a machine between `START` and `ACCEPT`, which will send us to `ACCEPT` (from `START`) given any string matching our  regular expression. Using this machine, we can check if our string $s$ matches, by treating each of its characters as a list of "actions" to take (in order) from `START`, where each "action" tells us the edges we can move along.

```mermaid
graph LR
      start[START];
      accept[ACCEPT];

      subgraph Machine
            node[...]
      end

      start -. Epsilon .-> node;
      node -. Epsilon .-> accept;
```
> Note that if for any state, the next character in $s$ fails to match any action, our input is `INVALID` and will always fail to `ACCEPT`. 

Let's build our machine.

Starting with our **base case**, say we have any single character $\sigma$. We can build a machine matching this character as so:
```mermaid
graph LR
      start[START];
      accept[ACCEPT];

      subgraph Machine
            n1[State] -. Character .-> n2[State]
      end

      start -. Epsilon .-> n1;
      n2 -. Epsilon .-> accept;
```

Given this base case, we can combine our machines using the concatenate, union, and kleene operators.
1. To **concatenate** two machines together, we can use $\epsilon$ to link the end of one machine to the start of another.
   ```mermaid
   graph LR
      start[START];
      accept[ACCEPT];

      subgraph Machine 1
            n1[...]
      end
      subgraph Machine 2
            n2[...]
      end
      n1 -. Epsilon .-> n2;
      
      start -. Epsilon .-> n1;
      n2 -. Epsilon .-> accept;
   ```
2. To perform the **union** of two machines, we can use $\epsilon$ to go to either machine.
   ```mermaid
   graph LR
      start[START];
      accept[ACCEPT];

      subgraph Machine 1
            n1[...]
      end
      subgraph Machine 2
            n2[...]
      end
      
      start -. Epsilon .-> n1 & n2;
      n1 & n2 -. Epsilon .-> accept;
   ```
3. Finally, to perform the **kleene** operator on a machine, we can use $\epsilon$ to give us the option to traverse the machine again, or skip it altogether.
   ```mermaid
   graph LR
      start[START];
      accept[ACCEPT];

      subgraph Machine
            n1[...]
      end
      
      start -. Epsilon .-> n1;
      n1 -. Epsilon .-> accept;
      accept -. Epsilon .-> start;
      start -. Epsilon .-> accept;
   ```
> Note that while $\epsilon$ allows us to very conveniently define these operators, it by its very nature creates non-determinism!

Using these operators and the base case, we can build any regular expression into a NFA! Some examples are given below.
> Note that we can express an NFA with a list of nodes $Q$, a starting node $q \in Q$, and list of accept nodes $F$, and a set of edges (actions) $\bar{o}$!


> [!Example]- Example: Building a NFA
> Say we have regular expression `"/ab|cd/"`. How can we create a finite state machine for this?
>
> ```mermaid
> graph LR
>       subgraph ab
>                subgraph a
>                      a1[A Start] -. a .-> a2[A End];
>                end
>                subgraph b
>                      b1[B Start] -. b .-> b2[B End];
>                end
>                a2 -. Epsilon .-> b1;
>       end
>
>       subgraph cd
>                subgraph c
>                         c1[C Start] -. c .-> c2[C End];
>                end
>                subgraph d
>                         d1[D Start] -. d .-> d2[D End];
>                end
>                c2 -. Epsilon .-> d1;
>       end
>
>       s[START] -. Epsilon .-> a1 & c1;
>       d2 & b2 -. Epsilon .-> e[ACCEPT];
> ```

> [!Example]- Example: Building a NFA (2)
> Say we have regular expression `"/(a|b)*/"`. How can we create a finite state machine for this?
>
> ```mermaid
> graph LR
>       subgraph a
>                a1[A Start] -. a .-> a2[A End];
>       end
>       subgraph b
>                b1[B Start] -. b .-> b2[B End];
>       end
>
>       start[START];
>       accept[ACCEPT];
>
>       start -. Epsilon .-> a1 & b1;
>       a2 & b2 -. Epsilon .-> accept;
>       start -. Epsilon .-> accept -. Epsilon .-> start;
> ```


### Deterministic Finite State Machines (DFAs)
Now that we have a NFA for our regular expression, we want to be able to convert it to a DFA for evaluation, as evaluating NFAs can be slow (due to their non-deterministic nature).

To perform this conversion, we need to capture the "uncertainty" at any given state, and remove it, but how do we do this? Consider the following NFA:

```mermaid
graph LR
         A -. a .-> B & C;
```

Given action `a` at state $A$, we aren't sure whether to go to B or C! However, what if we went to a state representing both?

```mermaid
graph LR
      A -. a .-> n[B, C];
```

This removes the "uncertainty" from our NFA, as now, for action `a` at node $A$, we only have one possible node we can go to!

This is the key idea behind converting from a NFA to a DFA - we can remove "uncertainty" of multiple paths by combining all possible paths we can move through into one! To do this, we will use two operations:
- A `move(state, action)` operation, which will give us a list of all states we can reach from an initial state and action. Conceptually, this gives us a grouping of states (which we'll combine as a single node) that our path will point to.
- An `e_closure(state)` operation, which will give us a list of all states we can reach using purely epsilon transitions. Conceptually, this gives us a list of states that our state is "equivalent" to, as they can be epsilon transitioned to at no cost.

Note that combining uncertain paths will yield a new node which represents multiple states at once, which we'll have to account for.
> For example, if we take an action from a node representing multiple states, we will have to union the result of `move(state, action)` for all states the node represents!

Using these operations, we can convert our NFA to a DFA by doing the following. Let us start with an NFA with states $Q$, actions (edges $E$, and accept states $F$.

First, take our starting state $S_0$. Perform an epsilon closure (`e_closure`) on our starting state, and let this be our starting node $N_0$. Then, for every subsequent $N$ starting from our start:
1. For every action $A$ we can perform, call `move(S, A)` with every state $S$ the node represents, and union the results to obtain all states we can move to with this action, from $N$.

2. Epsilon close our result by calling `e_closure()`, to obtain all possible states we can move to (factoring in epsilon transitions) with our action.

3. Check if this group of states already exists somewhere as a node in the graph. If it does not, create a new node representing this group. Create an edge from our node $N$ to this new node, with the action being our previously mentioned action $A$.

4. For any newly created node, recursively call this function on these nodes to build the rest of the graph.

Finally, mark any node that contains an accept state as an accept node.

One deep dive example of this algorithm is given below.

> [!Example]- Example: NFA to DFA (Deep Dive)
> Convert the following NFA to a DFA.
> ```mermaid
> graph LR
>       0[START] -. a, b .-> 0;
>       1 -. Epsilon .-> 2;
>       0 -. a .-> 1 -. b .-> 2 -. b .-> 3[ACCEPT];
>       2-. Epsilon .-> 1;
> ```
>
> We start with `START`. Because `START` has no epsilon transitions, our starting node will only represent `START`.
>
> ```mermaid
> graph LR
>       0[START];
> ```
> 
> Now, we go through each possible action from `START` and find what states these actions can go to.
> - Taking action `a`, we can move to states `START` and `1`, giving us a group [`START`, `1`].
> - Taking action `b`, we can move to states `START`, giving us group [`START`].
>
> We now apply epsilon closure on these groups to include any states we can traverse to (with no cost) using epsilon transitions. This will transform [`START`, `1`] into [`START`, `1`, `2`]. Because there is no node for [`START`, `1`, `2`], we create one and make a recursive call on it.
> 
> ```mermaid
> graph LR
>       0[START];
>       0 -. a .-> 1[START, 1, 2];
>       0 -. b .-> 0;
> ```
>
> We now go through every possible action for node [`START`, `1`, `2`] and find what states we can go to with these actions.
> - Taking action `a`, we see that `START` can go to `START`, and `1` and `2` cannot go anywhere, giving us group [`START`].
> - Taking action `b`, we see that `START` can go to `START`, and `1` can go to `2`, giving us group [`2`].
>
> Applying epsilon closure on these groups, we obtain [`START`], and [`1`, `2`] as there is an epsilon transition from nodes `2` to `1`. Because there is no node for [`1`,`2`], we create one and make a recursive call on it.
>
> ```mermaid
> graph LR
>       0[START];
>       0 -. a .-> 1[START, 1, 2];
>       0 -. b .-> 0;
>
>       1 -. a .-> 0;
>       1 -. b .-> 2[1,2];
> ```
>
> We repeat the same process for [`1`, `2`].
> 1. For action `a`, we get no group.
> 2. For action `b`, we get [`2`, `ACCEPT`].
>
> Applying epsilon closure on these groups, we obtain [`1`, `2`, `ACCEPT`]. Because we create a node for [`1`, `2`, `ACCEPT`], we repeat the algorithm with this node.
>
> ```mermaid
> graph LR
>       0[START];
>       0 -. a .-> 1[START, 1, 2];
>       0 -. b .-> 0;
>
>       1 -. a .-> 0;
>       1 -. b .-> 2[1,2];
>
>       2 -. b .-> 3[1, 2, ACCEPT];
> ```
>
> We repeat the same process for [`1`, `2`, `ACCEPT`].
> - For action `a`, we get no group.
> - For action `b`, we get [`2`, `ACCEPT`]. Applying epsilon closure, we obtain [`1`, `2`, `ACCEPT`].
>
> ```mermaid
> graph LR
>       0[START];
>       0 -. a .-> 1[START, 1, 2];
>       0 -. b .-> 0;
>
>       1 -. a .-> 0;
>       1 -. b .-> 2[1,2];
>
>       2 -. b .-> 3[1, 2, ACCEPT] -. b .-> 3;
> ```
>
> Finally, we mark our starting state, accept states, and rename the rest!
>
> ```mermaid
> graph LR
>       0[START];
>       0 -. a .-> 1;
>       0 -. b .-> 0;
>
>       1 -. a .-> 0;
>       1 -. b .-> 2;
>
>       2 -. b .-> 3[ACCEPT] -. b .-> 3;
> ```
>
> We are done! Note that both of the graphs return the same results. Using this DFA, we can now use any regular expression to traverse a graph, and see if it matches!
