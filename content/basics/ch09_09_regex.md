---
title: Ch09 09 Regex
date: 2025-12-27
author: Your Name
cell_count: 21
score: 20
---

# Chapter 9.9: Python Regular Expressions (RegEx)

This notebook covers Regular Expressions - a powerful tool for searching, matching, and manipulating text patterns using the `re` module.

## 1. What is RegEx

Regular Expressions (RegEx) provide a powerful way to search, match, and manipulate text patterns.


```python
import re

text = "Python is powerful"
match = re.search("Python", text)
print(match.group())  # Python

# The re module enables pattern-based text processing
```

## 2. Using re.match()

match() checks for a pattern at the start of the string only.


```python
import re

text = "Python Programming"
result = re.match("Python", text)

print(result.group())  # Python
```

## 3. Using re.search()

search() scans the entire string for the first match.


```python
import re

text = "Learn Python Programming"
result = re.search("Python", text)

print(result.group())  # Python
```

## 4. Using re.findall()

Returns all matches as a list.


```python
import re

text = "The rain in Spain"
matches = re.findall("ai", text)
print(matches)  # ['ai', 'ai']
```

## 5. Using re.sub() (Replace Text)

Replaces matched patterns with new content.


```python
import re

text = "I love Java"
new_text = re.sub("Java", "Python", text)
print(new_text)  # I love Python
```

## 6. Using Character Classes

Common patterns:
[a-z] → lowercase letters
[A-Z] → uppercase letters
[0-9] → digits


```python
import re

text = "abc123"
result = re.findall("[a-z]", text)
print(result)  # ['a', 'b', 'c']
```

## 7. Metacharacters and Special Sequences

Common sequences:
\d → digit
\w → alphanumeric
\s → whitespace


```python
import re

text = "Email: test123@gmail.com"
pattern = r"\\w+@\\w+\\.\\w+"

match = re.search(pattern, text)
print(match.group())
```

## 8. Using Quantifiers

Quantifiers:
* → 0 or more
+ → 1 or more
? → 0 or 1
{n} → exact count


```python
import re

text = "Helloooo"
pattern = r"o+"

print(re.findall(pattern, text))  # ['oooo']
```

## 9. Grouping with Parentheses

Groups allow segmented extraction of patterns.


```python
import re

text = "John Doe"
pattern = r"(John) (Doe)"

match = re.search(pattern, text)
print(match.groups())  # ('John', 'Doe')
```

## 10. Real-World RegEx Example (Phone Validation)

Used for input validation and sanitization in production systems.


```python
import re

def validate_phone(phone):
    pattern = r"^\\+?\\d{10,13}$"
    return bool(re.match(pattern, phone))

print(validate_phone("+911234567890"))  # True
print(validate_phone("12345"))          # False

# Used for input validation and sanitization in production systems
```


---
**Score: 20**