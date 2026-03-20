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

## 10. Ключевые выводы

1. **Единая дизайн-система:** Все цвета, отступы, шрифты стандартизированы
2. **Tailwind + Custom CSS:** Гибкая система для быстрой вёрстки
3. **Компонентный подход:** Карточки, кнопки, секции переиспользуются
4. **Анимации:** Готовый Intersection Observer для появления контента
5. **Адаптивность:** Mobile-first подход с Tailwind брейкпоинтами
6. **Schema.org:** Внедрена микроразметка для SEO

**Новая страница будет:**
- Консистентной с главным лендингом
- Быстро реализуемой с помощью готовых компонентов
- SEO-оптимизированной с помощью Schema.org
- Адаптивной для всех устройств
