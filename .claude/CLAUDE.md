# Devbook — Claude Code Instructions

## 1. Purpose

Devbook is a personal, work-focused engineering knowledge base.

It is an Obsidian vault backed by Git, intended to preserve practical technical knowledge, troubleshooting solutions, reusable commands, workflow shortcuts, external resources, and technical references.

The primary objective is to build a clean, searchable, reusable engineering handbook.

## 2. Directory Structure

Maintain the following structure:

```text
Devbook/
├── .claude/
│   └── CLAUDE.md
├── .obsidian/
├── Troubleshooting/
├── Commands/
├── Aliases/
├── Clippings/
├── References/
│   ├── Decisions/       (ADRs)
│   ├── Personal/        (legacy exception — see §10)
│   └── MOCs/            (per-folder Dataview index notes)
├── Roadmaps/            (per-technology learning tracks, e.g. Roadmaps/Python)
│   └── Roadmaps MOC.md  (Dataview index over the #roadmap tag)
├── README.md
└── .gitignore
```

New top-level directories still require explicit approval; `Roadmaps/` is approved. Subfolders under `References/` as shown above are permitted; avoid adding further subfolders under `References/` or `Roadmaps/` without approval.

Every note under `Roadmaps/<Track>/` must carry `tags: [roadmap, roadmap/<track-slug>]` in its frontmatter (track slug lowercase, hyphenated, e.g. `roadmap/react-native`) so it is discoverable via the `#roadmap` tag and grouped correctly by `Roadmaps/Roadmaps MOC.md`.

## 3. Content Categories

### Troubleshooting/

Purpose: Document technical problems and their solutions.

Examples:
- Application errors
- Build failures
- Deployment issues
- API failures
- Database problems
- Framework-specific issues
- Environment and configuration problems

Documentation structure:

# Problem Title

## Problem
Describe the issue and observed behavior.

## Root Cause
Explain the actual cause, when identified.

## Solution
Document the verified resolution.

## Verification
Explain how to confirm the issue is resolved.

## References
Include relevant documentation or source links.

Rules:
- One problem per note.
- Never invent root causes.
- Distinguish confirmed findings from hypotheses.
- Preserve relevant error messages and logs.
- Prefer reproducible solutions.
- Keep unresolved investigations in the same note.

### Commands/

Purpose: Maintain reusable development and terminal commands.

Examples:
- Git commands
- Linux commands
- Flutter commands
- Python and Django commands
- Database commands
- Docker commands
- Deployment commands

Documentation structure:

# Command Title

## Purpose
What the command does.

## Command
The exact command.

## Usage
Practical examples.

## Notes
Important flags, limitations, and risks.

Rules:
- Include only useful and reusable commands.
- Preserve exact syntax.
- Explain destructive operations and their consequences.
- Avoid documenting trivial commands without practical value.

### Aliases/

Purpose: Document developer workflow shortcuts and command aliases.

Examples:
- Git aliases
- Shell aliases
- Terminal shortcuts
- Development workflow shortcuts

Documentation structure:

# Alias Title

## Purpose
Why the alias exists.

## Configuration
The exact alias configuration.

## Usage
Example invocation and expected behavior.

## Notes
Mention whether the alias is local, global, or environment-specific.

Rules:
- Include actual configuration.
- Clearly distinguish local and global aliases.
- Avoid duplicating command documentation.

### Clippings/

Purpose: Preserve useful external engineering content.

Examples:
- Technical articles
- Engineering blog posts
- Tutorials
- Technical write-ups
- Architecture discussions
- Engineering best practices

Documentation structure:

# Resource Title

## Source
Original URL.

## Author / Publisher
Author or publisher, when available.

## Published
Original publication date, when available.

## Summary
A concise explanation of the resource.

## Key Takeaways
Important technical insights.

## Notes
Personal observations or practical applications.

Rules:
- Preserve the original source URL.
- Prefer authoritative and original sources.
- Include proper attribution.
- Do not copy entire copyrighted articles.
- Avoid saving duplicate or low-value content.
- Preserve the original context of the resource.

### References/

Purpose: Maintain reusable technical knowledge for quick lookup.

Examples:
- API references
- Technical specifications
- Architecture patterns
- Framework documentation
- Configuration examples
- Database concepts
- Security guidelines
- Performance guidelines
- Cheat sheets
- Protocol references

Documentation structure:

# Reference Title

## Overview
Brief explanation of the topic.

## Details
Relevant technical information.

## Examples
Code snippets, configurations, or practical examples.

