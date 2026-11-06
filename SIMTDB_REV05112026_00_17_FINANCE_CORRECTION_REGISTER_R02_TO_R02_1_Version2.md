# SIM-TDB — FINANCE CORRECTION REGISTER
## R02 → R02.1
### Independent Audit Findings and Corrective Action Plan

**Document ID:** SIMTDB-REV05112026-00-17-FIN-CR-R01  
**Filename:** `SIMTDB_REV05112026_00_17_FINANCE_CORRECTION_REGISTER_R02_TO_R02_1.md`  
**Revision:** REV05112026-R01  
**Status:** Draft Corrective Action Register — OPEN  
**Mode:** Documentation correction planning only — no implementation  
**Project:** Sistem Informasi Manajemen Tanggap Darurat Bencana (SIM-TDB)  
**Organization:** Caritas Keuskupan Malang — Tim Solidaritas Kemanusiaan Keuskupan Malang (TSKKM)

---

## 1. Executive Summary

Dokumen ini mengubah temuan Independent Audit Report 00.16 menjadi tindakan korektif yang dapat diverifikasi untuk Finance Logical Architecture R02.

Register ini:

- Mempertahankan temuan CR-001 sampai CR-016.
- Menambahkan CR-017 dan CR-018 untuk temuan independen 00.16 mengenai file target R02 yang tidak dapat diverifikasi langsung dan keterbatasan bukti file Correction Register sumber.
- Memetakan setiap corrective action ke acceptance criteria dan metode verifikasi.
- Mempertahankan GOV-01 sampai GOV-09, FIN-DEC-01 sampai FIN-DEC-33, dan FIN-TEST-01 sampai FIN-TEST-105 tanpa perubahan.
- Mempertahankan semua keputusan organisasi yang masih pending.
- Tidak mengubah SOP, R02, R01, R05.1, atau file sumber.
- Tidak membuat physical schema, SQL, migration, seed, API, atau code.
- Tidak menjalankan test.

**R02 belum lulus audit independen.** Status hasil audit 00.16 adalah `NOT PASSED — CORRECTION REQUIRED`. R02.1 hanya dapat diajukan kembali setelah tindakan korektif diterapkan dan evidence penerimaan tersedia.

### Ringkasan jumlah corrective items

| Kategori | Jumlah | Status awal |
|---|---:|---|
| Temuan CR-001 sampai CR-016 | 16 | Dipertahankan dari audit 00.16 |
| Temuan tambahan CR-017 sampai CR-018 | 2 | Ditambahkan dari temuan independen 00.16 |
| **Total** | **18** | **OPEN / BLOCKED sesuai dependency** |

### Prioritas

| Priority | Jumlah |
|---|---:|
| P0 | 7 |
| P1 | 10 |
| P2 | 1 |
| P3 | 0 |

Rincian dan justifikasi terdapat pada Section 9.

---

## 2. Document Control

| Item | Nilai |
|---|---|
| Dokumen target koreksi | Finance Logical Architecture R02 |
| Target dokumen setelah koreksi | Finance Logical Architecture R02.1 — belum dibuat |
| Baseline governance/decision/test | Finance Decision Register R05.1 |
| Audit sumber corrective actions | Independent Audit Report 00.16 |
| Status R01 | `NOT PASSED — CORRECTION REQUIRED` menurut audit 00.16 |
| Status R02 | Menunggu corrective actions dan independent re-audit |
| Finance Logical Architecture Final | `BLOCKED` |
| Physical Database Design | `NO_GO` |
| Implementation | `NO_GO` |

### 2.1 Batas dokumen

Register ini adalah rencana koreksi. `READY FOR RE-AUDIT` tidak berarti R02.1 telah lulus; status itu baru dapat diberikan setelah R02.1 tersedia dan evidence penerapan koreksi dapat ditinjau.

---

## 3. Source Documents

| Source ID | Dokumen | Status | Penggunaan dalam register |
|---|---|---|---|
| SRC-00-16 | `SIMTDB_REV05112026_00_16_FINANCE_R02_INDEPENDENT_AUDIT_REPORT_R01.md` | Konten audit disampaikan dalam percakapan dan digunakan | Sumber utama finding, audit result, dan readiness. File workspace langsung belum diverifikasi. |
| SRC-R02 | `SIMTDB_REV05112026_00_14_FINANCE_LOGICAL_ARCHITECTURE_R02_Version2.md` | `EVIDENCE_NOT_AVAILABLE` sebagai file workspace; konten R02 lain tersedia dalam percakapan | Objek yang perlu dikoreksi. Audit 00.16 secara eksplisit tidak dapat memastikan file `_Version2.md` identik dengan konten R02 yang sebelumnya ditampilkan. |
| SRC-R01 | `SIMTDB_REV05112026_00_14_FINANCE_LOGICAL_ARCHITECTURE_R01.md` | Konten tersedia dalam percakapan | Baseline pembanding konseptual. |
| SRC-R05.1 | `SIMTDB_REV05112026_00_13_FINANCE_DECISION_REGISTER_FINAL_AUDIT_R05_1.md` | Konten tersedia dalam percakapan | Baseline governance, FIN-DEC-01–33, dan FIN-TEST-01–105. |
| SRC-CR-ORIGINAL | Finance Correction Register R01 → R02 | Isi correction criteria disampaikan dalam percakapan; file asli workspace belum diverifikasi | Sumber acceptance criteria awal yang dikutip. |
| SRC-00-15 | `SIMTDB_REV05112026_00_15_FINANCE_CORRECTION_REGISTER_BASIS_CLARIFICATION.md` | Konten tersedia dalam percakapan | Menjelaskan R01 sebagai target dan R05.1 sebagai decision baseline. |
| SRC-SOP-16-29 | Gambar SOP halaman cetak 16–29 | Tersedia dalam percakapan | Evidence SOP parsial, khususnya halaman 23–24. |
| SRC-SOP-OTHER | SOP halaman 1–15 dan 30–95 | `EVIDENCE_NOT_AVAILABLE` | Tidak boleh direkonstruksi. |
| SRC-FIN-FORMS | SOP Finance p.40–41, template p.49, SOP p.62–69 | `EVIDENCE_NOT_AVAILABLE` | Tidak tersedia untuk verifikasi langsung. |
| SRC-AUTH | SK, mandate, delegation, approval matrix, dan closure authority evidence | `EVIDENCE_NOT_AVAILABLE` | Tidak tersedia untuk verifikasi formal. |
| SRC-REPO | Repository, code, database, schema, migrations, seeds, test suite | `EVIDENCE_NOT_AVAILABLE` | Tidak diperiksa atau diubah. |

### 3.1 Source authority

- R05.1 mengendalikan governance requirements, keputusan, test IDs, dan status pending.
- SOP yang tersedia mengendalikan isi operasional yang benar-benar terlihat.
- Owner clarification digunakan sesuai lingkup yang dinyatakan, tetapi tidak menggantikan SK atau formal authority evidence.
- Technical recommendations tetap rekomendasi.
- Missing source harus tetap `EVIDENCE_NOT_AVAILABLE`; tidak boleh diisi dengan asumsi.

---

## 4. Audit Report Reference

Audit 00.16 menyatakan:

- **Overall verdict:** `NOT PASSED — CORRECTION REQUIRED`.
- CR-001 sampai CR-016: 1 PASS, 13 PARTIAL, 2 FAIL.
- CR-003 dinilai FAIL karena relationship atomicity belum ditunjukkan secara memadai.
- CR-011 dinilai FAIL karena edge-to-Relationship-ID mapping tidak konsisten/tidak ditunjukkan lengkap.
- CR-001, CR-002, CR-004–CR-010, CR-012–CR-014, dan CR-016 dinilai PARTIAL.
- CR-015 dinilai PASS hanya untuk pengungkapan keterbatasan evidence, bukan karena seluruh SOP sudah diaudit.
- R02_Version2 exact file tidak tersedia untuk pemeriksaan langsung.
- Repository, code, database, schema, migrations, seeds, dan test execution tidak diperiksa.
- Finance Logical Design Final tetap BLOCKED; Physical Database Design dan Implementation tetap NO_GO.

Correction Register ini menurunkan temuan tersebut menjadi tindakan korektif; tidak mengubah verdict audit 00.16.

---

## 5. Correction Methodology

Setiap correction item memiliki:

- Finding ID.
- Original CR ID jika berlaku.
- Audit evidence.
- Current and required condition.
- Corrective action.
- Acceptance criteria.
- Verification method.
- GOV/FIN-DEC/FIN-TEST references.
- Evidence and decision dependencies.
- Status.

### 5.1 Klasifikasi tindakan

- **Required correction:** dibutuhkan untuk memenuhi finding/acceptance criteria audit.
- **Organizational decision dependency:** harus diputuskan otoritas organisasi; tidak boleh diselesaikan teknis.
- **Missing evidence dependency:** memerlukan source/record yang tidak tersedia.
- **Technical design dependency:** pilihan logical architecture yang belum diputuskan.
- **Recommended improvement:** bukan blocker kecuali kemudian diadopsi sebagai requirement.

