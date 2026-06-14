# High-Level Feature API Map (Backend)

Dokumen ini memetakan area API backend tingkat tinggi yang diimplementasikan pada folder `server/` (sebelumnya `tb-backend` Express.js - legacy).

---

## 🗺️ Peta Fitur API (API Map)

| Feature ID | Feature Name | API Area | Route/Controller/Service | Auth/Role | Status | Notes |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **F01** | Authentication & Role-Based Access | Auth API | `Draft / Needs Discovery` | Public / Token Validation | **Draft / Needs Discovery** | Log masuk, log keluar, validasi sesi token via HTTP-only cookie. |
| **F02** | Admin Dashboard | Analytics API | `Draft / Needs Discovery` | Admin | **Draft / Needs Discovery** | Endpoint data statistik omzet toko dan grafik laba bersih harian. |
| **F03** | Inventory Management | Products API | `Draft / Needs Discovery` | Admin | **Draft / Needs Discovery** | Endpoint CRUD data produk/barang lengkap dengan info HPP. |
| **F04** | Staff Management | Staff API | `Draft / Needs Discovery` | Admin | **Draft / Needs Discovery** | Endpoint pendaftaran kasir/staff baru oleh admin. |
| **F05** | Shop Settings | Settings API | `Draft / Needs Discovery` | Admin | **Draft / Needs Discovery** | Endpoint konfigurasi detail toko dan ambang batas limit stok. |
| **F06** | CS POS Terminal | Transactions API | `Draft / Needs Discovery` | CS (Staff) | **Draft / Needs Discovery** | Endpoint pembuatan transaksi, pemotongan stok atomic, dan pencetakan struk. |
| **F07** | CS Inventory Read-only | Products (CS) API | `Draft / Needs Discovery` | CS (Staff) | **Draft / Needs Discovery** | Endpoint eksplorasi stok produk (HPP disembunyikan/dihilangkan dari response). |
| **F08** | CS Transaction History | Shift/Transactions API| `Draft / Needs Discovery` | CS (Staff) | **Draft / Needs Discovery** | Endpoint riwayat transaksi kasir berdasarkan sesi shift kasir aktif. |
| **F09** | CS Profile | Profile API | `Draft / Needs Discovery` | CS (Staff) | **Draft / Needs Discovery** | Endpoint pembaruan profil kasir mandiri. |

---

## 📌 Catatan Peta API
- Berkas rincian endpoint API detail seperti `API_ENDPOINTS.md` sengaja tidak dibuat pada batch ini.
- Untuk detail file route fisik, fungsi controller, dan service, statusnya ditandai sebagai `Draft / Needs Discovery` sampai audit kode backend secara rinci disetujui.
