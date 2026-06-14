# Feature Batch F01 — Documentation Structure

## 🎯 Tujuan Struktur Dokumentasi
Memastikan seluruh informasi teknis, riwayat status, dan onboarding pengembang terdokumentasi dengan rapi dan terstruktur secara logis. Hal ini meminimalkan waktu onboarding AI/pengembang baru dan menjaga agar context window AI tetap efisien.

---

## 📂 Folder Utama Dokumentasi
Dokumentasi diatur di bawah folder `docs/` dengan pembagian fungsi berikut:
1. **`docs/project/`**: Lapisan kontrol alur kerja, onboarding sistem, dan deskripsi proyek global (`docs/project/PROJECT_OVERVIEW.md`).
2. **`docs/frontend/`**: Dokumentasi spesifikasi arsitektur, pemetaan antarmuka, dan gaya dari sub-proyek frontend.
3. **`docs/backend/`**: Dokumentasi rute API, middleware, kontroler, dan layanan sub-proyek backend.
4. **`docs/database/`**: Dokumentasi skema database relasional (Prisma/SQLite) dan data seeder.
5. **`docs/development/`**: Panduan instalasi lokal dan instruksi cara menjalankan server lokal.
6. **`docs/history/`**: Log status proyek saat ini (`CURRENT_STATUS.md`) dan riwayat pengerjaan batch fitur.

---

## 🏛️ Justifikasi Pembuatan `docs/history/features/`
Folder `docs/history/features/` bertindak sebagai **Persistent Memory Layer** (Lapisan Ingatan Proyek yang Persisten).
- **Alasan**: Seiring berkembangnya sistem, context window AI akan kewalahan jika semua log pengerjaan ditaruh dalam satu berkas besar. Dengan membagi setiap batch fitur utama (seperti F00, F01, dll.) ke dalam file markdown tersendiri, AI eksekutor hanya perlu membaca file indeks `FEATURE_HISTORY.md` dan detail berkas fitur yang sedang dikerjakan. Ini membuat penelusuran riwayat sistem menjadi modular dan terisolasi.

---

## 📈 Status Batch
- **Status**: **Done**
- **Tanggal Selesai**: Juni 2026
