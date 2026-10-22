# Video 2 — Hermes Dashboard, Telegram, dan Struktur Memori Agent

## Mengakses Hermes Dashboard dari Komputer Lokal

Sekarang kita lanjut membahas cara mengakses Hermes Dashboard melalui browser di komputer lokal.

Pertama, buka tab baru pada koneksi Hermes Agent yang sudah dibuat. Kemudian jalankan perintah berikut:

~~~
hermes dashboard
~~~

Saat perintah tersebut dijalankan, Hermes akan membangun dan menjalankan web UI-nya. Setelah selesai, Hermes akan memberikan URL, misalnya:

~~~
127.0.0.1:9119
~~~

Masalahnya, URL tersebut belum dapat langsung diakses dari komputer lokal karena Hermes berjalan di VPS. Kita perlu menambahkan konfigurasi port forwarding pada Termius.

## Membuat Port Forwarding di Termius

Langkahnya:

1. Buka Termius.
2. Pilih host Hermes Agent.
3. Buka menu port forwarding.
4. Buat forwarding baru.
5. Pilih tipe lokal.
6. Masukkan local port number 9119.
7. Gunakan bind address 127.0.0.1.
8. Pilih host Hermes Agent yang sudah dibuat.
9. Beri label, misalnya Hermes Dashboard Demo.
10. Tekan Done.

Konfigurasi tersebut menghubungkan komputer lokal dengan host Hermes yang berjalan di VPS.

Setelah forwarding dibuat, forwarding tersebut belum langsung aktif. Klik forwarding Hermes Dashboard Demo dan mulai koneksinya. Jika indikatornya berubah menjadi biru, berarti port forwarding sudah aktif.

Sekarang kembali ke browser dan refresh URL Hermes Dashboard. Dashboard seharusnya sudah dapat diakses.

## Fitur Hermes Dashboard

Dashboard lebih nyaman digunakan daripada terminal. Pada halaman awal terdapat profile default yang digunakan sebagai agent utama. Nantinya kita juga dapat membuat beberapa agent atau multiple agent.

Dashboard juga menampilkan:

- Status gateway.
- API keys.
- Environment keys.
- Model yang digunakan.
- Fitur chat.

Model OpenRouter yang sebelumnya dipilih, yaitu Nemotron 3 Ultra, juga dapat dilihat dari dashboard.

Sebelumnya kita harus menjalankan perintah Hermes Chat melalui terminal. Dengan Hermes Dashboard, fitur chat sudah tersedia di dalam dashboard.

Sebagai contoh, kita dapat mengirimkan pesan:

Halo, saya ingin kamu menjadi asisten pribadi untuk membantu pencatatan.

Hermes akan membalas dan dapat diarahkan untuk membantu pencatatan harian, pencatatan keuangan, serta pekerjaan lainnya.

## Menghubungkan Hermes dengan Telegram

Tahap berikutnya adalah menghubungkan Hermes dengan Telegram agar kita tidak harus selalu menggunakan Termius atau Hermes Dashboard.

Pastikan sudah memiliki akun Telegram. Aplikasi Telegram versi desktop direkomendasikan karena lebih mudah digunakan dan lebih stabil dibandingkan versi web.

### Membuat Telegram Bot

Telegram menyediakan bot resmi bernama BotFather untuk membuat dan mengatur bot.

Langkahnya:

1. Buka Telegram.
2. Cari akun BotFather.
3. Jalankan perintah /newbot.
4. Masukkan nama bot, misalnya Hermes Agent.
5. Masukkan username bot yang unik.
6. Pastikan username diakhiri dengan kata bot.

Jika berhasil, BotFather akan memberikan:

- URL untuk membuka bot.
- Telegram bot token.

Bot token bersifat privat. Jangan membagikannya kepada orang lain karena token tersebut digunakan untuk menghubungkan bot Telegram dengan Hermes.

## Setup Telegram di Hermes Dashboard

Kembali ke Hermes Dashboard dan buka pilihan channel. Karena kita akan menggunakan Telegram, pilih Telegram.

