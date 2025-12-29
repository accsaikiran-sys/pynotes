---
title: Ch04 04 Strings
date: 2025-12-27
author: Your Name
cell_count: 12
score: 10
---

```python
#Created: 20251210
# https://csp.gitbook.io/python-learning/basics/ch04-python-data-types/python-string
```


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
text = "Python"

print(text[0])    # P
print(text[-1])   # n
```

    P
    n



```python
word = "Programming"

print(word[0:6])   # Output: Progra
print(word[:4])    # Output: Prog
print(word[4:])    # Output: ramming
```

    Progra
    Prog
    ramming



```python
name = "Python"

# name[0] = "J"  # Raises TypeError
print(name)
```

    Python



```python
first = "Hello"
second = "World"

print(first + " " + second)  # Hello World
print(first * 3)             # HelloHelloHello
```

    Hello World
    HelloHelloHello



```python
message = "Data Science"

print(len(message))         # Output: 12
print("Data" in message)    # True
print("AI" not in message)  # True
```

    12
    True
    True



```python
text = "  python programming  "

print(text.upper())     # PYTHON PROGRAMMING
print(text.lower())     # python programming
print(text.strip())     # python programming
print(text.replace("python", "Java"))  # Java programming
```

      PYTHON PROGRAMMING  
      python programming  
    python programming
      Java programming  



```python
sentence = "Python is powerful"

words = sentence.split(" ")
print(words)  # ['Python', 'is', 'powerful']

joined = "-".join(words)
print(joined)  # Python-is-powerful
```

    ['Python', 'is', 'powerful']
    Python-is-powerful



```python
sentence = "Python is powerful"

words = sentence.split(" ")
print(words)  # ['Python', 'is', 'powerful']

joined = "-".join(words)
print(joined)  # Python-is-powerful
```

    ['Python', 'is', 'powerful']
    Python-is-powerful



```python
word = "Code"

for char in word:
    print(char)
```

    C
    o
    d
    e



```python

```


---
**Score: 10**