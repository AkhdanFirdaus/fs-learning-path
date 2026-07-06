# 📅 Hari 21 — Schema Produk dan Kategori
**Fase 4: PostgreSQL, SQL, dan Drizzle ORM**

[← Hari 20](./day-20-setup-drizzle.md) | [📑 Daftar Silabus](../../README.md) | [Hari 22 →](./day-22-migration-seed.md)

---

### Tabel kategori

```text
id
name
created_at
updated_at
```

### Tabel produk

```text
id
category_id
sku
name
price
stock
is_active
created_at
updated_at
```

### Constraint

* `sku` harus unik.
* `price` harus positif.
* `stock` tidak boleh negatif.
* `category_id` harus mengarah ke kategori valid.

### Latihan

* Insert produk.
* Select semua produk.
* Filter produk aktif.
* Search nama produk.
* Update harga.
* Soft delete menggunakan `is_active`.

---

## 📋 Checklist Target Hari Ini

- [ ] Memahami seluruh materi teori dan konsep pada **Hari 21: Schema Produk dan Kategori**
- [ ] Mengimplementasikan spesifikasi fitur dan tugas yang diinstruksikan
- [ ] Melakukan pengujian dan verifikasi fungsionalitas di lingkungan pengembangan lokal
- [ ] Menyimpan checkpoint progres dengan *git commit* (misal: `git commit -m "feat: complete day 21 schema produk dan kategori"`)


---

[← Hari 20](./day-20-setup-drizzle.md) | [📑 Daftar Silabus](../../README.md) | [Hari 22 →](./day-22-migration-seed.md)
