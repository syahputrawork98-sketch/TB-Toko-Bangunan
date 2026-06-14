# F01 - Authentication & Role-Based Access

## 1. Status Fitur
Status:
- Existing / Partial

Keterangan:
- Sistem login, manajemen state sesi di sisi klien, dan pembatasan rute backend/frontend berdasarkan peran (ADMIN dan CS) telah diimplementasikan namun verifikasi menyeluruh untuk integrasi multi-sesi (seperti token invalidasi di multi-browser) masih berstatus partial.

## 2. Tujuan Fitur
Menyediakan mekanisme login yang aman untuk membedakan hak akses halaman dasbor ADMIN (`/admin/*`) dan halaman kasir CS (`/cs/*`), serta menjamin proteksi data API backend melalui JWT token.

## 3. File / Path Evidence
Frontend:
- [client/src/middleware.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/client/src/middleware.ts) - Mengatur proteksi rute Next.js berdasarkan cookie peran dan token.
- [client/src/store/authStore.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/client/src/store/authStore.ts) - Manajemen state login client (Zustand) dan sinkronisasi cookie.
- [client/src/utils/api.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/client/src/utils/api.ts) - Axios interceptor untuk menyuntikkan header Authorization JWT dan memicu redirect ke `/login` jika error 401.

Backend/API:
- [server/src/routes/authRoutes.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/server/src/routes/authRoutes.ts) - Rute API autentikasi POST `/login`.
- [server/src/controllers/authController.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/server/src/controllers/authController.ts) - Logika otentikasi login, komparasi bcrypt password hash, dan pembuatan token JWT.
- [server/src/middlewares/authMiddleware.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/server/src/middlewares/authMiddleware.ts) - Middleware otentikasi Express (`authenticateToken`, `isAdmin`, `isCS`).

Database:
- [server/prisma/schema.prisma](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/server/prisma/schema.prisma) - Model `User` yang menampung kolom `id`, `username`, `password`, dan `role`.
- [server/prisma/seed.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/server/prisma/seed.ts) - Akun seeder default (`admin`/`admin123` dengan role `ADMIN`, dan `cs`/`cs123` dengan role `CS`).

## 4. UI / Frontend Area
- **Halaman Login (`/login`)**: UI input username dan password yang memicu `useAuthStore.getState().setAuth` setelah sukses dari backend API.
- **Rute Admin (`/admin/*`)**: Hanya dapat diakses bila cookie `tb_role` bernilai `ADMIN` dan cookie `tb_token` terdefinisi.
- **Rute CS (`/cs/*`)**: Hanya dapat diakses bila cookie `tb_role` bernilai `CS` dan cookie `tb_token` terdefinisi.

## 5. API / Backend Area
API Autentikasi:
- **Method**: `POST`
- **Path**: `/api/auth/login`
- **Request data**: `{ username, password }`
- **Response data**: `{ message: 'Login successful', token: string, user: { id: number, username: string, role: string } }`
- **File sumber**: `server/src/controllers/authController.ts`

## 6. Database Area
- **Tabel `User`**:
  - Kolom `id` (Primary Key, autoincrement)
  - Kolom `username` (String, unique)
  - Kolom `password` (String, terenkripsi bcrypt)
  - Kolom `role` (String, bernilai `"ADMIN"` atau `"CS"`)
  - Relasi `transactions` (one-to-many ke model `Transaction`)

## 7. Alur Kerja Fitur
1. User memasukkan username dan password di halaman `/login` frontend.
2. Frontend mengirim permintaan `POST /api/auth/login` ke backend.
3. Backend memeriksa keberadaan user di database SQLite melalui Prisma, mencocokkan password menggunakan `bcrypt.compare`, dan menandatangani JWT dengan rahasia `JWT_SECRET` (default ke `'supersecret'`) dengan masa berlaku 1 hari (`1d`).
4. Backend mengembalikan detail user dan string token ke klien.
5. Zustand store di sisi klien menyimpan detail user dan token di localStorage (`tb-auth-storage`), serta menyetel cookie `tb_token` dan `tb_role` (durasi 1 hari, path `/`) agar terbaca oleh middleware Next.js.
6. Middleware Next.js mengarahkan user secara otomatis berdasarkan peran (`ADMIN` ke `/admin/analytics`, `CS` ke `/cs/pos`).
7. Saat logout, Zustand store menghapus status login, menghapus cookie `tb_token` dan `tb_role`, membersihkan localStorage, dan mengalihkan halaman browser ke `/login`.

## 8. Batasan Role & Security
- **Next.js Middleware Guard**:
  - `pathname === '/'` mengarahkan user terotentikasi ke halaman dasbor yang sesuai atau melempar user tidak terotentikasi ke `/login`.
  - Halaman `/admin/*` tidak dapat diakses jika token tidak valid/kosong, atau peran bukan `ADMIN`.
  - Halaman `/cs/*` tidak dapat diakses jika token tidak valid/kosong, atau peran bukan `CS`.
- **Backend Middleware Guard**:
  - `authenticateToken` memverifikasi token JWT di header `Authorization: Bearer <token>`.
  - `isAdmin` (membatasi hak akses untuk role `ADMIN` saja).
  - `isCS` (membatasi hak akses untuk role `CS` saja).

## 9. Catatan Integrasi
- Request API yang dikirim melalui Axios helper `client/src/utils/api.ts` secara otomatis menyematkan header `Authorization: Bearer <token>` kecuali untuk endpoint `/auth/login`.
- Jika backend merespon dengan status `401 Unauthorized`, interceptor Axios di frontend akan otomatis menghapus sesi lokal (cookie & localStorage) dan me-redirect browser ke `/login`.

## 10. Risiko / Catatan Perbaikan
- **Penyimpanan Token**: Saat ini token JWT disimpan di cookie client-side biasa (`js-cookie`) dan Zustand persist localStorage agar terbaca middleware. Hal ini lebih rentan terhadap serangan XSS dibandingkan HTTP-only cookie.
- **Invalidation**: Token JWT tidak disimpan/di-blacklist di database saat logout, sehingga token lama masih valid di sisi server hingga masa kedaluwarsa 1 hari tercapai jika didekripsi secara mandiri tanpa cek state logout.
- **Keamanan JWT Secret**: Variabel lingkungan `JWT_SECRET` memiliki fallback string `'supersecret'` yang tertulis keras (hardcoded), perlu dipastikan didefinisikan secara aman di production env.

## 11. Out of Scope
- Tidak mengubah algoritma enkripsi password (tetap bcrypt).
- Tidak memodifikasi Next.js middleware atau store Zustand.
- Tidak menambahkan endpoint registrasi user baru atau fitur lupa password.
- Tidak memodifikasi middleware role-based di server backend.

## 12. Unknown / Belum Terverifikasi
- Kebijakan token refresh (token rotasi) belum diimplementasikan atau diverifikasi.
- Integrasi CORS penuh di deployment stage non-lokal belum diverifikasi.

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
