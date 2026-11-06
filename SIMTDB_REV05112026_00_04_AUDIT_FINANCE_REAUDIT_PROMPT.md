# SIM-TDB — AUDIT PROMPT RE-AUDIT FINANCE

**Document ID:** SIMTDB-REV05112026-00-04-AUDIT-FIN  
**File yang diaudit:** `SIMTDB_REV05112026_00_03_FINANCE_CLARIFICATION_REAUDIT_AND_TEST_PROMPT.md`  
**Status:** Audit dokumen / desk review  
**Mode:** Audit dan rancangan pengujian saja — tanpa implementasi  
**Project:** Sistem Informasi Manajemen Tanggap Darurat Bencana (SIM-TDB)  
**Organization:** Caritas Keuskupan Malang — Tim Solidaritas Kemanusiaan Keuskupan Malang (TSKKM)

---

## 1. Kesimpulan eksekutif

Prompt yang diaudit memiliki arah yang benar untuk meninjau klarifikasi pemilik proyek tentang nominal Rp50.000.000 dan Rp100.000.000. Prompt tersebut secara tepat meminta agar:

- Kedua nominal diperlakukan sebagai contoh, bukan nilai baku atau batas otomatis.
- Isu CHR-020 tidak dianggap seluruhnya selesai.
- Sumber nominal aktual dapat ditelusuri ke transaksi keuangan.
- Otoritas persetujuan tidak disimpulkan dari fleksibilitas nominal.
- Tes yang belum dijalankan tidak diklaim lulus.
- Tidak dilakukan implementasi.

**Penilaian:** `CONDITIONAL PASS` sebagai prompt audit setelah koreksi.

### Koreksi utama yang diperlukan

1. **Potensi benturan nama file.** File yang diaudit bernomor `00_03`, sedangkan output yang diperintahkan pada Part C juga bernomor `00_03` dengan nama berbeda. Ini dapat menimbulkan kebingungan versi atau overwrite.
2. **Klasifikasi status perlu lebih presisi.** Klarifikasi pemilik proyek secara eksplisit mencakup fleksibilitas nominal, pemisahan kategori anggaran, histori perubahan, traceability sumber dana, serta asal angka laporan dari transaksi aktual tercatat dan disahkan. Detail implementasi seperti workflow status, formula remaining budget, type database, serta kontrol concurrency tetap merupakan usulan teknis atau keputusan yang belum ditetapkan.
3. **Perlu tes eksplisit untuk hardcoded threshold dan approval threshold.** Prompt membahas risiko ini, tetapi daftar test case perlu memisahkan: (a) pencarian nilai contoh yang ditanam sebagai rule; dan (b) dukungan bagi threshold lain hanya jika ada kebijakan formal yang disahkan.
4. **Perlu mengunci satu sumber nilai aktual.** Rancangan harus mencegah nilai aktual yang sama dapat diedit pada transaksi dan salinan “actual expenditure reference”.
5. **Beberapa expected results berpotensi mengasumsikan kebijakan teknis.** Contoh: automatic flag untuk aturan sumber dana yang belum disetujui dan penggunaan status `posted/authorized`. Keduanya perlu diberi label proposal atau menunggu kosakata status Finance resmi.
6. **Kardinalitas sumber pendanaan dan relasi budget–program–activity belum jelas.** Prompt sudah meminta audit hal ini, tetapi hasilnya harus mempertahankan status sebagai keputusan desain/bisnis terbuka, bukan memilih kardinalitas sepihak.

Tidak ada bukti bahwa tes aplikasi dijalankan. Seluruh tes pada dokumen yang diaudit harus diperlakukan sebagai rancangan tes, kecuali ada hasil eksekusi dan evidence yang disediakan kemudian.

---

## 2. Ruang lingkup dan keterbatasan

Audit ini memeriksa isi prompt yang diberikan dalam percakapan, termasuk:

- Kesimpulan audit independen.
- Temuan koreksi teknis FIN-CR-01 sampai FIN-CR-12.
- Klasifikasi status persyaratan.
- Rancangan tes FIN-TEST-01 sampai FIN-TEST-12.
- Prompt lanjutan untuk Copilot.
- Review gate Finance.

Audit ini **tidak**:

- Membuka repository atau file lain di workspace.
- Memeriksa SOP halaman 1–95 secara penuh.
- Memeriksa template finance atau halaman 49, kecuali informasi yang tersedia dari gambar/material percakapan.
- Menjalankan aplikasi, query, migration, atau tes otomatis.
- Menyimpan perubahan ke file proyek.

Label temuan:

- `PASS` — cukup tepat berdasarkan materi yang tersedia.
- `CONDITIONAL` — benar arahnya, tetapi perlu batasan atau bukti.
- `GAP` — perlu ditambahkan atau diperjelas.
- `BLOCKED` — tidak dapat diverifikasi tanpa sumber yang belum tersedia.

---

## 3. Temuan audit

| ID | Tingkat | Status | Temuan | Dampak | Rekomendasi |
|---|---|---|---|---|---|
| FIN-PROMPT-01 | Tinggi | `GAP` | Prompt yang diaudit bernomor `00_03`, tetapi Part C menyuruh membuat output `SIMTDB_REV05112026_00_03_FINANCE_CLARIFICATION_REAUDIT.md`. | Dua artefak berbeda dapat memiliki nomor revisi yang sama; risiko salah membandingkan atau menimpa file. | Beri nomor baru, misalnya `00_04`, atau nama revision candidate yang jelas. Jangan menimpa file prompt sumber. |
| FIN-PROMPT-02 | Tinggi | `CONDITIONAL` | Part A benar mengkritik pemberian label `CLARIFIED_BY_PROJECT_OWNER` secara terlalu luas, tetapi perlu mengakui seluruh butir addendum yang memang dinyatakan oleh pemilik proyek. | Persyaratan pemilik proyek bisa secara tidak sengaja diturunkan menjadi usulan teknis. | Beri label pemilik proyek hanya pada pernyataan yang eksplisit di addendum: contoh nominal, fleksibilitas anggaran, pemisahan kategori, histori perubahan, traceability, otoritas tidak berubah, dan angka aktual dari catatan keuangan yang tercatat/disahkan. |
| FIN-PROMPT-03 | Tinggi | `GAP` | Daftar tes tidak memiliki pemeriksaan yang jelas atas hardcoding di aturan aplikasi, konfigurasi, seed, validasi, dan migrasi. | Nominal contoh masih dapat tertanam sebagai batas meskipun dokumen menyatakan sebaliknya. | Tambahkan tes pencarian rule aplikasi/konfigurasi untuk Rp50m dan Rp100m, dengan pengecualian sumber historis/dokumen yang hanya menyebutnya sebagai contoh. |
| FIN-PROMPT-04 | Tinggi | `GAP` | Belum ada acceptance test tersendiri bahwa threshold nominal hanya dapat digunakan bila berasal dari kebijakan/authority matrix formal yang disahkan. | “Jangan gunakan angka contoh sebagai threshold” dapat keliru ditafsirkan sebagai “sistem tidak boleh mendukung threshold apa pun”, atau sebaliknya. | Tambahkan tes negatif untuk threshold yang diinferensikan dari contoh dan tes kondisional untuk threshold lain yang memiliki sumber, versi, scope, dan effective date yang disetujui. |
| FIN-PROMPT-05 | Tinggi | `CONDITIONAL` | Prompt dengan tepat mengidentifikasi potensi duplikasi `actual_amount`, tetapi test set belum menguji secara langsung bahwa hanya satu sumber nilai aktual yang dapat diedit. | Laporan dapat menampilkan angka berbeda dari transaksi kanonis. | Tambahkan tes bahwa nilai aktual pada report/reference diturunkan dari transaksi sumber; jika snapshot diperlukan, harus immutable dan menjelaskan sumber versi serta rekonsiliasinya. |
| FIN-PROMPT-06 | Sedang | `CONDITIONAL` | Model funding source dan alokasi multi-sumber belum ditentukan; prompt telah mengangkat isu ini dengan baik. | Desain bisa memaksakan satu sumber atau mengizinkan pembagian tanpa persetujuan. | Pertahankan sebagai pending. Hasil audit harus menjelaskan pilihan model dan konsekuensi masing-masing tanpa memilih policy. |
| FIN-PROMPT-07 | Sedang | `CONDITIONAL` | `program_id / activity_id` ditandai sebagai relasi ambigu dengan benar. | Polymorphic reference dapat melemahkan integritas FK atau membuat hubungan anggaran tidak jelas. | Minta model eksplisit dan kardinalitas setelah model Program/Activity disetujui; jangan menetapkan bentuk fisik pada audit ini. |
| FIN-PROMPT-08 | Sedang | `CONDITIONAL` | Lifecycle revisi anggaran perlu dibedakan dari status bisnis resmi. | Daftar status teknis dapat dianggap sebagai workflow Finance yang disahkan. | Jelaskan status seperti requested/approved/rejected/effective/superseded hanya sebagai state kandidat sampai proses disetujui. |
| FIN-PROMPT-09 | Sedang | `CONDITIONAL` | Rumus remaining budget belum ditetapkan dengan benar; faktor komitmen, PO, invoice, pembayaran, refund, dan cut-off masih terbuka. | Angka sisa anggaran dapat salah dipresentasikan sebagai saldo definitif. | Pertahankan sebagai blocked/pending policy. Jika tampil sebagai estimasi, tampilkan basis dan statusnya secara eksplisit. |
| FIN-PROMPT-10 | Sedang | `CONDITIONAL` | Prompt menyarankan `posted/authorized` sebagai istilah expected result pada salah satu tes. | Kosakata status tersebut belum dibuktikan sebagai status resmi Finance. | Gunakan istilah netral “transaksi yang statusnya diakui untuk pelaporan sesuai kebijakan yang disahkan” sampai status resmi tersedia. |
| FIN-PROMPT-11 | Sedang | `CONDITIONAL` | Tes sumber dana dengan kebijakan yang belum lengkap menyebut “flag for manual review” sebagai hasil yang diharapkan. | Ini adalah perilaku teknis yang belum tentu disetujui; bisa dianggap aturan SOP. | Tandai sebagai `TECHNICAL_RECOMMENDATION` dan minta keputusan apakah sistem memblokir, memberi peringatan, atau hanya menampilkan informasi. |
| FIN-PROMPT-12 | Sedang | `CONDITIONAL` | Penggunaan numeric precision, rounding, multi-currency, dan exchange-rate dibahas sebagai best practice. | Keputusan fisik dapat terkunci sebelum DBMS dan kebijakan Finance ditetapkan. | Pertahankan hanya sebagai rekomendasi teknis; jangan menentukan precision, rounding, atau konversi final sekarang. |
| FIN-PROMPT-13 | Sedang | `GAP` | Batas antara procurement request, PO, invoice, payment, commitment, dan expense recognition perlu ditautkan pada spesifikasi lintas modul dan SOP lengkap. | Angka actual/remaining dapat dihitung dari transaksi yang salah atau ganda. | Pastikan output meminta dependency matrix tanpa menetapkan invoice-versus-GRN order yang masih pending. |
| FIN-PROMPT-14 | Sedang | `PASS` | Prompt secara benar menyatakan bahwa page 49 atau template yang tidak tersedia harus dicatat `EVIDENCE_NOT_AVAILABLE`. | Mengurangi risiko mengarang struktur form. | Pertahankan. |
| FIN-PROMPT-15 | Sedang | `PASS` | Prompt secara benar mensyaratkan label tes `TEST_DESIGNED`, `TEST_EXECUTED_PASS`, `TEST_EXECUTED_FAIL`, `BLOCKED_BY_MISSING_POLICY`, dan `BLOCKED_BY_MISSING_SOURCE`. | Menghindari klaim tes yang tidak pernah dijalankan. | Pertahankan dan wajibkan evidence untuk semua status `TEST_EXECUTED_*`. |
| FIN-PROMPT-16 | Tinggi | `PASS` | Prompt melarang implementasi, migrations, kebijakan akuntansi rekaan, kewenangan rekaan, dan menandai CHR-020 tidak selesai seluruhnya. | Membatasi risiko perubahan tanpa persetujuan. | Pertahankan. |

