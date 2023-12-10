---
title: Regular Expressions
tags:
- up-to-date
- deprecated
---


# Implementing Regular Expressions
## Python `re` Module
To perform regular expressions in Python, we first need to import Python's built-in regular expression module, `re`.
> We can use the [PYTHEX](https://pythex.org/) website to test Python regular expression matching!


```python
import re # Lets us perform regular expression matching
```

Then, we can compile a **regular expression** object using `compile()`! This object can then be used to match strings for a particular pattern.

```python
# can be used to match 3 digits XXX
regex_object = re.compile(r"[0-9]{3}")
```
> Note the use of the `r` before the string. In Python, this stands for **raw string**, meaning escape sequences `\` won't be translated!

Below we provide some of the commonly used functions in `re`. Assume we've already compiled a regular expression object `regex` for use.

> [!Info] Match Objects
> If we obtain a `Match` object from a `re` function, there is a variety of information we can pull from it.
>
> ```python
> # assume match is a Match object 
> span = match.span() # tuple containing start and end position of the match
> string = match.string # string passed in ("hello world")
> group = match.group() # part of the string where the match was found
> ```
>
> Additionally, we can even use `Match` objects for **string parsing**! In some languages like Python, the precedence operator `( )` is also an operator for **grouping** values that can be pulled out of our regular expression!
>
> ```python
> # matches phone number XXXXXXXXXX
> # we group by the first 3 digits, then the next 3 digits, finally the last 4 digits
> regex = re.compile(r"([0-9]{3})([0-9]{3})([0-9]{4})")
> m = regex.match("1234567890")
>
> print(m.group(0)) # "123456890" - 0 returns the entire match
> print(m.group(1)) # "123"
> print(m.group(2)) # "456"
> print(m.group(3)) # "7890"
> ```
> > Group IDs are assigned in the order of their open parentheses, as we read the string left to right! Note that we can nest groups together, though we cannot overlap groups.

### `regex.findall(pattern,string)`
Finds all matches of a regular expression in a string, or an empty list if no matches are found.

```python
regex = re.compile(r"cmsc3[0-9]{2}")
regex.findall("cmsc330 cmsc250 cmsc351") # ['cmsc330', 'cmsc351']
regex.findall("cmsc110 cmsc131 cmsc216") # []
```

### `regex.fullmatch(string)`
Returns a `Match` object if the entire string matches the regular expression, or `None` of this does not occur.

```python
regex = re.compile(r"ab*")
regex.fullmatch("abbbbbb") # Returns Match object
regex.fullmatch("abbbbc") # None
```

### `regex.match(string)`
Returns a `Match` object if any substring starting from the beginning of `string` matches the regular expression, or `None` of this does not occur.

```python
regex = re.compile(r"ab*")
regex.fullmatch("abbbcc") # Returns Match object
regex.fullmatch("cabbb") # None
```