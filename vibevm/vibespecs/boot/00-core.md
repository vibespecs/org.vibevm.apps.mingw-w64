# MinGW-w64 toolchain package

This package declares one Windows installation route for the winlibs build of
the MinGW-w64 GCC toolchain. The archive is identified by its exact URL and
SHA-256; the launchers and public commands name the tools in `bin/`.

Before changing the package, read `vibe.toml` and `README.md`. When moving to
a new winlibs release, download the archive, verify its digest against the
actual bytes, confirm the `mingw64/bin` tool set still matches the declared
launchers, and keep the public command names stable: other packages depend on
them.
