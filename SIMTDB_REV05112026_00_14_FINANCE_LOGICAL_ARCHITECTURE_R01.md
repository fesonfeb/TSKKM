# SIM-TDB — FINANCE LOGICAL ARCHITECTURE
## Enterprise Logical Architecture, Entity Catalogue, Relationship Specification & Financial Integrity Design

**Document ID:** SIMTDB-REV05112026-00-14-FIN-LA-R01  
**Filename:** `SIMTDB_REV05112026_00_14_FINANCE_LOGICAL_ARCHITECTURE_R01.md`  
**Revision:** REV05112026-R01  
**Status:** Draft logical architecture untuk review  
**Mode:** Logical architecture only — no physical implementation  
**Project:** Sistem Informasi Manajemen Tanggap Darurat Bencana (SIM-TDB)  
**Organization:** Caritas Keuskupan Malang — Tim Solidaritas Kemanusiaan Keuskupan Malang (TSKKM)

---

## 1. Executive Summary

Dokumen ini menyusun rancangan **Finance Logical Architecture** berdasarkan Finance Decision Register R05.1 dan materi sumber yang tersedia.

Arsitektur dirancang untuk memisahkan secara jelas:

- Master Policy dan policy versions.
- Policy Freeze Scope dan Ceiling Aggregation Scope.
- Program Budget dan emergency-fund ceiling.
- Fund Source, Funding Allocation, Fund Pool, dan Cash Account.
- Fund Request, Approval Decision, dan authority evidence.
- Ceiling Consumption Event dan Cash Movement Event.
- Disbursement dan Expenditure Recognition.
- Financial Obligation, Financial Reconciliation, Program Closure, dan Financial Closure.
- Dokumen pendukung, audit, correlation, causation, dan source transaction references.

### Kesimpulan

R01 menyediakan **logical architecture candidate** untuk review, tetapi belum menjadi arsitektur final yang disetujui. Hal-hal penting yang masih bergantung pada keputusan adalah:

- Rekonsiliasi wording SOP halaman 23 dengan klarifikasi pemilik proyek.
- Initial policy amount/mode/scope.
- Control unit untuk `PER_INCIDENT`.
- Scope `GLOBAL_ALL_INCIDENTS`.
- Event yang mengonsumsi ceiling.
- Eligible available cash dan canonical cash source.
- Financial approval authority, termasuk FIN-DEC-33.
- Actual expenditure recognition.
- Program dan financial closure evidence.
- Cardinality Program–Activity–Budget–Incident–Response Operation.

Tidak dibuat physical schema, SQL, foreign key, index, migration, seed, API, atau code.

---

## 2. Document Control and Revision History

| Versi | Deskripsi |
|---|---|
| Finance 00.10 | Finance foundation re-audit; mengidentifikasi policy modes, cash control, ledger separation, dan Finance decisions. |
| Finance 00.11 R01 | Governance dan transaction-control requirements yang menjadi bagian baseline pemilik proyek. |
| Finance 00.12 | Audit prompt dan provenance correction. |
| Finance 00.13 R01–R05.1 | Decision-register harmonization, test preservation, dan logical relationship correction. |
| **Finance Logical Architecture R01** | **Rancangan logical architecture untuk review; belum final dan belum approved.** |

Dokumen ini tidak mengubah dan tidak menggantikan R05.1. R05.1 tetap menjadi register keputusan dan dependency utama.

---

## 3. Architecture Objectives and Scope

### 3.1 Tujuan arsitektur

Finance Logical Architecture harus:

- Mengikuti SOP dan governance pemilik proyek.
- Mencegah sumber data keuangan ganda.
- Menjaga traceability setiap keputusan, permintaan, transaksi, dokumen, dan koreksi.
- Mencegah transaksi ganda akibat retry atau synchronization.
- Mencegah double counting antara reservation, disbursement, cash movement, dan expenditure.
- Memisahkan permission sistem dari kewenangan organisasi.
- Mendukung integrasi dengan Program, Incident, Response Operation, Procurement, Logistics/Inventory, Document Management, dan Audit.
- Menyediakan hubungan logical yang dapat direview tanpa mengunci physical database design.

### 3.2 Cakupan

Termasuk:

- Master Policy, Policy Version, Policy Scope, dan policy freeze.
- Finance request dan approval.
- Emergency-fund ceiling control.
- Funding source, funding allocation, fund pool, cash, dan ledger concepts.
- Disbursement, expense recognition, reconciliation, refund/reversal, dan obligations.
- Authority, SuperAdmin capability, evidence documents, audit, idempotency, correlation, dan integration contracts.
- Test and traceability architecture.

Tidak termasuk:

- Physical database schema.
- Data types, tables, columns, SQL, constraints, indexes, triggers, migrations, dan seeds.
- API endpoint definitions.
- Application code, UI, deployment, atau production configuration.
- Keputusan final atas policy dan authority yang masih pending.

---

## 4. Source Authority and Evidence Classification

### 4.1 Sumber yang diperiksa

| Sumber | Status | Batas |
|---|---|---|
| Finance Decision Register R05.1 | Tersedia dalam konteks percakapan dan digunakan sebagai baseline | Working document, bukan Finance policy final. |
| Klarifikasi owner tentang Rp50m, Rp100m, dan aggregation modes | Tersedia dalam percakapan | Menetapkan design requirements; bukan bukti SK atau mandate formal. |
| Gambar SOP halaman cetak 16–29 | Tersedia dan ditelaah | Halaman 23–24 relevan; audit SOP tetap parsial. |
| SOP halaman 1–15 dan 30–95 | `EVIDENCE_NOT_AVAILABLE` | Tidak dinyatakan telah diperiksa. |
| SOP Finance halaman 40–41, halaman 49, dan halaman 62–69 | `EVIDENCE_NOT_AVAILABLE` | Template dan detail prosedur belum diverifikasi. |
| SK, mandate/delegation, approval matrix, dan closure evidence | `EVIDENCE_NOT_AVAILABLE` | Tidak tersedia untuk verifikasi formal. |
| Repository, code, database, schema, migration, dan test suite | `EVIDENCE_NOT_AVAILABLE` | Tidak diperiksa atau diubah. |

### 4.2 Status provenance

| Label | Makna |
|---|---|
| `SOP_CONFIRMED` | Didukung langsung oleh bagian SOP yang tersedia dan terbaca. |
| `CLARIFIED_BY_PROJECT_OWNER` | Klarifikasi pemilik proyek yang dapat ditelusuri. |
| `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` | Governance requirement sistem yang ditetapkan pemilik proyek. |
| `ORG_DECISION_CONFIRMED` | Keputusan organisasi formal dengan bukti tersedia dan terverifikasi. |
| `SOURCE_CONFLICT` | Sumber atau interpretasi belum selaras. |
| `EVIDENCE_NOT_AVAILABLE` | Bukti tidak tersedia. |
| `PENDING_ORG_DECISION` | Memerlukan keputusan organisasi, authority, atau policy Finance. |
| `PENDING_DESIGN_DECISION` | Memerlukan keputusan logical/domain design. |
| `TECHNICAL_RECOMMENDATION` | Rekomendasi teknis, bukan ketentuan organisasi. |

`PROJECT_OWNER_GOVERNANCE_REQUIREMENT` tidak membuktikan bahwa SK, signatory, mandate, delegation, atau closure authority tertentu telah diterbitkan dan diverifikasi.

---

## 5. Governance Requirements

### 5.1 GOV-01 sampai GOV-09

Seluruh governance requirement berikut dipertahankan tanpa perubahan substansi atau status:

| ID | Requirement | Status |
|---|---|---|
| GOV-01 | Master Policy ditetapkan sebelum program operasional dimulai. | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| GOV-02 | Tidak ada program operasional yang aktif tanpa policy yang berlaku. | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| GOV-03 | Policy setup/amendment terkunci saat ada program yang berjalan atau belum resmi ditutup. | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| GOV-04 | Policy amendment juga terkunci sampai program dan seluruh keuangan terkait selesai. | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| GOV-05 | Hanya kapabilitas SuperAdmin yang dapat melakukan setup awal dan amendment yang memenuhi syarat. | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| GOV-06 | Setiap amendment memerlukan SK Pengaturan terlampir dengan detail yang dapat ditelusuri. | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| GOV-07 | SK Pengaturan tidak membypass program/financial closure gate. | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| GOV-08 | Tidak ada SuperAdmin override saat policy terkunci. | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| GOV-09 | Amendment menghasilkan policy version baru; histori tidak ditimpa diam-diam. | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |

### 5.2 Batas penerapan

Governance di atas tidak menetapkan otomatis:

- Vocabulary status program.
- Bukti formal closure.
- Financial closure authority.
- Identitas/mandate Ketua TSKKM.
- Approval authority untuk pengeluaran dana darurat.
- Policy amount/mode awal.
- Control unit atau global scope.
- Cash eligibility formula.
- Event yang mengonsumsi ceiling.

Semua detail tersebut dirujuk ke Decision Register.

