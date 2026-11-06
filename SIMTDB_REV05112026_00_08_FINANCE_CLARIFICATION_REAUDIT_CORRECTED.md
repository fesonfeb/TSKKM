# SIM-TDB — RE-AUDIT FINANCE TERKOREKSI
## Kebijakan Dana Darurat, Kontrol Per Kejadian, dan Ketersediaan Kas

**Document ID:** SIMTDB-REV05112026-00-08-FIN  
**Filename:** `SIMTDB_REV05112026_00_08_FINANCE_CLARIFICATION_REAUDIT_CORRECTED.md`  
**Revision:** REV05112026  
**Status:** Draft untuk review pemilik proyek dan pihak berwenang  
**Mode:** Audit dokumen, requirement harmonization, dan rancangan pengujian — tanpa implementasi  
**Project:** Sistem Informasi Manajemen Tanggap Darurat Bencana (SIM-TDB)  
**Organization:** Caritas Keuskupan Malang — Tim Solidaritas Kemanusiaan Keuskupan Malang (TSKKM)

---

## 1. Executive Summary

Audit ini mengoreksi hasil Finance sebelumnya berdasarkan:

- Klarifikasi pemilik proyek tentang nominal Rp50.000.000 dan Rp100.000.000.
- Klarifikasi lanjutan bahwa Rp50.000.000 merupakan maksimum pengeluaran dana darurat TSKKM untuk satu kejadian/operasi respons.
- Penegasan bahwa beberapa kejadian berbeda dapat masing-masing menerima dana hingga batas per kejadian, tetapi totalnya tetap harus berada dalam kas darurat yang benar-benar tersedia.
- Dokumen audit Finance 00_02 sampai 00_06 dan Prompt Re-audit 00_07.
- Gambar SOP TSKKM halaman cetak 16–29 yang tersedia dalam percakapan.

### Kesimpulan kebijakan

Prinsip kerja yang harus dibawa ke desain SIM-TDB adalah:

1. **Rp100.000.000 adalah contoh ilustratif saja**, bukan nominal baku, plafon, default, atau approval threshold.
2. **Rp50.000.000 adalah batas maksimum pengeluaran dana darurat TSKKM untuk satu kejadian/operasi respons**, berdasarkan klarifikasi langsung yang diberikan.
3. Batas Rp50.000.000 **bukan batas global** untuk seluruh kejadian TSKKM.
4. Beberapa kejadian berbeda masing-masing dapat menerima dana darurat, sepanjang setiap kejadian mematuhi batas per kejadian dan jumlah keseluruhan tidak melebihi kas yang memenuhi syarat dan benar-benar tersedia.
5. Batas per kejadian dan batas ketersediaan kas merupakan **dua kontrol berbeda**:
   - Kontrol per kejadian: maksimum Rp50.000.000 untuk control unit yang ditetapkan.
   - Kontrol kas: seluruh komitmen/disbursement yang dihitung menurut policy tidak melebihi kas darurat yang memenuhi syarat.
6. Fleksibilitas lintas kejadian tidak mengubah kewenangan persetujuan.
7. Belum boleh diputuskan tanpa konfirmasi lebih lanjut:
   - Apakah satu kejadian dapat berisi beberapa operasi yang masing-masing punya batas terpisah.
   - Tahap transaksi apa yang mengonsumsi limit per kejadian dan kas.
   - Definisi kas yang memenuhi syarat/tersedia.
   - Perlakuan terhadap reservasi, pembayaran tertunda, advance, refund, reversal, dan dana yang dibatasi penggunaannya.

### Catatan sumber penting

Gambar SOP halaman 23 yang tersedia menampilkan kalimat tentang dana darurat sebesar Rp50.000.000 dan persetujuan Ketua TSKKM. Klarifikasi pemilik proyek yang lebih baru menetapkan bahwa nominal tersebut adalah **maksimum per kejadian/operasi**, bukan jumlah wajib atau cap global.

Klarifikasi tersebut menjadi baseline proyek untuk rancangan sistem. Namun redaksi halaman SOP yang terlihat dapat dibaca berbeda dari klarifikasi terbaru. Karena SOP merupakan sumber operasional pengendali, perbedaan ini dicatat sebagai **`SOURCE_CONFLICT` yang harus dikonfirmasi secara formal** sebelum kebijakan sistem dinyatakan final atau diterapkan.

### Readiness

**Status keseluruhan: `BLOCKED` untuk logical design final dan implementasi.**

Audit ini cukup untuk menetapkan arah kontrol dan test plan. Belum cukup untuk mengunci model operasi/kejadian, perhitungan kas tersedia, otoritas formal, atau accounting treatment.

---

## 2. Scope, Sources, and Evidence Availability

### 2.1 Sumber yang diperiksa

| Source ID | Sumber | Status | Cakupan dan batas |
|---|---|---|---|
| SRC-00-02 | `SIMTDB_REV05112026_00_02_FINANCIAL_AMOUNT_CLARIFICATION.md` | Teks diberikan dalam percakapan; dibaca | Klarifikasi awal bahwa Rp50m dan Rp100m adalah contoh; budget fleksibel dan data harus ditelusuri. Klarifikasi terbaru pada prompt 00_07 mengubah interpretasi Rp50m. |
| SRC-00-03 | `SIMTDB_REV05112026_00_03_FINANCE_CLARIFICATION_REAUDIT_AND_TEST_PROMPT.md` | Teks diberikan dalam percakapan; dibaca | Prompt audit sebelumnya; bukan hasil eksekusi. |
| SRC-00-04 | `SIMTDB_REV05112026_00_04_AUDIT_FINANCE_REAUDIT_PROMPT.md` | Hasil audit prompt diberikan dalam percakapan; dibaca | Review dokumen, bukan hasil tes aplikasi. |
| SRC-00-05 | `SIMTDB_REV05112026_00_05_FINANCE_REAUDIT_PROMPT_R01.md` | Teks diberikan dalam percakapan; dibaca | Prompt re-audit utama dan guardrails read-only. |
| SRC-GUARDRAIL | Addendum Audit Execution Control | Teks diberikan dalam percakapan; dibaca | Mengatur read-only, provenance, source coverage, dan file output. |
| SRC-00-06 | `SIMTDB_REV05112026_00_06_FINANCE_CLARIFICATION_REAUDIT.md` | Teks diberikan dalam percakapan; dibaca | Audit Finance sebelumnya; sebagian kesimpulan direvisi di dokumen ini. |
| SRC-00-07 | `SIMTDB_REV05112026_00_07_FINANCE_OWNER_CLARIFICATION_AND_CORRECTION_PROMPT.md` | Teks diberikan oleh pemilik proyek dalam percakapan; dibaca | Klarifikasi terbaru mengenai Rp50m per kejadian/operasi, Rp100m ilustratif, dan kas tersedia. |
| SRC-SOP-16-29 | Gambar SOP cetak halaman 16–29 | Gambar tersedia dan telah ditelaah | Halaman 23–24 relevan untuk dana darurat dan APP Nasional; bukan seluruh SOP. |
| SRC-SOP-49 | Template Permohonan Dana Darurat APP-KWI halaman 49 | `EVIDENCE_NOT_AVAILABLE` | Tidak tersedia sebagai gambar dalam audit ini. |
| SRC-SOP-40-41 | SOP Finance halaman 40–41 | `EVIDENCE_NOT_AVAILABLE` | Tidak tersedia sebagai gambar dalam audit ini. |
| SRC-SOP-62-69 | SOP Procurement/Finance dan dokumen terkait | `EVIDENCE_NOT_AVAILABLE` | Tidak tersedia untuk pemeriksaan langsung dalam audit ini. |
| SRC-CHR-020 | Correction & Harmonization Register, CHR-020 | Teks diberikan sebelumnya; dibaca | Isu sumber dana dan perbedaan nominal; status diperbarui pada bagian 18. |
| SRC-REPO | Repository aplikasi | `EVIDENCE_NOT_AVAILABLE` | Repository, branch, commit, file, dan scope pencarian tidak tersedia. |
| SRC-DB | Database, schema, migrations, seeds | `EVIDENCE_NOT_AVAILABLE` | Tidak diperiksa dan tidak diakses. |
| SRC-TEST | Test suite atau hasil test aktual | `EVIDENCE_NOT_AVAILABLE` | Tidak ada test run atau evidence eksekusi. |

### 2.2 Pernyataan coverage

Audit ini menggunakan seluruh dokumen sebelumnya yang tersedia dalam percakapan dan gambar SOP halaman cetak 16–29. Audit ini **tidak** mengklaim telah memeriksa:

- Seluruh SOP halaman 1–95.
- Template halaman 49.
- Repository, branch, commit, source code, database, migration, atau seed.
- Test suite atau aplikasi berjalan.
- Bukti formal organisasi di luar klarifikasi yang diberikan dalam percakapan.

### 2.3 Tidak ada implementasi

Tidak dilakukan:

- Perubahan source code atau file proyek.
- Perubahan database, schema, atau data.
- Migration, seed, atau deployment.
- Integration test, database test, atau test suite.
- Perintah atau tindakan yang mengubah lingkungan proyek.

