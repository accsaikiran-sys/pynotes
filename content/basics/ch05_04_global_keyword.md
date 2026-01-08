---
title: Ch05 04 Global Keyword
date: 2026-01-07
author: Your Name
cell_count: 12
score: 10
---

```python
#Created : 20251210
# https://csp.gitbook.io/python-learning/basics/ch05-python-functions/python-global-keyword
```


```python
count = 10

def display():
    print(count)

display()  # Output: 10
```

    10



```python
value = 5

def update():
    value = value + 1  # UnboundLocalError
```


```python
counter = 0

def increment():
    global counter
    counter += 1

increment()
print(counter)  # Output: 1
```

    1



```python
status = "inactive"

def activate():
    global status
    status = "active"

def show_status():
    print(status)

activate()
show_status()  # Output: active
```

    active



```python
x = 100

def outer():
    def inner():
        global x
        x = 200

    inner()

outer()
print(x)  # Output: 200
```

    200



```python
x = 50

def outer():
    x = 10
    
    def inner():
        global x
        x = 99

    inner()
    print("Outer x:", x)

outer()
print("Global x:", x)
```

    Outer x: 10
    Global x: 99



```python
requests = 0

def handle_request():
    global requests
    requests += 1

handle_request()
handle_request()
print(requests)  # Output: 2
```

    2



```python
mode = "light"

def toggle_mode():
    global mode
    if mode == "light":
        mode = "dark"
    else:
        mode = "light"

toggle_mode()
print(mode)  # Output: dark
```

    dark



```python
config = {"theme": "dark"}

def update_config(new_theme):
    config["theme"] = new_theme  # No global keyword needed
```


```python
class Counter:
    def __init__(self):
        self.value = 0

    def increment(self):
        self.value += 1

counter = Counter()
counter.increment()
print(counter.value)  # Output: 1
```

    1



```python

```


---
**Score: 10**