---
type: project
title: Visual Engine — Browser Automation & Animation Intelligence Architecture
status: in-progress
updated: 2026-11-06
tags: [visual-engine, playwright, animation, scrollytelling, motion-capture, classification]
---

# 👁️ Visual Engine — Browser Automation & Animation Intelligence

Sistem inspeksi, eksperimen scroll, dan kecerdasan analisis animasi berbasis Playwright dan TypeScript di lingkungan Windows native (`D:\projects\visual-engine`).

Dirancang sebagai fondasi modular untuk jangka panjang:
1. **Website Replication Engine** — kemampuan menganalisis dan mereplikasi tata letak serta interaksi web.
2. **Animation Learning Engine** — pemetaan matematis perilaku animasi (CSS, GSAP, requestAnimationFrame).
3. **Video Intelligence Engine** — integrasi analitik visual dinamis.

---

## 🏗️ Status Milestones

### Milestone 1 — Browser Inspection Foundation (Selesai)
- Peluncuran browser Playwright Headed/Headless.
- Inspeksi DOM, Computed CSS, dan geometri layout (`getBoundingClientRect`).
- Navigasi scroll dasar maju dan mundur.
- Deteksi sinyal animasi awal dan ekspor artifact terstruktur.
- CLI runner dan unit test suite.

### Milestone 2A — Page Readiness & Complete Coverage (Selesai & Terverifikasi)
- Deteksi loader dan kesiapan halaman (*readiness checks*).
- Penanganan dynamic document height saat scrolling.
- Verifikasi batas bawah halaman (*verified bottom check*).
- Page mapping dan pelaporan coverage navigasi.
- Skema JSON evidence versioned (8/8 valid).
- **Catatan Benchmark**: Benchmark terhadap target eksternal `grail-app.com` mengembalikan HTTP 402 pada koneksi otomatis; dicatat jujur sebagai batas isolasi/jaringan, sementara local test suite lulus 12/12.

### Milestone 2B — Scroll Experimentation & Motion Capture (Selesai)
- Runner eksperimen scroll terstruktur dengan pergerakan terencana:
  - *Forward exploration* (scroll linear terarah).
  - *Reverse exploration* (analisis reversibilitas dan histeresis).
  - *Dwell / Pause checkpoints* (pengamatan perubahan saat scroll berhenti untuk memisahkan time-based vs scroll-driven).
  - *Speed variation* (scroll lambat vs cepat).
  - *Repeatability analyzer* (pengulangan 3x untuk mendeteksi variabilitas dan jitter).
- Instrumentasi sampling per-frame sinkron dengan `requestAnimationFrame`.
- Ekstraksi computed styles (`transform`, `opacity`, `position`, `visibility`, dll.) dan geometri.
- Format manifest dan trace output modular per-seksi (`forward-trace.json`, `reverse-trace.json`, `dwell-trace.json`, `repeatability.json`).

### Milestone 2C — Animation Behavior Classification (Selesai)
- Mesin klasifikasi berbasis aturan (rule-based) transparan tanpa ketergantungan API cloud/LLM.
- Kategori animasi terverifikasi:
  - `Static`: Konten normal tanpa gerak animasi.
  - `Sticky / Pinned`: Elemen tetap diam di viewport sepanjang rentang scroll (CSS sticky & GSAP pin).
  - `Parallax`: Elemen bergerak dengan rasio kecepatan diferensial terhadap scroll natural.
  - `Scroll Reveal`: Elemen bertransisi masuk (opacity/translate/clip-path) berdasarkan progres scroll.
  - `Scroll-Scrubbed Motion`: Animasi terikat langsung dan reversibel dengan pergerakan scroll.
  - `Discrete Scroll Trigger`: Titik scroll memicu transisi waktu independen.
  - `Time-Based Animation`: Animasi tetap berjalan saat scroll berhenti (terdeteksi via dwell test).
  - `Mixed Animation`: Kombinasi pemicu scroll dan pelambatan waktu (easing).
  - `Unknown / Insufficient Evidence`: Klasifikasi aman jika bukti tidak konklusif.
- Pemisahan ketat tri-level: **Observed** (fakta terukur) vs **Inferred** (dugaan teknis) vs **Verified** (cocok dengan ground-truth fixture).
- Evaluator confidence (`high`, `medium`, `low`, `insufficient`) berbasis kelengkapan bukti dan konsistensi multi-run.
- Generator spesifikasi animasi terstruktur dan laporan naratif Markdown (`animation-intelligence-report.md`).

### Milestone 2D — Measurement Accuracy, Interaction Intelligence & Engine Hardening (Selesai)
- **Nested Scroll Support**: Opsi `--scroll-target` untuk container terisolasi, mengukur `scrollTop` aktual dan geometri relatif.
- **Trajectory Measurement**: Pelacakan kurva scroll instan, smooth, reverse, dan interrupted.
- **Interaction Intelligence**: Recorder transisi `hover`, `leave`, dan `click` pada loopback fixtures.
- **Ground Truth Validation (278 sampel)**:
  - Max Opacity Error: $3.33 \times 10^{-7}$ (toleransi 0.05).
  - Max Geometry/Transform Error: $0\text{ px}$ (toleransi 2–3 px).
  - Missing Samples: 0.
- **Multilabel Evaluation (11 elemen)**: 16 True Positives, 0 False Positives, 0 False Negatives (100% precision & recall pada controlled fixture set).
- **Status Akhir**: **CONDITIONAL GO** untuk eksperimen rekonstruksi frontend lokal (Milestone 3).

---

## 🧪 Hasil Pengujian & Verifikasi Terkini
- **Typecheck**: `npm run typecheck` (Lulus, 0 error).
- **Build**: `npm run build` (Lulus, 0 error).
- **Automated Tests**: 14/14 lulus (0 gagal, 0 dilewati).
- **Integritas Skema**: Validasi terhadap `experiment.schema.json` (JSON Schema 2.1.0) 100% konsisten.
- **Laporan & Evidence**: `measurement-quality.json`, `classification-evaluation.json`, dan `docs/verification-2d.md`.

---

## 📌 Batasan Saat Ini & Rekomendasi Selanjutnya
1. **Validasi Fixture vs Web Arbitrer**: Akurasi sempurna (0 px error, 0 FP/FN) berlaku pada fixture deterministik terkontrol; untuk web publik arbitrer tetap akan ada noise rendering.
2. **Target Eksternal**: Grail tidak dicoba ulang setelah respons HTTP 402; tidak menghambat engine inti.
3. **Langkah Berikut (Milestone 3)**: Memulai *Website Replication Engine* (tahap rekonstruksi kode CSS/GSAP) dengan target eksperimen fixture lokal mandiri terlebih dahulu sesuai rekomendasi CONDITIONAL GO.