---

## 3. Corrected Provenance and Source Hierarchy

### 3.1 Kamus provenance

| Label | Makna |
|---|---|
| `SOP_CONFIRMED` | Didukung langsung oleh bagian SOP asli yang tersedia dan telah diperiksa. |
| `CLARIFIED_BY_PROJECT_OWNER` | Dinyatakan langsung oleh pemilik proyek dalam klarifikasi yang diberikan. |
| `ORG_DECISION_CONFIRMED` | Didukung keputusan organisasi formal yang dapat diidentifikasi. |
| `PROJECT_REQUIREMENT_STATED_IN_ADDENDUM` | Tertulis dalam addendum proyek; penerimaan/otorisasi terpisah belum jelas. |
| `PENDING_OWNER_ACCEPTANCE` | Memerlukan persetujuan eksplisit pemilik proyek. |
| `TECHNICAL_RECOMMENDATION` | Rekomendasi desain teknis; bukan aturan SOP atau policy organisasi. |
| `PENDING_DESIGN_DECISION` | Memerlukan keputusan desain domain/arsitektur. |
| `PENDING_ORG_DECISION` | Memerlukan keputusan organisasi atau policy Finance. |
| `SOURCE_CONFLICT` | Sumber yang tersedia berbeda atau belum terselaraskan. |
| `EVIDENCE_NOT_AVAILABLE` | Bukti sumber tidak tersedia. |
| `TEST_DESIGNED` | Skenario tes dirancang; belum dijalankan. |
| `TEST_EXECUTED_PASS` | Tes benar-benar dijalankan dan evidence tersedia. |
| `TEST_EXECUTED_FAIL` | Tes benar-benar dijalankan dan evidence tersedia. |
| `BLOCKED_BY_MISSING_POLICY` | Tidak dapat diputuskan karena policy belum disahkan. |
| `BLOCKED_BY_MISSING_SOURCE` | Tidak dapat diputuskan karena sumber belum tersedia. |

Tidak ada tes pada dokumen ini yang berstatus `TEST_EXECUTED_PASS` atau `TEST_EXECUTED_FAIL`.

### 3.2 Hierarki sumber domain-specific

Sumber digunakan sesuai domain:

| Domain | Sumber yang mengendalikan | Perlakuan terhadap konflik |
|---|---|---|
| Makna dan tujuan kebijakan proyek SIM-TDB | Klarifikasi langsung pemilik proyek yang diberikan | Catat sebagai `CLARIFIED_BY_PROJECT_OWNER`; jangan menyatakan sebagai perubahan teks SOP. |
| Prosedur operasi | SOP asli yang dapat diverifikasi | Jika klarifikasi tampak berbeda dari redaksi SOP, catat `SOURCE_CONFLICT` dan minta konfirmasi otoritas yang berwenang. |
| Role, mandat, dan delegasi | Keputusan organisasi formal | Jangan menyimpulkan jabatan/otoritas dari nama fungsi atau akses teknis. |
| Finance/accounting treatment | Pedoman Finance yang disahkan | Jika belum tersedia, tandai `PENDING_ORG_DECISION`. |
| Desain arsitektur/data | Keputusan teknis yang diterima | Usulan desain tetap `TECHNICAL_RECOMMENDATION` sampai diterima. |
| Hasil pengujian | Evidence eksekusi aktual | Test yang belum dijalankan hanya `TEST_DESIGNED`. |

**Koreksi prinsip sumber:** Klarifikasi proyek memberi arahan untuk desain SIM-TDB, tetapi tidak secara diam-diam mengganti atau mengubah SOP formal. Bila teks SOP yang terlihat berbeda, perbedaan dicatat sampai direkonsiliasi secara formal.

---

## 4. Updated Owner Clarification Register

| ID | Pernyataan pemilik proyek | Provenance | Batas |
|---|---|---|---|
| OCL-01 | Rp100.000.000 yang muncul sebagai contoh nilai kebutuhan dana merupakan ilustrasi saja; bukan nilai baku, kewajiban, maksimum, cap, atau threshold approval. | `CLARIFIED_BY_PROJECT_OWNER` | Tidak digunakan sebagai default, validasi, workflow condition, atau limit sistem. |
| OCL-02 | Maksimum pengeluaran dana darurat TSKKM untuk satu kejadian/operasi respons adalah Rp50.000.000. | `CLARIFIED_BY_PROJECT_OWNER` | Bukan nilai wajib yang harus dihabiskan; pemakaian aktual dapat lebih kecil. |
| OCL-03 | Pengeluaran aktual untuk satu kejadian/operasi juga dibatasi oleh kas darurat yang benar-benar tersedia dan berlaku untuk pengeluaran tersebut. | `CLARIFIED_BY_PROJECT_OWNER` untuk prinsip batas kas | Definisi eligible available cash dan cara menghitungnya belum ditentukan. |
| OCL-04 | Setiap kejadian/operasi yang berbeda dapat memiliki pengeluaran dana darurat sendiri, masing-masing tunduk pada maksimum per kejadian/operasi dan kas tersedia secara keseluruhan. | `CLARIFIED_BY_PROJECT_OWNER` | Batas antara satu kejadian dan beberapa operasi di bawah satu kejadian masih memerlukan definisi formal. |
| OCL-05 | Total pengeluaran untuk beberapa kejadian berbeda boleh melebihi Rp50.000.000, selama setiap kejadian/operasi patuh terhadap limit masing-masing dan kas mencukupi. | `CLARIFIED_BY_PROJECT_OWNER` | Tidak menghapus approval atau pembatasan sumber dana lain. |
| OCL-06 | Rp50.000.000 bukan cap global semua aktivitas TSKKM, program, kejadian gabungan, atau transaksi lain yang tidak terkait dana darurat untuk control unit tersebut. | `CLARIFIED_BY_PROJECT_OWNER` | Cakupan dana/jenis transaksi harus diidentifikasi sebelum kontrol diterapkan. |
| OCL-07 | Fleksibilitas jumlah dan banyaknya kejadian tidak mengubah kewenangan persetujuan. | `CLARIFIED_BY_PROJECT_OWNER` | Authority harus berasal dari mandat/delegasi formal yang terverifikasi. |

### Pernyataan yang bukan klarifikasi langsung pemilik proyek

Hal-hal berikut tidak boleh dilabeli `CLARIFIED_BY_PROJECT_OWNER` kecuali terdapat persetujuan tambahan:

- Agregasi otomatis oleh sistem berdasarkan parent incident.
- Anti-splitting controls untuk voucher, sektor, aktivitas, user, atau sub-record.
- Reservasi dana saat approval.
- Cara perhitungan kas available.
- Perlakuan komitmen atau payment instruction yang belum dibayar.
- Aturan concurrency dan locking.
- Model entity dan cardinality.
- Workflow status dan state transitions.
- Formula remaining budget.
- Accounting recognition.
- Perilaku partial approval.

Item tersebut merupakan `TECHNICAL_RECOMMENDATION`, `PENDING_DESIGN_DECISION`, atau `PENDING_ORG_DECISION`.

---

## 5. SOP Finance Evidence Ledger dan Konflik Nominal

| Rujukan | Isi yang tampak pada sumber | Interpretasi sistem | Status / batas |
|---|---|---|---|
| SOP halaman 23 | Halaman terlihat menyebut sumber dana darurat/awal dan persetujuan pengeluaran oleh Ketua TSKKM. Teks angka Rp50.000.000 juga tampak pada konteks dana awal. | Catat sebagai bukti SOP terkait dana awal dan approval oleh Ketua TSKKM. | `SOP_CONFIRMED` untuk teks yang terlihat; transkripsi perlu dicocokkan dengan scan jelas. |
| Klarifikasi terbaru pemilik proyek | Rp50m merupakan maksimum per satu kejadian/operasi, bukan jumlah wajib dan bukan cap global; aktual juga dibatasi kas tersedia. | Gunakan sebagai baseline kebijakan proyek untuk rancangan kontrol. | `CLARIFIED_BY_PROJECT_OWNER`. |
| Perbedaan pembacaan halaman 23 dan klarifikasi | Redaksi halaman 23 yang tampak dapat dibaca sebagai nominal tertentu, sedangkan klarifikasi mendefinisikannya sebagai maksimum per kejadian/operasi. | Jangan diam-diam mengubah makna SOP; jangan juga mengabaikan klarifikasi pemilik proyek. | `SOURCE_CONFLICT`; perlu konfirmasi/keputusan formal agar pemetaan SOP dan policy proyek terdokumentasi. |
| SOP halaman 24 | Dana APP Nasional diakses melalui KARINA-KWI dengan SITREP dan rencana penggunaan anggaran sebagaimana ringkasan halaman yang terlihat. | Pertahankan keterlacakan dokumen sumber. | `SOP_CONFIRMED` untuk teks yang terlihat; alur lengkap belum diperiksa. |
| SOP halaman 24 | Halaman menyebut kategori pengeluaran kantor yang tidak ditanggung dana APP Nasional. | Pertahankan larangan sebagaimana sumber; jangan menciptakan kategori atau enforcement tambahan. | `SOP_CONFIRMED` secara parsial; verifikasi scan dan konteks lengkap dibutuhkan sebelum automated blocking. |
| SOP halaman 49 | Materi lama menyebut Rp100m pada template permohonan dana APP-KWI. | Nominal diperlakukan ilustratif berdasarkan klarifikasi pemilik proyek. | Makna nominal `CLARIFIED_BY_PROJECT_OWNER`; template/field `EVIDENCE_NOT_AVAILABLE`. |

