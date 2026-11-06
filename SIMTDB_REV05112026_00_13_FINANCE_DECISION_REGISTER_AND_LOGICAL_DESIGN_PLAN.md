# SIM-TDB — FINANCE DECISION REGISTER
## Agenda Klarifikasi dan Rencana Finalisasi Logical Design

**Document ID:** SIMTDB-REV05112026-00-13-FIN  
**Filename:** `SIMTDB_REV05112026_00_13_FINANCE_DECISION_REGISTER_AND_LOGICAL_DESIGN_PLAN.md`  
**Revision:** REV05112026  
**Status:** Draft untuk review pemilik proyek dan organisasi  
**Mode:** Governance dan logical-design planning — tanpa implementasi  
**Project:** Sistem Informasi Manajemen Tanggap Darurat Bencana (SIM-TDB)  
**Organization:** Caritas Keuskupan Malang — Tim Solidaritas Kemanusiaan Keuskupan Malang (TSKKM)

---

## 1. Tujuan

Dokumen ini melanjutkan hasil audit Finance dan menyediakan satu paket kerja untuk:

1. Memisahkan keputusan pemilik proyek yang sudah ditetapkan dari keputusan organisasi yang masih belum tersedia.
2. Membawa pertanyaan Finance ke forum klarifikasi tanpa mengubah SOP atau menciptakan kewenangan.
3. Mengatur urutan pekerjaan sebelum logical design Finance dinyatakan final.
4. Menetapkan bukti yang dibutuhkan agar setiap keputusan dapat ditelusuri.
5. Menjaga agar SIM-TDB mengikuti aturan organisasi, bukan memaksa organisasi mengikuti asumsi aplikasi.

Dokumen ini **bukan** implementasi, physical schema, atau persetujuan otomatis atas opsi yang tercantum.

---

## 2. Status dan sumber yang menjadi dasar

### 2.1 Materi yang digunakan

- Klarifikasi pemilik proyek tentang fleksibilitas nominal dan setup policy Finance.
- Klarifikasi pemilik proyek tentang governance Master Policy, freeze, SuperAdmin, dan SK Pengaturan.
- Prompt Finance 00_07 sampai 00_11 R01.
- Audit Prompt 00.12.
- Audit Finance 00_10 dan dokumen sebelumnya yang tersedia dalam percakapan.
- Gambar SOP halaman cetak 16–29 yang telah diunggah, terutama halaman 23–24.
- CHR-020 sebagaimana disampaikan sebelumnya.

### 2.2 Batas evidence

Audit sumber saat ini terbatas:

- SOP yang dapat ditelaah: gambar halaman cetak 16–29.
- SOP Finance lain, termasuk halaman 40–41, halaman 49, dan halaman 62–69: belum tersedia untuk pemeriksaan langsung.
- Repository, branch, commit, code, database, schema, dan test suite: tidak tersedia.
- Dokumen SK, mandat, delegation, approval matrix, dan bukti formal lainnya: belum tersedia dalam materi yang diperiksa.

Untuk semua hal yang belum diperiksa, gunakan `EVIDENCE_NOT_AVAILABLE`. Jangan menganggap sumber telah diverifikasi hanya karena namanya disebut dalam dokumen terdahulu.

---

## 3. Prinsip yang telah menjadi baseline

### 3.1 Klarifikasi kebijakan nominal dan mode

| Prinsip | Status | Batas penerapan |
|---|---|---|
| Rp100.000.000 yang tampil dalam contoh/template adalah ilustrasi; bukan default, mandatory amount, cap, atau approval threshold. | `CLARIFIED_BY_PROJECT_OWNER` | Jangan hardcode atau jadikan trigger sistem. |
| Rp50.000.000 adalah nilai referensi awal untuk ceiling dana darurat berdasarkan klarifikasi pemilik proyek sebelumnya. | `CLARIFIED_BY_PROJECT_OWNER` | Nilai aktif harus ditentukan melalui policy setup yang berwenang; bukan angka permanen di code. |
| Nilai ceiling dan aggregation mode dikelola melalui controlled policy setup. | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` | Setup dan amendment mengikuti governance yang telah diklarifikasi. |
| Pilihan mode mencakup `PER_INCIDENT` dan `GLOBAL_ALL_INCIDENTS`. | `CLARIFIED_BY_PROJECT_OWNER` | Makna tiap mode dan scope harus ditetapkan dalam konfigurasi yang sah. |
| General program/activity budgets tidak otomatis terkena emergency-fund ceiling. | `CLARIFIED_BY_PROJECT_OWNER` | Pembatasan sumber dana dan otorisasi lain tetap berlaku. |
| Kas eligible merupakan batas terpisah dari policy ceiling. | `CLARIFIED_BY_PROJECT_OWNER` | Definisi kas eligible dan sumber datanya masih perlu ditentukan. |

### 3.2 Governance Master Policy yang telah diklarifikasi pemilik proyek

Berikut bukan lagi pertanyaan untuk menerima atau menolak prinsip dasarnya:

| ID | Governance requirement | Status |
|---|---|---|
| GOV-01 | Master Policy ditetapkan sebelum program operasional dimulai. | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| GOV-02 | Tidak ada program operasional yang boleh aktif tanpa policy yang berlaku. | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| GOV-03 | Policy setup/amendment terkunci saat ada program yang berjalan atau belum resmi ditutup. | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| GOV-04 | Policy amendment juga terkunci sampai program dan seluruh keuangan terkait selesai. | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| GOV-05 | Hanya kapabilitas SuperAdmin yang dapat melakukan setup awal dan amendment yang memenuhi syarat. | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| GOV-06 | Setiap amendment memerlukan SK Pengaturan terlampir dengan detail yang dapat ditelusuri. | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| GOV-07 | SK Pengaturan tidak membypass program/financial closure gate. | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| GOV-08 | Tidak ada SuperAdmin override saat policy terkunci. | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |
| GOV-09 | Amendment menghasilkan versi policy baru; histori policy dan transaksi tidak ditimpa diam-diam. | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` |

