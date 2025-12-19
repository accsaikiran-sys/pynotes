---
title: Ch07 8 Raising Your Own Exception
date: 2025-12-18
author: Your Name
cell_count: 2
score: 0
---

# ch07_8_raising_your_own_exception

Created: 20251121


```python
def check_age(age):
    if age < 18:
        raise Exception("Not eligible")
    print("Eligible!")


try:
    check_age(15)

except Exception as e:
    print(f"Error: {e}")
```


---
**Score: 0**