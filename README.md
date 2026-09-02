# prompt-bothub




# 
```

```
# 
```

```
# 
```

```
# 
```

```
# 
```

```
# 
```

```
# 
```

```
# 
```

```
# 
```

```
# 
```

```
# 
```

```
# 
```

```
# 
```

```
# 
```

```
# 
```
Cek repo BotHub sekarang.

Siapkan repository ini agar bisa langsung di-deploy melalui Vercel Web dengan cara Import Git Repository.

Jangan melakukan deployment melalui VPS dan jangan menggunakan Vercel CLI.

Lakukan audit dan pastikan:
1. Project bisa di-build di environment Vercel.
2. Semua konfigurasi Vercel yang diperlukan sudah benar.
3. API/webhook endpoint kompatibel dengan Vercel Functions.
4. Tidak menggunakan long polling.
5. Tidak bergantung pada local filesystem sebagai persistent storage.
6. Semua secret menggunakan environment variables.
7. Buat atau perbaiki `vercel.json` hanya jika memang diperlukan.
8. Pastikan `package.json`, build command, output, dan routing sudah sesuai.
9. Jalankan lint, typecheck, test, dan production build.
10. Perbaiki semua error yang ditemukan.

Jangan memasang webhook Telegram dulu dan jangan menambahkan fitur baru.

Tujuan akhir:
Repository BotHub harus siap sehingga saya cukup membuka website Vercel, memilih Import Git Repository, memilih repo BotHub, mengisi Environment Variables, lalu klik Deploy.

Setelah selesai, laporkan:
- Build: PASS/FAIL
- Test: PASS/FAIL
- Vercel configuration: READY/NOT READY
- Environment Variables yang harus saya isi di Vercel
- Apakah repo sudah siap untuk tombol Deploy di Vercel Web
```

