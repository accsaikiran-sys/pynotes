---
title: Ch09 08 Property Decorator
date: 2025-12-20
author: Your Name
cell_count: 21
score: 20
---

# Chapter 9.8: @property Decorator in Python

This notebook covers the @property decorator - a powerful tool for creating attribute-like access to methods with controlled logic, validation, and encapsulation.

## 1. What is @property

The @property decorator allows a method to be accessed like an attribute while still providing controlled logic behind the scenes.


```python
# Basic @property example
class Person:
    def __init__(self, name):
        self._name = name
    
    @property
    def name(self):
        return self._name

p = Person("Alice")
print(f"Name: {p.name}")  # Alice - accessed like an attribute

# Compare with regular method
class PersonWithMethod:
    def __init__(self, name):
        self._name = name
    
    def get_name(self):
        return self._name

p2 = PersonWithMethod("Bob")
print(f"Name (method): {p2.get_name()}")  # Requires parentheses

# Demonstrate the difference
print(f"\nProperty access: p.name = {p.name}")
print(f"Method access: p2.get_name() = {p2.get_name()}")

# Show that it's still a method underneath
print(f"\nType of Person.name: {type(Person.name)}")
print(f"Type of PersonWithMethod.get_name: {type(PersonWithMethod.get_name)}")
```

## 2. Encapsulation Using @property

Prevents direct access to internal variables while still exposing data.


```python
class Product:
    def __init__(self, price):
        self._price = price
    
    @property
    def price(self):
        return self._price

item = Product(100)
print(f"Product price: ${item.price}")

# The underscore convention indicates "private" - discourage direct access
print(f"Direct access (not recommended): ${item._price}")
```

## 3. Read-Only Property

Computed properties behave like read-only attributes.


```python
class Circle:
    def __init__(self, radius):
        self._radius = radius
    
    @property
    def area(self):
        return 3.14 * self._radius ** 2
    
    @property
    def radius(self):
        return self._radius

c = Circle(5)
print(f"Circle radius: {c.radius}")
print(f"Circle area: {c.area}")

# Try to set area (this will fail)
try:
    c.area = 100
except AttributeError as e:
    print(f"Error: {e}")
```

## 4. Using @property with Setter

Allows controlled updates with validation.


```python
class Employee:
    def __init__(self, salary):
        self._salary = salary
    
    @property
    def salary(self):
        return self._salary
    
    @salary.setter
    def salary(self, value):
        if value < 0:
            raise ValueError("Salary cannot be negative")
        self._salary = value

e = Employee(5000)
print(f"Initial salary: ${e.salary}")

e.salary = 6000
print(f"Updated salary: ${e.salary}")

# Try to set negative salary
try:
    e.salary = -1000
except ValueError as error:
    print(f"Validation error: {error}")
```

## 5. @property with Deleter

Supports controlled deletion of attributes.


```python
class Account:
    def __init__(self, balance):
        self._balance = balance
    
    @property
    def balance(self):
        return self._balance
    
    @balance.deleter
    def balance(self):
        print("Deleting balance...")
        del self._balance
    
    def has_balance(self):
        return hasattr(self, '_balance')

acc = Account(1000)
print(f"Account balance: ${acc.balance}")
print(f"Has balance: {acc.has_balance()}")

del acc.balance
print(f"Has balance after deletion: {acc.has_balance()}")

# Try to access deleted balance
try:
    print(acc.balance)
except AttributeError as e:
    print(f"Error accessing deleted balance: {e}")
```

## 6. Computed Property Example

Encapsulates derived data logic.


```python
class Rectangle:
    def __init__(self, length, width):
        self.length = length
        self.width = width
    
    @property
    def area(self):
        return self.length * self.width
    
    @property
    def perimeter(self):
        return 2 * (self.length + self.width)
    
    @property
    def is_square(self):
        return self.length == self.width

rect = Rectangle(10, 5)
print(f"Rectangle: {rect.length} x {rect.width}")
print(f"Area: {rect.area}")
print(f"Perimeter: {rect.perimeter}")
print(f"Is square: {rect.is_square}")

# Create a square
square = Rectangle(7, 7)
print(f"\nSquare: {square.length} x {square.width}")
print(f"Is square: {square.is_square}")
```

## 7. Difference: @property vs Normal Method

@property improves readability and API design.


```python
class User:
    def __init__(self, name):
        self._name = name
    
    def get_name(self):
        return self._name
    
    @property
    def name(self):
        return self._name
    
    def get_display_name(self):
        return f"User: {self._name}"
    
    @property
    def display_name(self):
        return f"User: {self._name}"

u = User("Bob")

# Method calls require parentheses
print(f"Method call: {u.get_name()}")
print(f"Method call: {u.get_display_name()}")

# Property access looks like attribute access
print(f"Property access: {u.name}")
print(f"Property access: {u.display_name}")

# Properties feel more natural for data-like access
print(f"\nMore natural: user.name = '{u.name}'")
print(f"Less natural: user.get_name() = '{u.get_name()}'")
```

