# SIM-TDB — FINANCE LOGICAL ARCHITECTURE R02
## Enterprise Logical Architecture, Entity Catalogue, Relationship Specification & Financial Integrity Design

**Document ID:** SIMTDB-REV05112026-00-14-FIN-LA-R02  
**Filename:** `SIMTDB_REV05112026_00_14_FINANCE_LOGICAL_ARCHITECTURE_R02.md`  
**Revision:** REV05112026-R02  
**Status:** Draft logical architecture untuk audit ulang dan review  
**Mode:** Logical architecture only — read-only, no physical implementation  
**Project:** Sistem Informasi Manajemen Tanggap Darurat Bencana (SIM-TDB)  
**Organization:** Caritas Keuskupan Malang — Tim Solidaritas Kemanusiaan Keuskupan Malang (TSKKM)

---

## 1. Executive Summary

R02 adalah koreksi dan harmonisasi Finance Logical Architecture R01 berdasarkan Finance Decision Register R05.1 dan Correction Register CR-001 sampai CR-016.

R02:

- Mempertahankan GOV-01 sampai GOV-09, FIN-DEC-01 sampai FIN-DEC-33, dan FIN-TEST-01 sampai FIN-TEST-105.
- Melengkapi entity inventory, ownership, logical attributes, lifecycle, source-of-truth boundary, dan decision dependencies.
- Membedakan **Financial Obligation** dari **Financial Closure Blocker**.
- Memisahkan **Funding Source Allocation** dari **Funding Assignment** sebagai dua tanggung jawab konseptual yang mungkin perlu model terpisah. Keputusan final tetap menunggu FIN-DEC-10/14.
- Memisahkan **Cash Ledger**, **Ceiling Consumption Ledger**, dan **Expenditure Ledger**. Reservation, consumption, release, cash movement, disbursement, expenditure recognition, dan reconciliation bukan satu transaksi atau satu status.
- Menyediakan Policy Amendment, Policy Lock Evaluation, Cash Evidence, Authority Evidence, Mandate/Delegation, Program State, Closure Authorities, Reconciliation Discrepancy, Advance, dan Commitment concepts.
- Menambahkan relationship catalogue yang dapat ditelusuri; hubungan yang belum disetujui tetap bertanda pending dan tidak memiliki cardinality final.
- Menyediakan conceptual ERD, SOP traceability terbatas pada halaman yang tersedia, test traceability, integration contracts, dan correction log.

### Status akhir

| Area | Status |
|---|---|
| Finance Logical Architecture R02 | Draft; siap untuk audit ulang dokumen |
| Finance Logical Architecture Final | `BLOCKED` sampai keputusan kritis dan evidence tersedia |
| Physical Database Design | `NO_GO` |
| Implementation | `NO_GO` |

Tidak ada SQL, physical table, migration, seed, API, code, atau database yang dibuat atau diubah. Tidak ada test yang dijalankan.

---

## 2. Document Control and Revision History

| Versi | Deskripsi |
|---|---|
| Finance Logical Architecture R01 | Logical entity catalogue, process flows, relationship catalogue, integration outline, dan traceability awal. |
| Finance Decision Register R05.1 | Baseline governance, FIN-DEC-01–33, dan FIN-TEST-01–105. |
| Correction Register CR-001–CR-016 | Menetapkan temuan dan acceptance criteria untuk koreksi R01 ke R02. |
| **Finance Logical Architecture R02** | **Melengkapi katalog entity/attributes, normalisasi ownership, relationships, ledgers, authority, reconciliation, integration, SOP traceability, test traceability, dan correction disposition.** |

R02 mempertahankan histori R01, R05.1, dan Correction Register. Perubahan arsitektur tidak mengubah source SOP atau menyelesaikan keputusan organisasi yang masih pending.

---

## 3. Source Authority and Evidence Classification

### 3.1 Evidence yang tersedia

| Sumber | Status | Batas |
|---|---|---|
| Finance Decision Register R05.1 | Tersedia dalam konteks proyek dan digunakan sebagai baseline | Working decision register; bukan pengganti SOP atau keputusan formal. |
| GOV-01–GOV-09 dan owner clarifications | Tersedia dalam percakapan/dokumen | Project-owner requirements; tidak membuktikan SK/mandate tertentu telah diterbitkan. |
| SOP gambar halaman cetak 16–29 | Tersedia dan ditelaah | Halaman 23–24 relevan untuk Finance; pemeriksaan SOP tetap parsial. |
| SOP halaman 1–15 dan 30–95 | `EVIDENCE_NOT_AVAILABLE` | Tidak direkonstruksi. |
| SOP Finance p.40–41, template p.49, SOP p.62–69 | `EVIDENCE_NOT_AVAILABLE` | Template dan detail prosedur belum diverifikasi. |
| SK, mandate/delegation, approval matrix, closure authority evidence | `EVIDENCE_NOT_AVAILABLE` | Tidak tersedia untuk verifikasi formal. |
| Repository/code/database/schema/migration/seed | `EVIDENCE_NOT_AVAILABLE` | Tidak diperiksa atau diubah. |
| Test execution environment/report | `EVIDENCE_NOT_AVAILABLE` | Tidak ada test yang dijalankan. |

### 3.2 Provenance labels

- `SOP_CONFIRMED`: didukung langsung oleh bagian SOP yang tersedia dan terbaca.
- `CLARIFIED_BY_PROJECT_OWNER`: klarifikasi pemilik proyek yang dapat ditelusuri.
- `PROJECT_OWNER_GOVERNANCE_REQUIREMENT`: governance requirement sistem yang ditetapkan pemilik proyek.
- `ORG_DECISION_CONFIRMED`: hanya bila bukti keputusan formal tersedia dan diverifikasi.
- `SOURCE_CONFLICT`: sumber atau interpretasi belum direkonsiliasi.
- `EVIDENCE_NOT_AVAILABLE`: bukti belum tersedia.
- `PENDING_ORG_DECISION`: menunggu keputusan organisasi/Finance.
- `PENDING_DESIGN_DECISION`: menunggu keputusan desain domain/arsitektur.
- `TECHNICAL_RECOMMENDATION`: rekomendasi teknis, bukan kebijakan organisasi.

Project-owner requirement tidak membuktikan bahwa SK, signatory, mandate, delegation, atau authority organisasi tertentu telah diterbitkan dan diverifikasi.

### 3.3 Test labels

- Test belum dijalankan: `TEST_DESIGNED`.
- Detail test/source tidak tersedia: `EVIDENCE_NOT_AVAILABLE` atau execution readiness yang sesuai.
- Tidak ada `TEST_EXECUTED_PASS` atau `TEST_EXECUTED_FAIL` pada R02.
- Semua Actual Result tetap **Not Executed**.

---

## 4. Governance Requirements

### 4.1 GOV-01 sampai GOV-09

Seluruh governance requirement dipertahankan tanpa perubahan substansi dan status.

| ID | Requirement | Status |
|---|---|---|
| GOV-01 | Master Policy ditetapkan sebelum program operasional dimulai. | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| GOV-02 | Tidak ada program operasional yang boleh aktif tanpa policy yang berlaku. | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| GOV-03 | Policy setup/amendment terkunci saat ada program berjalan atau belum resmi ditutup. | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| GOV-04 | Policy amendment juga terkunci sampai program dan seluruh keuangan terkait selesai. | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| GOV-05 | Hanya kapabilitas SuperAdmin yang dapat melakukan setup awal dan amendment yang memenuhi syarat. | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| GOV-06 | Setiap amendment memerlukan SK Pengaturan terlampir dengan detail yang dapat ditelusuri. | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| GOV-07 | SK Pengaturan tidak membypass program/financial closure gate. | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| GOV-08 | Tidak ada SuperAdmin override saat policy terkunci. | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| GOV-09 | Amendment menghasilkan policy version baru dan histori tidak ditimpa diam-diam. | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |

### 4.2 Boundary

GOV-01–GOV-09 tidak menetapkan otomatis status program, canonical closure records, closure authority, policy mode awal, eligible-cash formula, atau ceiling-consuming event. Detail tersebut tetap pada FIN-DEC register.

---

## 5. Finance Domain Boundaries

| Domain | Owner konseptual | Tanggung jawab Finance | Boundary |
|---|---|---|---|
| Core/IAM | Core/IAM | Mengonsumsi actor, role, permission, SuperAdmin capability references | Finance tidak menggandakan user/role/permission master. |
| Program Management | Program | Membaca Program, Activity, Program State, dan closure evidence references | Finance bukan source of truth Program/Activity. |
| Incident Management | Incident | Membaca Incident reference | Finance tidak membuat duplicate incident master. |
| Response Operations | Response Operations | Membaca Response Operation reference | Operation tidak diasumsikan sama dengan Incident atau Program. |
| Procurement | Procurement | Membaca request, PO, invoice, dan commitment references yang relevan | Finance tidak memiliki salinan editable PO/invoice master. |
| Logistics/Inventory | Logistics/Inventory | Membaca goods-receipt/stock evidence references jika relevan | Finance tidak menjadi source of stock movements. |
| Document Management | Document Management | Menghubungkan financial processes ke document references | Finance tidak menimpa atau menggandakan document master. |
| Finance | Finance | Mengelola request, policy references, financial events, ledgers, obligations, reconciliation sesuai policy | Canonical accounting treatment masih memerlukan decisions. |
| Reporting/Audit | Reporting/Audit | Mengonsumsi derived financial facts dan audit evidence | Laporan bukan source transaksi alternatif. |

---

## 6. Policy and Ceiling Architecture

### 6.1 Nilai kebijakan

- **Rp50.000.000:** batas maksimum pengeluaran dana darurat untuk satu kejadian/operasi respons berdasarkan klarifikasi pemilik proyek. Bukan jumlah wajib untuk dihabiskan, bukan cap global semua kejadian, dan bukan konstanta permanen. `CLARIFIED_BY_PROJECT_OWNER`.
- **Rp100.000.000:** nilai ilustratif saja; bukan default, ceiling, global cap, maximum, atau approval threshold. `CLARIFIED_BY_PROJECT_OWNER`.
- Nilai aktif, mode, scope, dan tanggal berlaku merupakan bagian dari Master Policy yang terkendali.
- Nilai awal dan mode awal belum menjadi konfigurasi aktif tanpa keputusan yang sah.

