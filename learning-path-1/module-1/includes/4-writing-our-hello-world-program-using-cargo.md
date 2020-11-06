# 5. What is Cargo?

Just compiling with `rustc` is fine for simple programs, but as your project grows, you’ll want to
manage all the options and make it easy to share your code.

The good news is when you install `rustup` you’ll also get the latest stable version of the Rust
build tool and package manager, also known as Cargo.

Cargo does lots of things for you:

-   create new project templates with `cargo new`
-   build your project with `cargo build`
-   run your project with `cargo run`
-   test your project with `cargo test`
-   build documentation for your project with `cargo doc`
-   publish a library to crates.io with `cargo publish`


## Writing our Hello World program using Cargo

To start, we’ll use Cargo to make a new project for us.

Make sure you terminal is at our `rust-learning-path` directory and run the following command:

`cargo new hello-cargo`

This will generate a new directory called `hello-cargo` with the following files:

    hello-cargo
    |- Cargo.toml
    |- src
      |- main.rs

`Cargo.toml` is the manifest file for Rust. It’s where you keep metadata for your project, as well as dependencies.

`src/main.rs` is where we’ll write our application code.

You can see that `cargo new` generated a boilerplate "Hello, world!" project for us!
We can run this program by moving into the new directory `helo-cargo` and running this in our
terminal:

You should see this in your terminal:

    $ cd hello-cargo
    $ cargo run
       Compiling hello-cargo v0.1.0 (/tmp/.OFUp/hello-cargo)
        Finished dev [unoptimized + debuginfo] target(s) in 1.59s
         Running `target/debug/hello-cargo`
    Hello, world!

Congratulations! You've just learned how to initialize your first Rust project with Cargo!
