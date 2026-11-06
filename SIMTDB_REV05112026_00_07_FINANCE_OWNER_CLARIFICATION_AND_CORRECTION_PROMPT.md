# SIM-TDB — FINANCE OWNER CLARIFICATION & AUDIT CORRECTION PROMPT

**Document ID:** SIMTDB-REV05112026-00-07-FIN  
**Filename:** `SIMTDB_REV05112026_00_07_FINANCE_OWNER_CLARIFICATION_AND_CORRECTION_PROMPT.md`  
**Revision:** REV05112026  
**Date:** 05 November 2026  
**Project:** Sistem Informasi Manajemen Tanggap Darurat Bencana (SIM-TDB)  
**Mode:** Audit correction and requirement harmonization only — NO IMPLEMENTATION

---

# 1. MANDATE

Act as a Principal Finance Systems Architect, Enterprise Data Architect, Senior Business Analyst, Internal Control Specialist, Security/Authorization Architect, and QA Lead.

Re-audit and correct the Finance audit document `SIMTDB_REV05112026_00_06_FINANCE_CLARIFICATION_REAUDIT.md` using:
- The project-owner clarifications in this prompt.
- The original SOP pages actually available in the workspace.
- Existing Finance audit documents and CHR records.
- The read-only execution guardrails.

This is a correction and harmonization task. Do not discard valid findings from 00_06. Retain findings that remain correct, correct inaccurate classifications, and explicitly document changes.

**Do not write code, create database tables, migrations, seed data, APIs, or alter application configuration. Do not run commands that mutate project files, databases, or environments.**

# 2. CONTROLLING OWNER CLARIFICATIONS — FINANCIAL AMOUNTS

The project owner has now clarified the meaning of the two example amounts and the emergency-fund limit. These statements supersede earlier ambiguous interpretations in the Finance audit.

## 2.1 Rp100,000,000 — illustrative amount only

Rp100,000,000 appearing in the SOP/template or example of emergency funding need is an illustrative example only.

It is NOT:
- A fixed amount.
- A mandatory budget.
- A maximum amount.
- A spending cap.
- An approval threshold.
- A default value that the application must insert.

Do not turn Rp100,000,000 into a validation rule or workflow condition.

## 2.2 Rp50,000,000 — maximum emergency-fund expenditure per one incident/response operation

The project owner clarified:

- TSKKM may issue emergency funds up to a maximum of Rp50,000,000 for one emergency incident/response operation.
- Rp50,000,000 is the maximum for that one incident/operation, not a mandatory amount and not an amount that must always be spent.
- The amount actually issued must also be limited by the emergency cash genuinely available.
- If TSKKM participates in multiple distinct incidents/response operations, it may issue emergency funds for each distinct incident/operation, subject to the per-incident/operation maximum and the cash-availability constraint.
- Therefore, the aggregate emergency-fund expenditure across several distinct incidents may exceed Rp50,000,000, provided each incident/operation complies with its own maximum and total available cash is sufficient.
- Rp50,000,000 is NOT a global cap for all TSKKM emergency activities, all incidents combined, all programs, or all activities.

This is a direct project-owner clarification. Record it as `CLARIFIED_BY_PROJECT_OWNER`.

## 2.3 Scope boundary

The Rp50,000,000 maximum applies specifically to the TSKKM emergency-fund expenditure for one incident/response operation, as clarified by the project owner.

Do NOT automatically apply this limit to:
- All program budgets.
- All activity budgets.
- All donor or grant funds.
- All APP Nasional funds.
- All procurement.
- All ordinary operational expenditure.
- All financial transactions unrelated to the relevant emergency fund.

Other funding sources remain governed by their own verified restrictions, approval rules, and formal decisions.

Do not assume that an amount above Rp50,000,000 for one incident can automatically be paid from another funding source. Any additional funding must follow the rules and approvals applicable to that source.

# 3. REQUIRED BUSINESS-RULE INTERPRETATION

