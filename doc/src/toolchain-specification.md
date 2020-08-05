# Toolchain specification

Many `rustup` commands deal with *toolchains*, a single installation of the
Rust compiler. `rustup` supports multiple types of toolchains. The most basic
track the official release channels: *stable*, *beta* and *nightly*; but
`rustup` can also install toolchains from the official archives, for alternate
host platforms, and from local builds.

Standard release channel toolchain names have the following form:

```
<channel>[-<date>][-<host>]

<channel>       = stable|beta|nightly|<version>
<date>          = YYYY-MM-DD
<host>          = <target-triple>
```

'channel' is either a named release channel or an explicit version number,
such as '1.42.0'. Channel names can be optionally appended with an archive
date, as in 'nightly-2014-12-18', in which case the toolchain is downloaded
from the archive for that date.

Finally, the host may be specified as a target triple. This is most useful for
installing a 32-bit compiler on a 64-bit platform, or for installing the
[MSVC-based toolchain][msvc-toolchain] on Windows. For example:

```console
$ rustup toolchain install stable-x86_64-pc-windows-msvc
```

For convenience, elements of the target triple that are omitted will be
inferred, so the above could be written:

```console
$ rustup toolchain install stable-msvc
```

Toolchain names that don't name a channel instead can be used to name [custom
toolchains].

[msvc-toolchain]: https://www.rust-lang.org/tools/install?platform_override=win
[custom toolchains]: custom-toolchains.md
