---
type: project-tasks
title: "Paket Task Implementasi EduNotify MVP (Handoff untuk Bagus)"
project: "EduNotify"
version: "1.0.0"
status: "READY_FOR_HANDOFF"
created: 2026-10-22
updated: 2026-10-22
author: "Diva (Product & System Analyst)"
target_builder: "Bagus (Builder Agent)"
governance_reference: "AGENTS.md"
prd_reference: "[[wiki/projects/edunotify-prd.md]]"
---

# 📦 Paket Task Implementasi EduNotify MVP (Bagus Handoff)

Dokumen ini mendefinisikan 6 task Kanban resmi untuk implementasi EduNotify MVP oleh **Bagus (`web-dev-bagus`)** sesuai aturan tata kelola di `AGENTS.md`.

---

## 🗺️ Peta Dependensi Antartask

```text
[EDUNOTIFY-01: Fondasi, DB Drizzle & RBAC]
         │
         ▼
[EDUNOTIFY-02: Master Data & Kalender Akademik]
         │
         ▼
[EDUNOTIFY-03: Mesin Presensi Estafet & Konkurensi]
         │
         ▼
[EDUNOTIFY-04: Monitoring Wali Kelas, WA Click-to-Chat & Koreksi Audit]
         │
         ▼
[EDUNOTIFY-05: Rule-Engine EWS & Provider-Agnostic AI Service]
         │
         ▼
[EDUNOTIFY-06: Dashboard Peran, Pelaporan & Ekspor PDF/Excel]
```

---

## 📋 Detail Spesifikasi Task Kanban

---

### [EDUNOTIFY-01]: Inisialisasi Proyek, Skema Database Drizzle Multitenant & Autentikasi RBAC

- **Tujuan**: Membangun fondasi aplikasi fullstack Next.js App Router, migrasi skema database PostgreSQL menggunakan Drizzle ORM dengan dukungan isolasi multitenant (`school_id`), serta sistem autentikasi email/password dengan otorisasi RBAC (Admin Sekolah, Guru Mapel, Wali Kelas, Kepala Sekolah).
- **Workspace**: `/home/ubuntu/edunotify`
- **Repository**: `edunotify`
- **Target Branch**: `bagus/edunotify-01-foundation-db-auth`
- **Referensi PRD**: Bab 1 (Prinsip Desain), Bab 2 (RBAC), Bab 7 (Model Data), Bab 10 (Keamanan)
- **Dependensi**: Tidak ada (Task Fondasi Pertama).
- **File Boleh Diubah**:
  - `package.json`, `tsconfig.json`, `tailwind.config.ts`, `postcss.config.mjs`
  - `src/db/**/*` (skema Drizzle, koneksi DB, migrasi)
  - `src/lib/auth/**/*` (hashing password Argon2id/Bcrypt, session/JWT, token verification)
  - `src/middleware.ts` (RBAC route protection)
  - `src/app/(auth)/**/*` (halaman & server action login/logout)
  - `tests/auth/**/*`, `tests/db/**/*`
- **File Dilarang Diubah**: `.env` (hanya boleh membuat `.env.example`), branch `main`.
- **Kriteria Selesai (DoD)**:
  1. Proyek Next.js App Router dengan TypeScript dan Tailwind CSS terinisialisasi bersih.
  2. Seluruh tabel inti (`schools`, `users`, `classes`, `students`, `academic_years`, `academic_calendars`, `teaching_schedules`, `attendance_sessions`, `attendance_records`, `attendance_corrections`, `attendance_follow_ups`, `early_warning_logs`, `audit_logs`) terdefinisi di skema Drizzle dan memiliki kolom `school_id`.
  3. Script migrasi dan seeder awal berjalan sukses (1 dummy school, 4 user uji coba untuk tiap peran).
  4. Autentikasi login berhasil memvalidasi kredensial, menghasilkan session/cookie aman, dan middleware me-redirect user sesuai hak akses rolenya.
  5. Password tersimpan dalam bentuk hash aman, bukan plaintext.
- **Cara Pengujian**:
  - **Unit Test**: Test hashing password, verifikasi JWT/session, dan isolasi query `school_id`.
  - **Smoke Test**: Login berhasil untuk 4 peran berbeda dan ditolak untuk kredensial salah.
- **Batasan Keamanan**:
  - Dilarang menyimpan credential atau password plaintext di kode/seeder.
  - Session cookie wajib diset `HttpOnly`, `SameSite=Lax`.

---

### [EDUNOTIFY-02]: Modul Master Data Sekolah & Kalender Akademik (Import CSV/Excel)