---

## 6. Finance Domain Overview

### 6.1 Domain boundaries

| Domain | Fakta utama yang dikelola | Boundary |
|---|---|---|
| Master Policy | Amount, aggregation mode, policy scope, effective version | Bukan transaksi, budget, atau cash balance. |
| Program Budget | Anggaran program/activity sesuai Finance policy | Bukan emergency ceiling atau cash tersedia. |
| Funding | Sumber dana, alokasi, pool, restriction | Tidak otomatis membuktikan kas tersedia. |
| Cash | Cash account/evidence/movement/balance basis | Bukan ceiling consumption atau expenditure recognition. |
| Fund Request and Approval | Permintaan, review, decision, authority evidence | Permission tidak sama dengan authority. |
| Ceiling Control | Event yang dihitung terhadap policy ceiling | Event semantics masih pending. |
| Disbursement | Dana yang dikeluarkan/dibayarkan | Tidak otomatis sama dengan recognized expenditure. |
| Expenditure Recognition | Pengeluaran yang diakui untuk reporting | Mengikuti Finance policy yang disahkan. |
| Reconciliation and Closure | Mencocokkan record, evidence, obligations, dan closure | Tidak menimpa source records. |
| Document and Audit | Evidence, versions, actor, event, correlation, causation | Tidak menjadi source transaksi pengganti. |

### 6.2 Nominal dan aggregation mode

- **Rp50.000.000:** batas maksimum pengeluaran dana darurat untuk satu kejadian/operasi respons berdasarkan klarifikasi pemilik proyek. Nilai ini bukan wajib dibelanjakan dan bukan konstanta permanen. `CLARIFIED_BY_PROJECT_OWNER`.
- **Rp100.000.000:** nilai ilustratif; bukan default, ceiling, global cap, maximum, atau approval threshold. `CLARIFIED_BY_PROJECT_OWNER`.
- Amount dan mode ditempatkan pada Master Policy configuration; nilai awal yang aktif belum disetujui.
- `PER_INCIDENT`: aggregation per control unit yang ditetapkan.
- `GLOBAL_ALL_INCIDENTS`: satu ceiling bersama dalam policy scope yang ditetapkan.
- Control unit dan global scope tetap pending FIN-DEC-04/05/06.

---

## 7. Financial Policy Architecture

### 7.1 Policy Freeze Scope

Policy Freeze Scope menjawab:

> Kapan policy setup/amendment tidak boleh dilakukan?

Freeze scope mengikuti GOV-03/GOV-04:

- Program sedang berjalan atau belum formal closed: amendment terkunci.
- Program closed tetapi keuangan terkait belum selesai: amendment tetap terkunci.
- SK Pengaturan tidak membypass lock.
- Tidak ada SuperAdmin override.

Status: `PROJECT_OWNER_GOVERNANCE_REQUIREMENT`.

### 7.2 Ceiling Aggregation Scope

Ceiling Aggregation Scope menjawab:

> Incident, operation, atau transaksi mana yang berbagi configured ceiling?

Mode:

- `PER_INCIDENT`: per control unit yang ditetapkan.
- `GLOBAL_ALL_INCIDENTS`: satu ceiling kumulatif dalam scope policy.

Control unit, global scope, membership, dan reset/supersession: `PENDING_ORG_DECISION` atau `PENDING_DESIGN_DECISION`.

### 7.3 Scope yang harus tetap terpisah

| Scope | Fungsi | Status |
|---|---|---|
| Policy Freeze Scope | Mengunci amendment selama program/financial closure gate belum lulus. | Governance requirement |
| Ceiling Aggregation Scope | Mengagregasi penggunaan ceiling. | Mode tersedia; detail pending |
| Fund Pool Eligibility Scope | Menentukan fund/cash yang eligible. | Finance policy pending |
| Financial Reporting Scope | Menentukan transaksi yang diakui untuk laporan. | Finance policy pending |

Jangan menggunakan salah satu scope sebagai pengganti scope lainnya.

---

## 8. Logical Entity Catalogue

Nama berikut adalah **logical/conceptual entities**, bukan table names atau physical schema.

### 8.1 Policy and Governance Domain

| Entity | Tujuan dan tanggung jawab | Lifecycle konseptual | Hubungan utama | Status/evidence |
|---|---|---|---|---|
| Master Policy | Identitas policy Finance yang mengatur emergency-fund ceiling dan parameter kritis yang disahkan. | Initial setup → active versions → amendment/supersession → retired bila disahkan. | Memiliki Policy Versions dan berhubungan dengan Freeze/Aggregation Scopes. | Governance principles `PROJECT_OWNER_GOVERNANCE_REQUIREMENT`; policy detail pending. |
| Policy Version | Menyimpan versi amount, mode, scope, effective references, dan governing evidence. | Draft/candidate → validated/active → superseded; status names candidate. | Terhubung ke Master Policy dan dapat direferensikan oleh program/request sesuai aturan binding. | Version history mandatory; activation detail pending. |
| Policy Freeze Scope | Merepresentasikan governance gate yang menentukan kelayakan setup/amendment. | Locked → eligible for controlled amendment; candidate state. | Membaca program state/evidence dan financial blockers/evidence. | High-level gate owner-approved; source/status mapping pending. |
| Ceiling Aggregation Scope | Menentukan unit atau policy scope yang dihitung bersama terhadap ceiling. | Configured as part of approved policy version. | Terkait ke Policy Version dan scope-membership records. | Mode approved as selectable options; scope pending. |
| Policy Scope Membership | Menghubungkan Program, Incident, atau Response Operation dengan scope policy jika aturan menetapkan. | Pending/active/ended membership; labels candidate. | Menautkan scope ke record sumber tanpa menyimpan copy policy. | Candidate concept; membership/cardinality pending FIN-DEC-05/27/28. |
| Policy Amendment | Mencatat usulan dan aktivasi versi baru dengan SK Pengaturan yang diwajibkan. | Draft/evidence/eligible/activated states; exact lifecycle pending. | Referensi old/new versions, SK, lock evaluation, actor. | GOV-06/GOV-09; workflow detail pending. |
| Policy Lock Evaluation | Evaluasi derived terhadap program dan financial blockers untuk menjelaskan locked/eligible state. | Evaluation event/history. | Membaca canonical records dari Program dan Finance. | Technical concept; fail behavior pending FIN-DEC-29. |

### 8.2 Program and Response Domain

| Entity | Tujuan dan tanggung jawab | Lifecycle konseptual | Hubungan utama | Status/evidence |
|---|---|---|---|---|
| Program | Wadah program operasional dan konteks kegiatan. | Lifecycle milik Program module. | Dapat terkait ke Activity, Budget, Incident/Operation dan Policy Version, tetapi cardinality belum final. | Owner module Program; status model pending FIN-DEC-17/27/28. |
| Program State | Menyediakan status proses Program untuk lock evaluation. | Source status; vocabulary belum dimapping. | Dimiliki Program module dan dibaca Policy Freeze evaluation. | Source vocabulary `EVIDENCE_NOT_AVAILABLE`; mapping pending FIN-DEC-17. |
| Program Closure Evidence | Evidence bahwa Program telah ditutup sesuai governance/proses yang disahkan. | Submitted/verified/rejected candidate lifecycle. | Program dan Program Closure Authority. | Evidence/authority pending FIN-DEC-18. |
| Program Closure Authority | Authority yang mengesahkan program closure. | Mandate/effective-period candidate. | Terkait dengan closure decision dan evidence. | Tidak ada jabatan/nama ditetapkan; pending FIN-DEC-18. |
| Activity | Aktivitas dalam program, bila model Program menetapkan hubungan tersebut. | Lifecycle domain Program. | Dapat dikaitkan ke Program Budget, Budget Line, Obligation, dan Evidence. | Candidate; FIN-DEC-14 pending. |
| Program Budget | Catatan anggaran program/activity sesuai Finance policy. | Proposed/approved/revised/closed concepts; status belum disahkan. | Dapat terkait Program, Activity, Budget Line dan Funding Allocation. | Budget structure pending FIN-DEC-14/15. |
| Budget Line | Rincian budget menurut kategori/aktivitas bila disetujui. | Lifecycle mengikuti budget policy. | Parent budget/activity/category; cardinality pending. | Candidate; FIN-DEC-14 pending. |
| Incident | Identitas kejadian bencana. | Lifecycle milik Incident module. | Berbeda dari Program dan Response Operation; dapat menjadi control-unit candidate. | Entity boundary baseline; cardinality pending FIN-DEC-27. |
| Response Operation | Catatan operasi respons terhadap satu/lebih konteks sesuai model organisasi. | Lifecycle milik Response Operations. | Dapat terkait Incident, Program, Fund Request; cardinality pending. | Tidak diasumsikan sama dengan Program atau Incident. |

### 8.3 Funding and Cash Domain

