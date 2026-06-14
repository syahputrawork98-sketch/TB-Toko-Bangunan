# Gambaran Umum Frontend (Frontend Overview)

## Purpose
Dokumen ini mendokumentasikan spesifikasi teknis, struktur, dan konfigurasi dari aplikasi frontend **TB (Toko Bangunan)**.

---

## Current Frontend Status
* **Status**: **Ready for Consolidation** (Stabil pada repositori lama, siap dipindahkan).
* **Dependency Check**: Menggunakan Next.js 16.2.4 dan React 19.2.4.

---

## Frontend Details
* **Source Path**: `tb-frontend/` (di dalam repositori utama `TB-Toko-Bangunan`).
* **Framework**: Next.js 16 (App Router).
* **Bahasa**: TypeScript.
* **Routing System**: Next.js App Router:
  - Rute Publik: `/login`
  - Rute Super Admin:
    - `/admin` (Analytics & Staff stats)
    - `/admin/inventory` (Kelola Produk)
    - `/admin/staff` (Kelola CS)
    - `/admin/settings` (Pengaturan Toko)
  - Rute CS (Customer Service):
    - `/cs` (Dashboard Shift)
    - `/cs/pos` (Kasir POS)
    - `/cs/inventory` (Cek Stok)
    - `/cs/history` (Riwayat Struk)
    - `/cs/settings` (Profil Mandiri)
* **Styling**: Vanilla CSS Modules (berbasis file `*.module.css` untuk memastikan kecepatan rendering tinggi tanpa dependensi tambahan).
* **State Management**: Zustand 5.0.12 dengan `persist` middleware untuk menjaga keadaan sesi login pengguna.

---

## Environment Variables
Sistem membaca konfigurasi API melalui:
* `NEXT_PUBLIC_API_URL`: Alamat dasar API backend (default lokal: `http://localhost:5000/api`).

---

## Notes
* Proteksi rute diatur pada berkas `src/middleware.ts` untuk memisahkan hak akses antara halaman `/admin/*` dan `/cs/*` menggunakan cookie JWT.

---

## Next Step
1. Salin seluruh direktori `tb-frontend/` (tanpa `.git`, `node_modules`, `.next`, `.env.local`).
2. Jalankan `npm install` bersih untuk men-download dependensi.
3. Buat berkas `tb-frontend/.env.example` untuk panduan deployment/lokal.
4. Lakukan pengetesan lokal dengan perintah `npm run dev` dan `npm run build`.
