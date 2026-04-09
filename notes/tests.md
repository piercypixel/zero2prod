# tests

## 3 ways to write tests in Rust

1. Alongside the code in the same file

    An embedded test module is a part of your project, i.e.

    Can access all the code in the parent module, including private items.

    ```rust
    #[cfg(test)]
    mod tests {
      // Import the SUT (all the code in the parent module) into the test module's scope
      use super::*;

      // Write tests here
    }
    ```

2. In a separate `/tests` directory at the root of the project, with each file being a separate test module (integration tests)

    Can only access the public API of your crate.

    Mostly for integration tests, which test the public API of your crate as a whole (i.e., black-box testing).

    Requires the SUT to be exposed as a library crate (i.e., with a `lib.rs` file), which can be imported in the test files. You cannot import a binary crate (i.e., with a `main.rs` file) in the test files.

3. Embedded in public docs, which are written in the documentation comments and can be run with `cargo test` (also called doctests)

    ```rust
    /// Check if a number is even
    /// ```rust
    /// use my_crate::is_even;
    /// 
    /// assert!(is_even(2));
    /// assert!(!is_even(1));
    /// ```
    pub fn is_even(x: u64) -> bool {
      x % 2 == 0
    }
    ```
