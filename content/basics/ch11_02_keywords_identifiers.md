---
title: Ch11 02 Keywords Identifiers
date: 2026-01-07
author: Your Name
cell_count: 33
score: 30
---

# Python Keywords and Identifiers

Overview of reserved keywords and how to name identifiers in Python.

## 1. What are Python Keywords



```python
import keyword

print(keyword.kwlist)
```

Keywords are reserved words that define Python syntax and cannot be used as identifiers.
Examples: if, else, while, class, def, return, try, except, True, False, None

## 2. List of Python Keywords (Core Examples)



```python
import keyword

for word in keyword.kwlist:
    print(word)
```

Common categories:
- Control Flow: if, elif, else, for, while, break, continue
- Function & Class: def, return, class, lambda
- Exception Handling: try, except, finally, raise
- Logical: and, or, not, is, in

## 3. What are Identifiers



```python
total = 100
def calculate_sum():
    pass

class User:
    pass

print(total, calculate_sum, User)
```

Identifiers name variables, functions, classes, modules, or objects.

## 4. Rules for Identifiers



```python
valid_name = 10
_invalid = 20
# 1value = 30  # Invalid: starts with digit
print(valid_name, _invalid)
```

Identifier rules:
- Start with a letter (a-z, A-Z) or underscore (_).
- Do not start with a digit.
- Only letters, digits, and underscores are allowed.
- Cannot be a Python keyword.

## 5. Case Sensitivity in Identifiers



```python
value = 10
Value = 20

print(value)  # 10
print(Value)  # 20
```

`value` and `Value` are different identifiers.

## 6. Invalid Identifier Examples



```python
# 2data = 100      # Starts with digit (Invalid)
# class = 10       # Keyword (Invalid)
# my-name = 5      # Special character (Invalid)
print('Invalid examples are commented out to keep code runnable')
```

Python enforces strict syntax rules for naming identifiers.

## 7. Naming Conventions (PEP 8 Standard)



```python
# Variable
total_price = 500

# Function
def calculate_total():
    pass

# Class
class UserAccount:
    pass

print(total_price, calculate_total, UserAccount)
```

Conventions: variables/functions → snake_case, classes → PascalCase, constants → UPPER_CASE.

## 8. Difference Between Keywords and Identifiers


- Keywords: reserved words that control Python syntax (e.g., `if`, `class`).
- Identifiers: user-defined names for variables, functions, classes (e.g., `count`, `UserData`).
- Keywords cannot be customized; identifiers are user-chosen within naming rules.

## 9. Checking if a Word is a Keyword



```python
import keyword

print(keyword.iskeyword("if"))      # True
print(keyword.iskeyword("value"))   # False
```

Useful for compilers, linters, and code validators.

## 10. Real-World Naming Example



```python
class OrderProcessor:
    def calculate_tax(self, amount):
        tax_rate = 0.18
        return amount * tax_rate

processor = OrderProcessor()
print(processor.calculate_tax(1000))
```

Demonstrates professional, readable identifiers in practice.

## Summary
- Keyword: reserved word in Python.
- Identifier: user-defined name for entities.
- Naming rules: start with letter/underscore, no keywords, case-sensitive.
- Conventions: follow PEP 8 for clarity.

## Best Practices
- Never use keywords as identifiers.
- Use meaningful, descriptive names.
- Keep naming consistent and follow PEP 8.
- Avoid single-character names in production code.

## Enterprise Importance
- Improves readability and maintainability.
- Lowers bug rates via clear intent.
- Supports scalable architectures and team standards in APIs, AI/ML pipelines, and large systems.


---
**Score: 30**