<!-- markdownlint-disable MD001 -->

# Elm

- [Print](#print)
- [Variables](#variables)
- [Data types](#data-types)
- [Operators](#operators)
- [Control flow](#control-flow)
- [Functions](#functions)
- [Error handling](#error-handling)

### Print

``` elm
import Html exposing (text)

main =
text "Hello World"
```

### Variables

``` elm
x = 4
x: Int = 4
```

### Data types

``` elm
-- Basic types
x: number
x: Int
x: Float
x: String
x: Char
x: Bool

-- List
myList: List = [1, 2, 3]

-- Tuple
myTuple: Tuple = (1, 2, 3)

-- Maybe
x: Maybe

-- Result
x: Result
```

### Operators

``` elm
-- Arithmetic operators
% -- modulo (remainder)
// -- floor division

-- Logical operators
== -- equal
!= -- not equal
&& -- AND
|| -- OR
xor -- XOR
not -- NOT
```

### Control flow

``` elm
if a > b then
    -- statement
else 
    -- statement
```

### Functions

``` elm
add x y = x+y

-- Call function
add 5 10
```

### Error handling

``` elm
-- Maybe type
userName: Maybe String
userName = Just "Peter"
userName = Nothing

-- Result type
userId: Result String Int
userId = Ok 10
userId = Err "Not a valid id"
```
