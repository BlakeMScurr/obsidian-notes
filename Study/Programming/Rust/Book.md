#flashcards/rustbook

# Hello World

What is the rust file extension?
?
`.rs`
<!--SR:2022-10-12,37,270-->

How do you compile a rust program, say `main.rs`?
?
`rustc main.rs`
<!--SR:2022-10-06,24,270-->

How do you create a new cargo project, called, say `hello_world`?
?
`cargo new hello_world`
<!--SR:2022-10-11,37,290-->

How do you run a cargo project?
?
`cargo run`
<!--SR:2022-12-15,78,290-->

How do you compile a cargo project?
?
`cargo build`
<!--SR:2022-10-11,35,270-->

What does `cargo check` do?
?
It checks that the cargo project still compiles without producing an executable.
<!--SR:2022-10-12,38,270-->

How do you build a cargo project ready for release?
?
`cargo build --release`
<!--SR:2022-10-13,38,270-->

How do you locally access the rust documentation?
?
`rustup docs`
<!--SR:2022-10-05,33,270-->

How do you manually format a rust file, say `main.rs`?
?
`rustfmt main.rs`
<!--SR:2022-10-16,39,270-->

# Guessing Game

How do you bring the input/output library into scope?
?
`use std: :io;`
<!--SR:2022-10-09,33,270-->

What is the identifier for the standard library?
?
`std`
<!--SR:2022-12-20,82,290-->

What is the identifier for the input/output library?
?
`io`
<!--SR:2022-10-07,33,270-->

What is the keyword used to bring libraries into scope?
?
`use`
<!--SR:2022-10-13,39,290-->

What is the prelude?
?
A set of items defined in the standard library that is brought into scope by default into every program.
<!--SR:2022-11-24,63,270-->

How do you define the entrypoint for a rust program?
?
`fn main () {}`
<!--SR:2022-10-01,29,270-->

How do you print a string, say, `"hello"` to stdout?
?
`println!("hello");`
<!--SR:2022-10-17,41,290-->

Are variables mutable or immutable by default?
?
Immutable
<!--SR:2022-10-11,36,270-->

How do you create a new immutable variable `a` set to `5`?
?
`let a = 5;`
<!--SR:2022-10-04,33,290-->

What keyword is used to create variables?
?
`let`
<!--SR:2022-10-18,41,270-->

How do you create a new mutable variable `b` and set it to `5`?
?
`let mut b = 5;`
<!--SR:2022-10-09,34,270-->

What is `String`?
?
A type from the standard library that is a growable, UTF-8 encoded piece of text.
<!--SR:2022-11-16,54,250-->

What is `String: :new`?
?
A function that returns a new instance of `String`.
<!--SR:2022-10-15,39,270-->

What does the `: :` syntax on `String: :new` indicate?
?
That `new` is an associated function of the string type.
<!--SR:2022-10-06,32,270-->

What is an associated function?
?
A function that's implemented on a type, but doesn't have access to a specific instance like a method.
<!--SR:2022-11-18,56,250-->

What does `let mut guess = String: :new()` do, exactly?
?
Creates a mutable variable called guess and binds it to a new, empty instance of the type `String`.
<!--SR:2022-10-26,47,270-->

What does `io: :stdin()` return?
?
An instance of `std: :io: :Stdin`, which is a type that represents a handle to the standard input to the terminal.
<!--SR:2022-12-01,65,250-->

What is `read_line`?
?
A method on the standard input handle to get input from the user.
<!--SR:2022-10-19,42,290-->

How do you get the user's input into a string called `guess`?
?
```
io::stdin()
	.read_line(&mut guess)
```
<!--SR:2022-10-05,7,190-->

What is a `Result`?
?
An enum type that is either `Ok` or `Err`.
<!--SR:2022-10-23,44,270-->

What does the `expect`  method on the `Result` type do?
?
Crash the program with the provided message if the `Result` is an `Err` value.
Return the appropriate value if the `Result` is an `Ok` value.
<!--SR:2022-10-24,45,270-->

How can you use placeholders to print the value "x is 5", where the varialbe `x` has the value `5`?
?
`println!("x is {x}");`
<!--SR:2022-10-22,43,270-->

How can you use multiple placeholders to print the values of `x` and `y`?
?
`println!("x = {}, y = {}", x, y);`
<!--SR:2022-10-08,34,270-->

How do you get access to random numbers in Rust?
?
Using the `rand` crate.
<!--SR:2022-10-25,46,270-->

What two kinds of crates are there and how are they different?
?
Library and binary.
Library crates can't be run but they can be included in other programs.
Binary crates are executables.
<!--SR:2022-10-14,39,270-->

Where are dependency crates defined?
?
`Cargo.toml`
<!--SR:2022-11-18,51,270-->

How do you create a random number between 1 and 100 (inclusive)?
?
```
use rand::Rng;
rand::thread_rng().gen_range(1..=100);
```
<!--SR:2022-10-16,19,150-->