### 5.2 Correction status

- `OPEN`
- `IN_PROGRESS`
- `BLOCKED_BY_MISSING_EVIDENCE`
- `BLOCKED_BY_ORG_DECISION`
- `READY FOR RE-AUDIT`
- `VERIFIED_CLOSED`

Semua correction dalam dokumen ini dimulai sebagai `OPEN` atau blocked sesuai dependency. Tidak ada correction yang berstatus `VERIFIED_CLOSED`.

---

## 6. Correction Register CR-001 sampai CR-016

### CR-001 — Complete Entity and Attribute Catalogue

| Field | Isi |
|---|---|
| Finding ID | `AUD-R02-001` |
| Original CR ID | `CR-001` |
| Correction Title | Entity and Attribute Catalogue completeness |
| Severity | CRITICAL |
| Priority | P0 |
| Audit Evidence | Audit 00.16 Section 9 dan Section 12 menyebut R02 memiliki entity catalogue dan grouped attributes, tetapi belum menunjukkan full per-entity coverage untuk purpose, owner, source, lifecycle, logical attributes, requiredness, validation, evidence status, dan dependency. |
| Current Condition | R02 memuat entity dan attribute concepts, namun coverage lengkap per entity belum dapat dibuktikan. |
| Required Condition | Setiap logical entity harus memiliki definisi, classification, owner/source of truth, purpose, lifecycle, attributes, requiredness, validation, evidence status, dan decision dependencies; atau alasan eksplisit sebagai external reference, derived record, grouping, atau value object. |
| Root Cause | Katalog dan atribut disajikan dalam beberapa bagian tanpa completeness crosswalk yang membuktikan setiap entity tercakup. |
| Business Impact | Pemilik proses dan developer dapat mengisi kebutuhan data yang berbeda atau melewatkan informasi penting. |
| Technical Impact | Model logical berisiko incomplete sebelum physical design. |
| Target Document Section | Entity Classification and Ownership; Logical Entity Catalogue; Entity Attribute Catalogue. |
| Corrective Action | Buat entity inventory tunggal dengan satu baris per logical concept. Tambahkan cross-reference dari setiap entity ke attribute catalogue dan ownership. Untuk external/derived/logical reference, jelaskan atribut yang dimiliki source module dan data yang hanya direferensikan Finance. |
| Detailed Instruction | Audit semua entity di R02 overview, process flows, relationship catalogue, dan diagrams. Jangan menghitung external references sebagai Finance-owned entities tanpa alasan. Cantumkan candidate attributes tanpa menetapkan physical types. Tandai atribut dan validation yang bergantung pada pending decisions. |
| Acceptance Criteria | 1) Setiap entity yang disebut di seluruh dokumen muncul dalam inventory atau daftar external references. 2) Tidak ada entity tanpa owner/source. 3) Setiap entity mempunyai purpose, lifecycle, classification, sensitivity/provenance jika tersedia, dan decision dependency. 4) Atribut setiap entity tercatat atau external/derived status dijelaskan. 5) Tidak ada type SQL/physical schema. |
| Verification Method | Cocokkan inventory dengan semua entity mentions, ERD nodes, process flows, relationship sources/targets, dan traceability matrix. Laporkan entity count serta definisi inclusion/exclusion. |
| Related GOV ID | GOV-01–GOV-09 sesuai entity terkait |
| Related FIN-DEC ID | FIN-DEC-10–18, 19–33 sesuai entity terkait |
| Related FIN-TEST ID | FIN-TEST-01–105 sesuai domain |
| Evidence Dependency | R02 exact file; Program/Finance/SOP sources yang relevan |
| Dependency on Other Corrections | CR-002, CR-012, CR-016 |
| Responsible Domain | Finance Architecture; domain owner untuk external references |
| Correction Status | `BLOCKED_BY_MISSING_EVIDENCE` untuk exact R02 Version2; substansi siap dirapikan setelah sumber tersedia |

### CR-002 — Relationship Coverage and Atomicity

| Field | Isi |
|---|---|
| Finding ID | `AUD-R02-002` |
| Original CR ID | `CR-002` |
| Correction Title | Complete and traceable relationship coverage |
| Severity | CRITICAL |
| Priority | P0 |
| Audit Evidence | Audit 00.16 Sections 9, 10, and 13: relationship catalogue tersedia, tetapi belum ada bukti lengkap bahwa setiap hubungan yang disebut dalam narasi dan ERD memiliki satu relationship definition yang dapat ditelusuri. |
| Current Condition | Hubungan sebagian disajikan sebagai group; diagram dan catalogue belum terbukti sinkron edge-by-edge. |
| Required Condition | Setiap logical edge harus mempunyai unique REL ID, source, target, business meaning, status, evidence, dependency, cardinality alternatives, dan optionality bila diketahui. |
| Root Cause | Relationship catalogue dan domain diagrams dibuat sebagai ringkasan, tanpa full edge crosswalk. |
| Business Impact | Relasi penting dapat terlewat, digandakan, atau berbeda interpretasinya antar-reviewer. |
| Technical Impact | Implementer dapat menciptakan relationship yang tidak pernah disetujui. |
| Target Document Section | Relationship Catalogue; Cardinality and Dependency Matrix; Conceptual ERDs. |
| Corrective Action | Buat relationship register yang menjadi satu-satunya katalog logical edges. Pastikan setiap node pair yang disebut dalam prose/diagram mempunyai REL ID atau dijelaskan sebagai non-persisted conceptual link. |
| Detailed Instruction | Enumerasi candidate links antara policy, program, incident, response operation, funding, request, approval, ledgers, obligations, reconciliation, documents, audit, dan closure. Jangan menetapkan physical FK atau cardinality final tanpa evidence. |
| Acceptance Criteria | 1) Setiap edge diagram menunjuk REL ID. 2) Setiap REL ID memiliki satu source dan target yang terdefinisi. 3) Pending relationships menyebut FIN-DEC dependency. 4) Tidak ada orphan relationship atau diagram edge tanpa definisi. 5) Tidak ada cardinality yang dipaksakan. |
| Verification Method | Bandingkan daftar node/edge dari seluruh diagram dengan relationship register; hitung edge yang terpetakan, pending, atau tidak mempunyai source. |
| Related GOV ID | GOV-01–GOV-09 bila relationship mendukung governance |
| Related FIN-DEC ID | FIN-DEC-01–FIN-DEC-33 sesuai relationship |
| Related FIN-TEST ID | FIN-TEST-01–105 sesuai relationship |
| Evidence Dependency | R02 exact file; R05.1 |
| Dependency on Other Corrections | CR-001, CR-003, CR-011, CR-012 |
| Responsible Domain | Finance Logical Architecture |
| Correction Status | `OPEN` |

### CR-003 — Atomic Relationship Specification

| Field | Isi |
|---|---|
| Finding ID | `AUD-R02-003` |
| Original CR ID | `CR-003` |
| Correction Title | Atomic relationship identifiers and grouped-edge control |
| Severity | HIGH |
| Priority | P0 |
| Audit Evidence | Audit 00.16 Section 10 menyatakan beberapa REL entries masih dapat menggabungkan beberapa source/target relationships tanpa atomic sub-edge IDs. Contoh yang diminta diperiksa termasuk REL-15, REL-30, REL-33, REL-34. |
| Current Condition | Beberapa Relationship IDs menjelaskan beberapa business links atau target sets sekaligus; sub-edge mapping tidak selalu tersedia. |
| Required Condition | Satu REL ID merepresentasikan satu logical edge. Relationship group boleh dipakai hanya sebagai heading/container yang memiliki atomic sub-RELs. |
| Root Cause | Relationship IDs digunakan untuk merangkum integration groups, bukan untuk melacak setiap edge. |
| Business Impact | Approval atas satu link dapat terbaca sebagai approval atas link lain yang berbeda makna. |
| Technical Impact | Cardinality, source ownership, dan event semantics menjadi ambigu. |
| Target Document Section | Relationship Catalogue and Conceptual ERDs. |
| Corrective Action | Pecah grouped RELs menjadi atomic relationship IDs atau tambahkan sub-REL register. Pertahankan original IDs sebagai historical group references, dengan explicit mapping jika dipertahankan. |
| Detailed Instruction | Periksa REL-15, REL-30, REL-33, REL-34 dan relationship lain yang menggabungkan beberapa entity pairs. Pisahkan Cash Account→Cash Movement, Cash Movement→Cash Ledger, Reconciliation→Cash, Ceiling, Disbursement, Expenditure, dan Document→record relationships menjadi sub-edges yang bisa diuji. Jangan menetapkan cardinality. |
| Acceptance Criteria | 1) Setiap atomic relationship memiliki source/target tunggal. 2) Group ID memiliki daftar sub-REL IDs bila digunakan. 3) Diagram edge dapat ditelusuri ke atomic REL. 4) Tidak ada kehilangan histori ID. 5) Pending dependency tetap terlihat. |
| Verification Method | Manual review per REL entry, followed by diagram-to-catalogue edge check. |
| Related GOV ID | GOV-09 |
| Related FIN-DEC ID | FIN-DEC-07–18, FIN-DEC-27–33 sesuai hubungan |
| Related FIN-TEST ID | FIN-TEST-09–15, 22–23, 54, 60–72, 99 |
| Evidence Dependency | R02 exact file |
| Dependency on Other Corrections | CR-002, CR-011 |
| Responsible Domain | Finance Logical Architecture |
| Correction Status | `OPEN` |

