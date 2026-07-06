# 🚀 Full-Stack Web Development 30 Days Mastery (Mini POS Study Case)

Selamat datang di pusat pembelajaran interaktif **Full-Stack Web Development intensif selama 30 hari + Fase Tambahan Deployment Mastery**! Workspace ini dirancang sebagai media belajar mandiri maupun terpandu yang mengubah kurikulum monolitik menjadi ekosistem berstruktur modular, jelas, dan siap dipraktikkan.

Selama 30 hari ke depan, Anda tidak sekadar belajar teori terputus-putus, melainkan membangun **satu aplikasi Point of Sales (Mini POS) secara berulang dan berevolusi** melalui 4 tahapan teknologi:
1. **Vanilla JavaScript DOM & Tailwind CSS**
2. **React 18+ & Component Architecture**
3. **Next.js App Router (Server & Client Components)**
4. **PostgreSQL Database, SQL & Drizzle ORM**
*Plus Fase Bonus Tambahan:* **Masterclass Deployment Production (Hari 31–33: Vercel PaaS, Manual VPS + Nginx, dan Docker Containerization)**.

---

## 🧭 Navigasi Utama Workspace

Workspace ini dibagi menjadi 5 direktori utama agar pembelajaran teratur dan mudah diakses:

| Direktori | Deskripsi & Isi | Link Cepat |
| :--- | :--- | :--- |
| 📘 **`01-overview/`** | Dokumen fundamental, roadmap 30 hari, standar kelulusan, dan rincian stack teknologi. | [Roadmap & Timeline](01-overview/roadmap-and-timeline.md)<br>[Standar Kelulusan](01-overview/target-and-graduation-standards.md)<br>[Detail Stack](01-overview/tech-stack-details.md) |
| 🛒 **`02-study-case-minipos/`** | Spesifikasi lengkap studi kasus Mini POS: daftar fitur, aturan bisnis (*business rules*), desain skema database, dan arsitektur folder. | [Overview & Fitur](02-study-case-minipos/01-overview-and-features.md)<br>[Aturan Bisnis](02-study-case-minipos/02-business-rules.md)<br>[Schema Database](02-study-case-minipos/03-database-schema.md)<br>[Arsitektur Proyek](02-study-case-minipos/04-project-architecture.md) |
| 📅 **`03-curriculum/`** | **Materi Inti & Tugas Harian (30 Hari + 3 Hari Bonus)** yang dipisahkan ke dalam 7 folder fase. | *Lihat Daftar Silabus Lengkap di Bawah ↓* |
| 📋 **`04-checklists/`** | Dashboard interaktif (*checkboxes*) untuk memantau progres belajar Anda dari Hari 1 hingga Hari 33. | [📊 Dashboard Progres](04-checklists/daily-progress-tracker.md)<br>[Checklist Fase 1](04-checklists/phase-1-checklist.md) – [Fase Bonus](04-checklists/phase-7-checklist.md) |
| 📚 **`references/`** | Kumpulan tautan dokumentasi resmi (Next.js, Drizzle, PostgreSQL, Tailwind, React, Docker, Nginx, MDN) serta materi pendukung. | [🔗 Referensi Eksternal](references/external-links-and-docs.md) |

---

## 📅 Silabus & Materi Harian (30 Hari + Bonus Mastery)

Klik tautan pada masing-masing hari untuk membaca panduan materi, latihan, dan spesifikasi fitur yang harus diselesaikan:

### 🟢 Fase 1 — Vanilla JavaScript DOM dan Tailwind CSS (Hari 1–7)
* [Hari 01 — Setup dan Tampilan Dashboard POS](03-curriculum/phase-1-vanilla-js-dom/day-01-setup-dashboard.md)
* [Hari 02 — Product Catalog](03-curriculum/phase-1-vanilla-js-dom/day-02-product-catalog.md)
* [Hari 03 — Search, Filter, dan Sorting](03-curriculum/phase-1-vanilla-js-dom/day-03-search-filter-sort.md)
* [Hari 04 — Shopping Cart](03-curriculum/phase-1-vanilla-js-dom/day-04-shopping-cart.md)
* [Hari 05 — Checkout & Kalkulasi Kembalian](03-curriculum/phase-1-vanilla-js-dom/day-05-checkout.md)
* [Hari 06 — localStorage dan Riwayat Transaksi](03-curriculum/phase-1-vanilla-js-dom/day-06-localstorage-history.md)
* [Hari 07 — Refactoring Vanilla JavaScript](03-curriculum/phase-1-vanilla-js-dom/day-07-refactoring.md)

### 🔵 Fase 2 — React dan Tailwind CSS (Hari 8–13)
* [Hari 08 — Migrasi Product Catalog ke React](03-curriculum/phase-2-react-tailwind/day-08-react-catalog.md)
* [Hari 09 — State dan Shopping Cart](03-curriculum/phase-2-react-tailwind/day-09-state-cart.md)
* [Hari 10 — Form Produk (Controlled Components)](03-curriculum/phase-2-react-tailwind/day-10-product-form.md)
* [Hari 11 — useEffect dan localStorage Synchronization](03-curriculum/phase-2-react-tailwind/day-11-useeffect-storage.md)
* [Hari 12 — Halaman dan Routing (Multi-view SPA)](03-curriculum/phase-2-react-tailwind/day-12-routing-pages.md)
* [Hari 13 — Context dan Role UI (Simulasi Kasir vs Admin)](03-curriculum/phase-2-react-tailwind/day-13-context-role.md)

