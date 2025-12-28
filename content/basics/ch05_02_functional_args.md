---
title: Ch05 02 Functional Args
date: 2025-12-26
author: Your Name
cell_count: 12
score: 10
---

```python
# Created:20251210
# https://csp.gitbook.io/python-learning/basics/ch05-python-functions/python-function-arguments
```


```python
def display_info(name, age):
    print(f"Name: {name}, Age: {age}")

display_info("Alice", 25)
```

    Name: Alice, Age: 25



```python
def greet(name="Guest"):
    print(f"Hello, {name}")

greet()
greet("Bob")
```

    Hello, Guest
    Hello, Bob



```python
def greet(name="Guest"):
    print(f"Hello, {name}")

greet()
greet("Bob")
```

    Hello, Guest
    Hello, Bob



```python
def login(username, password):
    print(f"User: {username}")

login("admin", "1234")
# login("admin")  # Raises TypeError
```

    User: admin



```python
def calculate_sum(*numbers):
    return sum(numbers)

print(calculate_sum(1, 2, 3))      # 6
print(calculate_sum(5, 10, 15, 5)) # 35
```

    6
    35



```python
def user_profile(**details):
    for key, value in details.items():
        print(f"{key}: {value}")

user_profile(name="Alice", role="Developer", level="Senior")
```

    name: Alice
    role: Developer
    level: Senior



```python
def full_profile(name, *skills, **info):
    print("Name:", name)
    print("Skills:", skills)
    print("Details:", info)

full_profile("Alice", "Python", "ML", age=30, city="Toronto")
```

    Name: Alice
    Skills: ('Python', 'ML')
    Details: {'age': 30, 'city': 'Toronto'}



```python
def divide(a, b, /):
    return a / b

print(divide(10, 2))
# divide(a=10, b=2)  # Raises TypeError
```

    5.0



```python
def configure(*, mode="light"):
    print(f"Mode: {mode}")

configure(mode="dark")
```

    Mode: dark



```python
def multiply(a, b, c):
    return a * b * c

values = (2, 3, 4)
print(multiply(*values))  # Output: 24

data = {"a": 1, "b": 2, "c": 3}
print(multiply(**data))   # Output: 6
```

    24
    6



```python

```


---
**Score: 10**