### CR-004 — Funding Allocation Consistency

| Field | Isi |
|---|---|
| Finding ID | `AUD-R02-004` |
| Original CR ID | `CR-004` |
| Correction Title | Normalize Funding Source Allocation and Funding Assignment concepts |
| Severity | CRITICAL |
| Priority | P0 |
| Audit Evidence | Audit 00.16 Section 10 menyatakan source/pool/target relationships dan cardinality belum final. |
| Current Condition | Funding Source Allocation dan Funding Assignment diperkenalkan, tetapi boundary, ownership, target, dan lifecycle belum lengkap. |
| Required Condition | Pisahkan secara jelas source-to-pool relationship dari assignment of funding to request/budget/activity target, kecuali ada keputusan model yang menggabungkannya dengan alasan. |
| Root Cause | Istilah Funding Allocation dipakai untuk dua business meanings. |
| Business Impact | Funding-source reporting dan restriction control dapat tidak konsisten. |
| Technical Impact | Risiko duplicate allocation records atau undocumented many-to-many links. |
| Target Document Section | Funding and Cash Architecture; Entity Catalogue; Relationship Catalogue; Master Data Catalogue. |
| Corrective Action | Definisikan dua konsep: Funding Source Allocation dan Funding Assignment. Jelaskan opsi bahwa satu konsep dapat menjadi group atau record type bila model yang disetujui demikian. |
| Detailed Instruction | Tampilkan candidate relationships Fund Source↔Funding Source Allocation↔Fund Pool dan Funding Assignment↔Fund Request/Program Budget/Activity. Jangan menyimpulkan one-source/one-pool, multi-source, atau allocation level final. |
| Acceptance Criteria | 1) Dua istilah memiliki definisi non-overlapping. 2) Owner/source tercatat. 3) Tidak ada edge duplikatif. 4) FIN-DEC-10/14 ditampilkan sebagai dependencies. 5) Tidak ada cardinality final tanpa keputusan. |
| Verification Method | Review entity definitions dan REL catalogue; cek konsistensi laporan per source dan budget targets. |
| Related GOV ID | Tidak menambah governance rule; jaga GOV-01–09 |
| Related FIN-DEC ID | FIN-DEC-10, FIN-DEC-14 |
| Related FIN-TEST ID | FIN-TEST-07, 19, 23, 45 |
| Evidence Dependency | R05.1; funding-source SOP lengkap belum tersedia |
| Dependency on Other Corrections | CR-001, CR-002, CR-009 |
| Responsible Domain | Finance; Funding Source owner to be designated |
| Correction Status | `BLOCKED_BY_ORG_DECISION` untuk cardinality final; definisi konseptual dapat dilengkapi |

### CR-005 — Ceiling Consumption Ledger Representation

| Field | Isi |
|---|---|
| Finding ID | `AUD-R02-005` |
| Original CR ID | `CR-005` |
| Correction Title | Explicitly define Ceiling Consumption Ledger and its source events |
| Severity | CRITICAL |
| Priority | P0 |
| Audit Evidence | Audit 00.16 Sections 10 and 14: event and ledger semantics belum lengkap; ceiling ledger disebut tetapi attributes/lifecycle/relationships belum demonstrably complete. |
| Current Condition | Ceiling Consumption Event ada; Ceiling Consumption Ledger belum dipisahkan dan dijelaskan secara konsisten sebagai record set/ledger concept. |
| Required Condition | Definisikan ledger concept terpisah dari event, Cash Ledger, Disbursement Event, Expenditure Ledger, dan Reconciliation. |
| Root Cause | Event object dan ledger record set dipakai bergantian tanpa definisi batas. |
| Business Impact | Risiko reservation/disbursement/consumption dihitung ganda atau hilang. |
| Technical Impact | Tidak dapat merekonstruksi ceiling usage pada waktu tertentu. |
| Target Document Section | Ledger and Event Transition Architecture; Entity Catalogue; Relationship Catalogue. |
| Corrective Action | Jelaskan Ceiling Consumption Event sebagai event unit dan Ceiling Consumption Ledger sebagai logical collection/projection dari event yang memenuhi policy rule, atau jelaskan model alternative. |
| Detailed Instruction | Catat candidate logical attributes: event identity, policy version/scope, control unit, source event, amount/direction, time, actor, correlation, causation, reversal reference, evidence. Jangan menetapkan physical columns atau event consumption rule. |
| Acceptance Criteria | 1) Event dan ledger dibedakan. 2) Cash dan Expenditure ledgers tetap terpisah. 3) Reservation/conversion/reversal tidak double count. 4) FIN-DEC-07/31/32 tetap pending. 5) Historical usage dapat direkonstruksi secara konseptual. |
| Verification Method | Event-to-ledger transition matrix review and traceability walkthrough. |
| Related GOV ID | GOV-09 |
| Related FIN-DEC ID | FIN-DEC-07, 31, 32 |
| Related FIN-TEST ID | FIN-TEST-13–15, 27–29, 32–33, 64–72, 93–95 |
| Evidence Dependency | Finance policy event semantics unavailable |
| Dependency on Other Corrections | CR-001, CR-002, CR-014 |
| Responsible Domain | Finance |
| Correction Status | `BLOCKED_BY_ORG_DECISION` untuk event semantics; logical distinction wajib diperjelas |

### CR-006 — Policy Freeze and Amendment Lifecycle

| Field | Isi |
|---|---|
| Finding ID | `AUD-R02-006` |
| Original CR ID | `CR-006` |
| Correction Title | Complete Policy Amendment and Lock Evaluation lifecycle |
| Severity | CRITICAL |
| Priority | P0 |
| Audit Evidence | Audit 00.16 Section 10 menyatakan lifecycle/transitions dan evidence chain belum lengkap. |
| Current Condition | Policy Amendment dan Policy Lock Evaluation disebut, tetapi transition preconditions, evidence, source states, and history link belum lengkap. |
| Required Condition | Logical lifecycle menunjukkan initial setup, lock evaluation, amendment eligibility, SK basis, validation, activation, supersession, and retained history without bypass. |
| Root Cause | Narrative governance requirements belum dipetakan menjadi explicit candidate transitions and evidence links. |
| Business Impact | Policy changes dapat tertahan tanpa alasan yang dapat dipahami atau teraktivasi tanpa closure evidence. |
| Technical Impact | Lock berisiko diterapkan hanya dengan satu status sederhana. |
| Target Document Section | Policy Amendment and Freeze Architecture; Process Architecture; Relationship Catalogue. |
| Corrective Action | Tambahkan candidate transition table dan relationship map yang menghubungkan Policy Amendment, old/new versions, SK, actor, Policy Lock Evaluation, program gate, finance gate, and activation evidence. |
| Detailed Instruction | Untuk setiap transition tulis initiator capability, preconditions, source evidence, lock result, resulting version, audit event, and pending decisions. Jangan menetapkan approval authority atau status vocabulary yang tidak bersumber. |
| Acceptance Criteria | 1) GOV-01–09 ditelusuri ke model. 2) SK tidak menjadi bypass. 3) SuperAdmin tidak memiliki override. 4) Program closure dan financial closure gate terpisah. 5) Amendment membuat new immutable version. |
| Verification Method | Governance transition walkthrough and FIN-TEST-47–62/74–92 cross-check. |
| Related GOV ID | GOV-01–09 |
| Related FIN-DEC ID | FIN-DEC-16–24, FIN-DEC-29 |
| Related FIN-TEST ID | FIN-TEST-47–62, 74–92 |
| Evidence Dependency | Program and Finance status sources; actual SK/authority evidence |
| Dependency on Other Corrections | CR-001, CR-002, CR-010, CR-012, CR-013 |
| Responsible Domain | Core Policy Governance and Finance |
| Correction Status | `BLOCKED_BY_MISSING_EVIDENCE` / `BLOCKED_BY_ORG_DECISION` for detailed source/authority mapping |

### CR-007 — Financial Obligation and Closure Blocker Semantics

