---
title: Ch09 01 List Comprehension
date: 2026-01-07
author: Your Name
cell_count: 44
score: 40
---

# Chapter 9.1: List Comprehension in Python

This notebook covers Python list comprehensions - a powerful, concise way to create lists through declarative expressions.

## 1. Strategic Overview

Python List Comprehension is a high-performance, declarative construct for generating lists through compact expressions. It replaces verbose iterative patterns with expressive, memory-efficient, and semantically rich syntax.

**It enables:**
- Concise data transformation
- Declarative iteration logic
- Higher performance than traditional loops
- Functional-style programming paradigms
- Readable, maintainable data workflows

## 2. Enterprise Significance

**Poor iteration strategies result in:**
- Bloated code
- Reduced performance
- Error-prone loop logic
- Unreadable transformation steps
- Maintenance complexity

**Strategic list comprehension usage ensures:**
- Clean data pipelines
- Optimized performance
- Predictable transformation logic
- Reduced boilerplate
- Improved developer productivity

## 3. Conceptual Execution Model

```
Source Iterable → Expression → Optional Condition → Result List
```

**Formal structure:**
```python
[expression for item in iterable if condition]
```

## 4. Basic List Comprehension


```python
# List comprehension
squares = [x**2 for x in range(5)]
print("Squares:", squares)

# Equivalent traditional loop
squares_loop = []
for x in range(5):
    squares_loop.append(x**2)
print("Squares (loop):", squares_loop)
```

## 5. Conditional Filtering


```python
# Filter even numbers
even_numbers = [x for x in range(10) if x % 2 == 0]
print("Even numbers:", even_numbers)

# Filter positive numbers
numbers = [-2, -1, 0, 1, 2, 3]
positive = [x for x in numbers if x > 0]
print("Positive numbers:", positive)
```

## 6. Nested List Comprehensions


```python
# Create a 3x3 matrix
matrix = [[i * j for j in range(3)] for i in range(3)]
print("Matrix:")
for row in matrix:
    print(row)

# Multiplication table
mult_table = [[i * j for j in range(1, 4)] for i in range(1, 4)]
print("\nMultiplication table:")
for row in mult_table:
    print(row)
```

## 7. List Comprehension with Function Calls


```python
def transform(x):
    return x * 10

def is_valid(x):
    return x > 2

# Apply function transformation
result = [transform(x) for x in range(5)]
print("Transformed:", result)

# Combine function calls
filtered_transformed = [transform(x) for x in range(5) if is_valid(x)]
print("Filtered & Transformed:", filtered_transformed)
```

## 8. Multiple Conditions


```python
# Multiple conditions with 'if'
result = [x for x in range(20) if x > 5 if x % 2 == 0]
print("Numbers > 5 and even:", result)

# Alternative with 'and'
result_and = [x for x in range(20) if x > 5 and x % 2 == 0]
print("Same with 'and':", result_and)
```

## 9. If-Else Expressions


```python
# Conditional value assignment
status = ["even" if x % 2 == 0 else "odd" for x in range(5)]
print("Status:", status)

# Grade assignment
scores = [85, 92, 78, 96, 88]
grades = ["A" if score >= 90 else "B" if score >= 80 else "C" for score in scores]
print("Grades:", grades)
```

## 10. Performance Advantage

List comprehensions are implemented in C and typically outperform equivalent loops by 20–40% for moderate workloads.


```python
import time

# Performance comparison
n = 100000

# List comprehension timing
start = time.time()
comp_result = [x**2 for x in range(n)]
comp_time = time.time() - start

# Traditional loop timing
start = time.time()
loop_result = []
for x in range(n):
    loop_result.append(x**2)
loop_time = time.time() - start

print(f"List comprehension: {comp_time:.4f} seconds")
print(f"Traditional loop: {loop_time:.4f} seconds")
print(f"Speedup: {loop_time/comp_time:.2f}x")
```

## 11. Memory Considerations

List comprehensions allocate full memory upfront. For large datasets, generator expressions are preferred:


```python
# List comprehension (allocates all memory)
squares_list = [x**2 for x in range(10)]
print("List:", squares_list)

# Generator expression (lazy evaluation)
squares_gen = (x**2 for x in range(10))
print("Generator:", squares_gen)
print("Generator values:", list(squares_gen))
```

## 12. Readability vs Complexity

**Best practice threshold:**
- ✅ Single transformation + condition
- ✅ Clear business logic
- ❌ Deep nested logic
- ❌ Multi-branch complexity


```python
# Good: Simple and readable
good_example = [x * 2 for x in range(10) if x % 2 == 0]
print("Good example:", good_example)

# Avoid: Too complex
# bad_example = [complex_func(x, y) for x in data1 for y in data2 if condition1(x) and condition2(y) and x > y]

# Better: Break into steps
data = range(10)
filtered_data = [x for x in data if x % 2 == 0]
result = [x * 2 for x in filtered_data]
print("Better approach:", result)
```

## 13. Advanced Pattern: Flattening Lists


```python
# Flatten nested lists
nested = [[1, 2], [3, 4], [5]]
flat = [item for sublist in nested for item in sublist]
print("Flattened:", flat)

# Flatten with condition
nested_mixed = [[1, 2, 3], [4, 5], [6, 7, 8, 9]]
flat_even = [item for sublist in nested_mixed for item in sublist if item % 2 == 0]
print("Flattened even numbers:", flat_even)
```

