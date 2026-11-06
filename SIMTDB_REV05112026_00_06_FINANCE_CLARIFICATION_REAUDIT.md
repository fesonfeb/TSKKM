# SIM-TDB — RE-AUDIT KLARIFIKASI FINANCE
## Audit Substantif, Rekonsiliasi Requirement, dan Rancangan Pengujian

**Document ID:** SIMTDB-REV05112026-00-06-FIN  
**Filename:** `SIMTDB_REV05112026_00_06_FINANCE_CLARIFICATION_REAUDIT.md`  
**Revision:** REV05112026  
**Status:** Draft untuk review pemilik proyek  
**Mode:** Audit dokumen dan test design saja — tanpa implementasi  
**Project:** Sistem Informasi Manajemen Tanggap Darurat Bencana (SIM-TDB)  
**Organization:** Caritas Keuskupan Malang — Tim Solidaritas Kemanusiaan Keuskupan Malang (TSKKM)

---

## 1. Executive Summary

Audit ini menelaah klarifikasi pemilik proyek tentang nominal Rp50.000.000 dan Rp100.000.000, instruksi re-audit Finance, hasil audit prompt sebelumnya, dan gambar SOP TSKKM yang tersedia.

### Kesimpulan

1. **Klarifikasi nominal:** `CLARIFIED_BY_PROJECT_OWNER`. Rp50.000.000 dan Rp100.000.000 adalah contoh nilai; bukan nominal baku, plafon tetap, batas maksimal pengeluaran, default wajib, atau approval threshold otomatis.
2. **Finance business rules:** klarifikasi nominal dapat diterapkan pada spesifikasi. Namun, aturan lifecycle, model entitas, pengakuan pengeluaran, kardinalitas sumber dana, dan rumus remaining budget belum seluruhnya disahkan.
3. **SOP evidence:** gambar halaman cetak 23–24 memberikan bukti parsial terkait sumber dana, persetujuan dana awal oleh Ketua TSKKM, serta larangan penggunaan dana APP Nasional untuk biaya kantor tertentu. Halaman finance dan procurement lain belum tersedia untuk audit.
4. **Source of truth actual expenditure:** materi tersedia belum menunjukkan model Finance aktual atau repository. Karena itu, sumber kanonis yang sudah diterapkan **belum dapat diverifikasi**. Rekomendasi desain adalah satu sumber transaksi Finance kanonis dan angka laporan diturunkan darinya.
5. **Kewenangan persetujuan:** fleksibilitas nominal tidak mengubah kewenangan persetujuan. Identitas dan relasi formal antara Ketua TSKKM, Romo Direktur Caritas, Koordinator, serta fungsi operasional tetap harus diverifikasi.
6. **Pengujian:** seluruh 23 skenario adalah rancangan. Tidak ada migration, seed, integration test, database test, atau test suite yang dijalankan.
7. **Kesiapan:** `BLOCKED` untuk finalisasi logical Finance design karena model aktual expenditure, otoritas approval, funding cardinality/restrictions, relasi Program–Activity–Budget, lifecycle revisi, dan basis remaining budget belum lengkap atau belum disahkan.

### Keputusan audit

- **PASS** untuk interpretasi pemilik proyek bahwa dua nominal tersebut hanya ilustrasi.
- **CONDITIONAL** untuk rancangan business rules dan target Source of Truth.
- **BLOCKED** untuk mengklaim bahwa repository, code, database, atau implementasi Finance telah diaudit.
- **BLOCKED** untuk physical schema dan implementation.

---

## 2. Scope dan Batasan

Audit dilakukan secara read-only atas materi yang tersedia di percakapan. Tidak ada akses repository atau workspace yang diberikan.

Audit ini tidak:

- Mengubah code, file proyek, configuration, database, schema, atau data.
- Menjalankan migration, seed, integration test, database test, atau command yang dapat mengubah proyek/lingkungan.
- Membuat tabel fisik, API, atau aplikasi.
- Mengklaim code atau test suite telah lulus.
- Menetapkan kebijakan akuntansi, pejabat approval baru, atau formula anggaran.
- Menganggap seluruh SOP telah diperiksa.

Gambar SOP yang tersedia sebelumnya memperlihatkan halaman cetak **16–29**. Bagian yang relevan untuk Finance pada audit ini terutama halaman 23–24. Halaman finance/procurement dan template lain yang tidak tersedia dicatat sebagai `EVIDENCE_NOT_AVAILABLE`.

---

## 3. Source Inventory dan Evidence Availability

| Source ID | Sumber | Status pemeriksaan | Cakupan dan batas |
|---|---|---|---|
| SRC-00-02 | `SIMTDB_REV05112026_00_02_FINANCIAL_AMOUNT_CLARIFICATION.md` | Teks diberikan dalam percakapan; dibaca | Klarifikasi pemilik proyek tentang nilai contoh dan aturan anggaran. |
| SRC-00-03 | `SIMTDB_REV05112026_00_03_FINANCE_CLARIFICATION_REAUDIT_AND_TEST_PROMPT.md` | Teks diberikan dalam percakapan; dibaca | Instruksi re-audit awal dan test design; bukan bukti hasil eksekusi. |
| SRC-00-04 | `SIMTDB_REV05112026_00_04_AUDIT_FINANCE_REAUDIT_PROMPT.md` | Teks audit prompt diberikan dalam percakapan; dibaca | Review kualitas prompt; bukan audit aplikasi atau database. |
| SRC-00-05 | `SIMTDB_REV05112026_00_05_FINANCE_REAUDIT_PROMPT_R01.md` | Teks diberikan dalam percakapan; dibaca | Prompt utama re-audit Finance yang dikendalikan addendum. |
| SRC-GUARDRAIL | Addendum Audit Execution Control | Teks diberikan dalam percakapan; dibaca | Mengatur read-only, provenance, source coverage, dan file output. |
| SRC-SOP-16-29 | Gambar SOP halaman cetak 16–29 | Gambar tersedia dan telah ditelaah | Halaman 23–24 relevan untuk sumber dana dan pembatasan APP Nasional; kualitas gambar membatasi transkripsi detail tabel lain. |
| SRC-SOP-40-41 | SOP Finance halaman 40–41 | `EVIDENCE_NOT_AVAILABLE` | Materi proyek sebelumnya merujuk halaman ini, tetapi gambar halaman tidak tersedia untuk audit ini. |
| SRC-SOP-49 | Template Permohonan Dana Darurat APP-KWI halaman 49 | `EVIDENCE_NOT_AVAILABLE` | Tidak tersedia; tidak menarik kesimpulan tentang field/template dari sumber primer. |
| SRC-SOP-62-69 | SOP Procurement/Finance dan dokumen terkait | `EVIDENCE_NOT_AVAILABLE` | Tidak tersedia untuk pemeriksaan langsung dalam audit ini. |
| SRC-PHASE-0.1D | Phase 0.1D — Procurement, Finance & Logistics | Teks spesifikasi diberikan sebelumnya | Materi kerja lama; bukan pengganti SOP dan bukan bukti implementasi. |
| SRC-CHR-020 | CHR-020 — sumber dana dan nominal Rp50 juta/Rp100 juta | Teks CHR diberikan sebelumnya | Status lama perlu diperbarui hanya untuk makna nominal; bagian lain tidak otomatis selesai. |
| SRC-REPO | Repository aplikasi | `EVIDENCE_NOT_AVAILABLE` | URL/akses repository tidak disediakan. Tidak ada branch, commit, file, atau code yang dapat diperiksa. |
| SRC-DB | Database, schema, migration, seed | `EVIDENCE_NOT_AVAILABLE` | Tidak ada akses database atau artefak schema. |
| SRC-TEST | Test suite atau hasil test aktual | `EVIDENCE_NOT_AVAILABLE` | Tidak ada test run atau evidence eksekusi yang diberikan. |

### Pernyataan coverage

Audit ini menggunakan file `00_02`, `00_03`, `00_04`, `00_05`, addendum guardrails, serta SOP halaman 16–29 yang tersedia. Audit **tidak** menganggap halaman SOP 1–95, repository, database, atau test suite telah diperiksa.

---

## 4. Source Hierarchy dan Provenance

Urutan sumber yang digunakan:

