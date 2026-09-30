# Genba 5R Map

Peta denah interaktif untuk closing temuan Genba 5R.
Frontend statis (GitHub Pages) + Google Apps Script & Spreadsheet sebagai backend/database.

```
index.html      Aplikasi (frontend)
config.js       API_URL & Google Client ID
backend/Code.gs Backend Apps Script
```

## 1. Backend (Apps Script)
1. Buat Google Spreadsheet baru → **Extensions → Apps Script**, tempel `backend/Code.gs`.
2. Jalankan fungsi `setup` sekali (membuat sheet & menjadikan Anda superadmin).
3. **Deploy → New deployment → Web app** — *Execute as: Me*, *Who has access: Anyone*.
   Salin URL `/exec` ke `config.js` (`API_URL`).
   > Setiap ubah `Code.gs`, deploy ulang via **Manage deployments → Edit → New version**.

## 2. Google Sign-In
1. Google Cloud Console → **APIs & Services → Credentials → Create OAuth client ID → Web application**.
2. *Authorized JavaScript origins*: `https://USERNAME.github.io` (dan `http://localhost:8080` untuk uji lokal).
3. Salin Client ID ke `config.js` **dan** ke konstanta `CLIENT_ID` di `Code.gs`, lalu deploy ulang.

## 3. GitHub
```bash
git init && git add . && git commit -m "Genba 5R Map"
git branch -M main
git remote add origin https://github.com/USERNAME/genba-5r-map.git
git push -u origin main
```
**Settings → Pages → Deploy from branch → main / (root)**.
Aplikasi tampil di `https://USERNAME.github.io/genba-5r-map/`.

## Peran & keamanan
Hanya email yang terdaftar di sheet **Users** (atau tab Master) yang bisa masuk:
`superadmin` (kelola master), `auditor` (catat temuan), `operator` (lihat & closing).
`config.js` aman dipublikasikan (Client ID & URL API memang publik); akses dijaga verifikasi token di backend.

Uji lokal: `python3 -m http.server 8080`
