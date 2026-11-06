# SIM-TDB — TSKKM ROLE & AUTHORITY SOURCE REGISTER
## Source Extraction, Classification, and Verification Register — R01

**Document ID:** SIMTDB-REV06112026-DEV-01-TSKKM-ROLE-AUTH-R01  
**Filename:** `SIMTDB_REV06112026_DEV_01_TSKKM_ROLE_AUTHORITY_SOURCE_REGISTER_R01.md`  
**Revision:** REV06112026-R01  
**Status:** DRAFT — SOURCE RECONCILIATION REQUIRED  
**Mode:** Read-only source inventory and role/authority traceability — no implementation  
**Project:** Sistem Informasi Manajemen Tanggap Darurat Bencana (SIM-TDB)  
**Organization:** Caritas Keuskupan Malang — Tim Solidaritas Kemanusiaan Keuskupan Malang (TSKKM)

---

## 1. Purpose

Register ini menjadi dokumen pendukung untuk menelusuri istilah struktur organisasi, peran, fungsi, tim, tanggung jawab, penugasan, dan kewenangan yang dirujuk dalam rancangan SIM-TDB.

Tujuannya:

1. Memisahkan istilah yang bersumber dari materi SOP yang tersedia dari istilah yang hanya disebut dalam materi proyek.
2. Mencatat sumber dan halaman yang diklaim relevan tanpa menganggap sumber yang tidak tersedia telah diperiksa.
3. Mengklasifikasikan istilah secara sementara tanpa mengubah jabatan, peran, atau kewenangan organisasi.
4. Menjadi dasar kerja untuk ekstraksi lengkap Buku TSKKM sebelum Role Catalog, User Management, atau Permission Matrix difinalisasi.
5. Menjaga batas antara posisi organisasi, TSKKM role, fungsi operasional, assignment, system permission, dan formal authority.

Register ini **bukan** Role Catalog final, Permission Matrix, keputusan organisasi, atau persetujuan implementasi.

---

## 2. Document Authority and Baseline

### 2.1 Source authority

Buku Prosedur Operasional Baku (SOP) Tanggap Darurat Bencana Keuskupan Malang merupakan sumber utama untuk mengekstrak struktur, peran, fungsi, tanggung jawab, dan mekanisme kerja TSKKM.

Setiap interpretasi tetap tunduk pada:

1. SOP resmi yang tersedia dan dapat dibaca.
2. Keputusan organisasi formal dengan bukti yang dapat diverifikasi.
3. Baseline project-owner governance yang berlaku.
4. FIN-DEC-01 sampai FIN-DEC-33 untuk keputusan Finance.
5. Rekomendasi teknis yang hanya berstatus proposal sampai disetujui.

Register ini tidak menggantikan SOP dan tidak menyelesaikan konflik sumber.

### 2.2 Baselines preserved

Dokumen ini tidak mengubah:

- GOV-01 sampai GOV-09.
- FIN-DEC-01 sampai FIN-DEC-33.
- FIN-TEST-01 sampai FIN-TEST-105.
- Kewenangan persetujuan yang telah dinyatakan dalam sumber.
- Status keputusan yang masih pending.

R05.1 tetap menjadi baseline keputusan Finance. FIN-DEC-33 tetap berlaku untuk pertanyaan formal authority persetujuan pengeluaran dana darurat. Register ini tidak menetapkan identitas pemegang jabatan, mandat, delegasi, batas kewenangan, atau mapping ke akun sistem.

---

## 3. Source Inventory and Evidence Availability

| Source ID | Source / exact filename | Page or section | Availability | Inspection status | Use and limitation |
|---|---|---:|---|---|---|
| SRC-01 | `SIMTDB_REV05112026_00_01_SOP_PARTIAL_AUDIT.md` | Melaporkan gambar cetak p.16–29 | Konten diberikan dalam percakapan | Dibaca sebagai laporan audit parsial | Bukan Buku TSKKM lengkap; membatasi klaim pada halaman yang disebut dan terbaca. |
| SRC-02 | Gambar SOP TSKKM | Cetak p.16–29 | Tersedia menurut materi proyek | Teks/hasil telaah yang tersedia digunakan; tidak semua gambar diperiksa ulang secara langsung dalam pembuatan register ini | P.17, p.20–24, dan p.23 relevan; sebagian angka p.16 buram menurut audit parsial. |
| SRC-03 | Buku TSKKM / SOP asli lengkap | P.1–95 dan lampiran | `EVIDENCE_NOT_AVAILABLE` untuk pemeriksaan lengkap | Tidak diperiksa secara penuh | Tidak boleh mengklaim seluruh role, responsibility, authority, atau workflow telah diekstrak. |
| SRC-04 | Lampiran 2 — Manajemen Operasi Tanggap Darurat | Disebut p.34–42 | `EVIDENCE_NOT_AVAILABLE` sebagai halaman asli | Tidak tersedia untuk transkripsi langsung | Istilah di register ini yang merujuk lampiran hanya berasal dari kutipan/ringkasan yang diberikan; belum diverifikasi terhadap halaman asli. |
| SRC-05 | Contoh Surat Keputusan | Disebut p.45 | `EVIDENCE_NOT_AVAILABLE` sebagai halaman asli | Tidak tersedia untuk pemeriksaan langsung | Tidak dipakai untuk menyimpulkan batas jumlah anggota atau authority umum. |
| SRC-06 | `SIMTDB_REV05112026_00_13_FINANCE_DECISION_REGISTER_FINAL_AUDIT_R05_1.md` | FIN-DEC-33 | Konten diberikan dalam percakapan | Dibaca sebagai baseline | FIN-DEC-33 tetap pending untuk identity/mandate/delegation/account mapping. |
| SRC-07 | `SIMTDB_REV05112026_00_14_FINANCE_LOGICAL_ARCHITECTURE_R02_Version2.md` | Authority/IAM dan Finance traceability | Konten diberikan dalam percakapan | Dibaca sebagai konteks | Bukan bukti formal mandate atau authority. |
| SRC-08 | Master Context R01 | §§5, 8.2, 9, 12, 19 | Konten diberikan dalam percakapan | Dibaca | Draft yang perlu dikoreksi melalui change control; tidak diubah oleh register ini. |
| SRC-09 | Keputusan formal, mandat, delegasi, approval matrix | Tidak diketahui | `EVIDENCE_NOT_AVAILABLE` | Tidak diperiksa | Tidak boleh direka atau disimpulkan dari jabatan/permission. |
| SRC-10 | Role/permission matrix yang disetujui | Tidak diketahui | `EVIDENCE_NOT_AVAILABLE` | Tidak diperiksa | Tidak dapat menyatakan permission mapping telah disetujui. |

