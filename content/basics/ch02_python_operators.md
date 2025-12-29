---
title: Ch02 Python Operators
date: 2025-12-27
author: Your Name
cell_count: 12
score: 10
---

```python
Created:20251128
https://csp.gitbook.io/python-learning/basics/ch02-python-fundamentals/python-operators
```


```python
a = 10
b = 3

print(a + b)   # Addition → 13
print(a - b)   # Subtraction → 7
print(a * b)   # Multiplication → 30
print(a / b)   # Division → 3.333...
print(a // b)  # Floor Division → 3
print(a % b)   # Modulus → 1
print(a ** b)  # Exponentiation → 1000
```

    13
    7
    30
    3.3333333333333335
    3
    1
    1000



```python
x = 10
x += 5   # x = x + 5
x -= 2   # x = x - 2
x *= 3   # x = x * 3
x /= 2   # x = x / 2

print(x)  # Output: 19.5
```

    19.5



```python
a = 5
b = 10

print(a == b)   # Equal to → False
print(a != b)   # Not equal → True
print(a > b)    # Greater than → False
print(a < b)    # Less than → True
print(a >= b)   # Greater than or equal → False
print(a <= b)   # Less than or equal → True
```

    False
    True
    False
    True
    False
    True



```python
x = 5
y = 10

print(x > 2 and y > 5)   # True
print(x > 8 or y > 5)    # True
print(not(x > 2))        # False
```

    True
    True
    False



```python
a = 10  # 1010 in binary
b = 4   # 0100 in binary

print(a & b)   # AND → 0
print(a | b)   # OR → 14
print(a ^ b)   # XOR → 14
print(~a)      # NOT → -11
print(a << 1)  # Left shift → 20
print(a >> 1)  # Right shift → 5
```

    0
    14
    14
    -11
    20
    5



```python
fruits = ["apple", "banana", "orange"]

print("apple" in fruits)      # True
print("grape" not in fruits)  # True
```

    True
    True



```python
a = [1, 2, 3]
b = a
c = [1, 2, 3]

print(a is b)      # True (same object)
print(a is c)      # False (different objects)
print(a == c)      # True (values equal)
```

    True
    False
    True



```python
x = 5

print(+x)  # Unary plus → 5
print(-x)  # Unary minus → -5
```

    5
    -5



```python
age = 20

status = "Adult" if age >= 18 else "Minor"
print(status)  # Output: Adult
```

    Adult



```python
result = 10 + 5 * 2 ** 2
print(result)  # Output: 30
```

    30



```python

```


---
**Score: 10**