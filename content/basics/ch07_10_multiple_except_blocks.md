---
title: Ch07 10 Multiple Except Blocks
date: 2025-12-24
author: Your Name
cell_count: 2
score: 0
---

# ch07_10_multiple_except_blocks

Created: 20251121


```python
try:
    num1 = float(input("Enter first number: "))
    num2 = float(input("Enter second number: "))
    result = num1 / num2
    print(f"Result: {result}")

except ZeroDivisionError:
    print("Error: Cannot divide by zero! Please enter a non-zero divisor.")

except ValueError:
    print("Error: Invalid input! Please enter valid numbers only.")
```


---
**Score: 0**