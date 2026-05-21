# Skill: observability

**Type:** atomic

## Purpose

Design or improve the metrics, logging, and distributed tracing for a service such that its internal state is externally visible — enabling operators to answer "what is the system doing?" without reading source code or attaching a debugger.

## When to Invoke

- A new service is being deployed and needs observability from the start.
- An existing service is hard to debug in production because its state is opaque.
- An incident has revealed a gap in visibility — something failed but there was nothing to see.
- An SLO is being defined and the signals needed to measure it don't yet exist.

## Workflow

1. **Define what questions observability must answer.** Start with the SLO:
   - Is the service meeting its availability and latency targets?
   - Where are requests slow or failing?
   - What does a healthy service look like vs. a degraded one?
   If there is no SLO yet, define one before designing observability — you cannot know what to measure without knowing what success looks like.

2. **Design metrics (RED + USE).** Use two frameworks:
   - **RED** (for request-handling services): Rate (requests/second), Errors (error rate), Duration (latency distribution p50/p95/p99)
   - **USE** (for resource-handling systems): Utilisation, Saturation, Errors per resource (CPU, memory, connections, queues)
   Define which metrics will be emitted, their labels/dimensions, and their cardinality. High-cardinality metrics (unbounded label values) are expensive — scope them carefully.

3. **Design logging.** Define a logging standard for the service:
   - Use structured logs (JSON) — not free-text
   - Log level conventions: ERROR for actionable failures, WARN for unexpected but non-fatal, INFO for significant events, DEBUG for diagnostic detail (off in production)
   - Each log line must include: timestamp, service name, level, trace/request ID, and event description
   - Never log PII, credentials, or tokens at any level

4. **Design distributed tracing.** For services that call other services:
   - Propagate trace context across all outbound calls (HTTP headers, queue metadata)
   - Create spans for: inbound requests, outbound calls, database queries, and queue operations
   - Include span attributes that help diagnose slow traces: resource identifiers, result codes, data sizes

5. **Define dashboards.** For each service, define at least one dashboard with:
   - The RED metrics for all key endpoints
   - The USE metrics for all key resources
   - SLO burn rate (how fast is the error budget being consumed?)
   The dashboard must be useful during an incident — not just a collection of graphs.

6. **Verify signal quality.** For each signal, confirm:
   - It is emitted in all relevant code paths (not just the happy path)
   - It can be queried efficiently in the observability platform
   - It produces actionable information when a problem occurs

## Output

- **Metrics design** — list of metrics with names, types, labels, and rationale
- **Logging standard** — log levels, format, required fields, and what NOT to log
- **Tracing design** — span boundaries, context propagation, and key attributes
- **Dashboard definition** — the panels, queries, and layout for the service dashboard
- **SLO signal map** — which signals feed each SLO measurement
