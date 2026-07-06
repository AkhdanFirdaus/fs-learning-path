# 🖥️ Langkah 2: Deploy Manual ke VPS (Ubuntu, Nginx, PM2 & SSL)

Mengelola *Virtual Private Server* (VPS) sendiri memberikan Anda kontrol penuh atas arsitektur sistem, efisiensi biaya untuk lalu lintas tinggi, serta pemahaman mendalam tentang bagaimana sebuah server web bekerja di bawah kap mesin (*under-the-hood*).

---

## 🏛️ Arsitektur Server Manual

```text
[ Internet / Browser User ]
            │
            ▼
┌────────────────────────────────────────────────────────┐
│ VPS Ubuntu 24.04 LTS (e.g., DigitalOcean / IDCloudHost)│
│                                                        │
│   [ UFW Firewall ] (Port 80 HTTP & 443 HTTPS Open)     │
│          │                                             │
│          ▼                                             │
│   [ Nginx Reverse Proxy & SSL Let's Encrypt ]         │
│          │ (Forwarding dari port 80/443 ke 3000)       │
│          ▼                                             │
│   [ PM2 Process Manager ]                              │
│          │                                             │
│          ▼                                             │
│   [ Next.js Node.js Server ] (Running on 127.0.0.1:3000)│
│          │                                             │
│          ▼                                             │
│   [ PostgreSQL Database ] (Local Unix Socket / Cloud)  │
└────────────────────────────────────────────────────────┘
```

---

## 🛠️ Langkah-Langkah Setup VPS

### 1. Provisioning & Keamanan Dasar Server (Ubuntu 22.04 / 24.04)
1. Akses server via SSH:
   ```bash
   ssh root@ip-address-vps-anda
   ```
2. Perbarui seluruh paket sistem:
   ```bash
   apt update && apt upgrade -y
   ```
3. Buat user non-root demi keamanan (misal: `deployer`):
   ```bash
   adduser deployer
   usermod -aG sudo deployer
   su - deployer
   ```
4. Konfigurasi Firewall (UFW):
   ```bash
   sudo ufw allow OpenSSH
   sudo ufw allow 'Nginx Full'
   sudo ufw enable
   sudo ufw status
   ```

### 2. Instalasi Node.js (via NVM) & Git
Instal Node.js versi LTS (v20+) menggunakan Node Version Manager (NVM):
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
source ~/.bashrc
nvm install 20
nvm use 20
node -v && npm -v
sudo apt install git -y
```

### 3. Instalasi & Setup PostgreSQL Lokal di VPS (Opsional)
Jika Anda tidak menggunakan cloud DB dan ingin menjalankan PostgreSQL langsung di dalam VPS:
```bash
sudo apt install postgresql postgresql-contrib -y
sudo systemctl start postgresql
sudo systemctl enable postgresql

# Masuk ke shell postgres dan buat user serta database
sudo -u postgres psql
```
Di dalam prompt SQL (`postgres=#`):
```sql
CREATE USER minipos_user WITH PASSWORD 'rahasia_super_kuat';
CREATE DATABASE minipos_db OWNER minipos_user;
GRANT ALL PRIVILEGES ON DATABASE minipos_db TO minipos_user;
\q
```

### 4. Clone Repository & Build Aplikasi Next.js
1. Clone repositori ke dalam folder `/var/www` atau home direktori Anda:
   ```bash
   mkdir -p ~/apps && cd ~/apps
   git clone https://github.com/username/mini-pos.git
   cd mini-pos
   ```
2. Buat file `.env.production`:
   ```bash
   nano .env.production
   ```
   Isi dengan:
   ```env
   DATABASE_URL="postgresql://minipos_user:rahasia_super_kuat@localhost:5432/minipos_db"
   NEXTAUTH_SECRET="kunci_rahasia_jwt_anda_yang_panjang"
   NEXTAUTH_URL="https://minipos.domainanda.com"
   NODE_ENV="production"
   PORT=3000
   ```
3. Install dependensi, jalankan migrasi database, dan build aplikasi:
   ```bash
   npm ci
   npx drizzle-kit migrate
   npx tsx src/db/seed.ts
   npm run build
   ```

### 5. PM2 Process Manager
PM2 menjaga server Next.js Anda tetap hidup 24/7 dan otomatis restart jika terjadi error atau server reboot:
```bash
# Instalasi PM2 secara global
npm install -g pm2

# Mulai aplikasi Next.js menggunakan PM2
pm2 start npm --name "mini-pos" -- start

# Periksa status dan log aplikasi
pm2 status
pm2 logs mini-pos

# Konfigurasi agar PM2 otomatis start saat VPS reboot
pm2 startup
# (Jalankan perintah sudo yang muncul di layar terminal Anda)
pm2 save
```

### 6. Setup Nginx sebagai Reverse Proxy
Nginx berfungsi menerima lalu lintas HTTP/HTTPS dari internet dan meneruskannya (*reverse proxy*) ke port `3000` milik Next.js:
1. Instal Nginx:
   ```bash
   sudo apt install nginx -y
   ```
2. Buat konfigurasi virtual host baru:
   ```bash
   sudo nano /etc/nginx/sites-available/mini-pos
   ```
3. Masukkan konfigurasi berikut (ganti `minipos.domainanda.com` dengan domain atau IP VPS Anda):
   ```nginx
   server {
       listen 80;
       server_name minipos.domainanda.com;

       location / {
           proxy_pass http://127.0.0.1:3000;
           proxy_http_version 1.1;
           proxy_set_header Upgrade $http_upgrade;
           proxy_set_header Connection 'upgrade';
           proxy_set_header Host $host;
           proxy_cache_bypass $http_upgrade;
           proxy_set_header X-Real-IP $remote_addr;
           proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
           proxy_set_header X-Forwarded-Proto $scheme;
       }
   }
   ```
4. Aktifkan konfigurasi dan restart Nginx:
   ```bash
   sudo ln -s /etc/nginx/sites-available/mini-pos /etc/nginx/sites-enabled/
   # Hapus default site jika tidak diperlukan
   sudo rm /etc/nginx/sites-enabled/default
   
   # Uji sintaks konfigurasi Nginx
   sudo nginx -t
   
   # Reload Nginx
   sudo systemctl reload nginx
   ```

### 7. SSL Gratis dengan Let's Encrypt (Certbot)
Agar aplikasi aman (HTTPS) dan kredensial login terenkripsi:
```bash
sudo apt install certbot python3-certbot-nginx -y
sudo certbot --nginx -d minipos.domainanda.com
```
Ikuti instruksi di layar (pilih opsi redirect HTTP ke HTTPS). Sertifikat akan diperbarui secara otomatis setiap 90 hari via *cron job* bawaan Certbot!

---

## 🏁 Hasil Akhir
Aplikasi Mini POS kini berjalan dengan performa maksimal di VPS Anda, dilindungi HTTPS, dikelola oleh PM2, dan menggunakan reverse proxy Nginx yang profesional!

---

[← Kembali ke Langkah 1: Vercel](./deploy-step-1-vercel.md) | [📑 Daftar Silabus](../../README.md) | [Lanjut ke Langkah 3: Deploy Docker VPS →](./deploy-step-3-docker-vps.md)
