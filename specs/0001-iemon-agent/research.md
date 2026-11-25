# Research questions and decision log

No final renderer engine/dependency is selected yet. Selection is gated on a true terminal-rendering prototype and measurements.

## Candidate criteria
True 3D geometry/camera/materials/animation; offscreen image support; iTerm2/Kitty/Sixel encoding; Windows/macOS Intel/Apple Silicon; software fallback; CPU/RAM/GPU/VRAM and binary/dependency size; headless deterministic testing; license/maintenance/security; pause and disposal; integration cost with Rust terminal application.

## Decision record template
- Decision and date/owner:
- Options compared:
- Prototype commit:
- OS/hardware/terminal:
- Measurements:
- Compatibility impact:
- Dependency licenses:
- Risks:
- Selected option and rationale:
- Rejected options and rationale:
- Rollback/fallback:

## Mandatory spike questions
Can it render real 3D offscreen on both OS families? Can frames encode to target terminal protocols without corruption? What are CPU/RAM/VRAM/binary costs at static and 10/30/100 agents? Can it fully pause when hidden? Is software fallback acceptable? Is licensing compatible with proprietary distribution?
