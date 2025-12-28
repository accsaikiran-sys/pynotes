---
title: Ch04 Functions Comprehensive Guide
date: 2025-12-26
author: Your Name
cell_count: 60
score: 60
---

# Python Functions Comprehensive Guide


## 1. What is a Function in Python
A function is a named, reusable block of code designed to perform a specific task.



```python
def greet():
    return "Hello, Python"

print(greet())

```

Functions enable code reusability, modularity, readability, and maintainability.


## 2. Function with Parameters and Return Values



```python
def add(a, b):
    return a + b

result = add(10, 20)
print(result)

```

Core components: Parameters → Input, Return → Output, Body → Logic.


## 3. Positional, Keyword, and Default Arguments



```python
def register(name, role="User"):
    return f"{name} registered as {role}"

print(register("Alice"))
print(register("Bob", role="Admin"))

```

Argument types: positional, keyword, and default.


## 4. Variable-Length Arguments (*args, **kwargs)



```python
def process(*args, **kwargs):
    print(args)
    print(kwargs)

process(1, 2, 3, mode="fast", status="active")

```

Used for flexible API design and extensibility.


## 5. Function Return Behavior



```python
def status(flag):
    if flag:
        return "Success"
    return None

print(status(True))

```

Rules: functions can return multiple values; return without value yields None; return terminates execution.


## 6. Nested Functions and Scope



```python
def outer():
    def inner():
        return "Inner Function"
    return inner()

print(outer())

```

Used in closures and encapsulation patterns.


## 7. Closures and Function Factories



```python
def power(n):
    def calculate(x):
        return x ** n
    return calculate

square = power(2)
print(square(5))

```

Closure preserves parent scope values.


## 8. Higher-Order Functions



```python
def apply(func, value):
    return func(value)

print(apply(lambda x: x * 2, 10))

```

Functions can be passed as arguments and returned from other functions.


## 9. Lambda Functions (Anonymous Functions)



```python
square = lambda x: x * x
print(square(6))

```

Best for single-line logic, inline transformations, sorting, and filtering.


## 10. Recursive Functions



```python
def factorial(n):
    if n == 0:
        return 1
    return n * factorial(n - 1)

print(factorial(5))

```

Use cases: tree traversal and divide-and-conquer algorithms.


## Advanced Function Features
### 11. Decorators (Function Enhancement)



```python
def audit(func):
    def wrapper(*args, **kwargs):
        print("Executing...")
        return func(*args, **kwargs)
    return wrapper

@audit
def save_data():
    print("Data saved")

save_data()

```

Used for logging, authorization, timing, and caching.


### 12. Generator Functions



```python
def generate_numbers():
    for i in range(3):
        yield i

for num in generate_numbers():
    print(num)

```

Benefits: memory efficiency and lazy evaluation.


### 13. Function Annotations and Type Hints



```python
def calculate(a: int, b: int) -> int:
    return a + b

```

Implements safer and more readable contracts.


### 14. Pure vs Impure Functions
Pure | Impure
--- | ---
No side effects | Modifies external state
Predictable | Unpredictable



```python
def pure(a, b):
    return a + b

```

### 15. Mutation and Side Effects



```python
values = []

def add_item(x):
    values.append(x)

add_item(5)
print(values)

```

Avoid side effects when possible for testability and scalability.


### 16. Function Introspection



```python
def demo(a, b):
    """Sample function"""

print(demo.__name__)
print(demo.__doc__)
print(demo.__annotations__)

```

Used in reflection, debugging, and dynamic systems.


### 17. Keyword-Only Arguments



```python
def configure(*, mode="safe"):
    print(mode)

configure(mode="fast")

```

Forces explicit naming for safer APIs.


### 18. Argument Validation Pattern



```python
def withdraw(balance, amount):
    if amount <= 0:
        raise ValueError("Invalid amount")
    return balance - amount

```

Essential for enterprise-grade security.


### 19. Function Composition Pattern



```python
def double(x): return x * 2

def increment(x): return x + 1

result = double(increment(5))
print(result)

```

Supports declarative pipelines.


### 20. Enterprise Example: Transaction Handler



```python
def process_transaction(user_id: int, amount: float, *, currency="USD") -> dict:
    if amount <= 0:
        raise ValueError("Invalid transaction")
    return {
        "user": user_id,
        "amount": amount,
        "currency": currency,
        "status": "success"
    }

print(process_transaction(1001, 250.50))

```

Demonstrates named-only args, validation, and structured return.



---
**Score: 60**