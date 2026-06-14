# Feature Batch F02 — Frontend Migration

## 🎯 Tujuan Migrasi Frontend
Memindahkan kode antarmuka (frontend Next.js 16) dari repositori lama yang terpisah ke dalam folder `client/` (sebelumnya `tb-frontend/` - legacy) di bawah repositori terpadu **TB-Toko-Bangunan** guna menyatukan pengelolaan repositori.

---

## 📦 Ringkasan Migrasi
- Direktori `client/` (sebelumnya `tb-frontend/` - legacy) dipindahkan ke root `TB-Toko-Bangunan`.
- Folder `.git` lama dibuang untuk mencegah konflik multi-git repository.
- Folder dependencies (`node_modules`), folder build (`.next`, `dist`, `build`), serta file rahasia (`.env.local`) tidak disertakan saat pemindahan.
- Proses build dan compile lokal Next.js terverifikasi sukses dijalankan di lingkungan baru.

---

## 📌 Catatan Tambahan (Notes)
- **Status Integrasi**: Pengujian integrasi lokal (Local Integration Test) yang menghubungkan frontend dan backend masih dalam status **Pending** (belum dijalankan).
