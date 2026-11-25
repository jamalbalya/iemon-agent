# IEMON Agent — Product Requirements Specification

**ID:** IEMON-0001 | **Version:** 1.0.0 | **Status:** Proposed  
**Owner:** Jamal Balya  
**Platforms:** Windows 10/11 x64; macOS Intel and Apple Silicon (minimum macOS release to be confirmed through dependency research)

## 1. Vision
Evolve `cicingik/claude-monitor` into **IEMON Agent**, a cross-platform Claude Code session monitor with a polished, real-time 3D animated office. Preserve the established terminal-first experience and every existing functional behavior while making 3D optional, efficient, accessible and incapable of disrupting other work. IEMON is a monitor/controller, not an LLM, Claude Code replacement or agent runtime.

## 2. Problem
The owner's local experience is not satisfactory on macOS and current office visualization is 2D. 3D may increase CPU/GPU/memory pressure. A careless rewrite may break hooks, prompt queues, permission handoff, background resume, multiple account discovery, terminal fallback or other existing behavior.

## 3. Goals
- G1: Native Windows and macOS support (Intel and Apple Silicon where dependencies allow).
- G2: True 3D geometry, 3D characters, depth, spatial motion and camera—not perspective-transformed 2D sprites.
- G3: Preserve upstream features and semantics.
- G4: Retain terminal-first operation across image-capable and text-only terminals.
- G5: Bound CPU, memory, GPU, FPS, queues and scan work.
- G6: Core monitoring/control works when graphics fail or are disabled.
- G7: Selectively use project-local skills for design, implementation and QA.
- G8: Reproducible cross-platform tests and performance evidence.

## 4. Non-goals
No replacement of Claude Code, LLM inference, non-Claude agent support absent another spec, cloud rendering, telemetry, analytics, hosted backend, wholesale rewrite, discrete GPU requirement, graphical desktop app requirement, or modifications to Claude transcript formats/hooks/permission model/credential files. Resource budgets are verified on documented reference machines, not promised identical on all hardware.

## 5. Main user scenarios
Monitor many Claude Code sessions and subagents; inspect role/activity/events/model/token usage; navigate hierarchy and spawn/message/handback edges; send prompts/answer permissions/resume/create sessions; work across terminals with iTerm2/Kitty/Sixel/text fallback; keep scene quiet when unfocused, idle or under pressure.

## 6. Functional requirements

### FR-001 Platform support
Build/run on Windows 10/11 x64 and macOS Intel/Apple Silicon. Paths, process inspection, terminal capability detection, filesystem notifications, signals and process spawning live behind platform adapters. Unsupported operations fail clearly, never crash.

### FR-002 Upstream feature compatibility
Before implementation inventory actual upstream source and test every existing feature. Minimum README-derived compatibility scope:
- discover `~/.claude/projects`, all `~/.claude-*/projects`, repeated `--root`;
- main and nested subagent transcript parsing; skip malformed/unknown lines safely;
- process detection and running/active/idle/waiting/done status;
- office scene, visitors, pet, agent cards and selection;
- tree view, Activity/Interactions/Usage tabs, navigation and expand/collapse;
- token accounting without duplicate message usage;
- spawn/message/handback graph;
- account usage limits and isolated/offline network behavior;
- CLI `--dump`, `--snapshot`, `--since`, `--sprites`, `--protocol`, `--font`, `--offline`;
- prompt panel, slash command discovery, history, queue/take-back behavior;
- hook install/uninstall and backup;
- permission/plan approvals;
- resume/background session, new session, trust-folder handling;
- documented Windows/WSL behavior confirmed from source.
This list is not exhaustive. Never remove a feature because it complicates 3D. If README and source differ, source behavior must be recorded and tested.

### FR-003 Renderer independence
Domain/session state and presentation must be separated. Scanning, event interpretation, tree, token accounting, prompt dispatch, hooks, permission workflow and process lifecycle work without graphics. Renderer failures are isolated.

### FR-004 Genuine 3D office
Provide 3D geometry and characters, depth/perspective, camera with accessible framing/limited orbit/zoom, work/rest/meeting/lobby zones, state visualization, selection, and movement/working/idle/waiting/completion/interaction animations. Avoid expensive real-time effects by default. Details remain in terminal text UI; scene must remain legible at terminal resolution.

### FR-005 Rendering modes
Provide `auto`, `3d`, `3d-reduced`, `static`, `2d-fallback`, and `text-fallback`. Static is event-driven with no continuous animation. Reduced mode disables expensive effects and caps FPS. Mode changes preserve session selection, tab, scroll/filter and prompt panel state; fallback should not require restart when feasible.

