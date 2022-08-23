#flashcards/rustbook

# Hello World

What is the rust file extension?
?
`.rs`
<!--SR:2022-09-04,12,270-->

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
<!--SR:2022-09-06,13,270-->

What does `cargo check` do?
?
It checks that the cargo project still compiles without producing an executable.
<!--SR:2022-09-03,12,270-->

How do you build a cargo project ready for release?
?
`cargo build --release`
<!--SR:2022-09-05,13,270-->

How do you locally access the rust documentation?
?
`rustup docs`
<!--SR:2022-09-02,11,270-->

How do you manually format a rust file, say `main.rs`?
?
`rustfmt main.rs`
<!--SR:2022-09-07,14,270-->

# Guessing Game

How do you bring the input/output library into scope?
?
`use std: :io;`
<!--SR:2022-09-06,13,270-->

What is the identifier for the standard library?
?
`std`
<!--SR:2022-08-31,9,290-->

What is the identifier for the input/output library?
?
`io`
<!--SR:2022-09-03,11,270-->

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
<!--SR:2022-09-02,10,270-->

How do you print a string, say, `"hello"` to stdout?
?
`println!("hello");`
<!--SR:2022-09-06,14,290-->

Are variables mutable or immutable by default?
?
Immutable
<!--SR:2022-09-05,13,270-->

How do you create a new immutable variable `a` set to `5`?
?
`let a = 5;`
<!--SR:2022-09-01,10,290-->

What keyword is used to create variables?
?
`let`
<!--SR:2022-09-07,14,270-->

How do you create a new mutable variable `b` and set it to `5`?
?
`let mut b = 5;`
<!--SR:2022-09-05,13,270-->

What is `String`?
?
A type from the standard library that is a growable, UTF-8 encoded piece of text.
<!--SR:2022-08-25,3,250-->

What is `String: :new`?
?
A function that returns a new instance of `String`.
<!--SR:2022-09-06,13,270-->

What does the `: :` syntax on `String: :new` indicate?
?
That `new` is an associated function of the string type.
<!--SR:2022-09-03,11,270-->

What is an associated function?
?
A function that's implemented on a type, but doesn't have access to a specific instance like a method.
<!--SR:2022-09-01,8,250-->

What does `let mut guess = String: :new()` do, exactly?
?
Creates a mutable variable called guess and binds it to a new, empty instance of the type `String`.
<!--SR:2022-09-09,16,270-->

What does `io: :stdin()` return?
?
An instance of `std: :io: :Stdin`, which is a type that represents a handle to the standard input to the terminal.
<!--SR:2022-08-30,8,250-->

What is `read_line`?
?
A method on the standard input handle to get input from the user.
<!--SR:2022-09-07,15,290-->

How do you get the user's input into a string called `guess`?
?
```
io::stdin()
	.read_line(&mut guess)
```
<!--SR:2022-08-27,4,250-->

What is a `Result`?
?
An enum type that is either `Ok` or `Err`.
<!--SR:2022-09-08,15,270-->

What does the `expect`  method on the `Result` type do?
?
Crash the program with the provided message if the `Result` is an `Err` value.
Return the appropriate value if the `Result` is an `Ok` value.
<!--SR:2022-09-08,15,270-->

How can you use placeholders to print the value "x is 5", where the varialbe `x` has the value `5`?
?
`println!("x is {x}");`
<!--SR:2022-09-09,16,270-->

How can you use multiple placeholders to print the values of `x` and `y`?
?
`println!("x = {}, y = {}", x, y);`
<!--SR:2022-09-04,12,270-->

How do you get access to random numbers in Rust?
?
Using the `rand` crate.
<!--SR:2022-09-08,15,270-->

What two kinds of crates are there and how are they different?
?
Library and binary.
Library crates can't be run but they can be included in other programs.
Binary crates are executables.
<!--SR:2022-09-05,13,270-->

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
<!--SR:2022-08-27,3,170-->

What keyword do we use to get an infinite loop?
?
`loop {}`
<!--SR:2022-09-01,9,270-->

What keyword do we use to break out of an infinite loop?
?
`break`
<!--SR:2022-09-01,9,270-->


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
<!--SR:2022-08-27,4,250-->