1. Klarifikasi langsung pemilik proyek dalam instruksi `00_02` dan addendum.
2. SOP asli yang tersedia dan dapat dibaca.
3. Keputusan organisasi formal yang dapat diidentifikasi.
4. Requirement proyek lain yang secara eksplisit diterima pemilik proyek.
5. Spesifikasi, prompt, dan audit terdahulu.
6. Rekomendasi teknis audit.

### Status provenance

| Label | Makna dalam dokumen ini |
|---|---|
| `SOP_CONFIRMED` | Didukung langsung oleh SOP asli yang telah diperiksa. |
| `CLARIFIED_BY_PROJECT_OWNER` | Dinyatakan langsung oleh pemilik proyek dan dapat ditelusuri pada klarifikasi yang diberikan. |
| `ORG_DECISION_CONFIRMED` | Didukung keputusan organisasi formal yang dapat diidentifikasi. |
| `PROJECT_REQUIREMENT_STATED_IN_ADDENDUM` | Tertulis dalam addendum, tetapi bukti penerimaan/otorisasi terpisah belum jelas. |
| `PENDING_OWNER_ACCEPTANCE` | Memerlukan penerimaan eksplisit pemilik proyek. |
| `TECHNICAL_RECOMMENDATION` | Rekomendasi teknis, bukan kebijakan SOP/organisasi. |
| `PENDING_DESIGN_DECISION` | Memerlukan keputusan desain domain/arsitektur. |
| `PENDING_ORG_DECISION` | Memerlukan keputusan organisasi atau pedoman Finance. |
| `SOURCE_CONFLICT` | Sumber yang tersedia berbeda atau belum terselaraskan. |
| `EVIDENCE_NOT_AVAILABLE` | Bukti tidak tersedia. |
| `TEST_DESIGNED` | Skenario tes dirancang, belum dijalankan. |
| `TEST_EXECUTED_PASS` | Hanya untuk tes yang benar-benar dijalankan dan memiliki evidence. |
| `TEST_EXECUTED_FAIL` | Hanya untuk tes yang benar-benar dijalankan dan memiliki evidence. |
| `BLOCKED_BY_MISSING_POLICY` | Tidak dapat diselesaikan karena policy belum disahkan. |
| `BLOCKED_BY_MISSING_SOURCE` | Tidak dapat diselesaikan karena sumber belum tersedia. |

Tidak ada test dalam audit ini yang berstatus `TEST_EXECUTED_PASS` atau `TEST_EXECUTED_FAIL`.

---

## 5. Owner Clarification Register

| ID | Pernyataan | Status | Batas interpretasi |
|---|---|---|---|
| OCL-01 | Rp50.000.000 dan Rp100.000.000 dalam contoh/ilustrasi bukan nilai baku, plafon, batas maksimal pengeluaran, default wajib, atau approval threshold otomatis. | `CLARIFIED_BY_PROJECT_OWNER` | Berlaku untuk interpretasi dua nominal tersebut; tidak mengubah authority. |
| OCL-02 | Anggaran dapat disesuaikan dengan kebutuhan program/kegiatan, kondisi bencana, sumber pendanaan, dan anggaran yang disetujui. | `CLARIFIED_BY_PROJECT_OWNER` | Tidak berarti anggaran dapat dibelanjakan tanpa persetujuan yang berlaku. |
| OCL-03 | Proposed budget, approved budget, budget revision, actual expenditure, dan remaining budget harus dibedakan. | `CLARIFIED_BY_PROJECT_OWNER` | Kebutuhan pemisahan dinyatakan; bentuk entitas, status, dan workflow fisik tetap perlu desain. |
| OCL-04 | Perubahan anggaran harus memiliki riwayat, alasan, aktor, waktu, dan referensi persetujuan. | `CLARIFIED_BY_PROJECT_OWNER` | Otoritas, status revisi, dan proses persetujuan tidak ditetapkan oleh klarifikasi. |
| OCL-05 | Setiap sumber pendanaan harus dapat ditelusuri. | `CLARIFIED_BY_PROJECT_OWNER` | Tidak menetapkan cardinality sumber pendanaan maupun aturan alokasinya. |
| OCL-06 | Otorisasi harus tetap mengikuti kewenangan organisasi yang telah diverifikasi. | `CLARIFIED_BY_PROJECT_OWNER` | Tidak mengidentifikasi pejabat approval untuk setiap tahap Finance. |
| OCL-07 | Nominal pada transaksi dan laporan harus berasal dari data keuangan aktual yang tercatat dan disahkan. | `CLARIFIED_BY_PROJECT_OWNER` | Tidak mendefinisikan status transaksi atau aturan accounting recognition. |

### Interpretasi yang dilarang

Klarifikasi tersebut **tidak** berarti:

- Batas kewenangan Ketua TSKKM berubah.
- Ketua TSKKM atau pejabat mana pun memperoleh kewenangan baru.
- Semua nominal dapat disetujui oleh pihak mana pun.
- Threshold formal yang disahkan di masa depan dilarang.
- Remaining budget dapat dihitung tanpa policy accounting.
- Nilai contoh boleh digunakan sebagai default untuk memudahkan penggunaan aplikasi.

---

## 6. SOP Finance Evidence Ledger

| Ref | Isi sumber yang terlihat atau tersedia | Interpretasi proses bisnis | Implikasi sistem | Batas/pending |
|---|---|---|---|---|
| SOP halaman 23 | Sumber pendanaan mencakup dana siaga dan dana operasional Keuskupan Malang, dana APP Nasional, serta bantuan umat. | Sumber dana yang disebut SOP perlu dibedakan dan dilacak. | Catatan anggaran/transaksi perlu merujuk sumber dana yang relevan. | Kategori lengkap, owner master, dan aturan pencampuran dana belum dapat disimpulkan dari halaman ini saja. |
| SOP halaman 23 | Dana siaga digunakan sebagai sumber pendanaan untuk respons awal tanggap darurat. | Dana siaga memiliki tujuan penggunaan sebagaimana teks yang terlihat. | Data sumber dana dan relasi ke kegiatan/transaksi perlu dapat ditelusuri. | Detail pengakuan dan proses accounting belum tersedia. |
| SOP halaman 23 | Dana tersebut hanya dapat dikeluarkan atas persetujuan Ketua TSKKM. | Pengeluaran dana siaga memerlukan persetujuan yang disebut sumber. | Sistem perlu merekam bukti approval dan aktor/authority yang relevan setelah pemetaan resmi. | Identitas, delegasi, dan relasi Ketua TSKKM dengan role sistem belum diverifikasi. |
| SOP halaman 23 | Contoh/angka Rp50.000.000 tercantum pada konteks dana awal. | Setelah klarifikasi pemilik proyek, nominal ini diperlakukan sebagai contoh, bukan cap atau batas. | Tidak boleh menjadi hardcode, default wajib, cap, atau threshold approval. | Makna contoh: `CLARIFIED_BY_PROJECT_OWNER`. |
| SOP halaman 24 | Dana darurat APP Nasional dapat diakses melalui KARINA-KWI dengan mengirim SITREP dan rencana penggunaan anggaran. | Akses pendanaan APP Nasional memiliki dokumen pendukung yang disebut pada halaman tersebut. | Dukungan relasi ke SITREP dan rencana penggunaan anggaran mungkin diperlukan. | Detail template, approval, dan tahapan tidak boleh disimpulkan tanpa halaman/form lengkap. |
| SOP halaman 24 | Dana APP Nasional tidak digunakan untuk biaya administrasi/operasional kantor yang dirinci pada halaman itu: gaji staf, perawatan gedung, perlengkapan/alat tulis kantor, perawatan harian kendaraan kantor, komunikasi harian kantor/staf, serta alkohol/minuman keras, rokok, dan minuman suplemen. | Terdapat pembatasan penggunaan sumber dana yang terlihat pada halaman 24. | Sistem dapat perlu menyimpan restriction/reference yang dapat ditelusuri. | Jangan membuat automatic blocking sebelum teks penuh, kategori expense, pengecualian, dan interpretasi yang berwenang diverifikasi. |
| SOP halaman 24 | Pada skala besar, Gereja Katolik Keuskupan Malang dapat menerima asistensi program dan dana Caritas Internationalis yang difasilitasi KARINA-KWI. | Sumber/dukungan tambahan disebut untuk kondisi skala besar. | Sumber pendanaan dan dokumen pendukung mungkin perlu dihubungkan. | Definisi skala besar dan workflow akses tidak ditetapkan oleh halaman ini saja. |
| SOP halaman 24 | Sumbangan pihak ketiga dapat diterima bila tidak terikat dan sesuai norma/nilai Gereja Katolik. | Penerimaan sumber pihak ketiga memiliki syarat pada teks SOP. | Sistem perlu provenance sumber donasi bila modul Finance mendukungnya. | Prosedur pemeriksaan, penerimaan, dan otoritas belum terverifikasi. |
| SOP halaman 49 | Template permohonan dana APP-KWI disebut di materi terdahulu dengan angka Rp100.000.000. | Halaman/template primer tidak tersedia dalam audit ini. | Jangan membangun rule atau template berdasarkan klaim belum diverifikasi. | `EVIDENCE_NOT_AVAILABLE`; nominal contoh ditafsirkan sesuai klarifikasi pemilik proyek. |

