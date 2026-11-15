# Gemini Computer Task Execution Skill (macOS)

A screenshot-free macOS desktop automation skill for **Gemini**, adapted from `hermes-computer-task-execution`. It uses native macOS shell commands (`open -a`) and AppleScript (`osascript`) with System Events Accessibility mapping to control apps, open URLs, and automate Apple Notes without capturing screenshots.

## Key Capabilities

- **Direct App & URL Launching:** Opens macOS apps and browser URLs with `open -a` instead of GUI navigation.
- **System Events Accessibility Inspection:** Queries UI element roles, titles, and properties as text via `osascript`.
- **Apple Notes Automation:** Creates and structures notes directly through Apple Notes' AppleScript dictionary.
- **Built-In Safety Guardrails:** Explicitly blocks automated input into password fields, sudo prompts, and system authorization dialogs.

## Installation

1. Download or clone this repository.
2. Upload `SKILL.md` in Gemini's **Skills Manager** UI (or ask Gemini to import it from your local folder).
3. *(For UI button clicking via System Events)* Enable **Accessibility** permissions for Terminal / Gemini in **System Settings → Privacy & Security → Accessibility**.

## Example Prompts

Once enabled, trigger the skill naturally in Gemini:

- *"Open my GitHub profile in Safari"*
- *"Launch VS Code and Notes"*
- *"Create a new note in Apple Notes with today's study checklist"*
- *"Click the Share button in the active Safari window"*

## Repository Structure

```text
.
├── SKILL.md          # Canonical Gemini skill definition
├── README.md         # Documentation, setup, and usage examples
├── CHANGELOG.md      # Release history
├── CONTRIBUTING.md   # Guidelines for adding macOS AppleScript workflows
├── LICENSE           # MIT License
└── .gitignore        # Standard macOS and editor ignore rules
```

## License

This project is licensed under the **MIT License** — see `LICENSE` for details.
