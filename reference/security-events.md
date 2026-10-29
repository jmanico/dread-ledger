# Security event checklist

Assess every item for the selected application boundary using the
[coverage rules](coverage.md). IDs are stable review references, not runtime
event names or severity levels. Preserve existing application names.

Record one summary disposition per ID, with evidence, owner, and next action.
Split applicable subcases into linked event rows; an item is covered only when
all applicable subcases pass verification at the stated boundary. Add
application-specific requirements beyond this list. Keep IDs stable when the
list grows; never reuse a retired ID for a different requirement.

Use existing controls and authoritative signals. A missing detector or provider
feed is unavailable_signal, not not_applicable. Infrastructure or provider-owned
items need an owner and evidence boundary; unavailable access does not authorize
new collection or imply absence. The checklist does not authorize production
access, new detectors, changed enforcement, or broader data collection.

All items follow the shared privacy rules. Location/device/network context needs
an approved purpose, minimum useful precision, and trusted provenance. Record
changes to recovery channels or ownership without copying contact values.
Credential references must be separately allocated non-authenticating audit
surrogates under the event contract; never actual keys, session IDs, token IDs,
hashes, or fingerprints. Use safe rule/resource references instead of raw
commands, queries, URLs, tool content, or rejected payloads. Record disclosure
signals and affected data categories, never the disclosed content.

## Authentication and identity

- **SEC-001:** Authentication successes and failures, including interactive
  logins, API clients, service accounts, and workload identities.
- **SEC-002:** Successful authentication following repeated failures, account
  lockout, or a recent credential reset.
- **SEC-003:** Password spraying, credential stuffing, brute-force attempts, and
  account enumeration detections.
- **SEC-004:** Account lockouts, unlocks, suspensions, reactivations, and
  attempts to use disabled accounts.
- **SEC-005:** Password changes, reset requests, reset completions, and failed
  recovery attempts.
- **SEC-006:** MFA challenges, approvals, denials, timeouts, repeated push
  requests, and suspected MFA fatigue.
- **SEC-007:** MFA enrollment, removal, replacement, recovery-code use, and
  authentication-strength downgrades.
- **SEC-008:** Passkey or security-key registration, removal, and verification
  failures.
- **SEC-009:** Changes to recovery email addresses, telephone numbers, trusted
  devices, or account ownership.
- **SEC-010:** Authentication using emergency, default, shared, dormant, or
  unexpected service accounts.
- **SEC-011:** Impossible-travel and atypical-travel detections, including the
  supporting timestamps, locations, and known VPN or proxy context.
- **SEC-012:** Sign-ins from unfamiliar devices, networks, countries,
  anonymizing services, or sources associated with malicious activity.
- **SEC-013:** Suspicious concurrent sessions, abrupt session-location changes,
  and anomalous token use.
- **SEC-014:** Suspected adversary-in-the-middle phishing, stolen session
  cookies, and compromised credentials.

## Authorization and privilege

- **SEC-015:** Authorization failures involving objects, records, files,
  functions, administrative interfaces, or protected fields.
- **SEC-016:** Cross-tenant access attempts and tenant-boundary enforcement
  failures.
- **SEC-017:** Attempts to access another user's resources through manipulated
  identifiers or ownership fields.
- **SEC-018:** Privilege-escalation attempts and successful elevation, including
  temporary privilege grants and expiration.
- **SEC-019:** User, group, role, permission, resource-owner, and
  delegated-access changes.
- **SEC-020:** Administrative impersonation, support access, emergency access,
  and actions performed during those sessions.
- **SEC-021:** Authorization-policy changes, policy-evaluation errors, and
  fail-open behavior.
- **SEC-022:** Access that succeeds despite an expected denial, revoked
  entitlement, or expired privilege.

## Sessions, credentials, and federation

- **SEC-023:** Session creation, renewal, expiration, logout, revocation, and
  failed invalidation.
- **SEC-024:** Suspected session fixation, session hijacking, and use of revoked
  sessions.
- **SEC-025:** Token and API-key issuance, rotation, revocation, and permission
  changes, recording identifiers and scope rather than secret values.
- **SEC-026:** Token validation failures involving signatures, issuers,
  audiences, expiration, or required claims.