**Catatan kutipan:** ringkasan di atas merupakan parafrasa atas bagian yang tampak pada gambar halaman 23–24; bukan transkripsi lengkap atau verifikasi OCR. Untuk penerapan sebagai persyaratan final, perlu pemeriksaan scan halaman yang tajam dan dokumen SOP lengkap.

---

## 7. Corrected Financial Business Rule Register

| Rule ID | Business rule | Provenance | Status |
|---|---|---|---|
| FIN-BR-01 | Rp50.000.000 dan Rp100.000.000 dalam contoh/ilustrasi bukan nilai baku, plafon tetap, batas maksimal pengeluaran, default wajib, atau approval threshold otomatis. | Klarifikasi pemilik proyek | `CLARIFIED_BY_PROJECT_OWNER` |
| FIN-BR-02 | Sistem tidak boleh hardcode kedua nominal sebagai cap, default wajib, atau approval threshold. | Klarifikasi pemilik proyek | `CLARIFIED_BY_PROJECT_OWNER` |
| FIN-BR-03 | Besaran anggaran dapat bervariasi berdasarkan kebutuhan program/kegiatan, kondisi bencana, sumber pendanaan, dan anggaran yang disetujui. | Klarifikasi pemilik proyek | `CLARIFIED_BY_PROJECT_OWNER` |
| FIN-BR-04 | Proposed budget, approved budget, budget revision, actual expenditure, dan remaining budget harus dibedakan. | Klarifikasi pemilik proyek | `CLARIFIED_BY_PROJECT_OWNER` |
| FIN-BR-05 | Perubahan anggaran harus memiliki riwayat, alasan, aktor, waktu, dan referensi persetujuan. | Klarifikasi pemilik proyek | `CLARIFIED_BY_PROJECT_OWNER` |
| FIN-BR-06 | Setiap sumber pendanaan harus dapat ditelusuri. | Klarifikasi pemilik proyek | `CLARIFIED_BY_PROJECT_OWNER` |
| FIN-BR-07 | Otorisasi dan pejabat persetujuan tetap mengikuti kewenangan organisasi yang telah diverifikasi. Fleksibilitas nominal tidak mengubah kewenangan. | Klarifikasi pemilik proyek | `CLARIFIED_BY_PROJECT_OWNER`; mapping authority tetap pending |
| FIN-BR-08 | Nominal transaksi dan laporan bersumber dari data Finance aktual yang tercatat dan disahkan. | Klarifikasi pemilik proyek | `CLARIFIED_BY_PROJECT_OWNER`; istilah status Finance belum ditentukan |
| FIN-BR-09 | Pengeluaran dana siaga memerlukan persetujuan Ketua TSKKM sebagaimana halaman 23 yang terlihat. | SOP halaman 23, parsial | `SOP_CONFIRMED` untuk teks yang terlihat; identitas/authority mapping pending |
| FIN-BR-10 | Dana APP Nasional tidak digunakan untuk kategori biaya kantor yang disebut pada halaman 24. | SOP halaman 24, parsial | `SOP_CONFIRMED` untuk daftar yang terlihat; klasifikasi dan enforcement belum ditentukan |
| FIN-BR-11 | Dana APP Nasional diakses melalui KARINA-KWI dengan SITREP dan rencana penggunaan anggaran sebagaimana teks halaman 24. | SOP halaman 24, parsial | `SOP_CONFIRMED` untuk teks yang terlihat; workflow rinci pending |
| FIN-BR-12 | Tidak ada threshold nominal lain yang boleh diaktifkan tanpa sumber kebijakan/authority formal yang disahkan. | Rekomendasi kontrol berdasarkan klarifikasi | `TECHNICAL_RECOMMENDATION` |
| FIN-BR-13 | Formula remaining budget belum boleh dikunci sebelum dasar accounting, komitmen, cut-off, refund, reversal, dan faktor terkait diputuskan. | Ketidaktersediaan policy dan desain | `PENDING_ORG_DECISION` |
| FIN-BR-14 | Cardinality funding source per budget, budget line, dan expense belum ditetapkan. | Belum ada model/keputusan | `PENDING_DESIGN_DECISION` |
| FIN-BR-15 | Workflow status revisi anggaran merupakan rancangan teknis sampai disahkan. | Belum ada workflow Finance final | `TECHNICAL_RECOMMENDATION` / `PENDING_OWNER_ACCEPTANCE` |
| FIN-BR-16 | Pencatatan actual expenditure tidak boleh membuat salinan nominal editable yang berbeda dari transaksi kanonis. | Rekomendasi integritas data dari klarifikasi | `TECHNICAL_RECOMMENDATION` |
| FIN-BR-17 | Perubahan dan koreksi transaksi harus mempertahankan sejarah dan alasan yang dapat ditelusuri. | Spesifikasi proyek terdahulu; detail kebijakan belum lengkap | `PROJECT_REQUIREMENT_STATED_IN_ADDENDUM` atau `PENDING_OWNER_ACCEPTANCE` bila acceptance terpisah tidak tersedia |

---

## 8. Financial Source of Truth Matrix

| Fakta/data | Sumber otoritatif target | Konsumsi modul lain | Status dan batas |
|---|---|---|---|
| Proposed budget | Catatan proposal Finance yang terhubung ke program/kegiatan dan sumber dana | Program, Procurement, laporan | Pemisahan dari approved budget diklarifikasi; struktur entitas masih desain. |
| Approved budget | Catatan budget yang disetujui beserta referensi bukti approval | Procurement, Finance, laporan | Approval authority harus terverifikasi; belum ada model aktual untuk diperiksa. |
| Budget revision | Riwayat revisi budget dan referensi persetujuan; versi sebelumnya tetap dapat ditelusuri | Finance, Procurement, laporan | Riwayat wajib dari klarifikasi; status lifecycle rinci belum disahkan. |
| Actual expenditure | Catatan transaksi Finance kanonis yang tercatat dan disahkan sesuai kebijakan | Financial report, operation/program report | Target Source of Truth; repository/model aktual tidak tersedia untuk memastikan implementasi. |
| Funding source | Register/catatan sumber pendanaan yang dikelola sesuai otoritas | Budget, transaction, report | Traceability diklarifikasi; katalog dan owner belum ditetapkan. |
| Funding allocation | Catatan alokasi antar sumber, jika multi-source disetujui | Budget line, expense, donor/source reports | `PENDING_DESIGN_DECISION`; tidak menganggap multi-source sudah diizinkan. |
| Remaining budget | Nilai turunan dari budget dan transaksi berdasarkan formula yang disahkan | Dashboard/laporan | Belum menjadi sumber kanonis; formula dan perlakuan komitmen pending. |
| Approval authority | Catatan mandat/delegasi formal dan approval record | Budget approval, expense approval | Authority harus berasal dari keputusan formal; mapping belum tersedia. |
| Financial document | Register dan versi dokumen keuangan yang menyertai transaksi | Finance, audit, final report | Template dan retention rules belum seluruhnya tersedia. |

### Prinsip

