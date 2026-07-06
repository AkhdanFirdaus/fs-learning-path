# 📅 Hari 34 — Fundamental GraphQL, Setup Apollo/Yoga di Next.js & Query Katalog
**Fase Tambahan: GraphQL & Real-time API Mastery**

[← Hari 33 (Docker Deploy)](../phase-7-deployment-mastery/day-33-deploy-docker-vps.md) | [📑 Daftar Silabus](../../README.md) | [Hari 35 →](./day-35-graphql-mutation-checkout.md)

---

## 🎯 Tujuan Hari Ini
Apakah studi kasus **Mini POS** cukup untuk menguasai GraphQL? **Sangat Cukup dan Ideal!**  
Pada hari ke-34 ini, kita memulai eksplorasi **GraphQL** sebagai alternatif atau pendamping REST API dan Server Actions. Anda akan mempelajari mengapa struktur data POS yang relasional (Kategori → Produk → Order → Order Item) merupakan tempat latihan paling sempurna untuk GraphQL Query dan pencegahan masalah *Over-fetching* serta *Under-fetching* (N+1 Problem).

---

## 💡 Mengapa Mini POS Sangat Cocok untuk GraphQL?

Dalam REST API konvensional, jika layar kasir ingin menampilkan daftar transaksi beserta detail barang, nama kategori, dan sisa stok barang tersebut, browser mungkin harus memanggil banyak endpoint secara beruntun:
1. `GET /api/orders` (Dapatkan daftar order)
2. `GET /api/orders/:id/items` (Dapatkan item per order — N kali panggilan!)
3. `GET /api/products/:id` (Dapatkan detail produk untuk tahu stok sekarang)

Dengan **GraphQL**, Anda cukup mengirimkan **1 buah Query tunggal** dari browser kasir, dan server akan merespons dengan struktur JSON yang persis sama dengan bentuk query Anda:
```graphql
query GetCashierScreenData {
  categories {
    id
    name
    products {
      id
      name
      price
      stock
    }
  }
}
```

---

## 🛠️ Langkah Implementasi di Next.js App Router

### 1. Instalasi Library GraphQL & Server (GraphQL Yoga / Apollo)
Kita akan menggunakan **GraphQL Yoga** (atau Apollo Server) yang sangat ringan dan mudah diintegrasikan ke dalam Next.js Route Handler (`app/api/graphql/route.ts`):
```bash
npm install graphql graphql-yoga
```

### 2. Definisi Skema GraphQL (`typeDefs`)
Buat file skema di `src/graphql/schema.ts` yang memetakan tabel Drizzle ORM kita ke tipe data GraphQL:
```typescript
export const typeDefs = /* GraphQL */ `
  type Category {
    id: ID!
    name: String!
    description: String
    products: [Product!]!
  }

  type Product {
    id: ID!
    sku: String!
    name: String!
    price: Float!
    stock: Int!
    category: Category
  }

  type Query {
    products(search: String, categoryId: ID): [Product!]!
    product(id: ID!): Product
    categories: [Category!]!
  }
`;
```

### 3. Pembuatan Resolver yang Terhubung ke Drizzle ORM
Buat file resolver di `src/graphql/resolvers.ts` yang mengeksekusi query database menggunakan `db.select()`:
```typescript
import { db } from "@/db";
import { products, categories } from "@/db/schema";
import { eq, ilike, and } from "drizzle-orm";

export const resolvers = {
  Query: {
    products: async (_, { search, categoryId }) => {
      let conditions = [];
      if (search) conditions.push(ilike(products.name, `%${search}%`));
      if (categoryId) conditions.push(eq(products.categoryId, Number(categoryId)));
      
      return await db.query.products.findMany({
        where: and(...conditions),
        with: {
          category: true, // Auto-join ke tabel kategori!
        },
      });
    },
    categories: async () => {
      return await db.query.categories.findMany({
        with: {
          products: true,
        },
      });
    },
  },
};
```

### 4. Setup Endpoint Route Handler (`src/app/api/graphql/route.ts`)
```typescript
import { createYoga, createSchema } from "graphql-yoga";
import { typeDefs } from "@/graphql/schema";
import { resolvers } from "@/graphql/resolvers";

const { handleRequest } = createYoga({
  schema: createSchema({
    typeDefs,
    resolvers,
  }),
  graphqlEndpoint: "/api/graphql",
  fetchAPI: { Response },
});

export { handleRequest as GET, handleRequest as POST };
```

---

## 🔍 Pengujian dengan GraphiQL Studio
1. Jalankan server lokal: `npm run dev`.
2. Buka browser dan navigasikan ke `http://localhost:3000/api/graphql`.
3. Anda akan melihat antarmuka **GraphiQL Explorer** yang indah! Coba jalankan query berikut:
   ```graphql
   query TestPOSCatalog {
     categories {
       name
       products {
         sku
         name
         price
         stock
       }
     }
   }
   ```
4. Periksa betapa cepatnya server mengembalikan data bersarang (*nested data*) dengan tipe data yang terjamin!

---

## 📋 Checklist Target Hari Ini
- [ ] Memahami konsep dasar GraphQL: Schema, Type Definitions (`typeDefs`), Resolvers, dan Query
- [ ] Berhasil menginstal library `graphql` dan `graphql-yoga` di dalam proyek Next.js
- [ ] Berhasil mendefinisikan skema GraphQL untuk entitas `Product` dan `Category`
- [ ] Berhasil menulis Resolver yang terhubung dengan Drizzle ORM Relational Query (`db.query`)
- [ ] Berhasil membuka GraphiQL Studio di `/api/graphql` dan mengeksekusi query katalog produk

---

[← Hari 33 (Docker Deploy)](../phase-7-deployment-mastery/day-33-deploy-docker-vps.md) | [📑 Daftar Silabus](../../README.md) | [Hari 35 →](./day-35-graphql-mutation-checkout.md)
