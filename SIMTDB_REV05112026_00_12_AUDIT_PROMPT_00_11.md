# SIM-TDB — AUDIT PROMPT 00.11
## Finance Logical Integrity, Transaction Control, and Master Policy Governance

**Document ID:** SIMTDB-REV05112026-00-12-AUDIT-11  
**File yang diaudit:** `SIMTDB_REV05112026_00_11_FINANCE_LOGICAL_INTEGRITY_AND_TRANSACTION_CONTROL_PROMPT.md`  
**Status:** Draft hasil audit dokumen untuk review  
**Mode:** Read-only audit dan analisis — tanpa implementasi  
**Project:** Sistem Informasi Manajemen Tanggap Darurat Bencana (SIM-TDB)  
**Organization:** Caritas Keuskupan Malang — Tim Solidaritas Kemanusiaan Keuskupan Malang (TSKKM)

---

## 1. Kesimpulan eksekutif

Prompt 00.11 mengidentifikasi banyak risiko teknis Finance yang relevan, termasuk konsumsi ceiling ganda, concurrency, retry, offline synchronization, versi policy, rekonsiliasi kas, dan audit trail.

Namun, **Prompt 00.11 belum aman digunakan tanpa koreksi provenance dan tata kelola**. Bagian “New Governance Requirement” menyatakan seolah-olah project owner telah secara eksplisit menyetujui:

- Master Policy harus dibekukan selama program aktif.
- Tidak ada perubahan policy saat kewajiban keuangan masih terbuka.
- Hanya SuperAdmin yang dapat membuat setup awal atau mengamendemen policy.
- Setiap amendment harus memiliki SK/decision number, tanggal, penerbit, dokumen asli, dan verifikasi.
- Tidak boleh ada override SuperAdmin saat policy terkunci.

Aturan-aturan tersebut **tidak ditetapkan secara eksplisit dalam instruksi pemilik proyek yang terlihat pada percakapan sebelumnya**. Arahan yang telah disampaikan adalah menyiapkan opsi dan menu setup agar policy dapat dikonfigurasi secara fleksibel dengan kontrol dan akuntabilitas. Arahan tersebut belum menetapkan freeze menyeluruh, aturan wajib SK, SuperAdmin sebagai satu-satunya eksekutor, atau larangan override absolut.

Karena itu, klaim bahwa aturan governance tersebut “explicitly approved” adalah **temuan kritis**. Aturan itu harus diklasifikasikan sebagai `PENDING_OWNER_ACCEPTANCE` atau `PENDING_ORG_DECISION`, kecuali ada bukti persetujuan terpisah.

### Penilaian keseluruhan

| Area | Penilaian |
|---|---|
| Kontrol integritas transaksi dan idempotency | Baik sebagai rancangan teknis; perlu dipisahkan dari policy organisasi |
| Ledger konsumsi ceiling | Relevan dan perlu dianalisis; event yang mengonsumsi ceiling tetap pending |
| Policy configurability | Konsisten dengan arahan pemilik proyek |
| Freeze policy saat operasi aktif | Belum terbukti disetujui; berpotensi overblocking |
| Kewajiban SK untuk setiap amendment | Belum terbukti sebagai aturan organisasi; perlu keputusan |
| SuperAdmin | Kapabilitas teknis berisiko menjadi kewenangan organisasi baru jika tidak dibatasi |
| Offline/concurrency recovery | Arah baik, tetapi perlu status sebagai rekomendasi teknis |
| Provenance dokumen | Perlu koreksi sebelum prompt dijalankan |
| Implementasi atau pengujian | Tidak dilakukan |

**Rekomendasi:** jangan jalankan Prompt 00.11 sebagai prompt yang menganggap governance freeze dan SK wajib sudah disetujui. Revisi terlebih dahulu agar menghasilkan **opsi keputusan** dan mencatat aturan tersebut sebagai pending sampai pemilik/otoritas organisasi mengesahkannya.

---

## 2. Scope dan keterbatasan audit

Audit ini memeriksa teks Prompt 00.11 yang disampaikan dalam percakapan dan membandingkannya dengan arahan sebelumnya yang tersedia di percakapan.

Audit ini tidak:

- Memeriksa file di workspace atau repository.
- Memeriksa branch, commit, code, schema, API, migration, seed, konfigurasi, atau test suite.
- Menjalankan aplikasi atau test.
- Memeriksa seluruh SOP.
- Menetapkan keputusan organisasi.
- Mengubah code, database, dokumen sumber, atau file proyek.

### Evidence yang tersedia

