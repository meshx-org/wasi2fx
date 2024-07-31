

# wasi2fx

![Tests](https://github.com/meshx-org/wasi2fx/actions/workflows/rust.yml/badge.svg?event=push)
[![Coverage](https://codecov.io/gh/meshx-org/wasi2fx/graph/badge.svg?token=XE48Z6JSYS)](https://codecov.io/gh/meshx-org/wasi2fx)

`wasi2fx` is a tool to convert WebAssembly System Interface (WASI) dependent Wasm module to run on the Fiber runtime.


## Compiling wasi2fx

* Clone the https://github.com/meshx-org/wasi2fx: 
```bash
  git clone https://github.com/meshx-org/wasi2fx
```

* Enter the `wasi2fx` folder

* Compile the project with `cargo build` and copy the tool to some executable path or alternatively use `cargo install --path .`, but note that the project is still in the early development.


## Usage

To use this tool, navigate to the directory where the WASI-dependent project resides, and run the command:

```bash
  wasi2fx <input-wasm-file> <output_wasm_file>
```

This will read the old Wasm file and create a new Wasm file with the WASI dependencies removed.

**NOTE**

The tool requires that the polyfill implementation is present in your Wasm binary, to include the polyfill implementation into your canister project you need to add the dependency:

```bash
cargo add --git https://github.com/wasm-forge/fx-wasi-polyfill
```

This will create the polyfill methods in your `.wasm` file, which are needed for `wasi2fx`.

Also add the call to the init of the polyfill, example:

```rust
#[fx_cdk::init]
fn init() {
    unsafe {
        fx_wasi_polyfill::init();
    }
}
```



**NOTE2**

The polyfill library is still in early development, and not all methods are implemented. Feel free to review its current state before use.


## Related repositories



| Repository                                      |  Description                  | 
| --------------------------------------------- | ----------------------------- |
| [Polyfill library](https://github.com/meshx-org/fx-wasi-polyfill) | Polyfill library implementing the low-level WASI calls. |
| [stable-fs](https://github.com/wasm-forge/stable-fs) | Simple file system implementation based on the stable structures implementing the backend of the polyfill library. |
| [demo1](https://github.com/wasm-forge/demo1) | Basic demonstration of creating a "Hello World" application using Rust and running it on the Internet Computer. |
| [demo2](https://github.com/wasm-forge/demo2) | Basic demonstration of creating a "Hello World" application using C++ and running it on the Internet Computer. |
| [demo3](https://github.com/wasm-forge/demo3) | Example of running the Sqllite server on the Internet Computer. |
| [demo4](https://github.com/wasm-forge/demo4) | Example of running the Boa JavaScript interpretter on the Internet Computer. |

