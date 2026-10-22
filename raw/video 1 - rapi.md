# Video 1 — Pengenalan Hermes AI Agent dan Persiapan Instalasi

Halo, guys. Selamat datang di channel gue. Ini adalah video YouTube gue yang pertama.

Fokus gue di sini adalah membahas bagaimana AI Agent bisa membantu kalian menjalankan bisnis dan usaha. Jadi, ketika menggunakan AI, kalian bukan hanya sekadar bertanya, tetapi juga bisa memiliki AI yang membantu kalian bekerja selama 24 jam setiap hari tanpa henti.

## Topik yang Akan Dibahas

Ada beberapa topik yang akan dibahas:

1. Penjelasan mengenai Agent, ChatGPT, Hermes, dan istilah terkait lainnya.
2. Prasyarat yang perlu disiapkan.
3. Instalasi Hermes.
4. Setup Hermes.
5. Pembuatan sandbox workspace agar lebih aman.
6. Integrasi dengan Google Sheets.

Untuk bisnis yang masih baru atau dalam tahap awal, sebagian besar data biasanya masih menggunakan Google Sheets, belum menggunakan database besar seperti pada skala enterprise.

## Perbedaan AI Agent dan ChatGPT

Apa sebenarnya AI Agent itu? Apa perbedaannya dengan ChatGPT?

Perbedaannya dapat dilihat dari dua hal:

1. Sistem yang digunakan.
2. Cara kerjanya.

### Perbedaan dari Sisi Sistem

AI Agent bekerja pada perangkat milik kita sendiri, misalnya mini PC atau VPS. Karena sistemnya berjalan pada perangkat kita sendiri, kita memiliki kendali penuh terhadap AI Agent tersebut.

Sementara itu, ChatGPT bekerja pada sistem cloud milik OpenAI. Meskipun sekarang ChatGPT juga mulai memiliki fitur seperti Work, sistemnya tetap belum sekuat AI Agent seperti Hermes atau OpenClaw.

Dengan demikian, AI Agent memberikan kontrol yang lebih besar, sedangkan ChatGPT atau Claude memiliki kontrol yang lebih terbatas.

Mengapa kontrol penuh diperlukan?

Jika kita ingin AI melakukan banyak pekerjaan, seperti mengedit file, mengedit video, membuat video, atau menjalankan tugas lain, AI memerlukan akses yang luas. Saat menggunakan ChatGPT, kita mungkin bisa memanfaatkan beberapa koneksi atau plugin. Namun, jika plugin atau koneksi yang dibutuhkan tidak tersedia, eksekusi tersebut tidak dapat dilakukan.

AI Agent dapat dianalogikan seperti seorang pegawai yang kita rekrut. Kemudian, kita memberikan komputer kepada pegawai tersebut. Setelah memiliki komputer, ia dapat melakukan berbagai pekerjaan di dalam komputer itu.

Perbedaannya, pegawai tersebut bukan manusia, melainkan AI Agent.

### Perbedaan dari Sisi Cara Kerja

Karena berjalan pada perangkat sendiri, AI Agent dapat bekerja secara otonom dan otomatis. AI Agent juga dapat bersifat proaktif.

Artinya, AI Agent tidak selalu harus menunggu perintah dari kita. Ia dapat berjalan di latar belakang, menyelesaikan pekerjaan, dan memberikan notifikasi secara proaktif.

ChatGPT memang memiliki fitur jadwal, tetapi belum sekuat AI Agent seperti Hermes atau OpenClaw. Cara kerja ChatGPT cenderung reaktif, yaitu harus diberikan perintah terlebih dahulu sebelum bekerja.

Jadi, perbedaan antara ChatGPT dan AI Agent seperti Hermes atau OpenClaw dapat dilihat dari:

- Sistem yang digunakan.
- Cara kerjanya.
- Tingkat kendali.
- Tingkat otonomi dan proaktivitas.

## Apa Itu Hermes?

Hermes adalah framework atau sistem yang memungkinkan AI Agent bekerja dengan dua karakteristik utama:

1. Memiliki kendali penuh karena berjalan pada perangkat sendiri.
2. Dapat bekerja secara otonom dan proaktif.

Hermes memiliki konsep yang mirip dengan OpenClaw. Namun, pada video ini, Hermes digunakan karena dianggap lebih stabil.

## Prasyarat Sebelum Instalasi Hermes

Sebelum menginstal Hermes, ada beberapa hal yang perlu disiapkan.

### 1. Perangkat

Pertama, kita harus menentukan AI Agent akan dijalankan di mana.

Beberapa pilihan yang tersedia:

- Komputer pribadi.
- Mini PC.
- Mac Mini.
- VPS.

Untuk pemula, penggunaan VPS direkomendasikan karena kita tidak perlu membeli perangkat sendiri. Jika menggunakan mini PC atau Mac Mini, perangkat tersebut harus menyala selama 24 jam dan terus terhubung ke listrik.

