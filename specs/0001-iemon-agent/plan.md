# Implementation plan

## Phase 0 — Establish baseline (mandatory)
- Pin upstream commit; inspect actual code, modules, dependencies, CI, tests and README discrepancies.
- Build/run unmodified source on Windows/macOS and measure baseline resources.
- Add fixtures for transcripts, hooks, settings, subagents, usage and platform paths.
- Activate appropriate project-local skills.
**Exit:** reviewed inventory, tested baseline and recorded gaps.

## Phase 1 — Cross-platform foundation
Define platform interfaces for paths, process inspection/spawning, filesystem watching, terminal capabilities and shutdown. Verify macOS adapters while retaining Windows/WSL behavior. Add native OS CI.
**Exit:** core compatibility tests pass with renderer disabled on both OS families.

## Phase 2 — Renderer architecture spike
Compare Rust-compatible true-3D/offscreen approaches for terminal encoding, OS/CPU/GPU support, software fallback, RAM/VRAM, binary/dependency size, license and headless tests. Prototype character + camera; encode through at least one graphics protocol and half-block fallback. Benchmark Apple Silicon and Windows. Test resize/cleanup.
**Exit:** documented decision record supported by measurements and owner approval.

## Phase 3 — Core/renderer separation
Introduce immutable scene snapshots and bounded/coalesced event channel. Renderer must not mutate core except explicit user commands. Add lifecycle, fault containment, capability negotiation and mode switch. Retain existing 2D renderer.
**Exit:** core tests pass with absent, disabled and fault-injected renderer.

## Phase 4 — 3D office
Implement geometry, character rigs/animations, camera, state visuals, selection and interaction links; preserve semantic room zones and text details. Add reduced motion/static modes.
**Exit:** visual review and functional parity.

## Phase 5 — Resource governor
Implement FPS cap, focus pause, adaptive quality/hysteresis, bounded buffers, diagnostics and cleanup. Run soak, high-session, resize, suspend/resume, GPU failure and low-memory tests.
**Exit:** budgets pass or auto degrades without affecting core.

## Phase 6 — Release hardening
Cross-platform CI, compatibility matrix, dependency/license/security review, reproducible artifacts/checksums and fresh-machine install validation.
**Exit:** acceptance criteria met and residual risks accepted.
