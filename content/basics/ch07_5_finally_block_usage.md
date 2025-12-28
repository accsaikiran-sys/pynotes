---
title: Ch07 5 Finally Block Usage
date: 2025-12-26
author: Your Name
cell_count: 2
score: 0
---

# ch07_5_finally_block_usage

Created: 20251121


```python
try:
    num1 = float(input("Enter first number: "))
    num2 = float(input("Enter second number: "))
    result = num1 / num2
    print(f"Result: {result}")

except ZeroDivisionError:
    print("Cannot divide by zero!")
except ValueError:
    print("Please enter valid numbers!")

finally:
    print("This block always runs")
```


---
**Score: 0**