# F02 - Admin Dashboard

## 1. Status Fitur
Status:
- Existing / Implemented

Keterangan:
- Halaman dashboard utama yang berfokus pada visualisasi metrik bisnis analitik (Admin Analytics / Business Intelligence Dashboard). Route `/admin` otomatis melakukan redirect ke rute aktif di `/admin/analytics`.

## 2. Tujuan Fitur
Menampilkan visualisasi ringkasan kinerja keuangan toko meliputi total pendapatan (revenue), jumlah transaksi, estimasi total keuntungan kotor (profit) dari selisih harga jual dan HPP (cost price) barang, serta grafik tren penjualan mingguan (7 hari terakhir) untuk membantu Admin memantau perkembangan bisnis.

## 3. File / Path Evidence
Frontend:
- [client/src/app/(dashboard)/admin/page.tsx](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/client/src/app/(dashboard)/admin/page.tsx) - Menangani redirect rute `/admin` ke `/admin/analytics`.
- [client/src/app/(dashboard)/admin/analytics/page.tsx](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/client/src/app/(dashboard)/admin/analytics/page.tsx) - Halaman utama Admin Analytics.
- [client/src/app/(dashboard)/layout.tsx](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/client/src/app/(dashboard)/layout.tsx) - Wrapper dashboard yang menggunakan komponen Sidebar dan Navbar.
- [client/src/components/layout/Sidebar/Sidebar.tsx](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/client/src/components/layout/Sidebar/Sidebar.tsx) - Menu samping untuk peran ADMIN berisi navigasi: Analytics, Staff, Inventory, Reports, dan Settings.
- [client/src/components/layout/Navbar/Navbar.tsx](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/client/src/components/layout/Navbar/Navbar.tsx) - Header dashboard dengan breadcrumb dan tampilan role user berdasarkan path saat ini.
- [client/src/app/(dashboard)/admin/analytics/analytics.module.css](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/client/src/app/(dashboard)/admin/analytics/analytics.module.css) - Styling kartu informasi dan kustomisasi bagan grafik batang (bar chart).
- [client/src/store/authStore.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/client/src/store/authStore.ts) - Mengambil data user yang sedang login untuk menampilkan username.
- [client/src/utils/api.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/client/src/utils/api.ts) - Axios HTTP client terkonfigurasi baseURL dan JWT Bearer interceptor.
- [client/src/utils/format.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/client/src/utils/format.ts) - Fungsi utilitas untuk memformat nilai mata uang Rupiah (IDR).

Backend/API:
- [server/src/routes/analyticsRoutes.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/server/src/routes/analyticsRoutes.ts) - Rute Express untuk API analitik (endpoint `/summary`, `/chart`, dan `/cs-stats`).
- [server/src/controllers/analyticsController.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/server/src/controllers/analyticsController.ts) - Logika kalkulasi ringkasan, profit, revenue, dan tren grafik 7 hari terakhir.
- [server/src/middlewares/authMiddleware.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/server/src/middlewares/authMiddleware.ts) - Middleware keamanan (`authenticateToken`, `authorizeRole`, `isAdmin`).
- [server/src/app.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/server/src/app.ts) - Registrasi route root `/api/analytics`.

Database:
- [server/prisma/schema.prisma](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/server/prisma/schema.prisma) - Model relasional data `User`, `Product`, `Transaction`, `TransactionItem`, dan `Setting`.

