---
title: Ch09 05 Namespace Scope
date: 2025-12-27
author: Your Name
cell_count: 34
score: 30
---

# Chapter 10.1: Namespace and Scope in Python

This notebook covers Python namespaces and scope - how Python organizes and resolves variable names in different contexts.

## 1. What is a Namespace

A namespace is a container that holds identifiers (variables, functions, objects) and maps them to their corresponding values.


```python
# Basic namespace example
a = 10
print(f"Variable 'a' has value: {a}")
print(f"Variable 'a' is stored at memory address: {id(a)}")

# Multiple variables in the same namespace
name = "Alice"
age = 25
is_student = True

print(f"\nVariables in current namespace:")
print(f"name: {name}")
print(f"age: {age}")
print(f"is_student: {is_student}")

# Namespace prevents naming conflicts
x = "string value"
print(f"\nx as string: {x}")
x = 42
print(f"x as integer: {x}")
```

Here, `a` resides in a namespace and points to the value 10.

**Types of namespaces:**
- Built-in namespace
- Global namespace
- Local namespace

## 2. Built-in Namespace

Contains built-in functions and objects provided by Python.


```python
# Built-in functions are always available
print(len([1, 2, 3]))  # len is in built-in namespace
print(type(100))       # type is in built-in namespace
print(abs(-5))         # abs is in built-in namespace
print(max([1, 5, 3]))  # max is in built-in namespace

# View some built-in names
import builtins
builtin_names = dir(builtins)
print(f"\nNumber of built-in names: {len(builtin_names)}")
print("Some built-in functions:")
common_builtins = ['print', 'len', 'type', 'abs', 'max', 'min', 'sum', 'range']
for name in common_builtins:
    if name in builtin_names:
        print(f"  {name}")

# Built-in exceptions
print("\nSome built-in exceptions:")
exceptions = ['ValueError', 'TypeError', 'IndexError', 'KeyError']
for exc in exceptions:
    if exc in builtin_names:
        print(f"  {exc}")
```

These functions belong to the built-in namespace and are always available.

## 3. Global Namespace

Created when a module is loaded and remains until the program terminates.


```python
# Global variables
x = 50  # Global variable
company = "TechCorp"
version = 1.0

def show_global():
    print(f"Accessing global x: {x}")
    print(f"Company: {company}")
    print(f"Version: {version}")

show_global()

# Global variables persist across function calls
def increment_version():
    global version
    version += 0.1
    print(f"Version updated to: {version}")

print("\nBefore increment:")
print(f"Version: {version}")

increment_version()

print("After increment:")
print(f"Version: {version}")

# Multiple functions can access global variables
def show_company_info():
    print(f"\n{company} v{version}")

show_company_info()
```

Global variables are accessible throughout the module.

## 4. Local Namespace

Created inside a function and destroyed when the function exits.


```python
def calculate():
    y = 20  # Local variable
    z = 30  # Another local variable
    result = y + z
    print(f"Inside function - y: {y}, z: {z}, result: {result}")
    return result

# Call the function
output = calculate()
print(f"Function returned: {output}")

# Try to access local variables outside function
try:
    print(y)  # This will raise NameError
except NameError as e:
    print(f"\nError accessing local variable: {e}")

# Demonstrate local namespace isolation
def function_a():
    local_var = "Function A"
    print(f"In function_a: {local_var}")

def function_b():
    local_var = "Function B"
    print(f"In function_b: {local_var}")

print("\nDemonstrating local namespace isolation:")
function_a()
function_b()

# Local variables with same name don't conflict
def process_data(data):
    count = len(data)  # Local variable
    total = sum(data)  # Local variable
    average = total / count if count > 0 else 0
    print(f"Data: {data}, Count: {count}, Total: {total}, Average: {average}")

process_data([1, 2, 3, 4, 5])
process_data([10, 20, 30])
```

Local namespace is limited to function scope.

## 5. Accessing Namespace Using globals()


```python
# Global variables
x = 100
name = "Python"
pi = 3.14159

# Access global namespace
print("Accessing globals() dictionary:")
print(f"x from globals(): {globals()['x']}")
print(f"name from globals(): {globals()['name']}")

# List some global variables
print("\nSome global variables:")
global_vars = {k: v for k, v in globals().items() 
               if not k.startswith('_') and k in ['x', 'name', 'pi']}
for var_name, var_value in global_vars.items():
    print(f"  {var_name}: {var_value}")

# Modify global variable through globals()
print(f"\nBefore modification: x = {x}")
globals()['x'] = 200
print(f"After modification: x = {x}")

# Add new global variable
globals()['dynamic_var'] = "Created dynamically"
print(f"Dynamic variable: {dynamic_var}")

# Function using globals()
def show_globals():
    print("\nGlobal variables accessible in function:")
    for var in ['x', 'name', 'pi', 'dynamic_var']:
        if var in globals():
            print(f"  {var}: {globals()[var]}")

show_globals()
```

