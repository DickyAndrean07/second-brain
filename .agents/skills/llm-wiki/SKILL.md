---
name: llm-wiki
description: >-
  Gunakan skill ini ketika pengguna ingin memasukkan atau memproses dokumen sumber baru (ingest),
  bertanya atau mengeksplorasi knowledge base (query), menyusun sintesis pengetahuan, atau
  menjalankan audit/pemeriksaan kesehatan wiki (lint) pada Obsidian LLM Wiki (Second Brain).
  Trigger: "ingest", "proses sumber", "tanya wiki", "lint wiki", "health check wiki",
  "second brain", "masukkan ke wiki", "update wiki", "rangkum dokumen ke wiki".
---

# LLM Wiki — Obsidian Second Brain Skill

Skill ini memandu AI Agent untuk mengelola personal knowledge base (Second Brain) berbasis Obsidian secara disiplin, inkremental, dan akumulatif sesuai pola **LLM Wiki**.

---

## 📌 Prinsip Utama
1. **Raw Sources (`raw/`) Bersifat Immutable**: JANGAN PERNAH mengubah atau menghapus file di `raw/`.
2. **Wiki Bersifat Akumulatif (`wiki/`)**: Setiap informasi baru harus dikaitkan dengan pengetahuan yang sudah ada. Jika ada kontradiksi atau perkembangan pemikiran, catat perbedaannya, jangan ditimpa begitu saja.
3. **Disiplin Pengindeksan & Pencatatan**:
   - Selalu perbarui `index.md` jika ada halaman baru atau perubahan penting.
   - Selalu tambahkan baris aktivitas baru di `log.md` setelah selesai operasi.
4. **Obsidian-First**: Gunakan format `[[wikilinks]]` dan callout Obsidian (`> [!info]`, `> [!tip]`, `> [!warning]`, `> [!quote]`).

---

## 🚀 ALUR KERJA 1: INGEST (Memproses Sumber Baru)

Gunakan alur ini ketika pengguna meminta untuk memproses file dokumen di `raw/`.

### Langkah 1 — Membaca & Menganalisis Dokumen
1. Gunakan tool `view_file` untuk membaca dokumen mentah di `raw/<nama-file>`.
2. Identifikasi:
   - **Tesis utama & argumen**: Apa poin inti yang disampaikan penulis?
   - **Poin wawasan**: Fakta, metode, atau wawasan penting apa yang ditawarkan?
   - **Konsep & Teori**: Konsep atau kerangka kerja apa yang diperkenalkan atau dirujuk?
   - **Entitas**: Tokoh, buku, riset, atau organisasi apa yang disebutkan?
   - **Kutipan emas**: 1–3 kutipan paling tajam dan bernilai.

### Langkah 2 — Membuat Catatan Sumber (`wiki/sources/`)
1. Buat file baru di `wiki/sources/<slug-judul>.md` menggunakan template [source-template.md](./resources/source-template.md).
2. Tuliskan ringkasan eksekutif, poin-poin kunci, entitas/konsep yang terhubung dengan `[[wikilinks]]`, dan kutipan penting.

### Langkah 3 — Membuat atau Memperbarui Konsep & Entitas
1. **Periksa Konsep Terkait**:
   - Untuk setiap konsep kunci, periksa apakah file `wiki/concepts/<nama-konsep>.md` sudah ada.
   - **Jika BELUM ada**: Buat file baru menggunakan template [concept-template.md](./resources/concept-template.md). Hubungkan kembali ke sumber asalnya.
   - **Jika SUDAH ada**: Buka file tersebut, tambahkan wawasan baru dari sumber ini pada bagian yang relevan, dan perbarui bagian `## 📚 Sumber yang Membahas Konsep Ini`.
   - **Jika terjadi Kontradiksi**: Tambahkan callout `> [!warning] Perbedaan Pandangan` yang menjelaskan perbedaan klaim antara sumber lama dan sumber baru.
2. **Periksa Entitas Terkait**:
   - Untuk tokoh penting atau institusi kunci, buat/perbarui di `wiki/entities/<nama-entitas>.md` menggunakan template [entity-template.md](./resources/entity-template.md).

### Langkah 4 — Perbarui `index.md`
1. Buka `index.md`.
2. Tambahkan link ke sumber baru di bagian `## 📚 Sources` dengan ringkasan 1 kalimat.
3. Tambahkan konsep atau entitas baru di bagian masing-masing jika belum tercantum.

### Langkah 5 — Catat di `log.md`
Tambahkan entri kronologis di bagian paling atas log (di bawah header):
```markdown
## [YYYY-MM-DD] ingest | <Judul Dokumen>
- **Raw**: [[raw/<nama-file>]]
- **Source Note**: [[wiki/sources/<slug-judul>.md]]
- **Updated/Created**: [[wiki/concepts/<konsep-1>]], [[wiki/entities/<entitas-1>]]
- **Summary**: <Ringkasan 1-2 kalimat tentang dampak sumber ini terhadap wiki>
```

