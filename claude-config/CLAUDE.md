\# Global Claude Code Rules



\## Response Style

\- Always state which model you are running (e.g., "claude-sonnet-4-6") at the start of any response where the model is ambiguous or set to default/auto.

\- No emojis unless required for UI implementation.

\- No preamble, filler, or congratulatory language.

\- No meta-commentary ("Here's what I think...", "Great question!", etc.).

\- Respond directly to the content. Keep answers brief and high-density.

\- Avoid generic sentence starters ("This suggests that...", "In summary...").

\- Avoid em dashes in any drafted, published, or pushed content (code, docs, submissions). This does not apply to Claude's own chat responses.

\- Do not repeat observations in different words.

\- Never use inline LaTeX dollar-sign notation (e.g. $O(n)$, $\log n$) in chat responses or markdown files. The Claude Code VSCode extension sidebar does not render it. Use plain text equivalents instead (e.g. O(n log n), O(log n)). This applies until further notice.



\## Code Style

\- Prefer if/else over ternaries for readability.

\- Comment liberally — especially for frontend/React code where Tailwind class strings, animation logic, or component behavior isn't self-evident. When in doubt, add a comment.

\- Modularize aggressively. When a file is getting long, proactively suggest breaking it into components, hooks, interfaces, subclasses, or helper modules. This applies to all languages, not just React. When suggesting a split, include a proposed directory tree of the new file structure for review before proceeding.

\- Flag long files unprompted — don't wait for the user to notice.



\## Editing Standards

\- When editing structured text (Markdown, JSON, YAML), splice into the appropriate location — do not append to the end.

\- Blend edits into surrounding structure so the document reads coherently.



\## Git Commit Messages

\- Format: `<type>: <summary>` (e.g., `feat: update branding and refactor components`)

\- Follow with bullet points describing specific file and code changes.

\- Be specific about what was changed, added, or deleted.



\## Peer AI Workflow Integration

\- At the start of any session, scan for peer AI tool directories under `~/` (e.g., `~/.gemini/`, `~/.copilot/`, `~/.codex/`, or any `~/.<tool>/` pattern that exists).

\- Check those directories for globally useful skills, workflows, scripts, or commands (e.g., in subdirs like `global_workflows/`, `workflows/`, `prompts/`, `scripts/`).

\- If any are relevant to the current session or generally useful across projects, port or apply them before proceeding. Do not limit this check to the current task -- treat it as a general capability import.

\- Do not hardcode specific tool names -- discover what exists at runtime.



\## Task Handoffs

When writing a handoff prompt for another tool (Cursor, Gemini, Copilot, etc.):

\- \*\*Objective\*\*: Core goal and current blockers.

\- \*\*Context \& Key Files\*\*: Relevant paths and specs.

\- \*\*Failed Approaches\*\*: What was tried and why it failed. Acknowledge if stuck in a loop.

\- \*\*Recommendation\*\*: A specific new angle that avoids previous mistakes.

\- \*\*Project Rule Sync\*\*: Remind the next tool to check `\~/.gemini/GEMINI.md` and the project `CLAUDE.md` for current constraints.

