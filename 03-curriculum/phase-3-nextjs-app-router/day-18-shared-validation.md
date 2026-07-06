# 📅 Hari 18 — Validasi Bersama
**Fase 3: Next.js App Router**

[← Hari 17](./day-17-server-action.md) | [📑 Daftar Silabus](../../README.md) | [Hari 19 →](../phase-4-postgresql-drizzle/day-19-relational-db.md)

---

Gunakan Zod atau validasi manual terstruktur.

### Schema

```ts
const productSchema = {
  name: "required",
  sku: "required and unique",
  price: "positive integer",
  stock: "non-negative integer"
};
```

### Validasi dilakukan pada:

1. Form frontend.
2. Server Action atau Route Handler.
3. Database constraint.

Validasi frontend tidak boleh dianggap sebagai perlindungan backend.

---

# Fase 4 — PostgreSQL, SQL, dan Drizzle ORM

---

## 📋 Checklist Target Hari Ini

- [ ] Memahami seluruh materi teori dan konsep pada **Hari 18: Validasi Bersama**
- [ ] Mengimplementasikan spesifikasi fitur dan tugas yang diinstruksikan
- [ ] Melakukan pengujian dan verifikasi fungsionalitas di lingkungan pengembangan lokal
- [ ] Menyimpan checkpoint progres dengan *git commit* (misal: `git commit -m "feat: complete day 18 validasi bersama"`)


---

[← Hari 17](./day-17-server-action.md) | [📑 Daftar Silabus](../../README.md) | [Hari 19 →](../phase-4-postgresql-drizzle/day-19-relational-db.md)
