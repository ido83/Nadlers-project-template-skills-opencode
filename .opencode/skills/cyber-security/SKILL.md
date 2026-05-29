---
name: cyber-security
description: Cybersecurity, secure coding, security gates, SBOM, .gitignore, .dockerignore, AI agent tokens, OpenAI, Claude, Gemini, Anthropic, CVE/CVSS policy, gitleaks, trivy, kics, lint scans, threat modeling, vulnerability fixes, remediation, mitigation, attestation, evidence, auth hardening, secrets handling, dependency risk, and security reviews. Use when assessing or changing security-sensitive code, configuration, authentication, authorization, cryptography, input handling, CI security gates, SBOMs, ignore files, Docker build context, AI provider credentials, or scan results.
---

# Cyber Security

Use this skill for secure coding, vulnerability analysis, security gates, threat modeling, authentication, authorization, secrets, cryptography, dependency risk, and security reviews.

## Workflow

- Identify assets, actors, trust boundaries, inputs, outputs, and privilege changes before editing.
- Prefer simple, standard security controls over custom cryptography or clever validation.
- Enforce authorization server-side and deny by default for sensitive operations.
- Treat secrets, tokens, session data, PII, credentials, and AI provider keys as sensitive.
- Treat AI agent and LLM provider credentials as secrets, including OpenAI, Anthropic, Claude, Gemini, Google AI, Azure OpenAI, Mistral, Cohere, Groq, OpenRouter, Hugging Face, Perplexity, Together, Replicate, and xAI tokens.
- Do not print, commit, or expose secret values.
- When changing security gates, preserve the existing pass/fail policy unless the user explicitly asks to change severity thresholds.
- For package and image dependencies, require known CVEs to have CVSS scores under 8.0 unless there is documented remediation, mitigation, or an explicit accepted-risk decision.
- Always create or update the SBOM when changing dependencies, lockfiles, container images, build artifacts, release assets, or security gates. If an SBOM already exists, update it in the same format and location unless the user asks otherwise.
- Always create or update `.gitignore` and `.dockerignore` for security-sensitive work, dependency changes, container changes, build changes, or new projects. Preserve existing entries and add relevant ignores for secrets, local state, generated files, and Docker build context hygiene.

## Checks

- Check for injection, XSS, CSRF, SSRF, path traversal, insecure deserialization, open redirects, and broken access control.
- Check password, token, cookie, session, and CORS behavior where relevant.
- Check dependency and configuration changes for widened attack surface.
- Run relevant security, test, lint, or dependency audit commands when available.

## Security Gates

- Run `gitleaks` for secret scanning when secrets, config, CI, deployment files, or repository history risk is relevant.
- Run `trivy` for dependency, container image, filesystem, and IaC vulnerability scanning when packages, lockfiles, Dockerfiles, images, Kubernetes, Terraform, or deployment assets change.
- Run `kics` for infrastructure-as-code scanning when Terraform, Kubernetes, Docker Compose, CloudFormation, Helm, or other IaC files change. If the user says "kicks", treat it as likely referring to `kics` unless the repo uses a different tool.
- Run project linters for security-sensitive code paths, because many injection, unsafe API, and configuration mistakes are caught by language or framework lint rules.
- Prefer repository-provided commands from `package.json`, `Makefile`, CI workflows, scripts, or docs before inventing new scan commands.
- If a scanner is not installed, report that clearly and provide the exact command that would be run in CI or a prepared environment.
- Do not suppress or downgrade scan findings without documenting the reason, scope, and compensating control.

## SBOM

- Check for an existing SBOM before creating a new one. Common names include `sbom.json`, `sbom.cdx.json`, `bom.json`, `cyclonedx.json`, `spdx.json`, and files under `security/`, `docs/security/`, `compliance/`, `audit/`, or CI artifact paths.
- Preserve the existing SBOM format when updating, such as CycloneDX JSON, CycloneDX XML, SPDX JSON, or SPDX tag-value.
- If no SBOM exists, prefer CycloneDX JSON unless the project or CI already uses SPDX or another standard.
- Generate the SBOM from the actual lockfiles, installed dependencies, image, or build artifact being scanned. Do not hand-write package inventories.
- Include the SBOM in security evidence or attestation when applicable.
- If the required SBOM tool is not installed, report that clearly and provide the exact command to run in CI or a prepared environment.

Common SBOM commands:

```sh
trivy fs --format cyclonedx --output sbom.cdx.json .
trivy image --format cyclonedx --output sbom.cdx.json IMAGE_NAME
syft . -o cyclonedx-json=sbom.cdx.json
syft IMAGE_NAME -o cyclonedx-json=sbom.cdx.json
```

