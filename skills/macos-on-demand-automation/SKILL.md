---
name: macos-on-demand-automation
description: Automate any task on demand on macOS using shell commands, AppleScript (osascript), System Events UI scripting, clipboard/file utilities, and system controls. Compatible with any AI agent that has terminal or shell execution access.
version: 0.3.0
license: MIT
platforms: [macos]
compatibility: Universal (Gemini, Hermes Agent, Claude Code, OpenCode, Cursor, local LLM tool-calling agents)
---
# macOS On-Demand Automation (Universal Cross-AI)

Automate desktop, file, app, and system tasks on demand on macOS. Always pick the fastest, most reliable layer first: native CLI/shell, then app AppleScript dictionaries, then System Events UI scripting only when no direct API exists.

## Cross-AI Compatibility

- **Any Shell/Terminal Agent (Gemini, Claude Code, OpenCode, Cursor, local LLMs):** Execute the commands below via your terminal/shell tool.
- **Sandboxed Agents:** If GUI/AppleScript execution is blocked by the host sandbox, run only shell/file commands (`mv`, `cp`, `find`, `python3`, `pbcopy`, `pbpaste`) and provide any `osascript` / `open -a` commands to the user directly.

## When to Use

- Organizing, renaming, archiving, or batch-processing files and folders on macOS.
- Launching, quitting, hiding, or arranging macOS applications and windows.
- Automating Safari, Chrome, Finder, Apple Notes, Reminders, or other scriptable macOS apps.
- Controlling macOS system utilities (clipboard, notifications, volume, appearance, running processes).
- Driving UI buttons, menus, or keystrokes in apps that lack a CLI or AppleScript dictionary.

**Do not use for:**

- Entering passwords, sudo credentials, keychain prompts, or bypassing macOS security/authorization dialogs.
- Modifying protected system directories (`/System`, `/bin`, `/usr/bin`).

## Steps

### 1. Choose the Right Automation Layer

1. **Shell / File Utilities (Fastest, works even in strict sandboxes):** Use `mv`, `cp`, `find`, `python3`, `pbcopy`, `pbpaste`, or `open -a` for files, folders, clipboard, and launching apps or URLs.
2. **App AppleScript Dictionaries (`osascript`):** Use direct app scripting (`tell application "Notes"`, `"Finder"`, `"Safari"`) for structured app actions.
3. **System Events UI Scripting (Fallback):** Use `tell application "System Events"` when an app has no CLI or AppleScript API for the requested action.

### 2. Common On-Demand Workflows

**Files, Clipboard, and Notifications:**

```bash
# Copy or read clipboard
printf "text" | pbcopy
pbpaste

# Show a macOS notification
osascript -e 'display notification "Task finished" with title "Automation"'
```

**Apps, Windows, and System Controls:**

```bash
# Launch or quit an app cleanly
open -a "Visual Studio Code" ~/my-project
osascript -e 'tell application "Safari" to quit'

# Toggle Dark Mode
osascript -e 'tell app "System Events" to tell appearance preferences to set dark mode to not dark mode'

# Set output volume (0 to 100)
osascript -e 'set volume output volume 50'
```

**Inspect and Click UI Controls (Fallback):**

```bash
# Inspect UI elements of the frontmost window first
osascript -e 'tell application "System Events" to tell process "Finder" to get properties of UI elements of window 1'

# Click a specific button or trigger a keyboard shortcut
osascript -e 'tell application "System Events" to tell process "Finder" to click button 1 of window 1'
osascript -e 'tell application "System Events" to keystroke "n" using {command down}'
```

### 3. Verify and Report

After running the automation, verify the result (check the target folder, query the app state, or confirm exit code `0`) and summarize what changed cleanly.

## Gotchas

- **Sandboxed / Policy-Blocked Actions:** If a shell sandbox blocks GUI automation or `osascript` (e.g., error `-10827`), do not retry—inform the user plainly and provide the exact command to run in Terminal.
- **Accessibility Permissions:** `System Events` UI scripting requires Accessibility permission for the host app in **System Settings - Privacy & Security - Accessibility** (error `-1719` or `not allowed assistive access`).
- **Destructive File Ops:** Confirm with the user before deleting or overwriting existing files in bulk.