---

## 4. Penilaian terhadap klarifikasi pemilik proyek

Klarifikasi pemilik proyek menyatakan nominal Rp50.000.000 dan Rp100.000.000 adalah contoh dan tidak boleh menjadi nilai baku, plafon, batas maksimal pengeluaran, default wajib, atau threshold approval otomatis.

Klarifikasi juga secara eksplisit meminta:

- Anggaran fleksibel berdasarkan kebutuhan program/kegiatan, kondisi bencana, sumber pendanaan, dan anggaran yang disetujui.
- Pemisahan proposed budget, approved budget, budget revision, actual expenditure, dan remaining budget.
- Riwayat perubahan dengan alasan, aktor, waktu, dan referensi persetujuan.
- Traceability sumber pendanaan.
- Otorisasi tetap mengikuti kewenangan organisasi yang telah diverifikasi.
- Angka transaksi/laporan berasal dari data aktual yang tercatat dan disahkan.

### Klasifikasi yang disarankan

| Pernyataan | Status yang disarankan |
|---|---|
| Nominal Rp50m/Rp100m hanya contoh, bukan cap/default/threshold | `CLARIFIED_BY_PROJECT_OWNER` |
| Anggaran bervariasi sesuai kebutuhan dan anggaran yang disetujui | `CLARIFIED_BY_PROJECT_OWNER` |
| Lima kategori anggaran harus dibedakan | `CLARIFIED_BY_PROJECT_OWNER` |
| Perubahan memerlukan histori, alasan, aktor, waktu, dan referensi persetujuan | `CLARIFIED_BY_PROJECT_OWNER` |
| Sumber pendanaan harus dapat ditelusuri | `CLARIFIED_BY_PROJECT_OWNER` |
| Kewenangan persetujuan tetap mengikuti organisasi yang diverifikasi | `CLARIFIED_BY_PROJECT_OWNER` |
| Angka transaksi/laporan berasal dari catatan aktual yang tercatat dan disahkan | `CLARIFIED_BY_PROJECT_OWNER` |
| Nama entitas/tabel, tipe data, constraints, state-machine status, event/outbox, cache invalidation | `TECHNICAL_RECOMMENDATION` |
| Cardinality satu atau banyak sumber pendanaan | `PENDING_DESIGN_DECISION` |
| Formula remaining budget dan perlakuan komitmen | `PENDING_ORG_DECISION` |
| Pengakuan akuntansi, cut-off, reversal, refund, kurs, pembulatan | `PENDING_ORG_DECISION` atau menunggu pedoman Finance yang disahkan |
| Threshold approval lain di masa depan | Hanya dapat digunakan jika ada kebijakan/authority formal yang disahkan |

