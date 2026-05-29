---
name: performance
description: Performance optimization, profiling, latency, memory, bundle size, database query speed, caching, throughput, and scalability. Use when diagnosing or improving slow, resource-heavy, or high-traffic behavior.
---

# Performance

Use this skill for latency, throughput, memory, CPU, bundle size, query performance, caching, scalability, and profiling work.

## Workflow

- Establish the performance symptom and likely bottleneck before optimizing.
- Prefer measuring or reproducing over guessing.
- Make the smallest change that addresses the bottleneck.
- Preserve correctness before improving speed.
- Avoid caching unless invalidation and staleness behavior are clear.

## Checks

- Check database query plans, N+1 queries, unnecessary network calls, expensive rendering, large payloads, and repeated work.
- Check memory growth, unbounded queues, and missing timeouts for server-side issues.
- Check bundle size, hydration cost, image weight, and layout thrashing for frontend issues.
- Run relevant benchmark, profiler, test, build, or smoke command when available.

## Response Style

- Explain the bottleneck and why the change should improve it.
- Include before/after measurements when available.
