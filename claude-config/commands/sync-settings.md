---
description: Sync Claude Code settings between local (~/.claude) and the claude-code-web repo. Supports push (local → repo) and pull (repo → local).
argument-hint: [push|pull]
allowed-tools: [Read, Write, Bash, Glob]
---

# Sync Claude Settings

Syncs Claude Code config files between `~/.claude/` and `C:\Users\the10\OneDrive\Documents\GitHub\claude-code-web\claude-config\`.

## Files synced
- `CLAUDE.md`
- `settings.json`
- `commands/*.md` (all command files)

## Arguments

The user invoked this with: $ARGUMENTS

- **push** (default): Copy local `~/.claude/` → repo, then commit and push.
- **pull**: Copy repo → local `~/.claude/`, overwriting local files.

## Push workflow

1. Copy `~/.claude/CLAUDE.md` → repo `claude-config/CLAUDE.md`
2. Copy `~/.claude/settings.json` → repo `claude-config/settings.json`
3. Copy all `~/.claude/commands/*.md` → repo `claude-config/commands/`
4. `cd` into the repo, `git add -A claude-config/`, commit with message `chore: sync claude settings`, and push.

## Pull workflow

1. Copy repo `claude-config/CLAUDE.md` → `~/.claude/CLAUDE.md`
2. Copy repo `claude-config/settings.json` → `~/.claude/settings.json`
3. Copy all repo `claude-config/commands/*.md` → `~/.claude/commands/`

## Rules
- Always confirm with the user before overwriting files in either direction.
- After push, confirm the git push succeeded and report which files changed.
- After pull, list which files were updated locally.
