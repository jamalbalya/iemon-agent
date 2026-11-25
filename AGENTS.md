# Instructions for AI coding agents

Mandatory project guidance: read before planning, editing, running commands or committing.

## Mission
Implement `specs/0001-iemon-agent/` while preserving the upstream Claude Monitor feature set. This repository is specifications/governance only; implementation follows after these specs are merged into a local clone of upstream.

## Mandatory startup
1. Read `README.md`, this file, and every document under `specs/0001-iemon-agent/`.
2. Read `docs/SKILLS.md`.
3. Inspect the actual project-local `skill/` directory. Never assume a skill exists.
4. Read `skill/36-master-skill-activation-router.md` first when present. Follow its routing rules, then read the selected skill files fully.
5. If `skill/` is absent, report that and continue without fabricating skill content.
6. Inspect upstream source, branch, build system, tests and actual platform constraints. README is not a substitute for source inspection.
7. Produce an implementation plan and identify compatibility risks before editing.

## Skill policy
Skills guide the work; they do not override this spec, safety, security, or owner instructions. They do not authorize destructive actions, data exfiltration, credential disclosure or unreviewed dependency installation.

Suggested routing:
- Architecture/delivery: `05-senior-engineering-manager.md`, `03-senior-fullstack-engineer.md`
- Rust/platform/performance: `02-senior-backend-engineer.md`, `03-senior-fullstack-engineer.md`
- UI/3D: `07-senior-uiux-designer.md`, `41-anti-ai-slop-ui-art-director.md`, `01-senior-frontend-engineer.md`
- AI/session/hooks: `29-senior-ai-engineer.md`, `31-senior-prompt-engineer.md`
- QA/SDET: `38-senior-qa-architect.md`, `40-senior-sdet-architect.md`, `39-senior-sdet.md`, `04-senior-qa-engineer.md`
- Security/release: `08-senior-security-engineer.md`, `16-senior-devsecops.md`
- Skill routing: `36-master-skill-activation-router.md`

Record chosen skills, rationale and applied checklist in implementation/PR notes. Do not load all 41 skills for every task.

## Hard constraints
- Preserve all existing features unless an approved spec change says otherwise.
- Renderer must not be a dependency of core monitoring/session control.
- 3D is optional presentation; never a prerequisite for core behavior.
- Rendering must never block scanning, hooks, input, prompt dispatch or permissions.
- No unbounded queues/buffers, uncontrolled frame loop or per-frame heap churn.
- No renderer network calls, telemetry, analytics, model inference or cloud rendering.
- Keep credentials/raw transcript bodies out of logs, crash reports, snapshots and network requests.
- Do not silently alter settings, hooks, permission semantics, session IDs or file formats.
- Do not claim performance compliance without Windows and macOS measurements.
- No unsafe Rust without documented rationale and focused tests.
- Never commit secrets, transcripts, credentials or machine-specific files.

## Workflow and done criteria
Map every upstream feature to tests; measure upstream baseline; implement platform adapters and renderer behind interfaces; test core without graphics and with renderer fault injection; add functional, integration, performance, leak, interaction and cross-platform CI coverage; run format/lint/tests/release builds; review diff for regressions/security/dependency bloat/resource budget. Completion requires acceptance criteria, regression tests, platform checks, resource budgets and docs. Record unavailable tests honestly.
