---
title: Ch11 06 Args Kwargs
date: 2026-01-07
author: Your Name
cell_count: 35
score: 35
---

# Python *args and **kwargs

Using variable positional (*args) and variable keyword (**kwargs) arguments for flexible function signatures.

## 1. What are *args and **kwargs



```python
def demo(*args, **kwargs):
    print(args)
    print(kwargs)

demo(1, 2, 3, name='Alice', age=30)
```

*args captures positional arguments as a tuple; **kwargs captures keyword arguments as a dict.

## 2. Using *args (Variable Positional Arguments)



```python
def add_numbers(*args):
    return sum(args)

print(add_numbers(1, 2, 3, 4))  # 10
```

All positional arguments are captured as a tuple.

## 3. Iterating Over *args



```python
def display_values(*args):
    for value in args:
        print(value)

display_values('Python', 'AI', 'ML')
```

Ideal for functions handling unknown input sizes.

## 4. Using **kwargs (Variable Keyword Arguments)



```python
def display_profile(**kwargs):
    for key, value in kwargs.items():
        print(f'{key}: {value}')

display_profile(name='Alice', role='Engineer', location='Toronto')
```

All keyword arguments are captured as a dictionary.

## 5. Combining *args and **kwargs



```python
def process_data(*args, **kwargs):
    print('Positional:', args)
    print('Keyword:', kwargs)

process_data(10, 20, user='CSP', status='Active')
```

Supports highly dynamic functions.

## 6. Order of Parameters



```python
def example(a, b, *args, c=10, **kwargs):
    print(a, b, args, c, kwargs)

example(1, 2, 3, 4, key='value')
```

Order: regular params → *args → defaults → **kwargs. Violating this order causes syntax errors.

## 7. Unpacking Arguments with * and **



```python
def greet(name, age):
    print(f'{name} is {age} years old')

data = ('Alice', 30)
greet(*data)

info = {'name': 'Bob', 'age': 25}
greet(**info)
```

Use * and ** to unpack tuples/dicts into arguments.

## 8. Forwarding Arguments to Another Function



```python
def calculate(a, b):
    return a + b

def wrapper(*args, **kwargs):
    return calculate(*args, **kwargs)

print(wrapper(5, 10))
```

Common in decorators and middleware for argument forwarding.

## 9. Dynamic API Handler Example



```python
def api_handler(endpoint, *args, **kwargs):
    print(f'Calling {endpoint}')
    print('Params:', args)
    print('Options:', kwargs)

api_handler('/users', 1, 2, limit=10, sort='asc')
```

Useful for REST clients and flexible service routers.

## 10. Enterprise-Grade Example



```python
def log_event(event_type, *args, **kwargs):
    print(f'Event: {event_type}')
    if args:
        print('Details:', args)
    if kwargs:
        print('Metadata:', kwargs)

log_event('LOGIN', 'UserID:101', ip='192.168.1.1', status='success')
```

Ideal for dynamic logging, analytics, and telemetry systems.

## Comparison: *args vs **kwargs
- *args → tuple of positional arguments.
- **kwargs → dict of named arguments.
- Use for extensible APIs, decorators, middleware, and plugin systems.

## Common Mistakes
- Assuming args is a list (it's a tuple).
- Incorrect parameter order.
- Overusing when fixed parameters suffice.
- Naming differently but expecting *args/**kwargs semantics.

## Best Practices
- Use *args for extensibility, not ambiguity.
- Prefer descriptive parameter names and type hints.
- Validate arguments where applicable.
- Document expected keys and argument shapes.

## Enterprise Value
- Powers extensible APIs, decorators, middleware, and modular systems.
- Enables reusable utilities and dynamic execution engines.


---
**Score: 35**