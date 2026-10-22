---
type: source
title: "Video 5 — Membangun Mission Control untuk AI Team"
author: "YouTube Creator"
date_ingested: 2026-10-22
tags:
  - source/video
  - topic/mission-control
  - topic/opencode
  - topic/prompt-engineering
  - topic/development-cycle
original_file: "[[raw/video 5 - rapi.md]]"
---

# 📖 Video 5 — Membangun Mission Control untuk AI Team

> [!abstract] Ringkasan Eksekutif
> Menjelaskan proses perancangan dan pembangunan **Mission Control** — sebuah portal pemantauan dan pengelolaan operasional tim AI. Menekankan filosofi "mulai dari kebutuhan pengguna, bukan coding", membedakan fungsi konfigurasi Hermes Dashboard vs fungsi operasional Mission Control, serta mempraktikkan siklus pengembangan software otonom menggunakan hierarki: Business Owner → Lead Agent → Lead Engineer Agent → [[wiki/entities/opencode|OpenCode]] (didukung subscription OpenAI Codex).

## 🎯 Argumen & Tesis Utama
- Jangan memulai pembuatan aplikasi dengan instruksi langsung coding (*"Buatkan saya Mission Control"*). Mulailah dari perumusan masalah, user persona, kebutuhan data, dan fitur aksi nyata.
- **Hermes Dashboard** berfungsi untuk *konfigurasi teknis* internal Hermes, sedangkan **[[wiki/concepts/mission-control|Mission Control]]** berfungsi untuk *pemantauan operasional* harian tim AI (apa yang sedang dikerjakan di latar belakang).
- Pembuatan software skala penuh dapat didelegasikan ke AI melalui pemisahan peran yang jelas: Lead Agent (strategi/kebutuhan bisnis), Lead Engineer (arsitektur teknis & review), dan OpenCode (eksekutor koding, testing, dan debugging).

## 🔑 Poin-Poin Kunci & Wawasan
- **4 Pertanyaan Kunci Sebelum Coding**:
  1. Siapa yang akan menggunakan produk?
  2. Masalah apa yang ingin diselesaikan?
  3. Informasi apa yang ingin ditampilkan?
  4. Fitur atau aksi apa yang ingin dibangun?
- **Fitur MVP Mission Control**:
  - *Dashboard*: Ringkasan jumlah agent, task aktif, task selesai, aktivitas terkini.
  - *Agent List*: Status, role, responsibility, dan konfigurasi agent.
  - *Board (Kanban)*: Status alur kerja (*To do, Ready, In progress, Backlog, Review, Done*).
  - *Calendar*: Visualisasi jadwal pengerjaan otomatis oleh agent.
  - *Activity*: Log kejadian real-time (tugas selesai, error, pembaruan data).
  - *Office 2D (Pixel Art)*: Representasi visual status agent nyata (bekerja di workstation, idle di sofa, atau off/istirahat). Bukan sekadar animasi hiasan.
- **Hierarki & Siklus Pengembangan Otonom**:
  $$\text{Business Owner} \longrightarrow \text{Lead Agent} \longrightarrow \text{Lead Engineer} \longrightarrow \text{OpenCode}$$
  - *Lead Agent*: Menjaga konteks bisnis dan berkomunikasi dengan owner.
  - *Lead Engineer*: Membuat product specification dan implementation plan, memecah tugas, serta me-review hasil kerja.
  - *[[wiki/entities/opencode|OpenCode]]*: Framework open-source (bundle di Hermes) yang membaca codebase, menulis kode, menjalankan dev server (`5173`), menguji, dan memperbaiki bug secara mandiri.
- **Penerapan Prompt Pack Bertahap (Bukan One-Shot Prompt)**:
  - *Prompt 1 (Planning)*: Membimbing pembuatan dokumen spesifikasi produk dan acceptance criteria.
  - *Prompt 2 (Build MVP)*: OpenCode mengeksekusi fondasi aplikasi, komponen UI, dan router.
  - *Prompt 3 (Office 2D)*: Menyuntikkan aset pixel art dan sinkronisasi status agent ke workstation.
  - *Prompt 4 (Review & Fix)*: Pengujian menyeluruh dan perbaikan bug.
  - *Prompt 5 (Customization)*: Kustomisasi fitur khusus divisi bisnis (misal: invoice approval, review konten).
- **Akses Aplikasi via Termius**:
  - Port forwarding port `5173` dari VPS ke `127.0.0.1:5173` komputer lokal agar web GUI dapat dibuka di browser.

## 💡 Konsep & Entitas Terkait
- **Konsep**: [[wiki/concepts/mission-control]], [[wiki/concepts/multi-agent-system]]
- **Entitas**: [[wiki/entities/opencode]], [[wiki/entities/hermes-agent]], [[wiki/entities/termius]]

## 💬 Kutipan Penting
> "Jangan mulai dari coding. Mulailah dari kebutuhan."
> "Office bukan sekadar dekorasi. Status visual harus merepresentasikan status agent yang sebenarnya. Jika agent sedang bekerja, karakter harus berada di workstation."

## 🔗 Referensi Silang & Catatan Lanjutan
- Sumber sebelumnya: [[wiki/sources/video-4-struktur-ai-team-dan-arsitektur|Video 4 — Struktur AI Team, Memory, Workspace, Skill, dan MCP]]
- Sumber berikutnya: [[wiki/sources/video-6-instalasi-ruang-mission-control-3d|Video 6 — Instalasi Ruang Mission Control 3D]]
