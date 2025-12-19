---
title: Ch07 15 Safe Calculator
date: 2025-12-18
author: Your Name
cell_count: 2
score: 0
---

# ch07_15_safe_calculator

Created:20251121


```python
try:
    num1 = int(input("Enter first number: "))
    operator = input("Enter operator (+, -, *, /): ")
    num2 = int(input("Enter second number: "))

    if operator == '+':
        result = num1 + num2
    elif operator == '-':
        result = num1 - num2
    elif operator == '*':
        result = num1 * num2
    elif operator == '/':
        result = num1 / num2
    else:
        raise ValueError("Unsupported operator")

    print("Result:", result)

except ZeroDivisionError:
    print("Error: Cannot divide by zero")
except ValueError as e:
    if str(e) == "Unsupported operator":
        print("Error: Unsupported operator")
    else:
        print("Error: Invalid number")
```


---
**Score: 0**