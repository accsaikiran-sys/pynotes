---
title: Ch10 02 Strftime
date: 2025-12-10
author: Your Name
cell_count: 31
score: 30
---

# Python `strftime()`

`strftime()` converts a datetime object into a formatted string based on specified format codes.

## 1. What is `strftime()`



```python
from datetime import datetime

now = datetime.now()
formatted = now.strftime("%Y-%m-%d")
print(formatted)  # e.g., 2025-11-24
```

It is essential for displaying dates in human-readable formats, logs, and reports.

## 2. Basic Date Formatting



```python
from datetime import datetime

now = datetime.now()

print(now.strftime("%d/%m/%Y"))  # Day/Month/Year
print(now.strftime("%m-%d-%Y"))  # Month-Day-Year
```

Customizes how date appears in different regional formats.

## 3. Time Formatting



```python
from datetime import datetime

now = datetime.now()

print(now.strftime("%H:%M:%S"))  # 24-hour format
print(now.strftime("%I:%M %p"))  # 12-hour format with AM/PM
```

Used for clock displays and timestamping.

## 4. Including Day and Month Names



```python
from datetime import datetime

now = datetime.now()

print(now.strftime("%A"))  # Full weekday name
print(now.strftime("%a"))  # Short weekday name
print(now.strftime("%B"))  # Full month name
print(now.strftime("%b"))  # Short month name
```

Enhances readability in user-facing outputs.

## 5. Combining Date and Time



```python
from datetime import datetime

now = datetime.now()

print(now.strftime("%Y-%m-%d %H:%M:%S"))
```

Common format for logs and system monitoring.

## 6. Using `strftime()` for File Naming



```python
from datetime import datetime

filename = "backup_" + datetime.now().strftime("%Y%m%d_%H%M%S") + ".zip"
print(filename)
```

Ideal for generating timestamped files safely.

## 7. ISO 8601 Format Using `strftime`



```python
from datetime import datetime

now = datetime.now()
iso_format = now.strftime("%Y-%m-%dT%H:%M:%S")
print(iso_format)
```

Used in APIs and structured data exchange.

## 8. Custom Human-Readable Format



```python
from datetime import datetime

now = datetime.now()

print(now.strftime("Today is %A, %d %B %Y at %I:%M %p"))
```

Creates expressive, user-friendly messages.

## 9. Formatting Specific `datetime` Object



```python
from datetime import datetime

custom_date = datetime(2025, 12, 25, 18, 30)

print(custom_date.strftime("%A, %d %B %Y - %H:%M"))
```

Formats fixed or scheduled execution dates.

## 10. Enterprise Use Case: Log Timestamp



```python
from datetime import datetime

def log_message(message):
    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    print(f"[{timestamp}] {message}")

log_message("Server started")
log_message("User authenticated")
```

Standard pattern for production logging and auditing systems.


---
**Score: 30**