Tersedia pilihan quick setup dan manual setup. Pada contoh ini digunakan manual setup karena bot token sudah tersedia.

Masukkan Telegram bot token yang diberikan BotFather.

### Membatasi Telegram User ID

Pada langkah berikutnya terdapat pilihan allow Telegram user ID. Pengaturan ini menentukan siapa saja yang boleh berbicara dengan AI Agent.

Jika dikosongkan, semua pengguna Telegram dapat menghubungi AI Agent. Hal ini berbahaya apabila AI Agent memiliki akses terhadap data konfidensial.

Masukkan Telegram User ID milik pengguna yang diizinkan. Jika diperlukan, Telegram User ID anggota tim lain juga dapat ditambahkan.

### Mendapatkan Telegram User ID

Untuk mendapatkan Telegram User ID, cari bot user info di Telegram. Kemudian jalankan atau kirimkan perintah /start.

Bot tersebut akan memberikan informasi seperti:

- ID.
- First name.
- Last name.
- Informasi pengguna lainnya.

Yang diperlukan hanya nilai ID.

Salin ID tersebut, kembali ke Hermes Dashboard, lalu masukkan pada bagian allow Telegram user ID. Setelah itu:

1. Simpan konfigurasi.
2. Aktifkan channel Telegram.
3. Restart gateway.

Perubahan channel baru akan berjalan setelah gateway di-restart. Tunggu sampai status gateway berubah menjadi hijau atau running.

## Menguji Telegram Bot

Buka URL bot Telegram yang diberikan BotFather dan tekan Start. Kemudian kirim pesan:

Halo

Jika Hermes membalas, berarti integrasi Telegram berhasil.

Hermes biasanya meminta agar chat tersebut dijadikan home channel. Pilih Set Home.

Home channel adalah channel utama yang digunakan Hermes untuk mengirim:

- Notifikasi.
- Informasi progres.
- Hasil pekerjaan.
- Pesan proaktif lainnya.

Setelah itu, kita dapat mengirim pesan seperti:

Kamu siapa dan apa saja tugasmu?

Hermes akan menjelaskan identitas serta kemampuannya.

## File Memori Default Hermes

Saat membuat AI Agent, Hermes secara otomatis membuat beberapa file untuk membantu agent mengingat konteks dan profil.

File yang dibuat antara lain:

- soul.md
- memory.md
- agent.md
- user.md

Format .md adalah Markdown, yaitu format teks yang mudah dibaca manusia dan AI Agent.

### user.md

File ini berisi profil pengguna secara global, misalnya:

- Nama pengguna.
- Preferensi kerja.
- Kebiasaan.
- Informasi profil lain yang berkaitan dengan pengguna.

### agent.md

File ini berisi profil agent berdasarkan project atau peran tertentu. Jika kita memiliki beberapa agent, setiap agent dapat memiliki tujuan dan fungsi masing-masing.

Contohnya:

- Agent finance untuk pekerjaan keuangan.
- Agent sales untuk pencatatan lead.
- Agent marketing untuk pekerjaan pemasaran.

### memory.md

File ini digunakan untuk mengingat history pekerjaan, tugas, SOP, dan informasi lain yang perlu dipertahankan oleh agent.

### soul.md

File ini berisi profil dan karakter AI Agent itu sendiri. Misalnya, jika kita membuat agent finance, file ini dapat menjelaskan bahwa agent tersebut berfungsi sebagai AI Agent finance dan apa saja tugasnya.

Semua file tersebut dibuat dan diperbarui secara otomatis oleh Hermes. Kita tidak perlu membuat atau mengubahnya secara manual.

## Tahap Berikutnya

Pada tahap ini, beberapa bagian sudah selesai:

- VPS sudah disiapkan.
- Hermes sudah berjalan.
- AI model OpenRouter sudah dipilih.
- Termius sudah digunakan.
- Hermes Dashboard sudah dapat diakses.
- Telegram sudah terintegrasi.

Tahap berikutnya adalah menyiapkan Google Account dan Google Apps untuk membangun sandbox, kemudian mengintegrasikan Hermes dengan Google Drive dan Google Sheets.
