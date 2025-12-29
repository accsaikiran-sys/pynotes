---
title: Ch02 Python Varibles Literals
date: 2025-12-27
author: Your Name
cell_count: 11
score: 10
---

```python
Created:20251128
https://csp.gitbook.io/python-learning/basics/ch02-python-fundamentals/python-variables-and-literals
```


```python
# Variable assignment
count = 10
price = 99.99
name = "Python"

print(count)   # Output: 10
print(price)   # Output: 99.99
print(name)    # Output: Python 
```

    10
    99.99
    Python



```python
a, b,c  = 1 ,2, 3
print(a)
print(b)
print(c)
```

    1
    2
    3



```python
value = 100
print(value)
value = "none"
print(value) #reassigned
```

    100
    none



```python
integer_literal = 42
float_literal = 3.14
complex_literal = 2 + 3j

print(integer_literal)  # Output: 42
print(float_literal)    # Output: 3.14
print(complex_literal)  # Output: (2+3j)
```

    42
    3.14
    (2+3j)



```python
single_quote = 'Hello'
double_quote = "World"
multi_line = """This is
a multi-line
string"""

print(single_quote)  
print(double_quote)  
print(multi_line)
```

    Hello
    World
    This is
    a multi-line
    string



```python
is_active = True
is_logged_in = False

print(is_active)     
print(is_logged_in)   
```

    True
    False



```python
result = None

if result is None:
    print("No value assigned yet")
```

    No value assigned yet



```python
binary = 0b1010
octal = 0o12
hexadecimal = 0xA

print(binary)      
print(octal)        
print(hexadecimal)  
```

    10
    10
    10



```python
x = 5
y = 3

sum_result = x + y
product_result = x * y

print(sum_result)      
print(product_result)  
```

    8
    15



```python

```


---
**Score: 10**