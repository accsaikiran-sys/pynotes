---
title: Ch04 03 Tuple
date: 2025-12-16
author: Your Name
cell_count: 12
score: 10
---

```python
#Created: 20251210
# https://csp.gitbook.io/python-learning/basics/ch04-python-data-types/python-tuple
```


```python
empty_tuple = ()
single_element = (10,)   # Comma required for single-element tuple
numbers = (1, 2, 3, 4)
mixed = (10, "Python", True)

print(empty_tuple)
print(single_element)
print(numbers)
print(mixed)
```

    ()
    (10,)
    (1, 2, 3, 4)
    (10, 'Python', True)



```python
colors = ("red", "green", "blue")

print(colors[0])    # First element
print(colors[-1])   # Last element
```

    red
    blue



```python
values = (0, 1, 2, 3, 4)

print(values[1:4])   # Output: (1, 2, 3)
print(values[:3])    # Output: (0, 1, 2)
```

    (1, 2, 3)
    (0, 1, 2)



```python
coords = (10, 20)

# coords[0] = 30  # This will raise TypeError
print(coords)
```

    (10, 20)



```python
person = ("Alice", 25, "Engineer")

name, age, profession = person

print(name)        # Alice
print(age)         # 25
print(profession)  # Engineer
```

    Alice
    25
    Engineer



```python
data = ((1, 2), (3, 4), (5, 6))

print(data[1])       # Output: (3, 4)
print(data[1][0])    # Output: 3
```

    (3, 4)
    3



```python
numbers = (10, 20, 30)

print(len(numbers))     # Output: 3
print(20 in numbers)    # Output: True
```

    3
    True



```python
languages = ("Python", "Java", "Go")

for lang in languages:
    print(lang)
```

    Python
    Java
    Go



```python
values = (1, 2, 3)

list_version = list(values)
tuple_again = tuple(list_version)

print(list_version)   # [1, 2, 3]
print(tuple_again)    # (1, 2, 3)
```

    [1, 2, 3]
    (1, 2, 3)



```python
def get_coordinates():
    return (40.7128, -74.0060)

lat, lon = get_coordinates()

print(lat)
print(lon)
```

    40.7128
    -74.006



```python

```


---
**Score: 10**