---

## 5. Koreksi yang disarankan terhadap isi prompt

### 5.1 Koreksi nama output

Hindari output memakai sequence yang sama dengan file prompt sumber.

Pilihan yang lebih jelas:

- Prompt yang diberikan tetap: `SIMTDB_REV05112026_00_03_FINANCE_CLARIFICATION_REAUDIT_AND_TEST_PROMPT.md`
- Hasil audit/revisi prompt: `SIMTDB_REV05112026_00_04_FINANCE_CLARIFICATION_REAUDIT.md`

Jika output berupa revisi prompt dan bukan hasil re-audit, gunakan nama berbeda yang menjelaskan fungsi, misalnya:

- `SIMTDB_REV05112026_00_04_FINANCE_REAUDIT_PROMPT_R01.md`

### 5.2 Penegasan sumber nilai actual

Tambahkan aturan:

> Nilai actual expenditure memiliki satu sumber kanonis pada catatan transaksi keuangan yang diakui untuk pelaporan sesuai kebijakan Finance yang disahkan. Entitas laporan/referensi tidak boleh menyimpan salinan nominal yang dapat diedit terpisah. Snapshot hanya boleh dipakai jika tujuannya dijelaskan, immutable, menyimpan sumber dan versinya, serta memiliki aturan rekonsiliasi.

### 5.3 Penegasan threshold

Tambahkan aturan:

> Rp50.000.000 dan Rp100.000.000 tidak boleh dipakai untuk hardcoded threshold, default, atau approval gate. Threshold lain tidak otomatis dilarang, tetapi hanya boleh berlaku jika ada authority matrix/kebijakan formal yang disetujui, berscope jelas, memiliki masa berlaku dan versi, serta dapat diaudit.

### 5.4 Penegasan funding allocation

Tambahkan pertanyaan desain:

> Apakah satu budget line/expense dapat didanai oleh satu sumber atau beberapa sumber? Jika beberapa sumber diperbolehkan, apakah diperlukan catatan alokasi per sumber dan bagaimana nilainya direkonsiliasi? Jangan menetapkan kardinalitas sebelum ada keputusan.

### 5.5 Penegasan status tes

Tambahkan aturan:

> Semua skenario yang belum dijalankan diberi `TEST_DESIGNED`. Status `TEST_EXECUTED_PASS` atau `TEST_EXECUTED_FAIL` memerlukan evidence eksekusi, lingkungan, test input, hasil aktual, dan referensi build/commit bila ada.

---

## 6. Desk test atas prompt dan desain tes

Ini adalah uji struktur dan kelengkapan dokumen. Tes aplikasi tidak dijalankan.

| Test ID | Pemeriksaan dokumen | Hasil yang diharapkan | Status audit |
|---|---|---|---|
| DOC-TEST-01 | Apakah prompt mempertahankan arti nominal contoh? | Tidak ada yang mengubah nominal contoh menjadi cap/default/threshold. | `TEST_DESIGNED`; isi prompt memenuhi prinsip ini. |
| DOC-TEST-02 | Apakah status owner clarification dibatasi pada yang dinyatakan? | Pemisahan antara klarifikasi pemilik proyek dan rekomendasi teknis. | `CONDITIONAL`; perlu koreksi klasifikasi seperti FIN-CR-01. |
| DOC-TEST-03 | Apakah output filename unik? | Prompt sumber dan hasil tidak menggunakan nomor/nama yang dapat membingungkan atau menimpa. | `FAIL`; konflik sequence `00_03` perlu diperbaiki. |
| DOC-TEST-04 | Apakah actual amount mempunyai satu source of truth? | Nilai report/reference diturunkan dari transaksi kanonis atau snapshot immutable yang dijelaskan. | `CONDITIONAL`; isu teridentifikasi tetapi belum menjadi test case eksplisit yang cukup. |
| DOC-TEST-05 | Apakah funding cardinality tidak diasumsikan? | Kardinalitas dinyatakan sebagai pertanyaan terbuka sampai disetujui. | `PASS` sebagai pertanyaan audit; output harus menjaga status pending. |
| DOC-TEST-06 | Apakah Program/Activity reference memiliki integritas? | Relasi tidak dibiarkan ambigu atau polimorfik tanpa strategi integritas. | `PASS` sebagai temuan; model akhir masih pending. |
| DOC-TEST-07 | Apakah remaining budget tidak dipresentasikan sebagai final tanpa kebijakan? | Formula dan komitmen tetap pending, atau tampilan jelas berstatus estimasi. | `PASS` sebagai prinsip; perlu test case UI/report. |
| DOC-TEST-08 | Apakah transaction/payment/expense dipisahkan? | Reconciliation matrix membedakan request, PO, invoice, payment, expense, refund, reversal, dan commitment. | `CONDITIONAL`; tercakup sebagai audit requirement, tetapi perlu kontrak lintas modul. |
| DOC-TEST-09 | Apakah tes benar-benar dijalankan? | Tidak ada klaim PASS tanpa evidence eksekusi. | `PASS` pada instruksi; belum ada tes aplikasi yang dieksekusi. |
| DOC-TEST-10 | Apakah template yang tidak tersedia ditangani dengan aman? | Ditandai `EVIDENCE_NOT_AVAILABLE`, bukan direka. | `PASS`. |
| DOC-TEST-11 | Apakah CHR-020 tetap terbuka sebagian? | Hanya interpretasi nominal yang ditutup; isu lain tetap dicatat. | `PASS`. |
| DOC-TEST-12 | Apakah akses persetujuan terpisah dari edit permission? | User yang bisa mengubah data tidak otomatis bisa menyetujui. | `PASS` sebagai requirement; implementasi belum diuji. |

---

## 7. Test cases yang perlu ditambahkan

Semua test berikut berstatus `TEST_DESIGNED`, bukan hasil eksekusi.

