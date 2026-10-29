# Repair unsafe existing logging

Paste the [shared instruction](00-shared-instruction.md) first.

```text
Apply the shared instruction (00-shared-instruction.md). Assess the selected
unsafe logging path, then make a bounded local repair. This pass may precede
Wave 0 to stop an existing exposure; it does not waive the foundation for new
event coverage.

If a ledger already exists, update affected rows and invalidate stale evidence.
If none exists, say ledger not yet established, report only the repair's scope,
and hand off to assessment; do not delay a bounded leak repair to fabricate a
full inventory. Keep coverage claims limited to the repaired path.

Trace raw request/response, exception, framework, ORM, trace baggage, collector,
fallback, LLM/agent tracing SDK, and export paths. Locate sensitive data,
interpolation/injection, arbitrary objects, unbounded events, recursive error
logging, or unsafe sink access. Cite code and data categories without displaying
actual values. Do not fetch production logs.

Replace unsafe context with a per-event allowlist and safe references; retain
useful security event presence and outcomes. Use the existing structured
encoder, fix limits and fallback behavior, and preserve consumer mappings. Do
not solve leakage by globally turning off audit, weakening authentication, or
hiding all failures.

Add synthetic regression canaries in headers, query strings, payloads,
filenames, exceptions, and nested fields as applicable. Test every reachable
sink and error path. Prove injection resistance and bounded resource use. Record
consumers requiring updates. If code suggests historical leakage, report the
exposure category and recommend the existing incident/credential-rotation
process; do not copy evidence, delete historical logs, rotate credentials, or
change legal holds in this pass.

Return repair evidence and remaining foundation work. Invoke prompt 07 in
repair-only mode for this diff, its affected paths, and consumer dependencies.
Run relevant local safety and regression checks; missing prerequisites still
block a verified-repair claim. Update affected rows if a ledger exists;
otherwise record ledger not yet established. Mark full checklist reconciliation
NOT RUN and hand off to assessment. This mode permits no new event coverage or
blanket foundation/deployment PASS. Rollback must not reintroduce the exposure.
If the repair cannot be verified, report the specific blocker rather than
declaring the path fixed.
```
