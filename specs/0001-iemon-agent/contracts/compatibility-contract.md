# Compatibility contract

Pin upstream source as behavioral reference. Inventory public CLI, keys, hook names/payload expectations, settings edits, prompt timing, state inference, token accounting, parsing, terminal protocols and OS behavior.

Compatibility requires existing invocation syntax, equivalent outputs/status semantics, stable session IDs and prompt ordering, correct permission idempotency, reversible hook install/uninstall with settings backups, useful dump/snapshot behavior, terminal restoration, actionable unsupported-capability errors and fixtures for malformed/partial transcripts.

Any intentional breaking change requires a new spec decision, migration notes, tests and explicit owner approval.