Create or correct the Financial Business Rule Register with at least these rules:

| ID | Business rule | Required provenance |
|---|---|---|
| FIN-BR-OWNER-01 | Rp100m is an illustrative amount only; it is not a fixed value, cap, default, or approval threshold | `CLARIFIED_BY_PROJECT_OWNER` |
| FIN-BR-OWNER-02 | Maximum TSKKM emergency-fund expenditure for one incident/response operation is Rp50m | `CLARIFIED_BY_PROJECT_OWNER` |
| FIN-BR-OWNER-03 | Actual emergency-fund expenditure for one incident/operation must not exceed the lower of Rp50m and the genuinely available emergency cash applicable to that expenditure | `CLARIFIED_BY_PROJECT_OWNER` for the two limits; implementation mechanics are `TECHNICAL_RECOMMENDATION` |
| FIN-BR-OWNER-04 | Each distinct incident/response operation may have its own emergency-fund expenditure, subject to its own Rp50m maximum and the overall available-cash constraint | `CLARIFIED_BY_PROJECT_OWNER` |
| FIN-BR-OWNER-05 | Aggregate expenditure across several distinct incidents may exceed Rp50m if each incident complies and cash is sufficient | `CLARIFIED_BY_PROJECT_OWNER` |
| FIN-BR-TECH-01 | The system must aggregate all emergency-fund disbursements linked to the same incident/operation when checking the Rp50m maximum | `TECHNICAL_RECOMMENDATION` derived from owner clarification |
| FIN-BR-TECH-02 | The system must prevent splitting one incident into multiple transactions, sectors, activities, users, or sub-records to reset the Rp50m limit | `TECHNICAL_RECOMMENDATION` derived from owner clarification |
| FIN-BR-TECH-03 | The system must check available cash before authorizing/recording a disbursement, using a consistent and approved cash-balance basis | `TECHNICAL_RECOMMENDATION`; exact accounting basis may remain pending |
| FIN-BR-TECH-04 | Multiple disbursements/installments for one incident must be aggregated against the same incident/operation limit | `TECHNICAL_RECOMMENDATION`; operational approval mechanics require confirmation |
| FIN-BR-TECH-05 | Concurrent requests must not collectively exceed either the incident-level cap or available cash | `TECHNICAL_RECOMMENDATION` |

Do not classify technical implementation mechanics as direct owner quotations. Preserve provenance precisely.

# 4. FORMULA — CONCEPTUAL CONTROL ONLY

For one incident/response operation:

`Maximum permitted emergency-fund expenditure for that incident = MIN(Rp50,000,000, eligible available emergency cash)`

The actual amount requested or approved must not exceed this amount.

For multiple distinct incidents:

`Total emergency-fund expenditure across incidents = SUM(actual emergency-fund expenditure for each distinct incident)`

The sum may exceed Rp50,000,000, but the total must remain within the genuinely available emergency cash across the fund.

Important:
- This is a business-control expression, not a final accounting formula.
- Do not equate cash balance with budget balance.
- Do not invent the accounting treatment of commitments, outstanding payment instructions, advances, refunds, or restricted cash.
- The exact calculation of eligible available emergency cash must be documented as a pending Finance policy/design dependency if not supported by an approved source.
- To avoid overspending under concurrent operations, evaluate valid reservations/approved but unpaid disbursements as part of the available-cash control. Mark the exact treatment as `PENDING_ORG_DECISION` if no Finance policy defines it.

# 5. INCIDENT IDENTITY AND ANTI-SPLITTING CONTROL

This is a critical data-integrity requirement.

The system must not enforce Rp50,000,000 per transaction, per sector, per activity, per user, per voucher, or per department. The control is per one incident/response operation as clarified by the owner.

Analyze and propose a canonical identity model:
- Incident ID.
- Response operation ID, if distinct from incident.
- Parent-child relationship if one incident can contain multiple response operations.
- Emergency-fund disbursement references.
- Sector/activity references.
- Approval and evidence references.

