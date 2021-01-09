# Knowledge check

When are Rust traits useful?

- When a function or struct needs to accept optional parameters.
  - False. In Rust there are no optional parameters in function or struct signatures.
- When we need to specify function or struct parameters in terms of of behaviour instead of concrete value.
  - True. Rust traits are useful when we want to specify functions or struct parameters.
- When we need to avoid the compile time guarantees of the Borrow Checker.
  - False. Rust compile time guarantees can't be affected by using Traits
- When we need our values to continue valid even past their lifefime scope.
  - False. Traits can't alter when values go out of scope.

What does the following function signature mean? `fn show_on_screen<T: Display>(data: T)`

- The `data` parameter can be of any type.
  - False. The type of `data` must be any type that implements the `Display` trait.
- The `data` parameter is restricted only to types that implements the `Display` trait.
  - Correct. The data parameter can only have types which implement the  `Display` trait.
- The `data` parameter can be of any type that optionally implements the `Display` trait.
  - False. It is mandatory that the value passed as the `data` parameter implements the `Display` trait.
- The `data` parameter is optional.
  - False. There are no optional parameters in Rust.
