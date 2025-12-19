---
title: Python Type Conversion
date: 2025-12-18
author: Your Name
cell_count: 16
score: 15
---

```python
Created:20251128
https://csp.gitbook.io/python-learning/basics/ch02-python-fundamentals/python-type-conversion
```


```python
interger_value  = 10
float_value = 3.33

result = interger_value + float_value

print(result)
print(type(result))

```

    13.33
    <class 'float'>



```python
float_value = 9.99
string_value = "33"

iff = int(float_value)
ifs = int(string_value)

print(iff)
print(ifs)
```

    9
    33



```python
int_value = 7
string_value = "3.14"

float_from_int = float(int_value)
float_from_string = float(string_value)

print(float_from_int)      # Output: 7.0
print(float_from_string)   # Output: 3.14
```

    7.0
    3.14



```python
int_value = 100
float_value = 25.5
bool_value = True

str_int = str(int_value)
str_float = str(float_value)
str_bool = str(bool_value)

print(str_int)    # Output: '100'
print(str_float)  # Output: '25.5'
print(str_bool)   # Output: 'True'
```

    100
    25.5
    True



```python
print(bool(0))        # Output: False
print(bool(1))        # Output: True
print(bool(""))       # Output: False
print(bool("text"))   # Output: True
print(bool([]))       # Output: False
print(bool([1, 2]))   # Output: True
```

    False
    True
    False
    True
    False
    True



```python
text = "python"
char_list = list(text)
print(char_list)

text2 = ''.join(char_list)
print(text2)
```

    ['p', 'y', 't', 'h', 'o', 'n']
    python



```python
n_list = [1,2,3,4]
n_tuple = tuple(n_list)
print(n_tuple)
n_set = set(n_list)
print(n_set)
```

    (1, 2, 3, 4)
    {1, 2, 3, 4}



```python
pairs_list = [("a", 1), ("b", 2)]
pairs_tuple = (("x", 10), ("y", 20))

dict_from_list = dict(pairs_list)
dict_from_tuple = dict(pairs_tuple)

print(dict_from_list)   # Output: {'a': 1, 'b': 2}
print(dict_from_tuple)  # Output: {'x': 10, 'y': 20}
```

    {'a': 1, 'b': 2}
    {'x': 10, 'y': 20}



```python
def safe_int_convert(value: str) -> int:
    try:
        return int(value)
    except ValueError:
        print(f"Cannot convert '{value}' to int. Defaulting to 0.")
        return 0

print(safe_int_convert("123"))   # Output: 123
print(safe_int_convert("abc"))   # Output: Cannot convert 'abc' to int. Defaulting to 0.
                                 #         0
```

    123
    Cannot convert 'abc' to int. Defaulting to 0.
    0



```python
class Score:
    def __init__(self, points: int):
        self.points = points

    def __str__(self) -> str:
        return f"Score: {self.points}"

    def __int__(self) -> int:
        return self.points

player_score = Score(95)

print(str(player_score))  # Output: Score: 95
print(int(player_score))  # Output: 95
```

    Score: 95
    95



```python

```


```python

```


```python

```


```python

```


```python

```


---
**Score: 15**