## Ignore Files

- Ensure `.gitignore` exists and excludes secrets, credentials, local environment files, editor files, dependency directories, generated artifacts, logs, caches, and operating system files relevant to the project.
- Ensure `.dockerignore` exists when Dockerfiles, images, containers, deployment packaging, or Docker build context are relevant.
- Never add `.git` to `.gitignore` as a tracked ignore rule for Git behavior; add `.git` to `.dockerignore` so repository history is not sent to Docker build contexts.
- Preserve files that must remain tracked, such as lockfiles, example environment files, templates, documentation, migrations, and source code.
- Prefer explicit secret patterns over broad patterns that could hide important source files.
- Ignore local AI agent credential stores and provider token files explicitly; avoid broad patterns like `*token*` that can hide legitimate source files.
- If adding ignore rules could stop tracking files already committed, report that and recommend removing them from Git history or the index with care.

Common `.gitignore` security entries:

```gitignore
.env
.env.*
!.env.example
*.pem
*.key
*.p12
*.pfx
*.crt
*.csr
id_rsa*
id_ed25519*
secrets/
credentials/
.openai/
.anthropic/
.claude/settings.local.json
.claude/.credentials.json
.gemini/credentials.json
.gemini/oauth_creds.json
.codex/
.aider*
.openai-key
.openai-token
.anthropic-key
.anthropic-token
.claude-key
.claude-token
.gemini-key
.gemini-token
ai-tokens.*
agent-tokens.*
llm-tokens.*
*.log
node_modules/
dist/
build/
coverage/
.cache/
.DS_Store
Thumbs.db
```

Common `.dockerignore` security entries:

```dockerignore
.git
.gitignore
.env
.env.*
!.env.example
*.pem
*.key
*.p12
*.pfx
secrets/
credentials/
.openai/
.anthropic/
.claude/settings.local.json
.claude/.credentials.json
.gemini/credentials.json
.gemini/oauth_creds.json
.codex/
.aider*
.openai-key
.openai-token
.anthropic-key
.anthropic-token
.claude-key
.claude-token
.gemini-key
.gemini-token
ai-tokens.*
agent-tokens.*
llm-tokens.*
node_modules/
dist/
build/
coverage/
.cache/
*.log
Dockerfile*
docker-compose*.yml
README.md
```

Adjust ignore entries to the repository's language, framework, package manager, and build system. Do not blindly copy every example if it would exclude required build inputs.

## Vulnerability Policy

- Prefer fixed package versions with no known high-risk CVEs. Do not introduce or keep dependencies with CVSS 8.0 or higher without a documented exception.
- For CVEs with CVSS 8.0 or higher, first attempt remediation by upgrading, replacing, removing, patching, or reconfiguring the affected package or image.
- If remediation is not immediately possible, document mitigation such as disabling vulnerable features, restricting network exposure, adding compensating controls, pinning safer transitive versions, or isolating the component.
- If neither remediation nor mitigation is possible in the current change, document the blocker, affected asset, CVE ID, CVSS score, exploitability, impact, owner, and target fix date.
- Treat ignored findings as risk acceptances, not fixes. Every ignore must include scope, expiration, justification, and approver when the project has an approval process.

## Attestation And Evidence

- Create evidence for security gates when requested or when making security-sensitive dependency, image, CI, or infrastructure changes.
- Evidence should include tool name, command, timestamp when available, target scanned, scanner version when available, policy threshold, pass/fail result, and remaining findings.
- Attestation should state what was scanned, which policy was applied, whether the artifact passed, and any exceptions or mitigations.
- Prefer existing project evidence locations such as `security/`, `docs/security/`, `compliance/`, `audit/`, or CI artifacts. If no convention exists, ask before adding a new evidence directory.
- Do not include secrets, private tokens, full vulnerable payloads, or sensitive infrastructure details in evidence files.

## Common Commands

```sh
gitleaks detect --source . --redact
trivy fs .
trivy config .
kics scan --path .
```

Use project-specific flags when available, such as severity thresholds, ignore files, output formats, or CI config. Avoid printing secret values; prefer redacted scanner output.

## Response Style

- Lead with concrete risks and exploitability.
- Distinguish confirmed vulnerabilities from hardening suggestions.
- Summarize security gate results by tool, pass/fail status, and blocking findings.
- Include safe remediation steps without providing exploit instructions beyond what is needed to fix the issue.
