# Дизайн-система Фрегат

## Структура файлов

```
fregat/
├── index.html          # Главная страница
├── styles.css          # Основные стили дизайн-системы
├── tailwind.config.js  # Конфигурация Tailwind CSS
└── DESIGN-SYSTEM.md    # Этот файл
```

## Цветовая палитра

### Основные цвета
```css
--color-gold:       #D4AF37  /* Золотой - основной акцент */
--color-gold-light: #FBE5A8  /* Светло-золотой */
--color-gold-dark:  #B8860B  /* Тёмно-золотой */
```

### Фоновые цвета
```css
--color-bg:         #142125  /* Основной фон */
--color-bg-card:    #0d181b  /* Фон карточек */
--color-bg-dark:    #0a1214  /* Тёмный фон (footer) */
```

### Текстовые цвета
```css
--color-text-primary:  #FFFFFF  /* Заголовки */
--color-text-secondary: #E0E0E0  /* Основной текст */
--color-text-muted:    #9CA3AF  /* Второстепенный текст */
```

### Tailwind классы для цветов
```html
<div class="bg-gold">           <!-- #D4AF37 -->
<div class="bg-gold-light">     <!-- #FBE5A8 -->
<div class="bg-dark-bg">        <!-- #142125 -->
<div class="bg-dark-card">      <!-- #0d181b -->
<div class="bg-dark-footer">    <!-- #0a1214 -->
```

## Типографика

### Размеры шрифтов (CSS переменные)
```css
--text-xs:   0.75rem   /* 12px */
--text-sm:   0.875rem  /* 14px */
--text-base: 1rem      /* 16px */
--text-lg:   1.125rem  /* 18px */
--text-xl:   1.25rem   /* 20px */
--text-2xl:  1.5rem    /* 24px */
--text-3xl:  1.875rem  /* 30px */
--text-4xl:  2.25rem   /* 36px */
--text-5xl:  3rem      /* 48px */
--text-6xl:  3.75rem   /* 60px */
--text-7xl:  4.5rem    /* 72px */
```

### Иерархия заголовков
```html
<h1> - text-4xl → text-6xl → text-7xl (responsive)
<h2> - text-3xl → text-4xl (responsive)
<h3> - text-2xl
<h4> - text-xl
```

### Золотой градиент для текста
```html
<span class="text-gold-gradient">Текст</span>
```

## Отступы (Spacing)

### CSS переменные
```css
--spacing-xs:  0.5rem   /* 8px */
--spacing-sm:  1rem     /* 16px */
--spacing-md:  1.5rem   /* 24px */
--spacing-lg:  2rem     /* 32px */
--spacing-xl:  3rem     /* 48px */
--spacing-2xl: 4rem     /* 64px */
--spacing-3xl: 6rem     /* 96px */
```

### Классы для секций
```html
<section class="section">      <!-- padding: 96px 0 -->
<section class="section-sm">   <!-- padding: 64px 0 -->
<section class="section-xs">   <!-- padding: 48px 0 -->
```

## Компоненты

### Кнопки

#### Базовые классы
```html
<button class="btn btn-gold">Кнопка</button>
<button class="btn btn-gold btn-sm">Маленькая</button>
<button class="btn btn-gold btn-md">Средняя</button>
<button class="btn btn-gold btn-lg">Большая</button>
```

#### Tailwind аналог
```html
<button class="bg-gradient-to-r from-gold to-gold-dark text-black font-semibold py-4 px-8 rounded-lg hover:shadow-gold-lg transition-all">
    Кнопка
</button>
```

### Карточки

#### Базовый класс
```html
<div class="card">
    <h3>Заголовок</h3>
    <p>Содержимое</p>
</div>
```

#### Выделенная карточка
```html
<div class="card card-featured">
    <span class="absolute top-0 right-0 bg-gold text-black px-3 py-1 text-xs font-bold uppercase">
        Популярно
    </span>
    ...
</div>
```

#### Tailwind аналог
```html
<div class="bg-dark-card border border-gold/30 rounded-card p-8 hover:border-gold/80 hover:shadow-gold-md hover:-translate-y-1 transition-all">
    ...
</div>
```

## Эффекты

### Glow (свечение)
```css
--glow-sm: 0 0 15px rgba(212, 175, 55, 0.15)
--glow-md: 0 0 25px rgba(212, 175, 55, 0.15)
--glow-lg: 0 0 35px rgba(212, 175, 55, 0.5)
```

### Tailwind классы
```html
<div class="shadow-gold-sm">
<div class="shadow-gold-md">
<div class="shadow-gold-lg">
```

## Анимации

### Появление при скролле
```html
<div class="animate-section">Контент</div>
<!-- Добавляется JS: .visible -->
```

### Tailwind аналог
```html
<div class="animate-fade-in">Контент</div>
```

### Кастомные анимации
```css
animation: drift 15s ease-in-out infinite  /* Геометрия */
```

## Радиусы скругления

```css
--radius-sm:   0.25rem  /* 4px */
--radius-md:   0.5rem   /* 8px */
--radius-lg:   0.75rem  /* 12px */
--radius-xl:   1rem     /* 16px */
--radius-full: 9999px
```

## Правила использования

### ✅ DO (правильно)
```html
<!-- Используй CSS классы из дизайн-системы -->
<div class="card">...</div>
<button class="btn btn-gold btn-md">...</button>
<section class="section">...</section>

<!-- Используй Tailwind utility классы -->
<div class="bg-dark-card text-gold p-8">...</div>
```

### ❌ DON'T (неправильно)
```html
<!-- Не хардкоди цвета -->
<div style="background: #142125; color: #D4AF37;">...</div>

<!-- Не создавай новые цвета inline -->
<div style="border: 1px solid rgba(212, 175, 55, 0.3);">...</div>

<!-- Не используй случайные отступы -->
<div class="py-17 px-9">...</div>
```

## Адаптивность

### Мобильная версия
```html
<!-- Скрывать на мобильных -->
<div class="hidden md:block">...</div>

<!-- Показывать только на мобильных -->
<div class="block md:hidden">...</div>

<!-- Отзывчивый текст -->
<h1 class="text-4xl md:text-6xl lg:text-7xl">...</h1>
```

## Доступность

### Контраст
- Текст на тёмном фоне: минимум 4.5:1
- Используй `color: var(--color-text-secondary)` для основного текста

### Фокус
```css
input:focus {
    border-color: var(--color-gold);
    box-shadow: 0 0 15px rgba(212, 175, 55, 0.2);
}
```

## Миграция на WordPress

При миграции:
1. Скопировать `styles.css` в тему WordPress
2. Настроить `tailwind.config.js` в сборке
3. Заменить хардкод цвета на CSS переменные
4. Использовать `get_template_directory_uri()` для логотипа

## Чеклист для новых компонентов

- [ ] Используются CSS переменные для цветов
- [ ] Отступы из spacing scale
- [ ] Шрифты из типографики
- [ ] Hover эффекты с glow
- [ ] Адаптивность на мобильных
- [ ] Достаточный контраст
- [ ] Анимации не слишком медленные
