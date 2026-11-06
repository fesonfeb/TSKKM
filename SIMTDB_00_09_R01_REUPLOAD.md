# SIM-TDB — FINANCE POLICY RECONCILIATION & LOGICAL DESIGN READINESS PROMPT

**Document ID:** SIMTDB-REV05112026-00-09-FIN  
**Filename:** `SIMTDB_REV05112026_00_09_FINANCE_POLICY_RECONCILIATION_AND_LOGICAL_DESIGN_READINESS_PROMPT.md`  
**Revision:** REV05112026-R01 (configurable emergency-fund policy update)  
**Project:** Sistem Informasi Manajemen Tanggap Darurat Bencana (SIM-TDB)  
**Organization:** Caritas Keuskupan Malang — Tim Solidaritas Kemanusiaan Keuskupan Malang (TSKKM)  
**Mode:** Read-only policy reconciliation, requirement provenance correction, and logical-design readiness preparation  
**Implementation:** PROHIBITED

---

# 1. ROLE AND MANDATE

Act as a Principal Enterprise Architect, Senior Finance Systems Analyst, Business Process Architect, Data Architect, Internal Control Specialist, and QA Lead.

Your task is to perform the next controlled review stage based on:

1. `SIMTDB_REV05112026_00_08_FINANCE_CLARIFICATION_REAUDIT_CORRECTED.md` — primary document to review.
2. `SIMTDB_REV05112026_00_07_FINANCE_OWNER_CLARIFICATION_AND_CORRECTION_PROMPT.md`.
3. Earlier Finance audit and clarification documents 00_02 through 00_06, if available.
4. Original SOP pages/images actually available in the workspace, especially printed page 23 and page 24.
5. The read-only execution guardrails.

Do not simply repeat the 00_08 audit. Perform a focused independent correction and prepare a decision-ready Finance policy reconciliation package.

Preserve valid findings. Do not silently change source wording, owner statements, organizational policy, or technical recommendations.

**Do not implement anything.** Do not write or modify application source code, database schema, migrations, seed data, API endpoints, configuration, workflow code, or deployment files. Do not execute mutating commands.

**Revision note:** This is an updated revision of the existing 00_09 prompt, not a new 00_10 prompt. It incorporates the project owner's new requirement that the emergency-fund amount and aggregation mode be configurable.

# 2. NON-NEGOTIABLE OWNER CLARIFICATIONS

The following statements are direct project-owner clarifications. Preserve their meaning and scope.

## 2.1 Rp100,000,000

Rp100,000,000 appearing in an example/template of emergency funding need is illustrative only.

It is not:
- A fixed amount.
- A mandatory amount.
- A maximum.
- A global cap.
- A default.
- An approval threshold.

Record this as `CLARIFIED_BY_PROJECT_OWNER`.

## 2.2 Configurable emergency-fund amount and aggregation scope

The earlier project-owner clarification identified Rp50,000,000 as the current maximum for one emergency incident/response operation. The project owner has now added an important architectural requirement:

**The emergency-fund amount and the scope over which that amount is aggregated must be configurable through a controlled Finance policy/master-data setup. They must not be permanently hardcoded in application code.**

The current Rp50,000,000 amount should be retained as the current reference/initial candidate configuration based on the earlier clarification. Do not assume that it must remain the permanent amount, and do not silently activate a new value or policy version without the required owner/organizational confirmation.

The authorized configuration must allow selection of one of these modes:

### Mode A — `PER_INCIDENT`

- The configured amount is the maximum cumulative emergency-fund limit for each defined incident/response-operation control unit.
- Different incidents have separate limits.
- Example with a configured amount of Rp50,000,000: Incident A may use up to Rp50,000,000 and Incident B may independently use up to Rp50,000,000, subject to eligible cash and all applicable approvals.
- Aggregate expenditure across distinct incidents may exceed Rp50,000,000.
- Multiple vouchers, sectors, activities, users, or transactions within the same control unit must not reset the limit.

### Mode B — `GLOBAL_ALL_INCIDENTS`

