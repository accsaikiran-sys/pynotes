---
title: Ch08 03 Multiple Inheritance
date: 2025-12-24
author: Your Name
cell_count: 31
score: 30
---

# Chapter 8.3: Multiple Inheritance in Python

This notebook covers multiple inheritance concepts in Python, including Method Resolution Order (MRO), the diamond problem, and real-world applications.

## 1. What is Multiple Inheritance

Multiple inheritance occurs when a class inherits from more than one parent class.


```python
class Father:
    def skill1(self):
        print("Driving")

class Mother:
    def skill2(self):
        print("Cooking")

class Child(Father, Mother):
    pass

c = Child()
c.skill1()
c.skill2()
```

The child class gains features from all parent classes.

## 2. Basic Multiple Inheritance Structure


```python
class A:
    def show_a(self):
        print("Class A")

class B:
    def show_b(self):
        print("Class B")

class C(A, B):
    pass

obj = C()
obj.show_a()
obj.show_b()
```

The child class can access methods from both parents.

## 3. Overlapping Method Names


```python
class A:
    def display(self):
        print("From A")

class B:
    def display(self):
        print("From B")

class C(A, B):
    pass

obj = C()
obj.display()
```

Python follows Method Resolution Order (MRO) to determine which method to invoke.

## 4. Understanding Method Resolution Order (MRO)


```python
class A:
    def show(self):
        print("A")

class B:
    def show(self):
        print("B")

class C(A, B):
    pass

print(C.mro())
```

MRO defines the order of class traversal: C → A → B → object

## 5. Calling Parent Methods Explicitly


```python
class A:
    def process(self):
        print("Process A")

class B:
    def process(self):
        print("Process B")

class C(A, B):
    def process(self):
        A.process(self)
        B.process(self)

c = C()
c.process()
```

Allows execution of logic from multiple parents.

## 6. Multiple Inheritance with Constructors


```python
class A:
    def __init__(self):
        print("Constructor A")

class B:
    def __init__(self):
        print("Constructor B")

class C(A, B):
    def __init__(self):
        super().__init__()

c = C()
```

Only the first parent's constructor executes due to MRO.

## 7. Cooperative Multiple Inheritance Using super()


```python
class A:
    def __init__(self):
        print("A init")
        super().__init__()

class B:
    def __init__(self):
        print("B init")
        super().__init__()

class C(A, B):
    def __init__(self):
        print("C init")
        super().__init__()

c = C()
```

Demonstrates cooperative method chaining through MRO.

## 8. Diamond Problem Example


```python
class Grandparent:
    def greet(self):
        print("Hello from Grandparent")

class Parent1(Grandparent):
    pass

class Parent2(Grandparent):
    pass

class Child(Parent1, Parent2):
    pass

c = Child()
c.greet()
```

Python resolves this ambiguity using MRO, avoiding duplicate calls.

## 9. Visualizing the Inheritance Hierarchy


```python
class X:
    pass

class Y(X):
    pass

class Z(X):
    pass

class W(Y, Z):
    pass

print(W.mro())
```

Helps understand order of class resolution for debugging.

## 10. Real-World Multiple Inheritance Example


```python
class Logger:
    def log(self):
        print("Logging data")

class Validator:
    def validate(self):
        print("Validating data")

class Service(Logger, Validator):
    def execute(self):
        self.log()
        self.validate()
        print("Executing service")

service = Service()
service.execute()
```

Combines cross-cutting concerns such as logging and validation.


---
**Score: 30**