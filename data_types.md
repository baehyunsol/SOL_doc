# Data Types

### Basic types
```python
# integer #
1
100_000_000    # Use underscores for readability #


# fraction #
3.14                     # Compiler translates it to 157 / 50 #
1 / 3 + 1 / 3 + 1 / 3    # Unlike float values, it gives exact 1. #
# Fraction arithmetics are EXTREMLY slow! #
# If you're to build a game... try C++. #


# string #
"hello, world!"
'hello, world!'            # Single quotes and double quotes don't have any semantic difference. #
"hello, " ++ "world!"      # Use concat operator, not add operator. #


None         # built_in type #
True         # integer 1 #
False        # integer 0 #
```


### List

**It's not the list in C++. It's a Python list. In other languages it's called vector/array.**

Use square brackets to create or index a list.
```python
# list #
[1, 2, 3]

# It's dynamically typed. #
[1, 2, 3, 3.14, [1, 2, 3]]

# Indexing #
[1, 2, 3][1]              # 2 #
[1, 2, 3][2]              # 3 #
[1, 2, 3, 4][-1]          # 4 #
[1, 2, 3, 4][-2]          # 3 #
[1, 2, 3][3]              # Returns an error instead of crashing #
```
It's the only type that is implemented directly inside SOL Runtime, which means it's the fastest.
It takes O(1) to index.
It **always** takes O(n) to update / concat / append.
Since it's immutable, it has to create an entire list each time those operations are applied.
Use stack instead when it's updated frequently.

SOL has fancy built_in syntaxes for lists.
```python
# range #
[0..100..2]             # SOL #
list(range(0, 100, 2))  # Python counterpart #

[..100..2]              # default value of start index is 0 #
[0..100]                # default value of step is -1 #
[..100]
[..]                    # Unlike Haskell, SOL can't init an infinite list #



# slice #
a[3:10:2]               # SOL and Python has indentical syntax for slicing a list #
# In case you don't know, it's [start:end:step] #
a[::-1]                # reverse a list #

# Creating and indexing a slice object for a list takes O(1) time. #
# Doing other operations takes O(n) time because it has to create a new object. #



# list comprehension #
[
    do: x * x;
    for: x, [..20];
    if: x % 2 == 0;
]
# quite intuitive, isn't it? #
# You can omit do or if but not both #

[
    do: x * y;
    for: x, [..3];
    for: y, [..4];
]
# 2-dimensional list comprehension #
```


### Dictionary

Use braces to define a new dictionary. In other languages, it's called hash table, or a map.
(Add more explanations later...)


### Struct (Work in progress)
```python
struct player {
    x, y, x_speed = 3, y_speed = 3,
    hp, xp, mp, name
}

# let's say p1 is an instance of player #
p1.x   # accessing a member variable #

p1 | [.x, p1.x + p1.x_speed]  # updating a member variable (if the update operator is not overloaded) #
```
Simply it's a typed named tuple.


[Back to SOL_doc](README.md)
