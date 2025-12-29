---
title: Ch06 Oop
date: 2025-12-27
author: Your Name
cell_count: 43
score: 40
---

# Python Object-Oriented Programming


## 1. Concept Overview
Object-Oriented Programming (OOP) in Python is a programming paradigm that structures code around objects — entities that combine data (attributes) and behavior (methods).

It provides:

- Modularity
- Reusability
- Abstraction
- Scalability
- Maintainability

OOP is central to enterprise-grade system design and architecture.


## 2. Core OOP Principles
Python implements the four classical OOP pillars:

| Principle | Definition |
| --- | --- |
| Encapsulation | Hiding internal data |
| Abstraction | Exposing essential behavior |
| Inheritance | Reusing parent class features |
| Polymorphism | Multiple behavior forms |


## 3. Defining a Class and Creating Objects



```python
class User:
    def __init__(self, name, role):
        self.name = name
        self.role = role

    def display(self):
        return f"{self.name} ({self.role})"

user1 = User("Alice", "Admin")
print(user1.display())

```

Here:

- User is a class
- user1 is an object


## 4. Encapsulation (Data Hiding)



```python
class Account:
    def __init__(self, balance):
        self.__balance = balance

    def get_balance(self):
        return self.__balance

```

__balance is private and cannot be accessed directly.


## 5. Abstraction



```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

```

Forces child classes to implement specific methods.


## 6. Inheritance



```python
class Animal:
    def sound(self):
        return "Some sound"

class Dog(Animal):
    def sound(self):
        return "Bark"

```

Dog inherits features from Animal.


## 7. Polymorphism



```python
def make_sound(animal):
    print(animal.sound())

make_sound(Dog())

```

Same function behaves differently for different objects.


## 8. Constructors & Destructors



```python
class Resource:
    def __init__(self):
        print("Acquired")

    def __del__(self):
        print("Released")

```

Manages resource lifecycle.


## 9. Class Variables vs Instance Variables



```python
class Counter:
    count = 0

    def __init__(self):
        Counter.count += 1

```

Class variable shared, instance variable unique.


## 10. Method Types



```python
class Example:
    @staticmethod
    def greet():
        return "Hello"

    @classmethod
    def info(cls):
        return cls.__name__

```

Method Types:

- Instance
- Class
- Static


## 11. Dunder (Magic) Methods



```python
class Vector:
    def __init__(self, x):
        self.x = x

    def __add__(self, other):
        return Vector(self.x + other.x)

```

Supports operator overloading.


## 12. Multiple Inheritance



```python
class A:
    def method(self):
        return "A"

class B:
    def method(self):
        return "B"

class C(A, B):
    pass

print(C().method())

```

Python resolves via MRO (Method Resolution Order).


## 13. Composition Over Inheritance



```python
class Engine:
    def start(self):
        return "Engine started"

class Car:
    def __init__(self):
        self.engine = Engine()

```

Preferred for flexible architectures.


## 14. Enterprise Example: Domain Model



```python
class Transaction:
    def __init__(self, user_id, amount):
        self.user_id = user_id
        self.amount = amount

    def process(self):
        return f"Processed {self.amount} for {self.user_id}"

```

Used in:

- Banking systems
- ERP software
- Payment platforms


## 15. OOP vs Procedural Programming

| OOP | Procedural |
| --- | --- |
| Structured around objects | Structured around functions |
| High scalability | Limited scalability |
| Encapsulation | No data hiding |
| Easier maintenance | Harder for large systems |


## 16. Key OOP Patterns

| Pattern | Use Case |
| --- | --- |
| Singleton | One instance |
| Factory | Object creation control |
| Strategy | Dynamic behavior switching |
| Observer | Event notification |


## 17. Best Practices
- Prefer composition over inheritance
- Use private attributes carefully
- Keep classes focused
- Follow SOLID principles
- Avoid God objects


## 18. Common Mistakes
- Overusing inheritance
- Not using encapsulation
- Tight coupling
- Ignoring abstraction
- Mixing business logic across classes



---
**Score: 40**