Prinsip-prinsip ini telah ditetapkan pemilik proyek sebagai requirement desain SIM-TDB. Namun, itu **tidak membuktikan** bahwa SK tertentu telah diterbitkan, signatory telah diverifikasi, atau authority organisasi tertentu telah didokumentasikan.

---

## 4. Decision register — keputusan organisasi dan desain yang masih terbuka

### Status

- `PENDING_ORG_DECISION`: perlu keputusan atau bukti organisasi/pedoman Finance.
- `PENDING_DESIGN_DECISION`: perlu keputusan desain logical model yang tidak boleh diasumsikan.
- `BLOCKED_BY_MISSING_SOURCE`: sumber yang diperlukan belum tersedia.
- `PROJECT_OWNER_GOVERNANCE_REQUIREMENT`: prinsip sudah ditetapkan pemilik proyek dan tidak dibuka ulang dalam register pending.

| ID | Pertanyaan keputusan | Opsi untuk dibahas — bukan keputusan final | Dampak pilihan | Bukti yang dibutuhkan | Pemilik keputusan | Status | Menghambat finalisasi logical design? |
|---|---|---|---|---|---|---|---|
| FIN-DEC-01 | Bagaimana menafsirkan redaksi SOP halaman 23 tentang Rp50.000.000 bersama klarifikasi pemilik proyek bahwa nilainya merupakan ceiling per kejadian/operasi dan dapat diatur? | A. Klarifikasi menjadi interpretasi operasional resmi; B. klarifikasi berlaku sebagai policy sistem dengan keputusan formal terpisah; C. redaksi perlu revisi/penjelasan oleh authority SOP. | Menentukan cara requirement ditautkan ke SOP dan cara konflik dicatat. | SOP halaman 23 yang jelas; keputusan/interpretasi tertulis dari authority yang berwenang. | `OWNER TO BE DESIGNATED` | `SOURCE_CONFLICT` sampai direkonsiliasi | **Ya** |
| FIN-DEC-02 | Berapa nilai dan tanggal berlaku konfigurasi awal emergency-fund ceiling? | A. Rp50m sebagai reference awal setelah disahkan; B. nilai lain yang ditetapkan organisasi; C. policy awal belum aktif sampai keputusan tersedia. | Menentukan policy version pertama. | Decision basis dan effective date yang disetujui. | `OWNER TO BE DESIGNATED` | `PENDING_ORG_DECISION` | **Ya**, untuk aktivasi awal |
| FIN-DEC-03 | Mode agregasi awal mana yang dipilih? | A. `PER_INCIDENT`; B. `GLOBAL_ALL_INCIDENTS`. | Menentukan cara sistem mengagregasi penggunaan ceiling. | Keputusan policy sebelum program pertama aktif. | `OWNER TO BE DESIGNATED` | `PENDING_ORG_DECISION` | **Ya**, untuk aktivasi awal |
| FIN-DEC-04 | Pada `PER_INCIDENT`, apa control unit yang sah? | A. Satu real-world parent incident; B. formally independent response operation; C. unit lain yang ditetapkan organisasi. | Menentukan cap aggregation dan potensi anti-splitting. | Definisi incident/operation dan authority yang menetapkan hubungan. | `OWNER TO BE DESIGNATED` | `PENDING_ORG_DECISION` | **Ya** |
| FIN-DEC-05 | Pada `GLOBAL_ALL_INCIDENTS`, apa batas policy scope? | A. Satu emergency-response activation; B. satu response period; C. satu program/campaign; D. policy term lain. | Menentukan incident mana berbagi ceiling. | Decision record yang menyebut scope, waktu berlaku, dan keanggotaan. | `OWNER TO BE DESIGNATED` | `PENDING_ORG_DECISION` | **Ya** |
| FIN-DEC-06 | Bagaimana global scope berakhir, di-reset, atau diganti? | A. Tidak ada reset otomatis; B. scope baru hanya dengan policy version baru; C. aturan lain yang disahkan. | Mencegah reset implisit dan penghitungan kumulatif yang ambigu. | Policy decision dengan boundary dan effective dates. | `OWNER TO BE DESIGNATED` | `PENDING_ORG_DECISION` | **Ya** |
| FIN-DEC-07 | Event mana yang mengonsumsi ceiling? | A. Approval; B. cash reservation; C. payment instruction; D. cash release/disbursement; E. event lain yang disahkan. | Menentukan kapan sisa limit berubah dan bagaimana cancellation/retry ditangani. | Pedoman Finance/operasional dan keputusan yang menyebut event. | `OWNER TO BE DESIGNATED` | `PENDING_ORG_DECISION` | **Ya** |
| FIN-DEC-08 | Apa definisi eligible available emergency cash? | A. Saldo rekening yang memenuhi syarat; B. saldo dikurangi reserved/outstanding amounts; C. basis lain menurut Finance policy. | Menentukan global cash control dan risiko overspending. | Finance policy, cash records, dan restriction rules. | `OWNER TO BE DESIGNATED` | `PENDING_ORG_DECISION` | **Ya** |
| FIN-DEC-09 | Apa perlakuan reservations dan payment instructions yang belum selesai? | A. Mengurangi eligible cash sejak reservation; B. mengurangi pada event lain; C. belum dihitung sampai cash release, dengan kontrol lain. | Mempengaruhi available cash dan concurrency. | Finance policy yang menjelaskan reservation/outstanding payment. | `OWNER TO BE DESIGNATED` | `PENDING_ORG_DECISION` | **Ya** |
| FIN-DEC-10 | Apakah policy dapat menggunakan satu atau beberapa fund pools/sumber dana? | A. Satu fund pool per policy; B. beberapa pool; C. alokasi per request/expense; D. model lain. | Menentukan fund restrictions, cash aggregation, dan reporting. | Funding-source register dan Finance policy. | `OWNER TO BE DESIGNATED` | `PENDING_DESIGN_DECISION` / `PENDING_ORG_DECISION` | **Ya** |
| FIN-DEC-11 | Bagaimana restricted cash dipisahkan dari eligible cash? | A. Eligibility per fund source; B. eligibility per transaction/use; C. metode lain yang disahkan. | Mencegah dana terikat digabung dengan kas bebas. | Daftar restriction dan otoritas interpretasi. | `OWNER TO BE DESIGNATED` | `PENDING_ORG_DECISION` | **Ya** |
| FIN-DEC-12 | Apa sumber kanonis actual expenditure dan apa status Finance yang dapat dilaporkan? | A. sumber transaksi sesuai pedoman Finance; B. journal/expense record yang ditetapkan Finance; C. model lain. | Menentukan provenance laporan tanpa menyamakan payment dan expense recognition. | Finance policy dan model transaksi yang disetujui. | `OWNER TO BE DESIGNATED` | `PENDING_ORG_DECISION` | **Ya** |
| FIN-DEC-13 | Apa formula remaining budget dan apakah commitments diperhitungkan? | Opsi mencakup actual-only atau basis lain yang memasukkan commitments, PO, invoice, advances, reversals, dan cut-off. | Mempengaruhi laporan dan rekonsiliasi. | Pedoman accounting/Finance yang disahkan. | `OWNER TO BE DESIGNATED` | `PENDING_ORG_DECISION` | **Ya**, untuk angka definitif |
| FIN-DEC-14 | Bagaimana budget berelasi dengan Program, Activity, dan Budget Line? | A. budget di program; B. di activity; C. header + lines; D. kombinasi dengan aturan eksplisit. | Mempengaruhi foreign-key integrity, roll-up, revision, dan laporan. | Logical model Program/Activity yang disetujui. | `OWNER TO BE DESIGNATED` | `PENDING_DESIGN_DECISION` | **Ya** |
| FIN-DEC-15 | Apa lifecycle resmi budget revision? | Status kandidat dapat mencakup draft, review, approved, rejected, effective; jangan dianggap resmi sebelum disahkan. | Menentukan kapan revisi mengganti baseline aktif. | Finance workflow/pedoman yang disetujui. | `OWNER TO BE DESIGNATED` | `PENDING_ORG_DECISION` | **Ya** |
| FIN-DEC-16 | Kewajiban finansial apa yang memblokir policy amendment? | Minimal blocker dari governance requirement; detail kategori dan source-of-truth per blocker perlu ditetapkan. | Menentukan apakah policy lock gate dapat dievaluasi andal. | Daftar kewajiban, owner module, lifecycle, closure evidence. | `OWNER TO BE DESIGNATED` | `PENDING_ORG_DECISION` / `PENDING_DESIGN_DECISION` | **Ya** |
| FIN-DEC-17 | Status program mana yang dianggap running, closing, dan formally closed? | Mapping dari vocabulary program yang disetujui; status paused/on hold tetap belum closed menurut governance requirement. | Menentukan lock gate. | Program workflow/state register aktual. | `OWNER TO BE DESIGNATED` | `PENDING_DESIGN_DECISION` | **Ya** |
| FIN-DEC-18 | Siapa yang mengesahkan program dan financial closure? | A. Authority yang telah ditetapkan SOP/organisasi; B. pihak lain yang disahkan. | Menentukan bukti yang dapat membuka policy setup setelah seluruh gate terpenuhi. | Mandat/delegasi dan closure procedure. | `OWNER TO BE DESIGNATED` | `PENDING_ORG_DECISION` | **Ya** |
| FIN-DEC-19 | Siapa yang memverifikasi isi dan authority SK Pengaturan? | A. pemegang authority yang ditunjuk; B. proses verification lain yang disahkan. | Upload file saja tidak membuktikan authenticity atau relevansi. | Prosedur dan authority verification formal. | `OWNER TO BE DESIGNATED` | `PENDING_ORG_DECISION` | **Ya**, sebelum amendment bisa aktif |
| FIN-DEC-20 | Bagaimana SuperAdmin diangkat, diprovision, dipulihkan, dan dicabut? | Proses harus mengikuti account governance organisasi; detail belum tersedia. | Menentukan akses ke policy setup. | Prosedur user/account management yang disahkan. | `OWNER TO BE DESIGNATED` | `PENDING_ORG_DECISION` | **Ya**, sebelum operasional policy setup |
| FIN-DEC-21 | Apakah initial setup memerlukan SK khusus atau dapat memakai governing source lain yang telah diterima? | A. SOP/policy adopted; B. SK; C. dokumen lain yang disahkan. | Menentukan evidence initial policy. | Kebijakan governance yang berlaku. | `OWNER TO BE DESIGNATED` | `PENDING_ORG_DECISION` | **Ya**, sebelum policy awal aktif |
| FIN-DEC-22 | Apakah ada verifikator terpisah untuk amendment selain SuperAdmin? | A. SuperAdmin mengeksekusi berdasarkan SK; B. ada verification actor lain yang sah; C. mekanisme lain. | Menentukan segregation of duties dan authority. | Keputusan organisasi dan delegation matrix. | `OWNER TO BE DESIGNATED` | `PENDING_ORG_DECISION` | **Ya**, jika verification disyaratkan |
| FIN-DEC-23 | Policy version mana berlaku pada incident/program aktif saat policy berubah setelah gate terbuka? | A. referensi lama tetap; B. transaksi baru memakai versi baru; C. aturan transition lain yang disahkan. | Mencegah reinterpretasi transaksi dan stale policy. | Transition rule yang disetujui. | `OWNER TO BE DESIGNATED` | `PENDING_ORG_DECISION` | **Ya** |
| FIN-DEC-24 | Apa yang terjadi pada amendment future-dated jika program baru dimulai sebelum tanggal efektif? | Opsi: activation ditahan, program memakai policy lama, atau aturan lain yang disahkan. | Mencegah program mulai dengan policy yang ambigu. | Policy effective-date/activation rule. | `OWNER TO BE DESIGNATED` | `PENDING_DESIGN_DECISION` / `PENDING_ORG_DECISION` | **Ya** |
| FIN-DEC-25 | Apa otoritas offline untuk request, approval, dan disbursement? | Request capture offline dapat dipertimbangkan; approval/disbursement tidak diasumsikan dapat offline. | Menentukan field operation dan synchronization behavior. | Kebijakan operasional offline yang disahkan. | `OWNER TO BE DESIGNATED` | `PENDING_ORG_DECISION` | **Ya**, untuk offline workflow final |
| FIN-DEC-26 | Apa currency, precision, rounding, cut-off, dan kurs yang berlaku? | Mengikuti Finance policy; tidak ditentukan audit ini. | Mempengaruhi amount integrity dan reporting. | Finance policy dan keputusan platform saat waktunya. | `OWNER TO BE DESIGNATED` | `PENDING_ORG_DECISION` | **Ya**, sebelum physical design |
| FIN-DEC-27 | Bagaimana cardinality Program–Incident–Response Operation? | Satu/multiple hubungan hanya jika didukung source dan kebutuhan organisasi. | Menentukan policy binding, scope, dan anti-splitting. | Master workflow dan model Program/Incident yang disetujui. | `OWNER TO BE DESIGNATED` | `PENDING_DESIGN_DECISION` | **Ya** |
| FIN-DEC-28 | Apakah satu policy scope dapat mencakup beberapa program? | A. Satu scope per program; B. beberapa program berbagi scope; C. policy-specific rule lain. | Mempengaruhi global ceiling dan lock scope. | Keputusan policy scope. | `OWNER TO BE DESIGNATED` | `PENDING_DESIGN_DECISION` | **Ya** |
| FIN-DEC-29 | Bagaimana sistem bertindak jika modul sumber status/obligation unavailable atau datanya stale? | A. Fail closed; B. unresolved state yang tetap memblokir; C. opsi lain yang disahkan. | Mencegah sistem menyimpulkan gate clear dari data yang tidak tersedia. | SLA/freshness dan cross-module contract. | `OWNER TO BE DESIGNATED` | `PENDING_DESIGN_DECISION` | **Ya** |
| FIN-DEC-30 | Siapa dapat melihat lock eligibility report dan detail blocker? | Role/scope harus berdasarkan need-to-know; jangan membuka data finance sensitif secara luas. | Mempengaruhi keamanan dan privacy. | Access matrix dan data classification. | `OWNER TO BE DESIGNATED` | `PENDING_ORG_DECISION` | **Ya**, untuk report operasional |
| FIN-DEC-31 | Bagaimana menangani refund, reversal, correction, advance, dan disputed transactions terhadap cash dan ceiling ledger? | Tidak ada treatment yang dipilih dalam audit. | Mempengaruhi aggregate limit, cash availability, dan close gate. | Finance/accounting rules yang disahkan. | `OWNER TO BE DESIGNATED` | `PENDING_ORG_DECISION` | **Ya** |
| FIN-DEC-32 | Bagaimana expiry/cancellation reservation melepaskan capacity? | Harus mengikuti policy event yang disahkan; jangan lepaskan otomatis dengan asumsi. | Mempengaruhi available ceiling dan kas. | Reservation policy. | `OWNER TO BE DESIGNATED` | `PENDING_ORG_DECISION` | **Ya**, jika reservation dipakai |

