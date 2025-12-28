---
title: Ch07 1 Divide Two Numbers Safely
date: 2025-12-26
author: Your Name
cell_count: 2
score: 0
---

# ch07_1_divide_two_numbers_safely

Created: 20251121


```python
try:
    num1 = float(input("enter first number: "))
    num2 = float(input("enter second number: "))

    print("Result: ", num1 / num2)

except ZeroDivisionError:
    print("Cannot divide by zero!")
```


---
**Score: 0**