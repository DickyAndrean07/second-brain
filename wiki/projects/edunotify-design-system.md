---
type: design-spec
title: "EduNotify Design System — Desktop & Mobile Webapp"
project: "EduNotify"
version: "1.0.0"
status: "APPROVED"
created: 2026-10-23
updated: 2026-10-23
author: "Diva (Product & System Analyst)"
target_builder: "Bagus (Builder Agent)"
reference_source: "edunotify/docs/design-reference.html"
tags:
  - project/edunotify
  - design/design-system
  - ui/responsive
---

# 🎨 EduNotify Design System & UI Reference

Acuan visual resmi redesain UI EduNotify (desktop & mobile responsive) berdasarkan referensi `edunotify-design-reference-desktop-mobile.html`.

## 1. Brand Identity & Logo
- **Logo Style**: Monogram **EN** geometris (Logo 03 — Insight).
- **Gradien Logo**: Linear gradient `#1351C6` (biru tua) ke `#04B9E8` (cyan cerah).
- **Aksen Titik**: Dot mint `#58F0CE` di sudut kanan atas monogram.
- **Wordmark**: `edu` (font-weight 800, warna dark navy / putih) + `notify` (warna biru `#176DFF` / cyan).

## 2. Color Palette & Theming
Mendukung **Light Mode** dan **Dark Mode**:

| Token | Hex Code | Penggunaan |
|---|---|---|
| **Brand Primary** | `#1351C6` | Tombol utama, header aktif, gradien brand |
| **Brand Cyan** | `#04B9E8` | Highlight, aksen grafik, status aktif |
| **Dark Canvas** | `#071325` | Background utama dark mode |
| **Dark Surface** | `#0E1E36` / `#11233B` | Card container, sidebar, navbar dark |
| **Light Canvas** | `#F3F7FE` | Background utama light mode |
| **Light Surface** | `#FFFFFF` | Card container, modal, tabel light |
| **Mint Accent** | `#35E6BD` / `#58F0CE` | Badge kehadiran tinggi, status sukses, dot logo |
| **Warning / Alpa** | `#FF4D4D` / `#FFAA00` | Sinyal operasional Alpa & peringatan EWS |

## 3. Komponen Antarmuka Desktop
- **Header**: Glassmorphism (`backdrop-filter: blur`), logo monogram, notifikasi, avatar profil, toggle switch Light/Dark mode.
- **Kartu Ringkasan (Metric Cards)**: Total siswa, persentase kehadiran sekolah/kelas, jumlah Alpa, status kelengkapan.
- **Tabel Kehadiran**: Baris rapi, avatar inisial, badge status warna tegas (Hadir: Hijau, Sakit: Kuning, Izin: Biru, Alpa: Merah).
- **Grafik Tren**: Area chart gradien halus dan bar chart komparasi antarkelas.

## 4. Mobile Webapp Responsiveness (390px – 430px)
Dioptimalkan untuk 3 layar kunci Wali Kelas:
1. **01 / Dashboard Mobile**:
   - Header ringkas dengan logo dan notifikasi.
   - Kartu persentase kehadiran dengan tren visual melengkung (*soft wave curve*).
   - Indikator status presensi hari ini.
   - Navigasi bawah (*bottom bar*) ramah jempol.
2. **02 / Layar Siswa Alpa (Intervensi Cepat)**:
   - Filter cepat (Semua, Alpa, Sakit, Izin).
   - Kartu per siswa Alpa memuat nama anak, nama ortu, dan tanggal kejadian.
   - Tombol tegas **"Kirim WhatsApp"** (`wa.me`) warna hijau WhatsApp + tombol konfirmasi status **"Sudah Dihubungi"**.
   - Teks panduan transparan: membuka WA bukan bukti pesan terkirim.
3. **03 / Layar AI Insight & EWS**:
   - Kartu peringatan dini dengan level urgensi (Tinggi / Sedang).
   - Narasi analitik AI dalam bahasa Indonesia yang empatik dan faktual.
   - Checklist rekomendasi tindak lanjut guru/wali kelas (non-punitif).

## 5. Batasan Implementasi
- Jangan mengubah arsitektur backend, logika presensi estafet, otorisasi RBAC, atau Drizzle schema.
- Redesain fokus 100% pada styling Tailwind, layout responsive, komponen UI, dan integrasi mode Light/Dark.
- 190 vitest unit tests wajib tetap 100% lulus.
