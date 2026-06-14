# F03 - Admin Inventory Management

## 1. Status Fitur
Status:
- Existing / Implemented

Keterangan:
- Fitur manajemen inventaris penuh untuk tingkat Admin yang berada di rute `/admin/inventory` untuk mengelola data master produk, termasuk data SKU, nama, kategori, harga jual, harga pokok pembelian (HPP/cost price), stok barang, unit satuan, dan ikon produk.

## 2. Tujuan Fitur
Menyediakan antarmuka bagi Admin untuk melakukan operasi CRUD (Create, Read, Update, Delete) pada katalog produk/material bangunan guna menjaga keakuratan persediaan fisik, harga jual, dan pencatatan harga pokok (HPP) yang digunakan untuk kalkulasi profitabilitas di sistem.

## 3. File / Path Evidence
Frontend:
- [client/src/app/(dashboard)/admin/inventory/page.tsx](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/client/src/app/(dashboard)/admin/inventory/page.tsx) - Halaman utama dan komponen utama `AdminInventoryPage` untuk F03.
- [client/src/app/(dashboard)/cs/inventory/page.tsx](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/client/src/app/(dashboard)/cs/inventory/page.tsx) - Halaman pembanding stok khusus peran CS (Cek Stok Barang / F07, terpisah dari F03).
- [client/src/components/layout/Sidebar/Sidebar.tsx](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/client/src/components/layout/Sidebar/Sidebar.tsx) - Menu samping untuk mengarahkan Admin ke "Inventaris" (`/admin/inventory`) dan CS ke "Cek Stok Barang" (`/cs/inventory`).
- [client/src/utils/api.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/client/src/utils/api.ts) - Axios HTTP client terkonfigurasi baseURL dan JWT Bearer interceptor.

Backend/API:
- [server/src/routes/productRoutes.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/server/src/routes/productRoutes.ts) - Rute API `/products` Express dengan pembatasan hak akses Admin untuk memanipulasi produk.
- [server/src/controllers/productController.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/server/src/controllers/productController.ts) - Logika kendali untuk mengambil, membuat, mengedit, menghapus, serta memperbarui stok produk.
- [server/src/middlewares/authMiddleware.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/server/src/middlewares/authMiddleware.ts) - Middleware keamanan (`authenticateToken`, `authorizeRole`, `isAdmin`, `isCS`).
- [server/src/app.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/server/src/app.ts) - Registrasi route root `/api/products`.

Database:
- [server/prisma/schema.prisma](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/server/prisma/schema.prisma) - Definisi model `Product` dan relasinya ke detail transaksi.

Dokumentasi Terkait:
- [F03_INVENTORY_MANAGEMENT.md](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/docs/history/features/F03_INVENTORY_MANAGEMENT.md)
- [F07_CS_INVENTORY_READ_ONLY.md](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/docs/history/features/F07_CS_INVENTORY_READ_ONLY.md)

## 4. UI / Frontend Area
- **Rute Akses**: `/admin/inventory` (menu "Inventaris" pada Sidebar Admin).
- **Elemen Teks Antarmuka**:
  - Judul Halaman: "Inventory Mastery"
  - Deskripsi Halaman: "Manage your material building product catalog."
- **Komponen Tabel Utama**:
  - Kolom data yang ditampilkan: **SKU**, **Product Name**, **Category**, **Price Sell/Cost**, **Stock**, dan **Actions**.
  - Poin Penting: Admin dapat melihat data harga jual (`price`) sekaligus harga pokok (`costPrice` / HPP).
- **Fitur Interaksi UI**:
  - **Daftar/Tabel Produk**: Menampilkan semua baris produk yang tersedia.
  - **Pencarian Produk**: Melakukan pencarian *client-side* berdasarkan nama produk dan SKU.
  - **Tambah Produk**: Tombol "Add New Product" membuka modal form untuk mengirim permintaan `POST /products`.
  - **Edit Produk**: Tombol edit berikon `Pencil` mengisi `formData` dan membuka modal dalam mode "Edit Product" untuk mengirim permintaan `PATCH /products/:id`.
  - **Hapus Produk**: Tombol hapus berikon `Trash2` menampilkan konfirmasi browser: *"Are you sure you want to delete this product?"* sebelum mengirim permintaan `DELETE /products/:id`.
  - **Input Stok Manual**: Penyesuaian stok dilakukan secara manual melalui kolom form tambah atau edit produk.
  - **Low Stock Indicator**: Menggunakan konstanta lokal `LOW_STOCK_THRESHOLD = 10` di mana stok bernilai `<= 10` akan dihiasi ikon `AlertTriangle` dan class CSS `lowStock`.
