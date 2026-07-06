# 📅 Hari 24 — Inventory dan Stock Movement
**Fase 4: PostgreSQL, SQL, dan Drizzle ORM**

[← Hari 23](./day-23-repository-query.md) | [📑 Daftar Silabus](../../README.md) | [Hari 25 →](../phase-5-backend-integration/day-25-backend-crud.md)

---

### Tabel stock movement

```text
id
product_id
type
quantity
reference
created_at
created_by
```

### Tipe mutasi

```text
initial
purchase
sale
adjustment
return
```

### Business rule

* Stok keluar tidak boleh melebihi stok tersedia.
* Perubahan stok harus menghasilkan movement.
* Stock movement tidak boleh dihapus sembarangan.
* Koreksi dilakukan melalui adjustment baru.
* Quantity harus lebih besar dari nol.

Jangan hanya mengubah kolom `products.stock`. Tanpa movement log, tidak ada audit trail.

---

# Fase 5 — Backend dan Integrasi Full-Stack

---

## 📋 Checklist Target Hari Ini

- [ ] Memahami seluruh materi teori dan konsep pada **Hari 24: Inventory dan Stock Movement**
- [ ] Mengimplementasikan spesifikasi fitur dan tugas yang diinstruksikan
- [ ] Melakukan pengujian dan verifikasi fungsionalitas di lingkungan pengembangan lokal
- [ ] Menyimpan checkpoint progres dengan *git commit* (misal: `git commit -m "feat: complete day 24 inventory dan stock movement"`)


---

[← Hari 23](./day-23-repository-query.md) | [📑 Daftar Silabus](../../README.md) | [Hari 25 →](../phase-5-backend-integration/day-25-backend-crud.md)