| Field | Isi |
|---|---|
| Finding ID | `AUD-R02-007` |
| Original CR ID | `CR-007` |
| Correction Title | Separate Financial Obligation from Financial Closure Blocker |
| Severity | HIGH |
| Priority | P1 |
| Audit Evidence | Audit 00.16 Section 10: source, clearing event, owner, and closure rules not final. |
| Current Condition | Concepts are distinguished, but classification, sources, blocker criteria, and resolution evidence remain incomplete. |
| Required Condition | Obligation represents an actual financial responsibility; blocker represents any unresolved condition preventing closure and may have no monetary amount. |
| Root Cause | Closure gate depends on multiple Finance and cross-module facts without a complete canonical mapping. |
| Business Impact | False closure or indefinite blocking. |
| Technical Impact | Blocker records could duplicate source-state facts or become stale. |
| Target Document Section | Obligation and Closure Architecture; Entity Catalogue; Relationship Catalogue. |
| Corrective Action | Define obligation categories only where source-backed; map each blocker to source module, canonical record, state, clearing event, and evidence. |
| Detailed Instruction | Add candidate relationships to Program, Activity, Budget, Fund Request, Disbursement, Expenditure Recognition, Reconciliation, and Closure Evidence. Do not require every obligation to have every link or an amount. |
| Acceptance Criteria | 1) Obligation and blocker are separate concepts. 2) No unsupported blocker type is presented as policy. 3) Every blocker can identify source/owner/clearance evidence where known. 4) FIN-DEC-16/18/29 remain dependencies. |
| Verification Method | Trace representative obligation/blocker cases through policy lock evaluation. |
| Related GOV ID | GOV-04 |
| Related FIN-DEC ID | FIN-DEC-14, 16, 18, 29, 31 |
| Related FIN-TEST ID | FIN-TEST-49, 60, 77, 82, 88, 90, 97 |
| Evidence Dependency | Finance closure process/status sources unavailable |
| Dependency on Other Corrections | CR-001, CR-002, CR-008, CR-013 |
| Responsible Domain | Finance and source modules |
| Correction Status | `BLOCKED_BY_ORG_DECISION` for blocker rules |

### CR-008 — Reconciliation Architecture Detail

| Field | Isi |
|---|---|
| Finding ID | `AUD-R02-008` |
| Original CR ID | `CR-008` |
| Correction Title | Complete Reconciliation Case, Item, Discrepancy, and Resolution model |
| Severity | HIGH |
| Priority | P1 |
| Audit Evidence | Audit 00.16 Section 10: detailed ownership/lifecycle/source mapping not demonstrated. |
| Current Condition | Reconciliation concepts exist, but item-level comparison, discrepancy lifecycle, source references, and closure links are incomplete. |
| Required Condition | Reconciliation can cover multiple source records and repeated runs; each discrepancy and resolution is traceable without changing source records. |
| Root Cause | Reconciliation described as a process without complete entity/relationship details. |
| Business Impact | Discrepancies may be lost, duplicated, or treated as resolved without evidence. |
| Technical Impact | Reports may not reconstruct reconciliation history. |
| Target Document Section | Reconciliation and Closure Architecture; Entity/Relationship Catalogue. |
| Corrective Action | Define logical roles/attributes of Reconciliation, Item, Discrepancy, Resolution, Source Reference, and Closure Evidence; clarify whether each is persisted entity or derived/reference concept. |
| Detailed Instruction | Specify candidate lifecycle and source links; status names remain candidate unless approved. Corrections/reversals must be linked to original source event. |
| Acceptance Criteria | 1) Reconciliation source records are identified. 2) Discrepancy links to its source. 3) Resolution links to discrepancy and corrective event/evidence. 4) No source record is overwritten. 5) FIN-DEC-12/16/18/31 remain visible. |
| Verification Method | Walk reconciliation examples across cash, ceiling, disbursement, and expenditure records. |
| Related GOV ID | GOV-09 |
| Related FIN-DEC ID | FIN-DEC-12, 16, 18, 31 |
| Related FIN-TEST ID | FIN-TEST-10, 15, 54, 60, 66–69, 82, 99 |
| Evidence Dependency | Finance reconciliation procedure/templates unavailable |
| Dependency on Other Corrections | CR-001, CR-002, CR-005, CR-007 |
| Responsible Domain | Finance |
| Correction Status | `OPEN` |

### CR-009 — Commitment, Procurement Reference, and Advance

| Field | Isi |
|---|---|
| Finding ID | `AUD-R02-009` |
| Original CR ID | `CR-009` |
| Correction Title | Complete Commitment and Advance Logical Representation |
| Severity | HIGH |
| Priority | P1 |
| Audit Evidence | Audit 00.16 Section 10: concepts mentioned but ownership, attributes, lifecycle, and links incomplete. |
| Current Condition | Commitment/PO/Invoice/Advance/Settlement concepts are mentioned without a complete ownership/reference map. |
| Required Condition | Procurement remains canonical owner for its records; Finance stores references or Finance-owned accounting facts only as needed. |
| Root Cause | Cross-module accounting treatment remains pending. |
| Business Impact | Remaining budget or closure can omit commitments or unsettled advances. |
| Technical Impact | Duplicate PO/invoice records or double-counted liabilities. |
| Target Document Section | Budget/Commitment Architecture; Cross-Module Integration; Entity Catalogue. |
| Corrective Action | Classify Budget Commitment, Procurement Commitment Reference, Advance, Advance Settlement, Outstanding Payable, and Settlement Evidence by owner and source. |
| Detailed Instruction | For each concept state whether it is Finance-owned, Procurement-owned reference, or derived; add candidate links to Program Budget/Activity, Fund Request, Payment/Disbursement, and Financial Obligation without duplicating source records. |
| Acceptance Criteria | 1) Procurement-owned PO/invoice not duplicated as Finance master. 2) Commitment distinct from cash movement and expenditure recognition. 3) Advance/settlement traceable. 4) No remaining-budget formula invented. 5) FIN-DEC-13/31/32 preserved. |
| Verification Method | Source ownership and event lineage review. |
| Related GOV ID | GOV-09 |
| Related FIN-DEC ID | FIN-DEC-13, 14, 16, 31, 32 |
| Related FIN-TEST ID | FIN-TEST-11, 15, 21, 49, 77, 88 |
| Evidence Dependency | Procurement/Finance SOP and accounting policy |
| Dependency on Other Corrections | CR-001, CR-002, CR-008, CR-013 |
| Responsible Domain | Finance and Procurement |
| Correction Status | `BLOCKED_BY_MISSING_EVIDENCE` |

### CR-010 — Authority and IAM Logical Model

| Field | Isi |
|---|---|
| Finding ID | `AUD-R02-010` |
| Original CR ID | `CR-010` |
| Correction Title | Complete Authority, IAM, Mandate, and Approval Relationships |
| Severity | CRITICAL |
| Priority | P0 |
| Audit Evidence | Audit 00.16 Section 10: logical separation exists, but attributes/authority scope/validity/relationship details are incomplete and formal evidence is unavailable. |
| Current Condition | User, role, permission, SuperAdmin, financial authority, mandate, evidence, and decision are described; complete source mapping is not demonstrated. |
| Required Condition | System permission, role, SuperAdmin capability, and organizational financial authority remain separate and traceable. |
| Root Cause | Formal authority evidence and IAM account governance are unavailable. |
| Business Impact | Approval may be attributed to an unauthorized actor. |
| Technical Impact | Role-based access may be mistakenly implemented as approval authority. |
| Target Document Section | Authority/Security/Audit Architecture; Entity Catalogue; Relationship Catalogue. |
| Corrective Action | Provide logical model for actor references, permission, SuperAdmin capability, approval authority, mandate/delegation, authority evidence, approval decision, revocation, and validity. |
| Detailed Instruction | Do not invent names, positions, limits, or authorities. Represent such fields as references to evidence where applicable. Keep FIN-DEC-19/20/22/33 pending. |
| Acceptance Criteria | 1) SuperAdmin not treated as financial approver. 2) Permission does not imply authority. 3) Mandate/delegation references support scope/time where evidence exists. 4) Approval decision can cite authority evidence. 5) No authority is invented. |
| Verification Method | Authority relationship walk-through and negative test traceability review. |
| Related GOV ID | GOV-05/06/08 |
| Related FIN-DEC ID | FIN-DEC-19, 20, 22, 33 |
| Related FIN-TEST ID | FIN-TEST-12, 50–57, 78–79, 84, 100–105 |
| Evidence Dependency | IAM/account governance, mandate/delegation, authority matrix |
| Dependency on Other Corrections | CR-001, CR-002, CR-006 |
| Responsible Domain | Core/IAM, Finance, Organization |
| Correction Status | `BLOCKED_BY_MISSING_EVIDENCE` |

### CR-011 — Conceptual ERD and Edge Traceability

