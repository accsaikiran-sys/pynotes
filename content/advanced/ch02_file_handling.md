---
title: Ch02 File Handling
date: 2025-12-18
author: Your Name
cell_count: 93
score: 90
---

# Python File HandlingFile handling lets Python programs read, write, update, and manage files on disk for persistence, exchange, logging, and configuration.

## 1. Introduction to File Handling

Persistent storage, log management, data exchange, and configuration.


```python
file = open('sample.txt', 'r')print(file.read())file.close()
```

## 2. File Opening Modes

Modes: r (read), w (overwrite), a (append), x (create), b (binary), t (text), + (read & write).


```python
file = open('log.txt', 'w')
```

## 3. Using with Statement (Best Practice)


```python
with open('data.txt', 'r') as file:    content = file.read()    print(content)
```

## 4. Reading Files


```python
# Read entire filewith open('file.txt') as f:    print(f.read())# Line by linewith open('file.txt') as f:    for line in f:        print(line.strip())# Read specific characterswith open('file.txt') as f:    print(f.read(5))
```

## 5. Writing Files


```python
with open('output.txt', 'w') as f:    f.write('Hello Python')    f.write('File Handling Example')
```

## 6. Appending Data


```python
with open('log.txt', 'a') as f:    f.write('New entry added')
```

## 7. Working with Binary Files


```python
with open('image.png', 'rb') as file:    binary_data = file.read()
```

Used for images, PDFs, audio, and other binary assets.

## 8. File Pointer and seek()


```python
with open('file.txt', 'r') as f:    print(f.read(5))    f.seek(0)    print(f.read(5))
```

## 9. File Attributes


```python
with open('file.txt') as f:    print(f.name)    print(f.mode)    print(f.closed)
```

## 10. Enterprise Example: Log File Processor


```python
def log_reader(file_path):    with open(file_path, 'r') as f:        for line in f:            if 'ERROR' in line:                print(line.strip())log_reader('application.log')
```

## Advanced File Operations

### 11. Checking File Existence


```python
import osif os.path.exists('report.txt'):    print('File exists')
```

### 12. Deleting Files


```python
import osos.remove('old_data.txt')
```

### 13. Renaming Files


```python
import osos.rename('old.txt', 'new.txt')
```

### 14. Directory Operations


```python
import osos.mkdir('reports')os.rmdir('reports')
```

### Handling Large Files Efficiently


```python
with open('bigfile.txt') as f:    for line in f:        process(line)
```

Prefer streaming to avoid loading entire files into memory.

## File Handling Best Practices

Use context managers, handle exceptions, avoid hardcoded paths, prefer streaming for large files.

## Common Errors

FileNotFoundError, PermissionError, IOError, IsADirectoryError

## Enterprise Applications

Essential for ETL pipelines, AI datasets, configuration systems, backups, and log aggregation.

## Performance Considerations

Read in chunks for large files, use buffering, avoid repeated open/close cycles, handle exceptions gracefully.

---

# Python File Handling — Deep Dive & Enterprise Guide

## 1. Concept Overview

Foundational for persistence, ETL, logs, configs, backups; high-level and low-level APIs with OS integration.

## 2. File Operation Lifecycle


```python
file = open('data.txt', 'r')content = file.read()file.close()
```

Context managers replace manual close for safety.

## 3. Context Manager (with) – Enterprise Standard


```python
with open('data.txt', 'r') as file:    content = file.read()
```

Automatic cleanup, exception safety, cleaner flow.

## 4. File Modes Deep Dive

r, w, a, x, b, t, r+ (read/write)


```python
open('log.txt', 'w')open('image.png', 'rb')open('data.txt', 'a+')
```

## 5. Reading Files at Scale


```python
with open('file.txt') as f:    data = f.read()with open('file.txt') as f:    for line in f:        print(line.strip())
```

Streaming prevents memory overflow on large files.

## 6. Writing and Appending Strategies


```python
with open('report.txt', 'w') as f:    f.write('Annual Report')with open('log.txt', 'a') as f:    f.write('New log entry')
```

## 7. Binary File Handling


```python
with open('photo.jpg', 'rb') as file:    binary_data = file.read()
```

## 8. File Pointer Management


```python
with open('file.txt') as f:    print(f.read(5))    f.seek(0)    print(f.read(5))
```

## 9. Chunk-Based File Processing (Performance Pattern)


```python
def read_large_file(path):    with open(path, 'r') as f:        while chunk := f.read(1024):            process(chunk)
```

Prevents memory saturation.

## 10. File Attributes and Metadata


```python
import osprint(os.path.getsize('file.txt'))print(os.path.getmtime('file.txt'))
```

## 11. Directory Handling


```python
import osos.mkdir('reports')os.listdir('.')os.rmdir('reports')
```

## 12. Recursive File Traversal


```python
import osfor root, dirs, files in os.walk('project'):    for file in files:        print(file)
```

## 13. File Security and Permissions


```python
import osos.chmod('secure.txt', 0o644)
```

## 14. Exception Handling in File Operations


```python
try:    with open('data.txt') as f:        print(f.read())except FileNotFoundError:    print('File missing')finally:    print('Execution finished')
```

## 15. File Locking (Concurrency Control)


```python
import fcntl# fcntl.flock(file, fcntl.LOCK_EX)  # example usage on Unix
```

## 16. Enterprise Use Case: Log Processing Engine


```python
def error_scanner(file_path):    with open(file_path) as f:        for line in f:            if 'ERROR' in line:                print(line.strip())error_scanner('server.log')
```

## 17. Python File Handling vs Database

Files: lightweight, great for logs/archives. Databases: structured, transactional, relational.

## 18. Performance Optimization Techniques

Streaming, buffering, chunk reads, context managers.

## 19. Common Pitfalls

Leaving files open, loading huge files into memory, hardcoded paths, ignoring errors, parallel write conflicts.

## 20. Best Practices

Always use with; stream large files; handle exceptions; avoid path confusion; separate logic from I/O.

## 21. Enterprise Importance

Critical for distributed logging, ETL, backups, AI datasets, and automation—delivers persistence, fault tolerance, scalability, and resilience.


---
**Score: 90**