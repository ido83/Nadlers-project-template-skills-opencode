# Nadlers Project Template Skills for opencode

Project-local opencode skills and a Docker Compose based security scanning toolkit.

## Contents

- `.opencode/skills/` contains project skills loaded by opencode.
- `.opencode/skills/mr/SKILL.md` adds merge request and pull request workflows.
- `.opencode/skills/jira-user-story/SKILL.md` adds Jira user story writing workflows.
- `docker-compose.security.yml` runs common security scanners in containers.
- `.gitignore` and `.dockerignore` exclude local secrets, generated output, caches, and scan artifacts.

## opencode Skills

The repository includes skills for backend, frontend, fullstack, database, DevOps, testing, performance, code review, README documentation, cyber security, merge requests, and Jira user stories.

The `mr` skill is used when preparing or reviewing merge requests and pull requests. It focuses on:

- MR-ready summaries.
- Testing and risk notes.
- Review findings with file and line references.
- Avoiding commits, pushes, or remote MR changes unless explicitly requested.

The `jira-user-story` skill is used when creating or improving Jira stories, backlog items, epics, and feature tickets. It includes:

- Subject and user story structure.
- Context info, scope, dependencies, and assumptions.
- Mermaid diagram guidance.
- Motivation, success criteria, Definition of Done, and delivery checklist.

Restart opencode after changing files under `.opencode/skills/`; running sessions keep the already-loaded configuration.

## Security Scanning

Use `docker-compose.security.yml` to run security tools without installing them locally.

Validate the Compose file:

```sh
docker compose -f docker-compose.security.yml config
```

Run all services as a smoke test:

```sh
docker compose -f docker-compose.security.yml up --abort-on-container-exit --remove-orphans
```

For complete scan results, run scanners individually because some tools finish earlier than others:

```sh
docker compose -f docker-compose.security.yml run --rm gitleaks
docker compose -f docker-compose.security.yml run --rm trivy-fs
docker compose -f docker-compose.security.yml run --rm trivy-config
docker compose -f docker-compose.security.yml run --rm trivy-sbom
docker compose -f docker-compose.security.yml run --rm kics
docker compose -f docker-compose.security.yml run --rm syft
docker compose -f docker-compose.security.yml run --rm grype
docker compose -f docker-compose.security.yml run --rm semgrep
```

Clean stopped containers after scans:

```sh
docker compose -f docker-compose.security.yml down --remove-orphans
```

## Included Tools

- `gitleaks`: secret scanning.
- `trivy-fs`: filesystem vulnerability, secret, misconfiguration, and license scanning.
- `trivy-config`: infrastructure/configuration misconfiguration scanning.
- `trivy-sbom`: CycloneDX SBOM generation to `sbom.cdx.json`.
- `kics`: infrastructure-as-code scanning.
- `syft`: CycloneDX SBOM generation to `sbom.cdx.json`.
- `grype`: dependency vulnerability scanning.
- `semgrep`: static application security testing.

## Current Scan Notes

The compose stack was tested with individual scanner runs:

- `gitleaks`: passed, no leaks found.
- `semgrep`: passed, 0 findings.
- `syft`: passed and generated `sbom.cdx.json`.
- `grype`: passed, no vulnerabilities found.
- `trivy-fs`: passed, no vulnerabilities detected in the scanned lockfile.
- `trivy-config`: passed, but no supported config files were found.
- `trivy-sbom`: passed and generated `sbom.cdx.json`.
- `kics`: completed and reported medium hardening findings against `docker-compose.security.yml`, including missing `security_opt`, missing healthchecks, unrestricted capabilities, and shared volumes.

`sbom.cdx.json` is ignored by Git as a local scan artifact.
