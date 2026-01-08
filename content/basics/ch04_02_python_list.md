---
title: Ch04 02 Python List
date: 2026-01-07
author: Your Name
cell_count: 12
score: 10
---

```python
# Created: 20251210
# https://csp.gitbook.io/python-learning/basics/ch04-python-data-types/python-list
```


```python
empty_list = []
numbers = [1, 2, 3, 4, 5]
mixed = [10, "Python", True, 5.5]

print(empty_list)
print(numbers)
print(mixed)
```

    []
    [1, 2, 3, 4, 5]
    [10, 'Python', True, 5.5]



```python
fruits = ["apple", "banana", "orange"]

print(fruits[0])   # First element
print(fruits[-1])  # Last element
```

    apple
    orange



```python
numbers = [0, 1, 2, 3, 4, 5]

print(numbers[1:4])   # Output: [1, 2, 3]
print(numbers[:3])    # Output: [0, 1, 2]
print(numbers[3:])    # Output: [3, 4, 5]
```

    [1, 2, 3]
    [0, 1, 2]
    [3, 4, 5]



```python
items = ["pen", "pencil", "eraser"]
items[1] = "marker"

print(items)  # Output: ['pen', 'marker', 'eraser']
```

    ['pen', 'marker', 'eraser']



```python
numbers = [1, 2, 3]

numbers.append(4)
numbers.insert(1, 10)

print(numbers)  # Output: [1, 10, 2, 3, 4]
```

    [1, 10, 2, 3, 4]



```python
data = [10, 20, 30, 40]

data.remove(20)

print(data)

last = data.pop()

print(data)  # Output: [10, 30]
print(last)  # Output: 40

```

    [10, 30, 40]
    [10, 30]
    40



```python
values = [5, 10, 15]

print(len(values))       # Output: 3
print(10 in values)      # Output: True
print(100 not in values) # Output: True
```

    3
    True
    True



```python
cities = ["New York", "London", "Tokyo"]

for city in cities:
    print(city)
```

    New York
    London
    Tokyo



```python
squares = [x**2 for x in range(5)]
print(squares)  # Output: [0, 1, 4, 9, 16]
```

    [0, 1, 4, 9, 16]



```python
numbers = [4, 1, 3, 2]

numbers.sort()
print(numbers)  # Output: [1, 2, 3, 4]

numbers.reverse()
print(numbers)  # Output: [4, 3, 2, 1]
```

    [1, 2, 3, 4]
    [4, 3, 2, 1]



```python

```


---
**Score: 10**