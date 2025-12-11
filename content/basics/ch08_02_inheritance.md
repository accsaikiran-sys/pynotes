---
title: Ch08 02 Inheritance
date: 2025-12-11
author: Your Name
cell_count: 31
score: 30
---

# Chapter 8.1: Inheritance in Python

This notebook covers inheritance concepts in Python object-oriented programming, including single inheritance, multiple inheritance, method overriding, and more.

## 1. What is Inheritance

Inheritance allows a class (child) to acquire properties and behaviors of another class (parent).


```python
class Animal:
    def eat(self):
        print("Animal is eating")

class Dog(Animal):
    pass

d = Dog()
d.eat()  # Inherited method
```

Promotes code reusability and hierarchical design.

## 2. Single Inheritance


```python
class Parent:
    def show(self):
        print("This is the parent class")

class Child(Parent):
    pass

c = Child()
c.show()
```

A child class inherits from one parent class.

## 3. Adding New Methods in Child Class


```python
class Animal:
    def sound(self):
        print("Some sound")

class Dog(Animal):
    def bark(self):
        print("Dog barks")

d = Dog()
d.sound()
d.bark()
```

Child classes can extend functionality beyond the parent.

## 4. Method Overriding


```python
class Animal:
    def sound(self):
        print("Animal makes sound")

class Dog(Animal):
    def sound(self):
        print("Dog barks")

d = Dog()
d.sound()  # Dog barks
```

Child class can redefine parent methods.

## 5. Using super() to Call Parent Method


```python
class Animal:
    def sound(self):
        print("Animal makes sound")

class Dog(Animal):
    def sound(self):
        super().sound()
        print("Dog barks")

d = Dog()
d.sound()
```

super() invokes the parent class method within the child.

## 6. Multilevel Inheritance


```python
class Grandparent:
    def feature(self):
        print("Grandparent feature")

class Parent(Grandparent):
    pass

class Child(Parent):
    pass

c = Child()
c.feature()
```

Inheritance chain stretches across multiple levels.

## 7. Multiple Inheritance


```python
class Father:
    def skill(self):
        print("Driving")

class Mother:
    def talent(self):
        print("Cooking")

class Child(Father, Mother):
    pass

c = Child()
c.skill()
c.talent()
```

A child class inherits from multiple parent classes.

## 8. Method Resolution Order (MRO)


```python
class A:
    def show(self):
        print("A")

class B(A):
    def show(self):
        print("B")

class C(B):
    pass

c = C()
c.show()
print(C.mro())
```

MRO defines the order in which methods are resolved in inheritance.

## 9. Constructor Inheritance


```python
class Parent:
    def __init__(self, name):
        self.name = name

class Child(Parent):
    def __init__(self, name, age):
        super().__init__(name)
        self.age = age

c = Child("Alice", 25)
print(c.name, c.age)
```

Child constructors can call parent constructors using super().

## 10. Real-World Inheritance Example


```python
class Vehicle:
    def start(self):
        print("Vehicle started")

class Car(Vehicle):
    def drive(self):
        print("Car is driving")

class Bike(Vehicle):
    def ride(self):
        print("Bike is riding")

car = Car()
bike = Bike()

car.start()
car.drive()

bike.start()
bike.ride()
```

Demonstrates inheritance in an object-oriented system.


---
**Score: 30**