| Sumber | Status | Batas |
|---|---|---|
| Prompt 00.11 | Tersedia dalam percakapan dan dibaca | Instruksi audit, bukan bukti keputusan organisasi. |
| Arahan fleksibilitas dan setup policy dari pemilik proyek | Tersedia dalam percakapan | Mendukung kebutuhan opsi/configuration; tidak menyebut seluruh freeze/SK/SuperAdmin rules dalam 00.11. |
| Dokumen 00_10 | Isinya tersedia sebelumnya dalam percakapan | Audit terdahulu; bukan keputusan organisasi formal. |
| Gambar SOP halaman cetak 16–29 | Pernah diunggah dan menjadi konteks percakapan | Audit parsial; halaman lain dan template Finance tidak tersedia. |
| SOP halaman 1–15 dan 30–95 | `EVIDENCE_NOT_AVAILABLE` | Tidak dapat menyimpulkan isi atau policy dari halaman yang tidak tersedia. |
| Repository/code/database/tests | `EVIDENCE_NOT_AVAILABLE` | Tidak diperiksa atau diubah. |
| SK, mandat, delegation, dan approval matrix | `EVIDENCE_NOT_AVAILABLE` | Tidak ada dokumen bukti formal yang dapat diverifikasi. |

---

## 3. Temuan audit utama

| ID | Keparahan | Status | Temuan | Dampak | Rekomendasi |
|---|---|---|---|---|---|
| AUD-11-01 | **Kritis** | `SOURCE_CONFLICT` / `EVIDENCE_NOT_AVAILABLE` | Prompt menyatakan aturan freeze, SK wajib, dan SuperAdmin sebagai governance requirement yang telah “explicitly approved”. Bukti tersebut tidak muncul dalam arahan pemilik proyek sebelumnya yang tersedia. | Usulan teknis dapat salah dianggap sebagai kebijakan organisasi yang telah disetujui. | Hapus klaim “explicitly approved” kecuali ada keputusan tertulis. Tandai sebagai opsi dan `PENDING_OWNER_ACCEPTANCE` / `PENDING_ORG_DECISION`. |
| AUD-11-02 | **Kritis** | `PENDING_ORG_DECISION` | “No Legal Basis, No Policy Change” membuat SK/decision number dan original document wajib untuk setiap perubahan. Tidak ada bukti bahwa seluruh perubahan policy harus berbentuk SK. | Dapat menambahkan persyaratan hukum/administratif baru dan menghambat perubahan yang sah tetapi memakai bentuk keputusan lain. | Minta organisasi menentukan jenis decision basis yang diterima; jangan menetapkan SK sebagai satu-satunya bentuk tanpa otorisasi. |
| AUD-11-03 | **Tinggi** | `PENDING_ORG_DECISION` | Freeze selama program aktif dan seluruh kewajiban terbuka dapat membuat konfigurasi tidak dapat diperbarui selama operasi berjalan. | Potensi operasional dead end jika kebijakan perlu dikoreksi saat krisis, atau program terus aktif tanpa terminal state yang jelas. | Sajikan opsi: perubahan hanya untuk operasi baru; draft dapat disiapkan tetapi aktivasi ditunda; atau freeze penuh. Minta keputusan tentang pengecualian dan dampak ke transaksi aktif. |
| AUD-11-04 | **Tinggi** | `PENDING_ORG_DECISION` | SuperAdmin ditetapkan sebagai satu-satunya pelaksana setup/amendment, tetapi otoritas pengangkatan dan cakupan kapabilitas teknis belum disahkan. | Dapat menciptakan role/capability baru yang berimplikasi governance dan akses luas. | Pisahkan technical capability dari empat role organisasi. Minta keputusan tentang penunjukan, provisioning, revocation, dan dual control. |
| AUD-11-05 | **Tinggi** | `PENDING_DESIGN_DECISION` | Prompt mengunci perilaku policy ketika program aktif menjadi “selalu blocked”, tetapi tidak membedakan membuat draft policy dari mengaktifkan policy. | Tidak ada jalur persiapan perubahan saat operasi aktif; perubahan bisa tertunda sampai semua perkara selesai. | Bedakan draft preparation, authorization, scheduling, dan activation. Minta keputusan mana yang diblokir pada tiap tahap. |
| AUD-11-06 | **Tinggi** | `PENDING_DESIGN_DECISION` | Policy lock gate bergantung pada lifecycle program, incident, request, reservation, payment, advance, reconciliation, laporan, dan dokumen yang belum didefinisikan lintas modul. | Gate dapat memiliki false positive, false negative, atau tidak pernah terbuka. | Tetapkan kontrak status dan owner per modul sebelum membuat lock eligibility rule. |
| AUD-11-07 | **Tinggi** | `PENDING_DESIGN_DECISION` | Program dianggap sebagai pemicu utama freeze, padahal unit kebijakan dana darurat mungkin incident/operation/policy scope. | Cakupan freeze bisa terlalu luas atau tidak cocok dengan transaksi yang menggunakan policy. | Putuskan apakah policy mengikat program, incident, response operation, fund pool, atau gabungan; jangan mengasumsikan program sebagai unit penguncian universal. |
| AUD-11-08 | **Tinggi** | `PENDING_ORG_DECISION` | “All relevant obligations” dan “financial closure gate” belum memiliki definisi, daftar sumber, atau pejabat yang mengesahkan. | Sistem berpotensi menahan policy tanpa batas karena satu catatan atau dokumen tidak lengkap. | Buat daftar obligation yang berbasis sumber, owner, kondisi selesai, dan authority closure. |
| AUD-11-09 | **Tinggi** | `PENDING_DESIGN_DECISION` | Prompt mensyaratkan transaksi policy amendment dan program activation diserialisasi/atomik, tetapi belum mendefinisikan boundary lintas service dan kegagalan parsial. | Persyaratan concurrency dapat menjadi slogan tanpa kriteria penerimaan yang dapat diuji. | Definisikan invariant dan precondition/commit semantics secara vendor-neutral; physical mechanism menunggu database decision. |
| AUD-11-10 | **Sedang** | `TECHNICAL_RECOMMENDATION` | Hash/checksum, append-only audit, outbox/inbox, idempotency, dan ledger adalah kontrol teknis yang tepat untuk dievaluasi, tetapi beberapa di antaranya dapat terbaca sebagai kewajiban policy final. | Rekomendasi teknis bercampur dengan aturan organisasi. | Labeli sebagai opsi teknis; tentukan kebutuhan berdasarkan risk dan architecture review. |
| AUD-11-11 | **Sedang** | `PENDING_DESIGN_DECISION` | Policy Scope Instance, Program Policy Binding, Incident Scope Membership, dan Consumption Ledger ditawarkan sebagai konsep tanpa source-of-truth atau lifecycle final. | Risiko duplikasi policy values dan relasi polimorfik/orphan. | Definisikan owner dan canonical record; pertahankan nama sebagai konsep, bukan tabel final. |
| AUD-11-12 | **Sedang** | `PENDING_DESIGN_DECISION` | Prompt meminta test FIN-TEST-01 sampai FIN-TEST-80 tetapi tidak memuat seluruh test 01–46 di dalam teks, hanya meminta mencari di 00.10. | Jika 00.10 tidak tersedia di workspace, output test plan bisa tidak lengkap atau ID hilang. | Lampirkan daftar 01–46 dalam prompt atau wajib nyatakan `EVIDENCE_NOT_AVAILABLE` dan jangan mengarang isi test yang hilang. |
| AUD-11-13 | **Sedang** | `EVIDENCE_NOT_AVAILABLE` | Prompt menginstruksikan “inspect available project/workspace files” dan membuat satu file, tetapi dalam konteks saat ini tidak ada akses workspace/repository. | Auditor dapat terlanjur mengklaim pemeriksaan file/repository. | Nyatakan akses aktual; jika hanya teks percakapan yang tersedia, audit dibatasi pada teks tersebut. |
| AUD-11-14 | **Sedang** | `PENDING_OWNER_ACCEPTANCE` | Kewajiban lock eligibility report dan seluruh metrik blocker belum dibuktikan sebagai kebutuhan pemilik proyek. | Dapat menambah fitur atau data exposure tanpa keputusan. | Jadikan usulan teknis, tentukan akses, provenance, dan penggunaan report sebelum finalisasi. |

