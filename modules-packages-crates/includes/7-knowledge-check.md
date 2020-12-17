# Knowledge check

Why does the following code won't compile?

```rust
mod container {
    pub struct ClosedBox<T> {
	contents: T,
    }
    impl<T> ClosedBox<T> {
	pub fn new(contents: T) -> ClosedBox<T> {
	    ClosedBox { contents: contents }
	}
    }
}

fn main() {
    let closed_box = container::ClosedBox::new("classified information");
    println!("The closed box contains: {}", closed_box.contents);
```

-   The struct `ClosedBox` is generic over the type `T` and `T` cannot be printed using the `"{}"`
    format specifier.
    -   Incorrect. In the example code, `ClosedBox` was used with the concrete type `&str`, which
        does implement the `Display` trait and thus can be formatted using the `"{}`" specifier.
-   The struct `ClosedBox` is private in the `main` function scope.
    -   Incorrect. The `pub` keyword before the `struct ClosedBox` declaration specifies that it is
        accessible whenever the `container` module is visible.
-   The `ClosedBox::new` function is private.
    -   Incorrect. The `pub` keyword before the `fn new` declaration specifies that it is accessible
        whenever the `container` module is visible.
-   The field `contents` of struct `ClosedBox` is private.
    -   Correct
