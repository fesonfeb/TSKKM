# SIM-TDB — PROMPT 00.11
## Finance Logical Integrity, Transaction Control, and Master Policy Governance Hardening

**Document ID:** SIMTDB-REV05112026-00-11-FIN-PROMPT  
**Filename:** `SIMTDB_REV05112026_00_11_FINANCE_LOGICAL_INTEGRITY_AND_TRANSACTION_CONTROL_PROMPT_R01.md`  
**Revision:** REV05112026-R01 (owner-approved governance clarification and 00.12 audit reconciliation)  
**Project:** Sistem Informasi Manajemen Tanggap Darurat Bencana (SIM-TDB)  
**Organization:** Caritas Keuskupan Malang — Tim Solidaritas Kemanusiaan Keuskupan Malang (TSKKM)  
**Primary inputs:** `SIMTDB_REV05112026_00_10_FINANCE_FOUNDATION_REAUDIT.md`; `SIMTDB_REV05112026_00_12_AUDIT_PROMPT_00_11.md`; project-owner clarifications recorded after the 00.12 audit  
**Mode:** Independent re-audit, logical integrity hardening, transaction-control analysis, and test design  
**Implementation status:** NO IMPLEMENTATION — audit and logical design only
**Prompt revision note:** R01 supersedes the original R00 prompt for the next Copilot run. It incorporates the 00.12 audit and the project owner's subsequent explicit governance clarifications.

---

# A. INSTRUCTIONS TO GITHUB COPILOT

Act as a senior software architect, financial-systems analyst, database integrity specialist, security architect, and audit-minded systems engineer.

Your task is to conduct a deep, skeptical, evidence-based review of the existing SIM-TDB Finance foundation, reconcile the findings in the 00.12 audit of the original Prompt 00.11, incorporate the project owner's subsequent explicit clarifications, and produce the corrected 00.11 audit document.

Do not merely agree with the previous document. Challenge its assumptions, identify missing relationships, test edge cases, and distinguish confirmed requirements from technical recommendations and unresolved organizational decisions.

The target is a Finance foundation that can later be implemented in Emergent and operated reliably in the field, including poor connectivity, repeated submissions, concurrent users, interrupted workflows, and financial reconciliation.

## A.1 Required source inspection

Before writing the report:

1. Inspect the available project/workspace files and identify the exact 00.10 document.
2. Read `SIMTDB_REV05112026_00_10_FINANCE_FOUNDATION_REAUDIT.md` completely.
3. Inspect `SIMTDB_REV05112026_00_12_AUDIT_PROMPT_00_11.md` and reconcile its findings against the latest owner clarifications: the project owner has now explicitly approved the Master Policy freeze, the requirement that both programs and associated finances be completed before amendment, SuperAdmin-only setup/amendment, mandatory SK Pengaturan for amendments, and no SuperAdmin override. Inspect any available preceding 00.09 R01 prompt/result, owner clarification documents, Correction & Harmonization Register (especially CHR-020), and relevant SOP extracts if actually available in the workspace.
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

`SIMTDB_REV05112026_00_11_FINANCE_LOGICAL_INTEGRITY_AND_TRANSACTION_CONTROL_REAUDIT_R01.md`

Do not create additional files unless explicitly authorized later.

The report must contain logical models, candidate entity relationships, state-transition descriptions, test cases, risk analysis, and decision registers. It must not contain executable implementation changes.

## A.3 Evidence and provenance discipline

For every important statement, classify its origin. Use these labels consistently:

- `SOP_CONFIRMED`
- `CLARIFIED_BY_PROJECT_OWNER`
- `PROJECT_OWNER_GOVERNANCE_REQUIREMENT`
- `ORG_DECISION_CONFIRMED`
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

The project owner has explicitly approved the Master Policy governance requirements described in Section 2 through the conversation clarifications. Classify those requirements as `PROJECT_OWNER_GOVERNANCE_REQUIREMENT`; do not continue to label them `PENDING_OWNER_ACCEPTANCE`.

However, owner approval of the system requirement is not the same as proof that a particular organizational SK has been issued, that an issuer/signatory has been verified, or that an organizational delegation document exists. Do not label an actual formal organizational instrument as `ORG_DECISION_CONFIRMED` unless its evidence is available and verified.