### 3.1 Evidence distinction

Register menggunakan empat macam evidence basis:

- **Source wording in supplied material:** redaksi atau istilah yang tersedia dalam materi yang diberikan.
- **Partial SOP audit report:** ringkasan pembacaan gambar p.16–29; bukan pemeriksaan seluruh SOP.
- **Project document statement:** requirement yang dicantumkan dalam Master Context atau audit proyek; belum tentu kutipan langsung SOP.
- **Unavailable source:** halaman/dokumen asli belum tersedia untuk pencocokan.

Jika sumber asli tidak tersedia, klasifikasi yang sesuai adalah `EVIDENCE_NOT_AVAILABLE` atau `SOP_NOT_VERIFIED`, bukan `SOP_CONFIRMED`.

---

## 4. Classification and Status Vocabulary

### 4.1 Classification

| Classification | Meaning |
|---|---|
| `ORGANIZATIONAL_POSITION_CANDIDATE` | Istilah tampak sebagai jabatan/posisi dalam struktur; klasifikasi final masih harus dicocokkan dengan diagram dan konteks sumber. |
| `TSKKM_OPERATIONAL_ROLE_CANDIDATE` | Istilah disebut sebagai peran operasional TSKKM; belum otomatis menjadi application role. |
| `OPERATIONAL_FUNCTION_CANDIDATE` | Fungsi kerja; tidak otomatis merupakan jabatan atau role permanen. |
| `UNIT_OR_TEAM_CANDIDATE` | Bidang, unit, atau tim; tidak otomatis satu user role. |
| `OPERATIONAL_ASSIGNMENT_CANDIDATE` | Penugasan untuk kejadian/operasi; harus memiliki sumber/keputusan pembentuk dan masa berlaku bila ditetapkan. |
| `EXTERNAL_STAKEHOLDER_CANDIDATE` | Organisasi atau pihak eksternal; tidak otomatis menjadi internal application role. |
| `SYSTEM_PERMISSION_CONCEPT` | Hak tindakan di aplikasi; bukan jabatan atau formal authority. |
| `FORMAL_AUTHORITY_REFERENCE` | Kewenangan yang harus didukung sumber/mandat/keputusan formal; tidak disimpulkan dari nama jabatan. |
| `PROJECT_SNAPSHOT_ONLY` | Daftar awal dari materi proyek; bukan daftar lengkap atau otoritatif. |
| `NEEDS_CLASSIFICATION` | Belum cukup evidence untuk menentukan jenis istilah. |

### 4.2 Verification Status

| Status | Meaning |
|---|---|
| `VERIFIED_FROM_SOURCE` | Sumber asli yang memuat istilah telah tersedia dan diperiksa langsung dengan lokasi yang dapat ditelusuri. |
| `PARTIALLY_VERIFIED` | Bukti terbatas/parsial mendukung istilah, tetapi konteks atau keseluruhan sumber belum diperiksa. |
| `NEEDS_CLASSIFICATION` | Istilah terlihat, tetapi jenisnya belum dapat dipastikan. |
| `NEEDS_CLARIFICATION` | Makna, relasi, atau batas tanggung jawab belum jelas. |
| `PENDING_AUTHORITY_MAPPING` | Peran/istilah terlihat, tetapi formal authority dan pemetaan aplikasi belum diverifikasi. |
| `EVIDENCE_NOT_AVAILABLE` | Sumber yang diperlukan tidak tersedia untuk pemeriksaan. |
| `NOT_APPLICABLE` | Field tidak relevan untuk istilah tersebut. |

Tidak ada entri di bawah ini yang dinyatakan `APPROVED_FOR_CONFIGURATION` atau “Role Catalog final”.

---

## 5. Register A — Istilah Struktur TSKKM, Printed Page 17

**Evidence boundary:** daftar di bawah berasal dari ringkasan audit parsial atas gambar halaman cetak 17. Gambar sumber lengkap tidak disertakan sebagai file terpisah dalam audit ini. Istilah dapat dicatat, tetapi hubungan komando dan klasifikasi rinci harus dicocokkan kembali pada diagram asli.

