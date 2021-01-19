# Knowledge check

Each of the following, if true, describe **modules** in Rust, EXCEPT:

- A module is a (possibly nested) unit of code organization inside a crate.
  - Incorrect. This statement is true.
- There are two ways to declare modules in Rust: inline or in another file.
  - Incorrect. This statement is true.
- A module is a compilation unit, which is the smallest amount of code that the Rust compiler can operate on.
  - Correct. The smallest compilation unit in Rust is a **crate**, not a **module**.
- A module is a collection of items: functions, structs, traits, impl blocks, and even other modules.
  - Incorrect. This statement is true.


Each of the following, if true, describe **third party modules** in Rust, EXCEPT:

- Dependencies can be fetched and compiled by Cargo.
  - Incorrect. This statement is true.
- Third party crates and their intended versions should be declared in the `src/main.rs` file.
  - Correct. Third party crates should be declared in the `Cargo.toml` file.
- Dependencies are normally fetched from the Crates.io repository.
  - Incorrect. This statement is true.
- Only public items can be accessed from third party crates.
  - Incorrect. This statement is true.