Do not invent an SK number, date, issuing authority, signatory, policy approval, effective date, or actual legal document. The requirement to attach an SK Pengaturan for each amendment is approved; the actual SK for a future amendment must still be supplied and checked.

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

## 1.1 Latest owner clarification — controlling interpretation

The project owner has now expressly confirmed:
- The Master Policy must be established before activities begin.
- Policy setup/amendment is unavailable while any SIM-TDB program is still running or not formally closed.
- Even after programs are closed, policy amendment remains blocked until the associated financial matters are also complete.
- Only SuperAdmin may perform the policy setup/amendment.
- Every amendment requires an attached SK Pengaturan.
- The SK does not permit amendment while the program/financial closure gate remains blocked.

These are `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` items. They supersede the 00.12 audit's earlier conclusion that these high-level governance choices were not yet approved by the project owner. The 00.12 audit remains useful for its technical and evidence-related findings; do not discard all of its findings merely because some governance provenance findings have now been resolved.



---

# 2. OWNER-APPROVED REQUIREMENT — MASTER POLICY GOVERNANCE, FREEZE, AND FORMAL AMENDMENT

The project owner has explicitly approved the governance direction below in the conversation. Treat these as mandatory project requirements for the SIM-TDB system design. They are not merely options awaiting owner acceptance.

Use provenance label `PROJECT_OWNER_GOVERNANCE_REQUIREMENT`.

This owner approval does not, by itself, prove that a formal organizational SK has already been issued. Actual SK evidence for a future amendment must be supplied when that amendment is performed.

## 2.1 Governing principle: rules must precede activities

**The organizational rules and Master Policy must be established first. Operational programs and activities may begin only after the applicable policy has been configured, approved for use, and activated.**

The system must not allow activities to run first and then permit policy-critical rules to be improvised or changed during execution.

The `PER_INCIDENT` versus `GLOBAL_ALL_INCIDENTS` selection is a foundational policy decision. It must be selected before operations begin and must not be treated as a casual operational toggle.

The same principle applies to policy-critical parameters designated by the organization, including where applicable:

- Emergency-fund ceiling amount.
- Aggregation mode.
- Control-unit definition.
- Global policy-scope boundary.
- Applicable fund-pool/source restrictions.
- Policy effective period.
- Other financial policy parameters formally designated as policy-critical.

Do not automatically classify every ordinary master-data record as a Master Policy. Distinguish policy-critical configuration from ordinary operational master data.

## 2.2 Initial setup before program activation

- Initial Master Policy setup must be completed before the first operational program is activated.
- Initial setup is performed only by the authorized SuperAdmin capability.
- The initial configuration must reference its governing source, such as the applicable SOP, approved policy, or formal organizational decision actually available.
- Record the source document identity and location/page where applicable.
- Do not invent a nominal value or mode.
- Rp50,000,000 remains a reference candidate only until the organization formally approves the initial configuration.
- Rp100,000,000 must never become an automatic default because it appears in an example.
- The SuperAdmin is the technical/administrative executor of the approved organizational rules, not the person who independently creates organizational policy.

If no valid initial policy has been established and activated, program activation must be blocked. Do not permit an operational program to start with an undefined, missing, or ambiguous policy.

The owner has specifically approved SuperAdmin as the system capability that performs initial setup and controlled policy changes. The actual account identity, provisioning, and access security must still follow the organization's authorized account-management process.

## 2.3 Full policy freeze during operational programs

Once an operational program has started, the active Master Policy is frozen.

**No user — including SuperAdmin — may change the active policy amount, aggregation mode, scope, or other locked policy-critical parameters while any SIM-TDB operational program is running or has not been formally closed.**

The freeze is system-wide for the policy governance area; do not silently narrow it to one incident, one response operation, or one fund pool unless the project owner later changes this requirement.

A program that is paused, suspended, on hold, closing, or awaiting formal closure is not considered fully completed. It continues to block policy amendment.

## 2.4 Financial completion is an independent mandatory gate

Program completion alone is insufficient.

**Policy amendment remains blocked until both conditions are satisfied:**

1. All relevant SIM-TDB programs have been formally completed/closed; and
2. All financial transactions, obligations, accountability, and reconciliations associated with those programs have been completed and resolved.

