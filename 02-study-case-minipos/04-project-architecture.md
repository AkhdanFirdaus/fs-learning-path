# 🏗️ Struktur Final Project & Arsitektur Aplikasi

Mulai dari **Fase 3 (Next.js App Router)** hingga **Fase 6**, proyek Mini POS akan distrukturkan menggunakan standar direktori modern yang bersih, terpisah berdasarkan tanggung jawab (*separation of concerns*), dan mudah diskalakan.

---

## 📁 Struktur Direktori Standar (`mini-pos/`)

```text
mini-pos/
├── app/                        # Next.js App Router (Pages, Layouts, & API Routes)
│   ├── api/                    # Route Handlers untuk REST API endpoints
│   │   ├── products/
│   │   ├── categories/
│   │   └── transactions/
│   ├── dashboard/              # Halaman Dashboard (Admin)
│   ├── products/               # Halaman Manajemen Produk & Stok
│   ├── transactions/           # Halaman POS Kasir & Riwayat Penjualan
│   ├── login/                  # Halaman Authentication
│   ├── layout.tsx              # Root Layout & Global Providers
│   └── page.tsx                # Landing atau Redirect ke Dashboard
├── components/                 # React UI Components (Reusable)
│   ├── ui/                     # Primitif UI (Button, Modal, Input, Badge, Table)
│   ├── products/               # Komponen spesifik produk (ProductCard, ProductForm)
│   ├── cart/                   # Komponen keranjang belanja (CartPanel, CartItem)
│   └── transactions/           # Komponen riwayat & cetak faktur (InvoiceModal)
├── src/                        # Core Application Logic & Data Layer
│   ├── actions/                # Next.js Server Actions (mutasi form & checkout)
│   ├── auth/                   # Konfigurasi Authentication & Session
│   ├── db/                     # Database layer (PostgreSQL & Drizzle ORM)
│   │   ├── schema/             # Definisi skema tabel Drizzle
│   │   ├── index.ts            # Inisialisasi koneksi DB (Pool & ORM client)
│   │   └── seed.ts             # Script seeder untuk admin awal & sampel produk
│   ├── repositories/           # Abstraksi query DB (misal: productRepo.ts)
│   ├── services/               # Business logic & kalkulasi kompleks (checkoutService.ts)
│   ├── validators/             # Skema validasi Zod (productSchema.ts, checkoutSchema.ts)
│   └── utils/                  # Helper fungsi (formatRupiah.ts, formatDate.ts)
├── drizzle/                    # Folder hasil generasi migrasi SQL dari Drizzle Kit
├── tests/                      # Folder Unit & Integration Tests
├── drizzle.config.ts           # Konfigurasi Drizzle Kit CLI
├── next.config.ts              # Konfigurasi Next.js
├── tailwind.config.ts          # Konfigurasi Tailwind CSS & Theme
├── tsconfig.json               # Konfigurasi TypeScript
└── package.json                # Daftar dependensi & scripts
```

---

## 🏛️ Arsitektur Alur Data (Data Flow)

```text
[ Browser / UI Client ]
        │
        ├── 1. Request Page (GET) ───────────────> [ Next.js Server Component ]
        │                                                  │
        │                                            Query │ via Repository Layer
        │                                                  v
        │                                          [ PostgreSQL Database ]
        │
        ├── 2. Mutasi Data (Checkout/Save) ──────> [ Next.js Server Action / API ]
        │                                                  │
        │                                         Validasi │ Zod Schema & Session Auth
        │                                                  v
        │                                         [ Service Layer (Business Logic) ]
        │                                                  │
        │                                         Tx Atomic│ Drizzle ORM Transaction
        │                                                  v
        │                                          [ PostgreSQL Database ]
        v
[ UI Revalidate / Refresh ] <────────────────────── Revalidate Path / Tag
```

---

## 💡 Prinsip Arsitektur Utama

1. **Server-First Rendering:** Manfaatkan React Server Component (RSC) sebagai default untuk mengambil data katalog dan riwayat langsung di server tanpa efek *waterfall fetch* di client.
2. **Client Components Seperlunya:** Gunakan `"use client"` hanya pada komponen yang butuh interaktivitas langsung seperti tombol cart, modal, filter input, dan form handler.
3. **Validasi Bersama (Shared Validation):** Skema Zod di `src/validators/` diimpor oleh form frontend untuk memberi feedback error langsung ke user, sekaligus diimpor oleh Server Action/API untuk mencegah *tampering data*.
4. **Isolasi Database Layer:** Semua perintah `db.select()`, `db.insert()`, dll diletakkan di dalam `src/repositories/` atau `src/services/`. Jangan menulis query database mentah berserakan langsung di dalam file UI Component!
