# Astro — Custom Learning Documentation 🚀

## Table of Contents
1. What Is Astro?
2. Why Astro?
3. Main Philosophy
4. How Astro Works Internally
5. Rendering Lifecycle
6. Project Structure
7. Astro Components
8. Props
9. Layouts
10. Routing
11. Dynamic Routes
12. Data Fetching
13. Islands Architecture
14. Client Directives
15. React Integration
16. Tailwind Integration
17. Environment Variables
18. Images & Assets
19. SSG vs SSR
20. API Integration
21. Authentication
22. SEO
23. Performance Optimization
24. Deployment
25. Astro + NestJS Architecture
26. Best Practices
27. Common Mistakes
28. Interview Questions
29. Final Mental Model

---

# What Is Astro?

Astro is a modern frontend framework focused on delivering extremely fast websites.

Core Philosophy:

```txt
Ship Less JavaScript
```

Astro renders content on the server and only sends JavaScript for components that actually require interactivity.

---

# Why Astro?

Traditional frameworks often hydrate the entire page.

```txt
Browser
  ↓
Download JS
  ↓
Hydrate App
  ↓
Interactive
```

Astro:

```txt
Browser
  ↓
HTML Ready
  ↓
Content Visible
  ↓
Optional Hydration
```

Benefits:
- Better SEO
- Better Lighthouse Scores
- Faster Initial Load
- Smaller Bundle Size
- Improved User Experience

---

# Main Philosophy

```txt
HTML First
JavaScript Only When Needed
```

Astro is content-first rather than application-first.

Ideal for:
- Blogs
- Documentation
- Company Websites
- Landing Pages
- Portfolios

---

# How Astro Works Internally

Request Flow:

```txt
User Request
      ↓
Astro Server
      ↓
Build HTML
      ↓
Send HTML
      ↓
Hydrate Interactive Islands
```

---

# Rendering Lifecycle

```txt
Component
    ↓
Astro Compiler
    ↓
Static HTML
    ↓
Browser
```

Most pages need no JavaScript at all.

---

# Project Structure

```txt
src/
├── pages/
├── layouts/
├── components/
├── styles/
├── content/

public/
astro.config.mjs
package.json
```

## pages
Contains routes.

## components
Reusable UI.

## layouts
Shared page structure.

## public
Static assets.

---

# Astro Components

```astro
---
const title = "Hello Astro";
---

<h1>{title}</h1>
```

Structure:

```txt
Frontmatter
    +
Template
```

---

# Props

Component:

```astro
---
const { title } = Astro.props;
---

<h1>{title}</h1>
```

Usage:

```astro
<Card title="My Blog" />
```

---

# Layouts

BaseLayout:

```astro
<html>
  <body>
    <slot />
  </body>
</html>
```

Usage:

```astro
<BaseLayout>
  <h1>Home</h1>
</BaseLayout>
```

---

# Routing

```txt
src/pages/index.astro
```
→ /

```txt
src/pages/about.astro
```
→ /about

---

# Dynamic Routes

```txt
src/pages/blog/[slug].astro
```

Examples:

```txt
/blog/react
/blog/astro
```

```astro
const { slug } = Astro.params;
```

---

# Data Fetching

```astro
---
const response = await fetch(
  "http://localhost:8000/blogs"
);

const blogs = await response.json();
---
```

No useEffect.
No useState.

---

# Islands Architecture

Astro's most important concept.

```txt
Header
Footer
Content
```
remain static.

```txt
Like Button
Comment Box
Search Input
```
receive JavaScript.

---

# Client Directives

## client:load

```astro
<Button client:load />
```

Load immediately.

## client:visible

```astro
<Button client:visible />
```

Load when visible.

## client:idle

```astro
<Button client:idle />
```

Load when browser becomes idle.

---

# React Integration

Install:

```bash
npx astro add react
```

Use:

```astro
---
import Counter from "./Counter.jsx";
---

<Counter client:load />
```

---

# Tailwind Integration

Install:

```bash
npx astro add tailwind
```

Usage:

```html
<h1 class="text-4xl font-bold">
  Hello Astro
</h1>
```

---

# Environment Variables

.env

```env
PUBLIC_API_URL=http://localhost:8000
```

Usage:

```js
import.meta.env.PUBLIC_API_URL
```

---

# Images & Assets

```txt
public/logo.png
```

```html
<img src="/logo.png" alt="logo" />
```

---

# SSG vs SSR

## SSG

Generated at build time.

```bash
npm run build
```

Best for:
- Blogs
- Docs
- Portfolios

## SSR

```astro
export const prerender = false;
```

Best for:
- User Dashboards
- Dynamic Content
- Auth Pages

---

# API Integration

```astro
---
const blogs = await fetch(
  "http://localhost:8000/blogs"
).then(res => res.json());
---
```

---

# Authentication

Typical Flow:

```txt
Login
   ↓
JWT Generated
   ↓
Stored in Cookie
   ↓
Protected Routes
```

---

# SEO

Astro is naturally SEO friendly because:

- HTML is pre-rendered
- Fast loading
- Clean markup

Example:

```astro
<head>
  <title>My Blog</title>
  <meta name="description" content="Astro Blog" />
</head>
```

---

# Performance Optimization

Checklist:

- Optimize Images
- Lazy Load Components
- Use Islands Architecture
- Avoid Unnecessary React Components
- Minimize Client JS

---

# Deployment

Supported Platforms:

- Vercel
- Netlify
- Cloudflare Pages
- Railway
- VPS

Build:

```bash
npm run build
```

---

# Astro + NestJS Architecture

```txt
Frontend (Astro)
        ↓
NestJS Backend
        ↓
PostgreSQL
```

Blog Flow:

```txt
User
 ↓
Astro
 ↓
NestJS API
 ↓
Database
```

---

# Best Practices

1. Keep pages mostly static.
2. Use React only when required.
3. Create reusable layouts.
4. Store API URLs in env files.
5. Keep components small.

---

# Common Mistakes

❌ Using React everywhere.

❌ Loading large client bundles.

❌ Ignoring Islands Architecture.

❌ Fetching client-side unnecessarily.

---

# Interview Questions

### What is Astro?

A performance-first frontend framework that ships minimal JavaScript.

### What is Islands Architecture?

A pattern where only interactive components receive JavaScript.

### Difference between SSG and SSR?

SSG generates pages at build time.
SSR generates pages per request.

### Why is Astro fast?

Because it sends mostly HTML instead of large JavaScript bundles.

---

# Final Mental Model

```txt
Astro
   ↓
HTML First
   ↓
Minimal JavaScript
   ↓
Fast Websites
```

Golden Rule:

```txt
Use Astro for Content.
Use React for Interactivity.
```