- The configured amount is one shared cumulative emergency-fund ceiling for all incidents within the defined policy scope.
- Example with a configured amount of Rp50,000,000: if Incident A consumes Rp20,000,000 and Incident B consumes Rp15,000,000, only Rp15,000,000 remains for other incidents in that same policy scope.
- The ceiling is shared across the included incidents; it is not a separate Rp50,000,000 allowance for each incident.
- The scope boundary must be defined (for example, one emergency-response activation, one response period, one program, one financial year, or another approved unit). Do not assume the global ceiling applies forever or automatically resets at a calendar boundary.

### Important distinction

The selected mode changes the meaning of the configured amount:

- `PER_INCIDENT`: configured amount applies separately to each defined incident/operation control unit.
- `GLOBAL_ALL_INCIDENTS`: configured amount applies once cumulatively across all incidents within the configured policy scope.

Do not apply both modes simultaneously unless the project owner explicitly approves a future `HYBRID` policy with both per-incident and global ceilings. Do not invent a hybrid mode as the default.

For either mode:
- The configured amount is a ceiling, not a mandatory spending target.
- Actual disbursement is also constrained by genuinely available eligible cash in the relevant fund pool.
- Funding-source restrictions and approval authority continue to apply.
- A configured ceiling does not itself prove that cash exists.
- The configured amount and scope are policy data, not constants embedded in code.

Record the latest configurability and mode-selection requirement as `CLARIFIED_BY_PROJECT_OWNER`. Preserve provenance for the earlier Rp50,000,000 reference amount separately.

## 2.3 General program/activity budget flexibility

The project owner previously clarified that example financial amounts are not universal fixed amounts and that program/activity amounts may be adjusted to actual needs.

Preserve this clarification for general program/activity budgeting.

Do not confuse:
- General program/activity budget, which is determined by actual program/activity needs and applicable approvals/source restrictions.
- The configurable emergency-fund ceiling, whose amount and aggregation mode are set through controlled policy configuration.
- Eligible available cash, which is a separate financial constraint.

The emergency-fund ceiling must not automatically be applied to unrelated program/activity budgets. Conversely, general budget flexibility does not bypass the configured emergency-fund ceiling when an expenditure is classified as covered by that emergency-fund policy.

## 2.4 Traceability

The owner has required financial data to be traceable. Preserve this at the level actually stated.

Do not silently expand it into a fully approved accounting architecture, exact event model, specific table structure, or final source-of-truth implementation.

## 2.5 Controlled policy/master-data configuration — new requirement

Design a controlled configuration capability, provisionally named `Emergency Fund Policy Configuration`.

This should be managed through Finance setup/master data or a dedicated policy-configuration area. Do not treat it as an ordinary editable lookup list available to every user.

At minimum, analyze these configuration attributes:

| Attribute | Purpose | Requirement/status |
|---|---|---|
| Policy ID/code | Stable identity of the policy configuration | `TECHNICAL_RECOMMENDATION` |
| Policy name/description | Human-readable policy name | `TECHNICAL_RECOMMENDATION` |
| Configured ceiling amount | Amount of the emergency-fund ceiling | Configurable; current reference amount Rp50m |
| Currency | Currency for the ceiling | Default currency and multi-currency needs require confirmation |
| Aggregation mode | `PER_INCIDENT` or `GLOBAL_ALL_INCIDENTS` | Required selectable configuration |
| Policy scope/boundary | Defines which incidents are aggregated together | Required; exact boundary is `PENDING_OWNER_DECISION` |
| Applicable fund pool/source | Identifies which eligible funds the policy controls | Required relationship; exact model pending |
| Effective-from date/time | Prospective activation date | `TECHNICAL_RECOMMENDATION` |
| Effective-to date/time | Optional expiry/supersession | `TECHNICAL_RECOMMENDATION` |
| Version number | Distinguishes policy revisions | `TECHNICAL_RECOMMENDATION` |
| Status | Draft, pending approval, active, superseded, retired, or another approved lifecycle | Proposed statuses only; approval lifecycle pending |
| Created/updated metadata | Actor and timestamp | `TECHNICAL_RECOMMENDATION` |
| Approval evidence | Who authorized the configuration and by what record | Governance requirement; authority evidence pending |
| Change reason | Explains why the amount/scope changed | `TECHNICAL_RECOMMENDATION` |
| Audit history | Retains previous values and who changed them | `TECHNICAL_RECOMMENDATION` |

