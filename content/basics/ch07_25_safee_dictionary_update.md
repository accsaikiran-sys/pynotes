---
title: Ch07 25 Safee Dictionary Update
date: 2025-12-10
author: Your Name
cell_count: 2
score: 0
---

# ch07_25_safee_dictionary_update

Created:20251122


```python
data = {"name": "Jerin", "age": 22}

try:
    key = input("Enter key to update: ")
    # Accessing the key to trigger KeyError if it doesn't exist
    _ = data[key]
    
    # If key exists, update it (using 25 as per previous context)
    key_data = input("Enter value to update: ")
    data[key] = key_data
    print("Updated dictionary:", data)
except KeyError:
    print("Key does not exist.")
```


---
**Score: 0**