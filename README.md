# TOKO KITA — Website + Dashboard Admin

Paket berisi:
- `index.html` — katalog pelanggan, pencarian/kategori, share produk, keranjang, checkout WhatsApp, pendaftaran penjual.
- `admin.html` — dashboard admin terpisah, manajemen pesanan/penjual/produk/pengaturan rekening.
- `Code.gs` — backend Google Apps Script dan koneksi Google Spreadsheet.

## A. Siapkan Google Spreadsheet
1. Buat Google Spreadsheet baru.
2. Salin ID spreadsheet dari URL: `https://docs.google.com/spreadsheets/d/ID_SPREADSHEET/edit`.
3. Buka **Extensions → Apps Script**.
4. Hapus kode awal, tempel isi `Code.gs`.
5. Ganti `PASTE_SPREADSHEET_ID_HERE` dengan ID spreadsheet.
6. Ganti `GANTI_PASSWORD_ADMIN_YANG_KUAT` dengan password admin yang kuat.
7. Jalankan fungsi `initialize` satu kali dari editor Apps Script dan setujui izin. Fungsi ini membuat tab database.
8. Pilih **Deploy → New deployment → Web app**.
   - Execute as: **Me**
   - Who has access: **Anyone**
9. Klik Deploy, salin URL Web app yang berakhiran `/exec`.

## B. Hubungkan halaman
Pada `index.html` dan `admin.html`, cari:
`PASTE_GOOGLE_APPS_SCRIPT_WEB_APP_URL_HERE`
Ganti dengan URL `/exec` dari Apps Script. Simpan.

## C. Upload ke GitHub
1. Buat repository baru, misalnya `toko-kita`.
2. Upload `index.html` dan `admin.html` ke root repository.
3. Buka **Settings → Pages**.
4. Pilih **Deploy from a branch**, branch `main`, folder `/root`, lalu Save.
5. Tunggu alamat GitHub Pages aktif.
6. Toko: `https://USERNAME.github.io/toko-kita/`
7. Admin: `https://USERNAME.github.io/toko-kita/admin.html`

## D. Pengaturan pertama
1. Buka halaman admin dan login memakai password yang ditentukan di `Code.gs`.
2. Masuk tab **Pengaturan** dan isi nomor WhatsApp admin dengan format internasional tanpa `+` (contoh `62812...`), serta nama bank, nomor rekening, dan nama pemilik.
3. Tambahkan produk melalui tab Produk.
4. Pendaftaran penjual masuk ke tab Penjual dengan status Menunggu. Admin dapat menyetujui dan menentukan masa aktif. WhatsApp penjual dibuka dengan informasi rekening admin.
5. Pesanan masuk ke tab Pesanan. Tombol konfirmasi mengubah status dan membuka WhatsApp pembeli berisi nota teks.

## Catatan penting
- Ini versi awal yang ringan. Foto produk menggunakan URL gambar publik; unggah gambar ke layanan hosting gambar lalu tempel URL-nya.
- Nota dikirim sebagai teks terformat melalui WhatsApp, bukan file PDF. Pengiriman WhatsApp tetap memerlukan admin menekan tombol kirim di aplikasi WhatsApp.
- Masa aktif penjual dicatat dan dikelola admin. Versi ini belum otomatis menonaktifkan produk penjual saat masa aktif habis.
- Backend memakai JSONP agar halaman GitHub Pages dapat berkomunikasi dengan Apps Script. Karena JSONP menggunakan GET, jangan menaruh data sensitif pelanggan di URL. Password admin diverifikasi server-side dan token login berumur 6 jam.
- Untuk toko produksi dengan data pembayaran sensitif, disarankan menambah autentikasi yang lebih kuat, pembatasan akses, validasi pembayaran, dan mekanisme upload gambar khusus.
