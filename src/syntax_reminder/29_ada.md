<!-- markdownlint-disable MD001 -->

# Ada

- [Print](#print)
- [Variables](#variables)
- [Data types](#data-types)
- [Operators](#operators)
- [Control flow](#control-flow)
- [Functions](#functions)

### Print

``` ada
Ada.Text_IO.Put_Line ("Hello, World!");
```

### Variables

``` ada
X := 4;
X: Integer := 4;
X: constant Integer := 4;
```

### Data types

``` ada
-- basic types
X: Integer;
X: Float;
X: String;
type Boolean is (False, True);

-- enum
type Color is (Red, Green, Blue);
```

### Operators

``` ada
-- Logical operators
= -- equal
/= -- not equal
and -- AND
or -- OR
xor -- XOR
```

### Control flow

``` ada
-- if-else
if a > b then
    statement;
elsif a == b then
    statement;
else
    statement;
end if;
```

### Functions

``` ada
-- procedure
procedure Add (A, B: in Integer; C: out Integer) is
begin
   C := A + B;
end Add;

-- function
function Add (X, Y: Integer) return Integer is
begin
    return X + Y;
end Add;
```
