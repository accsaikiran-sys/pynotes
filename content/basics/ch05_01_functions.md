---
title: Ch05 01 Functions
date: 2025-12-10
author: Your Name
cell_count: 12
score: 10
---

```python
#Created: 20251210
# https://csp.gitbook.io/python-learning/basics/ch05-python-functions/python-functions
```


```python
def greet():
    print("Hello, Python!")

greet()
```

    Hello, Python!



```python
def greet_user(name):
    print(f"Hello, {name}!")

greet_user("Alice")
```

    Hello, Alice!



```python
def add(a, b):
    return a + b

result = add(5, 3)
print(result)  # Output: 8
```

    8



```python
def greet(name="Guest"):
    print(f"Hello, {name}!")

greet()
greet("Bob")
```

    Hello, Guest!
    Hello, Bob!



```python
def student_info(name, age):
    print(f"Name: {name}, Age: {age}")

student_info(age=20, name="Alice")
```

    Name: Alice, Age: 20



```python
def sum_numbers(*args):
    return sum(args)

print(sum_numbers(1, 2, 3, 4))  # Output: 10
```

    10



```python
def display_profile(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

display_profile(name="Alice", role="Engineer")
```

    name: Alice
    role: Engineer



```python
def complete_profile(*args, **kwargs):
    print("Positional:", args)
    print("Keyword:", kwargs)

complete_profile("Python", level="Advanced", year=2025)
```

    Positional: ('Python',)
    Keyword: {'level': 'Advanced', 'year': 2025}



```python
square = lambda x: x ** 2
print(square(5))  # Output: 25
```

    25



```python
def factorial(n):
    if n == 0:
        return 1
    return n * factorial(n - 1)

print(factorial(5))  # Output: 120
```

    120



```python

```


---
**Score: 10**