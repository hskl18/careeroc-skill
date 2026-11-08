# Management contract

This contract specifies required behavior; it is not an implemented storage or delivery adapter.
Use it when staging, delivering, recovering, or updating job-search state.
Use the existing user-selected backend when it can enforce these invariants.
Ask for a backend choice before replacing real state or migrating records.

## Records and ownership

Keep these records distinguishable even if the backend stores them together:

- Source observations: source/tenant, full requisition ID, literal official URL, snapshot or content hash, observed times, completeness, and source health.
- Personal assessments: user, job identity, profile/preferences versions, eligibility, fit evidence, gaps, and decision/rule version.
- Pending recommendations: stable decision ID, verification evidence, review status, and unresolved delivery attempts.
- Delivery history: user, canonical job, recommendation year, timezone, first successful visibility time, channel receipts, and idempotency key.
- User outcomes: opened, saved, dismissed with reason, confirmed applied, interview, rejection, withdrawal, and offer, each with provenance and time.
- Verification retries: job identity, attempts, methods, first/last attempt, failure reason, next retry, expiry, and owner.

Use separate posting state `OPEN / CLOSED / UNKNOWN` and personal eligibility `ELIGIBLE / INELIGIBLE / UNKNOWN`.
Do not interpret a personal rejection as job closure or expose one user's assessment to another.

Assign ownership by operation: collection, publication, archive movement, and audit repair can have different authorized owners.
A collector stages but does not become the publisher merely because it can access the queue.
Human notes and manually chosen workflow states remain user-owned.

## Annual delivery boundary

Coordinate recommendation decisions through an atomic uniqueness boundary equivalent to:

```text
unique(user_id, canonical_job_id, recommendation_year)
```

Calculate the year from successful delivery time in the user's configured timezone and retain that timezone and the UTC timestamp.
Reserve a decision before external delivery so concurrent workers cannot create separate recommendations for the same key.
An unsuccessful reservation or draft is not a delivered recommendation.
Reuse the same decision and channel idempotency keys when recovering a pending delivery.
Mark delivered only after the feed becomes user-visible or an enabled channel confirms successful sending.
If the acknowledgment is unknown, preserve that state and reconcile it before sending again.
A database uniqueness constraint alone cannot establish exactly-once external sending.

One recommendation can have several channel receipts; channels share the same history and decision.
Do not generate another daily, weekly, or monthly recommendation because a different channel lacks a receipt.
Never set delivered merely while updating seen history or staging.

Treat company-and-role application cooldown as a separate configurable policy based on confirmed application time.
An opened link is not application confirmation or automatic permanent suppression.
Do not convert unknown historical delivery into false confirmed history during import.

## Checkpoints and recovery

Advance a source checkpoint only after a successful, complete parse and durable preservation of the observations and unresolved candidates it covers.
Check fetch, revision lookup, diff, and snapshot command exit status independently.
A valid old revision after a failed fetch is not a successful fresh check.
Do not turn an error into a successful empty result or close missing jobs after an incomplete fetch.
Preserve checkpoint and pending state on failure.

Use an owned token or backend transaction for bounded writes and release ownership in a finalizer.
Do not hold a root lock during browser work, dependency loading, rendering, or another unbounded operation.
Read-before-write duplicate checks without an atomic boundary do not protect concurrent writers.

Verify stored identities and material fields after publication, not just row count or first-column IDs.
Keep raw external text out of formula-enabled spreadsheet cells unless the adapter safely escapes it.
Do not consume pending rows or update delivery history if publication or readback fails.
Stop with an explicit error instead of printing failed validation and returning success.

Preserve unreadable or corrupt state for recovery; do not replace it with an empty ledger and start recommending again.
Use a backend-supported consistent backup and restore process before destructive state repair.

## Retry and quarantine

Use configurable retry limits, backoff, source budgets, and expiry.
Count distinct attempts and record first/last attempt times so retry thresholds are auditable.
Quarantine persistent verification failures while retaining identity, evidence, and failure reason.
Quarantine and expiry mean unverified, not closed or delivered.
Allow a later successful official verification to restore eligibility for review without fabricating prior delivery.
Do not adopt a historical permanent exclusion merely because a source was once inaccessible.
Pause on a challenge or missing access and request the user's permitted handoff; do not bypass controls.

## Link health, handoff, and archiving

Inspect the requested queue scope and disclose any fixed-range or budget limit.
Use explicit official closure evidence and source health; redirects, response size, or HTTP status alone may be ambiguous.
Notify only newly meaningful failures according to the user's notification policy.

For an explicitly requested link handoff, preserve identities, resume choices, reasons, and notes.
Record opening separately from application submission.
Removing or consuming queue rows requires the user's authorization and verified archival of the exact records.
Browser and shell-opening tools remain subject to the host's current restrictions.

Archive only records with explicit applied confirmation.
Upsert or reconcile the destination by stable identity before removing source rows.
Read back the full destination record and re-read the source identity and user-owned fields immediately before removal.
After interruption, reconcile the destination before retrying; an append-then-delete sequence without this check duplicates records.
Preserve native tables, headers, formatting, validation, and unrelated user rows.
