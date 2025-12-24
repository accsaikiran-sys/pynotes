---
title: Ch04 05 Set
date: 2025-12-24
author: Your Name
cell_count: 11
score: 10
---

```python
# CReated: 20251210
# https://csp.gitbook.io/python-learning/basics/ch04-python-data-types/python-set
```


```python
empty_set = set()
unique_numbers = {1, 2, 3, 4}
mixed_set = {1, "Python", 3.5, True}

print(empty_set)
print(unique_numbers)
print(mixed_set)
```

    set()
    {1, 2, 3, 4}
    {3.5, 1, 'Python'}



```python
numbers = {1, 2, 2, 3, 3, 4}
print(numbers)  # Output: {1, 2, 3, 4}
```

    {1, 2, 3, 4}



```python
fruits = {"apple", "banana"}

fruits.add("orange")
print(fruits)
```

    {'banana', 'apple', 'orange'}



```python
colors = {"red", "green"}
colors.update(["blue", "yellow"])

print(colors)
```

    {'red', 'green', 'yellow', 'blue'}



```python
numbers = {10, 20, 30, 40}

numbers.remove(20)
numbers.discard(50)  # No error if element doesn't exist

print(numbers)
```

    {40, 10, 30}



```python
data = {5, 10, 15}

print(len(data))       # Output: 3
print(10 in data)      # True
print(100 not in data) # True
```

    3
    True
    True



```python
languages = {"Python", "Java", "Go"}

for lang in languages:
    print(lang)
```

    Python
    Go
    Java



```python
A = {1, 2, 3}
B = {1, 2}

print(B.issubset(A))     # True
print(A.issuperset(B))   # True
```

    True
    True



```python
values_set = {1, 2, 3}

list_version = list(values_set)
tuple_version = tuple(values_set)

print(list_version)   # [1, 2, 3]
print(tuple_version)  # (1, 2, 3)
```

    [1, 2, 3]
    (1, 2, 3)



```python

```


---
**Score: 10**