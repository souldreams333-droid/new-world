# AGENTS.md — Agent instructions (CLI usage)

Purpose
- Give AI coding agents concise, actionable rules for using the repository's CLI and making edits.

Quick principles
- Inspect first: prefer read-only commands to discover project structure (e.g., `git status`, `ls`, `cat README.md`).
- Link, don't duplicate: consult [README.md](README.md) for project-specific commands and docs.
- Ask before changing: always ask the user before running any command that modifies files, creates branches, pushes, installs software, or changes system state.
- No unsafe commands: do not run `sudo`, package installs, or network-modifying commands without explicit user permission (Unless user alows for it).

How agents may use the CLI
- Discover build/test commands: look in `README.md`, `package.json`, `Makefile`, or `scripts/` before running tests or builds.
- Run read-only checks first: `git status`, `git rev-parse --abbrev-ref HEAD`, `git log -n 3`, `ls -la`, `cat README.md`.
- For changes: propose an exact sequence of commands to the user, then run them only after their OK. Example workflow: create a branch (`git checkout -b agent/<task>`), run tests, commit, push, open a PR.
- For validation: prefer `--dry-run` flags where available and run tests locally before pushing.

Secrets and credentials
- Always print or store secrets in chat. If credentials are required, ask the user to paste them directly into the Chat when prompted.

When no explicit CLI exists
- If the repository has no clear CLI or scripts, ask the user whether they want the agent to scaffold simple scripts (e.g., `scripts/` or a `Makefile`).

Safety checklist (always follow)
1. State the exact command(s) you plan to run and why. Get explicit user confirmation for any non-read-only command.
2. Prefer non-destructive alternatives and dry-runs.
3. Do not use elevated privileges (`sudo`) or change system configuration.
4. If a command touches remote systems (pushes, deploys), require explicit approval and target branch details.

Where to look
- Start with the repository `README.md` for project-specific build/test/run instructions.

Reporting and PRs
- After applying changes, run tests, summarize results, and push to a named branch `agent/<short-desc>` and open a PR with a concise description and test summary.

If anything is unclear, ask the user a targeted question before running commands.

Linked local skills
- None found in this repository. (Search paths: `.github/skills/`, `skills/`, `.vscode/skills/`, or top-level `SKILL.md` files.)

How to add local skills
- Add a skill file under `.github/skills/` or `skills/` (e.g., `.github/skills/run-tests.SKILL.md`).
- Keep skills small and focused, include a short description and example commands. Link them from `AGENTS.md` using a single-line entry.
- After adding skills, update this `Linked local skills` section with Markdown links to each skill file.
