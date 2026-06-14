# 🏗️ TB (Toko Bangunan) - Consolidated Repository

Selamat datang di repositori utama dan final **TB-Toko-Bangunan**. Repositori tunggal ini menggabungkan seluruh komponen sistem aplikasi Manajemen Toko Bangunan (TB) yang sebelumnya terpisah pada dua repositori mandiri. Setelah migrasi ini selesai, repositori lama (`tb-frontend` dan `tb-backend` di GitHub) berstatus **legacy** (sumber lama) dan tidak lagi menjadi sumber utama pengembangan.

---

## 📁 Struktur Repositori Terkonsolidasi

Seluruh kode sumber dan dokumentasi diatur dalam folder berikut:
* **`tb-frontend/`**: Kode aplikasi antarmuka web (Next.js 16) yang menyajikan dashboard Admin dan POS CS.
* **`tb-backend/`**: Kode mesin server (Express.js & Prisma ORM) yang mengelola logika bisnis, autentikasi, dan database.
* **`docs/`**: Seluruh dokumentasi teknis sistem terpusat (mengadopsi pola dokumentasi terstruktur dari referensi `WK-Workflow-Kit`).
* **`README.md`**: Panduan navigasi utama ini.
* **`.gitignore`**: Aturan pengabaian Git root terpusat untuk mengamankan data konfigurasi lokal.

---

## 📑 Navigasi Dokumentasi

Seluruh panduan teknis dan operasional sistem telah didokumentasikan secara rinci menggunakan pola dokumentasi terstruktur dari `WK-Workflow-Kit`:

1.  **Project Overview**: Silakan baca [PROJECT_OVERVIEW.md](docs/project/PROJECT_OVERVIEW.md) untuk memahami modul Admin Dashboard, Customer Service (CS) Terminal, dan alur bisnis inti.
2.  **Rencana Migrasi**: Detail langkah-langkah konsolidasi repositori dicatat pada [MIGRATION_PLAN.md](docs/project/MIGRATION_PLAN.md).
3.  **Frontend Tech Stack**: Lihat [FRONTEND_OVERVIEW.md](docs/frontend/FRONTEND_OVERVIEW.md) untuk detail arsitektur Next.js, Zustand, dan Vanilla CSS Modules.
4.  **Backend Logic & API**: Baca [BACKEND_OVERVIEW.md](docs/backend/BACKEND_OVERVIEW.md) untuk rute API, proteksi rute JWT, dan service layer.
5.  **Database & Schema**: Skema relasi tabel dan snapshot BPP (HPP) dijelaskan di [DATABASE_OVERVIEW.md](docs/database/DATABASE_OVERVIEW.md).
6.  **Local Setup Guide**: Ikuti panduan instalasi dan instruksi running di [LOCAL_SETUP.md](docs/development/LOCAL_SETUP.md).
7.  **Current Status**: Status fitur dan riwayat rilis modul saat ini tercatat di [CURRENT_STATUS.md](docs/history/CURRENT_STATUS.md).

---

## 🚀 Memulai Cepat (Quick Start)

Untuk menjalankan proyek secara lokal, pastikan Anda telah mengonfigurasi variabel lingkungan `.env` di masing-masing sub-folder (`tb-frontend` dan `tb-backend`) sesuai dengan berkas `.env.example` yang tersedia.

Info selengkapnya mengenai instalasi dependensi, sinkronisasi database Prisma, dan proses menjalankan server dapat dibaca pada [LOCAL_SETUP.md](docs/development/LOCAL_SETUP.md).

---
*Authorized by Antigravity AI Architect. v1.0.0*