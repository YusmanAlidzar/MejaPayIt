# 🍽️ MejaPayIt - Point of Sale (POS) System

**MejaPayIt** adalah sistem Point of Sale (POS) modern yang dirancang khusus untuk restoran dan kafe. Dibangun dengan teknologi web mutakhir (Laravel 12 + React 19 + Inertia.js) untuk memberikan pengalaman yang mulus bagi pelanggan (self-order/digital menu) maupun kasir/administrator.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Laravel](https://img.shields.io/badge/Laravel-12.x-red.svg)
![React](https://img.shields.io/badge/React-19.x-blue.svg)
![TypeScript](https://img.shields.io/badge/TypeScript-5.x-blue.svg)
![Database](https://img.shields.io/badge/Database-SQLite-lightgrey.svg)

---

## ✨ Fitur Utama

### 🛍️ Antarmuka Pelanggan (Customer Interface)
- **Menu Digital Interaktif**: Katalog produk responsif dengan foto, deskripsi, dan kategori.
- **Smart Cart**: Keranjang belanja tersimpan otomatis di browser (`localStorage`).
- **Pencarian & Filter Cepat**: Filter berdasarkan kategori menu dan pencarian teks.
- **Table Number System**: Input nomor meja dan nama pemesan saat checkout.
- **Mobile Optimized**: Tampilan ramah perangkat ponsel (layar sentuh / scan QR di meja).

### 💳 Sistem Pembayaran
- **Integrasi Midtrans**: Dukungan QRIS, Gopay, Transfer Bank / Virtual Account.
- **Kalkulasi Pajak Otomatis**: Perhitungan pajak (default 10%) transparan pada nota.
- **Pelacakan Status Real-time**: Pelanggan dapat memantau pesanan (Pending → Diproses → Selesai).
- **Digital Receipt**: Bukti pesanan digital yang dapat disimpan oleh pelanggan.

### 🔧 Dashboard Admin
- **Manajemen Menu**: Tambah, ubah, hapus produk makanan & minuman beserta foto.
- **Manajemen Kategori**: Kelompokkan menu (Makanan, Minuman, Dessert, dll.).
- **Monitor Pesanan**: Pantau dan perbarui status pesanan yang masuk secara langsung.
- **Laporan & Riwayat**: Rekapitulasi transaksi dan pembayaran.
- **Quick Switch**: Akses langsung ke dashboard atau logout dari header menu pelanggan.

### 🖨️ Cetak Struk (Thermal Printer)
- Dukungan printer kasir thermal ESC/POS (USB / Network).
- Format struk otomatis siap cetak saat pesanan selesai.

---

## 🏗️ Tech Stack

- **Backend**: Laravel 12.x, Inertia.js (PHP 8.2+)
- **Database**: SQLite (default, zero-config) atau MySQL/MariaDB
- **Frontend**: React 19, TypeScript, Tailwind CSS v4, shadcn/ui, Lucide Icons
- **Build Tool**: Vite
- **Payment Gateway**: Midtrans Snap SDK

---

## 🚀 Panduan Inisiasi & Setup Awal

### Persyaratan Sistem
- **PHP** 8.2 atau lebih baru (dengan extension `openssl`, `pdo_sqlite`, `sqlite3`, `fileinfo`, `zip`, `gd`, `intl`, `mbstring`, `curl`)
- **Composer** (atau `composer.phar` di folder project)
- **Node.js** 18+ dan **NPM**

### Langkah Inisiasi Pertama Kali

1. **Clone Repository / Buka Folder Project**:
   ```bash
   git clone https://github.com/YusmanAlidzar/MejaPayIt.git
   cd MejaPayIt
   ```

2. **Salin Environment File**:
   ```bash
   copy .env.example .env
   ```
   Pastikan di file `.env`:
   ```env
   APP_NAME=MejaPayIt
   APP_URL=http://localhost:8000
   DB_CONNECTION=sqlite
   ```

3. **Install Dependencies PHP & Node.js**:
   ```bash
   # PHP dependencies
   php composer.phar install
   # atau jika composer terpasang global:
   composer install

   # Node.js dependencies
   npm install
   ```

4. **Generate Application Key**:
   ```bash
   php artisan key:generate
   ```

5. **Setup Database & Seeding Awal**:
   ```bash
   # Buat file database SQLite jika belum ada (Windows PowerShell):
   New-Item -ItemType File -Path "database/database.sqlite" -Force

   # Jalankan migrasi dan data dummy:
   php artisan migrate --seed
   ```

6. **Hubungkan Storage Publik**:
   ```bash
   php artisan storage:link
   ```

7. **Build Aset Frontend**:
   ```bash
   npm run build
   ```

---

## 🏃 Cara Menjalankan Aplikasi Secara Manual

Setelah langkah instalasi di atas selesai, Anda dapat menjalankan aplikasi dengan salah satu metode berikut:

### Opsi 1: Mode Development (Disarankan saat Mengedit Kode)
Gunakan 2 terminal terpisah agar perubahan frontend langsung ter-update (Hot Module Replacement):

- **Terminal 1 (Backend Laravel)**:
  ```bash
  php artisan serve
  ```
  *(Server berjalan di `http://127.0.0.1:8000`)*

- **Terminal 2 (Frontend Vite Hot-Reload)**:
  ```bash
  npm run dev
  ```

---

### Opsi 2: Mode Single Terminal (Aset Sudah Di-build)
Jika Anda hanya ingin menjalankan aplikasi tanpa mengedit UI frontend secara aktif:

1. Jalankan build satu kali:
   ```bash
   npm run build
   ```
2. Cukup jalankan server Laravel:
   ```bash
   php artisan serve
   ```
3. Buka browser di [http://localhost:8000](http://localhost:8000).

---

### Opsi 3: One-Command All-in-One
Project ini dilengkapi script `concurrently` bawaan untuk menyalakan backend, queue, logs, dan vite sekaligus dalam satu perintah:
```bash
composer run dev
```

---

## 🔑 Akun & Kredensial Default

Setelah menjalankan `php artisan migrate --seed`, akun admin berikut siap digunakan:

| Role | URL Login | Email | Password |
|---|---|---|---|
| **Admin** | [http://localhost:8000/login](http://localhost:8000/login) | `admin@example.com` | `password` |
| **Test User** | [http://localhost:8000/login](http://localhost:8000/login) | `test@example.com` | `password` |

Menu Pelanggan / Self-Order dapat langsung dibuka di halaman utama:
👉 **[http://localhost:8000](http://localhost:8000)**

---

## 🔧 Konfigurasi Midtrans (Opsional untuk Pembayaran Digital)

Untuk mengaktifkan pembayaran online via Midtrans:
1. Daftar atau masuk ke akun Sandbox di [Midtrans](https://midtrans.com).
2. Dapatkan **Server Key** dan **Client Key**.
3. Isi pada file `.env`:
   ```env
   MIDTRANS_SERVER_KEY=SB-Mid-server-xxxxxxxxx
   MIDTRANS_CLIENT_KEY=SB-Mid-client-xxxxxxxxx
   MIDTRANS_MERCHANT_ID=Gxxxxxxxxx
   MIDTRANS_IS_PRODUCTION=false
   ```

---

## 📁 Struktur Direktori Project

```
MejaPayIt/
├── app/
│   ├── Http/Controllers/     # Controller (Menu, Checkout, Print, dll)
│   ├── Models/               # Model Eloquent (Product, Order, Payment)
│   └── Providers/
├── database/
│   ├── database.sqlite       # File database SQLite lokal
│   ├── migrations/          # Struktur tabel database
│   └── seeders/             # Data awal menu & admin user
├── resources/
│   ├── js/                  # Frontend React + TypeScript
│   │   ├── components/      # UI components (shadcn/ui, modal, cart)
│   │   ├── pages/
│   │   │   ├── customer/    # Menu digital, checkout, tracking pesanan
│   │   │   └── admin/       # Dashboard & manajemen menu
│   │   └── types/           # Definisi TypeScript
│   └── css/                 # Styling Tailwind CSS
├── routes/
│   ├── web.php              # Rute web aplikasi
│   └── auth.php             # Rute otentikasi login
├── public/                  # Aset publik & build hasil kompilasi
├── .env                     # File konfigurasi environment
├── composer.json            # Dependensi PHP
└── package.json             # Dependensi Node.js & React
```

---

## 📄 Lisensi
Project ini menggunakan lisensi [MIT License](LICENSE.md). Bebas digunakan dan dimodifikasi untuk kebutuhan operasional restoran atau kafe Anda.