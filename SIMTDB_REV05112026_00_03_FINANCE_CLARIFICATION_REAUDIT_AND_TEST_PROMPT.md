# SIM-TDB — RE-AUDIT ADDENDUM FINANCE & TEST PROMPT

**Document ID:** SIMTDB-REV05112026-00-03-FIN  
**Filename:** `SIMTDB_REV05112026_00_03_FINANCE_CLARIFICATION_REAUDIT_AND_TEST_PROMPT.md`  
**Revision:** REV05112026  
**Date:** 05 November 2026  
**Mode:** Specification audit and test design only — no implementation

---

# PART A — INDEPENDENT AUDIT

## 1. Audit conclusion

The addendum `SIMTDB_REV05112026_00_02_FINANCIAL_AMOUNT_CLARIFICATION.md` correctly captures the project owner's clarification that Rp50,000,000 and Rp100,000,000 are illustrative amounts, not fixed budget values, caps, mandatory defaults, or automatic approval thresholds.

**Overall status:** PASS for the central interpretation of the two illustrative amounts; CONDITIONAL for completeness and precision of the Finance data model; NOT READY for physical database design or implementation.

This is a document/design review. No repository, application, database, migration, or executable test was run. All tests below are designed tests or desk simulations, not claimed execution results.

## 2. Findings that are correct and should be retained

| ID | Finding | Assessment |
|---|---|---|
| FIN-AUD-01 | Rp50m and Rp100m are examples, not fixed amounts or caps | Correct; retain `CLARIFIED_BY_PROJECT_OWNER` |
| FIN-AUD-02 | No hardcoding/default/automatic threshold based on those examples | Correct |
| FIN-AUD-03 | Budget can vary according to program/activity needs and approved funding | Correct |
| FIN-AUD-04 | Proposed, approved, revised, actual, and remaining amounts are distinct concepts | Good design requirement; status label needs refinement |
| FIN-AUD-05 | Budget revisions preserve history, reason, actor, time, and approval reference | Good control; approval workflow and authority need source confirmation |
| FIN-AUD-06 | Funding source must be traceable | Correct requirement; cardinality and restrictions need more design |
| FIN-AUD-07 | Remaining budget formula is not invented | Correct; keep unresolved |
| FIN-AUD-08 | CHR-020 is only partially resolved | Correct |
| FIN-AUD-09 | Actual report amounts must trace to recorded financial records | Correct direction; accounting recognition and transaction statuses remain unresolved |

## 3. Corrections and technical risks

### FIN-CR-01 — Over-classification as `CLARIFIED_BY_PROJECT_OWNER`

The owner explicitly clarified:
- Rp50m and Rp100m are examples only.
- Budget amounts may vary according to program/activity needs.
- These amounts are not fixed caps or automatic approval thresholds.

That clarification alone does not formally settle every detailed accounting or workflow rule in the addendum.

Therefore:
- FIN-BR-001 and the illustrative-amount interpretation may remain `CLARIFIED_BY_PROJECT_OWNER`.
- Flexible budget amounts may carry that status only to the extent they restate the owner's statement.
- Detailed lifecycle controls, audit fields, versioning, actual-expenditure recognition, and report lineage should be classified as `TECHNICAL_RECOMMENDATION` or an explicitly accepted project requirement—not automatically as an SOP-confirmed or organization-wide accounting policy.
- If the owner approves these as project requirements, record the approval separately with date and scope.

### FIN-CR-02 — Potential duplicate source of truth for actual amount

The addendum proposes both `financial_transaction_id` and `actual_amount` inside an `Actual expenditure reference`.

This may duplicate the amount already stored in the canonical financial transaction or transaction line.

Preferred direction:
- Finance transaction/transaction-line is the canonical source of actual amount.
- An expenditure reference/report points to that transaction and derives its amount.
- If an immutable snapshot is genuinely required, identify it as a snapshot with reason, timestamp, source transaction version, and reconciliation rule.
- Do not maintain two editable copies of the same actual amount.

### FIN-CR-03 — Funding-source cardinality is undefined

The proposed budget model uses one `funding_source_id`. This may be insufficient if one program, activity, budget line, or expense can be funded by more than one source.

Explicitly determine whether:
- Each budget proposal has exactly one funding source; or
- One budget may have several sources; or
- One expense may be allocated across multiple sources.

If multiple sources are permitted, evaluate an allocation relationship containing budget/budget line, funding source, allocated amount, allocation version/status, restrictions, and evidence.

Do not assume multiple-source allocation is approved policy. Preserve it as a design question.

### FIN-CR-04 — Funding-source restrictions need structured representation

The earlier SOP audit records restrictions on APP Nasional funds for certain expense types. A funding-source ID alone does not enforce such restrictions.

