---
title: Ch07 12 Assert Positive Number
date: 2025-12-10
author: Your Name
cell_count: 2
score: 0
---

# ch07_12_assert_positive_number

Created: 20251121


```python
try: 
    num = int(input("Enter number: "))
    assert num >= 0, "Number should be positive"
except AssertionError as e:
    print(e)
```


---
**Score: 0**