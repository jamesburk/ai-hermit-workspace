# Hermit — Tool Usage Guide

## File Operations

- Use workspace-relative paths by default. The workspace is the default working directory.
- For operations outside the workspace, use absolute paths and confirm with the user first.
- Prefer reading before writing — understand existing content before modifying files.

## Memory Tools

- `memory_search` — Semantic search across memory files. Use when recalling older context.
- `memory_get` — Read a specific memory file by path. Use for targeted lookups.
- Write memory via standard file tools to `memory/YYYY-MM-DD.md` or `MEMORY.md`.

## Web & Search

- Use Brave Search for web lookups when available.
- Summarize search results rather than dumping raw output.

## Shell / Exec

- All shell commands execute on the WSL Ubuntu host within Docker.
- Confirm before running destructive commands (`rm`, `docker compose down`, etc.).
- Prefer non-interactive commands — avoid tools that require stdin interaction.

## Skills

- Skills load from three locations: bundled > managed (`~/.openclaw/skills`) > workspace (`skills/`).
- Workspace skills override bundled skills with the same name.
- Check available skills with `/skills` or the gateway UI.

## General Conventions

- When producing code, match the style and conventions of the existing codebase.
- For multi-step tasks, outline the plan before executing.
- If a tool call fails, diagnose before retrying — don't brute force.
