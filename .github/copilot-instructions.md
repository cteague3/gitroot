# Copilot Instructions

## High-level architecture

This umbrella repository houses shared configuration and cross-repo automation. The folders underneath it are mostly independent Git repositories; treat them as sibling working trees, not as source directories inside this repo.

The shared surfaces in this repo are intentionally narrow:

- `.github\` for Copilot guidance and other repo-level metadata
- `scripts\` for automation that works across the sibling repositories
- `ChipsRepos.code-workspace` for the shared VS Code workspace
- any future root-level config that is explicitly unignored in `.gitignore`

The repository uses an ignore-by-default model. New files stay ignored until `.gitignore` explicitly whitelists them, so adding a shared config surface usually requires updating `.gitignore` in the same change.

## Nested repositories

The umbrella includes several independent Git repositories as siblings:
- **bggstuff** - Board game related project
- **ChipsPlayGround** - Experimentation/sandbox repo
- **cthulhucli** - Python-based CLI (uses Makefile, pyproject.toml)
- **geekrush** - TBD
- **gitignore** - Git-related utilities
- **GoWork** - Go language projects
- **RulesEngine** - C# project (RulesEngine.sln, uses .NET)
- **xgit** - C# project (xgit.sln, uses .NET)

When working on source code, enter the nested repository directory and treat it as a standalone project. Each repo has its own build, test, and lint tools.

## Workspace setup

Open `ChipsRepos.code-workspace` in VS Code to load the currently active repositories as a multi-folder workspace. This is the recommended way to navigate across repos.

## Commands

There is no umbrella-level build, test, or lint toolchain.

- Validate repository visibility and the whitelist: `git status --short --ignored` from the umbrella root
- To work on a nested repo, `cd` into it and use its native build/test commands (e.g., `make`, `npm`, `dotnet`, `python`)
- If you change a script under `scripts\`, run that script directly with its native interpreter or shell

## Key conventions

- Keep changes focused on shared config, workspace metadata, and cross-repo automation; do not fold nested repository source into this repo
- Use relative paths from the umbrella root in scripts so they can locate sibling repositories consistently
- Work inside the target sibling repository when a task is about that repo's source code
- If you add a new tracked folder, unignore both the directory and its contents in `.gitignore`
- Preserve `ChipsRepos.code-workspace` unless the task is specifically about changing the shared workspace
- When transitioning between umbrella work and nested repo work, verify you're in the correct directory before making changes

## Common patterns

- **Python repos** use `Makefile` and `pyproject.toml` (e.g., cthulhucli)
- **.NET projects** use `.sln` files and `dotnet` CLI (e.g., RulesEngine, xgit)
- **Path resolution** in scripts should use umbrella-root-relative paths for consistency

## Troubleshooting

- **File not tracked?** Check `.gitignore` — it uses ignore-by-default. New umbrella files must be explicitly whitelisted.
- **Path errors in scripts?** Ensure scripts use umbrella-root-relative paths, not assume the current working directory.
- **Nested repo changes being ignored?** You're likely in the umbrella repo. `cd` into the nested repo and stage changes there.
