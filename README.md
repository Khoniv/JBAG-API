# ⚡ JBAG-API - RESTful Backend Services for JBAG Marketplace

<div align="center">

![Laravel](https://img.shields.io/badge/Laravel-11.x-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)
![PHP](https://img.shields.io/badge/PHP-8.2%2B%20%7C%208.3-777BB4?style=for-the-badge&logo=php&logoColor=white)
![Database](https://img.shields.io/badge/MySQL-8.x-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![Sanctum](https://img.shields.io/badge/Auth-Laravel%20Sanctum-red?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Active%20Production-success?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

**Layanan Backend RESTful API untuk Ekosistem Marketplace Jual Beli Akun Game (JBAG).**

[Tentang Proyek](#-tentang-proyek) • [Fitur Utama](#-fitur-utama) • [Teknologi](#-teknologi--dependensi) • [Arsitektur](#-arsitektur--struktur-direktori) • [Panduan Instalasi](#-panduan-instalasi-cepat) • [Dokumentasi API](#-dokumentasi-endpoint-api) • [Pengembang](#-pengembang--kontak)

</div>

---

## 📖 Tentang Proyek

**JBAG-API** adalah mesin backend RESTful API berbasis **Laravel 11** yang menangani seluruh proses bisnis aplikasi marketplace JBAG. Backend ini mengelola autentikasi berbasis token (*Laravel Sanctum*), transaksi pesanan, manajemen katalog game, sinkronisasi keranjang belanja, penanganan multi metode pembayaran (E-Wallet & Bank Transfer), verifikasi bukti pembayaran, hingga notifikasi pengiriman kredensial akun via email secara aman.

API ini dirancang untuk melayani aplikasi client [JBAG Flutter App](https://github.com/Khoniv/jbag-jual-beli-akun-game) dengan respon JSON standar dan tingkat keamanan tinggi.

---

## 🚀 Fitur Utama

- **Autentikasi Multi-Peran (Multi-Role Auth)**:
  - Registrasi & Login pembeli (`buyer`) dan penjual (`seller`).
  - Manajemen sesi API aman via **Laravel Sanctum**.
- **Katalog Akun Game (Account Management)**:
  - CRUD listing akun game lengkap dengan judul, deskripsi, harga, spesifikasi, dan lampiran gambar cover.
  - Fitur pencarian (*Search*) akun game berbasis kata kunci.
  - Filter akun game per penjual / toko.
- **Keranjang Belanja Dinamis (Cart Engine)**:
  - Penambahan, pembaruan kuantitas, dan penghapusan item keranjang per user.
- **Sistem Transaksi & Checkout**:
  - Pembuatan order dengan kalkulasi biaya otomatis.
  - Multi-channel metode pembayaran penjual (E-Wallet & Bank).
  - Unggah dan verifikasi gambar bukti pembayaran.
  - Perubahan siklus status transaksi (Menunggu Verifikasi, Diproses, Selesai, Dibatalkan).
- **Pengiriman Kredensial Akun Game (Secure Delivery)**:
  - Endpoint pengiriman kredensial akun game (Username & Password) kepada pembeli setelah diverifikasi.
  - Terintegrasi modul pengiriman email konfirmasi (`App\Mail`).
- **Rating & Testimoni (Reviews Engine)**:
  - Pengumpulan ulasan bintang dan ulasan tertulis dari pembeli untuk reputasi penjual.
- **Master Data Game & E-Wallet**:
  - Manajemen data referensi game yang didukung serta daftar provider e-wallet aktif.

---

## 🛠️ Teknologi & Dependensi

| Komponen | Teknologi | Deskripsi |
|---|---|---|
| **Framework** | [Laravel 11.x](https://laravel.com) | Modern PHP Web & API Framework |
| **Bahasa Pemrograman** | PHP 8.2 / 8.3 | High performance modern PHP runtime |
| **Autentikasi API** | [Laravel Sanctum](https://laravel.com/docs/sanctum) | Lightweight token authentication |
| **Database** | MySQL 8.x / MariaDB | Relational Database Management System |
| **ORM** | Eloquent ORM | Object-Relational Mapping & Model Relationships |
| **Testing** | PHPUnit 11 | Unit & Feature testing suite |
| **Client Frontend** | [JBAG Flutter App](https://github.com/Khoniv/jbag-jual-beli-akun-game) | Cross-platform Mobile & Web client |

---

## 📂 Arsitektur & Struktur Direktori

```text
JBAG-API/
├── app/
│   ├── Http/
│   │   ├── Controllers/
│   │   │   └── Api/                  # Controller endpoint RESTful API
│   │   │       ├── AkunGameController.php
│   │   │       ├── AuthController.php
│   │   │       ├── CheckoutController.php
│   │   │       ├── EwalletController.php
│   │   │       ├── GameController.php
│   │   │       ├── KeranjangController.php
│   │   │       ├── PenilaianController.php
│   │   │       └── TransaksiController.php
│   │   └── Resources/                # Transformasi JSON API Resource
│   ├── Mail/                         # Mailable classes untuk notifikasi akun
│   ├── Models/                       # Eloquent Models (User, AkunGame, Transaksi, dll.)
│   └── Providers/                    # Service Providers
├── config/                           # Konfigurasi aplikasi & database
├── database/
│   ├── migrations/                   # Skema migrasi tabel database
│   └── seeders/                      # Data awal game, e-wallet, dan dummy user
├── public/                           # Web server root & upload storage
├── routes/
│   ├── api.php                       # Definisi seluruh rute REST API
│   └── web.php                       # Rute web standar
├── storage/                          # File upload bukti transfer & cover akun
├── .env.example                      # Template variabel lingkungan
├── artisan                           # CLI Artisan runner
├── composer.json                     # Konfigurasi dependensi PHP & composer
└── README.md                         # Dokumentasi utama proyek
```

---

## 💻 Panduan Instalasi Cepat

### 1. Prasyarat Sistem
Pastikan telah terinstal:
- **PHP** >= 8.2 (ekstensi `pdo_mysql`, `mbstring`, `fileinfo`, `openssl`, `tokenizer`, `xml`)
- **Composer** (v2+)
- **MySQL / MariaDB Server**
- **Git**

### 2. Clone Repositori
```bash
git clone https://github.com/Khoniv/JBAG-API.git
cd JBAG-API
```

### 3. Pasang Dependensi Composer
```bash
composer install
```

### 4. Salin Variabel Lingkungan & Generate App Key
```bash
cp .env.example .env
php artisan key:generate
```

### 5. Atur Koneksi Database di `.env`
```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=jbag_db
DB_USERNAME=root
DB_PASSWORD=
```

### 6. Jalankan Migrasi & Storage Link
```bash
# Buat database jbag_db di MySQL terlebih dahulu, lalu:
php artisan migrate --seed
php artisan storage:link
```

### 7. Jalankan Server API Lokal
```bash
php artisan serve --host=0.0.0.0 --port=8000
```
Server REST API siap menerima request di: `http://127.0.0.1:8000/api`

---

## 📡 Dokumentasi Endpoint API

| Method | Endpoint | Deskripsi |
|---|---|---|
| `POST` | `/api/register-user` | Pendaftaran akun pembeli |
| `POST` | `/api/register-penjual` | Pendaftaran akun penjual |
| `POST` | `/api/login` | Autentikasi user & perolehan token bearer |
| `POST` | `/api/logout` | Revoke token autentikasi (Memerlukan token) |
| `GET` | `/api/akungame` | Mengambil seluruh katalog akun game |
| `GET` | `/api/akungame/search` | Mencari akun game berdasarkan kata kunci |
| `GET` | `/api/akungame/{id}` | Detail informasi spesifikasi akun game |
| `POST` | `/api/akungame` | Menambahkan listing akun game baru (Penjual) |
| `POST` | `/api/akungame/update/{id}` | Memperbarui data listing akun game |
| `DELETE` | `/api/akungame/{id}` | Menghapus listing akun game |
| `GET` | `/api/keranjang/user/{id}` | Mengambil daftar keranjang belanja pengguna |
| `POST` | `/api/keranjang` | Menambahkan item akun game ke keranjang |
| `DELETE` | `/api/keranjang/{id}` | Menghapus item dari keranjang |
| `GET` | `/api/checkout` | Mengambil metode pembayaran penjual yang aktif |
| `POST` | `/api/transaksi` | Membuat pesanan transaksi baru |
| `GET` | `/api/transaksi/user/{id}` | Riwayat transaksi milik pembeli |
| `GET` | `/api/transaksi/penjual/{id}` | Riwayat pesanan masuk ke penjual |
| `POST` | `/api/transaksi/update/{id}` | Mengunggah bukti pembayaran transaksi |
| `PATCH` | `/api/kirim-akun` | Mengirim data login akun ke pembeli |
| `GET` | `/api/penilaian/{id}` | Mengambil testimoni ulasan untuk akun |
| `POST` | `/api/penilaian` | Mengirim ulasan & rating baru |
| `GET` | `/api/games` | Daftar referensi kategori game |
| `GET` | `/api/ewallets` | Daftar referensi e-wallet |

---

## 👤 Pengembang & Kontak

* **Pengembang**: **Khonif Zakaria** ([NivDev](https://github.com/Khoniv))
* **GitHub**: [@Khoniv](https://github.com/Khoniv)
* **Email**: [oniefzk11@gmail.com](mailto:oniefzk11@gmail.com)
* **Repositori Frontend**: [Khoniv/jbag-jual-beli-akun-game](https://github.com/Khoniv/jbag-jual-beli-akun-game)

---

<div align="center">
Dibuat dengan ❤️ oleh <a href="https://github.com/Khoniv">Khonif Zakaria</a>.
</div>
