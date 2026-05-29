---
name: devops
description: DevOps, CI/CD, infrastructure, containers, cloud, deployments, monitoring, and reliability. Use when working on pipelines, Docker, Kubernetes, Terraform, cloud config, release automation, or operational runbooks.
---

# DevOps

Use this skill for DevOps and operations work, including CI/CD pipelines, infrastructure as code, containers, Kubernetes, cloud configuration, deployment automation, monitoring, incident response, and reliability improvements.

## Workflow

- Inspect existing project conventions before changing pipeline, infrastructure, or deployment files.
- Prefer the smallest safe change that fixes the operational problem.
- Treat secrets, credentials, tokens, and private keys as sensitive. Do not print, commit, or hardcode them.
- Preserve existing environment names, release flows, and rollback mechanisms unless explicitly asked to change them.
- Validate syntax and behavior with the most relevant local command when available.

## Common Checks

- For CI changes, verify workflow syntax and job dependencies.
- For Docker changes, verify build context, ignored files, image size, runtime user, exposed ports, and health checks.
- For Kubernetes changes, verify namespaces, labels/selectors, probes, resources, config maps, secrets references, and rollout behavior.
- For Terraform changes, run formatting and validation before proposing apply steps.
- For deployment changes, identify rollback steps and blast radius.

## Response Style

- State operational risks clearly.
- Include exact commands that were run and their results.
- If a change requires credentials or access outside the workspace, explain the blocker and the safest next step.