The system must aggregate all applicable emergency-fund disbursements belonging to the same control unit.

Do not allow a user to bypass the maximum by:
- Creating several vouchers for one incident.
- Dividing the request among sectors.
- Dividing the request among activities.
- Using different requestors or approvers.
- Creating multiple transactions.
- Retrying a request after a timeout.
- Creating duplicate incident records for the same real-world event.

## 5.1 Incident versus operation — unresolved modeling question

The owner used the phrase “satu kejadian/operasi tanggap darurat.” Do not silently assume that one real-world incident may be split into several separately capped operations.

Analyze this distinction and record a specific pending decision:

- Does one real-world incident always have one Rp50m aggregate cap, even if several operational workstreams/sectors exist?
- Or can the organization formally identify multiple independent response operations within one broader incident, each with a separate Rp50m cap?

Until the organization formally defines this distinction, recommend the conservative anti-circumvention behavior: aggregate under the parent incident and do not reset the cap merely because a new sector, activity, voucher, or operational sub-record is created.

Classify this default as `TECHNICAL_RECOMMENDATION` / `PENDING_ORG_DECISION`, not as an additional owner-confirmed rule.

# 6. REQUIRED EXAMPLES AND EXPECTED RESULTS

Use these examples in the corrected audit and test plan.

## 6.1 Several distinct incidents

Assume eligible available emergency cash is Rp200,000,000.

| Incident | Requested/issued amount | Per-incident result |
|---|---:|---|
| Flood A | Rp50,000,000 | Within limit |
| Landslide B | Rp35,000,000 | Within limit |
| Flood C | Rp45,000,000 | Within limit |
| Fire D | Rp20,000,000 | Within limit |
| **Total** | **Rp150,000,000** | **Permitted if all approvals and cash controls are satisfied** |

The total exceeds Rp50m, but no individual incident exceeds Rp50m.

## 6.2 One incident exceeding the maximum

Assume eligible available emergency cash is Rp100,000,000.

| Incident | Requested amount | Maximum for incident | Expected |
|---|---:|---:|---|
| Flood A | Rp75,000,000 | Rp50,000,000 | Reject or require revised request; never authorize Rp75m from this emergency fund |

## 6.3 Cash availability below the per-incident maximum

Assume eligible available emergency cash is Rp30,000,000.

| Incident | Requested amount | Maximum by incident rule | Maximum by cash | Expected |
|---|---:|---:|---:|---|
| Landslide B | Rp50,000,000 | Rp50,000,000 | Rp30,000,000 | Must not disburse more than Rp30m |

Whether the system can approve a partial amount or must return the request for revision is a pending workflow decision. Do not invent that policy.

## 6.4 Multiple disbursements for one incident

Assume Incident A has:
- First disbursement: Rp20,000,000.
- Second disbursement request: Rp25,000,000.
- Third disbursement request: Rp10,000,000.

Cumulative requested/issued amount would be Rp55,000,000.

Expected:
- The system aggregates all three amounts under Incident A.
- The third request cannot cause cumulative emergency-fund expenditure to exceed Rp50m.
- The control is cumulative, not per voucher.
- The workflow for partial approval/revision remains subject to the approved procedure.

## 6.5 One incident, multiple sectors

Assume Incident A includes Logistics, Health, Shelter, and Education activities.

Emergency-fund disbursements:
- Logistics: Rp20m.
- Health: Rp15m.
- Shelter: Rp10m.
- Education: Rp10m.

Cumulative amount: Rp55m.

Expected:
- The system recognizes these as one incident if they belong to the same registered incident/control unit.
- The Rp50m cap is exceeded.
- Creating four sector records must not reset the limit.

# 7. CORRECT THE PRIOR 00_06 AUDIT FINDINGS

Re-audit and correct these items from the previous independent review.

## 7.1 Owner Clarification Register

