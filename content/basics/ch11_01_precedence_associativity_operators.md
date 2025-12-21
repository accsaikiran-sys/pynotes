---
title: Ch11 01 Precedence Associativity Operators
date: 2025-12-20
author: Your Name
cell_count: 35
score: 35
---

# Precedence and Associativity of Operators in Python

Understand how Python decides the order of evaluation in expressions and how associativity resolves ties.

## 1. What is Operator Precedence



```python
result = 10 + 5 * 2
print(result)  # 20, not 30
```

Multiplication (*) has higher precedence than addition (+).

## 2. What is Operator Associativity



```python
result = 100 / 10 / 2
print(result)  # 5.0
# Division is left-to-right associative: (100 / 10) / 2
```

Associativity determines the direction of evaluation for operators with the same precedence.

## 3. Using Parentheses to Override Precedence



```python
result = (10 + 5) * 2
print(result)  # 30
```

Parentheses explicitly control evaluation order.

## 4. Arithmetic Operator Precedence



```python
result = 2 + 3 * 4 - 5
print(result)  # 9
# Order: * then + then -
```

Arithmetic operators follow a defined priority where multiplication/division come before addition/subtraction.

## 5. Comparison and Logical Precedence



```python
result = 10 > 5 and 5 > 2
print(result)  # True
# Order: comparisons first, then logical AND
```

Comparisons are evaluated before logical operators like `and` and `or`.

## 6. Logical Operator Hierarchy



```python
result = True or False and False
print(result)  # True
# not > and > or, so it becomes True or (False and False)
```

Logical NOT binds tighter than AND, which binds tighter than OR.

## 7. Assignment Precedence



```python
x = y = 10 + 5
print(x, y)  # 15 15
# Assignment happens after arithmetic
```

Assignment (=) has lower precedence than arithmetic operators.

## 8. Exponentiation Associativity (Right to Left)



```python
result = 2 ** 3 ** 2
print(result)  # 512
# Evaluated as 2 ** (3 ** 2)
```

Exponentiation is right-associative, so it groups from the right.

## 9. Bitwise Operator Precedence



```python
result = 5 & 3 | 2
print(result)  # 3
# Order: & then |
```

Bitwise AND evaluates before bitwise OR for predictable results.

## 10. Complex Expression Evaluation Example



```python
result = 5 + 2 ** 3 * 4 > 20 and not False
print(result)  # True
```

Step-by-step:
- Exponentiation → 2 ** 3 = 8
- Multiplication → 8 * 4 = 32
- Addition → 5 + 32 = 37
- Comparison → 37 > 20 → True
- Logical NOT → not False → True
- AND → True and True → True

## Operator Precedence Table (High → Low)

1. ()
2. **
3. +x, -x, ~x
4. *, /, //, %
5. +, -
6. <<, >>
7. &
8. ^
9. |
10. Comparisons (==, !=, >, <, >=, <=)
11. not
12. and
13. or

## Associativity Summary

- Most operators: Left → Right
- Exponentiation (**): Right → Left
- Assignment (=): Right → Left

## Best Practices

- Use parentheses for readability and predictability.
- Avoid overly complex expressions.
- Break logic across lines if needed.
- Do not rely on memory for precedence in critical logic.

## Enterprise Relevance

- Accurate business rule logic.
- Correct financial calculations.
- Reliable conditional flows.
- Bug-free algorithm design (quant systems, validation engines, rule-based logic, workflow automation).


---
**Score: 35**