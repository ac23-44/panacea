# Panacea: Non-interactive and Stateless Oblivious RAM

**WARNING**:

This is proof-of-concept implementation.
It may contain bugs and security issues.
Please do not use in production systems.

## Building and testing

Our implementation is written in the Rust programming language.
Please refer to [The Rust Programming Language Website](https://www.rust-lang.org/tools/install)
to install the required tools (e.g., `rustup`, `cargo` and `rustc`).
The main library we use is [concrete-core](https://github.com/zama-ai/concrete-core),
but this is imported automatically with `cargo`.

The stable toolchain can be used for Linux and Mac computers with Intel processors.

Compiling for Windows is not supported at the moment.

### To Compile
```
cargo build --release
```

### To Run Tests
```
cargo test --release
```
### Special Instructions Mac computers with ARM Chips
To build natively on Mac computers with ARM chips (e.g., M1 and M2),
the Rust nightly toolchain (1.68 or above) must be used.
This can be installed by running
```
rustup toolchain install nightly
```

Additionally, `.cargo/config.toml` should be modified by swapping the commented lines so that it looks like this:
```
[build]
# rustflags = ["-C", "target-cpu=native"]
rustflags = ["-C", "target-cpu=apple-m1"]
```

For convenience, you can execute the following command so that the nightly toolchain is always used under the repo's directory
```
rustup override set nightly 
```
Then you can compile and test using the commands above.

Otherwise, you can use the `+nightly` modifier with `cargo` every time to specify the desired toolchain
```
# To install:
cargo +nightly build --release
# To test:
cargo +nightly test --release
```
## Running

### Getting the CLI options

```
cargo run --release -- --help
# or
./target/release/panacea --help
```

### Running

```
cargo run --release -- --params params.json
# or
./target/release/panacea --params params.json
```

Some parameters used in the paper are given in `params.json`.
The executable runs the ORAM protocol,
acting both as the client and the server.

Note that larger parameters have higher memory requirement
(batched mode with `rows=384` and `cols=4096` needs 1 TB of memory).
Please refer to the paper to for the exact memory requirements.

### Setting the number of threads

```
# for example, 8 threads
RAYON_NUM_THREADS=8 ./target/release/panacea --params params.json
```