Dengan VPS, kita cukup menyewa server. Saat ini juga sudah tersedia VPS yang menyediakan sistem operasi dengan Hermes yang sudah terinstal.

Pada video ini, perangkat yang digunakan adalah VPS.

### 2. AI Model

Setelah memiliki perangkat, kita membutuhkan AI model.

Untuk tahap awal, OpenRouter direkomendasikan karena menyediakan berbagai model gratis dan berbayar. Kita dapat menggunakan model gratis terlebih dahulu, misalnya model dari NVIDIA seperti Nemotron.

Pada tahap ini, model AI akan digunakan melalui OpenRouter.

### 3. Google Account dan Google Drive

Kita juga memerlukan Google Account karena nantinya akan menggunakan Google Drive sebagai sandbox.

Karena AI Agent akan bekerja secara otonom selama 24 jam, kita harus memastikan bahwa AI Agent tidak dapat mengakses data penting yang seharusnya tidak boleh diakses atau diubah.

Google Drive dapat digunakan untuk menyediakan ruang kerja yang terpisah dan lebih aman.

### 4. Google Sheets

Google Sheets digunakan sebagai contoh tempat AI Agent berinteraksi dengan data.

Untuk pelaku bisnis yang baru memulai, Google Sheets biasanya masih cukup digunakan untuk mencatat dan merekap data. Kita belum harus menggunakan database kompleks seperti pada sistem enterprise.

### 5. Google Apps Console

Kita perlu membuat kredensial dari Google Account atau Google Drive yang nantinya akan diakses oleh AI Agent.

Untuk itu, kita akan menggunakan Google Apps Console.

### 6. Google Workspace CLI

Google Workspace CLI, atau GWS CLI, digunakan untuk membantu integrasi dengan layanan Google Workspace, termasuk:

- Google Drive.
- Google Sheets.
- Layanan Google Workspace lainnya.

GWS CLI dikembangkan untuk memudahkan integrasi dengan Google Workspace.

### 7. Termius

Termius adalah aplikasi yang digunakan untuk mengakses VPS.

VPS tidak memiliki antarmuka seperti komputer pribadi. Sebagian besar pengelolaannya dilakukan melalui terminal. Termius membantu kita mengakses VPS dengan antarmuka yang lebih mudah digunakan.

### 8. Telegram

Telegram digunakan sebagai channel untuk berinteraksi dengan AI Agent.

Sebenarnya kita juga dapat menggunakan WhatsApp atau platform lain, tetapi Telegram dipilih karena:

- Gratis.
- Mudah membuat bot.
- Tidak membutuhkan setup yang terlalu kompleks.
- Dapat digunakan untuk membuat akun bot.

Jadi, prasyarat yang perlu disiapkan adalah:

1. VPS.
2. Hermes.
3. AI model melalui OpenRouter.
4. Google Account.
5. Google Drive.
6. Google Sheets.
7. Google Apps Console.
8. Google Workspace CLI.
9. Termius.
10. Telegram.

## Instalasi Hermes

Sumber utama Hermes berasal dari Nous Research. Di situs resminya juga tersedia panduan instalasi.

Hermes juga memiliki versi desktop. Namun, pada video ini, Hermes akan dijalankan pada VPS.

## Membuat VPS melalui Sumopod

Pada video ini, VPS dibuat melalui Sumopod.

Langkah umumnya:

1. Membuat akun Sumopod.
2. Masuk ke menu VPS.
3. Memilih opsi **Create**.
4. Memberi nama VPS, misalnya `Hermes Agent`.
5. Memilih provider.
6. Memilih region atau data center.
7. Memilih sistem operasi yang sudah memiliki Hermes.
8. Memilih server plan.
9. Membuat VPS.
10. Menunggu proses provisioning selesai.

Provider dan lokasi data center dapat memengaruhi harga serta latensi. Pada contoh ini tersedia provider seperti Tencent dan provider lainnya. Region Indonesia dapat dipilih agar latensinya lebih rendah.

Keuntungan memilih sistem operasi yang sudah memiliki Hermes adalah kita tidak perlu menginstal Hermes dari awal.

Pada contoh ini, server plan yang digunakan memiliki spesifikasi:

- 2 vCPU.
- 2 GB RAM.
- 40 GB storage.
- Harga sekitar Rp60.000 per bulan.

Spesifikasi tersebut dianggap cukup untuk penggunaan awal yang belum terlalu berat.

Setelah VPS selesai dibuat, kita dapat melihat:

- Public IP address.
- Private IP address.
- Username.
- Password.

Informasi tersebut digunakan untuk mengakses VPS.

## Menghubungkan VPS dengan Termius

Setelah VPS dibuat, kita menghubungkannya dengan komputer lokal menggunakan Termius.

