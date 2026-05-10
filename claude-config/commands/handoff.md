---
description: Preserve task state across context boundaries — write a session handoff file or export a structured prompt for another agent.
argument-hint: [resume|export]
allowed-tools: [Read, Write, Glob, Grep, Bash]
---

# Session Handoff

Preserve task state when the context window is full or you need to hand off to another model/tool.

## Mode Selection

The user invoked this with: $ARGUMENTS

- **resume** (default): Write state to `.agents/session_handoff.md` in the current project root for same-model continuation.
- **export**: Output a structured prompt to the chat for the user to copy into another tool (Gemini, Cursor, Copilot, etc.).

## Handoff Structure

Produce all of the following sections:

**Timestamp**: ISO-8601 timestamp.

**Current Objective**: The core goal right now and any active blockers.

**Active Files**: Exact paths currently in scope — code files, specs, configs.

**Environmental State**: Any running servers, active venvs, background processes.

**Last Working State**: The most recent thing that worked correctly before the current issue.

**Failed Approaches**: Every strategy tried and why it failed. Explicitly flag if stuck in a logic loop.

**Captured User Intent**: Verbatim text of the user's most recent request. This is the absolute priority for the next session.

**Recommendation**: Specific next steps for the next model, including a targeted grep path or directory focus to avoid surface-level re-analysis.

**Workflow Delta**: Any new or modified global workflows active in this session.

## Rules

- For **resume** mode: write the handoff to `.agents/session_handoff.md`, creating the `.agents/` directory if it doesn't exist.
- For **export** mode: output the handoff as a clean code block the user can paste elsewhere.
- Always remind the next agent to sync platform rules against `~/.claude/CLAUDE.md` (or `~/.gemini/GEMINI.md` if handing off to Gemini).
- Record the exact user message that triggered this handoff under Captured User Intent — do not paraphrase.
