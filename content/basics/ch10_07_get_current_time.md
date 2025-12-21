---
title: Ch10 07 Get Current Time
date: 2025-12-20
author: Your Name
cell_count: 31
score: 30
---

# Python Get Current Time

Examples to retrieve and format the current time in Python.

## 1. Using `datetime.now().time()` (Standard Method)



```python
from datetime import datetime

current_time = datetime.now().time()
print(current_time)
```

Includes hours, minutes, seconds, and microseconds.

## 2. Using `strftime()` for Formatted Time



```python
from datetime import datetime

now = datetime.now()
formatted_time = now.strftime("%H:%M:%S")
print(formatted_time)
```

Ideal for logs and UI display.

## 3. 12-Hour Format with AM/PM



```python
from datetime import datetime

time_12_hour = datetime.now().strftime("%I:%M %p")
print(time_12_hour)
```

Common in user-facing applications.

## 4. Using the `time` Module (System Clock)



```python
import time

current_time = time.strftime("%H:%M:%S")
print(current_time)
```

Reads the system clock directly.

## 5. Get Only Hour, Minute, Second



```python
from datetime import datetime

now = datetime.now()

print("Hour:", now.hour)
print("Minute:", now.minute)
print("Second:", now.second)
```

Useful for conditional logic and scheduling.

## 6. Get Current UTC Time



```python
from datetime import datetime

utc_time = datetime.utcnow().time()
print(utc_time)
```

Recommended for distributed and API-based systems.

## 7. Timezone-Aware Current Time



```python
from datetime import datetime
from zoneinfo import ZoneInfo

tokyo_time = datetime.now(ZoneInfo("Asia/Tokyo")).time()
print(tokyo_time)
```

Ensures accurate time across regions.

## 8. Current Time with Microseconds



```python
from datetime import datetime

now = datetime.now()
print(now.strftime("%H:%M:%S.%f"))
```

Used in high-precision logging.

## 9. UNIX Time (Epoch Seconds)



```python
import time

epoch_time = time.time()
print(epoch_time)
```

Represents time in seconds since Jan 1, 1970.

## 10. Enterprise Logging Example (Time-Only Logger)



```python
from datetime import datetime

def log_event(event):
    current_time = datetime.now().strftime("%H:%M:%S")
    print(f"[{current_time}] {event}")

log_event("Service initialized")
log_event("Task executed")
```

Standard pattern for time-stamped events.


---
**Score: 30**