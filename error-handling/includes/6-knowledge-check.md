# Knowledge Check

All of the following attempts would cause a Rust program to panic, except:
- Access an out-of-bounds index of a Vector with `vector[index]` notation
  - Wrong. Directly accessing a vector element through index notation might cause a panic if the
    index is out of bounds.
- Access an out-of-bounds index of a Vector with `vector.get(index)` notation ***CORRECT***
  - Correct. Using the `Vector.get` method will return an `Option` type and will never panic.
- Access an out-of-bounds index of an Array with `array[index]` notation
  - Wrong. Directly accessing an array element through index notation might cause a panic if the
    index is out of bounds.
- Access a non-existing key of a HashMap with `hashmap[key]` notation
  - Wrong. Directly accessing a hashmap value through index notation might cause a panic if the key
    does not exist in the hashmap.

How can we represent the possibility of absence of a value of a given type `T` in Rust?
- The `Option<T>` type
  - Correct. The `Option::None` variant can express the absence of a value, while the
    `Option::Some(value)` can represent its presence.
- The `Result<T, bool>` type
  - Wrong. The `Result` type is used to express *failure*, not *absence*.
- An empty tuple: `()`
  - Wrong. The empty tuple doesn't represent anything.
- A `false` value of the `bool` type
  - Wrong. The `bool` type represents the truth about something, nut not absence of value.

How can we represent the possibility of I/O failure when obtaining a value of a given type `T`?
- The `Option<T>` type
  - Wrong. The `Option` type couldn't represent the cause of failure in a unsuccessfull I/O
    operation.
- The `Result<T, io::Error>` type
  - Correct. The `Result` type is used to represent failure, while the `io::Err` type represents all
    the possible outcomes of a failed I/O operation.
- An empty `Vec<T>`
  - Wrong. An empty vector doesn't convey meaning about a failed I/O operation.
- An empty tuple: `()`
  - Wrong. An empty tuple doesn't convey meaning about a failed I/O operation.