- Laporan dan dashboard merupakan view turunan, bukan sumber data yang dapat mengubah transaksi.
- Actual amount tidak boleh menjadi nilai editable kedua yang bertentangan dengan transaksi Finance.
- Perbedaan antara angka laporan dan transaksi sumber harus terlihat, teridentifikasi, dan ditangani melalui proses koreksi yang sah.
- Nominal contoh Rp50 juta dan Rp100 juta tidak menjadi rule sistem.
- Formula remaining budget tidak boleh dinyatakan final sebelum policy disahkan.

---

## 9. Single Source of Truth — Actual Expenditure Analysis

### 9.1 Temuan

Materi yang tersedia belum berisi model transaksi Finance aktual yang dapat diverifikasi. Phase 0.1D menyebut entitas seperti `financial_payments`, `journal_entries`, `journal_entry_lines`, `payment_vouchers`, dan dokumen Finance, tetapi tidak menyediakan ERD final atau field-level dictionary yang disetujui.

Oleh karena itu:

- **Sumber kanonis aktual yang sudah diterapkan:** `EVIDENCE_NOT_AVAILABLE`.
- **Target rekomendasi:** transaksi/transaction line Finance yang disahkan menjadi sumber nilai actual expenditure; laporan mengambil nilai dari sumber tersebut.
- **Status target:** `TECHNICAL_RECOMMENDATION` sampai model Finance dan kebijakan accounting disetujui.

### 9.2 Kontrol yang direkomendasikan

1. Hindari field nominal kedua yang dapat diedit pada record report/reference.
2. Reference report menyimpan hubungan ke transaksi sumber; nilai diturunkan dari transaksi sumber.
3. Bila snapshot diperlukan, dokumentasikan tujuan, waktu snapshot, sumber/versi transaksi, sifat immutable, dan aturan rekonsiliasi.
4. Perbedaan angka tidak dihapus atau ditimpa diam-diam.
5. Perubahan aktual mengikuti mekanisme koreksi/refund/reversal yang disahkan dan mempertahankan hubungan ke catatan asal.
6. Status transaksi yang boleh masuk laporan belum boleh dinamai `posted`, `authorized`, atau `recognized` tanpa sumber yang membuktikannya. Gunakan istilah netral:
   **“transaksi yang statusnya diakui untuk pelaporan sesuai kebijakan Finance yang disahkan.”**

### 9.3 Test negatif

Jika report/reference memiliki nilai berbeda dari transaksi Finance sumber:

- Perbedaan harus terdeteksi.
- Sistem tidak boleh mengganti transaksi sumber untuk menyamakan report.
- Sistem tidak boleh menyembunyikan perbedaan.
- Penyelesaian harus melalui prosedur koreksi yang sah, beralasan, dan dapat diaudit.

---

## 10. Funding Source and Restriction Model Alternatives

### 10.1 Alternatif cardinality

| Alternatif | Bentuk konseptual | Manfaat | Risiko/dampak | Status |
|---|---|---|---|---|
| A — Satu funding source per budget | Setiap budget memiliki satu sumber | Laporan per sumber lebih sederhana | Tidak mendukung campuran sumber bila organisasi memerlukan; bisa memaksa duplikasi budget | `PENDING_DESIGN_DECISION` |
| B — Banyak funding source per budget | Budget dapat dihubungkan ke beberapa sumber | Mendukung beberapa sumber pada anggaran program | Tidak jelas jumlah per sumber jika tanpa allocation record; rekonsiliasi dapat ambigu | `PENDING_DESIGN_DECISION` |
| C — Alokasi pada budget line/expense | Setiap line/expense mempunyai satu atau beberapa allocation record | Dapat menunjukkan jumlah yang dialokasikan per sumber | Menambah kontrol dan rekonsiliasi; memerlukan aturan jumlah, revisi, pembatalan, dan sisa alokasi | `PENDING_DESIGN_DECISION` |

### 10.2 Pertanyaan keputusan

1. Apakah satu program atau kegiatan boleh didanai oleh lebih dari satu sumber?
2. Jika boleh, alokasi dibuat pada level program, activity, budget line, commitment, atau transaksi aktual?
3. Apakah satu expense dapat dibagi lintas sumber dana?
4. Apakah alokasi harus selalu berjumlah sama dengan nilai budget/expense terkait?
5. Siapa yang berwenang mengubah alokasi sumber dana?
6. Bagaimana revisi alokasi dan histori sumber dana dipertanggungjawabkan?

Jangan menetapkan cardinality atau allocation policy sebelum keputusan tersebut tersedia.

### 10.3 Funding-source restriction

Dari gambar halaman 24 yang tersedia, kategori berikut disebut sebagai biaya yang tidak digunakan untuk ditutupi dana darurat APP Nasional:

- Gaji staf.
- Perawatan gedung.
- Perlengkapan dan alat tulis kantor.
- Biaya perawatan kendaraan harian kantor.
- Komunikasi harian kantor dan staf.
- Pembelian alkohol/minuman keras, rokok, dan minuman suplemen.

**Evidence status:** ringkasan dari gambar SOP halaman 24; verifikasi scan resolusi tinggi dan konteks lengkap tetap dianjurkan.

Pilihan enforcement sistem yang belum diputuskan:

1. Hard block.
2. Warning.
3. Manual review.
4. Informational display tanpa blocking.

Tidak ada pilihan yang ditetapkan oleh audit ini. Kategori expense, pengecualian, definisi istilah, dan otoritas interpretasi harus diverifikasi sebelum membuat aturan otomatis.

---

## 11. Budget Lifecycle and Revision Model

### 11.1 Konsep yang harus dibedakan

1. **Proposed budget** — anggaran yang diajukan.
2. **Approved budget** — anggaran yang disetujui melalui authority yang sah.
3. **Budget revision** — perubahan terhadap anggaran, disimpan sebagai riwayat.
4. **Actual expenditure** — nominal aktual dari catatan Finance yang diakui untuk pelaporan sesuai kebijakan.
5. **Remaining budget** — nilai turunan setelah formula dan basis perhitungannya disahkan.

Pemisahan lima konsep merupakan `CLARIFIED_BY_PROJECT_OWNER`. Bentuk teknis dan detail workflow masing-masing tetap perlu desain.

### 11.2 Data revisi minimum yang diklarifikasi

Setiap revisi harus memiliki:

- Riwayat.
- Alasan.
- Aktor.
- Waktu.
- Referensi persetujuan.

### 11.3 State model kandidat — bukan status resmi

State berikut hanya contoh untuk analisis desain:

- Draft/requested.
- Under review.
- Approved.
- Rejected.
- Withdrawn/cancelled.
- Effective.
- Superseded.

Status resmi, aktor transisi, dan urutan proses tidak ditetapkan oleh addendum. Jangan menerapkannya sebagai workflow organisasi sebelum persetujuan.

### 11.4 Integritas revisi

Rekomendasi teknis:

- Revisi yang belum disetujui tidak mengubah approved baseline.
- Nilai lama tetap dapat ditelusuri.
- Revisi menyimpan nilai sebelum dan sesudah.
- Revisi tidak menimpa catatan terdahulu.
- Perubahan bersamaan mendeteksi stale version atau konflik; jangan silent overwrite.
- Reference ke approval hanya dianggap sah jika authority-nya terverifikasi.

Status kontrol integritas tersebut: `TECHNICAL_RECOMMENDATION` atau memerlukan penerimaan sebagai project requirement.

---

## 12. Program–Activity–Budget Relationship Alternatives

Field `program_id / activity_id` tidak cukup untuk mendefinisikan hubungan relasional yang dapat divalidasi.

| Alternatif | Kardinalitas konseptual | Kelebihan | Risiko/ketergantungan |
|---|---|---|---|
| A — Budget pada level program | Program memiliki satu atau lebih budget; activity mengacu pada program | Roll-up pada program sederhana | Sulit membedakan alokasi tiap activity jika diperlukan |
| B — Budget pada level activity | Activity memiliki budget; activity menjadi bagian program jika model mengharuskannya | Hubungan biaya ke aktivitas lebih rinci | Perlu aturan roll-up dan revisi program |
| C — Budget header + budget lines | Budget header terkait program; lines berhubungan dengan activity/category | Mendukung pelaporan agregat dan detail | Model Program/Activity, funding allocation, serta revision workflow harus disepakati |
| D — Budget bisa pada program atau activity | Referensi ke salah satu level | Fleksibel | Polymorphic reference dan integritas FK berisiko tanpa desain eksplisit |

