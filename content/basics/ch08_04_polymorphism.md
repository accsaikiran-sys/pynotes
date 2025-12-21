---
title: Ch08 04 Polymorphism
date: 2025-12-20
author: Your Name
cell_count: 31
score: 30
---

# Chapter 8.4: Polymorphism in Python

This notebook covers polymorphism concepts in Python, including method overriding, operator overloading, duck typing, and abstract base classes.

## 1. What is Polymorphism

Polymorphism allows the same interface (method or operator) to behave differently based on the object or context.


```python
print(len("Python"))   # String length
print(len([1, 2, 3]))  # List length
```

The same function works for multiple data types.

## 2. Function Polymorphism


```python
def add(a, b, c=0):
    return a + b + c

print(add(2, 3))        # 5
print(add(2, 3, 4))     # 9
```

A single function adapts behavior based on arguments.

## 3. Built-in Polymorphism


```python
print(5 + 10)          # Integer addition
print("Hello " + "AI") # String concatenation
```

The + operator behaves differently based on operand types.

## 4. Method Overriding (Runtime Polymorphism)


```python
class Animal:
    def speak(self):
        print("Animal sound")

class Dog(Animal):
    def speak(self):
        print("Dog barks")

pet = Dog()
pet.speak()
```

Child class alters the behavior of a parent method.

## 5. Operator Overloading


```python
class Vector:
    def __init__(self, x):
        self.x = x
    
    def __add__(self, other):
        return Vector(self.x + other.x)

v1 = Vector(10)
v2 = Vector(20)
v3 = v1 + v2

print(v3.x)  # Output: 30
```

Custom behavior for operators using magic methods.

## 6. Polymorphism with Different Classes


```python
class Cat:
    def sound(self):
        print("Meow")

class Dog:
    def sound(self):
        print("Bark")

def make_sound(animal):
    animal.sound()

make_sound(Cat())
make_sound(Dog())
```

Different objects responding to the same method call.

## 7. Duck Typing


```python
class Car:
    def move(self):
        print("Car moving")

class Boat:
    def move(self):
        print("Boat sailing")

def start(vehicle):
    vehicle.move()

start(Car())
start(Boat())
```

Behavior is determined by method presence, not class type.

## 8. Method Overloading via Default Arguments


```python
class Calculator:
    def multiply(self, a, b=1):
        return a * b

calc = Calculator()
print(calc.multiply(5))     # 5
print(calc.multiply(5, 3))  # 15
```

Python simulates overloading using default parameters.

## 9. Abstract Base Class Polymorphism


```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

class Rectangle(Shape):
    def area(self):
        return 10 * 5

shape = Rectangle()
print(shape.area())
```

Ensures consistent interface across implementations.

## 10. Real-World Polymorphism Example


```python
class Notification:
    def send(self):
        print("Sending notification")

class Email(Notification):
    def send(self):
        print("Sending Email")

class SMS(Notification):
    def send(self):
        print("Sending SMS")

def notify(service):
    service.send()

notify(Email())
notify(SMS())
```

Multiple behaviors implemented under a unified interface.


---
**Score: 30**