### Catatan

Tabel ini tidak membuka ulang GOV-01 sampai GOV-09. Tabel hanya mencatat rincian yang dibutuhkan untuk menerjemahkan governance yang sudah disetujui menjadi desain yang dapat diuji dan tidak bertentangan dengan sumber organisasi.

---

## 5. Paket rapat klarifikasi

### 5.1 Tujuan rapat

Rapat bukan untuk memilih teknologi atau membangun aplikasi. Tujuannya adalah menyepakati keputusan dan bukti yang dibutuhkan untuk menyelesaikan logical Finance design.

### 5.2 Agenda yang disarankan

1. Konfirmasi arti per kejadian/operasi dan cakupan `PER_INCIDENT`.
2. Pilih mode policy awal: `PER_INCIDENT` atau `GLOBAL_ALL_INCIDENTS`.
3. Jika global, tetapkan policy scope dan reset/supersession rule.
4. Tetapkan event yang mengonsumsi ceiling.
5. Tetapkan cara menghitung eligible available cash.
6. Sepakati perlakuan reservations, outstanding payments, advances, refund, reversal, dan restricted funds.
7. Definisikan program closure dan financial closure serta sumber bukti masing-masing.
8. Petakan authority untuk:
   - Initial Master Policy source/approval.
   - SuperAdmin account provisioning.
   - SK Pengaturan verification.
   - Program closure certification.
   - Financial closure certification.
