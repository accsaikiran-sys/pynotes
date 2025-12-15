---
title: Ch08 05 Operator Overloading
date: 2025-12-14
author: Your Name
cell_count: 31
score: 30
---

# Chapter 8.5: Operator Overloading in Python

This notebook covers operator overloading concepts in Python, including arithmetic operators, comparison operators, and special methods (dunder methods).

## 1. What is Operator Overloading

Operator overloading allows custom classes to define how standard operators behave using special (dunder) methods.


```python
class Number:
    def __init__(self, value):
        self.value = value
    
    def __add__(self, other):
        return self.value + other.value

n1 = Number(10)
n2 = Number(20)

print(n1 + n2)  # Output: 30
```

The + operator is redefined for the Number class.

## 2. Overloading the Addition Operator (+)


```python
class Vector:
    def __init__(self, x):
        self.x = x
    
    def __add__(self, other):
        return Vector(self.x + other.x)

v1 = Vector(5)
v2 = Vector(7)
v3 = v1 + v2

print(v3.x)  # Output: 12
```

Implements vector addition logic.

## 3. Overloading the Subtraction Operator (-)


```python
class Balance:
    def __init__(self, amount):
        self.amount = amount
    
    def __sub__(self, other):
        return Balance(self.amount - other.amount)

b1 = Balance(100)
b2 = Balance(40)

result = b1 - b2
print(result.amount)  # Output: 60
```

Custom logic for subtraction.

## 4. Overloading Multiplication Operator (*)


```python
class Repeater:
    def __init__(self, text):
        self.text = text
    
    def __mul__(self, times):
        return self.text * times

r = Repeater("AI ")
print(r * 3)  # Output: AI AI AI 
```

Defines how objects behave with *.

## 5. Overloading Division Operator (/)


```python
class Calculator:
    def __init__(self, value):
        self.value = value
    
    def __truediv__(self, other):
        return self.value / other.value

c1 = Calculator(100)
c2 = Calculator(4)

print(c1 / c2)  # Output: 25.0
```

Implements custom division logic.

## 6. Overloading Equality Operator (==)


```python
class Point:
    def __init__(self, x):
        self.x = x
    
    def __eq__(self, other):
        return self.x == other.x

p1 = Point(5)
p2 = Point(5)

print(p1 == p2)  # True
```

Controls object comparison behavior.

## 7. Overloading Less Than and Greater Than


```python
class Score:
    def __init__(self, marks):
        self.marks = marks
    
    def __lt__(self, other):
        return self.marks < other.marks
    
    def __gt__(self, other):
        return self.marks > other.marks

s1 = Score(85)
s2 = Score(70)

print(s1 > s2)  # True
```

Supports sorting and ranking operations.

## 8. Overloading In-place Operators (+=)


```python
class Counter:
    def __init__(self, value):
        self.value = value
    
    def __iadd__(self, other):
        self.value += other
        return self

c = Counter(10)
c += 5
print(c.value)  # Output: 15
```

Modifies object in-place.

## 9. Overloading String Representation (str())


```python
class Product:
    def __init__(self, name, price):
        self.name = name
        self.price = price
    
    def __str__(self):
        return f"{self.name} costs ${self.price}"

p = Product("Laptop", 1200)
print(p)  # Laptop costs $1200
```

Enhances readability of object display.

## 10. Comprehensive Operator Overloading Example


```python
class ComplexNumber:
    def __init__(self, real):
        self.real = real
    
    def __add__(self, other):
        return ComplexNumber(self.real + other.real)
    
    def __sub__(self, other):
        return ComplexNumber(self.real - other.real)
    
    def __str__(self):
        return str(self.real)

c1 = ComplexNumber(10)
c2 = ComplexNumber(3)

print(c1 + c2)  # 13
print(c1 - c2)  # 7
```

Fully custom arithmetic for a domain-specific class.


---
**Score: 30**