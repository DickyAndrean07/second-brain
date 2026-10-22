---
type: project-spec
title: "Product Requirements Document (PRD) — EduNotify MVP"
project: "EduNotify"
version: "1.0.0"
status: "APPROVED_FOR_SPEC"
created: 2026-10-22
updated: 2026-10-22
author: "Diva (Product & System Analyst)"
target_builder: "Bagus (Builder Agent)"
tags:
  - project/edunotify
  - spec/prd
  - domain/education
  - architecture/multitenant
---

# 📘 Product Requirements Document (PRD) — EduNotify MVP

---

## 1. Executive Summary & Visi Produk

**EduNotify** adalah platform web presensi siswa berbasis alur jadwal pelajaran (*schedule-driven relay attendance*) yang dilengkapi dengan *Early Warning System* deterministik dan narasi analitik berbasis AI. 

### Masalah Utama yang Diselesaikan
1. **Presensi Menggantung**: Guru jam pertama berhalangan hadir sehingga presensi harian sering tidak tercatat hingga akhir hari.
2. **Keterlambatan Intervensi Siswa Alpa**: Wali kelas terlambat mengetahui siswa tidak hadir tanpa keterangan karena rekap baru ada sore atau keesokan harinya.
3. **Biaya & Kompleksitas Komunikasi**: Layanan WhatsApp Business API berbayar mahal untuk sekolah kecil-menengah. EduNotify memanfaatkan mekanisme *Click-to-Chat* (`wa.me`) langsung dari WhatsApp web/device wali kelas tanpa biaya per pesan.
4. **Analisis Manual & Subjektif**: Sekolah kesulitan mengidentifikasi pola absensi kronis sebelum siswa terlanjur tertinggal jauh.

### Prinsip Desain
- **Komersial & Portofolio Nyata**: Dibangun untuk operasional nyata satu sekolah percontohan, namun memiliki arsitektur terisolasi per sekolah (`school_id`) untuk kesiapan SaaS masa depan.
- **Deterministik Sebelum AI**: Seluruh metrik statistik, persentase, dan indikator peringatan dihitung 100% oleh program backend. AI hanya bertindak sebagai narator ringkasan dan penyedia rekomendasi non-punitif.
- **Provider-Agnostic AI**: Lapisan integrasi AI modular yang dapat beralih antara endpoint lokal (9Router/Ollama) dan API cloud (OpenAI/Anthropic/Gemini) melalui *environment variables*.
- **Privacy-First**: Penghapusan data identitas pribadi (PII) sebelum data dikirimkan ke model AI.

---

## 2. Target Pengguna & Matriks Hak Akses (RBAC)

### 2.1 Persona Pengguna

| Role | Deskripsi | Kebutuhan Utama |
|---|---|---|
| **Admin Sekolah** | Staf tata usaha / operator IT sekolah | Kelola master data, jadwal, kalender akademik, akun guru, monitoring kelengkapan data harian, dan audit log. |
| **Guru Mata Pelajaran** | Pengajar di kelas sesuai jam pelajaran | Melihat jadwal mengajar hari ini, melakukan input presensi estafet untuk kelas yang belum diabsen. |
| **Wali Kelas** | Guru penanggung jawab satu rombongan belajar (rombel) | Monitoring presensi kelas binaan, tindak lanjut siswa Alpa via WhatsApp Click-to-Chat, melihat peringatan dini siswa. |
| **Kepala Sekolah** | Pimpinan manajerial sekolah | Monitoring agregat tingkat kehadiran sekolah, tren antarkelas, dan ringkasan eksekutif AI. |
| **Operator Platform** | Administrator teknis EduNotify (SaaS tier) | *Internal role* masa depan; pada MVP tidak memiliki akses ke rekaman data siswa individual sekolah. |

### 2.2 Matriks Hak Akses Fitur

