# Gambaran Umum Proyek (Project Overview)

Dokumen ini merangkum visi, arsitektur, dan modul fungsional dari aplikasi **TB (Toko Bangunan) Industrial Management System**.

---

## 🎯 Visi & Konsep Desain
Membangun infrastruktur digital yang tangguh, efisien, dan memiliki estetika **"Industrial Blueprint"** untuk manajemen operasional toko bangunan modern.
- **Warna Aksen**: *Deep Industrial Gray* dan *Safety Orange* untuk memberikan kesan profesional teknik.
- **Tipografi**: Menggunakan font *Inter* untuk keterbacaan tingkat tinggi di area kasir/lapangan yang sibuk.
- **Desain Geometris**: Sudut-sudut tajam (*premium corner accents*) pada kartu data dan tabel.

---

## 🏗️ Modul & Fitur Aplikasi

Sistem memiliki dua modul utama berdasarkan hak akses/peran (Role):

### 🏢 1. Modul Super Admin Dashboard
Pusat kendali strategis untuk pemilik/manajer toko.
- **Analytics & Reporting Hub**:
  - Total pendapatan kotor real-time.
  - Perhitungan laba kotor otomatis berdasarkan sistem *Snapshot Harga Pokok Penjualan (HPP)*.
  - Grafik tren penjualan 7 hari terakhir.
- **Inventory CRUD**:
  - Manajemen penuh data barang (Nama, Kategori, Stok, Satuan, Icon).
  - Pemisahan Harga Pokok Penjualan (HPP/BPP) dan Harga Jual.
- **Staff Management**:
  - Pendaftaran akun Customer Service (CS) baru dan pencabutan akses.
- **Global Shop Settings**:
  - Ubah profil struk (Nama Toko, Alamat, Telepon).
  - Pengaturan *Low Stock Threshold* (Ambang batas stok tipis).

### 💼 2. Modul Customer Service (CS) Terminal
Pusat operasional pelayanan pelanggan dan kasir harian.
- **Point of Sale (POS) Terminal**:
  - Pencarian barang instan berdasarkan Nama atau SKU.
  - Sistem keranjang belanja dengan validasi stok otomatis.
  - Pemrosesan transaksi aman dan pencetakan struk belanja.
- **Inventory Explorer**:
  - Cek ketersediaan stok barang secara instan (Read-only).
  - *Data Shield*: Harga modal (HPP) disembunyikan dari modul CS demi kerahasiaan bisnis.
- **Personal History**:
  - Laporan penjualan mandiri milik kasir yang aktif per-shift.
  - Cetak ulang struk transaksi lama.
- **Self Profile**:
  - Update username & password mandiri dengan pengaman *show/hide password*.

---

## 🚀 Poin Keunggulan Teknis
- **Financial Snapshots**: Harga modal (HPP) dikunci di tabel transaksi saat pembayaran dilakukan. Hal ini mencegah kesalahan perhitungan laba historis jika harga modal produk berubah di masa depan.
- **Atomic Transactions**: Transaksi kasir aman dari kegagalan sinkronisasi stok jika koneksi terputus tiba-tiba.
- **Zero-Loop Navigation**: Middleware cerdas mencegah pengulangan rute tanpa akhir saat proses pengecekan sesi login.

---
*Status Sistem: Siap Produksi (Verified Stable).*
