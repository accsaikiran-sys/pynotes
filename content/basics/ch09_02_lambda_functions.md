---
title: Ch09 02 Lambda Functions
date: 2025-12-24
author: Your Name
cell_count: 36
score: 35
---

# Chapter 9.2: Lambda / Anonymous Functions in Python

This notebook covers Python lambda functions - small, anonymous functions that can be defined inline for concise operations.

## 1. What is a Lambda Function

A lambda function is a small anonymous function defined using the lambda keyword. It can have any number of arguments but only one expression.


```python
# Basic lambda function
square = lambda x: x ** 2
print(square(5))  # Output: 25

# Lambda for simple calculations
double = lambda x: x * 2
print(double(7))  # Output: 14
```

Lambda functions are used for concise, one-line operations.

## 2. Lambda with Multiple Arguments


```python
# Lambda with two arguments
add = lambda a, b: a + b
print(add(10, 5))  # Output: 15

# Lambda with three arguments
multiply_three = lambda x, y, z: x * y * z
print(multiply_three(2, 3, 4))  # Output: 24

# Lambda with default arguments
power = lambda x, n=2: x ** n
print(power(3))     # Output: 9 (3^2)
print(power(3, 3))  # Output: 27 (3^3)
```

Supports multiple inputs with a single return expression.

## 3. Lambda Without Assignment (Inline Usage)


```python
# Immediate execution
print((lambda x, y: x * y)(4, 5))  # Output: 20

# Complex inline calculation
result = (lambda a, b, c: (a + b) * c)(2, 3, 4)
print(result)  # Output: 20

# Conditional lambda
max_value = (lambda x, y: x if x > y else y)(10, 15)
print(max_value)  # Output: 15
```

Lambda can be defined and executed immediately.

## 4. Lambda with map()


```python
# Apply function to each element
numbers = [1, 2, 3, 4]
squares = list(map(lambda x: x ** 2, numbers))
print(squares)  # Output: [1, 4, 9, 16]

# Convert temperatures
celsius = [0, 20, 30, 40]
fahrenheit = list(map(lambda c: (c * 9/5) + 32, celsius))
print(fahrenheit)  # Output: [32.0, 68.0, 86.0, 104.0]

# String operations
words = ["hello", "world", "python"]
capitalized = list(map(lambda s: s.capitalize(), words))
print(capitalized)  # Output: ['Hello', 'World', 'Python']
```

Used to apply a function to each item in an iterable.

## 5. Lambda with filter()


```python
# Filter even numbers
numbers = [1, 2, 3, 4, 5, 6]
even_numbers = list(filter(lambda x: x % 2 == 0, numbers))
print(even_numbers)  # Output: [2, 4, 6]

# Filter positive numbers
mixed_numbers = [-3, -1, 0, 2, 5, -2]
positive = list(filter(lambda x: x > 0, mixed_numbers))
print(positive)  # Output: [2, 5]

# Filter strings by length
words = ["cat", "elephant", "dog", "butterfly"]
long_words = list(filter(lambda w: len(w) > 5, words))
print(long_words)  # Output: ['elephant', 'butterfly']
```

Filters elements based on a condition.

## 6. Lambda with reduce()


```python
from functools import reduce

# Sum all numbers
numbers = [1, 2, 3, 4]
total = reduce(lambda x, y: x + y, numbers)
print(total)  # Output: 10

# Find maximum
numbers = [3, 7, 2, 9, 1]
maximum = reduce(lambda x, y: x if x > y else y, numbers)
print(maximum)  # Output: 9

# Multiply all numbers
numbers = [2, 3, 4]
product = reduce(lambda x, y: x * y, numbers)
print(product)  # Output: 24
```

Reduces an iterable to a single result.

## 7. Lambda for Sorting Key


```python
# Sort by second element (grade)
students = [("Alice", 85), ("Bob", 72), ("Charlie", 90)]
students.sort(key=lambda x: x[1])
print("Sorted by grade:", students)

# Sort by name length
names = ["Alice", "Bob", "Charlie", "David"]
names.sort(key=lambda name: len(name))
print("Sorted by length:", names)

# Sort dictionaries
people = [
    {"name": "Alice", "age": 30},
    {"name": "Bob", "age": 25},
    {"name": "Charlie", "age": 35}
]
people.sort(key=lambda person: person["age"])
print("Sorted by age:", people)
```

Lambda is commonly used as a custom sorting key.

## 8. Lambda in List Comprehension Context


