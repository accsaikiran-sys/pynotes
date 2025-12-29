---
title: Ch05 08 Main Function
date: 2025-12-27
author: Your Name
cell_count: 12
score: 10
---

```python
#Create: 20251210
# https://csp.gitbook.io/python-learning/basics/ch05-python-functions/python-main-function
```


```python
def main():
    print("Program started")

main()
```

    Program started



```python
def main():
    print("Main function executed")

if __name__ == "__main__":
    main()
```

    Main function executed



```python
print(__name__)
```

    __main__



```python
def main(name):
    print(f"Welcome, {name}")

if __name__ == "__main__":
    main("Alice")
```

    Welcome, Alice



```python
def process_data():
    print("Processing data...")

def main():
    print("Initializing system...")
    process_data()

if __name__ == "__main__":
    main()
```

    Initializing system...
    Processing data...



```python
import sys

def main():
    print("Arguments received:", sys.argv)

if __name__ == "__main__":
    main()
```

    Arguments received: ['/home/kiran/miniconda3/envs/py12/lib/python3.12/site-packages/ipykernel_launcher.py', '-f', '/home/kiran/.local/share/jupyter/runtime/kernel-74017ddb-8190-498f-86af-a0086716c68e.json']



```python
def calculate_total(a, b):
    return a + b

def main():
    result = calculate_total(10, 20)
    print("Total:", result)

if __name__ == "__main__":
    main()
```

    Total: 30



```python
def initialize():
    print("System initialized")

def run():
    print("Application running")

def shutdown():
    print("System shutdown")

def main():
    initialize()
    run()
    shutdown()

if __name__ == "__main__":
    main()
```

    System initialized
    Application running
    System shutdown



```python
def main():
    try:
        print("Executing task...")
    except Exception as e:
        print("Error occurred:", e)

if __name__ == "__main__":
    main()
```

    Executing task...



```python
def main():
    """Application entry point"""
    print("Application started")

if __name__ == "__main__":
    main()
```

    Application started



```python

```


---
**Score: 10**