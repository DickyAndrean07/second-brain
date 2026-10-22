---
type: concept
title: "Model Context Protocol (MCP)"
created: 2026-10-22
updated: 2026-10-22
tags:
  - concept/mcp
  - concept/integration
  - concept/standards
aliases:
  - "MCP"
  - "Universal Port AI"
sources:
  - "[[wiki/sources/video-4-struktur-ai-team-dan-arsitektur]]"
---

# 💡 Model Context Protocol (MCP)

> [!info] Definisi
> **Model Context Protocol (MCP)** adalah standar protokol terbuka yang bertindak sebagai "port universal" (dianalogikan seperti colokan USB untuk AI) yang memungkinkan AI Agent terhubung, bertukar konteks, dan mengeksekusi aksi pada berbagai perangkat lunak eksternal, sistem basis data, dan API secara seragam.

## 🔍 Mengapa MCP Menjadi Standar Krusial?
Sebelum adanya MCP, menghubungkan AI Agent dengan setiap aplikasi pihak ketiga (seperti database SQL, browser, sistem file, atau aplikasi desktop) memerlukan penulisan kode integrasi custom yang rapuh dan berbeda-beda.

Dengan MCP:
- Pengembang membuat atau memasang **MCP Server** untuk aplikasi target.
- AI Agent (sebagai MCP Client) secara otomatis mengenali skema alat (*tool schema*), parameter yang dibutuhkan, dan cara memanggilnya tanpa konfigurasi ad-hoc yang rumit.

## 🛠️ Contoh Penerapan dalam Video
Pada [[wiki/sources/video-4-struktur-ai-team-dan-arsitektur|Video 4]], tim AI memanfaatkan MCP untuk:
1. **Flomeria Desktop**: Menghubungkan agent dengan aplikasi desktop untuk otomatisasi alur kerja pembuatan konten.
2. **Custom Web Clipper**: Menghubungkan agent dengan alat kliping artikel web internal yang dibuat sendiri.

## 🧩 Hubungan dengan Konsep Lain
- Memperluas kapabilitas: [[wiki/concepts/ai-agent-vs-chatbot]] — memberi agent kemampuan eksekusi di dunia nyata.
- Menyediakan tools bagi: [[wiki/concepts/multi-agent-system]] — agent dapat berbagi atau menggunakan server MCP spesifik sesuai divisinya.

## 📚 Sumber yang Membahas Konsep Ini
- [[wiki/sources/video-4-struktur-ai-team-dan-arsitektur]] — Konsep MCP sebagai port USB universal untuk AI team.
