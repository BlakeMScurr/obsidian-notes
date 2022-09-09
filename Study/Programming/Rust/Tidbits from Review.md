#flashcards/rust_lessons

What trait can we implement for a default function taking no arguments, and why would we?
?
The `Default` trait (in the prelude).
So that where we implement `Default` for `T`, for values of type `t: Option<T>`, we can use methods like `t.unwrap_or_default()`.
<!--SR:2022-10-06,27,250-->

What does `unwrap_or_default()` do?
?
Takes an `Option<Default>`, and returns a value of type `T`, either the `Some` inside, or whatever is returned from `default()`
<!--SR:2022-10-07,28,250-->

How do you make a `u8` typed range from, `0` to `26`?
?
`0..26_u8`
<!--SR:2022-09-11,12,250-->

How can you remove from a `Vec` in constant time, and what is the downside?
?
`swap_remove`
Doesn't preserve order.
<!--SR:2022-09-11,12,250-->

How do you add a large collection of items to an `Vec`?
?
`append` for an existing `Vec`, and `extend` for items that aren't already a `Vec`, but implement `IntoIterator`
<!--SR:2022-09-20,14,230-->