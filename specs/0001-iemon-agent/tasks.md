# Implementation task breakdown (planning only)

Do not begin full renderer work before baseline inventory and spike approval.

## P0 — Baseline
- [ ] Pin and inspect upstream commit.
- [ ] Build/run upstream on Windows/macOS.
- [ ] Inventory CLI, keys, modules, hooks, data formats.
- [ ] Create compatibility fixtures and baseline report.
- [ ] Measure platform resource baseline.
- [ ] Activate relevant local skills and record selection.

## P1 — Platform
- [ ] Define platform interfaces.
- [ ] Implement/verify macOS process/path behavior.
- [ ] Preserve/verify Windows and WSL behavior.
- [ ] Add Windows/macOS CI and release builds.
- [ ] Verify terminal restoration and capability detection.

## P2 — Renderer spike
- [ ] Evaluate at least three credible approaches.
- [ ] Prototype true-3D offscreen frame.
- [ ] Validate iTerm2/Kitty/Sixel/half-block output.
- [ ] Measure CPU/RAM/VRAM and binary/dependency size.
- [ ] Record decision and obtain owner approval.

## P3 — Core separation
- [ ] Define immutable scene snapshot.
- [ ] Implement bounded/coalescing snapshot channel.
- [ ] Isolate renderer behind interface.
- [ ] Preserve 2D fallback.
- [ ] Test core without renderer and with fault injection.

## P4 — 3D
- [ ] Model office geometry/zones.
- [ ] Create/select appropriately licensed 3D assets.
- [ ] Map agent state to animation.
- [ ] Implement camera/selection.
- [ ] Add reduced-motion/static.
- [ ] Visual validation at terminal sizes.

## P5 — Resources
- [ ] FPS cap and visibility/focus pause.
- [ ] Adaptive quality/hysteresis.
- [ ] Bound all queues/caches/buffers.
- [ ] Add diagnostics.
- [ ] Stress, soak and recovery testing.
- [ ] Meet budgets on each platform.

## P6 — Release
- [ ] Run complete compatibility matrix.
- [ ] Test Windows/macOS.
- [ ] Audit dependencies/licenses/security/privacy.
- [ ] Fresh-machine install and upgrade validation.
- [ ] Publish checksums, support matrix and release notes.
- [ ] Owner accepts residual risks.
