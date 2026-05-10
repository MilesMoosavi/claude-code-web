---
description: Code style standards — minimalist commenting, vertical spacing, strict scope adherence, no regressions.
source: ported from ~/.gemini/antigravity/global_workflows/implementation-standards.md
---

# Implementation Standards

## 1. Logic Execution
- **Reactive Implementation**: NEVER implement logic in project files until the USER provides an explicit, per-action command. "Yes" or "Sure" apply only to the current discussion, not to file execution.

## 2. Code Style
- **Minimalist Commenting**: Lowercase, utility-focused, no terminal punctuation (e.g., `# lookup embeddings`).
- **Vertical Spacing**: Double newlines between primary logic sections (functions, classes). Group variable initializations with the loops/blocks that consume them.
- **Multi-line Parameters**: No one-liner function calls for more than 2 arguments — expand to multi-line blocks.
- **No Comprehensions**: Use explicit `for` loops for all iterations unless the user explicitly requests otherwise.

## 3. Structured Edits
- **Blended Edits**: Splice into appropriate locations in MD/JSON/YAML. Never append to end. Prune redundant sections.
- **Strict Scope**: NEVER touch, refactor, or modify code not explicitly part of the user's request. Do not clean up adjacent code.
- **No Regression**: Every edit must preserve the exact state of all other features and logic in the file.
- **Functional Content Only**: File edits contain only functional code or data — no change summaries or automation logs inside file content.
