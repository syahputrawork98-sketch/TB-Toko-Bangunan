# Status Proyek Saat Ini (Current Status)

## Project Snapshot
- **Project Name**: TB (Toko Bangunan) Industrial Management System
- **Current Mode**: Consolidation / Repository Unification
- **Primary Workspace**: Anti-Gravity IDE
- **Target Repository**: `TB-Toko-Bangunan`
- **Active Directory Structure**:
  - `client/` (Frontend - Next.js 16)
  - `server/` (Backend - Express & Prisma SQLite)
  - `docs/` (Dokumentasi Terpadu)
- **Legacy Directory Names**: `tb-frontend/`, `tb-backend/` (sebelum standardisasi F08)

## 📁 Status Konsolidasi Repositori (Consolidation Status)
- **Repository consolidation**: completed
- **Frontend migration**: completed
- **Backend migration**: completed
- **Onboarding/workflow adoption**: completed
- **Final repository audit**: completed
- **Integration test**: pending
- **Legacy repo cleanup**: ready for archive/delete decision

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
| Repo | Konsolidasi Repositori Tunggal | **Completed** | Penyatuan legacy `tb-frontend` & legacy `tb-backend` ke `TB-Toko-Bangunan` (sekarang di-rename menjadi `client/` dan `server/`). |
| Repo | Pengujian Integrasi Lokal | **Pending** | Pengujian sambungan frontend-backend pasca-migrasi belum dijalankan. |

---

