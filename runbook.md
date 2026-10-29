# Runbook

## Start a pass

Work in the application checkout. Select one service or security boundary and a
small batch of events. Read the [shared instruction](prompts/00-shared-instruction.md)
before every pass, including resumed sessions.

Assessment produces a report only. Implementation passes permit scoped local
changes and relevant non-production tests; inspect commands for external side
effects first. Ask only for missing consequential decisions, respecting existing
authorization. Deployment remains separate.

Return reports inline unless an approved private location is supplied. Before
saving inside the target checkout, verify that location is excluded from version
control. Keep operational details out of this library and redact reports before
sharing. Commit a sanitized report only under the target owner's explicit policy.

## Gates

| Gate | Evidence needed |
| --- | --- |
| Scope | Inspected paths, existing coverage and consumers, risks, exclusions, baseline results |
| Local foundation | Safe encoding, allowlists and bounds, trusted context, explicit failure policy, real local capture, applicable isolation/failure tests |
| Each wave | Selected ledger rows linked to code and passing contract/verification tests; existing coverage retained |
| Deployment readiness | Actual transport and storage controls, retention and tenant isolation, consumer/alert delivery, independent health, owner, measurable canary thresholds, safe rollback |

Mark each gate PASS, FAIL, or NOT RUN with evidence. A failed local foundation
requires Wave 0 before coverage work. Missing infrastructure can block deployment
while verified local work continues. Mock assertions do not establish delivery;
an unresolved prerequisite prevents its gate from passing.

## Priority and policy

Rank gaps by affected assets, plausible abuse, exposure, audit obligations, and
missing investigation evidence. Review highest-risk gaps first and explain
deferrals. Reorder waves for application risk; monitoring health belongs in Wave
0. Wave order, runtime severity, and audit obligation are separate.

Preserve required audit, baseline authentication, privileged-action, and denial
events even when frequent. Capacity problems need an explicit policy/design
decision. Use established infrastructure; do not add cryptography, detectors, or
a telemetry stack to satisfy the inventory. Verify producer correctness
separately from storage protection.

New destinations, personal-data collection, retention/legal-hold changes,
audit-related transaction changes, and production rollout require an established
owner decision. When policy is missing, propose options with costs and failure
semantics; continue unaffected work.

## Ledger and handoff format

Maintain one private ledger per application boundary and preserve prior
versions. Use the [coverage guide](reference/coverage.md) to account for every
candidate event in the assessed boundary, including existing and proposed
events. Use covered, missing, not_applicable, or unavailable_signal with their
defined evidence requirements. Unknown applicability or missing
detector/provider access remains unavailable_signal. Full coverage requires
every applicable row to be verified at the claimed boundary; a bounded wave may
finish with assigned gaps.

Include one summary row per [checklist ID](reference/security-events.md), with
linked event subrows when needed. Use the Event column for the SEC ID or an
application event reference. Record the checklist's library revision and local
additions. A compound summary can pass only when all applicable subcases pass;
keep partial results and unavailable evidence visible. Apply the
[summary precedence](reference/coverage.md#checklist-accounting): known gaps,
then unavailable evidence, then covered or evidenced not_applicable. Reconcile
the complete checklist at assessment and full-wave verification; repair-only
verification uses the exception below.

Use this layout. Inventory cells reference evidence sections; escape literal
pipes in Markdown tables. Expand contracts only for selected or covered events.

```markdown
Target revision:
Library revision:
Scope:
Gate local:
Gate deployment:

| Event | Status | Evidence | Owner | Next |
| --- | --- | --- | --- | --- |

## Contracts

## Checks

## Decisions and blockers

## Handoff
```

- **Metadata:** exact commits or identifiable working-tree snapshots, inspected
  scope and gate results with evidence references.
- **Inventory:** evidence, owner, and next action for each gap. Covered rows
  require an owner; unresolved ownership needs an explicit assignment action.
- **Contracts:** trigger/location, local mapping/version, runtime
  severity, wave, purpose, field types/trust/limits, identity provenance,
  privacy/retention, delivery/failure policy, correlation, consumer, and owner.
- **Checks:** commands, revisions, synthetic fixture categories, and results.
  Separate emitter, collector, storage, query, alert, and production-policy
  evidence. Explain NOT RUN and inapplicable checks. Record measured
  latency/volume/cost where available.
- **Decisions and blockers:** existing policy, missing decisions/infrastructure,
  owner, alternatives, and consequences of deferral.
- **Handoff:** changed rows/files, gate results, gaps by implementation priority
  and status (highest-risk first), assumptions, missing access, next pass, and
  rollback.

## Resume work

Compare the current target revision/diff and configuration with the ledger.
Reuse unchanged evidence at its original revision; do not label it newly run.
Revalidate rows affected by logger/schema/filter, identity/tenant, policy,
transport, collector, consumer, or event-mapping changes. Shared changes can
invalidate many rows. Explain why unaffected evidence remains valid.

Downgrade stale covered rows to missing (unverified), or unavailable_signal when
access/signals are missing. Revisit not_applicable when architecture changes.

An urgent repair can precede assessment. Use prompt 07's repair-only mode after
prompt 08: verify the repaired paths and affected consumers, update affected
ledger rows if present, and record "ledger not yet established" otherwise. Mark
full checklist reconciliation NOT RUN and assessment as the next pass. Preserve
local safety checks and safe rollback; do not add new coverage or infer a passing
foundation/deployment gate. A change review without a baseline ledger reports
that limitation rather than reconstructing prior coverage.
