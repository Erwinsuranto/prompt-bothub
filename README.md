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
Perbaiki konfigurasi webhook Manager Bot pada project bothub.

Kondisi saat ini:
- Repository: zenolambee/bothub
- Deployment: https://bothub-seven.vercel.app
- Environment Variables Vercel sudah tersedia:
  - MANAGER_BOT_TOKEN
  - WEBHOOK_BASE_URL
  - ENCRYPTION_KEY
  - ADMIN_IDS
- Jangan meminta atau mencetak nilai secret.
- Jangan hardcode token atau encryption key.
- Jangan menggunakan token dari VPS.

Masalah:
src/manager/bot.ts sudah menggunakan grammY webhookCallback, tetapi api/webhook.ts hanya meneruskan request ke managerBotHandler jika path mengandung "/manager". Endpoint webhook Manager Bot harus menggunakan:
https://bothub-seven.vercel.app/api/webhook/manager

Tugas:
1. Audit seluruh flow Manager Bot dan webhook.
2. Pastikan endpoint GET / tetap mengembalikan:
   {"status":"ok","service":"bothub"}
3. Pastikan POST /api/webhook/manager diteruskan ke managerBotHandler dengan benar.
4. Implementasikan mekanisme aman untuk otomatis mendaftarkan Telegram webhook menggunakan MANAGER_BOT_TOKEN dan WEBHOOK_BASE_URL dari process.env.
5. Webhook target harus dibentuk sebagai:
   ${WEBHOOK_BASE_URL}/api/webhook/manager
   tanpa hardcode domain.
6. Registrasi webhook harus terjadi otomatis saat deployment/initialization yang sesuai dengan arsitektur Vercel Serverless, tanpa membutuhkan token di VPS.
7. Jangan membuat endpoint publik yang memungkinkan orang lain mengganti webhook tanpa autentikasi.
8. Jangan log MANAGER_BOT_TOKEN, ENCRYPTION_KEY, atau nilai secret apa pun.
9. Jika mekanisme otomatis membutuhkan perubahan build/deployment, implementasikan dengan cara yang kompatibel dengan Vercel.
10. Pastikan tidak terjadi infinite loop atau registrasi webhook pada setiap request secara tidak perlu.
11. Pertahankan command Manager Bot yang sudah ada:
    /start
    /help
    /createbot
    /mybots
    /botstatus
    /startbot
    /stopbot
    /deletebot
12. Jangan merusak file-sharing bot atau routing bot lain.
13. Tambahkan test untuk memastikan route /api/webhook/manager benar.
14. Jalankan npm test dan npm run build. Perbaiki error jika ada.
15. Commit perubahan ke branch main dan push ke origin/main.

Setelah selesai, tampilkan hanya:
- file yang diubah
- hasil test
- hasil build
- commit hash

Jangan pernah menampilkan nilai secret/environment variable.

```
# 
```
Cek repo BotHub dan perbaiki error deployment Vercel berikut:

500: INTERNAL_SERVER_ERROR
Code: FUNCTION_INVOCATION_FAILED

Deployment URL:
https://bothub-seven.vercel.app

Jangan menambahkan fitur baru.

Lakukan debugging berdasarkan implementasi repo saat ini:

1. Periksa seluruh source code yang berkaitan dengan Vercel Function.
2. Fokus terutama pada:
   - api/webhook.ts
   - src/webhook/
   - src/manager/
   - src/config/
   - src/database/
   - package.json
   - vercel.json
3. Periksa Vercel runtime compatibility.
4. Cari kemungkinan crash saat module initialization/import.
5. Periksa environment variable yang diakses saat function dijalankan.
6. Pastikan environment variable yang belum diisi tidak menyebabkan function crash ketika endpoint dipanggil.
7. Pastikan route `/` tetap dapat mengembalikan health response.
8. Pastikan `/manager` dan `/webhook/{botId}` tidak crash hanya karena konfigurasi bot belum lengkap.
9. Jangan memasukkan secret/token asli ke source code.
10. Jangan menggunakan long polling.
11. Jangan mengubah arsitektur modular.
12. Jangan menganggap masalah selesai hanya karena build lokal berhasil.

Jika tersedia, periksa Vercel deployment/runtime logs untuk menemukan error sebenarnya di balik `FUNCTION_INVOCATION_FAILED`.

Setelah menemukan penyebab:
- perbaiki root cause
- jalankan lint
- jalankan typecheck
- jalankan test
- jalankan production build
- commit perubahan
- push ke GitHub branch main

Jangan melakukan deployment melalui VPS atau Vercel CLI.

Karena deployment dilakukan melalui Vercel Web/Git integration, cukup push perbaikan ke GitHub agar Vercel membuat deployment baru.

Setelah selesai laporkan:
- root cause error
- file yang diperbaiki
- lint: PASS/FAIL
- typecheck: PASS/FAIL
- test: PASS/FAIL
- build: PASS/FAIL
- apakah commit sudah dipush ke GitHub
- apakah deployment baru sudah dipicu Vercel

