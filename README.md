# gitroot

`D:\code` is the umbrella repository for shared development configuration and automation that applies across the sibling repositories stored here.

## Layout

- Nested directories such as `bggstuff`, `ChipsPlayGround`, `GoWork`, and the other existing project folders remain independent Git repositories.
- Root-level tracked files are explicitly whitelisted in `.gitignore`.
- `scripts\` is reserved for shared automation that works across the repositories in this folder.
- `ChipsRepos.code-workspace` is the shared VS Code workspace for the repo set.

## Tracking model

This repository uses an ignore-by-default `.gitignore`. To add a new shared asset, unignore it explicitly in `.gitignore` before staging it.

Examples:

- Track a root config file: `!nuget.config`
- Track a folder of shared settings: `!configs/` and `!configs/**`

Keep tracked files focused on shared configuration, workspace metadata, and cross-repo automation. Leave project-specific source code in each nested repository.
