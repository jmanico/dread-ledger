# Wave 0 — build the safe path

Paste the [shared instruction](00-shared-instruction.md) first.

```text
Apply the shared instruction (00-shared-instruction.md). Implement the smallest
safe foundation for the selected service using its existing logger and
framework. Wave 0 is a prerequisite for all coverage waves. Preserve existing
events and consumers.

Review the audit-pipeline items in reference/security-events.md, especially
logging changes, loss, collection delay, clock anomalies, and redaction
failures. Establish their local safety requirements before coverage waves.

Read the assessment and identify a single shared security-event path. Define and
test a versioned field allowlist, stable names, explicit types and byte limits,
constant messages, trusted actor/tenant extraction, event IDs and interaction
IDs where a real interaction exists, UTC timestamps, and outcome semantics. If
reference/event-contract.md is available, adapt it to the existing logger and
consumer formats. Prefer an adapter over replacement.

Exclude sensitive values before any queue or sink. Inspect automatic HTTP, ORM,
exception, LLM/agent tracing SDK, tracing, and exporter instrumentation for
bypasses. Keep raw exceptions out of security events. Reject unknown metadata;
preserve a minimal event if optional context is malformed. Apply output encoding
and size caps without producing invalid JSON or silently losing required fields.
Verify consumer compatibility and filtering.

Document and implement bounded transport behavior using existing facilities:
capacity, encoded bytes, spool permissions/quota, retries/backoff/timeouts,
overflow handling, and shutdown deadline. Required audit follows its existing
policy; unresolved audit atomicity or fail behavior defers that event's
instrumentation, not its business operation. Record loss windows honestly. For a
required durable event, demonstrate the durable boundary, not merely queue
acceptance. Add nonrecursive, independent health monitoring for saturation,
drops, lag, and silence.

Define sink access separation, tenant isolation, retention and deletion/hold
handling, transport authentication, and evidence-integrity prerequisites.
Implement authorized local configuration; mark unavailable infrastructure checks
as deployment blockers. Do not invent retention durations, custom cryptography,
or a new destination.

Use representative synthetic fixtures for each distinct serializer, schema
branch, transport adapter, and consumer parser in scope. Mark uncovered branches
NOT RUN. Exercise real encoding and strict unknown-version/invalid-type consumer
handling. Test secret canaries, malformed optional context, CR/LF and Unicode
controls, encoded-size overflow, logger exception, full queue, sink timeout,
concurrent tenant requests, and shutdown behavior. Preserve business responses
and decisions.

A synchronous sink can still block; no queue does not establish a timeout or
bounded shutdown. Verify the selected sink's actual completion semantics,
including partial or zero-byte writes where applicable. Do not label callback
return or queue acceptance as delivery. If a newly used path can block the
business operation without an established bound/policy, keep its local gate
open; do not move that code-level uncertainty into deployment prerequisites.

Report local and deployment gates separately. The local gate covers inspected
code/configuration, real encoding into an isolated sink, applicable isolation
and failure tests, and an explicit contract. Remote retention, access,
transport, consumer/alert delivery, and operational ownership need deployment
evidence. Unknown production infrastructure blocks deployment, not otherwise
verified local coverage work. Unresolved local safety or policy still blocks
that work. Do not treat test doubles as production evidence.

Return the contract/ledger, code and configuration changes, exact test evidence,
limits, consumer migration needs, and foundation gate status. Do not add broad
new coverage until the relevant foundation checks pass. Run the verification
prompt for this pass.
```
