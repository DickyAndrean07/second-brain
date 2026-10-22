# Video 3 — Sandbox Google Drive dan Integrasi Google Workspace

## Apa Itu Sandbox?

Sandbox adalah ruang kerja yang dibuat secara khusus dan terpisah agar AI Agent tidak langsung memiliki akses ke semua data utama kita.

Saat bekerja, kita biasanya memiliki workspace di Google Drive. Di dalamnya terdapat berbagai macam file, seperti:

- Google Sheets.
- Google Docs.
- PDF.
- Google Slides.
- Berbagai format file lainnya.

Setiap file juga memiliki tingkat permission yang berbeda. Ada file yang bersifat privat, ada file yang berisiko tinggi, dan ada file yang tidak boleh sembarangan dimodifikasi karena perubahan pada file tersebut dapat berdampak ke file atau sistem lain.

AI Agent bekerja secara probabilistik. Tidak ada jaminan 100 persen bahwa AI Agent selalu akurat dan tidak pernah melakukan kesalahan. Jika AI Agent diberikan akses langsung ke workspace utama tanpa sandbox, ada risiko AI Agent salah mengubah atau bahkan menghapus data.

Karena itu, kita membuat Google Drive khusus sebagai sandbox.

## Membuat Google Drive Sandbox

Google Drive sandbox memiliki isi yang mirip dengan workspace biasa, seperti:

- Google Sheets.
- PDF.
- Google Slides.
- File lainnya.

Namun, data di dalam sandbox sebaiknya:

- Tidak bersifat sangat privat.
- Tidak memiliki risiko tinggi.
- Memiliki backup.
- Tidak menjadi satu-satunya tempat penyimpanan data penting.

AI Agent diarahkan untuk mengakses Google Drive sandbox, bukan Google Drive utama.

Cara yang digunakan adalah membuat akun Google baru atau akun terpisah sebagai akun sandbox. Akun ini khusus digunakan oleh AI Agent.

## Membagikan Folder dari Akun Utama

Jika data sudah banyak berada di Google Drive utama, kita tidak perlu memindahkan semua file secara manual. Kita dapat menggunakan fitur sharing.

Langkahnya:

1. Buat folder khusus untuk data yang boleh diakses AI Agent.
2. Buka menu Share pada folder tersebut.
3. Tambahkan akun Gmail sandbox.
4. Berikan permission yang diperlukan, misalnya Editor.
5. Buka Google Drive menggunakan akun sandbox.
6. Periksa folder tersebut pada bagian Shared with me.

Dengan cara ini, file tetap berada pada akun utama, tetapi akun sandbox dapat mengakses folder yang memang sudah dibagikan.

## Membuat Folder untuk Setiap Agent

Pada contoh ini terdapat folder utama bernama Hermes Data. Di dalamnya terdapat folder-folder untuk setiap agent.

Contohnya:

- Folder untuk agent finance.
- Folder untuk agent sales.
- Folder untuk agent marketing.
- Folder agent demo.

Setiap agent sebaiknya memiliki folder sendiri. Folder agent demo akan digunakan oleh agent demo untuk membuat file, memodifikasi file, dan menyimpan data hasil pekerjaannya.

Dengan pemisahan ini, masing-masing agent memiliki ruang kerja yang lebih terisolasi.

## Integrasi Google Drive dan Google Sheets

Setelah Google Account dan Google Drive sandbox tersedia, kita dapat mengintegrasikannya dengan Hermes menggunakan Google Workspace CLI atau GWS CLI.

Hermes Agent yang sudah dibuat dapat menjadi lead agent atau agent utama. Lead agent ini nantinya dapat membantu mengatur pekerjaan lain dan mengakses layanan Google Workspace sesuai permission yang diberikan.

Untuk mencari panduan GWS CLI, buka GitHub dan cari repository Google Workspace CLI. Repository tersebut berisi instruksi penggunaan dan bersifat open source.

Kita dapat memberikan URL repository tersebut kepada Hermes Agent dengan instruksi seperti:

Saya ingin kamu membantu menyiapkan GWS CLI agar saya dapat mengintegrasikan Google Drive dan Google Sheets. Pandu saya langkah demi langkah sampai berhasil.