- **Komponen Pendukung**: Button, Modal, Input, Badge, serta ikon-ikon dari `lucide-react` (`Package`, `Pencil`, `Trash2`, `AlertTriangle`, `Search`, `Plus`).
- **State Manajemen**: Komponen memanfaatkan React *local state* (`products`, `search`, `loading`, `isModalOpen`, `editingProduct`, `formData`). Tidak ada store khusus Zustand yang menampung data produk ini.

## 5. API / Backend Area
API Client terhubung menggunakan Axios instance dengan Base URL `NEXT_PUBLIC_API_URL || http://localhost:5000/api` dan JWT Token dari cookie `tb_token` dikirim via header `Authorization: Bearer <token>`.

Rute API di server Express didefinisikan pada `/api/products` dengan endpoint:
1. **GET `/api/products`**
   - **Frontend call**: `api.get('/products')`
   - **Fungsi**: Mengambil seluruh produk dari database, diurutkan ascending berdasarkan nama.
2. **POST `/api/products`**
   - **Frontend call**: `api.post('/products')`
   - **Fungsi**: Menambahkan data produk baru (`sku`, `name`, `category`, `price`, `costPrice`, `stock`, `unit`, `icon`).
3. **PATCH `/api/products/:id`**
   - **Frontend call**: `api.patch('/products/' + id)`
   - **Fungsi**: Memperbarui kolom data produk berdasarkan ID (termasuk memperbarui angka stok dari form modal).
4. **DELETE `/api/products/:id`**
   - **Frontend call**: `api.delete('/products/' + id)`
   - **Fungsi**: Menghapus produk berdasarkan ID dari database.

*Catatan Fungsional Backend*:
Backend menyediakan endpoint `PATCH /api/products/:id/stock` (mengaktifkan fungsi `updateStock` di controller), namun endpoint ini **tidak digunakan** secara langsung di UI Admin Inventory (F03). Pembaruan stok pada F03 murni melewati form edit dan rute `PATCH /api/products/:id`.

## 6. Database Area
Prisma Client memetakan model **`Product`** pada database SQLite dengan field berikut:
- `id` (Int, Primary Key, autoincrement)
- `sku` (String, unique)
- `name` (String)
- `category` (String)
- `price` (Float / Harga Jual)
- `costPrice` (Float, default: 0 / HPP)
- `stock` (Int)
- `unit` (String)
- `icon` (String, optional)
- Relasi `transactionItems` (one-to-many ke model `TransactionItem` untuk melacak item terjual)

## 7. Alur Kerja Fitur
1. Pengguna masuk sebagai Admin dan membuka halaman `/admin/inventory`.
2. Komponen memicu pemanggilan `GET /api/products` saat inisiasi untuk mengambil katalog produk utuh dari database yang diurutkan berdasarkan alfabet nama produk.
3. Klien menyimpan respons ke dalam state local `products` lalu merendernya dalam baris tabel yang menampilkan harga jual, HPP, serta indikator stok tipis jika stok produk `<= 10`.
4. Saat Admin mencari produk, teks input menyaring state `products` secara lokal (client-side) mencocokkan field nama atau SKU produk.
5. Admin dapat menambah produk dengan menekan "Add New Product", mengisi form, dan menekan submit untuk memicu `POST /api/products`.
6. Admin dapat mengedit detail produk atau mengubah kuantitas stok produk melalui form edit yang memicu `PATCH /api/products/:id`.
7. Admin dapat menghapus produk dengan menekan icon Trash2, menyetujui konfirmasi dialog browser default, yang kemudian memicu `DELETE /api/products/:id` untuk menghapus record dari SQLite.

