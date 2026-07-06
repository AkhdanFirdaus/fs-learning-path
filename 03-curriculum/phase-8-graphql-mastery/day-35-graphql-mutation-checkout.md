# 📅 Hari 35 — Mutasi GraphQL & Integrasi Transaksi Atomic POS
**Fase Tambahan: GraphQL & Real-time API Mastery**

[← Hari 34](./day-34-graphql-setup-query.md) | [📑 Daftar Silabus](../../README.md) | [Hari 36 →](./day-36-graphql-client-subscription.md)

---

## 🎯 Tujuan Hari Ini
Setelah berhasil mengambil data (*fetching*) menggunakan GraphQL Query di Hari ke-34, hari ini kita akan menguasai cara mengubah, menambah, dan memanipulasi data melalui **GraphQL Mutation**. Kita akan mengimplementasikan mutasi untuk penambahan produk baru serta mutasi kritis untuk **Checkout Kasir POS** yang melibatkan *database transaction atomic*.

---

## 🛠️ Langkah Implementasi Mutasi POS

### 1. Penambahan Input Types dan Mutation pada Skema
Buka kembali file `src/graphql/schema.ts` dan tambahkan definisi `input` serta tipe `Mutation`:
```typescript
export const typeDefs = /* GraphQL */ `
  # ... (Tipe Category dan Product dari Hari 34 tetap ada)

  type OrderItem {
    id: ID!
    productId: ID!
    quantity: Int!
    unitPrice: Float!
    product: Product
  }

  type Order {
    id: ID!
    invoiceNumber: String!
    totalAmount: Float!
    createdAt: String!
    items: [OrderItem!]!
  }

  # Input khusus untuk pengiriman data belanjaan kasir
  input OrderItemInput {
    productId: ID!
    quantity: Int!
  }

  input CreateOrderInput {
    cashierId: ID!
    items: [OrderItemInput!]!
    paymentAmount: Float!
  }

  type CheckoutPayload {
    success: Boolean!
    message: String!
    order: Order
    changeAmount: Float
  }

  type Mutation {
    createProduct(sku: String!, name: String!, price: Float!, stock: Int!, categoryId: ID!): Product!
    updateStock(productId: ID!, newStock: Int!): Product!
    processCheckout(input: CreateOrderInput!): CheckoutPayload!
  }
`;
```

### 2. Implementasi Resolver untuk Mutasi Atomic (`processCheckout`)
Buka `src/graphql/resolvers.ts` dan tambahkan objek `Mutation` yang menggunakan `db.transaction()` milik Drizzle ORM agar spesifikasi *Business Rules* POS kita tetap patuh 100%:

```typescript
import { db } from "@/db";
import { products, orders, orderItems } from "@/db/schema";
import { eq, sql } from "drizzle-orm";

export const resolvers = {
  Query: {
    // ... (Resolver Query dari Hari 34)
  },
  Mutation: {
    createProduct: async (_, { sku, name, price, stock, categoryId }) => {
      const [newProduct] = await db.insert(products).values({
        sku,
        name,
        price: Number(price),
        stock: Number(stock),
        categoryId: Number(categoryId),
      }).returning();
      return newProduct;
    },

    processCheckout: async (_, { input }) => {
      // Jalankan seluruh proses dalam satu Database Transaction (ACID)
      return await db.transaction(async (tx) => {
        let calculatedTotal = 0;
        const itemDetails = [];

        // 1. Verifikasi stok & hitung subtotal dengan harga aktual saat ini (Price Snapshot)
        for (const item of input.items) {
          const product = await tx.query.products.findFirst({
            where: eq(products.id, Number(item.productId)),
          });

          if (!product || product.stock < item.quantity) {
            throw new Error(`Stok produk ${product?.name || item.productId} tidak mencukupi!`);
          }

          calculatedTotal += product.price * item.quantity;
          itemDetails.push({
            productId: product.id,
            quantity: item.quantity,
            unitPrice: product.price,
          });

          // 2. Potong stok produk secara atomic
          await tx.update(products)
            .set({ stock: sql`${products.stock} - ${item.quantity}` })
            .where(eq(products.id, product.id));
        }

        // 3. Buat record Order utama
        const invoiceNum = `INV-${Date.now()}`;
        const [newOrder] = await tx.insert(orders).values({
          invoiceNumber: invoiceNum,
          totalAmount: calculatedTotal,
          cashierId: Number(input.cashierId),
        }).returning();

        // 4. Buat record Order Items (Snapshot harga)
        for (const detail of itemDetails) {
          await tx.insert(orderItems).values({
            orderId: newOrder.id,
            productId: detail.productId,
            quantity: detail.quantity,
            unitPrice: detail.unitPrice,
          });
        }

        const change = input.paymentAmount - calculatedTotal;

        return {
          success: true,
          message: "Transaksi checkout berhasil diproses!",
          order: {
            ...newOrder,
            items: itemDetails,
          },
          changeAmount: change >= 0 ? change : 0,
        };
      });
    },
  },
};
```

---

## 🔍 Pengujian Mutasi Checkout di GraphiQL
Buka studio di `/api/graphql` dan coba lakukan simulasi transaksi kasir dengan mengirimkan GraphQL Mutation berikut:
```graphql
mutation TestKasirCheckout {
  processCheckout(
    input: {
      cashierId: 1
      paymentAmount: 100000
      items: [
        { productId: 1, quantity: 2 }
        { productId: 2, quantity: 1 }
      ]
    }
  ) {
    success
    message
    changeAmount
    order {
      invoiceNumber
      totalAmount
      items {
        quantity
        unitPrice
      }
    }
  }
}
```
Jika berhasil, Anda akan menerima respons JSON seketika dengan kembalian uang (*changeAmount*) dan nomor faktur yang baru saja dibentuk, dan stok produk di database PostgreSQL Anda dijamin telah berkurang!

---

## 📋 Checklist Target Hari Ini
- [ ] Memahami sintaks input types dan Mutation pada GraphQL
- [ ] Berhasil menambahkan definisi `Mutation` untuk `createProduct` dan `processCheckout`
- [ ] Berhasil mengimplementasikan resolver mutasi kasir menggunakan `db.transaction()` Drizzle ORM
- [ ] Berhasil memverifikasi bahwa aturan bisnis (stok minus gagal, snapshot harga persisten) dipatuhi oleh GraphQL
- [ ] Berhasil menjalankan pengujian mutasi dari antarmuka GraphiQL Studio

---

[← Hari 34](./day-34-graphql-setup-query.md) | [📑 Daftar Silabus](../../README.md) | [Hari 36 →](./day-36-graphql-client-subscription.md)
