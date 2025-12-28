---
title: Python Basic Input Output
date: 2025-12-26
author: Your Name
cell_count: 15
score: 15
---

```python
Created:20251128
https://csp.gitbook.io/python-learning/basics/ch02-python-fundamentals/python-basic-input-and-output
```


```python
print("Hello, Python!")
print(100)
print(3.14)
```


```python
name = "Alice"
age = 30

print(name, age)  
# Output: Alice 30
```


```python
print("Python", "is", "powerful", sep=" - ", end="!")
# Output: Python - is - powerful!
```


```python
name = "Bob"
score = 88

print(f"Student {name} scored {score} marks.")
# Output: Student Bob scored 88 marks.
```


```python
product = "Laptop"
price = 1200
li = 66

print("The price of {} is ${}.{}".format(product, price,li))
# Output: The price of Laptop is $1200
```


```python
item = "Book"
quantity = 5

print("You bought %d %s(s)." % (quantity, item))
# Output: You bought 5 Book(s).
```


```python
name = input("Enter your name: ")
print("Hello,", name)
```


```python
age = int(input("Enter your age: "))

print(f"You will be {age + 1} next year.")

```


```python
numbers = input("Enter two numbers: ").split()

num1 = int(numbers[0])
num2 = int(numbers[1])

print(num1 + num2)
```


```python
# with open("output.txt", "w") as file:
#     print("This text goes into the file.", file=file)

# print("Data successfully written to output.txt")

```


```python

```


```python

```


```python

```


```python

```


---
**Score: 15**