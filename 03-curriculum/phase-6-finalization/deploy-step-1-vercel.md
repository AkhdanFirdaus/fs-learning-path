# 🚀 Langkah 1: Deployment ke Vercel (PaaS / Serverless)

**Vercel** adalah platform pencipta Next.js dan merupakan standar industri untuk deployment aplikasi Next.js secara *serverless* dan *zero-configuration*.

---

## 🎯 Mengapa Deploy ke Vercel?
1. **Zero-Config CI/CD:** Setiap kali Anda melakukan *push* ke branch `main` di GitHub, Vercel secara otomatis membangun (*build*) dan merilis aplikasi Anda dalam hitungan detik.
2. **Global Edge Network:** Konten statis (HTML, CSS, JS, Image) didistribusikan ke CDN global, sementara Server Components dan Route Handlers dijalankan sebagai Serverless Functions yang skalabel.
3. **Preview Deployments:** Setiap Pull Request (PR) mendapatkan URL live tersendiri untuk pengujian sebelum digabungkan ke production.

---

## 📋 Prasyarat
- Akun GitHub dengan repository proyek **Mini POS** yang sudah di-push.
- Akun Vercel gratis ([https://vercel.com/signup](https://vercel.com/signup)).
- Database PostgreSQL cloud yang aktif dan dapat diakses publik dari cloud (misal: **Neon PostgreSQL**, **Supabase**, atau **Aiven**).

---

## 🛠️ Langkah-Langkah Deployment

### 1. Persiapan Database Cloud (Neon / Supabase)
Karena Vercel bersifat *serverless* (tidak menyimpan state database lokal), Anda wajib menggunakan cloud database:
1. Buat project baru di [Neon.tech](https://neon.tech) atau [Supabase.com](https://supabase.com).
2. Salin *Connection String* (`DATABASE_URL`). Pastikan menggunakan format koneksi SSL (biasanya diakhiri dengan `?sslmode=require`).
3. Dari terminal lokal Anda, jalankan migrasi Drizzle ke database cloud tersebut untuk membentuk tabel:
   ```bash
   DATABASE_URL="postgresql://user:pass@host.region.aws.neon.tech/dbname?sslmode=require" npx drizzle-kit migrate
   ```
4. Jalankan seeder untuk membuat akun admin awal:
   ```bash
   DATABASE_URL="postgresql://user:pass@host.region.aws.neon.tech/dbname?sslmode=require" npx tsx src/db/seed.ts
   ```

### 2. Import Project ke Vercel Dashboard
1. Login ke [Vercel Dashboard](https://vercel.com/dashboard).
2. Klik tombol **"Add New..."** -> **"Project"**.
3. Hubungkan akun GitHub Anda dan pilih repository `mini-pos` (atau nama repositori Anda).
4. Klik **"Import"**.

### 3. Konfigurasi Environment Variables di Vercel
Pada halaman *Configure Project*, buka dropdown **Environment Variables** dan masukkan seluruh variabel yang dibutuhkan aplikasi:

| Key | Example Value | Deskripsi |
| :--- | :--- | :--- |
| `DATABASE_URL` | `postgresql://user:pass@...neon.tech/dbname?sslmode=require` | Koneksi database PostgreSQL Cloud |
| `NEXTAUTH_SECRET` | `a8f9d0e1b2c3...` (string acak panjang) | Kunci enkripsi sesi untuk Auth / JWT |
| `NEXTAUTH_URL` | `https://mini-pos-pro.vercel.app` | URL production aplikasi Anda |
| `NODE_ENV` | `production` | Mode lingkungan eksekusi |

### 4. Build & Deploy
1. Biarkan *Build Command* default (`next build`) dan *Output Directory* default (`.next`).
2. Klik tombol **"Deploy"**.
3. Tunggu 1–2 menit hingga animasi konfeti muncul! Aplikasi Anda kini live di URL Vercel (contoh: `https://mini-pos-xxx.vercel.app`).

---

## 🔍 Verifikasi Pasca-Deployment
- [ ] **Login Admin:** Buka halaman login di URL live dan coba masuk menggunakan akun admin hasil seeding.
- [ ] **Test Mutasi Data:** Coba tambahkan produk baru atau lakukan penyesuaian stok.
- [ ] **Test Transaksi Kasir:** Lakukan transaksi pembelian dan pastikan stok di database cloud benar-benar berkurang.

---

## 💡 Tips & Gotchas di Vercel
* **Connection Pooling:** Serverless functions di Vercel dapat membuat ribuan koneksi simultan saat traffic tinggi. Gunakan connection pooler dari Neon atau Supabase (biasanya port `6543` pada Supabase) agar database tidak mengalami *too many clients error*.
* **File Uploads:** Karena sistem file serverless bersifat *read-only* saat runtime, jika Anda memiliki fitur upload gambar produk, gunakan penyimpanan cloud eksternal seperti **Cloudinary**, **AWS S3**, atau **Vercel Blob Storage**.

---

[← Kembali ke Hari 30](./day-30-refactoring-deploy.md) | [📑 Daftar Silabus](../../README.md) | [Lanjut ke Langkah 2: Deploy Manual VPS →](./deploy-step-2-manual-vps.md)