What keyword do we use to get an infinite loop?
?
`loop {}`
<!--SR:2022-12-08,72,270-->

What keyword do we use to break out of an infinite loop?
?
`break`
<!--SR:2022-11-29,63,270-->


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
<!--SR:2022-10-08,31,250-->

Why is it useful to create immutable variables in Rust?
?
You might write code that assumes that a variable doesn't change. One part of the code may assume that the variable will never change, and if it does change that will introduce a bug. So it's useful to have the compiler ensure that doesn't happen.
<!--SR:2022-10-20,39,270-->

When are constants evalutated?
?
Compile time.
<!--SR:2022-11-07,49,250-->

What do constants require that variables don't?
?
A type annotation.
<!--SR:2022-11-14,45,230-->

??? Why?

Can constants be mutable?
?
No
<!--SR:2022-10-09,30,250-->

What is shadowing?
?
When a new variable is declared with the same name as an old one.
<!--SR:2022-10-17,35,250-->

How is shadowing with mutable variables different to having mutable varialbes?
?
The variables are still immutable after the shadowing has been done.
With shadowing, we are making multiple variables but reusing the name for human purposes - the compiler regards them as different variables.
<!--SR:2022-10-20,37,250-->

How do you shadow a variable?
?
By reusing the `let` keyword.
```
let x = 5;
let x = 3;
```
<!--SR:2022-10-29,40,250-->

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
<!--SR:2022-10-13,34,250-->

What is wrong with the following code?
```
fn main() {
	let mut spaces = " ";
	spaces = spaces.len();
	println!("{spaces}");
}
```
?
You can't assign a new type of value to a variable, even if it's mutable.
<!--SR:2022-11-15,54,250-->

## Data Types

### Integers

What is wrong with the following code?
`let guess = "42".parse().expect("Not a number!");`
?
There needs to be a type annotation on guess, as `parse()` is ambiguous and could give multiple types. I.e.,:
`let guess: u32 = "42".parse().expect("Not a number!");`
<!--SR:2022-10-11,32,250-->

What is a scalar type?
?
A type that represents a single value.
<!--SR:2022-11-23,55,230-->

What are the main scalar types?
?
Integers
Floating point numbers
Booleans
Characters
<!--SR:2022-10-03,27,250-->

What are the different bit sizes available for integers in rust?
?
8, 16, 32, 64, 128, arch
<!--SR:2022-11-01,43,250-->

What is the type annotation for an unsigned arch sized integer?
?
`usize`
<!--SR:2022-11-07,49,250-->

What are the prefixes to represent signed an unsigned integers?
?
`u` for unsigned
`i` for signed
<!--SR:2022-11-28,61,250-->

How are signed integers represented?
?
Using two's complement representation.
<!--SR:2022-10-31,42,250-->

What range of values can a signed integer store?
?
$-(2^{n-1})$ to $2^{n-1}-1$, where n is the number of bits
<!--SR:2022-10-16,36,270-->

What range of values can an unsigned integer store?
?
$0$ to $2^n-1$
<!--SR:2022-11-07,49,250-->

What does the `_` mean in a number literal?
?
It's a visual separator to make it easier to read. I.e., `1_000_000`.
<!--SR:2022-10-28,45,270-->

What is the visual separator character for number literals?
?
`_`
<!--SR:2022-10-03,27,250-->

What is the prefix for hex number literals?
?
`0x`
<!--SR:2022-10-10,31,250-->

What is the prefix for octal number literals?
?
`0o`
<!--SR:2022-10-03,28,250-->

What is the prefix for binary number literals?
?
`0b`
<!--SR:2022-10-19,34,230-->

What is the syntax for byte number literals?
?
`b'A'`, where `A` represents an 8bit integer.
<!--SR:2022-11-01,43,250-->

Why might integer overflow cause different kinds of behaviours in Rust?
?
Because compiling in debug mode panics, whereas the overflow actually occurs when the compiler is run in release mode with the `--release` flag.
<!--SR:2022-10-14,35,250-->

What do we use to explicitly handle overflowing?
?
Using methods from the standard library that handle the overflow differently than standard arithmetic operators, i.e., `wrapping_add` rather than `+`
<!--SR:2022-10-23,41,270-->

What are the different method prefixes for handling overflow explicitly?
?
`wrapping`, `checked`, `overflowing`, `saturating`.
<!--SR:2022-10-06,9,170-->

What does `wrapping_*` do?
?
Wraps in all modes, (including debug).
<!--SR:2022-11-14,53,250-->

What does `checked_*` do?
?
Returns the `None` value if there is overflow.
<!--SR:2022-10-31,42,230-->

What does `overflowing_*` do?
?
Return the value and a boolean indicating whether there was overflow.
<!--SR:2022-10-09,12,130-->

What does `saturating_*` do?
?
Saturates at the value's maximum or minimum values.
<!--SR:2022-12-06,67,250-->

