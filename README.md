
# 📚 ASM Management Consultations - Technical Documentation

## 📋 Overview

**ASM Management Consultations** - A modern multi-page website built with **Vanilla JavaScript** and **Vite** build system, optimized for high performance.

### Key Features

- ⚡ **High Performance**: Optimized for 90+ Lighthouse score
- 🌐 **Bilingual**: Arabic/English with automatic RTL support
- 🌙 **Dark Mode**: Smooth theme switching
- 📱 **Responsive Design**: Works on all devices
- 🔗 **Clean URLs**: `/about` instead of `/about.html`

---

## 📁 Project Structure

```
ASM Project v3/
├── 📄 index.html          # Homepage
├── 📄 about.html           # About page
├── 📄 services.html        # Services page
├── 📄 contact.html         # Contact page
├── 📄 faq.html             # FAQ page
├── 📄 booking.html         # Booking page
│
├── 📂 js/                  # JavaScript source
│   ├── app.js              # Main entry point
│   ├── components.js       # Component loader
│   ├── content.js          # i18n content data
│   ├── darkMode.js         # Dark mode handler
│   ├── i18n.js             # Translation engine
│   ├── services-data.js    # Services data
│   ├── utils.js            # Helper functions
│   └── 📂 modules/         # Lazy-loaded modules
│       ├── accordion.js    # FAQ accordion
│       ├── booking.js      # Booking page logic
│       ├── events.js       # Event handlers
│       ├── forms.js        # Form handling
│       ├── modal-ui.js     # Modal component
│       ├── navbar-ui.js    # Navbar behavior
│       └── services-ui.js  # Services rendering
│
├── 📂 css/                 # Stylesheets
│   ├── variables.css       # Design tokens
│   ├── base.css            # Base styles
│   ├── layout.css          # Layout system
│   ├── components.css      # Component imports
│   ├── pages.css           # Page style imports
│   ├── 📂 components/      # Component styles
│   └── 📂 pages/           # Page-specific styles
│
├── 📂 components/          # Reusable HTML components
│   ├── navbar.html
│   ├── footer.html
│   └── modal.html
│
├── 📂 assets/              # Static assets
│   ├── images/
│   └── fonts/
│
├── 📂 public/              # Files copied to dist
│   ├── components/         # Production components
│   ├── .htaccess           # Apache config
│   ├── 404.html            # Error page
│   └── ...
│
├── 📂 dist/                # Build output (auto-generated)
│
├── 📄 vite.config.js       # Vite configuration
├── 📄 package.json         # Dependencies
└── 📄 postcss.config.cjs   # PostCSS config
```

---

## 🔧 Build System (Vite)

### NPM Scripts

| Command                 | Description                          |
| ----------------------- | ------------------------------------ |
| `npm run dev`           | Start development server (port 3000) |
| `npm run build`         | Build for production                 |
| `npm run preview`       | Preview production build             |
| `npm run build:analyze` | Build with bundle analysis           |

### Vite Configuration

**Code Splitting:**

```javascript
manualChunks: {
  vendor: ["./js/utils.js", "./js/darkMode.js"],        // Core utilities
  i18n: ["./js/i18n.js", "./js/content.js"],            // Translations
  "services-data": ["./js/services-data.js"],           // Large, lazy-loaded
  "ui-modules": [...],                                   // UI components
  "page-modules": [...],                                 // Page-specific
}
```

**Clean URLs Plugin:**

- Rewrites `/about` → `/about.html` internally
- Works in both dev and preview servers

**Minification:**

- Uses Terser for JS compression
- Removes console.log in production
- PostCSS with cssnano for CSS

---

## 🎨 CSS Architecture

### Design Tokens (`variables.css`)

```css
:root {
  /* Colors */
  --color-primary: #0d9488;
  --color-secondary: #0ea5e9;

  /* Gradients */
  --gradient-primary: linear-gradient(135deg, #0d9488, #0ea5e9);

  /* Spacing (4px base) */
  --space-4: 1rem;
  --space-8: 2rem;

  /* Typography */
  --font-ar: "Cairo", sans-serif;
  --font-en: "Inter", sans-serif;
}

/* Dark mode overrides */
[data-theme="dark"] {
  --color-bg: #0a0f1a;
  --color-text: #f8fafc;
}
```

### CSS File Organization

| File             | Purpose                              |
| ---------------- | ------------------------------------ |
| `variables.css`  | Design tokens, CSS custom properties |
| `base.css`       | Reset, typography, global styles     |
| `layout.css`     | Grid, containers, sections           |
| `components.css` | Imports all component styles         |
| `pages.css`      | Imports all page-specific styles     |

---

## ⚡ JavaScript Architecture

### Entry Point (`app.js`)

```javascript
async function init() {
  // 1. Load shared components (critical)
  await loadAllComponents();

  // 2. Render content based on language (critical for CLS)
  renderContent(pageName, lang);

  // 3. Initialize dark mode (visible)
  initDarkMode();

  // 4. Deferred: Load modules and bind events
  deferWork(async () => {
    await loadModulesLazily();
    events.bindEvents(pageName);
  });
}
```

### Module System