| Field | Isi |
|---|---|
| Finding ID | `AUD-R02-011` |
| Original CR ID | `CR-011` |
| Correction Title | Complete ERDs and Relationship-ID Crosswalk |
| Severity | HIGH |
| Priority | P0 |
| Audit Evidence | Audit 00.16 Section 10: diagrams exist in available R02 content but edge-to-REL mapping is not consistent. |
| Current Condition | Domain diagrams are present; every diagram edge is not demonstrably mapped to a Relationship ID. |
| Required Condition | Diagrams must be consistent with Entity and Relationship Catalogues, with status and dependency on each edge. |
| Root Cause | ERD and relationship catalogue were produced separately without completed reconciliation. |
| Business Impact | Reviewers cannot verify whether relationships are missing or unsupported. |
| Technical Impact | Implementation may follow diagram assumptions rather than approved logical relationships. |
| Target Document Section | Conceptual ERD; Relationship Specification; Traceability. |
| Corrective Action | Provide domain diagrams and consolidated diagram; add REL ID/status/decision dependency on every edge or a complete edge-to-REL crosswalk. |
| Detailed Instruction | Include Policy/Governance; Program/Incident/Response; Funding/Budget/Cash; Request/Approval/Authority; Ceiling/Disbursement/Expenditure; Reconciliation/Closure; Document/Audit. Use dotted lines for pending relations. |
| Acceptance Criteria | 1) Required diagrams exist. 2) All critical entities are present or explicitly external. 3) Every edge maps to REL ID/sub-REL. 4) No unsupported cardinality. 5) Diagrams render as Mermaid. |
| Verification Method | Diagram render check and edge-by-edge comparison with catalogue. |
| Related GOV ID | GOV-01–09 as applicable |
| Related FIN-DEC ID | FIN-DEC-01–33 as applicable |
| Related FIN-TEST ID | FIN-TEST-01–105 as applicable |
| Evidence Dependency | Exact R02 Version2 file |
| Dependency on Other Corrections | CR-001, CR-002, CR-003, CR-012 |
| Responsible Domain | Enterprise/Logical Architecture |
| Correction Status | `BLOCKED_BY_MISSING_EVIDENCE` for exact target; `OPEN` for content |

### CR-012 — Requirement and Architecture Traceability

| Field | Isi |
|---|---|
| Finding ID | `AUD-R02-012` |
| Original CR ID | `CR-012` |
| Correction Title | Complete Bidirectional Traceability Matrix |
| Severity | HIGH |
| Priority | P1 |
| Audit Evidence | Audit 00.16 Section 10: traceability matrix is summary-level, not complete per entity, attribute, relationship, process, and test. |
| Current Condition | Selected requirements map to architecture, but full coverage is not demonstrated. |
| Required Condition | Source → requirement → process → entity → attribute → relationship → test traceability, with pending status retained. |
| Root Cause | Traceability grouped by domain/decision rather than atomic requirement. |
| Business Impact | Requirements or unresolved decisions can be lost during revision. |
| Technical Impact | Test gaps and unsupported attributes remain hidden. |
| Target Document Section | Traceability Matrix; Test Traceability. |
| Corrective Action | Expand traceability to item level and report unmapped items. |
| Detailed Instruction | Map each source requirement or owner clarification to entity/process/relationship/test; mark technical recommendations and missing evidence separately. |
| Acceptance Criteria | 1) Every critical architecture element has source/provenance or technical rationale. 2) Every pending decision maps to affected entities/relationships/tests. 3) Unmapped elements are listed. 4) Test execution is not inferred. |
| Verification Method | Coverage review and cross-reference check. |
| Related GOV ID | GOV-01–09 |
| Related FIN-DEC ID | FIN-DEC-01–33 |
| Related FIN-TEST ID | FIN-TEST-01–105 |
| Evidence Dependency | Exact target document and complete source files |
| Dependency on Other Corrections | CR-001–CR-011, CR-016 |
| Responsible Domain | Requirements/Architecture |
| Correction Status | `OPEN` |

### CR-013 — Cross-Module Integration Contracts

| Field | Isi |
|---|---|
| Finding ID | `AUD-R02-013` |
| Original CR ID | `CR-013` |
| Correction Title | Complete Per-Module Logical Integration Contracts |
| Severity | HIGH |
| Priority | P1 |
| Audit Evidence | Audit 00.16 Section 10: module owners are listed, but per-integration version, freshness, cancellation, retry, failure, and reconciliation details are incomplete. |
| Current Condition | Integration overview exists; complete contract coverage per module pair is not demonstrated. |
| Required Condition | Each integration identifies owner, consumer, canonical ID, event, version/time, freshness, correction/cancellation, idempotency/retry, failure, and reconciliation responsibility. |
| Root Cause | Integration design remains summary-level. |
| Business Impact | Stale or corrected records may be misused by Finance or closure gate. |
| Technical Impact | Retries may create duplicate events or inconsistent policy evaluations. |
| Target Document Section | Cross-Module Integration Architecture. |
| Corrective Action | Add a contract matrix per integration without defining API endpoints or physical transport. |
| Detailed Instruction | Cover Core/IAM, Program, Incident, Response Operations, Procurement, Logistics/Inventory, Document Management, Finance, Reporting/Audit. Distinguish references from duplicated data. |
| Acceptance Criteria | Each integration has the required contract fields or an explicit pending dependency. No module ownership is reassigned. |
| Verification Method | Contract-by-contract checklist and source ownership review. |
| Related GOV ID | GOV-02–04/06/09 as applicable |
| Related FIN-DEC ID | FIN-DEC-16–18/25/27–30 |
| Related FIN-TEST ID | FIN-TEST-13, 29–32, 58, 60, 64–65, 70–80, 90, 92 |
| Evidence Dependency | Source-module state vocabularies and integration requirements |
| Dependency on Other Corrections | CR-001, CR-002, CR-007, CR-008, CR-012 |
| Responsible Domain | Cross-Module Architecture |
| Correction Status | `OPEN` |

### CR-014 — Ledger Event Semantics

| Field | Isi |
|---|---|
| Finding ID | `AUD-R02-014` |
| Original CR ID | `CR-014` |
| Correction Title | Complete Conditional Ledger/Event Effect Matrix |
| Severity | CRITICAL |
| Priority | P0 |
| Audit Evidence | Audit 00.16 Section 10: ledger concepts separated, but event-by-ledger transition matrix is incomplete. |
| Current Condition | Reservation, consumption, cash movement, disbursement, expenditure recognition, reversal, and reconciliation are named but their exact effects remain pending. |
| Required Condition | Each event concept has purpose, source, possible ledger effects, reversal/correction links, and decision dependency. |
| Root Cause | FIN-DEC-07/08/09/12/31/32 are unresolved. |
| Business Impact | Double counting, incorrect cash availability, or wrong expenditure totals. |
| Technical Impact | Event processing can produce inconsistent ledger states. |
| Target Document Section | Financial Ledger Architecture; Transaction Safety; Process Architecture. |
| Corrective Action | Add event-to-ledger matrix with conditional effects; do not choose accounting or ceiling policy. |
| Detailed Instruction | Cover reservation, consumption, release, conversion, cash movement, disbursement, expenditure recognition, correction, reversal, refund, and reconciliation. |
| Acceptance Criteria | 1) Cash, ceiling, and expenditure ledgers remain distinct. 2) Reservation is not automatically expenditure. 3) Conversion does not double count. 4) Corrections link to original events. 5) Pending decision is shown for every unresolved effect. |
| Verification Method | Scenario walkthrough against FIN-TEST-13–15, 32, 64–72, 99. |
| Related GOV ID | GOV-09 |
| Related FIN-DEC ID | FIN-DEC-07, 08, 09, 12, 31, 32 |
| Related FIN-TEST ID | FIN-TEST-13–15, 32, 64–72, 99 |
| Evidence Dependency | Finance policy/accounting treatment |
| Dependency on Other Corrections | CR-005, CR-008, CR-009 |
| Responsible Domain | Finance/Internal Control |
| Correction Status | `BLOCKED_BY_ORG_DECISION` for event semantics |

### CR-015 — SOP and Evidence Traceability

| Field | Isi |
|---|---|
| Finding ID | `AUD-R02-015` |
| Original CR ID | `CR-015` |
| Correction Title | Preserve Evidence Boundaries and Complete Source Traceability |
| Severity | HIGH |
| Priority | P1 |
| Audit Evidence | Audit 00.16 Section 10: R02 correctly limits direct SOP claims but Finance source pages/templates remain unavailable. |
| Current Condition | Evidence limitations are disclosed; source coverage remains incomplete. |
| Required Condition | Every SOP-derived rule cites verified page/source; unavailable evidence remains explicitly unavailable. |
| Root Cause | SOP scans/templates outside pages 16–29 were not provided for audit. |
| Business Impact | Unverified SOP requirements may be omitted or misinterpreted. |
| Technical Impact | Data model may not preserve official forms/processes. |
| Target Document Section | Source Inventory; SOP Traceability; Evidence Register. |
| Corrective Action | Preserve existing limitation statements and collect missing Finance/procurement source pages before finalization. |
| Detailed Instruction | List exact missing pages/templates and identify affected FIN-DEC/CRs; do not reconstruct their contents. |
| Acceptance Criteria | 1) Every SOP claim is page-linked. 2) Missing pages remain `EVIDENCE_NOT_AVAILABLE`. 3) No unsupported form/field/policy is asserted. |
| Verification Method | Compare source inventory and every SOP-derived rule. |
| Related GOV ID | GOV-01–09 as applicable |
| Related FIN-DEC ID | FIN-DEC-01, 10–13, 19, 21, 33 |
| Related FIN-TEST ID | FIN-TEST-08, 20, 35, 45, 98 |
| Evidence Dependency | SOP pages 1–15/30–95; Finance pages 40–41/49/62–69 |
| Dependency on Other Corrections | CR-012 |
| Responsible Domain | SOP/Requirements Traceability |
| Correction Status | `BLOCKED_BY_MISSING_EVIDENCE` |

