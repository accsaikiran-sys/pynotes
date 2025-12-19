---
title: Ch09 06 Closures
date: 2025-12-18
author: Your Name
cell_count: 32
score: 30
---

# Chapter 9.2: Closures in Python

This notebook covers Python closures - functions that remember and have access to variables from their enclosing scope even after the outer function has finished execution.

## 1. What is a Closure

A closure is a function that remembers and has access to variables from its enclosing scope even after the outer function has finished execution.


```python
# Basic closure example
def outer():
    message = "Hello"  # Variable in enclosing scope
    
    def inner():
        return message  # Access to enclosing variable
    
    return inner

# Create closure
func = outer()
print(func())  # Output: Hello

# Demonstrate that outer() has finished but inner() still has access
print(f"Function name: {func.__name__}")
print(f"Has closure: {func.__closure__ is not None}")

# Multiple calls to outer() create different closures
def create_greeter(greeting):
    def greet(name):
        return f"{greeting}, {name}!"
    return greet

hello_greeter = create_greeter("Hello")
hi_greeter = create_greeter("Hi")

print("\nDifferent greetings:")
print(hello_greeter("Alice"))  # Hello, Alice!
print(hi_greeter("Bob"))       # Hi, Bob!
```

The inner function retains access to `message`.

## 2. Basic Closure Structure


```python
# Closure with parameter
def multiplier(x):
    def multiply(y):
        return x * y  # x is captured from enclosing scope
    return multiply

# Create different multipliers
times2 = multiplier(2)
times3 = multiplier(3)
times10 = multiplier(10)

print("Multiplier closures:")
print(f"times2(5) = {times2(5)}")    # 10
print(f"times3(5) = {times3(5)}")    # 15
print(f"times10(5) = {times10(5)}")  # 50

# Power function closure
def power_function(exponent):
    def power(base):
        return base ** exponent
    return power

square = power_function(2)
cube = power_function(3)

print("\nPower function closures:")
print(f"square(4) = {square(4)}")  # 16
print(f"cube(3) = {cube(3)}")      # 27

# String formatter closure
def create_formatter(template):
    def format_string(value):
        return template.format(value)
    return format_string

currency_formatter = create_formatter("${:.2f}")
percentage_formatter = create_formatter("{:.1f}%")

print("\nFormatter closures:")
print(currency_formatter(123.456))    # $123.46
print(percentage_formatter(0.789))    # 0.8%
```

Functions carry state without using global variables.

## 3. Closure Retaining State


```python
# Counter closure with persistent state
def counter():
    count = 0  # Enclosing variable
    
    def increment():
        nonlocal count
        count += 1
        return count
    
    return increment

# Create independent counters
c1 = counter()
c2 = counter()

print("Independent counters:")
print(f"c1(): {c1()}")  # 1
print(f"c1(): {c1()}")  # 2
print(f"c2(): {c2()}")  # 1 (independent state)
print(f"c1(): {c1()}")  # 3
print(f"c2(): {c2()}")  # 2

# Bank account closure
def create_account(initial_balance):
    balance = initial_balance
    
    def deposit(amount):
        nonlocal balance
        balance += amount
        return balance
    
    def withdraw(amount):
        nonlocal balance
        if balance >= amount:
            balance -= amount
            return balance
        else:
            return f"Insufficient funds. Balance: {balance}"
    
    def get_balance():
        return balance
    
    # Return multiple functions
    return deposit, withdraw, get_balance

# Create account
deposit, withdraw, get_balance = create_account(1000)

print("\nBank account closure:")
print(f"Initial balance: {get_balance()}")
print(f"After deposit(200): {deposit(200)}")
print(f"After withdraw(150): {withdraw(150)}")
print(f"Try withdraw(2000): {withdraw(2000)}")
print(f"Final balance: {get_balance()}")

# Statistics accumulator
def create_stats_accumulator():
    values = []
    
    def add_value(value):
        values.append(value)
        return len(values)
    
    def get_stats():
        if not values:
            return {"count": 0, "sum": 0, "avg": 0}
        return {
            "count": len(values),
            "sum": sum(values),
            "avg": sum(values) / len(values),
            "min": min(values),
            "max": max(values)
        }
    
    return add_value, get_stats

add_value, get_stats = create_stats_accumulator()

print("\nStats accumulator:")
add_value(10)
add_value(20)
add_value(15)
print(f"Stats: {get_stats()}")
```