When supported by approved policy, the future model should represent:
- Eligible expense categories.
- Ineligible expense categories.
- Required documents.
- Geographic/program restrictions.
- Validity period.
- Policy/source reference.
- Version and approval status.

Do not invent restrictions or enable automatic blocking until the complete official wording and authorized interpretation are available.

### FIN-CR-05 — Ambiguous `program_id / activity_id`

A field definition written as `program_id / activity_id` does not establish a valid relational design.

Avoid an unvalidated polymorphic reference that can point to different tables without foreign-key integrity.

Determine:
- Whether every activity belongs to a program.
- Whether a budget may exist at program level, activity level, or both.
- Whether activity-level budgets roll up to a program.
- Whether budget lines belong to a budget header or directly to an activity.

Then define explicit foreign keys and cardinality. Do not finalize the relationship until the business rule and Program/Activity entity model are approved.

### FIN-CR-06 — Budget revision needs a precise lifecycle

The addendum includes `previous_amount`, `revised_amount`, reason, actor, timestamp, and approval reference. This is a useful start but does not distinguish:
- Revision requested.
- Revision under review.
- Revision approved.
- Revision rejected.
- Revision cancelled/withdrawn.
- Revision effective in the budget baseline.

Do not create these as final official statuses until the process is confirmed. The design must distinguish a proposed revision from an approved/effective revision.

Preserve historical approved budgets. Define version number, effective date, approval reference, and supersession behavior.

### FIN-CR-07 — Remaining budget is not ready for a final formula

The addendum correctly leaves the formula open.

Unresolved concepts include:
- Actual expenditure recognition basis.
- Outstanding commitments/encumbrances.
- Purchase orders not yet invoiced.
- Invoices received but unpaid.
- Advances.
- Refunds and reversals.
- Cancelled transactions.
- Period cut-off.
- Currency conversion, if multiple currencies are permitted.
- Rounding.

Do not show a definitive remaining budget until the basis is approved. A draft view may show separately labelled components, but must not imply a final accounting balance.

### FIN-CR-08 — Money data type and currency handling

At physical database design:
- Do not use binary floating-point types for monetary values.
- Use a precise decimal/numeric representation, or integer minor units if justified by the chosen currency and platform.
- Store currency explicitly where multi-currency is possible.
- Do not invent exchange rates or conversion dates.
- Define rounding and precision based on approved finance policy.

This is a technical recommendation, not an SOP requirement.

### FIN-CR-09 — Approval thresholds

The two example values must never become approval thresholds.

However, do not prohibit every possible amount-based approval threshold forever. If Caritas later approves an authority matrix containing thresholds, the system may enforce it separately.

Any such threshold must come from a formal approved authority/policy source, have an effective date and version, identify authority and scope, and be auditable. It must never be inferred from Rp50m or Rp100m examples.

### FIN-CR-10 — Acceptance test scope

FIN-AMT-10 should search application logic, configuration, validation rules, migrations, and seed data for hardcoded caps/defaults/thresholds. It should not fail merely because the immutable SOP source or clarification document contains the example numbers.

Tests in the addendum have not been executed. Their status must be `TEST_DESIGNED`, not `PASS`.

### FIN-CR-11 — Missing budget dimensions

Before a full Finance data dictionary is finalized, determine whether the process requires:
- Budget period/fiscal year.
- Program and activity hierarchy.
- Budget category/expense category.
- Budget line.
- Quantity and unit cost, where relevant.
- Funding-source allocation.
- Commitment.
- Actual transaction.
- Supporting document.
- Revision and approval history.

Do not add every field automatically. Map each dimension to an SOP, approved finance policy, or explicitly accepted technical requirement.

### FIN-CR-12 — Budget versus transaction controls

Keep distinct:
- Budget proposal.
- Approved budget.
- Budget allocation.
- Commitment/encumbrance, if used.
- Purchase request/purchase order.
- Invoice.
- Payment.
- Expense recognition.
- Reversal/refund.
- Financial report.

Do not treat procurement request, purchase order, invoice, payment, or expense as interchangeable. Reconcile their accounting relationship with the full SOP and finance templates.

## 4. Revised status classification

