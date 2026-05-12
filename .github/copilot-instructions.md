# Copilot Instructions

## High-level architecture

`D:\code` is an umbrella repository for shared configuration and cross-repo automation. The folders underneath it are mostly independent Git repositories; treat them as sibling working trees, not as source directories inside this repo.

The shared surfaces in this repo are intentionally narrow:

- `.github\` for Copilot guidance and other repo-level metadata
- `scripts\` for automation that works across the sibling repositories
- `ChipsRepos.code-workspace` for the shared VS Code workspace
- any future root-level config that is explicitly unignored in `.gitignore`

The repository uses an ignore-by-default model. New files stay ignored until `.gitignore` explicitly whitelists them, so adding a shared config surface usually requires updating `.gitignore` in the same change.

## Commands

There is no umbrella-level build, test, or lint toolchain yet.

- Validate repository visibility and the whitelist with `git status --short --ignored` from `D:\code`.
- There is no standard single-test command at the umbrella level because no test framework is configured here.
- If you change a script under `scripts\`, run that script directly with its native interpreter or shell instead of relying on a repo-wide wrapper.

## Key conventions

- Keep changes focused on shared config, workspace metadata, and cross-repo automation; do not fold nested repository source into this repo.
- Use root-relative or `D:\code`-relative paths in scripts so they can locate sibling repositories consistently.
- Work inside the target sibling repository when a task is about that repo’s source code.
- If you add a new tracked folder, unignore both the directory and its contents in `.gitignore`.
- Preserve `ChipsRepos.code-workspace` unless the task is specifically about changing the shared workspace.
