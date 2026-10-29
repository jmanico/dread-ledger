# Verification matrix

Use synthetic fixtures in an isolated environment. Adapt to the runtime and mark
inapplicable cases with reasons. An unavailable test is NOT RUN, never PASS.
This matrix supplements [the verification
prompt](../prompts/07-verify-and-rollout.md).

| Test | Required observation |
| --- | --- |
| Successful and denied operation | Correct event name, outcome, actor/target, and count; original business response and state unchanged |
| Commit/rollback and async failure | No committed-success claim before commit; denied attempts survive rollback where policy requires; late job outcome distinct from enqueue |
| Unknown account/forged actor | No fabricated authenticated actor, no new account lookup/enumeration, generic external behavior retained |
| Spoofed forwarding/correlation | Trusted proxy rules enforced; validated trace context never grants identity or tenant membership |
| Concurrent tenants, impersonation, worker reuse | Effective actor/subject/original impersonator and provenance correct; no cross-request context leakage or cross-tenant queries |
| Secret canaries in all reachable inputs | Exact canaries absent from emitter, queue/spool, framework, exception, exporter, retry, fallback, and final fixture output |
| CR/LF, NUL, Unicode controls, delimiters | One parsable logical record; no injected keys, names, severity, or synthetic record; viewer/export encoding checked |
| Lazy/async object capture | Only allowlisted primitive snapshots enter the queue; later mutation cannot expose raw data or alter recorded identity |
| CSV spreadsheet exports | Formula prefixes `=`, `+`, `-`, `@`, including leading whitespace/control characters, remain literal in the supported spreadsheet consumer; ordinary quoting is insufficient |
| Oversize multibyte strings/arrays/nesting | Encoded event and memory caps honored; no broken encoding or required-field corruption |
| Unknown/malformed optional fields | Minimal valid event retained, unknown fields excluded, bounded safe validation signal; no raw rejected value |
| Invalid required envelope | Explicit producer error/health evidence and established audit failure policy; no falsely accepted required record |
| Sink slow/down, TLS/auth failure, disk full, permissions denied | Declared timeout/overflow/durability policy; bounded memory/disk/retries and unchanged ordinary business behavior |
| Logger throws or fails recursively | Original exception/outcome preserved; no recursive logging or emergency secret dump |
| Flood/noisy tenant/high-cardinality keys | Bounded state and resource use; documented optional aggregation; required audit retained or explicit policy failure, never silent loss |
| Process killed/restarted, shutdown deadline | Honest crash-loss window; durable backlog recovery where promised; no fabricated shutdown event |
| ID collisions and conflicting retransmissions | Authenticated producer namespaces separate equal IDs; client correlation never sets canonical ID; same-ID/different-record conflicts remain visible and both records retained/quarantined, not deduplicated away |
| Cross-tenant denial routing | Actor/resource tenant provenance and visibility decision tested for both tenants and central security; denied requests do not cause protected-resource enrichment or cross-tenant disclosure |
| Detector signal provenance | Client reports cannot spoof server/provider provenance; detector version and confidence semantics known; report/match text never asserts confirmed exploitation |
| Consumer egress | Alerts/tickets/chat/email/paging use approved field subsets, tenant-safe authorized links, retention/access policy, and safe rendering in isolated test targets |
| Retries, duplicates, reordering, clock skew | Stable retransmission IDs; distinct attempts retained; consumers do not invent total order from clocks |
| Production filters and unsampled traces | Required INFO/security records remain; security events independent of diagnostic sampling |
| Historical identity references | Equal local IDs across issuers/tenants and deleted/recreated accounts do not silently merge; attribution limits are documented without extending data retention |
| Field ownership and normalization | Duplicate keys, exporter/context overwrites, aliases, case-folding and normalized-name collisions cannot silently replace trusted event/actor/severity/outcome/tenant fields; conflicts follow visible approved failure handling |
| LLM/agent tracing and administrative entry points | Raw prompts/completions/tool I/O stay excluded across SDK capture and fallback paths; consoles, migrations and ops commands do not bypass required privileged-event coverage |
| Parser/schema migration | Every distinct serializer/schema branch/adapter/parser tested or NOT RUN; unknown versions and invalid types visibly rejected/quarantined under audit policy, never silently coerced/dropped |
| Consumer query and alert simulation | Expected record counts/IDs arrive; detection case matches and benign case does not; test route only |
| Collector silence and queue saturation | Independent health signal reaches its test destination within the declared budget |
| Storage/query permissions | Producer cannot read/delete unless explicitly needed; unauthorized tenant reads fail; log access monitored |
| Retention/hold/disposal | Approved policies cover spool, archives, replicas, backups, exports; local checks separated from infrastructure evidence |
| Performance and cost | Measured baseline and change under representative synthetic load; budgets stated, no invented measurements |
| Rollback | Existing audit and privacy controls remain; consumer compatibility and health still work |

Combine exact synthetic canaries with allowlist/schema assertions, code-path
review, and actual encoded output. Confirm that the application's secret-leak
checks reject a deliberately unsafe synthetic fixture.

## Coverage reconciliation

For repair-only mode under [prompt 08](../prompts/08-repair.md), apply the matrix
to the repaired paths and affected consumers. Retain applicable local safety
checks; mark full checklist reconciliation NOT RUN and assessment as the next
pass. Update affected existing ledger rows without inventing an absent ledger.
A verified repair does not establish foundation or deployment readiness.

For full-wave verification, reconcile every SEC ID in the
[security event checklist](security-events.md).
Verify the listed subcases and shared metadata rules, retaining their separate
boundaries and partial results. Report checklist dispositions separately from
runtime event counts; a shared event must not inflate either count.

Reconcile every ledger row using the [coverage status rules](coverage.md).
Report totals by implementation priority, highest-risk gaps first, and
owners/actions for remaining work. Verify triggers, safe context, and
delivery/detection at the claimed boundary. Check semantic equivalence for local
names or records mapped to multiple requirements; preserve severity mappings and
avoid duplicate emission.

## Synchronous completion and blocking

For each selected sink, distinguish callback return, full write, flush, and
required durability. Exercise short or zero-byte writes when supported by its
API; they must not silently count as complete delivery. A callable that returns
without throwing has not necessarily accepted the whole event.

Use controlled local blocking with a guaranteed release to check whether logging
can delay business responses or shutdown. No queue does not imply bounded I/O.
Record the actual bound and existing policy; an unresolved code-level blocking
path prevents that local foundation gate from passing. Do not build a new
transport solely for a test, or treat a temporary-file success as evidence for
an arbitrary caller-supplied sink.

Check failures before the sink as well as sink exceptions: encoding failures
must follow the documented loss-observation policy. When adding an event,
verify the consumer's expanded invocation set and timing; an unchanged callback
signature alone does not establish behavioral compatibility.
