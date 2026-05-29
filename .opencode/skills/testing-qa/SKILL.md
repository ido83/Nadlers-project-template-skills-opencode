---
name: testing-qa
description: Testing and QA work including unit tests, integration tests, end-to-end tests, fixtures, mocks, flaky tests, test coverage, and regression verification. Use when adding, fixing, reviewing, or running tests.
---

# Testing QA

Use this skill for adding, fixing, reviewing, and running tests across unit, integration, end-to-end, contract, and regression suites.

## Workflow

- Identify the behavior under test before choosing the test layer.
- Prefer deterministic tests that verify observable behavior, not implementation details.
- Keep fixtures small and explicit.
- Avoid broad mocks when a narrower fake or real integration is more valuable and practical.
- Reproduce failing tests before changing behavior when feasible.

## Checks

- Verify happy paths, edge cases, validation failures, authorization failures, and regressions.
- Check for timing assumptions, shared state, order dependence, and environment coupling in flaky tests.
- Run the smallest relevant test first, then broader suites if needed.

## Response Style

- State what behavior is now covered.
- Include exact test commands and results.