### 🟣 Fase 3 — Next.js App Router (Hari 14–18)
* [Hari 14 — Migrasi ke Next.js App Router](03-curriculum/phase-3-nextjs-app-router/day-14-nextjs-migration.md)
* [Hari 15 — Server dan Client Component (`"use client"`)](03-curriculum/phase-3-nextjs-app-router/day-15-rsc-vs-client.md)
* [Hari 16 — Route Handler (`app/api/...`)](03-curriculum/phase-3-nextjs-app-router/day-16-route-handler.md)
* [Hari 17 — Server Action untuk Form Mutasi](03-curriculum/phase-3-nextjs-app-router/day-17-server-action.md)
* [Hari 18 — Validasi Bersama (Shared Validation via Zod)](03-curriculum/phase-3-nextjs-app-router/day-18-shared-validation.md)

### 🟠 Fase 4 — PostgreSQL, SQL, dan Drizzle ORM (Hari 19–24)
* [Hari 19 — Fundamental Database Relasional (SQL & ERD)](03-curriculum/phase-4-postgresql-drizzle/day-19-relational-db.md)
* [Hari 20 — Setup PostgreSQL dan Drizzle ORM](03-curriculum/phase-4-postgresql-drizzle/day-20-setup-drizzle.md)
* [Hari 21 — Schema Produk dan Kategori (`pgTable`)](03-curriculum/phase-4-postgresql-drizzle/day-21-schema-product.md)
* [Hari 22 — Migration dan Seed Data Awal](03-curriculum/phase-4-postgresql-drizzle/day-22-migration-seed.md)
* [Hari 23 — Repository dan Query Layer (`db.select`)](03-curriculum/phase-4-postgresql-drizzle/day-23-repository-query.md)
* [Hari 24 — Inventory dan Stock Movement Audit](03-curriculum/phase-4-postgresql-drizzle/day-24-inventory-stock.md)

### 🔴 Fase 5 — Backend dan Integrasi Full-Stack (Hari 25–28)
* [Hari 25 — Backend CRUD Produk Persisten](03-curriculum/phase-5-backend-integration/day-25-backend-crud.md)
* [Hari 26 — Checkout dengan Database Transaction (`db.transaction`)](03-curriculum/phase-5-backend-integration/day-26-db-transaction.md)
* [Hari 27 — Authentication (Login/Logout & Session Security)](03-curriculum/phase-5-backend-integration/day-27-authentication.md)
* [Hari 28 — Authorization dan Audit Trail (Role Admin vs Kasir)](03-curriculum/phase-5-backend-integration/day-28-authorization-audit.md)

### 🏆 Fase 6 — Penyelesaian dan Verifikasi Akhir (Hari 29–30)
* [Hari 29 — Testing dan Security Review](03-curriculum/phase-6-finalization/day-29-testing-security.md)
* [Hari 30 — Refactoring Final dan Dokumentasi README](03-curriculum/phase-6-finalization/day-30-refactoring-deploy.md)

### 🌟 Fase Tambahan (Bonus Mastery) — Production Deployment Mastery (Hari 31–33)
* [Hari 31 — Deployment ke Vercel (PaaS / Serverless)](03-curriculum/phase-7-deployment-mastery/day-31-deploy-vercel.md)
* [Hari 32 — Deployment Manual ke VPS (Ubuntu, Nginx, PM2 & SSL)](03-curriculum/phase-7-deployment-mastery/day-32-deploy-manual-vps.md)
* [Hari 33 — Deployment ke VPS Menggunakan Docker (Masterclass Containerization)](03-curriculum/phase-7-deployment-mastery/day-33-deploy-docker-vps.md)

---

## 💡 Tips Penggunaan Workspace Ini

1. **Gunakan sebagai Panduan & Tracker:** Bukalah file materi harian di folder `03-curriculum/` untuk membaca teori dan tugas setiap harinya. Setelah selesai, buka [📊 Dashboard Progres](04-checklists/daily-progress-tracker.md) dan centang kotak `- [x]` hari tersebut!
2. **Jangan Lompat Fase:** Setiap fase dibangun di atas fundamen fase sebelumnya. Jika Anda kesulitan di Fase 3 (Next.js), periksa kembali konsep komponen & state di Fase 2 (React).
3. **Perhatikan Aturan Bisnis Mutlak:** Baca secara saksama dokumen [Aturan Bisnis Mini POS](02-study-case-minipos/02-business-rules.md). Fitur kalkulasi kasir dan pemotongan stok wajib mengikuti standar transaksi atomic yang telah dijelaskan.
4. **Pilih Metode Deployment Tambahan Sesuai Kebutuhan:** Setelah menyelesaikan 30 hari kelas utama, lanjutkan ke Hari 31, 32, atau 33 untuk menguasai skill DevOps & Cloud Deployment!
5. **Manfaatkan Folder Referensi:** Kunjungi folder [📚 References](references/external-links-and-docs.md) untuk menuju dokumentasi resmi dan materi panduan tambahan.

Selamat belajar dan berkreasi! Konsistensi 3–4 jam setiap hari akan mengubah Anda menjadi developer full-stack yang matang dan siap kerja. 🚀
