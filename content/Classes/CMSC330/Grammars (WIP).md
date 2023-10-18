---
title: Context Free Grammars
---

## Intuition
Here, we discuss how to build context free grammars, which can be used to build a parser! This is the first step in building our compiler.

Recall that for a language, we need **syntax** and **semantics**. We discuss grammar, which is a subset of syntax. Given some sentence, how do we know that it is gramatically correct?

> [!Example]+ Example: The Need for Grammer
> Consider the sentence *"the blue truck"*. How do we know if this is a valid sentence?
>
> We know this is a valid sentence because:
> 1) All symbols being used are valid English letters
> 2) The combinations of symbols (words) used are valid
> 3) The order of the words, i.e. the structure of the sentence is valid

Note that in the above example, we can determine (1) and (2) using regular expressions, but regular expressions cannot tell us if the structure of our sentence is valid - they are simply not powerful enough. How can we determine this?

Here, we'll just focus on the simplest, next powerful machine for grammars, though there are far more powerful ones out there.

Let's define what a **grammar** is. Remember how we recursively defined a regular expression sequence, which creates a set of strings encapsulating every possible word in a language.
> CFGs have MEMORYYY, meaning they remember what they previously saw

We define the set of all valid sentences $S$. For any value $a$ in the set, 

**Nonterminal**: Symbol that stands (or is a placeholder) of other symbols. A symbol that represents something else (think of a regular expression $R$ representing a set of other strings!)

**Terminals**: Base symbols, symbols found in alphabet ("a", "b", "")

**Production Rules**: Rules that declare what terminals / order of terminals that non-terminals can stand for.
> We build non-terminals from terminals.

Consider the regular expresion definition.
$$
\begin{align*}
R \to &\epsilon \\
      &\sigma \in \sum \\
      &RR \\
      &R \vert R \\
      &|R*
\end{align*}
$$

In this example, our non-terminals are $R$, our terminals are $\epsilon, \sigma, *, \vert$, and our production rules are specified by the arrow operator, i.e. $R \to ...$.
> We're abstracting what regular expressions mean into a even more powerful layer.

These production rules specify restrictions that must hold true in order for a expression to be valid. For example, we know the regular expression $a*$ is valid as it satisfies $R*$, but $|ab$ is not as it does not satisfy $R|R$.

**derivation**: A way to prove / derive a string is valid, given a context-free grammar

How does derivation work? Well, say we start from a non-terminal $R$. We can then use the definition to derive
$$
R \to R* \to a*
$$
to show $a*$ is valid. We are using the recursively defined rules themselves to build specific terminal sequences that can match and show what we have is valid!

When deriving, we typically will "derive" (translate non-terminal into terminals) from order of leftmost to rightmost non-terminals, known as "leftmost derivation".
$$
R \to \underline{R} \vert R \to \underline{R}* \vert R \to a* \vert R \to a* \vert b
$$
> We call **expanding** when we use our non-terminal to get another larger non-terminal sequence, and **defining** when we use our non-terminal to get a terminal.

Note that we cannot use the derivation to **GET ANYTHING INVALID** - thus, as long as we can match our sentence with the derivation, we know we have a valid derivation!!

Say we have the grammar
$$
E \to E + E \vert n, n \in \mathbb{Z}
$$
We can use this to show that expressions like $1 + 2 + 3$ are valid.
$$
E \to \underline{E} + E \to 1 + \underline{E} \to 1 + \underline{E} + E \to 1 + 2 + \underline{E} \to 1 + 2 + 3
$$
However, there's ambiguity in the leftmost derivation - i.e. there are multiple ways we can get the same result! Thus is not optimal.
$$
E \to E + E \to (E + E) + E \to 1 + E + E \to 1 + 2 + E \to 1 + 2 + 3
$$
$$
E \to E + E \to 1 + E \to 1 + E + E \to 1 + 2 + E \to 1 + 2 + 3
$$

We can define ambiguity in a CFG context if two leftmost derivations exist for any particular string. This may be bad in situations where order of operations does indeed matter. For example, $2 * 3 + 4$ with grammar $E \to E + E \vert E * E \vert n$, which can be derived as
$$
E \to E*E \to 2*E \to 2*(E+E) \to 2*3+E \to 2*3+4
$$
$$
E \to E+E \to E*E + E \to 2*E + E \to 2*3 + E \to 2*3+4
$$
> This derivation gives us a parser tree, but the ambiguity may make us evaluate our order of operations in the wrong way. There is thus a concept of production rules having precedence over one another.

