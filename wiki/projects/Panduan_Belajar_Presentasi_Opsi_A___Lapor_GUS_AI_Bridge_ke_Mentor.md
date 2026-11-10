# Panduan Belajar: Presentasi Opsi A — Lapor GUS AI Bridge & Web Triage ke Mentor Diskominfo

## 1. Pembuka: Pertanyaan Pembuka ke Mentor

Mulai dengan pertanyaan konfirmasi terkait tata kelola pengaduan masyarakat sebelum menjelaskan sistem. Tujuannya untuk memvalidasi alur birokrasi dan menunjukkan kamu paham proses bisnis SPBE.

**Pertanyaan pertama:**

> *"Sebelum saya menjelaskan proposal kami, izinkan saya bertanya agar tidak salah arah Bu/Pak. Kemarin pas riset, saya melihat Pemkab Gresik punya kanal pengaduan masyarakat seperti Lapor GUS dan GoWA — apakah pusat pengelolaan dan rekap aduannya memang berada di bawah Diskominfo?"*

**Kalau mentor mengonfirmasi → lanjut:**

> *"Baik, dan apakah dalam praktiknya pesan dari warga yang masuk via WhatsApp itu formatnya masih campur aduk (banyak curhat tidak terstruktur), sehingga admin di sini harus membaca manual satu per satu sebelum memilah dan menginputnya ke portal Service Desk dinas?"*

**Kalau mentor mengonfirmasi lagi → baru masuk penjelasan sistem.**

Logika pendekatan ini: kamu mendudukkan masalah operasional staf (beban sortir manual) sebelum menawarkan solusi perangkat lunak.

---

## 2. Penjelasan Sistem: Alur Triage Dua Sisi

Setelah mentor mengonfirmasi repotnya menyortir aduan warga, masuk ke penjelasan sistem.

**Kalimat pembuka yang bisa dipakai:**

> *"Pas sekali Bu/Pak, di proposal opsi A kami merancang prototipe bernama **Lapor GUS AI Bridge & Web Triage Dashboard**. Intinya sistem ini membantu admin merapikan, mengklasifikasikan, dan mendisposisikan aduan warga secara semi-otomatis."*

---

### Sisi Warga — WhatsApp Parser & Intake
Warga sering melapor dengan bahasa emosional, panjang lebar, dan tanpa data jelas (misal: "jalan rusak parah tolong diperbaiki" tanpa sebut lokasi).
- AI bertindak sebagai asisten penerima: memilah informasi inti (Apa masalahnya, Di mana lokasinya, Siapa pelapornya).
- Jika informasi belum lengkap (misal: foto bukti atau RT/RW belum ada), sistem meminta kelengkapan secara sopan sebelum diteruskan.

### Sisi Admin — Web Dashboard Triage (Human-in-the-Loop)
Aduan yang sudah rapi masuk ke antrean Web Dashboard:
- **Rekomendasi Dinas Tujuan:** AI menyarankan dinas penanggung jawab (contoh: jalan berlubang ➔ DPUTR, lampu padam ➔ Dishub, sampah menumpuk ➔ DLH).
- **Tingkat Urgensi:** Membedakan laporan darurat (pohon tumbang halangi jalan) vs reguler.
- **Fitur Satu-Klik Salin (One-Click Copy):** Admin cukup menekan satu tombol untuk menyalin teks yang sudah terformat rapi sesuai kolom form portal *Service Desk* Pemkab Gresik.

---

## 3. Mekanisme Integrasi & Keamanan (Jawaban Pertanyaan 1)

Pertanyaan yang kemungkinan besar ditanya mentor:  
*"Apakah sistem ini langsung menembak database portal Service Desk resmi Pemkab, atau bagaimana alurnya?"*

**Jawaban tegas: Tidak menembak langsung (Prinsip Zero-Risk):**

> *"Kami menerapkan prinsip **Human-in-the-Loop**, Pak/Bu. Sistem kami sengaja tidak melakukan direct API/database injection ke server Service Desk resmi Pemkab, demi menjaga integritas data dan keamanan sistem internal.*  
> 
> *Admin tetap menjadi pemegang kendali penuh. AI hanya bertindak sebagai 'juru ketik dan penyortir pintar'. Ketika admin menyetujui draf di dashboard, tersedia format ringkas yang siap dipaste ke Service Desk dalam hitungan detik."*

**Kenapa ini poin plus besar di mata dinas:**
- Instansi pemerintah sangat sensitif terhadap risiko kerusakan database produksi.
- Pendekatan jembatan perantara (*bridge*) dinilai sangat aman dan realistis untuk tugas magang 1 bulan.

---

## 4. Efisiensi Jam Kerja & Klasifikasi AI (Jawaban Pertanyaan 2)

Pertanyaan kedua yang kemungkinan ditanya:  
*"Aduan warga masuk 24 jam termasuk tengah malam dan hari libur. Bagaimana sistem menangani ini jika staf kantor sedang libur?"*

**Jawaban:**

> *"Justru di situ nilai tambah utamanya, Pak/Bu:*  
> 1. ***Respon Instan 24/7:*** *Saat kantor tutup (malam atau akhir pekan), warga tetap langsung dilayani oleh asisten WhatsApp dan mendapatkan tiket tanda terima sementara bahwa aduannya tercatat.*  
> 2. ***Antrean Siap Kerja di Pagi Hari:*** *Saat petugas kantor masuk jam 08.00 pagi, mereka tidak perlu membaca tumpukan chat panjang. Di dashboard sudah tersaji daftar aduan yang sudah terangkum rapi per kategori dinas, siap diverifikasi dan diteruskan."*

---

## 5. Pertanyaan Lanjutan yang Perlu Disiapkan

Siapkan jawaban untuk dua pertanyaan operasional ini:

### Pertanyaan A — Pengujian WhatsApp (Nomor Dinas Resmi)
> *"Kanal WhatsApp dinas kan nomor resmi pemkab, bagaimana cara kalian mengujinya tanpa mengganggu nomor dinas yang sedang jalan?"*

**Jawaban:**  
*"Untuk pengujian magang, kami menggunakan nomor pengujian terpisah (sandbox environment / nomor khusus tim magang). Kami tidak akan menyentuh atau memindai nomor WhatsApp dinas resmi sampai prototipe terbukti stabil dan diizinkan oleh pembimbing."*

### Pertanyaan B — Pelaporan & Analitik Pimpinan
> *"Selain memilah tiket, apakah dashboard bisa menampilkan rekap untuk laporan ke pimpinan?"*

**Jawaban:**  
*"Bisa Pak/Bu. Di dashboard kami sediakan grafik rekapitulasi: total aduan masuk mingguan/bulanan, dinas mana yang paling sering menerima aduan, serta status laporan (Menunggu Verifikasi, Diteruskan ke OPD, Selesai)."*

---

## 6. Tips Presentasi Khusus Opsi A

1. **Bantu Staf, Bukan Gantikan Staf:**  
   Jangan gunakan kata *"AI akan menggantikan peran admin"*. Gunakan kalimat: *"AI meringankan beban administrasi staf agar tidak lelah mengetik dan memilah ratusan chat manual."*
2. **Kesesuaian Syarat Akademik:**  
   Tegaskan bahwa output proyek ini adalah **Web Dashboard CRUD** lengkap dengan database relasional (PostgreSQL/MySQL), sesuai syarat mutlak mata kuliah Tugas Khusus kampus.
3. **Fleksibilitas:**  
   Jika mentor ternyata lebih tertarik pada opsi keamanan web (Subdomain Guard) atau tugas internal lain, langsung ikuti arah mentor.
