# Copilot Instructions

## High-level architecture

This repository is an umbrella repo rooted at `D:\code`. Its purpose is to store shared configuration and cross-repo automation for the sibling repositories that also live under `D:\code`.

The child directories in `D:\code` are independent Git repositories, not source folders that belong to this repo. Treat them as external working trees unless the task explicitly targets one of those repos. Changes for this repo should stay focused on root-level shared assets such as:

- `.github\`
- `scripts\`
- shared workspace metadata like `ChipsRepos.code-workspace`
- future explicitly whitelisted config files or folders

The repository uses an ignore-by-default model. New files are ignored unless `.gitignore` explicitly unignores them. When adding a shared config surface, update `.gitignore` as part of the same change.

## Commands

There is no repo-wide build, test, or lint toolchain yet. For changes in this repo:

- Use `git status --short --ignored` from `D:\code` to confirm the whitelist behaves as expected.
- If you add or modify a script under `scripts\`, validate that script directly with the command appropriate to its language.

There is no standard single-test command because no test framework is configured at the umbrella-repo level.

## Key conventions

- Keep this repo scoped to shared config, workspace files, and cross-repo automation; do not absorb files from the nested project repositories.
- Prefer root-relative or repo-root-relative paths in scripts so they can locate sibling repositories reliably.
- When a task targets one of the nested repositories, work in that repository directly rather than trying to manage its source through this umbrella repo.
- If you add a new tracked folder, unignore both the directory and its contents in `.gitignore`.
- Preserve the existing shared VS Code workspace file unless the task is specifically about changing the workspace composition or settings.
