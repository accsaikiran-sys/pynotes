---
title: Ch07 All Examples Combined
date: 2025-12-18
author: Your Name
cell_count: 51
score: 50
---

# Chapter 7 - Exception Handling Examples

This notebook contains all 25 Python exception handling examples in separate cells.

## Example 1: Divide Two Numbers Safely


```python
try:
    num1 = float(input("enter first number: "))
    num2 = float(input("enter second number: "))

    print("Result: ", num1 / num2)

except ZeroDivisionError:
    print("Cannot divide by zero!")
```

## Example 2: Convert Input Interger


```python
try:
    value = input("Enter a value:" )
    result = int(value)
    print (result)

except ValueError:
    print("Enter a valid value")
```

## Example 3: List Index Access


```python
my_list = ["apple", "banana", "cherry"]

try:
    index = int(input("Enter an index to access: "))
    print(f"Item at index {index}: {my_list[index]}")

except IndexError:
    print("Index out of range!")
except ValueError:
    print("Please enter a valid integer!")
```

## Example 4: File Not Found Message


```python
try:
    with open("data.txt", "r") as file:
        content = file.read()
        print(content)

except FileNotFoundError:
    print("File not found.")
```

## Example 5: Finally Block Usage


```python
try:
    num1 = float(input("Enter first number: "))
    num2 = float(input("Enter second number: "))
    result = num1 / num2
    print(f"Result: {result}")

except ZeroDivisionError:
    print("Cannot divide by zero!")
except ValueError:
    print("Please enter valid numbers!")

finally:
    print("This block always runs")
```

## Example 6: Try Except Else


```python
try:
    user_input = input("Enter a number: ")
    number = int(user_input)

except ValueError:
    print("Invalid input! Please enter a valid integer.")

else:
    print("Success!")
```

## Example 7: Keyerror Ex


```python
user = {"name": "yourname", "age": 22}

try:
    print(user["email"])

except KeyError:
    print("Email key not found")
```

## Example 8: Raising Your Own Exception


```python
def check_age(age):
    if age < 18:
        raise Exception("Not eligible")
    print("Eligible!")


try:
    check_age(15)

except Exception as e:
    print(f"Error: {e}")
```

## Example 9: Custom Exception Class


```python
class InvalidNumber(Exception):
    pass


def validate_number(num):
    if num < 0:
        raise InvalidNumber("Number cannot be negative!")
    print(f"Valid number: {num}")


try:
    validate_number(-5)

except InvalidNumber as e:
    print(f"Error: {e}")
```

## Example 10: Multiple Except Blocks


```python
try:
    num1 = float(input("Enter first number: "))
    num2 = float(input("Enter second number: "))
    result = num1 / num2
    print(f"Result: {result}")

except ZeroDivisionError:
    print("Error: Cannot divide by zero! Please enter a non-zero divisor.")

except ValueError:
    print("Error: Invalid input! Please enter valid numbers only.")
```

## Example 11: Input Util Correct


```python
while True:
    try:
        number = int(input("Enter a number: "))
        print(f"Success! You entered: {number}")
        break

    except ValueError:
        print("Invalid input! Please enter a valid integer.")
```

## Example 12: Assert Positive Number


```python
try: 
    num = int(input("Enter number: "))
    assert num >= 0, "Number should be positive"
except AssertionError as e:
    print(e)
```

## Example 13: Exception In A Function


```python
def get_item(lst, index):
    try:
        return lst[index]
    except (IndexError, TypeError):
        return "Error occurred"
```

## Example 14: Simple Exception Chaining


```python
try:
    # Try converting a string to int
    result = int("abc")
except ValueError as original_exception:
    # If it fails, raise a new Exception with a custom message from the original exception
    raise Exception("Custom error message") from original_exception
```

## Example 15: Safe Calculator


```python
try:
    num1 = int(input("Enter first number: "))
    operator = input("Enter operator (+, -, *, /): ")
    num2 = int(input("Enter second number: "))

    if operator == '+':
        result = num1 + num2
    elif operator == '-':
        result = num1 - num2
    elif operator == '*':
        result = num1 * num2
    elif operator == '/':
        result = num1 / num2
    else:
        raise ValueError("Unsupported operator")

    print("Result:", result)

except ZeroDivisionError:
    print("Error: Cannot divide by zero")
except ValueError as e:
    if str(e) == "Unsupported operator":
        print("Error: Unsupported operator")
    else:
        print("Error: Invalid number")
```

## Example 16: String To Float Conversion


```python
try:
    user_input = input("Enter a number: ")
    result = float(user_input)
    print(f"Converted number: {result}")
except ValueError:
    print("Please enter a valid decimal number.")
```

## Example 17: Square Root Calc


```python
try:
    num = float(input("Enter a number: "))
    result = num ** 0.5
    print(f"Square root of {num} is {result}")
except ValueError:
    print("Please enter a valid decimal number.")
```

## Example 18: Safe File Reading


```python
try:
    user_input = input("Enter file name: ")
    file = open(user_input, "r")
    content = file.read()
    print(content)
except FileNotFoundError:
    print("Unable to read file .")
```

## Example 19: Integer Only List


```python
values = [5, "hello", 7, "world", 3]
for value in values:
    try:
        result = int(value)
        print(result)
    except ValueError:
        print("Skipping non-number")
```

## Example 20: No Internet Exception


```python
def connect_to_internet():
    raise ConnectionError("No internet connection")

try:
    connect_to_internet()
except ConnectionError:
    print("Please check your network")
```

## Example 21: Temp Validator


```python
try:
    user_input = int(input("Enter temperature: "))
    if user_input < -273:
        raise ValueError("Temperature below absolute zero")
except ValueError as e:
    print("Invalid temperature value")
```

## Example 22: Password Checker


```python
try:
    password = input("Enter password: ")
    if len(password) < 6:
        raise ValueError("Password too short")
    else:
        print("Password is valid")
except ValueError as e:
    print(e)
```

## Example 23: Calc With Try Finally


```python
try:
    num1 = int(input("Enter first number: "))
    num2 = int(input("Enter second number: "))
    result = num1 / num2
    print("Result:", result)
except ZeroDivisionError:
    print("Error: Cannot divide by zero")
finally:
    print("This will always execute")
```

## Example 24: Simple Age Group Checker


```python
try:
    age = int(input ("Enter age: "))
    if age <13:
        print ("Child")
    elif age <18:
        print ("Teenager")
    else:
        print ("Adult")
except ValueError :
    print ("Invalid age")
```

## Example 25: Safee Dictionary Update


```python
data = {"name": "Jerin", "age": 22}

try:
    key = input("Enter key to update: ")
    # Accessing the key to trigger KeyError if it doesn't exist
    _ = data[key]
    
    # If key exists, update it (using 25 as per previous context)
    key_data = input("Enter value to update: ")
    data[key] = key_data
    print("Updated dictionary:", data)
except KeyError:
    print("Key does not exist.")
```


---
**Score: 50**