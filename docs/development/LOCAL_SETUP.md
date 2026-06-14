# Panduan Pengaturan Lokal (Local Setup Guide)

## Purpose
Dokumen ini memandu pengembang untuk menyiapkan lingkungan pengembangan lokal dan menjalankan aplikasi **TB (Toko Bangunan)**.

---

## 🛠️ Langkah Instalasi Awal

### 1. Prasyarat (Prerequisites)
Pastikan komputer Anda sudah terinstal:
- **Node.js** (versi 18 ke atas direkomendasikan).
- **npm** (bawaan dari instalasi Node.js).

---

## 🎨 Setup Frontend (`client`)

1. **Masuk ke folder frontend**:
   ```bash
   cd client
   ```

2. **Instal dependensi**:
   ```bash
   npm install
   ```

3. **Konfigurasi Environment**:
   Salin berkas `.env.example` menjadi `.env.local`:
   ```bash
   copy .env.example .env.local
   ```
   *Catatan: Pastikan `NEXT_PUBLIC_API_URL` mengarah ke backend engine (default: `http://localhost:5000/api`).*

4. **Jalankan aplikasi (Development)**:
   ```bash
   npm run dev
   ```
   *Aplikasi frontend akan berjalan pada `http://localhost:3000`.*

---

## 🏗️ Setup Backend (`server`)

1. **Masuk ke folder backend**:
   ```bash
   cd ../server
   ```

2. **Instal dependensi**:
   ```bash
   npm install
   ```

3. **Konfigurasi Environment**:
   Salin berkas `.env.example` menjadi `.env`:
   ```bash
   copy .env.example .env
   ```
   *Catatan: Anda dapat menyesuaikan isi `JWT_SECRET` untuk keamanan sesi.*

4. **Setup Database (Prisma & SQLite)**:
   Jalankan perintah berikut untuk membuat database SQLite lokal baru, menerapkan skema, men-generate Prisma Client, dan memasukkan data seeder awal:
   ```bash
   npx prisma generate
   npx prisma migrate dev --name init
   npx prisma db seed
   ```

5. **Jalankan backend engine (Development)**:
   ```bash
   npm run dev
   ```
   *Backend API akan berjalan pada `http://localhost:5000`.*

---

## 🔑 Kredensial Login Default (Untuk Pengujian)

Setelah berhasil melakukan *seeding* database, gunakan akun berikut untuk masuk ke dashboard:

| Peran | Username | Password |
| :--- | :--- | :--- |
| **Super Admin** | `admin` | `admin123` |
| **Customer Service** | `cs` | `cs123` |

---

## ⚠️ Masalah Umum (Known Issues) & Penanganan

### Database File Lock (Isu Windows SQLite)
* **Masalah**: Pesan error "database file is locked" atau kegagalan penulisan saat transaksi.
* **Solusi**: Pastikan tidak ada aplikasi database viewer pihak ketiga yang sedang membuka file `server/prisma/dev.db` secara eksklusif. Matikan dev server backend sebentar, lalu jalankan `npx prisma generate` ulang.
