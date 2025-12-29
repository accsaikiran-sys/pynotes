---
title: Ch07 6 Try Except Else
date: 2025-12-27
author: Your Name
cell_count: 2
score: 0
---

# ch07_6_try_except_else

Created: 20251121


```python
try:
    user_input = input("Enter a number: ")
    number = int(user_input)

except ValueError:
    print("Invalid input! Please enter a valid integer.")

else:
    print("Success!")
```


---
**Score: 0**