### Aturan penanganan konflik

- Jangan mengubah teks atau nilai dalam SOP historis.
- Jangan memakai nominal Rp50m sebagai global cap.
- Jangan memakai Rp100m sebagai cap, default, atau threshold.
- Gunakan klarifikasi pemilik proyek untuk merancang batas per kejadian.
- Tandai perbedaan dengan teks SOP sebagai `SOURCE_CONFLICT`.
- Minta konfirmasi tertulis dari otoritas yang berwenang untuk menetapkan bagaimana klarifikasi diadopsi sebagai interpretasi operasional resmi.

---

## 6. Corrected Financial Business Rule Register

| Rule ID | Business rule | Provenance | Implementasi final |
|---|---|---|---|
| FIN-BR-OWNER-01 | Rp100m merupakan contoh ilustratif saja; bukan nilai tetap, cap, default wajib, atau approval threshold. | `CLARIFIED_BY_PROJECT_OWNER` | Dilarang menjadi rule aplikasi. |
| FIN-BR-OWNER-02 | Maksimum pengeluaran dana darurat TSKKM untuk satu kejadian/operasi respons adalah Rp50m. | `CLARIFIED_BY_PROJECT_OWNER` | Batas berlaku per control unit; definisi incident/operation final perlu keputusan. |
| FIN-BR-OWNER-03 | Aktual dana darurat untuk control unit tidak boleh melebihi nilai yang lebih rendah antara Rp50m dan kas eligible yang tersedia untuk pengeluaran tersebut. | `CLARIFIED_BY_PROJECT_OWNER` untuk kedua batas; mechanics `TECHNICAL_RECOMMENDATION` | Cash basis dan event yang mengonsumsi limit pending. |
| FIN-BR-OWNER-04 | Setiap kejadian/operasi berbeda dapat memiliki pengeluaran dana darurat sendiri, tunduk pada limit per kejadian dan kontrol kas total. | `CLARIFIED_BY_PROJECT_OWNER` | Tidak berlaku pada seluruh funding source/program secara otomatis. |
| FIN-BR-OWNER-05 | Aggregate pengeluaran beberapa kejadian dapat melebihi Rp50m apabila setiap kejadian patuh dan kas cukup. | `CLARIFIED_BY_PROJECT_OWNER` | Tidak merupakan izin melewati per-incident limit. |
| FIN-BR-OWNER-06 | Rp50m bukan cap global semua insiden/aktivitas/program TSKKM. | `CLARIFIED_BY_PROJECT_OWNER` | Batasi aturan pada pengeluaran dana darurat yang termasuk cakupan. |
| FIN-BR-OWNER-07 | Rp50m/Rp100m tidak boleh menjadi default mandatory atau approval threshold otomatis. | `CLARIFIED_BY_PROJECT_OWNER` | Cari dan uji seluruh rules/configuration saat repository tersedia. |
| FIN-BR-OWNER-08 | Fleksibilitas anggaran atau multi-incident tidak mengubah authority persetujuan. | `CLARIFIED_BY_PROJECT_OWNER` | Approval tetap berdasarkan mandat/delegasi yang diverifikasi. |
| FIN-BR-OWNER-09 | Anggaran dapat disesuaikan berdasarkan kebutuhan program/kegiatan, kondisi bencana, funding source, dan anggaran yang disetujui. | `CLARIFIED_BY_PROJECT_OWNER` | Tidak memberi kewenangan belanja tanpa approval. |
| FIN-BR-OWNER-10 | Proposed budget, approved budget, budget revision, actual expenditure, dan remaining budget dibedakan. | `CLARIFIED_BY_PROJECT_OWNER` | Model teknis dan policy calculation tetap perlu dirancang/disetujui. |
| FIN-BR-OWNER-11 | Budget revision memiliki histori, alasan, aktor, waktu, dan referensi persetujuan. | `CLARIFIED_BY_PROJECT_OWNER` | State/workflow revision tetap pending. |
| FIN-BR-OWNER-12 | Sumber pendanaan dapat ditelusuri. | `CLARIFIED_BY_PROJECT_OWNER` | Tidak menetapkan cardinality sumber pendanaan. |
| FIN-BR-OWNER-13 | Angka transaksi/laporan bersumber dari data aktual yang tercatat dan disahkan. | `CLARIFIED_BY_PROJECT_OWNER` | Status transaksi yang diakui untuk pelaporan belum didefinisikan. |
| FIN-BR-SOP-01 | Pengeluaran dana darurat memerlukan persetujuan Ketua TSKKM sebagaimana halaman 23 yang terlihat. | `SOP_CONFIRMED` parsial | Identitas/mandat dan mapping ke role sistem perlu verifikasi; konflik interpretasi nilai dicatat terpisah. |
| FIN-BR-SOP-02 | Pembatasan APP Nasional pada halaman 24 dipertahankan sesuai kategori yang terbaca. | `SOP_CONFIRMED` parsial | Enforcement mode belum ditetapkan. |
| FIN-BR-TECH-01 | Sistem mengagregasi pengeluaran dana darurat yang terkait pada control unit kejadian/operasi yang sama. | `TECHNICAL_RECOMMENDATION` | Batas control unit harus disahkan. |
| FIN-BR-TECH-02 | Sektor, aktivitas, voucher, user, atau banyak transaksi tidak mereset limit control unit. | `TECHNICAL_RECOMMENDATION` berdasarkan kebijakan | Mekanisme anti-splitting harus diuji. |
| FIN-BR-TECH-03 | Sistem mengontrol kas eligible secara global pada fund pool terkait. | `TECHNICAL_RECOMMENDATION` | Definisi kas, reservation, dan concurrency basis pending. |
| FIN-BR-TECH-04 | Multiple disbursement untuk satu control unit dihitung kumulatif. | `TECHNICAL_RECOMMENDATION` | Event konsumsi cap perlu policy. |
| FIN-BR-TECH-05 | Permintaan bersamaan tidak boleh secara kumulatif melewati cap per control unit atau kas eligible. | `TECHNICAL_RECOMMENDATION` | Perlu desain atomic reservation/commit dan policy cash. |
| FIN-BR-PENDING-01 | Definisi control unit: satu incident, satu response operation, atau hubungan keduanya. | `PENDING_ORG_DECISION` / `PENDING_DESIGN_DECISION` | Jangan memisahkan cap per sub-operation tanpa persetujuan. |
| FIN-BR-PENDING-02 | Event yang mengonsumsi limit: request, approval, reservation, disbursement authorization, atau cash release. | `PENDING_ORG_DECISION` | Jangan finalisasi workflow. |
| FIN-BR-PENDING-03 | Eligible available emergency cash dan perlakuan komitmen/outstanding payment. | `PENDING_ORG_DECISION` | Jangan menghitung kas dengan asumsi. |
| FIN-BR-PENDING-04 | Partial approval atau permintaan revisi saat cash kurang. | `PENDING_ORG_DECISION` | Tidak boleh mengarang keputusan workflow. |
| FIN-BR-PENDING-05 | Formula remaining budget/accounting recognition. | `PENDING_ORG_DECISION` | Bukan formula yang sama dengan kontrol kas darurat. |

---

## 7. Per-Incident Emergency-Fund Limit Model

### 7.1 Prinsip kontrol

Klarifikasi pemilik proyek menyatakan batas maksimal dana darurat per kejadian/operasi. Secara konseptual:

`Batas maksimum dana darurat untuk satu control unit = MIN(Rp50.000.000, eligible available emergency cash yang berlaku)`

Formula ini menyatakan **dua batas independen**:

1. **Incident/operation cap:** Rp50m.
2. **Cash cap:** kas eligible yang tersedia.

Formula ini bukan formula accounting, bukan penetapan remaining budget, dan bukan keputusan tentang transaksi mana yang telah “mengonsumsi” limit.

### 7.2 Multi-incident aggregate

`Total dana darurat lintas kejadian = jumlah dana darurat untuk semua kejadian/control unit yang berbeda`

Total dapat melebihi Rp50m jika:

- Control unit benar-benar berbeda dan terdaftar secara sah.
- Setiap unit tidak melampaui cap per unit.
- Total pengeluaran/reservasi yang dihitung menurut policy tidak melampaui kas eligible.
- Approval dan restriction funding source tetap dipenuhi.

### 7.3 Contoh kebijakan yang diberikan pemilik proyek

Misalkan kas eligible tersedia Rp200.000.000:

