# SIM-TDB — PROMPT REVISI RE-AUDIT FINANCE
**Document ID:** SIMTDB-REV05112026-00-05-FIN-PROMPT-R01  
**Filename:** `SIMTDB_REV05112026_00_05_FINANCE_REAUDIT_PROMPT_R01.md`  
**Revision:** REV05112026  
**Tanggal:** 05 November 2026  
**Project:** Sistem Informasi Manajemen Tanggap Darurat Bencana (SIM-TDB)  
**Organisasi:** Caritas Keuskupan Malang — Tim Solidaritas Kemanusiaan Keuskupan Malang (TSKKM)  
**Mode:** Audit dokumen, rekonsiliasi requirement, dan rancangan pengujian. TANPA IMPLEMENTASI.

---

# A. PERAN DAN MANDAT

Bertindak sebagai tim multidisiplin yang terdiri dari:
1. Principal Finance Systems Architect.
2. Enterprise Data Architect.
3. Senior Business Analyst.
4. Database Architect.
5. Procurement and Supply Chain Systems Analyst.
6. Security and Authorization Architect.
7. QA/Test Architect.
8. Internal Control and Audit Specialist.

Tugas Anda adalah melakukan re-audit spesifikasi Finance SIM-TDB berdasarkan sumber yang benar-benar tersedia. Jangan sekadar mengaudit kualitas prompt. Audit substansi persyaratan, konsistensi model data konseptual, integrasi lintas modul, dan rancangan test case.

**Larangan mutlak:** jangan menulis kode aplikasi, membuat tabel fisik, migration, seed, API, atau mengubah file proyek yang sudah ada. Jangan mengklaim aplikasi atau tes telah dijalankan jika tidak ada bukti eksekusi.

# B. FILE DAN SUMBER YANG WAJIB DIPERIKSA

Periksa file berikut jika tersedia di workspace:

1. `SIMTDB_REV05112026_00_02_FINANCIAL_AMOUNT_CLARIFICATION.md`
2. `SIMTDB_REV05112026_00_03_FINANCE_CLARIFICATION_REAUDIT_AND_TEST_PROMPT.md`
3. `SIMTDB_REV05112026_00_04_AUDIT_FINANCE_REAUDIT_PROMPT.md`
4. `SIMTDB_REV05112026_00_01_SOP_PARTIAL_AUDIT.md`
5. `SIMTDB_REV05112026_00_01_AUDIT_AND_CORE_FOUNDATION_ANALYSIS.md`
6. Master Prompt SIM-TDB V1.0.
7. Correction & Harmonization Register (CHR), terutama CHR-020.
8. SOP asli halaman 16–29.
9. SOP halaman 30–95, lampiran, dan template keuangan/procurement jika tersedia.
10. Repository aplikasi hanya jika benar-benar tersedia dan akses baca diizinkan.

Jika salah satu sumber tidak tersedia, tuliskan nama sumber dan status `EVIDENCE_NOT_AVAILABLE`. Jangan mengarang isi atau menganggap sumber tersebut sudah diperiksa.

## B.1 Hierarki sumber dan provenance

Gunakan urutan berikut untuk menilai bukti:

1. Pernyataan langsung pemilik proyek yang tercantum dalam instruksi prompt ini.
2. SOP asli yang dapat dibaca dan diverifikasi.
3. Keputusan organisasi formal yang memiliki penerbit, tanggal, cakupan, dan bukti persetujuan.
4. Addendum/requirement proyek yang secara eksplisit telah diterima pemilik proyek.
5. Hasil audit dan spesifikasi terdahulu.
6. Rekomendasi teknis auditor.

Jangan menyamakan rekomendasi teknis dengan ketentuan SOP atau keputusan organisasi.

Jika suatu persyaratan hanya muncul pada dokumen addendum, tetapi bukti penerimaan pemilik proyek atas persyaratan tersebut tidak jelas, catat sebagai `PROJECT_REQUIREMENT_STATED_IN_ADDENDUM` atau `PENDING_OWNER_ACCEPTANCE`, sesuai bukti. Jangan mengklaimnya sebagai kutipan langsung pemilik proyek.

