---
type: concept
title: "AI Agent vs Chatbot"
created: 2026-10-22
updated: 2026-10-22
tags:
  - concept/ai-fundamentals
  - concept/autonomy
aliases:
  - "Perbedaan AI Agent dan Chatbot"
  - "Autonomous AI Agent"
sources:
  - "[[wiki/sources/video-1-pengenalan-hermes-dan-instalasi]]"
  - "[[wiki/sources/video-4-struktur-ai-team-dan-arsitektur]]"
---

# 💡 AI Agent vs Chatbot

> [!info] Definisi
> **Chatbot** (seperti ChatGPT atau Claude standar) adalah antarmuka percakapan reaktif berbasis cloud yang hanya memproses dan menjawab teks saat diberikan prompt oleh pengguna. 
> Sedangkan **AI Agent** adalah entitas komputasi otonom yang berjalan di lingkungan perangkat milik pengguna (VPS/lokal), memiliki akses ke sistem file, memori persisten, alat eksekusi (*tools*), dan mampu bekerja secara proaktif selama 24 jam tanpa harus menunggu instruksi manual terus-menerus.

## 🔍 Penjelasan Mendalam & Matriks Komparatif

Perbedaan mendasar antara keduanya terletak pada dua sumbu utama: **sistem kepemilikan lingkungan** dan **otonomi cara kerja**.

| Aspek | Chatbot Konvensional (ChatGPT / Claude) | AI Agent Otonom (Hermes, OpenClaw) |
| :--- | :--- | :--- |
| **Lokasi Eksekusi** | Cloud vendor terpusat (OpenAI / Anthropic) | Komputer sendiri (VPS, Mini PC, Mac Mini) |
| **Tingkat Kontrol** | Terbatas pada plugin/antarmuka vendor | Kontrol penuh atas OS, file system, dan skrip |
| **Pola Kerja** | Reaktif (harus ada prompt dari manusia) | Otonom & Proaktif (bisa dijadwalkan, background job) |
| **Akses Alat & Aksi**| Terbatas (sandbox tertutup cloud) | Luas (CLI, Git, Spreadsheet, API, terminal) |
| **Memori Konteks** | Satu sesi percakapan / memori cloud global | Memori terstruktur Markdown, Obsidian graph, LLM Wiki |
| **Analog Bisnis** | Konsultan cerdas yang dipanggil sesekali | Pegawai tetap yang diberi meja & komputer kerja |

## 🧩 Hubungan dengan Konsep Lain
- Berkaitan erat dengan: [[wiki/concepts/sandbox-security]] — karena AI Agent memiliki kendali eksekusi lokal, ruang kerjanya harus diisolasi dalam sandbox.
- Fondasi bagi: [[wiki/concepts/multi-agent-system]] — beberapa AI Agent dapat dikelompokkan menjadi tim kerja fungsional.
- Memerlukan: [[wiki/concepts/skill-as-sop]] — agar tugas yang dijalankan konsisten dan terarah.

## 📚 Sumber yang Membahas Konsep Ini
- [[wiki/sources/video-1-pengenalan-hermes-dan-instalasi]] — Pengantar filosofi AI Agent sebagai pegawai digital 24 jam di VPS.
- [[wiki/sources/video-4-struktur-ai-team-dan-arsitektur]] — Integrasi agent dengan tools, workspace, dan schedule mandiri.
