# AI Agent Guide - dibayar.in

## Quick Reference

| Item | Value |
|------|-------|
| Project Type | Static HTML Landing Page |
| Primary Language | Indonesian (Bahasa Indonesia) |
| Main File | `index.html` |
| Config File | `config.js` |
| Exchange API | `https://open.er-api.com/v6/latest/USD` |

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────┐
│                      index.html                              │
│  ┌─────────────────────────────────────────────────────┐    │
│  │  Inline CSS Styles (lines ~100-700)                 │    │
│  └─────────────────────────────────────────────────────┘    │
│  ┌─────────────────────────────────────────────────────┐    │
│  │  HTML Content                                       │    │
│  │  - Hero Section (calculator)                        │    │
│  │  - Order Form                                       │    │
│  │  - QRIS Section                                     │    │
│  │  - Testimonials                                     │    │
│  └─────────────────────────────────────────────────────┘    │
│  ┌─────────────────────────────────────────────────────┐    │
│  │  Inline JavaScript (lines ~1710-1841)               │    │
│  │  - fetchKurs()                                      │    │
│  │  - calculateTotal()                                 │    │
│  │  - handleWhatsAppClick()                            │    │
│  └─────────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────────┘
         │
         ▼
┌─────────────────┐
│    config.js    │
│  - MARKUP       │
│  - FEE          │
│  - WA_NUMBER    │
└─────────────────┘
```

## Core Functions

### fetchKurs()
```javascript
// Fetches USD/IDR rate from API
// Calculates: kursMarkup = kursDasar + CONFIG.MARKUP
// Fallback: kursDasar = 16000 if API fails
```

### calculateTotal(usd)
```javascript
// Formula: (usd * kursMarkup) + CONFIG.FEE
// Returns: number (IDR)
```

### handleWhatsAppClick()
```javascript
// Validates form inputs
// Builds WhatsApp message with order details
// Opens: https://wa.me/{WA_NUMBER}?text={encoded_message}
```

## Form Platform Auto-Fill Logic

Located in platform change event listener:

```javascript
// Auto-fill mapping
'Claude Pro' → 20 USD
'ChatGPT Go' → 5.5 USD
'Lainnya' → Show custom input field
```

## Common Tasks for AI Agents

### Task: Add new platform with fixed price
1. Add `<option value="PlatformName">PlatformName</option>` to select#platform
2. Add auto-fill condition in change event listener:
   ```javascript
   else if (this.value === 'PlatformName') {
       formUsd.value = PRICE;
       updateFormTotal();
   }
   ```

### Task: Modify pricing structure
1. Edit `config.js`:
   - `MARKUP`: Additional IDR per USD
   - `FEE`: Fixed fee per transaction

### Task: Create new SEO article
1. Create new HTML file with proper SEO meta tags
2. Include JSON-LD schema for Service/FAQPage
3. Link to index.html for order form
4. Update sitemap.xml

### Task: Change WhatsApp number
1. Edit `config.js`:
   ```javascript
   WA_NUMBER: '628xxxxxxxxxx'
   ```

## File Locations

| Component | File | Line Range |
|-----------|------|------------|
| CSS Styles | index.html | ~100-700 |
| Hero Calculator | index.html | ~700-750 |
| Order Form | index.html | ~750-760 |
| JavaScript | index.html | ~1710-1841 |
| Config | config.js | All |
| QRIS Image | qris.jpg | - |
| Favicon | icon.svg | - |

## SEO Structure

Each SEO article page should include:
1. Meta tags (description, keywords, og:*, twitter:*)
2. JSON-LD Schema (Service, FAQPage, or Article)
3. Canonical URL
4. Internal links to index.html

## Platform Dropdown Options (Current)

```
Claude Pro (auto-fill: $20)
ChatGPT Go (auto-fill: $5.5)
Zai
Coder
Claude
ChatGPT
Gemini
Minimax
Github Copilot
Trae
Cursor
Topup Paypal
Notion
Kie Ai
OpenAI Api
Zoom
Lainnya (custom input)
```

## Payment Flow

1. User enters name
2. User selects platform (optional auto-fill)
3. User enters USD amount
4. System calculates: `(USD × kursMarkup) + FEE`
5. User clicks "Konfirmasi Via WhatsApp"
6. WhatsApp opens with pre-filled order message
7. Admin processes order manually

## Rate Calculation Example

```
Given:
- USD amount: 20
- Current rate: 16,000 IDR
- MARKUP: 1,100 IDR
- FEE: 50,000 IDR

Calculation:
- kursMarkup = 16,000 + 1,100 = 17,100
- total = (20 × 17,100) + 50,000
- total = 342,000 + 50,000 = 392,000 IDR
```

## Dependencies

- **None** - Pure vanilla HTML/CSS/JS
- No npm packages required
- No build process needed
- External API: open.er-api.com (free, no auth required)
