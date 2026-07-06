# 📅 Hari 19 — Fundamental Database Relasional
**Fase 4: PostgreSQL, SQL, dan Drizzle ORM**

[← Hari 18](../phase-3-nextjs-app-router/day-18-shared-validation.md) | [📑 Daftar Silabus](../../README.md) | [Hari 20 →](./day-20-setup-drizzle.md)

---

### Materi

* Table.
* Row.
* Column.
* Primary key.
* Foreign key.
* Unique constraint.
* Index.
* One-to-many.
* Many-to-many.
* Transaction database.

### Entity POS

```text
users
categories
products
stock_movements
sales
sale_items
```

### Relasi

```text
categories 1 ─── n products
products   1 ─── n stock_movements
users      1 ─── n sales
sales      1 ─── n sale_items
products   1 ─── n sale_items
```

---

## 📋 Checklist Target Hari Ini

- [ ] Memahami seluruh materi teori dan konsep pada **Hari 19: Fundamental Database Relasional**
- [ ] Mengimplementasikan spesifikasi fitur dan tugas yang diinstruksikan
- [ ] Melakukan pengujian dan verifikasi fungsionalitas di lingkungan pengembangan lokal
- [ ] Menyimpan checkpoint progres dengan *git commit* (misal: `git commit -m "feat: complete day 19 fundamental database relasional"`)


---

[← Hari 18](../phase-3-nextjs-app-router/day-18-shared-validation.md) | [📑 Daftar Silabus](../../README.md) | [Hari 20 →](./day-20-setup-drizzle.md)
