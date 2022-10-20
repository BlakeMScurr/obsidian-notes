#flashcards/rust_lessons

# Truncate PR 1

What trait can we implement for a default function taking no arguments, and why would we?
?
The `Default` trait (in the prelude).
So that where we implement `Default` for `T`, for values of type `t: Option<T>`, we can use methods like `t.unwrap_or_default()`.
<!--SR:2023-01-05,79,250-->

What does `unwrap_or_default()` do?
?
Takes an `Option<Default>`, and returns a value of type `T`, either the `Some` inside, or whatever is returned from `default()`
<!--SR:2023-01-10,84,250-->

How do you make a `u8` typed range from, `0` to `26`?
?
`0..26_u8`
<!--SR:2023-01-19,93,250-->

How can you remove from a `Vec` in constant time, and what is the downside?
?
`swap_remove`
Doesn't preserve order.
<!--SR:2023-01-17,91,250-->

How do you add a large collection of items to an `Vec`?
?
`append` for an existing `Vec`, and `extend` for items that aren't already a `Vec`, but implement `IntoIterator`
<!--SR:2022-11-13,26,190-->

# Truncate PR 2

What is an `AsRef<str>` and why is it useful?
?
Any type that can be a reference to a str.
It lets you accept `String`, `&mut String` , `str` etc etc as an argument to your functions rather than just `&str`, and having to wrangle types.
<!--SR:2022-11-28,41,250-->

What is the `any` function on an iterator?
?
It returns whether any of the elements match the condition of the closure.
<!--SR:2022-11-23,36,250-->

What is `skip`?
?
A method on iterators that skips a certain number of elements.
<!--SR:2022-11-25,36,250-->

What is `step_by`?
?
A method on iterators that makes it step through by a certain number of steps. I.e., `step_by(2)` would make the iterator yield even indexed elements.
<!--SR:2022-11-22,35,250-->

What is `get_mut`?
?
A method on collections that gets a mutable reference to the element at an index. The same as `get` except the returned value is mutable.
<!--SR:2022-11-30,40,250-->

What is `with_capacity`?
?
An associated function on `Vec` that lets you initialised a new `Vec` with a given capacity to save allocations when filling it up.
<!--SR:2022-10-22,17,250-->

What does `..` refer to in a match statement? Say, `if let Some(Square: :Occupied(..))` etc?
<!--SR:2022-09-30,3,250-->
?
Ignore all properties.
Equivalent to `(_, _)` where the enum has 2 properties, for example.
<!--SR:2022-11-23,34,250-->

What is `and_then`?
?
A function on `Option` that runs as closure on the wrapped value, or returns None if the option is None.
<!--SR:2022-10-24,6,210-->