Why is it useful to create immutable variables in Rust?
?
You might write code that assumes that a variable doesn't change. One part of the code may assume that the variable will never change, and if it does change that will introduce a bug. So it's useful to have the compiler ensure that doesn't happen.
<!--SR:2022-08-28,5,270-->

When are constants evalutated?
?
Compile time.
<!--SR:2022-08-25,2,250-->

What do constants require that variables don't?
?
A type annotation.
<!--SR:2022-08-27,4,250-->

??? Why?

Can constants be mutable?
?
No
<!--SR:2022-08-27,4,250-->

What is shadowing?
?
When a new variable is declared with the same name as an old one.
<!--SR:2022-08-25,2,250-->

How is shadowing with mutable variables different to having mutable varialbes?
?
The variables are still immutable after the shadowing has been done.
With shadowing, we are making multiple variables but reusing the name for human purposes - the compiler regards them as different variables.
<!--SR:2022-08-25,2,250-->

How do you shadow a variable?
?
By reusing the `let` keyword.
```
let x = 5;
let x = 3;
```
<!--SR:2022-08-25,2,250-->

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
<!--SR:2022-08-27,4,250-->

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
<!--SR:2022-08-26,3,250-->

## Data Types

### Integers

What is wrong with the following code?
`let guess = "42".parse().expect("Not a number!");`
?
There needs to be a type annotation on guess, as `parse()` is ambiguous and could give multiple types. I.e.,:
`let guess: u32 = "42".parse().expect("Not a number!");`
<!--SR:2022-08-27,4,250-->

What is a scalar type?
?
A type that represents a single value.
<!--SR:2022-08-27,3,230-->

What are the main scalar types?
?
Integers
Floating point numbers
Booleans
Characters
<!--SR:2022-08-27,4,250-->

What are the different bit sizes available for integers in rust?
?
8, 16, 32, 64, 128, arch
<!--SR:2022-08-25,2,250-->

What is the type annotation for an unsigned arch sized integer?
?
`usize`
<!--SR:2022-08-25,2,250-->

What are the prefixes to represent signed an unsigned integers?
?
`u` for unsigned
`i` for signed
<!--SR:2022-08-26,3,250-->

How are signed integers represented?
?
Using two's complement representation.
<!--SR:2022-08-25,2,250-->

What range of values can a signed integer store?
?
$-(2^{n-1})$ to $2^{n-1}-1$, where n is the number of bits
<!--SR:2022-08-28,5,270-->

What range of values can an unsigned integer store?
?
$0$ to $2^n-1$
<!--SR:2022-08-25,2,250-->

What does the `_` mean in a number literal?
?
It's a visual separator to make it easier to read. I.e., `1_000_000`.
<!--SR:2022-08-28,5,270-->

What is the visual separator character for number literals?
?
`_`
<!--SR:2022-08-27,4,250-->

What is the prefix for hex number literals?
?
`0x`
<!--SR:2022-08-27,4,250-->

What is the prefix for octal number literals?
?
`0o`
<!--SR:2022-08-26,3,250-->

What is the prefix for binary number literals?
?
`0b`
<!--SR:2022-08-26,2,230-->

What is the syntax for byte number literals?
?
`b'A'`, where `A` represents an 8bit integer.
<!--SR:2022-08-25,2,250-->

Why might integer overflow cause different kinds of behaviours in Rust?
?
Because compiling in debug mode panics, whereas the overflow actually occurs when the compiler is run in release mode with the `--release` flag.
<!--SR:2022-08-27,4,250-->

What do we use to explicitly handle overflowing?
?
Using methods from the standard library that handle the overflow differently than standard arithmetic operators, i.e., `wrapping_add` rather than `+`
<!--SR:2022-08-28,5,270-->

What are the different method prefixes for handling overflow explicitly?
?
`wrapping`, `checked`, `overflowing`, `saturating`.
<!--SR:2022-08-25,1,210-->

What does `wrapping_*` do?
?
Wraps in all modes, (including debug).
<!--SR:2022-08-26,3,250-->

What does `checked_*` do?
?
Returns the `None` value if there is overflow.
<!--SR:2022-08-26,2,230-->

What does `overflowing_*` do?
?
Return the value and a boolean indicating whether there was overflow.
<!--SR:2022-08-25,1,210-->

What does `saturating_*` do?
?
Saturates at the value's maximum or minimum values.
<!--SR:2022-08-26,3,250-->

