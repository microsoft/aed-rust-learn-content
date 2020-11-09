# 2. What is Rust?

Rust is an open source systems programming language that helps you write faster, more reliable
software. Rust offers control over low-level details (such as memory usage) in combination with
high-level ergonomics (such as iteration and interfaces), eliminating the hassle traditionally
associated with low-level languages.

Rust’s modern, flexible type system and the novel borrow checker ensures your program is free of
null pointer dereferences, double frees, dangling pointers, and similar bugs, all at compile time,
without runtime overhead.

In multi-threaded code, Rust catches data races at compile time, making concurrency much easier to
use.

Rust has been Stack Overflow's most loved language for four years in a row, indicating that many of
those who have had the opportunity to use Rust have fallen in love with it.

In short, Rust is the only language that ticks all the boxes:
- Type safe
- Memory safe
- Data race-free
- Ahead-of-time compiled
- Built on and encourages zero-cost abstractions
- Minimal runtime (no garbage collection, no JIT compiler, no Virtual Machine)
- Low memory footprint (programs run in resource constrained-environments like small microcontrollers)
- Targets bare-metal (e.g. write an OS kernel or device driver; use Rust as a ‘high level assembler’)
