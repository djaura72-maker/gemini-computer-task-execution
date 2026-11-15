# Contributing to Gemini macOS Automation Skills

Contributions to expand macOS shell and AppleScript (`osascript`) automation workflows are welcome!

## Guidelines

1. **Layered, Zero-Screenshot Design:** Prefer native CLI/shell tools first, then app AppleScript dictionaries, and System Events UI scripting only as a fallback. Never introduce screenshot or pixel-coordinate dependencies.
2. **Safety First:** Never add patterns that automate password fields, keychain prompts, sudo credentials, system authorization dialogs, or protected system directories.
3. **Verify Locally:** Test every shell and AppleScript snippet in macOS Terminal before opening a pull request, and keep `README.md` and `CHANGELOG.md` in sync.