9. Rekonsiliasi redaksi SOP halaman 23 dengan klarifikasi pemilik proyek.
10. Konfirmasi hubungan Program–Incident–Response Operation–Policy Scope.
11. Tetapkan offline limitations yang berlaku untuk request, approval, dan disbursement.
12. Catat seluruh keputusan, sumber, tanggal, penerbit, scope, serta status.

### 5.3 Pertanyaan yang tidak boleh dijawab dengan asumsi teknis

- Apakah “operation” dapat memiliki cap terpisah dari parent incident?
- Apakah satu global cap berlaku per activation, periode, atau unit lain?
- Kapan request mulai mengonsumsi ceiling?
- Apa yang dimaksud kas darurat “tersedia”?
- Apakah reservation mengurangi cash availability?
- Siapa yang sah mengesahkan closure finansial?
- Siapa memverifikasi SK Pengaturan?
- Apakah suatu transaksi sudah termasuk actual expenditure?
- Apakah suatu restriction sumber dana berarti sistem harus hard-block?
- Apakah status program yang terlihat di aplikasi cukup untuk menutup policy gate?

---

## 6. Template pencatatan keputusan

Gunakan formulir pencatatan berikut untuk setiap keputusan yang diambil. Jangan mengisi contoh fiktif sebagai keputusan nyata.

