# Video 5 — Membangun Mission Control untuk AI Team

## Apa Itu Mission Control?

Mission Control adalah tools yang dibuat khusus untuk membantu mengelola dan memantau AI team.

Mission Control bukan aplikasi bawaan Hermes yang cukup diinstal. Ini adalah tools tambahan yang dibangun sesuai kebutuhan AI team.

Dengan Hermes, kita tidak hanya dapat membuat Mission Control. Kita juga dapat membuat:

- Dashboard lain.
- Tools operasional.
- Aplikasi internal.
- Fitur khusus untuk kebutuhan AI team.

Mission Control dibangun dari awal, mulai dari:

1. Menentukan kebutuhan.
2. Membuat requirement.
3. Mendelegasikan pekerjaan kepada agent.
4. Menjalankan proses development menggunakan OpenCode.

Repository dan prompt pack Mission Control juga dapat dibagikan agar pengguna lain dapat membuat versi sesuai kebutuhannya.

## Perbedaan Hermes Dashboard dan Mission Control

Hermes dapat dianggap sebagai environment tempat AI Agent bekerja. Seiring waktu, kita mungkin memiliki banyak role agent, seperti:

- Finance.
- Marketing.
- Operasional.
- Sales.

Setiap agent memiliki workflow dan schedule masing-masing.

Hermes Dashboard berfokus pada konfigurasi dan pengaturan agent Hermes.

Mission Control berfokus pada operasional, yaitu membantu memantau apa yang sedang dikerjakan AI team.

Semakin banyak agent yang dimiliki, semakin banyak pekerjaan yang berlangsung di belakang layar. Mission Control membantu kita melihat pekerjaan tersebut.

## Mulai dari Kebutuhan, Bukan Coding

Kesalahan yang sering terjadi adalah langsung memberikan instruksi panjang seperti:

Buatkan saya Mission Control.

Hasilnya mungkin berupa aplikasi, tetapi kita belum tentu memahami fitur yang dibuat dan alasan fitur tersebut diperlukan.

Sebelum coding, tentukan terlebih dahulu definisi dan kebutuhan produk.

Empat pertanyaan awal yang perlu dijawab:

1. Siapa yang akan menggunakan produk?
2. Masalah apa yang ingin diselesaikan?
3. Informasi apa yang ingin ditampilkan?
4. Fitur atau action apa yang ingin dibangun?

Prinsipnya, jangan mulai dari coding. Mulailah dari kebutuhan.

## MVP Mission Control

Pada versi awal, Mission Control tidak perlu terlalu kompleks. Mulai dari kebutuhan dasar.

### 1. Dashboard

Dashboard digunakan untuk melihat:

- Jumlah agent.
- Task yang sedang aktif.
- Task yang sudah selesai.
- Schedule berikutnya.
- Activity terakhir.

### 2. Agent

Bagian agent digunakan untuk melihat:

- Agent yang dimiliki.
- Role setiap agent.
- Responsibility setiap agent.
- Konfigurasi setiap agent.

### 3. Board

Board digunakan untuk memonitor pekerjaan tiap agent, misalnya:

- To do.
- Ready.
- In progress.
- Backlog.
- Review.
- Selesai.

Dengan board, task yang dikerjakan tidak hilang dan progresnya dapat dilacak.

### 4. Calendar

Karena agent bersifat proaktif dan memiliki banyak schedule, kita perlu melihat jadwal yang akan dieksekusi tiap agent.

### 5. Activity

Activity digunakan untuk melihat kejadian terbaru, seperti:

- Task yang baru selesai.
- Error.
- Perubahan.
- Aktivitas lain yang baru dilakukan AI team.

### 6. Memory atau Knowledge

AI team memiliki persistent memory, knowledge, skill, dan dokumen. Mission Control dapat digunakan untuk memonitor dokumen serta skill tiap agent.

### 7. Office

Office adalah fitur visual untuk melihat status agent.

Office bukan fitur yang paling penting. Tanpa Office, Mission Control tetap dapat berjalan.

Namun, Office memberikan cara yang lebih mudah untuk melihat agent yang:

- Sedang bekerja.
- Idle.
- Berada di area tertentu.
- Sedang off atau beristirahat.

Status visual harus merepresentasikan status agent yang sebenarnya. Jika agent sedang bekerja, karakter harus berada di workstation. Jika idle, statusnya juga harus idle.

Office bukan sekadar dekorasi.

## Struktur Agent untuk Development

Pada contoh ini digunakan struktur sederhana:

1. Lead Agent.
2. Lead Engineer Agent.

Untuk struktur yang lebih besar, dapat ditambahkan Product Manager Agent.

Pembagian tugasnya:

- Business owner memberikan kebutuhan.
- Lead Agent memahami tujuan besar dan berkomunikasi dengan business owner.
- Lead Agent mendelegasikan pekerjaan kepada Lead Engineer.
- Lead Engineer membuat product specification dan implementation plan.
- OpenCode mengerjakan development.

