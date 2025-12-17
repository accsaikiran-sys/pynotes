---
title: Ch04 Closures And Nested Functions
date: 2025-12-17
author: Your Name
cell_count: 30
score: 30
---

# Closures and Nested Functions


## 1. Concept Overview
Nested Functions: functions defined inside another function.
Closures: nested functions that remember and retain access to variables from their enclosing scope, even after the outer function has finished execution. This enables persistent state without using global variables or classes.


## 2. Defining a Nested Function



```python
def outer():
    def inner():
        print("Inner function executed")
    inner()

outer()

```

inner exists only inside outer and cannot be accessed globally.


## 3. Basic Closure Example



```python
def outer(message):
    def inner():
        print(message)
    return inner

func = outer("Hello from Closure")
func()

```

Even after outer finishes, inner remembers message—core closure principle.


## 4. Closure Memory Retention



```python
def multiplier(factor):
    def multiply(value):
        return value * factor
    return multiply

double = multiplier(2)
triple = multiplier(3)

print(double(10))
print(triple(10))

```

Each closure maintains its own independent state.


## 5. Variable Binding in Closures



```python
def make_counter():
    count = 0

    def increment():
        nonlocal count
        count += 1
        return count

    return increment

counter = make_counter()
print(counter())
print(counter())

```

Uses nonlocal to modify enclosing scope state.


## 6. Understanding the Closure Mechanism



```python
def outer():
    x = 10
    def inner():
        print(x)
    return inner

closure_func = outer()
print(closure_func.__closure__)

```

Closures store referenced variables in __closure__.


## 7. Closures vs Global Variables
Closures encapsulate state; globals share state. Closures are safer, more testable, and more scalable (less risky in concurrency).


## 8. Nested Scopes with Multiple Levels



```python
def level_one():
    a = "Level 1"

    def level_two():
        b = "Level 2"

        def level_three():
            print(a, b)
        return level_three

    return level_two()

func = level_one()
func()

```

Demonstrates LEGB across multiple nesting levels.


## 9. Closures in Real-World Patterns (Function Factory)



```python
def power(n):
    def calculate(x):
        return x ** n
    return calculate

square = power(2)
cube = power(3)

print(square(5))
print(cube(5))

```

Useful in strategy patterns, pipelines, and configuration binding.


## 10. Enterprise Example: Stateful Logger



```python
def logger(prefix):
    def log(message):
        print(f"[{prefix}] {message}")
    return log

error_logger = logger("ERROR")
info_logger = logger("INFO")

error_logger("Database failed")
info_logger("Service started")

```

Closure captures context dynamically for logging.


## 11. Closure as a Lightweight Class Alternative



```python
def bank_account(balance):
    def withdraw(amount):
        nonlocal balance
        if amount <= balance:
            balance -= amount
        return balance
    return withdraw

account = bank_account(1000)
print(account(200))
print(account(300))

```

Provides persistent state without OOP overhead.



---
**Score: 30**