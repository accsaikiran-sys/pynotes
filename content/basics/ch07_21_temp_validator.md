---
title: Ch07 21 Temp Validator
date: 2026-01-07
author: Your Name
cell_count: 2
score: 0
---

# ch07_21_temp_validator

Created:20251121


```python
try:
    user_input = int(input("Enter temperature: "))
    if user_input < -273:
        raise ValueError("Temperature below absolute zero")
except ValueError as e:
    print("Invalid temperature value")
```


---
**Score: 0**