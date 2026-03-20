# Анализ кодовой базы проекта "Фрегат"
## Для создания страницы "Сведения об образовательной организации"

**Дата анализа:** 2026-03-20
**Проект:** Школа тендерного обучения «Фрегат»
**Цель:** Изучить текущую структуру для создания новой страницы

---

## 1. Текущая структура файлов

### Основные файлы проекта
```
/Users/artemsuazov/Documents/Products/fregat/
├── index.html              # Главная страница (1137 строк)
├── styles.css              # Дизайн-система (364 строки)
├── tailwind.config.js      # Конфигурация Tailwind CSS
├── DESIGN-SYSTEM.md        # Документация дизайн-системы
├── readme.md               # Описание проекта
└── .archive/               # Архивные версии index.html
```

### Технический стек
- **HTML5** — семантическая разметка
- **Tailwind CSS** (CDN) — utility-first CSS фреймворк
- **Custom CSS** (`styles.css`) — дизайн-система Фрегат
- **Vanilla JavaScript** — интерактивность (без библиотек)
- **Google Fonts** — Inter, Playfair Display

---

## 2. Организация index.html

### 2.1. Структура `<head>`

**Мета-теги:**
```html
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="description" content="...">
<meta http-equiv="Content-Security-Policy" content="...">
```

**Подключение стилей:**
1. Tailwind CSS через CDN
2. Inline Tailwind config (цвета, шрифты)
3. Google Fonts (Inter, Playfair Display)
4. Custom styles.css
5. Schema.org микроразметка (JSON-LD)

**Важный паттерн:**
- CSP (Content Security Policy) настроен для работы с CDN
- Schema.org описывает курс как образовательную программу

### 2.2. Глобальные элементы (перед `<main>`)

```html
<!-- Прогресс бар прокрутки -->
<div id="scroll-progress"></div>

<!-- Кнопка "Наверх" -->
<div id="back-to-top">...</div>

<!-- Вертикальная надпись (брендинг) -->
<div class="vertical-brand hidden lg:block">
    School Fregat • Tender Training
</div>

<!-- Геометрический фон -->
<div class="global-geo">...</div>
```

**Паттерн:** Все глобальные UI элементы имеют `fixed` позиционирование и high z-index

### 2.3. Header (Навигация)

```html
<header class="fixed w-full top-0 z-50 backdrop-blur-md border-b border-white/10">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <!-- Логотип + название -->
        <div class="flex items-center gap-3">
            <img src="..." class="h-12 w-auto logo-clean">
            <span class="text-2xl font-light tracking-widest text-gold-gradient">
                ФРЕГАТ
            </span>
        </div>

        <!-- Навигация -->
        <nav class="hidden md:flex gap-10">
            <a href="#advantages">Преимущества</a>
            <a href="#program">Программа</a>
            <a href="#price">Стоимость</a>
            <a href="#faq">FAQ</a>
        </nav>

        <!-- CTA кнопка -->
        <a href="#cta-form" class="btn-gold">Записаться</a>
    </div>
</header>
```

**Ключевые особенности:**
- Fixed позиционирование
- Backdrop blur эффект
- Responsive: мобильная версия скрывает nav (требует доработки)
- Максимальная ширина контейнера: `max-w-7xl` (1280px)

### 2.4. Основные секции

| Секция | ID | Класс | Описание |
|--------|-----|-------|----------|
| Hero | - | `hero-with-expert` | Две колонки: фото директора + контент |
| Преимущества | `#advantages` | `section` | Grid 4 колонки с иконками |
| Аудитория | - | `section` | Grid 3 колонки (новички, предприниматели, руководители) |
| Зарплаты | `#salary` | `section` | Progress bars с анимацией |
| Программа | `#program` | `section` | 5 модулей с уроками |
| FAQ | `#faq` | `section` | Accordion (12 вопросов) |
| Тарифы | `#price` | `section` | 4 карточки с ценами |
| CTA форма | `#cta-form` | `section` | Форма захвата (пока заглушка) |

### 2.5. Footer

```html
<footer class="py-12 border-t border-white/10 bg-[#0a1214]">
    <div class="max-w-7xl mx-auto px-6">
        <div class="grid md:grid-cols-3 gap-8">
            <!-- Логотип + описание -->
            <!-- Реквизиты компании -->
            <!-- Документы (ссылки) -->
        </div>
        <!-- Копирайт + лицензия -->
    </div>
</footer>
```