| Kejadian | Pengeluaran | Hasil batas per kejadian | Hasil kontrol kas |
|---|---:|---|---|
| Banjir A | Rp50.000.000 | Dalam batas | Dalam contoh total |
| Longsor B | Rp35.000.000 | Dalam batas | Dalam contoh total |
| Banjir C | Rp45.000.000 | Dalam batas | Dalam contoh total |
| Kebakaran D | Rp20.000.000 | Dalam batas | Dalam contoh total |
| **Total** | **Rp150.000.000** | Masing-masing ≤ Rp50m | Dapat diterima sesuai contoh, dengan syarat approval dan cash controls terpenuhi |

Total lebih besar dari Rp50m **tidak** melanggar kebijakan karena pengeluaran dibagi pada kejadian yang berbeda, dan setiap kejadian mematuhi cap masing-masing.

### 7.4 Batas yang belum diputuskan

Belum ditentukan apakah limit dikonsumsi oleh:

- Permintaan dana yang diajukan.
- Persetujuan dana.
- Reservasi cash.
- Instruksi pembayaran.
- Dana yang dilepas secara aktual.
- Event lain yang ditentukan pedoman Finance.

Untuk mencegah overspending selama kebijakan belum diputuskan, proposal teknis adalah menahan/mereservasi dana pada tahap yang disetujui organisasi dan mengembalikan reservasi secara terkontrol bila transaksi dibatalkan. Proposal ini **bukan** policy yang telah dikonfirmasi.

---

## 8. Global Available-Cash Control Model

### 8.1 Prinsip

Kontrol ketersediaan kas global tidak sama dengan perhitungan budget atau remaining budget.

Jangan menyamakan:

- Budget.
- Kas/bank yang benar-benar tersedia.
- Pengeluaran kas aktual.
- Expense recognition.
- Commitment/encumbrance.
- Invoice.
- Payment.
- Goods receipt atau inventory posting.
- Restriksi penggunaan dana.

### 8.2 Konsep yang perlu dipisahkan

| Konsep | Tujuan | Status |
|---|---|---|
| Emergency-fund pool | Mengidentifikasi kumpulan dana darurat yang menjadi sumber pengeluaran | Katalog, owner, dan cakupan perlu disahkan |
| Eligible cash balance | Kas yang benar-benar boleh digunakan untuk pengeluaran tertentu | Definisi/policy belum tersedia |
| Reserved amount | Nilai yang dicadangkan untuk permintaan/approval yang belum dicairkan | Penanganan sebagai cash control merupakan rekomendasi teknis; policy pending |
| Released/disbursed amount | Dana yang telah dikeluarkan sesuai event yang disahkan | Definisi event yang mengonsumsi kontrol masih pending |
| Outstanding payment instruction | Instruksi yang belum diselesaikan | Perlakuan terhadap cash basis pending |
| Refund/reversal | Pengembalian atau koreksi dana | Treatment dan hubungan ke transaksi asal pending |
| Restricted cash | Kas dengan pembatasan sumber atau tujuan | Identifikasi dan aturan penggunaan memerlukan policy/sumber yang sah |

### 8.3 Risiko concurrency

Jika dua kejadian berbeda meminta dana hampir bersamaan, pemeriksaan saldo yang dilakukan terpisah tanpa pengendalian atomik dapat membuat keduanya tampak tersedia walau jika digabungkan kas tidak mencukupi.

Rekomendasi teknis:

- Evaluasi seluruh permintaan bersamaan terhadap satu cash pool yang disepakati.
- Gunakan mekanisme reservasi/otorisasi yang mencegah dua keputusan menggunakan saldo yang sama.
- Ulangi validasi pada saat event pengeluaran yang ditentukan policy terjadi.
- Simpan hubungan antara request, approval, reservation, disbursement, dan reversal.
- Gunakan idempotency sehingga retry tidak mengurangi kas atau mengonsumsi cap dua kali.
- Jangan menetapkan status transaksi atau cash basis final tanpa pedoman Finance.

Semua mekanisme tersebut `TECHNICAL_RECOMMENDATION`; treatment resmi terhadap commitment/reservation/outstanding payments tetap `PENDING_ORG_DECISION`.

---

## 9. Incident/Operation Identity and Anti-Splitting Analysis

### 9.1 Entitas konseptual yang dibutuhkan

| Konsep | Peran |
|---|---|
| Incident identity | Identitas kejadian bencana di dunia nyata; menautkan laporan masuk dan catatan lain. |
| Response operation | Catatan operasi yang dibuat untuk menjalankan respons, jika keputusan Respons mengizinkan. |
| Emergency-fund control unit | Identitas yang dipakai untuk mengagregasi limit per kejadian/operasi; belum diputuskan apakah sama dengan incident atau operation. |
| Emergency-fund request/disbursement | Permintaan, persetujuan, reservasi, atau pengeluaran dana yang tertaut ke control unit dan sumber dana. |
| Sector/activity | Rincian kegiatan dalam satu kejadian/operasi; tidak boleh otomatis mereset cap. |
| Approval/evidence | Bukti mandat, keputusan, dokumen, dan catatan otorisasi. |

### 9.2 Anti-splitting control

Kontrol teknis yang disarankan:

- Jangan menghitung batas per voucher, sektor, activity, user, department, atau request.
- Agregasikan transaksi pada control unit kejadian/operasi yang disetujui.
- Retry dengan idempotency key yang sama tidak boleh membuat disbursement atau konsumsi cap ganda.
- Kemungkinan duplikasi incident harus ditandai untuk review; merge otomatis tidak disarankan tanpa prosedur.
- Perubahan relasi incident/operation harus terversi dan diaudit.
- Setiap reversal/refund harus tertaut ke transaksi asal dan mengikuti treatment kas yang disahkan.

### 9.3 Keputusan penting: incident versus operation

Klarifikasi pemilik proyek menggunakan frasa “satu kejadian/operasi tanggap darurat”, tetapi belum memastikan apakah:

- Satu real-world incident selalu mempunyai satu aggregate cap Rp50m; atau
- Satu incident yang lebih besar dapat memiliki beberapa response operations independen, masing-masing dengan cap tersendiri.

**Rekomendasi sementara untuk mencegah circumvention:**

> Sampai ada keputusan formal, agregasikan di bawah parent incident dan jangan mereset cap hanya karena dibuat sektor, activity, voucher, team, atau sub-record baru.

Status rekomendasi tersebut: `TECHNICAL_RECOMMENDATION` dan `PENDING_ORG_DECISION`; bukan tambahan klarifikasi langsung dari pemilik proyek.

### 9.4 Pertanyaan keputusan

1. Apakah satu kejadian dunia nyata selalu memiliki satu cap agregat Rp50m?
2. Dalam kondisi apa beberapa operasi boleh dianggap independent untuk cap dana darurat?
3. Siapa yang mengesahkan bahwa dua operasi merupakan operasi yang berbeda?
4. Apakah parent incident selalu menjadi control unit konservatif?
5. Bagaimana insiden duplikat/kejadian berulang di lokasi yang sama dibedakan?
6. Apakah limit dihitung berdasarkan total request, approved reservation, atau cash disbursement?

---

## 10. Funding Source and Restriction Model

### 10.1 Funding source cardinality — alternatif

| Alternatif | Model konseptual | Kelebihan | Risiko/dampak | Status |
|---|---|---|---|---|
| A — Satu sumber per budget | Setiap budget memiliki satu funding source | Pelaporan dan kontrol sederhana | Tidak mendukung campuran sumber bila diperlukan; dapat memaksa duplikasi budget | `PENDING_DESIGN_DECISION` |
| B — Banyak sumber per budget | Budget dapat merujuk beberapa funding source | Mendukung beberapa sumber untuk satu program | Tanpa allocation record, nilai per sumber tidak jelas | `PENDING_DESIGN_DECISION` |
| C — Allocation per budget line/expense | Setiap line/expense dapat memiliki satu atau beberapa allocation record | Mendukung rekonsiliasi granular | Membutuhkan aturan jumlah, revisi, sisa alokasi, dan laporan | `PENDING_DESIGN_DECISION` |

### 10.2 Pertanyaan cardinality

- Apakah satu program/aktivitas boleh menerima dana dari beberapa sumber?
- Apakah satu pengeluaran bisa dibagi antara beberapa sumber?
- Alokasi dilakukan pada level program, activity, budget line, request, commitment, atau transaksi?
- Apakah total alokasi harus sama dengan nilai budget/expense?
- Bagaimana sumber dana direvisi dan ditelusuri?

Jangan menetapkan alokasi multi-sumber sebagai policy tanpa keputusan.

### 10.3 Batas penggunaan dana APP Nasional yang terlihat

Gambar SOP halaman 24 yang tersedia menyebut kategori biaya kantor berikut dalam daftar yang tidak dibiayai oleh dana APP Nasional:

- Gaji staf.
- Perawatan gedung.
- Perlengkapan/alat tulis kantor.
- Perawatan kendaraan harian kantor.
- Komunikasi harian kantor dan staf.
- Alkohol/minuman keras, rokok, dan minuman suplemen.

