---
title: Ch01 Variable Scope
date: 2025-12-17
author: Your Name
cell_count: 37
score: 35
---

# Python Variable Scope (Local, Global, Nonlocal)Variable scope defines where a name is accessible and modifiable. Python resolves names using LEGB: Local → Enclosing → Global → Built-in.

## 1. Local Scope


```python
def show_value():    x = 10  # Local variable    print(x)show_value()# print(x)  # NameError: x is not defined
```

Local variables exist only within the function where they are declared.

## 2. Global Scope


```python
x = 20  # Global variabledef display():    print(x)display()print(x)
```

Global variables are accessible throughout the module.

## 3. Local vs Global Variable Conflict


```python
value = 50def update():    value = 10  # Local variable shadows global    print("Inside function:", value)update()print("Outside function:", value)
```

Local variables override global variables within function scope.

## 4. Using the global Keyword


```python
count = 0def increment():    global count    count += 1increment()print(count)  # Output: 1
```

The global keyword allows modification of global variables inside functions.

## 5. Enclosing Scope (Nested Functions)


```python
def outer():    message = "Hello"    def inner():        print(message)  # Accessing enclosing variable    inner()outer()
```

Nested functions can access variables from their enclosing scope.

## 6. Using the nonlocal Keyword


```python
def outer_nonlocal():    count = 0    def inner():        nonlocal count        count += 1        print(count)    inner()    inner()outer_nonlocal()
```

nonlocal allows modification of variables from the enclosing (but not global) scope.

## 7. LEGB Rule (Scope Resolution Order)


```python
x = "Global"def outer_legb():    x = "Enclosing"    def inner():        x = "Local"        print(x)    inner()outer_legb()
```

Python resolves variables using LEGB: Local → Enclosing → Global → Built-in.

## 8. Built-in Scope


```python
print(len([1, 2, 3]))  # Built-in function
```

Built-in functions and exceptions reside in the built-in scope.

## 9. Scope Inside Loops


```python
for i in range(3):    loop_var = iprint(loop_var)  # Accessible outside loop
```

Python loop variables are function-scoped, not block-scoped.

## 10. Practical Example of Scope Management


```python
total = 100def calculate():    total = 50    def adjust():        nonlocal total        total += 10    adjust()    return totalprint(calculate())  # Output: 60print(total)        # Output: 100
```

Demonstrates coordinated use of local, enclosing, and global scopes.

## Comprehensive Guide Overview

Scope controls visibility and lifetime:- Local: inside current function.- Enclosing: outer function variables for nested functions.- Global: module-level.- Built-in: provided by Python runtime.Understanding scope prevents subtle bugs and unpredictable behavior.

## Additional Examples and Best Practices


```python
# Shadowing variablesvalue = 10def display():    value = 5    print(value)display()print(value)# Scope in conditionals (function-level)def test_block():    if True:        x = 50    print(x)test_block()
```

Best practices:- Prefer locals; minimize globals.- Use nonlocal only when maintaining closure state.- Avoid shadowing built-ins (e.g., `len`).- Pass data via parameters instead of mutating globals.- Keep naming consistent to reduce confusion.

Enterprise value: Correct scope handling yields predictable behavior, thread-safe design, clean modular architecture, and debug-friendly systems across distributed services, AI pipelines, and financial platforms.


---
**Score: 35**