- **Tujuan**: Membangun modul manajemen data siswa, guru, kelas/rombel, jadwal mengajar mingguan, kalender akademik (hari belajar aktif & hari libur), serta parser impor data massal via CSV/Excel dengan validasi duplikasi.
- **Workspace**: `/home/ubuntu/edunotify`
- **Repository**: `edunotify`
- **Target Branch**: `bagus/edunotify-02-master-data-calendar`
- **Referensi PRD**: Bab 3.1 (Poin 2), Bab 7 (Entitas), Bab 8 (US-01/03)
- **Dependensi**: `EDUNOTIFY-01`
- **File Boleh Diubah**:
  - `src/app/(dashboard)/admin/**/*`
  - `src/lib/importers/**/*` (parser CSV/Excel, schema validator)
  - `src/services/masterDataService.ts`
  - `src/components/master-data/**/*`
  - `tests/importers/**/*`, `tests/services/masterData.test.ts`
- **File Dilarang Diubah**: `src/lib/auth/**/*`, `.env`, branch `main`.
- **Kriteria Selesai (DoD)**:
  1. Halaman CRUD Siswa, Guru, dan Kelas berfungsi penuh dengan filter pencarian dan paginasi.
  2. Input jadwal pelajaran mingguan memetakan Kelas, Hari, Jam Mulai/Selesai, Mapel, dan Guru Pengampu.
  3. Kalender akademik dapat menandai tanggal sebagai `ACTIVE_KBM`, `HOLIDAY`, atau `SPECIAL_EVENT`.
  4. Fitur impor file CSV/Excel siswa & guru berjalan dengan validasi duplikasi NIS/NIP; jika ada data duplikat, tampilkan daftar baris yang error secara transparan tanpa merusak database.
- **Cara Pengujian**:
  - **Unit Test**: Parser CSV/Excel dengan file uji valid dan file uji corrupt/duplikat.
  - **Visual Check**: Form input jadwal responsif dan kalender akademik menampilkan hari libur dengan visual jelas.
- **Batasan Keamanan**:
  - Validasi tipe file upload (hanya mime type `.csv`, `.xlsx`).
  - Sanitasi input string untuk mencegah XSS pada nama siswa/guru.

---

### [EDUNOTIFY-03]: Mesin Presensi Estafet & Proteksi Konkurensi Backend

- **Tujuan**: Mengimplementasikan logika presensi harian berbasis jadwal pelajaran dengan validasi backend ketat (guru terdaftar, jam mengajar aktif), proteksi konkurensi (atomic save & idempotency), trigger warning pukul 12.00, serta penanganan kelas belum diabsen di akhir hari KBM.
- **Workspace**: `/home/ubuntu/edunotify`
- **Repository**: `edunotify`
- **Target Branch**: `bagus/edunotify-03-relay-attendance-engine`
- **Referensi PRD**: Bab 3.1 (Poin 3), Bab 4.1 & 4.2, Bab 8 (US-01 & US-03), Bab 9 (Edge Cases 1 & 2)
- **Dependensi**: `EDUNOTIFY-01`, `EDUNOTIFY-02`
- **File Boleh Diubah**:
  - `src/app/(dashboard)/teacher/**/*`
  - `src/services/attendanceService.ts`
  - `src/app/api/attendance/**/*`
  - `src/components/attendance/**/*`
  - `tests/services/attendance.test.ts`
- **File Dilarang Diubah**: `src/lib/auth/**/*`, `src/lib/importers/**/*`, branch `main`.
- **Kriteria Selesai (DoD)**:
  1. Siswa otomatis terinisialisasi `Belum Diabsen` pada hari aktif.
  2. Backend memvalidasi otorisasi guru secara server-side: hanya guru yang memiliki jadwal di kelas tersebut pada hari itu yang dapat mengabsen.
  3. Alur estafet berfungsi: Guru jam ke-2 dapat mengisi jika jam ke-1 belum mengisi; setelah sesi berstatus `SUBMITTED`, guru jam berikutnya hanya dapat melihat (*read-only*).
  4. Proteksi konkurensi database: Percobaan submit kedua secara paralel ditolak dengan error ramah (mencegah *race condition* dan data duplikat).
  5. Perhitungan status warning pukul 12.00 dan eskalasi akhir hari (`UNCOMPLETED_ALERT`) berjalan deterministik.
  6. Pengisian susulan setelah jam sekolah mencatat `is_late_submission = true`.
- **Cara Pengujian**:
  - **Unit Test**: Test otorisasi estafet jam 1 vs jam 2, simulasi submit ganda konkuren (race condition test), dan penolakan presensi di hari libur.
  - **Browser Check**: Form presensi guru responsif di mobile/desktop dengan tombol radio/toggle status Hadir, Sakit, Izin, Alpa.