Status: `SOP_CONFIRMED` secara parsial dari gambar yang tersedia.

Tidak ditentukan oleh audit ini:

- Cara memetakan kata-kata SOP ke expense categories sistem.
- Pengecualian.
- Apakah validasi menjadi hard block, warning, manual review, atau informational.
- Apakah daftar tersebut lengkap pada konteks pendanaan terkait.

Jangan membuat kategori larangan baru atau mengaktifkan automatic blocking tanpa verifikasi sumber dan keputusan enforcement.

---

## 11. Actual Expenditure / Cash Disbursement Source-of-Truth Analysis

### 11.1 Fakta yang berbeda

Jangan menyamakan:

- Permintaan dana.
- Approved budget.
- Reservasi.
- Cash availability.
- Cash disbursement/release.
- Payment.
- Actual expenditure.
- Expense recognition.
- Commitment.
- Invoice.
- Stock receipt.

Batas Rp50m adalah kontrol atas **pengeluaran dana darurat per kejadian/operasi**, tetapi event tepat yang mengonsumsi cap belum ditentukan oleh materi yang tersedia.

### 11.2 Sumber kanonis

Model Finance aktual dan repository tidak tersedia. Oleh sebab itu:

- **Canonical source yang sudah diterapkan:** `EVIDENCE_NOT_AVAILABLE`.
- **Target rekomendasi:** setiap fakta keuangan memiliki satu source of truth di Finance sesuai maknanya.
- **Actual expenditure:** jangan mengasumsikan payment sebagai sumber kanonis tanpa kebijakan Finance yang disahkan.
- **Cash disbursement:** harus dibedakan dari budget, commitment, expense recognition, dan remaining budget.
- **Laporan:** mengambil angka dari catatan Finance yang diakui untuk pelaporan sesuai policy yang disahkan.

### 11.3 Kontrol nilai ganda

- Jangan menyimpan dua nilai aktual yang dapat diedit untuk transaksi yang sama.
- Report/reference idealnya merujuk transaksi kanonis dan menurunkan nominal dari sana.
- Snapshot hanya jika ada alasan terdokumentasi, sumber/version, waktu snapshot, status immutable, dan aturan rekonsiliasi.
- Jika nominal report berbeda dari transaksi sumber, tampilkan discrepancy; jangan menimpa atau menyamarkan transaksi asal.
- Koreksi mengikuti prosedur yang sah dan mempertahankan histori.

---

## 12. Finance–Procurement–Logistics Integration

| Record/process | Pemilik data target | Relasi lintas modul | Implikasi dana darurat | Batas/pending |
|---|---|---|---|---|
| Request/requisition | Procurement | Program/activity/incident/operation jika model mengizinkan | Tidak otomatis merupakan cash disbursement atau expense | Workflow dan sumber halaman lengkap belum diperiksa |
| Quotation/bid analysis | Procurement | Request/supplier | Evidence pengadaan; tidak otomatis mengonsumsi cap cash | Template dan persetujuan belum seluruhnya diverifikasi |
| Purchase order | Procurement | Request/supplier/budget reference | Mungkin menjadi commitment jika policy menetapkan; tidak otomatis disbursement | Perlakuan commitment pending |
| Physical receipt/Goods Received Note | Warehouse/Logistics | PO/items/warehouse | Penerimaan barang tidak otomatis sama dengan cash release | Pemisahan Finance dan physical inspection dipertahankan |
| Invoice | Finance/document owner sesuai governance | Supplier/PO/receipt jika berlaku | Tidak otomatis sama dengan pembayaran atau cash disbursement | Urutan invoice/GRN/payment belum ditetapkan |
| Payment voucher | Finance | Invoice/request/approval evidence | Dokumen proses pembayaran | Template/authority belum lengkap |
| Payment/cash release | Finance | Voucher/bank/fund source/source document | Kemungkinan event yang mengonsumsi cash control; perlu policy | Event tepat belum disahkan |
| Expense recognition | Finance/accounting | Transaction/source documents | Menentukan angka expense dalam report | Accounting treatment pending |
| Commitment/reservation | Finance/Procurement sesuai keputusan | PO/request/approval | Dapat memengaruhi available cash hanya bila policy menentukan | Definisi dan treatment pending |
| Inventory posting | Inventory/Warehouse | GRN/stock movement | Bukan pembayaran dan bukan automatically expense recognition | Inventory Movement tetap milik domain Inventory |
| Refund/reversal | Finance | Transaksi asal | Harus tertaut ke asal; pengaruh pada cash/cap ditentukan policy | Treatment pending |
| Financial accountability report | Finance/reporting layer | Finance transactions/documents | Nilai harus dapat ditelusuri ke sumber keuangan kanonis | Format/approval lengkap belum tersedia |

### Integritas lintas modul

- Tidak ada penggantian sumber data dengan angka laporan.
- Reconciliation menampilkan selisih; tidak menimpa sumber otomatis.
- Event lintas modul yang membuat transaksi perlu idempotency.
- Procurement request, PO, invoice, payment, disbursement, expense, goods receipt, dan stock posting tetap terpisah.
- Jangan menyimpulkan urutan invoice, GRN, atau payment dari audit ini.

---

## 13. Updated Finance Entity Registry and Data Dictionary (Logical Only)

Nama entitas di bawah bersifat konseptual, bukan nama tabel final.

### 13.1 Entity Registry

| Entitas konseptual | Tujuan | Relasi penting | Status |
|---|---|---|---|
| Incident | Identitas kejadian dunia nyata | Menautkan incoming reports; mungkin menjadi parent operasi | Pemisahan incident/report/operation sudah menjadi baseline proyek; model aktual belum tersedia |
| Response operation | Merekam operasi respons | Tertaut ke incident dan operasi/program terkait | Apakah satu incident dapat memiliki beberapa independently capped operation: `PENDING_ORG_DECISION` |
| Emergency-fund control unit | Menentukan ruang lingkup agregasi cap Rp50m | Merujuk incident atau operation sesuai keputusan | `PENDING_DESIGN_DECISION` |
| Emergency-fund request | Mencatat permintaan dana | Control unit, source fund, approval evidence | Lifecycle/request status pending |
| Emergency-fund approval/reservation reference | Mencatat approval atau reservasi bila policy menetapkan | Request, authority, source, amount | Tidak menetapkan event konsumsi cap |
| Emergency-fund disbursement | Mencatat kas yang dikeluarkan | Control unit, fund pool, payment evidence | Status/canonical source belum tersedia |
| Emergency-fund adjustment/reversal | Mencatat koreksi, refund, reversal | Link ke transaksi asal | Finance policy pending |
| Emergency-fund cash pool | Membedakan kas darurat yang relevan untuk control | Funding source/account/cash records | Owner dan availability basis pending |
| Cash availability snapshot/ledger reference | Bukti/basis available cash pada waktu tertentu | Cash source, timestamp, policy version | Snapshot design merupakan usulan; policy pending |
| Budget proposal | Mencatat anggaran yang diajukan | Program/activity/funding source | Pemisahan tahap diklarifikasi; relasi pending |
| Approved budget record | Anggaran yang disetujui | Approval/authority evidence | Authority dan status pending |
| Budget revision record | Histori revisi | Budget/version/reason/actor/time/approval | Metadata wajib diklarifikasi; workflow states pending |
| Funding source reference | Identitas sumber dana | Budget/transaction/allocation | Traceability diklarifikasi; cardinality/owner pending |
| Funding allocation | Alokasi nilai ke sumber dana | Budget line/expense/source | Hanya jika model multi-source disetujui |
| Financial transaction | Catatan Finance kanonis untuk fakta transaksi sesuai domain | Document/source/fund/incident reference | Model aktual tidak tersedia |
| Financial report view | Menyajikan angka turunan | Transaction/source records | Bukan source of truth |
| Approval authority record | Mandat/delegasi yang sah | Actor/action/scope/document/effective period | Bukti formal belum tersedia |

### 13.2 Logical field requirements

| Entitas | Field logis | Aturan |
|---|---|---|
| Incident | Incident ID, identity/reference, duplicate-review status | Tidak boleh membuat kontrol cap per voucher/sector/activity; duplicate matching memerlukan review terkontrol. |
| Response operation | Operation ID, parent incident reference, operation identity/status | Kardinalitas dan kewenangan membentuk operation belum final. |
| Control unit | Control unit ID, incident reference, operation reference, effective scope/version | Tidak boleh menetapkan batas per operation tanpa keputusan yang mendefinisikan independensi operation. |
| Emergency-fund request | Request ID, control unit, requested amount, fund source, creator/time, evidence | Meminta dana tidak otomatis berarti approval atau cash release. |
| Approval/reservation | Approval/reservation ID, authority reference, amount, effective time, status | Status dan kapan memengaruhi cap/kas harus disahkan. |
| Disbursement | Disbursement ID, control unit, fund pool/source, amount, transaction reference, event time | Menautkan kas yang dikeluarkan; status kanonis mengikuti policy Finance. |
| Cash availability | Fund pool/source, available amount, as-of time, basis/policy reference | Definisi eligible cash dan perlakuan outstanding/reserved amounts pending. |
| Budget | Proposed/approved/revision/actual/remaining distinctions | Lima kategori berbeda; formula remaining tidak ditentukan. |
| Revision | Previous/revised values, reason, actor, time, approval reference, version | Histori dipertahankan; revision belum disetujui tidak boleh dianggap efektif sebagai rekomendasi teknis. |
| Funding source | Source ID/code, source evidence, restrictions reference, effective/version status | Restriction tidak boleh ditambah tanpa sumber/persetujuan. |
| Report reference | Source transaction IDs, report period, derivation metadata | Jangan menyediakan editable duplicate actual amount. |