### Pertanyaan keputusan

- Apakah semua activity harus berada dalam program?
- Bolehkah ada budget pada tingkat Program, Activity, atau keduanya?
- Apakah budget line selalu punya category atau expense type?
- Apakah budget activity harus menjumlah sama dengan program budget?
- Bagaimana revision pada program berpengaruh ke budget activity?
- Bagaimana biaya bersama dialokasikan?

**Status:** `PENDING_DESIGN_DECISION`. Tidak ada physical schema atau kardinalitas final yang ditetapkan.

---

## 13. Remaining Budget Policy Dependency

Rumus remaining budget **tidak ditetapkan** oleh audit ini.

Faktor yang perlu diklarifikasi oleh kebijakan Finance:

- Approved budget dan revisinya yang efektif.
- Actual expenditure yang diakui untuk pelaporan.
- Commitment/encumbrance.
- Purchase order yang belum selesai.
- Invoice yang diterima tetapi belum dibayar.
- Pembayaran/advance.
- Refund dan reversal.
- Transaksi yang dibatalkan.
- Period cut-off.
- Multi-currency dan exchange rate jika diizinkan.
- Rounding dan precision.

### Ilustrasi perbedaan basis — bukan rumus yang disetujui

Contoh hipotetis:

- Approved budget: Rp100 juta.
- Actual expenditure: Rp20 juta.
- Purchase order terbuka: Rp10 juta.
- Invoice belum dibayar: Rp5 juta.

Bila hanya actual expenditure dikurangkan, hasil sementara berbeda dari perhitungan yang juga mengurangi komitmen atau invoice belum dibayar. Ilustrasi ini hanya menunjukkan bahwa basis perhitungan dapat mengubah angka yang tampil. Audit ini **tidak memilih** hasil mana yang benar.

Jika organisasi memerlukan tampilan sebelum formula final disahkan, opsi teknis adalah menampilkan nilai sebagai **estimasi**, disertai basis komponen dan status. Opsi ini adalah `TECHNICAL_RECOMMENDATION`, bukan kebijakan yang telah disetujui.

---

## 14. Finance–Procurement–Logistics Dependency Matrix

| Domain record | Pemilik data yang diusulkan | Referensi lintas modul | Implikasi Finance | Status/pending |
|---|---|---|---|---|
| Procurement request / requisition | Procurement | Program/activity/needs | Dapat menjadi dasar permintaan; tidak otomatis merupakan actual expenditure | Detail proses mengacu SOP procurement yang belum diperiksa penuh |
| Quotation / bid analysis | Procurement | Supplier/request | Evidence pemilihan/estimasi; tidak otomatis menjadi payment atau expense | Template/otoritas belum diverifikasi dari sumber penuh |
| Purchase order | Procurement | Request, supplier, budget reference | Potensi commitment bila policy menetapkan; jangan anggap otomatis actual | Pengakuan commitment pending |
| Physical receipt / Goods Received Note | Warehouse/Logistics | PO, item, warehouse | Bukti barang diterima; bukan invoice/payment | Pemisahan dokumen fisik dan Finance harus dipertahankan |
| Invoice | Finance/document record sesuai ownership yang disahkan | Supplier, PO, receipt bila relevan | Klaim pembayaran/biaya; timing dan accounting treatment belum ditetapkan | Urutan invoice/GRN/payment jangan diasumsikan |
| Payment voucher | Finance | Invoice/request, approval evidence | Dokumentasi permohonan pembayaran | Template/approval authority belum seluruhnya tersedia |
| Payment | Finance | Voucher, bank/financial account, source documents | Transaksi uang; menjadi actual hanya sesuai policy Finance | Status aktual dan pengakuan perlu definisi |
| Expense recognition | Finance/accounting | Invoice/payment/journal/source documents | Menentukan angka actual pada laporan | `PENDING_ORG_DECISION`; tidak disimpulkan dari payment saja |
| Commitment/encumbrance | Finance atau Procurement sesuai keputusan ownership | PO, approved budget | Dapat memengaruhi remaining budget jika policy mengharuskan | Model dan basis pending |
| Inventory posting | Inventory/Warehouse | GRN, stock movement | Tidak otomatis sama dengan pengeluaran atau payment | Source of inventory balance adalah domain Inventory |
| Refund/reversal | Finance | Transaksi asal dan dokumen koreksi | Harus tertaut ke transaksi awal; perlakuan laporan mengikuti policy | Policy dan status belum tersedia |
| Financial accountability report | Finance/reporting layer | Finance transactions, supporting documents | Angka aktual harus berasal dari catatan Finance kanonis | Format/approval final belum lengkap |

### Kontrol lintas modul

- Procurement request, PO, invoice, payment, expense recognition, stock posting, dan distribution tidak saling menggantikan.
- Invoice checking dan physical goods inspection harus tetap berbeda.
- Tidak menetapkan urutan pembayaran terhadap penerimaan barang tanpa sumber/pedoman yang sah.
- Setiap event lintas modul harus idempotent bila memicu transaksi.
- Reconciliation menampilkan selisih; tidak menimpa sumber data secara otomatis.
- Actual Finance amount harus ditelusuri dari record kanonis dan dokumen pendukung.

---

## 15. Finance Entity Registry — konseptual

| Entitas konseptual | Tujuan | Source of truth / ownership | Status |
|---|---|---|---|
| Budget proposal | Mencatat anggaran yang diusulkan | Finance/budget owner yang perlu disahkan | Entitas logis yang diusulkan; field dan owner final pending |
| Approved budget record | Menyimpan anggaran yang disetujui dan evidence | Finance plus authority record | Persetujuan harus mengikuti authority terverifikasi |
| Budget revision record | Mempertahankan riwayat revisi dan metadata wajib | Finance/budget owner | Riwayat diklarifikasi; lifecycle teknis pending |
| Budget line | Mewakili rincian budget bila diperlukan | Finance/program relationship | Kebutuhan dan kardinalitas belum ditentukan |
| Funding source reference | Mengidentifikasi sumber pendanaan | Pemilik master Finance yang perlu ditetapkan | Traceability diklarifikasi; katalog/owner pending |
| Funding allocation | Merepresentasikan pembagian nilai antar sumber jika diizinkan | Finance | Tidak dianggap wajib sebelum keputusan cardinality |
| Financial transaction | Mencatat transaksi Finance kanonis | Finance | Bentuk model aktual tidak tersedia |
| Financial transaction line | Rincian transaksi bila model domain memerlukan | Finance | Rancangan teknis; perlu model aktual |
| Approval reference | Menautkan transaksi/budget ke dasar authority dan bukti | Authority/document governance | Otoritas dan storage record perlu disetujui |
| Actual expenditure reference/view | Menyajikan angka dari transaksi kanonis | Finance transaction sebagai source target | Hindari nominal editable ganda |
| Remaining budget view | Menampilkan perhitungan berbasis policy | Turunan, bukan sumber | Formula pending |
| Financial document reference | Menghubungkan dokumen pendukung ke budget/transaksi | Document registry/Finance | Template dan retention belum lengkap |

Nama entitas di atas bersifat konseptual dan tidak menetapkan nama tabel fisik.

---

## 16. Finance Data Dictionary Corrections — logical level only

