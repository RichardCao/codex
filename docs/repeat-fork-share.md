# Repeat Fork Share Copy

This document contains ready-to-share descriptions for this fork and its
`/repeat` prototype.

## Chinese

### Short

```text
我在 openai/codex 的 TUI slash commands 里加了一个 `/repeat` 命令。

- `/repeat <seconds> <message>`：每隔 N 秒向当前 thread 发送一条消息
- `/repeat off`：停止重复发送
- 当前激活 thread 会在 CLI 里看到本地回显
- 加了 generation 过滤，避免 `/repeat off` 后残留最后一条旧 tick

分支：
https://github.com/RichardCao/codex/tree/richardcao/repeat-slash-command

Diff：
https://github.com/openai/codex/compare/main...RichardCao:richardcao/repeat-slash-command
```

### Longer

```text
这是一个基于 openai/codex 的 fork，我在 TUI 的 slash command 体系里加了一个 `/repeat` 原型命令。

功能：
- `/repeat <seconds> <message>`：周期性向当前 thread/session 发送一条文本消息
- `/repeat off`：停止当前 repeat
- 如果该 thread 正处于当前激活视图，重复消息会在 CLI 历史里本地回显
- 使用 generation 过滤旧 tick，避免停止后又漏出最后一条排队消息

代码分支：
https://github.com/RichardCao/codex/tree/richardcao/repeat-slash-command

对比上游：
https://github.com/openai/codex/compare/main...RichardCao:richardcao/repeat-slash-command

本地验证：
1. 启动本地 codex
2. 输入 `/repeat 5 hello`
3. 再输入 `/repeat off`
```

## English

### Short

```text
This fork adds a prototype `/repeat` slash command to the Codex TUI.

- `/repeat <seconds> <message>` periodically submits a user message to the current thread
- `/repeat off` stops the active repeating task
- repeated messages are locally echoed in the active CLI view
- stale queued ticks are suppressed so stopping repeat does not leak one last tick

Branch:
https://github.com/RichardCao/codex/tree/richardcao/repeat-slash-command

Diff:
https://github.com/openai/codex/compare/main...RichardCao:richardcao/repeat-slash-command
```

### Longer

```text
This is a fork of openai/codex with a prototype `/repeat` slash command added to the TUI command system.

What it does:
- `/repeat <seconds> <message>` periodically submits a text message to the current thread/session
- `/repeat off` stops the current repeating task
- if that thread is currently active in the TUI, repeated messages are also echoed into local history
- stale queued ticks are filtered with a generation check so stopping repeat does not leak one last pending tick

Branch:
https://github.com/RichardCao/codex/tree/richardcao/repeat-slash-command

Compare against upstream:
https://github.com/openai/codex/compare/main...RichardCao:richardcao/repeat-slash-command

Quick validation:
1. Start the local codex build
2. Run `/repeat 5 hello`
3. Run `/repeat off`
```

## Local Validation

Run the local build:

```bash
cd /Users/create/Codex_Workspace/codex
git checkout richardcao/repeat-slash-command
export LK_CUSTOM_WEBRTC=/Users/create/Codex_Workspace/webrtc-mac-arm64-release/mac-arm64-release
$HOME/.cargo/bin/cargo run --bin codex --manifest-path /Users/create/Codex_Workspace/codex/codex-rs/Cargo.toml
```

Or run tests directly:

```bash
cd /Users/create/Codex_Workspace/codex/codex-rs
export LK_CUSTOM_WEBRTC=/Users/create/Codex_Workspace/webrtc-mac-arm64-release/mac-arm64-release
$HOME/.cargo/bin/cargo test -p codex-tui slash_commands
```