At minimum, analyze these financial blockers:

- Fund request pending review or approval.
- Approved amount still reserved.
- Payment instruction outstanding.
- Advance/cash advance not yet accounted for.
- Disbursement not reconciled.
- Refund, reversal, correction, or disputed transaction unresolved.
- Required financial report or accountability document outstanding.
- Outstanding payable, commitment, or other policy-linked financial obligation.
- Any other unresolved financial record required by the approved Finance closure process.

Do not assume exact status names or accounting treatments are already defined. Map actual source vocabulary where available. If unavailable, mark exact status mapping, source-of-truth, closure evidence, and closure authority as `PENDING_DESIGN_DECISION` or `PENDING_ORG_DECISION`. The high-level requirement that program and finance must both be complete is already approved and must not be reopened as an owner-acceptance question.

Do not use a simple `program.status = completed` check as the sole unlock condition. Program closure and financial closure are separate mandatory gates.

## 2.5 Policy setup menu behavior while locked

While any program is running/not formally closed, or any related financial obligation remains unresolved:

- The policy setup/amendment menu must be unavailable for editing.
- The menu may be hidden or displayed as locked with a clear explanation; the exact UI presentation is a design choice.
- An authorized read-only view of the active policy may remain available.
- No policy draft, amendment submission, amount editor, mode selector, scope editor, or activation action may be initiated through the application while the gate is locked.
- SuperAdmin must not receive an override button.
- Direct API calls, alternate routes, browser manipulation, client-side state changes, or replayed requests must not bypass the backend lock.
- The backend must independently evaluate the gate on every policy-changing operation.
- Hiding the menu is only a UI behavior; server-side/domain-level enforcement is mandatory.

This is not merely a restriction on activation. During the locked period, the policy change/setup function itself is unavailable through the application. Preparing an SK outside the application does not unlock the policy menu.

## 2.6 No SuperAdmin override

This rule is mandatory:

**SuperAdmin cannot bypass the policy freeze while any program remains unclosed or any relevant financial obligation remains unresolved.**

An attached SK does not override the lock gate. The SK is a mandatory basis for a permitted amendment after the gate becomes clear; it is not an exception that allows policy change during an active program or unfinished financial closure.

Do not create:
- Emergency override.
- Force unlock.
- Admin bypass.
- Hidden route.
- Direct database-edit workaround.
- Special permission that defeats the lock.
- A policy amendment path that activates a new version during the locked period.

If the organization later changes this principle, that change must be handled as a new formally approved governance requirement. Do not invent an exception in this task.

## 2.7 Conditions to reopen policy setup

The policy setup/amendment function may become available only after all of the following are true:

1. No SIM-TDB operational program remains running.
2. Every program has reached its formally accepted terminal/closed state; paused, suspended, on-hold, and closing states do not qualify.
3. All financial transactions and obligations associated with the programs are completed.
4. All required reconciliations and accountability evidence are complete.
5. No unresolved policy-linked transaction remains.
6. The system can produce a traceable lock-eligibility result showing why the gate is clear.
7. A valid SK Pengaturan for the proposed amendment is available and attached before the amendment is activated.

Passing the gate makes the amendment workflow eligible; it does not itself change the policy. The amendment must still be performed by SuperAdmin with the required SK evidence and a complete audit trail.

The exact status mapping, canonical data sources, evidence of closure, and person/authority that certifies financial completion remain implementation/governance details to be resolved from source documents. Do not weaken the approved two-part gate while investigating those details.

## 2.8 Policy amendment workflow after the gate is clear

Only after all programs are formally closed and all associated finances are complete:

1. SuperAdmin accesses the policy setup/amendment menu.
2. SuperAdmin provides the SK Pengaturan.
3. The application requires the SK number, date, issuing authority, subject/title, relevant decision summary, original document attachment, effective date, and reason for change.
4. The application links the prior policy version automatically.
5. The application generates a before/after comparison.
6. The system validates the lock gate again at the authoritative transaction boundary.
7. The system validates required SK fields and records verification status/evidence.
8. A new immutable policy version is created and activated only after all required checks pass.
9. The old policy version and all historical transactions remain unchanged and traceable.

