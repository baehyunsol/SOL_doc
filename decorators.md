# Decorators(Work in Progress)

With decorators, functions can have special properties.

Decorators come before the `def` keyword.

Each decorator is embraced with double greater/less signs.

A function can have multiple decorators if needed. See the explanations below for more details.


## Cache
The decorated function is cached.
```python
<<cache>>
def fibo(n) {

    @ n < 2 => (
        1
    )

    @ => (
        fibo(n - 1) + fibo(n - 2)
    )
}
```

## Function overloading

Functions can be overloaded based on args' types.

Type checks are done at run time. The number of arguments is at most 2.

Let's say you want `len()` function to work on your own `stack` type.
```python
<<for x: stack>>
def len(x) {
    # function body goes here #
}
```

To define a default behavior of a function, use `any` type.
```python
<<for x: stack>>
def len(x) {
    # len() function for your stack type #
}

<<for x: any>>
def len(x) {
    # default len() function #
}
```

The numbers of the arguments must match across all the definitions.
```python
<<for x: stack>>
def len(x) {
    # function body goes here #
}

<<for x: list, y: any>>
def len(x, y) {
    # You can't do this #
}
```

## Operator overloading

Let's say you implemented a stack.

First, you need a concat operator for two stacks.
```python
<<++ for x: stack, y: stack>>
def stack_concat(x, y) {
    # function body goes here #
}
```

With the above decorator, `stack_concat` function is called everytime `++` is used with matching types.
You can still use the `stack_concat` function like a normal function.

Next, you need an append operator that works with any type.
```python
<<+ for x: stack, y: any>>
def stack_append(x, y) {
    # function body goes here #
}
```
`any` is a special type name that matches any type.

When you try to append an integer to a stack, SOL first looks for `<<+ for x: stack, y: int>>`.

If it can't find one, then it searches for `<<+ for x: stack, y: any>>`, which is defined above.

If the above is not defined, it would try to find `<<+ for x: any, y: int>>`. Finally it would try `<<+ for x: any, y: any>>` or return an error.

If you want your stack to work only on integers and strings, use `or`.

```python
<<+ for x: stack, y: int or string>>
def stack_append(x, y) {
    # function body goes here #
}


# It's also valid #
<<+ for x: stack, y: int>>
<<+ for x: stack, y: string>>
def stack_append(x, y) {
    # function body goes here #
}
```

#### List of overloadable operators
- `+`: add
- `-`: sub
- `*`: multiply
- `/`: divide
- `//`: floor division
- `%`: mod
- `++`: concat
- `|`: update
- `<`: less than
- `>`: greater than
- `<=`: less or equal
- `>=`: greater or equal
- `==`: equal
- `!=`: not equal
- `not`: not
- `[]`: index, index(a, b) for a[b]


[Back to SOL_doc](README.md)
