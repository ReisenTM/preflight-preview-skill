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
