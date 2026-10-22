---
type: concept
title: "Skill as SOP"
created: 2026-10-22
updated: 2026-10-22
tags:
  - concept/skill
  - concept/sop
  - concept/standardization
aliases:
  - "Skill sebagai SOP"
  - "Agent Skills"
sources:
  - "[[wiki/sources/video-3-sandbox-google-drive-dan-gws]]"
  - "[[wiki/sources/video-4-struktur-ai-team-dan-arsitektur]]"
---

# 💡 Skill as SOP (Skill sebagai Prosedur Operasional Standar)

> [!info] Definisi
> **Skill as SOP** adalah prinsip di mana instruksi operasional yang berulang (seperti pencatatan transaksi kas, pengiriman notifikasi invoice, atau onboarding agent) tidak diketik secara manual setiap saat, melainkan dikemas menjadi berkas instruksi modular (**Skill**) yang dapat dipanggil oleh AI Agent secara konsisten.

## 🔍 Karakteristik & Anatomi Skill
Sebuah Skill membungkus:
1. **Nama & Trigger**: Kapan skill harus dieksekusi (otomatis atau via perintah pengguna).
2. **Prasyarat & Dependensi**: CLI apa yang dibutuhkan (misal: GWS CLI), format data masukan, atau skrip pembantu.
3. **Instruksi Step-by-Step (Runbook)**: Prosedur pemrosesan data, validasi kolom, dan mitigasi kesalahan.
4. **Format Output Standar**: Standar penulisan hasil ke file spreadsheet, markdown, atau pesan chat.

## ⚙️ Studi Kasus: Skill Input Transaksi
Pada [[wiki/sources/video-3-sandbox-google-drive-dan-gws|Video 3]], alih-alih mengetik perintah rumit setiap kali ada struk pembelian:
- Dibuat skill bernama `input transaksi`.
- Agent secara otomatis:
  1. Menerima input teks atau gambar struk.
  2. Mengekstrak nominal, merchant, tanggal, dan kategori.
  3. Memetakan ke kolom Google Sheet `Transaction Log`.
  4. Menjalankan perintah Google Workspace CLI untuk append baris baru.
  5. Melaporkan konfirmasi ke pengguna di Telegram.

> [!tip] Skalabilitas Bisnis
> Nilai sesungguhnya dari tim AI bukan pada model AI apa yang digunakan hari ini, melainkan pada perpustakaan SOP (kumpulan skill) yang berhasil distandarkan. Jika model diganti ke versi yang lebih baru di masa depan, skill-skill ini tetap berfungsi sebagai aset intelektual bisnis.

## 🧩 Hubungan dengan Konsep Lain
- Menjaga kepatuhan pada: [[wiki/concepts/sandbox-security]] — skill mengatur batasan akses folder.
- Dijalankan oleh agen dalam: [[wiki/concepts/multi-agent-system]] — agent finance memiliki skill finance, sales memiliki skill sales.
- Tersimpan dalam: [[wiki/concepts/agent-memory-architecture#knowledge-vs-memory|Knowledge Base]] atau folder skill lokal.

## 📚 Sumber yang Membahas Konsep Ini
- [[wiki/sources/video-3-sandbox-google-drive-dan-gws]] — Pembuatan skill pencatatan transaksi Google Sheets.
- [[wiki/sources/video-4-struktur-ai-team-dan-arsitektur]] — Skill sebagai SOP pembeda kapabilitas tiap profil agent.
