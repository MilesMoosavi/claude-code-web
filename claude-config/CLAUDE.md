\# Global Claude Code Rules



\## Response Style

\- Always state which model you are running (e.g., "claude-sonnet-4-6") at the start of any response where the model is ambiguous or set to default/auto.

\- No emojis unless required for UI implementation.

\- No preamble, filler, or congratulatory language.

\- No meta-commentary ("Here's what I think...", "Great question!", etc.).

\- Respond directly to the content. Keep answers brief and high-density.

\- Avoid generic sentence starters ("This suggests that...", "In summary...").

\- In drafted/published/pushed content (code, docs, submissions): preserve double dashes (`--`) if the user's original draft used them, but do not introduce them. Use em dashes (—) only if the user's draft used them. Claude's own chat responses may use em dashes freely.

\- Do not repeat observations in different words.

\- No dollar-sign LaTeX in Claude's own chat responses only. Any file Claude writes (markdown, .tex, etc.) may use inline LaTeX freely -- it renders fine in the VSCode editor and Overleaf. Backticks also fine in chat.



\## Code Style

\- Prefer if/else over ternaries for readability.

\- Comment liberally — especially for frontend/React code where Tailwind class strings, animation logic, or component behavior isn't self-evident. When in doubt, add a comment.

\- Modularize aggressively. When a file is getting long, proactively suggest breaking it into components, hooks, interfaces, subclasses, or helper modules. This applies to all languages, not just React. When suggesting a split, include a proposed directory tree of the new file structure for review before proceeding.

\- Flag long files unprompted — don't wait for the user to notice.



\## File Paths

\- When the user references any local repo or project by name (e.g. "look at cmsc250-homeworks"), assume it lives at `C:\Users\the10\OneDrive\Documents\GitHub\<repo-name>` unless a different path is explicitly given. Do not ask for the path.



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