| Modul / Tindakan | Admin Sekolah | Guru Mapel | Wali Kelas | Kepala Sekolah |
|---|:---:|:---:|:---:|:---:|
| Kelola Data Siswa, Guru, Kelas, Rombel | **Full** | No | No | Read |
| Kelola Jadwal Pelajaran & Kalender Akademik | **Full** | Read (Jadwal Sendiri) | Read (Kelas Binaan) | Read |
| Input Presensi Hari H (Jam Mengajar) | Override | **Input** (Sesuai Jadwal) | **Input** (Jika Mengajar) | No |
| Monitoring Siswa Alpa Hari Ini | Global | Kelas yang Diajar | **Kelas Binaan** | Global Summary |
| Buka Link WA Click-to-Chat Orang Tua | No | No | **Ya** (Kelas Binaan) | No |
| Catat Status Tindak Lanjut WA | No | No | **Ya** | Read |
| Koreksi Presensi: Hari H | **Ya** | **Ya** (Pengisi Asli) | **Ya** (Kelas Binaan) | No |
| Koreksi Presensi: H-1 s/d H-3 | **Ya** | No | **Ya** (Wajib Alasan) | No |
| Koreksi Presensi: > H-3 | **Ya** (Wajib Alasan) | No | No | No |
| Lihat Audit Log Koreksi | **Full** | Riwayat Sendiri | Riwayat Kelas Binaan | Read Summary |
| Lihat Early Warning System (EWS) | Full | Siswa di Kelasnya | **Kelas Binaan** | Global |
| Generate Ringkasan AI Mingguan/Bulanan | Full | No | **Kelas Binaan** | **Sekolah** |
| Ekspor Laporan Excel/PDF | **Full** | Terbatas | **Kelas Binaan** | **Full** |

---

## 3. Ruang Lingkup MVP (Scope Boundary)

### 3.1 In-Scope (MVP)
1. **Autentikasi & Otorisasi**: Login via Email & Password, aktivasi akun terkelola oleh Admin, sesi berbasis JWT/Secure Cookie, proteksi RBAC.
2. **Master Data & Kalender**:
   - CRUD data siswa (NIS, NISN, Nama, Gender, Kelas, Kontak Ortu).
   - CRUD data guru (NIP, Nama, Email, Kontak).
   - CRUD data kelas & rombongan belajar.
   - Impor massal siswa dan guru via template Excel/CSV dengan validasi duplikasi.
   - Kalender sekolah: penetapan hari belajar aktif, hari libur nasional/sekolah, hari khusus (kegiatan non-KBM).
   - Jadwal mingguan: pemetaan Kelas + Hari + Jam Mulai/Selesai + Mata Pelajaran + Guru Pengampu.
3. **Mesin Presensi Estafet (Schedule-Driven Relay Attendance)**:
   - Inisialisasi otomatis status harian siswa: `Belum Diabsen` pada hari aktif.
   - Otorisasi pengisian dinamis: Guru jam pertama diizinkan pertama kali; jika belum terisi, guru jam berikutnya dapat mengisi.
   - Penguncian atomik (*idempotency & locking*): mencegah konflik jika dua guru membuka kelas bersamaan.
   - Peringatan pukul 12.00 waktu lokal jika kelas belum diisi.
   - Penandaan kelas belum selesai setelah jadwal terakhir berakhir dan eskalasi ke Wali Kelas/Admin.
   - Pengisian terlambat (*late submission*) dengan pencatatan status terlambat.
4. **Alur Komunikasi WhatsApp Manual**:
   - Filter instan daftar siswa status `Alpa` per kelas pada dashboard Wali Kelas.
   - Tombol *Click-to-Chat* (`https://wa.me/<nomor>?text=<encoded_template>`).
   - Template pesan baku berisi nama sekolah, nama siswa, tanggal, kelas, dan permohonan konfirmasi.
   - Manajemen status tindak lanjut: `Belum Dibuka`, `WhatsApp Dibuka`, `Ditandai Sudah Dihubungi`.
   - Dukungan satu nomor kontak untuk multi-siswa (kakak-beradik).
5. **Koreksi Presensi & Audit Trail**:
   - Formulir koreksi status kehadiran dengan input alasan wajib.
   - Validasi batas tanggal koreksi berbasis RBAC (Hari H, H-1..H-3, >H-3).
   - Tabel audit log terenkapsulasi: timestamp, user_id, student_id, old_status, new_status, reason.
