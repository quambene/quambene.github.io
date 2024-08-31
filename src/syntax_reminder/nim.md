<!-- markdownlint-disable MD001 -->

# Nim

- [Print](#print)
- [Variables](#variables)
- [Data types](#data-types)
- [Operators](#operators)
- [Control flow](#control-flow)
- [Functions](#functions)

### Print

``` nim
var name: string = "world"
echo "Hello ", name, "!"
```

### Variables

``` nim
var x: int = 4
let x: int = 4
const x: int = 4
```

### Data types

``` nim
# basic types
let x: int
let x: string
let x: bool

# tuple
let x = tuple[name: string, age: int]

# enum
let Color = enum cRed, cBlue, cGreen
```

### Operators

``` nim
# Logical operators
== # equal
!= # not equal
and # AND
or # OR
xor # XOR
```

### Control flow

``` nim
# if-else
if a > b:
    # statement
elif a == b:
    # statement
else:
    # statement
```

### Functions

``` nim
# procedure
proc printNumber(i: int) =
    echo i

# function
func add(x: int, y: int): int =
    x + y
```