**Важно:** В футере уже есть ссылка на "Сведения об образовательной организации"

### 2.6. JavaScript (inline)

```javascript
// 1. Scroll Animation (Intersection Observer)
const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
        if (entry.isIntersecting) {
            entry.target.classList.add('visible');
        }
    });
});

// 2. Progress Bar & Back to Top
window.addEventListener('scroll', () => {
    // Обновление ширины прогресс-бара
    // Показ/скрытие кнопки "Наверх"
});

// 3. FAQ Accordion
document.querySelectorAll('.faq-question').forEach(item => {
    item.addEventListener('click', (event) => {
        // Toggle open/close
    });
});
```

---

## 3. Дизайн-система (styles.css)

### 3.1. CSS переменные

**Цвета:**
```css
:root {
    /* Золотая палитра */
    --color-gold: #D4AF37;
    --color-gold-light: #FBE5A8;
    --color-gold-dark: #B8860B;

    /* Фоны */
    --color-bg: #142125;
    --color-bg-card: #0d181b;
    --color-bg-dark: #0a1214;

    /* Текст */
    --color-text-primary: #FFFFFF;
    --color-text-secondary: #E0E0E0;
    --color-text-muted: #9CA3AF;

    /* Glow эффекты */
    --glow-sm: 0 0 15px rgba(212, 175, 55, 0.15);
    --glow-md: 0 0 25px rgba(212, 175, 55, 0.15);
    --glow-lg: 0 0 35px rgba(212, 175, 55, 0.5);
}
```

**Отступы:**
```css
--spacing-xs: 0.5rem;    /* 8px */
--spacing-sm: 1rem;      /* 16px */
--spacing-md: 1.5rem;    /* 24px */
--spacing-lg: 2rem;      /* 32px */
--spacing-xl: 3rem;      /* 48px */
--spacing-2xl: 4rem;     /* 64px */
--spacing-3xl: 6rem;     /* 96px */
```

**Размеры шрифтов:**
```css
--text-xs: 0.75rem;      /* 12px */
--text-sm: 0.875rem;     /* 14px */
--text-base: 1rem;       /* 16px */
--text-lg: 1.125rem;     /* 18px */
--text-xl: 1.25rem;      /* 20px */
--text-2xl: 1.5rem;      /* 24px */
--text-3xl: 1.875rem;    /* 30px */
--text-4xl: 2.25rem;     /* 36px */
--text-5xl: 3rem;        /* 48px */
--text-6xl: 3.75rem;     /* 60px */
--text-7xl: 4.5rem;      /* 72px */
```

### 3.2. Готовые компоненты

#### Кнопки
```css
.btn {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    font-weight: 600;
    transition: all var(--duration-base) ease;
    cursor: pointer;
    border: none;
    border-radius: var(--radius-lg);
}

.btn-gold {
    background: linear-gradient(135deg, var(--color-gold) 0%, var(--color-gold-dark) 100%);
    color: #000;
}

.btn-gold:hover {
    box-shadow: var(--glow-lg);
    transform: translateY(-2px);
}

.btn-sm, .btn-md, .btn-lg /* Размеры */
```

#### Карточки
```css
.card {
    background-color: var(--color-bg-card);
    border: 1px solid rgba(212, 175, 55, 0.3);
    border-radius: var(--radius-xl);
    padding: var(--spacing-lg);
    transition: all var(--duration-base) ease;
}

.card:hover {
    border-color: rgba(212, 175, 55, 0.8);
    box-shadow: var(--glow-md);
    transform: translateY(-5px);
}
```

#### Хлебные крошки
```css
.breadcrumb {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    padding: var(--spacing-sm) 0;
    font-size: var(--text-sm);
}
```

### 3.3. Анимации

**Появление при скролле:**
```css
.animate-section {
    opacity: 0;
    transform: translateY(40px);
    transition: opacity var(--duration-slower) ease-out,
                transform var(--duration-slower) ease-out;
}

.animate-section.visible {
    opacity: 1;
    transform: translateY(0);
}
```

