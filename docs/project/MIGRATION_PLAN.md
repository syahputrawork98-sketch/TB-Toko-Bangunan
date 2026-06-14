# Rencana Migrasi & Konsolidasi Repositori (Migration Plan)

Dokumen ini mencatat rencana strategis penyatuan repositori `tb-frontend` dan `tb-backend` ke dalam satu repositori utama `TB-Toko-Bangunan`.

---

## 🎯 Tujuan Proyek
Mempermudah manajemen repositori di GitHub dengan menyatukan frontend dan backend ke dalam struktur sub-folder pada satu repositori tunggal tanpa mengganggu jalannya aplikasi yang sudah stabil.

---

## 🧼 Aturan Kebersihan Git & Eksklusi File
Untuk memastikan proses migrasi berjalan aman tanpa membocorkan kredensial lokal dan menjaga repositori tetap bersih:
- **Eksklusi `.git`**: Folder `.git` dari folder lama (`tb-frontend` dan `tb-backend`) tidak boleh ikut disalin ke repositori baru. Git history akan menggunakan repositori baru `TB-Toko-Bangunan`.
- **Eksklusi `.env*`**: File `.env` (backend) dan `.env.local` (frontend) tidak boleh dimasukkan ke Git. Versi contoh (`.env.example`) disediakan untuk setup lokal baru.
- **Eksklusi `dev.db`**: File database SQLite (`prisma/dev.db`) tidak boleh di-commit.
- **Eksklusi Build & Dependencies**: Folder `node_modules`, `.next`, `dist`, dan `build` diabaikan sepenuhnya.

---

## 🏗️ Struktur Target Folder

```text
TB-Toko-Bangunan/
├── docs/                # Folder dokumentasi ini
├── tb-frontend/         # Folder kode frontend
└── tb-backend/          # Folder kode backend
```

---

## 🚀 Status Tahapan Migrasi (Migration Status)

*   **Fase 1: Inisialisasi Dokumentasi Awal** ➡️ **[COMPLETED]**
    *   Pembuatan direktori `docs/` dan template overview dasar di target repositori `TB-Toko-Bangunan`.
*   **Fase 2: Pemindahan Frontend (`tb-frontend`)** ➡️ **[COMPLETED]**
    *   Pemindahan kode sumber Next.js dari legacy repository.
    *   Instalasi dependensi bersih dan turbopack build berhasil (`✓ Compiled successfully`).
    *   Pembuatan berkas `.env.example` ter-track Git.
*   **Fase 3: Pemindahan Backend (`tb-backend`)** ➡️ **[COMPLETED]**
    *   Pemindahan kode Express.js & Prisma ORM dari legacy repository.
    *   Instalasi dependensi bersih.
    *   Sinkronisasi database SQLite lokal baru (`dev.db`) & data seeder berhasil.
    *   Uji dev server berjalan lancar pada port `5000`.
*   **Fase 4A: Sinkronisasi Dokumentasi & Finalisasi Identitas** ➡️ **[COMPLETED]**
    *   Pembersihan nama dan identitas project yang rancu di dokumen target.
    *   Pembaruan file status migrasi dan penyusunan checklist hapus repositori lama.
*   **Fase 4B: Adopsi Onboarding & Workflow** ➡️ **[COMPLETED]**
    *   Adopsi dan adaptasi selektif berkas `onboarding/` (instruksi ChatGPT, room prompts) dan `workflow/` (working system, existing mode, project starter checklist) dari referensi `WK-Workflow-Kit` ke dalam repositori `TB-Toko-Bangunan`.
*   **Fase 4: Integrasi & Verifikasi Akhir** ➡️ **[PENDING]**
    *   Pengujian cross-connection antara frontend dan backend secara lokal.
*   **Fase 5: Arsip / Hapus Repositori Lama di GitHub** ➡️ **[PENDING]**
    *   Tindakan penghapusan/arsip repositori `tb-frontend` dan `tb-backend` lama setelah seluruh sistem terbukti stabil di repositori terpadu `TB-Toko-Bangunan`.

---

## 📋 Checklist Sebelum Menghapus/Mengarsipkan Repositori Lama

Sebelum repositori legacy `tb-frontend` dan `tb-backend` dihapus dari GitHub, pastikan poin-poin berikut telah dicentang:
- [x] Repositori `TB-Toko-Bangunan` sudah terunggah paling update di GitHub.
- [x] Folder `tb-frontend` sudah masuk ke repositori utama.
- [x] Folder `tb-backend` sudah masuk ke repositori utama.
- [x] Berkas `.env.example` untuk frontend dan backend sudah tersedia dan ter-commit di Git.
- [x] Aturan pengabaian Git `.gitignore` telah dipastikan bekerja (tidak ada `.env` asli, `dev.db`, `node_modules`, `.next/`, `dist/`, atau file log yang tidak sengaja ter-commit).
- [x] Proses compile & build frontend pernah sukses di repositori baru (`npm run build`).
- [x] Proses compile & build backend pernah sukses di repositori baru (`npm run build`).
- [x] Seluruh dokumentasi teknis (`docs/`) telah disinkronkan dan bebas dari nama/path lama yang rancu.
- [ ] Pengujian integrasi minimal (cross-connection lokal) sudah dilakukan dengan sukses (Fase 4).
- [ ] Persetujuan akhir dari Head of Project untuk penghapusan repositori lama telah diperoleh.

---
*Status Akhir: Fase 4B - Adopsi Onboarding & Workflow selesai. Siap untuk Fase 4.*
