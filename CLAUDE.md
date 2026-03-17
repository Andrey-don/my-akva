# CLAUDE.md — Правила работы с проектом 2akva.ru

Паспорт проекта: [project.md](project.md)
Паспорт (HTML, для печати): [ПАСПОРТ_ПРОЕКТА_2akva.ru.html](ПАСПОРТ_ПРОЕКТА_2akva.ru.html)

---

## Что за проект

Корпоративный WordPress-сайт компании **ООО «2Н АКВА»** — **2akva.ru**.
Тематика: водоподготовка, насосное оборудование, дренажные системы (2H GEOdek).
CMS: WordPress 6.9.4 · Тема: кастомная **2akva** (одна, без дочерней).
Хостинг: **Sweb.ru (SpaceWeb)**, PHP 8.3, MySQL 8.0.
Локальная среда: **http://2akva.local** (Local by Flywheel).
Репозиторий: **Andrey-don/my-akva**, ветка master.
Файлы WP в репо: `site/public_html/`.

---

## Текущее состояние (март 2026)

| Параметр | Статус |
|---|---|
| Сайт на хостинге | ✓ Работает (https://2akva.ru) |
| Сайт локально | ✓ Работает (2akva.local) |
| WordPress 6.9.4 / PHP 8.3 | ✓ Совместимость ✓ |
| Тема 2akva | ✓ Активна |
| HTTPS / SSL | ✓ Работает (Really Simple Security) |
| Почта @2akva.ru (Яндекс 360) | ✓ Работает |
| SMTP с сайта | ✓ Работает (WP Mail SMTP + Spaceweb) |
| SPF / DKIM / DMARC | ✓ Настроено |
| Yoast SEO | ✓ Настроен |
| Site Health | ✓ Хорошо |
| debug.log | ✓ Закрыт (.htaccess) |

---

## Структура репозитория

```
2KVA/
├── site/
│   └── public_html/          # Корень WordPress
│       ├── .htaccess
│       ├── robots.txt
│       ├── wp-config-sample.php
│       └── wp-content/
│           └── themes/
│               └── 2akva/    # Кастомная тема
├── Arhiv/                    # Архивные материалы
├── CLAUDE.md                 # Этот файл
├── project.md                # Паспорт проекта
├── ПАСПОРТ_ПРОЕКТА_2akva.ru.html
├── ТЗ_и_Отчет_2akva.ru.html
└── ТЗ_и_Отчет_2akva.ru.md
```

**НЕ в репозитории:**
- `wp-content/uploads/` — медиафайлы
- `wp-config.php` — учётные данные БД (не коммитить!)
- `wp-content/plugins/` — плагины (не в git)
- `wp-content/cache/`, `languages/`, `upgrade/`

---

## Важные особенности проекта

- **Кастомные поля (ACF + Repeater)** — главная страница использует ACF Repeater для блоков. Не удалять ACF.
- **jQuery 4.0 → 3.7.1** — в `functions.php` есть фильтр, заменяющий jQuery 4.0 на 3.7.1 (CDN). При обновлении темы проверять наличие фильтра.
- **wp-includes/class-wp-query.php** — содержит ручное исправление в строке 756 (`intval()`). При обновлении WordPress нужно вносить правку повторно.
- **Почта Яндекс 360** — MX-запись `mx.yandex.net` (приоритет 10). **НЕ менять!** Все сотрудники используют @2akva.ru через Яндекс 360.
- **CPT** — зарегистрированы два Custom Post Type: `equipment` и `areas_of_use`.
- **wp-config.php** исключён из Git. При переносе создавать вручную.
- **Плагины** не в Git — устанавливать вручную при переносе.

---

## Правила работы AI

- Перед любыми правками в теме — прочитать файл, понять контекст, не менять лишнего
- Не трогать `wp-content/plugins/` без явного запроса
- Не коммитить `wp-config.php` — содержит пароли БД
- **НЕ менять MX-запись домена** — Яндекс 360 для почты сотрудников
- Перед обновлением WordPress — напомнить про правку в `class-wp-query.php` строка 756
- Перед обновлением WordPress или плагинов — напомнить про резервную копию (Duplicator)
- Коммиты с `Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>`
- При любых сомнениях — задавать вопросы, а не принимать решения самостоятельно

---

## Быстрый старт для новой сессии

1. Локальный сервер: запустить **Local WP** → сайт доступен на http://2akva.local
2. Рабочая папка: `C:/Users/profi/Documents/Project/2KVA`
3. Проверить состояние: `git status` и `git log --oneline`
4. Проверить сайт: `curl -s http://2akva.local | head -5`
