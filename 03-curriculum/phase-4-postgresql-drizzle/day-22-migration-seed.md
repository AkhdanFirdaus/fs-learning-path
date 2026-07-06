# 📅 Hari 22 — Migration dan Seed
**Fase 4: PostgreSQL, SQL, dan Drizzle ORM**

[← Hari 21](./day-21-schema-product.md) | [📑 Daftar Silabus](../../README.md) | [Hari 23 →](./day-23-repository-query.md)

---

### Workflow

```bash
npx drizzle-kit generate
npx drizzle-kit migrate
```

### Seed data

Buat:

* Dua akun.
* Lima kategori.
* Dua puluh produk.
* Stok awal.
* Beberapa transaksi contoh.

### Prinsip

* Schema adalah source of truth.
* Migration disimpan di Git.
* Jangan mengedit database production secara manual.
* Seed development harus dapat dijalankan ulang dengan aman.

---

## 📋 Checklist Target Hari Ini

- [ ] Memahami seluruh materi teori dan konsep pada **Hari 22: Migration dan Seed**
- [ ] Mengimplementasikan spesifikasi fitur dan tugas yang diinstruksikan
- [ ] Melakukan pengujian dan verifikasi fungsionalitas di lingkungan pengembangan lokal
- [ ] Menyimpan checkpoint progres dengan *git commit* (misal: `git commit -m "feat: complete day 22 migration dan seed"`)


---

[← Hari 21](./day-21-schema-product.md) | [📑 Daftar Silabus](../../README.md) | [Hari 23 →](./day-23-repository-query.md)
