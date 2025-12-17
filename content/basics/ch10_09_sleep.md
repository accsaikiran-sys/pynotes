---
title: Ch10 09 Sleep
date: 2025-12-17
author: Your Name
cell_count: 31
score: 30
---

# Python `sleep()`

Examples showing how to pause execution using `time.sleep()` and the async alternative.

## 1. What is `sleep()`



```python
import time

print("Start")
time.sleep(2)
print("Resumed after 2 seconds")
```

`sleep()` pauses execution for the specified number of seconds and halts the current thread.

## 2. Basic Delay in Seconds



```python
import time

time.sleep(5)
print("Executed after 5 seconds")
```

Used for simple task delays and throttling.

## 3. Sleep with Float Values (Sub-second Precision)



```python
import time

time.sleep(0.5)
print("Executed after 0.5 seconds")
```

Supports millisecond-level control.

## 4. Using `sleep()` in Loops



```python
import time

for i in range(3):
    print("Processing", i)
    time.sleep(1)
```

Creates controlled iteration intervals.

## 5. Sleep for Countdown Timer



```python
import time

for i in range(5, 0, -1):
    print("Countdown:", i)
    time.sleep(1)
print("Go!")
```

Common in task scheduling and CLI interfaces.

## 6. Sleep in Retry Mechanism



```python
import time

def retry_operation():
    for attempt in range(3):
        print("Attempt", attempt + 1)
        time.sleep(2)

retry_operation()
```

Used for backoff strategies.

## 7. Sleep in API Rate Limiting



```python
import time

def api_request():
    print("Request sent")
    time.sleep(1)

for _ in range(5):
    api_request()
```

Prevents hitting API limits by spacing requests.

## 8. Sleep for Background Task Simulation



```python
import time

print("Task started...")
time.sleep(3)
print("Task completed.")
```

Simulates long-running processes.

## 9. Non-blocking Alternative (`asyncio.sleep`)



```python
import asyncio

async def task():
    print("Waiting...")
    await asyncio.sleep(2)
    print("Done")

asyncio.run(task())
```

Preferred in asynchronous applications.

## 10. Enterprise Use Case: Controlled Batch Processing



```python
import time

def process_batches():
    for batch in range(1, 4):
        print(f"Processing batch {batch}")
        time.sleep(2)

process_batches()
```

Used in data pipelines, scheduled jobs, ETL, and monitoring systems.


---
**Score: 30**