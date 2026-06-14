# Feature Batch F03 — Backend Migration

## 🎯 Tujuan Migrasi Backend
Memindahkan kode server (backend Express.js 5 & Prisma ORM) ke folder `server/` (sebelumnya `tb-backend/` - legacy) di bawah repositori terpadu **TB-Toko-Bangunan** guna mempermudah sinkronisasi API dan skema database.

---

## 📦 Ringkasan Migrasi
- Direktori `server/` (sebelumnya `tb-backend/` - legacy) dipindahkan ke root `TB-Toko-Bangunan`.
- Folder dependencies (`node_modules`) dan folder `.git` sub-proyek lama dibuang sebelum proses penyalinan.
- Berkas database lokal SQLite `prisma/dev.db` dan kredensial `.env` tidak diikutsertakan.
- Database lokal dibuat bersih dari awal menggunakan perintah migrasi Prisma, dilanjutkan dengan seeding data dummy/awal menggunakan `seed.ts` lokal.
- Dev server backend berhasil dijalankan dan mendengarkan permintaan di port `5000` dengan lancar.

---

## 📌 Catatan Tambahan (Notes)
- **Git Protection**: Berkas `dev.db` harus tetap dimasukkan ke dalam daftar `.gitignore` agar tidak ter-commit ke repositori Git global.
- **Status Integrasi**: Pengujian integrasi lokal (Local Integration Test) antara frontend dan backend masih dalam status **Pending**.
