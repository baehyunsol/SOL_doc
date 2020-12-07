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
Chains of `@` means `if elif elif ... `. `@ => ()` is a syntactic sugar for `@ True => ()`which is used as `else` branch.

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
Do you see that `do_something()` is called twice with same arguments? It's totally unnecessary since it's a pure function.

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


### Pipelines

If you want more complicated chains of `call_it` operators, use pipelines.

```
def return_15() {

    |:
        $a = 1;
        $b = 2;
        $c = $a + 3;
        $d = $b + $c;
        $a + $b + $c + $d
    :| + 2
}
```

Pipeline begins with `|:` and ends with `:|`.

Pipeline is a syntactic sugar for `call_it` operators. It automatically assign local variables and reshape the inner expression.

Each declaration must be seperated by semi colon. The expression comes at the last and it's the value of the entire pipeline.

The entire pipeline is a single expression. Local variables declared inside a pipeline cannot be accessed outside.



[Back to SOL_doc](README.md)
