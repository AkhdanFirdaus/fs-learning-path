# 📅 Hari 23 — Repository dan Query Layer
**Fase 4: PostgreSQL, SQL, dan Drizzle ORM**

[← Hari 22](./day-22-migration-seed.md) | [📑 Daftar Silabus](../../README.md) | [Hari 24 →](./day-24-inventory-stock.md)

---

### Struktur

```text
src/
├── db/
├── repositories/
│   ├── product-repository.ts
│   ├── inventory-repository.ts
│   └── sale-repository.ts
├── services/
│   ├── product-service.ts
│   ├── inventory-service.ts
│   └── checkout-service.ts
└── actions/
```

### Tanggung jawab

#### Repository

* Berkomunikasi dengan Drizzle.
* Menjalankan query.
* Mengembalikan data.

#### Service

* Menjalankan business rule.
* Menggabungkan beberapa repository.
* Menangani proses checkout.
* Melempar domain error.

#### UI atau Action

* Membaca input.
* Memanggil service.
* Mengubah hasil menjadi response.

Jangan menulis query database langsung di setiap React component.

---

## 📋 Checklist Target Hari Ini

- [ ] Memahami seluruh materi teori dan konsep pada **Hari 23: Repository dan Query Layer**
- [ ] Mengimplementasikan spesifikasi fitur dan tugas yang diinstruksikan
- [ ] Melakukan pengujian dan verifikasi fungsionalitas di lingkungan pengembangan lokal
- [ ] Menyimpan checkpoint progres dengan *git commit* (misal: `git commit -m "feat: complete day 23 repository dan query layer"`)


---

[← Hari 22](./day-22-migration-seed.md) | [📑 Daftar Silabus](../../README.md) | [Hari 24 →](./day-24-inventory-stock.md)
