---
title: Ch06 Polymorphism
date: 2026-01-07
author: Your Name
cell_count: 40
score: 40
---

# Python Polymorphism

## 1. Concept Overview

Polymorphism in Python refers to the ability of different objects to respond to the same method, operator, or interface in different ways.

It enables:

- Flexible interface design
- Dynamic behavior substitution
- Decoupled architecture
- Runtime adaptability
- Scalable object models

Polymorphism allows one interface to support multiple behaviors.

## 2. Why Polymorphism Matters in Enterprise Systems

When applied correctly, polymorphism provides:

- Pluggable system components
- Extensible service models
- Reduced conditional complexity
- Clean abstraction layers
- Scalable behavioral evolution

When misused, it causes:

- Hidden behavior logic
- Runtime ambiguity
- Debugging complexity
- Performance unpredictability

## 3. Types of Polymorphism in Python

| Type | Description |
|------|-------------|
| Compile-time | Simulated via operator overloading |
| Runtime | Achieved via method overriding |
| Duck Typing | Behavior-based polymorphism |
| Parametric | Generic-like behavior |

Python primarily implements runtime polymorphism.

## 4. Basic Polymorphism Example


```python
class Dog:
    def speak(self):
        return "Bark"

class Cat:
    def speak(self):
        return "Meow"

def animal_sound(animal):
    return animal.speak()

print(animal_sound(Dog()))
print(animal_sound(Cat()))
```

Same function, different behavior.

## 5. Method Overriding (Runtime Polymorphism)


```python
class Vehicle:
    def move(self):
        return "Moving"

class Car(Vehicle):
    def move(self):
        return "Driving"

v = Car()
print(v.move())
```

The method behavior is decided at runtime.

## 6. Operator Overloading (Compile-Time Behavior)


```python
class Vector:
    def __init__(self, x):
        self.x = x

    def __add__(self, other):
        return Vector(self.x + other.x)
```

The + operator exhibits polymorphic behavior.

## 7. Duck Typing


```python
class FileLogger:
    def write(self):
        return "Writing to file"

class DBLogger:
    def write(self):
        return "Writing to database"

def log(writer):
    return writer.write()
```

Object type is irrelevant — behavior matters.

## 8. Function Polymorphism


```python
print(len("Hello"))
print(len([1, 2, 3, 4]))
```

The same function adapts to different data types.

## 9. Polymorphism with Inheritance


```python
class Shape:
    def draw(self):
        pass

class Circle(Shape):
    def draw(self):
        return "Drawing Circle"

class Square(Shape):
    def draw(self):
        return "Drawing Square"
```

Each class implements its own behavior.

## 10. Abstract Base Class Polymorphism


```python
from abc import ABC, abstractmethod

class Payment(ABC):
    @abstractmethod
    def process(self):
        pass

class CreditCard(Payment):
    def process(self):
        return "Processing credit card payment"
```

Forces structured polymorphic behavior.

## 11. Polymorphism in Interface Design


```python
def process_item(item):
    return item.execute()
```

As long as the object implements execute(), it works.

## 12. Polymorphism vs Conditional Logic

❌ Bad:


```python
if type(obj) == A:
    obj.method_a()
elif type(obj) == B:
    obj.method_b()
```

✅ Good:


```python
obj.process()
```

Reduces coupling and increases modularity.

## 13. Real-World Example: Payment Gateway


```python
class PaymentGateway:
    def pay(self):
        raise NotImplementedError

class PayPal(PaymentGateway):
    def pay(self):
        return "Paying via PayPal"

class Stripe(PaymentGateway):
    def pay(self):
        return "Paying via Stripe"
```

Used in:

- E-commerce
- FinTech platforms
- SaaS billing systems

## 14. Dynamic Polymorphism


```python
def identify(obj):
    await obj.execute()
```

Runtime behavior changes dynamically.

## 15. Polymorphism in API Frameworks

Frameworks like Django and FastAPI rely on polymorphism to:

- Handle different request types
- Route data dynamically
- Abstract service interfaces


---
**Score: 40**