## 8. Enforcing Data Integrity

Common pattern for safe state management.


```python
class Temperature:
    def __init__(self, celsius):
        self._celsius = celsius
    
    @property
    def celsius(self):
        return self._celsius
    
    @celsius.setter
    def celsius(self, value):
        if value < -273.15:
            raise ValueError("Temperature below absolute zero")
        self._celsius = value
    
    @property
    def fahrenheit(self):
        return (self._celsius * 9/5) + 32
    
    @fahrenheit.setter
    def fahrenheit(self, value):
        celsius_value = (value - 32) * 5/9
        if celsius_value < -273.15:
            raise ValueError("Temperature below absolute zero")
        self._celsius = celsius_value
    
    @property
    def kelvin(self):
        return self._celsius + 273.15

# Valid temperature
temp = Temperature(25)
print(f"Temperature: {temp.celsius}°C = {temp.fahrenheit}°F = {temp.kelvin}K")

# Update via Fahrenheit
temp.fahrenheit = 100
print(f"Boiling point: {temp.celsius}°C = {temp.fahrenheit}°F = {temp.kelvin}K")

# Try invalid temperature
try:
    temp.celsius = -300
except ValueError as e:
    print(f"Validation error: {e}")
```

## 9. Lazy Evaluation with @property

Data is calculated only when required.


```python
import time

class DataLoader:
    def __init__(self):
        self._data = None
        self._expensive_calculation = None
    
    @property
    def data(self):
        if self._data is None:
            print("Loading data...")
            time.sleep(1)  # Simulate expensive operation
            self._data = [1, 2, 3, 4, 5]
        return self._data
    
    @property
    def expensive_calculation(self):
        if self._expensive_calculation is None:
            print("Performing expensive calculation...")
            time.sleep(0.5)  # Simulate computation
            self._expensive_calculation = sum(x**2 for x in self.data)
        return self._expensive_calculation

loader = DataLoader()
print("DataLoader created (no data loaded yet)")

print(f"\nFirst access to data: {loader.data}")
print(f"Second access to data: {loader.data}")

print(f"\nFirst expensive calculation: {loader.expensive_calculation}")
print(f"Second expensive calculation: {loader.expensive_calculation}")
```

## 10. Enterprise-Style Implementation Example

Provides clean API, robust validation, and business-rule enforcement.


```python
from datetime import datetime

class BankAccount:
    def __init__(self, owner, balance, account_type="checking"):
        self.owner = owner
        self._balance = balance
        self._account_type = account_type
        self._transactions = []
        self._created_at = datetime.now()
    
    @property
    def balance(self):
        return self._balance
    
    @balance.setter
    def balance(self, amount):
        if amount < 0:
            raise ValueError("Balance cannot be negative")
        
        old_balance = self._balance
        self._balance = amount
        
        # Log transaction
        self._transactions.append({
            'timestamp': datetime.now(),
            'old_balance': old_balance,
            'new_balance': amount,
            'change': amount - old_balance
        })
    
    @property
    def account_type(self):
        return self._account_type
    
    @account_type.setter
    def account_type(self, acc_type):
        valid_types = ["checking", "savings", "business"]
        if acc_type not in valid_types:
            raise ValueError(f"Account type must be one of: {valid_types}")
        self._account_type = acc_type
    
    @property
    def account_age_days(self):
        return (datetime.now() - self._created_at).days
    
    @property
    def transaction_count(self):
        return len(self._transactions)
    
    @property
    def account_summary(self):
        return {
            'owner': self.owner,
            'balance': self.balance,
            'type': self.account_type,
            'age_days': self.account_age_days,
            'transactions': self.transaction_count
        }
    
    def deposit(self, amount):
        if amount <= 0:
            raise ValueError("Deposit amount must be positive")
        self.balance = self.balance + amount
    
    def withdraw(self, amount):
        if amount <= 0:
            raise ValueError("Withdrawal amount must be positive")
        if amount > self.balance:
            raise ValueError("Insufficient funds")
        self.balance = self.balance - amount

# Create and use the account
account = BankAccount("Alice Johnson", 1000)
print(f"Initial account: {account.account_summary}")

# Make some transactions
account.deposit(500)
print(f"After deposit: Balance = ${account.balance}")

account.withdraw(200)
print(f"After withdrawal: Balance = ${account.balance}")

# Change account type
account.account_type = "savings"
print(f"Account type changed to: {account.account_type}")

# Show final summary
print(f"\nFinal account summary: {account.account_summary}")

# Test validation
try:
    account.balance = -100
except ValueError as e:
    print(f"\nValidation error: {e}")

try:
    account.account_type = "invalid"
except ValueError as e:
    print(f"Validation error: {e}")
```


---
**Score: 20**