Closure maintains persistent state across calls.

## 4. nonlocal in Closures


```python
# Power with incrementing exponent
def power(base):
    exponent = 2  # Initial exponent
    
    def calculate():
        nonlocal exponent
        result = base ** exponent
        exponent += 1  # Increment for next call
        return result
    
    return calculate

p = power(2)
print("Power with incrementing exponent:")
print(f"First call: 2^2 = {p()}")   # 4
print(f"Second call: 2^3 = {p()}")  # 8
print(f"Third call: 2^4 = {p()}")   # 16

# Configuration manager
def create_config_manager(initial_config):
    config = initial_config.copy()
    
    def get_config(key, default=None):
        return config.get(key, default)
    
    def set_config(key, value):
        nonlocal config
        config[key] = value
    
    def update_config(updates):
        nonlocal config
        config.update(updates)
    
    def get_all_config():
        return config.copy()
    
    return get_config, set_config, update_config, get_all_config

# Create config manager
get_config, set_config, update_config, get_all_config = create_config_manager({
    'debug': True,
    'max_connections': 100
})

print("\nConfiguration manager:")
print(f"Initial config: {get_all_config()}")
print(f"Debug setting: {get_config('debug')}")

set_config('timeout', 30)
update_config({'debug': False, 'max_connections': 200})
print(f"Updated config: {get_all_config()}")

# Rate limiter
import time

def create_rate_limiter(max_calls, time_window):
    calls = []
    
    def is_allowed():
        nonlocal calls
        current_time = time.time()
        
        # Remove old calls outside the time window
        calls = [call_time for call_time in calls 
                if current_time - call_time < time_window]
        
        if len(calls) < max_calls:
            calls.append(current_time)
            return True
        return False
    
    def get_status():
        current_time = time.time()
        recent_calls = [call_time for call_time in calls 
                       if current_time - call_time < time_window]
        return {
            'calls_made': len(recent_calls),
            'calls_remaining': max_calls - len(recent_calls),
            'window_seconds': time_window
        }
    
    return is_allowed, get_status

# Create rate limiter (3 calls per 5 seconds)
is_allowed, get_status = create_rate_limiter(3, 5)

print("\nRate limiter demo:")
for i in range(5):
    if is_allowed():
        print(f"Call {i+1}: Allowed")
    else:
        print(f"Call {i+1}: Rate limited")
    print(f"  Status: {get_status()}")
```

`nonlocal` allows modification of enclosed variables.

## 5. Closure vs Global Variable


```python
# Global variable approach (problematic)
factor = 10

def using_global():
    return lambda x: x * factor

# Closure approach (better)
def using_closure():
    factor = 10  # Encapsulated in closure
    return lambda x: x * factor

# Create functions
global_func = using_global()
closure_func = using_closure()

print("Initial results:")
print(f"Global function: {global_func(5)}")   # 50
print(f"Closure function: {closure_func(5)}") # 50

# Modify global variable
factor = 20

print("\nAfter changing global factor to 20:")
print(f"Global function: {global_func(5)}")   # 100 (affected!)
print(f"Closure function: {closure_func(5)}") # 50 (unaffected)

# Demonstrate isolation with multiple closures
def create_isolated_multiplier(factor):
    def multiply(x):
        return x * factor
    return multiply

mult_by_2 = create_isolated_multiplier(2)
mult_by_5 = create_isolated_multiplier(5)
mult_by_10 = create_isolated_multiplier(10)

print("\nIsolated multipliers:")
print(f"mult_by_2(3) = {mult_by_2(3)}")   # 6
print(f"mult_by_5(3) = {mult_by_5(3)}")   # 15
print(f"mult_by_10(3) = {mult_by_10(3)}") # 30

# Problem with shared mutable state
shared_list = []

def bad_list_appender():
    return lambda x: shared_list.append(x)

def good_list_appender():
    my_list = []  # Private to this closure
    def append_and_return(x):
        my_list.append(x)
        return my_list.copy()
    return append_and_return

bad_append = bad_list_appender()
good_append1 = good_list_appender()
good_append2 = good_list_appender()

print("\nList appender comparison:")
bad_append(1)
bad_append(2)
print(f"Shared list after bad_append: {shared_list}")

print(f"good_append1(1): {good_append1(1)}")
print(f"good_append1(2): {good_append1(2)}")
print(f"good_append2(10): {good_append2(10)}")
print(f"good_append2(20): {good_append2(20)}")
```

