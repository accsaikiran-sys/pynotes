---
title: Ch11 03 Asserts
date: 2025-12-20
author: Your Name
cell_count: 34
score: 30
---

# Python Asserts

Using assertions to validate internal logic and invariants during development and testing.

## 1. What is an Assertion



```python
x = 10
assert x > 0
print('Assertion passed for x > 0')
```

An assertion tests a condition and raises `AssertionError` if it is False.

## 2. Basic Assertion Syntax



```python
age = 18
assert age >= 18
print('Age is valid')
```

Program continues only if the condition is true.

## 3. Assertion with Custom Message



```python
score = 40
assert score >= 50, 'Score must be at least 50 to pass'
```

Custom messages provide clear context on failure.

## 4. Assertion Failure Example



```python
value = -5
assert value > 0, 'Value must be positive'
```

When the condition fails, Python raises `AssertionError: Value must be positive`. Useful during validation and debugging.

## 5. Using Assertions in Functions



```python
def calculate_square(num):
    assert isinstance(num, int), 'Input must be an integer'
    return num * num

print(calculate_square(5))
```

Ensures correct parameter usage before proceeding.

## 6. Assertions for Invariant Checks



```python
def withdraw(balance, amount):
    assert amount <= balance, 'Insufficient balance'
    return balance - amount

print(withdraw(500, 600))
```

Guarantees logical consistency during execution.

## 7. Assertions vs Exception Handling


- Assertion: `assert x != 0, 'x must not be zero'` (debugging aid, can be disabled).
- Exception: 
```python
if x == 0:
    raise ValueError('x must not be zero')
```
Use assertions for internal logic; use exceptions for user-input validation and production safety.

## 8. Disabling Assertions in Production



```python
# Run Python with -O to remove assertions at runtime
# python -O script.py
```

Assertions are stripped when running with optimization (-O). Do not rely on them for critical runtime checks.

## 9. Advanced Assertion with Complex Logic



```python
def process_data(data):
    assert data is not None and len(data) > 0, 'Data cannot be empty'
    return sum(data)

print(process_data([10, 20, 30]))
```

Combines multiple conditions to enforce data validity.

## 10. Enterprise Use Case: Defensive Programming



```python
def process_order(order):
    assert 'id' in order, 'Order must contain ID'
    assert order['amount'] > 0, 'Order amount must be positive'
    return 'Order Processed'

order = {'id': 101, 'amount': 250}
print(process_order(order))
```

Keeps internal system contracts valid. Replace with exceptions for user-facing validation in production.

## Assertion Lifecycle
- Development: detect logical errors early.
- Testing: enforce internal rules.
- Production: typically disabled or replaced by explicit exceptions.

## Best Practices
- Use assertions for internal logic validation.
- Avoid using them for user-input validation.
- Keep conditions simple and side-effect free.
- Combine with logging for traceability.

## Common Mistakes
- Using asserts for runtime error handling.
- Relying on asserts in production logic (they can be disabled).
- Overly complex assertion expressions.
- Forgetting that assertions vanish under -O.

## Enterprise Importance
- Detect programming errors early and preserve invariants.
- Improve reliability in AI pipelines, financial computations, workflow engines, and backend services.


---
**Score: 30**