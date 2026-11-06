# SIM-TDB — PROMPT 00.11
## Finance Logical Integrity, Transaction Control, and Master Policy Governance Hardening

**Document ID:** SIMTDB-REV05112026-00-11-FIN-PROMPT  
**Filename:** `SIMTDB_REV05112026_00_11_FINANCE_LOGICAL_INTEGRITY_AND_TRANSACTION_CONTROL_PROMPT.md`  
**Revision:** REV05112026-R00  
**Project:** Sistem Informasi Manajemen Tanggap Darurat Bencana (SIM-TDB)  
**Organization:** Caritas Keuskupan Malang — Tim Solidaritas Kemanusiaan Keuskupan Malang (TSKKM)  
**Primary input:** `SIMTDB_REV05112026_00_10_FINANCE_FOUNDATION_REAUDIT.md`  
**Mode:** Independent re-audit, logical integrity hardening, transaction-control analysis, and test design  
**Implementation status:** NO IMPLEMENTATION — audit and logical design only

---

# A. INSTRUCTIONS TO GITHUB COPILOT

Act as a senior software architect, financial-systems analyst, database integrity specialist, security architect, and audit-minded systems engineer.

Your task is to conduct a deep, skeptical, evidence-based review of the existing SIM-TDB Finance foundation and produce the next audit document, numbered 00.11.

Do not merely agree with the previous document. Challenge its assumptions, identify missing relationships, test edge cases, and distinguish confirmed requirements from technical recommendations and unresolved organizational decisions.

The target is a Finance foundation that can later be implemented in Emergent and operated reliably in the field, including poor connectivity, repeated submissions, concurrent users, interrupted workflows, and financial reconciliation.

## A.1 Required source inspection

Before writing the report:

1. Inspect the available project/workspace files and identify the exact 00.10 document.
2. Read `SIMTDB_REV05112026_00_10_FINANCE_FOUNDATION_REAUDIT.md` completely.
3. Inspect any available preceding 00.09 R01 prompt/result, owner clarification documents, Correction & Harmonization Register (especially CHR-020), and relevant SOP extracts if they are actually available in the workspace.
4. Inspect the repository, code, schema, migrations, seed files, API routes, tests, and configuration only if they are actually available and within the authorized workspace.
5. Record exact filenames, versions, branch/commit identifiers, and evidence inspected where available.
6. If a source is unavailable, record `EVIDENCE_NOT_AVAILABLE`. Do not pretend to have inspected it.
7. Do not reconstruct missing SOP pages, SK documents, approval matrices, or financial rules from assumptions.
8. Preserve the exact wording and provenance of source-derived rules. Do not silently rewrite the SOP.

## A.2 Strict implementation boundary

This is an audit and logical-design task.

**You MUST NOT:**

- Implement application code.
- Modify existing source code.
- Create or modify physical database tables.
- Create migrations, seed data, triggers, stored procedures, or indexes.
- Change environment variables, deployment settings, authentication configuration, or production data.
- Execute destructive or mutating commands.
- Alter the original SOP, source documents, or prior audit documents.
- Claim that a test passed unless it was actually executed and evidence is available.
- Claim that a repository, database, or application was audited if it was not accessible.

**You MAY create exactly one new report file:**

`SIMTDB_REV05112026_00_11_FINANCE_LOGICAL_INTEGRITY_AND_TRANSACTION_CONTROL_REAUDIT.md`

Do not create additional files unless explicitly authorized later.

The report must contain logical models, candidate entity relationships, state-transition descriptions, test cases, risk analysis, and decision registers. It must not contain executable implementation changes.

## A.3 Evidence and provenance discipline

For every important statement, classify its origin. Use these labels consistently:

- `SOP_CONFIRMED`
- `CLARIFIED_BY_PROJECT_OWNER`
- `PROJECT_OWNER_GOVERNANCE_REQUIREMENT`
- `ORG_DECISION_CONFIRMED`
- `PENDING_OWNER_ACCEPTANCE`
- `PENDING_ORG_DECISION`
- `PENDING_DESIGN_DECISION`
- `TECHNICAL_RECOMMENDATION`
- `SOURCE_CONFLICT`
- `EVIDENCE_NOT_AVAILABLE`
- `TEST_DESIGNED`
- `TEST_EXECUTED_PASS`
- `TEST_EXECUTED_FAIL`
- `BLOCKED_BY_MISSING_POLICY`
- `BLOCKED_BY_MISSING_SOURCE`

Do not label a project-owner statement as `ORG_DECISION_CONFIRMED` unless an actual formal organizational decision document is available and verified.

Do not invent an SK number, date, issuing authority, signatory, policy approval, or effective date.

---

# 1. PROJECT CONTEXT AND BASELINE

The current 00.10 report established the following baseline:

1. Rp100,000,000 appearing in examples/templates is illustrative only. It is not a fixed amount, mandatory amount, maximum, global cap, default, or approval threshold.
2. Rp50,000,000 was clarified by the project owner as an earlier/current reference maximum for one emergency incident/response-operation control unit. It is not a permanent hardcoded value and is not an amount that must be spent.
3. The emergency-fund ceiling amount and aggregation scope are configurable policy data, not permanent code constants.
4. Two selectable aggregation modes are contemplated:
   - `PER_INCIDENT`
   - `GLOBAL_ALL_INCIDENTS`
5. Under `PER_INCIDENT`, distinct incidents may have separate ceilings, subject to the configured amount, eligible cash, source restrictions, and approval rules.
6. Under `GLOBAL_ALL_INCIDENTS`, incidents within one explicitly defined policy scope share one cumulative ceiling.
7. The ceiling is independent from eligible available cash. A configured ceiling does not prove that money exists.
8. General program/activity budgets are not automatically subject to the emergency-fund ceiling.
9. Incident, response operation, program, activity, budget, request, approval, reservation, disbursement, payment, expense recognition, and reporting are different concepts and must not be conflated.
10. The SOP page 23 wording and the project owner's later interpretation remain a `SOURCE_CONFLICT` until the appropriate organizational authority formally resolves or adopts the interpretation.
11. The 00.10 report identified major unresolved decisions: control-unit identity, global-scope boundary, event that consumes the ceiling, eligible cash basis, authority mapping, source restrictions, and policy-version transition.
12. FIN-TEST-01 through FIN-TEST-46 were designed in 00.10, but were not executed. Preserve that fact.

Do not erase, weaken, or silently reinterpret this baseline.

---

