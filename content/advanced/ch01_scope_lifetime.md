---
title: Ch01 Scope Lifetime
date: 2025-12-14
author: Your Name
cell_count: 39
score: 35
---

# Python Scope and LifetimeScope defines where variables are visible; lifetime defines how long they exist in memory. Python resolves names with LEGB: Local → Enclosing → Global → Built-in.

## 1. What is Scope in Python


```python
x = 10  # Globaldef show():    y = 5  # Local    print(x, y)show()
```

Determines where Python searches for a variable during execution (LEGB).

## 2. Local Scope


```python
def calculate():    total = 100    print(total)calculate()# print(total)  # Error: total not defined
```

Local variables exist only within the function block.

## 3. Global Scope


```python
rate = 0.15def tax(amount):    return amount * rateprint(tax(1000))
```

Accessible throughout the entire module.

## 4. Enclosing Scope (Nested Functions)


```python
def outer():    msg = "Hello"    def inner():        print(msg)    inner()outer()
```

Variables from outer functions are available to inner functions.

## 5. Built-in Scope


```python
print(len([1, 2, 3]))  # len is built-in
```

Built-in names like len, sum, range, type, print should not be overridden.

## 6. LEGB Variable Resolution Example


```python
x = "Global"def outer_legb():    x = "Enclosing"    def inner():        x = "Local"        print(x)    inner()outer_legb()  # Output: Local
```

Search order: Local → Enclosing → Global → Built-in.

## 7. Lifetime of Variables


```python
def demo():    temp = 50    print(temp)demo()# temp lives only while the function executes
```

Lifetime is the duration a variable exists in memory.

## 8. Using global Keyword


```python
count = 0def increment():    global count    count += 1increment()print(count)
```

Allows modifying global variables inside functions.

## 9. Using nonlocal Keyword


```python
def outer_nonlocal():    value = 10    def inner():        nonlocal value        value += 5    inner()    print(value)outer_nonlocal()
```

Modifies variables in the enclosing scope (but not global).

## 10. Scope Isolation Example


```python
def scope_test():    a = 5    if a > 3:        b = 10    print(b)scope_test()
```

Python uses function scope (not block scope), so loop/if variables persist within the function.

## Scope Types Summary

- Local: inside function.- Enclosing: outer function of nested functions.- Global: module-level.- Built-in: Python reserved names.

## Variable Lifetime Stages

- Creation: variable defined.- Active: accessible and in memory.- Termination: garbage collected when out of scope.

## Common Scope Pitfalls

- Modifying globals without `global`.- Shadowing built-in names.- Forgetting `nonlocal` in closures.- Misunderstanding nested scopes.

## Best Practices

- Minimize use of global variables; prefer parameters.- Avoid name collisions and shadowing built-ins.- Use meaningful names and clear scope boundaries.- Encapsulate logic in functions/classes for clarity.


---
**Score: 35**