# 📅 Hari 30 — Refactoring, Dokumentasi README, dan Deployment Mastery
**Fase 6: Penyelesaian & Deployment**

[← Hari 29](./day-29-testing-security.md) | [📑 Daftar Silabus](../../README.md) | [🎓 Standar Kelulusan](../../01-overview/target-and-graduation-standards.md)

---

## 🎯 Tujuan Hari Ini
Selamat tiba di hari puncak kurikulum 30 hari! Pada hari terakhir ini, kita akan melakukan tiga tahapan krusial untuk menyempurnakan aplikasi **Mini POS**:
1. **Refactoring Akhir:** Membersihkan kode, menghapus duplikasi, dan mengoptimalkan performa.
2. **Dokumentasi README.md:** Menyusun dokumentasi teknis yang profesional untuk portofolio Anda.
3. **Deployment Mastery (3 Langkah):** Mempelajari dan mempraktikkan rilis produksi melalui 3 metode standar industri: **Vercel PaaS**, **Manual VPS (Nginx + PM2)**, dan **Docker Containerization**.

---

## 1. 🧹 Refactoring Kode Akhir

Sebelum merilis aplikasi ke publik, lakukan pemeriksaan dan pembersihan menyeluruh pada *codebase* Anda:
* **Pecah Function Terlalu Panjang:** Jika ada fungsi di dalam Route Handler atau Server Action yang melebihi 50 baris, pisahkan menjadi helper functions di `src/services/` atau `src/utils/`.
* **Hapus Kode Duplikat (DRY Principle):** Gunakan satu komponen UI bersama (misal: `<Modal />` atau `<ProductCard />`) daripada menulis ulang struktur JSX yang sama.
* **Rapikan Query Layer:** Pastikan seluruh interaksi database PostgreSQL tersentralisasi di dalam folder `src/repositories/`.
* **Hapus Logging Sensitif:** Cari dan hapus semua perintah `console.log(user)`, `console.log(password)`, atau logging payload transaksi yang bersifat rahasia.
* **Periksa Penggunaan `"use client"`:** Jangan pasang direktif `"use client"` pada komponen yang hanya bertugas menampilkan data statis tanpa interaksi browser.
* **Periksa State & Error Handling:** Pastikan setiap halaman memiliki penanganan *Loading State* (`loading.tsx`), *Empty State* (saat katalog/riwayat kosong), dan *Error Boundary* (`error.tsx`).

---

## 2. 📝 Pembuatan Dokumentasi `README.md` Proyek

Sebuah proyek portofolio tidak lengkap tanpa dokumen `README.md` yang impresif di root repository GitHub Anda. Gunakan template berikut:

```markdown
# 🛒 Mini POS — Full-Stack Point of Sales Application

Mini POS adalah aplikasi sistem kasir cloud web modern yang dirancang untuk toko ritel kecil, dikembangkan menggunakan stack teknologi terkini dengan fokus pada integritas data, transaksi atomic, dan performa tinggi.

## ✨ Features
- **Katalog Produk & Kategori:** Manajemen barang dengan pencarian instan dan filter kategori.
- **Inventory & Stock Tracking:** Pemantauan stok aktual dan audit log pergerakan barang (*Stock Movements*).
- **Interactive Shopping Cart:** Kalkulasi otomatis subtotal dan pencegahan stok minus.
- **Atomic Checkout & Point of Sales:** Pemrosesan transaksi keuangan dan pemotongan stok dalam satu *database transaction*.
- **Riwayat Penjualan & Snapshot Harga:** Laporan transaksi permanen dengan rekam jejak harga historis yang *immutable*.
- **Role-Based Access Control (RBAC):** Hak akses terpisah antara **Admin (Pemilik Toko)** dan **Kasir (Operator)**.

## 🛠️ Technology Stack
- **Framework:** Next.js App Router (React 18+, Server Components, Server Actions)
- **Styling:** Tailwind CSS
- **Database:** PostgreSQL
- **ORM & Migrations:** Drizzle ORM & Drizzle Kit
- **Validation:** Zod TypeScript Schema
- **Deployment:** Vercel / VPS Ubuntu / Docker Container

## 🚀 Installation & Local Development

1. **Clone repository:**
   ```bash
   git clone https://github.com/username/mini-pos.git
   cd mini-pos
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Setup Environment Variables:**
   Salin file `.env.example` menjadi `.env.local` dan sesuaikan koneksi database Anda:
   ```env
   DATABASE_URL="postgresql://postgres:password@localhost:5432/minipos_db"
   NEXTAUTH_SECRET="your-secret-key"
   NEXTAUTH_URL="http://localhost:3000"
   ```

