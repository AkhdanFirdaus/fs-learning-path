# 🛒 Spesifikasi Studi Kasus: Mini POS (Point of Sales)

**Mini POS** adalah aplikasi sistem kasir untuk toko kecil yang dikembangkan dari awal hingga menjadi aplikasi cloud production selama 30 hari kurikulum.

---

## 📌 Problem Statement
Toko ritel kecil sering mengalami kesulitan dalam:
1. Melacak stok barang yang keluar-masuk secara akurat.
2. Mencatat transaksi penjualan kasir secara cepat dan minim kesalahan kalkulasi.
3. Membedakan hak akses pemilik toko (*Admin*) yang berhak menambah/mengubah barang dan melihat laporan, dengan *Kasir* yang hanya melayani transaksi harian.
4. Mencegah kerugian akibat kesalahan pencatatan harga atau stok negatif.

Aplikasi Mini POS ini hadir sebagai solusi digital ringan, cepat, interaktif, dan terdesentralisasi namun terpusat di cloud database.

---

## 👥 Target User & Roles
Aplikasi mendukung 2 hak akses (*role*) utama:

| Role | Hak Akses & Kemampuan |
| :--- | :--- |
| **Admin (Pemilik Toko)** | • Mengelola Katalog Produk (Create, Read, Update, Delete)<br>• Mengelola Kategori Produk<br>• Melakukan penyesuaian stok (*Stock Adjustment*)<br>• Melihat seluruh Riwayat Transaksi & Laporan Penjualan<br>• Mengelola akun pengguna kasir |
| **Kasir (Operator)** | • Melihat Katalog Produk & mencari/memfilter barang<br>• Mengoperasikan Keranjang Belanja (*Shopping Cart*)<br>• Memproses pembayaran transaksi dan mencetak faktur<br>• Melihat riwayat transaksi yang dibuatnya sendiri |

---

## 🌟 Daftar Fitur Utama (12+ Features)

### 1. Katalog Produk (Product Catalog)
* Tampilan grid/list produk dengan gambar, nama, SKU, harga, dan indikator stok.
* Filter berdasarkan kategori barang.
* Pencarian cepat (*instant search*) berdasarkan nama atau SKU barang.
* Pengurutan (*sorting*) berdasarkan harga termurah/termahal atau nama alfabetis.

### 2. Manajemen Stok & Inventory
* Penampilkan status stok aktual secara real-time.
* Peringatan visual jika stok menipis atau habis (*Out of Stock*).
* Pencatatan log perubahan stok (*Stock Movements*) baik dari transaksi penjualan maupun penyesuaian manual oleh admin.

### 3. Keranjang Belanja (Shopping Cart)
* Penambahan item ke keranjang dari katalog hanya dengan satu klik.
* Pengaturan kuantitas (+ / -) dan penghapusan item dari keranjang.
* Pencegahan penambahan item melebihi batas stok yang tersedia.
* Kalkulasi otomatis subtotal per item dan total keranjang belanja.

### 4. Checkout & Pembayaran
* Perhitungan total bayar dan diskon opsional.
* Input nominal uang pembayaran (*Paid Amount*).
* Perhitungan otomatis kembalian uang (*Change Amount*).
* Validasi pembayaran tidak boleh kurang dari total tagihan.
* Pembuatan nomor faktur unik (misal: `INV-20260706-0001`).

### 5. Riwayat & Detail Transaksi
* Daftar riwayat penjualan yang tersimpan permanen.
* Fitur filter transaksi berdasarkan tanggal atau nama kasir.
* Halaman detail transaksi yang menampilkan rincian barang yang dibeli (*snapshot* harga saat beli).

### 6. Dashboard Penjualan (Analytics)
* Ringkasan total pendapatan (*Total Revenue*).
* Jumlah transaksi berhasil hari ini / bulan ini.
* Daftar produk terlaris (*Best Sellers*).

### 7. Security & Authentication
* Halaman Login dan Logout yang aman.
* Proteksi rute halaman berdasarkan role (*Role-Based Access Control*).
