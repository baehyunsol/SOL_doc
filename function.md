# Function

### Definition
To define a new function, use `def` keyword.

Every function is made of exactly one expression.
```python

def add(x, y) {x + y}
def add2(x) x + 2  # Curly braces are optional #

def PI 3.14     # Define a constant by not giving an argument list. #
def pi() 3.14   # Functions and constants are different. I'll talk about that later. #

def sub(x, y=0) x - y  # Default arguments #
```

Functions and constants are different.
In the example above, if you want the pi value, you should either call `pi()` or use `PI`.

If you call `PI()`, that would be calling `3.14()`, which would raise a runtime error.

Calling a `frac` instance is not defined in SOL, and overloading `__call__` is not supported in SOL.

If you try `pi + 3`, that would be adding a function and an integer, which is not defined.

That doesn't raise any error though, because `+` can be overloaded.


### First class function
You can return a function, or pass it as an argument.

```python
def add1(x) x + 1
def add2(x) x + 2

def apply(f, x) f(x)

def main() print(apply(f = add1, x = 3))  # 4 #
```

SOL supports lambda functions that captures its environment.

It uses Python-like syntax. See below.
```python
map(
    func = lmd x: x + 3,
    iter = [3..10]
)
```


### Function call
When calling a function, every argument has to be named unless obvious.
```python
def foo(x, y = 4) ...

foo(3)          # legal #
foo(x = 3)      # legal #
foo(x = 3, 4)   # legal #
foo(3, y = 4)   # legal #
foo(3, 4)       # illegal #
```


There are some syntactic sugars that helps implementing loops using recursions.
`foo(x^)` -> `foo(x = x)`

`foo(x -= 3)` -> `foo(x = x - 3)`

You'll see better examples in control_flow.md.