| Entity | Tujuan dan tanggung jawab | Lifecycle konseptual | Hubungan utama | Status/evidence |
|---|---|---|---|---|
| Fund Source | Identitas asal dana dan restriction yang berlaku. | Active/inactive/history sesuai governance master. | Dapat dirujuk oleh Funding Allocation dan Fund Pool, sesuai cardinality yang disetujui. | Sumber tertentu disebut SOP p.23–24; complete catalogue pending. |
| Funding Allocation | Konsep logical untuk menyatakan bagaimana nominal/request/budget/expense dialokasikan ke source/pool jika model mengizinkan. | Draft/approved/effective candidate states; status belum final. | Candidate links ke Fund Request, Program Budget, Activity, Fund Source, Fund Pool. | Cardinality pending FIN-DEC-10/14. |
| Fund Pool | Unit grouping funds untuk cash control jika organisasi/Finance menyetujuinya. | Active/reconciled candidate lifecycle. | Dapat mengelompokkan sumber dan berhubungan dengan Cash Account. | Tidak semua sumber/kas otomatis digabung; FIN-DEC-08/10. |
| Cash Account | Rekening atau akun kas sebagai sumber bukti cash balance/movement. | Open/active/closed candidate states. | Terhubung ke Cash Movement Event dan Fund Pool bila disetujui. | SOP halaman 40–41 tidak tersedia; source details pending. |
| Cash Evidence | Evidence saldo/statement/rekonsiliasi cash. | As-of timestamp and verification lifecycle candidate. | Mendukung Cash Ledger/eligible-cash evaluation. | Canonical source pending FIN-DEC-08. |
| Cash Movement Event | Peristiwa receipt, payment, transfer, refund, atau movement sesuai Finance policy. | Event history; koreksi melalui linked event. | Cash Account, Disbursement, source transaction, reconciliation. | Event taxonomy/accounting rules pending. |
| Cash Ledger | Representasi pergerakan/posisi kas yang bersumber dari canonical Finance records. | Append/adjust through governed events; physical implementation not specified. | Cash Account, Cash Movement Event, source documents. | Logical source-of-truth belum ditetapkan FIN-DEC-08. |

### 8.4 Request and Approval Domain

| Entity | Tujuan dan tanggung jawab | Lifecycle konseptual | Hubungan utama | Status/evidence |
|---|---|---|---|---|
| Fund Request | Permintaan penggunaan dana dengan konteks kegiatan/kejadian dan sumber yang diusulkan. | Draft/submitted/review/approved/rejected/cancelled candidate states. | Program/Activity/Incident/Operation, Funding Allocation, Approval Decision, supporting documents. | State vocabulary/authority pending. |
| Actor/User Account Reference | Identitas actor yang melakukan aksi. | Lifecycle milik Core/IAM. | Audit, request, approval, amendment actions. | Tidak menggantikan authority. |
| Role/Permission Reference | Sistem authorization untuk action. | Lifecycle milik IAM/Core. | Dapat mengizinkan akses/aksi teknis. | Permission bukan authority organisasi. |
| SuperAdmin Capability | Kapabilitas teknis untuk setup/amendment policy sesuai governance. | Provision/revoke sesuai account governance. | Policy setup/amendment actions. | GOV-05; account process pending FIN-DEC-20. |
| Financial Approval Authority | Authority formal untuk menyetujui tindakan Finance. | Effective period/scope/delegation candidate. | Approval Decision dan Authority Evidence. | FIN-DEC-33 pending. |
| Authority Evidence | Bukti mandate/delegation/decision yang mendukung approval. | Valid/expired/revoked candidate; exact workflow pending. | Actor/authority/approval. | Source documents unavailable. |
| Mandate/Delegation | Cakupan dan masa berlaku authority yang didelegasikan. | Effective/expired/revoked candidate. | Principal, delegate, action/scope, evidence. | FIN-DEC-33 pending. |
| Approval Decision | Record keputusan terhadap Fund Request atau action Finance. | Decision history; no silent overwrite. | Actor, Authority Evidence, request, source document. | Approval authority belum final. |

### 8.5 Ceiling and Transaction Domain

| Entity | Tujuan dan tanggung jawab | Lifecycle konseptual | Hubungan utama | Status/evidence |
|---|---|---|---|---|
| Ceiling Consumption Event | Event yang menambah, menahan, melepas, atau mengoreksi nilai yang dihitung terhadap ceiling. | Event history; exact event taxonomy pending. | Policy Version/Scope, control unit, request/approval/disbursement source event. | FIN-DEC-07 pending. |
| Disbursement Event | Record pelepasan/pembayaran dana sesuai transaction process. | Initiated/confirmed/failed/returned candidate states; tidak final. | Request, authority/evidence, cash movement, possible ceiling event. | Payment/status semantics pending. |
| Expenditure Recognition | Record atau reference pengeluaran yang diakui untuk pelaporan sesuai Finance policy. | Recognition/reversal/correction process pending. | Source transaction, disbursement/document, expenditure ledger. | FIN-DEC-12 pending. |
| Expenditure Ledger | Logical record set untuk expenditure yang diakui. | Historical events preserved. | Expenditure Recognition, reconciliation, reports. | Canonical source pending FIN-DEC-12. |

### 8.6 Financial Obligation and Closure Domain

| Entity | Tujuan dan tanggung jawab | Lifecycle konseptual | Hubungan utama | Status/evidence |
|---|---|---|---|---|
| Financial Obligation/Blocker | Mewakili kewajiban atau unresolved finance item yang dapat memblokir policy amendment atau closure. | Open/cleared/disputed candidate states; source vocabulary pending. | Program; Activity/Budget bila relevan; Fund Request; Disbursement; Expenditure Recognition; Reconciliation; Closure Evidence. | FIN-DEC-16 pending. |
| Financial Reconciliation | Mencatat pencocokan record/ledger/documents dan discrepancy. | Open/reviewed/closed candidate states. | Cash, ceiling, disbursement, expenditure, documents, obligations. | Reconciliation policy pending. |
| Financial Closure Evidence | Bukti bahwa kewajiban dan reconciliation terkait telah diselesaikan. | Submitted/verified/accepted candidate lifecycle. | Program/obligation/reconciliation dan Financial Closure Authority. | FIN-DEC-16/18 pending. |
| Financial Closure Authority | Authority yang mengesahkan financial closure. | Mandate/scope/effective period candidate. | Financial Closure Evidence dan audit. | Tidak mengasumsikan sama dengan Program Closure Authority; FIN-DEC-18 pending. |

### 8.7 Document and Audit Domain

| Entity | Tujuan dan tanggung jawab | Hubungan | Status |
|---|---|---|---|
| Financial Document | Menyimpan reference/evidence dokumen untuk request, approval, disbursement, expenditure, reconciliation, SK, atau closure. | Dapat berhubungan dengan lebih dari satu record bila dokumen mendukung beberapa proses; tidak diasumsikan 1:1. | Document governance dan access rules pending. |
| Audit Reference | Menunjukkan actor/action/time/target/source/policy context. | Dapat menaut ke seluruh event kritis. | Append-only sebagai logical requirement; physical tamper-resistance belum dinilai. |
| Correlation Reference | Mengelompokkan langkah-langkah yang merupakan satu process/request chain. | Dapat dipakai di request, approval, reservation, disbursement, reconciliation. | Scope/uniqueness rules technical design. |
| Causation Reference | Menjelaskan event yang menyebabkan event berikutnya. | Reversal/correction merujuk source event yang menjadi sebab. | Logical traceability requirement. |
| Source Transaction Reference | Menunjuk record asal/otoritatif. | Mencegah reliance pada display text/free text. | Source-of-truth per domain masih pending. |

---

## 9. Entity Attribute Catalogue

Atribut berikut adalah candidate logical attributes, bukan field wajib yang telah disetujui. Tidak ada physical type, column, primary key, foreign key, index, atau constraint yang ditetapkan.

### 9.1 Policy and Governance

| Entity | Attribute | Business meaning | Requiredness | Source/validation | Status |
|---|---|---|---|---|---|
| Master Policy | Policy reference | Identitas konseptual policy | Candidate required | Stable reference; generation method later | `TECHNICAL_RECOMMENDATION` |
| Master Policy | Policy name/description | Nama policy untuk pembaca | Candidate | Tidak mengubah makna policy | `TECHNICAL_RECOMMENDATION` |
| Master Policy | Policy owner/governing authority reference | Menunjuk sumber governance | Required in concept; actual authority pending | Evidence harus dapat ditelusuri | `PENDING_ORG_DECISION` |
| Policy Version | Version reference/number | Mengidentifikasi revisi policy | Required in concept | Versi lama dipertahankan | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| Policy Version | Configured ceiling amount | Batas dana darurat aktif | Required if policy uses ceiling | Rp50m reference; active value requires approval | `CLARIFIED_BY_PROJECT_OWNER` |
| Policy Version | Aggregation mode | `PER_INCIDENT` atau `GLOBAL_ALL_INCIDENTS` | Required for active policy | Hanya satu mode aktif kecuali policy baru mengizinkan mode lain | `CLARIFIED_BY_PROJECT_OWNER` |
| Policy Version | Control-unit/scope reference | Dasar aggregation | Conditional | Definition pending FIN-DEC-04/05 | `PENDING_ORG_DECISION` |
| Policy Version | Effective date/period | Menentukan periode penerapan | Required in concept | Tidak boleh mengarang tanggal | `PENDING_ORG_DECISION` |
| Policy Version | Governing source/decision reference | Source policy | Required in concept | Referensi sumber yang tersedia/verifikasi | `PENDING_ORG_DECISION` |
| Policy Freeze Scope | Gate evaluation reference | Hasil evaluasi program/finance closures | Candidate | Dibangun dari canonical records | `TECHNICAL_RECOMMENDATION` |
| Policy Scope Membership | Member reference/type | Program/Incident/Operation yang masuk scope | Conditional | Membership rules pending | `PENDING_DESIGN_DECISION` |