`globals()` returns a dictionary of all global identifiers.

## 6. Accessing Namespace Using locals()


```python
def demo_locals():
    a = 10
    b = 20
    c = "local string"
    
    print("Local variables:")
    local_dict = locals()
    for var_name, var_value in local_dict.items():
        print(f"  {var_name}: {var_value}")
    
    return local_dict

local_vars = demo_locals()

# More complex example
def calculate_stats(numbers):
    count = len(numbers)
    total = sum(numbers)
    average = total / count if count > 0 else 0
    minimum = min(numbers) if numbers else None
    maximum = max(numbers) if numbers else None
    
    print("\nFunction locals():")
    for name, value in locals().items():
        print(f"  {name}: {value}")
    
    return locals()

stats = calculate_stats([1, 2, 3, 4, 5])

# locals() in global scope
global_x = 42
global_y = "global"

print("\nlocals() in global scope (same as globals()):")
local_in_global = locals()
print(f"Are locals() and globals() the same in global scope? {local_in_global is globals()}")

# Nested function locals
def outer_function():
    outer_var = "outer"
    
    def inner_function():
        inner_var = "inner"
        print("\nInner function locals():")
        for name, value in locals().items():
            print(f"  {name}: {value}")
    
    print("\nOuter function locals():")
    for name, value in locals().items():
        print(f"  {name}: {value}")
    
    inner_function()

outer_function()
```

`locals()` returns a dictionary of local variables within a scope.

## 7. LEGB Rule (Scope Resolution Order)

Python resolves variable names in the following order:
- **L**ocal
- **E**nclosing
- **G**lobal
- **B**uilt-in


```python
# LEGB Rule demonstration
x = "Global"  # Global scope

def outer():
    x = "Enclosing"  # Enclosing scope
    
    def inner():
        x = "Local"  # Local scope
        print(f"Inner function sees: {x}")
    
    def inner_no_local():
        print(f"Inner (no local) sees: {x}")  # Uses enclosing
    
    print(f"Outer function sees: {x}")
    inner()
    inner_no_local()

print(f"Global scope: {x}")
outer()
print(f"After function calls: {x}")

# Built-in scope example
def demonstrate_builtin():
    # No local 'len' defined, so Python looks up the scope chain
    result = len([1, 2, 3, 4])  # Uses built-in len
    print(f"Using built-in len: {result}")

demonstrate_builtin()

# Shadowing built-in names (not recommended)
def shadow_builtin():
    len = "I'm not the built-in len!"  # Shadows built-in len
    print(f"Local len: {len}")
    
    # To access built-in len, we need to be explicit
    import builtins
    real_len = builtins.len([1, 2, 3])
    print(f"Built-in len result: {real_len}")

print("\nShadowing built-in names:")
shadow_builtin()

# Complex LEGB example
name = "Global Name"  # Global

def level1():
    name = "Level 1 Name"  # Enclosing for level2
    
    def level2():
        name = "Level 2 Name"  # Enclosing for level3
        
        def level3():
            # No local name, looks up the chain
            print(f"Level 3 sees: {name}")  # Level 2 Name
        
        def level3_with_local():
            name = "Level 3 Local"  # Local
            print(f"Level 3 (with local) sees: {name}")
        
        print(f"Level 2 sees: {name}")
        level3()
        level3_with_local()
    
    print(f"Level 1 sees: {name}")
    level2()

print("\nComplex LEGB example:")
level1()
```

Output follows the closest scope: Local → Enclosing → Global → Built-in.

## 8. Enclosing Namespace

Occurs in nested functions, holding variables from outer functions.


```python
# Basic enclosing namespace
def outer():
    message = "Hello from outer function"  # Enclosing variable
    number = 42
    
    def inner():
        print(f"Inner function accessing: {message}")
        print(f"Inner function accessing: {number}")
    
    inner()
    return inner  # Return the inner function

outer()

# Closure example - enclosing variables persist
def create_multiplier(factor):
    def multiply(number):
        return number * factor  # 'factor' is from enclosing scope
    return multiply

# Create different multipliers
double = create_multiplier(2)
triple = create_multiplier(3)
times_ten = create_multiplier(10)

print("\nClosure examples:")
print(f"double(5) = {double(5)}")
print(f"triple(5) = {triple(5)}")
print(f"times_ten(5) = {times_ten(5)}")

# Multiple enclosing levels
def level_1():
    var1 = "Level 1 variable"
    
    def level_2():
        var2 = "Level 2 variable"
        
        def level_3():
            var3 = "Level 3 variable"
            print(f"Level 3 can access: {var1}")  # From level 1
            print(f"Level 3 can access: {var2}")  # From level 2
            print(f"Level 3 can access: {var3}")  # Local
        
        level_3()
    
    level_2()

print("\nMultiple enclosing levels:")
level_1()

# Practical example: Configuration closure
def create_config_handler(app_name, version):
    def get_config(key, default=None):
        config_data = {
            'app_name': app_name,
            'version': version,
            'debug': True,
            'max_connections': 100
        }
        return config_data.get(key, default)
    
    return get_config

# Create configuration handlers for different apps
web_config = create_config_handler("WebApp", "1.0")
api_config = create_config_handler("API", "2.1")

print("\nConfiguration closure example:")
print(f"Web app name: {web_config('app_name')}")
print(f"Web app version: {web_config('version')}")
print(f"API app name: {api_config('app_name')}")
print(f"API version: {api_config('version')}")
```

