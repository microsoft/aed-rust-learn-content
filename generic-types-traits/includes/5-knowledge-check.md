# Knowledge check

What does the following type declaration means?

```rust
struct  Content<T: Summary> {
  date_published: Date,
  reviewed: bool,
  content: T
}
```

-   `Content` is a struct that is generic over its `date_published` and `content` fields.
    -   False. The `date_published` is not a generic field. It always receives a value of type `Date`.
-   `Content` is generic over its `content` field, which can be of any type.
    -   False. The `content` field type is restricted for implementors of the `Summary` trait.
-   `Content` is generic over its `content` field, which can be of any type that implements the `Summary` trait.
    -   Correct.
-   `Content` is generic over its field `date_published`, which can be of any type that implements the `Date` trait.
    -   False. `Date` is a type, not a trait, and `Content` is not generic over its `date_published` field.

What does the following function signature means?

```rust
fn print_to_user<T: Display>(data: T) {
  println!("Hey, here is some data: {}", data);
}
```

-   The `data` parameter can be of any type.
    -   False. The type of `data` must be any type that implements the `Display` trait.
-   The `data` parameter is restricted only to types that implements the `Display` trait.
    -   Correct
-   The `data` parameter can be of any type that optionally implements the `Display` trait.
    -   False. It is mandatory that the value passed as the `data` parameter implements the `Display` trait.
-   The `data` parameter is opional.
    -   False. There are no optional parameters in Rust.
