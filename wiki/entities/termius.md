---
type: entity
title: "Termius"
entity_type: tool
created: 2026-10-22
updated: 2026-10-22
tags:
  - entity/tool
  - entity/ssh
  - entity/devops
aliases:
  - "Termius SSH"
sources:
  - "[[wiki/sources/video-1-pengenalan-hermes-dan-instalasi]]"
  - "[[wiki/sources/video-2-hermes-dashboard-telegram-memori]]"
  - "[[wiki/sources/video-5-membangun-mission-control-ai-team]]"
  - "[[wiki/sources/video-6-instalasi-ruang-mission-control-3d]]"
---

# 🏛️ Termius

> [!info] Profil Singkat
> **Termius** adalah aplikasi klien SSH dan SFTP modern multi-platform yang memudahkan pengelolaan koneksi server jarak jauh (VPS), sinkronisasi kredensial, dan konfigurasi penerusan porta (*port forwarding*).

## 📌 Peran Krusial dalam Ekosistem AI Agent
Karena VPS yang menjalankan [[wiki/entities/hermes-agent|Hermes]] dan aplikasi tim AI tidak memiliki antarmuka grafis desktop, Termius digunakan untuk:
1. Mengakses baris perintah terminal VPS dari komputer lokal.
2. **Local SSH Port Forwarding**: Menghubungkan porta server internal VPS ke browser komputer lokal sehingga antarmuka web berikut dapat diakses:
   - **Port `9119`**: Hermes Dashboard bawaan.
   - **Port `5173`**: Dev server Mission Control 2D.
   - **Port `3001`**: Ruang Mission Control 3D.

## 💡 Konsep & Sumber Terkait
- Konsep: [[wiki/concepts/mission-control]], [[wiki/concepts/ai-agent-vs-chatbot]]
- Sumber: [[wiki/sources/video-1-pengenalan-hermes-dan-instalasi]], [[wiki/sources/video-2-hermes-dashboard-telegram-memori]], [[wiki/sources/video-6-instalasi-ruang-mission-control-3d]]
