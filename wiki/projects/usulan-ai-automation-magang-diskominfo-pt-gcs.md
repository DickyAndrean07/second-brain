---
type: project-proposal
title: Usulan Proyek AI Automation Magang — Diskominfo Gresik vs PT GCS
created: 2026-11-05
updated: 2026-11-05
status: draft
tags:
  - magang
  - ai-automation
  - diskominfo-gresik
  - pt-gcs
  - web-dev
---

# 🚀 Usulan Proyek AI Automation Magang: Diskominfo Gresik vs PT GCS

Dokumen referensi eksplorasi usulan sistem berbasis **Web Development** dan **AI Automation** untuk kebutuhan magang/tugas khusus Mas Dicky (mahasiswa Teknik Informatika semester 7).

---

## 🎯 Konteks & Parameter Pemilihan

- **Profil Pengembang**: Sedang mendalami Web Development (Next.js, Drizzle ORM, PostgreSQL) dan AI Automation (LLM API via 9Router, Multimodal Vision, Agentic Workflow, Scraping/Worker).
- **Kondisi Lapangan**:
  - **PT Gresik Cipta Sejahtera (PT GCS)**: Sudah berstatus diterima. Perusahaan bergerak di bidang perdagangan, distribusi, dan logistik pupuk, bahan kimia, serta gas industri di lingkungan Petrokimia Gresik Group.
  - **Diskominfo Kabupaten Gresik**: Instansi pengelola domain `gresikkab.go.id`, pusat data daerah, jaringan SPBE, dan persandian/keamanan siber (CSIRT) tingkat kabupaten.
- **Tujuan**: Membangun sistem yang terpakai riil, memiliki nilai jual portofolio tinggi, dan selaras dengan target pembelajaran AI Automation.

---

## 🏛️ Usulan Proyek AI Automation — Diskominfo Kabupaten Gresik

### 📌 Judul Proposal Resmi & Kegiatan SEPEKAN
> **"PENERAPAN AI AUTOMATION UNTUK OPTIMALISASI LAYANAN DIGITAL DAN MONITORING KEAMANAN SPBE PADA DINAS KOMUNIKASI DAN INFORMATIKA KABUPATEN GRESIK"**
- **Fungsi**: Digunakan pada kolom form *Judul Kegiatan* portal SEPEKAN Bappeda Gresik dan sampul dokumen proposal magang/PKL.
- **Cakupan Payung**: Mengakomodasi 2 pilar kebutuhan utama Diskominfo: Optimalisasi Layanan Digital (Aptika / Lapor GUS & Service Desk) serta Monitoring Keamanan SPBE (Persandian / CSIRT Subdomain Guard).

### 1. AI Subdomain Guard & Visual Deface Inspector (Cybersecurity AI) ⭐ [Rekomendasi Utama]
- **Latar Belakang Masalah**:
- Subdomain OPD Pemkab Gresik kerap menjadi sasaran empuk peretasan *Black Hat SEO* judi online karena memiliki otoritas domain (`.go.id`) tinggi.
- Peretas menggunakan teknik *conditional cloaking*: pengunjung manual melihat tampilan web normal, sedangkan Googlebot disuguhi halaman promosi slot/judi.
- Pengecekan manual terhadap puluhan subdomain memakan waktu dan sering luput dari pengawasan Tim CSIRT/Persandian.
- **Bukti Empiris Lapangan (Live Findings)**:
  1. `geodatabase.gresikkab.go.id` — Terinjeksi cloaking slot PONTI4D (meta title/desc dan link luar `geodata.pafigressikab.com` terbaca Googlebot).
  2. `desadoudo.gresikkab.go.id/assets/import/excel` — Injeksi parameter URL spam slot & konten dewasa.
  3. `kelurahanpekelingan.gresikkab.go.id` — Spam post phishing/scam keuangan (Indodax fake CS).
  4. `dispendik.gresikkab.go.id` — Kebocoran error fatal PHP dan path file server (`/opt/lampp/htdocs/`).
  5. `data.gresikkab.go.id` — Misfortune konfigurasi (default page "Welcome to CentOS").
  6. `testing-jdih.gresikkab.go.id` — Subdomain staging/testing bocor dan terindeks di Google publik tanpa proteksi auth.
