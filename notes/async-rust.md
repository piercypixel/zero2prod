# async rust

## futures crate

<https://docs.rs/futures/latest/futures/>

Sream - a sequence of values produced asynchronously over time

Sink - provide support for asynchronous writing of data

## Future trait - a single value produced by asynchronous computation (i.e. Promise in JavaScript)

All futures expose a `poll` method that checks if the future is ready to produce a value or if it needs to be polled again later (i.e. the `await` keyword in Rust)

```rust
fn poll(self: Pin<&mut Self>, cx: &mut Context<'_>) -> Poll<Self::Output>
```

## Executor trait - runs asynchronous tasks (i.e. event loop in JavaScript)

Rust `futures are lazy` - they do not start executing until they are polled (i.e. the `await` keyword in Rust). `Pull` model - the caller controls futures execution by polling them, rather than the futures themselves controlling when they execute in a `Push` model (i.e. JavaScript promises).

Rust standard library `by design` does not include an async runtime.

There is no configuration syntax to tell the Rust compiler that one of your dependencies is an async runtime, so you need to explicitly launch the async runtime in your main function and use it to execute your async code (futures).

So `main` cannot be an async function, as there is no async runtime and no caller to `poll` the future returned by an async main function at the time the main function is executed.

The `#[tokio::main]` macro from the `tokio` crate allows us to write an async main function that will be executed by the `tokio` runtime.
