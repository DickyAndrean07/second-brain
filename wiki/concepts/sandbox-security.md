---
type: concept
title: "Sandbox Security"
created: 2026-10-22
updated: 2026-10-22
tags:
  - concept/security
  - concept/best-practice
aliases:
  - "Isolasi Lingkungan AI"
  - "Sandbox Google Drive"
sources:
  - "[[wiki/sources/video-1-pengenalan-hermes-dan-instalasi]]"
  - "[[wiki/sources/video-3-sandbox-google-drive-dan-gws]]"
  - "[[wiki/sources/video-6-instalasi-ruang-mission-control-3d]]"
---

# 💡 Sandbox Security (Isolasi Keamanan AI Agent)

> [!info] Definisi
> **Sandbox Security** adalah strategi pembatasan lingkungan dan hak akses bagi AI Agent untuk memitigasi risiko kerusakan, penghapusan, atau kebocoran data akibat sifat model AI yang probabilistik (tidak 100% akurat).

## 🔍 Mengapa Sandbox Wajib untuk AI Agent?
AI Agent bekerja dengan mengeksekusi aksi nyata (membaca, mengedit, membuat file, menjalankan skrip). Karena AI bekerja secara probabilistik, selalu ada peluang kesalahan interpretasi atau halusinasi instruksi. Memberikan AI Agent akses langsung ke storage utama (misalnya Google Drive pribadi atau direktori root server) merupakan risiko keamanan yang fatal.

## 🛡️ Tiga Lapisan Perlindungan Sandbox
1. **Pemisahan Akun & Storage (Account-Level Sandbox)**:
   - Buat akun Google/email khusus untuk AI Agent (bukan email utama bisnis).
   - Simpan data kerja di Google Drive milik akun sandbox tersebut.
   - Jika butuh data dari akun utama, bagikan (*share*) hanya folder tertentu dengan permission terbatas.
2. **Pemisahan Folder per-Agent (Workspace Isolation)**:
   - Di dalam storage, buat folder khusus per profil: `agent-finance/`, `agent-sales/`, `agent-marketing/`.
   - Suntikkan *strict folder rule* ke dalam memori agent (Folder ID spesifik yang boleh diakses).
3. **Portal & Profile Locking (Access Security)**:
   - *Access Code*: Kode otentikasi global untuk membuka antarmuka web operasional ([[wiki/concepts/mission-control]]).
   - *Profile Lock (PIN)*: Mengunci profil agent berpangkat tinggi (seperti Lead Engineer atau Finance) agar tidak sembarang orang dapat membaca prompt atau kredensial internalnya.

> [!warning] Human-in-the-Loop untuk Tugas Finansial
> Khusus untuk data berisiko tinggi (misalnya pencatatan transaksi kas masuk/keluar dari foto bon/struk), jangan langsung menganggap hasil ekstraksi agent sebagai data final. Sediakan mekanisme review manual oleh manusia sebelum data disetujui.

## 🧩 Hubungan dengan Konsep Lain
- Melindungi: [[wiki/concepts/multi-agent-system]] — mencegah satu agent merusak workspace agent lain.
- Diimplementasikan oleh: [[wiki/entities/google-workspace-cli]] — membatasi scope OAuth API dan folder ID.
- Dipantau via: [[wiki/concepts/mission-control]] — melihat aktivitas dan akses folder secara transparan.

## 📚 Sumber yang Membahas Konsep Ini
- [[wiki/sources/video-3-sandbox-google-drive-dan-gws]] — Desain Google Drive sandbox dan bahaya kesalahan baca model gratis.
- [[wiki/sources/video-6-instalasi-ruang-mission-control-3d]] — Access code dan PIN profile locking pada Ruang 3D.
