---
title: Ch09 07 Decorators
date: 2025-12-18
author: Your Name
cell_count: 32
score: 30
---

# Chapter 9.7: Decorators in Python

This notebook covers Python decorators - functions that modify the behavior of other functions without changing their source code, enabling clean separation of concerns.

## 1. What is a Decorator

A decorator is a function that modifies the behavior of another function without changing its source code.


```python
# Basic decorator example
def my_decorator(func):
    def wrapper():
        print("Before function execution")
        func()
        print("After function execution")
    return wrapper

@my_decorator
def say_hello():
    print("Hello")

print("Calling decorated function:")
say_hello()

# Another example with different behavior
def debug_decorator(func):
    def wrapper():
        print(f"Calling function: {func.__name__}")
        result = func()
        print(f"Function {func.__name__} completed")
        return result
    return wrapper

@debug_decorator
def calculate():
    result = 2 + 2
    print(f"Calculation result: {result}")
    return result

print("\nCalling debug decorated function:")
output = calculate()
print(f"Returned value: {output}")
```

Decorators wrap additional logic around an existing function.

## 2. Decorator Without @ Syntax


```python
# Manual decorator application
def greet():
    print("Welcome")

print("Original function:")
greet()

# Apply decorator manually
greet = my_decorator(greet)

print("\nAfter manual decoration:")
greet()

# Demonstrate equivalence
def simple_func():
    print("Simple function")

# These two approaches are equivalent:
# Method 1: Using @ syntax
@my_decorator
def decorated_func1():
    print("Decorated function 1")

# Method 2: Manual application
def decorated_func2():
    print("Decorated function 2")

decorated_func2 = my_decorator(decorated_func2)

print("\nBoth methods produce same result:")
print("Method 1 (@decorator):")
decorated_func1()

print("\nMethod 2 (manual):")
decorated_func2()

# Show function names after decoration
print(f"\nFunction names after decoration:")
print(f"decorated_func1.__name__: {decorated_func1.__name__}")
print(f"decorated_func2.__name__: {decorated_func2.__name__}")
```

This demonstrates manual application of a decorator.

## 3. Decorator with Arguments


```python
# Decorator that handles function arguments
def log_decorator(func):
    def wrapper(*args, **kwargs):
        print(f"Function: {func.__name__}")
        print(f"Arguments: {args}")
        print(f"Keyword arguments: {kwargs}")
        result = func(*args, **kwargs)
        print(f"Result: {result}")
        return result
    return wrapper

@log_decorator
def add(a, b):
    return a + b

@log_decorator
def greet(name, greeting="Hello"):
    return f"{greeting}, {name}!"

print("Function with positional arguments:")
result1 = add(5, 3)

print("\nFunction with mixed arguments:")
result2 = greet("Alice", greeting="Hi")

print("\nFunction with keyword arguments:")
result3 = greet(name="Bob")

# Decorator for input validation
def validate_positive(func):
    def wrapper(*args, **kwargs):
        for arg in args:
            if isinstance(arg, (int, float)) and arg < 0:
                raise ValueError(f"Negative value not allowed: {arg}")
        return func(*args, **kwargs)
    return wrapper

@validate_positive
def square_root(x):
    return x ** 0.5

@validate_positive
def multiply(a, b):
    return a * b

print("\nValidation decorator:")
print(f"square_root(9): {square_root(9)}")
print(f"multiply(3, 4): {multiply(3, 4)}")

try:
    square_root(-4)
except ValueError as e:
    print(f"Validation error: {e}")
```

Handles flexible function signatures.

## 4. Chaining Multiple Decorators


