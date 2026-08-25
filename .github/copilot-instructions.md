# Copilot Instructions

## High-level architecture

This is an umbrella repository for shared development configuration, IDE/workspace metadata, and cross-repo automation. The child directories are independent Git repositories, not source directories of this repository; each has its own history, working tree, build, and local Copilot instructions.

The root repository intentionally tracks only shared surfaces:

- `.github\` for Copilot guidance and repository metadata
- `scripts\` for automation that works across the sibling repositories
- `ChipsRepos.code-workspace` and `.idea\` for the shared workspace
- `README.md`, `.gitignore`, and explicitly whitelisted shared configuration

The root uses an ignore-by-default model. New shared files remain ignored until `.gitignore` whitelists both the directory and its contents, when applicable.

## Nested repositories

The workspace currently includes independent repositories such as `bggstuff`, `ChipsPlayGround`, `cthulhucli`, `devcontainer.images`, `devcontainer.spec`, `geekrush`, `gitignore`, `GoWork`, `RulesEngine`, and `xgit`.

Before changing project source, change into the target repository and confirm the boundary with `git rev-parse --show-toplevel`. Read that repository's `.github\copilot-instructions.md`, `README.md`, and `CONTRIBUTING.md` when present. In particular, `cthulhucli` is a Python/Make project, `RulesEngine` and `xgit` are .NET solutions, `GoWork` contains Go modules, and `devcontainer.images` builds Docker development-container images with Yarn/Node tooling.

## Workspace setup

Open `ChipsRepos.code-workspace` in VS Code to load the active repositories as a multi-folder workspace. JetBrains mappings in `.idea\` also treat the child repositories as separate Git roots.

## Build, test, and lint

There is no umbrella-level application build, test, or lint toolchain. Do not run a nested repository's command from `D:\code`; run it from that repository's root using its own documentation and instruction file.

Root checks:

```powershell
git status --short --ignored
git ls-files
```

The first command exposes ignored files and helps diagnose the whitelist; the second confirms what belongs to the umbrella repository. There is no root-level single-test command. For nested work, use the native runner and its single-test selector (for example, `dotnet test <project> --filter FullyQualifiedName~<test>` or the repository's documented Python/Go/Node selector).

If a shared script is added under `scripts\`, run it directly with its native interpreter from the umbrella root and keep its paths relative to that root.

## Key conventions

- Keep changes focused on shared config, workspace metadata, and cross-repo automation; do not fold nested repository source into this repo
- Resolve sibling paths relative to the umbrella root in shared scripts; do not depend on the caller's current directory
- Keep commits and status checks scoped to the correct Git root; a nested repository's changes do not belong in the umbrella commit
- If a new shared folder is tracked, add both `!path/` and `!path/**` entries to `.gitignore`
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