| Module             | Description                                           |
| ------------------ | ----------------------------------------------------- |
| `utils.js`         | DOM helpers (`$`, `$$`), `onReady()`, `getPageName()` |
| `components.js`    | Loads navbar, footer, modal via fetch                 |
| `i18n.js`          | Language switching, content rendering                 |
| `content.js`       | All translatable content (AR/EN)                      |
| `darkMode.js`      | Theme persistence and switching                       |
| `services-data.js` | Services categories and items                         |

### Lazy Loading

```javascript
// Modules loaded only when needed
const servicesModule = await import("./modules/services-ui.js");
const accordionModule = await import("./modules/accordion.js");
```

---

## 🌐 Internationalization (i18n)

### How It Works

1. **Data Attributes in HTML:**

```html
<h1 data-content="hero_title"></h1>
<input data-placeholder="form_email" />
```

2. **Content Object (`content.js`):**

```javascript
export const CONTENT = {
  ar: {
    home: {
      hero_title: "شريكك الأمثل في النجاح",
    },
  },
  en: {
    home: {
      hero_title: "Your Partner in Success",
    },
  },
};
```

3. **Rendering:**

```javascript
renderContent(pageName, lang);
// Fills all [data-content] elements with matching keys
```

### Language Switching

```javascript
// User triggers language change
switchLanguage("en");
// - Saves to localStorage
// - Updates html[lang] and html[dir]
// - Re-renders all content
```

---

## 🌙 Dark Mode

### Implementation

```javascript
// Check saved preference or system preference
const saved = localStorage.getItem("theme");
const prefersDark = matchMedia("(prefers-color-scheme: dark)").matches;

// Apply theme
document.documentElement.setAttribute("data-theme", "dark");
```

### CSS Variables

```css
[data-theme="dark"] {
  --color-bg: #0a0f1a;
  --color-bg-alt: #111827;
  --color-text: #f8fafc;
  --color-border: #1e293b;
  --shadow-sm: 0 2px 8px rgba(0, 0, 0, 0.3);
}
```

---

## 📦 Build Output

### Production Build

```bash
npm run build
```

**Output structure:**

```
dist/
├── index.html              # Minified HTML
├── about.html
├── js/
│   ├── main.[hash].js      # Entry point
│   └── chunks/
│       ├── vendor.[hash].js      # ~1.4 KB
│       ├── i18n.[hash].js        # ~22 KB
│       └── services-data.[hash].js # ~70 KB
├── css/
│   ├── main.[hash].css     # Core styles
│   └── pages.[hash].css    # Page styles
├── components/             # HTML components
├── .htaccess              # Apache config
└── _redirects             # CDN redirects
```

### Cache Strategy

- JS/CSS files have content hashes → immutable caching
- HTML files → short cache, revalidate
- Assets → long-term caching with immutable header

---

## 🔗 Clean URLs

### Server Configuration

**Apache (.htaccess):**

```apache
RewriteEngine On

# Redirect .html to clean URL
RewriteCond %{THE_REQUEST} \.html [NC]
RewriteRule ^(.*)\.html$ /$1 [R=301,L]

# Serve clean URL as .html
RewriteCond %{REQUEST_FILENAME} !-d
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME}.html -f
RewriteRule ^(.*)$ $1.html [L]
```

**Netlify/Cloudflare (\_redirects):**

```
/about.html  /about  301
/about       /about.html  200
```

---

## 🛠️ Adding New Content

### New Page

1. Create `newpage.html` with standard structure
2. Add to `vite.config.js` → `rollupOptions.input`
3. Add content in `content.js`
4. Add nav link in `components/navbar.html`
5. Update `sitemap.xml`

### New Service Category

Edit `js/services-data.js`:

```javascript
export const SERVICES = {
  categories: [
    {
      id: "new-category",
      title_ar: "الفئة الجديدة",
      title_en: "New Category",
      icon: "fas fa-star",
      services: [...]
    }
  ]
};
```

### New Translation

Add to `js/content.js`:

```javascript
CONTENT.ar.pagename.key = "النص العربي";
CONTENT.en.pagename.key = "English text";
```

Use in HTML:

```html
<span data-content="key"></span>
```

---

## ⚡ Performance Optimizations

| Optimization       | Implementation                      |
| ------------------ | ----------------------------------- |
| Code Splitting     | Vite manual chunks                  |
| Lazy Loading       | Dynamic imports, `loading="lazy"`   |
| Critical CSS       | Preload essential stylesheets       |
| Image Optimization | WebP format, lazy loading           |
| Font Loading       | `font-display: optional`            |
| Compression        | GZIP via .htaccess                  |
| Caching            | Immutable headers for hashed assets |
| Minification       | Terser (JS), cssnano (CSS)          |

---

## 📝 Code Conventions

### JavaScript

- ES Modules (`import`/`export`)
- Async/await for promises
- JSDoc comments for functions

### CSS

- BEM naming: `.block__element--modifier`
- CSS custom properties for theming
- Mobile-first responsive design

### HTML

- Semantic elements (`<main>`, `<nav>`, `<section>`)
- Data attributes for dynamic content
- Accessible (ARIA labels, alt text)

---

**Last Updated**: February 2026