- **Batasan Keamanan**:
  - Otorisasi guru WAJIB divalidasi di backend lewat session ID pengguna, bukan sekadar mempercayai `teacher_id` di request body.

---

### [EDUNOTIFY-04]: Monitoring Wali Kelas, WhatsApp Click-to-Chat & Koreksi Audit Trail

- **Tujuan**: Membangun dashboard Wali Kelas untuk memantau presensi kelas binaan, filter instan siswa Alpa, generator tautan WhatsApp Click-to-Chat (`wa.me`) manual dengan penanganan nomor kontak multi-siswa, state tracking intervensi, serta modal koreksi presensi berjenjang dengan audit log terenkapsulasi.
- **Workspace**: `/home/ubuntu/edunotify`
- **Repository**: `edunotify`
- **Target Branch**: `bagus/edunotify-04-homeroom-wa-corrections`
- **Referensi PRD**: Bab 3.1 (Poin 4 & 5), Bab 4.3 (Matriks Koreksi), Bab 5 (Integrasi WA), Bab 8 (US-02 & US-04)
- **Dependensi**: `EDUNOTIFY-03`
- **File Boleh Diubah**:
  - `src/app/(dashboard)/homeroom/**/*`
  - `src/services/whatsappService.ts`
  - `src/services/correctionService.ts`
  - `src/components/homeroom/**/*`
  - `tests/services/whatsapp.test.ts`, `tests/services/correction.test.ts`
- **File Dilarang Diubah**: `src/services/attendanceService.ts` (kecuali penambahan hook koreksi), branch `main`.
- **Kriteria Selesai (DoD)**:
  1. Dashboard Wali Kelas menampilkan kartu rekap kehadiran kelas hari ini dan daftar siswa Alpa.
  2. Tombol "Kirim WhatsApp" menghasilkan tautan `https://wa.me/{phone}?text={encoded}` sesuai template resmi PRD.
  3. Status intervensi berubah dari `Belum Dibuka` ➔ `WhatsApp Dibuka` saat tautan diklik, dan dapat diubah menjadi `Ditandai Sudah Dihubungi` melalui tombol manual.
  4. Terdapat teks bantuan jelas bahwa membuka WA bukan bukti pesan telah terkirim.
  5. Multi-siswa satu nomor kontak menghasilkan kartu terpisah dengan nama siswa yang sesuai di template pesan.
  6. Form koreksi menerapkan aturan RBAC: Hari H (Guru/Wali Kelas), H-1 s/d H-3 (Hanya Wali Kelas), > H-3 (Hanya Admin). Kolom alasan koreksi wajib diisi (min. 10 karakter).
  7. Riwayat koreksi tercatat lengkap di tabel `attendance_corrections` (data lama tidak dihapus).
- **Cara Pengujian**:
  - **Unit Test**: Generator URL `wa.me` (sanitasi nomor 08 ke 628, encoding karakter spasi/baris baru), validasi batas tanggal koreksi RBAC.
  - **Visual Check**: Klik tombol WA membuka tab baru dengan URL benar; modal koreksi menampilkan error jika alasan kosong.
- **Batasan Keamanan**:
  - Tidak ada integrasi bot/API WhatsApp otomatis; murni URL generator di client.
  - Validasi ketat otorisasi wali kelas pada kelas binaannya.

---

### [EDUNOTIFY-05]: Rule-Engine Early Warning Deterministik & Provider-Agnostic AI Service

- **Tujuan**: Membangun *Rule Engine* matematis untuk menghitung metrik Early Warning System (Alpa beruntun, Alpa bulanan, pola hari, drop tren) dengan proteksi *cold-start* (minimal 14 hari aktif), serta modul AI service *provider-agnostic* (dukungan 9Router, OpenAI, Ollama via `.env`) yang dilengkapi sanitasi data (minimisasi data & pseudonymization) untuk menghasilkan narasi insight dan rekomendasi non-punitif.
- **Workspace**: `/home/ubuntu/edunotify`
- **Repository**: `edunotify`
- **Target Branch**: `bagus/edunotify-05-ews-ai-service`
- **Referensi PRD**: Bab 3.1 (Poin 6), Bab 6 (Arsitektur AI & EWS), Bab 8 (US-05)
- **Dependensi**: `EDUNOTIFY-03`, `EDUNOTIFY-04`
- **File Boleh Diubah**:
  - `src/services/earlyWarningService.ts`
  - `src/lib/ai/**/*` (AI provider interface, adapter 9router/openai/ollama, prompt builder, data sanitizer)
  - `src/components/early-warning/**/*`
  - `tests/services/earlyWarning.test.ts`, `tests/lib/ai/sanitizer.test.ts`
