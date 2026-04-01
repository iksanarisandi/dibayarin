# dibayar.in - Jasa Pembayaran Internasional

## Project Overview

dibayar.in adalah landing page untuk jasa pembayaran layanan internasional (ChatGPT, Claude, AI tools, dll) tanpa kartu kredit di Indonesia. Website ini memungkinkan pengguna Indonesia membayar subscription AI dan layanan internasional menggunakan QRIS, transfer bank, atau e-wallet lokal.

## Tech Stack

- **Frontend**: Static HTML + Vanilla JavaScript + Inline CSS
- **No Build Tools**: Pure static files, no bundler required
- **API**: Exchange rate dari `open.er-api.com/v6/latest/USD`
- **Payment Integration**: WhatsApp untuk konfirmasi pesanan

## File Structure

```
dibayarin/
├── index.html              # Landing page utama dengan form pemesanan
├── config.js               # Konfigurasi (markup, fee, nomor WA)
├── sitemap.xml             # Sitemap untuk SEO
├── robots.txt              # Robots configuration
├── qris.jpg                # QR code untuk pembayaran
├── ogimage.jpg             # Open Graph image
├── icon.svg                # Favicon
├── *.html                  # SEO articles (100+ halaman)
├── CLAUDE.md               # File ini
├── AGENT.md                # Panduan untuk AI agents
└── SEO Strategy/           # Dokumentasi strategi SEO
```

## Konfigurasi (config.js)

```javascript
const CONFIG = {
    MARKUP: 1100,      // Markup kurs per USD (dalam IDR)
    FEE: 50000,        // Fee tetap per transaksi (dalam IDR)
    WA_NUMBER: '6282347303153'  // Nomor WhatsApp admin
};
```

## Fitur Utama

### 1. Kalkulator Kurs (Hero Section)
- Fetch kurs USD/IDR real-time dari API
- Menampilkan kurs dasar + kurs dengan markup
- Kalkulasi total bayar: `(USD × kursMarkup) + FEE`

### 2. Form Pemesanan
- Input: Nama, Platform, Nominal USD
- Platform dengan auto-fill nominal:
  - **Claude Pro** → $20
  - **ChatGPT Go** → $5.5
- Platform "Lainnya" menampilkan input tambahan
- Tombol WhatsApp untuk konfirmasi pesanan

### 3. SEO Articles
- 100+ halaman artikel SEO untuk berbagai keyword
- Target keyword: jasa bayar AI, payment gateway, dll
- Semua artikel dalam Bahasa Indonesia

## Platform yang Didukung

- Claude Pro, Claude
- ChatGPT Go, ChatGPT
- Gemini
- Github Copilot
- Cursor
- Zai, Coder, Trae, Minimax
- Notion, Kie Ai, OpenAI Api
- Zoom
- Topup Paypal
- Lainnya (custom input)

## Style Guidelines

- Warna utama: `#0070ba` (PayPal blue)
- Font: System fonts (-apple-system, BlinkMacSystemFont, Segoe UI, Roboto)
- Border radius: 8px untuk cards, 4px untuk inputs
- Responsive: Mobile-first design

## Cara Kerja Form

1. User mengisi nama dan memilih platform
2. Jika platform Claude Pro/ChatGPT Go, nominal terisi otomatis
3. User memasukkan nominal USD (atau menggunakan auto-fill)
4. Sistem menghitung total: `(USD × (kurs + markup)) + fee`
5. User klik "Konfirmasi Via WhatsApp"
6. Tab baru terbuka dengan pesan WhatsApp yang terisi otomatis

## Pengembangan

### Menambah Platform Baru dengan Auto-fill
Edit `index.html`:
1. Tambah `<option>` di dalam `<select id="platform">`
2. Tambah kondisi di event listener `platform.change`

### Mengubah Kurs/Markup
Edit `config.js`:
- `MARKUP`: nilai markup per USD
- `FEE`: biaya tetap per transaksi

### Mengubah Nomor WhatsApp
Edit `config.js`:
- `WA_NUMBER`: nomor tanpa + atau 0 di depan

## SEO Strategy

- Target: Keyword "jasa bayar AI", "jasa pembayaran internasional", dll
- Articles: Long-form SEO articles di setiap halaman
- Schema: JSON-LD untuk Service dan FAQPage
- Meta: Open Graph dan Twitter Cards

## Deployment

Website ini adalah static site yang bisa di-deploy ke:
- GitHub Pages
- Netlify
- Vercel
- Cloudflare Pages
- Hosting tradisional (shared hosting)

Tidak memerlukan build process atau server-side rendering.
