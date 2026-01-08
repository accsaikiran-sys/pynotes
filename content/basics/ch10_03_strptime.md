---
title: Ch10 03 Strptime
date: 2026-01-07
author: Your Name
cell_count: 31
score: 30
---

# Python `strptime()`

`strptime()` converts a date/time string into a datetime object using a specified format pattern.

## 1. What is `strptime()`



```python
from datetime import datetime

date_string = "2025-11-24"
dt = datetime.strptime(date_string, "%Y-%m-%d")
print(dt)
```

It enables reliable parsing of user input, file data, and API responses.

## 2. Parsing Basic Date Format



```python
from datetime import datetime

date_string = "24/11/2025"
parsed = datetime.strptime(date_string, "%d/%m/%Y")
print(parsed)
```

Ensures correct interpretation of regional date formats.

## 3. Parsing Date and Time Together



```python
from datetime import datetime

datetime_string = "2025-11-24 18:45:30"
dt = datetime.strptime(datetime_string, "%Y-%m-%d %H:%M:%S")
print(dt)
```

Supports full timestamp reconstruction.

## 4. Parsing with Month and Day Names



```python
from datetime import datetime

date_string = "Monday, November 24 2025"
dt = datetime.strptime(date_string, "%A, %B %d %Y")
print(dt)
```

Handles human-readable date representations.

## 5. Parsing 12-Hour Clock Format



```python
from datetime import datetime

time_string = "07:30 PM"
dt = datetime.strptime(time_string, "%I:%M %p")
print(dt.time())
```

Supports AM/PM based time parsing.

## 6. Using `strptime()` for File Data Processing



```python
from datetime import datetime

log_entry = "2025-11-24 10:15:00 - Server Started"
timestamp = log_entry.split(" - ")[0]

dt = datetime.strptime(timestamp, "%Y-%m-%d %H:%M:%S")
print(dt)
```

Common pattern for log parsing in backend systems.

## 7. Handling Incorrect Format Errors



```python
from datetime import datetime

try:
    dt = datetime.strptime("24-11-2025", "%Y-%m-%d")
except ValueError as e:
    print("Parsing failed:", e)
```

Raises ValueError when format does not match.

## 8. Converting User Input Safely



```python
from datetime import datetime

user_input = "15-06-2025"

try:
    parsed_date = datetime.strptime(user_input, "%d-%m-%Y")
    print("Valid date:", parsed_date)
except ValueError:
    print("Invalid date format")
```

Ensures safe user input validation.

## 9. Combining `strptime()` and `strftime()`



```python
from datetime import datetime

raw = "2025/11/24"
dt = datetime.strptime(raw, "%Y/%m/%d")
formatted = dt.strftime("%d-%m-%Y")

print(formatted)  # 24-11-2025
```

Transforms one date format into another.

## 10. Enterprise Use Case: API Timestamp Parsing



```python
from datetime import datetime

api_timestamp = "2025-11-24T14:35:59"
dt = datetime.strptime(api_timestamp, "%Y-%m-%dT%H:%M:%S")

print("Parsed API Timestamp:", dt)
```

Critical for normalizing and processing structured time data.


---
**Score: 30**