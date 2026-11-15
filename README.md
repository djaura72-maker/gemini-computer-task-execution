# Gemini macOS Task Execution & On-Demand Automation Skills

Screenshot-free macOS desktop automation skills for **Gemini**, evolved from `hermes-computer-task-execution`. This repository provides two complementary skills using native macOS shell commands, AppleScript (`osascript`), and System Events Accessibility mapping without capturing screenshots.

## Included Skills

| Skill | File | Focus |
| :--- | :--- | :--- |
| **`computer-task-execution`** | [`SKILL.md`](SKILL.md) | Launching apps/URLs (`open -a`), inspecting System Events UI hierarchies, clicking controls, and automating Apple Notes |
| **`macos-on-demand-automation`** | [`skills/macos-on-demand-automation/SKILL.md`](skills/macos-on-demand-automation/SKILL.md) | Full on-demand Mac automation: file/folder sorting, clipboard (`pbcopy`/`pbpaste`), notifications, Dark Mode & volume toggles, app lifecycle, and UI fallback |

## Key Capabilities

- **Layered Automation Priority:** Picks native shell/CLI tools first, then app AppleScript dictionaries, and falls back to System Events UI scripting only when needed.
- **Direct App, URL & Window Control:** Opens, quits, and switches apps or URLs deterministically with `open -a` and `osascript`.
- **Files, Clipboard & System Utilities:** Automates batch file organization, clipboard read/write, macOS notifications, volume, and Dark Mode.
- **System Events Accessibility Inspection:** Queries UI element roles, titles, and properties as text via `osascript` before clicking buttons or sending shortcuts.
- **Built-In Safety Guardrails:** Blocks automated input into password fields, sudo prompts, keychain dialogs, and protected system directories (`/System`, `/bin`, `/usr/bin`).

## Installation

1. Download or clone this repository.
2. Upload [`SKILL.md`](SKILL.md) and/or [`skills/macos-on-demand-automation/SKILL.md`](skills/macos-on-demand-automation/SKILL.md) in Gemini's **Skills Manager** UI (or ask Gemini to import them from your local folder).
3. *(For UI button clicking via System Events)* Enable **Accessibility** permissions for Terminal / Gemini in **System Settings → Privacy & Security → Accessibility**.

## Example Prompts

Once enabled, trigger either skill naturally in Gemini:

- *"Organize my Downloads folder by file type"*
- *"Toggle Dark Mode on my Mac"*
- *"Open VS Code on my project folder and show a macOS notification when it's ready"*
- *"Create a new note in Apple Notes with today's study checklist"*
- *"Click the Share button in the active Safari window"*

## Repository Structure

```text
.
├── SKILL.md                                     # computer-task-execution skill
├── skills/
│   └── macos-on-demand-automation/
│       └── SKILL.md                             # macos-on-demand-automation skill
├── README.md                                    # Documentation, setup, and usage examples
├── CHANGELOG.md                                 # Release history
├── CONTRIBUTING.md                              # Guidelines for adding macOS workflows
├── LICENSE                                      # MIT License
└── .gitignore                                   # Standard macOS and editor ignore rules
```

## License

This project is licensed under the **MIT License** — see [`LICENSE`](LICENSE) for details.