- **Arsitektur & Fitur AI**:
  - **Dual-Mode Headless Crawler**: Worker background (cron) melakukan inspeksi berkala dengan dua User-Agent (browser umum vs Googlebot).
  - **Multimodal Visual & Semantic Inspector**: Screenshot halaman web dianalisis menggunakan Multimodal LLM (Gemini Flash Vision via 9Router) bersamaan dengan ekstraksi meta tag untuk mendeteksi deface visual maupun teks judi tersamar yang lolos dari regex.
  - **SSL & Uptime Monitoring**: Pengecekan status HTTP (200/500/timeout) dan masa berlaku sertifikat SSL/TLS.
  - **Incident Report & Alert Dispatcher**: Bot Telegram CSIRT mengirimkan alert darurat otomatis disertai ringkasan analisis ancaman ketika anomali terdeteksi.
- **Tech Stack**: Next.js (Dashboard Admin), Playwright/Puppeteer, PostgreSQL, Drizzle ORM, 9Router (Gemini Flash Vision), Telegram Bot API.

### 2. AI Intake & Triage Assistant Lapor GUS — Service Desk Bridge (Human-in-the-Loop Web Dashboard) ⭐ [Rekomendasi Utama Presentasi]
- **Latar Belakang Masalah & Kebutuhan Akademik**:
  - Portal `servicedesk.gresikkab.go.id` mewajibkan registrasi akun, verifikasi email, dan form berbelit yang enggan digunakan warga.
  - Warga memilih chat WhatsApp (Lapor GUS / GoWA) dengan pesan informal, tidak lengkap, dan tertimbun saat jam kerja berakhir.
  - Tugas Khusus kampus mewajibkan output aplikasi **berbentuk Web minimal CRUD**.
- **Arsitektur Sistem (Next.js Web Dashboard + WA AI Gateway)**:
  - **Pintu Masuk Warga**: Chat WhatsApp interaktif memandu warga melengkapi data (lokasi, foto, rincian keluhan).
  - **AI Parser & Router Engine**: Mengekstrak data tidak berstruktur menjadi JSON baku dan mengklasifikasikan dinas (OPD) tujuan.
  - **Web Dashboard Triage (CRUD Akademik)**:
    - **Create**: Tiket aduan masuk otomatis dari webhook WA/AI ke database PostgreSQL, serta form input manual jika warga melapor via telepon/kantor.
    - **Read**: Tabel antrean aduan interaktif lengkap dengan filter dinas, status disposisi, dan tingkat urgensi (Tinggi/Sedang/Rendah).
    - **Update**: Editor draf aduan sebelum disahkan, penandaan status (`Draf` ➔ `Di-input ke Service Desk` ➔ `Selesai`), serta input nomor tiket resmi.
    - **Delete**: Fitur arsip/hapus untuk menyaring spam, ujaran kebencian, atau aduan duplikat.
  - **Fitur Human-in-the-Loop (Jembatan Aman ke Service Desk)**:
    - Dilengkapi tombol **One-Click Copy per Field** (`[ 📋 ]`) pada dashboard (Subjek, Dinas, Deskripsi Terstruktur) untuk memudahkan admin menyalin-tempel ke form terpisah `servicedesk.gresikkab.go.id` tanpa re-typing manual dan tanpa risiko menyentuh database produksi dinas.
- **Tech Stack**: Next.js (App Router), Tailwind CSS, PostgreSQL, Drizzle ORM, Node.js / Baileys (WA), 9Router (Gemini Flash).

### 3. AI WhatsApp Assistant Pelayanan Terpadu & PPID (Agentic RAG)
- **Latar Belakang Masalah**:
  - Pertanyaan berulang mengenai persyaratan berkas adminduk, izin usaha, SOP dinas, dan pengajuan informasi publik membebani admin dinas.
- **Arsitektur & Fitur AI**:
  - Bot WhatsApp interaktif berbasis RAG (Retrieval-Augmented Generation).
  - Mengambil rujukan dari korpus dokumen regulasi, Perbup, dan SOP pelayanan Pemkab Gresik.
  - Menyediakan jawaban interaktif dalam bahasa Indonesia santai lengkap dengan sitasi pasal dan link unduh berkas formulir resmi.
- **Tech Stack**: Node.js / Baileys, PostgreSQL (pgvector) / Vector DB, 9Router (LLM Agent).

### 4. AI Validator Metadata "Satu Data Gresik"
- **Latar Belakang Masalah**:
  - OPD mengunggah dataset statistik sektoral dalam format tabular (Excel/CSV) yang sering tidak memenuhi standar metadata Satu Data Indonesia (SDI).
- **Arsitektur & Fitur AI**:
  - Validasi cerdas format tabel, tipe data kolom, dan kelengkapan deskripsi metadata.
  - Rekomendasi perbaikan otomatis bagi admin OPD sebelum data dipublikasikan ke portal Satu Data.