Correct the previous OCL register.

Only direct owner statements may use `CLARIFIED_BY_PROJECT_OWNER`.

At minimum, include:
- Rp100m illustrative only.
- Rp50m maximum per one incident/response operation.
- Per-incident maximum does not create a global TSKKM cap.
- Multiple distinct incidents can each receive emergency funds within the per-incident maximum.
- Actual disbursement is also limited by available cash.

Do not classify the following as direct owner clarifications unless separate acceptance evidence exists:
- Five-part budget data model.
- Specific revision metadata.
- Exact funding allocation schema.
- Actual-expenditure accounting recognition basis.
- Exact approval workflow implementation.
- Remaining-budget formula.
- Technical concurrency controls.

## 7.2 Source hierarchy and conflict handling

Correct the hierarchy. Do not treat a project-owner clarification as authority to amend formal SOPs or organizational decisions.

Use domain-specific authority:
- Application intent and project requirement: project-owner clarification.
- Operational procedure: applicable SOP.
- Role/delegation/authority: formal organizational decision.
- Financial accounting policy: approved Finance policy.
- Architecture/database design: accepted technical decision.
- Test outcome: actual test evidence.

If sources conflict, record `SOURCE_CONFLICT`, identify the relevant decision owner, and stop short of silently choosing one.

## 7.3 Actual expenditure and cash availability

Do not equate:
- Budget.
- Cash balance.
- Cash disbursement.
- Expense recognition.
- Commitment.
- Invoice.
- Payment.
- Inventory receipt.

Preserve the need for one canonical source for each financial fact, but do not decide that payment is necessarily the canonical actual-expense source without approved Finance policy.

The Rp50m incident-level limit is a control on emergency-fund expenditure/disbursement. The system must separately define which transaction event consumes this limit (for example, approved reservation, authorized disbursement, or actual cash release). If policy is unavailable, record it as a pending Finance decision and propose a safe control without presenting it as confirmed policy.

## 7.4 Test status consistency

Use only:
- `TEST_DESIGNED`
- `TEST_EXECUTED_PASS`
- `TEST_EXECUTED_FAIL`
- `BLOCKED_BY_MISSING_POLICY`
- `BLOCKED_BY_MISSING_SOURCE`

A test whose logic is designed but awaits a policy decision should normally remain `TEST_DESIGNED` with a separate dependency field `PENDING_ORG_DECISION` or `PENDING_DESIGN_DECISION`.

Do not introduce undefined labels such as `PENDING_SOURCE`.

# 8. ADDITIONAL TEST CASES — MANDATORY

Add at least these tests to the existing FIN-TEST suite:

| ID | Scenario | Expected result |
|---|---|---|
| FIN-TEST-24 | One incident requests Rp75m while cash is Rp100m | Cannot disburse more than Rp50m from the emergency fund for that incident |
| FIN-TEST-25 | Four distinct incidents request Rp50m, Rp35m, Rp45m, Rp20m; cash Rp200m | Per-incident limits pass; aggregate Rp150m is allowed subject to approval |
| FIN-TEST-26 | One incident requests Rp50m while eligible cash is Rp30m | Cannot disburse more than Rp30m; partial approval behavior remains pending |
| FIN-TEST-27 | One incident has multiple vouchers totaling Rp55m | Aggregate cap violation detected; no per-voucher reset |
| FIN-TEST-28 | One incident has multiple sectors/activities whose emergency-fund allocations total Rp55m | Aggregate cap violation detected |
| FIN-TEST-29 | Two distinct incidents each request Rp50m; available cash Rp80m | Each incident passes its individual cap, but total disbursement must not exceed available cash |
| FIN-TEST-30 | Same real-world incident is entered twice with separate IDs | Duplicate/possible duplicate incident must be detected or flagged for controlled review |
| FIN-TEST-31 | Two users authorize disbursements concurrently for different incidents against the same cash pool | Global cash control prevents aggregate disbursement/reservations from exceeding eligible available cash |
| FIN-TEST-32 | Same disbursement is retried after network timeout | Idempotent processing prevents duplicate disbursement and duplicate cap consumption |
| FIN-TEST-33 | One incident has an initial Rp20m disbursement and later requests Rp35m | Cumulative amount Rp55m is detected; additional amount cannot exceed remaining incident cap |
| FIN-TEST-34 | A non-emergency program budget exceeds Rp50m | Rp50m emergency-fund cap is not incorrectly applied to unrelated program budgets |
| FIN-TEST-35 | Rp100m appears as an example in documentation | It is not treated as an application cap, default, or approval threshold |

