# Scheduled work

The host supplies scheduling; this reference defines run responsibilities.
Select one mode per invocation and read only its source policy and relevant state.
Do not create or alter a schedule as a side effect of using this skill.

## Boot and telemetry

Use a stable run ID, an attempt ID, a UTC start time, and the profile, preference, policy, and source-registry versions.
Check the selected workspace's audit, source freshness, cached resume facts, and policy changes before relying on cached decisions.
Reload changed authoritative rules and report policy drift.
Reuse existing validated helpers instead of recreating pipeline mechanics in an agent prompt.

Record one idempotent telemetry event for each logical run, updating it when a retry resumes that run.
Keep measured zeroes distinct from unavailable counts.
Report source scope, attempts, verified/eligible/staged/delivered counts, pending state, duration, and concrete blockers.
Keep one durable run report; update summary history only for a material result, changed blocker, or policy change.
Do not preload whole ledgers, browsing history, resumes, or unrelated dated reports when targeted identity queries suffice.

Return `success`, `partial`, `blocked`, or `failed` according to actual completion.
A complete strict-gate search with no eligible jobs can succeed.
A missing completion record, interrupted publisher, or failed telemetry must not be reported as a complete successful run.

## Inventory

Fetch only the declared source registry and bounded scope.
Budget each source family separately; one slow or deeply paginated family can otherwise use up a shared budget.
Preserve raw observations, parser versions, source health, and complete/partial results.
Validate the published snapshot's version, hash, and expected source families.
If coverage is incomplete, publish only a clearly marked partial view when the configured pipeline permits it.
Do not stage personal recommendations or write personal outcomes in inventory mode.

## Discovery

Query a fresh shared inventory before repeating source enumeration.
Refresh profile or resume evidence only when its version is stale.
Apply confirmed eligibility, location, role, industry, seniority, and quality gates, then check relevant recommendation, pending, and application identities.
Use private opened-link history only when the user has enabled that signal; do not expose unrelated history.
Use configured verification budgets and official ATS endpoints or permitted page tools.
Probe a failing access path once when useful rather than spending the entire budget on repeated empty pages.
Preserve transient failures for retry without draining the whole backlog during discovery.
Stage accepted assessments in one short owned write interval, then validate state.
Discovery does not edit the user's delivery destination or claim delivery.

## Retry

Claim only due identities within configured run/day budgets and reclaim expired claims using the backend's ownership rules.
Recheck current history, pending decisions, source state, profile, and exclusions before repeating verification.
Record methods, distinct attempts, failure reasons, next retry, and expiry.
Finalize source availability and personal eligibility separately.
Stage newly qualifying roles through the same normal staging path.
Keep failed or expired verification as unverified, not a permanent delivered recommendation or invented closure.
Release claims and locks on every exit path and report unresolved counts.

## Publisher

Require authorized publication and a configured delivery or spreadsheet adapter.
Prepare an immutable snapshot of pending decisions and check current annual history before reserving delivery.
Skip loading the delivery adapter when there is no work or it has recently failed to load.
Load the selected adapter with no root lock held and honor its bounded retry policy.
Inspect the destination, preserve protected user fields, publish by stable identity, and verify complete record readback.
For a spreadsheet, preserve its tables, formatting, validation, and protected sheets.
If the configured adapter fails to load, stop instead of switching to an unverified substitute.
Reconcile only verified publication; preserve pending records and acknowledgment-unknown results for recovery.
Publication authorizes recommendation delivery, not employer submission.

## Queue audit

Read and validate the requested queue and its writer contract.
If a required adapter cannot load, stop before mutation and report unavailable counts.
Reconcile only source closure, explicit user outcomes, and history evidence supported by the current policy.
Do not recreate sheets or records the user removed.
Repairs and row removal require their own authorization, stable-identity checks, backups, and readback.

## Market report

Use versioned job observations over the requested window and declare source coverage.
Report active/new/removed postings, occupation/skill/location mix, and supported hiring changes.
Posting counts measure observed labor demand, not completed hires or headcount.
Keep layoffs as a separately sourced event stream.
Reuse the configured reporting runtime and verify requested Markdown, images, or snapshots without mutating source data.

## Efficiency report

Summarize run statuses, blockers, verification failures, staging/delivery rates, duration, and runs with missing telemetry.
Missing records are instrumentation gaps, not zero activity.
Do not change cadence or broaden crawling from one weak run without the user's direction.

## Evidence review

Aggregate only durable JD and assessment evidence for the requested period.
Identify recurring strengths or gaps across relevant roles and preserve population and coverage limits.
Propose resume or strategy improvements without modifying resumes or application records unless separately requested.
