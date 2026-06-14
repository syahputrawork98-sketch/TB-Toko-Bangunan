# Application Feature F08 — CS Transaction History

## 🎯 Detail Status Fitur
- **Title**: CS Transaction History
- **Status**: **Draft / Needs Discovery**
- **Feature Type**: History / Reprint Struk
- **User Role**: CS
- **Discovery Status**: Pending Audit UI/API/Data

---

## 📝 Deskripsi (Purpose)
Membantu kasir memantau riwayat penjualan pribadi yang ia proses selama shift aktif berjalan serta mencetak ulang struk lama jika pelanggan meminta salinan struk.

---

## 🛠️ Peta Wilayah Teknis (Possible Areas)
- **Antarmuka (UI Area)**: Rute `/cs/history`, daftar transaksi harian kasir aktif, detail struk modal popup.
- **API Area (Backend)**: Controller transaksi/shift Express dengan query parameter id kasir terkait.
- **Database Area**: Pembacaan tabel `Transaction` dengan filter berdasarkan `cashierId` kasir yang sedang terautentikasi.

---

## 📌 Catatan Tambahan (Notes)
- Kasir CS tidak diperbolehkan menghapus atau mengedit data transaksi yang sudah ter-record di database.