# 2. NEW GOVERNANCE REQUIREMENT — MASTER POLICY LOCK AND FORMAL AMENDMENT

The project owner has now explicitly approved the following design direction in this conversation. Treat it as a project requirement for the SIM-TDB design. Do not mislabel it as a formally issued organizational SK unless such a document is actually supplied.

## 2.1 Core principle

**Master Policy is established by organizational authority, configured by authorized SuperAdmin, and frozen throughout active operations.**

The system must not allow policy-critical settings to be changed casually or at the discretion of an ordinary administrator.

The `PER_INCIDENT` versus `GLOBAL_ALL_INCIDENTS` selection is a foundational policy decision. It is not an operational toggle that users can switch whenever convenient.

The same principle applies to other policy-critical parameters designated by the organization, including, where applicable:

- Emergency-fund ceiling amount.
- Aggregation mode.
- Control-unit definition.
- Global policy-scope boundary.
- Applicable fund-pool/source restrictions.
- Policy effective period.
- Other policy-critical financial controls explicitly designated by the organization.

Do not automatically classify every ordinary master-data record as a Master Policy. Distinguish policy-critical configuration from ordinary operational master data.

## 2.2 Initial setup

- Initial Master Policy setup occurs before the first operational program is activated.
- Initial setup is performed only by an authorized SuperAdmin account.
- The initial configuration must identify its governing source, such as the applicable SOP, formal decision, SK, or other authority document accepted by the organization.
- Record the source document identity and location/page where applicable.
- Do not invent a nominal value or mode.
- Rp50,000,000 remains a reference candidate only until the organization formally approves the initial configuration.
- Rp100,000,000 must never become an automatic default because it appears in an example.
- The SuperAdmin is the technical/administrative executor of an organizational decision, not the person who independently creates organizational policy.

If the required governing basis for initial setup is unavailable, mark the setup as blocked or pending. Do not fabricate approval.

## 2.3 Policy freeze while operations are active

Once an operational program is running, the active Master Policy must be frozen.

**While at least one program is running, no user — including SuperAdmin — may change the active policy amount, aggregation mode, scope, or other locked policy-critical parameters.**

The system must also block policy amendments while any relevant financial obligation or transaction remains unresolved, even if a program has been marked complete.

The following are minimum blockers to analyze:

- A program is active or in progress.
- A program is temporarily suspended, paused, on hold, or otherwise not finally closed.
- A program is in a closing state but has not passed the approved financial closure/reconciliation gate.
- A relevant incident or response operation remains open, if it is within the policy's operational scope.
- A fund request is pending review or approval.
- An approved amount remains reserved.
- A payment instruction remains outstanding.
- An advance or cash advance has not been accounted for.
- A disbursement has not been reconciled.
- A refund, reversal, correction, or disputed transaction remains unresolved.
- A financial report or required accountability document remains outstanding.
- Any other policy-linked obligation remains open under the approved closure rules.

Do not assume the exact program status names are already defined. Map the actual status vocabulary if available. If it is not available, propose candidate groupings and mark the mapping as `PENDING_DESIGN_DECISION` or `PENDING_ORG_DECISION`.

**Important:** Do not use a simple `program.status = completed` check as the sole unlock condition. Program closure and financial closure are separate gates.

## 2.4 Locked-menu behavior

When the policy is frozen:

- The policy-edit/setup menu must not be available for editing.
- It may be hidden or shown as disabled with a clear explanation, according to the UI decision.
- An authorized read-only view of the active policy may remain available.
- No edit action, mode selector, amount editor, scope editor, or activation action may be exposed to ordinary users.
- SuperAdmin must not receive an override button.
- A direct API call, manually crafted request, alternate route, browser manipulation, or client-side state change must not bypass the backend lock.
- The backend must independently evaluate the lock condition on every policy-changing operation.
- The UI lock is a usability feature; the server-side lock is the actual security and integrity control.

The lock must be enforced at the service/domain boundary and at the transaction boundary, not only by hiding a frontend menu.

## 2.5 No SuperAdmin override while locked

This rule is mandatory:

**SuperAdmin cannot bypass the policy freeze while any blocking program or unresolved obligation exists.**

Do not create:
- Emergency override.
- Force unlock.
- Admin bypass.
- Hidden route.
- Direct database-edit workaround.
- Special permission that defeats the lock.

If the organization later requires a legally exceptional mechanism, it must be designed as a separately approved governance amendment, not silently included in this design.

## 2.6 Conditions to reopen policy setup

Policy setup may become eligible for amendment only after:

1. No operational program remains running.
2. All relevant programs have reached a formally accepted terminal/closed state.
3. All relevant financial obligations have been resolved.
4. All required reconciliations and accountability evidence have been completed.
5. No unresolved policy-linked transaction remains.
6. The system can produce a policy-lock eligibility report showing why the gate is clear.
7. A valid formal decision basis for the proposed change is available.

Passing the gate means the change may be submitted for controlled processing. It does not itself authorize a change.

The exact definition of final closure and the authority that certifies it must be recorded as a decision if not supported by existing organizational documents.

## 2.7 Race-condition protection

Analyze the race condition where:
- SuperAdmin begins a policy amendment while an operator activates a new program; or
- A program begins while a policy amendment is being activated.

These two operations must be serialized or protected by an equivalent atomic mechanism.

The system must never allow:
- A new program to start using a half-updated policy.
- A policy to change after a program has started.
- A policy lock check to pass using stale status data.
- Two concurrent policy amendments to create conflicting active versions.

Describe the logical transaction boundary, lock acquisition, re-check, commit, and rollback behavior. Do not implement code or choose a database-specific mechanism at this stage.

---

# 3. FORMAL SK / DECISION BASIS — NO LEGAL BASIS, NO POLICY CHANGE

## 3.1 Mandatory amendment evidence

Every amendment to a locked Master Policy must have a formal organizational decision basis.

The policy-change workflow must require, at minimum:

| Field | Requirement |
|---|---|
| Legal/decision basis type | Required |
| SK/decision number | Required; exact official number, not a free-form substitute such as “management approval” |
| SK/decision date | Required |
| Issuing organization/authority | Required |
| Authorized signatory/position | Required where shown in the document |
| Decision subject/title | Required |
| Summary of relevant decision | Required |
| Original document attachment | Required |
| Effective date of policy change | Required |
| Change reason/context | Required |
| Previous policy version | System-linked, not manually typed as the source of truth |
| Proposed new policy version | System-generated draft/version reference |
| Changed fields | System-generated before/after comparison |
| SuperAdmin actor | Automatically captured from authenticated identity |
| Submission/activation timestamp | System-generated |
| Verification status | Required lifecycle field |
| Verification evidence/notes | Required where verification is performed |

