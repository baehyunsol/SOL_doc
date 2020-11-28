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

**It's not the list in C++. It's a Python list. In other languages it's called vector.**

Use square brackets to create or index a list.
```python
[1, 2, 3]                   # list #
[1, 2, 3, 3.14, [1, 2, 3]]  # It's dynamically typed. #
[1, 2, 3][1]                # index #
[1, 2, 3, 4][-1]            # negative index #
```

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


### Struct (Work in progress)
```python
struct player {
    x, y, x_speed = 3, y_speed = 3,
    hp, xp, mp, name
}

# let's say p1 is an instance of player #
p1.x   # accessing a member variable #

p1 | [.x, p1.x + p1.x_speed]  # updating a member variable (if not overloaded) #
```
Simply it's a typed named tuple.


[Back to SOL_doc](README.md)
