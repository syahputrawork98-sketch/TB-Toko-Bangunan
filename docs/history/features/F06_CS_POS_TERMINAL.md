# Application Feature F06 — CS POS Terminal

## 🎯 Detail Status Fitur
- **Title**: CS POS Terminal
- **Status**: **Draft / Needs Discovery**
- **Feature Type**: POS / Transaction
- **User Role**: CS (Customer Service / Kasir)
- **Discovery Status**: Pending Audit UI/API/Data

---

## 📝 Deskripsi (Purpose)
Terminal transaksi kasir untuk menginput pembelanjaan material pelanggan, menghitung kembalian, memotong stok secara aman, dan menerbitkan struk belanja.

---

## 🛠️ Peta Wilayah Teknis (Possible Areas)
- **Antarmuka (UI Area)**: Rute `/cs/pos`, pencarian SKU kilat, panel keranjang belanja, print struk view.
- **API Area (Backend)**: Controller transaksi Express (endpoint POST `/api/transactions`).
- **Database Area**: Tabel `Transaction`, `TransactionItem`, dan pengurangan atomic field `stock` di `Product`.

---

## 📌 Catatan Tambahan (Notes)
- **HPP Snapshot**: Transaksi wajib menyalin dan mengunci harga beli modal produk (`costPrice`) ke dalam tabel `TransactionItem` saat pembayaran diselesaikan.