Do not create fake examples that could be mistaken for real SK records. If examples are needed, visibly label them `ILLUSTRATIVE — NOT A REAL SK`.

## 3.2 SK validation

Design a validation checklist that checks:

- SK/decision number is present.
- Date is present and valid.
- Issuing authority is identified.
- Subject is relevant to the proposed policy change.
- The document is attached and readable.
- Effective date is coherent with the decision document.
- The document has not been superseded, revoked, or expired, if such information is available.
- The signatory/issuer appears to have the relevant authority, subject to organizational verification.
- The document is not being reused as an unrelated basis for a different policy change.
- The document reference can be retrieved later during audit.

A file upload alone does not prove that the SK is authentic or legally sufficient. The system may record verification status and evidence, but a competent organizational person must verify the authority and content.

If the SK is missing, incomplete, unrelated, rejected, or not verified to the required level, the amendment must not activate.

## 3.3 Evidence integrity

Recommend a logical evidence model that preserves:

- Original uploaded file.
- File name and media type.
- File size.
- Upload actor and timestamp.
- Cryptographic checksum/hash as a technical recommendation.
- Document reference/identifier.
- Verification actor, date, result, and notes.
- Supersedes/revokes relationship, if relevant.
- Policy amendment record that relies on the document.

Do not overwrite the original SK attachment. A replacement/corrected document must be stored as a new evidence version or linked record.

## 3.4 SK and amendment audit trail

Every amendment must preserve:

- Old policy version.
- New policy version.
- Old and new values for every changed field.
- SK number and date.
- Issuer and subject.
- Document reference.
- Effective date.
- Change reason.
- SuperAdmin identity.
- Verification/approval evidence.
- Time of each lifecycle event.
- Lock-gate result and blocker report at the time of change.

Audit records must be append-only from the application's normal permission model. No ordinary administrator or SuperAdmin UI action may delete or rewrite historical amendment evidence.

Do not claim absolute tamper-proof storage unless the underlying infrastructure has been inspected and verified. Describe the logical integrity requirements and any additional infrastructure controls as recommendations.

## 3.5 Initial setup versus amendment

Distinguish:
- Initial Master Policy setup before operations.
- Amendment of an existing active policy after operations have fully closed.

Initial setup must record its governing source and authority evidence. Subsequent amendments must require the formal SK/decision basis described above.

If the organization later requires an SK for initial setup as well, record that as an explicit governance rule. Do not infer a real SK exists when none was provided.

---

# 4. SUPERADMIN ROLE AND ACCESS CONTROL

## 4.1 Intended use

SuperAdmin is a highly restricted technical/administrative account used for:

- Initial Master Policy setup before operations begin.
- Formal policy amendment after the lock gate is clear and the required SK/decision evidence is available.
- Other explicitly authorized core-system bootstrap functions, if separately approved.

SuperAdmin is not an everyday operational account and is not the owner of organizational policy.

## 4.2 Required access controls

Analyze and recommend:

- Individual named SuperAdmin identity; no shared account.
- Strong authentication and MFA.
- Least-privilege access.
- Restricted assignment and revocation process.
- No routine operational transactions under SuperAdmin.
- Automatic capture of authenticated actor identity.
- Session and access logging.
- Re-authentication or step-up authentication before policy activation, if appropriate.
- Separation between viewing policy and changing policy.
- Explicit denial of policy changes for every non-SuperAdmin role.
- Server-side authorization on every route/API/action.
- Negative tests for direct API calls and manipulated client requests.

Do not invent the real person's identity, organizational appointment, or authority.

## 4.3 No hidden bypass

Verify the logical design against these bypass attempts:

- Direct URL access to the policy editor.
- Calling an API endpoint without using the UI.
- Changing browser/client state.
- Replaying an old request.
- Reusing another user's session.
- Calling a stale policy-version endpoint.
- Submitting a policy change while a program is active.
- Submitting a policy change while a financial obligation is open.
- Concurrently starting a program and activating a new policy.

Every attempt must be rejected at the authoritative backend/service layer when the gate is not satisfied.

---

# 5. POLICY LIFECYCLE AND FREEZE STATE MODEL

Create a logical lifecycle model. Candidate state names may be proposed, but mark them as technical recommendations until accepted.

At minimum analyze:

1. `DRAFT`
2. `EVIDENCE_PENDING`
3. `READY_FOR_AUTHORIZATION`
4. `AUTHORIZED`
5. `SCHEDULED` (only if future effective dates are supported)
6. `ACTIVE_LOCKED`
7. `SUPERSEDED`
8. `RETIRED`
9. `REJECTED`
10. `CANCELLED`

Do not treat these candidate labels as already approved organizational terminology.

For each transition specify:
- Who can initiate it.
- Preconditions.
- Required evidence.
- Lock-gate check.
- Resulting active policy version.
- Audit event.
- Whether rollback is allowed.
- What happens to programs/requests already referencing the previous version.

## 5.1 Lock eligibility matrix

Create a detailed matrix for cases such as:

| Condition | Policy change eligibility |
|---|---|
| No program has ever started; initial setup not yet completed | Eligible for controlled initial setup, subject to governing source |
| At least one program is active | Block |
| Program is paused/suspended/on hold | Block unless formally closed under approved rules |
| Program is closing but not financially closed | Block |
| Program is complete but has an outstanding advance | Block |
| Program is complete but a payment is outstanding | Block |
| Program is complete but a reconciliation is pending | Block |
| All programs terminal and all relevant obligations reconciled | Eligible to submit amendment, subject to formal decision evidence |
| SuperAdmin attempts override while any blocker exists | Block |
| A new program activation races with policy activation | Serialize; only one operation may commit under a consistent policy state |

Map actual source status names where available. If not available, mark the status mapping as pending.

## 5.2 Lock report

Design a logical `Policy Lock Eligibility Report` showing:

- Evaluation timestamp.
- Active policy version.
- Program count by blocking status.
- Open incident/operation count if relevant.
- Pending request count.
- Reserved amount.
- Outstanding payment count/amount.
- Outstanding advance count/amount.
- Unreconciled disbursement count/amount.
- Pending refund/reversal/correction count.
- Missing accountability documents.
- Final list of blockers.
- Overall result: `LOCKED` or `ELIGIBLE_FOR_AMENDMENT`.

Do not expose sensitive personal/financial details to users who are not authorized to see them.