| Konsep | Field logis | Perlakuan | Status |
|---|---|---|---|
| Proposed budget | Proposal ID, program/activity reference, proposed amount, funding source reference, creator, timestamp, version | Pisahkan dari nilai disetujui; relasi program/activity jangan memakai FK ambigu. | Pemisahan kategori `CLARIFIED_BY_PROJECT_OWNER`; bentuk field teknis |
| Approved budget | Approved amount, approval reference, approver, approval timestamp, effective version | Tidak dianggap approved tanpa authority yang berlaku dan evidence sesuai policy. | Authority/policy pending |
| Budget revision | Revision ID, previous/revised value, reason, actor, timestamp, approval reference, version/effective state | Riwayat tidak ditimpa; state final menunggu persetujuan workflow. | Metadata pokok `CLARIFIED_BY_PROJECT_OWNER`; detail teknis pending |
| Funding source | Funding source ID/code, label, source/evidence, status/effective period jika disetujui | Referensi dapat ditelusuri; kategori dan owner harus berasal dari sumber resmi. | Traceability `CLARIFIED_BY_PROJECT_OWNER`; master detail pending |
| Funding allocation | Budget/line/expense reference, funding source, allocated value, version/status | Hanya bila multi-source allocation disetujui. | `PENDING_DESIGN_DECISION` |
| Actual expenditure | Canonical transaction reference; amount derived from source, not a second editable copy | Report/reference menunjuk transaksi; snapshot hanya jika immutable dan beralasan. | Target `TECHNICAL_RECOMMENDATION`; model aktual belum tersedia |
| Remaining budget | Derived amount plus calculation basis/version | Jangan input/edit sebagai angka definitif sebelum formula disahkan. | `PENDING_ORG_DECISION` |
| Approval reference | Approval/authority document and applicable scope/date/version | Tidak menyimpulkan authority dari edit permission atau nominal contoh. | Authority registry dan model approval pending |
| Currency | Currency code | Jangan mengunci multi-currency atau currency conversion tanpa policy. | `PENDING_ORG_DECISION` / physical-design dependency |
| Monetary precision | Decimal precision/representation | Hindari binary floating point sebagai rekomendasi teknis; nilai fisik belum dipilih. | `TECHNICAL_RECOMMENDATION` |

Nullability, uniqueness, physical data types, rounding, accounting status values, dan constraint tidak ditetapkan dalam audit ini.

---

## 17. Approval Authority and Permission Dependency

### 17.1 Bukti yang tersedia

- SOP halaman 23 yang terlihat menyatakan pengeluaran dana siaga atas persetujuan Ketua TSKKM.
- Klarifikasi pemilik proyek menyatakan fleksibilitas nominal tidak mengubah kewenangan persetujuan.
- Materi proyek sebelumnya menyatakan kewenangan Respons/Tidak Respons dan beberapa role, tetapi keputusan formal pendukung tidak dilampirkan dalam audit ini.

### 17.2 Batas kesimpulan

- Tidak dapat dipastikan dari materi ini apakah Ketua TSKKM adalah Romo Direktur Caritas, atau apakah kewenangan tersebut didelegasikan.
- Tidak tersedia approval matrix Finance yang lengkap.
- Tidak ada bukti threshold nominal resmi.
- Tidak ada dasar untuk memberikan approval authority kepada Finance Officer, Administrasi, Koordinator, atau operational assignment lainnya.

### 17.3 Rekomendasi pemisahan

Pisahkan:

1. Permission teknis untuk membuat/mengubah/mengirim data.
2. Assignment operasional.
3. Approval authority yang bersumber dari mandat/delegasi formal.
4. Approval record atas keputusan tertentu.
5. Audit event dan dokumen pendukung.

Edit permission tidak otomatis memberikan approval authority. Nominal contoh tidak boleh menentukan authority. Threshold lain hanya dapat diterapkan bila berasal dari kebijakan/authority matrix formal yang disahkan, memiliki scope, versi, tanggal berlaku, dan otoritas yang jelas.

---

## 18. Test Plan FIN-TEST-01 sampai FIN-TEST-23

**Status seluruh tes:** belum dijalankan; hasil aktual dicatat **“belum dijalankan”**.  
Tes repository/code yang memerlukan repository berstatus `BLOCKED_BY_MISSING_SOURCE`.  
Tidak ada hasil `TEST_EXECUTED_PASS` atau `TEST_EXECUTED_FAIL`.

| Test ID | Tujuan dan skenario | Preconditions / data | Expected result | Actual result | Status dan dependency/evidence |
|---|---|---|---|---|---|
| FIN-TEST-01 | Catat proposed budget Rp25 juta | Model budget dan validasi tersedia pada lingkungan test | Tidak terkena cap/default yang berasal dari nominal contoh; aturan validasi lain harus bersumber policy yang sah | Belum dijalankan | `TEST_DESIGNED`; implementasi/policy belum tersedia |
| FIN-TEST-02 | Catat proposed budget Rp75 juta | Sama seperti FIN-TEST-01 | Tidak otomatis dianggap melanggar threshold Rp50m/Rp100m | Belum dijalankan | `TEST_DESIGNED` |
| FIN-TEST-03 | Catat proposed budget Rp250 juta | Sama seperti FIN-TEST-01 | Tidak otomatis ditolak berdasarkan kedua nilai contoh | Belum dijalankan | `TEST_DESIGNED` |
| FIN-TEST-04 | Proposed budget berbeda dari approved budget | Proposed Rp75m; approved value dengan bukti approval yang valid | Proposal dan approved value tetap terpisah; approval reference dapat ditelusuri | Belum dijalankan | `TEST_DESIGNED`; authority/policy dan model belum tersedia |
| FIN-TEST-05 | Revision belum disetujui | Approved baseline aktif; revision diajukan tetapi belum disetujui | Revisi belum mengubah baseline approved yang berlaku | Belum dijalankan | `TEST_DESIGNED`; status/workflow revision belum disahkan |
| FIN-TEST-06 | Uji metadata revisi | Revision mempunyai perubahan nilai | Histori, alasan, aktor, waktu, nilai sebelum/sesudah, dan approval reference tersedia sesuai requirement yang disetujui | Belum dijalankan | `TEST_DESIGNED`; beberapa field merupakan kebutuhan pemilik proyek, lifecycle approval pending |
| FIN-TEST-07 | Uji cardinality satu/banyak funding source | Model funding source belum diputuskan | Sistem/specification tidak menganggap satu atau banyak sumber sebagai kebijakan tanpa keputusan | Belum dijalankan | `BLOCKED_BY_MISSING_POLICY` untuk menetapkan hasil bisnis; test desain tetap tersedia |
| FIN-TEST-08 | Uji restriction funding source yang didukung SOP | Gunakan kategori yang benar-benar tampak pada halaman 24; jangan menambah kategori | Perilaku mengikuti policy enforcement yang secara resmi dipilih; tidak membuat larangan baru | Belum dijalankan | `BLOCKED_BY_MISSING_POLICY`; perlu verifikasi sumber lebih lengkap dan pilihan enforcement |
| FIN-TEST-09 | Report actual expenditure mengambil nominal dari satu sumber kanonis | Model transaksi aktual kanonis telah disetujui | Nilai laporan diturunkan dari transaksi sumber yang diakui untuk pelaporan sesuai policy | Belum dijalankan | `TEST_DESIGNED`; model aktual dan status accounting belum tersedia |
| FIN-TEST-10 | Report/reference berbeda dari nominal transaksi sumber | Sumber transaksi nominal A; report mencoba nominal B | Selisih terdeteksi dan dapat ditelusuri; tidak ada overwrite diam-diam; koreksi mengikuti proses sah | Belum dijalankan | `TEST_DESIGNED`; model transaksi/correction belum tersedia |
| FIN-TEST-11 | Remaining budget sebelum formula disahkan | Budget, actual, PO, invoice atau commitment tersedia | Angka tidak dinyatakan sebagai saldo definitif; jika estimasi ditampilkan, basisnya jelas dan dilabeli | Belum dijalankan | `BLOCKED_BY_MISSING_POLICY` untuk nilai definitif; tampilan estimasi adalah usulan teknis |
| FIN-TEST-12 | User memiliki edit permission tanpa approval authority | User dapat mengubah draft, tidak memiliki authority | Approval ditolak; alasan/denial dapat diaudit sesuai kontrol yang disahkan | Belum dijalankan | `TEST_DESIGNED`; approval matrix belum tersedia |
| FIN-TEST-13 | Retry menggunakan idempotency key yang sama | Revision/transaksi command dikirim berulang | Tidak membuat revision/transaksi duplikat | Belum dijalankan | `TEST_DESIGNED`; idempotency adalah rekomendasi teknis |
| FIN-TEST-14 | Dua revisi berjalan bersamaan | Dua user mengubah baseline versi yang sama | Konflik/stale version terdeteksi; tidak ada silent overwrite | Belum dijalankan | `TEST_DESIGNED`; implementasi dan concurrency policy belum tersedia |
| FIN-TEST-15 | Refund/reversal | Ada transaksi asal dan dokumen koreksi | Transaksi asal tetap terlacak; refund/reversal terhubung ke asal; pelaporan mengikuti policy | Belum dijalankan | `BLOCKED_BY_MISSING_POLICY`; accounting treatment belum disahkan |
| FIN-TEST-16 | Cari hardcoded nominal pada repository | Repository dan branch/commit tersedia dengan izin baca | Pencarian mencakup logic/config/seed/validation/workflow/migration/test fixture; dokumentasi contoh tidak salah dianggap rule | Belum dijalankan | `BLOCKED_BY_MISSING_SOURCE`; repository tidak tersedia |
| FIN-TEST-17 | Threshold selain nilai contoh tanpa authority formal | Konfigurasi candidate memiliki threshold tanpa sumber formal | Tidak diaktifkan sebagai policy; tindakan akhir mengikuti governance yang disahkan | Belum dijalankan | `TEST_DESIGNED`; authority policy dan enforcement belum tersedia |
| FIN-TEST-18 | Threshold formal dengan scope/version/effective date | Ada dokumen formal dan authority yang dapat diverifikasi | Hanya dipertimbangkan setelah persetujuan organisasi; fleksibilitas nominal tidak mengubah authority | Belum dijalankan | `BLOCKED_BY_MISSING_SOURCE` sampai dokumen formal dan approval tersedia |
| FIN-TEST-19 | Multi-source allocation sebelum cardinality disetujui | Proposal mencoba mengalokasikan lebih dari satu source | Tidak dinilai valid/invalid berdasarkan asumsi; keputusan tetap pending | Belum dijalankan | `BLOCKED_BY_MISSING_POLICY` |
| FIN-TEST-20 | Funding restriction belum diverifikasi | Expense category dipertanyakan terhadap sumber dana | Tidak menjadi automatic block rule; status dan sumber ketidakpastian terlihat | Belum dijalankan | `BLOCKED_BY_MISSING_SOURCE` untuk penerapan policy; perilaku manual/warning/block masih pending |
| FIN-TEST-21 | PO terbuka dan invoice belum dibayar pada perhitungan remaining | Approved budget, PO, invoice, dan actual tersedia | Tidak menghasilkan remaining budget definitif tanpa basis commitment/accrual yang disahkan | Belum dijalankan | `BLOCKED_BY_MISSING_POLICY` |
| FIN-TEST-22 | Hubungan Program/Activity/Budget | Budget terkait program/activity/line | Tidak ada orphan reference atau polymorphic ambiguity; relasi diuji setelah entity model disetujui | Belum dijalankan | `BLOCKED_BY_MISSING_SOURCE`; model Program/Activity dan Finance belum tersedia |
| FIN-TEST-23 | Report per funding source | Allocation dan transaksi sudah mempunyai model yang disetujui | Total per source dapat direkonsiliasi ke alokasi/transaksi kanonis tanpa double count | Belum dijalankan | `BLOCKED_BY_MISSING_POLICY`; cardinality/alokasi dan model transaksi belum disahkan |

