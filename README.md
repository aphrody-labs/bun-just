# bun-just

The `just` plugin of the Aphrody Bun fork: the `bun-just` executable that
`bun just` dispatches to (`src/runtime/cli/plugin_command.rs` in
[aphrody-labs/bun](https://github.com/aphrody-labs/bun)).

Imported from aphrody-labs/bun commit `f31829d8aa36e9f34e662c8a9e5edf6e25705c86` (src/plugins/just; bun_just is the submodule vendor/just, aphrody-labs/just branch bun). That repository keeps the
earlier history.

## Install

Nothing to install: the first `bun just ...` downloads `bun-just-<target>` from the
release of the running bun, checks it against that release's `SHA256SUMS.txt`
and caches it in the plugin directory. A `bun-just` next to the bun executable
takes precedence.

## Build from source

This workspace path-depends on crates of the Bun checkout, so it builds only
mounted in it as `plugins/just` (an optional submodule, `update = none`):

```sh
git -C <bun checkout> submodule update --init --checkout --recursive plugins/just
bun bd --target=plugins          # build/<profile>/bun-just next to bun
# or directly:
cd <bun checkout>/plugins/just && cargo build --locked --profile plugin -p bun_plugin_just --bin bun-just
```

The toolchain is the Bun checkout's `rust-toolchain.toml`. `Cargo.lock` was
derived from the Bun workspace lockfile, so dependency versions match what the
fork built before the move.