The report must be derived from canonical records, not manually maintained counters.

---

# 6. POLICY SCOPE, INCIDENT, RESPONSE OPERATION, AND PROGRAM RELATIONSHIPS

## 6.1 Separate the concepts

The logical model must distinguish:

- Master Policy.
- Policy Version.
- Policy Scope Instance.
- Program.
- Incident.
- Response Operation.
- Fund Request.
- Approval Decision.
- Ceiling Consumption Event.
- Cash Movement.
- Disbursement.
- Expense Recognition.
- Financial Reconciliation.

Do not assume that a Program is the same as an Incident, or that a Response Operation is the same as a Program.

## 6.2 `PER_INCIDENT`

The project owner has approved the option as a possible policy mode, but the exact control unit remains unresolved.

Analyze at least:

- One ceiling per real-world parent incident.
- One ceiling per formally independent response operation.
- Another formally defined control unit, if the organization chooses it.

For each option assess:
- Anti-splitting risk.
- Duplicate incident risk.
- Parent-child relationship.
- Aggregation across sectors, activities, teams, vouchers, users, and sub-records.
- Reporting and audit implications.
- Required organizational definition.

Do not choose one as an established policy without evidence. You may recommend a conservative default for discussion, but mark it `TECHNICAL_RECOMMENDATION` and `PENDING_ORG_DECISION`.

## 6.3 `GLOBAL_ALL_INCIDENTS`

The global mode requires an explicit `Policy Scope Instance` or equivalent logical identity.

Analyze possible boundaries without choosing one automatically:

- One emergency-response activation.
- One response period.
- One approved program/campaign.
- One defined policy term.
- Another organization-approved scope.

Do not assume:
- Global means forever.
- Global resets every calendar year.
- A new incident automatically belongs to the previous scope.
- Closing one incident resets the global ceiling.
- A new program automatically creates a new global ceiling.

The scope boundary and any reset/supersession behavior must be explicitly approved and traceable.

## 6.4 Policy binding to programs and incidents

Recommend how each program, incident, response operation, and fund request references the policy version and scope instance applicable to it.

Analyze whether:
- A program binds to one policy version at activation.
- Multiple programs can share a single policy scope.
- An incident can be linked to more than one program.
- A response operation can span multiple incidents.
- A program can be linked to multiple incidents.

Do not finalize cardinalities that the source documents do not establish. Present alternatives and decision consequences.

---

# 7. EMERGENCY FUND CONSUMPTION LEDGER

This is a major new focus. The 00.10 design discusses control records and transaction events but does not fully specify a ledger model that prevents duplicate consumption.

Design a logical, append-only `Emergency Fund Consumption Ledger` concept.

## 7.1 Purpose

The ledger must provide a traceable record of every event that increases, reserves, releases, converts, reverses, or otherwise changes the amount counted against the emergency-fund ceiling.

It must not be confused with:
- Cash/bank movement ledger.
- General accounting ledger.
- Budget ledger.
- Expense recognition.
- Request history.
- Approval history.

These records may be linked but have different meanings.

## 7.2 Candidate logical fields

Analyze at least:

- Consumption event ID.
- Policy ID.
- Policy version ID.
- Policy scope instance ID.
- Control-unit ID/type.
- Incident ID.
- Response Operation ID, if applicable.
- Program ID, if applicable.
- Fund Request ID.
- Approval decision reference.
- Disbursement/payment reference, if applicable.
- Source event ID.
- Event type.
- Signed amount or explicit increase/decrease direction.
- Currency.
- Event timestamp.
- Effective/business timestamp.
- Actor/system process.
- Idempotency key.
- Correlation ID.
- Causation/source-event reference.
- Reversal-of reference.
- Status/validation outcome.
- Evidence/document reference.

Do not convert this list into physical table columns or database types.

## 7.3 Event semantics must remain explicit

Analyze candidate event types such as:

- Ceiling reservation.
- Reservation increase.
- Reservation reduction.
- Reservation release.
- Disbursement conversion from reservation.
- Direct disbursement consumption, if approved.
- Cancellation.
- Reversal.
- Refund.
- Correction/adjustment.

These are candidate logical events, not automatically approved accounting events.

**The exact event that consumes the ceiling remains a pending policy decision unless an approved source resolves it.**

Evaluate options:
- Request submission.
- Approval.
- Reservation.
- Payment instruction.
- Actual cash release/disbursement.
- Another formal event.

For every option, explain:
- Whether concurrent requests can overcommit.
- Whether an unapproved request consumes the ceiling.
- Whether an approved-but-unpaid request consumes the ceiling.
- How a cancellation releases capacity.
- How partial disbursement works.
- How reservation converts to release without double counting.
- How a refund/reversal affects the ceiling.
- How the system handles an expired reservation.

Do not silently choose an accounting treatment.

## 7.4 Core ledger invariants

Design controls ensuring:

1. One source event cannot be posted twice under the same idempotency identity.
2. A retry after timeout cannot create a second consumption event.
3. A reservation converted into disbursement is not counted twice.
4. A reversal must reference the original event.
5. Original events are not deleted or overwritten.
6. A correction is represented by a new linked event.
7. A partial disbursement consumes only the amount defined by the approved event semantics.
8. The ledger can be reconciled to requests, approvals, cash movement, and disbursements.
9. A report can reconstruct the ceiling usage at a past point in time.
10. Each event can be traced to the policy version and scope instance that governed it.
11. No event may silently migrate to a new policy version.
12. Duplicate incident resolution must preserve identifiers and transaction history.

## 7.5 Conceptual formulas only

For `PER_INCIDENT`:

`Remaining ceiling = configured ceiling - net counted consumption for the approved control unit`

For `GLOBAL_ALL_INCIDENTS`:

`Remaining ceiling = configured ceiling - net counted consumption for all included control units in the approved policy scope`

These are conceptual formulas only. Define the event set and treatment of reversals/reservations only after the relevant policy decision.

Do not calculate the remaining ceiling from a manually editable total field.

---

# 8. ELIGIBLE CASH, FUND POOL, AND CASH MOVEMENT CONTROL

Extend the 00.10 cash model without inventing accounting rules.

## 8.1 Keep separate concepts

- Funding Source.
- Fund Pool.
- Bank/Cash Account.
- Cash Evidence.
- Cash Balance.
- Restricted Cash.
- Eligible Cash.
- Reserved Cash.
- Outstanding Payment.
- Advance.
- Cash Release/Disbursement.
- Refund.
- Reversal.
- Expense Recognition.

