# Presensi App

Project presensi berbasis Laravel untuk absensi siswa dan pemindaian QR.

## Clone Project

Pastikan repo di-clone di dalam folder `www` di Laragon.

Cara paling mudah:

1. Buka folder `www` di Laragon.
2. Klik kiri area kosong di dalam folder tersebut.
3. Pilih `Open in terminal` / `Open Command Prompt` / `Git Bash Here` jika tersedia.
4. Jika tidak ada opsi tersebut, masuk ke folder `www` lalu ketik `cmd` di search bar file manager, lalu tekan Enter.
5. Setelah terminal terbuka, jalankan:

```bash / Terminal
git clone <link-repository-projek-ini>
```

Contoh:
```bash / Terminal
git clone https://github.com/username/nama-repo.git
```

Setelah clone selesai, masuk ke folder project.

## Persiapan Database

Buat database baru di MySQL/Laragon dengan nama:

```sql
presensi
```

Database dibuat dalam keadaan kosong, lalu nanti akan diisi lewat migration dan seeder.

## Instalasi Dependensi

Jalankan di terminal project:

```bash / Terminal
composer install
```

Jika terjadi masalah saat install, bisa pakai:

```bash / Terminal
composer update
```

## Setup Environment

buat file `.env.example` menjadi `.env`:

```bash / Terminal
copy .env.example .env
```

Pada Windows PowerShell:

```powershell
Copy-Item .env.example .env
```

Setelah itu, generate app key:

```bash / Terminal
php artisan key:generate
```

## Konfigurasi Database di .env

Buka file `.env` lalu sesuaikan konfigurasi database seperti berikut:

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=presensi
DB_USERNAME=root
DB_PASSWORD=
```

Jika setup database Laragon kamu berbeda, sesuaikan username dan password sesuai konfigurasi local.

## Migrasi dan Seeder

Jalankan migrasi database:

```bash / Terminal
php artisan migrate
```

Jika migrasi gagal atau ada error yang berkaitan dengan struktur tabel, coba:

```bash / Terminal
php artisan migrate:fresh
```

Lalu jalankan seeder:

```bash / Terminal
php artisan db:seed
```

## Menjalankan Aplikasi

Jalankan server lokal:

```bash / Terminal
php artisan serve
```

Buka browser dan akses:

```text
http://127.0.0.1:8000
```

## Login Default

Data akun default dibuat di lokasi file:

- [database/seeders/DatabaseSeeder.php](database/seeders/DatabaseSeeder.php)

Akun admin:

- Email: `admin@absensi.com`
- Password: `admin123`

Akun wali kelas:

- Email: `budi@absensi.com`
- Password: `budi01`

## QR Code Scanner

Saat melakukan scanning QR, tanda bahwa proses absensi berhasil adalah:

- Bingkai scanner berubah menjadi hijau
- Artinya QR berhasil terbaca dan valid

Jika bingkai scanner tidak berubah hijau, biasanya ada masalah pada data QR, token, atau proses validasi.

## Catatan Penting

- Database harus dibuat terlebih dahulu dengan nama `presensi`.
- Pastikan `.env` sudah terisi benar sebelum menjalankan migrate.
- Jika ada error saat migrate, lakukan `php artisan migrate:fresh` lalu coba lagi.
- Setelah `db:seed`, akun login default akan tersedia otomatis.

## Troubleshooting Singkat

### 1. `composer install` gagal
```bash / Terminal
composer update
```

### 2. `php artisan migrate` gagal
```bash / Terminal
php artisan migrate:fresh
php artisan db:seed
```

### 3. QR tidak valid
Periksa data siswa dan token QR yang dibuat di seeder, lalu coba scan kembali.

## Sumber Data Default

Semua data akun default dan data awal project disiapkan di:

- [database/seeders/DatabaseSeeder.php](database/seeders/DatabaseSeeder.php)