### 6.2 Aggregation modes

| Mode | Logical behavior | Pending detail |
|---|---|---|
| `PER_INCIDENT` | Ceiling dihitung kumulatif per control unit kejadian/operasi yang ditetapkan dalam policy. Kejadian berbeda dapat memiliki batas tersendiri, dengan syarat cash dan approval rules terpenuhi. | Real-world Incident vs formally independent Response Operation: FIN-DEC-04. |
| `GLOBAL_ALL_INCIDENTS` | Satu ceiling digunakan bersama untuk incident yang masuk scope policy. | Scope boundary, membership, period, reset/supersession: FIN-DEC-05/06. |

Mode hybrid tidak diasumsikan.

### 6.3 Policy Freeze versus aggregation scope

| Concept | Menjawab pertanyaan | Basis |
|---|---|---|
| Policy Freeze Scope | Kapan policy setup/amendment terkunci? | GOV-03/GOV-04 |
| Ceiling Aggregation Scope | Kejadian/transaksi mana berbagi ceiling? | Active Policy Version dan selected mode |
| Fund Pool Eligibility Scope | Dana apa yang eligible untuk request? | Finance/source restriction decision |
| Financial Reporting Scope | Record apa yang menjadi dasar laporan? | Finance/accounting policy |

Freeze scope tidak menentukan bahwa semua kejadian memakai global ceiling. Aggregation scope tidak mengganti atau mempersempit policy freeze.

### 6.4 Policy governance concepts

| Concept | Logical responsibility | Dependency |
|---|---|---|
| Master Policy | Mengidentifikasi policy dan versi yang mengatur Finance controls. | GOV-01–09; FIN-DEC-02–07/21 |
| Policy Version | Menyimpan perubahan amount/mode/scope/effective references tanpa menimpa histori. | GOV-09; FIN-DEC-23/24 |
| Policy Amendment | Menautkan old/new version, SK, actor, lock evaluation, dan activation decision. | GOV-06/07/09; FIN-DEC-19/20/22 |
| Policy Freeze Scope | Membaca status Program dan financial closure gates. | GOV-03/04; FIN-DEC-16–18/29 |
| Policy Lock Evaluation | Menjelaskan mengapa policy change locked atau eligible pada waktu evaluasi. | FIN-DEC-16–18/29 |
| Ceiling Aggregation Scope | Menetapkan aggregation mode dan membership. | FIN-DEC-03–06/27/28 |
| Policy Scope Membership | Menghubungkan scope dengan Program/Incident/Response Operation bila disahkan. | FIN-DEC-05/27/28 |

---

## 7. Entity Classification and Ownership

### 7.1 Kategori

- **Finance-Owned Business Entity:** record proses bisnis Finance.
- **Finance-Owned Configuration Entity:** controlled Finance policy/reference.
- **Business Event:** kejadian transaksi atau keputusan.
- **Ledger Record/Projection:** event record set atau derived ledger view.
- **External Module Reference:** canonical record yang dimiliki modul lain.
- **Evidence/Document Reference:** document-owned reference.
- **Derived Evaluation Record:** evaluation yang dihitung dari canonical source records.
- **Value Object/Logical Reference:** logical concept yang tidak otomatis menjadi persisted entity.

### 7.2 Entity Ownership Matrix

| Entity/concept | Classification | Data owner | Source of truth | Finance responsibility | Lifecycle | Dependency |
|---|---|---|---|---|---|---|
| Master Policy | Finance-Owned Configuration | Policy authority to be designated; SuperAdmin executes | Approved policy version registry | Configure/reference policy under governance | Initial/active/amended/superseded | GOV-01–09; FIN-DEC-02–07/21 |
| Policy Version | Finance-Owned Configuration | Finance policy governance | Versioned policy history | Bind applicable policy without overwriting history | Candidate/active/superseded | GOV-09; FIN-DEC-23/24 |
| Policy Amendment | Business Event/governance record | Finance policy governance | Amendment record + SK reference | Record old/new version, actor, gate result | Draft/validated/activated candidates | GOV-06/07/09; FIN-DEC-19/20/22 |
| Policy Freeze Scope | Value Object/Derived Evaluation input | Core policy governance consumes modules | Program/Finance states and evidence | Apply freeze requirement | Re-evaluated | GOV-03/04; FIN-DEC-16–18/29 |
| Policy Lock Evaluation | Derived Evaluation Record | Core/policy governance | Evaluation result with source references | Explain gate outcome | Append evaluation history candidate | FIN-DEC-16–18/29 |
| Ceiling Aggregation Scope | Finance-Owned Configuration | Finance policy governance | Active policy version | Define aggregation context | Effective per policy version | FIN-DEC-03–06 |
| Policy Scope Membership | External-reference association candidate | Scope owner to be designated | Program/Incident/Operation canonical references | Read membership for ceiling aggregation | Effective-dated candidate | FIN-DEC-05/27/28 |
| Program | External Module Reference | Program Management | Program module | Read program identity/state | Program-owned lifecycle | FIN-DEC-17/18/28 |
| Program State | External Module Reference | Program Management | Program state history | Consume for freeze evaluation | Program-owned | FIN-DEC-17 |
| Program Closure Evidence | Evidence/External Reference | Program Management | Program closure record/document | Read closure gate evidence | Program-owned | FIN-DEC-17/18 |
| Program Closure Authority | External Authority Reference | Organization/Program authority owner | Mandate/decision evidence | Validate reference only | Effective/revoked candidate | FIN-DEC-18 |
| Activity | External Module Reference | Program Management | Program module | Consume activity context | Program-owned | FIN-DEC-14/16 |
| Program Budget | Finance-owned record or approved shared contract | Finance owns financial facts; Program owns Program | Approved Finance budget records | Budget lifecycle/allocation/reporting | Proposed/approved/revised candidates | FIN-DEC-14/15 |
| Budget Line | Finance-owned detail candidate | Finance | Finance budget model | Budget detail | Follows approved budget lifecycle | FIN-DEC-14/15 |
| Incident | External Module Reference | Incident Management | Incident module | Consume incident context | Incident-owned | FIN-DEC-04/27 |
| Response Operation | External Module Reference | Response Operations | Response module | Consume operation context | Operations-owned | FIN-DEC-04/27 |
| Fund Source | Finance reference or authoritative funding master | Owner to be designated | Approved funding-source register | Track source and restrictions reference | Controlled reference lifecycle | FIN-DEC-10/11 |
| Funding Source Allocation | Finance relationship/event candidate | Finance | Approved source-to-pool allocation | Assign source to pool if approved | Versioned relationship candidate | FIN-DEC-10 |
| Funding Assignment | Finance relationship/event candidate | Finance | Approved allocation/assignment | Assign funding to request/budget/activity target if allowed | Versioned/correctable candidate | FIN-DEC-10/14 |
| Fund Pool | Finance configuration/business concept | Finance | Approved pool definition | Group eligible funds only as authorized | Effective-dated candidate | FIN-DEC-08/10/11 |
| Cash Account | External or Finance account reference | Finance/accounting owner to be designated | Finance account records | Link cash source | Account lifecycle | FIN-DEC-08/26 |
| Cash Evidence | Evidence/Document Reference | Finance and Document Management boundary | Statement/balance evidence | Track source, time, verification/freshness | Versioned evidence | FIN-DEC-08/09 |
| Eligible Cash Evaluation | Derived Evaluation Record | Finance | Cash source, restrictions, reservation rules | Evaluate eligible amount | Evaluation history | FIN-DEC-08/09/11 |
| Cash Reservation/Encumbrance | Business Event candidate | Finance | Approved cash-control process | Record reservation if adopted | Reserve/release/convert candidates | FIN-DEC-09/32 |
| Cash Movement Event | Business Event | Finance | Cash source transaction | Record cash movement | Append/correction history candidate | FIN-DEC-08/09/31 |
| Cash Ledger | Ledger Record/Projection | Finance | Cash events/accounting source | Present cash position/movement | Source model pending | FIN-DEC-08 |
| Fund Request | Finance-Owned Business Entity | Finance | Finance request record | Request lifecycle and context links | Request states pending | FIN-DEC-07/08/10/33 |
| Actor/User Account Reference | External Module Reference | Core/IAM | IAM | Reference actor | IAM-owned lifecycle | FIN-DEC-20 |
| Role/Permission Reference | External Module Reference | Core/IAM | IAM | Consume permissions | IAM-owned | Core/IAM decisions |
| SuperAdmin Capability | External Module Reference/capability | Core/IAM governance | IAM capability assignment | Permit policy setup under GOV-05 | Provision/revoke candidates | GOV-05; FIN-DEC-20 |
| Financial Approval Authority | Authority Reference/Value Object | Organization | Mandate/decision evidence | Validate approval basis | Effective/revoked candidate | FIN-DEC-33 |
| Authority Evidence | Evidence/Document Reference | Organization/Document Management | Formal authority document | Support authority verification | Versioned evidence | FIN-DEC-19/33 |
| Mandate/Delegation | Authority Evidence/logical entity candidate | Organization | Formal mandate/delegation | Define delegated scope/time | Effective/expired/revoked candidates | FIN-DEC-33 |
| Approval Decision | Business Event | Finance/authority process | Decision record and authority evidence | Record outcome and actor | Append decision history candidate | FIN-DEC-19/22/33 |
| Ceiling Reservation Event | Business Event candidate | Finance | Policy semantics | Reserve ceiling if adopted | Reserve/release/convert candidates | FIN-DEC-07 |
| Ceiling Consumption Event | Business Event | Finance | Approved consumption event rule | Record ceiling effect | Append/correction candidates | FIN-DEC-07/31/32 |
| Ceiling Release/Reversal Event | Business Event candidate | Finance | Original ceiling event | Reverse/release prior event if allowed | Linked correction event | FIN-DEC-31/32 |
| Disbursement Event | Business Event | Finance | Disbursement/payment evidence | Record funds released | Initiated/outcome candidate lifecycle | FIN-DEC-08/12/33 |
| Expenditure Recognition | Business Event/Finance record | Finance | Approved recognition source | Record expense recognized for reporting | Recognize/correct candidates | FIN-DEC-12/31 |
| Expenditure Ledger | Ledger Record/Projection | Finance | Expenditure recognition records | Present recognized expense | Source model pending | FIN-DEC-12 |
| Financial Obligation | Finance-Owned Business Entity | Finance; source may vary | Canonical payable/advance/commitment/other obligation | Track actual financial responsibility | Open/settled/disputed candidates | FIN-DEC-16/31 |
| Financial Closure Blocker | Derived evaluation/business issue candidate | Finance closure process | Obligation/evidence/source-state evaluation | Record unresolved closure condition | Open/cleared/disputed candidates | FIN-DEC-16/18/29 |
| Financial Reconciliation | Finance-Owned process/case | Finance | Reconciliation record/source records | Compare records and resolve discrepancy | Open/partial/unresolved/corrected/closed candidates | FIN-DEC-12/16/18/31 |
| Reconciliation Item | Reconciliation detail candidate | Finance | Source records in a reconciliation | Compare record-level values | Per reconciliation process | FIN-DEC-16 |
| Reconciliation Discrepancy | Derived/business issue candidate | Finance | Comparison result | Track discrepancy and resolution | Open/resolved/disputed candidates | FIN-DEC-16/31 |
| Financial Closure Evidence | Evidence/Document Reference | Finance/Document Management | Reconciliation/closure records | Support financial closure gate | Submitted/verified/accepted candidates | FIN-DEC-18 |
| Financial Closure Authority | External Authority Reference | Organization | Formal mandate/decision | Certify Finance closure if authorized | Effective/revoked candidates | FIN-DEC-18 |
| Financial Document | Evidence/Document Reference | Document Management | Document service | Link evidence to Finance process | Document-owned lifecycle | GOV-06/document governance |
| Audit Reference | Audit record/event | Audit/Core | Audit service/source records | Trace actor/action/time/target | Append-only logical history | GOV-09 |
| Correlation Reference | Value Object/Logical Reference | Shared system integration | Process context | Group related process events | Scoped candidate | Technical design |
| Causation Reference | Value Object/Logical Reference | Shared system integration | Source event | Link event to cause | Candidate immutable link | Technical design |
| Source Transaction Reference | Value Object/External Reference | Owning source module | Canonical source record | Point to source of truth | Source-owned lifecycle | Domain source-of-truth decisions |