### 9.2 Program and Response

| Entity | Attribute | Business meaning | Requiredness | Source/validation | Status |
|---|---|---|---|---|---|
| Program | Program reference | Identitas program dari modul pemilik | Required for linked Finance records | Finance tidak membuat duplicate Program master | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| Program | Program state reference | Status lifecycle program | Required for freeze evaluation | Vocabulary/source mapping pending FIN-DEC-17 | `PENDING_DESIGN_DECISION` |
| Program Closure Evidence | Closure evidence reference | Evidence formal closure | Conditional on closure | Evidence format and authority pending | `PENDING_ORG_DECISION` |
| Program Closure Authority | Authority reference | Pihak yang mengesahkan program closure | Conditional | Tidak menetapkan nama/jabatan tanpa bukti | `PENDING_ORG_DECISION` |
| Activity | Activity reference | Identitas activity dari Program module | Conditional | Tidak membuat duplicate activity master | `PENDING_DESIGN_DECISION` |
| Program Budget | Budget reference | Identitas budget | Candidate | Relationship to program/activity pending FIN-DEC-14 | `PENDING_DESIGN_DECISION` |
| Program Budget | Proposed/approved/revised amount reference | Nilai pada tahapan budget | Conditional | Lifecycle/policy pending FIN-DEC-15 | `PENDING_ORG_DECISION` |
| Budget Line | Budget line reference/category | Rincian anggaran bila model mengharuskan | Conditional | Category master/source pending | `PENDING_DESIGN_DECISION` |
| Incident | Incident reference | Identitas incident dari Incident module | Conditional | Bukan pengganti Program/Operation | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| Response Operation | Operation reference | Identitas operation dari Response module | Conditional | Cardinality incident-operation pending FIN-DEC-27 | `PENDING_DESIGN_DECISION` |

### 9.3 Funding and Cash

| Entity | Attribute | Business meaning | Requiredness | Source/validation | Status |
|---|---|---|---|---|---|
| Fund Source | Source reference/type | Sumber dana | Required where known | SOP/Finance master source; complete catalogue pending | `SOP_CONFIRMED` parsial |
| Fund Source | Restriction reference | Aturan penggunaan source | Conditional | Hanya dari approved source | `PENDING_ORG_DECISION` |
| Funding Allocation | Allocation reference/value | Pengalokasian nilai ke target/source/pool | Conditional | Cardinality and allocation level pending FIN-DEC-10/14 | `PENDING_DESIGN_DECISION` |
| Funding Allocation | Target reference | Request, budget, activity, atau expenditure yang dialokasikan | Conditional | Tidak memakai polymorphic implementation assumption | `PENDING_DESIGN_DECISION` |
| Fund Pool | Pool reference | Unit pengelompokan eligible funds | Conditional | Composition and owner pending FIN-DEC-10 | `PENDING_ORG_DECISION` |
| Cash Account | Account reference | Akun/rekening yang menjadi source cash evidence | Conditional | SOP/Finance account source pending | `EVIDENCE_NOT_AVAILABLE` |
| Cash Movement Event | Movement reference/type | Cash receipt, release, transfer, refund atau event lain | Conditional | Event vocabulary mengikuti Finance policy | `PENDING_ORG_DECISION` |
| Cash Movement Event | Source/cause reference | Transaksi penyebab movement | Required in concept for traceability | Source record sesuai Finance model | `TECHNICAL_RECOMMENDATION` |
| Cash Ledger | Cash position/event reference | Representasi cash records untuk reconciliation | Derived/recorded per Finance model | Canonical source pending FIN-DEC-08 | `PENDING_ORG_DECISION` |

### 9.4 Request, Approval, Ceiling, Disbursement

| Entity | Attribute | Business meaning | Requiredness | Source/validation | Status |
|---|---|---|---|---|---|
| Fund Request | Request reference | Identitas permintaan dana | Required in concept | Tidak menentukan numbering fisik | `TECHNICAL_RECOMMENDATION` |
| Fund Request | Requesting actor | Pengguna yang membuat request | Required for accountability | IAM identity reference | `TECHNICAL_RECOMMENDATION` |
| Fund Request | Program/Activity/Incident/Operation context | Context bisnis request | Conditional | Relationships pending FIN-DEC-14/27 | `PENDING_DESIGN_DECISION` |
| Fund Request | Requested amount/purpose/source | Isi permintaan | Conditional by process | Rule source and funding eligibility | `PENDING_ORG_DECISION` |
| Approval Decision | Decision reference/outcome/date | Keputusan terhadap request/action | Required where approval occurs | Approval workflow pending | `PENDING_ORG_DECISION` |
| Approval Decision | Actor reference | User yang mengambil keputusan | Required in concept | Tidak otomatis menentukan authority | `TECHNICAL_RECOMMENDATION` |
| Approval Decision | Authority/mandate evidence | Basis kewenangan | Required where relevant | FIN-DEC-33/19/22 | `PENDING_ORG_DECISION` |
| Ceiling Consumption Event | Event reference/type/amount | Event yang mempengaruhi ceiling | Conditional | Consuming event pending FIN-DEC-07 | `PENDING_ORG_DECISION` |
| Ceiling Consumption Event | Policy version/scope/control-unit reference | Rule yang digunakan | Required in concept for traceability | Scope/control unit pending | `TECHNICAL_RECOMMENDATION` |
| Disbursement Event | Disbursement reference/date/amount/status | Pelepasan dana | Required when disbursement occurs | Status and process pending | `PENDING_ORG_DECISION` |
| Disbursement Event | Request/approval/source/evidence references | Provenance and evidence | Required in concept | No forced 1:1 cardinality | `TECHNICAL_RECOMMENDATION` |
| Expenditure Recognition | Recognition reference/amount/basis | Expense yang diakui untuk reporting | Conditional per Finance policy | Canonical recognition criteria pending FIN-DEC-12 | `PENDING_ORG_DECISION` |
| Expenditure Ledger | Source recognition event reference | Record set of recognized expenditure | Derived from approved source | Canonical model pending | `PENDING_ORG_DECISION` |

### 9.5 Obligation, Closure, Document, Audit

| Entity | Attribute | Business meaning | Requiredness | Source/validation | Status |
|---|---|---|---|---|---|
| Financial Obligation/Blocker | Obligation reference/type/status | Kewajiban yang dapat memblokir closure | Conditional | Type/source status pending FIN-DEC-16 | `PENDING_ORG_DECISION` |
| Financial Obligation/Blocker | Program/Activity/Budget context | Konteks program/activity bila relevan | Conditional | Not every obligation has all contexts | `PENDING_DESIGN_DECISION` |
| Financial Obligation/Blocker | Source transaction reference | Record asal obligation | Required in concept when known | May reference request, disbursement, expense, payable, or other source | `TECHNICAL_RECOMMENDATION` |
| Financial Reconciliation | Reconciliation reference/status/outcome | Hasil pencocokan dan discrepancy | Conditional | Process/status vocabulary pending | `PENDING_ORG_DECISION` |
| Program Closure Evidence | Evidence reference/date/status | Bukti penutupan program | Required for closure gate if defined | FIN-DEC-17/18 | `PENDING_ORG_DECISION` |
| Financial Closure Evidence | Finance evidence/status | Bukti semua kewajiban selesai | Required for financial gate if defined | FIN-DEC-16/18 | `PENDING_ORG_DECISION` |
| Closure Authority | Actor/authority/evidence reference | Pihak yang mengesahkan closure | Required if approval is required | No name/position assumed | `PENDING_ORG_DECISION` |
| Financial Document | Document reference/type/version/source | Evidence untuk proses terkait | Conditional | One document may support multiple records if allowed | `TECHNICAL_RECOMMENDATION` |
| Audit Reference | Actor/action/time/target/source/policy version | Audit provenance | Required in concept for critical events | Detail technical model pending | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| Correlation Reference | Process correlation | Menghubungkan workflow chain | Conditional | Scope/uniqueness pending technical design | `TECHNICAL_RECOMMENDATION` |
| Causation Reference | Causing event link | Menjelaskan sebab suatu event | Conditional | Particularly corrections/reversals | `TECHNICAL_RECOMMENDATION` |
| Source Transaction Reference | Authoritative source record link | Traceback ke source of truth | Required in concept when event derives from another record | Canonical source per domain pending | `TECHNICAL_RECOMMENDATION` |

