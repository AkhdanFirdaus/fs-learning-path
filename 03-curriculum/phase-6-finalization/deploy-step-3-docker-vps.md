# 🐳 Langkah 3: Deploy ke VPS Menggunakan Docker (Masterclass Containerization)

Mengemas aplikasi ke dalam **Docker Container** adalah standar modern dalam *software engineering*. Dengan Docker, seluruh aplikasi beserta dependensi sistem operasinya dibungkus menjadi satu kesatuan yang terisolasi dan identik di segala mesin.

---

## 📚 Sub-Materi Mendalam: Fundamental Docker & Containerization

### 1. Apa itu Docker? (Container vs Virtual Machine)
Banyak pemula bertanya: *"Mengapa tidak pakai Virtual Machine (VM) biasa saja?"*

| Fitur | Virtual Machine (VM) | Docker Container |
| :--- | :--- | :--- |
| **Arsitektur** | Membawa Guest OS lengkap (Kernel sendiri) di atas Hypervisor. | Berbagi Kernel OS host (Host OS), hanya mengisolasi *user space*. |
| **Ukuran** | Sangat besar (berkisar antara beberapa GB hingga puluhan GB). | Sangat ringan (berkisar antara puluhan MB hingga ratusan MB). |
| **Waktu Boot** | Lambat (bisa memakan waktu hitungan menit). | Sangat cepat (hitung detik atau mili-detik). |
| **Konsumsi RAM/CPU**| Berat karena harus memelihara OS tamu yang duplikatif. | Sangat efisien, hampir setara dengan menjalankan native process. |

> [!IMPORTANT]
> **Solusi "It Works on My Machine":**  
> Pernahkah aplikasi berjalan lancar di laptop Anda, namun eror saat di-deploy ke server karena perbedaan versi Node.js atau library OS? **Docker menyelesaikan masalah ini 100%.** Jika sebuah image berjalan di laptop Anda, ia dijamin berjalan persis sama di server AWS, VPS DigitalOcean, ataupun Google Cloud.

---

### 2. Konsep Kunci Docker
* **Docker Image:** Cetakan biru (*blueprint*) atau *snapshot read-only* dari aplikasi Anda, termasuk kode, runtime Node.js, library sistem, dan konfigurasi environment.
* **Docker Container:** Instance aktif/hidup yang berjalan dari sebuah Docker Image. Satu image bisa dijalankan menjadi puluhan container simultan.
* **Dockerfile:** File teks berisi instruksi langkah demi langkah (*script*) bagaimana membangun sebuah Docker Image dari nol.
* **Docker Compose:** Tool orchestrator ringan berbasis YAML (`docker-compose.yml`) untuk mendefinisikan dan menjalankan sistem multi-container secara bersamaan (misal: Container Next.js + Container PostgreSQL + Container Nginx).

---

### 3. Rahasia Multi-Stage Build di Next.js
Jika Anda membangun image Next.js secara naif, ukurannya bisa mencapai **> 1.5 GB** karena menyertakan seluruh folder `node_modules` pengembangan dan file cache.

Dengan **Multi-Stage Build**, kita membagi `Dockerfile` menjadi 4 tahap terisolasi:
1. **`base`:** Menyiapkan sistem operasi minimal (Alpine Linux) dan Node.js.
2. **`deps`:** Menginstal dependensi dari `package-lock.json`.
3. **`builder`:** Melakukan kompilasi `npm run build`. Next.js memiliki mode `output: 'standalone'` yang melacak dan memisahkan hanya file dan library yang **benar-benar terpakai** saat runtime.
4. **`runner`:** Container produksi akhir yang **super ringan (< 150 MB)**. Tahap ini hanya menyalin hasil folder `standalone` dan `static` dari tahap *builder*, meninggalkan seluruh sisa `node_modules` mentah yang berat!

---

## 🛠️ Eksekusi Deployment Docker di VPS

### 1. Instalasi Docker & Docker Compose di VPS Ubuntu
Akses VPS Anda via SSH dan jalankan script instalasi resmi Docker Engine:
```bash
# Hapus versi lama jika ada
sudo apt-get remove docker docker-engine docker.io containerd runc -y

# Download dan instal Docker resmi
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh

# Tambahkan user Anda ke grup docker agar tidak perlu ketik 'sudo' terus-menerus
sudo usermod -aG docker $USER
newgrp docker

# Verifikasi instalasi
docker --version
docker compose version
```

### 2. Konfigurasi `next.config.ts` untuk Standalone Mode
Buka proyek lokal Anda dan pastikan opsi `output: 'standalone'` aktif pada file `next.config.ts`:
```typescript
import type { NextConfig } from "next";

const nextConfig: NextConfig = {
  output: "standalone", // Wajib diaktifkan untuk optimasi Docker
  images: {
    unoptimized: true, // Opsional jika tidak menggunakan Next Image Optimization eksternal
  },
};

export default nextConfig;
```

