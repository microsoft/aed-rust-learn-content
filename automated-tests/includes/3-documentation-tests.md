# Documention Tests

The primary way of documenting a Rust library is through annotating the source code with triple
forward slashes, known as *documentation comments*.

Documentation comments are written in markdown and support code blocks in them, so these code blocks
are compiled and used as tests.

To try out this feature, you'll need to create a new library project first.

```sh
$ cargo new --lib basic_math
$ cd basic_math
```

Open the file `src/lib.rs` in your editor and put the following code in it:

```rust
/// Generally, the first line is a brief summary describing the function.
///
/// The next lines present detailed documentation. Code blocks start with triple backquotes and have
/// implicit `fn main()` inside and `extern crate <cratename>`.
///
/// ```
/// let result = basic_math::add(2, 3);
/// assert_eq!(result, 5);
/// ```
pub fn add(a: i32, b: i32) -> i32 {
    a + b
}
```

You can call the test suite for this code with the command `$ cargo test`, and the output would be
like this:

```
$ cargo test
    Finished test [unoptimized + debuginfo] target(s) in 0.00s
     Running target/debug/deps/basic_math-910b859a2a6f3c3f

running 0 tests

test result: ok. 0 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out

   Doc-tests basic_math

running 1 test
test src/lib.rs - add (line 6) ... ok

test result: ok. 1 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out
```
