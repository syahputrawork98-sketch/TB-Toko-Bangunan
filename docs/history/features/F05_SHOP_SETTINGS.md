# F05 - Shop Settings

## 1. Status Fitur
Status:
- Existing / Implemented

Keterangan:
- Sistem pengaturan global untuk konfigurasi identitas toko dan ambang batas stok tipis (`lowStockThreshold`). Menu "Settings" tersedia bagi peran Admin (akses edit penuh di `/admin/settings`) dan CS (akses informasi toko read-only di `/cs/settings`).

## 2. Tujuan Fitur
Menyediakan mekanisme bagi Admin untuk memperbarui data identitas fisik toko (nama, alamat, nomor telepon) serta ambang batas stok tipis global (`lowStockThreshold`) yang dimanfaatkan oleh backend analytics untuk memantau inventaris kritis pada dashboard Admin dan kasir.

## 3. File / Path Evidence
Frontend:
- [client/src/app/(dashboard)/admin/settings/page.tsx](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/client/src/app/(dashboard)/admin/settings/page.tsx) - Halaman antarmuka manajemen pengaturan bagi Admin (CRUD settings).
- [client/src/app/(dashboard)/cs/settings/page.tsx](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/client/src/app/(dashboard)/cs/settings/page.tsx) - Halaman antarmuka bagi CS yang menampilkan profil toko secara read-only.
- [client/src/components/layout/Sidebar/Sidebar.tsx](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/client/src/components/layout/Sidebar/Sidebar.tsx) - Menu samping untuk navigasi ke rute `/admin/settings` atau `/cs/settings` sesuai peran pengguna.
- [client/src/utils/api.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/client/src/utils/api.ts) - Axios API client dengan konfigurasi base URL dan interseptor Bearer token JWT.
- [client/src/store/authStore.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/client/src/store/authStore.ts) - Penyimpan status autentikasi lokal dan pembuat cookie.
- [client/src/middleware.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/client/src/middleware.ts) - Proteksi rute halaman `/admin` dan `/cs`.

Backend/API:
- [server/src/app.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/server/src/app.ts) - Registrasi route root `/api/settings`.
- [server/src/routes/settingRoutes.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/server/src/routes/settingRoutes.ts) - Rute Express untuk mengambil (GET) dan memperbarui (PATCH) pengaturan global toko.
- [server/src/controllers/settingController.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/server/src/controllers/settingController.ts) - Logika kendali untuk membaca database setting atau membuat default setting jika record kosong.
- [server/src/middlewares/authMiddleware.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/server/src/middlewares/authMiddleware.ts) - Middleware otentikasi Express (`authenticateToken`, `isAdmin`).

Database:
- [server/prisma/schema.prisma](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/server/prisma/schema.prisma) - Model `Setting` untuk menyimpan record konfigurasi.
- [server/prisma/seed.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/server/prisma/seed.ts) - Inisialisasi awal record setting dengan ID 1 menggunakan metode upsert.

Integrasi Analytics:
- [server/src/controllers/analyticsController.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/server/src/controllers/analyticsController.ts) - Penggunaan kolom `lowStockThreshold` untuk memfilter stok kritis pada dashboard Admin & CS.

## 4. UI / Frontend Area
- **Navigasi Sidebar**: Menu "Settings" mengarah secara dinamis ke `/admin/settings` (Admin) atau `/cs/settings` (CS).
- **Antarmuka Admin Settings (`/admin/settings`)**:
  - Memiliki 3 tab: **Profil Toko**, **Sistem Kasir**, dan **Keamanan Akun**.
  - **Profil Toko**: Input form Nama Toko, Alamat Lengkap, dan Nomor Telepon. Melakukan submit ke `PATCH /settings`.
  - **Sistem Kasir**: Input form Ambang Batas Stok Rendah (`lowStockThreshold`).
  - **Keamanan Akun**: Form untuk memperbarui username dan password pribadi Admin aktif. Ini berinteraksi dengan rute `/users/profile` (integrasi dengan F01 Auth/Profile, bukan inti F05).
- **Antarmuka CS Settings (`/cs/settings`)**:
  - Memiliki 2 tab: **Keamanan Akun** (update profil/password kasir via `/users/profile`) dan **Informasi Toko**.
  - **Informasi Toko**: Menampilkan Nama Toko, Alamat Lengkap, dan Nomor Telepon secara dinonaktifkan (disabled/read-only) dengan catatan: *"Hanya Admin yang dapat mengubah informasi profil toko."*
- **State Manajemen**: Komponen UI mengelola state `shopName`, `shopAddress`, `shopPhone`, dan `lowStockThreshold` menggunakan state React local.
- **Komponen Pendukung**: Button, Input, CSS module, useAuthStore, serta ikon dari `lucide-react` (`Building2`, `Settings`, `ShieldCheck`, `AlertTriangle`).

## 5. API / Backend Area
API client mengirim JWT bearer token dari cookie `tb_token` pada header Request. Rute API didaftarkan pada `/api/settings` dengan rincian:
1. **GET `/api/settings`**
   - **Otorisasi**: `authenticateToken` (dapat diakses oleh Admin maupun CS).
   - **Fungsi**: Mengambil record Setting dengan ID 1. Jika record belum ada di database, controller secara otomatis membuat baris data default:
     - `shopName`: `'Toko Bangunan (TB)'`
     - `shopAddress`: `'Jl. Raya Industri No. 1'`
     - `shopPhone`: `'0812-3456-7890'`
     - `lowStockThreshold`: `10`