### 7.3 Entity Count and classification note

R01 refers to 44 entity candidates, while its named logical concepts include concepts that may be references, derived records, events, or value objects rather than independent business entities. R02 lists all named concepts above and classifies them; it does not assert that every concept must become a persisted entity. The original count is retained as historical wording, not used as a physical table count.

---

## 8. Entity Attribute Catalogue

Atribut berikut adalah candidate logical attributes. “Required” means required in the logical concept when the relevant event/process exists; it does not create an operational requirement absent a source. No physical types are specified.

### 8.1 Policy and Governance

| Entity | Attribute | Meaning | Requiredness | Source/validation | Lifecycle | Evidence status | Dependency |
|---|---|---|---|---|---|---|---|
| Master Policy | Policy reference | Identitas policy | Candidate required | Stable, non-reused reference | Setup/versioned | `TECHNICAL_RECOMMENDATION` | FIN-DEC-21 |
| Master Policy | Policy name/description | Label dan tujuan | Candidate | Tidak mengubah policy meaning | Versioned | `TECHNICAL_RECOMMENDATION` | — |
| Master Policy | Governing source reference | Basis policy | Required in concept | Must reference available/approved source | Retained | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` | FIN-DEC-21 |
| Master Policy | Current version reference | Active policy version | Required for active policy | Must point to one policy version according to approved rules | Changes by amendment | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` | FIN-DEC-23/24 |
| Policy Version | Version reference/number | Identitas versi | Candidate required | Immutable history | Draft/active/superseded candidates | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` | GOV-09 |
| Policy Version | Configured amount/currency | Ceiling amount | Conditional on policy mode | Rp50m is reference maximum; active value requires approval; Rp100m illustrative | Versioned | `CLARIFIED_BY_PROJECT_OWNER` | FIN-DEC-02/26 |
| Policy Version | Aggregation mode | `PER_INCIDENT` or `GLOBAL_ALL_INCIDENTS` | Required for active policy | One selected mode unless future approved policy changes it | Versioned | `CLARIFIED_BY_PROJECT_OWNER` | FIN-DEC-03 |
| Policy Version | Scope/control-unit reference | Unit/scope for aggregation | Required according to mode | Must be explicit before activation | Versioned | `PENDING_ORG_DECISION` | FIN-DEC-04/05/06 |
| Policy Version | Effective dates | Applicability interval | Required for activation concept | Dates must not be invented | Versioned | `PENDING_ORG_DECISION` | FIN-DEC-23/24 |
| Policy Version | Governing evidence/SK reference | Basis for version/amendment | Amendment requires SK Pengaturan | Reference original document; no invented SK | Retained | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` | FIN-DEC-19/21 |
| Policy Amendment | Previous/proposed version references | Version transition | Required for amendment concept | System links, not manually retyped source | New amendment record | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` | GOV-06/09 |
| Policy Amendment | SK reference and reason | Amendment evidence/context | Required for amendment per GOV-06 | SK must be verifiable; reason does not replace SK | Retained | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` | FIN-DEC-19/22 |
| Policy Freeze Scope | Program/finance evaluation inputs | Gate basis | Required to evaluate gate | Canonical sources; status mapping pending | Re-evaluated | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` | FIN-DEC-16–18/29 |
| Policy Lock Evaluation | Evaluation time/result/source states | Reconstruct why locked/eligible | Candidate required for traceability | Derived, not manually asserted clear | Append history candidate | `TECHNICAL_RECOMMENDATION` | FIN-DEC-29 |
| Ceiling Aggregation Scope | Mode/scope membership rules | Determine shared ceiling | Required according to selected mode | Must not infer reset/membership | Versioned | `CLARIFIED_BY_PROJECT_OWNER` | FIN-DEC-03–06 |
| Policy Scope Membership | Member reference/type/effective period | Policy scope membership | Conditional | Program/Incident/Operation source references | Effective-dated candidate | `PENDING_DESIGN_DECISION` | FIN-DEC-05/27/28 |

### 8.2 Program, Activity, Budget and Response

| Entity | Attribute | Meaning | Requiredness | Source/validation | Lifecycle | Evidence status | Dependency |
|---|---|---|---|---|---|---|---|
| Program | Canonical program reference | External Program identity | Required when Finance links a program | Read from Program module | Program-owned | `EVIDENCE_NOT_AVAILABLE` for actual model | FIN-DEC-17/28 |
| Program | State/status reference | Running/closed source state | Required for freeze evaluation | Must use Program source vocabulary | Program-owned | `EVIDENCE_NOT_AVAILABLE` | FIN-DEC-17 |
| Program State | State value/effective time/source event | Status history | Source-defined | Do not invent status names | Program-owned history | `EVIDENCE_NOT_AVAILABLE` | FIN-DEC-17 |
| Program Closure Evidence | Closure reference/date/source document/status | Formal program closure evidence | Conditional on closure | Authority/source verification | Program-owned | `EVIDENCE_NOT_AVAILABLE` | FIN-DEC-18 |
| Program Closure Authority | Actor/authority/instrument/scope/effective period | Authority for program closure | Conditional if required | No name/position assumed | Effective/revoked candidates | `EVIDENCE_NOT_AVAILABLE` | FIN-DEC-18 |
| Activity | Canonical activity reference/program context/state | Activity identity and status | Conditional for Finance links | Read from Program module | Program-owned | `EVIDENCE_NOT_AVAILABLE` | FIN-DEC-14/17 |
| Program Budget | Budget reference, program/activity context, amount/status/version/source | Budget facts | Conditional | Lifecycle follows Finance policy | Proposed/approved/revised candidates | `PENDING_ORG_DECISION` | FIN-DEC-14/15 |
| Budget Line | Line reference, category/context, amount/version | Budget detail | Conditional if budget model uses lines | Category source not invented | Follows budget version | `PENDING_DESIGN_DECISION` | FIN-DEC-14 |
| Incident | Canonical incident reference/status | Incident identity | Conditional for emergency fund control | Read from Incident module | Incident-owned | `EVIDENCE_NOT_AVAILABLE` | FIN-DEC-04/27 |
| Response Operation | Canonical operation reference/status/incident context | Operation identity | Conditional | Read from Response module | Operations-owned | `EVIDENCE_NOT_AVAILABLE` | FIN-DEC-04/27 |

### 8.3 Funding, Cash, Request and Approval

| Entity | Attribute | Meaning | Requiredness | Source/validation | Lifecycle | Evidence status | Dependency |
|---|---|---|---|---|---|---|---|
| Fund Source | Source reference/type/restriction reference | Funding origin and restrictions | Required when source is known | Only approved source catalog/rules | Controlled reference | `SOP_CONFIRMED` partial | FIN-DEC-10/11 |
| Funding Source Allocation | Source/pool/effective-period/evidence references | Relates source to pool if approved | Conditional | Cardinality not assumed | Versioned relation candidate | `PENDING_DESIGN_DECISION` | FIN-DEC-10 |
| Funding Assignment | Target/source or pool/amount/purpose reference | Assigns eligible source to target if allowed | Conditional | Must reference approved source and target | Controlled assignment candidate | `PENDING_DESIGN_DECISION` | FIN-DEC-10/14 |
| Fund Pool | Pool reference/source composition/restrictions | Cash-control grouping | Conditional | No source/pool 1:1 assumption | Controlled configuration candidate | `PENDING_ORG_DECISION` | FIN-DEC-08/10/11 |
| Cash Account | Account reference/source owner/status | Cash account context | Conditional | Canonical account source | Account-owned | `EVIDENCE_NOT_AVAILABLE` | FIN-DEC-08/26 |
| Cash Evidence | Evidence reference/account/pool/as-of time/source/verification/freshness | Evidence of cash position | Required for evaluation if adopted | Must identify source/time and verification | Versioned evidence | `PENDING_ORG_DECISION` | FIN-DEC-08/09 |
| Eligible Cash Evaluation | Evaluation reference/as-of time/components/restrictions/result | Derived eligibility outcome | Conditional | Formula not finalized | Evaluation history candidate | `PENDING_ORG_DECISION` | FIN-DEC-08/09/11 |
| Cash Reservation/Encumbrance | Reservation reference/request/pool/amount/status/expiry | Cash reserved if adopted | Conditional | Must avoid double count | Reserve/release/convert candidates | `PENDING_ORG_DECISION` | FIN-DEC-09/32 |
| Cash Movement Event | Event reference/account/type/amount/date/source/actor/evidence | Cash event | Required when movement occurs | Source and outcome evidence | Event/correction history | `PENDING_ORG_DECISION` | FIN-DEC-08/09/31 |
| Cash Ledger | Source event references/as-of position/reconciliation status | Logical cash record set/view | Depends on Finance source model | Derived/recorded per approved accounting source | Ongoing | `PENDING_ORG_DECISION` | FIN-DEC-08 |
| Fund Request | Request reference/actor/context/amount/purpose/source/evidence/status | Request for funding | Required when request occurs | Required fields per process approval | Request lifecycle pending | `PENDING_ORG_DECISION` | FIN-DEC-07/08/10/33 |
| Actor/User Account Reference | IAM subject/account/status reference | Actor identity | Required for authenticated action | IAM canonical identity | IAM-owned | `EVIDENCE_NOT_AVAILABLE` | FIN-DEC-20 |
| Role/Permission Reference | Role/permission/scope reference | Technical authorization | Conditional | Read from Core/IAM | IAM-owned | `EVIDENCE_NOT_AVAILABLE` | Core/IAM decisions |
| SuperAdmin Capability | Capability assignment/actor/effective status | Policy setup capability | Required for policy setup execution | Does not imply financial approval | Provision/revoke candidate | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` | FIN-DEC-20 |
| Financial Approval Authority | Authority/action/scope/amount limit if formal/validity/source | Approval authority reference | Required where approval rule applies | No amount limit invented | Effective/revoked candidates | `EVIDENCE_NOT_AVAILABLE` | FIN-DEC-33 |
| Authority Evidence | Document/instrument/issuer/scope/date/verification | Evidence of authority | Required to validate authority | Only real, retrievable evidence | Versioned | `EVIDENCE_NOT_AVAILABLE` | FIN-DEC-19/33 |
| Mandate/Delegation | Principal/delegate/action/scope/effective dates/revocation/source | Delegated authority | Conditional | Must be supported by formal evidence | Effective/expired/revoked candidates | `EVIDENCE_NOT_AVAILABLE` | FIN-DEC-33 |
| Approval Decision | Decision reference/actor/authority/outcome/time/request/evidence | Financial decision event | Required where approval occurs | Actor and authority separate | Append decision history candidate | `PENDING_ORG_DECISION` | FIN-DEC-19/22/33 |

