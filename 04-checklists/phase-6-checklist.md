# 📋 Checklist Fase 6: Penyelesaian & Deployment Mastery (Hari 29–30)

[← Kembali ke Dashboard Progres](daily-progress-tracker.md) | [📑 Daftar Silabus](../README.md)

---

## 📌 Hari 29: Testing dan Security Review
- [ ] Lakukan pengujian akhir dari sudut pandang pengguna nyata (*end-to-end testing* sederhana)
- [ ] Periksa penanganan error (*error boundary* & pesan error yang ramah pengguna)
- [ ] Audit keamanan: pastikan tidak ada *hardcoded secret* atau kata sandi di dalam kode repository
- [ ] Periksa loading state, empty state (katalog kosong), dan penanganan tombol saat proses *submit*

## 📌 Hari 30: Refactoring Final & Dokumentasi README
- [ ] Lakukan pembersihan kode: hapus `console.log` sensitif dan impor yang tidak terpakai
- [ ] Pecah function yang terlalu panjang (>50 baris) dan hapus kode JSX/logic yang duplikatif
- [ ] Lengkapi file `README.md` dengan deskripsi proyek, fitur, stack, instruksi instalasi lokal, dan arsitektur

## 📌 Hari 30 (Langkah 1): Deploy ke Vercel (PaaS / Serverless)
- [ ] Siapkan database PostgreSQL di cloud (Neon / Supabase / Aiven) dengan format SSL (`?sslmode=require`)
- [ ] Jalankan migrasi Drizzle (`npx drizzle-kit migrate`) dan seeder admin ke database cloud tersebut
- [ ] Hubungkan repository GitHub proyek Mini POS ke dasbor Vercel
- [ ] Konfigurasi *Environment Variables* di Vercel (`DATABASE_URL`, `NEXTAUTH_SECRET`, `NEXTAUTH_URL`)
- [ ] Lakukan deploy dan verifikasi bahwa transaksi kasir memotong stok di database cloud dengan benar

## 📌 Hari 30 (Langkah 2): Deploy Manual ke VPS (Ubuntu, Nginx, PM2 & SSL)
- [ ] Provisioning VPS Linux (Ubuntu 22.04/24.04 LTS) dan setup firewall UFW (Port 22, 80, 443)
- [ ] Instal Node.js v20+ LTS via NVM dan Git di dalam server VPS
- [ ] Clone repository, buat file `.env.production`, dan build aplikasi (`npm run build`)
- [ ] Instal **PM2** Process Manager (`npm i -g pm2`), jalankan aplikasi, dan konfigurasi auto-restart (`pm2 startup`)
- [ ] Instal dan konfigurasi **Nginx** sebagai *reverse proxy* yang meneruskan port 80 ke `http://127.0.0.1:3000`
- [ ] Instal **Certbot (Let's Encrypt)** dan aktifkan enkripsi HTTPS otomatis (`certbot --nginx -d domainanda.com`)

## 📌 Hari 30 (Langkah 3): Deploy ke VPS Menggunakan Docker (Masterclass Containerization)
- [ ] Pahami konsep fundamental Docker: perbedaan Container vs Virtual Machine (VM) dan keunggulan isolasi
- [ ] Pahami konsep **Multi-Stage Build** pada Dockerfile untuk memangkas image Next.js dari >1.5GB menjadi ~100MB
- [ ] Instal Docker Engine dan Docker Compose di server VPS Ubuntu
- [ ] Aktifkan mode `output: 'standalone'` pada file `next.config.ts` di proyek Anda
- [ ] Buat `Dockerfile` produksi 4-stage (`base`, `deps`, `builder`, `runner`) dengan user non-root (`nextjs`)
- [ ] Buat `docker-compose.yml` untuk mengatur kontainer `web` (Next.js), `postgres` (DB persistent), dan `nginx`
- [ ] Jalankan sistem dengan perintah `docker compose up -d --build` dan eksekusi migrasi Drizzle di dalam kontainer!

---
[← Kembali ke Dashboard Progres](daily-progress-tracker.md)
