<!-- markdownlint-disable MD001 -->

# Zig

- [Print](#print)
- [Variables](#variables)
- [Data types](#data-types)
- [Operators](#operators)
- [Control flow](#control-flow)
- [Functions](#functions)

### Print

``` zig
std.debug.print("Hello, {s}!\n", .{"World"});
```

### Variables

``` zig
const x: i32 = 4;
var x: u32 = 4;
```

### Data types

``` zig
// basic types
const x: i32;
const x: i64;
const x: u32;
const x: u64;
const x: f64;
const x: bool;

// array
const my_array = [3]u32{ 1, 2, 3 };

// vector
const x: Vector(3, u32) = .{ 1, 2, 3 };

// enum
const Color = enum { red, green, blue };

// struct
const User = struct {
    username: []const u8,
    email: []const u8,
}
```

### Operators

``` zig
// Arithmetic operators
% // modulo (remainder)
// -- floor division

// Logical operators
== // equal
!= // not equal
&& // AND
|| // OR

// Bitwise operation
& // AND
| // OR
^ // XOR
~ // NOT
```

### Control flow

``` zig
// if-else
if (a < b) {
    // statement
} else {
    // statement
}

// While loop
while (i < 3) {
    // statement
}
```

### Functions

``` zig
fn add(x: u32, y: u32) u32 {
    return x + y;
}
```