# 
```
Cek repo BotHub sekarang.

Fondasi project sudah selesai dan build berhasil. Jangan menambahkan fitur baru dulu. Fokuskan pekerjaan sekarang pada deployment production ke Vercel.

Lakukan langkah berikut:

1. Audit ulang project dan konfigurasi Vercel.
2. Pastikan endpoint `api/webhook.ts` benar-benar kompatibel dengan Vercel Functions.
3. Pastikan arsitektur menggunakan webhook, bukan long polling.
4. Pastikan routing webhook siap menangani banyak bot secara aman.
5. Pastikan environment variables yang dibutuhkan sudah jelas:
   - MANAGER_BOT_TOKEN
   - WEBHOOK_BASE_URL
   - ENCRYPTION_KEY
   - DATABASE_URL atau konfigurasi database yang memang digunakan project
6. Pastikan tidak ada secret/token yang hardcode di source code.
7. Pastikan database connection aman untuk environment serverless.
8. Jalankan:
   - npm install
   - lint
   - typecheck
   - test
   - production build
9. Perbaiki semua error yang ditemukan.
10. Jika Vercel CLI tersedia dan sudah login, deploy ke Vercel.
11. Jika belum login atau credential Vercel belum tersedia, jangan mengarang hasil deployment. Berhenti pada bagian tersebut dan jelaskan command yang harus saya jalankan.
12. Setelah deployment berhasil, cek URL production dan pastikan endpoint webhook dapat diakses.
13. Jangan memasang webhook Telegram menggunakan URL palsu.
14. Jangan mengklaim Bot Manager atau File Sharing Bot sudah online sebelum webhook dan konfigurasi production benar-benar siap.

Setelah selesai, laporkan secara singkat:
- Build: PASS/FAIL
- Test: PASS/FAIL
- Vercel deployment: PASS/FAIL
- Production URL
- Environment variables yang masih harus saya isi
- Langkah berikutnya untuk menghubungkan MANAGER_BOT ke Telegram

Jangan mengubah arsitektur modular yang sudah dibuat dan jangan menambahkan fitur baru sebelum deployment dasar berhasil.
```
# 
```
Buat project **BotHub** dari repository yang masih kosong.

BotHub adalah platform Telegram Bot Manager yang seluruh pengelolaannya dilakukan langsung melalui Telegram, tanpa website/dashboard.

## Tujuan utama

Buat satu **Manager Bot** yang dapat digunakan oleh banyak akun Telegram untuk membuat dan mengelola bot Telegram mereka sendiri.

Contoh:

User A → Manager Bot → membuat File Sharing Bot A

User B → Manager Bot → membuat File Sharing Bot B

User A dan User B tidak harus menggunakan akun Telegram yang sama dengan bot yang mereka buat.

Bot yang dibuat harus memiliki owner Telegram ID sehingga hanya pemiliknya dan admin BotHub yang dapat mengelolanya.

## Fitur awal

Manager Bot harus menyediakan menu Telegram yang jelas untuk:

* Create Bot
* My Bots
* Bot Settings
* Bot Status
* Start/Stop Bot
* Delete Bot
* Webhook Status
* Help

Saat Create Bot:

1. User memilih tipe bot: **File Sharing Bot**.
2. Bot meminta Bot Token dari @BotFather.
3. Validasi token menggunakan Telegram Bot API.
4. Ambil informasi bot seperti username dan bot ID.
5. User memasukkan konfigurasi database yang diperlukan.
6. Validasi konfigurasi tersebut.
7. Simpan konfigurasi secara aman.
8. Daftarkan bot ke BotHub.
9. Pasang webhook.
10. Tampilkan status bahwa bot berhasil dibuat.

## File Sharing Bot

Implementasikan engine modular untuk File Sharing Bot dengan fitur dasar:

* /start
* menerima file dari user
* menyimpan Telegram file_id dan metadata
* membuat identifier/share code
* mengambil file berdasarkan identifier
* mengirim kembali file menggunakan Telegram API
* basic owner/admin controls

Utamakan Telegram `file_id` dan jangan menyimpan binary file secara permanen di filesystem server.

## Multi-bot architecture

BotHub harus mampu menjalankan banyak bot secara bersamaan melalui satu backend.

Gunakan arsitektur seperti:

Manager Bot
↓
Bot Registry
↓
Bot Engine
↓
Bot Type Module
↓
Telegram API

Setiap bot harus mempunyai:

* bot ID
* Telegram bot ID
* bot token
* owner Telegram ID
* bot type
* database configuration
* webhook configuration
* status
* timestamps

Jangan membuat process/server terpisah untuk setiap bot.

Gunakan webhook architecture sehingga banyak bot dapat ditangani oleh satu deployment.

## Arsitektur modular

Jangan membuat satu file besar.

Pisahkan logic minimal menjadi:

* manager
* bot registry
* bot engine
* bot types
* file sharing module
* webhook manager
* database layer
* user/owner authorization
* configuration
* security
* logging
* error handling

Bot type harus menggunakan struktur modular/plugin sehingga nanti mudah menambahkan:

* File Sharing Bot
* Auto Reply Bot
* URL Shortener Bot
* Downloader Bot
* Custom Bot

tanpa mengubah core BotHub secara besar-besaran.

## Database

Buat database abstraction layer.

Jangan hardcode database credential.

Database configuration dan bot token adalah secret dan harus disimpan dengan aman.

Jangan pernah menampilkan token atau credential secara plaintext kepada user setelah disimpan.

Buat struktur data yang memungkinkan setiap bot mempunyai database/configuration yang terisolasi.

## Security

Implementasikan sejak awal:

* owner authorization
* admin authorization
* token validation
* input validation
* rate limiting dasar
* secret protection
* audit logging
* error handling
* pencegahan akses bot milik user lain

## Deployment target: Vercel

Project harus dirancang sejak awal untuk **Vercel**.

Gunakan webhook/serverless architecture.

Jangan menggunakan long polling sebagai mekanisme utama.

Jangan bergantung pada local filesystem sebagai persistent storage.

Pastikan API/webhook endpoint kompatibel dengan Vercel Functions.

Buat konfigurasi environment variables yang jelas untuk secret dan konfigurasi utama.

Jika diperlukan, buat `vercel.json` dengan konfigurasi minimal dan benar.

## Development requirements

Gunakan stack yang stabil dan cocok untuk Vercel.

Buat:

* package configuration
* source structure
* environment example
* README
* deployment instructions
* database setup instructions

Tambahkan validasi environment variables saat aplikasi dijalankan.

Gunakan TypeScript jika sesuai dengan stack yang dipilih.

## Testing

Tambahkan test yang relevan untuk:

* bot token validation
* authorization
* bot registration
* bot configuration
* webhook routing
* file sharing logic
* multi-bot isolation

Jangan membuat integration test yang membutuhkan credential Telegram nyata.

## Aturan penting

* Repository ini masih kosong, jadi bangun fondasi project dengan rapi.
* Jangan membuat website/dashboard.
* Semua user interaction utama dilakukan melalui Manager Bot Telegram.
* Jangan mengasumsikan hanya satu user atau satu bot.
* Jangan menggabungkan semua kode ke satu file.
* Jangan hardcode secret.
* Jangan menggunakan long polling.
* Jangan menyimpan file secara permanen di local filesystem.
* Prioritaskan arsitektur yang aman, modular, scalable, dan cocok untuk Vercel.
* Jangan menambahkan fitur yang belum diperlukan jika dapat membuat core architecture menjadi rumit.

Setelah implementasi selesai:

1. Jalankan install/dependency check.
2. Jalankan lint.
3. Jalankan typecheck.
4. Jalankan test.
5. Jalankan production build.
6. Perbaiki semua error yang ditemukan.
7. Pastikan project siap di-deploy ke Vercel.
8. Jangan mengklaim deployment berhasil jika belum benar-benar dilakukan.
9. Tampilkan struktur folder final dan ringkasan implementasi.

Mulai dari repository kosong dan kerjakan fondasi BotHub sampai production build berhasil.

```
# 
```
Cek repo BotForge sekarang dan siapkan project ini untuk deployment production di Vercel.

Jangan membuat ulang project dari awal. Audit terlebih dahulu struktur dan implementasi yang sudah ada, lalu perbaiki hanya bagian yang diperlukan agar BotForge dapat berjalan dengan benar di Vercel menggunakan arsitektur webhook/serverless.

Pastikan:

* Bot Manager Telegram berjalan melalui webhook.
* Banyak bot Telegram dapat dikelola secara bersamaan.
* Setiap bot memiliki owner dan konfigurasi yang terisolasi.
* File Sharing Bot menggunakan webhook, bukan long polling.
* Tidak bergantung pada local filesystem sebagai persistent storage.
* Environment variables/secrets digunakan untuk credential sensitif.
* Bot token dan database credential tidak bocor ke response, log, atau source code.
* API/webhook route kompatibel dengan Vercel Functions.
* Database connection aman untuk environment serverless.
* Tidak ada proses/background worker yang harus hidup terus-menerus.
* Build, lint, typecheck, dan test yang tersedia harus dijalankan dan diperbaiki jika gagal.
* Tambahkan atau perbaiki konfigurasi Vercel seperti vercel.json hanya jika memang diperlukan.
* Pastikan endpoint webhook dapat menerima request Telegram dengan benar.
* Pastikan routing dapat membedakan bot yang menerima update.
* Pastikan error handling dan logging production-ready.

Setelah semuanya siap:

1. Audit repo.
2. Perbaiki masalah yang ditemukan.
3. Jalankan build/test.
4. Siapkan konfigurasi deployment Vercel.
5. Jika Vercel CLI dan authentication sudah tersedia, lakukan deployment production.
6. Jika deployment tidak dapat dilakukan karena credential/login/domain/environment variable belum tersedia, jangan mengarang hasil deployment. Jelaskan persis apa yang masih diperlukan.
7. Setelah deployment berhasil, lakukan pengecekan endpoint dan webhook yang relevan.
8. Laporkan URL deployment, status deployment, hasil build/test, dan hal yang masih perlu dikonfigurasi.

Jangan menghapus fitur yang sudah bekerja. Pertahankan arsitektur modular BotForge dan jangan menggabungkan seluruh logic ke satu file.

```
# 
```
Cek repo BotForge sekarang dan siapkan project ini untuk deployment production di Vercel.

Jangan membuat ulang project dari awal. Audit terlebih dahulu struktur dan implementasi yang sudah ada, lalu perbaiki hanya bagian yang diperlukan agar BotForge dapat berjalan dengan benar di Vercel menggunakan arsitektur webhook/serverless.

Pastikan:

* Bot Manager Telegram berjalan melalui webhook.
* Banyak bot Telegram dapat dikelola secara bersamaan.
* Setiap bot memiliki owner dan konfigurasi yang terisolasi.
* File Sharing Bot menggunakan webhook, bukan long polling.
* Tidak bergantung pada local filesystem sebagai persistent storage.
* Environment variables/secrets digunakan untuk credential sensitif.
* Bot token dan database credential tidak bocor ke response, log, atau source code.
* API/webhook route kompatibel dengan Vercel Functions.
* Database connection aman untuk environment serverless.
* Tidak ada proses/background worker yang harus hidup terus-menerus.
* Build, lint, typecheck, dan test yang tersedia harus dijalankan dan diperbaiki jika gagal.
* Tambahkan atau perbaiki konfigurasi Vercel seperti vercel.json hanya jika memang diperlukan.
* Pastikan endpoint webhook dapat menerima request Telegram dengan benar.
* Pastikan routing dapat membedakan bot yang menerima update.
* Pastikan error handling dan logging production-ready.

Setelah semuanya siap:

1. Audit repo.
2. Perbaiki masalah yang ditemukan.
3. Jalankan build/test.
4. Siapkan konfigurasi deployment Vercel.
5. Jika Vercel CLI dan authentication sudah tersedia, lakukan deployment production.
6. Jika deployment tidak dapat dilakukan karena credential/login/domain/environment variable belum tersedia, jangan mengarang hasil deployment. Jelaskan persis apa yang masih diperlukan.
7. Setelah deployment berhasil, lakukan pengecekan endpoint dan webhook yang relevan.
8. Laporkan URL deployment, status deployment, hasil build/test, dan hal yang masih perlu dikonfigurasi.

Jangan menghapus fitur yang sudah bekerja. Pertahankan arsitektur modular BotForge dan jangan menggabungkan seluruh logic ke satu file.

```
