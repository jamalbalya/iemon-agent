# Domain and renderer data model

Logical contracts only; they do not authorize changes to Claude Code's on-disk formats.

## Core entities
- `Account`: Claude config root identifier/path; never expose credential values.
- `ProjectRoot`: discovered projects directory.
- `Session`: session ID, project/cwd label, process-running flag, last activity, account reference and agents.
- `Agent`: agent ID/parent ID, role/type, description, model label, state, last activity, own token counts and pending tool summary.
- `AgentEvent`: normalized timestamp/type/safe summary; raw transcript stays at parser boundary.
- `InteractionEdge`: source/target and kind (spawn/message/handback), timestamp.
- `UsageSnapshot`: token counts and optional account utilization/reset values; never OAuth tokens.
- `ControlRequest`: prompt, permission, plan approval, resume/new-session action with correlation/idempotency semantics.
- `RendererCapabilities`: protocol, color/size, cell pixel estimate, GPU/software capability and bitmap limits.
- `RendererConfig`: mode, max FPS, quality/resource profile and reduced motion.
- `SceneSnapshot`: immutable bounded agents, positions/states, edges, selection and display-only labels.
- `RendererDiagnostics`: mode, fallback, frame timing, target FPS, queue depth, memory estimate and device failure.

## Invariants
1. Renderer never owns authoritative session/token/permission/prompt state.
2. Renderer receives minimized display-safe data.
3. IDs remain stable through mode changes.
4. User control goes through validated core commands; renderer cannot directly edit settings/hooks.
5. Prompt and permission requests survive renderer stalls/failure.
6. Scene snapshots and queues have hard bounds.
7. Summaries are truncated/redacted by default; full prompt shown only in explicit existing prompt panel.
8. Credentials never enter scene snapshots, diagnostics, logs or images.
