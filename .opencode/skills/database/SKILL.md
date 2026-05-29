---
name: database
description: Database schemas, SQL, migrations, indexes, query performance, transactions, ORMs, data modeling, and persistence bugs. Use when changing tables, migrations, queries, relationships, constraints, or database access code.
---

# Database

Use this skill for data modeling, migrations, SQL, ORM queries, indexes, constraints, transactions, and persistence behavior.

## Workflow

- Inspect the current schema, migrations, relationships, indexes, and query patterns before editing.
- Prefer safe, reversible migration steps for production data.
- Preserve existing data unless the user explicitly asks for destructive changes.
- Use constraints and transactions to protect invariants when supported by the project.
- Avoid N+1 queries and unnecessary full-table scans.

## Checks

- Verify migration order, rollback behavior, nullability, defaults, and backfills.
- Verify indexes match real filter, join, and sort patterns.
- Verify queries handle empty results and duplicate rows correctly.
- Run formatting, migration validation, query tests, or database test suites when available.

## Response Style

- Highlight migration safety and data compatibility.
- Note any manual production rollout or backfill steps.
