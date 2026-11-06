# SIM-TDB — ADDENDUM PELAKSANAAN AUDIT READ-ONLY

**Status:** Instruksi pelaksanaan audit  
**Berlaku untuk:** Re-audit Finance SIM-TDB dan analisis terkait  
**Mode:** Read-only audit dan specification — tanpa implementasi

## 1. Referensi wajib

Audit wajib menggunakan dan merekonsiliasi sumber berikut jika tersedia:

1. `SIMTDB_REV05112026_00_02_FINANCIAL_AMOUNT_CLARIFICATION.md`
2. `SIMTDB_REV05112026_00_03_FINANCE_CLARIFICATION_REAUDIT_AND_TEST_PROMPT.md`
3. `SIMTDB_REV05112026_00_04_AUDIT_FINANCE_REAUDIT_PROMPT.md`
4. `SIMTDB_REV05112026_00_05_FINANCE_REAUDIT_PROMPT_R01.md`
5. SOP TSKKM yang telah diunggah dan bagian SOP lain yang tersedia.
6. Master Prompt SIM-TDB V1.0, CHR, serta spesifikasi terdahulu jika tersedia.

Untuk setiap sumber, catat:
- Nama file atau identifikasi gambar.
- Judul/revisi jika tersedia.
- Status ketersediaan dan pemeriksaan.
- Halaman atau bagian yang benar-benar diperiksa.
- Keterbatasan keterbacaan atau cakupan.
- Hubungannya dengan temuan audit.

Jangan menyatakan sebuah sumber sudah diperiksa jika hanya disebut dalam daftar.

## 2. Batas sumber SOP

Gambar SOP yang tersedia dalam percakapan saat addendum ini dibuat memperlihatkan halaman cetak **16–29**.

Karena itu:

- Gunakan hanya bagian yang benar-benar tersedia dan dapat dibaca sebagai evidence langsung.
- Tandai halaman atau template yang belum tersedia sebagai `EVIDENCE_NOT_AVAILABLE`.
- Jangan menganggap seluruh SOP halaman 1–95 telah diperiksa.
- Jangan mengarang isi halaman, lampiran, template, atau prosedur yang belum tersedia.
- Jika bagian gambar buram atau tidak lengkap, tandai sebagai keterbatasan evidence dan minta sumber yang lebih jelas.

## 3. Batas perubahan

Audit harus tetap **read-only**.

Dilarang:

- Mengubah source code.
- Mengubah konfigurasi aplikasi.
- Mengubah authentication atau authorization.
- Mengubah database, collection, table, schema, atau data.
- Membuat, menjalankan, atau mengubah migration.
- Membuat seed atau akun.
- Menginstal, menghapus, atau memperbarui dependency.
- Mengubah atau menimpa file proyek yang sudah ada.
- Melakukan deploy atau publikasi.

Hasil kerja hanya berupa analisis, spesifikasi, test design, dan dokumen audit baru yang tidak menimpa file sumber.

Jika repository diperiksa, lakukan hanya pembacaan. Laporkan secara eksplisit file/area yang diperiksa dan area yang tidak dapat diperiksa.

## 4. Tujuan fondasi sistem

Audit dilakukan untuk mendukung fondasi SIM-TDB yang nantinya harus:

- Dapat digunakan secara nyata dalam operasi lapangan.
- Konsisten lintas modul dan tidak membuat sumber data ganda.
- Menjaga traceability data, keputusan, transaksi, dokumen, dan perubahan.
- Mempertahankan kewenangan organisasi dan proses SOP.
- Mendukung pengujian positif dan negatif.
- Tidak mengubah aturan organisasi melalui asumsi teknis.

Setiap rekomendasi teknis harus diberi label terpisah dari SOP dan keputusan organisasi.

## 5. Prioritas rekonsiliasi

Saat sumber berbeda atau belum lengkap:

1. Catat sumber dan perbedaannya.
2. Bedakan ketentuan langsung pemilik proyek, SOP yang terbaca, keputusan organisasi, dokumen kerja terdahulu, dan rekomendasi teknis.
3. Jangan menyelesaikan konflik dengan asumsi.
4. Tandai keputusan yang belum cukup bukti sebagai pending.
5. Jangan menaikkan status proposal menjadi keputusan yang disetujui.
6. Pastikan hasil audit menjelaskan dampak ke sumber data, approval authority, transaksi, laporan, dan pengujian.

## 6. Status hasil

Semua test yang belum benar-benar dijalankan harus berstatus `TEST_DESIGNED`, `BLOCKED_BY_MISSING_POLICY`, atau `BLOCKED_BY_MISSING_SOURCE`.

Jangan menyatakan code, database, repository, atau test suite lulus kecuali benar-benar diperiksa/dijalankan dan evidence-nya tersedia.

**Ketentuan penutup:** audit membangun fondasi spesifikasi yang dapat dipertanggungjawabkan; audit ini bukan izin untuk memulai atau mengubah implementasi.