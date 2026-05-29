---
name: mr
description: Merge request, MR, pull request, PR preparation, review, description, checklist, and change-summary workflow. Use when creating, updating, or reviewing merge requests.
---

# Merge Request

Use this skill when the user asks to create, prepare, update, review, or summarize an MR or PR.

## Workflow

- Inspect `git status`, the relevant diff, and recent commits before writing an MR summary or review.
- Identify the target branch, source branch, included commits, and changed files when that information is needed.
- Separate confirmed behavior changes from inferred intent.
- Highlight risky areas, migrations, config changes, security impact, and test coverage gaps.
- Do not commit, push, open an MR, or edit remote metadata unless the user explicitly asks.
- Preserve user-authored changes and avoid reverting unrelated work in a dirty worktree.

## MR Description

Prefer this structure unless the repository has a template:

```markdown
## Summary
-

## Testing
-

## Risk
-
```

Include screenshots, rollout notes, migration notes, or follow-up tasks only when relevant.

## Review Focus

- Check for regressions, missing validation, missing authorization, data loss, concurrency issues, and insufficient tests.
- Include file and line references for findings.
- Prioritize actionable issues over style preferences.
- If no findings are found, state that clearly and mention any residual testing gaps.

## Response Style

- Lead with MR-ready output or review findings.
- Keep summaries concise and concrete.
- Include exact commands run and whether they passed when verification was performed.