## 8.2 Required analysis

1. Identify canonical source records for cash balances, if available.
2. Determine whether one policy can use one or multiple fund pools.
3. Determine whether a request can be allocated across multiple funding sources.
4. Explain source restrictions and why organization-wide balances cannot automatically be combined.
5. Distinguish cash availability from approved budget and remaining budget.
6. Explain the treatment options for reserved amounts and outstanding payment instructions.
7. Explain how cash reservation converts into actual cash release without double counting.
8. Explain reconciliation of cash movement to bank/cash evidence.
9. Identify the required source and timing of balance snapshots.
10. Identify the risks of stale balances and concurrent use.

Do not invent the eligible-cash formula. Present the necessary components and decision options, then mark unresolved accounting treatment as pending.

## 8.3 Separate cash ledger from ceiling ledger

A single financial event may affect:
- The policy ceiling.
- The available cash.
- The actual expenditure.
- The accounting record.

Those effects must be linked but must not be collapsed into one amount or one status.

Produce a mapping table showing which event affects which logical record, subject to policy decisions.

---

# 9. TRANSACTION LIFECYCLE AND STATE TRANSITIONS

Build a logical lifecycle for:

1. Fund Request.
2. Review/Approval.
3. Ceiling Reservation, if adopted.
4. Cash Reservation, if adopted.
5. Payment Instruction.
6. Disbursement/Cash Release.
7. Expense Recognition.
8. Accountability/Settlement.
9. Refund.
10. Reversal/Correction.
11. Reconciliation/Closure.

For each lifecycle:
- Provide candidate states.
- Explain allowed transitions.
- Identify who may perform each action, but do not invent authority.
- Identify required evidence.
- Identify which ledger(s) are affected.
- Identify whether the action is reversible.
- Identify the audit event.
- Identify retry/idempotency behavior.
- Identify pending policy/accounting decisions.

Explicitly test:
- Rejected request.
- Cancelled request.
- Approved but unpaid request.
- Reserved request.
- Partial disbursement.
- Multiple disbursements for one request.
- Disbursement retry after timeout.
- Payment failure.
- Refund after disbursement.
- Reversal after erroneous posting.
- Advance not yet accounted for.
- Program closed administratively but finance still open.
- Program closure after full reconciliation.

Do not equate `APPROVED`, `RESERVED`, `PAID`, `DISBURSED`, `EXPENSE_RECOGNIZED`, and `SETTLED`.

---

# 10. IDEMPOTENCY, DUPLICATE PREVENTION, CORRELATION, AND CONCURRENCY

The system must be reliable when field users repeat actions, connections fail, or multiple users act simultaneously.

## 10.1 Idempotency

Design a logical idempotency approach for:
- Creating fund requests.
- Submitting approval decisions.
- Creating reservations.
- Sending payment instructions.
- Recording disbursements.
- Posting reversals/refunds.
- Synchronizing offline submissions.
- Re-running reconciliation jobs.

For each operation define:
- Idempotency identity.
- Scope of uniqueness.
- Payload consistency check.
- Duplicate response behavior.
- Retention period decision.
- Conflict response.
- Audit behavior.

A repeated request with the same idempotency identity must return or reference the original result rather than create a second financial effect.

Do not use only a client-generated timestamp as an idempotency key.

## 10.2 Duplicate business records

Distinguish:
- Duplicate HTTP/API request.
- Duplicate user submission.
- Duplicate fund request.
- Duplicate disbursement instruction.
- Duplicate incident record.
- Two legitimate transactions with the same amount.
- Duplicate document upload.

Do not auto-merge records merely because names, dates, or amounts are similar.

Use controlled review and preserve original IDs and links if a duplicate is confirmed.

## 10.3 Correlation and causation

Every multi-step process should be traceable through stable correlation and causation references.

Design a logical chain such as:

`Program → Incident/Operation → Fund Request → Approval → Reservation → Payment Instruction → Disbursement → Ledger Event → Reconciliation`

This is illustrative. Adjust it to the actual domain model.

No step may rely solely on a mutable display name or manually typed text to find its parent transaction.

## 10.4 Concurrency

Analyze simultaneous:
- Two requests against the same `GLOBAL_ALL_INCIDENTS` ceiling.
- Two requests against the same `PER_INCIDENT` control unit.
- Two requests against the same fund pool.
- Two SuperAdmin policy amendment attempts.
- Program activation versus policy amendment.
- Reservation conversion versus cancellation.
- Duplicate retry versus original transaction still processing.

Describe the logical consistency strategy, such as atomic validation-and-posting, locking/serialization, optimistic version checks, or equivalent approaches.

Do not choose a database vendor or implement database-specific syntax.

The design must prevent:
- Overspending a ceiling.
- Overspending eligible cash.
- Double reservation.
- Double disbursement.
- Lost updates.
- Stale policy selection.
- Partial commit between linked financial records.

---

# 11. OFFLINE / POOR CONNECTIVITY AND FIELD OPERATIONS

The application is intended for field operations where connectivity may be interrupted.

Analyze:

- User submits a request and the network drops before confirmation.
- User retries the same request.
- Device reconnects and synchronizes queued actions.
- Two devices submit the same business action.
- A request is submitted offline while the active policy remains frozen.
- A policy change is attempted from a disconnected device.
- An offline approval is queued and later synchronized.
- A local transaction conflicts with a server-side status change.
- A disbursement confirmation is delayed or duplicated.

Requirements:

1. Server-side policy and financial state remain authoritative.
2. Offline actions must not bypass active policy or approval rules.
3. Policy setup/amendment must not be available offline.
4. Every queued action must retain a stable client-generated idempotency identity and correlation reference.
5. Sync must be idempotent.
6. Conflict resolution must not silently overwrite server records.
7. A transaction with an unknown outcome must be reconciled before retry creates a new financial effect.
8. The UI must clearly distinguish local pending, server accepted, rejected, and reconciled states.
9. Do not promise offline financial approval or disbursement unless an approved offline operating policy explicitly allows it.
10. Mark offline authority and queue rules as pending where organizational policy is required.

---

# 12. LOGICAL ENTITY AND RELATIONSHIP REVIEW

Review the 00.10 ERD and propose a corrected logical model. The names below are conceptual candidates, not approved physical table names:

