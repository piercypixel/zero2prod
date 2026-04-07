# Zero To Production In Rust

[https://github.com/rust-lang/rust](https://github.com/rust-lang/rust)

## Cloud-native software

- Highly-available running in a failure-prone environment (i.e. keep serving requests with no downtime when some of the machines in our fleet start failing, note: AWS Spot Instance)
- Allows to continiously release new versions with zero downtime
- Handles dynamic workloads (e.g. variable request volumes, i.e. scalable distributed fleet)

[Gitflow Workflow | Atlassian Git Tutorial](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)

## Toolchain management

[rustup.rs - The Rust toolchain installer](https://rustup.rs/)

```bash
rustup update

rustup toolchain list
```

### Toolchain

1. Compilation target
2. Release channel

### Compilation target

- An arch + OS combo (e.g. x64-linux, x64-osx)
- You need a separate Rust compiler backend for each compilation target

```bash
rustc --version

cargo --version

# create a new rust project
cargo new zero2prod
```

**Platform support tiers**

1. Guaranteed to work
2. Guaranteed to build
3. Best effort

[Platform Support - The rustc book](https://doc.rust-lang.org/nightly/rustc/platform-support.html)

### Release channel

1. stable - the latest tested release
2. beta - the next release candidate
3. nightly - built from the master branch every night

[Overview - Rust Forge](https://forge.rust-lang.org/)

[https://github.com/rust-lang/crater](https://github.com/rust-lang/crater)

[Shipping a compiler every six weeks](https://www.pietroalbini.org/blog/shipping-a-compiler-every-six-weeks/)

[The Unstable Book - The Rust Unstable Book](https://doc.rust-lang.org/nightly/unstable-book/the-unstable-book.html)

[rust-analyzer](https://rust-analyzer.github.io/)

### Linking

- Assembling a final binary from the outputs of the earlier compilation stages
- Faster linkers are especially important for the `incremental compilation` for the `inner development loop`, where only a small part of the codebase is recompiled, but the whole codebase needs to be linked together
- `lld` (Windows, Linux) - `LLVM` linker
- `zld` (MacOS)

[Linker (computing)](https://en.wikipedia.org/wiki/Linker_(computing))

[Linking with LLD · Issue #39915 · rust-lang/rust](https://github.com/rust-lang/rust/issues/39915#issuecomment-618726211)

[https://github.com/rui314/mold](https://github.com/rui314/mold)

### Dependency management

```bash
cargo add tokio actix-web # adds dependencies to Cargo.toml and fetches them from crates.io
cargo add tokio --features macros,rt-multi-thread

```

#### Rust crate features

Optional parts of the library hidden behind a compilation flag to:

- Reduce compilation times - only compile the code you need
- Reduce the size of the final binary - only include the code you need
- Avoid pulling in unnecessary dependencies - only include the dependencies you need

### CI

```bash
cargo install cargo-watch

# executes cargo commands on every file change
cargo watch -x check

cargo watch -x check -x test -x run

# also caches dependencies for future CI commands like test
cargo build

cargo test

# At the time of writing tarpaulin only supports
# x86_64 CPU architectures running Linux.
cargo install cargo-tarpaulin

# collect code coverage
cargo tarpaulin --ignore-tests

# Often CI environments use rustup’s minimal profile, which does not include clippy.
rustup component add clippy

cargo clippy

# fail linting on any warning
cargo clippy -- -D warnings

# For rustup minimal profile
rustup component add rustfmt

cargo fmt

# CI
cargo fmt -- --check

cargo install cargo-audit

# Scan for known vulnerabilities
cargo audit
```

[https://github.com/xd009642/tarpaulin](https://github.com/xd009642/tarpaulin)

[https://github.com/rust-lang/rust-clippy](https://github.com/rust-lang/rust-clippy)

[https://github.com/rust-lang/rustfmt](https://github.com/rust-lang/rustfmt)

[RustSec](https://github.com/RustSec)

[https://github.com/RustSec/advisory-db](https://github.com/RustSec/advisory-db)

[Embark Studios Open Source](https://embark.dev/)

[https://github.com/EmbarkStudios/cargo-deny](https://github.com/EmbarkStudios/cargo-deny)

```rust
/* Mute warnings at code block level */
#[allow(clippy::lint_name)]

/* Mute warnings at project level */
#![allow(clippy::lint_name)]
```

[](https://crates.io/)

```rust
actix-web

use actix_web::{App, HttpRequest, HttpServer, Responder, web}

HttpServer # transport-level conserns: listener socket, concurrent conns limit, rate limiting, tls, etc.
App # application-level logic: routing, middlewares, handlers, etc.
```
