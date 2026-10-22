---
type: source
title: "Video 4 — Struktur AI Team, Memory, Workspace, Skill, dan MCP"
author: "YouTube Creator"
date_ingested: 2026-10-22
tags:
  - source/video
  - topic/ai-team
  - topic/architecture
  - topic/obsidian
  - topic/mcp
  - topic/llm-wiki
original_file: "[[raw/video 4 - rapi.md]]"
---

# 📖 Video 4 — Struktur AI Team, Memory, Workspace, Skill, dan MCP

> [!abstract] Ringkasan Eksekutif
> Menjelaskan arsitektur lengkap tim AI yang matang untuk operasional bisnis harian. Membedakan peran multi-agent, fungsi orkestrasi Lead Agent dan onboarding SOP, pembagian memori jangka pendek bawaan Hermes vs memori jangka panjang berbasis Obsidian (bidirectional graph), pemisahan antara Memory (pengalaman) dan Knowledge ([[wiki/concepts/agent-memory-architecture#knowledge-vs-memory|LLM Wiki]]), backup otomatis ke GitHub, serta integrasi alat pihak ketiga via Model Context Protocol (MCP).

## 🎯 Argumen & Tesis Utama
- AI Agent yang berdaya guna bukan sekadar hasil instalasi model, melainkan ekosistem lengkap yang memiliki: role, workspace, skill, memori, dan tools. Tanpa lingkungan ini, agent hanya akan menjadi chatbot yang rumit.
- Satu agent tidak boleh menangani semua bidang (finance, sales, marketing) karena kelebihan konteks (*context pollution*) akan menurunkan akurasi. Solusinya adalah struktur **[[wiki/concepts/multi-agent-system|Multi-Agent System]]** dengan **Lead Agent** sebagai orkestrator.
- Pemilik bisnis tidak perlu terobsesi mengejar model AI terbaru. Nilai jangka panjang terbesar ada pada SOP, sistem workflow, dan akumulasi memori/pengetahuan yang dibangun.

## 🔑 Poin-Poin Kunci & Wawasan
- **Infrastruktur: Dedicated Hardware vs VPS**:
  - Mac Mini / Mini PC memberikan isolasi data total dan kontrol software penuh.
  - VPS tetap menjadi opsi terbaik dan termurah untuk memulai tanpa modal perangkat keras.
- **Strategi Pemilihan Model AI**:
  - Lead Agent: Wajib menggunakan model berpikir terbaik (seperti OpenAI via Codex) untuk mengatur konteks, merencanakan tugas, dan membimbing sub-agent.
  - Sub-agent tugas spesifik (personal assistant, rekapitulasi data): Cukup model ringan, cepat, dan murah.
- **Mengapa Butuh Struktur Multi-Agent?**:
  - Mencegah kebingungan konteks antar-divisi.
  - Setiap agent memiliki profil, role, folder workspace terpisah di Google Drive, dan kumpulan skill tersendiri.
  - *Lead Agent*: Bertugas mendelegasikan tugas, troubleshooting, dan melakukan *onboarding* agent baru agar mematuhi SOP sistem.
- **Arsitektur Memori vs Knowledge**:
  - *Short-Term Memory*: File Markdown bawaan Hermes (`soul.md`, `memory.md`, dll.). Memiliki keterbatasan skala dan rawan bias jika file terlalu besar.
  - *Long-Term Memory*: Menggunakan [[wiki/entities/obsidian|Obsidian]]. Memanfaatkan *bidirectional linking* (`[[wikilinks]]`) dan *graph view* untuk menghubungkan potongan-potongan konteks secara asosiatif.
  - *Knowledge (LLM Wiki)*: Dipelopori oleh Andrej Karpathy. **Memory adalah pengalaman kerja agent, sedangkan Wiki adalah referensi faktual / source of truth** (SOP, FAQ, dokumentasi internal).
- **Backup & Self-Maintenance Otomatis**:
  - Seluruh konfigurasi, memori Markdown, dan workspace Hermes disinkronkan secara terjadwal setiap malam ke GitHub menggunakan schedule job.
  - AI Agent dapat memelihara dirinya sendiri (*self-healing*).
- **[[wiki/concepts/model-context-protocol|Model Context Protocol (MCP)]]**:
  - Protokol universal (diibaratkan port USB) untuk menghubungkan agent dengan aplikasi pihak ketiga atau software internal kustom (misal: Flomeria Desktop, Web Clipper).
- **11 Pilar AI Team Lengkap**:
  1. Infrastruktur, 2. AI Model, 3. Struktur AI Agent, 4. Channel, 5. Memory, 6. Knowledge, 7. Workspace, 8. Skill, 9. Tools, 10. Automation, 11. Backup.

## 💡 Konsep & Entitas Terkait
- **Konsep**: [[wiki/concepts/multi-agent-system]], [[wiki/concepts/agent-memory-architecture]], [[wiki/concepts/model-context-protocol]], [[wiki/concepts/skill-as-sop]]
- **Entitas**: [[wiki/entities/hermes-agent]], [[wiki/entities/obsidian]], [[wiki/entities/openrouter]]

## 💬 Kutipan Penting
> "Memory adalah pengalaman. Wiki adalah referensi faktual."
> "Nilai utama AI team berada pada SOP yang dibangun, workflow yang dibangun, dan sistem yang dibuat — bukan hanya pada model AI yang digunakan."

## 🔗 Referensi Silang & Catatan Lanjutan
- Sumber sebelumnya: [[wiki/sources/video-3-sandbox-google-drive-dan-gws|Video 3 — Sandbox Google Drive dan Integrasi Google Workspace]]
- Sumber berikutnya: [[wiki/sources/video-5-membangun-mission-control-ai-team|Video 5 — Membangun Mission Control untuk AI Team]]