The exact human verification responsibility for the SK may be mapped from organizational evidence. Do not invent an additional organizational role or assume that a file upload alone proves legal authenticity.

## 2.9 Race-condition protection

Analyze the race condition where:
- SuperAdmin begins a policy amendment while an operator attempts to activate a new program; or
- A program activation begins while a policy amendment is being activated.

These operations must be serialized or protected by an equivalent atomic mechanism.

The system must never allow:
- A new program to start using a half-updated policy.
- A policy to change after a program has started.
- A policy lock check to pass using stale status data.
- A program to activate without exactly one valid active policy version.
- Two concurrent policy amendments to create conflicting active versions.
- A program activation and policy amendment to commit incompatible states.

Describe the logical transaction boundary, lock acquisition, re-check, commit, and rollback behavior. Do not implement code or choose a database-specific mechanism at this stage.

# 3. MANDATORY SK PENGATURAN — NO SK, NO POLICY AMENDMENT

The project owner has explicitly approved the requirement that every change to Master Policy must be supported by an attached SK Pengaturan.

Classify this as `PROJECT_OWNER_GOVERNANCE_REQUIREMENT`.

Do not weaken this requirement by treating a free-form reason, chat message, email, verbal instruction, or ordinary administrative note as a substitute for the required SK Pengaturan. If the owner later changes this rule, that must be recorded as a new owner-approved requirement.

## 3.1 Mandatory amendment evidence

Every amendment to an existing Master Policy must have, at minimum:

| Field | Requirement |
|---|---|
| Document type | `SK_PENGATURAN` |
| SK number | Required; exact official number |
| SK date | Required |
| Issuing organization/authority | Required |
| Signatory/name and position | Capture where stated in the SK |
| Decision subject/title | Required |
| Relevant decision summary | Required |
| Original SK document attachment | Required |
| Policy effective date | Required and must be consistent with the SK |
| Change reason/context | Required |
| Previous policy version | System-linked, not manually typed as source of truth |
| Proposed new policy version | System-generated draft/version reference |
| Changed fields | System-generated before/after comparison |
| SuperAdmin actor | Automatically captured from authenticated identity |
| Submission/activation timestamp | System-generated |
| Verification status | Required lifecycle field |
| Verification evidence/notes | Captured where verification is performed |

Do not create fake examples that could be mistaken for real SK records. If examples are needed, visibly label them `ILLUSTRATIVE — NOT A REAL SK`.

The SK requirement applies to policy amendments. For initial setup, reference the actual governing SOP/policy/decision available to the organization; do not invent an SK or assume that an amendment SK already exists.

## 3.2 SK validation

Design validation that checks:

- SK number is present.
- SK date is present and valid.
- Issuing authority is identified.
- Signatory/position is captured where stated.
- Subject is relevant to the proposed policy change.
- Original document is attached, readable, and retrievable.
- Effective date is coherent with the SK.
- The SK has not been superseded, revoked, or expired, if such information is available.
- The document is not being reused as an unrelated basis for another policy change.
- The policy fields being changed are within the subject and scope of the SK.
- The amendment cannot activate while the program/financial closure gate is blocked.

A file upload alone does not prove authenticity or legal sufficiency. The system must preserve the evidence and its verification status. The person/authority responsible for substantive SK verification must be identified from organizational evidence; do not invent that authority.

If the SK is missing, incomplete, unrelated, rejected, or not verified to the required level, the amendment must not activate.

## 3.3 Evidence integrity

Recommend a logical evidence model that preserves:

- Original uploaded SK file.
- File name and media type.
- File size.
- Upload actor and timestamp.
- Cryptographic checksum/hash as a technical recommendation.
- Document reference/identifier.
- Verification actor, date, result, and notes where applicable.
- Supersedes/revokes relationship, if relevant.
- Policy amendment record that relies on the document.

Do not overwrite the original SK attachment. A replacement/corrected document must be stored as a new evidence version or linked record.

## 3.4 SK and amendment audit trail

Every amendment must preserve:

- Old policy version.
- New policy version.
- Old and new values for every changed field.
- SK number and date.
- Issuer, signatory where stated, and subject.
- Original document reference.
- Effective date.
- Change reason.
- SuperAdmin identity.
- Verification/approval evidence where applicable.
- Time of each lifecycle event.
- Program/financial lock-gate result at the time of amendment.