### CR-016 — Test Traceability

| Field | Isi |
|---|---|
| Finding ID | `AUD-R02-016` |
| Original CR ID | `CR-016` |
| Correction Title | Complete Per-Test Architecture Traceability |
| Severity | HIGH |
| Priority | P1 |
| Audit Evidence | Audit 00.16 Section 10: test IDs are preserved, but per-test entity/relationship/process/decision mapping is incomplete. |
| Current Condition | Test coverage is grouped by ranges/domains; individual mapping is not demonstrated. |
| Required Condition | Each FIN-TEST maps to requirement, process, entity, relationship, expected result, decision dependency, design status, execution readiness, and actual result. |
| Root Cause | Test traceability summarized rather than itemized. |
| Business Impact | Critical entity or transaction path may lack a test. |
| Technical Impact | Pending policy could be mistaken for a fixed expected result. |
| Target Document Section | Test Traceability Matrix. |
| Corrective Action | Create a row per FIN-TEST-01–105 and map every test to architecture elements without changing IDs or claiming execution. |
| Detailed Instruction | If original test details are unavailable, record missing details as `EVIDENCE_NOT_AVAILABLE`; do not recreate or invent scenario content. Keep Actual Result `Not Executed`. |
| Acceptance Criteria | 1) All IDs 01–105 appear exactly once. 2) No ID is deleted/renumbered. 3) Each test has dependencies and expected result status. 4) Actual Result remains Not Executed absent evidence. |
| Verification Method | Test ID count/duplicate check and test-to-entity/relationship crosswalk. |
| Related GOV ID | GOV-01–09 as relevant |
| Related FIN-DEC ID | FIN-DEC-01–33 |
| Related FIN-TEST ID | FIN-TEST-01–105 |
| Evidence Dependency | Full original test register and R02 Version2 file |
| Dependency on Other Corrections | CR-001, CR-002, CR-012 |
| Responsible Domain | QA/Requirements Traceability |
| Correction Status | `BLOCKED_BY_MISSING_EVIDENCE` for exact test source details |

---

## 7. Additional Findings CR-017 Onward

### CR-017 — Exact R02 Target File Availability and Revision Identity

| Field | Isi |
|---|---|
| Finding ID | `AF-01` |
| Original CR ID | N/A — new finding from audit 00.16 |
| Correction Title | Verify exact R02 Version2 file and document identity |
| Severity | HIGH |
| Priority | P0 |
| Audit Evidence | Audit 00.16 Section 2: exact requested file `SIMTDB_REV05112026_00_14_FINANCE_LOGICAL_ARCHITECTURE_R02_Version2.md` tidak tersedia untuk pemeriksaan langsung. |
| Current Condition | Audit menilai konten R02 yang tersedia dalam percakapan dengan nama berbeda; identitas dengan file Version2 belum dapat dipastikan. |
| Required Condition | Exact target file, document ID, filename, revision, and content hash/version reference are recorded before re-audit. |
| Root Cause | File workspace/repository tidak tersedia dalam audit context. |
| Business Impact | Verdict mungkin tidak berlaku pada file target yang sebenarnya. |
| Technical Impact | Correction verification dapat dilakukan pada versi yang salah. |
| Target Document Section | Document Control and Source Inventory R02.1 |
| Corrective Action | Sediakan exact R02_Version2 file; catat filename, document ID, revision, date, and source location. |
| Detailed Instruction | Jangan mengubah file R02 saat menyiapkan bukti. Pastikan auditor dapat membedakan R01, R02, dan R02_Version2. |
| Acceptance Criteria | Exact file tersedia dan audited; revision/filename/content identity dicatat; audit findings menunjuk lokasi pada file tersebut. |
| Verification Method | Inspect source file and compare document control/revision metadata; no implementation inspection implied. |
| Related GOV ID | Tidak mengubah governance |
| Related FIN-DEC ID | Tidak mengubah decision register |
| Related FIN-TEST ID | Tidak mengubah test IDs |
| Evidence Dependency | Exact R02_Version2 file |
| Dependency on Other Corrections | Mendahului verification akhir seluruh CR |
| Responsible Domain | Document Control |
| Correction Status | `BLOCKED_BY_MISSING_EVIDENCE` |

### CR-018 — Original Correction Register Provenance

| Field | Isi |
|---|---|
| Finding ID | `AF-02` |
| Original CR ID | N/A — new finding from audit 00.16 |
| Correction Title | Verify original CR-001–CR-016 register source and version |
| Severity | MEDIUM |
| Priority | P1 |
| Audit Evidence | Audit 00.16 Additional Findings: correction criteria disampaikan dalam percakapan, tetapi original register file workspace belum dapat diverifikasi. |
| Current Condition | Acceptance criteria tersedia dari supplied text; provenance/version of original document is not independently confirmed. |
| Required Condition | Original Correction Register file/version is preserved and its CR descriptions/acceptance criteria are checked against the audit working copy. |
| Root Cause | Original file location/access was not available. |
| Business Impact | Corrective action could unintentionally omit or reword original acceptance criteria. |
| Technical Impact | R02.1 may be evaluated against an incomplete register. |
| Target Document Section | Correction Control and Document History |
| Corrective Action | Provide the original Correction Register file or formally confirm the supplied text is the authoritative version for CR-001–CR-016. |
| Detailed Instruction | Do not create or alter findings to match a guessed original. Record differences as document-control items if found. |
| Acceptance Criteria | Original CR IDs and criteria are compared; deviations are explicitly recorded; no CR is removed/renumbered. |
| Verification Method | Side-by-side document review and CR ID/acceptance criteria cross-check. |
| Related GOV ID | No governance change |
| Related FIN-DEC ID | FIN-DEC-01–33 as related |
| Related FIN-TEST ID | FIN-TEST-01–105 as related |
| Evidence Dependency | Original Correction Register file or owner confirmation |
| Dependency on Other Corrections | CR-001–CR-016 verification |
| Responsible Domain | Document Control/Requirements Governance |
| Correction Status | `BLOCKED_BY_MISSING_EVIDENCE` |

---

## 8. Detailed Corrective Action Specifications

### 8.1 Dependency sequence

| Sequence | Corrections | Reason |
|---|---|---|
| 1 | CR-017, CR-018 | Establish exact audit target and corrective baseline. |
| 2 | CR-001, CR-002, CR-003 | Entity/relationship inventory and atomic structure. |
| 3 | CR-004, CR-005, CR-007, CR-008, CR-009, CR-010 | Finance model, ledgers, obligations, authority. |
| 4 | CR-006, CR-011, CR-013 | Governance lifecycle, diagrams, cross-module contracts. |
| 5 | CR-012, CR-014, CR-016 | Traceability, transaction semantics, test coverage. |
| 6 | CR-015 | Source completeness; must remain pending if evidence is not provided. |

Sequence is a work order, not a decision status.

### 8.2 Required vs dependency-bound work

| Work type | Can proceed without organizational decision? | Constraint |
|---|---|---|
| Entity classification and terminology cleanup | Yes, as documentation correction | Must not invent source ownership/authority. |
| Relationship atomicity and ID mapping | Yes, as logical correction | Cardinality stays pending. |
| Ledger conceptual separation | Yes | Event impacts remain conditional. |
| Authority evidence attributes | Partially | No named authority, role, or mandate invented. |
| Policy lifecycle documentation | Partially | GOV-01–09 preserved; source status mapping pending. |
| SOP traceability | Partially | Only verified pages are mapped; missing pages remain unavailable. |
| Test traceability | Partially | Missing historic test details are not reconstructed. |
| Funding cardinality and accounting treatment | No finalization | Requires FIN-DEC-10/12/13 and related decisions. |

---

## 9. Priority and Severity Matrix

| Priority | Meaning | Corrections |
|---|---|---|
| P0 | Must be addressed before R02 can be re-audited for logical completeness. | CR-001, CR-002, CR-003, CR-004, CR-005, CR-006, CR-010, CR-011, CR-017 |
| P1 | Must be resolved or explicitly dependency-blocked before final architecture approval. | CR-007, CR-008, CR-009, CR-012, CR-013, CR-014, CR-015, CR-016, CR-018 |
| P2 | No P2 item currently assigned. | — |
| P3 | No P3 item currently assigned. | — |

Severity and priority are separate. A P1 correction can still depend on unavailable evidence or pending decisions.

---

## 10. Entity and Relationship Correction Plan

### 10.1 Entity correction

R02.1 shall:

1. Inventory every entity/concept referenced in headings, process flows, diagrams, attributes, relationships, and integrations.
2. Assign one classification:
   - Finance-owned business entity.
   - Finance-owned configuration entity.
   - Business event.
   - Ledger record/projection.
   - External module reference.
   - Evidence/document reference.
   - Derived evaluation.
   - Value object/logical reference.
