# SIM-TDB — ADDENDUM DASAR AUDIT CORRECTION REGISTER

**Document ID:** SIMTDB-REV05112026-00-15-FIN-CR-BASIS  
**Status:** Catatan klarifikasi untuk audit berikutnya  
**Mode:** Dokumentasi dan audit planning — tanpa implementasi  
**Project:** Sistem Informasi Manajemen Tanggap Darurat Bencana (SIM-TDB)  
**Organization:** Caritas Keuskupan Malang — Tim Solidaritas Kemanusiaan Keuskupan Malang (TSKKM)

---

## 1. Tujuan

Addendum ini mencatat klarifikasi bahwa **SIM-TDB Finance Correction Register — Audit Findings and Corrective Action Register R01 → R02** disusun berdasarkan pemeriksaan ulang dua dokumen utama:

1. `SIMTDB_REV05112026_00_14_FINANCE_LOGICAL_ARCHITECTURE_R01.md`
2. `SIMTDB_REV05112026_00_13_FINANCE_DECISION_REGISTER_FINAL_AUDIT_R05_1.md`

Addendum ini menjadi konteks untuk audit dan koreksi R01 berikutnya. Addendum tidak menggantikan Correction Register dan tidak menutup temuan apa pun.

## 2. Peran dokumen dalam audit

| Dokumen | Peran dalam audit |
|---|---|
| `SIMTDB_REV05112026_00_14_FINANCE_LOGICAL_ARCHITECTURE_R01.md` | Objek utama pemeriksaan: katalog entitas, atribut, hubungan, proses, integrasi, dan traceability. |
| `SIMTDB_REV05112026_00_13_FINANCE_DECISION_REGISTER_FINAL_AUDIT_R05_1.md` | Baseline pengendali: governance, FIN-DEC-01–33, koreksi hubungan logical, FIN-TEST-01–105, serta evidence dan status keputusan. |
| Finance Correction Register R01 → R02 | Register temuan, prioritas, tindakan koreksi, acceptance criteria, dan status perbaikan. |

## 3. Aturan penggunaan sumber

1. R05.1 digunakan sebagai baseline keputusan dan provenance; R01 diperiksa terhadap baseline tersebut.
2. Temuan dalam Correction Register harus memiliki rujukan ke bagian R01, kebutuhan/keputusan R05.1, dan corrective action yang dapat diuji.
3. Correction Register tidak dengan sendirinya mengubah atau menyetujui keputusan organisasi.
4. GOV-01–GOV-09, FIN-DEC-01–FIN-DEC-33, dan FIN-TEST-01–FIN-TEST-105 tetap dipertahankan sesuai baseline yang berlaku.
5. Keputusan yang belum memiliki evidence tetap pending; rekomendasi teknis tidak diubah menjadi kebijakan.
6. Status R01 tetap **NOT PASSED — CORRECTION REQUIRED** sampai tindakan koreksi diperiksa.
7. R02 tetap belum diserahkan sampai dokumen lengkap dibuat dan siap diaudit ulang.

## 4. Status kerja yang dipertahankan

| Item | Status |
|---|---|
| Finance Logical Architecture R01 | `NOT PASSED — CORRECTION REQUIRED` |
| Finance Logical Architecture R02 | `NOT YET SUBMITTED` |
| Finance Logical Architecture Final | `BLOCKED` |
| Physical Database Design | `NO_GO` |
| Implementation | `NO_GO` |
| Perubahan code/database | Tidak dilakukan |

## 5. Batas audit

Audit dan koreksi selanjutnya tetap read-only terhadap code dan database. Pemeriksaan dokumen tidak berarti repository, schema, aplikasi, atau test suite telah diperiksa atau dijalankan.

Sumber SOP yang belum tersedia tetap ditandai `EVIDENCE_NOT_AVAILABLE`. Tidak ada isi SOP, authority, mandat, data model, atau hasil test yang boleh dikarang untuk mengisi kekosongan.

**Kesimpulan:** Correction Register dikendalikan oleh pembacaan Finance Logical Architecture R01 terhadap baseline Finance Decision Register R05.1. R01 belum lulus dan R02 belum diserahkan; status tersebut tetap berlaku sampai tindakan koreksi selesai serta lolos audit ulang.