# C. KLARIFIKASI PEMILIK PROYEK — ATURAN YANG TIDAK BOLEH DIUBAH

Pemilik proyek menyatakan bahwa:

- Nominal Rp50.000.000 dan Rp100.000.000 yang muncul sebagai contoh dalam SOP/template merupakan ilustrasi nilai keuangan.
- Kedua nominal bukan nilai baku, plafon tetap, batas maksimal pengeluaran, default wajib, atau threshold persetujuan otomatis.
- Besaran anggaran dapat disesuaikan dengan kebutuhan program atau kegiatan.

Klasifikasikan pernyataan langsung tersebut sebagai `CLARIFIED_BY_PROJECT_OWNER`.

Implikasi wajib:
1. Jangan hardcode Rp50.000.000 atau Rp100.000.000 sebagai cap, default wajib, atau approval threshold.
2. Jangan menyimpulkan nominal tersebut sebagai batas kewenangan Ketua TSKKM atau pejabat lain.
3. Jangan mengubah kewenangan organisasi karena nominal anggaran fleksibel.
4. Nominal yang muncul dalam sumber historis boleh tetap tercantum sebagai contoh, sepanjang tidak diubah menjadi rule sistem.
5. Threshold nominal lain tidak otomatis dilarang. Threshold lain hanya dapat diberlakukan jika bersumber dari kebijakan/authority matrix formal yang disahkan, dengan scope, versi, tanggal berlaku, dan otoritas yang jelas.

# D. KLASIFIKASI STATUS — WAJIB KONSISTEN

Gunakan label berikut:

- `CLARIFIED_BY_PROJECT_OWNER`: hanya untuk pernyataan langsung pemilik proyek yang dapat ditelusuri.
- `SOP_CONFIRMED`: didukung langsung oleh SOP asli yang telah diperiksa.
- `ORG_DECISION_CONFIRMED`: didukung keputusan organisasi formal yang dapat diidentifikasi.
- `PROJECT_REQUIREMENT_STATED_IN_ADDENDUM`: dinyatakan pada addendum proyek, tetapi penerimaan/otorisasi terpisah perlu ditelusuri.
- `PENDING_OWNER_ACCEPTANCE`: membutuhkan persetujuan eksplisit pemilik proyek.
- `TECHNICAL_RECOMMENDATION`: usulan desain teknis, bukan kebijakan.
- `PENDING_DESIGN_DECISION`: memerlukan keputusan desain domain/arsitektur.
- `PENDING_ORG_DECISION`: memerlukan keputusan organisasi atau pedoman Finance.
- `SOURCE_CONFLICT`: terdapat perbedaan sumber.
- `EVIDENCE_NOT_AVAILABLE`: bukti tidak tersedia.
- `TEST_DESIGNED`: skenario dirancang tetapi belum dijalankan.
- `TEST_EXECUTED_PASS`: tes benar-benar dijalankan dan bukti hasil tersedia.
- `TEST_EXECUTED_FAIL`: tes benar-benar dijalankan dan gagal.
- `BLOCKED_BY_MISSING_POLICY`: terhalang kebijakan yang belum disahkan.
- `BLOCKED_BY_MISSING_SOURCE`: terhalang sumber yang belum tersedia.

Jangan menggunakan `PASS` untuk tes aplikasi jika tidak ada evidence eksekusi.

# E. RUANG LINGKUP AUDIT SUBSTANTIF

## E1. Audit Business Rules dan nominal

Audit seluruh referensi nominal Rp50 juta dan Rp100 juta dalam dokumen dan, jika tersedia, repository.

