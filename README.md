# ios-verify-ui

A Claude Code plugin that builds, runs, and visually verifies iOS apps on a simulator using [XcodeBuildMCP](https://github.com/cameroncooke/XcodeBuildMCP).

## Skills

| Skill | Invoke | Description |
| ----- | ------ | ----------- |
| verify-ui | `/ios-verify-ui:verify-ui` | Build and run the app, take a screenshot, evaluate against UI conventions |
| verify-test | `/ios-verify-ui:verify-test` | Run the unit and UI test suite, report pass/fail with details |
| verify | `/ios-verify-ui:verify` | Full check: runs `verify-ui` then `verify-test` in sequence |

## Prerequisites

- Xcode 16+ with at least one iOS 18+ simulator installed
- [XcodeBuildMCP](https://github.com/cameroncooke/XcodeBuildMCP) configured as a Claude Code MCP server

## Installation

```bash
claude plugin add https://github.com/vivqu/claude-ios-verify-ui-plugin
```

## Usage

```bash
/ios-verify-ui:verify-ui
/ios-verify-ui:verify-test LoginTests
/ios-verify-ui:verify
```

Pass a description of what changed to verify-ui:

```bash
/ios-verify-ui:verify-ui login button color changed to red
```

### Extending UI Conventions

Pass a path to a supplemental conventions Markdown file:

```bash
/ios-verify-ui:verify-ui ./docs/my-conventions.md
```

The skill detects file paths (starts with `/`, `./`, `~/`, or ends in `.md`) and merges the file's rules with the built-in conventions.

## Built-in UI Conventions

See [`skills/verify-ui/references/ui-conventions.md`](skills/verify-ui/references/ui-conventions.md).

Key rules:

- Respect safe areas — never underlap the status bar, Dynamic Island, or home indicator
- All interactive and meaningful UI elements must have `.accessibilityIdentifier` set
- Minimum 4.5:1 contrast ratio (WCAG AA)
- Use adaptive semantic colors for light/dark mode support

## License

MIT
