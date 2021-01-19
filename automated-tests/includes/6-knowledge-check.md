# Knowledge Check

## What is the expected outcome of a test function tagged with the `#[test]` attribute?

- This function should not be executed during tests.
  - Incorrect. The `$[ignore]` attribute, which disables a test function during test execution, is
        not applied to this funcion.
- This function should panic during tests.
  - Incorrect. The `$[should_panic]` attribute, which indicates a test should generate a panic, is
        not applied to this funcion.
- This function should execute without any panic.
  - Correct.

## What is the expected outcome of a test function tagged with the `#[test]` and `#[should_panic]` attributes?

- This function should not be executed during tests.
  - Incorrect. The `$[ignore]` attribute, which disables a test function during test execution, is
        not applied to this funcion.
- This function should panic during tests.
  - Correct. The `$[should_panic]` attribute indicates a test should generate a panic.
- This function should execute without any panic.
  - Incorrect. The `$[should_panic]` attribute indicates a test should generate a panic.

## What is the expected outcome of a test function tagged with the `#[test]` and `#[ignore]` attributes?

- This function should not be executed during tests.
  - Correct. The `#[ignore]` attribute disables a test function during test execution.
- This function should panic during tests.
  - Incorrect. The `$[should_panic]` attribute, which indicates a test should generate a panic, is
        not applied to this funcion.
- This function should execute without any panic.
  - Incorrect. This funciton is marked with The `#[ignore]` attribute, that disables a test function
        during test execution.
