# 📋 Checklist Fase 1: Vanilla JavaScript DOM & Tailwind CSS (Hari 1–7)

[← Kembali ke Dashboard Progres](daily-progress-tracker.md) | [📑 Daftar Silabus](../README.md)

---

## 📌 Hari 1: Setup & Tampilan Dashboard
- [ ] Buat file `index.html` dengan struktur semantik
- [ ] Integrasikan CDN Tailwind CSS atau via npm
- [ ] Buat layout responsif (sidebar, header, product grid, cart panel)
- [ ] Pastikan tampilan rapi di mobile dan desktop

## 📌 Hari 2: Product Catalog
- [ ] Buat struktur data array of objects untuk produk (`id`, `name`, `price`, `stock`, `img`)
- [ ] Buat fungsi `renderProducts()` untuk mencetak katalog ke DOM
- [ ] Gunakan `document.createElement` atau template string dengan `innerHTML`

## 📌 Hari 3: Search, Filter, dan Sorting
- [ ] Tambahkan input search dan event listener `input` / `keyup`
- [ ] Buat dropdown filter kategori dan fungsi `filterProducts()`
- [ ] Implementasikan fungsi pengurutan (`sort`) berdasarkan harga termurah/termahal

## 📌 Hari 4: Shopping Cart
- [ ] Buat state array `cart = []`
- [ ] Implementasi event click pada tombol 'Tambah ke Keranjang'
- [ ] Logika jika barang sudah ada di keranjang: tambahkan `qty`
- [ ] Logika cegah `qty` melebihi batas stok tersedia
- [ ] Buat fungsi `renderCart()` untuk mencetak rincian item

## 📌 Hari 5: Checkout & Kalkulasi Kembalian
- [ ] Buat form input nominal bayar (`paid_amount`)
- [ ] Hitung otomatis subtotal, diskon, total tagihan, dan kembalian
- [ ] Validasi pencegahan jika uang bayar kurang dari total tagihan
- [ ] Buat nomor faktur unik (misal: `INV-TIMESTAMP`)

## 📌 Hari 6: localStorage dan Riwayat Transaksi
- [ ] Simpan data keranjang dan riwayat transaksi ke `localStorage.setItem()`
- [ ] Ambil data saat load browser menggunakan `localStorage.getItem()` dan `JSON.parse()`
- [ ] Buat tampilan tabel daftar riwayat transaksi kasir

## 📌 Hari 7: Refactoring Vanilla JavaScript
- [ ] Pisahkan kode menjadi modul yang bersih (`js/data.js`, `js/dom.js`, `js/app.js`)
- [ ] Hilangkan variabel global yang berserakan
- [ ] Lakukan pengujian kelancaran alur POS dari awal sampai riwayat muncul

---
[← Kembali ke Dashboard Progres](daily-progress-tracker.md)
