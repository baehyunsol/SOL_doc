# Operators

SOL has quite lots of operators and **all of them can be overloaded**. I'll explain the default behaviors of the operators here.

### `+`: add/append operator
```python
3 + 4       # 7 #
[1, 2, 3] + 4   # [1, 2, 3, 4] #
[1, 2, 3] + [4, 5, 6]  # [1, 2, 3, [4, 5, 6]]
```

### `*`, `-`, `%`, `*`, `and`, `or`, `not`, `==`, `>`, `<`, `!=`, `>=`, `<=`

Nothing special about above.

We dont't use `!`, `&&` and `||` in SOL.


### `//`: floordiv operator

It's equivalent to `//` operator in Python (a // b returns int(a / b)).

### `/`: div operator

`int / int` returns a `frac`, not an `int`.

### `++`: concatenation operator
```python
[1, 2, 3] ++ [3, 4, 5]  # [1, 2, 3, 3, 4, 5] #
"hello" ++ " world!"    # "hello world!" #
```

### `in` operator

It checks if an iterator contains an element.
```python
2 in [1, 2, 3]   # 1 #
10 in [1, 2, 3]  # 0 #
```


### `|`: update operator

Among basic types, only `list` has its implementation.

Based on the second operand, `|` does 3 operations on a `list`.

#### Update a single element
```python
# list | [index, value]  ->  list[index] = value #
# index should be an integer. #
# The second operand of | should be a list with two elements. #

[1, 2, 3, 4, 5] | [1, 10]  # [1, 10, 3, 4, 5] #
```

#### Update multiple elements
```python
# list | [[index1, value1], [index2, value2], [index3, value3]]#
# The second operand of | should be a list with pairs of indexes and values. #

[1, 2, 3, 4, 5, 6, 7] | [[0, -1], [2, -3], [4, -5]]  # [-1, 2, -3, 4, -5] #
```

#### Update a multidimensional list
```python
# list | [index1, index2, index3, value] -> list[index1][index2][index3] = value #
# The second operand of | should be a list(not nested) with multiple index integers and a value. #

[1, 2, [3, 4, [5, 6]] | [2, 2, 1, 100]  # [1, 2, [3, 4, [5, 100]]] #
```

`a | [b, c, d, e]` is just a syntactic sugar for
```python
a | [
    b,
    a[b] | [
        c,
        a[b][c] | [
            d,
            e
        ]
    ]
]
```
