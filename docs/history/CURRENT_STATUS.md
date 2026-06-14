# Status Proyek Saat Ini (Current Status)

## Project Snapshot
- **Project Name**: TB (Toko Bangunan) Industrial Management System
- **Current Mode**: Consolidation / Repository Unification
- **Primary Workspace**: Anti-Gravity IDE
- **Target Repository**: `TB-Toko-Bangunan`

---

## 📈 Perkembangan Fitur (Feature Milestones)

| Peran / Area | Nama Fitur | Status | Keterangan |
| :--- | :--- | :--- | :--- |
| **Global** | Multi-Role Authentication (Admin & CS) | **Completed** | Proteksi rute berbasis JWT cookie terverifikasi stabil. |
| **Admin** | Dashboard Analitik & Tren Penjualan | **Completed** | Grafik tren 7 hari & akumulasi laba bersih (dari snapshot HPP). |
| **Admin** | Inventory CRUD (BPP vs Harga Jual) | **Completed** | Manajemen inventaris lengkap dengan menyembunyikan HPP dari CS. |
| **Admin** | Staff Account Management | **Completed** | Registrasi akun staff/kasir baru oleh admin. |
| **Admin** | Global Shop Configurations | **Completed** | Pengaturan nama toko, alamat, telepon struk, dan ambang batas stok. |
| **CS** | Point of Sale (POS) Terminal | **Completed** | Pencarian SKU kilat, kalkulasi otomatis, dan potong stok atomic. |
| **CS** | Inventory Explorer (Read-only) | **Completed** | CS dapat mengecek ketersediaan stok tanpa bisa melihat HPP barang. |
| **CS** | Personal Shift History | **Completed** | Kasir memantau riwayat transaksi shift sendiri & cetak ulang struk. |
| **Repo** | Konsolidasi Repositori Tunggal | **In Progress** | Penyatuan `tb-frontend` & `tb-backend` ke `TB-Toko-Bangunan`. |

---

## 🛠️ Riwayat Aktivitas Terakhir (Last Checkpoint)
- **Fase 1 - Dokumentasi Awal**: Diinisialisasi di dalam repositori target (`TB-Toko-Bangunan/docs/`). 
- **Kebersihan File**: Menyiapkan `.gitignore` root untuk mencegah kebocoran `.env`, database lokal SQLite (`dev.db`), serta folder dependencies/build.

---

## 🛡️ Aturan Keamanan Repository
- Jangan men-commit berkas `.env` atau `.env.local` asli ke repositori Git.
- Jangan menyertakan folder `.git` lama dari `tb-frontend` atau `tb-backend` saat menyalin kode.
- Database SQLite lokal `dev.db` harus diabaikan dan dibuat secara dinamis menggunakan script seeder.