*for convention, we will denote all non-terminals as capital letters*
> other grammars include context-sensitive grammars, and recursively enumerated grammars.

> [!Example] Example: Context Free Grammar (with Precedence)
> Consider the following context free grammar:
> $$
> \begin{align*}
>    &E \to M + E \vert M \\
>    &M \to N * M \vert N \\
>    &N \to 1 \vert 2 \vert 3
> \end{align*}
> $$
> Note that by the way we define this grammar, we naturally have an order of operations. We do this by ensuring our non-terminal cannot define itself more than once, removing any ambiguity.
>
> We have non-terminals $E, M, N$, and terminals $+, 1, 2, 3$. Now say we want to use this grammar to derive $1 * 2 + 3$. We can do it as so:
>
> $$
> \begin{align*}
>       E &\to M + E \to N * M + E \to 1 * M + E \\
>         &\to 1 * N + E \to 1 * 2 + E \to 1 * 2 + M \\
>         &\to 1 * 2 + N \to 1 * 2 + 3
> \end{align*}
> $$

This makes CFGs really powerful!

consider the regex `a*b+c?`. We can build a CFG to match for it as follows:
$$
\begin{align*}
        &R \to ABC \\
        &A \to aA \vert \epsilon \\
        &B \to bB \vert b \\
        &C \to c \vert \epsilon
\end{align*}
$$


# Pushdown Automata
Context free grammars also have an alaogous machie, known as a PDA


^ Context Free Grammars o.o

*Later, there is also recursively enumerable grammar, which can be implemented with a turing machine.*


To make meaning from a written language, we must do the following:

1. **Lexing (Tokenizing)**: The proces of taking a string ocharacters, and making sure the string contains valid words.
  > We can do that with regular expressions.

2. **Parsing**: The process of ensuring that the structure of the words are valid - in other words, ensuring that words are in the correct order.
> We can do this with CFGs

3. **Evaluator**: We need to evaluate the semantics of words, in other words, derive meaning from it. We can do this either using an interpreter or compiler.

For our purposes, we will:
- With lexing, we will take a string and return a token list.
- With parsing, we wil take a token list and return a parsing tree, otherwise known as an **abstract syntax tree**.
- With evaluation, we will evaluate the syntax tree and either translate it into a value, or code (such as assembly).

Let's start with lexing. How do we build a lexer in Python?

Suppose we want to lex a mathetmatical expression, given with definition

$$
\begin{align*}
        &E \to M + E | M - E | M \\
        &M \to N * M | N / M | N \\
        &N \to n | (E)
\end{align*}
$$

Let's start by determining our terminals. As we're pasing a mathematical expression, we know that any number $n$ is valid, and any operator $+, -, *, /, ()$ is valid.

```python
import re

# first, check that all of our words are valid.
# we easily do this by building a regular expression
# which can that a word is valid in our language match.
def lex(in_string):

    valid_words = re.compile(r"^([+-/*()]|-?[0-9]+)")

    token_list = []
    pos = 0
    
    while pos < len(in_string):
          match = re.match(valid_words, in_string[pos:])

          if match:
             token_list.append(match.group(1))
             pos += len(match.group(1))
          else:
             raise Exception("Invalid Character Detected")
            
    return token_list
```

Now that we have a list of tokens, we need to parse it to ensure that the structure of the tokens is correct. A common way to do this is by using an **abstract syntax tree**.

There are a variety of different parsers that exist.
- Left leaning and right leaning parsers
- Look ahead parsers
- Backtracking parsers
- Recursive Descent
- Bottom-Up Parsers

In this course, we will only talk about the left leaning parser, look ahead by 1 (LL1) parser (via recursive descent). Howeer, LL1 parsers have some restrictions:
1. Cannot parse ambiguous grammars. However, ambiguous grammars can be converted to non-ambiguous grammars, if you are restrained to LL1 parsers.

```python
# takes a token list, and returns an abstract
# syntax tree!
def parser(token_list):
    # some important edge cases
    # 1) 1 + 2 - (we check for remainders after getting a valid sequence)
    # 2) 1 - 2 * 4 (order of operations is followed)
    # Note that our non-terminals E,M,N all represent a specific sub-expression in our token list.


def parse_E(token_list):
    # The grammar allows M + E, M - E, M
    mparse = parse_M(token_list) # after parsing m, our token list should have nothing, or a (+ E) or a (- E).

    # process the remaining tokens after M is parsed, which should be [], [+, ...], or [-, ...]
    
    
def parse_M(token_list):

def parse_N(token_list):
```