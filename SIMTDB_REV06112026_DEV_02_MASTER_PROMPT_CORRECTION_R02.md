# SIM-TDB — MASTER PROMPT CORRECTION R02
## Audit Ulang Sumber Buku TSKKM dan Ekstraksi Role, Struktur, Tugas, serta Kewenangan

**Document ID:** SIMTDB-REV06112026-DEV-02-MASTER-PROMPT-CORRECTION-R02  
**Filename:** `SIMTDB_REV06112026_DEV_02_MASTER_PROMPT_CORRECTION_R02.md`  
**Revision:** REV06112026-R02  
**Tanggal pembuatan:** 6 November 2026  
**Status:** PROMPT KERJA — MENUNGGU PEMERIKSAAN VISUAL PDF DAN REVIEW PEMILIK PROSES  
**Mode:** Audit sumber dan ekstraksi dokumenter; tanpa desain permission final, database, atau implementasi  
**Project:** Sistem Informasi Manajemen Tanggap Darurat Bencana (SIM-TDB)  
**Organization:** Caritas Keuskupan Malang — Tim Solidaritas Kemanusiaan Keuskupan Malang (TSKKM)

---

## 1. Tujuan Dokumen

Dokumen ini adalah **Master Prompt Correction R02** untuk mengarahkan Copilot melakukan audit ulang Buku/SOP TSKKM secara disiplin berdasarkan PDF yang dirujuk pemilik proyek. Prompt ini meminta ekstraksi menyeluruh yang dapat ditelusuri ke halaman sumber; bukan persetujuan struktur organisasi, penetapan kewenangan, Role Catalog final, Permission Matrix, maupun otorisasi implementasi.

Bahan audit terakhir yang diberikan dalam percakapan adalah:

- `SIMTDB_REV06112026_DEV_01_TSKKM_ROLE_AUTHORITY_SOURCE_REGISTER_R01_Version2.md`
- `SIMTDB_REV05112026_00_13_FINANCE_DECISION_REGISTER_FINAL_AUDIT_R05_1.md`

Sumber primer yang ditunjuk pemilik proyek:

