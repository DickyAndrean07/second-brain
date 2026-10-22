# Video 4 — Struktur AI Team, Memory, Workspace, Skill, dan MCP

## Gambaran AI Team

Ini adalah tim AI yang digunakan untuk pekerjaan sehari-hari. Setiap agent memiliki:

- Profile.
- Memory.
- Workspace.
- Tools.
- Skill.

Dengan kemampuan tersebut, setiap agent dapat menjalankan pekerjaan secara otomatis.

Contohnya, ketika ada pekerjaan membuat invoice untuk klien, instruksi dapat diberikan melalui Telegram. Agent akan mengerjakan tugas tersebut dan mengirimkan hasilnya kembali melalui Telegram.

AI team perlu berjalan pada mesin yang dapat aktif selama 24 jam. Tujuannya agar agent dapat bekerja kapan saja, termasuk ketika pemiliknya sedang tidur.

AI Agent yang proper bukan hanya hasil instalasi. Agent juga perlu memiliki role, skill, dan workspace. Environment di sekitar agent inilah yang membuat AI Agent benar-benar berguna.

Jika hanya menginstal AI Agent lalu langsung menggunakannya tanpa environment yang tepat, hasilnya tidak lebih dari chatbot yang lebih rumit.

Engine utama yang digunakan pada video ini adalah Hermes.

## Mesin untuk Menjalankan AI Agent

Untuk kebutuhan sehari-hari, dedicated machine seperti mini PC atau Mac Mini dapat digunakan. Pada contoh ini digunakan Mac Mini.

Dedicated machine memberikan kontrol penuh terhadap:

- Data.
- Software.
- Tools.
- Aplikasi.
- Environment tempat Hermes berjalan.

Dedicated machine juga membantu menjaga keamanan karena agent bekerja pada lingkungan yang sudah disterilisasi.

Jika agent dijalankan pada komputer utama yang menyimpan banyak data penting, terdapat risiko agent salah menghapus atau mengubah data.

AI Agent bersifat probabilistik. Kita tidak dapat menjamin 100 persen bahwa agent tidak pernah melakukan kesalahan.

Namun, bagi yang masih memulai atau masih dalam tahap testing, dedicated hardware tidak wajib. Kita dapat menggunakan VPS atau Virtual Private Server.

VPS dapat berjalan 24 jam tanpa harus membeli hardware dan menyalakannya sendiri. Dari sisi biaya, VPS juga lebih murah untuk tahap awal.

## AI Model sebagai Otak Agent

Setelah memiliki mesin sebagai tempat tinggal agent, kita perlu memilih AI model sebagai otaknya.

AI model adalah bagian penting karena model tersebut yang membuat agent dapat memahami dan mengerjakan tugas.

Semua agent tidak harus menggunakan model yang sama. Kita dapat mengombinasikan berbagai model sesuai kebutuhan tiap agent.

Untuk pekerjaan yang tidak terlalu kompleks, model murah atau model gratis dapat digunakan. Namun, model gratis sebaiknya tidak digunakan untuk data yang konfidensial atau kritikal.

Untuk pekerjaan yang kompleks dan membutuhkan proses berpikir lebih canggih, kita dapat menggunakan model berbayar, misalnya model OpenAI yang diakses melalui Codex.

OpenRouter juga dapat digunakan karena menyediakan berbagai provider dan model, baik model berbayar maupun gratis. Model gratis dari keluarga NVIDIA Nemotron, seperti varian Super dan Ultra, dapat digunakan dengan batas tertentu.

Jika memiliki hardware yang sangat kuat, model lokal juga dapat digunakan. Namun, untuk tahap awal, penggunaan model lokal tidak direkomendasikan karena setup dan troubleshooting-nya dapat menghabiskan banyak waktu sebelum use case bisnis selesai dibangun.

Pertanyaan yang penting bukan model mana yang paling canggih, melainkan model mana yang paling sesuai dan efisien untuk pekerjaan yang ingin diselesaikan.

### Contoh Pembagian Model

Lead agent sebaiknya menggunakan model yang paling canggih karena tugasnya tidak hanya mengerjakan instruksi, tetapi juga membantu mengatur agent lain.

Untuk personal assistant yang bertugas membuat catatan atau rekap, model yang lebih ringan dapat digunakan karena lebih cepat dan murah.

## Channel untuk Berinteraksi dengan Agent

Hermes memiliki interface bawaan yang dapat dipanggil melalui perintah Hermes Dashboard. Namun, untuk penggunaan sehari-hari, Telegram lebih praktis.

Dengan integrasi Telegram, kita cukup membuka aplikasi Telegram untuk berkomunikasi dengan AI Agent.

Telegram cocok ketika:

- Penggunanya adalah pemilik atau tim internal.
- Dibutuhkan channel operasional yang sederhana.
- Biaya harus ditekan.

WhatsApp lebih cocok ketika:

