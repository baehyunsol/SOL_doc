# Operators

SOL has quite lots of operators and **all of them can be overloaded**. I'll explain the default behaviors of the operators here.

### `+`: add/push operator
```python
3 + 4       # 7 #
[1, 2, 3] + 4   # [1, 2, 3, 4] #
[1, 2, 3] + [4, 5, 6]  # [1, 2, 3, [4, 5, 6]]
```

### `*`, `-`, `%`, `*`, `and`, `or`, `not`, `==`, `>`, `<`, `!=`, `>=`, `<=`

Nothing special about above.

We dont't use `&&` and `||` in SOL.


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


### list update operators

`_u` updates a single value in a list.
```python
list _u [index, value]  # list[index] = value #

[1, 2, 3] _u [2, 10]  # [1, 2, 10] #

# use . to update a member variable #
player _u [.x, player.x + player.x_speed]
```

`_um` updates Multiple values in a list.
```python
list _um [[index1, value1], [index2, value2], ...]

[1, 2, 3, 4, 5, 6] _um [[0, 10], [2, 20]]  # [10, 2, 20, 4, 5, 6] #

player _um [
    [.x, player.x + player.x_speed],
    [.y, player.y + player.y_speed]
]
```

`_ud` updates a multi Dimensional list.

```python
a _ud [b, c, d, e]  # a[b][c][d] = e #
```

It's just a syntactic sugar for
```python
a _u [
    b,
    a[b] _u [
        c,
        a[b][c] _u [d, e]
    ]
]
```