Closures prevent unintended side-effects on global state.

## 6. Multiple Closures from Same Function


```python
# Basic adder function
def make_adder(x):
    def adder(y):
        return x + y
    return adder

# Create multiple independent adders
add5 = make_adder(5)
add10 = make_adder(10)
add100 = make_adder(100)

print("Multiple adders:")
print(f"add5(3) = {add5(3)}")     # 8
print(f"add10(3) = {add10(3)}")   # 13
print(f"add100(3) = {add100(3)}") # 103

# Validator factory
def create_validator(min_val, max_val):
    def validate(value):
        if value < min_val:
            return f"Value {value} is below minimum {min_val}"
        elif value > max_val:
            return f"Value {value} is above maximum {max_val}"
        else:
            return f"Value {value} is valid"
    return validate

# Create different validators
age_validator = create_validator(0, 120)
percentage_validator = create_validator(0, 100)
temperature_validator = create_validator(-273, 1000)

print("\nValidators:")
print(age_validator(25))        # Valid
print(age_validator(-5))        # Below minimum
print(percentage_validator(150)) # Above maximum
print(temperature_validator(25)) # Valid

# Timer factory
def create_timer(name):
    start_time = None
    
    def start():
        nonlocal start_time
        start_time = time.time()
        print(f"Timer '{name}' started")
    
    def stop():
        if start_time is None:
            return f"Timer '{name}' was not started"
        elapsed = time.time() - start_time
        return f"Timer '{name}' elapsed: {elapsed:.4f} seconds"
    
    return start, stop

# Create multiple timers
start_timer1, stop_timer1 = create_timer("Process A")
start_timer2, stop_timer2 = create_timer("Process B")

print("\nTimer example:")
start_timer1()
time.sleep(0.1)  # Simulate work
print(stop_timer1())

start_timer2()
time.sleep(0.05)  # Different work duration
print(stop_timer2())

# Cache factory
def create_cache(max_size=100):
    cache = {}
    access_order = []
    
    def get(key):
        if key in cache:
            # Move to end (most recently used)
            access_order.remove(key)
            access_order.append(key)
            return cache[key]
        return None
    
    def put(key, value):
        nonlocal cache, access_order
        
        if key in cache:
            access_order.remove(key)
        elif len(cache) >= max_size:
            # Remove least recently used
            oldest = access_order.pop(0)
            del cache[oldest]
        
        cache[key] = value
        access_order.append(key)
    
    def stats():
        return {
            'size': len(cache),
            'max_size': max_size,
            'keys': list(cache.keys())
        }
    
    return get, put, stats

# Create independent caches
get1, put1, stats1 = create_cache(max_size=2)
get2, put2, stats2 = create_cache(max_size=3)

print("\nCache example:")
put1('a', 1)
put1('b', 2)
print(f"Cache 1 stats: {stats1()}")

put2('x', 10)
put2('y', 20)
put2('z', 30)
print(f"Cache 2 stats: {stats2()}")

print(f"Cache 1 get 'a': {get1('a')}")
print(f"Cache 2 get 'y': {get2('y')}")
```

Each closure holds its own independent environment.

## 7. Inspecting Closure Variables


