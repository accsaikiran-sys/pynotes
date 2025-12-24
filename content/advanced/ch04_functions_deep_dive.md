---
title: Ch04 Functions Deep Dive
date: 2025-12-24
author: Your Name
cell_count: 44
score: 40
---

# Python Functions Deep Dive


## 1. What is a Function in Python
A function is a reusable block of code that performs a specific task and can return a result.



```python
def greet():
    print("Hello, Python!")

greet()

```

Functions promote: code reusability, modularity, and maintainability.


## 2. Function with Parameters



```python
def add(a, b):
    return a + b

print(add(10, 20))  # 30

```

Parameters allow dynamic input into functions.


## 3. Function with Return Value



```python
def square(num):
    return num * num

result = square(5)
print(result)

```

return sends output back to the caller.


## 4. Default Arguments



```python
def greet(name="Guest"):
    return f"Hello, {name}"

print(greet())
print(greet("Alice"))

```

Provides fallback values when arguments are not passed.


## 5. Keyword Arguments



```python
def employee(name, role):
    print(name, role)

employee(role="Engineer", name="Bob")

```

Arguments can be passed using their parameter names.


## 6. Positional vs Keyword Arguments



```python
def display(a, b):
    print(a, b)

display(1, 2)               # Positional
display(b=2, a=1)           # Keyword

```

Python supports both flexible invocation styles.


## 7. Variable Length Arguments



```python
def total(*args):
    return sum(args)

print(total(1, 2, 3, 4))

```

Allows functions to accept unlimited positional inputs.


## 8. Nested Functions



```python
def outer():
    def inner():
        return "Inner Function"
    return inner()

print(outer())

```

Used in closures and advanced functional design patterns.


## 9. Recursive Functions



```python
def factorial(n):
    if n == 1:
        return 1
    return n * factorial(n - 1)

print(factorial(5))

```

Function calling itself for repetitive problem-solving.


## 10. Lambda Functions (Anonymous Functions)



```python
square = lambda x: x * x
print(square(4))

```

Single-expression function with concise syntax.


## Advanced Function Concepts
### Function as First-Class Object



```python
def multiply(x):
    return x * 2

operation = multiply
print(operation(5))

```

Functions can be assigned to variables, passed as arguments, and returned from other functions.


### Function Annotations (Type Hints)



```python
def calculate(a: int, b: int) -> int:
    return a + b

```

Improves readability and static analysis.


### Function Lifecycle
Phase | Description
--- | ---
Definition | Function created
Invocation | Function executed
Execution | Logic runs
Return | Output returned
Completion | Control passed back


### Common Function Patterns
Pattern | Usage
--- | ---
Utility functions | Reusable tasks
Pure functions | No side effects
Callback functions | Event handlers
Decorated functions | Enhanced behavior
Recursive functions | Tree processing


## Real-World Enterprise Example



```python
def log_transaction(user_id, amount, currency="USD"):
    return {
        "user": user_id,
        "amount": amount,
        "currency": currency,
        "status": "completed"
    }

print(log_transaction(101, 250))

```

Used in microservices APIs, AI inference pipelines, financial systems, and workflow engines.


## Common Mistakes
- Forgetting return statement
- Using mutable default arguments
- Overloading functions unnecessarily
- Mixing business logic in a single function
- Deep nesting


## Best Practices
- Keep functions small and focused
- Use descriptive naming
- Follow Single Responsibility Principle
- Avoid side effects where possible
- Document functions clearly



---
**Score: 40**