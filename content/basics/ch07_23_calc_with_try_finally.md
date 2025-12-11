---
title: Ch07 23 Calc With Try Finally
date: 2025-12-10
author: Your Name
cell_count: 2
score: 0
---

# ch07_23_calc_with_try_finally

Created:20251122


```python
try:
    num1 = int(input("Enter first number: "))
    num2 = int(input("Enter second number: "))
    result = num1 / num2
    print("Result:", result)
except ZeroDivisionError:
    print("Error: Cannot divide by zero")
finally:
    print("This will always execute")
```


---
**Score: 0**