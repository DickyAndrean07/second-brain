---
type: synthesis
title: "Arsitektur Lengkap AI Team Otonom untuk Bisnis"
created: 2026-10-22
updated: 2026-10-22
tags:
  - synthesis/blueprint
  - synthesis/ai-team
  - synthesis/best-practices
sources:
  - "[[wiki/sources/video-1-pengenalan-hermes-dan-instalasi]]"
  - "[[wiki/sources/video-2-hermes-dashboard-telegram-memori]]"
  - "[[wiki/sources/video-3-sandbox-google-drive-dan-gws]]"
  - "[[wiki/sources/video-4-struktur-ai-team-dan-arsitektur]]"
  - "[[wiki/sources/video-5-membangun-mission-control-ai-team]]"
  - "[[wiki/sources/video-6-instalasi-ruang-mission-control-3d]]"
---

# 🔮 Sintesis: Arsitektur Lengkap AI Team Otonom untuk Bisnis

> [!summary] Intisari Sintesis
> Mengintegrasikan wawasan dari seluruh seri 6 video ke dalam satu cetak biru (*blueprint*) komprehensif: bagaimana membangun tim AI mandiri yang bekerja 24/7 di VPS/lokal, menggunakan pembagian peran fungsional (*multi-agent*), mengamankan data via sandbox, menyimpan pengalaman di Obsidian dan pengetahuan faktual di LLM Wiki, serta memonitor operasional secara visual melalui Ruang Mission Control 3D.

---

## 🏗️ 1. Lapisan Arsitektur Tim AI Terintegrasi

Berdasarkan keseluruhan seri materi, ekosistem AI Agent yang matang dibangun di atas **5 layer vertikal**:

```text
┌─────────────────────────────────────────────────────────────┐
│ 5. OBSERVABILITY & PORTAL: Ruang Mission Control 3D         │
│    (Office 3D, Kanban, Calendar, Token Tracker, PIN Lock)   │
├─────────────────────────────────────────────────────────────┤
│ 4. INTERAKSI & WORKSPACE: Telegram Bot + Google Workspace   │
│    (Home Channel, Whitelist User ID, Sandbox Google Drive)  │
├─────────────────────────────────────────────────────────────┤
│ 3. MEMORY & KNOWLEDGE: Multi-Tier Storage                   │
│    - Short-Term: soul.md, memory.md, agent.md, user.md      │
│    - Long-Term: Obsidian Bidirectional Graph                │
│    - Knowledge Base: LLM Wiki (Faktual, SOP, FAQ)          │
├─────────────────────────────────────────────────────────────┤
│ 2. AGENT ROLES & TOOLS: Multi-Agent Hierarchy & MCP         │
│    - Lead Agent (Orchestrator)                              │
│    - Sub-Agents: Finance, Sales, Marketing                  │
│    - Technical: Lead Engineer Agent -> OpenCode Executor    │
│    - Integrasi: MCP Universal Ports + GWS CLI               │
├─────────────────────────────────────────────────────────────┤
│ 1. INFRASTRUKTUR & MODEL: Perangkat & Otak Komputasi        │
│    - Server: VPS (Sumopod / Ubuntu) atau Mac Mini lokal     │
│    - Remote & Tunnel: Termius (SSH Port Forwarding)         │
│    - Model Router: OpenRouter (Nemotron) + OpenAI Codex     │
└─────────────────────────────────────────────────────────────┘
```

---

## ⚖️ 2. Temuan Kritis & Rekonsiliasi Prinsip Desain

### A. Kontrol Penuh vs Cloud Sandbox
[[wiki/concepts/ai-agent-vs-chatbot|AI Agent otonom]] membutuhkan kontrol lokal agar dapat mengeksekusi bash command, menjalankan file, dan mengedit spreadsheet. Namun kebebasan ini membawa risiko: karena AI bekerja secara probabilistik, **keamanan sandbox** ([[wiki/concepts/sandbox-security]]) wajib ditegakkan:
- Akun Google terpisah untuk sandbox.
- Folder ID khusus per profil agent.
- Proteksi akses portal dengan Access Code dan PIN Lock pada profil sensitif.

