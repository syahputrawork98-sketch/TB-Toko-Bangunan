# Application Feature F02 — Admin Dashboard

## 🎯 Detail Status Fitur
- **Title**: Admin Dashboard
- **Status**: **Draft / Needs Discovery**
- **Feature Type**: Analytics / Reporting
- **User Role**: Admin (Super Admin)
- **Discovery Status**: Pending Audit UI/API/Data

---

## 📝 Deskripsi (Purpose)
Menampilkan visualisasi ringkasan kinerja keuangan toko meliputi akumulasi laba bersih kotor (dari kalkulasi HPP produk saat transaksi) dan grafik tren penjualan mingguan demi mempermudah owner memantau bisnis.

---

## 🛠️ Peta Wilayah Teknis (Possible Areas)
- **Antarmuka (UI Area)**: Rute `/admin` atau `/admin/analytics`, grafik data analitik, dan panel informasi.
- **API Area (Backend)**: Controller analitik (pendapatan kotor, laba kotor, omzet harian) di Express.
- **Database Area**: Query agregasi dari tabel transaksi dan relasi detail transaksi.

---

## 📌 Catatan Tambahan (Notes)
- Grafik performa disarankan menggunakan pustaka visualisasi yang responsif dan mematuhi skema warna industrial/gray-accent.
