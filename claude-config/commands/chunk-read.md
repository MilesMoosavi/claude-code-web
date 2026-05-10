---
description: Internalize a long or complex file by reading it in digestible chunks rather than all at once.
argument-hint: <file-path> [chunk-size]
allowed-tools: [Read, Glob, Grep]
---

# Chunked Reading

Use when a file is too large to internalize in one pass, or when you need to reason carefully about each section before moving on.

## Arguments

The user invoked this with: $ARGUMENTS

- **file-path** (required): The target file — PDF, Markdown, source code, JSON, etc.
- **chunk-size** (optional): How much to read per iteration. Defaults to one logical section (heading boundary, class definition, or ~50 lines). Override with a number (e.g., `20` for 20 lines) or a descriptor (e.g., `function`, `section`).

## Procedure

1. **Orient**: Read the first 20 lines to understand structure (headings, class layout, section markers).
2. **Chunk Loop**: For each chunk:
   - Read exactly one chunk using the `offset` and `limit` parameters of the Read tool.
   - Synthesize the core concepts from that chunk in 2-3 sentences.
   - Flag anything that needs follow-up or contradicts prior chunks.
   - If a task is immediately actionable from this chunk, execute it before moving on.
3. **Continuity Check**: After the final chunk, produce a one-paragraph summary of the whole document for logical continuity.

## Rules

- Never read ahead. One chunk at a time.
- If the chunk contains a definition that a later section will reference, note it explicitly so you don't lose it.
- For source code: chunk at function or class boundaries, not arbitrary line counts.
- For JSON/YAML: chunk at top-level keys.