3. Identify owner/source of truth or mark `OWNER TO BE DESIGNATED` / `EVIDENCE_NOT_AVAILABLE`.
4. Provide per-entity candidate attributes and explain non-persisted/external concepts.
5. Explain the entity count; do not equate conceptual entity count with physical table count.

### 10.2 Relationship correction

R02.1 shall:

1. Preserve REL-01–REL-34 and existing later IDs; no renumbering.
2. Add further IDs only after the highest existing REL ID and only where a distinct relationship is identified.
3. Split or enumerate grouped relationships into atomic sub-edges.
4. Map every diagram edge to an REL ID.
5. Preserve candidate/pending status and cardinality alternatives.
6. Identify unlinked entity nodes or explain them as external/derived references.
7. Avoid physical FK or DDL.

### 10.3 Relationship ID integrity

- Every REL ID must be unique.
- Every relationship must reference known source and target concepts.
- Every relationship must state meaning, dependency, evidence status, relationship status, and unresolved risk.
- Grouped relationships must have enumerated sub-relations.
- A relationship that exists only as a narrative statement must be either added to the catalogue or marked explicitly as non-edge/contextual reference.

---

## 11. Ledger and Financial Integrity Correction Plan

R02.1 shall provide an event-effect matrix that keeps the following distinct:

| Concept | Required documentation |
|---|---|
| Cash Reservation/Encumbrance | Whether reservation exists, source, release/expiry, and cash impact; FIN-DEC-09/32 remain pending. |
| Ceiling Reservation | Whether reservation exists and its relationship to ceiling consumption; FIN-DEC-07 pending. |
| Ceiling Consumption | Event selected by approved policy; do not choose in advance. |
| Ceiling Release/Reversal | Links to original event and applies only if policy permits. |
| Cash Movement | Cash account/pool/source and evidence reference. |
| Disbursement | Request, authority, payment evidence, and actual outcome references. |
| Expenditure Recognition | Canonical Finance recognition source; FIN-DEC-12 pending. |
| Expenditure Correction | Linked correction/reversal; original remains intact. |
| Financial Reconciliation | Compares records; does not replace source ledgers. |

Acceptance:

- No reservation is automatically treated as expenditure.
- No disbursement is automatically treated as recognized expenditure.
- No reservation-to-disbursement transition double counts.
- No correction overwrites the original.
- Every event has source, actor, time, and applicable policy context where evidence allows.
- Unresolved treatment remains explicitly pending.

---

## 12. ERD Correction Plan

R02.1 shall include conceptual diagrams for:

1. Policy and Governance.
2. Program, Incident, and Response Operation.
3. Funding, Budget, and Cash.
4. Request, Approval, and Authority.
5. Ceiling, Disbursement, and Financial Ledgers.
6. Reconciliation and Closure.
7. Document and Audit.
8. Consolidated Finance Logical Overview.

For each diagram:

- Every node must exist in the Entity Catalogue or be labeled an external reference/derived concept.
- Every edge must include an REL ID or refer to an explicit edge mapping table.
- Pending edges use dotted representation and show Decision IDs.
- Solid lines are limited to conceptual relationships sufficiently supported by the baseline; no physical cardinality is implied.
- No disconnected critical entity remains without explanation.
- Diagrams must be valid Mermaid and cross-checked against the Relationship Catalogue.

---

## 13. Integration Correction Plan

R02.1 shall supply one row per integration contract with:

| Required field | Requirement |
|---|---|
| Source module and owner | Identify the canonical data owner. |
| Consumer module | Identify Finance or policy-gate consumer. |
| Canonical identifier | Reference the source record without duplicating the master. |
| Data meaning | Define what fact/reference is exchanged. |
| Business trigger | Identify event that causes the logical exchange. |
| Source version/effective time | Include where the source supports it; otherwise mark pending. |
| Freshness | Define or mark decision dependency. |
| Correction/cancellation behavior | Explain how downstream references remain traceable. |
| Retry/idempotency | Specify logical expectation without API implementation. |
| Failure behavior | Missing/stale source must not silently prove closure. |
| Reconciliation owner | Identify source of discrepancy resolution. |

No endpoint, API payload, database event, or implementation detail is authorized by this Correction Register.

---

## 14. SOP and Evidence Dependency Register

| Evidence ID | Required source/evidence | Corrective actions affected | Current status |
|---|---|---|---|
| EV-01 | Exact R02_Version2 file | All CR verification | `BLOCKED_BY_MISSING_EVIDENCE` |
| EV-02 | Original CR-001–CR-016 register file/version | CR-001–CR-016 acceptance verification | `BLOCKED_BY_MISSING_EVIDENCE` |
| EV-03 | SOP pages 1–15 and 30–95 | SOP traceability and Finance process review | `BLOCKED_BY_MISSING_EVIDENCE` |
| EV-04 | SOP Finance p.40–41 | Finance/entity/source validation | `BLOCKED_BY_MISSING_EVIDENCE` |
| EV-05 | APP-KWI template p.49 | Form and nominal-source verification | `BLOCKED_BY_MISSING_EVIDENCE` |
| EV-06 | SOP Procurement/Finance p.62–69 | Commitment, invoice, payment, procurement integration | `BLOCKED_BY_MISSING_EVIDENCE` |
| EV-07 | Formal mandate/delegation/approval matrix | CR-010; FIN-DEC-19/20/22/33 | `BLOCKED_BY_MISSING_EVIDENCE` |
| EV-08 | Program state/closure source records and evidence | CR-006/007/013 | `BLOCKED_BY_MISSING_EVIDENCE` |
| EV-09 | Finance closure and accounting policy | CR-005/007/008/009/014 | `BLOCKED_BY_MISSING_EVIDENCE` |
| EV-10 | Full historical FIN-TEST register details | CR-016 | `BLOCKED_BY_MISSING_EVIDENCE` if not in R05.1/source files |

Missing evidence must not be reconstructed from assumption or earlier paraphrase.

---

## 15. Decision Dependency Register

R02.1 must preserve R05.1 decisions without altering status. Correction work may document impact and options; it may not decide for the organization.

| Decision group | IDs | Correction impact |
|---|---|---|
| SOP/Rp50m reconciliation | FIN-DEC-01 | Preserve wording and clarification separately; source conflict remains until formal resolution. |
| Initial policy/configuration | FIN-DEC-02/03/21 | Do not activate or assume value/mode/source. |
| Ceiling control unit/scope | FIN-DEC-04/05/06 | Do not finalize aggregation key or reset behavior. |
| Ceiling event semantics | FIN-DEC-07 | Ledger event-effect matrix remains conditional. |
| Cash/funding | FIN-DEC-08/09/10/11 | Do not finalize eligible cash, allocation cardinality, or restriction enforcement. |
| Expenditure/budget | FIN-DEC-12/13/14/15 | Do not finalize recognition, formula, or budget cardinality. |
| Closure | FIN-DEC-16/17/18/29 | Do not finalize blockers, status mapping, authority, freshness/failure behavior. |
| SK/SuperAdmin/authority | FIN-DEC-19/20/22/33 | No actual identity, mandate, verifier, or approver is invented. |
| Policy transitions | FIN-DEC-23/24 | Do not reinterpret active/historical programs. |
| Offline/representation | FIN-DEC-25/26 | Do not finalize offline authority or currency policy. |
| Program/Incident/Operation and scope | FIN-DEC-27/28 | Do not set cardinality or scope membership. |
| Corrections/reservations | FIN-DEC-31/32 | Do not decide ledger reversal or release behavior. |

---

## 16. FIN-TEST Traceability Correction Plan

R02.1 must preserve FIN-TEST-01–FIN-TEST-105, without deleting or renumbering.

For every test, the corrected traceability matrix must identify:

- Test ID.
- Requirement or control.
- Relevant process.
- Entity/relationship.
- FIN-DEC dependency.
- Expected result.
- Test Design Status.
- Execution Readiness.
- Actual Result.
- Evidence reference or missing evidence.

### Test status constraints

- Actual Result remains **Not Executed** unless execution evidence exists.
- A pending decision must make Expected Result conditional or mark execution readiness blocked.
- A test fixture is not source evidence.
- No test can be reported pass because the logical design contains an expected outcome.
- The full details for tests whose source text is unavailable must be marked `EVIDENCE_NOT_AVAILABLE`; do not recreate the missing scenario.

---

## 17. Acceptance Criteria Matrix