- `MASTER_POLICY`
- `MASTER_POLICY_VERSION`
- `POLICY_LEGAL_BASIS_REFERENCE`
- `POLICY_AMENDMENT_RECORD`
- `POLICY_LOCK_EVALUATION`
- `POLICY_SCOPE_INSTANCE`
- `PROGRAM`
- `PROGRAM_POLICY_BINDING`
- `INCIDENT`
- `RESPONSE_OPERATION`
- `INCIDENT_SCOPE_MEMBERSHIP`
- `FUND_SOURCE`
- `FUND_POOL`
- `CASH_EVIDENCE_RECORD`
- `FUND_REQUEST`
- `APPROVAL_DECISION`
- `CEILING_CONSUMPTION_LEDGER`
- `CASH_MOVEMENT_LEDGER`
- `PAYMENT_INSTRUCTION`
- `DISBURSEMENT_EVENT`
- `EXPENSE_RECOGNITION_REFERENCE`
- `REFUND_REVERSAL_REFERENCE`
- `FINANCIAL_DOCUMENT_REFERENCE`
- `AUDIT_EVENT`
- `IDEMPOTENCY_RECORD`
- `CORRELATION_REFERENCE`

For each concept provide:
- Purpose.
- Candidate identifier.
- Key logical attributes.
- Relationship/cardinality.
- Lifecycle.
- Source of truth.
- Provenance.
- Pending decisions.
- Duplicate/orphan prevention requirements.

## 12.1 Required logical relationships to analyze

At minimum:

- One Master Policy has multiple Policy Versions.
- A Policy Version references its legal/decision basis.
- A Policy Version may be linked to multiple Programs, subject to policy scope.
- A Program references the policy version applicable at activation.
- A Policy Scope Instance groups only the incidents/operations formally within its scope.
- An Incident may have one or more Response Operations, if supported by the approved model.
- A Fund Request belongs to a valid program/incident/operation context according to the business rules.
- A Fund Request may have multiple approval decisions over its lifecycle.
- A Fund Request may have multiple reservation/disbursement events.
- A consumption-ledger event references its source event and policy scope.
- A cash-movement event references the relevant fund pool/source.
- A refund/reversal references the original event.
- Audit events reference the actor and target record.
- Idempotency records identify the operation and original result.

Do not force cardinalities that source documents do not support. Present alternatives where necessary.

## 12.2 Required logical diagrams

Produce:
1. Master Policy Governance ERD (logical only).
2. Finance Transaction and Ledger ERD (logical only).
3. Program–Incident–Response Operation relationship diagram.
4. Policy Freeze and Amendment workflow.
5. Fund Request to Reconciliation lifecycle.
6. Lock-gate decision flow.

Use Mermaid in the report. Label diagrams as conceptual/logical, not physical database schema.

---

# 13. SECURITY, AUDITABILITY, AND ACCOUNTABILITY CONTROLS

Review the design against:

- Authentication.
- Authorization.
- SuperAdmin isolation.
- Role/permission separation.
- Object-level access.
- Direct API access.
- Document upload integrity.
- Audit record immutability.
- Policy version immutability.
- Transaction history immutability.
- Sensitive financial data access.
- Session management.
- MFA/step-up authentication.
- Administrative access review.
- Backup and recovery implications.
- Audit evidence retrieval.

Distinguish:
- Organizational authority.
- Formal delegation.
- User account.
- System role.
- Permission.
- Operational assignment.
- Approval action.
- Policy amendment execution.

A technical permission must never create an organizational authority that does not exist in formal evidence.

The SuperAdmin may encode an authorized decision but must not become the policy-making authority merely because the account has technical privileges.

---

# 14. REQUIRED TEST PLAN — PRESERVE FIN-TEST-01 THROUGH FIN-TEST-46 AND ADD NEW TESTS

## 14.1 Existing tests

Review FIN-TEST-01 through FIN-TEST-46 from 00.10.

- Do not delete test IDs.
- Do not silently change their purpose.
- Correct domain classification where necessary.
- Separate assertions for policy ceiling, eligible cash, and accounting recognition.
- Add explicit preconditions and transaction sequence.
- Keep actual result as `not executed` unless genuinely executed with evidence.
- Retain `BLOCKED_BY_MISSING_POLICY` or `BLOCKED_BY_MISSING_SOURCE` where appropriate.

## 14.2 Add at least FIN-TEST-47 through FIN-TEST-80

Create a detailed test matrix containing:

| ID | Required scenario | Expected control |
|---|---|---|
| FIN-TEST-47 | SuperAdmin attempts policy change while one program is active | Blocked; no override |
| FIN-TEST-48 | Policy change while a program is paused/suspended/on hold | Blocked unless formally terminal under approved rules |
| FIN-TEST-49 | Program marked complete but financial obligation remains open | Blocked |
| FIN-TEST-50 | SuperAdmin attempts policy change with no SK/decision number | Blocked |
| FIN-TEST-51 | SK number exists but date, issuer, subject, or attachment is missing | Blocked |
| FIN-TEST-52 | SK attachment uploaded but verification is pending/rejected | Not activated |
| FIN-TEST-53 | Non-SuperAdmin calls policy amendment API directly | Denied server-side and logged |
| FIN-TEST-54 | SuperAdmin attempts hidden/alternate route while policy is locked | Denied server-side |
| FIN-TEST-55 | Policy version is amended after all gates pass | New version created; old version remains immutable |
| FIN-TEST-56 | Policy amendment records complete before/after comparison and SK reference | Audit evidence complete |
| FIN-TEST-57 | Attempt to edit or delete historical policy version | Denied |
| FIN-TEST-58 | Policy amendment and program activation occur concurrently | Atomic serialization; no mixed policy state |
| FIN-TEST-59 | No active approved policy exists and a program is activated | Program activation blocked |
| FIN-TEST-60 | Lock eligibility report is generated | All blockers and source references are derived and traceable |
| FIN-TEST-61 | Global policy scope receives multiple incidents | Only explicitly included incidents consume the scope ceiling |
| FIN-TEST-62 | Global scope boundary changes | New approved version/scope behavior; no silent reset |
| FIN-TEST-63 | Per-incident control unit receives multiple vouchers/sectors/activities | No artificial reset through child records |
| FIN-TEST-64 | Same source event is retried with the same idempotency key | Original result returned/referenced; no duplicate ledger effect |
| FIN-TEST-65 | Same disbursement request is retried after timeout | No duplicate cash release or ceiling consumption |
| FIN-TEST-66 | Reservation converts to disbursement | No double counting; original reservation is converted/reconciled according to approved semantics |
| FIN-TEST-67 | Reservation is cancelled before disbursement | Release treatment follows approved rule; history preserved |
| FIN-TEST-68 | Partial disbursement against a larger approved request | Only the correct amount affects each ledger |
| FIN-TEST-69 | Refund/reversal is recorded | Linked compensating event; original event remains |
| FIN-TEST-70 | Two simultaneous requests compete for the same global ceiling | Atomic control prevents over-consumption |
| FIN-TEST-71 | Two simultaneous requests compete for the same per-incident ceiling | Atomic control prevents over-consumption |
| FIN-TEST-72 | Two simultaneous requests compete for the same eligible cash pool | Cash is not allocated twice |
| FIN-TEST-73 | Duplicate incident candidates are detected | No automatic merge; controlled resolution preserves IDs and links |
| FIN-TEST-74 | Policy version changes after prior programs are closed | Historical programs retain their original policy references |
| FIN-TEST-75 | New program starts while a policy amendment is pending | Start/amendment gate prevents inconsistent activation |
| FIN-TEST-76 | Policy edit menu is hidden/disabled while locked but read-only policy view remains | No edit path is available; read-only data is accurate |
| FIN-TEST-77 | Program is administratively closed with unsettled advance/payment/reconciliation | Policy remains locked |
| FIN-TEST-78 | Policy change has valid SK but lock gate is not clear | Blocked; SK does not bypass operational freeze |
| FIN-TEST-79 | No valid SK but all programs and obligations are closed | Blocked; clear gate alone does not authorize policy change |
| FIN-TEST-80 | Offline queued request is synchronized after reconnect | Idempotent processing; server policy remains authoritative |