| Register ID | Istilah sumber | Source reference | Candidate classification | Responsibility/meaning available in supplied material | Verification status | Pending item |
|---|---|---|---|---|---|---|
| TS-ORG-001 | Ketua TSKKM | SOP cetak p.17; approval wording juga diringkas pada p.23 | `ORGANIZATIONAL_POSITION_CANDIDATE` | Terlihat sebagai bagian struktur. P.23 menyebut persetujuan Ketua TSKKM untuk pengeluaran dana darurat dalam konteks yang terlihat. | `PARTIALLY_VERIFIED` | Hubungan ke role lain, pemegang jabatan, mandate, cakupan authority, dan mapping akun belum diverifikasi. |
| TS-ORG-002 | Sekretaris | SOP cetak p.17 | `ORGANIZATIONAL_POSITION_CANDIDATE` | Terlihat dalam struktur organisasi. Tanggung jawab rinci belum tersedia pada materi ini. | `PARTIALLY_VERIFIED` | Perlu transkripsi/klasifikasi diagram dan uraian tugas dari sumber lengkap. |
| TS-ORG-003 | Bendahara | SOP cetak p.17 | `ORGANIZATIONAL_POSITION_CANDIDATE` | Terlihat dalam struktur organisasi. Tidak cukup bukti untuk menyimpulkan approval authority Finance. | `PARTIALLY_VERIFIED` | Tanggung jawab dan authority formal pending. |
| TS-ORG-004 | Koordinator TD | SOP cetak p.17 | `NEEDS_CLASSIFICATION` | Terlihat pada struktur. Hubungan dengan “Koordinator” pada p.20 belum dapat disamakan otomatis. | `NEEDS_CLARIFICATION` | Perlu verifikasi apakah jabatan, fungsi, atau peran operasional yang berbeda. |
| TS-ORG-005 | Bidang pengungsi | SOP cetak p.17, menurut ringkasan audit parsial | `UNIT_OR_TEAM_CANDIDATE` | Nama bidang/fungsi ditampilkan dalam struktur. | `NEEDS_CLASSIFICATION` | Perlu pemeriksaan diagram dan uraian tugas. |
| TS-ORG-006 | Bidang kesehatan | SOP cetak p.17, menurut ringkasan audit parsial | `UNIT_OR_TEAM_CANDIDATE` | Nama bidang/fungsi ditampilkan dalam struktur. | `NEEDS_CLASSIFICATION` | Perlu pemeriksaan diagram dan uraian tugas. |
| TS-ORG-007 | Tim dapur | SOP cetak p.17, menurut ringkasan audit parsial | `UNIT_OR_TEAM_CANDIDATE` | Tim/fungsi ditampilkan dalam struktur. | `NEEDS_CLASSIFICATION` | Tidak otomatis satu application role; perlu definisi tugas/scope. |
| TS-ORG-008 | Logistik | SOP cetak p.17–18, menurut ringkasan audit parsial | `UNIT_OR_TEAM_CANDIDATE` | Disebut sebagai bidang/fungsi dan juga sektor pelayanan pada p.18. Makna pada dua konteks harus dibedakan. | `NEEDS_CLASSIFICATION` | Jangan menggabungkan unit organisasi dan sektor program tanpa model/sumber. |
| TS-ORG-009 | Gudang | SOP cetak p.17, menurut ringkasan audit parsial | `UNIT_OR_TEAM_CANDIDATE` | Ditampilkan sebagai bidang/fungsi. | `NEEDS_CLASSIFICATION` | Hubungan dengan Staff Gudang/operasi gudang perlu sumber langsung. |
| TS-ORG-010 | Transportasi | SOP cetak p.17, menurut ringkasan audit parsial | `UNIT_OR_TEAM_CANDIDATE` | Ditampilkan sebagai bidang/fungsi. | `NEEDS_CLASSIFICATION` | Tanggung jawab dan relasi ke fungsi lain pending. |
| TS-ORG-011 | Distribusi | SOP cetak p.17–18, menurut ringkasan audit parsial | `UNIT_OR_TEAM_CANDIDATE` | Ditampilkan sebagai bidang/fungsi; p.18 juga menyebut sektor pelayanan terkait distribusi/logistik. | `NEEDS_CLASSIFICATION` | Verifikasi apakah unit, fungsi, atau sektor pada tiap konteks. |
| TS-ORG-012 | Monitoring dan Evaluasi | SOP cetak p.17 dan p.26, menurut ringkasan audit parsial | `UNIT_OR_TEAM_CANDIDATE` | Ditampilkan sebagai fungsi/bidang; monitoring/evaluasi juga dibahas pada p.26. | `NEEDS_CLASSIFICATION` | Pisahkan struktur unit dari proses monitoring/evaluasi. |
| TS-ORG-013 | Mitigasi | SOP cetak p.17–18, menurut ringkasan audit parsial | `UNIT_OR_TEAM_CANDIDATE` | Ditampilkan dalam struktur/fungsi; p.18 juga memasukkan mitigasi sebagai jenis pelayanan. | `NEEDS_CLASSIFICATION` | Pisahkan unit organisasi dari kategori pelayanan bila keduanya berbeda. |

### 5.1 Interpretation rule for page 17

1. Daftar ini adalah transkripsi awal dari ringkasan materi yang tersedia, bukan verifikasi penuh diagram.
2. Garis komando, hubungan parent/child, dan authority tidak direkonstruksi tanpa diagram asli yang dapat dibaca.
3. “Bidang”, “tim”, dan “fungsi” tidak otomatis menjadi role pengguna.
4. Jumlah atau susunan anggota tidak ditetapkan dari daftar ini.
5. Klasifikasi akhir harus menggunakan Buku TSKKM lengkap dan persetujuan pemilik data/organisasi yang berwenang.

---

## 6. Register B — TSKKM Roles, Printed Page 20

**Evidence boundary:** audit parsial yang disediakan menyatakan bahwa halaman 20 menyebut fungsi Koordinator, Fasilitator, dan Animator. Deskripsi berikut mengikuti substansi yang tersedia dalam Master Context; redaksi tepat harus diverifikasi terhadap halaman asli.

| Register ID | Istilah sumber | Source reference | Candidate classification | Responsibility/meaning available in supplied material | Verification status | Pending item |
|---|---|---|---|---|---|---|
| TS-ROLE-001 | Koordinator | SOP cetak p.20 menurut materi yang tersedia | `TSKKM_OPERATIONAL_ROLE_CANDIDATE` | Mengatur, mengoordinasi, memberi arahan, dan meningkatkan kapasitas tanggap darurat di tingkat Dekenat dan Paroki, menurut teks Master Context yang disuplai. | `PARTIALLY_VERIFIED` | Cocokkan redaksi asli, cakupan, decision rights, dan perbedaan dari Koordinator TD. |
| TS-ROLE-002 | Fasilitator | SOP cetak p.20 menurut materi yang tersedia | `TSKKM_OPERATIONAL_ROLE_CANDIDATE` | Melengkapi kapasitas yang ada di tingkat Dekenat dan Paroki, menurut materi yang disuplai. | `PARTIALLY_VERIFIED` | Verifikasi redaksi, tanggung jawab rinci, dan authority. |
| TS-ROLE-003 | Animator | SOP cetak p.20 menurut materi yang tersedia | `TSKKM_OPERATIONAL_ROLE_CANDIDATE` | Membantu mengelola dan menganimasi komunitas yang peduli beserta kapasitasnya di tingkat Paroki, menurut materi yang disuplai. | `PARTIALLY_VERIFIED` | Verifikasi redaksi, lingkup kerja, dan authority. |