- [TSKKM SCANNER.pdf](https://github.com/fesonfeb/TSKKM/blob/main/TSKKM%20SCANNER.pdf)
- Repository: `fesonfeb/TSKKM`, branch `main`

**Status akses saat dokumen ini dibuat:** keberadaan PDF di repository dan metadata filenya dapat dikonfirmasi. Isi halaman PDF belum dapat dibaca/dirender oleh proses pembuatan dokumen ini. Karena itu, dokumen ini tidak mengklaim bahwa PDF sudah ditelaah ulang atau bahwa rekonstruksi halaman 17 telah diverifikasi terhadap gambar asli. Copilot yang menjalankan prompt ini harus membuka dan memeriksa isi PDF sebelum menyatakan hasil ekstraksi.

---

## 2. Instruksi Utama untuk Copilot

> Lakukan audit ulang terhadap `TSKKM SCANNER.pdf` dari repository `fesonfeb/TSKKM`, branch `main`, dengan membaca/merender halaman PDF yang relevan dan menelusuri seluruh halaman serta lampiran yang memuat struktur, peran, fungsi, tugas, personel, proses keputusan, penugasan, dan kewenangan. Gunakan dua dokumen audit terakhir yang diberikan sebagai bahan pembanding, bukan sebagai pengganti sumber primer.
>
> Hasilkan register ekstraksi yang akurat, lengkap sejauh sumber dapat dibaca, dan dapat diverifikasi. Pertahankan teks sumber secara verbatim untuk nama, jabatan, istilah, dan pernyataan tugas/kewenangan; cantumkan nomor halaman cetak dan nomor halaman PDF bila keduanya berbeda atau belum diketahui; sertakan kutipan pendek yang relevan serta lokasi visual/section. Klasifikasikan setiap entri secara provisional dan tandai ketidakjelasan secara eksplisit.
>
> Jangan mengarang, menyimpulkan, menormalkan, menggabungkan, memecah, menerjemahkan, atau menetapkan role, struktur komando, responsibility, decision right, mandat, delegasi, approval authority, batas nominal, user mapping, system permission, atau workflow jika hal tersebut tidak dinyatakan jelas oleh sumber yang dapat diperiksa. Jika gambar tidak terbaca, nyatakan bagian yang tidak terbaca dan minta sumber yang lebih jelas; jangan mengisi teks berdasarkan dugaan.
>
> Pisahkan secara tegas: posisi organisasi; role operasional TSKKM; fungsi; unit/tim; personel/keanggotaan; assignment per kejadian; pihak eksternal; decision gate; formal authority; identitas pengguna; system role/permission; dan status workflow. Tidak satu pun kategori tersebut otomatis membuktikan kategori lainnya.
>
> Audit ini bersifat dokumenter dan read-only. Jangan mengubah SOP, Master Context, baseline GOV/FIN, keputusan organisasi, repository source selain menyimpan dokumen audit yang secara eksplisit diminta, schema, database, migration, API, test, maupun aplikasi. Jangan menyatakan implementasi atau persetujuan telah dilakukan.

---

## 3. Dua Belas Temuan Audit yang Harus Ditangani

Temuan berikut adalah **temuan audit atas kecukupan dan batas bukti dokumen kerja sebelumnya**, bukan pernyataan bahwa isi PDF telah diverifikasi ulang. Copilot harus menjawab setiap temuan dengan bukti halaman, status, dan tindak lanjut.

| ID | Temuan audit | Tindakan wajib dalam audit R02 |
|---|---|---|
| F-01 | Audit terdahulu menyebut sumber lengkap Buku TSKKM belum diperiksa langsung; sekarang ada tautan PDF dalam repository. Keberadaan file saja tidak membuktikan isi telah dibaca. | Buka/unduh dan periksa PDF. Catat apakah seluruh halaman dapat dirender, jumlah halaman PDF, identitas/revisi dokumen yang terbaca, halaman yang hilang, serta keterbatasan OCR. Bedakan akses metadata dari inspeksi konten. |
| F-02 | Referensi “halaman 16”, “p.17”, dan seterusnya dapat merujuk nomor cetak, bukan indeks halaman PDF. | Buat pemetaan nomor halaman cetak ↔ indeks halaman PDF untuk setiap halaman yang dikutip. Jika nomor cetak tidak tampak, gunakan `PRINTED_PAGE_NOT_VISIBLE`; jangan menebaknya. |
| F-03 | Daftar struktur halaman cetak 17 dalam register lama bersumber dari ringkasan audit parsial, bukan transkripsi dan pemeriksaan ulang diagram asli. | Rekonstruksi hanya berdasarkan diagram yang terlihat. Sajikan hubungan garis/parent-child hanya jika jelas pada gambar; jika tidak, catat nama elemen tanpa hubungan. Tandai rekonstruksi sebagai provisional dan lampirkan bukti visual/rujukan halaman. |
| F-04 | Istilah jabatan, role operasional, fungsi, unit, dan tim pernah berada dalam satu inventaris sehingga berisiko dianggap sebagai role pengguna. | Klasifikasikan satu per satu dengan kategori terpisah. Berikan alasan yang merujuk ke tata letak/kalimat sumber; gunakan `NEEDS_CLASSIFICATION` saat konteks tidak cukup. |
| F-05 | “Koordinator”, “Koordinator TD”, “Koordinator Operasi”, “Koordinator Lapangan”, “Koordinator Relawan”, dan “Koordinator Bagian” berpotensi dianggap sama tanpa bukti. | Pertahankan setiap bentuk persis sebagaimana tertulis. Buat daftar kandidat istilah serupa untuk verifikasi, tetapi jangan gabungkan atau nyatakan ekuivalen kecuali sumber secara eksplisit menghubungkannya. |
| F-06 | Istilah yang diklaim berasal dari Lampiran 2 halaman 34–42 sebelumnya berstatus belum diverifikasi dari halaman asli. | Periksa seluruh rentang halaman yang ada pada PDF, bukan hanya daftar istilah sebelumnya. Ekstrak struktur operasi, istilah, tugas, dan relasi secara verbatim; tandai halaman yang tidak ada/tidak terbaca. Jangan menganggap daftar lama lengkap. |
| F-07 | Referensi Lampiran 4/personel dan halaman 45 (contoh SK) sebelumnya belum menjadi bukti yang dapat diperiksa langsung. | Temukan dan periksa halaman/lampiran yang relevan. Pisahkan isi contoh/template dari aturan yang berlaku. Jangan menyimpulkan bahwa format contoh membuktikan mandat, authority umum, batas jumlah anggota, atau SK yang benar-benar telah diterbitkan. |
| F-08 | Alur Kajian Cepat dan keputusan Respons/Tidak Respons memiliki beberapa aktor/gate yang tidak boleh dilebur. | Transkripsikan tahapan dan aktor sesuai sumber. Bedakan assessment, validasi, keputusan Respons/Tidak Respons, pembentukan tim Paroki, monitoring, dan persetujuan dana. Jika aktor atau urutan tidak eksplisit, tandai `NEEDS_CLARIFICATION`. |
| F-09 | Teks persetujuan pengeluaran dana darurat oleh Ketua TSKKM pada halaman 23 (dilaporkan oleh audit terdahulu) tidak membuktikan identitas pemegang jabatan, mandat/delegasi, cakupan kewenangan, atau account mapping. | Verifikasi redaksi halaman 23 langsung. Laporkan hanya teks yang terlihat dan konteksnya. Pisahkan `source wording` dari penetapan formal authority; pertahankan FIN-DEC-33 sebagai pending untuk mandate/delegation dan mapping yang belum tersedia. |
| F-10 | Role/permission aplikasi, keanggotaan tim, assignment, serta formal authority merupakan relasi yang berbeda. | Jadikan pemisahan ini kontrol eksplisit untuk seluruh hasil. Jangan menurunkan permission atau authority dari nama jabatan, nama tim, atau kepemilikan akun. Tandai mapping sebagai belum diputuskan bila tidak ada matriks/keputusan formal. |
| F-11 | Status evidence sebelumnya menggunakan istilah parsial/terkonfirmasi, tetapi cakupan bukti tiap klaim harus lebih granular. | Setiap klaim harus memiliki sumber, halaman, kutipan singkat, cara inspeksi (teks/OCR/visual), tingkat keterbacaan, status verifikasi, dan batas interpretasi. Jangan memberi status `VERIFIED_FROM_SOURCE` jika halaman asli tidak diperiksa langsung. |
| F-12 | Dokumen audit terdahulu menegaskan status no-go untuk Role Catalog final, Permission Matrix, desain fisik, dan implementasi; audit ulang tidak dengan sendirinya mengubah status tata kelola. | Pertahankan baseline dan status keputusan yang belum disetujui. R02 boleh merekomendasikan langkah dokumentasi berikutnya saja. Jangan mengubah GOV-01–GOV-09, FIN-DEC-01–FIN-DEC-33, FIN-TEST-01–FIN-TEST-105, FIN-DEC-33, atau menyatakan keputusan/implementasi telah disetujui. |

---

## 4. Rekonstruksi Kerja Struktur Halaman Cetak 17

### 4.1 Batas bukti

Daftar berikut merekam istilah yang telah disebut dalam register audit sebelumnya untuk halaman cetak 17. **Ini bukan hasil pembacaan ulang PDF dan bukan rekonstruksi diagram yang terverifikasi.** Nama dan keberadaan setiap elemen harus dicocokkan oleh Copilot dengan gambar halaman asli. Jangan menyimpulkan garis komando, kelompok, jumlah orang, relasi pelaporan, atau kewenangan dari daftar teks ini.

### 4.2 Kandidat elemen untuk dicocokkan

| Ref kerja | Istilah sebagaimana dilaporkan | Kategori sementara untuk audit | Instruksi verifikasi |
|---|---|---|---|
| P17-01 | Ketua TSKKM | Kandidat posisi organisasi | Periksa label dan posisi visual; authority hanya dicatat jika dinyatakan pada sumber terkait. |
| P17-02 | Sekretaris | Kandidat posisi organisasi | Periksa ejaan, posisi, relasi garis, dan konteks. |
| P17-03 | Bendahara | Kandidat posisi organisasi | Jangan simpulkan sebagai approver Finance; periksa teks tugas/authority terpisah. |
| P17-04 | Koordinator TD | Perlu klasifikasi | Pertahankan sebagai istilah sendiri; jangan samakan dengan “Koordinator” tanpa bukti. |
| P17-05 | Bidang pengungsi | Kandidat unit/bidang | Periksa apakah benar label diagram dan apakah ada tugas tertulis. |
| P17-06 | Bidang kesehatan | Kandidat unit/bidang | Periksa label dan relasi pada diagram. |
| P17-07 | Tim dapur | Kandidat tim/fungsi | Jangan otomatis membuat application role. |
| P17-08 | Logistik | Kandidat unit/fungsi | Bandingkan konteks halaman lain; jangan gabungkan penggunaan berbeda. |
| P17-09 | Gudang | Kandidat unit/fungsi | Jangan samakan dengan “Staff Gudang” sebelum ada bukti eksplisit. |
| P17-10 | Transportasi | Kandidat unit/fungsi | Periksa label dan uraian tugas jika tersedia. |
| P17-11 | Distribusi | Kandidat unit/fungsi | Bandingkan dengan istilah sektor/pelayanan pada halaman lain. |
| P17-12 | Monitoring dan Evaluasi | Kandidat unit/fungsi | Bedakan dari proses monitoring/evaluasi, jika keduanya disebut. |
| P17-13 | Mitigasi | Kandidat unit/fungsi | Bedakan label organisasi dari kategori pelayanan/program. |

### 4.3 Format rekonstruksi yang harus dihasilkan setelah inspeksi

Copilot harus mengganti/melengkapi tabel kandidat di atas dengan tabel bukti berikut. Jangan mengisi relasi visual jika garis atau label tidak dapat dibaca.

| Elemen verbatim | Halaman cetak | Halaman PDF | Posisi/relasi yang benar-benar terlihat | Klasifikasi provisional | Kutipan/catatan visual | Keterbacaan | Status | Catatan/pending |
|---|---:|---:|---|---|---|---|---|---|
| … | … | … | `VISIBLE` / `NOT_CLEAR` / `NOT_SHOWN` | … | … | … | … | … |

Jika mungkin, sertakan crop gambar halaman 17 atau koordinat/region yang memungkinkan reviewer menelusuri elemen. Diagram teks (misalnya Mermaid) hanya boleh dibuat jika hubungan visual memang jelas; tandai semua interpretasi dan jangan menambahkan struktur yang tidak ada di halaman.

---

## 5. Indeks Halaman Sumber yang Harus Diperiksa

Indeks di bawah menggabungkan rujukan yang disebut dokumen audit sebelumnya. Semua nomor adalah **nomor halaman cetak yang diklaim**, belum dipetakan ke indeks PDF dalam dokumen ini. Copilot wajib memverifikasinya terhadap PDF dan memperluas indeks bila menemukan halaman lain yang relevan.

| Halaman cetak / rentang yang dirujuk | Topik yang diklaim relevan | Dasar rujukan saat ini | Pemeriksaan R02 |
|---|---|---|---|
| 16 | Tingkat respons Rendah/Sedang/Tinggi; Paroki, TSKKM, KARINA-KWI | Register audit dan finance audit sebelumnya menyebut gambar/hasil telaah parsial | Periksa tabel asli, seluruh ambang, catatan kaki, aktor, keterbacaan angka. Catat nomor PDF. |
| 17 | Struktur organisasi TSKKM | Ringkasan audit parsial yang dikutip di register sebelumnya | Periksa diagram penuh, ejaan, garis, pengelompokan, dan legenda. Jangan inferensikan hubungan yang tidak jelas. |
| 18 | Sektor pelayanan/konteks Logistik, Distribusi, Mitigasi | Referensi audit parsial sebelumnya | Verifikasi redaksi dan bedakan sektor pelayanan dari unit organisasi. |
| 20 | Koordinator, Fasilitator, Animator | Rujukan audit parsial/Master Context yang disuplai | Kutip uraian tugas persis; catat subjek, kata kerja, tingkat wilayah, dan batas yang benar-benar tertulis. |
| 21–22 | Kajian Cepat, Tim Kajian, SITREP #1, Respons/Tidak Respons, monitoring | Ringkasan audit parsial sebelumnya | Rekonstruksi urutan proses dan aktor per kalimat/diagram; identifikasi form/output serta status bila tertulis. |
| 22–23 | Keputusan dan pembentukan Tim Tanggap Darurat Paroki | Ringkasan audit parsial sebelumnya | Pisahkan actor, gate, keputusan, dan bukti pembentukan. Verifikasi urutan dan kata kerja. |
| 23 | Pengeluaran dana darurat dan persetujuan Ketua TSKKM; nominal yang terlihat | Ringkasan audit parsial; FIN-DEC-33 | Verifikasi kata-kata, konteks tabel/paragraf, satuan, nominal, syarat dan catatan. Jangan simpulkan mandat atau identitas pemegang jabatan. |
| 24 | Sumber/kategori penggunaan dana; kategori pembatasan APP Nasional; KARINA-KWI dalam konteks terkait | Finance audit sebelumnya menyatakan gambar p.24 ditelaah parsial | Verifikasi semua redaksi dan daftar lengkap; jangan perluas larangan/aturan beyond source. |
| 26 | Monitoring dan Evaluasi | Ringkasan audit parsial sebelumnya | Bedakan unit/fungsi/aktivitas dan dokumentasikan tugas yang tertulis. |
| 34–42 | Lampiran 2 — Manajemen Operasi Tanggap Darurat; struktur dan tim operasi | Dirujuk sebagai rentang dalam register sebelumnya, tetapi halaman asli saat itu belum tersedia untuk inspeksi | Periksa seluruh rentang pada PDF. Catat setiap heading, istilah gabungan, deskripsi tugas, diagram, tabel, dan aktor. Jangan menganggap istilah lama lengkap. |
| 45 | Contoh Surat Keputusan | Dirujuk dalam register sebelumnya; belum diperiksa langsung saat itu | Identifikasi sebagai contoh/template atau dokumen formal; jangan gunakan contoh untuk menetapkan authority aktual. |
| Lampiran 4 / halaman terkait | Istilah/personel operasional yang disebut dalam materi proyek | Rujukan audit sebelumnya belum memiliki indeks halaman pasti | Cari di seluruh PDF, catat judul lampiran dan nomor halaman tepat; jangan merekonstruksi nomor. |
| 49 (rujukan terpisah) | Template APP-KWI yang disebut pada finance audit | R05.1 menyatakan template halaman 49 tidak tersedia untuk diperiksa saat audit sebelumnya | Periksa apakah halaman tersebut ada di PDF yang sama dan apa sumbernya. Jangan anggap tersedia atau sama dengan SOP sebelum verifikasi. |
| Semua halaman lain | Struktur, definisi, prosedur, lampiran, glosarium, revisi dokumen | Belum terinventarisasi menyeluruh | Lakukan scan keseluruhan dokumen untuk menemukan sumber tambahan; indeks bukan daftar tertutup. |

### 5.1 Format indeks halaman final

Setiap halaman yang dikutip dalam laporan akhir harus dicatat dengan format:

| Source ID | Nama sumber/revisi | Halaman PDF | Halaman cetak | Bagian/heading | Elemen yang diekstrak | Metode (visual/OCR/teks) | Keterbacaan | Link/crop atau locator | Status verifikasi |
|---|---|---:|---:|---|---|---|---|---|---|

Jangan menyebut “p.17” saja bila nomor halaman cetak/PDF berpotensi berbeda.

---

## 6. Aturan Ekstraksi Verbatim dan Provenance

1. **Salin istilah persis.** Pertahankan ejaan, kapitalisasi, tanda baca, singkatan, bahasa, dan bentuk tunggal/jamak sumber. Koreksi OCR hanya boleh dicatat sebagai saran terpisah, bukan mengganti kutipan sumber.
2. **Kutip tugas/kewenangan secara langsung.** Jangan mengubah kata kerja seperti “membantu”, “mengatur”, “mengoordinasi”, “menyetujui”, atau “memutuskan” menjadi kewenangan yang lebih kuat/lemah.
3. **Satu klaim, satu rujukan.** Setiap nama, responsibility, relasi, decision gate, nominal, atau authority harus menunjuk halaman/section dan bagian sumber yang mendukungnya.
4. **Tandai keterbacaan.** Gunakan `CLEAR`, `PARTIALLY_LEGIBLE`, `ILLEGIBLE`, atau `NOT_INSPECTED`. Jangan mengisi bagian `ILLEGIBLE` berdasarkan konteks saja.
5. **Pisahkan sumber primer dan ringkasan.** Ringkasan audit, Master Context, percakapan, maupun proposal adalah sumber konteks, bukan kutipan langsung SOP. Beri label asalnya.
6. **Jangan gabungkan istilah yang mirip.** Buat cross-reference kandidat bila perlu, tetapi status ekuivalensi harus `NOT_ESTABLISHED` sampai ada bukti eksplisit.
7. **Jangan membentuk hierarki dari urutan daftar.** Garis, kotak, indentasi, posisi, legenda, dan label harus terlihat jelas sebelum menyatakan parent/child atau reporting line.
8. **Jangan menambahkan tugas dari pengetahuan umum.** Kolom tanggung jawab harus berisi kutipan/para-frasa dekat yang didukung sumber. Jika tidak ada, tulis `NOT_STATED_IN_INSPECTED_SOURCE`.
9. **Jangan menyamakan kehadiran dengan kewenangan.** Kehadiran pada tabel/diagram partisipasi atau level respons bukan bukti approval authority, system permission, ataupun penugasan permanen.
10. **Jangan menyimpulkan mandate/delegation.** Jabatan yang disebut sumber bukan bukti siapa pemegangnya saat ini, cakupan mandat, masa berlaku, delegasi, acting authority, atau pemetaan account.
11. **Pertahankan konflik.** Jika dua sumber berbeda, kutip masing-masing, beri `SOURCE_CONFLICT`, dan jangan memilih salah satunya tanpa keputusan pemilik yang berwenang.
12. **Cantumkan absensi bukti.** Bedakan `EVIDENCE_NOT_AVAILABLE`, `NOT_FOUND_AFTER_SEARCH`, `NOT_INSPECTED`, dan `ILLEGIBLE`; semuanya memiliki arti berbeda.
13. **Jangan mengklaim kelengkapan tanpa pemeriksaan menyeluruh.** Laporkan halaman yang diperiksa, yang dilewati, dan alasan keterbatasan.
14. **OCR bukan kebenaran sumber.** Bila OCR tidak sesuai visual, prioritaskan visual dan catat koreksi/transkripsi dengan reviewer atau confidence note.
15. **Jangan membuat keputusan konfigurasi.** Klasifikasi provisional tidak berarti Role Catalog, permission mapping, schema, atau proses organisasi telah disetujui.

---

## 7. Taksonomi Klasifikasi dan Status

Gunakan klasifikasi terpisah berikut sebagai label kerja, bukan keputusan final:

- `ORGANIZATIONAL_POSITION_CANDIDATE`
- `TSKKM_OPERATIONAL_ROLE_CANDIDATE`
- `OPERATIONAL_FUNCTION_CANDIDATE`
- `UNIT_OR_TEAM_CANDIDATE`
- `PERSONNEL_OR_MEMBERSHIP_TERM`
- `OPERATIONAL_ASSIGNMENT_CANDIDATE`
- `EXTERNAL_STAKEHOLDER_CANDIDATE`
- `DECISION_GATE_CANDIDATE`
- `FORMAL_AUTHORITY_REFERENCE`
- `SYSTEM_PERMISSION_CONCEPT`
- `NEEDS_CLASSIFICATION`

Status verifikasi yang diizinkan:

- `VERIFIED_FROM_SOURCE` — halaman asli diperiksa langsung, teks/relasi terbaca dan locator tersedia.
- `PARTIALLY_VERIFIED` — hanya sebagian wording/konteks yang terbaca atau cakupan sumber parsial.
- `NEEDS_CLASSIFICATION`
- `NEEDS_CLARIFICATION`
- `PENDING_AUTHORITY_MAPPING`
- `SOURCE_CONFLICT`
- `EVIDENCE_NOT_AVAILABLE`
- `NOT_INSPECTED`
- `ILLEGIBLE`
- `NOT_APPLICABLE`

**Tidak ada status otomatis `APPROVED_FOR_CONFIGURATION`.** Persetujuan hanya dapat dinyatakan dengan bukti keputusan formal yang tersedia dan diverifikasi.

---

## 8. Skema Register Ekstraksi yang Diminta

Buat satu baris per istilah/klaim sumber. Jangan satukan beberapa istilah hanya karena kemungkinan merujuk fungsi yang sama.

| Field | Isi wajib |
|---|---|
| Register ID | ID unik yang stabil. Jangan menimpa ID lama tanpa crosswalk. |
| Exact source wording | Kutipan pendek verbatim atau label persis. |
| Source ID and version | Nama file, versi/revisi, metadata yang terbaca. |
| Printed page / PDF page | Keduanya, atau status tidak diketahui yang eksplisit. |
| Section/visual locator | Heading, paragraf, tabel, kotak, baris, diagram, atau crop. |
| Classification | Satu label provisional atau `NEEDS_CLASSIFICATION`. |
| Responsibility wording | Kutipan sumber; `NOT_STATED_IN_INSPECTED_SOURCE` bila tidak ditemukan. |
| Relationship shown | Hanya relasi yang benar-benar tampak/tertulis. |
| Evidence method/readability | Visual/OCR/text; `CLEAR`/parsial/tidak terbaca. |
| Verification status | Salah satu status di §7. |
| Interpretation boundary | Apa yang tidak dapat disimpulkan dari bukti ini. |
| Open question / evidence request | Sumber atau klarifikasi yang masih diperlukan. |

Untuk keputusan/authority, tambahkan: actor seperti tertulis; tindakan; objek keputusan; kondisi; tahap proses; sumber mandat (jika ada); scope/nominal (hanya jika tertulis); masa berlaku/delegasi (hanya jika tertulis); dan account mapping status.

---

## 9. Kontrol Khusus Finance dan Authority

1. FIN-DEC-33 tetap menjadi keputusan pending untuk identitas pemegang authority formal, mandat/delegasi, scope, validity period, acting authority, prosedur persetujuan, dan mapping user/account.
2. Bila halaman 23 menunjukkan persetujuan Ketua TSKKM untuk pengeluaran dana darurat, laporkan hanya redaksi dan konteks yang benar-benar terbaca. Jangan menyimpulkan siapa pemegang jabatan, apakah mandat didelegasikan, atau apakah approval berlaku untuk keputusan Respons/Tidak Respons.
3. Keputusan Respons/Tidak Respons, validasi kajian cepat, pembentukan Tim Tanggap Darurat Paroki, dan persetujuan pengeluaran dana adalah decision gate terpisah kecuali SOP secara eksplisit menghubungkannya.
4. Pertahankan FIN-DEC-01–FIN-DEC-33 dan FIN-TEST-01–FIN-TEST-105 sebagai baseline yang dikutip dokumen terakhir. Jangan mengedit atau menyatakan statusnya berubah melalui audit ekstraksi ini.
5. Jangan mengubah arti Rp50.000.000 atau fixture Rp100.000.000. Jangan menetapkan nilai baru/default/threshold dari hasil OCR atau contoh dokumen.
6. System administrator/SuperAdmin, permission, account, authority organisasi, dan authority Finance adalah konsep yang berbeda.

---

## 10. Bentuk Output Audit R02

Hasil kerja Copilot setelah memeriksa PDF harus berisi bagian berikut:

1. **Ringkasan eksekutif** — apa yang diperiksa, cakupan, batasan, dan status kesiapan.
2. **Metadata sumber** — judul/revisi/tanggal/penerbit sebagaimana terbaca; jumlah halaman PDF; halaman cetak yang tampak.
3. **Metode audit** — inspeksi visual, ekstraksi teks, OCR, quality check; catat keterbatasan.
4. **Indeks halaman sumber final** — cetak dan PDF page mapping.
5. **12 temuan audit** — status tiap F-01–F-12, bukti halaman, hasil, open issue.
6. **Ekstraksi struktur p.17** — verbatim, layout/relasi yang benar-benar terlihat, klasifikasi provisional, bukti visual, ketidakjelasan.
7. **Register seluruh istilah/role/fungsi/tim/personel** yang relevan dari semua halaman dan lampiran yang diperiksa.
8. **Register proses/decision gate/authority** dengan actor, tindakan, kondisi, urutan, sumber mandat, dan batas bukti.
9. **Crosswalk** terhadap dua dokumen audit terdahulu: cocok, perlu koreksi, belum terverifikasi, atau konflik; jangan hapus provenance.
10. **Daftar konflik dan permintaan bukti** termasuk halaman kabur, halaman tidak ada, mandate/delegation, serta matriks permission bila relevan.
11. **Readiness assessment** untuk source extraction, role inventory, authority mapping, Permission Matrix, desain database fisik, dan implementasi.
12. **Correction log dan kesimpulan**. Tegaskan apa yang tidak diubah dan keputusan apa yang tetap pending.

### Syarat kualitas

- Setiap temuan substantif dapat ditelusuri ke halaman dan locator.
- Istilah sumber tidak dinormalisasi diam-diam.
- Tidak ada role atau kewenangan yang dikarang.
- Klaim “seluruh Buku TSKKM telah diperiksa” hanya boleh dibuat jika semua halaman dan lampiran memang dibuka dan diperiksa, dengan pengecualian dicatat.
- Bila PDF tidak bisa dibuka/diekstrak, berhenti pada audit akses dan daftar evidence yang diperlukan; jangan mengisi register seolah-olah sudah membaca sumber.

---

## 11. Larangan Tegas

Copilot tidak boleh:

- Mengarang nama jabatan, role, tim, responsibility, hubungan hierarki, atau kewenangan.
- Mengubah dugaan audit lama menjadi fakta sumber.
- Menganggap daftar halaman 17 di §4 sebagai transkripsi PDF yang telah diverifikasi.
- Menyamakan Ketua TSKKM dengan Romo Direktur, Koordinator dengan Koordinator TD, atau posisi lain tanpa bukti eksplisit.
- Menurunkan system permission, approval workflow, authority, atau user role dari jabatan/keanggotaan tim.
- Menafsirkan gambar buram atau OCR confidence rendah sebagai fakta.
- Menganggap contoh SK sebagai SK yang berlaku atau bukti mandat aktual.
- Menganggap keterlibatan KARINA-KWI/pihak eksternal sebagai user internal atau role aplikasi.
- Membuat keputusan nominal, aggregation, funding, closure, atau policy baru.
- Mengubah baseline project-owner governance, Finance decisions/tests, SOP, Master Context, atau source repository.
- Membuat schema, FK, migration, API, seed, kode, atau implementasi dari inventaris provisional.
- Menyatakan audit disetujui organisasi tanpa bukti persetujuan yang dapat ditinjau.

---

## 12. Baseline yang Dipertahankan

Dokumen ini tidak mengubah:

- GOV-01 sampai GOV-09.
- FIN-DEC-01 sampai FIN-DEC-33, termasuk FIN-DEC-33 yang tetap pending untuk authority mapping formal.
- FIN-TEST-01 sampai FIN-TEST-105; seluruh Actual Result yang sebelumnya `Not Executed` tetap demikian kecuali ada bukti eksekusi baru yang terpisah.
- Status R05.1 sebagai working audit document.
- Status Role Catalog/Permission Matrix final yang belum disetujui.
- Status Physical Database Design `NO_GO` dan Implementation `NO_GO` pada bahan audit terakhir.

Audit ekstraksi sumber dapat memperbaiki bukti dokumenter, tetapi tidak sendirinya menetapkan keputusan organisasi atau mengubah status no-go.

---

## 13. Status Dokumen Ini

**Master Prompt Correction R02:** prompt kerja untuk audit ulang.  
**Pemeriksaan isi PDF dalam pembuatan file ini:** belum dilakukan; metadata/keberadaan file dapat dikonfirmasi, isi halaman belum ditelaah langsung.  
**Rekonstruksi p.17:** kandidat dari audit sebelumnya, belum terverifikasi.  
**Role Catalog final / Permission Matrix:** tidak dibuat dan tidak disetujui oleh dokumen ini.  
**Physical Database Design / Implementation:** tidak dilakukan; tetap mengikuti baseline no-go yang diberikan.

**End of Master Prompt Correction R02.**
