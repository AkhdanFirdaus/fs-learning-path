# 📅 Hari 29 — Testing dan Security Review
**Fase 6: Penyelesaian**

[← Hari 28](../phase-5-backend-integration/day-28-authorization-audit.md) | [📑 Daftar Silabus](../../README.md) | [Hari 30 →](./day-30-refactoring-deploy.md)

---

### Unit test

Uji:

* Perhitungan subtotal.
* Diskon.
* Kembalian.
* Validasi stok.
* Validasi quantity.
* Role permission.
* Status produk.
* Pembuatan nomor transaksi.

### Integration test

Uji:

* Create product.
* Duplicate SKU.
* Checkout berhasil.
* Checkout dengan stok kurang.
* Checkout dengan produk tidak aktif.
* User tanpa izin mengubah produk.

### Security checklist

* Input divalidasi di server.
* Query menggunakan Drizzle, bukan interpolasi SQL mentah.
* Password di-hash.
* Secret tidak berada di repository.
* Error database tidak dikirim mentah ke client.
* Route dilindungi authentication.
* Authorization diperiksa di backend.
* Harga dihitung ulang di server.
* Cookie session memiliki konfigurasi aman.
* Tidak menggunakan `innerHTML` untuk input pengguna.

---

## 📋 Checklist Target Hari Ini

- [ ] Memahami seluruh materi teori dan konsep pada **Hari 29: Testing dan Security Review**
- [ ] Mengimplementasikan spesifikasi fitur dan tugas yang diinstruksikan
- [ ] Melakukan pengujian dan verifikasi fungsionalitas di lingkungan pengembangan lokal
- [ ] Menyimpan checkpoint progres dengan *git commit* (misal: `git commit -m "feat: complete day 29 testing dan security review"`)


---

[← Hari 28](../phase-5-backend-integration/day-28-authorization-audit.md) | [📑 Daftar Silabus](../../README.md) | [Hari 30 →](./day-30-refactoring-deploy.md)