**Progress bars:**
```css
.progress-bar {
    width: 0;
    transition: width 1.5s ease-in-out;
}

.visible .progress-bar {
    width: var(--target-width);
}
```

---

## 4. Tailwind конфигурация

### 4.1. Кастомные цвета

```javascript
colors: {
    gold: {
        DEFAULT: '#D4AF37',
        light: '#FBE5A8',
        dark: '#B8860B',
    },
    dark: {
        bg: '#142125',
        card: '#0d181b',
        footer: '#0a1214',
    }
}
```

### 4.2. Кастомные шрифты

```javascript
fontFamily: {
    sans: ['Inter', '-apple-system', 'BlinkMacSystemFont', 'Segoe UI', 'Roboto', 'sans-serif'],
    serif: ['Playfair Display', 'Georgia', 'serif'],
}
```

### 4.3. Кастомные анимации

```javascript
animation: {
    'drift': 'drift 15s ease-in-out infinite',
    'fade-in': 'fadeIn 0.8s ease-out',
}
```

---

## 5. Переиспользуемые паттерны

### 5.1. Сетка контейнера

```html
<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
    <!-- Контент -->
</div>
```

### 5.2. Секции

```html
<section class="py-24 border-t border-white/5">  <!-- Стандартная -->
<section class="py-24 border-t border-white/5 bg-[#0d181b]">  <!-- С тёмным фоном -->
<section class="py-16 border-t border-white/5">  <!-- Уменьшенная -->
```

### 5.3. Заголовки секций

```html
<div class="text-center mb-16 animate-section">
    <h2 class="text-3xl md:text-4xl font-bold mb-4 text-white">
        Заголовок <span class="text-gold-gradient">с акцентом</span>
    </h2>
    <p class="text-gray-400 max-w-2xl mx-auto">
        Описание секции
    </p>
</div>
```

### 5.4. Grid layouts

```html
<!-- 2 колонки -->
<div class="grid md:grid-cols-2 gap-8">...</div>

<!-- 3 колонки -->
<div class="grid md:grid-cols-3 gap-6">...</div>

<!-- 4 колонки -->
<div class="grid md:grid-cols-2 lg:grid-cols-4 gap-6">...</div>

<!-- Адаптивный (2 на десктопе, 1 на мобильном) -->
<div class="grid lg:grid-cols-2 gap-12 items-center">...</div>
```

### 5.5. Иконки в круге

```html
<div class="w-16 h-16 mx-auto mb-4 border border-gold rounded-full flex items-center justify-center">
    <svg class="w-8 h-8 text-gold" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <!-- SVG path -->
    </svg>
</div>
```

### 5.6. Карточка с контентом

```html
<div class="bg-[#0d181b] border-gold p-6 transition duration-300 animate-section">
    <h3 class="font-bold mb-2 text-white">Заголовок</h3>
    <p class="text-gray-400 text-sm">Описание</p>
</div>
```

### 5.7. Badge (лейбл)

```html
<div class="absolute -top-3 left-1/2 -translate-x-1/2 bg-gold text-black px-3 py-1 text-xs font-bold uppercase rounded-full">
    Популярно
</div>
```

---

## 6. Микроразметка Schema.org

**Текущая реализация:**
```html
<script type="application/ld+json">
{
    "@context": "https://schema.org",
    "@type": "Course",
    "name": "Тендеры с нуля...",
    "provider": {
        "@type": "Organization",
        "name": "Школа «Фрегат»",
        "license": "Л035‑01217‑26/03829175"
    },
    ...
}
</script>
```

**Для новой страницы рекомендуется добавить:**
- `EducationalOrganization` schema
- `CollegeOrUniversity` schema
- Филиалы, контакты, программы

---

## 7. Рекомендации по созданию новой страницы

### 7.1. Структура файла

**Создать файл:** `/Users/artemsuazov/Documents/Products/fregat/about.html`

