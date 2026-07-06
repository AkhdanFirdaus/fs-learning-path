# 📅 Hari 26 — Checkout dengan Database Transaction
**Fase 5: Backend dan Integrasi Full-Stack**

[← Hari 25](./day-25-backend-crud.md) | [📑 Daftar Silabus](../../README.md) | [Hari 27 →](./day-27-authentication.md)

---

Ini bagian backend terpenting.

### Proses checkout

1. Validasi cart tidak kosong.
2. Ambil produk dari database.
3. Periksa harga aktual.
4. Periksa stok aktual.
5. Hitung subtotal di server.
6. Hitung diskon di server.
7. Buat record sale.
8. Buat sale items.
9. Kurangi stok.
10. Buat stock movements.
11. Commit transaksi database.

### Aturan

Frontend tidak boleh menentukan total final secara sepihak.

Backend wajib menghitung ulang:

```text
harga
subtotal
diskon
total
stok
kembalian
```

Jika salah satu tahap gagal, seluruh checkout harus dibatalkan.

---

## 📋 Checklist Target Hari Ini

- [ ] Memahami seluruh materi teori dan konsep pada **Hari 26: Checkout dengan Database Transaction**
- [ ] Mengimplementasikan spesifikasi fitur dan tugas yang diinstruksikan
- [ ] Melakukan pengujian dan verifikasi fungsionalitas di lingkungan pengembangan lokal
- [ ] Menyimpan checkpoint progres dengan *git commit* (misal: `git commit -m "feat: complete day 26 checkout dengan database transaction"`)


---

[← Hari 25](./day-25-backend-crud.md) | [📑 Daftar Silabus](../../README.md) | [Hari 27 →](./day-27-authentication.md)
