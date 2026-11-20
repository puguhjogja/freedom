# TOKO KITA — Website + Dashboard Admin + Dashboard Penjual

Paket berisi:
- `index.html` — katalog pelanggan (promo & tak terbatas), pencarian/kategori, share produk, keranjang, checkout WhatsApp, pendaftaran penjual.
- `admin.html` — dashboard admin (pesanan/penjual/produk/pengaturan).
- `seller.html` — **dashboard penjual** (login via kode akses, kelola produk, lihat pesanan).
- `Code.gs` — backend Google Apps Script + Google Spreadsheet.

## Fitur Baru v2
- ✅ Dashboard penjual mandiri (login kode akses via WhatsApp)
- ✅ **Masa aktif promo**: harga khusus + tanggal mulai/berakhir otomatis
- ✅ **Masa aktif tak terbatas**: produk tampil selamanya
- ✅ Badge promo/tak terbatas di katalog
- ✅ Harga coret otomatis saat promo aktif
- ✅ Penjual hanya bisa mengelola produknya sendiri
- ✅ Pesanan difilter per penjual

## A. Siapkan Google Spreadsheet
1. Buat Google Spreadsheet baru.
2. Salin ID dari URL: `https://docs.google.com/spreadsheets/d/ID_SPREADSHEET/edit`.
3. Buka **Extensions → Apps Script**, tempel `Code.gs`.
4. Ganti `PASTE_SPREADSHEET_ID_HERE` dan `GANTI_PASSWORD_ADMIN_YANG_KUAT`.
5. Jalankan `initialize` sekali (setujui izin) — membuat tab database baru.
6. **Deploy → New deployment → Web app** (Execute as: Me, Who has access: Anyone).
7. Salin URL `/exec`.

> ⚠️ Jika spreadsheet lama sudah memiliki sheet `Products`, **hapus dulu** sheet lama lalu jalankan `initialize()` agar kolom promo/sellerId baru terbentuk.

## B. Hubungkan halaman
Pada `index.html`, `admin.html`, dan `seller.html`, ganti:
`PASTE_GOOGLE_APPS_SCRIPT_WEB_APP_URL_HERE` → URL `/exec`.

## C. Upload ke GitHub
1. Upload `index.html`, `admin.html`, `seller.html`, `README.md` ke root repo.
2. **Settings → Pages → Deploy from branch → main /root → Save**.
3. URL:
   - Toko: `https://USERNAME.github.io/toko-kita/`
   - Admin: `https://USERNAME.github.io/toko-kita/admin.html`
   - **Penjual: `https://USERNAME.github.io/toko-kita/seller.html`**

## D. Alur Kerja
1. **Pembeli** belanja di `index.html` → checkout WA.
2. **Calon penjual** daftar di `index.html` → WA admin.
3. **Admin** login `admin.html` → tab **Penjual** → **Setujui + Kode Akses** → kode dikirim via WA.
4. **Penjual** login `seller.html` dengan kode → tambah produk (Promo/Tak Terbatas) → kelola & lihat pesanan.
5. **Admin** juga bisa tambah produk langsung dengan masa aktif promo/tak terbatas.

## Masa Aktif Produk
| Tipe | Perilaku |
|---|---|
| **∞ Tak Terbatas** | Produk tampil selamanya (selama status Aktif dan penjual aktif) |
| **🔥 Promo** | Harga khusus berlaku antara tanggal mulai–berakhir. Sebelum mulai: tampil harga normal dengan badge "Terjadwal". Setelah berakhir: tampil harga normal dengan badge "Berakhir". Saat aktif: harga coret + badge "Promo Aktif". |

## Catatan
- Foto produk via URL publik (hosting gambar eksternal).
- Nota dikirim sebagai teks WhatsApp, bukan PDF.
- Backend JSONP (GET) — jangan kirim data sensitif di URL.
- Password admin server-side, token 6 jam. Token penjual juga 6 jam.
- Masa aktif penjual dikelola manual admin (belum auto-nonaktif).