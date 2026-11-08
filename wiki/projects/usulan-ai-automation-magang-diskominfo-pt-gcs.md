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

### 2. AI Intake & Triage Assistant Lapor GUS — Service Desk Bridge (Human-in-the-Loop) ⭐ [Rekomendasi Utama Presentasi]
- **Latar Belakang Masalah**:
  - Portal `servicedesk.gresikkab.go.id` mewajibkan registrasi akun, verifikasi email, dan form panjang yang rumit bagi warga awam.
  - Warga memilih chat WhatsApp (Lapor GUS / GoWA) dengan pesan tidak lengkap, bahasa santai/Jawa Gresikan, dan sering tertimbun di luar jam kerja (hanya greeting message otomatis).
  - Admin Diskominfo harus membaca, mengonfirmasi kelengkapan data manual, dan mengetik ulang satu per satu ke web Service Desk.
- **Arsitektur & Pendekatan Dua Fase**:
  - **Fase 1 (Human-in-the-Loop / Presentasi Awal Tanpa Risiko)**:
    - Chat WA warga dipandu interaktif oleh AI jika data belum lengkap (lokasi, foto, rincian).
    - AI mengekstrak entitas penting (Nama, No WA, Lokasi, Kategori, Urgensi) dan menentukan rekomendasi dinas/OPD terkait.
    - AI menyusun draf laporan terstruktur siap salin-tempel (*ready-to-copy*) untuk admin Diskominfo, menjaga kendali penuh admin dan keamanan sistem internal tanpa menyentuh source code atau database produksi.
  - **Fase 2 (Otomasi API Lanjutan)**:
    - Jika izin dan kredensial/API staging diberikan mentor, draf langsung ditembakkan via REST API / endpoint ke Service Desk.
- **Tech Stack**: Node.js / Baileys (WA), 9Router (Gemini Flash / Structured Output JSON), PostgreSQL.

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

## 📌 Rekomendasi Eksekusi
1. **Amankan PT GCS**: Jangan tolak penerimaan PT GCS terlebih dahulu sebelum ada kepastian hitam di atas putih dari Diskominfo.
2. **Pengajuan ke Diskominfo**: Bawa proposal ringkas 1-2 lembar berbasis usulan **AI Subdomain Guard** (menyertakan bukti live temuan cloaking judol di domain Pemkab) langsung ke bagian SPBE/Persandian.
3. **Pilihan Final**: Jika Diskominfo menyetujui dalam tenggat waktu konfirmasi PT GCS, ambil Diskominfo; jika berbelit-belit atau kuota penuh, ambil PT GCS dengan mengajukan sistem AI Document Parser.