Kemudian kirimkan URL repository GWS CLI kepada agent.

## Menyiapkan Google Cloud Project

Agent akan menjelaskan bahwa kita perlu:

1. Membuka Google Cloud Console.
2. Membuat project baru.
3. Mengaktifkan Google Workspace API.
4. Menyiapkan OAuth consent screen.
5. Membuat OAuth client.
6. Menginstal GWS CLI.

Gunakan akun Gmail sandbox ketika membuat project. Dengan demikian, kredensial dan akses yang digunakan oleh AI Agent tetap berada pada akun sandbox.

Buka console.cloud.google.com menggunakan akun sandbox, lalu buat project baru.

Nama project dapat dibuat bebas. Pada contoh ini digunakan nama GWS CLI.

## Mengaktifkan API Google Sheets dan Google Drive

Setelah project dibuat, aktifkan API berikut:

1. Google Sheets API.
2. Google Drive API.

Google Sheets API diperlukan agar agent dapat membaca dan menulis Google Sheets. Google Drive API diperlukan agar agent dapat mengakses file dan folder pada Google Drive.

## Menyiapkan OAuth Consent Screen

Buka menu OAuth consent screen, lalu mulai proses setup.

Langkahnya:

1. Masukkan nama aplikasi, misalnya Hermes Agent.
2. Masukkan support email.
3. Pilih tipe pengguna External.
4. Masukkan email pengguna.
5. Selesaikan proses pembuatan consent screen.

Setelah itu, buat OAuth client:

1. Masuk ke bagian Clients.
2. Pilih Create Client.
3. Pilih tipe aplikasi Desktop App.
4. Beri nama client, misalnya Hermes Agent.
5. Klik Create.
6. Download file JSON yang dihasilkan.

File JSON tersebut akan digunakan oleh Hermes Agent untuk konfigurasi OAuth.

## Proses OAuth dan Autentikasi

Jika GWS CLI sudah diinstal, minta Hermes Agent menyiapkan URL autentikasi. Autentikasi dilakukan pada komputer lokal karena komputer lokal memiliki browser.

Buka URL yang diberikan agent, kemudian pilih akun sandbox yang sudah didaftarkan.

Jika aplikasi belum dipublikasikan, publikasikan terlebih dahulu. Karena aplikasi ini hanya digunakan untuk kebutuhan pribadi, peringatan bahwa aplikasi belum diverifikasi masih dapat diterima untuk tahap pengujian.

Pada halaman peringatan:

1. Pilih Advanced.
2. Pilih Go to Hermes Agent.
3. Izinkan permission yang diminta.
4. Pilih semua akses yang diperlukan.
5. Tekan Continue.

Setelah itu akan muncul kode autentikasi. Salin kode tersebut dan kirimkan kepada Hermes Agent. Agent akan menyimpan kode tersebut sebagai session agar dapat mengakses Google Workspace.

Jika proses berhasil, agent dapat menggunakan Sheets API dan Drive API.

## Membatasi Akses Agent ke Folder Tertentu

Setelah autentikasi berhasil, ditemukan bahwa agent dapat membaca folder lain di Google Drive. Ini menunjukkan bahwa memberikan akses pada level akun saja masih terlalu luas.

Jika kita memberikan akses ke Google Drive utama, agent berpotensi mengakses seluruh folder dan data di dalamnya. Karena itu, akses perlu dibatasi lagi.

Langkahnya:

1. Buka folder agent demo.
2. Salin link folder tersebut.
3. Ambil folder ID dari link tersebut.
4. Berikan instruksi kepada agent agar hanya mengakses folder tersebut.
5. Minta agent menyimpan aturan tersebut di memorinya.

Contoh instruksinya:

Saya ingin kamu hanya boleh mengakses data-data yang ada di dalam folder ini. Catat dan simpan aturan ini di memori.

Aturan tersebut menjadi strict rule bagi agent. Folder lain yang dimiliki agent lain tidak boleh diakses.

