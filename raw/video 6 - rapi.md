# Video 6 — Instalasi Ruang Mission Control 3D

## Update Mission Control

Pada video sebelumnya dibahas cara membuat dashboard atau Mission Control sendiri menggunakan AI Agent. Repository dan prompt pack juga sudah dibagikan agar pengguna dapat langsung menggunakan Mission Control tanpa membangun semuanya dari awal.

Pada versi sebelumnya, Mission Control masih menggunakan tampilan dua dimensi. Repository tersebut kini sudah mengalami perubahan besar dan menyediakan tampilan tiga dimensi yang lebih interaktif.

Mission Control versi baru ini diberi nama Ruang. Repository-nya bersifat publik sehingga source code dapat disalin dan digunakan untuk kebutuhan sendiri.

## Prasyarat

Sebelum menginstal Ruang Mission Control, pastikan:

- Hermes Agent sudah tersedia.
- Hermes Agent sudah berjalan.
- Hermes Agent sudah terintegrasi dengan Telegram.
- Hermes berjalan di VPS atau perangkat lokal.

Model yang digunakan juga sebaiknya cukup baik. Jika sudah terintegrasi dengan OpenAI atau Codex, pilih model yang sesuai. Model yang lebih rendah dari provider tersebut juga masih dapat digunakan untuk proses instalasi.

## Menginstal Ruang Mission Control

Pertama, buka repository Ruang Mission Control di GitHub dan salin URL repository tersebut.

Kemudian, buka Telegram dan berikan URL repository kepada AI Agent dengan instruksi sederhana:

Instal atau pasang project ini. Pastikan project berjalan secara lokal. Setelah selesai, berikan alamat dan port tempat project ini berjalan.

AI Agent akan:

1. Membaca repository.
2. Membaca instruksi instalasi.
3. Memeriksa dependensi.
4. Menjalankan perintah instalasi.
5. Menjalankan project.
6. Memberikan alamat dan port project.

Repository biasanya sudah berisi informasi mengenai:

- Cara instalasi.
- Perintah untuk menjalankan project.
- Dependensi yang diperlukan.
- Cara penggunaan.

Karena AI Agent membaca instruksi di repository, proses instalasi dapat dilakukan sesuai dokumentasi yang tersedia.

## Mengakses Mission Control dari VPS

Jika Ruang Mission Control diinstal pada komputer lokal yang sama dengan Hermes, biasanya tidak ada masalah network.

Namun, jika Hermes dan Ruang Mission Control berjalan di VPS, sedangkan browser dibuka dari komputer lokal, keduanya berada di network yang berbeda. URL localhost dari VPS tidak dapat langsung dibuka dari komputer lokal.

Termius dapat digunakan untuk membuat port forwarding dari VPS ke komputer lokal.

## Membuat Port Forwarding dengan Termius

Pada contoh ini Hermes berjalan di VPS Sumopod dan sudah terhubung ke Termius.

Langkahnya:

1. Buka Termius.
2. Pastikan host VPS sudah tersedia.
3. Buka host tersebut dan pastikan koneksi berjalan.
4. Buka menu port forwarding.
5. Pilih New Forwarding.
6. Pilih Local.
7. Masukkan bind address 127.0.0.1.
8. Masukkan port Mission Control, pada contoh ini 3001.
9. Pilih host tempat VPS Hermes berjalan.
10. Masukkan destination address 127.0.0.1.
11. Masukkan destination port 3001.
12. Beri label, misalnya Ruang Mission Control.
13. Tekan Done.

Setelah forwarding dibuat, klik atau double-click forwarding tersebut untuk menjalankannya. Tunggu sampai indikator berubah menjadi biru.

Jika indikator sudah biru, kembali ke browser dan reload URL Mission Control. Ruang Mission Control seharusnya sudah dapat diakses.

## Office 3D

Setelah berhasil dibuka, Mission Control menampilkan Office 3D untuk AI Agent.

Tampilan Office dibuat dengan nuansa Indonesia, lengkap dengan bendera dan area santai.

Setiap area merepresentasikan status agent. Contohnya:

- Agent yang sedang bekerja berada di workstation.
- Agent yang idle dapat berada di area santai.
- Agent yang tidak aktif dapat berada di area istirahat.
- Agent yang sedang menjalankan schedule job terlihat aktif di area kerjanya.

