# Changelog

All notable changes to the `gemini-computer-task-execution` repository are documented in this file.

## [0.3.0] - 2026-11-15
### Changed
- Made both `SKILL.md` and `skills/macos-on-demand-automation/SKILL.md` vendor-agnostic and compatible with any AI agent (Gemini, Hermes Agent, Claude Code, OpenCode, Cursor, local LLM agents) by removing vendor-locked `allowed-tools` metadata and adding a Cross-AI Compatibility section.
- Added explicit sandbox fallback guidance (`-10827`) alongside Accessibility permission notes (`-1719`).

## [0.2.0] - 2026-11-15
### Added
- `skills/macos-on-demand-automation/SKILL.md`: Full on-demand macOS automation skill covering layered execution (shell/CLI, AppleScript app dictionaries, System Events fallback), clipboard (`pbcopy`/`pbpaste`), notifications, Dark Mode/volume toggles, and safety guardrails.
- Updated `README.md` and `CONTRIBUTING.md` to cover both skills and the expanded repository structure.

## [0.1.0] - 2026-11-15
### Added
- Initial Gemini-adapted `computer-task-execution` skill (`SKILL.md`) focused on macOS shell (`open -a`) and AppleScript (`osascript`) workflows.
- Initial repository documentation (`README.md`, `CONTRIBUTING.md`, `LICENSE`, `.gitignore`).
