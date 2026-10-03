---
name: seo-growth-architect
description: "MANDATORY - Must execute view_file on this skill before optimizing SEO, metadata, sitemaps, JSON-LD schema, page speed, copywriting, or analytics tracking. Technical SEO, Schema JSON-LD, Core Web Vitals, CRO, and GA4."
---

# 🔍 SEO & Growth Architect — Technical SEO, Conversion & DataLayer Architecture

This skill maximizes organic search visibility (Technical SEO / Schema JSON-LD), Core Web Vitals performance, Conversion Rate Optimization (CRO), and enterprise analytics event streams (GA4 / GTM DataLayer) for web applications and SaaS platforms.

---

# HARD BANS — UNFORGIVABLE SEO & PERFORMANCE ANTI-PATTERNS

The following practices are **STRICTLY PROHIBITED**:

### 1. Client-Side Only (CSR) Metadata is BANNED
- ❌ **Prohibited:** Setting page titles, meta descriptions, or OpenGraph tags via client-side hooks (e.g., `useEffect(() => { document.title = ... })`).
- 💣 **Failure Mode:** Search engine crawlers (Googlebot, Bingbot) and social link scrapers (Twitter, LinkedIn) receive blank or default metadata, destroying SERP ranking and social CTR.
- ✅ **Mandatory:** Generate metadata server-side via Next.js `generateMetadata()` or SSR HTML tags before hydration.

### 2. Dimensionless Image Tags are BANNED
- ❌ **Prohibited:** Rendering standard `<img>` tags without explicit `width`, `height`, or CSS `aspect-ratio`.
- 💣 **Failure Mode:** When images load asynchronously, the layout jumps abruptly, triggering massive Cumulative Layout Shift (CLS > 0.25) penalties from Google Search algorithms.
- ✅ **Mandatory:** Use `next/image` or apply strict `aspect-ratio` container wrappers to reserve layout space before asset download.

### 3. Non-Slugified Dirty URLs are BANNED
- ❌ **Prohibited:** Exposing URLs with uppercase letters, whitespace `%20`, special characters, or underscores (e.g., `/Products/AI_Terminal%20v2`).
- 💣 **Failure Mode:** Causes duplicate indexing, canonical conflicts, broken external backlinks, and 404 crawl errors.
- ✅ **Mandatory:** Enforce lowercase, hyphenated, clean URL slugs: `/products/ai-terminal-v2`.

### 4. Non-Reciprocal Hreflang Tags are BANNED
- ❌ **Prohibited:** Linking from Language A to Language B without having Language B link reciprocally back to Language A.
- 💣 **Failure Mode:** Google's indexing algorithm rejects one-way hreflang relationships entirely, failing international localization indexing.
- ✅ **Mandatory:** Multi-language setups must provide bidirectional, self-referential alternate hreflang tags across all target locales.

### 5. Blocking Search Engine Crawlers on CSS/JS is BANNED
- ❌ **Prohibited:** Adding `Disallow: /_next/` or blocking CSS/JS assets inside `robots.txt`.
- 💣 **Failure Mode:** Googlebot requires CSS and JavaScript to render and score mobile-friendliness and layout shifts. Blocking assets leads to indexing penalties.
- ✅ **Mandatory:** Keep stylesheet and script assets open to crawler agents; restrict only sensitive administrative routes (`/admin/`, `/api/`, `/checkout/`).

---

# TECHNICAL SEO, SCHEMA & CWV STANDARDS

### 1. Dynamic `sitemap.xml` & `robots.txt`
```text
User-agent: *
Allow: /
Disallow: /api/
Disallow: /admin/
Disallow: /checkout/
Disallow: /*?*sort=

Sitemap: https://www.example.com/sitemap.xml
```

### 2. Multi-Language Hreflang & OpenGraph

In Next.js App Router, declare alternates and OpenGraph via the native `Metadata` API (never inject manual `<link>` tags into root heads):
```typescript
import type { Metadata } from "next";

export const metadata: Metadata = {
  title: "AI Finance Terminal | Real-Time Market Analytics",
  description: "Analyze financial markets with empirical depth and AI intelligence.",
  alternates: {
    canonical: "https://www.example.com/products/ai-terminal",
    languages: {
      en: "https://www.example.com/en/products/ai-terminal",
      tr: "https://www.example.com/tr/products/ai-terminal",
      nl: "https://www.example.com/nl/products/ai-terminal",
      "x-default": "https://www.example.com/en/products/ai-terminal",
    },
  },
  openGraph: {
    type: "website",
    title: "AI Finance Terminal | Real-Time Market Analytics",
    description: "Analyze financial markets with empirical depth and AI intelligence.",
    images: [{ url: "https://www.example.com/assets/og-cover.jpg", width: 1200, height: 630 }],
  },
  twitter: {
    card: "summary_large_image",
  },
};
```

### 3. Structured Data (Schema.org JSON-LD)
```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "Organization",
      "@id": "https://www.example.com/#organization",
      "name": "DCM Development",
      "url": "https://www.example.com",
      "logo": "https://www.example.com/assets/logo.png"
    },
    {
      "@type": "WebSite",
      "@id": "https://www.example.com/#website",
      "url": "https://www.example.com",
      "name": "DCM Development",
      "publisher": { "@id": "https://www.example.com/#organization" },
      "potentialAction": {
        "@type": "SearchAction",
        "target": "https://www.example.com/search?q={search_term_string}",
        "query-input": "required name=search_term_string"
      }
    }
  ]
}
```

### 4. Core Web Vitals Targets
- **LCP (Largest Contentful Paint < 2.5s):** Priority loading on hero media (`priority={true}`).
- **CLS (Cumulative Layout Shift < 0.1):** Explicit dimension reservation on all dynamic slots.
- **INP (Interaction to Next Paint < 200ms):** Zero main-thread blocking loops.

### 5. Standardized GA4 / GTM DataLayer
```typescript
export function trackDataLayerEvent(event: string, payload: Record<string, any>) {
  if (typeof window !== "undefined") {
    window.dataLayer = window.dataLayer || [];
    window.dataLayer.push({ event, ...payload, timestamp: Date.now() });
  }
}
```
