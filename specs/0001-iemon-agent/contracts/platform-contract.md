# Platform adapter contract

Platform-specific concerns live behind Windows/macOS interfaces:
- Claude configuration/project roots and path expansion;
- process/session discovery and PID liveness;
- process creation/resume and working directory;
- filesystem watch/poll;
- terminal capability/protocol detection and terminal restoration;
- signals, shutdown, suspend/resume;
- clipboard if supported by upstream.

Handle spaces, Unicode, case sensitivity, Windows drives/UNC/WSL, macOS app environments, permissions and missing APIs. Unit tests use fakes; integration tests run on native OS CI. Platform branching must not leak into transcript parsing or domain state.
