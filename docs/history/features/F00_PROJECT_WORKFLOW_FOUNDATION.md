# Feature Batch F00 — Project Workflow Foundation

## 🎯 Tujuan Fondasi Workflow
Menetapkan alur kerja standar dan batasan keamanan pengembangan sistem **TB-Toko-Bangunan** untuk memastikan tidak ada kode yang pecah (broken code), perubahan tidak sengaja pada data sensitif, atau refactor yang tidak terarah.

---

## 🏛️ Ringkasan Repositori Terpadu (Consolidated Repository)
Proyek ini mengonsolidasikan repositori terpisah (`tb-frontend` dan `tb-backend` mandiri) ke dalam satu repositori terpadu **TB-Toko-Bangunan** dengan pembagian folder:
- **`tb-frontend/`**: Berisi kode antarmuka berbasis Next.js 16.
- **`tb-backend/`**: Berisi kode backend server Express.js 5 & database SQLite dengan Prisma ORM.
- **`docs/`**: Berisi seluruh panduan, petunjuk teknis, onboarding, dan sejarah status proyek.

---

## 👥 Pembagian Peran Pengembang
Untuk membagi beban kognitif AI dan menjaga kualitas kode, alur pengerjaan dibagi menjadi beberapa peran AI terisolasi di bawah koordinasi User:
1. **User (Owner)**: Pemilik proyek yang memiliki hak penuh atas persetujuan rencana, pengujian langsung secara manual di localhost, serta operasi Git manual (commit, push, merge).
2. **Roomchat Spesialis (AI Spesialis)**: AI di ChatGPT yang diajak berdiskusi tentang analisis teknis mendalam per bidang/fitur spesifik. Menghasilkan *Technical Discussion Summary*. Tidak diperkenankan membuat batch resmi atau memberi instruksi langsung ke Gemini.
3. **Roomchat 00 (Manager)**: AI di ChatGPT yang merancang rencana batch fitur resmi (FXX) dan menuliskan instruksi eksekusi teknis untuk Gemini Anti-Gravity.
4. **Roomchat 01 (Reviewer)**: AI di ChatGPT yang mengaudit rencana batch (Batch Gate) guna memastikan kelayakan arsitektur dan meminimalkan risiko regresi sebelum disetujui User.
5. **Gemini Anti-Gravity (Local Executor)**: Model AI lokal yang berjalan di Anti-Gravity IDE untuk menulis kode, membuat berkas dokumentasi, dan memverifikasi perubahan lokal.

---

## 🔗 Hubungan dengan Berkas WORKING_SYSTEM.md
Seluruh aturan pembagian tugas AI, batasan batch kerja (Small, Medium, Large), kebijakan penggunaan model, dan definisi selesai (Definition of Done) dijabarkan secara formal dan mengikat pada berkas [WORKING_SYSTEM.md](../workflow/WORKING_SYSTEM.md).

---

## 📈 Status Batch
- **Status**: **Done**
- **Tanggal Selesai**: Juni 2026
