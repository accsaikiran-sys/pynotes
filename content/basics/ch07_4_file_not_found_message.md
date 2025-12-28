---
title: Ch07 4 File Not Found Message
date: 2025-12-26
author: Your Name
cell_count: 2
score: 0
---

# ch07_4_file_not_found_message

Created: 20251121


```python
try:
    with open("data.txt", "r") as file:
        content = file.read()
        print(content)

except FileNotFoundError:
    print("File not found.")
```


---
**Score: 0**