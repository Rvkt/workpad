# Workpad

Workpad is a minimal collection of work-related developer notes, troubleshooting solutions, useful commands, and aliases.

It serves as a clean, practical reference library—not a task manager, project management system, or second-brain productivity framework.

## Folder Structure

```text
Workpad/
├── Troubleshooting/
├── Commands/
├── Aliases/
├── Templates/
├── README.md
└── .obsidian/
```

## Folder Responsibilities

- **Troubleshooting/**: Technical problems, error messages, investigation steps, workarounds, and verified solutions. Follow the rule: *one problem per Markdown note*.
- **Commands/**: Frequently used commands, scripts, and command-line examples (e.g., Git, Docker, Linux, CLI tools).
- **Aliases/**: Shortcuts and aliases for developer tools (Git, Bash, Zsh, PowerShell) along with configuration and setup instructions.
- **Templates/**: Standardized templates to ensure consistent, readable note structures across the vault.

## Note Creation Conventions

1. **One Note per Topic**: Keep notes atomic—one technical problem, command set, or alias group per note.
2. **Readable File Names**: Use clear, human-readable titles (e.g., `Git Rebase Conflict on Merge.md`, `Docker System Prune.md`).
3. **Template Usage**: Apply the appropriate template from `Templates/` when creating new notes:
   - `Troubleshooting Template`
   - `Command Template`
   - `Alias Template`
   - `General Reference Template`
4. **Internal Linking**: Prefer internal Wikilinks (`[[Note Name]]`) for cross-referencing related notes.
5. **Verified Solutions**: Focus on verified solutions and practical references over untested suggestions.
6. **No Clutter**: Keep notes markdown-first and Git-friendly. Do not add unnecessary metadata, tags, or status tracking.

## Basic Usage Guidelines

- **Capturing Notes**: Choose the target folder, create a note with a descriptive title, insert the corresponding template from `Templates/`, and document the details.
- **Searching Notes**: Retrieve notes quickly using Obsidian's Quick Switcher (`Ctrl+O` / `Cmd+O`) or Global Search (`Ctrl+Shift+F` / `Cmd+Shift+F`).
- **Git Version Control**: The vault is Git-ready with a `.gitignore` that preserves notes and essential settings while excluding transient workspace state and local caches.
