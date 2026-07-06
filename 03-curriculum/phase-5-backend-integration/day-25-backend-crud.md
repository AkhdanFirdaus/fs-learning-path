# 📅 Hari 25 — Backend CRUD Produk
**Fase 5: Backend dan Integrasi Full-Stack**

[← Hari 24](../phase-4-postgresql-drizzle/day-24-inventory-stock.md) | [📑 Daftar Silabus](../../README.md) | [Hari 26 →](./day-26-db-transaction.md)

---

Hubungkan Product Management dengan PostgreSQL.

### Endpoint

```text
GET    /api/products
GET    /api/products/:id
POST   /api/products
PATCH  /api/products/:id
DELETE /api/products/:id
```

### Response error

```json
{
  "error": {
    "code": "PRODUCT_NOT_FOUND",
    "message": "Product was not found"
  }
}
```

### Status code

```text
200 OK
201 Created
400 Bad Request
404 Not Found
409 Conflict
500 Internal Server Error
```

### Target

Tidak ada lagi data produk yang berasal dari array atau localStorage.

---

## 📋 Checklist Target Hari Ini

- [ ] Memahami seluruh materi teori dan konsep pada **Hari 25: Backend CRUD Produk**
- [ ] Mengimplementasikan spesifikasi fitur dan tugas yang diinstruksikan
- [ ] Melakukan pengujian dan verifikasi fungsionalitas di lingkungan pengembangan lokal
- [ ] Menyimpan checkpoint progres dengan *git commit* (misal: `git commit -m "feat: complete day 25 backend crud produk"`)


---

[← Hari 24](../phase-4-postgresql-drizzle/day-24-inventory-stock.md) | [📑 Daftar Silabus](../../README.md) | [Hari 26 →](./day-26-db-transaction.md)