- **SEC-027:** Authorization-code replay, refresh-token reuse, and detected
  access-token replay.
- **SEC-028:** OAuth redirect-URI, state, nonce, PKCE, and sender-binding
  validation failures.
- **SEC-029:** OAuth application registration, consent grants, scope expansion,
  and grant revocation.
- **SEC-030:** SSO federation, identity-provider, signing-key, and
  trust-configuration changes.

## Validation, abuse, and resource controls

- **SEC-031:** Security-relevant input-validation failures, including invalid
  encodings, unexpected fields, prohibited values, and schema violations.
- **SEC-032:** Suspected SQL, NoSQL, command, template, LDAP, and other
  injection attempts.
- **SEC-033:** Suspected cross-site scripting, path traversal, file inclusion,
  and unsafe deserialization.
- **SEC-034:** CSRF validation failures and rejected cross-origin requests.
- **SEC-035:** Content Security Policy violations, with enforcement mode and
  sanitized report metadata.
- **SEC-036:** SSRF detections and blocked requests to internal services, cloud
  metadata endpoints, or prohibited destinations.
- **SEC-037:** Unexpected HTTP methods, method-override attempts, malformed
  requests, and request-smuggling detections.
- **SEC-038:** File-upload policy violations, malware detections, executable
  uploads, archive traversal, and decompression-limit violations.
- **SEC-039:** Endpoint scanning, object enumeration, forced browsing, and
  abnormal concentrations of missing-resource requests.
- **SEC-040:** Rate-limit, concurrency-limit, request-size, query-complexity,
  and resource-budget violations.

## Sensitive data and storage

- **SEC-041:** Sensitive-data access, including successful reads, searches,
  downloads, exports, and denied attempts.
- **SEC-042:** Bulk retrieval, unusually broad queries, rapid record
  enumeration, and abnormal download volumes.
- **SEC-043:** Sensitive-data creation, modification, deletion, restoration, and
  ownership changes.
- **SEC-044:** External sharing, public-link creation, access-control changes,
  and newly public storage.
- **SEC-045:** DLP detections, attempted secret disclosure, and transfers to
  unapproved destinations.
- **SEC-046:** Database permission changes, audit-setting changes, and
  privileged administrative queries.
- **SEC-047:** Backup and snapshot creation, access, export, sharing, deletion,
  and restoration.
- **SEC-048:** Suspected data staging, unusual archive creation, mass
  encryption, and destructive deletion patterns.

## Business workflows and transactions

- **SEC-049:** Business-workflow violations, including skipped approvals,
  invalid state transitions, and separation-of-duties failures.
- **SEC-050:** Transaction replay, duplicate execution, idempotency violations,
  and suspected race-condition exploitation.
- **SEC-051:** Suspicious changes to payment destinations, beneficiaries,
  refunds, discounts, or transaction limits.
- **SEC-052:** High-impact actions, recording initiation, authorization,
  approval, execution outcome, and reversal.
- **SEC-053:** Attempts to bypass fraud controls, transaction limits, or
  required secondary verification.

## Cryptography, secrets, and transport trust

- **SEC-054:** Cryptographic-operation failures, including encryption,
  decryption, signing, signature verification, and authenticated-integrity
  checks.
- **SEC-055:** Cryptographic-key creation, import, export, rotation, disabling,
  scheduled deletion, and destruction.
- **SEC-056:** Key-management permission changes and unusual or denied key use.
- **SEC-057:** Secret-store access, secret updates, rotation failures, and
  unexpected retrieval bursts.
- **SEC-058:** TLS handshake failures, certificate validation failures, hostname
  mismatches, and rejected client certificates.
- **SEC-059:** Certificate issuance, renewal, revocation, expiration, and
  trust-store changes.
- **SEC-060:** Attempts to enable weak cryptography, downgrade protocols, or
  bypass certificate verification.
- **SEC-061:** Cryptographic random-number-generator failures and detected nonce
  or IV reuse.

## Platform, network, and workload operations

- **SEC-062:** Security-control changes, including disabling authentication,
  authorization, encryption, filtering, or endpoint protection.
- **SEC-063:** Cloud control-plane operations, including administrative reads,
  writes, resource creation, and deletion.
