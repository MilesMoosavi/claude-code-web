---
description: Present technical data, logic flows, or step-by-step code verification with structured formatting.
argument-hint: [structured|compact|mcq|debug]
allowed-tools: [Read, Grep, Bash]
---

# Trace

Use to walk through code execution, logic flows, data transformations, or multi-step comparisons with explicit formatting discipline.

## Arguments

The user invoked this with: $ARGUMENTS

Select a mode based on the task:

- **structured** (default): Multi-stage processes, complex logic, anywhere precision matters. Use bold labels on their own lines followed by a colon. Wrap all snippets in fenced code blocks with language specifiers.
- **compact**: Trivial examples, single-line comparisons, brevity-first. Use inline backticks and bullet lists. Maintain separation with clear headers or line breaks.
- **mcq**: Multiple-choice or comparative scenarios. Bold labels (e.g., **Option 1:**) on their own lines, each option's content in its own fenced code block.
- **debug**: Interactive step-through of user code. One logical step at a time — no spoilers. Show variable states and comparison results for the current line only using minimal code blocks. Do not announce bugs or final outputs unless the trace naturally reaches them.

## Rules

- Never mix modes within a single example group.
- Always specify the language for fenced code blocks.
- In **debug** mode: observe no-spoilers discipline — do not work ahead, do not anticipate the next step, do not suggest what the bug might be until the trace reaches it naturally.
- Introduce tables, horizontal rules, or unique line breaks freely if they improve scannability — as long as core logic formatting is preserved.