---

## 4. Perbandingan arahan pemilik proyek dengan aturan baru Prompt 00.11

### 4.1 Arahan yang didukung oleh percakapan

Arahan pemilik proyek sebelumnya mendukung:

- Policy dana darurat fleksibel dan dapat diatur melalui setup yang terkendali.
- Pilihan mode `PER_INCIDENT` atau `GLOBAL_ALL_INCIDENTS`.
- Nilai referensi Rp50m tidak di-hardcode permanen.
- Rp100m tetap nilai contoh.
- Kontrol kas eligible dan batas kebijakan tetap dipisahkan.
- Tujuan aplikasi: fleksibel tanpa kehilangan kontrol, integritas data, dan akuntabilitas.

Status: `CLARIFIED_BY_PROJECT_OWNER` sejauh sesuai teks arahan yang diberikan.

### 4.2 Ketentuan yang belum terbukti disetujui

Arahan yang tersedia belum menetapkan secara eksplisit:

- Policy dibekukan sepanjang ada satu program aktif.
- Policy tidak dapat diubah sampai semua kewajiban keuangan selesai.
- Hanya SuperAdmin yang boleh mengatur policy.
- Perubahan wajib memiliki SK dengan nomor dan tanggal.
- Setiap amendment harus memiliki original SK attachment.
- Tidak ada emergency override dalam kondisi apa pun.
- Program closure menjadi satu-satunya atau prasyarat wajib perubahan policy.
- Lock report harus menjadi fitur wajib.
- Policy change hanya boleh berlaku setelah semua operasi ditutup.