- **File Dilarang Diubah**: `src/lib/auth/**/*`, `src/services/whatsappService.ts`, branch `main`.
- **Kriteria Selesai (DoD)**:
  1. *Rule Engine* backend menghitung 4 kode EWS (`EWS_ALPA_STREAK`, `EWS_ALPA_MONTHLY`, `EWS_DAY_PATTERN`, `EWS_TREND_DROP`) secara 100% deterministik.
  2. Siswa dengan data historis < 14 hari aktif tidak memicu peringatan pola/tren (menghindari alarm palsu).
  3. Modul AI mengimplementasikan antarmuka `AICompletionProvider` yang dikonfigurasi melalui environment variable.
  4. Fungsi sanitasi data menghapus seluruh PII (Nama Asli, NIS, No Telp, Catatan Bebas) sebelum payload dikirim ke AI; ID samaran dipetakan kembali secara lokal saat render UI.
  5. Prompt AI berisi larangan keras mendiagnosis kondisi medis/mental atau memberi label negatif kepada siswa.
  6. Antarmuka UI menampilkan kartu rekomendasi tindak lanjut dan memiliki *fallback fail-safe* jika koneksi AI terputus.
  7. Payload AI dan response tidak bocor ke dalam error log aplikasi.
- **Cara Pengujian**:
  - **Unit Test**: Perhitungan matematis EWS dengan mock dataset absensi, uji sanitasi data PII (memastikan tidak ada string nama asli di payload prompt), mock response AI adapter.
  - **Smoke Test**: Toggle switch provider via mock `.env` dan verifikasi fallback UI saat API AI error/offline.
- **Batasan Keamanan**:
  - Masking API key di log aplikasi.
  - Batasi antrean request AI (concurrency limit) agar tidak membebani CPU VPS.

---

### [EDUNOTIFY-06]: Dashboard Peran, Pelaporan Agregat Sekolah & Ekspor PDF/Excel

- **Tujuan**: Membangun dashboard eksekutif Kepala Sekolah dan Admin Sekolah, tabel pelaporan presensi dengan filter multi-dimensi (tanggal, kelas, siswa, status), generator dokumen ekspor Excel (.xlsx) dan PDF siap cetak, serta verifikasi integrasi sistem secara end-to-end.
- **Workspace**: `/home/ubuntu/edunotify`
- **Repository**: `edunotify`
- **Target Branch**: `bagus/edunotify-06-dashboards-reports-export`
- **Referensi PRD**: Bab 2.2, Bab 3.1 (Poin 7), Bab 8 (Semua User Stories), Bab 10 & 11
- **Dependensi**: `EDUNOTIFY-01` s/d `EDUNOTIFY-05`
- **File Boleh Diubah**:
  - `src/app/(dashboard)/principal/**/*`
  - `src/app/(dashboard)/admin/reports/**/*`
  - `src/services/reportService.ts`
  - `src/lib/exporters/**/*` (generator Excel & PDF)
  - `src/components/reports/**/*`, `src/components/charts/**/*`
  - `tests/e2e/**/*` atau `tests/integration/**/*`
- **File Dilarang Diubah**: Core logic database dan auth (`src/db/**/*`, `src/lib/auth/**/*`), branch `main`.
- **Kriteria Selesai (DoD)**:
  1. Dashboard Kepala Sekolah menyajikan grafik persentase kehadiran sekolah, perbandingan antarkelas, dan kartu ringkasan eksekutif AI.
  2. Dashboard Admin menampilkan indikator kelengkapan presensi harian seluruh kelas.
  3. Halaman Laporan menyediakan filter: Rentang Tanggal, Kelas, Siswa, dan Status Kehadiran.
  4. Ekspor Excel menghasilkan file `.xlsx` dengan format tabel rapi, header sekolah, dan formula persentase kehadiran yang valid.
  5. Ekspor PDF menghasilkan dokumen cetak rekap presensi resmi dengan kop sekolah dan layout tabel proporsional.
  6. Seluruh alur end-to-end (Admin setup data ➔ Guru absen estafet ➔ Wali kelas tindak lanjut WA ➔ EWS trigger ➔ Laporan diekspor) teruji lancar.
- **Cara Pengujian**:
  - **Unit Test**: Generator file Excel dan PDF menghasilkan output byte buffer valid.
  - **Visual & Smoke Test**: Pengujian tampilan dashboard di layar desktop dan mobile; verifikasi unduhan file Excel dan PDF.
- **Batasan Keamanan**:
  - Proteksi query ekspor: membatasi rentang tanggal wajar (maksimal 1 tahun ajaran per unduhan) untuk mencegah memori server habis (*Denial of Service / OOM*).

---
*Paket Task Implementasi ini disusun oleh Diva dan siap dieksekusi secara bertahap oleh Bagus via Hermes Kanban.*
