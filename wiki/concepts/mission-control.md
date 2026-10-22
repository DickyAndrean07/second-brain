---
type: concept
title: "Mission Control"
created: 2026-10-22
updated: 2026-10-22
tags:
  - concept/mission-control
  - concept/dashboard
  - concept/observability
aliases:
  - "Mission Control AI Team"
  - "Ruang Mission Control"
  - "Office 2D/3D"
sources:
  - "[[wiki/sources/video-5-membangun-mission-control-ai-team]]"
  - "[[wiki/sources/video-6-instalasi-ruang-mission-control-3d]]"
---

# 💡 Mission Control (Portal Operasional AI Team)

> [!info] Definisi
> **Mission Control** adalah portal aplikasi web yang dibangun khusus untuk memberikan visibilitas, pengawasan operasional (*observability*), dan kontrol terpusat terhadap aktivitas tim AI otonom yang bekerja 24/7 di latar belakang.

## 🔍 Perbedaan: Hermes Dashboard vs Mission Control

| Dimensi | Hermes Dashboard | Mission Control (Sultan / Ruang 3D) |
| :--- | :--- | :--- |
| **Fokus Utama** | Konfigurasi sistem teknis internal Hermes | Operasional harian & progres kerja tim bisnis |
| **Audiens** | Developer / Administrator sistem | Business Owner, Manajer Operasional, Tim Bisnis |
| **Fitur Kunci** | API Keys, Gateway restart, Setup model & channel | Kanban Board, Jadwal Calendar, Log aktivitas, Visual Office |
| **Pelacakan Beban** | Status gateway aktif/mati | Analisis pemakaian token (Token Usage) per agent |
| **Asal Perangkat Lunak** | Fitur bawaan (*bundled*) framework Hermes | Aplikasi kustom yang dibangun sesuai kebutuhan bisnis |

## 🕹️ Fitur Inti Mission Control yang Matang
1. **Office Visual (2D Pixel Art / 3D Ruang)**:
   - Merefleksikan status fisik agen secara *live*:
     - *Di Workstation*: Agent sedang aktif mengeksekusi instruksi/skrip.
     - *Di Area Santai / Sofa*: Agent dalam status idle menunggu perintah.
     - *Di Area Istirahat / Lantai Atas*: Agent dalam status nonaktif/off.
2. **Kanban Task Board**:
   - Memastikan tidak ada pekerjaan yang hilang di dalam riwayat chat. Status alur kerja: *To do, Ready, In progress, Backlog, Review, Done*.
3. **Calendar**:
   - Menampilkan agenda pekerjaan rutin yang dijadwalkan otomatis (*cron/schedule jobs*).
4. **Token Usage Analytics**:
   - Memonitor penggunaan token LLM per agent dalam periode 24 jam terakhir untuk audit efisiensi biaya.
5. **Memory & Folder Explorer**:
   - Membaca memori Markdown dan dokumen kerja agent langsung dari GUI tanpa memerlukan koneksi SSH terminal.
6. **Keamanan Bertingkat**:
   - Perlindungan portal dengan **Access Code** dan penguncian profil agen sensitif dengan **Profile Lock (PIN)**.

## 🧩 Hubungan dengan Konsep Lain
- Menampilkan status dari: [[wiki/concepts/multi-agent-system]] — memantau seluruh profil agent dalam satu layar.
- Membantu menegakkan: [[wiki/concepts/sandbox-security]] — mengaudit akses folder dan log error.
- Dikembangkan otonom oleh: [[wiki/entities/opencode]] — menggunakan pendekatan Prompt Pack terarah.

## 📚 Sumber yang Membahas Konsep Ini
- [[wiki/sources/video-5-membangun-mission-control-ai-team]] — Konsep dasar, kebutuhan MVP, Office 2D, dan Prompt Pack.
- [[wiki/sources/video-6-instalasi-ruang-mission-control-3d]] — Evolusi ke Ruang 3D, token tracking, dan keamanan PIN.