```python
# Multiple decorators
def bold(func):
    def wrapper():
        print("<b>")
        func()
        print("</b>")
    return wrapper

def italic(func):
    def wrapper():
        print("<i>")
        func()
        print("</i>")
    return wrapper

def underline(func):
    def wrapper():
        print("<u>")
        func()
        print("</u>")
    return wrapper

@bold
@italic
@underline
def display():
    print("Text")

print("Chained decorators (bottom to top execution):")
display()

# Demonstrate execution order
def first_decorator(func):
    def wrapper():
        print("First decorator - before")
        func()
        print("First decorator - after")
    return wrapper

def second_decorator(func):
    def wrapper():
        print("Second decorator - before")
        func()
        print("Second decorator - after")
    return wrapper

def third_decorator(func):
    def wrapper():
        print("Third decorator - before")
        func()
        print("Third decorator - after")
    return wrapper

@first_decorator
@second_decorator
@third_decorator
def test_order():
    print("Original function")

print("\nExecution order demonstration:")
test_order()

# Practical example: HTTP response decorators
def add_headers(func):
    def wrapper(*args, **kwargs):
        result = func(*args, **kwargs)
        return f"Headers: Content-Type: application/json\n{result}"
    return wrapper

def add_status(func):
    def wrapper(*args, **kwargs):
        result = func(*args, **kwargs)
        return f"Status: 200 OK\n{result}"
    return wrapper

def add_timestamp(func):
    def wrapper(*args, **kwargs):
        import time
        result = func(*args, **kwargs)
        timestamp = time.strftime("%Y-%m-%d %H:%M:%S")
        return f"Timestamp: {timestamp}\n{result}"
    return wrapper

@add_headers
@add_status
@add_timestamp
def api_response():
    return "Body: {\"message\": \"Hello, World!\"}"

print("\nHTTP response with chained decorators:")
print(api_response())
```

Decorators execute from bottom to top order.

## 5. Decorator with Return Value


```python
# Transform return values
def uppercase(func):
    def wrapper(*args, **kwargs):
        result = func(*args, **kwargs)
        if isinstance(result, str):
            return result.upper()
        return result
    return wrapper

@uppercase
def message():
    return "hello world"

@uppercase
def get_name():
    return "alice"

print("Uppercase decorator:")
print(f"message(): {message()}")
print(f"get_name(): {get_name()}")

# Format numbers
def format_currency(func):
    def wrapper(*args, **kwargs):
        result = func(*args, **kwargs)
        if isinstance(result, (int, float)):
            return f"${result:.2f}"
        return result
    return wrapper

@format_currency
def calculate_price(base_price, tax_rate=0.1):
    return base_price * (1 + tax_rate)

@format_currency
def get_discount(original, discount_percent):
    return original * (discount_percent / 100)

print("\nCurrency formatting decorator:")
print(f"Price with tax: {calculate_price(100)}")
print(f"Discount amount: {get_discount(200, 15)}")

# Result caching decorator
def cache_result(func):
    cache = {}
    
    def wrapper(*args, **kwargs):
        # Create cache key
        key = str(args) + str(sorted(kwargs.items()))
        
        if key in cache:
            print(f"Cache hit for {func.__name__}")
            return cache[key]
        
        print(f"Cache miss for {func.__name__}")
        result = func(*args, **kwargs)
        cache[key] = result
        return result
    
    return wrapper

@cache_result
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n-1) + fibonacci(n-2)

@cache_result
def expensive_calculation(x, y):
    import time
    time.sleep(0.1)  # Simulate expensive operation
    return x ** y

print("\nCaching decorator:")
print(f"fibonacci(10): {fibonacci(10)}")
print(f"fibonacci(10) again: {fibonacci(10)}")

print(f"\nexpensive_calculation(2, 8): {expensive_calculation(2, 8)}")
print(f"expensive_calculation(2, 8) again: {expensive_calculation(2, 8)}")
```

Wraps and transforms return values.

## 6. Decorator Preserving Function Metadata


```python
from functools import wraps

# Decorator without @wraps (loses metadata)
def bad_decorator(func):
    def wrapper(*args, **kwargs):
        """This is the wrapper function"""
        return func(*args, **kwargs)
    return wrapper

# Decorator with @wraps (preserves metadata)
def good_decorator(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        """This is the wrapper function"""
        return func(*args, **kwargs)
    return wrapper

def original_function():
    """This is the original function"""
    return "original"

@bad_decorator
def bad_decorated_function():
    """This is the original function"""
    return "bad decorated"

@good_decorator
def good_decorated_function():
    """This is the original function"""
    return "good decorated"

print("Metadata comparison:")
print(f"Original function name: {original_function.__name__}")
print(f"Original function doc: {original_function.__doc__}")

print(f"\nBad decorated function name: {bad_decorated_function.__name__}")
print(f"Bad decorated function doc: {bad_decorated_function.__doc__}")

print(f"\nGood decorated function name: {good_decorated_function.__name__}")
print(f"Good decorated function doc: {good_decorated_function.__doc__}")

# Comprehensive metadata preservation example
def comprehensive_decorator(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__}")
        result = func(*args, **kwargs)
        print(f"Finished {func.__name__}")
        return result
    return wrapper

@comprehensive_decorator
def calculate_area(length, width):
    """Calculate the area of a rectangle.
    
    Args:
        length (float): The length of the rectangle
        width (float): The width of the rectangle
    
    Returns:
        float: The area of the rectangle
    """
    return length * width

print("\nComprehensive metadata preservation:")
print(f"Function name: {calculate_area.__name__}")
print(f"Function docstring: {calculate_area.__doc__}")
print(f"Function module: {calculate_area.__module__}")
print(f"Function annotations: {getattr(calculate_area, '__annotations__', {})}")

# Test the function
area = calculate_area(5, 3)
print(f"\nCalculated area: {area}")

# Help function works correctly with @wraps
print("\nHelp information:")
help(calculate_area)
```

