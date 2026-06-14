# F00 - Existing Project Zero Point

## 1. Status Fitur
Status:
- Existing / Baseline

Keterangan:
- Halaman baseline fungsional sistem pasca konsolidasi monorepo dengan folder `client/` dan `server/`.

## 2. Tujuan Fitur
Menjadi titik awal (zero-point baseline) pencatatan status fungsional dan arsitektur repositori terpadu `TB-Toko-Bangunan` pasca pemindahan kode.

## 3. File / Path Evidence
Frontend:
- `client/src/app/page.tsx`
- `client/package.json`

Backend/API:
- `server/src/app.ts`
- `server/package.json`

Database:
- `server/prisma/schema.prisma`

Integration/Helper:
- `client/src/utils/api.ts`

## 4. UI / Frontend Area
- Halaman pendaratan dasar Next.js di rute `/` yang dikontrol oleh `client/src/app/page.tsx`.

## 5. API / Backend Area
API Dasar Backend:
- Method: `GET`
- Path/function: `/`
- Request data: None
- Response data: `{ message: string, status: string, version: string }`
- File sumber: `server/src/app.ts`

## 6. Database Area
Seluruh skema Prisma relasional di `server/prisma/schema.prisma` yang mencakup model `User`, `Product`, `Transaction`, `TransactionItem`, dan `Setting`.

## 7. Alur Kerja Fitur
1. User menjalankan backend server lokal di port 5000 dan frontend di port 3000.
2. Sistem server menerima request dasar `GET /` untuk verifikasi status backend.
3. User membuka halaman root `/` di browser.
4. Sistem frontend memeriksa status login melalui middleware.
5. Output akhir diarahkan ke halaman login `/login` atau dashboard yang sesuai.

## 8. Batasan Role & Security
- Halaman root `/` dilindungi oleh `client/src/middleware.ts` yang mendeteksi cookie token. Jika tidak memiliki token, user dilempar ke `/login`.

## 9. Catatan Integrasi
Terintegrasi secara langsung dengan middleware Next.js (`client/src/middleware.ts`) dan status verifikasi server backend.

## 10. Risiko / Catatan Perbaikan
- Pengujian cross-origin CORS diset allow-all (`origin: true`) pada server Express untuk mempermudah dev, perlu diperketat saat production.

## 11. Out of Scope
- Tidak membuat fitur baru.
- Tidak refactor kode.
- Tidak mengubah logic frontend/backend.
- Tidak mengubah database.
- Tidak menambah endpoint.
- Tidak memperbaiki bug.
- Tidak mengisi berdasarkan asumsi.

## 12. Unknown / Belum Terverifikasi
- Konfigurasi deployment produksi VPS atau PM2 belum diverifikasi pada tahap ini.

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