### 6.1 Mapping rule

- Tiga istilah di atas wajib masuk **source-based operational role/function inventory** setelah diverifikasi.
- Tidak otomatis dibuat sebagai application role dengan permission tertentu.
- Tidak disamakan dengan jabatan organisasi atau Koordinator TD tanpa bukti eksplisit.
- Pemetaan ke user, assignment, permission, scope, dan authority harus menjadi relasi/keputusan tersendiri.

---

## 7. Register C — Disaster Scale and Response Participation, Printed Page 16

| Register ID | Istilah sumber | Source reference | Candidate classification | Responsibility/meaning available in supplied material | Verification status | Pending item |
|---|---|---|---|---|---|---|
| TS-RESP-001 | Rendah | SOP cetak p.16 menurut audit parsial | `OPERATIONAL_FUNCTION_CANDIDATE` / response-level label | Tabel level respons memasangkan Rendah dengan Paroki pada materi yang diberikan. | `PARTIALLY_VERIFIED` | Verifikasi tabel asli dan seluruh ambang. |
| TS-RESP-002 | Sedang | SOP cetak p.16 menurut audit parsial | `OPERATIONAL_FUNCTION_CANDIDATE` / response-level label | Tabel level respons memasangkan Sedang dengan Paroki dan TSKKM pada materi yang diberikan. | `PARTIALLY_VERIFIED` | Verifikasi tabel asli, batas kategori, dan aktor keputusan. |
| TS-RESP-003 | Tinggi | SOP cetak p.16 menurut audit parsial | `OPERATIONAL_FUNCTION_CANDIDATE` / response-level label | Tabel level respons memasangkan Tinggi dengan Paroki, TSKKM, dan KARINA-KWI pada materi yang diberikan. | `PARTIALLY_VERIFIED` | Verifikasi tabel asli; keterlibatan tidak otomatis memberi system role/permission. |
| TS-ORG-014 | Paroki | SOP cetak p.16 dan konteks p.22–23 | `ORGANIZATIONAL_UNIT_CANDIDATE` | Berpartisipasi pada level respons yang ditampilkan; p.23 juga menyebut peran Pastor Paroki pada pembentukan tim. | `PARTIALLY_VERIFIED` | Unit, actor, approval, dan responsibility harus dipisahkan. |
| TS-EXT-001 | KARINA KWI | SOP cetak p.16/24 menurut materi yang tersedia | `EXTERNAL_STAKEHOLDER_CANDIDATE` | Disebut dalam konteks dukungan/koordinasi; fungsi per level harus diverifikasi. | `PARTIALLY_VERIFIED` | Tidak menjadi internal role otomatis. |

**Pembatasan:** level respons dan pihak yang terlibat tidak otomatis menetapkan individu, hak akses, approval authority, atau batas pendanaan. Nilai ambang pada tabel p.16 tidak ditranskripsi karena sebagian gambar disebut kurang jelas.

---

## 8. Register D — Rapid Assessment and Response Decision, Printed Pages 21–23

| Register ID | Istilah sumber | Source reference | Candidate classification | Responsibility/meaning available in supplied material | Verification status | Pending item |
|---|---|---|---|---|---|---|
| TS-FUNC-001 | Tim Kajian | SOP cetak p.21–22 menurut audit parsial | `UNIT_OR_TEAM_CANDIDATE` | Melakukan kajian cepat; hasilnya menghasilkan SITREP #1 menurut ringkasan materi. | `PARTIALLY_VERIFIED` | Periksa komposisi, leader, authority, lifecycle, dan record ownership. |
| TS-FUNC-002 | Kajian Cepat TSKKM | SOP cetak p.21–22 menurut audit parsial | `OPERATIONAL_FUNCTION_CANDIDATE` | Menghasilkan SITREP #1 sebelum keputusan Respons/Tidak Respons, menurut audit parsial. | `PARTIALLY_VERIFIED` | Verifikasi trigger, input, form, reviewer, dan status. |
| TS-DG-001 | Validasi hasil kajian / assessment review | Master Context/R05.1 yang disuplai; authority mapping belum diverifikasi dari SOP lengkap | `DECISION_GATE_CANDIDATE` | Master Context menyatakan Koordinator memvalidasi rapid assessment. Ini merupakan statement dalam project document; belum diverifikasi sebagai redaksi SOP/mandat formal. | `PENDING_AUTHORITY_MAPPING` | Temukan sumber kewenangan dan siapa yang dapat memvalidasi. |
| TS-DG-002 | Keputusan Respons/Tidak Respons | SOP cetak p.21–22 dan baseline proyek | `DECISION_GATE_CANDIDATE` | SOP partial audit menyebut keputusan Respons/Tidak Respons; baseline proyek menyebut Romo Direktur berdasarkan mandat/delegasi. | `SOURCE_CONFLICT` | Rekonsiliasi actor/mandate tanpa menyamakan Ketua TSKKM dan Romo Direktur. |
| TS-DG-003 | Pembentukan Tim Tanggap Darurat Paroki | SOP cetak p.22–23 menurut audit parsial | `DECISION_GATE_CANDIDATE` | Materi menyatakan Pastor Paroki mengeluarkan keputusan pembentukan tim setelah keputusan respons; gate ini terpisah. | `PARTIALLY_VERIFIED` | Verifikasi wording, actor, evidence, dan relasi dengan TSKKM decision. |
| TS-FUNC-003 | Monitoring pada jalur Tidak Respons | SOP cetak p.21–22 menurut audit parsial | `OPERATIONAL_FUNCTION_CANDIDATE` | Tim Kajian tetap memantau dan menginformasikan TSKKM; laporan lanjutan/lifecycle belum ditentukan. | `PARTIALLY_VERIFIED` | Format, nomor, owner, dan lifecycle laporan perkembangan pending. |

