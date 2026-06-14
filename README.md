# 🏗️ TB (Toko Bangunan) - Consolidated Repository

Selamat datang di repositori utama dan final **TB-Toko-Bangunan**. Repositori tunggal ini menggabungkan seluruh komponen sistem aplikasi Manajemen Toko Bangunan (TB) yang sebelumnya terpisah pada dua repositori mandiri. Setelah migrasi ini selesai, repositori lama (`tb-frontend` dan `tb-backend` di GitHub) berstatus **legacy** (sumber lama) dan tidak lagi menjadi sumber utama pengembangan.

---

## 📁 Struktur Repositori Terkonsolidasi

Seluruh kode sumber dan dokumentasi diatur dalam folder berikut:
* **`client/`** (sebelumnya `tb-frontend/` - legacy): Kode aplikasi antarmuka web (Next.js 16) yang menyajikan dashboard Admin dan POS CS.
* **`server/`** (sebelumnya `tb-backend/` - legacy): Kode mesin server (Express.js & Prisma ORM) yang mengelola logika bisnis, autentikasi, dan database.
* **`docs/`**: Seluruh dokumentasi teknis sistem terpusat (mengadopsi pola dokumentasi terstruktur dari referensi `WK-Workflow-Kit`).
* **`README.md`**: Panduan navigasi utama ini.
* **`.gitignore`**: Aturan pengabaian Git root terpusat untuk mengamankan data konfigurasi lokal.

---

## 📑 Navigasi Dokumentasi

Seluruh panduan teknis, alur kerja, dan operasional sistem telah didokumentasikan secara rinci:

1.  **Project Overview**: Silakan baca [PROJECT_OVERVIEW.md](docs/project/PROJECT_OVERVIEW.md) untuk memahami modul Admin Dashboard, Customer Service (CS) Terminal, dan alur bisnis inti.
2.  **Rencana Migrasi**: Detail langkah-langkah konsolidasi repositori dicatat pada [MIGRATION_PLAN.md](docs/project/MIGRATION_PLAN.md).
3.  **Instruksi Onboarding AI**: Gunakan [CHATGPT_PROJECT_INSTRUCTIONS.md](docs/project/onboarding/CHATGPT_PROJECT_INSTRUCTIONS.md) untuk inisiasi sesi chat asisten AI baru.
4.  **Prompt Roomchat Spesialis**: Gunakan [ROOM_SPECIALIST_PROMPT.md](docs/project/onboarding/ROOM_SPECIALIST_PROMPT.md) untuk menginisiasi sesi diskusi teknis terfokus dengan AI Spesialis.
5.  **Sistem Kerja Proyek**: Aturan pengerjaan batch dan batas keamanan diatur dalam [WORKING_SYSTEM.md](docs/project/workflow/WORKING_SYSTEM.md).
6.  **Frontend Tech Stack**: Lihat [FRONTEND_OVERVIEW.md](docs/frontend/FRONTEND_OVERVIEW.md) untuk detail arsitektur Next.js, Zustand, dan Vanilla CSS Modules.
7.  **Peta Fitur Frontend (UI Map)**: Lihat [FEATURE_UI_MAP.md](docs/frontend/FEATURE_UI_MAP.md) untuk pemetaan halaman dan antarmuka pengguna tingkat tinggi.
8.  **Backend Logic & API**: Baca [BACKEND_OVERVIEW.md](docs/backend/BACKEND_OVERVIEW.md) untuk rute API, proteksi rute JWT, dan service layer.
9.  **Peta Fitur API Backend (API Map)**: Lihat [FEATURE_API_MAP.md](docs/backend/FEATURE_API_MAP.md) untuk pemetaan area dan rute API backend tingkat tinggi.
10. **Database & Schema**: Skema relasi tabel dan snapshot BPP (HPP) dijelaskan di [DATABASE_OVERVIEW.md](docs/database/DATABASE_OVERVIEW.md).
11. **Peta Fitur Data Database (Data Map)**: Lihat [FEATURE_DATA_MAP.md](docs/database/FEATURE_DATA_MAP.md) untuk pemetaan model data dan tabel tingkat tinggi.
12. **Local Setup Guide**: Ikuti panduan instalasi dan instruksi running di [LOCAL_SETUP.md](docs/development/LOCAL_SETUP.md).
13. **Current Status**: Status fitur dan riwayat rilis modul saat ini tercatat di [CURRENT_STATUS.md](docs/history/CURRENT_STATUS.md).
14. **Riwayat Fitur Aplikasi (Feature History)**: Lihat indeks batch riwayat fitur lengkap di [FEATURE_HISTORY.md](docs/history/FEATURE_HISTORY.md).

---

## 🚀 Memulai Cepat (Quick Start)

Untuk menjalankan proyek secara lokal, pastikan Anda telah mengonfigurasi variabel lingkungan `.env` di masing-masing sub-folder (`client` dan `server`) sesuai dengan berkas `.env.example` yang tersedia.

Info selengkapnya mengenai instalasi dependensi, sinkronisasi database Prisma, dan proses menjalankan server dapat dibaca pada [LOCAL_SETUP.md](docs/development/LOCAL_SETUP.md).

---
*Authorized by Antigravity AI Architect. v1.0.0*