### Langkah 6 — Laporkan ke Pengguna
Beri tahu pengguna file apa saja yang dibuat/diperbarui, poin inti yang dipelajari wiki, dan tanyakan apakah ada aspek tertentu yang ingin ditelaah lebih dalam.

---

## 🔍 ALUR KERJA 2: QUERY (Tanya Jawab & Eksplorasi)

Gunakan alur ini saat pengguna mengajukan pertanyaan penelitian atau ingin menghubungkan ide-ide di wiki.

### Langkah 1 — Cari Konteks di Wiki
1. Baca `index.md` untuk memetakan halaman mana saja yang relevan dengan pertanyaan.
2. Gunakan `grep_search` pada direktori `wiki/` jika memerlukan pencarian kata kunci tertentu.
3. Buka dan baca halaman konsep, entitas, dan sumber yang relevan menggunakan `view_file`.

### Langkah 2 — Susun Sintesis Jawaban
1. Susun jawaban yang komprehensif dan runtut.
2. Sertakan sitasi eksplisit dalam bentuk `[[wiki/sources/...]]` dan `[[wiki/concepts/...]]`.
3. Tunjukkan hubungan antardokumen (misal: bagaimana konsep A dari dokumen X diterapkan pada konteks dokumen Y).

### Langkah 3 — Tawarkan Feedback Loop (Simpan ke Wiki)
Jika jawaban menghasilkan analisis komparatif atau wawasan baru yang berbobot:
1. Tanyakan kepada pengguna:
   > *"Apakah Anda ingin sintesis ini saya arsipkan sebagai catatan baru di `wiki/synthesis/<judul-topik>.md` agar menjadi pengetahuan permanen?"*
2. Jika pengguna setuju:
   - Gunakan template [synthesis-template.md](./resources/synthesis-template.md) untuk membuat file di `wiki/synthesis/`.
   - Tautkan halaman sintesis tersebut ke `index.md`.
   - Catat di `log.md` dengan format `## [YYYY-MM-DD] query | <Topik Sintesis>`.

---

## 🩺 ALUR KERJA 3: LINT (Audit & Pemeliharaan Wiki)

Gunakan alur ini ketika pengguna meminta pemeriksaan berkala (contoh: *"audit wiki"*, *"lint wiki"*, *"cek kesehatan second brain"*).

### Langkah 1 — Pengecekan Integritas
1. **Broken Links**: Telusuri semua file di `wiki/` untuk menemukan tautan `[[...]]` yang target filenya belum ada.
2. **Orphan Pages**: Periksa apakah ada catatan di `wiki/` yang tidak ditautkan oleh halaman lain sama sekali.
3. **Missing Concepts**: Cari istilah penting yang muncul berulang kali di berbagai catatan sumber namun belum memiliki halaman konsep di `wiki/concepts/`.
4. **Index Sync**: Pastikan setiap file di `wiki/` telah tercatat di `index.md`.
5. **Kontradiksi atau Data Usang**: Periksa apakah ada catatan yang saling bertentangan yang belum diberi catatan rekonsiliasi.

### Langkah 2 — Laporan & Rencana Aksi
1. Sajikan laporan kesehatan wiki yang mencakup:
   - Jumlah total sumber, konsep, entitas, dan sintesis.
   - Daftar link rusak (broken links) & usulan pembuatannya.
   - Daftar catatan yatim (orphan pages) & usulan penautannya.
   - Usulan konsep baru yang sebaiknya dibuatkan halaman sendiri.
2. Catat audit ini di `log.md`:
   ```markdown
   ## [YYYY-MM-DD] lint | Wiki Health Check
   - **Status**: <Kondisi umum wiki>
   - **Findings**: <Ringkasan temuan link rusak, orphan, dll>
   - **Actions Taken / Recommended**: <Langkah perbaikan>
   ```

---

## 📁 Struktur Direktori Standar

```text
c:\secondBrain\
├── .obsidian/                    # Konfigurasi Obsidian
├── .agents/
│   └── skills/
│       └── llm-wiki/
│           ├── SKILL.md          # Instruksi skill ini
│           └── resources/        # Template catatan
├── raw/                          # Layer 1: Dokumen mentah asli (Immutable)
│   ├── README.md
│   └── assets/                   # Gambar lampiran
├── wiki/                         # Layer 2: Pengetahuan yang dikelola AI
│   ├── sources/                  # Ringkasan per sumber dokumen
│   ├── concepts/                 # Halaman konsep & tema
│   ├── entities/                 # Halaman tokoh, buku, tools, organisasi
│   └── synthesis/                # Sintesis lintas-topik & perbandingan
├── index.md                      # Layer 3: Master Map of Content (Katalog)
├── log.md                        # Layer 3: Catatan kronologis append-only
├── agent.md                      # Schema & aturan agent
└── AGENTS.md                     # Aturan agent (standar Antigravity)
```
