---
title: Ch04 Functions And Scope
date: 2025-12-26
author: Your Name
cell_count: 62
score: 60
---

# Functions and Scope


## 1. Strategic Overview
Functions and Scope define where names (variables, functions, constants) are visible and how they are resolved during execution. Together, they form the core of Python's execution model:

- Functions create scope boundaries
- Scope determines where a name can be read or written
- Name resolution follows a deterministic search order

In production systems, misunderstanding scope leads to subtle bugs, leaky state, hard-to-debug side effects, and unexpected interactions between modules.

Functions encapsulate behavior; scope encapsulates where names live and how they are resolved.


## 2. Enterprise Significance
Poor scope handling results in:
- Accidental dependence on globals
- Name collisions across modules
- Hidden mutations and side effects
- Non-deterministic behavior during refactors

Disciplined use of functions and scope enables predictable behavior boundaries, safer refactoring of large codebases, clear ownership of state, easy reasoning about variable lifetimes, and clean API and module design.


## 3. The LEGB Rule: Name Resolution Order
Python resolves names according to the LEGB rule:
- L – Local: Inside the current function (or comprehension)
- E – Enclosing: In any enclosing function scopes (for nested functions)
- G – Global: At module level
- B – Built-in: Python's built-in namespace (len, print, etc.)

When you reference a name, Python searches in that order.



```python
x = "global"

def outer():
    x = "enclosing"

    def inner():
        x = "local"
        print(x)

    inner()

outer()  # prints "local"

```

## 4. Function Scope: Local Namespace
A function call creates a local scope.



```python
def process_order(order_id):
    status = "PENDING"  # Local to process_order
    print(order_id, status)

```

Properties: names defined inside a function are not visible outside it; they live for the duration of the function call; different calls get independent local scopes.


## 5. Global Scope: Module Namespace
Names at the top level of a module live in the module's global scope.



```python
TIMEOUT_SECONDS = 30  # Global (module-level)

def connect():
    print(TIMEOUT_SECONDS)

```

Key points: "Global" means module-level, not entire program; each module has its own global namespace; other modules see globals via imports.


## 6. Built-in Scope
Provided by Python: core functions (len, print, sum, etc.) and exceptions (ValueError, TypeError, etc.).



```python
import builtins
print('len' in dir(builtins))

```

Best practice: avoid defining variables with the same names as built-ins to prevent shadowing.


## 7. Enclosing (Nonlocal) Scope and Nested Functions
Nested functions introduce enclosing scopes.



```python
def outer():
    message = "outer"

    def inner():
        print(message)  # from enclosing scope

    inner()

outer()

```

Foundation for closures, decorators, factory functions, and function-based configuration.


## 8. Closures: Functions Capturing Scope
A closure "remembers" variables from its enclosing scope, even after that scope has finished executing.



```python
def multiplier(factor):
    def inner(x):
        return x * factor  # captures factor
    return inner

double = multiplier(2)
print(double(10))  # 20

```

Captured variables are stored in __closure__; useful for configurable behavior and decorators.


## 9. Reading vs Writing Variables: Scope Rules
Reading follows LEGB. Writing inside a function creates/updates a local variable unless declared otherwise.



```python
x = 10

def func():
    x = 20  # local, does not change global x

func()
print(x)  # 10

```

To write to global or enclosing variables, explicitly declare intent.


## 10. global Keyword: Modifying Module-Level State



```python
counter = 0  # module-level

def increment():
    global counter
    counter += 1

increment()
print(counter)

```

Globals introduce coupling and testing challenges; use sparingly.


## 11. nonlocal Keyword: Modifying Enclosing Scope



```python
def outer():
    count = 0

    def inner():
        nonlocal count
        count += 1
        return count

    print(inner())  # 1
    print(inner())  # 2

outer()

```

Targets nearest enclosing function scope; useful for stateful closures and decorators, but can reduce clarity if overused.


## 12. Shadowing: Name Collisions Across Scopes



