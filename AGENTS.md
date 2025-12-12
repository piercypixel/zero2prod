# Agent Guidelines for zero2prod

## Build/Test/Lint Commands
- **Build**: `cargo build`
- **Test all**: `cargo test`
- **Test single**: `cargo test <test_name>` or `cargo test <module>::<test_name>`
- **Lint**: `cargo clippy -- -D warnings`
- **Format**: `cargo fmt`
- **Format check**: `cargo fmt -- --check`
- **Watch**: `cargo watch -x check -x test -x run`

## Code Style Guidelines
- **Edition**: Rust 2024 (see Cargo.toml)
- **Formatting**: Use `rustfmt` defaults via `cargo fmt`
- **Linting**: All clippy warnings must pass (`-D warnings`)
- **Imports**: Group std, external crates, then local modules; use `rustfmt` ordering
- **Naming**: snake_case for functions/variables, PascalCase for types/traits, SCREAMING_SNAKE_CASE for constants
- **Error handling**: Use `Result<T, E>` for fallible operations; prefer `?` operator; avoid `.unwrap()` in production code
- **Types**: Leverage Rust's type system; prefer strong typing over stringly-typed APIs
- **Documentation**: Use `///` for public items; include examples in doc comments when helpful
