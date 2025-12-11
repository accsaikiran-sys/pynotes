---
title: Ch09 04 Generators
date: 2025-12-10
author: Your Name
cell_count: 36
score: 35
---

# Chapter 9.4: Generators in Python

This notebook covers Python generators - special functions that return iterators and yield values one at a time, providing memory-efficient lazy evaluation.

## 1. What is a Generator

A generator is a special type of function that returns an iterator and yields values one at a time using the yield keyword instead of return.


```python
# Basic generator function
def simple_generator():
    yield 1
    yield 2
    yield 3

# Create generator object
gen = simple_generator()
print("Generator object:", gen)
print("Type:", type(gen))

# Get values one by one
print("First value:", next(gen))   # 1
print("Second value:", next(gen))  # 2
print("Third value:", next(gen))   # 3

# Convert to list
gen2 = simple_generator()
print("All values:", list(gen2))   # [1, 2, 3]
```

Generators produce values lazily, improving memory efficiency.

## 2. Generator vs Normal Function


```python
# Normal function - returns once
def normal_function():
    return 10
    return 20  # This line is never reached

# Generator function - yields multiple times
def generator_function():
    yield 10
    yield 20
    yield 30

print("Normal function result:", normal_function())          # 10
print("Generator function result:", generator_function())    # <generator object>
print("Generator as list:", list(generator_function()))     # [10, 20, 30]

# Demonstrate multiple calls
print("\nMultiple calls:")
print("Normal function call 1:", normal_function())
print("Normal function call 2:", normal_function())

gen = generator_function()
print("Generator call 1:", next(gen))
print("Generator call 2:", next(gen))
print("Generator call 3:", next(gen))
```

    Normal function result: 10
    Generator function result: <generator object generator_function at 0x71e2d0ca1dd0>
    Generator as list: [10, 20, 30]
    
    Multiple calls:
    Normal function call 1: 10
    Normal function call 2: 10
    Generator call 1: 10
    Generator call 2: 20
    Generator call 3: 30


A normal function returns once; a generator yields multiple times.

## 3. Iterating Over a Generator


```python
# Generator with loop logic
def count_up(n):
    for i in range(1, n + 1):
        yield i

print("Counting up to 5:")
for num in count_up(5):
    print(f"Number: {num}")

# Generator with conditional logic
def even_numbers(limit):
    for i in range(limit):
        if i % 2 == 0:
            yield i

print("\nEven numbers up to 10:")
for num in even_numbers(11):
    print(num, end=" ")
print()

# Generator with string processing
def word_generator(text):
    for word in text.split():
        yield word.upper()

print("\nWord processing:")
for word in word_generator("hello world python"):
    print(word)
```

Generators integrate seamlessly with loops.

## 4. Generator State Preservation


```python
# Demonstrate state preservation
def demo_state():
    print("Generator started")
    yield 1
    print("After first yield")
    yield 2
    print("After second yield")
    yield 3
    print("Generator finished")

print("Creating generator:")
g = demo_state()
print("\nCalling next() first time:")
print("Value:", next(g))
print("\nCalling next() second time:")
print("Value:", next(g))
print("\nCalling next() third time:")
print("Value:", next(g))

# Generator with local variables
def counter_with_state():
    count = 0
    while count < 3:
        count += 1
        yield f"Count is {count}"

print("\n\nCounter with state:")
counter = counter_with_state()
for value in counter:
    print(value)
```

Execution pauses and resumes, preserving internal state automatically.

## 5. Memory Efficiency of Generators


```python
import sys

# Memory comparison: List vs Generator
def create_list(n):
    return [i for i in range(n)]

def create_generator(n):
    for i in range(n):
        yield i

# Small example for demonstration
n = 1000

# Create list
my_list = create_list(n)
list_size = sys.getsizeof(my_list)

# Create generator
my_gen = create_generator(n)
gen_size = sys.getsizeof(my_gen)

print(f"List of {n} items: {list_size} bytes")
print(f"Generator for {n} items: {gen_size} bytes")
print(f"Memory ratio: {list_size / gen_size:.1f}x")

# Demonstrate lazy evaluation
def large_numbers():
    print("Generator created, but no computation yet")
    for i in range(1000000):
        yield i * i

print("\nCreating generator for 1 million squares:")
gen = large_numbers()
print("Generator created (no memory allocated for all values)")

print("Getting first few values:")
print(next(gen))  # 0
print(next(gen))  # 1
print(next(gen))  # 4
```

Unlike lists, generators do not load all data into memory.

## 6. Generator Expression


