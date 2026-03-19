---
created: "2026-03-20"
status: draft
size: M
---
---

# Tech Spec: Обновить index.html по ТЗ

## Architecture

Frontend-only feature. No backend involved.

### Current Structure
- Single HTML file with embedded CSS and JavaScript
- Tailwind CSS via CDN
- Google Fonts via CDN
- No build process or bundler

### Target Structure
- Same: single HTML file approach
- No changes to build tooling or dependencies

## Implementation Tasks

### Wave 1: Foundation Changes

**Task 1: Обновить Hero секцию с фоном эксперта**
- Description: Интегрировать фото эксперта как фон Hero секции, сохранить существующий контент
- Skill: `code-writing`
- Files to modify: `index.html` (Hero section)
- Reviewers: none
- Files to read: `index.html` (Hero section)

**Task 2: Заменить Audience Slider на статичный контент**
- Description: Заменить анимированный слайдер на 3 статичные карточки, сохранить контент
- Skill: `code-writing`
- Files to modify: `index.html` (Slider section)
- Reviewers: none
- Files to read: `index.html` (Slider section)

### Wave 2: Секция «Забронируйте место»

**Task 3: Добавить секцию «Забронируйте место»**
- Description: Создать новую секцию для фиксации скидки и бронирования места с бейджем скидки и датой дедлайна
- Skill: `code-writing`
- Files to modify: `index.html` (insert new section)
- Reviewers: none
- Files to read: `index.html` (structure reference)

**Task 4: Изменить секцию «Практика»**
- Description: Изменить текст на «80% практики на реальных площадках. Вы научитесь, а не просто послушаете»
- Skill: `code-writing`
- Files to modify: `index.html` (Practice section)
- Reviewers: none
- Files to read: `index.html` (Practice section)

**Task 5: Изменить секцию «Трудоустройство»**
- Description: Изменить текст на «Стажировка в реальных компаниях. Возможность трудоустройства в ООО «Фрегат» и ООО «УКЭ»»
- Skill: `code-writing`
- Files to modify: `index.html` (Advantages section)
- Reviewers: none
- Files to read: `index.html` (Advantages section)

### Wave 3: Зарплаты и Обучение

**Task 6: Изменить секцию «Зарплаты»**
- Description: Убрать англицизмы (Junior/Middle/Senior → Начинающий/Специалист/Ведущий специалист), изменить формат на «от 50 000 ₽ + %»
- Skill: `code-writing`
- Files to modify: `index.html` (Salary section)
- Reviewers: none
- Files to read: `index.html` (Salary section)

**Task 7: Изменить секцию «Как проходит обучение»**
- Description: Удалить «Тестирование», добавить 2-й блок программы, добавить «Практические задания с проверкой и обратной связью от эксперта», заменить «Диплом» на «Удостоверение о повышении квалификации» и «Сертификат»
- Skill: `code-writing`
- Files to modify: `index.html` (How it works section)
- Reviewers: none
- Files to read: `index.html` (How it works section)

### Wave 4: Новые секции

**Task 8: Добавить секцию «Ближайший набор»**
- Description: Создать новую секцию с датой «1 мая 2026 г.» и CTA кнопкой
- Skill: `code-writing`
- Files to modify: `index.html` (insert new section)
- Reviewers: none
- Files to read: `index.html` (structure reference)

