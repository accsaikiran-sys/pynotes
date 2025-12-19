---
title: Ch07 19 Integer Only List
date: 2025-12-18
author: Your Name
cell_count: 2
score: 0
---

# ch07_19_integer_only_list

Created:20251121


```python
values = [5, "hello", 7, "world", 3]
for value in values:
    try:
        result = int(value)
        print(result)
    except ValueError:
        print("Skipping non-number")
```


---
**Score: 0**