2. **PATCH `/api/settings`**
   - **Otorisasi**: `authenticateToken` + `isAdmin` (hanya dapat dieksekusi oleh Admin).
   - **Fungsi**: Memperbarui kolom data setting (`shopName`, `shopAddress`, `shopPhone`, `lowStockThreshold`). Angka `lowStockThreshold` otomatis dikonversi backend menjadi tipe data Number.

## 6. Database Area
Model **`Setting`** didefinisikan pada skema Prisma SQLite dengan detail:
- `id` (Int, Primary Key, default: 1)
- `shopName` (String, default: "Toko Bangunan (TB)")
- `shopAddress` (String, default: "Jl. Raya Industri No. 1")
- `shopPhone` (String, default: "0812-3456-7890")
- `lowStockThreshold` (Int, default: 10)
- `updatedAt` (DateTime, auto-update)

*Konteks Database & Seeder*:
- Seeder (`seed.ts`) menginisialisasi tabel Setting dengan ID 1.
- Terdapat perbedaan default text alamat antara schema/controller (`"Jl. Raya Industri No. 1"`) dengan seeder (`"Jl. Raya Industri No. 1, Jakarta"`). Ini dicatat sebagai perbedaan data baseline di kode existing.

## 7. Alur Kerja Fitur
1. Pengguna membuka menu Settings di sidebar (mengarahkan ke `/admin/settings` atau `/cs/settings`).
2. Komponen frontend memicu panggilan `GET /api/settings` untuk memuat data profil toko.
3. Di server, `settingController.getSettings` mencari record ID 1 di SQLite. Jika kosong, record default dibuat otomatis. Server mengembalikan JSON setting.
4. Di frontend Admin, data mengisi input form Profil Toko dan Sistem Kasir. Admin dapat mengedit field lalu menekan submit untuk mengirim permintaan `PATCH /api/settings`.
5. Di frontend CS, data dirender sebagai teks atau input disabled (read-only) sehingga CS tidak dapat mengubahnya.
6. Admin dan CS dapat berpindah ke tab Keamanan Akun untuk mengubah detail username/password pribadi, yang mengirim data ke `/api/users/profile`.

## 8. Batasan Role & Security
- **Otorisasi Klien**:
  - Halaman `/admin/settings` dilindungi middleware Next.js agar hanya peran `ADMIN` yang dapat mengakses. Halaman `/cs/settings` hanya untuk peran `CS`.
- **Otorisasi Backend**:
  - Mutasi konfigurasi global (`PATCH /api/settings`) dibatasi keras untuk peran Admin saja (`authenticateToken` + `isAdmin`). Permintaan dari CS akan diblokir dengan status `403 Forbidden`.

## 9. Catatan Integrasi
- **Relasi dengan F01 (Auth/Profile)**: Membaca hak akses navigasi dan token JWT. Menu "Keamanan Akun" yang berada di halaman settings sebenarnya terintegrasi langsung dengan rute profil pengguna (`/api/users/profile`), bukan bagian dari model setting toko.
- **Relasi dengan F02 (Analytics)**: Ambang batas stok rendah (`lowStockThreshold`) yang dikonfigurasi di F05 digunakan secara langsung oleh controller analitik backend untuk menghitung total produk stok rendah (`lowStockItems`) pada dasbor analitik Admin (`getSummary`) dan statistik dasbor kasir CS (`getCSDashboardStats`).
- **Integrasi POS/Receipt**: Antarmuka Admin Settings menyatakan bahwa informasi toko disiapkan untuk tercetak pada kop struk belanja POS. Namun, pada implementasi kode POS existing, integrasi cetak data toko ke struk ini belum ditemukan/terverifikasi.

## 10. Risiko / Catatan Perbaikan
- **Integrasi POS Terputus**: Meskipun UI menyatakan Nama/Alamat Toko akan tercetak di struk belanja kasir, kode pencetakan struk existing belum memanfaatkan model Setting ini.
- **Perbedaan Default Data**: Perbedaan string alamat default antara script seeder dan handler controller Express (penambahan kata ", Jakarta" di seeder).
- **Minimal Validasi**: Backend settings belum memvalidasi format nomor telepon atau batasan angka threshold minimum, melainkan langsung melakukan penyimpanan dan konversi parser ke Number.
- **Domain Keamanan Akun**: Form pembaruan akun pribadi diletakkan di halaman settings, yang secara arsitektur domain lebih dekat ke lingkup otorisasi F01.
- **Service Layer**: Logika settings diproses langsung pada modul `settingController.ts` tanpa menggunakan service layer.

## 11. Out of Scope
- Tidak menyediakan fitur unggah gambar logo toko (tidak ada field database logo).
- Tidak mendukung konfigurasi toko multi-cabang (model Setting didesain single record ID 1).
- Tidak menyediakan pengaturan pajak (tax config), konfigurasi printer, atau metode pembayaran.
- Tidak menyediakan fitur penyesuaian footer struk belanja secara kustom (custom receipt footer).

## 12. Unknown / Belum Terverifikasi
- Penerapan dinamis data Setting (Nama Toko, Alamat, Telepon) pada output struk cetak POS kasir belum terverifikasi di kode existing.

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
