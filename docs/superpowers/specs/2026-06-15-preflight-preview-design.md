# Preflight Preview Design

## Goal

Create a Codex Skill named `preflight-preview` that forces a preview step before implementation for new projects and larger development tasks.

The skill should make future Codex instances produce a realistic preview artifact before coding:

- For web development: a static demo HTML using mock data.
- For backend or tool development: an architecture diagram plus a mock-data demo when useful.
- For larger backend or tool efforts: the architecture diagram alone is acceptable when a demo would add noise or false precision.

## Scope

This skill applies to:

- New projects.
- Larger features.
- Significant UI changes.
- Behavior changes that materially affect user-visible flows.
- Backend or tool work with meaningful architectural impact.
- Requests where the user explicitly wants to preview the concept before implementation.

This skill does not apply by default to:

- Small bug fixes.
- Narrow refactors.
- Pure explanation tasks.
- Localized maintenance edits.
- Minor configuration changes.

It may still apply to smaller tasks if the user explicitly asks for a preview, demo, mockup, or architecture-first workflow.

## Core Behavior

### Web Development

Before implementation, produce a previewable demo HTML that:

- Uses mock data.
- Reflects the requested project's main features.
- Matches the intended art direction, tone, and interaction model.
- Avoids generic wireframes that do not represent the requested product.

If the project already has a design system or established UI language, the demo should align with it. If not, the demo should establish a clear visual direction rather than defaulting to a bland placeholder layout.

### Backend And Tool Development

Before implementation, prefer producing:

- An architecture diagram.
- A mock-data demo.

The mock-data demo may take forms such as:

- CLI sample output.
- Example request/response payloads.
- Pseudo-run logs.
- Minimal HTML control surface.
- JSON fixtures that demonstrate the core flow.

For sufficiently large or architecture-heavy work, the skill may produce only the architecture diagram first. In that case, it must explain briefly why a demo is being skipped at that stage.

## Preview Gate

The skill should instruct Codex not to begin full implementation until the preview artifact has been shown to the user and the user has had a chance to respond.

If the user explicitly chooses to skip preview and proceed directly to implementation, Codex may continue, but should state that the preview step was intentionally bypassed by user direction.

## Quality Bar

The skill should make Codex verify that the preview:

- Uses explicit mock data rather than empty placeholders.
- Covers the main happy-path functionality.
- Represents the requested style and product direction.
- Clarifies implementation boundaries rather than pretending to be final production code.

## Deliverable Shape

Use a lightweight skill folder with a single `SKILL.md`.

Do not add templates, scripts, or assets in the initial version unless a concrete future need appears. The skill is primarily a behavioral gate and decision framework, not a code scaffold.

## Triggering Strategy

Use a balanced triggering strategy:

- Default to using the skill for new builds and meaningful feature work.
- Avoid triggering for minor edits unless the request explicitly asks for a preview-first workflow.

The frontmatter description should bias toward these larger-scope triggers so the skill is useful without becoming noisy.

## Risks And Mitigations

### Risk: Over-triggering

If the skill activates on every small change, it will slow routine work and be bypassed mentally.

Mitigation:

- Keep the trigger language focused on new work, substantial changes, or explicit preview requests.

### Risk: Low-value previews

If Codex produces generic wireframes or mock data with no connection to the request, the preview step becomes ceremony.

Mitigation:

- State that demo style and core functionality must resemble the requested project.
- Require meaningful mock data and primary-flow coverage.

### Risk: Over-prescriptive outputs

If the skill forces one demo format for every backend/tool task, it will fit some tasks poorly.

Mitigation:

- Allow architecture diagram plus any suitable mock-data demo format.
- Allow architecture-only output for sufficiently large work.

## Implementation Notes

The `SKILL.md` should stay concise and focus on:

- Trigger conditions.
- When not to use the skill.
- Required preview artifact by project type.
- Approval gate before implementation.
- Conditions for skipping the backend/tool demo.
- A short verification checklist.
