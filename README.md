# Partitur RNHKBP-PELIKAN

Website partitur PDF (GitHub Pages + Supabase + Google Drive).

Halaman: `index.html` (publik) dan `admin.html` (admin).

## 1. Supabase
1. **SQL Editor** → tempel isi `setup.sql` → Run.
2. **Authentication → Users → Add user** (centang Auto Confirm User) → buat akun admin pertama, lalu jalankan di SQL Editor:
   `insert into public.admins (user_id) select id from auth.users where email = 'emailmu@gmail.com';`
3. **Authentication → Sign In / Providers → Email**: matikan **Confirm email** agar akun yang dibuat dari panel admin langsung bisa dipakai.
4. **Authentication → URL Configuration**:
   - Site URL: `https://USERNAME.github.io/NAMA-REPO/`
   - Redirect URLs: tambahkan `https://USERNAME.github.io/NAMA-REPO/admin.html` (wajib untuk "Lupa kata sandi").

## 2. Google Drive
Buat folder di Drive untuk menyimpan PDF, buka folder itu, salin ID dari URL (`drive.google.com/drive/folders/ID_INI`).

## 3. Google Apps Script (upload foto → PDF → Drive)
1. Buka https://script.google.com → **New project** → hapus isi, tempel isi `Code.gs`.
2. Ganti `FOLDER_ID` dengan ID folder tadi.
3. **Deploy → New deployment → Web app**: *Execute as* **Me**, *Who has access* **Anyone** → Deploy → izinkan akses Drive.
4. Salin **Web app URL** (berakhiran `/exec`) dan tempel di `common.js` pada `APPS_SCRIPT_URL`.
   Jika kamu mengubah `Code.gs` lagi, buat **New version** di Manage deployments.

## 4. GitHub Pages
Unggah `index.html`, `admin.html`, `app.js`, `admin.js`, `common.js`, `style.css` ke root repository (hapus `admin-config.js` lama). Settings → Pages → Deploy from a branch → main → / (root).

## Catatan
- Notifikasi lagu baru: banner "partitur baru sejak kunjunganmu", label BARU (7 hari), serta pemberitahuan langsung (toast + notifikasi browser jika diizinkan) saat halaman sedang terbuka. Push saat situs ditutup membutuhkan layanan push terpisah.
- Menghapus partitur dari panel tidak menghapus file PDF di Google Drive.
- Email reset kata sandi memakai pengirim bawaan Supabase yang dibatasi beberapa email per jam. Untuk pemakaian ramai, pasang SMTP sendiri di Supabase.
- Hanya bagikan PDF yang hak distribusinya kamu miliki.
