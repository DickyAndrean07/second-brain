---
type: source
title: "Video 6 — Instalasi Ruang Mission Control 3D"
author: "YouTube Creator"
date_ingested: 2026-10-22
tags:
  - source/video
  - topic/mission-control
  - topic/3d-office
  - topic/security
  - topic/analytics
original_file: "[[raw/video 6 - rapi.md]]"
---

# 📖 Video 6 — Instalasi Ruang Mission Control 3D

> [!abstract] Ringkasan Eksekutif
> Menjelaskan evolusi besar Mission Control dari tampilan 2D pixel art menjadi **Ruang Mission Control 3D** yang interaktif bernuansa Indonesia. Memandu instalasi otomatis via AI Agent di VPS, konfigurasi port forwarding Termius (port `3001`), monitoring konsumsi token model AI, serta implementasi sistem keamanan berlapis (Access Code global dan Profile Lock berbasis PIN untuk agen bernilai tinggi).

## 🎯 Argumen & Tesis Utama
- Evolusi antarmuka dari 2D ke 3D meningkatkan kejelasan visual mengenai status operasional tim AI secara spasial (area workstation untuk kerja aktif, area santai untuk idle, lantai atas untuk off/istirahat).
- Pemantauan biaya operasional (konsumsi token LLM per agent) sangat penting agar skala sistem AI tetap terkendali dan efisien secara finansial.
- Portal operasional tim AI memerlukan pengamanan bertingkat (*defense in depth*): proteksi akses portal publik dengan **Access Code** dan penguncian agent kritikal (seperti Lead Engineer) menggunakan **Profile Lock (PIN)**.

## 🔑 Poin-Poin Kunci & Wawasan
- **Evolusi [[wiki/entities/ruang-mission-control|Ruang Mission Control]]**:
  - Dikembangkan dari repository open source publik "Ruang".
  - Dilengkapi fitur peralihan fleksibel antara mode 2D dan 3D.
  - Lingkungan 3D bertema Indonesia dengan workstation kerja, area santai, serta lantai atas/balkon yang mencerminkan status live setiap agent.
- **Instalasi Otonom oleh AI Agent**:
  - Pengguna hanya perlu memberikan URL repository GitHub kepada Hermes Agent di Telegram dengan instruksi: *"Instal project ini, pastikan berjalan lokal, dan berikan alamat serta port-nya."*
  - AI Agent secara mandiri mengkloning repo, membaca dokumentasi instalasi, menginstal dependensi, dan menjalankan server pada port `3001`.
- **Port Forwarding Termius Port 3001**:
  - Bind Address `127.0.0.1`, Local Port `3001`, Destination Host VPS Hermes, Destination Port `3001`.
- **Fitur Baru & Pemantauan Operasional**:
  - *Token Usage Analytics*: Memantau volume konsumsi token per agent dalam 24 jam terakhir untuk audit biaya model.
  - *Kanban & Calendar*: Pelacakan pekerjaan dan jadwal otomatis (*scheduled tasks*).
  - *Memory Inspector*: Membaca dan memeriksa isi memori markdown tiap agent secara langsung dari web GUI tanpa membuka terminal.
  - *Folder & Log Explorer*: Navigasi file kerja agent dan pelacakan log error sistem.
  - *Dark Mode*: Antarmuka ramah mata untuk pemantauan jangka panjang.
- **Fitur Keamanan Baru**:
  1. **Access Code**: Melindungi seluruh halaman portal web dari akses tanpa izin.
  2. **Profile Lock**: Fitur penguncian berbasis PIN pada profil agent tertentu yang menyimpan informasi sensitif atau hak akses tinggi (misal: Lead Engineer atau Finance Agent).

## 💡 Konsep & Entitas Terkait
- **Konsep**: [[wiki/concepts/mission-control]], [[wiki/concepts/sandbox-security]], [[wiki/concepts/multi-agent-system]]
- **Entitas**: [[wiki/entities/ruang-mission-control]], [[wiki/entities/hermes-agent]], [[wiki/entities/termius]]

## 💬 Kutipan Penting
> "Access code melindungi seluruh Ruang Mission Control, sedangkan profile lock melindungi agent tertentu yang menyimpan data kritikal."
> "Area tersebut bukan sekadar animasi. Status visual harus mencerminkan status agent yang sebenarnya."

## 🔗 Referensi Silang & Catatan Lanjutan
- Sumber sebelumnya: [[wiki/sources/video-5-membangun-mission-control-ai-team|Video 5 — Membangun Mission Control untuk AI Team]]
- Sintesis lengkap: [[wiki/synthesis/arsitektur-lengkap-ai-team-otonom|Sintesis Arsitektur Tim AI Otonom]]
