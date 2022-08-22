#flashcards/rustbook

# Hello World

What is the rust file extension?
?
`.rs`
<!--SR:2022-08-23,4,270-->

How do you compile a rust program, say `main.rs`?
?
`rustc main.rs`
<!--SR:2022-09-04,13,290-->

How do you create a new cargo project, called, say `hello_world`?
?
`cargo new hello_world`
<!--SR:2022-09-03,12,290-->

How do you run a cargo project?
?
`cargo run`
<!--SR:2022-08-31,9,290-->

How do you compile a cargo project?
?
`cargo build`
<!--SR:2022-08-24,5,270-->

What does `cargo check` do?
?
It checks that the cargo project still compiles without producing an executable.
<!--SR:2022-09-03,12,270-->

How do you build a cargo project ready for release?
?
`cargo build --release`
<!--SR:2022-08-23,4,270-->

How do you locally access the rust documentation?
?
`rustup docs`
<!--SR:2022-09-02,11,270-->

How do you manually format a rust file, say `main.rs`?
?
`rustfmt main.rs`
<!--SR:2022-08-24,5,270-->

# Guessing Game

How do you bring the input/output library into scope?
?
`use std::io;`
<!--SR:2022-08-24,5,270-->

What is the identifier for the standard library?
?
`std`
<!--SR:2022-08-31,9,290-->

What is the identifier for the input/output library?
?
`io`
<!--SR:2022-08-23,4,270-->

What is the keyword used to bring libraries into scope?
?
`use`
<!--SR:2022-09-04,13,290-->

What is the prelude?
?
A set of items defined in the standard library that is brought into scope by default into every program.
<!--SR:2022-08-29,7,270-->

How do you define the entrypoint for a rust program?
?
`fn main () {}`
<!--SR:2022-08-23,4,270-->

How do you print a string, say, `"hello"` to stdout?
?
`println!("hello");`
<!--SR:2022-08-23,4,270-->

Are variables mutable or immutable by default?
?
Immutable
<!--SR:2022-08-23,4,270-->

How do you create a new immutable variable `a` set to `5`?
?
`let a = 5;`
<!--SR:2022-09-01,10,290-->

What keyword is used to create variables?
?
`let`
<!--SR:2022-08-24,5,270-->

How do you create a new mutable variable `b` and set it to `5`?
?
`let mut b = 5;`
<!--SR:2022-08-23,4,270-->

What is `String`?
?
A type from the standard library that is a growable, UTF-8 encoded piece of text.
<!--SR:2022-08-25,3,250-->

What is `String: :new`?
?
A function that returns a new instance of `String`.
<!--SR:2022-08-24,5,270-->

What does the `: :` syntax on `String: :new` indicate?
?
That `new` is an associated function of the string type.
<!--SR:2022-08-23,3,250-->

What is an associated function?
?
A function that's implemented on a type, but doesn't have access to a specific instance like a method.
<!--SR:2022-08-24,4,250-->

What does `let mut guess = String: :new()` do, exactly?
?
Creates a mutable variable called guess and binds it to a new, empty instance of the type `String`.
<!--SR:2022-08-24,5,270-->

What does `io: :stdin()` return?
?
An instance of `std: :io: :Stdin`, which is a type that represents a handle to the standard input to the terminal.
<!--SR:2022-08-30,8,250-->

What is `read_line`?
?
A method on the standard input handle to get input from the user.
<!--SR:2022-08-23,4,270-->

How do you get the user's input into a string called `guess`?
?
```
io::stdin()
	.read_line(&mut guess)
```
<!--SR:2022-08-23,1,230-->

What is a `Result`?
?
An enum type that is either `Ok` or `Err`.
<!--SR:2022-08-24,5,270-->

What does the `expect`  method on the `Result` type do?
?
Crash the program with the provided message if the `Result` is an `Err` value.
Return the appropriate value if the `Result` is an `Ok` value.
<!--SR:2022-08-24,5,270-->

How can you use placeholders to print the value "x is 5", where the varialbe `x` has the value `5`?
?
`println!("x is {x}");`
<!--SR:2022-08-24,5,270-->

How can you use multiple placeholders to print the values of `x` and `y`?
?
`println!("x = {}, y = {}", x, y);`
<!--SR:2022-08-23,4,270-->

How do you get access to random numbers in Rust?
?
Using the `rand` crate.
<!--SR:2022-08-24,5,270-->

What two kinds of crates are there and how are they different?
?
Library and binary.
Library crates can't be run but they can be included in other programs.
Binary crates are executables.
<!--SR:2022-08-23,4,270-->

Where are dependency crates defined?
?
`Cargo.toml`
<!--SR:2022-09-02,11,290-->

How do you create a random number between 1 and 100 (inclusive)?
?
```
use rand::Rng;
rand::thread_rng().gen_range(1..=100);
```
<!--SR:2022-08-23,1,190-->

What keyword do we use to get an infinite loop?
?
`loop {}`
<!--SR:2022-08-23,4,270-->

What keyword do we use to break out of an infinite loop?
?
`break`
<!--SR:2022-08-23,4,270-->


# Common Concepts

## Variables

