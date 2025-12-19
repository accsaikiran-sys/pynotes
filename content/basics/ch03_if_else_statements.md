---
title: Ch03 If Else Statements
date: 2025-12-18
author: Your Name
cell_count: 12
score: 10
---

```python
Created:20251128
https://csp.gitbook.io/python-learning/basics/ch03-python-flow-control/python-if...else-statement
```


```python
age = 20

if age >= 18:
    print("Eligible to vote")
    
```

    Eligible to vote



```python
temperature = 15

if temperature > 25:
    print("It's warm outside")
else:
    print("It's cold outside")
```

    It's cold outside



```python
score = 85

if score >= 90:
    print("Grade: A")
elif score >= 75:
    print("Grade: B")
elif score >= 60:
    print("Grade: C")
else:
    print("Grade: D")
```

    Grade: B



```python
username = "admin"
password = "1234"

if username == "admin":
    if password == "1234":
        print("Access granted")
    else:
        print("Incorrect password")
```

    Access granted



```python
age = 25
is_verified = True

if age > 18 and is_verified:
    print("User can proceed")
```

    User can proceed



```python
x = 10

if x > 5: print("x is greater than 5")
```

    x is greater than 5



```python
num = 7

result = "Even" if num % 2 == 0 else "Odd"
print(result)  # Output: Odd
```

    Odd



```python
day = "Sunday"

if day in ["Saturday", "Sunday"]:
    print("Weekend")
else:
    print("Weekday")
```

    Weekend



```python
username = "Alice"

if username.lower() == "alice":
    print("Welcome Alice")
```

    Welcome Alice



```python
value = 5

if value > 0:
    pass  # Placeholder for future logic

print("Program continues...")
```

    Program continues...



```python

```


---
**Score: 10**