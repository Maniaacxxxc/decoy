# ME-CLI - XL Axiata Package Management System

<p align="center">
  <img src="CLI-VERSION/bnr.png" alt="ME-CLI Banner" width="400">
</p>

<p align="center">
  <b>CLI & Telegram Bot untuk Manajemen Paket XL Axiata</b>
</p>

<p align="center">
  <a href="#fitur-utama">Fitur</a> •
  <a href="#instalasi">Instalasi</a> •
  <a href="#cara-penggunaan">Penggunaan</a> •
  <a href="#arsitektur-sistem">Arsitektur</a> •
  <a href="#dokumentasi-api">API</a>
</p>

---

## 📋 Daftar Isi

- [Gambaran Umum](#gambaran-umum)
- [Fitur Utama](#fitur-utama)
- [Struktur Project](#struktur-project)
- [Instalasi](#instalasi)
  - [CLI Version](#cli-version)
  - [Telegram Bot Version](#telegram-bot-version)
- [Konfigurasi](#konfigurasi)
- [Cara Penggunaan](#cara-penggunaan)
- [Arsitektur Sistem](#arsitektur-sistem)
- [Sistem Autentikasi](#sistem-autentikasi)
- [Penyimpanan Token](#penyimpanan-token)
- [Metode Pembayaran](#metode-pembayaran)
- [Dokumentasi API](#dokumentasi-api)
- [Kontribusi](#kontribusi)
- [Disclaimer](#disclaimer)

---

## 📖 Gambaran Umum

**ME-CLI** adalah sistem manajemen paket XL Axiata yang komprehensif dengan dua versi:

| Versi | Deskripsi | Platform |
|-------|-----------|----------|
| **CLI-VERSION** | Command Line Interface untuk terminal/Termux | Linux, Termux, macOS |
| **xl_mecli_bot** | Telegram Bot dengan fitur multi-user | Cross-platform via Telegram |

### Apa yang bisa dilakukan?

- 🔐 Login ke akun XL menggunakan OTP
- 💰 Melihat saldo/pulsa dan kuota
- 📦 Membeli paket internet dengan berbagai metode pembayaran
- 🔖 Menyimpan paket favorit (bookmark)
- 🔄 Melakukan pembelian massal (loop purchase)
- 👨‍👩‍👧‍👦 Mengelola Family Plan / Akrab
- ⭕ Melihat informasi Circle
- 📜 Riwayat transaksi
- 🔥 Akses paket HOT/promo

---

## ✨ Fitur Utama

### CLI Version
```
┌─────────────────────────────────────────────────────────────┐
│  MENU UTAMA CLI                                             │
├─────────────────────────────────────────────────────────────┤
│  1. 👤 Login / Ganti Akun                                   │
│  2. 📦 Lihat Paket Saya                                     │
│  0. 🔖 Bookmark Paket                                       │
│  3. 🔥 Beli Paket HOT                                       │
│  4. 🔥 Beli Paket HOT-2                                     │
│  5. 🎯 Beli via Option Code                                 │
│  6. 📑 Beli via Family Code                                 │
│  7. 🔄 Beli Semua di Family (Loop)                          │
│  8. 🧾 Riwayat Transaksi                                    │
│  9. 👨‍👩‍👧‍👦 Family Plan / Akrab                                  │
│ 10. ⭕ Circle                                                │
│ 11. 🏪 Store Segments                                       │
│ 12. 📋 Store Family List                                    │
│ 13. 📦 Store Packages                                       │
│ 14. 🎁 Redeemables                                          │
│  R. 📝 Register NIK/KK                                      │
│  V. ✓ Validate MSISDN                                       │
│  N. 🔔 Notifikasi                                           │
│ 99. 🚪 Tutup Aplikasi                                       │
└─────────────────────────────────────────────────────────────┘
```

### Telegram Bot Version
```
┌─────────────────────────────────────────────────────────────┐
│  INLINE KEYBOARD TELEGRAM BOT                               │
├─────────────────────────────────────────────────────────────┤
│  📦 Paket Saya    │    💰 Saldo                             │
│  🔥 Paket HOT     │    🔖 Bookmark                          │
│  🛒 Beli Paket    │    🗑️ Hapus Paket                       │
│  👨‍👩‍👧‍👦 Akrab         │    📜 Riwayat                           │
│  📖 Panduan       │    👤 Akun                              │
│  ⚙️ Pengaturan    │    🔄 Refresh                           │
└─────────────────────────────────────────────────────────────┘
```

---

## 📁 Struktur Project

```
ME-CLI-NEXT-11-FEB/
│
├── 📄 cara-kerja.txt              # Dokumentasi teknis lengkap
├── 📄 install.sh                  # Script instalasi
│
├── 📁 CLI-VERSION/                # Versi Command Line
│   ├── 📄 main.py                 # Entry point CLI
│   ├── 📄 refresh-tokens.json     # Penyimpanan token akun
│   ├── 📄 bookmark.json           # Penyimpanan bookmark
│   ├── 📄 active.number           # Nomor aktif saat ini
│   ├── 📄 ax.fp                   # Fingerprint device
│   ├── 📄 .env                    # Environment variables
│   ├── 📄 requirements.txt        # Python dependencies
│   ├── 📄 setup.sh                # Setup script
│   ├── 📄 run.sh                  # Run script
│   │
│   └── 📁 app/
│       ├── 📄 colors.py           # Color/styling utilities
│       ├── 📄 type_dict.py        # Type definitions
│       ├── 📄 ui_helper.py        # UI helper functions
│       ├── 📄 ui_rich.py          # Rich text formatting
│       ├── 📄 util.py             # Utility functions
│       │
│       ├── 📁 client/             # API Clients
│       │   ├── 📄 ciam.py         # Auth API (OTP, Login, Token)
│       │   ├── 📄 engsel.py       # Main API (Profile, Balance, Packages)
│       │   ├── 📄 encrypt.py      # Enkripsi/Dekripsi payload
│       │   ├── 📄 circle.py       # Circle API
│       │   ├── 📄 famplan.py      # Family Plan API
│       │   ├── 📄 registration.py # Registration API
│       │   │
│       │   ├── 📁 purchase/       # Metode Pembayaran
│       │   │   ├── 📄 balance.py  # Bayar dengan pulsa
│       │   │   ├── 📄 qris.py     # Bayar dengan QRIS
│       │   │   └── 📄 ewallet.py  # Bayar dengan E-Wallet
│       │   │
│       │   └── 📁 store/          # Store API
│       │
│       ├── 📁 menus/              # UI Menu CLI
│       │   ├── 📄 account.py      # Menu manajemen akun
│       │   ├── 📄 bookmark.py     # Menu bookmark
│       │   ├── 📄 circle.py       # Menu circle
│       │   ├── 📄 family.py       # Menu family
│       │   ├── 📄 famplan.py      # Menu family plan
│       │   ├── 📄 hot.py          # Menu paket HOT
│       │   ├── 📄 notification.py # Menu notifikasi
│       │   ├── 📄 package.py      # Menu paket
│       │   ├── 📄 payment.py      # Menu pembayaran
│       │   ├── 📄 purchase.py     # Menu pembelian
│       │   └── 📄 util.py         # Menu utilities
│       │
│       └── 📁 service/            # Service Layer
│           ├── 📄 auth.py         # Manajemen autentikasi
│           ├── 📄 bookmark.py     # Manajemen bookmark
│           ├── 📄 crypto_helper.py# Crypto utilities
│           ├── 📄 decoy.py        # Sistem decoy package
│           ├── 📄 git.py          # Git update checker
│           ├── 📄 sentry.py       # Sentry mode
│           └── 📄 telegram.py     # Notifikasi Telegram
│
└── 📁 xl_mecli_bot/               # Versi Telegram Bot
    ├── 📄 simple_bot.py           # Simple bot entry
    ├── 📄 check_tokens.py         # Token checker
    ├── 📄 refresh-tokens.json     # Shared tokens
    ├── 📄 requirements.txt        # Bot dependencies
    │
    ├── 📁 app/                    # Shared app modules (sama dgn CLI)
    │
    └── 📁 telegram_bot/           # Telegram Bot Core
        ├── 📄 bot.py              # Bot entry point
        ├── 📄 main.py             # Alternative entry
        ├── 📄 config.py           # Konfigurasi bot
        ├── 📄 models.py           # Data models
        ├── 📄 utils.py            # Utilities
        ├── 📄 api.py              # API wrapper
        ├── 📄 hot.py              # Hot packages logic
        ├── 📄 decorators.py       # Function decorators
        ├── 📄 decoy_config.json   # Decoy configuration
        ├── 📄 Dockerfile          # Docker build
        ├── 📄 docker-compose.yml  # Docker compose
        │
        ├── 📁 core/               # Core API wrapper
        │   └── 📄 api.py          # Bridge ke app modules
        │
        ├── 📁 database/           # Database layer
        │   ├── 📄 models.py       # SQLAlchemy models
        │   └── 📄 crud.py         # CRUD operations
        │
        ├── 📁 handlers/           # Telegram handlers
        │   ├── 📄 admin.py        # Admin panel
        │   ├── 📄 auth.py         # Login/OTP handler
        │   ├── 📄 balance.py      # Balance handler
        │   ├── 📄 bookmark.py     # Bookmark handler
        │   ├── 📄 famplan.py      # Family plan handler
        │   ├── 📄 history.py      # History handler
        │   ├── 📄 hot.py          # Paket HOT handler
        │   ├── 📄 menu.py         # Main menu handler
        │   ├── 📄 packages.py     # Packages handler
        │   ├── 📄 purchase.py     # Purchase handler
        │   ├── 📄 start.py        # Start command handler
        │   ├── 📄 token.py        # Token handler
        │   ├── 📄 token_admin.py  # Token admin handler
        │   └── 📄 unsubscribe.py  # Unsubscribe handler
        │
        ├── 📁 keyboards/          # Inline keyboards
        │   ├── 📄 main.py         # Main menu keyboard
        │   ├── 📄 account.py      # Account keyboard
        │   ├── 📄 packages.py     # Packages keyboard
        │   └── 📄 purchase.py     # Purchase keyboard
        │
        ├── 📁 middlewares/        # Middleware
        │   └── 📄 auth.py         # Authorization middleware
        │
        ├── 📁 states/             # FSM States
        │   └── 📄 __init__.py     # State definitions
        │
        └── 📁 utils/              # Utilities
            └── 📄 messages.py     # Message templates
```

---

## 🚀 Instalasi

### CLI Version

#### Menggunakan Termux (Android)

```bash
# 1. Update & Upgrade Termux
pkg update && pkg upgrade -y

# 2. Install Git dan Python
pkg install git python -y

# 3. Clone repository
git clone https://github.com/purplemashu/me-cli

# 4. Masuk ke folder
cd me-cli/CLI-VERSION

# 5. Jalankan setup
bash setup.sh

# 6. Buat file .env (lihat bagian Konfigurasi)
nano .env

# 7. Jalankan aplikasi
python main.py
```

#### Menggunakan Linux/macOS

```bash
# 1. Clone repository
git clone https://github.com/purplemashu/me-cli
cd me-cli/CLI-VERSION

# 2. Buat virtual environment (opsional)
python3 -m venv venv
source venv/bin/activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Buat file .env
cp .env.example .env
nano .env

# 5. Jalankan
python main.py
```

### Telegram Bot Version

#### Menggunakan Python langsung

```bash
# 1. Masuk ke folder bot
cd xl_mecli_bot/telegram_bot

# 2. Install dependencies
pip install -r requirements.txt

# 3. Buat file .env
nano .env

# 4. Jalankan bot
python -m telegram_bot.bot
```

#### Menggunakan Docker

```bash
# 1. Masuk ke folder bot
cd xl_mecli_bot/telegram_bot

# 2. Build dan jalankan dengan docker-compose
docker-compose up -d

# Lihat logs
docker-compose logs -f
```

---

## ⚙️ Konfigurasi

### Environment Variables (.env)

```env
# ============================================
# API Configuration (Wajib)
# ============================================
BASE_CIAM_URL=https://xxx.xl.co.id       # Auth server URL
BASE_API_URL=https://xxx.xl.co.id        # Main API URL
BASIC_AUTH=xxxx                           # Basic auth untuk CIAM
UA=Mozilla/5.0 xxx                        # User Agent
API_KEY=xxxx                              # API Key

# ============================================
# Telegram Bot (Untuk Bot Version)
# ============================================
TG_BOT_TOKEN=123456:ABC-xxx               # Bot token dari BotFather
ADMIN_IDS=123456789                       # Telegram ID admin (comma separated)
REQUIRE_TOKEN_ACCESS=true                 # Wajib token untuk akses bot

# ============================================
# Database (Untuk Bot Version)
# ============================================
DATABASE_URL=sqlite:///data/bot.db        # Database path

# ============================================
# Redis (Opsional, untuk FSM storage)
# ============================================
REDIS_URL=redis://localhost:6379          # Redis URL

# ============================================
# Notifikasi (Opsional, untuk CLI)
# ============================================
TELEGRAM_BOT_TOKEN=xxx                    # Bot token untuk notifikasi
TELEGRAM_CHAT_ID=xxx                      # Chat ID untuk notifikasi
```

> 💡 **Tip**: Dapatkan environment variables dari [Telegram Channel](https://t.me/alyxcli)

---

## 📱 Cara Penggunaan

### CLI Version

#### 1. Login Pertama Kali

```
1. Jalankan: python main.py
2. Pilih menu 1 (Login / Ganti Akun)
3. Masukkan nomor XL (format: 628xxxxxxxxx)
4. Masukkan OTP yang diterima via SMS
5. Login berhasil! Token tersimpan otomatis
```

#### 2. Membeli Paket

**Via Paket HOT:**
```
1. Pilih menu 3 (Beli Paket HOT)
2. Pilih paket dari daftar
3. Pilih metode pembayaran
4. Konfirmasi pembelian
```

**Via Family Code:**
```
1. Pilih menu 6 (Beli via Family Code)
2. Masukkan family code paket
3. Pilih variant dan option
4. Pilih metode pembayaran
```

**Via Option Code:**
```
1. Pilih menu 5 (Beli via Option Code)
2. Masukkan option code langsung
3. Pilih metode pembayaran
```

#### 3. Loop Purchase (Beli Semua dalam Family)

```
1. Pilih menu 7 (Beli Semua di Family)
2. Masukkan family code
3. Set opsi:
   - Start from option number: 1
   - Use decoy package: y/n
   - Pause on success: y/n
   - Delay between purchases: 0-n seconds
4. Sistem akan membeli semua paket dalam family secara otomatis
```

### Telegram Bot Version

#### Commands yang Tersedia

| Command | Deskripsi |
|---------|-----------|
| `/start` | Memulai bot, menampilkan menu utama |
| `/login` | Login ke akun XL |
| `/hot` | Lihat paket HOT |
| `/saldo` | Cek saldo dan kuota |
| `/paket` | Lihat paket aktif |
| `/admin` | Admin panel (khusus admin) |

#### Alur Login Telegram Bot

```
1. Ketik /login
2. Masukkan nomor XL
3. Bot mengirim request OTP
4. Masukkan OTP 6 digit
5. Login berhasil, akun tersimpan di database
```

---

## 🏗️ Arsitektur Sistem

### Alur Data Keseluruhan

```
                              USER REQUEST
                                   │
                   ┌───────────────┴───────────────┐
                   │                               │
              CLI VERSION                   TELEGRAM BOT
                   │                               │
           ┌───────┴───────┐               ┌──────┴──────┐
           │   main.py     │               │   bot.py    │
           │   (loop)      │               │  (polling)  │
           └───────┬───────┘               └──────┬──────┘
                   │                               │
           ┌───────┴───────┐               ┌──────┴──────┐
           │ AuthInstance  │               │  Database   │
           │ (JSON-based)  │               │  (SQLite)   │
           └───────┬───────┘               └──────┬──────┘
                   │                               │
                   └───────────────┬───────────────┘
                                   │
                           ┌───────┴───────┐
                           │    SHARED     │
                           │  app/client/  │
                           │   modules     │
                           └───────┬───────┘
                                   │
                    ┌──────────────┼──────────────┐
                    │              │              │
               ciam.py        engsel.py     purchase/
             (Auth API)     (Main API)    (Payment API)
                    │              │              │
                    └──────────────┴──────────────┘
                                   │
                              ENCRYPTED
                                   │
                                   ▼
                          XL AXIATA SERVERS
```

### Komponen Utama

#### 1. Client Layer (`app/client/`)

| File | Fungsi |
|------|--------|
| `ciam.py` | Autentikasi (OTP, Login, Refresh Token) |
| `engsel.py` | API Utama (Profile, Balance, Packages) |
| `encrypt.py` | Enkripsi/Dekripsi payload |
| `purchase/*.py` | Metode pembayaran |

#### 2. Service Layer (`app/service/`)

| File | Fungsi |
|------|--------|
| `auth.py` | Singleton untuk manajemen autentikasi |
| `decoy.py` | Sistem decoy package |
| `bookmark.py` | Manajemen bookmark |
| `telegram.py` | Notifikasi via Telegram |

#### 3. Menu Layer (`app/menus/`)

| File | Fungsi |
|------|--------|
| `account.py` | UI manajemen akun |
| `hot.py` | UI paket HOT |
| `purchase.py` | UI pembelian |
| `bookmark.py` | UI bookmark |

---

## 🔐 Sistem Autentikasi

### Alur Autentikasi XL

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                           ALUR AUTENTIKASI                                  │
└─────────────────────────────────────────────────────────────────────────────┘

1. REQUEST OTP
   ┌────────────────────────────────────────────────────────────────────────┐
   │  GET /realms/xl-ciam/auth/otp?contact=628xxx&contactType=SMS          │
   │                                                                        │
   │  Headers:                                                              │
   │  - Authorization: Basic {BASIC_AUTH}                                   │
   │  - Ax-Device-Id: {generated device id}                                 │
   │  - Ax-Fingerprint: {fingerprint dari ax.fp}                            │
   │  - Ax-Request-At: {timestamp ISO format}                               │
   │  - Ax-Request-Id: {UUID}                                               │
   │                                                                        │
   │  Response: { "subscriber_id": "xxx-xxx-xxx" }                          │
   └────────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
2. VERIFY OTP & GET TOKENS
   ┌────────────────────────────────────────────────────────────────────────┐
   │  POST /realms/xl-ciam/protocol/openid-connect/token                    │
   │                                                                        │
   │  Body (x-www-form-urlencoded):                                         │
   │  - grant_type: password                                                │
   │  - contact: {nomor HP}                                                 │
   │  - contactType: SMS                                                    │
   │  - code: {OTP 6 digit}                                                 │
   │                                                                        │
   │  Response:                                                             │
   │  - access_token                                                        │
   │  - refresh_token                                                       │
   │  - id_token                                                            │
   │  - expires_in                                                          │
   └────────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
3. REFRESH TOKEN (saat expired)
   ┌────────────────────────────────────────────────────────────────────────┐
   │  POST /realms/xl-ciam/protocol/openid-connect/token                    │
   │                                                                        │
   │  Body:                                                                 │
   │  - grant_type: refresh_token                                           │
   │  - refresh_token: {stored refresh token}                               │
   │                                                                        │
   │  Response: New set of tokens                                           │
   └────────────────────────────────────────────────────────────────────────┘
```

### Auto-Refresh Token

- Token di-refresh otomatis setiap **5 menit** saat aktif
- Jika session expired, sistem akan extend session menggunakan `subscriber_id`
- Semua token update disimpan ke storage

---

## 💾 Penyimpanan Token

### CLI Version - JSON Storage

Token disimpan di file `refresh-tokens.json`:

```json
[
  {
    "number": 6281234567890,
    "subscriber_id": "xxx-xxx-xxx",
    "subscription_type": "PREPAID",
    "refresh_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "alias": "Nomor Utama"
  },
  {
    "number": 6289876543210,
    "subscriber_id": "yyy-yyy-yyy",
    "subscription_type": "POSTPAID",
    "refresh_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "alias": "Nomor Kedua"
  }
]
```

**Active User** disimpan di `active.number`:
```
6281234567890
```

### Telegram Bot - SQLite Database

```sql
-- Table: tg_users
CREATE TABLE tg_users (
    id INTEGER PRIMARY KEY,
    tg_id INTEGER UNIQUE NOT NULL,
    username VARCHAR(100),
    first_name VARCHAR(100),
    tier VARCHAR(20) DEFAULT 'none',        -- none, reguler, premium
    is_admin BOOLEAN DEFAULT FALSE,
    is_authorized BOOLEAN DEFAULT FALSE,
    authorized_until DATETIME,
    created_at DATETIME,
    last_active DATETIME
);

-- Table: xl_accounts
CREATE TABLE xl_accounts (
    id INTEGER PRIMARY KEY,
    tg_id INTEGER REFERENCES tg_users(tg_id),
    xl_number VARCHAR(20) NOT NULL,
    subscriber_id VARCHAR(100),
    subscription_type VARCHAR(20),           -- PREPAID, POSTPAID
    refresh_token TEXT,
    access_token TEXT,
    id_token TEXT,
    alias VARCHAR(50),
    is_active BOOLEAN DEFAULT TRUE,          -- Currently selected
    token_updated_at DATETIME,
    created_at DATETIME
);

-- Table: transactions
CREATE TABLE transactions (
    id INTEGER PRIMARY KEY,
    tg_id INTEGER REFERENCES tg_users(tg_id),
    xl_number VARCHAR(20),
    package_code VARCHAR(100),
    package_name VARCHAR(200),
    price INTEGER DEFAULT 0,
    payment_method VARCHAR(50),              -- BALANCE, QRIS, EWALLET
    status VARCHAR(20),                      -- SUCCESS, FAILED, PENDING
    error_message TEXT,
    created_at DATETIME
);

-- Table: hot_packages (Admin managed)
CREATE TABLE hot_packages (
    id INTEGER PRIMARY KEY,
    name VARCHAR(200),
    family_code VARCHAR(100),
    variant_name VARCHAR(100),
    option_code VARCHAR(100),
    option_order INTEGER,
    price INTEGER,
    is_enterprise BOOLEAN,
    is_active BOOLEAN,
    tier VARCHAR(20) DEFAULT 'reguler',      -- reguler, premium
    display_order INTEGER,
    created_at DATETIME
);

-- Table: bookmarks
CREATE TABLE bookmarks (
    id INTEGER PRIMARY KEY,
    tg_id INTEGER REFERENCES tg_users(tg_id),
    name VARCHAR(200),
    family_code VARCHAR(100),
    variant_code VARCHAR(100),
    option_code VARCHAR(100),
    option_order INTEGER,
    price INTEGER,
    created_at DATETIME
);
```

---

## 💳 Metode Pembayaran

### Daftar Metode Pembayaran

| Metode | Deskripsi | API Endpoint |
|--------|-----------|--------------|
| **BALANCE** | Bayar dengan pulsa | `/payments/api/v8/settlement-multipayment` |
| **QRIS** | Generate QR untuk scan | `/payments/api/v8/settlement-multipayment/qris` |
| **E-WALLET** | OVO, GoPay, Dana, dll | `/payments/api/v8/settlement-multipayment/ewallet` |
| **BOUNTY** | Redeem voucher | `/payments/api/v8/settlement-voucher` |
| **LOYALTY** | Tukar poin reward | `/payments/api/v8/settlement-loyalty` |
| **DECOY** | Teknik khusus (lihat bawah) | Combined settlement |

### Sistem Decoy Package

Decoy adalah teknik untuk pembelian paket dengan manipulasi harga:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  CARA KERJA DECOY:                                                          │
│                                                                             │
│  1. Ambil paket target (misal: paket 50GB Rp50.000)                         │
│  2. Ambil paket decoy (paket murah/gratis dari server remote)               │
│  3. Kirim keduanya dalam satu request "multi-payment"                       │
│  4. Set total amount = harga decoy saja                                     │
│  5. Server memproses keduanya dengan harga decoy                            │
│                                                                             │
│  Source Decoy:                                                              │
│  https://raw.githubusercontent.com/Maniaacxxxc/decoy/.../default-*.json     │
└─────────────────────────────────────────────────────────────────────────────┘
```

**Jenis Decoy:**

| Nama | Keterangan |
|------|------------|
| `default-balance` | Untuk PREPAID dengan pulsa |
| `default-qris` | Untuk PREPAID dengan QRIS |
| `prio-balance` | Untuk PRIORITAS/PRIOHYBRID dengan pulsa |
| `prio-qris` | Untuk PRIORITAS/PRIOHYBRID dengan QRIS |

### Alur Pembayaran dengan Pulsa

```python
# 1. Get payment methods
payment_path = "payments/api/v8/payment-methods-option"
# Response: token_payment, timestamp

# 2. Build settlement payload
settlement_payload = {
    "payment_method": "BALANCE",
    "total_amount": amount,
    "items": [package_item],
    "token_payment": token_payment,
    # ... other fields
}

# 3. Encrypt & Sign
encrypted_payload = encryptsign_xdata(api_key, "POST", path, id_token, payload)
x_signature = get_x_signature_payment(...)

# 4. Send settlement request
response = POST /payments/api/v8/settlement-multipayment
```

---

## 🔒 Sistem Enkripsi API

Semua request ke API XL menggunakan enkripsi:

```
┌────────────────────────────────────────────────────────────────────────────┐
│  REQUEST STRUCTURE:                                                        │
│                                                                            │
│  Headers:                                                                  │
│  - x-api-key: {API_KEY}                                                    │
│  - x-hv: v3                                                                │
│  - x-signature: {calculated signature}                                     │
│  - x-signature-time: {timestamp in seconds}                                │
│  - x-request-id: {UUID}                                                    │
│  - Authorization: Bearer {id_token}                                        │
│                                                                            │
│  Body: {encrypted payload with xtime}                                      │
└────────────────────────────────────────────────────────────────────────────┘
```

### Signature Calculation

```python
def ax_api_signature(api_key, timestamp, contact, code, contact_type):
    """
    Menggunakan HMAC dengan secret key
    Input: method + path + timestamp + payload
    Output: base64 encoded signature
    """
```

---

## 🔥 Sistem Paket HOT

### CLI Version
- Diambil dari: `https://me.mashu.lol/pg-hot.json`
- Alternatif: `https://prem.jajanvpn.top/ACC/xl/hot.json`

### Telegram Bot Version
- Disimpan di database (`hot_packages` table)
- Admin bisa manage via Admin Panel
- Support tier: reguler & premium
- Fallback ke JSON remote jika database kosong

**Format JSON HOT:**
```json
[
  {
    "name": "Internet 50GB",
    "family_code": "FAM_CODE",
    "family_name": "Paket Internet",
    "variant_name": "50GB",
    "option_name": "30 Hari",
    "order": 1,
    "price": 50000,
    "is_enterprise": false
  }
]
```

---

## 📊 Perbedaan CLI vs Telegram Bot

| Aspek | CLI Version | Telegram Bot |
|-------|-------------|--------------|
| **Interface** | Terminal/Console | Telegram Chat |
| **Storage** | JSON files | SQLite Database |
| **Multi-user** | Single user per device | Multi-user support |
| **Auth** | JSON token storage | Database + FSM states |
| **Access Control** | Siapa saja | Token-based authorization |
| **Admin Panel** | Tidak ada | Ada (kelola user, broadcast) |
| **Hot Packages** | Remote JSON only | Database + fallback JSON |
| **Async** | Synchronous | Asynchronous (aiogram) |
| **Platform** | Linux/Termux | Cross-platform via Telegram |
| **Deployment** | Local execution | Docker support |

---

## 🛡️ Admin Panel (Telegram Bot)

### Akses Admin
```
/admin - Membuka admin panel
```

### Fitur Admin

1. **👥 Users Management**
   - Lihat daftar user
   - Hapus user
   - Cari user by ID/username
   - Set tier user (reguler/premium)

2. **📢 Broadcast**
   - Kirim pesan ke semua user
   - Kirim ke tier tertentu

3. **🔥 HOT Management**
   - Tambah paket HOT
   - Edit paket HOT
   - Hapus paket HOT
   - Set tier paket (reguler/premium)

4. **🔑 Token Management**
   - Generate access token
   - Set expiry date
   - Revoke token

5. **📊 Statistics**
   - Total users
   - Total transactions
   - Success rate

---

## ⚠️ Troubleshooting

### Token Expired

```
Error: Invalid refresh token / Session not active
```

**Solusi:**
1. Hapus akun dari daftar
2. Login ulang dengan OTP

### Failed to Decrypt

```
Error: [decrypt err] ...
```

**Solusi:**
- Pastikan API_KEY valid
- Cek koneksi internet

### OTP Not Received

**Solusi:**
1. Pastikan nomor aktif
2. Tunggu 1-2 menit
3. Coba request OTP ulang

### Rate Limited

**Solusi:**
- Tunggu beberapa menit
- Jangan spam request

---

## 📝 Changelog

### v2.0.0 (Latest)
- ✨ Telegram Bot version
- ✨ Multi-user support
- ✨ Database storage
- ✨ Admin panel
- ✨ Docker support

### v1.0.0
- 🎉 Initial CLI release
- ✨ OTP Login
- ✨ Purchase packages
- ✨ Bookmark feature
- ✨ Loop purchase

---

## ⚖️ Disclaimer

```
By using this tool, the user agrees to:

1. Comply with all applicable laws and regulations
2. Release the developer from any and all claims arising from its use
3. Use responsibly and not for any illegal activities

This tool is provided "AS IS" without warranty of any kind.
The developer is not responsible for any misuse or damage caused by this tool.
```

---

## 📞 Contact

- 📧 Email: contact@mashu.lol
- 📱 Telegram: [@alyxcli](https://t.me/alyxcli)

---

<p align="center">
  Made with ❤️ for XL Axiata users
</p>
