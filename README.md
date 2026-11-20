# TOKO KITA — Toko, Portal Penjual, Admin & Google Sheets

Isi paket:
- `index.html` — toko pembeli, katalog, keranjang, checkout, pendaftaran penjual.
- `penjual.html` — halaman login penjual, tambah produk, lihat status, dan hapus produk.
- `admin.html` — dashboard admin, persetujuan penjual dan produk, pesanan, pengaturan, serta tambah/edit/simpan/hapus produk.
- `Code.gs` — backend Google Apps Script yang menghubungkan semua halaman ke satu Spreadsheet.

## 1. Siapkan Google Spreadsheet dan Apps Script
1. Buat Google Spreadsheet baru dan salin ID dari URL di antara `/d/` dan `/edit`.
2. Buka **Ekstensi → Apps Script**.
3. Ganti seluruh kode di editor dengan isi file `Code.gs` dari paket ini.
4. Pada bagian atas `Code.gs`, ganti:
   - `PASTE_SPREADSHEET_ID_HERE` dengan ID Spreadsheet.
   - `GANTI_PASSWORD_ADMIN_YANG_KUAT` dengan password admin yang kuat.
5. Simpan, pilih fungsi `initialize`, lalu klik **Run/Jalankan** dan berikan izin Google.
6. Jika memakai Spreadsheet dari versi TOKO KITA sebelumnya, tetap gunakan Spreadsheet yang sama. Kode baru menambahkan kolom `sellerId` dan `passwordHash` secara otomatis tanpa menghapus data yang sudah ada.

## 2. Deploy sebagai Web App
1. Klik **Deploy → New deployment → Web app**.
2. **Execute as:** Me.
3. **Who has access:** Anyone.
4. Klik Deploy dan salin URL yang berakhiran `/exec`.
5. Jika Google meminta otorisasi, selesaikan prosesnya.

## 3. Jika memperbarui dari versi TOKO KITA sebelumnya
1. Buka Apps Script yang terhubung ke Spreadsheet toko.
2. Ganti seluruh kode lama dengan `Code.gs` terbaru dari paket ini, lalu simpan.
3. Jalankan fungsi `initialize` satu kali. Kolom `storeCode` akan ditambahkan otomatis dan kode untuk penjual lama akan dibuat dari ID penjual. Data produk, pesanan, dan akun yang sudah ada tidak dihapus.
4. Buka **Deploy → Manage deployments**, pilih deployment Web App, klik Edit, pilih **New version**, lalu Deploy. Gunakan URL `/exec` yang sama jika deployment tetap sama.

## 4. Pasang URL Apps Script pada tiga halaman
Di masing-masing file `index.html`, `admin.html`, dan `penjual.html`, cari:
`PASTE_GOOGLE_APPS_SCRIPT_WEB_APP_URL_HERE`
Ganti seluruh teks itu dengan URL `/exec` hasil deploy. Gunakan URL yang sama di ketiga file.

## 5. Upload ke GitHub Pages
1. Upload hanya tiga file halaman ke root repository GitHub: `index.html`, `penjual.html`, dan `admin.html`. File `Code.gs` ditempel di editor Apps Script, tidak perlu dipublikasikan di GitHub Pages.
2. Buka **Settings → Pages**.
3. Pilih **Deploy from a branch**, branch `main`, folder `/root`, lalu Save.
4. Setelah aktif, alamat halaman:
   - Toko pembeli: `https://USERNAME.github.io/NAMA-REPO/`
   - Portal penjual: `https://USERNAME.github.io/NAMA-REPO/penjual.html`
   - Admin: `https://USERNAME.github.io/NAMA-REPO/admin.html`

## 6. Alur penggunaan penjual
1. Calon penjual membuka toko dan klik **Gabung Jadi Penjual**.
2. Isi data termasuk nomor WhatsApp dan password akun (minimal 6 karakter). Password jangan digunakan ulang di layanan lain.
3. Admin membuka dashboard → tab **Penjual** → klik **Setujui** dan tentukan jumlah hari masa aktif.
4. Setelah disetujui, penjual login di halaman `penjual.html` menggunakan nomor WhatsApp dan password yang dibuat saat daftar.
5. Penjual menambahkan produk. Produk berstatus **Menunggu** dan belum terlihat di katalog.
6. Admin membuka tab **Produk**, lalu menyetujui atau menolak produk.
7. Produk yang disetujui tampil di toko. Produk dari penjual juga otomatis tidak ditampilkan jika masa aktif penjual berakhir.

## 7. Pengaturan admin
- Login admin menggunakan password yang ditetapkan di `Code.gs`.
- Tab Pengaturan untuk mengubah WhatsApp admin dan informasi rekening.
- Tab Pesanan untuk melihat pesanan dan mengonfirmasi nota melalui WhatsApp.
- Tab Penjual untuk menyetujui akun dan menetapkan masa aktif.
- Tab Produk untuk meninjau produk yang dikirim penjual, serta menambah, mengedit, menyimpan perubahan, mengubah status, dan menghapus produk.

## 8. Format nomor WhatsApp
- Bisa memasukkan nomor lokal seperti `081234567890` atau format internasional seperti `6281234567890`.
- Format yang paling disarankan adalah `628xxxxxxxxxx`: gunakan kode negara `62`, hilangkan angka `0` di depan, dan jangan gunakan tanda `+`, spasi, atau strip.
- Contoh: `089653135369` menjadi `6289653135369`. Sistem akan menormalkan nomor sebelum menyimpan atau membuka WhatsApp.

## 9. Catatan
- Foto produk saat ini memakai **URL gambar publik**, bukan upload file langsung ke server. Tempel tautan gambar yang bisa dibuka publik.
- WhatsApp terbuka dengan teks yang sudah disiapkan; admin/penjual tetap menekan tombol kirim di aplikasi WhatsApp.
- Portal penjual menggunakan akun yang dibuat saat pendaftaran. Pendaftaran harus disetujui admin dan masa aktif harus berlaku.
- API pada paket ini memakai JSONP/GET agar kompatibel dengan GitHub Pages dan Apps Script. Karena parameter permintaan ikut berada di URL, gunakan password unik khusus TOKO KITA, jangan gunakan password yang sama dengan akun lain. Untuk operasional dengan keamanan lebih tinggi, backend sebaiknya ditingkatkan ke autentikasi dan endpoint POST.
- Jangan bagikan URL dashboard admin dan password admin kepada penjual.
