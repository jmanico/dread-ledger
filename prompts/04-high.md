# Wave 2 — authentication, authorization, and sessions

Paste the [shared instruction](00-shared-instruction.md) first.

```text
Apply the shared instruction (00-shared-instruction.md). Verify Wave 0 before
edits. Wave 2 is high implementation priority, not a log-level setting. Retain
or promote these events into Wave 1 wherever identity/access risks make them
critical.

Reconcile the identity, authorization, session, credential, and federation items
in reference/security-events.md. Include passkeys, recovery-channel changes, MFA
lifecycle, OAuth consent and validation, federation trust changes, and existing
stolen-credential or session-risk signals.

Trace actual local and delegated login flows, credential checks, MFA/recovery,
password changes, token lifecycle, authorization denials, impersonation, logout,
and session expiry/renewal. Include machine identities, jobs, APIs, and external
provider gaps. Log successful and failed authentication, not failures alone.
Avoid duplicating framework/provider events without a reason and shared
correlation design.

Use stable application names for the actual authentication, account-lock,
credential-change, session, and access-control outcomes. Distinguish ordinary
credential use from presentation of a revoked credential, and user-requested
session extension from automatic renewal. Correlated failure bursts or login
after failures require existing safe correlation and counters; do not introduce
identity joins or detection state for logging.

For existing identity-risk signals, retain provider provenance, rule/version,
confidence, and approved coarse location context only. Do not introduce location
collection or a new risk engine. Relevant unavailable signals remain gaps.

Record expired-session use only when authoritative validation or existing state
establishes prior validity and expiry. Unknown or forged credentials do not
establish expiry. Keep logout, revocation, and expiration distinct; never retain
credentials or change session retention, destruction, or reauthentication policy
to create evidence.

Source authenticated IDs from the verified security context. Failed login may
have no authenticated actor; do not promote a submitted username to verified
identity or look up accounts just to enrich a log. Use generic failure reasons
and policy-approved non-secret correlation. No credentials, JWT claims dumps,
raw tokens, session IDs, email addresses, MFA secrets, or recovery links. Do not
change enumeration resistance, HTTP responses, timing protections, session
lifecycle, lockouts, or authorization.

Keep required security events independent of debug levels and trace sampling.
Test unknown account, wrong secret, success after failures, rejected
MFA/recovery, expiry, revocation, logout, permission denial, and concurrent
requests in relevant flows. Only include cases supported by the actual
application. Verify delegated-provider coverage claims against available config;
unavailable provider evidence stays unknown.

Add queries/fixtures for relevant failure bursts and success after failures.
Define windows, grouping, threshold ownership, and benign controls; do not
invent universal thresholds, production paging, account blocking, or an
impossible-travel detector. Test required events under a failed sink/full queue
according to established policy. Return ledger and checks, then run the
verification and rollout prompt.
```