Status: `PENDING_OWNER_ACCEPTANCE` dan/atau `PENDING_ORG_DECISION`.

### 4.3 Prinsip yang perlu dipertahankan

Fleksibilitas setup bukan berarti siapa saja dapat mengubah policy. Namun kebutuhan kontrol dapat diwujudkan melalui beberapa opsi governance yang berbeda. Prompt 00.11 sebaiknya meminta perbandingan, bukan menyatakan satu model sebagai keputusan final.

---

## 5. Isu policy freeze dan risiko operasional

### 5.1 Potensi masalah

Freeze total sepanjang program aktif dapat menyebabkan:

- Policy salah atau konfigurasi awal yang keliru tidak dapat dikoreksi ketika kejadian berlangsung.
- Perubahan yang hanya berlaku untuk incident baru tertahan karena program lama masih terbuka.
- Program yang berstatus “active” tetapi tidak lagi menjalankan aktivitas dapat menahan policy tanpa batas.
- Program administratif selesai tetapi bukti finansial kecil belum lengkap dapat menghalangi semua perubahan policy.
- Kebijakan global dapat berubah secara prospektif untuk scope baru, tetapi aturan freeze tidak membedakan scope lama dengan scope baru.
- Kesalahan policy dapat terus mempengaruhi operasi karena tidak ada proses koreksi yang diizinkan.
- Tidak ada jalur pemulihan bila SuperAdmin salah mengaktifkan policy atau SK kemudian dinyatakan tidak relevan.

### 5.2 Opsi governance yang perlu ditawarkan

| Opsi | Perilaku | Kelebihan | Risiko/keputusan |
|---|---|---|---|
| A. Freeze penuh | Tidak ada perubahan amount/mode/scope saat ada program atau obligation aktif. | Melindungi konsistensi transaksi berjalan. | Dapat menahan koreksi penting dan menimbulkan deadlock. |
| B. Draft boleh dibuat, activation ditahan | Persiapan/amendment proposal boleh dilakukan; versi baru tidak aktif sampai gate bersih. | Mempercepat persiapan perubahan tanpa mengubah policy yang sedang digunakan. | Perlu membedakan draft dan active version. |
| C. Perubahan prospektif untuk scope baru | Policy lama tetap untuk kasus aktif; versi baru dapat digunakan pada scope/activation baru setelah disahkan. | Mendukung operasi lain tanpa menafsirkan ulang transaksi aktif. | Perlu aturan policy binding dan anti-overlap. |
| D. Amendment terbatas dengan keputusan formal | Perubahan tertentu dapat dilakukan selama operasi aktif berdasarkan decision basis khusus. | Menyediakan jalur koreksi saat diperlukan. | Kewenangan dan kondisi pengecualian wajib diputuskan; jangan menambahkan override diam-diam. |
| E. Freeze pada transaksi/control unit, bukan semua program | Policy yang terkait transaksi aktif terkunci; konfigurasi lain yang tidak mempengaruhi scope tersebut dapat dikelola bila diizinkan. | Lebih granular. | Memerlukan definisi scope dan dampak lintas modul yang matang. |

Tidak ada opsi yang dipilih oleh audit ini.

### 5.3 Rekomendasi untuk tahap spesifikasi

**`TECHNICAL_RECOMMENDATION`:** bedakan pembuatan draft, review, authorization, effective date, dan activation. Jangan menafsirkan perubahan draft sebagai perubahan policy aktif.

**`PENDING_ORG_DECISION`:** apakah activation selalu diblokir selama ada aktivitas/obligation, dapat berlaku prospektif untuk scope baru, atau mempunyai prosedur amendment khusus.

---

## 6. SK dan decision-basis governance

### 6.1 Temuan

Prompt 00.11 mewajibkan nomor SK/keputusan, tanggal, penerbit, penandatangan, judul, ringkasan, dokumen asli, tanggal efektif, alasan perubahan, dan verifikasi.

Ini merupakan kontrol dokumentasi yang rinci, tetapi tidak ada evidence yang tersedia bahwa organisasi menetapkan seluruh field tersebut sebagai persyaratan wajib untuk setiap perubahan Master Policy.

### 6.2 Risiko

- “SK” dapat dipaksakan walaupun keputusan sah menggunakan bentuk dokumen lain.
- System field dapat meminta nomor SK yang tidak ada dan mendorong pengisian data rekaan.
- Upload file dianggap bukti otentik padahal tidak memverifikasi kewenangan atau keaslian.
- Satu dokumen dapat dipakai untuk amendment yang tidak tercakup oleh subject/authority-nya.
- Persetujuan teknis SuperAdmin dapat salah dianggap sebagai keputusan kebijakan.

### 6.3 Rekomendasi

