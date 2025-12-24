---
title: Ch05 Lists And Operations
date: 2025-12-24
author: Your Name
cell_count: 30
score: 30
---

# Python Lists and List Operations


## 1. What is a List in Python
A list is an ordered, mutable collection of elements that can store mixed data types.
Lists are one of the most frequently used data structures in Python.



```python
numbers = [1, 2, 3, 4]
mixed = [10, "Python", True, 3.14]

print(numbers)
print(mixed)

```

## 2. List Indexing and Slicing



```python
data = ["a", "b", "c", "d", "e"]

print(data[0])      # a
print(data[-1])     # e
print(data[1:4])    # ['b', 'c', 'd']
print(data[:3])     # ['a', 'b', 'c']

```

Provides precise element access and extraction.


## 3. Modifying List Elements



```python
items = [10, 20, 30]
items[1] = 99

print(items)  # [10, 99, 30]

```

Lists support direct modification due to mutability.


## 4. Adding Elements to List



```python
data = [1, 2]

data.append(3)           # Add single item
data.extend([4, 5])      # Add multiple items
data.insert(1, 10)       # Insert at index

print(data)

```

List expansion techniques: append(), extend(), insert().


## 5. Removing Elements from List



```python
values = [5, 10, 15, 20]

values.remove(10)
values.pop()
del values[0]

print(values)

```

Removal methods: remove(), pop(), del, clear().


## 6. Searching and Sorting Lists



```python
nums = [4, 1, 3, 2]

print(nums.index(3))
nums.sort()
print(nums)

nums.reverse()
print(nums)

```

Supports index(), count(), sort(), reverse().


## 7. List Comprehension (Advanced Usage)



```python
squares = [x**2 for x in range(1, 6) if x % 2 == 0]
print(squares)

```

Efficient and expressive list transformations.


## 8. Copying Lists (Shallow vs Deep)



```python
import copy

original = [1, [2, 3]]

shallow = original.copy()
deep = copy.deepcopy(original)

original[1][0] = 99

print(shallow)  # Reflects change
print(deep)     # Independent copy

```

Critical in nested list operations.


## 9. Iterating Through Lists



```python
data = ["Python", "AI", "ML"]

for index, value in enumerate(data):
    print(index, value)

```

Preferred for readability and index-aware processing.


## 10. Enterprise Example: Data Filtering Pipeline



```python
transactions = [120, -50, 300, -20, 150]

valid_transactions = [x for x in transactions if x > 0]
print(valid_transactions)

```

Used for data validation, preprocessing filters, feature selection, and ETL pipelines.



---
**Score: 30**