```python
# Generator expression (similar to list comprehension)
squares = (x ** 2 for x in range(5))
print("Generator expression:", squares)
print("Values:", list(squares))

# Compare with list comprehension
squares_list = [x ** 2 for x in range(5)]
squares_gen = (x ** 2 for x in range(5))

print(f"\nList comprehension type: {type(squares_list)}")
print(f"Generator expression type: {type(squares_gen)}")

# Generator with filtering
even_squares = (x ** 2 for x in range(10) if x % 2 == 0)
print("\nEven squares:", list(even_squares))

# Nested generator expressions
matrix = ((i * j for j in range(3)) for i in range(3))
print("\nMatrix (nested generators):")
for row in matrix:
    print(list(row))

# Generator with string processing
words = "hello world python programming".split()
lengths = (len(word) for word in words)
print("\nWord lengths:", list(lengths))
```

Similar to list comprehensions but return a generator object.

## 7. Using Generators with next()


```python
# Manual control with next()
def alpha_generator():
    yield "A"
    yield "B"
    yield "C"

gen = alpha_generator()
print("Manual iteration:")
print("First:", next(gen))
print("Second:", next(gen))
print("Third:", next(gen))

# Using next() with default value
gen2 = alpha_generator()
print("\nWith default values:")
print(next(gen2, "DEFAULT"))  # A
print(next(gen2, "DEFAULT"))  # B
print(next(gen2, "DEFAULT"))  # C
print(next(gen2, "DEFAULT"))  # DEFAULT (no StopIteration)

# Conditional processing
def number_generator():
    for i in range(10):
        yield i

print("\nConditional processing:")
num_gen = number_generator()
while True:
    value = next(num_gen, None)
    if value is None:
        print("Generator exhausted")
        break
    if value > 5:
        print(f"Found number > 5: {value}")
        break
    print(f"Processing: {value}")
```

Direct control over iteration flow.

## 8. Infinite Generator


```python
# Infinite counter
def infinite_counter(start=1, step=1):
    num = start
    while True:
        yield num
        num += step

counter = infinite_counter()
print("First 5 numbers from infinite counter:")
for i in range(5):
    print(next(counter), end=" ")
print()

# Infinite Fibonacci sequence
def fibonacci():
    a, b = 0, 1
    while True:
        yield a
        a, b = b, a + b

fib = fibonacci()
print("\nFirst 10 Fibonacci numbers:")
for i in range(10):
    print(next(fib), end=" ")
print()

# Infinite cycle through items
def cycle(items):
    while True:
        for item in items:
            yield item

colors = cycle(["red", "green", "blue"])
print("\nCycling through colors:")
for i in range(8):
    print(next(colors), end=" ")
print()

# Random number generator
import random

def random_numbers(min_val=1, max_val=100):
    while True:
        yield random.randint(min_val, max_val)

rand_gen = random_numbers(1, 10)
print("\n5 random numbers:")
for i in range(5):
    print(next(rand_gen), end=" ")
print()
```

Produces an infinite sequence until manually stopped.

## 9. Generator with try...finally


```python
# Resource management with generators
def resource_handler():
    print("Acquiring resource")
    try:
        yield "Using resource"
        yield "Still using resource"
    finally:
        print("Resource released")

print("Normal completion:")
gen = resource_handler()
print(next(gen))
print(next(gen))
try:
    print(next(gen))  # This will raise StopIteration
except StopIteration:
    print("Generator completed")

# Early termination
print("\nEarly termination:")
gen2 = resource_handler()
print(next(gen2))
gen2.close()  # Explicitly close generator

# File-like resource management
def file_processor(content):
    print("Opening file")
    try:
        lines = content.split('\n')
        for line in lines:
            yield line.strip()
    finally:
        print("Closing file")

print("\nFile processing:")
content = "Line 1\nLine 2\nLine 3"
processor = file_processor(content)
for line in processor:
    print(f"Processing: {line}")
    if line == "Line 2":
        break  # Early exit
# Finally block still executes
```

Ensures cleanup logic is executed after generator completion.

## 10. Real-World Generator Example (Streaming Data)