---

## 10. Relationship Specification

Cardinality final tidak ditetapkan pada R01 ini. Setiap hubungan kandidat harus mengikuti FIN-DEC dependencies dan source evidence.

| Relationship ID | Source → Target | Description/business rule | Cardinality alternatives | Dependency | Evidence Status | Relationship Status | Risk if unresolved |
|---|---|---|---|---|---|---|---|
| REL-01 | Master Policy → Policy Version | Policy memiliki versi historis yang tidak ditimpa | One-to-many candidate | GOV-09 | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` | `CONFIRMED_CONCEPTUAL` | Hilang histori policy |
| REL-02 | Policy Version → Program | Program dapat reference policy version yang berlaku | Binding per program, per scope, atau aturan lain | FIN-DEC-28 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_DESIGN_DECISION` | Program memakai policy ambigu |
| REL-03 | Policy Version → Ceiling Aggregation Scope | Versi menetapkan mode/ceiling/scope | Scope embedded atau linked object | FIN-DEC-03/05/06 | `CLARIFIED_BY_PROJECT_OWNER` untuk opsi; scope pending | `CANDIDATE_RELATIONSHIP` | Ceiling salah diagregasi |
| REL-04 | Aggregation Scope → Policy Scope Membership | Mengelompokkan Program/Incident/Operation yang termasuk | One/many alternatives | FIN-DEC-05/27/28 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_DESIGN_DECISION` | Membership tidak konsisten |
| REL-05 | Program → Activity | Activity merupakan konteks program bila source model menyatakan | One/many/optional alternatives | FIN-DEC-14 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_DESIGN_DECISION` | Entity ownership/cardinality rancu |
| REL-06 | Program/Activity → Program Budget | Budget dapat berada pada program, activity, atau header/line model | Alternatives pending | FIN-DEC-14/15 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_DESIGN_DECISION` | Roll-up/duplication |
| REL-07 | Program Budget → Budget Line | Budget lines merinci budget bila dibutuhkan | One/many/optional alternatives | FIN-DEC-14 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_DESIGN_DECISION` | Budget amount cannot reconcile |
| REL-08 | Program ↔ Incident | Business context relation | One/many/optional alternatives | FIN-DEC-27 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_DESIGN_DECISION` | Policy and report scope ambiguous |
| REL-09 | Incident ↔ Response Operation | Response operation terkait incident | One/many/optional alternatives | FIN-DEC-04/27 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_ORG_DECISION` | Per-incident cap circumvention |
| REL-10 | Fund Source ↔ Fund Pool | Sumber dana dikelompokkan ke pool jika approved | One/many alternatives | FIN-DEC-10 | SOP sources partial; model unavailable | `PENDING_DESIGN_DECISION` | Restricted cash mixed |
| REL-11 | Funding Allocation ↔ Fund Request | Request dapat memuat allocation bila policy mengizinkan | Optional/multiple alternatives | FIN-DEC-10 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_DESIGN_DECISION` | Request source allocation unclear |
| REL-12 | Funding Allocation ↔ Program Budget/Activity | Allocation dapat dibuat pada budget/activity bila disetujui | Alternatives pending | FIN-DEC-10/14 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_DESIGN_DECISION` | Budget/report allocation duplication |
| REL-13 | Funding Allocation ↔ Fund Pool | Allocation dapat memilih pool yang memenuhi eligibility | Alternatives pending; no fixed cardinality | FIN-DEC-10 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_DESIGN_DECISION` | Cash eligibility ambiguity |
| REL-14 | Fund Pool ↔ Cash Account | Pool dapat berhubungan dengan account(s) sesuai model | One/many alternatives | FIN-DEC-08/10 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_DESIGN_DECISION` | Cash source reconciliation failure |
| REL-15 | Cash Account → Cash Movement Event → Cash Ledger | Movement direkam dan dapat ditelusuri ke account/source | No fixed event-to-ledger cardinality asserted | FIN-DEC-08/09 | `EVIDENCE_NOT_AVAILABLE` | `CANDIDATE_RELATIONSHIP` | Cash balance not auditable |
| REL-16 | Fund Request ↔ Approval Decision | Decision merupakan bagian workflow request | Multiple decisions or other lifecycle alternatives | FIN-DEC-33 | SOP approval evidence partial; authority mapping pending | `CANDIDATE_RELATIONSHIP` | Approval history/authority lost |
| REL-17 | Actor ↔ System Permission/Role Assignment | System access is separate from organizational authority | Multiple assignments possible; exact cardinality not fixed here | Core/IAM decisions | `EVIDENCE_NOT_AVAILABLE` | `CANDIDATE_RELATIONSHIP` | Permission mistaken for authority |
| REL-18 | Actor/Authority ↔ Mandate/Delegation Evidence | Evidence supports authority within scope/time | Multiple/dated alternatives | FIN-DEC-19/22/33 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_ORG_DECISION` | Unauthorized approval |
| REL-19 | Fund Request → Ceiling Consumption Event | Request may cause ceiling event only if approved policy defines it | Zero/many alternatives | FIN-DEC-07 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_ORG_DECISION` | Wrong ceiling timing |
| REL-20 | Approval Decision → Ceiling Consumption Event | Approval may affect ceiling only if chosen event | Zero/many alternatives | FIN-DEC-07 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_ORG_DECISION` | Double or premature consumption |
| REL-21 | Disbursement → Ceiling Consumption Event | Disbursement may affect ceiling if chosen event | Zero/many alternatives | FIN-DEC-07 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_ORG_DECISION` | Ceiling/cash double count |
| REL-22 | Disbursement → Cash Movement Event | Disbursement may result in one or more cash events | No 1:1 assumption | FIN-DEC-08/09 | `EVIDENCE_NOT_AVAILABLE` | `CANDIDATE_RELATIONSHIP` | Cash event missing/duplicated |
| REL-23 | Disbursement → Expenditure Recognition | Disbursement may or may not be recognized as expense at the same time | No 1:1 assumption | FIN-DEC-12 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_ORG_DECISION` | Actual expenditure misstated |
| REL-24 | Financial Obligation ↔ Program | Obligation can be linked to relevant program(s) | Optional/multiple alternatives | FIN-DEC-16 | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` for closure gate; detail pending | `CANDIDATE_RELATIONSHIP` | Closure gate misses obligations |
| REL-25 | Financial Obligation ↔ Activity | Direct activity link if obligation is activity-specific; otherwise trace through budget/program | Direct, indirect, or both alternatives | FIN-DEC-14/16 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_DESIGN_DECISION` | Obligation not traceable to activity or double-linked |
| REL-26 | Financial Obligation ↔ Program Budget | Obligation can be associated with budget when relevant | Optional/multiple alternatives | FIN-DEC-14/16 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_DESIGN_DECISION` | Budget closure incomplete |
| REL-27 | Financial Obligation ↔ Fund Request | Obligation may derive from request but not all obligations do | Optional/multiple alternatives | FIN-DEC-16 | `EVIDENCE_NOT_AVAILABLE` | `CANDIDATE_RELATIONSHIP` | Blocker source lost |
| REL-28 | Financial Obligation ↔ Disbursement/Expenditure Recognition | Obligation may be related to one or more transaction records | Optional/multiple alternatives | FIN-DEC-12/16/31 | `EVIDENCE_NOT_AVAILABLE` | `CANDIDATE_RELATIONSHIP` | Unresolved payment/expense blocker |
| REL-29 | Financial Obligation ↔ Financial Reconciliation | Reconciliation may identify or clear obligation | No fixed cardinality | FIN-DEC-16/18 | `EVIDENCE_NOT_AVAILABLE` | `CANDIDATE_RELATIONSHIP` | Closure evidence ambiguous |
| REL-30 | Financial Reconciliation ↔ Cash/Ceiling/Disbursement/Expenditure Records | Reconciliation consumes relevant source records without replacing them | One reconciliation may cover multiple sources; records may recur per policy | FIN-DEC-08/12/16 | `EVIDENCE_NOT_AVAILABLE` | `CANDIDATE_RELATIONSHIP` | Reconciliation double-count or orphan |
| REL-31 | Program Closure Authority → Program Closure Evidence | Authority evidence applies to program closure | No actor/cardinality assumption | FIN-DEC-18 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_ORG_DECISION` | Unauthorized program closure |
| REL-32 | Financial Closure Authority → Financial Closure Evidence | Authority evidence applies to financial closure | No actor/cardinality assumption | FIN-DEC-18 | `EVIDENCE_NOT_AVAILABLE` | `PENDING_ORG_DECISION` | Unauthorized financial unlock |
| REL-33 | Financial Document ↔ Request/Approval/Disbursement/Expenditure/Reconciliation | Document supports one or more relevant records as allowed | No one-document/one-transaction assumption | Document policy | `EVIDENCE_NOT_AVAILABLE` | `CANDIDATE_RELATIONSHIP` | Evidence duplication/loss |
| REL-34 | Audit/Correlation/Causation → Business Events | Trace actor, event chain, cause, and source | Context-dependent | GOV-09; technical architecture | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` for traceable history; implementation detail pending | `CANDIDATE_RELATIONSHIP` | Lost traceability |

