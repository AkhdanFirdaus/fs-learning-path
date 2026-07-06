# 📅 Hari 36 — GraphQL Client (Apollo/Urql) & Real-time Subscriptions di POS
**Fase Tambahan: GraphQL & Real-time API Mastery**

[← Hari 35](./day-35-graphql-mutation-checkout.md) | [📑 Daftar Silabus](../../README.md) | [🎓 Standar Kelulusan](../../01-overview/target-and-graduation-standards.md)

---

## 🎯 Tujuan Hari Ini
Pada hari puncak dari **Fase Bonus GraphQL Mastery** ini, Anda akan mempelajari cara menghubungkan antarmuka UI React Next.js (Client Components) ke server GraphQL menggunakan library client modern (seperti **Urql** atau **Apollo Client**). Selain itu, kita akan membahas *killer feature* dari GraphQL untuk studi kasus POS: **Real-time Subscriptions (WebSockets)** untuk notifikasi stok menipis dan pembaruan antrian pesanan dapur (*Kitchen Display System*).

---

## 💡 Mengapa Real-time Subscriptions Sangat Penting di POS?
Bayangkan skenario toko ritel atau kafe yang sibuk:
1. **Kitchen Display System (KDS):** Saat kasir di depan menekan tombol *"Checkout"*, layar monitor di dapur harus **langsung menampilkan** pesanan baru tanpa koki harus merefresh halaman browser!
2. **Low Stock Notification:** Saat stok barang tinggal 2 unit karena baru saja dibeli di kasir A, layar kasir B dan layar gudang langsung mendapatkan peringatan kilat: *"⚠️ Stok Kopi Susu tinggal 2!"*

Inilah kekuatan **GraphQL Subscription** berteknologi WebSockets atau Server-Sent Events (SSE).

---

## 🛠️ Langkah Integrasi Client di Next.js (`"use client"`)

### 1. Instalasi Library Client (Urql)
Kita akan menggunakan **Urql** — GraphQL client modern yang super ringan, cepat, dan sangat bersahabat dengan Next.js App Router:
```bash
npm install urql @urql/next
```

### 2. Konfigurasi Urql Provider (`src/components/GraphQLProvider.tsx`)
Buat komponen provider agar seluruh Client Components di aplikasi Mini POS dapat melakukan query dan mutasi GraphQL dengan hooks:
```tsx
"use client";

import { UrqlProvider, ssrExchange, fetchExchange, createClient } from "@urql/next";
import { useMemo } from "react";

export function GraphQLProvider({ children }: { children: React.ReactNode }) {
  const [client, ssr] = useMemo(() => {
    const ssr = ssrExchange({
      isClient: typeof window !== "undefined",
    });
    const client = createClient({
      url: "/api/graphql",
      exchanges: [fetchExchange, ssr],
    });
    return [client, ssr];
  }, []);

  return (
    <UrqlProvider client={client} ssr={ssr}>
      {children}
    </UrqlProvider>
  );
}
```

### 3. Mengambil Data Katalog di Komponen Kasir (`useQuery`)
Di dalam komponen kasir Anda (`src/app/pos/page.tsx`), Anda kini dapat menggantikan pemanggilan REST API atau state manual dengan hook `useQuery`:
```tsx
"use client";

import { useQuery, useMutation } from "urql";

const GET_CATALOG_QUERY = /* GraphQL */ `
  query GetCashierCatalog($search: String) {
    products(search: $search) {
      id
      sku
      name
      price
      stock
      category {
        name
      }
    }
  }
`;

const PROCESS_CHECKOUT_MUTATION = /* GraphQL */ `
  mutation ProcessCashierCheckout($input: CreateOrderInput!) {
    processCheckout(input: $input) {
      success
      message
      changeAmount
    }
  }
`;

export default function CashierPOSPage() {
  const [result, reexecuteQuery] = useQuery({
    query: GET_CATALOG_QUERY,
    variables: { search: "" },
  });

  const [checkoutResult, executeCheckout] = useMutation(PROCESS_CHECKOUT_MUTATION);

  const { data, fetching, error } = result;

  if (fetching) return <div className="p-8 text-center animate-pulse">⏳ Memuat Katalog GraphQL...</div>;
  if (error) return <div className="p-8 text-red-500">❌ Error: {error.message}</div>;

  const handleCheckout = async (cartItems: any[], payment: number) => {
    const res = await executeCheckout({
      input: {
        cashierId: 1,
        paymentAmount: payment,
        items: cartItems.map(item => ({ productId: item.id, quantity: item.qty })),
      },
    });

    if (res.data?.processCheckout?.success) {
      alert(`🎉 ${res.data.processCheckout.message} (Kembalian: Rp ${res.data.processCheckout.changeAmount})`);
      reexecuteQuery({ requestPolicy: "network-only" }); // Refresh stok barang di layar kasir!
    }
  };

  return (
    <div className="p-6 grid grid-cols-3 gap-6">
      {/* Render Product Grid dari data.products */}
    </div>
  );
}
```

---

## 📡 Konsep GraphQL Subscription & Server-Sent Events (SSE) di Yoga
Untuk mengaktifkan fitur real-time di GraphQL Yoga tanpa perlu setup server WebSocket terpisah yang rumit, Yoga mendukung protokol **Server-Sent Events (SSE)** yang langsung berjalan di HTTP/2 Next.js!

Contoh definisi Subscription pada Skema Anda:
```typescript
type Subscription {
  orderCreated: Order!
  stockLowWarning: Product!
}
```
Ketika mutasi `processCheckout` berhasil di resolver server, Anda dapat memicu event pub/sub (`pubsub.publish('ORDER_CREATED', newOrder)`). Seluruh layar dapur yang sedang berlangganan (*subscribe*) akan menerima objek pesanan baru detik itu juga!

---

## 📋 Checklist Target Hari Ini
- [ ] Memahami perbedaan cara kerja GraphQL Client (Urql / Apollo) dibandingkan `fetch` REST biasa
- [ ] Berhasil menginstal `urql` dan memasang `<GraphQLProvider />` pada Root Layout aplikasi
- [ ] Berhasil mengambil data katalog produk di halaman kasir menggunakan hook `useQuery`
- [ ] Berhasil mengeksekusi mutasi checkout kasir dari UI menggunakan hook `useMutation`
- [ ] Memahami konsep Real-time Subscriptions (WebSockets/SSE) untuk implementasi *Kitchen Display System* dan notifikasi stok

---

## 🏆 Selamat! Anda Telah Menjadi Master Full-Stack & GraphQL!
Dengan menguasai kurikulum 30 Hari, Fase Tambahan Deployment Mastery (Hari 31–33), serta **Fase Bonus GraphQL Mastery (Hari 34–36)** ini, Anda tidak hanya memahami standar arsitektur REST dan Server Actions, tetapi juga siap merancang sistem API bergaya GraphQL yang efisien, strongly-typed, dan real-time untuk aplikasi berskala enterprise! 🎓🚀

---

[← Hari 35](./day-35-graphql-mutation-checkout.md) | [📑 Daftar Silabus](../../README.md) | [🎓 Standar Kelulusan](../../01-overview/target-and-graduation-standards.md)