### 8.4 Ledger, Obligation, Reconciliation and Document

| Entity | Attribute | Meaning | Requiredness | Source/validation | Lifecycle | Evidence status | Dependency |
|---|---|---|---|---|---|---|---|
| Ceiling Reservation Event | Event/source request/policy scope/control unit/amount/release-conversion references | Reserve ceiling if adopted | Conditional | Not final consumption unless policy says so | Reserve/release/convert candidate | `PENDING_ORG_DECISION` | FIN-DEC-07 |
| Ceiling Consumption Event | Policy version/scope/control unit/source event/amount/reversal reference | Event counted against ceiling | Conditional | Event selection pending | Append-linked events | `PENDING_ORG_DECISION` | FIN-DEC-07/31/32 |
| Ceiling Release/Reversal Event | Original event/amount/reason/actor/evidence | Reverse/release ceiling effect | Conditional | Must link original | Linked correction event | `PENDING_ORG_DECISION` | FIN-DEC-31/32 |
| Disbursement Event | Request/approval/amount/date/recipient/account/outcome/evidence | Release/payment of funds | Required if disbursed | Status semantics follow Finance process | Initiated/outcome candidates | `PENDING_ORG_DECISION` | FIN-DEC-08/12/33 |
| Expenditure Recognition | Source transaction/amount/basis/period/correction reference | Expense recognized for reporting | Conditional | Recognition basis pending | Recognize/correct candidates | `PENDING_ORG_DECISION` | FIN-DEC-12/31 |
| Expenditure Ledger | Recognition event references/period/scope/reconciliation status | Logical recognized-expenditure record set | Conditional on finance model | Does not equate cash release to expense | Ongoing | `PENDING_ORG_DECISION` | FIN-DEC-12 |
| Financial Obligation | Obligation reference/type/source/program/activity/budget/amount if monetary/due/status/evidence | Actual financial responsibility | Conditional | May have no amount until source provides it; not all obligations are disbursements | Open/settled/disputed candidates | `PENDING_ORG_DECISION` | FIN-DEC-16/31 |
| Financial Closure Blocker | Blocker reference/type/source record/reason/status/owner/resolution evidence | Unresolved condition preventing closure | Conditional; may have no amount | Derived from approved blocker rules | Open/cleared/disputed candidates | `PENDING_ORG_DECISION` | FIN-DEC-16/18/29 |
| Financial Reconciliation | Case/run/scope/time/source set/outcome/status/evidence | Reconciliation process record | Conditional | Does not overwrite source ledgers | Open/partial/unresolved/corrected/closed candidates | `PENDING_ORG_DECISION` | FIN-DEC-12/16/18/31 |
| Reconciliation Item | Reconciliation/source record pair or group/comparison basis/result | Item-level comparison | Conditional | Does not imply 1:1 | Per reconciliation candidate | `PENDING_DESIGN_DECISION` | FIN-DEC-16 |
| Reconciliation Discrepancy | Discrepancy reference/source records/reason/amount if applicable/resolution | Tracks mismatch | Conditional | Must link source and resolution | Open/resolved/disputed candidates | `PENDING_ORG_DECISION` | FIN-DEC-16/31 |
| Reconciliation Resolution | Resolution reference/discrepancy/correction/reversal/evidence/actor | Resolves discrepancy through controlled action | Conditional | No overwrite of origin | Linked resolution event | `PENDING_ORG_DECISION` | FIN-DEC-31 |
| Financial Closure Evidence | Evidence/source records/reconciliation/status/time | Proof Finance gate completed | Required for gate if defined | Actual closure evidence not available | Submitted/verified/accepted candidates | `PENDING_ORG_DECISION` | FIN-DEC-18 |
| Financial Closure Authority | Authority reference/instrument/scope/validity/actor | Authority for Finance closure | Conditional | Not assumed same as Program authority | Effective/revoked candidates | `PENDING_ORG_DECISION` | FIN-DEC-18 |
| Financial Document | Document reference/type/version/source/access/related-record references | Evidence for multiple relevant processes | Conditional | May relate to multiple records if allowed | Document-owned lifecycle | `TECHNICAL_RECOMMENDATION` | GOV-06/document policy |
| Audit Reference | Actor/action/time/target/outcome/source/policy/correlation | Audit trace | Required conceptually for critical events | No physical mechanism specified | Append-only logical history | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` | GOV-09 |
| Correlation Reference | Process scope/group identity | Groups related process events | Conditional | Scope/uniqueness later design | Process lifecycle | `TECHNICAL_RECOMMENDATION` | Integration design |
| Causation Reference | Cause/source event relation | Explains why an event occurred | Conditional | Corrections/reversals link to origin | Immutable link candidate | `TECHNICAL_RECOMMENDATION` | Transaction design |
| Source Transaction Reference | Canonical source record reference | Points to source of truth | Required when event derives from source | Owner-module reference; no free-text-only linkage | Source-owned lifecycle | `TECHNICAL_RECOMMENDATION` | Domain source-of-truth decisions |

---

## 9. Relationship Catalogue

### 9.1 REL-01–REL-34 retained

| REL ID | Relationship summary | Status/dependency |
|---|---|---|
| REL-01 | Master Policy → Policy Version | `CONFIRMED_CONCEPTUAL`; GOV-09 |
| REL-02 | Policy Version → Program | `PENDING_DESIGN_DECISION`; FIN-DEC-28 |
| REL-03 | Policy Version → Ceiling Aggregation Scope | Candidate; FIN-DEC-03–06 |
| REL-04 | Aggregation Scope → Policy Scope Membership | `PENDING_DESIGN_DECISION`; FIN-DEC-05/27/28 |
| REL-05 | Program → Activity | `PENDING_DESIGN_DECISION`; FIN-DEC-14 |
| REL-06 | Program/Activity → Program Budget | `PENDING_DESIGN_DECISION`; FIN-DEC-14/15 |
| REL-07 | Program Budget → Budget Line | `PENDING_DESIGN_DECISION`; FIN-DEC-14/15 |
| REL-08 | Program ↔ Incident | `PENDING_DESIGN_DECISION`; FIN-DEC-27 |
| REL-09 | Incident ↔ Response Operation | `PENDING_ORG_DECISION`; FIN-DEC-04/27 |
| REL-10 | Fund Source ↔ Fund Pool | `PENDING_DESIGN_DECISION`; FIN-DEC-10 |
| REL-11 | Funding Allocation ↔ Fund Request | `PENDING_DESIGN_DECISION`; FIN-DEC-10 |
| REL-12 | Funding Allocation ↔ Program Budget/Activity | `PENDING_DESIGN_DECISION`; FIN-DEC-10/14 |
| REL-13 | Funding Allocation ↔ Fund Pool | `PENDING_DESIGN_DECISION`; FIN-DEC-10 |
| REL-14 | Fund Pool ↔ Cash Account | `PENDING_DESIGN_DECISION`; FIN-DEC-08/10 |
| REL-15 | Cash Account → Cash Movement Event → Cash Ledger | Candidate; FIN-DEC-08/09 |
| REL-16 | Fund Request ↔ Approval Decision | Candidate process association; FIN-DEC-33 |
| REL-17 | Actor ↔ System Permission/Role Assignment | Candidate external IAM relationship |
| REL-18 | Actor/Authority ↔ Mandate/Delegation Evidence | `PENDING_ORG_DECISION`; FIN-DEC-19/22/33 |
| REL-19 | Fund Request → Ceiling Consumption Event | `PENDING_ORG_DECISION`; FIN-DEC-07 |
| REL-20 | Approval Decision → Ceiling Consumption Event | Candidate if policy selects approval event; FIN-DEC-07 |
| REL-21 | Disbursement → Ceiling Consumption Event | Candidate if policy selects disbursement event; FIN-DEC-07 |
| REL-22 | Disbursement → Cash Movement Event | Candidate, no 1:1 assumption; FIN-DEC-08/09 |
| REL-23 | Disbursement → Expenditure Recognition | `PENDING_ORG_DECISION`; FIN-DEC-12 |
| REL-24 | Financial Obligation ↔ Program | Candidate; FIN-DEC-16 |
| REL-25 | Financial Obligation ↔ Activity | Candidate direct or indirect; FIN-DEC-14/16 |
| REL-26 | Financial Obligation ↔ Program Budget | Candidate; FIN-DEC-14/16 |
| REL-27 | Financial Obligation ↔ Fund Request | Candidate; FIN-DEC-16 |
| REL-28 | Financial Obligation ↔ Disbursement/Expenditure Recognition | Candidate; FIN-DEC-12/16/31 |
| REL-29 | Financial Obligation ↔ Financial Reconciliation | Candidate; FIN-DEC-16/18 |
| REL-30 | Financial Reconciliation ↔ Cash/Ceiling/Disbursement/Expenditure records | Candidate; FIN-DEC-08/12/16 |
| REL-31 | Program Closure Authority → Program Closure Evidence | `PENDING_ORG_DECISION`; FIN-DEC-18 |
| REL-32 | Financial Closure Authority → Financial Closure Evidence | `PENDING_ORG_DECISION`; FIN-DEC-18 |
| REL-33 | Financial Document ↔ Request/Approval/Disbursement/Expenditure/Reconciliation | Candidate; no 1:1 assumption |
| REL-34 | Audit/Correlation/Causation references ↔ Business Events | Candidate traceability; GOV-09 |

### 9.2 REL-35–REL-58 retained from R02 harmonization

| REL ID | Relationship summary | Status/dependency |
|---|---|---|
| REL-35 | Policy Amendment → Previous Policy Version | Candidate; GOV-09 |
| REL-36 | Policy Amendment → Proposed New Policy Version | Candidate; GOV-09 |
| REL-37 | Policy Amendment → SK Pengaturan/Financial Document | Required evidence concept for amendment; GOV-06; FIN-DEC-19/22 |
| REL-38 | Policy Amendment → Policy Lock Evaluation | Candidate; GOV-03/04; FIN-DEC-29 |
| REL-39 | Policy Amendment → Activation Decision/Effective Date | Pending lifecycle; FIN-DEC-23/24 |
| REL-40 | Policy Freeze Evaluation → Program State/Closure Evidence | Candidate; FIN-DEC-17/18 |
| REL-41 | Policy Freeze Evaluation → Financial Blockers/Closure Evidence | Candidate; FIN-DEC-16/18/29 |
| REL-42 | Financial Obligation → Financial Closure Blocker | Candidate; FIN-DEC-16 |
| REL-43 | Financial Closure Blocker → Program/Activity/Budget context | Candidate; FIN-DEC-14/16 |
| REL-44 | Financial Closure Blocker → Request/Disbursement/Expenditure/Reconciliation source records | Candidate; FIN-DEC-16 |
| REL-45 | Financial Obligation/Blocker → Activity | Candidate direct/indirect; FIN-DEC-14/16 |
| REL-46 | Program Closure Authority → Program/Closure Evidence | Pending authority; FIN-DEC-18 |
| REL-47 | Financial Closure Authority → Financial Closure Evidence/Reconciliation | Pending authority; FIN-DEC-18 |
| REL-48 | Cash Evidence → Cash Account/Fund Pool/Eligible Cash Evaluation | Candidate; FIN-DEC-08/09/11 |
| REL-49 | Funding Source Allocation → Fund Source/Fund Pool | Candidate; FIN-DEC-10 |
| REL-50 | Funding Assignment → Request/Program Budget/Activity target | Candidate; FIN-DEC-10/14 |
| REL-51 | Fund Request → Disbursement Event | Candidate; FIN-DEC-07/12/33 |
| REL-52 | Disbursement → Cash Movement/Cash Ledger | Candidate; no 1:1; FIN-DEC-08/09/31 |
| REL-53 | Disbursement → Expenditure Recognition/Expenditure Ledger | Pending accounting treatment; FIN-DEC-12/31 |
| REL-54 | Financial Reconciliation → Reconciliation Item/Discrepancy | Candidate; FIN-DEC-16/18/31 |
| REL-55 | Reconciliation Resolution → Source Correction/Reversal Event | Pending; FIN-DEC-31 |
| REL-56 | Authority Evidence/Mandate → Approval Decision | Pending authority; FIN-DEC-19/22/33 |
| REL-57 | Financial Document → Obligation/Blocker/Closure Evidence | Candidate; FIN-DEC-16/18 |
| REL-58 | Program Budget/Activity → Financial Obligation | Candidate; FIN-DEC-14/16 |

### 9.3 REL-59 onward

| REL ID | Source → Target | Meaning | Cardinality alternatives | Dependency | Evidence Status | Relationship Status |
|---|---|---|---|---|---|---|
| REL-59 | Policy Lock Evaluation → Program State Reference | Records source status used in evaluation | One/multiple states or source snapshots; not fixed | FIN-DEC-17/29 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_DESIGN_DECISION` |
| REL-60 | Policy Lock Evaluation → Program Closure Evidence | Records evidence examined | One/multiple evidence records; not fixed | FIN-DEC-17/18 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_DESIGN_DECISION` |
| REL-61 | Policy Lock Evaluation → Financial Closure Blocker | Records blockers considered | Zero/multiple blockers; result history retained | FIN-DEC-16/18/29 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_DESIGN_DECISION` |
| REL-62 | Policy Lock Evaluation → Financial Closure Evidence | Records evidence examined for Finance gate | One/multiple evidence records; not fixed | FIN-DEC-18/29 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_DESIGN_DECISION` |
| REL-63 | Program Closure Authority → Program | Authority may apply to program closure decision | Scope/cardinality not fixed | FIN-DEC-18 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_ORG_DECISION` |
| REL-64 | Financial Closure Authority → Program/Financial Closure Scope | Authority may apply to financial closure scope | Scope/cardinality not fixed | FIN-DEC-18 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_ORG_DECISION` |
| REL-65 | Financial Obligation → Financial Document | Document may evidence obligation or settlement | One/multiple documents and obligations; not fixed | FIN-DEC-16/31 | `EVIDENCE_NOT_AVAILABLE` | `CANDIDATE_RELATIONSHIP` |
| REL-66 | Cash Reservation/Encumbrance → Cash Movement/Disbursement | Reservation may later release/convert; no double counting | One/multiple candidate transitions; event policy pending | FIN-DEC-09/32 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_ORG_DECISION` |
| REL-67 | Cash Reservation/Encumbrance → Fund Request | Reservation may be created from approved/request context | Optional/multiple alternatives; not fixed | FIN-DEC-09 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_DESIGN_DECISION` |
| REL-68 | Ceiling Reservation Event → Ceiling Consumption/Release Event | Reservation may be converted or released according to policy | Event sequence pending; no 1:1 assumed | FIN-DEC-07/32 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_ORG_DECISION` |
| REL-69 | Expenditure Recognition → Expenditure Correction/Reversal | Correction references recognized source without overwrite | Zero/multiple corrections; not fixed | FIN-DEC-12/31 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_ORG_DECISION` |
| REL-70 | Reconciliation Discrepancy → Reconciliation Resolution | Resolution addresses discrepancy | One/multiple resolutions; no final cardinality | FIN-DEC-31 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_DESIGN_DECISION` |
| REL-71 | Financial Closure Blocker → Financial Closure Evidence | Evidence may resolve or retain blocker | One/multiple evidence records; not fixed | FIN-DEC-16/18/29 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_DESIGN_DECISION` |
| REL-72 | Funding Assignment → Funding Source Allocation | Assignment may consume or reference source allocation if adopted | Relationship optional and model-dependent | FIN-DEC-10/14 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_DESIGN_DECISION` |
| REL-73 | Eligible Cash Evaluation → Cash Evidence/Reservation/Restriction | Evaluation derives from available evidence and approved treatment | Inputs vary by policy; not fixed | FIN-DEC-08/09/11 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_ORG_DECISION` |

REL-59–REL-73 are new logical relationship identifiers. They do not establish physical relationships or cardinality.

---

## 10.1 Cardinality and Dependency Matrix

| Area | Alternatives | Dependencies | Status |
|---|---|---|---|
| Master Policy–Policy Version | Version history with effective version binding | GOV-09; FIN-DEC-23/24 | Candidate |
| Program–Policy Version | Bind on activation, bind by scope, or another approved model | FIN-DEC-28 | Pending |
| Program–Activity–Budget–Budget Line | Program budget, activity budget, or budget header/lines | FIN-DEC-14/15 | Pending |
| Program–Incident–Response Operation | Source-supported one-to-many/many-to-many/other | FIN-DEC-27 | Pending |
| Per-incident unit | Parent incident, formal response operation, or approved unit | FIN-DEC-04 | Pending |
| Global membership/reset | Scope and effective period | FIN-DEC-05/06/28 | Pending |
| Fund source/pool/allocation | Single/multiple and target level | FIN-DEC-10/14 | Pending |
| Request/approval/disbursement | Business workflow and record cardinality | FIN-DEC-07/33 | Pending |
| Cash movement/disbursement | Delayed/partial/one-to-many event alternatives | FIN-DEC-08/09/31 | Pending |
| Disbursement/expenditure recognition | Same-event or separately recognized | FIN-DEC-12/31 | Pending |
| Obligation/blocker/source records | Direct or indirect links, multiple sources | FIN-DEC-14/16 | Pending |
| Reconciliation/items/discrepancies | One case may compare several source records | FIN-DEC-16/18/31 | Pending |
| Program/financial closure authorities | Same actor only if organization approves | FIN-DEC-18 | Pending |

---

## 11. Financial Process Architecture

### 11.1 Process A — Master Policy Setup

1. Authorized SuperAdmin capability is authenticated.
2. Initial governing source and configuration basis are referenced.
3. Amount, mode, and scope are recorded from the approved policy basis.
4. Approval/evidence requirements are checked according to approved governance.
5. Active Policy Version is established only after required gates pass.
6. Program activation references an applicable valid Policy Version.
7. Historical policy versions remain traceable and unchanged.

Initial amount/mode and any approval workflow beyond GOV-01–09 remain pending.

### 11.2 Process B — Program Activation and Freeze

1. Program module provides canonical Program identity and state.
2. System checks that an applicable valid policy exists.
3. Program activation without a valid policy is blocked under GOV-01/02.
4. A running or unclosed program locks policy amendment under GOV-03.
5. After Program closure, financial completion is evaluated separately under GOV-04.
6. Amendment remains locked if either gate is unresolved.
7. Lock evaluation records source references and freshness; source-state mapping is pending.

### 11.3 Process C — Fund Request

1. Request actor creates Fund Request.
2. Request references Program/Activity/Incident/Response Operation as applicable under approved relationship rules.
3. Funding source and eligible pool are evaluated.
4. Cash availability and ceiling availability are evaluated separately.
5. Request creation does not automatically consume ceiling unless FIN-DEC-07 specifies it.
6. Request proceeds to approval under an authority model supported by evidence.

### 11.4 Process D — Approval

1. Resolve actor identity through Core/IAM.
2. Evaluate system permission separately from organizational authority.
3. Evaluate authority/mandate/delegation/scope/validity.
4. Record Approval Decision and supporting evidence.
5. SuperAdmin capability does not automatically provide financial approval authority.
6. FIN-DEC-33 must be resolved before approval authority mapping is final.

### 11.5 Process E — Ceiling and Cash Control

Evaluate distinct steps:

- Ceiling calculation.
- Ceiling reservation, if adopted.
- Ceiling consumption, according to FIN-DEC-07.
- Eligible-cash evaluation, according to FIN-DEC-08/09.
- Cash reservation, if adopted.
- Cash movement.
- Expenditure recognition.

No event is selected by this document as the final ceiling-consuming event.

### 11.6 Process F — Disbursement and Expenditure

1. Disbursement follows applicable approval.
2. Cash Movement Event records cash movement according to the Finance source model.
3. Ceiling impact follows the approved ceiling event semantics.
4. Expenditure Recognition follows the approved accounting policy; it is not automatically identical to disbursement.
5. Supporting evidence remains linked.
6. Failure, refund, reversal, or correction creates traceable events; original history is preserved.

### 11.7 Process G — Reconciliation

1. Gather applicable cash, ceiling, disbursement, expenditure, obligation, and document records.
2. Compare source values and evidence.
3. Record match, partial match, discrepancy, unresolved item, and resolution.
4. Corrections link to original events.
5. Reconciliation does not overwrite cash/ceiling/expenditure source records.
6. Closure evidence is generated/accepted only according to approved closure process.

### 11.8 Process H — Program and Financial Closure

- Program Closure Authority relates to Program Closure Evidence.
- Financial Closure Authority relates to Financial Closure Evidence.
- The same actor may perform both only if organizational authority permits.
- Both gates must be satisfied before policy amendment becomes eligible under GOV-04.
- Source vocabulary and closure evidence remain pending FIN-DEC-16–18.

---

## 12. Ledger and Event Transition Architecture

### 12.1 Separate ledger responsibilities

| Logical record set | Records | Must not be conflated with |
|---|---|---|
| Cash Ledger | Cash Movement Events and cash-position evidence according to Finance source model | Ceiling consumption or expenditure recognition |
| Ceiling Consumption Ledger | Ceiling reservation/consumption/release/reversal events under policy semantics | Cash movement or expense recognition |
| Expenditure Ledger | Expenditure Recognition events under approved accounting policy | Cash release, invoice, or budget |
| Reconciliation records | Comparisons, discrepancies, resolution references | Source ledger replacement |

“Ledger” here is a logical record set; it does not assert a formal accounting-ledger implementation.

### 12.2 Candidate event distinctions

| Event concept | Meaning | Policy dependency |
|---|---|---|
| Cash Reservation/Encumbrance | Reserves cash if Finance policy adopts it | FIN-DEC-09/32 |
| Ceiling Reservation | Reserves ceiling capacity if policy adopts it | FIN-DEC-07 |
| Ceiling Consumption | Counts against ceiling according to selected event semantics | FIN-DEC-07 |
| Ceiling Release | Releases a prior reservation/consumption according to policy | FIN-DEC-31/32 |
| Cash Movement | Records actual/recognized movement according to source model | FIN-DEC-08/09 |
| Disbursement | Records funds released/paid | FIN-DEC-08/12/33 |
| Expenditure Recognition | Recognizes expense for reporting according to Finance policy | FIN-DEC-12 |
| Expenditure Correction | Linked correction/reversal without overwriting source history | FIN-DEC-12/31 |
| Reconciliation Resolution | Records discrepancy handling and source links | FIN-DEC-16/31 |

### 12.3 Event transition safeguards

- Reservation is not automatically final expenditure.
- Reservation converted to consumption/disbursement must not double count.
- Failed, pending, and unknown payment outcomes must not be merged into one state.
- Timeout alone is not proof of failure or success.
- Reversal references the original event.
- Correction preserves the original and links to the correction.
- Event semantics are not finalized until FIN-DEC-07/08/09/12/31/32 are decided.

---

## 13. Authority, Security and Auditability

### 13.1 Logical separation

1. User Identity/Account.
2. Role Assignment.
3. System Permission.
4. SuperAdmin Capability.
5. Financial Approval Authority.
6. Mandate/Delegation/Acting Authority.
7. Approval Decision.
8. Program Closure Authority.
9. Financial Closure Authority.

These are separate concepts. No role, permission, assignment, or SuperAdmin capability automatically creates organizational authority.

### 13.2 FIN-DEC-33

SOP page 23 visible wording indicates that emergency-fund expenditure requires approval by Ketua TSKKM. The evidence confirms the visible wording only.

Still unavailable:

- Identity of the authority holder for a specific operation.
- Mandate/delegation.
- Scope/limits.
- Validity period.
- Acting authority.
- Mapping to SIM-TDB user/account.

Evidence Status: `SOP_CONFIRMED` (partial).  
Decision Status: `PENDING_ORG_DECISION`.

### 13.3 Audit concepts

Critical events should be traceable to actor, action, time, target, result, relevant Policy Version, source transaction, authority evidence where applicable, and correlation/causation references. Physical immutability guarantees are not claimed.

---

## 14. Master and Reference Data Catalogue

| Reference concept | Owner/source candidate | Finance use | Change control/status |
|---|---|---|---|
| Fund Source Category | Finance/organization | Classify funding origins | Values require approved source; FIN-DEC-10/11 |
| Fund Pool Classification | Finance | Cash-control grouping | Pool definition pending FIN-DEC-08/10 |
| Funding Source Allocation Type | Finance | Describe source/pool relationship | Pending FIN-DEC-10 |
| Funding Assignment Type | Finance | Assign funding to target context | Pending FIN-DEC-10/14 |
| Transaction/Event Type | Finance | Classify request, movement, disbursement, recognition, correction | Vocabulary pending FIN-DEC-07/12/31 |
| Approval Decision Type | Finance/governance | Record approval actions | Must not invent authority; FIN-DEC-33 |
| Financial Obligation Type | Finance/process owners | Identify obligation/blocker | FIN-DEC-16 |
| Expenditure Category | Finance | Reporting/restriction mapping | Only source-backed categories; FIN-DEC-11/12 |
| Document Type | Document Management | SK and financial evidence references | Document owner remains Document Management |
| Policy Status | Core/policy governance | Candidate policy lifecycle | Exact values pending FIN-DEC-23/24 |
| Program/Activity References | Program module | Finance context | External canonical records |
| Incident/Response Operation References | Owning modules | Control unit/context candidates | FIN-DEC-04/27 |
| Currency Reference | Core/Finance policy | Amount interpretation | FIN-DEC-26 |
| Reconciliation Status | Finance | Candidate reconciliation process state | FIN-DEC-16/18/31 |
| Authority/Mandate Reference | Organization/Core document service | Authority evidence | FIN-DEC-19/20/22/33 |

Finance must consume canonical reference data from the owning module where applicable and must not silently duplicate it.

---

## 15. Cross-Module Integration Contracts

| Source module | Consumer | Data exchanged | Trigger | Source of truth | Failure handling/dependency |
|---|---|---|---|---|---|
| Core/IAM | Finance/Policy Governance | Actor/account, role/permission, SuperAdmin capability reference | Authenticated action | IAM/Core | Permission is not authority; FIN-DEC-20 |
| Program Management | Finance/Policy Freeze | Program, Activity, state, closure evidence references | Program activation/state/closure | Program module | Unavailable/stale state cannot prove closure; FIN-DEC-17/29 |
| Incident Management | Finance/Policy Scope | Incident identity/status | Fund request/control-unit assignment | Incident module | No duplicate master; FIN-DEC-04/27 |
| Response Operations | Finance/Policy Scope | Operation identity/state/closure reference | Request/control unit | Operations module | Cardinality pending FIN-DEC-04/27 |
| Program Management | Finance Budget | Program/activity references | Budget/request lifecycle | Program owns Program/Activity | FIN-DEC-14 |
| Procurement | Finance | Request/PO/invoice/commitment references | Procurement events | Procurement module | Finance does not duplicate PO/invoice master; commitment treatment pending |
| Logistics/Inventory | Finance | Goods receipt/stock evidence references | Receipt/reconciliation | Logistics/Inventory module | Receipt is not automatically payment/expenditure |
| Document Management | Finance | SK and financial document references/versions | Upload/verification/transaction | Document service | Missing or unreadable source remains unresolved |
| Finance | Reporting/Audit | Derived cash/ceiling/disbursement/expenditure/reconciliation data | Reporting | Canonical financial records per domain | Reports are derived and preserve discrepancy |
| Audit/Reporting | Finance/Core | Audit references | Audit/review/closure | Audit source | No overwrite of source transactions |

### Contract fields to be settled later

- Source owner and consumer.
- Canonical identifier.
- Business meaning.
- Source version/effective timestamp.
- Freshness.
- Cancellation/correction behavior.
- Idempotency/retry rule.
- Failure handling.
- Reconciliation responsibility.

These are logical contract topics, not API schemas.

---

## 16. SOP and Decision Traceability

### 16.1 Available SOP-to-system mapping

| SOP page | Visible activity/evidence | Candidate system area | Finance relationship | Evidence status/limitation |
|---|---|---|---|---|
| 16–17 | Criteria and disaster scale/response level | Incident/Response/Program | Policy applicability context | `SOP_CONFIRMED` partial; some table values need clearer source. |
| 18 | Six service sectors | Program/Activity | Budget/activity context if approved | `SOP_CONFIRMED` from visible page; budget relationship pending FIN-DEC-14. |
| 19 | Coordination and command relationships | Core/Response/Stakeholder | Authority/evidence context only | `SOP_CONFIRMED` partial; authority mapping pending. |
| 20 | TSKKM functions | Organization/Assignment | Function does not itself confer Finance authority | `SOP_CONFIRMED` visible; mapping pending. |
| 21 | Master disaster-response workflow | Workflow/Incident/Response | Finance activity follows applicable response process | `SOP_CONFIRMED` visible; no Finance sequence invented. |
| 22 | Rapid Assessment, SITREP #1, decision branches, coordination/funding context | Incident/Assessment/Decision/Response | Request may reference incident/response context | `SOP_CONFIRMED` visible; time anchor/authority details require review. |
| 23 | Funding sources, approval by Ketua TSKKM, Rp50m wording | Finance/Fund Source/Approval | Fund Request/authority/disbursement evidence candidates | `SOP_CONFIRMED` partial; Rp50m interpretation remains `SOURCE_CONFLICT`; mandate unavailable. |
| 24 | APP Nasional access with SITREP/budget plan; restricted-use categories | Finance/Document/Program | Funding source and restriction references | `SOP_CONFIRMED` partial; full context and enforcement pending. |
| 25–26 | Protection, safety/security, monitoring/evaluation | Protection/Monitoring/Response | Finance may reference evidence, not own these records | `SOP_CONFIRMED` visible; forms/ownership outside available pages. |
| 27 | Report components and reporting time described | Reporting/Finance/Logistics | Financial reporting uses Finance source records | `SOP_CONFIRMED` visible; program completion trigger/authority mapping pending. |
| 28–29 | SOP close and Code of Conduct beginning | Document Governance | Governing-source reference | `SOP_CONFIRMED` visible; does not establish Finance amendment authority. |
| 30–95 | Not available in this audit context | Relevant modules | Finance forms/process details may be present | `EVIDENCE_NOT_AVAILABLE` |

### 16.2 Process boundary

- Digitalization must preserve the SOP process; it must not create operational approval stages.
- Finance may validate completeness and trace evidence but must not replace authorized human decisions.
- Missing SOP pages/forms remain unavailable evidence; no procedure is reconstructed.

---

## 17. Data Integrity and Transaction Safety

### 17.1 Duplicate prevention

- Distinguish duplicate delivery, repeated user submission, duplicate business request, duplicate disbursement, and legitimate transactions with identical amount/date.
- Retryable operations need a logical idempotency identity and source event reference.
- Duplicate detection does not automatically authorize merging or deletion.
- Corrections preserve original IDs and histories.

### 17.2 Correlation, causation, source transaction

| Reference | Meaning |
|---|---|
| Source Transaction Reference | Canonical record from which an event derives or which it affects. |
| Correlation Reference | Groups events within a defined request/process context. |
| Causation Reference | Identifies the event that caused a later event, such as a reversal or correction. |
| Audit Reference | Actor/action/time/target/outcome/source/policy evidence. |

One reference must not silently substitute for another.

### 17.3 Double counting and ledger safety

- Cash movement is distinct from ceiling consumption.
- Ceiling reservation is distinct from final consumption unless approved semantics define otherwise.
- Reservation conversion to disbursement must not double count.
- Disbursement is distinct from expenditure recognition.
- Reconciliation does not replace source ledgers.
- Failed, pending, and unknown outcomes must remain distinguishable according to an approved process.

### 17.4 Concurrency and recovery

The logical integrity requirement is that concurrent requests must not use the same ceiling or cash capacity more than once. Atomic validation/serialization is a technical design option; no physical mechanism is chosen.

Timeout, retry, callback, source unavailability, and reconciliation mismatch require source-outcome checks before a new financial effect is created.

### 17.5 Correction, reversal, and disputed transactions

Corrections must:

- Preserve original records.
- Link to original events.
- Carry reason, actor, time, and evidence according to approved policy.
- Treat cash, ceiling, expenditure, and closure impacts separately.
- Avoid deleting historical events.

Final treatment remains subject to FIN-DEC-31/32.

---

## 18. Full Traceability Matrix

| Architecture element | R05.1 / GOV | FIN-DEC | FIN-TEST | SOP evidence | Status |
|---|---|---|---|---|---|
| Master Policy before program activation | GOV-01/02 | FIN-DEC-21 | 59/85 | SOP workflow pages 21–22; owner governance | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| Policy Freeze Scope | GOV-03/04 | FIN-DEC-16–18/29 | 47–60, 75–82, 89–97 | SOP workflow plus owner governance | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT`; mapping pending |
| SuperAdmin policy capability | GOV-05 | FIN-DEC-20/22 | 40/53/54/84/100 | Owner governance | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| SK Pengaturan amendment | GOV-06/07 | FIN-DEC-19/21/22 | 50–52/78/79/86/87/91 | Owner governance; actual SK unavailable | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| Policy version immutability | GOV-09 | FIN-DEC-23/24 | 55/57/74 | Owner governance | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| Rp50m emergency maximum | Owner clarification; SOP p.23 partial conflict | FIN-DEC-01/02/04 | 24–29/33/36/63/71/93 | SOP p.23 image | `CLARIFIED_BY_PROJECT_OWNER` + `SOURCE_CONFLICT` |
| Rp100m illustrative | Owner clarification | FIN-DEC-02 | 35/45 | Template p.49 unavailable | `CLARIFIED_BY_PROJECT_OWNER`; fixture only |
| Aggregation modes | Owner clarification | FIN-DEC-03–06 | 24–29/36–39/42/61–63/70/71/93–95 | Owner clarification | Mode options clarified; scope pending |
| Cash eligibility | Owner clarification | FIN-DEC-08/09/11 | 26/29/31/44/45/72/98 | Finance sources partial | Formula/source pending |
| Ketua TSKKM approval wording | SOP p.23 | FIN-DEC-33 | 12/100–105 | SOP p.23 visible | `SOP_CONFIRMED` partial; authority pending |
| APP Nasional restrictions | SOP p.24 partial | FIN-DEC-11 | 08/20/45/98 | SOP p.24 image | `SOP_CONFIRMED` partial; enforcement pending |
| Program Budget structure | Phase 0.1C/D, incomplete model | FIN-DEC-14/15 | 04–06/22/23 | SOP pages outside Finance evidence as available | Pending logical model |
| Funding Allocation | R05.1 logical correction | FIN-DEC-10/14 | 07/19/23/45 | Funding sources p.23–24 partial | Pending cardinality |
| Financial Obligation/Blocker | GOV-04 and Finance closure requirements | FIN-DEC-14/16/18/29 | 49/60/77/82/88/90/97 | Closure policy source incomplete | Candidate relations |
| Ledger separation | Finance integrity requirements | FIN-DEC-07/08/12/31/32 | 09–15/66–72/99 | Finance policy/source incomplete | Logical requirement; event policy pending |
| Reconciliation | Finance accountability architecture | FIN-DEC-12/16/18/31 | 10/15/54/60/66–69/82/99 | Full Finance forms unavailable | Candidate model |
| Authority model | SOP p.23 plus governance | FIN-DEC-19/20/22/33 | 12/50–57/78/79/84/100–105 | Authority documents unavailable | Pending authority evidence |

