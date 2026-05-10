---
description: Deep-dive inspection of an unfamiliar codebase — architecture, components, ecosystem, and implementation style.
argument-hint: <repo-path-or-url>
allowed-tools: [Read, Glob, Grep, Bash]
---

# Inspect Codebase

Use when onboarding to an unfamiliar repository or handing off a codebase analysis to another agent.

## Arguments

The user invoked this with: $ARGUMENTS

Target: the repo path (local) or URL to inspect.

## Inspection Procedure

**1. Ecosystem scan**
- Identify primary language(s) and framework(s).
- Read `package.json`, `requirements.txt`, `Cargo.toml`, `pyproject.toml`, `docker-compose.yml` — whatever is present — and list major dependencies.
- Locate README, deployed links, or production endpoints.

**2. Architecture pattern**
- Identify the architectural pattern: Next.js app, FastAPI backend, data pipeline, monorepo, etc.
- Find the main entry points.

**3. Domain-specific discovery**

- **Frontend/Fullstack**: Name all major sections and components. Identify UI libraries, design tokens (colors, typography), global state management, and assets. Explicitly grep for micro-interactions and animations (Framer Motion, CSS transforms, parallax).
- **Backend/API**: Analyze routing, middleware, database schemas (ORMs, migrations), auth mechanisms, and external integrations.
- **Data Science/Scripts**: Identify data processing pipelines, model training logic, visualization strategies, and main entry points.

**4. Implicit assumptions and blindspots**
- Do not stop at structural summaries. If a feature is mentioned, grep for its exact implementation.
- Check `docs/`, `figma` links, or architecture diagrams if present.
- Review `.cursorrules`, `CLAUDE.md`, or equivalent project rule files and note any constraints.

**5. Handoff output**
Produce a structured prompt the user can hand to another agent, covering:
- Objective and project context
- Ecosystem summary (languages, deps, entry points)
- Key implementation details found (not just file names)
- A targeted grep path or directory focus to skip surface-level re-analysis
- Any active project rules to sync

## Rules

- Never rely on generic structural summaries alone — always grep for specific implementation details.
- If the repo is remote, note that the next agent will need local access or a clone.
