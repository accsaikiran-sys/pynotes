---
title: Ch07 24 Simple Age Group Checker
date: 2025-12-18
author: Your Name
cell_count: 2
score: 0
---

# Ch07 24 Simple Age Group Checker


```python
try:
    age = int(input ("Enter age: "))
    if age <13:
        print ("Child")
    elif age <18:
        print ("Teenager")
    else:
        print ("Adult")
except ValueError :
    print ("Invalid age")
```


---
**Score: 0**