### B. Memory vs Knowledge (Pembedaan Krusial)
Catatan kerja agent tidak boleh ditumpuk dalam satu file raksasa. Sesuai [[wiki/concepts/agent-memory-architecture]]:
- **Memory** adalah catatan pengalaman kerja lampau (disimpan sebagai atomic notes di [[wiki/entities/obsidian|Obsidian]]).
- **Knowledge** adalah referensi faktual/SOP perusahaan yang dijadikan sumber kebenaran (*source of truth*) melalui format LLM Wiki.

### C. Alokasi Model AI yang Efisien
- **Model Tingkat Tinggi (Codex / GPT / Claude)**: Dialokasikan untuk Lead Agent (perencanaan dan orkestrasi) serta Lead Engineer (analisis arsitektur kode).
- **Model Ringan / Gratis ([[wiki/entities/openrouter|OpenRouter]] Nemotron)**: Digunakan untuk tugas administratif repetitif (pencatatan data, asisten rekapitulasi).
- *Peringatan*: Hindari menggunakan model gratis untuk ekstraksi data finansial penting tanpa adanya mekanisme *human-in-the-loop*.

---

## 🚀 3. Panduan Implementasi Langkah-demi-Langkah

1. **Fase Fondasi**: Sewa VPS murah, pasang [[wiki/entities/hermes-agent|Hermes]], buat akun [[wiki/entities/openrouter|OpenRouter]], dan sambungkan ke Telegram Bot dengan whitelist ID akun Anda via [[wiki/entities/termius|Termius]].
2. **Fase Integrasi Data**: Setup Google Cloud OAuth via [[wiki/entities/google-workspace-cli|GWS CLI]], buat folder Google Drive sandbox per-agen, dan buat skill operasional ([[wiki/concepts/skill-as-sop]]).
3. **Fase Multi-Agent**: Konfigurasikan Lead Agent sebagai titik orkestrasi utama dan aktifkan [[wiki/entities/opencode|OpenCode]] untuk otomatisasi rekayasa perangkat lunak.
4. **Fase Monitoring**: Pasang [[wiki/entities/ruang-mission-control|Ruang Mission Control 3D]] untuk memantau status agen secara visual dan mengaudit penggunaan token secara real-time.
5. **Fase Pemeliharaan**: Jadwalkan backup otomatis ke GitHub setiap malam untuk seluruh konfigurasi dan memori.

---

## 🔗 Halaman Terkait
- **Sumber Lengkap**: [[wiki/sources/video-1-pengenalan-hermes-dan-instalasi]], [[wiki/sources/video-2-hermes-dashboard-telegram-memori]], [[wiki/sources/video-3-sandbox-google-drive-dan-gws]], [[wiki/sources/video-4-struktur-ai-team-dan-arsitektur]], [[wiki/sources/video-5-membangun-mission-control-ai-team]], [[wiki/sources/video-6-instalasi-ruang-mission-control-3d]]
- **Konsep Kunci**: [[wiki/concepts/ai-agent-vs-chatbot]], [[wiki/concepts/sandbox-security]], [[wiki/concepts/agent-memory-architecture]], [[wiki/concepts/multi-agent-system]], [[wiki/concepts/skill-as-sop]], [[wiki/concepts/mission-control]], [[wiki/concepts/model-context-protocol]]
- **Entitas Utama**: [[wiki/entities/hermes-agent]], [[wiki/entities/opencode]], [[wiki/entities/obsidian]], [[wiki/entities/google-workspace-cli]], [[wiki/entities/termius]], [[wiki/entities/openrouter]], [[wiki/entities/ruang-mission-control]]