Audit records must be append-only from the application's normal permission model. No ordinary administrator or SuperAdmin UI action may delete or rewrite historical amendment evidence.

Do not claim absolute tamper-proof storage unless the underlying infrastructure has been inspected and verified. Describe logical integrity requirements and additional infrastructure controls as recommendations.

## 3.5 Initial setup versus amendment

Distinguish clearly:

- Initial Master Policy setup before any program starts: based on the governing SOP/policy/decision actually adopted and available.
- Amendment of an existing Master Policy: requires the SK Pengaturan and all mandatory lock-gate conditions.
- A future SK cannot bypass an active program or unfinished financial closure.
- A new policy version cannot reinterpret or overwrite historical transactions.

# 4. SUPERADMIN ROLE AND ACCESS CONTROL

## 4.1 Owner-approved capability and intended use

The project owner has approved SuperAdmin as the only system capability permitted to perform:
- Initial Master Policy setup before the first operational program is activated.
- Policy amendment after all programs are formally closed and all associated financial obligations/reconciliations are complete, with the required SK Pengaturan attached.
- Other explicitly approved core-system bootstrap functions, if separately specified.

This is a `PROJECT_OWNER_GOVERNANCE_REQUIREMENT`.

SuperAdmin is not an everyday operational account and is not the person who creates organizational policy. SuperAdmin executes the established organizational rules and formal SK Pengaturan in the application.

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

The project-owner approval establishes the SuperAdmin capability in the system design. The actual account identity, provisioning, recovery, and revocation process must follow the organization's authorized account-management procedure.

## 4.3 No hidden bypass

Verify the logical design against these bypass attempts:

- Direct URL access to the policy editor.
- Calling an API endpoint without using the UI.
- Changing browser/client state.
- Replaying an old request.
- Reusing another user's session.
- Calling a stale policy-version endpoint.
- Submitting a policy change while a program is running or not formally closed.
- Submitting a policy change while financial closure is incomplete.
- Submitting an amendment without an attached SK Pengaturan.
- Concurrently starting a program and activating a new policy.

Every attempt must be rejected at the authoritative backend/service layer when the gate or authorization is not satisfied.

# 5. POLICY LIFECYCLE AND FREEZE STATE MODEL

Create a logical lifecycle model. Candidate state names may be proposed, but mark them as technical recommendations until accepted.

At minimum analyze:

1. `INITIAL_DRAFT`
2. `INITIAL_SETUP_VALIDATION`
3. `ACTIVE_LOCKED`
4. `AMENDMENT_ELIGIBLE`
5. `AMENDMENT_WITH_SK`
6. `SUPERSEDED`
7. `RETIRED`
8. `REJECTED`
9. `CANCELLED`

Do not treat these candidate labels as already approved organizational terminology.

The workflow must respect the following owner-approved sequence:

- Initial policy setup is completed before program activation.
- Once a program starts, policy setup/amendment is locked and unavailable through the application.
- Policy setup/amendment remains locked until every program is formally closed AND all associated financial obligations, transactions, and reconciliations are complete.
- Only after both closure gates pass may SuperAdmin access the amendment function.
- An amendment requires the SK Pengaturan.
- The SK does not bypass the closure gates.
- Every successful amendment creates a new immutable version.
- Historical policy versions and transactions remain unchanged.

For each transition specify:
- Who can initiate it.
- Preconditions.
- Required SK evidence for amendments.
- Program closure gate.
- Financial closure gate.
- Resulting active policy version.
- Audit event.
- Whether rollback is allowed.
- What happens to programs/requests already referencing the previous version.

## 5.1 Lock eligibility matrix

Create a detailed matrix:

| Condition | Policy change eligibility |
|---|---|
| No program has started; initial setup not yet completed | Initial setup may proceed through SuperAdmin with valid governing source |
| At least one program is active/in progress | Block |
| Program is paused/suspended/on hold | Block; not formally completed |
| Program is closing but not formally closed | Block |
| All programs appear closed but a financial obligation remains open | Block |
| Program is complete but an advance is outstanding | Block |
| Program is complete but payment is outstanding | Block |
| Program is complete but reconciliation is pending | Block |
| Program and finance closure are complete, but SK Pengaturan is missing | Block |
| Program and finance closure are complete, SK is attached, and SuperAdmin is authorized | Eligible for controlled amendment |
| SuperAdmin attempts override while any blocker exists | Block |
| A new program activation races with policy amendment | Serialize; only one operation may commit under a consistent policy state |

