# 📚 توثيق مشروع ASM Management Consultations

## 📋 نظرة عامة

موقع شركة **ASM للاستشارات الإدارية** - موقع حديث متعدد الصفحات مبني بـ **Vanilla JavaScript** مع نظام بناء **Vite** للأداء العالي.

### المميزات الرئيسية

- ⚡ **أداء عالي**: محسّن للحصول على 90+ في Lighthouse
- 🌐 **دعم اللغتين**: عربي/إنجليزي مع RTL تلقائي
- 🌙 **الوضع الداكن**: تبديل سلس بين الوضعين
- 📱 **تصميم متجاوب**: يعمل على جميع الأجهزة
- 🔗 **روابط نظيفة**: `/about` بدلاً من `/about.html`

---

## 📁 هيكل المشروع

```
ASM Project v3/
├── 📄 index.html          # الصفحة الرئيسية
├── 📄 about.html           # من نحن
├── 📄 services.html        # الخدمات
├── 📄 contact.html         # تواصل معنا
├── 📄 faq.html             # الأسئلة الشائعة
├── 📄 booking.html         # حجز موعد
│
├── 📂 js/                  # كود JavaScript
│   ├── app.js              # نقطة الدخول الرئيسية
│   ├── components.js       # تحميل المكونات
│   ├── content.js          # المحتوى متعدد اللغات
│   ├── darkMode.js         # الوضع الداكن
│   ├── i18n.js             # محرك الترجمة
│   ├── services-data.js    # بيانات الخدمات
│   ├── utils.js            # دوال مساعدة
│   └── 📂 modules/         # وحدات إضافية
│       ├── accordion.js    # الأكورديون (FAQ)
│       ├── booking.js      # صفحة الحجز
│       ├── events.js       # أحداث المستخدم
│       ├── forms.js        # النماذج
│       ├── modal-ui.js     # النافذة المنبثقة
│       ├── navbar-ui.js    # شريط التنقل
│       └── services-ui.js  # عرض الخدمات
│
├── 📂 css/                 # ملفات الأنماط
│   ├── variables.css       # المتغيرات (الألوان، الخطوط)
│   ├── base.css            # الأنماط الأساسية
│   ├── layout.css          # التخطيط العام
│   ├── components.css      # استيراد جميع المكونات
│   ├── pages.css           # استيراد أنماط الصفحات
│   ├── styles.css          # ملف الأنماط الرئيسي
│   ├── 📂 components/      # أنماط المكونات
│   │   ├── navbar.css
│   │   ├── footer.css
│   │   ├── buttons.css
│   │   ├── cards.css
│   │   ├── forms.css
│   │   ├── modal.css
│   │   └── ...
│   └── 📂 pages/           # أنماط الصفحات
│       ├── home.css
│       ├── about.css
│       ├── services.css
│       └── ...
│
├── 📂 components/          # مكونات HTML القابلة لإعادة الاستخدام
│   ├── navbar.html         # شريط التنقل
│   ├── footer.html         # الفوتر
│   └── modal.html          # النافذة المنبثقة
│
├── 📂 assets/              # الموارد الثابتة
│   ├── images/             # الصور
│   └── fonts/              # الخطوط
│
├── 📂 public/              # الملفات العامة (تُنسخ للـ dist)
│   ├── components/         # المكونات للإنتاج
│   ├── .htaccess           # إعدادات Apache
│   ├── 404.html            # صفحة الخطأ
│   ├── _headers            # للـ Cloudflare/Netlify
│   ├── _redirects          # التحويلات
│   └── manifest.json       # PWA manifest
│
├── 📂 dist/                # مخرجات البناء (لا تُعدّل يدوياً)
│
├── 📄 vite.config.js       # إعدادات Vite
├── 📄 package.json         # تبعيات المشروع
├── 📄 postcss.config.cjs   # إعدادات PostCSS
└── 📄 sitemap.xml          # خريطة الموقع
```

---

## 🔧 نظام البناء (Vite)

### الأوامر المتاحة

```bash
# تشغيل سيرفر التطوير
npm run dev

# بناء للإنتاج
npm run build

# معاينة البناء
npm run preview

# تحليل حجم الحزم
npm run build:analyze
```

### إعدادات Vite (`vite.config.js`)

```javascript
// الميزات الرئيسية:

// 1. تقسيم الكود (Code Splitting)
manualChunks: {
  vendor: ["./js/utils.js", "./js/darkMode.js"],
  i18n: ["./js/i18n.js", "./js/content.js"],
  "services-data": ["./js/services-data.js"],
  "ui-modules": [...],
  "page-modules": [...],
}

// 2. روابط نظيفة (Clean URLs)
// /about بدلاً من /about.html
function cleanUrlsPlugin() { ... }

// 3. تصغير الكود (Minification)
minify: "terser"
terserOptions: {
  compress: { drop_console: true }
}
```

---

## 🎨 بنية CSS

### المتغيرات (`variables.css`)

