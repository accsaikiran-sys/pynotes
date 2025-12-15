---
title: Ch07 13 Exception In A Function
date: 2025-12-14
author: Your Name
cell_count: 2
score: 0
---

# ch07_13_exception_in_a_function

Created: 20251121


```python
def get_item(lst, index):
    try:
        return lst[index]
    except (IndexError, TypeError):
        return "Error occurred"
```


---
**Score: 0**