### 8.1 Response-decision authority note

Materi yang tersedia tidak cukup untuk menyatakan bahwa:

- Ketua TSKKM dan Romo Direktur adalah jabatan/aktor yang sama.
- Keputusan pengeluaran dana dan keputusan Respons/Tidak Respons adalah kewenangan yang sama.
- Role aplikasi otomatis mengikuti jabatan struktural.

Masing-masing authority memerlukan source/mandate mapping yang terpisah.

---

## 9. Register E — Emergency Response Operations, Appendix 2 Pages 34–42

**Evidence limitation:** halaman asli 34–42 tidak tersedia untuk pemeriksaan langsung. Istilah pada bagian ini berasal dari daftar yang disebut dalam rekomendasi/proposal Master Context. Karena sumber halaman belum diverifikasi, semua entri diberi `EVIDENCE_NOT_AVAILABLE` atau `NEEDS_CLARIFICATION` dan tidak menjadi katalog final.

| Register ID | Istilah yang dilaporkan | Claimed source reference | Candidate classification | Responsibility/meaning available in supplied material | Verification status | Required verification |
|---|---|---|---|---|---|---|
| TS-OPS-001 | Direktur | Lampiran 2, diklaim p.34–42 | `NEEDS_CLASSIFICATION` | Disebut sebagai unsur struktur operasi minimum dalam materi proyek. | `EVIDENCE_NOT_AVAILABLE` | Periksa halaman asli; jangan samakan dengan jabatan Caritas tanpa bukti. |
| TS-OPS-002 | LO/Communication Officer | Lampiran 2, diklaim p.34–42 | `OPERATIONAL_ROLE_CANDIDATE` | Istilah/nomenklatur disebut dalam daftar minimum yang disuplai. | `EVIDENCE_NOT_AVAILABLE` | Verifikasi bentuk, tugas, authority, dan scope pada sumber. |
| TS-OPS-003 | Program Manajer/Koordinator Operasi | Lampiran 2, diklaim p.34–42 | `NEEDS_CLASSIFICATION` | Ditampilkan sebagai satu istilah gabungan dalam daftar minimum. | `EVIDENCE_NOT_AVAILABLE` | Jangan memecah menjadi dua role tanpa bukti sumber. |
| TS-OPS-004 | Finance | Lampiran 2, diklaim p.34–42 | `NEEDS_CLASSIFICATION` | Disebut sebagai unsur minimum; tidak diketahui apakah jabatan, fungsi, unit, atau penugasan. | `EVIDENCE_NOT_AVAILABLE` | Verifikasi bentuk dan tugas; jangan menyimpulkan financial approval authority. |
| TS-TEAM-001 | Tim Kajian | Lampiran 2, diklaim p.34–42 | `UNIT_OR_TEAM_CANDIDATE` | Tim kerja disebut dalam daftar operasi. | `EVIDENCE_NOT_AVAILABLE` | Verifikasi komposisi dan hubungan ke Tim Kajian p.21–22. |
| TS-TEAM-002 | Tim Pembelian/Procurement | Lampiran 2, diklaim p.34–42 | `UNIT_OR_TEAM_CANDIDATE` | Tim kerja disebut dalam daftar operasi. | `EVIDENCE_NOT_AVAILABLE` | Verifikasi nomenklatur asli, responsibilities, dan role mapping. |
| TS-TEAM-003 | Tim Pergudangan/Warehouse | Lampiran 2, diklaim p.34–42 | `UNIT_OR_TEAM_CANDIDATE` | Tim kerja disebut dalam daftar operasi. | `EVIDENCE_NOT_AVAILABLE` | Verifikasi istilah dan hubungan dengan Gudang/Staff Gudang. |
| TS-TEAM-004 | Tim Penyaluran bantuan/Distribusi | Lampiran 2, diklaim p.34–42 | `UNIT_OR_TEAM_CANDIDATE` | Tim kerja disebut dalam daftar operasi. | `EVIDENCE_NOT_AVAILABLE` | Verifikasi istilah dan tanggung jawab. |
| TS-TEAM-005 | Tim Pemantauan | Lampiran 2, diklaim p.34–42 | `UNIT_OR_TEAM_CANDIDATE` | Tim kerja disebut dalam daftar operasi. | `EVIDENCE_NOT_AVAILABLE` | Verifikasi relasi dengan Monitoring dan Evaluasi. |

### 9.1 Pending classification

Jangan menormalkan ejaan, memecah istilah gabungan, atau mengubah Bahasa Indonesia/Inggris nomenclature sebelum dokumen sumber diperiksa dan pemetaan disetujui.

---

## 10. Register F — Personnel and Operational Assignment Terms

**Evidence limitation:** daftar ini merupakan istilah yang diklaim muncul pada uraian Lampiran 2/Lampiran 4 dalam materi proyek. Halaman asli tidak tersedia untuk pemeriksaan langsung. Entri bukan Role Catalog final.