```css
:root {
  /* الألوان الأساسية */
  --color-primary: #0d9488; /* أخضر-أزرق */
  --color-secondary: #0ea5e9; /* أزرق فاتح */
  --color-accent: #10b981; /* أخضر */

  /* التدرجات */
  --gradient-primary: linear-gradient(135deg, #0d9488 0%, #0ea5e9 100%);
  --gradient-hero: linear-gradient(
    135deg,
    #021b1a 0%,
    #042f3d 50%,
    #0a1628 100%
  );

  /* المسافات */
  --space-4: 1rem;
  --space-8: 2rem;

  /* الخطوط */
  --font-ar: "Cairo", sans-serif;
  --font-en: "Inter", sans-serif;
}

/* الوضع الداكن */
[data-theme="dark"] {
  --color-bg: #0a0f1a;
  --color-text: #f8fafc;
}
```

### استخدام الأنماط

```html
<!-- في HTML -->
<link rel="stylesheet" href="css/variables.css" />
<link rel="stylesheet" href="css/base.css" />
<link rel="stylesheet" href="css/layout.css" />
<link rel="stylesheet" href="css/components.css" />
<link rel="stylesheet" href="css/pages.css" />
```

---

## ⚡ JavaScript Architecture

### نقطة الدخول (`app.js`)

```javascript
// التسلسل:
async function init() {
  // 1. تحميل المكونات (navbar, footer, modal)
  await loadAllComponents();

  // 2. عرض المحتوى حسب اللغة
  renderContent(pageName, lang);

  // 3. تفعيل الوضع الداكن
  initDarkMode();

  // 4. تحميل الوحدات الإضافية (lazy loading)
  deferWork(async () => {
    await loadModulesLazily();
    // ربط الأحداث
    events.bindEvents(pageName);
  });
}
```

### نظام الترجمة (`i18n.js`)

```javascript
// استخدام data attributes للمحتوى
<h1 data-content="hero_title"></h1>
<input data-placeholder="form_email" />

// المحتوى في content.js
CONTENT = {
  ar: {
    home: {
      hero_title: "شريكك الأمثل في النجاح",
      form_email: "البريد الإلكتروني"
    }
  },
  en: {
    home: {
      hero_title: "Your Partner in Success",
      form_email: "Email"
    }
  }
}
```

### تحميل المكونات (`components.js`)

```javascript
// المكونات تُحمّل عبر fetch
export async function loadAllComponents() {
  await Promise.all([
    loadComponent("navbar-slot", "/components/navbar.html"),
    loadComponent("footer-slot", "/components/footer.html"),
    loadComponent("modal-slot", "/components/modal.html"),
  ]);
}

// في HTML
<div id="navbar-slot"></div>
<!-- يُحمّل navbar.html هنا -->
```

---

## 🌐 نظام اللغات

### تبديل اللغة

```javascript
// في i18n.js
function switchLanguage(lang) {
  setLang(lang); // حفظ في localStorage
  document.documentElement.lang = lang;
  document.documentElement.dir = lang === "ar" ? "rtl" : "ltr";
  renderContent(pageName, lang);
}
```

### إضافة محتوى جديد

1. أضف المفتاح في `js/content.js`:

```javascript
CONTENT = {
  ar: {
    home: {
      new_text: "النص الجديد",
    },
  },
  en: {
    home: {
      new_text: "New Text",
    },
  },
};
```

2. استخدمه في HTML:

```html
<p data-content="new_text"></p>
```

---

## 🌙 الوضع الداكن

### الإعداد

```javascript
// darkMode.js
export function initDarkMode() {
  const saved = localStorage.getItem("theme");
  const prefersDark = window.matchMedia("(prefers-color-scheme: dark)").matches;

  if (saved === "dark" || (!saved && prefersDark)) {
    document.documentElement.setAttribute("data-theme", "dark");
  }
}
```

### CSS

```css
/* في variables.css */
[data-theme="dark"] {
  --color-bg: #0a0f1a;
  --color-bg-alt: #111827;
  --color-text: #f8fafc;
  --color-border: #1e293b;
}
```

---

## 📱 المكونات

### Navbar (`components/navbar.html`)

```html
<nav class="navbar" id="main-navbar">
  <div class="container">
    <a href="/" class="navbar__logo">
      <img src="/assets/images/logo.webp" alt="ASM Logo" />
      <span>A.S.M</span>
    </a>

    <ul class="navbar__menu">
      <li><a href="/" data-content="nav_home">الرئيسية</a></li>
      <li><a href="/about" data-content="nav_about">من نحن</a></li>
      <li><a href="/services" data-content="nav_services">خدماتنا</a></li>
      <li><a href="/contact" data-content="nav_contact">تواصل معنا</a></li>
    </ul>

    <!-- أزرار اللغة والوضع الداكن -->
  </div>
</nav>
```

### Modal (`components/modal.html`)