`@wraps` preserves function name, docstring, and metadata.

## 7. Decorator for Timing Execution


```python
import time
from functools import wraps

# Basic timing decorator
def timer(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"{func.__name__} execution time: {end - start:.4f} seconds")
        return result
    return wrapper

@timer
def process_data():
    # Simulate processing
    total = 0
    for i in range(1000000):
        total += i
    return total

@timer
def slow_function():
    time.sleep(0.1)
    return "Done"

print("Basic timing decorator:")
result1 = process_data()
result2 = slow_function()

# Advanced timing decorator with statistics
def advanced_timer(func):
    times = []
    
    @wraps(func)
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        
        execution_time = end - start
        times.append(execution_time)
        
        print(f"{func.__name__} execution time: {execution_time:.4f}s")
        print(f"  Average: {sum(times)/len(times):.4f}s")
        print(f"  Min: {min(times):.4f}s, Max: {max(times):.4f}s")
        print(f"  Total calls: {len(times)}")
        
        return result
    
    # Add method to get statistics
    wrapper.get_stats = lambda: {
        'call_count': len(times),
        'total_time': sum(times),
        'average_time': sum(times) / len(times) if times else 0,
        'min_time': min(times) if times else 0,
        'max_time': max(times) if times else 0
    }
    
    return wrapper

@advanced_timer
def fibonacci_recursive(n):
    if n <= 1:
        return n
    return fibonacci_recursive(n-1) + fibonacci_recursive(n-2)

print("\nAdvanced timing decorator:")
for i in range(3):
    result = fibonacci_recursive(20)
    print(f"Fibonacci(20) = {result}")
    print()

print(f"Final statistics: {fibonacci_recursive.get_stats()}")

# Performance profiler decorator
def profile(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        import cProfile
        import pstats
        import io
        
        pr = cProfile.Profile()
        pr.enable()
        
        result = func(*args, **kwargs)
        
        pr.disable()
        s = io.StringIO()
        ps = pstats.Stats(pr, stream=s).sort_stats('cumulative')
        ps.print_stats(10)  # Top 10 functions
        
        print(f"\nProfile for {func.__name__}:")
        print(s.getvalue())
        
        return result
    return wrapper

@profile
def complex_calculation():
    # Some complex calculation
    result = []
    for i in range(1000):
        result.append(sum(range(i)))
    return len(result)

print("\nProfiling decorator:")
complex_result = complex_calculation()
```

Used for performance profiling.

## 8. Decorator with Parameters


