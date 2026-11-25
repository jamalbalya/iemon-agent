# IEMON Agent — Product Specification

**Status:** Specification baseline (pre-implementation)  
**Owner:** Jamal Balya  
**Target platforms:** Windows 10/11 x64 and macOS (Intel + Apple Silicon)  
**Upstream reference:** https://github.com/cicingik/claude-monitor  
**Specification repository:** https://github.com/jamalbalya/iemon-agent

IEMON Agent is a proposed cross-platform evolution of the Claude Monitor terminal application. The goal is to preserve the upstream application's existing monitoring and session-control capabilities while adding a genuinely 3D animated office presentation that remains resource-conscious.

> This repository contains specifications and governance documents only. It is not yet the application implementation.

## Start here

1. Read [AGENTS.md](AGENTS.md) before any work.
2. Read [specs/0001-iemon-agent/spec.md](specs/0001-iemon-agent/spec.md).
3. Read the plan, data model, research, tasks, and contracts under `specs/0001-iemon-agent/`.
4. Inspect the upstream source code before proposing implementation changes.
5. Read and activate relevant local skills using `skill/36-master-skill-activation-router.md`.

## Non-negotiable principles

- Preserve all existing supported features; no feature may silently disappear.
- Windows and macOS are first-class targets; isolate platform differences behind adapters.
- 3D must not compromise monitoring, prompt delivery, hooks, permissions, session recovery, or terminal usability.
- Measure and bound resource use.
- Graceful degradation: 3D → reduced 3D → static/2D → text/half-block.
- No renderer telemetry, analytics, cloud dependency, network calls, or AI inference.
- No destructive upstream behavior changes without approved decisions and tests.

## License and repository privacy

The included `LICENSE` reserves all rights and grants no permission to clone, use, modify, redistribute, or create derivative works without the owner's prior written permission. A public GitHub repository can nevertheless be viewed and cloned; a restrictive license is not a technical access control. **Set this repository to Private** in GitHub Settings and grant access only to authorized collaborators.
