---
name: computer-task-execution
description: Execute desktop tasks on macOS without screenshots using AppleScript (osascript), System Events UI element mapping, and native shell commands. Use when the user asks to launch or switch macOS apps, open URLs in Safari or Chrome, automate Apple Notes, or interact with macOS app windows and UI controls via terminal commands.
allowed-tools: client
---
# Computer Task Execution (macOS AppleScript and Shell)

Execute desktop tasks on macOS using native OS launch commands and AppleScript (`osascript`) UI element mapping, avoiding screenshot capture or pixel-coordinate guessing.

## When to Use

- Launching or switching macOS applications (Safari, Chrome, Notes, VS Code, Finder).
- Opening URLs directly in a target browser.
- Inspecting or clicking macOS app UI controls via System Events Accessibility hierarchy.
- Automating native macOS apps such as Apple Notes.

**Do not use for:**

- Pure file edits (use file tools directly instead).
- Entering passwords, keychain credentials, or interacting with security/authorization modals.

## Steps

### 1. Launch Apps and URLs Directly

Prefer `open -a` over GUI menu navigation because it is faster, deterministic, and requires no Accessibility permissions.

```bash
# Launch applications
open -a "Safari"
open -a "Notes"

# Open a URL directly in a target browser
open -a "Safari" "https://github.com"
```

### 2. Inspect UI Elements via System Events

When you need to interact with an open app window, query its Accessibility hierarchy as text first so you target exact element names and roles.

```bash
osascript -e 'tell application "System Events" to tell process "Safari" to get properties of UI elements of window 1'
```

### 3. Click Controls or Automate Native Apps

Target UI elements by their exact role and name, or use app-specific AppleScript dictionaries (such as Notes).

```bash
# Click a named button in a window
osascript -e 'tell application "System Events" to tell process "Safari" to click button "Share" of window 1'

# Create a new note in Apple Notes
osascript -e 'tell application "Notes" to make new note at folder "Notes" with properties {name:"Meeting Notes", body:"Agenda: ..."}'
```

### 4. Verify State Changes

Re-query the target window's UI elements or check app state with `osascript` after executing an action to confirm the expected change took place.

## Gotchas

- **Accessibility Permissions:** `System Events` UI scripting requires Accessibility permission for the host app (Terminal or Gemini) in **System Settings - Privacy & Security - Accessibility**. If `osascript` returns a permission error (`-1719` or `not allowed assistive access`), inform the user which app needs permission enabled rather than retrying blindly.
- **Safety Protection:** Never automate input into password fields, sudo prompts, or system authorization dialogs.