6. **AI Analytics & Early Warning Engine**:
   - *Rule-Engine* deterministik untuk menghitung: frekuensi Alpa, Alpa beruntun, pola Alpa hari tertentu (misal: Senin/Jumat), dan deviasi kehadiran.
   - Narator pola kehadiran siswa & ringkasan mingguan kelas berbasis AI.
   - Rekomendasi intervensi operasional (pembinaan wali kelas, mediasi BK, pemanggilan ortu).
   - Lapisan AI *provider-agnostic* (konfigurasi `.env`).
7. **Laporan & Ekspor**:
   - Filter rekap harian, mingguan, bulanan, semester.
   - Ekspor lembar rekapitulasi ke format Excel (.xlsx) dan dokumen cetak PDF.

### 3.2 Out-of-Scope (Bukan untuk MVP)
- WhatsApp Business API (Cloud API) atau gateway pihak ketiga berbayar.
- Chatbot otomatis WhatsApp dua arah atau webhook penerima pesan balasan.
- Portal/Akun login mandiri untuk Orang Tua dan Siswa.
- Mesin presensi biometrik fisik (fingerprint/face recognition hardware).
- Billing, subscription, dan registrasi mandiri multi-sekolah publik (SaaS billing).
- Penilaian akademik / sistem rapor siswa.

---

## 4. Alur Bisnis & Spesifikasi Logika Sistem

### 4.1 Siklus Harian Presensi Siswa

```
[Mulai Hari Sekolah Aktif]
         │
         ▼
[Semua Siswa Terjadwal di-set "Belum Diabsen"]
         │
         ▼
[Guru Jam 1 Mengajar] ──(Hadir & Mengisi?)──► [Simpan Presensi Resmi] ──► [Kunci Presensi Hari Ini]
         │ Tidak / Berhalangan                                                   │
         ▼                                                                       │
[Guru Jam 2 Mengajar] ──(Hadir & Mengisi?)──► [Simpan Presensi Resmi] ───────────┤
         │ Tidak / Berhalangan                                                   │
         ▼                                                                       │
[Pukul 12.00: Warning Belum Terisi] ──► (Dashboard Wali Kelas & Admin)          │
         │                                                                       │
         ▼                                                                       │
[Seluruh Jam Selesai: Status Belum Selesai] ─────────────────────────────────────┤
         │                                                                       │
         ▼                                                                       │
[Pengisian Terlambat oleh Guru/Wali Kelas]                                        │
         │                                                                       │
         ▼                                                                       │
[Tercatat Resmi] ◄───────────────────────────────────────────────────────────────┘
         │
         ├──► Jika ada ALPA ──► Wali Kelas: Klik "Kirim WA" ──► Update Status Intervensi
         └──► Hitung Metrik EWS ──► Deteksi Anomali ──► Generate Rekomendasi AI
```

### 4.2 Aturan Validasi Otorisasi Estafet
1. **Otorisasi Jam Pelajaran**:
   - Guru $G$ berhak mengisi presensi kelas $K$ pada tanggal $T$ jika dan hanya jika $G$ terdaftar sebagai pengampu mata pelajaran di kelas $K$ pada hari tersebut.
   - Guru urutan jam lebih awal diprioritaskan. Jika jam ke-1 belum menyimpan data, jam ke-2 otomatis berhak mengisi saat jam pelajarannya dimulai atau berlangsung.
   - Begitu data presensi resmi kelas $K$ tanggal $T$ berhasil disimpan (`status = SUBMITTED`), guru jam berikutnya **hanya dapat membaca** dan tidak dapat menimpa presensi kecuali melalui mekanisme koreksi.
2. **Penanganan Konkurensi & Double-Submit**:
   - Endpoint penyimpanan presensi wajib menerapkan *idempotency key* dan *database unique constraint* pada kombinasi `(school_id, class_id, date)`.
   - Menggunakan mekanisme *optimistic locking* atau *atomic conditional write*: jika status presensi sudah berubah menjadi `SUBMITTED`, transaksi kedua wajib ditolak dengan pesan: *"Presensi untuk kelas ini baru saja disimpan oleh [Nama Guru]."*.
3. **Pengisian Terlambat (Late Filing)**:
   - Jika hingga jam pelajaran terakhir selesai presensi belum terisi, sesi presensi ditandai `UNCOMPLETED_ALERT`.
   - Pengisian setelah jam sekolah berakhir pada Hari H tetap diizinkan oleh Wali Kelas atau salah satu Guru Pengampu hari itu, dengan tanda `is_late_submission = true` di audit log.