### Floating-point

What are the kinds of floating-point types?
?
`f32` and `f64`
<!--SR:2022-10-27,45,270-->

What is the default floating-point type and why?
?
`f64`, because it's roughly as fast as `f32` on modern CPUs, and allows more precision.
<!--SR:2022-10-29,46,270-->

What standard are floats implemented according to?
?
IEEE-754
<!--SR:2022-10-23,39,250-->

What is the output of `println!("{}", 5 / 4);` and why?
?
1, because integer division rounds down to the nearest integer.
<!--SR:2022-10-24,40,250-->

### Boolean

How do we write the boolean literals?
?
`true` and `false`
<!--SR:2022-10-07,30,250-->

### Characters

How many bytes is a `char`?
?
4
<!--SR:2022-10-13,30,230-->

How do we declare a `char`?
?
With single quotes, i.e.;
`let c = 'z';`
<!--SR:2022-11-13,52,250-->

What standard does a char represent?
?
A Unicode Scalar Value
<!--SR:2022-11-09,40,210-->

### Compound Types

What are the primitive compound types?
?
Arrays and tuples.
<!--SR:2022-10-23,30,210-->

#### Tuples

Do tuples have a fixed or variable length?
?
Fixed.
<!--SR:2022-11-06,48,250-->

Are type annotations required for tuples?
?
No.
<!--SR:2022-12-05,66,250-->

How do you declare a tuple? (give type annotations).
?
`let tup: (i32, f64, u8) = (500, 6.4, 1);`
<!--SR:2022-10-19,38,270-->

How do you destructure a tuple?
?
Using pattern matching, i.e.:
`let (x, y, z) = tup;`
<!--SR:2022-10-11,31,250-->

How do we directly access a tuple element?
?
Dot notation, i.e.,:
`tup.0`
<!--SR:2022-11-27,60,250-->

What is the name for the  tuple without values?
?
The unit
<!--SR:2022-11-03,45,250-->

How do you write the unit and its type?
?
Both as `()`
<!--SR:2022-11-11,51,250-->

What do expressions implicitly return if they don't return any other value?
?
The unit, i.e., the empty tuple `()`
<!--SR:2022-10-04,28,250-->

#### Arrays

Do arrays have fixed or variable lengths?
?
Fixed.
<!--SR:2022-11-18,52,250-->

Can the elements in an array have different types from one another?
?
No.
<!--SR:2022-12-02,64,250-->

How do you declare an array?
?
`let a = [1,2,3,4];`
<!--SR:2022-10-10,31,250-->

Are arrays stored on the stack or the heap?
?
Stack.
<!--SR:2022-11-05,47,250-->

What is the more flexible type similar to an array?
?
Vector.
<!--SR:2022-10-17,28,250-->

How do you write an array's type?
?
Square brackets and a semicolon, i.e., an array of 5 `i32`s:
````rust
let a: [i32; 5] = [1, 2, 3, 4, 5];
````
<!--SR:2022-10-04,18,230-->

How do you write an array filled with the same value? (show the fully explicit way of writing it too).
?
`let a = [3;5]` will make `[3,3,3,3,3]`
<!--SR:2022-11-25,59,250-->

