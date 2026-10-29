# Review a change for logging drift

Paste the [shared instruction](00-shared-instruction.md) first.

```text
Apply the shared instruction (00-shared-instruction.md). Review the specified
diff and existing event ledger read-only; write only the report. Do not modify
application code or invent a baseline. Identify the revisions/paths actually
inspected.

If the baseline ledger is missing, review the supplied diff with explicit limits
and recommend assessment; do not fabricate prior coverage. With a ledger, retain
all event rows but revalidate the changed paths and any affected identities,
policy, configuration, collector, or consumer dependencies. Downgrade stale
covered evidence to missing (unverified), or unavailable_signal if its inputs
cannot be inspected. State which unchanged evidence was reused and why.

Trace new or moved security decisions, renamed events, changed field types,
logger filters, sampling, privacy controls, queue/failure policy, tenant
context, transports, retention, and consumer queries. Check whether new
auth/admin/data paths bypass the shared event path or whether framework upgrades
add automatic sensitive capture. Inspect removed events and weakened tests.
Distinguish a removed duplicate from lost coverage, and a changed implementation
from an actual semantic regression.

Reconcile the ledger against the assessed boundary and changed requirements,
features, controls, and reference/security-events.md. Preserve every SEC ID and
revalidate affected subcases. Reconcile checklist revisions without relabeling
old evidence as newly verified. Detect lost mappings, omitted rows, new
unassessed paths, and stale not_applicable decisions. Review event meanings and
consumer mappings when contracts change; preserve approved severity choices.

For each finding provide file/line or symbol evidence, affected event/consumer,
trigger, consequence, priority rationale, and focused verification. Suggest a
bounded repair and relevant wave. Flag unknown deployment configuration rather
than assuming it. Return no findings when supported; never invent issues to fill
a severity bucket. Report checks run/not run and missing baseline artifacts. Do
not apply fixes.
```
