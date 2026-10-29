# Assess before adding events

Paste the [shared instruction](00-shared-instruction.md) first.

```text
Assess this application using the shared instruction (00-shared-instruction.md).
Do not modify application code, dependencies, or configuration. Write an
assessment only in the agreed report location. Inspect before choosing checks;
run only relevant non-production baseline checks already authorized by the task.

Map entry points, authentication/authorization decisions, privileged operations,
sensitive data access/export, background jobs, management commands, consoles,
migrations, operations scripts, external identity providers, and tenant
boundaries to actual files and symbols. Inventory existing logging calls,
framework middleware, automatic request/exception capture, collector transforms,
transports, sinks, filters, trace sampling, retention, access controls,
consumers, and alerts. Distinguish missing evidence from confirmed missing
logging. Do not read real logs.

Build an event ledger: existing trigger and coverage; gap; existing or proposed
application event name; safe context; priority and rationale; privacy/cost risk;
consumer and owner; verification plan. Check whether INFO security events
survive production filters. Identify secrets or injection exposure in existing
logging first. Do not print discovered values; cite the code path and data
category only.

Build the inventory from the selected application's security requirements,
features, decision points, and investigation needs using reference/coverage.md
when available. Review all wave categories, including absent or uninspected
features; do not limit assessment to existing log calls. Include authentication,
sessions, authorization, privileged actions, sensitive data, validation, abuse
signals, integrations, and operational health. Record scope and uninspected
areas. Give each candidate event a trigger, stable application name, and
covered, missing, not_applicable, or unavailable_signal disposition with
evidence. For each gap record owner, next action, proposed wave, and needed
decisions. Prioritize by application risk and justify deferrals. Assess response
ownership, timestamps, field/privacy choices, error capture, and exclusions.

Read reference/security-events.md and reconcile every SEC ID, not only events
already found in code. Review all applicable subcases, including successful,
denied, failed, and reversed outcomes where listed. Record one summary status
per ID and link detailed event rows as needed. Apply the checklist's metadata,
inferred-threat, and exclusion rules. Name provider/platform owners and missing
evidence rather than creating collectors or assuming coverage. If the checklist
is unavailable, mark reconciliation NOT RUN and request it; do not claim a
complete assessment.

Propose Wave 0 and critical/high/medium/lower-priority groups tailored to this
system. Promote authentication or sensitive reads when their risk warrants it.
Identify required audit and its existing durability/failure policy. Ask for
unresolved policy decisions without guessing. Distinguish app emission from
collector, sink, and alert evidence.

Use the runbook ledger format if available. For clipboard-only use, emit a
single inventory table with columns Event, Status, Evidence, Owner, Next, one
summary row per checklist ID plus linked event rows where needed. Evidence
points to code/configuration and check results, with boundary and uncertainty; a
log call alone does not establish coverage. Record target revision, library
revision, scope, local/deployment gate status, decisions, and next pass above
the table. Keep detailed contracts and check results in named sections below it.
Do not include raw logs or secrets.

Return a bounded first change, baseline results, event ledger, known limits, and
the minimum missing decisions. Stop at assessment; do not implement the plan.
```
