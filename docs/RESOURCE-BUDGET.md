# Resource budget and performance gates

Performance is a release requirement: IEMON must not noticeably interfere with normal work. These initial targets must be validated against upstream baseline on Windows and macOS. Do not loosen them to force a pass without owner approval.

| Metric | 3D normal | 3D reduced | Static/fallback |
|---|---:|---:|---:|
| Frame cap | 20 FPS | 10 FPS | 0 continuous |
| Foreground CPU average | <= 8% of one logical core | <= 4% | <= 2% |
| Idle/unfocused CPU average | <= 1% | <= 1% | <= 0.5% |
| Incremental renderer resident memory | <= 150 MiB | <= 100 MiB | <= 40 MiB |
| GPU memory if measurable | <= 128 MiB | <= 64 MiB | <= 32 MiB |
| Core input p95 latency | <= 100 ms | <= 100 ms | <= 100 ms |

CPU is normalized to one core (100% means one fully utilized logical core). Memory is renderer incremental overhead over core/text baseline. GPU metrics may not be available on all platforms; record limitations and use process/system metrics and frame timing.

## Workload profiles
- Idle: no transcript changes.
- Typical: 1-3 sessions, up to 10 agents.
- Busy: 5-10 sessions, up to 30 agents.
- Stress: 20 sessions or 100 agents, whichever occurs first.
- Recovery: repeated renderer restart, resize, sleep/wake and device failure.

## Required behavior
1. Static scenes render only on state change.
2. Unfocused/hidden scenes stop continuous frame production.
3. If budgets are exceeded for 10 seconds, degrade one level; recover only after 30 seconds below a hysteresis threshold.
4. Scanning cadence is independent of render FPS.
5. Coalesce visual events rather than queueing each transcript line.
6. Bound frame buffers, queues, textures, agent instances and caches.
7. Avoid synchronous GPU readback and blocking resource creation on input thread.
8. Renderer uses immutable snapshots/bounded channels; stale snapshots can be replaced.
9. Verify cleanup on mode switch and exit.

## Benchmark protocol
Record OS, CPU, RAM, GPU, terminal/version, build, mode, agent/session counts, warmup, duration, median/p95 CPU, resident/GPU memory if measurable, frame time, input latency and scan latency. Run three repetitions. Compare upstream baseline, IEMON core/text, 2D fallback, 3D reduced and 3D normal. Test Apple Silicon and Windows hardware; test Intel Mac if supported. Never publish transcript or credential information.

## Release gate
Fail a platform/mode if over budget, visibly lags input, blocks core work, leaks unbounded memory, or loses/duplicates control events. Auto mode must select a cheaper mode and explain the fallback.