### Configuration governance

- Only specifically authorized users may create or change policy configurations.
- Permission to edit ordinary Finance records must not automatically grant permission to change the emergency-fund policy.
- Separate policy maintenance from policy approval where organizational governance requires separation of duties.
- Keep a complete audit trail of old value, new value, old mode, new mode, actor, timestamp, reason, approval evidence, and effective date.
- Do not overwrite historical policy versions.
- Changes should normally be prospective. Do not retroactively change the limit applied to an already processed incident/request unless a formally approved migration/transition rule explicitly permits it.
- The policy version applied to each relevant request/incident must be traceable.
- Analyze how active incidents behave when a new policy version becomes effective. Do not assume whether they retain the old version or move to the new version; record the decision required.
- Do not allow two active configurations with overlapping scope/effective periods to create ambiguous policy selection.
- Define validation for positive amounts, currency precision, date ranges, and mutually exclusive scope modes.
- Do not allow a normal user to bypass a policy limit by editing a transaction or incident record.

### Master data versus transaction data

Keep the policy configuration separate from:
- Incident/operation records.
- Emergency-fund requests.
- Disbursements.
- Cash balances.
- Funding-source restrictions.
- General program/activity budgets.

The policy configuration defines the rule. Transactions record what happened. Cash records establish what is actually available. Reports derive values from their canonical sources.

The exact data entities and UI are logical-design topics only; do not create physical tables or code in this task.


# 3. REQUIRED PROVENANCE CORRECTION

Audit every item in the 00_08 Owner Clarification Register and Financial Business Rule Register.

## 3.1 Direct owner statements

At minimum, preserve these direct statements and their chronology:
- Rp100m appearing as an example is illustrative only; it must not become a fixed amount or automatic system rule merely because it appears in a template.
- The earlier clarification identified Rp50m as the maximum for one incident/response operation.
- The latest clarification adds that the emergency-fund amount must be configurable and the aggregation mode must be selectable between `PER_INCIDENT` and `GLOBAL_ALL_INCIDENTS`.
- In `PER_INCIDENT` mode, distinct incidents may each use up to the configured per-incident ceiling, subject to eligible available cash and applicable approvals.
- In `GLOBAL_ALL_INCIDENTS` mode, one configured ceiling is shared cumulatively across all incidents within the defined policy scope.
- Actual expenditure is constrained by eligible available emergency cash regardless of aggregation mode.
- The configured amount may change in the future through controlled policy configuration; it must not be permanently hardcoded.
- General program/activity financial amounts are flexible according to actual needs, subject to applicable rules.
- Financial data must be traceable.

Do not retain the older statement “Rp50m is not a global cap” as an unconditional rule. The latest owner requirement expressly permits a configurable `GLOBAL_ALL_INCIDENTS` mode. The correct rule is that the active configuration determines whether the ceiling is per incident or shared globally across the defined policy scope.

## 3.2 Statements that must not automatically be labeled direct owner clarification

Review and reclassify, unless exact owner evidence is present:
- Proposed/approved/actual/remaining budget lifecycle.
- Five-category budget model.
- Budget revision metadata (reason, actor, timestamp, approval reference).
- Exact workflow states for budget revisions.
- Exact canonical actual-expenditure source.
- Exact cash reservation mechanics.
- Exact funding-source cardinality.
- Exact remaining-budget formula.
- Approval authority matrix.
- Concurrency/locking/idempotency implementation.
- Exact incident/operation parent-child cardinality.

Use the appropriate status:
- `PROJECT_REQUIREMENT_STATED_IN_ADDENDUM`
- `TECHNICAL_RECOMMENDATION`
- `PENDING_OWNER_ACCEPTANCE`
- `PENDING_DESIGN_DECISION`
- `PENDING_ORG_DECISION`
- `SOP_CONFIRMED`
- `SOURCE_CONFLICT`
- `EVIDENCE_NOT_AVAILABLE`