**Базовый шаблон:**
```html
<!DOCTYPE html>
<html lang="ru">
<head>
    <!-- Мета-теги (адаптировать под страницу) -->
    <title>Сведения об образовательной организации | Школа «Фрегат»</title>
    <meta name="description" content="...">

    <!-- CSP -->
    <meta http-equiv="Content-Security-Policy" content="...">

    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        gold: {
                            DEFAULT: '#D4AF37',
                            light: '#FBE5A8',
                            dark: '#B8860B',
                        },
                        dark: {
                            bg: '#142125',
                            card: '#0d181b',
                            footer: '#0a1214',
                        }
                    },
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                        serif: ['Playfair Display', 'serif'],
                    }
                }
            }
        }
    </script>

    <!-- Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Playfair+Display:ital,wght@0,400;0,700;1,400&display=swap" rel="stylesheet">

    <!-- Styles -->
    <link rel="stylesheet" href="styles.css">

    <!-- Schema.org -->
    <script type="application/ld+json">
    {
        "@context": "https://schema.org",
        "@type": "EducationalOrganization",
        "name": "Школа «Фрегат»",
        ...
    }
    </script>
</head>
<body class="geo-pattern">
    <!-- Глобальные элементы (скопировать из index.html) -->

    <!-- Header (адаптировать навигацию) -->

    <!-- Хлебные крошки (новый компонент) -->

    <!-- Main content -->
    <main>
        <!-- Секции с информацией об организации -->
    </main>

    <!-- Footer (скопировать из index.html) -->

    <!-- Scripts (скопировать из index.html) -->
</body>
</html>
```

### 7.2. Адаптация Header

**Изменить навигацию:**
```html
<nav class="hidden md:flex gap-10 text-sm text-gray-300">
    <a href="index.html#advantages">Преимущества</a>
    <a href="index.html#program">Программа</a>
    <a href="index.html#price">Стоимость</a>
    <a href="index.html#faq">FAQ</a>
</nav>
```

**Добавить breadcrumb:**
```html
<div class="breadcrumb max-w-7xl mx-auto px-6">
    <a href="index.html" class="breadcrumb-item">Главная</a>
    <span class="breadcrumb-separator">→</span>
    <span class="breadcrumb-item active">Сведения об организации</span>
</div>
```

### 7.3. Контент для страницы

**Рекомендуемые секции:**

1. **Hero (упрощённый)**
   - Заголовок: "Сведения об образовательной организации"
   - Подзаголовок: "Лицензия № Л035‑01217‑26/03829175"

2. **Основная информация**
   - Полное наименование
   - Юридический адрес
   - Фактический адрес
   - Телефоны, email
   - Режим работы

3. **Документы**
   - Лицензия на образовательную деятельность
   - Устав
   - Свидетельство о государственной регистрации
   - Аккредитация

4. **Программы обучения**
   - Список программ
   - Уровни образования
   - Сроки обучения
   - Выдаваемые документы

5. **Материально-техническое обеспечение**
   - Площадки для обучения
   - Оборудование
   - Электронные ресурсы

6. **Педагогический состав**
   - Руководитель
   - Преподаватели
   - Квалификация

7. **Финансово-хозяйственная деятельность**
   - Бюджет
   - Платные образовательные услуги

### 7.4. Компоненты для переиспользования

**Из index.html:**
- Header (с адаптацией ссылок)
- Footer (без изменений)
- Кнопка "Наверх"
- Progress bar
- Стили из `styles.css`
- JavaScript для анимаций

**Новые компоненты:**
- Breadcrumb (уже есть в `styles.css`)
- Table (для расписания, документов)
- Accordion (для FAQ)
- Card (для документов, преподавателей)

### 7.5. Стилизация таблицы

**Добавить в styles.css:**
```css
.table {
    width: 100%;
    border-collapse: collapse;
    background-color: var(--color-bg-card);
    border: 1px solid rgba(212, 175, 55, 0.3);
    border-radius: var(--radius-xl);
    overflow: hidden;
}

.table th,
.table td {
    padding: var(--spacing-md);
    text-align: left;
    border-bottom: 1px solid rgba(212, 175, 55, 0.1);
}

.table th {
    background-color: rgba(212, 175, 55, 0.1);
    color: var(--color-gold);
    font-weight: 600;
}

.table tr:last-child td {
    border-bottom: none;
}

.table tbody tr:hover {
    background-color: rgba(212, 175, 55, 0.05);
}
```

### 7.6. Schema.org для страницы