```python
# Parameterized decorator (decorator factory)
def repeat(n):
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            for i in range(n):
                print(f"Execution {i+1}:")
                result = func(*args, **kwargs)
            return result  # Return result from last execution
        return wrapper
    return decorator

@repeat(3)
def greet(name):
    print(f"Hello, {name}!")
    return f"Greeted {name}"

print("Repeat decorator:")
result = greet("Alice")
print(f"Final result: {result}")

# Retry decorator with parameters
def retry(max_attempts=3, delay=1, exceptions=(Exception,)):
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            for attempt in range(max_attempts):
                try:
                    return func(*args, **kwargs)
                except exceptions as e:
                    if attempt == max_attempts - 1:
                        print(f"All {max_attempts} attempts failed")
                        raise e
                    print(f"Attempt {attempt + 1} failed: {e}. Retrying in {delay}s...")
                    time.sleep(delay)
        return wrapper
    return decorator

# Simulate unreliable function
import random

@retry(max_attempts=5, delay=0.1, exceptions=(ValueError, ConnectionError))
def unreliable_network_call():
    if random.random() < 0.7:  # 70% chance of failure
        raise ConnectionError("Network timeout")
    return "Success: Data retrieved"

print("\nRetry decorator:")
try:
    result = unreliable_network_call()
    print(f"Result: {result}")
except ConnectionError as e:
    print(f"Final failure: {e}")

# Rate limiting decorator
def rate_limit(calls_per_second=1):
    def decorator(func):
        last_called = [0]  # Use list to make it mutable
        
        @wraps(func)
        def wrapper(*args, **kwargs):
            current_time = time.time()
            time_since_last = current_time - last_called[0]
            min_interval = 1.0 / calls_per_second
            
            if time_since_last < min_interval:
                sleep_time = min_interval - time_since_last
                print(f"Rate limiting: sleeping for {sleep_time:.2f}s")
                time.sleep(sleep_time)
            
            last_called[0] = time.time()
            return func(*args, **kwargs)
        return wrapper
    return decorator

@rate_limit(calls_per_second=2)  # Max 2 calls per second
def api_call(endpoint):
    print(f"Making API call to {endpoint}")
    return f"Response from {endpoint}"

print("\nRate limiting decorator:")
for i in range(3):
    result = api_call(f"/endpoint{i}")
    print(f"Result: {result}")

# Validation decorator with parameters
def validate_types(**type_checks):
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            # Get function signature
            import inspect
            sig = inspect.signature(func)
            bound_args = sig.bind(*args, **kwargs)
            bound_args.apply_defaults()
            
            # Validate types
            for param_name, expected_type in type_checks.items():
                if param_name in bound_args.arguments:
                    value = bound_args.arguments[param_name]
                    if not isinstance(value, expected_type):
                        raise TypeError(
                            f"Parameter '{param_name}' must be of type {expected_type.__name__}, "
                            f"got {type(value).__name__}"
                        )
            
            return func(*args, **kwargs)
        return wrapper
    return decorator

@validate_types(name=str, age=int, salary=float)
def create_employee(name, age, salary=0.0):
    return f"Employee: {name}, Age: {age}, Salary: ${salary}"

print("\nType validation decorator:")
print(create_employee("Alice", 30, 50000.0))

try:
    create_employee("Bob", "thirty", 60000.0)  # Invalid age type
except TypeError as e:
    print(f"Validation error: {e}")
```

Supports configurable decorator logic.

## 9. Class-Based Decorator


