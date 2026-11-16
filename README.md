# Halaman publik SiMPATI (GitHub Pages)

Tiga halaman statis tanpa dependensi:

| Berkas | Kegunaan di App Store Connect |
| --- | --- |
| `index.html` | halaman root (pengantar) |
| `support.html` | **Support URL** (wajib) |
| `privacy.html` | **Privacy Policy URL** (wajib) |

## Sebelum publikasi

Ganti dua placeholder di semua berkas:

- `{{NAMA_INSTITUSI}}` → nama resmi institusi
- `{{EMAIL_DUKUNGAN}}` → email bantuan yang aktif

```powershell
(Get-ChildItem site\*.html) | ForEach-Object {
  (Get-Content $_.FullName -Raw) -replace '\{\{NAMA_INSTITUSI\}\}', 'Politeknik Imigrasi' `
    -replace '\{\{EMAIL_DUKUNGAN\}\}', 'alamat@email.aktif' | Set-Content $_.FullName -NoNewline
}
```

## Publikasi

Repo `sipena` bersifat **private**, sehingga GitHub Pages hanya tersedia pada paket GitHub Pro/Team/Enterprise.
Dua jalur:

### A. Pages dari repo ini (butuh Pro)

1. Repo → Settings → Pages → Source: **GitHub Actions**.
2. Tab **Actions** → *Deploy halaman publik SiMPATI* → **Run workflow** (workflow memakai `workflow_dispatch` agar tidak gagal otomatis bila Pages belum aktif).
3. URL: `https://<akun>.github.io/sipena/support.html` dan `.../privacy.html`.

Bila Pages sudah aktif dan ingin terbit otomatis setiap push, buka `.github/workflows/pages.yml` dan aktifkan blok `push:` yang sudah disiapkan di komentar.

### B. Repo publik terpisah (gratis)

1. Buat repo publik baru, mis. `simpati-pages`.
2. Terbitkan hanya folder `site/`:

```powershell
git subtree push --prefix site https://github.com/<akun>/simpati-pages.git main
```

3. Di repo baru: Settings → Pages → Source: **Deploy from a branch** → `main` / `/ (root)`.
4. URL: `https://<akun>.github.io/simpati-pages/support.html` dan `.../privacy.html`.

Kedua URL bisa diganti kapan saja di App Store Connect tanpa submit ulang.
