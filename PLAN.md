# Gas Cafe One Stop — New Website Build Plan

## Context

Gas Cafe One Stop (602 Butte Ave, Crested Butte, CO) wants a new website replacing their current site builder page. The brand is rock & roll — AC/DC-style logo with a lightning bolt, "Grillin' High in the Rockies since 1998." They want a merchandise shop but no online food ordering (yet). Hosting is Bluehost shared, so we're building PHP + Tailwind CSS with a lightweight MySQL-backed CMS for menu and store management, deployed via SFTP. The customer is reviewing **6 design direction mockups** before committing to a full build.

**Palette:** Black, white, red, and blue (rock & roll Americana)
**Primary logo:** `stock images/Logo AC-DC.jpg` — blocky AC/DC-style "GAS⚡CAFE"
**Pages:** Home, Menu, Shop, About, Reviews, Contact
**Mockups live at:** https://philkomarny.github.io/GasCafe/mockups/

---

## Phase 0: Archive & Scaffold ✅ COMPLETE

- Archived existing APP/ (Next.js ordering app) and Website/ folders to `_archive/`
- Scaffolded new project structure
- Web-scraped existing site content + all 44 images to `web-scrape/`
- Stock images and logos in `stock images/`

---

## Phase 1: Design Mockups ✅ COMPLETE — AWAITING CUSTOMER DECISION

Six self-contained HTML mockups, each showing a complete homepage layout: hero, sample menu section, sample merch section, reviews, and footer. Same palette (black/white/red/blue) and AC/DC logo, different visual treatments.

### Mockup 1: "Highway to Flavor" — Bold Horizontal Bands
- Full-bleed horizontal color bands: black, red stripe, blue stripe
- AC/DC logo oversized and centered in hero, white on black
- Red pinstripe navigation bar
- Thick white horizontal rules between sections
- Vibe: concert tour poster / highway billboard

### Mockup 2: "Backstage Pass" — Dark & Moody
- Nearly all-black with chalkboard texture background
- Red as the sole accent (borders, CTAs, hover states, lightning bolt)
- Blue only as secondary accent (links, info badges)
- Semi-transparent dark cards with red left-border
- Vibe: the actual Gas Cafe interior — dark tin ceiling, chalkboard menus

### Mockup 3: "Vinyl Record" — Circular & Retro
- Circular motifs: vinyl records, gas pump gauges, rounded badges
- AC/DC logo inside a large circle (record label style)
- Red/white/blue in equal measure — vintage Americana feel
- Retro halftone dot textures as accents
- Vibe: 1970s rock album packaging meets vintage gas station

### Mockup 4: "Neon Nights" — Electric Glow
- Pure black background, elements styled as neon signs
- AC/DC logo with glowing white neon effect (CSS text-shadow)
- Red and blue as neon glow colors on borders and interactive elements
- Neon-tube underlines on menu items, pulse animation on CTAs
- Vibe: gas station signs glowing on a dark mountain highway

### Mockup 5: "Americana Station" — Clean & Structured
- White background sections alternating with dark sections
- Classic patriotic red/white/blue gas station sign palette
- AC/DC logo contained in a header badge (not oversized)
- Strong grid layout, clear hierarchy
- Menu as a clean scannable layout, blue header/footer bars, red CTAs
- Vibe: modern restaurant site with Gas Cafe rock edge in the typography

### Mockup 6: "Apple Clean" — Premium Minimal
- Pure CSS (no framework), Apple-style design patterns
- Backdrop-blur sticky nav, gradient hero with badge and stats
- Clean typography with subtle hover effects throughout
- Rounded product cards with soft shadows, star-rated review cards
- Dark about section, minimal footer
- Vibe: premium restaurant experience — elegance meets rock & roll

**Deliverable:** 6 HTML files live on GitHub Pages. Customer picks one direction or a hybrid ("layout from #6, colors from #2"). This gates Phase 2.

---

## Phase 2: Build Shared Components (after customer picks direction)

### 2.1 — Design system in Tailwind config
Custom color tokens:
| Token | Hex | Usage |
|-------|-----|-------|
| `gc-black` | `#0a0a0a` | Page background (dark sections) |
| `gc-charcoal` | `#1a1a1a` | Cards, panels |
| `gc-dark` | `#222222` | Hover states |
| `gc-red` | `#dc2626` | CTAs, accents, prices |
| `gc-blue` | `#1e3a8a` | Headers, info, secondary accent |
| `gc-white` | `#f5f5f5` | Text, light backgrounds |
| `gc-gray` | `#9ca3af` | Body text, muted elements |