| Register ID | Istilah yang dilaporkan | Claimed source reference | Candidate classification | Responsibility/meaning available in supplied material | Verification status | Pending issue |
|---|---|---|---|---|---|---|
| TS-PER-001 | Finance Officer | Lampiran 2/4, halaman belum diverifikasi | `OPERATIONAL_ROLE_CANDIDATE` | Disebut sebagai personnel/function term dalam materi yang disuplai. | `EVIDENCE_NOT_AVAILABLE` | Jangan menyamakan dengan Bendahara atau approver Finance. |
| TS-PER-002 | Koordinator Relawan | Lampiran 2/4, halaman belum diverifikasi | `OPERATIONAL_ROLE_CANDIDATE` | Istilah koordinasi relawan disebut dalam daftar yang disuplai. | `EVIDENCE_NOT_AVAILABLE` | Hubungan ke Koordinator, Koordinator TD, dan Volunteer assignment belum diverifikasi. |
| TS-PER-003 | Koordinator Lapangan | Lampiran 2/4, halaman belum diverifikasi | `OPERATIONAL_ROLE_CANDIDATE` | Istilah koordinasi lapangan disebut dalam daftar yang disuplai. | `EVIDENCE_NOT_AVAILABLE` | Jangan disamakan dengan Koordinator TD atau Koordinator Bagian tanpa sumber. |
| TS-PER-004 | Koordinator Bagian | Lampiran 2/4, halaman belum diverifikasi | `OPERATIONAL_ROLE_CANDIDATE` | Istilah disebut dalam daftar personel/fungsi yang disuplai. | `EVIDENCE_NOT_AVAILABLE` | Bagian dan kewenangannya belum diverifikasi. |
| TS-PER-005 | Penanggungjawab Lapangan | Lampiran 2/4, halaman belum diverifikasi | `OPERATIONAL_ROLE_CANDIDATE` | Istilah disebut dalam daftar personel yang disuplai. | `EVIDENCE_NOT_AVAILABLE` | Tanggung jawab, supervision, dan authority belum diverifikasi. |
| TS-PER-006 | Staff Lapangan | Lampiran 2/4, halaman belum diverifikasi | `OPERATIONAL_ASSIGNMENT_CANDIDATE` | Personnel term disebut dalam daftar yang disuplai. | `EVIDENCE_NOT_AVAILABLE` | Jangan memberi permission dari label ini saja. |
| TS-PER-007 | Staff Gudang | Lampiran 2/4, halaman belum diverifikasi | `OPERATIONAL_ASSIGNMENT_CANDIDATE` | Personnel term disebut dalam daftar yang disuplai. | `EVIDENCE_NOT_AVAILABLE` | Hubungan ke unit Gudang/Tim Pergudangan perlu verifikasi. |
| TS-PER-008 | Admin | Lampiran 2/4, halaman belum diverifikasi | `NEEDS_CLASSIFICATION` | Istilah disebut dalam daftar yang disuplai; tidak diketahui apakah posisi, fungsi, atau personel. | `EVIDENCE_NOT_AVAILABLE` | Jangan samakan dengan role Administrasi Caritas atau system administrator. |
| TS-PER-009 | Relawan Tanggap Darurat | Lampiran 2/4, halaman belum diverifikasi | `OPERATIONAL_ASSIGNMENT_CANDIDATE` | Relawan respons disebut sebagai peserta operasi dalam materi yang disuplai. | `EVIDENCE_NOT_AVAILABLE` | Verifikasi proses recruitment, assignment, status, dan authority. |
| TS-PER-010 | Anggota Tim Tanggap Darurat | Lampiran 2/4, halaman belum diverifikasi | `OPERATIONAL_ASSIGNMENT_CANDIDATE` | Anggota tim disebut sebagai peserta operasi. | `EVIDENCE_NOT_AVAILABLE` | Tidak otomatis menjadi permanent role atau approver. |

### 10.1 Non-equivalence control

Sampai dibuktikan oleh sumber:

- Finance Officer ≠ otomatis Bendahara.
- Koordinator ≠ otomatis Koordinator TD ≠ Koordinator Operasi ≠ Koordinator Lapangan ≠ Koordinator Relawan ≠ Koordinator Bagian.
- Admin ≠ otomatis Administrasi organisasi ≠ SuperAdmin teknis.
- Staff Gudang ≠ otomatis role Gudang.
- Relawan ≠ otomatis user aplikasi.
- Keanggotaan tim ≠ approval authority.

---

## 11. Register G — Finance Approval and Authority References

| Register ID | Authority/source statement | Source reference | Candidate classification | Verification status | Limitation / decision link |
|---|---|---|---|---|---|
| TS-AUTH-001 | Pengeluaran dana darurat memerlukan persetujuan Ketua TSKKM | SOP cetak p.23, sebagaimana diringkas dalam audit parsial; R05.1 FIN-DEC-33 | `FORMAL_AUTHORITY_REFERENCE` | `PARTIALLY_VERIFIED` untuk visible wording | Identitas holder, mandate/delegation, scope, validity, acting authority, account mapping belum tersedia; FIN-DEC-33 tetap `PENDING_ORG_DECISION`. |
| TS-AUTH-002 | Keputusan Respons/Tidak Respons oleh Romo Direktur berdasarkan mandat/delegasi | Baseline proyek/Finance or Core materials yang disuplai; exact formal source belum tersedia | `FORMAL_AUTHORITY_REFERENCE` | `NEEDS_CLARIFICATION` | Jangan menyamakan dengan Ketua TSKKM atau TS-AUTH-001. Perlu mandate/delegation dan source reference. |
| TS-AUTH-003 | Validasi kajian cepat oleh Koordinator | Master Context/requirement yang disuplai; direct SOP authority source belum terverifikasi | `FORMAL_AUTHORITY_REFERENCE` | `NEEDS_CLARIFICATION` | Verifikasi apakah Koordinator adalah role, fungsi, assignment, dan scope yang mana. |
| TS-AUTH-004 | Keputusan pembentukan Tim Tanggap Darurat Paroki oleh Pastor Paroki | SOP cetak p.22–23 menurut audit parsial | `FORMAL_AUTHORITY_REFERENCE` | `PARTIALLY_VERIFIED` untuk tahapan yang dilaporkan | Mandate, dokumen bukti, dan mapping akun belum tersedia. |
| TS-AUTH-005 | Amendment Master Policy oleh SuperAdmin capability dengan closure/SK controls | GOV-01–GOV-09, R05.1 | `PROJECT_OWNER_GOVERNANCE_REQUIREMENT` | `VERIFIED_FROM_SUPPLIED_BASELINE_CONTENT`; file-level integrity belum diverifikasi | Tidak memberi SuperAdmin financial approval authority; account lifecycle pending FIN-DEC-20. |

