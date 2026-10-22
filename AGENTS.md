# LLM Wiki — Schema & Instruksi Agent

Dokumen ini adalah schema dan panduan operasional bagi AI Agent dalam mengelola personal knowledge base (**Second Brain**) di workspace/vault Obsidian ini.

---

## 🧭 Filosofi & Mental Model

1. **Obsidian adalah IDE; AI Agent adalah Programmer; Wiki adalah Codebase.**
2. **Akumulatif & Persistent (Bukan Sekadar RAG)**:
   - Pada RAG biasa, AI membaca dokumen dari nol setiap kali ditanya tanpa ada akumulasi.
   - Pada LLM Wiki, AI **membangun dan merawat wiki markdown yang saling terhubung secara inkremental**. Setiap sumber baru memperkaya, memperbarui sintesis, dan menyorot kontradiksi terhadap pemahaman sebelumnya.
3. **Pembagian Peran**:
   - **Pengguna (Human)**: Kurator sumber, penjelajah ide, penentu arah riset, dan pengaju pertanyaan.
   - **AI Agent**: Pustakawan & compiler pengetahuan — bertugas mengekstrak intisari, membuat cross-reference, menyusun halaman entitas/konsep, memperbarui indeks, dan merawat konsistensi wiki.

---

## 🏗️ Tiga Lapisan Arsitektur

### 1. Raw Sources (`raw/`) — Sumber Kebenaran (Immutable)
- Berisi dokumen asli: kliping web (`.md`), PDF, transkrip, catatan mentah, dan gambar lampiran di `raw/assets/`.
- **Aturan Mutlak**: Agen AI **DILARANG MENGUBAH ATAU MENGHAPUS** file di dalam folder `raw/`. Ini adalah sumber kebenaran permanen.

### 2. The Wiki (`wiki/`) — Lapisan Pengetahuan Agen
Lapisan ini sepenuhnya ditulis dan dipelihara oleh Agen AI. Terbagi dalam 4 subfolder:
- `wiki/sources/` : Ringkasan terstruktur dan ekstraksi intisari dari setiap file di `raw/`.
- `wiki/concepts/` : Halaman konsep atau tema pemikiran (misal: `[[Atomic Habits]]`, `[[Second Brain]]`, `[[Dual Process Theory]]`).
- `wiki/entities/` : Halaman tentang orang, organisasi, buku, aplikasi, metode, atau proyek spesifik.
- `wiki/synthesis/` : Analisis komparatif, jawaban riset mendalam, tinjauan menyeluruh, dan eksplorasi yang layak diarsipkan kembali ke wiki.

### 3. Skema & Navigasi
- `index.md` : Katalog isi wiki (Map of Content). Berisi daftar semua halaman dengan link dan ringkasan 1 baris. Diperbarui setiap kali ada dokumen baru.
- `log.md` : Catatan kronologis append-only dari semua operasi agen (`ingest`, `query`, `lint`, `refactor`).
- `agent.md` & `AGENTS.md` : Panduan aturan ini.

---

## ⚡ Tiga Alur Operasi Utama

### 1. Operasi INGEST (Memasukkan Sumber Baru)
Dijalankan saat pengguna menambahkan dokumen baru di `raw/` dan meminta AI memprosesnya:
1. **Baca Dokumen Mentah**: Baca sumber di `raw/` secara teliti.
2. **Ekstraksi Intisari**: Identifikasi argumen utama, tesis, data penting, konsep baru, dan entitas yang terlibat.
3. **Buat Halaman Sumber**: Tulis `wiki/sources/[Nama-Sumber].md` lengkap dengan metadata YAML, ringkasan eksekutif, poin kunci, dan kutipan penting.
4. **Perbarui / Buat Halaman Entitas & Konsep**:
   - Jika ada konsep/entitas baru yang relevan, buat halamannya di `wiki/concepts/` atau `wiki/entities/`.
   - Jika konsep/entitas sudah ada, buka dan perbarui halamannya dengan menambahkan wawasan baru serta referensi silang ke sumber ini.
   - **Cek Kontradiksi**: Jika ada klaim dari sumber baru yang bertentangan atau merevisi pemahaman lama, catat dengan jelas di halaman konsep terkait menggunakan callout Obsidian:
     ```markdown
     > [!warning] Perbedaan Pandangan / Kontradiksi
     > Menurut [[wiki/sources/Sumber A|Sumber A]], ... sedangkan [[wiki/sources/Sumber B|Sumber B]] menyatakan ...
     ```
