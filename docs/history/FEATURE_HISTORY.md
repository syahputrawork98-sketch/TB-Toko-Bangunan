# Riwayat Fitur Global (Feature History Index)

Dokumen ini mencatat indeks riwayat pengembangan fitur (Feature Batch) yang dikerjakan pada sistem **TB-Toko-Bangunan**. 

---

## 📈 Indeks Batch Fitur

| Batch | Judul Fitur | Area | Ringkasan | Status | Tautan Detail |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **F00** | Project Workflow Foundation | Workspace / Repo | Menetapkan fondasi alur kerja, integrasi model AI, pemisahan tugas AI (Room 00, Room 01, Gemini), dan batas-batas keamanan repositori. | **Done** | [Detail](features/F00_PROJECT_WORKFLOW_FOUNDATION.md) |
| **F01** | Documentation Structure | Dokumentasi | Mengadopsi struktur dokumen terstandar untuk membagi antara Control Layer (onboarding/workflow) dan Persistent Memory Layer. | **Done** | [Detail](features/F01_DOCUMENTATION_STRUCTURE.md) |
| **F02** | Frontend Migration | tb-frontend / Repo | Memindahkan Next.js 16 sub-proyek frontend ke repositori terpadu tanpa menyertakan history Git lama, node_modules, `.env`, atau build folder. | **Done** | [Detail](features/F02_FRONTEND_MIGRATION.md) |
| **F03** | Backend Migration | tb-backend / Repo | Memindahkan Express.js & Prisma SQLite sub-proyek backend, menginisiasi database SQLite lokal baru, dan melakukan seeding data awal. | **Done** | [Detail](features/F03_BACKEND_MIGRATION.md) |
| **F04** | Repository Consolidation Audit | Repo / Workflow | Melakukan sinkronisasi identitas berkas, adopsi onboarding, dan audit keamanan terhadap file sensitif/terlarang di Git. | **Done** | [Detail](features/F04_REPOSITORY_CONSOLIDATION_AUDIT.md) |
| **F05-CP** | Onboarding Role Expansion: Roomchat Spesialis | Dokumentasi / Workflow | Menambahkan peran Roomchat Spesialis ke sistem kerja untuk diskusi teknis mendalam sebelum konsolidasi rencana oleh Room 00. | **Done** | [Detail](features/F05_ONBOARDING_ROLE_EXPANSION.md) |
| **F06** | Feature History Foundation & High-Level Feature Maps | Dokumentasi / Arsitektur | Membuat indeks riwayat fitur global dan memetakan komponen UI, endpoint API, dan database secara garis besar (high-level map). | **Done** | [Detail](FEATURE_HISTORY.md) |
| **F07** | Retroactive Feature History Backfill | Dokumentasi / Histori | Melengkapi riwayat kronologis pengerjaan batch yang terlewat (F02, F03, F04, F05-CP) berdasarkan log dokumen status sebelumnya. | **Done** | *File Ini* |

---

## 📌 Catatan Penggunaan
- Setiap penyelesaian batch fitur utama wajib dicatat di berkas ini.
- Untuk detail implementasi tiap batch (terutama F00, F01, dan batch mendatang), buat berkas khusus di dalam folder `docs/history/features/` untuk merekam kronologis perubahan dan keputusan arsitektural yang diambil.
