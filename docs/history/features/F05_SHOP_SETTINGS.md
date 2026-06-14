# Application Feature F05 — Shop Settings

## 🎯 Detail Status Fitur
- **Title**: Shop Settings
- **Status**: **Draft / Needs Discovery**
- **Feature Type**: Configuration
- **User Role**: Admin
- **Discovery Status**: Pending Audit UI/API/Data

---

## 📝 Deskripsi (Purpose)
Memungkinkan admin mengonfigurasi profil fisik toko bangunan (nama toko, alamat, dan nomor telepon) yang akan dicetak di struk belanja, serta mengatur threshold stok tipis global.

---

## 🛠️ Peta Wilayah Teknis (Possible Areas)
- **Antarmuka (UI Area)**: Halaman pengaturan `/admin/settings`, formulir konfigurasi.
- **API Area (Backend)**: Controller pengaturan global (`/api/settings/*`) Express.
- **Database Area**: Model `Setting` (yang berisi data tunggal global di database).

---

## 📌 Catatan Tambahan (Notes)
- Tabel setting disarankan di-seed di awal dengan data default agar endpoint `/api/settings` dapat membaca tanpa kesalahan database.
