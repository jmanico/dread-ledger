# Wave 3 — validation, abuse, and workflow signals

Paste the [shared instruction](00-shared-instruction.md) first.

```text
Apply the shared instruction (00-shared-instruction.md). Verify Wave 0 before
edits. Wave 3 means medium implementation priority by default; promote
consequential gaps. Instrument existing controls and validators rather than
creating new attack detection.

Use reference/security-events.md for validation, abuse, resource controls,
business workflows, cryptographic failures, and AI/tool signals. Include replay
and idempotency failures, approval bypass, supply-chain verification failures,
and existing fraud/control detections; promote high-impact gaps as needed.

Inspect input/output validation, rate limits, suspicious session limits, upload
scan and processing results, CSRF/CSP controls, cryptographic failures, webhook
verification, and business workflow sequence checks. Use actual signals; a 404
or unusual user agent alone does not establish malicious intent. Client CSP
reports and other untrusted reports are claims with limited confidence, not
authenticated user evidence. Record controlled signal provenance
(client_report/server_control/trusted_provider/heuristic), approved detector
ID/version, and documented low/medium/high/unknown confidence. Consumers must
describe a report or match, not confirmed exploitation.

Use established application event names with precise control outcomes. Record
cryptographic operation failures without key material or plaintext. For workflow
sequence warnings, record the action's actual outcome whether or not the
existing control rejected it; do not add enforcement for logging.

Assess existing repeated-not-found, unexpected-field, tool-signature, origin,
and object-access signals. Use fixed field categories and approved rule IDs,
never submitted values. A claimed user agent is spoofable. Origin-policy
rejections do not establish unauthorized access or replace authorization/CSRF
controls. Preserve object-access denial evidence and avoid duplicate emission
when an existing access-control event already captures the same decision.

For AI and tool integrations, inspect existing injection, resource-limit, and
tool-integrity signals. Record approved tool/server IDs, bounded usage counts,
rule/version, and actual control outcomes. Keep prompts, tool content, inputs,
outputs, and signatures excluded. Do not introduce blocking or quarantine
policy. Distinguish absent functionality from a relevant but unavailable
detector.

Do not conflate ordinary validation failure with proven malicious behavior.
Exercise benign client mistakes, spoofed tool claims, rejected origins, and
object denials as applicable. SQLi and CSRF logging preserve existing primary
prevention controls; CSP reports remain untrusted and payload-free.

Log bounded allowlisted field/rule IDs, result enums, and non-secret object
references. For attacker-invented field names use a fixed unknown_field marker
and bounded counts. Never log rejected values, raw URLs, filenames, uploaded
content, SQL, prompts, tool arguments/results, webhook bodies, signatures, or
crypto material. Do not hash these payloads as a workaround. Distinguish scan
failed, scan unavailable, and scan passed. Document severity for each outcome
under the application's policy and preserve failure visibility.

Model attacker-generated event volume. Bound state used for counters and
aggregation; attacker-controlled keys must not exhaust memory or metric
cardinality. Required audit cannot be sampled away. For policy-eligible optional
signals, aggregation needs explicit counts, windows, group semantics, and
visible loss accounting; protect rare/high-impact signals from a noisy tenant.
Test bursts without live attacks or production traffic.

Test legitimate mistakes and client bugs as well as synthetic rejected inputs;
prove unchanged validation, CSRF, upload quarantine, cryptography, and
rate-limit decisions. Verify the safe event survives malicious optional fields
and does not forge a record. Return ledger, false-positive cases, volume
evidence, and gaps. Run verification next.
```
