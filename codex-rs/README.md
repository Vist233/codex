# infinityCodex CLI (Rust Implementation)

We provide infinityCodex CLI as a standalone, native executable to ensure a zero-dependency install.

## Installing infinityCodex

Today, the easiest way to install infinityCodex is via `npm`:

```shell
npm i -g @infinity/codex
infinity-codex
```

You can also install via Homebrew (`brew install --cask infinity-codex`) or download a platform-specific release directly from our [GitHub Releases](https://github.com/openai/codex/releases).

## Documentation quickstart

- First run with infinityCodex? Start with [`docs/getting-started.md`](../docs/getting-started.md) (links to the walkthrough for prompts, keyboard shortcuts, and session management).
- Want deeper control? See [`docs/config.md`](../docs/config.md) and [`docs/install.md`](../docs/install.md).

## What's new in the Rust CLI

The Rust implementation is now the maintained infinityCodex CLI and serves as the default experience. It includes a number of features that the legacy TypeScript CLI never supported.

### Config

infinityCodex supports a rich set of configuration options. Note that the Rust CLI uses `config.toml` instead of `config.json`. See [`docs/config.md`](../docs/config.md) for details.

### Model Context Protocol Support

#### MCP client

infinityCodex CLI functions as an MCP client that allows the infinityCodex CLI and IDE extension to connect to MCP servers on startup. See the [`configuration documentation`](../docs/config.md#connecting-to-mcp-servers) for details.

#### MCP server (experimental)

infinityCodex can be launched as an MCP _server_ by running `infinity-codex mcp-server`. This allows _other_ MCP clients to use infinityCodex as a tool for another agent.

Use the [`@modelcontextprotocol/inspector`](https://github.com/modelcontextprotocol/inspector) to try it out:

```shell
npx @modelcontextprotocol/inspector infinity-codex mcp-server
```

Use `infinity-codex mcp` to add/list/get/remove MCP server launchers defined in `config.toml`, and `infinity-codex mcp-server` to run the MCP server directly.

### Notifications

You can enable notifications by configuring a script that is run whenever the agent finishes a turn. The [notify documentation](../docs/config.md#notify) includes a detailed example that explains how to get desktop notifications via [terminal-notifier](https://github.com/julienXX/terminal-notifier) on macOS. When infinityCodex detects that it is running under WSL 2 inside Windows Terminal (`WT_SESSION` is set), the TUI automatically falls back to native Windows toast notifications so approval prompts and completed turns surface even though Windows Terminal does not implement OSC 9.

### `infinity-codex exec` to run infinityCodex programmatically/non-interactively

To run infinityCodex non-interactively, run `infinity-codex exec PROMPT` (you can also pass the prompt via `stdin`) and infinityCodex will work on your task until it decides that it is done and exits. Output is printed to the terminal directly. You can set the `RUST_LOG` environment variable to see more about what's going on.
Use `infinity-codex exec --ephemeral ...` to run without persisting session rollout files to disk.

### Experimenting with the infinityCodex Sandbox

To test to see what happens when a command is run under the sandbox provided by infinityCodex, we provide the following subcommands in infinityCodex CLI:

```
# macOS
infinity-codex sandbox macos [--full-auto] [--log-denials] [COMMAND]...

# Linux
infinity-codex sandbox linux [--full-auto] [COMMAND]...

# Windows
infinity-codex sandbox windows [--full-auto] [COMMAND]...

# Legacy aliases
infinity-codex debug seatbelt [--full-auto] [--log-denials] [COMMAND]...
infinity-codex debug landlock [--full-auto] [COMMAND]...
```

### Selecting a sandbox policy via `--sandbox`

The Rust CLI exposes a dedicated `--sandbox` (`-s`) flag that lets you pick the sandbox policy **without** having to reach for the generic `-c/--config` option:

```shell
# Run infinityCodex with the default, read-only sandbox
infinity-codex --sandbox read-only

# Allow the agent to write within the current workspace while still blocking network access
infinity-codex --sandbox workspace-write

# Danger! Disable sandboxing entirely (only do this if you are already running in a container or other isolated env)
infinity-codex --sandbox danger-full-access
```

The same setting can be persisted in `~/.codex/config.toml` via the top-level `sandbox_mode = "MODE"` key, e.g. `sandbox_mode = "workspace-write"`.

## Code Organization

This folder is the root of a Cargo workspace. It contains quite a bit of experimental code, but here are the key crates:

- [`core/`](./core) contains the business logic for infinityCodex. Ultimately, we hope this to be a library crate that is generally useful for building other Rust/native applications that use infinityCodex.
- [`exec/`](./exec) "headless" CLI for use in automation.
- [`tui/`](./tui) CLI that launches a fullscreen TUI built with [Ratatui](https://ratatui.rs/).
- [`cli/`](./cli) CLI multitool that provides the aforementioned CLIs via subcommands.

If you want to contribute or inspect behavior in detail, start by reading the module-level `README.md` files under each crate and run the project workspace from the top-level `codex-rs` directory so shared config, features, and build scripts stay aligned.
