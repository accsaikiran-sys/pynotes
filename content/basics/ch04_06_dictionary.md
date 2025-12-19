---
title: Ch04 06 Dictionary
date: 2025-12-18
author: Your Name
cell_count: 13
score: 10
---

```python
#Created: 20251210
# https://csp.gitbook.io/python-learning/basics/ch04-python-data-types/python-dictionary
```


```python
empty_dict = {}
student = {"name": "Alice", "age": 22, "grade": "A"}

print(empty_dict)
print(student)
```

    {}
    {'name': 'Alice', 'age': 22, 'grade': 'A'}



```python
employee = {"id": 101, "name": "John", "role": "Developer"}

print(employee["name"])        # Output: John
print(employee.get("role"))    # Output: Developer
```

    John
    Developer



```python
profile = {"username": "admin"}

profile["email"] = "admin@example.com"
profile["username"] = "administrator"

print(profile)
```

    {'username': 'administrator', 'email': 'admin@example.com'}



```python
data = {"a": 1, "b": 2, "c": 3}

removed_value = data.pop("b")
del data["a"]

print(data)         # {'c': 3}
print(removed_value)  # 2
```

    {'c': 3}
    2



```python
settings = {"theme": "dark", "version": 1.0}

print(len(settings))        # Output: 2
print("theme" in settings)  # True
```

    2
    True



```python
user = {"name": "Alice", "age": 30, "city": "London"}

for key in user:
    print(key, ":", user[key])

for key, value in user.items():
    print(key, "=>", value)
```

    name : Alice
    age : 30
    city : London
    name => Alice
    age => 30
    city => London



```python
data = {"x": 10, "y": 20}

print(data.keys())     # dict_keys(['x', 'y'])
print(data.values())   # dict_values([10, 20])
print(data.items())    # dict_items([('x', 10), ('y', 20)])
```

    dict_keys(['x', 'y'])
    dict_values([10, 20])
    dict_items([('x', 10), ('y', 20)])



```python
dict1 = {"a": 1, "b": 2}
dict2 = {"c": 3, "d": 4}

merged = dict1 | dict2
print(merged)
```

    {'a': 1, 'b': 2, 'c': 3, 'd': 4}



```python
employee = {
    "id": 101,
    "personal": {
        "name": "John",
        "email": "john@example.com"
    }
}

print(employee["personal"]["name"])  # Output: John
```

    John



```python
squares = {x: x**2 for x in range(5)}
print(squares)  # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

    {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}



```python

```


```python

```


---
**Score: 10**