Do not use `CLARIFIED_BY_PROJECT_OWNER` merely because an idea is sensible or appeared in an earlier assistant recommendation.

## 3.3 Specific 00_08 corrections

Review these entries explicitly:

- OCL-07 (“flexibility does not change approval authority”): unless direct owner evidence exists, reclassify as a governance/control recommendation or derive it from verified SOP/formal delegation evidence. Do not call it a direct owner clarification by assumption.
- FIN-BR-OWNER-09: preserve the direct statement that program/activity amounts are flexible according to needs. Separate additional conditions such as disaster circumstances, funding source, and approved budget unless each has its own evidence.
- FIN-BR-OWNER-10: separate proposed/approved/revision/actual/remaining budget lifecycle as a technical or project requirement unless direct owner acceptance is evidenced.
- FIN-BR-OWNER-11: revision history metadata must not be called owner policy without evidence.
- FIN-BR-OWNER-12: preserve traceability as owner clarification, but do not invent its full implementation.
- FIN-BR-OWNER-13: “actual figures must come from recorded and authorized actual data” must be classified according to its real source; do not assume it was a direct owner statement.

For every corrected rule, show:
1. Exact statement.
2. Evidence/source.
3. Provenance status.
4. Scope.
5. Technical implication.
6. Pending decision, if any.

# 4. RECONCILE SOP PAGE 23 — DO NOT ASSUME A CONFLICT

The 00_08 document records a possible `SOURCE_CONFLICT` between the visible wording on SOP printed page 23 and the latest owner clarification.

Re-examine the original SOP image if it is actually available.

Required evidence:
- Verbatim transcription of the complete relevant sentence.
- At least the preceding and following sentence/paragraph.
- Printed page number and document version, if visible.
- The exact grammatical object of Rp50,000,000:
  - Initial emergency fund amount?
  - Maximum expenditure?
  - Per-incident allocation?
  - General fund balance?
  - Another meaning?
- The exact wording concerning approval by Ketua TSKKM.
- A clear distinction between what the SOP literally says and what the owner clarified later.

Do not rely on a prior summary or paraphrase when the original image is available.

Classify the relationship accurately:
- If the complete SOP wording and owner clarification are consistent, remove the conflict and explain why.
- If the wording is genuinely inconsistent, retain `SOURCE_CONFLICT` and specify the exact conflicting phrases.
- If the image is not sufficiently legible or unavailable, use `EVIDENCE_NOT_AVAILABLE` or `BLOCKED_BY_MISSING_SOURCE`; do not assert a confirmed conflict.

Do not rewrite or silently amend the SOP.

Create a decision item for the competent organizational authority if formal adoption/interpretation is required.

# 5. CORRECT THE CONFIGURABLE EMERGENCY-FUND LIMIT MODEL

## 5.1 Configuration-driven policy, not hardcoded business logic

The amount and aggregation scope must be selected from an active, authorized policy configuration.

At minimum, the configuration has:
- `configured_limit_amount`
- `currency`
- `aggregation_mode`: `PER_INCIDENT` or `GLOBAL_ALL_INCIDENTS`
- `policy_scope_key` or equivalent scope definition
- `applicable_fund_pool`
- `effective_from` and optional `effective_to`
- `policy_version`
- approval and audit metadata

The current reference amount is Rp50,000,000, but the application must read the active configuration rather than embed Rp50,000,000 as a constant in code.

The amount may be changed prospectively through authorized policy maintenance. Historical transactions and policy versions must remain traceable.

## 5.2 Two selectable aggregation modes

**Mode A — `PER_INCIDENT`**
- The configured amount is the maximum cumulative emergency-fund expenditure for each defined incident/response-operation control unit.
- The amount is aggregated across all relevant requests/disbursements belonging to that same control unit.
- It is not a limit per voucher, sector, activity, user, team, or transaction.
- Distinct incidents have separate configured ceilings.
- Aggregate expenditure across distinct incidents may exceed the configured amount, subject to eligible cash and other rules.

