---
title: Ch10 01 Date Time
date: 2025-12-18
author: Your Name
cell_count: 31
score: 30
---

# Chapter 10.1: Python datetime

The `datetime` module is used for handling date and time operations with high precision and reliability.

## 1. Overview of the datetime Module



```python
import datetime

print(datetime.datetime.now())
```

It supports full timestamping, scheduling, comparisons, and formatting.

## 2. Current Date and Time



```python
from datetime import datetime

now = datetime.now()
print(now)
```

Returns the current system date and time including microseconds.

## 3. Extracting Date Components



```python
from datetime import datetime

now = datetime.now()

print(now.year)
print(now.month)
print(now.day)
print(now.hour)
print(now.minute)
print(now.second)
```

Allows granular access to individual components.

## 4. Using `date` and `time` Objects



```python
from datetime import date, time

d = date(2025, 6, 15)
t = time(14, 30, 45)

print(d)
print(t)
```

Separates pure date and pure time values.

## 5. Formatting with `strftime()`



```python
from datetime import datetime

now = datetime.now()
print(now.strftime("%d-%m-%Y"))
print(now.strftime("%A, %B %d %Y"))
```

Frequently used format directives:
- `%d` → Day
- `%B` → Full month name
- `%A` → Weekday name

## 6. Parsing Strings with `strptime()`



```python
from datetime import datetime

date_string = "15-06-2025"
dt = datetime.strptime(date_string, "%d-%m-%Y")
print(dt)
```

Transforms formatted strings into datetime objects.

## 7. Time Difference using `timedelta`



```python
from datetime import datetime, timedelta

start = datetime.now()
end = start + timedelta(hours=5, minutes=30)

print("Start:", start)
print("End:", end)
```

Controls duration logic precisely.

## 8. Timezone Handling with `zoneinfo`



```python
from datetime import datetime
from zoneinfo import ZoneInfo

ny_time = datetime.now(ZoneInfo("America/New_York"))
tokyo_time = datetime.now(ZoneInfo("Asia/Tokyo"))

print("New York:", ny_time)
print("Tokyo:", tokyo_time)
```

Critical for international systems and APIs.

## 9. ISO Format Conversion



```python
from datetime import datetime

dt = datetime.now()
print(dt.isoformat())
```

Produces standardized time format (ISO 8601) for interoperability.

## 10. Practical Example: Scheduling Logic



```python
from datetime import datetime, timedelta

meeting_time = datetime.now() + timedelta(days=2)

if datetime.now() < meeting_time:
    print("Meeting scheduled")
else:
    print("Meeting overdue")
```

Used in reminders, CRON systems, task automation, and expiry tracking.


---
**Score: 30**