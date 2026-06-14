# Project Starter Checklist (TB-Toko-Bangunan)

Dokumen ini digunakan sebagai checklist inisiasi saat pengembang/AI memulai pengerjaan batch baru di repositori **TB-Toko-Bangunan**.

---

## 📋 Daftar Periksa Awal (Starter Checklist)

### 1. Mode Kerja & Konteks Repositori
- [x] Memahami bahwa proyek ini adalah **Fullstack Multi Role** (Admin Dashboard & CS POS).
- [x] Memahami bahwa frontend berada di `tb-frontend/` dan backend berada di `tb-backend/`.
- [x] Memahami bahwa repositori lama di GitHub sudah berstatus *legacy* dan tidak boleh diubah.

### 2. Kepatuhan Dokumentasi (Discovery-First)
- [x] Seluruh berkas panduan di `docs/` telah dibaca dan dipahami.
- [x] `docs/history/CURRENT_STATUS.md` telah diperiksa untuk melihat checkpoint terakhir.
- [ ] Fitur yang akan dikerjakan sudah tercatat di index/history dokumen.
- [ ] Relasi teknis area (Frontend/Backend/Database) sudah dipetakan dengan status *Found*, *Needs Review*, dll.

### 3. Pemeriksaan Keamanan & Git (Wajib)
- [x] Aturan pengabaian berkas `.gitignore` telah aktif dan diperiksa (menghindari penambahan berkas `.env` atau database SQLite `dev.db`).
- [x] File `.env.example` sudah tersedia di folder `tb-frontend` dan `tb-backend`.
- [ ] Dilarang keras menginstal dependensi baru (`npm install <package>`) tanpa konfirmasi dan persetujuan eksplisit dari User.
- [ ] Dilarang keras melakukan penghapusan file atau pengubahan struktur folder tanpa instruksi langsung dari User.

### 4. Siklus Pengerjaan Batch
- [ ] Rencana perubahan dipecah menjadi batch kecil (Small/Medium Batch) untuk mempermudah review.
- [ ] Melakukan kompilasi build testing (`npm run build` di frontend & backend) untuk memverifikasi kestabilan sebelum melaporkan pekerjaan selesai.
- [ ] Memperbarui status proyek pada `docs/history/CURRENT_STATUS.md` setelah pengerjaan selesai.
