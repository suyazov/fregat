---
title: "Tech Spec: Сведения об образовательной организации"
created: "2026-03-20"
status: approved
size: M
branch: main
feature: about-organization-page
---

## Tech Spec: Сведения об образовательной организации

## Architecture Overview

### Тип системы
Статический HTML-сайт в рамках Фазы 1. Новая страница использует существующую дизайн-систему и компоненты.

### Компоненты
1. **svedeniya-ob-obrazovatelnoy-organizatsii.html** — новая страница
2. **index.html** — источник для копирования header/footer
3. **styles.css** — общие стили (без изменений)
4. **tailwind.config.js** — конфигурация Tailwind (без изменений)

### Поток данных
Статический контент → HTML → Browser (no backend, no database)

## Decisions

### D1: Организация многострочности
**Решение:** Копировать header/footer в каждый HTML-файл (Вариант А)

**Обоснование:**
- Фаза 1 — статический сайт без сборщика
- Быстрая реализация
- На Фазе 2 (WordPress) компоненты будут автоматическими

**Альтернативы:** JavaScript includes, SSG (Eleventy) — отклонены из-за сложности для статического сайта

### D2: Иконка поиска
**Решение:** SVG иконка в header без функционала (Вариант А)

**Обоснование:**
- Placeholder для будущего функционала
- Готовит UI к поиску
- Минимальные затраты

### D3: Размещение ссылки в footer
**Решение:** Первый столбец (разделы сайта)

**Обоснование:**
- Логическая группировка с другими разделами
- Удобство навигации для пользователей

### D4: Schema.org тип
**Решение:** `CollegeOrUniversity` для этой страницы

**Обоснование:**
- Эта страница описывает организацию, а не курс
- `Course` тип остается на index.html
- SEO: правильная семантика для разных страниц

## Shared Resources
**None** — статический сайт без shared state, pools, или connections

## Implementation Tasks

### Wave 1: Foundation

#### Task 1.1: Создать HTML-каркас новой страницы
**Description:** Создать файл `svedeniya-ob-obrazovatelnoy-organizatsii.html` с базовой структурой, адаптированным `<head>` и OG тегами.

**Skill:** `do-task`
**Reviewers:** `code-reviewer`
**Verify-smoke:** `grep -q "<title>" svedeniya-ob-obrazovatelnoy-organizatsii.html && echo "OK"`
**Files to modify:** `svedeniya-ob-obrazovatelnoy-organizatsii.html` (create)
**Files to read:** `index.html` (lines 1-50 for head pattern)

---

#### Task 1.2: Скопировать и адаптировать header с иконкой поиска
**Description:** Скопировать header из index.html, добавить SVG иконку поиска в навигацию (без функционала).

**Skill:** `do-task`
**Reviewers:** `code-reviewer`
**Files to modify:** `svedeniya-ob-obrazovatelnoy-organizatsii.html`
**Files to read:** `index.html` (lines 100-200 for header)

---

#### Task 1.3: Реализовать хлебные крошки
**Description:** Добавить breadcrumbs component (Главная → Сведения об образовательной организации) используя стили из styles.css.

**Skill:** `do-task`
**Reviewers:** `code-reviewer`
**Files to modify:** `svedeniya-ob-obrazovatelnoy-organizatsii.html`
**Files to read:** `styles.css` (lines 338-363 for breadcrumb styles)

---

### Wave 2: Content Sections

#### Task 2.1: Создать секцию «Об организации»
**Description:** Добавить секцию с названием, историей, миссией (placeholder content).

**Skill:** `do-task`
**Reviewers:** `code-reviewer`
**Files to modify:** `svedeniya-ob-obrazovatelnoy-organizatsii.html`
**Files to read:** `index.html` (for section pattern)

---

#### Task 2.2: Создать секцию «Лицензия и документы»
**Description:** Добавить секцию с номером лицензии Л035‑01217‑26/03829175, датой, placeholder для скана.

**Skill:** `do-task`
**Reviewers:** `code-reviewer`
**Files to modify:** `svedeniya-ob-obrazovatelnoy-organizatsii.html`

---

#### Task 2.3: Создать секцию «Образовательные программы»
**Description:** Добавить секцию с описанием курса «Тендеры с нуля» (placeholder).

**Skill:** `do-task`
**Reviewers:** `code-reviewer`
**Files to modify:** `svedeniya-ob-obrazovatelnoy-organizatsii.html`

---

#### Task 2.4: Создать секцию «Преподавательский состав»
**Description:** Добавить 2-3 placeholder-профиля преподавателей.

**Skill:** `do-task`
**Reviewers:** `code-reviewer`
**Files to modify:** `svedeniya-ob-obrazovatelnoy-organizatsii.html`

---

#### Task 2.5: Создать секцию «Материально-техническая база»
**Description:** Добавить описание платформы обучения (placeholder).

