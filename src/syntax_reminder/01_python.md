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
```

### Data types

```python
# Basic types
x: int
x: float
x: complex
x: str
x: bool

from typing import Any
x: Any

# Integer
x = 42 # decimal
x = 0b101010 # binary
x = 0x2a # hex
x = 0o52 # octal

# String
len(my_string)
my_string[start:end] # substring [start:end)
my_string[-1] # last character

# List
x = ["item1", "item2", "item3"]
x: List[str] = ["item1", "item2", "item3"] # typed
x[0:3] # Indexing is inclusive-exclusive
x[-3:-1] # Negative indexes count from the last item backwards

# Tuple
x = (1, 2, 3)
x: Tuple[int, int, int] = (1, 2, 3) # typed

# Dictionary
x = {"key1": 1, "key2": 2}
x: Dict[int, int] = {"key1": 1, "key2": 2} # typed

# Option
x: Optional[str] = some_function()
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
