# Control Flow


### If
If expression is the most basic control flow for all functions. Note that it's an expression, not a statement.
```python
if cond1:
    expr1

elif cond2:
    expr2

else:
    expr3
```
is equivalent to
```python
@ cond1 => (
    expr1
)
@ cond2 => (
    expr2
)
@ => (
    expr3
)
```
Chains of `@` means `if elif elif ... `. `@ => ` is a syntactic sugar for `@ True => `which is used as `else` branch.

The entire chain is an expression that returns a value depending on the conditions.

Omit else branch only when it covers the whole cases or it will cause a runtime error.



### Switch (Working in progress)
```python
switch x => (
    value1 => expr1,
    value2 => expr2,
    value3 => expr3,
    _ => expr4,      # default case #
)
```


### Local variables
You can declare immutable local variables for efficiency.

See the example below
```python
def iteration(iter^, index, result^) {

    @ index == len(iter) => (result)

    @ is_valid(iter[index]) => (
        iteration(
            index = get_next_index(
                do_something(iter[index])
            ),
            result += do_something(iter[index])
        )
    )

    @ => (
        iteration(index += 1)
    )
}

# you might wonder what '^' and '+=' do. Read function.md file. #
```
Do you see that `do_something()` is called twice with same arguments? It's totally unnecessary in functional languages.

There are two ways to avoid such redundancy.

First is to use `call_it` operator.
```python
def iteration(iter^, index, result^) {

    @ index == len(iter) => (result)

    @ is_valid(iter[index]) => (
        iteration(
            index = get_next_index(
                do_something(iter[index]) call_it $value1
            ),
            result += $value1
        )
    )

    @ => (
        iteration(index += 1)
    )
}
```
`call_it` operator assigns a value to another name. The name must begin with a letter '$'.


Second is to declare a local variable.
```python
def iteration(iter^, index, result^) {

    $value1 = do_something(iter[index]);

    @ index == len(iter) => (result)

    @ is_valid(iter[index]) => (
        iteration(
            index = get_next_index(
                $value1
            ),
            result += $value1
        )
    )

    @ => (
        iteration(index += 1)
    )
}
```

All the local variables are lazily evaluated.

Names of the locals should begin with a letter '$'.

When using local vars, the function body must be wrapped with curly braces.


### Pipeline (Working in progress)
```python
def count_even_length_nums(nums):

    strings = map(str, nums)
    lengths = map(len, strings)
    evens = filter(lambda x: x % 2 == 0, lengths)
    return len(list(evens))
```

Above is a Python code that counts how many numbers in the list are even numbers of digits long.

If you want to do the samething is SOL, that would be like below.
```python
def count_even_length_nums(nums)

    len(
        filter(
            func = lmd x: x % 2 == 0,
            iter = map(
                func = len,
                iter = map(
                    func = str,
                    iter = nums
                )
            )
        )
    )
```
That's verbose... isn't it?

How about this one?
```python
def count_even_length_nums(nums)

    |:
        map(func = str, iter = nums)
        -> map(func = len, iter = $)
        -> filter(func = lmd x: x % 2 == 0, iter = $)
        -> len($)
    :|
```
Looks much better.

If you want shorter one and readability doesn't matter, use list comprehensions.
```python
def count_even_length_nums(nums)
    len([le | [len; s | [str(n); n | nums]]; le % 2 == 0])
```


[Back to SOL_doc](README.md)
