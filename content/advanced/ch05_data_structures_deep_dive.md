---
title: Ch05 Data Structures Deep Dive
date: 2025-12-20
author: Your Name
cell_count: 32
score: 30
---

# Python Data Structures Deep Dive


## 1. Overview of Python Data Structures
Python provides built-in data structures for efficient data storage and manipulation:
- List → Ordered, mutable sequence
- Tuple → Ordered, immutable sequence
- Set → Unordered, unique elements
- Dictionary → Key-value mapping



```python
data = [1, 2, 3]          # List
coords = (10, 20)         # Tuple
unique = {1, 2, 3}        # Set
user = {"id": 101}        # Dictionary

```

Each structure is optimized for specific use-cases.


## 2. Advanced List Operations



```python
numbers = [5, 2, 9, 1]

numbers.append(7)
numbers.sort()
numbers.reverse()

print(numbers)

```

Key capabilities: dynamic resizing, index-based access, rich built-in methods (append, extend, remove, pop, sort, copy).


## 3. List Comprehension for High Performance



```python
squares = [x ** 2 for x in range(1, 6)]
print(squares)

```

List comprehensions offer faster execution, cleaner syntax, and readable transformations.


## 4. Tuple Immutability & Performance



```python
coordinates = (10, 20, 30)
# coordinates[0] = 5  # Error - Immutable

```

Benefits: faster than lists, safer for constant data, hashable (usable as dict keys).


## 5. Set Operations & Mathematical Use



```python
a = {1, 2, 3, 4}
b = {3, 4, 5}

print(a | b)   # Union
print(a & b)   # Intersection
print(a - b)   # Difference

```

Sets excel at deduplication, membership testing, and mathematical operations.


## 6. Dictionary Deep Dive (Key-Value Engine)



```python
employee = {
    "name": "Alice",
    "role": "Engineer",
    "salary": 80000
}

employee["department"] = "AI"
print(employee.get("role"))

```

Advanced features: fast lookup (hash-based), dynamic keys, nested mapping support.


## 7. Nested Data Structures



```python
company = {
    "employees": [
        {"name": "Alice", "id": 1},
        {"name": "Bob", "id": 2}
    ]
}

print(company["employees"][0]["name"])

```

Used in JSON structures, API payloads, and database models.


## 8. Specialized Data Structures


### deque (Double-ended Queue)



```python
from collections import deque

dq = deque([1, 2, 3])
dq.appendleft(0)
dq.append(4)

print(dq)

```

Optimized for fast appends/pops on both ends.


### heapq (Priority Queue)



```python
import heapq

nums = [5, 1, 3]
heapq.heapify(nums)
heapq.heappush(nums, 0)
print(heapq.heappop(nums))

```

Used in scheduling algorithms and optimized sorting.


## 9. Comparative Complexity
Structure | Access | Insert | Delete
--- | --- | --- | ---
List | O(1) | O(n) | O(n)
Tuple | O(1) | N/A | N/A
Set | O(1) | O(1) | O(1)
Dict | O(1) | O(1) | O(1)
Understanding complexity is vital for performance-critical systems.


## 10. Enterprise Example: Data Pipeline Structure



```python
pipeline = {
    "users": [
        {"id": 1, "name": "Alice", "skills": {"Python", "ML"}},
        {"id": 2, "name": "Bob", "skills": {"Java", "Cloud"}}
    ],
    "metadata": {
        "version": "1.0",
        "record_count": 2
    }
}

print(pipeline["users"][0]["skills"])

```


---
**Score: 30**