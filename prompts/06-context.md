# Wave 4 — lower-priority investigation context

Paste the [shared instruction](00-shared-instruction.md) first.

```text
Apply the shared instruction (00-shared-instruction.md). Verify Wave 0 before
edits. Wave 4 is lower implementation priority, not DEBUG or permission to log
everything. Only add context that answers a named investigation or operational
security question.

Revisit reference/security-events.md for remaining lifecycle and operational
context. Record account, data, backup, process, and job transitions only where
they answer a defined security question. Promote sensitive or privileged gaps.

Review remaining account creation/change/archival/deletion, sensitive-data
create/read/update/delete, upload processing, process lifecycle, configuration
version references, and background-job outcomes. Use application event names and
promote consequential gaps to earlier waves.

Distinguish upload receipt, storage, scan results, and deletion; receipt or
storage does not establish safe content. Record sensitive-data operations with
periodic review ownership and no content copies. Keep initiating actor and
affected account distinct. Preserve deletion, archival, and retention behavior;
logging a deletion does not authorize retaining the deleted data.

Use safe field-name enums and opaque references, never user profile dumps,
configuration values, raw file paths/names, data snapshots, or environment
variables. Do not log every request or successful authorization by default.
Explain why existing infrastructure logs do not already answer the question.
Never fabricate a shutdown/crash event when the process cannot execute; rely on
independent observation for abrupt termination.

Preserve useful correlation through jobs/retries without copying secrets or
arbitrary trace baggage. Verify context cleanup across threads, asynchronous
work, and worker reuse. A correlation ID links activity but cannot prove
identity or ordering.

Estimate event volume from measured/explicitly hypothetical workload and event
size; include indexes, replicas, retention, and ingestion cost where known.
Identify who will use each event. Do not add events with no purpose or owner.
Remove only newly proposed unnecessary fields, not existing audit coverage,
without an explicit decision.

Verify schema stability, useful queries, privacy, tenant access, and
cost/latency limits. Return accepted and rejected proposals with reasons. Run
verification and rollout next.
```
