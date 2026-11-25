# Renderer contract

Boundary: `Core -> bounded snapshot channel -> Renderer -> terminal protocol output`. Interactions return through `RendererInput -> CoreCommand`.

Renderer MUST NOT scan sessions, spawn processes, write files/hooks, decide permissions, or call network APIs.

Lifecycle requirements:
- initialize with terminal/device capabilities and config;
- submit snapshots non-blockingly, replacing stale pending snapshots;
- render only when allowed by FPS/visibility/resource policy;
- switch modes without losing core state;
- shutdown and restore terminal even after partial initialization.

Types follow upstream style after baseline inspection; this contract does not prescribe a graphics crate. Errors are contained, safely diagnosed and trigger fallback. Panics must not cross into core control flow. GPU faults never reset prompt queues or permission state.

Bound channels, images, textures, objects and caches. Use latest-value/coalescing for visual state. No synchronous GPU readback in the input thread and no core-state locks during rendering.