### 4.3 Matriks Koreksi Presensi

| Kondisi Waktu | Pihak Berwenang | Syarat Wajib | Efek Sistem |
|---|---|---|---|
| **Hari H (Hari Pelaksanaan)** | Guru Pengisi Asli OR Wali Kelas | Alasan koreksi (min. 10 karakter) | Status record diperbarui, dicatat di `attendance_corrections`. |
| **H-1 s/d H-3 (3 Hari Kalender)** | Hanya Wali Kelas | Alasan koreksi + verifikasi dokumen (misal: surat izin) | Dicatat di audit log dengan flag *Post-Day Correction*. |
| **Lebih dari H-3 (> 72 jam)** | Hanya Admin Sekolah | Alasan resmi + konfirmasi kepala sekolah | Akses terkunci bagi guru; hanya Admin yang dapat membuka form koreksi. |

*Aturan Audit*: Nilai lama (`old_status`) **tidak pernah dihapus** dari database, melainkan ditimpa di tabel aktif dan riwayat lengkap diarsipkan di tabel histori log koreksi.

---

## 5. Integrasi WhatsApp Manual (Click-to-Chat)

### 5.1 Format Link & Enkoding
Tautan dibuat menggunakan skema resmi WhatsApp:
```
https://wa.me/{nomor_telepon_e164}?text={pesan_terenkode}
```
Aturan sanitasi nomor:
- Hilangkan karakter non-numerik (spasi, tanda hubung, tanda kurung).
- Konversi awalan `08...` menjadi kode negara Indonesia `628...`.

### 5.2 Template Pesan Baku
```text
Yth. Orang Tua / Wali dari {nama_siswa} ({kelas}),
Kami dari {nama_sekolah} menginformasikan bahwa pada hari ini, {hari_tanggal}, ananda tercatat TIDAK HADIR di sekolah tanpa keterangan (Alpa).

Mohon konfirmasi mengenai kondisi ananda melalui balasan pesan ini.
Terima kasih atas perhatian dan kerja samanya.

Salam,
{nama_wali_kelas}
Wali Kelas {kelas}
```

### 5.3 State Tracking Intervensi

```
[Belum Dibuka] ──(Wali Kelas Klik Tombol WA)──► [WhatsApp Dibuka] 
                                                        │
                               (Wali Kelas Konfirmasi Mandiri di UI)
                                                        ▼
                                          [Ditandai Sudah Dihubungi]
```

- **`Belum Dibuka`**: Status bawaan saat siswa terdata Alpa.
- **`WhatsApp Dibuka`**: Otomatis berubah saat link `wa.me` di-klik (dicatat via endpoint internal sebelum *redirect* atau event listener frontend).
- **`Ditandai Sudah Dihubungi`**: Tombol ceklis manual yang ditekan wali kelas setelah mengirim pesan secara nyata di aplikasi WhatsApp miliknya.

*Catatan Kritis*: UI harus secara eksplisit menampilkan teks bantuan: *"Menekan tombol WA membuka WhatsApp di perangkat Anda. Tandai 'Sudah Dihubungi' setelah Anda selesai mengirim pesan."* Sistem tidak boleh mengklaim pesan terkirim secara otomatis.

### 5.4 Penanganan Multi-Siswa Satu Nomor
- Jika dua siswa atau lebih (kakak-beradik) memiliki `guardian_phone` yang sama, sistem menampilkan kartu tindak lanjut terpisah untuk masing-masing siswa.
- Parameter pesan tetap mengacu pada nama masing-masing siswa agar pesan yang dikirim spesifik dan tidak tertukar.

---

## 6. Arsitektur & Spesifikasi AI

### 6.1 Desain Provider-Agnostic (Adapter Pattern)
Sistem backend EduNotify mengisolasi modul AI di belakang antarmuka terstandarisasi:

```typescript
interface AICompletionProvider {
  generateText(prompt: string, options?: AIOptions): Promise<string>;
  healthCheck(): Promise<boolean>;
}
```

