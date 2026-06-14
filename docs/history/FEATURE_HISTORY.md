# Riwayat Fitur Aplikasi (Application Feature History Index)

Dokumen ini mencatat indeks riwayat pengembangan fitur fungsional aplikasi/web (**Application Features / FXX**) yang dikerjakan pada sistem **TB-Toko-Bangunan**. 

Seluruh rincian teknis mendalam mengenai antarmuka, endpoint API, dan struktur database di setiap fitur berstatus **Draft / Needs Discovery** sampai dilakukan audit kode fungsional secara terperinci.

---

## 📈 Indeks Fitur Aplikasi

| Batch | Judul Fitur | Area | User Role | Ringkasan | Status | Tautan Detail |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **F00** | Existing Project Zero Point | Global / Base | Global | Titik baseline pencatatan fungsional sistem pasca-migrasi dan konsolidasi monorepo target. | **Baseline** | [Detail](features/F00_EXISTING_PROJECT_ZERO_POINT.md) |
| **F01** | Authentication & Role-Based Access | Security / Auth | Admin & CS | Autentikasi pengguna berbasis JWT cookie HTTP-only dengan pembagian akses rute Admin vs CS. | **Partial** | [Detail](features/F01_AUTHENTICATION_ROLE_BASED_ACCESS.md) |
| **F02** | Admin Dashboard | Client / Server | Admin | Dasbor visual statistik penjualan, ringkasan kas, dan grafik tren laba kotor. | **Implemented** | [Detail](features/F02_ADMIN_DASHBOARD.md) |
| **F03** | Inventory Management | Client / Server | Admin | Pengelolaan data inventaris barang (CRUD), penyesuaian stok, serta pembedaan harga beli (HPP) vs harga jual. | **Draft** | [Detail](features/F03_INVENTORY_MANAGEMENT.md) |
| **F04** | Staff Management | Client / Server | Admin | Pendaftaran akun kasir/CS baru serta pengaturan status keaktifan akun staff. | **Draft** | [Detail](features/F04_STAFF_MANAGEMENT.md) |
| **F05** | Shop Settings | Client / Server | Admin | Pengaturan profil fisik toko (nama, alamat, telepon struk) dan batas minimum stok tipis global. | **Draft** | [Detail](features/F05_SHOP_SETTINGS.md) |
| **F06** | CS POS Terminal | Client / Server | CS (Staff) | Terminal kasir transaksi penjualan, pencarian SKU produk cepat, keranjang belanja, kalkulasi, dan cetak struk. | **Draft** | [Detail](features/F06_CS_POS_TERMINAL.md) |
| **F07** | CS Inventory Read-only | Client / Server | CS (Staff) | Modul pencarian stok dan ketersediaan barang untuk staff kasir tanpa memperlihatkan field harga pokok (HPP). | **Draft** | [Detail](features/F07_CS_INVENTORY_READ_ONLY.md) |
| **F08** | CS Transaction History | Client / Server | CS (Staff) | Modul riwayat transaksi penjualan mandiri milik kasir aktif pada shift berjalan serta fitur cetak ulang struk. | **Draft** | [Detail](features/F08_CS_TRANSACTION_HISTORY.md) |
| **F09** | CS Profile | Client / Server | CS (Staff) | Halaman pengaturan profil data pribadi dasar dan pembaruan password untuk akun CS yang sedang masuk. | **Draft** | [Detail](features/F09_CS_PROFILE.md) |

---

## 📌 Catatan Penggunaan
- Setiap penyelesaian fitur fungsional aplikasi baru wajib dicatat di berkas ini.
- Untuk detail implementasi tiap fitur, buat berkas khusus di dalam folder `docs/history/features/` untuk merekam rincian antarmuka, API area, dan data area terkait.
