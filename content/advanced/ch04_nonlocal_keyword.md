---
title: Ch04 Nonlocal Keyword
date: 2025-12-26
author: Your Name
cell_count: 26
score: 25
---

# Python Nonlocal Keyword


## 1. Concept Overview
The nonlocal keyword is used within nested functions to modify variables defined in the enclosing (outer) function's scope.

It applies to:
- Variables in the immediate outer function
- Not global variables
- Not local variables of the inner function

nonlocal bridges the scope between nested functions and their parent function.


## 2. Why nonlocal Exists
By default, Python treats any variable assigned inside a function as local to that function, leading to UnboundLocalError when trying to modify an outer variable without nonlocal.



```python
def outer():
    count = 0

    def inner():
        nonlocal count
        count += 1
        return count

    return inner

counter = outer()
print(counter())
print(counter())

```

nonlocal tells Python to bind count from the enclosing scope.


## 3. How nonlocal Works



```python
def parent():
    message = "Hello"

    def child():
        nonlocal message
        message = "Updated Message"
        print(message)

    child()
    print(message)

parent()

```

child modifies message in the parent scope; change persists.


## 4. nonlocal vs Local vs Global
Keyword | Targets | Scope Level
--- | --- | ---
none | Current function only | Local
nonlocal | Enclosing function | Nested
global | Module-level | Global



```python
x = 100

def outer():
    x = 50
    def inner():
        nonlocal x
        x += 10
        print(x)
    inner()

outer()
print(x)  # global x unchanged

```

## 5. Scoped State Maintenance Example



```python
def create_counter():
    count = 0

    def increment():
        nonlocal count
        count += 1
        return count

    return increment

counter = create_counter()
print(counter())  # 1
print(counter())  # 2
print(counter())  # 3

```

Creates private state that persists across calls.


## 6. Usage in Real-World Function Factories



```python
def tax_calculator(rate):
    tax = rate

    def calculate(amount):
        nonlocal tax
        return amount * tax

    return calculate

gst = tax_calculator(0.18)
print(gst(1000))

```

Closure + nonlocal enable dynamic configuration.


## 7. Nested Closure Control



```python
def outer():
    a = 10

    def middle():
        b = 20

        def inner():
            nonlocal b
            b += a
            return b

        return inner

    return middle()

func = outer()
print(func())

```

nonlocal modifies only direct enclosing variable (b), not a.


## 8. Error Without nonlocal



```python
def demo():
    x = 5

    def change():
        nonlocal x
        x += 1
        return x

    print(change())

demo()

```

Without nonlocal, x inside change would raise UnboundLocalError.


## 9. Enterprise Example: Session-Based Value Tracking



```python
def session_tracker(user):
    activity = 0

    def track():
        nonlocal activity
        activity += 1
        return f"{user} activity count: {activity}"

    return track

tracker = session_tracker("CSP")
print(tracker())
print(tracker())

```

Models session persistence/stateful services/user analytics handlers.


## 10. Common Use Cases
- Counters
- Logging handlers
- State machines
- Configuration wrappers
- Event-driven triggers



---
**Score: 25**