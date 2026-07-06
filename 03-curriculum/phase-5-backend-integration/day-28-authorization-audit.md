# 📅 Hari 28 — Authorization dan Audit
**Fase 5: Backend dan Integrasi Full-Stack**

[← Hari 27](./day-27-authentication.md) | [📑 Daftar Silabus](../../README.md) | [Hari 29 →](../phase-6-finalization/day-29-testing-security.md)

---

### Role

```text
admin
cashier
```

### Backend authorization

* Admin dapat mengelola produk.
* Kasir tidak dapat membuat atau menghapus produk.
* Admin dan kasir dapat melakukan checkout.
* User yang belum login tidak dapat mengakses dashboard.
* Setiap transaksi menyimpan user kasir.

### Audit data

Simpan minimal:

```text
created_by
created_at
updated_at
```

Untuk stock adjustment, simpan alasan perubahan.

Menyembunyikan tombol di frontend bukan authorization. Backend tetap harus memeriksa role setiap request atau mutation.

---

# Fase 6 — Penyelesaian

---

## 📋 Checklist Target Hari Ini

- [ ] Memahami seluruh materi teori dan konsep pada **Hari 28: Authorization dan Audit**
- [ ] Mengimplementasikan spesifikasi fitur dan tugas yang diinstruksikan
- [ ] Melakukan pengujian dan verifikasi fungsionalitas di lingkungan pengembangan lokal
- [ ] Menyimpan checkpoint progres dengan *git commit* (misal: `git commit -m "feat: complete day 28 authorization dan audit"`)


---

[← Hari 27](./day-27-authentication.md) | [📑 Daftar Silabus](../../README.md) | [Hari 29 →](../phase-6-finalization/day-29-testing-security.md)
