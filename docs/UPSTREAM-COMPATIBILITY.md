# Upstream compatibility inventory

Upstream reference: https://github.com/cicingik/claude-monitor

Preliminary list derived from upstream README; this is not confirmation of current source behavior. Inspect source and add executable tests for every feature before changes.

| Area | Behavior to preserve | Evidence |
|---|---|---|
| Discovery | `~/.claude/projects`, all `~/.claude-*/projects`, repeatable `--root` | path fixtures on Windows/macOS |
| Parsing | main/nested subagent JSONL; skip malformed/unknown lines | parser tests |
| Agent states | running/active/idle/waiting/done | state transition tests |
| Office | layout, visitors, pet, agent cards | scene/interaction tests |
| Tree | nested hierarchy, expand/collapse, selection | keyboard tests |
| Activity | recent events, pending tool, summaries | fixture comparison |
| Interactions | spawn/message/handback edges | graph tests |
| Usage | per-agent/model/session tokens and account limits | de-duplication/mocked network |
| CLI | dump, snapshot, since, sprites, protocol, font, offline | CLI contract tests |
| Prompt panel | send/history/queue/take-back/slash commands | hook bridge tests |
| Permission | permission and plan approval | race/timeout/idempotency tests |
| Lifecycle | resume/background/new session/trust flow | process adapter tests |
| Hooks | install/uninstall, backups, waiter/async wakeup | rollback/compatibility tests |
| Terminal | iTerm2, Kitty, Sixel, half-block/text | emulator matrix/golden outputs |
| Windows | Windows process/path and WSL root behavior | Windows CI/manual tests |
| Accounts | multiple Claude account dirs | multi-account fixtures |

Retain upstream modules where possible. Create a file/module migration map. Replacement code must prove equivalent tests before removing existing implementation.