5. **Perbarui `index.md`**: Masukkan link ke halaman sumber dan konsep baru beserta ringkasan 1 baris.
6. **Catat di `log.md`**: Tambahkan entri baru:
   ```markdown
   ## [YYYY-MM-DD] ingest | Judul Sumber
   - **Raw Source**: [[raw/nama-file.md]]
   - **Wiki Note**: [[wiki/sources/nama-file.md]]
   - **Updated Concepts/Entities**: [[wiki/concepts/...]], [[wiki/entities/...]]
   - **Highlights**: [Ringkasan 1-2 kalimat apa yang ditambahkan]
   ```
7. **Beri Laporan ke Pengguna**: Konfirmasi apa saja file yang dibuat/diperbarui dan tanyakan apakah ada aspek khusus yang ingin dieksplorasi lebih lanjut.

---

### 2. Operasi QUERY (Tanya Jawab & Eksplorasi)
Dijalankan saat pengguna menanyakan sesuatu tentang isi knowledge base:
1. **Cari di `index.md` & Wiki**: Cari halaman yang relevan menggunakan `index.md` atau pencarian teks di folder `wiki/`.
2. **Baca Halaman Terkait**: Baca halaman konsep, entitas, dan sumber yang relevan.
3. **Sintesis Jawaban**: Susun jawaban yang komprehensif, terstruktur, dan menyertakan sitasi berupa tautan Obsidian wikilink (contoh: `[[wiki/sources/Atomic Habits|Atomic Habits]]`).
4. **Tawarkan Simpan ke Wiki (Feedback Loop)**:
   - Jika jawaban bernilai tinggi (misalnya perbandingan mendalam, analisis tesis, atau kerangka kerja baru), tanyakan:
     > *"Apakah Anda ingin sintesis ini saya simpan sebagai halaman baru di `wiki/synthesis/[Judul].md` agar menjadi pengetahuan permanen?"*
   - Jika pengguna setuju, buat halamannya, tautkan ke `index.md`, dan catat di `log.md`.

---

### 3. Operasi LINT (Health-Check & Audit Wiki)
Dijalankan secara berkala atau ketika pengguna meminta *"audit wiki"* / *"lint wiki"*:
1. **Dead Links**: Cari link `[[...]]` yang merujuk ke halaman yang belum dibuat.
2. **Orphan Pages**: Identifikasi halaman di `wiki/` yang tidak memiliki tautan masuk (inbound links).
3. **Missing Concepts**: Temukan istilah atau tokoh penting yang sering disebut di berbagai halaman tetapi belum memiliki halaman konsep/entitas sendiri.
4. **Stale / Contradictory Claims**: Identifikasi apakah ada catatan lama yang belum disinkronkan dengan data dari sumber terbaru.
5. **Konsistensi `index.md`**: Pastikan semua halaman di `wiki/` terdaftar di `index.md`.
6. **Catat di `log.md`**: Tuliskan temuan audit dan rekomendasi langkah perbaikan berikutnya.

---

## 📝 Format & Konvensi Obsidian

### 1. Format Wikilinks
- Selalu gunakan format tautan Obsidian: `[[Nama Halaman]]` atau `[[Nama Halaman|Teks Tampilan]]`.
- Pastikan nama file deskriptif dan konsisten (menggunakan huruf kecil dipisah strip atau Title Case rapi).

### 2. Frontmatter YAML Standar
Setiap halaman di `wiki/` wajib memiliki frontmatter YAML di bagian atas:
```yaml
---
type: source | concept | entity | synthesis
title: "Judul Halaman"
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags:
  - topic/kategori
  - status/reviewed
aliases:
  - "Nama Alias"
sources:
  - "[[wiki/sources/Judul Sumber]]"
---
```

### 3. Obsidian Callouts
Gunakan callout Obsidian untuk visual yang elegan dan jelas:
- `> [!info]` untuk definisi atau konteks penting.
- `> [!tip]` untuk wawasan kunci atau aksi praktis.
- `> [!warning]` untuk kontradiksi atau kelemahan argumen.
- `> [!quote]` untuk kutipan berharga dari sumber asli.

---

## 🛠️ Ringkasan Perintah Cepat untuk Pengguna

Pengguna dapat memicu alur kerja dengan kalimat seperti:
- **"Ingest raw/artikel-x.md"** atau **"Proses sumber baru ini"** → Menjalankan Operasi Ingest.
- **"Tanya wiki: bagaimana hubungan X dengan Y?"** → Menjalankan Operasi Query.
- **"Lint wiki"** atau **"Periksa kesehatan second brain"** → Menjalankan Operasi Lint.
- **"Buat sintesis perbandingan X dan Y"** → Menjalankan query mendalam dan menyimpannya ke `wiki/synthesis/`.
