---
title: Ch10 05 Timestamp Conversion
date: 2025-12-11
author: Your Name
cell_count: 31
score: 30
---

# Python timestamp to datetime and vice-versa

Working with Unix timestamps (seconds since January 1, 1970) and converting to/from Python `datetime`.

## 1. What is a Timestamp



```python
import time

timestamp = time.time()
print(timestamp)  # e.g. 1732452305.4829
```

A timestamp represents time as the number of seconds since January 1, 1970 (Unix Epoch).

## 2. Convert Timestamp → datetime (Local Time)



```python
from datetime import datetime

timestamp = 1732452305
dt = datetime.fromtimestamp(timestamp)

print(dt)
```

Returns a readable local datetime object.

## 3. Convert Timestamp → UTC datetime



```python
from datetime import datetime

timestamp = 1732452305
utc_dt = datetime.utcfromtimestamp(timestamp)

print(utc_dt)
```

Ensures consistency across global systems.

## 4. Convert datetime → Timestamp



```python
from datetime import datetime

dt = datetime.now()
timestamp = dt.timestamp()

print(timestamp)
```

Transforms a datetime object into Unix epoch seconds.

## 5. Timestamp Conversion with Formatting



```python
from datetime import datetime

timestamp = 1732452305
dt = datetime.fromtimestamp(timestamp)

print(dt.strftime("%Y-%m-%d %H:%M:%S"))
```

Useful for human-readable logs and reports.

## 6. Using `time` Module for Conversion



```python
import time

timestamp = 1732452305
readable = time.ctime(timestamp)

print(readable)
```

Generates formatted string without datetime objects.

## 7. Convert UTC Timestamp to Local Timezone



```python
from datetime import datetime
from zoneinfo import ZoneInfo

timestamp = 1732452305

utc = datetime.fromtimestamp(timestamp, ZoneInfo("UTC"))
local = utc.astimezone(ZoneInfo("Asia/Kolkata"))

print("UTC:", utc)
print("Local:", local)
```

Critical for timezone-aware applications.

## 8. Convert datetime String → Timestamp



```python
from datetime import datetime

date_string = "2025-11-24 14:30:00"
dt = datetime.strptime(date_string, "%Y-%m-%d %H:%M:%S")
timestamp = dt.timestamp()

print(timestamp)
```

Common in API and log file processing.

## 9. Millisecond Timestamp Handling



```python
from datetime import datetime

ms_timestamp = 1732452305482  # milliseconds
dt = datetime.fromtimestamp(ms_timestamp / 1000)

print(dt)
```

Required for JavaScript and some REST APIs.

## 10. Enterprise Example: Database Time Normalization



```python
from datetime import datetime

def normalize_timestamp(input_value):
    if isinstance(input_value, (int, float)):
        return datetime.fromtimestamp(input_value)
    elif isinstance(input_value, str):
        dt = datetime.strptime(input_value, "%Y-%m-%d %H:%M:%S")
        return dt.timestamp()

print(normalize_timestamp(1732452305))
print(normalize_timestamp("2025-11-24 14:30:00"))
```

Standard pattern for system-wide time normalization.


---
**Score: 30**