# Application Feature F04 — Staff Management

## 🎯 Detail Status Fitur
- **Title**: Staff Management
- **Status**: **Draft / Needs Discovery**
- **Feature Type**: User & Access Control
- **User Role**: Admin
- **Discovery Status**: Pending Audit UI/API/Data

---

## 📝 Deskripsi (Purpose)
Memfasilitasi admin untuk mendaftarkan akun kasir (CS) baru, mengubah info dasar staff, serta mencabut akses masuk jika diperlukan.

---

## 🛠️ Peta Wilayah Teknis (Possible Areas)
- **Antarmuka (UI Area)**: Halaman `/admin/staff`, formulir registrasi kasir, dan tabel data akun kasir.
- **API Area (Backend)**: Controller manajemen user/staff (`/api/staff/*` atau `/api/users/*`) Express.
- **Database Area**: Penambahan data ke tabel `User` dengan penetapan filter role `"CS"`.

---

## 📌 Catatan Tambahan (Notes)
- Password kasir baru wajib di-hash menggunakan `bcryptjs` sebelum disimpan ke database SQLite.