```python
# Basic closure inspection
def outer():
    value = 42
    name = "closure"
    
    def inner():
        return f"{name}: {value}"
    
    return inner

func = outer()

print("Closure inspection:")
print(f"Function name: {func.__name__}")
print(f"Has closure: {func.__closure__ is not None}")

if func.__closure__:
    print(f"Number of closure variables: {len(func.__closure__)}")
    for i, cell in enumerate(func.__closure__):
        print(f"  Variable {i}: {cell.cell_contents}")

# More detailed inspection
def create_complex_closure(a, b, c):
    x = a * 2
    y = b + 10
    z = c
    
    def compute():
        return x + y + z
    
    return compute

complex_func = create_complex_closure(5, 3, 7)

print("\nComplex closure inspection:")
print(f"Result: {complex_func()}")
print(f"Closure variables:")
for i, cell in enumerate(complex_func.__closure__):
    print(f"  Cell {i}: {cell.cell_contents}")

# Inspect closure with code object
print(f"\nCode object info:")
code = complex_func.__code__
print(f"Free variables: {code.co_freevars}")
print(f"Variable names: {code.co_varnames}")

# Utility function for closure inspection
def inspect_closure(func):
    """Utility to inspect closure details"""
    print(f"\nInspecting function: {func.__name__}")
    
    if func.__closure__ is None:
        print("  No closure (not a closure function)")
        return
    
    print(f"  Closure variables: {len(func.__closure__)}")
    
    # Get variable names from code object
    free_vars = func.__code__.co_freevars
    
    for i, (name, cell) in enumerate(zip(free_vars, func.__closure__)):
        try:
            value = cell.cell_contents
            print(f"    {name}: {value} (type: {type(value).__name__})")
        except ValueError:
            print(f"    {name}: <empty cell>")

# Test the inspection utility
def test_closure(message, count):
    def repeat():
        return message * count
    return repeat

test_func = test_closure("Hello ", 3)
inspect_closure(test_func)

# Regular function (no closure)
def regular_function():
    return "I'm not a closure"

inspect_closure(regular_function)
```

Shows internal structure of closure data.

## 8. Closures as Function Factories


```python
# Logger factory
def logger(prefix):
    def log(message):
        timestamp = time.strftime("%Y-%m-%d %H:%M:%S")
        print(f"[{timestamp}] {prefix}: {message}")
    return log

# Create specialized loggers
info_logger = logger("INFO")
error_logger = logger("ERROR")
debug_logger = logger("DEBUG")

print("Logger factory example:")
info_logger("System started")
error_logger("Database connection failed")
debug_logger("Processing user request")

# HTTP client factory
def create_http_client(base_url, headers=None):
    default_headers = headers or {}
    
    def get(endpoint):
        url = f"{base_url.rstrip('/')}/{endpoint.lstrip('/')}"
        return f"GET {url} with headers {default_headers}"
    
    def post(endpoint, data):
        url = f"{base_url.rstrip('/')}/{endpoint.lstrip('/')}"
        return f"POST {url} with data {data} and headers {default_headers}"
    
    return get, post

# Create API clients
api_get, api_post = create_http_client(
    "https://api.example.com",
    {"Authorization": "Bearer token123"}
)

print("\nHTTP client factory:")
print(api_get("users"))
print(api_post("users", {"name": "Alice"}))

# Database query builder factory
def create_query_builder(table_name):
    def select(columns="*", where=None):
        query = f"SELECT {columns} FROM {table_name}"
        if where:
            query += f" WHERE {where}"
        return query
    
    def insert(data):
        columns = ", ".join(data.keys())
        values = ", ".join([f"'{v}'" for v in data.values()])
        return f"INSERT INTO {table_name} ({columns}) VALUES ({values})"
    
    def update(data, where):
        set_clause = ", ".join([f"{k}='{v}'" for k, v in data.items()])
        return f"UPDATE {table_name} SET {set_clause} WHERE {where}"
    
    def delete(where):
        return f"DELETE FROM {table_name} WHERE {where}"
    
    return select, insert, update, delete

# Create table-specific query builders
user_select, user_insert, user_update, user_delete = create_query_builder("users")
product_select, product_insert, product_update, product_delete = create_query_builder("products")

print("\nQuery builder factory:")
print(user_select("name, email", "age > 18"))
print(user_insert({"name": "Alice", "email": "alice@example.com"}))
print(product_select(where="price < 100"))

# Event handler factory
def create_event_handler(event_type, callback):
    def handle_event(data):
        print(f"Handling {event_type} event")
        return callback(data)
    
    # Add metadata
    handle_event.event_type = event_type
    handle_event.callback = callback
    
    return handle_event

# Create event handlers
def user_created_callback(data):
    return f"Welcome {data.get('name', 'User')}!"

def order_placed_callback(data):
    return f"Order #{data.get('id')} for ${data.get('amount')} placed"

user_handler = create_event_handler("user_created", user_created_callback)
order_handler = create_event_handler("order_placed", order_placed_callback)

print("\nEvent handler factory:")
print(user_handler({"name": "Alice"}))
print(order_handler({"id": "12345", "amount": 99.99}))
print(f"User handler type: {user_handler.event_type}")
print(f"Order handler type: {order_handler.event_type}")
```

