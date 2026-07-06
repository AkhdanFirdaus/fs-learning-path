# 📋 Checklist Fase 6: Penyelesaian, Security Review & Deployment (Hari 29–30)

[← Kembali ke Dashboard Progres](daily-progress-tracker.md) | [📑 Daftar Silabus](../README.md)

---

## 📌 Hari 29: Testing dan Security Review
- [ ] Lakukan pengujian akhir dari sudut pandang pengguna nyata (*end-to-end testing* sederhana)
- [ ] Periksa penanganan error (*error boundary* & pesan error yang ramah pengguna)
- [ ] Audit keamanan: pastikan tidak ada *hardcoded secret* atau kata sandi di dalam kode repository
- [ ] Periksa loading state, empty state (katalog kosong), dan penanganan tombol saat proses *submit*

## 📌 Hari 30: Refactoring Final, Dokumentasi README, dan Deployment Cloud
- [ ] Lakukan pembersihan kode: hapus `console.log` sensitif dan impor yang tidak terpakai
- [ ] Lengkapi file `README.md` dengan instalasi, konfigurasi `.env`, dan tangkapan layar aplikasi
- [ ] Deploy database PostgreSQL ke cloud (Neon / Supabase / Railway)
- [ ] Deploy aplikasi Next.js ke cloud production (Vercel / Railway / Docker)
- [ ] Lakukan verifikasi akhir di URL production: login, checkout barang, dan pastikan stok berkurang persisten!

---
[← Kembali ke Dashboard Progres](daily-progress-tracker.md)
