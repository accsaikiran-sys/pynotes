---
title: Ch07 18 Safe File Reading
date: 2025-12-14
author: Your Name
cell_count: 2
score: 0
---

# ch07_18_safe_file_reading

Created:20251121


```python
try:
    user_input = input("Enter file name: ")
    file = open(user_input, "r")
    content = file.read()
    print(content)
except FileNotFoundError:
    print("Unable to read file .")
```


---
**Score: 0**