| CR ID | Required acceptance condition | Verification |
|---|---|---|
| CR-001 | Every entity is defined or explicitly classified external/derived/logical; owner, source, lifecycle, attributes and dependencies documented. | Entity inventory-to-attribute matrix completeness check. |
| CR-002 | Every business relationship has a unique ID and complete source/target/meaning/status/dependency. | Relationship catalogue-to-entity cross-check. |
| CR-003 | Every relationship ID is atomic or has enumerated atomic sub-edges. | REL-by-REL review and diagram edge mapping. |
| CR-004 | Funding source allocation and assignment meanings are distinct or explicitly reconciled. | Funding model review against FIN-DEC-10/14. |
| CR-005 | Ceiling Consumption Event and Ledger are separately defined and traceable. | Event-to-ledger transition matrix review. |
| CR-006 | Policy amendment/freeze lifecycle traces gates, SK, actors, evidence, version, and audit history. | Governance transition walkthrough against GOV-01–09. |
| CR-007 | Obligation and blocker are semantically distinct, sourced, and clearable by evidence. | Obligation/blocker lifecycle review. |
| CR-008 | Reconciliation, item, discrepancy, resolution, source, and closure links are explicit. | Reconciliation scenario walkthrough. |
| CR-009 | Commitment/advance references preserve Procurement ownership and do not invent accounting treatment. | Cross-module ownership and Finance treatment review. |
| CR-010 | Permission/role/SuperAdmin/authority/mandate/decision remain separate. | Authority model review and FIN-TEST-100–105 mapping. |
| CR-011 | Required conceptual ERDs exist; all edges map to REL IDs; no unsupported cardinality. | Mermaid render and edge-to-catalogue reconciliation. |
| CR-012 | Source-to-test traceability covers every critical entity/attribute/relationship/process. | Traceability coverage report. |
| CR-013 | Each integration contract identifies owner, canonical ID, event/version/freshness/correction/retry/failure/reconciliation. | Per-integration checklist. |
| CR-014 | Ledger event effects are separated; reservation/consumption/release/reversal do not double count. | Event matrix walkthrough. |
| CR-015 | Missing SOP/evidence is explicit; no unsupported rules are asserted. | Source inventory and rule-to-page check. |
| CR-016 | FIN-TEST-01–105 each map to requirements/entities/relationships/decisions with no execution claim. | Test ID integrity and traceability matrix. |
| CR-017 | Exact R02 file identity is confirmed. | Document control/file identity review. |
| CR-018 | Original Correction Register provenance/version is confirmed. | Side-by-side source register review. |

---

## 18. Correction Dependency Matrix

| Correction | Depends on | Can proceed before decisions? | Blocking note |
|---|---|---|---|
| CR-001 | Exact R02; domain sources | Partially | Catalogue structure can improve; ownership/evidence may remain pending. |
| CR-002 | CR-001; exact R02 | Partially | Candidate relationships can be enumerated; cardinality remains pending. |
| CR-003 | CR-002 | Yes, as documentation normalization | No decision needed to make IDs atomic. |
| CR-004 | CR-001/002; FIN-DEC-10/14 | Partially | Semantics can be clarified; cardinality cannot be finalized. |
| CR-005 | CR-001/002; FIN-DEC-07/31/32 | Partially | Ledger/event distinction can be documented; consuming event pending. |
| CR-006 | CR-001/002/010; GOV-01–09; FIN-DEC-16–24/29 | Partially | Governance must remain fixed; source mapping pending. |
| CR-007 | CR-001/002/008; FIN-DEC-16/18/29 | Partially | Concept separation can be documented; blocker rules pending. |
| CR-008 | CR-001/002/005; FIN-DEC-12/16/18/31 | Partially | Logical components can be described; status/accounting policy pending. |
| CR-009 | CR-001/002/013; FIN-DEC-13/14/31/32 | Partially | Ownership boundaries can be stated; accounting effects pending. |
| CR-010 | CR-001/002; FIN-DEC-19/20/22/33 | Partially | Concept separation can be documented; actual authority pending. |
| CR-011 | CR-001/002/003; exact R02 | Yes, after document source provided | Diagram edge mapping must be direct and auditable. |
| CR-012 | CR-001–011; FIN-TEST list | Partially | Mapping can be drafted; missing test detail remains unavailable. |
| CR-013 | CR-001/002/007/008; module contracts | Partially | Logical contract template can be completed; source states/freshness pending. |
| CR-014 | CR-005/008; FIN-DEC-07/08/09/12/31/32 | Partially | Event alternatives can be documented; no policy effect may be selected. |
| CR-015 | Missing SOP and Finance documents | No, for source completion | Explicit missing-source record can be maintained. |
| CR-016 | CR-001/002/012; FIN-TEST-01–105 source | Partially | IDs can be preserved; missing scenarios cannot be reconstructed. |
| CR-017 | Exact R02 file | No | Must supply exact target file. |
| CR-018 | Original Correction Register | No | Must supply original version or owner confirmation. |

---

## 19. Correction Status Dashboard

All statuses are initial statuses for the corrective-action plan. They do not claim that R02 has been corrected.

| CR ID | Severity | Priority | Initial status |
|---|---|---|---|
| CR-001 | CRITICAL | P0 | `BLOCKED_BY_MISSING_EVIDENCE` |
| CR-002 | CRITICAL | P0 | `OPEN` |
| CR-003 | HIGH | P0 | `OPEN` |
| CR-004 | CRITICAL | P0 | `BLOCKED_BY_ORG_DECISION` |
| CR-005 | CRITICAL | P0 | `BLOCKED_BY_ORG_DECISION` |
| CR-006 | CRITICAL | P0 | `BLOCKED_BY_MISSING_EVIDENCE` |
| CR-007 | HIGH | P1 | `BLOCKED_BY_ORG_DECISION` |
| CR-008 | HIGH | P1 | `OPEN` |
| CR-009 | HIGH | P1 | `BLOCKED_BY_MISSING_EVIDENCE` |
| CR-010 | CRITICAL | P0 | `BLOCKED_BY_MISSING_EVIDENCE` |
| CR-011 | HIGH | P0 | `BLOCKED_BY_MISSING_EVIDENCE` |
| CR-012 | HIGH | P1 | `OPEN` |
| CR-013 | HIGH | P1 | `OPEN` |
| CR-014 | CRITICAL | P0 | `BLOCKED_BY_ORG_DECISION` |
| CR-015 | HIGH | P1 | `BLOCKED_BY_MISSING_EVIDENCE` |
| CR-016 | HIGH | P1 | `BLOCKED_BY_MISSING_EVIDENCE` |
| CR-017 | HIGH | P0 | `BLOCKED_BY_MISSING_EVIDENCE` |
| CR-018 | MEDIUM | P1 | `BLOCKED_BY_MISSING_EVIDENCE` |

No item is `READY FOR RE-AUDIT`, `VERIFIED_CLOSED`, or `CLOSED` until corrections and evidence are available.

---

## 20. Re-Audit Readiness Criteria

R02 may be submitted for re-audit when:

1. Exact R02 target file is available and document control is consistent.
2. Original Correction Register source/version is available or its supplied text is formally confirmed as controlling.
3. CR-001 through CR-016 have revised locations and evidence.
4. Every Entity Catalogue entry maps to attributes or explicit external/derived/logical classification.
5. Every Relationship ID is atomic or has traceable atomic sub-edges.
6. Every ERD edge maps to Relationship ID.
7. Funding Allocation semantics are unambiguous as a candidate model, with FIN-DEC-10/14 still pending where applicable.
8. Ceiling Consumption Ledger, Cash Ledger, and Expenditure Ledger are separately defined.
9. Policy amendment/lock lifecycle is traceable without bypassing GOV-01–09.
10. Obligation and blocker semantics are separate.
11. Reconciliation components have ownership and source links.
12. Authority/IAM separation is explicit.
13. Integration contracts state source ownership and unresolved freshness/failure dependencies.
14. SOP and missing evidence are correctly identified.
15. FIN-TEST-01–105 remain intact and map to architecture without execution claims.
16. Every pending decision remains visibly pending.
17. No physical schema or implementation has been introduced.

Passing this gate means **ready for independent re-audit**, not final approval.

---

## 21. Final Recommendation

1. Preserve this Correction Register as the controlling plan for R02 corrections.
2. First obtain the exact R02_Version2 file and original Correction Register provenance (CR-017/018).
3. Complete P0 corrections before requesting re-audit.
4. Keep organizational and accounting decisions pending until appropriate evidence/authority is supplied.
5. Do not make R02.1, physical database design, or implementation part of this Correction Register task.
6. After R02 is corrected and evidence is attached, conduct independent re-audit against the acceptance criteria above.

### Current status

- R01: `NOT PASSED — CORRECTION REQUIRED` (per Correction Register basis).
- R02: awaits corrective actions and independent re-audit.
- Finance Logical Architecture Final: `BLOCKED`.
- Physical Database Design: `NO_GO`.
- Implementation: `NO_GO`.
- Code/database changes: none.

---

## 22. Final Instruction Compliance

- GOV-01–GOV-09 preserved.
- FIN-DEC-01–FIN-DEC-33 preserved.
- FIN-TEST-01–FIN-TEST-105 preserved.
- No decision or authority invented.
- No source evidence fabricated.
- No physical schema, SQL, migration, seed, API, or code created.
- No source file changed.
- No test executed or claimed as passed.

**End of Finance Correction Register R02 → R02.1.**