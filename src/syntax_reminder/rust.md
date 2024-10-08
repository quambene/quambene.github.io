<!-- markdownlint-disable MD001 -->

# Rust

- [Print](#print)
- [Variables](#variables)
- [Data types](#data-types)
- [Operators](#operators)
- [Control flow](#control-flow)
- [Functions](#functions)
- [Generics](#generics-parametric-polymorphism)
- [Traits](#traits-ad-hoc-polymorphism)
- [Lifetimes](#lifetimes)
- [Macros](#macros)
- [Error handling](#error-handling)
- [Testing](#testing)
- [Documentation](#documentation)
- [Visibility](#visibility)
- [Modules](#modules)
- [Crates](#crates)
- [Packages](#packages-cargotoml)
- [Cargo (package manager)](#cargo-package-manager)
- [Rustup (toolchain manager)](#rustup-toolchain-manager)

### Print

```rust
let name = "world";
println!("Hello, {}!", name);
println!("Debug: {:?}", name); // for debugging
println!(":#?", my_struct); // pretty-print structs
println!("{:b}", my_int); // binary representation
println!("{:08b}", my_int); // binary representation
```

### Variables

**Reference**: Refer to some value without taking ownership of it.

**Lifetime**: The scope for which a reference is valid.

**Ownership rules**:

- each value in Rust has a variable that’s called its owner
- there can only be one owner at a time
- when the owner goes out of scope, the value will be dropped

**Borrowing rules**:

- at any given time, you can have either one mutable reference or any number of immutable references
- references must always be valid

```rust
let x; // declare
x = 42; // assign value
let x = 42;
let x: i32 = 42; // assign value (typed)
let x = 0b101010; // binary
let x = 0x2a // hex
let x = 0o52 // octal
let _x = 42; // compiler won't warn about variable being unused
let x = x + 1; // shadowing
let mut x; // mutable
let x_borrowed = &x; // reference
let x_owned = *x; // dereferencing
let x: &'a str; // reference with an explicit lifetime
let x: &'a mut str; // mutable reference with an explicit lifetime
let x: *const str; // const pointer (the asterisk isn’t the dereference operator; it’s part of the type name)
let x: *mut str; // mut pointer
const MYCONST: f32 = 3.14; // immutable value
static MYSTATIC: &str = "Rust"; // mutable variable with static lifetime
let r#fn = "name"; // raw identifier for reserved keywords
```

### Data types

```rust
// Basic types
let x: i32; // signed integer
let x: i64;
let x: u32; // unsigned integer
let x: u64;
let x: f32; // floating point
let x: f64;
let x: &str; // borrowed string slice
let x: String; // owned string type
let x: &'static str; // string with static lifetime
let x: bool;
let x: char = 'ℤ'; // unicode character
let x: &[T]; // slice
let x: &mut [T]; // mutable slice

// Type alias
type MyId = u32;
type Point = (u8, u8);

// Array
let arr: [i32; 5] = [1, 2, 3, 4, 5];
let first_arr = arr[0];

// Tuple
let tup: (i32, f64, u8) = (500, 6.4, 1);
let first_tup = tup.0; // access a tuple element
let (x, y, z) = tup; // destructuring

// Vector
let vec: Vec<i32> = Vec::new();
let vec = vec![1, 2, 3];
let first_vec = vec.get(0);
let first_vec = &vec[0];
vec.push(4);

// Slice
// view into a vector, cannot grow
let s = &my_arr[1..3]
let s = &my_vec[1..3]

// Hash map
let mut my_hashmap = HashMap::new();
my_hashmap.insert(String::from("Key1"), String::from("Value1"));

// Enum
enum Option<T> {
    Some(T),
    None,
}

enum Result<T, E> {
    Ok(T),
    Err(E),
}

enum Color {
    Red,
    Green,
    Blue,
}

let red = Color::Red;

// Struct (custom data type)
struct MyStruct; // unit struct
struct MyStruct(i32, i32); // tuple struct
struct Email(String) // newtype pattern

struct User {
    username: String,
    email: String,
}

// Instantiation of struct
let user = User {
    email: String::from("someone@example.com"),
    username: String::from("someusername"),
}

// Store references (see lifetimes)
struct User {
    username: &str,
    email: &str,
}

// Smart pointer (heap allocation)
Box<T> // exclusive ownership
Rc<T> // shared ownership (reference counted)
Arc<T> // shared ownership (atomically reference counted)

// Interior mutability
Cell<T>
RefCell<T>
Mutex<T> // thread-safe
RwLock<T> // thread-safe
```

### Operators

``` rust
// Logical operators
&& // AND
|| // OR
! // NOT

// Arithmetic operators
+ // addition
- // subtraction
* // multiplication
/ // division
num::pow // exponentiation
% // modulo (remainder)
num::integer::div_floor // floor division

// Bitwise operators
& // AND
| // OR
^ // XOR
! // NOT
<< // left shift
>> // right shift
>>> // right shift with zero
(value >> index) & 1 // get bit
value & !(1 << index) // set bit to 0
value | (1 << index) // set bit to 1
value ^ (1 << index) // swap bit
```

More operators: <https://doc.rust-lang.org/book/appendix-02-operators.html>

### Control flow

```rust
// for loop
for element in set {
    // statement
};

// while loop
while i < 3 {
    // statement
};

// if-else
if a < b {
    // statement
} else if a == b {
    // statement
} else {
    // statement
};

// pattern matching
match my_option {
    Some(i) => Some(i + 1),
    None => None,
}

match some_value {
    4 => println!("four"),
    _ => (),
}

// if let
if let Some(i) = my_option {
    println!("Matched {}", i)
} else {
    println!("Didn't match")
}

// while let
while let Some(i) = my_option  {
    println!("Matched {}", i)
}
```

### Functions

```rust
fn my_function(x: i32) -> i32 {
    let y = 3; // statement
    x + y // expression (return value without semicolon)
}

// Method (similar to classes in OOP)
impl MyStruct { // implement struct
    fn my_function(&self) -> i32 {
        // ...
    }
}
my_struct.my_function(); // call method

// Associated function
impl MyStruct {
    fn my_function(x: i32) -> i32 {
        // ...
    }
}
MyStruct::my_function(42); // call associated function

// Closure
let my_closure = |i| i + 1;
let my_closure = |i: i32| -> i32 { i + 1 }; // typed
```

### Generics (parametric polymorphism)

```rust
fn my_generic_function<T>(list: &[T]) -> T {
    // ...
}

impl<T> MyGenericStruct<T> {
    fn my_function(&self) -> &T {
        // ...
    }
}
```

### Traits (ad-hoc polymorphism)

```rust
// A collection of methods defined for an unknown type
trait MyTrait {
    type MyAssociatedType;

    fn new(name: &'static str) -> Self;
    fn my_method(&self, &Self::MyAssociatedType) -> String;
    fn my_default_method(&self) {
        // default implementation
    };
    fn my_associated_funtion() -> String;
}

impl MyTrait for String {
    fn my_method(&self) -> String { format!("string: {}", *self) }
}

impl MyTrait for u8 {
    // ...
}

impl MyTrait for MyStruct {
    // ...
}

// static dispatch
fn do_something<T: MyTrait>(x: T) {
    x.my_method();
}

// dynamic dispatch
fn do_something(x: &MyTrait) { // trait object &MyTrait
    x.my_method();
}

impl dyn MyTrait {
    // ...
}

// trait bounds
struct MyStruct<T: MyTraitBound>(T);

fn my_function<T: MyTraitBound>(t: T) {}

fn my_function(t: impl MyTraitBound) {}

fn my_function<T, U>(t: &T, u: &U) 
where 
    T: Display + Clone,
    U: AsRef<str>,
{}

// Supertrait (a superset of another trait)
trait MyTrait: MySuperTrait {
    fn my_method(&self) -> String;
}
```

### Lifetimes

```rust
/*  Every reference has a lifetime;
    and lifetime parameters for functions or structs
    that use references have to be specified */
fn longest<'a>(x: &'a str, y: &'a str) -> &'a str {
    if x.len() > y.len() {
        x
    } else {
        y
    }
}
```

### Macros

#### Declarative macros

```rust
#[macro_export]
macro_rules! my_macro {
    () => {
        println!("This is my macro!");
    };
}

fn main() {
    my_macro!();
}
```

#### Procedural macros

``` rust
// derive macro
#[derive(MyMacro)]
struct MyStruct

// attribute-like macro
#[route(GET, "/")]
fn index() {}

// function-like macro
unimplemented!()
todo!()
let sql = sql!(select * from posts where id=1);
```

### Error handling

```rust
// ? operator (propagating errors)
fn read_username_from_file() -> Result<String, io::Error> {
    let mut s = String::new();
    File::open("hello.txt")?.read_to_string(&mut s)?;
    Ok(s)
}
```

### Testing

```rust
// Unit tests
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn my_unit_test() {
        let my_res = my_add_function(1, 2);
        assert_eq!(my_res, 3)
    }
}

// Integration tests
// tests/common.rs can be used to share code between integration tests.
```

``` bash
cargo test # Run tests
cargo test -- --nocapture # Show output
cargo test -- --show-output # Show output
cargo test -- --ignored # Run ignored tests
cargo test -- --test-threads=1 # Run tests serially
cargo test --no-run # Compile, but don’t run tests
cargo test my_test_name # Run all tests which names match my_test_name
cargo test my_test_name -- --exact # Run one specific test
cargo test --lib # Run unit tests
cargo test --test '*' # Run integration tests
```

### Documentation

``` rust
// My line comment

/*
    My block comment
*/

/// My doc comment

//! My module-level or crate-level doc comment

// links
/// <https:://my-link.com>

// doc link if item is in scope
/// [`MyStruct`] 

// doc link if item is not in scope
/// [`MyStruct`](super::my_module::MyStruct)
/// [`MyStruct`](crate::my_module::MyStruct)

// doc link if name is ambiguous
/// [`struct@Foo`]
/// [`enum@Foo`]
/// [`foo()`]
/// [`fn@foo`]
/// [`mod@foo`]

// inter-crate doc links in workspaces
/// [`my_crate::MyStruct::my_method`](../my_crate/struct.MyStruct.html#method.my_method)

// define doc link
/// [`MyStruct`]
///
/// [`MyStruct`]: crate::my_module::MyStruct
```

``` bash
cargo doc # Build the documentation
cargo doc --open # Open the documentation
cargo doc --no-deps # Do not build documentation for dependencies
cargo doc --document-private-items # Include non-public items in the documentation
```

- [The rustdoc book, How to write documentation](https://doc.rust-lang.org/rustdoc/how-to-write-documentation.html)
- [`intra_rustdoc_links`](https://rust-lang.github.io/rfcs/1946-intra-rustdoc-links.html)

### Visibility

``` rust
pub struct MyStruct { ... }
pub(crate) struct MyStruct // Use this one, so it is not accidentally exposed to another crate
```

### Modules

```rust
// A collection of items: functions, structs, traits, impl blocks, and other modules
mod my_mod {
    fn my_private_function() {
        // ...
    }

    pub fn my_public_function() {
        // ...
    }

    pub struct MyPublicStruct {
        // ...
    }
}

// absolute path
use crate::my_crate::my_function(); // referring to an item in the module tree

// relative path
self::my_function(); // current module scope
super::my_function(); // parent scope

// external crate
use std::io;

// renaming external crate
use futures as f;
use self::f::Future;

// submodules
foo.rs // module
foo/bar.rs // submodule
```

### Crates

Crate: a tree of modules that produces a library or executable

```bash
cargo init # create binary crate in current directory
cargo new --bin my-bin # create binary crate
cargo new --lib my-lib # create library crate
```

### Packages (Cargo.toml)

Crate registry: <https://crates.io>

```toml
[dependencies]
package_name = "^1.2.3" # < 2.0.0 (caret)
package_name = "~1.2.3" # < 1.3.0 (tilde)
package_name = "1.2.*" # < 1.3.0 (wildcard)
package_name = "=1.2.3" # = 1.2.3
package_name = "*" # > 0.0.0
```

### Cargo (package manager)

```bash
cargo --version # Show cargo version
cargo init # Create binary crate in current directory
cargo new <bin> --bin # Create binary crate
cargo new <lib> --lib # Create library crate
cargo fmt # Format source code
cargo check # Validate source code
cargo run # Run binary in debug mode
cargo run --release # Run binary in release mode
cargo watch -x run # Run and watch for changes
cargo watch -x 'run --bin=my_binary' # Run and watch for changes
cargo test # Run tests
cargo build # Compile source code in debug mode
cargo build --release # Compile source code in release mode
cargo clean # Remove target directory
cargo update # Update dependencies in the Cargo.lock file to the latest version
cargo add <crate> -F <feature> # Add dependency
cargo rm <crate> # Remove dependency
cargo install <crate> # Install Rust binary
cargo bloat --time --release -j 1 # Check which dependencies take the most time to compile
cargo clippy # Run clippy
cargo clippy --fix # Apply fixes automatically
```

### Rustup (toolchain manager)

``` bash
rustup --version
rustup show
rustup self update # Update rustup
rustup update # Update rust compiler
rustup update stable # Update stable rust compiler
rustup toolchain list # List installed toolchains
rustup toolchain install X.X.X # Install specific Rust version
rustup toolchain uninstall X.X.X # Uninstall specific Rust version
rustup toolchain install nightly # Install nightly toolchain
rustup default stable # Set default toolchain
rustup override set X.X.X # Set specific Rust version
rustup override set stable # Switch to stable toolchain
rustup override set nightly # Switch to nightly toolchain
rustup component list # List components
rustup component add <component> # Add component to toolchain
rustup component add <component> --toolchain nightly # Add component to nightly toolchain
rustup target add <target> # Install target for toolchain
rustup target add <target> --toolchain nightly # Install target for nightly toolchain
```