Konfigurasi runtime dikontrol via `.env`:
- `AI_PROVIDER`: `9router` | `openai` | `anthropic` | `ollama`
- `AI_BASE_URL`: URL endpoint OpenAI-compatible (contoh: `http://127.0.0.1:20128/v1` untuk 9Router lokal)
- `AI_API_KEY`: Kredensial rahasia (disimpan aman di `.env`)
- `AI_MODEL_NAME`: Identifier model (contoh: `9router`, `gpt-4o-mini`, `qwen2.5:7b`)

### 6.2 Sanitasi & Privasi Data (Pseudonymization Guardrail)
Sebelum payload dikirimkan ke model LLM, data siswa wajib disanitasi:
- **Dilarang Dikirim**: NIS, NISN, Nama Lengkap Asli, Alamat Rumah, Nomor Telepon, Nama Orang Tua.
- **Diperbolehkan Dikirim**: ID Samaran (misal: `Siswa_A1`, `Siswa_B4`), Gender, Riwayat Kehadiran (array status per tanggal), Persentase Kehadiran, Hari Kejadian.
- Setelah LLM menghasilkan respons narasi, backend memetakan kembali ID Samaran ke Nama Siswa di sisi presentasi dashboard untuk dibaca oleh Wali Kelas/Guru.

### 6.3 Rule Engine Deterministik (Early Warning System)
Indikator peringatan dini dihitung secara matematis oleh backend tanpa melibatkan LLM:

| Kode Indikator | Kriteria Pemicu (Deterministik) | Tingkat Urgensi | Tindakan yang Disarankan |
|---|---|:---:|---|
| `EWS_ALPA_STREAK` | Alpa $\ge$ 2 hari berturut-turut | **TINGGI** | Hubungi ortu hari ini; jadwalkan konfirmasi langsung. |
| `EWS_ALPA_MONTHLY` | Alpa akumulasi $\ge$ 3 hari dalam 30 hari kalender | **SEDANG** | Diskusi empat mata dengan siswa; catat kendala. |
| `EWS_DAY_PATTERN` | $\ge 70\%$ ketidakhadiran jatuh pada hari yang sama (misal: setiap Senin/Jumat) | **SEDANG** | Investigasi kendala spesifik hari tersebut bersama BK. |
| `EWS_TREND_DROP` | Persentase kehadiran turun $\ge 15\%$ dibandingkan bulan sebelumnya | **TINGGI** | Rapat koordinasi wali kelas dan guru BK. |

### 6.4 AI Recommendation & Narrative Engine
- **Input ke LLM**: Tabel statistik terverifikasi + kode indikator EWS aktif + rekap tren kelas.
- **Output dari LLM**:
  1. *Executive Summary*: 2–3 kalimat evaluasi kehadiran kelas dalam Bahasa Indonesia formal dan empatik.
  2. *Actionable Guidance*: Rekomendasi langkah pembinaan pendukung keputusan (bukan vonis hukuman).
- **Guardrail Output**: LLM diinstruksikan dalam *system prompt* untuk:
  - Dilarang mendiagnosis gangguan mental/fisik siswa.
  - Dilarang memberikan label negatif (*pemalas*, *bermasalah*, *nakal*).
  - Dilarang merekomendasikan sanksi fisik atau skorsing sepihak.

---

## 7. Model Data & Kebutuhan Entitas (Database Requirements)

Setiap tabel operasional **wajib** memiliki kolom `school_id` sebagai kunci isolasi multitenancy.

```
┌─────────────────────────────────────────────────────────────┐
│                       ENTITAS UTAMA                         │
│                                                             │
│  schools ──◄ users (admin, guru, wali_kelas, kepsek)        │
│    │                                                        │
│    ├──◄ academic_years ──◄ terms                            │
│    │                          │                             │
│    ├──◄ academic_calendars ───┘                             │
│    │                                                        │
│    ├──◄ classes ──◄ class_enrollments ──► students          │
│    │        │                                  │            │
│    │        └──◄ teaching_schedules            │            │
│    │                     │                     │            │
│    └──◄ attendance_sessions ──◄ attendance_records          │
│                  │                     │                    │
│                  │                     ├──◄ corrections     │
│                  │                     └──◄ follow_ups      │
│                  │                                          │
│                  └──◄ early_warning_logs                    │
└─────────────────────────────────────────────────────────────┘
```

