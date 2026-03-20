# Implementation Plan: Сведения об образовательной организации

**Feature:** About Organization Page
**File:** `svedeniya-ob-obrazovatelnoy-organizatsii.html`
**Status:** Ready for Implementation
**Estimated Time:** 5-6.5 hours

---

## Quick Reference

### Component Locations

| Component | Source File | Lines | Action |
|-----------|-------------|-------|--------|
| Head meta | `index.html` | 3-108 | Copy & adapt |
| Global UI | `index.html` | 112-142 | Copy |
| Header | `index.html` | 144-159 | Copy & adapt |
| Breadcrumb styles | `styles.css` | 338-363 | Use existing |
| Footer | `index.html` | 1045-1092 | Copy |
| JavaScript | `index.html` | 1094-1135 | Copy & extend |

### Key File Paths

```
Project Root: /Users/artemsuazov/Documents/Products/fregat/

Source Files:
├── index.html (main page)
├── styles.css (design system)
└── tailwind.config.js

Target File:
└── svedeniya-ob-obrazovatelnoy-organizatsii.html (NEW)
```

---

## Implementation Steps

### Step 1: Create File (5 min)

```bash
cd /Users/artemsuazov/Documents/Products/fregat/
touch svedeniya-ob-obrazovatelnoy-organizatsii.html
```

### Step 2: Copy & Adapt Head (15 min)

Copy from `index.html` lines 3-108 and modify:

```html
<title>Сведения об образовательной организации | Школа «Фрегат»</title>
<meta name="description" content="Лицензия ДПО № Л035‑01217‑26/03829175. Полные сведения об образовательной организации, программах обучения, преподавателях и материально-технической базе.">

<!-- ADD NEW: OG Tags -->
<meta property="og:type" content="website">
<meta property="og:title" content="Сведения об образовательной организации | Школа «Фрегат»">
<meta property="og:description" content="Лицензия ДПО № Л035‑01217‑26/03829175. Полные сведения об образовательной организации.">
<meta property="og:url" content="https://fregat-school.ru/svedeniya-ob-obrazovatelnoy-organizatsii.html">
<meta property="og:image" content="https://z-cdn-media.chatglm.cn/files/13817077-3fd8-4076-ab8b-31702a8b0e59.png">
<!-- ... see code-research.md for complete OG tags ... -->

<!-- MODIFY: Schema.org -->
<script type="application/ld+json">
{
    "@context": "https://schema.org",
    "@type": "CollegeOrUniversity",
    "name": "Школа тендерного обучения «Фрегат»",
    <!-- ... see code-research.md for complete schema ... -->
}
</script>
```

### Step 3: Copy Global UI Elements (5 min)

Copy from `index.html` lines 112-142:

- Scroll progress bar
- Back to top button
- Vertical brand text
- Global geometry

### Step 4: Adapt Header (20 min)

Copy from `index.html` lines 144-159 and modify:

```html
<header class="fixed w-full top-0 z-50 backdrop-blur-md border-b border-white/10">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 flex justify-between items-center h-20">
        <!-- Logo (same) -->
        <div class="flex items-center gap-3">
            <img src="..." class="h-12 w-auto logo-clean">
            <span class="text-2xl font-light tracking-widest text-gold-gradient">ФРЕГАТ</span>
        </div>

        <!-- Navigation: UPDATE links -->
        <nav class="hidden md:flex gap-10 text-sm text-gray-300">
            <a href="index.html#advantages">Преимущества</a>
            <a href="index.html#program">Программа</a>
            <a href="index.html#price">Стоимость</a>
            <a href="index.html#faq">FAQ</a>
        </nav>

        <!-- ADD: Search icon + CTA -->
        <div class="flex items-center gap-4">
            <button class="p-2 text-gray-300 hover:text-gold transition" aria-label="Поиск">
                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path>
                </svg>
            </button>
            <a href="index.html#cta-form" class="btn-gold px-6 py-3 rounded text-sm tracking-wide">Записаться</a>
        </div>
    </div>
</header>
```