- AI Agent berhadapan langsung dengan pelanggan.
- Dibutuhkan channel customer-facing.
- Tersedia budget untuk biaya layanan resmi.

Telegram bersifat gratis dan dapat digunakan untuk membuat hingga sekitar 20 bot atau AI chatbot. WhatsApp memerlukan proses resmi dan dapat menimbulkan biaya, seperti biaya chat dan push message.

## Mengapa Perlu Struktur Banyak Agent?

Ketika pekerjaan mulai beragam, misalnya finance, sales, marketing, personal assistant, dan engineering, satu profile agent akan menerima terlalu banyak konteks.

Hal tersebut dapat membuat agent bingung dan menurunkan akurasi.

Solusinya adalah membuat profile untuk masing-masing pekerjaan:

- Agent sales.
- Agent marketing.
- Agent personal assistant.
- Agent finance.
- Agent engineering.

Setiap profile memiliki:

- Role.
- Workspace.
- Skill.
- Tools.
- Environment yang terisolasi.

Dengan pemisahan tersebut, setiap agent dapat fokus pada tugasnya.

## Lead Agent

Jika sudah memiliki banyak profile agent, perlu ada satu agent yang berperan sebagai lead agent.

Fungsi lead agent:

- Mengatur sub-agent.
- Mendelegasikan pekerjaan.
- Membantu troubleshooting.
- Mengatur struktur AI team.
- Melakukan onboarding agent baru.

Onboarding agent baru dapat dianalogikan seperti onboarding pegawai. Agent baru diperkenalkan dengan sistem, struktur, proses, dan SOP yang berlaku.

Lead agent dapat diberi skill khusus untuk melakukan onboarding. Setiap kali agent baru dibuat, lead agent diminta melakukan onboarding agar agent tersebut langsung mengikuti environment dan SOP yang sudah ditetapkan.

## Dashboard untuk Mengelola AI Team

Jika jumlah agent sudah banyak, diperlukan dashboard untuk mengelola dan memantau setiap agent.

Hermes sudah memiliki Hermes Dashboard. Dashboard ini membantu konfigurasi dan interaksi tanpa harus selalu menggunakan terminal.

Pada contoh ini dibuat dashboard tambahan bernama Sultan Mission Control. Dashboard tersebut merupakan extension dari Hermes Dashboard yang hanya menampilkan fitur yang benar-benar diperlukan.

Fitur yang dibuat antara lain:

- Kanban board.
- Office.
- Data monitoring.
- Tampilan dua dimensi.
- Status agent.

Tampilan office digunakan untuk melihat agent yang sedang bekerja, idle, atau beristirahat. Tampilan tersebut merepresentasikan status agent, bukan sekadar dekorasi.

Teknologi boleh kompleks, tetapi bagi business owner, sistem sebaiknya dapat digunakan tanpa harus memahami seluruh detail teknisnya.

## Memory Agent

Agar agent tidak cepat lupa dan dapat bekerja lebih cepat, agent membutuhkan memory.

Memory dibagi menjadi dua area:

1. Short-term memory.
2. Long-term memory.

### Short-Term Memory Hermes

Short-term memory adalah memory bawaan Hermes. Setiap profile agent secara otomatis memiliki file profile, soul, user, memory, dan agent dalam format Markdown.

Memory bawaan tersebut memiliki keterbatasan. Jika data terus bertambah besar, agent dapat memiliki bias terhadap isi memory tersebut.

### Long-Term Memory dengan Obsidian

Untuk long-term memory, digunakan Obsidian.

Obsidian memiliki versi gratis atau open source dan versi berbayar yang di-host oleh Obsidian. Pada contoh ini digunakan versi gratis atau open source.

Obsidian juga menggunakan Markdown, tetapi memiliki beberapa fitur tambahan:

- Bidirectional linking.
- Tampilan visual hubungan antarcatatan.
- Struktur catatan yang saling terhubung.

Dengan bidirectional linking, catatan yang dibuat oleh AI Agent dapat terhubung dengan dokumen lain yang relevan. Hal ini membantu agent menemukan hubungan antara informasi dengan lebih cepat.

Obsidian juga menyediakan graph view untuk melihat hubungan antar-memory atau catatan.

Catatan dapat dibuat menjadi file-file kecil yang saling terhubung, bukan satu file panjang. Semakin lama AI Agent bekerja, konteks dan catatan pekerjaan dapat berkembang menjadi aset yang bernilai.

Contohnya, ketika agent membaca catatan tentang meeting dengan klien, agent juga dapat menemukan hubungan klien tersebut dengan project atau SOP pada dokumen lain.

## Memory dan Knowledge

Selain memory, AI Agent juga memerlukan knowledge atau referensi faktual.

Memory adalah pengalaman atau catatan yang perlu diingat agent. Knowledge adalah referensi atau source of truth yang digunakan ketika agent membutuhkan informasi faktual.