### 3. Pembuatan `Dockerfile` Production-Ready
Buat file bernama `Dockerfile` (tanpa ekstensi) di root directory proyek Anda:
```dockerfile
# --- STAGE 1: Base Image ---
FROM node:20-alpine AS base
WORKDIR /app
RUN apk add --no-cache libc6-compat

# --- STAGE 2: Install Dependencies ---
FROM base AS deps
COPY package.json package-lock.json ./
RUN npm ci

# --- STAGE 3: Build Application ---
FROM base AS builder
COPY --from=deps /app/node_modules ./node_modules
COPY . .
# Disable telemetry selama build
ENV NEXT_TELEMETRY_DISABLED 1
ENV NODE_ENV production
# Build aplikasi Next.js
RUN npm run build

# --- STAGE 4: Production Runner (Super Lightweight) ---
FROM base AS runner
WORKDIR /app

ENV NODE_ENV production
ENV NEXT_TELEMETRY_DISABLED 1
ENV PORT 3000
ENV HOSTNAME "0.0.0.0"

# Buat user non-root demi keamanan kontainer (Security Best Practice)
RUN addgroup --system --gid 1001 nodejs
RUN adduser --system --uid 1001 nextjs

# Salin aset publik dan file standalone hasil build
COPY --from=builder /app/public ./public
COPY --from=builder --chown=nextjs:nodejs /app/.next/standalone ./
COPY --from=builder --chown=nextjs:nodejs /app/.next/static ./.next/static

USER nextjs

EXPOSE 3000

CMD ["node", "server.js"]
```

### 4. Pembuatan `docker-compose.yml` (App + PostgreSQL + Nginx)
Buat file `docker-compose.yml` di root directory untuk mengatur seluruh ekosistem Mini POS dalam satu perintah:
```yaml
services:
  # 1. Database PostgreSQL Container
  postgres:
    image: postgres:16-alpine
    container_name: minipos-db
    restart: always
    environment:
      POSTGRES_USER: ${DB_USER:-minipos_user}
      POSTGRES_PASSWORD: ${DB_PASSWORD:-supersecretpassword}
      POSTGRES_DB: ${DB_NAME:-minipos_db}
    volumes:
      - postgres_data:/var/lib/postgresql/data
    networks:
      - minipos-net
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U ${DB_USER:-minipos_user} -d ${DB_NAME:-minipos_db}"]
      interval: 5s
      timeout: 5s
      retries: 5

  # 2. Next.js Web Application Container
  web:
    build:
      context: .
      dockerfile: Dockerfile
    container_name: minipos-web
    restart: always
    depends_on:
      postgres:
        condition: service_healthy
    environment:
      DATABASE_URL: postgresql://${DB_USER:-minipos_user}:${DB_PASSWORD:-supersecretpassword}@postgres:5432/${DB_NAME:-minipos_db}
      NEXTAUTH_SECRET: ${NEXTAUTH_SECRET:-kunci_rahasia_jwt_anda_yang_panjang}
      NEXTAUTH_URL: ${NEXTAUTH_URL:-http://localhost:3000}
      NODE_ENV: production
      PORT: 3000
    networks:
      - minipos-net

  # 3. Nginx Reverse Proxy Container (Opsional jika ingin Nginx dalam kontainer)
  nginx:
    image: nginx:alpine
    container_name: minipos-nginx
    restart: always
    ports:
      - "80:80"
    volumes:
      - ./nginx/conf.d:/etc/nginx/conf.d:ro
    depends_on:
      - web
    networks:
      - minipos-net

volumes:
  postgres_data:

networks:
  minipos-net:
    driver: bridge
```

### 5. Konfigurasi Nginx untuk Docker (`nginx/conf.d/default.conf`)
Buat folder `nginx/conf.d/` dan masukkan file `default.conf`:
```nginx
server {
    listen 80;
    server_name _;

    location / {
        proxy_pass http://web:3000; # Mengarah ke nama service 'web' di Docker Compose
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```

### 6. Build & Launch Sistem di VPS
1. Salin seluruh proyek Anda (termasuk `Dockerfile`, `docker-compose.yml`, dan folder `nginx/`) ke server VPS via Git atau `rsync/scp`.
2. Di dalam folder proyek di VPS, jalankan perintah ajaib Docker Compose:
   ```bash
   docker compose up -d --build
   ```
   *Penjelasan:* `-d` menjalankan container di latar belakang (*detached mode*), `--build` merakit ulang image dari kode terbaru.
3. Periksa status dan log container yang sedang berjalan:
   ```bash
   docker compose ps
   docker compose logs -f web
   ```
4. **Jalankan Migrasi Database di dalam Container:**  
   Karena database ada di dalam jaringan Docker, jalankan migrasi Drizzle dengan mengeksekusi perintah di dalam container `web`:
   ```bash
   docker compose exec web npx drizzle-kit migrate
   # Jalankan seeder admin
   docker compose exec web npx tsx src/db/seed.ts
   ```

---

## 🧹 Maintenance & Optimasi Docker di VPS
* **Melihat penggunaan sumber daya (RAM & CPU):**
  ```bash
  docker stats
  ```
* **Membersihkan sampah Image & Cache lama (Penting agar disk VPS tidak penuh):**
  ```bash
  docker system prune -a --volumes
  ```
* **Update & Re-deploy Aplikasi saat Ada Kode Baru:**
  ```bash
  git pull origin main
  docker compose up -d --build
  ```

---

## 🏆 Selamat! Anda Telah Menguasai 3 Metode Deployment!
Dengan menguasai Vercel (PaaS), Manual VPS (PM2/Nginx), dan Docker Containerization, Anda kini memiliki keahlian *DevOps & Deployment* yang sangat dicari di industri rekayasa perangkat lunak modern.

---

[← Kembali ke Langkah 2: Manual VPS](./deploy-step-2-manual-vps.md) | [📑 Daftar Silabus](../../README.md) | [🎓 Kembali ke Standar Kelulusan](../../01-overview/target-and-graduation-standards.md)
