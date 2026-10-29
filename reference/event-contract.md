# Event contract

Adapt these fields to the application's existing logger and consumers. Define
each field's type, maximum encoded length, trusted source, purpose, and policy.
Version mappings and test migrations.

## Minimal envelope

| Field | Rule |
| --- | --- |
| `schema_version` | Positive integer or established version convention; never silently reinterpret fields |
| `event_id` | Non-secret producer-generated unique identifier; stable for retransmissions of the same logical record |
| `event` | Stable application event name with a documented trigger; never concatenate actor data |
| `timestamp` | Origin event time in an offset-aware format, preferably UTC; keep observation time separately where needed |
| `service`, `environment` | Deployment-established bounded identifiers, not request input |
| `severity` | Documented logger enum, independent of wave and detection confidence |
| `outcome` | Controlled enum such as success, failure, denied, attempted, rolled_back, unknown; definition attached to the exact trigger |
| `security_relevant` | True for this event stream; use existing consumer classification if equivalent |
| `audit_required` | Policy-established boolean; cannot be overridden by client input |

Conditional fields include `actor_ref`, `actor_kind`, `actor_provenance`,
`tenant_ref`, `target_ref`, `action`, `reason_code`, `interaction_id`,
`trace_id`, `observed_timestamp`, `confidence`, `rule_id`, `impersonator_ref`,
`impersonator_provenance`, `context_status`, `session_audit_ref`,
`token_record_ref`, `actor_tenant_ref`, `resource_tenant_ref`,
`signal_provenance`, `detector_id`, and `detector_version`. Absence is
preferable to a fabricated identity. The ledger defines which are required for a
particular event. `actor_kind=unknown` is appropriate when a failed login
establishes no identity. A tenant claim is not a trusted tenant reference.

In this template, `actor_kind` is user, service, anonymous, or unknown;
`actor_provenance` is verified_session, validated_token, authenticated_service,
trusted_internal_assertion, or server_assumed_identity; omit it when no identity
has been established. During impersonation, `actor_ref` is the effective subject
whose permissions are used, and `actor_provenance=server_assumed_identity` means
the server validated the authorized assumption of that identity, not that the
subject logged in. `impersonator_ref` is the original authenticated operator,
with `impersonator_provenance` set to that operator's verified_session,
validated_token, authenticated_service, or trusted_internal_assertion source.
`target_ref` remains the object/account affected by the action. Use both
identity fields for investigation; never attribute an impersonated action solely
to the effective subject. Multi-hop delegation requires a separately designed
bounded provenance contract; do not flatten it into a fabricated direct login.
Submitted identity claims are omitted by default; approved alternate contracts
must keep them explicitly unverified and never promote them to `actor_ref`. This
may limit account-level detection; document the limit instead of inventing a
join. `context_status` is omitted for normal context or set to a fixed
optional_context_omitted / optional_context_invalid code.

Outcome meanings: attempted means initiation only; success means the named
operation completed (for mutations, committed); denied means a policy/validation
control rejected it; failure means an attempted operation did not complete,
including rejected credential verification; rolled_back means a started mutation
was undone; unknown means completion is unestablished. Fix the meaning per event
rather than using HTTP status as a proxy. For example, login rejection is
failure, an authorization rejection is denied, and a rolled-back role change
cannot be success.

The event ledger can mark audit policy pending_decision. Runtime
`audit_required` is a boolean only after policy is resolved and is derived from
the trusted event catalog, not chosen ad hoc by callers. An unresolved policy
blocks new instrumentation on that path; it must never be coerced to false.

Optional context is allowlisted separately for each event. There is no general
`metadata` escape hatch. Stable route templates can replace raw URLs. Use
non-secret object IDs in place of names/content. If the event is too large, omit
optional context with a fixed `context_status` marker. Reserve enough capacity
for the minimal envelope; do not truncate serialized JSON bytes, split an event
into forged records, or trim a required field into a different identity.

Consumers must handle unsupported schema versions or invalid types visibly:
reject or quarantine under the established audit failure policy, retain required
evidence in an access-controlled bounded facility when policy permits, and emit
fixed safe health codes. Never silently coerce types, reinterpret versions, or
discard required audit. Unknown-version and invalid-type tests must cover every
applicable parser.

Malformed trusted envelope fields indicate a producer defect. Emit a fixed safe
schema-failure signal through the bounded health mechanism and apply the
established audit failure policy. Do not turn invalid required audit into a
claimed success. Malformed *optional untrusted* context must not erase an
otherwise valid security event.

## Checklist metadata

For the [security event checklist](security-events.md), map event type, action,
outcome, reason, source, actor/workload, tenant, target, correlation, and policy
or rule to the existing schema. Record event time at the producer and ingestion
time at the receiver; keep the fields distinct and document unavailable times.
Document unknown or inapplicable context instead of manufacturing values or
collecting unnecessary identifiers. For inferred threats, preserve confidence
and access-controlled supporting event references separately from confirmed
actions or compromise. Apply the same exclusions when reporting a disclosure.

## Identity and data protection

Record actor and affected subject separately; delegated actions may also need
the original impersonator. Bind tenant IDs to validated server context. Verify
context cleanup on reused worker threads and asynchronous jobs. Client-supplied
trace and forwarding headers need validation and trust-boundary handling. Do not
treat a validly formatted trace ID as authoritative identity.

For each event, `tenant_ref` identifies the approved routing/visibility
partition, not whatever tenant was requested. When relevant, `actor_tenant_ref`
and `resource_tenant_ref` hold separately established tenant identities. Omit
unverified claims; never look up a protected resource solely to enrich a denied
event. Cross-tenant denials need an explicit routing/access decision,
potentially a security-only partition. Test both tenants' visibility and central
security access: neither tenant may receive the other's identity or resource
details merely because the event mentions it.

