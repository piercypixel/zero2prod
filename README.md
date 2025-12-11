# zero2prod

## Setup

### Rust Toolchain

Install Rust using [rustup](https://rustup.rs/):

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Add required components (for minimal profile):

```bash
rustup component add clippy
rustup component add rustfmt
```

### Development Tools

```bash
cargo install cargo-watch
cargo install cargo-tarpaulin  # Linux x86_64 only
cargo install cargo-audit
```

## Development

### Build

```bash
cargo build
```

### Run

```bash
cargo run
```

### Watch Mode

Execute cargo commands on every file change:

```bash
cargo watch -x check
```

Run check, test, and run on file changes:

```bash
cargo watch -x check -x test -x run
```

### Testing

```bash
cargo test
```

### Code Coverage

```bash
cargo tarpaulin --ignore-tests
```

> Note: tarpaulin only supports x86_64 CPU architectures running Linux.

### Linting

```bash
cargo clippy
```

Fail on any warning:

```bash
cargo clippy -- -D warnings
```

### Formatting

```bash
cargo fmt
```

Check formatting (CI):

```bash
cargo fmt -- --check
```

### Security Audit

Scan for known vulnerabilities:

```bash
cargo audit
```