Periksa:
- Apakah nominal hanya menjadi contoh pada dokumen sumber.
- Apakah nominal tertanam sebagai default, cap, threshold, atau approval gate.
- Apakah ada rule yang menganggap nominal tersebut sebagai batas dana siaga.
- Apakah nominal digunakan pada UI, validasi, backend, konfigurasi, seed, migration, test fixture, workflow, atau report calculation.
- Apakah terdapat format angka yang berbeda: `50000000`, `50.000.000`, `50,000,000`, `Rp 50.000.000`, dan variasi representasi lainnya.
- Lakukan pemeriksaan serupa untuk Rp100 juta.

Pengecualian: kemunculan nominal dalam file SOP, addendum, audit historis, atau dokumentasi yang jelas menyebutnya sebagai contoh tidak otomatis dianggap hardcoding rule. Bedakan kemunculan teks dari penggunaan angka sebagai logika aplikasi.

Jika repository tidak tersedia, jangan menyatakan pencarian kode telah dilakukan. Beri status `BLOCKED_BY_MISSING_SOURCE`.

## E2. Approval threshold formal

Buat pengujian terpisah untuk:
1. Rp50 juta/Rp100 juta tidak boleh menjadi threshold.
2. Threshold lain tanpa authority source formal tidak boleh dianggap kebijakan aktif.
3. Threshold lain yang memiliki dokumen formal, otoritas, scope, versi, dan effective date dapat dipertimbangkan untuk konfigurasi setelah persetujuan organisasi.
4. Perubahan authority matrix harus berversi dan dapat diaudit.
5. Edit permission tidak otomatis memberikan approval authority.

Jangan mengasumsikan bahwa semua threshold nominal dilarang selamanya. Yang dilarang adalah menginferensikan threshold dari nominal contoh atau mengaktifkan threshold tanpa sumber formal.

## E3. Budget lifecycle

Periksa pemisahan konseptual berikut:
- Proposed budget.
- Approved budget.
- Budget revision.
- Actual expenditure.
- Remaining budget.

Addendum proyek menyebut kebutuhan pemisahan tersebut. Pastikan status provenance masing-masing sesuai hierarki sumber di Bagian B.

Audit apakah model mampu:
- Menyimpan proposal tanpa mengubah approved budget.
- Menyimpan revisi tanpa menghapus versi sebelumnya.
- Menyimpan nilai sebelum dan sesudah revisi.
- Menyimpan alasan, aktor, waktu, dan referensi persetujuan.
- Membedakan revisi diajukan, diperiksa, disetujui, ditolak, dibatalkan, dan berlaku hanya sebagai kandidat state teknis sampai workflow disahkan.
- Mencegah revisi yang belum disetujui mengubah baseline anggaran aktif.
- Menangani dua revisi bersamaan tanpa silent overwrite.

Jangan menetapkan nama status workflow sebagai status resmi organisasi tanpa bukti.

## E4. Single Source of Truth untuk actual expenditure

Ini adalah kontrol kritis.

Tentukan sumber kanonis nominal actual expenditure berdasarkan model Finance yang benar-benar tersedia. Jika belum ada model aktual, nyatakan sebagai keputusan desain yang belum final.

Prinsip target:
- Satu nominal aktual harus memiliki satu sumber kanonis.
- Referensi laporan mengambil nominal dari sumber kanonis tersebut.
- Jangan menyediakan dua kolom nominal yang dapat diedit terpisah untuk transaksi yang sama.
- Snapshot hanya boleh digunakan jika alasan, sumber, versi, waktu snapshot, sifat immutable, dan aturan rekonsiliasinya jelas.

Buat test negatif:
- Jika report/reference mencoba menampilkan nominal berbeda dari transaksi sumber, sistem tidak boleh mengubah atau menyembunyikan perbedaan tersebut.
- Perbedaan harus dapat ditelusuri dan direkonsiliasi melalui proses koreksi yang sah.
- Jangan menghapus atau menimpa transaksi asal tanpa jejak.