## 4. UI / Frontend Area
- **Rute `/admin`**: Berfungsi sebagai entry point yang secara langsung melakukan redirect otomatis ke rute utama `/admin/analytics`.
- **Halaman `/admin/analytics`**: 
  - Menampilkan judul header "Business Intelligence".
  - Greeting berupa pesan selamat datang kepada admin yang sedang aktif: "Welcome back, {username}".
  - Tombol interaktif "Refresh Data" untuk memicu pemuatan ulang data dari API backend.
  - Kartu statistik (Stat Cards) yang menampilkan:
    - **Total Revenue**: Total pendapatan yang terformat dalam IDR.
    - **Total Transactions**: Total transaksi penjualan yang telah diproses.
    - **Est. Total Profit**: Estimasi laba kotor toko (IDR).
  - Tampilan Grafik (Chart):
    - **Revenue Trend Last 7 Days**: Visualisasi tren penjualan mingguan.
    - Dibuat secara manual menggunakan custom CSS bar chart (bukan library visualisasi pihak ketiga) dengan interaksi hover tooltip yang menampilkan nominal jumlah transaksi/pendapatan secara presisi.
  - State kosong (Empty State):
    - Jika tidak ada data transaksi penjualan, UI akan menampilkan pesan fallback: "No sales data available yet.".
  - State managemen pada komponen frontend:
    - Menyimpan status data ringkasan dalam state `summary`.
    - Menyimpan data tren grafik dalam state `chartData`.
    - Mengelola status loading dengan state boolean `loading`.
    - Memanfaatkan `useAuthStore` untuk mengambil objek data user login guna menampilkan username Admin.

## 5. API / Backend Area
Endpoint backend yang diakses oleh fitur ini meliputi:
1. **GET `/api/analytics/summary`**
   - **Frontend call**: `api.get('/analytics/summary')`
   - **Middleware Keamanan**: `authenticateToken` + `isAdmin`
   - **Controller Handler**: `getSummary`
   - **Response data**:
     ```json
     {
       "totalRevenue": number,
       "totalProfit": number,
       "totalTransactions": number,
       "totalProducts": number,
       "lowStockItems": number
     }
     ```
   - *Catatan Fungsional*: Frontend F02 saat ini hanya menampilkan data `totalRevenue`, `totalProfit`, dan `totalTransactions`. Nilai `totalProducts` dan `lowStockItems` telah dihitung dan disediakan oleh backend, namun belum dirender/ditampilkan di antarmuka frontend F02.

2. **GET `/api/analytics/chart`**
   - **Frontend call**: `api.get('/analytics/chart')`
   - **Middleware Keamanan**: `authenticateToken` + `isAdmin`
   - **Controller Handler**: `getSalesChart`
   - **Response data**: Array objek tren harian dalam kurun waktu 7 hari terakhir:
     ```json
     [
       {
         "date": "string",
         "amount": number
       }
     ]
     ```

## 6. Database Area
Query data analitik memanfaatkan tabel-tabel berikut melalui Prisma ORM:
1. **Model `Transaction`**:
   - Kolom `totalAmount`: Digunakan untuk menjumlahkan total pendapatan (revenue) serta nominal harian pada grafik penjualan.
   - Kolom `createdAt`: Digunakan untuk memfilter rentang waktu transaksi dalam kurun waktu 7 hari terakhir.
   - Kolom `cashierId` & `cashier`: Digunakan untuk mendapatkan relasi kasir pembuat transaksi.
2. **Model `TransactionItem`**:
   - Kolom `unitPrice`, `costPrice`, dan `quantity`: Digunakan untuk menghitung estimasi keuntungan kotor (profit) dengan rumus selisih harga jual dengan HPP dikalikan jumlah barang terjual.
3. **Model `Product`**:
   - Kolom `stock`, `costPrice`, dan `price`: Digunakan backend untuk menghitung agregat jumlah produk (`totalProducts`) dan menyaring barang dengan stok menipis (`lowStockItems`).
4. **Model `Setting`**:
   - Kolom `lowStockThreshold`: Menentukan batas minimum stok tipis secara global (jika record pengaturan tidak ditemukan, server backend fallback ke threshold default bernilai `10`).
5. **Model `User`**:
   - Kolom `role`: Menentukan hak akses Admin agar dapat memanggil database analitik.

## 7. Alur Kerja Fitur
1. Pengguna masuk ke sistem sebagai `ADMIN` lalu diarahkan ke rute `/admin/analytics`.
2. Halaman memicu efek inisiasi (`useEffect`) untuk memanggil API backend `GET /api/analytics/summary` dan `GET /api/analytics/chart` menggunakan Axios helper `client/src/utils/api.ts` dengan Authorization Header pembawa token.
3. Controller Express memproses query ke SQLite via Prisma, menjumlahkan total transaksi dan pendapatan, memfilter data 7 hari terakhir, menghitung selisih HPP (profit), dan mengirimkan respons JSON kembali ke client.
4. Klien memperbarui state lokal `summary` dan `chartData` setelah data berhasil diterima, lalu menonaktifkan status `loading`.
5. Format Rupiah diaplikasikan pada nominal angka uang sebelum dirender ke dalam kartu dasbor.
6. Custom CSS memetakan nilai harian dari API chart ke tinggi bar chart secara proporsional, serta memunculkan tooltip data saat user mengarahkan kursor mouse (hover) ke bar chart terkait.
7. Admin dapat menenang tombol "Refresh Data" kapan pun untuk mengulangi proses pengambilan data terbaru dari server.

