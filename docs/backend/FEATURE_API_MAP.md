# High-Level Feature API Map (Backend)

Dokumen ini memetakan area API backend tingkat tinggi yang diimplementasikan pada folder `server/` (sebelumnya `tb-backend` Express.js - legacy).

---

## 🗺️ Peta Fitur API (API Map)

| Feature | API Area | Route/Controller/Service | Auth/Role | Status | Notes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Authentication** | Auth API | `Draft / Needs Discovery` | Public / Token Validation | **Done** | Log masuk, log keluar, validasi sesi token via HTTP-only cookie. |
| **Admin Dashboard** | Analytics API | `Draft / Needs Discovery` | Admin | **Done** | Endpoint data statistik omzet toko dan grafik laba bersih harian. |
| **Inventory Management** | Products API | `Draft / Needs Discovery` | Admin | **Done** | Endpoint CRUD data produk/barang lengkap dengan info HPP. |
| **Staff Management** | Staff API | `Draft / Needs Discovery` | Admin | **Done** | Endpoint pendaftaran kasir/staff baru oleh admin. |
| **Shop Settings** | Settings API | `Draft / Needs Discovery` | Admin | **Done** | Endpoint konfigurasi detail toko dan ambang batas limit stok. |
| **CS POS Terminal** | Transactions API | `Draft / Needs Discovery` | CS (Staff) | **Done** | Endpoint pembuatan transaksi, pemotongan stok atomic, dan pencetakan struk. |
| **CS Inventory Read-only** | Products (CS) API | `Draft / Needs Discovery` | CS (Staff) | **Done** | Endpoint eksplorasi stok produk (HPP disembunyikan/dihilangkan dari response). |
| **CS Transaction History** | Shift/Transactions API| `Draft / Needs Discovery` | CS (Staff) | **Done** | Endpoint riwayat transaksi kasir berdasarkan sesi shift kasir aktif. |
| **CS Profile** | Profile API | `Draft / Needs Discovery` | CS (Staff) | **Done** | Endpoint pembaruan profil kasir mandiri. |

---

## 📌 Catatan Peta API
- Berkas rincian endpoint API detail seperti `API_ENDPOINTS.md` sengaja tidak dibuat pada batch ini.
- Untuk detail file route fisik, fungsi controller, dan service, statusnya ditandai sebagai `Draft / Needs Discovery` sampai audit kode backend secara rinci disetujui.
