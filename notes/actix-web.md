# actix-web (Rust web framework)

## Incompatibilities and interop between different async runtimes

`actix-web` is built on top of `tokio`, so it uses `tokio`'s async runtime and features. This means that if you want to use `actix-web`, you need to use `tokio` as your async runtime for all asynchronous code in your application.

You cannot use `async-std` or other async runtimes with `actix-web` without some form of interop layer, which can be complex and may not be fully supported.

Rust async ecosystem has largely consolidated around `Tokio` for production server applications.

## Server - HttpServer

- Allocates listening socket and accepts incoming connections.
- Manages concurrent connections, rate limiting, TLS, etc. (handles all `transport-level` concerns)
- Invokes the application logic ( `App`) for each incoming request (established connection)

## Application - App

- Manages `application-level` logic, such as routing, middlewares, request handlers, etc.
- Builder pattern fluent API
- `App::new()` creates a new instance of the application, which can be configured with routes and middlewares (basically an http router)
- `Route` struct combines a `handler` with a set of `guards` (e.g., HTTP method, path, etc.) to determine which handler should be invoked for a given request
- `Guard::check` method of a guard trait
- `web::get()` is a shortcut for `Route::new().guard(guard::Get())`
- `Responder` trait is implemented by types that can be converted into an HTTP response, such as `String`, `&str`, `HttpResponse`, etc. (i.e., the return type of a handler function)
