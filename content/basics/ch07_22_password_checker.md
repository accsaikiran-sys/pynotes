---
title: Ch07 22 Password Checker
date: 2025-12-16
author: Your Name
cell_count: 2
score: 0
---

# ch07_22_password_checker

Created:20251121


```python
try:
    password = input("Enter password: ")
    if len(password) < 6:
        raise ValueError("Password too short")
    else:
        print("Password is valid")
except ValueError as e:
    print(e)
```


---
**Score: 0**