- Ganti “mandatory SK” dengan “decision basis resmi yang disetujui organisasi”, kecuali organisasi secara formal mensyaratkan SK.
- Sediakan jenis dokumen dasar keputusan yang dikonfigurasi setelah organisasi menyetujuinya; jangan membuat jenis legal basis tanpa persetujuan.
- Bedakan upload, verifikasi administratif, verifikasi authority, dan activation.
- Jangan membuat contoh SK palsu. Bila contoh diperlukan, beri label jelas `ILLUSTRATIVE — NOT A REAL SK`.
- Catat kewajiban nomor/tanggal/issuer/signatory hanya berdasarkan dokumen yang benar-benar memiliki atribut tersebut atau kebijakan formal.

Status: `PENDING_ORG_DECISION`.

---

## 7. SuperAdmin dan batas role organisasi

### 7.1 Isu

Baseline SIM-TDB menetapkan tepat empat role organisasi. Prompt 00.11 menambahkan “authorized SuperAdmin account” sebagai aktor tunggal policy setup.

Prompt sebelumnya menyebut kapabilitas admin teknis harus terpisah dari empat role dan memerlukan persetujuan Caritas. Prompt 00.11 harus membawa ketentuan itu dengan jelas; saat ini ia menyatakan SuperAdmin sebagai requirement tanpa bukti pengangkatan atau governance.

### 7.2 Kontrol yang dapat direkomendasikan

`TECHNICAL_RECOMMENDATION`:

- SuperAdmin, jika disetujui, adalah technical capability, bukan role organisasi kelima.
- Gunakan identitas individual, bukan akun bersama.
- Terapkan least privilege dan MFA/step-up authentication.
- Pisahkan policy read dari policy change.
- Catat session dan action.
- Jangan izinkan SuperAdmin menciptakan authority organisasi.
- Uji deny server-side untuk user non-authorized.

### 7.3 Keputusan yang dibutuhkan

- Siapa menunjuk dan mencabut SuperAdmin?
- Apakah SuperAdmin boleh mengusulkan saja atau juga mengaktifkan policy?
- Apakah diperlukan verifikator/approver terpisah?
- Apa proses bila SuperAdmin tidak tersedia?
- Apakah akses emergency account diizinkan dan dalam kondisi apa?

Jangan menetapkan jawabannya atas nama organisasi.

---

## 8. Deadlock dan race-condition audit

### 8.1 Initial setup bootstrap deadlock

Prompt menetapkan:

- Setup awal hanya sebelum program pertama diaktifkan.
- Program tidak boleh diaktifkan tanpa policy aktif (test 59).
- Setup awal hanya dilakukan oleh SuperAdmin.
- Setup harus memiliki governing source.
- Authority SuperAdmin dan sumber policy belum tersedia.

Tanpa pemilik, SuperAdmin, sumber policy, dan approval path yang ditetapkan, program tidak dapat mulai. Ini bukan salah secara teknis, tetapi **bootstrap dependency harus ditangani sebagai keputusan governance**.

### 8.2 Lock gate menunggu penutupan yang tidak terdefinisi

Policy diblokir sampai program, incident, operation, transaksi, advances, payments, reconciliations, reports, dan obligations selesai. Namun:

- Status sumber belum diselaraskan.
- “Final closure” belum didefinisikan.
- Pemilik setiap blocker belum ditetapkan.
- Tidak ada mekanisme penyelesaian jika dokumen atau transaksi disengketakan.
- Belum ada daftar apakah setiap item benar-benar mengunci seluruh policy atau hanya scope terkait.

Risikonya adalah policy terkunci permanen atau report kelayakan salah menyatakan “eligible”.

### 8.3 Race antara policy activation dan program activation

Prompt benar meminta perlindungan race-condition, tetapi belum cukup membatasi invariant yang akan diuji.

Invariant logis yang disarankan:

1. Setiap program activation menggunakan tepat satu policy version yang telah aktif dan cocok dengan scope-nya.
2. Policy amendment tidak dapat mengubah policy version yang sedang dipakai program/transaction.
3. Policy activation dan program activation harus menggunakan satu keputusan konsisten; tidak boleh terjadi commit parsial.
4. Policy selection dan lock gate harus dievaluasi ulang pada batas commit.
5. Konflik concurrent menyebabkan satu operasi ditolak/diulang dengan hasil yang dapat ditelusuri; tidak ada silent overwrite.

Mekanisme teknis/DB-specific tidak ditetapkan.

---

## 9. Audit kelengkapan data dan workflow

### 9.1 Policy lock eligibility

Prompt mengusulkan banyak blocker, tetapi perlu menambahkan:

- Owner data untuk setiap blocker.
- Source-of-truth record.
- Apakah blocker berlaku untuk seluruh policy atau hanya scope/fund pool terkait.
- Bukti yang membuat blocker dianggap selesai.
- Siapa yang mengesahkan penutupan.
- Cara menangani data yang disputed/unknown.
- Refresh/freshness requirement pada lock report.
- Apa yang terjadi bila salah satu modul tidak merespons.
- Perbedaan antara hard blocker dan warning.

