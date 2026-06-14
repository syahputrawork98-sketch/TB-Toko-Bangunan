# F04 - Staff Management

## 1. Status Fitur
Status:
- Existing / Implemented

Keterangan:
- Fitur administrasi bagi Admin untuk mengelola akun user/staff toko. Manajemen ini murni menggunakan model database `User` (bukan model `Staff` terpisah) yang berlokasi pada rute `/admin/staff`.

## 2. Tujuan Fitur
Menyediakan antarmuka bagi Admin untuk mengontrol akses masuk ke sistem dengan mendaftarkan akun baru (memilih peran `ADMIN` atau `CS`), melihat daftar akun aktif, dan menghapus akun yang tidak lagi diperlukan, guna menjamin keamanan operasional toko.

## 3. File / Path Evidence
Frontend:
- [client/src/app/(dashboard)/admin/staff/page.tsx](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/client/src/app/(dashboard)/admin/staff/page.tsx) - Halaman utama dan komponen utama `StaffManagementPage` untuk F04.
- [client/src/components/layout/Sidebar/Sidebar.tsx](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/client/src/components/layout/Sidebar/Sidebar.tsx) - Menu samping Admin untuk navigasi ke "Staf Toko" (`/admin/staff`).
- [client/src/utils/api.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/client/src/utils/api.ts) - API client global dengan base URL `/api` dan JWT Bearer interceptor.
- [client/src/middleware.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/client/src/middleware.ts) - Proteksi navigasi klien berdasarkan cookie `tb_token` dan `tb_role`.

Backend/API:
- [server/src/app.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/server/src/app.ts) - Registrasi root route `/api/users`.
- [server/src/routes/userRoutes.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/server/src/routes/userRoutes.ts) - Definsi rute Express untuk manipulasi user dengan batasan otorisasi Admin.
- [server/src/controllers/userController.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/server/src/controllers/userController.ts) - Logika kendali untuk mengambil daftar user, membuat akun baru, menghapus akun, dan memperbarui profil sendiri.
- [server/src/middlewares/authMiddleware.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/server/src/middlewares/authMiddleware.ts) - Middleware otentikasi Express (`authenticateToken`, `authorizeRole`, `isAdmin`).

Database:
- [server/prisma/schema.prisma](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/server/prisma/schema.prisma) - Model `User` dan relasi transactions.
- [server/prisma/seed.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/server/prisma/seed.ts) - Data pemula akun default (`admin` dan `cs`) dengan password ter-hash.

## 4. UI / Frontend Area
- **Rute Akses**: `/admin/staff` (menu "Staf Toko" pada Sidebar Admin).
- **Komponen Tabel Utama**:
  - Kolom data yang ditampilkan: **Username**, **Role**, **Created At**, dan kolom aksi (**Delete**).
  - Terdapat badge informasi jumlah total user/staff yang sedang terdaftar: `users.length` dengan label: "Total".
- **Fitur Interaksi UI**:
  - **Daftar User/Staff**: Tabel yang merender koleksi akun user aktif.
  - **Tambah User/Staff**: Tombol "Add New Staff" (dihiasi ikon `UserPlus`) yang membuka modal form pendaftaran. Form ini menerima masukan: `username`, `password`, dan seleksi peran (`role`: `CS` / Customer Service atau `ADMIN` / Super Admin). Form submit mengirim permintaan `POST /users`.
  - **Hapus User/Staff**: Tombol aksi berikon `Trash2` yang memicu fungsi `handleDeleteUser(user.id)` untuk mengirim permintaan `DELETE /users/:id`.
- **Komponen Pendukung**: Button, Modal, Input, Badge, serta ikon `Trash2` dan `UserPlus` dari `lucide-react`.
- **State Manajemen**: Komponen memanfaatkan React *local state* (`users`, `loading`, modal create, `username`, `password`, `role`, submit state). Tidak ada store Zustand khusus staff/user.

## 5. API / Backend Area
API Client terhubung menggunakan Axios instance dengan Base URL `NEXT_PUBLIC_API_URL || http://localhost:5000/api` dan JWT Token dari cookie `tb_token` dikirim via header `Authorization: Bearer <token>`.

Rute API di server Express didefinisikan pada `/api/users` dengan endpoint:
1. **GET `/api/users`**
   - **Frontend call**: `api.get('/users')`
   - **Fungsi**: Mengambil seluruh user di database (hanya menyaring kolom `id`, `username`, `role`, `createdAt`; kolom password tidak dikirim ke frontend demi keamanan).
2. **POST `/api/users`**
   - **Frontend call**: `api.post('/users')`
   - **Fungsi**: Membuat akun user baru. Backend melakukan hash password menggunakan `bcrypt.hash(password, 10)`. Jika role tidak dideklarasikan, backend otomatis menetapkan default role ke `'CS'`.