```python
# Basic class-based decorator
class Logger:
    def __init__(self, func):
        self.func = func
        self.call_count = 0
    
    def __call__(self, *args, **kwargs):
        self.call_count += 1
        print(f"Call #{self.call_count} to {self.func.__name__}")
        result = self.func(*args, **kwargs)
        print(f"Finished call #{self.call_count}")
        return result

@Logger
def show_data(data):
    print(f"Processing data: {data}")
    return f"Processed: {data}"

print("Class-based decorator:")
result1 = show_data("first")
result2 = show_data("second")
print(f"Total calls to show_data: {show_data.call_count}")

# Parameterized class-based decorator
class TimedCache:
    def __init__(self, ttl_seconds=60):
        self.ttl_seconds = ttl_seconds
        self.cache = {}
    
    def __call__(self, func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            # Create cache key
            key = str(args) + str(sorted(kwargs.items()))
            current_time = time.time()
            
            # Check if cached result is still valid
            if key in self.cache:
                cached_time, cached_result = self.cache[key]
                if current_time - cached_time < self.ttl_seconds:
                    print(f"Cache hit for {func.__name__} (age: {current_time - cached_time:.1f}s)")
                    return cached_result
                else:
                    print(f"Cache expired for {func.__name__}")
                    del self.cache[key]
            
            # Execute function and cache result
            print(f"Cache miss for {func.__name__}")
            result = func(*args, **kwargs)
            self.cache[key] = (current_time, result)
            return result
        
        return wrapper

@TimedCache(ttl_seconds=2)  # Cache for 2 seconds
def expensive_operation(x):
    time.sleep(0.1)  # Simulate expensive operation
    return x ** 2

print("\nTimed cache decorator:")
print(f"Result 1: {expensive_operation(5)}")
print(f"Result 2: {expensive_operation(5)}")  # Should be cached
time.sleep(2.1)  # Wait for cache to expire
print(f"Result 3: {expensive_operation(5)}")  # Should be cache miss

# Access control class decorator
class RequireRole:
    def __init__(self, required_role):
        self.required_role = required_role
    
    def __call__(self, func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            # In a real application, you'd get the current user from session/context
            current_user = getattr(wrapper, '_current_user', None)
            
            if not current_user:
                return "Error: No user logged in"
            
            user_roles = current_user.get('roles', [])
            if self.required_role not in user_roles:
                return f"Error: Requires {self.required_role} role"
            
            return func(*args, **kwargs)
        
        return wrapper

@RequireRole('admin')
def delete_user(user_id):
    return f"User {user_id} deleted"

@RequireRole('moderator')
def ban_user(user_id):
    return f"User {user_id} banned"

print("\nRole-based access control:")
print(delete_user(123))  # Should fail - no user

# Set current user
delete_user._current_user = {'name': 'Alice', 'roles': ['user']}
ban_user._current_user = {'name': 'Bob', 'roles': ['moderator', 'user']}

print(delete_user(123))  # Should fail - insufficient role
print(ban_user(456))     # Should succeed

# Update Alice's role
delete_user._current_user = {'name': 'Alice', 'roles': ['admin', 'user']}
print(delete_user(123))  # Should succeed now

# Statistics collector decorator
class FunctionStats:
    def __init__(self, func):
        self.func = func
        self.calls = 0
        self.total_time = 0
        self.errors = 0
        self.last_result = None
    
    def __call__(self, *args, **kwargs):
        self.calls += 1
        start_time = time.time()
        
        try:
            result = self.func(*args, **kwargs)
            self.last_result = result
            return result
        except Exception as e:
            self.errors += 1
            raise e
        finally:
            self.total_time += time.time() - start_time
    
    def get_stats(self):
        return {
            'function_name': self.func.__name__,
            'total_calls': self.calls,
            'total_time': self.total_time,
            'average_time': self.total_time / self.calls if self.calls > 0 else 0,
            'error_count': self.errors,
            'success_rate': (self.calls - self.errors) / self.calls if self.calls > 0 else 0,
            'last_result': self.last_result
        }

@FunctionStats
def risky_calculation(x):
    if x < 0:
        raise ValueError("Negative values not allowed")
    time.sleep(0.01)  # Simulate work
    return x ** 0.5

print("\nFunction statistics decorator:")
for value in [4, 9, -1, 16, -2, 25]:
    try:
        result = risky_calculation(value)
        print(f"sqrt({value}) = {result:.2f}")
    except ValueError as e:
        print(f"Error with {value}: {e}")

print(f"\nFinal statistics: {risky_calculation.get_stats()}")
```

Implements decorators using classes.

## 10. Real-World Decorator Example (Authentication)