### Step 5: Add Breadcrumb (10 min)

```html
<!-- After header, before main -->
<nav class="breadcrumb max-w-7xl mx-auto px-4 sm:px-6 lg:px-8" aria-label="Breadcrumb">
    <ol class="flex items-center gap-2">
        <li>
            <a href="index.html" class="breadcrumb-item hover:text-gold flex items-center gap-1">
                <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6"></path>
                </svg>
                Главная
            </a>
        </li>
        <li>
            <span class="breadcrumb-separator" aria-hidden="true">→</span>
        </li>
        <li>
            <span class="breadcrumb-item active" aria-current="page">Сведения об образовательной организации</span>
        </li>
    </ol>
</nav>
```

### Step 6: Create Content Sections (2-3 hours)

Use existing design system patterns:

```html
<main>
    <!-- Hero Section -->
    <section class="py-24 border-t border-white/5">
        <div class="max-w-7xl mx-auto px-6 text-center animate-section">
            <h1 class="text-4xl md:text-5xl lg:text-6xl font-bold text-white mb-6">
                Сведения об <span class="text-gold-gradient">образовательной организации</span>
            </h1>
            <p class="text-gray-400 text-lg">
                Лицензия на образовательную деятельность № Л035‑01217‑26/03829175
            </p>
        </div>
    </section>

    <!-- Organization Info -->
    <section class="py-24 border-t border-white/5 bg-[#0d181b]">
        <div class="max-w-7xl mx-auto px-6">
            <h2 class="text-3xl font-bold mb-8 text-white">Об организации</h2>
            <div class="grid md:grid-cols-2 gap-8">
                <div class="bg-[#142125] border-gold p-6">
                    <h3 class="text-gold-gradient font-bold mb-2">Полное наименование</h3>
                    <p class="text-gray-300">ООО «Фрегат»</p>
                </div>
                <!-- ... more sections ... -->
            </div>
        </div>
    </section>

    <!-- License & Documents -->
    <!-- ... use card components ... -->

    <!-- Programs -->
    <!-- ... use grid layout ... -->

    <!-- Teachers -->
    <!-- ... similar to index.html teachers section ... -->

    <!-- Material Base -->
    <!-- ... use card components ... -->
</main>
```

### Step 7: Copy Footer (5 min)

Copy from `index.html` lines 1045-1092 without modifications.

### Step 8: Copy & Extend JavaScript (20 min)

Copy from `index.html` lines 1094-1135 and add:

```javascript
// ... existing scroll animation, progress bar, back-to-top code ...

// NEW: Search handler (placeholder)
document.querySelector('[aria-label="Поиск"]').addEventListener('click', () => {
    // Phase 2: Implement search functionality
    console.log('Поиск будет реализован в Phase 2');
    alert('Поиск по сайту будет доступен в ближайшее время');
});
```

### Step 9: Test & Validate (1 hour)

```bash
# HTML Validation
# Visit: https://validator.w3.org/
# Upload file and check for errors

# Schema.org Validation
# Visit: https://validator.schema.org/
# Paste JSON-LD and check

# OG Tags Validation
# Visit: https://www.opengraph.xyz/
# Enter URL and check

# Responsive Testing
# Test on: mobile (375px), tablet (768px), desktop (1280px+)
```

---

## Code Patterns Reference

### Card Component

```html
<div class="bg-[#0d181b] border-gold p-6 transition duration-300 animate-section">
    <h3 class="font-bold mb-2 text-white">Заголовок</h3>
    <p class="text-gray-400 text-sm">Описание</p>
</div>
```

### Grid Layout (2 columns)

```html
<div class="grid md:grid-cols-2 gap-8">
    <!-- Content -->
</div>
```

### Grid Layout (3 columns)

```html
<div class="grid md:grid-cols-3 gap-6">
    <!-- Content -->
</div>
```

### Section with Dark Background

