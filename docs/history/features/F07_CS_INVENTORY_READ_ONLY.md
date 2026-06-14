# Application Feature F07 — CS Inventory Read-only

## 🎯 Detail Status Fitur
- **Title**: CS Inventory Read-only
- **Status**: **Draft / Needs Discovery**
- **Feature Type**: Inventory Explorer (Read-only)
- **User Role**: CS
- **Discovery Status**: Pending Audit UI/API/Data

---

## 📝 Deskripsi (Purpose)
Memungkinkan kasir/CS memeriksa ketersediaan stok barang secara cepat tanpa memiliki hak akses untuk melihat nominal BPP/HPP (harga pokok pembelian modal) produk demi kerahasiaan data internal toko.

---

## 🛠️ Peta Wilayah Teknis (Possible Areas)
- **Antarmuka (UI Area)**: Rute `/cs/inventory`, tabel stok produk, pencarian barang.
- **API Area (Backend)**: Controller produk Express khusus untuk CS (menghilangkan/men-select out field `costPrice`).
- **Database Area**: Pembacaan dari tabel `Product` dengan pengecualian field sensitif.

---

## 📌 Catatan Tambahan (Notes)
- **Data Shield**: Pastikan field `costPrice` sama sekali tidak dikirim dalam payload response API backend saat kasir mengakses endpoint ini.
