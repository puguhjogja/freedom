# TOKO KITA - Aplikasi Toko Online WhatsApp & Multi-Vendor

## Daftar File di Dalam Paket Ini
1. `code.gs` — Kode Backend & Setup Otomatis untuk Google Apps Script.
2. `index.html` — Halaman Utama Katalog Pembeli, Share Produk Gambar, & Pendaftaran Mitra.
3. `admin.html` — Dashboard Admin Satu Pintu (Konfirmasi Pesanan Pembeli & Aktivasi Akun Mitra).
4. `tambah-produk.html` — Halaman Tersembunyi Khusus Kontributor untuk Menambah Produk.

---

## Panduan Pemasangan Cepat

### 1. Siapkan Database Google Sheets & Backend (`code.gs`)
1. Buat Google Spreadsheet baru (misal: `Database TOKO KITA`).
2. Buka menu **Extensions > Apps Script**.
3. Hapus kode bawaan, lalu salin dan tempel seluruh isi file `code.gs`.
4. Klik **Save**, pilih fungsi **`setupToko`** pada dropdown di bagian atas, lalu klik **Run** (berikan izin akses jika diminta). Semua sheet (`Produk`, `Pesanan`, `Kontributor`) dan contoh produk akan otomatis dibuat.
5. Klik **Deploy > New deployment > Web app**:
   - *Execute as:* **Me**
   - *Who has access:* **Anyone**
6. Salin **URL Web App (`/exec`)** yang muncul.

### 2. Konfigurasi File HTML
Buka file `index.html`, `admin.html`, dan `tambah-produk.html` menggunakan editor teks, lalu ganti:
- `URL_WEB_APP_ANDA` $ightarrow$ dengan URL Web App (`/exec`) dari langkah 1.
- `NOMOR_WA_ANDA` (di `index.html`) $ightarrow$ dengan nomor WhatsApp Anda berawalan `62` (contoh: `628123456789`).

### 3. Hosting Online (Gratis via GitHub Pages)
1. Buat repository baru di GitHub.
2. Unggah `index.html`, `admin.html`, dan `tambah-produk.html` ke repository tersebut.
3. Aktifkan **Settings > Pages** (pilih branch `main`).
4. Link toko Anda siap dibagikan! Semua tautan menuju `admin.html` dan `tambah-produk.html` otomatis menyesuaikan domain hosting Anda.