### Bukti minimum untuk perubahan status tes menjadi `TEST_EXECUTED_*`

- Lingkungan dan versi/build/commit.
- Test data atau fixture.
- Langkah eksekusi.
- Expected result dan actual result.
- Log/output yang relevan.
- Tidak ada perubahan data produksi.
- Referensi test report yang dapat ditinjau.

---

## 19. Updated CHR-020 Mapping

| Isu dalam CHR-020 | Status setelah klarifikasi | Catatan |
|---|---|---|
| Sumber pendanaan dari halaman 23 | Sebagian memiliki evidence dari gambar halaman 23 | Perlu pemeriksaan sumber penuh dan klasifikasi detail. |
| Dana siaga dan dana operasional | Teks halaman 23 terlihat | Pengelolaan dan aturan accounting rinci belum tersedia. |
| Persetujuan pengeluaran dana awal oleh Ketua TSKKM | Teks halaman 23 terlihat | Authority identity, delegation, dan pemetaan ke role sistem masih perlu bukti formal. |
| Nominal Rp50 juta | Makna sebagai nilai contoh diklarifikasi pemilik proyek | Tidak boleh menjadi fixed amount, cap, default wajib, atau approval threshold. |
| Nominal Rp100 juta pada template halaman 49 | Makna sebagai nilai contoh diklarifikasi pemilik proyek | Halaman 49/template belum tersedia; bentuk template dan field tetap `EVIDENCE_NOT_AVAILABLE`. |
| Pembatasan APP Nasional pada halaman 24 | Sebagian daftar terlihat dalam gambar | Verifikasi scan dan konteks lengkap; jangan membuat enforcement baru tanpa policy. |
| Hubungan Rp50m dengan Rp100m | Tidak perlu dianggap hubungan nominal karena keduanya contoh | Jangan menyamakan, menjumlahkan, atau menjadikannya batas. |
| Identitas pejabat “Ketua TSKKM” | Belum selesai | Jangan menyamakan otomatis dengan Romo Direktur Caritas. |
| Batas/approval threshold lain | Tidak ditetapkan addendum | Hanya dapat berasal dari kebijakan/authority formal yang disahkan. |
| Seluruh CHR-020 | **Masih terbuka sebagian** | Klarifikasi nominal tidak menutup isu sumber, kewenangan, restriction, atau prosedur lainnya. |

---

## 20. Pending Finance Decision Register

| ID | Keputusan/sumber yang diperlukan | Status | Pengaruh jika belum selesai |
|---|---|---|---|
| FIN-DEC-01 | Repository/branch/commit untuk pemeriksaan hardcoded rules | `EVIDENCE_NOT_AVAILABLE` | Tidak dapat memeriksa apakah nilai contoh tertanam dalam code/config. |
| FIN-DEC-02 | SOP Finance/procurement lengkap dan scan halaman terkait | `EVIDENCE_NOT_AVAILABLE` | Tidak dapat menyelesaikan seluruh business rule dan form mapping. |
| FIN-DEC-03 | Template halaman 49 dan bukti sumber versi dokumen | `EVIDENCE_NOT_AVAILABLE` | Struktur dan field template tidak dapat diaudit. |
| FIN-DEC-04 | Identitas/mandat/delegasi Ketua TSKKM untuk approval dana siaga | `PENDING_ORG_DECISION` / sumber formal belum tersedia | Tidak dapat mengunci authority mapping. |
| FIN-DEC-05 | Approval matrix Finance dan procurement | `PENDING_ORG_DECISION` | Tidak dapat menentukan approver tiap proses. |
| FIN-DEC-06 | Cardinality sumber dana pada program, budget, line, dan expense | `PENDING_DESIGN_DECISION` | Model alokasi dan laporan per sumber belum final. |
| FIN-DEC-07 | Program–Activity–Budget relationship | `PENDING_DESIGN_DECISION` | FK/cardinality dan budget roll-up belum final. |
| FIN-DEC-08 | Budget revision lifecycle dan state resmi | `PENDING_ORG_DECISION` atau `PENDING_OWNER_ACCEPTANCE` | Revisi belum dapat dibangun sebagai workflow final. |
| FIN-DEC-09 | Actual expenditure recognition/source of truth pada model Finance yang berlaku | `PENDING_DESIGN_DECISION` / bukti model aktual tidak ada | Tidak dapat mengklaim Source of Truth aktual telah ditetapkan. |
| FIN-DEC-10 | Accounting treatment untuk PO, commitment, invoice, payment, dan expense | `PENDING_ORG_DECISION` | Remaining budget dan reporting tidak dapat dihitung final. |
| FIN-DEC-11 | Formula remaining budget dan period cut-off | `PENDING_ORG_DECISION` | Saldo anggaran tidak boleh disajikan sebagai angka definitif. |
| FIN-DEC-12 | Refund, reversal, advance, cancellation, dan cut-off | `PENDING_ORG_DECISION` | Pengaruh transaksi koreksi ke actual/remaining belum dapat disahkan. |
| FIN-DEC-13 | Funding-source restrictions dan enforcement mode | `PENDING_ORG_DECISION` untuk enforcement; sebagian isi SOP terlihat | Sistem tidak boleh membuat hard block baru tanpa interpretasi/persetujuan. |
| FIN-DEC-14 | Currency, multi-currency, precision, rounding, exchange rate | `PENDING_ORG_DECISION` dan physical design dependency | Tidak dapat mengunci tipe/konversi final. |
| FIN-DEC-15 | Retensi dokumen Finance dan audit evidence | `PENDING_ORG_DECISION` / sumber belum lengkap | Retention/archive policy belum dapat ditetapkan. |

