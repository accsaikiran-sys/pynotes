---
title: Ch02 Explicit-Call
date: 2025-12-24
author: Your Name
cell_count: 2
score: 0
---

```python


import simple_print

# simple_print.print_numbers(50)


# obj = simple_print.NumberPrinter(7)
# print(obj)
# obj.print_numbers()
# obj.print_numbers_double()

# Explicitly trigger the destructor
# del obj

obj2 = simple_print.NumberPrinter
print(obj2)
obj2.print_numbers()
```


    ---------------------------------------------------------------------------

    ModuleNotFoundError                       Traceback (most recent call last)

    Cell In[1], line 1
    ----> 1 import simple_print
          3 # simple_print.print_numbers(50)
          4 
          5 
       (...)
         11 # Explicitly trigger the destructor
         12 # del obj
         14 obj2 = simple_print.NumberPrinter


    ModuleNotFoundError: No module named 'simple_print'



```python

```


---
**Score: 0**