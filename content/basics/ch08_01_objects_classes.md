---
title: Ch08 01 Objects Classes
date: 2025-12-24
author: Your Name
cell_count: 31
score: 30
---

# Chapter 8.1: Objects and Classes in Python

This notebook covers the fundamentals of object-oriented programming in Python, including classes, objects, and their key concepts.

## 1. What is a Class and an Object

A class is a blueprint for creating objects. An object is an instance of a class.


```python
class Person:
    pass

p1 = Person()
print(p1)
```

    <__main__.Person object at 0x72dab84bf710>


Classes define structure; objects represent real entities.

## 2. Defining a Class with Attributes


```python
class Person:
    name = "Alice"
    age = 25

p = Person()
print(p.name)
print(p.age)
```

Attributes represent properties of the class.

## 3. Constructor Method (__init__)


```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

p = Person("Bob", 30)
print(p.name, p.age)
```

The constructor initializes object data at creation.

## 4. Instance Methods


```python
class Person:
    def __init__(self, name):
        self.name = name
    
    def greet(self):
        return f"Hello, my name is {self.name}"

p = Person("Alice")
print(p.greet())
```

Instance methods operate on object data using self.

## 5. Class Variables vs Instance Variables


```python
class Student:
    school = "Global Academy"  # Class variable
    
    def __init__(self, name):
        self.name = name        # Instance variable

s1 = Student("Alice")
s2 = Student("Bob")

print(s1.school)
print(s2.school)
```

Class variables are shared; Instance variables are unique per object.

## 6. Creating Multiple Objects


```python
class Car:
    def __init__(self, brand):
        self.brand = brand

c1 = Car("Toyota")
c2 = Car("Tesla")

print(c1.brand)
print(c2.brand)
```

Multiple objects can be created from the same class.

## 7. Modifying Object Properties


```python
class Employee:
    def __init__(self, name):
        self.name = name

emp = Employee("John")
emp.name = "Michael"

print(emp.name)
```

Objects allow runtime modification of attributes.

## 8. Deleting Object Properties and Objects


```python
class Product:
    def __init__(self, price):
        self.price = price

item = Product(100)

del item.price
# del item  # Deletes the object entirely
```

Use del to remove attributes or the object itself.

## 9. Built-in Object Functions


```python
class User:
    pass

user = User()

print(isinstance(user, User))  # True
print(type(user))              # <class '__main__.User'>
```

Common object-related built-ins:
- `type()`
- `isinstance()`

## 10. Real-World Class Example


```python
class BankAccount:
    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance
    
    def deposit(self, amount):
        self.balance += amount
    
    def withdraw(self, amount):
        self.balance -= amount

account = BankAccount("Alice", 1000)
account.deposit(500)
print(account.balance)  # Output: 1500
```

Encapsulation of data and behavior into a single unit.


---
**Score: 30**