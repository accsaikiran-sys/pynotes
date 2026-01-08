---
title: Ch06 Inheritance
date: 2026-01-07
author: Your Name
cell_count: 25
score: 25
---

# Python Inheritance

## 1. Concept Overview

Inheritance in Python is an Object-Oriented Programming (OOP) mechanism that allows a class (child) to acquire attributes and behaviors from another class (parent).

It enables:

- Code reuse
- Hierarchical classification
- Behavioral extensibility
- Polymorphic design
- Modular system architecture

Inheritance establishes an “is-a” relationship between objects.

## 2. Why Inheritance Matters in Enterprise Systems

When used correctly, inheritance provides:

- Reduced code duplication
- Standardized interfaces
- Extensible architecture
- Maintainable domain models
- Predictable system evolution

When misused, it creates:

- Rigid systems
- Tight coupling
- Fragile design
- Inheritance hell

## 3. Basic Inheritance Syntax


```python
class Animal:
    def speak(self):
        return "Some sound"

class Dog(Animal):
    def speak(self):
        return "Bark"

dog = Dog()
print(dog.speak())  # Bark
```

The Dog class inherits methods from Animal.

## 4. Parent-Child Relationship Model

Base Class (Parent) → Derived Class (Child)

Children automatically gain access to the parent's:

- Methods
- Properties
- Class variables

## 5. Types of Inheritance in Python

| Type | Description |
| :--- | :--- |
| **Single** | One parent, one child |
| **Multiple** | Multiple parents |
| **Multilevel** | Chain hierarchy |
| **Hierarchical** | Multiple children |
| **Hybrid** | Combination |

Python supports all forms through its dynamic object model.

## 6. Method Overriding

Copy

```python
class Vehicle:
    def move(self):
        return "Moving"

class Car(Vehicle):
    def move(self):
        return "Driving"
```

The child redefines parent behavior.

## 7. Using super()

Copy

```python
class Employee:
    def __init__(self, name):
        self.name = name

class Manager(Employee):
    def __init__(self, name, level):
        super().__init__(name)
        self.level = level
```

super() ensures parent logic execution.

## 8. Attribute Inheritance

Copy

```python
class Base:
    version = "1.0"

class Derived(Base):
    pass

print(Derived.version)
```

All child classes inherit static attributes.

## 9. Multilevel Inheritance Example

Copy

```python
class Shape:
    def draw(self):
        return "Drawing"

class Polygon(Shape):
    pass

class Triangle(Polygon):
    pass
```

Creates layered hierarchy.

## 10. Multiple Inheritance

Copy

```python
class Flyer:
    def fly(self):
        return "Flying"

class Swimmer:
    def swim(self):
        return "Swimming"

class Duck(Flyer, Swimmer):
    pass
```

Duck inherits behaviors from both.

## 11. Method Resolution Order (MRO)

Determines which method gets called first.

Copy

```python
print(Duck.__mro__)
```

Python uses C3 Linearization algorithm.

## 12. Cooperative Multiple Inheritance

Copy

```python
class A:
    def action(self):
        print("A")
        super().action()

class B:
    def action(self):
        print("B")
        super().action()

class C(A, B):
    def action(self):
        super().action()
```

Supports graceful call chaining.

## 13. Protected vs Private Inheritance

Python conventions:

_protected → Intended for subclass use

__private → Name mangling

## 14. Abstract Base Classes (ABC)

Copy

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass
```

Forces child implementation.

## 15. Inheritance vs Composition

Inheritance
Composition
"is-a" relationship

"has-a" relationship

Tight coupling

Loose coupling

Harder to refactor

More flexible

Enterprise systems often prefer composition.

## 16. Real-World Enterprise Example

Copy

```python
class User:
    def login(self):
        pass

class Admin(User):
    def delete_user(self):
        pass
```

Creates hierarchical permission systems.

## 17. Liskov Substitution Principle (LSP)

A subclass must be usable wherever its parent is expected.

Violation example:


Copy

```python
class Bird:
    def fly(self): pass

class Penguin(Bird):
    def fly(self): raise Exception()
```

Breaks system predictability.

## 18. Inheritance Design Patterns

Common patterns:

Template Method

Strategy (via inheritance)

Factory

Decorator

Inheritance enables scalable design frameworks.

## 19. Anti-Patterns in Inheritance

| Anti-Pattern | Impact |
| :--- | :--- |
| God classes | Unmanageable hierarchy |
| Deep inheritance tree | Complexity explosion |
| Unnecessary inheritance | Over-engineering |
| Breaking LSP | Logic inconsistency |

## 20. Best Practices

Favor composition over inheritance

Keep hierarchies shallow

Use interfaces (ABC)

Maintain clear parent responsibility

Apply SOLID principles

## 21. Enterprise Architecture Role

Inheritance is foundational in:

Domain modeling

Framework architecture

Plugin systems

Object pipelines

Enterprise APIs

When applied correctly, it drives extensibility.

## 22. Inheritance Execution Flow

Copy

Instantiate Child → Resolve MRO → Execute Overridden Methods → Delegate to Parent

Ensures predictable method resolution.

## 23. Debugging Inherited Behavior

Use:


Copy

```python
print(ClassName.__mro__)
```

To track method resolution and debug conflicts.


---
**Score: 25**