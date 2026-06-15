# ChipsRepos Umbrella

This repository is an umbrella for shared development configuration, IDE settings, and cross-repo automation that applies across the sibling repositories stored here.

## What this repo tracks

The repository uses an **ignore-by-default** model. Only these items are tracked in Git:

- `.github/` — Copilot guidance and shared repository metadata
- `.idea/` — JetBrains IDE shared workspace configuration
- `.vscode/` — VS Code shared settings
- `.editorconfig` — Shared editor rules
- `ChipsRepos.code-workspace` — VS Code multi-folder workspace
- `scripts/` — Shared automation and utilities
- `README.md` — This file

Everything else is automatically ignored.

## Layout

- **Nested directories** (`bggstuff`, `ChipsPlayGround`, `cthulhucli`, `geekrush`, `gitignore`, `GoWork`, `RulesEngine`, `xgit`) are independent Git repositories
- **Root-level tracked files** are explicitly whitelisted in `.gitignore`
- **`scripts/`** is reserved for shared automation that works across all repositories
- **`ChipsRepos.code-workspace`** opens multiple repos in VS Code as a single workspace

## Adding new shared assets

To add a new file or folder to this umbrella repository:

1. Create or edit the file
2. Unignore it in `.gitignore` with `!path/to/file` or `!path/to/dir/` and `!path/to/dir/**`
3. Stage and commit: `git add <file>` and `git commit`

Example:

```
# Track a new config file
!config.ini

# Track a new shared folder
!configs/
!configs/**
```

Keep tracked files focused on shared configuration, workspace metadata, and cross-repo automation. **Leave project-specific source code in each nested repository.**

## For Copilot sessions

See `.github/copilot-instructions.md` for guidance on working across this umbrella and its nested repositories.
