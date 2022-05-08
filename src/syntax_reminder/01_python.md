<!-- markdownlint-disable MD001 -->

# Python

- [Print](#print)
- [Variables](#variables)
- [Data types](#data-types)
- [Operators](#operators)
- [Control flow](#control-flow)
- [Functions](#functions)
- [Classes](#classes)
- [Error handling](#error-handling)
- [Testing](#testing)

### Print

```python
name = "world"
print("Hello ", name)
print(f"Hello, {name}!")
print("This %(verb)s a %(noun)s." % {"noun": "test", "verb": "is"})
print("integer: %d float: %f" % (my_int, my_float))
print(f"binary: {4:b}")
print(f"binary (zero-padded): {4:04b}")
```

### Variables

```python
x: int # Declare type
x = 4 # Assign value
x: int = 4 # Assign value (typed)
x = y = z = 0 # Multiple assignment
x += 1 # Increment
x -= 1 # Decrement
_x = 4 # Suppress 'unused variable' warning

# Random number
random.random() # Random float in [0, 1)
random.randint(a, b) # Random int in [a, b]
random.randrange(a, b) # Random int in [a, b)
```

### Data types

```python
# Basic types
x: int
x: float
x: complex
x: str
x: bool

type(x) # Check type

from typing import Any
x: Any

# Integer
x = 42 # decimal
x = 0b101010 # binary
x = 0x2a # hex
x = 0o52 # octal
bin(42) # convert to binary number
hex(42) # convert to hex number
oct(42) # convert to octal number
ord('a') # convert character to unicode
chr(97) # convert unicode to character
int("101010", 2) # convert binary to decimal number

# String
len(my_str)
my_str[0] # first character
my_str[-1] # last character
my_str[start:end] # substring [start, end)
s1 + s2 # Concatenate strings
" ".join([s1, s2]) # Concatenate with separator
my_str.split(" ", -1) # Split blank-separated string into a list
list(my_string) # Convert string to list of characters
4 * "01" # Concatenate string multiple times
if my_substr in my_str # check if string contains substring 
my_str.lower() # lower case string
my_str.upper() # upper case string

# List (dynamic array)
my_arr = ["item1", "item2", "item3"]
my_arr: List[str] = ["item1", "item2", "item3"] # typed
my_arr = [] # empty list
my_arr[0:3] # Indexing is inclusive-exclusive
my_arr[-3:-1] # Negative indexes count from the last item backwards
len(my_arr)
min(my_arr)
max(my_arr)
my_arr.append(value)
my_arr.remove(value)
my_arr.insert(index, value)
my_arr.pop(index)
my_arr.reverse() # in-place
reversed(my_arr) # copy
my_arr.sort() # in-place
sorted(my_arr) # copy
my_arr[i], my_arr[j] = my_arr[j], my_arr[i] # Swap items

# Tuple
my_tup = (1, 2, 3)
my_tup = () # empty tuple
my_tup: Tuple[int, int, int] = (1, 2, 3) # typed

# Dictionary
my_dict = {"key1": 1, "key2": 2}
my_dict: Dict[int, int] = {"key1": 1, "key2": 2} # typed

# Set
my_set = {"foo", "bar"}
my_set: Set[str] = {"foo", "bar"} # typed
my_set = set() # empty set
my_set.add(el) # Add element to set
my_set.remote(el) # Remove element
my_set.discard(el) # Remove element (fail quietly)
my_set.clear() # Removes all elements
x1 | x2 # union
x1.union(x2) # union
x1 & x2 # intersection
x1.intersection(x2) # intersection
x1 - x2 # difference
x1.difference(x2) # difference
x1 ^ x2 # symmetric difference / disjunctive union
x1.symmetric_difference(x2) # symmetric difference / disjunctive union
x1.isdisjoint(x2) # check if disjoint sets
x1 <= x2 # check if subset
x1.issubset(x2) # check if subset
x1 < x2 # check if proper subset
x1 >= x2 # check if superset
x1.issuperset(x2) # check if superset
enumerate(my_set) # returns enumerated iterator
list(my_set) # Convert set to list

# Bytearray
my_bytearray = bytearray(4) # empty bytearray of bytes
my_bytearray = bytearray(my_str, "utf-8") # Convert string to bytearray

# (dynamic) Array
import array as arr
my_arr = arr.array('i', [1, 2, 3]) # array of unsigned integers

# Linked list / double-ended queue
from collections import deque
llist = deque() # empty linked list
llist = deque('abc')

# Binary trees
from binarytree import Node

# Binary search
from bisect import bisect_left

# Option
from typing import Optional
x: Optional[str] = some_function()

# Callback
from typing import Callable
x: Callable[[int], int]
```

### Operators

``` python
# Logical operators
and
or
not

# Identity operators
is
is not

# Membership operators
in
not in

# Arithmetic operators
+ # addition
- # subtraction
* # multiplication
/ # division
** # exponentiation
% # modulo (remainder)
// # floor division

# Bitwise operators
& # AND
| # OR
~ # NOT
^ # XOR
>> # right shift
<< # left shift
```

### Control flow

```python
# Loop control statements
continue
break
pass

# for loop
for i in range(4): # [0, 1, 2, 3]
    print(i)

# while loop
while i < 3:
    print(i)

# if-else
if a < b:
    # statement
elif a == b:
    # statement
else:
    # statement
```

### Functions

```python
def my_function(arg, optional_arg = 'default value'):
    return arg, optional_arg

# Typed function
def my_function(arg1: int, arg2: int) -> Tuple[int, int]:
    return arg1, arg2

# Lambda function
add_one = lambda x: x + 1

# Decorator
@my_decorator
def my_function():
    return
```

### Classes

```python
class MyClass:
    my_class_var = 100

    def __init__(self, my_instance_var):
        self.my_instance_var = my_instance_var

    def my_function(self):
        pass

# Instantiation
my_class = MyClass()
my_class.my_function()
my_class.my_class_var
my_class.my_instance_var

# Inheritance
class MyDerivedClass(MyBaseClass):
    pass

# Abstract class
from abc import ABC, abstractmethod

class MyAbstractClass(ABC)
    @abstractmethod
    def my_abstract_method(self):
        pass

# Data class
@dataclass
class User:
    name: str
    email: str
```

### Error handling

```python
try:
    # statement
except ZeroDivisionError: # if an exception was raised in the try clause
    # statement
else: # if no exceptions were raised in the try clause
    # statement
finally: # always executed
    # statement

# Raise error
raise ValueError("error message")
```

### Testing

``` python
import pytest


def my_func():
    return 4


def test_my_func():
    assert my_func() == 4


@pytest.mark.unit
def test_my_func2():
    assert my_func() == 4


@pytest.mark.integration
def test_my_func3():
    assert my_func() == 4

```

``` bash
# Run tests
pytest
pytest -v
pytest -v *.py
pytest -v -m unit *.py
pytest -v -m integration *.py
```
