---
title: Ch09 03 Iterators
date: 2025-12-16
author: Your Name
cell_count: 36
score: 35
---

# Chapter 9.3: Iterators in Python

This notebook covers Python iterators - objects that allow traversal through collections one element at a time, following the iterator protocol.

## 1. What is an Iterator

An iterator is an object that allows traversal through all elements of a collection, one element at a time.


```python
# Basic iterator usage
numbers = [1, 2, 3, 4]
iterator = iter(numbers)

print(next(iterator))  # 1
print(next(iterator))  # 2
print(next(iterator))  # 3
print(next(iterator))  # 4

# Iterator with strings
text = "Hello"
text_iter = iter(text)
print(next(text_iter))  # H
print(next(text_iter))  # e
```

An iterator follows two core methods: `__iter__()` and `__next__()`.

## 2. Iterable vs Iterator


```python
# Iterable vs Iterator demonstration
data = [10, 20, 30]

print("Original list:", data)
print("Is list iterable?", hasattr(data, '__iter__'))
print("Is list iterator?", hasattr(data, '__next__'))

# Convert to iterator
data_iter = iter(data)
print("\nIterator object:", data_iter)
print("Is iterator iterable?", hasattr(data_iter, '__iter__'))
print("Is iterator iterator?", hasattr(data_iter, '__next__'))

# Check types
print(f"\nType of list: {type(data)}")
print(f"Type of iterator: {type(data_iter)}")
```

**Iterable** → Can be looped over  
**Iterator** → Produces values one-by-one

## 3. Using next() with Iterators


```python
# Manual iteration with next()
items = ["A", "B", "C"]
it = iter(items)

print("First item:", next(it))
print("Second item:", next(it))
print("Third item:", next(it))

# Using next() with default value
print("Fourth item (with default):", next(it, "No more items"))

# Dictionary iteration
person = {"name": "Alice", "age": 30, "city": "New York"}
key_iter = iter(person)
print("\nDictionary keys:")
print(next(key_iter))
print(next(key_iter))
print(next(key_iter))
```

`next()` retrieves the next value from the iterator.

## 4. StopIteration Exception


```python
# Demonstrating StopIteration
items = [1, 2]
it = iter(items)

print("Item 1:", next(it))
print("Item 2:", next(it))

# This would raise StopIteration
try:
    print("Item 3:", next(it))
except StopIteration:
    print("No more items - StopIteration raised")

# Safe iteration with default
it2 = iter(["x", "y"])
print("\nSafe iteration:")
print(next(it2, "END"))  # x
print(next(it2, "END"))  # y
print(next(it2, "END"))  # END (no exception)
```

When no items remain, `StopIteration` is raised.

## 5. Iterators in for Loops


```python
# for loop automatically handles iterators
colors = ["red", "green", "blue"]

print("Using for loop:")
for color in colors:
    print(f"Color: {color}")

# Equivalent manual iteration
print("\nManual iteration (equivalent):")
color_iter = iter(colors)
try:
    while True:
        color = next(color_iter)
        print(f"Color: {color}")
except StopIteration:
    print("Iteration complete")

# Multiple iterations
print("\nMultiple for loops on same list:")
for i, color in enumerate(colors):
    print(f"{i}: {color}")
```

The for loop automatically handles iterator creation and termination.

## 6. Creating Custom Iterator Class


```python
# Custom iterator class
class CountUp:
    def __init__(self, limit):
        self.limit = limit
        self.current = 0
    
    def __iter__(self):
        return self
    
    def __next__(self):
        if self.current < self.limit:
            self.current += 1
            return self.current
        raise StopIteration

# Using custom iterator
counter = CountUp(5)
print("Custom iterator output:")
for number in counter:
    print(f"Count: {number}")

# Manual usage
print("\nManual usage:")
counter2 = CountUp(3)
it = iter(counter2)
print(next(it))  # 1
print(next(it))  # 2
print(next(it))  # 3
```

Defines user-controlled iteration logic.

## 7. Infinite Iterator Example


