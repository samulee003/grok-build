# Agent Instructions

## Repository overview

Grok Build is a Rust workspace for the `grok` terminal-based AI coding agent.
The main application is composed from crates under `crates/codegen/`, with
shared support crates under `crates/common/`, build-time crates under
`crates/build/`, and a small `prod/mc/` package. Vendored upstream code is
under `third_party/`.

The primary packages are:

- `crates/codegen/xai-grok-pager-bin`: composition root and binary target.
- `crates/codegen/xai-grok-pager`: terminal UI.
- `crates/codegen/xai-grok-shell`: agent runtime and entry points.
- `crates/codegen/xai-grok-tools`: tool implementations.
- `crates/codegen/xai-grok-workspace`: filesystem, VCS, execution, and
  checkpoint support.

This tree is periodically synchronized from the SpaceXAI monorepo. The
`SOURCE_REV` file records the source monorepo revision.

## Important repository conventions

- The root `Cargo.toml` is generated. Do not edit it directly; make dependency
  or package changes in the relevant per-crate `Cargo.toml` instead.
- Use the pinned Rust toolchain from `rust-toolchain.toml` (`rustup` will
  install it).
- Builds may require DotSlash for hermetic tools in `bin/`, especially
  `bin/protoc`. Ensure `dotslash` is installed and on `PATH`; a system
  `protoc` or `$PROTOC` can be used as a fallback.
- Do not modify vendored code in `third_party/` unless the task specifically
  concerns that dependency. Preserve its upstream licensing.
- Avoid broad workspace builds when a targeted crate command is sufficient.

## Building and testing

From the repository root:

```sh
# Fast validation for the main binary
cargo check -p xai-grok-pager-bin

# Build or run the main application
cargo build -p xai-grok-pager-bin --release
cargo run -p xai-grok-pager-bin

# Test a targeted crate
cargo test -p xai-grok-config

# Lint and format
cargo clippy -p <crate>
cargo fmt --all
```

For changes affecting many crates or the toolchain, use the broader checks
only when needed:

```sh
cargo check --all-targets --workspace
cargo clippy --all-targets --workspace
```

Run the narrowest relevant checks first, then expand validation for changes
that cross crate boundaries. Do not add new test or lint tooling without a
specific need.

## Making changes

1. Locate the owning crate and read its `Cargo.toml`, source, and nearby tests
   before editing.
2. Keep changes focused and follow existing Rust formatting and error-handling
   patterns.
3. Add or update tests when behavior changes, preferably in the affected
   crate.
4. Run `cargo fmt --all` and the narrowest applicable `cargo check`, `cargo
   test`, or `cargo clippy` commands.
5. Review the final diff and ensure no credentials, tokens, or generated
   artifacts were added.

## Contribution and security

This repository does not accept external pull requests or unsolicited patches;
see `CONTRIBUTING.md`. Security issues must be reported using the process in
`SECURITY.md` and must not be opened as public issues.

