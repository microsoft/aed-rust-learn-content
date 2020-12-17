# Exercise - Visibility

Unless otherwise noted, every path in rust is private.

Your assignment in this exercise is to make the following code compile without modifying the `main`
function.

```rust
mod car_factory {
    fn build_car() {
	println!("Honk honk!");
    }
}

fn main() {
    car_factory::build_car();
}
```

Hint: The compiler error should point to the thing that needs to be public.

You can also view this exercise at this [Rust Playground
link](https://play.rust-lang.org/?version=stable&mode=debug&edition=2018&gist=fe45044ec8efe9344f5ed81c7fa3ad06).

To find the sollution for this exercise, check this other [Rust Playground
link](https://play.rust-lang.org/?version=stable&mode=debug&edition=2018&gist=5298832fadbaad2afb8a09cfa0fcac3e).
