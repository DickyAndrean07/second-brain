---
type: source
title: "Video 3 — Sandbox Google Drive dan Integrasi Google Workspace"
author: "YouTube Creator"
date_ingested: 2026-10-22
tags:
  - source/video
  - topic/security
  - topic/sandbox
  - topic/google-workspace
  - topic/skills
original_file: "[[raw/video 3 - rapi.md]]"
---

# 📖 Video 3 — Sandbox Google Drive dan Integrasi Google Workspace

> [!abstract] Ringkasan Eksekutif
> Menjelaskan pentingnya prinsip sandbox keamanan saat memberikan akses data ke AI Agent yang probabilistik. Memandu pembuatan Google Cloud Project, OAuth consent, aktivasi Google Sheets API & Google Drive API menggunakan GWS CLI, pembatasan folder per-agent, serta pembuatan skill input transaksi (baik via teks maupun ekstraksi gambar struk pembayaran).

## 🎯 Argumen & Tesis Utama
- AI Agent bersifat probabilistik dan tidak ada jaminan akurasi 100%. Jangan pernah memberikan akses langsung ke Google Drive utama yang berisi data pribadi atau data kritikal bisnis.
- Akses harus diisolasi dalam **Google Drive Sandbox** terpisah dengan akun Google khusus, dan folder dibagikan secara spesifik menggunakan izin folder terbatas (*strict folder rule*).
- Untuk otomatisasi operasional yang konsisten, instruksi repetitif harus diubah menjadi **[[wiki/concepts/skill-as-sop|Skill]]** (SOP yang dapat dipanggil kapan saja).

## 🔑 Poin-Poin Kunci & Wawasan
- **[[wiki/concepts/sandbox-security|Konsep Sandbox Lingkungan Kerja]]**:
  - Akun sandbox Google terpisah khusus AI Agent.
  - Berbagi folder terpilih dari akun utama ke akun sandbox dengan hak akses *Editor*.
  - Pemisahan subfolder di dalam Drive: `Hermes Data/` → folder per-agent (`agent-finance/`, `agent-sales/`, `agent-demo/`).
  - Strict Rule di memori agent: Agent diberikan Folder ID spesifik dan diinstruksikan tidak boleh mengakses file di luar folder tersebut.
- **Integrasi [[wiki/entities/google-workspace-cli|Google Workspace CLI (GWS CLI)]]**:
  1. Buat Google Cloud Project baru di `console.cloud.google.com` menggunakan akun sandbox.
  2. Aktifkan **Google Drive API** dan **Google Sheets API**.
  3. Konfigurasi OAuth Consent Screen (tipe External, support email).
  4. Buat OAuth Client ID (tipe *Desktop App*), unduh JSON credentials.
  5. Jalankan autentikasi OAuth melalui browser lokal dan kirimkan session token ke Hermes.
- **Pengujian Pencatatan Transaksi**:
  - Pembuatan file Google Sheet: `Transaction Log` dengan kolom lengkap (Tanggal, Waktu, Tipe, Kategori, Merchant, Deskripsi, Jumlah, Harga Satuan, Metode Pembayaran, Catatan).
  - *Input Transaksi via Teks*: Agent otomatis mengeksekusi GWS CLI untuk append data ke baris spreadsheet.
  - *Pembuatan Skill `input transaksi`*: Membungkus prompt panjang menjadi SOP yang dapat dipanggil ringkas.
  - *Input Transaksi via Foto Struk/Bon*: Agent membaca gambar struk, melakukan OCR/ekstraksi data, dan mengisikannya ke sheet.
- **Risiko Model Gratis & Human-in-the-Loop**:
  - Pada pengujian, model gratis (Nemotron) salah mengekstrak harga dari struk (membaca Rp5.000 dari yang seharusnya Rp35.700.000).
  - Wawasan krusial: Model gratis rawan kesalahan ekstraksi angka; gunakan model berbayar/canggih (seperti Codex/OpenAI) untuk tugas finansial, serta wajib sediakan validasi manusia (*human-in-the-loop*) sebelum data dinyatakan final.

## 💡 Konsep & Entitas Terkait
- **Konsep**: [[wiki/concepts/sandbox-security]], [[wiki/concepts/skill-as-sop]], [[wiki/concepts/ai-agent-vs-chatbot]]
- **Entitas**: [[wiki/entities/google-workspace-cli]], [[wiki/entities/hermes-agent]]

## 💬 Kutipan Penting
> "AI Agent bekerja secara probabilistik. Tidak ada jaminan 100 persen bahwa AI Agent selalu akurat dan tidak pernah melakukan kesalahan. Jika AI Agent diberikan akses langsung ke workspace utama tanpa sandbox, ada risiko AI Agent salah mengubah atau bahkan menghapus data."

## 🔗 Referensi Silang & Catatan Lanjutan
- Sumber sebelumnya: [[wiki/sources/video-2-hermes-dashboard-telegram-memori|Video 2 — Hermes Dashboard, Telegram, dan Struktur Memori Agent]]
- Sumber berikutnya: [[wiki/sources/video-4-struktur-ai-team-dan-arsitektur|Video 4 — Struktur AI Team, Memory, Workspace, Skill, dan MCP]]
