# Define shared behavior with traits

A trait is a common interface that a group of types can implement. In more technical terms, a trait
describes an abstract interface that types can implement.

The Rust's standard library has a lot of useful traits, such as:

-   `io::Read` for values that can read bytes from a source.
-   `io::Write` for values that can write out bytes.
-   `Debug` for values that can be printed in the console using the "{:?}" format specifier.
-   `Clone` for values that can be explicitly duplicated in memory.
-   `ToString` for values that can be converted to a `String`.
-   `Default` for types that have a sensible default value, like zero for numbers, empty for
    vectors, “” for `String`, etc.
-   `Iterator` for types that can produce a sequence of values.

Each trait definition is a collection of methods defined for an unknown type, usually representing a
capability or behaviour that it's implementors can do.

To represent the concept of "having a 2-dimensional area", we could define the following trait:

```rust
trait Area {
    fn area(&self) -> f64;
}
```

Here, we declare a trait using the `trait` keyword and then the trait’s name, which is `Area` in
this case.

Inside the curly brackets, we declare the method signatures that describe the behaviors of the types
that implement this trait, which in this case is the funtcion signature `fn area(&self) -> f64`. The
compiler will then check that each type implementing this trait must provide its own custom behavior
for the body of the method.

Now, lets create some new types that will implement our `Area` trait:

```rust
struct Circle {
    radius: f64,
}

struct Rectangle {
    width: f64,
    height: f64,
}

impl Area for Circle {
    fn area(&self) -> f64 {
	use std::f64::consts::PI;
	PI * self.radius.powf(2.0)
    }
}

impl Area for Rectangle {
    fn area(&self) -> f64 {
	self.width * self.height
    }
}
```

To implement a trait for a type, we use the keywords `impl Trait for Type`, where `Trait` is the
name of the trait being implemented and `Type` is the name of the implementor struct or the enum.

Within the `impl` block, we put the method signatures that the trait definition has required,
filling the method body with the specific behavior that we want the methods of the trait to have for
the particular type.

When a type implements a given trait it is promising to uphold its contract. After implementing the
trait, we can call the methods on instances of `Circle` and `Rectangle` in the same way we call
regular methods, like this:

```rust
let circle = Circle { radius: 5.0 };
let rectangle = Rectangle {
    width: 10.0,
    height: 20.0,
};

println!("Circle area: {}", circle.area());
println!("Rectangle area: {}", rectangle.area());
```

