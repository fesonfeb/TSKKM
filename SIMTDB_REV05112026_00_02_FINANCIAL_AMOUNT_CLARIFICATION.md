# SIM-TDB — ADDENDUM KLARIFIKASI FLEKSIBILITAS NOMINAL KEUANGAN

**Document ID:** SIMTDB-REV05112026-ADD-FA  
**Revision:** REV05112026  
**Status:** Klarifikasi pemilik proyek — untuk harmonisasi dokumen  
**Mode:** Pembaruan spesifikasi saja — tanpa implementasi  
**Klasifikasi keputusan:** `CLARIFIED_BY_PROJECT_OWNER`  
**Ruang lingkup:** Makna nominal Rp50.000.000 dan Rp100.000.000 yang muncul dalam contoh atau ilustrasi keuangan SOP

---

## 1. Tujuan

Addendum ini mencatat klarifikasi pemilik proyek bahwa nominal Rp50.000.000 dan Rp100.000.000 yang muncul dalam contoh atau ilustrasi keuangan pada dokumen SOP adalah **contoh nilai keuangan**, bukan nominal baku atau batas otomatis.

Klarifikasi ini hanya berlaku untuk interpretasi nominal tersebut. Addendum ini **tidak mengubah ketentuan SOP lainnya** dan tidak menetapkan kewenangan persetujuan baru.

---

## 2. Klarifikasi pemilik proyek

Nominal Rp50.000.000 dan Rp100.000.000:

- Bukan nominal baku.
- Bukan plafon tetap.
- Bukan batas maksimal pengeluaran.
- Bukan standar alokasi anggaran.
- Hanya merupakan contoh nilai keuangan.

Besaran anggaran dapat disesuaikan dengan kebutuhan program, kegiatan, kondisi bencana, sumber pendanaan, serta anggaran yang disetujui.

**Status:** `CLARIFIED_BY_PROJECT_OWNER`

---

## 3. Aturan teknis yang harus dipertahankan

1. Jangan melakukan hardcoding terhadap nominal Rp50.000.000 atau Rp100.000.000.
2. Jangan menjadikan nominal tersebut sebagai nilai default wajib.
3. Jangan menggunakan nominal tersebut sebagai batas otomatis persetujuan transaksi.
4. Pengelolaan anggaran harus fleksibel berdasarkan program dan kegiatan.
5. Pisahkan secara jelas:
   - Proposed budget.
   - Approved budget.
   - Budget revision.
   - Actual expenditure.
   - Remaining budget.
6. Setiap perubahan anggaran harus memiliki riwayat, alasan, aktor, waktu, dan referensi persetujuan.
7. Setiap sumber pendanaan harus dapat ditelusuri.
8. Otorisasi dan pejabat pemberi persetujuan tetap mengikuti kewenangan organisasi yang telah diverifikasi.
9. Fleksibilitas nominal tidak berarti kewenangan persetujuan dapat berubah secara bebas.
10. Nominal transaksi dan laporan harus bersumber dari data keuangan aktual yang tercatat dan disahkan.

---

## 4. Dampak terhadap audit dan spesifikasi sebelumnya

### 4.1 Pembaruan temuan audit pendanaan

Kesimpulan audit sebelumnya mengenai nominal pada halaman 23 dan halaman 49 harus diperbarui:

> Klarifikasi pemilik proyek menetapkan bahwa nominal Rp50.000.000 dan Rp100.000.000 yang muncul dalam contoh atau ilustrasi merupakan nilai contoh, bukan nominal baku, plafon, batas pengeluaran, atau standar alokasi. Klarifikasi ini tidak mengubah kewenangan persetujuan maupun ketentuan SOP lainnya.

Dengan klarifikasi tersebut, pertanyaan mengenai **makna kedua nominal sebagai nilai contoh** dianggap terjawab.

Hal-hal berikut **tidak** otomatis dianggap terjawab:

- Siapa pejabat yang berwenang menyetujui setiap jenis anggaran atau transaksi.
- Hubungan dan batas penggunaan masing-masing sumber pendanaan.
- Kebijakan akuntansi dan pengakuan actual expenditure.
- Aturan perhitungan remaining budget.
- Field, struktur, atau approval pada template keuangan yang belum diperiksa.
- Isu pendanaan lain yang tercatat dalam CHR-020.

### 4.2 Batas penerapan

Addendum ini:

- Tidak mengubah alur atau otoritas dalam SOP.
- Tidak mencabut ketentuan persetujuan dana yang tercantum dalam sumber SOP.
- Tidak menetapkan pejabat persetujuan baru.
- Tidak membuat batas nominal baru.
- Tidak menentukan aturan pengakuan akuntansi.
- Tidak mengubah nilai transaksi yang telah tercatat.
- Tidak mengesahkan perubahan anggaran tertentu.

---

## 5. Financial Business Rule Register — pembaruan

| Rule ID | Aturan | Sumber/status | Pengujian yang diperlukan |
|---|---|---|---|
| FIN-BR-001 | Rp50.000.000 dan Rp100.000.000 yang muncul sebagai contoh atau ilustrasi bukan nominal baku, plafon tetap, batas maksimal pengeluaran, atau standar alokasi. | `CLARIFIED_BY_PROJECT_OWNER` | Pastikan tidak ada hardcode, default wajib, atau batas approval otomatis yang menggunakan kedua nominal tersebut. |
| FIN-BR-002 | Anggaran dapat ditentukan berdasarkan kebutuhan program/kegiatan, kondisi bencana, sumber pendanaan, dan anggaran yang disetujui. | `CLARIFIED_BY_PROJECT_OWNER` | Uji penyimpanan dan penelusuran anggaran dengan nilai yang berbeda tanpa aturan nominal contoh. |
| FIN-BR-003 | Proposed budget, approved budget, budget revision, actual expenditure, dan remaining budget harus dibedakan. | `CLARIFIED_BY_PROJECT_OWNER` | Uji bahwa setiap kategori memiliki status, sumber, relasi, dan riwayat yang dapat dibedakan. |
| FIN-BR-004 | Perubahan anggaran harus menyimpan riwayat, alasan, aktor, waktu, serta referensi persetujuan. | `CLARIFIED_BY_PROJECT_OWNER` | Uji bahwa revisi tidak menghapus nilai sebelumnya dan menyimpan metadata perubahan. |
| FIN-BR-005 | Sumber pendanaan untuk anggaran/transaksi harus dapat ditelusuri. | `CLARIFIED_BY_PROJECT_OWNER` | Uji lineage dari anggaran dan transaksi ke sumber pendanaan. |
| FIN-BR-006 | Kewenangan persetujuan tetap mengikuti kewenangan organisasi yang telah diverifikasi. | `CLARIFIED_BY_PROJECT_OWNER`; detail kewenangan lain tetap perlu sumber yang disahkan | Uji bahwa nominal fleksibel tidak memberikan atau mengubah otoritas persetujuan. |
| FIN-BR-007 | Nominal pada transaksi dan laporan bersumber dari data keuangan aktual yang tercatat dan disahkan. | `CLARIFIED_BY_PROJECT_OWNER` | Uji provenance angka laporan hingga catatan keuangan sumber yang disahkan. |
| FIN-BR-008 | Dasar penghitungan remaining budget dan perlakuan komitmen belum ditetapkan oleh addendum ini. | `PENDING_ORG_DECISION` atau menunggu pedoman keuangan yang disahkan | Jangan menerapkan formula final tanpa kebijakan akuntansi/keuangan yang disetujui. |

### Catatan perhitungan remaining budget

Addendum mengharuskan `remaining budget` dibedakan, tetapi tidak menetapkan formula atau basis akuntansinya. Karena itu:

- Jangan menetapkan formula final melalui asumsi teknis.
- Jangan menentukan sendiri apakah perhitungan mengurangi approved budget dengan actual expenditure saja atau juga memperhitungkan komitmen.
- Rumus, basis periode, perlakuan pembatalan/reversal, dan kebijakan pembulatan tetap mengikuti pedoman keuangan yang disahkan.
- Jika angka remaining budget disajikan sebelum dasar tersebut disahkan, tampilkan sebagai proposal teknis dengan label/status yang jelas.

---

## 6. Source of Truth Matrix — pembaruan keuangan

| Data | Sumber otoritatif | Aturan lineage | Status |
|---|---|---|---|
| Proposed budget | Catatan proposal anggaran program/kegiatan | Simpan pembuat, waktu, versi, dan hubungan ke program/kegiatan serta sumber pendanaan yang diusulkan. | `CLARIFIED_BY_PROJECT_OWNER` untuk pemisahan status; model rinci teknis |
| Approved budget | Catatan anggaran yang disetujui beserta bukti persetujuannya | Nilai harus dapat ditelusuri ke keputusan/dokumen persetujuan yang sah. | Otoritas dan bentuk bukti tetap mengikuti keputusan organisasi yang diverifikasi |
| Budget revision | Riwayat revisi anggaran dan referensi persetujuan | Jangan menimpa nilai sebelumnya; catat nilai sebelum/sesudah, alasan, aktor, waktu, dan bukti persetujuan. | `CLARIFIED_BY_PROJECT_OWNER` |
| Actual expenditure | Catatan keuangan aktual yang tercatat dan disahkan | Laporan mengambil nominal dari catatan keuangan sumber, bukan pengetikan ulang tanpa provenance. | `CLARIFIED_BY_PROJECT_OWNER`; aturan pengakuan akuntansi tetap mengikuti pedoman yang disahkan |
| Remaining budget | Nilai turunan dari data anggaran dan data keuangan sesuai kebijakan yang disahkan | Tampilkan basis perhitungan dan sumber yang digunakan; jangan jadikan kolom bebas yang dapat menyimpang dari transaksi. | Formula dan perlakuan komitmen belum ditetapkan |
| Funding source | Register/catatan sumber pendanaan yang disahkan | Setiap anggaran/transaksi harus merujuk ke sumber pendanaan yang dapat diidentifikasi. | Kategori dan tata kelola mengikuti sumber resmi |
| Nominal Rp50.000.000/Rp100.000.000 dalam contoh | Dokumen contoh/ilustrasi ditambah klarifikasi pemilik proyek | Nominal ini tidak menjadi default atau threshold otomatis. | `CLARIFIED_BY_PROJECT_OWNER` |

**Prinsip laporan:** dashboard dan laporan adalah tampilan turunan. Nominal transaksi dan laporan harus berasal dari catatan keuangan aktual yang tercatat dan disahkan.

---

## 7. CHR Mapping — pembaruan

| Register | Isu | Pembaruan status |
|---|---|---|
| CHR-020 | Sumber dana dan perbedaan Rp50 juta dengan Rp100 juta | **Sebagian diselesaikan.** Makna kedua nominal sebagai contoh telah diklarifikasi oleh pemilik proyek. Isu lain dalam CHR-020—otoritas, tata kelola sumber dana, pembatasan, dan prosedur—tetap terbuka jika belum didukung keputusan atau dokumen yang diverifikasi. |
| PDR-10 | Nilai Rp100 juta pada template APP-KWI | **Diselesaikan untuk makna nominal.** Nilai contoh bukan nominal baku, plafon, atau batas transaksi berdasarkan klarifikasi pemilik proyek. Pemeriksaan field/template halaman 49 dan isu lain yang tidak dicakup klarifikasi tetap mengikuti hasil audit sumber. |

### Catatan status