```html
<section class="py-24 border-t border-white/5 bg-[#0d181b]">
    <div class="max-w-7xl mx-auto px-6">
        <!-- Content -->
    </div>
</section>
```

### Section with Standard Background

```html
<section class="py-24 border-t border-white/5">
    <div class="max-w-7xl mx-auto px-6">
        <!-- Content -->
    </div>
</section>
```

### Placeholder Pattern

```html
<!-- Text placeholder -->
<p class="text-gray-500 italic">[ЗАГЛУШКА: описание]</p>

<!-- Image placeholder -->
<div class="bg-gray-700 border border-dashed border-gray-500 rounded-lg p-8 text-center">
    <p class="text-gray-400">[PLACEHOLDER: изображение]</p>
</div>
```

---

## Validation Checklist

- [ ] HTML5 valid (no errors in W3C validator)
- [ ] All links work (no 404s)
- [ ] Breadcrumb navigation works
- [ ] Header navigation links point to index.html
- [ ] Footer link to new page works
- [ ] Schema.org CollegeOrUniversity valid
- [ ] OG tags present and correct
- [ ] Responsive on mobile (375px)
- [ ] Responsive on tablet (768px)
- [ ] Responsive on desktop (1280px+)
- [ ] Search icon displays (click shows placeholder alert)
- [ ] Back to top button works
- [ ] Scroll progress bar works
- [ ] All animations trigger on scroll
- [ ] Color scheme matches index.html
- [ ] Typography consistent with index.html
- [ ] Footer link "Сведения об организации" points to new file

---

## File Structure After Implementation

```
/Users/artemsuazov/Documents/Products/fregat/
├── index.html                                      (main page)
├── svedeniya-ob-obrazovatelnoy-organizatsii.html   (NEW - about page)
├── styles.css                                      (shared styles)
├── tailwind.config.js                              (shared config)
└── work/
    └── about-organization-page/
        ├── user-spec.md                            (requirements)
        ├── code-research.md                        (technical analysis)
        └── implementation-plan.md                  (this file)
```

---

## Common Issues & Solutions

### Issue: Breadcrumb not styling correctly

**Solution:** Ensure `styles.css` is linked before closing `</head>`:

```html
<link rel="stylesheet" href="styles.css">
```

### Issue: Schema.org validation fails

**Solution:** Check JSON-LD syntax:
- All quotes must be double quotes
- No trailing commas
- Valid JSON structure

### Issue: OG tags not working

**Solution:**
- Check all meta tags are in `<head>`
- Ensure `og:image` URL is accessible
- Image should be 1200x630px minimum

### Issue: Header links broken

**Solution:** Add `index.html#` prefix to anchor links:

```html
<a href="index.html#advantages">Преимущества</a>
```

---

## Success Criteria

The implementation is successful when:

1. ✅ Page exists at root: `/svedeniya-ob-obrazovatelnoy-organizatsii.html`
2. ✅ Header matches index.html design with search icon
3. ✅ Breadcrumb navigation works and shows correct path
4. ✅ All sections present with placeholder content
5. ✅ Footer matches index.html with link to new page
6. ✅ Schema.org CollegeOrUniversity validates
7. ✅ OG tags present and validate
8. ✅ Responsive on all device sizes
9. ✅ All interactive elements work (buttons, links, scroll)
10. ✅ Design consistent with index.html

---

## Next Steps After Implementation

1. **Update index.html footer** (if not already done):
   - Ensure link "Сведения об образовательной организации" points to new file

2. **Commit changes**:
   ```bash
   git add svedeniya-ob-obrazovatelnoy-organizatsii.html
   git commit -m "feat: add about organization page with FZ-273 compliance"
   ```

3. **Deploy to staging** (if available)

4. **User acceptance testing** with stakeholders

5. **Replace placeholders** when real data becomes available

---

**Prepared by:** Code Research Agent
**Date:** 2026-03-20
**Status:** Ready for implementation