## Important Notes
Limitations, considerations, and common pitfalls.

## Sources
Authoritative documentation and useful links.

Rules:
- Keep information concise and structured.
- Prefer evergreen technical knowledge.
- Use official documentation whenever possible.
- Preserve useful code examples.
- Distinguish facts from assumptions.
- Avoid duplicating content from other categories.
- Per-technology learning material (roadmaps, phase notes, technology stacks, learning resources) belongs under `References/Roadmaps/<Technology>/`.
- Architecture Decision Records belong under `References/Decisions/`.

## 4. Content Classification

Before creating a note, identify its primary purpose:

| Content | Destination |
|---|---|
| Technical problem and resolution | Troubleshooting |
| Reusable executable command | Commands |
| Workflow shortcut or alias | Aliases |
| External published content | Clippings |
| Reusable technical knowledge | References |

Choose one primary location for each note.

Use Obsidian links to connect related notes instead of duplicating information.

## 5. Markdown Conventions

- Use standard Markdown.
- Keep notes concise, readable, and practical.
- Use descriptive filenames.
- Use meaningful headings.
- Use fenced code blocks with language identifiers.
- Use relative Obsidian-compatible links.
- Prefer simple formatting over complex layouts.
- YAML frontmatter is allowed and expected: use `type`, `tags`, `created` (and `domain` on MOC notes) consistently with existing notes.
- Tags are allowed and already in use; keep them consistent with existing tag names rather than inventing new ones per note.

## 6. Obsidian Conventions

- Keep the vault Markdown-first.
- Keep the folder hierarchy shallow outside the `References/` subfolders listed in §2.
- Preserve compatibility with standard Obsidian functionality.
- Dataview is an accepted dependency: every folder's `*MOC.md` (or `Clippings.md`) note uses a Dataview query to auto-list its folder's contents. Keep this pattern when adding new folders' MOCs. Avoid introducing further plugin dependencies beyond Dataview without approval.
- Do not create new daily notes, task dashboards, or project-management structures for new content (see §10). `References/Personal/` and `References/Home.md` are existing legacy exceptions — do not add to them or model new notes on them.

## 7. Git Conventions

- Keep all documentation Git-friendly.
- Preserve existing repository structure.
- Do not modify `.obsidian/` settings unnecessarily.
- Never overwrite existing notes without inspecting them.
- Avoid unnecessary file renames and moves.
- Do not commit credentials, tokens, secrets, or sensitive company information.
- Keep changes focused on the requested task.
- Never modify Git history or repository configuration without explicit approval.

## 8. Working Behavior

Before creating or updating documentation:

1. Inspect the existing vault structure.
2. Search for existing notes covering the same topic.
3. Identify the appropriate category.
4. Follow the existing documentation conventions.
5. Create or update the note.
6. Check Markdown formatting and internal links.
7. Verify commands and technical examples when possible.

When updating existing notes:

- Preserve useful existing information.
- Modify only relevant sections.
- Avoid unnecessary restructuring.
- Do not create duplicate documentation.

When information is insufficient:

- Ask for clarification when necessary.
- Never fabricate technical details.
- Clearly identify unverified assumptions.
- Do not present speculative solutions as verified.

## 9. Security and Confidentiality

This is an office-related knowledge base.

- Never store passwords, API keys, access tokens, or credentials.
- Do not expose confidential company information.
- Sanitize internal URLs, customer data, and production identifiers where appropriate.
- Do not copy proprietary company documentation into external services without authorization.

## 10. Scope Protection

Devbook is an engineering knowledge base.

It is NOT:
- A project management system.
- A task tracker.
- A daily journal.
- A personal productivity system.
- A general-purpose second brain.
- A duplicate of project-specific documentation.

**Legacy exception:** `References/Personal/` (daily notes, journal entries, status reports, milestones) and `References/Home.md` (a dashboard note) predate this rule and are kept as-is. Do not expand them, do not use them as a model for new notes, and do not create equivalent structures elsewhere in the vault. If asked to log a daily note, journal entry, task list, or dashboard going forward, point out that it falls outside Devbook's scope per this section before proceeding.

Do not otherwise expand the scope without explicit approval.

## 11. Primary Objective

Every note should answer at least one practical question:

- How do I solve this problem?
- How do I execute this command?
- How do I perform this workflow faster?
- What useful external information should I preserve?
- Where can I quickly find reliable technical information?

Prioritize accuracy, clarity, reusability, and maintainability over documentation volume.
