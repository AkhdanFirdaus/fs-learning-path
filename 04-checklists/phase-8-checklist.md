# 📋 Checklist Fase Tambahan 2: GraphQL & Real-time API Mastery (Hari 34–36)

[← Kembali ke Checklist Fase Bonus 1 (Deployment)](phase-7-checklist.md) | [← Dashboard Progres](daily-progress-tracker.md) | [📑 Daftar Silabus](../README.md)

---

## 📌 Hari 34: Fundamental GraphQL, Setup Apollo/Yoga di Next.js & Query Katalog
- [ ] Memahami konsep dasar GraphQL: Schema, Type Definitions (`typeDefs`), Resolvers, dan keuntungan 1-endpoint
- [ ] Berhasil menginstal library `graphql` dan `graphql-yoga` di dalam proyek Next.js
- [ ] Berhasil mendefinisikan skema GraphQL untuk entitas `Product` dan `Category` (`typeDefs`)
- [ ] Berhasil menulis Resolver yang terhubung dengan Drizzle ORM Relational Query (`db.query`)
- [ ] Berhasil membuka GraphiQL Studio di `/api/graphql` dan mengeksekusi query katalog produk dengan filter

## 📌 Hari 35: Mutasi GraphQL & Integrasi Transaksi Atomic POS
- [ ] Memahami sintaks input types dan Mutation pada GraphQL
- [ ] Berhasil menambahkan definisi `Mutation` untuk `createProduct` dan `processCheckout`
- [ ] Berhasil mengimplementasikan resolver mutasi kasir menggunakan `db.transaction()` Drizzle ORM
- [ ] Berhasil memverifikasi bahwa aturan bisnis (stok minus gagal, snapshot harga persisten) dipatuhi oleh GraphQL
- [ ] Berhasil menjalankan pengujian mutasi dari antarmuka GraphiQL Studio dan memeriksa pengurangan stok database

## 📌 Hari 36: GraphQL Client (Urql/Apollo) & Real-time Subscriptions di POS
- [ ] Memahami perbedaan cara kerja GraphQL Client (Urql / Apollo) dibandingkan `fetch` REST biasa
- [ ] Berhasil menginstal `urql` dan memasang `<GraphQLProvider />` pada Root Layout aplikasi Next.js
- [ ] Berhasil mengambil data katalog produk di halaman kasir menggunakan hook `useQuery`
- [ ] Berhasil mengeksekusi mutasi checkout kasir dari UI menggunakan hook `useMutation`
- [ ] Memahami konsep Real-time Subscriptions (WebSockets/SSE) untuk implementasi *Kitchen Display System* dan notifikasi stok

---
[← Kembali ke Dashboard Progres](daily-progress-tracker.md)