Jangan mengklaim error sudah selesai sebelum root cause ditemukan dan diperbaiki.

```
# 
```
Cek repo BotHub sekarang.

Saya melihat repository GitHub BotHub hanya berisi README.md, sedangkan implementasi lengkap BotHub sudah ada di working repository/local project.

Jangan membuat ulang project dan jangan mengubah fitur.

Lakukan:

1. Periksa `git status`.
2. Pastikan semua source code BotHub yang sudah selesai memang ada di repository lokal.
3. Pastikan file penting seperti:
   - package.json
   - tsconfig.json
   - vercel.json jika digunakan
   - src/
   - api/
   - tests/
   - README.md
   dan seluruh file project yang diperlukan ada.
4. Periksa `.gitignore` dan pastikan file source penting tidak ikut ter-ignore.
5. JANGAN pernah commit secret, bot token, database credential, `.env`, atau private key.
6. Pastikan `.env` dan file secret masuk `.gitignore`.
7. Jalankan git diff/status untuk memastikan tidak ada perubahan yang tidak diinginkan.
8. Commit seluruh source code BotHub yang diperlukan dengan commit message yang jelas.
9. Push commit tersebut ke repository GitHub BotHub pada branch `main`.
10. Setelah push berhasil, verifikasi bahwa GitHub benar-benar menampilkan source code lengkap, bukan hanya README.md.
11. Jangan melakukan deployment Vercel dulu.

Setelah selesai laporkan:
- jumlah file yang berhasil di-push
- commit hash
- branch
- status push
- apakah source code lengkap sudah terlihat di GitHub
- apakah repo sekarang siap di-import melalui Vercel Web

Jika remote GitHub atau authentication bermasalah, jangan mengarang hasil. Jelaskan error yang sebenarnya.
```
# 
```
Cek repo BotHub dan deployment Vercel yang sekarang.

Fondasi dan routing sudah PASS. Sekarang fokus menghubungkan Manager Bot dengan Telegram menggunakan deployment Vercel yang sudah ada.

Jangan menambahkan fitur baru dan jangan mengubah arsitektur yang sudah benar.

Lakukan:

1. Pastikan Manager Bot menggunakan `MANAGER_BOT_TOKEN`.
2. Pastikan `WEBHOOK_BASE_URL` menggunakan URL production Vercel yang sebenarnya.
3. Pastikan webhook Manager Bot diarahkan ke:

   {WEBHOOK_BASE_URL}/manager

4. Pastikan endpoint `/manager` menerima Telegram webhook update dengan benar.
5. Pastikan handler Manager Bot dapat merespons `/start`.
6. Pastikan validasi owner/admin tetap berjalan.
7. Pastikan `ENCRYPTION_KEY` dan `ADMIN_IDS` digunakan sesuai konfigurasi project.
8. Jangan menampilkan atau mencetak token bot maupun secret ke log.
9. Jangan menggunakan long polling.
10. Jangan menggunakan VPS sebagai server runtime BotHub.

Jika environment variables belum tersedia di Vercel:
- Jangan membuat nilai palsu.
- Jelaskan tepat variable apa saja yang harus saya isi di Vercel.

Jika environment variables sudah tersedia:
- Verifikasi konfigurasi.
- Pastikan webhook Manager Bot dapat didaftarkan.
- Cek status webhook menggunakan Telegram Bot API tanpa membocorkan token.

Setelah selesai laporkan:
- Manager Bot endpoint: PASS/FAIL
- `/manager`: PASS/FAIL
- `/start`: PASS/FAIL
- Webhook: PASS/FAIL
- Environment variables: READY/NOT READY
- Masalah yang ditemukan
- Langkah berikutnya

Jangan lanjut ke pembuatan File Sharing Bot sebelum Manager Bot berhasil menerima `/start`.
```
# 
```
Cek deployment Vercel BotHub yang baru saja berhasil.

Jangan menambahkan fitur baru.

Periksa deployment production dan pastikan:

1. Identifikasi URL production Vercel yang sebenarnya.
2. Cek route/API endpoint yang tersedia pada project.
3. Pastikan endpoint webhook BotHub dapat diakses melalui Vercel.
4. Jika `/` menghasilkan 404 tetapi endpoint API/webhook benar-benar tersedia, jangan menganggap deployment gagal.
5. Pastikan `api/webhook.ts` ter-deploy sebagai Vercel Function.
6. Periksa apakah ada masalah routing atau konfigurasi `vercel.json`.
7. Pastikan build production tetap PASS.
8. Jangan memasang webhook Telegram dulu.
9. Jangan menggunakan token asli atau credential asli untuk testing.

Di akhir berikan:
- URL production
- Root `/` status
- Webhook endpoint status
- Vercel Function status
- Build status
- Apakah BotHub sudah siap untuk konfigurasi environment variables dan webhook Telegram

Jika ada masalah, perbaiki hanya masalah deployment/routing yang diperlukan.

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
