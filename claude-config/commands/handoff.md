---
description: Preserve session state across context boundaries to kill hallucinations and continue seamlessly. Detects whether the next session should resume a specific task or simply stand by for instructions.
argument-hint: [resume|export|continue]
allowed-tools: [Read, Write, Glob, Grep, Bash]
---

# Session Handoff

Use when the context window is getting long enough that hallucinations are creeping in, or when explicitly switching to a fresh session. The goal is maximum continuity with minimum re-orientation cost.

## Arguments

The user invoked this with: $ARGUMENTS

- **resume** (default): Write state to `.agents/session_handoff.md` in the current project root. Next session reads it and waits for further instructions.
- **continue**: Same as resume, but signals to the next session that a specific task is mid-flight and should be picked up immediately without waiting.
- **export**: Output a structured prompt as a copyable code block for pasting into another tool (Gemini, Cursor, Copilot, Codex, etc.).

The user may also pass a **session title** as a free-form string (e.g., `/handoff continue "CMSC451 Final Exam Prep (pt. 3)"`). If provided, use it verbatim. If not provided, generate one following the Title Generation rules below.

## Mode Detection

Before writing the handoff, infer the user's intent:

- If the user says "continue [task]", "pick up where we left off", "keep going", or references a specific in-progress task → use **continue** mode.
- If the user says "start fresh", "new session", "clean slate", or doesn't reference a specific next task → use **resume** mode (stand-by on arrival).
- If ambiguous, ask: "Should the next session pick up a specific task, or stand by for your instructions?"

## Title Generation

If the user did not specify a title, generate one that reflects the **expected scope of the next session**, not just the immediate trigger task.

Rules:
- Think about what the user will likely work through in the next session, not just what they're doing right now.
- If this is part of an ongoing series (e.g. study prep, a multi-session project), increment a part number (e.g. `pt. 3`).
- Format: `<Project/Topic> (<qualifier>)` — e.g. `CMSC451 Final Exam Prep (pt. 3)`, `Semantix Refactor (auth flow)`, `claude-code-web Setup (cont.)`.
- Lean broad rather than narrow. A session titled after Q4(a) that ends up covering Q4-Q6 is worse than one titled for the exam prep arc.
- Output the suggested title at the top of the handoff and in the chat so the user can confirm or override it before starting the new session.

## Handoff Structure

Produce all of the following sections:

**Suggested Title**: The name for the next conversation. User-specified if provided, otherwise generated per Title Generation rules above.

**Timestamp**: ISO-8601 timestamp.

**Session Mode**: `continue` or `stand-by`. If `continue`, state exactly what task to resume immediately. If `stand-by`, instruct the next session to read this file, acknowledge it, then wait.

**Current Objective**: The core goal at time of handoff, and any active blockers.

**Active Files**: Exact paths currently in scope — code files, notes, configs, exams, etc.

**Session Context**: Key facts established this session that won't be in the next session's memory — decisions made, answers confirmed, approaches ruled out. Be specific; this is the main anti-hallucination payload.

**Environmental State**: Any running servers, active venvs, background processes, or open tools.

**Last Working State**: The most recent thing confirmed correct before this handoff.

**Failed Approaches**: Every strategy tried and why it failed. Flag explicitly if stuck in a logic loop.

**Captured User Intent**: Verbatim text of the user's most recent substantive request. Absolute priority for the next session.

**Recommendation**: Specific next steps, including targeted file paths or grep patterns. Avoid generic re-analysis.

**Workflow Delta**: Any new or modified global workflows, commands, or rules activated this session that the next session needs to know about.

**Primer**: A short (3-5 sentence) behavioral primer the next session should apply immediately — tone, mode, constraints. E.g., if this session was Socratic study mode, say so explicitly so the next session doesn't revert to default behavior.

## Rules

- **resume** mode: write to `.agents/session_handoff.md`, creating `.agents/` if it doesn't exist.
- **continue** mode: same file, but prepend `ACTION REQUIRED: resume [task] immediately after reading.`
- **export** mode: output as a clean fenced code block for copy-paste.
- Always instruct the next session to read `~/.claude/CLAUDE.md` and check `~/.claude/commands/` on arrival.
- Do not paraphrase Captured User Intent — quote verbatim.
- The handoff is a makeshift fix, not a perfect memory transfer. Flag anything the user may still need to re-confirm in the new session.
