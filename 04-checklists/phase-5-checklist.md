# 📋 Checklist Fase 5: Backend dan Integrasi Full-Stack (Hari 25–28)

[← Kembali ke Dashboard Progres](daily-progress-tracker.md) | [📑 Daftar Silabus](../README.md)

---

## 📌 Hari 25: Backend CRUD Produk Persisten
- [ ] Hubungkan seluruh halaman UI Manajemen Produk Next.js dengan Repository PostgreSQL
- [ ] Gantikan total penggunaan `localStorage` untuk katalog produk dengan database persisten
- [ ] Uji coba Tambah, Edit, dan Non-aktifkan (`is_active = false`) produk dari antarmuka web

## 📌 Hari 26: Checkout dengan Database Transaction (`db.transaction`)
- [ ] Definisikan tabel `sales` dan `sale_items` di Drizzle schema
- [ ] Buat file `src/services/checkoutService.ts`
- [ ] Implementasikan alur checkout di dalam blok `db.transaction(async (tx) => { ... })`
- [ ] Dalam satu transaksi: Insert ke `sales`, Insert ke `sale_items`, Update decrement `products.stock`, dan Insert ke `stock_movements`
- [ ] Uji coba simulasi kegagalan (stok kurang) dan pastikan terjadi *rollback* otomatis

## 📌 Hari 27: Authentication (Login/Logout & Session Security)
- [ ] Implementasikan sistem autentikasi (menggunakan NextAuth.js / Auth.js, atau JWT/Session cookie kustom dengan `bcryptjs`/`argon2`)
- [ ] Buat tabel `users` persisten dengan verifikasi password hash
- [ ] Buat form Login dan mekanisme pemeliharaan sesi kasir/admin

## 📌 Hari 28: Authorization dan Audit Trail (Role Admin vs Kasir)
- [ ] Implementasi Middleware Next.js (`middleware.ts`) untuk membedakan akses rute `/dashboard` dan `/products`
- [ ] Tambahkan verifikasi role (`if (user.role !== 'admin') throw new Error('Unauthorized')`) di dalam setiap Server Action
- [ ] Pastikan setiap transaksi penjualan dan pergerakan stok mencantumkan `cashier_id` / `created_by`

---
[← Kembali ke Dashboard Progres](daily-progress-tracker.md)