---

## 21. Risk Register

| Risk ID | Risiko | Pencegahan | Deteksi | Pemulihan/penanganan | Status |
|---|---|---|---|---|---|
| FIN-RISK-01 | Nominal contoh tertanam menjadi cap/default/threshold | Requirement harus melarang penggunaan sebagai logic; code/config review saat repository tersedia | Cari variasi angka pada logic/config/seed/validation/workflow/migration/test | Hapus rule tidak sah lewat perubahan terkendali; audit dan uji regresi | `BLOCKED_BY_MISSING_SOURCE` untuk repository audit |
| FIN-RISK-02 | Approval authority diasumsikan dari nominal atau edit permission | Pisahkan permission dan authority registry | Positive/negative approval tests dan audit review | Cabut permission/authority yang keliru; pertahankan bukti dan koreksi melalui proses resmi | `PENDING_ORG_DECISION` |
| FIN-RISK-03 | Actual amount tersimpan dalam dua sumber editable | Satu canonical Finance transaction; report amount diturunkan | Rekonsiliasi report dengan transaction source | Tampilkan discrepancy dan lakukan koreksi tercatat; jangan menimpa sumber | `TECHNICAL_RECOMMENDATION` |
| FIN-RISK-04 | Multi-source funding tidak dapat dilacak atau dialokasikan konsisten | Putuskan cardinality dan allocation level | Rekonsiliasi per source/line/transaction | Tahan alokasi yang ambigu untuk keputusan, tanpa auto-transfer | `PENDING_DESIGN_DECISION` |
| FIN-RISK-05 | Restriction APP Nasional diterapkan salah | Transkripsikan sumber lengkap dan minta keputusan enforcement | Uji kategori allowed/restricted hanya setelah policy disahkan | Nonaktifkan rule yang tidak didukung; pertahankan log dan review | `PENDING_ORG_DECISION` |
| FIN-RISK-06 | Budget/activity memakai referensi polimorfik dan menjadi orphan | Tetapkan relasi Program/Activity dan FK eksplisit sebelum schema | Referential integrity dan relationship tests | Perbaiki model melalui revisi terkontrol; jangan hilangkan histori | `PENDING_DESIGN_DECISION` |
| FIN-RISK-07 | Remaining budget menyesatkan karena commitment/cut-off tidak jelas | Tunda formula definitif; jelaskan basis tampilan | Uji komponen approved/actual/PO/invoice/advance | Labeli ulang sebagai estimasi atau tarik report yang tidak berdasar | `PENDING_ORG_DECISION` |
| FIN-RISK-08 | Revision menimpa approved baseline atau kehilangan histori | Versioning dan revision record; approval terpisah | Uji revision before/after dan concurrency | Restore versi historis melalui proses tercatat; jangan menghapus revision | `TECHNICAL_RECOMMENDATION` |
| FIN-RISK-09 | Procurement, payment, expense, dan inventory dicampur | Tetapkan domain ownership dan integration contracts | Cross-module reconciliation tests | Catat discrepancy dan koreksi pada source domain yang berwenang | `PENDING_SOURCE` untuk SOP lengkap |
| FIN-RISK-10 | Report tidak dapat ditelusuri ke dokumen sumber | Source references dan lineage wajib untuk angka penting | Sample trace dari report ke transaction/document | Perbaiki provenance melalui record koreksi; jangan ketik ulang tanpa sumber | `CLARIFIED_BY_PROJECT_OWNER` untuk asal angka; detail model teknis |
| FIN-RISK-11 | Retry atau concurrency membuat revisi/transaksi ganda | Idempotency dan version checks sebagai rekomendasi teknis | Retry/concurrent submission tests | Rekonsiliasi duplikasi dengan jejak audit; tidak menghapus sejarah diam-diam | `TECHNICAL_RECOMMENDATION` |

---

## 22. Evidence Missing / Required

Sebelum logical Finance design dapat difinalisasi, diperlukan:

1. SOP Finance dan procurement lengkap, termasuk halaman 34–35, 40–41, 62–69, dan halaman lain yang relevan.
2. Scan resolusi memadai untuk semua tabel dan formulir.
3. Template permohonan dana APP-KWI halaman 49.
4. Dokumen/keputusan formal tentang kewenangan Ketua TSKKM dan delegasinya.
5. Approval matrix untuk Finance dan Procurement.
6. Pedoman keuangan/akuntansi yang disahkan, termasuk pengakuan actual expenditure, commitment, cut-off, reversal, refund, advance, rounding, dan currency.
7. Model Program/Activity yang disetujui.
8. Keputusan apakah funding allocation boleh menggunakan beberapa sumber dan pada level apa.
9. Model transaksi Finance aktual atau ERD/data dictionary yang ditinjau.
10. Repository dan branch/commit jika audit hardcoding diminta.
11. Dokumen pemilik data, steward, retention, dan akses Finance.
12. Bukti hasil pengujian bila status test ingin dinaikkan dari `TEST_DESIGNED`.

---

## 23. Readiness Assessment

### Status: `BLOCKED`

Alasan:

- Repository/code tidak tersedia untuk audit hardcoding.
- Model Finance aktual dan canonical actual expenditure record tidak tersedia.
- Approval authority formal untuk seluruh Finance workflow belum dipetakan.
- Restriction funding source baru diverifikasi sebagian dari gambar SOP halaman 24; enforcement mode belum disahkan.
- Funding-source cardinality belum diputuskan.
- Program–Activity–Budget relationship belum disetujui.
- Budget revision lifecycle belum disahkan.
- Formula dan basis remaining budget belum diputuskan.
- Finance/procurement source pages dan template terkait belum tersedia lengkap.

### Kesiapan menurut tahap

| Tahap | Status |
|---|---|
| Pencatatan klarifikasi nominal | **READY** sebagai requirement yang jelas |
| Audit dokumentasi parsial | **CONDITIONAL** pada evidence yang tersedia |
| Finance logical design final | **BLOCKED** oleh keputusan dan sumber yang belum tersedia |
| Physical database design | **BLOCKED** dan tidak termasuk dalam pekerjaan ini |
| Implementasi aplikasi | **BLOCKED** dan dilarang dalam audit ini |

Tidak ada code, database, migration, atau test suite yang dinyatakan lulus.

---

## 24. Recommended Next Prompt

Setelah pemilik proyek meninjau dokumen ini dan menyediakan sumber yang hilang, langkah berikut yang disarankan adalah:

> **Lakukan rekonsiliasi Finance–Procurement–Program berdasarkan SOP lengkap dan dokumen keputusan organisasi. Perbarui requirement traceability, authority matrix, funding restriction register, canonical Finance transaction model, Program–Activity–Budget relationship alternatives, serta remaining-budget policy dependencies. Tetap read-only dan jangan membuat schema, migration, code, atau perubahan database. Tandai semua sumber yang belum tersedia dan semua keputusan yang masih pending.**

Jangan lanjut ke physical schema atau implementation sebelum:
- Dokumen SOP Finance/procurement lengkap diperiksa.
- Authority dan delegation diverifikasi.
- Source of Truth actual expenditure disepakati.
- Funding cardinality dan restriction model disetujui.
- Budget revision lifecycle dan remaining-budget basis ditentukan.
- Pemilik proyek meninjau dan menyetujui logical Finance specification.

---

## 25. Pernyataan akhir

Klarifikasi pemilik proyek menyelesaikan interpretasi bahwa Rp50.000.000 dan Rp100.000.000 hanya merupakan nilai contoh. Kedua nominal tidak boleh menjadi hardcoded cap, default wajib, atau automatic approval threshold.

Klarifikasi tersebut tidak menyelesaikan kewenangan approval, cardinality sumber dana, aturan alokasi, pengakuan accounting, formula remaining budget, atau hubungan Finance dengan procurement dan Program/Activity. Isu-isu itu tetap pending sampai tersedia sumber dan keputusan yang sah.

Audit ini read-only. Tidak ada code, database, migration, seed, integration test, database test, atau test suite yang dijalankan maupun diubah. Hasil ini diserahkan untuk review pemilik proyek; tidak ada tindak lanjut implementasi yang dilakukan.