Lead Engineer di Hermes tidak langsung mengerjakan seluruh coding. Tugasnya adalah memahami requirement, memecahnya menjadi task, mendelegasikan pekerjaan, dan me-review hasil.

## OpenCode

OpenCode adalah framework open source untuk membangun aplikasi dengan bantuan AI.

Membangun aplikasi bukan hanya menghasilkan code. AI juga perlu:

- Membaca codebase.
- Melakukan inspect.
- Mengedit code.
- Menjalankan aplikasi.
- Melakukan testing.
- Memperbaiki error.

Framework seperti Claude Code dan Codex juga dirancang untuk membantu AI melakukan proses coding tersebut.

OpenCode bersifat open source dan dapat menggunakan berbagai model dari provider yang berbeda. Hal ini membuatnya lebih fleksibel.

OpenCode secara default sudah menjadi bundle atau sudah tersedia di Hermes. Namun, OpenCode perlu diaktifkan pada agent yang akan digunakan.

Pastikan:

- Hermes Agent sudah tersedia.
- Hermes Agent sudah terintegrasi dengan Telegram.
- Lead Engineer Agent sudah dibuat.

## Membuat Lead Engineer Agent

Buka Hermes Dashboard, lalu:

1. Masuk ke bagian Profile.
2. Pilih Create Profile.
3. Beri nama profile, misalnya lead engineer.
4. Pilih apakah konfigurasi akan di-clone.
5. Buat profile.
6. Restart gateway.

Setelah gateway berjalan, switch ke profile lead engineer. Uji dengan pesan:

Halo, apakah kamu siap?

Jika agent membalas, berarti profile lead engineer sudah berjalan.

Prompt dan instruksi berikutnya dikirim melalui Telegram agar lebih praktis.

## Mengaktifkan OpenCode

Berikan instruksi kepada lead engineer:

Periksa apakah OpenCode sudah siap. Jika belum, instal dan aktifkan OpenCode mengikuti dokumentasi yang tersedia.

Agent akan membaca skill dan dokumentasi, lalu menjalankan langkah yang diperlukan.

Jika ada approval yang diminta, berikan persetujuan agar proses instalasi atau aktivasi selesai.

Perbedaan pentingnya:

- Lead Engineer mengorkestrasi pekerjaan.
- Lead Engineer membuat planning.
- OpenCode mengeksekusi pekerjaan coding.

## Arsitektur dan Development Cycle

Alur arsitekturnya:

1. Business owner memberikan kebutuhan.
2. Lead Agent memahami tujuan.
3. Lead Agent memberikan task kepada Lead Engineer.
4. Lead Engineer memecah pekerjaan engineering.
5. OpenCode melakukan implementasi.

Development cycle-nya:

1. Kebutuhan.
2. Lead Agent.
3. Lead Engineer.
4. Product specification.
5. Implementation plan.
6. OpenCode.
7. Build.
8. Run.
9. Test.
10. Fix.

## Login OpenCode dengan Codex

Setelah OpenCode siap, OpenCode dapat meminta proses login.

Pada contoh ini digunakan subscription Codex atau ChatGPT. Instruksikan kepada agent agar menggunakan subscription Codex.

Pastikan akun ChatGPT yang digunakan memiliki subscription yang mendukung Codex, minimal paket Pro sesuai kebutuhan tutorial.

Agent akan memberikan:

- URL autentikasi.
- Kode autentikasi.

Buka URL tersebut, masukkan kode, dan pastikan proses login berhasil. Setelah berhasil, OpenCode dapat menggunakan model melalui subscription ChatGPT atau Codex.

## Prompt Pack Mission Control

Prompt pack dibuat secara bertahap, bukan satu prompt raksasa. Tujuannya agar kita dapat melihat hasil setiap tahap dan melakukan koreksi jika diperlukan.

Prompt pack terdiri dari beberapa bagian, mulai dari:

- Perencanaan Mission Control.
- Pembangunan MVP.
- Pembuatan Office.
- Review dan perbaikan.
- Kustomisasi.

### Prompt Pack 1 — Planning

Prompt pertama diberikan kepada Lead Agent untuk menjelaskan rencana pembangunan.

Isi rencana mencakup:

- Tujuan Mission Control.
- Dashboard.
- Agent.
- Board.
- Office.
- Acceptance criteria.
- Fitur MVP.

Kirim prompt pertama melalui Telegram dan tunggu sampai Lead Agent membuat plan.

Pastikan model yang digunakan cukup baik. Model gratis dapat menghasilkan pekerjaan yang kurang konsisten. Pada contoh ini digunakan model OpenAI yang disebut GPT 5.6.

Output yang diharapkan:

- Lead Agent memahami MVP.
- Fitur yang akan dibuat jelas.
- Acceptance criteria tersedia.
- Rencana implementasi dapat ditinjau.

Jika hasilnya sudah sesuai, lanjutkan ke prompt kedua.

### Prompt Pack 2 — Build MVP

Prompt kedua memulai proses coding.

Peran tiap agent dijelaskan sebagai berikut:

- Lead Agent mengatur konteks besar.
- Lead Engineer membuat perencanaan dan melakukan review.
- OpenCode mengerjakan development.

