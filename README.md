# Kalcite packages

This is the official Git package monorepo for reusable Kalcite libraries. Each
directory in [`packages/`](packages) is an independently versioned KLC package
with a small `kalcite-package.toml` descriptor and an allocation-free entry
point in `src/lib.klc`.

## Install with Kally

```sh
kally add hash git:https://github.com/Kalcite-Engine/kalcite-pkgs.git#packages/hash main
kally add http git:https://github.com/Kalcite-Engine/kalcite-pkgs.git#packages/http main
kally sync --locked
```

Kally records the exact Git commit and a source-tree checksum in `kally.lock`.
Use `kally update NAME` to intentionally advance a dependency.

## Packages

| Package | Purpose |
| --- | --- |
| `hash` | FNV-1a and Adler-32 over bounded strings, plus hash composition. |
| `filesystem` | Portable safe-relative-path validation before filesystem adapters perform I/O. |
| `http` | HTTP status, method and header validation plus HTTPS defaults. |
| `git` | Git reference, revision and repository-subdirectory validation for package tooling. |

The HTTP, filesystem and Git transports are target capabilities; the bounded,
deterministic policy and parsing logic lives in KLC. This keeps packages
portable and lets applications fail at capability selection rather than by
silently using an emulation.

## Contributing a package

Create `packages/<name>/kalcite-package.toml` and `packages/<name>/src/lib.klc`.
The CI compiles every entry point against the current Kalcite compiler. Keep
the public API bounded, allocation-free and explicit about platform
capabilities.
