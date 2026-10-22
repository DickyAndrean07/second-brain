---
type: entity
title: "RigorPilot"
entity_type: tool
created: 2026-10-22
updated: 2026-10-22
tags:
  - entity/tool
  - entity/research
  - research/reproduction
aliases:
  - "RigorPilot Skills"
  - "repo-intake-and-plan"
sources:
  - "https://github.com/lllllllama/rigorpilot-skills"
---

# 🔬 RigorPilot (Research Reproduction Framework)

> [!info] Ringkasan Entitas
> **RigorPilot** (`lllllllama/rigorpilot-skills`) adalah framework skill AI untuk mereplikasi kode riset (*research reproduction*) langsung dari `README.md` repositori ilmiah dengan eksekusi terbatas (*bounded execution*), audit bukti independen, dan preservasi file README asli.

## 📌 Peran & Komponen Utama
- **Fungsi Inti**: Membantu agen AI menjalankan dan mereplikasi eksperimen dari paper/repositori GitHub orang lain secara terukur tanpa mengeksekusi perintah berbahaya atau memboroskan resource.
- **Skill Utama**:
  - `ai-research-reproduction`: Skill orkestrator end-to-end untuk replikasi riset.
  - `repo-intake-and-plan`: Skill auditor/intake yang membaca `README.md`, menginventarisasi perintah, mengelompokkan kategori (inferensi, evaluasi, training), dan merancang rencana pengujian terkecil yang aman (*minimum trustworthy reproduction*).

## 🎯 Kegunaan untuk AI Team & Mas Dicky
1. **Riset & Skripsi AI**: Sangat berguna saat Mas Dicky menemukan paper arXiv dengan implementasi kode di GitHub. Agen dapat membedah repo tersebut terlebih dahulu sebelum mencoba menjalankan demo/inferensinya di VPS (RAM 4GB).
2. **Pencegahan Overload Server**: Menjaga agar agen tidak secara otomatis mendownload model berukuran puluhan gigabyte atau menjalankan training berat tanpa persetujuan eksplisit.

## 💡 Konsep & Sumber Terkait
- Konsep: [[wiki/concepts/sandbox-security]], [[wiki/concepts/skill-as-sop]]
- Framework: [[wiki/entities/hermes-agent]]
- Repositori: `https://github.com/lllllllama/rigorpilot-skills`
