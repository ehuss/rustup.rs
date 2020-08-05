# Installation

Follow the instructions at <https://www.rust-lang.org/tools/install>. If that
doesn't work for you there are [other installation
methods](#other-installation-methods).

`rustup` installs `rustc`, `cargo`, `rustup` and other standard tools to
Cargo's `bin` directory. On Unix it is located at `$HOME/.cargo/bin` and on
Windows at `%USERPROFILE%\.cargo\bin`. This is the same directory that `cargo
install` will install Rust programs and Cargo plugins.

This directory will be in your `$PATH` environment variable, which means you
can run them from the shell without further configuration. Open a *new* shell
and type the following:

```console
rustc --version
```

If you see something like `rustc 1.19.0 (0ade33941 2017-07-17)` then you are
ready to Rust. If you decide Rust isn't your thing, you can completely remove
it from your system by running `rustup self uninstall`.

## Choosing where to install

`rustup` allows you to customise your installation by setting the environment
variables `CARGO_HOME` and `RUSTUP_HOME` before running the `rustup-init`
executable. As mentioned in the [Environment Variables] section, `RUSTUP_HOME`
sets the root `rustup` folder, which is used for storing installed toolchains
and configuration options. `CARGO_HOME` contains cache files used by [cargo].

Note that you will need to ensure these environment variables are always set
and that `CARGO_HOME/bin` is in the `$PATH` environment variable when using
the toolchain.

[Environment Variables]: environment-variables.md
[cargo]: https://github.com/rust-lang/cargo

## Installing nightly

When `rustup-init` installs the initial toolchain it _forces_ the installation
and so will install the `nightly` channel regardless of whether it might be
missing components that you want.  For example, if you want to make a fresh
installation of `rustup` and then install `nightly` along with `clippy` or
`miri` you will need to do this in two phases.

Firstly install `rustup` by means of:

```console
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- --default-toolchain none -y
```

Next you can install `nightly` allowing `rustup` to downgrade until it finds
the components you need:

```console
rustup toolchain install nightly --allow-downgrade --profile minimal --component clippy
```

This can be used to great effect in CI, to get you a toolchain rapidly which
meets your criteria.

## Enable tab completion for Bash, Fish, Zsh, or PowerShell

`rustup` now supports generating completion scripts for Bash, Fish, Zsh, and
PowerShell. See `rustup help completions` for full details, but the gist is as
simple as using one of the following:

```console
# Bash
$ rustup completions bash > ~/.local/share/bash-completion/completions/rustup

# Bash (macOS/Homebrew)
$ rustup completions bash > $(brew --prefix)/etc/bash_completion.d/rustup.bash-completion

# Fish
$ mkdir -p ~/.config/fish/completions
$ rustup completions fish > ~/.config/fish/completions/rustup.fish

# Zsh
$ rustup completions zsh > ~/.zfunc/_rustup

# PowerShell v5.0+
$ rustup completions powershell >> $PROFILE.CurrentUserCurrentHost
# or
$ rustup completions powershell | Out-String | Invoke-Expression
```

**Note**: you may need to restart your shell in order for the changes to take
effect.

For `zsh`, you must then add the following line in your `~/.zshrc` before
`compinit`:

```zsh
fpath+=~/.zfunc
```

## Other installation methods

The primary installation method, as described at https://rustup.rs, differs by platform:

* On Windows, download and run the [rustup-init.exe built for
  `i686-pc-windows-gnu` target][setup]. In general, this is the build of
  `rustup` one should install on Windows. Despite being built against the GNU
  toolchain, _the Windows build of `rustup` will install Rust for the MSVC
  toolchain if it detects that MSVC is installed_. If you prefer to install
  GNU toolchains or x86_64 toolchains by default this can be modified at
  install time, either interactively or with the `--default-host` flag, or
  after installation via `rustup set default-host`.
* On Unix, run `curl https://sh.rustup.rs -sSf | sh` in your shell. This
  downloads and runs [`rustup-init.sh`], which in turn downloads and runs the
  correct version of the `rustup-init` executable for your platform.

[setup]: https://static.rust-lang.org/rustup/dist/i686-pc-windows-gnu/rustup-init.exe
[`rustup-init.sh`]: https://static.rust-lang.org/rustup/rustup-init.sh

`rustup-init` accepts arguments, which can be passed through the shell script.
Some examples:

```console
$ curl https://sh.rustup.rs -sSf | sh -s -- --help
$ curl https://sh.rustup.rs -sSf | sh -s -- --no-modify-path
$ curl https://sh.rustup.rs -sSf | sh -s -- --default-toolchain nightly
$ curl https://sh.rustup.rs -sSf | sh -s -- --default-toolchain none
$ curl https://sh.rustup.rs -sSf | sh -s -- --profile minimal --default-toolchain nightly
```

If you prefer you can directly download `rustup-init` for the platform of your
choice:

- [aarch64-linux-android](https://static.rust-lang.org/rustup/dist/aarch64-linux-android/rustup-init)
- [aarch64-unknown-linux-gnu](https://static.rust-lang.org/rustup/dist/aarch64-unknown-linux-gnu/rustup-init)
- [arm-linux-androideabi](https://static.rust-lang.org/rustup/dist/arm-linux-androideabi/rustup-init)
- [arm-unknown-linux-gnueabi](https://static.rust-lang.org/rustup/dist/arm-unknown-linux-gnueabi/rustup-init)
- [arm-unknown-linux-gnueabihf](https://static.rust-lang.org/rustup/dist/arm-unknown-linux-gnueabihf/rustup-init)
- [armv7-linux-androideabi](https://static.rust-lang.org/rustup/dist/armv7-linux-androideabi/rustup-init)
- [armv7-unknown-linux-gnueabihf](https://static.rust-lang.org/rustup/dist/armv7-unknown-linux-gnueabihf/rustup-init)
- [i686-apple-darwin](https://static.rust-lang.org/rustup/dist/i686-apple-darwin/rustup-init)
- [i686-linux-android](https://static.rust-lang.org/rustup/dist/i686-linux-android/rustup-init)
- [i686-pc-windows-gnu](https://static.rust-lang.org/rustup/dist/i686-pc-windows-gnu/rustup-init.exe)
- [i686-pc-windows-msvc](https://static.rust-lang.org/rustup/dist/i686-pc-windows-msvc/rustup-init.exe)[^msvc]
- [i686-unknown-linux-gnu](https://static.rust-lang.org/rustup/dist/i686-unknown-linux-gnu/rustup-init)
- [mips-unknown-linux-gnu](https://static.rust-lang.org/rustup/dist/mips-unknown-linux-gnu/rustup-init)
- [mips64-unknown-linux-gnuabi64](https://static.rust-lang.org/rustup/dist/mips64-unknown-linux-gnuabi64/rustup-init)
- [mips64el-unknown-linux-gnuabi64](https://static.rust-lang.org/rustup/dist/mips64el-unknown-linux-gnuabi64/rustup-init)
- [mipsel-unknown-linux-gnu](https://static.rust-lang.org/rustup/dist/mipsel-unknown-linux-gnu/rustup-init)
- [powerpc-unknown-linux-gnu](https://static.rust-lang.org/rustup/dist/powerpc-unknown-linux-gnu/rustup-init)
- [powerpc64-unknown-linux-gnu](https://static.rust-lang.org/rustup/dist/powerpc64-unknown-linux-gnu/rustup-init)
- [powerpc64le-unknown-linux-gnu](https://static.rust-lang.org/rustup/dist/powerpc64le-unknown-linux-gnu/rustup-init)
- [s390x-unknown-linux-gnu](https://static.rust-lang.org/rustup/dist/s390x-unknown-linux-gnu/rustup-init)
- [x86_64-apple-darwin](https://static.rust-lang.org/rustup/dist/x86_64-apple-darwin/rustup-init)
- [x86_64-linux-android](https://static.rust-lang.org/rustup/dist/x86_64-linux-android/rustup-init)
- [x86_64-pc-windows-gnu](https://static.rust-lang.org/rustup/dist/x86_64-pc-windows-gnu/rustup-init.exe)
- [x86_64-pc-windows-msvc](https://static.rust-lang.org/rustup/dist/x86_64-pc-windows-msvc/rustup-init.exe)<sup>[†](#vs2019)</sup>
- [x86_64-unknown-freebsd](https://static.rust-lang.org/rustup/dist/x86_64-unknown-freebsd/rustup-init)
- [x86_64-unknown-linux-gnu](https://static.rust-lang.org/rustup/dist/x86_64-unknown-linux-gnu/rustup-init)
- [x86_64-unknown-linux-musl](https://static.rust-lang.org/rustup/dist/x86_64-unknown-linux-musl/rustup-init)
- [x86_64-unknown-netbsd](https://static.rust-lang.org/rustup/dist/x86_64-unknown-netbsd/rustup-init)

[^msvc]: MSVC builds of `rustup` additionally require an [installation of Visual
    Studio 2019 or the Visual C++ Build Tools 2019][vs]. For Visual Studio,
    make sure to check the "C++ tools" and "Windows 10 SDK" option. No
    additional software installation is necessary for basic use of the GNU
    build.

[vs]: https://visualstudio.microsoft.com/downloads/

You can fetch an older version from
`https://static.rust-lang.org/rustup/archive/{rustup-version}/{target-triple}/rustup-init[.exe]`

To install from source just run `cargo run --release`. Note that currently
`rustup` only builds on nightly Rust, and that after installation the `rustup`
toolchains will supersede any pre-existing toolchains by prepending
`~/.cargo/bin` to the `PATH` environment variable.