For each test provide:
- Purpose.
- Preconditions.
- Data.
- Steps.
- Expected result.
- Actual result (write “not executed” if no executable test occurred).
- Status.
- Required evidence.
- Dependencies/pending decisions.

Do not claim tests passed unless executed in an authorized isolated environment with evidence.

# 9. FINANCE DATA AND CONTROL DESIGN REVIEW

Update the conceptual Finance model and data dictionary to support:
- Distinct incident/response-operation identity.
- Per-incident emergency-fund cap.
- Multiple disbursements linked to one incident.
- Multiple sectors/activities linked to one incident without resetting the cap.
- Global emergency cash availability across incidents.
- Audit trail for requests, approvals, reservations, disbursements, reversals, and corrections, subject to approved workflow.
- Explicit source-fund identity and restrictions.
- Distinction between budget and cash.
- Safe concurrent processing and idempotency.

Do not produce physical schema or database-specific types.

Identify the likely conceptual relationships, but mark unresolved cardinality and event/operation hierarchy decisions as pending.

# 10. OUTPUT FILE

Save the corrected audit as:

`SIMTDB_REV05112026_00_08_FINANCE_CLARIFICATION_REAUDIT_CORRECTED.md`

Do not overwrite:
- 00_02 financial clarification.
- 00_03 earlier audit prompt.
- 00_04 Copilot prompt audit.
- 00_05 finance re-audit prompt.
- 00_06 Finance audit result.
- Existing SOP source files.

The output must include:
1. Executive Summary.
2. Updated Owner Clarification Register.
3. Corrected Provenance and Source Hierarchy.
4. Corrected Financial Business Rule Register.
5. Per-Incident Emergency-Fund Limit Model.
6. Global Available-Cash Control Model.
7. Incident/Operation Identity and Anti-Splitting Analysis.
8. Funding Source and Restriction Model.
9. Actual Expenditure / Cash Disbursement Source-of-Truth Analysis.
10. Finance–Procurement–Logistics Integration.
11. Updated Finance Entity Registry and Data Dictionary (logical only).
12. Corrected FIN-TEST-01 through FIN-TEST-35.
13. Updated Risk Register.
14. Updated CHR-020 mapping.
15. Pending Owner/Organization/Finance Decisions.
16. Evidence Required.
17. Readiness Assessment.
18. Exact next recommended prompt.

# 11. READINESS AND STOP RULES

Use one of:
- `READY_FOR_LOGICAL_DESIGN`
- `CONDITIONAL`
- `BLOCKED`

Do not mark Finance ready for logical design if critical questions remain about:
- Incident/operation identity and cap aggregation.
- Available emergency cash basis.
- Approval authority.
- Funding-source restrictions.
- Actual expenditure versus cash disbursement.
- Program/Activity/Budget relationships.

Do not proceed to physical schema, coding, migration, seed, or deployment.

Stop after saving the corrected audit and wait for project-owner review.

**Final design principle:** Rp50,000,000 is a maximum emergency-fund expenditure for one distinct incident/response operation, not a global TSKKM cap. Multiple distinct incidents may each receive emergency funds within that per-incident maximum, but the total must never exceed genuinely available emergency cash. Rp100,000,000 remains an illustrative amount only.
