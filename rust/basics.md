# RUST basics
## features
- good multi-thrading
- type 
- generate documentation
- auto format

## installation
Install toolchain (rustup, cargo, rustc, ...)
~~~bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
~~~
Everything is installed in:
~~~
~/.cargo/bin
~~~

## cargo
cargo is the package manager for rust

### create new project
~~~bash
cargo init <name>
~~~

### compile and run
in the project folder
~~~bash
cargo run
~~~

## comments
~~~rust
// this is a comment
~~~

## data type
### integer type
|Length |signed|unsigned|
|-------|------|--------|
|8 bit  |i8    |u8      |
|16 bit |i16   |u16     |
|32 bit |i32   |u32     |
|64 bit |i64   |u64     |
|126bit |i128  |u128    |

|number literals|example    |
|---------------|-----------|
|decimal        |98_222     |
|hex            |0xff       |
|octal          |0o77       |
|binary         |0b1111_0000|
|byte (u8 only)	|b'A'       |

###  float type
|Length |signed|unsigned|
|-------|------|--------|
|32 bit |f32   |-       |
|64 bit |f64   |-       |

### boolean type
~~~rust
let is_nice: bool = true;
~~~

### char type
~~~rust
let letter: char = 'C';
~~~

### tuple type
~~~rust
let tup: (i32, f64, bool) = (1138, 3.14, false);
~~~

### array type
~~~rust
let a = [1, 2, 3, 4, 5];
let b: [i32; 5] = [1, 2, 3, 4, 5];
~~~
## variables

- a variable can be mutable(can be changed) or immutable(can not be changed after init.)
- by default immutable
- define with keyword "let"
~~~rust
let x = 1138;
let name = "Jean Dujardin";
let is_ok = true;
let mut title = "hello world";
let new_title = title;
~~~

## constants
Can be used in the global scope
~~~rust
const ADDRESS: i32 = 1234;
~~~

## functions
~~~rust
fn add(a: i32, b: i32) -> i32 {
    a + b
}
~~~
The output of the last statement will be returned.
"return" can also be used.

## println macro
~~~rust
let name = "Jean Dujardin";
println!("Hallo");
println!(name);
println!("Your name is {:?}.", name);
println!("Your name is {name}");
println!("Your name is {:?}. {:?} is a nice name.", name, name);
~~~

## if..else
~~~rust
let x = 1138;
if x > 1142 {
    println!("Good");
} else {
    println!("Bad");
}
~~~

## match
Compiler will check if every possibilities are checked
~~~rust
let is_nice = true;
match is_nice {
    true => println!("nice"),
    false => println!("Not nice")
}
~~~
~~~rust
let a = 2;
match a {
    1 => println!("1"),
    2 => println!("2"),
    3 => println!("3"),
    _ => println!("something else")
}
~~~


## loop
~~~rust
let mut i = 0;
loop {
    if i == 5 {
        break;
    }
    i = i + 1;
}
~~~

## while
~~~rust
let mut i = 0;
while i != 5 {
    i = i + 1;
}
~~~

## enum
~~~rust
enum Direction {
    up,
    down,
    left,
    right
}
~~~

## unwrap, unwrap_or_else, expect
Most of the rust functions returns an Enum with an Ok or an Err.
~~~rust
enum Result<T, E> {
    Ok(T),
    Err(E)
}
~~~
### unwrap()
Unwrap will return the data for the `Ok` variant and panik for the `Err` variant.
~~~rust
let variable = function().unwrap();
~~~
### unwrap_or_else(closure)
This function will return the data for the `Ok` variant and run the closure for the `Err` variant.
~~~rust
let variable = function().unwrap_or_else(|error| {
    panik!("Error: {:?}", error);
});
~~~
### expect(string)
This function will return the data for the `Ok` variant and panik with the given string for the `Err` variant.
~~~rust
let variable = function().expect("Error string");
~~~

## closure (anonymous function)
~~~rust
let closure = |x| {
    x + 1;
}
println!("{}", closure(5));
//returns 6
~~~