4. **Run Database Migrations & Seeding:**
   ```bash
   npx drizzle-kit migrate
   npx tsx src/db/seed.ts
   ```

5. **Start Development Server:**
   ```bash
   npm run dev
   ```
   Buka `http://localhost:3000` di browser Anda.

## 🏛️ Architecture & Database Design
Aplikasi ini menerapkan separation of concerns dengan lapisan UI, Server Actions, Service Layer, Repository Layer, dan Drizzle ORM.
*(Lihat dokumentasi lengkap di folder `/02-study-case-minipos/`)*
```

---

## 3. 🚀 Deployment Mastery (3 Metode Industri)

Sebagai pembuktian akhir dari perjalanan Full-Stack Anda, kami telah menyusun **3 Panduan Deployment Rinci** yang mencakup seluruh skenario dunia kerja nyata. Anda dapat memilih salah satu atau mencoba ketiganya:

### 🌟 [Langkah 1: Deploy ke Vercel (PaaS / Serverless)](./deploy-step-1-vercel.md)
* **Cocok untuk:** Rilis cepat, portofolio instan, dan zero-configuration CI/CD.
* **Materi:** Koneksi database cloud (Neon/Supabase), setup environment variables di Vercel dashboard, dan verifikasi serverless edge functions.
👉 **[Baca Panduan Langkah 1: Vercel →](./deploy-step-1-vercel.md)**

### 🖥️ [Langkah 2: Deploy Manual ke VPS (Ubuntu, Nginx, PM2 & SSL)](./deploy-step-2-manual-vps.md)
* **Cocok untuk:** Kontrol penuh atas server, efisiensi biaya, dan pemahaman mendalam arsitektur Linux/Web Server.
* **Materi:** Provisioning VPS Ubuntu, konfigurasi firewall UFW, instalasi Node.js via NVM, pengelolaan process 24/7 dengan **PM2**, setup **Nginx Reverse Proxy**, dan instalasi sertifikat SSL gratis **Let's Encrypt (Certbot)**.
👉 **[Baca Panduan Langkah 2: Manual VPS →](./deploy-step-2-manual-vps.md)**

### 🐳 [Langkah 3: Deploy ke VPS Menggunakan Docker (Masterclass Containerization)](./deploy-step-3-docker-vps.md)
* **Cocok untuk:** Standar industri modern, skalabilitas, dan menghilangkan masalah *"It works on my machine"*.
* **Sub-Materi Khusus:**
  * **Teori Mendalam Docker:** Perbedaan fundamental Container vs Virtual Machine (VM), mengapa container ringan dan cepat.
  * **Rahasia Multi-Stage Build:** Cara memangkas ukuran image Next.js dari >1.5 GB menjadi hanya ~100 MB menggunakan mode `output: 'standalone'`.
  * **Orchestration:** Pembuatan `Dockerfile` production dan `docker-compose.yml` untuk menjalankan kontainer Next.js + PostgreSQL + Nginx secara terintegrasi.
👉 **[Baca Panduan Langkah 3: Docker VPS →](./deploy-step-3-docker-vps.md)**

---

## 📋 Checklist Target Hari Ini

- [ ] Melakukan pemeriksaan dan pembersihan kode (*refactoring*) pada seluruh komponen dan server action
- [ ] Membuat dan melengkapi dokumen `README.md` di root repository proyek final Anda
- [ ] **Memilih dan Mempraktikkan Minimal 1 Metode Deployment:**
  - [ ] **Opsi A:** Berhasil men-deploy aplikasi ke Vercel dengan koneksi database cloud
  - [ ] **Opsi B:** Berhasil men-deploy manual ke VPS Ubuntu menggunakan PM2, Nginx, dan HTTPS Certbot
  - [ ] **Opsi C:** Berhasil mengemas aplikasi ke dalam Docker Container (Multi-Stage Build) dan menjalankan `docker compose` di VPS
- [ ] Melakukan verifikasi akhir: uji coba login admin dan transaksi kasir di URL live production!
- [ ] Menyimpan checkpoint final dengan *git commit & tag* (misal: `git commit -m "chore: release v1.0.0 production ready"` & `git tag v1.0.0`)

---

## 🏆 Selamat Atas Kelulusan Anda!
Anda telah menuntaskan seluruh roadmap **Full-Stack Web Development Intensif 30 Hari**. Dari manipulasi DOM dasar di Hari 1, hingga arsitektur cloud containerization Docker di Hari 30—Anda kini siap menghadapi tantangan industri perangkat lunak modern! 🎓🚀

---

[← Hari 29](./day-29-testing-security.md) | [📑 Daftar Silabus](../../README.md) | [🎓 Standar Kelulusan](../../01-overview/target-and-graduation-standards.md)