```python
value = "global"

def func():
    value = "local"  # shadows global
    print(value)

func()
print(value)

```

Avoid unintentional shadowing; choose descriptive names and avoid reusing names from outer scopes unless intentional.


## 13. Scope and Default Parameter Values
Defaults are evaluated once at function definition time in the defining scope.



```python
DEFAULT_TIMEOUT = 10

def connect(timeout=DEFAULT_TIMEOUT):
    return timeout

```

Mutable default anti-pattern:



```python
def add_item(item, items=[]):  # BAD
    items.append(item)
    return items

```

Fix:



```python
def add_item(item, items=None):
    if items is None:
        items = []
    items.append(item)
    return items

```

## 14. Scope in Comprehensions (Python 3+)
Comprehension variables are local to the comprehension and do not leak into surrounding scope.



```python
squares = [x * x for x in range(5)]
print('x' in globals())  # False in Python 3

```

Generator expressions also have their own scope, reducing namespace pollution.


## 15. Scope and Lambdas
Lambdas close over variables, not values.



```python
funcs = []
for i in range(3):
    funcs.append(lambda: i)

print([f() for f in funcs])  # [2, 2, 2]

# Fix using default argument capture
funcs = []
for i in range(3):
    funcs.append(lambda i=i: i)
print([f() for f in funcs])  # [0, 1, 2]

```

Critical scope behavior in real systems.


## 16. Scope and Modules: Import Patterns
Modules are scopes; import style affects visibility and maintainability.



```python
# a.py
VALUE = 10

# b.py
from a import VALUE
import a

# In b.py, VALUE is the imported name; a.VALUE refers to module attribute

```

Prefer `import module` over `from module import *`; avoid star imports to reduce collisions and improve tooling.


## 17. Functions as Scope Boundaries for Refactoring
Use functions to introduce scopes and reduce globals.



```python
def main():
    # move script logic here to limit globals
    ...

if __name__ == "__main__":
    main()

```

Localizes variables, improves testability, and reduces state leakage on import.


## 18. Scope and Testing: Isolating State
Avoid test-dependent globals and singletons with module-level state; encapsulate state in functions/classes to prevent cross-test contamination.



```python
def build_service(config):
    # config is scoped to this function
    return Service(config)

```

Test multiple configurations safely.


## 19. Scope-Aware API Design
Minimize reliance on module-level mutable state; prefer explicit parameters over hidden dependencies. If globals are used, encapsulate access.



```python
_config = {}

def set_config(cfg):
    global _config
    _config = cfg

def get_config():
    return _config

```

Better: pass config explicitly to functions and objects.


## 20. Scope in Decorators
Decorators rely on nested functions and closures.



```python
def log_calls(func):
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__}")
        return func(*args, **kwargs)
    return wrapper

```


```python
def count_calls(func):
    count = 0
    def wrapper(*args, **kwargs):
        nonlocal count
        count += 1
        print(f"{func.__name__} called {count} times")
        return func(*args, **kwargs)
    return wrapper

```

Closures and nonlocal are essential for robust decorator design.


## 21. Common Scope Anti-Patterns
Anti-Pattern | Risk/Impact
--- | ---
Overuse of global for shared state | Tight coupling, unpredictable behavior
Hidden dependencies on module-level variables | Hard-to-test, fragile refactors
Name shadowing of built-ins (e.g., list) | Confusing errors, broken expectations
Complex nested closures with nonlocal webs | Hard-to-reason-about state, maintenance hazards
Relying on default scope leaks (Py2 habits) | Wrong mental model, subtle bugs in Py3


## 22. Governance Model: Functions + Scope
Intent → Function Boundary → Scope Definition → Name Resolution (LEGB) → State Ownership (local/enclosing/global) → Mutation Rules (local/global/nonlocal) → Testability & Refactorability.

Decisions should be explicit about where state lives, intentional about where names are read/written, and designed for long-term maintainability.



---
**Score: 60**