---

## 19. Risk and Gap Analysis

| Risk ID | Description/root cause | Impact | Affected concepts | Decision dependency | Proposed mitigation | Status |
|---|---|---|---|---|---|---|
| R-01 | Rp50m hardcoded or treated as global cap | Policy distorted and multiple incidents constrained incorrectly | Master Policy/Ceiling | FIN-DEC-02/03 | Configured Policy Version; separate aggregation modes | Pending active configuration |
| R-02 | Incident/operation control unit ambiguous | Ceiling misapplied or circumvented | Incident/Operation/Ceiling Ledger | FIN-DEC-04/27 | Keep control-unit links candidate | Pending |
| R-03 | Global scope/reset undefined | Incorrect aggregation or implicit reset | Policy Scope Membership | FIN-DEC-05/06/28 | Explicit membership/effective period | Pending |
| R-04 | Policy freeze conflated with ceiling scope | Policy lock and spending control diverge | Policy/Program/Incident | GOV-03/04; FIN-DEC-03–06 | Separate concepts and tests | Addressed conceptually |
| R-05 | Financial Obligation/Blocker conflated | Administrative blocker treated as monetary liability or vice versa | Obligation/Blocker | FIN-DEC-16 | Separate logical concepts | Correction included; rules pending |
| R-06 | Program and Financial Closure Authority conflated | Invalid closure authorization | Closure evidence | FIN-DEC-18 | Separate authority concepts | Pending |
| R-07 | Funding Allocation cardinality assumed | Misreported source allocation/restrictions | Fund Source/Pool/Allocation/Budget | FIN-DEC-10/14 | Separate source allocation and assignment concepts | Pending |
| R-08 | Cash movement equated with expenditure | Incorrect reports | Cash/Expenditure Ledgers | FIN-DEC-08/12 | Ledger separation | Pending source policy |
| R-09 | Disbursement forced 1:1 with ledgers/reconciliation | Orphan/duplicate associations | Disbursement and ledgers | FIN-DEC-07/08/12 | Candidate relationships only | Pending |
| R-10 | Reservation/disbursement double count | Ceiling/cash overstated | Reservation/Disbursement | FIN-DEC-07/09/32 | Define conversion/release events | Pending |
| R-11 | Approval authority inferred from access | Unauthorized financial approval | IAM/Authority/Approval | FIN-DEC-19/22/33 | Separate capability and authority evidence | Pending |
| R-12 | SOP page 23 silently reinterpreted | Digital system changes organization policy | Policy/SOP | FIN-DEC-01 | Preserve wording and source conflict | Pending formal reconciliation |
| R-13 | APP Nasional restriction expanded | Unapproved financial restriction | Fund Source/Expense categories | FIN-DEC-11 | Use only verified categories | Partial source |
| R-14 | Policy/transaction history overwritten | Loss of accountability | Version/ledgers | GOV-09 | Versioned corrections | Governance requirement |
| R-15 | Offline retry creates duplicate effect | Double disbursement/consumption | Requests/Events | FIN-DEC-25/29/32 | Idempotency and reconciliation | Technical design |
| R-16 | Concurrent requests overspend ceiling/cash | Financial overcommit | Scope/Cash/Events | FIN-DEC-07/08/09 | Atomic validation requirement | Physical approach pending |
| R-17 | Missing/stale source interpreted as no blocker | Premature policy unlock | Lock evaluation | FIN-DEC-29 | Treat unavailable source as unresolved per approved rule | Pending |
| R-18 | Test design reported as execution | False assurance | QA/audit | Test evidence | Separate statuses | No test executed |
| R-19 | Financial Document constrained 1:1 | Evidence duplication/loss | Documents and transactions | Document policy | Candidate multi-record references | Pending |
| R-20 | SK fixture or example mistaken as actual authority document | False governance evidence | Policy Amendment | FIN-DEC-19/21/22 | Label illustrative fixtures and require actual evidence for activation | Pending evidence |