Inner functions can reference enclosing variables.

## 9. Modifying Enclosing Variables with nonlocal


```python
# Basic nonlocal example
def counter():
    value = 0  # Enclosing variable
    
    def increment():
        nonlocal value  # Declare intention to modify enclosing variable
        value += 1
        return value
    
    def decrement():
        nonlocal value
        value -= 1
        return value
    
    def get_value():
        return value  # Read-only access doesn't need nonlocal
    
    return increment, decrement, get_value

# Create counter functions
inc, dec, get = counter()

print("Counter example:")
print(f"Initial value: {get()}")
print(f"After increment: {inc()}")
print(f"After increment: {inc()}")
print(f"After decrement: {dec()}")
print(f"Current value: {get()}")

# Without nonlocal (creates local variable instead)
def broken_counter():
    value = 0
    
    def increment():
        # This creates a local variable, doesn't modify enclosing
        value = value + 1  # UnboundLocalError!
        return value
    
    return increment

print("\nTrying broken counter (without nonlocal):")
try:
    broken_inc = broken_counter()
    broken_inc()
except UnboundLocalError as e:
    print(f"Error: {e}")

# Multiple nonlocal variables
def create_bank_account(initial_balance):
    balance = initial_balance
    transaction_count = 0
    
    def deposit(amount):
        nonlocal balance, transaction_count
        balance += amount
        transaction_count += 1
        print(f"Deposited ${amount}. New balance: ${balance}")
    
    def withdraw(amount):
        nonlocal balance, transaction_count
        if balance >= amount:
            balance -= amount
            transaction_count += 1
            print(f"Withdrew ${amount}. New balance: ${balance}")
        else:
            print(f"Insufficient funds. Current balance: ${balance}")
    
    def get_info():
        return {
            'balance': balance,
            'transactions': transaction_count
        }
    
    return deposit, withdraw, get_info

# Create bank account
deposit, withdraw, get_info = create_bank_account(1000)

print("\nBank account example:")
print(f"Initial state: {get_info()}")
deposit(200)
withdraw(150)
withdraw(2000)  # Insufficient funds
print(f"Final state: {get_info()}")

# Nested nonlocal
def outer_function():
    outer_var = "original"
    
    def middle_function():
        middle_var = "middle"
        
        def inner_function():
            nonlocal outer_var, middle_var
            outer_var = "modified by inner"
            middle_var = "also modified"
        
        print(f"Before inner call: outer_var='{outer_var}', middle_var='{middle_var}'")
        inner_function()
        print(f"After inner call: outer_var='{outer_var}', middle_var='{middle_var}'")
    
    middle_function()
    print(f"In outer function: outer_var='{outer_var}'")

print("\nNested nonlocal example:")
outer_function()
```

`nonlocal` allows modification of variables in the enclosing namespace.

## 10. Namespace Lifecycle Demonstration