For each test include:
1. Test ID.
2. Domain.
3. Objective.
4. Preconditions.
5. Exact test data.
6. Step-by-step execution sequence.
7. Expected result.
8. Separate assertions for ceiling, cash, transaction state, and audit trail where relevant.
9. Actual result (`not executed` unless truly run).
10. Status.
11. Evidence reference.
12. Dependencies and pending decisions.

Add further tests if gaps are discovered. Do not stop at FIN-TEST-80 if the audit identifies additional critical cases.

---

# 15. FAILURE, RECOVERY, AND RECONCILIATION DESIGN

Analyze how the system recovers from:

- API timeout after the database transaction committed.
- Timeout before commit.
- Network loss during request submission.
- Network loss during disbursement confirmation.
- Duplicate webhook/callback.
- Partial failure between linked ledger records.
- Stale client policy version.
- Concurrent program closure and policy amendment.
- Failed attachment upload.
- Missing SK file after amendment draft creation.
- Reconciliation job interrupted and retried.
- Duplicate or out-of-order offline sync events.
- Invalid parent-child references.
- Orphaned ledger events.
- A transaction with an unknown external payment outcome.

Define logical safeguards:
- Idempotent retry.
- Correlation and causation IDs.
- Atomic transaction boundaries.
- Outbox/inbox patterns as technical options, not mandatory architecture unless justified.
- Reconciliation queue.
- Exception handling.
- Manual review with traceable resolution.
- No silent deletion or overwrite.
- No infinite retry loop.
- Clear terminal error state and operator guidance.

Do not claim the system can guarantee exactly-once processing across external systems. Explain the practical approach: at-least-once delivery with idempotent effect, reconciliation, and explicit handling of unknown outcomes.

---

# 16. CROSS-MODULE CONTRACTS

The Master Policy Governance mechanism is a Core System concern and should be reusable by other modules.

Analyze the required contracts between:

| Module | Required relationship |
|---|---|
| Core System / Master Policy Governance | Owns policy version, lock state, legal basis, amendment audit |
| Program Management | Reports program lifecycle and activation/closure state to policy lock gate |
| Incident Management | Provides incident identity and operational state |
| Response Operations | Provides operation identity and closure state if applicable |
| Finance | Owns fund request, ceiling ledger, cash control, disbursement, reconciliation |
| Procurement | Provides purchase/commitment references without falsely treating PO as payment |
| Logistics/Inventory | Provides goods receipt and stock movement references without conflating them with cash release |
| User Management / RBAC | Provides authenticated actor, role, permission, and SuperAdmin control |
| Document Management | Stores original SK and financial evidence references |
| Audit/Reporting | Provides immutable traceability and derived reports |

Do not duplicate the active Master Policy independently inside each module.

A module must reference the authoritative policy version and must not keep a separately editable copy of its policy-critical values.

Define logical API/service contracts only as descriptions:
- Policy lookup/read.
- Policy version reference.
- Lock eligibility check.
- Amendment eligibility evaluation.
- Program activation gate.
- Policy amendment submission.
- Audit event retrieval.

Do not write endpoint code or final API schemas.

---

# 17. REQUIRED OUTPUT DOCUMENT

Create exactly this report:

`SIMTDB_REV05112026_00_11_FINANCE_LOGICAL_INTEGRITY_AND_TRANSACTION_CONTROL_REAUDIT.md`

The report must be written in formal, precise Indonesian with English technical terms where appropriate.

Use this structure:

1. Executive Summary.
2. Scope, Source Inventory, and Evidence Availability.
3. Audit Method and Limitations.
4. Provenance / Source Authority Matrix.
5. Updated Owner Clarification and Governance Requirement Register.
6. 00.10 Findings: Confirmed, Corrected, and Still Open.
7. Master Policy Governance Principle.
8. Policy Freeze / Lock-Gate Model.
9. Formal SK / Decision Basis and Amendment Evidence Model.
10. SuperAdmin Access and No-Override Control.
11. Policy Lifecycle and Version Transition.
12. Program/Incident/Response Operation/Policy Scope Logical Relationships.
13. Emergency Fund Consumption Ledger.
14. Eligible Cash and Cash Movement Control.
15. Fund Request to Reconciliation Lifecycle.
16. Idempotency, Duplicate Prevention, Correlation, and Concurrency.
17. Offline / Poor Connectivity Handling.
18. Logical ERD and Entity Registry.
19. Logical Data Dictionary.
20. Security and Auditability.
21. Failure Recovery and Reconciliation.
22. Cross-Module Contracts.
23. Corrected FIN-TEST-01 through FIN-TEST-46.
24. New FIN-TEST-47 onward.
25. Risk Register.
26. Decision Register.
27. Evidence Required from Organization / SOP / Finance.
28. Readiness Assessment.
29. Recommendation for 00.12.

Include:
- Mermaid diagrams.
- Tables.
- Explicit status labels.
- Decision owners only where evidence supports them; otherwise say `OWNER TO BE DESIGNATED`.
- A clear distinction between owner requirements, SOP text, formal organizational decisions, and technical recommendations.