---

## 20. Outstanding Decision Register

Keputusan kritis tetap:

- **FIN-DEC-01:** Rekonsiliasi SOP halaman 23 dengan klarifikasi pemilik proyek.
- **FIN-DEC-04–07:** Control unit, global scope, reset, dan ceiling-consuming event.
- **FIN-DEC-08–13:** Eligible cash, reservation/outstanding payments, fund source/pool, restrictions, expenditure recognition, remaining budget.
- **FIN-DEC-14–18:** Program/Activity/Budget relationships, financial obligations, program/financial closure evidence and authority.
- **FIN-DEC-19/20/22/33:** SK verification, SuperAdmin lifecycle, checker separation, financial approver authority.
- **FIN-DEC-23/24:** Policy version/effective-date transition.
- **FIN-DEC-25/26:** Offline behavior dan monetary representation.
- **FIN-DEC-27–30:** Program/Incident/Operation relationships, policy scope continuity, source freshness, lock report access.
- **FIN-DEC-31/32:** Refund/reversal/correction dan reservation release.

Tidak ada keputusan pending yang diselesaikan oleh R02.

---

## 21. Readiness Assessment

| Area | Status | Alasan |
|---|---|---|
| Entity Catalogue | `CONDITIONAL` | Ownership/classification lengkap secara logical; beberapa source contracts masih pending. |
| Entity Attribute Catalogue | `CONDITIONAL` | Atribut konseptual per entity tercatat; requiredness/validation mengikuti pending decisions. |
| Relationship Catalogue | `BLOCKED_BY_DESIGN_DECISION` | Cardinality dan source relationships masih menunggu FIN-DEC. |
| Policy Amendment/Freeze | `CONDITIONAL` | Governance high-level jelas; source/status mapping dan authority evidence pending. |
| Funding/Cash | `BLOCKED_BY_ORG_DECISION` | Eligible cash, pool, restriction, allocation belum diputuskan. |
| Budget/Commitment | `BLOCKED_BY_ORG_DECISION` | Budget lifecycle, commitment, advance, dan remaining-budget formula pending. |
| Ceiling/Ledger | `BLOCKED_BY_ORG_DECISION` | Ceiling-consuming event dan reservation treatment pending. |
| Authority/Security | `BLOCKED_BY_ORG_DECISION` | FIN-DEC-19/20/22/33 dan evidence mandate belum tersedia. |
| Reconciliation/Closure | `BLOCKED_BY_ORG_DECISION` | Blocker source, reconciliation lifecycle, dan closure authority belum final. |
| SOP Traceability | `CONDITIONAL` | Hanya halaman 16–29 tersedia untuk review. |
| Test design | `CONDITIONAL` | FIN-TEST-01–105 ditautkan; beberapa behavior menunggu decision. |
| Test execution | `BLOCKED_BY_MISSING_EVIDENCE` | Tidak ada test environment atau execution report. |
| Finance Logical Architecture Final | `BLOCKED` | Policy-critical decisions dan relationships belum selesai. |
| Physical Database Design | `NO_GO` | Logical architecture belum disetujui final. |
| Implementation | `NO_GO` | Tidak termasuk tahap ini. |

