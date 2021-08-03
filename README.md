# [tauri-apps/tauri#2336](https://github.com/tauri-apps/tauri/issues/2336) repro case

Simply try running `yarn run tauri dev` and you should see the following error:

```
error[E0433]: failed to resolve: use of undeclared crate or module `base64`
   --> /home/cynthia/.cargo/registry/src/github.com-1ecc6299db9ec823/tauri-1.0.0-beta.5/src/endpoints/file_system.rs:359:3
    |
359 |   base64::decode(contents)
    |   ^^^^^^ use of undeclared crate or module `base64`

error[E0433]: failed to resolve: use of undeclared crate or module `base64`
  --> /home/cynthia/.cargo/registry/src/github.com-1ecc6299db9ec823/tauri-1.0.0-beta.5/src/error.rs:47:24
   |
47 |   Base64Decode(#[from] base64::DecodeError),
   |                        ^^^^^^ use of undeclared crate or module `base64`

error[E0277]: the size for values of type `[u8]` cannot be known at compilation time
   --> /home/cynthia/.cargo/registry/src/github.com-1ecc6299db9ec823/tauri-1.0.0-beta.5/src/endpoints/file_system.rs:361:16
    |
361 |     .and_then(|c| {
    |                ^ doesn't have a size known at compile-time
    |
    = help: the trait `Sized` is not implemented for `[u8]`
    = help: unsized fn params are gated as an unstable feature
help: function arguments must have a statically known size, borrowed types always have a known size
    |
361 |     .and_then(|&c| {
    |                ^

Some errors have detailed explanations: E0277, E0433.
For more information about an error, try `rustc --explain E0277`.
error: could not compile `tauri` due to 3 previous errors
```

## Environment information
Note: I used yarn, and I also was able to reproduce on Rust stable 1.54.0
```
Operating System - Arch Linux, version Rolling Release X64

Node.js environment
  Node.js - 16.4.2
  @tauri-apps/cli - 1.0.0-beta.6
  @tauri-apps/api - 1.0.0-beta.5

Global packages
  npm - 7.18.1
  yarn - 1.22.10

Rust environment
  rustc - 1.56.0-nightly
  cargo - 1.55.0-nightly

App directory structure
/src-tauri
/node_modules
/app

App
  tauri.rs - 1.0.0-beta.5
  build-type - bundle
  CSP - default-src blob: data: filesystem: ws: wss: http: https: tauri: 'unsafe-eval' 'unsafe-inline' 'self' img-src: 'self'
```