Map actual source status names where available. If not available, mark exact status mapping as pending; do not weaken the high-level two-part closure requirement.

## 5.2 Lock eligibility report

Design a logical `Policy Lock Eligibility Report` showing:

- Evaluation timestamp.
- Active policy version.
- Program count by blocking status.
- Program references that are not formally closed.
- Pending request count.
- Reserved amount.
- Outstanding payment count/amount.
- Outstanding advance count/amount.
- Unreconciled disbursement count/amount.
- Pending refund/reversal/correction count.
- Missing accountability documents.
- Source-of-truth module/record for each blocker.
- Owner module for each blocker.
- Final list of blockers.
- Overall result: `LOCKED` or `ELIGIBLE_FOR_AMENDMENT`.

The report must be derived from canonical records, not manually maintained counters. Treat the report as a technical recommendation for traceability; determine its access permissions and data minimization requirements. A missing/unavailable source module must not be interpreted as proof that no blocker exists.

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
| FIN-TEST-50 | SuperAdmin attempts policy change with no SK Pengaturan number | Blocked |
| FIN-TEST-51 | SK Pengaturan number exists but date, issuer, subject, or original attachment is missing | Blocked |
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
| FIN-TEST-78 | Policy change has valid SK Pengaturan but any program or financial closure gate is not clear | Blocked; SK does not bypass the owner-approved freeze |
| FIN-TEST-79 | No valid SK Pengaturan but all programs and obligations are closed | Blocked; clear gate alone does not authorize policy change |
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

### Additional mandatory governance tests: FIN-TEST-81 onward

| ID | Required scenario | Expected control |
|---|---|---|
| FIN-TEST-81 | No program is currently executing, but one program is paused/suspended/on hold and not formally closed | Policy amendment remains blocked |
| FIN-TEST-82 | All programs are formally closed, but a financial reconciliation remains pending | Policy amendment remains blocked |
| FIN-TEST-83 | All programs are closed, all associated finances are complete, SK Pengaturan is valid/attached, and SuperAdmin initiates amendment | Amendment may proceed through controlled validation and new version creation |
| FIN-TEST-84 | All closure gates pass and SK is attached, but a non-SuperAdmin attempts amendment | Denied server-side |
| FIN-TEST-85 | No active policy exists and a user attempts to activate a program | Program activation is blocked |
| FIN-TEST-86 | A valid SK Pengaturan is attached while a program remains active | Amendment remains blocked; SK does not bypass the lock |
| FIN-TEST-87 | All programs and finances are closed, but SK is missing, revoked, expired, or unrelated to the proposed change | Amendment is blocked |
| FIN-TEST-88 | Program closure is recorded, but an advance, outstanding payment, or unresolved refund remains | Amendment remains blocked |
| FIN-TEST-89 | Policy setup menu is accessed while a program or financial blocker exists | Menu is unavailable for editing; direct backend/API attempt is denied |
| FIN-TEST-90 | A source module needed to determine program/financial closure is unavailable or stale | System must not assume the gate is clear; amendment remains blocked or enters an explicit unresolved evaluation state |
| FIN-TEST-91 | All programs and finances are complete, but the SK effective date conflicts with the proposed policy activation date | Amendment is blocked pending correction |
| FIN-TEST-92 | Policy amendment and program activation occur at the same time after the gate initially appears clear | Atomic re-check/serialization ensures only a consistent operation commits |

For each additional test include the same 12 test fields required in Section 14.2. Actual result remains `not executed` unless execution evidence exists.

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

`SIMTDB_REV05112026_00_11_FINANCE_LOGICAL_INTEGRITY_AND_TRANSACTION_CONTROL_REAUDIT_R01.md`

The report must be written in formal, precise Indonesian with English technical terms where appropriate.

Use this structure:

1. Executive Summary.
2. Scope, Source Inventory, and Evidence Availability.
3. Audit Method and Limitations.
4. Provenance / Source Authority Matrix.
5. Updated Owner Clarification and Governance Requirement Register.
6. Disposition of AUD-11-01 through AUD-11-14 from `SIMTDB_REV05112026_00_12_AUDIT_PROMPT_00_11.md`: resolved, partially resolved, still valid, or pending.
7. 00.10 Findings: Confirmed, Corrected, and Still Open.
8. Master Policy Governance Principle.
9. Policy Freeze / Lock-Gate Model.
10. Formal SK Pengaturan and Amendment Evidence Model.
11. SuperAdmin Access and No-Override Control.
12. Policy Lifecycle and Version Transition.
13. Program/Incident/Response Operation/Policy Scope Logical Relationships.
14. Emergency Fund Consumption Ledger.
15. Eligible Cash and Cash Movement Control.
16. Fund Request to Reconciliation Lifecycle.
17. Idempotency, Duplicate Prevention, Correlation, and Concurrency.
18. Offline / Poor Connectivity Handling.
19. Logical ERD and Entity Registry.
20. Logical Data Dictionary.
21. Security and Auditability.
22. Failure Recovery and Reconciliation.
23. Cross-Module Contracts.
24. Corrected FIN-TEST-01 through FIN-TEST-46.
25. New FIN-TEST-47 onward.
26. Risk Register.
27. Decision Register.
28. Evidence Required from Organization / SOP / Finance.
29. Readiness Assessment.
30. Recommendation for the next stage after 00.11 R01.

Include:
- Mermaid diagrams.
- Tables.
- Explicit status labels.
- Decision owners only where evidence supports them; otherwise say `OWNER TO BE DESIGNATED`.
- A clear distinction between SOP text, project-owner-approved requirements, formal organizational decisions, and technical recommendations.
- A specific statement that the owner-approved governance rules are not `PENDING_OWNER_ACCEPTANCE`, while actual SK evidence, signatory authority, source status mapping, and organizational closure certification still require their own evidence.


# 18. REQUIRED DECISION REGISTER

Do not reopen decisions already explicitly approved by the project owner. Record the following as resolved project requirements:

| ID | Requirement | Status |
|---|---|---|
| GOV-01 | Master Policy must be established before operational programs begin | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| GOV-02 | Policy setup/amendment is unavailable while any program is running or not formally closed | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| GOV-03 | Policy amendment remains blocked until all programs are closed AND associated financial obligations/reconciliations are complete | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| GOV-04 | Only SuperAdmin may perform initial policy setup and eligible amendments | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| GOV-05 | Every policy amendment requires an attached SK Pengaturan with traceable official number/date and relevant document details | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| GOV-06 | SK Pengaturan does not override an active-program or unfinished-finance lock | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| GOV-07 | SuperAdmin has no override/bypass while policy is locked | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| GOV-08 | Historical policy versions and transactions must remain immutable and traceable | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |

Then create a separate pending Decision Register for details not yet established by available source evidence:

1. Formal reconciliation of SOP page 23 wording with later project-owner interpretation.
2. Initial policy amount and effective date.
3. Initial aggregation mode.
4. `PER_INCIDENT` control-unit definition.
5. `GLOBAL_ALL_INCIDENTS` scope boundary.
6. Global-scope reset/supersession rule.
7. Event that consumes the ceiling.
8. Eligible cash formula and canonical source.
9. Reservation and outstanding-payment treatment.
10. Funding-source/fund-pool cardinality.
11. Actual expenditure recognition.
12. Exact program status vocabulary and source records used to determine formal closure.
13. Evidence that makes a program formally closed.
14. Exact financial obligations that block policy amendment.
15. Canonical source records for each financial blocker.
16. Authority/person who certifies financial closure.
17. SK verification responsibility and verification evidence.
18. SuperAdmin account provisioning, recovery, and revocation process.
19. Whether an additional human verifier is required for SK evidence; do not assume one.
20. Whether initial setup requires an SK or another source already accepted by the organization.
21. Policy effective-date and transition behavior.
22. Behavior of any future-dated amendment if a new program is activated before its effective date.
23. Offline request/approval authority.
24. Currency, precision, rounding, and accounting cut-off.
25. Program–Incident–Operation relationship cardinalities.
26. Policy scope continuity across multiple programs.
27. Data freshness and fail-closed behavior when a source module is unavailable during lock evaluation.
28. Access rights and data minimization for the Policy Lock Eligibility Report.

