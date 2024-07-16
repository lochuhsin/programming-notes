---
Created: 2023-08-11 16:49
aliases:
  - fd
  - file descriptor
card link:
  - "[[Operat"
---

Source:  
Card Link: [[Operating System]]  
Tags:

## Description
---

A file descriptor is a non-negative integer that represents a I/O source in Unix like system.

0, 1, 2 represents the standard inputs, standard outputs, standard errors.

When opening a file in application level, what it actually does is calling operating system to open a file, (This is a blocking call, since the application needs to wait the system call). Then the operating system will return an integer (usually larger than 2). This is a file descriptor, just like a key, since the actual file or data … whatever the implementation under operating system is hidden under OS. 

The application uses this file descriptor to interact with the operating system to get data.

```python
# In python
import os

fd = os.open("path to file", flag=???) #flag indicates the operation like read or delete ...etc. It's an integer.

fd2 = os.open("path to file 2", flag=???)

# fd will represents 3 and fd2 is 4 since fd and fd2 are different files.
# now we can read the data in bytes

# read the file in 100 bytes
file1_data = os.read(fd, 100)

# close the file
os.close(fd)

# what happend if .... after closing the file
os.read(fd) # this returns error obviously
```