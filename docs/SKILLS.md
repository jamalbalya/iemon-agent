# Project-local skill operating guide

The owner supplied a ZIP with 41 professional role skills plus a `.codex`-oriented copy. It includes a master skill activation router and skills for engineering, frontend/full-stack, UI/UX, AI, QA/SDET, security and DevSecOps.

## Mandatory use
1. Read `skill/36-master-skill-activation-router.md` first when available.
2. Let its routing workflow select the relevant primary/supporting skills.
3. Read selected skill files fully before the task.
4. Record selected filenames, rationale and applied guidance in task/PR notes.
5. Do not load all skills for every task.
6. If `skill/` is absent or structured differently, inspect and report; do not fabricate content.

## Suggested task mapping
| Work | Primary | Supporting |
|---|---|---|
| Architecture/delivery | `05-senior-engineering-manager.md` | `03-senior-fullstack-engineer.md` |
| Rust/platform/core | `02-senior-backend-engineer.md` | `03-senior-fullstack-engineer.md`, `16-senior-devsecops.md` |
| 3D visual design | `41-anti-ai-slop-ui-art-director.md` | `07-senior-uiux-designer.md`, `01-senior-frontend-engineer.md` |
| AI/session/hooks | `29-senior-ai-engineer.md` | `31-senior-prompt-engineer.md`, `08-senior-security-engineer.md` |
| Compatibility/QA | `38-senior-qa-architect.md` | `40-senior-sdet-architect.md`, `39-senior-sdet.md`, `04-senior-qa-engineer.md` |
| Performance | `40-senior-sdet-architect.md` | `04-senior-qa-engineer.md`, `02-senior-backend-engineer.md` |
| Security/release | `16-senior-devsecops.md` | `08-senior-security-engineer.md` |

The master router takes precedence within constraints in `AGENTS.md`.

## Important
This spec repo does not bundle/copy the skill library. The owner will add the ZIP skills to the app repo separately. Expected layout is `skill/*.md` and `.codex/...`. If Claude Code's current discovery convention expects `SKILL.md` directories or another layout, inspect and implement a compatible discovery/index mechanism; do not silently rename/rewrite files. Skills cannot override requirements, safety, security or owner instructions.