## 14. Data Cleaning Pipeline Example


```python
# ETL and preprocessing
raw = ["  apple ", " Banana", "cherry ", "  ORANGE  "]
cleaned = [item.strip().lower() for item in raw]
print("Raw data:", raw)
print("Cleaned data:", cleaned)

# Filter and clean
raw_numbers = [" 123 ", "abc", "456", "  789  ", "xyz"]
clean_numbers = [int(item.strip()) for item in raw_numbers if item.strip().isdigit()]
print("Clean numbers:", clean_numbers)
```

## 15. Combining with zip()


```python
# Structured mapping pattern
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 35]
pairs = [(name, age) for name, age in zip(names, ages)]
print("Name-Age pairs:", pairs)

# Calculate with zip
list1 = [1, 2, 3, 4]
list2 = [10, 20, 30, 40]
products = [x * y for x, y in zip(list1, list2)]
print("Products:", products)
```

## 16. Dictionary Creation via List Comprehension


```python
# Dictionary comprehension (related pattern)
keys = ["a", "b", "c"]
values = [1, 2, 3]
data = {k: v for k, v in zip(keys, values)}
print("Dictionary:", data)

# Square mapping
squares_dict = {x: x**2 for x in range(5)}
print("Squares dict:", squares_dict)
```

## 17. Filtering Objects


```python
# Simulate user objects
class User:
    def __init__(self, name, is_active):
        self.name = name
        self.is_active = is_active
    
    def __repr__(self):
        return f"User({self.name}, active={self.is_active})"

users = [
    User("Alice", True),
    User("Bob", False),
    User("Charlie", True)
]

# Entity filtering in domain systems
active_users = [u for u in users if u.is_active]
print("Active users:", active_users)

# Extract names
active_names = [u.name for u in users if u.is_active]
print("Active user names:", active_names)
```

## 18. List Comprehension with Enumerate


```python
# Index-aware processing
items = ["apple", "banana", "cherry"]
indexed = [(i, v) for i, v in enumerate(items)]
print("Indexed items:", indexed)

# Filter by index
even_indexed = [v for i, v in enumerate(items) if i % 2 == 0]
print("Even indexed items:", even_indexed)
```

## 19. Set and Dict Comprehensions


```python
# Set comprehension (unified paradigm)
numbers = [1, 2, 2, 3, 3, 4]
unique = {x for x in numbers}
print("Unique set:", unique)

# Dictionary comprehension
mapped = {x: x**2 for x in range(5)}
print("Mapped dict:", mapped)

# Conditional dict comprehension
even_squares = {x: x**2 for x in range(10) if x % 2 == 0}
print("Even squares:", even_squares)
```

## 20. Comprehensions in Functional Pipelines


```python
# Efficient transformation layer
data = [-2, -1, 0, 1, 2, 3, 4, 5]

# Multi-step pipeline
pipeline = [x * 2 for x in data if x > 0]
print("Pipeline result:", pipeline)

# Chained transformations
step1 = [x for x in data if x > 0]  # Filter positive
step2 = [x * 2 for x in step1]      # Double values
step3 = [x for x in step2 if x < 10] # Filter < 10
print("Chained result:", step3)
```

## 21. Best Practices Summary

**✅ Do:**
- Keep logic simple
- Prefer readability over compactness
- Use generator for large data
- Comment complex comprehensions

**❌ Avoid:**
- Deep nested comprehensions
- Heavy logic inside comprehensions
- Side effects
- Multi-step expressions

## 22. Real-World Business Scenario


```python
# Simulate order objects
class Order:
    def __init__(self, id, amount, status):
        self.id = id
        self.amount = amount
        self.status = status
    
    def __repr__(self):
        return f"Order({self.id}, ${self.amount}, {self.status})"

orders = [
    Order(1, 1500, "completed"),
    Order(2, 800, "completed"),
    Order(3, 2000, "pending"),
    Order(4, 1200, "completed")
]

# Analytics and financial systems
high_value_orders = [o for o in orders if o.amount > 1000]
print("High value orders:", high_value_orders)

# Completed high-value orders
completed_high_value = [o for o in orders if o.amount > 1000 and o.status == "completed"]
print("Completed high-value:", completed_high_value)

# Revenue calculation
completed_revenue = sum([o.amount for o in orders if o.status == "completed"])
print(f"Total completed revenue: ${completed_revenue}")
```

## 23. Performance Comparison Summary

| Method | Speed | Readability |
|--------|-------|-------------|
| For-loop | Moderate | High |
| List Comprehension | Fast | High |
| Map/Filter | Fast | Moderate |


```python
# Comparison of different approaches
data = range(1000)

# List comprehension
comp_result = [x * 2 for x in data if x % 2 == 0]

# Map and filter
map_result = list(map(lambda x: x * 2, filter(lambda x: x % 2 == 0, data)))

# Traditional loop
loop_result = []
for x in data:
    if x % 2 == 0:
        loop_result.append(x * 2)

print("All methods produce same result:", comp_result == map_result == loop_result)
print("First 10 elements:", comp_result[:10])
```

## Summary

Python List Comprehension enables:
- **Concise and expressive iteration**
- **High-performance data transformation**
- **Declarative code architecture**
- **Maintainable transformation logic**
- **Enterprise-grade data processing workflows**

When used strategically, list comprehensions become a cornerstone of scalable, readable, and optimized Python systems — turning data iteration into clean, structured transformation pipelines.


---
**Score: 40**