For each pending decision provide:
- Decision ID.
- Exact question.
- Options.
- Consequence of each option.
- Required evidence.
- Proper decision owner or `OWNER TO BE DESIGNATED`.
- Current status.
- Whether it blocks logical finalization or physical design.

Do not make unresolved decisions on behalf of the organization. The high-level governance rules in the first table are already approved by the project owner and must not be returned as pending owner acceptance.

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
- Master Policy governance (owner-approved principle).
- Policy freeze gate (owner-approved principle; exact status mapping still to be evidenced).
- Mandatory SK Pengaturan for amendments (owner-approved principle; actual SK evidence must be supplied per amendment).
- SuperAdmin access (owner-approved capability; actual account provisioning remains to be arranged).
- No-override control (owner-approved principle).
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

# 21. RECOMMENDATION FOR THE NEXT STAGE AFTER 00.11 R01

Recommend the next stage based on actual findings.

Possible next stage may include:
- Reconciliation of the 00.12 audit findings against the now-confirmed owner-approved governance requirements.
- Program and financial closure source/status mapping.
- Policy and governance detail workshop for only the still-pending implementation decisions.
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

1. **Rules must be established before operational activities begin.**
2. **No program may activate without a valid, active, approved Master Policy.**
3. **No policy amendment while any SIM-TDB program is running or not formally closed.**
4. **No policy amendment until all programs are formally closed AND all associated financial transactions, obligations, accountability, and reconciliations are complete.**
5. **Only SuperAdmin may perform initial Master Policy setup and eligible amendments.**
6. **Every amendment requires an attached SK Pengaturan with traceable official number, date, issuer, subject, and original document.**
7. **An SK Pengaturan does not override the program/financial closure lock.**
8. **No SuperAdmin override, force unlock, hidden route, or direct database bypass while the policy is locked.**
9. **SuperAdmin executes the approved organizational decision; SuperAdmin does not independently create organizational authority.**
10. **Every policy amendment creates a new immutable policy version.**
11. **Historical policy versions and transactions are never silently overwritten or reinterpreted.**
12. **The backend enforces the lock; hiding a menu is not sufficient.**
13. **Policy amendment and program activation must be race-safe and atomic.**
14. **Ceiling consumption, cash movement, and expense recognition are separate logical concerns.**
15. **Reservation-to-disbursement conversion must not double count.**
16. **Retries and offline synchronization must be idempotent.**
17. **Concurrent requests must not consume the same ceiling or cash twice.**
18. **No implicit reset of global scope or consumption.**
19. **No automatic merge or deletion of duplicate incidents/transactions.**
20. **Every critical transaction must retain source, correlation, causation, policy-version, and audit references.**
21. **No test is reported as passed without execution evidence.**
22. **No source conflict is silently resolved by the developer or AI.**
23. **No physical implementation begins while policy-critical design details, transaction semantics, or data relationships remain unresolved.**

## Final instruction

Be rigorous, skeptical, and explicit. Treat the Master Policy governance requirements above as approved project-owner requirements, not as pending options. At the same time, do not claim that a specific organizational SK, signatory authority, closure certificate, or source-system status has been verified unless evidence is available.

Prefer a clearly documented `PENDING_ORG_DECISION` for genuinely unresolved organizational details. Prefer a blocked policy amendment over an ambiguous lock state. Prefer immutable evidence and traceable correction over silent data modification.

The goal is to produce a logically complete, auditable, implementable Finance foundation that will not create duplicate transactions, conflicting policy states, circular workflows, orphaned relationships, incorrect financial totals, or operational dead ends.

**End of Prompt 00.11 — Revision R01.**

## Final instruction

Be rigorous, skeptical, and explicit. Prefer a clearly documented `PENDING_ORG_DECISION` over an invented rule. Prefer a blocked activation over an ambiguous policy. Prefer immutable evidence and traceable correction over silent data modification.

The goal is not to produce the longest possible document. The goal is to produce a logically complete, auditable, implementable Finance foundation that will not create duplicate transactions, conflicting policy states, circular workflows, orphaned relationships, incorrect financial totals, or operational dead ends.

**End of Prompt 00.11.**
