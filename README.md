# Akses SEO Platform v2

> Multi-tenant SEO management platform built for signboard & local business clients in Malaysia.

![Laravel](https://img.shields.io/badge/Laravel-13-FF2D20?style=flat&logo=laravel&logoColor=white)
![Filament](https://img.shields.io/badge/Filament-v5-FDAE4B?style=flat)
![MySQL](https://img.shields.io/badge/MySQL-8-4479A1?style=flat&logo=mysql&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-646CFF?style=flat&logo=vite&logoColor=white)
![PHP](https://img.shields.io/badge/PHP-8.2-777BB4?style=flat&logo=php&logoColor=white)

**Live Demo**: [blogpanel.aksesreka.com](https://blogpanel.aksesreka.com/seopov2)

---

## Overview

Akses SEO Platform v2 is a white-label, multi-tenant admin panel that allows an agency (owner) to manage multiple clients and their websites from a single installation. Each client gets isolated access to their own content, SEO settings, and analytics — with zero cross-tenant data leakage.

Built on Laravel 13 + Filament v5, deployed on shared hosting at Hostinger.

---

## Key Features

### Multi-Tenancy
- 3-tier hierarchy: **Owner → Client → Site**
- Per-site data isolation via global `TenantScope` on all 18 content models
- Role system: `owner`, `client_owner`, `editor` with Spatie Permission v7.3
- 150 granular permissions across 15 resources
- IDOR protection via `VerifiesTenantOwnership` policy trait
- Atomic quota enforcement via `QuotaService` (DB-level locks)

### Content Management
- Posts, Services, Service Locations, Products, Projects, Locations
- Tags, Categories, Media Library (with auto-metadata extraction)
- Hero Slider, Redirects Manager, Broken Links checker

### SEO Tooling
- **In-editor SERP Preview** — Google-like live preview with real tenant domain
- **Focus Keyphrase Analyzer** — density check, prominence score, readability hints
- **SEO Score** — per-post scoring (title, meta, keyphrase, readability, schema, AEO, GEO)
- **Internal Link Suggestions** — auto-queries related content by shared tags + keyphrase overlap
- **Schema.org Generator** — Article, LocalBusiness, Product, Service, FAQPage
- **Bulk Service × Location Generator** — generates city-targeted service pages at scale
- **SEO Content Calendar** — month-view calendar with color-coded post pipeline

### AEO & GEO (AI-Era SEO)
- FAQ Repeater on all content types → FAQPage JSON-LD
- `/llms.txt` generator with site info, key pages, AI policy
- Opt-out controls for 14 AI training crawlers via `robots.txt`

### Google Search Console
- Full GSC API integration (site-level OAuth credentials)
- Performance metrics surfaced directly in the Post form (clicks, impressions, CTR, position)
- Top queries widget on dashboard

### Security
- TOTP 2FA (full implementation)
- CSP + HSTS middleware
- Honeypot on public forms
- Input sanitization (`SanitizesSeoFields`)
- Safe redirect validation (`SafeRedirectUrl`)
- Activity logging on 9 models with per-site isolation
- Global FileUpload MIME validation

### Other
- 4 theme palettes with live preview (`ThemeService` singleton + CSS vars)
- Sitemap (7 sub-sitemaps: posts, services, products, projects, locations, service-locations, tags)
- 3-step setup wizard (admin path, credentials, site identity)
- Appearance system (logo, favicon, colors — 1hr cache)
- Deployment Checklist page

---

## Architecture Highlights

```
app/
├── Models/         18 content + settings models, all TenantAware
├── Policies/       12 resource policies with VerifiesTenantOwnership
├── Services/
│   ├── QuotaService          Atomic DB-lock quota enforcement
│   ├── TenantContext         Singleton for safe job/command tenant access
│   ├── RoleAssignmentService Role promotion rules
│   ├── SeoScoreService       Per-post + homepage SEO scoring
│   ├── SchemaService         Schema.org JSON-LD generator
│   └── GoogleSearchConsoleService  GSC API wrapper
├── Http/Middleware/
│   ├── DetectSiteFromDomain  Resolves tenant from public domain
│   ├── ContentSecurityPolicy
│   └── HstsMiddleware
└── Filament/
    ├── Resources/  18 resources (Owner/ClientOwner/Editor scoped)
    └── Pages/      SEO Hub, Content Calendar, Bulk Generator, GSC, Appearance, Setup
```

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Backend | Laravel 13, PHP 8.2 |
| Admin Panel | Filament v5 |
| Database | MySQL 8 |
| Frontend Build | Vite |
| Auth / Roles | Laravel Sanctum + Spatie Permission v7.3 |
| SEO Data | Google Search Console API, Spatie Sitemap |
| Activity Log | Spatie ActivityLog |
| Hosting | Hostinger Shared (cPanel) |

---

## Screenshots

### Dashboard — Site Health & Content Pipeline
![Dashboard showing site health metrics, content pipeline stats, and recent activity](screenshots/01-dashboard.png)

### Multi-Site Management
![Sites list showing multiple client websites managed from a single installation](screenshots/02-sites-list.png)

### In-Editor SERP Preview
![Post editor with live Google SERP preview showing real tenant domain, breadcrumb, favicon and meta description](screenshots/03-serp-preview.png)

### SEO Score Breakdown
![Per-post SEO score panel showing 62/100 with detailed breakdown across Meta, Content, Keyphrase, AEO categories](screenshots/04-seo-score.png)

### Actionable SEO Issues
![SEO issues panel listing 6 specific fixes with clear instructions for each](screenshots/05-seo-issues.png)

### SEO Content Calendar
![Month-view content calendar for April 2026 with pipeline stats and color-coded post chips](screenshots/06-content-calendar.png)

### Lighthouse Scores (Client Site)
![Lighthouse audit showing Performance 72, Accessibility 97, Best Practices 100, SEO 100](screenshots/07-lighthouse.png)

---

## Source Code

This repository is **private**. The source code is available on request for potential employers or collaborators.

Contact: [aksesreka@gmail.com](mailto:aksesreka@gmail.com)