```html
<script type="application/ld+json">
{
    "@context": "https://schema.org",
    "@type": "EducationalOrganization",
    "name": "Школа тендерного обучения «Фрегат»",
    "url": "https://fregat-school.ru",
    "logo": "https://z-cdn-media.chatglm.cn/files/13817077-3fd8-4076-ab8b-31702a8b0e59.png",
    "legalName": "ООО «ФРЕГАТ»",
    "taxId": "ИНН_КОМПАНИИ",
    "address": {
        "@type": "PostalAddress",
        "streetAddress": "ГОРОД, УЛИЦА, ДОМ",
        "addressLocality": "ГОРОД",
        "addressCountry": "RU"
    },
    "contactPoint": {
        "@type": "ContactPoint",
        "telephone": "+7-XXX-XXX-XX-XX",
        "contactType": "customer service"
    },
    "sameAs": [
        "https://vk.com/fregat",
        "https://telegram.me/fregat"
    ]
}
</script>
```

---

## 8. Чеклист для реализации

- [ ] Создать файл `about.html`
- [ ] Скопировать `<head>` из index.html
- [ ] Обновить title, description, Schema.org
- [ ] Скопировать глобальные элементы (progress bar, back-to-top, geo)
- [ ] Адаптировать Header (обновить ссылки nav)
- [ ] Добавить breadcrumb
- [ ] Создать секции с контентом
- [ ] Использовать компоненты из дизайн-системы
- [ ] Скопировать Footer
- [ ] Скопировать JavaScript
- [ ] Добавить стили для таблиц (если нужно)
- [ ] Проверить адаптивность
- [ ] Проверить валидность HTML
- [ ] Проверить Schema.org

---

## 9. Полезные ресурсы

- **Файл стилей:** `/Users/artemsuazov/Documents/Products/fregat/styles.css`
- **Tailwind config:** `/Users/artemsuazov/Documents/Products/fregat/tailwind.config.js`
- **Главная страница:** `/Users/artemsuazov/Documents/Products/fregat/index.html`
- **Дизайн-система:** `/Users/artemsuazov/Documents/Products/fregat/DESIGN-SYSTEM.md`

---

## 10. Технические требования для новой страницы

### 10.1. OG теги (Open Graph) - НОВОЕ

**Текущее состояние:** OG теги НЕ реализованы на index.html

**Что нужно добавить:**
```html
<meta property="og:type" content="website">
<meta property="og:locale" content="ru_RU">
<meta property="og:title" content="Сведения об образовательной организации | Школа «Фрегат»">
<meta property="og:description" content="Лицензия ДПО № Л035‑01217‑26/03829175. Полные сведения об образовательной организации, программах обучения, преподавателях и материально-технической базе.">
<meta property="og:url" content="https://fregat-school.ru/svedeniya-ob-obrazovatelnoy-organizatsii.html">
<meta property="og:image" content="https://z-cdn-media.chatglm.cn/files/13817077-3fd8-4076-ab8b-31702a8b0e59.png">
<meta property="og:site_name" content="Школа «Фрегат»">
<meta property="og:image:width" content="1200">
<meta property="og:image:height" content="630">
<meta property="og:image:alt" content="Логотип Школы «Фрегат»">

<!-- Twitter Card (дополнительно) -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="Сведения об образовательной организации | Школа «Фрегат»">
<meta name="twitter:description" content="Лицензия ДПО № Л035‑01217‑26/03829175. Полные сведения об образовательной организации.">
<meta name="twitter:image" content="https://z-cdn-media.chatglm.cn/files/13817077-3fd8-4076-ab8b-31702a8b0e59.png">
```

**Где добавить:** В секцию `<head>` после meta description

### 10.2. Schema.org CollegeOrUniversity - РАСШИРЕНО

**Текущая реализация на index.html:**
- `@type: "Course"` для описания курса
- `@type: "Organization"` для провайдера