```html
<div class="modal" id="consultation-modal">
  <div class="modal__content">
    <form id="modal-form">
      <!-- حقول النموذج -->
    </form>
  </div>
</div>
```

---

## 📦 البناء والنشر

### 1. بناء للإنتاج

```bash
npm run build
```

**المخرجات في `dist/`:**

```
dist/
├── index.html
├── about.html
├── services.html
├── ...
├── js/
│   ├── main.[hash].js
│   └── chunks/
│       ├── vendor.[hash].js
│       ├── i18n.[hash].js
│       └── ...
├── css/
│   ├── main.[hash].css
│   └── pages.[hash].css
├── components/
│   ├── navbar.html
│   ├── footer.html
│   └── modal.html
├── .htaccess
├── _redirects
└── ...
```

### 2. النشر على Apache

```apache
# .htaccess يتضمن:
# - ضغط GZIP
# - التخزين المؤقت للمتصفح
# - روابط نظيفة
# - Security Headers

# مثال - روابط نظيفة
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-d
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME}.html -f
RewriteRule ^(.*)$ $1.html [L]
```

### 3. النشر على Netlify/Cloudflare

```
# _redirects
/about.html    /about    301
/services.html /services 301
/about         /about.html 200
```

---

## 🔍 SEO

### Meta Tags

```html
<head>
  <title>ASM | الصفحة</title>
  <meta name="description" content="..." />
  <link rel="canonical" href="https://asm.money/about" />

  <!-- Open Graph -->
  <meta property="og:title" content="..." />
  <meta property="og:description" content="..." />
  <meta property="og:image" content="..." />

  <!-- Hreflang -->
  <link rel="alternate" hreflang="ar" href="..." />
  <link rel="alternate" hreflang="en" href="..." />
</head>
```

### Structured Data

```html
<script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "Organization",
    "name": "ASM Management Consultations",
    "url": "https://asm.money",
    ...
  }
</script>
```

---

## ⚡ تحسينات الأداء

### 1. تحميل كسول (Lazy Loading)

```javascript
// الوحدات تُحمّل عند الحاجة
deferWork(async () => {
  await loadModulesLazily();
});

// الصور
<img loading="lazy" src="..." />;
```

### 2. تقسيم الكود

```javascript
// Vite يقسم الكود تلقائياً
manualChunks: {
  vendor: [...],       // ~1.4 KB
  i18n: [...],         // ~22 KB
  "services-data": [...]  // ~70 KB (محمّل عند الحاجة)
}
```

### 3. التخزين المؤقت

```apache
# في .htaccess
<FilesMatch "\.(js|css|webp|woff2)$">
  Header set Cache-Control "max-age=31536000, immutable"
</FilesMatch>
```

### 4. Critical CSS

```html
<!-- تحميل مسبق للـ CSS الحرج -->
<link rel="preload" href="css/variables.css" as="style" />
<link rel="preload" href="css/base.css" as="style" />
```

---

## 🛠️ إضافة صفحة جديدة

### 1. إنشاء ملف HTML

```html
<!-- newpage.html -->
<!DOCTYPE html>
<html lang="ar" dir="rtl">
  <head>
    <title>ASM | الصفحة الجديدة</title>
    <link rel="canonical" href="https://asm.money/newpage" />
    <!-- CSS -->
  </head>
  <body>
    <div class="page-wrapper">
      <div id="navbar-slot"></div>

      <main id="main" class="main-content" data-page="newpage">
        <!-- المحتوى -->
      </main>

      <div id="footer-slot"></div>
      <div id="modal-slot"></div>
    </div>

    <script type="module" src="js/app.js"></script>
  </body>
</html>
```

### 2. إضافة للـ Vite

```javascript
// vite.config.js
rollupOptions: {
  input: {
    // ...
    newpage: resolve(__dirname, "newpage.html"),
  }
}
```

### 3. إضافة المحتوى

```javascript
// content.js
CONTENT = {
  ar: {
    newpage: {
      title: "عنوان الصفحة",
      description: "وصف الصفحة",
    },
  },
};
```

### 4. إضافة للـ Navbar

```html
<!-- components/navbar.html -->
<li><a href="/newpage" data-content="nav_newpage">الصفحة الجديدة</a></li>
```

---

## ❓ الأسئلة الشائعة للمطورين

### كيف أغير الألوان؟

عدّل المتغيرات في `css/variables.css`

### كيف أضيف خدمة جديدة؟

أضفها في `js/services-data.js` في المصفوفة المناسبة

### كيف أغير معلومات التواصل؟

1. `js/content.js` للنصوص
2. `components/footer.html` للفوتر
3. `contact.html` للصفحة

### أين أضع الصور الجديدة؟

في `assets/images/` - استخدم صيغة WebP للأداء الأفضل

### كيف أختبر الإنتاج محلياً؟

```bash
npm run build
npm run preview
# افتح http://localhost:4173
```

---

## 📞 الدعم

للمساعدة التقنية، تواصل مع فريق التطوير.

---

**آخر تحديث**: فبراير 2026