### Kamus Entitas Pokok:
1. **`schools`**: `id`, `name`, `npsn`, `address`, `timezone`, `created_at`.
2. **`users`**: `id`, `school_id`, `name`, `email`, `password_hash`, `role`, `nip`, `phone`, `is_active`.
3. **`classes`**: `id`, `school_id`, `name`, `grade_level`, `academic_year_id`, `homeroom_teacher_id` (FK to users).
4. **`students`**: `id`, `school_id`, `nis`, `nisn`, `name`, `gender`, `guardian_name`, `guardian_phone`, `is_active`.
5. **`class_enrollments`**: `id`, `school_id`, `class_id`, `student_id`, `academic_year_id`.
6. **`academic_calendars`**: `id`, `school_id`, `date`, `day_type` (`ACTIVE_KBM`, `HOLIDAY`, `SPECIAL_EVENT`), `description`.
7. **`teaching_schedules`**: `id`, `school_id`, `class_id`, `teacher_id`, `subject_name`, `day_of_week` (1-7), `period_order` (1, 2, 3..), `start_time`, `end_time`.
8. **`attendance_sessions`**: `id`, `school_id`, `class_id`, `date`, `submitted_by_teacher_id`, `status` (`DRAFT`, `SUBMITTED`, `UNCOMPLETED_ALERT`), `submitted_at`, `is_late_submission`. *(Unique key: school_id, class_id, date)*.
9. **`attendance_records`**: `id`, `school_id`, `session_id`, `student_id`, `status` (`UNRECORDED`, `PRESENT`, `SICK`, `PERMIT`, `ABSENT_ALPA`), `notes`.
10. **`attendance_corrections`**: `id`, `school_id`, `attendance_record_id`, `corrected_by_user_id`, `old_status`, `new_status`, `reason`, `created_at`.
11. **`attendance_follow_ups`**: `id`, `school_id`, `attendance_record_id`, `user_id` (wali kelas), `channel` (`WHATSAPP`), `status` (`CLICKED`, `MARKED_CONTACTED`), `notes`, `created_at`.
12. **`early_warning_logs`**: `id`, `school_id`, `student_id`, `indicator_code`, `severity`, `metric_snapshot_json`, `ai_narrative`, `created_at`.
13. **`audit_logs`**: `id`, `school_id`, `user_id`, `action`, `entity_type`, `entity_id`, `details_json`, `ip_address`, `created_at`.

---

## 8. User Stories & Acceptance Criteria (DoD)

### US-01: Presensi Estafet Guru Mapel
- **Sebagai** Guru Mata Pelajaran Jam ke-2.
- **Saya ingin** dapat mengisi presensi kelas jika Guru Jam ke-1 berhalangan hadir.
- **Agar** presensi resmi kelas tetap terisi tepat waktu tanpa menunggu proses manual yang rumit.
- **Kriteria Penerimaan (Acceptance Criteria)**:
  1. *Given* Kelas X-A belum memiliki data presensi tersimpan pada tanggal hari ini.
  2. *When* Guru Jam ke-2 membuka menu jadwal mengajarnya dan memilih Kelas X-A.
  3. *Then* Sistem menampilkan form presensi dengan seluruh siswa berstatus awal `Belum Diabsen`.
  4. *When* Guru Jam ke-2 selesai mengisi dan menekan "Simpan Presensi Resmi".
  5. *Then* Status sesi presensi menjadi `SUBMITTED`, tercatat nama guru pengisi, dan form terkunci untuk pengeditan biasa bagi guru jam ke-3 dan seterusnya.

