# Preflight Preview Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Create a lightweight Codex Skill named `preflight-preview`.

**Architecture:** The repository will contain the confirmed design spec, this implementation plan, and a single skill folder `preflight-preview/` with `SKILL.md`. The skill is a behavioral gate: it tells Codex when to produce web demos, backend/tool architecture diagrams, and mock-data previews before implementation.

**Tech Stack:** Markdown skill specification, YAML frontmatter, `quick_validate.py` from the local `skill-creator` system skill.

---

### Task 1: Create The Skill Document

**Files:**
- Create: `preflight-preview/SKILL.md`
- Read: `docs/superpowers/specs/2026-06-15-preflight-preview-design.md`

- [ ] **Step 1: Initialize the skill directory**

Run:

```bash
python3 /Users/c.c/.codex/skills/.system/skill-creator/scripts/init_skill.py preflight-preview --path . --interface 'display_name=Preflight Preview' --interface 'short_description=Preview demos and diagrams before implementation' --interface 'default_prompt=Use $preflight-preview before building a substantial web, backend, or tool feature.'
```

Expected: directory `preflight-preview/` exists with generated skill files.

- [ ] **Step 2: Write the complete skill**

Create `preflight-preview/SKILL.md` with this content:

```markdown
---
name: preflight-preview
description: Use when starting new web, backend, or tool development; implementing larger features; making significant UI or behavior changes; or when the user asks for a preview, demo, mockup, prototype, architecture diagram, or mock-data flow before implementation.
---

# Preflight Preview

## Principle

Before substantial implementation, give the user a concrete preview artifact that represents the intended product or system. Use this for new builds and meaningful feature work; do not slow down small fixes unless the user asks for preview-first work.

## First Decision

Use this skill for:

- New projects or greenfield builds.
- Larger features or behavior changes.
- Significant UI, UX, workflow, or architecture changes.
- Backend or tool work with meaningful module, data-flow, or integration design.
- Requests that mention preview, demo, mockup, prototype, architecture diagram, simulated flow, or mock data.

Do not use this skill by default for:

- Small bug fixes.
- Narrow refactors.
- Pure explanation or code review tasks.
- Localized maintenance edits.
- Minor configuration changes.

If a small task still affects user-visible experience or system shape, use judgment and prefer a lightweight preview.

## Web Development

Before implementation, produce a previewable demo HTML.

The demo must:

- Use realistic mock data.
- Represent the requested product's main features and happy path.
- Match the requested or inferred art direction, tone, visual hierarchy, and interaction model.
- Be specific to the user's project, not a generic wireframe.
- Be independent from production code unless the user asks to preserve it.

If an existing app, design system, or brand language is present, inspect it and align the demo with that style. If no style exists, establish a clear visual direction appropriate to the product instead of using bland defaults.

Show or link the demo for user review before coding the actual feature.

## Backend And Tool Development

Before implementation, prefer producing both:

- An architecture diagram.
- A mock-data demo.

The architecture diagram should show:

- Main modules or services.
- Data flow and control flow.
- External dependencies.
- Persistence or state boundaries.
- Key failure paths and recovery behavior.

The mock-data demo can be any format that makes the intended behavior concrete:

- CLI sample session.
- Example API requests and responses.
- JSON input and output fixtures.
- Pseudo-run logs.
- Minimal HTML control panel.
- Script transcript using fake data.

For large, ambiguous, or architecture-heavy work, produce only the architecture diagram first when a demo would create false precision or distract from structural decisions. State briefly why the demo is being skipped for now.

## Preview Gate

Do not begin full implementation until the preview artifact has been shown and the user has had a chance to respond.

If the user explicitly says to skip the preview and implement directly, continue, but state that the preview gate is being bypassed by user direction.

## Quality Checklist

Before presenting the preview, verify:

- Mock data is explicit and meaningful.
- The main happy path is visible.
- The artifact reflects the requested style, product direction, or system purpose.
- Limitations are clear, so the preview is not mistaken for production-ready implementation.
- The next implementation boundary is obvious.
```

- [ ] **Step 3: Confirm the file exists**

Run: `test -f preflight-preview/SKILL.md && echo present`

Expected: `present`

- [ ] **Step 4: Remove generated optional metadata file**

Use `apply_patch` to delete `preflight-preview/agents/openai.yaml`.

Expected: the only tracked file in the skill folder is `SKILL.md`, matching the lightweight single-file design.

### Task 2: Validate The Skill

**Files:**
- Read: `preflight-preview/SKILL.md`
- Tool: `/Users/c.c/.codex/skills/.system/skill-creator/scripts/quick_validate.py`

- [ ] **Step 1: Run skill validation**

Run: `/Users/c.c/.codex/skills/.system/skill-creator/scripts/quick_validate.py preflight-preview`

Expected: validation passes with no required-field or naming errors.

- [ ] **Step 2: Inspect frontmatter**

Run: `sed -n '1,16p' preflight-preview/SKILL.md`

Expected: frontmatter contains only `name` and `description`, and `name` is `preflight-preview`.

### Task 3: Commit The Work

**Files:**
- Commit: `docs/superpowers/specs/2026-06-15-preflight-preview-design.md`
- Commit: `docs/superpowers/plans/2026-06-15-preflight-preview.md`
- Commit: `preflight-preview/SKILL.md`

- [ ] **Step 1: Review changed files**

Run: `git status --short`

Expected: the design spec, implementation plan, and skill document are untracked or modified.

- [ ] **Step 2: Commit files**

Run:

```bash
git add docs/superpowers/specs/2026-06-15-preflight-preview-design.md docs/superpowers/plans/2026-06-15-preflight-preview.md preflight-preview/SKILL.md
git commit -m "feat: add preflight preview skill"
```

Expected: commit succeeds.