- Jangan menandai seluruh CHR-020 sebagai selesai hanya karena interpretasi nilai contoh sudah diklarifikasi.
- Jangan menyimpulkan bahwa pejabat persetujuan, plafon, atau sumber dana telah berubah.
- Simpan status keputusan dengan referensi ke addendum ini dan tanggal/revisi yang tercantum.

---

## 8. Core Entity Registry — pembaruan

Entitas berikut adalah kebutuhan konseptual untuk mendukung klarifikasi. Ini **bukan** persetujuan nama tabel fisik.

| Entitas konseptual | Tujuan dan data utama | Relasi/provenance | Status |
|---|---|---|---|
| Budget proposal | Mencatat proposed budget menurut program/kegiatan dan sumber pendanaan yang diusulkan. | Program/kegiatan; funding source; pembuat; versi. | Diperlukan untuk pemisahan status anggaran; desain fisik belum diputuskan. |
| Approved budget record | Mencatat anggaran yang disetujui dan status persetujuannya. | Budget proposal/revision; bukti persetujuan; authority record. | Otoritas dan proses persetujuan harus mengikuti aturan organisasi yang diverifikasi. |
| Budget revision record | Menyimpan perubahan sebagai riwayat, termasuk alasan, aktor, waktu, nilai, dan referensi persetujuan. | Approved budget/program/activity; document/approval reference. | Append-only/versioned sebagai usulan teknis yang mendukung klarifikasi. |
| Actual expenditure reference | Menghubungkan nilai laporan ke catatan transaksi keuangan aktual yang tercatat dan disahkan. | Finance transactions, financial documents, funding source. | Aturan pengakuan tetap mengikuti pedoman keuangan yang disahkan. |
| Remaining budget view/record | Menyajikan saldo anggaran berdasarkan basis perhitungan yang disetujui. | Approved budget/revisions dan data actual expenditure; komitmen bila kebijakan menetapkan. | Formula dan perlakuan komitmen belum disahkan. |
| Funding source reference | Menautkan proposal, anggaran, revisi, dan transaksi kepada sumber dana. | Funding source register dan bukti sumber. | Owner dan katalog final mengikuti keputusan organisasi. |
| Budget approval reference | Merujuk keputusan, dokumen, atau delegation yang memberi dasar persetujuan. | Approval authority/delegation record dan document registry. | Jangan membuat otoritas baru; hanya simpan otoritas yang terverifikasi. |

### Integritas dan lifecycle

- Perubahan budget tidak menghapus riwayat sebelumnya.
- Approved budget tidak boleh disamakan dengan proposed budget.
- Budget revision harus memiliki referensi approval yang sesuai.
- Transaksi aktual tidak boleh diganti dengan angka pada proposal atau ilustrasi.
- Remaining budget merupakan nilai yang diturunkan sesuai kebijakan yang disahkan; belum boleh diasumsikan sebagai angka yang diedit langsung.
- Nominal contoh Rp50.000.000 dan Rp100.000.000 tidak ditanam sebagai nilai sistem wajib.

---

## 9. Finance Data Dictionary — tambahan field konseptual

Daftar berikut menambah kebutuhan field-level pada domain Finance. Tipe data masih logis dan tidak menetapkan DBMS.

