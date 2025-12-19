---
title: Ch07 20 No Internet Exception
date: 2025-12-18
author: Your Name
cell_count: 2
score: 0
---

# ch07_20_no_internet_exception

Created:20251121


```python
def connect_to_internet():
    raise ConnectionError("No internet connection")

try:
    connect_to_internet()
except ConnectionError:
    print("Please check your network")
```


---
**Score: 0**