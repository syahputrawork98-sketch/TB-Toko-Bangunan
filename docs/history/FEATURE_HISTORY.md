# Riwayat Fitur Global (Feature History Index)

Dokumen ini mencatat indeks riwayat pengembangan fitur (Feature Batch) yang dikerjakan pada sistem **TB-Toko-Bangunan**. 

---

## 📈 Indeks Batch Fitur

| Batch | Judul Fitur | Area | Ringkasan | Status | Tautan Detail |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **F00** | Project Workflow Foundation | Workspace / Repo | Menetapkan fondasi alur kerja, integrasi model AI, pemisahan tugas AI (Room 00, Room 01, Gemini), dan batas-batas keamanan repositori. | **Done** | [Detail](features/F00_PROJECT_WORKFLOW_FOUNDATION.md) |
| **F01** | Documentation Structure | Dokumentasi | Mengadopsi struktur dokumen terstandar untuk membagi antara Control Layer (onboarding/workflow) dan Persistent Memory Layer. | **Done** | [Detail](features/F01_DOCUMENTATION_STRUCTURE.md) |
| **F05-CP** | Onboarding Role Expansion: Roomchat Spesialis | Dokumentasi / Workflow | Menambahkan peran Roomchat Spesialis ke sistem kerja untuk diskusi teknis mendalam sebelum konsolidasi oleh Room 00. | **Done** | [Detail](../project/onboarding/ROOM_SPECIALIST_PROMPT.md) |
| **F06** | Feature History Foundation & High-Level Feature Maps | Dokumentasi / Arsitektur | Membuat indeks riwayat fitur dan memetakan komponen UI, endpoint API, dan database secara garis besar (high-level map). | **Done** | *File Ini* |

---

## 📌 Catatan Penggunaan
- Setiap penyelesaian batch fitur utama wajib dicatat di berkas ini.
- Untuk detail implementasi tiap batch (terutama F00, F01, dan batch mendatang), buat berkas khusus di dalam folder `docs/history/features/` untuk merekam kronologis perubahan dan keputusan arsitektural yang diambil.