```python
# Namespace isolation demonstration
x = "Global"  # Global namespace

def test():
    x = "Local"  # Local namespace
    print(f"Inside function: {x}")
    
    # Show that local and global are separate
    print(f"Local x id: {id(x)}")
    print(f"Global x id: {id(globals()['x'])}")
    print(f"Are they the same object? {x is globals()['x']}")

print(f"Before function call: {x}")
test()
print(f"After function call: {x}")

# Namespace lifecycle with multiple calls
def lifecycle_demo():
    local_var = "Created in function"
    print(f"Function call - local_var: {local_var}")
    print(f"Local namespace id: {id(locals())}")
    return local_var

print("\nNamespace lifecycle:")
result1 = lifecycle_demo()
result2 = lifecycle_demo()
print(f"Results are same value: {result1 == result2}")
print(f"Results are same object: {result1 is result2}")

# Global vs local variable interaction
counter = 0  # Global counter

def increment_global():
    global counter
    counter += 1
    print(f"Global counter incremented to: {counter}")

def increment_local():
    counter = 100  # Local variable, shadows global
    counter += 1
    print(f"Local counter: {counter}")
    print(f"Global counter unchanged: {globals()['counter']}")

print("\nGlobal vs local interaction:")
print(f"Initial global counter: {counter}")
increment_global()
increment_local()
print(f"Final global counter: {counter}")

# Namespace pollution example
def demonstrate_namespace_pollution():
    # Bad practice: modifying global namespace from function
    globals()['polluted_var'] = "This shouldn't be here"
    
    # Good practice: return values instead
    clean_var = "This is returned properly"
    return clean_var

print("\nNamespace pollution demonstration:")
print(f"Before function: 'polluted_var' in globals(): {'polluted_var' in globals()}")
clean_result = demonstrate_namespace_pollution()
print(f"After function: 'polluted_var' in globals(): {'polluted_var' in globals()}")
print(f"Clean result: {clean_result}")

# Class namespace example
class NamespaceDemo:
    class_var = "Class variable"  # Class namespace
    
    def __init__(self):
        self.instance_var = "Instance variable"  # Instance namespace
    
    def show_namespaces(self):
        local_var = "Local variable"  # Local namespace
        print(f"Local: {local_var}")
        print(f"Instance: {self.instance_var}")
        print(f"Class: {self.class_var}")
        print(f"Global x: {x}")

print("\nClass namespace example:")
demo_obj = NamespaceDemo()
demo_obj.show_namespaces()
```

Shows that separate namespaces prevent conflicts between global and local variables.

## Advanced Namespace Concepts


```python
# Module namespace simulation
class ModuleSimulator:
    """Simulate how modules create their own namespace"""
    def __init__(self, name):
        self.name = name
        self.namespace = {}
    
    def add_variable(self, name, value):
        self.namespace[name] = value
    
    def get_variable(self, name):
        return self.namespace.get(name, "Not found")
    
    def list_variables(self):
        return list(self.namespace.keys())

# Create "modules"
math_module = ModuleSimulator("math")
string_module = ModuleSimulator("string")

# Add variables to different "modules"
math_module.add_variable("pi", 3.14159)
math_module.add_variable("e", 2.71828)
string_module.add_variable("vowels", "aeiou")
string_module.add_variable("digits", "0123456789")

print("Module namespace simulation:")
print(f"Math module variables: {math_module.list_variables()}")
print(f"String module variables: {string_module.list_variables()}")
print(f"Math pi: {math_module.get_variable('pi')}")
print(f"String vowels: {string_module.get_variable('vowels')}")

# Namespace inspection utilities
def inspect_namespace(namespace_dict, name):
    """Utility to inspect a namespace"""
    print(f"\n{name} namespace inspection:")
    print(f"Total items: {len(namespace_dict)}")
    
    # Categorize items
    functions = [k for k, v in namespace_dict.items() if callable(v)]
    classes = [k for k, v in namespace_dict.items() if isinstance(v, type)]
    variables = [k for k, v in namespace_dict.items() 
                if not callable(v) and not isinstance(v, type) and not k.startswith('_')]
    
    print(f"Functions: {len(functions)}")
    print(f"Classes: {len(classes)}")
    print(f"Variables: {len(variables)}")
    
    if variables:
        print(f"Sample variables: {variables[:5]}")

# Inspect current global namespace
inspect_namespace(globals(), "Global")

# Namespace best practices demonstration
def namespace_best_practices():
    """Demonstrate namespace best practices"""
    
    # ✅ Good: Use descriptive names
    user_count = 100
    max_connections = 50
    
    # ✅ Good: Avoid global modifications
    def calculate_ratio(count, maximum):
        return count / maximum if maximum > 0 else 0
    
    # ✅ Good: Use local variables for temporary data
    temp_result = calculate_ratio(user_count, max_connections)
    
    # ✅ Good: Return values instead of modifying globals
    return {
        'user_count': user_count,
        'max_connections': max_connections,
        'ratio': temp_result
    }

print("\nBest practices example:")
result = namespace_best_practices()
print(f"Result: {result}")
```

## Summary

Python namespaces and scope provide:
- **Organized variable storage** through different namespace types
- **Name resolution** following the LEGB rule
- **Scope isolation** preventing variable conflicts
- **Flexible access** to different namespace levels
- **Memory management** through namespace lifecycle

**Key concepts:**
- **Namespace**: Container mapping names to objects
- **Scope**: Region where a namespace is accessible
- **LEGB Rule**: Local → Enclosing → Global → Built-in
- **global**: Modify global variables from local scope
- **nonlocal**: Modify enclosing variables from nested functions

**Best practices:**
- Minimize global variable usage
- Use descriptive variable names
- Avoid shadowing built-in names
- Return values instead of modifying global state
- Understand scope when using nested functions
- Use `global` and `nonlocal` judiciously


---
**Score: 30**