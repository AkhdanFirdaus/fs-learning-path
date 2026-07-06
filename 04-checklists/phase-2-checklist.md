# 📋 Checklist Fase 2: React & Tailwind CSS (Hari 8–13)

[← Kembali ke Dashboard Progres](daily-progress-tracker.md) | [📑 Daftar Silabus](../README.md)

---

## 📌 Hari 8: Migrasi Product Catalog ke React
- [ ] Setup proyek React menggunakan Vite (`npm create vite@latest ./ -- --template react-ts`)
- [ ] Instalasi dan konfigurasi Tailwind CSS di React
- [ ] Buat komponen `ProductCard.tsx` dan `ProductGrid.tsx`
- [ ] Passing data melalui Props secara terstruktur

## 📌 Hari 9: State dan Shopping Cart
- [ ] Gunakan hook `useState` untuk menyimpan daftar produk dan item keranjang
- [ ] Buat fungsi `addToCart(product)` dan `removeFromCart(id)`
- [ ] Buat komponen `CartPanel.tsx` yang secara reaktif menghitung subtotal

## 📌 Hari 10: Form Produk (Controlled Components)
- [ ] Buat form input produk baru (Nama, SKU, Harga, Stok, Kategori)
- [ ] Gunakan *controlled components* (`value={state}` & `onChange`)
- [ ] Implementasi validasi sederhana (harga dilarang minus, nama wajib isi)
- [ ] Tambahkan produk baru ke dalam array state utama

## 📌 Hari 11: useEffect dan localStorage Synchronization
- [ ] Gunakan `useEffect` untuk memuat data dari `localStorage` saat *initial render*
- [ ] Gunakan `useEffect` untuk menyimpan state cart & transaksi ke `localStorage` setiap kali ada perubahan
- [ ] Tangani masalah hydration atau sinkronisasi state

## 📌 Hari 12: Halaman dan Routing
- [ ] Instalasi `react-router-dom` atau gunakan navigasi view ber-state
- [ ] Buat rute halaman: `/` (POS Kasir), `/products` (Manajemen Katalog), `/history` (Riwayat)
- [ ] Implementasi navbar aktif berdasarkan rute saat ini

## 📌 Hari 13: Context dan Role UI
- [ ] Buat `AuthContext` sederhana untuk simulasi user log in (`{ name: 'Kasir 1', role: 'cashier' }`)
- [ ] Buat *toggle switcher* untuk berganti role secara cepat antara **Admin** dan **Kasir**
- [ ] Sembunyikan tombol 'Tambah Produk' dan menu 'Manajemen Katalog' jika role adalah Kasir

---
[← Kembali ke Dashboard Progres](daily-progress-tracker.md)
