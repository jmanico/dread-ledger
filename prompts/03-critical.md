# Wave 1 — critical coverage gaps

Paste the [shared instruction](00-shared-instruction.md) first.

```text
Apply the shared instruction (00-shared-instruction.md). Verify Wave 0 before
edits. Wave 1 means critical implementation priority, not CRITICAL logger level.
Select the highest-impact missing evidence in this application; implement a
small batch only.

Use reference/security-events.md to review privilege and policy changes,
sensitive data, key-management changes, platform administration, repository and
deployment controls, and high-impact agent or response actions. Include existing
response outcomes without authorizing containment or remediation in this pass.

Review the assessment's highest-impact gaps before selecting a batch. Consider
account takeover, cross-tenant access, privileged misuse, sensitive-data loss,
and loss of monitoring evidence. Promote consequential gaps from later waves;
record an owner and rationale for deferrals or unavailable signals. Preserve
approved runtime severity mappings and existing detection/blocking behavior.

Trace privileged actions, role/permission changes, tenant administration,
service-token creation/revocation, key-management actions, break-glass use,
security configuration changes, monitoring changes, bulk export, destructive
sensitive-data operations, and sensitive reads where high impact. Promote
authentication here if identity compromise dominates the threat. Instrument only
features actually present. Include service accounts and trusted admins.
Inventory all privileged-account activity, including routine operations and
denials, not only changes to roles or configuration. Use bounded action
categories and approved context; preserve unresolved coverage in the ledger.

Use the application's established event names and document new names with their
exact triggers. Preserve consumer mappings. Distinguish credential issuance,
revocation, and deletion, and monitoring configuration from verified delivery.
Keep actor, impersonator, target, and tenant distinct. Use allowlisted operation
and permission identifiers, never before/after object dumps, credential values,
or export contents. A token_record_ref must meet the shared instruction's
separate-surrogate rules; otherwise omit it. Never reuse a credential, actual
token ID, or credential derivative.

Locate the authoritative decision and commit points. Separate attempts/denials
from committed changes; transaction rollback must not produce a success claim.
Define deduplication and crash windows. If durable audit and transaction
consistency require a design change, document it and defer
instrumentation/rollout for that event until policy is established; do not
silently add remote blocking to authorization or a transaction. Capture failures
safely.

For every event add a ledger row, synthetic success and denial/rollback
fixtures, and an investigation query or detection acceptance case. Verify
trusted actor/target, tenant isolation, secret exclusion, retries/duplicates,
sink failure, and outcome accuracy. Where existing automation does not expose a
signal, record a coverage gap instead of inventing an event. Do not alter
privilege or access-control decisions.

Return implemented/deferred rows and evidence. Run the verification and rollout
prompt for this batch. Keep the next wave separate.
```
