# Knowledge Check

All of the following attempts would cause a Rust program to panic, except:
- Access an out-of-bounds index of a Vector with `vector[index]` notation
- Access an out-of-bounds index of a Vector with `vector.get(index)` notation ***CORRECT***
- Access an out-of-bounds index of an Array with `array[index]` notation
- Access a non-existing key of a HashMap with `hashmap[key]` notation

How can we represent the possibility of absence of a value of a given type `T` in Rust?
- The `Option<T>` type ***CORRECT***
- The `Result<T, bool>` type
- An empty tuple: `()`
- A `false` value of the `bool` type

How can we represent the possibility of I/O failure when obtaining a value of a given type `T`?
- The `Option<T>` type
- The `Result<T, io::Error>` type ***CORRECT***
- An empty `Vec<T>`
- An empty tuple: `()`
