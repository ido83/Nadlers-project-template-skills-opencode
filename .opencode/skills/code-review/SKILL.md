---
name: code-review
description: Code review, PR review, diff review, maintainability review, regression risk, bug finding, and review comments. Use when the user asks for a review or wants risks, defects, or missed tests identified.
---

# Code Review

Use this skill when reviewing changes for correctness, regressions, security issues, maintainability, and missing tests.

## Workflow

- Inspect the diff and relevant surrounding code before forming conclusions.
- Prioritize bugs, behavioral regressions, security risks, data loss risks, and missing tests.
- Avoid style-only comments unless they materially affect maintainability or violate clear project conventions.
- Verify assumptions against code when possible.

## Findings Format

- List findings first, ordered by severity.
- Include file and line references.
- Explain the user-visible or operational impact.
- Suggest a focused fix when the fix is clear.

## Response Style

- If no findings are discovered, say so explicitly.
- Mention residual risks or test gaps separately from confirmed findings.
