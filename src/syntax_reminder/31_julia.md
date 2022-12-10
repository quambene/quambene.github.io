<!-- markdownlint-disable MD001 -->

# Julia

- [Print](#print)
- [Variables](#variables)
- [Data types](#data-types)
- [Operators](#operators)
- [Control flow](#control-flow)
- [Functions](#functions)

### Print

``` julia
x = "world"
println("hello ", x)
```

### Variables

``` julia
x = 4
x::Int32 = 4
```

### Data types

``` julia
# Basic types
x::Int32 = 4
x::UInt32 = 4
x::Float32 = 4.5
x::Bool = true

# Rational number
x = 4//5

# Complex number
x = 2 + 3im

# Array
arr = [1, 2, 3]

# Tuple
tup = (1, 2, 3)

# Dictionary
dict = Dict("key1" => "val1", "key2" => "val2")

# Set
set = Set{String}(["red", "green", "blue"])

# Struct
struct User
    username::String
    email::String
end
```

### Operators

``` julia
# Arithmetic operators
% # modulo (remainder)
// # floor division

# Logical operators
== # equal
!= # not equal
&& # AND
|| # OR
! # NOT

# Bitwise operators
& # AND
| # OR
^ # XOR
~ # NOT
<< # left shift
>> # right shift
>>> # right shift with zero
```

### Control flow

``` julia
if a < b
    # statement
elseif a == b
    # statement
else
    # statement
end
```

### Functions

``` julia
f(x, y) = x + y

function add(x, y)
    x + y
end

function add(x::Any, y::Any)
    x + y
end
```
