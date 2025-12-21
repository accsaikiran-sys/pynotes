---
title: Ch05 05 Recursion
date: 2025-12-20
author: Your Name
cell_count: 12
score: 10
---

```python
# Created: 20251210
# https://csp.gitbook.io/python-learning/basics/ch05-python-functions/python-recursion
```


```python
def print_numbers(n):
    if n == 0:
        return
    print(n)
    print_numbers(n - 1)

print_numbers(5)
```

    5
    4
    3
    2
    1



```python
def factorial(n):
    if n==0:
        return 1
    return n * factorial (n-1)
print(factorial(5))
```

    120



```python
def sum_n(n):
    if n == 1:
        return 1
    return n + sum_n(n - 1)

print(sum_n(5))  # Output: 15
```

    15



```python
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

print(fibonacci(6))  # Output: 8
```

    8



```python
def factorial_iterative(n):
    result = 1
    for i in range(1, n + 1):
        result *= i
    return result

print(factorial_iterative(5))  # 120
```

    120



```python
def print_list(lst):
    if not lst:
        return
    print(lst[0])
    print_list(lst[1:])

print_list([1, 2, 3, 4])
```

    1
    2
    3
    4



```python
def reverse_string(text):
    if len(text) == 0:
        return text
    return reverse_string(text[1:]) + text[0]

print(reverse_string("Python"))  # Output: nohtyP
```

    nohtyP



```python
def infinite_recursion():
    return infinite_recursion()

# infinite_recursion()  # Raises RecursionError
```


```python
import sys

print(sys.getrecursionlimit())  # Default ~1000
```

    3000



```python
from functools import lru_cache

@lru_cache(maxsize=None)
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

print(fibonacci(30))  # Optimized recursion
```

    832040



```python

```


---
**Score: 10**