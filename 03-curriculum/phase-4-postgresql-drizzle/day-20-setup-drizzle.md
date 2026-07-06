# 📅 Hari 20 — Setup PostgreSQL dan Drizzle
**Fase 4: PostgreSQL, SQL, dan Drizzle ORM**

[← Hari 19](./day-19-relational-db.md) | [📑 Daftar Silabus](../../README.md) | [Hari 21 →](./day-21-schema-product.md)

---

### Package

```bash
npm install drizzle-orm pg
npm install -D drizzle-kit @types/pg
```

### Environment

```env
DATABASE_URL=postgresql://user:password@localhost:5432/mini_pos
```

### Struktur database

```text
src/
└── db/
    ├── index.ts
    ├── schema/
    │   ├── users.ts
    │   ├── products.ts
    │   ├── inventory.ts
    │   └── sales.ts
    └── seed.ts

drizzle/
drizzle.config.ts
```

Jangan melakukan commit file `.env`.

---

## 📋 Checklist Target Hari Ini

- [ ] Memahami seluruh materi teori dan konsep pada **Hari 20: Setup PostgreSQL dan Drizzle**
- [ ] Mengimplementasikan spesifikasi fitur dan tugas yang diinstruksikan
- [ ] Melakukan pengujian dan verifikasi fungsionalitas di lingkungan pengembangan lokal
- [ ] Menyimpan checkpoint progres dengan *git commit* (misal: `git commit -m "feat: complete day 20 setup postgresql dan drizzle"`)


---

[← Hari 19](./day-19-relational-db.md) | [📑 Daftar Silabus](../../README.md) | [Hari 21 →](./day-21-schema-product.md)
