# High-Level Feature UI Map (Frontend)

Dokumen ini memetakan halaman antarmuka pengguna (UI) tingkat tinggi yang diimplementasikan pada folder `tb-frontend` Next.js.

---

## 🗺️ Peta Fitur Antarmuka (UI Map)

| Feature | Route/Page | Component/Area | Role | Status | Notes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Login** | `/login` | `Draft / Needs Discovery` | Public | **Done** | Halaman masuk menggunakan kredensial akun staff/admin. |
| **Admin Dashboard** | `/admin` | `Draft / Needs Discovery` | Admin | **Done** | Statistik performa toko, ringkasan shift, dan grafik tren laba. |
| **Inventory Management** | `/admin/inventory` | `Draft / Needs Discovery` | Admin | **Done** | Kelola data barang toko, harga jual, dan BPP (HPP) barang. |
| **Staff Management** | `/admin/staff` | `Draft / Needs Discovery` | Admin | **Done** | Pendaftaran dan manajemen data akun staff CS baru. |
| **Shop Settings** | `/admin/settings` | `Draft / Needs Discovery` | Admin | **Done** | Pengaturan profil toko, info alamat struk, dan ambang batas stok tipis. |
| **CS POS Terminal** | `/cs/pos` | `Draft / Needs Discovery` | CS (Staff) | **Done** | Kasir penjualan produk, pencarian SKU, potong stok atomic, dan print struk. |
| **CS Inventory Read-only** | `/cs/inventory` | `Draft / Needs Discovery` | CS (Staff) | **Done** | Eksplorasi produk dan cek stok tipis tanpa menampilkan informasi BPP (HPP). |
| **CS Transaction History** | `/cs/history` | `Draft / Needs Discovery` | CS (Staff) | **Done** | Melihat riwayat transaksi penjualan mandiri pada shift yang sedang berjalan. |
| **CS Profile** | `/cs/settings` | `Draft / Needs Discovery` | CS (Staff) | **Done** | Manajemen data profil dasar mandiri untuk staff CS. |

---

## 📌 Catatan Peta UI
- Berkas pemetaan detail seperti `ROUTING_MAP.md` sengaja tidak dibuat pada batch ini.
- Untuk detail file fisik halaman (`page.tsx`) dan komponen antarmuka, statusnya ditandai sebagai `Draft / Needs Discovery` sampai dilakukan audit kode frontend secara rinci.