## 8. Batasan Role & Security
- **Middleware Rute Klien**:
  - Rute `/admin/inventory` dilindungi Next.js middleware, memastikan cookie `tb_token` valid dan cookie `tb_role` bernilai `'ADMIN'`. Jika dilanggar, user dilempar ke `/login`.
- **Keamanan Rute Backend**:
  - `GET /api/products` dapat diakses oleh Admin dan CS (menggunakan `authenticateToken`).
  - `POST /api/products`, `PATCH /api/products/:id`, dan `DELETE /api/products/:id` dikunci keras hanya untuk Admin menggunakan middleware gabungan `authenticateToken` dan `isAdmin` (berasal dari `authorizeRole(['ADMIN'])`).

## 9. Catatan Integrasi
- **Relasi dengan F01 (Auth)**: Menentukan validitas akses menu di sidebar serta token otorisasi header untuk transaksi API produk.
- **Relasi dengan F02 (Analytics)**: Data produk dari F03 digunakan oleh backend analytics `/summary` untuk menghitung agregat total produk (`totalProducts`) dan jumlah barang kritis (`lowStockItems`).
- **Relasi dengan F07 (CS Inventory Read-only)**: Rute Admin (F03) dan rute CS (F07) sama-sama membaca data catalog melalui `GET /api/products`. Namun, UI CS di rute `/cs/inventory` membatasi visibilitas data agar tidak memperlihatkan HPP (`costPrice`) serta tidak menyediakan tombol aksi manipulasi data (CRUD).

## 10. Risiko / Catatan Perbaikan
- **Inkonsistensi Threshold Stok Tipis**: Nilai batas stok tipis di halaman Admin Inventory (F03) di-hardcode sebesar `10` di tingkat klien Next.js. Sedangkan dasbor analitik Admin (F02) membaca threshold dinamis dari `Setting.lowStockThreshold` milik backend.
- **Keamanan endpoint Stok**: Rute `PATCH /api/products/:id/stock` hanya dilindungi middleware `authenticateToken` tanpa `isAdmin`, meskipun rute manipulasi produk lainnya dikunci oleh `isAdmin`.
- **Payload Data**: Baik Admin maupun CS memanggil API `GET /api/products` yang sama, sehingga backend tetap mengirim data lengkap (termasuk `costPrice` / HPP) ke browser CS meskipun UI CS (F07) menyembunyikannya dari tabel.
- **Handling Error UI**: Validasi form sebatas atribut input required bawaan HTML5 dan penanganan kegagalan API murni menampilkan alert browser standar tanpa UI state error khusus.
- **Tidak ada Service Layer**: Logika data catalog diimplementasikan langsung pada `productController.ts`.

## 11. Out of Scope
- Tidak menyediakan pagination tabel inventaris (semua item dimuat sekaligus).
- Tidak menyediakan filter kategori barang di antarmuka Admin (pencarian terbatas pada nama/SKU).
- Tidak menyediakan tombol sort kolom tabel.
- Tidak menyediakan fitur impor/ekspor data masal (bulk import/export).
- Tidak mendukung fitur pemindaian kode batang (barcode scanner).
- Tidak mencatat histori mutasi / penyesuaian stok (stock adjustment history).

## 12. Unknown / Belum Terverifikasi
- Ikon Search terdeteksi di-import di frontend, namun tidak terlihat implementasi visualnya secara eksplisit dalam kode masukan form pencarian.
- Tidak ada pesan umpan balik kosong (empty state text) khusus jika hasil filter pencarian tidak menemukan kecocokan produk apa pun.

## 13. Definition of Done Dokumentasi
Dokumentasi FXX dianggap selesai jika:
- Semua file evidence sudah dicatat.
- UI/frontend sudah dijelaskan berdasarkan kode.
- API/backend sudah diverifikasi.
- Database area sudah dicek.
- Role/security sudah dicek.
- Alur kerja fitur tidak mengandung asumsi.
- Risiko dan unknown sudah dicatat.
- Tidak ada fitur baru yang ditambahkan ke dokumentasi.
