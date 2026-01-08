---
title: Ch06 01 Directory File Management
date: 2026-01-07
author: Your Name
cell_count: 11
score: 10
---

```python
#Created : 20251210
#https://csp.gitbook.io/python-learning/basics/ch06-python-files/python-directory-and-files-management
```


```python
import os

current_dir = os.getcwd()
print(current_dir)
```

    /home/kiran/pynotes/notebooks/basics



```python
import os

os.chdir("C:/Projects")
print(os.getcwd())
```


    ---------------------------------------------------------------------------

    FileNotFoundError                         Traceback (most recent call last)

    Cell In[3], line 3
          1 import os
    ----> 3 os.chdir("C:/Projects")
          4 print(os.getcwd())


    FileNotFoundError: [Errno 2] No such file or directory: 'C:/Projects'



```python
import os

items = os.listdir(".")
print(items)
```


```python
import os

os.mkdir("new_folder")
os.makedirs("parent/child/grandchild")
```


```python
import os

print(os.path.exists("data.txt"))      # True or False
print(os.path.isfile("data.txt"))     # Checks file
print(os.path.isdir("new_folder"))    # Checks directory
```


```python
with open("sample.txt", "w") as file:
    file.write("Hello, Python File System")
```


```python
with open("sample.txt", "r") as file:
    content = file.read()

print(content)
```


```python
import os

os.rename("sample.txt", "renamed.txt")
os.remove("renamed.txt")
```


```python
import shutil

shutil.copy("source.txt", "backup.txt")
shutil.move("backup.txt", "archive/backup.txt")
```


    ---------------------------------------------------------------------------

    FileNotFoundError                         Traceback (most recent call last)

    Cell In[4], line 3
          1 import shutil
    ----> 3 shutil.copy("source.txt", "backup.txt")
          4 shutil.move("backup.txt", "archive/backup.txt")


    File ~/miniconda3/envs/py12/lib/python3.12/shutil.py:435, in copy(src, dst, follow_symlinks)
        433 if os.path.isdir(dst):
        434     dst = os.path.join(dst, os.path.basename(src))
    --> 435 copyfile(src, dst, follow_symlinks=follow_symlinks)
        436 copymode(src, dst, follow_symlinks=follow_symlinks)
        437 return dst


    File ~/miniconda3/envs/py12/lib/python3.12/shutil.py:260, in copyfile(src, dst, follow_symlinks)
        258     os.symlink(os.readlink(src), dst)
        259 else:
    --> 260     with open(src, 'rb') as fsrc:
        261         try:
        262             with open(dst, 'wb') as fdst:
        263                 # macOS


    FileNotFoundError: [Errno 2] No such file or directory: 'source.txt'



```python
from pathlib import Path

file_path = Path("example.txt")

file_path.write_text("Using pathlib module")
print(file_path.read_text())

print(file_path.exists())
print(file_path.parent)
```


---
**Score: 10**