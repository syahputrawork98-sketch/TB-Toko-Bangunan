# Gambaran Umum Backend (Backend Overview)

## Purpose
Dokumen ini mendokumentasikan spesifikasi teknis, rute API, dan arsitektur backend engine dari aplikasi **TB (Toko Bangunan)**.

---

## Current Backend Status
* **Status**: **Consolidated in TB-Toko-Bangunan / Pending Local Integration Test**
* **Database Driver**: Prisma Client dengan database target SQLite.

---

## Backend Details
* **Source Path**: `server/` (di dalam repositori utama `TB-Toko-Bangunan`, sebelumnya `tb-backend/` - legacy).
* **Framework**: Express.js 5.2.1.
* **Language**: TypeScript (dijalankan lewat `ts-node-dev` untuk live reload saat development).
* **API Style**: RESTful API.
* **Auth Strategy**: JWT (JSON Web Token) dengan penyimpanan token pada cookie browser (`tb_token`). Kredensial di-hash menggunakan `bcryptjs`.

---

## Directory Structure
* `src/controllers/`: Mengatur logika bisnis (Auth, Analytics, Products, Settings, Transactions).
* `src/routes/`: Menyediakan endpoint API.
* `src/middlewares/`: Penanganan autentikasi, validasi peran user, dan penanganan error terpusat.
* `src/utils/`: Inisialisasi Prisma Client (`src/utils/db.ts`).
* `prisma/`: Berisi berkas skema database `schema.prisma` dan data awal `seed.ts`.

---

## Environment Variables
Konfigurasi lingkungan yang dibutuhkan (dibuat di `.env` sub-folder `server/`):
* `PORT`: Port jalannya server backend (default: `5000`).
* `DATABASE_URL`: Alamat database relasional (SQLite: `file:./dev.db`).
* `JWT_SECRET`: Kunci rahasia untuk tanda tangan token keamanan JWT.

---

## Next Step
1. Salin folder `server/` ke repositori target (tanpa `.git`, `node_modules`, `.env`, `prisma/dev.db`).
2. Jalankan `npm install` bersih di folder tujuan.
3. Jalankan `npx prisma generate` untuk memperbarui Prisma Client.
4. Buat database SQLite lokal baru dan lakukan seeding data awal dengan `npx prisma db seed`.
