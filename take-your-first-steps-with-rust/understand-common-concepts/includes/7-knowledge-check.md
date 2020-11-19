# Knowledge check

In this unit your challenge is to fix the missing parts of each exercise's code to make them compile.

You can use your local development environment or use the Rust Playground to edit the code.

# Exercise 1: Structs and Enums

Lets build cars!

Edit only the `car_factory` function so it can return `Car` objects as requested by the clients.

```rust
struct Car {
    color: String,
    transmission: Transmission,
    conversible: bool,
    mileage: u32,
}

#[derive(PartialEq, Debug)]
enum Transmission {
    Manual,
    SemiAuto,
    Automatic,
}

fn car_factory(color: String, transmission: Transmission, conversible: bool) -> Car {
    // TODO: Replace the ??? for an actual Car instance
    let car: Car = ???;

    // Factory's Quality Control Department says that new cars must always have zero mileage!
    assert_eq!(car.mileage, 0);
    return car;
}

fn main() {
    let client_request_1 = car_factory(String::from("Red"), Transmission::Manual, false);
    assert_eq!(client_request_1.color, "Red");
    assert_eq!(client_request_1.transmission, Transmission::Manual);
    assert_eq!(client_request_1.conversible, false);

    let client_request_2 = car_factory(String::from("Silver"), Transmission::Automatic, true);
    assert_eq!(client_request_2.color, "Silver");
    assert_eq!(client_request_2.transmission, Transmission::Automatic);
    assert_eq!(client_request_2.conversible, true);

    let client_request_2 = car_factory(String::from("Yellow"), Transmission::SemiAuto, false);
    assert_eq!(client_request_2.color, "Yellow");
    assert_eq!(client_request_2.transmission, Transmission::SemiAuto);
    assert_eq!(client_request_2.conversible, false);
}
```

You can run this code in your local computer or use this [Rust Playground link](https://play.rust-lang.org/?version=stable&mode=debug&edition=2018&gist=a6392731e066f804d30c3c56bc8bd7ae).


# Exercise 2: Indexing

In this exercise, modify the code for the two functions and use the index notation to access the
required elements of the `numbers` tuple and the `letters` array.

Remember that tuples and arrays have different indexing notation.

You can put the expression for each required element where ??? is so that the assertions passes.

```rust
fn indexing_tuple() {
    let numbers = (1, 2, 3);
    // Replace below ??? with the tuple indexing syntax.
    let second = ???;

    assert_eq!(
	2, second,
	"This is not the 2nd number in the tuple: {}",
	second
    )
}

fn indexing_array() {
    let characters = ['a', 'b', 'c', 'd', 'e'];
    // Replace below ??? with the array indexing syntax.
    let letter_d = ???;

    assert_eq!(
	'd', letter_d,
	"This is not the character for the letter d: {}",
	letter_d
    )
}
```

You can run this code in your local computer or use this [Rust Playground link](https://play.rust-lang.org/?version=stable&mode=debug&edition=2018&gist=2feac2d3023de64774d9633f396bf24f).


# Exercise 3: Hashmaps

In this exercise you will need to define a basket of fruits in the form of a hash map, where the key
represents the name of the fruit and the value represents how many of that particular fruit is in
the basket.

You have to put at least three different types of fruits (e.g apple, banana, mango) in the basket
and the total count of all the fruits should be at least five.

Keep in mind that you only need to edit the `fruit_basket` function in this exercise.

```rust
use std::collections::HashMap;

fn fruit_basket() -> HashMap<String, u32> {
    let mut basket = ??? ; // TODO: declare your hash map here.

    // Two bananas are already given for you :)
    basket.insert(String::from("banana"), 2);

    // TODO: Put more fruits in your basket here.

    basket
}

fn main() {
    let basket = fruit_basket();
    assert!(
	basket.len() >= 3,
	"basket must have at least three types of fruits"
    );
    assert!(
	basket.values().sum::<u32>() >= 5,
	"basket must have at least five fruits"
    );
}
```

You can run this code in your local computer or use this [Rust Playground link](https://play.rust-lang.org/?version=stable&mode=debug&edition=2018&gist=8351e5ee4fc27335e54cdc027383f238).