---

## 11. Cardinality and Dependency Matrix

| Relationship area | Alternatives to evaluate | Decision dependency | Status |
|---|---|---|---|
| Policy Version–Program | Policy binding at program activation, policy scope binding, or another approved pattern | FIN-DEC-28 | `PENDING_DESIGN_DECISION` |
| Program–Activity–Budget–Budget Line | Program-level budget, activity-level budget, or header/line arrangement | FIN-DEC-14/15 | `PENDING_DESIGN_DECISION` |
| Program–Incident–Response Operation | One-to-many, many-to-many, or other structure based on SOP/operation model | FIN-DEC-27 | `PENDING_DESIGN_DECISION` |
| Incident/Operation ceiling control | Parent incident, formal response operation, or other defined unit | FIN-DEC-04 | `PENDING_ORG_DECISION` |
| Global membership | Incident/operation/program membership in a policy scope | FIN-DEC-05/06/28 | `PENDING_ORG_DECISION` |
| Fund Source–Fund Pool–Funding Allocation | Single or multiple source/pool allocation; allocation level | FIN-DEC-10 | `PENDING_DESIGN_DECISION` |
| Fund Request–Approval Decision | One or multiple decisions/history entries | FIN-DEC-33 and Finance workflow | `PENDING_ORG_DECISION` |
| Disbursement–Cash Movement | One or multiple cash movements per disbursement or vice versa | FIN-DEC-08/09 | `PENDING_DESIGN_DECISION` |
| Disbursement–Expenditure Recognition | Same-event or delayed/separate recognition | FIN-DEC-12 | `PENDING_ORG_DECISION` |
| Obligation–Program/Activity/Transaction | Direct, indirect, optional, and many-to-many candidate relationships | FIN-DEC-14/16 | `PENDING_DESIGN_DECISION` |
| Reconciliation–Source Records | One reconciliation across multiple source records; repeat reconciliations | FIN-DEC-12/16/31 | `PENDING_DESIGN_DECISION` |
| Program/Finance closure authority | Same or different authorized actors | FIN-DEC-18 | `PENDING_ORG_DECISION` |

No relationship above is converted into physical cardinality or FK in this logical architecture.

---

## 12. Financial Process Architecture

### 12.1 Master Policy Setup

1. Authorized SuperAdmin capability is authenticated.
2. Initial governing source and policy configuration are recorded.
3. Amount, mode, and applicable scope are specified.
4. Approval/evidence requirements are checked according to the policy process.
5. Policy version is activated only after applicable governance conditions are met.
6. Program activation references a valid active policy.
7. Policy version history remains traceable and immutable.

The exact approval workflow and initial amount/mode remain pending. A SuperAdmin capability does not independently create organizational policy.

### 12.2 Program Activation and Freeze

1. Program module provides program identity and state.
2. System checks that an active valid policy applies.
3. If no valid policy applies, activation is blocked under GOV-01/GOV-02.
4. Once a program is running or not formally closed, policy setup/amendment is locked under GOV-03.
5. After program closure, financial completion is checked independently under GOV-04.
6. An amendment remains locked while either closure gate is unresolved.
7. Closure authorities and source records are determined by FIN-DEC-16–18.

### 12.3 Fund Request

1. Actor creates a Fund Request with program/incident/operation context where defined.
2. System validates the request against the active policy version and source restrictions.
3. Available cash and ceiling checks use their separate canonical inputs.
4. Request is routed to approval under an authority model that remains pending FIN-DEC-33.
5. Request submission is not assumed to consume the ceiling unless FIN-DEC-07 selects that event.

### 12.4 Approval

1. Actor identity is verified.
2. System permission is evaluated.
3. Financial approval authority and mandate/delegation evidence are evaluated separately.
4. Decision outcome and evidence are recorded.
5. SuperAdmin capability does not imply financial approval authority.
6. Unauthorized or unsupported approval is denied according to the approved access model.

### 12.5 Ceiling and Cash Control

The following are distinct logical steps:

- Ceiling calculation.
- Ceiling reservation, if adopted.
- Ceiling consumption, according to FIN-DEC-07.
- Eligible cash evaluation, according to FIN-DEC-08/09.
- Cash reservation, if adopted.
- Actual cash movement.
- Expenditure recognition.

No event timing or accounting treatment is selected by this document.

### 12.6 Disbursement and Expenditure

1. Disbursement is processed under applicable approval.
2. Cash movement is recorded from the appropriate account/pool/source.
3. Ceiling ledger effect is determined by the approved policy event.
4. Expenditure recognition follows Finance policy, not an automatic assumption that payment equals expense.
5. Supporting evidence and source transactions are linked.
6. Corrections/reversals are new traceable events; original history is preserved.

### 12.7 Reconciliation

1. Identify relevant Cash Ledger, Ceiling Consumption Ledger, Disbursement, Expenditure, Obligation, and Document records.
2. Compare source amounts and evidence.
3. Record match, discrepancy, unresolved item, and responsible source domain.
4. Correct through a linked event or approved process.
5. Do not silently overwrite source records.
6. Reconciliation closure evidence may contribute to Financial Closure only under approved closure rules.

### 12.8 Program and Financial Closure

Program Closure and Financial Closure are distinct:

- Program Closure Authority relates to Program Closure Evidence.
- Financial Closure Authority relates to Financial Closure Evidence.
- One actor may perform both only if organizational authority explicitly permits it.
- Both gates must be satisfied before policy amendment becomes eligible under GOV-04.

---

## 13. Data Integrity and Transaction Safety

### 13.1 Duplicate transactions

Logical requirements:

- Distinguish duplicate request delivery from duplicate business request.
- Identify a source event and idempotency identity for retryable actions.
- A retry must return/reference the prior outcome rather than create a second financial effect.
- Similar amount, name, or date alone does not prove a duplicate.
- Duplicate business records require controlled review; do not auto-merge or delete.

Details of idempotency scope, retention, payload comparison, and conflict handling are technical design dependencies.

### 13.2 Correlation, causation, and source transaction

| Reference concept | Purpose |
|---|---|
| Source Transaction Reference | Identifies the authoritative record that an event derives from or affects. |
| Correlation Reference | Groups events belonging to one process/workflow context. It should have a defined scope, not be reused indiscriminately for unrelated processes. |
| Causation Reference | Identifies the event that caused a later event, such as a correction or reversal. |
| Audit Reference | Records actor/action/time/target/result and related evidence. |

These references are logical traceability concepts. They do not prescribe implementation-specific IDs, database keys, or API fields.

### 13.3 Double counting

- Cash movement is separate from ceiling consumption.
- Ceiling reservation is separate from final consumption unless policy defines otherwise.
- Reservation-to-disbursement conversion must not count the same amount twice.
- Disbursement is separate from expenditure recognition.
- Financial reconciliation reads these records; it does not duplicate or replace them.
- Retries and repeated callbacks must not create duplicate financial effects.

### 13.4 Concurrency

Scenario: two requests read the same available ceiling or cash pool and both attempt to proceed.

Logical invariant:

> Combined committed or reserved amounts, using the event semantics approved by the organization, must not exceed the applicable policy ceiling or eligible cash.

Possible technical approaches—atomic validation-and-posting, serialization, optimistic version checking, or equivalent—are `TECHNICAL_RECOMMENDATION`. No physical mechanism is selected.

### 13.5 Reversal and correction

Cancellation, expiry, reversal, refund, correction, and disputed transactions must:

- Preserve the original record.
- Link the correction to the original source event.
- Record actor, time, reason, evidence, and policy version where relevant.
- Apply cash, ceiling, expenditure, and closure effects according to approved Finance decisions.
- Avoid deleting history or silently rewriting totals.

Dependencies: FIN-DEC-07, FIN-DEC-31, FIN-DEC-32.

### 13.6 Failure and recovery

Design must account for:

- Payment/approval timeout.
- Duplicate callback.
- Network interruption and retry.
- Partial linked-event failure.
- Source module unavailable or stale.
- Reconciliation mismatch.
- Delayed sync.
- Unknown external transaction outcome.

A timeout alone is not evidence that a transaction succeeded or failed. Reconcile against source evidence before retrying an action with possible financial effect.

---

## 14. Authority, Security and Auditability

### 14.1 Separate concepts

1. User identity/account.
2. Organizational role assignment.
3. System permission.
4. SuperAdmin capability.
5. Financial approval authority.
6. Mandate.
7. Delegation.
8. Program Closure Authority.
9. Financial Closure Authority.
10. Approval Decision.

