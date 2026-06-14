# Rencana Migrasi & Konsolidasi Repositori (Migration Plan)

Dokumen ini mencatat rencana strategis penyatuan repositori `tb-frontend` dan `tb-backend` ke dalam satu repositori utama `TB-Toko-Bangunan`.

---

## 🎯 Tujuan Proyek
Mempermudah manajemen repositori di GitHub dengan menyatukan frontend dan backend ke dalam struktur sub-folder pada satu repositori tunggal tanpa mengganggu jalannya aplikasi yang sudah stabil.

---

## 🧼 Aturan Kebersihan Git & Eksklusi File
Untuk memastikan proses migrasi berjalan aman tanpa membocorkan kredensial lokal dan menjaga repositori tetap bersih:
- **Eksklusi `.git`**: Folder `.git` dari folder lama (`tb-frontend` dan `tb-backend`) tidak boleh ikut disalin ke repositori baru. Git history akan menggunakan repositori baru `TB-Toko-Bangunan`.
- **Eksklusi `.env*`**: File `.env` (backend) dan `.env.local` (frontend) tidak boleh dimasukkan ke Git. Versi contoh (`.env.example`) disediakan untuk setup lokal baru.
- **Eksklusi `dev.db`**: File database SQLite (`prisma/dev.db`) tidak boleh di-commit.
- **Eksklusi Build & Dependencies**: Folder `node_modules`, `.next`, `dist`, dan `build` diabaikan sepenuhnya.

---

## 🏗️ Struktur Target Folder

```text
TB-Toko-Bangunan/
├── docs/                # Folder dokumentasi ini
├── tb-frontend/         # Folder kode frontend
└── tb-backend/          # Folder kode backend
```

---

## 🚀 Tahapan Migrasi

### Fase 1: Inisialisasi Dokumentasi Awal (Sedang Berjalan)
- Membuat struktur direktori `docs/`.
- Menyiapkan file-file overview dan konfigurasi dasar.
- Berhenti untuk melaporkan kesiapan dokumen ke user.

### Fase 2: Pemindahan Frontend (`tb-frontend`)
- Salin folder `tb-frontend` ke target repositori dengan menerapkan daftar eksklusi.
- Buat file `.env.example` di dalam `tb-frontend/`.
- Jalankan `npm install` dan pastikan `npm run build` sukses.

### Fase 3: Pemindahan Backend (`tb-backend`)
- Salin folder `tb-backend` ke target repositori dengan menerapkan daftar eksklusi.
- Buat file `.env.example` di dalam `tb-backend/`.
- Jalankan `npm install` bersih.
- Regenerasi client database menggunakan `npx prisma generate`.
- Buat database SQLite lokal baru yang bersih dengan `npx prisma db seed`.

### Fase 4: Integrasi & Verifikasi Akhir
- Jalankan backend dan frontend secara bersamaan.
- Uji fungsionalitas login admin (`admin`/`admin123`) & CS (`cs`/`cs123`).
- Uji fungsionalitas POS, pengurangan stok, dan dashboard analitik.

---
*Status: Fase 1 - Pembuatan Dokumentasi Awal sedang berlangsung.*