Tanpa ini, `Policy Lock Eligibility Report` dapat memberikan hasil tidak akurat.

### 9.2 Ledger konsumsi ceiling

Konsep ledger yang diajukan relevan, tetapi belum menentukan:

- Apakah event dicatat saat reservation, approval, cash release, atau tahap lain.
- Apakah satu event dapat mempengaruhi ceiling dan cash secara berbeda.
- Cara mengonversi reservation ke release tanpa double count.
- Bagaimana amount/currency/policy-version diperlakukan bila policy berubah.
- Bagaimana correction dan reversal mempengaruhi rekonstruksi historis.
- Apakah ledger ini subledger Finance atau control ledger operasional.

Semua hal tersebut harus tetap pending, bukan disimpulkan dari field list.

### 9.3 Test IDs 01–46

Prompt 00.11 menginstruksikan pelestarian FIN-TEST-01–46, tetapi tidak memuat daftar tersebut. Jika file 00.10 tidak tersedia di workspace, test IDs dan detailnya tidak boleh direkonstruksi dengan tebakan.

Instruksi harus menyatakan:
- Jika daftar asli tersedia, lampirkan atau kutip versi yang diperiksa.
- Jika tidak tersedia, catat `EVIDENCE_NOT_AVAILABLE` dan minta sumbernya.
- Jangan membuat daftar pengganti yang diklaim sama.

---

## 10. Uji logika prompt 00.11

Uji ini menilai konsistensi instruksi prompt, bukan aplikasi.

| ID | Uji | Hasil review |
|---|---|---|
| PROMPT-TEST-01 | Apakah prompt menjaga Rp100m sebagai ilustratif? | Ya, baseline meminta hal tersebut; pertahankan. |
| PROMPT-TEST-02 | Apakah mode `PER_INCIDENT` dan `GLOBAL_ALL_INCIDENTS` tetap dapat dipilih? | Ya, tetapi policy-freeze rules tambahan belum disetujui. |
| PROMPT-TEST-03 | Apakah mode aktif menentukan agregasi? | Ya, dinyatakan dengan jelas. |
| PROMPT-TEST-04 | Apakah eligible cash dipisahkan dari ceiling? | Ya, arah yang benar; basis kas tetap pending. |
| PROMPT-TEST-05 | Apakah prompt membedakan owner clarification dari formal organization decision? | Sebagian. Ia melarang label `ORG_DECISION_CONFIRMED` tanpa bukti, tetapi salah menyebut beberapa governance rules sebagai explicitly approved. |
| PROMPT-TEST-06 | Apakah SK wajib memiliki sumber bukti? | Tidak. Persyaratan SK wajib diasumsikan tanpa bukti formal. |
| PROMPT-TEST-07 | Apakah SuperAdmin tetap terpisah dari empat role? | Belum cukup tegas; pengangkatan dan kapabilitasnya masih harus disetujui. |
| PROMPT-TEST-08 | Apakah lock gate punya status dan owner data? | Belum lengkap. |
| PROMPT-TEST-09 | Apakah program closure sama dengan financial closure? | Prompt membedakan keduanya dengan benar, tetapi definisi dan authority closure belum tersedia. |
| PROMPT-TEST-10 | Apakah policy activation dan program activation race-safe dapat diuji secara logis? | Ya sebagai requirement, tetapi commit invariant dan kegagalan parsial perlu diperjelas. |
| PROMPT-TEST-11 | Apakah konsumsi ceiling dan cash movement dipisahkan? | Ya, fokus yang baik; event semantics tetap pending. |
| PROMPT-TEST-12 | Apakah test terdahulu dapat dipertahankan tanpa sumber? | Tidak. Prompt bergantung pada 00.10 yang mungkin tidak tersedia; perlu aturan evidence missing. |
| PROMPT-TEST-13 | Apakah prompt hanya mengizinkan satu output baru? | Ya; tidak ada implementasi yang diminta. |
| PROMPT-TEST-14 | Apakah read-only boundary cukup? | Ya pada prinsip; bila workspace tidak ada, harus menyatakan audit hanya atas teks percakapan. |
| PROMPT-TEST-15 | Apakah kebijakan fleksibel dapat berubah saat operasi aktif? | Prompt memilih freeze penuh, tetapi pilihan ini belum terbukti disetujui dan dapat membuat deadlock. |

---

## 11. Rekomendasi koreksi pada Prompt 00.11

Sebelum digunakan, lakukan perubahan berikut pada prompt tersebut. Perubahan ini adalah rekomendasi untuk dokumen prompt, bukan perubahan code atau database.

