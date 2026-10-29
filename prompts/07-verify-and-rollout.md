# Verify each wave and prepare rollout

Paste the [shared instruction](00-shared-instruction.md) first.

```text
Apply the shared instruction (00-shared-instruction.md). Verify the selected
diff and ledger, including the foundation. Use reference/verification.md when
available. Do not deploy, activate production alerts, send notifications, or
test production faults.

Default to full-wave verification. When invoked by prompt 08 for a bounded
repair without new event coverage, use repair-only mode: verify the diff,
affected paths, and consumer dependencies with the applicable checks below.
Update affected ledger rows if available; otherwise record ledger not yet
established. Mark full checklist reconciliation NOT RUN and hand off to
assessment instead of generating an inventory. Keep unrelated evidence at its
original revision. Report the repair's result separately from foundation and
deployment gates; do not pass either on the repair alone. Missing local safety
prerequisites block a verified-repair claim. New coverage requires Wave 0 and
full-wave verification.

Run relevant baseline/regression tests plus focused positive, negative,
secret-canary, injection, encoded-size, tenant/async-context, sink-failure,
queue-pressure, shutdown, retry/duplicate, and transaction-outcome tests.
Exercise real encoding and configured filters, not just mocks. Check logging at
normal production levels and when traces are unsampled. Inspect output from
applicable framework, exporter, fallback, and error paths.

Reconcile expected synthetic event IDs/counts through emitter, collector,
persisted sink, query, and only explicitly designated isolated test
destinations, tagged environment=test or its project equivalent. Never infer a
test target from current configuration. If no isolated target exists, mark that
boundary NOT RUN. Identify each untested boundary. Test parser/version
compatibility and a benign case that must not alert. Record
retention/access/tenant-isolation and log-access audit checks separately. Test
independent detection of logging silence and queue saturation: a broken pipeline
cannot be its only health channel. Verify drop/loss signals remain bounded and
safe.

For full-wave verification, reconcile the ledger against assessed features,
controls, risks, and requirements and every SEC ID in
reference/security-events.md. Verify each applicable subcase before marking its
summary covered. Preserve missing and unavailable rows, and report checklist
totals separately from event counts. Every candidate event needs a disposition;
identify uninspected areas and newly discovered gaps. For covered rows require
trigger/mapping evidence, safe fields, owner, consumer, and actual test results
at the claimed boundary. NOT RUN is not verification. Revalidate not_applicable
decisions against architecture; missing detectors or provider access remain
unavailable_signal, not covered or not_applicable. Report totals by
implementation priority and status, list the highest-risk gaps first, and carry
owners/actions for all unresolved rows. A partial wave can finish locally with
gaps disclosed; do not call the application's coverage complete while applicable
events remain missing, unavailable, or unverified.

Define a canary plan with owner, scope, duration, expected volume, measured
baseline, latency/resource/cost budgets, alert delivery target with its own
outgoing-field allowlist/access/retention policy, and rollback triggers. Use
actual project thresholds or label proposed values pending an owner decision. Do
not fabricate performance results. A staged rollout must preserve existing
required audit and privacy controls. Include consumer compatibility across
schema versions, backlog/spool drain or format compatibility, and an owner
decision for already-collected new data. Do not delete retained evidence
automatically. Reverting must not restore secrets or disable all security
logging. Where rollback cannot preserve them, propose a safe forward fix and
call out the limitation.

Report PASS/FAIL/NOT RUN per check with exact commands, sanitized evidence, and
why a check was not run. Distinguish local implementation verified from
deployment ready and end-to-end verified. List unresolved policy/infrastructure
decisions and follow-up owner. Limit coverage and detection claims to the
boundaries actually verified.
```
