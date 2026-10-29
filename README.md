<p align="center"><img src="logo.svg" alt="Dread Ledger" width="120" height="120"></p>
<h1 align="center">Dread Ledger</h1>
<p align="center"><strong>Leave the evidence. Bury the secrets.</strong><br>Security logging prompts for AI coding agents.</p>

Add security logging to an existing application in small, verified waves.
Inspired by [Trim Reaper](https://github.com/jmanico/trim-reaper) and
[Grim Prompter](https://github.com/jmanico/grim-prompter).

## Use the prompts

1. Open your application in a coding agent.
2. Paste the [shared instruction](prompts/00-shared-instruction.md), then the
   [assessment prompt](prompts/01-assess.md). Identify the service to review.
3. Run the foundation prompt, then one bounded wave at a time. Verify each
   change and keep the resulting ledger for your next session.

For file-based use, give the agent this checkout's path and the selected prompt.
Resolve library references here and make changes in the application checkout.
For clipboard use, include the [security event checklist](reference/security-events.md)
with the shared instruction and assessment prompt. Assessment reviews all 90
items, then adds requirements specific to the application.

| Pass | Purpose | Prompt |
| --- | --- | --- |
| Assess | Inventory code, controls, consumers, and evidence gaps | [01 · Assess](prompts/01-assess.md) |
| Wave 0 · Foundation | Safe schema, existing logger integration, privacy, bounded delivery | [02 · Foundation](prompts/02-foundation.md) |
| Wave 1 · Critical gaps | Privileged actions, sensitive operations, monitoring tampering | [03 · Critical](prompts/03-critical.md) |
| Wave 2 · High gaps | Authentication, authorization, recovery, and sessions | [04 · High](prompts/04-high.md) |
| Wave 3 · Medium gaps | Validation, abuse controls, uploads, and workflow failures | [05 · Medium](prompts/05-medium.md) |
| Wave 4 · Lower-priority context | Useful lifecycle and investigation context | [06 · Context](prompts/06-context.md) |
| Every wave | Adversarial tests, consumer checks, canary and rollback plan | [07 · Verify and roll out](prompts/07-verify-and-rollout.md) |
| Focused repair | Existing logs leak data, inject records, or exhaust resources | [08 · Repair](prompts/08-repair.md) |
| Ongoing | Review a diff for lost coverage or schema drift | [09 · Change review](prompts/09-change-review.md) |

Wave priority reflects the consequences of a coverage gap, not the event's
logger level. Reorder waves for your application's risks; establish the safe
foundation first. Keep deployment separate from local implementation and
report checks not run.

## Supporting references

- [Runbook](runbook.md): scope, gates, and a reusable private ledger.
- [Security event checklist](reference/security-events.md): 90 review items
  spanning identity, data, infrastructure, delivery, AI agents, and audit health.
- [Coverage](reference/coverage.md): application-specific inventory and evidence
  requirements.
- [Event contract](reference/event-contract.md): privacy, trusted fields,
  compatibility, and delivery semantics.
- [Verification](reference/verification.md): application-specific safety checks.

## About the author

Created by Jim Manico of [manicode.ai](https://manicode.ai) and
[Manicode Security](https://manicode.com).

For teams looking to guide secure coding from the start,
[manicode.ai](https://manicode.ai) offers commercial secure-coding prompts for AI
assistants, designed to reduce avoidable security rework and the time and tokens
spent on it.

## License

Dread Ledger's original prompts and documentation are licensed under the
[MIT License](LICENSE). Copyright (c) 2026 Jim Manico.
