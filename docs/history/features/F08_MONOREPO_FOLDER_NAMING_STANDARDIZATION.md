# Feature Batch F08 — Monorepo Folder Naming Standardization

## 🎯 Tujuan Standardisasi
Menstandarkan nama folder sub-proyek di dalam repositori monorepo dari nama spesifik proyek lama (`tb-frontend` dan `tb-backend`) menjadi nama yang lebih bersih dan profesional (`client` dan `server`). Hal ini menyelaraskan repositori dengan best practices monorepo modern dan mempermudah pemeliharaan jangka panjang.

---

## 📦 Rename yang Dilakukan
- **Frontend**: `tb-frontend/` ➔ **`client/`**
- **Backend**: `tb-backend/` ➔ **`server/`**

---

## 📑 Dokumentasi & Konfigurasi yang Disinkronkan
Seluruh berkas panduan setup lokal, onboarding, status, dan riwayat di bawah folder `docs/` serta berkas root `README.md` telah diperbarui untuk:
1. Mengubah instruksi navigasi lokal (contoh: `cd tb-frontend` menjadi `cd client`, `cd ../tb-backend` menjadi `cd ../server`).
2. Mengubah rujukan konfigurasi path (seperti lokasi database SQLite `server/prisma/dev.db` dan `.env` paths).
3. Melabeli folder lama (`tb-frontend` dan `tb-backend`) dengan label **legacy** pada semua catatan riwayat dan konteks historis lama guna menjaga keterlacakan kronologis.

---

## 🛡️ Hal yang Tidak Diubah (Constraints)
- **Logika Bisnis**: Tidak ada logika bisnis frontend (`client/`) maupun backend (`server/`) yang diubah.
- **Skema & Migrasi Database**: Skema Prisma (`server/prisma/schema.prisma`) dan berkas migrasi tidak diubah atau ditambah.
- **Dependensi**: Tidak ada instalasi dependensi baru maupun peningkatan versi dependensi yang sudah ada.
- **Package.json**: Nama paket (`"name": "tb-frontend"` dan `"name": "tb-backend"`) pada masing-masing subfolder sengaja dipertahankan untuk menghindari efek samping pengenalan package name baru secara mendadak.
- **Git State**: Tidak dilakukan commit atau push otomatis (tahap ini diserahkan kepada User).

---

## 📌 Catatan Legacy Naming
Konteks historis pada fase pengerjaan `F00` sampai `F05-CP` tetap dipertahankan dengan label legacy `tb-frontend` dan legacy `tb-backend` agar catatan sejarah migrasi repositori lama tetap akurat secara kronologis.

---

## 🔍 Validasi yang Disarankan
1. **Pemeriksaan Teks**: Jalankan pencarian teks global untuk kata `tb-frontend` dan `tb-backend` di luar label legacy untuk memastikan tidak ada rujukan path aktif yang tertinggal.
2. **Kompilasi Ulang**:
   - Masuk ke folder `client/` lalu jalankan `npm run build` untuk memverifikasi proses build antarmuka.
   - Masuk ke folder `server/` lalu jalankan `npm run build` untuk memverifikasi proses kompilasi engine server.
3. **Pengujian Integrasi**: Jalankan server backend dan frontend secara bersamaan untuk memastikan komunikasi cross-origin API berjalan stabil pada port lokal masing-masing (`http://localhost:3000` dan `http://localhost:5000/api`).
