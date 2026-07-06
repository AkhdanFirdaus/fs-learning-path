# 📋 Checklist Fase 3: Next.js App Router (Hari 14–18)

[← Kembali ke Dashboard Progres](daily-progress-tracker.md) | [📑 Daftar Silabus](../README.md)

---

## 📌 Hari 14: Migrasi ke Next.js App Router
- [ ] Setup proyek Next.js 15+ (`npx create-next-app@latest ./ --typescript --tailwind --app`)
- [ ] Pahami struktur folder `app/`, `layout.tsx`, dan `page.tsx`
- [ ] Migrasikan komponen UI dari Vite ke dalam struktur direktori Next.js

## 📌 Hari 15: Server dan Client Component
- [ ] Identifikasi komponen mana yang statis (Server Component) dan mana yang interaktif (Client Component)
- [ ] Tambahkan direktif 'use client' hanya pada komponen yang memiliki `useState`, `onClick`, atau `useEffect`
- [ ] Pastikan halaman utama me-render katalog secara optimal dari server

## 📌 Hari 16: Route Handler (`app/api/...`)
- [ ] Buat endpoint REST API: `app/api/products/route.ts` (GET & POST)
- [ ] Buat endpoint transaksi: `app/api/transactions/route.ts`
- [ ] Gunakan `NextResponse.json()` dan tangani status code standar (`200`, `201`, `400`, `404`, `500`)

## 📌 Hari 17: Server Action untuk Form Mutasi
- [ ] Buat file `src/actions/productActions.ts` dengan direktif 'use server'
- [ ] Buat fungsi asinkron `createProduct(formData: FormData)`
- [ ] Hubungkan form HTML/React langsung ke Server Action menggunakan atribut `action={createProduct}`
- [ ] Gunakan `revalidatePath('/products')` untuk memperbarui data layar tanpa refresh browser

## 📌 Hari 18: Validasi Bersama (Shared Validation via Zod)
- [ ] Instalasi library Zod (`npm install zod`)
- [ ] Buat skema validasi `productSchema` dan `checkoutSchema` di `src/validators/`
- [ ] Gunakan skema Zod di frontend untuk validasi sebelum submit
- [ ] Gunakan skema Zod yang sama di dalam Server Action untuk memvalidasi payload di server

---
[← Kembali ke Dashboard Progres](daily-progress-tracker.md)