---

## 22. R01-to-R02 Correction Log

| CR ID | Temuan | Koreksi R02 | Status dokumen |
|---|---|---|---|
| CR-001 | Incomplete Entity Attribute Catalogue | Semua logical concepts yang dinamai di R01 diklasifikasikan dan diberi candidate attributes atau dijelaskan sebagai reference/derived/value object; physical fields tidak dibuat. | `READY FOR RE-AUDIT`; policy-dependent detail tetap pending |
| CR-002 | Incomplete Formal Relationship Coverage | Relationship catalogue dilengkapi REL-35–REL-58 dan REL-59–REL-73; candidate relations diberi Decision ID. | `READY FOR RE-AUDIT` |
| CR-003 | Non-Atomic Relationship Specification | Relationship catalogue memisahkan relasi yang berbeda dan menjelaskan tujuan setiap edge. | `READY FOR RE-AUDIT`; cardinality tetap pending |
| CR-004 | Funding Allocation Relationship Inconsistency | Funding Source Allocation dan Funding Assignment dipisahkan sebagai konsep; hubungan dan cardinality tetap bergantung FIN-DEC-10/14. | `READY FOR RE-AUDIT`; decision pending |
| CR-005 | Ceiling Consumption Ledger not explicit | Ceiling Consumption Ledger dimasukkan sebagai logical record set dan dibedakan dari Ceiling Consumption Event, Cash Ledger, dan Expenditure Ledger. | `READY FOR RE-AUDIT`; event semantics pending FIN-DEC-07 |
| CR-006 | Policy Freeze/Amendment Lifecycle incomplete | Policy Amendment dan Lock Evaluation dilengkapi secara logical; GOV-01–09 diterapkan tanpa menciptakan status final. | `READY FOR RE-AUDIT`; source/authority mapping pending |
| CR-007 | Obligation/Blocker ambiguity | Financial Obligation dan Financial Closure Blocker didefinisikan terpisah, dengan candidate relationships. | `READY FOR RE-AUDIT`; blocker rules pending |
| CR-008 | Reconciliation detail insufficient | Ditambahkan Reconciliation Item, Discrepancy, Resolution concepts tanpa overwrite source records. | `READY FOR RE-AUDIT`; statuses/ownership pending |
| CR-009 | Commitment/Advance representation gap | Ditambahkan candidate Budget Commitment, Procurement Commitment Reference, Advance, dan Settlement references; Procurement ownership dipertahankan. | `READY FOR RE-AUDIT`; accounting treatment pending |
| CR-010 | Authority/IAM relationships incomplete | User, role, permission, SuperAdmin, financial authority, mandate, evidence, approval decision dipisahkan dan dihubungkan secara logical. | `READY FOR RE-AUDIT`; authority evidence pending |
| CR-011 | Conceptual ERD not provided | Disediakan 7 Mermaid diagrams domain serta combined logical overview. | `READY FOR RE-AUDIT` |
| CR-012 | Traceability matrix incomplete | Ditambahkan requirement-to-entity/decision/test/SOP traceability matrix. | `READY FOR RE-AUDIT`; evidence missing tetap ditandai |
| CR-013 | Cross-module contracts incomplete | Ditambahkan module integration ownership/data/failure matrix dan logical contract topics. | `READY FOR RE-AUDIT`; detailed contracts pending |
| CR-014 | Ledger event semantics incomplete | Dibedakan reservation, consumption, release, cash movement, disbursement, recognition, reconciliation; transitions pending decisions. | `READY FOR RE-AUDIT`; event semantics pending |
| CR-015 | Source evidence incomplete | SOP mapping dibatasi pada halaman 16–29; missing source inventory dipertahankan. | `PENDING EVIDENCE` |
| CR-016 | Entity/relationship/test traceability too broad | Test traceability matrix dan entity/relationship decision dependencies ditambahkan; FIN-TEST-01–105 tetap utuh. | `READY FOR RE-AUDIT`; tests not executed |

