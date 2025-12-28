---
title: Ch07 14 Simple Exception Chaining
date: 2025-12-26
author: Your Name
cell_count: 2
score: 0
---

# ch07_14_simple_exception_chaining

Created:20251121


```python
try:
    # Try converting a string to int
    result = int("abc")
except ValueError as original_exception:
    # If it fails, raise a new Exception with a custom message from the original exception
    raise Exception("Custom error message") from original_exception
```


---
**Score: 0**