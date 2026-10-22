---
type: entity
title: "Hermes Agent"
entity_type: framework
created: 2026-10-22
updated: 2026-10-22
tags:
  - entity/framework
  - entity/hermes
  - entity/nous-research
aliases:
  - "Hermes"
  - "Nous Hermes"
sources:
  - "[[wiki/sources/video-1-pengenalan-hermes-dan-instalasi]]"
  - "[[wiki/sources/video-2-hermes-dashboard-telegram-memori]]"
  - "[[wiki/sources/video-4-struktur-ai-team-dan-arsitektur]]"
---

# 🏛️ Hermes Agent

> [!info] Profil Singkat
> **Hermes** adalah framework sistem AI Agent otonom yang dikembangkan oleh **Nous Research**. Hermes dirancang untuk dijalankan pada perangkat milik pengguna sendiri (VPS atau komputer lokal) dengan dukungan otonomi penuh, penjadwalan latar belakang, manajemen profil multi-agent, integrasi channel pesan, dan arsitektur memori Markdown persisten.

## 📌 Karakteristik & Fitur Utama
- **Menjalankan Operasi Otonom 24/7**: Mampu mengeksekusi tugas latar belakang dan proaktif memberikan notifikasi.
- **Dukungan Multi-Provider**: Terhubung mulus dengan model cloud via [[wiki/entities/openrouter|OpenRouter]], Anthropic, OpenAI Codex, maupun model lokal.
- **Hermes Dashboard Bawaan**: Antarmuka web di port `9119` untuk mengelola API keys, channel integrasi, switch profile, dan chat testing.
- **Struktur Memori Otomatis**: Menghasilkan 4 berkas Markdown inti: `soul.md`, `memory.md`, `agent.md`, dan `user.md`.
- **Integrasi Channel**: Mendukung Telegram bot (dengan fitur *home channel* dan *whitelist User ID*).
- **Ekosistem Tools**: Mendukung instalasi skill internal, integrasi [[wiki/entities/opencode|OpenCode]], dan MCP.

## 💡 Konsep & Sumber Terkait
- Konsep: [[wiki/concepts/ai-agent-vs-chatbot]], [[wiki/concepts/agent-memory-architecture]], [[wiki/concepts/multi-agent-system]]
- Sumber: [[wiki/sources/video-1-pengenalan-hermes-dan-instalasi]], [[wiki/sources/video-2-hermes-dashboard-telegram-memori]]
