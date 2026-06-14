# Application Feature F03 — Inventory Management

## 🎯 Detail Status Fitur
- **Title**: Inventory Management
- **Status**: **Draft / Needs Discovery**
- **Feature Type**: CRUD / Inventory
- **User Role**: Admin
- **Discovery Status**: Pending Audit UI/API/Data

---

## 📝 Deskripsi (Purpose)
Manajemen data produk/material bangunan toko lengkap meliputi penambahan SKU, nama barang, harga jual, harga pokok (HPP/BPP modal), update stok manual, dan kategori barang.

---

## 🛠️ Peta Wilayah Teknis (Possible Areas)
- **Antarmuka (UI Area)**: Halaman kelola produk `/admin/inventory`, form produk, dan tabel material.
- **API Area (Backend)**: Controller produk (`/api/products/*`) Express.
- **Database Area**: Model `Product` (field `sku`, `name`, `price`, `costPrice`, `stock`, `unit`).

---

## 📌 Catatan Tambahan (Notes)
- Panel Admin harus dapat menampilkan nilai HPP/BPP secara eksplisit (sedangkan modul CS menyembunyikannya).
