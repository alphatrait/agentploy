# Universal SEO Optimization Playbook (Framework-Agnostic)

## Purpose
A framework-neutral instruction set for any AI or automation agent to implement **SEO optimization** on existing websites or applications — without altering design, layout, or visible content. Works with **React (JSX/TSX)**, **Vue**, **Svelte**, **Angular**, **HTML**, **Next.js**, **Gatsby**, **Nuxt**, or any other framework.

---

## Core Principle — Zero Design Change
- Do **not** modify layout, text, colors, spacing, fonts, or component structure.  
- Do **not** alter existing visible content or reorder elements.  
- Only inject or append elements that are **non-visual** (in `<head>`, or as invisible structured data).
- Add semantic meaning, accessibility improvements, and metadata without touching visuals.

### Allowed Additions
- `<meta>`, `<title>`, `<link>`, `<script type="application/ld+json">` in the document head.
- Invisible attributes on existing elements (e.g., `alt`, `aria-*`, `lang`, `loading`, `decoding`, `width`, `height`).
- ARIA roles or landmark tags for accessibility.
- Internal links only inside existing elements (no new visible content).

### Forbidden Changes
- ❌ No modification of text, CSS classes, or inline styles.  
- ❌ No new visible UI elements, banners, or CTAs.  
- ❌ No layout or spacing changes.  
- ❌ No content rewriting.

---

## Phase 1 — Baseline SEO
**Goal:** Ensure all pages are crawlable, descriptive, and properly indexed.

### 1. Metadata
Add the following tags to `<head>`:
- `<title>`: Unique per page, 45–60 characters.
- `<meta name="description">`: Unique, 120–160 characters.
- `<link rel="canonical">`: Points to the preferred URL.
- Open Graph tags: `og:title`, `og:description`, `og:type`, `og:url`, `og:image`.
- Twitter tags: `twitter:card`, `twitter:title`, `twitter:description`, `twitter:image`.

### 2. Structure and Accessibility
- One logical **H1** per page (keep others as H2–H6 or add `role="heading" aria-level="…"`).
- Add landmark roles: `role="banner"`, `role="navigation"`, `role="main"`, `role="contentinfo"`.
- Ensure all interactive elements (buttons, links, forms) have accessible labels.

### 3. Images
- Add `alt` text describing image purpose; empty `alt=""` for decorative ones.
- Set `width` and `height` attributes to prevent layout shifts.
- Add `loading="lazy"` for below-the-fold images.

### 4. Internal Linking
- Create contextual internal links using existing content blocks or footers.
- Ensure every page links to at least one other relevant page.

### Deliverables
- Meta and OG/Twitter tags present and unique.
- Properly labeled H1 and landmark roles.
- All images have alt and dimensions.
- Internal linking confirmed.

---

## Phase 2 — Structured Data and Index Control
**Goal:** Add schema markup, configuration, and global controls for search engines.

### 1. Central SEO Configuration
Create a config file or system (JSON, YAML, ENV, CMS, etc.) with fields for:
- title, description, canonical, og, twitter, robots, locale.
- Validate each route/page at build time or runtime.

### 2. Structured Data (JSON-LD)
Inject `<script type="application/ld+json">` objects in the `<head>` for:
- **Organization** — site or brand info.
- **Product/Service** — name, description, brand, offers.
- **Article/BlogPosting** — headline, author, datePublished, image.
- **LocalBusiness** — address, contact, geo coordinates.
- **BreadcrumbList** — mirror navigation.

Ensure that structured data:
- Matches visible page content exactly.
- Passes Google Rich Results validation.

### 3. Robots and Sitemap
- Add or update `robots.txt` with `Sitemap:` link.
- Disallow only private or duplicate routes.
- Use `<meta name="robots" content="index, follow">` by default.

### 4. i18n (if applicable)
- Add `<html lang="en">` or appropriate language code.
- Add `<link rel="alternate" hrefLang="…">` for translated versions.

---

## Phase 3 — Performance and Quality Guardrails
**Goal:** Improve Core Web Vitals (CWV) and maintain scalable SEO consistency.

### 1. Performance Targets
- **LCP ≤ 2.0s**, **CLS ≤ 0.1**, **INP ≤ 200ms** (mobile).
- Reserve media space using existing visual dimensions.
- Preload only essential assets (fonts, hero images) if it doesn’t alter visuals.
- Defer third-party scripts (analytics, marketing) until after main render.

### 2. Media Optimization
- Keep visual sizes identical, but offer modern formats (`WebP`, `AVIF`) as optional sources.
- Maintain accurate `alt` text and real file names for better image SEO.

### 3. Validation and Reporting
- Generate an SEO validation report each build/deployment:
  - Missing or duplicate titles/descriptions.
  - Empty or missing `alt` text.
  - Orphan pages (no internal links).
  - Oversized images (>200 KB above the fold).
  - Broken canonical or sitemap links.

### 4. Linking and Crawl Depth
- Every page should be reachable within **three clicks** from home.
- Maintain consistent footer/nav links for crawl paths.

### 5. Compliance and Tracking
- Add optional hooks for Consent Management Platforms (CMPs).
- Use `meta name="robots"` with `max-snippet`, `max-image-preview`, or `max-video-preview` if privacy-sensitive.

---

## Phase 4 — Quality and Maintenance
**Goal:** Continuously enforce SEO and accessibility rules across any framework.

### Checklist for Agents
✅ Head/meta tags complete and unique  
✅ Structured data matches visible content  
✅ Robots.txt and sitemap valid  
✅ H1 hierarchy correct  
✅ All images have alt and dimensions  
✅ Internal linking coverage  
✅ Core Web Vitals within target thresholds  
✅ No visible or layout changes introduced

### Optional Enhancements
- Add a `seo-report.json` summary after each build.
- Integrate Lighthouse or custom SEO linting into CI/CD pipeline.
- Monitor structured data via Search Console API.