Closures generate specialized functions dynamically.

## 9. Closure in Decorators (Foundation Pattern)


```python
# Basic decorator using closure
def my_decorator(func):
    def wrapper(*args, **kwargs):
        print("Before execution")
        result = func(*args, **kwargs)
        print("After execution")
        return result
    return wrapper

@my_decorator
def greet(name):
    return f"Hello, {name}!"

print("Basic decorator:")
result = greet("Alice")
print(f"Result: {result}")

# Timing decorator
def timing_decorator(func):
    def wrapper(*args, **kwargs):
        start_time = time.time()
        result = func(*args, **kwargs)
        end_time = time.time()
        print(f"{func.__name__} took {end_time - start_time:.4f} seconds")
        return result
    return wrapper

@timing_decorator
def slow_function():
    time.sleep(0.1)
    return "Done"

print("\nTiming decorator:")
slow_function()

# Parameterized decorator (decorator factory)
def retry_decorator(max_attempts=3, delay=1):
    def decorator(func):
        def wrapper(*args, **kwargs):
            for attempt in range(max_attempts):
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    if attempt == max_attempts - 1:
                        raise e
                    print(f"Attempt {attempt + 1} failed: {e}. Retrying in {delay}s...")
                    time.sleep(delay)
        return wrapper
    return decorator

@retry_decorator(max_attempts=2, delay=0.1)
def unreliable_function(should_fail=True):
    if should_fail:
        raise ValueError("Something went wrong")
    return "Success!"

print("\nRetry decorator:")
try:
    unreliable_function()
except ValueError as e:
    print(f"Final failure: {e}")

# Caching decorator
def cache_decorator(func):
    cache = {}  # Closure variable
    
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
    
    # Add cache inspection methods
    wrapper.cache = cache
    wrapper.cache_info = lambda: {"size": len(cache), "keys": list(cache.keys())}
    wrapper.cache_clear = lambda: cache.clear()
    
    return wrapper

@cache_decorator
def expensive_calculation(n):
    time.sleep(0.1)  # Simulate expensive operation
    return n ** 2

print("\nCaching decorator:")
print(f"Result: {expensive_calculation(5)}")
print(f"Result: {expensive_calculation(5)}")  # Should be cached
print(f"Cache info: {expensive_calculation.cache_info()}")

# Access control decorator
def require_permission(permission):
    def decorator(func):
        def wrapper(*args, **kwargs):
            # Simulate user context (in real app, get from session/token)
            user_permissions = getattr(wrapper, '_user_permissions', [])
            
            if permission not in user_permissions:
                return f"Access denied: {permission} permission required"
            
            return func(*args, **kwargs)
        
        wrapper.required_permission = permission
        wrapper._user_permissions = []  # Default empty permissions
        return wrapper
    return decorator

@require_permission("admin")
def delete_user(user_id):
    return f"User {user_id} deleted"

@require_permission("read")
def get_user(user_id):
    return f"User {user_id} data"

print("\nAccess control decorator:")
print(delete_user(123))  # Should fail

# Grant permissions
delete_user._user_permissions = ["admin"]
get_user._user_permissions = ["read"]

print(delete_user(123))  # Should succeed
print(get_user(456))     # Should succeed
```

Decorators rely on closures to extend function behaviour.

## 10. Real-World Closure Example (Configuration)


