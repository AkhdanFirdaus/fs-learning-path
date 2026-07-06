# 🛠️ Detail Stack Teknologi

Kurikulum ini menggunakan kombinasi teknologi modern yang dipilih secara ketat karena standar industri, efisiensi developer (*developer experience*), serta performa tinggi di lingkungan production.

---

## 1. Core & Frontend Stack

### Vanilla JavaScript (ES6+) & DOM
* **Mengapa dipakai di Fase 1?** Sebelum menggunakan framework, seorang engineer wajib memahami bagaimana browser bekerja, bagaimana DOM tree dimanipulasi, pengelolaan event listener, serta sifat asinkronus JavaScript (Promise & Async/Await).
* **Fokus:** Array manipulation, Object profiling, Higher-order functions (`map`, `filter`, `reduce`), modularisasi code (`import/export`), dan browser storage (`localStorage`).

### React 18+ (Library UI)
* **Mengapa dipakai di Fase 2?** React adalah standar industri untuk membangun antarmuka pengguna berbasis komponen.
* **Fokus:** Functional Components, Props passing, Local State (`useState`), Side Effects (`useEffect`), dan Global State sederhana via React Context (`useContext`).

### Tailwind CSS (Styling Engine)
* **Mengapa Tailwind?** Memberikan kecepatan penulisan styling yang luar biasa dengan pendekatan *utility-first*, tanpa harus meninggalkan file komponen atau menghadapi konflik nama class CSS (*BEM naming fatigue*).
* **Fokus:** Responsive design (`sm:`, `md:`, `lg:`), Flexbox/Grid layouting, state variants (`hover:`, `focus:`, `disabled:`), dan dark mode.

---

## 2. Full-Stack Framework & Routing

### Next.js (App Router)
* **Mengapa Next.js?** Next.js bukan sekadar framework React, melainkan platform full-stack yang menyatukan rendering server dan client. App Router (`app/`) adalah standar terbaru Next.js berbasis React Server Components (RSC).
* **React Server Components (RSC):** Komponen yang di-render eksklusif di server. Mengurangi ukuran bundle JavaScript yang dikirim ke browser dan memungkinkan akses langsung ke database tanpa API layer perantara.
* **Client Components (`"use client"`):** Komponen interaktif yang berjalan di browser (untuk *event listener*, *state*, dan *browser APIs*).
* **Route Handlers:** API endpoint RESTful standar di dalam Next.js (`app/api/.../route.ts`) yang mendukung HTTP methods (`GET`, `POST`, `PUT`, `PATCH`, `DELETE`).
* **Server Actions:** Fungsi asinkron di server yang dapat dipanggil langsung dari Client Components atau form HTML untuk mutasi data yang aman dan cepat.

---

## 3. Database & ORM

### PostgreSQL (Relational Database)
* **Mengapa PostgreSQL?** Database open-source paling canggih, robust, dan terpercaya di industri perangkat lunak. Sangat kuat dalam menangani relasi data kompleks, integritas referensial, dan transaksi finansial (ACID compliance).
* **Fokus:** Primary key, Foreign key, Indexing, tipe data SQL (`VARCHAR`, `INTEGER`, `NUMERIC`, `TIMESTAMP`, `BOOLEAN`), serta pembatasan (*constraints*).

### Drizzle ORM
* **Mengapa Drizzle ORM?** ORM TypeScript modern yang sangat cepat, ringan, dan **dekat dengan SQL (*SQL-like*)**. Berbeda dengan ORM tradisional yang menyembunyikan SQL di balik abstraksi berat, Drizzle memberi Anda kontrol penuh layaknya menulis SQL murni, namun dengan perlindungan *type-safety* TypeScript 100%.
* **Drizzle Kit:** Tool CLI pendamping untuk manajemen skema database, menghasilkan file SQL migration secara otomatis dari kode TypeScript (*code-first migration*), dan menerapkannya ke database secara aman.

---

## 4. Tooling & Architecture
* **TypeScript:** Memberikan pengetikan statis untuk mencegah bug saat runtime dan meningkatkan intellisense di code editor.
* **Zod:** Library validasi skema TypeScript-first yang digunakan secara konsisten baik di frontend (validasi form) maupun di backend (validasi payload API & Server Action).
* **Git & GitHub:** Standar version control untuk melacak progres harian dan mendokumentasikan rilis fase.

---

## 5. Deployment & DevOps Mastery Stack

Sebagai pelengkap kompetensi Full-Stack, kurikulum ini menyertakan 3 metode deployment standar industri di Fase 6:

### Vercel (Platform-as-a-Service / Serverless)
* **Mengapa Vercel?** Platform kreator Next.js dengan arsitektur serverless edge. Memberikan integrasi CI/CD otomatis (*push to deploy*) dan optimasi caching tingkat dunia tanpa konfigurasi server yang rumit.

### Linux VPS + Nginx + PM2 (Manual Server Deployment)
* **Mengapa Manual VPS?** Memberikan pemahaman mendalam tentang administrasi sistem Linux (Ubuntu), konfigurasi firewall (UFW), manajemen proses node.js 24/7 menggunakan **PM2**, serta perancangan **Nginx** sebagai *reverse proxy* berkinerja tinggi lengkap dengan enkripsi SSL/HTTPS gratis dari **Let's Encrypt (Certbot)**.

### Docker & Containerization (Masterclass)
* **Mengapa Docker?** Menghilangkan kutukan *"It works on my machine"* dengan membungkus aplikasi, runtime Node.js, dan library sistem ke dalam container yang terisolasi dan identik di semua lingkungan.
* **Multi-Stage Build:** Optimasi canggih pada `Dockerfile` untuk memangkas ukuran image produksi Next.js dari >1.5 GB menjadi hanya ~100 MB menggunakan mode `output: 'standalone'`.
* **Docker Compose:** Alat orkestrasi untuk menjalankan ekosistem multi-container (Next.js Web + PostgreSQL Database + Nginx Proxy) secara sinkron dengan satu perintah `docker compose up -d`.