| Field | Isi keputusan |
|---|---|
| Decision ID |  |
| Judul keputusan |  |
| Pertanyaan yang diputuskan |  |
| Opsi yang dipertimbangkan |  |
| Keputusan yang diambil |  |
| Alasan/rasional |  |
| Sumber SOP/halaman/section |  |
| Dokumen keputusan/mandat/SK |  |
| Nomor dokumen resmi |  |
| Tanggal dokumen |  |
| Penerbit/authority |  |
| Cakupan keputusan |  |
| Effective date |  |
| Pihak yang memutuskan |  |
| Pihak yang mencatat |  |
| Status verifikasi bukti |  |
| Dampak ke workflow |  |
| Dampak ke data/relasi |  |
| Dampak ke permission/authority |  |
| Dampak ke test cases |  |
| Related CHR/FIN issue |  |
| Status | `PENDING_ORG_DECISION` / `ORG_DECISION_CONFIRMED` / status yang relevan |
| Catatan/perubahan berikutnya |  |

### Persyaratan pencatatan

- `ORG_DECISION_CONFIRMED` hanya digunakan bila decision evidence yang relevan tersedia dan telah diverifikasi.
- Keputusan lisan atau catatan rapat tanpa authority dan dokumen yang diwajibkan tidak boleh otomatis dianggap keputusan final.
- Bila pemilik proyek menetapkan requirement desain tetapi belum ada keputusan organisasi formal, catat sesuai status project-owner governance, jangan naikkan menjadi keputusan organisasi.

---

## 7. Prioritas finalisasi logical Finance design

### Prioritas 0 — Pertahankan keputusan yang sudah disepakati

Jangan mengubah atau melemahkan:

- Configurable emergency-fund amount and aggregation mode.
- Pilihan mode `PER_INCIDENT` / `GLOBAL_ALL_INCIDENTS`.
- Policy ditetapkan sebelum program.
- Policy setup/amendment lock selama program berjalan/belum close.
- Program closure dan financial closure keduanya wajib.
- Hanya SuperAdmin menjalankan setup/amendment yang memenuhi syarat.
- SK Pengaturan wajib untuk amendment.
- SK tidak membypass lock.
- Tidak ada SuperAdmin override.
- Histori policy dan transaksi immutable dan traceable.

**Status:** `PROJECT_OWNER_GOVERNANCE_REQUIREMENT`.

### Prioritas 1 — Selesaikan policy semantics

Selesaikan:

- Initial mode.
- Control unit per incident.
- Global scope boundary.
- Ceiling-consumption event.
- Policy version binding.
- Effective-date transition.
- Pembatasan funding source.

**Status jika belum diputuskan:** `PENDING_ORG_DECISION` atau `PENDING_DESIGN_DECISION`.

### Prioritas 2 — Selesaikan cash and transaction semantics

Selesaikan:

- Fund source dan fund pool.
- Eligible cash basis.
- Reservation/outstanding payment treatment.
- Cash release/disbursement lifecycle.
- Actual expenditure recognition.
- Refund, reversal, advance, correction, dan disputed transactions.
- Remaining budget formula, bila diperlukan.

**Status jika belum diputuskan:** `PENDING_ORG_DECISION`.

### Prioritas 3 — Selesaikan closure gates dan cross-module data ownership

Untuk setiap blocker policy lock, tentukan:

| Aspek | Yang harus ditetapkan |
|---|---|
| Source module | Modul pemilik fakta |
| Canonical record | Entitas/record otoritatif |
| Blocking status | Status yang mengunci perubahan |
| Clearing event | Peristiwa yang membuat blocker selesai |
| Evidence | Dokumen/transaksi yang membuktikan selesai |
| Authority | Siapa yang mengesahkan closure |
| Freshness | Seberapa mutakhir data untuk dievaluasi |
| Failure behavior | Apa yang terjadi jika data tidak tersedia |
| Scope | Apakah blocker berlaku global atau hanya pada scope/fund pool terkait |

### Prioritas 4 — Finalisasi logical entities dan relationships

Setelah prioritas 1–3 didukung bukti/keputusan, finalisasi logical model untuk:

- Master Policy dan Policy Version.
- Program.
- Incident dan Response Operation.
- Policy Scope Instance.
- Fund Source dan Fund Pool.
- Fund Request.
- Approval Decision.
- Ceiling Consumption Ledger.
- Cash Movement Ledger.
- Payment Instruction dan Disbursement.
- Expense Recognition Reference.
- Refund/Reversal.
- Financial Reconciliation.
- SK/document reference.
- Audit Event.
- Idempotency/Correlation reference.

Tidak ada physical table, data type, SQL, atau migration pada tahap ini.

### Prioritas 5 — Uji kontrol melalui logical test cases

- Pertahankan FIN-TEST-01 sampai FIN-TEST-46.
- Pertahankan FIN-TEST-47 sampai set yang ditetapkan Prompt 00.11 R01.
- Jika daftar asli test tidak tersedia, tandai `EVIDENCE_NOT_AVAILABLE`; jangan membuat ulang seolah-olah sama.
- Tambahkan skenario baru hanya dengan ID baru dan alasan.
- Seluruh test belum dijalankan sampai ada bukti eksekusi nyata.

---

## 8. Kriteria hubungan data yang jelas

Logical design hanya dapat direview sebagai konsisten jika mampu menjawab, tanpa asumsi tersembunyi:

1. Policy version mana yang berlaku pada program/request/incident?
2. Bagaimana policy scope ditentukan dan dibuktikan?
3. Apa control unit yang digunakan dalam `PER_INCIDENT`?
4. Incident mana yang termasuk dalam `GLOBAL_ALL_INCIDENTS` scope?
5. Event apa yang menambah, menahan, mengurangi, atau melepaskan konsumsi ceiling?
6. Bagaimana konsumsi ceiling ditautkan ke request, approval, cash event, dan disbursement?
7. Bagaimana reservation dikonversi tanpa double count?
8. Bagaimana cash movement ditautkan ke fund pool dan restriction?
9. Bagaimana refund/reversal merujuk transaksi asal?
10. Bagaimana program closure dan financial closure diturunkan dari canonical records?
11. Apa yang terjadi jika salah satu modul sumber tidak tersedia atau statusnya stale?
12. Bagaimana setiap angka laporan ditelusuri ke transaksi/ledger sumber?
13. Bagaimana policy amendment mempertahankan old/new version dan bukti SK?
14. Bagaimana duplicate request/incident ditangani tanpa automatic deletion atau silent merge?
15. Bagaimana sistem membuktikan bahwa tidak ada amendment saat program atau financial obligation masih terbuka?

Jika salah satu jawaban belum tersedia, tandai secara eksplisit sebagai pending dan jangan menyamarkan kekurangan sebagai keputusan teknis.

---

## 9. Kriteria kontrol transaksi yang dapat diuji

Sebelum logical Finance design final, setiap kontrol harus memiliki:

| Elemen uji | Keterangan |
|---|---|
| Invariant | Aturan yang harus selalu benar |
| Actor/context | Siapa melakukan tindakan dan scope apa |
| Preconditions | Status, policy version, authority, cash, evidence |
| Transaction boundary | Kapan perubahan menjadi efektif |
| Idempotency identity | Cara mengenali retry yang sama |
| Concurrency case | Perilaku jika tindakan bersamaan |
| Failure case | Timeout, attachment failure, module unavailable |
| Audit evidence | Catatan actor, event, policy, source, timestamp |
| Recovery | Cara melanjutkan tanpa duplicate atau overwrite |
| Expected result | Hasil yang dapat diperiksa |
| Actual result | “Not executed” sampai ada evidence |

### Invariant minimum yang perlu dipertahankan

- Tidak ada program aktif tanpa policy version valid.
- Tidak ada policy amendment selama salah satu closure gate belum clear.
- Tidak ada SK yang melewati policy lock.
- Tidak ada non-SuperAdmin policy amendment.
- Tidak ada policy value atau mode yang diubah dengan overwrite versi lama.
- Tidak ada request/disbursement mengonsumsi ceiling lebih dari sekali karena retry.
- Tidak ada concurrent request yang memakai cash atau ceiling yang sama dua kali.
- Tidak ada report actual yang berbeda dari sumber transaksi tanpa discrepancy trace.
- Tidak ada cash dari fund pool restricted yang dianggap eligible tanpa rule yang sah.
- Tidak ada program/finance closure yang disimpulkan dari satu status umum saja.
- Tidak ada test yang dinyatakan lulus tanpa evidence eksekusi.

Status untuk invariant yang perlu implementasi: belum diuji; test design saja.

---

## 10. Checklist review logical design

### Governance

- [ ] Semua project-owner governance requirements termuat dengan provenance yang benar.
- [ ] Tidak ada governance requirement yang sudah disetujui dibuka ulang sebagai pending owner acceptance.
- [ ] Keputusan organisasi formal dibedakan dari project-owner requirement.
- [ ] SK Pengaturan amendment tetap mandatory menurut requirement pemilik proyek.
- [ ] Tidak ada SuperAdmin override.
- [ ] SuperAdmin tetap technical capability, bukan role organisasi kelima.

### Policy

- [ ] Policy amount/mode/scope configurable, bukan hardcoded.
- [ ] Policy version memiliki effective date dan audit trail.
- [ ] `PER_INCIDENT` dan `GLOBAL_ALL_INCIDENTS` tidak diterapkan sekaligus tanpa persetujuan.
- [ ] Scope, reset, dan policy transition tidak diasumsikan.
- [ ] Policy baru tidak menafsirkan ulang transaksi historis.
- [ ] Program tidak dapat aktif tanpa active policy.

### Finance

- [ ] Budget, ceiling, cash, commitment, payment, disbursement, expense recognition, dan remaining budget dibedakan.
- [ ] Fund source, fund pool, cash account, restricted cash, dan eligible cash dibedakan.
- [ ] Ceiling ledger dan cash movement ledger dipisahkan.
- [ ] Actual amount memiliki satu canonical source yang disetujui.
- [ ] Reservation conversion tidak double count.
- [ ] Refund/reversal tetap tertaut pada event asal.
- [ ] Tidak ada formula remaining budget yang dibuat tanpa policy.

### Relationships and integration

- [ ] Program–Incident–Response Operation cardinality tidak dipaksakan tanpa sumber.
- [ ] Fund Request memiliki relasi yang dapat ditelusuri ke program/incident/operation sesuai policy.
- [ ] Policy Scope Instance memiliki membership rules yang jelas.
- [ ] Setiap consumption event memiliki policy version dan source event reference.
- [ ] Closure gate mengambil data dari source module yang tepat.
- [ ] Tidak ada policy copy yang dapat diedit bebas di modul lain.

### Tests and evidence

- [ ] FIN-TEST-01 sampai 46 dipertahankan atau dinyatakan tidak tersedia.
- [ ] Tes governance dan lock gate tercakup.
- [ ] Tes idempotency, concurrency, offline, retry, refund, dan reconciliation tersedia.
- [ ] Semua hasil yang belum dijalankan berstatus `TEST_DESIGNED` atau blocked.
- [ ] Bukti sumber SOP dan keputusan organisasi terhubung ke requirement.

---

## 11. Readiness assessment

