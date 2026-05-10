---
description: Scan the current repo for high-value documentation and sync it to Notion via the Notion MCP. Falls back to a local roadmap file if MCP is unavailable.
argument-hint: [scan|sync|roadmap|config]
allowed-tools: [Read, Write, Glob, Grep, Bash]
---

# Notion Sync

Automated archivist: scan the repo for docs, roadmaps, and specs, then push them to Notion via the Notion MCP — or maintain a local roadmap if MCP is unavailable.

## Arguments

The user invoked this with: $ARGUMENTS

- **scan** (default): Identify candidate files and present a checklist for user approval. No writes.
- **sync**: Execute the sync for previously approved files, or re-present the checklist if no approval on record.
- **roadmap**: Update or create `.agents/project-roadmap.md` from current repo state only — no Notion API calls.
- **config**: Sync AI assistant configuration (CLAUDE.md, settings, commands, workflows) from `claude-code-web` or the local `~/.claude/` directory to a universal Notion workspace — intended as a cross-IDE handoff layer. See Config Mode below.

## Procedure

### 1. Repository Scan

Scan the repo and identify candidates across these categories:

- **Roadmaps & Logs**: `.agents/project-roadmap.md`, `.agents/session_handoff.md`, `CHANGELOG.md`
- **Architecture & Specs**: anything in `docs/`, `specs/`, `design/` — overviews, design specs, ADRs
- **Project Config**: `README.md`, `CLAUDE.md`, `package.json` (deps section only)
- **Visual Assets**: screenshots in `.agents/screenshots/`, SVGs in `public/`

If `.agents/project-roadmap.md` does not exist, create a baseline version from current repo context before proceeding.

### 2. Prepare Checklist

Present a structured checklist grouped by intended Notion hierarchy:

```
Root Page: <project-name>
├── Docs/
│   ├── Architecture
│   └── Design Spec
├── Logs/
│   ├── Session Handoff
│   └── Changelog
└── Assets/      ← note: images need public URLs to embed in Notion
```

Wait for explicit user approval on which items to sync. Do not proceed without confirmation.

### 3. Sync to Notion

On approval, use the Notion MCP tools to create or update pages:

- Use `notion-create-pages` to create new pages.
- Use `notion-update-page` to patch existing ones.
- Images cannot be uploaded via the Notion API — they must be publicly hosted (GitHub raw URL, CDN). Flag any local images: they serve as LLM context only and require manual upload by the user.

### 4. Fallback — Local Roadmap

If the Notion MCP is unavailable, errors, or the user prefers local-only:

- Write all prepared content to `.agents/project-roadmap.md` as the staging source of truth.
- Log every major milestone with a `[T+HH:MM]` relative timestamp from project start.
- Maintain two sections: **What got done** (log) and **What is next** (priority list). No rigid future time blocks.

---

## Config Mode (`/notion-sync config`)

Use this mode to sync AI assistant preferences to Notion as a universal cross-IDE handoff layer. When onboarding a new coding assistant (Cursor, Codex, Copilot, etc.), point it at the Notion config page to catch it up instantly.

### Sources (in priority order)
1. `claude-code-web/claude-config/` repo — canonical source of truth if available.
2. `~/.claude/` local directory — fallback if repo is not accessible.
3. Any other discovered `~/.<ai-tool>/` peer directories (Gemini, Copilot, etc.) — scan and include relevant global workflows.

### Notion Page Structure
```
Root Page: AI Assistant Config (Universal)
├── Global Rules (CLAUDE.md)
├── Settings (settings.json — redact any API keys)
├── Commands/
│   └── <one sub-page per slash command>
└── Workflows/
    └── <one sub-page per workflow file>
```

### Steps
1. **Discover**: Locate config files from the sources above. Scan for any `~/.<ai-tool>/global_workflows/` or equivalent dirs.
2. **Redact**: Strip any API keys, tokens, or credentials before syncing. Replace with `YOUR_KEY_HERE` placeholders.
3. **Checklist**: Present the full list of files to be synced and wait for explicit user approval.
4. **Sync**: Push each file as a Notion page under the universal config root. Use `notion-update-page` if the page already exists.
5. **Confirm**: Report which pages were created/updated and flag any that require manual attention (e.g., images, binary files).

### Rules
- NEVER sync `config.json` or any file containing real API keys without redacting first.
- Keep the Notion structure flat — Commands and Workflows as sibling pages, not deeply nested.
- This page is IDE-agnostic: write content in plain language, not Claude-specific syntax, so any assistant can consume it.

---

## Rules (all modes)

- Never copy or modify files without user confirmation from the checklist step.
- Never call Notion MCP tools unless explicitly requested or approved — API calls are rate-limited.
- On any Notion API failure, immediately pivot to the local roadmap fallback without asking.
- Keep Notion page hierarchy flat where possible — deep nesting is hard to navigate.