### 11.1 Authority boundary

Register ini tidak menetapkan bahwa daftar jabatan/role memberikan authority dengan sendirinya. Authority baru dapat dipetakan setelah:

1. Sumber formal ditemukan.
2. Scope tindakan ditetapkan.
3. Masa berlaku dan delegasi diverifikasi.
4. Actor/account mapping disetujui.
5. Segregation-of-duties requirements diputuskan.

---

## 12. Master Context Cross-Section Consistency Register

Bagian 5 role/authority tidak boleh menjadi satu-satunya tempat yang memuat prinsip tersebut. Bagian terkait pada Master Context harus diselaraskan melalui revisi dan change control yang sah.

| Master Context section | Consistency requirement | Proposed insertion/update direction | Evidence/approval status |
|---|---|---|---|
| §5 — Organizational Structure, Roles, User Management and Authority | Memuat seluruh source-based distinctions dan status ekstraksi. | Jadikan register ini referensi pendukung; jangan anggap empat posisi sebagai batas/katalog lengkap. | Draft; buku penuh/approval belum tersedia. |
| §8.2 — Core System as Shared Foundation | Core scope harus mendukung user/personnel growth dan sumber data kanonis. | Tambahkan candidate capabilities: Personnel Registry, Organizational Structure Reference, TSKKM Role/Function Catalog, Assignment Management, Authority/Delegation Reference, Permission Mapping, dan History. Setiap capability masih mengikuti source/approval status. | Rekomendasi desain; belum approved physical/logical schema. |
| §9 — Security and Access Control | Authorization harus membedakan identitas, posisi, role, assignment, scope, permission, authority, dan workflow state. | Nyatakan bahwa create-user tidak otomatis membuat assignment/permission/authority; approval memerlukan authority evidence yang relevan. | Prinsip sudah dinyatakan sebagian; mapping formal pending. |
| §12 — Development Strategy and Module Control | User/role management bergantung pada source-based role/function inventory. | Tambahkan dependency bahwa final Role Catalog/Permission Matrix menunggu ekstraksi dan verifikasi Buku TSKKM; pekerjaan dokumentasi Core dapat lanjut sebagai draft bila status pending jelas. | Dependency rekomendasi; owner acceptance pending. |
| §19 — Open Issues and Pending Decisions | Mencakup ekstraksi penuh Buku TSKKM dan verifikasi nomenklatur/authority. | Tambahkan issue: “Extract and verify all positions, roles, units, functions, responsibilities, decision gates, and authority references from the complete Book TSKKM; reconcile duplicates/ambiguities without normalizing source terminology prematurely.” | `PENDING_ORG_DECISION` / `EVIDENCE_NOT_AVAILABLE` sesuai butir. |
| Finance / FIN-DEC-33 references | Kewenangan Ketua TSKKM untuk persetujuan dana darurat dipisahkan dari User Management role assignment. | Pertahankan teks SOP p.23 sebagai evidence parsial; mapping authority tetap FIN-DEC-33 pending. User creation, role assignment, or permission must not expand the authority. | SOP wording partial; mandate/account mapping unavailable. |

### 12.1 Document change control

Tabel ini adalah audit/recommendation register, bukan perubahan terhadap Master Context R01. Tidak ada source file yang diubah. Setiap perubahan ke Master Context harus memiliki revisi baru dan persetujuan sesuai tata kelola dokumen proyek.

---

## 13. Role and Authority Extraction Workflow — Pending Work

Langkah berikut diperlukan sebelum Role Catalog/Permission Matrix dinyatakan final:

1. Sediakan salinan lengkap Buku TSKKM yang dapat dibaca, termasuk lampiran dan halaman yang dirujuk.
2. Catat metadata sumber: judul, penerbit, tanggal/revisi, cakupan, status berlaku.
3. Ekstrak istilah secara verbatim ke register dengan halaman dan bagian.
4. Pisahkan kategori: position, role, function, unit/team, stakeholder, assignment, decision gate, authority.
5. Catat responsibility dan authority hanya jika teks sumber menyatakannya.
6. Tandai istilah ambigu sebagai `NEEDS_CLASSIFICATION` atau `NEEDS_CLARIFICATION`.
7. Bandingkan istilah yang sama lintas halaman tanpa otomatis menggabungkannya.
8. Buat mapping ke system permission hanya setelah authority basis dan scope terverifikasi.
9. Review hasil ekstraksi oleh pemilik proses/organisasi yang berwenang.
10. Simpan perubahan, reviewer, tanggal, dan source version dalam document control.

**Tidak ada langkah di atas yang telah dinyatakan selesai oleh audit ini.**

---

## 14. Acceptance Criteria for This Register

Register ini dapat diajukan sebagai **source extraction baseline candidate** setelah:

- [ ] Buku TSKKM lengkap tersedia dan metadata sumber dicatat.
- [ ] Semua istilah role/position/function/unit/team/personnel/authority yang relevan diekstrak dengan page/section reference.
- [ ] Istilah asli dipertahankan tanpa normalisasi yang mengubah makna.
- [ ] Setiap entri memiliki classification atau status `NEEDS_CLASSIFICATION`.
- [ ] Tanggung jawab yang tidak disebut sumber tidak diisi dengan tebakan.
- [ ] Ambiguitas nama (contoh: Koordinator vs Koordinator TD vs Koordinator Lapangan) dicatat sebagai pending.
- [ ] FIN-DEC-33 tetap konsisten dengan SOP p.23 dan R05.1; authority mapping tidak ditutup tanpa bukti.
- [ ] Posisi, role, fungsi, assignment, permission, dan authority tidak digabung.
- [ ] Master Context §8.2, §9, §12, dan §19 memiliki perubahan usulan yang terlacak; sumbernya tidak diubah tanpa change control.
- [ ] Pemilik/authority yang berwenang meninjau dan menyetujui hasil ekstraksi sebelum konfigurasi.