## 8. Batasan Role & Security
- **Proteksi Rute Klien (Next.js Middleware)**:
  - Middleware membaca cookie `tb_token` dan `tb_role`.
  - Jika pengguna mengakses `/admin` atau `/admin/*` tanpa token aktif, mereka langsung dialihkan ke `/login`.
  - Jika pengguna terotentikasi mengakses `/admin` atau `/admin/*` dengan peran di luar `ADMIN` (seperti `CS`), rute akan diblokir dan dialihkan kembali ke `/login`.
  - Jika pengguna yang sudah login dengan peran `ADMIN` mengakses rute akar `/` atau halaman `/login`, mereka diarahkan secara otomatis ke `/admin/analytics`.
- **Proteksi Endpoint API Backend**:
  - Endpoint `/api/analytics/summary` dan `/api/analytics/chart` dilindungi secara berlapis oleh middleware `authenticateToken` dan `isAdmin` (berasal dari `authorizeRole(['ADMIN'])`). Pengguna dengan token tidak sah atau ber-role selain `ADMIN` akan mendapatkan respon error `403 Forbidden` atau `401 Unauthorized`.

## 9. Catatan Integrasi
- **Ketergantungan pada F01**: Fitur dasbor admin ini sangat bergantung pada modul keamanan F01 karena proses pembatasan navigasi klien ditentukan oleh cookie `tb_token` dan `tb_role` yang ditulis oleh `authStore` (Zustand), serta autentikasi data API backend dikontrol secara mutlak oleh validitas JWT token yang disisipkan oleh interseptor Axios.

## 10. Risiko / Catatan Perbaikan
- **Visualisasi Grafik**: Tidak menggunakan library visualisasi pihak ketiga (seperti Chart.js atau Recharts). Grafik dirender secara kustom memanfaatkan flexbox/grid CSS murni, yang membatasi fleksibilitas modifikasi visual grafik.
- **Handling Error UI**: Jika terjadi kegagalan pemanggilan API (fetch error), sistem tidak memunculkan notifikasi error khusus ke interface pengguna. Pesan kesalahan hanya dicatat langsung ke console browser (`console.error`).
- **Data yang Tidak Ditampilkan**: Backend mengembalikan nilai `totalProducts` dan `lowStockItems`, namun bagian antarmuka frontend saat ini tidak memetakan/menampilkan data tersebut.
- **Batasan Skala Waktu Grafik**: Belum ada kontrol visual (filter range picker) untuk mengubah filter periode analitik; grafik batang secara keras (hardcoded) membatasi tampilan hanya untuk rentang 7 hari terakhir dari sisi query database.
- **Service Layer**: Tidak ada service layer khusus untuk memisahkan urusan analitik di backend; seluruh logika agregasi data diproses langsung di dalam modul controller.

## 11. Out of Scope
- Tidak menggunakan library grafik eksternal (Recharts, Chart.js, ApexCharts, dll.).
- Tidak menyediakan fitur ekspor laporan (CSV, Excel, PDF).
- Tidak menyediakan filter rentang waktu kustom (harian, bulanan, tahunan) di halaman dashboard.
- Tidak menyajikan modul analitik tingkat lanjut (seperti metrik performa individual kasir/staff atau laporan stok terlaris langsung pada dashboard ini).
- Tidak menyajikan notifikasi banner error yang terlihat oleh user.

## 12. Unknown / Belum Terverifikasi
- Indikator pemuatan data (loading spinner/shimmer) yang spesifik tidak ditemukan saat state loading bernilai true, meskipun state status loading dikelola di dalam kode.

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
