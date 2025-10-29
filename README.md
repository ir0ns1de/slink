# Simple Shortlink

Aplikasi shortlink sederhana yang menggunakan Google Spreadsheet sebagai database utama. Aplikasi ini sepenuhnya berbasis HTML dan tidak memerlukan server backend tambahan, kecuali Google Apps Script untuk menangani API.

## Deskripsi

Aplikasi ini memungkinkan Anda membuat dan mengelola shortlink dengan mudah. Pengguna dapat membuat shortlink melalui halaman web sederhana, dan shortlink tersebut akan mengarahkan ke URL asli. Semua data disimpan di Google Spreadsheet, sehingga mudah dikelola tanpa perlu database eksternal.

## Fitur

- **Buat Shortlink**: Generate kode unik (6 karakter) dan buat shortlink dari URL panjang.
- **Redirect Otomatis**: Shortlink akan mengarahkan pengguna ke URL asli dengan animasi loading.
- **Validasi API Key**: Pastikan hanya pengguna yang memiliki key yang bisa membuat shortlink.
- **UI Sederhana**: Menggunakan Tailwind CSS untuk tampilan yang responsif dan modern.
- **Error Handling**: Menangani kesalahan seperti kode tidak ditemukan atau koneksi gagal.

## Persyaratan

- Akun Google (untuk Google Spreadsheet dan Apps Script).
- Hosting statis untuk file HTML (misalnya GitHub Pages, Vercel, atau hosting lainnya).

## Instalasi dan Setup

### 1. Buat Google Spreadsheet

1. Buka [Google Sheets](https://sheets.google.com).
2. Buat spreadsheet baru.
3. Beri nama sheet pertama sebagai `Data` (atau ubah konstanta `SHEET_NAME` di kode Apps Script jika berbeda).
4. Tambahkan header di baris pertama: `no | kode | link`.
   - Kolom `no`: Nomor urut (otomatis).
   - Kolom `kode`: Kode unik shortlink.
   - Kolom `link`: URL asli.

### 2. Setup Google Apps Script

1. Di spreadsheet yang sama, buka **Extensions > Apps Script**.
2. Hapus kode default dan salin isi dari file `apps.txt` ke editor.
3. Ubah konstanta jika diperlukan:
   - `SHEET_NAME`: Nama sheet (default: 'Data').
   - `API_KEY`: Ganti dengan API key unik Anda sendiri (misalnya: 'my-secret-key-123').
4. Simpan proyek dengan nama yang sesuai (misalnya: "Shortlink API").
5. Deploy sebagai web app:
   - Klik **Deploy > New deployment**.
   - Pilih type: **Web app**.
   - Set **Execute as**: Me (your email).
   - Set **Who has access**: Anyone (atau sesuai kebutuhan).
   - Klik **Deploy** dan salin URL endpoint yang dihasilkan (misalnya: `https://script.google.com/macros/s/YOUR_SCRIPT_ID/exec`).

### 3. Setup File HTML

1. Upload file `index.html`, `go.html`, dan `lorip.js` ke hosting statis Anda (misalnya GitHub Pages atau Vercel).
2. Edit file `lorip.js`:
   - Ganti `ENDPOINT` dengan URL dari langkah 2 di atas.
   - `BASE_URL` sudah otomatis mengikuti domain hosting Anda.
3. Pastikan file `lorip.js` tidak dipublikasikan secara publik (atur permission server jika perlu).

## Cara Penggunaan

### Membuat Shortlink

1. Kunjungi halaman `go.html` (misalnya: `https://yourdomain.com/go.html`).
2. Isi form:
   - **Unique Code**: Masukkan kode unik (6 karakter) atau klik "Generate" untuk auto-generate.
   - **Link**: Masukkan URL asli (misalnya: `https://example.com`).
   - **Pass to Create**: Masukkan API key yang Anda set di Apps Script.
3. Klik **Buat Shortlink**.
4. Jika berhasil, Anda akan mendapat shortlink seperti: `https://yourdomain.com?s=ABC123`.

### Menggunakan Shortlink

- Kunjungi shortlink tersebut, dan Anda akan diarahkan ke URL asli dengan halaman loading di `index.html`.

## Struktur File

- `index.html`: Halaman redirect dengan animasi loading.
- `go.html`: Halaman untuk membuat shortlink.
- `lorip.js`: Konfigurasi endpoint dan base URL.
- `apps.txt`: Kode Google Apps Script untuk API (doGet dan doPost).

## Troubleshooting

- **Error: API key tidak valid**: Pastikan API key di form dan di Apps Script sama.
- **Error: Sheet tidak ditemukan**: Pastikan nama sheet di Apps Script sesuai dengan spreadsheet.
- **Redirect tidak berfungsi**: Periksa URL endpoint di `lorip.js` dan pastikan Apps Script di-deploy dengan akses publik.
- **Kode duplikat**: Jika kode sudah ada, gunakan kode lain.

## Kontribusi

Silakan buat issue atau pull request jika ada perbaikan atau fitur tambahan.

## Lisensi

Proyek ini open-source. Gunakan sesuai kebutuhan Anda.

---

**Catatan**: Pastikan untuk mengamankan API key dan tidak membagikannya secara publik. Jika digunakan untuk production, pertimbangkan validasi tambahan.