- **Tech Stack**: Next.js, Python Data Parser, LLM Schema Extraction.

---

## 🏭 Usulan Proyek AI Automation — PT Gresik Cipta Sejahtera (PT GCS)

### 1. AI Document Parser Surat Jalan & Delivery Order Fisik (OCR + LLM) ⭐ [Rekomendasi Utama]
- **Latar Belakang Masalah**:
  - Alur logistik distribusi pupuk dan bahan kimia melibatkan ribuan dokumen fisik: Surat Jalan, Delivery Order (DO), dan faktur dari sopir truk armada.
  - Input manual memakan waktu staf administrasi gudang dan rawan *human error* pada nomor seri DO atau tonase muatan.
- **Arsitektur & Fitur AI**:
  - Upload foto/scan lembar DO ke portal web.
  - Pipeline OCR + Vision LLM mengekstrak entitas penting secara terstruktur ke JSON: Nomor DO, nama kios/pabrik tujuan, jenis pupuk/kimia, kuantum (ton/karung), nama sopir, plat nomor armada.
  - Sinkronisasi otomatis ke basis data PostgreSQL internal.
- **Tech Stack**: Next.js, Tesseract / PaddleOCR, Gemini Flash (Vision Parsing via 9Router), PostgreSQL.

### 2. AI WhatsApp Agent Tracking Distribusi & Ketersediaan Stok
- **Latar Belakang Masalah**:
  - Kios pengecer dan pabrik rekanan terus-menerus menghubungi tim penjualan hanya untuk menanyakan posisi pengiriman armada atau ketersediaan stok pupuk tertentu.
- **Arsitektur & Fitur AI**:
  - Bot WhatsApp conversational bertenaga LLM Tool Calling.
  - Menghubungkan bahasa natural pengguna dengan query basis data sistem inventori & logistik PT GCS.
  - Menjawab status perjalanan DO dan sisa kuota stok gudang secara otomatis 24/7.
- **Tech Stack**: Node.js (Baileys / WA Cloud API), LLM Function Calling, PostgreSQL.

### 3. AI Rekonsiliasi & Deteksi Anomali Slip Timbangan Truk
- **Latar Belakang Masalah**:
  - Truk pengangkut pupuk curah/cair atau gas industri rentan mengalami kebocoran, susut berlebih, atau manipulasi saat transit antara pabrik produsen dan gudang transit GCS.
- **Arsitektur & Fitur AI**:
  - Parser cerdas membaca slip timbangan bruto/tara/netto pabrik awal dan gudang tujuan.
  - Deteksi anomali otomatis berbasis aturan deviasi toleransi (>0.5%); menghasilkan draf tiket investigasi audit otomatis ke bagian operasional jika ditemukan ketidaksesuaian berat.
- **Tech Stack**: Next.js, Python Anomaly Worker, PostgreSQL.

### 4. AI Customer Support & Logistik Dispatcher Otomatis
- **Latar Belakang Masalah**:
  - Komplain terkait keterlambatan pengiriman armada atau kendala mutu kemasan pupuk sering tercecer di riwayat obrolan admin.
- **Arsitektur & Fitur AI**:
  - Analisis keluhan pelanggan via email/WA, klasifikasi prioritas armada, penerbitan tiket kendala ke staf armada terkait, dan saran draf tanggapan otomatis untuk ditinjau sebelum dikirim ke pelanggan.
- **Tech Stack**: Next.js, LLM Classifier, PostgreSQL.

---

## ⚖️ Matriks Perbandingan Strategis

| Parameter | Diskominfo Gresik (AI Subdomain Guard) | PT GCS (AI DO Parser / WA Agent) |
| :--- | :--- | :--- |
| **Status Approval** | Belum ada kepastian (perlu pengajuan surat) | **Sudah diterima** |
| **Urgensi Kebutuhan** | **Sangat Tinggi** (insiden peretasan judol live) | Sedang - Tinggi (efisiensi operasional gudang) |
| **Peluang Terpakai Riil** | Sangat besar (diadopsi CSIRT/SPBE) | Besar (jika belum tercakup ERP SAP holding) |
| **Kesesuaian Waktu (Skripsi/Warung)** | Ritme kerja fleksibel, waktu leluasa | Ritme industri logistik lebih padat |
| **Portofolio AI & Web** | Full-stack Next.js + Security AI Worker | Full-stack Next.js + Document/Vision AI Parser |