### Floating-point

What are the kinds of floating-point types?
?
`f32` and `f64`
<!--SR:2022-08-28,5,270-->

What is the default floating-point type and why?
?
`f64`, because it's roughly as fast as `f32` on modern CPUs, and allows more precision.
<!--SR:2022-08-28,5,270-->

What standard are floats implemented according to?
?
IEEE-754
<!--SR:2022-08-25,2,250-->

What is the output of `println!("{}", 5 / 4);` and why?
?
1, because integer division rounds down to the nearest integer.
<!--SR:2022-08-25,2,250-->

### Boolean

How do we write the boolean literals?
?
`true` and `false`
<!--SR:2022-08-27,4,250-->

### Characters

How many bytes is a `char`?
?
4
<!--SR:2022-08-25,2,250-->

How do we declare a `char`?
?
With single quotes, i.e.;
`let c = 'z';`
<!--SR:2022-08-26,3,250-->

What standard does a char represent?
?
A Unicode Scalar Value
<!--SR:2022-08-26,2,230-->

### Compound Types

What are the primitive compound types?
?
Arrays and tuples.
<!--SR:2022-08-26,3,250-->

#### Tuples

Do tuples have a fixed or variable length?
?
Fixed.
<!--SR:2022-08-26,3,250-->

Are type annotations required for tuples?
?
No.
<!--SR:2022-08-26,3,250-->

How do you declare a tuple? (give type annotations).
?
`let tup: (i32, f64, u8) = (500, 6.4, 1);`
<!--SR:2022-08-28,5,270-->

How do you destructure a tuple?
?
Using pattern matching, i.e.:
`let (x, y, z) = tup;`
<!--SR:2022-08-25,2,250-->

How do we directly access a tuple element?
?
Dot notation, i.e.,:
`tup.0`
<!--SR:2022-08-26,3,250-->

What is the name for the  tuple without values?
?
The unit
<!--SR:2022-08-25,2,250-->

How do you write the unit and its type?
?
Both as `()`
<!--SR:2022-08-26,3,250-->

What do expressions implicitly return if they don't return any other value?
?
The unit, i.e., the empty tuple `()`
<!--SR:2022-08-27,4,250-->

#### Arrays

Do arrays have fixed or variable lengths?
?
Fixed.
<!--SR:2022-08-26,3,250-->

Can the elements in an array have different types from one another?
?
No.
<!--SR:2022-08-26,3,250-->

How do you declare an array?
?
`let a = [1,2,3,4];`
<!--SR:2022-08-27,4,250-->

Are arrays stored on the stack or the heap?
?
Stack.
<!--SR:2022-08-25,2,250-->

What is the more flexible type similar to an array?
?
Vector.
<!--SR:2022-08-27,4,250-->

How do you write an array's type?
?
Square brackets and a semicolon, i.e., an array of 5 `i32`s:
````rust
let a: [i32; 5] = [1, 2, 3, 4, 5];
````
<!--SR:2022-08-27,4,250-->

How do you write an array filled with the same value? (show the fully explicit way of writing it too).
?
`let a = [3;5]` will make `[3,3,3,3,3]`
<!--SR:2022-08-26,3,250-->

