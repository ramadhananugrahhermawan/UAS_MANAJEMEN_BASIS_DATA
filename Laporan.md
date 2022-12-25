# UAS_MANAJEMEN_BASIS_DATA

### Kelompok 6 
- Rafi Andamira (1207050098)
- Raihan (1207050099)
- Ramadhan Anugrah Hermawan (1207050101)

# Cara Install Laravel

## ada beberapa hal yang perlu Anda siapkan dan install terlebih dahulu untuk mendukung instalasi Laravel di Windows.
Aplikasi pendukung tersebut adalah :
- Aplikasi XAMPP (Download Xampp)
- Composer (Download Composer)

# Cara install Laravel di Windows terdiri dari beberapa langkah, yaitu:

1. Masuk ke Command Prompt atau CMD
Setelah itu arahkan CMD atau terminal Anda agar berada di dalam direktori file server.
Lokasi file server di XAMPP sendiri secara default yaitu di xampp/htdocs. Anda hanya perlu
memasukkan perintah dibawah ini untuk masuk ke direktori htdocs.

2. Mulai Install Laravel
Jika Anda sudah masuk ke direktori htdocs, Anda perlu mengambil sekaligus install file
Laravel yang berada di dalam repositori Github. Masukkan perintah ini di terminal anda :
composer create-project --prefer-dist laravel/laravel nama_projectmu
tunggu hingga proses instalasi selesai

3. Cek Instalasi Framework Laravel di Browser
Jika Anda ingin memastikan Laravel sudah terinstall atau belum, Anda bisa arahkan
Command Prompt ke direktori yang sudah dibuat sebelumnya. Setelah itu, gunakan kode
dibawah ini:
php artisan serve
Jika di terminal Anda terlihat tulisan Laravel development server started setelah Anda
gunakan kode tersebut, maka selanjutnya Anda bisa buka link yang tampil tersebut di
browser. Default nya yaitu 127.0.0.1:8000. Nanti di homepage tersebut akan muncul tulisan
Laravel.

4. Buat database di MySQL
Buka terlebih dahulu XAMPP dan jalankan MySQL Database serta Apache nya
Lalu buka pada browser http://localhost/phpmyadmin/
Buat database baru bernamakan bebas sesuai keinginan (disini kami menamainya
lashoped)
Jika sudah tinggal membuat tabel dari isi database yang akan dibuat

5. Konfgurasi Database

Sebagai contoh di project kita kali ini, katakanlah nama database yang akan kita
pakai itu db_blog, lalu credential mysql di laptop kita itu usernamenya itu admin dan
passwordnya itu password.
























