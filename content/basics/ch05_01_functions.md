---
title: Ch05 01 Functions
date: 2025-12-10
author: Your Name
cell_count: 6
score: 5
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

```


---
**Score: 5**