Model gratis dapat membutuhkan beberapa langkah dan pengulangan untuk memahami instruksi. Model berbayar biasanya lebih cepat dan lebih konsisten. Pada contoh ini, model Codex dari OpenAI juga disebut sebagai alternatif ketika akun ChatGPT Pro sudah tersedia.

## Membuat Google Sheet Transaction Log

Setelah akses Google Workspace tersedia dan folder agent demo sudah dibatasi, kita dapat menguji kemampuan agent untuk membuat file.

Minta agent membuat Google Sheet bernama Transaction Log di dalam folder agent demo. Sheet tersebut digunakan untuk pencatatan transaksi.

Contoh kolom yang dibuat:

- Tanggal.
- Waktu.
- Tipe transaksi.
- Kategori.
- Merchant.
- Deskripsi.
- Jumlah.
- Harga satuan.
- Metode pembayaran.
- Catatan.

Jika file berhasil dibuat di dalam folder agent demo, berarti agent sudah dapat:

- Membaca Google Drive.
- Membuat file.
- Menulis Google Sheets.

## Menguji Input Transaksi Berbasis Teks

Pengujian pertama dilakukan dengan mengirimkan transaksi melalui teks.

Contoh instruksi:

Tolong catat transaksi pembelian senilai Rp2.000.000 untuk pembelian bahan produksi.

Hermes akan menggunakan GWS CLI untuk membangun dan menjalankan perintah pada terminal. Setelah selesai, transaksi akan dimasukkan ke Google Sheet Transaction Log.

## Membuat Skill Input Transaksi

Jika setiap kali mencatat transaksi kita harus memberikan instruksi yang sangat panjang, prosesnya akan merepotkan. Karena itu, alur tersebut dapat dibuat menjadi skill.

Minta Hermes membuat skill bernama input transaksi. Skill tersebut berfungsi sebagai SOP untuk:

1. Membaca data transaksi.
2. Menentukan kolom yang sesuai.
3. Memasukkan data ke Google Sheet Transaction Log.
4. Menjaga proses tetap konsisten.

Setelah skill dibuat, kita dapat memanggil skill tersebut setiap kali ada transaksi baru.

## Menguji Input Transaksi dari Foto Struk

Pengujian kedua dilakukan dengan mengirimkan foto struk atau bon.

Contoh alurnya:

1. Kirim foto transaksi.
2. Minta agent menggunakan skill input transaksi.
3. Agent membaca gambar.
4. Agent mengekstrak teks dan angka dari gambar.
5. Agent memasukkan hasilnya ke Google Sheet Transaction Log.

Pada contoh ini digunakan gambar bon dari internet yang berisi tiga unit barang. Agent membaca isi gambar, mengekstrak data, lalu memasukkannya ke Google Sheet sesuai SOP.

Model gratis membutuhkan waktu lebih lama dan memiliki risiko kesalahan ekstraksi lebih besar. Pada contoh, harga satuan terbaca salah sebagai Rp5.000, padahal seharusnya Rp35.700.000.

Kesalahan ini menunjukkan pentingnya:

- Menggunakan model yang lebih baik untuk data penting.
- Melakukan validasi hasil.
- Menyediakan human-in-the-loop sebelum data dianggap final.

Model berbayar seperti Codex dapat menjadi pilihan jika diperlukan akurasi dan proses yang lebih konsisten.

## Kesimpulan

Pada rangkaian ini, kita sudah:

- Membuat Google Account sandbox.
- Menyiapkan Google Drive sandbox.
- Membuat Google Cloud project.
- Mengaktifkan Google Sheets API.
- Mengaktifkan Google Drive API.
- Membuat OAuth consent screen.
- Membuat OAuth client.
- Mengautentikasi Hermes dengan Google Workspace.
- Membatasi akses agent ke folder tertentu.
- Membuat Google Sheet Transaction Log.
- Menguji pencatatan transaksi melalui teks.
- Membuat skill input transaksi.
- Menguji pencatatan transaksi melalui foto struk.

Dengan demikian, kita sudah memiliki AI Agent yang dapat membaca dan menulis Google Drive serta Google Sheets untuk membantu pencatatan keuangan.

Pada tahap berikutnya, pembahasan dapat dilanjutkan ke memory agent, multiple agent, dan integrasi dengan service lain.
