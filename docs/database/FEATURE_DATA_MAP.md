# High-Level Feature Data Map (Database)

Dokumen ini memetakan model data/tabel database tingkat tinggi yang digunakan oleh berbagai fitur di `TB-Toko-Bangunan`.

---

## 🗺️ Peta Fitur Data (Data Map)

| Feature | Model/Table | Used By | Status | Notes |
| :--- | :--- | :--- | :--- | :--- |
| **Authentication** | `Draft / Needs Discovery` | Auth, Staff Controller | **Done** | Menyimpan kredensial pengguna (kata sandi ter-hash) dan peran. |
| **Admin Dashboard** | `Draft / Needs Discovery` | Analytics Controller | **Done** | Mengagregasi data transaksi untuk grafik performa keuangan. |
| **Inventory Management** | `Draft / Needs Discovery` | Products Controller | **Done** | Menyimpan data produk, harga beli (HPP), harga jual, dan jumlah stok. |
| **Staff Management** | `Draft / Needs Discovery` | Staff Controller | **Done** | Menyimpan detail profil staff kasir (CS). |
| **Shop Settings** | `Draft / Needs Discovery` | Settings Controller | **Done** | Menyimpan konfigurasi global toko. |
| **CS POS Terminal** | `Draft / Needs Discovery` | Transactions Controller | **Done** | Menyimpan item transaksi, catatan kasir, nominal, dan pemotongan stok. |
| **CS Inventory Read-only** | `Draft / Needs Discovery` | Products Controller (CS) | **Done** | Mengakses daftar produk (stok) tanpa memperlihatkan field harga beli (HPP). |
| **CS Transaction History** | `Draft / Needs Discovery` | Transactions Controller | **Done** | Mengakses data transaksi berdasarkan ID kasir dan status shift kasir. |
| **CS Profile** | `Draft / Needs Discovery` | Profile Controller | **Done** | Mengakses dan mengubah detail profil akun kasir mandiri. |

---

## 📌 Catatan Peta Data
- Berkas detail skema seperti `SCHEMA_MAP.md` dan `RELATION_MAP.md` sengaja tidak dibuat pada batch ini.
- Untuk detail nama model Prisma dan tabel SQLite yang tepat, statusnya ditandai sebagai `Draft / Needs Discovery` sampai audit skema prisma secara detail dijalankan.