| Test ID | Skenario | Expected result |
|---|---|---|
| FIN-TEST-13 | Telusuri logic, configuration, seed data, validation, dan migration candidate untuk Rp50m/Rp100m. | Tidak ada rule yang memakai kedua nilai sebagai mandatory default, cap, atau threshold. Sumber historis yang hanya menampilkan contoh tidak dihitung sebagai hardcoded rule. |
| FIN-TEST-14 | Sistem menemukan threshold persetujuan selain Rp50m/Rp100m tanpa authority source. | Threshold tidak diberlakukan sebagai policy; ditolak atau ditandai sesuai proses governance yang disahkan. |
| FIN-TEST-15 | Threshold lain memiliki authority source formal, scope, versi, dan masa berlaku. | Hanya dapat dipakai bila organisasi menyetujui kebijakan dan implementasinya; tidak diinferensikan dari nilai contoh. |
| FIN-TEST-16 | Report mencoba menulis `actual_amount` berbeda dari transaksi sumber. | Perbedaan tidak dapat diedit diam-diam; report mengambil nominal kanonis atau menampilkan discrepancy yang dapat ditelusuri. |
| FIN-TEST-17 | Revisi anggaran dibuat dengan metadata sebagian hilang. | Revisi tidak dapat dianggap lengkap/approved jika field wajib yang telah disahkan belum terpenuhi; field tersebut tidak boleh ditebak. |
| FIN-TEST-18 | Budget allocation memakai lebih dari satu funding source sebelum cardinality disetujui. | Sistem/specification tidak menganggap alokasi valid atau invalid berdasarkan tebakan; kasus tetap pending untuk keputusan desain/organisasi. |
| FIN-TEST-19 | Expense terkena restriction funding source yang telah diverifikasi. | Sistem mengikuti aturan yang disahkan dan menautkan sumber kebijakannya. |
| FIN-TEST-20 | Expense terkena dugaan restriction yang sumbernya belum diverifikasi. | Tidak ada kebijakan baru yang otomatis dibuat; perlakuan sistem ditandai pending atau menggunakan mekanisme manual yang telah disetujui. |
| FIN-TEST-21 | Transaksi refund/reversal dicatat. | Transaksi asal tetap terlacak; pengakuan nilai dan dampaknya pada laporan mengikuti kebijakan yang disahkan. |
| FIN-TEST-22 | Perhitungan remaining budget melibatkan purchase order terbuka dan invoice belum dibayar. | Tidak ditampilkan sebagai saldo definitif sampai dasar perlakuan komitmen disahkan; basis yang digunakan dinyatakan. |

---

## 8. Risiko yang paling penting

### Risiko tinggi

1. **Threshold keuangan terselubung.** Nominal contoh dapat tertanam di validasi, kode, konfigurasi, seed, atau aturan approval.
2. **Nilai actual ganda.** Salinan nominal di tabel laporan/referensi bisa berbeda dari transaksi kanonis.
3. **Approval authority tertukar dengan permission.** Hak edit atau fungsi Finance tidak otomatis memberi kewenangan menyetujui.
4. **Remaining budget menyesatkan.** Penghitungan tanpa aturan commitment/cut-off dapat memberi kesan saldo akuntansi yang tidak sah.
5. **Sumber dana tidak terurai.** Pemaksaan satu sumber atau alokasi banyak sumber tanpa aturan dapat membuat laporan donor dan pembatasan dana keliru.
6. **Hubungan budget dengan activity tidak memiliki FK jelas.** Polymorphic reference dapat menghasilkan orphan atau laporan yang tidak konsisten.

### Kontrol yang direkomendasikan

| Risiko | Pencegahan | Deteksi | Pemulihan / penanganan |
|---|---|---|---|
| Threshold terselubung | Requirement dan code review; tidak menambah nominal contoh sebagai rule. | Search pada logic/config/seed/test/migration candidate. | Hapus rule tidak sah melalui perubahan terkendali; catat audit dan uji regresi. |
| Nilai actual ganda | Satu sumber kanonis; report amount diturunkan. | Rekonsiliasi report dengan transaksi sumber. | Tandai discrepancy dan perbaiki melalui proses koreksi tercatat; jangan overwrite transaksi. |
| Persetujuan tanpa authority | Authority registry terpisah dari permission; deny-by-default. | Uji negative access dan audit approval event. | Cabut akses yang salah; pertahankan bukti transaksi/approval dan lakukan review. |
| Remaining budget salah | Tunda formula final; tampilkan basis dan status. | Bandingkan komponen anggaran/transaksi dengan hasil report. | Tarik atau labeli ulang angka yang menyesatkan; revisi melalui versioning. |
| Funding allocation tidak jelas | Tetapkan cardinality dan allocation model sebelum finalisasi. | Uji laporan per funding source dan rekonsiliasi jumlah alokasi. | Eskalasi sebagai pending; jangan otomatis memindahkan nilai antar sumber. |
| Relasi Program/Activity ambigu | FK eksplisit setelah model domain disahkan. | Integrity/relationship tests. | Perbaiki model melalui revisi terkontrol tanpa kehilangan referensi historis. |

