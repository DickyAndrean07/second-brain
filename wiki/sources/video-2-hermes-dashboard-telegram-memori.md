---
type: source
title: "Video 2 — Hermes Dashboard, Telegram, dan Struktur Memori Agent"
author: "YouTube Creator"
date_ingested: 2026-10-22
tags:
  - source/video
  - topic/hermes
  - topic/dashboard
  - topic/telegram
  - topic/agent-memory
original_file: "[[raw/video 2 - rapi.md]]"
---

# 📖 Video 2 — Hermes Dashboard, Telegram, dan Struktur Memori Agent

> [!abstract] Ringkasan Eksekutif
> Menjelaskan konfigurasi teknis untuk mengakses web interface Hermes Dashboard melalui SSH port forwarding Termius, integrasi bot Telegram sebagai kanal percakapan harian (lengkap dengan pengamanan User ID whitelist), serta membongkar 4 file arsitektur memori internal bawaan Hermes (`soul.md`, `memory.md`, `agent.md`, `user.md`).

## 🎯 Argumen & Tesis Utama
- Antarmuka terminal tidak praktis untuk operasional harian; Telegram adalah kanal paling efektif dan berbiaya nol untuk berinteraksi dengan AI team secara mobile.
- Mengamankan akses bot Telegram dengan whitelist `allow Telegram user ID` adalah keharusan mutlak agar pihak luar tidak bisa mengeksploitasi data atau mengeksekusi perintah.
- AI Agent membutuhkan struktur memori persisten berupa file Markdown agar memiliki identitas peran, mengingat preferensi pengguna, dan melacak riwayat tugas.

## 🔑 Poin-Poin Kunci & Wawasan
- **Port Forwarding Dashboard via Termius**:
  - Jalankan `hermes dashboard` di VPS (berjalan pada port `127.0.0.1:9119`).
  - Di Termius: Buat Port Forwarding Local dengan port `9119`, bind address `127.0.0.1`, destination host VPS Hermes.
  - Akses `127.0.0.1:9119` langsung dari browser lokal.
- **Integrasi Telegram Bot**:
  1. Buat bot via `@BotFather` di Telegram (`/newbot`), simpan Bot Token privat.
  2. Dapatkan ID akun Telegram pribadi via bot user info (`/start`).
  3. Di Hermes Dashboard: Masukkan Bot Token dan isi **`allow Telegram user ID`** dengan ID akun Anda untuk memblokir akses publik.
  4. Simpan konfigurasi, aktifkan channel, dan restart gateway Hermes.
  5. Di chat bot: Kirim pesan dan jadikan percakapan tersebut sebagai **Home Channel** (kanal utama untuk laporan berkala dan pesan proaktif).
- **[[wiki/concepts/agent-memory-architecture|4 File Memori Bawaan Hermes]]**:
  - `user.md`: Menyimpan profil pengguna global, kebiasaan, dan preferensi kerja.
  - `agent.md`: Profil agen berdasarkan peran/proyek spesifik (misal: Finance, Sales, Marketing).
  - `memory.md`: Log riwayat pekerjaan, tugas yang telah selesai, dan catatan operasional.
  - `soul.md`: Karakter, gaya komunikasi, dan kepribadian inti dari agen.
  - *Sifat*: Semua file ini berformat Markdown `.md` dan diperbarui secara otomatis oleh Hermes.

## 💡 Konsep & Entitas Terkait
- **Konsep**: [[wiki/concepts/agent-memory-architecture]], [[wiki/concepts/ai-agent-vs-chatbot]]
- **Entitas**: [[wiki/entities/hermes-agent]], [[wiki/entities/termius]]

## 💬 Kutipan Penting
> "Home channel adalah channel utama yang digunakan Hermes untuk mengirim notifikasi, informasi progres, hasil pekerjaan, dan pesan proaktif lainnya."

## 🔗 Referensi Silang & Catatan Lanjutan
- Sumber sebelumnya: [[wiki/sources/video-1-pengenalan-hermes-dan-instalasi|Video 1 — Pengenalan Hermes AI Agent dan Persiapan Instalasi]]
- Sumber berikutnya: [[wiki/sources/video-3-sandbox-google-drive-dan-gws|Video 3 — Sandbox Google Drive dan Integrasi Google Workspace]]
