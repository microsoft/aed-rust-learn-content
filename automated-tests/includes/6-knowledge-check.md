# Knowledge Check

## What is the expected outcome of this test function?

```rust
#[test]
fn math_works() {
    assert_eq!(2 + 2, 4)
}
```

- This function should not be executed during tests.
  - Incorrect. The `$[ignore]` attribute, which disables a test function during test execution, is
        not applied to this funcion.
- This function should panic during tests.
  - Incorrect. The `$[should_panic]` attribute, which indicates a test should generate a panic, is
        not applied to this funcion.
- This function should execute without any panic.
  - Correct.

## What is the expected outcome of this test function?

```rust
#[test]
#[should_panic]
fn unwrap_is_dangerous() {
    let content: Option<String> = None;
    assert_eq!(content.unwrap(), String::from(""))
}
```

- This function should not be executed during tests.
  - Incorrect. The `$[ignore]` attribute, which disables a test function during test execution, is
        not applied to this funcion.
- This function should panic during tests.
  - Correct. The `$[should_panic]` attribute indicates a test should generate a panic.
- This function should execute without any panic.
  - Incorrect. The `$[should_panic]` attribute indicates a test should generate a panic.

## What is the expected outcome of this test function?

```rust
#[test]
#[ignore = "api design isn't finished yet"]
fn unstable_feature() {
    let foo: Bar::new();
    assert_eq!(foo.x_axis, (0, 0));
}
```

- This function should not be executed during tests.
  - Correct. The `#[ignore]` attribute disables a test function during test execution.
- This function should panic during tests.
  - Incorrect. The `$[should_panic]` attribute, which indicates a test should generate a panic, is
        not applied to this funcion.
- This function should execute without any panic.
  - Incorrect. This funciton is marked with The `#[ignore]` attribute, that disables a test function
        during test execution.