Opaque identifiers can still be personal data. Minimize access, retention, and
linking across datasets. Avoid unsalted hashes of predictable identifiers. If
approved pseudonymization is necessary, use the organization's established
keyed/tokenization service and document rotation, access, collision, and
correlation tradeoffs. Never invent cryptography or fingerprint passwords,
bearer tokens, or payloads. A permitted `session_audit_ref` or
`token_record_ref` is separately allocated, non-authenticating, non-reversible
to credential material, policy-approved, and distinct from the application's
actual token/session ID, JWT ID, hash, or fingerprint. Use it only where
correlation is essential; otherwise omit. Calling a credential or credential
derivative a "reference" does not make it permissible.

The never-log rules in the shared instruction apply before queues, local files,
stdout, collector export, retries, and error handlers. Audit automatic
instrumentation too. Encryption at rest does not make collecting unnecessary
secrets safe. Health messages must contain fixed codes and counts, not the event
that failed serialization.

## Four separate classifications

| Dimension | Example | Meaning |
| --- | --- | --- |
| Wave priority | Wave 1 | Implement this gap early in this app |
| Logger severity | INFO | A successful operation occurred |
| Detection confidence | Low | A rule matched but malicious intent is uncertain |
| Audit obligation | Required | The policy requires this record's specified durability/retention |

Use the application's approved severity mapping. Record rationale and test
consumer behavior when introducing or changing levels. Preserve severity text
through transport adapters, and map numeric values explicitly between formats.
Keep required INFO events through production filters. Proposed mappings remain
pending until approved; implementation priority never sets a runtime level.

Detector-derived events additionally require `signal_provenance` from a
controlled set (client_report, server_control, trusted_provider, heuristic), an
approved detector ID/version, and confidence low/medium/high/unknown with
detector-specific documented meaning. Unknown confidence is not high confidence.
A client chooses neither trusted provenance nor severity. Consumer text says
reported or matched; these fields do not establish successful exploitation.

## Delivery and failure contract

For each event class, write down producer acceptance, queue admission, durable
persistence, collector acknowledgment, searchable storage, and alert delivery
separately. Specify at-most-once/at-least-once behavior as supported, stable
deduplication IDs, retry limits, out-of-order arrival, maximum delay, crash-loss
windows, and shutdown limits. Do not claim exactly-once from a local logger
call. Bind IDs to a trusted producer namespace established from authenticated
source/config, not just a producer name supplied in the event. Never reuse
client interaction/trace IDs as canonical event IDs. Deduplicate only identical
immutable producer records within that namespace, excluding explicitly defined
collector-added metadata from the comparison. Same-ID/different-record conflicts
must retain or quarantine both under a bounded, access-controlled policy and
raise a safe health signal; never silently keep only the first. Namespace and
collision tests are part of consumer verification.

Ordinary telemetry should not throw into business logic, wait indefinitely, or
re-log its own failure recursively. Keep queues and spools bounded, with safe
permissions and capacity reserved away from critical application storage.
Publish bounded counters for failures, drops, queue age, and lag; use an
independent monitor for silence. A metric that traverses the same failed
collector is not independent.

Required audit needs a policy-backed durability boundary. Preserve an existing
transactional outbox or equivalent mechanism where present. A transactional
record can cover committed changes but a rejected transaction must not erase
evidence of a denied attempt; give those attempts an appropriate separate path.
Adding an outbox, blocking, fail-closed behavior, or a new loss policy changes
application semantics and needs an explicit design decision. Do not promise
unbounded durable retention in a bounded buffer. Required audit cannot be
sampled or silently aggregated away. Dedupe identical retransmissions only, not
distinct repeated security actions.

Optional event aggregation needs a documented eligible event set, bounded
grouping state, window start/end, counts, and visible losses. Preserve
rare/high-impact records and isolate noisy tenants. Neither a sample nor an
aggregate is a complete individual audit trail.

## Storage and use

Use authenticated secure transport and a separately controlled destination where
available. Separate producer write access from query, retention, and delete
privileges. Restrict tenant-scoped reads in the storage/query authorization
layer, not merely a dashboard filter. Monitor reads/exports/admin changes
without recursively auditing each audit write. Review temporary spools,
replicas, backups, extracts, and dead-letter queues under the same data policy.

Set retention, residency, disposal, and legal-hold handling with the appropriate
owners. Use established append-only/immutable facilities where needed, and
verify producer correctness separately. Apply context-appropriate encoding to
viewers and exports, and
parameterize query operations. Diagnostic enrichment must be approved,
time-limited, audited, and unable to bypass the allowlist or required audit.

Alerts, tickets, chat, email, and paging are additional data destinations.
Define a per-destination field allowlist, access/retention policy, tenant-safe
deep links, and rendering tests. Do not forward whole events by default. A link
to protected evidence still needs authorization at access time and must not
carry credentials in its URL.

## Historical identity and field ownership

Record how actor, target, and tenant references remain unambiguous across
identity issuers, tenants, account deletion, and account recreation. Use
existing stable identifiers with issuer/tenant qualification where necessary; an
equal provider-local ID must not silently merge unrelated identities. Do not
invent new personal-data retention or retain deleted profiles to preserve
attribution. When historical attribution is limited, document that limit and its
evidence.

Define which producer, collector, and consumer owns each envelope field.
Optional context, exporter attributes, aliases, case folding, and normalization
must not silently overwrite event, actor, severity, outcome, or tenant identity.
Test duplicate keys and normalized-name collisions across actual adapters.
Reject or quarantine conflicting records visibly under the approved failure
policy; keep required audit and consumer compatibility intact rather than
guessing a winner.