```python
# Infinite iterator (use with caution!)
class InfiniteNumbers:
    def __init__(self, start=0, step=1):
        self.start = start
        self.step = step
    
    def __iter__(self):
        self.num = self.start
        return self
    
    def __next__(self):
        current = self.num
        self.num += self.step
        return current

# Limited usage of infinite iterator
infinite = InfiniteNumbers(1, 2)
it = iter(infinite)

print("First 10 odd numbers:")
for i in range(10):
    print(next(it), end=" ")
print()

# Fibonacci infinite iterator
class Fibonacci:
    def __iter__(self):
        self.a, self.b = 0, 1
        return self
    
    def __next__(self):
        current = self.a
        self.a, self.b = self.b, self.a + self.b
        return current

fib = Fibonacci()
fib_iter = iter(fib)
print("\nFirst 10 Fibonacci numbers:")
for i in range(10):
    print(next(fib_iter), end=" ")
print()
```

Produces an endless sequence unless manually stopped.

## 8. Iterator from Built-in Functions


```python
# String iteration
data = "Python"
it = iter(data)
print("String as list:", list(it))

# Range iteration
range_iter = iter(range(5))
print("Range as list:", list(range_iter))

# Dictionary iterations
person = {"name": "Alice", "age": 30}
print("\nDictionary iterations:")
print("Keys:", list(iter(person.keys())))
print("Values:", list(iter(person.values())))
print("Items:", list(iter(person.items())))

# Set iteration
colors = {"red", "green", "blue"}
print("\nSet iteration:", list(iter(colors)))

# Tuple iteration
coordinates = (10, 20, 30)
print("Tuple iteration:", list(iter(coordinates)))
```

Many built-in data types support iteration natively.

## 9. Checking if an Object is an Iterator


```python
from collections.abc import Iterator, Iterable

# Test different objects
test_objects = [
    [1, 2, 3],           # list
    iter([1, 2, 3]),     # list iterator
    "hello",             # string
    iter("hello"),       # string iterator
    range(5),            # range
    iter(range(5)),      # range iterator
    CountUp(3),          # custom iterator
]

print("Object type analysis:")
print("-" * 50)
for obj in test_objects:
    obj_type = type(obj).__name__
    is_iterable = isinstance(obj, Iterable)
    is_iterator = isinstance(obj, Iterator)
    print(f"{obj_type:15} | Iterable: {is_iterable:5} | Iterator: {is_iterator}")

# Manual check
def check_iterator_protocol(obj):
    has_iter = hasattr(obj, '__iter__')
    has_next = hasattr(obj, '__next__')
    return has_iter and has_next

print("\nManual protocol check:")
numbers = [1, 2, 3]
numbers_iter = iter(numbers)
print(f"List is iterator: {check_iterator_protocol(numbers)}")
print(f"List iterator is iterator: {check_iterator_protocol(numbers_iter)}")
```

Ensures an object conforms to iterator protocol.

## 10. Real-World Iterator Example


```python
# File line reader iterator
class FileLineReader:
    def __init__(self, content):
        # Simulate file content (in real scenario, use filename)
        self.lines = content.split('\n')
        self.index = 0
    
    def __iter__(self):
        return self
    
    def __next__(self):
        if self.index < len(self.lines):
            line = self.lines[self.index]
            self.index += 1
            return line.strip()
        raise StopIteration

# Simulate file content
file_content = """Line 1: Hello World
Line 2: Python Programming
Line 3: Iterator Example
Line 4: End of File"""

print("File line reader:")
reader = FileLineReader(file_content)
for line_num, line in enumerate(reader, 1):
    print(f"{line_num}: {line}")

# CSV-like data processor
class CSVRowIterator:
    def __init__(self, csv_data):
        self.rows = csv_data.strip().split('\n')
        self.index = 0
        self.headers = self.rows[0].split(',') if self.rows else []
    
    def __iter__(self):
        self.index = 1  # Skip header row
        return self
    
    def __next__(self):
        if self.index < len(self.rows):
            row_data = self.rows[self.index].split(',')
            self.index += 1
            # Return as dictionary
            return dict(zip(self.headers, row_data))
        raise StopIteration

# Sample CSV data
csv_data = """name,age,city
Alice,25,New York
Bob,30,San Francisco
Charlie,35,Chicago"""

print("\nCSV data processing:")
csv_reader = CSVRowIterator(csv_data)
for row in csv_reader:
    print(f"Name: {row['name']}, Age: {row['age']}, City: {row['city']}")
```