1. Ganti klaim “project owner has explicitly approved” pada bagian Master Policy Lock dengan:
   > “Ini adalah opsi governance yang diajukan untuk dianalisis. Kecuali ada evidence keputusan terpisah, tandai sebagai `PENDING_OWNER_ACCEPTANCE` atau `PENDING_ORG_DECISION`.”

2. Jangan tetapkan SK sebagai satu-satunya dasar setiap amendment sebelum ada keputusan formal. Minta analisis opsi:
   - SK.
   - Keputusan tertulis lain.
   - Delegasi/mandat yang berlaku.
   - Dokumen resmi lain yang diterima organisasi.

3. Jadikan freeze penuh sebagai salah satu opsi, bukan aturan yang sudah final. Bandingkan dengan:
   - Draft boleh disiapkan saat operasi berlangsung tetapi activation ditahan.
   - Policy baru berlaku prospektif untuk scope/activation baru.
   - Amendment pada scope aktif hanya melalui decision process formal, jika organisasi memilih opsi tersebut.

4. Pisahkan:
   - Policy draft.
   - Policy review.
   - Policy authorization.
   - Policy activation.
   - Policy freeze terhadap versi aktif.
   - Policy change terhadap scope baru.

5. Jelaskan bahwa SuperAdmin:
   - Bukan role organisasi kelima.
   - Belum disahkan sebagai aktor atau pemegang otoritas.
   - Hanya dapat menjadi technical capability bila disetujui.
   - Tidak menjadi pembuat policy organisasi.

6. Definisikan lock blocker melalui:
   - Entitas sumber.
   - Owner module.
   - Status yang dibaca.
   - Bukti resolusi.
   - Scope dampak.
   - Pihak yang mengesahkan closure.

7. Jangan membuat lock report yang menggabungkan data finance pribadi/sensitif tanpa access policy dan redaction yang disetujui.

8. Jika 00.10 atau test FIN-TEST-01–46 tidak tersedia, tandai sumber/test list sebagai `EVIDENCE_NOT_AVAILABLE`; jangan mengarang kembali.

9. Pertahankan requirement output 00.11 hanya jika tugasnya memang menjalankan Prompt 00.11. Jika tugasnya audit Prompt 00.11, buat output audit baru dengan nama berbeda agar tidak terjadi benturan.

10. Tetapkan readiness berdasarkan bukti, bukan berdasarkan keberadaan diagram atau daftar test.

---

## 12. Pending Decision Register

| ID | Pertanyaan | Opsi awal untuk dibahas | Evidence yang dibutuhkan | Pemilik keputusan |
|---|---|---|---|---|
| GOV-01 | Apakah policy aktif harus benar-benar dibekukan selama program berjalan? | Freeze penuh; draft-only selama aktif; prospective policy untuk scope baru; opsi lain | Keputusan governance tertulis dan alasan operasional | `OWNER TO BE DESIGNATED` |
| GOV-02 | Apakah amendment wajib memiliki SK, atau dapat menggunakan jenis keputusan formal lain? | SK wajib; jenis dokumen resmi yang diakui; mandate/delegation tertentu | Kebijakan/dokumen formal yang mengatur decision basis | `OWNER TO BE DESIGNATED` |
| GOV-03 | Siapa berwenang menetapkan initial policy? | Authority organisasi + technical executor; struktur lain yang disahkan | Mandat/keputusan organisasi | `OWNER TO BE DESIGNATED` |
| GOV-04 | Apakah SuperAdmin disetujui sebagai technical capability? | Tidak digunakan; capability terpisah; pembagian tugas khusus | Keputusan akses dan provisioning | `OWNER TO BE DESIGNATED` |
| GOV-05 | Siapa boleh membuat draft, memverifikasi evidence, mengesahkan, dan mengaktifkan policy? | Satu pelaksana; maker-checker; alur lain | Approval/delegation matrix | `OWNER TO BE DESIGNATED` |
| GOV-06 | Apakah draft amendment boleh dibuat saat operasi aktif? | Boleh tanpa activation; tidak boleh dibuat; opsi lain | Keputusan governance | `OWNER TO BE DESIGNATED` |
| GOV-07 | Apakah policy baru boleh berlaku prospektif untuk incident/activation baru saat policy lama sedang digunakan? | Ya; tidak; hanya pada scope berbeda | Keputusan policy version/binding | `OWNER TO BE DESIGNATED` |
| GOV-08 | Program status apa yang dianggap aktif, ditangguhkan, terminal, atau ditutup? | Mapping dari vocabulary existing; status baru hanya jika disahkan | Data dictionary/workflow Program | `OWNER TO BE DESIGNATED` |
| GOV-09 | Apa financial closure gate dan siapa yang mengesahkannya? | Berdasarkan rekonsiliasi; dokumentasi; keputusan lain | Pedoman Finance dan authority | `OWNER TO BE DESIGNATED` |
| GOV-10 | Obligation apa yang mengunci perubahan policy? | Daftar blocker dengan scope dan resolusi | SOP/Finance policy | `OWNER TO BE DESIGNATED` |
| GOV-11 | Apakah lock berlaku untuk seluruh policy atau hanya fund pool/scope terkait? | Global; per scope; per fund pool | Keputusan governance dan model policy | `OWNER TO BE DESIGNATED` |
| GOV-12 | Siapa memverifikasi SK/decision document dan apa cakupan verifikasinya? | Petugas/authority yang ditunjuk; proses dokumen | Keputusan organisasi dan document governance | `OWNER TO BE DESIGNATED` |
| GOV-13 | Apa status yang berlaku bagi active incident ketika policy berubah? | Retain old version; new request adopts new version; formal migration | Keputusan transisi | `OWNER TO BE DESIGNATED` |
| GOV-14 | Bagaimana menangani policy yang salah atau berpotensi membahayakan operasi saat active? | Hold future activation; correction workflow; opsi formal lain | Keputusan emergency governance | `OWNER TO BE DESIGNATED` |
| GOV-15 | Siapa yang memiliki dan mengakses Policy Lock Eligibility Report? | Finance-only; restricted admin; role lain sesuai scope | Access matrix dan privacy review | `OWNER TO BE DESIGNATED` |

