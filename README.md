# MinGW-w64 toolchain package

This package installs the [winlibs](https://winlibs.com/) build of the
MinGW-w64 GCC toolchain (GCC 15.2.0, MinGW-w64 13.0.0 UCRT, POSIX threads,
SEH) as a portable Vibe application on Windows x86_64. It contains no
binaries: the pinned upstream ZIP (about 264 MB) is downloaded during
installation and verified against its SHA-256 digest.

The payload is the archive's `mingw64/` tree, placed in a Vibe storage
library; it may be moved between libraries with `vibe storage move`. The
public commands `gcc`, `g++`, `c++`, `cpp`, `ar`, `as`, `ld`, `nm`, `objcopy`,
`objdump`, `ranlib`, `strip`, `windres`, `dlltool`, `gdb` and `mingw32-make`
appear in `opt\bin` of the Vibe home as PATH proxies, so a shell opened with
`vibe shell` — or any shell with that directory on PATH — can compile at once.
Each proxy starts the real executable in the payload, so GCC finds its own
`libexec` and `lib` directories relative to itself.

```text
vibe install -g org.vibevm.apps/mingw-w64
vibe shell
gcc --version
```

Only the tools are on PATH, not the toolchain's `bin` directory with its
runtime DLLs (`libstdc++-6.dll`, `libgcc_s_seh-1.dll`, `libwinpthread-1.dll`).
A program that links them dynamically runs from `vibe shell --with
org.vibevm.apps/mingw-w64` or after `vibe app expose`; link with `-static`
for an executable that runs anywhere.

Other application packages that build from sources on Windows may require
this package through the ordinary `[requires]` table, resolved across the
configured registries like any Vibe dependency
(`spec://org.vibevm.core/vibevm/common/PROP-065#app-dependencies`); until that
mechanism ships, a package's `needs = ["command:gcc"]` is met by installing
this package and running the build from `vibe shell`.

This package's metadata is UPL-1.0. The winlibs build retains the licenses of
GCC, MinGW-w64 and their components.
