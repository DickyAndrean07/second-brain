---
type: source
title: "Video 1 — Pengenalan Hermes AI Agent dan Persiapan Instalasi"
author: "YouTube Creator"
date_ingested: 2026-10-22
tags:
  - source/video
  - topic/ai-agent
  - topic/hermes
  - topic/infrastructure
original_file: "[[raw/video 1 - rapi.md]]"
---

# 📖 Video 1 — Pengenalan Hermes AI Agent dan Persiapan Instalasi

> [!abstract] Ringkasan Eksekutif
> Video pembuka seri implementasi AI Agent untuk bisnis. Membahas perbedaan mendasar antara chatbot reaktif (seperti ChatGPT standar) dengan AI Agent otonom yang bekerja 24/7 di perangkat sendiri (VPS/Mini PC). Memandu persiapan infrastruktur awal, pemilihan AI model via OpenRouter, dan instalasi dasar framework [[wiki/entities/hermes-agent|Hermes]].

## 🎯 Argumen & Tesis Utama
- AI Agent bukan sekadar alat tanya-jawab (chatbot), melainkan pegawai digital otonom yang bekerja di komputer sendiri selama 24 jam sehari secara proaktif.
- Kontrol penuh atas perangkat (VPS/Dedicated Hardware) sangat penting agar AI memiliki akses luas untuk eksekusi tugas nyata (edit file, olah spreadsheet, buat video).
- Menggunakan VPS (seperti Sumopod) adalah cara paling hemat dan praktis untuk pemula dibanding membeli perangkat keras dedicated di awal.

## 🔑 Poin-Poin Kunci & Wawasan
- **[[wiki/concepts/ai-agent-vs-chatbot|AI Agent vs ChatGPT]]**:
  - *Sistem*: AI Agent berjalan di perangkat sendiri (kontrol penuh), sedangkan ChatGPT berjalan di cloud pihak ketiga.
  - *Cara Kerja*: AI Agent bekerja otonom & proaktif di latar belakang (background schedule), sedangkan ChatGPT bersifat reaktif menunggu perintah (*prompt*).
- **Prasyarat Infrastruktur**:
  1. Perangkat: VPS (direkomendasikan spesifikasi awal 2 vCPU, 2GB RAM, 40GB storage seharga ~Rp60.000/bulan).
  2. Framework: [[wiki/entities/hermes-agent|Hermes]] dari Nous Research.
  3. Model AI: [[wiki/entities/openrouter|OpenRouter]] (dapat menggunakan model gratis seperti NVIDIA Nemotron Ultra 550B untuk pengujian awal).
  4. Akses SSH: [[wiki/entities/termius|Termius]] untuk remote management dan port forwarding.
  5. Antarmuka Komunikasi: Telegram Bot (gratis, ringan, mudah dikonfigurasi).
  6. Data & Workspace: Akun Google terpisah untuk sandbox Google Drive & Google Sheets.
- **Instalasi & Verifikasi Awal**:
  - Pengecekan status: `hermes status`.
  - Inisialisasi cepat: `hermes setup` (memilih *Quick setup* dan terminal backend lokal).
  - Hubungkan model: `hermes model` → pilih OpenRouter → masukkan API Key → pilih model Nemotron Ultra.
  - Verifikasi terminal: `hermes chat`.
- **Hermes Dashboard**:
  - Web UI bawaan untuk konfigurasi tanpa terminal (`hermes dashboard` berjalan di port `127.0.0.1:9119`). Memerlukan port forwarding via Termius karena VPS tidak memiliki browser GUI.

## 💡 Konsep & Entitas Terkait
- **Konsep**: [[wiki/concepts/ai-agent-vs-chatbot]], [[wiki/concepts/sandbox-security]]
- **Entitas**: [[wiki/entities/hermes-agent]], [[wiki/entities/openrouter]], [[wiki/entities/termius]]

## 💬 Kutipan Penting
> "AI Agent dapat dianalogikan seperti seorang pegawai yang kita rekrut. Kemudian, kita memberikan komputer kepada pegawai tersebut. Setelah memiliki komputer, ia dapat melakukan berbagai pekerjaan di dalam komputer itu. Perbedaannya, pegawai tersebut bukan manusia, melainkan AI Agent."

## 🔗 Referensi Silang & Catatan Lanjutan
- Lanjutan alur kerja: [[wiki/sources/video-2-hermes-dashboard-telegram-memori|Video 2 — Hermes Dashboard, Telegram, dan Struktur Memori Agent]]