### FR-006 Terminal protocols
Retain and test iTerm2, Kitty, Sixel and half-block/text auto-detection. Never assume terminal supports direct GPU APIs. Validate frame output and encoding in a technical spike before selecting renderer technology.

### FR-007 Interactions
Preserve existing keyboard/mouse actions: select agent, open/close card, navigate, tree, inspect, prompt panel, tabs, rescan and quit. Camera controls cannot override existing shortcuts. Full keyboard operation remains available.

### FR-008 Resource governor
Renderer never blocks core event loop. Use visibility/focus-aware pause, capped FPS, bounded/coalescing queues, batching/instancing, no per-frame allocation churn, deterministic disposal, and no continuous animation for static scenes. Add `--no-3d`, `--render-mode`, `--max-fps`, and `--resource-profile` without breaking existing CLI. Auto-degrade on sustained pressure or device errors. See RESOURCE-BUDGET.

### FR-009 Diagnostics
Expose renderer mode, target/current FPS, frame time, memory estimate where measurable, scan duration, counts and fallback reason. Never expose credentials, full prompt bodies or transcript contents.

### FR-010 Privacy/security
Local-first. Renderer has no network capability. Credentials never printed, serialized to snapshots, sent to renderer or logged. Preserve existing usage endpoint isolation/offline setting. Prompt panel may display content as upstream does; warn about shoulder-surfing. Hook changes only through explicit install/uninstall with backups preserved.

### FR-011 Configuration
Add rendering mode, frame cap, resource profile, reduced-motion/static option and graphics disablement. Precedence: CLI > project/user config > safe defaults. Never silently modify Claude account settings.

### FR-012 Graceful failure
Missing GPU, unsupported protocol, init/device/OOM error, invalid assets, resize or suspend/resume must not stop core or lose prompt/permission state. Provide diagnostic and fallback.

### FR-013 Accessibility
Reduced motion, disable animation, color-independent status, keyboard operation, readable contrast and adjustable camera. Animation is never the only status channel.

### FR-014 Packaging
Reproducible Windows x64, macOS Apple Silicon and (if supported) Intel builds; checksums, install instructions, version info and unsigned/notarized status. No elevated privilege for ordinary use.

### FR-015 Observability
Privacy-safe diagnostics and opt-in support bundle excluding secrets/transcript bodies by default, with preview before writing. No telemetry upload.

## 7. Non-functional requirements
- NFR-001: Meet measured budgets on reference hardware.
- NFR-002: No crash/deadlock/lost prompts/lost permission answers/settings corruption during mode changes, resize, sleep/wake and repeated launch/exit.
- NFR-003: Core input/dispatch/permission paths never wait for GPU/render tasks.
- NFR-004: Bounded memory under long sessions and high event volume; soak tests required.
- NFR-005: Isolate OS APIs; handle Unicode, spaces, case sensitivity, Windows UNC/drive/WSL paths and macOS permissions.
- NFR-006: Small modules, documented interfaces, justified dependencies, reproducible toolchain; no wholesale rewrite absent evidence.
- NFR-007: Preserve flags, formats, hooks, prompts, keys and terminal protocols unless explicitly versioned and approved.

## 8. Acceptance criteria
1. Clean CI builds for every supported OS/architecture.
2. Full upstream compatibility matrix passes; no unexplained regressions.
3. Core tests pass with renderer disabled and deliberately faulted.
4. 3D is demonstrably 3D: geometry, depth, character, camera and state-driven movement.
5. All modes switch without loss of core/session/control state.
6. Resource budgets pass for each platform.
7. At least 8-hour soak shows bounded memory reaching a plateau.
8. Stress/recovery tests have no lost prompts, duplicate permissions or corrupted settings/hooks.
9. Keyboard parity and supported mouse interaction.
10. Security review verifies no renderer network access and privacy-safe logs/snapshots.
11. Fresh-machine install/upgrade validation on Windows/macOS.
12. Docs explain modes, limits, resource behavior and platform differences.

## 9. Constraints and decisions
3D becomes default only on capable terminals after budgets pass; until then auto picks the best supported measured mode. Core must work if 3D never initializes. Select engine only after comparing terminal encoding, portability, memory/binary size, dependency license, headless tests and fallback. Retain current 2D renderer during migration. The implementation will merge these specifications into an upstream clone; this repo does not replace upstream source.

## 10. Open decisions
Research/prototype which Rust renderer can produce actual offscreen 3D frames on both OS families and encode to terminal protocols; determine tested terminal versions, minimum macOS, Windows process APIs and reference hardware. Every decision requires measured evidence and an owner-approved decision record.
