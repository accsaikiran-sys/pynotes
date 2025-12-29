---
title: Ch04 Function Decorators Advanced
date: 2025-12-27
author: Your Name
cell_count: 66
score: 65
---

# Python Function Decorators (Advanced)


## 1. Strategic Overview
Advanced Python Function Decorators enable dynamic modification of function behavior without altering source code. At an enterprise level, they enforce cross-cutting concerns like logging, authentication, caching, performance monitoring, circuit breaking, validation, and access control.

They enable behavior injection without duplication, clean separation of concerns, policy-driven execution control, runtime augmentation, and modular architecture. Decorators act as behavioral middleware for execution pipelines.


## 2. Enterprise Significance
Without advanced decorators: repetitive boilerplate, tight coupling, low maintainability, unscalable cross-cutting concerns, unsafe execution control.
With decorators: centralized governance, uniform policy enforcement, clean scaling, performance/security control, predictable flows.


## 3. Decorator Execution Architecture
Function Definition → Decorator Application → Wrapper Injection → Runtime Execution → Behavior Modification.
Decorators dynamically redefine call behavior.


## 4. Basic Decorator Recap



```python
def my_decorator(func):
    def wrapper(*args, **kwargs):
        print("Before execution")
        result = func(*args, **kwargs)
        print("After execution")
        return result
    return wrapper

@my_decorator
def process():
    print("Processing...")

process()

```

Base pattern for advanced usage.


## 5. Decorators with Arguments



```python
def repeat(times):
    def decorator(func):
        def wrapper(*args, **kwargs):
            for _ in range(times):
                func(*args, **kwargs)
        return wrapper
    return decorator

@repeat(3)
def greet():
    print("Hello")

greet()

```

Creates configurable behavior.


## 6. Preserving Function Metadata



```python
from functools import wraps

def logged(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs)
    return wrapper

```

Prevents loss of function identity (name, docstring, signature).


## 7. Authentication Decorator



```python
def require_auth(func):
    def wrapper(user, *args, **kwargs):
        if not getattr(user, "is_authenticated", False):
            raise PermissionError("Unauthorized")
        return func(user, *args, **kwargs)
    return wrapper

```

Common in APIs and service layers.


## 8. Logging Decorator



```python
def log_execution(func):
    def wrapper(*args, **kwargs):
        print(f"Executing {func.__name__}")
        return func(*args, **kwargs)
    return wrapper

```

Centralized tracing.


## 9. Performance Monitoring Decorator



```python
import time

def timeit(func):
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        print(f"Time: {time.time() - start}")
        return result
    return wrapper

```

Optimization diagnostics.


## 10. Caching Decorator



```python
from functools import lru_cache

@lru_cache(maxsize=128)
def compute(x):
    return x * x

```

Essential for high-performance systems.


## 11. Retry Mechanism Decorator



```python
def retry(times=3):
    def decorator(func):
        def wrapper(*args, **kwargs):
            for attempt in range(times):
                try:
                    return func(*args, **kwargs)
                except Exception:
                    continue
            raise RuntimeError("Failed after retries")
        return wrapper
    return decorator

```

Used in network/reliability engineering.


## 12. Input Validation Decorator



```python
def validate_positive(func):
    def wrapper(x):
        if x < 0:
            raise ValueError("Negative value")
        return func(x)
    return wrapper

```

Enforces safe inputs.


## 13. Stateful Decorators



```python
def call_counter(func):
    count = 0
    def wrapper(*args, **kwargs):
        nonlocal count
        count += 1
        return func(*args, **kwargs)
    return wrapper

```

Useful for analytics/telemetry.


## 14. Class-Based Decorators



```python
class Logger:
    def __init__(self, func):
        self.func = func

    def __call__(self, *args, **kwargs):
        print("Logging...")
        return self.func(*args, **kwargs)

```

Supports advanced object control.


## 15. Decorators for Access Control



```python
def admin_only(func):
    def wrapper(user, *args, **kwargs):
        if getattr(user, "role", None) != "admin":
            raise PermissionError("Admin only")
        return func(user, *args, **kwargs)
    return wrapper

```

Crucial for security layers.


## 16. Chained Decorators



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
def fetch_data():
    print('data')

fetch_data()  # deco1(deco2(fetch_data))

```

Layer behaviors in sequence.


## 17. Exception Handling Decorator



```python
def safe_execute(func):
    def wrapper(*args, **kwargs):
        try:
            return func(*args, **kwargs)
        except Exception as e:
            print("Handled:", e)
    return wrapper

```

Used in fault tolerance.


## 18. Decorators for Dependency Injection



```python
def inject_db(func):
    def wrapper(*args, **kwargs):
        kwargs['db'] = 'DB_CONN'
        return func(*args, **kwargs)
    return wrapper

```

Improves modularity.


## 19. Decorator for Rate Limiting



```python
def rate_limit(limit):
    calls = 0
    def decorator(func):
        def wrapper(*args, **kwargs):
            nonlocal calls
            if calls >= limit:
                raise Exception("Rate limit exceeded")
            calls += 1
            return func(*args, **kwargs)
        return wrapper
    return decorator

```

Prevents abuse.


## 20. Metadata Injection Decorators



```python
def tag(label):
    def decorator(func):
        func.tag = label
        return func
    return decorator

```

Useful for introspection and frameworks.


## 21. Decorators in Web Frameworks
Flask (@app.route), FastAPI (@app.get), Django (@login_required), Celery (@task) all rely heavily on decorators to define behavior flow.


## 22. Decorators for Transaction Control



```python
def transaction(func):
    def wrapper(*args, **kwargs):
        # begin()
        try:
            result = func(*args, **kwargs)
            # commit()
            return result
        except:
            # rollback()
            raise
    return wrapper

```

Used in finance and data systems.


## 23. Anti-Patterns
- Deep nesting (comprehension loss)
- Ignoring wraps (metadata corruption)
- Overusing decorators (debug complexity)
- Silent mutation (unpredictability)


## 24. Best Practices
- Always use functools.wraps
- Keep decorators single-purpose
- Avoid heavy business logic inside decorators
- Document behavior
- Maintain predictable ordering


## 25. Decorator Governance Model
Function Core → Decorator Layer → Execution Policy → Output Behavior. Separates policy from logic.


## 26. Advanced Decorator Patterns
Policy-driven decorators, context-aware decorators, async-compatible decorators, retry + circuit breaker hybrids, distributed telemetry decorators.


## 27. Async Decorators



```python
def async_logger(func):
    async def wrapper(*args, **kwargs):
        print("Starting async task")
        return await func(*args, **kwargs)
    return wrapper

```

Used in event-driven architectures.



---
**Score: 65**