| Requirement | Correct status |
|---|---|
| Rp50m and Rp100m are illustrative only | `CLARIFIED_BY_PROJECT_OWNER` |
| Do not hardcode those amounts as caps/defaults/thresholds | `CLARIFIED_BY_PROJECT_OWNER` |
| Budget value varies by program/activity needs and approved funding | `CLARIFIED_BY_PROJECT_OWNER` |
| Separate proposed and approved budget | `TECHNICAL_RECOMMENDATION` / accepted project requirement if owner approves |
| Preserve budget revision history | `TECHNICAL_RECOMMENDATION` / accepted project requirement if owner approves |
| Actual reports derive from Finance transactions | `TECHNICAL_RECOMMENDATION` / accepted project requirement if owner approves |
| Funding-source traceability | `TECHNICAL_RECOMMENDATION` / accepted project requirement if owner approves |
| APP Nasional restrictions | Retain SOP evidence from relevant page; full rules require source verification |
| Ketua TSKKM approval for standby-fund expenditure | Preserve as source-derived requirement from partial SOP audit; identity/authority mapping remains pending |
| Remaining budget formula | `PENDING_ORG_DECISION` / pending approved finance policy |
| Funding-source cardinality | `PENDING_DESIGN_DECISION` |
| Accounting recognition and commitment basis | `PENDING_ORG_DECISION` |
| Currency precision, storage type, rounding | `TECHNICAL_RECOMMENDATION` pending physical design and policy |

---

# PART B — INDEPENDENT DESK TESTS

These are scenario-based design tests. They are not evidence that an application has been executed or passed.

| Test ID | Scenario | Expected result | Status |
|---|---|---|---|
| FIN-TEST-01 | Proposals of Rp25m, Rp75m, Rp250m | Can be recorded under approved validation; no Rp50m/Rp100m cap or default | `TEST_DESIGNED` |
| FIN-TEST-02 | Proposed Rp75m; approved Rp60m | Values remain separate; approved amount links to valid approval | `TEST_DESIGNED` |
| FIN-TEST-03 | Approved version 1 Rp60m; revision request Rp68m without approval | Version 1 remains effective; Rp68m is not treated as approved | `TEST_DESIGNED` |
| FIN-TEST-04 | One program proposes two funding sources | Explicit allocation records if allowed, or clear rejection under approved one-source rule | `TEST_DESIGNED` |
| FIN-TEST-05 | Expense category may be excluded from a funding source | Apply only verified rules; otherwise flag for manual review | `TEST_DESIGNED` |
| FIN-TEST-06 | Report actual expenditure from a posted transaction | Amount derives from canonical transaction; no editable duplicate amount | `TEST_DESIGNED` |
| FIN-TEST-07 | Approved budget Rp60m, actual Rp20m, open PO Rp10m | Do not assert final remaining budget until commitment basis is approved | `TEST_DESIGNED` |
| FIN-TEST-08 | User with edit permission attempts to approve revision without authority | Denied and audited; edit permission does not imply approval authority | `TEST_DESIGNED` |
| FIN-TEST-09 | Same revision command retried with same idempotency key | One revision only; retry returns original result | `TEST_DESIGNED` |
| FIN-TEST-10 | Two users revise same budget version concurrently | Stale-version/conflict detected; no silent overwrite | `TEST_DESIGNED` |
| FIN-TEST-11 | Generate financial report | Actual amounts trace to posted/authorized source records; no duplicate transactions | `TEST_DESIGNED` |
| FIN-TEST-12 | Transaction reversed/refunded | Original remains auditable; reversal links to original; accounting treatment follows approved policy | `TEST_DESIGNED` |

---

# PART C — NEXT GITHUB COPILOT PROMPT

## 5. Prompt identity

**Prompt ID:** SIMTDB-REV05112026-P00-03-FIN  
**Output filename:** `SIMTDB_REV05112026_00_03_FINANCE_CLARIFICATION_REAUDIT.md`  
**Mode:** Re-audit and specification correction only  
**No implementation:** Mandatory

## 6. COPY THIS PROMPT TO GITHUB COPILOT

Act as a Principal Finance Systems Architect, Enterprise Data Architect, Senior Business Analyst, Database Architect, Security Architect, and QA Lead.

Re-audit these project documents:
1. `SIMTDB_REV05112026_00_02_FINANCIAL_AMOUNT_CLARIFICATION.md`
2. `SIMTDB_REV05112026_00_01_SOP_PARTIAL_AUDIT.md`
3. `SIMTDB_REV05112026_00_01_AUDIT_AND_CORE_FOUNDATION_ANALYSIS.md`
4. Relevant Master Prompt V1.0 and CHR materials available in the workspace.
5. Official SOP pages 16–29 currently available in the workspace.
6. Page 49 and complete finance templates, if available.

### A. Owner clarification — controlling interpretation

The project owner clarified:
- Rp50,000,000 and Rp100,000,000 are illustrative amounts only.
- They are not fixed amounts, caps, mandatory defaults, maximum expenditure limits, or automatic approval thresholds.
- Amounts may be adjusted according to program/activity needs, disaster conditions, funding sources, and approved budgets.
- This clarification does not change other SOP requirements or approval authorities.

Use `CLARIFIED_BY_PROJECT_OWNER` only for statements directly supported by this clarification. Do not label every technical recommendation as an owner-confirmed organizational or accounting policy.

