# High-Level Feature Data Map (Database)

Dokumen ini memetakan model data/tabel database tingkat tinggi yang digunakan oleh berbagai fitur di `TB-Toko-Bangunan`.

---

## 🗺️ Peta Fitur Data (Data Map)

| Feature ID | Feature Name | Model/Table | Used By | Status | Notes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **F01** | Authentication & Role-Based Access | `Draft / Needs Discovery` | Auth, Staff Controller | **Draft / Needs Discovery** | Menyimpan kredensial pengguna (kata sandi ter-hash) dan peran. |
| **F02** | Admin Dashboard | `Draft / Needs Discovery` | Analytics Controller | **Draft / Needs Discovery** | Mengagregasi data transaksi untuk grafik performa keuangan. |
| **F03** | Inventory Management | `Draft / Needs Discovery` | Products Controller | **Draft / Needs Discovery** | Menyimpan data produk, harga beli (HPP), harga jual, dan jumlah stok. |
| **F04** | Staff Management | `Draft / Needs Discovery` | Staff Controller | **Draft / Needs Discovery** | Menyimpan detail profil staff kasir (CS). |
| **F05** | Shop Settings | `Draft / Needs Discovery` | Settings Controller | **Draft / Needs Discovery** | Menyimpan konfigurasi global toko. |
| **F06** | CS POS Terminal | `Draft / Needs Discovery` | Transactions Controller | **Draft / Needs Discovery** | Menyimpan item transaksi, catatan kasir, nominal, dan pemotongan stok. |
| **F07** | CS Inventory Read-only | `Draft / Needs Discovery` | Products Controller (CS) | **Draft / Needs Discovery** | Mengakses daftar produk (stok) tanpa memperlihatkan field harga beli (HPP). |
| **F08** | CS Transaction History | `Draft / Needs Discovery` | Transactions Controller | **Draft / Needs Discovery** | Mengakses data transaksi berdasarkan ID kasir dan status shift kasir. |
| **F09** | CS Profile | `Draft / Needs Discovery` | Profile Controller | **Draft / Needs Discovery** | Mengakses dan mengubah detail profil akun kasir mandiri. |

---

## 📌 Catatan Peta Data
- Berkas detail skema seperti `SCHEMA_MAP.md` dan `RELATION_MAP.md` sengaja tidak dibuat pada batch ini.
- Untuk detail nama model Prisma dan tabel SQLite yang tepat, statusnya ditandai sebagai `Draft / Needs Discovery` sampai audit skema prisma secara detail dijalankan.
