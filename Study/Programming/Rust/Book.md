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



