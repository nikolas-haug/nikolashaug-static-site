# Nikolas Haug — Static Site

A static site generator built with Node.js, using markdown content and JSON data files. Compiles to static HTML/CSS/JS suitable for GitHub Pages deployment.

## Features

- **Markdown-based content** — Easy to edit page content in markdown format
- **Blog post system** — Individual post pages generated from `content/posts/`
- **Sveltia CMS** — Browser-based content editor at `/admin`
- **SEO built-in** — Meta tags, Open Graph, Twitter Cards, sitemap, structured data, and `llms.txt`
- **SCSS styling** — Modular SCSS compiled to a single CSS file
- **Mobile-responsive** — Full navigation toggle and responsive layout
- **Fast builds** — Simple Node.js build script with watch mode

---

## Project Structure

```
nikolashaug-static-site/
├── admin/
│   ├── index.html       # Sveltia CMS entry point
│   └── config.yml       # CMS collection configuration
├── assets/
│   └── images/          # Images uploaded via CMS
├── content/
│   ├── pages/           # Markdown files for static pages
│   │   ├── index.md
│   │   ├── fiction.md
│   │   ├── blog.md
│   │   ├── about.md
│   │   └── contact.md
│   └── posts/           # Markdown files for blog posts
│       └── *.md
├── data/                # JSON data files
│   └── site.json        # Site config (siteUrl, nav, social links)
├── static/              # Static assets copied verbatim into build/
│   ├── css/             # Vendor CSS (Font Awesome)
│   ├── js/              # JavaScript files
│   └── webfonts/        # Font Awesome webfonts
├── templates/           # HTML templates
│   ├── page.html        # Generic content page (home, fiction, about)
│   ├── blog.html        # Blog listing page
│   ├── post.html        # Individual blog post
│   ├── contact.html     # Contact page
│   └── partials/        # Reusable template parts (head, header, nav, footer)
├── scripts/
│   └── build-content.js # Main build script (HTML, sitemap, SEO)
├── src/
│   └── styles/          # SCSS source files (compiled to build/css/style.css)
├── llms.txt             # AI discoverability file
└── build/               # Generated output (gitignored)
```

---

## Getting Started

### Prerequisites

- Node.js (v14 or higher)
- npm

### Installation

```bash
npm install
```

### Build the Site

```bash
npm run build
```

This will:
1. Compile SCSS from `src/styles/` to `build/css/style.css`
2. Process markdown to generate HTML in `build/`
3. Copy JavaScript, Font Awesome, and other assets from `static/`
4. Generate `sitemap.xml`, `robots.txt`, and copy `llms.txt`

### Development Workflow

```bash
npm run dev
```

Serve locally:

```bash
npm run serve
```

Then open `http://localhost:3000` in your browser.

---

## Editing Content

### Option A: Sveltia CMS

Go to `https://nikolashaug.com/admin` and log in with your GitHub account.

Update the `repo` and `branch` fields in `admin/config.yml` to match your GitHub repo.

### Option B: Edit files directly

#### Pages

All static page content lives in `content/pages/` as markdown files. Each file uses YAML frontmatter for configuration.

```markdown
---
title: About
layout: page
permalink: /about
metaDescription: A short description for search engines.
---

Your page content here in markdown.
```

#### Blog Posts

Blog posts live in `content/posts/`. Each post uses YAML frontmatter:

```markdown
---
title: My Post Title
date: 2025-07-01
slug: my-post-title
excerpt: A short excerpt shown in the blog listing.
heroImage: images/my-image.jpg
metaDescription: SEO description for this post.
---

Full post content in markdown.
```

Post URLs are flat: `/my-post-title/`

#### Site Configuration

Edit `data/site.json` for:

- Site URL (used for canonical URLs, sitemap, and OG image fallbacks)
- Site title, description, and tagline
- Navigation links
- Social media links
- Google verification code

---

## SEO

All SEO is configured via frontmatter in your markdown files. Most pages only need:

```yaml
---
title: My Page
metaDescription: A great description for search engines (150–160 chars).
---
```

Available frontmatter fields: `metaTitle`, `metaDescription`, `metaKeywords`, `metaAuthor`, `metaRobots`, `canonicalUrl`, `ogTitle`, `ogDescription`, `ogImage`, `ogType`, `twitterTitle`, `twitterDescription`, `twitterImage`, `schemaType`, `heroImage`.

Auto-generated on every build: `sitemap.xml`, `robots.txt`, `llms.txt`.

---

## Deployment

Every push to `master` triggers `.github/workflows/deploy-pages.yml`, which builds and deploys to GitHub Pages.

**One-time setup:**
1. Push the repo to GitHub.
2. Go to **Settings → Pages**.
3. Under "Build and deployment", set **Source** to **GitHub Actions**.

---

## Build Scripts

| Command | Description |
|---|---|
| `npm run build` | Full build (CSS + content) |
| `npm run build:css` | Compile SCSS only |
| `npm run build:content` | Generate HTML only |
| `npm run dev` | Build and watch for changes |
| `npm run serve` | Build and serve locally at localhost:3000 |

---

## Theme & Styling

All styles are in `src/styles/`. The partials follow a standard structure:

- `_variables.scss` — colors, fonts, spacing
- `_base.scss` — base element styles
- `_layout.scss` — page structure (header, main, footer, grid)
- `_components.scss` — reusable UI components (nav, cards, buttons, forms)
- `_utilities.scss` — helper classes
- `_custom.scss` — MailerLite overrides, image wrappers, misc

Font Awesome is included locally via `static/css/font-awesome.css` and `static/webfonts/`.

---

© Nikolas Haug
