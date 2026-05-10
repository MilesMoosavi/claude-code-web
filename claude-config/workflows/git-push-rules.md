---
description: Explicit per-action git permission policy — never commit, push, or merge without user confirmation.
source: ported from ~/.gemini/antigravity/global_workflows/git-push-rules.md
---

# Git & Push Rules

## 1. Commit Standards
- **Format**: `<type>: <summary>`. Use backticks for symbols.
- **Content**: Use specific, bulleted technical changes; do not summarize.

## 2. Permissions
- **EXTREME PRIORITY**: NEVER commit, push, or merge without explicit, per-action permission.
- **NO AUTO-COMMITTING**: NEVER execute `git commit` or any git mutation as part of a task unless the USER explicitly says "commit this now" for that specific change.
- **Scope**: "Sure" or "Yes" do not apply to Git actions unless Git is explicitly mentioned.

## 3. Branch Synchronization
- **IDE Status**: If a task requires working on a different branch, ALWAYS confirm with the USER that they have switched their IDE branch indicator before proceeding with any file modifications.
