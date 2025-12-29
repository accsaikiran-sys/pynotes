---
title: Ch04 Function Scope And Lifetime
date: 2025-12-27
author: Your Name
cell_count: 37
score: 35
---

# Python Function Scope and Lifetime


## 1. Concept Overview
Function scope and lifetime determine:
- Where variables are accessible
- How long variables exist in memory

Python follows the LEGB Rule for scope resolution:
- Local
- Enclosing
- Global
- Built-in

This defines how Python resolves variable names at runtime.


## 2. Local Scope



```python
def calculate():
    result = 50
    print(result)

calculate()
# print(result)  # NameError

```

Local variables exist only during function execution.


## 3. Global Scope



```python
rate = 0.18

def compute_tax(amount):
    return amount * rate

print(compute_tax(100))

```

Accessible throughout the module unless overridden.


## 4. Enclosing Scope (Nested Functions)



```python
def outer():
    message = "Outer Scope"

    def inner():
        print(message)
    inner()

outer()

```

Inner functions can access variables from their enclosing scope.


## 5. Built-in Scope



```python
print(len([1, 2, 3]))  # len is built-in

```

Avoid overriding built-ins.


## 6. LEGB Resolution Demonstration



```python
x = "Global"

def outer():
    x = "Enclosing"

    def inner():
        x = "Local"
        print(x)

    inner()

outer()

```

Variable resolution order: Local → Enclosing → Global → Built-in.


## 7. Variable Lifetime



```python
def demo():
    temp = 25
    print(temp)

demo()
# temp is deallocated after function exit

```

## 8. Using global Keyword



```python
count = 0

def increment():
    global count
    count += 1

increment()
print(count)

```

Allows modifying global variables inside functions.


## 9. Using nonlocal Keyword



```python
def outer():
    value = 10

    def inner():
        nonlocal value
        value += 5
    inner()
    print(value)

outer()

```

Modifies variables in enclosing (non-global) scope.


## 10. Scope Isolation Examples



```python
def test():
    if True:
        x = 10
    print(x)

test()

```

Python does not have block scope; it has function scope.


## Scope Types Summary
Scope | Accessibility
--- | ---
Local | Within function
Enclosing | Outer function
Global | Module-level
Built-in | Always available


## Variable Lifetime Phases
Phase | Description
--- | ---
Initialization | Variable created
Active | In use
Termination | Destroyed (garbage collected)


## Common Pitfalls
- Forgetting global when modifying globals
- Shadowing outer scope variables
- Misusing nonlocal
- Overlapping variable names
- Accidental redefinition of built-ins


## Real-World Enterprise Example



```python
config_value = 10

def service():
    multiplier = 2

    def process():
        nonlocal multiplier
        multiplier *= config_value
        return multiplier

    return process()

print(service())

```

Used in configuration propagation, stateful closures, and session-based systems.


## Performance Implications
- Overuse of globals increases coupling
- Deeply nested scopes reduce readability
- Memory is not freed if references persist


## Best Practices
- Minimize global variable usage
- Use function parameters instead of globals
- Prefer nonlocal for closures
- Use scoped variables for clarity
- Avoid name shadowing


## Enterprise Importance
Understanding scope and lifetime ensures:
- Predictable variable behavior
- Memory efficiency
- Safer multithreading
- Bug prevention
- Maintainable architecture
Critical for backend services, AI pipeline orchestration, multi-user systems, concurrent applications, and large-scale codebases.



---
**Score: 35**