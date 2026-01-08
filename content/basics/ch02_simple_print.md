---
title: Ch02 Simple Print
date: 2026-01-07
author: Your Name
cell_count: 2
score: 0
---

```python




# 1
# print("1")

# print("2")


# print("10")


# 2
import sys

# limit = int(sys.argv[1])

# print(limit)

# def print_numbers(limit_x = 25):
#     for index in range(limit_x):
#         print(index + 1)


# print_numbers(limit)

class NumberPrinter:

    def __init__(self, limit_y = 20):
        print("inside init")
        self.limit = limit_y

    def __del__(self):
        print("inside destructor")

    def print_numbers(self=None):
        print("printing numbers")
        limit = self.limit if self else 20
        for index in range(limit):
            # print("abc")
            print(index + 1)

    def print_numbers_double(self):
        print("printing double")
        for index in range(self.limit):
            # 
            print(index * 2) 
```


```python

```


---
**Score: 0**