What happens if you provide an invalid array access?
?
Panic at runtime (or compile time if it's compile time detectable).
<!--SR:2022-10-18,36,250-->

## Functions


What is the conventional case for writing variables and functions?
?
snake_case
<!--SR:2022-10-02,27,250-->

What's the keyword for creating functions?
?
`fn`
<!--SR:2022-10-04,28,250-->

Can you call a function that is defined later in a scope?
?
Yes.
<!--SR:2022-10-01,26,250-->

What is the difference between a parameter and argument?
?
A parameter is the name for something passed into a function in the function definition, and an argument is a concrete value passed into a specific function call.
<!--SR:2022-10-04,28,250-->

How could you define a function that takes a `i32` parameter called `x`?
?
`fn foo(x: i32) {}`
<!--SR:2022-11-10,48,230-->

Do you have to put type annotations on function parameters? Why?
?
Yes, because it means that they rarely have to be used elsewhere, as the compiler can infer the types from that.
<!--SR:2022-10-04,28,250-->

What is the difference between a statement and an expression?
?
_Statements_ are instructions that perform some action and do not return a value.
_Expressions_ evaluate to a resulting value.
<!--SR:2022-11-22,55,250-->

Does `let` create an expression or a statement?
?
Statement.
<!--SR:2022-10-02,27,250-->

Are function definitions expressions or statements?
?
Statements.
<!--SR:2022-11-02,44,250-->

What is wrong with the following code?
```
fn main() { 
	let x = (let y = 6); 
}
```
?
It expects a statement to evaluate to a value.
<!--SR:2022-11-26,60,250-->

What does the following code print?
```
fn main() {
	let y = {
		let x = 3;
		x + 1
	};
	println!("The value of y is: {y}");
}
```
?
The value of y is: 4
<!--SR:2022-11-16,50,250-->

What is the syntactic difference between statements and expressions?
?
Statements end in a semicolon, and expressions do not.
<!--SR:2022-10-05,28,250-->

How do you make scopes created with curly brackets into expressions?
?
By ending them in an expression, which the whole scope evaluates to.
<!--SR:2022-11-06,48,250-->

How do you write a function that returns an `i32`?
?
`fn foo () -> i32 {}`
<!--SR:2022-10-12,33,250-->

Do you have to declare the return type of a function?
?
Yes.
<!--SR:2022-10-19,35,250-->

How do you return a value from a function?
?
By ending the function's block with an expression of that value, or using the `return` keyword earlier.
<!--SR:2022-10-27,41,250-->

What character creates comments?
?
`//`
<!--SR:2022-10-14,35,250-->

How do you do multiline comments?
?
`//` on each line
<!--SR:2022-10-06,29,250-->

## Control Flow
### If

Do `if` expressions require brackets for the condition?
?
No.
<!--SR:2022-11-04,46,250-->

What is wrong with the following code?
```
fn main() { 
	let number = 3; 
	if number { 
		println!("number was three"); 
	} 
}
```
?
We need a bool in the if's condition, whereas we have an int.
<!--SR:2022-10-25,41,250-->

Does rust convert non boolean types by default?
?
No.
<!--SR:2022-11-06,48,250-->

Does rust have a ternary operator? Why?
?
No, because if/else expressions do the same thing with (arguably) clearer syntax.
<!--SR:2022-11-08,49,250-->

### Loops

#### Loop

How do you return a value from a `loop`?
?
By passing a value to the `break` statement, i.e.:
`break x + 2;`
<!--SR:2022-11-03,45,250-->

What is a loop label for?
?
Disambiguating between multiple loops, so you can break from the correct one.
<!--SR:2022-10-15,32,230-->

What is the syntax for creating and using a loop label?
?
Start with a single backtick.
Declare before the `loop` keyword with a colon.
```
'counting_up: loop {
	...
	break 'counting_up;
```
<!--SR:2022-10-01,25,250-->

What is a `while` loop for?
?
Looping while a condition is true, which saves code compared to implementing the same behaviour using `loop`, `if/else`, and `break`
<!--SR:2022-10-01,26,250-->

Can you use labels and breaks with a `while` loop?
?
Yes.
<!--SR:2022-10-20,35,250-->

Can `while` loops return a value?
?
No.
<!--SR:2022-10-02,9,170-->

??? Can you use labels and breaks with a `for` loop?

What does a `for` loop do? Why does it exist?
?
Loops over a collection with simpler syntax than the equivalent `while` loop (which has to keep track of an index, and concern itself with index out of bounds errors).
<!--SR:2022-10-01,26,250-->

How do you write a `for` loop? Say, over an array literal `[1,2,3]`, printing each value.
?
```
for x in [1,2,3] {
	println!("{x}");
}
```
<!--SR:2022-10-03,28,250-->

How do you make a range from 1 to 4?
?
`1..4`
<!--SR:2022-11-15,49,230-->

How do you make a range from 4 down to 1?
?
`(1..4).rev()`
<!--SR:2022-10-03,28,250-->

Can we shorten `+= 1` with `++`? Why?
?
No.
Because it can be understood to return a value, which can lead to subtle bugs.
<!--SR:2022-11-22,56,250-->

# Ownership

## Ownership

What is the purpose of ownership?
?
To make memory safety guarantees without needing a garbage collector.
<!--SR:2022-11-12,52,250-->

What is ownership?
?
A set of rules governing how rust manages memory.
<!--SR:2022-11-02,44,250-->

When are ownership rules checked?
?
Compile time.
<!--SR:2022-11-04,46,250-->

### The Stack and the Heap

How does the stack work, roughly?
?
Data can be pushed on or popped off, and nothing else is possible.
<!--SR:2022-10-02,27,250-->

Which is faster to push to, the stack or the heap? Why?
?
The stack. 
Because the allocator doesn't have to look for a location for the new data - it's always at the top of the stack.
<!--SR:2022-10-08,29,250-->

Which is faster to pull from, the stack or the heap? Why?
?
The stack.
Because of the cost to the processor of moving around memory. Values on the stack are near each other, whereas values on the heap can be far away.
<!--SR:2022-10-09,32,250-->

What kind of data can be put on the stack?
?
Data with a known size at compile time.
<!--SR:2022-10-07,28,250-->

Where is data with unknown size at compile time stored?
?
The heap.
<!--SR:2022-10-21,38,250-->

How does allocating on the heap work, roughly?
?
You request a certain amount of memory.
The allocator finds some memory.
The allocator returns a _pointer_, which is the address of the location.
<!--SR:2022-10-21,36,230-->

How is the stack used by functions?
?
When a function is called, the values passed to the function are pushed to the stack.
When the function is over, those values are popped off the stack.
<!--SR:2022-10-19,30,210-->

What problems does the heap have, that ownership addresses?
?
Keeping track of what parts of code are using what data on the heap.
Minimizing duplicate data on the heap.
Cleaning up unused data to make sure you don't run out of space.
<!--SR:2022-10-30,33,190-->

### Ownership Rules

What are the ownership rules?
?
Each value has an owner.
There can only be one owner at a time.
When the owner goes out of scope, the value is dropped.
<!--SR:2022-10-04,25,230-->

What is the relationship between variable validity and scope?
?
When a variable comes into scope it is valid.
When it goes out of scope it's invalid.
<!--SR:2022-11-05,47,250-->

### Strings

How do you create a new string of type `String` from a string literal, say, `"hello"`?
?
`let x = String: :from("hello");`
<!--SR:2022-10-06,29,250-->

How do you push a new string literal to a `String`?
?
`s.push_str("literal");`
<!--SR:2022-10-27,34,250-->

Why are string literals more efficient than mutable strings?
?
Because their size is known at compile time, and it hardcoded into the executable, whereas this can't be done for strings that could change size.
<!--SR:2022-10-25,39,230-->

How do we request memory from the allocator for a new string?
?
`String: :from("literal");` does this for us.
<!--SR:2022-10-26,40,250-->

What function is called for us when a variable goes out of scope?
?
`drop`
<!--SR:2022-11-04,46,250-->


What is wrong with the following code?
```
let s1 = String: :from("hello"); 
let s2 = s1; 
println!("{}, world!", s1);
```
?
`s1` is being moved when it is assigned to `s2`, so it is no longer accessible.
<!--SR:2022-10-22,38,250-->

Why can't strings be accessed after they're moved?
?
When they're moved you end up with two variables pointing at the same memory, and if the first variable were still accessible you could cause memory issues (like double dropping memory as the two variables go out of scope).
<!--SR:2022-11-10,42,210-->

What does `drop` do?
?
Deallocates the memory for that variable.
<!--SR:2022-11-30,62,250-->

What's the difference between a shallow copy and a move?
?
Moves are shallow copies where the first variable is invalidated.
<!--SR:2022-11-29,62,250-->

When is automatic copying deep vs shallow?
?
Rust never does automatic deep copying.
<!--SR:2022-11-28,60,250-->

How do you clone a `String`?
?
`let s2 = s1.clone();`
<!--SR:2022-12-04,65,250-->

Why aren't integers moved when another value is assigned to their value?
?
Because they live solely on the stack, and can be efficiently copied.
<!--SR:2022-10-04,28,250-->

What trait indicates that a type lives on the stack?
?
The `Copy` trait.
<!--SR:2022-10-25,39,250-->

What trait can't coexist with the `Copy` trait, and how exactly?
?
`Drop`.
If the type or any of its parts implement `Drop`, it can't implement `Copy`.
<!--SR:2022-10-16,33,250-->

What kinds of types tend to implement the `Copy` trait?
?
Groups of scalar values.
<!--SR:2022-10-17,33,230-->

What's wrong with the following code?
```
fn main() {
	let s = String::from("hello");
	f(s);
	println!("{}", s)
}
fn f(s: String) {
	println!("{}", s);
}
```
?
`s` is moved by the call `f(s)`, so it's inaccessible on the next line.
<!--SR:2022-10-07,30,250-->

What operations can move a value?
?
Assingment, and function calls.
<!--SR:2022-10-06,29,250-->

How can you return ownership that was taken by a function?
?
By returning the value.
<!--SR:2022-11-08,49,250-->


## References and Borrowing


# MISSING 4.2 to 6.3
# Module System
## Packages and Crates

What are the components of the module system?
?
Packages
Crates
Modules
Paths
<!--SR:2022-10-22,37,250-->

What is a crate?
?
A tree of modules that produces a library or executable.
<!--SR:2022-10-12,28,230-->

What are the types of crate?
?
Binary and library.
<!--SR:2022-10-02,26,250-->

What kinds of crates have a main function?
?
Binary, not library.
<!--SR:2022-11-11,49,250-->

What is a crate root?
?
The file containing the root module of a crate.
<!--SR:2022-10-15,32,230-->

What is a package?
?
A bundle of crates.
<!--SR:2022-10-05,16,230-->

How many crates can/must a package have?
?
As many binary packages as it likes.
At most one library crate.
At least one crate.
<!--SR:2022-10-16,34,250-->

What is the name and type of the crate whose root is at `src/main.rs`?
?
A binary crate named the same as the package.
<!--SR:2022-10-14,31,230-->

What is the name and type of the crate whose root is at `src/lib.rs`?
?
A library crate named the same as the package.
<!--SR:2022-11-25,58,250-->

Where do extra binary packages go?
?
`src/bin`
<!--SR:2022-10-16,34,250-->

## Modules

Where does the compiler look first when compiling a crate?
?
The crate root.
<!--SR:2022-10-03,24,230-->

Where would the compiler look for, say, the `garden` module declared in the crate root?
?
Inline, within curly brackets that replace the semicolon following `mod garden`,
In the file `src/garden.rs`,
Or in the file `src/garden/mod.rs`
<!--SR:2022-10-28,42,250-->

Where can you declare submodules?
?
Any file but the crate root.
<!--SR:2022-10-20,31,210-->

Where would the compiler look for, say, the `vegetables` module declared in `src/garden.rs`?
?
Inline in curly brackets directly following `mod vegetables`,
In the file `src/garden/vegetables.rs`,
Or in the file `src/garden/vegetables/mod.rs`
<!--SR:2022-10-02,25,250-->

When can you refer to code in another module?
?
Whenever that module is part of the same crate, as long as privacy allows.
<!--SR:2022-10-21,35,230-->

How do you make code in a module public and private?
?
The whole module is private by default.
Use `pub mod` when declaring the module to make the module public.
Use `pub` before any declarations in the module to make those items public.
<!--SR:2022-10-02,21,230-->

What does `use` do for a module within the same crate?
?
Creates a shortcut.
I.e., after `use crate: :garden: :vegetables: :asparagus` you can refer directly to `asparagus`
<!--SR:2022-11-24,58,250-->

## Paths

What kinds of paths are there?
?
Absolute and relative.
<!--SR:2022-10-01,25,250-->

What does an absolute path start with?
?
The literal `crate`, referring to the crate root.
<!--SR:2022-10-17,35,250-->

What does a relative path start with?
?
`self`, `super`, or an identifier in the current module.
<!--SR:2022-10-12,29,230-->

What is the path delimiter?
?
`::`
<!--SR:2022-10-05,28,250-->

Are modules private or public by default?
?
Private
<!--SR:2022-10-21,37,250-->

Are functions, structs, etc private or public by default?
?
Private
<!--SR:2022-11-23,57,250-->

Are fields on structs public or private by default?
?
Private
<!--SR:2022-11-08,47,250-->

Does making a struct public make its fields public?
?
No
<!--SR:2022-11-03,45,250-->

Does making a module public make its functions and structs etc public?
?
No
<!--SR:2022-10-24,39,250-->

How do you create shortcuts to paths?
?
With the `use` keyword
<!--SR:2022-11-09,47,250-->

Do `use` shortcuts apply in child modules defined in the same file?
?
No
<!--SR:2022-10-22,36,230-->

How do you use `use` paths idiomatically?
?
`use` the module and call its functions off that module.
`use` structs, enums, and other items directly
<!--SR:2022-10-14,17,230-->

What keyword do we use to create aliases?
?
`as`
<!--SR:2022-10-16,32,230-->

How do you import `std: :io: :Result` as `IoResult`?
?
`use std: :io: :Result as IoResult;`
<!--SR:2022-11-21,55,250-->

How do you re-export?
?
`pub use crate: :thingA: :thingB;`
<!--SR:2022-11-17,51,250-->

What is re-exporting for?
?
Organising the API of your code when its internals are structured differently to how programmers using it would think about the domain.
<!--SR:2022-11-19,53,250-->

How can you rewrite the following code with nested paths?
```
use std::cmp::Ordering;
use std::io;
```
?
`use std::{cmp::Ordering, io};`
<!--SR:2022-10-05,28,250-->

How can you rewrite the following code with nested paths?
```
use std: :io;
use std: :io: :Write;
```
?
`use std: :io::{self, Write};`
<!--SR:2022-10-16,32,230-->

How could you bring everything in `std: :collections` into scope?
?
`use std: :collections: :*;`
<!--SR:2022-11-20,54,250-->

What two things does `use` do?
?
Creates shortcuts to accessible code in other submodules of the crate.
Brings inaccessible code from external packages into scope.
<!--SR:2022-10-05,24,230-->

# MISSING 8
# Error Handling

What are the two major categories of errors?
?
Recoverable and unrecoverable.
<!--SR:2022-11-05,47,250-->

## Panic

What do we use for unrecoverable errors?
?
The `panic!` macro
<!--SR:2022-11-25,59,250-->

How do you use `panic!`?
?
Pass a string (etc) to it:
`panic!("you didn't do this right");`
<!--SR:2022-10-19,37,250-->

How can you find the stacktrace for a panic?
?
By running with the environment variable `RUST_BACKTRACE=1`, i.e.,:
`RUST_BACKTRACE=1 cargo run`
<!--SR:2022-10-08,26,230-->

## Result

What do we use for recoverable errors?
?
The `Result` type.
<!--SR:2022-10-17,34,250-->

What is the definition of the `Result` type?
?
```
enum Result<T, E> {
	Ok(T),
	Err(E),
}
```
<!--SR:2022-10-30,41,250-->

How do you open a file called `"hello.txt"`?
?
```
use std::fs::File;
File::open("hello.txt");
```
<!--SR:2022-10-03,6,130-->

What is the basic way to handle `Result` errors (without methods of the result type), for say, opening a file?
?
Matching on the type of the `Result` enum, i.e.,:
```Rust
let greeting_file_result = File::open("hello.txt");
let greeting_file = match greeting_file_result {
	Ok(file) => file,
	Err(error) => panic!("Problem opening the file: {:?}", error),
};
```
<!--SR:2022-10-18,33,230-->

Are `Result` and its variants in the prelude?
?
Yes.
<!--SR:2022-10-28,42,250-->

How do you match on the "file not found" error type?
?
```Rust
use std::io::ErrorKind;
// ...
fn main() {
	// ...
	match error.kind() {
		ErrorKind::NotFound => //...
	}
}
```
<!--SR:2022-10-04,7,170-->

What method can we use to clean up nested match statements when dealing with errors?
?
`unwrap_or_else`
<!--SR:2022-10-29,37,230-->

What does `unwrap_or_else` do?
?
Returns the unwrapped value inside `Ok` if the `Result` is `Ok`, otherwise runs a closure to handle the `Err` and returns the result from that closure.
<!--SR:2022-11-01,35,230-->

What are the shortcut methods for panicking on error?
?
`unwrap` and `expect`
<!--SR:2022-10-30,31,210-->

What does `unwrap` do?
?
Returns the unwrapped value inside `Ok` if the `Result` is `Ok`, otherwise panics on the `Err`'s value.
<!--SR:2022-10-15,18,170-->

What does `expect` do?
?
Returns the unwrapped value inside `Ok` if the `Result` is `Ok`, otherwise panics with the message passed as an argument to `expect`.
<!--SR:2022-10-14,23,210-->

Which of `expect` and `unwrap` is generally preferred for production code and why?
?
`expect` because it gives more information in the error, and can explain your assumptions about why the code is always expected to succeed.
<!--SR:2022-10-13,22,230-->

## Propogation

How do you propogate an error up to the parent function?
?
By returning a `Result` type.
<!--SR:2022-11-29,60,250-->

What is the fully explicit method for handling and propogating an error?
?
Match the result, return the error in a new `Err` type, i.e.;
```
match something {
	Ok(inner_value) => Ok(inner_value),
	Err(e) => return Err(e), 
}
```
<!--SR:2022-10-18,36,250-->

What does the `?` operator do?
?
If the `Result` is `Ok` it just evalutes to the value inside the `Ok` and the code continues through the current function. If the `Result` is `Err`, it returns that error from the current function.
<!--SR:2022-11-17,51,250-->

What is the difference between `?` and the basic manual way of propogating errors (by matching on the `Result`'s type and returning if it's an `Err`)?
?
`?` calls the `from` function defined on the `From` trait in the standard library, which converts the error type to the error type of the current function.
<!--SR:2022-11-21,55,250-->

When can you use the `?` operator?
?
On a `Result` type in a function that returns a `Result`, or on an `Option` type in a function that returns an `Option`.
<!--SR:2022-11-06,40,230-->

How can you use the `?` operator in the `main` function?
?
By setting the return type of main to `Result<(), Box<dyn Error>>`
<!--SR:2022-10-02,4,190-->

How can we understand `Box<dyn Error>` at a high level?
?
As "any kind of error."
<!--SR:2022-10-25,35,230-->

What happens when a main function with a return type of `Result<(), E>` returns?
?
If it returns `Ok`, the executable exits with `0`.
It returns a non zero exit value if it returns an `Err` value.
<!--SR:2022-10-12,32,250-->

What kinds of types can the main function return?
?
Types that implement the `std: :process: :Termination` trait.
<!--SR:2022-10-09,19,170-->

## When to Panic!

When might you want to `panic!` instead of using the `Result` type?
?
When writing examples, prototypes, or test code.
Or to catch developer errors where there are logical issues that the compiler can't catch, i.e., parsing a hardcoded IP address.
Or to stop your code proceeding in a bad state.
<!--SR:2022-11-01,43,250-->

# Generics, Traits, and Lifetimes

## Outline

What are generics?
?
Abstract stand-ins for concrete types or other properties.
<!--SR:2022-11-13,44,230-->

What do traits do, broadly, as opposed to generics?
?
Traits abstract/generalise over behaviour.
Generics let different concrete types use the same behaviour with the same function call.
Traits let different concrete types use different behaviour with the same function call.
<!--SR:2022-10-20,36,250-->

What are lifetimes?
?
Generics that give the compiler information about how references relate to each other.
<!--SR:2022-10-29,38,230-->

## Generics

What is the conventional case for naming types?
?
CamelCase
<!--SR:2022-10-26,40,250-->

What is the conventional name for a generic type?
?
`T`
<!--SR:2022-10-08,28,250-->

Where do you declare a type parameter name in a function?
?
In angle brackets between the function name and the parameter list.
<!--SR:2022-10-13,32,250-->

What is the function signature for the `largest` method which is generic over types?
?
`fn largest<T: std::cmp::PartialOrd>(list: &[T]) -> &T {}`
<!--SR:2022-11-05,39,210-->

How do you make sure the value for a generic type parameter of a function can be compared?
?
`fn foo<T: std: :cmp: :PartialOrd>(...) {}`, by specifying the partial order trait on the type parameter.
<!--SR:2022-10-12,12,170-->

# Missing ...
Up to: file:///Users/blakemcalevey-scurr/.rustup/toolchains/stable-x86_64-apple-darwin/share/doc/rust/html/book/ch10-01-syntax.html#in-struct-definitions 

# Testing

## How to Write Tests

What is an attribute, broadly?
?
A piece of metadata about a piece of code.
<!--SR:2022-10-19,35,250-->

How do you change a function into a test function?
?
Adding `#[test]` on the line before `fn`
<!--SR:2022-10-09,29,250-->

What is `#[test]`?
?
The test attribute.
<!--SR:2022-10-06,27,250-->

What command do we use to run test?
?
`cargo test`
<!--SR:2022-10-10,30,250-->

What is the testing template that Cargo automatically gives us when writing a library crate?
?
```
#[cfg(test)]
mod tests {
	#[test]
	fn it_works() {
		let result = 2 + 2;
		assert_eq!(result, 4);
	}
}
```
<!--SR:2022-10-04,23,230-->

What does the `0 measured` statistic that is often output from `cargo test` mean?
?
That there are no benchmark tests. I.e., tests to measure performance.
<!--SR:2022-10-06,27,250-->

What does the `0 ignored` statistic that is often output from `cargo test` mean?
?
That there are no tests marked to be ignored (unless specifically requested).
<!--SR:2022-10-28,42,250-->

What does the `0 filtered` statistic that is often output from `cargo test` mean?
?
That there are no tests that are filtered out by our argument to `cargo test`
<!--SR:2022-10-23,38,250-->

When do tests fail?
?
When the test panics.
<!--SR:2022-10-09,29,250-->

What does `assert_eq!` do?
?
Panics if the values passed in are not equal, nothing otherwise.
<!--SR:2022-10-27,41,250-->

What does `assert!` do?
?
Panics if passed false, nothing if passed true.
<!--SR:2022-10-12,32,250-->

What does `assert_ne!` do?
?
Panics if the two arguments are equal, nothing otherwise.
<!--SR:2022-10-23,38,250-->

Which argument passed to `assert` etc is considered "expected" and which is "actual"?
?
Neither, in Rust they are just called left and right.
<!--SR:2022-10-14,33,250-->

What traits must arguments passed to `assert_eq!` and `assert_neq!` implement and why?
?
`PartialEq` because they're compared using `==` and `!=` respectively.
`Debug` because they're printed using debug formatting.
<!--SR:2022-10-15,34,250-->

How do you derive the traits required to use a struct/enum as an argument to `assert_eq!`?
?
`#[derive(PartialEq, Debug)]`
<!--SR:2022-10-31,33,210-->

What are the main assertion macros?
?
`assert!`, `assert_eq!`, and `assert_ne!`
<!--SR:2022-10-09,27,230-->

How do you add custom failure messages to `assert!`, `assert_eq!`, and `assert_ne!`?
?
Passing a format string and any values it requires after the required arguments.
I.e.,:
```rust
assert!(
	result.contains("Carol"),
	"Greeting did not contain name, value was `{}`",
	result
);
```
<!--SR:2022-10-10,30,250-->

How do you test that a function panics?
?
By adding the `should_panic` attribute, i.e.:
```rust
#[test]
#[should_panic]
fn some_test() {
	...
}
```
<!--SR:2022-10-22,37,250-->

How do you test that a function panics with a specific message?
?
By setting the expected panic message in the `shoud_panic attribute`, i.e.,:
```rust
#[test]
#[should_panic(expected = "some particular panic message")]
fn some_test() {
	...
}
```
<!--SR:2022-11-04,38,230-->

How do you make a test that can return an error?
?
Just change the function signature to return some kind of result, i.e.:
```
#[test]
fn some_test() -> Result<(), String> {
	...
}
```
<!--SR:2022-10-13,32,250-->

Why write tests that return `Result`s?
?
So you can use the question mark operator in the body of the tests, so you can conveniently fail if there is an `Err`.
<!--SR:2022-10-07,28,250-->

How do you assert that a result is an err?
?
`assert!(value.is_err())` - not by using the question mark operator.
<!--SR:2022-10-04,13,210-->

Can you use the `#[should_panic]` annotation on tests that return `Result`s?
?
No
<!--SR:2022-10-14,33,250-->

## How Tests are Run