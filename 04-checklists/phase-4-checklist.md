# 📋 Checklist Fase 4: PostgreSQL, SQL, dan Drizzle ORM (Hari 19–24)

[← Kembali ke Dashboard Progres](daily-progress-tracker.md) | [📑 Daftar Silabus](../README.md)

---

## 📌 Hari 19: Fundamental Database Relasional (SQL & ERD)
- [ ] Pahami konsep Normalisasi Database, Primary Key (PK), dan Foreign Key (FK)
- [ ] Rancang ERD untuk 6 tabel: `users`, `categories`, `products`, `sales`, `sale_items`, `stock_movements`
- [ ] Pahami alasan mutlak mengapa harga & nama produk harus di-snapshot di `sale_items`

## 📌 Hari 20: Setup PostgreSQL dan Drizzle ORM
- [ ] Siapkan database PostgreSQL (lokal via Docker / instalasi langsung, atau cloud via Supabase / Neon)
- [ ] Instalasi Drizzle ORM & Drizzle Kit (`npm i drizzle-orm pg dotenv` & `npm i -D drizzle-kit @types/pg`)
- [ ] Buat file `drizzle.config.ts` dan konfigurasi koneksi di `src/db/index.ts`
- [ ] Siapkan file `.env.local` dengan `DATABASE_URL=postgresql://...`

## 📌 Hari 21: Schema Produk dan Kategori (`pgTable`)
- [ ] Definisikan tabel `categories` dan `products` di `src/db/schema/index.ts`
- [ ] Tentukan tipe kolom yang tepat: `serial`, `varchar`, `numeric(12, 2)`, `integer`, `boolean`, `timestamp`
- [ ] Tambahkan *foreign key reference* dari `products.category_id` ke `categories.id`

## 📌 Hari 22: Migration dan Seed Data Awal
- [ ] Jalankan perintah generate migrasi: `npx drizzle-kit generate`
- [ ] Periksa file SQL yang dihasilkan di dalam folder `drizzle/`
- [ ] Jalankan perintah push/migrate: `npx drizzle-kit migrate` (atau `push`)
- [ ] Buat script `src/db/seed.ts` untuk mengisi akun admin awal dan 5-10 contoh produk
- [ ] Jalankan seeder via tsx/ts-node

## 📌 Hari 23: Repository dan Query Layer
- [ ] Buat folder `src/repositories/` (misal: `productRepo.ts`, `categoryRepo.ts`)
- [ ] Implementasi fungsi query: `findAllProducts()`, `findProductById(id)`, `createProduct(data)`, `updateProductStock(id, qty)`
- [ ] Gunakan sintaks query Drizzle yang type-safe (`db.select().from(products)...`)

## 📌 Hari 24: Inventory dan Stock Movement Audit
- [ ] Definisikan tabel `stock_movements` di dalam schema Drizzle
- [ ] Buat repository/service untuk mendokumentasikan setiap perubahan stok (tipe: `in`, `out`, `sale`, `adjustment`)
- [ ] Uji coba penambahan stok barang baru dan pastikan riwayat log tercatat sempurna

---
[← Kembali ke Dashboard Progres](daily-progress-tracker.md)
