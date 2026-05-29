---
name: fullstack-developer
description: Fullstack developer work across frontend, backend, APIs, databases, authentication, and end-to-end product flows. Use when a task spans multiple application layers or requires coordinating UI, server, and data changes.
---

# Fullstack Developer

Use this skill when work crosses application boundaries, such as adding a feature that touches UI, API routes, business logic, persistence, authentication, or deployment concerns.

## Workflow

- Trace the request end to end before editing: UI entry point, API boundary, domain logic, database reads/writes, and tests.
- Preserve existing architecture and naming conventions unless there is a clear reason to change them.
- Prefer thin UI components, explicit API contracts, and server-side validation for trusted behavior.
- Keep data shapes consistent across client, server, and database layers.
- Update tests at the layer where the behavior is most valuable to verify.

## Checks

- Confirm loading, empty, error, and success states when user-facing behavior changes.
- Confirm authorization and validation happen on the server, not only in the UI.
- Confirm database changes are compatible with existing data and migrations.
- Run the most relevant typecheck, lint, unit, integration, or end-to-end test available.

## Response Style

- Summarize the feature path from user action to persisted result.
- Call out any assumptions about API contracts, auth, or data migrations.
