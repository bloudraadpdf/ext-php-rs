# Windows build script tests

This package compiles the actual root `build.rs` and `windows_build.rs` with
the same workspace dependencies as the production build script. It does not
load PHP or run the downloader's entry point.

On Windows, run this command through the consumer's pinned Rust environment:

```sh
mise exec -- cargo test -p ext-php-rs-build-script-tests --bin windows-build-script
```

The existing Windows `cargo test --workspace` job also executes these tests.
They check ZIP Deflate extraction, replacement of only the selected pack, and
refusal of paths that can remove the output parent. Temporary files stay in the
package directory and are removed when each test ends. HTTP transport uses the
Rustls provider; a network download is not part of these unit tests.
