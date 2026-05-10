---
description: Surgical rollback of a failed implementation to the last stable state without touching unrelated working changes.
argument-hint: [file-path ...]
allowed-tools: [Read, Edit, Bash, Glob, Grep]
---

# Surgical Revert

Use when an implementation attempt has failed, is accumulating complexity without resolving the core issue, or when three consecutive attempts at the same bug have all failed.

## Arguments

The user invoked this with: $ARGUMENTS

Optional: one or more file paths to scope the revert. If omitted, identify the affected files from conversation and git history.

## Procedure

1. **Identify the failure point**: Scan conversation history and `git log` to find the last known stable state for the affected logic. Note it explicitly (e.g., "stable as of commit abc123" or "working before the X change").

2. **Surgical revert**: Target only the failed code:
   - `git restore <file>` to revert a file to HEAD.
   - `git checkout <commit> -- <file>` to revert to a specific commit.
   - `git restore --staged <file>` then `git restore <file>` for staged-but-failed changes.
   - If git is unavailable, manually undo only the specific changed blocks.

3. **Clean up state**: Remove any temporary files, components, or store changes created solely for the failed attempt.

4. **Report**: State exactly what was reverted and why the approach was abandoned. Then propose one fresh alternative angle — or wait for user direction.

## Rules

- NEVER revert unrelated working changes. Scope is everything.
- NEVER accumulate fix-on-top-of-fix for the same bug. If three consecutive attempts fail on the same issue, this workflow is mandatory.
- After reverting, do not immediately re-attempt the same strategy. Diagnose the root cause first.