```python
# Simulate large file reading
def read_large_file(content):
    """Simulate reading a large file line by line"""
    lines = content.split('\n')
    for line in lines:
        # Simulate processing time
        yield line.strip()

# Sample file content
file_content = """2023-01-01,user1,login
2023-01-01,user2,logout
2023-01-01,user1,purchase,100
2023-01-01,user3,login
2023-01-01,user2,login
2023-01-01,user1,logout"""

print("Processing log file:")
for line_num, line in enumerate(read_large_file(file_content), 1):
    if line:  # Skip empty lines
        parts = line.split(',')
        if len(parts) >= 3:
            date, user, action = parts[0], parts[1], parts[2]
            print(f"Line {line_num}: {user} performed {action} on {date}")

# Data processing pipeline with generators
def parse_log_line(line):
    """Parse a single log line"""
    parts = line.split(',')
    if len(parts) >= 3:
        return {
            'date': parts[0],
            'user': parts[1],
            'action': parts[2],
            'value': parts[3] if len(parts) > 3 else None
        }
    return None

def filter_actions(log_entries, action_type):
    """Filter log entries by action type"""
    for entry in log_entries:
        if entry and entry['action'] == action_type:
            yield entry

def process_purchases(log_entries):
    """Process purchase entries"""
    total = 0
    count = 0
    for entry in log_entries:
        if entry and entry['value']:
            total += int(entry['value'])
            count += 1
            yield {
                'user': entry['user'],
                'amount': int(entry['value']),
                'running_total': total,
                'transaction_count': count
            }

print("\nData processing pipeline:")
# Create processing pipeline
raw_lines = read_large_file(file_content)
parsed_entries = (parse_log_line(line) for line in raw_lines if line)
purchase_entries = filter_actions(parsed_entries, 'purchase')
processed_purchases = process_purchases(purchase_entries)

# Process the pipeline
for purchase in processed_purchases:
    print(f"User {purchase['user']}: ${purchase['amount']} "
          f"(Total: ${purchase['running_total']}, Count: {purchase['transaction_count']})")
```

Ideal for processing large files or streaming data efficiently.

## Advanced Generator Patterns


```python
# Generator delegation with yield from
def sub_generator():
    yield 1
    yield 2
    yield 3

def main_generator():
    yield "start"
    yield from sub_generator()  # Delegate to sub-generator
    yield "end"

print("Generator delegation:")
for value in main_generator():
    print(value)

# Generator with send() method
def accumulator():
    total = 0
    while True:
        value = yield total
        if value is not None:
            total += value

print("\nGenerator with send():")
acc = accumulator()
print("Initial:", next(acc))  # Start the generator
print("Send 10:", acc.send(10))
print("Send 5:", acc.send(5))
print("Send 3:", acc.send(3))

# Generator chaining
def chain_generators(*generators):
    for gen in generators:
        yield from gen

gen1 = (x for x in range(3))
gen2 = (x for x in range(3, 6))
gen3 = (x for x in range(6, 9))

print("\nChained generators:")
for value in chain_generators(gen1, gen2, gen3):
    print(value, end=" ")
print()
```

## Generator Best Practices


```python
# ✅ Good: Use generators for large datasets
def process_large_dataset(size):
    """Memory-efficient processing of large dataset"""
    for i in range(size):
        # Simulate expensive computation
        result = i ** 2 + i
        yield result

# ✅ Good: Generator for file processing
def process_csv_data(csv_content):
    """Process CSV data line by line"""
    lines = csv_content.strip().split('\n')
    headers = lines[0].split(',')
    
    for line in lines[1:]:
        values = line.split(',')
        yield dict(zip(headers, values))

# ✅ Good: Error handling in generators
def safe_generator(data):
    """Generator with proper error handling"""
    try:
        for item in data:
            if isinstance(item, (int, float)):
                yield item * 2
            else:
                print(f"Skipping invalid item: {item}")
    except Exception as e:
        print(f"Error in generator: {e}")
    finally:
        print("Generator cleanup completed")

# Example usage
print("Processing mixed data:")
mixed_data = [1, 2, "invalid", 3, 4.5, None, 6]
for result in safe_generator(mixed_data):
    print(f"Result: {result}")

# Performance comparison
import time

def list_approach(n):
    return [x ** 2 for x in range(n)]

def generator_approach(n):
    return (x ** 2 for x in range(n))

n = 100000

# Time list creation
start = time.time()
my_list = list_approach(n)
list_time = time.time() - start

# Time generator creation
start = time.time()
my_gen = generator_approach(n)
gen_time = time.time() - start

print(f"\nPerformance comparison for {n} items:")
print(f"List creation time: {list_time:.6f} seconds")
print(f"Generator creation time: {gen_time:.6f} seconds")
print(f"Generator is {list_time/gen_time:.0f}x faster to create")
```

## Summary

Python generators provide:
- **Memory efficiency** through lazy evaluation
- **State preservation** between yields
- **Clean syntax** with yield keyword
- **Iterator protocol** compliance
- **Streaming data processing** capabilities

**Key concepts:**
- **yield**: Pauses function execution and returns a value
- **Generator function**: Function containing yield statements
- **Generator expression**: Compact syntax like list comprehensions
- **Lazy evaluation**: Values computed on-demand
- **State preservation**: Local variables maintained between calls

**When to use generators:**
- Processing large datasets that don't fit in memory
- Streaming data processing
- Creating infinite sequences
- Pipeline data processing
- When you need iterator behavior with custom logic

**Best practices:**
- Use generators for memory-efficient data processing
- Include proper error handling with try/finally
- Consider generator expressions for simple cases
- Use `yield from` for generator delegation
- Document generator behavior and expected usage


---
**Score: 35**