### B. Audit the existing addendum

Verify:
1. Whether all references to Rp50m and Rp100m are correctly interpreted.
2. Whether either amount is accidentally used as a default, cap, threshold, or hardcoded rule.
3. Whether the addendum overstates owner approval of proposed/approved/revised/actual/remaining budget controls.
4. Whether actual amount is duplicated between transaction and expenditure reference.
5. Whether one `funding_source_id` is sufficient.
6. Whether multiple funding sources and expense allocations need explicit relationships.
7. Whether source restrictions are preserved and represented safely.
8. Whether `program_id / activity_id` creates an ambiguous or polymorphic foreign key.
9. Whether revision history distinguishes requested, approved, rejected, effective, and superseded revisions without inventing official status labels.
10. Whether remaining budget is incorrectly treated as a final formula.
11. Whether transaction, commitment, invoice, payment, expense recognition, refund, and reversal are separated.
12. Whether currency, decimal precision, rounding, and exchange-rate assumptions are controlled.
13. Whether approval thresholds can only be introduced from a formal approved authority source.
14. Whether acceptance tests are correctly marked as designed, not executed.

### C. Preserve SOP requirements

Use the partial SOP audit as evidence, but do not claim the entire SOP has been audited.

Preserve:
- Source names and page references.
- Funding sources identified in pages 23–24.
- The source-derived statement that expenditure of standby funds requires approval from Ketua TSKKM, while formal identity/authority mapping remains pending.
- Restrictions on APP Nasional funds as recorded in the SOP partial audit.
- Other relevant Finance requirements without altering them.

If page 49 is unavailable, state `EVIDENCE_NOT_AVAILABLE`. Do not infer exact template fields.

### D. Produce corrected specifications

Create:
1. Corrected Financial Business Rule Register.
2. Corrected Financial Source of Truth Matrix.
3. Funding Source and Restriction Model proposal.
4. Budget Lifecycle and Revision State Model proposal.
5. Finance Entity Registry additions.
6. Finance Data Dictionary corrections.
7. Approval Authority dependencies.
8. Finance-to-Procurement integration dependency matrix.
9. Report lineage specification.
10. Updated CHR-020 mapping.
11. Pending Finance Decision Register.
12. Revised acceptance test plan.

### E. Data integrity requirements

Ensure:
- No duplicate source of truth for actual amounts.
- No loose polymorphic foreign key without integrity strategy.
- Budget revision history is preserved.
- Multiple funding-source relationships are explicit if allowed.
- Source restrictions are never invented.
- Approval authority is separate from edit permission.
- No unapproved approval threshold is created.
- Remaining budget is not finalized before its formula is approved.
- Reports trace to canonical financial transactions.
- Idempotent retries cannot create duplicate budget revisions or financial transactions.
- Concurrent revisions cannot silently overwrite each other.

### F. Test classification

For every test use one of:
- `TEST_DESIGNED`
- `TEST_EXECUTED_PASS`
- `TEST_EXECUTED_FAIL`
- `BLOCKED_BY_MISSING_POLICY`
- `BLOCKED_BY_MISSING_SOURCE`

Never claim a test passed unless an actual executable test was run and evidence is supplied.

### G. Output and stop rules

Save as:
`SIMTDB_REV05112026_00_03_FINANCE_CLARIFICATION_REAUDIT.md`

Do not:
- Write application code.
- Create database tables or migrations.
- Change existing project files.
- Set physical DBMS types.
- Invent accounting policies.
- Invent approval authorities.
- Treat the two illustrative values as thresholds.
- Mark CHR-020 fully resolved.

End with:
1. Executive conclusion.
2. Corrected issue register.
3. Remaining blockers.
4. Evidence still required.
5. Whether Finance specification is READY, CONDITIONAL, or BLOCKED.
6. The exact next prompt recommended.

Wait for project owner review.

---

# PART D — REVIEW GATE

## 7. Conditions before Finance design can be finalized

The Finance module must not move to physical schema or implementation until:
- Full SOP Finance/Procurement pages and templates are inspected.
- Page 49 and relevant finance forms are verified.
- Funding-source restrictions are transcribed and validated.
- Authority for standby-fund expenditure is mapped to an approved organizational identity/mandate.
- Relationship between program, activity, budget, and funding source is defined.
- Actual-expenditure source of truth is fixed.
- Budget revision lifecycle is approved.
- Remaining-budget calculation basis is approved.
- Procurement and Finance transaction boundaries are reconciled.
- Acceptance tests are implemented and executed in the eventual application.

**Final principle:** flexible budget values do not mean uncontrolled spending. The system must support variable approved amounts while preserving funding restrictions, authority, evidence, transaction integrity, and auditability.