| Entitas konseptual | Field | Makna | Kewajiban/kondisi | Validasi dan relasi | Sumber/status |
|---|---|---|---|---|---|
| Budget proposal | `proposal_id` | Identitas proposal anggaran | Wajib untuk setiap proposal | ID stabil; unik | `TECHNICAL_RECOMMENDATION` |
| Budget proposal | `program_id` / `activity_id` | Program atau kegiatan yang menjadi dasar anggaran | Wajib sesuai tingkat penganggaran yang disetujui | FK ke entitas program/kegiatan | Perlu kontrak lintas modul |
| Budget proposal | `funding_source_id` | Sumber pendanaan yang direncanakan | Wajib bila sumber sudah diketahui; status belum ditentukan bila belum | FK ke funding source yang terdaftar | `CLARIFIED_BY_PROJECT_OWNER` |
| Budget proposal | `proposed_amount` | Nominal anggaran yang diusulkan | Wajib sesuai aturan proposal yang disahkan | Nilai numerik; mata uang mengikuti konfigurasi yang disetujui; tidak menggunakan nominal contoh sebagai default | `CLARIFIED_BY_PROJECT_OWNER` |
| Budget proposal | `currency_code` | Mata uang proposal | Wajib sesuai kebijakan sistem/organisasi | Referensi ke katalog mata uang yang disetujui | Konfigurasi perlu dikonfirmasi |
| Budget proposal | `proposal_status` | Status proposal | Wajib | Nilai/status harus dibakukan setelah proses disetujui | `PENDING_ORG_DECISION` untuk workflow final |
| Budget proposal | `created_by`, `created_at` | Pembuat dan waktu pembuatan | Wajib | User dan timestamp sistem | `TECHNICAL_RECOMMENDATION` |
| Approved budget | `approved_budget_id` | Identitas catatan anggaran disetujui | Wajib | ID stabil; unik | `TECHNICAL_RECOMMENDATION` |
| Approved budget | `approved_amount` | Nilai anggaran yang disetujui | Wajib bila status telah disetujui | Tidak boleh otomatis diisi dari contoh nominal | `CLARIFIED_BY_PROJECT_OWNER` |
| Approved budget | `approval_reference_id` | Referensi bukti/record persetujuan | Wajib untuk status approved | Harus menunjuk approval/document yang sah | Otoritas perlu diverifikasi |
| Approved budget | `approved_by` | Aktor persetujuan | Wajib ketika persetujuan dicatat | Harus memiliki authority yang berlaku | Jangan mengarang pejabat |
| Approved budget | `approved_at` | Waktu persetujuan | Wajib ketika persetujuan dicatat | Timestamp yang dapat diaudit | `TECHNICAL_RECOMMENDATION` |
| Budget revision | `revision_id` | Identitas revisi anggaran | Wajib untuk setiap revisi | ID stabil; unik | `TECHNICAL_RECOMMENDATION` |
| Budget revision | `previous_amount` | Nilai sebelum revisi | Wajib bila ada nilai sebelumnya | Berasal dari versi anggaran terdahulu | `CLARIFIED_BY_PROJECT_OWNER` |
| Budget revision | `revised_amount` | Nilai yang diajukan/disetujui setelah revisi | Wajib sesuai status revisi | Tidak menggunakan threshold contoh otomatis | `CLARIFIED_BY_PROJECT_OWNER` |
| Budget revision | `revision_reason` | Alasan revisi | Wajib | Tidak kosong untuk revisi yang diajukan | `CLARIFIED_BY_PROJECT_OWNER` |
| Budget revision | `actor_user_id` | Aktor yang membuat/mengajukan revisi | Wajib | FK ke user | `CLARIFIED_BY_PROJECT_OWNER` |
| Budget revision | `revision_timestamp` | Waktu revisi dicatat | Wajib | Timestamp sistem | `CLARIFIED_BY_PROJECT_OWNER` |
| Budget revision | `approval_reference_id` | Bukti/referensi persetujuan revisi | Wajib untuk revisi yang berstatus disetujui | FK/referensi ke approval/document | Kewenangan harus diverifikasi |
| Actual expenditure reference | `financial_transaction_id` | Referensi transaksi aktual | Wajib untuk angka aktual yang dilaporkan | Harus mengarah ke transaksi finance yang tercatat dan disahkan | `CLARIFIED_BY_PROJECT_OWNER` |
| Actual expenditure reference | `actual_amount` | Nominal aktual dari catatan keuangan | Wajib sesuai transaksi sumber | Tidak boleh diketik sebagai pengganti transaksi sumber | `CLARIFIED_BY_PROJECT_OWNER` |
| Actual expenditure reference | `funding_source_id` | Sumber pendanaan aktual | Wajib jika tercatat pada transaksi | Harus dapat ditelusuri ke sumber dana | `CLARIFIED_BY_PROJECT_OWNER` |
| Remaining budget | `remaining_amount` | Nilai sisa anggaran yang disajikan | Wajib hanya bila basis perhitungannya ditetapkan | Formula, komitmen, dan pembulatan belum boleh dikunci | `PENDING_ORG_DECISION` |
| Budget records | `record_version` | Versi catatan anggaran | Wajib untuk riwayat perubahan | Naik per revisi; tidak menimpa versi terdahulu | `TECHNICAL_RECOMMENDATION` |
| Budget records | `source_document_id` | Dokumen proposal, persetujuan, revisi, atau bukti terkait | Wajib bila diperlukan untuk traceability | FK/referensi ke document registry | `CLARIFIED_BY_PROJECT_OWNER` |