**Physical DB type, nullability final, constraints, index, state names, dan schema tidak ditetapkan.**

---

## 14. Corrected FIN-TEST-01 through FIN-TEST-35

**Catatan umum:** Semua test berstatus `TEST_DESIGNED`, `BLOCKED_BY_MISSING_POLICY`, atau `BLOCKED_BY_MISSING_SOURCE`. Tidak ada test yang dijalankan. Actual result untuk seluruh test: **“not executed.”**

| ID | Tujuan / preconditions / data / langkah | Expected result | Actual result | Status / evidence / dependency |
|---|---|---|---|---|
| FIN-TEST-01 | Uji proposal Rp25m; model validasi harus tersedia. | Tidak ditolak oleh contoh nominal Rp50m/Rp100m; aturan lain hanya dari policy yang sah. | Not executed | `TEST_DESIGNED`; perlu model dan policy validasi. |
| FIN-TEST-02 | Uji proposal Rp75m. | Tidak otomatis terkena threshold contoh Rp50m atau Rp100m. | Not executed | `TEST_DESIGNED`; implementasi belum tersedia. |
| FIN-TEST-03 | Uji proposal Rp250m. | Tidak otomatis ditolak karena melewati nominal ilustratif; approval tetap mengikuti authority policy. | Not executed | `TEST_DESIGNED`; authority matrix diperlukan. |
| FIN-TEST-04 | Proposed budget berbeda dari approved budget; sertakan bukti approval. | Dua nilai dan lifecycle tetap terpisah; approved value mempunyai sumber approval yang sah. | Not executed | `TEST_DESIGNED`; model dan authority belum disahkan. |
| FIN-TEST-05 | Budget revision diajukan tetapi belum disetujui. | Approved baseline yang berlaku tidak berubah sebelum approval/effectivity sesuai policy. | Not executed | `TEST_DESIGNED`; workflow status pending. |
| FIN-TEST-06 | Revisi dengan previous/revised value, reason, actor, time, approval reference. | Seluruh metadata wajib tersimpan dan versi sebelumnya tetap dapat ditelusuri. | Not executed | `TEST_DESIGNED`; kebutuhan metadata diklarifikasi, status workflow pending. |
| FIN-TEST-07 | Uji satu/multi funding source. | Tidak memaksa cardinality berdasarkan asumsi; keputusan model ditandai pending. | Not executed | `BLOCKED_BY_MISSING_POLICY`; perlu keputusan cardinality. |
| FIN-TEST-08 | Uji restriction yang benar-benar tampak di SOP halaman 24. | Tidak ada larangan baru; enforcement mengikuti interpretasi/keputusan yang disahkan. | Not executed | `BLOCKED_BY_MISSING_POLICY`; perlu transkripsi lengkap dan enforcement decision. |
| FIN-TEST-09 | Generate report dari actual transaction model yang telah disetujui. | Nominal diambil dari satu canonical source yang statusnya diakui untuk pelaporan sesuai policy. | Not executed | `BLOCKED_BY_MISSING_SOURCE`; model Finance aktual tidak tersedia. |
| FIN-TEST-10 | Report/reference mencoba menampilkan nilai berbeda dari transaksi sumber. | Perbedaan terdeteksi; tidak di-overwrite atau disembunyikan; koreksi mempunyai histori. | Not executed | `TEST_DESIGNED`; perlu source model dan correction process. |
| FIN-TEST-11 | Hitung remaining budget dengan approved budget, actual, PO, invoice, commitment. | Tidak disebut definitif sebelum basis perhitungan disahkan; jika ada estimasi, basisnya terlihat. | Not executed | `BLOCKED_BY_MISSING_POLICY`; accounting basis pending. |
| FIN-TEST-12 | User memiliki edit permission, tidak memiliki approval authority. | Approval ditolak; edit permission tidak memberi authority. | Not executed | `TEST_DESIGNED`; authority matrix belum tersedia. |
| FIN-TEST-13 | Retry request dengan idempotency key yang sama. | Tidak membuat revision/disbursement/transaction duplikat atau mengonsumsi limit dua kali. | Not executed | `TEST_DESIGNED`; mekanisme teknis belum ada. |
| FIN-TEST-14 | Dua revisi pada budget version yang sama secara bersamaan. | Konflik/stale version terdeteksi; tidak silent overwrite. | Not executed | `TEST_DESIGNED`; policy dan implementation belum ada. |
| FIN-TEST-15 | Refund/reversal terhadap transaksi asal. | Catatan asal tetap ada; reversal terhubung; pengaruh pada cap/kas mengikuti policy yang disahkan. | Not executed | `BLOCKED_BY_MISSING_POLICY`; treatment refund/reversal pending. |
| FIN-TEST-16 | Cari hardcoded nominal pada repository: code/config/seed/validation/workflow/migration/test fixture. | Tidak ada penggunaan Rp50m/Rp100m sebagai cap/default/threshold; dokumentasi contoh bukan rule. | Not executed | `BLOCKED_BY_MISSING_SOURCE`; repository tidak tersedia. |
| FIN-TEST-17 | Threshold selain nilai contoh tidak memiliki authority source formal. | Tidak diaktifkan sebagai policy; status ditolak/ditahan mengikuti governance yang disahkan. | Not executed | `BLOCKED_BY_MISSING_POLICY`; authority policy dan enforcement pending. |
| FIN-TEST-18 | Threshold lain memiliki source formal, scope, version, effective date, authority. | Hanya dipertimbangkan setelah persetujuan organisasi; tidak diinferensikan dari nominal contoh. | Not executed | `BLOCKED_BY_MISSING_SOURCE`; dokumen formal tidak tersedia. |
| FIN-TEST-19 | Multi-source allocation dicoba sebelum cardinality disetujui. | Tidak dianggap valid atau invalid berdasarkan asumsi; tetap pending. | Not executed | `BLOCKED_BY_MISSING_POLICY`. |
| FIN-TEST-20 | Restriction funding source belum diverifikasi. | Tidak menjadi automatic block rule; sumber dan ketidakpastian terlihat. | Not executed | `BLOCKED_BY_MISSING_SOURCE` untuk rule final; enforcement mode pending. |
| FIN-TEST-21 | PO terbuka dan invoice belum dibayar memengaruhi remaining budget. | Tidak menghasilkan angka definitif tanpa kebijakan commitment/accrual. | Not executed | `BLOCKED_BY_MISSING_POLICY`. |
| FIN-TEST-22 | Budget terkait program/activity. | Tidak ada orphan atau ambiguous polymorphic reference setelah relationship disetujui. | Not executed | `BLOCKED_BY_MISSING_SOURCE`; model Program/Activity belum tersedia. |
| FIN-TEST-23 | Report per funding source dari allocation/transaction. | Nilai per sumber direkonsiliasi tanpa double count jika model alokasi disetujui. | Not executed | `BLOCKED_BY_MISSING_POLICY`; cardinality/alokasi pending. |
| FIN-TEST-24 | Satu incident meminta Rp75m, eligible cash Rp100m. | Pengeluaran dana darurat untuk control unit tidak melebihi Rp50m; request harus ditolak atau direvisi sesuai workflow yang disahkan. | Not executed | `TEST_DESIGNED`; event consumption dan partial/revision workflow pending. |
| FIN-TEST-25 | Empat kejadian berbeda meminta Rp50m, Rp35m, Rp45m, Rp20m; cash Rp200m. | Per-incident cap terpenuhi; total Rp150m dapat diizinkan bila authority, cash eligibility, dan approval terpenuhi. | Not executed | `TEST_DESIGNED`; cash basis dan approval policy diperlukan. |
| FIN-TEST-26 | Satu incident meminta Rp50m, eligible cash Rp30m. | Pengeluaran tidak boleh melebihi Rp30m; partial approval versus return for revision tetap pending. | Not executed | `TEST_DESIGNED`; partial approval workflow pending. |
| FIN-TEST-27 | Beberapa voucher untuk satu incident berjumlah Rp55m. | Agregat Rp55m terdeteksi; voucher kedua/berikutnya tidak mereset cap. | Not executed | `TEST_DESIGNED`; control-unit mapping pending. |
| FIN-TEST-28 | Satu incident, banyak sector/activity, total dana darurat Rp55m. | Cap agregat terdeteksi; sector/activity tidak mereset limit. | Not executed | `TEST_DESIGNED`; anti-splitting technical control dan control-unit decision pending. |
| FIN-TEST-29 | Dua incident berbeda masing-masing Rp50m; eligible cash total Rp80m. | Individual cap terpenuhi tetapi total cash control mencegah pengeluaran/reservasi yang melampaui Rp80m. | Not executed | `TEST_DESIGNED`; available-cash basis dan reservation treatment pending. |
| FIN-TEST-30 | Real-world event yang sama dimasukkan dengan dua Incident ID. | Duplikasi/kemungkinan duplikasi dideteksi dan ditandai untuk controlled review; tidak auto-merge tanpa prosedur. | Not executed | `TEST_DESIGNED`; duplicate-review process pending. |
| FIN-TEST-31 | Dua user memproses pengeluaran bersamaan untuk incident berbeda dari cash pool yang sama. | Kontrol kas global mencegah total disbursement/reservation yang dihitung policy melebihi eligible cash. | Not executed | `TEST_DESIGNED`; cash basis dan concurrency design pending. |
| FIN-TEST-32 | Disbursement di-retry setelah network timeout. | Idempotency mencegah duplicate disbursement dan duplicate cap/cash consumption. | Not executed | `TEST_DESIGNED`; implementation belum tersedia. |
| FIN-TEST-33 | Incident yang sama telah mengeluarkan Rp20m dan meminta tambahan Rp35m. | Cumulative Rp55m terdeteksi; tambahan tidak dapat membuat total di atas Rp50m. | Not executed | `TEST_DESIGNED`; event yang mengonsumsi cap pending. |
| FIN-TEST-34 | Budget program non-darurat melebihi Rp50m. | Cap dana darurat per incident tidak diterapkan ke program/budget lain yang tidak termasuk ruang lingkup. | Not executed | `TEST_DESIGNED`; source-fund/domain classification perlu tersedia. |
| FIN-TEST-35 | Rp100m muncul di dokumentasi contoh. | Tidak diperlakukan sebagai cap, default, atau approval threshold sistem. | Not executed | `TEST_DESIGNED`; repository test blocked until source available. |

