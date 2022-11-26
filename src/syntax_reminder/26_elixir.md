<!-- markdownlint-disable MD001 -->

# Elixir

- [Print](#print)
- [Variables](#variables)
- [Data types](#data-types)
- [Operators](#operators)
- [Control flow](#control-flow)
- [Functions](#functions)
- [Error handling](#error-handling)

### Print

``` elixir
IO.puts "Hello world"
```

### Variables

``` elixir
x = 4
x = "my string"
```

### Data types

``` elixir
# Number
x = 4

# String
x = "hello world"

# Atom
x = :hello

# Tuple
{1, 2, true, 3}

# List
[1, 2, true, 3]

# Map
map = %{:name => "Peter", :age => 42}
```

### Operators

``` elixir
# Arithmetic operators
rem # modulo (remainder)
div # floor division

% Logical operators
== # equal
/= # not equal
=== # type check
and # AND
or # OR
not # NOT
&& # non-strict and
|| # non-strict or
! # non-strict not

% Bitwise operators
&&& # AND
||| # OR
^^^ # XOR
~~~ # NOT
<<< # left shift
>>> # right shift
```

### Control flow

``` elixir
# if-else
if a < b do
    # statement
else
    # statement
end
```

### Functions

``` elixir
def my_function(x, y) do
    x + y
end

# Anonymous function
sum = fn (x, y) -> x + y end
```

### Error handling

``` elixir
err = try do
    # statement
rescue
    e in RuntimeError -> e
end
```
