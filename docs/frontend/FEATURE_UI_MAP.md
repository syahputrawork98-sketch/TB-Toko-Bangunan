# High-Level Feature UI Map (Frontend)

Dokumen ini memetakan halaman antarmuka pengguna (UI) tingkat tinggi yang diimplementasikan pada folder `client/` (sebelumnya `tb-frontend` Next.js - legacy).

---

## 🗺️ Peta Fitur Antarmuka (UI Map)

| Feature ID | Feature Name | Route/Page | Component/Area | Role | Status | Notes |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **F01** | Authentication & Role-Based Access | `/login` | `Draft / Needs Discovery` | Public / CS / Admin | **Draft / Needs Discovery** | Halaman masuk menggunakan kredensial akun staff/admin. |
| **F02** | Admin Dashboard | `/admin` | `Draft / Needs Discovery` | Admin | **Draft / Needs Discovery** | Statistik performa toko, ringkasan shift, dan grafik tren laba. |
| **F03** | Inventory Management | `/admin/inventory` | `Draft / Needs Discovery` | Admin | **Draft / Needs Discovery** | Kelola data barang toko, harga jual, dan BPP (HPP) barang. |
| **F04** | Staff Management | `/admin/staff` | `Draft / Needs Discovery` | Admin | **Draft / Needs Discovery** | Pendaftaran dan manajemen data akun staff CS baru. |
| **F05** | Shop Settings | `/admin/settings` | `Draft / Needs Discovery` | Admin | **Draft / Needs Discovery** | Pengaturan profil toko, info alamat struk, dan ambang batas stok tipis. |
| **F06** | CS POS Terminal | `/cs/pos` | `Draft / Needs Discovery` | CS (Staff) | **Draft / Needs Discovery** | Kasir penjualan produk, pencarian SKU, potong stok atomic, dan print struk. |
| **F07** | CS Inventory Read-only | `/cs/inventory` | `Draft / Needs Discovery` | CS (Staff) | **Draft / Needs Discovery** | Eksplorasi produk dan cek stok tipis tanpa menampilkan informasi BPP (HPP). |
| **F08** | CS Transaction History | `/cs/history` | `Draft / Needs Discovery` | CS (Staff) | **Draft / Needs Discovery** | Melihat riwayat transaksi penjualan mandiri pada shift yang sedang berjalan. |
| **F09** | CS Profile | `/cs/settings` | `Draft / Needs Discovery` | CS (Staff) | **Draft / Needs Discovery** | Manajemen data profil dasar mandiri untuk staff CS. |

---

## 📌 Catatan Peta UI
- Berkas pemetaan detail seperti `ROUTING_MAP.md` sengaja tidak dibuat pada batch ini.
- Untuk detail file fisik halaman (`page.tsx`) dan komponen antarmuka, statusnya ditandai sebagai `Draft / Needs Discovery` sampai dilakukan audit kode frontend secara rinci.
