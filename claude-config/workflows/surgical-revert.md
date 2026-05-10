---
description: Surgical rollback of failed implementation attempts. Three-strikes rule — if three consecutive attempts fail, roll back and rethink.
source: ported from ~/.gemini/antigravity/global_workflows/surgical-revert.md
---

# Surgical Revert

Use when a technical implementation or bug fix attempt has failed or is accumulating complexity without resolving the core issue.

## Trigger
- User says "undo", "revert", "restore", "that didn't work", "stop doing that", or similar.
- You realize the current approach is fundamentally flawed or overly complex.

## Procedure
1. **Identify the Point of Failure**: Analyze conversation history and git logs to find the last known stable state.
2. **Surgical Revert**:
   - Use `git restore <file>` or `git checkout <commit> -- <file>` to revert specific files.
   - If staged but failed: `git restore --staged <file>` then `git restore <file>`.
   - If git is unavailable, manually undo only the specific failed blocks.
   - **CAUTION**: Do NOT revert unrelated working changes.
3. **Clean Up State**: Revert any state changes in stores or context tied to the failed logic. Delete temporary files created for the failed attempt.
4. **Notify User**: Summarize exactly what was reverted and why the approach was abandoned. Propose a fresh alternative or wait for direction.

## Rule
NEVER accumulate "fix on top of fix". If **three** consecutive attempts fail on the same bug, trigger this workflow, roll back to start, and rethink strategy.