**Новая реализация для about-page:**
```html
<script type="application/ld+json">
{
    "@context": "https://schema.org",
    "@type": "CollegeOrUniversity",
    "name": "Школа тендерного обучения «Фрегат»",
    "url": "https://fregat-school.ru",
    "logo": "https://z-cdn-media.chatglm.cn/files/13817077-3fd8-4076-ab8b-31702a8b0e59.png",
    "legalName": "ООО «ФРЕГАТ»",
    "taxId": "ИНН_КОМПАНИИ",
    "vatId": "КПП_КОМПАНИИ",
    "address": {
        "@type": "PostalAddress",
        "streetAddress": "УЛИЦА, ДОМ",
        "addressLocality": "ГОРОД",
        "addressRegion": "ОБЛАСТЬ",
        "postalCode": "ИНДЕКС",
        "addressCountry": "RU"
    },
    "contactPoint": {
        "@type": "ContactPoint",
        "telephone": "+7-XXX-XXX-XX-XX",
        "email": "info@fregat-school.ru",
        "contactType": "customer service",
        "areaServed": "RU",
        "availableLanguage": ["Russian"]
    },
    "sameAs": [
        "https://vk.com/fregat",
        "https://telegram.me/fregat"
    ],
    "hasCredential": {
        "@type": "EducationalOccupationalCredential",
        "credentialCategory": "Professional License",
        "name": "Лицензия на право ведения образовательной деятельности",
        "licenseNumber": "Л035‑01217‑26/03829175"
    },
    "offers": [
        {
            "@type": "Course",
            "name": "Тендеры с нуля: Профессия Тендерный специалист",
            "description": "Курс обучения тендерному делу с нуля",
            "educationalLevel": "Professional Training",
            "provider": {
                "@type": "Organization",
                "name": "Школа «Фрегат»"
            }
        }
    ]
}
</script>
```

### 10.3. Поисковая иконка в Header - НОВОЕ

**Текущее состояние:** Иконка поиска отсутствует в header на index.html

**Что нужно добавить в header:**
```html
<!-- Перед CTA кнопкой -->
<div class="flex items-center gap-4">
    <!-- Иконка поиска (заглушка) -->
    <button class="p-2 text-gray-300 hover:text-gold transition" aria-label="Поиск">
        <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path>
        </svg>
    </button>
    <!-- CTA кнопка -->
    <a href="#cta-form" class="btn-gold px-6 py-3 rounded text-sm tracking-wide">Записаться</a>
</div>
```

**JavaScript (заглушка):**
```javascript
// Поиск (заглушка - клик без действия)
document.querySelector('[aria-label="Поиск"]').addEventListener('click', () => {
    // Заглушка - в будущем здесь будет поиск
    console.log('Поиск будет реализован в Phase 2');
});
```

### 10.4. Breadcrumb компонент - РАСШИРЕНО

**Текущее состояние:** Стили для breadcrumb существуют в styles.css, но компонент не реализован

**Реализация breadcrumb:**
```html
<!-- После header, перед main content -->
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

---

## 11. Шаринг компонентов между страницами

### 11.1. Компоненты для копирования

**Полностью копируются:**
1. `<head>` секция (с адаптацией meta тегов)
2. Глобальные UI элементы:
   - `<div id="scroll-progress"></div>`
   - `<div id="back-to-top">...</div>`
   - `<div class="vertical-brand">...</div>`
   - `<div class="global-geo">...</div>`
3. Footer (без изменений)
4. JavaScript скрипты

**Адаптируются:**
1. Header:
   - Обновить ссылки навигации (добавить `index.html#`)
   - Добавить иконку поиска
   - Сохранить структуру и стили

**Новые компоненты:**
1. Breadcrumb (использовать существующие стили)
2. Секции с контентом организации

### 11.2. Стратегия копирования компонентов

**Вариант 1: Прямое копирование (Phase 1)**
- Скопировать header/footer из index.html
- Быстрая реализация
- Дублирование кода
- Рекомендуется для текущей задачи

**Вариант 2: Компоненты через JavaScript (Phase 2)**
- Использовать JavaScript для инъекции компонентов
- Единая точка управления
- Сложнее в реализации
- План для WordPress миграции

**Вариант 3: SSI или PHP includes (Phase 2)**
- Server-side includes
- Требует серверной части
- Будет реализовано на WordPress

**Рекомендация:** Использовать Вариант 1 для текущей задачи

### 11.3. Путь к файлу

**Согласно user-spec:**
- Имя файла: `svedeniya-ob-obrazovatelnoy-organizatsii.html`
- Расположение: `/Users/artemsuazov/Documents/Products/fregat/svedeniya-ob-obrazovatelnoy-organizatsii.html`