Kriteria yang bergantung pada dokumen yang belum tersedia berstatus `NOT VERIFIABLE` atau `BLOCKED_BY_MISSING_EVIDENCE`, bukan lulus.

---

## 15. Readiness Assessment

| Area | Status | Basis |
|---|---|---|
| Draft Source Register structure | `CONDITIONAL` | Istilah yang diberikan dapat diinventarisasi; sumber lampiran tertentu belum tersedia. |
| Complete Buku TSKKM role extraction | `BLOCKED_BY_MISSING_SOURCE` | Buku lengkap tidak tersedia untuk verifikasi langsung. |
| Organizational position catalogue | `PARTIAL` | Beberapa istilah dari diagram p.17 tersedia melalui audit parsial; classification/relationships belum diverifikasi. |
| TSKKM operational role catalogue | `PARTIAL` | Tiga role p.20 disebut dalam materi; wording dan authority perlu dicocokkan ke gambar asli. |
| Emergency operations structure p.34–42 | `BLOCKED_BY_MISSING_SOURCE` | Halaman asli tidak tersedia. |
| Finance approval authority mapping | `BLOCKED` | SOP p.23 visible wording parsial; formal mandate/delegation/account mapping unavailable; FIN-DEC-33 pending. |
| User Management design | `CONDITIONAL` for conceptual discussion only | Principle separation exists; final model and permission assignment remain pending. |
| Permission Matrix | `BLOCKED` | Source-based role/authority extraction and organizational approval incomplete. |
| Master Context alignment | `CONDITIONAL` | Required cross-section changes are identified but not applied to source. |
| Document Register approval | `BLOCKED` for final role/authority baseline | Source completeness and owner review are still required. |
| Physical Database Design | `NO_GO` | No approved role/authority/data model baseline. |
| Implementation | `NO_GO` | Not authorized by this audit. |

---

## 16. Open Questions and Evidence Required

| ID | Question/evidence request | Affected entries | Status |
|---|---|---|---|
| EV-01 | Full Buku TSKKM with pages 1–95 and all appendices | All role/authority entries | `EVIDENCE_NOT_AVAILABLE` |
| EV-02 | Clear image/source for p.17 organizational structure and reporting lines | TS-ORG-001–014 | `EVIDENCE_NOT_AVAILABLE` for direct reinspection |
| EV-03 | Clear image/source for p.20 role descriptions | TS-ROLE-001–003 | `PARTIALLY_VERIFIED`; exact wording pending |
| EV-04 | Original Lampiran 2 p.34–42 | TS-OPS-001–005 | `EVIDENCE_NOT_AVAILABLE` |
| EV-05 | Original Lampiran 4 pages relevant to personnel/function list | TS-PER-001–010 | `EVIDENCE_NOT_AVAILABLE` |
| EV-06 | SK/mandate/delegation and approval matrix for emergency fund | TS-AUTH-001 and FIN-DEC-33 | `EVIDENCE_NOT_AVAILABLE` |
| EV-07 | Formal authority for Respons/Tidak Respons and rapid assessment validation | TS-AUTH-002/003 | `EVIDENCE_NOT_AVAILABLE` |
| EV-08 | Formal authority for Paroki team establishment and assignment | TS-AUTH-004 | `EVIDENCE_NOT_AVAILABLE` |
| EV-09 | Approved permission, scope, and segregation-of-duties matrix | Master Context §§5, 9, 12 | `EVIDENCE_NOT_AVAILABLE` |
| EV-10 | Project-owner approval for four permanent system roles and their current status | Master Context baseline | `PENDING_OWNER_CONFIRMATION` if no formal approval record supplied |

---

## 17. Final Audit Decision

# `NOT READY — CORRECTION REQUIRED BEFORE DOCUMENT REGISTER BASELINE`

Four proposed permanent principles are appropriate to preserve as **candidate governance requirements for owner review**:

1. The four initially known personnel/positions are not a system user limit.
2. The complete Buku TSKKM is the primary source for operational roles and responsibilities.
3. Caritas’s organizational structure must be able to grow without requiring an architectural rebuild for ordinary personnel/unit changes.
4. Creating a user does not automatically grant role, assignment, permission, scope, or authority.

The audit cannot certify that the complete list of roles, duties, and authorities has been extracted because the full Buku TSKKM and formal authority evidence are unavailable. The register must remain a draft source inventory until that evidence is obtained and the authorized owner reviews it.

No change to the Master Context source was made. No Document Register, final Role Catalog, Permission Matrix, physical database design, or implementation was approved or created by this report.

---

## 18. Final Validation

| Check | Result |
|---|---|
| Four initial positions not treated as maximum user count | Preserved as a draft principle |
| Buku TSKKM treated as primary role source | Stated in draft; full source not verified |
| Organizational growth distinguished from authority change | Identified; change boundary needs approval |
| User creation separated from role/permission/authority grant | Stated; explicit test recommended |
| Full role/authority extraction completed | No — `EVIDENCE_NOT_AVAILABLE` |
| FIN-DEC-33 authority changed | No; remains pending formal mapping |
| GOV/FIN-DEC/FIN-TEST baselines changed | No |
| Source document modified | No |
| Code/database/implementation performed | No |
| Physical Database Design authorized | No |

**Report status:** Independent Audit Report — Working Document.  
**Master Context R01 status:** Draft under review; correction and owner review required before Document Register baseline approval.  
**Finance Logical Architecture Final:** `BLOCKED`.  
**Physical Database Design:** `NO_GO`.  
**Implementation:** `NO_GO`.

**End of TSKKM Role & Authority Source Register R01 Audit.**