| Area | Status | Alasan |
|---|---|---|
| Klarifikasi nominal dan konfigurabilitas policy | `READY` | Nilai contoh, reference amount, dan opsi mode telah dinyatakan oleh pemilik proyek. |
| Governance freeze, finance closure gate, SuperAdmin-only, mandatory SK, no override | `READY` sebagai project-owner requirements | High-level rule sudah ditetapkan pemilik proyek; details/evidence tetap perlu dilengkapi. |
| Rekonsiliasi SOP halaman 23 | `BLOCKED_BY_MISSING_SOURCE` / `SOURCE_CONFLICT` | Gambar tersedia, tetapi perlu interpretasi tertulis terhadap perbedaan wording dengan klarifikasi. |
| Initial policy amount/mode/effective date | `BLOCKED` | Tidak boleh mengarang konfigurasi aktif. |
| `PER_INCIDENT` control unit | `BLOCKED` | Incident versus operation belum ditentukan. |
| `GLOBAL_ALL_INCIDENTS` scope/reset | `BLOCKED` | Batas scope dan reset belum diputuskan. |
| Program closure mapping | `BLOCKED_BY_MISSING_SOURCE` | State vocabulary/source records belum tersedia. |
| Financial closure mapping | `BLOCKED_BY_MISSING_POLICY` | Obligations, canonical records, dan certifying authority belum ditentukan. |
| SK Pengaturan workflow | `CONDITIONAL` | Requirement amendment sudah jelas; actual SK dan authority verification workflow belum tersedia. |
| SuperAdmin governance | `CONDITIONAL` | Capability requirement jelas; account provisioning, recovery, dan revocation evidence pending. |
| Ceiling consumption semantics | `BLOCKED` | Event yang mengonsumsi ceiling belum diputuskan. |
| Eligible cash model | `BLOCKED` | Cash source, restrictions, reservations, outstanding payment, dan formula belum jelas. |
| Actual expenditure source of truth | `BLOCKED_BY_MISSING_SOURCE` | Model Finance aktual dan pedoman pengakuan tidak tersedia. |
| Logical relationships | `CONDITIONAL` | Kandidat entitas dapat ditinjau; cardinality kritis belum ditetapkan. |
| Transaction-control test design | `CONDITIONAL` | Banyak skenario dirancang; policy dependencies tetap ada. |
| Test execution | `BLOCKED_BY_MISSING_SOURCE` | Tidak ada aplikasi/test environment/evidence. |
| Repository/code/database audit | `BLOCKED_BY_MISSING_SOURCE` | Repository dan artefak teknis tidak tersedia. |
| Finance logical design final | `BLOCKED` | Keputusan policy, cash, closure, control unit, dan event semantics belum selesai. |
| Physical database design | `NO_GO` | Belum ada persetujuan logical design final dan bukti policy critical. |
| Development/implementation | `NO_GO` | Tidak diminta dan tidak dilakukan. |

### Kesimpulan readiness

- **Logical design workshop:** `CONDITIONAL` — dapat dilakukan untuk menyepakati hubungan dan decision options, tanpa mengunci hal yang belum diputuskan.
- **Finance logical design final:** `BLOCKED` sampai keputusan kritis dan evidence tersedia.
- **Physical database design:** `NO_GO`.
- **Implementation:** `NO_GO`.

---

## 12. Tahapan lanjutan yang disarankan

1. **Rapat keputusan policy dan Finance**
   - Gunakan FIN-DEC-01 sampai FIN-DEC-32.
   - Bedakan keputusan yang sudah disetujui pemilik proyek dari keputusan organisasi yang masih perlu authority/evidence.
2. **Kumpulkan sumber formal**
   - SOP lengkap yang relevan.
   - SK/decision basis yang benar-benar tersedia.
   - Mandat/delegation dan approval matrix.
   - Finance policy dan sumber transaksi yang berlaku.
3. **Susun source/status mapping**
   - Program states.
   - Finance obligation states.
   - Closure evidence.
   - Canonical source modules.
4. **Finalisasi logical relationship**
   - Policy, scope, program, incident/operation, request, ceiling ledger, cash ledger, disbursement, expense, reconciliation.
5. **Perbarui requirement traceability dan CHR**
   - Jangan menghapus isu lama; update hanya dengan bukti keputusan yang tercatat.
6. **Lengkapi test plan**
   - Pastikan seluruh FIN test ID tersedia dan tidak ada yang diklaim pass tanpa eksekusi.
7. **Review dan persetujuan logical Finance design**
   - Setelah semua blocker ditangani, lakukan review lintas Finance, Program, Incident, Procurement, Inventory, Core/IAM, dan governance.
8. **Baru setelah persetujuan logical design**
   - Pertimbangkan physical database design dalam fase terpisah.
   - Tidak ada database atau aplikasi yang dibangun melalui dokumen ini.

---

## 13. Pernyataan akhir

Tujuan SIM-TDB adalah aplikasi yang fleksibel, tetapi tetap memiliki kontrol, integritas data, dan akuntabilitas. Prinsip utamanya adalah **aplikasi mengikuti aturan organisasi**.

Karena itu:

- Aturan yang sudah ditetapkan pemilik proyek harus diterapkan konsisten sebagai requirement desain.
- Detail yang belum ditetapkan harus ditampilkan sebagai opsi dan keputusan yang perlu dibuktikan.
- Aplikasi tidak boleh mengarang authority, accounting policy, scope, closure status, atau event semantics.
- Lock gate harus bersumber dari canonical records dan status yang disetujui.
- SK Pengaturan wajib untuk amendment sesuai requirement pemilik proyek, tetapi dokumen nyata dan authority-nya tetap harus diverifikasi.
- Tidak ada code/database yang diubah.
- Tidak ada test yang dijalankan atau dinyatakan lulus.

**Status dokumen:** Draft decision register dan logical-design plan untuk review.  
**Finance logical design final:** `BLOCKED` sampai keputusan kritis dan bukti sumber tersedia.  
**Physical database design:** `NO_GO`.  
**Implementation:** Tidak dilakukan.