### US-02: Tindak Lanjut Siswa Alpa via WhatsApp
- **Sebagai** Wali Kelas.
- **Saya ingin** melihat daftar siswa Alpa hari ini dan memiliki tombol langsung ke WhatsApp orang tua.
- **Agar** saya dapat mengonfirmasi alasan ketidakhadiran siswa dalam hitungan detik secara personal.
- **Kriteria Penerimaan**:
  1. *Given* Presensi hari ini telah disimpan dan terdapat 2 siswa berstatus `Alpa`.
  2. *When* Wali Kelas membuka dashboard kelasnya.
  3. *Then* Sistem menampilkan tabel siswa Alpa lengkap dengan nama orang tua, nomor kontak, dan tombol "Kirim WhatsApp".
  4. *When* Wali Kelas menekan tombol "Kirim WhatsApp".
  5. *Then* Sistem mencatat status intervensi menjadi `WhatsApp Dibuka` dan membuka tab baru mengarah ke `wa.me` dengan teks template yang sudah terisi otomatis sesuai identitas siswa.
  6. *When* Wali Kelas kembali ke dashboard dan mengklik "Tandai Sudah Dihubungi".
  7. *Then* Status ter-update menjadi `Ditandai Sudah Dihubungi` beserta timestamp audit.

### US-03: Peringatan Pukul 12.00 & Eskalasi Akhir Hari
- **Sebagai** Wali Kelas dan Admin Sekolah.
- **Saya ingin** menerima peringatan jika ada kelas yang belum diabsen hingga pukul 12.00 dan status eskalasi setelah KBM selesai.
- **Agar** tidak ada kelas yang terlewat untuk didata kehadirannya.
- **Kriteria Penerimaan**:
  1. *Given* Jam menunjukkan pukul 12.00 waktu lokal sekolah dan Kelas X-B belum memiliki sesi presensi `SUBMITTED`.
  2. *Then* Dashboard Admin dan Wali Kelas memunculkan banner peringatan kuning: *"Kelas X-B belum mengisi presensi per 12.00 WIB."*.
  3. *Given* Waktu telah melewati jam pelajaran terakhir di kalender akademik hari tersebut dan status masih belum diisi.
  4. *Then* Status sesi otomatis berubah menjadi `UNCOMPLETED_ALERT` dan ditandai merah pada monitoring Admin.

### US-04: Koreksi Presensi dengan Alasan Wajib
- **Sebagai** Wali Kelas.
- **Saya ingin** mengubah status siswa dari `Alpa` menjadi `Sakit` untuk absensi 2 hari yang lalu (H-2) setelah orang tua mengirim surat dokter.
- **Agar** data kehadiran siswa akurat dan sesuai dengan kondisi faktual.
- **Kriteria Penerimaan**:
  1. *Given* Presensi tercatat pada H-2.
  2. *When* Wali Kelas membuka riwayat presensi siswa tersebut dan memilih opsi "Koreksi Status".
  3. *Then* Sistem mewajibkan pengisian kolom "Alasan Koreksi" (minimal 10 karakter).
  4. *When* Formulir disubmit dengan alasan valid: "Orang tua melampirkan surat dokter via WA".
  5. *Then* Status aktif siswa berubah menjadi `Sakit`, dan tabel `attendance_corrections` mencatat riwayat perubahan (lama: Alpa, baru: Sakit, pelaku: Wali Kelas, timestamp, alasan).

### US-05: Analisis AI Deterministik & Privasi
- **Sebagai** Kepala Sekolah.
- **Saya ingin** membaca ringkasan naratif tentang tren kehadiran mingguan sekolah.
- **Agar** saya mendapat wawasan cepat tanpa harus membaca ratusan baris data tabel.
- **Kriteria Penerimaan**:
  1. *Given* Data kehadiran satu minggu telah dihitung secara deterministik oleh backend (tingkat kehadiran sekolah: 94.2%, kelas dengan Alpa tertinggi: XI-RPL 1).
  2. *When* Kepala Sekolah menekan tombol "Generate Ringkasan Mingguan AI".
  3. *Then* Backend mengirimkan statistik agregat tanpa PII ke model AI yang dikonfigurasi di `.env`.
  4. *Then* Model mengembalikan narasi ringkas dalam Bahasa Indonesia yang menyajikan angka faktual sesuai hitungan program dan memberikan 2–3 poin rekomendasi manajemen.

---

## 9. Penanganan Kasus Batas (Edge Cases)

1. **Dua Guru Mengisi Bersamaan**:
   - Jika Guru Jam 1 dan Guru Jam 2 sama-sama membuka form presensi saat jam pergantian, transaksi database dibatasi `SELECT ... FOR UPDATE` atau *Conditional Insert*. Pengirim kedua akan menerima pesan: *"Presensi telah disubmit oleh [Nama Guru Pertama]. Data Anda tidak disimpan untuk mencegah duplikasi."*.