Langkahnya:

1. Membuka Termius.
2. Memilih **New Host**.
3. Memasukkan public IP address VPS sebagai hostname.
4. Memberi nama host, misalnya `Hermes Agent`.
5. Memasukkan username.
6. Memasukkan password.
7. Menekan tombol **Connect**.

Setelah berhasil terkoneksi, kita dapat mengakses terminal VPS melalui Termius.

## Mengecek Instalasi Hermes

Jika kita memilih sistem operasi yang sudah menyediakan Hermes, Hermes seharusnya sudah terinstal.

Untuk mengeceknya, jalankan:

```bash
hermes status
```

Jika Hermes belum tersedia, kita perlu menginstalnya menggunakan panduan instalasi dari situs resmi Nous Research.

## Setup Hermes

Untuk memulai setup Hermes, jalankan:

```bash
hermes setup
```

Hermes menyediakan beberapa pilihan setup, seperti:

- Quick setup.
- Full setup.
- Blank state.
- Pilihan lainnya.

Pada video ini digunakan **Quick setup**.

Menu dapat dinavigasi menggunakan tombol panah atas dan bawah, kemudian tekan Enter untuk memilih.

Hermes meminta pengguna melakukan registrasi. Registrasi tersebut biasanya meminta pairing dengan akun dan kartu kredit apabila ingin menggunakan model langsung dari Hermes.

Namun, karena pada tutorial ini model akan digunakan melalui OpenRouter, proses tersebut dapat dilewati dengan menekan:

```text
Ctrl + C
```

Pada pilihan terminal backend, pilih backend lokal dengan opsi seperti:

```text
Keep current local
```

Kemudian tekan Enter.

Setup messaging atau channel dapat dilakukan nanti. Untuk tahap awal, Hermes akan dijalankan melalui terminal terlebih dahulu agar kita dapat memastikan instalasinya berhasil.

## Menghubungkan Hermes dengan OpenRouter

Untuk mengatur AI model, jalankan:

```bash
hermes model
```

Kemudian pilih provider AI model. Tersedia berbagai pilihan provider, termasuk:

- Nous.
- OpenRouter.
- Anthropic.
- Provider lainnya.

Pada tutorial ini digunakan **OpenRouter** agar kita dapat menggunakan model gratis terlebih dahulu.

### Membuat OpenRouter API Key

Langkahnya:

1. Membuat akun OpenRouter.
2. Membuka halaman OpenRouter.
3. Masuk ke bagian API Keys.
4. Memilih **New Key**.
5. Memberi nama key, misalnya `Hermes Demo`.
6. Menekan **Create**.
7. Menyalin API key yang ditampilkan.

API key tersebut harus disimpan dengan aman dan jangan dibagikan kepada orang lain.

Kembali ke Termius. Saat Hermes meminta OpenRouter API key, tempelkan key tersebut.

Pada Windows, jika `Ctrl + V` tidak berfungsi di terminal, gunakan:

```text
Ctrl + Shift + V
```

Setelah API key dimasukkan, Hermes akan menampilkan daftar model yang tersedia.

Jika ingin menggunakan model gratis, pilih model yang tidak memiliki harga penggunaan. Beberapa model gratis yang disebutkan adalah model NVIDIA Nemotron, termasuk varian Super dan Ultra.

Pada contoh ini digunakan model Nemotron Ultra dengan parameter besar, sekitar 550 miliar parameter, untuk pengujian awal.

## Menguji Hermes

Setelah model dipilih, kita dapat menguji Hermes melalui terminal.

Jalankan:

```bash
hermes chat
```

Kemudian kirim pesan sederhana, misalnya:

```text
Halo, kamu siapa?
```

Jika Hermes membalas, berarti:

- Hermes berhasil diinstal.
- AI model berhasil dikonfigurasi.
- OpenRouter berhasil dihubungkan.
- Hermes sudah dapat menerima dan menjawab pesan.

Untuk penggunaan sehari-hari, interaksi melalui Telegram akan lebih praktis daripada selalu menggunakan terminal.

## Hermes Dashboard

Hermes juga menyediakan dashboard.

Dashboard berguna untuk:

- Mengatur konfigurasi Hermes.
- Mengakses Hermes.
- Melakukan percakapan dengan Hermes.
- Mengurangi kebutuhan mengetik perintah melalui terminal.

Jika Hermes dijalankan pada komputer lokal, dashboard dapat dibuka langsung melalui browser menggunakan alamat localhost.

Namun, VPS tidak memiliki browser sehingga dashboard tidak dapat dibuka secara langsung di VPS. Oleh karena itu, perlu dilakukan port forwarding agar alamat lokal pada VPS dapat diakses dari komputer kita.

Termius menyediakan konfigurasi untuk melakukan port forwarding tersebut. Pengaturan ini akan dibahas pada bagian berikutnya.