```python
# Threshold checker
def threshold_checker(threshold):
    def check(value):
        return value > threshold
    return check

# Create different threshold checkers
high_temp = threshold_checker(40)
low_temp = threshold_checker(0)
high_score = threshold_checker(90)

print("Threshold checkers:")
print(f"high_temp(35): {high_temp(35)}")   # False
print(f"high_temp(45): {high_temp(45)}")   # True
print(f"low_temp(-5): {low_temp(-5)}")     # False
print(f"high_score(95): {high_score(95)}") # True

# Configuration-based service factory
def create_service(config):
    base_url = config.get('base_url', 'http://localhost')
    timeout = config.get('timeout', 30)
    retry_count = config.get('retry_count', 3)
    api_key = config.get('api_key', '')
    
    def make_request(endpoint, method='GET', data=None):
        headers = {'Authorization': f'Bearer {api_key}'} if api_key else {}
        url = f"{base_url}/{endpoint.lstrip('/')}"
        
        for attempt in range(retry_count):
            try:
                # Simulate API call
                print(f"Attempt {attempt + 1}: {method} {url}")
                print(f"  Headers: {headers}")
                print(f"  Timeout: {timeout}s")
                if data:
                    print(f"  Data: {data}")
                
                # Simulate success after first attempt
                if attempt == 0:
                    return {"status": "success", "data": f"Response from {endpoint}"}
                
            except Exception as e:
                if attempt == retry_count - 1:
                    raise e
                print(f"  Retry {attempt + 1} failed, retrying...")
        
        return {"status": "error", "message": "Max retries exceeded"}
    
    def get_config():
        return {
            'base_url': base_url,
            'timeout': timeout,
            'retry_count': retry_count,
            'has_api_key': bool(api_key)
        }
    
    return make_request, get_config

# Create different service instances
dev_config = {
    'base_url': 'http://dev-api.example.com',
    'timeout': 10,
    'retry_count': 1,
    'api_key': 'dev-key-123'
}

prod_config = {
    'base_url': 'https://api.example.com',
    'timeout': 30,
    'retry_count': 5,
    'api_key': 'prod-key-xyz'
}

dev_request, dev_get_config = create_service(dev_config)
prod_request, prod_get_config = create_service(prod_config)

print("\nService configuration:")
print(f"Dev config: {dev_get_config()}")
print(f"Prod config: {prod_get_config()}")

print("\nDev service request:")
dev_response = dev_request('users/123')
print(f"Response: {dev_response}")

# Feature flag system
def create_feature_flag_checker(flags):
    enabled_flags = set(flags)
    
    def is_enabled(flag_name):
        return flag_name in enabled_flags
    
    def enable_flag(flag_name):
        nonlocal enabled_flags
        enabled_flags.add(flag_name)
    
    def disable_flag(flag_name):
        nonlocal enabled_flags
        enabled_flags.discard(flag_name)
    
    def get_enabled_flags():
        return list(enabled_flags)
    
    return is_enabled, enable_flag, disable_flag, get_enabled_flags

# Create feature flag checker
is_enabled, enable_flag, disable_flag, get_enabled_flags = create_feature_flag_checker([
    'new_ui', 'beta_features'
])

print("\nFeature flag system:")
print(f"Enabled flags: {get_enabled_flags()}")
print(f"new_ui enabled: {is_enabled('new_ui')}")
print(f"experimental enabled: {is_enabled('experimental')}")

enable_flag('experimental')
print(f"After enabling experimental: {get_enabled_flags()}")

disable_flag('beta_features')
print(f"After disabling beta_features: {get_enabled_flags()}")
```

Closures encapsulate configuration logic cleanly.

## Summary

Python closures provide:
- **State encapsulation** without global variables
- **Function factories** for creating specialized functions
- **Data privacy** through lexical scoping
- **Persistent state** across function calls
- **Foundation for decorators** and advanced patterns

**Key concepts:**
- **Closure**: Function + enclosing environment
- **Free variables**: Variables from enclosing scope
- **Cell objects**: Internal storage for closure variables
- **nonlocal**: Keyword to modify enclosing variables
- **Function factory**: Function that returns customized functions

**Common use cases:**
- Configuration management
- Event handlers and callbacks
- Decorators and middleware
- State machines and counters
- Caching and memoization
- API clients and service factories

**Best practices:**
- Use closures to avoid global state
- Keep closure logic simple and focused
- Document closure behavior clearly
- Consider memory implications of long-lived closures
- Use `nonlocal` judiciously for state modification


---
**Score: 30**