# Riwayat Checkpoint Proyek (Project Checkpoint History Index)

Dokumen ini mencatat tahapan pengerjaan infrastruktur proyek (**Project Checkpoints / PXX**), seperti setup alur kerja, struktur folder, migrasi repositori, standardisasi tata nama, dan audit repositori pada sistem **TB-Toko-Bangunan**.

Berbeda dengan **Feature History (FXX)** yang merepresentasikan fitur fungsional aplikasi nyata, checkpoint proyek ini fokus pada pengelolaan dan kesehatan struktur kode repositori.

---

## 📈 Indeks Checkpoint Proyek

| Checkpoint | Judul Checkpoint | Area | Ringkasan | Status | Tautan Detail |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **P00** | Project Workflow Foundation | Workspace / Repo | Menetapkan fondasi alur kerja, integrasi model AI, pemisahan tugas AI (Room 00, Room 01, Gemini), dan batas-batas keamanan repositori. | **Done** | [Detail](project/P00_PROJECT_WORKFLOW_FOUNDATION.md) |
| **P01** | Documentation Structure | Dokumentasi | Mengadopsi struktur dokumen terstandar untuk membagi antara Control Layer (onboarding/workflow) dan Persistent Memory Layer. | **Done** | [Detail](project/P01_DOCUMENTATION_STRUCTURE.md) |
| **P02** | Frontend Migration | client / Repo | Memindahkan Next.js 16 sub-proyek frontend ke repositori terpadu tanpa menyertakan history Git lama, node_modules, `.env`, atau build folder. | **Done** | [Detail](project/P02_FRONTEND_MIGRATION.md) |
| **P03** | Backend Migration | server / Repo | Memindahkan Express.js & Prisma SQLite sub-proyek backend, menginisiasi database SQLite lokal baru, dan melakukan seeding data awal. | **Done** | [Detail](project/P03_BACKEND_MIGRATION.md) |
| **P04** | Repository Consolidation Audit | Repo / Workflow | Melakukan sinkronisasi identitas berkas, adopsi onboarding, dan audit keamanan terhadap file sensitif/terlarang di Git. | **Done** | [Detail](project/P04_REPOSITORY_CONSOLIDATION_AUDIT.md) |
| **P05** | Onboarding Role Expansion: Roomchat Spesialis | Dokumentasi / Workflow | Menambahkan peran Roomchat Spesialis ke sistem kerja untuk diskusi teknis mendalam sebelum konsolidasi rencana oleh Room 00. | **Done** | [Detail](project/P05_ONBOARDING_ROLE_EXPANSION.md) |
| **P08** | Monorepo Folder Naming Standardization | Repo / Dokumentasi | Standardisasi tata nama folder monorepo dari `tb-frontend` / `tb-backend` menjadi `client` / `server` serta sinkronisasi seluruh path dokumentasi. | **Done** | [Detail](project/P08_MONOREPO_FOLDER_NAMING_STANDARDIZATION.md) |

---

## 📌 Catatan Penggunaan
- Setiap kali terdapat pengerjaan non-fitur aplikasi (seperti upgrade konfigurasi monorepo, setup Docker, audit keamanan repo, atau pembuatan deployment scripts), pengerjaan tersebut harus dicatat di berkas ini menggunakan kode `PXX`.
- Untuk detail setiap checkpoint, buat berkas khusus di dalam folder `docs/history/project/` untuk merekam detail kronologis teknis.
