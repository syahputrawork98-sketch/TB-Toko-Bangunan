# Aturan Mode Existing & Discovery-First

Dokumen ini menjelaskan alur kerja dan logika audit untuk modul existing yang ada di dalam repositori **TB-Toko-Bangunan**. Inti dari mode ini adalah **Discovery-First Documentation** (penemuan fitur terlebih dahulu).

---

## 1. Prinsip Discovery-First
Sebelum melakukan modifikasi kode atau penambahan fitur baru di `tb-frontend` atau `tb-backend`, pengembang wajib mematuhi aturan berikut:
1.  **Dilarang Langsung Refactor**: Jangan mengubah struktur kode existing yang sudah berjalan stabil tanpa mapping terlebih dahulu.
2.  **Pemetaan Fitur**: Setiap modul harus divalidasi dan dicatat relasi teknisnya (di mana letak UI frontend, letak endpoint API backend, dan model database Prisma yang terpengaruh).
3.  **Hutang Dokumentasi (Documentation Debt)**: Jika terjadi perubahan cepat di kode sumber, dokumentasi pendukung harus segera disinkronkan melalui checkpoint dokumentasi (`FXX-CP`).

---

## 2. Status Relasi Teknis Area
Untuk setiap audit fitur existing, gunakan label status berikut pada berkas dokumentasi relasi area:
-   **Found** — File kode/fungsi sudah ditemukan dan diverifikasi stabil.
-   **Needs Review** — File/fungsi terindikasi ada, namun kinerjanya atau integrasinya belum diaudit penuh.
-   **Unknown** — Belum diketahui apakah fitur tersebut memiliki dependensi/tabel database terkait.
-   **Not Required** — Fitur tersebut tidak membutuhkan area terkait (misal: halaman statis tidak membutuhkan database).
-   **Partial** — Kode sebagian sudah dipetakan, namun sebagian lagi belum terlacak.
-   **Blocked** — Pemetaan terhambat karena adanya error teknis, masalah file locking, dll.

---

## 3. Alur Kerja Modifikasi Fitur Existing
```text
Temukan Fitur ➡️ Catat di docs/ ➡️ Petakan Relasi API/Data ➡️ Ajukan Rencana Batch ➡️ Eksekusi & Validasi
```
*   **Pre-Batch**: Merencanakan perubahan di Room 00 dan mengaudit risiko di Room 01 sebelum melakukan coding lokal.
*   **Batch Execution**: Gemini Anti-Gravity melakukan coding di workspace lokal Anti-Gravity IDE.
*   **Post-Batch**: Menjalankan build test (`npm run build`) dan verifikasi kestabilan sebelum melakukan git commit/push.

---
*Referensi Pola: Diadopsi dari template WK-Workflow-Kit.*