**Task 9: Заменить Pricing на Абонементы**
- Description: Заменить существующую секцию Pricing (2 тарифа) на Абонементы (3 тарифа по конкуренту https://глав-тендер.рф/, блок «Нужна помощь на работе?»)
- Skill: `code-writing`
- Files to modify: `index.html` (Pricing section)
- Reviewers: none
- Files to read: `index.html` (Pricing section)

**Task 10: Расширить FAQ до 14 вопросов**
- Description: Добавить 11 новых вопросов (взять с конкурента https://niidpo.ru/seminar/specialist-v-sfere-zakupok-340-chasov и переписать под себя)
- Skill: `code-writing`
- Files to modify: `index.html` (FAQ section)
- Reviewers: none
- Files to read: `index.html` (FAQ section)

**Task 11: Добавить блок «Преподаватели»**
- Description: Добавить 2-3 преподавателя с фото, ФИО, должностью, опытом, био (заглушки)
- Skill: `code-writing`
- Files to modify: `index.html` (insert new section)
- Reviewers: none
- Files to read: `index.html` (structure reference)

### Wave 5: Финальные правки

**Task 12: Исправить номер лицензии**
- Description: Заменить все упоминания лицензии на `Л035‑01217‑26/03829175`
- Skill: `code-writing`
- Files to modify: `index.html` (all occurrences)
- Reviewers: `security-auditor`
- Files to read: `index.html`

**Task 13: Исправить мета-тег description и добавить CSP**
- Description: Заменить на «Удостоверение о повышении квалификации и сертификат», добавить CSP meta-тег (разрешить script-src: 'self', connect-src: 'self' https://cdn.tailwindcss.com https://fonts.googleapis.com')
- Skill: `code-writing`
- Files to modify: `index.html` (head section)
- Reviewers: `security-auditor`
- Files to read: `index.html` (head section)

**Task 14: Удалить форму CTA**
- Description: Удалить инпуты (имя, телефон, email), оставить только кнопку с текстом «Откроется квиз»
- Skill: `code-writing`
- Files to modify: `index.html` (Final CTA section)
- Reviewers: none
- Files to read: `index.html` (Final CTA section)

**Task 15: Удалить самостоятельную секцию Expert Block**
- Description: Удалить самостоятельную секцию (контент уже интегрирован в Hero)
- Skill: `code-writing`
- Files to modify: `index.html` (Expert Block section)
- Reviewers: none
- Files to read: `index.html`

### Wave 6: Audit Wave

**Task 16: Code Audit**
- Description: Holistic code quality review of all feature changes
- Skill: `code-reviewing`
- Files to read: `index.html` (modified sections)
- Reviewers: none

**Task 17: Security Audit**
- Description: OWASP Top 10 review across all modified sections, проверка: инъекции (XSS, HTML injection), аутентификация, шифрование данных
- Skill: `security-auditor`
- Files to read: `index.html` (all sections)
- Reviewers: none

**Task 18: Test Audit**
- Description: Test quality and coverage across all modified sections
- Skill: `test-master`
- Files to read: `index.html` (all sections)
- Reviewers: none

### Wave 7: Final Wave

**Task 19: QA**
- Description: Acceptance testing: verify all acceptance criteria from user-spec, test on mobile and desktop
- Skill: `pre-deploy-qa`
- Files to read: `index.html` (all sections)
- Verify-user: Open index.html in browser, verify readability, check responsive behavior

**Task 20: Verify mobile priority**
- Description: Specifically verify mobile version loads quickly, all text is readable
- Skill: `pre-deploy-qa`
- Files to read: `index.html` (all sections)
- Verify-user: Open in mobile browser or use dev tools mobile view

**Task 21: Verify section order**
- Description: Verify sections follow required order: Hero → Забронируйте место → Практика → Advantages → Slider (статичный) → Зарплаты → Как проходит обучение → Программа → Абонементы → Преподаватели → Ближайший набор → FAQ → Footer
- Skill: `pre-deploy-qa`
- Files to read: `index.html` (all sections)
- Verify-user: Visual check in browser

**Task 22: Verify placeholder content**
- Description: Verify all values (dates, prices, discounts, tariff content, FAQ texts) are placeholders, not hardcoded real data
- Skill: `pre-deploy-qa`
- Files to read: `index.html` (all new/modified sections)
- Verify-user: Manual check

## Decisions

### Decision 1: Использование существующего фото эксперта
- Chosen approach: Использовать существующее фото из кода (Unsplash) для фона Hero
- Rationale: Фото уже есть в проекте, нет необходимости просить заказчика о новом изображении

### Decision 2: Статичный контент вместо Slider
- Chosen approach: Заменить анимированный слайдер на 3 статичные карточки
- Rationale: Требование заказчика, упрощает код и улучшает UX на мобильных

### Decision 3: Дата «Ближайший набор» как статичная заглушка
- Chosen approach: Использовать статичную дату «1 мая 2026 г.» (это заглушка, будет заменена на Фазе 2 при переносе на WordPress)
- Rationale: Это статический сайт (Фаза 1), динамические даты невозможны без backend

### Decision 4: Контент для новых секций
- Chosen approach: Использовать заглушки с плейсхолдерами для всех значений (даты, цены, скидки, тарифы, FAQ)
- Rationale: Требование пользователя, контент будет меняться на Фазе 2 (WordPress)

### Decision 5: Порядок секций
- Chosen approach: Следовать порядку из ТЗ: Hero → Забронируйте место → Практика → Advantages → Slider (статичный) → Зарплаты → Как проходит обучение → Программа → Абонементы → Преподаватели → Ближайший набор → FAQ → Footer
- Rationale: Соответствует требованиям ТЗ

## Shared Resources

None (static HTML file, no external resources shared across components)

## Testing Strategy

### Testing Level
Size: Medium → moderate depth testing strategy

### Scope
- Acceptance testing: verify all acceptance criteria
- Responsive testing: desktop and mobile
- Manual verification: open in browser, check readability

### No automated testing required
- No unit tests (HTML/CSS changes only)
- No E2E tests (manual verification by user)
- No API integration tests (no backend)

## Dependencies

### External
- Tailwind CSS CDN: `https://cdn.tailwindcss.com`
- Google Fonts: Inter, Playfair Display
- Unsplash image: `https://images.unsplash.com/photo-1573496359142-b8d87734a5a2?ixlib=rb-1.2.1&auto=format&fit=crop&w=600&q=80`

### Local
- `index.html` — source file
- `tailwind.js` — не используется (CDN)

### No additional dependencies required
- No npm packages
- No build tools
- No bundlers
