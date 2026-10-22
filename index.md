---
type: index
title: Second Brain Master Index
updated: 2026-10-22
---

# 🧠 Second Brain — Master Index

Katalog konten utama personal knowledge base (LLM Wiki) yang dipelihara secara otomatis oleh AI Agent.

---

## 📚 Sources (`wiki/sources/`)
Daftar ringkasan dan ekstraksi dari dokumen mentah di `raw/`:

- [[wiki/sources/video-1-pengenalan-hermes-dan-instalasi|Video 1 — Pengenalan Hermes AI Agent dan Persiapan Instalasi]] — Konsep dasar AI Agent otonom vs ChatGPT, persiapan VPS, OpenRouter, dan instalasi awal Hermes.
- [[wiki/sources/video-2-hermes-dashboard-telegram-memori|Video 2 — Hermes Dashboard, Telegram, dan Struktur Memori Agent]] — Port forwarding Termius (port 9119), setup bot Telegram dengan proteksi whitelist ID, dan 4 file memori internal (`soul.md`, `memory.md`, `agent.md`, `user.md`).
- [[wiki/sources/video-3-sandbox-google-drive-dan-gws|Video 3 — Sandbox Google Drive dan Integrasi Google Workspace]] — Isolasi Google Drive sandbox, integrasi GWS CLI, Google Sheets API, pembuatan skill input transaksi, dan mitigasi risiko model gratis.
- [[wiki/sources/video-4-struktur-ai-team-dan-arsitektur|Video 4 — Struktur AI Team, Memory, Workspace, Skill, dan MCP]] — Arsitektur multi-agent, peran Lead Agent, short-term vs long-term memory (Obsidian), knowledge LLM Wiki, GitHub backup, dan MCP universal port.
- [[wiki/sources/video-5-membangun-mission-control-ai-team|Video 5 — Membangun Mission Control untuk AI Team]] — Perancangan portal operasional berbasis kebutuhan bisnis, kolaborasi Lead Agent, Lead Engineer, dan OpenCode, serta eksekusi 5 prompt pack.
- [[wiki/sources/video-6-instalasi-ruang-mission-control-3d|Video 6 — Instalasi Ruang Mission Control 3D]] — Pemantauan tim AI interaktif via Office 3D (port 3001), pelacakan konsumsi token, serta sistem keamanan Access Code dan PIN Profile Lock.

---

## 💡 Concepts & Topics (`wiki/concepts/`)
Ide-ide pokok, kerangka berpikir, teori, dan topik yang berkembang secara akumulatif:

- [[wiki/concepts/ai-agent-vs-chatbot|AI Agent vs Chatbot]] — Perbedaan fundamental antara sistem reaktif cloud (ChatGPT) dan sistem otonom proaktif 24/7 di perangkat lokal/VPS.
- [[wiki/concepts/sandbox-security|Sandbox Security]] — Strategi isolasi akun, pembatasan folder per-agen, dan review *human-in-the-loop* untuk memitigasi sifat AI yang probabilistik.
- [[wiki/concepts/agent-memory-architecture|Agent Memory Architecture]] — Tiga lapisan memori: file internal Hermes (short-term), graf Obsidian (long-term), dan LLM Wiki (knowledge/source of truth).
- [[wiki/concepts/multi-agent-system|Multi-Agent System]] — Struktur organisasi tim AI berdasarkan divisi fungsional (Finance, Sales, Marketing, Tech) di bawah orkestrasi Lead Agent untuk mencegah *context pollution*.
- [[wiki/concepts/skill-as-sop|Skill as SOP]] — Standarisasi instruksi repetitif menjadi modul SOP yang terstruktur dan dapat dipanggil kapan saja.
- [[wiki/concepts/mission-control|Mission Control]] — Portal operasional tim AI yang menggabungkan visualisasi status live (Office 2D/3D), Kanban board, calendar schedule, dan token analytics.
- [[wiki/concepts/model-context-protocol|Model Context Protocol (MCP)]] — Protokol universal standar industri yang menghubungkan AI Agent dengan berbagai aplikasi dan tools pihak ketiga.

---

## 🏛️ Entities (`wiki/entities/`)
Orang, organisasi, tools, aplikasi, framework, dan perangkat lunak penting:

- [[wiki/entities/hermes-agent|Hermes Agent]] — Framework sistem AI Agent otonom dari Nous Research yang berjalan di VPS/lokal.
- [[wiki/entities/opencode|OpenCode]] — Framework AI open-source untuk rekayasa perangkat lunak otonom (coding, testing, bug fixing).
- [[wiki/entities/obsidian|Obsidian]] — Aplikasi basis pengetahuan berbasis Markdown lokal dengan bidirectional links untuk memori jangka panjang dan LLM Wiki.
- [[wiki/entities/google-workspace-cli|Google Workspace CLI (GWS CLI)]] — Perangkat baris perintah untuk interaksi agent dengan Google Drive dan Google Sheets.
- [[wiki/entities/termius|Termius]] — Klien SSH modern yang digunakan untuk mengakses VPS dan mengonfigurasi local port forwarding (port 9119, 5173, 3001).
- [[wiki/entities/openrouter|OpenRouter]] — Agregator API multi-model AI terpadu (menyediakan model gratis seperti Nemotron dan model komersial).
- [[wiki/entities/ruang-mission-control|Ruang Mission Control]] — Portal operasional tim AI open-source berbasis visual Office 3D bertema lokal.
- [[wiki/entities/rigorpilot|RigorPilot]] — Framework skill AI untuk mereplikasi kode riset paper ilmiah secara terukur (bounded execution) dari README repositori.

---

## 🚀 Projects & Product Specs (`wiki/projects/`)
Spesifikasi produk, arsitektur teknis, dan PRD proyek yang dibangun:

- [[wiki/projects/edunotify-prd|Product Requirements Document (PRD) — EduNotify MVP]] — Dokumen kebutuhan produk lengkap sistem absensi sekolah estafet berbasis jadwal, integrasi WhatsApp Click-to-Chat manual, Early Warning System deterministik, dan analitik AI provider-agnostic.

---

## 🔮 Synthesis & Comparisons (`wiki/synthesis/`)
Analisis lintas-dokumen, jawaban mendalam terhadap pertanyaan riset, dan cetak biru komprehensif:

- [[wiki/synthesis/arsitektur-lengkap-ai-team-otonom|Arsitektur Lengkap AI Team Otonom untuk Bisnis]] — Cetak biru (*blueprint*) 5-layer terintegrasi menggabungkan infrastruktur VPS, memori multi-lapis, orkestrasi multi-agent, skill SOP, integrasi data Google Workspace, dan observabilitas Ruang 3D.