**Catatan:** tipe fisik, nullability final, unique constraints, pengakuan akuntansi, perlakuan pajak, dan formula saldo harus ditetapkan pada fase yang berwenang setelah pedoman keuangan dan database target tersedia.

---

## 10. Approval Workflow Requirements — pembaruan

### 10.1 Persyaratan

1. Sistem membedakan pencatatan proposal anggaran, anggaran disetujui, revisi, dan pengeluaran aktual.
2. Setiap revisi menyimpan alasan, aktor, waktu, dan referensi persetujuan.
3. Approval hanya dapat dicatat oleh pihak dengan kewenangan yang telah diverifikasi.
4. Fleksibilitas nilai anggaran tidak memberikan atau mengubah kewenangan persetujuan.
5. Nominal Rp50.000.000 dan Rp100.000.000 tidak digunakan sebagai trigger atau threshold otomatis.
6. Pengeluaran dana siaga yang pada sumber SOP terlihat memerlukan persetujuan Ketua TSKKM harus tetap diperlakukan sesuai sumber tersebut; identitas/relasi pejabat perlu verifikasi organisasi.
7. Approval record harus terpisah dari permission teknis untuk mengedit atau mengirim data.
8. Setiap approval dan perubahan terkait harus meninggalkan audit trail.
9. Laporan aktual harus mengambil nilai dari transaksi finansial yang tercatat dan disahkan.
10. Approval workflow tidak boleh menetapkan batas nominal baru tanpa keputusan organisasi.

### 10.2 Pembagian status

| Tahap | Makna | Otoritas |
|---|---|---|
| Proposed | Anggaran diajukan | Pembuat/pengusul sesuai proses yang disahkan |
| Approved | Anggaran disetujui | Hanya pejabat dengan kewenangan terverifikasi |
| Revised | Anggaran diubah melalui catatan revisi | Persetujuan mengikuti kewenangan yang berlaku |
| Actual expenditure | Pengeluaran aktual tercatat dan disahkan sesuai pedoman Finance | Mengikuti kebijakan dan kewenangan Finance yang disahkan |
| Remaining budget | Nilai turunan dari dasar anggaran dan transaksi sesuai aturan yang disetujui | Bukan keputusan/approval baru |

Status workflow rinci, pemisahan tugas, dan pejabat persetujuan untuk tiap jenis anggaran selain otoritas yang telah didukung sumber harus tetap pending.

---

## 11. Acceptance tests untuk klarifikasi nominal

Tes berikut adalah rancangan. Tes belum dijalankan pada aplikasi.