## 🛠️ Riwayat Aktivitas Terakhir (Last Checkpoint)
- **Fase 2 - Migrasi Frontend (legacy `tb-frontend`)**: Folder kode frontend berhasil dipindahkan tanpa membawa folder `.git` lama, dependencies, atau file `.env` rahasia. Build turbopack Next.js terverifikasi sukses.
- **Fase 3 - Migrasi Backend (legacy `tb-backend`)**: Folder kode backend Express & Prisma berhasil dipindahkan. Inisialisasi database SQLite lokal bersih dan seeding berhasil. Uji dev server berjalan lancar pada port `5000`.
- **Fase 4A - Sinkronisasi Identitas**: Semua dokumen dibersihkan dari nama/path lama yang membingungkan. Menambahkan checklist kesiapan sebelum repo lama boleh dihapus/diarsipkan.
- **Fase 4B - Adopsi Onboarding & Workflow**: Berkas-berkas alur kerja (`WORKING_SYSTEM.md`, `EXISTING_MODE.md`, `PROJECT_STARTER_CHECKLIST.md`) dan instruksi onboarding ChatGPT (`CHATGPT_PROJECT_INSTRUCTIONS.md`, Roomprompts) berhasil diadopsi dan disesuaikan.
- **Fase 4C - Audit Akhir Repositori**: Struktur target, kelengkapan berkas teknis, dan isolasi Git terhadap file sensitif/terlarang (`.env`, `dev.db`, `node_modules`, build folder) telah divalidasi 100% aman dan bersih.
- **Aturan Keamanan Tambahan**: Repositori lama (legacy `tb-frontend` dan legacy `tb-backend` mandiri) kini sudah dinyatakan **aman untuk diarsipkan/dihapus** oleh User setelah seluruh berkas terbukti berjalan stabil di repositori terpadu `TB-Toko-Bangunan`.
- **Fase 5 - Perluasan Peran Onboarding (Roomchat Spesialis)**: Menambahkan peran Roomchat Spesialis sebagai AI diskusi teknis terfokus sebelum pembuatan batch resmi oleh Roomchat 00. Membuat panduan prompt `ROOM_SPECIALIST_PROMPT.md` dan memperbarui `WORKING_SYSTEM.md` serta `CHATGPT_PROJECT_INSTRUCTIONS.md` untuk mencerminkan alur kerja baru. Status pengujian integrasi tetap dipertahankan *Pending*.
- **Fase 6 - Fondasi Riwayat Fitur & High-Level Feature Maps**: Membuat indeks global riwayat fitur `FEATURE_HISTORY.md` beserta log detail `F00_PROJECT_WORKFLOW_FOUNDATION.md` dan `F01_DOCUMENTATION_STRUCTURE.md`. Menyediakan template peta fitur tingkat tinggi `FEATURE_UI_MAP.md` (Frontend), `FEATURE_API_MAP.md` (Backend), dan `FEATURE_DATA_MAP.md` (Database) dengan penanda `Draft / Needs Discovery` untuk elemen-elemen detail yang belum diaudit. Status pengujian integrasi tetap dipertahankan *Pending*.
- **Fase 7 - Backfill Riwayat Fitur Retroaktif**: Melengkapi dokumen riwayat terperinci untuk pengerjaan batch masa lalu (`F02_FRONTEND_MIGRATION.md`, `F03_BACKEND_MIGRATION.md`, `F04_REPOSITORY_CONSOLIDATION_AUDIT.md`, `F05_ONBOARDING_ROLE_EXPANSION.md`) di bawah subfolder `docs/history/features/` berdasarkan data status berjalan sebelumnya. Melakukan pembaruan indeks tabel `FEATURE_HISTORY.md` agar berurutan secara rapi. Status pengujian integrasi lokal tetap dipertahankan *Pending*.
- **Fase 8 - Standarisasi Nama Folder Monorepo (client & server)**: Melakukan rename folder dari `tb-frontend` menjadi `client` dan `tb-backend` menjadi `server` agar sesuai standar penamaan monorepo profesional. Melakukan pembaruan terhadap seluruh berkas konfigurasi, instruksi lokal, dan dokumen onboarding di bawah `docs/` untuk menyelaraskan ke nama folder aktif yang baru, serta melabeli folder lama sebagai legacy (legacy `tb-frontend` dan legacy `tb-backend`). Status pengujian integrasi lokal tetap dipertahankan *Pending*.
- **Fase 9 - Penyederhanaan Sistem Riwayat ke APP/FXX**: Melakukan koreksi sistem pencatatan riwayat di mana pelacakan riwayat pengembangan disederhanakan kembali hanya menggunakan format fitur aplikasi (`APP`/`FXX`) terpadu. Seluruh riwayat proyek terkait migrasi dan standardisasi disatukan ke dalam sistem ini. Membuat detail berkas baru `F00` hingga `F09` di `docs/history/features/` dengan status `Draft / Needs Discovery` (kecuali `F00` sebagai baseline) dan menyinkronkan pemetaan fitur frontend/backend/database. Status pengujian integrasi lokal tetap dipertahankan *Pending*.
- **Fase 10 - Simplifikasi Riwayat Sistem ke APP/FXX saja**: Menghapus klasifikasi `PXX` / Project Checkpoint dan indeks `PROJECT_CHECKPOINT_HISTORY.md` dari repositori sesuai keputusan Owner. Seluruh pelacakan riwayat dikembalikan sepenuhnya ke format fitur aplikasi (`FXX`) terpadu untuk menyederhanakan alur dokumentasi. Status pengujian integrasi lokal tetap dipertahankan *Pending*.
- **Tahap 1 - Pengisian Detail Riwayat Fitur (F00 & F01)**: Mengisi ulang detail dokumentasi teknis mendalam untuk fitur dasar `F00_EXISTING_PROJECT_ZERO_POINT.md` dengan status `Existing / Baseline` dan `F01_AUTHENTICATION_ROLE_BASED_ACCESS.md` dengan status `Existing / Partial`. Dokumentasi disusun berdasarkan audit kode riil di folder `client/` dan `server/` tanpa mengubah kode fungsional maupun skema database. Status pengujian integrasi lokal tetap dipertahankan *Pending*.
- **Pengisian Detail Riwayat Fitur (F02)**: Mengisi detail dokumentasi teknis fungsional untuk `F02_ADMIN_DASHBOARD.md` dengan status `Existing / Implemented` berdasarkan data audit terverifikasi dari Roomchat 01. Dokumentasi merangkum visualisasi analitik bisnis, visualisasi bagan grafik manual, endpoint `/api/analytics`, model Prisma terkait, serta batasan peran login. Status pengujian integrasi lokal tetap dipertahankan *Pending*.
- **Pengisian Detail Riwayat Fitur (F03)**: Mengisi detail dokumentasi teknis fungsional untuk `F03_INVENTORY_MANAGEMENT.md` dengan status `Existing / Implemented` berdasarkan data audit terverifikasi dari Roomchat 01. Dokumentasi merangkum rute utama `/admin/inventory`, antarmuka CRUD barang material, field data produk (termasuk harga jual dan HPP/cost price), low stock indicator lokal (threshold 10), endpoint `/api/products` backend, skema tabel SQLite, serta integrasi batasan hak otorisasi role ADMIN. Status pengujian integrasi lokal tetap dipertahankan *Pending*.
- **Pengisian Detail Riwayat Fitur (F04)**: Mengisi detail dokumentasi teknis fungsional untuk `F04_STAFF_MANAGEMENT.md` dengan status `Existing / Implemented` berdasarkan data audit terverifikasi dari Roomchat 01. Dokumentasi merangkum rute utama `/admin/staff`, manajemen akun user (username, password hash, role), modal create user (ADMIN/CS), endpoint `/api/users` backend, relasi model database `User` dengan `Transaction` (cashierId), serta proteksi rute di client-side middleware. Status pengujian integrasi lokal tetap dipertahankan *Pending*.

---

## 🛡️ Aturan Keamanan Repository
- Jangan men-commit berkas `.env` atau `.env.local` asli ke repositori Git.
- Jangan menyertakan folder `.git` lama dari legacy `tb-frontend` atau legacy `tb-backend` saat menyalin kode.
- Database SQLite lokal `dev.db` harus diabaikan dan dibuat secara dinamis menggunakan script seeder.
