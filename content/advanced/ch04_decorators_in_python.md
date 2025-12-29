---
title: Ch04 Decorators In Python
date: 2025-12-27
author: Your Name
cell_count: 46
score: 45
---

# Decorators in Python


## 1. Concept Overview
Decorators in Python are a meta-programming construct used to dynamically modify or extend the behavior of functions, methods, or classes without altering their original source code.

They enable cross-cutting concern implementation, behavior enhancement without inheritance, cleaner separation of concerns, configurable execution control, and transparent function augmentation. Decorators wrap functionality around existing logic while preserving its core identity.


## 2. Why Decorators Matter in Enterprise Systems
In large-scale applications, decorators provide centralized logic control, reusable pre/post-processing layers, consistent behavioral injection, reduced code duplication, and modular extensibility. Critical for logging, authentication, authorization, performance monitoring, rate limiting, caching, and validation.


## 3. Basic Decorator Structure



```python
def my_decorator(func):
    def wrapper():
        print("Before execution")
        func()
        print("After execution")
    return wrapper

@my_decorator
def greet():
    print("Hello")

greet()

```

Flow: greet → wrapper → greet logic → wrapper exit.


## 4. Execution Flow of Decorators
Function Definition → Decorator Applied → Wrapper Generated → Execution Triggered. Decorators intercept execution transparently.


## 5. Decorators with Arguments



```python
def logger(func):
    def wrapper(*args, **kwargs):
        print("Calling function")
        return func(*args, **kwargs)
    return wrapper

```

Preserves argument flexibility.


## 6. Decorators with Parameters



```python
def repeat(times):
    def decorator(func):
        def wrapper():
            for _ in range(times):
                func()
        return wrapper
    return decorator

@repeat(3)
def say_hi():
    print("Hi")

say_hi()

```

Supports configurable behavior injection.


## 7. Class-Based Decorators



```python
class AuthDecorator:
    def __init__(self, func):
        self.func = func

    def __call__(self, *args, **kwargs):
        print("Authentication Check")
        return self.func(*args, **kwargs)

@AuthDecorator
def secured_action():
    print("secured")

secured_action()

```

Used for stateful decorations and complex execution control.


## 8. Built-in Decorators in Python
@staticmethod, @classmethod, @property, @abstractmethod provide core OOP behaviors.


## 9. Preserving Function Metadata



```python
from functools import wraps

def my_decorator(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs)
    return wrapper

```

wraps preserves name, docstring, and signature—critical for debugging and docs.


## 10. Chaining Multiple Decorators



```python
def deco1(fn):
    def w(*a, **k):
        print('deco1')
        return fn(*a, **k)
    return w

def deco2(fn):
    def w(*a, **k):
        print('deco2')
        return fn(*a, **k)
    return w

@deco1
@deco2
def process():
    print('process')

process()  # deco1(deco2(process))

```

Used heavily in frameworks; execution is top-down in decoration, bottom-up in call.


## 11. Logging Decorator Pattern



```python
def log_execution(func):
    def wrapper(*args, **kwargs):
        print(f"Executing {func.__name__}")
        return func(*args, **kwargs)
    return wrapper

```

Enterprise usage: observability systems, auditing, performance tracking.


## 12. Authentication Decorator



```python
def authorize(func):
    def wrapper(*args, **kwargs):
        # if not user_is_authenticated():
        #     raise Exception("Unauthorized")
        return func(*args, **kwargs)
    return wrapper

```

Used in admin panels, secure routes, API gateways.


## 13. Caching Decorator



```python
from functools import lru_cache

@lru_cache(maxsize=128)
def calculate(x):
    return x * x

```

Optimizes AI workloads, data processing, and high-latency functions.


## 14. Rate Limiting Decorator



```python
def rate_limit(func):
    def wrapper(*args, **kwargs):
        # if exceeded():
        #     raise Exception("Rate limit exceeded")
        return func(*args, **kwargs)
    return wrapper

```

Critical for API governance.


## 15. Timing Decorator



```python
import time

def timer(func):
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        print("Time:", time.time() - start)
        return result
    return wrapper

```

Used for performance debugging, profiling, benchmarking.


## 16. Decorators vs Inheritance
Decorators inject behavior dynamically; inheritance extends class hierarchies statically. Decorators are more modular and suited for cross-cutting concerns.


## 17. Enterprise Framework Usage
Flask (@app.route), FastAPI (@app.get), Django (@login_required), Celery (@task) rely on decorators to define system behavior flow.


## 18. Advanced Use Case: Validation Decorator



```python
def validate_positive(func):
    def wrapper(value):
        if value < 0:
            raise ValueError("Must be positive")
        return func(value)
    return wrapper

```

Ensures input safety.


## 19. Decorators for Dependency Injection



```python
def inject_dependency(service):
    def decorator(func):
        def wrapper():
            return func(service)
        return wrapper
    return decorator

```

Promotes loose coupling and modular design.



---
**Score: 45**