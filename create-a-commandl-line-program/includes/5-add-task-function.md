# The `add_task` function

The `add_task` function has to append a new `Task` value to a possibly existing collection of tasks
encoded in a JSON file.

So, before inserting a task into that collection, we must first read that file and assemble a vector
of tasks from its contents.

Its first version will look like this:

```rust

use std::fs::OpenOptions;
use std::io::{BufReader, Result, Seek, SeekFrom};
  // ...

pub fn add_task(journal_path: PathBuf, task: Task) -> Result<()> {
    // 1. open the file
    let file = OpenOptions::new()
	.read(true)
	.write(true)
	.create(true)
	.open(journal_path)?;

    // 2. consume file's contents as a vetcor of tasks
    let mut tasks: Vec<Tasks> = match serde_json::from_reader(file) {
	Ok(tasks) => tasks,
	Err(e) if e.is_eof() => Vec::new(),
	Err(e) => Err(e)?,
    };

    // 3. rewind the file after reading from it
    file.seek(SeekFrom::Start(0))?;

    // 4. write the modified task list back into the file
    tasks.push(task);
    serde_json::to_writer(file, &tasks)?;

    Ok(())
}
```

Let's comment this function in four steps:

## 1. open the file

First, we open our file using the `OpenOptions`, which allow us to specify some modes to operate the
file, such as `read`, `write` and `create` *(for when the file doesn't exist yet)*.

The question mark symbol after that statement is used to **propagate errors** without writing too
much boilerplate code. It is syntax sugar for early returning an error if that error matches with
the return type of the function it is inside of. Thus, the both snippets below are equivalent:

```rust
fn function_1() -> Result(Success, Failure) {
    match operation_that_might_fail() {
	Ok(success) => success,
	Err(failure) => return Err(failure),
    }
}

fn function_2() -> Result(Success, Failure) {
    operation_that_might_fail()?
}
```

That pattern is used a lot in code that needs to perform multiple I/O operations, such is our case.

## 2. build a Reader and consume its contents as a vetcor of tasks

The second step is to actually read our file, and to do that `serde_json` asks for any type that
implements the `Reader` trait. The `File` type implements that trait, so we just pass it as a
parameter to the `serde_json.from_reader` function while declaring that we expect to receive a
`Vec<Task>` from it.

Keep in mind that accessing the filesystem is an IO action that can fail for different reasons, so
we must take into account how our program should behave (ans possibly recover) in some specific
caeses. For instance, `serde_json` will return an error when it reaches the end of a file without
having found anything to parse, an event that will always happen in an empty file and that we must
be able to recover from.

To recover from specific kinds of errors, we use `guards` in our `match` expression to build an
empty `Vec` when that specific error occurs, representing an empty to-do list.

Note that `serde_json::Error` can be easily converted to the `std::io::Error` type because [it
implments the `From`
trait](https://docs.serde.rs/serde_json/error/struct.Error.html#impl-From%3CError%3E), making it
possible for us to use the `?` operator to unpack or early return them.

## 3. rewind the file after reading from it

Because we have moved the cursor to the end of our file, we must rewind it before writing over it
again. If we don't, we would begin writing at the cursor's last position, leading to a malformed
JSON file. The `Seek` trait and the `SeekFrom` enum from the `std::io` module are used to make that
happen.

## 4. write the modified task list back into the file

Last but not least, we push the `Task` value received as a function parameter to the task list and
use `serde_json` to write our task vector into our file. We then return the empty tuple value inside
an `Ok` to inform that everything went according to our plans.