### 22.1 Correction status note

`READY FOR RE-AUDIT` berarti dokumentasi correction telah dimasukkan ke R02 dan menunggu pemeriksaan independen. Status itu tidak berarti logical design telah disetujui atau keputusan organisasi telah ditutup.

---

## 23. Final Recommendation

1. Ajukan R02 untuk independent re-audit terhadap CR-001–CR-016.
2. Jangan menutup CR berdasarkan kelengkapan redaksi saja; acceptance criteria harus diverifikasi terhadap katalog, relationships, diagrams, traceability, dan test coverage.
3. Selesaikan FIN-DEC-01, FIN-DEC-07–18, FIN-DEC-19/20/22/33, FIN-DEC-23–29, dan FIN-DEC-31/32 sesuai prioritas dan authority.
4. Kumpulkan SOP Finance, SK/mandate, closure evidence, dan source-system status mapping yang belum tersedia.
5. Pertahankan R02 sebagai logical model candidate sampai keputusan/evidence kritis disahkan.
6. Jangan lanjut ke physical database design sampai Finance Logical Architecture Final disetujui.
7. Jangan memulai implementation atau mengubah database pada tahap ini.

**Prinsip akhir:** SIM-TDB harus mengikuti aturan organisasi. R02 mendokumentasikan struktur logical yang dapat direview dan dependencies yang belum diselesaikan; R02 tidak menciptakan kebijakan, authority, cardinality, atau accounting treatment baru.

**Status dokumen:** Draft Logical Architecture untuk audit ulang.  
**Finance Logical Architecture Final:** `BLOCKED`.  
**Physical Database Design:** `NO_GO`.  
**Implementation:** `NO_GO`.