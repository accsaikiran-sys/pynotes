---
title: Ch07 11 Input Util Correct
date: 2025-12-17
author: Your Name
cell_count: 2
score: 0
---

# ch07_11_input_util_correct

Created: 20251121


```python
while True:
    try:
        number = int(input("Enter a number: "))
        print(f"Success! You entered: {number}")
        break

    except ValueError:
        print("Invalid input! Please enter a valid integer.")
```


---
**Score: 0**