---

# 18. REQUIRED DECISION REGISTER

Create/update a Decision Register with at least these questions:

1. Formal resolution of SOP page 23 versus owner clarification.
2. Initial policy amount and effective date.
3. Initial aggregation mode.
4. `PER_INCIDENT` control-unit definition.
5. `GLOBAL_ALL_INCIDENTS` scope boundary.
6. Global-scope reset/supersession rule.
7. Event that consumes the ceiling.
8. Eligible cash formula and source.
9. Reservation and outstanding-payment treatment.
10. Funding-source/fund-pool cardinality.
11. Actual expenditure recognition.
12. Program statuses that block policy changes.
13. Definition of final program closure.
14. Financial obligations that block policy changes.
15. Authority that certifies financial closure.
16. SK/decision verification responsibility.
17. SuperAdmin appointment/provisioning authority.
18. Whether initial setup requires SK or another formally accepted governing source.
19. Whether any separate checker/verification role is required in addition to SuperAdmin.
20. Policy effective-date and transition behavior.
21. Behavior of future-dated policy amendments if a new program starts before the effective date.
22. Offline request/approval authority.
23. Currency, precision, rounding, and accounting cut-off.
24. Program–Incident–Operation relationship cardinalities.
25. Policy scope continuity across multiple programs.

For each decision provide:
- Decision ID.
- Exact question.
- Options.
- Consequence of each option.
- Required evidence.
- Proper decision owner or `OWNER TO BE DESIGNATED`.
- Current status.
- Whether it blocks logical finalization or physical design.

Do not make the decision on behalf of the organization.

---

# 19. RISK REGISTER — MINIMUM RISKS

Include and assess at least:

- Policy changes while a program is active.
- SuperAdmin bypass.
- Missing/invalid SK.
- Fake, unrelated, superseded, or unverifiable SK.
- Policy version overwritten.
- Historical transaction reinterpreted.
- Policy change race with program activation.
- Program administratively closed but financial obligations remain.
- Incorrect program-status mapping.
- Global scope reset without authority.
- Incident splitting to multiply ceilings.
- Duplicate incident records.
- Duplicate request/disbursement.
- Reservation/disbursement double counting.
- Refund/reversal deleting history.
- Concurrent requests exceeding ceiling.
- Concurrent requests exceeding cash.
- Restricted cash treated as eligible.
- Stale cash balance.
- Offline duplicate sync.
- Orphaned ledger event.
- Missing correlation/causation reference.
- Cross-module policy copies diverging.
- Unauthorized document replacement.
- Audit trail tampering.
- False claim that a test passed.
- Incorrect report derived from non-canonical data.

For each risk include:
- Risk ID.
- Scenario.
- Likelihood and impact rationale.
- Preventive control.
- Detective control.
- Recovery.
- Evidence required.
- Status.

Do not invent numerical risk scores without a defined scoring method.

---

# 20. READINESS GATE

At the end, assess whether Finance is ready for logical design finalization and whether physical database design may begin.

Use only these statuses:

- `READY`
- `CONDITIONAL`
- `BLOCKED`
- `BLOCKED_BY_MISSING_SOURCE`
- `NO_GO`

At minimum assess:

- Owner clarification.
- SOP reconciliation.
- Initial policy authority.
- Master Policy governance.
- Policy freeze gate.
- SK evidence model.
- SuperAdmin access.
- No-override control.
- Program lifecycle mapping.
- Financial closure definition.
- Policy scope identity.
- Incident/operation control unit.
- Consumption event semantics.
- Consumption ledger.
- Cash movement model.
- Eligible cash policy.
- Transaction lifecycle.
- Idempotency.
- Concurrency.
- Offline behavior.
- Logical entity relationships.
- Cross-module contracts.
- Test design.
- Actual test execution evidence.
- Repository/code inspection availability.
- Physical database design readiness.

Do not mark Finance `READY` merely because a logical diagram exists.

**Physical schema and implementation must remain `NO_GO` if policy-critical decisions, legal basis, lock behavior, transaction semantics, or data relationships remain unresolved.**

---

# 21. RECOMMENDATION FOR 00.12

Recommend the next stage based on actual findings.

Possible next stage may include:
- Policy and governance decision workshop.
- Finance domain model finalization.
- Finance logical data model review.
- Finance accounting policy clarification.
- Program/Incident relationship decision.
- Source document collection.
- Test specification refinement.

Do not automatically recommend physical database design if readiness gates remain blocked.

---

# 22. FINAL NON-NEGOTIABLE PRINCIPLES

The report must preserve these principles:

1. **No Legal Basis, No Policy Change.**
2. **No Active Program, No Unresolved Obligation, and No Pending Policy Lock Blocker before an amendment can proceed.**
3. **No SuperAdmin Override while the policy is locked.**
4. **SuperAdmin executes an authorized decision; SuperAdmin does not create organizational authority.**
5. **Every policy amendment must record the official SK/decision number, date, issuer, subject, original document, effective date, and change reason.**
6. **Every policy amendment creates a new immutable policy version.**
7. **Historical policy versions and transactions are never silently overwritten or reinterpreted.**
8. **The active policy is frozen during operations.**
9. **The backend enforces the lock; hiding a menu is not sufficient.**
10. **Policy amendment and program activation must be race-safe and atomic.**
11. **Ceiling consumption, cash movement, and expense recognition are separate logical concerns.**
12. **Reservation-to-disbursement conversion must not double count.**
13. **Retries and offline synchronization must be idempotent.**
14. **Concurrent requests must not consume the same ceiling or cash twice.**
15. **No implicit reset of global scope or consumption.**
16. **No automatic merge or deletion of duplicate incidents/transactions.**
17. **Every critical transaction must retain source, correlation, causation, policy-version, and audit references.**
18. **No test is reported as passed without execution evidence.**
19. **No source conflict is silently resolved by the developer or AI.**
20. **No physical implementation begins while policy-critical design gates remain blocked.**

## Final instruction

Be rigorous, skeptical, and explicit. Prefer a clearly documented `PENDING_ORG_DECISION` over an invented rule. Prefer a blocked activation over an ambiguous policy. Prefer immutable evidence and traceable correction over silent data modification.

The goal is not to produce the longest possible document. The goal is to produce a logically complete, auditable, implementable Finance foundation that will not create duplicate transactions, conflicting policy states, circular workflows, orphaned relationships, incorrect financial totals, or operational dead ends.

**End of Prompt 00.11.**
