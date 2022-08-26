#flashcards/rust_lessons

What trait can we implement for a default function taking no arguments, and why would we?
?
The `Default` trait (in the prelude).
So that where we implement `Default` for `T`, for values of type `t: Option<T>`, we can use methods like `t.unwrap_or_default()` which returns a value of type `T`, either the `Some` inside, or whatever is returned from `default()`.

How do you make a `u8` typed range from, `0` to `24`?
?
`0..26_u8`

How can you remove from a `Vec` in constant time, and what is the downside?
?
`swap_remove`
Doesn't preserve order.