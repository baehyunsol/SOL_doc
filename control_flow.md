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


### Pipelines

Pipelines are used for complex control flows.

You can declare local variables inside a pipeline. All the variables are immutable lazily evaluated.

```python
|:
    $a = f();
    $b = g();
    $a + $b
:|
```

Above code is basically `f() + g()`, but with local variables. Every variable declaration has to end with a semi colon. The last expression, which is the value of the entire pipeline, doesn't have a trailing semi colon.


### Syntactic sugar for loops

When you're to translate a C-style for-loop into SOL, you have to use recursive functions. I'll go with an example. See below.

```c
// C version
for (int i = 0; i < length; i++) {
    
    if (f(array[i])) {
        result[i] = g(i)
    }
    
    else {
        result[i] = h(i)
    }

}
```

```python

# SOL version #
fn iter(index, length, array, result) {

    @ index == length {
        result
    }

    @ f(array[i]) => (
        iter(
            index = index + 1,
            length = length,
            array = array,
            result = result | [i, g(i)]
        )
    )
    
    @ => (
        iter(
            index = index + 1,
            length = length,
            array = array,
            result = result | [i, h(i)]
        )
    )
}

```

In the SOL version, `index = index + 1`, `length = length`, and `array = array` look quite needless. Those can be shortened with `^` and `+=`.

```python

# SOL shortened version1 #
fn iter(index, length, array, result) {

    @ index == length {
        result
    }

    @ f(array[i]) => (
        iter(
            index += 1,
            length^,
            array^,
            result |= [i, g(i)]
        )
    )
    
    @ => (
        iter(
            index += 1,
            length^,
            array^,
            result |= [i, h(i)]
        )
    )
}

```

`a += b` is short for `a = a + b`, so is `|=`, and `x^` is for `x = x`. These syntactic sugars can be used when whatever function is called.

BTW, above still looks verbose. Let's shorten it even further.

```python

# SOL shortened version2 #
fn iter(index += 1, length^, array^, result) {

    @ index == length {
        result
    }

    @ f(array[i]) => (
        iter(
            result |= [i, g(i)]
        )
    )
    
    @ => (
        iter(
            result |= [i, h(i)]
        )
    )
}

```

You can use `^` and `+=` as default values.

So, is that idiomatic SOL code? I guess not... How about this one?

```python
def iter(index += 1, length^, array^, result) {|:
    $new_result = @ f(array[i]) => (
        result | [i, g(i)]
    )
    @ => (
        result | [i, h(i)]
    );
    
    @ index == length => (result)
    
    @ => (
        iter($new_result)
    )
:|}
```

It's better, but not fully functional yet.

```
[
    do: @ f(array[i]) => (g(i)) @ => (h(i));
    for: i, [..len(array)];
]
```

Above is the final translation of the C-style for-loop into an idiomatic SOL code.

[Back to SOL_doc](README.md)