Area tersebut bukan sekadar animasi. Status visual harus mencerminkan status agent yang sebenarnya.

Jika jumlah agent bertambah, agent yang sedang idle dapat berada di area lain, termasuk lantai atas yang memiliki kamar dan balkon.

## Mode Dua Dimensi dan Tiga Dimensi

Ruang Mission Control menyediakan mode dua dimensi dan tiga dimensi.

Mode dua dimensi adalah versi sebelumnya. Mode tiga dimensi memberikan pengalaman visual yang lebih interaktif.

Pengguna dapat berpindah dari tampilan dua dimensi ke tiga dimensi sesuai kebutuhan.

## Fitur Ruang Mission Control

Ruang Mission Control tidak hanya menampilkan Office 3D. Di dalamnya terdapat beberapa fitur operasional.

### Kanban Board

Kanban digunakan untuk melihat task yang dimiliki agent.

Status task dapat berupa:

- To do.
- Ready.
- In progress.
- Selesai.

Dengan Kanban, kita dapat melihat detail pekerjaan yang sedang dikerjakan agent.

### Calendar

Calendar menampilkan schedule dari tiap AI Agent. Dari sini kita dapat melihat jadwal yang akan dijalankan.

### Token Usage

Mission Control dapat memantau konsumsi token tiap agent.

Informasi ini membantu melihat agent mana yang menggunakan token paling banyak.

Pada environment demo, konsumsi token tidak terlalu besar. Namun, data tersebut tetap berguna untuk memantau penggunaan model.

Token usage dapat difilter berdasarkan tanggal atau periode tertentu, misalnya 24 jam terakhir.

### Dark Mode

Tampilan Mission Control dapat diubah ke dark mode sesuai preferensi pengguna.

### Panel Statistik

Panel menampilkan:

- Statistik penggunaan.
- Agent yang aktif.
- Jumlah agent.
- Activity log.

### Daftar Agent

Menu agent digunakan untuk melihat semua agent yang tersedia.

### Usage

Menu usage menampilkan informasi penggunaan token, sama seperti bagian token usage.

### Board dan Calendar

Board dan calendar juga tersedia melalui menu tersendiri agar task dan schedule dapat dibuka dengan lebih mudah.

### Activity

Activity menampilkan aktivitas yang baru terjadi pada AI team.

### Memory

Menu memory digunakan untuk memeriksa memory masing-masing agent.

Dengan fitur ini, kita dapat melihat informasi yang tersimpan pada memory agent tanpa harus membukanya melalui Termius.

### Folder

Menu folder digunakan untuk mengakses folder kerja agent, seperti ketika mengakses folder melalui Termius.

### Log

Menu log menampilkan error atau catatan aktivitas sistem. Jika terjadi masalah, log dapat digunakan untuk membantu proses pemeriksaan.

## Keamanan Mission Control

Menu Settings menyediakan beberapa fitur keamanan.

### Access Code

Access code digunakan untuk melindungi URL Mission Control. Jika access code diaktifkan, pengguna harus memasukkan kode sebelum dapat membuka isi Mission Control.

Access code dapat dibuat sendiri atau dihasilkan oleh sistem. Simpan kode tersebut dengan aman.

### Profile Lock

Profile lock digunakan untuk mengunci profile agent tertentu.

Contohnya, profile lead engineer mungkin berisi data kritikal. Profile tersebut dapat dikunci agar tidak sembarang orang dapat melihat datanya.

Langkahnya:

1. Pilih agent yang ingin dikunci.
2. Masukkan PIN.
3. Verifikasi PIN.
4. Aktifkan profile lock.

Access code melindungi seluruh Ruang Mission Control, sedangkan profile lock melindungi agent tertentu.

## Penutup

Ruang Mission Control dapat digunakan untuk membantu mengelola AI team dan memantau pekerjaan mereka.

Dengan menggabungkan Office 3D, Kanban, Calendar, Activity, Memory, Folder, Log, dan fitur keamanan, Mission Control menjadi portal operasional untuk AI team.

Untuk membangun AI team pertama, mulailah dari kebutuhan bisnis dan pekerjaan sehari-hari. Mission Control dapat dikembangkan sesuai kebutuhan tersebut.