Hindari istilah status seperti `posted`, `authorized`, atau `recognized` sebagai status resmi jika belum ditemukan dalam SOP/pedoman Finance. Gunakan frasa netral: “transaksi yang statusnya diakui untuk pelaporan sesuai kebijakan Finance yang disahkan”.

## E5. Funding Source dan cardinality

Jangan memilih cardinality secara sepihak.

Analisis setidaknya tiga alternatif:
1. Satu budget hanya boleh memiliki satu funding source.
2. Satu budget dapat mempunyai beberapa funding source.
3. Satu budget line atau expense dapat dialokasikan ke beberapa funding source.

Untuk setiap alternatif jelaskan:
- Kelebihan dan risiko.
- Dampak pada laporan per sumber dana.
- Dampak pada pembatasan penggunaan dana.
- Kebutuhan allocation record.
- Dampak pada rekonsiliasi.
- Dampak terhadap perubahan anggaran.

Buat pertanyaan keputusan yang spesifik untuk pemilik proses/organisasi. Tandai `PENDING_DESIGN_DECISION` atau `PENDING_ORG_DECISION`.

Jangan membuat alokasi multi-sumber seolah-olah sudah menjadi kebijakan.

## E6. Funding Source Restrictions

Audit sumber SOP halaman 23–24 yang tersedia. Pertahankan semua pembatasan penggunaan sumber dana yang didukung teks.

Untuk APP Nasional dan sumber dana lain:
- Kutip/parafrasekan hanya pembatasan yang benar-benar terbaca.
- Catat nomor halaman.
- Catat kategori pengeluaran yang diperbolehkan/dilarang hanya jika sumber menyebutkannya.
- Jangan membuat kategori larangan baru.
- Jangan membuat automatic blocking rule tanpa interpretasi resmi.
- Jika perilaku sistem belum disetujui, jelaskan alternatif: hard block, warning, atau manual review sebagai pilihan desain, bukan keputusan.

Jika template atau halaman terkait tidak tersedia, gunakan `EVIDENCE_NOT_AVAILABLE`.

## E7. Relasi Program, Activity, Budget, dan Budget Line

Audit field ambigu seperti `program_id / activity_id`.

Jangan menggunakan polymorphic reference tanpa strategi integritas yang jelas.

Tampilkan alternatif konseptual:
- Budget pada tingkat program.
- Budget pada tingkat activity.
- Program sebagai induk dan activity sebagai anak.
- Budget header dengan budget lines yang terkait ke activity/program.

Untuk tiap alternatif, jelaskan:
- Cardinality.
- Foreign-key integrity.
- Roll-up/reporting.
- Revisi anggaran.
- Risiko duplikasi.
- Ketergantungan pada Program Management.

Jangan menentukan physical schema atau foreign key final sebelum entity model Program/Activity disetujui.

## E8. Remaining Budget dan accounting policy

Jangan menetapkan formula final.

Periksa faktor berikut:
- Approved budget.
- Actual expenditure.
- Commitment/encumbrance.
- Purchase Order yang belum selesai.
- Invoice diterima tetapi belum dibayar.
- Payment.
- Advance.
- Refund.
- Reversal.
- Cancelled transaction.
- Period cut-off.
- Multi-currency dan exchange rate, bila berlaku.
- Rounding.

Buat contoh simulasi yang menunjukkan bagaimana angka remaining budget berbeda menurut basis perhitungan, tetapi jangan memilih formula.

Jika dashboard membutuhkan angka sementara, usulkan label “estimasi” dan tampilkan basis perhitungannya. Perilaku UI tersebut tetap `TECHNICAL_RECOMMENDATION` sampai disetujui.

## E9. Integrasi Finance–Procurement–Logistics

Buat dependency matrix yang membedakan:
- Purchase/request requisition.
- Bid analysis/quotation, jika didukung sumber.
- Purchase order.
- Penerimaan fisik/GRN.
- Invoice.
- Payment.
- Commitment.
- Expense recognition.
- Inventory posting.
- Refund/reversal.
- Financial reporting.