Untuk knowledge digunakan LLM Wiki. LLM Wiki diperkenalkan oleh Andrej Karpathy dan Hermes memiliki skill untuk menggunakannya.

LLM Wiki dapat diintegrasikan dengan Obsidian. Informasi faktual disimpan sebagai wiki, bukan sebagai memory biasa.

Contoh isi LLM Wiki:

- SOP.
- FAQ.
- Informasi internal.
- Referensi faktual.

Sederhananya:

- Memory adalah pengalaman.
- Wiki adalah referensi faktual.

## Workspace Setiap Agent

Setiap agent perlu memiliki workspace sendiri. Jika pegawai memiliki meja kerja masing-masing, AI Agent juga perlu memiliki ruang kerja masing-masing.

Pada contoh ini digunakan Google Workspace. Di dalam Google Drive dibuat folder khusus untuk tiap agent.

Contohnya:

- Folder sales untuk agent sales.
- Folder finance untuk agent finance.
- Folder marketing untuk agent marketing.

Lead agent dapat melakukan onboarding dan memberi tahu setiap agent folder mana yang boleh digunakan untuk menyimpan atau memodifikasi data.

Workspace saja belum cukup. Agent juga memerlukan SOP agar dapat bekerja sesuai aturan.

## Skill sebagai SOP

Skill adalah bentuk SOP yang berisi prompt atau instruction. Skill akan dipanggil ketika agent melakukan tugas tertentu.

Profile agent bukan sekadar nama. Setiap profile dapat memiliki kemampuan, skill, dan kapabilitas yang berbeda.

Contohnya, skill untuk agent finance berbeda dengan skill untuk agent sales.

## Backup dan Self-Maintenance

Jika seluruh skill, memory, workspace, dan konfigurasi hilang, kita tidak ingin membangun AI team dari awal.

Semakin lama AI Agent digunakan, semakin banyak data dan konfigurasi yang tersimpan. Karena itu, backup harus dilakukan secara rutin.

Pada contoh ini digunakan GitHub untuk membackup:

- Konfigurasi Hermes.
- Memory.
- Catatan.
- Data workspace.

Backup tidak harus dilakukan secara manual. Hermes dapat menjalankan schedule.

SOP backup dapat diberikan kepada agent agar agent secara rutin melakukan sinkronisasi workspace Hermes ke GitHub. Backup dijadwalkan setiap malam pada waktu yang telah ditentukan.

Dengan demikian, jika terjadi masalah, data dan konfigurasi masih memiliki cadangan.

AI Agent bukan hanya pekerja yang mengerjakan tugas. Agent juga dapat membantu maintenance dirinya sendiri dan melakukan self-healing ketika terjadi masalah.

## Integrasi dengan Sistem Eksternal

Setelah agent memiliki memory, skill, workspace, dan knowledge, agent perlu berinteraksi dengan dunia luar atau sistem pihak ketiga.

Contoh sistem eksternal:

- Google Workspace.
- Aplikasi desain.
- Aplikasi clipper.
- Service pihak ketiga lainnya.

Interaksi dengan sistem eksternal dilakukan melalui MCP atau Model Context Protocol.

## MCP atau Model Context Protocol

MCP dapat dianalogikan seperti port universal. Seperti USB yang dapat digunakan untuk menghubungkan komputer dengan berbagai perangkat, MCP menyediakan cara yang seragam untuk menghubungkan AI Agent dengan berbagai sistem.

AI team dapat menggunakan MCP pihak ketiga atau MCP yang dibuat sendiri.

Pada contoh ini dibuat MCP untuk:

- Flomeria Desktop, agar agent dapat membantu workflow pembuatan konten.
- Aplikasi clipper, agar agent dapat berinteraksi dengan aplikasi yang dibuat sendiri.

Dengan MCP, kita cukup memberikan perintah melalui Telegram dan agent dapat menjalankan pekerjaan pada aplikasi eksternal.

## Struktur Lengkap AI Team

Jika dilihat secara keseluruhan, struktur AI team terdiri dari:

1. Infrastruktur.
2. AI model.
3. Struktur AI Agent.
4. Channel.
5. Memory.
6. Knowledge.
7. Workspace.
8. Skill.
9. Tools.
10. Automation.
11. Backup.

Hermes hanya salah satu layer dari keseluruhan sistem. Sistem pendukung lainnya perlu dikonfigurasi agar AI team benar-benar dapat membantu pekerjaan sehari-hari.

Business owner tidak perlu terlalu terobsesi dengan model AI terbaru. Model AI akan terus berubah dan versi baru akan selalu muncul.

Nilai utama AI team berada pada:

- SOP yang dibangun.
- Workflow yang dibangun.
- Sistem yang dibuat.
- Integrasi dengan AI team.

Bukan hanya pada model AI yang digunakan.
