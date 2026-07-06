# 🏆 Target Akhir, Standar Kelulusan & Batasan Scope

Dokumen ini merangkum apa yang akan Anda capai di akhir kurikulum 30 hari, standar kompetensi yang diuji, serta batasan-batasan (*boundaries*) yang sengaja diterapkan agar Anda tidak terjebak dalam *scope creep*.

---

## 🚀 Target Akhir Aplikasi Mini POS
Aplikasi akhir yang berhasil dibangun dan di-deploy akan memiliki fitur lengkap berikut:
- [x] **Manajemen Produk & Kategori**: CRUD lengkap dengan pengelompokan kategori.
- [x] **Manajemen Stok & Inventory**: Pemantauan stok aktif dan pencatatan riwayat *stock movement*.
- [x] **Keranjang Belanja (Shopping Cart)**: Penambahan, pengurangan, dan kalkulasi subtotal instan.
- [x] **Checkout & Transaksi Kasir**: Pembayaran, penghitungan kembalian, dan pemotongan stok secara atomic.
- [x] **Riwayat & Detail Transaksi**: Laporan penjualan dengan nomor faktur dan snapshot item.
- [x] **Dashboard Penjualan**: Ringkasan performa penjualan dan statistik bisnis.
- [x] **Authentication & Authorization**: Keamanan akun dengan pembagian hak akses (Role: **Admin** vs **Kasir**).
- [x] **Database Production**: Menggunakan **PostgreSQL** dengan **Drizzle ORM** (migration & seeding).
- [x] **Quality Assurance**: Validasi berlapis (frontend + backend) dan unit testing dasar.
- [x] **Deployment**: Aplikasi live di cloud production yang siap didemonstrasikan.

---

## 🎓 Standar Kelulusan per Teknologi

### 1. JavaScript Fundamental & DOM
* Memahami tipe data dasar, array, object, function, module, dan *async code*.
* Bisa memisahkan *business logic* dari manipulasi DOM secara rapi.
* Bisa membaca, mendiagnosis, dan memperbaiki *error* dasar di browser console.

### 2. React & Component Architecture
* Memahami konsep *component*, *props*, *state*, dan *effect* (`useEffect`).
* Bisa membuat form yang terkontrol (*controlled components*) dan *shared state*.
* Mampu menentukan *state* yang benar-benar diperlukan dan menghindari *redundant state*.

### 3. Next.js App Router
* Memahami arsitektur dan routing pada Next.js App Router (`app/`).
* Mampu membedakan dengan tepat kapan menggunakan **Server Component** vs **Client Component** (`"use client"`).
* Bisa mengimplementasikan **Route Handler** (`api/...`) dan **Server Action** untuk mutasi data.
* Mampu membuat *protected route* dan *layouting* bersyarat.

### 4. Backend & Systems Logic
* Memahami siklus *request-response* dan HTTP status code standar.
* Mampu melakukan validasi data di sisi server (misal menggunakan Zod).
* Bisa menerapkan pola *service layer* dan *repository layer* yang bersih.
* Mampu mengeksekusi proses checkout secara **atomic** (menggunakan database transaction).
* Bisa menerapkan *authentication* dan *authorization* berbasis role.

### 5. Database Relasional & Drizzle ORM
* Bisa merancang tabel relasional, primary key, foreign key, dan index dasar.
* Mampu mendefinisikan schema Drizzle dengan tipe data TypeScript yang kuat.
* Bisa menghasilkan dan menjalankan *database migration* dengan aman via Drizzle Kit.
* Mampu membuat script *seeding* untuk data awal (admin & katalog contoh).
* Bisa melakukan *query* kompleks: `INSERT`, `SELECT`, `UPDATE`, `DELETE`, `JOIN`, serta `TRANSACTION`.

---

## 🛑 Batasan yang Sengaja Diterapkan (Scope Boundaries)

Untuk menjamin kelulusan dalam waktu 30 hari, teknologi dan arsitektur berikut **sengaja TIDAK dimasukkan**:
* ❌ Microservices & Kubernetes
* ❌ Redis & Caching layer eksternal
* ❌ Message queue (RabbitMQ/Kafka) & Event sourcing
* ❌ WebSocket (Real-time sync) & Offline synchronization
* ❌ Multi-tenant architecture
* ❌ Payment gateway nyata (Midtrans/Stripe/dll)
* ❌ Complex reporting & Big data analytics
* ❌ Redux / MobX / Zustand (Kita fokus pada React State/Context & Server State Next.js)
* ❌ GraphQL
* ❌ Clean architecture berlapis-lapis yang berlebihan (*over-engineering*) & Repository generik abstrak

> [!WARNING]
> **Mengapa dibatasi?**  
> Menambahkan semua elemen di atas dalam program 30 hari bukanlah sebuah ambisi, melainkan **kegagalan mengendalikan scope**. Kurikulum ini berorientasi pada kematangan fundamental, bukan tumpukan *buzzwords*.

---

## 📈 Hasil Realistis Setelah 30 Hari

Setelah menyelesaikan program ini, Anda mungkin belum menjadi *senior full-stack developer* dengan pengalaman bertahun-tahun. Namun, Anda **secara nyata dan terbukti mampu**:
1. Mendesain dan membangun antarmuka frontend modern yang responsif.
2. Mengembangkan API backend yang aman dan terstruktur.
3. Mendesain database relasional yang normatif untuk skala bisnis kecil-menengah.
4. Mengoperasikan PostgreSQL bersama Drizzle ORM secara *code-first*.
5. Menjalankan alur migrasi database dan manajemen state production.
6. Menerapkan keamanan *authentication* dan *role authorization*.
7. Memproses transaksi bisnis keuangan dan stok secara konsisten tanpa *race condition*.
8. Men-deploy dan merilis satu aplikasi full-stack live yang siap dijadikan portofolio unggulan.

> [!IMPORTANT]
> **Pergeseran Paradigma Kritis:**  
> Mulai Fase 4, **`localStorage` tidak lagi menjadi penyimpanan final!** `localStorage` hanya digunakan di awal untuk memahami konsep *persistence* dan menyimpan *temporary cart*. Seluruh data produk, pengguna, stok, serta transaksi final **wajib disimpan di dalam PostgreSQL**.
