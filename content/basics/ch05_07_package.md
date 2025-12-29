---
title: Ch05 07 Package
date: 2025-12-27
author: Your Name
cell_count: 9
score: 5
---

```python
# Created:20251210
# https://csp.gitbook.io/python-learning/basics/ch05-python-functions/python-package
```


```python
# my_package/module1.py
def greet():
    return "Hello from module1"

    # main.py
import my_package.module1

print(my_package.module1.greet())
```


    ---------------------------------------------------------------------------

    ModuleNotFoundError                       Traceback (most recent call last)

    Cell In[4], line 6
          3     return "Hello from module1"
          5     # main.py
    ----> 6 import my_package.module1
          8 print(my_package.module1.greet())


    ModuleNotFoundError: No module named 'my_package'



```python
# main.py
import my_package.module1

print(my_package.module1.greet())
```


    ---------------------------------------------------------------------------

    ModuleNotFoundError                       Traceback (most recent call last)

    Cell In[3], line 2
          1 # main.py
    ----> 2 import my_package.module1
          4 print(my_package.module1.greet())


    ModuleNotFoundError: No module named 'my_package'



```python
# my_package/__init__.py
from .module1 import greet


from my_package import greet

print(greet())
```


```python
from my_package.analytics.stats import calculate_mean
```


```python
# analytics/stats.py
from .utils import format_number
```


```python
from my_package.analytics.stats import calculate_mean
```


```python
# pip install requests

import requests

response = requests.get("https://api.example.com")
print(response.status_code)
```


```python
# setup.py
from setuptools import setup, find_packages

setup(
    name="mypackage",
    version="1.0",
    packages=find_packages()
)
```


---
**Score: 5**