Semua pertanyaan pada tabel ini tetap pending sampai bukti keputusan tersedia.

---

## 13. Readiness Assessment

| Area | Status | Alasan |
|---|---|---|
| Audit Prompt 00.11 sebagai dokumen | **CONDITIONAL** | Banyak kontrol teknis relevan, tetapi provenance governance harus dikoreksi. |
| Owner clarification configurable amount/mode | **READY** sebagai requirement yang dinyatakan | Konsisten dengan arahan pemilik proyek di percakapan. |
| Freeze policy selama operasi | **BLOCKED** | Belum ada persetujuan yang dapat diverifikasi. |
| SK sebagai dasar wajib setiap amendment | **BLOCKED** | Tidak ada bukti bahwa SK adalah satu-satunya bentuk dasar yang disahkan. |
| SuperAdmin capability | **BLOCKED** | Penunjukan, scope akses, dan governance belum disahkan. |
| Policy lock eligibility | **CONDITIONAL** | Dapat dirancang sebagai opsi, tetapi sumber status dan closure gate belum lengkap. |
| Consumption ledger | **CONDITIONAL** | Konsep berguna; event semantics dan canonical records belum ditentukan. |
| Cash availability model | **BLOCKED** | Formula/source/restricted fund treatment belum disahkan. |
| Transaction lifecycle | **CONDITIONAL** | Dapat menjadi candidate model; tidak boleh mengunci policy status/accounting terms. |
| Offline/concurrency test design | **CONDITIONAL** | Tes dapat dirancang; platform/DB dan operasi offline policy belum tersedia. |
| Repository/code/database audit | **BLOCKED_BY_MISSING_SOURCE** | Repository dan artefak teknis tidak tersedia. |
| Test execution | **BLOCKED_BY_MISSING_SOURCE** | Tidak ada application/test evidence. |
| Finance logical finalization | **BLOCKED** | Governance, authority, event semantics, cash model, dan relasi belum disahkan. |
| Physical schema/development | **NO_GO** | Tidak termasuk audit ini dan belum siap berdasarkan evidence. |

---

## 14. Pernyataan akhir

Prompt 00.11 mengandung rancangan integritas Finance yang berguna, tetapi melampaui bukti yang tersedia saat menyebut policy freeze, SK wajib, SuperAdmin, dan larangan override sebagai requirement yang telah disetujui pemilik proyek.

Arah yang lebih konsisten dengan tujuan SIM-TDB adalah:

- Tetap menyediakan policy setup yang fleksibel dan terkendali.
- Sajikan beberapa opsi governance, bukan menetapkan satu opsi tanpa persetujuan.
- Bedakan policy aktif, draft perubahan, authority formal, technical permission, dan transaksi.
- Pastikan perubahan versi tidak menafsirkan ulang histori.
- Definisikan lock berdasarkan sumber data dan scope yang jelas jika organisasi memilih mekanisme lock.
- Jangan menganggap seluruh perubahan harus berbentuk SK tanpa dasar formal.
- Jangan menjadikan SuperAdmin pemilik atau pembuat kewenangan organisasi.
- Pertahankan batas read-only dan jangan mengklaim repository/code/database/test telah diaudit.
- Tunda physical schema dan development sampai keputusan policy kritis disahkan.

**Status akhir:** Prompt 00.11 perlu direvisi sebelum digunakan sebagai instruksi audit yang menganggap governance tersebut telah disetujui. Audit ini read-only; tidak ada code, database, migration, seed, konfigurasi, atau test yang diubah atau dijalankan.