---

## 🗣️ Panduan Diskusi & Skrip Validasi Lapangan (Pintu Masuk Mentor Diskominfo)

Strategi komunikasi tatap muka: **Posisikan Diri Ingin Belajar & Meminta Arahan ➔ Validasi Alur/SOP Lapangan ➔ Sambut dengan Solusi Prototipe Konkret**. Jangan menggurui atau langsung menuduh sistem dinas memiliki kelemahan.

### 🚪 Etika & Skrip Pembuka Pertama Kali Masuk Ruangan (Ice Breaking Rendah Hati)
> *"Selamat pagi/siang Pak. Mohon izin memperkenalkan diri, saya Dicky dan ini rekan saya Bagus dari Prodi Teknik Informatika Universitas Muhammadiyah Gresik.*
> 
> *Tujuan kedatangan kami ke sini ingin bersilaturahmi sekaligus memohon izin untuk melaksanakan Praktek Kerja Lapangan (PKL) di Diskominfo Gresik. Di dalam proposal, kami sudah menyusun beberapa rancangan inisiatif awal berbasis web development dan automasi AI.*
> 
> *Namun sebelum melangkah lebih jauh, **kami ingin sowan dan memohon bimbingan serta konfirmasi dari Bapak terlebih dahulu**, sekiranya bidang atau program mana yang saat ini paling relevan dan menjadi prioritas kebutuhan dinas, agar apa yang kami pelajari dan bangun nanti benar-benar memberikan manfaat nyata."*

### Skenario 1 — Jalur Keamanan Siber & Subdomain (Bidang Persandian / CSIRT)
1. **Pertanyaan Pembuka (Eksplorasi Alur)**:
   > *"Pak, saya izin konfirmasi terkait alur di Pemkab. Kalau ada website atau subdomain OPD yang mengalami peretasan, deface, atau kendala server, itu biasanya dinas terkait yang melapor ke Diskominfo, atau memang dari tim CSIRT sini yang rutin memonitoring puluhan subdomain tersebut?"*
2. **Respon Masuk Solusi (Pivot to Proposal)**:
   - Begitu mentor menjelaskan keterbatasan pemantauan manual:
   > *"Pas sekali Pak. Kebetulan saya sempat menganalisis dan menemukan beberapa subdomain terindikasi injeksi cloaking SEO tersembunyi. Dari situ saya mengajukan inisiatif: bagaimana jika kami buatkan **crawler otomatis berkala (Dual-Mode Client vs Bot) terintegrasi AI Vision**, sehingga jika terdeteksi anomali atau deface, notifikasi langsung dikirimkan ke Telegram tim teknis Diskominfo sebelum dampak menyebar luas."*

### Skenario 2 — Jalur Layanan Publik & Aduan Warga (Bidang Aptika / IKP)
1. **Pertanyaan Pembuka (Eksplorasi Alur)**:
   > *"Pak, terkait kanal pengaduan masyarakat seperti Lapor GUS dan GoWA, apakah alur pengelolaannya terpusat di bawah Diskominfo sampai proses penerbitan tiket di portal Service Desk?"*
2. **Respon Masuk Solusi (Pivot to Proposal)**:
   - Begitu mentor menjelaskan alur rekap dan beban verifikasi chat manual admin:
   > *"Menarik sekali Pak. Saya sempat mencoba kanal tersebut, dan melihat peluang otomasi saat jam kerja kantor berakhir. Rencana kami di proposal ingin membangun **Web Dashboard Triage terintegrasi WhatsApp AI Assistant**. Pesan warga dirapikan otomatis oleh AI, dinas tujuannya terklasifikasi, dan admin tinggal menggunakan fitur salin satu-klik (one-click copy) ke portal Service Desk tanpa risiko mengubah database produksi dinas."*

---

## 📌 Rekomendasi Eksekusi
1. **Amankan PT GCS**: Jangan tolak penerimaan PT GCS terlebih dahulu sebelum ada kepastian hitam di atas putih dari Diskominfo.
2. **Pengajuan ke Diskominfo**: Bawa proposal ringkas 1-2 lembar berbasis usulan **AI Subdomain Guard** (menyertakan bukti live temuan cloaking judol di domain Pemkab) langsung ke bagian SPBE/Persandian.
3. **Pilihan Final**: Jika Diskominfo menyetujui dalam tenggat waktu konfirmasi PT GCS, ambil Diskominfo; jika berbelit-belit atau kuota penuh, ambil PT GCS dengan mengajukan sistem AI Document Parser.
