# Working with custom toolchains

For convenience of developers working on Rust itself, `rustup` can manage
local builds of the Rust toolchain. To teach `rustup` about your build, run:

```console
$ rustup toolchain link my-toolchain path/to/my/toolchain/sysroot
```

For example, on Ubuntu you might clone `rust-lang/rust` into `~/rust`, build
it, and then run:

```console
$ rustup toolchain link myrust ~/rust/build/x86_64-unknown-linux-gnu/stage2/
$ rustup default myrust
```

Now you can name `my-toolchain` as any other `rustup` toolchain. Create a
`rustup` toolchain for each of your `rust-lang/rust` workspaces and test them
easily with `rustup run my-toolchain rustc`.

Because the `rust-lang/rust` tree does not include Cargo, *when `cargo` is
invoked for a custom toolchain and it is not available, `rustup` will attempt
to use `cargo` from one of the release channels*, preferring 'nightly', then
'beta' or 'stable'.
