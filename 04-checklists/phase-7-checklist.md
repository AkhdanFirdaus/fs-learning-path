# 📋 Checklist Fase Tambahan 1: Production Deployment Mastery (Hari 31–33)

[← Kembali ke Checklist Fase 6](phase-6-checklist.md) | [← Dashboard Progres](daily-progress-tracker.md) | [Lanjut ke Checklist Bonus 2 (GraphQL) →](phase-8-checklist.md)

---

## 📌 Hari 31: Deployment ke Vercel (PaaS / Serverless)
- [ ] Siapkan database PostgreSQL di cloud (Neon / Supabase / Aiven) dengan format SSL (`?sslmode=require`)
- [ ] Jalankan migrasi Drizzle (`npx drizzle-kit migrate`) dan seeder admin ke database cloud tersebut
- [ ] Hubungkan repository GitHub proyek Mini POS ke dasbor Vercel
- [ ] Konfigurasi *Environment Variables* di Vercel (`DATABASE_URL`, `NEXTAUTH_SECRET`, `NEXTAUTH_URL`)
- [ ] Lakukan deploy dan verifikasi bahwa transaksi kasir memotong stok di database cloud dengan benar

## 📌 Hari 32: Deployment Manual ke VPS (Ubuntu, Nginx, PM2 & SSL)
- [ ] Provisioning VPS Linux (Ubuntu 22.04/24.04 LTS) dan setup firewall UFW (Port 22, 80, 443)
- [ ] Instal Node.js v20+ LTS via NVM dan Git di dalam server VPS
- [ ] Clone repository, buat file `.env.production`, dan build aplikasi (`npm run build`)
- [ ] Instal **PM2** Process Manager (`npm i -g pm2`), jalankan aplikasi, dan konfigurasi auto-restart (`pm2 startup`)
- [ ] Instal dan konfigurasi **Nginx** sebagai *reverse proxy* yang meneruskan port 80 ke `http://127.0.0.1:3000`
- [ ] Instal **Certbot (Let's Encrypt)** dan aktifkan enkripsi HTTPS otomatis (`certbot --nginx -d domainanda.com`)

## 📌 Hari 33: Deployment ke VPS Menggunakan Docker (Masterclass Containerization)
- [ ] Pahami konsep fundamental Docker: perbedaan Container vs Virtual Machine (VM) dan keunggulan isolasi
- [ ] Pahami konsep **Multi-Stage Build** pada Dockerfile untuk memangkas image Next.js dari >1.5GB menjadi ~100MB
- [ ] Instal Docker Engine dan Docker Compose di server VPS Ubuntu
- [ ] Aktifkan mode `output: 'standalone'` pada file `next.config.ts` di proyek Anda
- [ ] Buat `Dockerfile` produksi 4-stage (`base`, `deps`, `builder`, `runner`) dengan user non-root (`nextjs`)
- [ ] Buat `docker-compose.yml` untuk mengatur kontainer `web` (Next.js), `postgres` (DB persistent), dan `nginx`
- [ ] Jalankan sistem dengan perintah `docker compose up -d --build` dan eksekusi migrasi Drizzle di dalam kontainer!

---
[← Kembali ke Dashboard Progres](daily-progress-tracker.md) | [Lanjut ke Checklist Bonus 2 (GraphQL) →](phase-8-checklist.md)