```python
# Authentication decorator
def require_login(func):
    @wraps(func)
    def wrapper(user, *args, **kwargs):
        if not user.get("authenticated"):
            return "Access Denied: Please log in"
        return func(user, *args, **kwargs)
    return wrapper

@require_login
def view_profile(user):
    return f"Welcome to your profile, {user['name']}!"

@require_login
def update_settings(user, setting, value):
    return f"Updated {setting} to {value} for {user['name']}"

# Test users
authenticated_user = {"name": "Alice", "authenticated": True}
unauthenticated_user = {"name": "Bob", "authenticated": False}

print("Authentication decorator:")
print(view_profile(authenticated_user))
print(view_profile(unauthenticated_user))
print(update_settings(authenticated_user, "theme", "dark"))

# Authorization decorator (role-based)
def require_permission(permission):
    def decorator(func):
        @wraps(func)
        def wrapper(user, *args, **kwargs):
            if not user.get("authenticated"):
                return "Access Denied: Please log in"
            
            user_permissions = user.get("permissions", [])
            if permission not in user_permissions:
                return f"Access Denied: Requires '{permission}' permission"
            
            return func(user, *args, **kwargs)
        return wrapper
    return decorator

@require_permission('admin')
def delete_user_account(user, target_user_id):
    return f"Admin {user['name']} deleted user {target_user_id}"

@require_permission('moderator')
def moderate_content(user, content_id):
    return f"Moderator {user['name']} reviewed content {content_id}"

@require_permission('read')
def view_reports(user):
    return f"Showing reports to {user['name']}"

# Test users with different permissions
admin_user = {
    "name": "Admin Alice", 
    "authenticated": True, 
    "permissions": ["admin", "moderator", "read"]
}

moderator_user = {
    "name": "Mod Bob", 
    "authenticated": True, 
    "permissions": ["moderator", "read"]
}

regular_user = {
    "name": "User Charlie", 
    "authenticated": True, 
    "permissions": ["read"]
}

print("\nAuthorization decorator:")
print(delete_user_account(admin_user, 123))
print(delete_user_account(moderator_user, 123))
print(moderate_content(moderator_user, 456))
print(moderate_content(regular_user, 456))
print(view_reports(regular_user))

# API rate limiting and authentication combined
def api_endpoint(rate_limit_per_minute=60, require_auth=True):
    def decorator(func):
        # Rate limiting state
        call_times = []
        
        @wraps(func)
        def wrapper(request, *args, **kwargs):
            current_time = time.time()
            
            # Authentication check
            if require_auth:
                user = request.get('user')
                if not user or not user.get('authenticated'):
                    return {"error": "Authentication required", "status": 401}
            
            # Rate limiting check
            # Remove calls older than 1 minute
            call_times[:] = [t for t in call_times if current_time - t < 60]
            
            if len(call_times) >= rate_limit_per_minute:
                return {"error": "Rate limit exceeded", "status": 429}
            
            call_times.append(current_time)
            
            # Execute the API function
            try:
                result = func(request, *args, **kwargs)
                return {"data": result, "status": 200}
            except Exception as e:
                return {"error": str(e), "status": 500}
        
        return wrapper
    return decorator

@api_endpoint(rate_limit_per_minute=3, require_auth=True)
def get_user_data(request, user_id):
    return f"User data for ID {user_id}"

@api_endpoint(rate_limit_per_minute=10, require_auth=False)
def get_public_info(request):
    return "Public information available to all"

# Simulate API requests
authenticated_request = {
    "user": {"name": "API User", "authenticated": True}
}

unauthenticated_request = {}

print("\nAPI endpoint decorator:")
print(get_user_data(authenticated_request, 123))
print(get_user_data(unauthenticated_request, 123))
print(get_public_info(unauthenticated_request))

# Test rate limiting
print("\nTesting rate limiting:")
for i in range(5):
    result = get_user_data(authenticated_request, i)
    print(f"Request {i+1}: {result}")

# Audit logging decorator
def audit_log(action_type):
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            # Extract user info (assuming first arg is user)
            user = args[0] if args else {"name": "Unknown"}
            user_name = user.get("name", "Unknown") if isinstance(user, dict) else str(user)
            
            # Log the action
            timestamp = time.strftime("%Y-%m-%d %H:%M:%S")
            print(f"[AUDIT] {timestamp} - User '{user_name}' performed '{action_type}' via {func.__name__}")
            
            try:
                result = func(*args, **kwargs)
                print(f"[AUDIT] {timestamp} - Action '{action_type}' completed successfully")
                return result
            except Exception as e:
                print(f"[AUDIT] {timestamp} - Action '{action_type}' failed: {e}")
                raise
        return wrapper
    return decorator

@require_login
@audit_log("profile_update")
def update_user_profile(user, **updates):
    return f"Profile updated for {user['name']}: {updates}"

@require_permission('admin')
@audit_log("user_deletion")
def delete_user(user, target_id):
    return f"User {target_id} deleted by admin {user['name']}"

print("\nAudit logging decorator:")
result = update_user_profile(authenticated_user, email="new@example.com", phone="123-456-7890")
print(f"Result: {result}")

result = delete_user(admin_user, 999)
print(f"Result: {result}")
```

Encapsulates cross-cutting concerns like security and validation.

## Summary

Python decorators provide:
- **Clean separation of concerns** by wrapping functionality
- **Reusable cross-cutting logic** like logging, timing, authentication
- **Function modification** without changing source code
- **Flexible parameterization** through decorator factories
- **Metadata preservation** using `@wraps`

**Key concepts:**
- **Decorator**: Function that takes a function and returns a modified function
- **Wrapper function**: Inner function that adds behavior around the original
- **@syntax**: Syntactic sugar for applying decorators
- **Decorator factory**: Function that returns a decorator (for parameters)
- **Class decorators**: Using classes with `__call__` method

**Common use cases:**
- Authentication and authorization
- Logging and monitoring
- Performance timing and profiling
- Caching and memoization
- Input validation and type checking
- Rate limiting and throttling
- Retry logic and error handling
- API endpoint decoration

**Best practices:**
- Use `@wraps` to preserve function metadata
- Handle `*args` and `**kwargs` for flexible signatures
- Keep decorator logic focused and single-purpose
- Use decorator factories for parameterized decorators
- Consider class-based decorators for stateful behavior
- Chain decorators thoughtfully (bottom-to-top execution)
- Document decorator behavior and side effects


---
**Score: 30**