---

## 9. Penilaian prompt per bagian

| Bagian prompt | Penilaian |
|---|---|
| Part A — Independent Audit | Baik; temuan duplicate actual, funding cardinality, polymorphic reference, remaining budget dan status tes relevan. |
| Part A — classification correction | Perlu pemurnian agar persyaratan yang eksplisit di addendum tetap dianggap klarifikasi pemilik proyek. |
| Part B — Desk Tests | Baik sebagai rancangan, tetapi belum menguji hardcoding dan duplicate actual dengan cukup eksplisit. |
| Part C — Next Copilot Prompt | Kontrol no-implementation baik; output filename sequence perlu diperbaiki. |
| Part C — source constraints | Baik; page 49 dan template yang tidak tersedia harus `EVIDENCE_NOT_AVAILABLE`. |
| Part D — Review Gate | Baik; gate mencegah Finance maju ke schema/implementasi sebelum policy lengkap. |
| Keseluruhan | `CONDITIONAL PASS`; gunakan setelah perbaikan filename, classification, source-of-truth test, dan threshold tests. |

---

## 10. Checklist koreksi sebelum prompt digunakan

- [ ] Ganti output filename agar tidak menggunakan nomor `00_03` yang sama dengan file prompt sumber.
- [ ] Pertahankan `CLARIFIED_BY_PROJECT_OWNER` pada pernyataan eksplisit di addendum.
- [ ] Bedakan klarifikasi pemilik proyek dari rekomendasi teknis dan policy akuntansi.
- [ ] Tambahkan tes pencarian hardcoded amount rules pada logic/configuration/seed.
- [ ] Tambahkan tes untuk membedakan nilai contoh dari threshold formal yang sah.
- [ ] Tambahkan tes source-of-truth actual amount dan duplicate editable amount.
- [ ] Pertahankan funding cardinality dan Program/Activity relationship sebagai pending sampai disetujui.
- [ ] Jangan menetapkan status final untuk revision/remaining budget sebelum proses disahkan.
- [ ] Pertahankan pemisahan invoice, payment, expense recognition, commitment, refund, dan reversal.
- [ ] Pastikan tes yang belum dijalankan berstatus `TEST_DESIGNED`.
- [ ] Jangan menandai seluruh CHR-020 sebagai selesai.
- [ ] Jangan membuat schema, migration, atau aplikasi.

---

## 11. Status akhir

| Penilaian | Status |
|---|---|
| Interpretasi nominal Rp50m/Rp100m | **PASS** |
| Pengendalian no-implementation | **PASS** |
| Perlindungan dari klaim tes palsu | **PASS** |
| Ketepatan klasifikasi status | **CONDITIONAL** |
| Konsistensi penamaan output | **FAIL — perlu diperbaiki** |
| Uji hardcoding dan approval threshold | **GAP — perlu ditambahkan** |
| Uji single source of truth actual amount | **GAP — perlu diperjelas** |
| Kesiapan menjadi prompt audit lanjutan | **CONDITIONAL PASS** |
| Kesiapan desain fisik/implementasi Finance | **NOT READY** |

**Kesimpulan:** prompt yang diaudit merupakan dasar audit Finance yang baik, tetapi perlu koreksi sebelum dijalankan. Perubahan paling penting adalah memberi nama output unik, menjaga batas status `CLARIFIED_BY_PROJECT_OWNER`, serta menambahkan pengujian eksplisit untuk hardcoded thresholds dan duplikasi nominal aktual. Tidak ada tes aplikasi yang dijalankan dalam audit ini.