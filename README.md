# 🏗️ TB (Toko Bangunan) - Consolidated Repository

Selamat datang di repositori utama dan final untuk **Aplikasi Manajemen Toko Bangunan (TB)**. Repositori ini menggabungkan frontend (Next.js) dan backend (Express.js + Prisma) ke dalam satu struktur folder terpusat untuk mempermudah pemeliharaan, pengembangan, dan penerapan (deployment).

---

## 📁 Struktur Repositori

```text
TB-Toko-Bangunan/
├── README.md            # Dokumentasi utama ini
├── .gitignore           # Aturan abaikan git root terpusat
├── docs/                # Seluruh dokumentasi teknis & proses
│   ├── project/         # Konseptual & Rencana Migrasi
│   ├── frontend/        # Arsitektur Frontend (Next.js)
│   ├── backend/         # Arsitektur Backend (Express)
│   ├── database/        # Skema Relasi Database (Prisma)
│   ├── development/     # Panduan Pengaturan Lokal
│   └── history/         # Riwayat Status Fitur
├── tb-frontend/         # Folder Aplikasi Frontend (Next.js 16)
└── tb-backend/          # Folder Engine Backend (Express + SQLite/Prisma)
```

---

## 📑 Navigasi Dokumentasi

Seluruh panduan teknis dan operasional sistem telah didokumentasikan secara rinci menggunakan pola dokumentasi terstruktur dari `WK-Workflow-Kit`:

1.  **Project Overview**: Silakan baca [PROJECT_OVERVIEW.md](file:///docs/project/PROJECT_OVERVIEW.md) untuk memahami modul Admin Dashboard, Customer Service (CS) Terminal, dan alur bisnis inti.
2.  **Rencana Migrasi**: Detail langkah-langkah konsolidasi repositori dicatat pada [MIGRATION_PLAN.md](file:///docs/project/MIGRATION_PLAN.md).
3.  **Frontend Tech Stack**: Lihat [FRONTEND_OVERVIEW.md](file:///docs/frontend/FRONTEND_OVERVIEW.md) untuk detail arsitektur Next.js, Zustand, dan Vanilla CSS Modules.
4.  **Backend Logic & API**: Baca [BACKEND_OVERVIEW.md](file:///docs/backend/BACKEND_OVERVIEW.md) untuk rute API, proteksi rute JWT, dan service layer.
5.  **Database & Schema**: Skema relasi tabel dan snapshot BPP (HPP) dijelaskan di [DATABASE_OVERVIEW.md](file:///docs/database/DATABASE_OVERVIEW.md).
6.  **Local Setup Guide**: Ikuti panduan instalasi dan instruksi running di [LOCAL_SETUP.md](file:///docs/development/LOCAL_SETUP.md).
7.  **Current Status**: Status fitur dan riwayat rilis modul saat ini tercatat di [CURRENT_STATUS.md](file:///docs/history/CURRENT_STATUS.md).

---

## 🚀 Memulai Cepat (Quick Start)

Untuk menjalankan proyek secara lokal, pastikan Anda telah mengonfigurasi variabel lingkungan `.env` di masing-masing sub-folder (`tb-frontend` dan `tb-backend`) sesuai dengan berkas `.env.example` yang tersedia.

Info selengkapnya mengenai instalasi dependensi, sinkronisasi database Prisma, dan proses menjalankan server dapat dibaca pada [LOCAL_SETUP.md](file:///docs/development/LOCAL_SETUP.md).

---
*Authorized by Antigravity AI Architect. v1.0.0*