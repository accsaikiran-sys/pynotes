---
title: Ch11 04 Json
date: 2026-01-07
author: Your Name
cell_count: 35
score: 35
---

# Python JSON

Working with JSON for data interchange using Python's built-in `json` module.

## 1. What is JSON



```python
example = {
    'name': 'Alice',
    'age': 30,
    'active': True
}
print(example)
```

JSON (JavaScript Object Notation) is a lightweight format for storing and exchanging structured data. In Python, use the built-in `json` module.

## 2. Importing the JSON Module



```python
import json
print('json module imported')
```

Provides methods to convert between Python objects and JSON format.

## 3. Convert Python Object → JSON String (`json.dumps`)



```python
import json

data = {'name': 'Alice', 'age': 30, 'city': 'Toronto'}
json_string = json.dumps(data)

print(json_string)
```

Serializes Python objects into a JSON-formatted string.

## 4. Convert JSON String → Python Object (`json.loads`)



```python
import json

json_text = '{"name": "Bob", "age": 25}'
python_obj = json.loads(json_text)

print(python_obj)
print(type(python_obj))  # dict
```

Deserializes JSON strings into Python data structures.

## 5. Writing JSON to a File (`json.dump`)



```python
import json

data = {
    'product': 'Laptop',
    'price': 1200,
    'in_stock': True
}

with open('product.json', 'w') as file:
    json.dump(data, file)

print('Wrote product.json')
```

Stores structured data persistently.

## 6. Reading JSON from a File (`json.load`)



```python
import json

with open('product.json', 'r') as file:
    data = json.load(file)

print(data)
```

Loads JSON data into Python objects.

## 7. Pretty Printing JSON



```python
import json

data = {'name': 'Alice', 'skills': ['Python', 'AI', 'ML']}
pretty_json = json.dumps(data, indent=4)
print(pretty_json)
```

Improves readability for logs and debugging.

## 8. Handling Complex Data Types



```python
import json
from datetime import datetime

data = {'event': 'login', 'time': str(datetime.now())}
json_string = json.dumps(data)
print(json_string)
```

Non-serializable objects must be converted (e.g., datetime → string).

## 9. Sorting JSON Keys



```python
import json

data = {'b': 2, 'a': 1, 'c': 3}
sorted_json = json.dumps(data, sort_keys=True)
print(sorted_json)
```

Useful for consistent API responses and hashing.

## 10. Enterprise Example: API Response Handling



```python
import json

def parse_api_response(response):
    try:
        data = json.loads(response)
        return data.get('status'), data.get('payload')
    except json.JSONDecodeError:
        return 'error', None

response = '{"status": "success", "payload": {"id": 101}}'
print(parse_api_response(response))
```

Standard pattern for microservices and REST APIs.

## JSON ↔ Python Data Type Mapping
- Object → dict
- Array → list
- String → str
- Number (int) → int
- Number (float) → float
- true/false → True/False
- null → None

## Common JSON Errors
- JSONDecodeError: invalid JSON syntax
- TypeError: non-serializable object
- UnicodeDecodeError: encoding mismatch

## Best Practices
- Validate JSON structure and use try/except when decoding.
- Avoid storing sensitive data in plain JSON.
- Format JSON for logs; compress for production.
- Use schema validation when needed (e.g., Pydantic, Marshmallow).

## Enterprise Applications
- REST API communication
- Configuration files
- Microservices messaging
- Data interchange between systems
- AI model metadata storage


---
**Score: 35**