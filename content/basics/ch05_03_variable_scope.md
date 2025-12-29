---
title: Ch05 03 Variable Scope
date: 2025-12-27
author: Your Name
cell_count: 12
score: 10
---

```python
#Created: 20251210
# https://csp.gitbook.io/python-learning/basics/ch05-python-functions/python-variable-scope
```


```python
def show_value():
    x = 10  # Local variable
    print(x)

show_value()
# print(x)  # NameError: x is not defined
```

    10



```python
x = 20  # Global variable

def display():
    print(x)

display()
print(x)
```

    20
    20



```python
value = 50

def update():
    value = 10  # Local variable shadows global
    print("Inside function:", value)

update()
print("Outside function:", value)
```

    Inside function: 10
    Outside function: 50



```python
count = 0

def increment():
    global count
    count += 1

increment()
print(count)  # Output: 1
```

    1



```python
def outer():
    message = "Hello"

    def inner():
        print(message)  # Accessing enclosing variable

    inner()

outer()
```

    Hello



```python
def outer():
    count = 0

    def inner():
        nonlocal count
        count += 1
        print(count)

    inner()
    inner()

outer()
```

    1
    2



```python
x = "Global"

def outer():
    x = "Enclosing"

    def inner():
        x = "Local"
        print(x)

    inner()

outer()
```

    Local



```python
print(len([1, 2, 3]))  # Built-in function
```

    3



```python
for i in range(3):
    loop_var = i

print(loop_var)  # Accessible outside loop
```

    2



```python
total = 100

def calculate():
    total = 50

    def adjust():
        nonlocal total
        total += 10

    adjust()
    return total

print(calculate())  # Output: 60
print(total)        # Output: 100
```

    60
    100



```python

```


---
**Score: 10**