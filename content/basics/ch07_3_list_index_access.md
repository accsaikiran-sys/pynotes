---
title: Ch07 3 List Index Access
date: 2025-12-10
author: Your Name
cell_count: 2
score: 0
---

# ch07_3_list_index_access

Created: 20251121


```python
my_list = ["apple", "banana", "cherry"]

try:
    index = int(input("Enter an index to access: "))
    print(f"Item at index {index}: {my_list[index]}")

except IndexError:
    print("Index out of range!")
except ValueError:
    print("Please enter a valid integer!")
```


---
**Score: 0**