```python
# Create list of lambda functions
multipliers = [(lambda x, n=n: x * n) for n in range(1, 4)]
print(multipliers[0](5))  # Output: 5 (5 * 1)
print(multipliers[1](5))  # Output: 10 (5 * 2)
print(multipliers[2](5))  # Output: 15 (5 * 3)

# Apply different operations
operations = [
    lambda x: x + 1,
    lambda x: x * 2,
    lambda x: x ** 2
]

number = 5
results = [op(number) for op in operations]
print(f"Results for {number}:", results)  # [6, 10, 25]
```

Demonstrates functional programming patterns.

## 9. Lambda vs Normal Function


```python
# Normal function
def square_func(x):
    return x ** 2

# Lambda function
square_lambda = lambda x: x ** 2

# Both produce same result
print(square_func(4))     # 16
print(square_lambda(4))   # 16

# Performance comparison
import time

# Test with large dataset
numbers = list(range(100000))

# Normal function timing
start = time.time()
result1 = list(map(square_func, numbers))
func_time = time.time() - start

# Lambda timing
start = time.time()
result2 = list(map(square_lambda, numbers))
lambda_time = time.time() - start

print(f"Function time: {func_time:.4f}s")
print(f"Lambda time: {lambda_time:.4f}s")
print(f"Results equal: {result1 == result2}")
```

Lambda is more concise but less suitable for complex logic.

## 10. Real-World Lambda Example


```python
# Employee data processing
employees = [
    {"name": "Alice", "salary": 5000, "department": "Engineering"},
    {"name": "Bob", "salary": 3000, "department": "Marketing"},
    {"name": "Charlie", "salary": 7000, "department": "Engineering"},
    {"name": "Diana", "salary": 4500, "department": "Sales"}
]

# Find highest paid employee
highest_paid = max(employees, key=lambda emp: emp["salary"])
print("Highest paid:", highest_paid)

# Filter high earners
high_earners = list(filter(lambda emp: emp["salary"] > 4000, employees))
print("High earners:", [emp["name"] for emp in high_earners])

# Calculate total salary by department
from collections import defaultdict

dept_salaries = defaultdict(int)
for emp in employees:
    dept_salaries[emp["department"]] += emp["salary"]

# Sort departments by total salary
sorted_depts = sorted(dept_salaries.items(), key=lambda x: x[1], reverse=True)
print("Departments by total salary:", sorted_depts)

# Apply salary increase
updated_salaries = list(map(lambda emp: {**emp, "salary": emp["salary"] * 1.1}, employees))
print("After 10% increase:")
for emp in updated_salaries:
    print(f"{emp['name']}: ${emp['salary']:.2f}")
```

Lambda enables expressive data processing in analytics and business logic.

## Additional Examples: Advanced Lambda Usage


```python
# Lambda with conditional expressions
abs_value = lambda x: x if x >= 0 else -x
print(abs_value(-5))  # Output: 5
print(abs_value(3))   # Output: 3

# Lambda for data validation
is_valid_email = lambda email: "@" in email and "." in email
emails = ["user@example.com", "invalid-email", "test@domain.org"]
valid_emails = list(filter(is_valid_email, emails))
print("Valid emails:", valid_emails)

# Lambda for string processing
clean_text = lambda text: text.strip().lower().replace(" ", "_")
titles = ["  Hello World  ", "Python Programming", "  Data Science "]
cleaned = list(map(clean_text, titles))
print("Cleaned titles:", cleaned)
```

## Lambda Best Practices


```python
# ✅ Good: Simple, readable lambda
numbers = [1, 2, 3, 4, 5]
doubled = list(map(lambda x: x * 2, numbers))
print("Doubled:", doubled)

# ✅ Good: Lambda for sorting
data = [("apple", 5), ("banana", 2), ("cherry", 8)]
sorted_data = sorted(data, key=lambda item: item[1])
print("Sorted by count:", sorted_data)

# ❌ Avoid: Complex logic in lambda (use regular function instead)
# complex_lambda = lambda x: x * 2 if x > 0 else x / 2 if x < 0 else 0

# ✅ Better: Use regular function for complex logic
def process_number(x):
    if x > 0:
        return x * 2
    elif x < 0:
        return x / 2
    else:
        return 0

test_numbers = [-4, 0, 3]
processed = list(map(process_number, test_numbers))
print("Processed:", processed)
```

## Summary

Lambda functions in Python provide:
- **Concise syntax** for simple operations
- **Functional programming** capabilities
- **Inline usage** with map(), filter(), reduce()
- **Custom sorting** and data processing
- **Readable code** for simple transformations

**When to use lambda:**
- Simple, one-line operations
- Sorting keys
- Map/filter operations
- Callback functions

**When to avoid lambda:**
- Complex logic
- Multiple statements
- Reusable functions
- Functions needing documentation


---
**Score: 35**