Fonts: `font-metal` (Metal Mania), `font-bebas` (Bebas Neue), `font-body` (Inter) — all self-hosted.

### 2.2 — Header partial (`_partials/header.php`)
- Sticky nav bar with AC/DC logo (links home)
- Links: Home, Menu, Shop, About, Reviews, Contact
- Mobile hamburger → slide-out drawer
- Phone number visible on desktop, clickable `tel:` link
- Snipcart cart icon with item count badge (shop pages)

### 2.3 — Footer partial (`_partials/footer.php`)
- AC/DC logo (smaller)
- Address, phone, hours
- Social links: Facebook, Yelp
- "Grillin' High in the Rockies since 1998"
- Copyright

### 2.4 — Image optimization
- Rename hash-named scraped images to descriptive names
- Resize: 1200px (full) and 400px (thumbnail)
- Convert to WebP with JPG fallback via `<picture>` elements
- Compress at quality 80

---

## Phase 3: Build All Pages

### 3.1 — Home (`index.php`)
1. **Hero:** Full-viewport, dark background (chalkboard texture), AC/DC logo centered, tagline, scroll indicator
2. **Hours card:** Business hours + food photo
3. **Featured menu highlights:** 3-4 hero food photos linking to menu page
4. **"Grillin' High" callout:** Since 1998 graphic/treatment
5. **Quick info:** Address, phone, Mountain Express bus note
6. **Reviews teaser:** 1-2 customer quotes

### 3.2 — Menu (`menu.php`)
1. **Time note:** Breakfast until 11:30 AM, lunch after
2. **Sticky category nav:** Tabs that scroll to sections
3. **Breakfast section** — all 10 items with descriptions and prices
4. **Hot Sandwiches section** — 13 items, comes with fries
5. **Cold Sammies & Salads** — build-your-own ($11.99)
6. **Burgers & Fries** — "Best in the Butte" callout, 4 burgers + toppings
7. **Sides** — fries, rings, chicken fingers, nuggets

Menu content is **database-driven** — reads from the CMS (see Phase 3A). Prices extracted from menu board photos and stored in `web-scrape/menu.md` as reference.

### 3.3 — Shop (`shop.php`)
Product catalog is **database-driven** — reads from the CMS (see Phase 3A). Initial products identified from store photos:
- **Hats:** Gas/Cafe AC/DC-style caps, Gasser One Stop trucker hats, bucket hats
- **Hoodie:** Black "Gasser One Stop" hoodie
- **Cooler bag:** Black with gold AC/DC-style logo + "Crested Butte, CO"
- **Koozie:** Green with gas pump stealie logo
- **Stickers:** Gas Cafe sticker (red/white/blue pump logo)

**E-commerce: Snipcart** (recommended):
- Cart stays on-site (no redirect to external checkout)
- $0/mo base, 2% transaction fee
- Snipcart `data-item-*` attributes generated dynamically from product database
- Stripe handles payment processing

### 3.4 — About (`about.php`)
1. **Story header:** "Grillin' High in the Rockies since 1998" with hero image
2. **About text:** Deli, gas station, convenience store, rock & roll vibe
3. **Mountain Express bus:** Free bus every 15 min right next to the shop
4. **Photo gallery:** Interior shots, counter, atmosphere
5. **Newspaper clipping:** The original opening photo (founders Gitin and Eric Tunkey)
6. **Logo showcase:** AC/DC logo, Gasser Thrasher, stealie

### 3.5 — Reviews (`reviews.php`)
1. **Featured reviews:** Laura S. (Facebook) and Kristin C. (Yelp) as styled quote cards
2. **"Best in the Butte" callout:** Burger award highlight
3. **Review platform links:** "Read more on Facebook / Yelp / Google"
4. **CTA:** "Tried us? Leave a review!" with platform links

### 3.6 — Contact (`contact.php`)
1. **Contact form:** Name, email, subject, message, consent checkbox
2. **Google Maps embed:** 602 Butte Ave, Crested Butte
3. **Direct info:** Phone (clickable), address, hours
4. **Social links:** Facebook, Yelp icons

**Form backend:** PHP `mail()` with honeypot spam field + rate limiting via sessions.

---

## Phase 3A: Admin CMS (Menu & Store Management)

A lightweight PHP + MySQL admin panel so the customer can manage menu items and store products without touching code. Bluehost includes MySQL via cPanel — no extra cost.

### Architecture