**Skill:** `do-task`
**Reviewers:** `code-reviewer`
**Files to modify:** `svedeniya-ob-obrazovatelnoy-organizatsii.html`

---

#### Task 2.6: Создать секцию «Контакты и реквизиты»
**Description:** Добавить контакты и полные реквизиты (ИНН, ОГРН, КПП, адрес — placeholder).

**Skill:** `do-task`
**Reviewers:** `code-reviewer`
**Files to modify:** `svedeniya-ob-obrazovatelnoy-organizatsii.html`

---

### Wave 3: Integration & Meta

#### Task 3.1: Скопировать footer и обновить ссылку
**Description:** Скопировать footer из index.html, добавить ссылку на эту страницу в первый столбец.

**Skill:** `do-task`
**Reviewers:** `code-reviewer`
**Files to modify:** `svedeniya-ob-obrazovatelnoy-organizatsii.html`, `index.html` (footer link)
**Files to read:** `index.html` (footer section)

---

#### Task 3.2: Добавить Schema.org микроразметку
**Description:** Добавить JSON-LD с типом CollegeOrUniversity в `<head>`.

**Skill:** `do-task`
**Reviewers:** `code-reviewer`
**Verify-smoke:** `grep -q "CollegeOrUniversity" svedeniya-ob-obrazovatelnoy-organizatsii.html && echo "OK"`
**Files to modify:** `svedeniya-ob-obrazovatelnoy-organizatsii.html`

---

#### Task 3.3: Скопировать JavaScript и глобальные элементы
**Description:** Скопировать progress bar, back-to-top, geometry, scroll animations.

**Skill:** `do-task`
**Reviewers:** `code-reviewer`
**Files to modify:** `svedeniya-ob-obrazovatelnoy-organizatsii.html`
**Files to read:** `index.html` (lines 1100+ for JavaScript)

---

### Wave 4: Polish

#### Task 4.1: Проверить адаптивность
**Description:** Тестировать на mobile, tablet, desktop breakpoints.

**Skill:** `do-task`
**Reviewers:** `none`
**Verify-user:** Open in browser, test responsive behavior
**Files to modify:** `svedeniya-ob-obrazovatelnoy-organizatsii.html` (if needed)

---

#### Task 4.2: Валидация HTML5
**Description:** Проверить валидность HTML через W3C validator.

**Skill:** `do-task`
**Reviewers:** `code-reviewer`
**Verify-smoke:** `curl -F "uploaded_file=@svedeniya-ob-obrazovatelnoy-organizatsii.html" https://validator.w3.org/nu/?out=json | grep -q "errors\":[}0]" && echo "OK"`
**Files to read:** `svedeniya-ob-obrazovatelnoy-organizatsii.html`

---

### Wave 5: Audit

#### Task 5.1: Code Audit
**Description:** Holistic code quality review of all feature code.

**Skill:** `code-reviewing`
**Reviewers:** `none`

---

#### Task 5.2: Security Audit
**Description:** OWASP Top 10 review (CSP, input validation, XSS).

**Skill:** `security-auditor`
**Reviewers:** `none`

---

#### Task 5.3: Test Audit
**Description:** Test quality and coverage review.

**Skill:** `test-master`
**Reviewers:** `none`

---

### Wave 6: Final

#### Task 6.1: QA
**Description:** Acceptance testing: verify all AC from user-spec.

**Skill:** `pre-deploy-qa`
**Reviewers:** `none`
**Verify-user:** Check page on localhost, all sections present, responsive

---

#### Task 6.2: Deploy
**Description:** Commit to git, push to remote.

**Skill:** `deploy-pipeline`
**Reviewers:** `none`

---

## Testing Strategy

### Unit Testing
Не требуется — статический HTML без бизнес-логики

### Integration Testing
Не требуется — нет внешних зависимостей

### Visual Regression
Manual review — проверить consistency с index.html

### Cross-browser Testing
Chrome, Safari, Firefox (latest versions)

### Accessibility Testing
- Semantic HTML
- Alt tags for images
- Keyboard navigation
- Screen reader compatibility (basic)

## Rollout Plan

1. Создать страницу локально
2. Тестировать на localhost
3. Commit в main branch
4. Push в GitHub
5. Verify on live URL (if deployed)

## Rollback Plan
`git revert <commit>` — удалить страницу из репозитория

## Risks & Mitigations

| Risk | Probability | Impact | Mitigation |
|------|-------------|---------|------------|
| Broken links | Low | Low | Verify all links work |
| Inconsistent design | Low | Medium | Use design system components |
| Missing ФЗ-273 requirements | Low | High | Follow user-spec checklist |

## Open Questions
None

## References
- User-spec: `work/about-organization-page/user-spec.md`
- Code research: `work/about-organization-page/code-research.md`
- Design system: `styles.css`, `DESIGN-SYSTEM.md`