No system permission or operational assignment automatically creates financial or closure authority.

### 14.2 FIN-DEC-33 authority

SOP halaman 23 yang terlihat menyatakan pengeluaran dana darurat memerlukan persetujuan Ketua TSKKM.

Belum tersedia:

- Identitas pemegang jabatan pada waktu operasi.
- Mandate/delegation.
- Scope persetujuan.
- Masa berlaku kewenangan.
- Acting authority.
- Mapping authority ke user/account.

Status evidence: `SOP_CONFIRMED` secara parsial untuk redaksi persetujuan pada halaman 23.  
Decision status: `PENDING_ORG_DECISION`.

### 14.3 Audit evidence

Untuk aksi kritis, arsitektur secara konseptual membutuhkan:

- Actor.
- Action.
- Timestamp.
- Target record.
- Policy version/scope bila relevan.
- Source transaction and causal reference.
- Reason and supporting evidence jika diwajibkan.
- Authority evidence untuk approval/closure.
- Outcome dan correlation reference.

Persyaratan ini tidak mengizinkan pembuatan jabatan atau authority baru.

---

## 15. Master and Reference Data Catalogue

Katalog berikut merupakan evaluasi kandidat. Nilai final, owner, dan source harus disahkan; Finance tidak mengambil alih master yang dimiliki modul lain.

| Master/reference | Tujuan | Candidate owner/source | Lifecycle/change control | Status/dependency |
|---|---|---|---|---|
| Fund Source Category | Klasifikasi sumber dana | Finance; SOP/approved funding register | Version/deactivate without deleting history | Kategori lengkap pending |
| Fund Pool Classification | Identifikasi cash pool/restriction | Finance | Change controlled | FIN-DEC-08/10 |
| Funding Allocation Type | Menjelaskan jenis alokasi | Finance | Values only after policy | FIN-DEC-10 |
| Transaction Type | Klasifikasi transaksi Finance | Finance | Source-linked, versioned where needed | Finance model pending |
| Approval Decision Type | Klasifikasi keputusan | Finance/governance | Authority-controlled | FIN-DEC-33 |
| Financial Obligation Type | Klasifikasi blocker | Finance/process owners | Values require closure policy | FIN-DEC-16 |
| Expenditure Category | Kategori pengeluaran | Finance; SOP/policy | Restrictions tied to source evidence | FIN-DEC-11/12 |
| Document Type | SK Pengaturan, invoice, evidence, reconciliation docs | Document Governance/Finance | Preserve versions and source | GOV-06 |
| Policy Status | Draft/active/superseded candidate lifecycle | Core/Policy governance | Do not finalize status terms without approval | Design pending |
| Program/Activity Reference | Reference to Program module-owned records | Program module | Finance reads canonical source | FIN-DEC-14/17 |
| Incident/Operation Reference | Reference to Incident/Operations records | Respective modules | Finance reads canonical source | FIN-DEC-27 |
| Currency Reference | Currency used in records | Core/Finance policy | No multi-currency assumption | FIN-DEC-26 |
| Financial Event Status | Request/payment/reconciliation lifecycle | Finance | Status vocabulary requires policy | FIN-DEC-07/12/15 |
| Reconciliation Status | Match/discrepancy/closure states | Finance | Values require process approval | FIN-DEC-16/18 |

No generic all-purpose master table is prescribed. Finance should consume canonical references from owning modules rather than duplicate their data.

---

## 16. Cross-Module Integration Architecture

| Source module | Target/consumer | Data exchanged | Business trigger | Source of truth | Dependency/failure handling |
|---|---|---|---|---|---|
| Core System / IAM | Finance | Actor identity, permissions, SuperAdmin capability references | Authenticated Finance action | IAM/Core | Permission is not authority; deny if identity/permission evidence unavailable per approved policy |
| Program Management | Finance/Policy Freeze | Program identity, state, closure evidence/reference | Program creation, state change, closure | Program module | Unavailable/stale state cannot automatically prove closure; FIN-DEC-29 |
| Incident Management | Finance | Incident identity and status reference | Request/control-unit assignment | Incident module | No duplicate incident master; FIN-DEC-04/27 |
| Response Operations | Finance | Operation identity and status reference | Request/control-unit assignment | Response Operations module | Cardinality pending FIN-DEC-04/27 |
| Program Management | Finance Budget | Program/activity/budget context references | Budget proposal or request | Program module owns Program/Activity | FIN-DEC-14 |
| Finance | Procurement | Approved budget/fund reference and request linkage where authorized | Procurement request/commitment | Finance owns budget/fund data; Procurement owns procurement records | Do not equate PO with payment/expense |
| Procurement | Finance | Request, PO, invoice references, commitment candidates | Procurement workflow events | Procurement owns its records | Commitment treatment pending |
| Logistics/Inventory | Finance | Goods receipt/stock evidence references where relevant | Receipt/reconciliation | Inventory/Logistics owns stock records | Goods receipt is not automatically cash movement or expense recognition |
| Document Management | Finance | SK and financial document references/versions | Upload/verification/transaction evidence | Document service | Missing/corrupt attachment must not be represented as valid evidence |
| Finance | Reporting/Audit | Derived cash, ceiling, disbursement, expenditure, reconciliation data | Report generation | Each Finance record remains canonical in its domain | Report is derived; discrepancies remain visible |
| Audit/Reporting | Finance/Core | Event and traceability references | Audit review/closure | Audit source | No report should overwrite transaction sources |

### Failure handling principles

- Keep source ownership in the originating module.
- Use references/correlation rather than duplicating editable source facts.
- Mark unavailable/stale sources as unresolved; do not interpret absence as “no blocker”.
- Retry only with idempotent semantics.
- Reconcile uncertain external outcomes before creating a new financial effect.
- Record failure/recovery actions in traceable audit history.

---

## 17. Traceability Matrix

