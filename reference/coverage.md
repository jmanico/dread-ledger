# Application coverage

Build the inventory from the reviewed application's requirements, features,
security decisions, and investigation needs. Record the boundary, inspected
paths, and areas that could not be inspected. Review each wave's categories,
even when no related log call exists. An inventory derived only from current
logs will miss absent evidence.

## Checklist accounting

Use the [security event checklist](security-events.md) for every assessment.
Record one summary row per SEC ID, including absent or uninspectable areas, and
link it to the specific application events and requirements it covers. Add local
requirements beyond the checklist. An ID is a review reference, not an event
name or a prescribed logger level.

For compound items, retain each subcase's evidence and status, then choose the
summary in this order:

1. **missing** if any subcase has a known implementation or verification gap.
2. **unavailable_signal** if none is missing but any subcase has uncertain
   applicability, missing access, or an unavailable required signal.
3. **covered** if at least one subcase applies and every applicable subcase is
   verified; the rest must be evidenced not_applicable.
4. **not_applicable** only when every subcase is evidenced not_applicable.

An empty or unassessed item is unavailable_signal. Preserve unknown subcases
and their next actions even when a known gap makes the summary missing. A failed
or unrun check with available inputs is missing; unavailable inputs or access
are unavailable_signal. Shared events may support multiple IDs only with an
explicit semantic mapping; do not emit duplicates.

Use the same four dispositions below for summaries and event rows. Out-of-scope
provider/platform access is a named limitation or unavailable_signal when
relevant, not proof of non-applicability. If the checklist is unavailable,
continue bounded analysis but mark checklist reconciliation NOT RUN and request
the missing reference. Never claim checklist completeness without it.

## Find candidate events

Follow entry points through authentication, authorization, state changes, jobs,
and integrations. Include successful operations, denials, failures, and changes
to security controls. Check service accounts, administrative tools, background
workers, and external providers as well as user-facing requests.

Use these passes to organize the review:

| Pass | Questions to resolve |
| --- | --- |
| [Foundation](../prompts/02-foundation.md) | Can the existing logging path protect data, bound resource use, preserve business behavior, and make loss visible? |
| [Critical gaps](../prompts/03-critical.md) | What evidence is needed for privileged misuse, tenant-boundary violations, sensitive-data loss, and changes to security or monitoring? |
| [Identity and access](../prompts/04-high.md) | Can investigators distinguish authentication, credential, session, and access-control outcomes across local and delegated flows? |
| [Validation and abuse](../prompts/05-medium.md) | Which existing validators, limits, integrity checks, and detectors produce useful signals, and what do those signals actually establish? |
| [Context](../prompts/06-context.md) | Which account, data, upload, process, and job transitions answer a specific investigation question? |

Keep applicable gaps visible even when their implementation belongs in a later
wave. Rank them by plausible harm, exposure, audit obligations, and missing
investigation evidence. Explain deferrals and assign owners. Do not create new
detectors, collect new personal data, or change enforcement to complete a row.

## Name and classify events

Keep established event names and consumer behavior. Give new events stable names
in the application's namespace, with exact triggers and controlled outcomes.
Put approved context in fields rather than names. Record aliases and semantic
differences when preserving multiple formats. One event may satisfy several
requirements only when its evidence supports each; avoid duplicate emission.

Choose logger severity under the application's policy, independently of wave
priority and detection confidence. A detector match describes a signal, not
confirmed exploitation. Required audit follows its durability and retention
policy regardless of logger level.

## Track evidence

Give each candidate event one disposition in the private ledger:

- **covered:** the trigger, fields, owner, and consumer are documented, with
  passing verification at a named boundary. Separate emission, collection,
  storage, query, and alert results.
- **missing:** the event is needed but its implementation or verification is
  absent or incomplete. Name an owner and next action.
- **not_applicable:** the reviewed application lacks the relevant behavior.
  Cite evidence and state what architectural change would require reassessment.
- **unavailable_signal:** applicability is uncertain, inspection access is
  missing, or a needed detector/provider signal is unavailable. Name the missing
  evidence and the action needed to resolve it.

Missing detection is not evidence that a relevant risk is inapplicable. Do not
mark an event covered because its name appears in code. Preserve unresolved rows
across waves and revisit them when requirements or architecture change.

A completed assessment accounts for the reviewed scope and its limits. Claim
complete implementation only for an explicitly stated boundary whose applicable
events are verified. Report uninspected areas and outstanding gaps separately.
