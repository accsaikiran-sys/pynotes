---
title: Ch06 02 Read Write Csv
date: 2025-12-20
author: Your Name
cell_count: 11
score: 10
---

```python
#Created: 20251210
# https://csp.gitbook.io/python-learning/basics/ch06-python-files/python-csv-read-and-write-csv-files
```


```python
"""
1. What is a CSV File

A CSV (Comma-Separated Values) file stores tabular data in plain text, where each line represents a row and values are separated by commas.

Example:


Copy
name,age,city
Alice,25,New York
Bob,30,London
"""
```


```python
import csv

# Reads each row as a list of values.

with open("data.csv", "r") as file:
    reader = csv.reader(file)
    for row in reader:
        print(row)
```


```python
import csv

# Useful when the first row contains column names.


with open("data.csv", "r") as file:
    reader = csv.reader(file)
    next(reader)  # Skip header
    for row in reader:
        print(row)
```


```python
import csv

#Each row is read as an ordered dictionary mapped to column headers.


with open("data.csv", "r") as file:
    reader = csv.DictReader(file)
    for row in reader:
        print(row["name"], row["age"])
```


```python
import csv
# Creates and writes rows to a CSV file.


with open("output.csv", "w", newline="") as file:
    writer = csv.writer(file)
    writer.writerow(["name", "age", "city"])
    writer.writerow(["Alice", 25, "New York"])
    writer.writerow(["Bob", 30, "London"])
```


```python
import csv
# Efficient for bulk data writing.


data = [
    ["John", 28, "Toronto"],
    ["Emma", 35, "Berlin"]
]

with open("people.csv", "w", newline="") as file:
    writer = csv.writer(file)
    writer.writerows(data)
```


```python
import csv
# Ensures structured column mapping.


fieldnames = ["name", "age", "city"]

with open("users.csv", "w", newline="") as file:
    writer = csv.DictWriter(file, fieldnames=fieldnames)
    writer.writeheader()
    
    writer.writerow({"name": "Alice", "age": 25, "city": "Paris"})
    writer.writerow({"name": "Bob", "age": 30, "city": "Rome"})
```


```python
import csv
# CSV supports configurable delimiters for complex data formats.


with open("custom.csv", "w", newline="") as file:
    writer = csv.writer(file, delimiter="|")
    writer.writerow(["Name", "Age", "Country"])
    writer.writerow(["Alice", 25, "India"])
```


```python
import csv

# "a" mode appends data without overwriting existing rows.


with open("users.csv", "a", newline="") as file:
    writer = csv.writer(file)
    writer.writerow(["Charlie", 40, "USA"])
```


```python
import pandas as pd

# Pandas provides high-level, efficient CSV data manipulation for analytics and ML workflows.


df = pd.read_csv("data.csv")
print(df.head())
```


---
**Score: 10**