Untuk setiap entitas jelaskan:
- Pemilik data (system of record).
- Event pemicu.
- Data yang direferensikan modul lain.
- Apakah transaksi menciptakan catatan keuangan atau hanya referensi.
- Aturan idempotency.
- Bukti pendukung.
- Status sumber: SOP, keputusan organisasi, atau usulan teknis.

Jangan menetapkan urutan invoice/GRN/payment atau aturan akuntansi yang belum didukung SOP/pedoman Finance.

## E10. Monetary data type

Berikan rekomendasi konseptual saja:
- Hindari binary floating point untuk uang.
- Pertimbangkan decimal/numeric presisi atau integer minor units sesuai DBMS dan kebijakan.
- Currency code eksplisit jika multi-currency diizinkan.
- Precision, rounding, exchange rate, dan conversion date belum boleh dikunci tanpa kebijakan dan keputusan DBMS.

Jangan memilih tipe fisik atau DBMS pada audit ini.

# F. TEST PLAN WAJIB

Buat test case dengan ID berikut. Semua test yang belum dijalankan wajib `TEST_DESIGNED`.

| ID | Skenario wajib |
|---|---|
| FIN-TEST-01 | Nominal proposal Rp25 juta dapat dicatat tanpa terkena cap contoh |
| FIN-TEST-02 | Nominal proposal Rp75 juta dapat dicatat tanpa threshold contoh |
| FIN-TEST-03 | Nominal proposal Rp250 juta dapat dicatat tanpa threshold contoh |
| FIN-TEST-04 | Proposed budget berbeda dari approved budget |
| FIN-TEST-05 | Revision belum disetujui tidak mengubah approved baseline |
| FIN-TEST-06 | Revision menyimpan nilai sebelum/sesudah, alasan, aktor, waktu, dan approval reference sesuai requirement yang disetujui |
| FIN-TEST-07 | Uji cardinality satu/banyak funding source tetap pending sampai keputusan |
| FIN-TEST-08 | Uji restriction funding source yang benar-benar didukung SOP |
| FIN-TEST-09 | Actual expenditure report mengambil nominal dari satu sumber kanonis |
| FIN-TEST-10 | Dua nilai actual berbeda antara report/reference dan transaksi sumber terdeteksi |
| FIN-TEST-11 | Remaining budget tidak diklaim definitif sebelum formula disahkan |
| FIN-TEST-12 | User dengan edit permission tetapi tanpa approval authority tidak dapat menyetujui |
| FIN-TEST-13 | Retry dengan idempotency key sama tidak membuat revision/transaksi duplikat |
| FIN-TEST-14 | Dua revisi bersamaan tidak menyebabkan silent overwrite |
| FIN-TEST-15 | Refund/reversal mempertahankan hubungan ke transaksi asal |
| FIN-TEST-16 | Hardcoded Rp50 juta/Rp100 juta dicari pada logic/config/seed/validation/workflow/migration/test fixture jika repository tersedia |
| FIN-TEST-17 | Threshold selain nominal contoh tanpa authority source formal tidak dapat diaktifkan sebagai policy |
| FIN-TEST-18 | Threshold dengan authority formal, scope, versi, dan effective date hanya dapat dipertimbangkan setelah approval organisasi |
| FIN-TEST-19 | Multi-source allocation tidak dianggap valid/invalid berdasarkan asumsi sebelum cardinality diputuskan |
| FIN-TEST-20 | Funding restriction yang belum diverifikasi tidak berubah menjadi automatic block rule |
| FIN-TEST-21 | PO terbuka dan invoice belum dibayar tidak menghasilkan remaining budget definitif tanpa kebijakan |
| FIN-TEST-22 | Relasi Program/Activity tidak menghasilkan orphan reference atau polymorphic ambiguity |
| FIN-TEST-23 | Report per funding source dapat direkonsiliasi ke allocation/transaction sumber jika model tersebut disetujui |