Two independent CRUD systems sharing one admin shell:

```
site/
├── admin/
│   ├── .htaccess              # Password-protect the admin area
│   ├── index.php              # Admin dashboard (links to menu + store)
│   ├── login.php              # Session-based auth
│   ├── logout.php
│   ├── menu/
│   │   ├── index.php          # List all menu items (sortable by category)
│   │   ├── edit.php           # Create / edit a menu item
│   │   └── delete.php         # Soft-delete (mark inactive)
│   ├── store/
│   │   ├── index.php          # List all products
│   │   ├── edit.php           # Create / edit a product
│   │   ├── upload.php         # Product image upload handler
│   │   └── delete.php         # Soft-delete (mark inactive)
│   └── includes/
│       ├── db.php             # PDO connection (credentials from .env.php)
│       ├── auth.php           # Session check middleware
│       └── functions.php      # Shared helpers (CSRF token, sanitize, flash messages)
├── .env.php                   # DB credentials (outside admin/, never committed)
```

### Database Schema

**`menu_categories`**
| Column | Type | Notes |
|--------|------|-------|
| id | INT AUTO_INCREMENT | PK |
| name | VARCHAR(100) | e.g. "Breakfast", "Hot Sandwiches", "Burgers & Fries" |
| slug | VARCHAR(100) | URL-safe name |
| sort_order | INT | Display order |
| subtitle | VARCHAR(255) | e.g. "Served til 11:30", "Voted Best in the Butte!" |
| show_prices | TINYINT(1) | Default 1 |

**`menu_items`**
| Column | Type | Notes |
|--------|------|-------|
| id | INT AUTO_INCREMENT | PK |
| category_id | INT | FK → menu_categories |
| name | VARCHAR(150) | Item name |
| description | TEXT | Full description |
| price | DECIMAL(6,2) | NULL if no single price (e.g. build-your-own) |
| price_label | VARCHAR(50) | Optional, e.g. "$2.99 / $3.99" for size variants |
| sort_order | INT | Display order within category |
| is_active | TINYINT(1) | Soft delete / seasonal toggle |
| created_at | DATETIME | |
| updated_at | DATETIME | |

**`store_products`**
| Column | Type | Notes |
|--------|------|-------|
| id | INT AUTO_INCREMENT | PK |
| name | VARCHAR(150) | Product name |
| description | TEXT | |
| price | DECIMAL(6,2) | |
| sizes | VARCHAR(255) | JSON or comma-separated, e.g. "S,M,L,XL" |
| image_path | VARCHAR(255) | Relative path to uploaded product image |
| snipcart_id | VARCHAR(100) | Unique ID for Snipcart data-item-id |
| is_active | TINYINT(1) | Soft delete |
| sort_order | INT | Display order |
| created_at | DATETIME | |
| updated_at | DATETIME | |

### Admin Features