**Примечание:** Файл должен находиться в корне проекта рядом с `index.html`

---

## 12. Контент-стратегия (с заглушками)

### 12.1. Структура контента

**H1 Заголовок:**
```
Сведения об образовательной организации
```

**Секции с placeholder контентом:**

1. **Об организации**
   - Полное наименование: ООО «Фрегат»
   - История создания: [PLACEHOLDER]
   - Миссия: [PLACEHOLDER]

2. **Лицензия и документы**
   - Номер лицензии: Л035‑01217‑26/03829175
   - Дата выдачи: 25.11.2025
   - Скан лицензии: [PLACEHOLDER IMAGE]

3. **Контактная информация**
   - Юридический адрес: [PLACEHOLDER]
   - Фактический адрес: [PLACEHOLDER]
   - Телефон: [PLACEHOLDER]
   - Email: [PLACEHOLDER]

4. **Реквизиты**
   - ИНН: [PLACEHOLDER]
   - КПП: [PLACEHOLDER]
   - ОГРН: [PLACEHOLDER]
   - Р/с: [PLACEHOLDER]
   - Банк: [PLACEHOLDER]
   - БИК: [PLACEHOLDER]

5. **Образовательные программы**
   - «Тендеры с нуля»: [PLACEHOLDER]
   - Уровень образования: ДПО
   - Форма обучения: онлайн

6. **Преподавательский состав**
   - 2-3 placeholder-профиля преподавателей

7. **Материально-техническая база**
   - Описание платформы: [PLACEHOLDER]
   - Оборудование: [PLACEHOLDER]

### 12.2. Placeholder паттерны

**Для текстовых placeholder:**
```html
<p class="text-gray-500 italic">[ЗАГЛУШКА: описание]</p>
```

**Для изображений:**
```html
<div class="bg-gray-700 border border-dashed border-gray-500 rounded-lg p-8 text-center">
    <p class="text-gray-400">[PLACEHOLDER: изображение]</p>
</div>
```

**Для данных:**
```html
<span class="text-gray-400">[PLACEHOLDER]</span>
```

---

## 13. Валидация и тестирование

### 13.1. HTML валидация

**Инструменты:**
- W3C Markup Validation Service: https://validator.w3.org/
- HTML5 Validator

**Проверки:**
- [ ] Валидный HTML5
- [ ] Семантические теги (`<header>`, `<main>`, `<section>`, `<footer>`)
- [ ] ARIA атрибуты для accessibility
- [ ] Alt тексты для изображений

### 13.2. Адаптивность

**Брейкпоинты Tailwind:**
- `sm`: 640px
- `md`: 768px
- `lg`: 1024px
- `xl`: 1280px

**Проверки:**
- [ ] Mobile (< 640px)
- [ ] Tablet (640px - 1024px)
- [ ] Desktop (> 1024px)

### 13.3. Schema.org валидация

**Инструменты:**
- Google Rich Results Test: https://search.google.com/test/rich-results
- Schema.org Validator: https://validator.schema.org/

**Проверки:**
- [ ] Валидный JSON-LD
- [ ] Все обязательные поля заполнены
- [ ] Тип `CollegeOrUniversity` корректен

### 13.4. OG теги валидация

**Инструменты:**
- Open Graph Debugger: https://www.opengraph.xyz/
- Facebook Sharing Debugger: https://developers.facebook.com/tools/debug/

**Проверки:**
- [ ] Все OG теги присутствуют
- [ ] Изображение корректного размера (1200x630)
- [ ] Заголовок и описание не превышают лимиты

---

## 14. Технические ограничения и риски

### 14.1. Ограничения Phase 1

**Что НЕ реализуется:**
1. Динамический контент (всё статично)
2. Админка для управления контентом
3. Поиск по сайту (только заглушка иконки)
4. Мобильная навигация (гамбургер-меню)
5. Формы с отправкой данных

**Что реализуется с заглушками:**
1. Все текстовые данные (PLACEHOLDER)
2. Изображения (PLACEHOLDER)
3. Документы (PLACEHOLDER)

### 14.2. Риски миграции

**WordPress миграция (Phase 2):**
- Header/Footer станут темой WordPress
- Контент будет управляться через CMS
- Schema.org будет генерироваться динамически
- OG теги будут управляться SEO плагином