Untuk setiap test case, tulis:
- Tujuan.
- Preconditions.
- Test data.
- Langkah.
- Expected result.
- Actual result (isi “belum dijalankan” jika belum ada eksekusi).
- Status.
- Evidence yang diperlukan.
- Dependency/policy yang menghalangi.

Gunakan status:
`TEST_DESIGNED`, `TEST_EXECUTED_PASS`, `TEST_EXECUTED_FAIL`, `BLOCKED_BY_MISSING_POLICY`, `BLOCKED_BY_MISSING_SOURCE`.

`TEST_EXECUTED_PASS` atau `TEST_EXECUTED_FAIL` wajib memiliki evidence lingkungan, input, output, dan build/commit bila ada.

# G. OUTPUT YANG WAJIB DIBUAT

Simpan satu dokumen hasil audit baru dengan nama:

`SIMTDB_REV05112026_00_06_FINANCE_CLARIFICATION_REAUDIT.md`

Jangan menimpa dokumen 00_02, 00_03, 00_04, atau prompt 00_05 ini.

Struktur output:

1. Executive Summary.
2. Source Inventory dan Evidence Availability.
3. Source Hierarchy dan Provenance.
4. Owner Clarification Register.
5. SOP Finance Evidence Ledger (nomor halaman dan kutipan/inti bukti).
6. Corrected Financial Business Rule Register.
7. Financial Source of Truth Matrix.
8. Single Source of Truth — Actual Expenditure Analysis.
9. Funding Source and Restriction Model Alternatives.
10. Budget Lifecycle and Revision Model.
11. Program–Activity–Budget Relationship Alternatives.
12. Remaining Budget Policy Dependency.
13. Finance–Procurement–Logistics Dependency Matrix.
14. Finance Entity Registry (konseptual, bukan physical schema).
15. Finance Data Dictionary Corrections (logical level only).
16. Approval Authority and Permission Dependency.
17. Test Plan FIN-TEST-01 sampai FIN-TEST-23.
18. Updated CHR-020 Mapping.
19. Pending Finance Decision Register.
20. Risk Register: prevention, detection, recovery.
21. Evidence Missing / Required.
22. Readiness Assessment.
23. Recommended Next Prompt.

# H. READINESS GATE

Berikan salah satu status:

- `READY_FOR_LOGICAL_DESIGN`
- `CONDITIONAL`
- `BLOCKED`

Finance tidak boleh dinyatakan siap untuk logical design jika masih ada konflik kritis pada:
- Actual expenditure source of truth.
- Authority approval.
- Funding-source restriction.
- Program/Activity/Budget relationship.
- Budget revision lifecycle.
- Remaining budget basis.

Finance tidak boleh dinyatakan siap untuk physical schema atau implementation dalam prompt ini karena implementasi memang dilarang pada tahap ini.

# I. STOP RULES

Jangan:
1. Menulis kode.
2. Membuat database table atau migration.
3. Mengubah file proyek yang ada.
4. Mengarang kebijakan akuntansi.
5. Mengarang pejabat/otoritas persetujuan.
6. Menentukan cardinality funding source tanpa keputusan.
7. Menentukan formula remaining budget tanpa pedoman.
8. Menganggap nominal contoh sebagai threshold.
9. Menganggap seluruh CHR-020 selesai.
10. Mengklaim repository/code telah diaudit jika tidak tersedia.
11. Mengklaim tes berhasil jika tidak ada evidence.
12. Mengubah SOP atau keputusan organisasi.

Di akhir, berikan rekomendasi langkah berikutnya secara spesifik. Jangan melanjutkan ke implementasi tanpa persetujuan pemilik proyek.

**Prinsip akhir:** nilai anggaran harus fleksibel mengikuti kebutuhan dan persetujuan yang sah; namun setiap nominal harus memiliki sumber data, sumber pendanaan, otoritas, bukti, relasi, dan jejak audit yang dapat ditelusuri.