| Architecture element | Source/decision | GOV reference | FIN-DEC reference | FIN-TEST reference | Status |
|---|---|---|---|---|---|
| Master Policy before program activation | Owner governance clarification | GOV-01/02 | FIN-DEC-21 | FIN-TEST-59/85 | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| Policy freeze during active/unclosed programs | Owner governance clarification | GOV-03 | FIN-DEC-17 | FIN-TEST-47/48/54/76/81/89/96 | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| Finance completion as separate amendment gate | Owner governance clarification | GOV-04 | FIN-DEC-16/18 | FIN-TEST-49/77/82/88/97 | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| SuperAdmin policy capability | Owner governance clarification | GOV-05 | FIN-DEC-20/22 | FIN-TEST-40/53/54/84/100 | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| SK Pengaturan amendment basis | Owner governance clarification | GOV-06/07 | FIN-DEC-19/21/22 | FIN-TEST-50–52/78/79/86/87/91 | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| Immutable policy versions/history | Owner governance clarification | GOV-09 | FIN-DEC-23/24 | FIN-TEST-55/57/74/91 | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| Rp50m maximum per incident/operation | Owner clarification; SOP p.23 conflict | — | FIN-DEC-01/02/04 | FIN-TEST-24–29/33/36/63/71 | `CLARIFIED_BY_PROJECT_OWNER` + `SOURCE_CONFLICT` |
| Rp100m illustrative value | Owner clarification | — | FIN-DEC-02 | FIN-TEST-35/45 | `CLARIFIED_BY_PROJECT_OWNER` |
| `PER_INCIDENT`/`GLOBAL_ALL_INCIDENTS` | Owner clarification | — | FIN-DEC-03–06 | FIN-TEST-24–29/36–39/42/61/62/70/71/93–95 | `CLARIFIED_BY_PROJECT_OWNER`; details pending |
| Cash eligibility | Owner clarification and Finance decisions | — | FIN-DEC-08/09/11 | FIN-TEST-26/29/31/44/45/72/98 | `CLARIFIED_BY_PROJECT_OWNER`; formula pending |
| Approval authority | SOP p.23 | — | FIN-DEC-33 | FIN-TEST-12/100–105 | `SOP_CONFIRMED` partial; authority mapping pending |
| APP Nasional restrictions | SOP p.24 partial | — | FIN-DEC-11 | FIN-TEST-08/20/45/98 | `SOP_CONFIRMED` partial; enforcement pending |
| Program Budget relationships | Phase specs, incomplete logical model | — | FIN-DEC-14/15 | FIN-TEST-04–06/22/23 | `PENDING_DESIGN_DECISION` |
| Financial closure blockers | Owner governance requirement; source mapping pending | GOV-04 | FIN-DEC-16–18/29 | FIN-TEST-49/60/77/82/88/90/97 | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT`; mapping pending |
| Ledger separation | Finance logical/control requirements | GOV-09 | FIN-DEC-07/08/12/31/32 | FIN-TEST-09–15/66–72/99 | `TECHNICAL_RECOMMENDATION` plus pending policy |
| Idempotency/correlation | Technical integrity requirements | GOV-09 | FIN-DEC-07/29/31/32 | FIN-TEST-13/32/64/65/80 | `TECHNICAL_RECOMMENDATION` |

---

## 18. Risk and Gap Analysis

| Risk ID | Description/root cause | Impact | Affected concepts | Decision dependency | Mitigation | Status |
|---|---|---|---|---|---|---|
| R-01 | Rp50m di-hardcode atau dianggap global cap | Mengubah kebijakan dan membatasi operasi lintas incident | Master Policy, ceiling | FIN-DEC-02/03 | Configured policy version, separate per/global modes | Pending active policy |
| R-02 | Incident/operation control unit tidak jelas | Cap dapat di-reset atau diagregasi salah | Incident, Response Operation, ceiling ledger | FIN-DEC-04/27 | Do not finalize aggregation relationship; preserve parent/context references | `PENDING_ORG_DECISION` |
| R-03 | Global scope/reset tidak jelas | Over-aggregation atau implicit reset | Policy scope membership | FIN-DEC-05/06/28 | Explicit scope/version membership | `PENDING_ORG_DECISION` |
| R-04 | Freeze scope disamakan dengan aggregation scope | Policy lock atau ceiling salah diterapkan | Master Policy, Program, incident | GOV-03/04; FIN-DEC-03–06 | Separate concepts and tests | Logical control |
| R-05 | Obligation tidak terkait ke Program/Activity/transaksi yang relevan | Financial closure gate tidak lengkap | Financial Obligation, Program, Activity | FIN-DEC-14/16 | Candidate links and source references; no forced cardinality | `PENDING_DESIGN_DECISION` |
| R-06 | Program Closure Authority disamakan dengan Financial Closure Authority | Closure tidak sah atau salah direpresentasikan | Closure evidence/authority | FIN-DEC-18 | Separate authority concepts; one actor only if organization approves | `PENDING_ORG_DECISION` |
| R-07 | Funding Allocation memaksakan source/pool cardinality | Duplikasi atau funding report salah | Fund Source, Allocation, Pool, Budget | FIN-DEC-10/14 | Candidate allocation model; defer cardinality | `PENDING_DESIGN_DECISION` |
| R-08 | Cash Movement dianggap Expenditure Recognition | Financial report salah | Cash Ledger, Expenditure Ledger | FIN-DEC-08/12 | Separate logical ledgers | `PENDING_ORG_DECISION` |
| R-09 | Disbursement dianggap 1:1 dengan cash/ceiling/expenditure/reconciliation | Duplicate or orphan ledger record | Disbursement and ledgers | FIN-DEC-07/08/12 | Dotted candidate relationships and event references | `PENDING_DESIGN_DECISION` |
| R-10 | Reservation/disbursement double count | Ceiling/cash consumed twice | Ceiling and cash records | FIN-DEC-07/09/32 | Explicit event semantics and linked conversion | `PENDING_ORG_DECISION` |
| R-11 | Approval authority diasumsikan dari role/permission | Unauthorized financial approval | Actor, authority, decision | FIN-DEC-19/22/33 | Store authority evidence separately | `PENDING_ORG_DECISION` |
| R-12 | SOP p.23 diam-diam direvisi melalui aplikasi | Aplikasi mengubah SOP | Policy evidence | FIN-DEC-01 | Preserve wording; record source conflict | `SOURCE_CONFLICT` |
| R-13 | APP Nasional restriction diperluas atau di-hard-block tanpa source | Kebijakan baru tercipta | Fund Source/restriction | FIN-DEC-11 | Neutral wording; verify complete source/enforcement | Partial evidence |
| R-14 | Policy or transaction history overwrite | Loss of accountability | Version, ledgers, audit | GOV-09 | Immutable history and linked correction | Governance requirement |
| R-15 | Retry/offline sync duplicate effect | Double payment/ceiling/cash effect | Request, disbursement, ledgers | FIN-DEC-25/29/32 | Idempotency and source-event references | Technical design |
| R-16 | Concurrent requests exceed cash/ceiling | Overspend | Cash Pool, ceiling scope | FIN-DEC-07/08/09 | Atomic validation requirement; physical mechanism later | `PENDING_DESIGN_DECISION` |
| R-17 | Unavailable module dianggap tidak ada blocker | Policy unlock prematur | Lock gate and source modules | FIN-DEC-29 | Treat unavailable/stale as unresolved per approved behavior | `PENDING_DESIGN_DECISION` |
| R-18 | Test design diklaim sebagai test execution | False assurance | QA/audit record | Test execution evidence | Separate statuses; actual results Not Executed | No execution |
| R-19 | Rp100m test fixture disalahartikan sebagai template evidence | False claim SOP/template verified | FIN-TEST-35 | Source availability | Explicit fixture labels | `CONDITIONAL` |
| R-20 | Financial Document dipaksa 1:1 dengan transaksi | Evidence duplikasi atau hilang | Document, request, approval, reconciliation | Document model | Allow candidate multi-record support; defer constraints | `PENDING_DESIGN_DECISION` |

---

## 19. Outstanding Decision Register

FIN-DEC-01 sampai FIN-DEC-33 tetap menjadi register utama. Keputusan utama yang masih menghambat logical finalization meliputi:

- FIN-DEC-01: rekonsiliasi SOP halaman 23.
- FIN-DEC-04–07: control unit, global scope, reset, ceiling-consumption event.
- FIN-DEC-08–13: eligible cash, reservations, source/pool, restriction, expenditure, remaining budget.
- FIN-DEC-14–18: budget relationships, obligations, program/financial closure and authority.
- FIN-DEC-19/22/33: SK verification, checker separation, financial approver authority.
- FIN-DEC-23/24: policy version/effective-date transition.
- FIN-DEC-25/26: offline behavior and amount/currency policy.
- FIN-DEC-27–30: cross-module cardinality, policy scope continuity, source freshness, report access.
- FIN-DEC-31/32: reversal/correction and reservation release.

Tidak ada keputusan baru yang dibuat di bagian ini.

---

## 20. Logical Architecture Readiness Assessment

| Readiness area | Status | Alasan |
|---|---|---|
| Finance Decision Register | `READY_AS_CANDIDATE` | FIN-DEC-01–33 tercatat dan dapat dipakai untuk klarifikasi. |
| Entity Catalogue | `CONDITIONAL` | Kandidat entity dan ownership dijelaskan; beberapa owner/domain contracts belum final. |
| Attribute Catalogue | `CONDITIONAL` | Candidate attributes ada; requiredness dan validation banyak bergantung pada policy/source. |
| Relationship Specification | `BLOCKED_BY_DESIGN_DECISION` | FIN-DEC-10/14/27/28 dan lainnya menentukan cardinality. |
| Financial Process Architecture | `CONDITIONAL` | Process separation jelas; approvals, events, and states belum final. |
| Financial Ledger Architecture | `BLOCKED_BY_ORG_DECISION` | Ceiling, cash, expenditure event semantics belum disahkan. |
| Authority/Security | `BLOCKED_BY_ORG_DECISION` | FIN-DEC-19/20/22/33 and closure authority evidence missing. |
| Integration Architecture | `CONDITIONAL` | Ownership boundaries candidate; source contracts/freshness pending. |
| Test design | `CONDITIONAL` | FIN-TEST-01–105 terpetakan; expected behavior pending pada sejumlah test. |
| Test execution | `BLOCKED_BY_MISSING_EVIDENCE` | Tidak ada environment atau execution evidence. |
| Finance Logical Architecture Final | `BLOCKED` | Policy-critical decisions dan relationships belum selesai. |
| Physical Database Design | `NO_GO` | Logical architecture belum disetujui. |
| Implementation | `NO_GO` | Tidak termasuk tahap ini. |

---

## 21. Final Recommendation

1. Tinjau Entity Catalogue dan Relationship Specification sebagai candidate logical model, bukan schema yang disahkan.
2. Selesaikan FIN-DEC-01, FIN-DEC-33, FIN-DEC-04–07, FIN-DEC-08–13, FIN-DEC-16–18, dan FIN-DEC-27–29.
3. Verifikasi dokumen SOP yang belum tersedia sebelum membangun Finance rule berdasarkan template atau halaman yang belum diperiksa.
4. Setelah keputusan dan evidence tersedia, lakukan logical design review lintas Finance, Program, Incident, Response Operations, Procurement, Logistics/Inventory, IAM, Document Management, dan Audit.
5. Jangan memulai physical database design sampai Finance Logical Architecture disetujui.
6. Jangan memulai implementation atau mengubah database pada tahap ini.

**Prinsip akhir:** SIM-TDB harus mengikuti kebijakan dan kewenangan organisasi. Logical architecture hanya mengorganisasi aturan dan data agar konsisten, tertelusur, dan dapat diuji; architecture ini tidak menciptakan policy atau authority baru.

**Status dokumen:** Draft Logical Architecture untuk review.  
**Finance Logical Architecture Final:** `BLOCKED`.  
**Physical Database Design:** `NO_GO`.  
**Implementation:** `NO_GO`.