What is wrong with the following code?
```
fn main() {
	let x = 5;
	println!("The value of x is: {x}");
	x = 6;
	println!("The value of x is: {x}");`
}
```
?
cannot assign twice to immutable variable `x`

Why is it useful to create immutable variables in Rust?
?
You might write code that assumes that a variable doesn't change. One part of the code may assume that the variable will never change, and if it does change that will introduce a bug. So it's useful to have the compiler ensure that doesn't happen.

When are constants evalutated?
?
Compile time.

What do constants require that variables don't?
?
A type annotation.

Can constants be mutable?
?
No

What is shadowing?
?
When a new variable is declared with the same name as an old one.

How is shadowing with mutable variables different to having mutable varialbes?
?
The variables are still immutable after the shadowing has been done.
With shadowing, we are making multiple variables but reusing the name for human purposes - the compiler regards them as different variables.

How do you shadow a variable?
?
By reusing the `let` keyword.
```
let x = 5;
let x = 3;
```

What is the output of the following program?
```
fn main() {
	let x = 5;
	let x = x + 1;
	{
		let x = x * 2;
		println!("{x}");
	}
	println!("{x}");
}
```
?
12
6

What is wrong with the following code?
```
fn main() {
	let mut spaces = " ";
	spaces = spaces.len();
	println!("{spaces}");
}
```
?
You can't mutable the type of a variable.

## Data Types

### Integers

What is wrong with the following code?
`let guess = "42".parse().expect("Not a number!");`
?
There needs to be a type annotation on guess, as `parse()` is ambiguous and could give multiple types. I.e.,:
`let guess: u32 = "42".parse().expect("Not a number!");`

What is a scalar type?
?
A type that represents a single value.

What are the main scalar types?
?
Integers
Floating point numbers
Booleans
Characters

What are the different bit sizes available for integers in rust?
?
8, 16, 32, 64, 128, arch

What is the type annotation for an unsigned arch sized integer?
?
`usize`

What are the prefixes to represent signed an unsigned integers?
?
`u` for unsigned
`i` for signed

How are signed integers represented?
?
Using two's complement representation.

What range of values can a signed integer store?
?
$-(2^{n-1})$ to $2^{n-1}-1$, where n is the number of bits

What range of values can an unsigned integer store?
?
$0$ to $2^{n-1}$

What does the `_` mean in a number literal?
?
It's a visual separator to make it easier to read. I.e., `1_000_000`.

What is the visual separator character for number literals?
?
`_`

What is the prefix for hex number literals?
?
`0x`

What is the prefix for octal number literals?
?
`0x`

What is the prefix for binary number literals?
?
`0b`

What is the syntax for byte number literals?
?
`b'A'`, where `A` represents an 8bit integer.

Why might integer overflow cause different kinds of behaviours in Rust?
?
Because compiling in debug mode panics, whereas the overflow actually occurs when the compiler is run in release mode with the `--release` flag.

What do we use to explicitly handle overflowing?
?
Using methods from the standard library that handle the overflow differently than standard arithmetic operators, i.e., `wrapping_add` rather than `+`

What does `wrapping_*` do?
?
Wraps in all modes, (including debug).

What does `checked_*` do?
?
Returns the `None` value if there is overflow.

What does `overflowing_*` do?
?
Return the value and a boolean indicating whether there was overflow.

What does `saturating_*` do?
?
Saturates at the value's maximum or minimum values.

### Floating-point

What are the floating-point types?
?
`f32` and `f64`

What is the default floating-point type and why?
?
`f64`, because it's roughly as fast as `f32` on modern CPUs, and allows more precision.

What standard are floats implemented according to?
?
IEEE-754

What is the output of `println!("{}", 5 / 4);` and why?
?
1, because integer division rounds down to the nearest integer.

### Boolean

How do we write the boolean literals?
?
`true` and `false`

### Characters

How many bytes is a `char`?
?
4

How do we declare a `char`?
?
With single quotes, i.e.;
`let c = 'z';`

What standard does a char represent?
?
A Unicode Scalar Value

### Compound Types

What are the primitive compound types?
?
Arrays and tuples.

#### Tuples

Do tuples have a fixed or variable length?
?
Fixed.

Are type annotations required for tuples?
?
No.

How do you declare a tuple? (give type annotations).
?
`let tup: (i32, f64, u8) = (500, 6.4, 1);`

How do you destructure a tuple?
?
Using pattern matching, i.e.:
`let (x, y, z) = tup;`

How do we directly access a tuple element?
?
Dot notation, i.e.,:
`tup.0`

What is the name for the  tuple without values?
?
The unit

How do you write the unit and its type?
?
Both as `()`

What do expressions implicitly return if they don't return any other value?
?
The unit, i.e., the empty tuple `()`

#### Arrays

Do arrays have fixed or variable lengths?
?
Fixed.

Can the elements in an array have different types from one another?
?
No.

How do you declare an array?
?
`let a = [1,2,3,4];`

Are arrays stored on the stack or the heap?
?
Stack.

What is the more flexible type similar to an array?
?
Vector.

How do you write an array's type?
?
Square brackets and a semicolon, i.e., an array of 5 `i32`s:
````rust
let a: [i32; 5] = [1, 2, 3, 4, 5];
````

How do you write an array filled with the same value?
?
`let a = [3;5]` will make `[3,3,3,3,3]`

What happens if you provide an invalid array access?
?
Panic at runtime (or compile time if it's compile time detectable).
## Functions