**Совет:** Структура HTML должна быть подготовлена для легкой миграции на WordPress

---

## 15. Чеклист реализации

### 15.1. Подготовка

- [ ] Создать файл `svedeniya-ob-obrazovatelnoy-organizatsii.html` в корне проекта
- [ ] Скопировать `<head>` из index.html
- [ ] Обновить title: "Сведения об образовательной организации | Школа «Фрегат»"
- [ ] Обновить meta description
- [ ] Добавить OG теги (включая Twitter Card)
- [ ] Обновить Schema.org на `CollegeOrUniversity`

### 15.2. Компоненты

- [ ] Скопировать глобальные UI элементы (progress, back-to-top, geo, vertical-brand)
- [ ] Скопировать Header из index.html
- [ ] Адаптировать навигацию (добавить `index.html#` к ссылкам)
- [ ] Добавить иконку поиска в Header
- [ ] Добавить JavaScript обработчик для поиска (заглушка)
- [ ] Реализовать Breadcrumb компонент

### 15.3. Контент

- [ ] Создать секцию "Об организации" с placeholder
- [ ] Создать секцию "Лицензия и документы" с placeholder
- [ ] Создать секцию "Контакты" с placeholder
- [ ] Создать секцию "Реквизиты" с placeholder
- [ ] Создать секцию "Образовательные программы" с placeholder
- [ ] Создать секцию "Преподаватели" с placeholder
- [ ] Создать секцию "Материально-техническая база" с placeholder

### 15.4. Footer

- [ ] Скопировать Footer из index.html
- [ ] Убедиться, что ссылка на "Сведения об организации" ведет на новый файл

### 15.5. JavaScript

- [ ] Скопировать scroll animation код
- [ ] Скопировать progress bar код
- [ ] Скопировать back-to-top код
- [ ] Добавить обработчик для поиска (заглушка)

### 15.6. Тестирование

- [ ] Проверить HTML валидность
- [ ] Проверить адаптивность (mobile, tablet, desktop)
- [ ] Проверить Schema.org валидность
- [ ] Проверить OG теги
- [ ] Проверить все ссылки
- [ ] Проверить breadcrumb навигацию

---

## 16. Ключевые выводы

### 16.1. Сильные стороны

1. **Единая дизайн-система:** Все цвета, отступы, шрифты стандартизированы в `styles.css`
2. **Tailwind + Custom CSS:** Гибкая система для быстрой вёрстки
3. **Компонентный подход:** Карточки, кнопки, секции легко переиспользуются
4. **Анимации:** Готовый Intersection Observer для появления контента
5. **Адаптивность:** Mobile-first подход с Tailwind брейкпоинтами
6. **Schema.org:** Опыт внедрения микроразметки на index.html
7. **Готовые стили:** Breadcrumb стили уже существуют в `styles.css`

### 16.2. Новые элементы для реализации

1. **OG теги:** Не реализованы на index.html, нужно добавить с нуля
2. **Иконка поиска:** Отсутствует в header, нужно добавить
3. **Breadcrumb:** Стили есть, компонент не реализован
4. **CollegeOrUniversity schema:** Новый тип Schema.org для организации

### 16.3. Оценка трудозатрат

- **Копирование компонентов:** 1 час
- **Адаптация header и добавление поиска:** 30 минут
- **Реализация breadcrumb:** 15 минут
- **Создание секций с placeholder:** 2-3 часа
- **Schema.org и OG теги:** 1 час
- **Тестирование и валидация:** 1 час
- **Итого:** 5-6.5 часов (соответствует оценке в user-spec)

### 16.4. Следующие шаги

1. Создать файл `svedeniya-ob-obrazovatelnoy-organizatsii.html`
2. Скопировать базовую структуру из `index.html`
3. Адаптировать компоненты согласно чеклисту
4. Реализовать placeholder контент
5. Провести валидацию и тестирование
6. Обновить футер на `index.html` для ссылки на новую страницу

**Новая страница будет:**
- Консистентной с главным лендингом
- Быстро реализуемой с помощью готовых компонентов
- SEO-оптимизированной с помощью Schema.org и OG тегов
- Адаптивной для всех устройств
- Готовой к миграции на WordPress в Phase 2
