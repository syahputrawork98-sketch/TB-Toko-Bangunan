# Application Feature F01 — Authentication & Role-Based Access

## 🎯 Detail Status Fitur
- **Title**: Authentication & Role-Based Access
- **Status**: **Draft / Needs Discovery**
- **Feature Type**: Core Application Security
- **User Role**: Admin & CS
- **Discovery Status**: Pending Audit UI/API/Data

---

## 📝 Deskripsi (Purpose)
Menangani sesi otorisasi pengguna untuk mengakses rute dasbor admin (`/admin/*`) dan kasir/CS (`/cs/*`) secara terisolasi. Mengamankan token autentikasi di tingkat klien menggunakan cookie secure HTTP-only.

---

## 🛠️ Peta Wilayah Teknis (Possible Areas)
- **Antarmuka (UI Area)**: Rute `/login`, Next.js middleware protection (`src/middleware.ts`), dan Zustand auth store.
- **API Area (Backend)**: Controller autentikasi (Login, Logout, Verify Token) dan route `/api/auth/*` di Express.
- **Database Area**: Model `User` (field username, password ter-hash, dan role `"ADMIN" | "CS"`).

---

## 📌 Catatan Tambahan (Notes)
- Penanganan token wajib menggunakan pengaman cookie HTTP-only (`tb_token`) guna meminimalkan risiko eksploitasi XSS pada browser.
