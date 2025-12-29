---
title: Ch10 08 Time Module
date: 2025-12-27
author: Your Name
cell_count: 31
score: 30
---

# Python `time` Module

The `time` module provides low-level time-related functions for timestamps, delays, performance measurement, and system clock interactions.

## 1. What is the `time` Module



```python
import time

print(time.time())
```

Returns current time in seconds since the Unix Epoch.

## 2. Get Current Time as Readable String



```python
import time

current_time = time.ctime()
print(current_time)
```

Outputs human-readable system time, e.g.: Mon Nov 24 09:45:32 2025.

## 3. Get Current Time Components



```python
import time

t = time.localtime()
print("Hour:", t.tm_hour)
print("Minute:", t.tm_min)
print("Second:", t.tm_sec)
```

Breaks current time into structured components.

## 4. Sleep / Delay Execution



```python
import time

print("Start")
time.sleep(2)
print("End after 2 seconds")
```

Pauses program execution for specified seconds.

## 5. Measure Execution Time (Performance Timing)



```python
import time

start = time.time()
time.sleep(1)
end = time.time()

print("Execution Time:", end - start, "seconds")
```

Used for benchmarking and performance profiling.

## 6. High-Precision Timer with `perf_counter()`



```python
import time

start = time.perf_counter()
time.sleep(0.5)
end = time.perf_counter()

print("Precise Time:", end - start)
```

Recommended for performance-sensitive measurements.

## 7. Formatting Time with `strftime()`



```python
import time

formatted = time.strftime("%Y-%m-%d %H:%M:%S")
print(formatted)
```

Formats time using system clock.

## 8. Parsing Time with `strptime()`



```python
import time

parsed = time.strptime("24-11-2025 10:30:00", "%d-%m-%Y %H:%M:%S")
print(parsed)
```

Converts strings into time-struct objects.

## 9. Convert Timestamp to Readable Time



```python
import time

timestamp = time.time()
readable = time.ctime(timestamp)

print(readable)
```

Common pattern for API responses and logs.

## 10. Enterprise Use Case: Rate Limiting Logic



```python
import time

last_request = time.time()

def can_execute():
    global last_request
    current = time.time()
    if current - last_request >= 5:
        last_request = current
        return True
    return False

print(can_execute())
```

Controls execution frequency in APIs and services.


---
**Score: 30**