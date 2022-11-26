<!-- markdownlint-disable MD001 -->

# Erlang

- [Print](#print)
- [Variables](#variables)
- [Data types](#data-types)
- [Operators](#operators)
- [Control flow](#control-flow)
- [Functions](#functions)
- [Error handling](#error-handling)

### Print

``` erlang
% my comment
-module(helloworld). 
-export([start/0]).

start() ->
   io:fwrite("Hello, world!\n").
```

### Variables

``` erlang
X = 4
```

### Data types

``` erlang
% number
X=4,

% atom
X = 'MyString',

% Bit string
Bin1 = <<10,20>>,

% Tuple
T = {john, peter},

% Map
M = #{name=>peter, age=>40},

% List
L = [10,20,30],
```

### Operators

``` erlang
% Arithmetic operators
rem % modulo (remainder)
div % floor division

% Logical operators
== % equal
/= % not equal
and % AND
or % OR
xor % XOR
not % NOT

% Bitwise operators
band % AND
bor % OR
bxor % XOR
bnot % NOT
```

### Control flow

``` erlang
% if-else
if 
    A < B -> 
        % statement; 
    A == B ->
        % statement;
    true -> 
        % default statement
end.

% case statement
case A of 
    5 -> io:fwrite("five"); 
    6 -> io:fwrite("six") 
end.
```

### Functions

``` erlang
add(X,Y) ->
   Z = X+Y.

% Anonymous function
Fn = hello() ->
    io:fwrite("hello") end,
Fn().
```

### Error handling

``` erlang
try generate_exception(N) of 
    Val -> {N, normal, Val} 
catch 
    throw:X -> {N, caught, thrown, X}; 
    exit:X -> {N, caught, exited, X}; 
    error:X -> {N, caught, error, X} 
end.
```