### Status pelaksanaan tes

Semua hasil aktual: **not executed**.  
Tidak ada klaim aplikasi atau test suite lulus.

---

## 15. Updated Risk Register

| Risk ID | Risiko | Pencegahan | Deteksi | Pemulihan | Status |
|---|---|---|---|---|---|
| FIN-RISK-01 | Rp50m diterapkan sebagai cap global | Scope limit secara eksplisit ke emergency fund per control unit | Tes beberapa incident dan audit konfigurasi | Hentikan rule global; koreksi melalui perubahan terkendali dan audit trail | `CLARIFIED_BY_PROJECT_OWNER`; repository check blocked |
| FIN-RISK-02 | Batas per incident terlewati dengan pemecahan voucher/activity/sector | Agregasi di control unit kanonis dan anti-splitting controls | FIN-TEST-27/28/33 | Blokir/hold transaksi tambahan sesuai workflow yang disahkan; review catatan yang sudah terjadi | `TECHNICAL_RECOMMENDATION`; control unit pending |
| FIN-RISK-03 | Banyak incident menghabiskan kas yang sama secara bersamaan | Kontrol/reservasi cash pool yang konsisten | FIN-TEST-29/31; audit cash ledger | Tahan proses dan rekonsiliasi; jangan diam-diam mengubah transaksi | `TECHNICAL_RECOMMENDATION`; cash basis pending |
| FIN-RISK-04 | Incident yang sama diduplikasi untuk mereset limit | Duplicate detection, controlled incident review, traceable linking | FIN-TEST-30 | Tautkan/rekonsiliasi melalui proses terotorisasi; jangan auto-merge | `TECHNICAL_RECOMMENDATION`; duplicate policy pending |
| FIN-RISK-05 | Operasi terpisah dibuat untuk memperoleh cap tambahan | Definisi independent operation dan approval formal | Audit parent-child incident/operation dan test anti-splitting | Hold cap reset sampai keputusan formal | `PENDING_ORG_DECISION` |
| FIN-RISK-06 | Rp50m dari SOP dianggap fixed amount, padahal klarifikasi menyebut maximum | Simpan SOP evidence dan owner clarification secara berdampingan | Source traceability review | Minta konfirmasi resmi; jangan menulis ulang SOP | `SOURCE_CONFLICT` |
| FIN-RISK-07 | Kas dianggap sama dengan approved budget atau remaining budget | Modelkan cash, budget, expense, commitment terpisah | Rekonsiliasi source records | Koreksi laporan melalui proses tercatat; jangan menghapus transaksi | `PENDING_ORG_DECISION` |
| FIN-RISK-08 | Reservasi/approved but unpaid tidak dihitung dan mengakibatkan overspend | Tentukan kapan cash dicadangkan/dikonsumsi | Concurrency and cash-control tests | Hold/resolve pending reservations berdasarkan policy | `PENDING_ORG_DECISION` |
| FIN-RISK-09 | Approval authority disimpulkan dari role, assignment, atau nominal | Authority registry terpisah dari permission dan assignment | Negative approval tests | Cabut hak salah dan audit semua transaksi terdampak | `PENDING_ORG_DECISION` |
| FIN-RISK-10 | Actual expenditure disalin dalam report dan berbeda dari transaksi | Satu source kanonis; report amount diturunkan | FIN-TEST-09/10 | Tampilkan discrepancy dan koreksi via transaksi/proses sah | `TECHNICAL_RECOMMENDATION` |
| FIN-RISK-11 | Restriction APP Nasional diterapkan terlalu luas atau salah | Transkripsi SOP dan keputusan enforcement sebelum automation | Test kategori berdasarkan sumber | Nonaktifkan aturan yang tidak didukung; review transaksi terdampak | `PENDING_ORG_DECISION` |
| FIN-RISK-12 | Retry menimbulkan pengeluaran atau konsumsi limit ganda | Idempotency key dan duplicate command handling | FIN-TEST-13/32 | Rekonsiliasi dengan bukti request; tidak menghapus history | `TECHNICAL_RECOMMENDATION` |
| FIN-RISK-13 | Refund/reversal mengembalikan kas atau cap secara salah | Aturan hubungan transaction/reversal dan basis cash ditetapkan dahulu | FIN-TEST-15 | Review dan koreksi berdasarkan policy Finance | `PENDING_ORG_DECISION` |

---

## 16. Updated CHR-020 Mapping

| Isu CHR-020 | Status setelah klarifikasi | Catatan |
|---|---|---|
| Sumber pendanaan yang terlihat pada halaman 23 | Sebagian didukung gambar SOP | Perlu pemeriksaan sumber penuh dan tata kelola funding-source. |
| Dana siaga dan dana operasional | Halaman 23 terlihat | Klasifikasi pool dan accounting basis belum lengkap. |
| Persetujuan dana darurat oleh Ketua TSKKM | Halaman 23 terlihat | Identitas, mandat, delegasi, dan relasi ke role SIM-TDB perlu diverifikasi. |
| Rp50 juta | Klarifikasi terbaru menyebut maksimum per satu kejadian/operasi, tidak wajib dan bukan cap global. | `CLARIFIED_BY_PROJECT_OWNER`; terdapat `SOURCE_CONFLICT` interpretasi dengan redaksi halaman 23 yang perlu konfirmasi formal. |
| Rp100 juta pada template halaman 49 | Klarifikasi terbaru menetapkan contoh ilustratif saja. | Makna nominal `CLARIFIED_BY_PROJECT_OWNER`; halaman/template tetap `EVIDENCE_NOT_AVAILABLE`. |
| Beberapa incident dapat menerima dana masing-masing | Dinyatakan dalam prompt klarifikasi terbaru | Setiap kejadian tunduk cap per unit dan total kas tersedia. |
| Total lintas kejadian dapat lebih dari Rp50 juta | Dinyatakan dalam prompt klarifikasi terbaru | Tidak boleh melampaui eligible available cash dan approval yang sah. |
| Batas incident versus operation | Belum pasti apakah beberapa operasi di satu incident mendapat cap terpisah | `PENDING_ORG_DECISION`; rekomendasi konservatif parent incident untuk sementara. |
| Event yang mengonsumsi cap | Belum ditentukan | `PENDING_ORG_DECISION` |
| Definisi eligible available cash | Belum tersedia | `PENDING_ORG_DECISION` |
| Pembatasan dana APP Nasional | Sebagian terlihat halaman 24 | Verifikasi sumber lengkap dan tentukan enforcement resmi. |
| Keseluruhan CHR-020 | Tetap terbuka sebagian | Klarifikasi mengatasi interpretasi nominal dan batas per kejadian, bukan seluruh policy Finance. |

---

## 17. Pending Owner, Organization, and Finance Decisions