**Mode B — `GLOBAL_ALL_INCIDENTS`**
- The configured amount is one shared cumulative ceiling across all incidents inside the configured policy scope.
- The amount is not independently available to every incident.
- All applicable incident requests/disbursements consume the same shared ceiling according to the approved consumption event.
- The exact policy boundary must be defined (for example, one emergency-response activation, response period, program, financial year, or another approved scope).
- Do not assume the global scope lasts forever or resets automatically each calendar year.
- Unless a separate per-incident limit is explicitly approved, do not also impose a per-incident ceiling in this mode.

Do not apply both modes simultaneously by default. A future `HYBRID` mode with both a per-incident ceiling and a global aggregate ceiling may be evaluated as an optional extension, but it must not be implemented or assumed without explicit owner approval.

## 5.3 Independent eligible-cash control

For either mode:
- Actual disbursement/reservation, according to the approved policy event, must not exceed eligible available cash in the relevant fund pool.
- Restricted funds are not freely interchangeable.
- Do not combine separate fund pools merely because all balances belong to the organization.
- Funding-source restrictions and cash-pool ownership must be respected.
- The configured ceiling is not proof that cash exists.
- The eligible-cash calculation is separate from the configured policy ceiling.

## 5.4 Remaining-limit formulas — conceptual only

For `PER_INCIDENT`:

`Remaining incident limit = max(0, configured_limit_amount - cumulative amount already counted for that incident control unit)`

`Maximum new amount = min(remaining incident limit, eligible cash available in the applicable fund pool)`

For `GLOBAL_ALL_INCIDENTS`:

`Remaining global limit = max(0, configured_limit_amount - cumulative amount already counted across all incidents in the policy scope)`

`Maximum new amount = min(remaining global limit, eligible cash available in the applicable fund pool)`

These are conceptual control expressions only, not approved accounting formulas.

Do not finalize what “cumulative amount already counted” means until the organization decides which event consumes the limit:
- Request submission.
- Approval.
- Cash reservation.
- Payment instruction.
- Actual cash release/disbursement.
- Another formally defined event.

Do not count the same amount twice when it transitions from reservation to actual disbursement.

## 5.5 Policy versioning and effective-date behavior

Analyze and document:
- Which policy version applies to a new incident.
- Which policy version applies to a new request under an existing incident.
- What happens to open incidents when a new amount becomes effective.
- What happens when aggregation mode changes from `PER_INCIDENT` to `GLOBAL_ALL_INCIDENTS`, or vice versa.
- Whether a policy can be retired while open requests still reference it.
- Whether policy changes require approval and dual control.

Do not silently migrate historical/active transactions to a new policy version. Recommend prospective application and immutable historical references, but mark the exact transition rule as `PENDING_OWNER_DECISION` if it has not been approved.

## 5.6 Worked examples

Include and verify all of these cases:

1. `PER_INCIDENT`, configured amount Rp50m: Incident A has prior counted amount Rp20m; new request Rp40m; eligible cash Rp100m. The new amount cannot make the cumulative amount for Incident A exceed Rp50m.
2. `PER_INCIDENT`, configured amount Rp50m: Incident A and Incident B are distinct; requests Rp50m and Rp35m; eligible cash Rp100m. Combined Rp85m may be allowed subject to approval and policy.
3. `PER_INCIDENT`, configured amount Rp50m: two distinct incidents request Rp50m each; eligible cash is Rp80m. Per-incident limits pass, but global cash control prevents total release/reservation beyond Rp80m.
4. `GLOBAL_ALL_INCIDENTS`, configured amount Rp50m: Incident A consumes Rp20m and Incident B consumes Rp15m. Only Rp15m remains for all other incidents in that policy scope.
5. `GLOBAL_ALL_INCIDENTS`, configured amount Rp50m: Incident A requests Rp30m and Incident B requests Rp25m. Aggregate Rp55m exceeds the shared ceiling; the excess must not be authorized.
6. One incident has four sectors requesting Rp20m, Rp15m, Rp10m, and Rp10m. In `PER_INCIDENT` mode, aggregate Rp55m must be detected if all belong to the same control unit.
7. General non-emergency program budget is Rp75m or Rp250m. The emergency-fund ceiling must not be applied merely because the value exceeds Rp50m.
8. The configured amount is changed prospectively from Rp50m to Rp75m. Historical policy versions and transactions remain traceable; the effective date determines which policy applies according to the approved transition rule.
9. Rp100m shown in a template must not create a default, cap, or approval threshold.