You can interact with this code at this [Rust Playground link
](https://play.rust-lang.org/?version=stable&mode=debug&edition=2018&gist=62d721bd992978bf8c822154b65c013f).

# Derive

You might have noticed that our custom types are a little unwieldy to use in practice. This simple
`Point` struct cannot be compared to other `Point` instances or displayed in the therminal.

The following code example will fail for three reasons:

```rust
struct Point {
    x: i32,
    y: i32,
}

fn main() {
    let p1 = Point { x: 1, y: 2 };
    let p2 = Point { x: 4, y: -3 };

    if p1 == p2 {          // can't compare two Point values!
	println!("equal!");
    } else {
	println!("not equal!");
    }

    println!("{}", p1);     // can't print using the '{}' format specifier!
    println!("{:?}", p1);  //  can't print using the '{:?}' format specifier!

}
```

    error[E0277]: `Point` doesn't implement `std::fmt::Display`
      --> src/main.rs:10:20
       |
    10 |     println!("{}", p1);
       |                    ^^ `Point` cannot be formatted with the default formatter
       |
       = help: the trait `std::fmt::Display` is not implemented for `Point`
       = note: in format strings you may be able to use `{:?}` (or {:#?} for pretty-print) instead
       = note: required by `std::fmt::Display::fmt`
       = note: this error originates in a macro (in Nightly builds, run with -Z macro-backtrace for more info)

    error[E0277]: `Point` doesn't implement `Debug`
      --> src/main.rs:11:22
       |
    11 |     println!("{:?}", p1);
       |                      ^^ `Point` cannot be formatted using `{:?}`
       |
       = help: the trait `Debug` is not implemented for `Point`
       = note: add `#[derive(Debug)]` or manually implement `Debug`
       = note: required by `std::fmt::Debug::fmt`
       = note: this error originates in a macro (in Nightly builds, run with -Z macro-backtrace for more info)

    error[E0369]: binary operation `==` cannot be applied to type `Point`
      --> src/main.rs:13:11
       |
    13 |     if p1 == p2 {
       |        -- ^^ -- Point
       |        |
       |        Point
       |
       = note: an implementation of `std::cmp::PartialEq` might be missing for `Point`

    error: aborting due to 3 previous errors#+end_example

This code fails to compiple because our `Point` type does not implement the following traits:

-   the `Debug` trait, that allows a type to be formatted using the `{:?}` format specifier, used in
    a programmer-facing, debugging context.
-   the `Display` trait, that allows a type to be formatted using the `{}` format specifier, is
    similar to `Debug`, but Display is better suited for user-facing output.
-   the `PartialEq` trait, that allows implementors to be compared for equality.

Luckily, the `Debug` and `PartialEq` traits can be automatically implemented for us by the Rust
compiler using the `#[derive(Trait)]` attribute, provided that each of its fields implements the
trait:

```rust
#[derive(Debug, PartialEq)]
struct Point {
    x: i32,
    y: i32,
}
```

Our code will still fail to compile because Rust's standard library does not provide automatic
implementation for the `Display` trait, since it is meant for end-users, but if we comment out that
line our code would now produce this output:

    Point { x: 1, y: 2 }
    not equal!

Nevertheless, we can implement the `Display` trait for our type by ourselves:

```rust
use std::fmt;

impl fmt::Display for Point {
    fn fmt(&self, f: &mut fmt::Formatter<'_>) -> fmt::Result {
	write!(f, "({}, {})", self.x, self.y)
    }
}
```

and our code wil then compile just fine:

    (1, 2)
    Point { x: 1, y: 2 }
    not equal!

Check out the code of this example at this [Rust Playground link
](https://play.rust-lang.org/?version=stable&mode=debug&edition=2018&gist=83e972b28e9d02bd93540f9e292ad20b).

# Trait Bounds // Generic Functions

Traits let us define functions that accept many different types, because when a type implements a
trait it can be treated abstractly as that trait.

We can declare function arguments to be an anonymous type parameter where the callee must provide a
type that has the bounds declared by the anonymous type parameter.

Lets imagine that we are writing a web application and would like to have a interface for
serializing values to the JSON format. We could write a trait like this:

```rust
trait AsJson {
    fn as_json(&self) -> String;
}
```

And then we could write a function that accepts any type that implements the `AsJson` trait. They
are written as `impl` followed by a set of trait bounds.

```rust
fn send_data_as_json(value: &impl AsJson) {
    println!("Sending JSON data to server...");
    println!("-> {}", value.as_json());
    println!("Done!\n");
}
```

Instead of a concrete type for the `item` parameter, we specify the `impl` keyword and the trait
name. This parameter accepts any type that implements the specified trait. Note that since the
function doesn't know anything about the concrete type it will receive, it can only use the methods
available by the trait bounds of the anonymous type parameter.

Another way to write the same function, but with a litte different syntax, that explicictly tells
that T is a generic type that must implement the `AsJson` trait:

```rust
fn send_data_as_json<T: AsJson>(value: &T) { ... }
```

We can then declare our types and implement the `AsJson` trait for them:

```rust
struct Person {
    name: String,
    age: u8,
    favorite_fruit: String,
}

struct Dog {
    name: String,
    color: String,
    likes_petting: bool,
}

impl AsJson for Person {
    fn as_json(&self) -> String {
	format!(
	    r#"{{ "type": "person", "name": "{}", "age": {}, "favoriteFruit": "{}" }}"#,
	    self.name, self.age, self.favorite_fruit
	)
    }
}

impl AsJson for Dog {
    fn as_json(&self) -> String {
	format!(
	    r#"{{ "type": "dog", "name": "{}", "color": "{}", "likesPetting": {} }}"#,
	    self.name, self.color, self.likes_petting
	)
    }
}
```

Now that both `Person` and `Dog` implements the `AsJson` trait, we can use them as input parameters
for our `send_data_as_json` function.

```rust
fn main() {
    let laura = Person {
	name: String::from("Laura"),
	age: 31,
	favorite_fruit: String::from("apples"),
    };

    let fido = Dog {
	name: String::from("Fido"),
	color: String::from("Black"),
	likes_petting: true,
    };

    send_data_as_json(&laura);
    send_data_as_json(&fido);
}
```

But what happens when we pass a type that doesn't implement the expected trait to the function? Lets
create a new struct and see what happens:

```rust
struct Cat {
    name: String,
    sharp_claws: bool,
}

let kitty = Cat {
    name: String::from("Kitty"),
    sharp_claws: false,
};

send_data_as_json(&kitty);
```

The compiler raises the following error:

    error[E0277]: the trait bound `Cat: AsJson` is not satisfied
      --> src/main.rs:70:23
       |
    5  | fn send_data_as_json(value: &impl AsJson) {
       |                                   ------ required by this bound in `send_data_as_json`
    ...
    70 |     send_data_as_json(&kitty);
       |                       ^^^^^^ the trait `AsJson` is not implemented for `Cat`

This happened because we tried to use a type which doesn't implement the `AsJson` trait in a place
which expected that trait: the `send_data_as_json` function.

To view the code used in this unit, visit this [Rust Playground link
](https://play.rust-lang.org/?version=stable&mode=debug&edition=2018&gist=eb322a632e8eca7f39056fcc6c966163).

As an optional challenge, you can try to implement the `AsJson` trait for the `Cat` type.

# Iterators

We have already covered how we can iterate over collection types using the loop, but this time we
will do a more in-depth review on how Rust handles the concept of iteration itself.

In Rust, all iterators implement a trait named `Iterator` that is defined in the standard library
and is used to implement iterators over collections such as ranges, arrays, vectors and hashmaps.

The core of that trait looks like this:

```rust
trait Iterator {
    type Item;
    fn next(&mut self) -> Option<Self::Item>;
}
```

An `iterator` has a method, `next`, which when called, returns an `Option<Item>`. `next` will return
`Some(Item)` as long as there are elements, and once they've all been exhausted, will return `None`
to indicate that iteration is finished.

Notice this definition uses some new syntax: `type Item` and `Self::Item`, which are defining an
associated type with this trait. This means that every implementation of the `Iterator` traits also
requires the definition of the associated `Item` type, wich is used as the return type of the `next`
method. In other words, the `Item` type will be the type returned from the iterator inside the `for`
loop block.

## Implementing our own iterator

Creating an iterator of your own involves two steps:

1.  Creating a struct to hold the iterator's state, and then
2.  Implementing Iterator for that struct.

Let's make an iterator named `Counter` which counts from 1 to an arbitrary number, defined when the
`Counter` struct is created.

First, we create the struct that will hold our iterator state. We also implement a `new` method to
control how it should be initiated.

```rust
#[derive(Debug)]
struct Counter {
    length: usize,
    count: usize,
}

impl Counter {
    fn new(length: usize) -> Counter {
	Counter {
	    count: 0,
	    length,
	}
    }
}
```

Then, we implement the `Iterator` trait for our `Counter` struct. We will be counting with usize, so
we declare that our associated `Item` type should be of that type.

`next()` is the only required method that we should define, and inside its body we increment our
count by 1 at every call *(this is why we started at zero)*, and then we check to see if we've
finished counting or not. We use the `Some(value)` variant of the `Option` type to express that
iteration is still yielding results and the `None` variant to express that iteration should stop.

```rust
impl Iterator for Counter {
    type Item = usize;

    fn next(&mut self) -> Option<Self::Item> {
	self.count += 1;
	if self.count <= self.length {
	    Some(self.count)
	} else {
	    None
	}
    }
}
```

We can check that our `Counter` works by explicitly calling its `next` function.

```rust
fn main() {
    let mut counter = Counter::new(6);
    println!("Counter just created: {:#?}", counter);

    assert_eq!(counter.next(), Some(1));
    assert_eq!(counter.next(), Some(2));
    assert_eq!(counter.next(), Some(3));
    assert_eq!(counter.next(), Some(4));
    assert_eq!(counter.next(), Some(5));
    assert_eq!(counter.next(), Some(6));
    assert_eq!(counter.next(), None);
    assert_eq!(counter.next(), None);  // further calls to `next` will return `None`
    assert_eq!(counter.next(), None);

    println!("Counter exhausted: {:#?}", counter);
}

```

But calling `next` this way gets repetitive. Rust allows us to use `for` loops in types that
implement the `Iterator` trait, so lets do that:

```rust
fn main() {
    for number in Counter::new(10) {
	println!("{}", number);
    }
}
```

The snippet above will then print the following in the console:

    1
    2
    3
    4
    5
    6
    7
    8
    9
    10

`Iterator`'s full definition includes a number of other methods as well, but they are default
methods, built on top of `next`, and so you get them for free:

```rust
let sum_until_10: usize = Counter::new(10).sum();
assert_eq!(sum_until_10, 55);

let powers_of_2: Vec<usize> = Counter::new(8).map(|n| 2usize.pow(n as u32)).collect();
assert_eq!(powers_of_2, vec![2, 4, 8, 16, 32, 64, 128, 256]);
```

You can check the complete code example of this unit at this [Rust Playground link
](https://play.rust-lang.org/?version=stable&mode=debug&edition=2018&gist=36fb2b6f5acdb60f78c7fe3efda5f278).