| ID | Keputusan/sumber yang dibutuhkan | Status | Dampak |
|---|---|---|---|
| FIN-DEC-01 | Konfirmasi formal interpretasi halaman 23: Rp50m adalah maksimum per kejadian/operasi menurut clarification, bukan nilai tetap | `SOURCE_CONFLICT` / perlu otoritas yang berwenang | Mencegah sistem tampak mengubah SOP secara diam-diam. |
| FIN-DEC-02 | Definisi “satu kejadian” versus “satu operasi tanggap darurat” untuk batas Rp50m | `PENDING_ORG_DECISION` | Menentukan control unit dan risiko cap reset. |
| FIN-DEC-03 | Apakah satu parent incident dapat memiliki beberapa independent operations dengan cap masing-masing | `PENDING_ORG_DECISION` | Tanpa keputusan, rekomendasi konservatif adalah agregasi parent incident. |
| FIN-DEC-04 | Event yang mengonsumsi limit: request, approval, reservation, payment instruction, atau actual cash release | `PENDING_ORG_DECISION` | Menentukan kapan cap dan cash control berubah. |
| FIN-DEC-05 | Definisi eligible available emergency cash | `PENDING_ORG_DECISION` | Menentukan global pool yang dapat dipakai. |
| FIN-DEC-06 | Perlakuan reservation/approved but unpaid/outstanding payment/advances | `PENDING_ORG_DECISION` | Mencegah overspend dan perhitungan kas salah. |
| FIN-DEC-07 | Perlakuan refund/reversal/cancelled disbursement terhadap cap dan kas | `PENDING_ORG_DECISION` | Menentukan kapan limit dapat kembali tersedia. |
| FIN-DEC-08 | Identitas dan delegasi Ketua TSKKM dalam approval dana darurat | `EVIDENCE_NOT_AVAILABLE` / `PENDING_ORG_DECISION` | Approval authority tidak dapat dimodelkan final. |
| FIN-DEC-09 | Approval matrix Finance yang lengkap | `EVIDENCE_NOT_AVAILABLE` | Tidak ada approval lain yang boleh ditebak. |
| FIN-DEC-10 | Funding-source cardinality dan allocation level | `PENDING_DESIGN_DECISION` | Mempengaruhi budget dan reporting per source. |
| FIN-DEC-11 | APP Nasional restriction enforcement mode | `PENDING_ORG_DECISION` | Hard block, warning, manual review, atau informasi belum diputuskan. |
| FIN-DEC-12 | Actual expenditure accounting recognition | `PENDING_ORG_DECISION` | Jangan menganggap payment otomatis sama dengan expense. |
| FIN-DEC-13 | Program–Activity–Budget relationship | `PENDING_DESIGN_DECISION` | FK dan aggregation/reporting belum final. |
| FIN-DEC-14 | Budget revision workflow state dan effective time | `PENDING_ORG_DECISION` / `PENDING_DESIGN_DECISION` | Belum boleh menjadi state resmi aplikasi. |
| FIN-DEC-15 | Remaining budget formula dan basis commitment/cut-off | `PENDING_ORG_DECISION` | Angka remaining belum boleh disebut definitif. |
| FIN-DEC-16 | Multi-currency, precision, rounding, exchange rate | `PENDING_ORG_DECISION` dan physical design dependency | Tidak dapat mengunci type/calculation. |
| FIN-DEC-17 | SOP Finance lengkap dan template halaman 49 | `EVIDENCE_NOT_AVAILABLE` | Audit Finance belum lengkap. |
| FIN-DEC-18 | Repository/branch/commit untuk pemeriksaan hardcoded values | `EVIDENCE_NOT_AVAILABLE` | Tidak dapat memastikan ada/tidaknya hardcoding. |

---

## 18. Evidence Required

Sebelum logical Finance design dapat diselesaikan:

1. SOP halaman 23 dalam scan resolusi tinggi untuk memastikan redaksi utuh tentang Rp50m.
2. Bukti/risalah persetujuan yang mengadopsi klarifikasi pemilik proyek sebagai interpretasi operasional formal, bila diperlukan oleh tata kelola organisasi.
3. SOP Finance halaman 40–41, procurement/finance halaman 62–69, dan template keuangan terkait.
4. Template halaman 49 dan versinya.
5. Mandat/delegasi formal Ketua TSKKM dan keputusan kewenangan terkait.
6. Kebijakan Finance tentang kas tersedia, komitmen, reservasi, outstanding payment, advance, refund, reversal, dan restricted cash.
7. Keputusan definisi kejadian/operasi sebagai control unit per incident cap.
8. Data model Program/Activity/Budget yang ditinjau.
9. Funding-source register dan restriction policy yang disahkan.
10. Repository dan branch/commit bila pemeriksaan hardcoding diperlukan.
11. Hasil test aktual bila status tes ingin dinaikkan dari `TEST_DESIGNED`.

---

## 19. Readiness Assessment

### Status: `BLOCKED`

Alasan:

- Ada perbedaan interpretasi yang perlu direkonsiliasi antara redaksi SOP halaman 23 yang terlihat dan klarifikasi bahwa Rp50m adalah maksimum per kejadian/operasi.
- Incident versus operation sebagai unit cap belum ditetapkan secara formal.
- Definisi eligible available cash belum tersedia.
- Event yang mengonsumsi cap dan cash control belum ditentukan.
- Authority formal Ketua TSKKM belum dipetakan ke struktur pengguna/assignment sistem.
- Funding-source restrictions baru diperiksa sebagian.
- Actual expenditure dan cash disbursement belum memiliki model kanonis yang dapat diverifikasi.
- Budget/activity relationships, revision lifecycle, dan remaining-budget basis masih pending.
- Repository, schema, dan test suite tidak tersedia untuk diperiksa.

### Kesiapan menurut tahap

| Tahap | Status |
|---|---|
| Interpretasi Rp100m sebagai contoh | **READY sebagai klarifikasi pemilik proyek** |
| Interpretasi Rp50m sebagai maksimum per kejadian/operasi | **Dinyatakan jelas oleh pemilik proyek; konfirmasi formal terhadap redaksi SOP halaman 23 masih diperlukan** |
| Prinsip beberapa kejadian dapat melampaui agregat Rp50m | **READY sebagai klarifikasi pemilik proyek, dengan batas kas dan approval yang berlaku** |
| Control design per kejadian dan kas global | **CONDITIONAL; detail event dan cash basis pending** |
| Finance logical design final | **BLOCKED** |
| Physical schema, migration, dan implementation | **BLOCKED dan tidak dilakukan** |
| Repository/code/test-suite audit | **BLOCKED_BY_MISSING_SOURCE** |

---

## 20. Recommended Next Prompt

Setelah pemilik proyek dan pihak berwenang meninjau dokumen ini, langkah berikut yang disarankan:

> **Lakukan konfirmasi kebijakan dan rekonsiliasi SOP untuk dana darurat TSKKM. Fokuskan pada: (1) penegasan formal Rp50.000.000 sebagai maksimum per incident/operation; (2) definisi incident versus response operation sebagai unit agregasi; (3) event yang mengonsumsi limit; (4) definisi eligible available emergency cash dan perlakuan reservation, outstanding payment, advance, refund, reversal, dan restricted cash; (5) hubungan authority Ketua TSKKM dengan mandat/delegasi yang berlaku; dan (6) cara mempertahankan sumber SOP tanpa mengubah redaksinya. Tetap read-only, jangan membuat schema atau mengimplementasikan aturan. Hasilkan decision record, updated traceability, dan daftar unresolved issues.**

Setelah keputusan tersebut tersedia, audit Finance–Procurement–Logistics dapat diperbarui dan diuji lagi pada tingkat spesifikasi. Jangan melanjutkan ke physical schema, code, migration, seed, atau deployment sebelum review pemilik proyek dan persetujuan yang diperlukan.

---

## 21. Pernyataan akhir

Kebijakan yang diarahkan pemilik proyek adalah **fleksibilitas untuk mendukung banyak kejadian berbeda dengan batas pengeluaran per kejadian/operasi dan kontrol ketersediaan kas secara keseluruhan**.

Untuk mencerminkan kebijakan itu dengan benar:

- Rp50m tidak boleh dijadikan cap global semua aktivitas TSKKM.
- Rp50m menjadi maksimum per control unit kejadian/operasi sesuai klarifikasi pemilik proyek.
- Kejadian berbeda dapat memiliki pengeluaran masing-masing dan totalnya boleh melampaui Rp50m.
- Total tetap dibatasi oleh kas darurat yang eligible dan tersedia.
- Satu kejadian tidak boleh melewati limit hanya karena pengeluaran dipisah ke banyak voucher, sektor, activity, atau user.
- Fleksibilitas nominal tidak mengubah approval authority.
- Definisi control unit dan cash availability harus disahkan sebelum sistem mengotomatisasi kontrol.
- Klarifikasi proyek tidak boleh digunakan untuk mengubah redaksi SOP secara diam-diam; perbedaan dengan halaman 23 harus direkonsiliasi secara formal.

**Status dokumen:** Draft hasil audit untuk review pemilik proyek.  
**Status implementasi:** Tidak dilakukan.  
**Status test:** Seluruh test belum dijalankan.  
**Status SOP keseluruhan:** Belum diaudit lengkap; yang tersedia dalam audit ini adalah gambar halaman 16–29.