---
title: Ch03 Break Continue
date: 2025-12-26
author: Your Name
cell_count: 9
score: 5
---

```python
Created: 20251128
https://csp.gitbook.io/python-learning/basics/ch03-python-flow-control/python-break-and-continue
```


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
count = 0

while True:
    if count == 3:
        break
    print(count)
    count += 1
```

    0
    1
    2



```python
num = 0

while num < 5:
    num += 1
    if num == 2:
        continue
    print(num)
```

    1
    3
    4
    5



```python
for i in range(3):
    for j in range(5):
        if j == 2:
            break
        print(f"i={i}, j={j}")
```

    i=0, j=0
    i=0, j=1
    i=1, j=0
    i=1, j=1
    i=2, j=0
    i=2, j=1



```python
found = False

for number in range(10):
    if number == 7:
        found = True
        break

print("Found:", found)
```

    Found: True



```python
for n in range(5):
    if n == 6:
        break
else:
    print("Loop completed without break")
```

    Loop completed without break



```python

```


---
**Score: 5**