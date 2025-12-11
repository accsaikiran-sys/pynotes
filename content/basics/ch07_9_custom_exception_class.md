---
title: Ch07 9 Custom Exception Class
date: 2025-12-10
author: Your Name
cell_count: 2
score: 0
---

# ch07_9_custom_exception_classCreated: 20251121


```python
class InvalidNumber(Exception):    passdef validate_number(num):    if num < 0:        raise InvalidNumber("Number cannot be negative!")    print(f"Valid number: {num}")try:    validate_number(-5)except InvalidNumber as e:    print(f"Error: {e}")
```


---
**Score: 0**