- **SEC-064:** Firewall, security-group, routing, DNS, ingress, egress, and
  remote-access configuration changes.
- **SEC-065:** Unexpected outbound connections, suspicious DNS activity,
  command-and-control detections, and lateral-movement indicators.
- **SEC-066:** Process creation, script execution, scheduled-task creation,
  service installation, and unusual parent-child process relationships.
- **SEC-067:** Unexpected use of administrative utilities, credential-dumping
  tools, remote shells, or persistence mechanisms.
- **SEC-068:** Security-relevant startup, shutdown, restart, crash, and
  resource-exhaustion events.
- **SEC-069:** Container and Kubernetes administrative activity, including
  privileged workload creation, role-binding changes, secret access, interactive
  execution, and port forwarding.
- **SEC-070:** Admission-policy denials, unauthorized image deployments, and
  changes that weaken workload isolation.

## Repository, build, and deployment

- **SEC-071:** Repository security changes, including visibility, ownership,
  collaborator access, branch protection, and required-review settings.
- **SEC-072:** CI/CD workflow changes, runner registration, deployment
  approvals, and production deployments.
- **SEC-073:** Security-check bypasses, secret-scanning bypasses, and
  vulnerability-alert dismissals.
- **SEC-074:** Build-artifact signature failures, provenance-verification
  failures, and unexpected dependency or package-source changes.

## AI agents and tool integrations

- **SEC-075:** AI prompt-injection detections, distinguishing suspected
  instructions from confirmed unauthorized actions.
- **SEC-076:** Agent tool-call requests, authorization decisions, approval
  references, execution outcomes, and policy versions.
- **SEC-077:** Attempts by agents to exceed delegated privileges, bypass
  approvals, or access another tenant's data.
- **SEC-078:** Unapproved model, tool, MCP server, connector, or
  external-provider use.
- **SEC-079:** Tool-definition changes, integrity-check failures, and suspected
  tool or retrieved-content poisoning.
- **SEC-080:** Agent memory changes, suspected memory poisoning, and cross-user
  context leakage.
- **SEC-081:** Sensitive-data disclosure through model output, retrieval
  results, tool arguments, or external requests.
- **SEC-082:** Agent sandbox violations, prohibited network access, and
  unexpected subprocess execution.
- **SEC-083:** Token-budget overruns, excessive tool calls, recursive
  delegation, repeated retries, and abnormal spending.

## Audit pipeline and detection configuration

- **SEC-084:** Audit-log access, export, deletion, clearing, modification, and
  integrity-verification failures.
- **SEC-085:** Logging-agent shutdowns, configuration changes, destination
  changes, and reduced audit coverage.
- **SEC-086:** Missing telemetry, ingestion failures, dropped events, full
  buffers, storage exhaustion, and unusual collection delays.
- **SEC-087:** Clock changes, synchronization failures, and timestamp anomalies
  that undermine event correlation.
- **SEC-088:** Changes to detection rules, alert suppression, retention periods,
  or log-storage permissions.
- **SEC-089:** Log-injection attempts and failures to redact credentials or
  sensitive information.

## Detection and response

- **SEC-090:** Detection and response actions, including alerts raised, accounts
  contained, sessions revoked, workloads isolated, and remediation failures.

## Requirements for every event

- Record event and ingestion times, event type, actor or workload identity,
  tenant, target, action, outcome, reason, source, correlation identifier, and
  applicable policy or rule. Define each field's trusted origin and purpose.
  The producer records event time; the receiving component records ingestion
  time. Preserve both without inventing unavailable timestamps. Document safe
  omissions when identity, tenant, target, correlation, or policy is unknown or
  inapplicable. Never manufacture identity or add unnecessary personal data.
- For inferred threats, record detection confidence and supporting event
  references. Distinguish suspicious behavior, blocked attempts, successful
  actions, and confirmed compromise. References must respect access and tenant
  boundaries; retain sanitized evidence rather than raw attack content.
- Exclude secrets and unnecessary sensitive content: passwords, bearer tokens,
  session cookies, private keys, raw sensitive payloads, and unredacted prompts
  or tool output. The shared instruction's full exclusions apply to every
  destination, including telemetry and alerting about a disclosure.
