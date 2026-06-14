# Sistem Kerja Proyek (Working System)

Sistem kerja **TB-Toko-Bangunan** dirancang untuk menjamin keamanan, konsistensi kode, dan keteraturan dalam pengembangan repositori terpadu.

---

## 🏛️ Prinsip Utama
1.  **Git & GitHub sebagai Source of Truth**: Seluruh perubahan kode harus dilacak dan dicatat dalam repositori terpadu `TB-Toko-Bangunan`.
2.  **Pemisahan Tugas AI**: 
    *   Sesi konseptual/perencanaan dilakukan oleh **Roomchat 00 (Manager)** di ChatGPT.
    *   Sesi peninjauan kritis dilakukan oleh **Roomchat 01 (Reviewer)** di ChatGPT.
    *   Eksekusi pengubahan berkas lokal dilakukan oleh **Gemini Anti-Gravity** di Anti-Gravity IDE.
3.  **Dilarang Git Commit/Push Otomatis**: AI eksekutor dilarang melakukan commit atau push secara mandiri. Tahap ini sepenuhnya berada di bawah kendali manual User (Owner).
4.  **Discovery-First & Zero-Refactor**: Jangan lakukan refactor kode atau modifikasi fitur existing sebelum merinci fiturnya di dokumen `/docs`.

---

## 👥 Pembagian Peran
-   **User (Owner)**: Pemilik proyek yang memegang kendali penuh atas persetujuan rencana, pengujian runtime, serta operasi git (commit, push, merge).
-   **Roomchat 00 (Manager)**: Merencanakan alur kerja, mendefinisikan scope batch fitur baru, dan menyusun instruksi teknis untuk eksekutor.
-   **Roomchat 01 (Reviewer)**: Menguji dan mengaudit rencana yang disusun Room 00 (Batch Gate) untuk meminimalkan risiko regresi kode.
-   **Gemini Anti-Gravity**: Melakukan coding, penulisan dokumentasi, dan verifikasi lokal di Anti-Gravity IDE berdasarkan rencana yang disetujui.

---

## 📦 Ukuran Batch Kerja (Batch Sizes)
Untuk meminimalkan konflik penggabungan dan mempercepat proses review:
-   **Small Batch**: Modifikasi 1–3 berkas (risiko rendah, perbaikan teks/bug kecil).
-   **Medium Batch**: Modifikasi 4–8 berkas (satu modul, penambahan endpoint, atau komponen UI minor).
-   **Large Batch**: Lebih dari 8 berkas. **Wajib dipecah** menjadi beberapa sub-batch yang lebih kecil.

---

## 📐 Penamaan Batch Fitur (Naming Policy)
Gunakan kode penamaan berikut pada riwayat dan dokumentasi fitur:
-   `F00` = Inisialisasi Alur Kerja & Setup Monorepo target
-   `F01` = Fitur Inti POS & Kasir CS
-   `F02` = Fitur Dasbor Analitik & Laba Kotor Admin
-   `F03` = Fitur Manajemen Inventaris CRUD Admin
-   `F04` = Integrasi Global Setting & Multi-role Authentication
-   `FXX-CP` = Checkpoint Sinkronisasi Dokumentasi (Penyelesaian Hutang Dokumentasi / *Documentation Debt*)

---

## 🛡️ Kebijakan Penggunaan Model AI (Model Policy)
Guna meningkatkan efisiensi biaya dan kecepatan:
-   **Default Executor Model**: **Gemini 3.5 Flash High** digunakan sebagai model utama untuk eksekusi penulisan kode, instalasi dependensi, penyalinan file, dan pembuatan dokumentasi umum.
-   **Escalation Model**: **Gemini 3.1 Pro** dicadangkan khusus untuk analisis arsitektur mendalam, pemecahan masalah (troubleshooting) kompleks, audit keamanan auth, dan refactor planning tingkat tinggi.

---

## 📑 Definisi Selesai (Definition of Done)
Sebuah batch kerja dinyatakan selesai (*Done*) jika memenuhi kriteria berikut:
1.  Seluruh kriteria penerimaan dalam instruksi batch terpenuhi.
2.  Proyek berhasil di-build tanpa error TypeScript, TypeScript build info terbarui, dan tidak ada linting error (`npm run build` sukses).
3.  Berkas status proyek (`docs/history/CURRENT_STATUS.md`) dan berkas detail fitur terkait telah diperbarui secara akurat.
4.  Laporan hasil eksekusi (walkthrough) telah diserahkan kepada User.
5.  User telah memverifikasi secara manual, melakukan commit, dan melakukan push ke GitHub.

---

## 📁 Struktur Dokumentasi Terpadu (History Layer)
Sesuai pola referensi *WK-Workflow-Kit*, dokumentasi dipisahkan menjadi dua lapisan:
1.  **Workflow/Control Layer** (`docs/project/`): Berisi panduan alur kerja dan onboarding sistem yang dapat dihapus/diabaikan jika proyek ingin diserahkan ke pihak luar secara bersih.
2.  **Persistent Project Memory Layer** (`docs/history/`): Berisi log status berjalan (`CURRENT_STATUS.md`) dan detail penemuan/milestone fitur (`features/`). Lapisan ini wajib dipertahankan untuk memelihara ingatan historis pengembangan sistem.