# 6. INCIDENT VERSUS RESPONSE OPERATION — DECISION REQUIRED

The owner has stated “satu kejadian/operasi tanggap darurat” and now requires the amount and aggregation mode to be configurable. The selected mode determines whether the configured ceiling is applied per incident or cumulatively across all incidents in the defined policy scope.

Do not silently decide that several operational sub-records under one real-world incident each receive a separate configured per-incident cap.

Prepare a decision table comparing:

- `PER_INCIDENT`: one configured cap per real-world incident, with sectors/activities/response workstreams aggregated under it.
- `PER_INCIDENT`: one configured cap per formally independent response operation, if the organization approves that identity rule.
- `GLOBAL_ALL_INCIDENTS`: one shared configured ceiling across all incidents inside a defined policy scope.
- Optional future `HYBRID`: both per-incident and global ceilings, only if explicitly approved.
- Another organization-approved definition.

For each alternative, explain:
- Operational meaning.
- Risk of cap circumvention.
- Required evidence/approval.
- Data relationships.
- Reporting implications.
- How duplicate or related incidents are handled.

For `PER_INCIDENT` mode, until a formal decision exists, recommend the conservative approach: aggregate under the parent incident and do not reset the cap by creating another sector, activity, voucher, user, team, or sub-record. For `GLOBAL_ALL_INCIDENTS` mode, aggregate all included incidents under the configured policy scope. The global scope boundary itself requires an explicit decision.

Label this conservative approach `TECHNICAL_RECOMMENDATION` / `PENDING_ORG_DECISION`, not direct owner policy.

# 7. CORRECT TEST CASE SCOPE AND EXPECTED RESULTS

Review FIN-TEST-01 through FIN-TEST-35 and add FIN-TEST-36 through FIN-TEST-46 for configurable policy behavior.

Every test must identify its domain:
- `GENERAL_PROGRAM_BUDGET`
- `EMERGENCY_FUND_PER_INCIDENT`
- `EMERGENCY_FUND_GLOBAL_ALL_INCIDENTS`
- `EMERGENCY_FUND_POLICY_CONFIGURATION`
- `RESTRICTED_FUNDING_SOURCE`
- `ORDINARY_OPERATIONAL_EXPENDITURE`
- `CROSS_MODULE_INTEGRATION`

Specifically:
- FIN-TEST-01, FIN-TEST-02, and FIN-TEST-03 must state whether the proposal is a general program/activity budget or an emergency-fund request.
- If general program/activity budget: do not apply the emergency-fund ceiling automatically.
- If emergency-fund request: read the active policy configuration and apply the selected aggregation mode (`PER_INCIDENT` or `GLOBAL_ALL_INCIDENTS`) plus the eligible-cash constraint.
- Do not hardcode Rp50m into test expectations where the configured amount may differ; use Rp50m only in test cases that explicitly set that value in test configuration.
- FIN-TEST-34 should explicitly verify that non-emergency program budget above the configured emergency-fund ceiling is not blocked by the emergency rule.
- FIN-TEST-24 through FIN-TEST-35 must remain and be refined, not removed.

For each test include:
1. Test ID and domain.
2. Objective.
3. Preconditions.
4. Test data.
5. Steps.
6. Expected result.
7. Actual result (“not executed” if not run).
8. Status.
9. Evidence.
10. Dependencies/pending decisions.

Add at least these mandatory configuration tests:

| ID | Domain | Scenario | Expected result |
|---|---|---|---|
| FIN-TEST-36 | `EMERGENCY_FUND_PER_INCIDENT` | Configured amount Rp50m, `PER_INCIDENT`; two distinct incidents each request Rp40m; eligible cash is sufficient | Both may pass their individual caps; aggregate may exceed Rp50m, subject to cash and approvals |
| FIN-TEST-37 | `EMERGENCY_FUND_GLOBAL_ALL_INCIDENTS` | Configured amount Rp50m, `GLOBAL_ALL_INCIDENTS`; Incident A requests Rp30m and Incident B requests Rp25m within the same policy scope | Aggregate Rp55m is blocked/held; shared remaining ceiling is Rp20m after the first Rp30m is counted |
| FIN-TEST-38 | `EMERGENCY_FUND_POLICY_CONFIGURATION` | Authorized policy change from Rp50m to Rp75m with a future effective date | New version is created; old version remains immutable; policy selection follows approved effective-date/transition rules |
| FIN-TEST-39 | `EMERGENCY_FUND_POLICY_CONFIGURATION` | Aggregation mode changes from `PER_INCIDENT` to `GLOBAL_ALL_INCIDENTS` | No silent reinterpretation of existing incidents/requests; transition behavior follows an approved decision |
| FIN-TEST-40 | `EMERGENCY_FUND_POLICY_CONFIGURATION` | User without policy-maintenance authority attempts to change amount or scope | Change is denied and logged; ordinary Finance edit access is insufficient |
| FIN-TEST-41 | `EMERGENCY_FUND_POLICY_CONFIGURATION` | Configuration contains zero/negative amount, invalid currency precision, invalid date range, or overlapping active policy scope | Invalid/ambiguous configuration is rejected or held for correction according to approved validation rules |
| FIN-TEST-42 | `EMERGENCY_FUND_GLOBAL_ALL_INCIDENTS` | Global policy is scoped to one approved response activation/period; another activation begins | Consumption is aggregated only within the correct approved policy scope; no invented automatic reset |
| FIN-TEST-43 | `EMERGENCY_FUND_POLICY_CONFIGURATION` | Policy amount, mode, scope, or effective dates are revised | Full old/new values, actor, timestamp, reason, approval evidence, and effective date are auditable |
| FIN-TEST-44 | `EMERGENCY_FUND_GLOBAL_ALL_INCIDENTS` | Two users concurrently submit requests against the same global ceiling and cash pool | Atomic control prevents the combined counted amount from exceeding the shared ceiling or eligible cash |
| FIN-TEST-45 | `RESTRICTED_FUNDING_SOURCE` | An explicitly authorized active policy is configured at Rp100m (not inferred from an example template), but eligible cash in the relevant fund pool is Rp30m; other restricted funds exist | Maximum disbursement is constrained by eligible cash; restricted balances are not added as freely available cash |
| FIN-TEST-46 | `EMERGENCY_FUND_POLICY_CONFIGURATION` | Repository search for hardcoded Rp50m/Rp100m in validation/workflow/configuration | Business logic reads the active authorized configuration; examples/documentation are not treated as active policy |


Use only these test statuses:
- `TEST_DESIGNED`
- `TEST_EXECUTED_PASS`
- `TEST_EXECUTED_FAIL`
- `BLOCKED_BY_MISSING_POLICY`
- `BLOCKED_BY_MISSING_SOURCE`

Do not claim a test passed unless actually executed and evidence is provided.

# 8. CASH POOL, FUNDING RESTRICTION, AND CONCURRENCY

Prepare a logical control model that distinguishes:
- Funding source.
- Fund pool.
- Bank/cash account.
- Eligible cash balance.
- Restricted cash.
- Reserved amount, if policy adopts reservation.
- Outstanding payment instruction.
- Actual cash release/disbursement.
- Refund/reversal.
- Transfer between funds, if allowed.

Do not add all organizational cash balances together.

A cash balance is eligible only if its source and restrictions allow the proposed emergency expenditure.

Analyze concurrent requests from multiple incidents:
- Prevent two requests from consuming the same available cash.
- Avoid double reservation.
- Avoid duplicate disbursement on retry.
- Avoid double counting when reservation becomes actual disbursement.
- Preserve the original transaction and audit trail.
- Define how expired/cancelled reservations are released, but label this as pending policy if no approved rule exists.

