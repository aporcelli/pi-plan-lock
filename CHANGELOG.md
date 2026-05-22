# Changelog

All notable changes to this project will be documented in this file.

## [0.3.1] — 2026-05-22

### Changed

- Added npm package metadata fields in `package.json`:
  - `repository`
  - `homepage`
  - `bugs`
- README restructured into a more visual quick-scan format (emoji sections, clearer command flow, architecture summary).
- Version bumped to `0.3.1` for documentation + package metadata refresh.

## [0.3.0] — 2026-05-22

### Added

- Keyboard shortcut `F3` to toggle plan mode ON/OFF.
- Shortcut uses the same internal flow as `/plan on` and `/plan off`, including lock checks.

### Changed

- README command table and header examples now include `F3` toggle support.
- Package version bumped to `0.3.0`.

## [0.2.0] — 2026-05-20

### Added

- **State awareness**: `before_agent_start` now ALWAYS injects plan mode state into
  every response generation. When ON, the model sees a structured `🔒` block with
  tool list, lock state, and explicit guidance for blocked tools. When OFF, it
  sees a `🔓` block confirming full tool access restored. Prevents "model tries
  blocked tool → error → retry loop" confusion.
- Documented state awareness in README architecture section.

### Changed

- `before_agent_start` handler no longer returns early when plan mode is OFF.

## [0.1.1] — 2026-05-20

### Changed

- Renamed package to `@porche/pi-plan-lock` (scoped).
- Updated README with full visual redesign, emojis, tables, ASCII arch diagram.
- Added English summary and compatibility section for agents/skills.
- Documented limits of slash commands vs. event-layer blocking.

## [0.1.0] — 2026-05-20

### Added

- Initial `/plan` extension with strict read-only planning mode.
- Tool gate: blocks `write`, `edit`, `bash`, MCP tools; only `read`, `grep`, `find`, `ls` pass.
- Sensitive path blocking: `.env`, `.ssh`, keys, credentials, secrets.
- Anti-jailbreak: prompt patterns in EN/ES/PT/FR detected and ignored.
- Lock mode: `/plan lock <key>` prevents `/plan off` until unlocked with same key.
- Anti-insistence: escalating response for users demanding execution.
- Input guard: blocks non-plan commands during plan mode.
- Read-loop prevention: limits excessive read/grep cycles.
- Footer status indicator: `plan (on) lock/unlock` — `plan (off) unlock`.
- `--plan` flag to start Pi already in plan mode.
