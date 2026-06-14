# F10 - Developer Suite: Persona Account Login

## 1. Status Fitur
Status:
- Existing / Implemented

Keterangan:
- Panel bantuan developer untuk login cepat (persona login) menggunakan akun seeder default (`admin` dan `cs`) yang hanya muncul pada mode *development* di halaman `/login` frontend Next.js.

## 2. Tujuan Fitur
Mempercepat proses pengembangan dan pengujian multi-role di tingkat lokal dengan menyediakan tombol login sekali klik untuk Admin Persona dan CS Persona, tanpa mem-bypass proses autentikasi server backend.

## 3. File / Path Evidence
Frontend:
- [client/src/app/(auth)/login/page.tsx](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/client/src/app/(auth)/login/page.tsx) - Halaman login yang memuat tombol "Developer Suite" dan fungsi pemicu login cepat `handleDevLogin`.
- [client/src/app/(auth)/login/login.module.css](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/client/src/app/(auth)/login/login.module.css) - Styling untuk area "DEVELOPER SUITE" dan tombol persona.

Backend/API:
- [server/src/routes/authRoutes.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/server/src/routes/authRoutes.ts) - Menggunakan route autentikasi POST `/login` existing.

Database:
- [server/prisma/seed.ts](file:///i:/Workspace/Workspace-Syahputrawork/TB-Toko-Bangunan/server/prisma/seed.ts) - Memanfaatkan akun seed default (`admin` / `admin123` dan `cs` / `cs123`).

## 4. UI / Frontend Area
- **Tampilan Halaman `/login`**:
  - Di bawah tombol utama "ACCESS SYSTEM", terdapat divider bertuliskan "DEVELOPER SUITE" dengan visualisasi garis putus-putus.
  - Terdapat dua tombol:
    - **🔑 Admin Persona**: Memicu login instan sebagai `admin` / `admin123`.
    - **🔑 CS Persona**: Memicu login instan sebagai `cs` / `cs123`.
- **Kondisional Visibilitas**:
  - Hanya merender panel Developer Suite jika `process.env.NODE_ENV === 'development'` bernilai `true` ATAU flag lingkungan `process.env.NEXT_PUBLIC_ENABLE_DEV_PERSONA_LOGIN === 'true'` aktif.

## 5. API / Backend Area
- Tidak membuat endpoint baru. Fitur ini memanfaatkan API login standar:
  - **Method**: `POST`
  - **Path**: `/api/auth/login`
  - **Request Body**: `{ username, password }`
  - **Response**: JWT token dan detail user (id, username, role).

## 6. Database Area
- Tidak ada perubahan skema database. Fitur ini bergantung pada data user di tabel `User` yang di-generate dari seeder (`seed.ts`):
  - Record User admin: `username: 'admin'`, password ter-hash dari `'admin123'`.
  - Record User cs: `username: 'cs'`, password ter-hash dari `'cs123'`.

## 7. Alur Kerja Fitur
1. Developer membuka halaman `/login`.
2. Next.js mengevaluasi mode env: jika mode *development* aktif, panel "DEVELOPER SUITE" dirender di bawah form.
3. Developer mengklik tombol "🔑 Admin Persona" atau "🔑 CS Persona".
4. Klik tombol memicu fungsi `handleDevLogin(username, password)`.
5. Fungsi memperbarui state input form, menampilkan status loading, dan mengirim permintaan HTTP POST ke `/api/auth/login`.
6. Server Express memverifikasi kredensial menggunakan SQLite dan mengembalikan JWT token.
7. Zustand store menyimpan sesi login, membuat cookie `tb_token` dan `tb_role` lokal, dan Next.js router melakukan pengalihan halaman secara otomatis sesuai role (Admin ke `/admin`, CS ke `/cs/pos`).

## 8. Batasan Role & Security
- **Proteksi Mode Produksi**:
  - Panel ini tidak akan dimuat pada rilis build produksi (`process.env.NODE_ENV === 'production'`) kecuali flag `process.env.NEXT_PUBLIC_ENABLE_DEV_PERSONA_LOGIN` diatur secara sengaja ke `'true'`.
- **Keamanan Kredensial**:
  - Kredensial yang digunakan adalah data seeder publik lokal dan tidak melibatkan rahasia kredensial produksi.
  - Alur otentikasi backend JWT dan middleware role guard tetap diproses 100% secara ketat tanpa bypass token.

## 9. Catatan Integrasi
- Terintegrasi langsung dengan helper API client Axios (`client/src/utils/api.ts`) dan Zustand Auth Store (`client/src/store/authStore.ts`).

## 10. Risiko / Catatan Perbaikan
- **Sifat Kredensial**: Tombol ini menaruh kredensial seeder secara keras (hardcoded) di frontend khusus mode pengujian dev. Jika file build produksi tidak di-minified/dikompresi dengan benar dan bendera flag dinonaktifkan secara salah, kredensial seeder lokal dapat dibaca di bundel JS klien, namun karena akun tersebut hanya ada di database lokal dev, risiko keamanan sistem live tetap rendah.

## 11. Out of Scope
- Registrasi user/staff baru dari layar login.
- Reset/pemulihan kata sandi.
- Modifikasi alur penandatanganan JWT token di server.
- Modifikasi skema basis data SQLite.

## 12. Unknown / Belum Terverifikasi
- Konfigurasi bundler Next.js optimasi produksi untuk pembuangan kode dev-only (tree shaking) belum diverifikasi secara mendalam.

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
