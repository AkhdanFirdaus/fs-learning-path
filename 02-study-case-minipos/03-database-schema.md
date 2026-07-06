# 🗄️ Desain Schema Database Minimum (PostgreSQL + Drizzle ORM)

Aplikasi Mini POS membutuhkan minimal **6 tabel utama** yang dirancang secara normalisasi untuk menangani relasi pengguna, katalog barang, transaksi kasir, dan audit stok.

---

## 📊 Entity Relationship Diagram (ERD) & Relasi

```text
+--------------+          +-------------------+          +-----------------+
|  categories  | 1 <----* |     products      | 1 <----* | stock_movements |
+--------------+          +-------------------+          +-----------------+
                                    ^                             |
                                    |                             |
                                    *                             v
+--------------+          +-------------------+          +-----------------+
|    users     | 1 <----* |    sale_items     | *----> 1 |      sales      |
+--------------+          +-------------------+          +-----------------+
```

1. Satu **Category** memiliki banyak **Products** (One-to-Many).
2. Satu **Product** memiliki banyak riwayat **Stock Movements** (One-to-Many).
3. Satu **User (Kasir)** melayani banyak transaksi **Sales** (One-to-Many).
4. Satu transaksi **Sale** memiliki banyak **Sale Items** (One-to-Many).
5. Setiap **Sale Item** merujuk pada satu **Product** (Many-to-One).

---

## 📋 Spesifikasi Skema Tabel

### 1. `users` (Pengguna Sistem)
Menyimpan kredensial dan role untuk Admin dan Kasir.
```sql
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  email VARCHAR(150) UNIQUE NOT NULL,
  password_hash VARCHAR(255) NOT NULL,
  role VARCHAR(20) NOT NULL CHECK (role IN ('admin', 'cashier')),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 2. `categories` (Kategori Produk)
Pengelompokan barang (misal: Makanan, Minuman, Snack, Lainnya).
```sql
CREATE TABLE categories (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100) UNIQUE NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 3. `products` (Katalog Barang & Stok)
Menyimpan barang yang dijual beserta stok aktual.
```sql
CREATE TABLE products (
  id SERIAL PRIMARY KEY,
  category_id INTEGER REFERENCES categories(id) ON DELETE SET NULL,
  sku VARCHAR(50) UNIQUE NOT NULL,
  name VARCHAR(150) NOT NULL,
  price NUMERIC(12, 2) NOT NULL DEFAULT 0,
  stock INTEGER NOT NULL DEFAULT 0 CHECK (stock >= 0),
  is_active BOOLEAN DEFAULT TRUE,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 4. `sales` (Header Transaksi Penjualan / Faktur)
Mencatat informasi umum faktur pembayaran kasir.
```sql
CREATE TABLE sales (
  id SERIAL PRIMARY KEY,
  invoice_number VARCHAR(50) UNIQUE NOT NULL,
  cashier_id INTEGER REFERENCES users(id) ON DELETE SET NULL,
  subtotal NUMERIC(12, 2) NOT NULL DEFAULT 0,
  discount NUMERIC(12, 2) NOT NULL DEFAULT 0,
  total NUMERIC(12, 2) NOT NULL DEFAULT 0,
  paid_amount NUMERIC(12, 2) NOT NULL DEFAULT 0,
  change_amount NUMERIC(12, 2) NOT NULL DEFAULT 0,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 5. `sale_items` (Rincian Item Transaksi)
Mencatat barang apa saja yang dibeli dalam satu faktur.
> **Penting:** Kolom `product_name` dan `unit_price` disimpan di sini sebagai *snapshot historis*.
```sql
CREATE TABLE sale_items (
  id SERIAL PRIMARY KEY,
  sale_id INTEGER REFERENCES sales(id) ON DELETE CASCADE,
  product_id INTEGER REFERENCES products(id) ON DELETE SET NULL,
  product_name VARCHAR(150) NOT NULL,
  unit_price NUMERIC(12, 2) NOT NULL,
  quantity INTEGER NOT NULL CHECK (quantity > 0),
  subtotal NUMERIC(12, 2) NOT NULL
);
```

### 6. `stock_movements` (Audit Trail Stok Barang)
Mencatat setiap pergerakan stok masuk maupun keluar.
```sql
CREATE TABLE stock_movements (
  id SERIAL PRIMARY KEY,
  product_id INTEGER REFERENCES products(id) ON DELETE CASCADE,
  type VARCHAR(20) NOT NULL CHECK (type IN ('in', 'out', 'adjustment', 'sale')),
  quantity INTEGER NOT NULL,
  reference VARCHAR(100), -- Contoh: nomor faktur 'INV-001' atau 'MANUAL-ADJ'
  notes TEXT,
  created_by INTEGER REFERENCES users(id) ON DELETE SET NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---

## 🔧 Contoh Definisi Drizzle ORM (`src/db/schema/index.ts`)

Berikut adalah representasi skema di atas dalam format Drizzle ORM TypeScript:

```typescript
import { pgTable, serial, varchar, numeric, integer, boolean, timestamp, text } from "drizzle-orm/pg-core";

export const categories = pgTable("categories", {
  id: serial("id").primaryKey(),
  name: varchar("name", { length: 100 }).unique().notNull(),
  createdAt: timestamp("created_at").defaultNow(),
  updatedAt: timestamp("updated_at").defaultNow(),
});

export const products = pgTable("products", {
  id: serial("id").primaryKey(),
  categoryId: integer("category_id").references(() => categories.id),
  sku: varchar("sku", { length: 50 }).unique().notNull(),
  name: varchar("name", { length: 150 }).notNull(),
  price: numeric("price", { precision: 12, scale: 2 }).notNull().default("0"),
  stock: integer("stock").notNull().default(0),
  isActive: boolean("is_active").default(true),
  createdAt: timestamp("created_at").defaultNow(),
  updatedAt: timestamp("updated_at").defaultNow(),
});
```
