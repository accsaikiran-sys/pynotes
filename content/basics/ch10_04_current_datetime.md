---
title: Ch10 04 Current Datetime
date: 2025-12-14
author: Your Name
cell_count: 31
score: 30
---

# How to get current date and time in Python?

Examples for retrieving and formatting current date/time values.

## 1. Using `datetime.now()` (Most Common Method)



```python
from datetime import datetime

current_datetime = datetime.now()
print(current_datetime)
```

Returns date and time including microseconds.

## 2. Get Only Current Date



```python
from datetime import date

today = date.today()
print(today)
```

Useful for applications requiring date-only tracking.

## 3. Get Only Current Time



```python
from datetime import datetime

current_time = datetime.now().time()
print(current_time)
```

Extracts only the time component.

## 4. Formatted Current Date and Time



```python
from datetime import datetime

now = datetime.now()
formatted = now.strftime("%Y-%m-%d %H:%M:%S")
print(formatted)
```

Ideal for logs, UI display, and reports.

## 5. Using `time` Module



```python
import time

current_timestamp = time.ctime()
print(current_timestamp)
```

Returns a human-readable timestamp string.

## 6. Using UNIX Timestamp



```python
import time

timestamp = time.time()
print(timestamp)
```

Returns seconds since Jan 1, 1970 (Epoch time).

## 7. Current UTC Date and Time



```python
from datetime import datetime

utc_now = datetime.utcnow()
print(utc_now)
```

Used in distributed systems and APIs.

## 8. Current Date and Time with Timezone



```python
from datetime import datetime
from zoneinfo import ZoneInfo

local_time = datetime.now(ZoneInfo("America/New_York"))
print(local_time)
```

Provides timezone-aware timestamps.

## 9. Human-Friendly Display



```python
from datetime import datetime

now = datetime.now()
print(now.strftime("Today is %A, %d %B %Y - %I:%M %p"))
```

Used for dashboards and user notifications.

## 10. Enterprise Logging Example



```python
from datetime import datetime

def log_event(event):
    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    print(f"[{timestamp}] {event}")

log_event("Server Started")
log_event("User Login Successful")
```

Standard pattern for system and audit logs.


---
**Score: 30**