OpenCode akan:

1. Membaca repository.
2. Memeriksa code yang sudah ada.
3. Mengimplementasikan modul.
4. Menjalankan aplikasi.
5. Menjalankan testing.
6. Memperbaiki error.
7. Menjalankan testing kembali.

Proses dapat berlangsung beberapa menit atau lebih, tergantung kompleksitas aplikasi.

Setelah selesai, agent akan memberikan laporan mengenai:

- Modul yang sudah dibangun.
- Dashboard.
- Agent.
- Board.
- Navigation.
- Placeholder Office.
- Hasil testing.
- URL aplikasi.

Hasil tiap pengguna tidak harus sama karena menggunakan generative AI. Yang penting fitur dan acceptance criteria terpenuhi.

## Mengakses Mission Control melalui VPS

Jika URL aplikasi dibuka langsung dari komputer lokal, aplikasi mungkin tidak dapat diakses karena aplikasi berjalan di VPS, sedangkan browser digunakan dari komputer lokal.

Keduanya berada di network yang berbeda. Termius dapat digunakan untuk membuat port forwarding.

Sebelum membuat forwarding, minta agent memberikan alamat dan port tempat Mission Control berjalan.

Contoh alamat dan port:

127.0.0.1:5173

### Konfigurasi Port Forwarding

1. Buka Termius.
2. Buat new forwarding.
3. Pilih Local.
4. Masukkan local port dan bind address sesuai informasi agent.
5. Gunakan bind address 127.0.0.1.
6. Pilih host tempat Hermes Agent berjalan.
7. Masukkan destination address 127.0.0.1.
8. Masukkan destination port, misalnya 5173.
9. Beri nama, misalnya YouTube Mission Control.
10. Simpan konfigurasi.
11. Start forwarding.

Forwarding harus berubah menjadi biru agar aktif.

Setelah aktif, buka kembali URL dari browser dan refresh halaman. Mission Control seharusnya sudah dapat diakses.

## Prompt Pack 3 — Membuat Office 2D

Prompt ketiga digunakan untuk membangun Office visual bergaya pixel art dua dimensi.

Kirim:

- Prompt Office.
- Screenshot contoh visual.
- Instruksi agar agent mengimplementasikan task sampai selesai.

Screenshot dapat digunakan sebagai referensi visual agar agent memahami tampilan yang diharapkan.

Pembangunan aplikasi dengan AI tidak selalu selesai dalam satu kali prompt. Proses yang normal adalah:

1. Build.
2. Review.
3. Memberikan feedback.
4. Improve.
5. Test kembali.

Jika avatar belum tampil atau status agent masih terbaca unknown, berikan instruksi perbaikan kepada agent.

Setelah perbaikan, refresh halaman dan periksa kembali:

- Karakter pixel sudah tampil.
- Lead Agent tampil.
- Lead Engineer tampil.
- OpenCode tampil.
- Status agent sudah benar.

Uji status dengan mengirimkan pesan kepada Lead Agent. Jika agent mulai bekerja, statusnya seharusnya berubah dari idle atau off menjadi aktif dan berpindah ke workstation.

## Prompt Pack 4 — Review dan Fix

Prompt keempat digunakan untuk meminta Lead Agent melakukan review menyeluruh terhadap Mission Control.

Fungsinya:

- Memeriksa error.
- Menguji fitur.
- Memperbaiki masalah.
- Mendelegasikan perbaikan kepada agent terkait.

Jangan langsung membangun banyak fitur sekaligus. Mulailah bertahap berdasarkan kebutuhan bisnis.

Contohnya:

- Finance tool untuk review invoice.
- Finance tool untuk approval invoice.
- Marketing tool untuk approval konten.
- Sales tool untuk monitoring lead.

Mission Control tiap pengguna seharusnya berbeda karena dibuat berdasarkan kebutuhan bisnis masing-masing.

## Prompt Pack 5 — Kustomisasi

Prompt kelima digunakan jika ingin mengembangkan Mission Control lebih lanjut.

Agent dapat membimbing proses berdasarkan area yang ingin dibangun, misalnya:

- Marketing.
- Sales.
- Finance.
- Operasional.

Berikan instruksi kustomisasi kepada agent. Agent akan membimbing proses tahap demi tahap.

## Alur Keseluruhan

Business owner memiliki tujuan bisnis. Hermes atau Lead Agent berfungsi sebagai orkestrator.

Lead Agent menangani kebutuhan dan product specification. Lead Engineer memecah requirement menjadi pekerjaan teknis. OpenCode menjalankan coding, build, run, testing, dan perbaikan.

Alur ini menghasilkan Mission Control yang sesuai dengan kebutuhan AI team.

Hal yang paling penting bukan hanya Mission Control atau Office visualnya. Yang perlu dipelajari adalah bahwa AI Agent dapat membantu membangun tools sesuai kebutuhan bisnis sendiri.

Jangan berhenti pada contoh Mission Control. Eksplorasi dan bangun tools yang sesuai dengan kebutuhan AI team masing-masing.