| Test ID | Skenario | Hasil yang diharapkan |
|---|---|---|
| FIN-AMT-01 | Membuat proposal dengan nominal selain Rp50 juta dan Rp100 juta | Dapat dicatat jika memenuhi validasi keuangan yang disahkan. |
| FIN-AMT-02 | Memeriksa konfigurasi dan validasi transaksi | Tidak terdapat hardcoded rule yang menjadikan Rp50 juta atau Rp100 juta sebagai mandatory default, cap, atau approval threshold. |
| FIN-AMT-03 | Proposal dibandingkan dengan anggaran yang disetujui | Nilai proposal dan approved budget tetap terpisah dan dapat ditelusuri. |
| FIN-AMT-04 | Membuat revisi anggaran | Riwayat, alasan, aktor, waktu, nilai sebelum/sesudah, dan referensi persetujuan tercatat. |
| FIN-AMT-05 | Revisi dibuat tanpa bukti approval sementara status diminta “approved” | Sistem menolak status approved jika persyaratan otorisasi belum dipenuhi. Detail aturan akhir mengikuti keputusan organisasi. |
| FIN-AMT-06 | Angka aktual ditampilkan pada laporan | Angka berasal dari transaksi aktual yang tercatat dan disahkan, bukan dari proposal atau nominal ilustrasi. |
| FIN-AMT-07 | Anggaran memiliki sumber pendanaan | Laporan dapat menelusuri budget dan transaksi ke sumber pendanaannya. |
| FIN-AMT-08 | Nilai anggaran fleksibel diubah | Perubahan nominal tidak mengubah approver atau authority secara otomatis. |
| FIN-AMT-09 | Menampilkan remaining budget | Basis perhitungan dapat ditelusuri dan formula tidak dianggap final sebelum disahkan. |
| FIN-AMT-10 | Mencari nominal Rp50 juta/Rp100 juta dalam konfigurasi aplikasi | Tidak ditemukan sebagai default wajib, hardcoded cap, atau threshold approval. |

---

## 12. Batas perubahan terhadap SOP dan spesifikasi lain

Klarifikasi ini **hanya** mengubah interpretasi nominal contoh Rp50.000.000 dan Rp100.000.000 serta kebutuhan model anggaran yang fleksibel.

Klarifikasi ini **tidak**:

- Mengubah proses procurement atau finance lainnya.
- Mengubah sumber pendanaan yang tercantum pada SOP.
- Menghapus pembatasan penggunaan dana APP Nasional.
- Mengubah persetujuan Ketua TSKKM yang disebut pada halaman SOP.
- Menetapkan approval authority untuk pejabat atau fungsi baru.
- Mengubah keputusan Respons/Tidak Respons.
- Menetapkan nominal batas baru.
- Mengubah kebijakan akuntansi.
- Menetapkan formula remaining budget.
- Menyelesaikan seluruh CHR-020.

---

## 13. Ringkasan status

| Area | Status |
|---|---|
| Makna Rp50 juta dan Rp100 juta sebagai contoh | **Diklarifikasi oleh pemilik proyek** |
| Hardcoding/default/threshold berdasarkan kedua nominal | **Dilarang** |
| Fleksibilitas anggaran menurut program/kegiatan | **Diklarifikasi oleh pemilik proyek** |
| Pemisahan proposed/approved/revision/actual/remaining | **Diklarifikasi sebagai kebutuhan spesifikasi** |
| Riwayat perubahan anggaran | **Diklarifikasi sebagai kebutuhan spesifikasi** |
| Traceability sumber pendanaan | **Diklarifikasi sebagai kebutuhan spesifikasi** |
| Approval authority | **Tidak berubah; tetap mengikuti kewenangan terverifikasi** |
| Formula remaining budget dan perlakuan komitmen | **Belum ditetapkan** |
| Seluruh CHR-020 | **Masih terbuka sebagian** |
| Implementasi aplikasi | **Tidak dilakukan** |

**Kesimpulan:** nominal Rp50.000.000 dan Rp100.000.000 tidak boleh dipakai sebagai nilai wajib atau batas otomatis. Catatan anggaran perlu memisahkan tahap proposal, persetujuan, revisi, realisasi, dan sisa anggaran dengan traceability. Otoritas persetujuan tetap mengikuti kewenangan organisasi yang telah diverifikasi.