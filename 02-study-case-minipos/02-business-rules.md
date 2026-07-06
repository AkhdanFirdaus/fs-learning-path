# ⚖️ Aturan Bisnis (Business Rules & Domain Logic)

Dalam perancangan perangkat lunak finansial dan inventaris seperti Mini POS, desain antarmuka yang bagus tidak ada artinya jika **aturan bisnis (*business rules*)** diabaikan. Berikut adalah aturan bisnis mutlak yang harus diterapkan pada aplikasi ini:

---

## 1. Snapshot Harga pada Transaksi (Price & Name Snapshot)
> [!CAUTION]
> **Aturan Mutlak:**  
> Kolom `unit_price` dan `product_name` **WAJIB** disimpan secara duplikatif/eksplisit di dalam tabel `sale_items` sebagai *snapshot* pada detik transaksi terjadi.

* **Alasan Bisnis:** Jika pelanggan membeli "Kopi Susu" seharga Rp 15.000 hari ini, lalu bulan depan admin menaikkan harga kopi tersebut menjadi Rp 18.000, **laporan penjualan historis bulan ini tidak boleh berubah menjadi Rp 18.000!**
* Transaksi historis harus bersifat *immutable* (tidak dapat diubah setelah selesai dibayar).

---

## 2. Transaksi & Pemotongan Stok yang Atomic (Database Transaction)
* Saat kasir menekan tombol **"Bayar / Checkout"**, aplikasi melakukan beberapa tindakan sekaligus:
  1. Membuat rekor di tabel `sales` (faktur).
  2. Memasukkan rincian item ke tabel `sale_items`.
  3. Mengurangi kolom `stock` di tabel `products` sesuai jumlah beli.
  4. Mencegat dan mencatat riwayat di tabel `stock_movements`.
* **Aturan Atomic:** Seluruh 4 langkah di atas **harus dibungkus dalam satu Database Transaction (`db.transaction(...)`)**.
* Jika salah satu langkah gagal (misal: tiba-tiba stok produk di database kurang karena baru saja dibeli di kasir sebelah), maka **SELURUH proses transaksi dibatalkan (*rollback*)**. Tidak boleh ada tagihan yang tercipta tanpa berkurangnya stok, atau sebaliknya.

---

## 3. Validasi Stok Negatif
* Aplikasi **dilarang keras** membiarkan stok produk bernilai negatif (< 0).
* Validasi harus dilakukan di **2 lapis**:
  1. **Frontend (UI):** Tombol "Tambah ke Keranjang" dinonaktifkan jika `qty >= stock`.
  2. **Backend (Server Action / API):** Sebelum eksekusi checkout, server wajib mengecek ulang query stok terkini di database. Jika stok tidak cukup, kembalikan error status `400 Bad Request` atau `Insufficient Stock`.

---

## 4. Pembatasan Hak Akses (Role-Based Authorization)
* **Kasir dilarang:**
  * Mengakses rute `/products/new`, `/products/[id]/edit`, atau `/categories`.
  * Melakukan *delete* atau *update* pada transaksi yang sudah selesai.
  * Melakukan *manual stock adjustment* yang tidak melalui penjualan resmi.
* **Admin berhak:**
  * Mengakses seluruh rute dan melakukan mutasi data katalog serta melihat audit log.
* Setiap endpoint Route Handler atau Server Action yang bersifat mutasi **wajib memverifikasi session user dan role-nya di sisi server**, bukan hanya menyembunyikan tombol di UI!

---

## 5. Kalkulasi Keuangan
* `Subtotal Item` = `unit_price` × `quantity`.
* `Total Tagihan` = `Sum(Subtotal Items)` − `Discount`.
* `Change Amount (Kembalian)` = `Paid Amount` − `Total Tagihan`.
* Jika `Paid Amount` < `Total Tagihan`, transaksi tidak boleh diproses.
* Semua tipe uang di dalam database relasional disarankan menggunakan tipe `NUMERIC(12, 2)` atau `INTEGER` (menyimpan dalam satuan Rupiah penuh tanpa desimal floating-point error).