3. **DELETE `/api/users/:id`**
   - **Frontend call**: `api.delete('/users/' + id)`
   - **Fungsi**: Menghapus user berdasarkan ID dari database.

*Catatan Fungsional Backend*:
Terdapat endpoint `PATCH /api/users/profile` (mengaktifkan fungsi `updateProfile` di controller) yang diproteksi `authenticateToken`, namun ini digunakan untuk memperbarui profil user yang sedang login saat itu (sesi aktif), bukan untuk memanipulasi profil staff lain secara administratif dari halaman F04.

## 6. Database Area
Prisma Client memetakan model **`User`** pada database SQLite dengan field berikut:
- `id` (Int, Primary Key, autoincrement)
- `username` (String, unique)
- `password` (String, terenkripsi bcrypt)
- `role` (String, bernilai `"ADMIN"` atau `"CS"`)
- `createdAt` (DateTime, default now)
- `updatedAt` (DateTime, auto-update)
- Relasi `transactions` (one-to-many ke model `Transaction`)

*Catatan Database*:
- Model data staff disatukan langsung pada model `User` (tidak ada model `Staff` terpisah).
- Kolom `role` disimpan sebagai string biasa tanpa enum bawaan database Prisma.
- Tidak terdapat kolom seperti `isActive`, `status`, `shift`, `payroll`, `attendance`, maupun field hak akses granular.

## 7. Alur Kerja Fitur
1. Admin membuka halaman `/admin/staff`.
2. Komponen memicu panggilan API `GET /api/users` dengan header token JWT.
3. Controller Express mengambil koleksi user dari SQLite, mengecualikan hash password, dan mengirim kembali array user dalam format JSON.
4. Komponen merender baris data user dan menghitung total jumlah staf di badge counter.
5. Admin dapat mendaftarkan staf baru melalui modal input form yang mengirim data ke `POST /api/users` untuk di-hash dan disimpan.
6. Admin dapat menghapus staf dengan menekan tombol hapus (ikon Trash2) yang memicu `DELETE /api/users/:id`.

## 8. Batasan Role & Security
- **Middleware Rute Klien**:
  - Rute `/admin/staff` dilindungi Next.js middleware, memastikan cookie `tb_token` valid dan cookie `tb_role` bernilai `'ADMIN'`. Jika dilanggar, user dialihkan ke `/login`.
- **Keamanan Rute Backend**:
  - Seluruh rute administratif F04 (`GET /api/users`, `POST /api/users`, `DELETE /api/users/:id`) diproteksi ketat menggunakan middleware gabungan `authenticateToken` dan `isAdmin` (berasal dari `authorizeRole(['ADMIN'])`).

## 9. Catatan Integrasi
- **Relasi dengan F01 (Auth)**: F04 mengelola akun `User` yang digunakan langsung oleh sistem login. Sukses autentikasi F01 menghasilkan JWT yang memuat klaim ID, username, dan role dari record User ini.
- **Relasi dengan Transaksi (Cashier)**: Record `User` yang dibuat melalui F04 bertindak sebagai kasir/operator pada data transaksi (`Transaction.cashierId`). Saat transaksi dibuat di POS, ID pengguna aktif disimpan sebagai `cashierId`. Saat memuat data riwayat, backend menyertakan nama kasir via join `cashier.username`.

## 10. Risiko / Catatan Perbaikan
- **Integritas Penghapusan (Foreign Key Constraint)**: Tidak ada handling database atau logic khusus di `deleteUser` untuk mencegah penghapusan user yang sudah memiliki keterikatan data transaksi (`Transaction`). Menghapus kasir aktif dapat merusak integritas relasi foreign key pada riwayat transaksi penjualan.
- **Batasan Administrasi**: F04 belum menyediakan fitur edit data staf umum secara administratif oleh Admin, reset password staff dari panel Admin, maupun status pembekuan akun (tidak ada field `isActive` / status keaktifan user).
- **Service Layer**: Logika manajemen user diproses langsung di dalam modul controller `userController.ts` tanpa abstraksi service terpisah.

## 11. Out of Scope
- Tidak menyediakan fitur edit data staf umum oleh Admin.
- Tidak menyediakan fitur reset password staf oleh Admin.
- Tidak menyediakan fitur membekukan/mengaktifkan akun (activate/deactivate user).
- Tidak menyediakan fitur HR (absensi/attendance, daftar gaji/payroll, jadwal shift, dsb.).
- Tidak memiliki pengelolaan permission granular di luar role ADMIN dan CS.
- Tidak menggunakan model database `Staff` terpisah.

## 12. Unknown / Belum Terverifikasi
- Belum diverifikasi perilaku sistem (behavior) jika Admin mencoba menghapus akun user yang telah terikat dengan transaksi penjualan di database SQLite.

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
