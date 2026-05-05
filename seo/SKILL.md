---
name: seo
description: "Search Engine Optimization (SEO) best practices for web development. Focuses on meta tags, semantic HTML, and performance as a ranking factor."
---

# Search Engine Optimization (SEO) Standards

Mandatory SEO guidelines to ensure high-performance visibility and indexability across all web applications.

## When to Apply

- Building any page or static route
- Implementing metadata (Title tags, Meta descriptions)
- Designing the heading structure
- Integrating semantic HTML

## Core Requirements (Oshyn FE Lead Standards)

### 1. Title Tags & Meta Descriptions
- **Title Tags**: Include proper, descriptive title tags for each page. Each page must have a unique, content-rich title.
- **Meta Descriptions**: Add compelling meta descriptions that accurately summarize page content. Ensure they are between 150-160 characters for optimal display.

### 2. Heading Structure
- **One H1 per Page**: Use a single `<h1>` per page. It should be the most descriptive heading.
- **Logical Hierarchy**: Use `<h2>` through `<h6>` in a nested, logical order. NEVER skip levels (e.g., from H1 to H3).

### 3. Semantic HTML
- **HTML5 Elements**: Use appropriate HTML5 semantic elements (`<header>`, `<main>`, `<section>`, `<article>`, `<footer>`, `<aside>`).
- **Semantic Data**: Use microdata or JSON-LD schema where applicable to enhance context for search engines.

### 4. Performance & Core Web Vitals
- **Vitals as Ranking Factors**: Performance (LCP, CLS, TBT) are paramount for SEO. No layout thrashing allowed.
- **Image Optimization**: Use correct image formats (WebP/AVIF) and ensure explicit `width` and `height` to prevent Cumulative Layout Shift (CLS).

### 5. Social Tags (Open Graph)
- Implement `og:title`, `og:description`, `og:image`, and `og:url` for all public-facing pages to ensure high-quality social sharing.

## ⚠️ SEO Checklist

- [ ] **Unique Page Titles**: Verified all pages have unique title tags.
- [ ] **Meta Descriptions**: Verified all pages have compelling summaries.
- [ ] **Heading Sequence**: Verified logical heading hierarchy (H1 -> H2 -> H3).
- [ ] **Semantic Elements**: Verified use of appropriate HTML5 tags throughout.
- [ ] **Social Metadata**: Verified Open Graph tags for public pages.
- [ ] **Performance Audit**: Verified that Core Web Vitals pass performance thresholds.