**Menu Manager:**
- List view grouped by category, drag-to-reorder (or sort_order input)
- Add/edit item: name, description, price, price_label, category (dropdown), active toggle
- Add/edit category: name, subtitle, sort order
- Toggle items active/inactive (seasonal items, 86'd items)
- Seed script to import current menu from `web-scrape/menu.md`

**Store Manager:**
- List view with product thumbnails
- Add/edit product: name, description, price, sizes, image upload, active toggle
- Image upload with resize to 800px max width, stored in `images/merch/`
- Toggle products active/inactive

**Shared:**
- Session-based login (single admin account, credentials in `.env.php`)
- CSRF token on all forms
- Flash messages for success/error feedback
- Responsive admin layout (Tailwind CDN for admin pages — separate from public site CSS)
- All DB queries use PDO prepared statements (SQL injection prevention)

### Public Pages Read from DB

`menu.php` queries `menu_categories` + `menu_items` (WHERE is_active=1) grouped by category, ordered by sort_order. No hardcoded menu content.

`shop.php` queries `store_products` (WHERE is_active=1) and generates Snipcart `data-item-*` attributes dynamically from each product row.

### Security

- Admin directory behind `.htaccess` IP restriction (optional) + PHP session auth
- `.env.php` returns early if accessed directly (`if (!defined('APP_ROOT')) die()`)
- PDO prepared statements for all queries
- CSRF tokens on all write operations
- Image upload validates file type + max size, renames to prevent directory traversal
- Rate limiting on login (prevent brute force)

---

## Phase 4: SEO, Performance & Polish

### SEO
- Unique `<title>` + `<meta description>` per page
- Open Graph tags (og:title, og:description, og:image)
- JSON-LD structured data: LocalBusiness schema (name, address, phone, hours, menu URL)
- `robots.txt` + `sitemap.xml`
- Clean URLs via `.htaccess` (`/menu` → `menu.php`)

### Performance
- WebP images with JPG fallback, lazy loading below fold
- Self-hosted fonts with `font-display: swap`
- Single compiled CSS (<30KB minified), deferred JS
- Target: Lighthouse 90+ across all metrics

### Accessibility
- Semantic HTML (nav, main, section, footer)
- Alt text on all images, aria-labels on icon buttons
- Focus states, skip-to-content link, keyboard-navigable mobile menu
- WCAG AA contrast ratios (careful with red-on-black — use `#ef4444` minimum)

### `.htaccess`
- Clean URL rewrites
- HTTPS redirect
- Security headers (X-Content-Type-Options, X-Frame-Options)
- GZIP compression
- Browser caching (images 1yr, CSS/JS 1mo)

---

## Phase 5: Deploy to Bluehost

1. `npm run build` — compile minified Tailwind CSS
2. Create MySQL database via Bluehost cPanel, run schema SQL
3. Run seed script to import menu items from `web-scrape/menu.md`
4. Upload `.env.php` with production DB credentials (never in git)
5. SFTP upload to `/public_html/` (all `.php`, `admin/`, `css/`, `js/`, `images/`, `fonts/`, `.htaccess`, `robots.txt`, `sitemap.xml`)
6. Do NOT upload: `node_modules/`, `package.json`, `tailwind.config.js`, `src/`
7. Verify file permissions: directories 755, files 644, `.env.php` 600
8. Enable SSL (Let's Encrypt via cPanel)
9. Test all pages, admin CMS, contact form, shop checkout (Snipcart test mode)
10. Switch Snipcart to live mode after customer approval

---

## Phase 6: Verification

- [ ] All 6 pages load, no 404s, all internal links work
- [ ] Mobile hamburger menu opens/closes correctly
- [ ] Contact form submits and delivers email
- [ ] Phone number clickable on mobile
- [ ] Google Maps embed loads
- [ ] All images load (no broken images)
- [ ] Shop: add to cart, change size, remove, checkout (test mode)
- [ ] Clean URLs work (`/menu`, `/shop`, etc.)
- [ ] HTTPS works, HTTP redirects
- [ ] Chrome, Safari, Firefox desktop + iOS Safari, Android Chrome
- [ ] Lighthouse: Performance 90+, Accessibility 95+, SEO 95+
- [ ] Google Business Profile updated with new URL
- [ ] Admin CMS: login works, CRUD menu items, CRUD store products
- [ ] Admin CMS: image upload for store products works
- [ ] Admin CMS: toggling active/inactive reflects on public pages
- [ ] Admin CMS: menu changes show immediately on menu.php

---

## Sequencing

| Phase | Depends On | Effort | Deliverable |
|-------|-----------|--------|-------------|
| 0: Archive + Scaffold | — | 1-2hr | Clean project structure ✅ |
| 1: Design Mockups | Phase 0 | 4-6hr | 6 HTML mockups for customer review ✅ |
| **CUSTOMER PICKS DIRECTION** | Phase 1 | — | **⬅️ WE ARE HERE** |
| 2: Shared Components | Customer decision | 2-3hr | Header, footer, design system |
| 3: Build Pages | Phase 2 | 8-12hr | All 6 public pages |
| 3A: Admin CMS | Phase 2 | 6-8hr | Menu + Store CRUD, DB schema, seed data |
| 4: SEO + Polish | Phase 3 + 3A | 2-3hr | Production-ready |
| 5: Deploy | Phase 4 | 2-3hr | Live on Bluehost (includes DB setup) |
| 6: Verification | Phase 5 | 1-2hr | Signed off |

**Total:** ~25-35 hours dev + customer review turnaround at the mockup gate.

---

## Open Items (need customer input)

1. **Design direction** — pick a mockup or hybrid (e.g., "layout from #6, colors from #2")
2. **Menu prices** — not on the current website; need current pricing
3. **Merch catalog** — confirm exact products, prices, available sizes
4. **Shipping policy** — for merch orders (flat rate? free over $X?)
5. **Business email** — for contact form delivery
6. **Domain** — keeping gascafe1stop.com or changing?
7. **Google Reviews** — add live widget or stick with curated quotes?
8. **Future ordering** — should we include a placeholder "Order Online Coming Soon" button?
