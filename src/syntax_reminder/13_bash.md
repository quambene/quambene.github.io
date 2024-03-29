<!-- markdownlint-disable MD001 -->

# Bash

- [Shebang](#shebang)
- [Print](#print)
- [Input](#input)
- [Variables](#variables)
- [Operators](#operators)
- [Commands](#commands)
- [Functions](#functions)
- [Control flow](#control-flow)
- [Error handling](#error-handling)

### Shebang

```bash
#!/bin/bash

# alternative:
#!/usr/bin/env bash
```

### Print

```bash
$name="world"
echo "hello $name"

printf "hello %s \n" world
```

### Input

```bash
echo -e "Please enter your name: "
read name
echo "Nice to meet you $name"
```

### Variables

```bash
# Use letters, numbers and underscores for variable names

my_variable=my_value
my_variable='hello world' # single quotes are not interpreted
my_variable="hello $name" # double quotes allow substitution
my_dir=/home/dev
my_array=(1, 2, 3, 4)
variable=$( my_command ) # save output of command into a variable
timestamp=$(date +"%Y-%m-%d_%H:%M:%S")

$my_dir 
${my_dir} # variable expansion
${#my_string} # string length
${my_var=default_value}
${my_var1?my_var2} # use my_var2 if my_var1 is null

a{d,c,b}e # brace expansion: "ade ace abe"

# environment variable (export to all child processes created from that shell)
export MY_VAR=my_val
source .env

MY_VAR=my_val
set -a && source .env && set +a

# positional parameters
$0 # name of the script
$1 - $9 # first 9 arguments of the script
$# # number of arguments passed to the script
$? # the exit status of the most recently run process
$$ # the process ID of the current script
$USER # the username of the user running the script
$HOSTNAME # the hostname of the machine the script is running on
$SECONDS # the number of seconds since the script was started
$RANDOM # return a random number
$LINENO # returns the current line number in the script
```

## Operators

``` bash
# logical operators
&& # and
|| # or

# arithmetic operators inside [] or [[ ]]: 
-eq, -ne, -lt, -gt, -le, -ge

# arithmetic operators inside (( )):
==, !=, <, >, <=, >=
```

### Commands

```bash
# commands separated by ";" are executed sequentially
command1; command2; command3

# commands separated by "&" are executed in parallel (and in background)
command2 & command2 & command3

# command2 is executed iff command1 returns an exit status of zero
command1 && command2

# command2 is executed iff command1 returns a non-zero exit status
command1 || command2

# execute in subshell
( cd directory && command1 )

# If the value of the expression is non-zero, the return status is 0; otherwise the return status is 1
(( expression ))

# Return a status of 0 or 1 depending on the evaluation of the conditional expression
# Word splitting and pathname expansion are not performed
# Improved version for [ expression ]
[[ expression ]]
```

### Functions

```bash
function my_function {
    local var=$1

    # ...

    # optional return status
    return my_return_status
}

# alternative syntax
my_function () {
    # ...
}

# call function after declaration
my_function my_arg1 my_arg2
```

### Control flow

```bash
# if-else
if (( $a < $b )); then
    # ...
elif (( $a == $b )); then
    # ...
else 
    # ...
fi

# for loop
for i in {1..3}
do
    # ...
done

# for all arguments of function
for arg in "$@"
do
    # ...
done

# directory exists
if [[ -d $directory ]]; then
    # ...
fi

# file exists
if [[ -f $file ]]; then
    # ...
fi

# case
read -p "Continue (yes or no)?" choice
case "$choice" in 
  yes ) 
    # ...
    ;;
  no )
    # ...
    ;;
  * ) 
    # ...
    ;;
esac
```

### Error handling

```bash
exit N
# N = 0: executed successfully
# N != 0: error occured
```
