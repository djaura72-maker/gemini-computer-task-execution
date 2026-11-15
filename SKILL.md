---
name: computer-task-execution
description: Execute desktop tasks on macOS, Linux, and Windows without screenshots using native shell commands, AppleScript (osascript), and System Events UI element mapping. Compatible with any AI agent that has terminal or shell execution access.
version: 0.3.0
license: MIT
platforms: [macos, linux, windows]
compatibility: Universal (Gemini, Hermes Agent, Claude Code, OpenCode, Cursor, local LLM tool-calling agents)
---
# Computer Task Execution (Universal Cross-AI)

Execute desktop tasks without screenshots using native OS launch commands, shell utilities, and (on macOS) AppleScript (`osascript`) UI element mapping. Designed to work across any AI agent runtime.

## Cross-AI Compatibility

Use whichever execution tool your current AI runtime provides:
- **Shell / Terminal Agents (Claude Code, OpenCode, Cursor, Gemini, local LLMs):** Run the `open -a`, `osascript`, `xdg-open`, or `powershell` commands below via your terminal/shell tool.
- **Accessibility-Capable Agents (e.g., Hermes Agent):** Optionally pair with `computer_use(action="capture", mode="ax")` and `cdp(...)` when available, falling back to `osascript` / shell commands otherwise.

## When to Use

- Launching or switching applications (Safari, Chrome, Notes, VS Code, Finder).
- Opening URLs directly in a target browser.
- Inspecting or clicking macOS app UI controls via System Events Accessibility hierarchy.
- Automating native macOS apps such as Apple Notes.

**Do not use for:**

- Pure file edits (use native file read/write tools directly instead).
- Entering passwords, keychain credentials, or interacting with security/authorization modals.

## Steps

### 1. Launch Apps and URLs Directly

Prefer direct OS launch primitives over GUI menu navigation:

```bash
# macOS
open -a "Safari"
open -a "Safari" "https://github.com"

# Linux
xdg-open "https://github.com" &

# Windows (PowerShell / CMD)
start msedge "https://github.com"
```

### 2. Inspect UI Elements via System Events (macOS)

Query an app window's Accessibility hierarchy as text first so you target exact element names and roles:

```bash
osascript -e 'tell application "System Events" to tell process "Safari" to get properties of UI elements of window 1'
```

### 3. Click Controls or Automate Native Apps (macOS)

```bash
# Click a named button in a window
osascript -e 'tell application "System Events" to tell process "Safari" to click button "Share" of window 1'

# Create a new note in Apple Notes
osascript -e 'tell application "Notes" to make new note at folder "Notes" with properties {name:"Meeting Notes", body:"Agenda: ..."}'
```

### 4. Verify State Changes

Re-query the target window's UI elements or check app state after executing an action to confirm the expected change took place.

## Gotchas

- **Sandboxed Runtimes:** If your AI runtime's shell sandbox blocks GUI automation or `osascript` (e.g., error `-10827`), do not loop or retry—explain the restriction plainly and give the user the exact command to run in Terminal.
- **Accessibility Permissions:** `System Events` UI scripting requires Accessibility permission for the host app in **System Settings - Privacy & Security - Accessibility** (error `-1719` or `not allowed assistive access`).
- **Safety Protection:** Never automate input into password fields, sudo prompts, or system authorization dialogs.