No physical database schema or code.

# 9. APPROVAL AUTHORITY AND GOVERNANCE

Revisit the statement about approval by Ketua TSKKM on SOP page 23.

Separate:
- Job title/organizational authority.
- Formal delegation/mandate.
- User account.
- Role-based permission.
- Assignment to a response operation.
- Approval action.

Do not infer that a user can approve because they have edit access, are assigned to an incident, or hold a similarly named role.

If SOP evidence indicates approval by Ketua TSKKM, quote the source and identify what formal mandate/delegation evidence is still required to map it to the system.

Do not invent additional approval thresholds or approval levels.

# 10. REQUIRED OUTPUT STRUCTURE

Create:

`SIMTDB_REV05112026_00_09_FINANCE_POLICY_RECONCILIATION_AND_LOGICAL_DESIGN_READINESS.md`

Include:

1. Executive Summary.
2. Scope and Evidence Availability.
3. Corrected Owner Clarification Register.
4. Corrected Provenance Register for every FIN-BR.
5. Verbatim SOP Page 23 Evidence and Context.
6. SOP/Owner Clarification Reconciliation.
7. Corrected Configurable Emergency-Fund Business Rules.
8. Emergency-Fund Policy Configuration Master/Setup Model.
9. `PER_INCIDENT` and `GLOBAL_ALL_INCIDENTS` Aggregation Models.
10. Policy Versioning, Effective Dates, Approval, and Audit Trail.
11. Eligible Cash Pool and Restriction Model.
12. Incident/Response Operation Alternatives and Decision Table.
13. Corrected FIN-TEST-01 through FIN-TEST-46 with explicit domains.
14. Approval Authority Evidence and Mapping Gaps.
15. Finance–Procurement–Logistics Ownership Boundaries.
16. Logical Entity/Relationship Concepts only.
17. Risk Register.
18. Decision Register with decision owner and evidence required.
19. Readiness Assessment.
20. Recommended next stage.

# 11. READINESS GATE

Assess separately:

- Owner clarification completeness.
- SOP reconciliation.
- Authority mapping.
- Incident/operation identity.
- Configurable amount and aggregation mode.
- Policy versioning/effective-date behavior.
- Policy maintenance and approval authority.
- Global policy scope boundary.
- Eligible cash policy.
- Funding-source restrictions.
- Transaction event/cap consumption.
- Actual expenditure/cash disbursement treatment.
- Program–Activity–Budget relationships.
- Test readiness.
- Logical design readiness.

Use:
- `READY`
- `CONDITIONAL`
- `BLOCKED`

Do not mark final Finance logical design ready while critical policy decisions remain unresolved.

A preliminary conceptual model may be documented, but label unresolved relationships and business rules as pending. Do not present them as approved.

# 12. STRICT STOP CONDITIONS

- Read-only review only.
- Do not alter existing source documents.
- Do not alter SOP wording.
- Do not modify source code, database, migrations, seed, config, dependencies, or deployment.
- Do not run mutating commands.
- Do not invent missing policy or authority.
- Do not infer that an unexecuted test passed.
- Do not claim repository/database inspection if the sources are unavailable.
- Do not proceed to physical database design or implementation.
- Stop after creating the output file and wait for project-owner review.

**Final controlling principle:** The emergency-fund ceiling amount and its aggregation mode must be configurable through controlled, versioned Finance policy/master-data setup. The current reference amount is Rp50,000,000, but it must not be hardcoded as an immutable application constant. In `PER_INCIDENT` mode, the configured amount applies cumulatively to each defined incident/operation control unit. In `GLOBAL_ALL_INCIDENTS` mode, the configured amount is one shared cumulative ceiling across all incidents within the explicitly defined policy scope. The selected mode, policy boundary, effective date, approval, and treatment of active incidents must be traceable. For either mode, eligible available cash and funding-source restrictions remain separate constraints. Rp100,000,000 remains illustrative only. General program/activity budget flexibility must not be confused with the emergency-fund policy ceiling.
