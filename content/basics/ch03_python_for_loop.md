---
title: Ch03 Python For Loop
date: 2025-12-24
author: Your Name
cell_count: 12
score: 10
---

```python
Created: 20251128
https://csp.gitbook.io/python-learning/basics/ch03-python-flow-control/python-for-loop
```


```python
fruits = ["apple", "banana", "orange"]

for fruit in fruits:
    print(fruit)
```

    apple
    banana
    orange



```python
for i in range(5):
    print(i)
```

    0
    1
    2
    3
    4



```python
for i in range(2, 10, 2):
    print(i)
```

    2
    4
    6
    8



```python
word = "Python"

for char in word:
    print(char)
```

    P
    y
    t
    h
    o
    n



```python
languages = ["Python", "Java", "C++"]

for index, lang in enumerate(languages):
    print(index, lang)
```

    0 Python
    1 Java
    2 C++



```python
for i in range(3):
    for j in range(2):
        print(f"i={i}, j={j}")
```

    i=0, j=0
    i=0, j=1
    i=1, j=0
    i=1, j=1
    i=2, j=0
    i=2, j=1



```python
for number in range(1, 10):
    if number == 5:
        break
    print(number)
```

    1
    2
    3
    4



```python
for number in range(1, 6):
    if number == 3:
        continue
    print(number)
```

    1
    2
    4
    5



```python
for num in range(10):
    if num == 3:
        continue
    # if num == 5:
    #     break
    print(num)
else:
    print("Loop completed successfully")
```

    0
    1
    2
    4
    5
    6
    7
    8
    9
    Loop completed successfully



```python
student = {"name": "Alice", "age": 22, "grade": "A"}

for key, value in student.items():
    print(key, ":", value)
```

    name : Alice
    age : 22
    grade : A



```python

```


---
**Score: 10**