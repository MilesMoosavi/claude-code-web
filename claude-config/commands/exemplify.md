---
description: Present high-fidelity technical examples, logic flows, or I/O demonstrations with structured formatting and at least two distinct examples.
argument-hint: [io|state|logic]
allowed-tools: [Read, Grep, Bash]
---

# Exemplify

Use to provide concrete technical demonstrations, input/output traces, or logic-state walkthroughs. Always provide at least two distinct examples to help the user identify patterns.

## Arguments

The user invoked this with: $ARGUMENTS

Select a mode based on the task:

- **io** (default): Show how a specific input transforms into an output. Use bold **Input:** and **Output:** labels. Wrap all content in fenced code blocks with language specifiers.
- **state**: Show how variables or object attributes change over time. Wrap all attribute/value pairs in a single fenced code block. Use comments to explain complex states.
- **logic**: Explain complex control flows or decision trees. Break into numbered steps. Use minimal code snippets per step wrapped in fenced blocks.

## Rules

- **At least 2 examples per invocation** — including at least one counterexample when explaining why a condition is necessary.
- **No truncation** — never use `...` to shorten arrays, matrices, or lists. Show all values.
- **Mandatory syntax highlighting** — every piece of technical data must be in a fenced code block with a language specifier (`text`, `python`, `json`, etc.).
- **Verbatim accuracy** — if referencing existing code or algorithms, values must be exact, not approximated.
- **Standard punctuation** — colons and dashes are fine inside example blocks even if suppressed elsewhere.
- Never mix modes within a single example group.
- For trees or ASCII diagrams, precede the code block with at least two newlines and a descriptive label line to preserve indentation.