2. **Hari Libur Dadakan / Tanggap Bencana**:
   - Admin dapat mengubah status hari di `academic_calendars` dari `ACTIVE_KBM` menjadi `HOLIDAY`.
   - Efek instan: Seluruh kelas pada hari tersebut dibebaskan dari kewajiban presensi, sistem tidak menembakkan warning pukul 12.00, dan metrik persentase kehadiran tidak menghitung hari tersebut sebagai pembagi (*denominator*).
3. **Satu Nomor Telepon untuk Lebih dari Satu Siswa**:
   - Skema kontak tidak menggunakan nomor telepon sebagai *unique identifier*.
   - Relasi data siswa ke kontak adalah relasi entitas terpisah, sehingga link WA tetap spesifik menyebutkan nama anak yang bersangkutan.
4. **Koreksi Melampaui Batas Waktu H-3**:
   - Tombol koreksi di dashboard Guru dan Wali Kelas dinonaktifkan (*disabled*) dengan tooltip: *"Koreksi lebih dari 3 hari yang lalu hanya dapat dilakukan oleh Admin Sekolah."*.
5. **Koneksi AI Putus / Provider Error**:
   - Jika endpoint AI mengalami *timeout* atau *connection error*, antarmuka dashboard tetap menyajikan 100% data tabel dan metrik EWS numerik.
   - Kotak narasi AI menampilkan fallback pesan ramah: *"Ringkasan AI sementara tidak tersedia. Data statistik di bawah tetap valid dan akurat."*. Sistem tidak boleh crash (*fail-safe*).

---

## 10. Persyaratan Non-Fungsional & Keamanan

1. **Isolasi Data (Multitenancy Readiness)**:
   - Setiap query data operasional wajib menyertakan filter `WHERE school_id = :current_user_school_id`.
   - Menggunakan *middleware/interceptor* di tingkat framework backend untuk menginjeksi `school_id` secara otomatis dari token autentikasi.
2. **Keamanan Autentikasi**:
   - Penyimpanan password menggunakan algoritma hashing modern (**Argon2id** atau **Bcrypt** dengan *cost factor* $\ge 12$).
   - Token JWT berumur pendek (*short-lived access token* 15–30 menit) + *HttpOnly, Secure, SameSite=Lax refresh token cookie*.
3. **Integritas Audit Log**:
   - Tabel `audit_logs` dan `attendance_corrections` bersifat *append-only*.
   - Tidak ada endpoint API atau antarmuka UI yang menyediakan operasi `UPDATE` atau `DELETE` pada tabel log riwayat.
4. **Efisiensi Sumber Daya VPS (2 vCPU / 4 GB RAM)**:
   - Backend dirancang *stateless* dan ringan (Node.js/TypeScript atau Python FastAPI/Go).
   - Penggunaan *connection pooling* database (PostgreSQL/SQLite terisolasi) agar tidak membebani memori server.
   - Panggilan LLM AI dibatasi *concurrency queue* (maksimal 1–2 request simultan) agar tidak menyebabkan lonjakan CPU pada server.

---

## 11. Roadmap Implementasi untuk Bagus (Implementation Handoff Phases)

Pekerjaan implementasi didelegasikan kepada Bagus melalui 6 milestone bertahap:

```text
Milestone 1: Fondasi Skema Basis Data & RBAC Multitenant (school_id)
      │
      ▼
Milestone 2: Manajemen Master Data & Kalender Akademik (Import CSV/Excel)
      │
      ▼
Milestone 3: Mesin Presensi Estafet & Proteksi Konkurensi
      │
      ▼
Milestone 4: Modul Monitoring Wali Kelas, WA Click-to-Chat & Koreksi Audit
      │
      ▼
Milestone 5: Rule-Engine Early Warning & Provider-Agnostic AI Service
      │
      ▼
Milestone 6: Dashboard Peran, Pelaporan Agregat & Ekspor PDF/Excel
```

---
*Dokumen ini adalah Baseline Spesifikasi Resmi Proyek EduNotify v1.0.0 dan tersimpan di repositori pengetahuan tim `second-brain`.*