What happens if you provide an invalid array access?
?
Panic at runtime (or compile time if it's compile time detectable).
<!--SR:2022-08-25,2,250-->

## Functions


What is the conventional case for writing variables and functions?
?
snake_case
<!--SR:2022-08-26,3,250-->

What's the keyword for creating functions?
?
`fn`
<!--SR:2022-08-27,4,250-->

Can you call a function that is defined later in a scope?
?
Yes.
<!--SR:2022-08-26,3,250-->

What is the difference between a parameter and argument?
?
A parameter is the name for something passed into a function in the function definition, and an argument is a concrete value passed into a specific function call.
<!--SR:2022-08-27,4,250-->

How could you define a function that takes a `i32` parameter called `x`?
?
`fn foo(x: i32) {}`
<!--SR:2022-08-27,3,230-->

Do you have to put type annotations on function parameters? Why?
?
Yes, because it means that they rarely have to be used elsewhere, as the compiler can infer the types from that.
<!--SR:2022-08-27,4,250-->

What is the difference between a statement and an expression?
?
_Statements_ are instructions that perform some action and do not return a value.
_Expressions_ evaluate to a resulting value.
<!--SR:2022-08-27,4,250-->

Does `let` create an expression or a statement?
?
Statement.
<!--SR:2022-08-26,3,250-->

Are function definitions expressions or statements?
?
Statements.
<!--SR:2022-08-25,2,250-->

What is wrong with the following code?
```
fn main() { 
	let x = (let y = 6); 
}
```
?
It expects a statement to evaluate to a value.
<!--SR:2022-08-26,3,250-->

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
<!--SR:2022-08-27,4,250-->

What is the syntactic difference between statements and expressions?
?
Statements end in a semicolon, and expressions do not.
<!--SR:2022-08-27,4,250-->

How do you make scopes created with curly brackets into expressions?
?
By ending them in an expression, which the whole scope evaluates to.
<!--SR:2022-08-25,2,250-->

How do you write a function that returns an `i32`?
?
`fn foo () -> i32 {}`
<!--SR:2022-08-27,4,250-->

Do you have to declare the return type of a function?
?
Yes.
<!--SR:2022-08-27,4,250-->

How do you return a value from a function?
?
By ending the function's block with an expression of that value, or using the `return` keyword earlier.
<!--SR:2022-08-26,3,250-->

What character creates comments?
?
`//`
<!--SR:2022-08-27,4,250-->

How do you do multiline comments?
?
`//` on each line
<!--SR:2022-08-27,4,250-->

## Control Flow
### If

Do `if` expressions require brackets for the condition?
?
No.
<!--SR:2022-08-25,2,250-->

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
<!--SR:2022-08-25,2,250-->

Does rust convert non boolean types by default?
?
No.
<!--SR:2022-08-25,2,250-->

Does rust have a ternary operator? Why?
?
No, because if/else expressions do the same thing with (arguably) clearer syntax.
<!--SR:2022-08-26,3,250-->

### Loops

#### Loop

How do you return a value from a `loop`?
?
By passing a value to the `break` statement, i.e.:
`break x + 2;`
<!--SR:2022-08-25,2,250-->

What is a loop label for?
?
Disambiguating between multiple loops, so you can break from the correct one.
<!--SR:2022-08-26,3,250-->

What is the syntax for creating and using a loop label?
?
Start with a single backtick.
Declare before the `loop` keyword with a colon.
```
'counting_up: loop {
	...
	break 'counting_up;
```
<!--SR:2022-08-27,4,250-->

What is a `while` loop for?
?
Looping while a condition is true, which saves code compared to implementing the same behaviour using `loop`, `if/else`, and `break`
<!--SR:2022-08-26,3,250-->

Can you use labels and breaks with a `while` loop?
?
Yes.
<!--SR:2022-08-25,2,250-->

Can `while` loops return a value?
?
No.
<!--SR:2022-08-26,3,250-->

??? Can you use labels and breaks with a `for` loop?

What does a `for` loop do? Why does it exist?
?
Loops over a collection with simpler syntax than the equivalent `while` loop (which has to keep track of an index, and concern itself with index out of bounds errors).
<!--SR:2022-08-26,3,250-->

How do you write a `for` loop? Say, over an array literal `[1,2,3]`, printing each value.
?
```
for x in [1,2,3] {
	println!("{x}");
}
```
<!--SR:2022-08-26,3,250-->

How do you make a range from 1 to 4?
?
`1..4`
<!--SR:2022-08-27,3,230-->

How do you make a range from 4 down to 1?
?
`(1..4).rev()`
<!--SR:2022-08-26,3,250-->

Can we shorten `+= 1` with `++`? Why?
?
No.
Because it can be understood to return a value, which can lead to subtle bugs.
<!--SR:2022-08-26,3,250-->

# Ownership

## Ownership

What is the purpose of ownership?
?
To make memory safety guarantees without needing a garbage collector.
<!--SR:2022-08-26,3,250-->

What is ownership?
?
A set of rules governing how rust manages memory.
<!--SR:2022-08-25,2,250-->

When are ownership rules checked?
?
Compile time.
<!--SR:2022-08-25,2,250-->

### The Stack and the Heap

How does the stack work, roughly?
?
Data can be pushed on or popped off, and nothing else is possible.
<!--SR:2022-08-26,3,250-->

Which is faster to push to, the stack or the heap? Why?
?
The stack. 
Because the allocator doesn't have to look for a location for the new data - it's always at the top of the stack.
<!--SR:2022-08-27,4,250-->

Which is faster to pull from, the stack or the heap? Why?
?
The stack.
Because of the cost to the processor of moving around memory. Values on the stack are near each other, whereas values on the heap can be far away.
<!--SR:2022-08-27,4,250-->

What kind of data can be put on the stack?
?
Data with a known size at compile time.
<!--SR:2022-08-25,2,250-->

Where is data with unknown size at compile time stored?
?
The heap.
<!--SR:2022-08-25,2,250-->

How does allocating on the heap work, roughly?
?
You request a certain amount of memory.
The allocator finds some memory.
The allocator returns a _pointer_, which is the address of the location.
<!--SR:2022-08-26,2,230-->

How is the stack used by functions?
?
When a function is called, the values passed to the function are pushed to the stack.
When the function is over, those values are popped off the stack.
<!--SR:2022-08-26,3,250-->

What problems does heap has, that ownership addresses?
?
Keeping track of what parts of code are using what data on the heap.
Minimizing duplicate data on the heap.
Cleaning up unused data to make sure you don't run out of space.
<!--SR:2022-08-25,1,210-->

### Ownership Rules

What are the ownership rules?
?
Each value has an owner.
There can only be one owner at a time.
When the owner goes out of scope, the value is dropped.
<!--SR:2022-08-25,2,250-->

What is the relationship between variable validity and scope?
?
When a variable comes into scope it is valid.
When it goes out of scope it's invalid.
<!--SR:2022-08-25,2,250-->

### Strings

How do you create a new string of type `String` from a string literal, say, `"hello"`?
?
`let x = String::from("hello");`
<!--SR:2022-08-27,4,250-->

How do you push a new string literal to a `String`?
?
`s.push_str("literal");`
<!--SR:2022-08-27,4,250-->

Why are string literals more efficient than mutable strings?
?
Because their size is known at compile time, and it hardcoded into the executable, whereas this can't be done for strings that could change size.
<!--SR:2022-08-26,2,230-->

How do we request memory from the allocator for a new string?
?
`String::from("literal");` does this for us.
<!--SR:2022-08-25,2,250-->

What function is called for us when a variable goes out of scope?
?
`drop`
<!--SR:2022-08-25,2,250-->


What is wrong with the following code?
```
let s1 = String::from("hello"); 
let s2 = s1; 
println!("{}, world!", s1);
```
?
`s1` is being moved when it is assigned to `s2`, so it is no longer accessible.
<!--SR:2022-08-25,2,250-->

Why can't strings be accessed after they're moved?
?
When they're moved you end up with two variables pointing at the same memory, and if the first variable were still accessible you could cause memory issues (like double dropping memory as the two variables go out of scope).
<!--SR:2022-08-27,3,230-->

What does `drop` do?
?
Deallocates the memory for that variable.
<!--SR:2022-08-26,3,250-->

What's the difference between a shallow copy and a move?
?
Moves are shallow copies where the first variable is invalidated.
<!--SR:2022-08-26,3,250-->

When is automatic copying deep vs shallow?
?
Rust never does automatic deep copying.
<!--SR:2022-08-26,3,250-->

How do you clone a `String`?
?
`let s2 = s1.clone();`
<!--SR:2022-08-27,4,250-->

Why aren't integers moved when another value is assigned to their value?
?
Because they live solely on the stack, and can be efficiently copied.
<!--SR:2022-08-27,4,250-->

What trait indicates that a type lives on the stack?
?
The `Copy` trait.
<!--SR:2022-08-25,2,250-->

What trait can't coexist with the `Copy` trait, and how exactly?
?
`Drop`.
If the type or any of its parts implement `Drop`, it can't implement `Copy`.
<!--SR:2022-08-28,5,270-->

What kinds of types tend to implement the `Copy` trait?
?
Groups of scalar values.
<!--SR:2022-08-26,2,230-->

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
<!--SR:2022-08-27,4,250-->

What operations can move a value?
?
Assingment, and function calls.
<!--SR:2022-08-27,4,250-->

How can you return ownership that was taken by a function?
?
By returning the value.
<!--SR:2022-08-26,3,250-->


## References and Borrowing



