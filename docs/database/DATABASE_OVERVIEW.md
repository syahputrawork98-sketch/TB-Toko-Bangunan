# Gambaran Umum Database (Database Overview)

## Purpose
Dokumen ini mendokumentasikan desain database, relasi tabel, dan aturan bisnis tingkat data pada aplikasi **TB (Toko Bangunan)**.

---

## Current Database Status
* **Status**: **Stable (SQLite)**.
* **ORM**: Prisma ORM (`prisma-client-js`).
* **Lokasi Skema**: `server/prisma/schema.prisma` (sebelumnya `tb-backend/prisma/schema.prisma` - legacy).

---

## Database Schema & Models

Database menggunakan SQLite dengan tabel-tabel berikut:

### 1. Model: `User`
Menyimpan kredensial pengguna dan perannya.
* `id` (Int, PK, Auto Increment)
* `username` (String, Unique)
* `password` (String, Hashed)
* `role` (String, `"ADMIN"` | `"CS"`)
* `createdAt` & `updatedAt` (DateTime)

### 2. Model: `Product`
Menyimpan data material dan inventaris barang toko.
* `id` (Int, PK, Auto Increment)
* `sku` (String, Unique) - Kode barang unik
* `name` (String) - Nama material
* `category` (String) - Kategori barang
* `price` (Float) - Harga jual ke pelanggan
* `costPrice` (Float) - Harga pokok pembelian (HPP/BPP)
* `stock` (Int) - Ketersediaan barang
* `unit` (String) - Satuan barang (misal: "Sak", "Batang", "Pail")
* `icon` (String, Optional) - Emoji representasi barang

### 3. Model: `Transaction`
Mencatat informasi transaksi penjualan global.
* `id` (Int, PK, Auto Increment)
* `totalAmount` (Float) - Total belanja
* `cashierId` (Int, FK -> User.id) - Kasir yang memproses
* `createdAt` (DateTime)

### 4. Model: `TransactionItem`
Mencatat item produk detail dari setiap transaksi belanja.
* `id` (Int, PK, Auto Increment)
* `transactionId` (Int, FK -> Transaction.id)
* `productId` (Int, FK -> Product.id)
* `quantity` (Int) - Jumlah barang dibeli
* `unitPrice` (Float) - Harga jual barang saat transaksi
* **`costPrice` (Float)**: *Snapshot HPP/BPP* barang saat transaksi. Digunakan untuk menghitung laba bersih kotor masa lalu tanpa terganggu perubahan harga modal barang saat ini.

### 5. Model: `Setting`
Konfigurasi identitas toko dan ambang batas stok.
* `id` (Int, PK, Default = 1)
* `shopName` (String, Default: "Toko Bangunan (TB)")
* `shopAddress` (String, Optional)
* `shopPhone` (String, Optional)
* `lowStockThreshold` (Int, Default = 10) - Batas sistem menandai stok tipis

---

## 💡 Strategi Snapshot HPP/BPP (Laba Akurat)
Pada tabel `TransactionItem`, harga modal (`costPrice`) disalin langsung dari harga pokok produk saat transaksi terjadi. 
* Jika di masa depan harga semen naik dari Rp58.000 menjadi Rp60.000, transaksi lama yang diproses pada harga modal Rp58.000 akan tetap dihitung menggunakan Rp58.000. Hal ini menjamin laporan keuangan masa lalu tidak bergeser (stabil secara akuntansi).

---

## Seed Data
Seed data diatur pada `server/prisma/seed.ts` yang otomatis menginisialisasi:
- User Admin: `admin` (password: `admin123`)
- User CS: `cs` (password: `cs123`)
- Setting toko awal.
- Tiga contoh produk (Semen Tiga Roda, Besi Beton, Cat Dulux).
