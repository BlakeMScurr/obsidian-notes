## Static lifetime

How long does the static lifetime last?
?
The duration of the program - essentially forever.

To what can you assign a variable with a static lifetime?
?
Any variable with the same type and a shorter lifetime, that is, any variable of the same type.

Are all lifetimes static by default?
?
No, lifetimes are generally limited to the length they are required for. I.e., the lifetime of a variable defined in a function and not returned from it will only last until the function returns (i.e., when the stack frame is popped).

How do we know quoted strings have static lifetimes?
?
They are literally in the binary of your code, and therefore they are kept in readonly memory for the duration of the program. Therefore a pointer into that part of the program's memory will always remain valid, and point to the same correct data.

## 

When are lifetimes ended by default?
?
When variables go out of scope or are moved.

What does it mean for a variable to be moved?
?
Rust variables are in charge of freeing their own resources, and therefore only have one owner. That owner can be moved as we pass variables into functions, or we move heap allocated data from one variable to another in the same scope. Rust is unusual in that once this is done, you can't access the data from the earlier non-owning scope/variable.