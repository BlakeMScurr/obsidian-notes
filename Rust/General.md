#flashcards 
# General

How do you define a test in rust?
?
With the test attribute: `#[test]`

What is a `collection`?
?
A series of data holding objects, like Vec, VecDeque, BinaryHeap etc.

What does `collect` do?
?
Turns an `Iterator` into a `collection`

What does `.take()` do?
?
Take is implemented on options, and takes a mutable reference to the option, and gives you back that option. It returns None if the Option was None, if it returns something else, it sets the Option to None. "Take", therefore means that the T was taken from this option to a new variable. Type signature:
`impl<T> Option<T> {fn take(&mut self) -> Option<T>`

What does `*` in an expression like `*remainder = something` do?
?
`*` is a deference, it means that the left hand side is not a reference, but rather the place the reference points to. So overall, we are putting `something` in the place the the `remainder` pointer points to.
