# Examples

Learn how to code in SOL with valid SOL codes.

Since Github doesn't support SOL syntax highlighting, I used Python syntax instead.

### Simple Math Functions
```python

def factorial(n) {  # braces are optional, but I recommend you using it unless function's body is a single line.#

    @ n == 1 => (1)

    @ => (n * factorial(n - 1))

}


<<cache>>  # It runs in O(n)! #
def fibonacci(n) {

    @ n < 1 => (1)
    
    @ => (fibonacci(n - 1) + fibonacci(n - 2))

}


def fibonacci2(n, a=1, b=1) {

    @ n == 0 => (a)

    @ => (
        fibonacci2(
            n -= 1,
            a += b,
            b = a
        )
    )

}


def gcd(a, b) {

    @ a < b => (gcd(b = a, a = b))
    
    @ b == 0 => (a)
    
    @ => (
        gcd(a = b, b = a % b)
    )
}
```


### Sorting Algorithms
```python

# It's much slower than O(n log n) due to concatonations.#
def quicksort(arr) {

    @ len(arr) == 0 => (arr)

    @ => (
        quicksort([
            for: x, arr;
            if: x < arr[0]
        ]) ++ [
            for: x , arr;
            if: x == arr[0]
        ] ++ quicksort([
            for: x , arr;
            if: x > arr[0];
        ])
    )

}

```


### Standard Library implemented in pure SOL code
```python
def map(func, iter) {

    worker_map(
        func^, iter^, result = [],  # Use a stack for result to make it O(n) #
        index = 0, length = len(iter)
    )

}


def worker_map(func^, iter^, result, index += 1, length^) {

    @ index == length => (result)

    @ => (
        worker_map(
            result += func(iter[index])
        )
    )

}


def filter(func, iter) {

    worker_filter(
        func^, iter^, result = [],  # Use stack for result to make it O(n) #
        index = 0, length = len(iter)
    )

}


def worker_filter(func^, iter^, result, index += 1, length^) {

    @ index == length => (result)
    
    @ func(iter[index]) => (
        worker_filter(
            result += iter[index]
        )
    )
    
    @ => (
        worker_filter(result^)
    )

}
```
