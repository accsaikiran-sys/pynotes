---
title: Ch06 04 Write Cav Files
date: 2025-12-10
author: Your Name
cell_count: 8
score: 5
---

```python
# Created: 20251210
# https://csp.gitbook.io/python-learning/basics/ch06-python-files/writing-csv-files-in-python
```


```python
import csv

with open("output.csv", "w", newline="") as file:
    writer = csv.writer(file)
    writer.writerow(["name", "age", "city"])
    writer.writerow(["Alice", 25, "New York"])
```


```python
import csv

data = [
    ["Bob", 30, "London"],
    ["Emma", 28, "Berlin"],
]

with open("people.csv", "w", newline="") as file:
    writer = csv.writer(file)
    writer.writerows(data)
```


```python
import csv

with open("data_pipe.csv", "w", newline="") as file:
    writer = csv.writer(file, delimiter="|")
    writer.writerow(["Name", "Age", "Country"])
    writer.writerow(["John", 35, "India"])
```


```python
import csv

with open("quotes.csv", "w", newline="") as file:
    writer = csv.writer(file, quoting=csv.QUOTE_ALL)
    writer.writerow(["Alice", "Software Engineer", "New York"])
```


```python
import csv

with open("users.csv", "a", newline="") as file:
    writer = csv.writer(file)
    writer.writerow(["Charlie", 40, "Canada"])
```


```python
import csv

fieldnames = ["name", "age", "city"]

with open("users.csv", "w", newline="") as file:
    writer = csv.DictWriter(file, fieldnames=fieldnames)
    writer.writeheader()
    writer.writerow({"name": "Alice", "age": 25, "city": "Paris"})
```


```python
import csv

def validate_row(row):
    return all(row)

data = [
    ["John", 28, "Toronto"],
    ["", 35, "Berlin"]
]

with open("validated.csv", "w", newline="") as file:
    writer = csv.writer(file)
    for row in data:
        if validate_row(row):
            writer.writerow(row)
```


---
**Score: 5**