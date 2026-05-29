---
name: backend
description: Backend services, APIs, server logic, authentication, authorization, validation, queues, jobs, and integrations. Use when editing routes, controllers, services, workers, server config, or external API integrations.
---

# Backend

Use this skill for server-side work: APIs, service logic, auth, validation, jobs, queues, integrations, caching, and operational behavior.

## Workflow

- Identify the request boundary, trust boundary, data model, side effects, and error handling before editing.
- Validate inputs at the server boundary and enforce authorization close to the protected resource.
- Keep API responses consistent with existing contracts.
- Prefer explicit errors and structured logging where the project already supports it.
- Avoid leaking secrets or sensitive data in logs and responses.

## Checks

- Verify status codes, response bodies, validation failures, and authorization failures.
- Verify idempotency for retryable operations and background jobs.
- Verify timeouts and failure behavior for external integrations.
- Run relevant unit, integration, API, typecheck, or lint commands when available.

## Response Style

- State API behavior changes clearly.
- Call out security, data integrity, and compatibility risks.
