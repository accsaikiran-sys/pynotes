---
title: Ch06 03 Read Csv Files
date: 2025-12-11
author: Your Name
cell_count: 11
score: 10
---

```python
# Created: 20251210
# https://csp.gitbook.io/python-learning/basics/ch06-python-files/reading-csv-files-in-python
```


```python
import csv

with open("data.csv", "r") as file:
    reader = csv.reader(file)
    for row in reader:
        print(row)
```


    ---------------------------------------------------------------------------

    FileNotFoundError                         Traceback (most recent call last)

    Cell In[1], line 3
          1 import csv
    ----> 3 with open("data.csv", "r") as file:
          4     reader = csv.reader(file)
          5     for row in reader:


    File ~/miniconda3/envs/py12/lib/python3.12/site-packages/IPython/core/interactiveshell.py:284, in _modified_open(file, *args, **kwargs)
        277 if file in {0, 1, 2}:
        278     raise ValueError(
        279         f"IPython won't let you open fd={file} by default "
        280         "as it is likely to crash IPython. If you know what you are doing, "
        281         "you can use builtins' open."
        282     )
    --> 284 return io_open(file, *args, **kwargs)


    FileNotFoundError: [Errno 2] No such file or directory: 'data.csv'



```python
import csv

with open("data.csv", "r") as file:
    reader = csv.reader(file)
    header = next(reader)
    print("Header:", header)

    for row in reader:
        print(row)
```


```python
import csv

with open("data.csv", "r") as file:
    reader = csv.DictReader(file)
    for row in reader:
        print(row)
```


```python
import csv

with open("data.csv", "r") as file:
    reader = csv.DictReader(file)
    for row in reader:
        print(row["name"], row["age"])
```


```python
import csv

with open("data_pipe.csv", "r") as file:
    reader = csv.reader(file, delimiter="|")
    for row in reader:
        print(row)
```


```python
import csv

with open("large_data.csv", "r") as file:
    reader = csv.reader(file)
    for row in reader:
        process = row  # Lazy iteration prevents memory overload
```


```python
import csv

with open("data.csv", "r") as file:
    reader = csv.DictReader(file)
    for row in reader:
        age = int(row["age"])
        salary = float(row["salary"])
        print(age, salary)
        
# CSV values are strings by default and often require type casting.
```


```python
import csv

try:
    with open("data.csv", "r") as file:
        reader = csv.reader(file)
        for row in reader:
            print(row)
except FileNotFoundError:
    print("CSV file not found.")

# Ensures robustness in production code.
```


```python
import csv

with open("data.csv", "r") as file:
    reader = csv.reader(file)
    data = list(reader)

print(data)

# Loads the entire CSV into memory (use cautiously for large files).
```


```python
import pandas as pd

df = pd.read_csv("data.csv")

print(df)
print(df["name"])


# Pandas offers a high-level interface for complex data analysis and transformations.


```


---
**Score: 10**