Efficient for processing large datasets line-by-line.

## Advanced Iterator Patterns


```python
# Iterator with state management
class StatefulIterator:
    def __init__(self, data):
        self.data = data
        self.reset()
    
    def reset(self):
        self.index = 0
        self.processed_count = 0
    
    def __iter__(self):
        return self
    
    def __next__(self):
        if self.index < len(self.data):
            value = self.data[self.index]
            self.index += 1
            self.processed_count += 1
            return value
        raise StopIteration
    
    def get_progress(self):
        return f"{self.processed_count}/{len(self.data)} processed"

# Usage
data = ["apple", "banana", "cherry", "date"]
stateful_iter = StatefulIterator(data)

print("Stateful iterator:")
for item in stateful_iter:
    print(f"Processing: {item} - {stateful_iter.get_progress()}")

# Chained iterators
class ChainedIterator:
    def __init__(self, *iterables):
        self.iterables = iterables
        self.current_iter = None
        self.iter_index = 0
    
    def __iter__(self):
        self.iter_index = 0
        self.current_iter = iter(self.iterables[0]) if self.iterables else None
        return self
    
    def __next__(self):
        while self.current_iter is not None:
            try:
                return next(self.current_iter)
            except StopIteration:
                self.iter_index += 1
                if self.iter_index < len(self.iterables):
                    self.current_iter = iter(self.iterables[self.iter_index])
                else:
                    self.current_iter = None
        raise StopIteration

# Usage
print("\nChained iterator:")
chained = ChainedIterator([1, 2], [3, 4], [5, 6])
for item in chained:
    print(item, end=" ")
print()
```

## Iterator Best Practices


```python
# ✅ Good: Memory efficient for large datasets
def process_large_dataset():
    # Simulate large dataset processing
    class LargeDataIterator:
        def __init__(self, size):
            self.size = size
            self.current = 0
        
        def __iter__(self):
            return self
        
        def __next__(self):
            if self.current < self.size:
                # Simulate processing one item at a time
                result = f"processed_item_{self.current}"
                self.current += 1
                return result
            raise StopIteration
    
    return LargeDataIterator(1000000)  # 1 million items

# Memory efficient processing
print("Processing first 5 items from large dataset:")
large_data = process_large_dataset()
for i, item in enumerate(large_data):
    if i >= 5:  # Only process first 5
        break
    print(item)

# ✅ Good: Proper error handling
def safe_iteration(iterable):
    iterator = iter(iterable)
    while True:
        try:
            item = next(iterator)
            yield item  # Using generator for memory efficiency
        except StopIteration:
            break

print("\nSafe iteration:")
for item in safe_iteration(["a", "b", "c"]):
    print(f"Safe: {item}")
```

## Summary

Python iterators provide:
- **Memory efficient** data processing
- **Lazy evaluation** for large datasets
- **Custom iteration logic** through `__iter__()` and `__next__()`
- **Protocol-based design** for consistency
- **Integration** with for loops and built-in functions

**Key concepts:**
- **Iterable**: Objects that can be iterated over (have `__iter__()`)
- **Iterator**: Objects that produce values one at a time (have `__iter__()` and `__next__()`)
- **StopIteration**: Exception raised when iteration is complete
- **Custom iterators**: User-defined classes following the iterator protocol

**Best practices:**
- Use iterators for memory-efficient processing of large datasets
- Implement proper error handling with StopIteration
- Consider generators for simpler iterator creation
- Always implement both `__iter__()` and `__next__()` methods


---
**Score: 35**